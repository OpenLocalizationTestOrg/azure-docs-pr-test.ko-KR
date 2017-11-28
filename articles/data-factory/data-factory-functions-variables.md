---
title: "aaaData 팩터리 함수 및 시스템 변수 | Microsoft Docs"
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
ms.openlocfilehash: d2936c2821797947bb37d9775226a6c19c4b8ab9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---functions-and-system-variables"></a><span data-ttu-id="75d8e-103">Azure 데이터 팩터리 - 함수 및 시스템 변수</span><span class="sxs-lookup"><span data-stu-id="75d8e-103">Azure Data Factory - Functions and System Variables</span></span>
<span data-ttu-id="75d8e-104">이 문서에서는 Azure 데이터 팩터리에서 지원하는 함수와 변수에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-104">This article provides information about functions and variables supported by Azure Data Factory.</span></span>

## <a name="data-factory-system-variables"></a><span data-ttu-id="75d8e-105">데이터 팩터리 시스템 변수</span><span class="sxs-lookup"><span data-stu-id="75d8e-105">Data Factory system variables</span></span>
| <span data-ttu-id="75d8e-106">변수 이름</span><span class="sxs-lookup"><span data-stu-id="75d8e-106">Variable Name</span></span> | <span data-ttu-id="75d8e-107">설명</span><span class="sxs-lookup"><span data-stu-id="75d8e-107">Description</span></span> | <span data-ttu-id="75d8e-108">개체 범위</span><span class="sxs-lookup"><span data-stu-id="75d8e-108">Object Scope</span></span> | <span data-ttu-id="75d8e-109">JSON 범위 및 사용 사례</span><span class="sxs-lookup"><span data-stu-id="75d8e-109">JSON Scope and Use Cases</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="75d8e-110">WindowStart</span><span class="sxs-lookup"><span data-stu-id="75d8e-110">WindowStart</span></span> |<span data-ttu-id="75d8e-111">현재 작업 실행 창에 대한 시간 간격의 시작</span><span class="sxs-lookup"><span data-stu-id="75d8e-111">Start of time interval for current activity run window</span></span> |<span data-ttu-id="75d8e-112">작업</span><span class="sxs-lookup"><span data-stu-id="75d8e-112">activity</span></span> |<ol><li><span data-ttu-id="75d8e-113">데이터 선택 쿼리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-113">Specify data selection queries.</span></span> <span data-ttu-id="75d8e-114">Hello 커넥터 문서의 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="75d8e-114">See connector articles referenced in hello [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span></li> |
| <span data-ttu-id="75d8e-115">WindowEnd</span><span class="sxs-lookup"><span data-stu-id="75d8e-115">WindowEnd</span></span> |<span data-ttu-id="75d8e-116">현재 작업 실행 창에 대한 시간 간격의 끝</span><span class="sxs-lookup"><span data-stu-id="75d8e-116">End of time interval for current activity run window</span></span> |<span data-ttu-id="75d8e-117">작업</span><span class="sxs-lookup"><span data-stu-id="75d8e-117">activity</span></span> |<span data-ttu-id="75d8e-118">WindowStart와 동일</span><span class="sxs-lookup"><span data-stu-id="75d8e-118">same as WindowStart.</span></span> |
| <span data-ttu-id="75d8e-119">SliceStart</span><span class="sxs-lookup"><span data-stu-id="75d8e-119">SliceStart</span></span> |<span data-ttu-id="75d8e-120">생성되는 데이터 조각에 대한 시간 간격 시작</span><span class="sxs-lookup"><span data-stu-id="75d8e-120">Start of time interval for data  slice being produced</span></span> |<span data-ttu-id="75d8e-121">작업</span><span class="sxs-lookup"><span data-stu-id="75d8e-121">activity</span></span><br/><span data-ttu-id="75d8e-122">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="75d8e-122">dataset</span></span> |<ol><li><span data-ttu-id="75d8e-123">[Azure Blob](data-factory-azure-blob-connector.md) 및 [파일 시스템 데이터 집합](data-factory-onprem-file-system-connector.md)과 작업하는 동안 동적 폴더 경로 및 파일 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-123">Specify dynamic folder paths and file names while working with [Azure Blob](data-factory-azure-blob-connector.md) and [File System datasets](data-factory-onprem-file-system-connector.md).</span></span></li><li><span data-ttu-id="75d8e-124">작업 입력 컬렉션에서 데이터 팩터리 함수에 입력 종속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-124">Specify input dependencies with data factory functions in activity inputs collection.</span></span></li></ol> |
| <span data-ttu-id="75d8e-125">SliceEnd</span><span class="sxs-lookup"><span data-stu-id="75d8e-125">SliceEnd</span></span> |<span data-ttu-id="75d8e-126">현재 데이터 조각에 대한 시간 간격 끝</span><span class="sxs-lookup"><span data-stu-id="75d8e-126">End of time interval for current data slice.</span></span> |<span data-ttu-id="75d8e-127">작업</span><span class="sxs-lookup"><span data-stu-id="75d8e-127">activity</span></span><br/><span data-ttu-id="75d8e-128">dataset</span><span class="sxs-lookup"><span data-stu-id="75d8e-128">dataset</span></span> |<span data-ttu-id="75d8e-129">SliceStart와 동일</span><span class="sxs-lookup"><span data-stu-id="75d8e-129">same as SliceStart.</span></span> |

