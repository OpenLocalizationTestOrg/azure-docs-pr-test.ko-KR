---
title: "Azure Portal을 사용하여 Azure DNS 시작 | Microsoft Docs"
description: "Azure DNS에 DNS 영역 및 레코드를 만드는 방법을 알아봅니다. Azure Portal을 사용하여 첫 번째 DNS 영역 및 레코드를 만들고 관리하는 단계별 가이드입니다."
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
ms.openlocfilehash: 93b24e3d9fbb3fbb3ea995271fd63d1e82eb9c9e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-dns-using-the-azure-portal"></a><span data-ttu-id="bff10-104">Azure Portal을 사용하여 Azure DNS 시작</span><span class="sxs-lookup"><span data-stu-id="bff10-104">Get started with Azure DNS using the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="bff10-105">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="bff10-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="bff10-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bff10-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="bff10-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="bff10-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="bff10-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="bff10-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="bff10-109">이 문서에서는 Azure Portal을 사용하여 DNS 영역 및 레코드를 만드는 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-109">This article walks you through the steps to create your first DNS zone and record using the Azure portal.</span></span> <span data-ttu-id="bff10-110">Azure PowerShell 또는 플랫폼 간 Azure CLI를 사용하여 이러한 단계를 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-110">You can also perform these steps using Azure PowerShell or the cross-platform Azure CLI.</span></span>

<span data-ttu-id="bff10-111">DNS 영역은 특정 도메인에 대한 DNS 레코드를 호스트하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-111">A DNS zone is used to host the DNS records for a particular domain.</span></span> <span data-ttu-id="bff10-112">Azure DNS에서 도메인 호스팅을 시작하려면 해당 도메인 이름의 DNS 영역을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-112">To start hosting your domain in Azure DNS, you need to create a DNS zone for that domain name.</span></span> <span data-ttu-id="bff10-113">그러면 이 DNS 영역 안에 도메인의 각 DNS 레코드가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="bff10-114">마지막으로 DNS 영역을 인터넷에 게시하려면 도메인에 대한 이름 서버를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-114">Finally, to publish your DNS zone to the Internet, you need to configure the name servers for the domain.</span></span> <span data-ttu-id="bff10-115">각 단계는 다음 단계에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-115">Each of these steps is described in the following steps.</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="bff10-116">DNS 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="bff10-116">Create a DNS zone</span></span>

1. <span data-ttu-id="bff10-117">Azure 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-117">Sign in to the Azure portal</span></span>
2. <span data-ttu-id="bff10-118">허브 메뉴에서 **새로 만들기 > 네트워킹 >**을 클릭한 다음 **DNS 영역**을 클릭하여 DNS 영역 블레이드 만들기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-118">On the Hub menu, click and click **New > Networking >** and then click **DNS zone** to open the Create DNS zone blade.</span></span>

    ![DNS 영역](./media/dns-getstarted-portal/openzone650.png)

