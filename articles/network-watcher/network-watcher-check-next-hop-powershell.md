---
title: "Azure Network Watcher Next Hop을 사용하여 다음 홉 찾기 - PowerShell | Microsoft Docs"
description: "이 문서에서는 PowerShell에서 Next Hop을 사용하여 다음 홉 유형 및 IP 주소를 찾을 수 있는 방법을 설명합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 6a656c55-17bd-40f1-905d-90659087639c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 00161e7c6fb4becdb7d8eab266fa27128e50f8ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-azure-network-watcher-using-powershell"></a><span data-ttu-id="635f7-103">PowerShell을 사용하는 Azure Network Watcher에서 Next Hop 기능을 사용하는 다음 홉이 무엇인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="635f7-103">Find out what the next hop type is using the Next Hop capability in Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="635f7-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="635f7-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="635f7-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="635f7-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="635f7-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="635f7-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="635f7-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="635f7-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="635f7-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="635f7-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="635f7-109">Next Hop은 Network Watcher의 기능으로 지정된 가상 컴퓨터를 기반으로 하는 다음 홉 유형 및 IP 주소를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="635f7-109">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="635f7-110">이 기능은 가상 컴퓨터에서 나가는 트래픽이 게이트웨이, 인터넷 또는 가상 네트워크를 트래버스하여 대상에 도달할지 여부를 결정하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="635f7-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="635f7-111">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="635f7-111">Before you begin</span></span>

<span data-ttu-id="635f7-112">이 시나리오에서는 Azure Portal을 사용하여 다음 홉 유형 및 IP 주소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="635f7-112">In this scenario, you will use the Azure portal to find the next hop type and IP address.</span></span>

<span data-ttu-id="635f7-113">이 시나리오에서는 사용자가 Network Watcher를 만드는 [Network Watcher 만들기](network-watcher-create.md)의 단계를 이미 수행했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="635f7-113">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="635f7-114">또한 시나리오에서는 유효한 가상 컴퓨터를 포함한 리소스 그룹을 사용할 수 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="635f7-114">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="635f7-115">시나리오</span><span class="sxs-lookup"><span data-stu-id="635f7-115">Scenario</span></span>

<span data-ttu-id="635f7-116">이 문서에서 다루는 시나리오는 리소스에 대한 다음 홉 유형 및 IP 주소를 찾는 Network Watcher의 기능인 Next Hop을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="635f7-116">The scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="635f7-117">Next Hop에 대한 자세한 내용을 보려면 [Next Hop 개요](network-watcher-next-hop-overview.md)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="635f7-117">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="635f7-118">Network Watcher 검색</span><span class="sxs-lookup"><span data-stu-id="635f7-118">Retrieve Network Watcher</span></span>

<span data-ttu-id="635f7-119">첫 번째 단계는 Network Watcher 인스턴스를 검색하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="635f7-119">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="635f7-120">`$networkWatcher` 변수는 다음 홉 확인 cmdlet으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="635f7-120">The `$networkWatcher` variable is passed to the next hop verify cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-virtual-machine"></a><span data-ttu-id="635f7-121">가상 컴퓨터 가져오기</span><span class="sxs-lookup"><span data-stu-id="635f7-121">Get a virtual machine</span></span>

<span data-ttu-id="635f7-122">Next Hop이 가상 컴퓨터에서 다음 홉과 다음 홉의 IP 주소를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="635f7-122">Next hop returns the next hop and the IP address of the next hop from a virtual machine.</span></span> <span data-ttu-id="635f7-123">가상 컴퓨터의 ID가 cmdlet에 대해 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="635f7-123">An Id of a virtual machine is required for the cmdlet.</span></span> <span data-ttu-id="635f7-124">사용할 가상 컴퓨터의 ID를 이미 알고 있는 경우 이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="635f7-124">If you already know the ID of the virtual machine to use, you can skip this step.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

> [!NOTE]
> <span data-ttu-id="635f7-125">다음 홉에서는 VM 리소스가 실행되기 위해 할당되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="635f7-125">Next hop requires that the VM resource is allocated to run.</span></span>

