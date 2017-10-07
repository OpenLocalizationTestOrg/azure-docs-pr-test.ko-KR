---
title: "Application Insights에서 원격 분석의 aaaContinuous 내보내기 | Microsoft Docs"
description: "Microsoft Azure에서 진단 및 사용 현황 데이터 toostorage 내보내고 여기에서 다운로드 합니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 5b859200-b484-4c98-9d9f-929713f1030c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: bwren
ms.openlocfilehash: be9ed7e05922c1c8186df9ca4e642862adaa5fd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="export-telemetry-from-application-insights"></a><span data-ttu-id="f4b8e-103">Application Insights에서 원격 분석 내보내기</span><span class="sxs-lookup"><span data-stu-id="f4b8e-103">Export telemetry from Application Insights</span></span>
<span data-ttu-id="f4b8e-104">Hello 표준 보존 기간 보다 오랫동안 tookeep 원격 분석을 선택 하십시오.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-104">Want tookeep your telemetry for longer than hello standard retention period?</span></span> <span data-ttu-id="f4b8e-105">또는 일부 특수한 방식으로 처리하시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="f4b8e-105">Or process it in some specialized way?</span></span> <span data-ttu-id="f4b8e-106">그렇다면 연속 내보내기가 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-106">Continuous Export is ideal for this.</span></span> <span data-ttu-id="f4b8e-107">JSON 형식으로 Microsoft Azure에서 내보낸된 toostorage hello 이벤트 hello Application Insights 포털에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-107">hello events you see in hello Application Insights portal can be exported toostorage in Microsoft Azure in JSON format.</span></span> <span data-ttu-id="f4b8e-108">여기에서 데이터를 다운로드 및 무엇이 든 코드를 작성할 수 있습니다 tooprocess 할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-108">From there you can download your data and write whatever code you need tooprocess it.</span></span>  

