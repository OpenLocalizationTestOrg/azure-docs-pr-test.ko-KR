---
title: "Azure 구독에 대 한 청구 또는 신용 경고를 aaaSet | Microsoft Docs"
description: "갑작스러운 청구에 당황하지 않도록 Azure 청구에 대한 경고를 설정하는 방법을 설명합니다."
keywords: "크레딧 경고, 청구 경고"
services: 
documentationcenter: 
author: vikdesai
manager: tonguyen
editor: 
tags: billing
ms.assetid: 9b7b3eeb-cd9d-4690-86a3-51b1e2a8974f
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: vikdesai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 711b9c72c59874792b0e229cdc5ec0fa517c24c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-billing-or-credit-alerts-for-your-microsoft-azure-subscriptions"></a><span data-ttu-id="3884e-104">Microsoft Azure 구독에 대한 청구 또는 크레딧 경고 설정</span><span class="sxs-lookup"><span data-stu-id="3884e-104">Set up billing or credit alerts for your Microsoft Azure subscriptions</span></span>
<span data-ttu-id="3884e-105">Azure 구독에 대 한 hello 계정 관리자 인 경우 hello Azure 청구 경고 서비스 toocreate 사용자 지정 된 청구 경고 데 도움이 되는 모니터링 하 고 Azure 계정에 대 한 대금 청구 작업 관리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3884e-105">If you’re hello Account Admin for an Azure subscription, you can use hello Azure Billing Alert Service toocreate customized billing alerts that help you monitor and manage billing activity for your Azure accounts.</span></span>

<span data-ttu-id="3884e-106">이 서비스는 미리 보기, tooenable 필요 것 hello 미리 보기 기능 페이지에 먼저입니다.</span><span class="sxs-lookup"><span data-stu-id="3884e-106">This service is in preview, so you need tooenable it in hello Preview Features page first.</span></span>

