---
title: "Azure에서 VHD에서 관리 되는 디스크 aaaCreate | Microsoft Docs"
description: "Hello 리소스 관리자 배포 모델을 사용 하는 Azure 저장소 계정에 현재 사용 중인 VHD에서 관리 되는 디스크를 만듭니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/05/2017
ms.author: cynthn
ms.openlocfilehash: 77adaac5419186ff85039fe2c4752f021aa5e448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-managed-disks-from-unmanaged-disks-in-a-storage-account"></a>저장소 계정의 비관리 디스크로 관리 디스크 만들기

현재 Azure 저장소 계정에 있는 기존 데이터 디스크 또는 OS 디스크로 관리 디스크를 만들 수 있습니다. 또한 VM의 새 데이터 디스크로 사용할 수 있는 빈 디스크를 만들 수 있습니다. 

## <a name="before-you-begin"></a>시작하기 전에
PowerShell을 사용 하는 경우 hello hello AzureRM.Compute PowerShell 모듈의 최신 버전이 있는지 확인 합니다. 실행 명령 tooinstall 다음 hello 합니다.

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
자세한 내용은 [Azure PowerShell 버전 관리](/powershell/azure/overview)를 참조하세요.


## <a name="create-a-managed-disk-from-a-vhd-in-an-azure-storage-account"></a>Azure 저장소 계정에서 VHD로 관리 디스크 만들기 | Microsoft Docs

관리 되는 디스크는 VHD에서 디스크를 생성 하 고 toohello 매개 변수를 할당 하는 hello 예제 **$disk1** toouse 나중입니다. 

hello 관리 되는 디스크에에서 생성 됩니다 hello **West US** 이라는 리소스 그룹에 위치 **myResourceGroup**합니다. hello 디스크 이름은 **myDisk** 라는 VHD 파일에서 생성 됩니다 **myDisk.vhd** 라는 tooa 저장소 계정에서는 이전에 업로드 **mystorageaccount**합니다. 관리 되는 디스크 hello 프리미엄 로컬 중복 저장소 (LRS)에서 생성 됩니다. StandardLRS 및 PremiumLRS는 hello만 **-AccountType** 옵션에 사용할 수 있는 디스크를 관리 합니다. 

1.  일부 매개 변수 설정

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $diskName = "myDisk"
    $vhdUri = "https://mystorageaccount.blob.core.windows.net/vhds/myDisk.vhd"
    ```

2. Hello 데이터 디스크를 만듭니다. 
    ```powershell
    $disk1 = New-AzureRmDisk -DiskName $diskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $vhdUri) -ResourceGroupName $rgName
    ```
    
    

## <a name="create-an-empty-data-disk-as-a-managed-disk"></a>관리 디스크로 빈 데이터 디스크 만들기

관리 되는 디스크와 빈 데이터 디스크를 생성 하 고 toohello 매개 변수를 할당 하는 hello 예제 **$dataDisk2** toouse 나중입니다. 빈 데이터 디스크 toobe 초기화 toohello VM에서에서 로깅 및 diskmgmt.msc 사용 해야 합니다 또는 [WinRM 및 스크립트를 사용 하 여 원격으로](attach-disk-ps.md#initialize-the-disk), 연결 된 tooa VM을 실행 하는 것입니다.

hello에 hello 빈 데이터 디스크를 만들 수는 **중앙 미국 서 부** 이라는 리소스 그룹에 위치 **myResourceGroup**합니다. hello 디스크 이름은 **myEmptyDataDisk**합니다. hello 빈 디스크를 프리미엄 로컬 중복 저장소 (LRS)에서 생성 됩니다. StandardLRS 및 PremiumLRS는 hello만 **-AccountType** 옵션에 사용할 수 있는 디스크를 관리 합니다.

이 예에서 hello 디스크 크기는 128GB, 있지만 VM에서 실행 중인 모든 응용 프로그램의 hello 요구를 충족 하는 크기를 선택 해야 합니다.

1.  일부 매개 변수 설정

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $dataDiskName = "myEmptyDataDisk"
    ```

2. Hello 데이터 디스크를 만듭니다.
    ```powershell
    $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Empty -DiskSizeGB 128) -ResourceGroupName $rgName
    ```
    
## <a name="next-steps"></a>다음 단계   
- 이미 VM이 있는 경우 [데이터 디스크를 연결](attach-disk-portal.md)할 수 있습니다.
