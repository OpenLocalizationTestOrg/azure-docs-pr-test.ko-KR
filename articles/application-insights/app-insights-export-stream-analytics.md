---
title: "Azure Application Insights에서 스트림 분석을 사용 하 여 aaaExport | Microsoft Docs"
description: "스트림 분석 지속적으로 변형할 수, Application Insights에서 내보내는 hello 데이터 필터 및 경로입니다."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 31594221-17bd-4e5e-9534-950f3b022209
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: fda9b64f588c520833b2669eafdf650efc3de6be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-stream-analytics-tooprocess-exported-data-from-application-insights"></a><span data-ttu-id="00e77-103">Application Insights에서 내보내는 데이터를 사용 하 여 스트림 분석 tooprocess</span><span class="sxs-lookup"><span data-stu-id="00e77-103">Use Stream Analytics tooprocess exported data from Application Insights</span></span>
<span data-ttu-id="00e77-104">[Azure 스트림 분석](https://azure.microsoft.com/services/stream-analytics/) 는 데이터 처리를 위한 이상적인 도구 hello [Application Insights에서 내보낸](app-insights-export-telemetry.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-104">[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) is hello ideal tool for processing data [exported from Application Insights](app-insights-export-telemetry.md).</span></span> <span data-ttu-id="00e77-105">Stream Analytics는 다양한 원본의 데이터를 가져와서</span><span class="sxs-lookup"><span data-stu-id="00e77-105">Stream Analytics can pull data from a variety of sources.</span></span> <span data-ttu-id="00e77-106">변환 하 고 hello 데이터를 필터링 하 고 tooa 다양 한 싱크 라우팅할 수 것입니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-106">It can transform and filter hello data, and then route it tooa variety of sinks.</span></span>

<span data-ttu-id="00e77-107">이 예제에서는 이름 바꾸기, Application Insights에서 데이터를 가져와서 hello 필드 중 일부를 처리 하 고 Power BI로 파이프 하는 어댑터를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-107">In this example, we'll create an adaptor that takes data from Application Insights, renames and processes some of hello fields, and pipes it into Power BI.</span></span>

> [!WARNING]
> <span data-ttu-id="00e77-108">더 나은 훨씬 손쉽고 없는 [권장 방법으로 Power BI에서 toodisplay Application Insights 데이터](app-insights-export-power-bi.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-108">There are much better and easier [recommended ways toodisplay Application Insights data in Power BI](app-insights-export-power-bi.md).</span></span> <span data-ttu-id="00e77-109">hello 여기에서 설명 하는 경로는 예제 tooillustrate 방금 tooprocess 데이터를 내보내는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-109">hello path illustrated here is just an example tooillustrate how tooprocess exported data.</span></span>
> 
> 

![SA tooPBI 통해 내보내기에 대 한 블록 다이어그램](./media/app-insights-export-stream-analytics/020.png)

## <a name="create-storage-in-azure"></a><span data-ttu-id="00e77-111">Azure에서 저장소 만들기</span><span class="sxs-lookup"><span data-stu-id="00e77-111">Create storage in Azure</span></span>
<span data-ttu-id="00e77-112">연속 내보내기를 먼저 toocreate hello 저장소가 필요 하므로 항상 데이터 tooan Azure 저장소 계정을 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-112">Continuous export always outputs data tooan Azure Storage account, so you need toocreate hello storage first.</span></span>

1. <span data-ttu-id="00e77-113">Hello에 구독에서 "클래식" 저장소 계정을 만드는 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-113">Create a "classic" storage account in your subscription in hello [Azure portal](https://portal.azure.com).</span></span>
   
   ![Azure 포털에서 새로 만들기, 데이터, 저장소 선택](./media/app-insights-export-stream-analytics/030.png)
2. <span data-ttu-id="00e77-115">컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="00e77-115">Create a container</span></span>
   
    ![Hello 새 저장소를 선택 하세요.를 hello 컨테이너 타일 및 추가 클릭 합니다.](./media/app-insights-export-stream-analytics/040.png)
3. <span data-ttu-id="00e77-117">Hello 저장소 액세스 키를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-117">Copy hello storage access key</span></span>
   
    <span data-ttu-id="00e77-118">해야 곧 tooset hello 입력된 toohello 스트림 분석 서비스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-118">You'll need it soon tooset up hello input toohello stream analytics service.</span></span>
   
    ![Hello 저장소에서 설정, 키를 열고 hello 기본 액세스 키의 복사본](./media/app-insights-export-stream-analytics/045.png)

## <a name="start-continuous-export-tooazure-storage"></a><span data-ttu-id="00e77-120">연속 내보내기를 tooAzure 저장소 시작</span><span class="sxs-lookup"><span data-stu-id="00e77-120">Start continuous export tooAzure storage</span></span>
<span data-ttu-id="00e77-121">[연속 내보내기](app-insights-export-telemetry.md) 는 Application Insights에서 Azure 저장소로 데이터를 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-121">[Continuous export](app-insights-export-telemetry.md) moves data from Application Insights into Azure storage.</span></span>

1. <span data-ttu-id="00e77-122">Hello Azure 포털에서에서 응용 프로그램에 대해 만든 toohello Application Insights 리소스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-122">In hello Azure portal, browse toohello Application Insights resource you created for your application.</span></span>
   
    ![찾아보기, Application Insights, 응용 프로그램 선택](./media/app-insights-export-stream-analytics/050.png)
2. <span data-ttu-id="00e77-124">연속 내보내기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-124">Create a continuous export.</span></span>
   
    ![설정, 연속 내보내기, 추가를 차례로 선택](./media/app-insights-export-stream-analytics/060.png)

    <span data-ttu-id="00e77-126">이전에 만든 hello 저장소 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-126">Select hello storage account you created earlier:</span></span>

    ![Hello 내보내기 대상을 설정합니다](./media/app-insights-export-stream-analytics/070.png)

    <span data-ttu-id="00e77-128">Toosee 원하는 hello 이벤트 유형을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-128">Set hello event types you want toosee:</span></span>

    ![이벤트 유형 선택](./media/app-insights-export-stream-analytics/080.png)

1. <span data-ttu-id="00e77-130">일부 데이터가 누적되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-130">Let some data accumulate.</span></span> <span data-ttu-id="00e77-131">한동안 사용자가 응용 프로그램을 사용하도록 놓아둡니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-131">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="00e77-132">원격 분석이 제공되어 [메트릭 탐색기](app-insights-metrics-explorer.md)에서 통계 차트가, [진단 검색](app-insights-diagnostic-search.md)에서 개별 이벤트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-132">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="00e77-133">및 또한 hello 데이터는 tooyour 저장소를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-133">And also, hello data will export tooyour storage.</span></span> 
2. <span data-ttu-id="00e77-134">Hello 내보낸 데이터를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-134">Inspect hello exported data.</span></span> <span data-ttu-id="00e77-135">Visual Studio에서 **보기/클라우드 탐색기**를 선택하고 Azure/저장소를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-135">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="00e77-136">(Tooinstall hello Azure SDK이 메뉴 옵션에 없을 경우 해야: hello 새 프로젝트 대화 상자를 열고 엽니다 Visual C# / 클라우드 / Microsoft Azure SDK for.NET 가져오기.)</span><span class="sxs-lookup"><span data-stu-id="00e77-136">(If you don't have this menu option, you need tooinstall hello Azure SDK: Open hello New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![](./media/app-insights-export-stream-analytics/04-data.png)
   
    <span data-ttu-id="00e77-137">Hello 응용 프로그램 이름 및 계측 키에서 파생 된 hello 경로 이름의 hello 공통 부분을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-137">Make a note of hello common part of hello path name, which is derived from hello application name and instrumentation key.</span></span> 

<span data-ttu-id="00e77-138">hello 이벤트는 JSON 형식의 tooblob 파일 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-138">hello events are written tooblob files in JSON format.</span></span> <span data-ttu-id="00e77-139">각 파일에는 하나 이상의 이벤트가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-139">Each file may contain one or more events.</span></span> <span data-ttu-id="00e77-140">따라서 싶습니다 tooread hello 이벤트 데이터와 원하는 hello 필드를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-140">So we'd like tooread hello event data and filter out hello fields we want.</span></span> <span data-ttu-id="00e77-141">모든 종류의 hello 데이터로 수행 하는 항목이 없지만 현재 계획으로 오늘 toouse 스트림 분석 toopipe hello 데이터 tooPower BI는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-141">There are all kinds of things we could do with hello data, but our plan today is toouse Stream Analytics toopipe hello data tooPower BI.</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="00e77-142">Azure 스트림 분석 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="00e77-142">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="00e77-143">Hello에서 [클래식 Azure 포털](https://manage.windowsazure.com/)hello Azure 스트림 분석 서비스를 선택 하 고 새 스트림 분석 작업 만들기:</span><span class="sxs-lookup"><span data-stu-id="00e77-143">From hello [Classic Azure Portal](https://manage.windowsazure.com/), select hello Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](./media/app-insights-export-stream-analytics/090.png)

![](./media/app-insights-export-stream-analytics/100.png)

<span data-ttu-id="00e77-144">Hello 새 작업을 만든 경우 해당 세부 정보를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-144">When hello new job is created, expand its details:</span></span>

![](./media/app-insights-export-stream-analytics/110.png)

### <a name="set-blob-location"></a><span data-ttu-id="00e77-145">Blob 위치 설정</span><span class="sxs-lookup"><span data-stu-id="00e77-145">Set blob location</span></span>
<span data-ttu-id="00e77-146">연속 내보내기 blob의 tootake 입력으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-146">Set it tootake input from your Continuous Export blob:</span></span>

![](./media/app-insights-export-stream-analytics/120.png)

<span data-ttu-id="00e77-147">이제 기본 액세스 키 hello 앞에서 기록해 둔 저장소 계정에서 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-147">Now you'll need hello Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="00e77-148">저장소 계정 키 hello로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-148">Set this as hello Storage Account Key.</span></span>

![](./media/app-insights-export-stream-analytics/130.png)

### <a name="set-path-prefix-pattern"></a><span data-ttu-id="00e77-149">경로 접두사 패턴 설정</span><span class="sxs-lookup"><span data-stu-id="00e77-149">Set path prefix pattern</span></span>
![](./media/app-insights-export-stream-analytics/140.png)

<span data-ttu-id="00e77-150">**있는지 tooset hello 날짜 형식 tooYYYY-월-일 (포함 대시) 수입니다.**</span><span class="sxs-lookup"><span data-stu-id="00e77-150">**Be sure tooset hello Date Format tooYYYY-MM-DD (with dashes).**</span></span>

<span data-ttu-id="00e77-151">hello 경로 접두사 패턴 스트림 분석 hello 저장소의 hello 입력된 파일을 찾는 하는 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-151">hello Path Prefix Pattern specifies where Stream Analytics finds hello input files in hello storage.</span></span> <span data-ttu-id="00e77-152">Tooset 필요한 것 연속 내보내기가 toocorrespond toohow hello 데이터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-152">You need tooset it toocorrespond toohow Continuous Export stores hello data.</span></span> <span data-ttu-id="00e77-153">다음과 같이 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-153">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="00e77-154">이 예제에서:</span><span class="sxs-lookup"><span data-stu-id="00e77-154">In this example:</span></span>

* <span data-ttu-id="00e77-155">`webapplication27`hello Application Insights 리소스의 hello 이름인 **모두 소문자로**합니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-155">`webapplication27` is hello name of hello Application Insights resource **all lower case**.</span></span>
* <span data-ttu-id="00e77-156">`1234...`hello Application Insights 리소스의 계측 키 hello **대시 생략**합니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-156">`1234...` is hello instrumentation key of hello Application Insights resource, **omitting dashes**.</span></span> 
* <span data-ttu-id="00e77-157">`PageViews`hello 형식인 원하는 tooanalyze 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-157">`PageViews` is hello type of data you want tooanalyze.</span></span> <span data-ttu-id="00e77-158">연속 내보내기에서 설정한 hello 필터에 대 한 hello 사용 가능한 형식에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-158">hello available types depend on hello filter you set in Continuous Export.</span></span> <span data-ttu-id="00e77-159">사용 가능한 다른 유형 hello 내보낸된 데이터 toosee hello를 검사 하 고 hello 참조 [데이터 모델을 내보낼](app-insights-export-data-model.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-159">Examine hello exported data toosee hello other available types, and see hello [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="00e77-160">`/{date}/{time}` 은 문자로 기록된 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-160">`/{date}/{time}` is a pattern written literally.</span></span>

> [!NOTE]
> <span data-ttu-id="00e77-161">그러면 오른쪽 hello 경로 가져올 hello 저장소 toomake를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-161">Inspect hello storage toomake sure you get hello path right.</span></span>
> 
> 

### <a name="finish-initial-setup"></a><span data-ttu-id="00e77-162">초기 설치 완료</span><span class="sxs-lookup"><span data-stu-id="00e77-162">Finish initial setup</span></span>
<span data-ttu-id="00e77-163">Hello 직렬화 형식을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-163">Confirm hello serialization format:</span></span>

![마법사 확인 후 닫기](./media/app-insights-export-stream-analytics/150.png)

<span data-ttu-id="00e77-165">Hello 마법사를 닫고 설치 프로그램 toocomplete hello에 대 한 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-165">Close hello wizard and wait for hello setup toocomplete.</span></span>

> [!TIP]
> <span data-ttu-id="00e77-166">Hello 샘플 명령은 toodownload 일부 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-166">Use hello Sample command toodownload some data.</span></span> <span data-ttu-id="00e77-167">지속적으로 테스트 샘플 toodebug 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-167">Keep it as a test sample toodebug your query.</span></span>
> 
> 

## <a name="set-hello-output"></a><span data-ttu-id="00e77-168">집합 hello 출력</span><span class="sxs-lookup"><span data-stu-id="00e77-168">Set hello output</span></span>
<span data-ttu-id="00e77-169">이제 작업을 선택 하 고 hello 출력을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-169">Now select your job and set hello output.</span></span>

![Hello 새 채널을 선택, 출력, 추가, Power BI를 클릭 합니다.](./media/app-insights-export-stream-analytics/160.png)

<span data-ttu-id="00e77-171">제공 프로그램 **회사 또는 학교 계정** tooauthorize 스트림 분석 tooaccess 사용자 Power BI 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-171">Provide your **work or school account** tooauthorize Stream Analytics tooaccess your Power BI resource.</span></span> <span data-ttu-id="00e77-172">그런 다음 만들 hello 출력 하 고 hello 대상 Power BI 데이터 집합 및 테이블에 대 한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-172">Then invent a name for hello output, and for hello target Power BI dataset and table.</span></span>

![이름 3개를 생성합니다.](./media/app-insights-export-stream-analytics/170.png)

## <a name="set-hello-query"></a><span data-ttu-id="00e77-174">집합 hello 쿼리</span><span class="sxs-lookup"><span data-stu-id="00e77-174">Set hello query</span></span>
<span data-ttu-id="00e77-175">hello 쿼리 입력된 toooutput에서 hello 번역을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-175">hello query governs hello translation from input toooutput.</span></span>

![Hello 작업을 선택 하 고 쿼리를 클릭 합니다.](./media/app-insights-export-stream-analytics/180.png)

<span data-ttu-id="00e77-178">Hello 테스트 함수 toocheck hello 오른쪽 출력을 가져올 수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-178">Use hello Test function toocheck that you get hello right output.</span></span> <span data-ttu-id="00e77-179">Hello 입력 페이지에서 수행한 hello 예제 데이터를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-179">Give it hello sample data that you took from hello inputs page.</span></span> 

### <a name="query-toodisplay-counts-of-events"></a><span data-ttu-id="00e77-180">쿼리 이벤트 toodisplay 수</span><span class="sxs-lookup"><span data-stu-id="00e77-180">Query toodisplay counts of events</span></span>
<span data-ttu-id="00e77-181">이 쿼리 붙여넣기:</span><span class="sxs-lookup"><span data-stu-id="00e77-181">Paste this query:</span></span>

```SQL

    SELECT
      flat.ArrayValue.name,
      count(*)
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.[event]) as flat
    GROUP BY TumblingWindow(minute, 1), flat.ArrayValue.name
```

* <span data-ttu-id="00e77-182">내보내기 입력은 hello 별칭 toohello 스트림 입력 적용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-182">export-input is hello alias we gave toohello stream input</span></span>
* <span data-ttu-id="00e77-183">pbi 출력은 정의한 hello 출력 별칭</span><span class="sxs-lookup"><span data-stu-id="00e77-183">pbi-output is hello output alias we defined</span></span>
* <span data-ttu-id="00e77-184">사용 하 여 [외부 적용 GetElements](https://msdn.microsoft.com/library/azure/dn706229.aspx) hello 이벤트 이름은 중첩 된 JSON arrray 이므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-184">We use [OUTER APPLY GetElements](https://msdn.microsoft.com/library/azure/dn706229.aspx) because hello event name is in a nested JSON arrray.</span></span> <span data-ttu-id="00e77-185">그런 다음 hello 선택 선택 hello hello hello 기간에에서 같은 이름의 인스턴스 수의 개수와 함께 이벤트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-185">Then hello Select picks hello event name, together with a count of hello number of instances with that name in hello time period.</span></span> <span data-ttu-id="00e77-186">hello [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) 절 기간을 1 분으로 hello 요소를 그룹화 합니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-186">hello [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) clause groups hello elements into time periods of 1 minute.</span></span>

### <a name="query-toodisplay-metric-values"></a><span data-ttu-id="00e77-187">쿼리 toodisplay 메트릭 값</span><span class="sxs-lookup"><span data-stu-id="00e77-187">Query toodisplay metric values</span></span>
```SQL

    SELECT
      A.context.data.eventtime,
      avg(CASE WHEN flat.arrayvalue.myMetric.value IS NULL THEN 0 ELSE  flat.arrayvalue.myMetric.value END) as myValue
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.context.custom.metrics) as flat
    GROUP BY TumblingWindow(minute, 1), A.context.data.eventtime

``` 

* <span data-ttu-id="00e77-188">이 쿼리는 hello 메트릭 원격 분석 tooget hello 이벤트 시간 및 hello 메트릭 값으로 드릴 합니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-188">This query drills into hello metrics telemetry tooget hello event time and hello metric value.</span></span> <span data-ttu-id="00e77-189">외부 적용 GetElements 패턴 tooextract hello 행 hello를 사용 하도록 배열, 내부 hello 메트릭 값은입니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-189">hello metric values are inside an array, so we use hello OUTER APPLY GetElements pattern tooextract hello rows.</span></span> <span data-ttu-id="00e77-190">이 경우 "myMetric"는 hello 이름 hello 메트릭입니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-190">"myMetric" is hello name of hello metric in this case.</span></span> 

### <a name="query-tooinclude-values-of-dimension-properties"></a><span data-ttu-id="00e77-191">차원 속성의 tooinclude 값 쿼리</span><span class="sxs-lookup"><span data-stu-id="00e77-191">Query tooinclude values of dimension properties</span></span>
```SQL

    WITH flat AS (
    SELECT
      MySource.context.data.eventTime as eventTime,
      InstanceId = MyDimension.ArrayValue.InstanceId.value,
      BusinessUnitId = MyDimension.ArrayValue.BusinessUnitId.value
    FROM MySource
    OUTER APPLY GetArrayElements(MySource.context.custom.dimensions) MyDimension
    )
    SELECT
     eventTime,
     InstanceId,
     BusinessUnitId
    INTO AIOutput
    FROM flat

```

* <span data-ttu-id="00e77-192">이 쿼리 hello 차원 배열에서 고정된 된 인덱스에 특정 차원에 따라 없이 hello 차원 속성의 값을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-192">This query includes values of hello dimension properties without depending on a particular dimension being at a fixed index in hello dimension array.</span></span>

## <a name="run-hello-job"></a><span data-ttu-id="00e77-193">Hello 작업 실행</span><span class="sxs-lookup"><span data-stu-id="00e77-193">Run hello job</span></span>
<span data-ttu-id="00e77-194">Hello toostart hello 작업에서 이전에 날짜를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-194">You can select a date in hello past toostart hello job from.</span></span> 

![Hello 작업을 선택 하 고 쿼리를 클릭 합니다.](./media/app-insights-export-stream-analytics/190.png)

<span data-ttu-id="00e77-197">Hello 작업이 실행 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-197">Wait until hello job is Running.</span></span>

## <a name="see-results-in-power-bi"></a><span data-ttu-id="00e77-198">Power BI에 결과를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00e77-198">See results in Power BI</span></span>
> [!WARNING]
> <span data-ttu-id="00e77-199">더 나은 훨씬 손쉽고 없는 [권장 방법으로 Power BI에서 toodisplay Application Insights 데이터](app-insights-export-power-bi.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-199">There are much better and easier [recommended ways toodisplay Application Insights data in Power BI](app-insights-export-power-bi.md).</span></span> <span data-ttu-id="00e77-200">hello 여기에서 설명 하는 경로는 예제 tooillustrate 방금 tooprocess 데이터를 내보내는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-200">hello path illustrated here is just an example tooillustrate how tooprocess exported data.</span></span>
> 
> 

<span data-ttu-id="00e77-201">작업 또는 학교 계정 및 선택 hello 데이터 집합 및 hello 스트림 분석 작업의 hello 출력으로 정의 되어 테이블을 사용 하 여 Power BI를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-201">Open Power BI with your work or school account, and select hello dataset and table that you defined as hello output of hello Stream Analytics job.</span></span>

![Power BI에서 데이터 집합과 필드를 선택합니다.](./media/app-insights-export-stream-analytics/200.png)

<span data-ttu-id="00e77-203">이제 [Power BI](https://powerbi.microsoft.com)의 보고서 및 대시보드에서 이 데이터 집합을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-203">Now you can use this dataset in reports and dashboards in [Power BI](https://powerbi.microsoft.com).</span></span>

![Power BI에서 데이터 집합과 필드를 선택합니다.](./media/app-insights-export-stream-analytics/210.png)

## <a name="no-data"></a><span data-ttu-id="00e77-205">데이터가 없나요?</span><span class="sxs-lookup"><span data-stu-id="00e77-205">No data?</span></span>
* <span data-ttu-id="00e77-206">확인을 [hello 날짜 형식 설정](#set-path-prefix-pattern) 올바르게 tooYYYY-월-일 (대시) 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-206">Check that you [set hello date format](#set-path-prefix-pattern) correctly tooYYYY-MM-DD (with dashes).</span></span>

## <a name="video"></a><span data-ttu-id="00e77-207">비디오</span><span class="sxs-lookup"><span data-stu-id="00e77-207">Video</span></span>
<span data-ttu-id="00e77-208">Noam Ben Zeev tooprocess Stream Analytics을 사용 하 여 데이터를 내보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-208">Noam Ben Zeev shows how tooprocess exported data using Stream Analytics.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Export-to-Power-BI-from-Application-Insights/player]
> 
> 

## <a name="next-steps"></a><span data-ttu-id="00e77-209">다음 단계</span><span class="sxs-lookup"><span data-stu-id="00e77-209">Next steps</span></span>
* [<span data-ttu-id="00e77-210">연속 내보내기</span><span class="sxs-lookup"><span data-stu-id="00e77-210">Continuous export</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="00e77-211">세부 데이터는 hello 속성 형식 및 값에 대 한 참조를 모델링합니다.</span><span class="sxs-lookup"><span data-stu-id="00e77-211">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="00e77-212">Application Insights</span><span class="sxs-lookup"><span data-stu-id="00e77-212">Application Insights</span></span>](app-insights-overview.md)