## <a name="get-the-network-interfaces"></a><span data-ttu-id="635f7-126">네트워크 인터페이스 가져오기</span><span class="sxs-lookup"><span data-stu-id="635f7-126">Get the network interfaces</span></span>

<span data-ttu-id="635f7-127">가상 컴퓨터에 있는 NIC의 IP 주소가 필요합니다. 이 예제에서는 가상 컴퓨터의 NIC를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="635f7-127">The IP address of a NIC on the virtual machine is needed, in this example we retrieve the NICs on a virtual machine.</span></span> <span data-ttu-id="635f7-128">가상 컴퓨터에서 테스트하려는 IP 주소를 이미 알고 있는 경우 이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="635f7-128">If you already know the IP address that you want to test on the virtual machine, you can skip this step.</span></span>

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="get-next-hop"></a><span data-ttu-id="635f7-129">다음 홉 가져오기</span><span class="sxs-lookup"><span data-stu-id="635f7-129">Get Next Hop</span></span>

<span data-ttu-id="635f7-130">이제 `Get-AzureRmNetworkWatcherNextHop` cmdlet을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="635f7-130">Now we call the `Get-AzureRmNetworkWatcherNextHop` cmdlet.</span></span> <span data-ttu-id="635f7-131">cmdlet을 Network Watcher, 가상 컴퓨터 ID, 원본 IP 주소 및 대상 IP 주소에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="635f7-131">We pass the cmdlet the Network Watcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="635f7-132">이 예제에서 대상 IP 주소는 다른 가상 네트워크의 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="635f7-132">In this example, the destination IP address is to a VM in another virtual network.</span></span> <span data-ttu-id="635f7-133">두 개의 가상 네트워크 간에 가상 네트워크 게이트웨이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="635f7-133">There is a virtual network gateway between the two virtual networks.</span></span>

```powershell
Get-AzureRmNetworkWatcherNextHop -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id -SourceIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress  -DestinationIPAddress 10.0.2.4 
```

## <a name="review-results"></a><span data-ttu-id="635f7-134">결과 검토</span><span class="sxs-lookup"><span data-stu-id="635f7-134">Review results</span></span>

<span data-ttu-id="635f7-135">완료되면 결과가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="635f7-135">When complete, the results are provided.</span></span> <span data-ttu-id="635f7-136">리소스의 유형뿐만 아니라 다음 홉 IP 주소가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="635f7-136">The next hop IP address is returned as well as the type of resource it is.</span></span> <span data-ttu-id="635f7-137">이 시나리오에서는 가상 네트워크 게이트웨이의 공용 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="635f7-137">In this scenario, it is the public IP address of the virtual network gateway.</span></span>

```
NextHopIpAddress NextHopType           RouteTableId 
---------------- -----------           ------------ 
13.78.238.92     VirtualNetworkGateway Gateway Route
```

<span data-ttu-id="635f7-138">다음 목록에서는 현재 사용할 수 있는 NextHopType 값을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="635f7-138">The following list shows the currently available NextHopType values:</span></span>

<span data-ttu-id="635f7-139">**다음 홉 유형**</span><span class="sxs-lookup"><span data-stu-id="635f7-139">**Next Hop Type**</span></span>

* <span data-ttu-id="635f7-140">인터넷</span><span class="sxs-lookup"><span data-stu-id="635f7-140">Internet</span></span>
* <span data-ttu-id="635f7-141">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="635f7-141">VirtualAppliance</span></span>
* <span data-ttu-id="635f7-142">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="635f7-142">VirtualNetworkGateway</span></span>
* <span data-ttu-id="635f7-143">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="635f7-143">VnetLocal</span></span>
* <span data-ttu-id="635f7-144">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="635f7-144">HyperNetGateway</span></span>
* <span data-ttu-id="635f7-145">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="635f7-145">VnetPeering</span></span>
* <span data-ttu-id="635f7-146">없음</span><span class="sxs-lookup"><span data-stu-id="635f7-146">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="635f7-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="635f7-147">Next steps</span></span>

<span data-ttu-id="635f7-148">[Network Watcher를 사용하여 NSG 감사](network-watcher-nsg-auditing-powershell.md)를 방문하여 네트워크 보안 그룹 설정을 프로그래밍 방식으로 검토하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="635f7-148">Learn how to review your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>

















