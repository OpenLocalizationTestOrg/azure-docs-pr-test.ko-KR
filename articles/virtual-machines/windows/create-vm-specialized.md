---
title: "Azure에서 특수화 된 VHD에서 Windows VM aaaCreate | Microsoft Docs"
description: "Hello 리소스 관리자 배포 모델에서 사용 하 여 hello 운영 체제 디스크와 관리 되는 특수 한 디스크를 연결 하 여 새 Windows VM을 만듭니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3b7d3cd5-e3d7-4041-a2a7-0290447458ea
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: cynthn
ms.openlocfilehash: c72c6f4fb650e2664e87cf38ec9be62f0b2209fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-vm-from-a-specialized-disk"></a>특수한 디스크에서 Windows VM 만들기

Powershell을 사용 하 여 hello 운영 체제 디스크와 관리 되는 특수 한 디스크를 연결 하 여 새 VM을 만듭니다. 특수 한 디스크 hello 사용자 계정 및 응용 프로그램, 원래 VM에서 다른 상태 데이터를 유지 하는 기존 VM에서 가상 하드 디스크 (VHD)의 복사본을입니다. 

특수 한 VHD toocreate 새 VM을 사용 하는 경우 새 VM의 hello 컴퓨터 이름을 그대로 유지 하는 hello hello 원본 VM입니다. 다른 컴퓨터 관련 정보도 유지되며, 경우에 따라 이 중복된 정보로 인해 문제가 발생할 수 있습니다. VM을 복사할 때 응용 프로그램이 어떤 유형의 컴퓨터 관련 정보에 의존하는지 알아야 합니다.

