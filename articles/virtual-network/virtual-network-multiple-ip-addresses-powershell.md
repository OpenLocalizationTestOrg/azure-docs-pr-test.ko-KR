---
title: "Azure 가상 컴퓨터-PowerShell aaaMultiple IP 주소 | Microsoft Docs"
description: "어떻게 tooassign 여러 IP 주소에 대해 알아봅니다 PowerShell을 사용 하 여 tooa 가상 컴퓨터 | 리소스 관리자입니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c44ea62f-7e54-4e3b-81ef-0b132111f1f8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/24/2017
ms.author: jdial;annahar
ms.openlocfilehash: df54c4386ce13521e660a3e7208c8c1ab1459bc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-powershell"></a>PowerShell을 사용 하 여 toovirtual 컴퓨터 여러 IP 주소를 할당 합니다.

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

이 문서에서는 PowerShell을 사용 하 여 toocreate hello Azure 리소스 관리자 배포를 통해 가상 컴퓨터 (VM)을 모델링 하는 방법을 설명 합니다. Hello 클래식 배포 모델을 통해 만든 tooresources 여러 IP 주소를 할당할 수 없습니다. Azure 배포 모델을 읽을 hello에 대 한 자세한 toolearn [배포 모델을 이해](../resource-manager-deployment-model.md) 문서.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>여러 IP 주소를 사용하여 VM 만들기

수행 하는 hello 단계 hello 시나리오에 설명 된 대로 toocreate 예로 여러 IP 사용 하 여 VM 해결 하는 방법을 설명 합니다. 변수 값을 구현에 필요한 대로 변경합니다.

1. PowerShell 명령 프롬프트를 열고 단일 PowerShell 세션 내에서이 섹션의 단계를 완료 hello 남은 합니다. PowerShell 설치 및 구성, 아직 없는 경우 전체 hello hello의 단계를 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) 문서.
2. Hello로 로그인 tooyour 계정 `login-azurermaccount` 명령입니다.
3. *myResourceGroup* 및 *westus*를 선택한 이름과 위치로 바꿉니다. 리소스 그룹을 만듭니다. 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.

    ```powershell
    $RgName   = "MyResourceGroup"
    $Location = "westus"

    New-AzureRmResourceGroup `
    -Name $RgName `
    -Location $Location
    ```

