---
title: "로그 분석의 aaaCustom 필드 | Microsoft Docs"
description: "로그 분석의 hello 사용자 정의 필드 기능 toocreate 수 있습니다. 수집 된 레코드의 toohello 속성을 추가 하는 OMS 데이터에서 고유한 검색 가능 필드입니다.  이 문서는 hello 프로세스 toocreate 사용자 지정 필드에 설명 하 고 샘플 이벤트와 자세한 연습을 제공 합니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 31572b51-6b57-4945-8208-ecfc3b5304fc
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: 1aa0e497d5b1d7898b0da6a5ef40f568e63bc589
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="custom-fields-in-log-analytics"></a><span data-ttu-id="94cc4-104">Log Analytics의 사용자 지정 필드</span><span class="sxs-lookup"><span data-stu-id="94cc4-104">Custom fields in Log Analytics</span></span>
<span data-ttu-id="94cc4-105">hello **사용자 정의 필드** 로그 분석의 기능은 hello OMS 리포지토리에 tooextend 기존 레코드 고유한 검색 가능 필드를 추가 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-105">hello **Custom Fields** feature of Log Analytics allows you tooextend existing records in hello OMS repository by adding your own searchable fields.</span></span>  <span data-ttu-id="94cc4-106">Hello 다른 속성에서 추출 된 데이터에서 자동으로 채워진 사용자 지정 필드를 같은 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-106">Custom fields are automatically populated from data extracted from other properties in hello same record.</span></span>

![사용자 지정 필드 개요](media/log-analytics-custom-fields/overview.png)

<span data-ttu-id="94cc4-108">예를 들어 hello 샘플 레코드 아래에 hello 이벤트 설명에 포함 된 유용한 데이터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-108">For example, hello sample record below has useful data buried in hello event description.</span></span>  <span data-ttu-id="94cc4-109">이러한 데이터를 별도의 속성으로 추출하면 정렬 및 필터링 같은 작업에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-109">Extracting this data into separate properties makes it available for such actions as sorting and filtering.</span></span>

![로그 검색 단추](media/log-analytics-custom-fields/sample-extract.png)

> [!NOTE]
> <span data-ttu-id="94cc4-111">Hello 미리 보기, 작업 영역에 사용자 지정 필드 too100 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-111">In hello Preview, you are limited too100 custom fields in your workspace.</span></span>  <span data-ttu-id="94cc4-112">이러한 제한은 이 기능이 일반 공급이 될 때 확장됩니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-112">This limit will be expanded when this feature reaches general availability.</span></span>
> 
> 

## <a name="creating-a-custom-field"></a><span data-ttu-id="94cc4-113">사용자 지정 필드 만들기</span><span class="sxs-lookup"><span data-stu-id="94cc4-113">Creating a custom field</span></span>
<span data-ttu-id="94cc4-114">사용자 지정 필드를 만들 값 로그 분석 데이터 toouse toopopulate 어떤을 이해 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-114">When you create a custom field, Log Analytics must understand which data toouse toopopulate its value.</span></span>  <span data-ttu-id="94cc4-115">기술을 사용 tooquickly FlashExtract 라고 하는 Microsoft Research의이 데이터를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-115">It uses a technology from Microsoft Research called FlashExtract tooquickly identify this data.</span></span>  <span data-ttu-id="94cc4-116">필요 tooprovide 명시적 지침 hello 데이터에 대 한 로그 분석은 알아냅니다 하는 대신 사용자가 제공한 예제에 나오는 tooextract을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-116">Rather than requiring you tooprovide explicit instructions, Log Analytics learns about hello data you want tooextract from examples that you provide.</span></span>

<span data-ttu-id="94cc4-117">다음 섹션 hello 사용자 지정 필드를 만들기 위한 hello 절차를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-117">hello following sections provide hello procedure for creating a custom field.</span></span>  <span data-ttu-id="94cc4-118">이 문서의 맨 hello에 샘플 추출의 연습 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-118">At hello bottom of this article is a walkthrough of a sample extraction.</span></span>

> [!NOTE]
> <span data-ttu-id="94cc4-119">hello 사용자 지정 필드는 일치 하는 hello 레코드 수집 hello 사용자 지정 필드를 만든 후에 나타납니다 조건을 toohello OMS 데이터 저장소에 추가 된 지정 된 레코드로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-119">hello custom field is populated as records matching hello specified criteria are added toohello OMS data store, so it will only appear on records collected after hello custom field is created.</span></span>  <span data-ttu-id="94cc4-120">hello 사용자 지정 필드를 만들 때 hello 데이터 저장소에 이미 있는 toorecords를 추가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-120">hello custom field will not be added toorecords that are already in hello data store when it’s created.</span></span>
> 
> 

