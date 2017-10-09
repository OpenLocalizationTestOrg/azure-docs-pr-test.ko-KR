---
title: "Azure에서 관리 되는 VM 이미지에서 VM aaaCreate | Microsoft Docs"
description: "Hello 리소스 관리자 배포 모델에서 Azure PowerShell을 사용 하는 일반화 된 관리 되는 VM 이미지에서 Windows 가상 컴퓨터를 만듭니다."
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
ms.date: 05/22/2017
ms.author: cynthn
ms.openlocfilehash: 5036ef1533c144a9a328e94599b359e0166f337d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-managed-image"></a>관리되는 이미지에서 VM 만들기

Azure에서 관리 VM 이미지로 여러 VM을 만들 수 있습니다. 관리 되는 VM 이미지 hello 정보 필요한 toocreate hello OS 및 데이터 디스크를 포함 하 여 VM을 포함 합니다. hello Vhd hello 운영 체제 디스크와 모든 데이터 디스크를 포함 하는 hello 이미지를 구성 하는 관리 되는 디스크도 저장 됩니다. 


## <a name="prerequisites"></a>필수 조건

이미 toohave 필요한 [관리 되는 VM 이미지를 만들어](capture-image-resource.md) 작성용 toouse hello 새 VM입니다. 

Hello hello AzureRM.Compute 및 AzureRM.Network PowerShell 모듈의 최신 버전이 있는지 확인 합니다. 관리자 권한으로 PowerShell 프롬프트를 열고 다음 명령 tooinstall hello를 실행 하 합니다.

```powershell
Install-Module AzureRM.Compute,AzureRM.Network
```
자세한 내용은 [Azure PowerShell 버전 관리](/powershell/azure/overview)를 참조하세요.



## <a name="collect-information-about-hello-image"></a>Hello 이미지에 대 한 정보를 수집 합니다.

먼저 toogather hello 이미지에 대 한 기본 정보가 필요 하 고 hello 이미지에 대 한 변수를 만듭니다. 이 예에서는 이라는 관리 되는 VM 이미지를 사용 하 여 **myImage** 에 hello 즉 **myResourceGroup** hello의 리소스 그룹 **중앙 미국 서 부** 위치 합니다. 

```powershell
$rgName = "myResourceGroup"
$location = "West Central US"
$imageName = "myImage"
$image = Get-AzureRMImage -ImageName $imageName -ResourceGroupName $rgName
```

## <a name="create-a-virtual-network"></a>가상 네트워크 만들기
Hello vNet 및 hello의 서브넷을 만들 [가상 네트워크](../../virtual-network/virtual-networks-overview.md)합니다.

1. Hello 서브넷을 만듭니다. 이 예에서는 이라는 서브넷을 만듭니다 **mySubnet** hello 주소 접두사와 **10.0.0.0/24**합니다.  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Hello 가상 네트워크를 만듭니다. 이 예제에서는 명명 된 가상 네트워크를 만들어 **myVnet** hello 주소 접두사와 **10.0.0.0/16**합니다.  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a>공용 IP 주소 및 네트워크 인터페이스 만들기

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

## <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Hello 네트워크 보안 그룹 및 RDP 규칙 만들기

toobe 수 toolog tooyour에서 RDP를 사용 하 여 VM을 toohave RDP 포트 3389에 대 한 액세스를 허용 하는 네트워크 보안 규칙 (NSG) 필요 합니다. 

이 예에서는 포트 3389를 통한 RDP 트래픽을 허용하는 **myRdpRule**이라는 규칙을 포함하는 **myNsg**로 명명된 NSG를 만듭니다. Nsg에 대 한 자세한 내용은 참조 [PowerShell을 사용 하 여 Azure에서 VM 포트 tooa 여](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

```powershell
$nsgName = "myNsg"
$ruleName = "myRdpRule"
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


## <a name="create-a-variable-for-hello-virtual-network"></a>Hello 가상 네트워크에 대 한 변수 만들기

가상 네트워크를 완료 하는 hello에 대 한 변수를 만듭니다. 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-hello-credentials-for-hello-vm"></a>Hello VM에 대 한 hello 자격 증명 가져오기

hello 다음 cmdlet이 열립니다 입력할 수 있는 새 사용자 이름 및 암호 toouse hello 로컬 관리자 계정으로 원격으로 hello VM에 액세스 하기 위한 창. 

```powershell
$cred = Get-Credential
```

## <a name="set-variables-for-hello-vm-name-computer-name-and-hello-size-of-hello-vm"></a>Hello VM에 대 한 설정 변수 이름, 컴퓨터 이름 및 hello hello VM의 크기

1. Hello VM 이름 및 컴퓨터 이름에 대 한 변수를 만듭니다. Hello VM 이름으로 설정 하는이 예제 **myVM** 및 컴퓨터 이름으로 hello **myComputer**합니다.

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    ```
2. Hello 가상 컴퓨터의 hello 크기를 설정 합니다. 이 예제에서는 **Standard_DS1_v2** 크기의 VM을 만듭니다. Hello 참조 [VM 크기](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) 자세한 정보에 대 한 설명서입니다.

    ```powershell
    $vmSize = "Standard_DS1_v2"
    ```

3. Hello VM 이름 및 크기 toohello VM 구성에 추가 합니다.

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a>Hello에 대 한 원본 이미지로 집합 hello VM 이미지 새 VM

관리 되는 hello VM 이미지의 hello ID를 사용 하 여 hello 소스 이미지를 설정 합니다.

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a>운영 체제 구성 hello를 설정 하 고 hello NIC. 추가

Hello 저장소 유형 (PremiumLRS 또는 StandardLRS)와 hello OS 디스크의 hello 크기를 입력 합니다. 이 예에서는 설정 hello 계정 유형 너무**PremiumLRS**, 디스크 크기를 너무 hello**128GB** 및 디스크 캐싱에 너무**ReadWrite**합니다.

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm  -StorageAccountType PremiumLRS -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a>Hello VM 만들기

만들 작성 했으며 hello에 저장 하는 hello 구성을 사용 하 여 새 Vm hello **$vm** 변수입니다.

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-hello-vm-was-created"></a>VM이 생성 되었고 해당 hello를 확인 합니다.
새로 만든 VM의 hello hello 나타나야 완료 되 면 [Azure 포털](https://portal.azure.com) 아래 **찾아보기** > **가상 컴퓨터**, 또는 hello 다음을 사용 하 여 PowerShell 명령:

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a>다음 단계
Azure PowerShell을 사용한 새 가상 컴퓨터에 참조 toomanage [만들기 hello Azure PowerShell 모듈을 사용 하 여 Windows Vm을 관리 하 고](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

