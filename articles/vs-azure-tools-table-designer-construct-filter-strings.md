---
title: "테이블 디자이너에 대한 필터 문자열 생성하기 | Microsoft Docs"
description: "테이블 디자이너에 대한 필터 문자열 생성하기"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: a1a10ea1-687a-4ee1-a952-6b24c2fe1a22
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 069224d84462b4955912ce1462a65298a5acc04a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="constructing-filter-strings-for-the-table-designer"></a><span data-ttu-id="ad40e-103">테이블 디자이너에 대한 필터 문자열 생성하기</span><span class="sxs-lookup"><span data-stu-id="ad40e-103">Constructing Filter Strings for the Table Designer</span></span>
## <a name="overview"></a><span data-ttu-id="ad40e-104">개요</span><span class="sxs-lookup"><span data-stu-id="ad40e-104">Overview</span></span>
<span data-ttu-id="ad40e-105">Visual Studio **테이블 디자이너**에 표시된 Azure 테이블에서 데이터를 필터링하려면 필터 문자열을 생성하고 필터 필드에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40e-105">To filter data in an Azure table that is displayed in the Visual Studio **Table Designer**, you construct a filter string and enter it into the filter field.</span></span> <span data-ttu-id="ad40e-106">필터 문자열 구문은 WCF 데이터 서비스에 의해 정의되며 SQL WHERE 절과 유사하지만 HTTP 요청을 통해 테이블 서비스에 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad40e-106">The filter string syntax is defined by the WCF Data Services and is similar to a SQL WHERE clause, but is sent to the Table service via an HTTP request.</span></span> <span data-ttu-id="ad40e-107">**테이블 디자이너** 는 적절한 인코딩을 처리하므로 원하는 속성 값을 필터링하려면 단순히 속성 이름, 비교 연산자, 조건 값 및 필요에 따라 부울 연산자를 필터 필드에 입력하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad40e-107">The **Table Designer** handles the proper encoding for you, so to filter on a desired property value, you need only enter the property name, comparison operator, criteria value, and optionally, Boolean operator in the filter field.</span></span> <span data-ttu-id="ad40e-108">[저장소 서비스 REST API 참조](http://go.microsoft.com/fwlink/p/?LinkId=400447)를 통해 테이블 쿼리에 대한 URL을 생성하는 경우 $filter 쿼리 옵션은 포함할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ad40e-108">You do not need to include the $filter query option as you would if you were constructing a URL to query the table via the [Storage Services REST API Reference](http://go.microsoft.com/fwlink/p/?LinkId=400447).</span></span>

<span data-ttu-id="ad40e-109">WCF 데이터 서비스는 [개방형 데이터 프로토콜](http://go.microsoft.com/fwlink/p/?LinkId=214805) (OData)에 기반을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="ad40e-109">The WCF Data Services are based on the [Open Data Protocol](http://go.microsoft.com/fwlink/p/?LinkId=214805) (OData).</span></span> <span data-ttu-id="ad40e-110">필터 시스템 쿼리 옵션 (**$filter**)에 대한 자세한 내용은 [OData URI 규칙 사양](http://go.microsoft.com/fwlink/p/?LinkId=214806)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad40e-110">For details on the filter system query option (**$filter**), see the [OData URI Conventions specification](http://go.microsoft.com/fwlink/p/?LinkId=214806).</span></span>

## <a name="comparison-operators"></a><span data-ttu-id="ad40e-111">비교 연산자</span><span class="sxs-lookup"><span data-stu-id="ad40e-111">Comparison Operators</span></span>
<span data-ttu-id="ad40e-112">다음의 논리 연산자는 모든 속성 유형에 대해 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad40e-112">The following logical operators are supported for all property types:</span></span>

| <span data-ttu-id="ad40e-113">논리 연산자</span><span class="sxs-lookup"><span data-stu-id="ad40e-113">Logical operator</span></span> | <span data-ttu-id="ad40e-114">설명</span><span class="sxs-lookup"><span data-stu-id="ad40e-114">Description</span></span> | <span data-ttu-id="ad40e-115">필터 문자열의 예</span><span class="sxs-lookup"><span data-stu-id="ad40e-115">Example filter string</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ad40e-116">eq</span><span class="sxs-lookup"><span data-stu-id="ad40e-116">eq</span></span> |<span data-ttu-id="ad40e-117">같음</span><span class="sxs-lookup"><span data-stu-id="ad40e-117">Equal</span></span> |<span data-ttu-id="ad40e-118">'Redmond'와 같은 도시</span><span class="sxs-lookup"><span data-stu-id="ad40e-118">City eq 'Redmond'</span></span> |
| <span data-ttu-id="ad40e-119">gt</span><span class="sxs-lookup"><span data-stu-id="ad40e-119">gt</span></span> |<span data-ttu-id="ad40e-120">다음보다 큼</span><span class="sxs-lookup"><span data-stu-id="ad40e-120">Greater than</span></span> |<span data-ttu-id="ad40e-121">20보다 큰 가격</span><span class="sxs-lookup"><span data-stu-id="ad40e-121">Price gt 20</span></span> |
| <span data-ttu-id="ad40e-122">ge</span><span class="sxs-lookup"><span data-stu-id="ad40e-122">ge</span></span> |<span data-ttu-id="ad40e-123">다음보다 크거나 같음</span><span class="sxs-lookup"><span data-stu-id="ad40e-123">Greater than or equal to</span></span> |<span data-ttu-id="ad40e-124">10보다 크거나 같은 가격</span><span class="sxs-lookup"><span data-stu-id="ad40e-124">Price ge 10</span></span> |
| <span data-ttu-id="ad40e-125">lt</span><span class="sxs-lookup"><span data-stu-id="ad40e-125">lt</span></span> |<span data-ttu-id="ad40e-126">다음보다 적음</span><span class="sxs-lookup"><span data-stu-id="ad40e-126">Less than</span></span> |<span data-ttu-id="ad40e-127">20보다 적은 가격</span><span class="sxs-lookup"><span data-stu-id="ad40e-127">Price lt 20</span></span> |
| <span data-ttu-id="ad40e-128">le</span><span class="sxs-lookup"><span data-stu-id="ad40e-128">le</span></span> |<span data-ttu-id="ad40e-129">다음보다 적거나 같음</span><span class="sxs-lookup"><span data-stu-id="ad40e-129">Less than or equal</span></span> |<span data-ttu-id="ad40e-130">100보다 적거나 같은 가격</span><span class="sxs-lookup"><span data-stu-id="ad40e-130">Price le 100</span></span> |
| <span data-ttu-id="ad40e-131">ne</span><span class="sxs-lookup"><span data-stu-id="ad40e-131">ne</span></span> |<span data-ttu-id="ad40e-132">다음과 같지 않음</span><span class="sxs-lookup"><span data-stu-id="ad40e-132">Not equal</span></span> |<span data-ttu-id="ad40e-133">'London'과 같지 않은 도시</span><span class="sxs-lookup"><span data-stu-id="ad40e-133">City ne 'London'</span></span> |
| <span data-ttu-id="ad40e-134">and</span><span class="sxs-lookup"><span data-stu-id="ad40e-134">and</span></span> |<span data-ttu-id="ad40e-135">and</span><span class="sxs-lookup"><span data-stu-id="ad40e-135">And</span></span> |<span data-ttu-id="ad40e-136">200보다 적거나 같은 가격 및 3.5보다 큰 가격</span><span class="sxs-lookup"><span data-stu-id="ad40e-136">Price le 200 and Price gt 3.5</span></span> |
| <span data-ttu-id="ad40e-137">또는</span><span class="sxs-lookup"><span data-stu-id="ad40e-137">or</span></span> |<span data-ttu-id="ad40e-138">또는</span><span class="sxs-lookup"><span data-stu-id="ad40e-138">Or</span></span> |<span data-ttu-id="ad40e-139">3.5보다 적거나 같은 가격 또는 200보다 큰 가격</span><span class="sxs-lookup"><span data-stu-id="ad40e-139">Price le 3.5 or Price gt 200</span></span> |
| <span data-ttu-id="ad40e-140">not</span><span class="sxs-lookup"><span data-stu-id="ad40e-140">not</span></span> |<span data-ttu-id="ad40e-141">not</span><span class="sxs-lookup"><span data-stu-id="ad40e-141">Not</span></span> |<span data-ttu-id="ad40e-142">not isAvailable</span><span class="sxs-lookup"><span data-stu-id="ad40e-142">not isAvailable</span></span> |

<span data-ttu-id="ad40e-143">필터 문자열을 생성할 때 다음의 규칙이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40e-143">When constructing a filter string, the following rules are important:</span></span>

* <span data-ttu-id="ad40e-144">논리 연산자를 사용하여 속성 값을 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40e-144">Use the logical operators to compare a property to a value.</span></span> <span data-ttu-id="ad40e-145">참고로 동적 값에 속성을 비교할 수 있으며 식의 한쪽은 상수여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40e-145">Note that it is not possible to compare a property to a dynamic value; one side of the expression must be a constant.</span></span>
* <span data-ttu-id="ad40e-146">필터 문자열의 모든 부분은 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40e-146">All parts of the filter string are case-sensitive.</span></span>
* <span data-ttu-id="ad40e-147">상수 값은 유효한 결과를 반환하는 필터에 대한 속성과 동일한 데이터 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40e-147">The constant value must be of the same data type as the property in order for the filter to return valid results.</span></span> <span data-ttu-id="ad40e-148">속성 형식에 대한 자세한 내용은 [테이블 서비스 데이터 모델 이해](http://go.microsoft.com/fwlink/p/?LinkId=400448)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad40e-148">For more information about supported property types, see [Understanding the Table Service Data Model](http://go.microsoft.com/fwlink/p/?LinkId=400448).</span></span>

## <a name="filtering-on-string-properties"></a><span data-ttu-id="ad40e-149">문자열 속성 필터링</span><span class="sxs-lookup"><span data-stu-id="ad40e-149">Filtering on String Properties</span></span>
<span data-ttu-id="ad40e-150">문자열 속성으로 필터링하는 경우 문자열 상수를 작은따옴표로 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="ad40e-150">When you filter on string properties, enclose the string constant in single quotation marks.</span></span>

<span data-ttu-id="ad40e-151">다음의 예제는 **PartitionKey** 및 **RowKey** 속성으로 필터링하며, 추가적으로 키가 아닌 속성도 필터 문자열에 추가될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad40e-151">The following example filters on the **PartitionKey** and **RowKey** properties; additional non-key properties could also be added to the filter string:</span></span>

    PartitionKey eq 'Partition1' and RowKey eq '00001'

<span data-ttu-id="ad40e-152">필수는 아니지만 각 필터 식을 괄호로 묶을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad40e-152">You can enclose each filter expression in parentheses, although it is not required:</span></span>

    (PartitionKey eq 'Partition1') and (RowKey eq '00001')

<span data-ttu-id="ad40e-153">참고로 테이블 서비스는 와일드카드 쿼리를 지원하지 않으며 테이블 디자이너에서도 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ad40e-153">Note that the Table service does not support wildcard queries, and they are not supported in the Table Designer either.</span></span> <span data-ttu-id="ad40e-154">그러나 원하는 접두사에서 비교 연산자를 사용하여 접두사를 일치시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad40e-154">However, you can perform prefix matching by using comparison operators on the desired prefix.</span></span> <span data-ttu-id="ad40e-155">다음의 예제는 문자 ‘A’로 시작하는 LastName 속성을 가진 엔터티를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40e-155">The following example returns entities with a LastName property beginning with the letter 'A':</span></span>

    LastName ge 'A' and LastName lt 'B'

## <a name="filtering-on-numeric-properties"></a><span data-ttu-id="ad40e-156">숫자 속성 필터링</span><span class="sxs-lookup"><span data-stu-id="ad40e-156">Filtering on Numeric Properties</span></span>
<span data-ttu-id="ad40e-157">정수 또는 부동 소수점 숫자를 필터링하려면 따옴표 없이 숫자를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40e-157">To filter on an integer or floating-point number, specify the number without quotation marks.</span></span>

<span data-ttu-id="ad40e-158">이 예제는 값이 30보다 큰 Age 속성을 가진 모든 엔터티를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40e-158">This example returns all entities with an Age property whose value is greater than 30:</span></span>

    Age gt 30

<span data-ttu-id="ad40e-159">이 예제는 값이 100.25보다 작거나 같은 AmountDue 속성을 가진 모든 엔터티를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40e-159">This example returns all entities with an AmountDue property whose value is less than or equal to 100.25:</span></span>

    AmountDue le 100.25

## <a name="filtering-on-boolean-properties"></a><span data-ttu-id="ad40e-160">부울 속성 필터링</span><span class="sxs-lookup"><span data-stu-id="ad40e-160">Filtering on Boolean Properties</span></span>
<span data-ttu-id="ad40e-161">부울 값을 필터링하려면 **true** 또는 **false** 를 인용 부호 없이 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40e-161">To filter on a Boolean value, specify **true** or **false** without quotation marks.</span></span>

<span data-ttu-id="ad40e-162">다음의 예제는 IsActive 속성이 **true**로 설정된 모든 엔터티를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40e-162">The following example returns all entities where the IsActive property is set to **true**:</span></span>

    IsActive eq true

<span data-ttu-id="ad40e-163">논리 연산자 없이도 이 필터 식을 작성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad40e-163">You can also write this filter expression without the logical operator.</span></span> <span data-ttu-id="ad40e-164">다음의 예제에서는 테이블 서비스가 IsActive 속성이 **true**인 모든 엔터티를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40e-164">In the following example, the Table service will also return all entities where IsActive is **true**:</span></span>

    IsActive

<span data-ttu-id="ad40e-165">IsActive가 false인 모든 엔터티를 반환하려면 not 연산자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad40e-165">To return all entities where IsActive is false, you can use the not operator:</span></span>

    not IsActive

## <a name="filtering-on-datetime-properties"></a><span data-ttu-id="ad40e-166">DateTime 속성 필터링</span><span class="sxs-lookup"><span data-stu-id="ad40e-166">Filtering on DateTime Properties</span></span>
<span data-ttu-id="ad40e-167">DateTime 값을 필터링하려면 **datetime** 키워드를 지정하고 그 뒤에 날짜/시간 상수를 작은따옴표 안에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40e-167">To filter on a DateTime value, specify the **datetime** keyword, followed by the date/time constant in single quotation marks.</span></span> <span data-ttu-id="ad40e-168">날짜/시간 상수는 [DateTime 속성 값 형식 지정](http://go.microsoft.com/fwlink/p/?LinkId=400449)에 설명된 것처럼 결합된 UTC 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40e-168">The date/time constant must be in combined UTC format, as described in [Formatting DateTime Property Values](http://go.microsoft.com/fwlink/p/?LinkId=400449).</span></span>

<span data-ttu-id="ad40e-169">다음 예제는 CustomerSince 속성이 2008년 7월 10일과 같은 경우 엔터티를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ad40e-169">The following example returns entities where the CustomerSince property is equal to July 10, 2008:</span></span>

    CustomerSince eq datetime'2008-07-10T00:00:00Z'
