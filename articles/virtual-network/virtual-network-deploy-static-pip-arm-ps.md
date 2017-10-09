---
title: "고정 공용 IP 주소-Azure PowerShell을 사용 하 여 VM aaaCreate | Microsoft Docs"
description: "PowerShell을 사용 하 여 toocreate 고정 공용 IP 사용 하 여 VM을 해결 하는 방법을 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ad975ab9-d69f-45c1-9e45-0d3f0f51e87e
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0d2b88319cb114b8616f60dbee41e8fdc6d8b1b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-powershell"></a><span data-ttu-id="fc3b9-103">PowerShell을 사용하여 고정 공용 IP 주소를 사용하는 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="fc3b9-103">Create a VM with a static public IP address using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="fc3b9-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="fc3b9-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="fc3b9-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fc3b9-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="fc3b9-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="fc3b9-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="fc3b9-107">템플릿</span><span class="sxs-lookup"><span data-stu-id="fc3b9-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="fc3b9-108">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="fc3b9-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="fc3b9-109">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc3b9-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="fc3b9-110">이 문서에서는 Microsoft hello 클래식 배포 모델 대신 대부분의 새 배포에 권장 하는 hello 리소스 관리자 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc3b9-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="step-1---start-your-script"></a><span data-ttu-id="fc3b9-111">1단계 - 스크립트 시작</span><span class="sxs-lookup"><span data-stu-id="fc3b9-111">Step 1 - Start your script</span></span>
<span data-ttu-id="fc3b9-112">Hello 사용 되는 전체 PowerShell 스크립트를 다운로드할 수 있습니다 [여기](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/virtual-network-deploy-static-pip-arm-ps.ps1)합니다.</span><span class="sxs-lookup"><span data-stu-id="fc3b9-112">You can download hello full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/virtual-network-deploy-static-pip-arm-ps.ps1).</span></span> <span data-ttu-id="fc3b9-113">사용자 환경에서 toochange hello 스크립트 toowork 아래 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc3b9-113">Follow hello steps below toochange hello script toowork in your environment.</span></span>

<span data-ttu-id="fc3b9-114">Hello 값을 변경 hello 값을 기반으로 hello 변수 원하는 toouse 배포에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc3b9-114">Change hello values of hello variables below based on hello values you want toouse for your deployment.</span></span> <span data-ttu-id="fc3b9-115">이 문서에서 사용 하는 값 지도 toohello 시나리오를 따르는 hello:</span><span class="sxs-lookup"><span data-stu-id="fc3b9-115">hello following values map toohello scenario used in this article:</span></span>

```powershell
# Set variables resource group
$rgName                = "IaaSStory"
$location              = "West US"

# Set variables for VNet
$vnetName              = "WTestVNet"
$vnetPrefix            = "192.168.0.0/16"
$subnetName            = "FrontEnd"
$subnetPrefix          = "192.168.1.0/24"

# Set variables for storage
$stdStorageAccountName = "iaasstorystorage"

# Set variables for VM
$vmSize                = "Standard_A1"
$diskSize              = 127
$publisher             = "MicrosoftWindowsServer"
$offer                 = "WindowsServer"
$sku                   = "2012-R2-Datacenter"
$version               = "latest"
$vmName                = "WEB1"
$osDiskName            = "osdisk"
$nicName               = "NICWEB1"
$privateIPAddress      = "192.168.1.101"
$pipName               = "PIPWEB1"
$dnsName               = "iaasstoryws1"
```

## <a name="step-2---create-hello-necessary-resources-for-your-vm"></a><span data-ttu-id="fc3b9-116">2 단계-hello 필요한 리소스에 대 한 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="fc3b9-116">Step 2 - Create hello necessary resources for your VM</span></span>
<span data-ttu-id="fc3b9-117">VM을 만들기 전에 리소스 그룹, VNet, 공용 IP, 및 필요한 NIC toobe hello VM에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc3b9-117">Before creating a VM, you need a resource group, VNet, public IP, and NIC toobe used by hello VM.</span></span>

1. <span data-ttu-id="fc3b9-118">새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fc3b9-118">Create a new resource group.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name $rgName -Location $location
    ```

2. <span data-ttu-id="fc3b9-119">만들 hello VNet 및 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="fc3b9-119">Create hello VNet and subnet.</span></span>

    ```powershell
    $vnet = New-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName `
        -AddressPrefix $vnetPrefix -Location $location

    Add-AzureRmVirtualNetworkSubnetConfig -Name $subnetName `
        -VirtualNetwork $vnet -AddressPrefix $subnetPrefix

    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

3. <span data-ttu-id="fc3b9-120">Hello 공용 IP 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fc3b9-120">Create hello public IP resource.</span></span> 

    ```powershell
    $pip = New-AzureRmPublicIpAddress -Name $pipName -ResourceGroupName $rgName `
        -AllocationMethod Static -DomainNameLabel $dnsName -Location $location
    ```

4. <span data-ttu-id="fc3b9-121">Hello 공용 IP를 사용 하 여 위에서 만든 hello 서브넷에 VM hello에 대 한 hello 네트워크 인터페이스 (NIC)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fc3b9-121">Create hello network interface (NIC) for hello VM in hello subnet created above, with hello public IP.</span></span> <span data-ttu-id="fc3b9-122">Azure에서 hello VNet을 검색 하는 첫 번째 cmdlet hello,이 작업은 이후 필요는 `Set-AzureRmVirtualNetwork` 가 실행 된 toochange hello 기존 VNet입니다.</span><span class="sxs-lookup"><span data-stu-id="fc3b9-122">Notice hello first cmdlet retrieving hello VNet from Azure, this is necessary since a `Set-AzureRmVirtualNetwork` was executed toochange hello existing VNet.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name $subnetName
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
        -Subnet $subnet -Location $location -PrivateIpAddress $privateIPAddress `
        -PublicIpAddress $pip
    ```

5. <span data-ttu-id="fc3b9-123">저장소 계정 toohost hello VM 운영 체제 드라이브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fc3b9-123">Create a storage account toohost hello VM OS drive.</span></span>

    ```powershell
    $stdStorageAccount = New-AzureRmStorageAccount -Name $stdStorageAccountName `
    -ResourceGroupName $rgName -Type Standard_LRS -Location $location
    ```

