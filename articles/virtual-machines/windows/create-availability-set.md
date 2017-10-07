---
title: "Azure에서 VM 가용성 aaaCreate 설정 | Microsoft Docs"
description: "어떻게 toocreate 관리 되는 가용성 설정 하거나 관리 되지 않는 가용성 Azure PowerShell을 사용 하 여 가상 컴퓨터에 대 한 설정 또는 hello hello 리소스 관리자 배포 모델에서 포털에 알아봅니다."
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
ms.openlocfilehash: eadcdfcd28bb2fa21a4647f207b390c33e022ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="increase-vm-availability-by-creating-an-azure-availability-set"></a>Azure 가용성 집합을 만들어 VM 가용성 향상 
가용성 집합 중복 tooyour 응용 프로그램을 제공합니다. 둘 이상의 가상 컴퓨터를 가용성 집합으로 그룹화하는 것이 좋습니다. 이 구성을 통해 계획 되거나 계획 되지 않은 유지 관리 이벤트 중 하나에서 가상 컴퓨터를 하나 이상 있게 되며, 사용 가능 하 고 충족 hello 99.95% Azure SLA 합니다. 자세한 내용은 참조 hello [가상 컴퓨터에 대 한 SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/)합니다.

> [!IMPORTANT]
> Vm에에서 만들어야 hello 동일 hello 가용성 집합으로 리소스 그룹입니다.
> 

가용성 집합의 VM toobe 파트를 표시할 경우 toocreate hello 가용성 설정 하는 동안 첫 번째 또는 첫 번째 VM에에서 만드는 hello 집합. VM 디스크 관리를 사용 하는 경우 hello 가용성 집합 관리 되는 가용성 집합으로 만들어야 합니다.

