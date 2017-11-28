---
title: "aaaAdd 데이터 입력 tooyour 스트림 분석 작업 | Microsoft Docs"
description: "데이터 원본 tooyour 스트림 분석을 toohook 블로그 저장소에서 이벤트 허브 또는 참조 데이터에서 데이터 입력으로 스트리밍 작업 하는 방법을 알아봅니다."
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
ms.openlocfilehash: 674000268fcdf9bc000af3e2f166cb66f1366922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-streaming-data-input-or-reference-data-tooa-stream-analytics-job"></a><span data-ttu-id="7af84-104">스트리밍 데이터 입력, 참조 데이터 tooa 스트림 분석 작업을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7af84-104">Add a streaming data input or reference data tooa Stream Analytics job</span></span>
<span data-ttu-id="7af84-105">데이터 소스 tooyour 스트림 분석을 toohook 이벤트 허브 또는 참조 데이터 Blob 저장소에서 데이터 입력으로 스트리밍 작업 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7af84-105">Learn how toohook up a data source tooyour Stream Analytics job as streaming data input from Event Hubs or reference data from Blob storage.</span></span>

<span data-ttu-id="7af84-106">Azure 스트림 분석 작업 이상이 될 수 있으며 연결된 tooone 데이터 입력을 각각 연결 tooan 기존 데이터 원본을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7af84-106">Azure Stream Analytics jobs can be connected tooone data input or more, each of which define a connection tooan existing data source.</span></span> <span data-ttu-id="7af84-107">데이터는 전송 toothat 데이터 원본으로 hello 스트림 분석 작업에서 사용 되며 실시간으로 데이터를 스트리밍로 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="7af84-107">As data is sent toothat data source, it is consumed by hello Stream Analytics job and processed in real time as streaming data.</span></span> <span data-ttu-id="7af84-108">스트림 분석의 첫 번째 클래스 통합으로 [Azure 이벤트 허브](https://azure.microsoft.com/services/event-hubs/) 및 [Azure Blob 저장소](../storage/blobs/storage-dotnet-how-to-use-blobs.md) 내부와 외부 hello 작업의 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="7af84-108">Stream Analytics has first class integration with [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) and [Azure Blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md) both within and outside of hello job's subscription.</span></span>

<span data-ttu-id="7af84-109">이 문서는 hello 단계의 [스트림 분석 학습 경로](/documentation/learning-paths/stream-analytics/)합니다.</span><span class="sxs-lookup"><span data-stu-id="7af84-109">This article is a step in hello [Stream Analytics learning path](/documentation/learning-paths/stream-analytics/).</span></span>

## <a name="data-input-streaming-data-and-reference-data"></a><span data-ttu-id="7af84-110">데이터 입력: 스트리밍 데이터 및 참조 데이터</span><span class="sxs-lookup"><span data-stu-id="7af84-110">Data input: Streaming data and reference data</span></span>
<span data-ttu-id="7af84-111">Stream Analytics에는 데이터 스트림 및 참조 데이터 이렇게 두 가지 입력 형식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7af84-111">There are two distinct types of inputs in Stream Analytics: data streams and reference data.</span></span>

