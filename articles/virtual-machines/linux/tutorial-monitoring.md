---
title: "Azure에서 Linux 가상 컴퓨터 aaaMonitor | Microsoft Docs"
description: "Toomonitor Azure에서 Linux 가상 컴퓨터에서 진단 및 성능 메트릭을 확인을 부팅 방법에 대해 알아봅니다"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 282da0f03ab0bf37bd44750c22813ca8d1c89560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-a-linux-virtual-machine-in-azure"></a>어떻게 toomonitor Azure에서 Linux 가상 컴퓨터

Azure에서 가상 컴퓨터 (Vm)는 올바르게 실행 되는 tooensure, 부트 진단 및 성능 메트릭을 확인을 검토할 수 있습니다. 이 자습서에서는 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * Hello VM에 대 한 부트 진단 유틸리티를 사용 하도록 설정
> * 부트 진단 보기
> * 호스트 메트릭 보기
> * Hello VM에 진단 확장을 사용 하도록 설정
> * VM 메트릭 보기
> * 진단 메트릭을 기반으로 하는 알림 만들기
> * 고급 모니터링 설정


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 자습서를 사용 하려면 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 이상. 실행 `az --version` toofind hello 버전입니다. Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다. 

## <a name="create-vm"></a>VM 만들기

toosee 진단 및 작업에 따라 메트릭을 VM 해야합니다. 먼저 [az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다. hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroupMonitor* hello에 *eastus* 위치 합니다.

```azurecli-interactive 
az group create --name myResourceGroupMonitor --location eastus
```

이제 [az vm create](https://docs.microsoft.com/cli/azure/vm#create)로 VM을 만듭니다. hello 다음 예제에서는 V *myVM*:

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys
```

## <a name="enable-boot-diagnostics"></a>부팅 진단을 사용하도록 설정

Linux Vm의 경우 부팅 하는 대로 hello 부트 진단 확장 부팅 출력을 캡처하여이 Azure 저장소에 저장 합니다. 이 데이터에 사용 되는 tootroubleshoot VM 부팅 문제 수 있습니다. 부트 진단이 hello Azure CLI를 사용 하 여 Linux VM을 만들 때 자동으로 활성화 되지 않습니다.

부트 진단이를 활성화 하기 전에 저장소 계정에는 부팅 로그를 저장 하기 위해 만든 toobe가 필요 합니다. 저장소 계정은 전역적으로 고유한 이름을 가져야 하며, 3-24자 사이의 숫자와 소문자만 포함해야 합니다. Hello로 저장소 계정을 만드는 [az 저장소 계정에 create](/cli/azure/storage/account#create) 명령입니다. 이 예제에서는 임의 문자열은 사용 되는 toocreate 고유한 저장소 계정 이름 

```azurecli-interactive 
storageacct=mydiagdata$RANDOM

az storage account create \
  --resource-group myResourceGroupMonitor \
  --name $storageacct \
  --sku Standard_LRS \
  --location eastus
```

부트 진단이를 설정할 경우 hello URI toohello blob 저장소 컨테이너 필요 합니다. hello 명령 쿼리인 hello 저장소 계정 tooreturn이이 URI입니다. hello URI 값 변수 이름에 저장 됩니다 *bloburi*, hello 다음 단계에 사용 됩니다.

```azurecli-interactive 
bloburi=$(az storage account show --resource-group myResourceGroupMonitor --name $storageacct --query 'primaryEndpoints.blob' -o tsv)
```

이제 [az vm boot-diagnostics enable](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable)을 사용하여 부팅 진단을 사용하도록 설정합니다. hello `--storage` hello 이전 단계에 값이 hello blob URI를 수집 합니다.

```azurecli-interactive 
az vm boot-diagnostics enable \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --storage $bloburi
```


## <a name="view-boot-diagnostics"></a>부트 진단 보기

부트 진단이 설정 되 면 중지 하 고 hello VM을 시작할 때마다 hello 부팅 프로세스에 대 한 정보는 기록 tooa 로그 파일. 이 예에서는 먼저 할당을 취소 hello로 VM hello [az vm 할당을 취소](/cli/azure/vm#deallocate) 다음과 같이 명령:

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupMonitor --name myVM
```

이제 VM hello hello로 시작 [az vm 시작]( /cli/azure/vm#stop) 명령은 다음과 같습니다.

```azurecli-interactive 
az vm start --resource-group myResourceGroupMonitor --name myVM
```

Hello에 대 한 부트 진단 데이터를 가져올 수 있습니다 *myVM* hello로 [az vm 부팅 진단 get-부팅-로그](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) 명령은 다음과 같습니다.

```azurecli-interactive 
az vm boot-diagnostics get-boot-log --resource-group myResourceGroupMonitor --name myVM
```


## <a name="view-host-metrics"></a>호스트 메트릭 보기

Linux VM에는 Azure에서 상호 작용하는 전용 호스트가 있습니다. 메트릭은 hello 호스트에 대 한 자동으로 수집 되며 다음과 같이 hello Azure 포털에서에서 볼 수 있습니다.

1. Hello Azure 포털에서에서 클릭 **리소스 그룹**선택, **myResourceGroupMonitor**를 선택한 후 **myVM** hello 리소스 목록에 합니다.
1. toosee hello 호스트 VM을 수행 하는 방법을 클릭 **메트릭** hello VM 블레이드에서 다음 중 하나를 선택 hello *[호스트]* 에서 메트릭 **사용 가능한 메트릭**합니다.

    ![호스트 메트릭 보기](./media/tutorial-monitoring/monitor-host-metrics.png)


## <a name="install-diagnostics-extension"></a>진단 확장 설치

> [!IMPORTANT]
> 이 문서에서는 버전 2.3의 hello Linux 진단 확장을 사용 되지 않습니다. 버전 2.3은 2018년 6월 30일까지 지원됩니다.
>
> Hello Linux 진단 확장의 버전 3.0을 대신 사용할 수 있습니다. 자세한 내용은 참조 [설명서 hello](./diagnostic-extension.md)합니다.

hello 기본 호스트 메트릭을 사용할 수 있는 보다 세부적인 toosee 있고 VM 관련 메트릭, 있습니다 tooneed tooinstall hello Azure 진단 확장을 hello VM입니다. hello Azure 진단 확장 추가 모니터링 및 진단 데이터 toobe hello VM에서에서 검색을 허용 합니다. 이러한 성능 메트릭을 보고 하 고 hello VM 수행 하는 방법을 기반으로 경고를 만들 수 있습니다. hello 진단 확장 다음과 같이 hello Azure 포털을 통해 설치 됩니다.

1. Hello Azure 포털에서에서 클릭 **리소스 그룹**선택, **myResourceGroup**를 선택한 후 **myVM** hello 리소스 목록에 합니다.
1. **진단 설정**을 클릭합니다. hello 목록에 표시 하는 *진단 부팅* hello 이전 단원에서 이미 사용 하도록 설정 합니다. Hello에 대 한 확인란을 클릭 *기본 메트릭*합니다.
1. Hello에 *저장소 계정* 섹션에서 tooand 선택 hello 찾아보기 *mydiagdata [1234]* hello 이전 섹션에서 만든 계정.
1. Hello 클릭 **저장** 단추입니다.

    ![진단 메트릭 보기](./media/tutorial-monitoring/enable-diagnostics-extension.png)


## <a name="view-vm-metrics"></a>VM 메트릭 보기

Hello hello VM 메트릭을 볼 수 있습니다 동일한 방식으로 hello 호스트 VM 메트릭을 보았습니다.

1. Hello Azure 포털에서에서 클릭 **리소스 그룹**선택, **myResourceGroup**를 선택한 후 **myVM** hello 리소스 목록에 합니다.
1. toosee hello VM을 수행 하는 방법을 클릭 **메트릭** VM 블레이드 hello 되 고 아래 hello 진단 메트릭 중 하나를 선택 **사용 가능한 메트릭**합니다.

    ![VM 메트릭 보기](./media/tutorial-monitoring/monitor-vm-metrics.png)


## <a name="create-alerts"></a>경고 만들기

특정 성능 메트릭을 기반으로 하는 경고를 만들 수 있습니다. 경고에는 예를 들어 사용된 toonotify 평균 CPU 사용률이 특정 임계값 또는 사용 가능한 디스크 공간을 초과 하는 일정량 아래로 떨어질 수 있습니다. 경고나 hello Azure 포털에에서 표시 되는 전자 메일을 통해 보낼 수 있습니다. 또한 Azure 자동화 runbook 또는 Azure 논리 앱에서 생성 되 고 응답 tooalerts 트리거할 수 있습니다.

hello 다음 예제에서는 평균 CPU 사용량에 대 한 경고

1. Hello Azure 포털에서에서 클릭 **리소스 그룹**선택, **myResourceGroup**를 선택한 후 **myVM** hello 리소스 목록에 합니다.
2. 클릭 **규칙 경고** hello VM 블레이드에서 클릭 **추가 메트릭 경고** hello 경고 블레이드의 hello 위쪽 합니다.
4. *myAlertRule*과 같이 경고에 대한 **이름**을 입력합니다.
5. tootrigger CPU 백분율을 5 분 동안 1.0을 초과할 때 경고 모든 hello 선택한 다른 기본값을 그대로 둡니다.
6. 필요에 따라 확인란 hello에 대 한 *소유자, 참가자 및 독자를 전자 메일로 보내기* toosend 전자 메일 알림입니다. hello 기본 동작은 toopresent hello 포털의 알림입니다.
7. Hello 클릭 **확인** 단추입니다.


## <a name="advanced-monitoring"></a>고급 모니터링 

[Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview)를 사용하여 VM에 대한 고급 모니터링을 수행할 수 있습니다. 아직 사용해 보지 않았으면 Operations Management Suite의 [평가판](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial)에 등록할 수 있습니다.

액세스 toohello OMS 포털을 사용 하는 경우에 hello 설정 블레이드에서 hello 작업 영역 키 및 작업 영역 id를 찾을 수 있습니다. Replace < 작업 영역 키 > 및 < 작업 영역 id > OMS에 대 한 hello 값으로 작업 영역 및 다음 צ ְ ײ **az vm 확장 집합** tooadd hello OMS 확장 toohello VM:

```azurecli-interactive 
az vm extension set \
  --resource-group myResourceGroupMonitor \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.3 \
  --protected-settings '{"workspaceKey": "<workspace-key>"}' \
  --settings '{"workspaceId": "<workspace-id>"}'
```

Hello OMS 포털의 로그 검색 블레이드에서 hello 나타납니다 *myVM* 같은 hello 다음 그림에에서 표시 되는 내용:

![OMS 블레이드](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a>다음 단계

이 자습서에서는 Azure Security Center를 사용하여 VM을 구성하고 검토했습니다. 다음 방법에 대해 알아보았습니다.

> [!div class="checklist"]
> * Hello VM에 대 한 부트 진단 유틸리티를 사용 하도록 설정
> * 부트 진단 보기
> * 호스트 메트릭 보기
> * Hello VM에 진단 확장을 사용 하도록 설정
> * VM 메트릭 보기
> * 진단 메트릭을 기반으로 하는 알림 만들기
> * 고급 모니터링 설정

Azure 보안 센터에 대 한 다음 자습서 toolearn toohello를 진행 합니다.

> [!div class="nextstepaction"]
> [VM 보안 관리](./tutorial-azure-security.md)