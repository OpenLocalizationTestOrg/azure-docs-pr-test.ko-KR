---
title: "Stream Analytics을 위한 데이터 분석 처리 작업을 만드는 방법 | Microsoft Docs"
description: "Stream Analytics을 위한 데이터 분석 처리 작업 만들기 | 학습 경로 세그먼트."
keywords: "데이터 분석 처리"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: e825fbcf-69e9-443f-b402-3b7a4568f415
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 05fdf1e20efd129cdfc27e1d37bc9e124edf5dcd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-create-a-data-analytics-processing-job-for-stream-analytics"></a><span data-ttu-id="4ffb3-104">Stream Analytics을 위한 데이터 분석 처리 작업을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="4ffb3-104">How to create a data analytics processing job for Stream Analytics</span></span>
<span data-ttu-id="4ffb3-105">Azure Stream Analytics에서 최상위 리소스는 Stream Analytics 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="4ffb3-105">The top-level resource in Azure Stream Analytics is a Stream Analytics Job.</span></span>  <span data-ttu-id="4ffb3-106">하나 이상의 입력 데이터 원본, 데이터 변환을 표현하는 쿼리 및 결과가 기록되는 하나 이상의 출력 대상으로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ffb3-106">It consists of one or more input data sources, a query expressing the data transformation, and one or more output targets that results are written to.</span></span> <span data-ttu-id="4ffb3-107">이러한 요소가 모여서 데이터 시나리오 스트리밍을 위한 데이터 분석 처리 작업을 수행할 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="4ffb3-107">Together these enable the user to perform data analytics processing for streaming data scenarios.</span></span>

<span data-ttu-id="4ffb3-108">Stream Analytics 사용을 시작하려면 먼저 새 Stream Analytics 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4ffb3-108">To start using Stream Analytics, begin by creating a new Stream Analytics job.</span></span>  <span data-ttu-id="4ffb3-109">이 작업에 대한 비용은 작업이 시작될 때까지 청구되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4ffb3-109">Note this action has no billing implications until the job is started.</span></span>

