---
title: "Azure 구독에 대한 청구 또는 크레딧 경고 설정 | Microsoft Docs"
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
ms.openlocfilehash: 7a1b579fdde831fdc3afa0a2aee4c24890216ed1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-billing-or-credit-alerts-for-your-microsoft-azure-subscriptions"></a><span data-ttu-id="13ab1-104">Microsoft Azure 구독에 대한 청구 또는 크레딧 경고 설정</span><span class="sxs-lookup"><span data-stu-id="13ab1-104">Set up billing or credit alerts for your Microsoft Azure subscriptions</span></span>
<span data-ttu-id="13ab1-105">Azure 구독의 계정 관리자인 경우 Azure 청구 경고 서비스를 사용하여 Azure 계정에 대한 청구 활동을 모니터링하고 관리하는 데 도움이 되는 사용자 지정된 청구 경고를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13ab1-105">If you’re the Account Admin for an Azure subscription, you can use the Azure Billing Alert Service to create customized billing alerts that help you monitor and manage billing activity for your Azure accounts.</span></span>

<span data-ttu-id="13ab1-106">이 서비스는 미리 보기이므로 먼저 미리 보기 기능 페이지에서 이 서비스를 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ab1-106">This service is in preview, so you need to enable it in the Preview Features page first.</span></span>

