---
title: "Azure DNS에서 DNS 레코드 집합 및 레코드 관리 | Microsoft Docs"
description: "Azure DNS는 도메인을 호스트하는 경우 DNS 레코드 집합 및 레코드를 관리하는 기능을 제공합니다."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 18ed44a1-7bfe-454f-964e-922ad978264a
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 001b80ccba43beab44f6a598f820df65a85a345f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-dns-records-and-record-sets-by-using-the-azure-portal"></a><span data-ttu-id="27577-103">Azure 포털을 사용하여 DNS 레코드 및 레코드 집합 관리</span><span class="sxs-lookup"><span data-stu-id="27577-103">Manage DNS records and record sets by using the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="27577-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="27577-104">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="27577-105">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="27577-105">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="27577-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="27577-106">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="27577-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="27577-107">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="27577-108">이 문서는 Azure 포털을 사용하여 DNS 영역에 대한 레코드 집합 및 레코드를 관리하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="27577-108">This article shows you how to manage record sets and records for your DNS zone by using the Azure portal.</span></span>

<span data-ttu-id="27577-109">DNS 레코드 집합과 개별 DNS 레코드 사이의 차이를 이해하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="27577-109">It's important to understand the difference between DNS record sets and individual DNS records.</span></span> <span data-ttu-id="27577-110">레코드 집합은 영역 내에서 동일한 이름과 형식을 가진 DNS 레코드 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="27577-110">A record set is a collection of records in a zone that have the same name and are the same type.</span></span> <span data-ttu-id="27577-111">자세한 내용은 [Azure 포털을 사용하여 DNS 레코드 집합 및 레코드 만들기](dns-getstarted-create-recordset-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27577-111">For more information, see [Create DNS record sets and records by using the Azure portal](dns-getstarted-create-recordset-portal.md).</span></span>

## <a name="create-a-new-record-set-and-record"></a><span data-ttu-id="27577-112">새 레코드 집합 및 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="27577-112">Create a new record set and record</span></span>

