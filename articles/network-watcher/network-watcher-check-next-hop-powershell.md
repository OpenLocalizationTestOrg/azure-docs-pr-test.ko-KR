---
title: "Azure 네트워크 감시자 다음 홉-PowerShell aaaFind 다음 홉 | Microsoft Docs"
description: "이 문서는 다음 홉 형식 어떤 hello 및 PowerShell을 사용 하 여 다음 홉 ip 주소를 사용 하 여를 찾는 방법을 설명 합니다."
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
ms.openlocfilehash: fdb0b4a02d95fc45c103fe952fc1afa095414c18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-powershell"></a><span data-ttu-id="f2fb0-103">어떤 hello 다음 홉 형식이 hello 다음 홉 기능을 사용 하는 PowerShell을 사용 하 여 Azure 네트워크 감시자 확인</span><span class="sxs-lookup"><span data-stu-id="f2fb0-103">Find out what hello next hop type is using hello Next Hop capability in Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="f2fb0-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="f2fb0-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="f2fb0-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f2fb0-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="f2fb0-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="f2fb0-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="f2fb0-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f2fb0-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="f2fb0-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="f2fb0-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="f2fb0-109">다음 홉 hello 기능을 제공 하는 네트워크 감시자의 기능을 가져오고 hello 다음 홉 형식이 지정 된 가상 컴퓨터를 기반으로 하는 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fb0-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="f2fb0-110">이 기능은 가상 컴퓨터를 종료 하는 트래픽이 게이트웨이, 인터넷 또는 가상 네트워크 tooget tooits 대상에서 이동 하는 경우를 결정 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fb0-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f2fb0-111">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="f2fb0-111">Before you begin</span></span>

<span data-ttu-id="f2fb0-112">이 시나리오에서는 Azure 포털 toofind hello 다음 홉 형식이 hello 및 IP 주소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fb0-112">In this scenario, you will use hello Azure portal toofind hello next hop type and IP address.</span></span>

<span data-ttu-id="f2fb0-113">이 시나리오에서는 hello 단계에 따라 이미 가정 [네트워크 감시자를 만들](network-watcher-create.md) toocreate 네트워크 감시자 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fb0-113">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="f2fb0-114">hello 시나리오는 또한 적합 한 가상 컴퓨터가 리소스 그룹 사용 toobe 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fb0-114">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="f2fb0-115">시나리오</span><span class="sxs-lookup"><span data-stu-id="f2fb0-115">Scenario</span></span>

<span data-ttu-id="f2fb0-116">이 문서에서 설명 하는 hello 시나리오는 다음 홉 hello 다음 홉 형식 및 리소스에 대 한 IP 주소를 확인 하는 네트워크 감시자의 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fb0-116">hello scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="f2fb0-117">다음 홉에 대 한 자세한 toolearn 방문 [다음 홉 개요](network-watcher-next-hop-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fb0-117">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="f2fb0-118">Network Watcher 검색</span><span class="sxs-lookup"><span data-stu-id="f2fb0-118">Retrieve Network Watcher</span></span>

<span data-ttu-id="f2fb0-119">hello 첫 번째 단계는 tooretrieve hello 네트워크 감시자 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fb0-119">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="f2fb0-120">hello `$networkWatcher` 변수 toohello 다음 홉 전달 되는 cmdlet를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fb0-120">hello `$networkWatcher` variable is passed toohello next hop verify cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-virtual-machine"></a><span data-ttu-id="f2fb0-121">가상 컴퓨터 가져오기</span><span class="sxs-lookup"><span data-stu-id="f2fb0-121">Get a virtual machine</span></span>

<span data-ttu-id="f2fb0-122">다음 홉 가상 컴퓨터에서 다음 홉 hello 및 hello hello 다음 홉 IP 주소를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fb0-122">Next hop returns hello next hop and hello IP address of hello next hop from a virtual machine.</span></span> <span data-ttu-id="f2fb0-123">가상 컴퓨터의 Id가 hello cmdlet에 대 한 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fb0-123">An Id of a virtual machine is required for hello cmdlet.</span></span> <span data-ttu-id="f2fb0-124">가상 컴퓨터 toouse hello의 hello ID를 알고 있는 경우이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fb0-124">If you already know hello ID of hello virtual machine toouse, you can skip this step.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

> [!NOTE]
> <span data-ttu-id="f2fb0-125">다음 홉 VM 리소스 hello toorun가 할당 되는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fb0-125">Next hop requires that hello VM resource is allocated toorun.</span></span>

