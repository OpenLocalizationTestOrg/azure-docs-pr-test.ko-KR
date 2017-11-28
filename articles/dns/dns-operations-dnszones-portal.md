---
title: "Azure DNS-Azure 포털에서에서 aaaManage DNS 영역 | Microsoft Docs"
description: "Hello Azure 포털을 사용 하 여 DNS 영역을 관리할 수 있습니다. 이 문서에서는 tooupdate, 삭제 하 고 dns를 Azure DNS 영역을 만드는 방법을 설명합니다"
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
ms.openlocfilehash: 0d8ce302bb7126dfe8077a6f3e33418e16fcea64
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-hello-azure-portal"></a><span data-ttu-id="5458c-104">Toomanage DNS 영역에 Azure 포털을 hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="5458c-104">How toomanage DNS Zones in hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5458c-105">포털</span><span class="sxs-lookup"><span data-stu-id="5458c-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="5458c-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5458c-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="5458c-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="5458c-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="5458c-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5458c-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="5458c-109">이 문서에서는 어떻게 toomanage DNS 영역을 hello Azure 포털을 사용 하 여 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5458c-109">This article shows you how toomanage your DNS zones by using hello Azure portal.</span></span> <span data-ttu-id="5458c-110">플랫폼 간 hello를 사용 하 여 DNS 영역을 관리할 수 있습니다 [Azure CLI](dns-operations-dnszones-cli.md) Azure hello 또는 [PowerShell](dns-operations-dnszones.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5458c-110">You can also manage your DNS zones using hello cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or hello Azure [PowerShell](dns-operations-dnszones.md).</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="5458c-111">DNS 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="5458c-111">Create a DNS zone</span></span>

1. <span data-ttu-id="5458c-112">Azure 포털 toohello에 로그인</span><span class="sxs-lookup"><span data-stu-id="5458c-112">Sign in toohello Azure portal</span></span>
2. <span data-ttu-id="5458c-113">Hello 허브 메뉴에서를 클릭 하 고 클릭 **새로 만들기 > 네트워킹 >** 클릭 하 고 **DNS 영역** tooopen hello 만들 DNS 영역 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="5458c-113">On hello Hub menu, click and click **New > Networking >** and then click **DNS zone** tooopen hello Create DNS zone blade.</span></span>

    ![DNS 영역](./media/dns-operations-dnszones-portal/openzone650.png)

4. <span data-ttu-id="5458c-115">Hello에 **만들 DNS 영역** 블레이드 hello 다음 값을 입력 한 다음 클릭 **만들기**:</span><span class="sxs-lookup"><span data-stu-id="5458c-115">On hello **Create DNS zone** blade enter hello following values, then click **Create**:</span></span>


   | <span data-ttu-id="5458c-116">**설정**</span><span class="sxs-lookup"><span data-stu-id="5458c-116">**Setting**</span></span> | <span data-ttu-id="5458c-117">**값**</span><span class="sxs-lookup"><span data-stu-id="5458c-117">**Value**</span></span> | <span data-ttu-id="5458c-118">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="5458c-118">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="5458c-119">**Name**</span><span class="sxs-lookup"><span data-stu-id="5458c-119">**Name**</span></span>|<span data-ttu-id="5458c-120">contoso.com</span><span class="sxs-lookup"><span data-stu-id="5458c-120">contoso.com</span></span>|<span data-ttu-id="5458c-121">hello hello DNS 영역 이름</span><span class="sxs-lookup"><span data-stu-id="5458c-121">hello name of hello DNS zone</span></span>|
   |<span data-ttu-id="5458c-122">**구독**</span><span class="sxs-lookup"><span data-stu-id="5458c-122">**Subscription**</span></span>|<span data-ttu-id="5458c-123">[구독 이름]</span><span class="sxs-lookup"><span data-stu-id="5458c-123">[Your subscription]</span></span>|<span data-ttu-id="5458c-124">구독 toocreate hello DNS 영역을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5458c-124">Select a subscription toocreate hello DNS zone in.</span></span>|
   |<span data-ttu-id="5458c-125">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="5458c-125">**Resource group**</span></span>|<span data-ttu-id="5458c-126">**새로 만들기:** contosoDNSRG</span><span class="sxs-lookup"><span data-stu-id="5458c-126">**Create new:** contosoDNSRG</span></span>|<span data-ttu-id="5458c-127">리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5458c-127">Create a resource group.</span></span> <span data-ttu-id="5458c-128">hello 리소스 그룹 이름은 선택한 hello 구독 내에서 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5458c-128">hello resource group name must be unique within hello subscription you selected.</span></span> <span data-ttu-id="5458c-129">리소스 그룹을 읽기 hello에 대 한 자세한 toolearn [리소스 관리자](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) 개요 문서.</span><span class="sxs-lookup"><span data-stu-id="5458c-129">toolearn more about resource groups, read hello [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="5458c-130">**위치**:</span><span class="sxs-lookup"><span data-stu-id="5458c-130">**Location**</span></span>|<span data-ttu-id="5458c-131">미국 서부</span><span class="sxs-lookup"><span data-stu-id="5458c-131">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="5458c-132">hello 리소스 그룹 hello 리소스 그룹의 toohello 위치 참조 되었으며 hello DNS 영역에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5458c-132">hello resource group refers toohello location of hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="5458c-133">hello DNS 영역의 위치는 항상 "전역" 하 고 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5458c-133">hello DNS zone location is always "global", and is not shown.</span></span>

## <a name="list-dns-zones"></a><span data-ttu-id="5458c-134">DNS 영역 나열</span><span class="sxs-lookup"><span data-stu-id="5458c-134">List DNS zones</span></span>

<span data-ttu-id="5458c-135">Hello Azure 포털에서 탐색 너무**더 많은 서비스** > **네트워킹** > **DNS 영역**합니다.</span><span class="sxs-lookup"><span data-stu-id="5458c-135">In hello Azure portal, navigate too**More services** > **Networking** > **DNS zones**.</span></span> <span data-ttu-id="5458c-136">각 DNS 영역은 자체 리소스이며, 레코드 집합의 수 및 이름 서버와 같은 정보를 이 보기에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5458c-136">Each DNS zone is it's own resource, information such as number of record-sets and name servers are viewable from this view.</span></span> <span data-ttu-id="5458c-137">hello 열 **이름 서버** tooadd hello 기본 뷰에서 해당 클릭 되지 않습니다 **열**선택, **이름 서버** 클릭 **수행**합니다.</span><span class="sxs-lookup"><span data-stu-id="5458c-137">hello column **NAME SERVERS** is not in hello default view, tooadd it click **Columns**, select **Name servers** and click **Done**.</span></span>

![DNS 영역 나열](./media/dns-operations-dnszones-portal/listzones.png)

## <a name="delete-a-dns-zone"></a><span data-ttu-id="5458c-139">DNS 영역 삭제</span><span class="sxs-lookup"><span data-stu-id="5458c-139">Delete a DNS zone</span></span>

<span data-ttu-id="5458c-140">Hello 포털에서 tooa DNS 영역을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5458c-140">Navigate tooa DNS zone in hello portal.</span></span> <span data-ttu-id="5458c-141">Hello에 **DNS 영역** 블레이드에서 클릭 **영역 삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="5458c-141">On hello **DNS zone** blade, click **Delete zone**.</span></span> <span data-ttu-id="5458c-142">입력 정보 요청된 tooconfirm toodelete hello DNS 영역 부호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5458c-142">You are prompted tooconfirm you are wanting toodelete hello DNS zone.</span></span> <span data-ttu-id="5458c-143">DNS 영역을 삭제 하면 hello 영역에 포함 된 모든 hello 레코드 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="5458c-143">Deleting a DNS zone also deletes all hello records that are contained in hello zone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5458c-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5458c-144">Next steps</span></span>

<span data-ttu-id="5458c-145">자세한 방법을 프로그램 DNS 영역 및 레코드를 방문 하 여 toowork [hello Azure 포털을 사용 하 여 Azure DNS 시작](dns-getstarted-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5458c-145">Learn how toowork with your DNS Zone and records by visiting [Get started with Azure DNS using hello Azure portal](dns-getstarted-portal.md).</span></span>
