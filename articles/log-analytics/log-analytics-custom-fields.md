---
title: "Log Analytics의 사용자 지정 필드 | Microsoft Docs"
description: "Log Analytics의 사용자 지정 필드를 사용하면 수집된 레코드의 속성에 추가되는 OMS 데이터를 통해 자체 검색 가능한 필드를 만들 수 있습니다.  이 문서는 사용자 지정 필드를 만드는 프로세스를 설명하고 샘플 이벤트에 대한 자세한 연습을 제공합니다."
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
ms.openlocfilehash: 9e02094f155eaade9bc5fb49c4fbb798e546e989
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="custom-fields-in-log-analytics"></a><span data-ttu-id="b63cd-104">Log Analytics의 사용자 지정 필드</span><span class="sxs-lookup"><span data-stu-id="b63cd-104">Custom fields in Log Analytics</span></span>
<span data-ttu-id="b63cd-105">Log Analytics의 **사용자 지정 필드** 기능을 사용하면 자체적으로 검색 가능한 필드를 추가하여 OMS 리포지토리의 기존 레코드를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-105">The **Custom Fields** feature of Log Analytics allows you to extend existing records in the OMS repository by adding your own searchable fields.</span></span>  <span data-ttu-id="b63cd-106">사용자 지정 필드는 동일한 레코드의 다른 속성에서 추출한 데이터로 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-106">Custom fields are automatically populated from data extracted from other properties in the same record.</span></span>

![사용자 지정 필드 개요](media/log-analytics-custom-fields/overview.png)

<span data-ttu-id="b63cd-108">예를 들어, 아래 샘플 레코드에는 이벤트 설명에 파묻혀 있는 유용한 데이터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-108">For example, the sample record below has useful data buried in the event description.</span></span>  <span data-ttu-id="b63cd-109">이러한 데이터를 별도의 속성으로 추출하면 정렬 및 필터링 같은 작업에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-109">Extracting this data into separate properties makes it available for such actions as sorting and filtering.</span></span>

![로그 검색 단추](media/log-analytics-custom-fields/sample-extract.png)

> [!NOTE]
> <span data-ttu-id="b63cd-111">미리 보기에서는 작업 영역 내 사용자 지정 필드가 100개로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-111">In the Preview, you are limited to 100 custom fields in your workspace.</span></span>  <span data-ttu-id="b63cd-112">이러한 제한은 이 기능이 일반 공급이 될 때 확장됩니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-112">This limit will be expanded when this feature reaches general availability.</span></span>
> 
> 

## <a name="creating-a-custom-field"></a><span data-ttu-id="b63cd-113">사용자 지정 필드 만들기</span><span class="sxs-lookup"><span data-stu-id="b63cd-113">Creating a custom field</span></span>
<span data-ttu-id="b63cd-114">사용자 지정 필드를 만드는 경우, Log Analytics는 값을 채우는 데 사용할 데이터를 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-114">When you create a custom field, Log Analytics must understand which data to use to populate its value.</span></span>  <span data-ttu-id="b63cd-115">Microsoft Research의 FlashExtract라는 기술을 사용하여 이러한 데이터를 신속하게 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-115">It uses a technology from Microsoft Research called FlashExtract to quickly identify this data.</span></span>  <span data-ttu-id="b63cd-116">Log Analytics는 명시적인 지침을 제공하도록 요구하지 않고, 사용자가 제공하는 예제에서 추출할 데이터에 대해 알아냅니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-116">Rather than requiring you to provide explicit instructions, Log Analytics learns about the data you want to extract from examples that you provide.</span></span>

<span data-ttu-id="b63cd-117">다음 섹션은 사용자 지정 필드를 만드는 절차를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-117">The following sections provide the procedure for creating a custom field.</span></span>  <span data-ttu-id="b63cd-118">이 문서의 맨 아래에 샘플 추출 연습이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-118">At the bottom of this article is a walkthrough of a sample extraction.</span></span>