<span data-ttu-id="27577-113">Azure 포털에서 레코드 집합을 만들려면 [Azure 포털을 사용하여 DNS 레코드 만들기](dns-getstarted-create-recordset-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27577-113">To create a record set in the Azure portal, see [Create DNS records by using the Azure portal](dns-getstarted-create-recordset-portal.md).</span></span>

## <a name="view-a-record-set"></a><span data-ttu-id="27577-114">레코드 집합 보기</span><span class="sxs-lookup"><span data-stu-id="27577-114">View a record set</span></span>

1. <span data-ttu-id="27577-115">Azure 포털에서 **DNS 영역** 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="27577-115">In the Azure portal, go to the **DNS zone** blade.</span></span>
2. <span data-ttu-id="27577-116">레코드 집합을 검색한 후 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="27577-116">Search for the record set and select it.</span></span> <span data-ttu-id="27577-117">레코드 집합 속성이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="27577-117">This opens the record set properties.</span></span>

    ![레코드 집합 검색](./media/dns-operations-recordsets-portal/searchset500.png)

## <a name="add-a-new-record-to-a-record-set"></a><span data-ttu-id="27577-119">레코드 집합에 새 레코드 추가</span><span class="sxs-lookup"><span data-stu-id="27577-119">Add a new record to a record set</span></span>

<span data-ttu-id="27577-120">레코드 집합에 최대 20개의 레코드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27577-120">You can add up to 20 records to any record set.</span></span> <span data-ttu-id="27577-121">레코드 집합에는 두 개의 동일한 레코드가 포함될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="27577-121">A record set cannot contain two identical records.</span></span> <span data-ttu-id="27577-122">빈 레코드 집합(0개 레코드 포함)을 만들 수 있지만 Azure DNS 이름 서버에는 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="27577-122">Empty record sets (with zero records) can be created, but do not appear on the Azure DNS name servers.</span></span> <span data-ttu-id="27577-123">CNAME 형식의 레코드 집합은 최대 하나의 레코드를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27577-123">Record sets of type CNAME can contain one record at most.</span></span>

1. <span data-ttu-id="27577-124">DNS 영역에 대한 **레코드 설정 속성** 블레이드에서 레코드를 추가하려는 레코드 집합을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27577-124">On the **Record set properties** blade for your DNS zone, click the record set that you want to add a record to.</span></span>

    ![레코드 집합 선택](./media/dns-operations-recordsets-portal/selectset500.png)

2. <span data-ttu-id="27577-126">필드에 입력하여 레코드 집합 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="27577-126">Specify the record set properties by filling in the fields.</span></span>

    ![레코드 추가](./media/dns-operations-recordsets-portal/addrecord500.png)

3. <span data-ttu-id="27577-128">블레이드의 맨 위에서 **저장** 을 클릭하여 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="27577-128">Click **Save** at the top of the blade to save your settings.</span></span> <span data-ttu-id="27577-129">그런 다음 블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="27577-129">Then close the blade.</span></span>
4. <span data-ttu-id="27577-130">가장자리에 레코드가 저장되는 것이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="27577-130">In the corner, you will see that the record is saving.</span></span>

    ![레코드 집합 저장](./media/dns-operations-recordsets-portal/saving150.png)

<span data-ttu-id="27577-132">레코드가 저장된 후 **DNS 영역** 블레이드의 값은 새 레코드를 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="27577-132">After the record has been saved, the values on the **DNS zone** blade will reflect the new record.</span></span>

## <a name="update-a-record"></a><span data-ttu-id="27577-133">레코드 업데이트</span><span class="sxs-lookup"><span data-stu-id="27577-133">Update a record</span></span>

<span data-ttu-id="27577-134">기존 레코드 집합에서 레코드를 업데이트할 때 업데이트할 수 있는 필드는 사용하는 레코드의 유형에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="27577-134">When you update a record in an existing record set, the fields you can update depend on the type of record you're working with.</span></span>

1. <span data-ttu-id="27577-135">레코드 집합에 대한 **레코드 설정 속성** 블레이드에서 레코드를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="27577-135">On the **Record set properties** blade for your record set, search for the record.</span></span>
2. <span data-ttu-id="27577-136">레코드를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="27577-136">Modify the record.</span></span> <span data-ttu-id="27577-137">레코드를 수정할 때 레코드에 대해 사용 가능한 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27577-137">When you modify a record, you can change the available settings for the record.</span></span> <span data-ttu-id="27577-138">다음 예제에서는 **IP 주소** 필드가 선택되고 IP 주소는 수정되는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="27577-138">In the following example, the **IP address** field is selected, and the IP address is in the process of being modified.</span></span>

    ![레코드 수정](./media/dns-operations-recordsets-portal/modifyrecord500.png)

3. <span data-ttu-id="27577-140">블레이드의 맨 위에서 **저장** 을 클릭하여 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="27577-140">Click **Save** at the top of the blade to save your settings.</span></span> <span data-ttu-id="27577-141">오른쪽 위 모서리에서 레코드가 저장되었다는 알림을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27577-141">In the upper right corner, you'll see the notification that the record has been saved.</span></span>

    ![저장된 레코드 집합](./media/dns-operations-recordsets-portal/saved150.png)

<span data-ttu-id="27577-143">레코드가 저장된 후 **DNS 영역** 블레이드의 레코드 집합에 대한 값은 업데이트된 레코드를 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="27577-143">After the record has been saved, the values for the record set on the **DNS zone** blade will reflect the updated record.</span></span>

## <a name="remove-a-record-from-a-record-set"></a><span data-ttu-id="27577-144">레코드 집합에서 레코드 제거</span><span class="sxs-lookup"><span data-stu-id="27577-144">Remove a record from a record set</span></span>

<span data-ttu-id="27577-145">Azure 포털을 사용하여 레코드 집합에서 레코드를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27577-145">You can use the Azure portal to remove records from a record set.</span></span> <span data-ttu-id="27577-146">레코드 집합에서 마지막 레코드를 제거해도 레코드 집합은 삭제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="27577-146">Note that removing the last record from a record set does not delete the record set.</span></span>

1. <span data-ttu-id="27577-147">레코드 집합에 대한 **레코드 설정 속성** 블레이드에서 레코드를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="27577-147">On the **Record set properties** blade for your record set, search for the record.</span></span>
2. <span data-ttu-id="27577-148">제거하려는 레코드를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27577-148">Click the record that you want to remove.</span></span> <span data-ttu-id="27577-149">그런 후 **제거**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="27577-149">Then select **Remove**.</span></span>

    ![레코드 제거](./media/dns-operations-recordsets-portal/removerecord500.png)

3. <span data-ttu-id="27577-151">블레이드의 맨 위에서 **저장** 을 클릭하여 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="27577-151">Click **Save** at the top of the blade to save your settings.</span></span>
4. <span data-ttu-id="27577-152">레코드가 제거된 후 **DNS 영역** 블레이드의 레코드 값에 제거 결과가 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="27577-152">After the record has been removed, the values for the record on the **DNS zone** blade will reflect the removal.</span></span>

## <span data-ttu-id="27577-153"><a name="delete"></a>레코드 집합 삭제</span><span class="sxs-lookup"><span data-stu-id="27577-153"><a name="delete"></a>Delete a record set</span></span>

1. <span data-ttu-id="27577-154">레코드 집합에 대한 **레코드 집합 속성** 블레이드에서 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27577-154">On the **Record set properties** blade for your record set, click **Delete**.</span></span>

    ![레코드 집합 삭제](./media/dns-operations-recordsets-portal/deleterecordset500.png)

2. <span data-ttu-id="27577-156">레코드 집합을 삭제할지 묻는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="27577-156">A message appears asking if you want to delete the record set.</span></span>
3. <span data-ttu-id="27577-157">이름이 삭제하려는 레코드 집합과 일치하는지 확인한 다음 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27577-157">Verify that the name matches the record set that you want to delete, and then click **Yes**.</span></span>
4. <span data-ttu-id="27577-158">**DNS 영역** 블레이드에서 레코드 집합을 더 이상 볼 수 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="27577-158">On the **DNS zone** blade, verify that the record set is no longer visible.</span></span>

## <a name="work-with-ns-and-soa-records"></a><span data-ttu-id="27577-159">NS 및 SOA 레코드 작업</span><span class="sxs-lookup"><span data-stu-id="27577-159">Work with NS and SOA records</span></span>

<span data-ttu-id="27577-160">자동으로 생성되는 NS 및 SOA 레코드는 다른 레코드 유형과 다르게 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="27577-160">NS and SOA records that are automatically created are managed differently from other record types.</span></span>

### <a name="modify-soa-records"></a><span data-ttu-id="27577-161">SOA 레코드 수정</span><span class="sxs-lookup"><span data-stu-id="27577-161">Modify SOA records</span></span>

<span data-ttu-id="27577-162">영역 루트(이름 = "@")에 설정된 자동으로 생성된 SOA 레코드 집합에서 레코드를 추가 또는 제거할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="27577-162">You cannot add or remove records from the automatically created SOA record set at the zone apex (name = "@").</span></span> <span data-ttu-id="27577-163">그러나 SOA 레코드 내의 매개 변수("Host" 제외) 및 레코드 집합 TTL을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27577-163">However, you can modify any of the parameters within the SOA record (except "Host") and the record set TTL.</span></span>

### <a name="modify-ns-records-at-the-zone-apex"></a><span data-ttu-id="27577-164">영역 루트의 NS 레코드 수정</span><span class="sxs-lookup"><span data-stu-id="27577-164">Modify NS records at the zone apex</span></span>

<span data-ttu-id="27577-165">각 DNS 영역에 영역 루트의 NS 레코드 집합이 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="27577-165">The NS record set at the zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="27577-166">여기에는 영역에 할당된 Azure DNS 이름 서버의 이름이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="27577-166">It contains the names of the Azure DNS name servers assigned to the zone.</span></span>

<span data-ttu-id="27577-167">이 NS 레코드 집합에 추가 이름 서버를 추가하여 DNS 공급자가 2개 이상 있는 공동 호스팅 도메인을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27577-167">You can add additional name servers to this NS record set, to support co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="27577-168">또한 이 레코드 집합의 TTL 및 메타데이터를 수정할 수 있습니다.또한 이 레코드 집합의 TTL 및 메타데이터를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27577-168">You can also modify the TTL and metadata for this record set.</span></span> <span data-ttu-id="27577-169">그러나 미리 채워진 Azure DNS 이름 서버를 제거 또는 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="27577-169">However, you cannot remove or modify the pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="27577-170">이는 영역 루트에 있는 NS 레코드 집합에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="27577-170">Note that this applies only to the NS record set at the zone apex.</span></span> <span data-ttu-id="27577-171">영역의 다른 NS 레코드 집합은 제약 없이 수정할 수 있습니다(자식 영역을 위임하는 데 사용되므로).</span><span class="sxs-lookup"><span data-stu-id="27577-171">Other NS record sets in your zone (as used to delegate child zones) can be modified without constraint.</span></span>

### <a name="delete-soa-or-ns-record-sets"></a><span data-ttu-id="27577-172">SOA 또는 NS 레코드 집합 삭제</span><span class="sxs-lookup"><span data-stu-id="27577-172">Delete SOA or NS record sets</span></span>

<span data-ttu-id="27577-173">영역을 만들 때 자동으로 만들어진 영역 루트(이름 = "@")의 SOA 및 NS 레코드 집합은 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="27577-173">You cannot delete the SOA and NS record sets at the zone apex (name = "@") that are created automatically when the zone is created.</span></span> <span data-ttu-id="27577-174">영역을 삭제하면 자동으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="27577-174">They are deleted automatically when you delete the zone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="27577-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="27577-175">Next steps</span></span>

* <span data-ttu-id="27577-176">Azure DNS에 대한 자세한 내용은 [Azure DNS 개요](dns-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27577-176">For more information about Azure DNS, see the [Azure DNS overview](dns-overview.md).</span></span>
* <span data-ttu-id="27577-177">DNS 자동화에 대한 자세한 내용은 [.NET SDK를 사용하여 DNS 영역 및 레코드 집합 만들기](dns-sdk.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27577-177">For more information about automating DNS, see [Creating DNS zones and record sets using the .NET SDK](dns-sdk.md).</span></span>
* <span data-ttu-id="27577-178">역방향 DNS 레코드에 대한 자세한 내용은 [Azure의 역방향 DNS 및 지원 개요](dns-reverse-dns-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27577-178">For more information about reverse DNS records, see [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>
