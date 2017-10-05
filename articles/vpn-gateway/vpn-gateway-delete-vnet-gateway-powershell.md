---
title: "가상 네트워크 게이트웨이 삭제: PowerShell: Azure Resource Manager | Microsoft Docs"
description: "Resource Manager 배포 모델에서 PowerShell을 사용하여 가상 네트워크 게이트웨이를 삭제합니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: cherylmc
ms.openlocfilehash: 4d0f085423d5bd60b24d88649ee1d77bcd1d009f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="delete-a-virtual-network-gateway-using-powershell"></a><span data-ttu-id="35756-103">PowerShell을 사용하여 가상 네트워크 삭제</span><span class="sxs-lookup"><span data-stu-id="35756-103">Delete a virtual network gateway using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="35756-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="35756-104">Azure portal</span></span>](vpn-gateway-delete-vnet-gateway-portal.md)
> * [<span data-ttu-id="35756-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="35756-105">PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-powershell.md)
> * [<span data-ttu-id="35756-106">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="35756-106">PowerShell (classic)</span></span>](vpn-gateway-delete-vnet-gateway-classic-powershell.md)
>
>

<span data-ttu-id="35756-107">VPN 게이트웨이 구성에 대한 가상 네트워크 게이트웨이 삭제하려는 경우에 몇 가지 다른 접근 방법을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35756-107">There are a couple of different approaches you can take when you want to delete a virtual network gateway for a VPN gateway configuration.</span></span>

- <span data-ttu-id="35756-108">테스트 환경의 경우처럼 모든 항목을 삭제하고 다시 시작하려면 전체 리소스 그룹을 삭제하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="35756-108">If you want to delete everything and start over, as in the case of a test environment, you can delete the resource group.</span></span> <span data-ttu-id="35756-109">리소스 그룹을 삭제하면 그룹 내의 모든 리소스가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="35756-109">When you delete a resource group, it deletes all the resources within the group.</span></span> <span data-ttu-id="35756-110">이 방법은 리소스 그룹에 리소스를 유지하지 않으려는 경우에만 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="35756-110">This is method is only recommended if you don't want to keep any of the resources in the resource group.</span></span> <span data-ttu-id="35756-111">이 방법을 사용할 때는 몇 가지 리소스만 선택적으로 삭제할 수가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="35756-111">You can't selectively delete only a few resources using this approach.</span></span>

- <span data-ttu-id="35756-112">리소스 그룹에 일부 리소스를 유지하려는 경우 가상 네트워크 게이트웨이를 삭제하는 작업이 좀 더 복잡해집니다.</span><span class="sxs-lookup"><span data-stu-id="35756-112">If you want to keep some of the resources in your resource group, deleting a virtual network gateway becomes slightly more complicated.</span></span> <span data-ttu-id="35756-113">가상 네트워크 게이트웨이를 삭제하려면 먼저 게이트웨이에 의존하는 모든 리소스를 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-113">Before you can delete the virtual network gateway, you must first delete any resources that are dependent on the gateway.</span></span> <span data-ttu-id="35756-114">수행하는 단계는 만든 연결의 유형 및 각 연결에 대한 종속 리소스에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="35756-114">The steps you follow depend on the type of connections that you created and the dependent resources for each connection.</span></span>

## <a name="before-beginning"></a><span data-ttu-id="35756-115">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="35756-115">Before beginning</span></span>

### <a name="1-download-the-latest-azure-resource-manager-powershell-cmdlets"></a><span data-ttu-id="35756-116">1. 최신 Azure Resource Manager PowerShell cmdlet을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-116">1. Download the latest Azure Resource Manager PowerShell cmdlets.</span></span>

<span data-ttu-id="35756-117">최신 버전의 Azure Resource Manager PowerShell cmdlet을 다운로드하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-117">Download and install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="35756-118">PowerShell cmdlet 다운로드 및 설치에 대한 자세한 내용은 [Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35756-118">For more information about downloading and installing PowerShell cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="2-connect-to-your-azure-account"></a><span data-ttu-id="35756-119">2. Azure 계정에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-119">2. Connect to your Azure account.</span></span>

<span data-ttu-id="35756-120">PowerShell 콘솔을 열고 계정에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-120">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="35756-121">연결에 도움이 되도록 다음 예제를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-121">Use the following example to help you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="35756-122">계정에 대한 구독을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-122">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="35756-123">둘 이상의 구독이 있는 경우 사용할 구독을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-123">If you have more than one subscription, specify the subscription that you want to use.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
```

## <span data-ttu-id="35756-124"><a name="S2S"></a>사이트 간 VPN 게이트웨이 삭제</span><span class="sxs-lookup"><span data-stu-id="35756-124"><a name="S2S"></a>Delete a Site-to-Site VPN gateway</span></span>

<span data-ttu-id="35756-125">S2S 구성에 대한 가상 네트워크 게이트웨이를 삭제하려면 먼저 가상 네트워크 게이트웨이와 관련된 각 리소스를 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-125">To delete a virtual network gateway for a S2S configuration, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="35756-126">리소스는 종속성으로 인해 특정 순서로 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-126">Resources must be deleted in a certain order due to dependencies.</span></span> <span data-ttu-id="35756-127">아래 예제를 사용할 경우 일부 값은 지정되어야 하지만 일부 값은 출력 결과로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="35756-127">When working with the examples below, some of the values must be specified, while other values are an output result.</span></span> <span data-ttu-id="35756-128">데모를 위해 예제에 다음과 같은 특정 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-128">We use the following specific values in the examples for demonstration purposes:</span></span>

<span data-ttu-id="35756-129">VNet 이름: VNet1</span><span class="sxs-lookup"><span data-stu-id="35756-129">VNet name: VNet1</span></span><br>
<span data-ttu-id="35756-130">리소스 그룹 이름: RG1</span><span class="sxs-lookup"><span data-stu-id="35756-130">Resource Group name: RG1</span></span><br>
<span data-ttu-id="35756-131">가상 네트워크 게이트웨이 이름: GW1</span><span class="sxs-lookup"><span data-stu-id="35756-131">Virtual network gateway name: GW1</span></span><br>

<span data-ttu-id="35756-132">다음 단계는 Resource Manager 배포 모델에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="35756-132">The following steps apply to the Resource Manager deployment model.</span></span>

### <a name="1-get-the-virtual-network-gateway-that-you-want-to-delete"></a><span data-ttu-id="35756-133">1. 삭제하려는 가상 네트워크 게이트웨이를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="35756-133">1. Get the virtual network gateway that you want to delete.</span></span>

```powershell
$Gateway=get-azurermvirtualnetworkgateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="2-check-to-see-if-the-virtual-network-gateway-has-any-connections"></a><span data-ttu-id="35756-134">2. 가상 네트워크 게이트웨이에 연결이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-134">2. Check to see if the virtual network gateway has any connections.</span></span>

```powershell
get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
$Conns=get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
```

### <a name="3-delete-all-connections"></a><span data-ttu-id="35756-135">3. 모든 연결을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-135">3. Delete all connections.</span></span>

<span data-ttu-id="35756-136">각 연결의 삭제를 확인하라는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35756-136">You may be prompted to confirm the deletion of each of the connections.</span></span>

```powershell
$Conns | ForEach-Object {Remove-AzureRmVirtualNetworkGatewayConnection -Name $_.name -ResourceGroupName $_.ResourceGroupName}
```

### <a name="4-delete-the-virtual-network-gateway"></a><span data-ttu-id="35756-137">4. 가상 네트워크 게이트웨이를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-137">4. Delete the virtual network gateway.</span></span>

<span data-ttu-id="35756-138">게이트웨이의 삭제를 확인하라는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35756-138">You may be prompted to confirm the deletion of the gateway.</span></span> <span data-ttu-id="35756-139">이 VNet에 S2S 구성 외에 P2S 구성이 있는 경우 가상 네트워크 게이트웨이를 삭제하면 경고 없이 모든 P2S 클라이언트의 연결이 자동으로 끊어집니다.</span><span class="sxs-lookup"><span data-stu-id="35756-139">If you have a P2S configuration to this VNet in addition to your S2S configuration, deleting the virtual network gateway will automatically disconnect all P2S clients without warning.</span></span>


```powershell
Remove-AzureRmVirtualNetworkGateway -Name "GW1" -ResourceGroupName "RG1"
```

<span data-ttu-id="35756-140">이때 가상 네트워크 게이트웨이가 삭제되었습니다.</span><span class="sxs-lookup"><span data-stu-id="35756-140">At this point, your virtual network gateway has been deleted.</span></span> <span data-ttu-id="35756-141">다음 단계를 사용하여 더 이상 사용되지 않는 모든 리소스를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35756-141">You can use the next steps to delete any resources that are no longer being used.</span></span>

### <a name="5-delete-the-local-network-gateways"></a><span data-ttu-id="35756-142">5. 로컬 네트워크 게이트웨이를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-142">5 Delete the local network gateways.</span></span>

<span data-ttu-id="35756-143">해당 로컬 네트워크 게이트웨이 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="35756-143">Get the list of the corresponding local network gateways.</span></span>

```powershell
$LNG=Get-AzureRmLocalNetworkGateway -ResourceGroupName "RG1" | where-object {$_.Id -In $Conns.LocalNetworkGateway2.Id}
```

<span data-ttu-id="35756-144">로컬 네트워크 게이트웨이를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-144">Delete the local network gateways.</span></span> <span data-ttu-id="35756-145">각 로컬 네트워크 게이트웨이의 삭제를 확인하라는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35756-145">You may be prompted to confirm the deletion of each of the local network gateway.</span></span>

```powershell
$LNG | ForEach-Object {Remove-AzureRmLocalNetworkGateway -Name $_.Name -ResourceGroupName $_.ResourceGroupName}
```

### <a name="6-delete-the-public-ip-address-resources"></a><span data-ttu-id="35756-146">6. 공용 IP 주소 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-146">6. Delete the Public IP address resources.</span></span>

<span data-ttu-id="35756-147">가상 네트워크 게이트웨이의 IP 구성을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="35756-147">Get the IP configurations of the virtual network gateway.</span></span>

```powershell
$GWIpConfigs = $Gateway.IpConfigurations
```

<span data-ttu-id="35756-148">이 가상 네트워크 게이트웨이에 사용되는 공용 IP 주소 리소스 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="35756-148">Get the list of Public IP address resources used for this virtual network gateway.</span></span> <span data-ttu-id="35756-149">가상 네트워크 게이트웨이가 활성-활성인 경우 두 개의 공용 IP 주소가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="35756-149">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span>

```powershell
$PubIP=Get-AzureRmPublicIpAddress | where-object {$_.Id -In $GWIpConfigs.PublicIpAddress.Id}
```

<span data-ttu-id="35756-150">공용 IP 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-150">Delete the Public IP resources.</span></span>

```powershell
$PubIP | foreach-object {remove-azurermpublicIpAddress -Name $_.Name -ResourceGroupName "RG1"}
```

### <a name="7-delete-the-gateway-subnet-and-set-the-configuration"></a><span data-ttu-id="35756-151">7. 게이트웨이 서브넷을 삭제하고 구성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-151">7. Delete the gateway subnet and set the configuration.</span></span>

```powershell
$GWSub = Get-AzureRmVirtualNetwork -ResourceGroupName "RG1" -Name "VNet1" | Remove-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet"
Set-AzureRmVirtualNetwork -VirtualNetwork $GWSub
```

## <span data-ttu-id="35756-152"><a name="v2v"></a>VNet 간 VPN 게이트웨이 삭제</span><span class="sxs-lookup"><span data-stu-id="35756-152"><a name="v2v"></a>Delete a VNet-to-VNet VPN gateway</span></span>

<span data-ttu-id="35756-153">V2V 구성에 대한 가상 네트워크 게이트웨이를 삭제하려면 먼저 가상 네트워크 게이트웨이와 관련된 각 리소스를 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-153">To delete a virtual network gateway for a V2V configuration, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="35756-154">리소스는 종속성으로 인해 특정 순서로 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-154">Resources must be deleted in a certain order due to dependencies.</span></span> <span data-ttu-id="35756-155">아래 예제를 사용할 경우 일부 값은 지정되어야 하지만 일부 값은 출력 결과로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="35756-155">When working with the examples below, some of the values must be specified, while other values are an output result.</span></span> <span data-ttu-id="35756-156">데모를 위해 예제에 다음과 같은 특정 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-156">We use the following specific values in the examples for demonstration purposes:</span></span>

<span data-ttu-id="35756-157">VNet 이름: VNet1</span><span class="sxs-lookup"><span data-stu-id="35756-157">VNet name: VNet1</span></span><br>
<span data-ttu-id="35756-158">리소스 그룹 이름: RG1</span><span class="sxs-lookup"><span data-stu-id="35756-158">Resource Group name: RG1</span></span><br>
<span data-ttu-id="35756-159">가상 네트워크 게이트웨이 이름: GW1</span><span class="sxs-lookup"><span data-stu-id="35756-159">Virtual network gateway name: GW1</span></span><br>

<span data-ttu-id="35756-160">다음 단계는 Resource Manager 배포 모델에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="35756-160">The following steps apply to the Resource Manager deployment model.</span></span>

### <a name="1-get-the-virtual-network-gateway-that-you-want-to-delete"></a><span data-ttu-id="35756-161">1. 삭제하려는 가상 네트워크 게이트웨이를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="35756-161">1. Get the virtual network gateway that you want to delete.</span></span>

```powershell
$Gateway=get-azurermvirtualnetworkgateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="2-check-to-see-if-the-virtual-network-gateway-has-any-connections"></a><span data-ttu-id="35756-162">2. 가상 네트워크 게이트웨이에 연결이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-162">2. Check to see if the virtual network gateway has any connections.</span></span>

```powershell
get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
```
 
<span data-ttu-id="35756-163">다른 리소스 그룹의 일부인 가상 네트워크 게이트웨이에 대한 다른 연결이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35756-163">There may be other connections to the virtual network gateway that are part of a different resource group.</span></span> <span data-ttu-id="35756-164">각 추가 리소스 그룹에서 추가 연결을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-164">Check for additional connections in each additional resource group.</span></span> <span data-ttu-id="35756-165">이 예제에서 RG2의 연결을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-165">In this example, we are checking for connections from RG2.</span></span> <span data-ttu-id="35756-166">가상 네트워크 게이트웨이에 연결되어 있을 수 있는 각 리소스 그룹에 대해 이 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-166">Run this for each resource group that you have which may have a connection to the virtual network gateway.</span></span>

```powershell
get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG2" | where-object {$_.VirtualNetworkGateway2.Id -eq $GW.Id}
```

### <a name="3-get-the-list-of-connections-in-both-directions"></a><span data-ttu-id="35756-167">3. 양방향으로 연결 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="35756-167">3. Get the list of connections in both directions.</span></span>

<span data-ttu-id="35756-168">VNet 간 구성이기 때문에 양방향 연결 목록이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-168">Because this is a VNet-to-VNet configuration, you need the list of connections in both directions.</span></span>

```powershell
$ConnsL=get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
```
 
<span data-ttu-id="35756-169">이 예제에서 RG2의 연결을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-169">In this example, we are checking for connections from RG2.</span></span> <span data-ttu-id="35756-170">가상 네트워크 게이트웨이에 연결되어 있을 수 있는 각 리소스 그룹에 대해 이 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-170">Run this for each resource group that you have which may have a connection to the virtual network gateway.</span></span>

```powershell
 $ConnsR=get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "<NameOfResourceGroup2>" | where-object {$_.VirtualNetworkGateway2.Id -eq $GW.Id}
 ```

### <a name="4-delete-all-connections"></a><span data-ttu-id="35756-171">4. 모든 연결을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-171">4. Delete all connections.</span></span>

<span data-ttu-id="35756-172">각 연결의 삭제를 확인하라는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35756-172">You may be prompted to confirm the deletion of each of the connections.</span></span>

```powershell
$ConnsL | ForEach-Object {Remove-AzureRmVirtualNetworkGatewayConnection -Name $_.name -ResourceGroupName $_.ResourceGroupName}
$ConnsR | ForEach-Object {Remove-AzureRmVirtualNetworkGatewayConnection -Name $_.name -ResourceGroupName $_.ResourceGroupName}
```

### <a name="5-delete-the-virtual-network-gateway"></a><span data-ttu-id="35756-173">5. 가상 네트워크 게이트웨이를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-173">5. Delete the virtual network gateway.</span></span>

<span data-ttu-id="35756-174">가상 네트워크 게이트웨이의 삭제를 확인하라는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35756-174">You may be prompted to confirm the deletion of the virtual network gateway.</span></span> <span data-ttu-id="35756-175">VNet에 V2V 구성 외에 P2S 구성이 있는 경우 가상 네트워크 게이트웨이를 삭제하면 경고 없이 모든 P2S 클라이언트의 연결이 자동으로 끊어집니다.</span><span class="sxs-lookup"><span data-stu-id="35756-175">If you have P2S configurations to your VNets in addition to your V2V configuration, deleting the virtual network gateways will automatically disconnect all P2S clients without warning.</span></span>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name "GW1" -ResourceGroupName "RG1"
```

<span data-ttu-id="35756-176">이때 가상 네트워크 게이트웨이가 삭제되었습니다.</span><span class="sxs-lookup"><span data-stu-id="35756-176">At this point, your virtual network gateway has been deleted.</span></span> <span data-ttu-id="35756-177">다음 단계를 사용하여 더 이상 사용되지 않는 모든 리소스를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35756-177">You can use the next steps to delete any resources that are no longer being used.</span></span>

### <a name="6-delete-the-public-ip-address-resources"></a><span data-ttu-id="35756-178">6. 공용 IP 주소 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-178">6. Delete the Public IP address resources</span></span>

<span data-ttu-id="35756-179">가상 네트워크 게이트웨이의 IP 구성을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="35756-179">Get the IP configurations of the virtual network gateway.</span></span>

```powershell
$GWIpConfigs = $Gateway.IpConfigurations
```

<span data-ttu-id="35756-180">이 가상 네트워크 게이트웨이에 사용되는 공용 IP 주소 리소스 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="35756-180">Get the list of Public IP address resources used for this virtual network gateway.</span></span> <span data-ttu-id="35756-181">가상 네트워크 게이트웨이가 활성-활성인 경우 두 개의 공용 IP 주소가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="35756-181">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span>

```powershell
$PubIP=Get-AzureRmPublicIpAddress | where-object {$_.Id -In $GWIpConfigs.PublicIpAddress.Id}
```

<span data-ttu-id="35756-182">공용 IP 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-182">Delete the Public IP resources.</span></span> <span data-ttu-id="35756-183">공용 IP의 삭제를 확인하라는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35756-183">You may be prompted to confirm the deletion of the Public IP.</span></span>

```powershell
$PubIP | foreach-object {remove-azurermpublicIpAddress -Name $_.Name -ResourceGroupName "<NameOfResourceGroup1>"}
```

### <a name="7-delete-the-gateway-subnet-and-set-the-configuration"></a><span data-ttu-id="35756-184">7. 게이트웨이 서브넷을 삭제하고 구성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-184">7. Delete the gateway subnet and set the configuration.</span></span>

```powershell
$GWSub = Get-AzureRmVirtualNetwork -ResourceGroupName "RG1" -Name "VNet1" | Remove-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet"
Set-AzureRmVirtualNetwork -VirtualNetwork $GWSub
```

## <span data-ttu-id="35756-185"><a name="deletep2s"></a>지점 및 사이트 간 VPN Gateway 삭제</span><span class="sxs-lookup"><span data-stu-id="35756-185"><a name="deletep2s"></a>Delete a Point-to-Site VPN gateway</span></span>

<span data-ttu-id="35756-186">P2S 구성에 대한 가상 네트워크 게이트웨이를 삭제하려면 먼저 가상 네트워크 게이트웨이와 관련된 각 리소스를 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-186">To delete a virtual network gateway for a P2S configuration, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="35756-187">리소스는 종속성으로 인해 특정 순서로 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-187">Resources must be deleted in a certain order due to dependencies.</span></span> <span data-ttu-id="35756-188">아래 예제를 사용할 경우 일부 값은 지정되어야 하지만 일부 값은 출력 결과로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="35756-188">When working with the examples below, some of the values must be specified, while other values are an output result.</span></span> <span data-ttu-id="35756-189">데모를 위해 예제에 다음과 같은 특정 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-189">We use the following specific values in the examples for demonstration purposes:</span></span>

<span data-ttu-id="35756-190">VNet 이름: VNet1</span><span class="sxs-lookup"><span data-stu-id="35756-190">VNet name: VNet1</span></span><br>
<span data-ttu-id="35756-191">리소스 그룹 이름: RG1</span><span class="sxs-lookup"><span data-stu-id="35756-191">Resource Group name: RG1</span></span><br>
<span data-ttu-id="35756-192">가상 네트워크 게이트웨이 이름: GW1</span><span class="sxs-lookup"><span data-stu-id="35756-192">Virtual network gateway name: GW1</span></span><br>

<span data-ttu-id="35756-193">다음 단계는 Resource Manager 배포 모델에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="35756-193">The following steps apply to the Resource Manager deployment model.</span></span>


>[!NOTE]
> <span data-ttu-id="35756-194">VPN Gateway를 삭제하면 경고 없이 VNet에서 연결된 모든 클라이언트의 연결이 끊어집니다.</span><span class="sxs-lookup"><span data-stu-id="35756-194">When you delete the VPN gateway, all connected clients will be disconnected from the VNet without warning.</span></span>
>
>

### <a name="1-get-the-virtual-network-gateway-that-you-want-to-delete"></a><span data-ttu-id="35756-195">1. 삭제하려는 가상 네트워크 게이트웨이를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="35756-195">1. Get the virtual network gateway that you want to delete.</span></span>

```powershell
$Gateway=get-azurermvirtualnetworkgateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="2-delete-the-virtual-network-gateway"></a><span data-ttu-id="35756-196">2. 가상 네트워크 게이트웨이를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-196">2. Delete the virtual network gateway.</span></span>

<span data-ttu-id="35756-197">가상 네트워크 게이트웨이의 삭제를 확인하라는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35756-197">You may be prompted to confirm the deletion of the virtual network gateway.</span></span>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name "GW1" -ResourceGroupName "RG1"
```

<span data-ttu-id="35756-198">이때 가상 네트워크 게이트웨이가 삭제되었습니다.</span><span class="sxs-lookup"><span data-stu-id="35756-198">At this point, your virtual network gateway has been deleted.</span></span> <span data-ttu-id="35756-199">다음 단계를 사용하여 더 이상 사용되지 않는 모든 리소스를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35756-199">You can use the next steps to delete any resources that are no longer being used.</span></span>

### <a name="3-delete-the-public-ip-address-resources"></a><span data-ttu-id="35756-200">3. 공용 IP 주소 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-200">3. Delete the Public IP address resources</span></span>

<span data-ttu-id="35756-201">가상 네트워크 게이트웨이의 IP 구성을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="35756-201">Get the IP configurations of the virtual network gateway.</span></span>

```powershell
$GWIpConfigs = $Gateway.IpConfigurations
```

<span data-ttu-id="35756-202">이 가상 네트워크 게이트웨이에 사용되는 공용 IP 주소 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="35756-202">Get the list of Public IP addresses used for this virtual network gateway.</span></span> <span data-ttu-id="35756-203">가상 네트워크 게이트웨이가 활성-활성인 경우 두 개의 공용 IP 주소가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="35756-203">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span>

```powershell
$PubIP=Get-AzureRmPublicIpAddress | where-object {$_.Id -In $GWIpConfigs.PublicIpAddress.Id}
```

<span data-ttu-id="35756-204">공용 IP를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-204">Delete the Public IPs.</span></span> <span data-ttu-id="35756-205">공용 IP의 삭제를 확인하라는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35756-205">You may be prompted to confirm the deletion of the Public IP.</span></span>

```powershell
$PubIP | foreach-object {remove-azurermpublicIpAddress -Name $_.Name -ResourceGroupName "<NameOfResourceGroup1>"}
```

### <a name="4-delete-the-gateway-subnet-and-set-the-configuration"></a><span data-ttu-id="35756-206">4. 게이트웨이 서브넷을 삭제하고 구성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-206">4. Delete the gateway subnet and set the configuration.</span></span>

```powershell
$GWSub = Get-AzureRmVirtualNetwork -ResourceGroupName "RG1" -Name "VNet1" | Remove-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet"
Set-AzureRmVirtualNetwork -VirtualNetwork $GWSub
```

## <span data-ttu-id="35756-207"><a name="delete"></a>리소스 그룹을 삭제하여 VPN 게이트웨이 삭제</span><span class="sxs-lookup"><span data-stu-id="35756-207"><a name="delete"></a>Delete a VPN gateway by deleting the resource group</span></span>

<span data-ttu-id="35756-208">리소스 그룹에 리소스를 유지하지 않고 새로 시작하려는 경우 전체 리소스 그룹을 삭제하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="35756-208">If you are not concerned about keeping any of your resources in the resource group and you just want to start over, you can delete an entire resource group.</span></span> <span data-ttu-id="35756-209">모든 항목을 제거하는 빠른 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="35756-209">This is a quick way to remove everything.</span></span> <span data-ttu-id="35756-210">다음 단계는 Resource Manager 배포 모델에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="35756-210">The following steps apply only to the Resource Manager deployment model.</span></span>

### <a name="1-get-a-list-of-all-the-resource-groups-in-your-subscription"></a><span data-ttu-id="35756-211">1. 구독 중인 모든 리소스 그룹 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="35756-211">1. Get a list of all the resource groups in your subscription.</span></span>

```powershell
Get-AzureRmResourceGroup
```

### <a name="2-locate-the-resource-group-that-you-want-to-delete"></a><span data-ttu-id="35756-212">2. 삭제할 리소스 그룹을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="35756-212">2. Locate the resource group that you want to delete.</span></span>

<span data-ttu-id="35756-213">삭제하려는 리소스 그룹을 찾고 해당 리소스 그룹의 리소스 목록을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-213">Locate the resource group that you want to delete and view the list of resources in that resource group.</span></span> <span data-ttu-id="35756-214">이 예제에서 리소스 그룹의 이름은 RG1입니다.</span><span class="sxs-lookup"><span data-stu-id="35756-214">In the example, the name of the resource group is RG1.</span></span> <span data-ttu-id="35756-215">모든 리소스 목록을 검색하도록 예제를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-215">Modify the example to retrieve a list of all the resources.</span></span>

```powershell
Find-AzureRmResource -ResourceGroupNameContains RG1
```

### <a name="3-verify-the-resources-in-the-list"></a><span data-ttu-id="35756-216">3. 목록의 리소스를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-216">3. Verify the resources in the list.</span></span>

<span data-ttu-id="35756-217">목록이 반환되면 리소스 그룹의 모든 리소스와 리소스 그룹 자체를 삭제할 것인지도 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-217">When the list is returned, review it to verify that you want to delete all the resources in the resource group, as well as the resource group itself.</span></span> <span data-ttu-id="35756-218">리소스 그룹에 일부 리소스를 유지하려면 이 문서에 있는 이전 섹션의 단계를 사용하여 게이트웨이를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-218">If you want to keep some of the resources in the resource group, use the steps in the earlier sections of this article to delete your gateway.</span></span>

### <a name="4-delete-the-resource-group-and-resources"></a><span data-ttu-id="35756-219">4. 리소스 그룹 및 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-219">4. Delete the resource group and resources.</span></span>

<span data-ttu-id="35756-220">리소스 그룹 및 리소스 그룹에 포함된 모든 리소스를 삭제하려면 예제를 수정하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-220">To delete the resource group and all the resource contained in the resource group, modify the example and run.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name RG1
```

### <a name="5-check-the-status"></a><span data-ttu-id="35756-221">5. 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="35756-221">5. Check the status.</span></span>

<span data-ttu-id="35756-222">Azure에서 모든 리소스를 삭제하려면 다소 시간이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="35756-222">It takes some time for Azure to delete all the resources.</span></span> <span data-ttu-id="35756-223">다음 cmdlet을 사용하여 리소스 그룹의 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35756-223">You can check the status of your resource group by using this cmdlet.</span></span>

```powershell
Get-AzureRmResourceGroup -ResourceGroupName RG1
```

<span data-ttu-id="35756-224">반환되는 결과에는 'Succeeded'가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="35756-224">The result that is returned shows 'Succeeded'.</span></span>

```
ResourceGroupName : RG1
Location          : eastus
ProvisioningState : Succeeded
```