---
title: "Application Insights에서 원격 분석 연속 내보내기 | Microsoft Docs"
description: "Microsoft Azure에서 저장소에 진단 및 사용량 데이터를 내보내고 여기에서 다운로드합니다."
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
ms.openlocfilehash: 6ac3bda5101593b5ca66b4c9035e2fdac9d1e833
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="export-telemetry-from-application-insights"></a><span data-ttu-id="fe105-103">Application Insights에서 원격 분석 내보내기</span><span class="sxs-lookup"><span data-stu-id="fe105-103">Export telemetry from Application Insights</span></span>
<span data-ttu-id="fe105-104">표준 보존 기간 보다 오랫동안 원격 분석을 유지하시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="fe105-104">Want to keep your telemetry for longer than the standard retention period?</span></span> <span data-ttu-id="fe105-105">또는 일부 특수한 방식으로 처리하시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="fe105-105">Or process it in some specialized way?</span></span> <span data-ttu-id="fe105-106">그렇다면 연속 내보내기가 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-106">Continuous Export is ideal for this.</span></span> <span data-ttu-id="fe105-107">Application Insights 포털에 표시되는 이벤트는 JSON 형식으로 Microsoft Azure에서 저장소로 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-107">The events you see in the Application Insights portal can be exported to storage in Microsoft Azure in JSON format.</span></span> <span data-ttu-id="fe105-108">여기에서 데이터를 다운로드하고 프로세스에 필요한 모든 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-108">From there you can download your data and write whatever code you need to process it.</span></span>  

<span data-ttu-id="fe105-109">연속 내보내기를 사용할 경우 추가 요금이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-109">Using Continuous Export may incur an additional charge.</span></span> <span data-ttu-id="fe105-110">[가격 책정 모델](http://azure.microsoft.com/pricing/details/application-insights/)을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="fe105-110">Check your [pricing model](http://azure.microsoft.com/pricing/details/application-insights/).</span></span>

<span data-ttu-id="fe105-111">연속 내보내기를 설정하기 전에 고려하려는 일부 대안이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-111">Before you set up continuous export, there are some alternatives you might want to consider:</span></span>

* <span data-ttu-id="fe105-112">메트릭 또는 검색 블레이드 맨 위에 있는 내보내기 단추를 사용하면 테이블 및 차트를 Excel 스프레드시트에 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-112">The Export button at the top of a metrics or search blade lets you transfer tables and charts to an Excel spreadsheet.</span></span>

