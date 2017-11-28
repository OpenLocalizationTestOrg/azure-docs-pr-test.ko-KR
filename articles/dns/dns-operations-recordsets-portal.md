---
title: "DNS aaaManage 집합 및 Azure dns 레코드를 기록 합니다. | Microsoft Docs"
description: "Azure DNS 설정 하 고 도메인을 호스팅할 때 기록 하는 hello 기능 toomanage DNS 레코드를 제공 합니다."
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
ms.openlocfilehash: 2e62d017341589eaf8d1f8df2fe5db4b973381d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-record-sets-by-using-hello-azure-portal"></a><span data-ttu-id="1df23-103">Hello Azure 포털을 사용 하 여 DNS 레코드 및 레코드 집합 관리</span><span class="sxs-lookup"><span data-stu-id="1df23-103">Manage DNS records and record sets by using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1df23-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="1df23-104">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="1df23-105">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1df23-105">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="1df23-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1df23-106">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="1df23-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1df23-107">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="1df23-108">이 문서 toomanage 레코드 집합 및 레코드를 사용 하 여 DNS 영역이 hello Azure 포털에 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-108">This article shows you how toomanage record sets and records for your DNS zone by using hello Azure portal.</span></span>

<span data-ttu-id="1df23-109">DNS 레코드 집합 및 개별 DNS 레코드 간의 중요 한 toounderstand hello 차이</span><span class="sxs-lookup"><span data-stu-id="1df23-109">It's important toounderstand hello difference between DNS record sets and individual DNS records.</span></span> <span data-ttu-id="1df23-110">레코드 집합은 hello 동일한 이름을 지정 하 고 동일한 hello는 입력이 있는 영역에 있는 레코드의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-110">A record set is a collection of records in a zone that have hello same name and are hello same type.</span></span> <span data-ttu-id="1df23-111">자세한 내용은 참조 [만드는 DNS 레코드 집합 및 레코드를 사용 하 여 Azure 포털 hello](dns-getstarted-create-recordset-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-111">For more information, see [Create DNS record sets and records by using hello Azure portal](dns-getstarted-create-recordset-portal.md).</span></span>

## <a name="create-a-new-record-set-and-record"></a><span data-ttu-id="1df23-112">새 레코드 집합 및 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="1df23-112">Create a new record set and record</span></span>

