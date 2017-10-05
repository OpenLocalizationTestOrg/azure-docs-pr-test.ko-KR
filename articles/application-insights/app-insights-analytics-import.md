---
title: "Azure Application Insights의 Analytics로 데이터 가져오기 | Microsoft Docs"
description: "앱 원격 분석에 연결할 정적 데이터를 가져오거나 Analytics로 쿼리할 별도 데이터 스트림을 가져옵니다."
services: application-insights
keywords: "개방형 스키마, 데이터 가져오기"
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: bwren
ms.openlocfilehash: aa855a9050ec4e5e7c5db88b7209b8bb48bdba51
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="import-data-into-analytics"></a><span data-ttu-id="f6c27-104">Analytics로 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="f6c27-104">Import data into Analytics</span></span>

<span data-ttu-id="f6c27-105">테이블 형식 데이터를 [Analytics](app-insights-analytics.md)로 가져와 앱의 [Application Insights](app-insights-overview.md) 원격 분석과 연결하거나 별도 스트림으로 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-105">Import any tabular data into [Analytics](app-insights-analytics.md), either to join it with [Application Insights](app-insights-overview.md) telemetry from your app, or so that you can analyze it as a separate stream.</span></span> <span data-ttu-id="f6c27-106">Analytics는 타임스탬프가 지정된 고용량 원격 분석 스트림을 분석하는 데 적합한 강력한 쿼리 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-106">Analytics is a powerful query language well-suited to analyzing high-volume timestamped streams of telemetry.</span></span>

<span data-ttu-id="f6c27-107">사용자 고유의 스키마를 사용하여 Analytics로 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-107">You can import data into Analytics using your own schema.</span></span> <span data-ttu-id="f6c27-108">요청 또는 추적과 같은 표준 Application Insights 스키마를 사용할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-108">It doesn't have to use the standard Application Insights schemas such as request or trace.</span></span>

<span data-ttu-id="f6c27-109">JSON 또는 DSV(구분 기호 쉼표, 세미콜론 또는 탭으로 구분된 값) 파일을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-109">You can import JSON or DSV (delimiter-separated values - comma, semicolon or tab) files.</span></span>

<span data-ttu-id="f6c27-110">다음과 같은 세 가지 상황에서는 Analytics로 가져오는 것이 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-110">There are three situations where importing to Analytics is useful:</span></span>

* <span data-ttu-id="f6c27-111">**앱 원격 분석에 연결**</span><span class="sxs-lookup"><span data-stu-id="f6c27-111">**Join with app telemetry.**</span></span> <span data-ttu-id="f6c27-112">예를 들어 웹 사이트의 URL을 좀 더 읽기 쉬운 페이지 제목에 매핑하는 테이블을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-112">For example, you could import a table that maps URLs from your website to more readable page titles.</span></span> <span data-ttu-id="f6c27-113">Analytics에서 웹 사이트의 가장 인기 있는 10개 페이지를 표시하는 대시보드 차트 보고서를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-113">In Analytics, you can create a dashboard chart report that shows the ten most popular pages in your website.</span></span> <span data-ttu-id="f6c27-114">이제 URL 대신 페이지 제목을 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-114">Now it can show the page titles instead of the URLs.</span></span>
* <span data-ttu-id="f6c27-115">**응용 프로그램 원격 분석**과 네트워크 트래픽, 서버 데이터 또는 CDN 로그 파일 등의 다른 소스 간에 상관 관계를 형성합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-115">**Correlate your application telemetry** with other sources such as network traffic, server data, or CDN log files.</span></span>
* <span data-ttu-id="f6c27-116">**별도 데이터 스트림에 Analytics를 적용합니다.**</span><span class="sxs-lookup"><span data-stu-id="f6c27-116">**Apply Analytics to a separate data stream.**</span></span> <span data-ttu-id="f6c27-117">Application Insights Analytics는 타임스탬프가 스파스 스트림에 잘 작동하는 강력한 도구로, 많은 경우에 SQL보다 훨씬 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-117">Application Insights Analytics is a powerful tool, that works well with sparse, timestamped streams - much better than SQL in many cases.</span></span> <span data-ttu-id="f6c27-118">다른 소스에서 이러한 스트림이 제공되면 Analytics에서 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-118">If you have such a stream from some other source, you can analyze it with Analytics.</span></span>

