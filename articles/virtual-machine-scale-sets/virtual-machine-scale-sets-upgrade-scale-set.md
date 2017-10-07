---
title: "aaaUpgrade Azure 가상 컴퓨터 크기 집합 | Microsoft Docs"
description: "Azure 가상 컴퓨터 확장 집합 업그레이드"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e229664e-ee4e-4f12-9d2e-a4f456989e5d
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: guybo
ms.openlocfilehash: 068e98503f8d37ea71e45b8673a01da2e814f521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-virtual-machine-scale-set"></a>가상 컴퓨터 확장 집합 업그레이드
이 문서는 OS 업데이트 tooan Azure 가상 컴퓨터 크기 집합 가동 중지 시간 없이 롤아웃할 수는 방법을 설명 합니다. 이 컨텍스트에서에서 OS 업데이트 하려면 hello 사용자 지정 이미지의 URI를 변경 하거나 hello 버전 또는 hello OS의 SKU를 변경 합니다. 가동 중지 시간 없이 업데이트한다는 것은 가상 컴퓨터를 모두 한꺼번에 업데이트하지 않고 한 번에 하나씩 또는 그룹으로(예" 한 번에 하나의 장애 도메인) 업데이트하는 것을 의미합니다. 이렇게 하면 업그레이드되지 않는 모든 가상 컴퓨터를 계속 실행할 수 있습니다.

tooavoid 모호성을 보겠습니다 네 가지 유형의 할 수 있습니다는 OS 업데이트를 구분할 tooperform:

* Hello 버전 또는 플랫폼 이미지의 SKU를 변경 합니다. 예를 들어, Ubuntu 변경 14.04.201506100에서 14.04.2-LTS 버전 too14.04.201507060, 또는 hello Ubuntu 15.10/가장 늦은 SKU too16.04.0-LTS/latest 변경 합니다. 이 시나리오는 이 문서에서 설명합니다.
* 사용자 지정 이미지를 빌드한 tooa 새 버전을 가리키는 URI를 hello 변경 (**속성** > **virtualMachineProfile** > **storageProfile**  >  **osDisk** > **이미지** > **uri**). 이 시나리오는 이 문서에서 설명합니다.
* Azure 관리 되는 디스크를 사용 하 여 만든 크기 집합의 hello 이미지 참조를 변경 합니다.
* 가상 컴퓨터 내에서 OS hello 패치 (이 예에서는 보안 패치를 설치 하 고 Windows 업데이트 실행을 포함 하는 데 사용). 이 시나리오는 지원되지만 이 문서에서는 다루지 않습니다.

[Azure 서비스 패브릭](https://azure.microsoft.com/services/service-fabric/) 클러스터의 일부로 배포되는 가상 컴퓨터 크기 집합은 여기에서 다루지 않습니다. 서비스 패브릭 패치에 대한 자세한 내용은 [Service Fabric 클러스터에서 Windows OS 패치](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application)를 참조하세요.

hello 기본 시퀀스 변경에 대 한 hello OS 버전/플랫폼 이미지의 SKU 또는 사용자 지정 이미지의 URI hello 모양은 다음과 같습니다.

1. Hello 가상 컴퓨터 크기 조정 설정 모델을 가져옵니다.
2. Hello 버전, SKU, 이미지 참조 또는 hello 모델에 대 한 URI 값을 변경 합니다.
3. Hello 모델을 업데이트 합니다.
4. 수행 된 *manualUpgrade* hello 크기 집합의 hello 가상 컴퓨터에서 호출 합니다. 이 단계는 관련만 경우 *upgradePolicy* 너무 설정**수동** 프로그램 규모에 맞게 설정 합니다. 너무 설정 되어 있으면**자동**, 가동 중지 시간 오류를 발생 시킬 모든 hello 가상 컴퓨터를 한 번에 업그레이드 합니다.

이 정보에 주의 hello 버전 및 hello REST API를 사용 하 여 PowerShell에 설정 해 규모의 업데이트 수는 어떻게 확인해 보겠습니다. 이러한 예제는 플랫폼 이미지의 hello 대/소문자를 포함 하지만이 문서에서는이 프로세스 tooa 사용자 지정 이미지 tooadapt 하기에 충분 한 정보를 제공 합니다.

## <a name="powershell"></a>PowerShell
이 예에서는 업데이트는 Windows 가상 컴퓨터 크기 집합 (만드는 toohello 새로운 버전 4.0.20160229입니다. Hello 모델을 업데이트 한 다음 한 번에 하나의 가상 컴퓨터 인스턴스는 업데이트 수행 됩니다.

```powershell
$rgname = "myrg"
$vmssname = "myvmss"
$newversion = "4.0.20160229"
$instanceid = "1"

# get hello VMSS model
$vmss = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname

# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.version = $newversion

# update hello virtual machine scale set model
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $vmss

# now start updating instances
Update-AzureRmVmssInstance -ResourceGroupName $rgname -VMScaleSetName $vmssname -InstanceId $instanceId
```

플랫폼 이미지 버전을 변경 하는 대신 사용자 지정 이미지에 대 한 URI hello를 업데이트 하는 경우 대체 hello "집합 hello 새 버전"를 업데이트 하는 명령 사용 하 여 줄 hello 소스 이미지 URI입니다. 예를 들어 hello 크기 집합을 만들어진 경우 Azure 관리 되는 디스크를 사용 하지 않고 hello 업데이트 다음과 같이 표시 됩니다.

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.osDisk.image.uri= $newURI
```

사용자 지정 이미지에 크기 집합 기반를 만든 경우 Azure 관리 되는 디스크를 사용 하 여 후 hello 이미지 참조를 업데이트 합니다. 예:

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.id = $newImageReference
```

## <a name="hello-rest-api"></a>hello REST API
다음은 몇 가지 hello Azure REST API tooroll OS 버전 업데이트를 사용 하는 Python 예입니다. 둘 다 사용 hello lightweight [azurerm](https://pypi.python.org/pypi/azurerm) Azure REST API 래퍼 함수 toodo GET hello 눈금에서의 라이브러리 설정 모델을 업데이트 된 모델 PUT 옵니다. 또한 살펴봅니다 가상 컴퓨터 인스턴스 뷰 업데이트 도메인이 tooidentify hello 가상 컴퓨터.

### <a name="vmssupgrade"></a>Vmssupgrade
 [Vmssupgrade](https://github.com/gbowerman/vmsstools) 은 가상 컴퓨터 크기를 실행 중인 운영 체제 업그레이드 tooa 아웃 tooroll가 사용 하는 Python 스크립트 한 번에 하나의 업데이트 도메인을 설정 합니다.

![가상 컴퓨터 또는 업데이트 도메인을 선택하기 위한 Vmssupgrade 스크립트](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssupgrade-screenshot.png)

이 스크립트를 사용 하면 tooupdate 특정 가상 컴퓨터를 선택 하거나 업데이트 도메인을 지정할 수 있습니다. Hello 사용자 지정 이미지의 URI를 변경 하거나 플랫폼 이미지 버전을 지원 합니다.

### <a name="vmsseditor"></a>Vmsseditor
[Vmsseditor](https://github.com/gbowerman/vmssdashboard) 는 한 행이 하나의 업데이트 도메인을 나타내는 heatmap으로 가상 컴퓨터 상태를 표시하는 가상 컴퓨터 확장 집합에 대한 범용 편집기입니다. 특히, 새 버전, SKU 또는 사용자 지정 이미지 URI 크기 집합에 대 한 hello 모델을 업데이트 하 고 오류 도메인 tooupgrade가 선택 합니다. 이렇게 하면 해당 업데이트 도메인에 있는 모든 hello 가상 컴퓨터는 업그레이드 된 toohello 새 모델입니다. 또는 사용자가 선택한 hello 일괄 처리 크기에 따라 롤링 업그레이드를 수행할 수 있습니다.  

hello 다음 스크린샷은 크기 Ubuntu 14.04 2LTS 14.04.201507060 버전에 대 한 집합의 모델입니다. 더 많은 옵션 이후 추가 된 toothis 도구이 스크린샷 가져왔습니다.

![Ubuntu 14.04-2LTS에 대한 확장 집합의 Vmsseditor 모델](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor1.png)

클릭 한 후 **업그레이드** 차례로 **자세한 정보 얻기**, UD 0의에서 가상 컴퓨터 tooupdate를 시작 합니다.

![진행 중인 업데이트를 보여 주는 Vmsseditor](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor2.png)