4. <span data-ttu-id="bff10-120">**DNS 영역 만들기** 블레이드에서 다음 값을 입력한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-120">On the **Create DNS zone** blade enter the following values, then click **Create**:</span></span>


   | <span data-ttu-id="bff10-121">**설정**</span><span class="sxs-lookup"><span data-stu-id="bff10-121">**Setting**</span></span> | <span data-ttu-id="bff10-122">**값**</span><span class="sxs-lookup"><span data-stu-id="bff10-122">**Value**</span></span> | <span data-ttu-id="bff10-123">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="bff10-123">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="bff10-124">**Name**</span><span class="sxs-lookup"><span data-stu-id="bff10-124">**Name**</span></span>|<span data-ttu-id="bff10-125">contoso.com</span><span class="sxs-lookup"><span data-stu-id="bff10-125">contoso.com</span></span>|<span data-ttu-id="bff10-126">DNS 영역의 이름</span><span class="sxs-lookup"><span data-stu-id="bff10-126">The name of the DNS zone</span></span>|
   |<span data-ttu-id="bff10-127">**구독**</span><span class="sxs-lookup"><span data-stu-id="bff10-127">**Subscription**</span></span>|<span data-ttu-id="bff10-128">[구독 이름]</span><span class="sxs-lookup"><span data-stu-id="bff10-128">[Your subscription]</span></span>|<span data-ttu-id="bff10-129">DNS 영역을 만들 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-129">Select a subscription to create the DNS zone in.</span></span>|
   |<span data-ttu-id="bff10-130">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="bff10-130">**Resource group**</span></span>|<span data-ttu-id="bff10-131">**새로 만들기:** contosoDNSRG</span><span class="sxs-lookup"><span data-stu-id="bff10-131">**Create new:** contosoDNSRG</span></span>|<span data-ttu-id="bff10-132">리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-132">Create a resource group.</span></span> <span data-ttu-id="bff10-133">리소스 그룹 이름은 선택한 구독 내에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-133">The resource group name must be unique within the subscription you selected.</span></span> <span data-ttu-id="bff10-134">리소스 그룹에 대해 자세히 알아보려면 [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) 개요 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bff10-134">To learn more about resource groups, read the [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="bff10-135">**위치**:</span><span class="sxs-lookup"><span data-stu-id="bff10-135">**Location**</span></span>|<span data-ttu-id="bff10-136">미국 서부</span><span class="sxs-lookup"><span data-stu-id="bff10-136">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="bff10-137">리소스 그룹은 리소스 그룹의 위치를 나타내며 DNS 영역에 영향을 미치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-137">The resource group refers to the location of the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="bff10-138">DNS 영역 위치는 항상 "전역"이며 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-138">The DNS zone location is always "global", and is not shown.</span></span>

## <a name="create-a-dns-record"></a><span data-ttu-id="bff10-139">DNS 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="bff10-139">Create a DNS record</span></span>

<span data-ttu-id="bff10-140">다음 예제에서는 새로운 'A' 레코드를 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-140">The following example walks you through the process of creating new 'A' record.</span></span> <span data-ttu-id="bff10-141">다른 레코드 유형을 알아보고 기존 레코드를 수정하려면 [Azure Portal을 사용하여 DNS 레코드 및 레코드 집합 관리](dns-operations-recordsets-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bff10-141">For other record types and to modify existing records, see [Manage DNS records and record sets by using the Azure portal](dns-operations-recordsets-portal.md).</span></span> 

1. <span data-ttu-id="bff10-142">DNS 영역을 만든 후 Azure Portal의 **즐겨찾기** 창에서 **모든 리소스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-142">With the DNS Zone created, in the Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="bff10-143">모든 리소스 블레이드에서 **contoso.com** DNS 영역을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-143">Click the **contoso.com** DNS zone in the All resources blade.</span></span> <span data-ttu-id="bff10-144">선택한 구독에 이미 여러 개의 리소스가 있는 경우 **이름을 기준으로 필터링...**에 **contoso.com**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-144">If the subscription you selected already has several resources in it, you can enter **contoso.com** in the **Filter by name…**</span></span> <span data-ttu-id="bff10-145">DNS 영역에 간편하게 액세스할 수 있는 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-145">box to easily access the DNS Zone.</span></span>

1. <span data-ttu-id="bff10-146">**DNS 영역** 블레이드의 위쪽에서 **+레코드 집합**을 클릭하여 **레코드 집합 추가** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-146">At the top of the **DNS zone** blade, select **+ Record set** to open the **Add record set** blade.</span></span>

