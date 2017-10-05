---
title: "Azure에서 VM 가용성 집합 만들기 | Microsoft Docs"
description: "Resource Manager 배포 모델에서 Azure PowerShell 또는 포털을 사용하여 가상 컴퓨터에 대한 관리 가용성 집합 또는 비관리 가용성 집합을 만드는 방법에 대해 알아봅니다."
keywords: "가용성 집합"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a3db8659-ace8-4e78-8b8c-1e75c04c042c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e813ade8e105169f21138ed8a8eafda1ff39f42e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="increase-vm-availability-by-creating-an-azure-availability-set"></a>Azure 가용성 집합을 만들어 VM 가용성 향상 
가용성 집합은 응용 프로그램에 중복성을 제공합니다. 둘 이상의 가상 컴퓨터를 가용성 집합으로 그룹화하는 것이 좋습니다. 이 구성은 계획된 유지 관리 또는 계획되지 않은 유지 관리 이벤트 중에 적어도 하나의 가상 컴퓨터를 사용할 수 있고 99.95% Azure SLA가 충족되도록 합니다. 자세한 내용은 [가상 컴퓨터에 대한 SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/)를 참조하세요.

> [!IMPORTANT]
> 가용성 집합과 동일한 리소스 그룹에 VM을 만들어야 합니다.
> 

VM을 가용성 집합에 포함하려면 가용성 집합을 먼저 만들거나 집합에 첫 번째 VM을 만들 때 가용성 집합을 만들어야 합니다. VM에서 관리 디스크를 사용하게 될 경우 가용성 집합을 관리 가용성 집합으로 만들어야 합니다.

