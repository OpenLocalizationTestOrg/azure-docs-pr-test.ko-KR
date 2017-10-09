---
title: "Azure에서 일반화 된 VM의 관리 되지 않는 이미지 aaaCreate | Microsoft Docs"
description: "Azure에서의 일반화 된 Windows VM toouse toocreate 비관리 이미지로 VM의 여러 복사본을 만듭니다."
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
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: b8a044d20313efa6dd9b9757e61154f922134476
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-unmanaged-vm-image-from-an-azure-vm"></a>Azure VM에서 toocreate 관리 되지 않는 VM 이미지 하는 방법

이 문서에서는 저장소 계정을 사용하여 설명합니다. 저장소 계정 대신 관리 디스크 및 관리되는 이미지를 사용하는 것이 좋습니다. 자세한 내용은 [Azure에서 일반화된 VM의 관리되는 이미지 캡처](capture-image-resource.md)를 참조하세요.

이 문서에서는 Azure PowerShell toocreate toouse 저장소 계정을 사용 하 여 일반화 된 Azure VM의 이미지입니다. 그런 다음 다른 VM 이미지 toocreate hello를 사용할 수 있습니다. hello 이미지 hello OS 디스크 및 연결 된 toohello 가상 컴퓨터는 hello 데이터 디스크를 포함 합니다. 새 VM을 hello를 만들 때 이러한 리소스는 tooset 필요 하므로, hello 이미지 hello 가상 네트워크 리소스를 포함 하지 않습니다 됩니다. 

## <a name="prerequisites"></a>필수 조건
Toohave Azure PowerShell 버전 1.0. x 이상 버전이 설치 되어 있습니다. PowerShell을 아직 설치 하지 않은 경우 읽기 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) 설치 단계에 대 한 합니다.

## <a name="generalize-hello-vm"></a>Hello VM 일반화 
이 섹션에서는 toogeneralize 이미지 형식으로 사용할 Windows 가상 컴퓨터. VM 일반화 특히, 모든 개인 계정 정보를 제거 하 고 이미지 형식으로 사용 되는 hello 컴퓨터 toobe를 준비 합니다. Sysprep에 대 한 세부 정보를 참조 하십시오. [어떻게 tooUse Sysprep: 소개](http://technet.microsoft.com/library/bb457073.aspx)합니다.

Hello 컴퓨터에서 실행 되는 hello 서버 역할과 Sysprep에서 사용할 수 있는지 확인 합니다. 자세한 내용은 [서버 역할에 대한 Sysprep 지원](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)

> [!IMPORTANT]
> 업로드 하는 경우 프로그램 VHD tooAzure hello에 대 한 처음으로, 했는지 확인 [VM 준비](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Sysprep를 실행 하기 전에. 
> 
> 

사용 하 여 Linux VM을 일반화할 수 있습니다 `sudo waagent -deprovision+user` 다음 PowerShell toocapture hello VM을 사용 합니다. Hello CLI toocapture VM을 사용 하는 방법에 대 한 정보를 참조 하십시오. [어떻게 toogeneralize 및 사용 하 여 Linux 가상 컴퓨터 캡처 hello Azure CLI ](../linux/capture-image.md)합니다.


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

## <a name="log-in-tooazure-powershell"></a>PowerShell tooAzure 로그인
1. Azure PowerShell을 열고 tooyour Azure 계정에에서 로그인 합니다.
   
    ```powershell
    Login-AzureRmAccount
    ```
   
    Azure 계정 자격을 증명 tooenter 있습니다에 대 한 팝업 창이 열립니다.
2. 사용 가능한 구독에 대 한 hello 구독을 Id를 가져옵니다.
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. Hello 구독 id입니다.를 사용 하 여 hello 올바른 구독 설정
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="deallocate-hello-vm-and-set-hello-state-toogeneralized"></a>Hello VM 할당 취소 하 고 hello 상태 toogeneralized 설정
1. Hello VM 리소스 할당이 취소 되었습니다.
   
    ```powershell
    Stop-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName>
    ```
   
    hello *상태* hello Azure에에서 VM hello에 대 한 포털에서 변경 **Stopped** 너무**중지 됨 (할당 취소 됨)**합니다.
2. Hello 가상 컴퓨터의 hello 상태를 너무 설정**일반화 됨으로**합니다. 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName <resourceGroup> -Name <vmName> -Generalized
    ```
3. Hello VM의 hello 상태를 확인 합니다. hello **OSState/일반화** hello VM hello 있어야에 대 한 섹션 **DisplayStatus** 도**VM 일반화**합니다.  
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName> -Status
    $vm.Statuses
    ```

## <a name="create-hello-image"></a>Hello 이미지 만들기

이 명령을 사용 하 여 hello 대상 저장소 컨테이너에 관리 되지 않는 가상 컴퓨터 이미지를 만듭니다. hello 이미지가 만들어지고 hello에 동일한 저장소 계정으로 원본 가상 컴퓨터가 hello 합니다. hello `-Path` hello 소스 VM tooyour 로컬 컴퓨터에 대 한 hello JSON 서식 파일의 복사본을 저장 하는 매개 변수입니다. hello `-DestinationContainerName` 매개 변수는 hello 컨테이너 되도록 toohold 이미지의 hello 이름입니다. Hello 컨테이너가 존재 하지 않는 사용자에 대해 만들어집니다.
   
```powershell
Save-AzureRmVMImage -ResourceGroupName <resourceGroupName> -Name <vmName> `
    -DestinationContainerName <destinationContainerName> -VHDNamePrefix <templateNamePrefix> `
    -Path <C:\local\Filepath\Filename.json>
```
   
Hello JSON 파일 서식 파일에서 이미지의 hello URL을 가져올 수 있습니다. Toohello 이동 **리소스** > **storageProfile** > **osDisk** > **이미지**  >  **uri** hello 전체 경로 대 한 이미지의 섹션입니다. 다음과 같은 hello 이미지의 URL hello: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`합니다.
   
또한 hello URI hello 포털에서 확인할 수 있습니다. hello 이미지는 복사한 tooa 컨테이너인 **시스템** 저장소 계정에 있습니다. 

## <a name="create-a-vm-from-hello-image"></a>Hello 이미지에서 VM 만들기

이제 hello 관리 되지 않는 이미지에서 하나 이상의 가상 컴퓨터를 만들 수 있습니다.

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
hello 다음 PowerShell hello 가상 컴퓨터 구성 및 관리 되지 않는 이미지를 새로 설치 하는 hello에 대 한 hello 원본으로 사용 합니다.

</br>

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

### <a name="verify-that-hello-vm-was-created"></a>VM이 생성 되었고 해당 hello를 확인 합니다.
새로 만든 VM의 hello hello 나타나야 완료 되 면 [Azure 포털](https://portal.azure.com) 아래 **찾아보기** > **가상 컴퓨터**, 또는 hello 다음을 사용 하 여 PowerShell 명령:

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a>다음 단계
Azure PowerShell을 사용한 새 가상 컴퓨터에 참조 toomanage [Azure 리소스 관리자 및 PowerShell을 사용 하 여 가상 컴퓨터를 관리](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.