* <span data-ttu-id="7af84-112">**데이터 스트림을**: 스트림 분석 작업에는 하나 이상의 데이터 스트림 입력된 toobe 사용 하 고 hello 작업에 의해 변환할 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7af84-112">**Data Streams**: Stream Analytics jobs must include at least one data stream input toobe consumed and transformed by hello job.</span></span> <span data-ttu-id="7af84-113">Azure Blob 저장소 및 Azure 이벤트 허브는 데이터 스트림 입력 소스로 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="7af84-113">Azure Blob storage and Azure Event Hubs are supported as data stream input sources.</span></span> <span data-ttu-id="7af84-114">Azure 이벤트 허브는 연결 된 장치, 서비스 및 응용 프로그램에서 사용 되는 toocollect 이벤트 스트림을 합니다.</span><span class="sxs-lookup"><span data-stu-id="7af84-114">Azure Event Hubs are used toocollect event streams from connected devices, services and applications.</span></span> <span data-ttu-id="7af84-115">Azure Blob 저장소를 스트림으로 대량 데이터 수집을 위한 입력 소스로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7af84-115">Azure Blob storage can be used as an input source for ingesting bulk data as a stream.</span></span>  
* <span data-ttu-id="7af84-116">**참조 데이터**: Stream Analytics은 참조 데이터라는 두 번째 형식의 보조 입력을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7af84-116">**Reference data**: Stream Analytics supports a second type of auxiliary input called reference data.</span></span>  <span data-ttu-id="7af84-117">유동적인 것과 반대로 toodata로이 데이터는 정적 이거나 느리게 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="7af84-117">As opposed toodata in motion, this data is static or slowing changing.</span></span>  <span data-ttu-id="7af84-118">일반적으로 조회 및 상관 관계 데이터 스트림 toocreate 더욱 다양 한 데이터를 수행 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7af84-118">It is typically used for performing look-ups and correlations with data streams toocreate a richer data set.</span></span>  <span data-ttu-id="7af84-119">Azure Blob 저장소는 현재 참조 데이터에 대 한 입력된 소스 hello만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7af84-119">Azure Blob storage is currently hello only supported input source for reference data.</span></span>  

<span data-ttu-id="7af84-120">tooadd 입력된 tooyour 스트림 분석 작업:</span><span class="sxs-lookup"><span data-stu-id="7af84-120">tooadd an input tooyour Stream Analytics job:</span></span>

1. <span data-ttu-id="7af84-121">Hello Azure 포털에서에서 클릭 **입력** 클릭 하 고 **입력 추가** Stream Analytics 작업에서.</span><span class="sxs-lookup"><span data-stu-id="7af84-121">In hello Azure portal click **Inputs** and then click **Add an Input** in your Stream Analytics job.</span></span>
   
    ![Azure 클래식 포털 - 입력을 추가합니다.](./media/stream-analytics-add-inputs/1-stream-analytics-add-inputs.png)  
   
    <span data-ttu-id="7af84-123">Hello Azure 포털에서 hello **입력** Stream Analytics 작업에서 타일입니다.</span><span class="sxs-lookup"><span data-stu-id="7af84-123">In hello Azure portal click hello **Inputs** tile in your Stream Analytics job.</span></span>  
   
    ![Azure 포털 - 데이터 입력을 추가합니다.](./media/stream-analytics-add-inputs/7-stream-analytics-add-inputs.png)  
2. <span data-ttu-id="7af84-125">Hello 입력의 hello 유형을 지정: 어느 **데이터 스트림을** 또는 **참조 데이터**합니다.</span><span class="sxs-lookup"><span data-stu-id="7af84-125">Specify hello type of hello input: either **Data stream** or **Reference data**.</span></span>
   
    ![Hello 올바른 데이터 입력, 스트리밍 또는 참조를 추가 합니다.](./media/stream-analytics-add-inputs/2-stream-analytics-add-inputs.png)  
   
    ![Hello 올바른 데이터 입력, 스트리밍 또는 참조를 추가 합니다.](./media/stream-analytics-add-inputs/8-stream-analytics-add-inputs.png)  
3. <span data-ttu-id="7af84-128">데이터 스트림 입력을 만드는 경우에 hello 입력에 대 한 hello 소스 유형을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7af84-128">If creating a Data Stream input, specify hello source type for hello input.</span></span>  <span data-ttu-id="7af84-129">이때는 Blob 저장소만 지원되므로 참조 데이터를 만드는 동안에는 이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7af84-129">This step can be skipped during Reference Data creation as only Blob storage is supported at this time.</span></span>
   
    ![데이터 스트림 데이터 입력 추가](./media/stream-analytics-add-inputs/3-stream-analytics-add-inputs.png)  
   
    ![데이터 스트림 데이터 입력 추가](./media/stream-analytics-add-inputs/9-stream-analytics-add-inputs.png)  
