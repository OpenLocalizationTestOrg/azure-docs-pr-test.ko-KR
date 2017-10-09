---
title: "스트림 분석에 대 한 데이터 분석 처리 작업이 aaaHow toocreate | Microsoft Docs"
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
ms.openlocfilehash: d4a3c89d8862d59688d06a1719b063efa2ab1c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-data-analytics-processing-job-for-stream-analytics"></a><span data-ttu-id="02598-104">어떻게 toocreate 데이터 분석 처리는 스트림 분석에 대 한을 작업합니다</span><span class="sxs-lookup"><span data-stu-id="02598-104">How toocreate a data analytics processing job for Stream Analytics</span></span>
<span data-ttu-id="02598-105">Azure 스트림 분석에서 hello 최상위 리소스는 스트림 분석 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="02598-105">hello top-level resource in Azure Stream Analytics is a Stream Analytics Job.</span></span>  <span data-ttu-id="02598-106">하나 이루어져 하거나 더 많은 데이터 원본과 데이터 변환 hello를 표현 하는 쿼리 결과에 기록 되며 하나 이상의 출력 대상을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="02598-106">It consists of one or more input data sources, a query expressing hello data transformation, and one or more output targets that results are written to.</span></span> <span data-ttu-id="02598-107">스트리밍 데이터에 대 한 시나리오를 처리 하는 hello 사용자 tooperform 데이터 분석을 통해 이러한 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02598-107">Together these enable hello user tooperform data analytics processing for streaming data scenarios.</span></span>

<span data-ttu-id="02598-108">스트림 분석을 사용 하 여 toostart 먼저 새 스트림 분석 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="02598-108">toostart using Stream Analytics, begin by creating a new Stream Analytics job.</span></span>  <span data-ttu-id="02598-109">Note hello 작업이 시작 될 때까지이 작업에 요금이 청구 될 없습니다.</span><span class="sxs-lookup"><span data-stu-id="02598-109">Note this action has no billing implications until hello job is started.</span></span>