> [!NOTE]
> <span data-ttu-id="75d8e-130">해당 hello 예약에 지정 된 hello 데이터 팩터리를 사용 하려면 현재 hello 출력 데이터 집합의 가용성에 지정 된 hello 일정이 정확히 일치 하는 활동입니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-130">Currently data factory requires that hello schedule specified in hello activity exactly matches hello schedule specified in availability of hello output dataset.</span></span> <span data-ttu-id="75d8e-131">따라서 WindowStart, WindowEnd, 및 SliceStart와 SliceEnd 항상 매핑됩니다 toohello 동일한 기간과 단일 출력 조각 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-131">Therefore, WindowStart, WindowEnd, and SliceStart and SliceEnd always map toohello same time period and a single output slice.</span></span>
> 

### <a name="example-for-using-a-system-variable"></a><span data-ttu-id="75d8e-132">시스템 변수 사용 예제</span><span class="sxs-lookup"><span data-stu-id="75d8e-132">Example for using a system variable</span></span>
<span data-ttu-id="75d8e-133">Hello 예제, 연도, 월, 일 및 시간을 다음에 **SliceStart** 에서 사용 되는 개별 변수로 추출 **folderPath** 및 **fileName** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-133">In hello following example, year, month, day, and time of **SliceStart** are extracted into separate variables that are used by **folderPath** and **fileName** properties.</span></span>

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

## <a name="data-factory-functions"></a><span data-ttu-id="75d8e-134">데이터 팩터리 함수</span><span class="sxs-lookup"><span data-stu-id="75d8e-134">Data Factory functions</span></span>
<span data-ttu-id="75d8e-135">시스템 변수 함께 데이터 팩터리에서 목적으로 다음 hello에 대 한 함수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-135">You can use functions in data factory along with system variables for hello following purposes:</span></span>

