---
title: "Azure Network Watcher Next Hop을 사용하여 다음 홉 찾기 - Azure CLI 2.0 | Microsoft Docs"
description: "이 문서에서는 Azure CLI에서 다음 홉을 사용하여 다음 홉 유형 및 IP 주소를 찾을 수 있는 방법을 설명합니다."
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
ms.openlocfilehash: d1ee6870ba0188ff2c473e4cca12a5bdc1f97d3d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="7ca02-103">Azure CLI 2.0을 사용하는 Azure Network Watcher에서 Next Hop 기능을 사용하는 다음 홉이 무엇인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7ca02-103">Find out what the next hop type is using the Next Hop capability in Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="7ca02-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="7ca02-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="7ca02-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7ca02-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="7ca02-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="7ca02-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="7ca02-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="7ca02-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="7ca02-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="7ca02-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="7ca02-109">Next Hop은 Network Watcher의 기능으로 지정된 가상 컴퓨터를 기반으로 하는 다음 홉 유형 및 IP 주소를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ca02-109">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="7ca02-110">이 기능은 가상 컴퓨터에서 나가는 트래픽이 게이트웨이, 인터넷 또는 가상 네트워크를 트래버스하여 대상에 도달할지 여부를 결정하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="7ca02-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

<span data-ttu-id="7ca02-111">이 문서에서는 Windows, Mac 및 Linux에서 사용할 수 있는 리소스 관리 배포 모델용 차세대 CLI인 Azure CLI 2.0을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7ca02-111">This article uses our next generation CLI for the resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="7ca02-112">이 문서의 단계를 수행하려면 [Mac, Linux 및 Windows용 Azure 명령줄 인터페이스(Azure CLI)를 설치](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ca02-112">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7ca02-113">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="7ca02-113">Before you begin</span></span>

<span data-ttu-id="7ca02-114">이 시나리오에서는 Azure CLI를 사용하여 다음 홉 유형 및 IP 주소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7ca02-114">In this scenario, you will use the Azure CLI to find the next hop type and IP address.</span></span>

<span data-ttu-id="7ca02-115">이 시나리오에서는 사용자가 Network Watcher를 만드는 [Network Watcher 만들기](network-watcher-create.md)의 단계를 이미 수행했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ca02-115">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="7ca02-116">또한 시나리오에서는 유효한 가상 컴퓨터를 포함한 리소스 그룹을 사용할 수 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ca02-116">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="7ca02-117">시나리오</span><span class="sxs-lookup"><span data-stu-id="7ca02-117">Scenario</span></span>

<span data-ttu-id="7ca02-118">이 문서에서 다루는 시나리오는 리소스에 대한 다음 홉 유형 및 IP 주소를 찾는 Network Watcher의 기능인 Next Hop을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7ca02-118">The scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="7ca02-119">Next Hop에 대한 자세한 내용을 보려면 [Next Hop 개요](network-watcher-next-hop-overview.md)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="7ca02-119">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>


## <a name="get-next-hop"></a><span data-ttu-id="7ca02-120">다음 홉 가져오기</span><span class="sxs-lookup"><span data-stu-id="7ca02-120">Get Next Hop</span></span>

<span data-ttu-id="7ca02-121">다음 홉을 가져오려면 `az network watcher show-next-hop` cmdlet을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="7ca02-121">To get the next hop we call the `az network watcher show-next-hop` cmdlet.</span></span> <span data-ttu-id="7ca02-122">cmdlet을 Network Watcher 리소스 그룹, NetworkWatcher, 가상 컴퓨터 ID, 원본 IP 주소 및 대상 IP 주소에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="7ca02-122">We pass the cmdlet the Network Watcher resource group, the NetworkWatcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="7ca02-123">이 예제에서 대상 IP 주소는 다른 가상 네트워크의 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="7ca02-123">In this example, the destination IP address is to a VM in another virtual network.</span></span> <span data-ttu-id="7ca02-124">두 개의 가상 네트워크 간에 가상 네트워크 게이트웨이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ca02-124">There is a virtual network gateway between the two virtual networks.</span></span>

<span data-ttu-id="7ca02-125">아직 설치하지 않은 경우 최신 [Azure CLI 2.0](/cli/azure/install-az-cli2)을 설치 및 구성하고 [az login](/cli/azure/#login)을 사용하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7ca02-125">If you haven't yet, install and configure the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="7ca02-126">그런 후 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7ca02-126">Then run the following command:</span></span>

```azurecli
az network watcher show-next-hop --resource-group <resourcegroupName> --vm <vmNameorID> --source-ip <source-ip> --dest-ip <destination-ip>

```

> [!NOTE]
<span data-ttu-id="7ca02-127">VM에 여러 NIC가 있고 NIC에 IP를 전달할 수 있는 경우 NIC 매개 변수(-i nic-id)를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ca02-127">If the VM has multiple NICs and IP forwarding is enabled on any of the NICs, then the NIC parameter (-i nic-id) must be specified.</span></span> <span data-ttu-id="7ca02-128">그렇지 않은 경우 선택적입니다.</span><span class="sxs-lookup"><span data-stu-id="7ca02-128">Otherwise it is optional.</span></span>

## <a name="review-results"></a><span data-ttu-id="7ca02-129">결과 검토</span><span class="sxs-lookup"><span data-stu-id="7ca02-129">Review results</span></span>

<span data-ttu-id="7ca02-130">완료되면 결과가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ca02-130">When complete, the results are provided.</span></span> <span data-ttu-id="7ca02-131">리소스의 유형뿐만 아니라 다음 홉 IP 주소가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ca02-131">The next hop IP address is returned as well as the type of resource it is.</span></span>

```azurecli
{
    "nextHopIpAddress": null,
    "nextHopType": "Internet",
    "routeTableId": "System Route"
}
```

<span data-ttu-id="7ca02-132">다음 목록에서는 현재 사용할 수 있는 NextHopType 값을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7ca02-132">The following list shows the currently available NextHopType values:</span></span>

<span data-ttu-id="7ca02-133">**다음 홉 유형**</span><span class="sxs-lookup"><span data-stu-id="7ca02-133">**Next Hop Type**</span></span>

* <span data-ttu-id="7ca02-134">인터넷</span><span class="sxs-lookup"><span data-stu-id="7ca02-134">Internet</span></span>
* <span data-ttu-id="7ca02-135">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="7ca02-135">VirtualAppliance</span></span>
* <span data-ttu-id="7ca02-136">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="7ca02-136">VirtualNetworkGateway</span></span>
* <span data-ttu-id="7ca02-137">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="7ca02-137">VnetLocal</span></span>
* <span data-ttu-id="7ca02-138">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="7ca02-138">HyperNetGateway</span></span>
* <span data-ttu-id="7ca02-139">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="7ca02-139">VnetPeering</span></span>
* <span data-ttu-id="7ca02-140">없음</span><span class="sxs-lookup"><span data-stu-id="7ca02-140">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ca02-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7ca02-141">Next steps</span></span>

<span data-ttu-id="7ca02-142">[Network Watcher를 사용하여 NSG 감사](network-watcher-nsg-auditing-powershell.md)를 방문하여 네트워크 보안 그룹 설정을 프로그래밍 방식으로 검토하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7ca02-142">Learn how to review your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>