1. <span data-ttu-id="02598-110">온라인 hello에 로그인 [Azure 클래식 포털](http://manage.windowsazure.com) 또는 hello [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="02598-110">Sign in on hello online [Azure classic portal](http://manage.windowsazure.com) or hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="02598-111">Hello 포털에서: **새 클릭**, 클릭 **데이터 서비스** 또는 **데이터 분석** 포털을 클릭 한 다음에 따라 **Azure스트림분석** 또는 **Stream Analytics** 차례로 **빨리 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="02598-111">In hello portal: **Click New**, then click **Data Services** or **Data Analytics** depending on your portal and then click **Azure Stream Analytics** or **Stream Analytics** and then **Quick Create**.</span></span>
   
   ![데이터 분석 처리 작업 마법사](./media/stream-analytics-create-a-job/1-stream-analytics-create-a-job.png)  
   
   ![데이터 분석 처리 작업 만들기](./media/stream-analytics-create-a-job/4-stream-analytics-create-a-job.png)  
3. <span data-ttu-id="02598-114">Hello 스트림 분석 작업에 대 한 hello 원하는 구성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="02598-114">Specify hello desired configuration for hello Stream Analytics job.</span></span>
   
   * <span data-ttu-id="02598-115">Hello에 **작업 이름을** 상자에 이름 tooidentify hello 스트림 분석 작업을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="02598-115">In hello **Job Name** box, enter a name tooidentify hello Stream Analytics job.</span></span> <span data-ttu-id="02598-116">Hello 때 **작업 이름을** 의 유효성이 확인 되 hello 작업 이름 상자에 녹색 확인 표시가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="02598-116">When hello **Job Name** is validated, a green check mark appears in hello Job Name box.</span></span> <span data-ttu-id="02598-117">hello **작업 이름을** 영숫자 문자와 hello 포함 될 수 있습니다 '-' 문자, 있으며 3 ~ 63 자 사이 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02598-117">hello **Job Name** may contain only alphanumeric characters and hello '-' character, and must be between 3 and 63 characters.</span></span>
   * <span data-ttu-id="02598-118">사용 하 여 **지역** hello Azure 포털에서에서 또는 **위치** hello Azure에서에서 포털 toospecify hello toorun hello 작업 저장할 지리적 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="02598-118">Use **Region** in hello Azure portal or **Location** in hello Azure portal toospecify hello geographic location where you want toorun hello job.</span></span>
   * <span data-ttu-id="02598-119">Azure 포털을 hello를 사용 하 여, 선택 하거나 hello로 저장소 계정 toouse 만들 **지역별 모니터링 저장소 계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="02598-119">If using hello Azure portal, select or create a storage account toouse as hello **Regional Monitoring Storage Account**.</span></span> <span data-ttu-id="02598-120">이 저장소 계정은이 영역에서 실행 중인 모든 스트림 분석 작업에 대 한 데이터를 모니터링 하는 사용 되는 toostore입니다.</span><span class="sxs-lookup"><span data-stu-id="02598-120">This storage account is used toostore monitoring data for all Stream Analytics jobs running in this region.</span></span>
   * <span data-ttu-id="02598-121">Azure 포털을 hello를 사용 하 여, 지정 새 또는 기존 **리소스 그룹** toohold 관련 응용 프로그램에 대 한 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="02598-121">If using hello Azure portal, specify a new or existing **Resource Group** toohold related resources for your application.</span></span>
4. <span data-ttu-id="02598-122">새 스트림 분석 작업 옵션 hello 구성 되 면 클릭 **스트림 분석 작업 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="02598-122">Once hello new Stream Analytics job options are configured, click **Create Stream Analytics Job**.</span></span> <span data-ttu-id="02598-123">만든 hello 스트림 분석 작업 toobe 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02598-123">It can take a few minutes for hello Stream Analytics job toobe created.</span></span> <span data-ttu-id="02598-124">toocheck hello 상태 hello 알림 허브에서 hello 진행률을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02598-124">toocheck hello status, you can monitor hello progress in hello Notifications hub.</span></span>
   
   ![데이터 분석 처리 작업 알림 허브](./media/stream-analytics-create-a-job/2-stream-analytics-create-a-job.png)  
   
   ![Azure Portal 데이터 분석 처리 작업 만들기](./media/stream-analytics-create-a-job/5-stream-analytics-create-a-job.png)  
5. <span data-ttu-id="02598-127">hello 새 작업의 상태가 표시 됩니다 **Created**합니다.</span><span class="sxs-lookup"><span data-stu-id="02598-127">hello new job will show a status of **Created**.</span></span> <span data-ttu-id="02598-128">해당 hello 확인 **시작** 단추가 비활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02598-128">Notice that hello **Start** button is disabled.</span></span> <span data-ttu-id="02598-129">Hello 작업을 시작 하기 전에 hello 작업 입력, 쿼리 및 출력을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="02598-129">Configure hello job input, query, and output before you start hello job.</span></span>
   
   ![데이터 분석 처리 작업 상태](./media/stream-analytics-create-a-job/3-stream-analytics-create-a-job.png)  
   
   ![Azure Portal 데이터 분석 처리 작업 상태](./media/stream-analytics-create-a-job/6-stream-analytics-create-a-job.png)  

## <a name="get-help"></a><span data-ttu-id="02598-132">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="02598-132">Get help</span></span>
<span data-ttu-id="02598-133">추가 지원이 필요할 경우 [Azure 스트림 분석 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="02598-133">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="02598-134">다음 단계</span><span class="sxs-lookup"><span data-stu-id="02598-134">Next steps</span></span>
* [<span data-ttu-id="02598-135">스트림 분석 소개 tooAzure</span><span class="sxs-lookup"><span data-stu-id="02598-135">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="02598-136">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="02598-136">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="02598-137">Azure  Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="02598-137">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="02598-138">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="02598-138">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="02598-139">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="02598-139">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