## <a name="set-hello-alert-threshold-and-email-recipients"></a><span data-ttu-id="3884e-107">Hello 경고 임계값 및 전자 메일 받는 사람 설정</span><span class="sxs-lookup"><span data-stu-id="3884e-107">Set hello alert threshold and email recipients</span></span>
1. <span data-ttu-id="3884e-108">방문 [hello 미리 보기 기능 페이지](https://account.windowsazure.com/PreviewFeatures) 사용 하도록 설정 하 고 **청구 경고 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="3884e-108">Visit [hello Preview Features page](https://account.windowsazure.com/PreviewFeatures) and enable **Billing Alert Service**.</span></span>

1. <span data-ttu-id="3884e-109">구독에 대 한 hello 청구 서비스가 켜져 hello 전자 메일 확인을 받은 후 방문 [hello 구독 페이지](https://account.windowsazure.com/Subscriptions) hello 계정 포털에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3884e-109">After you receive hello email confirmation that hello billing service is turned on for your subscription, visit [hello Subscriptions page](https://account.windowsazure.com/Subscriptions) in hello account portal.</span></span> <span data-ttu-id="3884e-110">Hello 구독 toomonitor을 클릭 한 다음 클릭 **경고**합니다.</span><span class="sxs-lookup"><span data-stu-id="3884e-110">Click hello subscription you want toomonitor, and then click **Alerts**.</span></span>

    ![강조 표시 하는 경고의 Azure 계정 센터 hello 구독 보기의 스크린샷][Image1]

2. <span data-ttu-id="3884e-112">그런 다음 클릭 **경고 추가** toocreate 첫 번째 앱.</span><span class="sxs-lookup"><span data-stu-id="3884e-112">Next, click **Add Alert** toocreate your first one.</span></span> <span data-ttu-id="3884e-113">서로 다른 임계값으로 구독 당 5 개의 청구 경고의 요약을 하 고 각 경고에 대 한 tootwo 전자 메일 받는 사람을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3884e-113">You can set up a total of five billing alerts per subscription, with a different threshold and up tootwo email recipients for each alert.</span></span>

    ![Hello 경고를 추가할 수 있는 경고 보기의 스크린샷][Image2]

3. <span data-ttu-id="3884e-115">경고를 추가 하는 경우에 고유한 이름을 지정, 지출 임계값 선택한 hello 경고가 전송 된 전자 메일 주소를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3884e-115">When you add an alert, you give it a unique name, choose a spending threshold, and choose hello email addresses where alerts are sent.</span></span> <span data-ttu-id="3884e-116">Hello 임계값을 설정할 때 하나를 선택할 수 있습니다는 **청구 금액 합계** 또는 **화폐 성 차변** hello에서 **경고에 대 한** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="3884e-116">When setting up hello threshold, you can choose either a **Billing Total** or a **Monetary Credit** from hello **Alert For** list.</span></span> <span data-ttu-id="3884e-117">청구 금액 합계에 대 한 구독 지출이 hello 임계값을 초과 하는 경우 경고가 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3884e-117">For a billing total, an alert is sent when subscription spending exceeds hello threshold.</span></span> <span data-ttu-id="3884e-118">화폐 성 차변에 대 한 금액 크레딧을 hello 한도 아래로 떨어지면 때 경고가 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3884e-118">For a monetary credit, an alert is sent when monetary credits drop below hello limit.</span></span> <span data-ttu-id="3884e-119">일반적으로 화폐 성 차변 tooFree 평가판 및 Visual Studio 구독을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3884e-119">Monetary credits usually apply tooFree Trial and Visual Studio subscriptions.</span></span>

    ![받는 사람을 구성할 수 있는 hello 추가 경고 보기의 스크린샷][Image3]

<span data-ttu-id="3884e-121">Azure에서는 모든 전자 메일 주소를 지원 하지만 hello 전자 메일 주소가 작동 하는지 확인를 하지 있으므로 입력 오류를 다시 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3884e-121">Azure supports any email address but doesn't verify that hello email address works, so double-check for typos.</span></span>

## <a name="check-on-your-alerts"></a><span data-ttu-id="3884e-122">경고 확인</span><span class="sxs-lookup"><span data-stu-id="3884e-122">Check on your alerts</span></span>
<span data-ttu-id="3884e-123">경고를 설정 하면 r e 계정 센터 hello 나열 하 고 개수를 설정할 수 있습니다 더을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3884e-123">After you set up alerts, hello Account Center lists them and shows how many more you can set up.</span></span> <span data-ttu-id="3884e-124">각 경고에 대 한 hello 날짜와 보낸 것, 청구 금액 합계 또는 금액 크레딧에 대 한 경고 인지 시간을 설정 하는 hello 제한 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="3884e-124">For each alert, you see hello date and time it was sent, whether it’s an alert for Billing Total or Monetary Credit, and hello limit you set up.</span></span> <span data-ttu-id="3884e-125">hello 날짜 및 시간 형식이 24 시간 조정 UTC (Universal Time)이 고 hello 날짜가 yyyy-월-일 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="3884e-125">hello date and time format is 24-hour Universal Time Coordinate (UTC) and hello date is yyyy-mm-dd format.</span></span> <span data-ttu-id="3884e-126">Hello 클릭 플러스, hello 목록 tooedit에서 경고에 대 한 서명 하거나 hello 휴지통에 있는 toodelete 클릭 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3884e-126">Click hello plus sign for an alert in hello list tooedit it, or click hello trash-can toodelete it.</span></span>

## <a name="billing-alerts-for-enterprise-agreement-ea-customers"></a><span data-ttu-id="3884e-127">EA(기업 계약) 고객의 청구 경고</span><span class="sxs-lookup"><span data-stu-id="3884e-127">Billing alerts for Enterprise Agreement (EA) customers</span></span>
<span data-ttu-id="3884e-128">EA 고객은 지출 할당량을 설정하여 등록 상태인 각 부서에 대한 경고를 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3884e-128">EA customers can get alerts for each department under an enrollment by setting spending quotas.</span></span> <span data-ttu-id="3884e-129">참조 [부서 지출 할당량](https://ea.azure.com/helpdocs/departmentSpendingQuotas) hello EA 포털 tooget 시작에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3884e-129">See [Department Spending Quotas](https://ea.azure.com/helpdocs/departmentSpendingQuotas) in hello EA portal tooget started.</span></span>

## <a name="learn-more-about-azure-cost-management"></a><span data-ttu-id="3884e-130">Azure 비용 관리에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="3884e-130">Learn more about Azure cost management</span></span>
- <span data-ttu-id="3884e-131">Hello를 사용 하 여 비용을 예측 [가격 계산기](https://azure.microsoft.com/pricing/calculator/), [총 비용 소유권 계산기의](https://aka.ms/azure-tco-calculator), 및 서비스를 추가 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="3884e-131">Estimate costs using hello [pricing calculator](https://azure.microsoft.com/pricing/calculator/), [total cost of ownership calculator](https://aka.ms/azure-tco-calculator), and when you add a service.</span></span>
- <span data-ttu-id="3884e-132">[Azure Portal에서 정기적으로 사용량 및 비용을 검토합니다](billing-getting-started.md#costs).</span><span class="sxs-lookup"><span data-stu-id="3884e-132">[Review your usage and costs regularly in Azure portal](billing-getting-started.md#costs).</span></span>
- <span data-ttu-id="3884e-133">[Azure Advisor 비용 권장 사항](../advisor/advisor-cost-recommendations.md)을 켭니다.</span><span class="sxs-lookup"><span data-stu-id="3884e-133">Turn on [Azure Advisor cost recommendations](../advisor/advisor-cost-recommendations.md).</span></span>

<span data-ttu-id="3884e-134">toolearn 더 참조 [Azure 비용 관리 지침](billing-getting-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3884e-134">toolearn more, see [Azure cost management guidance](billing-getting-started.md).</span></span>

[Image1]: ./media/azure-billing-set-up-alerts/billingalert1.png 
[Image2]: ./media/azure-billing-set-up-alerts/billingalert2.png
[Image3]: ./media/azure-billing-set-up-alerts/billingalerts3.png 
