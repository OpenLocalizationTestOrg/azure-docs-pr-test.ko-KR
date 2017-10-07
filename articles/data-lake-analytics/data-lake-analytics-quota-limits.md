---
title: "데이터 레이크 분석 할당량 한도 aaaAzure | Microsoft Docs"
description: "Azure 데이터 레이크 분석 (ADLA) 계정에 tooadjust 및 증가 할당량 제한 하는 방법에 대해 알아봅니다."
services: data-lake-analytics
keywords: "Azure 데이터 레이크 분석"
documentationcenter: 
author: omidm1
editor: omidm1
ms.assetid: 49416f38-fcc7-476f-a55e-d67f3f9c1d34
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: omidm
ms.openlocfilehash: 875c4d00e0c57414031e50754495c02162bdca48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-lake-analytics-quota-limits"></a><span data-ttu-id="4691f-104">Azure Data Lake Analytics 할당량 한도</span><span class="sxs-lookup"><span data-stu-id="4691f-104">Azure Data Lake Analytics Quota Limits</span></span>

<span data-ttu-id="4691f-105">Azure 데이터 레이크 분석 (ADLA) 계정에 tooadjust 및 증가 할당량 제한 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4691f-105">Learn how tooadjust and increase quota limits in Azure Data Lake Analytics (ADLA) accounts.</span></span> <span data-ttu-id="4691f-106">이러한 한도를 알면 U-SQL 작업 동작을 이해하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4691f-106">Knowing these limits may help you understand your U-SQL job behavior.</span></span> <span data-ttu-id="4691f-107">모든 할당량 한도 소프트, 되므로 toous 접근할 여 hello 최대 한도 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4691f-107">All quota limits are soft, so you can increase hello maximum limits by reaching out toous.</span></span>

## <a name="azure-subscriptions-limits"></a><span data-ttu-id="4691f-108">Azure 구독 한도</span><span class="sxs-lookup"><span data-stu-id="4691f-108">Azure subscriptions limits</span></span>

