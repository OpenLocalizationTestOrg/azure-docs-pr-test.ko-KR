---
title: "Stream Analytics 작업에 대한 출력 데이터를 구성하는 방법 | Microsoft Docs"
description: "Stream Analytics 작업에 대한 출력 구성 | 학습 경로 세그먼트."
keywords: "데이터 출력, 데이터 이동"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 3bbea3da-bfce-4af1-a15e-d4b23874034f
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/26/2017
ms.author: samacha
ms.openlocfilehash: 1ffa517469da1a8d79917b9747abc97ca3bef463
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-data-outputs-for-stream-analytics-jobs"></a><span data-ttu-id="a3c2d-104">Stream Analytics 작업에 대한 출력 데이터를 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="a3c2d-104">How to configure data outputs for Stream Analytics jobs</span></span>

<span data-ttu-id="a3c2d-105">Azure Stream Analytics 작업은 기존 데이터 링크에 대한 연결을 정의하는 하나 이상의 데이터 출력에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3c2d-105">Azure Stream Analytics jobs can be connected to one or more data outputs, which define a connection to an existing data sink.</span></span> <span data-ttu-id="a3c2d-106">Stream Analytics 작업이 들어오는 데이터를 처리 및 변환하면 데이터 출력 이벤트 스트림이 작업의 출력에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3c2d-106">As your Stream Analytics job processes and transforms incoming data, a stream of data output events is written to your job's output.</span></span>

<span data-ttu-id="a3c2d-107">Stream Analytics 데이터 출력을 사용하여 실시간 대시보드 또는 경고를 제공하거나, 데이터 이동 워크플로를 트리거하거나, 나중에 일괄 처리하기 위해 데이터를 보관할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3c2d-107">Stream Analytics data outputs can be used to source real-time dashboards or alerts, trigger data movement workflows, or simply archive data for batch processing later on.</span></span> <span data-ttu-id="a3c2d-108">Stream Analytics은 여기에 자세히 문서화되어 있는 여러 Azure 서비스와 높은 수준으로 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3c2d-108">Stream Analytics has first class integration with several Azure services, which are documented in detail here.</span></span>

<span data-ttu-id="a3c2d-109">Stream Analytics 작업에 출력을 추가하려면</span><span class="sxs-lookup"><span data-stu-id="a3c2d-109">To add an output to your Stream Analytics job:</span></span>

1. <span data-ttu-id="a3c2d-110">[Azure Portal](https://portal.azure.com)에서 작업을 열고 **출력**을 클릭한 다음, 표시되는 출력 블레이드에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3c2d-110">In the [Azure portal](https://portal.azure.com), open your job and click **Outputs** and then click **Add** in the Outputs blade that appears.</span></span>
   
    ![출력 추가](./media/stream-analytics-add-outputs/1-stream-analytics-add-outputs.png)  
   
2. <span data-ttu-id="a3c2d-112">**출력 별칭** 상자에 이 출력의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a3c2d-112">Provide a friendly name for this output in the **Output Alias** box.</span></span> <span data-ttu-id="a3c2d-113">이 이름은 나중에 작업 쿼리에서 출력을 참조하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3c2d-113">This name can be used in your job's query later on to refer to the output.</span></span>  
   
    <span data-ttu-id="a3c2d-114">출력에 연결하는 데 필요한 나머지 연결 속성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a3c2d-114">Fill in the rest of the required connection properties to connect to your output.</span></span>  <span data-ttu-id="a3c2d-115">이러한 필드는 출력 형식마다 다르며 여기서 자세히 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3c2d-115">These fields vary by output type and are defined in detail here.</span></span>  
   
    ![데이터 이동 서비스 선택](./media/stream-analytics-add-outputs/2-stream-analytics-add-outputs.png)  
   
3. <span data-ttu-id="a3c2d-117">출력 형식에 따라 데이터를 직렬화하거나 형식을 지정하는 방법을 지정해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3c2d-117">Depending on the output type, you may need to specify how the data is serialized or formatted.</span></span> <span data-ttu-id="a3c2d-118">각 출력 형식에 대한 특정 직렬화 설정은 여기에 문서화되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3c2d-118">The specific serialization settings for each output type are documented here.</span></span>
   
    <span data-ttu-id="a3c2d-119">데이터 원본에 연결하는 데 필요한 나머지 연결 속성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a3c2d-119">Fill in the rest of the required connection properties to connect to your data source.</span></span> <span data-ttu-id="a3c2d-120">이러한 필드는 입력 형식 및 원본 형식마다 다르며 [작업 만들기 문서](stream-analytics-create-a-job.md)에 자세히 정의되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3c2d-120">These fields vary by type of input and source type and are defined in detail in the [Create Job article](stream-analytics-create-a-job.md).</span></span>  

> [!Note]
>
> <span data-ttu-id="a3c2d-121">작업에 추가 된 모든 출력 요소는 작업이 시작 및 이벤트 전송이 시작되기 전에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3c2d-121">Any output element added to the job, must exist before the job is started and events start flowing.</span></span> <span data-ttu-id="a3c2d-122">예를 들어, 출력으로 Blob 저장소를 사용한 경우, 작업은 저장소 계정을 자동으로 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a3c2d-122">For example, if you use Blob storage as an output, the job will not create a storage account automatically.</span></span> <span data-ttu-id="a3c2d-123">ASA 작업이 시작되기 전에 사용자가 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3c2d-123">It needs to be created by the user before the ASA job is started.</span></span>
> 
 

## <a name="get-help"></a><span data-ttu-id="a3c2d-124">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="a3c2d-124">Get help</span></span>
<span data-ttu-id="a3c2d-125">추가 지원이 필요할 경우 [Azure 스트림 분석 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="a3c2d-125">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3c2d-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a3c2d-126">Next steps</span></span>
* [<span data-ttu-id="a3c2d-127">Azure Stream Analytics 소개</span><span class="sxs-lookup"><span data-stu-id="a3c2d-127">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="a3c2d-128">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="a3c2d-128">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="a3c2d-129">Azure  Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="a3c2d-129">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="a3c2d-130">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="a3c2d-130">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="a3c2d-131">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="a3c2d-131">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