### <a name="step-1--identify-records-that-will-have-hello-custom-field"></a><span data-ttu-id="94cc4-121">1 단계 – hello 사용자 지정 필드를 만들 확인 레코드</span><span class="sxs-lookup"><span data-stu-id="94cc4-121">Step 1 – Identify records that will have hello custom field</span></span>
<span data-ttu-id="94cc4-122">hello 첫 번째 단계는 hello 사용자 지정 필드를 얻을 수 있는 tooidentify hello 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-122">hello first step is tooidentify hello records that will get hello custom field.</span></span>  <span data-ttu-id="94cc4-123">로 시작 하는 [표준 로그 검색](log-analytics-log-searches.md) 한 후 로그 분석에서 배웁니다 hello 모델로 레코드 tooact를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-123">You start with a [standard log search](log-analytics-log-searches.md) and then select a record tooact as hello model that Log Analytics will learn from.</span></span>  <span data-ttu-id="94cc4-124">사용자 지정 필드에 tooextract 데이터 것을 지정 하면 hello **필드 추출 마법사** 가 유효성을 검사 하 고 hello 조건을 구체화 열립니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-124">When you specify that you are going tooextract data into a custom field, hello **Field Extraction Wizard** is opened where you validate and refine hello criteria.</span></span>

1. <span data-ttu-id="94cc4-125">너무 이동**로그 검색** 사용 하는 [tooretrieve hello 레코드 쿼리](log-analytics-log-searches.md) hello 사용자 지정 필드를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-125">Go too**Log Search** and use a [query tooretrieve hello records](log-analytics-log-searches.md) that will have hello custom field.</span></span>
2. <span data-ttu-id="94cc4-126">로그 분석으로 사용 하 여 tooact 모델 데이터 toopopulate hello에 대 한 사용자 지정 필드를 추출 하기 위한 레코드를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-126">Select a record that Log Analytics will use tooact as a model for extracting data toopopulate hello custom field.</span></span>  <span data-ttu-id="94cc4-127">이 레코드에서 tooextract 원하는 및 비슷한 모든 레코드에 대 한 로그 분석에서이 정보 toodetermine hello 논리 toopopulate hello 사용자 지정 필드 사용할 hello 데이터를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-127">You will identify hello data that you want tooextract from this record, and Log Analytics will use this information toodetermine hello logic toopopulate hello custom field for all similar records.</span></span>
3. <span data-ttu-id="94cc4-128">Hello 단추 toohello hello 레코드 및 선택의 텍스트 속성 왼쪽 클릭 **에서 필드 추출**합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-128">Click hello button toohello left of any text property of hello record and select **Extract fields from**.</span></span>
4. <span data-ttu-id="94cc4-129">hello **필드 추출 마법사가 열리고**, 선택한 hello 레코드 hello에 표시 되는 **기본 예제** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-129">hello **Field Extraction Wizard is opened**, and hello record you selected is displayed in hello **Main Example** column.</span></span>  <span data-ttu-id="94cc4-130">hello 사용자 지정 필드는 선택 된 hello 속성에 값을 동일한 hello로 해당 레코드에 대해 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-130">hello custom field will be defined for those records with hello same values in hello properties that are selected.</span></span>  
5. <span data-ttu-id="94cc4-131">Hello은 정확히 원하는 작업을 하는 경우 추가 필드 toonarrow hello 기준을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-131">If hello selection is not exactly what you want, select additional fields toonarrow hello criteria.</span></span>  <span data-ttu-id="94cc4-132">Toochange hello 필드 값 hello 조건에 대 한 주문 하 고, 취소 하 고 원하는 hello 조건과 일치 하는 다른 레코드를 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-132">In order toochange hello field values for hello criteria, you must cancel and select a different record matching hello criteria you want.</span></span>

