---
title: "aaaImport Azure Application Insights에서 사용자 데이터 tooAnalytics | Microsoft Docs"
description: "정적 데이터 toojoin 된 응용 프로그램 원격 분석 가져오거나 분석을 별도 데이터 스트림 tooquery 가져올 합니다."
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
ms.openlocfilehash: 7a3a3c9155adc1885dd366ddb13dda80bb894adb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="import-data-into-analytics"></a><span data-ttu-id="56b04-104">Analytics로 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="56b04-104">Import data into Analytics</span></span>

<span data-ttu-id="56b04-105">모든 테이블 형식 데이터를 가져올 [분석](app-insights-analytics.md), 어느 toojoin 사용 하 여 [Application Insights](app-insights-overview.md) 응용 프로그램에서 원격 분석 또는 별도 스트림으로 분석할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-105">Import any tabular data into [Analytics](app-insights-analytics.md), either toojoin it with [Application Insights](app-insights-overview.md) telemetry from your app, or so that you can analyze it as a separate stream.</span></span> <span data-ttu-id="56b04-106">분석은 원격 분석의 강력한 쿼리 언어 잘 맞는 tooanalyzing 대용량 타임 스탬프 스트림을입니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-106">Analytics is a powerful query language well-suited tooanalyzing high-volume timestamped streams of telemetry.</span></span>

<span data-ttu-id="56b04-107">사용자 고유의 스키마를 사용하여 Analytics로 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-107">You can import data into Analytics using your own schema.</span></span> <span data-ttu-id="56b04-108">요청 또는 추적 같은 toouse hello 표준 Application Insights 스키마 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-108">It doesn't have toouse hello standard Application Insights schemas such as request or trace.</span></span>

<span data-ttu-id="56b04-109">JSON 또는 DSV(구분 기호 쉼표, 세미콜론 또는 탭으로 구분된 값) 파일을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-109">You can import JSON or DSV (delimiter-separated values - comma, semicolon or tab) files.</span></span>

<span data-ttu-id="56b04-110">가지 tooAnalytics 가져오기는 유용한 세 가지 상황이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-110">There are three situations where importing tooAnalytics is useful:</span></span>

* <span data-ttu-id="56b04-111">**앱 원격 분석에 연결**</span><span class="sxs-lookup"><span data-stu-id="56b04-111">**Join with app telemetry.**</span></span> <span data-ttu-id="56b04-112">예를 들어 Url에서 웹 사이트 toomore 읽을 수 있는 페이지 제목에 매핑하는 테이블을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-112">For example, you could import a table that maps URLs from your website toomore readable page titles.</span></span> <span data-ttu-id="56b04-113">분석에서 웹 사이트의 hello 10 개의 가장 인기 있는 페이지를 보여 주는 대시보드 차트 보고서를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-113">In Analytics, you can create a dashboard chart report that shows hello ten most popular pages in your website.</span></span> <span data-ttu-id="56b04-114">이제 hello 페이지 제목 hello Url 대신 표시할 수 있어 합니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-114">Now it can show hello page titles instead of hello URLs.</span></span>
* <span data-ttu-id="56b04-115">**응용 프로그램 원격 분석**과 네트워크 트래픽, 서버 데이터 또는 CDN 로그 파일 등의 다른 소스 간에 상관 관계를 형성합니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-115">**Correlate your application telemetry** with other sources such as network traffic, server data, or CDN log files.</span></span>
* <span data-ttu-id="56b04-116">**분석 tooa 별도 데이터 스트림에 적용 됩니다.**</span><span class="sxs-lookup"><span data-stu-id="56b04-116">**Apply Analytics tooa separate data stream.**</span></span> <span data-ttu-id="56b04-117">Application Insights Analytics는 타임스탬프가 스파스 스트림에 잘 작동하는 강력한 도구로, 많은 경우에 SQL보다 훨씬 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-117">Application Insights Analytics is a powerful tool, that works well with sparse, timestamped streams - much better than SQL in many cases.</span></span> <span data-ttu-id="56b04-118">다른 소스에서 이러한 스트림이 제공되면 Analytics에서 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-118">If you have such a stream from some other source, you can analyze it with Analytics.</span></span>

<span data-ttu-id="56b04-119">보내는 데이터 tooyour 데이터 원본을 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-119">Sending data tooyour data source is easy.</span></span> 