1. <span data-ttu-id="bff10-147">**레코드 집합 추가** 블레이드에서 다음 값을 입력하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-147">On the **Add record set** blade, enter the following values, and click **OK**.</span></span> <span data-ttu-id="bff10-148">이 예에서는 A 레코드를 만들 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-148">In this example, you are creating an A record.</span></span>

   |<span data-ttu-id="bff10-149">**설정**</span><span class="sxs-lookup"><span data-stu-id="bff10-149">**Setting**</span></span> | <span data-ttu-id="bff10-150">**값**</span><span class="sxs-lookup"><span data-stu-id="bff10-150">**Value**</span></span> | <span data-ttu-id="bff10-151">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="bff10-151">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="bff10-152">**Name**</span><span class="sxs-lookup"><span data-stu-id="bff10-152">**Name**</span></span>|<span data-ttu-id="bff10-153">www</span><span class="sxs-lookup"><span data-stu-id="bff10-153">www</span></span>|<span data-ttu-id="bff10-154">레코드 이름</span><span class="sxs-lookup"><span data-stu-id="bff10-154">Name of the record</span></span>|
   |<span data-ttu-id="bff10-155">**형식**</span><span class="sxs-lookup"><span data-stu-id="bff10-155">**Type**</span></span>|<span data-ttu-id="bff10-156">A</span><span class="sxs-lookup"><span data-stu-id="bff10-156">A</span></span>| <span data-ttu-id="bff10-157">만들 DNS 레코드 유형, 사용할 수 있는 값은 A, AAAA, CNAME, MX, NS, SRV, TXT 및 PTR입니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-157">Type of DNS record to create, acceptable values are A, AAAA, CNAME, MX, NS, SRV, TXT, and PTR.</span></span>  <span data-ttu-id="bff10-158">레코드 유형에 대한 자세한 내용은 [DNS 영역 및 레코드 개요](dns-zones-records.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bff10-158">For more information about record types, visit [Overview of DNS zones and records](dns-zones-records.md)</span></span>|
   |<span data-ttu-id="bff10-159">**TTL**</span><span class="sxs-lookup"><span data-stu-id="bff10-159">**TTL**</span></span>|<span data-ttu-id="bff10-160">1</span><span class="sxs-lookup"><span data-stu-id="bff10-160">1</span></span>|<span data-ttu-id="bff10-161">DNS 요청의 Time-to-Live입니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-161">Time-to-live of the DNS request.</span></span>|
   |<span data-ttu-id="bff10-162">**TTL 단위**</span><span class="sxs-lookup"><span data-stu-id="bff10-162">**TTL unit**</span></span>|<span data-ttu-id="bff10-163">시간</span><span class="sxs-lookup"><span data-stu-id="bff10-163">Hours</span></span>|<span data-ttu-id="bff10-164">TTL 값에 대한 시간 측정입니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-164">Measurement of time for TTL value.</span></span>|
   |<span data-ttu-id="bff10-165">**IP 주소**</span><span class="sxs-lookup"><span data-stu-id="bff10-165">**IP address**</span></span>|<span data-ttu-id="bff10-166">ipAddressValue</span><span class="sxs-lookup"><span data-stu-id="bff10-166">ipAddressValue</span></span>| <span data-ttu-id="bff10-167">이 값은 DNS 레코드가 확인하는 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-167">This value is the IP address that the DNS record resolves.</span></span>|

## <a name="view-records"></a><span data-ttu-id="bff10-168">레코드 보기</span><span class="sxs-lookup"><span data-stu-id="bff10-168">View records</span></span>

<span data-ttu-id="bff10-169">DNS 영역 블레이드의 아래쪽에서 DNS 영역에 대한 레코드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-169">In the lower part of the DNS zone blade, you can see the records for the DNS zone.</span></span> <span data-ttu-id="bff10-170">모든 영역에 생성된 기본 DNS 및 SOA 레코드와 사용자가 생성한 모든 새 레코드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-170">You should see the default DNS and SOA records, which are created in every zone, plus any new records you have created.</span></span>

![영역](./media/dns-getstarted-portal/viewzone500.png)


## <a name="update-name-servers"></a><span data-ttu-id="bff10-172">이름 서버 업데이트</span><span class="sxs-lookup"><span data-stu-id="bff10-172">Update name servers</span></span>

<span data-ttu-id="bff10-173">DNS 영역 및 레코드가 적절히 설정되었다면 Azure DNS 이름 서버를 사용하도록 도메인 이름을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-173">Once you are satisfied that your DNS zone and records have been set up correctly, you need to configure your domain name to use the Azure DNS name servers.</span></span> <span data-ttu-id="bff10-174">이렇게 하면 인터넷에 있는 다른 사용자가 DNS 레코드를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-174">This enables other users on the Internet to find your DNS records.</span></span>