## <a name="step-3---create-hello-vm"></a><span data-ttu-id="fc3b9-124">3 단계-hello VM 만들기</span><span class="sxs-lookup"><span data-stu-id="fc3b9-124">Step 3 - Create hello VM</span></span>
<span data-ttu-id="fc3b9-125">이제 필요한 모든 리소스를 배치했으므로 새 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc3b9-125">Now that all necessary resources are in place, you can create a new VM.</span></span>

1. <span data-ttu-id="fc3b9-126">Hello VM에 대 한 hello 구성 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fc3b9-126">Create hello configuration object for hello VM.</span></span>

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
    ```

2. <span data-ttu-id="fc3b9-127">Hello VM 로컬 관리자 계정에 대 한 자격 증명을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="fc3b9-127">Get credentials for hello VM local administrator account.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Type hello name and password for hello local administrator account."
    ```

3. <span data-ttu-id="fc3b9-128">VM 구성 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fc3b9-128">Create a VM configuration object.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $vmName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    ```

4. <span data-ttu-id="fc3b9-129">Hello VM에 대 한 hello 운영 체제 이미지를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc3b9-129">Set hello operating system image for hello VM.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -PublisherName $publisher `
        -Offer $offer -Skus $sku -Version $version
    ```

5. <span data-ttu-id="fc3b9-130">Hello OS 디스크를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc3b9-130">Configure hello OS disk.</span></span>

    ```powershell
    $osVhdUri = $stdStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $osDiskName + ".vhd"
    $vmConfig = Set-AzureRmVMOSDisk -VM $vmConfig -Name $osDiskName -VhdUri $osVhdUri -CreateOption fromImage
    ```

6. <span data-ttu-id="fc3b9-131">Hello NIC toohello VM을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc3b9-131">Add hello NIC toohello VM.</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id -Primary
    ```

7. <span data-ttu-id="fc3b9-132">Hello VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fc3b9-132">Create hello VM.</span></span>

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName $rgName -Location $location
    ```

8. <span data-ttu-id="fc3b9-133">Hello 스크립트 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc3b9-133">Save hello script file.</span></span>

## <a name="step-4---run-hello-script"></a><span data-ttu-id="fc3b9-134">4 단계-실행 hello 스크립트</span><span class="sxs-lookup"><span data-stu-id="fc3b9-134">Step 4 - Run hello script</span></span>
<span data-ttu-id="fc3b9-135">필요한 내용을 변경 하 고 hello 스크립트 이해 한 후 위에 표시할 hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc3b9-135">After making any necessary changes, and understanding hello script show above, run hello script.</span></span> 

1. <span data-ttu-id="fc3b9-136">PowerShell 콘솔 또는 PowerShell ISE에서 위의 hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc3b9-136">From a PowerShell console, or PowerShell ISE, run hello script above.</span></span>
2. <span data-ttu-id="fc3b9-137">몇 분 후 hello 출력 다음이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc3b9-137">hello following output should be displayed after a few minutes:</span></span>
   
        ResourceGroupName : IaaSStory
        Location          : westus
        ProvisioningState : Succeeded
        Tags              : 
        ResourceId        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory
   
        AddressSpace      : Microsoft.Azure.Commands.Network.Models.PSAddressSpace
        DhcpOptions       : Microsoft.Azure.Commands.Network.Models.PSDhcpOptions
        Subnets           : {FrontEnd}
        ProvisioningState : Succeeded
        AddressSpaceText  : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptionsText   : {}
        SubnetsText       : [
                              {
                                "Name": "FrontEnd",
                                "AddressPrefix": "192.168.1.0/24"
                              }
                            ]
        ResourceGroupName : IaaSStory
        Location          : westus
        ResourceGuid      : [Id]
        Tag               : {}
        TagsTable         : 
        Name              : WTestVNet
        Etag              : W/"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
        Id                : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet
   
        AddressSpace      : Microsoft.Azure.Commands.Network.Models.PSAddressSpace
        DhcpOptions       : Microsoft.Azure.Commands.Network.Models.PSDhcpOptions
        Subnets           : {FrontEnd}
        ProvisioningState : Succeeded
        AddressSpaceText  : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptionsText   : {
                              "DnsServers": []
                            }
        SubnetsText       : [
                              {
                                "Name": "FrontEnd",
                                "Etag": [Id],
                                "Id": "/subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/FrontEnd",
                                "AddressPrefix": "192.168.1.0/24",
                                "IpConfigurations": [],
                                "ProvisioningState": "Succeeded"
                              }
                            ]
        ResourceGroupName : IaaSStory
        Location          : westus
        ResourceGuid      : [Id]
        Tag               : {}
        TagsTable         : 
        Name              : WTestVNet
        Etag              : [Id]
        Id                : /subscriptions/[Subscription Id]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet
   
        TrackingOperationId : [Id]
        RequestId           : [Id]
        Status              : Succeeded
        StatusCode          : OK
        Output              : 
        StartTime           : [Subscription Id]
        EndTime             : [Subscription Id]
        Error               : 
        ErrorText           : 