### <a name="step-2---perform-initial-extract"></a><span data-ttu-id="94cc4-133">2단계 - 초기 추출을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-133">Step 2 - Perform initial extract.</span></span>
<span data-ttu-id="94cc4-134">Hello 사용자 지정 필드를 만들 hello 레코드를 식별 했으면 tooextract hello 데이터 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-134">Once you’ve identified hello records that will have hello custom field, you identify hello data that you want tooextract.</span></span>  <span data-ttu-id="94cc4-135">로그 분석 비슷한 레코드에서이 정보 tooidentify 비슷한 패턴을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-135">Log Analytics will use this information tooidentify similar patterns in similar records.</span></span>  <span data-ttu-id="94cc4-136">이후 hello 단계에서 있습니다 수 toovalidate hello 결과 되며 로그 분석 toouse는 분석에 대 한 추가 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-136">In hello step after this you will be able toovalidate hello results and provide further details for Log Analytics toouse in its analysis.</span></span>

1. <span data-ttu-id="94cc4-137">Hello 텍스트 toopopulate hello에 대 한 사용자 지정 필드를 원하는 hello 예제 레코드를 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-137">Highlight hello text in hello sample record that you want toopopulate hello custom field.</span></span>  <span data-ttu-id="94cc4-138">그런 다음 나타납니다 대화 상자 tooprovide와 hello 필드와 tooperform hello 초기 추출에 대 한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-138">You will then be presented with a dialog box tooprovide a name for hello field and tooperform hello initial extract.</span></span>  <span data-ttu-id="94cc4-139">문자 hello  **\_CF** 자동으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-139">hello characters **\_CF** will automatically be appended.</span></span>
2. <span data-ttu-id="94cc4-140">클릭 **추출** tooperform 수집 된 레코드의 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-140">Click **Extract** tooperform an analysis of collected records.</span></span>  
3. <span data-ttu-id="94cc4-141">hello **요약** 및 **검색 결과** 섹션에서는 정확성을 검사할 수 있도록 hello 추출의 hello 결과 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-141">hello **Summary** and **Search Results** sections display hello results of hello extract so you can inspect its accuracy.</span></span>  <span data-ttu-id="94cc4-142">**요약** hello 데이터 식별 된 각 값에 대 한 hello 사용 되는 조건 tooidentify 레코드 및 개수를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-142">**Summary** displays hello criteria used tooidentify records and a count for each of hello data values identified.</span></span>  <span data-ttu-id="94cc4-143">**검색 결과** hello 조건과 일치 하는 레코드의 세부 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-143">**Search Results** provides a detailed list of records matching hello criteria.</span></span>

### <a name="step-3--verify-accuracy-of-hello-extract-and-create-custom-field"></a><span data-ttu-id="94cc4-144">3 단계 – hello 추출의 정확도 확인 하 고, 사용자 지정 필드 만들기</span><span class="sxs-lookup"><span data-stu-id="94cc4-144">Step 3 – Verify accuracy of hello extract and create custom field</span></span>
<span data-ttu-id="94cc4-145">Hello 초기 추출을 수행한 경우 로그 분석은 이미 수집 된 데이터를 기반으로 결과 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-145">Once you have performed hello initial extract, Log Analytics will display its results based on data that has already been collected.</span></span>  <span data-ttu-id="94cc4-146">Hello 결과가 정확한 것 같으면 hello 사용자 지정 필드 추가 작업 없이를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-146">If hello results look accurate then you can create hello custom field with no further work.</span></span>  <span data-ttu-id="94cc4-147">그렇지 않은 경우 다음 로그 분석에서 논리를 향상할 수 있도록 hello 결과 구체화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-147">If not, then you can refine hello results so that Log Analytics can improve its logic.</span></span>

