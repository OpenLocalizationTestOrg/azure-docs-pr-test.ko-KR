---
title: "데이터 팩터리 함수 및 시스템 변수 | Microsoft Docs"
description: "Azure 데이터 팩터리 함수 및 시스템 변수 목록을 제공합니다."
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
services: data-factory
ms.assetid: b6b3c2ae-b0e8-4e28-90d8-daf20421660d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 72a966bdc271f86b9568d3310d2e22d83b447594
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-data-factory---functions-and-system-variables"></a><span data-ttu-id="a3653-103">Azure 데이터 팩터리 - 함수 및 시스템 변수</span><span class="sxs-lookup"><span data-stu-id="a3653-103">Azure Data Factory - Functions and System Variables</span></span>
<span data-ttu-id="a3653-104">이 문서에서는 Azure 데이터 팩터리에서 지원하는 함수와 변수에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-104">This article provides information about functions and variables supported by Azure Data Factory.</span></span>

## <a name="data-factory-system-variables"></a><span data-ttu-id="a3653-105">데이터 팩터리 시스템 변수</span><span class="sxs-lookup"><span data-stu-id="a3653-105">Data Factory system variables</span></span>
| <span data-ttu-id="a3653-106">변수 이름</span><span class="sxs-lookup"><span data-stu-id="a3653-106">Variable Name</span></span> | <span data-ttu-id="a3653-107">설명</span><span class="sxs-lookup"><span data-stu-id="a3653-107">Description</span></span> | <span data-ttu-id="a3653-108">개체 범위</span><span class="sxs-lookup"><span data-stu-id="a3653-108">Object Scope</span></span> | <span data-ttu-id="a3653-109">JSON 범위 및 사용 사례</span><span class="sxs-lookup"><span data-stu-id="a3653-109">JSON Scope and Use Cases</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a3653-110">WindowStart</span><span class="sxs-lookup"><span data-stu-id="a3653-110">WindowStart</span></span> |<span data-ttu-id="a3653-111">현재 작업 실행 창에 대한 시간 간격의 시작</span><span class="sxs-lookup"><span data-stu-id="a3653-111">Start of time interval for current activity run window</span></span> |<span data-ttu-id="a3653-112">작업</span><span class="sxs-lookup"><span data-stu-id="a3653-112">activity</span></span> |<ol><li><span data-ttu-id="a3653-113">데이터 선택 쿼리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-113">Specify data selection queries.</span></span> <span data-ttu-id="a3653-114">[데이터 이동 활동](data-factory-data-movement-activities.md) 문서에서 참조되는 커넥터 문서 참조)</span><span class="sxs-lookup"><span data-stu-id="a3653-114">See connector articles referenced in the [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span></li> |
| <span data-ttu-id="a3653-115">WindowEnd</span><span class="sxs-lookup"><span data-stu-id="a3653-115">WindowEnd</span></span> |<span data-ttu-id="a3653-116">현재 작업 실행 창에 대한 시간 간격의 끝</span><span class="sxs-lookup"><span data-stu-id="a3653-116">End of time interval for current activity run window</span></span> |<span data-ttu-id="a3653-117">작업</span><span class="sxs-lookup"><span data-stu-id="a3653-117">activity</span></span> |<span data-ttu-id="a3653-118">WindowStart와 동일</span><span class="sxs-lookup"><span data-stu-id="a3653-118">same as WindowStart.</span></span> |
| <span data-ttu-id="a3653-119">SliceStart</span><span class="sxs-lookup"><span data-stu-id="a3653-119">SliceStart</span></span> |<span data-ttu-id="a3653-120">생성되는 데이터 조각에 대한 시간 간격 시작</span><span class="sxs-lookup"><span data-stu-id="a3653-120">Start of time interval for data  slice being produced</span></span> |<span data-ttu-id="a3653-121">작업</span><span class="sxs-lookup"><span data-stu-id="a3653-121">activity</span></span><br/><span data-ttu-id="a3653-122">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="a3653-122">dataset</span></span> |<ol><li><span data-ttu-id="a3653-123">[Azure Blob](data-factory-azure-blob-connector.md) 및 [파일 시스템 데이터 집합](data-factory-onprem-file-system-connector.md)과 작업하는 동안 동적 폴더 경로 및 파일 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-123">Specify dynamic folder paths and file names while working with [Azure Blob](data-factory-azure-blob-connector.md) and [File System datasets](data-factory-onprem-file-system-connector.md).</span></span></li><li><span data-ttu-id="a3653-124">작업 입력 컬렉션에서 데이터 팩터리 함수에 입력 종속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-124">Specify input dependencies with data factory functions in activity inputs collection.</span></span></li></ol> |
| <span data-ttu-id="a3653-125">SliceEnd</span><span class="sxs-lookup"><span data-stu-id="a3653-125">SliceEnd</span></span> |<span data-ttu-id="a3653-126">현재 데이터 조각에 대한 시간 간격 끝</span><span class="sxs-lookup"><span data-stu-id="a3653-126">End of time interval for current data slice.</span></span> |<span data-ttu-id="a3653-127">작업</span><span class="sxs-lookup"><span data-stu-id="a3653-127">activity</span></span><br/><span data-ttu-id="a3653-128">dataset</span><span class="sxs-lookup"><span data-stu-id="a3653-128">dataset</span></span> |<span data-ttu-id="a3653-129">SliceStart와 동일</span><span class="sxs-lookup"><span data-stu-id="a3653-129">same as SliceStart.</span></span> |

> [!NOTE]
> <span data-ttu-id="a3653-130">현재 데이터 팩터리에서는 작업에 지정된 일정이 출력 데이터 집합의 가용성에 지정된 일정과 정확히 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-130">Currently data factory requires that the schedule specified in the activity exactly matches the schedule specified in availability of the output dataset.</span></span> <span data-ttu-id="a3653-131">따라서 WindowStart, WindowEnd, SliceStart 및 SliceEnd가 항상 같은 기간과 단일 출력 조각으로 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-131">Therefore, WindowStart, WindowEnd, and SliceStart and SliceEnd always map to the same time period and a single output slice.</span></span>
> 

### <a name="example-for-using-a-system-variable"></a><span data-ttu-id="a3653-132">시스템 변수 사용 예제</span><span class="sxs-lookup"><span data-stu-id="a3653-132">Example for using a system variable</span></span>
<span data-ttu-id="a3653-133">다음 예제에서 **SliceStart**의 연도, 월, 일 및 시간은 **folderPath** 및 **fileName** 속성에서 사용하는 별도 변수로 추출됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-133">In the following example, year, month, day, and time of **SliceStart** are extracted into separate variables that are used by **folderPath** and **fileName** properties.</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```

## <a name="data-factory-functions"></a><span data-ttu-id="a3653-134">데이터 팩터리 함수</span><span class="sxs-lookup"><span data-stu-id="a3653-134">Data Factory functions</span></span>
<span data-ttu-id="a3653-135">데이터 팩터리의 함수를 시스템 변수와 함께 다음과 같은 용도로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-135">You can use functions in data factory along with system variables for the following purposes:</span></span>

1. <span data-ttu-id="a3653-136">데이터 선택 쿼리 지정([데이터 이동 활동](data-factory-data-movement-activities.md) 문서에서 참조되는 커넥터 문서 참조)</span><span class="sxs-lookup"><span data-stu-id="a3653-136">Specifying data selection queries (see connector articles referenced by the [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span>
   
   <span data-ttu-id="a3653-137">데이터 팩터리 함수를 호출하는 구문은 데이터 선택 쿼리와 작업 및 데이터 집합의 기타 속성에 대해 **$$<function>** 입니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-137">The syntax to invoke a data factory function is: **$$<function>** for data selection queries and other properties in the activity and datasets.</span></span>  
2. <span data-ttu-id="a3653-138">작업 입력 컬렉션에서 데이터 팩터리 함수에 입력 종속성 지정</span><span class="sxs-lookup"><span data-stu-id="a3653-138">Specifying input dependencies with data factory functions in activity inputs collection.</span></span>
   
    <span data-ttu-id="a3653-139">$$는 입력 종속성 식을 지정할 때는 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-139">$$ is not needed for specifying input dependency expressions.</span></span>     

<span data-ttu-id="a3653-140">다음 샘플에서는 JSON 파일에서 **sqlReaderQuery** 속성을 `Text.Format` 함수가 반환하는 값에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-140">In the following sample, **sqlReaderQuery** property in a JSON file is assigned to a value returned by the `Text.Format` function.</span></span> <span data-ttu-id="a3653-141">또한 작업 실행 창의 시작 시간을 나타내는 **WindowStart**라는 시스템 변수도 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-141">This sample also uses a system variable named **WindowStart**, which represents the start time of the activity run window.</span></span>

```json
{
    "Type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
}
```

<span data-ttu-id="a3653-142">사용할 수 있는 다른 서식 옵션을 설명하는 [사용자 지정 날짜 및 시간 형식 문자열](https://msdn.microsoft.com/library/8kb3ddd4.aspx)(예: ay 및 yyyy) 토픽을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a3653-142">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: ay vs. yyyy).</span></span> 

### <a name="functions"></a><span data-ttu-id="a3653-143">함수</span><span class="sxs-lookup"><span data-stu-id="a3653-143">Functions</span></span>
<span data-ttu-id="a3653-144">다음 표에서는 Azure Data Factory의 모든 함수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-144">The following tables list all the functions in Azure Data Factory:</span></span>

| <span data-ttu-id="a3653-145">Category</span><span class="sxs-lookup"><span data-stu-id="a3653-145">Category</span></span> | <span data-ttu-id="a3653-146">함수</span><span class="sxs-lookup"><span data-stu-id="a3653-146">Function</span></span> | <span data-ttu-id="a3653-147">매개 변수</span><span class="sxs-lookup"><span data-stu-id="a3653-147">Parameters</span></span> | <span data-ttu-id="a3653-148">설명</span><span class="sxs-lookup"><span data-stu-id="a3653-148">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a3653-149">Time</span><span class="sxs-lookup"><span data-stu-id="a3653-149">Time</span></span> |<span data-ttu-id="a3653-150">AddHours(X,Y)</span><span class="sxs-lookup"><span data-stu-id="a3653-150">AddHours(X,Y)</span></span> |<span data-ttu-id="a3653-151">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="a3653-151">X: DateTime</span></span> <br/><br/><span data-ttu-id="a3653-152">Y: int</span><span class="sxs-lookup"><span data-stu-id="a3653-152">Y: int</span></span> |<span data-ttu-id="a3653-153">지정된 시간 X에 Y시간을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-153">Adds Y hours to the given time X.</span></span> <br/><br/><span data-ttu-id="a3653-154">예제: `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="a3653-154">Example: `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span></span> |
| <span data-ttu-id="a3653-155">Time</span><span class="sxs-lookup"><span data-stu-id="a3653-155">Time</span></span> |<span data-ttu-id="a3653-156">AddMinutes(X,Y)</span><span class="sxs-lookup"><span data-stu-id="a3653-156">AddMinutes(X,Y)</span></span> |<span data-ttu-id="a3653-157">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="a3653-157">X: DateTime</span></span> <br/><br/><span data-ttu-id="a3653-158">Y: int</span><span class="sxs-lookup"><span data-stu-id="a3653-158">Y: int</span></span> |<span data-ttu-id="a3653-159">X에 Y분을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-159">Adds Y minutes to X.</span></span><br/><br/><span data-ttu-id="a3653-160">예제: `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span><span class="sxs-lookup"><span data-stu-id="a3653-160">Example: `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span></span> |
| <span data-ttu-id="a3653-161">Time</span><span class="sxs-lookup"><span data-stu-id="a3653-161">Time</span></span> |<span data-ttu-id="a3653-162">StartOfHour(X)</span><span class="sxs-lookup"><span data-stu-id="a3653-162">StartOfHour(X)</span></span> |<span data-ttu-id="a3653-163">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="a3653-163">X: Datetime</span></span> |<span data-ttu-id="a3653-164">X의 시간 구성 요소로 표현되는 시간에 대한 시작 시간을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-164">Gets the starting time for the hour represented by the hour component of X.</span></span> <br/><br/><span data-ttu-id="a3653-165">예제: `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="a3653-165">Example: `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span></span> |
| <span data-ttu-id="a3653-166">Date</span><span class="sxs-lookup"><span data-stu-id="a3653-166">Date</span></span> |<span data-ttu-id="a3653-167">AddDays(X,Y)</span><span class="sxs-lookup"><span data-stu-id="a3653-167">AddDays(X,Y)</span></span> |<span data-ttu-id="a3653-168">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="a3653-168">X: DateTime</span></span><br/><br/><span data-ttu-id="a3653-169">Y: int</span><span class="sxs-lookup"><span data-stu-id="a3653-169">Y: int</span></span> |<span data-ttu-id="a3653-170">X에 Y일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-170">Adds Y days to X.</span></span> <br/><br/><span data-ttu-id="a3653-171">예제: 9/15/2013 12:00:00 PM + 2일 = 9/17/2013 12:00:00 PM</span><span class="sxs-lookup"><span data-stu-id="a3653-171">Example: 9/15/2013 12:00:00 PM + 2 days = 9/17/2013 12:00:00 PM.</span></span><br/><br/><span data-ttu-id="a3653-172">Y를 음수로 지정하여 일도 뺄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-172">You can subtract days too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="a3653-173">예: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="a3653-173">Example: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="a3653-174">Date</span><span class="sxs-lookup"><span data-stu-id="a3653-174">Date</span></span> |<span data-ttu-id="a3653-175">AddMonths(X,Y)</span><span class="sxs-lookup"><span data-stu-id="a3653-175">AddMonths(X,Y)</span></span> |<span data-ttu-id="a3653-176">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="a3653-176">X: DateTime</span></span><br/><br/><span data-ttu-id="a3653-177">Y: int</span><span class="sxs-lookup"><span data-stu-id="a3653-177">Y: int</span></span> |<span data-ttu-id="a3653-178">X에 Y개월을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-178">Adds Y months to X.</span></span><br/><br/><span data-ttu-id="a3653-179">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="a3653-179">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.</span></span><br/><br/><span data-ttu-id="a3653-180">Y를 음수로 지정하여 월도 뺄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-180">You can subtract months too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="a3653-181">예: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="a3653-181">Example: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span></span>|
| <span data-ttu-id="a3653-182">Date</span><span class="sxs-lookup"><span data-stu-id="a3653-182">Date</span></span> |<span data-ttu-id="a3653-183">AddQuarters(X,Y)</span><span class="sxs-lookup"><span data-stu-id="a3653-183">AddQuarters(X,Y)</span></span> |<span data-ttu-id="a3653-184">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="a3653-184">X: DateTime</span></span> <br/><br/><span data-ttu-id="a3653-185">Y: int</span><span class="sxs-lookup"><span data-stu-id="a3653-185">Y: int</span></span> |<span data-ttu-id="a3653-186">X에 Y * 3개월을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-186">Adds Y * 3 months to X.</span></span><br/><br/><span data-ttu-id="a3653-187">예제: `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="a3653-187">Example: `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span></span> |
| <span data-ttu-id="a3653-188">Date</span><span class="sxs-lookup"><span data-stu-id="a3653-188">Date</span></span> |<span data-ttu-id="a3653-189">AddWeeks(X,Y)</span><span class="sxs-lookup"><span data-stu-id="a3653-189">AddWeeks(X,Y)</span></span> |<span data-ttu-id="a3653-190">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="a3653-190">X: DateTime</span></span><br/><br/><span data-ttu-id="a3653-191">Y: int</span><span class="sxs-lookup"><span data-stu-id="a3653-191">Y: int</span></span> |<span data-ttu-id="a3653-192">X에 Y * 7일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-192">Adds Y * 7 days to X</span></span><br/><br/><span data-ttu-id="a3653-193">예: 9/15/2013 12:00:00 PM + 1주 = 9/22/2013 12:00:00 PM</span><span class="sxs-lookup"><span data-stu-id="a3653-193">Example: 9/15/2013 12:00:00 PM + 1 week = 9/22/2013 12:00:00 PM</span></span><br/><br/><span data-ttu-id="a3653-194">Y를 음수로 지정하여 주도 뺄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-194">You can subtract weeks too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="a3653-195">예: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="a3653-195">Example: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="a3653-196">Date</span><span class="sxs-lookup"><span data-stu-id="a3653-196">Date</span></span> |<span data-ttu-id="a3653-197">AddYears(X,Y)</span><span class="sxs-lookup"><span data-stu-id="a3653-197">AddYears(X,Y)</span></span> |<span data-ttu-id="a3653-198">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="a3653-198">X: DateTime</span></span><br/><br/><span data-ttu-id="a3653-199">Y: int</span><span class="sxs-lookup"><span data-stu-id="a3653-199">Y: int</span></span> |<span data-ttu-id="a3653-200">X에 Y년을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-200">Adds Y years to X.</span></span><br/><br/>`Example: 9/15/2013 12:00:00 PM + 1 year = 9/15/2014 12:00:00 PM`<br/><br/><span data-ttu-id="a3653-201">Y를 음수로 지정하여 년도 뺄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-201">You can subtract years too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="a3653-202">예: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="a3653-202">Example: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span></span> |
| <span data-ttu-id="a3653-203">Date</span><span class="sxs-lookup"><span data-stu-id="a3653-203">Date</span></span> |<span data-ttu-id="a3653-204">Day(X)</span><span class="sxs-lookup"><span data-stu-id="a3653-204">Day(X)</span></span> |<span data-ttu-id="a3653-205">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="a3653-205">X: DateTime</span></span> |<span data-ttu-id="a3653-206">X의 일 구성 요소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-206">Gets the day component of X.</span></span><br/><br/><span data-ttu-id="a3653-207">예: `Day of 9/15/2013 12:00:00 PM is 9`.</span><span class="sxs-lookup"><span data-stu-id="a3653-207">Example: `Day of 9/15/2013 12:00:00 PM is 9`.</span></span> |
| <span data-ttu-id="a3653-208">Date</span><span class="sxs-lookup"><span data-stu-id="a3653-208">Date</span></span> |<span data-ttu-id="a3653-209">DayOfWeek(X)</span><span class="sxs-lookup"><span data-stu-id="a3653-209">DayOfWeek(X)</span></span> |<span data-ttu-id="a3653-210">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="a3653-210">X: DateTime</span></span> |<span data-ttu-id="a3653-211">X의 요일 구성 요소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-211">Gets the day of week component of X.</span></span><br/><br/><span data-ttu-id="a3653-212">예: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span><span class="sxs-lookup"><span data-stu-id="a3653-212">Example: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span></span> |
| <span data-ttu-id="a3653-213">Date</span><span class="sxs-lookup"><span data-stu-id="a3653-213">Date</span></span> |<span data-ttu-id="a3653-214">DayOfYear(X)</span><span class="sxs-lookup"><span data-stu-id="a3653-214">DayOfYear(X)</span></span> |<span data-ttu-id="a3653-215">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="a3653-215">X: DateTime</span></span> |<span data-ttu-id="a3653-216">X의 연도 구성 요소로 표현되는 연도의 일을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-216">Gets the day in the year represented by the year component of X.</span></span><br/><br/><span data-ttu-id="a3653-217">예제:</span><span class="sxs-lookup"><span data-stu-id="a3653-217">Examples:</span></span><br/>`12/1/2015: day 335 of 2015`<br/>`12/31/2015: day 365 of 2015`<br/>`12/31/2016: day 366 of 2016 (Leap Year)` |
| <span data-ttu-id="a3653-218">Date</span><span class="sxs-lookup"><span data-stu-id="a3653-218">Date</span></span> |<span data-ttu-id="a3653-219">DaysInMonth(X)</span><span class="sxs-lookup"><span data-stu-id="a3653-219">DaysInMonth(X)</span></span> |<span data-ttu-id="a3653-220">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="a3653-220">X: DateTime</span></span> |<span data-ttu-id="a3653-221">매개 변수 X의 월 구성 요소로 표현되는 월의 일을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-221">Gets the days in the month represented by the month component of parameter X.</span></span><br/><br/><span data-ttu-id="a3653-222">예: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in the September month`.</span><span class="sxs-lookup"><span data-stu-id="a3653-222">Example: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in the September month`.</span></span> |
| <span data-ttu-id="a3653-223">Date</span><span class="sxs-lookup"><span data-stu-id="a3653-223">Date</span></span> |<span data-ttu-id="a3653-224">EndOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="a3653-224">EndOfDay(X)</span></span> |<span data-ttu-id="a3653-225">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="a3653-225">X: DateTime</span></span> |<span data-ttu-id="a3653-226">X의 끝나는 날(일 구성 요소)을 나타내는 날짜-시간을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-226">Gets the date-time that represents the end of the day (day component) of X.</span></span><br/><br/><span data-ttu-id="a3653-227">예: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span><span class="sxs-lookup"><span data-stu-id="a3653-227">Example: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span></span> |
| <span data-ttu-id="a3653-228">Date</span><span class="sxs-lookup"><span data-stu-id="a3653-228">Date</span></span> |<span data-ttu-id="a3653-229">EndOfMonth(X)</span><span class="sxs-lookup"><span data-stu-id="a3653-229">EndOfMonth(X)</span></span> |<span data-ttu-id="a3653-230">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="a3653-230">X: DateTime</span></span> |<span data-ttu-id="a3653-231">매개 변수 X의 월 구성 요소로 표현되는 월의 끝을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-231">Gets the end of the month represented by month component of parameter X.</span></span> <br/><br/><span data-ttu-id="a3653-232">예: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM`(9월의 끝을 나타내는 날짜 시간)</span><span class="sxs-lookup"><span data-stu-id="a3653-232">Example: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (date time that represents the end of September month)</span></span> |
| <span data-ttu-id="a3653-233">Date</span><span class="sxs-lookup"><span data-stu-id="a3653-233">Date</span></span> |<span data-ttu-id="a3653-234">StartOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="a3653-234">StartOfDay(X)</span></span> |<span data-ttu-id="a3653-235">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="a3653-235">X: DateTime</span></span> |<span data-ttu-id="a3653-236">매개 변수 X의 일 구성 요소로 표현되는 일의 시작을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-236">Gets the start of the day represented by the day component of parameter X.</span></span><br/><br/><span data-ttu-id="a3653-237">예: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span><span class="sxs-lookup"><span data-stu-id="a3653-237">Example: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span></span> |
| <span data-ttu-id="a3653-238">DateTime</span><span class="sxs-lookup"><span data-stu-id="a3653-238">DateTime</span></span> |<span data-ttu-id="a3653-239">From(X)</span><span class="sxs-lookup"><span data-stu-id="a3653-239">From(X)</span></span> |<span data-ttu-id="a3653-240">X: String</span><span class="sxs-lookup"><span data-stu-id="a3653-240">X: String</span></span> |<span data-ttu-id="a3653-241">문자열 X를 날짜 시간으로 구문 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-241">Parse string X to a date time.</span></span> |
| <span data-ttu-id="a3653-242">DateTime</span><span class="sxs-lookup"><span data-stu-id="a3653-242">DateTime</span></span> |<span data-ttu-id="a3653-243">Ticks(X)</span><span class="sxs-lookup"><span data-stu-id="a3653-243">Ticks(X)</span></span> |<span data-ttu-id="a3653-244">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="a3653-244">X: DateTime</span></span> |<span data-ttu-id="a3653-245">매개 변수 X의 틱 속성을 가져옵니다. 1틱은 100나노초에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-245">Gets the ticks property of the parameter X. One tick equals 100 nanoseconds.</span></span> <span data-ttu-id="a3653-246">이 속성 값은 0001년 1월 1일 자정 12:00:00 이후 경과된 틱 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-246">The value of this property represents the number of ticks that have elapsed since 12:00:00 midnight, January 1, 0001.</span></span> |
| <span data-ttu-id="a3653-247">텍스트</span><span class="sxs-lookup"><span data-stu-id="a3653-247">Text</span></span> |<span data-ttu-id="a3653-248">Format(X)</span><span class="sxs-lookup"><span data-stu-id="a3653-248">Format(X)</span></span> |<span data-ttu-id="a3653-249">X: String 변수</span><span class="sxs-lookup"><span data-stu-id="a3653-249">X: String variable</span></span> |<span data-ttu-id="a3653-250">텍스트의 서식을 지정합니다(`\\'` 조합을 사용하여 `'` 문자 이스케이프).</span><span class="sxs-lookup"><span data-stu-id="a3653-250">Formats the text (use `\\'` combination to escape `'` character).</span></span>|

> [!IMPORTANT]
> <span data-ttu-id="a3653-251">다른 함수 내에서 함수를 사용할 경우 내부 함수에 대한 접두사로 **$$** 를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-251">When using a function within another function, you do not need to use **$$** prefix for the inner function.</span></span> <span data-ttu-id="a3653-252">예: $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' 및 RowKey ge \\'{0: yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)).</span><span class="sxs-lookup"><span data-stu-id="a3653-252">For example: $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' and RowKey ge \\'{0: yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)).</span></span> <span data-ttu-id="a3653-253">이 예에서는 **Time.AddHours** 함수에 대해 **$$** 접두사가 사용되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-253">In this example, notice that **$$** prefix is not used for the **Time.AddHours** function.</span></span> 

#### <a name="example"></a><span data-ttu-id="a3653-254">예</span><span class="sxs-lookup"><span data-stu-id="a3653-254">Example</span></span>
<span data-ttu-id="a3653-255">다음 예제에서는 Hive 활동에 대한 입력 및 출력 매개 변수가 `Text.Format` 함수 및 SliceStart 시스템 변수를 사용하여 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-255">In the following example, input and output parameters for the Hive activity are determined by using the `Text.Format` function and SliceStart system variable.</span></span> 

```json  
{
    "name": "HiveActivitySamplePipeline",
        "properties": {
    "activities": [
            {
            "name": "HiveActivitySample",
            "type": "HDInsightHive",
            "inputs": [
                    {
                    "name": "HiveSampleIn"
                    }
            ],
            "outputs": [
                    {
                    "name": "HiveSampleOut"
                }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "typeproperties": {
                    "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                    "scriptLinkedService": "StorageLinkedService",
                    "defines": {
                        "Input": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                    },
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                }
            }
            }
    ]
    }
}
```

### <a name="example-2"></a><span data-ttu-id="a3653-256">예 2</span><span class="sxs-lookup"><span data-stu-id="a3653-256">Example 2</span></span>

<span data-ttu-id="a3653-257">다음 예제에서는 저장 프로시저 작업에 대 한 날짜/시간 매개 변수는 텍스트를 사용 하 여 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-257">In the following example, the DateTime parameter for the Stored Procedure Activity is determined by using the Text.</span></span> <span data-ttu-id="a3653-258">Format 함수 및 SliceStart 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-258">Format function and the SliceStart variable.</span></span> 

```json
{
    "name": "SprocActivitySamplePipeline",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                    }
                },
                "outputs": [
                    {
                        "name": "sprocsampleout"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
            "start": "2016-08-02T00:00:00Z",
            "end": "2016-08-02T05:00:00Z",
        "isPaused": false
    }
}
```

### <a name="example-3"></a><span data-ttu-id="a3653-259">예 3</span><span class="sxs-lookup"><span data-stu-id="a3653-259">Example 3</span></span>
<span data-ttu-id="a3653-260">SliceStart로 표현된 일 대신 이전 일의 데이터를 읽으려면 다음 예제와 같이 AddDays 함수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a3653-260">To read data from previous day instead of day represented by the SliceStart, use the AddDays function as shown in the following example:</span></span> 

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-01-01T08:00:00",
        "end": "2017-01-01T11:00:00",
        "description": "hive activity",
        "activities": [
            {
                "name": "SampleHiveActivity",
                "inputs": [
                    {
                        "name": "MyAzureBlobInput",
                        "startTime": "Date.AddDays(SliceStart, -1)",
                        "endTime": "Date.AddDays(SliceEnd, -1)"
                    }
                ],
                "outputs": [
                    {
                        "name": "MyAzureBlobOutput"
                    }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adftutorial\\hivequery.hql",
                    "scriptLinkedService": "StorageLinkedService",
                    "defines": {
                        "Year": "$$Text.Format('{0:yyyy}',WindowsStart)",
                        "Month": "$$Text.Format('{0:MM}',WindowStart)",
                        "Day": "$$Text.Format('{0:dd}',WindowStart)"
                    }
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "OldestFirst",
                    "retry": 2,
                    "timeout": "01:00:00"
                }
            }
        ]
    }
}
```

<span data-ttu-id="a3653-261">사용할 수 있는 다른 서식 옵션을 설명하는 [사용자 지정 날짜 및 시간 형식 문자열](https://msdn.microsoft.com/library/8kb3ddd4.aspx) (예: yy 대 yyyy) 토픽을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a3653-261">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: yy vs. yyyy).</span></span> 