## <a name="set-the-alert-threshold-and-email-recipients"></a><span data-ttu-id="13ab1-107">경고 임계값 및 메일 받는 사람 설정</span><span class="sxs-lookup"><span data-stu-id="13ab1-107">Set the alert threshold and email recipients</span></span>
1. <span data-ttu-id="13ab1-108">[미리 보기 기능 페이지](https://account.windowsazure.com/PreviewFeatures)를 방문하여 **청구 경고 서비스**를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="13ab1-108">Visit [the Preview Features page](https://account.windowsazure.com/PreviewFeatures) and enable **Billing Alert Service**.</span></span>

1. <span data-ttu-id="13ab1-109">구독에 대해 청구 서비스가 설정되었다는 메일 확인을 받은 후에 계정 포털의 [구독 페이지](https://account.windowsazure.com/Subscriptions) 를 방문합니다.</span><span class="sxs-lookup"><span data-stu-id="13ab1-109">After you receive the email confirmation that the billing service is turned on for your subscription, visit [the Subscriptions page](https://account.windowsazure.com/Subscriptions) in the account portal.</span></span> <span data-ttu-id="13ab1-110">모니터링할 구독을 클릭한 다음 **경고**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13ab1-110">Click the subscription you want to monitor, and then click **Alerts**.</span></span>

    ![경고가 강조 표시된 Azure 계정 센터의 구독 보기 스크린샷][Image1]

2. <span data-ttu-id="13ab1-112">다음으로 **경고 추가**를 클릭하여 첫 번째 경고를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="13ab1-112">Next, click **Add Alert** to create your first one.</span></span> <span data-ttu-id="13ab1-113">구독당 최대 총 5개의 청구 경고를 설정할 수 있으며, 각 경고에 대해 서로 다른 임계값을 설정하고, 각 경고에 대해 최대 두 명의 메일 받는 사람을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13ab1-113">You can set up a total of five billing alerts per subscription, with a different threshold and up to two email recipients for each alert.</span></span>

    ![경고를 추가할 수 있는 경고 보기의 스크린샷][Image2]

3. <span data-ttu-id="13ab1-115">경고를 추가할 때 고유 이름을 지정하고, 지출 임계값을 선택하고, 경고를 전송할 메일 주소를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="13ab1-115">When you add an alert, you give it a unique name, choose a spending threshold, and choose the email addresses where alerts are sent.</span></span> <span data-ttu-id="13ab1-116">임계값을 설정할 때 **경고 대상** 목록에서 **청구 금액 합계** 또는 **금액 크레딧**을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13ab1-116">When setting up the threshold, you can choose either a **Billing Total** or a **Monetary Credit** from the **Alert For** list.</span></span> <span data-ttu-id="13ab1-117">청구 금액 합계의 경우 경고는 구독 지출이 임계값을 초과하면 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="13ab1-117">For a billing total, an alert is sent when subscription spending exceeds the threshold.</span></span> <span data-ttu-id="13ab1-118">금액 크레딧의 경우 경고는 금액 크레딧이 한도 아래로 떨어지면 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="13ab1-118">For a monetary credit, an alert is sent when monetary credits drop below the limit.</span></span> <span data-ttu-id="13ab1-119">금액 크레딧은 일반적으로 무료 평가판 및 Visual Studio 구독에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="13ab1-119">Monetary credits usually apply to Free Trial and Visual Studio subscriptions.</span></span>

    ![받는 사람을 구성할 수 있는 경고 추가 보기의 스크린샷][Image3]

<span data-ttu-id="13ab1-121">Azure는 모든 메일 주소를 지원하지만 해당 메일 주소가 작동하는지 확인하지 않으므로 오타가 없는지 다시 한 번 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="13ab1-121">Azure supports any email address but doesn't verify that the email address works, so double-check for typos.</span></span>

## <a name="check-on-your-alerts"></a><span data-ttu-id="13ab1-122">경고 확인</span><span class="sxs-lookup"><span data-stu-id="13ab1-122">Check on your alerts</span></span>
<span data-ttu-id="13ab1-123">경고를 설정하고 나면 계정 센터에 해당 경고가 나열되고 더 설정할 수 있는 경고 횟수가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="13ab1-123">After you set up alerts, the Account Center lists them and shows how many more you can set up.</span></span> <span data-ttu-id="13ab1-124">각 경고에 대해 전송된 날짜 및 시간, 청구 금액 합계에 대한 경고인지 금액 크레딧에 대한 경고인지 여부 및 설정한 한도가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="13ab1-124">For each alert, you see the date and time it was sent, whether it’s an alert for Billing Total or Monetary Credit, and the limit you set up.</span></span> <span data-ttu-id="13ab1-125">날짜 및 시간 형식은 24시간 UTC(Universal Time Coordinate)이며 날짜는 yyyy-mm-dd 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="13ab1-125">The date and time format is 24-hour Universal Time Coordinate (UTC) and the date is yyyy-mm-dd format.</span></span> <span data-ttu-id="13ab1-126">경고를 편집하려면 목록에서 경고의 더하기 기호를 클릭하고, 경고를 삭제하려면 휴지통을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13ab1-126">Click the plus sign for an alert in the list to edit it, or click the trash-can to delete it.</span></span>

## <a name="billing-alerts-for-enterprise-agreement-ea-customers"></a><span data-ttu-id="13ab1-127">EA(기업 계약) 고객의 청구 경고</span><span class="sxs-lookup"><span data-stu-id="13ab1-127">Billing alerts for Enterprise Agreement (EA) customers</span></span>
<span data-ttu-id="13ab1-128">EA 고객은 지출 할당량을 설정하여 등록 상태인 각 부서에 대한 경고를 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13ab1-128">EA customers can get alerts for each department under an enrollment by setting spending quotas.</span></span> <span data-ttu-id="13ab1-129">시작 방법은 EA 포털에서 [부서 지출 할당량](https://ea.azure.com/helpdocs/departmentSpendingQuotas)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="13ab1-129">See [Department Spending Quotas](https://ea.azure.com/helpdocs/departmentSpendingQuotas) in the EA portal to get started.</span></span>

## <a name="learn-more-about-azure-cost-management"></a><span data-ttu-id="13ab1-130">Azure 비용 관리에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="13ab1-130">Learn more about Azure cost management</span></span>
- <span data-ttu-id="13ab1-131">[가격 계산기](https://azure.microsoft.com/pricing/calculator/), [총 소유 비용 계산기](https://aka.ms/azure-tco-calculator)를 사용하여 비용 및 서비스를 추가할 시기를 예측합니다.</span><span class="sxs-lookup"><span data-stu-id="13ab1-131">Estimate costs using the [pricing calculator](https://azure.microsoft.com/pricing/calculator/), [total cost of ownership calculator](https://aka.ms/azure-tco-calculator), and when you add a service.</span></span>
- <span data-ttu-id="13ab1-132">[Azure Portal에서 정기적으로 사용량 및 비용을 검토합니다](billing-getting-started.md#costs).</span><span class="sxs-lookup"><span data-stu-id="13ab1-132">[Review your usage and costs regularly in Azure portal](billing-getting-started.md#costs).</span></span>
- <span data-ttu-id="13ab1-133">[Azure Advisor 비용 권장 사항](../advisor/advisor-cost-recommendations.md)을 켭니다.</span><span class="sxs-lookup"><span data-stu-id="13ab1-133">Turn on [Azure Advisor cost recommendations](../advisor/advisor-cost-recommendations.md).</span></span>

<span data-ttu-id="13ab1-134">자세한 내용은 참조 [Azure 비용 관리 지침](billing-getting-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="13ab1-134">To learn more, see [Azure cost management guidance](billing-getting-started.md).</span></span>

[Image1]: ./media/azure-billing-set-up-alerts/billingalert1.png 
[Image2]: ./media/azure-billing-set-up-alerts/billingalert2.png
[Image3]: ./media/azure-billing-set-up-alerts/billingalerts3.png 
