---
title: "Azure DNS에서 DNS 영역 관리 - Azure Portal | Microsoft Docs"
description: "Azure Portal을 사용하여 DNS 영역을 관리할 수 있습니다. 이 문서에서는 Azure DNS에서 DNS 영역을 업데이트, 삭제 및 만드는 방법을 설명합니다."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/18/2017
ms.author: gwallace
ms.openlocfilehash: 69a509612e6204fc93dd42bf2fe69cb165b5777c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-dns-zones-in-the-azure-portal"></a><span data-ttu-id="1c555-104">Azure Portal에서 DNS 영역을 관리하는 방법</span><span class="sxs-lookup"><span data-stu-id="1c555-104">How to manage DNS Zones in the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1c555-105">포털</span><span class="sxs-lookup"><span data-stu-id="1c555-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="1c555-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1c555-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="1c555-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1c555-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="1c555-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1c555-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="1c555-109">이 문서는 Azure Portal을 사용하여 DNS 영역을 관리하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="1c555-109">This article shows you how to manage your DNS zones by using the Azure portal.</span></span> <span data-ttu-id="1c555-110">플랫폼 간 [Azure CLI](dns-operations-dnszones-cli.md) 또는 Azure [PowerShell](dns-operations-dnszones.md)을 사용하여 DNS 영역을 관리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c555-110">You can also manage your DNS zones using the cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or the Azure [PowerShell](dns-operations-dnszones.md).</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="1c555-111">DNS 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="1c555-111">Create a DNS zone</span></span>

1. <span data-ttu-id="1c555-112">Azure 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1c555-112">Sign in to the Azure portal</span></span>
2. <span data-ttu-id="1c555-113">허브 메뉴에서 **새로 만들기 > 네트워킹 >**을 클릭한 다음 **DNS 영역**을 클릭하여 DNS 영역 블레이드 만들기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1c555-113">On the Hub menu, click and click **New > Networking >** and then click **DNS zone** to open the Create DNS zone blade.</span></span>

    ![DNS 영역](./media/dns-operations-dnszones-portal/openzone650.png)

4. <span data-ttu-id="1c555-115">**DNS 영역 만들기** 블레이드에서 다음 값을 입력한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c555-115">On the **Create DNS zone** blade enter the following values, then click **Create**:</span></span>


   | <span data-ttu-id="1c555-116">**설정**</span><span class="sxs-lookup"><span data-stu-id="1c555-116">**Setting**</span></span> | <span data-ttu-id="1c555-117">**값**</span><span class="sxs-lookup"><span data-stu-id="1c555-117">**Value**</span></span> | <span data-ttu-id="1c555-118">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="1c555-118">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="1c555-119">**Name**</span><span class="sxs-lookup"><span data-stu-id="1c555-119">**Name**</span></span>|<span data-ttu-id="1c555-120">contoso.com</span><span class="sxs-lookup"><span data-stu-id="1c555-120">contoso.com</span></span>|<span data-ttu-id="1c555-121">DNS 영역의 이름</span><span class="sxs-lookup"><span data-stu-id="1c555-121">The name of the DNS zone</span></span>|
   |<span data-ttu-id="1c555-122">**구독**</span><span class="sxs-lookup"><span data-stu-id="1c555-122">**Subscription**</span></span>|<span data-ttu-id="1c555-123">[구독 이름]</span><span class="sxs-lookup"><span data-stu-id="1c555-123">[Your subscription]</span></span>|<span data-ttu-id="1c555-124">DNS 영역을 만들 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1c555-124">Select a subscription to create the DNS zone in.</span></span>|
   |<span data-ttu-id="1c555-125">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="1c555-125">**Resource group**</span></span>|<span data-ttu-id="1c555-126">**새로 만들기:** contosoDNSRG</span><span class="sxs-lookup"><span data-stu-id="1c555-126">**Create new:** contosoDNSRG</span></span>|<span data-ttu-id="1c555-127">리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1c555-127">Create a resource group.</span></span> <span data-ttu-id="1c555-128">리소스 그룹 이름은 선택한 구독 내에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c555-128">The resource group name must be unique within the subscription you selected.</span></span> <span data-ttu-id="1c555-129">리소스 그룹에 대해 자세히 알아보려면 [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) 개요 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1c555-129">To learn more about resource groups, read the [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="1c555-130">**위치**:</span><span class="sxs-lookup"><span data-stu-id="1c555-130">**Location**</span></span>|<span data-ttu-id="1c555-131">미국 서부</span><span class="sxs-lookup"><span data-stu-id="1c555-131">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="1c555-132">리소스 그룹은 리소스 그룹의 위치를 나타내며 DNS 영역에 영향을 미치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1c555-132">The resource group refers to the location of the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="1c555-133">DNS 영역 위치는 항상 "전역"이며 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1c555-133">The DNS zone location is always "global", and is not shown.</span></span>

## <a name="list-dns-zones"></a><span data-ttu-id="1c555-134">DNS 영역 나열</span><span class="sxs-lookup"><span data-stu-id="1c555-134">List DNS zones</span></span>

<span data-ttu-id="1c555-135">Azure Portal에서 **더 많은 서비스** > **네트워킹** > **DNS 영역**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1c555-135">In the Azure portal, navigate to **More services** > **Networking** > **DNS zones**.</span></span> <span data-ttu-id="1c555-136">각 DNS 영역은 자체 리소스이며, 레코드 집합의 수 및 이름 서버와 같은 정보를 이 보기에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c555-136">Each DNS zone is it's own resource, information such as number of record-sets and name servers are viewable from this view.</span></span> <span data-ttu-id="1c555-137">**이름 서버** 열은 기본 보기에 표시되지 않으며, 이를 추가하려면 **열**을 클릭하고 **이름 서버**를 선택한 후 **완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c555-137">The column **NAME SERVERS** is not in the default view, to add it click **Columns**, select **Name servers** and click **Done**.</span></span>

![DNS 영역 나열](./media/dns-operations-dnszones-portal/listzones.png)

## <a name="delete-a-dns-zone"></a><span data-ttu-id="1c555-139">DNS 영역 삭제</span><span class="sxs-lookup"><span data-stu-id="1c555-139">Delete a DNS zone</span></span>

<span data-ttu-id="1c555-140">포털에서 DNS 영역으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1c555-140">Navigate to a DNS zone in the portal.</span></span> <span data-ttu-id="1c555-141">**DNS 영역** 블레이드에서 **영역 삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1c555-141">On the **DNS zone** blade, click **Delete zone**.</span></span> <span data-ttu-id="1c555-142">DNS 영역을 삭제할지 확인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c555-142">You are prompted to confirm you are wanting to delete the DNS zone.</span></span> <span data-ttu-id="1c555-143">DNS 영역을 삭제하면 해당 영역에 포함된 모든 레코드도 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c555-143">Deleting a DNS zone also deletes all the records that are contained in the zone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c555-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1c555-144">Next steps</span></span>

<span data-ttu-id="1c555-145">[Azure Portal을 사용하여 Azure DNS 시작](dns-getstarted-portal.md)을 방문하여 DNS 영역 및 레코드 사용 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1c555-145">Learn how to work with your DNS Zone and records by visiting [Get started with Azure DNS using the Azure portal](dns-getstarted-portal.md).</span></span>