1. <span data-ttu-id="94cc4-148">Hello 클릭 hello 초기 추출의 값이 올바르지 않은 경우 **편집** 아이콘 다음 tooan 부정확 한 레코드 및 선택 **이 하이라이트 수정** 순서 toomodify hello 선택 항목의 합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-148">If any values in hello initial extract aren’t correct, then click hello **Edit** icon next tooan inaccurate record and select **Modify this highlight** in order toomodify hello selection.</span></span>
2. <span data-ttu-id="94cc4-149">hello 항목은 복사한 toohello **추가 예제** hello 아래 섹션 **기본 예제**합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-149">hello entry is copied toohello **Additional examples** section underneath hello **Main Example**.</span></span>  <span data-ttu-id="94cc4-150">Hello 강조를 조정할 수 여기 toohelp 로그 분석 이해 hello 선택 했어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-150">You can adjust hello highlight here toohelp Log Analytics understand hello selection it should have made.</span></span>
3. <span data-ttu-id="94cc4-151">클릭 **추출** toouse 기존 hello 모두이 새 정보 tooevaluate를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-151">Click **Extract** toouse this new information tooevaluate all hello existing records.</span></span>  <span data-ttu-id="94cc4-152">이러한 새 인텔리전스에 따라 수정한 것 하나 hello 이외의 레코드에 대 한 hello 결과 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-152">hello results may be modified for records other than hello one you just modified based on this new intelligence.</span></span>
4. <span data-ttu-id="94cc4-153">Hello 데이터 toopopulate hello 새 사용자 지정 필드를 식별 하는 tooadd 수정 hello에서 모든 레코드를 올바르게 추출 될 때까지 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-153">Continue tooadd corrections until all records in hello extract correctly identify hello data toopopulate hello new custom field.</span></span>
5. <span data-ttu-id="94cc4-154">클릭 **추출 저장** hello 결과 만족 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="94cc4-154">Click **Save Extract** when you are satisfied with hello results.</span></span>  <span data-ttu-id="94cc4-155">사용자 지정 필드 hello 이제 정의 하지만 추가 되지 않았습니다 tooany 레코드 아직.</span><span class="sxs-lookup"><span data-stu-id="94cc4-155">hello custom field is now defined, but it won’t be added tooany records yet.</span></span>
6. <span data-ttu-id="94cc4-156">새 레코드를 일치 하는 hello 지정 조건 toobe 수집 하 고 다음 hello 로그 검색을 다시 실행 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-156">Wait for new records matching hello specified criteria toobe collected and then run hello log search again.</span></span> <span data-ttu-id="94cc4-157">새 레코드에는 hello 사용자 지정 필드가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-157">New records should have hello custom field.</span></span>
7. <span data-ttu-id="94cc4-158">다른 레코드 속성 처럼 사용자 정의 필드 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-158">Use hello custom field like any other record property.</span></span>  <span data-ttu-id="94cc4-159">Tooaggregate 정보와 그룹 데이터를 사용할 수 있으며 새로운 통찰력 tooproduce 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-159">You can use it tooaggregate and group data and even use it tooproduce new insights.</span></span>

## <a name="viewing-custom-fields"></a><span data-ttu-id="94cc4-160">사용자 지정 필드 보기</span><span class="sxs-lookup"><span data-stu-id="94cc4-160">Viewing custom fields</span></span>
<span data-ttu-id="94cc4-161">Hello에서 관리 그룹의 모든 사용자 필드 목록을 볼 수 있습니다 **설정을** hello OMS 대시보드의 타일입니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-161">You can view a list of all custom fields in your management group from hello **Settings** tile of hello OMS dashboard.</span></span>  <span data-ttu-id="94cc4-162">**데이터**를 선택한 다음 **사용자 지정 필드**를 선택하여 작업 영역 내 모든 사용자 지정 필드의 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-162">Select **Data** and then **Custom fields** for a list of all custom fields in your workspace.</span></span>  

![사용자 지정 필드](media/log-analytics-custom-fields/list.png)

## <a name="removing-a-custom-field"></a><span data-ttu-id="94cc4-164">사용자 지정 필드 제거</span><span class="sxs-lookup"><span data-stu-id="94cc4-164">Removing a custom field</span></span>
<span data-ttu-id="94cc4-165">사용자 지정 필드는 두 가지 방법으로 tooremove 합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-165">There are two ways tooremove a custom field.</span></span>  <span data-ttu-id="94cc4-166">먼저는 hello hello **제거** 위에서 설명한 것 처럼 hello 전체 목록을 볼 때 각 필드에 대 한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-166">hello first is hello **Remove** option for each field when viewing hello complete list as described above.</span></span>  <span data-ttu-id="94cc4-167">hello 다른 메서드는 레코드 및 클릭 hello 단추 toohello hello 필드의 왼쪽 tooretrieve 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-167">hello other method is tooretrieve a record and click hello button toohello left of hello field.</span></span>  <span data-ttu-id="94cc4-168">hello 메뉴 옵션 tooremove hello 사용자 지정 필드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-168">hello menu will have an option tooremove hello custom field.</span></span>