> [!NOTE]
> <span data-ttu-id="b63cd-119">사용자 지정 필드는 특정 조건에 일치하는 레코드가 OMS 데이터 저장소에 추가되면 채워지기 때문에, 사용자 지정 필드가 생성된 후에 수집된 레코드에만 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-119">The custom field is populated as records matching the specified criteria are added to the OMS data store, so it will only appear on records collected after the custom field is created.</span></span>  <span data-ttu-id="b63cd-120">사용자 지정 필드는 생성 당시 데이터 저장소에 이미 있었던 레코드에는 추가되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-120">The custom field will not be added to records that are already in the data store when it’s created.</span></span>
> 
> 

### <a name="step-1--identify-records-that-will-have-the-custom-field"></a><span data-ttu-id="b63cd-121">1단계 – 사용자 지정 필드를 갖게 될 레코드를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-121">Step 1 – Identify records that will have the custom field</span></span>
<span data-ttu-id="b63cd-122">첫 번째 단계는 사용자 지정 필드를 갖게 될 레코드를 식별하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-122">The first step is to identify the records that will get the custom field.</span></span>  <span data-ttu-id="b63cd-123">[표준 로그 검색](log-analytics-log-searches.md) 부터 시작한 다음 Log Analytics가 학습하는 모델 역할을 할 레코드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-123">You start with a [standard log search](log-analytics-log-searches.md) and then select a record to act as the model that Log Analytics will learn from.</span></span>  <span data-ttu-id="b63cd-124">사용자 지정 필드에 데이터를 추출할 것이라고 지정하면, **Field Extraction Wizard** (필드 추출 마법사)가 열리고 여기서 조건의 유효성을 검사하고 구체화합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-124">When you specify that you are going to extract data into a custom field, the **Field Extraction Wizard** is opened where you validate and refine the criteria.</span></span>

1. <span data-ttu-id="b63cd-125">**로그 검색** 으로 이동하고 사용자 지정 필드를 갖게 될 [레코드를 검색할 쿼리](log-analytics-log-searches.md) 를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-125">Go to **Log Search** and use a [query to retrieve the records](log-analytics-log-searches.md) that will have the custom field.</span></span>
2. <span data-ttu-id="b63cd-126">Log Analytics가 사용자 지정 필드를 채울 데이터 추출을 위한 모델 역할을 하기 위해서 사용할 레코드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-126">Select a record that Log Analytics will use to act as a model for extracting data to populate the custom field.</span></span>  <span data-ttu-id="b63cd-127">사용자는 이 레코드로부터 추출할 데이터를 식별하고, Log Analytics는 이 정보를 사용하여 유사한 모든 레코드의 사용자 지정 필드를 채울 논리를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-127">You will identify the data that you want to extract from this record, and Log Analytics will use this information to determine the logic to populate the custom field for all similar records.</span></span>
3. <span data-ttu-id="b63cd-128">레코드 텍스트 속성 왼쪽의 단추를 클릭하고 **Extract fields from**(다음에서 필드 추출)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-128">Click the button to the left of any text property of the record and select **Extract fields from**.</span></span>
4. <span data-ttu-id="b63cd-129">**Field Extraction Wizard(필드 추출 마법사)가 열리고**, 선택한 레코드가 **Main Example**(기본 예제) 열에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-129">The **Field Extraction Wizard is opened**, and the record you selected is displayed in the **Main Example** column.</span></span>  <span data-ttu-id="b63cd-130">사용자 지정 필드가, 선택한 속성에 동일한 값을 포함하는 레코드에 대해 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-130">The custom field will be defined for those records with the same values in the properties that are selected.</span></span>  
5. <span data-ttu-id="b63cd-131">선택 내용이 정확히 원하는 내용이 아니면, 추가적인 필드를 선택하여 조건을 좁혀 나갑니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-131">If the selection is not exactly what you want, select additional fields to narrow the criteria.</span></span>  <span data-ttu-id="b63cd-132">조건에 대한 필드 값을 변경하기 위해서, 취소하고 원하는 조건에 맞는 다른 레코드를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-132">In order to change the field values for the criteria, you must cancel and select a different record matching the criteria you want.</span></span>

