---
title: "Azure Data Lake Analytics 할당량 제한 | Microsoft Docs"
description: "ADLA(Azure Data Lake Analytics) 계정에서 할당량 한도를 조정하고 늘리는 방법을 알아봅니다."
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
ms.openlocfilehash: 957f306ea0e80b5830ad64e5ef06c6d122d9eccc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-data-lake-analytics-quota-limits"></a><span data-ttu-id="dfc12-104">Azure Data Lake Analytics 할당량 한도</span><span class="sxs-lookup"><span data-stu-id="dfc12-104">Azure Data Lake Analytics Quota Limits</span></span>

<span data-ttu-id="dfc12-105">ADLA(Azure Data Lake Analytics) 계정에서 할당량 한도를 조정하고 늘리는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="dfc12-105">Learn how to adjust and increase quota limits in Azure Data Lake Analytics (ADLA) accounts.</span></span> <span data-ttu-id="dfc12-106">이러한 한도를 알면 U-SQL 작업 동작을 이해하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfc12-106">Knowing these limits may help you understand your U-SQL job behavior.</span></span> <span data-ttu-id="dfc12-107">모든 할당량 한도는 소프트 한도이며, Microsoft에 문의하여 최대 한도를 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfc12-107">All quota limits are soft, so you can increase the maximum limits by reaching out to us.</span></span>

## <a name="azure-subscriptions-limits"></a><span data-ttu-id="dfc12-108">Azure 구독 한도</span><span class="sxs-lookup"><span data-stu-id="dfc12-108">Azure subscriptions limits</span></span>

