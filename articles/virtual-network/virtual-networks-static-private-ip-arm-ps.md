---
title: "VM에 대한 개인 IP 주소 구성 - Azure PowerShell | Microsoft Docs"
description: "PowerShell을 사용하여 가상 컴퓨터에 대한 개인 IP 주소를 구성하는 방법을 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: d5f18929-15e3-40a2-9ee3-8188bc248ed8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2810190897c44c944912ef3325b1f40479aa3078
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-powershell"></a><span data-ttu-id="2df58-103">PowerShell을 사용하여 가상 컴퓨터에 대한 개인 IP 주소 구성</span><span class="sxs-lookup"><span data-stu-id="2df58-103">Configure private IP addresses for a virtual machine using PowerShell</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

<span data-ttu-id="2df58-104">Azure에는 Azure Resource Manager 및 클래식이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2df58-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="2df58-105">Resource Manager 배포 모델을 통해 리소스를 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2df58-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="2df58-106">두 가지 모델의 차이점에 대해 자세히 알아보려면 [Azure 배포 모델 이해](../azure-resource-manager/resource-manager-deployment-model.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2df58-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span> <span data-ttu-id="2df58-107">이 문서에서는 리소스 관리자 배포 모델에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2df58-107">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="2df58-108">[클래식 배포 모델에서 정적 개인 IP 주소를 관리](virtual-networks-static-private-ip-classic-ps.md)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2df58-108">You can also [manage static private IP address in the classic deployment model](virtual-networks-static-private-ip-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="2df58-109">아래 샘플 PowerShell 명령에는 위의 시나리오를 기반으로 이미 만들어져 있는 단순한 환경이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2df58-109">The sample PowerShell commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="2df58-110">이 문서에 표시된 대로 명령을 실행하려는 경우 먼저 [vnet 만들기](virtual-networks-create-vnet-arm-ps.md)에 설명된 테스트 환경을 구축합니다.</span><span class="sxs-lookup"><span data-stu-id="2df58-110">If you want to run the commands as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-arm-ps.md).</span></span>

## <a name="create-a-vm-with-a-static-private-ip-address"></a><span data-ttu-id="2df58-111">고정 개인 IP 주소를 사용하는 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="2df58-111">Create a VM with a static private IP address</span></span>
<span data-ttu-id="2df58-112">*192.168.1.101*의 정적 개인 IP 주소를 사용하여 *TestVNet*이라는 VNet의 *FrontEnd* 서브넷에 *DNS01*이라는 VM을 만들려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="2df58-112">To create a VM named *DNS01* in the *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow the steps below:</span></span>

1. <span data-ttu-id="2df58-113">사용할 저장소 계정, 위치, 리소스 그룹 및 자격 증명에 대한 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2df58-113">Set variables for the storage account, location, resource group, and credentials to be used.</span></span> <span data-ttu-id="2df58-114">VM에 대한 사용자 이름 및 암호를 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df58-114">You will need to enter a user name and password for the VM.</span></span> <span data-ttu-id="2df58-115">저장소 계정 및 리소스 그룹이 이미 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df58-115">The storage account and resource group must already exist.</span></span>

    ```powershell
    $stName  = "vnetstorage"
    $locName = "Central US"
    $rgName  = "TestRG"
    $cred    = Get-Credential -Message "Type the name and password of the local administrator account."
    ```

2. <span data-ttu-id="2df58-116">VM을 만들 가상 네트워크 및 서브넷을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="2df58-116">Retrieve the virtual network and subnet you want to create the VM in.</span></span>

    ```powershell
    $vnet   = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    $subnet = $vnet.Subnets[0].Id
    ```

3. <span data-ttu-id="2df58-117">필요한 경우 인터넷에서 VM에 액세스하기 위한 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2df58-117">If necessary, create a public IP address to access the VM from the Internet.</span></span>

    ```powershell
    $pip = New-AzureRmPublicIpAddress -Name TestPIP -ResourceGroupName $rgName `
    -Location $locName -AllocationMethod Dynamic
    ```

4. <span data-ttu-id="2df58-118">VM에 할당하려는 정적 개인 IP 주소를 사용하여 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2df58-118">Create a NIC using the static private IP address you want to assign to the VM.</span></span> <span data-ttu-id="2df58-119">IP가 VM을 추가할 서브넷 범위에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2df58-119">Make sure the IP is from the subnet range you are adding the VM to.</span></span> <span data-ttu-id="2df58-120">다음은 이 문서의 주요 단계로, 여기에서 개인 IP를 정적으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2df58-120">This is the main step for this article, where you set the private IP to be static.</span></span>

    ```powershell
    $nic = New-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName $rgName `
    -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id `
    -PrivateIpAddress 192.168.1.101
    ```

5. <span data-ttu-id="2df58-121">위에서 만든 NIC를 사용하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2df58-121">Create the VM using the NIC created above.</span></span>

    ```powershell
    $vm = New-AzureRmVMConfig -VMName DNS01 -VMSize "Standard_A1"
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName DNS01 `
    -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Set-AzureRmVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri = $storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/WindowsVMosDisk.vhd"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name "windowsvmosdisk" -VhdUri $osDiskUri `
    -CreateOption fromImage
    New-AzureRmVM -ResourceGroupName $rgName -Location $locName -VM $vm 
    ```

    <span data-ttu-id="2df58-122">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="2df58-122">Expected output:</span></span>
    
        EndTime             : [Date and time]
        Error               : 
        Output              : 
        StartTime           : [Date and time]
        Status              : Succeeded
        TrackingOperationId : [Id]
        RequestId           : [Id]
        StatusCode          : OK 

## <a name="retrieve-static-private-ip-address-information-for-a-network-interface"></a><span data-ttu-id="2df58-123">네트워크 인터페이스의 고정 개인 IP 주소 정보 검색</span><span class="sxs-lookup"><span data-stu-id="2df58-123">Retrieve static private IP address information for a network interface</span></span>
<span data-ttu-id="2df58-124">위의 스크립트로 만든 VM에 대한 정적 개인 IP 주소 정보를 보려면 다음 PowerShell 명령을 실행하고 *PrivateIpAddress* 및 *PrivateIpAllocationMethod*에 대한 값을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2df58-124">To view the static private IP address information for the VM created with the script above, run the following PowerShell command and observe the values for *PrivateIpAddress* and *PrivateIpAllocationMethod*:</span></span>

```powershell
Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
```

<span data-ttu-id="2df58-125">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="2df58-125">Expected output:</span></span>

    Name                 : TestNIC
    ResourceGroupName    : TestRG
    Location             : centralus
    Id                   : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
    Etag                 : W/"[Id]"
    ProvisioningState    : Succeeded
    Tags                 : 
    VirtualMachine       : {
                             "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01"
                           }
    IpConfigurations     : [
                             {
                               "Name": "ipconfig1",
                               "Etag": "W/\"[Id]\"",
                               "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                               "PrivateIpAddress": "192.168.1.101",
                               "PrivateIpAllocationMethod": "Static",
                               "Subnet": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                               },
                               "PublicIpAddress": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP"
                               },
                               "LoadBalancerBackendAddressPools": [],
                               "LoadBalancerInboundNatRules": [],
                               "ProvisioningState": "Succeeded"
                             }
                           ]
    DnsSettings          : {
                             "DnsServers": [],
                             "AppliedDnsServers": [],
                             "InternalDnsNameLabel": null,
                             "InternalFqdn": null
                           }
    EnableIPForwarding   : False
    NetworkSecurityGroup : null
    Primary              : True

## <a name="remove-a-static-private-ip-address-from-a-network-interface"></a><span data-ttu-id="2df58-126">네트워크 인터페이스에서 고정 개인 IP 주소 제거</span><span class="sxs-lookup"><span data-stu-id="2df58-126">Remove a static private IP address from a network interface</span></span>
<span data-ttu-id="2df58-127">위의 스크립트에서 VM에 추가된 정적 개인 IP 주소를 제거하려면 다음 PowerShell 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2df58-127">To remove the static private IP address added to the VM in the script above, run the following PowerShell commands:</span></span>

```powershell
$nic=Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
$nic.IpConfigurations[0].PrivateIpAllocationMethod = "Dynamic"
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="2df58-128">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="2df58-128">Expected output:</span></span>

    Name                 : TestNIC
    ResourceGroupName    : TestRG
    Location             : centralus
    Id                   : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
    Etag                 : W/"[Id]"
    ProvisioningState    : Succeeded
    Tags                 : 
    VirtualMachine       : {
                             "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/WindowsVM"
                           }
    IpConfigurations     : [
                             {
                               "Name": "ipconfig1",
                               "Etag": "W/\"[Id]\"",
                               "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                               "PrivateIpAddress": "192.168.1.101",
                               "PrivateIpAllocationMethod": "Dynamic",
                               "Subnet": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                               },
                               "PublicIpAddress": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP"
                               },
                               "LoadBalancerBackendAddressPools": [],
                               "LoadBalancerInboundNatRules": [],
                               "ProvisioningState": "Succeeded"
                             }
                           ]
    DnsSettings          : {
                             "DnsServers": [],
                             "AppliedDnsServers": [],
                             "InternalDnsNameLabel": null,
                             "InternalFqdn": null
                           }
    EnableIPForwarding   : False
    NetworkSecurityGroup : null
    Primary              : True