## <a name="sample-walkthrough"></a><span data-ttu-id="94cc4-169">샘플 연습</span><span class="sxs-lookup"><span data-stu-id="94cc4-169">Sample walkthrough</span></span>
<span data-ttu-id="94cc4-170">hello 다음 섹션 안내는 전체 예제는 사용자 지정 필드 만들기.</span><span class="sxs-lookup"><span data-stu-id="94cc4-170">hello following section walks through a complete example of creating a custom field.</span></span>  <span data-ttu-id="94cc4-171">이 예제에서는 서비스 변경 상태를 나타내는 Windows 이벤트의 hello 서비스 이름을 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-171">This example extracts hello service name in Windows events that indicate a service changing state.</span></span>  <span data-ttu-id="94cc4-172">이 예제에서는 서비스 제어 관리자에서 Windows 컴퓨터에서 hello 시스템 로그에 생성 된 이벤트에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-172">This relies on events created by Service Control Manager in hello System log on Windows computers.</span></span>  <span data-ttu-id="94cc4-173">이 예에서는 toofollow 원하는 상태 여야 [hello 시스템 로그에 대 한 정보 이벤트를 수집](log-analytics-data-sources-windows-events.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-173">If you want toofollow this example, you must be [collecting Information events for hello System log](log-analytics-data-sources-windows-events.md).</span></span>

<span data-ttu-id="94cc4-174">에서는 입력 쿼리 tooreturn 다음 hello 모든 이벤트 서비스 제어 관리자에서 이벤트 id 7036이 있는 hello 이벤트 서비스 시작 또는 중지를 나타내는입니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-174">We enter hello following query tooreturn all events from Service Control Manager that have an Event ID of 7036 which is hello event that indicates a service starting or stopping.</span></span>

![쿼리](media/log-analytics-custom-fields/query.png)

<span data-ttu-id="94cc4-176">그 다음 이벤트 ID가 7036인 레코드를 아무 레코드나 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-176">We then select any record with event ID 7036.</span></span>

![소스 레코드](media/log-analytics-custom-fields/source-record.png)

<span data-ttu-id="94cc4-178">Hello에 표시 되는 hello 서비스 이름을 원하는 **RenderedDescription** 속성과 선택 hello 단추 다음 toothis 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-178">We want hello service name that appears in hello **RenderedDescription** property and select hello button next toothis property.</span></span>

![추출 필드](media/log-analytics-custom-fields/extract-fields.png)

<span data-ttu-id="94cc4-180">hello **필드 추출 마법사** 열리며 hello **EventLog** 및 **EventID** hello에서 필드가 선택 되어 **기본 예제** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-180">hello **Field Extraction Wizard** is opened, and hello **EventLog** and **EventID** fields are selected in hello **Main Example** column.</span></span>  <span data-ttu-id="94cc4-181">이 해당 hello 사용자 지정 필드 hello 이벤트 ID 7036이 있는 시스템 로그의 이벤트에 대해 정의 됨을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-181">This indicates that hello custom field will be defined for events from hello System log with an event ID of 7036.</span></span>  <span data-ttu-id="94cc4-182">이것으로 충분 하므로 다른 필드 tooselect 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-182">This is sufficient so we don’t need tooselect any other fields.</span></span>

![Main Example](media/log-analytics-custom-fields/main-example.png)

<span data-ttu-id="94cc4-184">Hello hello에 hello 서비스 이름을 강조 해 서 **RenderedDescription** 속성 및 사용 **서비스** tooidentify hello 서비스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-184">We highlight hello name of hello service in hello **RenderedDescription** property and use **Service** tooidentify hello service name.</span></span>  <span data-ttu-id="94cc4-185">hello 사용자 지정 필드를 호출할지 **Service_CF**합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-185">hello custom field will be called **Service_CF**.</span></span>

![필드 제목](media/log-analytics-custom-fields/field-title.png)

<span data-ttu-id="94cc4-187">Hello 서비스 이름이 일부 레코드에 대 한 하지만만 적절 하 게 식별 되는 것이 보면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-187">We see that hello service name is identified properly for some records but not for others.</span></span>   <span data-ttu-id="94cc4-188">hello **검색 결과** hello에 대 한 hello 이름의 일부가 표시 **WMI Performance Adapter** 선택 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-188">hello **Search Results** show that part of hello name for hello **WMI Performance Adapter** wasn’t selected.</span></span>  <span data-ttu-id="94cc4-189">hello **요약** 갖는 레코드 4 표시 **DPRMA** 서비스 잘못 포함 여분의 단어 및 식별 하는 두 개의 레코드 **모듈 설치 관리자** 대신**Windows 모듈 설치 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-189">hello **Summary** shows that four records with **DPRMA** service incorrectly included an extra word, and two records identified **Modules Installer** instead of **Windows Modules Installer**.</span></span>  

![검색 결과](media/log-analytics-custom-fields/search-results-01.png)

<span data-ttu-id="94cc4-191">Hello로 시작 **WMI Performance Adapter** 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-191">We start with hello **WMI Performance Adapter** record.</span></span>  <span data-ttu-id="94cc4-192">편집 아이콘을 클릭한 다음 **Modify this highlight**(이 강조 표시 수정)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-192">We click its edit icon and then **Modify this highlight**.</span></span>  

![강조 표시 수정](media/log-analytics-custom-fields/modify-highlight.png)

<span data-ttu-id="94cc4-194">Hello 강조 tooinclude hello 단어 늘려 **WMI** 다음 hello 추출 다시 실행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="94cc4-194">We increase    hello highlight tooinclude hello word **WMI** and then rerun hello extract.</span></span>  

![추가 예제](media/log-analytics-custom-fields/additional-example-01.png)

<span data-ttu-id="94cc4-196">해당 hello 볼 수 있습니다에 대 한 항목 **WMI Performance Adapter** 수정 되었으며, 로그 분석이 해당 정보 toocorrect hello 레코드에 대 한 사용 **Windows 모듈 설치 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-196">We can see that hello entries for **WMI Performance Adapter** have been corrected, and Log Analytics also used that information toocorrect hello records for **Windows Module Installer**.</span></span>  <span data-ttu-id="94cc4-197">Hello에서 볼 수 **요약** 섹션 하지만 **DPMRA** 가 아직 올바르게 식별 되지 합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-197">We can see in hello **Summary** section though that **DPMRA** is still not being identified correctly.</span></span>

![검색 결과](media/log-analytics-custom-fields/search-results-02.png)

<span data-ttu-id="94cc4-199">DPMRA 서비스 hello로 tooa 레코드 스크롤하여 동일한 프로세스를 기록 하는 toocorrect hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-199">We scroll tooa record with hello DPMRA service and use hello same process toocorrect that record.</span></span>

![추가 예제](media/log-analytics-custom-fields/additional-example-02.png)

 <span data-ttu-id="94cc4-201">Hello 추출을 실행 하면 모든 결과가 내용이 올바르면 이제 았습니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-201">When we run hello extraction, we can see that all of our results are now accurate.</span></span>

![검색 결과](media/log-analytics-custom-fields/search-results-03.png)

<span data-ttu-id="94cc4-203">볼 수 있습니다 **Service_CF** 만들어지지만 tooany 레코드 아직 추가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-203">We can see that **Service_CF** is created but is not yet added tooany records.</span></span>

![초기 개수](media/log-analytics-custom-fields/initial-count.png)

<span data-ttu-id="94cc4-205">New 약간의 시간이 지난 후 이벤트를 수집할지, hello를 볼 수 있습니다 **Service_CF** 필드가 toorecords 우리의 조건과 일치 하는 추가 이제 합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-205">After some time has passed so new events are collected, we can see that that hello **Service_CF** field is now being added toorecords that match our criteria.</span></span>

![최종 결과](media/log-analytics-custom-fields/final-results.png)

<span data-ttu-id="94cc4-207">이제 다른 레코드 속성과 같이 hello 사용자 지정 필드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-207">We can now use hello custom field like any other record property.</span></span>  <span data-ttu-id="94cc4-208">tooillustrate이 새 hello 별로 그룹화 되는 쿼리를 작성 **Service_CF** 필드 tooinspect hello 가장 많이 실행 되는 서비스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-208">tooillustrate this, we create a query that groups by hello new **Service_CF** field tooinspect which services are hello most active.</span></span>

![쿼리로 그룹화](media/log-analytics-custom-fields/query-group.png)

## <a name="next-steps"></a><span data-ttu-id="94cc4-210">다음 단계</span><span class="sxs-lookup"><span data-stu-id="94cc4-210">Next steps</span></span>
* <span data-ttu-id="94cc4-211">에 대 한 자세한 내용은 [검색 로그](log-analytics-log-searches.md) toobuild 쿼리 조건에 대 한 사용자 지정 필드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-211">Learn about [log searches](log-analytics-log-searches.md) toobuild queries using custom fields for criteria.</span></span>
* <span data-ttu-id="94cc4-212">사용자 지정 필드를 사용하여 구문 분석하는 [사용자 지정 로그 파일](log-analytics-data-sources-custom-logs.md)을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="94cc4-212">Monitor [custom log files](log-analytics-data-sources-custom-logs.md) that you parse using custom fields.</span></span>