### <a name="step-2---perform-initial-extract"></a><span data-ttu-id="b63cd-133">2단계 - 초기 추출을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-133">Step 2 - Perform initial extract.</span></span>
<span data-ttu-id="b63cd-134">사용자 지정 필드를 갖게 될 레코드를 식별하고 나면, 추출할 데이터를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-134">Once you’ve identified the records that will have the custom field, you identify the data that you want to extract.</span></span>  <span data-ttu-id="b63cd-135">Log Analytics는 이 정보를 사용하여 비슷한 레코드에서 유사한 패턴을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-135">Log Analytics will use this information to identify similar patterns in similar records.</span></span>  <span data-ttu-id="b63cd-136">이 단계가 지나면 결과의 유효성을 검사하고 분석에 사용할 Log Analytics에 대한 자세한 정보를 제공할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-136">In the step after this you will be able to validate the results and provide further details for Log Analytics to use in its analysis.</span></span>

1. <span data-ttu-id="b63cd-137">사용자 지정 필드를 채울 샘플 레코드에서 텍스트를 강조 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-137">Highlight the text in the sample record that you want to populate the custom field.</span></span>  <span data-ttu-id="b63cd-138">그러면 필드의 이름을 제공하고 초기 추출을 수행할 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-138">You will then be presented with a dialog box to provide a name for the field and to perform the initial extract.</span></span>  <span data-ttu-id="b63cd-139">**\_CF** 문자가 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-139">The characters **\_CF** will automatically be appended.</span></span>
2. <span data-ttu-id="b63cd-140">**추출** 을 클릭하여 수집된 레코드에 대한 분석을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-140">Click **Extract** to perform an analysis of collected records.</span></span>  
3. <span data-ttu-id="b63cd-141">**요약** 및 **검색 결과** 섹션에 정확성을 검사할 수 있도록 추출 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-141">The **Summary** and **Search Results** sections display the results of the extract so you can inspect its accuracy.</span></span>  <span data-ttu-id="b63cd-142">**요약** 에 식별된 각각의 데이터 값에 대한 개수 및 레코드를 식별하는 데 사용된 조건이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-142">**Summary** displays the criteria used to identify records and a count for each of the data values identified.</span></span>  <span data-ttu-id="b63cd-143">**검색 결과** 에 조건에 맞는 레코드의 자세한 목록이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-143">**Search Results** provides a detailed list of records matching the criteria.</span></span>

### <a name="step-3--verify-accuracy-of-the-extract-and-create-custom-field"></a><span data-ttu-id="b63cd-144">3단계 – 사용자 지정 필드 만들기 및 추출의 정확성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-144">Step 3 – Verify accuracy of the extract and create custom field</span></span>
<span data-ttu-id="b63cd-145">초기 추출을 수행하면, Log Analytics에 이미 수집된 데이터에 기반한 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-145">Once you have performed the initial extract, Log Analytics will display its results based on data that has already been collected.</span></span>  <span data-ttu-id="b63cd-146">결과가 정확해 보이면 더 이상 작업을 수행하지 않고 사용자 지정 필드를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-146">If the results look accurate then you can create the custom field with no further work.</span></span>  <span data-ttu-id="b63cd-147">그렇지 않으면, Log Analytics의 논리를 개선할 수 있도록 결과를 구체화합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-147">If not, then you can refine the results so that Log Analytics can improve its logic.</span></span>

