---
title: "백업에 대 한 Azure 관리 되는 디스크의 복사본 aaaCreate | Microsoft Docs"
description: "위쪽 또는 문제 해결을 다시 디스크는 Azure 관리 되는 디스크 toouse의 복사본을 발급 하는 toocreate 방법에 대해 알아봅니다."
documentationcenter: 
author: cwatson-cat
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 15eb778e-fc07-45ef-bdc8-9090193a6d20
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 2/9/2017
ms.author: cwatson
ms.openlocfilehash: 2f33dbbee624bcd813f3c7c3e3401072d0933714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a>관리 스냅숏을 사용하여 Azure Managed Disk로 저장된 VHD 복사본 만들기
백업에 대 한 관리 되는 디스크의 스냅숏을 또는 hello 스냅숏에서 관리 되는 디스크를 만들어 tooa 테스트 가상 컴퓨터 tootroubleshoot를 연결 합니다. 관리 스냅숏은 VM Managed Disk의 특정 시점 전체 복사본입니다. VHD의 읽기 전용 복사본을 만들어서 기본적으로 표준 Managed Disk로 저장합니다. Managed Disk에 대한 자세한 내용은 [Azure Managed Disks 개요](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.

가격 책정에 대한 자세한 내용은 [Azure Storage 가격 책정](https://azure.microsoft.com/pricing/details/managed-disks/)을 참조하세요. 

## <a name="before-you-begin"></a>시작하기 전에
PowerShell을 사용 하는 경우 hello hello AzureRM.Compute PowerShell 모듈의 최신 버전이 있는지 확인 합니다. 실행 명령 tooinstall 다음 hello 합니다.

```
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
자세한 내용은 [Azure PowerShell 버전 관리](/powershell/azure/overview)를 참조하세요.

## <a name="copy-hello-vhd-with-a-snapshot"></a>스냅숏 사용 하 여 hello VHD 복사
Hello Azure 포털 또는 PowerShell tootake hello 관리 되는 디스크의 스냅숏 사용 합니다.

### <a name="use-azure-portal-tootake-a-snapshot"></a>Azure 포털 tootake 스냅숏을 사용 하 여 

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. 왼쪽 위에서 hello 년부터 클릭 **새로** 검색 한 **스냅숏**합니다.
3. Hello 스냅숏 블레이드에서 클릭 **만들기**합니다.
4. 입력 한 **이름** hello 스냅숏에 대 한 합니다.
5. 기존 선택 [리소스 그룹](../../azure-resource-manager/resource-group-overview.md#resource-groups) 또는 새 유형 hello 이름입니다. 
6. Azure 데이터 센터 위치를 선택합니다.  
7. 에 대 한 **원본 디스크**, 선택 hello toosnapshot 디스크 관리.
8. 선택 hello **계정 유형** toouse toostore hello 스냅숏 합니다. 고성능 디스크에 저장할 필요가 없다면 **Standard_LRS**를 권장합니다.
9. **만들기**를 클릭합니다.

### <a name="use-powershell-tootake-a-snapshot"></a>PowerShell tootake 스냅숏을 사용 하 여
hello 다음 단계 tooget hello VHD 복사 toobe 디스크 하는 방법을 알려주는 hello 스냅숏 구성을 만들고 새로 AzureRmSnapshot hello cmdlet을 사용 하 여 hello 디스크의 스냅숏을<!--Add link toocmdlet when available-->합니다. 

1. 일부 매개 변수를 설정합니다. 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$location = 'southeastasia' 
$dataDiskName = 'ContosoMD_datadisk1' 
$snapshotName = 'ContosoMD_datadisk1_snapshot1'  
```
  Hello 매개 변수 값을 바꿉니다.
  -  "myResourceGroup" hello VM의 리소스 그룹을 사용 합니다.
  -  "southeastasia" hello 지리적 위치에 저장 된 관리 되는 스냅숏을 저장할와 합니다. <!---How do you look these up? -->
  -  "ContosoMD_datadisk1" hello 이름의 hello VHD 디스크 toocopy 되도록 합니다.
  -  "ContosoMD_datadisk1_snapshot1" hello로 이름을 지정 하면 새 스냅숏을 hello에 대 한 toouse 원하는 합니다.

2. Hello VHD 디스크 toobe를 복사를 가져옵니다.

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $dataDiskName 
```
3. Hello 스냅숏 구성을 생성 합니다. 

 ```powershell
$snapshot =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -CreateOption Copy -Location $location 
```
4. Hello 스냅숏을 생성 합니다.

 ```powershell
New-AzureRmSnapshot -Snapshot $snapshot -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName 
```
Hello 매개 변수를 사용 하 여 관리 되는 디스크 toouse hello 스냅숏 toocreate를 계획 하 고 toobe 높은 수행 해야 하는 VM을 연결 하는 경우 `-AccountType Premium_LRS` hello AzureRmSnapshot 새로 만들기 명령을 사용 합니다. hello 매개 변수 hello 스냅숏을 생성 되어 프리미엄 관리 되는 디스크로 저장 됩니다. 프리미엄 Managed Disks는 표준 Managed Disks보다 비용이 많이 듭니다. 따라서 해당 매개 변수를 사용하기 전에 프리미엄이 필요한지 확인합니다.