1. <span data-ttu-id="56b04-120">(한 번) 데이터의 '데이터 원본' hello 스키마를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-120">(One time) Define hello schema of your data in a 'data source'.</span></span>
2. <span data-ttu-id="56b04-121">(주기적으로) 데이터 tooAzure 저장소에 업로드 하 고 새 데이터 수집에 대 한 기다리고 우리 hello REST API toonotify을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-121">(Periodically) Upload your data tooAzure storage, and call hello REST API toonotify us that new data is waiting for ingestion.</span></span> <span data-ttu-id="56b04-122">몇 분 안에 hello 데이터는 분석에서 쿼리를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-122">Within a few minutes, hello data is available for query in Analytics.</span></span>

<span data-ttu-id="56b04-123">hello hello 업로드 횟수가 정의 된 사용자에 의해 및 쿼리에 사용할 수 있는 사용자 데이터 toobe 시겠습니까 속도입니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-123">hello frequency of hello upload is defined by you and how fast would you like your data toobe available for queries.</span></span> <span data-ttu-id="56b04-124">1GB 보다 더 않고 더 큰 청크로 구성의 보다 효율적인 tooupload 데이터.</span><span class="sxs-lookup"><span data-stu-id="56b04-124">It is more efficient tooupload data in larger chunks, but not larger than 1GB.</span></span>