1. <span data-ttu-id="b63cd-148">초기 추출에 정확하지 않은 값이 있으면, 정확하지 않은 레코드 옆의 **편집** 아이콘을 클릭하고 선택을 수정하기 위해서 **Modify this highlight**(이 강조 표시 수정)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-148">If any values in the initial extract aren’t correct, then click the **Edit** icon next to an inaccurate record and select **Modify this highlight** in order to modify the selection.</span></span>
2. <span data-ttu-id="b63cd-149">해당 항목이 **Main Example**(기본 예제) 아래 **Additional examples**(추가 예제) 섹션으로 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-149">The entry is copied to the **Additional examples** section underneath the **Main Example**.</span></span>  <span data-ttu-id="b63cd-150">여기에서 Log Analytics가 만들어야 하는 섹션을 이해할 수 있도록 강조 표시를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-150">You can adjust the highlight here to help Log Analytics understand the selection it should have made.</span></span>
3. <span data-ttu-id="b63cd-151">**추출** 을 클릭하여 새로운 정보를 모든 기존 레코드를 평가하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-151">Click **Extract** to use this new information to evaluate all the existing records.</span></span>  <span data-ttu-id="b63cd-152">결과는 새로운 인텔리전스를 기반으로 사용자가 수정한 레코드가 아닌 다른 레코드에 대해 수정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-152">The results may be modified for records other than the one you just modified based on this new intelligence.</span></span>
4. <span data-ttu-id="b63cd-153">추출 내 모든 레코드가 새 사용자 지정 필드를 채울 데이터를 제대로 식별할 때까지 수정을 계속 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-153">Continue to add corrections until all records in the extract correctly identify the data to populate the new custom field.</span></span>
5. <span data-ttu-id="b63cd-154">결과에 만족하면 **Save Extract** (추출 저장)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-154">Click **Save Extract** when you are satisfied with the results.</span></span>  <span data-ttu-id="b63cd-155">사용자 지정 필드가 정의되었지만 아직 레코드에는 추가되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-155">The custom field is now defined, but it won’t be added to any records yet.</span></span>
6. <span data-ttu-id="b63cd-156">지정된 수집 조건에 일치하는 새 레코드를 기다린 다음 로그 검색을 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-156">Wait for new records matching the specified criteria to be collected and then run the log search again.</span></span> <span data-ttu-id="b63cd-157">새 레코드에 사용자 지정 필드가 생깁니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-157">New records should have the custom field.</span></span>
7. <span data-ttu-id="b63cd-158">사용자 지정 필드를 다른 레코드 속성처럼 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-158">Use the custom field like any other record property.</span></span>  <span data-ttu-id="b63cd-159">이것을 사용하여 데이터를 집계하고 그룹화하며 새로운 통찰을 생성하는 데도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-159">You can use it to aggregate and group data and even use it to produce new insights.</span></span>

## <a name="viewing-custom-fields"></a><span data-ttu-id="b63cd-160">사용자 지정 필드 보기</span><span class="sxs-lookup"><span data-stu-id="b63cd-160">Viewing custom fields</span></span>
<span data-ttu-id="b63cd-161">OMS 대시보드 **설정** 타일의 관리 그룹에서 모든 사용자 지정 필드 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-161">You can view a list of all custom fields in your management group from the **Settings** tile of the OMS dashboard.</span></span>  <span data-ttu-id="b63cd-162">**데이터**를 선택한 다음 **사용자 지정 필드**를 선택하여 작업 영역 내 모든 사용자 지정 필드의 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-162">Select **Data** and then **Custom fields** for a list of all custom fields in your workspace.</span></span>  

![사용자 지정 필드](media/log-analytics-custom-fields/list.png)

## <a name="removing-a-custom-field"></a><span data-ttu-id="b63cd-164">사용자 지정 필드 제거</span><span class="sxs-lookup"><span data-stu-id="b63cd-164">Removing a custom field</span></span>
<span data-ttu-id="b63cd-165">사용자 지정 필드를 제거하는 방법은 두 가지입니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-165">There are two ways to remove a custom field.</span></span>  <span data-ttu-id="b63cd-166">첫 번째는 위의 설명대로 전체 목록을 볼 때 각 필드의 **제거** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-166">The first is the **Remove** option for each field when viewing the complete list as described above.</span></span>  <span data-ttu-id="b63cd-167">다른 방법은 레코드를 검색하고 필드 왼쪽의 단추를 클릭하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-167">The other method is to retrieve a record and click the button to the left of the field.</span></span>  <span data-ttu-id="b63cd-168">메뉴에 사용자 지정 필드를 제거하는 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-168">The menu will have an option to remove the custom field.</span></span>