## <a name="get-hello-network-interfaces"></a><span data-ttu-id="f2fb0-126">Hello 네트워크 인터페이스 가져오기</span><span class="sxs-lookup"><span data-stu-id="f2fb0-126">Get hello network interfaces</span></span>

<span data-ttu-id="f2fb0-127">hello 가상 컴퓨터에서 NIC의 IP 주소가 hello hello Nic는 가상 컴퓨터에서 검색 하는이 예에서 필요할 때.</span><span class="sxs-lookup"><span data-stu-id="f2fb0-127">hello IP address of a NIC on hello virtual machine is needed, in this example we retrieve hello NICs on a virtual machine.</span></span> <span data-ttu-id="f2fb0-128">원하는 tootest hello IP 주소를 알고 있으면 hello 가상 컴퓨터에서이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fb0-128">If you already know hello IP address that you want tootest on hello virtual machine, you can skip this step.</span></span>

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="get-next-hop"></a><span data-ttu-id="f2fb0-129">다음 홉 가져오기</span><span class="sxs-lookup"><span data-stu-id="f2fb0-129">Get Next Hop</span></span>

<span data-ttu-id="f2fb0-130">Hello 이라고 이제 `Get-AzureRmNetworkWatcherNextHop` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f2fb0-130">Now we call hello `Get-AzureRmNetworkWatcherNextHop` cmdlet.</span></span> <span data-ttu-id="f2fb0-131">원본 IP 주소 및 대상 IP 주소를 hello cmdlet hello 네트워크 감시자 가상 컴퓨터 Id 통과 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fb0-131">We pass hello cmdlet hello Network Watcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="f2fb0-132">이 예제에서는 hello 대상 IP 주소는 다른 가상 네트워크에 VM tooa 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2fb0-132">In this example, hello destination IP address is tooa VM in another virtual network.</span></span> <span data-ttu-id="f2fb0-133">Hello 두 가상 네트워크 간의 가상 네트워크 게이트웨이는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f2fb0-133">There is a virtual network gateway between hello two virtual networks.</span></span>

```powershell
Get-AzureRmNetworkWatcherNextHop -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id -SourceIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress  -DestinationIPAddress 10.0.2.4 
```

## <a name="review-results"></a><span data-ttu-id="f2fb0-134">결과 검토</span><span class="sxs-lookup"><span data-stu-id="f2fb0-134">Review results</span></span>

<span data-ttu-id="f2fb0-135">완료 되 면 hello 결과가 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2fb0-135">When complete, hello results are provided.</span></span> <span data-ttu-id="f2fb0-136">hello 다음 홉 IP 주소는 리소스의 hello 형식을 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2fb0-136">hello next hop IP address is returned as well as hello type of resource it is.</span></span> <span data-ttu-id="f2fb0-137">이 시나리오에서 hello hello 가상 네트워크 게이트웨이의 공용 IP 주소는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f2fb0-137">In this scenario, it is hello public IP address of hello virtual network gateway.</span></span>

```
NextHopIpAddress NextHopType           RouteTableId 
---------------- -----------           ------------ 
13.78.238.92     VirtualNetworkGateway Gateway Route
```

<span data-ttu-id="f2fb0-138">hello 다음 목록은 hello 현재 사용 가능한 NextHopType 값.</span><span class="sxs-lookup"><span data-stu-id="f2fb0-138">hello following list shows hello currently available NextHopType values:</span></span>

<span data-ttu-id="f2fb0-139">**다음 홉 유형**</span><span class="sxs-lookup"><span data-stu-id="f2fb0-139">**Next Hop Type**</span></span>

* <span data-ttu-id="f2fb0-140">인터넷</span><span class="sxs-lookup"><span data-stu-id="f2fb0-140">Internet</span></span>
* <span data-ttu-id="f2fb0-141">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="f2fb0-141">VirtualAppliance</span></span>
* <span data-ttu-id="f2fb0-142">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="f2fb0-142">VirtualNetworkGateway</span></span>
* <span data-ttu-id="f2fb0-143">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="f2fb0-143">VnetLocal</span></span>
* <span data-ttu-id="f2fb0-144">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="f2fb0-144">HyperNetGateway</span></span>
* <span data-ttu-id="f2fb0-145">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="f2fb0-145">VnetPeering</span></span>
* <span data-ttu-id="f2fb0-146">없음</span><span class="sxs-lookup"><span data-stu-id="f2fb0-146">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2fb0-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f2fb0-147">Next steps</span></span>

<span data-ttu-id="f2fb0-148">자세한 내용은 방법 tooreview 방문 하 여 프로그래밍 방식으로 네트워크 보안 그룹 설정을 [NSG 감사 네트워크 감시자를](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="f2fb0-148">Learn how tooreview your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>

















