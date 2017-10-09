---
title: "Vm-Azure PowerShell에 대 한 aaaConfigure 개인 IP 주소 | Microsoft Docs"
description: "PowerShell을 사용 하 여 가상 컴퓨터에 대 한 개인 IP tooconfigure 해결 하는 방법을 알아봅니다."
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
ms.openlocfilehash: 4a3eb67de583e08208fcab40de1c2a8a9b65618c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-powershell"></a><span data-ttu-id="327f7-103">PowerShell을 사용하여 가상 컴퓨터에 대한 개인 IP 주소 구성</span><span class="sxs-lookup"><span data-stu-id="327f7-103">Configure private IP addresses for a virtual machine using PowerShell</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

<span data-ttu-id="327f7-104">Azure에는 Azure Resource Manager 및 클래식이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="327f7-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="327f7-105">Hello 리소스 관리자 배포 모델을 통해 리소스를 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="327f7-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="327f7-106">hello 읽기에 대해 더 알아봅니다 toolearn hello 두 모델 간의 차이 hello [이해 Azure 배포 모델](../azure-resource-manager/resource-manager-deployment-model.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="327f7-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span> <span data-ttu-id="327f7-107">이 문서에서는 hello 리소스 관리자 배포 모델에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="327f7-107">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="327f7-108">수도 있습니다 [hello 클래식 배포 모델에 개인 고정 IP 주소 관리](virtual-networks-static-private-ip-classic-ps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="327f7-108">You can also [manage static private IP address in hello classic deployment model](virtual-networks-static-private-ip-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="327f7-109">위의 hello 시나리오를 기반으로 hello 예제 PowerShell 명령 아래에 이미 만든 단순한 환경 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="327f7-109">hello sample PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="327f7-110">이 문서에 표시 된 대로 toorun hello 명령을 원하는 경우 먼저 hello 테스트 환경을 구축에 설명 된 [vnet을 만든](virtual-networks-create-vnet-arm-ps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="327f7-110">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-arm-ps.md).</span></span>

## <a name="create-a-vm-with-a-static-private-ip-address"></a><span data-ttu-id="327f7-111">고정 개인 IP 주소를 사용하는 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="327f7-111">Create a VM with a static private IP address</span></span>
<span data-ttu-id="327f7-112">toocreate 라는 VM *DNS01* hello에 *프런트 엔드* 라는 VNet의 서브넷 *TestVNet* 의 정적 개인 ip *192.168.1.101*, 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="327f7-112">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="327f7-113">Hello 저장소 계정, 위치, 리소스 그룹 및 자격 증명 toobe 사용에 대 한 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="327f7-113">Set variables for hello storage account, location, resource group, and credentials toobe used.</span></span> <span data-ttu-id="327f7-114">Hello VM에 대 한 tooenter 사용자 이름 및 암호가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="327f7-114">You will need tooenter a user name and password for hello VM.</span></span> <span data-ttu-id="327f7-115">hello 저장소 계정 및 리소스 그룹을 이미 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="327f7-115">hello storage account and resource group must already exist.</span></span>

    ```powershell
    $stName  = "vnetstorage"
    $locName = "Central US"
    $rgName  = "TestRG"
    $cred    = Get-Credential -Message "Type hello name and password of hello local administrator account."
    ```

2. <span data-ttu-id="327f7-116">검색 hello 가상 네트워크 및 서브넷 toocreate 선택에서 VM hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="327f7-116">Retrieve hello virtual network and subnet you want toocreate hello VM in.</span></span>

    ```powershell
    $vnet   = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    $subnet = $vnet.Subnets[0].Id
    ```

3. <span data-ttu-id="327f7-117">필요한 경우 hello 인터넷에서에서 공용 IP 주소 tooaccess hello VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="327f7-117">If necessary, create a public IP address tooaccess hello VM from hello Internet.</span></span>

    ```powershell
    $pip = New-AzureRmPublicIpAddress -Name TestPIP -ResourceGroupName $rgName `
    -Location $locName -AllocationMethod Dynamic
    ```

4. <span data-ttu-id="327f7-118">Hello 정적 개인 IP 주소를 tooassign toohello VM을 사용 하 여 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="327f7-118">Create a NIC using hello static private IP address you want tooassign toohello VM.</span></span> <span data-ttu-id="327f7-119">있는지 hello IP가 추가 하는 hello 서브넷 범위의 hello VM을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="327f7-119">Make sure hello IP is from hello subnet range you are adding hello VM to.</span></span> <span data-ttu-id="327f7-120">이 여기서 설정한 hello 개인 IP toobe 정적이 문서에 대 한 hello 주요 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="327f7-120">This is hello main step for this article, where you set hello private IP toobe static.</span></span>

    ```powershell
    $nic = New-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName $rgName `
    -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id `
    -PrivateIpAddress 192.168.1.101
    ```

5. <span data-ttu-id="327f7-121">Hello 위에서 만든 hello NIC를 사용 하 여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="327f7-121">Create hello VM using hello NIC created above.</span></span>

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

    <span data-ttu-id="327f7-122">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="327f7-122">Expected output:</span></span>
    
        EndTime             : [Date and time]
        Error               : 
        Output              : 
        StartTime           : [Date and time]
        Status              : Succeeded
        TrackingOperationId : [Id]
        RequestId           : [Id]
        StatusCode          : OK 

## <a name="retrieve-static-private-ip-address-information-for-a-network-interface"></a><span data-ttu-id="327f7-123">네트워크 인터페이스의 고정 개인 IP 주소 정보 검색</span><span class="sxs-lookup"><span data-stu-id="327f7-123">Retrieve static private IP address information for a network interface</span></span>
<span data-ttu-id="327f7-124">tooview hello 정적 개인 IP 주소 VM hello 다음 PowerShell 명령을 실행 합니다. 위의 hello 스크립트를 사용 하 여 만든 hello에 대 한 정보 및 hello에 대 한 값이 확인 *PrivateIpAddress* 및  *PrivateIpAllocationMethod*:</span><span class="sxs-lookup"><span data-stu-id="327f7-124">tooview hello static private IP address information for hello VM created with hello script above, run hello following PowerShell command and observe hello values for *PrivateIpAddress* and *PrivateIpAllocationMethod*:</span></span>

```powershell
Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
```

<span data-ttu-id="327f7-125">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="327f7-125">Expected output:</span></span>

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

## <a name="remove-a-static-private-ip-address-from-a-network-interface"></a><span data-ttu-id="327f7-126">네트워크 인터페이스에서 고정 개인 IP 주소 제거</span><span class="sxs-lookup"><span data-stu-id="327f7-126">Remove a static private IP address from a network interface</span></span>
<span data-ttu-id="327f7-127">다음 PowerShell 명령이 실행된 hello 위의 hello 스크립트 toohello VM을 추가 하는 tooremove hello 정적 개인 IP 주소:</span><span class="sxs-lookup"><span data-stu-id="327f7-127">tooremove hello static private IP address added toohello VM in hello script above, run hello following PowerShell commands:</span></span>

```powershell
$nic=Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
$nic.IpConfigurations[0].PrivateIpAllocationMethod = "Dynamic"
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="327f7-128">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="327f7-128">Expected output:</span></span>

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

## <a name="add-a-static-private-ip-address-tooa-network-interface"></a><span data-ttu-id="327f7-129">정적 개인 IP 주소 tooa 네트워크 인터페이스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="327f7-129">Add a static private IP address tooa network interface</span></span>
<span data-ttu-id="327f7-130">tooadd는 정적 개인 IP 주소 toohello 위의 hello 스크립트를 사용 하 여 만든 VM hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="327f7-130">tooadd a static private IP address toohello VM created using hello script above, run hello following commands:</span></span>

```powershell
$nic=Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
$nic.IpConfigurations[0].PrivateIpAllocationMethod = "Static"
$nic.IpConfigurations[0].PrivateIpAddress = "192.168.1.101"
Set-AzureRmNetworkInterface -NetworkInterface $nic
```
## <a name="change-hello-allocation-method-for-a-private-ip-address-assigned-tooa-network-interface"></a><span data-ttu-id="327f7-131">Tooa 네트워크 인터페이스에 할당 된 개인 IP 주소에 대 한 hello 할당 방법 변경</span><span class="sxs-lookup"><span data-stu-id="327f7-131">Change hello allocation method for a private IP address assigned tooa network interface</span></span>

<span data-ttu-id="327f7-132">개인 IP 주소가 NIC tooa hello 정적 또는 동적 할당 방법으로 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="327f7-132">A private IP address is assigned tooa NIC with hello static or dynamic allocation method.</span></span> <span data-ttu-id="327f7-133">동적 IP 주소 (할당 취소) 상태 중지 hello에 이전에 있던 VM을 시작 후 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="327f7-133">Dynamic IP addresses can change after starting a VM that was previously in hello stopped (deallocated) state.</span></span> <span data-ttu-id="327f7-134">Hello VM hello를 필요로 하는 서비스를 호스팅하는 경우 문제가 발생할 수 있습니다이 중지 (할당 취소) 상태에서 다시 시작 후에 동일한 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="327f7-134">This can potentially cause issues if hello VM is hosting a service that requires hello same IP address, even after restarts from a stopped (deallocated) state.</span></span> <span data-ttu-id="327f7-135">고정 IP 주소는 hello VM 삭제 될 때까지 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="327f7-135">Static IP addresses are retained until hello VM is deleted.</span></span> <span data-ttu-id="327f7-136">hello 뒤에서 동적 toostatic hello 할당 방법 변경 하는 스크립트를 실행 하는 IP 주소의 toochange hello 할당 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="327f7-136">toochange hello allocation method of an IP address, run hello following script, which changes hello allocation method from dynamic toostatic.</span></span> <span data-ttu-id="327f7-137">Hello 할당 방법 hello 현재 개인 IP 주소에 대 한 정적 이면 변경 *정적* 너무*동적* hello 스크립트를 실행 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="327f7-137">If hello allocation method for hello current private IP address is static, change *Static* too*Dynamic* before executing hello script.</span></span>

```powershell
$RG = "TestRG"
$NIC_name = "testnic1"

$nic = Get-AzureRmNetworkInterface -ResourceGroupName $RG -Name $NIC_name
$nic.IpConfigurations[0].PrivateIpAllocationMethod = 'Static'
Set-AzureRmNetworkInterface -NetworkInterface $nic 
$IP = $nic.IpConfigurations[0].PrivateIpAddress

Write-Host "hello allocation method is now set to"$nic.IpConfigurations[0].PrivateIpAllocationMethod"for hello IP address" $IP"." -NoNewline
```

<span data-ttu-id="327f7-138">Hello NIC의 hello 이름을 모르면 hello 다음 명령을 입력 하 여 리소스 그룹 내의 Nic의 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="327f7-138">If you don't know hello name of hello NIC, you can view a list of NICs within a resource group by entering hello following command:</span></span>

```powershell
Get-AzureRmNetworkInterface -ResourceGroupName $RG | Where-Object {$_.ProvisioningState -eq 'Succeeded'} 
```

## <a name="next-steps"></a><span data-ttu-id="327f7-139">다음 단계</span><span class="sxs-lookup"><span data-stu-id="327f7-139">Next steps</span></span>
* <span data-ttu-id="327f7-140">[예약된 공용 IP](virtual-networks-reserved-public-ip.md) 주소에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="327f7-140">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="327f7-141">[ILPIP(인스턴스 수준 공용 IP)](virtual-networks-instance-level-public-ip.md) 주소에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="327f7-141">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="327f7-142">Hello 참조 [예약 된 IP REST Api](https://msdn.microsoft.com/library/azure/dn722420.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="327f7-142">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