> [!NOTE]
> <span data-ttu-id="56b04-125">*다양 한 데이터 원본 tooanalyze 있으세요?*</span><span class="sxs-lookup"><span data-stu-id="56b04-125">*Got lots of data sources tooanalyze?*</span></span> [<span data-ttu-id="56b04-126">*사용 하는 것이 좋습니다* logstash *tooship Application Insights로 데이터입니다.*</span><span class="sxs-lookup"><span data-stu-id="56b04-126">*Consider using* logstash *tooship your data into Application Insights.*</span></span>](https://github.com/Microsoft/logstash-output-application-insights)
> 

## <a name="before-you-start"></a><span data-ttu-id="56b04-127">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="56b04-127">Before you start</span></span>

<span data-ttu-id="56b04-128">다음 작업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-128">You need:</span></span>

1. <span data-ttu-id="56b04-129">Microsoft Azure의 Application Insights 리소스.</span><span class="sxs-lookup"><span data-stu-id="56b04-129">An Application Insights resource in Microsoft Azure.</span></span>

 * <span data-ttu-id="56b04-130">Tooanalyze 다른 원격 분석에서 개별적으로 데이터를 원하는 경우 [새 Application Insights 리소스 만들기](app-insights-create-new-resource.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-130">If you want tooanalyze your data separately from any other telemetry, [create a new Application Insights resource](app-insights-create-new-resource.md).</span></span>
 * <span data-ttu-id="56b04-131">조인 또는 Application Insights로 이미 설정 하는 응용 프로그램에서 원격 분석을 사용 하 여 데이터를 비교 하는 경우 해당 앱에 대 한 hello 리소스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-131">If you're joining or comparing your data with telemetry from an app that is already set up with Application Insights, then you can use hello resource for that app.</span></span>
 * <span data-ttu-id="56b04-132">기여자 또는 소유자 액세스 toothat 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-132">Contributor or owner access toothat resource.</span></span>
 
2. <span data-ttu-id="56b04-133">Azure 저장소의 Blob을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-133">Azure storage.</span></span> <span data-ttu-id="56b04-134">TooAzure 저장소를 업로드 하 고 분석 여기에서 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-134">You upload tooAzure storage, and Analytics gets your data from there.</span></span> 

 * <span data-ttu-id="56b04-135">Blob에 대한 전용 저장소 계정을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-135">We recommend you create a dedicated storage account for your blobs.</span></span> <span data-ttu-id="56b04-136">Blob를 다른 프로세스와 공유 하는 경우 시간이 오래 걸리는 프로세스 tooread 취급에 대 한 blob입니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-136">If your blobs are shared with other processes, it takes longer for our processes tooread your blobs.</span></span>


## <a name="define-your-schema"></a><span data-ttu-id="56b04-137">스키마 정의</span><span class="sxs-lookup"><span data-stu-id="56b04-137">Define your schema</span></span>

<span data-ttu-id="56b04-138">데이터를 가져올 수 있습니다, 전에 정의 해야는 *데이터 소스* hello 데이터 스키마를 지정 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-138">Before you can import data, you must define a *data source,* which specifies hello schema of your data.</span></span>
<span data-ttu-id="56b04-139">Too50 데이터 원본에는 단일 Application Insights 리소스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-139">You can have up too50 data sources in a single Application Insights resource</span></span>

1. <span data-ttu-id="56b04-140">Hello 데이터 원본 마법사를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-140">Start hello data source wizard.</span></span> <span data-ttu-id="56b04-141">"새 데이터 원본 추가" 버튼을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-141">Use "Add new data source" button.</span></span> <span data-ttu-id="56b04-142">또는 오른쪽 위 모서리에서 설정 단추를 클릭하고 드롭다운 메뉴에서 "데이터 원본"을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-142">Alternatively - click on settings button in right upper corner and choose "Data Sources" in dropdown menu.</span></span>

    ![새 데이터 원본 추가](./media/app-insights-analytics-import/add-new-data-source.png)

    <span data-ttu-id="56b04-144">새 데이터 원본의 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-144">Provide a name for your new data source.</span></span>

2. <span data-ttu-id="56b04-145">업로드 하는 hello 파일의 형식을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-145">Define format of hello files that you will upload.</span></span>

    <span data-ttu-id="56b04-146">Hello 형식을 수동으로 정의 하거나 샘플 파일을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-146">You can either define hello format manually, or upload a sample file.</span></span>

    <span data-ttu-id="56b04-147">Hello 데이터가 CSV 형식의 이면 hello hello 샘플의 첫 번째 행에 열 머리글 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-147">If hello data is in CSV format, hello first row of hello sample can be column headers.</span></span> <span data-ttu-id="56b04-148">Hello 다음 단계에서 hello 필드 이름을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-148">You can change hello field names in hello next step.</span></span>

    <span data-ttu-id="56b04-149">hello 샘플 최소 10 개의 행 이나 데이터의 레코드에 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-149">hello sample should include at least 10 rows or records of data.</span></span>

    <span data-ttu-id="56b04-150">열 또는 필드 이름은 공백이나 문장 부호 없는 영숫자 이름이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-150">Column or field names should have alphanumeric names (without spaces or punctuation).</span></span>

    ![샘플 파일 업로드](./media/app-insights-analytics-import/sample-data-file.png)


3. <span data-ttu-id="56b04-152">마법사 hello 검토 hello 스키마 이었죠.</span><span class="sxs-lookup"><span data-stu-id="56b04-152">Review hello schema that hello wizard has got.</span></span> <span data-ttu-id="56b04-153">샘플에서 hello 형식 유추, 경우에 tooadjust 유추 hello 유형의 hello 열을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-153">If it inferred hello types from a sample, you might need tooadjust hello inferred types of hello columns.</span></span>

    ![검토 hello 유추 된 스키마](./media/app-insights-analytics-import/data-source-review-schema.png)

 * <span data-ttu-id="56b04-155">선택 사항입니다. 스키마 정의를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-155">(Optional.) Upload a schema definition.</span></span> <span data-ttu-id="56b04-156">다음과 같은 hello 형식을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="56b04-156">See hello format below.</span></span>

 * <span data-ttu-id="56b04-157">타임스탬프를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-157">Select a Timestamp.</span></span> <span data-ttu-id="56b04-158">Analytics의 모든 데이터에는 타임스탬프 필드가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-158">All data in Analytics must have a timestamp field.</span></span> <span data-ttu-id="56b04-159">형식이 있어야 `datetime`, 하지만 'timestamp' 라는 toobe 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-159">It must have type `datetime`, but it doesn't have toobe named 'timestamp'.</span></span> <span data-ttu-id="56b04-160">데이터 ISO 형식으로 시간과 날짜를 포함 하는 열이 있으면 hello 타임 스탬프 열으로 선택 하십시오.</span><span class="sxs-lookup"><span data-stu-id="56b04-160">If your data has a column containing a date and time in ISO format, choose this as hello timestamp column.</span></span> <span data-ttu-id="56b04-161">그렇지 않으면 "데이터로 도착"를 선택 하 고 hello 가져오기 프로세스는 타임 스탬프 필드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-161">Otherwise, choose "as data arrived", and hello import process will add a timestamp field.</span></span>

5. <span data-ttu-id="56b04-162">Hello 데이터 원본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-162">Create hello data source.</span></span>

### <a name="schema-definition-file-format"></a><span data-ttu-id="56b04-163">스키마 정의 파일 형식</span><span class="sxs-lookup"><span data-stu-id="56b04-163">Schema definition file format</span></span>

<span data-ttu-id="56b04-164">UI에 hello 스키마를 편집 하는 대신 hello 스키마 정의 파일에서 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-164">Instead of editing hello schema in UI, you can load hello schema definition from a file.</span></span> <span data-ttu-id="56b04-165">hello 스키마 정의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-165">hello schema definition format is as follows:</span></span> 

<span data-ttu-id="56b04-166">구분된 형식</span><span class="sxs-lookup"><span data-stu-id="56b04-166">Delimited format</span></span> 
```
[ 
    {"location": "0", "name": "RequestName", "type": "string"}, 
    {"location": "1", "name": "timestamp", "type": "datetime"}, 
    {"location": "2", "name": "IPAddress", "type": "string"} 
] 
```

<span data-ttu-id="56b04-167">JSON 형식</span><span class="sxs-lookup"><span data-stu-id="56b04-167">JSON format</span></span> 
```
[ 
    {"location": "$.name", "name": "name", "type": "string"}, 
    {"location": "$.alias", "name": "alias", "type": "string"}, 
    {"location": "$.room", "name": "room", "type": "long"} 
]
```
 
<span data-ttu-id="56b04-168">각 열은 hello 위치, 이름 및 유형으로 식별 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-168">Each column is identified by hello location, name and type.</span></span> 

* <span data-ttu-id="56b04-169">위치 – 구분 기호로 분리 된 파일 형식 지정에 대 한 hello 매핑된 값의 hello 위치는입니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-169">Location – For delimited file format it is hello position of hello mapped value.</span></span> <span data-ttu-id="56b04-170">JSON 형식으로 hello 매핑된 키의 hello jpath입니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-170">For JSON format, it is hello jpath of hello mapped key.</span></span>
* <span data-ttu-id="56b04-171">이름-hello hello 열의 이름을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-171">Name – hello displayed name of hello column.</span></span>
* <span data-ttu-id="56b04-172">형식 hello 해당 열의 데이터 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-172">Type – hello data type of that column.</span></span>
 
<span data-ttu-id="56b04-173">샘플 데이터를 사용 하 고 파일 형식을 구분에 경우 hello 스키마 정의 모든 열을 매핑할 하 고 hello 끝에 새 열을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-173">In case a sample data was used and file format is delimited, hello schema definition must map all columns and add new columns at hello end.</span></span> 

<span data-ttu-id="56b04-174">따라서 hello JSON 형식의 스키마 정의 없는 toomap 샘플 데이터에 있는 모든 키, JSON 데이터와 hello 부분 간의 매핑이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-174">JSON allows partial mapping of hello data, therefore hello schema definition of JSON format doesn’t have toomap every key which is found in a sample data.</span></span> <span data-ttu-id="56b04-175">Hello 샘플 데이터의 일부가 아닌 열은 매핑할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-175">It can also map columns which are not part of hello sample data.</span></span> 

## <a name="import-data"></a><span data-ttu-id="56b04-176">데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="56b04-176">Import data</span></span>

<span data-ttu-id="56b04-177">tooimport 데이터 tooAzure 저장소에 업로드 하 고,에 대 한 선택 키를 만들려면 다음 REST API 호출을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-177">tooimport data, you upload it tooAzure storage, create an access key for it, and then make a REST API call.</span></span>

![새 데이터 원본 추가](./media/app-insights-analytics-import/analytics-upload-process.png)

<span data-ttu-id="56b04-179">설정 자동화 된 시스템 toodo를 일정 한 간격 또는 프로세스를 수동으로 수행 하는 hello를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-179">You can perform hello following process manually, or set up an automated system toodo it at regular intervals.</span></span> <span data-ttu-id="56b04-180">이 단계를 보려면 toofollow 이러한 tooimport 하려는 데이터의 각 블록에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-180">You need toofollow these steps for each block of data you want tooimport.</span></span>

1. <span data-ttu-id="56b04-181">너무 hello 데이터 업로드[Azure blob 저장소](../storage/blobs/storage-dotnet-how-to-use-blobs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-181">Upload hello data too[Azure blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> 

 * <span data-ttu-id="56b04-182">Blob를 too1GB 압축 되지 않은 모든 크기 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-182">Blobs can be any size up too1GB uncompressed.</span></span> <span data-ttu-id="56b04-183">성능 측면에서는 수백 MB 단위의 큰 blob이 이상적입니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-183">Large blobs of hundreds of MB are ideal from a performance perspective.</span></span>
 * <span data-ttu-id="56b04-184">Gzip tooimprove 업로드 시간 및 hello 데이터 toobe 쿼리를 실행할 수에 대 한 대기 시간을 압축할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-184">You can compress it with Gzip tooimprove upload time and latency for hello data toobe available for query.</span></span> <span data-ttu-id="56b04-185">사용 하 여 hello `.gz` 파일 이름 확장명입니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-185">Use hello `.gz` filename extension.</span></span>
 * <span data-ttu-id="56b04-186">최상의 toouse 별도 저장소 계정을이 목적을 성능이 느려질 수 있으므로 서로 다른 서비스에서 tooavoid 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-186">It's best toouse a separate storage account for this purpose, tooavoid calls from different services slowing performance.</span></span>
 * <span data-ttu-id="56b04-187">자주 발생 하는 데이터를 보낼 때 몇 초 마다 좋습니다 toouse 두 개 이상의 성능상의 이유로 한 저장소 계정.</span><span class="sxs-lookup"><span data-stu-id="56b04-187">When sending data in high frequency, every few seconds, it is recommended toouse more than one storage account, for performance reasons.</span></span>

 
2. <span data-ttu-id="56b04-188">[Hello blob에 대 한 공유 액세스 서명 키를 만들](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-188">[Create a Shared Access Signature key for hello blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span></span> <span data-ttu-id="56b04-189">hello 키 1 일에 만료 기간이 고 읽기 권한을 부여 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-189">hello key should have an expiration period of one day and provide read access.</span></span>
3. <span data-ttu-id="56b04-190">REST 호출 toonotify 데이터를 기다리고 있는 Application Insights를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-190">Make a REST call toonotify Application Insights that data is waiting.</span></span>

 * <span data-ttu-id="56b04-191">끝점: `https://dc.services.visualstudio.com/v2/track`</span><span class="sxs-lookup"><span data-stu-id="56b04-191">Endpoint: `https://dc.services.visualstudio.com/v2/track`</span></span>
 * <span data-ttu-id="56b04-192">HTTP 메서드: POST</span><span class="sxs-lookup"><span data-stu-id="56b04-192">HTTP method: POST</span></span>
 * <span data-ttu-id="56b04-193">페이로드:</span><span class="sxs-lookup"><span data-stu-id="56b04-193">Payload:</span></span>

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

<span data-ttu-id="56b04-194">hello 자리 표시자는:</span><span class="sxs-lookup"><span data-stu-id="56b04-194">hello placeholders are:</span></span>

* <span data-ttu-id="56b04-195">`Blob URI with Shared Access Key`: 키를 만들기 위한 hello 프로시저에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-195">`Blob URI with Shared Access Key`: You get this from hello procedure for creating a key.</span></span> <span data-ttu-id="56b04-196">특정 toohello blob은</span><span class="sxs-lookup"><span data-stu-id="56b04-196">It is specific toohello blob.</span></span>
* <span data-ttu-id="56b04-197">`Schema ID`: hello에 정의 된 스키마에 대해 생성 된 스키마 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-197">`Schema ID`: hello schema ID generated for your defined schema.</span></span> <span data-ttu-id="56b04-198">이 blob의 데이터를 hello toohello 스키마를 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-198">hello data in this blob should conform toohello schema.</span></span>
* <span data-ttu-id="56b04-199">`DateTime`: hello 시간은 hello에 요청이 전송 될 UTC입니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-199">`DateTime`: hello time at which hello request is submitted, UTC.</span></span> <span data-ttu-id="56b04-200">허용되는 형식: ISO8601(예: "2016-01-01 13:45:01"), RFC822 ("Wed, 14 Dec 16 14:57:01 +0000"), RFC850 ("Wednesday, 14-Dec-16 14:57:00 UTC"), RFC1123 ("Wed, 14 Dec 2016 14:57:00 +0000").</span><span class="sxs-lookup"><span data-stu-id="56b04-200">We accept these formats: ISO8601 (like "2016-01-01 13:45:01"); RFC822 ("Wed, 14 Dec 16 14:57:01 +0000"); RFC850 ("Wednesday, 14-Dec-16 14:57:00 UTC"); RFC1123 ("Wed, 14 Dec 2016 14:57:00 +0000").</span></span>
* <span data-ttu-id="56b04-201">Application Insights 리소스의 `Instrumentation key`</span><span class="sxs-lookup"><span data-stu-id="56b04-201">`Instrumentation key` of your Application Insights resource.</span></span>

<span data-ttu-id="56b04-202">몇 분 후 hello 데이터를 분석에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-202">hello data is available in Analytics after a few minutes.</span></span>

## <a name="error-responses"></a><span data-ttu-id="56b04-203">오류 응답</span><span class="sxs-lookup"><span data-stu-id="56b04-203">Error responses</span></span>

* <span data-ttu-id="56b04-204">**400 잘못 된 요청**: 해당 hello 요청 페이로드가 잘못 되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-204">**400 bad request**: indicates that hello request payload is invalid.</span></span> <span data-ttu-id="56b04-205">다음을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="56b04-205">Check:</span></span>
 * <span data-ttu-id="56b04-206">올바른 계측 키</span><span class="sxs-lookup"><span data-stu-id="56b04-206">Correct instrumentation key.</span></span>
 * <span data-ttu-id="56b04-207">유효한 시간 값.</span><span class="sxs-lookup"><span data-stu-id="56b04-207">Valid time value.</span></span> <span data-ttu-id="56b04-208">UTC 이제 hello 시간 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-208">It should be hello time now in UTC.</span></span>
 * <span data-ttu-id="56b04-209">Hello 이벤트의 JSON toohello 스키마를 준수합니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-209">JSON of hello event conforms toohello schema.</span></span>
* <span data-ttu-id="56b04-210">**403**: 발송 한 hello blob에 액세스할 수 없으면입니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-210">**403 Forbidden**: hello blob you've sent is not accessible.</span></span> <span data-ttu-id="56b04-211">그 hello 공유 액세스 키가 유효 하 고 만료 되지 않았는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-211">Make sure that hello shared access key is valid and has not expired.</span></span>
* <span data-ttu-id="56b04-212">**404 찾을 수 없음**:</span><span class="sxs-lookup"><span data-stu-id="56b04-212">**404 Not Found**:</span></span>
 * <span data-ttu-id="56b04-213">hello blob이 존재 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-213">hello blob doesn't exist.</span></span>
 * <span data-ttu-id="56b04-214">hello 원본 Id가 잘못 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-214">hello sourceId is wrong.</span></span>

<span data-ttu-id="56b04-215">더 자세한 정보는 hello 응답 오류 메시지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-215">More detailed information is available in hello response error message.</span></span>


## <a name="sample-code"></a><span data-ttu-id="56b04-216">샘플 코드</span><span class="sxs-lookup"><span data-stu-id="56b04-216">Sample code</span></span>

<span data-ttu-id="56b04-217">이 코드 hello를 사용 하 여 [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) NuGet 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-217">This code uses hello [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) NuGet package.</span></span>

### <a name="classes"></a><span data-ttu-id="56b04-218">클래스</span><span class="sxs-lookup"><span data-stu-id="56b04-218">Classes</span></span>

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

### <a name="ingest-data"></a><span data-ttu-id="56b04-219">데이터 수집</span><span class="sxs-lookup"><span data-stu-id="56b04-219">Ingest data</span></span>

<span data-ttu-id="56b04-220">각 blob에 대한 이 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="56b04-220">Use this code for each blob.</span></span> 

```C#
   AnalyticsDataSourceClient client = new AnalyticsDataSourceClient(); 

   var ingestionRequest = new AnalyticsDataSourceIngestionRequest("iKey", "sourceId", "blobUrlWithSas"); 

   bool success = await client.RequestBlobIngestion(ingestionRequest);
```

## <a name="next-steps"></a><span data-ttu-id="56b04-221">다음 단계</span><span class="sxs-lookup"><span data-stu-id="56b04-221">Next steps</span></span>

* [<span data-ttu-id="56b04-222">로그 분석 쿼리 언어 hello 둘러보기</span><span class="sxs-lookup"><span data-stu-id="56b04-222">Tour of hello Log Analytics query language</span></span>](app-insights-analytics-tour.md)
* [<span data-ttu-id="56b04-223">사용 하 여 *Logstash* toosend 데이터 tooApplication Insights</span><span class="sxs-lookup"><span data-stu-id="56b04-223">Use *Logstash* toosend data tooApplication Insights</span></span>](https://github.com/Microsoft/logstash-output-application-insights)