<span data-ttu-id="bff10-175">영역에 대한 이름 서버는 Azure 포털에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-175">The name servers for your zone are given in the Azure portal:</span></span>

![영역](./media/dns-getstarted-portal/viewzonens500.png)

<span data-ttu-id="bff10-177">이러한 이름 서버는 사용자가 도메인 이름을 구입한 도메인 이름 등록 기관에서 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-177">These name servers should be configured with the domain name registrar (where you purchased the domain name).</span></span> <span data-ttu-id="bff10-178">등록 기관에서 도메인의 이름 서버를 설정하는 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-178">Your registrar offers the option to set up the name servers for the domain.</span></span> <span data-ttu-id="bff10-179">자세한 내용은 [Azure DNS에 도메인 위임](dns-domain-delegation.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bff10-179">For more information, see [Delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="bff10-180">모든 리소스 삭제</span><span class="sxs-lookup"><span data-stu-id="bff10-180">Delete all resources</span></span>

<span data-ttu-id="bff10-181">이 문서에서 만든 모든 리소스를 삭제하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-181">To delete all resources created in this article, complete the following steps:</span></span>

1. <span data-ttu-id="bff10-182">Azure Portal의 **즐겨찾기** 창에서 **모든 리소스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-182">In the Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="bff10-183">모든 리소스 블레이드에서 **MyResourceGroup** 리소스 그룹을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-183">Click the **MyResourceGroup** resource group in the All resources blade.</span></span> <span data-ttu-id="bff10-184">선택한 구독에 이미 여러 개의 리소스가 있는 경우 **이름을 기준으로 필터링...**에 **MyResourceGroup**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-184">If the subscription you selected already has several resources in it, you can enter **MyResourceGroup** in the **Filter by name…**</span></span> <span data-ttu-id="bff10-185">리소스 그룹에 간편하게 액세스할 수 있는 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-185">box to easily access the resource group.</span></span>
1. <span data-ttu-id="bff10-186">**MyResourceGroup** 블레이드에서 **삭제** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-186">In the **MyResourceGroup** blade, click the **Delete** button.</span></span>
1. <span data-ttu-id="bff10-187">포털에서 삭제할 리소스 그룹의 이름을 입력하여 리소스 그룹 삭제를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-187">The portal requires you to type the name of the resource group to confirm that you want to delete it.</span></span> <span data-ttu-id="bff10-188">**삭제**를 클릭하고, 리소스 그룹 이름으로 *MyResourceGroup*을 입력한 다음 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-188">Click **Delete**, Type *MyResourceGroup* for the resource group name, then click **Delete**.</span></span> <span data-ttu-id="bff10-189">리소스 그룹을 삭제하면 리소스 그룹 내 모든 리소스가 삭제되므로 리소스 그룹을 삭제하기 전에 리소스 그룹의 콘텐츠를 항상 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-189">Deleting a resource group deletes all resources within the resource group, so always be sure to confirm the contents of a resource group before deleting it.</span></span> <span data-ttu-id="bff10-190">포털에서 리소스 그룹 내 포함된 모든 리소스가 삭제된 다음 리소스 그룹 자체가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-190">The portal deletes all resources contained within the resource group, then deletes the resource group itself.</span></span> <span data-ttu-id="bff10-191">이 프로세스는 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="bff10-191">This process takes several minutes.</span></span>


## <a name="next-steps"></a><span data-ttu-id="bff10-192">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bff10-192">Next steps</span></span>

<span data-ttu-id="bff10-193">Azure DNS에 대한 자세한 내용은 [Azure DNS 개요](dns-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bff10-193">To learn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="bff10-194">Azure DNS에서 DNS 레코드 관리에 대한 자세한 내용은 [Azure Portal을 사용하여 DNS 레코드 및 레코드 집합 관리](dns-operations-recordsets-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bff10-194">To learn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets by using the Azure portal](dns-operations-recordsets-portal.md).</span></span>