4. 서브넷을 가상 네트워크 (VNet) 만들고 hello에 같은 hello 리소스 그룹 위치:

    ```powershell
    
    # Create a subnet configuration
    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name MySubnet `
    -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $VNet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $RgName `
    -Location $Location `
    -Name MyVNet `
    -AddressPrefix 10.0.0.0/16 `
    -Subnet $subnetConfig

    # Get hello subnet object
    $Subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $SubnetConfig.Name -VirtualNetwork $VNet
    ```

5. NSG(네트워크 보안 그룹) 및 규칙을 만듭니다. hello VM을 보호 하는 hello NSG 인바운드 및 아웃 바운드 규칙을 사용 하 여 합니다. 이 경우 포트 3389에 대해 들어오는 원격 데스크톱 연결을 허용하는 인바운드 규칙이 만들어집니다.

    ```powershell
    
    # Create an inbound network security group rule for port 3389

    $NSGRule = New-AzureRmNetworkSecurityRuleConfig `
    -Name MyNsgRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 -Access Allow
    
    # Create a network security group
    $NSG = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $RgName `
    -Location $Location `
    -Name MyNetworkSecurityGroup `
    -SecurityRules $NSGRule
    ```

6. Hello NIC. hello에 대 한 기본 IP 구성 정의 이전에 정의 된 hello 값을 사용 하지 않은 경우 만든 hello 서브넷에 tooa 유효한 주소 10.0.0.4 변경 합니다. 고정 IP 주소를 할당하기 전에 먼저 해당 주소를 이미 사용하고 있지 않은지 확인하는 것이 좋습니다. Hello 명령을 입력 `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`합니다. Hello 출력 반환 hello 주소를 사용할 수 있는 경우 *True*합니다. Hello 출력 반환 사용할 수 없는 경우 *False* 및 사용할 수 있는 주소 목록이 있습니다. 

    Hello 명령 뒤에 **hello 고유 DNS 이름 toouse < 바꾸기-와-사용자-고유-이름 > 바꿉니다.** hello 이름은 모든 공용 IP 주소는 Azure 지역 내에서 고유 해야 합니다. 선택적 매개 변수입니다. Tooconnect toohello VM만 하려는 경우 제거할 수 있는 hello 공용 IP 주소를 사용 하 여 합니다.

    ```powershell
    
    # Create a public IP address
    $PublicIP1 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP1" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -DomainNameLabel <replace-with-your-unique-name> `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign hello public IP ddress tooit
    $IpConfigName1 = "IPConfig-1"
    $IpConfig1     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName1 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.4 `
    -PublicIpAddress $PublicIP1 `
    -Primary
    ```

    Hello로 구성 중 하나를 할당 해야 여러 IP 구성은 tooa NIC에 할당 하면 *-주*합니다.

    > [!NOTE]
    > 공용 IP 주소에는 명목 요금이 부과됩니다. 가격 책정, 주소 IP에 대 한 자세한 toolearn 읽을 hello [IP 주소 가격](https://azure.microsoft.com/pricing/details/ip-addresses) 페이지. 구독에서 사용할 수 있는 공용 IP 주소의 제한이 toohello 수가입니다. hello 제한, hello 읽기에 대 한 자세한 toolearn [Azure 제한](../azure-subscription-service-limits.md#networking-limits) 문서.

7. Hello NIC. hello에 대 한 보조 IP 구성 정의 필요에 따라 구성을 추가 또는 제거할 수 있습니다. 각 IP 구성에 개인 IP 주소가 할당되어야 합니다. 경우에 따라 각 구성에 공용 IP 주소가 할당될 수 있습니다.

    ```powershell
    
    # Create a public IP address
    $PublicIP2 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP2" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign hello public IP ddress tooit
    $IpConfigName2 = "IPConfig-2"
    $IpConfig2     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName2 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.5 `
    -PublicIpAddress $PublicIP2
        
    $IpConfigName3 = "IpConfig-3"
    $IpConfig3 = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IPConfigName3 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.6
    ```

8. Hello NIC를 만들고 세 가지 IP 구성을 tooit hello 연결 합니다.

    ```powershell
    
    $NIC = New-AzureRmNetworkInterface `
    -Name MyNIC `
    -ResourceGroupName $RgName `
    -Location $Location `
    -NetworkSecurityGroupId $NSG.Id `
    -IpConfiguration $IpConfig1,$IpConfig2,$IpConfig3
    ```

    >[!NOTE]
    >모든 구성의 경우이 문서의 tooone NIC에 할당 되어 있지만 여러 IP 구성은 tooevery 연결 된 NIC toohello VM을 할당할 수 있습니다. 여러 Nic 사용 하 여 VM toocreate 읽으려면 어떻게 toolearn hello [여러 nic가 있는 VM을 만들](virtual-network-deploy-multinic-arm-ps.md) 문서.

9. Hello 다음 명령을 입력 하 여 hello VM을 만듭니다.

    ```powershell
    
    # Define a credential object. When you run these commands, you're prompted tooenter a sername and password for hello VM you're reating.
    $cred = Get-Credential
    
    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
    -VMName MyVM `
    -VMSize Standard_DS1_v2 | `
    Set-AzureRmVMOperatingSystem -Windows `
    -ComputerName MyVM `
    -Credential $cred | `
    Set-AzureRmVMSourceImage `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest | `
    Add-AzureRmVMNetworkInterface `
    -Id $NIC.Id
    
    # Create hello VM
    New-AzureRmVM `
    -ResourceGroupName $RgName `
    -Location $Location `
    -VM $VmConfig
    ```