만들기 및 가용성 집합을 사용 하는 방법에 대 한 자세한 내용은 참조 [관리 가상 컴퓨터의 가용성을 hello](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

## <a name="use-hello-portal-toocreate-an-availability-set-before-creating-your-vms"></a>Hello 포털 toocreate 가용성 집합에 Vm을 만들기 전에 사용 하 여
1. Hello 허브 메뉴에서 클릭 **찾아보기** 선택 **가용성 집합**합니다.
2. Hello에 **가용성 집합 블레이드**, 클릭 **추가**합니다.
   
    ![새 가용성 집합을 만들기 위한 단추를 추가 하는 hello를 보여 주는 스크린 샷.](./media/create-availability-set/add-availability-set.png)
3. Hello에 **가용성 집합 만들기** 블레이드, 사용자 집합에 대 한 전체 hello 정보입니다.
   
    ![Hello tooenter toocreate hello 가용성 필요한 정보를 표시 하는 스크린 샷 설정 합니다.](./media/create-availability-set/create-availability-set.png)
   
   * **이름** -hello 이름은 숫자, 문자, 마침표, 밑줄 및 대시만 구성 하는 1-80 자 여야 합니다. hello 첫 번째 문자는 문자 또는 숫자 여야 합니다. hello 마지막 문자는 문자, 숫자 또는 밑줄 이어야 합니다.
   * **오류 도메인** -오류 도메인 공통 전원 원본과 네트워크 스위치를 공유 하는 가상 컴퓨터의 hello 그룹을 정의 합니다. 기본적으로 hello Vm toothree 오류 도메인에 걸쳐 분리 되어 및 변경 된 toobetween 1 및 3 일 수 있습니다.
   * **업데이트 도메인** -5 개의 업데이트 도메인이 기본적으로 할당 되 고 1에서 20 toobetween 설정할 수 있습니다. 업데이트 도메인 hello에서 다시 부팅 해야 하는 기본 실제 하드웨어와 가상 컴퓨터 그룹을 나타내는 동시 합니다. 예를 들어 5 개의 업데이트 도메인을 6 개 이상의 가상 컴퓨터는 단일 가용 세트 hello 여섯 번째 가상 컴퓨터 내에서 구성 된 경우에 배치 됨 hello hello 첫 번째 가상 컴퓨터와 동일한 업데이트 도메인 hello 일곱 번째에서 지정 하는 경우 hello 동일 두 번째 가상 컴퓨터 hello 등으로 UD 합니다. hello 재부팅 hello 순서 순차적, 되지 않을 수 있지만 한 번에 하나의 업데이트 도메인을 다시 부팅 합니다.
   * **구독** -선택 hello 구독 toouse 여러 개 있는 경우.
   * **리소스 그룹** -hello 화살표를 클릭 하 고 hello에서 리소스 그룹을 선택 하 여 기존 리소스 그룹의 드롭다운 목록 선택 합니다. 또한 이름을 입력하여 새 리소스 그룹을 만들 수도 있습니다. hello 이름에 포함할 수 있는 문자 hello: 문자, 숫자, 마침표, 대시, 밑줄 및 opening 또는 닫는 괄호입니다. hello 이름은 마침표로 끝날 수 없습니다. 모든 hello 가용성 그룹에 Vm hello 필요 toobe hello에서 만든 가용성 집합 hello와 동일한 리소스 그룹입니다.
   * **위치** -hello 드롭다운 목록에서 위치를 선택 합니다.
   * **관리 되는** -선택 *예* toocreate 관리 되는 가용성 집합 관리 하는 디스크 저장소를 사용 하는 Vm과 toouse 합니다. 선택 **아니요** hello Vm hello 집합에 있는 경우 저장소 계정에 관리 되지 않는 디스크를 사용 합니다.
   
4. Hello 정보를 모두 입력 작업을 완료 하면 클릭 **만들기**합니다. 

## <a name="use-hello-portal-toocreate-a-virtual-machine-and-an-availability-set-at-hello-same-time"></a>가상 컴퓨터와 가용성 동일 하 게 설정 hello에 hello 포털 toocreate를 사용 하 여 시간
Hello 포털을 사용 하 여 새 VM을 만들면 hello를 만드는 동안 hello VM에 대해 설정할 새 가용성 만들 수도 있습니다 hello 집합의 첫 번째 VM입니다. VM에 대 한 toouse 관리 하는 디스크를 선택 하면 관리 되는 가용성 집합 생성 됩니다.

![새 유지를 hello VM을 만드는 동안 설정 hello 프로세스를 보여 주는 스크린 샷](./media/create-availability-set/new-vm-avail-set.png)

## <a name="add-a-new-vm-tooan-existing-availability-set-in-hello-portal"></a>새 VM tooan 기존 가용성 집합 hello 포털에서 추가
각 VM에 대해 추가 만들면 hello 집합에 속하는, 만드는 것에 있는지 확인 해야 하는 동일한 hello **리소스 그룹** 다음 선택 hello 3 단계에서에서 설정 하는 기존 가용성 및 합니다. 

![기존 가용성 tooselect toouse VM에 대 한 설정 하는 방법을 보여 주는 스크린샷](./media/create-availability-set/add-vm-to-set.png)

## <a name="use-powershell-toocreate-an-availability-set"></a>PowerShell toocreate 가용성을 사용 하 여 설정
이 예에서는 가용성 명명 된 집합을 만듭니다 **myAvailabilitySet** hello에 **myResourceGroup** hello의 리소스 그룹 **West US** 위치 합니다. 이 테스트 toobe hello를 만들기 전에 수행 해야 hello 집합에 있는 첫 번째 VM입니다.

시작 하기 전에 hello hello AzureRM.Compute PowerShell 모듈의 최신 버전이 있는지 확인 합니다. 실행 명령 tooinstall 다음 hello 합니다.

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
* 만들 때 VM에 사용할 가용성 집합을 hello hello 포털에서 hello 드롭 다운 목록에 없으면 만들었을 수 것 다른 리소스 그룹에 있습니다. 가능 여부에 대 한 hello 리소스 그룹 설정 toohello 허브 메뉴를 이동 하 고 찾아보기를 클릭 하 여 알 수 없는 경우 > 가용성 집합 toosee 목록이 가능 여부를 설정 하 고 있는 리소스 그룹에 속해 있습니다.

## <a name="next-steps"></a>다음 단계
추가 추가 하 여 추가 저장소 tooyour VM을 추가할 [데이터 디스크](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