## <a name="sample-walkthrough"></a><span data-ttu-id="b63cd-169">샘플 연습</span><span class="sxs-lookup"><span data-stu-id="b63cd-169">Sample walkthrough</span></span>
<span data-ttu-id="b63cd-170">다음 섹션은 사용자 지정 필드를 만드는 전체 예제를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-170">The following section walks through a complete example of creating a custom field.</span></span>  <span data-ttu-id="b63cd-171">이 예제는 서비스 변경 상태를 나타내는 Windows 이벤트의 서비스 이름을 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-171">This example extracts the service name in Windows events that indicate a service changing state.</span></span>  <span data-ttu-id="b63cd-172">이것은 Windows 컴퓨터의 시스템 로그에서 서비스 제어 관리자에 의해 생성되는 이벤트에 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-172">This relies on events created by Service Control Manager in the System log on Windows computers.</span></span>  <span data-ttu-id="b63cd-173">이 예제를 계속하려면, [시스템 로그에 대한 정보 이벤트를 수집](log-analytics-data-sources-windows-events.md)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-173">If you want to follow this example, you must be [collecting Information events for the System log](log-analytics-data-sources-windows-events.md).</span></span>

<span data-ttu-id="b63cd-174">서비스 시작 또는 중지를 나타내는 이벤트인, 이벤트 ID가 7036인 서비스 제어 관리자의 모든 이벤트를 반환하기 위해서 다음 쿼리를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-174">We enter the following query to return all events from Service Control Manager that have an Event ID of 7036 which is the event that indicates a service starting or stopping.</span></span>

![쿼리](media/log-analytics-custom-fields/query.png)

<span data-ttu-id="b63cd-176">그 다음 이벤트 ID가 7036인 레코드를 아무 레코드나 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-176">We then select any record with event ID 7036.</span></span>

![소스 레코드](media/log-analytics-custom-fields/source-record.png)

<span data-ttu-id="b63cd-178">**RenderedDescription** 속성에 표시되는 서비스 이름이 필요하며, 이 속성 옆의 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-178">We want the service name that appears in the **RenderedDescription** property and select the button next to this property.</span></span>

![추출 필드](media/log-analytics-custom-fields/extract-fields.png)

<span data-ttu-id="b63cd-180">**Field Extraction Wizard**(필드 추출 마법사)가 열리고 **EventLog** 및 **EventID** 필드가 **Main Example**(기본 예제) 열에서 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-180">The **Field Extraction Wizard** is opened, and the **EventLog** and **EventID** fields are selected in the **Main Example** column.</span></span>  <span data-ttu-id="b63cd-181">이것은 사용자 지정 필드가 이벤트 ID가 7036인 시스템 로그의 이벤트에 대해 정의된다는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-181">This indicates that the custom field will be defined for events from the System log with an event ID of 7036.</span></span>  <span data-ttu-id="b63cd-182">이것으로 충분하므로 다른 필드를 선택할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-182">This is sufficient so we don’t need to select any other fields.</span></span>

![Main Example](media/log-analytics-custom-fields/main-example.png)

<span data-ttu-id="b63cd-184">**RenderedDescription** 속성에서 서비스의 이름을 강조 표시하고 **Service**를 사용하여 서비스 이름을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-184">We highlight the name of the service in the **RenderedDescription** property and use **Service** to identify the service name.</span></span>  <span data-ttu-id="b63cd-185">사용자 지정 필드가 **Service_CF**라고 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-185">The custom field will be called **Service_CF**.</span></span>

![필드 제목](media/log-analytics-custom-fields/field-title.png)

<span data-ttu-id="b63cd-187">일부 레코드에 대해서는 서비스 이름이 적절하게 식별되었지만 나머지에 대해서는 그렇지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-187">We see that the service name is identified properly for some records but not for others.</span></span>   <span data-ttu-id="b63cd-188">**검색 결과**에 **WMI Performance Adapter**의 이름 일부가 선택되지 않은 것이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-188">The **Search Results** show that part of the name for the **WMI Performance Adapter** wasn’t selected.</span></span>  <span data-ttu-id="b63cd-189">**요약**에 **DPRMA** 서비스를 포함하는 네 개의 레코드에 추가적인 단어가 잘 못 포함되었고, 두 개의 레코드가 **Windows 모듈 설치 관리자**가 아닌 **모듈 설치 관리자**로 식별된 것이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-189">The **Summary** shows that four records with **DPRMA** service incorrectly included an extra word, and two records identified **Modules Installer** instead of **Windows Modules Installer**.</span></span>  

