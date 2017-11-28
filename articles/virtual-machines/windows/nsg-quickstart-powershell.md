---
title: "Azure PowerShell을 사용하여 VM으로 포트 열기 | Microsoft Docs"
description: "Azure Resource Manager 배포 모델 및 Azure PowerShell을 사용하여 Windows VM에 대한 포트를 열고 끝점을 만드는 방법 알아보기"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: cf45f7d8-451a-48ab-8419-730366d54f1e
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: e818e3b3c707e1471d6f580f8379a277d3575b89
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-open-ports-and-endpoints-to-a-vm-in-azure-using-powershell"></a><span data-ttu-id="6bb14-103">PowerShell을 사용하여 Azure에서 VM의 포트 및 끝점을 여는 방법</span><span class="sxs-lookup"><span data-stu-id="6bb14-103">How to open ports and endpoints to a VM in Azure using PowerShell</span></span>
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a><span data-ttu-id="6bb14-104">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="6bb14-104">Quick commands</span></span>
<span data-ttu-id="6bb14-105">네트워크 보안 그룹 및 ACL 규칙을 만들려면 [최신 버전의 Azure PowerShell을 설치](/powershell/azureps-cmdlets-docs)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb14-105">To create a Network Security Group and ACL rules you need [the latest version of Azure PowerShell installed](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="6bb14-106">[Azure 포털을 사용하여 수행할 수도 있습니다](nsg-quickstart-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6bb14-106">You can also [perform these steps using the Azure portal](nsg-quickstart-portal.md).</span></span>

<span data-ttu-id="6bb14-107">Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb14-107">Log in to your Azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="6bb14-108">다음 예제에서 매개 변수 이름을 고유한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6bb14-108">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="6bb14-109">예제 매개 변수 이름에는 *myResourceGroup*, *myNetworkSecurityGroup* 및 *myVnet*이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bb14-109">Example parameter names included *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="6bb14-110">[New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig)를 사용하여 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6bb14-110">Create a rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="6bb14-111">다음 예제에서는 포트 *80*의 *tcp* 트래픽을 허용하도록 *myNetworkSecurityGroupRule*이라는 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6bb14-111">The following example creates a rule named *myNetworkSecurityGroupRule* to allow *tcp* traffic on port *80*:</span></span>

```powershell
$httprule = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRule" `
    -Description "Allow HTTP" `
    -Access "Allow" `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority "100" `
    -SourceAddressPrefix "Internet" `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80
```

<span data-ttu-id="6bb14-112">그런 후 다음과 같이 [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup)을 사용하여 네트워크 보안 그룹을 만들고 방금 만든 HTTP 규칙을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb14-112">Next, create your Network Security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) and assign the HTTP rule you just created as follows.</span></span> <span data-ttu-id="6bb14-113">다음 예제에서는 *myNetworkSecurityGroup*이라는 네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6bb14-113">The following example creates a Network Security Group named *myNetworkSecurityGroup*:</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName "myResourceGroup" `
    -Location "EastUS" `
    -Name "myNetworkSecurityGroup" `
    -SecurityRules $httprule
```

<span data-ttu-id="6bb14-114">이제 서브넷에 네트워크 보안 그룹을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb14-114">Now let's assign your Network Security Group to a subnet.</span></span> <span data-ttu-id="6bb14-115">다음 예제에서는 [Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork)를 사용하여 *myVnet*이라는 기존 가상 네트워크를 *$vnet* 변수에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb14-115">The following example assigns an existing virtual network named *myVnet* to the variable *$vnet* with [Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork):</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork `
    -ResourceGroupName "myResourceGroup" `
    -Name "myVnet"
```

<span data-ttu-id="6bb14-116">[Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig)를 사용하여 네트워크 보안 그룹을 서브넷에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb14-116">Associate your Network Security Group with your subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="6bb14-117">다음 예제에서는 *mySubnet*이라는 서브넷을 네트워크 보안 그룹에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb14-117">The following example associates the subnet named *mySubnet* with your Network Security Group:</span></span>

```powershell
$subnetPrefix = $vnet.Subnets|?{$_.Name -eq 'mySubnet'}

Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name "mySubnet" `
    -AddressPrefix $subnetPrefix.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

<span data-ttu-id="6bb14-118">마지막으로, 변경 내용이 적용되도록 [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork)를 사용하여 가상 네트워크를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb14-118">Finally, update your virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) in order for your changes to take effect:</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```


## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="6bb14-119">네트워크 보안 그룹에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="6bb14-119">More information on Network Security Groups</span></span>
<span data-ttu-id="6bb14-120">여기서 빠른 명령을 사용하면 VM으로 트래픽이 이동되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bb14-120">The quick commands here allow you to get up and running with traffic flowing to your VM.</span></span> <span data-ttu-id="6bb14-121">네트워크 보안 그룹은 리소스에 대한 액세스를 제어하는 많은 기능과 세분성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb14-121">Network Security Groups provide many great features and granularity for controlling access to your resources.</span></span> <span data-ttu-id="6bb14-122">[여기서 네트워크 보안 그룹 및 ACL 규칙 만들기](tutorial-virtual-network.md#manage-internal-traffic)에 대해 자세히 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="6bb14-122">You can read more about [creating a Network Security Group and ACL rules here](tutorial-virtual-network.md#manage-internal-traffic).</span></span>

<span data-ttu-id="6bb14-123">고가용성 웹 응용 프로그램인 경우 VM을 Azure Load Balancer 뒤에 배치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb14-123">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="6bb14-124">부하 분산 장치는 트래픽 필터링을 제공하는 네트워크 보안 그룹으로 트래픽을 VM에 분산시킵니다.</span><span class="sxs-lookup"><span data-stu-id="6bb14-124">The load balancer distributes traffic to VMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="6bb14-125">자세한 내용은 [Azure의 Linux 가상 컴퓨터 부하를 분산하여 고가용성 응용 프로그램을 만드는 방법](tutorial-load-balancer.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6bb14-125">For more information, see [How to load balance Linux virtual machines in Azure to create a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6bb14-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6bb14-126">Next steps</span></span>
<span data-ttu-id="6bb14-127">이 예제에서는 HTTP 트래픽을 허용하는 간단한 규칙을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="6bb14-127">In this example, you created a simple rule to allow HTTP traffic.</span></span> <span data-ttu-id="6bb14-128">다음 문서에서 보다 자세한 환경을 만들기 위한 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bb14-128">You can find information on creating more detailed environments in the following articles:</span></span>

* [<span data-ttu-id="6bb14-129">Azure Resource Manager 개요</span><span class="sxs-lookup"><span data-stu-id="6bb14-129">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="6bb14-130">NSG(네트워크 보안 그룹)란?</span><span class="sxs-lookup"><span data-stu-id="6bb14-130">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="6bb14-131">부하 분산 장치에 대한 Azure Resource Manager 개요</span><span class="sxs-lookup"><span data-stu-id="6bb14-131">Azure Resource Manager Overview for Load Balancers</span></span>](../../load-balancer/load-balancer-arm.md)