<span data-ttu-id="4691f-109">**구독당 최대 ADLA 계정 수:** 5.</span><span class="sxs-lookup"><span data-stu-id="4691f-109">**Maximum number of ADLA accounts per subscription:**  5</span></span>

 <span data-ttu-id="4691f-110">구독 당 만들 수 있습니다 ADLA 계정의 hello 최대 수입니다.</span><span class="sxs-lookup"><span data-stu-id="4691f-110">This is hello maximum number of ADLA accounts you can create per subscription.</span></span> <span data-ttu-id="4691f-111">6 번째 toocreate ADLA 계정 시도 하면 "에 도달 했습니다 hello 최대 수가 허용 된 Data Lake 분석 계정 (5) 영역 구독 이름 아래 에" 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="4691f-111">If you try toocreate a sixth ADLA account, you will get an error "You have reached hello maximum number of Data Lake Analytics accounts allowed (5) in region under subscription name".</span></span> <span data-ttu-id="4691f-112">이 경우 삭제는 사용 하지 않는 ADLA 계정을 하거나 연락 하 여 toous [지원 티켓을 열어](#increase-maximum-quota-limits)합니다.</span><span class="sxs-lookup"><span data-stu-id="4691f-112">In this case, either delete any unused ADLA accounts, or reach out toous by [opening a support ticket](#increase-maximum-quota-limits).</span></span>

## <a name="adla-account-limits"></a><span data-ttu-id="4691f-113">ADLA 계정 한도</span><span class="sxs-lookup"><span data-stu-id="4691f-113">ADLA account limits</span></span>

<span data-ttu-id="4691f-114">**계정당 최대 AU(분석 단위) 수:** 250.</span><span class="sxs-lookup"><span data-stu-id="4691f-114">**Maximum number of Analytics Units (AUs) per account:** 250</span></span>

<span data-ttu-id="4691f-115">이것이 hello AUs 계정에서 동시에 실행할 수 있는 최대 수입니다.</span><span class="sxs-lookup"><span data-stu-id="4691f-115">This is hello maximum number of AUs that can run concurrently in your account.</span></span> <span data-ttu-id="4691f-116">모든 작업 간에 실행 중인 총 AU 수가 이 한도를 초과하면 최신 작업이 자동으로 큐에 대기됩니다.</span><span class="sxs-lookup"><span data-stu-id="4691f-116">If your total running AUs across all jobs exceeds this limit, newer jobs are queued automatically.</span></span> <span data-ttu-id="4691f-117">예:</span><span class="sxs-lookup"><span data-stu-id="4691f-117">For example:</span></span>

* <span data-ttu-id="4691f-118">하나의 작업이 있는 경우 250으로 AUs, 두 번째 제출할 때 작업을 실행할 것 hello 첫 번째 작업이 완료 될 때까지 hello 작업 큐에서 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="4691f-118">If you have only one job running with 250 AUs, when you submit a second job it will wait in hello job queue until hello first job completes.</span></span>
* <span data-ttu-id="4691f-119">이미 5 개의 작업이 실행 되 고 50 각각 사용 하는 경우 AUs, 20을 필요로 하는 여섯 번째 작업을 제출 하면 AUs 20 없을 때까지 hello 작업 큐에서 대기 AUs 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4691f-119">If you already have five jobs running and each is using 50 AUs, when you submit a sixth job that needs 20 AUs it waits in hello job queue until there are 20 AUs available.</span></span>

<span data-ttu-id="4691f-120">**계정당 동시 U-SQL 작업의 최대 수:** 20.</span><span class="sxs-lookup"><span data-stu-id="4691f-120">**Maximum number of concurrent U-SQL jobs per account:** 20</span></span>

<span data-ttu-id="4691f-121">Hello 계정에서 동시에 실행할 수 있는 작업의 최대 수입니다.</span><span class="sxs-lookup"><span data-stu-id="4691f-121">This is hello maximum number of jobs that can run concurrently in your account.</span></span> <span data-ttu-id="4691f-122">이 값을 초과하면 최신 작업이 자동으로 큐에 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="4691f-122">Above this value, newer jobs are queued automatically.</span></span>

## <a name="adjust-adla-quota-limits-per-account"></a><span data-ttu-id="4691f-123">계정당 ADLA 할당량 한도 조정</span><span class="sxs-lookup"><span data-stu-id="4691f-123">Adjust ADLA quota limits per account</span></span>

1. <span data-ttu-id="4691f-124">Toohello 로그온 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="4691f-124">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4691f-125">기존 ADLA 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4691f-125">Choose an existing ADLA account.</span></span>
3. <span data-ttu-id="4691f-126">**속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4691f-126">Click **Properties**.</span></span>
4. <span data-ttu-id="4691f-127">조정 **병렬 처리 수준** 및 **동시 작업** toosuit 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4691f-127">Adjust **Parallelism** and **Concurrent Jobs** toosuit your needs.</span></span>

    ![Azure 데이터 레이크 분석 포털 블레이드](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-properties.png)

## <a name="increase-maximum-quota-limits"></a><span data-ttu-id="4691f-129">최대 할당량 한도 늘리기</span><span class="sxs-lookup"><span data-stu-id="4691f-129">Increase maximum quota limits</span></span>

1. <span data-ttu-id="4691f-130">Azure Portal에서 지원 요청을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4691f-130">Open a support request in Azure Portal.</span></span>

    ![Azure 데이터 레이크 분석 포털 블레이드](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-help-support.png)

    ![Azure 데이터 레이크 분석 포털 블레이드](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request.png)
2. <span data-ttu-id="4691f-133">Hello 문제 유형을 선택 **할당량**합니다.</span><span class="sxs-lookup"><span data-stu-id="4691f-133">Select hello issue type **Quota**.</span></span>
3. <span data-ttu-id="4691f-134">**구독**을 선택합니다("평가판" 구독이 아닌지 확인).</span><span class="sxs-lookup"><span data-stu-id="4691f-134">Select your **Subscription** (make sure it is not a "trial" subscription).</span></span>
4. <span data-ttu-id="4691f-135">할당량 유형을 **Data Lake Analytics**로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4691f-135">Select quota type **Data Lake Analytics**.</span></span>

    ![Azure 데이터 레이크 분석 포털 블레이드](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-basics.png)

5. <span data-ttu-id="4691f-137">Hello 문제 블레이드를 포함 하 여 요청 된 증가 제한을 설명 **세부 정보** 이 추가 용량이 필요한 이유입니다.</span><span class="sxs-lookup"><span data-stu-id="4691f-137">In hello problem blade, explain your requested increase limit with **Details** of why you need this extra capacity.</span></span>

    ![Azure 데이터 레이크 분석 포털 블레이드](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-details.png)

6. <span data-ttu-id="4691f-139">귀하의 연락처 정보를 확인 하 고 hello 지원 요청을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4691f-139">Verify your contact information and create hello support request.</span></span>

<span data-ttu-id="4691f-140">Microsoft에서 요청을 검토 하 고 비즈니스 수요가 최대한 빨리 tooaccommodate 하려고 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="4691f-140">Microsoft reviews your request and tries tooaccommodate your business needs as soon as possible.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4691f-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4691f-141">Next steps</span></span>

* [<span data-ttu-id="4691f-142">Microsoft Azure 데이터 레이크 분석 개요</span><span class="sxs-lookup"><span data-stu-id="4691f-142">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="4691f-143">Azure PowerShell을 사용하여 Azure Data Lake Analytics 관리</span><span class="sxs-lookup"><span data-stu-id="4691f-143">Manage Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)
* [<span data-ttu-id="4691f-144">Azure 포털을 사용하여 Azure Data Lake Analytics 작업 모니터링 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="4691f-144">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
