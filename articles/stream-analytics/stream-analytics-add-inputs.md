---
title: "Stream Analytics 작업에 데이터 입력 추가 | Microsoft Docs"
description: "데이터 원본을 스트리밍 데이터 입력(이벤트 허브) 또는 참조 데이터(블로그 저장소)로 Stream Analytics 작업에 연결하는 방법을 알아봅니다."
keywords: "데이터 입력, 스트리밍 데이터"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: 
ms.assetid: 9e59bd24-2a80-4ecb-b6b2-309a07c70bcd
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 8bdbcf78f2892cbd1e1cc09cef220dff08dd9490
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="add-a-streaming-data-input-or-reference-data-to-a-stream-analytics-job"></a><span data-ttu-id="890c9-104">Stream Analytics 작업에 스트리밍 데이터 입력 또는 참조 데이터 추가</span><span class="sxs-lookup"><span data-stu-id="890c9-104">Add a streaming data input or reference data to a Stream Analytics job</span></span>
<span data-ttu-id="890c9-105">Blob 저장소에서 참조 데이터 또는 이벤트 허브에서 데이터 입력을 스트리밍하면서 데이터 소스를 Stream Analytics 작업에 연결하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="890c9-105">Learn how to hook up a data source to your Stream Analytics job as streaming data input from Event Hubs or reference data from Blob storage.</span></span>

<span data-ttu-id="890c9-106">Azure Stream Analytics 작업은 각각의 기존 데이터 원본에 대한 연결을 정의하는 하나 이상의 데이터 입력에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="890c9-106">Azure Stream Analytics jobs can be connected to one data input or more, each of which define a connection to an existing data source.</span></span> <span data-ttu-id="890c9-107">데이터가 해당 데이터 원본에 전송되면 Stream Analytics 작업에서 사용되고 스트리밍 데이터와 같이 실시간으로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="890c9-107">As data is sent to that data source, it is consumed by the Stream Analytics job and processed in real time as streaming data.</span></span> <span data-ttu-id="890c9-108">Stream Analytics는 작업 구독 내부 및 외부의 [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) 및 [Azure Blob 저장소](../storage/blobs/storage-dotnet-how-to-use-blobs.md)와 높은 수준으로 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="890c9-108">Stream Analytics has first class integration with [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) and [Azure Blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md) both within and outside of the job's subscription.</span></span>

<span data-ttu-id="890c9-109">이 문서는 [Stream Analytics 학습 경로](/documentation/learning-paths/stream-analytics/)의 한 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="890c9-109">This article is a step in the [Stream Analytics learning path](/documentation/learning-paths/stream-analytics/).</span></span>

## <a name="data-input-streaming-data-and-reference-data"></a><span data-ttu-id="890c9-110">데이터 입력: 스트리밍 데이터 및 참조 데이터</span><span class="sxs-lookup"><span data-stu-id="890c9-110">Data input: Streaming data and reference data</span></span>
<span data-ttu-id="890c9-111">Stream Analytics에는 데이터 스트림 및 참조 데이터 이렇게 두 가지 입력 형식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="890c9-111">There are two distinct types of inputs in Stream Analytics: data streams and reference data.</span></span>

* <span data-ttu-id="890c9-112">**데이터 스트림**: Stream Analytics 작업은 작업에서 사용되고 변환될 하나 이상의 데이터 스트림 입력을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="890c9-112">**Data Streams**: Stream Analytics jobs must include at least one data stream input to be consumed and transformed by the job.</span></span> <span data-ttu-id="890c9-113">Azure Blob 저장소 및 Azure 이벤트 허브는 데이터 스트림 입력 소스로 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="890c9-113">Azure Blob storage and Azure Event Hubs are supported as data stream input sources.</span></span> <span data-ttu-id="890c9-114">Azure 이벤트 허브는 연결된 장치, 서비스 및 응용 프로그램에서 이벤트 스트림을 수집하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="890c9-114">Azure Event Hubs are used to collect event streams from connected devices, services and applications.</span></span> <span data-ttu-id="890c9-115">Azure Blob 저장소를 스트림으로 대량 데이터 수집을 위한 입력 소스로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="890c9-115">Azure Blob storage can be used as an input source for ingesting bulk data as a stream.</span></span>  
* <span data-ttu-id="890c9-116">**참조 데이터**: Stream Analytics은 참조 데이터라는 두 번째 형식의 보조 입력을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="890c9-116">**Reference data**: Stream Analytics supports a second type of auxiliary input called reference data.</span></span>  <span data-ttu-id="890c9-117">동작 중인 데이터와 반대로, 이 데이터는 정적이거나 느리게 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="890c9-117">As opposed to data in motion, this data is static or slowing changing.</span></span>  <span data-ttu-id="890c9-118">일반적으로 조회 및 데이터 스트림과의 상관 관계를 수행하여 보다 풍부한 데이터 집합을 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="890c9-118">It is typically used for performing look-ups and correlations with data streams to create a richer data set.</span></span>  <span data-ttu-id="890c9-119">Azure Blob 저장소는 현재 유일하게 지원되는 참조 데이터용 입력 소스입니다.</span><span class="sxs-lookup"><span data-stu-id="890c9-119">Azure Blob storage is currently the only supported input source for reference data.</span></span>  

<span data-ttu-id="890c9-120">Stream Analytics 작업에 입력을 추가하려면</span><span class="sxs-lookup"><span data-stu-id="890c9-120">To add an input to your Stream Analytics job:</span></span>