1. <span data-ttu-id="75d8e-136">데이터 선택 쿼리 지정 (hello에서 참조 하는 커넥터 문서를 참조 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="75d8e-136">Specifying data selection queries (see connector articles referenced by hello [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span>
   
   <span data-ttu-id="75d8e-137">데이터 팩터리 함수는 구문 tooinvoke hello:  **$$ <function>**  데이터 선택 쿼리와 hello 활동 및 데이터 집합에 다른 속성에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-137">hello syntax tooinvoke a data factory function is: **$$<function>** for data selection queries and other properties in hello activity and datasets.</span></span>  
2. <span data-ttu-id="75d8e-138">작업 입력 컬렉션에서 데이터 팩터리 함수에 입력 종속성 지정</span><span class="sxs-lookup"><span data-stu-id="75d8e-138">Specifying input dependencies with data factory functions in activity inputs collection.</span></span>
   
    <span data-ttu-id="75d8e-139">$$는 입력 종속성 식을 지정할 때는 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-139">$$ is not needed for specifying input dependency expressions.</span></span>     

<span data-ttu-id="75d8e-140">다음 샘플에서는 hello에 **sqlReaderQuery** JSON 파일에 속성 hello 반환한 tooa 값이 할당 `Text.Format` 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-140">In hello following sample, **sqlReaderQuery** property in a JSON file is assigned tooa value returned by hello `Text.Format` function.</span></span> <span data-ttu-id="75d8e-141">또한이 샘플에서는 시스템 변수 라는 **WindowStart**, 창을 실행 하는 hello 활동의 hello 시작 시간을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-141">This sample also uses a system variable named **WindowStart**, which represents hello start time of hello activity run window.</span></span>

```json
{
    "Type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
}
```

<span data-ttu-id="75d8e-142">사용할 수 있는 다른 서식 옵션을 설명하는 [사용자 지정 날짜 및 시간 형식 문자열](https://msdn.microsoft.com/library/8kb3ddd4.aspx)(예: ay 및 yyyy) 토픽을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75d8e-142">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: ay vs. yyyy).</span></span> 

### <a name="functions"></a><span data-ttu-id="75d8e-143">함수</span><span class="sxs-lookup"><span data-stu-id="75d8e-143">Functions</span></span>
<span data-ttu-id="75d8e-144">다음 표에서 hello Azure 데이터 팩터리의 모든 hello 함수를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-144">hello following tables list all hello functions in Azure Data Factory:</span></span>

| <span data-ttu-id="75d8e-145">Category</span><span class="sxs-lookup"><span data-stu-id="75d8e-145">Category</span></span> | <span data-ttu-id="75d8e-146">함수</span><span class="sxs-lookup"><span data-stu-id="75d8e-146">Function</span></span> | <span data-ttu-id="75d8e-147">매개 변수</span><span class="sxs-lookup"><span data-stu-id="75d8e-147">Parameters</span></span> | <span data-ttu-id="75d8e-148">설명</span><span class="sxs-lookup"><span data-stu-id="75d8e-148">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="75d8e-149">Time</span><span class="sxs-lookup"><span data-stu-id="75d8e-149">Time</span></span> |<span data-ttu-id="75d8e-150">AddHours(X,Y)</span><span class="sxs-lookup"><span data-stu-id="75d8e-150">AddHours(X,Y)</span></span> |<span data-ttu-id="75d8e-151">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="75d8e-151">X: DateTime</span></span> <br/><br/><span data-ttu-id="75d8e-152">Y: int</span><span class="sxs-lookup"><span data-stu-id="75d8e-152">Y: int</span></span> |<span data-ttu-id="75d8e-153">지정 된 시간 X Y 시간 toohello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-153">Adds Y hours toohello given time X.</span></span> <br/><br/><span data-ttu-id="75d8e-154">예: `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="75d8e-154">Example: `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span></span> |
| <span data-ttu-id="75d8e-155">Time</span><span class="sxs-lookup"><span data-stu-id="75d8e-155">Time</span></span> |<span data-ttu-id="75d8e-156">AddMinutes(X,Y)</span><span class="sxs-lookup"><span data-stu-id="75d8e-156">AddMinutes(X,Y)</span></span> |<span data-ttu-id="75d8e-157">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="75d8e-157">X: DateTime</span></span> <br/><br/><span data-ttu-id="75d8e-158">Y: int</span><span class="sxs-lookup"><span data-stu-id="75d8e-158">Y: int</span></span> |<span data-ttu-id="75d8e-159">Y 분 tooX를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-159">Adds Y minutes tooX.</span></span><br/><br/><span data-ttu-id="75d8e-160">예: `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span><span class="sxs-lookup"><span data-stu-id="75d8e-160">Example: `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span></span> |
| <span data-ttu-id="75d8e-161">Time</span><span class="sxs-lookup"><span data-stu-id="75d8e-161">Time</span></span> |<span data-ttu-id="75d8e-162">StartOfHour(X)</span><span class="sxs-lookup"><span data-stu-id="75d8e-162">StartOfHour(X)</span></span> |<span data-ttu-id="75d8e-163">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="75d8e-163">X: Datetime</span></span> |<span data-ttu-id="75d8e-164">Hello 가져옵니다 X의 hello 시간 구성 요소는이 나타내는 hello 시간에 대 한 시간을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-164">Gets hello starting time for hello hour represented by hello hour component of X.</span></span> <br/><br/><span data-ttu-id="75d8e-165">예: `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="75d8e-165">Example: `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span></span> |
| <span data-ttu-id="75d8e-166">Date</span><span class="sxs-lookup"><span data-stu-id="75d8e-166">Date</span></span> |<span data-ttu-id="75d8e-167">AddDays(X,Y)</span><span class="sxs-lookup"><span data-stu-id="75d8e-167">AddDays(X,Y)</span></span> |<span data-ttu-id="75d8e-168">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="75d8e-168">X: DateTime</span></span><br/><br/><span data-ttu-id="75d8e-169">Y: int</span><span class="sxs-lookup"><span data-stu-id="75d8e-169">Y: int</span></span> |<span data-ttu-id="75d8e-170">Y 일 tooX를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-170">Adds Y days tooX.</span></span> <br/><br/><span data-ttu-id="75d8e-171">예제: 9/15/2013 12:00:00 PM + 2일 = 9/17/2013 12:00:00 PM</span><span class="sxs-lookup"><span data-stu-id="75d8e-171">Example: 9/15/2013 12:00:00 PM + 2 days = 9/17/2013 12:00:00 PM.</span></span><br/><br/><span data-ttu-id="75d8e-172">Y를 음수로 지정하여 일도 뺄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-172">You can subtract days too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="75d8e-173">예: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="75d8e-173">Example: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="75d8e-174">Date</span><span class="sxs-lookup"><span data-stu-id="75d8e-174">Date</span></span> |<span data-ttu-id="75d8e-175">AddMonths(X,Y)</span><span class="sxs-lookup"><span data-stu-id="75d8e-175">AddMonths(X,Y)</span></span> |<span data-ttu-id="75d8e-176">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="75d8e-176">X: DateTime</span></span><br/><br/><span data-ttu-id="75d8e-177">Y: int</span><span class="sxs-lookup"><span data-stu-id="75d8e-177">Y: int</span></span> |<span data-ttu-id="75d8e-178">Y 개월 tooX를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-178">Adds Y months tooX.</span></span><br/><br/><span data-ttu-id="75d8e-179">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="75d8e-179">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.</span></span><br/><br/><span data-ttu-id="75d8e-180">Y를 음수로 지정하여 월도 뺄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-180">You can subtract months too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="75d8e-181">예: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="75d8e-181">Example: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span></span>|
| <span data-ttu-id="75d8e-182">Date</span><span class="sxs-lookup"><span data-stu-id="75d8e-182">Date</span></span> |<span data-ttu-id="75d8e-183">AddQuarters(X,Y)</span><span class="sxs-lookup"><span data-stu-id="75d8e-183">AddQuarters(X,Y)</span></span> |<span data-ttu-id="75d8e-184">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="75d8e-184">X: DateTime</span></span> <br/><br/><span data-ttu-id="75d8e-185">Y: int</span><span class="sxs-lookup"><span data-stu-id="75d8e-185">Y: int</span></span> |<span data-ttu-id="75d8e-186">추가 Y * 3 개월 tooX 합니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-186">Adds Y * 3 months tooX.</span></span><br/><br/><span data-ttu-id="75d8e-187">예: `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="75d8e-187">Example: `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span></span> |
| <span data-ttu-id="75d8e-188">Date</span><span class="sxs-lookup"><span data-stu-id="75d8e-188">Date</span></span> |<span data-ttu-id="75d8e-189">AddWeeks(X,Y)</span><span class="sxs-lookup"><span data-stu-id="75d8e-189">AddWeeks(X,Y)</span></span> |<span data-ttu-id="75d8e-190">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="75d8e-190">X: DateTime</span></span><br/><br/><span data-ttu-id="75d8e-191">Y: int</span><span class="sxs-lookup"><span data-stu-id="75d8e-191">Y: int</span></span> |<span data-ttu-id="75d8e-192">추가 Y * 7 일 tooX</span><span class="sxs-lookup"><span data-stu-id="75d8e-192">Adds Y * 7 days tooX</span></span><br/><br/><span data-ttu-id="75d8e-193">예: 9/15/2013 12:00:00 PM + 1주 = 9/22/2013 12:00:00 PM</span><span class="sxs-lookup"><span data-stu-id="75d8e-193">Example: 9/15/2013 12:00:00 PM + 1 week = 9/22/2013 12:00:00 PM</span></span><br/><br/><span data-ttu-id="75d8e-194">Y를 음수로 지정하여 주도 뺄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-194">You can subtract weeks too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="75d8e-195">예: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="75d8e-195">Example: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="75d8e-196">Date</span><span class="sxs-lookup"><span data-stu-id="75d8e-196">Date</span></span> |<span data-ttu-id="75d8e-197">AddYears(X,Y)</span><span class="sxs-lookup"><span data-stu-id="75d8e-197">AddYears(X,Y)</span></span> |<span data-ttu-id="75d8e-198">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="75d8e-198">X: DateTime</span></span><br/><br/><span data-ttu-id="75d8e-199">Y: int</span><span class="sxs-lookup"><span data-stu-id="75d8e-199">Y: int</span></span> |<span data-ttu-id="75d8e-200">Y 년 tooX를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-200">Adds Y years tooX.</span></span><br/><br/>`Example: 9/15/2013 12:00:00 PM + 1 year = 9/15/2014 12:00:00 PM`<br/><br/><span data-ttu-id="75d8e-201">Y를 음수로 지정하여 년도 뺄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-201">You can subtract years too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="75d8e-202">예: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="75d8e-202">Example: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span></span> |
| <span data-ttu-id="75d8e-203">Date</span><span class="sxs-lookup"><span data-stu-id="75d8e-203">Date</span></span> |<span data-ttu-id="75d8e-204">Day(X)</span><span class="sxs-lookup"><span data-stu-id="75d8e-204">Day(X)</span></span> |<span data-ttu-id="75d8e-205">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="75d8e-205">X: DateTime</span></span> |<span data-ttu-id="75d8e-206">X의 hello 일 구성 요소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-206">Gets hello day component of X.</span></span><br/><br/><span data-ttu-id="75d8e-207">예: `Day of 9/15/2013 12:00:00 PM is 9`.</span><span class="sxs-lookup"><span data-stu-id="75d8e-207">Example: `Day of 9/15/2013 12:00:00 PM is 9`.</span></span> |
| <span data-ttu-id="75d8e-208">Date</span><span class="sxs-lookup"><span data-stu-id="75d8e-208">Date</span></span> |<span data-ttu-id="75d8e-209">DayOfWeek(X)</span><span class="sxs-lookup"><span data-stu-id="75d8e-209">DayOfWeek(X)</span></span> |<span data-ttu-id="75d8e-210">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="75d8e-210">X: DateTime</span></span> |<span data-ttu-id="75d8e-211">Hello 요일을 X의 요일 구성 요소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-211">Gets hello day of week component of X.</span></span><br/><br/><span data-ttu-id="75d8e-212">예: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span><span class="sxs-lookup"><span data-stu-id="75d8e-212">Example: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span></span> |
| <span data-ttu-id="75d8e-213">Date</span><span class="sxs-lookup"><span data-stu-id="75d8e-213">Date</span></span> |<span data-ttu-id="75d8e-214">DayOfYear(X)</span><span class="sxs-lookup"><span data-stu-id="75d8e-214">DayOfYear(X)</span></span> |<span data-ttu-id="75d8e-215">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="75d8e-215">X: DateTime</span></span> |<span data-ttu-id="75d8e-216">X의 hello 연도 구성 요소로 표시 되는 hello 연도 hello 날을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-216">Gets hello day in hello year represented by hello year component of X.</span></span><br/><br/><span data-ttu-id="75d8e-217">예제:</span><span class="sxs-lookup"><span data-stu-id="75d8e-217">Examples:</span></span><br/>`12/1/2015: day 335 of 2015`<br/>`12/31/2015: day 365 of 2015`<br/>`12/31/2016: day 366 of 2016 (Leap Year)` |
| <span data-ttu-id="75d8e-218">Date</span><span class="sxs-lookup"><span data-stu-id="75d8e-218">Date</span></span> |<span data-ttu-id="75d8e-219">DaysInMonth(X)</span><span class="sxs-lookup"><span data-stu-id="75d8e-219">DaysInMonth(X)</span></span> |<span data-ttu-id="75d8e-220">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="75d8e-220">X: DateTime</span></span> |<span data-ttu-id="75d8e-221">매개 변수 X의 hello 월 구성 요소로 표시 되는 hello 달의 hello 날짜를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-221">Gets hello days in hello month represented by hello month component of parameter X.</span></span><br/><br/><span data-ttu-id="75d8e-222">예: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in hello September month`.</span><span class="sxs-lookup"><span data-stu-id="75d8e-222">Example: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in hello September month`.</span></span> |
| <span data-ttu-id="75d8e-223">Date</span><span class="sxs-lookup"><span data-stu-id="75d8e-223">Date</span></span> |<span data-ttu-id="75d8e-224">EndOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="75d8e-224">EndOfDay(X)</span></span> |<span data-ttu-id="75d8e-225">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="75d8e-225">X: DateTime</span></span> |<span data-ttu-id="75d8e-226">Hello 날짜-시간 hello 쪽 X의 hello 날짜 (day 구성 요소)을 나타내는 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-226">Gets hello date-time that represents hello end of hello day (day component) of X.</span></span><br/><br/><span data-ttu-id="75d8e-227">예: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span><span class="sxs-lookup"><span data-stu-id="75d8e-227">Example: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span></span> |
| <span data-ttu-id="75d8e-228">Date</span><span class="sxs-lookup"><span data-stu-id="75d8e-228">Date</span></span> |<span data-ttu-id="75d8e-229">EndOfMonth(X)</span><span class="sxs-lookup"><span data-stu-id="75d8e-229">EndOfMonth(X)</span></span> |<span data-ttu-id="75d8e-230">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="75d8e-230">X: DateTime</span></span> |<span data-ttu-id="75d8e-231">매개 변수 X의 월 구성 요소로 표시 되는 hello 달의 hello 끝을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-231">Gets hello end of hello month represented by month component of parameter X.</span></span> <br/><br/><span data-ttu-id="75d8e-232">예: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (날짜 hello 9 월 말일을 나타내는 시간)</span><span class="sxs-lookup"><span data-stu-id="75d8e-232">Example: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (date time that represents hello end of September month)</span></span> |
| <span data-ttu-id="75d8e-233">Date</span><span class="sxs-lookup"><span data-stu-id="75d8e-233">Date</span></span> |<span data-ttu-id="75d8e-234">StartOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="75d8e-234">StartOfDay(X)</span></span> |<span data-ttu-id="75d8e-235">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="75d8e-235">X: DateTime</span></span> |<span data-ttu-id="75d8e-236">매개 변수 X의 hello 일 구성 요소로 표시 되는 hello 하루의 hello 시작을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-236">Gets hello start of hello day represented by hello day component of parameter X.</span></span><br/><br/><span data-ttu-id="75d8e-237">예: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span><span class="sxs-lookup"><span data-stu-id="75d8e-237">Example: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span></span> |
| <span data-ttu-id="75d8e-238">DateTime</span><span class="sxs-lookup"><span data-stu-id="75d8e-238">DateTime</span></span> |<span data-ttu-id="75d8e-239">From(X)</span><span class="sxs-lookup"><span data-stu-id="75d8e-239">From(X)</span></span> |<span data-ttu-id="75d8e-240">X: String</span><span class="sxs-lookup"><span data-stu-id="75d8e-240">X: String</span></span> |<span data-ttu-id="75d8e-241">날짜 시간 X tooa 문자열을 구문 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-241">Parse string X tooa date time.</span></span> |
| <span data-ttu-id="75d8e-242">DateTime</span><span class="sxs-lookup"><span data-stu-id="75d8e-242">DateTime</span></span> |<span data-ttu-id="75d8e-243">Ticks(X)</span><span class="sxs-lookup"><span data-stu-id="75d8e-243">Ticks(X)</span></span> |<span data-ttu-id="75d8e-244">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="75d8e-244">X: DateTime</span></span> |<span data-ttu-id="75d8e-245">Hello 틱 hello 매개 변수 X의 속성을 가져옵니다. 1 개 틱에 100 나노초입니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-245">Gets hello ticks property of hello parameter X. One tick equals 100 nanoseconds.</span></span> <span data-ttu-id="75d8e-246">이 속성의 hello 값 hello 0001 년 1 월 1 일 12시: 00 자정 이후 경과 된 틱 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-246">hello value of this property represents hello number of ticks that have elapsed since 12:00:00 midnight, January 1, 0001.</span></span> |
| <span data-ttu-id="75d8e-247">텍스트</span><span class="sxs-lookup"><span data-stu-id="75d8e-247">Text</span></span> |<span data-ttu-id="75d8e-248">Format(X)</span><span class="sxs-lookup"><span data-stu-id="75d8e-248">Format(X)</span></span> |<span data-ttu-id="75d8e-249">X: String 변수</span><span class="sxs-lookup"><span data-stu-id="75d8e-249">X: String variable</span></span> |<span data-ttu-id="75d8e-250">형식 hello 텍스트 (사용 하 여 `\\'` 조합 tooescape `'` 문자)입니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-250">Formats hello text (use `\\'` combination tooescape `'` character).</span></span>|

> [!IMPORTANT]
> <span data-ttu-id="75d8e-251">다른 함수 내에서 함수를 사용 하는 경우 toouse 불필요  **$$**  hello 내부 함수에 대 한 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-251">When using a function within another function, you do not need toouse **$$** prefix for hello inner function.</span></span> <span data-ttu-id="75d8e-252">예: $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' 및 RowKey ge \\'{0: yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)).</span><span class="sxs-lookup"><span data-stu-id="75d8e-252">For example: $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' and RowKey ge \\'{0: yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)).</span></span> <span data-ttu-id="75d8e-253">이 예제에서는 알 수 있듯이  **$$**  접두사가 hello에 대 한 사용 되지 않으면 **Time.AddHours** 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-253">In this example, notice that **$$** prefix is not used for hello **Time.AddHours** function.</span></span> 

#### <a name="example"></a><span data-ttu-id="75d8e-254">예제</span><span class="sxs-lookup"><span data-stu-id="75d8e-254">Example</span></span>
<span data-ttu-id="75d8e-255">Hello hello Hive 작업에 대 한 다음 예제에서는 입력 및 출력 매개 변수는 hello를 사용 하 여 결정 됩니다 `Text.Format` 함수 및 시스템 변수 SliceStart 합니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-255">In hello following example, input and output parameters for hello Hive activity are determined by using hello `Text.Format` function and SliceStart system variable.</span></span> 

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

### <a name="example-2"></a><span data-ttu-id="75d8e-256">예 2</span><span class="sxs-lookup"><span data-stu-id="75d8e-256">Example 2</span></span>

<span data-ttu-id="75d8e-257">다음 예제는 hello, hello DateTime 매개 변수를 사용 하 여 저장 프로시저 작업 결정은 hello에 대 한 텍스트를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-257">In hello following example, hello DateTime parameter for hello Stored Procedure Activity is determined by using hello Text.</span></span> <span data-ttu-id="75d8e-258">Format 함수 및 변수 SliceStart hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="75d8e-258">Format function and hello SliceStart variable.</span></span> 

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

### <a name="example-3"></a><span data-ttu-id="75d8e-259">예 3</span><span class="sxs-lookup"><span data-stu-id="75d8e-259">Example 3</span></span>
<span data-ttu-id="75d8e-260">다음 예제는 hello와 같이 hello AddDays 함수를 사용 하는 hello SliceStart,으로 표시 되는 대신 이전 날짜의 tooread 데이터:</span><span class="sxs-lookup"><span data-stu-id="75d8e-260">tooread data from previous day instead of day represented by hello SliceStart, use hello AddDays function as shown in hello following example:</span></span> 

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

<span data-ttu-id="75d8e-261">사용할 수 있는 다른 서식 옵션을 설명하는 [사용자 지정 날짜 및 시간 형식 문자열](https://msdn.microsoft.com/library/8kb3ddd4.aspx) (예: yy 대 yyyy) 토픽을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75d8e-261">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: yy vs. yyyy).</span></span> 