* <span data-ttu-id="fe105-113">[분석](app-insights-analytics.md)은 원격 분석을 위한 강력한 쿼리 언어를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-113">[Analytics](app-insights-analytics.md) provides a powerful query language for telemetry.</span></span> <span data-ttu-id="fe105-114">결과를 내보낼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-114">It can also export results.</span></span>
* <span data-ttu-id="fe105-115">[Power BI에서 데이터를 탐색](app-insights-export-power-bi.md)하려는 경우 연속 내보내기를 사용하지 않고 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-115">If you're looking to [explore your data in Power BI](app-insights-export-power-bi.md), you can do that without using Continuous Export.</span></span>
* <span data-ttu-id="fe105-116">[데이터 액세스 REST API](https://dev.applicationinsights.io/)를 사용하여 원격 분석에 프로그래밍 방식으로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-116">The [Data access REST API](https://dev.applicationinsights.io/) lets you access your telemetry programmatically.</span></span>

<span data-ttu-id="fe105-117">연속 내보내기를 통해 저장소에 데이터를 복사한 후에도(원하는 기간 동안 저장소에 유지할 수 있음) 일반적인 [보존 기간](app-insights-data-retention-privacy.md) 동안 Application Insights를 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-117">After Continuous Export copies your data to storage (where it can stay for as long as you like), it's still available in Application Insights for the usual [retention period](app-insights-data-retention-privacy.md).</span></span>

## <span data-ttu-id="fe105-118"><a name="setup"></a> 연속 내보내기 만들기</span><span class="sxs-lookup"><span data-stu-id="fe105-118"><a name="setup"></a> Create a Continuous Export</span></span>
1. <span data-ttu-id="fe105-119">앱에 대 한 Application Insights 리소스에서 연속 내보내기를 열고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-119">In the Application Insights resource for your app, open Continuous Export and choose **Add**:</span></span>

    ![아래로 스크롤하여 연속 내보내기 클릭](./media/app-insights-export-telemetry/01-export.png)

2. <span data-ttu-id="fe105-121">내보낼 원격 분석 데이터 유형을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-121">Choose the telemetry data types you want to export.</span></span>

3. <span data-ttu-id="fe105-122">데이터를 저장할 [Azure Storage 계정](../storage/common/storage-introduction.md)을 만들거나 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-122">Create or select an [Azure storage account](../storage/common/storage-introduction.md) where you want to store the data.</span></span>

    > [!Warning]
    > <span data-ttu-id="fe105-123">기본적으로 저장소 위치는 Application Insights 리소스와 동일한 지역으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-123">By default, the storage location will be set to the same geographical region as your Application Insights resource.</span></span> <span data-ttu-id="fe105-124">다른 지역에 저장하는 경우 전송 요금이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-124">If you store in a different region, you may incur transfer charges.</span></span>

    ![추가, 내보내기 대상, 저장소 계정을 클릭한 다음 새 저장소를 만들거나 기존 저장소 선택](./media/app-insights-export-telemetry/02-add.png)

4. <span data-ttu-id="fe105-126">저장소에서 컨테이너를 만들거나 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-126">Create or select a container in the storage:</span></span>

    ![이벤트 유형 선택 클릭](./media/app-insights-export-telemetry/create-container.png)

<span data-ttu-id="fe105-128">내보내기를 만들면 진행을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-128">Once you've created your export, it starts going.</span></span> <span data-ttu-id="fe105-129">내보내기를 만든 후에는 도착하는 데이터만 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-129">You only get data that arrives after you create the export.</span></span>

<span data-ttu-id="fe105-130">데이터가 저장소에 표시되려면 1시간 정도 지연될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-130">There can be a delay of about an hour before data appears in the storage.</span></span>

### <a name="to-edit-continuous-export"></a><span data-ttu-id="fe105-131">연속 내보내기를 편집하려면</span><span class="sxs-lookup"><span data-stu-id="fe105-131">To edit continuous export</span></span>

<span data-ttu-id="fe105-132">나중에 이벤트 유형을 변경하려는 경우 내보내기를 편집하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-132">If you want to change the event types later, just edit the export:</span></span>

![이벤트 유형 선택 클릭](./media/app-insights-export-telemetry/05-edit.png)

### <a name="to-stop-continuous-export"></a><span data-ttu-id="fe105-134">연속 내보내기를 중지하려면</span><span class="sxs-lookup"><span data-stu-id="fe105-134">To stop continuous export</span></span>

<span data-ttu-id="fe105-135">스트림을 중지하려면 사용 안 함을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-135">To stop the export, click Disable.</span></span> <span data-ttu-id="fe105-136">사용을 다시 클릭하면 내보내기는 새 데이터로 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-136">When you click Enable again, the export will restart with new data.</span></span> <span data-ttu-id="fe105-137">내보내기를 사용하지 않는 동안 포털에 도착한 데이터는 받지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-137">You won't get the data that arrived in the portal while export was disabled.</span></span>

<span data-ttu-id="fe105-138">내보내기를 영구적으로 중지하려면 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-138">To stop the export permanently, delete it.</span></span> <span data-ttu-id="fe105-139">이렇게 해도 저장소에서 데이터를 삭제하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-139">Doing so doesn't delete your data from storage.</span></span>

### <a name="cant-add-or-change-an-export"></a><span data-ttu-id="fe105-140">내보내기를 추가 또는 변경할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="fe105-140">Can't add or change an export?</span></span>
* <span data-ttu-id="fe105-141">내보내기를 추가 또는 변경하려면 소유자, 참여자 또는 Application Insights 참여자 액세스 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-141">To add or change exports, you need Owner, Contributor or Application Insights Contributor access rights.</span></span> <span data-ttu-id="fe105-142">[역할에 대해 알아봅니다][roles].</span><span class="sxs-lookup"><span data-stu-id="fe105-142">[Learn about roles][roles].</span></span>

## <span data-ttu-id="fe105-143"><a name="analyze"></a> 어떤 이벤트를 얻나요?</span><span class="sxs-lookup"><span data-stu-id="fe105-143"><a name="analyze"></a> What events do you get?</span></span>
<span data-ttu-id="fe105-144">클라이언트 IP 주소에서 계산하는 위치 데이터를 추가한다는 점을 제외하고 내보낸 데이터는 응용 프로그램에서 수신하는 원시 원격 분석입니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-144">The exported data is the raw telemetry we receive from your application, except that we add location data which we calculate from the client IP address.</span></span>

<span data-ttu-id="fe105-145">[샘플링](app-insights-sampling.md) 에서 무시된 데이터는 내보낸 데이터에 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-145">Data that has been discarded by [sampling](app-insights-sampling.md) is not included in the exported data.</span></span>

<span data-ttu-id="fe105-146">계산된 다른 메트릭은 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-146">Other calculated metrics are not included.</span></span> <span data-ttu-id="fe105-147">예를들어 평균 CPU 사용률을 내보내지 않지만 평균이 계산된 곳에서 원시 원격 분석을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-147">For example, we don't export average CPU utilisation, but we do export the raw telemetry from which the average is computed.</span></span>

<span data-ttu-id="fe105-148">데이터에는 설정한 [가용성 웹 테스트](app-insights-monitor-web-app-availability.md)의 결과도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-148">The data also includes the results of any [availability web tests](app-insights-monitor-web-app-availability.md) that you have set up.</span></span>

> [!NOTE]
> <span data-ttu-id="fe105-149">**샘플링**</span><span class="sxs-lookup"><span data-stu-id="fe105-149">**Sampling.**</span></span> <span data-ttu-id="fe105-150">응용 프로그램에서 많은 양의 데이터를 전송하는 경우 샘플링 기능이 작동하여 생성된 원격 분석의 일부만 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-150">If your application sends a lot of data, the sampling feature may operate and send only a fraction of the generated telemetry.</span></span> [<span data-ttu-id="fe105-151">샘플링에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-151">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <span data-ttu-id="fe105-152"><a name="get"></a> 데이터 검사</span><span class="sxs-lookup"><span data-stu-id="fe105-152"><a name="get"></a> Inspect the data</span></span>
<span data-ttu-id="fe105-153">포털에서 직접 저장소를 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-153">You can inspect the storage directly in the portal.</span></span> <span data-ttu-id="fe105-154">**찾아보기**를 클릭하고 저장소 계정을 선택한 후 **컨테이너**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-154">Click **Browse**, select your storage account, and then open **Containers**.</span></span>

<span data-ttu-id="fe105-155">Visual Studio에서 Azure Storage를 검사하려면 **보기**, **클라우드 탐색기**를 차례로 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-155">To inspect Azure storage in Visual Studio, open **View**, **Cloud Explorer**.</span></span> <span data-ttu-id="fe105-156">(해당 메뉴 명령이 없는 경우 Azure SDK를 설치해야 합니다. **새 프로젝트** 대화 상자를 열고 Visual C#/클라우드를 확장한 다음 **.NET용 Microsoft Azure SDK 가져오기**를 선택합니다.)</span><span class="sxs-lookup"><span data-stu-id="fe105-156">(If you don't have that menu command, you need to install the Azure SDK: Open the **New Project** dialog, expand Visual C#/Cloud and choose **Get Microsoft Azure SDK for .NET**.)</span></span>

<span data-ttu-id="fe105-157">blob 저장소를 열면 blob 파일 집합이 포함된 컨테이너가 보입니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-157">When you open your blob store, you'll see a container with a set of blob files.</span></span> <span data-ttu-id="fe105-158">Application Insights 리소스 이름, 계측 키, 원격 분석 유형/날짜/시간에서 파생된 각 파일의 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-158">The URI of each file derived from your Application Insights resource name, its instrumentation key, telemetry-type/date/time.</span></span> <span data-ttu-id="fe105-159">리소스 이름은 모두 소문자이고 계측 키에서 대시를 생략합니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-159">(The resource name is all lowercase, and the instrumentation key omits dashes.)</span></span>

![적합한 도구를 사용하여 blob 저장소 검사](./media/app-insights-export-telemetry/04-data.png)

<span data-ttu-id="fe105-161">날짜 및 시간은 UTC이며 생성된 시간이 아니라 원격 분석이 저장소에 보관된 시기입니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-161">The date and time are UTC and are when the telemetry was deposited in the store - not the time it was generated.</span></span> <span data-ttu-id="fe105-162">따라서 데이터를 다운로드할 코드를 작성하는 경우 데이터를 선형으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-162">So if you write code to download the data, it can move linearly through the data.</span></span>

<span data-ttu-id="fe105-163">경로의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-163">Here's the form of the path:</span></span>

    $"{applicationName}_{instrumentationKey}/{type}/{blobDeliveryTimeUtc:yyyy-MM-dd}/{ blobDeliveryTimeUtc:HH}/{blobId}_{blobCreationTimeUtc:yyyyMMdd_HHmmss}.blob"

<span data-ttu-id="fe105-164">Where</span><span class="sxs-lookup"><span data-stu-id="fe105-164">Where</span></span>

* <span data-ttu-id="fe105-165">`blobCreationTimeUtc` 는 Blob이 내부 준비 저장소에 만들어진 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-165">`blobCreationTimeUtc` is time when blob was created in the internal staging storage</span></span>
* <span data-ttu-id="fe105-166">`blobDeliveryTimeUtc` 는 Blob이 내보내기 대상 저장소에 복사되는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-166">`blobDeliveryTimeUtc` is the time when blob is copied to the export destination storage</span></span>

## <span data-ttu-id="fe105-167"><a name="format"></a> 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="fe105-167"><a name="format"></a> Data format</span></span>
* <span data-ttu-id="fe105-168">각 blob은 다중 '\n'-separated 행을 포함하는 텍스트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-168">Each blob is a text file that contains multiple '\n'-separated rows.</span></span> <span data-ttu-id="fe105-169">여기에는 약 30초 동안 처리된 원격 분석 데이터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-169">It contains the telemetry processed over a time period of roughly half a minute.</span></span>
* <span data-ttu-id="fe105-170">각 행은 요청 또는 페이지 보기와 같은 원격 분석 데이터 요소를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-170">Each row represents a telemetry data point such as a request or page view.</span></span>
* <span data-ttu-id="fe105-171">각 행은 서식이 지정되지 않은 JSON 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-171">Each row is an unformatted JSON document.</span></span> <span data-ttu-id="fe105-172">관찰만 하려는 경우 Visual Studio에서 열고 편집, 고급, 형식 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-172">If you want to sit and stare at it, open it in Visual Studio and choose Edit, Advanced, Format File:</span></span>

![적합한 도구를 사용하여 원격 분석 보기](./media/app-insights-export-telemetry/06-json.png)

<span data-ttu-id="fe105-174">시간 기간은 틱 단위이며 10,000틱은 1ms입니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-174">Time durations are in ticks, where 10 000 ticks = 1ms.</span></span> <span data-ttu-id="fe105-175">예를 들어 이러한 값은 브라우저에서 요청을 보내는 데 1ms, 받는 데 3ms, 브라우저에서 페이지를 처리하는 데 1.8s를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-175">For example, these values show a time of 1ms to send a request from the browser, 3ms to receive it, and 1.8s to process the page in the browser:</span></span>

    "sendRequest": {"value": 10000.0},
    "receiveRequest": {"value": 30000.0},
    "clientProcess": {"value": 17970000.0}

[<span data-ttu-id="fe105-176">속성 형식 및 값에 대한 자세한 데이터 모델 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-176">Detailed data model reference for the property types and values.</span></span>](app-insights-export-data-model.md)

## <a name="processing-the-data"></a><span data-ttu-id="fe105-177">데이터 처리</span><span class="sxs-lookup"><span data-stu-id="fe105-177">Processing the data</span></span>
<span data-ttu-id="fe105-178">작은 규모에서 데이터를 분리하고, 스프레드시트에서 읽는 등의 처리를 위한 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-178">On a small scale, you can write some code to pull apart your data, read it into a spreadsheet, and so on.</span></span> <span data-ttu-id="fe105-179">예:</span><span class="sxs-lookup"><span data-stu-id="fe105-179">For example:</span></span>

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

<span data-ttu-id="fe105-180">더 큰 코드 샘플에 대해서는 [작업자 역할 사용][exportasa]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe105-180">For a larger code sample, see [using a worker role][exportasa].</span></span>

## <span data-ttu-id="fe105-181"><a name="delete"></a>이전 데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="fe105-181"><a name="delete"></a>Delete your old data</span></span>
<span data-ttu-id="fe105-182">필요한 경우 스토리지 용량을 관리하고 오래된 데이터를 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-182">Please note that you are responsible for managing your storage capacity and deleting the old data if necessary.</span></span>

## <a name="if-you-regenerate-your-storage-key"></a><span data-ttu-id="fe105-183">저장소 키를 다시 생성하는 경우...</span><span class="sxs-lookup"><span data-stu-id="fe105-183">If you regenerate your storage key...</span></span>
<span data-ttu-id="fe105-184">저장소 키를 변경하는 경우 연속 내보내기 작업이 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-184">If you change the key to your storage, continuous export will stop working.</span></span> <span data-ttu-id="fe105-185">Azure 계정에 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-185">You'll see a notification in your Azure account.</span></span>

<span data-ttu-id="fe105-186">연속 내보내기 블레이드를 열고 내보내기를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-186">Open the Continuous Export blade and edit your export.</span></span> <span data-ttu-id="fe105-187">내보내기 대상을 편집하되 선택한 것과 동일한 저장소는 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-187">Edit the Export Destination, but just leave the same storage selected.</span></span> <span data-ttu-id="fe105-188">확인을 클릭하여 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-188">Click OK to confirm.</span></span>

![연속 내보내기를 편집하고 내보내기 대상을 열고 닫기](./media/app-insights-export-telemetry/07-resetstore.png)

<span data-ttu-id="fe105-190">연속 내보내기가 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-190">The continuous export will restart.</span></span>

## <a name="export-samples"></a><span data-ttu-id="fe105-191">내보내기 샘플</span><span class="sxs-lookup"><span data-stu-id="fe105-191">Export samples</span></span>

* <span data-ttu-id="fe105-192">[Stream Analytics를 사용하여 SQL로 내보내기][exportasa]</span><span class="sxs-lookup"><span data-stu-id="fe105-192">[Export to SQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="fe105-193">Stream Analytics 샘플 2</span><span class="sxs-lookup"><span data-stu-id="fe105-193">Stream Analytics sample 2</span></span>](app-insights-export-stream-analytics.md)

<span data-ttu-id="fe105-194">더 큰 규모에서는 [HDInsight](https://azure.microsoft.com/services/hdinsight/) (클라우드의 Hadoop 클러스터)를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-194">On larger scales, consider [HDInsight](https://azure.microsoft.com/services/hdinsight/) - Hadoop clusters in the cloud.</span></span> <span data-ttu-id="fe105-195">HDInsight는 빅 데이터에 대한 다양한 관리 분석 기술을 제공하므로 이를 사용하여 Application Insights에서 내보낸 데이터를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-195">HDInsight provides a variety of technologies for managing and analyzing big data, and you could use it to process data that has been exported from Application Insights.</span></span>

## <a name="q--a"></a><span data-ttu-id="fe105-196">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="fe105-196">Q & A</span></span>
* <span data-ttu-id="fe105-197">*하지만 원하는 모든 것은 차트의 일회성 다운로드입니다.*</span><span class="sxs-lookup"><span data-stu-id="fe105-197">*But all I want is a one-time download of a chart.*</span></span>  

    <span data-ttu-id="fe105-198">예, 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-198">Yes, you can do that.</span></span> <span data-ttu-id="fe105-199">블레이드 맨 위에서 **데이터 내보내기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-199">At the top of the blade, click **Export Data**.</span></span>
* <span data-ttu-id="fe105-200">*내보내기를 설정했지만 내 저장소에 데이터가 없습니다.*</span><span class="sxs-lookup"><span data-stu-id="fe105-200">*I set up an export, but there's no data in my store.*</span></span>

    <span data-ttu-id="fe105-201">내보내기를 설정한 후 Application Insights가 앱에서 원격 분석을 받았나요?</span><span class="sxs-lookup"><span data-stu-id="fe105-201">Did Application Insights receive any telemetry from your app since you set up the export?</span></span> <span data-ttu-id="fe105-202">새 데이터만 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-202">You'll only receive new data.</span></span>
* <span data-ttu-id="fe105-203">*내보내기를 설정하려 했지만 액세스가 거부되었습니다.*</span><span class="sxs-lookup"><span data-stu-id="fe105-203">*I tried to set up an export, but was denied access*</span></span>

    <span data-ttu-id="fe105-204">계정이 조직 소유인 경우 소유자 또는 참여자 그룹의 구성원이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-204">If the account is owned by your organization, you have to be a member of the owners or contributors groups.</span></span>
* <span data-ttu-id="fe105-205">*나만의 온-프레미스 저장소로 직접 내보낼 수 있나요?*</span><span class="sxs-lookup"><span data-stu-id="fe105-205">*Can I export straight to my own on-premises store?*</span></span>

    <span data-ttu-id="fe105-206">아니요. 죄송합니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-206">No, sorry.</span></span> <span data-ttu-id="fe105-207">우리의 내보내기 엔진은 현재 Azure 저장소에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-207">Our export engine currently only works with Azure storage at this time.</span></span>  
* <span data-ttu-id="fe105-208">*내 저장소에 보관하는 데이터량에 제한이 있나요?*</span><span class="sxs-lookup"><span data-stu-id="fe105-208">*Is there any limit to the amount of data you put in my store?*</span></span>

    <span data-ttu-id="fe105-209">아니요.</span><span class="sxs-lookup"><span data-stu-id="fe105-209">No.</span></span> <span data-ttu-id="fe105-210">내보내기를 삭제할 때까지 푸싱한 데이터를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-210">We'll keep pushing data in until you delete the export.</span></span> <span data-ttu-id="fe105-211">blob 저장소에 대한 외부 제한에 도달하는 경우 중지하지만 제한은 상당히 큽니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-211">We'll stop if we hit the outer limits for blob storage, but that's pretty huge.</span></span> <span data-ttu-id="fe105-212">사용자가 이용하는 저장소 크기는 사용자가 제어하기 나름입니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-212">It's up to you to control how much storage you use.</span></span>  
* <span data-ttu-id="fe105-213">*저장소에서 몇 개의 BLOB를 볼 수 있나요?*</span><span class="sxs-lookup"><span data-stu-id="fe105-213">*How many blobs should I see in the storage?*</span></span>

  * <span data-ttu-id="fe105-214">내보내려고 선택한 모든 데이터 형식에 대해 새 blob(데이터 파일이 사용 가능한 경우)이 매 분마다 만들어 집니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-214">For every data type you selected to export, a new blob is created every minute (if data is available).</span></span>
  * <span data-ttu-id="fe105-215">또한, 트래픽이 많은 응용 프로그램은 추가 파티션이 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-215">In addition, for applications with high traffic, additional partition units are allocated.</span></span> <span data-ttu-id="fe105-216">이 경우 모든 각 유닛이 매 분마다 blob을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-216">In this case each unit creates a blob every minute.</span></span>
* <span data-ttu-id="fe105-217">*내 저장소 키를 다시 생성하거나 컨테이너의 이름을 변경한 경우에는 현재 내보내기가 동작하지 않습니다.*</span><span class="sxs-lookup"><span data-stu-id="fe105-217">*I regenerated the key to my storage or changed the name of the container, and now the export doesn't work.*</span></span>

    <span data-ttu-id="fe105-218">내보내기를 편집하고 내보내기 대상 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-218">Edit the export and open the export destination blade.</span></span> <span data-ttu-id="fe105-219">이전과 마찬가지로 선택된 것과 동일한 저장소는 그대로 두고 확인을 클릭하여 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-219">Leave the same storage selected as before, and click OK to confirm.</span></span> <span data-ttu-id="fe105-220">내보내기가 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-220">Export will restart.</span></span> <span data-ttu-id="fe105-221">지난 몇 일 이내에 변경된 경우 데이터가 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-221">If the change was within the past few days, you won't lose data.</span></span>
* <span data-ttu-id="fe105-222">*내보내기를 일시 중지할 수 있나요?*</span><span class="sxs-lookup"><span data-stu-id="fe105-222">*Can I pause the export?*</span></span>

    <span data-ttu-id="fe105-223">예.</span><span class="sxs-lookup"><span data-stu-id="fe105-223">Yes.</span></span> <span data-ttu-id="fe105-224">사용 안함을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-224">Click Disable.</span></span>

## <a name="code-samples"></a><span data-ttu-id="fe105-225">코드 샘플</span><span class="sxs-lookup"><span data-stu-id="fe105-225">Code samples</span></span>

* [<span data-ttu-id="fe105-226">Stream Analytics 샘플</span><span class="sxs-lookup"><span data-stu-id="fe105-226">Stream Analytics sample</span></span>](app-insights-export-stream-analytics.md)
* <span data-ttu-id="fe105-227">[Stream Analytics를 사용하여 SQL로 내보내기][exportasa]</span><span class="sxs-lookup"><span data-stu-id="fe105-227">[Export to SQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="fe105-228">속성 형식 및 값에 대한 자세한 데이터 모델 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="fe105-228">Detailed data model reference for the property types and values.</span></span>](app-insights-export-data-model.md)

<!--Link references-->

[exportasa]: app-insights-code-sample-export-sql-stream-analytics.md
[roles]: app-insights-resources-roles-access-control.md