## <a name="add-a-static-private-ip-address-to-a-network-interface"></a><span data-ttu-id="2df58-129">네트워크 인터페이스에 고정 개인 IP 주소 추가</span><span class="sxs-lookup"><span data-stu-id="2df58-129">Add a static private IP address to a network interface</span></span>
<span data-ttu-id="2df58-130">위의 스크립트를 사용하여 만든 VM에 정적 개인 IP 주소를 추가하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2df58-130">To add a static private IP address to the VM created using the script above, run the following commands:</span></span>

```powershell
$nic=Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
$nic.IpConfigurations[0].PrivateIpAllocationMethod = "Static"
$nic.IpConfigurations[0].PrivateIpAddress = "192.168.1.101"
Set-AzureRmNetworkInterface -NetworkInterface $nic
```
## <a name="change-the-allocation-method-for-a-private-ip-address-assigned-to-a-network-interface"></a><span data-ttu-id="2df58-131">네트워크 인터페이스에 할당된 개인 IP 주소의 할당 방법 변경</span><span class="sxs-lookup"><span data-stu-id="2df58-131">Change the allocation method for a private IP address assigned to a network interface</span></span>

<span data-ttu-id="2df58-132">개인 IP 주소는 고정 또는 동적 할당 방법을 사용하여 NIC에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="2df58-132">A private IP address is assigned to a NIC with the static or dynamic allocation method.</span></span> <span data-ttu-id="2df58-133">동적 IP 주소는 이전에 중지(할당 취소) 상태였던 VM을 시작한 후 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2df58-133">Dynamic IP addresses can change after starting a VM that was previously in the stopped (deallocated) state.</span></span> <span data-ttu-id="2df58-134">이렇게 하면 VM이 동일한 IP 주소가 필요한 서비스를 호스팅하는 경우 중지(할당 취소) 상태에서 다시 시작하더라도 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2df58-134">This can potentially cause issues if the VM is hosting a service that requires the same IP address, even after restarts from a stopped (deallocated) state.</span></span> <span data-ttu-id="2df58-135">고정 IP 주소는 VM이 삭제될 때까지 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="2df58-135">Static IP addresses are retained until the VM is deleted.</span></span> <span data-ttu-id="2df58-136">IP 주소 할당 방법을 변경하려면 할당 방법을 동적에서 고정으로 변경하는 다음 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2df58-136">To change the allocation method of an IP address, run the following script, which changes the allocation method from dynamic to static.</span></span> <span data-ttu-id="2df58-137">현재 개인 IP 주소의 할당 방법이 고정이면 *고정*을 *동적*으로 변경한 후 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2df58-137">If the allocation method for the current private IP address is static, change *Static* to *Dynamic* before executing the script.</span></span>

