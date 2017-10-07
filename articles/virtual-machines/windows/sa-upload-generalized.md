---
title: "aaaUpload 일반화 VHD toocreate Azure에서 여러 Vm | Microsoft Docs"
description: "일반화 된 VHD tooan Azure 저장소 계정 toocreate hello 리소스 관리자 배포 모델에 Windows VM toouse를 업로드 합니다."
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
ms.date: 05/18/2017
ms.author: cynthn
ms.openlocfilehash: aa1af2a0acf81685e62853de71afa51e819cb696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-generalized-vhd-tooazure-toocreate-a-new-vm"></a>일반화 된 VHD tooAzure toocreate 새 VM을 업로드 합니다.

이 항목에서는 관리 되지 않는 디스크를 일반화 된 tooa 저장소 계정을 업로드 하 고 다음 업로드 hello 디스크를 사용 하 여 새 VM을 만들어 다룹니다. 일반화된 VHD 이미지에는 Sysprep을 사용하여 제거된 모든 개인 계정 정보가 포함되어 있습니다. 

저장소 계정에는 특수 한 VHD에서 VM toocreate 참조 [특수 VHD에서 VM 만들기](sa-create-vm-specialized.md)합니다.

이 항목에서는 저장소 계정을 사용 하 여 있지만 고객 대신 toousing 관리 하는 디스크를 이동 하는 것이 좋습니다. 전체 연습 tooprepare, 업로드 하 고 사용 하 여 새 VM을 만드는 방법의 디스크 관리에 대 한 참조 [관리 하는 디스크를 사용 하 여 일반화 된 VHD 업로드 tooAzure에서 새 VM 만들기](upload-generalized-managed.md)합니다.



## <a name="prepare-hello-vm"></a>Hello VM 준비

일반화된 VHD에는 Sysprep을 사용하여 제거된 모든 개인 계정 정보가 포함되어 있습니다. Toouse hello VHD 이미지 toocreate로 가져오려는 경우에서 새 Vm을 수행 해야 합니다.
  
  * [Windows VHD tooupload tooAzure 준비](prepare-for-upload-vhd-image.md)합니다. 
  * Sysprep를 사용 하 여 hello 가상 컴퓨터를 일반화 합니다.