1. <span data-ttu-id="4ffb3-110">[Azure 클래식 포털](http://manage.windowsazure.com) 또는 [Azure Portal](https://portal.azure.com/)에서 온라인으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4ffb3-110">Sign in on the online [Azure classic portal](http://manage.windowsazure.com) or the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="4ffb3-111">포털에서: **새로 만들기를 클릭**한 다음 사용자의 포털에 따라 **Data Services** 또는 **데이터 분석**을 클릭한 다음 **Azure Stream Analytics** 또는 **Stream Analytics**, **빨리 만들기**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4ffb3-111">In the portal: **Click New**, then click **Data Services** or **Data Analytics** depending on your portal and then click **Azure Stream Analytics** or **Stream Analytics** and then **Quick Create**.</span></span>
   
   ![데이터 분석 처리 작업 마법사](./media/stream-analytics-create-a-job/1-stream-analytics-create-a-job.png)  
   
   ![데이터 분석 처리 작업 만들기](./media/stream-analytics-create-a-job/4-stream-analytics-create-a-job.png)  
3. <span data-ttu-id="4ffb3-114">Stream Analytics 작업에 대한 원하는 구성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4ffb3-114">Specify the desired configuration for the Stream Analytics job.</span></span>
   
   * <span data-ttu-id="4ffb3-115">**작업 이름** 상자에 Stream Analytics 작업을 식별하는 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4ffb3-115">In the **Job Name** box, enter a name to identify the Stream Analytics job.</span></span> <span data-ttu-id="4ffb3-116">**작업 이름** 의 유효성이 검사되면 작업 이름 상자에 녹색 확인 표시가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="4ffb3-116">When the **Job Name** is validated, a green check mark appears in the Job Name box.</span></span> <span data-ttu-id="4ffb3-117">**작업 이름** 에는 영숫자 문자와 '-' 문자만 포함될 수 있으며, 3자에서 63자 사이여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ffb3-117">The **Job Name** may contain only alphanumeric characters and the '-' character, and must be between 3 and 63 characters.</span></span>
   * <span data-ttu-id="4ffb3-118">Azure Portal에서 **지역** 또는 Azure 포털에서 **위치**를 사용하여 작업을 실행하려는 지리적 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4ffb3-118">Use **Region** in the Azure portal or **Location** in the Azure portal to specify the geographic location where you want to run the job.</span></span>
   * <span data-ttu-id="4ffb3-119">Azure 포털을 사용하는 경우 **지역별 모니터링 저장소 계정**으로 사용하려는 저장소 계정을 선택하거나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4ffb3-119">If using the Azure portal, select or create a storage account to use as the **Regional Monitoring Storage Account**.</span></span> <span data-ttu-id="4ffb3-120">이 저장소 계정은 이 지역에서 실행 중인 모든 Stream Analytics 작업에 대한 모니터링 데이터를 저장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ffb3-120">This storage account is used to store monitoring data for all Stream Analytics jobs running in this region.</span></span>
   * <span data-ttu-id="4ffb3-121">Azure 포털을 사용하는 경우, 응용 프로그램에 대한 관련된 리소스를 저장하는 신규 및 기존 **리소스 그룹** 을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ffb3-121">If using the Azure portal, specify a new or existing **Resource Group** to hold related resources for your application.</span></span>
4. <span data-ttu-id="4ffb3-122">새 Stream Analytics 작업 옵션이 구성되면 **Stream Analytics 작업 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4ffb3-122">Once the new Stream Analytics job options are configured, click **Create Stream Analytics Job**.</span></span> <span data-ttu-id="4ffb3-123">Stream Analytics 작업을 만드는 데 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ffb3-123">It can take a few minutes for the Stream Analytics job to be created.</span></span> <span data-ttu-id="4ffb3-124">상태를 확인하려면 알림 허브에서 진행률을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ffb3-124">To check the status, you can monitor the progress in the Notifications hub.</span></span>
   
   ![데이터 분석 처리 작업 알림 허브](./media/stream-analytics-create-a-job/2-stream-analytics-create-a-job.png)  
   
   ![Azure Portal 데이터 분석 처리 작업 만들기](./media/stream-analytics-create-a-job/5-stream-analytics-create-a-job.png)  
5. <span data-ttu-id="4ffb3-127">새 작업이 **생성됨** 상태로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ffb3-127">The new job will show a status of **Created**.</span></span> <span data-ttu-id="4ffb3-128">**시작** 단추를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4ffb3-128">Notice that the **Start** button is disabled.</span></span> <span data-ttu-id="4ffb3-129">작업을 시작하기 전에 작업 입력, 쿼리 및 출력을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="4ffb3-129">Configure the job input, query, and output before you start the job.</span></span>
   
   ![데이터 분석 처리 작업 상태](./media/stream-analytics-create-a-job/3-stream-analytics-create-a-job.png)  
   
   ![Azure Portal 데이터 분석 처리 작업 상태](./media/stream-analytics-create-a-job/6-stream-analytics-create-a-job.png)  

## <a name="get-help"></a><span data-ttu-id="4ffb3-132">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="4ffb3-132">Get help</span></span>
<span data-ttu-id="4ffb3-133">추가 지원이 필요할 경우 [Azure 스트림 분석 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="4ffb3-133">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ffb3-134">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4ffb3-134">Next steps</span></span>
* [<span data-ttu-id="4ffb3-135">Azure Stream Analytics 소개</span><span class="sxs-lookup"><span data-stu-id="4ffb3-135">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="4ffb3-136">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="4ffb3-136">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="4ffb3-137">Azure  Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="4ffb3-137">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="4ffb3-138">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="4ffb3-138">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="4ffb3-139">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="4ffb3-139">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