10. 추가 hello 개인 IP 주소 수 toohello VM 운영 체제 hello에 운영 체제에 대 한 hello 단계를 완료 [추가 IP 주소 tooa VM 운영 체제](#os-config) 이 문서의 섹션. Hello 공용 IP 주소 toohello 운영 체제를 추가 하지 마십시오.

## <a name="add"></a>IP 주소 tooa VM 추가

개인 및 공용 IP 주소 tooa NIC를 수행 하는 hello 단계를 완료 하 여 추가할 수 있습니다. hello hello 다음 섹션의에서 예제에서는 이미 있다고 가정 VM hello에 설명 된 hello 3 IP 구성이 [시나리오](#Scenario) 이 문서에서는 하지만 필요 하지는 않도록 합니다.

1. PowerShell 명령 프롬프트를 열고 단일 PowerShell 세션 내에서이 섹션의 단계를 완료 hello 남은 합니다. PowerShell 설치 및 구성, 아직 없는 경우 전체 hello hello의 단계를 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) 문서.
2. Hello hello tooadd IP 주소 tooand hello 리소스 그룹 및 위치 hello NIC에 있는 원하는 NIC $Variables toohello 이름 뒤의 "값" hello를 변경 합니다.

    ```powershell
    $NicName  = "MyNIC"
    $RgName   = "MyResourceGroup"
    $Location = "westus"
    ```

    Hello toochange 원하는 NIC의 hello 이름을 모르면 hello 다음 명령을 입력 한 다음 hello hello 이전 변수 값을 변경:

    ```powershell
    Get-AzureRmNetworkInterface | Format-Table Name, ResourceGroupName, Location
    ```
3. 변수를 만들고 NIC hello 다음 명령을 입력 하 여 기존 toohello를 설정 합니다.

    ```powershell
    $MyNIC = Get-AzureRmNetworkInterface -Name $NicName -ResourceGroupName $RgName
    ```
4. Hello 명령 뒤에서 변경 *MyVNet* 및 *MySubnet* toohello 형태의 hello VNet과 서브넷 hello NIC에 연결 되어 있습니다. Hello 명령을 tooretrieve hello VNet과 서브넷 개체 hello NIC에 연결 되어 입력 합니다.

    ```powershell
    $MyVNet = Get-AzureRMVirtualnetwork -Name MyVNet -ResourceGroupName $RgName
    $Subnet = $MyVnet.Subnets | Where-Object { $_.Name -eq "MySubnet" }
    ```
    Hello VNet 또는 서브넷 이름 hello에 연결 된 NIC를 모르는 경우 hello 다음 명령을 입력 합니다.
    ```powershell
    $MyNIC.IpConfigurations
    ```
    Hello 출력 예제 출력 다음 텍스트와 유사한 toohello 나타나는지 확인 합니다.
    
    ```
    "Id": "/subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/MyVNet/subnets/MySubnet"
    ```
    이 출력에 *MyVnet* 는 VNet hello 및 *MySubnet* 는 hello 서브넷 hello NIC에 연결 되어 있습니다.

5. Hello 절, 요구 사항에 따라 다음 중 하나의 hello 단계를 완료 합니다.

    **개인 IP 주소 추가**

    개인 IP 주소 tooa NIC tooadd IP 구성을 만들어야 합니다. hello 다음 명령은 구성을 10.0.0.7 고정 IP 주소를 사용 합니다. 고정 IP 주소를 지정할 때는 hello 서브넷에 대 한 사용 되지 않는 주소 여야 합니다. Hello 주소 tooensure hello를 입력 하 여 사용할 수는 먼저 테스트 하는 것이 좋습니다. `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet` 명령입니다. Hello 출력 반환 hello IP 주소를 사용할 수 있는 경우 *True*합니다. Hello 출력 반환 사용할 수 없는 경우 *False*, 및 사용할 수 있는 주소 목록이 있습니다.

    ```powershell
    Add-AzureRmNetworkInterfaceIpConfig -Name IPConfig-4 -NetworkInterface `
    $MyNIC -Subnet $Subnet -PrivateIpAddress 10.0.0.7
    ```
    고유한 구성 이름과 개인 IP 주소를 사용하여 필요한 만큼 구성을 만듭니다(정적 IP 주소를 가진 구성의 경우).

    Hello에 운영 체제에는 hello 단계를 완료 하 여 hello 개인 IP 주소 toohello VM 운영 체제 추가 [추가 IP 주소 tooa VM 운영 체제](#os-config) 이 문서의 섹션.

    **공용 IP 주소 추가**

    공용 IP 주소는 새 IP 구성 또는 기존 IP 구성에 공용 IP 주소 리소스 tooeither를 연결 하 여 추가 됩니다. 필요한 만큼 따르려면 hello 섹션 중 하나에 hello 단계를 완료 합니다.

    > [!NOTE]
    > 공용 IP 주소에는 명목 요금이 부과됩니다. 가격 책정, 주소 IP에 대 한 자세한 toolearn 읽을 hello [IP 주소 가격](https://azure.microsoft.com/pricing/details/ip-addresses) 페이지. 구독에서 사용할 수 있는 공용 IP 주소의 제한이 toohello 수가입니다. hello 제한, hello 읽기에 대 한 자세한 toolearn [Azure 제한](../azure-subscription-service-limits.md#networking-limits) 문서.
    >

    - **Hello 공용 IP 주소 리소스 tooa 새 IP 구성에 연결**
    
        새 IP 구성의 공용 IP 주소를 추가할 때마다 모든 IP 구성 시 개인 IP 주소가 있어야 하기 때문에 개인 IP 주소도 추가해야 합니다. 기존 공용 IP 주소 리소스를 추가하거나 새로 만들 수 있습니다. toocreate 한 새 hello 다음 명령을 입력 합니다.
    
        ```powershell
        $myPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "myPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location `
        -AllocationMethod Static
        ```

        개인 고정 IP 주소와 연결 된 hello 새 IP 구성이 toocreate *myPublicIp3* 공용 IP 리소스에 주소를 hello 다음 명령을 입력 합니다.

        ```powershell
        Add-AzureRmNetworkInterfaceIpConfig `
        -Name IPConfig-4 `
        -NetworkInterface $myNIC `
        -Subnet $Subnet `
        -PrivateIpAddress 10.0.0.7 `
        -PublicIpAddress $myPublicIp3
        ```

    - **Hello 공용 IP 주소 리소스 tooan 기존 IP 구성에 연결**

        공용 IP 주소 리소스에 아직 연결 되어 관련된 tooan IP 구성만 가능 합니다. IP 구성 hello 다음 명령을 입력 하 여 연결 된 공용 IP 주소에 있는지 여부를 확인할 수 있습니다.

        ```powershell
        $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
        ```

        유사한 toohello 다음 출력이 표시 됩니다.

        ```     
        Name       PrivateIpAddress PublicIpAddress                                           Primary
        
        IPConfig-1 10.0.0.4         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress    True
        IPConfig-2 10.0.0.5         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress   False
        IpConfig-3 10.0.0.6                                                                     False
        ```

        Hello 이후 **PublicIpAddress** 열에 대 한 *IpConfig-3* 은 공백은, 공용 IP 주소 리소스가 현재 연결된 tooit입니다. 기존 공용 IP 주소 리소스 tooIpConfig-3, 더하거나 명령 toocreate 하나를 수행 하는 hello 입력:

        ```powershell
        $MyPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "MyPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location -AllocationMethod Static
        ```

        다음 명령을 tooassociate hello 공용 IP 주소 리소스 toohello 기존 IP 구성 라는 hello 입력 *IpConfig-3*:
    
        ```powershell
        Set-AzureRmNetworkInterfaceIpConfig `
        -Name IpConfig-3 `
        -NetworkInterface $mynic `
        -Subnet $Subnet `
        -PublicIpAddress $myPublicIp3
        ```

6. Hello 다음 명령을 입력 하 여 hello 새 IP 구성 사용 하 여 hello NIC를 설정 합니다.

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $MyNIC
    ```

7. 보기 hello 개인 IP 주소 및 다음 명령을 입력 하 여 NIC hello 공용 IP 주소 할당 된 리소스 toohello hello:

    ```powershell   
    $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
    ```
8. Hello에 운영 체제에는 hello 단계를 완료 하 여 hello 개인 IP 주소 toohello VM 운영 체제 추가 [추가 IP 주소 tooa VM 운영 체제](#os-config) 이 문서의 섹션. Hello 공용 IP 주소 toohello 운영 체제를 추가 하지 마십시오.

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
