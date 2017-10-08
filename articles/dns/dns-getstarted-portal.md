---
title: "hello Azure 포털을 사용 하 여 Azure DNS aaaGet 시작 | Microsoft Docs"
description: "자세한 내용은 방법 toocreate DNS 영역 및 Azure DNS에 레코드입니다. 단계별 가이드 toocreate 이며 첫 번째 DNS 영역 및 hello Azure 포털을 사용 하 여 레코드를 관리 합니다."
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 5cea01d840d794001cccac64defed8b329d948db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-hello-azure-portal"></a><span data-ttu-id="55405-104">Azure DNS hello Azure 포털을 사용 하 여 시작</span><span class="sxs-lookup"><span data-stu-id="55405-104">Get started with Azure DNS using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="55405-105">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="55405-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="55405-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="55405-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="55405-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="55405-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="55405-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="55405-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="55405-109">이 문서 안내 hello 단계 toocreate 첫 번째 DNS 영역과 hello Azure 포털을 사용 하 여 레코드.</span><span class="sxs-lookup"><span data-stu-id="55405-109">This article walks you through hello steps toocreate your first DNS zone and record using hello Azure portal.</span></span> <span data-ttu-id="55405-110">Azure PowerShell을 사용 하 여 이러한 단계를 수행 하거나 플랫폼 간 Azure CLI hello 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55405-110">You can also perform these steps using Azure PowerShell or hello cross-platform Azure CLI.</span></span>

<span data-ttu-id="55405-111">DNS 영역에는 특정 도메인에 대 한 사용 되는 toohost hello DNS 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="55405-111">A DNS zone is used toohost hello DNS records for a particular domain.</span></span> <span data-ttu-id="55405-112">Azure DNS에서 도메인 호스팅 toostart toocreate DNS 영역 해당 도메인 이름을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55405-112">toostart hosting your domain in Azure DNS, you need toocreate a DNS zone for that domain name.</span></span> <span data-ttu-id="55405-113">그러면 이 DNS 영역 안에 도메인의 각 DNS 레코드가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="55405-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="55405-114">마지막으로, toopublish DNS 영역 toohello 인터넷 tooconfigure hello 이름 서버 hello 도메인에 대 한 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="55405-114">Finally, toopublish your DNS zone toohello Internet, you need tooconfigure hello name servers for hello domain.</span></span> <span data-ttu-id="55405-115">이러한 각 단계는 단계를 수행 하는 hello에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55405-115">Each of these steps is described in hello following steps.</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="55405-116">DNS 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="55405-116">Create a DNS zone</span></span>

1. <span data-ttu-id="55405-117">Azure 포털 toohello에 로그인</span><span class="sxs-lookup"><span data-stu-id="55405-117">Sign in toohello Azure portal</span></span>
2. <span data-ttu-id="55405-118">Hello 허브 메뉴에서를 클릭 하 고 클릭 **새로 만들기 > 네트워킹 >** 클릭 하 고 **DNS 영역** tooopen hello 만들 DNS 영역 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="55405-118">On hello Hub menu, click and click **New > Networking >** and then click **DNS zone** tooopen hello Create DNS zone blade.</span></span>

    ![DNS 영역](./media/dns-getstarted-portal/openzone650.png)