### <a name="generalize-a-windows-virtual-machine-using-sysprep"></a>Sysprep을 사용하여 Windows 가상 컴퓨터 일반화
이 섹션에서는 toogeneralize 이미지 형식으로 사용할 Windows 가상 컴퓨터. Sysprep는 특히, 모든 개인 계정 정보를 제거 하 고 이미지 형식으로 사용 되는 hello 컴퓨터 toobe를 준비 합니다. Sysprep에 대 한 세부 정보를 참조 하십시오. [어떻게 tooUse Sysprep: 소개](http://technet.microsoft.com/library/bb457073.aspx)합니다.

Hello 컴퓨터에서 실행 되는 hello 서버 역할과 Sysprep에서 사용할 수 있는지 확인 합니다. 자세한 내용은 [서버 역할에 대한 Sysprep 지원](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)

> [!IMPORTANT]
> 를 사용 하 여 VHD tooAzure hello에 대 한 처음으로 업로드 하기 전에 Sysprep를 실행 하는 경우 했는지 확인 [VM 준비](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Sysprep를 실행 하기 전에. 
> 
> 

1. Windows 가상 컴퓨터 toohello에 로그인 합니다.
2. Hello 명령 프롬프트 창을 관리자 권한으로 엽니다. Hello 디렉터리도 변경**%windir%\system32\sysprep**, 한 다음 실행 `sysprep.exe`합니다.
3. Hello에 **시스템 준비 도구** 대화 상자에서 **입력 시스템을 기본 OOBE (Experience)**, 해당 hello 있는지 확인 하 고 **일반화** 확인란을 선택 합니다.
4. **종료 옵션**에서 **종료**를 선택합니다.
5. **확인**을 클릭합니다.
   
    ![Sysprep 시작](./media/upload-generalized-managed/sysprepgeneral.png)
6. Sysprep이 완료 된 hello 가상 컴퓨터를 종료 합니다. 

> [!IMPORTANT]
> 업로드 완료 hello VHD tooAzure 또는 hello VM에서에서 이미지를 만들 때까지 VM hello를 다시 시작 하지 않습니다. Hello VM 실수로 가져옵니다 다시 시작, 실행 Sysprep toogeneralize 다시 합니다.
> 
> 


## <a name="upload-hello-vhd"></a>Hello VHD 업로드

Hello VHD tooan Azure 저장소 계정에 업로드 합니다.

### <a name="log-in-tooazure"></a>TooAzure 로그인
PowerShell 버전 1.4가 없는 이상 읽기 설치 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.

1. Azure PowerShell을 열고 tooyour Azure 계정에에서 로그인 합니다. Azure 계정 자격을 증명 tooenter 있습니다에 대 한 팝업 창이 열립니다.
   
    ```powershell
    Login-AzureRmAccount
    ```
2. 사용 가능한 구독에 대 한 hello 구독을 Id를 가져옵니다.
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. Hello 구독 id입니다.를 사용 하 여 hello 올바른 구독 설정 대체 `<subscriptionID>` hello hello ID로 구독을 수정 합니다.
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

### <a name="get-hello-storage-account"></a>Hello 저장소 계정 가져오기
Azure toostore 업로드 hello VM 이미지에 저장소 계정이 필요합니다. 기존 저장소 계정을 사용하거나 새 계정을 만들 수 있습니다. 

tooshow hello 사용 가능한 저장소 계정을 입력 합니다.

```powershell
Get-AzureRmStorageAccount
```

Toouse 기존 저장소 계정을 사용할 경우 진행 toohello [hello VM 이미지 업로드](#upload-the-vm-vhd-to-your-storage-account) 섹션.

저장소 계정 toocreate 해야 할 경우 다음이 단계를 따르십시오.

1. Hello 저장소 계정을 만들어야 하는 hello 리소스 그룹의 hello 이름이 필요 합니다. 구독을 형식에 있는 모든 hello 리소스 그룹 아웃 toofind:
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    리소스 그룹 이름이 toocreate **myResourceGroup** hello에 **미국 서 부** 지역, 유형:

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. 라는 저장소 계정 만들기 **mystorageaccount** hello를 사용 하 여이 리소스 그룹에 [새로 AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
 
### <a name="start-hello-upload"></a>Hello 업로드를 시작 합니다. 

사용 하 여 hello [추가 AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) 저장소 계정의 cmdlet tooupload hello 이미지 tooa 컨테이너입니다. 이 예에서는 업로드 파일 hello **myVHD.vhd** 에서 `"C:\Users\Public\Documents\Virtual hard disks\"` tooa 저장소 계정인 **mystorageaccount** hello에 **myResourceGroup** 리소스 그룹입니다. hello 파일 라는 hello 컨테이너에 배치 됨 **mycontainer** hello 새 파일 이름이 됩니다 **myUploadedVHD.vhd**합니다.

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
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

이 명령은 네트워크 연결 및 VHD 파일의 hello 크기에 따라 시간이 걸릴 수 있습니다 toocomplete 합니다.


## <a name="create-a-new-vm"></a>새 VM 만들기 

사용 하 여 hello VHD toocreate 새 VM을 업로드 하는 이제 할 수 있습니다. 

### <a name="set-hello-uri-of-hello-vhd"></a>Hello hello VHD의 URI를 설정 합니다.

VHD toouse hello에 대 한 hello URI는 hello 형식: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd 합니다. 이 예에서 hello 라는 VHD **myVHD** hello 저장소 계정에는 **mystorageaccount** hello 컨테이너에 **mycontainer**합니다.

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a>가상 네트워크 만들기
Hello vNet 및 hello의 서브넷을 만들 [가상 네트워크](../../virtual-network/virtual-networks-overview.md)합니다.

1. Hello 서브넷을 만듭니다. hello 다음 샘플 서브넷을 만듭니다. 명명 된 **mySubnet** hello 리소스 그룹에 **myResourceGroup** hello 주소 접두사와 **10.0.0.0/24**합니다.  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Hello 가상 네트워크를 만듭니다. hello 다음 샘플 가상 네트워크를 만들어 명명 된 **myVnet** hello에 **West US** hello 주소 접두사를 사용 하 여 위치 **10.0.0.0/16**합니다.  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a>공용 IP 주소 및 네트워크 인터페이스 만들기
필요한 tooenable hello 가상 네트워크의 hello 가상 컴퓨터와의 통신을는 [공용 IP 주소](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) 및 네트워크 인터페이스.

1. 공용 IP 주소 만들기. 이 예에서는 **myPip**라는 공용 IP 주소를 만듭니다. 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. Hello NIC. 만들기 이 예에서는 **myNic**라는 NIC를 만듭니다. 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Hello 네트워크 보안 그룹 및 RDP 규칙 만들기
toobe 수 toolog tooyour에서 RDP를 사용 하 여 VM을 toohave RDP 포트 3389에 대 한 액세스를 허용 하는 보안 규칙 필요 합니다. 

이 예에서는 포트 3389를 통한 RDP 트래픽을 허용하는 **myRdpRule**이라는 규칙을 포함하는 **myNsg**로 명명된 NSG를 만듭니다. Nsg에 대 한 자세한 내용은 참조 [PowerShell을 사용 하 여 Azure에서 VM 포트 tooa 여](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-hello-virtual-network"></a>Hello 가상 네트워크에 대 한 변수 만들기
가상 네트워크를 완료 하는 hello에 대 한 변수를 만듭니다. 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-hello-vm"></a>Hello VM 만들기
hello 다음 PowerShell 스크립트에서는 tooset hello 가상 컴퓨터 구성 및 사용 하 여 hello를 새로 설치 하는 hello에 대 한 hello 소스로 VM 이미지를 업로드 하는 방법



```powershell
# Enter a new user name and password toouse as hello local administrator account 
    # for remotely accessing hello VM.
    $cred = Get-Credential

    # Name of hello storage account where hello VHD is located. This example sets hello 
    # storage account name as "myStorageAccount"
    $storageAccName = "myStorageAccount"

    # Name of hello virtual machine. This example sets hello VM name as "myVM".
    $vmName = "myVM"

    # Size of hello virtual machine. This example creates "Standard_D2_v2" sized VM. 
    # See hello VM sizes documentation for more information: 
    # https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/
    $vmSize = "Standard_D2_v2"

    # Computer name for hello VM. This examples sets hello computer name as "myComputer".
    $computerName = "myComputer"

    # Name of hello disk that holds hello OS. This example sets hello 
    # OS disk name as "myOsDisk"
    $osDiskName = "myOsDisk"

    # Assign a SKU name. This example sets hello SKU name as "Standard_LRS"
    # Valid values for -SkuName are: Standard_LRS - locally redundant storage, Standard_ZRS - zone redundant
    # storage, Standard_GRS - geo redundant storage, Standard_RAGRS - read access geo redundant storage,
    # Premium_LRS - premium locally redundant storage. 
    $skuName = "Standard_LRS"

    # Get hello storage account where hello uploaded image is stored
    $storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $rgName -AccountName $storageAccName

    # Set hello VM name and size
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

    #Set hello Windows operating system configuration and add hello NIC
    $vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

    # Create hello OS disk URI
    $osDiskUri = '{0}vhds/{1}-{2}.vhd' `
        -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName

    # Configure hello OS disk toobe created from hello existing VHD image (-CreateOption fromImage).
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri `
        -CreateOption fromImage -SourceImageUri $imageURI -Windows

    # Create hello new VM
    New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

## <a name="verify-that-hello-vm-was-created"></a>VM이 생성 되었고 해당 hello를 확인 합니다.
새로 만든 VM의 hello hello 나타나야 완료 되 면 [Azure 포털](https://portal.azure.com) 아래 **찾아보기** > **가상 컴퓨터**, 또는 hello 다음을 사용 하 여 PowerShell 명령:

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a>다음 단계
Azure PowerShell을 사용한 새 가상 컴퓨터에 참조 toomanage [Azure 리소스 관리자 및 PowerShell을 사용 하 여 가상 컴퓨터를 관리](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.


