---
title: "Azure 네트워크 감시자 다음 홉-Azure CLI 1.0 aaaFind 다음 홉 | Microsoft Docs"
description: "이 문서는 어떤 hello 다음 홉 형식 및 Azure CLI를 사용 하 여 다음 홉 ip 주소를 사용 하 여를 찾는 방법을 설명 합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 0700c274-3e0d-4dca-acfa-3ceac8990613
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 54124c051021413695d70ba93c370605abc6ebbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-azure-cli-10"></a><span data-ttu-id="42b58-103">어떤 hello 다음 홉 형식이 hello 다음 홉 기능을 사용 하는 Azure CLI 1.0을 사용 하 여 Azure 네트워크 감시자 확인</span><span class="sxs-lookup"><span data-stu-id="42b58-103">Find out what hello next hop type is using hello Next Hop capability in Azure Network Watcher using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="42b58-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="42b58-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="42b58-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="42b58-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="42b58-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="42b58-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="42b58-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="42b58-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="42b58-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="42b58-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="42b58-109">다음 홉 hello 기능을 제공 하는 네트워크 감시자의 기능을 가져오고 hello 다음 홉 형식이 지정 된 가상 컴퓨터를 기반으로 하는 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="42b58-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="42b58-110">이 기능은 가상 컴퓨터를 종료 하는 트래픽이 게이트웨이, 인터넷 또는 가상 네트워크 tooget tooits 대상에서 이동 하는 경우를 결정 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b58-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

<span data-ttu-id="42b58-111">이 문서에서는 Windows, Mac 및 Linux에 사용할 수 있는 플랫폼 간 Azure CLI 1.0을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="42b58-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="42b58-112">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="42b58-112">Before you begin</span></span>

<span data-ttu-id="42b58-113">이 시나리오에서는 Azure CLI toofind hello 다음 홉 형식이 hello 및 IP 주소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b58-113">In this scenario, you will use hello Azure CLI toofind hello next hop type and IP address.</span></span>

<span data-ttu-id="42b58-114">이 시나리오에서는 hello 단계에 따라 이미 가정 [네트워크 감시자를 만들](network-watcher-create.md) toocreate 네트워크 감시자 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b58-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="42b58-115">hello 시나리오는 또한 적합 한 가상 컴퓨터가 리소스 그룹 사용 toobe 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b58-115">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="42b58-116">시나리오</span><span class="sxs-lookup"><span data-stu-id="42b58-116">Scenario</span></span>

<span data-ttu-id="42b58-117">이 문서에서 설명 하는 hello 시나리오는 다음 홉 hello 다음 홉 형식 및 리소스에 대 한 IP 주소를 확인 하는 네트워크 감시자의 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b58-117">hello scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="42b58-118">다음 홉에 대 한 자세한 toolearn 방문 [다음 홉 개요](network-watcher-next-hop-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="42b58-118">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>


## <a name="get-next-hop"></a><span data-ttu-id="42b58-119">다음 홉 가져오기</span><span class="sxs-lookup"><span data-stu-id="42b58-119">Get Next Hop</span></span>

<span data-ttu-id="42b58-120">hello 이라고 tooget hello 다음 홉 `azure netowrk watcher next-hop` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="42b58-120">tooget hello next hop we call hello `azure netowrk watcher next-hop` cmdlet.</span></span> <span data-ttu-id="42b58-121">Hello cmdlet hello 네트워크 감시자 리소스 그룹, hello NetworkWatcher, 가상 컴퓨터 Id, 원본 IP 주소 및 대상 IP 주소 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="42b58-121">We pass hello cmdlet hello Network Watcher resource group, hello NetworkWatcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="42b58-122">이 예제에서는 hello 대상 IP 주소는 다른 가상 네트워크에 VM tooa 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b58-122">In this example, hello destination IP address is tooa VM in another virtual network.</span></span> <span data-ttu-id="42b58-123">Hello 두 가상 네트워크 간의 가상 네트워크 게이트웨이는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="42b58-123">There is a virtual network gateway between hello two virtual networks.</span></span> 

```azurecli
azure network watcher next-hop -g resourceGroupName -n networkWatcherName -t targetResourceId -a <source-ip> -d <destination-ip>
```

> [!NOTE]
<span data-ttu-id="42b58-124">Hello Nic의 IP 전달이 사용 VM hello에 여러 Nic를 다음 NIC 매개 변수 hello (-i nic id)를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="42b58-124">If hello VM has multiple NICs and IP forwarding is enabled on any of hello NICs, then hello NIC parameter (-i nic-id) must be specified.</span></span> <span data-ttu-id="42b58-125">그렇지 않은 경우 선택적입니다.</span><span class="sxs-lookup"><span data-stu-id="42b58-125">Otherwise it is optional.</span></span>

## <a name="review-results"></a><span data-ttu-id="42b58-126">결과 검토</span><span class="sxs-lookup"><span data-stu-id="42b58-126">Review results</span></span>

<span data-ttu-id="42b58-127">완료 되 면 hello 결과가 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="42b58-127">When complete, hello results are provided.</span></span> <span data-ttu-id="42b58-128">hello 다음 홉 IP 주소는 리소스의 hello 형식을 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="42b58-128">hello next hop IP address is returned as well as hello type of resource it is.</span></span>

```
data:    Next Hop Ip Address             : 10.0.1.2
info:    network watcher next-hop command OK
```

<span data-ttu-id="42b58-129">hello 다음 목록은 hello 현재 사용 가능한 NextHopType 값.</span><span class="sxs-lookup"><span data-stu-id="42b58-129">hello following list shows hello currently available NextHopType values:</span></span>

<span data-ttu-id="42b58-130">**다음 홉 유형**</span><span class="sxs-lookup"><span data-stu-id="42b58-130">**Next Hop Type**</span></span>

* <span data-ttu-id="42b58-131">인터넷</span><span class="sxs-lookup"><span data-stu-id="42b58-131">Internet</span></span>
* <span data-ttu-id="42b58-132">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="42b58-132">VirtualAppliance</span></span>
* <span data-ttu-id="42b58-133">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="42b58-133">VirtualNetworkGateway</span></span>
* <span data-ttu-id="42b58-134">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="42b58-134">VnetLocal</span></span>
* <span data-ttu-id="42b58-135">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="42b58-135">HyperNetGateway</span></span>
* <span data-ttu-id="42b58-136">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="42b58-136">VnetPeering</span></span>
* <span data-ttu-id="42b58-137">없음</span><span class="sxs-lookup"><span data-stu-id="42b58-137">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="42b58-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="42b58-138">Next steps</span></span>

<span data-ttu-id="42b58-139">자세한 내용은 방법 tooreview 방문 하 여 프로그래밍 방식으로 네트워크 보안 그룹 설정을 [NSG 감사 네트워크 감시자를](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="42b58-139">Learn how tooreview your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>
