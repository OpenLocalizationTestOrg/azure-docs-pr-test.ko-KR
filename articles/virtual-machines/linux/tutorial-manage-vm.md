---
title: "Linux Vm을 관리 하 고 aaaCreate hello Azure CLI | Microsoft Docs"
description: "자습서에서 만들고 있는 Linux Vm 관리 hello Azure CLI"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 05f7c1cf860f809bc13f110778d3bddd619ac6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-linux-vms-with-hello-azure-cli"></a>만들고 있는 Linux Vm 관리 hello Azure CLI

Azure 가상 컴퓨터는 완전히 구성 가능하고 유연한 컴퓨팅 환경을 제공합니다. 이 자습서에서는 VM 크기 선택, VM 이미지 선택 및 VM 배포 등 기본적인 Azure Virtual Machines 배포 항목에 대해 설명합니다. 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * 만들고 tooa VM 연결
> * VM 이미지 선택 및 사용
> * 특정 VM 크기 보기 및 사용
> * VM 크기 조정
> * VM 상태 보기 및 이해


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 자습서를 사용 하려면 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 이상. 실행 `az --version` toofind hello 버전입니다. Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다. 

## <a name="create-resource-group"></a>리소스 그룹 만들기

Hello로 리소스 그룹 만들기 [az 그룹 만들기](https://docs.microsoft.com/cli/azure/group#create) 명령입니다. 

Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다. 가상 컴퓨터보다 먼저 리소스 그룹을 만들어야 합니다. 이 예제에서는 리소스 그룹 이름이 *myResourceGroupVM* hello에서 만든 *eastus* 영역입니다. 

```azurecli-interactive 
az group create --name myResourceGroupVM --location eastus
```

hello 리소스 그룹은 생성 하거나이 자습서 전체에서 볼 수 있는 VM을 수정할 때 지정 됩니다.

## <a name="create-virtual-machine"></a>가상 컴퓨터 만들기

Hello로 가상 컴퓨터를 만들 [az vm 만들기](https://docs.microsoft.com/cli/azure/vm#create) 명령입니다. 

가상 컴퓨터를 만들 때 운영 체제 이미지, 디스크 크기 조정 및 관리 자격 증명 등의 몇 가지 옵션을 사용할 수 있습니다. 이 예제에서는 Ubuntu Server를 실행하는 *myVM*이라는 가상 컴퓨터를 만듭니다. 

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM --image UbuntuLTS --generate-ssh-keys
```

한 번 VM을 만든 hello, hello Azure CLI hello VM에 대 한 정보를 출력 합니다. Hello를 메모해 `publicIpAddress`,이 주소에서 사용 되는 tooaccess hello 가상 컴퓨터를 수 있습니다. 

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroupVM/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.174.34.95",
  "resourceGroup": "myResourceGroupVM"
}
```

## <a name="connect-toovm"></a>TooVM 연결

연결할 수 있습니다. VM toohello SSH를 사용 하 여 합니다. Hello로 hello 예제 IP 주소를 교체 `publicIpAddress` hello 이전 단계에서 설명 합니다.

```bash
ssh 52.174.34.95
```

VM hello로 완료 되 면 hello SSH 세션을 닫습니다. 

```bash
exit
```

## <a name="understand-vm-images"></a>VM 이미지 이해

hello Azure 마켓플레이스 사용된 toocreate Vm 수 있는 여러 이미지를 포함 합니다. Hello 이전 단계에서 Ubuntu 이미지를 사용 하 여 가상 컴퓨터를 만든 합니다. 이 단계에서는 Azure CLI는 CentOS 이미지의 경우이 사용 하는 toosearch hello 마켓플레이스는 hello toodeploy 두 번째 가상 컴퓨터를 사용 합니다.  

hello 목록이 toosee 가장 일반적으로 사용 되는 이미지, hello를 사용 하 여 [az vm 이미지 목록을](/cli/azure/vm/image#list) 명령입니다.

```azurecli-interactive 
az vm image list --output table
```

Azure의 hello 가장 인기 있는 VM 이미지를 반환 하는 hello 명령 출력 합니다.

```bash
Offer          Publisher               Sku                 Urn                                                             UrnAlias             Version
-------------  ----------------------  ------------------  --------------------------------------------------------------  -------------------  ---------
WindowsServer  MicrosoftWindowsServer  2016-Datacenter     MicrosoftWindowsServer:WindowsServer:2016-Datacenter:latest     Win2016Datacenter    latest
WindowsServer  MicrosoftWindowsServer  2012-R2-Datacenter  MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest  Win2012R2Datacenter  latest
WindowsServer  MicrosoftWindowsServer  2008-R2-SP1         MicrosoftWindowsServer:WindowsServer:2008-R2-SP1:latest         Win2008R2SP1         latest
WindowsServer  MicrosoftWindowsServer  2012-Datacenter     MicrosoftWindowsServer:WindowsServer:2012-Datacenter:latest     Win2012Datacenter    latest
UbuntuServer   Canonical               16.04-LTS           Canonical:UbuntuServer:16.04-LTS:latest                         UbuntuLTS            latest
CentOS         OpenLogic               7.3                 OpenLogic:CentOS:7.3:latest                                     CentOS               latest
openSUSE-Leap  SUSE                    42.2                SUSE:openSUSE-Leap:42.2:latest                                  openSUSE-Leap        latest
RHEL           RedHat                  7.3                 RedHat:RHEL:7.3:latest                                          RHEL                 latest
SLES           SUSE                    12-SP2              SUSE:SLES:12-SP2:latest                                         SLES                 latest
Debian         credativ                8                   credativ:Debian:8:latest                                        Debian               latest
CoreOS         CoreOS                  Stable              CoreOS:CoreOS:Stable:latest                                     CoreOS               latest
```

Hello를 추가 하 여 전체 목록을 볼 수 있습니다 `--all` 인수입니다. hello 이미지 목록에서 필터링 할 수도 있습니다 `--publisher` 또는 `–-offer`합니다. 이 예제에서는 일치 하는 제공 된 모든 이미지에 대 한 hello 목록 필터링 *CentOS*합니다. 

```azurecli-interactive 
az vm image list --offer CentOS --all --output table
```

부분 출력:

```azurecli-interactive 
Offer             Publisher         Sku   Urn                                     Version
----------------  ----------------  ----  --------------------------------------  -----------
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201501         6.5.201501
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201503         6.5.201503
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201506         6.5.201506
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20150904       6.5.20150904
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20160309       6.5.20160309
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20170207       6.5.20170207
```

특정 이미지를 사용 하는 VM toodeploy hello 값에서에서 기록해 hello *Urn* 열입니다. Hello 이미지를 지정할 때는 hello 이미지 버전 번호 수로 바뀝니다 "최신" hello hello 분포의 최신 버전을 선택 하는. 이 예제에서는 hello `--image` 인수는 사용 되는 toospecify hello CentOS 6.5 이미지의 최신 버전입니다.  

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM2 --image OpenLogic:CentOS:6.5:latest --generate-ssh-keys
```

## <a name="understand-vm-sizes"></a>VM 크기 이해

가상 컴퓨터 크기는 hello 양의 toohello 사용 가능한 가상 컴퓨터에 적용 된 메모리, CPU 및 GPU, 등 계산 리소스를 결정 합니다. 가상 컴퓨터 작업 부하 예상 hello에 대 한 크기가 적합 toobe를 해야 합니다. 워크로드가 증가할 경우 기존 가상 컴퓨터의 크기를 조정할 수 있습니다.

### <a name="vm-sizes"></a>VM 크기

다음 표에서 hello 사용 사례에 크기를 분류 합니다.  

| 형식                     | 크기           |    설명       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [범용](sizes-general.md)         |Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7| CPU 대 메모리 비율이 적당합니다. 개발에 대 한 이상적인 / 테스트 및 소규모 toomedium 응용 프로그램 및 데이터 솔루션입니다.  |
| [Compute에 최적화](sizes-compute.md)   | Fs, F             | CPU 대 메모리 비율이 높습니다. 트래픽이 중간 정도인 응용 프로그램, 네트워크 어플라이언스 및 일괄 처리 프로세스에 적합합니다.        |
| [메모리에 최적화](../virtual-machines-windows-sizes-memory.md)    | Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D   | 메모리 대 코어 비율이 높습니다. 관계형 데이터베이스, 중간 toolarge 캐시 및 메모리 내 분석에 매우 유용 합니다.                 |
| [Storage에 최적화](../virtual-machines-windows-sizes-storage.md)      | Ls                | 높은 디스크 처리량 및 IO 빅 데이터, SQL, NoSQL 데이터베이스에 적합합니다.                                                         |
| [GPU](sizes-gpu.md)          | NV, NC            | 대량의 그래픽 렌더링 및 비디오 편집에 적합한 전문 VM입니다.       |
| [고성능](sizes-hpc.md) | H, A8-11          | 당사의 가장 강력한 CPU VM으로, 필요한 경우 처리량이 높은 네트워크 인터페이스(RDMA)도 제공합니다. 


### <a name="find-available-vm-sizes"></a>사용 가능한 VM 크기 찾기

특정 지역에 toosee VM 목록을 사용할 수 있는 크기, hello를 사용 하 여 [az vm 목록 크기](/cli/azure/vm#list-sizes) 명령입니다. 

```azurecli-interactive 
az vm list-sizes --location eastus --output table
```

부분 출력:

```azurecli-interactive 
  MaxDataDiskCount    MemoryInMb  Name                      NumberOfCores    OsDiskSizeInMb    ResourceDiskSizeInMb
------------------  ------------  ----------------------  ---------------  ----------------  ----------------------
                 2          3584  Standard_DS1                          1           1047552                    7168
                 4          7168  Standard_DS2                          2           1047552                   14336
                 8         14336  Standard_DS3                          4           1047552                   28672
                16         28672  Standard_DS4                          8           1047552                   57344
                 4         14336  Standard_DS11                         2           1047552                   28672
                 8         28672  Standard_DS12                         4           1047552                   57344
                16         57344  Standard_DS13                         8           1047552                  114688
                32        114688  Standard_DS14                        16           1047552                  229376
                 1           768  Standard_A0                           1           1047552                   20480
                 2          1792  Standard_A1                           1           1047552                   71680
                 4          3584  Standard_A2                           2           1047552                  138240
                 8          7168  Standard_A3                           4           1047552                  291840
                 4         14336  Standard_A5                           2           1047552                  138240
                16         14336  Standard_A4                           8           1047552                  619520
                 8         28672  Standard_A6                           4           1047552                  291840
                16         57344  Standard_A7                           8           1047552                  619520
```

### <a name="create-vm-with-specific-size"></a>특정 크기로 VM 만들기

앞의 예에서 hello VM 만들기, 크기를 제공 하지 않았습니다, 결과적 기본 크기. VM 크기를 사용 하 여 만들 때 선택할 수 있습니다 [az vm 만들기](/cli/azure/vm#create) 및 hello `--size` 인수입니다. 

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupVM \
    --name myVM3 \
    --image UbuntuLTS \
    --size Standard_F4s \
    --generate-ssh-keys
```

### <a name="resize-a-vm"></a>VM 크기 조정

VM을 배포한 후 크기가 조정 된 tooincrease 하거나 이동할 수 있습니다 리소스 할당을 줄입니다.

VM의 크기를 조정 하기 전에 hello 원하는 크기는 hello 현재 Azure 클러스터에서 사용할 수 있는 경우를 확인 합니다. hello [az vm 목록-vm-크기 조정-옵션](/cli/azure/vm#list-vm-resize-options) 명령 반환 hello 크기의 목록입니다. 

```azurecli-interactive 
az vm list-vm-resize-options --resource-group myResourceGroupVM --name myVM --query [].name
```
Hello 원하는 크기는 사용할 수 있는 경우 hello VM 크기를 조정할 수 전원이 켜진 상태에서 있지만 hello 작업 동안 다시 부팅 합니다. 사용 하 여 hello [az vm 크기를 조정]( /cli/azure/vm#resize) 명령 tooperform hello 크기 조정 합니다.

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_DS4_v2
```

Hello 크기를 원하는 경우에 없습니다 hello 현재 클러스터에 VM hello 요구 hello 크기 조정 작업 전에 할당 취소 toobe 발생할 수 있습니다. 사용 하 여 hello [az vm 할당을 취소]( /cli/azure/vm#deallocate) toostop 명령 및 hello VM 할당을 취소 합니다. 참고 때 hello VM의 전원이 켜져 다시, hello 임시 디스크의 모든 데이터가 제거 될 수 있습니다. hello 공용 IP 주소는 고정 IP 주소를 사용 하는 하지 않는 경우에 변경 됩니다. 

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupVM --name myVM
```

할당이 취소 되 면 hello 크기 조정 발생할 수 있습니다. 

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_GS1
```

Hello, 크기 조정 hello VM을 시작할 수 있습니다.

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

## <a name="vm-power-states"></a>VM 전원 상태

Azure VM의 전원 상태는 여러 상태 중 하나일 수 있습니다. 이 상태를 hello 하이퍼바이저의 hello 관점에서 hello hello VM의 현재 상태를 나타냅니다. 

### <a name="power-states"></a>전원 상태

| 전원 상태 | 설명
|----|----|
| 시작 중 | Hello 가상 컴퓨터가 시작 되 고 나타냅니다. |
| 실행 중 | Hello 가상 컴퓨터 실행 중임을 나타냅니다. |
| 중지 중 | Hello 가상 컴퓨터를 중지 하 고 나타냅니다. | 
| 중지됨 | Hello 가상 컴퓨터 중지 되었음을 나타냅니다. Hello 중지 상태의 가상 컴퓨터 계산 비용이 계속 청구 됩니다.  |
| 할당 취소 중 | Hello 가상 컴퓨터를 할당 취소 되 고이 나타냅니다. |
| 할당 취소됨 | Hello 가상 컴퓨터는 hello 하이퍼바이저에서 제거 되지만 hello 제어 평면에서 여전히 사용할 수를 나타냅니다. Hello 할당 취소 됨 상태에서에서 가상 컴퓨터 계산 비용이 발생 하지 않습니다. |
| - | Hello 가상 컴퓨터의 전원 상태 hello 알려진 임을 나타냅니다. |

### <a name="find-power-state"></a>전원 상태 찾기

특정 VM 사용 하 여 hello의 tooretrieve hello 상태 [az vm 인스턴스 뷰 가져오기](/cli/azure/vm#get-instance-view) 명령입니다. 있는지 toospecify 가상 컴퓨터 및 리소스 그룹에 대 한 올바른 이름 이어야 합니다. 

```azurecli-interactive 
az vm get-instance-view \
    --name myVM \
    --resource-group myResourceGroupVM \
    --query instanceView.statuses[1] --output table
```

출력:

```azurecli-interactive 
ode                DisplayStatus    Level
------------------  ---------------  -------
PowerState/running  VM running       Info
```

## <a name="management-tasks"></a>관리 작업

Hello-주기 동안 가상 컴퓨터를 시작, 중지, 또는 가상 컴퓨터를 삭제 하는 등의 toorun 관리 작업을 할 수 있습니다. 또한 toocreate 스크립트 tooautomate 반복적 복잡 한 작업을 지정할 수 있습니다. Hello Azure CLI를 사용 하 여 여러 가지 일반적인 관리 작업 또는 실행할 수 있는 hello 명령줄에서 스크립트에 있습니다. 

### <a name="get-ip-address"></a>IP 주소 가져오기

이 명령은 가상 컴퓨터의 hello 개인 및 공용 IP 주소를 반환합니다.  

```azurecli-interactive 
az vm list-ip-addresses --resource-group myResourceGroupVM --name myVM --output table
```

### <a name="stop-virtual-machine"></a>가상 컴퓨터 중지

```azurecli-interactive 
az vm stop --resource-group myResourceGroupVM --name myVM
```

### <a name="start-virtual-machine"></a>가상 컴퓨터 시작

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

### <a name="delete-resource-group"></a>리소스 그룹 삭제

리소스 그룹을 삭제하면 그 안에 포함된 리소스도 모두 삭제됩니다.

```azurecli-interactive 
az group delete --name myResourceGroupVM --no-wait --yes
```

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음 방법과 같이 기본 VM을 만들고 관리하는 방법에 대해 알아보았습니다.

> [!div class="checklist"]
> * 만들고 tooa VM 연결
> * VM 이미지 선택 및 사용
> * 특정 VM 크기 보기 및 사용
> * VM 크기 조정
> * VM 상태 보기 및 이해

VM 디스크에 대 한 다음 자습서 toolearn toohello를 진행 합니다.  

> [!div class="nextstepaction"]
> [VM 디스크 만들기 및 관리](./tutorial-manage-disks.md)
