---
title: "hello 테이블 디자이너에 대 한 필터 문자열 aaaConstructing | Microsoft Docs"
description: "Hello 테이블 디자이너에 대 한 필터 문자열 생성"
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
ms.openlocfilehash: 48b38d27b97936064daa875e41881d51546bc11f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="constructing-filter-strings-for-hello-table-designer"></a><span data-ttu-id="0c371-103">테이블 디자이너 hello에 대 한 필터 문자열 생성</span><span class="sxs-lookup"><span data-stu-id="0c371-103">Constructing Filter Strings for hello Table Designer</span></span>
## <a name="overview"></a><span data-ttu-id="0c371-104">개요</span><span class="sxs-lookup"><span data-stu-id="0c371-104">Overview</span></span>
<span data-ttu-id="0c371-105">에 표시 되는 Azure 테이블의 데이터를 toofilter hello Visual Studio **테이블 디자이너**, 필터 문자열을 생성 하 고 hello 필터 필드에 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c371-105">toofilter data in an Azure table that is displayed in hello Visual Studio **Table Designer**, you construct a filter string and enter it into hello filter field.</span></span> <span data-ttu-id="0c371-106">hello 필터 문자열 구문은 hello WCF 데이터 서비스에 의해 정의 됩니다 및 유사한 tooa SQL WHERE 절, 하지만 toohello HTTP 요청을 통해 테이블 서비스로 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c371-106">hello filter string syntax is defined by hello WCF Data Services and is similar tooa SQL WHERE clause, but is sent toohello Table service via an HTTP request.</span></span> <span data-ttu-id="0c371-107">hello **테이블 디자이너** 핸들 적합 한 인코딩을, 원하는 속성 값에 따라서 toofilter hello, hello 속성 이름, 비교 연산자, 조건 값을 입력만 필요 하 고 hello의 부울 연산자 필터링 하는 필요에 따라 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="0c371-107">hello **Table Designer** handles hello proper encoding for you, so toofilter on a desired property value, you need only enter hello property name, comparison operator, criteria value, and optionally, Boolean operator in hello filter field.</span></span> <span data-ttu-id="0c371-108">Hello 통해 URL tooquery hello 테이블을 생성 하는 경우와 마찬가지로 tooinclude hello $filter 쿼리 옵션 불필요 [저장소 서비스 REST API 참조](http://go.microsoft.com/fwlink/p/?LinkId=400447)합니다.</span><span class="sxs-lookup"><span data-stu-id="0c371-108">You do not need tooinclude hello $filter query option as you would if you were constructing a URL tooquery hello table via hello [Storage Services REST API Reference](http://go.microsoft.com/fwlink/p/?LinkId=400447).</span></span>

<span data-ttu-id="0c371-109">hello WCF Data Services 기반 hello로 [개방형 데이터 프로토콜](http://go.microsoft.com/fwlink/p/?LinkId=214805) (OData).</span><span class="sxs-lookup"><span data-stu-id="0c371-109">hello WCF Data Services are based on hello [Open Data Protocol](http://go.microsoft.com/fwlink/p/?LinkId=214805) (OData).</span></span> <span data-ttu-id="0c371-110">Hello 필터 시스템 쿼리 옵션에 대 한 자세한 내용은 (**$filter**), 참조 hello [OData URI 규칙 사양](http://go.microsoft.com/fwlink/p/?LinkId=214806)합니다.</span><span class="sxs-lookup"><span data-stu-id="0c371-110">For details on hello filter system query option (**$filter**), see hello [OData URI Conventions specification](http://go.microsoft.com/fwlink/p/?LinkId=214806).</span></span>

## <a name="comparison-operators"></a><span data-ttu-id="0c371-111">비교 연산자</span><span class="sxs-lookup"><span data-stu-id="0c371-111">Comparison Operators</span></span>
<span data-ttu-id="0c371-112">hello 다음과 같은 논리 연산자는 모든 유형에 대해 지원 속성:</span><span class="sxs-lookup"><span data-stu-id="0c371-112">hello following logical operators are supported for all property types:</span></span>

| <span data-ttu-id="0c371-113">논리 연산자</span><span class="sxs-lookup"><span data-stu-id="0c371-113">Logical operator</span></span> | <span data-ttu-id="0c371-114">설명</span><span class="sxs-lookup"><span data-stu-id="0c371-114">Description</span></span> | <span data-ttu-id="0c371-115">필터 문자열의 예</span><span class="sxs-lookup"><span data-stu-id="0c371-115">Example filter string</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0c371-116">eq</span><span class="sxs-lookup"><span data-stu-id="0c371-116">eq</span></span> |<span data-ttu-id="0c371-117">같음</span><span class="sxs-lookup"><span data-stu-id="0c371-117">Equal</span></span> |<span data-ttu-id="0c371-118">'Redmond'와 같은 도시</span><span class="sxs-lookup"><span data-stu-id="0c371-118">City eq 'Redmond'</span></span> |
| <span data-ttu-id="0c371-119">gt</span><span class="sxs-lookup"><span data-stu-id="0c371-119">gt</span></span> |<span data-ttu-id="0c371-120">다음보다 큼</span><span class="sxs-lookup"><span data-stu-id="0c371-120">Greater than</span></span> |<span data-ttu-id="0c371-121">20보다 큰 가격</span><span class="sxs-lookup"><span data-stu-id="0c371-121">Price gt 20</span></span> |
| <span data-ttu-id="0c371-122">ge</span><span class="sxs-lookup"><span data-stu-id="0c371-122">ge</span></span> |<span data-ttu-id="0c371-123">보다 크거나 같은 너무</span><span class="sxs-lookup"><span data-stu-id="0c371-123">Greater than or equal too</span></span>|<span data-ttu-id="0c371-124">10보다 크거나 같은 가격</span><span class="sxs-lookup"><span data-stu-id="0c371-124">Price ge 10</span></span> |
| <span data-ttu-id="0c371-125">lt</span><span class="sxs-lookup"><span data-stu-id="0c371-125">lt</span></span> |<span data-ttu-id="0c371-126">다음보다 적음</span><span class="sxs-lookup"><span data-stu-id="0c371-126">Less than</span></span> |<span data-ttu-id="0c371-127">20보다 적은 가격</span><span class="sxs-lookup"><span data-stu-id="0c371-127">Price lt 20</span></span> |
| <span data-ttu-id="0c371-128">le</span><span class="sxs-lookup"><span data-stu-id="0c371-128">le</span></span> |<span data-ttu-id="0c371-129">다음보다 적거나 같음</span><span class="sxs-lookup"><span data-stu-id="0c371-129">Less than or equal</span></span> |<span data-ttu-id="0c371-130">100보다 적거나 같은 가격</span><span class="sxs-lookup"><span data-stu-id="0c371-130">Price le 100</span></span> |
| <span data-ttu-id="0c371-131">ne</span><span class="sxs-lookup"><span data-stu-id="0c371-131">ne</span></span> |<span data-ttu-id="0c371-132">다음과 같지 않음</span><span class="sxs-lookup"><span data-stu-id="0c371-132">Not equal</span></span> |<span data-ttu-id="0c371-133">'London'과 같지 않은 도시</span><span class="sxs-lookup"><span data-stu-id="0c371-133">City ne 'London'</span></span> |
| <span data-ttu-id="0c371-134">and</span><span class="sxs-lookup"><span data-stu-id="0c371-134">and</span></span> |<span data-ttu-id="0c371-135">and</span><span class="sxs-lookup"><span data-stu-id="0c371-135">And</span></span> |<span data-ttu-id="0c371-136">200보다 적거나 같은 가격 및 3.5보다 큰 가격</span><span class="sxs-lookup"><span data-stu-id="0c371-136">Price le 200 and Price gt 3.5</span></span> |
| <span data-ttu-id="0c371-137">또는</span><span class="sxs-lookup"><span data-stu-id="0c371-137">or</span></span> |<span data-ttu-id="0c371-138">또는</span><span class="sxs-lookup"><span data-stu-id="0c371-138">Or</span></span> |<span data-ttu-id="0c371-139">3.5보다 적거나 같은 가격 또는 200보다 큰 가격</span><span class="sxs-lookup"><span data-stu-id="0c371-139">Price le 3.5 or Price gt 200</span></span> |
| <span data-ttu-id="0c371-140">not</span><span class="sxs-lookup"><span data-stu-id="0c371-140">not</span></span> |<span data-ttu-id="0c371-141">not</span><span class="sxs-lookup"><span data-stu-id="0c371-141">Not</span></span> |<span data-ttu-id="0c371-142">not isAvailable</span><span class="sxs-lookup"><span data-stu-id="0c371-142">not isAvailable</span></span> |

<span data-ttu-id="0c371-143">필터 문자열을 생성할 때는 hello 다음 규칙은 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c371-143">When constructing a filter string, hello following rules are important:</span></span>

* <span data-ttu-id="0c371-144">Hello 논리 연산자 toocompare 속성 tooa 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c371-144">Use hello logical operators toocompare a property tooa value.</span></span> <span data-ttu-id="0c371-145">가능한 toocompare 속성 tooa 동적 값; 아닌지 참고 hello 식의 한 쪽은 상수 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c371-145">Note that it is not possible toocompare a property tooa dynamic value; one side of hello expression must be a constant.</span></span>
* <span data-ttu-id="0c371-146">Hello 필터 문자열의 모든 부분은 대/소문자를 구분 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0c371-146">All parts of hello filter string are case-sensitive.</span></span>
* <span data-ttu-id="0c371-147">hello hello 상수 값 이어야 합니다 hello 필터 tooreturn 유효한 결과에서 hello 속성으로 동일한 데이터 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="0c371-147">hello constant value must be of hello same data type as hello property in order for hello filter tooreturn valid results.</span></span> <span data-ttu-id="0c371-148">지원 되는 속성 형식에 대 한 자세한 내용은 참조 [테이블 서비스 데이터 모델 이해 hello](http://go.microsoft.com/fwlink/p/?LinkId=400448)합니다.</span><span class="sxs-lookup"><span data-stu-id="0c371-148">For more information about supported property types, see [Understanding hello Table Service Data Model](http://go.microsoft.com/fwlink/p/?LinkId=400448).</span></span>

## <a name="filtering-on-string-properties"></a><span data-ttu-id="0c371-149">문자열 속성 필터링</span><span class="sxs-lookup"><span data-stu-id="0c371-149">Filtering on String Properties</span></span>
<span data-ttu-id="0c371-150">문자열 속성으로 필터링 할 때 hello 문자열 상수가 작은따옴표로 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="0c371-150">When you filter on string properties, enclose hello string constant in single quotation marks.</span></span>

<span data-ttu-id="0c371-151">에 나오는 예제에서는 필터에 따라 hello hello **PartitionKey** 및 **RowKey** ; 키가 아닌 추가 속성 속성 toohello 필터 문자열 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c371-151">hello following example filters on hello **PartitionKey** and **RowKey** properties; additional non-key properties could also be added toohello filter string:</span></span>

    PartitionKey eq 'Partition1' and RowKey eq '00001'

<span data-ttu-id="0c371-152">필수는 아니지만 각 필터 식을 괄호로 묶을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c371-152">You can enclose each filter expression in parentheses, although it is not required:</span></span>

    (PartitionKey eq 'Partition1') and (RowKey eq '00001')

<span data-ttu-id="0c371-153">테이블 서비스 hello 와일드 카드 쿼리를 지원 하지 않습니다 및 지원 되지 않습니다 hello 테이블 디자이너에서에서 하거나 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c371-153">Note that hello Table service does not support wildcard queries, and they are not supported in hello Table Designer either.</span></span> <span data-ttu-id="0c371-154">그러나 원하는 접두사 hello에 비교 연산자를 사용 하 여 접두사 일치를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c371-154">However, you can perform prefix matching by using comparison operators on hello desired prefix.</span></span> <span data-ttu-id="0c371-155">hello 다음 예제에서는 엔터티를 반환 합니다 hello 문자 'A'로 시작 하는 LastName 속성:</span><span class="sxs-lookup"><span data-stu-id="0c371-155">hello following example returns entities with a LastName property beginning with hello letter 'A':</span></span>

    LastName ge 'A' and LastName lt 'B'

## <a name="filtering-on-numeric-properties"></a><span data-ttu-id="0c371-156">숫자 속성 필터링</span><span class="sxs-lookup"><span data-stu-id="0c371-156">Filtering on Numeric Properties</span></span>
<span data-ttu-id="0c371-157">정수 또는 부동 소수점 숫자 toofilter 따옴표 없이 hello 번호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c371-157">toofilter on an integer or floating-point number, specify hello number without quotation marks.</span></span>

<span data-ttu-id="0c371-158">이 예제는 값이 30보다 큰 Age 속성을 가진 모든 엔터티를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0c371-158">This example returns all entities with an Age property whose value is greater than 30:</span></span>

    Age gt 30

<span data-ttu-id="0c371-159">같은 AmountDue 속성 값이 포함 된 모든 엔터티를 반환 하는이 예제 보다 작거나 같은 too100.25:</span><span class="sxs-lookup"><span data-stu-id="0c371-159">This example returns all entities with an AmountDue property whose value is less than or equal too100.25:</span></span>

    AmountDue le 100.25

## <a name="filtering-on-boolean-properties"></a><span data-ttu-id="0c371-160">부울 속성 필터링</span><span class="sxs-lookup"><span data-stu-id="0c371-160">Filtering on Boolean Properties</span></span>
<span data-ttu-id="0c371-161">부울 값에 toofilter 지정 **true** 또는 **false** 인용 부호 제외 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c371-161">toofilter on a Boolean value, specify **true** or **false** without quotation marks.</span></span>

<span data-ttu-id="0c371-162">hello 다음 예제에서는 반환 모든 엔터티가 너무 hello IsActive 속성이 설정 되어 있는**true**:</span><span class="sxs-lookup"><span data-stu-id="0c371-162">hello following example returns all entities where hello IsActive property is set too**true**:</span></span>

    IsActive eq true

<span data-ttu-id="0c371-163">Hello 논리 연산자 없이이 필터 식을 작성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c371-163">You can also write this filter expression without hello logical operator.</span></span> <span data-ttu-id="0c371-164">다음 예제는 hello, hello 테이블 서비스는 모든 엔터티도 반환 IsActive가 **true**:</span><span class="sxs-lookup"><span data-stu-id="0c371-164">In hello following example, hello Table service will also return all entities where IsActive is **true**:</span></span>

    IsActive

<span data-ttu-id="0c371-165">모든 엔터티 IsActive가 false 이면 사용할 수 없습니다 hello tooreturn 연산자:</span><span class="sxs-lookup"><span data-stu-id="0c371-165">tooreturn all entities where IsActive is false, you can use hello not operator:</span></span>

    not IsActive

## <a name="filtering-on-datetime-properties"></a><span data-ttu-id="0c371-166">DateTime 속성 필터링</span><span class="sxs-lookup"><span data-stu-id="0c371-166">Filtering on DateTime Properties</span></span>
<span data-ttu-id="0c371-167">날짜/시간 값에 toofilter 지정 hello **datetime** 키워드와 작은따옴표로 hello date/time 상수입니다.</span><span class="sxs-lookup"><span data-stu-id="0c371-167">toofilter on a DateTime value, specify hello **datetime** keyword, followed by hello date/time constant in single quotation marks.</span></span> <span data-ttu-id="0c371-168">에 설명 된 대로 hello date/time 상수 결합 된 UTC 형식에서 이어야 합니다 [DateTime 속성 값 서식 지정](http://go.microsoft.com/fwlink/p/?LinkId=400449)합니다.</span><span class="sxs-lookup"><span data-stu-id="0c371-168">hello date/time constant must be in combined UTC format, as described in [Formatting DateTime Property Values](http://go.microsoft.com/fwlink/p/?LinkId=400449).</span></span>

<span data-ttu-id="0c371-169">다음 예에서는 hello 여기서 hello CustomerSince 속성은 같은 tooJuly 10, 2008 엔터티를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c371-169">hello following example returns entities where hello CustomerSince property is equal tooJuly 10, 2008:</span></span>

    CustomerSince eq datetime'2008-07-10T00:00:00Z'
