---
title: "aaaOpen 포트 tooa Azure PowerShell을 사용 하 여 VM | Microsoft Docs"
description: "자세한 방법을 tooopen 포트 끝점 tooyour Windows VM을 만들 / hello Azure 리소스 관리자 배포 모드 및 Azure PowerShell을 사용 하 여"
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
ms.openlocfilehash: c1817a0c447ae4ce7a1ce2a1fc6927bedf2dacb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-ports-and-endpoints-tooa-vm-in-azure-using-powershell"></a><span data-ttu-id="51b0d-103">어떻게 tooopen 포트와 끝점 tooa PowerShell을 사용 하 여 Azure에서 VM</span><span class="sxs-lookup"><span data-stu-id="51b0d-103">How tooopen ports and endpoints tooa VM in Azure using PowerShell</span></span>
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a><span data-ttu-id="51b0d-104">빠른 명령</span><span class="sxs-lookup"><span data-stu-id="51b0d-104">Quick commands</span></span>
<span data-ttu-id="51b0d-105">toocreate 네트워크 보안 그룹 및 ACL 규칙 필요한 [hello 최신 버전의 Azure PowerShell 설치](/powershell/azureps-cmdlets-docs)합니다.</span><span class="sxs-lookup"><span data-stu-id="51b0d-105">toocreate a Network Security Group and ACL rules you need [hello latest version of Azure PowerShell installed](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="51b0d-106">수도 있습니다 [hello Azure 포털을 사용 하 여 이러한 단계를 수행](nsg-quickstart-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="51b0d-106">You can also [perform these steps using hello Azure portal](nsg-quickstart-portal.md).</span></span>

<span data-ttu-id="51b0d-107">Azure 계정 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="51b0d-107">Log in tooyour Azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="51b0d-108">Hello 다음 예제에서는 고유한 값으로 매개 변수 이름 예를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="51b0d-108">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="51b0d-109">예제 매개 변수 이름에는 *myResourceGroup*, *myNetworkSecurityGroup* 및 *myVnet*이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="51b0d-109">Example parameter names included *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="51b0d-110">[New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig)를 사용하여 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="51b0d-110">Create a rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="51b0d-111">hello 다음 규칙을 만드는 예제는 명명 된 *myNetworkSecurityGroupRule* tooallow *tcp* 포트에서 트래픽을 *80*:</span><span class="sxs-lookup"><span data-stu-id="51b0d-111">hello following example creates a rule named *myNetworkSecurityGroupRule* tooallow *tcp* traffic on port *80*:</span></span>

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

<span data-ttu-id="51b0d-112">다음으로를 네트워크 보안 그룹을 만듭니다 [새로 AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) 및 할당 hello HTTP 방금 만든 규칙 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="51b0d-112">Next, create your Network Security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) and assign hello HTTP rule you just created as follows.</span></span> <span data-ttu-id="51b0d-113">hello 다음 예제에서는 네트워크 보안 그룹을 만든 라는 *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="51b0d-113">hello following example creates a Network Security Group named *myNetworkSecurityGroup*:</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName "myResourceGroup" `
    -Location "EastUS" `
    -Name "myNetworkSecurityGroup" `
    -SecurityRules $httprule
```

<span data-ttu-id="51b0d-114">이제 네트워크 보안 그룹 tooa 서브넷을 할당 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="51b0d-114">Now let's assign your Network Security Group tooa subnet.</span></span> <span data-ttu-id="51b0d-115">hello 다음 예제에서는 할당 명명 된 기존 가상 네트워크가 *myVnet* toohello 변수 *$vnet* 와 [Get AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="51b0d-115">hello following example assigns an existing virtual network named *myVnet* toohello variable *$vnet* with [Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork):</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork `
    -ResourceGroupName "myResourceGroup" `
    -Name "myVnet"
```

<span data-ttu-id="51b0d-116">[Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig)를 사용하여 네트워크 보안 그룹을 서브넷에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="51b0d-116">Associate your Network Security Group with your subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="51b0d-117">hello 다음 예제에서는 연결 라는 hello 서브넷 *mySubnet* 네트워크 보안 그룹과:</span><span class="sxs-lookup"><span data-stu-id="51b0d-117">hello following example associates hello subnet named *mySubnet* with your Network Security Group:</span></span>

```powershell
$subnetPrefix = $vnet.Subnets|?{$_.Name -eq 'mySubnet'}

Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name "mySubnet" `
    -AddressPrefix $subnetPrefix.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

<span data-ttu-id="51b0d-118">마지막으로 사용한 가상 네트워크를 업데이트 [집합 AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) 변경 tootake 효과 대 한 순서 대로:</span><span class="sxs-lookup"><span data-stu-id="51b0d-118">Finally, update your virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) in order for your changes tootake effect:</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```


## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="51b0d-119">네트워크 보안 그룹에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="51b0d-119">More information on Network Security Groups</span></span>
<span data-ttu-id="51b0d-120">빠른 명령을 여기 hello를 사용 하면를 tooget 및 트래픽 이동을 tooyour VM으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="51b0d-120">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="51b0d-121">네트워크 보안 그룹 많은 향상 된 기능 및 제어 tooyour 리소스 액세스에 대 한 세분성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="51b0d-121">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="51b0d-122">[여기서 네트워크 보안 그룹 및 ACL 규칙 만들기](tutorial-virtual-network.md#manage-internal-traffic)에 대해 자세히 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="51b0d-122">You can read more about [creating a Network Security Group and ACL rules here](tutorial-virtual-network.md#manage-internal-traffic).</span></span>

<span data-ttu-id="51b0d-123">고가용성 웹 응용 프로그램인 경우 VM을 Azure Load Balancer 뒤에 배치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51b0d-123">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="51b0d-124">hello 부하 분산 장치 트래픽 tooVMs 트래픽 필터링이 제공 하는 네트워크 보안 그룹에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="51b0d-124">hello load balancer distributes traffic tooVMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="51b0d-125">자세한 내용은 참조 [어떻게 tooload 균형 Linux 가상 컴퓨터에서 Azure toocreate 항상 사용 가능한 응용 프로그램](tutorial-load-balancer.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="51b0d-125">For more information, see [How tooload balance Linux virtual machines in Azure toocreate a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="51b0d-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="51b0d-126">Next steps</span></span>
<span data-ttu-id="51b0d-127">이 예제에서는 간단한 규칙 tooallow HTTP 트래픽을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="51b0d-127">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="51b0d-128">Hello 문서 다음에 보다 자세한 환경을 만드는 방법에 대 한 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51b0d-128">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="51b0d-129">Azure Resource Manager 개요</span><span class="sxs-lookup"><span data-stu-id="51b0d-129">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="51b0d-130">NSG(네트워크 보안 그룹)란?</span><span class="sxs-lookup"><span data-stu-id="51b0d-130">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="51b0d-131">부하 분산 장치에 대한 Azure Resource Manager 개요</span><span class="sxs-lookup"><span data-stu-id="51b0d-131">Azure Resource Manager Overview for Load Balancers</span></span>](../../load-balancer/load-balancer-arm.md)