4. <span data-ttu-id="55405-120">Hello에 **만들 DNS 영역** 블레이드 hello 다음 값을 입력 한 다음 클릭 **만들기**:</span><span class="sxs-lookup"><span data-stu-id="55405-120">On hello **Create DNS zone** blade enter hello following values, then click **Create**:</span></span>


   | <span data-ttu-id="55405-121">**설정**</span><span class="sxs-lookup"><span data-stu-id="55405-121">**Setting**</span></span> | <span data-ttu-id="55405-122">**값**</span><span class="sxs-lookup"><span data-stu-id="55405-122">**Value**</span></span> | <span data-ttu-id="55405-123">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="55405-123">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="55405-124">**Name**</span><span class="sxs-lookup"><span data-stu-id="55405-124">**Name**</span></span>|<span data-ttu-id="55405-125">contoso.com</span><span class="sxs-lookup"><span data-stu-id="55405-125">contoso.com</span></span>|<span data-ttu-id="55405-126">hello hello DNS 영역 이름</span><span class="sxs-lookup"><span data-stu-id="55405-126">hello name of hello DNS zone</span></span>|
   |<span data-ttu-id="55405-127">**구독**</span><span class="sxs-lookup"><span data-stu-id="55405-127">**Subscription**</span></span>|<span data-ttu-id="55405-128">[구독 이름]</span><span class="sxs-lookup"><span data-stu-id="55405-128">[Your subscription]</span></span>|<span data-ttu-id="55405-129">구독 toocreate hello DNS 영역을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="55405-129">Select a subscription toocreate hello DNS zone in.</span></span>|
   |<span data-ttu-id="55405-130">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="55405-130">**Resource group**</span></span>|<span data-ttu-id="55405-131">**새로 만들기:** contosoDNSRG</span><span class="sxs-lookup"><span data-stu-id="55405-131">**Create new:** contosoDNSRG</span></span>|<span data-ttu-id="55405-132">리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55405-132">Create a resource group.</span></span> <span data-ttu-id="55405-133">hello 리소스 그룹 이름은 선택한 hello 구독 내에서 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55405-133">hello resource group name must be unique within hello subscription you selected.</span></span> <span data-ttu-id="55405-134">리소스 그룹을 읽기 hello에 대 한 자세한 toolearn [리소스 관리자](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) 개요 문서.</span><span class="sxs-lookup"><span data-stu-id="55405-134">toolearn more about resource groups, read hello [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="55405-135">**위치**:</span><span class="sxs-lookup"><span data-stu-id="55405-135">**Location**</span></span>|<span data-ttu-id="55405-136">미국 서부</span><span class="sxs-lookup"><span data-stu-id="55405-136">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="55405-137">hello 리소스 그룹 hello 리소스 그룹의 toohello 위치 참조 되었으며 hello DNS 영역에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="55405-137">hello resource group refers toohello location of hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="55405-138">hello DNS 영역의 위치는 항상 "전역" 하 고 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="55405-138">hello DNS zone location is always "global", and is not shown.</span></span>

## <a name="create-a-dns-record"></a><span data-ttu-id="55405-139">DNS 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="55405-139">Create a DNS record</span></span>

<span data-ttu-id="55405-140">hello 다음 예에서는 과정을 보여 줍니다 hello 새 'A' 레코드를 만드는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="55405-140">hello following example walks you through hello process of creating new 'A' record.</span></span> <span data-ttu-id="55405-141">다른 레코드 종류 및 toomodify 기존 레코드에 대 한 참조 [관리 DNS 레코드 및 레코드 집합 사용 하 여 Azure 포털 hello](dns-operations-recordsets-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="55405-141">For other record types and toomodify existing records, see [Manage DNS records and record sets by using hello Azure portal](dns-operations-recordsets-portal.md).</span></span> 

1. <span data-ttu-id="55405-142">Hello로 DNS 영역에서에서 만든 hello Azure 포털 **즐겨찾기** 창에서 클릭 **모든 리소스**합니다.</span><span class="sxs-lookup"><span data-stu-id="55405-142">With hello DNS Zone created, in hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="55405-143">Hello 클릭 **contoso.com** 모든 리소스 블레이드 hello에 DNS 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="55405-143">Click hello **contoso.com** DNS zone in hello All resources blade.</span></span> <span data-ttu-id="55405-144">이미 선택한 hello 구독에 여러 자원이 인 경우 입력 하면 **contoso.com** hello에 **이름별으로 필터링...**</span><span class="sxs-lookup"><span data-stu-id="55405-144">If hello subscription you selected already has several resources in it, you can enter **contoso.com** in hello **Filter by name…**</span></span> <span data-ttu-id="55405-145">상자 tooeasily hello DNS 영역에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="55405-145">box tooeasily access hello DNS Zone.</span></span>

1. <span data-ttu-id="55405-146">Hello의 hello 위쪽 **DNS 영역** 블레이드를 **집합을 기록해 +** tooopen hello **레코드 집합을 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="55405-146">At hello top of hello **DNS zone** blade, select **+ Record set** tooopen hello **Add record set** blade.</span></span>

1. <span data-ttu-id="55405-147">Hello에 **레코드 집합을 추가** 블레이드에서 hello 다음 값을 입력 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="55405-147">On hello **Add record set** blade, enter hello following values, and click **OK**.</span></span> <span data-ttu-id="55405-148">이 예에서는 A 레코드를 만들 것입니다.</span><span class="sxs-lookup"><span data-stu-id="55405-148">In this example, you are creating an A record.</span></span>

   |<span data-ttu-id="55405-149">**설정**</span><span class="sxs-lookup"><span data-stu-id="55405-149">**Setting**</span></span> | <span data-ttu-id="55405-150">**값**</span><span class="sxs-lookup"><span data-stu-id="55405-150">**Value**</span></span> | <span data-ttu-id="55405-151">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="55405-151">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="55405-152">**Name**</span><span class="sxs-lookup"><span data-stu-id="55405-152">**Name**</span></span>|<span data-ttu-id="55405-153">www</span><span class="sxs-lookup"><span data-stu-id="55405-153">www</span></span>|<span data-ttu-id="55405-154">Hello 레코드의 이름</span><span class="sxs-lookup"><span data-stu-id="55405-154">Name of hello record</span></span>|
   |<span data-ttu-id="55405-155">**형식**</span><span class="sxs-lookup"><span data-stu-id="55405-155">**Type**</span></span>|<span data-ttu-id="55405-156">A</span><span class="sxs-lookup"><span data-stu-id="55405-156">A</span></span>| <span data-ttu-id="55405-157">유형 DNS 레코드 toocreate의 허용 되는 값은 A, AAAA, CNAME, MX, NS, SRV, TXT, 및 PTR입니다.</span><span class="sxs-lookup"><span data-stu-id="55405-157">Type of DNS record toocreate, acceptable values are A, AAAA, CNAME, MX, NS, SRV, TXT, and PTR.</span></span>  <span data-ttu-id="55405-158">레코드 유형에 대한 자세한 내용은 [DNS 영역 및 레코드 개요](dns-zones-records.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55405-158">For more information about record types, visit [Overview of DNS zones and records](dns-zones-records.md)</span></span>|
   |<span data-ttu-id="55405-159">**TTL**</span><span class="sxs-lookup"><span data-stu-id="55405-159">**TTL**</span></span>|<span data-ttu-id="55405-160">1</span><span class="sxs-lookup"><span data-stu-id="55405-160">1</span></span>|<span data-ttu-id="55405-161">-Time-to-live hello DNS 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="55405-161">Time-to-live of hello DNS request.</span></span>|
   |<span data-ttu-id="55405-162">**TTL 단위**</span><span class="sxs-lookup"><span data-stu-id="55405-162">**TTL unit**</span></span>|<span data-ttu-id="55405-163">시간</span><span class="sxs-lookup"><span data-stu-id="55405-163">Hours</span></span>|<span data-ttu-id="55405-164">TTL 값에 대한 시간 측정입니다.</span><span class="sxs-lookup"><span data-stu-id="55405-164">Measurement of time for TTL value.</span></span>|
   |<span data-ttu-id="55405-165">**IP 주소**</span><span class="sxs-lookup"><span data-stu-id="55405-165">**IP address**</span></span>|<span data-ttu-id="55405-166">ipAddressValue</span><span class="sxs-lookup"><span data-stu-id="55405-166">ipAddressValue</span></span>| <span data-ttu-id="55405-167">이 값은 hello DNS 레코드를 해결 하는 hello IP 주소.</span><span class="sxs-lookup"><span data-stu-id="55405-167">This value is hello IP address that hello DNS record resolves.</span></span>|

## <a name="view-records"></a><span data-ttu-id="55405-168">레코드 보기</span><span class="sxs-lookup"><span data-stu-id="55405-168">View records</span></span>

<span data-ttu-id="55405-169">Hello hello DNS 영역 블레이드의 아래 부분을 hello DNS 영역에 대 한 hello 레코드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55405-169">In hello lower part of hello DNS zone blade, you can see hello records for hello DNS zone.</span></span> <span data-ttu-id="55405-170">Hello 기본 DNS 및 SOA 레코드를 모든 영역에 만들어지는 플러스 만든 새 레코드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55405-170">You should see hello default DNS and SOA records, which are created in every zone, plus any new records you have created.</span></span>

![영역](./media/dns-getstarted-portal/viewzone500.png)


## <a name="update-name-servers"></a><span data-ttu-id="55405-172">이름 서버 업데이트</span><span class="sxs-lookup"><span data-stu-id="55405-172">Update name servers</span></span>

<span data-ttu-id="55405-173">일단 시작 되 면 DNS 영역과 레코드는 올바르게 설정 되었는지, tooconfigure 필요한 충족 도메인 이름 toouse hello Azure DNS 이름 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="55405-173">Once you are satisfied that your DNS zone and records have been set up correctly, you need tooconfigure your domain name toouse hello Azure DNS name servers.</span></span> <span data-ttu-id="55405-174">이렇게 하면 다른 사용자 hello 인터넷 toofind에 DNS 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="55405-174">This enables other users on hello Internet toofind your DNS records.</span></span>

<span data-ttu-id="55405-175">영역에 대 한 이름 서버 hello hello Azure 포털에서에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="55405-175">hello name servers for your zone are given in hello Azure portal:</span></span>

![영역](./media/dns-getstarted-portal/viewzonens500.png)

<span data-ttu-id="55405-177">이러한 이름 서버 hello 도메인 이름 등록 기관 (여기서 구입한 hello 도메인 이름)으로 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55405-177">These name servers should be configured with hello domain name registrar (where you purchased hello domain name).</span></span> <span data-ttu-id="55405-178">등록 자가 hello 옵션 tooset hello 도메인에 대 한 hello 이름 서버를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="55405-178">Your registrar offers hello option tooset up hello name servers for hello domain.</span></span> <span data-ttu-id="55405-179">자세한 내용은 참조 [사용자 도메인 tooAzure DNS 위임](dns-domain-delegation.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="55405-179">For more information, see [Delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="55405-180">모든 리소스 삭제</span><span class="sxs-lookup"><span data-stu-id="55405-180">Delete all resources</span></span>

<span data-ttu-id="55405-181">이 문서에서는 다음 단계 완료 hello에서에서 만든 모든 리소스를 toodelete:</span><span class="sxs-lookup"><span data-stu-id="55405-181">toodelete all resources created in this article, complete hello following steps:</span></span>

1. <span data-ttu-id="55405-182">Hello Azure 포털에서에서 **즐겨찾기** 창에서 클릭 **모든 리소스**합니다.</span><span class="sxs-lookup"><span data-stu-id="55405-182">In hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="55405-183">Hello 클릭 **MyResourceGroup** 리소스 그룹 hello에서 모든 리소스 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="55405-183">Click hello **MyResourceGroup** resource group in hello All resources blade.</span></span> <span data-ttu-id="55405-184">이미 선택한 hello 구독에 여러 자원이 인 경우 입력 하면 **MyResourceGroup** hello에 **이름별으로 필터링...**</span><span class="sxs-lookup"><span data-stu-id="55405-184">If hello subscription you selected already has several resources in it, you can enter **MyResourceGroup** in hello **Filter by name…**</span></span> <span data-ttu-id="55405-185">상자 tooeasily 액세스 hello 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="55405-185">box tooeasily access hello resource group.</span></span>
1. <span data-ttu-id="55405-186">Hello에 **MyResourceGroup** 블레이드에서 hello 클릭 **삭제** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="55405-186">In hello **MyResourceGroup** blade, click hello **Delete** button.</span></span>
1. <span data-ttu-id="55405-187">hello 포털 해야 tootype hello 이름의 hello 리소스 그룹 tooconfirm toodelete 원하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="55405-187">hello portal requires you tootype hello name of hello resource group tooconfirm that you want toodelete it.</span></span> <span data-ttu-id="55405-188">클릭 **삭제**, 형식 *MyResourceGroup* hello 리소스 그룹 이름에 대 한 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="55405-188">Click **Delete**, Type *MyResourceGroup* for hello resource group name, then click **Delete**.</span></span> <span data-ttu-id="55405-189">리소스 그룹을 삭제 hello 리소스 그룹 내에서 모든 리소스에 있으므로 항상 있는지 tooconfirm 리소스 그룹의 hello 내용을 삭제 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="55405-189">Deleting a resource group deletes all resources within hello resource group, so always be sure tooconfirm hello contents of a resource group before deleting it.</span></span> <span data-ttu-id="55405-190">hello 포털 hello 리소스 그룹 내에 포함 된 모든 리소스를 삭제 한 다음 자체 hello 리소스 그룹을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="55405-190">hello portal deletes all resources contained within hello resource group, then deletes hello resource group itself.</span></span> <span data-ttu-id="55405-191">이 프로세스는 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="55405-191">This process takes several minutes.</span></span>


## <a name="next-steps"></a><span data-ttu-id="55405-192">다음 단계</span><span class="sxs-lookup"><span data-stu-id="55405-192">Next steps</span></span>

<span data-ttu-id="55405-193">Azure DNS에 대해 자세히 toolearn 참조 [Azure DNS 개요](dns-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="55405-193">toolearn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="55405-194">Azure DNS에 DNS 레코드를 관리에 대해 자세히 toolearn 참조 [관리 DNS 레코드 및 레코드 집합 사용 하 여 Azure 포털 hello](dns-operations-recordsets-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="55405-194">toolearn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets by using hello Azure portal](dns-operations-recordsets-portal.md).</span></span>