다음 두 가지 옵션을 사용할 수 있습니다.
* [VHD 업로드](#option-1-upload-a-specialized-vhd)
* [기존 Azure VM 복사](#option-2-copy-an-existing-azure-vm)

이 항목에서는 toouse 디스크를 관리 하는 방법을 보여 줍니다. 저장소 계정을 사용해야 하는 레거시 배포가 있는 경우 [저장소 계정의 특수한 VHD에서 VM 만들기](sa-create-vm-specialized.md)를 참조하세요.

## <a name="before-you-begin"></a>시작하기 전에
PowerShell을 사용 하는 경우 hello hello AzureRM.Compute PowerShell 모듈의 최신 버전이 있는지 확인 합니다. 

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
자세한 내용은 [Azure PowerShell 버전 관리](/powershell/azure/overview)를 참조하세요.


## <a name="option-1-upload-a-specialized-vhd"></a>옵션 1: 특수한 VHD 업로드

Hello 하이퍼-V 또는 VM 사설 클라우드에서 다른 클라우드에서 내보낼 처럼 온-프레미스 가상화 도구를 사용 하 여 만든 특수 한 VM에서 VHD를 업로드할 수 있습니다.

### <a name="prepare-hello-vm"></a>Hello VM 준비
Toouse를 가져오려는 경우 VHD로 hello-toocreate 새 VM은 hello 다음 단계를 완료 합니다. 
  
  * [Windows VHD tooupload tooAzure 준비](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다. **없는** 일반화 Sysprep를 사용 하 여 VM hello 합니다.
  * 모든 게스트 가상화 도구와 hello VM (예: VMware 도구)에 설치 된 에이전트를 제거 합니다.
  * Hello VM 확인 해당 IP 주소 및 DNS 설정이 DHCP 통해 구성 된 toopull 됩니다. 이렇게 하면 해당 hello 서버를 시작할 때 hello VNet 내에서 IP 주소를 가져옵니다. 


### <a name="get-hello-storage-account"></a>Hello 저장소 계정 가져오기
저장소에 필요한 계정 Azure toostore hello에 VHD를 업로드 합니다. 기존 저장소 계정을 사용하거나 새 계정을 만들 수 있습니다. 

tooshow hello 사용 가능한 저장소 계정을 입력 합니다.

```powershell
Get-AzureRmStorageAccount
```

Toouse 기존 저장소 계정을 사용할 경우 진행 toohello [VHD 업로드 hello](#upload-the-vhd-to-your-storage-account) 섹션.

저장소 계정 toocreate 해야 할 경우 다음이 단계를 따르십시오.

1. Hello 저장소 계정을 만들어야 하는 hello 리소스 그룹의 hello 이름이 필요 합니다. 구독을 형식에 있는 모든 hello 리소스 그룹 아웃 toofind:
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    리소스 그룹 이름이 toocreate *myResourceGroup* hello에 *미국 서 부* 지역, 유형:

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. 라는 저장소 계정 만들기 *mystorageaccount* hello를 사용 하 여이 리소스 그룹에 [새로 AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```

### <a name="upload-hello-vhd-tooyour-storage-account"></a>Hello VHD tooyour 저장소 계정에 업로드 
사용 하 여 hello [추가 AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) 저장소 계정의 cmdlet tooupload hello VHD tooa 컨테이너입니다. 이 예에서는 업로드 파일 hello *myVHD.vhd* 에서 `"C:\Users\Public\Documents\Virtual hard disks\"` tooa 저장소 계정인 *mystorageaccount* hello에 *myResourceGroup* 리소스 그룹입니다. hello 파일은 라는 hello 컨테이너에 저장 *mycontainer* hello 새 파일 이름이 됩니다 *myUploadedVHD.vhd*합니다.

```powershell
$resourceGroupName = "myResourceGroup"
$urlOfUploadedVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $resourceGroupName -Destination $urlOfUploadedVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


성공 하면 다음과 비슷한 toothis 응답 가져오기:

```powershell
MD5 hash is being calculated for hello file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for hello operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

이 명령은 네트워크 연결 및 VHD 파일의 hello 크기에 따라 시간이 걸릴 수 있습니다 toocomplete

### <a name="create-a-managed-disk-from-hello-vhd"></a>Hello VHD에서에서 관리 되는 디스크를 만들려면

Hello에서 관리 되는 디스크를 만들 사용 하 여 저장소 계정에서 VHD를 특수화할 [새로 AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk)합니다. 이 예에서는 **myOSDisk1** hello 디스크 이름에 대 한 설정에서 디스크를 hello *StandardLRS* 저장 및 사용 하 여 *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* hello 원본 VHD에 대 한 URI를 hello으로 합니다.

Hello에 대 한 새 리소스 그룹을 만들려면 새 VM입니다.

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

만들 hello hello에서 새 운영 체제 디스크는 VHD를 업로드 합니다. 

```powershell
$sourceUri = https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd)
$osDiskName = 'myOsDisk'
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig -AccountType StandardLRS  -Location $location -CreateOption Import `
    -SourceUri $sourceUri) `
    -ResourceGroupName $destinationResourceGroup
```

## <a name="option-2-copy-an-existing-azure-vm"></a>옵션 2: 기존 Azure VM 복사

Hello, VM의 스냅숏을 수행 하 여 관리 디스크를 사용 하 여 다음 해당 스냅숏 toocreate를 사용 하 여 새 관리 되는 디스크와 새 VM의 VM의 복사본을 만들 수 있습니다.


### <a name="take-a-snapshot-of-hello-os-disk"></a>Hello OS 디스크에 대 한 스냅숏을 만들려면

전체 VM(모든 디스크 포함) 또는 단일 디스크의 스냅숏을 만들 수 있습니다. hello 다음 단계 보여 방법을 사용 하 여 VM의 바로 hello OS 디스크의 스냅숏을 tootake hello [새로 AzureRmSnapshot](/powershell/module/azurerm.compute/new-azurermsnapshot) cmdlet. 

일부 매개 변수를 설정합니다. 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$vmName = 'myVM'
$location = 'westus' 
$snapshotName = 'mySnapshot'  
```

Hello VM 개체를 가져옵니다.

```powershell
$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $resourceGroupName
```
Hello OS 디스크 이름을 가져옵니다.

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $vm.StorageProfile.OsDisk.Name
```

Hello 스냅숏 구성을 만듭니다. 

 ```powershell
$snapshotConfig =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -OsType Windows -CreateOption Copy -Location $location 
```

Hello 스냅숏을 생성 합니다.

```powershell
$snapShot = New-AzureRmSnapshot -Snapshot $snapshotConfig -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName
```


Hello 매개 변수를 사용 하 여 toouse hello 스냅숏 toocreate toobe 높은 수행 해야 하는 VM을 하려면 `-AccountType Premium_LRS` hello AzureRmSnapshot 새로 만들기 명령을 사용 하 여 합니다. hello 매개 변수 hello 스냅숏을 생성 되어 프리미엄 관리 되는 디스크로 저장 됩니다. 프리미엄 Managed Disks는 표준 Managed Disks보다 비용이 많이 듭니다. 따라서 프리미엄 hello 매개 변수를 사용 하기 전에 게이트웨이가 필요한 해야 합니다.

### <a name="create-a-new-disk-from-hello-snapshot"></a>Hello 스냅숏에서 새 디스크 만들기

사용 하 여 스냅숏 hello에서 관리 되는 디스크를 만들 [새로 AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk)합니다. 이 예에서는 *myOSDisk* hello 디스크 이름에 대 한 합니다.

Hello에 대 한 새 리소스 그룹을 만들려면 새 VM입니다.

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

Hello OS 디스크 이름을 설정 합니다. 

```powershell
$osDiskName = 'myOsDisk'
```

Hello 관리 되는 디스크를 만듭니다.

```powershell
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig  -Location $location -CreateOption Copy `
    -SourceResourceId $snapshot.Id) `
    -ResourceGroupName $destinationResourceGroup
```


## <a name="create-hello-new-vm"></a>만들 새 VM hello 

네트워킹 및 hello에서 사용 하는 다른 VM 리소스 toobe 만들 새 VM입니다.

### <a name="create-hello-subnet-and-vnet"></a>Hello 서브넷 및 vNet 만들기

Hello vNet 및 hello의 서브넷을 만들 [가상 네트워크](../../virtual-network/virtual-networks-overview.md)합니다.

Hello 서브넷을 만듭니다. 이 예에서는 이라는 서브넷을 만듭니다 **mySubNet**, hello 리소스 그룹에 **myDestinationResourceGroup**, 집합 서브넷 주소 접두사를 너무 hello 및**10.0.0.0/24**합니다.
   
```powershell
$subnetName = 'mySubNet'
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
```

Hello vNet을 만듭니다. 이 예제에서는 집합에 가상 네트워크 이름 toobe hello **myVnetName**, 위치를 너무 hello**미국 서 부**, hello 가상 네트워크에 대 한 주소 접두사를 너무 hello 및**10.0.0.0/16**합니다. 
   
```powershell
$vnetName = "myVnetName"
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $destinationResourceGroup -Location $location `
    -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
```    


### <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Hello 네트워크 보안 그룹 및 RDP 규칙 만들기
toobe 수 toolog tooyour에서 RDP를 사용 하 여 VM을 toohave RDP 포트 3389에 대 한 액세스를 허용 하는 보안 규칙 필요 합니다. 때문에 특수화 된 기존 VM에서 새 VM을 만든 hello에 대 한 VHD를 hello, RDP에 대 한 hello 소스 가상 컴퓨터에서 계정을 사용할 수 있습니다.

이 예제에서는 집합 hello NSG 이름을 너무**myNsg** 너무 hello RDP 규칙 이름 및**myRdpRule**합니다.

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $destinationResourceGroup -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

끝점 및 NSG 규칙에 대 한 자세한 내용은 참조 [PowerShell을 사용 하 여 Azure에서 VM 포트 tooa 여](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

### <a name="create-a-public-ip-address-and-nic"></a>공용 IP 주소 및 NIC 만들기
필요한 tooenable hello 가상 네트워크의 hello 가상 컴퓨터와의 통신을는 [공용 IP 주소](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) 및 네트워크 인터페이스.

Hello 공용 IP를 만듭니다. 이 예제에서는 hello 공용 IP 주소 이름이 설정 되어 너무**myIP**합니다.
   
```powershell
$ipName = "myIP"
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $destinationResourceGroup -Location $location `
   -AllocationMethod Dynamic
```       

Hello NIC. 만들기 이 예제에서는 hello NIC 이름이 설정 되어 너무**myNicName**합니다.
   
```powershell
$nicName = "myNicName"
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $destinationResourceGroup `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```



### <a name="set-hello-vm-name-and-size"></a>Hello VM 이름 및 크기를 설정 합니다.

이 예제에서는 집합 hello VM 이름을 너무*myVM* 고 hello VM 크기 너무*Standard_A2*합니다.

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a>Hello NIC를 추가 합니다.
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    

### <a name="add-hello-os-disk"></a>Hello OS 디스크 추가 

Hello OS 디스크 toohello 구성을 사용 하 여 추가 [집합 AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk)합니다. 이 예에서는 설정 hello 디스크의 hello 크기 너무*128GB* 와 연결 합니다. hello로 관리 되는 디스크는 *Windows* OS 디스크.
 
```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -StorageAccountType StandardLRS `
    -DiskSizeInGB 128 -CreateOption Attach -Windows
```

### <a name="complete-hello-vm"></a>전체 hello VM 

사용 하 여 hello VM 만들기 [새로 AzureRMVM](/powershell/module/azurerm.compute/new-azurermvm)hello 방금 만든 구성 합니다.

```powershell
New-AzureRmVM -ResourceGroupName $destinationResourceGroup -Location $location -VM $vm
```

이 명령에 성공할 경우 다음과 유사한 출력이 표시됩니다.

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-hello-vm-was-created"></a>VM이 생성 되었고 해당 hello를 확인 합니다.
Hello 새로 만든 VM hello에 표시 되어야 [Azure 포털](https://portal.azure.com)아래 **찾아보기** > **가상 컴퓨터**, 또는 다음 PowerShell hello를 사용 하 여 명령:

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $destinationResourceGroup
$vmList.Name
```

## <a name="next-steps"></a>다음 단계
tooyour 새 가상 컴퓨터, hello에 찾아보기 toohello VM에에서 toosign [포털](https://portal.azure.com), 클릭 **연결**, 및 열기 hello RDP 원격 데스크톱 파일입니다. Tooyour 새 가상 컴퓨터에 프로그램 원래 가상 컴퓨터 toosign의 hello 계정 자격 증명을 사용 합니다. 자세한 내용은 참조 [어떻게 tooconnect 로그온 tooan Azure 가상 컴퓨터 및 Windows를 실행](connect-logon.md)합니다.