<span data-ttu-id="f6c27-119">데이터 원본에 데이터를 보내는 것은 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-119">Sending data to your data source is easy.</span></span> 

1. <span data-ttu-id="f6c27-120">(한 번) '데이터 원본'에 데이터의 스키마를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-120">(One time) Define the schema of your data in a 'data source'.</span></span>
2. <span data-ttu-id="f6c27-121">(주기적으로) Azure Storage로 데이터를 업로드하고, REST API를 호출하여 새 데이터가 수집을 위해 대기 중임을 알립니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-121">(Periodically) Upload your data to Azure storage, and call the REST API to notify us that new data is waiting for ingestion.</span></span> <span data-ttu-id="f6c27-122">몇 분 내에 Analytics에서 해당 데이터를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-122">Within a few minutes, the data is available for query in Analytics.</span></span>

<span data-ttu-id="f6c27-123">업로드 빈도는 쿼리에 데이터를 얼마나 빠르게 사용하고 싶은지에 따라 사용자가 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-123">The frequency of the upload is defined by you and how fast would you like your data to be available for queries.</span></span> <span data-ttu-id="f6c27-124">더 큰 청크로 데이터를 업로드하는 것이 좀 더 효율적이지만 1GB보다 크지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-124">It is more efficient to upload data in larger chunks, but not larger than 1GB.</span></span>