1. <span data-ttu-id="890c9-121">Azure Portal에서 **입력**을 클릭한 다음 Stream Analytics 작업에서 **입력 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="890c9-121">In the Azure portal click **Inputs** and then click **Add an Input** in your Stream Analytics job.</span></span>
   
    ![Azure 클래식 포털 - 입력을 추가합니다.](./media/stream-analytics-add-inputs/1-stream-analytics-add-inputs.png)  
   
    <span data-ttu-id="890c9-123">Azure 포털에서 Stream Analytics 작업의 **입력** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="890c9-123">In the Azure portal click the **Inputs** tile in your Stream Analytics job.</span></span>  
   
    ![Azure 포털 - 데이터 입력을 추가합니다.](./media/stream-analytics-add-inputs/7-stream-analytics-add-inputs.png)  
2. <span data-ttu-id="890c9-125">입력 형식(**데이터 스트림** 또는 **참조 데이터**)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="890c9-125">Specify the type of the input: either **Data stream** or **Reference data**.</span></span>
   
    ![올바른 데이터 입력, 스트리밍 또는 참조 추가](./media/stream-analytics-add-inputs/2-stream-analytics-add-inputs.png)  
   
    ![올바른 데이터 입력, 스트리밍 또는 참조 추가](./media/stream-analytics-add-inputs/8-stream-analytics-add-inputs.png)  
3. <span data-ttu-id="890c9-128">데이터 스트림 입력을 만드는 경우 입력 소스 유형을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="890c9-128">If creating a Data Stream input, specify the source type for the input.</span></span>  <span data-ttu-id="890c9-129">이때는 Blob 저장소만 지원되므로 참조 데이터를 만드는 동안에는 이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="890c9-129">This step can be skipped during Reference Data creation as only Blob storage is supported at this time.</span></span>
   
    ![데이터 스트림 데이터 입력 추가](./media/stream-analytics-add-inputs/3-stream-analytics-add-inputs.png)  
   
    ![데이터 스트림 데이터 입력 추가](./media/stream-analytics-add-inputs/9-stream-analytics-add-inputs.png)  
4. <span data-ttu-id="890c9-132">입력 별칭 상자에 이 입력의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="890c9-132">Provide a friendly name for this input in the Input Alias box.</span></span>  <span data-ttu-id="890c9-133">이 이름은 나중에 작업 쿼리에서 입력을 참조하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="890c9-133">This name will be used in your job's query later on to refer to the input.</span></span>
   
    <span data-ttu-id="890c9-134">데이터 원본에 연결하는 데 필요한 나머지 연결 속성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="890c9-134">Fill in the rest of the required connection properties to connect to your data source.</span></span> <span data-ttu-id="890c9-135">이러한 필드는 입력 형식 및 소스 형식마다 다르며 [여기](stream-analytics-create-a-job.md)에 자세히 정의되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="890c9-135">These fields vary by type of input and source type and are defined in detail [here](stream-analytics-create-a-job.md).</span></span>  
   
    ![이벤트 허브 데이터 입력 추가](./media/stream-analytics-add-inputs/4-stream-analytics-add-inputs.png)  
5. <span data-ttu-id="890c9-137">입력 데이터에 대한 직렬화 설정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="890c9-137">Specify the serialization settings for the input data:</span></span>
   
   * <span data-ttu-id="890c9-138">쿼리가 예상대로 작동하게 하려면 들어오는 데이터의 **이벤트 직렬화 형식** 을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="890c9-138">To make sure your queries work the way you expect, specify the **Event Serialization Format** of incoming data.</span></span>  <span data-ttu-id="890c9-139">지원되는 직렬화 형식은 JSON, CSV 및 Avro입니다.</span><span class="sxs-lookup"><span data-stu-id="890c9-139">Supported serialization formats are JSON, CSV, and Avro.</span></span>
   * <span data-ttu-id="890c9-140">데이터의 **인코딩** 을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="890c9-140">Verify the **Encoding** for the data.</span></span>  <span data-ttu-id="890c9-141">지금은 지원되는 인코딩 형식이 UTF-8뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="890c9-141">UTF-8 is the only supported encoding format at this time.</span></span>
     
     ![데이터 입력에 대한 데이터 직렬화 설정](./media/stream-analytics-add-inputs/5-stream-analytics-add-inputs.png)  
     
     ![데이터 입력에 대한 데이터 직렬화 설정](./media/stream-analytics-add-inputs/10-stream-analytics-add-inputs.png)  
6. <span data-ttu-id="890c9-144">입력 만들기를 완료한 후 Stream Analytics에서 입력 소스에 연결할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="890c9-144">After completing the input creation, Stream Analytics will verify that it can connect to the input source.</span></span>  <span data-ttu-id="890c9-145">알림 허브에서 연결 테스트 작업의 상태를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="890c9-145">You can view the status of the Test Connection operation in the Notification hub.</span></span>
   
    ![스트리밍 데이터 입력의 연결 테스트](./media/stream-analytics-add-inputs/6-stream-analytics-add-inputs.png)  
   
    ![스트리밍 데이터 입력의 연결 테스트](./media/stream-analytics-add-inputs/11-stream-analytics-add-inputs.png)  

## <a name="get-help-with-streaming-data-inputs"></a><span data-ttu-id="890c9-148">스트리밍 데이터 입력에 대한 도움 받기</span><span class="sxs-lookup"><span data-stu-id="890c9-148">Get help with streaming data inputs</span></span>
<span data-ttu-id="890c9-149">추가 지원이 필요할 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="890c9-149">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="890c9-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="890c9-150">Next steps</span></span>
* [<span data-ttu-id="890c9-151">Azure Stream Analytics 소개</span><span class="sxs-lookup"><span data-stu-id="890c9-151">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="890c9-152">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="890c9-152">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="890c9-153">Azure  Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="890c9-153">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="890c9-154">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="890c9-154">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="890c9-155">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="890c9-155">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