<span data-ttu-id="dfc12-109">**구독당 최대 ADLA 계정 수:** 5.</span><span class="sxs-lookup"><span data-stu-id="dfc12-109">**Maximum number of ADLA accounts per subscription:**  5</span></span>

 <span data-ttu-id="dfc12-110">이는 구독당 만들 수 있는 ADLA 계정의 최대 개수입니다.</span><span class="sxs-lookup"><span data-stu-id="dfc12-110">This is the maximum number of ADLA accounts you can create per subscription.</span></span> <span data-ttu-id="dfc12-111">6번째 ADLA 계정을 만들려고 하면 "구독 이름에 따라 지역에서 허용되는 Data Lake Analytics 계정의 최대 수(5)에 도달했습니다." 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc12-111">If you try to create a sixth ADLA account, you will get an error "You have reached the maximum number of Data Lake Analytics accounts allowed (5) in region under subscription name".</span></span> <span data-ttu-id="dfc12-112">이 경우 사용하지 않는 모든 ADLA 계정을 삭제하거나 [지원 티켓을 열어](#increase-maximum-quota-limits) Microsoft에 문의합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc12-112">In this case, either delete any unused ADLA accounts, or reach out to us by [opening a support ticket](#increase-maximum-quota-limits).</span></span>

## <a name="adla-account-limits"></a><span data-ttu-id="dfc12-113">ADLA 계정 한도</span><span class="sxs-lookup"><span data-stu-id="dfc12-113">ADLA account limits</span></span>

<span data-ttu-id="dfc12-114">**계정당 최대 AU(분석 단위) 수:** 250.</span><span class="sxs-lookup"><span data-stu-id="dfc12-114">**Maximum number of Analytics Units (AUs) per account:** 250</span></span>

<span data-ttu-id="dfc12-115">이는 계정에서 동시에 실행할 수 있는 AU의 최대 개수입니다.</span><span class="sxs-lookup"><span data-stu-id="dfc12-115">This is the maximum number of AUs that can run concurrently in your account.</span></span> <span data-ttu-id="dfc12-116">모든 작업 간에 실행 중인 총 AU 수가 이 한도를 초과하면 최신 작업이 자동으로 큐에 대기됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfc12-116">If your total running AUs across all jobs exceeds this limit, newer jobs are queued automatically.</span></span> <span data-ttu-id="dfc12-117">예:</span><span class="sxs-lookup"><span data-stu-id="dfc12-117">For example:</span></span>

* <span data-ttu-id="dfc12-118">250AU로 실행되는 작업이 하나뿐인 경우 두 번째 작업을 제출하면 첫 번째 작업이 완료될 때까지 이 작업이 작업 큐에서 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc12-118">If you have only one job running with 250 AUs, when you submit a second job it will wait in the job queue until the first job completes.</span></span>
* <span data-ttu-id="dfc12-119">이미 5개의 작업이 실행 중이고 각각 50AU를 사용하는 경우 20AU가 필요한 6번째 작업을 제출하면 20AU가 사용 가능 상태가 될 때까지 작업 큐에서 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc12-119">If you already have five jobs running and each is using 50 AUs, when you submit a sixth job that needs 20 AUs it waits in the job queue until there are 20 AUs available.</span></span>

<span data-ttu-id="dfc12-120">**계정당 동시 U-SQL 작업의 최대 수:** 20.</span><span class="sxs-lookup"><span data-stu-id="dfc12-120">**Maximum number of concurrent U-SQL jobs per account:** 20</span></span>

<span data-ttu-id="dfc12-121">이는 계정에서 동시에 실행할 수 있는 작업의 최대 개수입니다.</span><span class="sxs-lookup"><span data-stu-id="dfc12-121">This is the maximum number of jobs that can run concurrently in your account.</span></span> <span data-ttu-id="dfc12-122">이 값을 초과하면 최신 작업이 자동으로 큐에 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc12-122">Above this value, newer jobs are queued automatically.</span></span>

## <a name="adjust-adla-quota-limits-per-account"></a><span data-ttu-id="dfc12-123">계정당 ADLA 할당량 한도 조정</span><span class="sxs-lookup"><span data-stu-id="dfc12-123">Adjust ADLA quota limits per account</span></span>

1. <span data-ttu-id="dfc12-124">[Azure Portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc12-124">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="dfc12-125">기존 ADLA 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc12-125">Choose an existing ADLA account.</span></span>
3. <span data-ttu-id="dfc12-126">**속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc12-126">Click **Properties**.</span></span>
4. <span data-ttu-id="dfc12-127">**병렬 처리** 및 **동시 작업**을 요구 사항에 맞게 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc12-127">Adjust **Parallelism** and **Concurrent Jobs** to suit your needs.</span></span>

    ![Azure 데이터 레이크 분석 포털 블레이드](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-properties.png)

## <a name="increase-maximum-quota-limits"></a><span data-ttu-id="dfc12-129">최대 할당량 한도 늘리기</span><span class="sxs-lookup"><span data-stu-id="dfc12-129">Increase maximum quota limits</span></span>

1. <span data-ttu-id="dfc12-130">Azure Portal에서 지원 요청을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dfc12-130">Open a support request in Azure Portal.</span></span>

    ![Azure 데이터 레이크 분석 포털 블레이드](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-help-support.png)

    ![Azure 데이터 레이크 분석 포털 블레이드](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request.png)
2. <span data-ttu-id="dfc12-133">문제 유형을 **할당량**으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc12-133">Select the issue type **Quota**.</span></span>
3. <span data-ttu-id="dfc12-134">**구독**을 선택합니다("평가판" 구독이 아닌지 확인).</span><span class="sxs-lookup"><span data-stu-id="dfc12-134">Select your **Subscription** (make sure it is not a "trial" subscription).</span></span>
4. <span data-ttu-id="dfc12-135">할당량 유형을 **Data Lake Analytics**로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc12-135">Select quota type **Data Lake Analytics**.</span></span>

    ![Azure 데이터 레이크 분석 포털 블레이드](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-basics.png)

5. <span data-ttu-id="dfc12-137">문제의 블레이드에서 요청한 증가 한도 및 이 추가 용량이 필요한 이유에 대한 **세부 정보**를 설명하세요.</span><span class="sxs-lookup"><span data-stu-id="dfc12-137">In the problem blade, explain your requested increase limit with **Details** of why you need this extra capacity.</span></span>

    ![Azure 데이터 레이크 분석 포털 블레이드](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-details.png)

6. <span data-ttu-id="dfc12-139">연락처 정보를 확인하고 지원 요청을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dfc12-139">Verify your contact information and create the support request.</span></span>

<span data-ttu-id="dfc12-140">Microsoft에서 요청을 검토하고 최대한 빨리 비즈니스 요구를 수용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc12-140">Microsoft reviews your request and tries to accommodate your business needs as soon as possible.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dfc12-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dfc12-141">Next steps</span></span>

* [<span data-ttu-id="dfc12-142">Microsoft Azure 데이터 레이크 분석 개요</span><span class="sxs-lookup"><span data-stu-id="dfc12-142">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="dfc12-143">Azure PowerShell을 사용하여 Azure Data Lake Analytics 관리</span><span class="sxs-lookup"><span data-stu-id="dfc12-143">Manage Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)
* [<span data-ttu-id="dfc12-144">Azure 포털을 사용하여 Azure Data Lake Analytics 작업 모니터링 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="dfc12-144">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