<span data-ttu-id="f4b8e-109">연속 내보내기를 사용할 경우 추가 요금이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-109">Using Continuous Export may incur an additional charge.</span></span> <span data-ttu-id="f4b8e-110">[가격 책정 모델](http://azure.microsoft.com/pricing/details/application-insights/)을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-110">Check your [pricing model](http://azure.microsoft.com/pricing/details/application-insights/).</span></span>

<span data-ttu-id="f4b8e-111">연속 내보내기의를 설정 하기 전에 몇 가지 대안 tooconsider 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-111">Before you set up continuous export, there are some alternatives you might want tooconsider:</span></span>

* <span data-ttu-id="f4b8e-112">메트릭 또는 검색 블레이드의 hello 위쪽 hello 내보내기 단추를 사용 하면 테이블 및 차트 tooan Excel 스프레드시트를 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-112">hello Export button at hello top of a metrics or search blade lets you transfer tables and charts tooan Excel spreadsheet.</span></span>

* <span data-ttu-id="f4b8e-113">[분석](app-insights-analytics.md)은 원격 분석을 위한 강력한 쿼리 언어를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-113">[Analytics](app-insights-analytics.md) provides a powerful query language for telemetry.</span></span> <span data-ttu-id="f4b8e-114">결과를 내보낼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-114">It can also export results.</span></span>
* <span data-ttu-id="f4b8e-115">너무에 찾고 있는 경우[Power BI에서 데이터를 탐색](app-insights-export-power-bi.md), 연속 내보내기가 사용 하지 않고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-115">If you're looking too[explore your data in Power BI](app-insights-export-power-bi.md), you can do that without using Continuous Export.</span></span>
* <span data-ttu-id="f4b8e-116">hello [데이터 REST API 액세스](https://dev.applicationinsights.io/) 원격 분석을 프로그래밍 방식으로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-116">hello [Data access REST API](https://dev.applicationinsights.io/) lets you access your telemetry programmatically.</span></span>

<span data-ttu-id="f4b8e-117">연속 내보내기 (여기서 것 유지 될 수 있는 대해 원하는 만큼) 하 여 데이터 toostorage을 복사한 후은 일반적인 hello에 대 한 Application Insights에서 계속 제공 [보존 기간](app-insights-data-retention-privacy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-117">After Continuous Export copies your data toostorage (where it can stay for as long as you like), it's still available in Application Insights for hello usual [retention period](app-insights-data-retention-privacy.md).</span></span>

## <span data-ttu-id="f4b8e-118"><a name="setup"></a> 연속 내보내기 만들기</span><span class="sxs-lookup"><span data-stu-id="f4b8e-118"><a name="setup"></a> Create a Continuous Export</span></span>
1. <span data-ttu-id="f4b8e-119">앱에 대 한 Application Insights 리소스 hello에 연속 내보내기가 열고 선택 **추가**:</span><span class="sxs-lookup"><span data-stu-id="f4b8e-119">In hello Application Insights resource for your app, open Continuous Export and choose **Add**:</span></span>

    ![아래로 스크롤하여 연속 내보내기 클릭](./media/app-insights-export-telemetry/01-export.png)

2. <span data-ttu-id="f4b8e-121">Hello 원격 분석 데이터 형식을 선택 tooexport 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-121">Choose hello telemetry data types you want tooexport.</span></span>

3. <span data-ttu-id="f4b8e-122">생성 또는 선택할는 [Azure 저장소 계정](../storage/common/storage-introduction.md) toostore hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-122">Create or select an [Azure storage account](../storage/common/storage-introduction.md) where you want toostore hello data.</span></span>

    > [!Warning]
    > <span data-ttu-id="f4b8e-123">기본적으로 hello 저장소 위치는 설정 toohello Application Insights 리소스와 동일한 지리적 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-123">By default, hello storage location will be set toohello same geographical region as your Application Insights resource.</span></span> <span data-ttu-id="f4b8e-124">다른 지역에 저장하는 경우 전송 요금이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-124">If you store in a different region, you may incur transfer charges.</span></span>

    ![추가, 내보내기 대상, 저장소 계정을 클릭한 다음 새 저장소를 만들거나 기존 저장소 선택](./media/app-insights-export-telemetry/02-add.png)

4. <span data-ttu-id="f4b8e-126">만들거나 hello 저장소에서 컨테이너를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-126">Create or select a container in hello storage:</span></span>

    ![이벤트 유형 선택 클릭](./media/app-insights-export-telemetry/create-container.png)

<span data-ttu-id="f4b8e-128">내보내기를 만들면 진행을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-128">Once you've created your export, it starts going.</span></span> <span data-ttu-id="f4b8e-129">만 hello 내보내기를 만든 후 들어오는 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-129">You only get data that arrives after you create hello export.</span></span>

<span data-ttu-id="f4b8e-130">약 1 시간 hello 저장소에 데이터 표시 될 때까지 지연 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-130">There can be a delay of about an hour before data appears in hello storage.</span></span>

### <a name="tooedit-continuous-export"></a><span data-ttu-id="f4b8e-131">연속 내보내기를 tooedit</span><span class="sxs-lookup"><span data-stu-id="f4b8e-131">tooedit continuous export</span></span>

<span data-ttu-id="f4b8e-132">Toochange hello 이벤트 유형을 나중 편집 hello 내보내기:</span><span class="sxs-lookup"><span data-stu-id="f4b8e-132">If you want toochange hello event types later, just edit hello export:</span></span>

![이벤트 유형 선택 클릭](./media/app-insights-export-telemetry/05-edit.png)

### <a name="toostop-continuous-export"></a><span data-ttu-id="f4b8e-134">연속 내보내기를 toostop</span><span class="sxs-lookup"><span data-stu-id="f4b8e-134">toostop continuous export</span></span>

<span data-ttu-id="f4b8e-135">toostop hello 내보내기 사용 안 함을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-135">toostop hello export, click Disable.</span></span> <span data-ttu-id="f4b8e-136">활성화를 다시 클릭 하면 새 데이터로 hello 내보내기를 다시 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-136">When you click Enable again, hello export will restart with new data.</span></span> <span data-ttu-id="f4b8e-137">내보내기 해제 된 동안 hello 포털에서 도착 하는 hello 데이터를 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-137">You won't get hello data that arrived in hello portal while export was disabled.</span></span>

<span data-ttu-id="f4b8e-138">toostop hello 내보내기 영구적으로 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-138">toostop hello export permanently, delete it.</span></span> <span data-ttu-id="f4b8e-139">이렇게 해도 저장소에서 데이터를 삭제하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-139">Doing so doesn't delete your data from storage.</span></span>

### <a name="cant-add-or-change-an-export"></a><span data-ttu-id="f4b8e-140">내보내기를 추가 또는 변경할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="f4b8e-140">Can't add or change an export?</span></span>
* <span data-ttu-id="f4b8e-141">tooadd 또는 변경 내보내기 소유자, 참가자 또는 응용 프로그램 통찰력 참가자 액세스 권한을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-141">tooadd or change exports, you need Owner, Contributor or Application Insights Contributor access rights.</span></span> <span data-ttu-id="f4b8e-142">[역할에 대해 알아봅니다][roles].</span><span class="sxs-lookup"><span data-stu-id="f4b8e-142">[Learn about roles][roles].</span></span>

## <span data-ttu-id="f4b8e-143"><a name="analyze"></a> 어떤 이벤트를 얻나요?</span><span class="sxs-lookup"><span data-stu-id="f4b8e-143"><a name="analyze"></a> What events do you get?</span></span>
<span data-ttu-id="f4b8e-144">hello 내보낸된 데이터는 hello 원시 원격 분석 응용 프로그램에서 수신 위치 데이터는 계산 hello 클라이언트 IP 주소에서 추가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-144">hello exported data is hello raw telemetry we receive from your application, except that we add location data which we calculate from hello client IP address.</span></span>

<span data-ttu-id="f4b8e-145">여는 삭제 되었으며 데이터 [샘플링](app-insights-sampling.md) hello 내보낸 데이터에 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-145">Data that has been discarded by [sampling](app-insights-sampling.md) is not included in hello exported data.</span></span>

<span data-ttu-id="f4b8e-146">계산된 다른 메트릭은 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-146">Other calculated metrics are not included.</span></span> <span data-ttu-id="f4b8e-147">예를 들어 म 하지 평균 CPU 활용도 내보내지만 hello 평균이 계산 되는 hello 원시 원격 분석 내보냅니다지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-147">For example, we don't export average CPU utilisation, but we do export hello raw telemetry from which hello average is computed.</span></span>

<span data-ttu-id="f4b8e-148">hello 데이터도 포함 된 hello 결과 [가용성 웹 테스트](app-insights-monitor-web-app-availability.md) 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-148">hello data also includes hello results of any [availability web tests](app-insights-monitor-web-app-availability.md) that you have set up.</span></span>

> [!NOTE]
> <span data-ttu-id="f4b8e-149">**샘플링**</span><span class="sxs-lookup"><span data-stu-id="f4b8e-149">**Sampling.**</span></span> <span data-ttu-id="f4b8e-150">응용 프로그램에서 많은 양의 데이터를 하는 경우 hello 샘플링 기능이 작동 하 고 hello 생성 된 원격 분석의 일부만 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-150">If your application sends a lot of data, hello sampling feature may operate and send only a fraction of hello generated telemetry.</span></span> [<span data-ttu-id="f4b8e-151">샘플링에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-151">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <span data-ttu-id="f4b8e-152"><a name="get"></a>Hello 데이터 검사</span><span class="sxs-lookup"><span data-stu-id="f4b8e-152"><a name="get"></a> Inspect hello data</span></span>
<span data-ttu-id="f4b8e-153">Hello 포털에서 직접 hello 저장소를 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-153">You can inspect hello storage directly in hello portal.</span></span> <span data-ttu-id="f4b8e-154">**찾아보기**를 클릭하고 저장소 계정을 선택한 후 **컨테이너**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-154">Click **Browse**, select your storage account, and then open **Containers**.</span></span>

<span data-ttu-id="f4b8e-155">Visual Studio에서 Azure 저장소 tooinspect 열고 **보기**, **클라우드 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-155">tooinspect Azure storage in Visual Studio, open **View**, **Cloud Explorer**.</span></span> <span data-ttu-id="f4b8e-156">(Tooinstall hello Azure SDK 메뉴 명령을 해당를 설정 하지 않은 경우 해야: 열기 hello **새 프로젝트** 대화 상자를 확장 하 고 Visual C# / 클라우드 선택 하 고 **Microsoft Azure SDK for.NET 가져오기**.)</span><span class="sxs-lookup"><span data-stu-id="f4b8e-156">(If you don't have that menu command, you need tooinstall hello Azure SDK: Open hello **New Project** dialog, expand Visual C#/Cloud and choose **Get Microsoft Azure SDK for .NET**.)</span></span>

<span data-ttu-id="f4b8e-157">blob 저장소를 열면 blob 파일 집합이 포함된 컨테이너가 보입니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-157">When you open your blob store, you'll see a container with a set of blob files.</span></span> <span data-ttu-id="f4b8e-158">hello 계측 키 Application Insights 리소스 이름, 원격 분석-유형/날짜/시간에서 파생 된 각 파일의 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-158">hello URI of each file derived from your Application Insights resource name, its instrumentation key, telemetry-type/date/time.</span></span> <span data-ttu-id="f4b8e-159">(hello 리소스 이름은 모두 소문자 및 hello 계측 키 대시를 생략 합니다.)</span><span class="sxs-lookup"><span data-stu-id="f4b8e-159">(hello resource name is all lowercase, and hello instrumentation key omits dashes.)</span></span>

![적합 한 도구와 hello blob 저장소를 검사 합니다.](./media/app-insights-export-telemetry/04-data.png)

<span data-ttu-id="f4b8e-161">hello 날짜 및 시간 UTC 이며 hello 원격 분석 hello 저장소에 보관 된-생성 된 hello 시간이 아닌 경우.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-161">hello date and time are UTC and are when hello telemetry was deposited in hello store - not hello time it was generated.</span></span> <span data-ttu-id="f4b8e-162">하므로 코드 toodownload hello 데이터를 작성 하는 경우 hello 데이터를 통해 선형으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-162">So if you write code toodownload hello data, it can move linearly through hello data.</span></span>

<span data-ttu-id="f4b8e-163">Hello 경로의 hello 형태는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-163">Here's hello form of hello path:</span></span>

    $"{applicationName}_{instrumentationKey}/{type}/{blobDeliveryTimeUtc:yyyy-MM-dd}/{ blobDeliveryTimeUtc:HH}/{blobId}_{blobCreationTimeUtc:yyyyMMdd_HHmmss}.blob"

<span data-ttu-id="f4b8e-164">Where</span><span class="sxs-lookup"><span data-stu-id="f4b8e-164">Where</span></span>

* <span data-ttu-id="f4b8e-165">`blobCreationTimeUtc`blob를 만든 시간 hello에 내부 저장소를 준비는</span><span class="sxs-lookup"><span data-stu-id="f4b8e-165">`blobCreationTimeUtc` is time when blob was created in hello internal staging storage</span></span>
* <span data-ttu-id="f4b8e-166">`blobDeliveryTimeUtc`blob 복사 toohello 내보내기 대상 저장소를가 하는 경우 hello 시간</span><span class="sxs-lookup"><span data-stu-id="f4b8e-166">`blobDeliveryTimeUtc` is hello time when blob is copied toohello export destination storage</span></span>

## <span data-ttu-id="f4b8e-167"><a name="format"></a> 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="f4b8e-167"><a name="format"></a> Data format</span></span>
* <span data-ttu-id="f4b8e-168">각 blob은 다중 '\n'-separated 행을 포함하는 텍스트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-168">Each blob is a text file that contains multiple '\n'-separated rows.</span></span> <span data-ttu-id="f4b8e-169">약 1/2 분의 시간 동안 처리 된 hello 원격 분석을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-169">It contains hello telemetry processed over a time period of roughly half a minute.</span></span>
* <span data-ttu-id="f4b8e-170">각 행은 요청 또는 페이지 보기와 같은 원격 분석 데이터 요소를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-170">Each row represents a telemetry data point such as a request or page view.</span></span>
* <span data-ttu-id="f4b8e-171">각 행은 서식이 지정되지 않은 JSON 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-171">Each row is an unformatted JSON document.</span></span> <span data-ttu-id="f4b8e-172">원할 경우 toosit 및 한번 stare, Visual Studio에서 열 선택, 고급, 서식 파일을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-172">If you want toosit and stare at it, open it in Visual Studio and choose Edit, Advanced, Format File:</span></span>

![적합 한 도구와 보기 hello 원격 분석](./media/app-insights-export-telemetry/06-json.png)

<span data-ttu-id="f4b8e-174">시간 기간은 틱 단위이며 10,000틱은 1ms입니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-174">Time durations are in ticks, where 10 000 ticks = 1ms.</span></span> <span data-ttu-id="f4b8e-175">이러한 값 1ms 시간을 표시 하는 예를 들어 hello 브라우저를 보내고 받았습니다의 요청 toosend tooreceive hello 브라우저에서 페이지 및 1.8s tooprocess hello:</span><span class="sxs-lookup"><span data-stu-id="f4b8e-175">For example, these values show a time of 1ms toosend a request from hello browser, 3ms tooreceive it, and 1.8s tooprocess hello page in hello browser:</span></span>

    "sendRequest": {"value": 10000.0},
    "receiveRequest": {"value": 30000.0},
    "clientProcess": {"value": 17970000.0}

[<span data-ttu-id="f4b8e-176">세부 데이터는 hello 속성 형식 및 값에 대 한 참조를 모델링합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-176">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)

## <a name="processing-hello-data"></a><span data-ttu-id="f4b8e-177">Hello 데이터 처리</span><span class="sxs-lookup"><span data-stu-id="f4b8e-177">Processing hello data</span></span>
<span data-ttu-id="f4b8e-178">작은 규모에서 떨어져 있는 일부 코드 toopull 데이터 작성, 스프레드시트에 읽기 및 등 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-178">On a small scale, you can write some code toopull apart your data, read it into a spreadsheet, and so on.</span></span> <span data-ttu-id="f4b8e-179">예:</span><span class="sxs-lookup"><span data-stu-id="f4b8e-179">For example:</span></span>

    private IEnumerable<T> DeserializeMany<T>(string folderName)
    {
      var files = Directory.EnumerateFiles(folderName, "*.blob", SearchOption.AllDirectories);
      foreach (var file in files)
      {
         using (var fileReader = File.OpenText(file))
         {
            string fileContent = fileReader.ReadToEnd();
            IEnumerable<string> entities = fileContent.Split('\n').Where(s => !string.IsNullOrWhiteSpace(s));
            foreach (var entity in entities)
            {
                yield return JsonConvert.DeserializeObject<T>(entity);
            }
         }
      }
    }

<span data-ttu-id="f4b8e-180">더 큰 코드 샘플에 대해서는 [작업자 역할 사용][exportasa]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-180">For a larger code sample, see [using a worker role][exportasa].</span></span>

## <span data-ttu-id="f4b8e-181"><a name="delete"></a>이전 데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="f4b8e-181"><a name="delete"></a>Delete your old data</span></span>
<span data-ttu-id="f4b8e-182">저장소 용량을 관리 하 고 필요한 경우 hello 오래 된 데이터 삭제에 대 한 책임이 note 하십시오.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-182">Please note that you are responsible for managing your storage capacity and deleting hello old data if necessary.</span></span>

## <a name="if-you-regenerate-your-storage-key"></a><span data-ttu-id="f4b8e-183">저장소 키를 다시 생성하는 경우...</span><span class="sxs-lookup"><span data-stu-id="f4b8e-183">If you regenerate your storage key...</span></span>
<span data-ttu-id="f4b8e-184">Hello tooyour 키 저장소를 변경 하면 연속 내보내기를 작동이 중지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-184">If you change hello key tooyour storage, continuous export will stop working.</span></span> <span data-ttu-id="f4b8e-185">Azure 계정에 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-185">You'll see a notification in your Azure account.</span></span>

<span data-ttu-id="f4b8e-186">Hello 연속 내보내기가 블레이드를 열고 내보내기의 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-186">Open hello Continuous Export blade and edit your export.</span></span> <span data-ttu-id="f4b8e-187">내보내기 대상 hello 편집 하지만 동일한 저장소 선택 hello 둡니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-187">Edit hello Export Destination, but just leave hello same storage selected.</span></span> <span data-ttu-id="f4b8e-188">Tooconfirm 확인을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-188">Click OK tooconfirm.</span></span>

![편집 hello 연속 내보내기을 열고 내보내기 대상을 다음 닫습니다.](./media/app-insights-export-telemetry/07-resetstore.png)

<span data-ttu-id="f4b8e-190">hello 연속 내보내기를 다시 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-190">hello continuous export will restart.</span></span>

## <a name="export-samples"></a><span data-ttu-id="f4b8e-191">내보내기 샘플</span><span class="sxs-lookup"><span data-stu-id="f4b8e-191">Export samples</span></span>

* <span data-ttu-id="f4b8e-192">[스트림 분석을 사용 하 여 내보내기 tooSQL][exportasa]</span><span class="sxs-lookup"><span data-stu-id="f4b8e-192">[Export tooSQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="f4b8e-193">Stream Analytics 샘플 2</span><span class="sxs-lookup"><span data-stu-id="f4b8e-193">Stream Analytics sample 2</span></span>](app-insights-export-stream-analytics.md)

<span data-ttu-id="f4b8e-194">더 큰 눈금에서 고려해 [HDInsight](https://azure.microsoft.com/services/hdinsight/) -hello 클라우드에서 Hadoop 클러스터.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-194">On larger scales, consider [HDInsight](https://azure.microsoft.com/services/hdinsight/) - Hadoop clusters in hello cloud.</span></span> <span data-ttu-id="f4b8e-195">HDInsight 다양 한 기술 관리 하 고 빅 데이터 분석을 제공 하 고 Application Insights에서 내보낸 tooprocess 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-195">HDInsight provides a variety of technologies for managing and analyzing big data, and you could use it tooprocess data that has been exported from Application Insights.</span></span>

## <a name="q--a"></a><span data-ttu-id="f4b8e-196">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="f4b8e-196">Q & A</span></span>
* <span data-ttu-id="f4b8e-197">*하지만 원하는 모든 것은 차트의 일회성 다운로드입니다.*</span><span class="sxs-lookup"><span data-stu-id="f4b8e-197">*But all I want is a one-time download of a chart.*</span></span>  

    <span data-ttu-id="f4b8e-198">예, 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-198">Yes, you can do that.</span></span> <span data-ttu-id="f4b8e-199">Hello 블레이드의 hello 위쪽 클릭 **데이터 내보내기**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-199">At hello top of hello blade, click **Export Data**.</span></span>
* <span data-ttu-id="f4b8e-200">*내보내기를 설정했지만 내 저장소에 데이터가 없습니다.*</span><span class="sxs-lookup"><span data-stu-id="f4b8e-200">*I set up an export, but there's no data in my store.*</span></span>

    <span data-ttu-id="f4b8e-201">Application Insights 받는지 모든 원격 분석 응용 프로그램에서 hello 내보내기를 설정한 후?</span><span class="sxs-lookup"><span data-stu-id="f4b8e-201">Did Application Insights receive any telemetry from your app since you set up hello export?</span></span> <span data-ttu-id="f4b8e-202">새 데이터만 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-202">You'll only receive new data.</span></span>
* <span data-ttu-id="f4b8e-203">*export를 tooset I 했으나 액세스가 거부 되었습니다.*</span><span class="sxs-lookup"><span data-stu-id="f4b8e-203">*I tried tooset up an export, but was denied access*</span></span>

    <span data-ttu-id="f4b8e-204">Hello 계정 조직에서 소유 하 고, 있으면 toobe hello 소유자 또는 참가자 그룹의 구성원입니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-204">If hello account is owned by your organization, you have toobe a member of hello owners or contributors groups.</span></span>
* <span data-ttu-id="f4b8e-205">*직선 toomy 자체 온-프레미스 저장소를 내보낼 수 있습니까?*</span><span class="sxs-lookup"><span data-stu-id="f4b8e-205">*Can I export straight toomy own on-premises store?*</span></span>

    <span data-ttu-id="f4b8e-206">아니요. 죄송합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-206">No, sorry.</span></span> <span data-ttu-id="f4b8e-207">우리의 내보내기 엔진은 현재 Azure 저장소에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-207">Our export engine currently only works with Azure storage at this time.</span></span>  
* <span data-ttu-id="f4b8e-208">*모든 제한 toohello 양의 내 저장소에 저장 하는 데이터는 무엇입니까?*</span><span class="sxs-lookup"><span data-stu-id="f4b8e-208">*Is there any limit toohello amount of data you put in my store?*</span></span>

    <span data-ttu-id="f4b8e-209">아니요.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-209">No.</span></span> <span data-ttu-id="f4b8e-210">म 합니다 유지 데이터 될 때까지 밀어 hello 내보내기를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-210">We'll keep pushing data in until you delete hello export.</span></span> <span data-ttu-id="f4b8e-211">Blob 저장소에 대 한 외부 제한을 hello 도달할 수 있지만 매우 큰 경우 중지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-211">We'll stop if we hit hello outer limits for blob storage, but that's pretty huge.</span></span> <span data-ttu-id="f4b8e-212">중인지 tooyou toocontrol 저장소 사용 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-212">It's up tooyou toocontrol how much storage you use.</span></span>  
* <span data-ttu-id="f4b8e-213">*Hello 저장소에서 볼 수 blob?*</span><span class="sxs-lookup"><span data-stu-id="f4b8e-213">*How many blobs should I see in hello storage?*</span></span>

  * <span data-ttu-id="f4b8e-214">모든 데이터 형식에 대해 선택한 tooexport, 새로운 blob (데이터 파일이 있는 경우) 1 분 마다 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-214">For every data type you selected tooexport, a new blob is created every minute (if data is available).</span></span>
  * <span data-ttu-id="f4b8e-215">또한, 트래픽이 많은 응용 프로그램은 추가 파티션이 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-215">In addition, for applications with high traffic, additional partition units are allocated.</span></span> <span data-ttu-id="f4b8e-216">이 경우 모든 각 유닛이 매 분마다 blob을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-216">In this case each unit creates a blob every minute.</span></span>
* <span data-ttu-id="f4b8e-217">*Hello toomy 키 저장소를 다시 생성 I 또는 hello 컨테이너의 hello 이름을 변경 하 고 hello 내보내기 현재 작동 하지 않습니다.*</span><span class="sxs-lookup"><span data-stu-id="f4b8e-217">*I regenerated hello key toomy storage or changed hello name of hello container, and now hello export doesn't work.*</span></span>

    <span data-ttu-id="f4b8e-218">Hello 내보내기를 편집 하 고 hello 내보내기 대상 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-218">Edit hello export and open hello export destination blade.</span></span> <span data-ttu-id="f4b8e-219">동일한 저장소 이전과 마찬가지로 선택 hello 두고 tooconfirm 확인을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-219">Leave hello same storage selected as before, and click OK tooconfirm.</span></span> <span data-ttu-id="f4b8e-220">내보내기가 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-220">Export will restart.</span></span> <span data-ttu-id="f4b8e-221">지난 몇 일 동안 hello 내 hello 변경 되었으면 데이터가 손실 되지 않고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-221">If hello change was within hello past few days, you won't lose data.</span></span>
* <span data-ttu-id="f4b8e-222">*Hello 내보내기 일시 중지할 수 있습니까?*</span><span class="sxs-lookup"><span data-stu-id="f4b8e-222">*Can I pause hello export?*</span></span>

    <span data-ttu-id="f4b8e-223">예.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-223">Yes.</span></span> <span data-ttu-id="f4b8e-224">사용 안함을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-224">Click Disable.</span></span>

## <a name="code-samples"></a><span data-ttu-id="f4b8e-225">코드 샘플</span><span class="sxs-lookup"><span data-stu-id="f4b8e-225">Code samples</span></span>

* [<span data-ttu-id="f4b8e-226">Stream Analytics 샘플</span><span class="sxs-lookup"><span data-stu-id="f4b8e-226">Stream Analytics sample</span></span>](app-insights-export-stream-analytics.md)
* <span data-ttu-id="f4b8e-227">[스트림 분석을 사용 하 여 내보내기 tooSQL][exportasa]</span><span class="sxs-lookup"><span data-stu-id="f4b8e-227">[Export tooSQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="f4b8e-228">세부 데이터는 hello 속성 형식 및 값에 대 한 참조를 모델링합니다.</span><span class="sxs-lookup"><span data-stu-id="f4b8e-228">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)

<!--Link references-->

[exportasa]: app-insights-code-sample-export-sql-stream-analytics.md
[roles]: app-insights-resources-roles-access-control.md