4. <span data-ttu-id="7af84-132">이 입력된에 hello 입력 별칭 상자에 대 한 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7af84-132">Provide a friendly name for this input in hello Input Alias box.</span></span>  <span data-ttu-id="7af84-133">이 이름은 작업의 쿼리 toorefer toohello 입력에 나중에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7af84-133">This name will be used in your job's query later on toorefer toohello input.</span></span>
   
    <span data-ttu-id="7af84-134">Hello 필요한 연결 속성 tooconnect tooyour 데이터 원본 hello 나머지를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7af84-134">Fill in hello rest of hello required connection properties tooconnect tooyour data source.</span></span> <span data-ttu-id="7af84-135">이러한 필드는 입력 형식 및 소스 형식마다 다르며 [여기](stream-analytics-create-a-job.md)에 자세히 정의되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7af84-135">These fields vary by type of input and source type and are defined in detail [here](stream-analytics-create-a-job.md).</span></span>  
   
    ![이벤트 허브 데이터 입력 추가](./media/stream-analytics-add-inputs/4-stream-analytics-add-inputs.png)  
5. <span data-ttu-id="7af84-137">Hello 입력된 데이터에 대 한 hello serialization 설정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7af84-137">Specify hello serialization settings for hello input data:</span></span>
   
   * <span data-ttu-id="7af84-138">쿼리를 원하는, hello 방식으로 작동 toomake 지정 hello **이벤트 직렬화 형식** 들어오는 데이터의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7af84-138">toomake sure your queries work hello way you expect, specify hello **Event Serialization Format** of incoming data.</span></span>  <span data-ttu-id="7af84-139">지원되는 직렬화 형식은 JSON, CSV 및 Avro입니다.</span><span class="sxs-lookup"><span data-stu-id="7af84-139">Supported serialization formats are JSON, CSV, and Avro.</span></span>
   * <span data-ttu-id="7af84-140">Hello 확인 **인코딩** hello 데이터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="7af84-140">Verify hello **Encoding** for hello data.</span></span>  <span data-ttu-id="7af84-141">U t F-8 hello만 현재 지원 인코딩 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="7af84-141">UTF-8 is hello only supported encoding format at this time.</span></span>
     
     ![Hello 데이터 입력에 대 한 데이터 serialization 설정](./media/stream-analytics-add-inputs/5-stream-analytics-add-inputs.png)  
     
     ![Hello 데이터 입력에 대 한 데이터 serialization 설정](./media/stream-analytics-add-inputs/10-stream-analytics-add-inputs.png)  
6. <span data-ttu-id="7af84-144">Hello 입력된 만들기를 완료 한 후 Stream Analytics는 toohello 입력된 소스를 연결할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7af84-144">After completing hello input creation, Stream Analytics will verify that it can connect toohello input source.</span></span>  <span data-ttu-id="7af84-145">Hello 알림 허브의 hello 연결 테스트 작업의 hello 상태를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7af84-145">You can view hello status of hello Test Connection operation in hello Notification hub.</span></span>
   
    ![데이터 입력 스트리밍 hello 연결 테스트](./media/stream-analytics-add-inputs/6-stream-analytics-add-inputs.png)  
   
    ![데이터 입력 스트리밍 hello 연결 테스트](./media/stream-analytics-add-inputs/11-stream-analytics-add-inputs.png)  

## <a name="get-help-with-streaming-data-inputs"></a><span data-ttu-id="7af84-148">스트리밍 데이터 입력에 대한 도움 받기</span><span class="sxs-lookup"><span data-stu-id="7af84-148">Get help with streaming data inputs</span></span>
<span data-ttu-id="7af84-149">추가 지원이 필요할 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="7af84-149">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="7af84-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7af84-150">Next steps</span></span>
* [<span data-ttu-id="7af84-151">스트림 분석 소개 tooAzure</span><span class="sxs-lookup"><span data-stu-id="7af84-151">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="7af84-152">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="7af84-152">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="7af84-153">Azure  Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="7af84-153">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="7af84-154">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="7af84-154">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="7af84-155">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="7af84-155">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