가용성 집합을 만들고 사용하는 방법에 대한 자세한 내용은 [가상 컴퓨터의 가용성 관리](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.

## <a name="use-the-portal-to-create-an-availability-set-before-creating-your-vms"></a>VM을 만들기 전에 포털을 사용하여 가용성 집합 만들기
1. 허브 메뉴에서 **찾아보기**를 클릭하고 **가용성 집합**을 선택합니다.
2. **가용성 집합 블레이드**에서 **추가**를 클릭합니다.
   
    ![새로운 가용성 집합을 만들기 위한 추가 단추를 보여 주는 스크린샷](./media/create-availability-set/add-availability-set.png)
3. **가용성 집합 만들기** 블레이드에서 해당 집합에 대한 정보를 입력합니다.
   
    ![가용성 집합을 만들기 위해 입력해야 할 정보를 보여 주는 스크린샷](./media/create-availability-set/create-availability-set.png)
   
   * **이름** - 이름은 숫자, 문자, 마침표, 밑줄 및 대시로 구성되며 1~ 80자 이내여야 합니다. 첫 번째 문자는 문자 또는 숫자여야 합니다. 마지막 문자는 문자, 숫자 또는 밑줄이어야 합니다.
   * **장애 도메인** - 장애 도메인은 공통 전원과 네트워크 스위치를 공유하는 가상 컴퓨터 그룹을 정의합니다. 기본적으로 VM은 최대 3개의 장애 도메인에 분산되어 있으며 장애 도메인 수는 1~3개 사이로 변경할 수 있습니다.
   * **업데이트 도메인** - 5개의 업데이트 도메인이 기본적으로 할당되며 1~20개 사이로 설정할 수 있습니다. 업데이트 도메인은 동시에 다시 부팅할 수 있는 가상 컴퓨터 그룹과 기본 물리적 하드웨어를 나타냅니다. 예를 들어 5개의 업데이트 도메인을 지정하며 단일 가용성 집합 내에 5개를 넘는 가상 컴퓨터를 구성한 경우 6번째 가상 컴퓨터는 동일한 업데이트 도메인에 첫 번째 가상 컴퓨터로 배치되고, 7번째 가상 컴퓨터는 동일한 UD에 두 번째 가상 컴퓨터로 배치되는 식입니다. 다시 부팅 순서는 순차적이지 않을 수 있지만 한 번에 하나의 업데이트 도메인만 다시 부팅합니다.
   * **구독** - 둘 이상의 구독이 있는 경우 사용할 구독을 선택합니다.
   * **리소스 그룹** -화살표를 클릭하고 드롭다운에서 리소스 그룹을 선택하여 기존 리소스 그룹을 선택합니다. 또한 이름을 입력하여 새 리소스 그룹을 만들 수도 있습니다. 이름에는 문자, 숫자, 마침표, 대시, 밑줄 및 여는 괄호 또는 닫는 괄호가 포함될 수 있습니다. 이름이 마침표로 끝날 수 없습니다. 가용성 그룹의 모든 VM은 가용성 집합과 동일한 리소스 그룹에 만들어야 합니다.
   * **위치** - 드롭다운 목록에서 위치를 선택합니다.
   * **관리** - 저장소에 Managed Disks를 사용하는 VM과 함께 사용할 관리 가용성 집합을 만들려면 *예*를 선택합니다. 집합에 포함될 VM이 저장소 계정에 비관리 디스크를 사용하는 경우 **아니요**를 선택합니다.
   
4. 정보를 다 입력했으면 **만들기**를 클릭합니다. 

## <a name="use-the-portal-to-create-a-virtual-machine-and-an-availability-set-at-the-same-time"></a>포털을 사용하여 가상 컴퓨터와 가용성 집합을 동시에 만들기
포털을 사용하여 새 VM을 만드는 경우 집합의 첫 번째 VM을 만드는 동안 VM에 대한 새 가용성 집합도 만들 수 있습니다. VM에 Managed Disks를 사용하기로 선택하면 관리 가용성 집합이 생성됩니다.

![VM을 만드는 동안 새로운 가용성 집합을 만드는 프로세스를 보여 주는 스크린샷](./media/create-availability-set/new-vm-avail-set.png)

## <a name="add-a-new-vm-to-an-existing-availability-set-in-the-portal"></a>포털에서 기존 가용성 집합에 새 VM 추가
집합에 포함하기 위해 만드는 각 VM을 동일한 **리소스 그룹** 에 만들어야 하며 3단계에서 기존 가용성 집합을 선택해야 합니다. 

![VM에 사용할 기존 가용성 집합을 선택하는 방법을 보여 주는 스크린샷](./media/create-availability-set/add-vm-to-set.png)

## <a name="use-powershell-to-create-an-availability-set"></a>PowerShell을 사용하여 가용성 집합 만들기
이 예제에서는 **미국 서부** 위치의 **myResourceGroup** 리소스 그룹에 **myAvailabilitySet**이라는 가용성 집합을 만듭니다. 집합에 포함될 첫 번째 VM을 만들기 전에 이 작업을 수행해야 합니다.

시작하기 전에 AzureRM.Compute PowerShell 모듈이 최신 버전인지 확인합니다. 다음 명령을 실행하여 PowerShell을 설치합니다.

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
자세한 내용은 [Azure PowerShell 버전 관리](/powershell/azure/overview)를 참조하세요.


VM에 관리 디스크를 사용하는 경우 다음을 입력합니다.

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" -managed
```

VM에 사용자 고유의 저장소 계정을 사용하는 경우 다음을 입력합니다.

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" 
```

자세한 내용은 [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset)를 참조하세요.

## <a name="troubleshooting"></a>문제 해결
* VM을 만들 때 원하는 가용성 집합이 포털의 드롭다운 목록에 없는 경우 다른 리소스 그룹에 만들었을 수 있습니다. 가용성 집합에 대한 리소스 그룹을 모르는 경우 허브 메뉴로 이동한 후 찾아보기 > 가용성 집합을 클릭하여 가용성 집합 및 해당 집합이 속하는 리소스 그룹 목록을 표시합니다.

## <a name="next-steps"></a>다음 단계
[데이터 디스크](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 더 추가하여 VM에 저장소를 좀 더 추가합니다.