<span data-ttu-id="1df23-113">toocreate hello Azure 포털에서에서 설정 하는 레코드 참조 [만드는 DNS 레코드를 사용 하 여 Azure 포털 hello](dns-getstarted-create-recordset-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-113">toocreate a record set in hello Azure portal, see [Create DNS records by using hello Azure portal](dns-getstarted-create-recordset-portal.md).</span></span>

## <a name="view-a-record-set"></a><span data-ttu-id="1df23-114">레코드 집합 보기</span><span class="sxs-lookup"><span data-stu-id="1df23-114">View a record set</span></span>

1. <span data-ttu-id="1df23-115">Hello Azure 포털에서에서 toohello 이동 **DNS 영역** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-115">In hello Azure portal, go toohello **DNS zone** blade.</span></span>
2. <span data-ttu-id="1df23-116">레코드 집합 hello 찾아 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-116">Search for hello record set and select it.</span></span> <span data-ttu-id="1df23-117">이 hello 레코드 집합 속성을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-117">This opens hello record set properties.</span></span>

    ![레코드 집합 검색](./media/dns-operations-recordsets-portal/searchset500.png)

## <a name="add-a-new-record-tooa-record-set"></a><span data-ttu-id="1df23-119">새 레코드 tooa 레코드 집합 추가</span><span class="sxs-lookup"><span data-stu-id="1df23-119">Add a new record tooa record set</span></span>

<span data-ttu-id="1df23-120">Too20 레코드 tooany 레코드 집합을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-120">You can add up too20 records tooany record set.</span></span> <span data-ttu-id="1df23-121">레코드 집합에는 두 개의 동일한 레코드가 포함될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-121">A record set cannot contain two identical records.</span></span> <span data-ttu-id="1df23-122">(0 개 레코드)와 빈 레코드 집합을 만들 수 있지만 hello Azure DNS 이름 서버에 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-122">Empty record sets (with zero records) can be created, but do not appear on hello Azure DNS name servers.</span></span> <span data-ttu-id="1df23-123">CNAME 형식의 레코드 집합은 최대 하나의 레코드를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-123">Record sets of type CNAME can contain one record at most.</span></span>

1. <span data-ttu-id="1df23-124">Hello에 **속성을 설정 하는 레코드** hello 레코드를 클릭 하는 DNS 영역이 블레이드 되도록 tooadd 레코드를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-124">On hello **Record set properties** blade for your DNS zone, click hello record set that you want tooadd a record to.</span></span>

    ![레코드 집합 선택](./media/dns-operations-recordsets-portal/selectset500.png)

2. <span data-ttu-id="1df23-126">Hello 필드에 입력 하 여 속성을 설정 하는 hello 레코드를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-126">Specify hello record set properties by filling in hello fields.</span></span>

    ![레코드 추가](./media/dns-operations-recordsets-portal/addrecord500.png)

3. <span data-ttu-id="1df23-128">클릭 **저장** 에 hello hello 블레이드 toosave 맨 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-128">Click **Save** at hello top of hello blade toosave your settings.</span></span> <span data-ttu-id="1df23-129">그런 다음 hello 블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-129">Then close hello blade.</span></span>
4. <span data-ttu-id="1df23-130">Hello 구석에 hello 레코드가 저장 하는지 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-130">In hello corner, you will see that hello record is saving.</span></span>

    ![레코드 집합 저장](./media/dns-operations-recordsets-portal/saving150.png)

<span data-ttu-id="1df23-132">Hello 레코드를 저장 한 후 hello hello에 대 한 값 **DNS 영역** 블레이드 hello 새 레코드에 반영 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-132">After hello record has been saved, hello values on hello **DNS zone** blade will reflect hello new record.</span></span>

## <a name="update-a-record"></a><span data-ttu-id="1df23-133">레코드 업데이트</span><span class="sxs-lookup"><span data-stu-id="1df23-133">Update a record</span></span>

<span data-ttu-id="1df23-134">기존 레코드 집합의 레코드를 업데이트할 때 hello 필드를 업데이트할 수 있습니다 작업 하는 레코드의 hello 형식에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-134">When you update a record in an existing record set, hello fields you can update depend on hello type of record you're working with.</span></span>

1. <span data-ttu-id="1df23-135">Hello에 **속성을 설정 하는 레코드** 블레이드 레코드 세트 hello 레코드에 대 한 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-135">On hello **Record set properties** blade for your record set, search for hello record.</span></span>
2. <span data-ttu-id="1df23-136">Hello 레코드를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-136">Modify hello record.</span></span> <span data-ttu-id="1df23-137">레코드를 수정 하는 경우 hello hello 레코드에 대 한 사용 가능한 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-137">When you modify a record, you can change hello available settings for hello record.</span></span> <span data-ttu-id="1df23-138">다음 예제는 hello에서 hello **IP 주소** 필드를 선택 하 고 수정 하 고 hello 프로세스의 hello IP 주소는 합니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-138">In hello following example, hello **IP address** field is selected, and hello IP address is in hello process of being modified.</span></span>

    ![레코드 수정](./media/dns-operations-recordsets-portal/modifyrecord500.png)

3. <span data-ttu-id="1df23-140">클릭 **저장** 에 hello hello 블레이드 toosave 맨 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-140">Click **Save** at hello top of hello blade toosave your settings.</span></span> <span data-ttu-id="1df23-141">Hello 오른쪽 상단에 저장 된 hello 레코드 hello 알림이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-141">In hello upper right corner, you'll see hello notification that hello record has been saved.</span></span>

    ![저장된 레코드 집합](./media/dns-operations-recordsets-portal/saved150.png)

<span data-ttu-id="1df23-143">Hello 레코드에 대 한 hello 값 hello에 설정 hello 레코드를 저장 한 후 **DNS 영역** 블레이드 업데이트 hello 레코드에 반영 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-143">After hello record has been saved, hello values for hello record set on hello **DNS zone** blade will reflect hello updated record.</span></span>

## <a name="remove-a-record-from-a-record-set"></a><span data-ttu-id="1df23-144">레코드 집합에서 레코드 제거</span><span class="sxs-lookup"><span data-stu-id="1df23-144">Remove a record from a record set</span></span>

<span data-ttu-id="1df23-145">레코드 집합에서 hello Azure 포털 tooremove 레코드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-145">You can use hello Azure portal tooremove records from a record set.</span></span> <span data-ttu-id="1df23-146">Note hello 마지막 레코드를 레코드 집합에서 제거 hello 레코드 집합을 삭제 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-146">Note that removing hello last record from a record set does not delete hello record set.</span></span>

1. <span data-ttu-id="1df23-147">Hello에 **속성을 설정 하는 레코드** 블레이드 레코드 세트 hello 레코드에 대 한 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-147">On hello **Record set properties** blade for your record set, search for hello record.</span></span>
2. <span data-ttu-id="1df23-148">Tooremove hello 레코드를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-148">Click hello record that you want tooremove.</span></span> <span data-ttu-id="1df23-149">그런 후 **제거**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-149">Then select **Remove**.</span></span>

    ![레코드 제거](./media/dns-operations-recordsets-portal/removerecord500.png)

3. <span data-ttu-id="1df23-151">클릭 **저장** 에 hello hello 블레이드 toosave 맨 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-151">Click **Save** at hello top of hello blade toosave your settings.</span></span>
4. <span data-ttu-id="1df23-152">Hello 레코드를 제거한 후 hello hello 레코드 hello에 대 한 값 **DNS 영역** 블레이드 hello 제거 반영 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-152">After hello record has been removed, hello values for hello record on hello **DNS zone** blade will reflect hello removal.</span></span>

## <span data-ttu-id="1df23-153"><a name="delete"></a>레코드 집합 삭제</span><span class="sxs-lookup"><span data-stu-id="1df23-153"><a name="delete"></a>Delete a record set</span></span>

1. <span data-ttu-id="1df23-154">Hello에 **속성을 설정 하는 레코드** 클릭 하 여 레코드 집합에 대 한 블레이드 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-154">On hello **Record set properties** blade for your record set, click **Delete**.</span></span>

    ![레코드 집합 삭제](./media/dns-operations-recordsets-portal/deleterecordset500.png)

2. <span data-ttu-id="1df23-156">Toodelete hello 레코드 집합을 원하는 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-156">A message appears asking if you want toodelete hello record set.</span></span>
3. <span data-ttu-id="1df23-157">설정 되어 있는지 확인 hello 이름 일치 hello 레코드 toodelete를 원하고 클릭 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-157">Verify that hello name matches hello record set that you want toodelete, and then click **Yes**.</span></span>
4. <span data-ttu-id="1df23-158">Hello에 **DNS 영역** 블레이드에서 hello 레코드 집합은 더 이상 볼 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-158">On hello **DNS zone** blade, verify that hello record set is no longer visible.</span></span>

## <a name="work-with-ns-and-soa-records"></a><span data-ttu-id="1df23-159">NS 및 SOA 레코드 작업</span><span class="sxs-lookup"><span data-stu-id="1df23-159">Work with NS and SOA records</span></span>

<span data-ttu-id="1df23-160">자동으로 생성되는 NS 및 SOA 레코드는 다른 레코드 유형과 다르게 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-160">NS and SOA records that are automatically created are managed differently from other record types.</span></span>

### <a name="modify-soa-records"></a><span data-ttu-id="1df23-161">SOA 레코드 수정</span><span class="sxs-lookup"><span data-stu-id="1df23-161">Modify SOA records</span></span>

<span data-ttu-id="1df23-162">추가 하거나 자동으로 설정 hello 영역 루트에 SOA 레코드를 생성 하는 hello에서 레코드를 제거할 수 없습니다 (이름 = "@").</span><span class="sxs-lookup"><span data-stu-id="1df23-162">You cannot add or remove records from hello automatically created SOA record set at hello zone apex (name = "@").</span></span> <span data-ttu-id="1df23-163">그러나 hello "호스트") (제외 SOA 레코드 내에 hello 매개 변수 중 하나를 수정 하 고 TTL을 설정 하는 hello 레코드.</span><span class="sxs-lookup"><span data-stu-id="1df23-163">However, you can modify any of hello parameters within hello SOA record (except "Host") and hello record set TTL.</span></span>

### <a name="modify-ns-records-at-hello-zone-apex"></a><span data-ttu-id="1df23-164">Hello 영역 루트에 있는 NS 레코드를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-164">Modify NS records at hello zone apex</span></span>

<span data-ttu-id="1df23-165">hello 영역 루트에서 설정 하는 hello NS 레코드는 각 DNS 영역과 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-165">hello NS record set at hello zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="1df23-166">Hello Azure DNS 이름 서버 할당된 toohello 영역의 hello 이름이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-166">It contains hello names of hello Azure DNS name servers assigned toohello zone.</span></span>

<span data-ttu-id="1df23-167">추가 이름 서버 toothis NS 레코드 집합을 공동 도메인 DNS 공급자를 둘 이상의 호스팅 toosupport를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-167">You can add additional name servers toothis NS record set, toosupport co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="1df23-168">또한 TTL hello 및이 레코드 집합에 대 한 메타 데이터를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-168">You can also modify hello TTL and metadata for this record set.</span></span> <span data-ttu-id="1df23-169">그러나 제거 하거나 hello 미리 채워진된 Azure DNS 이름 서버를 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-169">However, you cannot remove or modify hello pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="1df23-170">Note이 적용 hello 영역 루트에서 레코드 집합 toohello NS만 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-170">Note that this applies only toohello NS record set at hello zone apex.</span></span> <span data-ttu-id="1df23-171">제약 조건 없이 (사용 되는 toodelegate 하위 영역)으로 시간대에서 다른 NS 레코드 집합을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-171">Other NS record sets in your zone (as used toodelegate child zones) can be modified without constraint.</span></span>

### <a name="delete-soa-or-ns-record-sets"></a><span data-ttu-id="1df23-172">SOA 또는 NS 레코드 집합 삭제</span><span class="sxs-lookup"><span data-stu-id="1df23-172">Delete SOA or NS record sets</span></span>

<span data-ttu-id="1df23-173">Hello NS 및 SOA 레코드 집합 hello 영역 루트에서 삭제할 수 없습니다 (이름 = "@") hello 영역을 만들 때 자동으로 생성 됩니다입니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-173">You cannot delete hello SOA and NS record sets at hello zone apex (name = "@") that are created automatically when hello zone is created.</span></span> <span data-ttu-id="1df23-174">Hello 영역을 삭제 하면 자동으로 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-174">They are deleted automatically when you delete hello zone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1df23-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1df23-175">Next steps</span></span>

* <span data-ttu-id="1df23-176">Azure DNS에 대 한 자세한 내용은 참조 hello [Azure DNS 개요](dns-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-176">For more information about Azure DNS, see hello [Azure DNS overview](dns-overview.md).</span></span>
* <span data-ttu-id="1df23-177">DNS를 자동화 하는 방법에 대 한 자세한 내용은 참조 [만들 DNS 영역 및 레코드 집합을 사용 하 여 hello.NET SDK](dns-sdk.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1df23-177">For more information about automating DNS, see [Creating DNS zones and record sets using hello .NET SDK](dns-sdk.md).</span></span>
* <span data-ttu-id="1df23-178">역방향 DNS 레코드에 대한 자세한 내용은 [Azure의 역방향 DNS 및 지원 개요](dns-reverse-dns-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1df23-178">For more information about reverse DNS records, see [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>