```powershell
$RG = "TestRG"
$NIC_name = "testnic1"

$nic = Get-AzureRmNetworkInterface -ResourceGroupName $RG -Name $NIC_name
$nic.IpConfigurations[0].PrivateIpAllocationMethod = 'Static'
Set-AzureRmNetworkInterface -NetworkInterface $nic 
$IP = $nic.IpConfigurations[0].PrivateIpAddress

Write-Host "The allocation method is now set to"$nic.IpConfigurations[0].PrivateIpAllocationMethod"for the IP address" $IP"." -NoNewline
```

<span data-ttu-id="2df58-138">NIC의 이름을 모르는 경우 다음 명령을 입력하여 리소스 그룹 내에서 NIC 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2df58-138">If you don't know the name of the NIC, you can view a list of NICs within a resource group by entering the following command:</span></span>

```powershell
Get-AzureRmNetworkInterface -ResourceGroupName $RG | Where-Object {$_.ProvisioningState -eq 'Succeeded'} 
```

## <a name="next-steps"></a><span data-ttu-id="2df58-139">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2df58-139">Next steps</span></span>
* <span data-ttu-id="2df58-140">[예약된 공용 IP](virtual-networks-reserved-public-ip.md) 주소에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2df58-140">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="2df58-141">[ILPIP(인스턴스 수준 공용 IP)](virtual-networks-instance-level-public-ip.md) 주소에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2df58-141">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="2df58-142">[예약된 IP REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx)를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="2df58-142">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