![검색 결과](media/log-analytics-custom-fields/search-results-01.png)

<span data-ttu-id="b63cd-191">**WMI Performance Adapter** 레코드부터 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-191">We start with the **WMI Performance Adapter** record.</span></span>  <span data-ttu-id="b63cd-192">편집 아이콘을 클릭한 다음 **Modify this highlight**(이 강조 표시 수정)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-192">We click its edit icon and then **Modify this highlight**.</span></span>  

![강조 표시 수정](media/log-analytics-custom-fields/modify-highlight.png)

<span data-ttu-id="b63cd-194">**WMI**라는 단어를 포함하도록 강조 표시를 키운 다음 추출을 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-194">We increase    the highlight to include the word **WMI** and then rerun the extract.</span></span>  

![추가 예제](media/log-analytics-custom-fields/additional-example-01.png)

<span data-ttu-id="b63cd-196">**WMI Performance Adapter**에 대한 항목이 수정되었고, Log Analytics 역시 해당 정보를 사용하여 **Windows모듈 설치 관리자**에 대한 레코드를 수정한 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-196">We can see that the entries for **WMI Performance Adapter** have been corrected, and Log Analytics also used that information to correct the records for **Windows Module Installer**.</span></span>  <span data-ttu-id="b63cd-197">**요약** 섹션에서 **DPMRA**가 여전히 제대로 식별되지 않고 있는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-197">We can see in the **Summary** section though that **DPMRA** is still not being identified correctly.</span></span>

![검색 결과](media/log-analytics-custom-fields/search-results-02.png)

<span data-ttu-id="b63cd-199">DPMRA 서비스를 포함하는 레코드로 스크롤하고 동일한 프로세스를 사용하여 해당 레코드를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-199">We scroll to a record with the DPMRA service and use the same process to correct that record.</span></span>

![추가 예제](media/log-analytics-custom-fields/additional-example-02.png)

 <span data-ttu-id="b63cd-201">추출을 실행하면 이제 모든 결과가 정확한 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-201">When we run the extraction, we can see that all of our results are now accurate.</span></span>

![검색 결과](media/log-analytics-custom-fields/search-results-03.png)

<span data-ttu-id="b63cd-203">**Service_CF**가 생성되었지만 아직 어느 레코드에도 추가되지 않은 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-203">We can see that **Service_CF** is created but is not yet added to any records.</span></span>

![초기 개수](media/log-analytics-custom-fields/initial-count.png)

<span data-ttu-id="b63cd-205">새 이벤트가 수집될 만큼 시간이 지나면, **Service_CF** 필드가 조건에 일치하는 레코드에 추가되는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-205">After some time has passed so new events are collected, we can see that that the **Service_CF** field is now being added to records that match our criteria.</span></span>

![최종 결과](media/log-analytics-custom-fields/final-results.png)

<span data-ttu-id="b63cd-207">이제 사용자 지정 필드를 다른 레코드 속성처럼 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-207">We can now use the custom field like any other record property.</span></span>  <span data-ttu-id="b63cd-208">이것을 설명하기 위해, 가장 활동적인 서비스가 무엇인지를 검사하는 새로운 **Service_CF** 필드로 그룹화하는 쿼리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-208">To illustrate this, we create a query that groups by the new **Service_CF** field to inspect which services are the most active.</span></span>

![쿼리로 그룹화](media/log-analytics-custom-fields/query-group.png)

## <a name="next-steps"></a><span data-ttu-id="b63cd-210">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b63cd-210">Next steps</span></span>
* <span data-ttu-id="b63cd-211">조건에 대한 사용자 지정 필드를 사용하여 쿼리를 빌드하기 위해 [검색 로그](log-analytics-log-searches.md) 에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-211">Learn about [log searches](log-analytics-log-searches.md) to build queries using custom fields for criteria.</span></span>
* <span data-ttu-id="b63cd-212">사용자 지정 필드를 사용하여 구문 분석하는 [사용자 지정 로그 파일](log-analytics-data-sources-custom-logs.md)을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="b63cd-212">Monitor [custom log files](log-analytics-data-sources-custom-logs.md) that you parse using custom fields.</span></span>

