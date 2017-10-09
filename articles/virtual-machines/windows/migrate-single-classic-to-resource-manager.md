---
title: "클래식 VM tooan ARM 관리 디스크 VM aaaMigrate | Microsoft Docs"
description: "단일 Azure VM hello 클래식 배포에서 마이그레이션 tooManaged 디스크 hello 리소스 관리자 배포 모델에서 모델입니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: d8c4b9431f5dd8a071fcbc2ee36581a33f76ba62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manually-migrate-a-classic-vm-tooa-new-arm-managed-disk-vm-from-hello-vhd"></a>기본 VM tooa로 직접 마이그레이션하 ARM 관리 되는 디스크의에서 새 VM VHD hello 


이 섹션에서는 toomigrate 하면 기존 Azure Vm에 hello 클래식 배포 모델에서 너무[관리 하는 디스크](managed-disks-overview.md) hello 리소스 관리자 배포 모델에서.


## <a name="plan-for-hello-migration-toomanaged-disks"></a>Hello 마이그레이션 계획 tooManaged 디스크

이 섹션 toomake hello 최선의 결정을 VM 및 디스크 유형에 대 수 있도록 도와줍니다.


### <a name="location"></a>위치

Azure Managed Disks를 사용할 수 있는 위치를 선택합니다. TooPremium 관리 하는 디스크를 마이그레이션하는 경우 또한 toomigrate를 계획 하는 hello 지역에서 프리미엄 저장소를 사용할 수 있는지 확인 합니다. 사용 가능한 위치에 대한 최신 정보는 [지역별 Azure 서비스](https://azure.microsoft.com/regions/#services)를 참조하세요.

### <a name="vm-sizes"></a>VM 크기

TooPremium 관리 하는 디스크를 마이그레이션하는 경우 VM이 있는 hello 영역의 tooupdate hello 크기인 hello VM tooPremium 사용 가능한 저장소 가능 크기를 수 있습니다. 프리미엄 저장소 수 있는 hello VM 크기를 검토 합니다. hello Azure VM 크기 사양에 나열 된 [가상 컴퓨터의 크기](sizes.md)합니다.
프리미엄 저장소를 사용 하 고 작업에 가장 적합 한 hello 가장 적절 한 VM 크기를 선택 하는 가상 컴퓨터의 hello 성능 특성을 검토 합니다. VM toodrive hello 디스크 트래픽에 사용할 수 있는 충분 한 대역폭이 있는지 확인 합니다.

### <a name="disk-sizes"></a>디스크 크기

**프리미엄 Managed Disks**

VM에서 사용할 수 있는 프리미엄 관리 디스크에는 7가지 형식이 있으며 각 형식에는 특정 IOP 및 처리량 한도가 있습니다. Hello 프리미엄 디스크 유형 VM에 대 한 용량, 성능, 확장성, 관점에서 응용 프로그램의 hello 요구 사항에 따라 적중 영향과 최고 선택할 때 이러한 제한을 고려 합니다.

| 프리미엄 디스크 유형  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| 디스크 크기           | 128GB| 512GB| 128GB| 512GB            | 1,024GB(1TB)    | 2,048GB(2TB)    | 4,095GB(4TB)    | 
| 디스크당 IOPS       | 120   | 240   | 500   | 2,300              | 5,000              | 7,500              | 7,500              | 
| 디스크당 처리량 | 초당 25MB  | 초당 50MB  | 초당 100MB | 초당 150MB | 초당 200MB | 초당 250MB | 초당 250MB | 

**표준 Managed Disks**

VM에서 사용할 수 있는 표준 관리 디스크에는 7가지 형식이 있습니다. 각각은 용량이 다르지만 동일한 IOPS 및 처리량이 제한됩니다. Hello 유형의 응용 프로그램의 hello 용량 요구 사항에 따라 관리 되는 표준 디스크를 선택 합니다.

| 표준 디스크 유형  | S4               | S6               | S10              | S20              | S30              | S40              | S50              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| 디스크 크기           | 30GB            | 64GB            | 128GB           | 512GB           | 1,024GB(1TB)   | 2,048GB(2TB)    | 4,095GB(4TB)   | 
| 디스크당 IOPS       | 500              | 500              | 500              | 500              | 500              | 500             | 500              | 
| 디스크당 처리량 | 60 MB per second | 60 MB per second | 60 MB per second | 60 MB per second | 60 MB per second | 60 MB per second | 60 MB per second | 


### <a name="disk-caching-policy"></a>디스크 캐싱 정책 

**프리미엄 Managed Disks**

디스크 캐싱 정책은 기본적으로 *읽기 전용* 모든 hello 프리미엄 데이터 디스크에 대 한 및 *읽기 / 쓰기* hello 프리미엄 운영 체제 디스크에 대 한 toohello VM을 연결 합니다. 이 구성 설정은 응용 프로그램의 IOs 용 tooachieve hello 최적의 성능은 것이 좋습니다. 쓰기가 많거나 쓰기 전용인 디스크의 경우(예: SQL Server 로그 파일) 더 나은 응용 프로그램 성능을 얻기 위해 디스크 캐싱을 사용하지 않도록 설정합니다.

### <a name="pricing"></a>가격

검토 hello [관리 하는 디스크에 대 한 가격 책정](https://azure.microsoft.com/en-us/pricing/details/managed-disks/)합니다. 프리미엄 관리 되는 디스크의 가격 책정은 hello 프리미엄 관리 되지 않는 디스크와 동일 합니다. 하지만 표준 Managed Disks의 가격 책정은 관리되지 않는 표준 디스크와 다릅니다.


## <a name="checklist"></a>검사 목록

1.  TooPremium 관리 하는 디스크를 마이그레이션하는 경우은로 마이그레이션하는 hello 영역에 사용할 수 있는지 확인 합니다.

2.  사용 하려는 hello 새 VM 시리즈를 결정 합니다. TooPremium 관리 하는 디스크를 마이그레이션하는 경우 프리미엄 저장소를 지원 해야 합니다.

3.  Hello 정확한 VM 크기 사용 하 여로 마이그레이션하는 hello 지역에서 사용할 수 있는 결정 합니다. VM 크기에 있는 데이터 디스크 개수 충분히 큰 toosupport hello toobe 필요 합니다. 예를 들어 4 개의 데이터 디스크를 사용 하도록 설정한 경우 hello VM 두 개 이상의 코어에 있어야 합니다. 또한 처리 능력, 메모리 및 네트워크 대역폭 요구 사항을 고려합니다.

4.  정보 포함 하 고 hello 현재 VM 디스크 및 해당 VHD blob hello 목록을 포함 하 여 편리 합니다.

응용 프로그램의 가동 중지 시간을 준비합니다. 클린 마이그레이션 toodo toostop 모든 hello 처리는 hello 현재 시스템에서 합니다. 경우에 표시할 수 있습니다 마이그레이션할 수 없는 tooconsistent 상태 toohello 새 플랫폼입니다. 작동 중단 기간 hello 디스크 toomigrate의 데이터 양을 hello에 따라 달라 집니다.


## <a name="migrate-hello-vm"></a>Hello VM 마이그레이션

응용 프로그램의 가동 중지 시간을 준비합니다. 클린 마이그레이션 toodo toostop 모든 hello 처리는 hello 현재 시스템에서 합니다. 경우에 표시할 수 있습니다 마이그레이션할 수 없는 tooconsistent 상태 toohello 새 플랫폼입니다. 작동 중단 기간 hello hello 디스크 toomigrate의 데이터 양에 따라 달라 집니다.


1.  먼저, hello 공통 매개 변수를 설정 합니다.

    ```powershell
    $resourceGroupName = 'yourResourceGroupName'
    
    $location = 'your location' 
    
    $virtualNetworkName = 'yourExistingVirtualNetworkName'
    
    $virtualMachineName = 'yourVMName'
    
    $virtualMachineSize = 'Standard_DS3'
    
    $adminUserName = "youradminusername"
    
    $adminPassword = "yourpassword" | ConvertTo-SecureString -AsPlainText -Force
    
    $imageName = 'yourImageName'
    
    $osVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd'
    
    $dataVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk1.vhd'
    
    $dataDiskName = 'dataDisk1'
    ```

2.  Hello에서 VHD hello를 사용 하 여 관리 되는 운영 체제 디스크를 만들 클래식 VM입니다.

    Hello 완료 URI hello OS VHD toohello $osVhdUri 매개 변수를 제공 했는지 확인 합니다. 또한 마이그레이션하는 디스크의 종류(프리미엄 또는 표준)에 따라 **-AccountType**을 **PremiumLRS** 또는 **StandardLRS**로 입력합니다.

    ```powershell
    $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $osVhdUri) '
    -ResourceGroupName $resourceGroupName
    ```

3.  Hello OS 디스크 toohello 연결 새 VM입니다.

    ```powershell
    $VirtualMachine = New-AzureRmVMConfig -VMName $virtualMachineName -VMSize $virtualMachineSize
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -ManagedDiskId $osDisk.Id '
    -StorageAccountType PremiumLRS -DiskSizeInGB 128 -CreateOption Attach -Windows
    ```

4.  Hello 데이터 VHD 파일에서 관리 되는 데이터 디스크를 만들고 toohello 추가 새 VM입니다.

    ```powershell
    $dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreationDataCreateOption Import '
    -SourceUri $dataVhdUri ) -ResourceGroupName $resourceGroupName
    
    $VirtualMachine = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name $dataDiskName '
    -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1
    ```

5.  만들 공용 IP, 가상 네트워크 및 NIC. 설정 하 여 새 VM을 hello

    ```powershell
    $publicIp = New-AzureRmPublicIpAddress -Name ($VirtualMachineName.ToLower()+'_ip') '
    -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
    
    $vnet = Get-AzureRmVirtualNetwork -Name $virtualNetworkName -ResourceGroupName $resourceGroupName
    
    $nic = New-AzureRmNetworkInterface -Name ($VirtualMachineName.ToLower()+'_nic') '
    -ResourceGroupName $resourceGroupName -Location $location -SubnetId $vnet.Subnets[0].Id '
    -PublicIpAddressId $publicIp.Id
    
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $nic.Id
    
    New-AzureRmVM -VM $VirtualMachine -ResourceGroupName $resourceGroupName -Location $location
    ```

> [!NOTE]
>추가 단계가 필요한 toosupport 있을 수 있는 응용 프로그램에서 다룰 수 없는이 가이드입니다.
>
>

## <a name="next-steps"></a>다음 단계

- Toohello 가상 컴퓨터를 연결 합니다. 자세한 내용은 [어떻게 tooconnect 로그온 tooan Azure 가상 컴퓨터 및 Windows를 실행](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