> [!NOTE]
> <span data-ttu-id="f6c27-125">*분석할 많은 데이터 원본이 있나요?*</span><span class="sxs-lookup"><span data-stu-id="f6c27-125">*Got lots of data sources to analyze?*</span></span> [<span data-ttu-id="f6c27-126">logstash*를 사용하여 Application Insights로 데이터를 전달하는 것을 고려하세요.*</span><span class="sxs-lookup"><span data-stu-id="f6c27-126">*Consider using* logstash *to ship your data into Application Insights.*</span></span>](https://github.com/Microsoft/logstash-output-application-insights)
> 

## <a name="before-you-start"></a><span data-ttu-id="f6c27-127">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="f6c27-127">Before you start</span></span>

<span data-ttu-id="f6c27-128">다음 작업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-128">You need:</span></span>

1. <span data-ttu-id="f6c27-129">Microsoft Azure의 Application Insights 리소스.</span><span class="sxs-lookup"><span data-stu-id="f6c27-129">An Application Insights resource in Microsoft Azure.</span></span>

 * <span data-ttu-id="f6c27-130">다른 원격 분석과 별도로 데이터를 분석하려는 경우 [새 Application Insights 리소스를 만듭니다](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="f6c27-130">If you want to analyze your data separately from any other telemetry, [create a new Application Insights resource](app-insights-create-new-resource.md).</span></span>
 * <span data-ttu-id="f6c27-131">이미 Application Insights로 설정된 앱에서 원격 분석에 데이터를 연결하거나 데이터를 비교하는 경우 해당 앱의 리소스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-131">If you're joining or comparing your data with telemetry from an app that is already set up with Application Insights, then you can use the resource for that app.</span></span>
 * <span data-ttu-id="f6c27-132">해당 리소스에 대한 참가자 또는 소유자 액세스 권한</span><span class="sxs-lookup"><span data-stu-id="f6c27-132">Contributor or owner access to that resource.</span></span>
 
2. <span data-ttu-id="f6c27-133">Azure 저장소의 Blob을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-133">Azure storage.</span></span> <span data-ttu-id="f6c27-134">Azure Storage에 업로드하면 Analytics가 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-134">You upload to Azure storage, and Analytics gets your data from there.</span></span> 

 * <span data-ttu-id="f6c27-135">Blob에 대한 전용 저장소 계정을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-135">We recommend you create a dedicated storage account for your blobs.</span></span> <span data-ttu-id="f6c27-136">Blob이 다른 프로세스와 공유되면 프로세스에서 blob을 읽는 데 더 오래 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-136">If your blobs are shared with other processes, it takes longer for our processes to read your blobs.</span></span>


## <a name="define-your-schema"></a><span data-ttu-id="f6c27-137">스키마 정의</span><span class="sxs-lookup"><span data-stu-id="f6c27-137">Define your schema</span></span>

<span data-ttu-id="f6c27-138">데이터를 가져오려면 데이터 스키마를 지정하는 *데이터 원본*를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-138">Before you can import data, you must define a *data source,* which specifies the schema of your data.</span></span>
<span data-ttu-id="f6c27-139">단일 Application Insights 리소스에 최대 50개의 데이터 원본을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-139">You can have up to 50 data sources in a single Application Insights resource</span></span>

1. <span data-ttu-id="f6c27-140">데이터 원본 마법사를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-140">Start the data source wizard.</span></span> <span data-ttu-id="f6c27-141">"새 데이터 원본 추가" 버튼을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-141">Use "Add new data source" button.</span></span> <span data-ttu-id="f6c27-142">또는 오른쪽 위 모서리에서 설정 단추를 클릭하고 드롭다운 메뉴에서 "데이터 원본"을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-142">Alternatively - click on settings button in right upper corner and choose "Data Sources" in dropdown menu.</span></span>

    ![새 데이터 원본 추가](./media/app-insights-analytics-import/add-new-data-source.png)

    <span data-ttu-id="f6c27-144">새 데이터 원본의 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-144">Provide a name for your new data source.</span></span>

2. <span data-ttu-id="f6c27-145">업로드할 파일의 형식을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-145">Define format of the files that you will upload.</span></span>

    <span data-ttu-id="f6c27-146">형식을 수동으로 정의하거나 샘플 파일을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-146">You can either define the format manually, or upload a sample file.</span></span>

    <span data-ttu-id="f6c27-147">데이터가 CSV 형식인 경우 이 샘플의 첫 번째 행은 열 머리글일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-147">If the data is in CSV format, the first row of the sample can be column headers.</span></span> <span data-ttu-id="f6c27-148">다음 단계에서 필드 이름을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-148">You can change the field names in the next step.</span></span>

    <span data-ttu-id="f6c27-149">샘플은 10개 이상의 데이터 행 또는 레코드를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-149">The sample should include at least 10 rows or records of data.</span></span>

    <span data-ttu-id="f6c27-150">열 또는 필드 이름은 공백이나 문장 부호 없는 영숫자 이름이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-150">Column or field names should have alphanumeric names (without spaces or punctuation).</span></span>

    ![샘플 파일 업로드](./media/app-insights-analytics-import/sample-data-file.png)


3. <span data-ttu-id="f6c27-152">마법사가 제공하는 스키마를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-152">Review the schema that the wizard has got.</span></span> <span data-ttu-id="f6c27-153">샘플에서 형식을 유추한 경우 유추된 열 형식을 조정해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-153">If it inferred the types from a sample, you might need to adjust the inferred types of the columns.</span></span>

    ![유추된 스키마 검토](./media/app-insights-analytics-import/data-source-review-schema.png)

 * <span data-ttu-id="f6c27-155">선택 사항입니다. 스키마 정의를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-155">(Optional.) Upload a schema definition.</span></span> <span data-ttu-id="f6c27-156">아래 형식을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f6c27-156">See the format below.</span></span>

 * <span data-ttu-id="f6c27-157">타임스탬프를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-157">Select a Timestamp.</span></span> <span data-ttu-id="f6c27-158">Analytics의 모든 데이터에는 타임스탬프 필드가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-158">All data in Analytics must have a timestamp field.</span></span> <span data-ttu-id="f6c27-159">`datetime` 형식이어야 하지만 이름이 'timestamp'일 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-159">It must have type `datetime`, but it doesn't have to be named 'timestamp'.</span></span> <span data-ttu-id="f6c27-160">데이터에 ISO 형식의 날짜 및 시간을 포함하는 열이 있는 경우 이 열을 타임스탬프 열로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-160">If your data has a column containing a date and time in ISO format, choose this as the timestamp column.</span></span> <span data-ttu-id="f6c27-161">그렇지 않으면 "데이터 도착 시"를 선택합니다. 그러면 가져오기 프로세스가 타임스탬프 필드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-161">Otherwise, choose "as data arrived", and the import process will add a timestamp field.</span></span>

5. <span data-ttu-id="f6c27-162">데이터 원본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-162">Create the data source.</span></span>

### <a name="schema-definition-file-format"></a><span data-ttu-id="f6c27-163">스키마 정의 파일 형식</span><span class="sxs-lookup"><span data-stu-id="f6c27-163">Schema definition file format</span></span>

<span data-ttu-id="f6c27-164">UI에서 스키마를 편집하는 대신 파일에서 스키마 정의를 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-164">Instead of editing the schema in UI, you can load the schema definition from a file.</span></span> <span data-ttu-id="f6c27-165">스키마 정의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-165">The schema definition format is as follows:</span></span> 

<span data-ttu-id="f6c27-166">구분된 형식</span><span class="sxs-lookup"><span data-stu-id="f6c27-166">Delimited format</span></span> 
```
[ 
    {"location": "0", "name": "RequestName", "type": "string"}, 
    {"location": "1", "name": "timestamp", "type": "datetime"}, 
    {"location": "2", "name": "IPAddress", "type": "string"} 
] 
```

<span data-ttu-id="f6c27-167">JSON 형식</span><span class="sxs-lookup"><span data-stu-id="f6c27-167">JSON format</span></span> 
```
[ 
    {"location": "$.name", "name": "name", "type": "string"}, 
    {"location": "$.alias", "name": "alias", "type": "string"}, 
    {"location": "$.room", "name": "room", "type": "long"} 
]
```
 
<span data-ttu-id="f6c27-168">각 열은 위치, 이름 및 형식으로 식별됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-168">Each column is identified by the location, name and type.</span></span> 

* <span data-ttu-id="f6c27-169">위치 – 구분된 파일 형식인 경우 매핑된 값의 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-169">Location – For delimited file format it is the position of the mapped value.</span></span> <span data-ttu-id="f6c27-170">JSON 형식인 경우 매핑된 키의 jpath입니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-170">For JSON format, it is the jpath of the mapped key.</span></span>
* <span data-ttu-id="f6c27-171">이름 - 열의 표시 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-171">Name – the displayed name of the column.</span></span>
* <span data-ttu-id="f6c27-172">유형 – 해당 열의 데이터 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-172">Type – the data type of that column.</span></span>
 
<span data-ttu-id="f6c27-173">샘플 데이터가 사용되었고 파일 형식이 구분된 경우 스키마 정의에서 모든 열을 매핑하고 마지막에 새 열을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-173">In case a sample data was used and file format is delimited, the schema definition must map all columns and add new columns at the end.</span></span> 

<span data-ttu-id="f6c27-174">JSON은 데이터의 부분 매핑을 허용합니다. 따라서 JSON 형식의 스키마 정의가 샘플 데이터에서 발견되는 모든 키를 매핑할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-174">JSON allows partial mapping of the data, therefore the schema definition of JSON format doesn’t have to map every key which is found in a sample data.</span></span> <span data-ttu-id="f6c27-175">샘플 데이터에 포함되지 않은 열도 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-175">It can also map columns which are not part of the sample data.</span></span> 

## <a name="import-data"></a><span data-ttu-id="f6c27-176">데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="f6c27-176">Import data</span></span>

<span data-ttu-id="f6c27-177">데이터를 가져오려면 Azure Storage로 업로드하고, 액세스 키를 만든 다음 REST API 호출을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-177">To import data, you upload it to Azure storage, create an access key for it, and then make a REST API call.</span></span>

![새 데이터 원본 추가](./media/app-insights-analytics-import/analytics-upload-process.png)

<span data-ttu-id="f6c27-179">다음 프로세스를 수동으로 수행하거나 정기적으로 수행하도록 자동화 시스템을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-179">You can perform the following process manually, or set up an automated system to do it at regular intervals.</span></span> <span data-ttu-id="f6c27-180">가져올 데이터의 각 블록에 대해 이러한 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-180">You need to follow these steps for each block of data you want to import.</span></span>

1. <span data-ttu-id="f6c27-181">[Azure Blob Storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md)에 데이터를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-181">Upload the data to [Azure blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> 

 * <span data-ttu-id="f6c27-182">Blob은 압축하지 않은 상태로 최대 1GB 크기일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-182">Blobs can be any size up to 1GB uncompressed.</span></span> <span data-ttu-id="f6c27-183">성능 측면에서는 수백 MB 단위의 큰 blob이 이상적입니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-183">Large blobs of hundreds of MB are ideal from a performance perspective.</span></span>
 * <span data-ttu-id="f6c27-184">데이터를 쿼리에 사용하기 위해 Gzip으로 압축하여 업로드 시간 및 대기 시간을 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-184">You can compress it with Gzip to improve upload time and latency for the data to be available for query.</span></span> <span data-ttu-id="f6c27-185">`.gz` 파일 이름 확장명을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-185">Use the `.gz` filename extension.</span></span>
 * <span data-ttu-id="f6c27-186">여러 서비스의 호출로 인해 성능이 저하되는 것을 방지하려면 이 용도에 별도의 저장소 계정을 사용하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-186">It's best to use a separate storage account for this purpose, to avoid calls from different services slowing performance.</span></span>
 * <span data-ttu-id="f6c27-187">데이터를 몇 초 단위로 매우 자주 전송할 때는 성능상의 이유로 둘 이상의 저장소 계정을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-187">When sending data in high frequency, every few seconds, it is recommended to use more than one storage account, for performance reasons.</span></span>

 
2. <span data-ttu-id="f6c27-188">[Blob에 대한 공유 액세스 서명 키를 생성합니다](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span><span class="sxs-lookup"><span data-stu-id="f6c27-188">[Create a Shared Access Signature key for the blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span></span> <span data-ttu-id="f6c27-189">이 키는 만료 기간이 1일이고 읽기 액세스 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-189">The key should have an expiration period of one day and provide read access.</span></span>
3. <span data-ttu-id="f6c27-190">데이터가 대기 중임을 Application Insights에 알리기 위해 REST 호출을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-190">Make a REST call to notify Application Insights that data is waiting.</span></span>

 * <span data-ttu-id="f6c27-191">끝점: `https://dc.services.visualstudio.com/v2/track`</span><span class="sxs-lookup"><span data-stu-id="f6c27-191">Endpoint: `https://dc.services.visualstudio.com/v2/track`</span></span>
 * <span data-ttu-id="f6c27-192">HTTP 메서드: POST</span><span class="sxs-lookup"><span data-stu-id="f6c27-192">HTTP method: POST</span></span>
 * <span data-ttu-id="f6c27-193">페이로드:</span><span class="sxs-lookup"><span data-stu-id="f6c27-193">Payload:</span></span>

```JSON

    {
       "data": {
            "baseType":"OpenSchemaData",
            "baseData":{
               "ver":"2",
               "blobSasUri":"<Blob URI with Shared Access Key>",
               "sourceName":"<Schema ID>",
               "sourceVersion":"1.0"
             }
       },
       "ver":1,
       "name":"Microsoft.ApplicationInsights.OpenSchema",
       "time":"<DateTime>",
       "iKey":"<instrumentation key>"
    }
```

<span data-ttu-id="f6c27-194">자리 표시자:</span><span class="sxs-lookup"><span data-stu-id="f6c27-194">The placeholders are:</span></span>

* <span data-ttu-id="f6c27-195">`Blob URI with Shared Access Key`: 키를 만들기 위한 절차에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-195">`Blob URI with Shared Access Key`: You get this from the procedure for creating a key.</span></span> <span data-ttu-id="f6c27-196">Blob에 국한됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-196">It is specific to the blob.</span></span>
* <span data-ttu-id="f6c27-197">`Schema ID`: 정의된 스키마에 대해 생성된 스키마 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-197">`Schema ID`: The schema ID generated for your defined schema.</span></span> <span data-ttu-id="f6c27-198">이 blob의 데이터는 스키마를 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-198">The data in this blob should conform to the schema.</span></span>
* <span data-ttu-id="f6c27-199">`DateTime`: 요청이 제출된 시간(UTC).</span><span class="sxs-lookup"><span data-stu-id="f6c27-199">`DateTime`: The time at which the request is submitted, UTC.</span></span> <span data-ttu-id="f6c27-200">허용되는 형식: ISO8601(예: "2016-01-01 13:45:01"), RFC822 ("Wed, 14 Dec 16 14:57:01 +0000"), RFC850 ("Wednesday, 14-Dec-16 14:57:00 UTC"), RFC1123 ("Wed, 14 Dec 2016 14:57:00 +0000").</span><span class="sxs-lookup"><span data-stu-id="f6c27-200">We accept these formats: ISO8601 (like "2016-01-01 13:45:01"); RFC822 ("Wed, 14 Dec 16 14:57:01 +0000"); RFC850 ("Wednesday, 14-Dec-16 14:57:00 UTC"); RFC1123 ("Wed, 14 Dec 2016 14:57:00 +0000").</span></span>
* <span data-ttu-id="f6c27-201">Application Insights 리소스의 `Instrumentation key`</span><span class="sxs-lookup"><span data-stu-id="f6c27-201">`Instrumentation key` of your Application Insights resource.</span></span>

<span data-ttu-id="f6c27-202">몇 분 후에 Analytics에서 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-202">The data is available in Analytics after a few minutes.</span></span>

## <a name="error-responses"></a><span data-ttu-id="f6c27-203">오류 응답</span><span class="sxs-lookup"><span data-stu-id="f6c27-203">Error responses</span></span>

* <span data-ttu-id="f6c27-204">**400 잘못된 요청**: 요청 페이로드가 잘못되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-204">**400 bad request**: indicates that the request payload is invalid.</span></span> <span data-ttu-id="f6c27-205">다음을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="f6c27-205">Check:</span></span>
 * <span data-ttu-id="f6c27-206">올바른 계측 키</span><span class="sxs-lookup"><span data-stu-id="f6c27-206">Correct instrumentation key.</span></span>
 * <span data-ttu-id="f6c27-207">유효한 시간 값.</span><span class="sxs-lookup"><span data-stu-id="f6c27-207">Valid time value.</span></span> <span data-ttu-id="f6c27-208">현재 시간(UTC)이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-208">It should be the time now in UTC.</span></span>
 * <span data-ttu-id="f6c27-209">이벤트의 JSON이 스키마를 준수합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-209">JSON of the event conforms to the schema.</span></span>
* <span data-ttu-id="f6c27-210">**403 사용 권한 없음**: 전송한 Blob에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-210">**403 Forbidden**: The blob you've sent is not accessible.</span></span> <span data-ttu-id="f6c27-211">공유 액세스 키가 유효한지와 만료되지 않았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-211">Make sure that the shared access key is valid and has not expired.</span></span>
* <span data-ttu-id="f6c27-212">**404 찾을 수 없음**:</span><span class="sxs-lookup"><span data-stu-id="f6c27-212">**404 Not Found**:</span></span>
 * <span data-ttu-id="f6c27-213">Blob이 존재하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-213">The blob doesn't exist.</span></span>
 * <span data-ttu-id="f6c27-214">SourceId가 잘못되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-214">The sourceId is wrong.</span></span>

<span data-ttu-id="f6c27-215">응답 오류 메시지에서 좀 더 자세한 정보를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-215">More detailed information is available in the response error message.</span></span>


## <a name="sample-code"></a><span data-ttu-id="f6c27-216">샘플 코드</span><span class="sxs-lookup"><span data-stu-id="f6c27-216">Sample code</span></span>

<span data-ttu-id="f6c27-217">이 코드는 [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) NuGet 패키지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-217">This code uses the [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) NuGet package.</span></span>

### <a name="classes"></a><span data-ttu-id="f6c27-218">클래스</span><span class="sxs-lookup"><span data-stu-id="f6c27-218">Classes</span></span>

```C#
namespace IngestionClient 
{ 
    using System; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceIngestionRequest 
    { 
        #region Members 
        private const string BaseDataRequiredVersion = "2"; 
        private const string RequestName = "Microsoft.ApplicationInsights.OpenSchema"; 
        #endregion Members 

        public AnalyticsDataSourceIngestionRequest(string ikey, string schemaId, string blobSasUri, int version = 1) 
        { 
            Ver = version; 
            IKey = ikey; 
            Data = new Data 
            { 
                BaseData = new BaseData 
                { 
                    Ver = BaseDataRequiredVersion, 
                    BlobSasUri = blobSasUri, 
                    SourceName = schemaId, 
                    SourceVersion = version.ToString() 
                } 
            }; 
        } 


        [JsonProperty("data")] 
        public Data Data { get; set; } 

        [JsonProperty("ver")] 
        public int Ver { get; set; } 

        [JsonProperty("name")] 
        public string Name { get { return RequestName; } } 

        [JsonProperty("time")] 
        public DateTime Time { get { return DateTime.UtcNow; } } 

        [JsonProperty("iKey")] 
        public string IKey { get; set; } 
    } 

    #region Internal Classes 

    public class Data 
    { 
        private const string DataBaseType = "OpenSchemaData"; 

        [JsonProperty("baseType")] 
        public string BaseType 
        { 
            get { return DataBaseType; } 
        } 

        [JsonProperty("baseData")] 
        public BaseData BaseData { get; set; } 
    } 


    public class BaseData 
    { 
        [JsonProperty("ver")] 
        public string Ver { get; set; } 

        [JsonProperty("blobSasUri")] 
        public string BlobSasUri { get; set; } 

        [JsonProperty("sourceName")] 
        public string SourceName { get; set; } 

        [JsonProperty("sourceVersion")] 
        public string SourceVersion { get; set; } 
    } 

    #endregion Internal Classes 
} 


namespace IngestionClient 
{ 
    using System; 
    using System.IO; 
    using System.Net; 
    using System.Text; 
    using System.Threading.Tasks; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceClient 
    { 
        #region Members 
        private readonly Uri endpoint = new Uri("https://dc.services.visualstudio.com/v2/track"); 
        private const string RequestContentType = "application/json; charset=UTF-8"; 
        private const string RequestAccess = "application/json"; 
        #endregion Members 

        #region Public 

        public async Task<bool> RequestBlobIngestion(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            HttpWebRequest request = WebRequest.CreateHttp(endpoint); 
            request.Method = WebRequestMethods.Http.Post; 
            request.ContentType = RequestContentType; 
            request.Accept = RequestAccess; 

            string notificationJson = Serialize(ingestionRequest); 
            byte[] notificationBytes = GetContentBytes(notificationJson); 
            request.ContentLength = notificationBytes.Length; 

            Stream requestStream = request.GetRequestStream(); 
            requestStream.Write(notificationBytes, 0, notificationBytes.Length); 
            requestStream.Close(); 

            try 
            { 
                using (var response = (HttpWebResponse)await request.GetResponseAsync())
                {
                    return response.StatusCode == HttpStatusCode.OK;
                }
            } 
            catch (WebException e) 
            { 
                HttpWebResponse httpResponse = e.Response as HttpWebResponse; 
                if (httpResponse != null) 
                { 
                    Console.WriteLine( 
                        "Ingestion request failed with status code: {0}. Error: {1}", 
                        httpResponse.StatusCode, 
                        httpResponse.StatusDescription); 
                    return false; 
                }
                throw; 
            } 
        } 
        #endregion Public 

        #region Private 
        private byte[] GetContentBytes(string content) 
        { 
            return Encoding.UTF8.GetBytes(content);
        } 


        private string Serialize(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            return JsonConvert.SerializeObject(ingestionRequest); 
        } 
        #endregion Private 
    } 
} 
```

### <a name="ingest-data"></a><span data-ttu-id="f6c27-219">데이터 수집</span><span class="sxs-lookup"><span data-stu-id="f6c27-219">Ingest data</span></span>

<span data-ttu-id="f6c27-220">각 blob에 대한 이 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f6c27-220">Use this code for each blob.</span></span> 

```C#
   AnalyticsDataSourceClient client = new AnalyticsDataSourceClient(); 

   var ingestionRequest = new AnalyticsDataSourceIngestionRequest("iKey", "sourceId", "blobUrlWithSas"); 

   bool success = await client.RequestBlobIngestion(ingestionRequest);
```

## <a name="next-steps"></a><span data-ttu-id="f6c27-221">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f6c27-221">Next steps</span></span>

* [<span data-ttu-id="f6c27-222">Log Analytics 쿼리 언어 둘러보기</span><span class="sxs-lookup"><span data-stu-id="f6c27-222">Tour of the Log Analytics query language</span></span>](app-insights-analytics-tour.md)
* [<span data-ttu-id="f6c27-223">*Logstash*를 사용하여 Application Insights에 데이터 전송</span><span class="sxs-lookup"><span data-stu-id="f6c27-223">Use *Logstash* to send data to Application Insights</span></span>](https://github.com/Microsoft/logstash-output-application-insights)
