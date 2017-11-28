---
title: "Azure Advisor 백업 소개 | Microsoft Docs"
description: "Azure Advisor를 사용하여 Azure 배포를 최적화합니다."
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 35678142550f9f887562f311a5e7d9516495cf53
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-azure-advisor"></a><span data-ttu-id="b2eac-103">Azure Advisor 소개</span><span class="sxs-lookup"><span data-stu-id="b2eac-103">Introduction to Azure Advisor</span></span>

<span data-ttu-id="b2eac-104">Azure Advisor 및 주요 기능에 대해 알아보고 자주 묻는 질문과 답변을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="b2eac-104">Learn about Azure Advisor and its key capabilities, and get answers to frequently asked questions.</span></span>

## <a name="what-is-advisor"></a><span data-ttu-id="b2eac-105">Advisor란?</span><span class="sxs-lookup"><span data-stu-id="b2eac-105">What is Advisor?</span></span>
<span data-ttu-id="b2eac-106">Advisor는 Azure 배포를 최적화하기 위한 모범 사례를 따르는 데 도움이 되는 개인 설정된 클라우드 컨설턴트입니다.</span><span class="sxs-lookup"><span data-stu-id="b2eac-106">Advisor is a personalized cloud consultant that helps you follow best practices to optimize your Azure deployments.</span></span> <span data-ttu-id="b2eac-107">리소스 구성 및 사용량 원격 분석을 수행하고 Azure 리소스의 경제성, 성능, 고가용성 및 보안을 개선하는 데 도움이 되는 해결 방법을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="b2eac-107">It analyzes your resource configuration and usage telemetry and then recommends solutions that can help you improve the cost effectiveness, performance, high availability, and security of your Azure resources.</span></span>

<span data-ttu-id="b2eac-108">Advisor를 사용하면 다음과 같은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2eac-108">With Advisor, you can:</span></span>
* <span data-ttu-id="b2eac-109">사전 대응이 가능하고, 실행 가능하고, 개인화된 모범 사례 권장 사항</span><span class="sxs-lookup"><span data-stu-id="b2eac-109">Get proactive, actionable, and personalized best practices recommendations.</span></span> 
* <span data-ttu-id="b2eac-110">전체 Azure 사용을 줄일 수 있는 기회를 모색하면서 성능, 보안 및 고가용성 개선</span><span class="sxs-lookup"><span data-stu-id="b2eac-110">Improve the performance, security, and high availability of your resources, as you identify opportunities to reduce your overall Azure spend.</span></span>
* <span data-ttu-id="b2eac-111">온라인으로 작업이 제안되는 권장 사항 가져오기</span><span class="sxs-lookup"><span data-stu-id="b2eac-111">Get recommendations with proposed actions inline.</span></span>

<span data-ttu-id="b2eac-112">[Azure Portal](https://aka.ms/azureadvisordashboard)을 통해 Advisor에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2eac-112">You can access Advisor through the [Azure portal](https://aka.ms/azureadvisordashboard).</span></span> <span data-ttu-id="b2eac-113">[포털](https://portal.azure.com)에 로그인하고 **찾아보기**를 선택한 다음 **Azure Advisor**로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="b2eac-113">Sign in to the [portal](https://portal.azure.com), select **Browse**, and then scroll to **Azure Advisor**.</span></span> <span data-ttu-id="b2eac-114">Advisor 대시보드에 선택한 구독에 대한 개인화된 권장 사항이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2eac-114">The Advisor dashboard displays personalized recommendations for a selected subscription.</span></span> 

<span data-ttu-id="b2eac-115">권장 사항은 다음 네 가지 범주로 나뉩니다.</span><span class="sxs-lookup"><span data-stu-id="b2eac-115">The recommendations are divided into four categories:</span></span> 

* <span data-ttu-id="b2eac-116">**고가용성**: 업무상 중요한 응용 프로그램의 연속성을 보장하고 향상시키는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2eac-116">**High Availability**: To ensure and improve the continuity of your business-critical applications.</span></span> <span data-ttu-id="b2eac-117">자세한 내용은 [Advisor 고가용성 권장 사항](advisor-high-availability-recommendations.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b2eac-117">For more information, see [Advisor High Availability recommendations](advisor-high-availability-recommendations.md).</span></span>

* <span data-ttu-id="b2eac-118">**보안**: 보안 위반으로 이어질 수 있는 위협 및 취약점을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="b2eac-118">**Security**: To detect threats and vulnerabilities that might lead to security breaches.</span></span> <span data-ttu-id="b2eac-119">자세한 내용은 [Advisor 보안 권장 사항](advisor-security-recommendations.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b2eac-119">For more information, see [Advisor Security recommendations](advisor-security-recommendations.md).</span></span>

* <span data-ttu-id="b2eac-120">**성능**: 응용 프로그램의 속도를 향상시킵니다.</span><span class="sxs-lookup"><span data-stu-id="b2eac-120">**Performance**: To improve the speed of your applications.</span></span> <span data-ttu-id="b2eac-121">자세한 내용은 [Advisor 성능 권장 사항](advisor-performance-recommendations.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b2eac-121">For more information, see [Advisor Performance recommendations](advisor-performance-recommendations.md).</span></span>

* <span data-ttu-id="b2eac-122">**비용**: 전체 Azure 사용을 최적화하고 사용량을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="b2eac-122">**Cost**: To optimize and reduce your overall Azure spend.</span></span> <span data-ttu-id="b2eac-123">자세한 내용은 [Advisor 비용 권장 사항](advisor-cost-recommendations.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b2eac-123">For more information, see [Advisor Cost recommendations](advisor-cost-recommendations.md).</span></span>

  ![Advisor 권장 사항 유형](./media/advisor-overview/advisor-all-tab-examples.png)

> [!NOTE]
> <span data-ttu-id="b2eac-125">Advisor 권장 사항에 액세스하려면 먼저 Advisor에 *구독을 등록*해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2eac-125">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="b2eac-126">구독은 *구독 소유자*가 Advisor 대시보드를 시작하고 **권장 사항 가져오기** 단추를 클릭할 때 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2eac-126">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="b2eac-127">이 작업은 *한 번만* 수행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2eac-127">This is a *one-time operation*.</span></span> <span data-ttu-id="b2eac-128">구독이 등록된 후 구독, 리소스 그룹 또는 특정 리소스에 대한 *소유자*, *참여자* 또는 *리더*로 Advisor 권장 사항에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2eac-128">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

<span data-ttu-id="b2eac-129">권장 사항을 클릭하여 추가 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2eac-129">You can click a recommendation to learn more about it.</span></span> <span data-ttu-id="b2eac-130">기회를 활용하거나 문제를 해결하기 위해 수행할 수 있는 작업에 대해 알아볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2eac-130">You can also learn about actions that you can perform to take advantage of an opportunity or resolve an issue.</span></span> 

<span data-ttu-id="b2eac-131">Advisor는 인라인 작업 또는 설명서 링크가 있는 권장 사항을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b2eac-131">Advisor offers recommendations with inline actions or documentation links.</span></span> <span data-ttu-id="b2eac-132">인라인 작업을 클릭하면 "유도 사용자 경험"에 따라 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2eac-132">Clicking an inline action takes you through a “guided user journey” to implement it.</span></span> <span data-ttu-id="b2eac-133">설명서 링크를 클릭하면 작업을 수동으로 구현하는 방법을 설명하는 문서로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2eac-133">Clicking a documentation link points you to documentation that describes how to manually implement the action.</span></span> 

<span data-ttu-id="b2eac-134">Advisor는 시간별로 권장 사항을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="b2eac-134">Advisor updates recommendations hourly.</span></span> <span data-ttu-id="b2eac-135">권장 사항에 대해 즉각적인 작업을 수행하지 않으려는 경우 지정된 시간 후에 다시 알리거나 닫을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2eac-135">If you don’t intend to take immediate action on a recommendation, you can snooze it for a specified time period or dismiss it.</span></span> 

## <a name="frequently-asked-questions"></a><span data-ttu-id="b2eac-136">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="b2eac-136">Frequently asked questions</span></span>

### <a name="how-do-i-access-advisor"></a><span data-ttu-id="b2eac-137">Advisor에 액세스하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="b2eac-137">How do I access Advisor?</span></span>
<span data-ttu-id="b2eac-138">[Azure Portal](https://aka.ms/azureadvisordashboard)을 통해 Advisor에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2eac-138">You can access Advisor through the [Azure portal](https://aka.ms/azureadvisordashboard).</span></span> <span data-ttu-id="b2eac-139">[포털](https://portal.azure.com)에 로그인하고 **찾아보기**를 선택한 다음 **Azure Advisor**로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="b2eac-139">Sign in to the [portal](https://portal.azure.com), select **Browse**, and then scroll to **Azure Advisor**.</span></span> <span data-ttu-id="b2eac-140">Advisor 대시보드에 선택한 구독에 대한 개인화된 권장 사항이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2eac-140">The Advisor dashboard displays personalized recommendations for a selected subscription.</span></span> 

<span data-ttu-id="b2eac-141">가상 컴퓨터 리소스 블레이드를 통해 Advisor 권장 사항을 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2eac-141">You can also view Advisor recommendations through the virtual machine resource blade.</span></span> <span data-ttu-id="b2eac-142">가상 컴퓨터를 선택하고 메뉴에서 Advisor 권장 사항으로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="b2eac-142">Choose a virtual machine, and then scroll to Advisor recommendations in the menu.</span></span> 

### <a name="what-permissions-do-i-need-to-access-advisor"></a><span data-ttu-id="b2eac-143">Advisor에 액세스하려면 어떤 권한이 필요하나요?</span><span class="sxs-lookup"><span data-stu-id="b2eac-143">What permissions do I need to access Advisor?</span></span>

<span data-ttu-id="b2eac-144">Advisor 권장 사항에 액세스하려면 먼저 Advisor에 *구독을 등록*해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2eac-144">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="b2eac-145">구독은 *구독 소유자*가 Advisor 대시보드를 시작하고 **권장 사항 가져오기** 단추를 클릭할 때 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2eac-145">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="b2eac-146">이 작업은 *한 번만* 수행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2eac-146">This is a *one-time operation*.</span></span> <span data-ttu-id="b2eac-147">구독이 등록된 후 구독, 리소스 그룹 또는 특정 리소스에 대한 *소유자*, *참여자* 또는 *리더*로 Advisor 권장 사항에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2eac-147">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

### <a name="how-often-are-advisor-recommendations-updated"></a><span data-ttu-id="b2eac-148">Advisor 권장 사항은 얼마나 자주 업데이트되나요?</span><span class="sxs-lookup"><span data-stu-id="b2eac-148">How often are Advisor recommendations updated?</span></span>

<span data-ttu-id="b2eac-149">Advisor 권장 사항은 시간별로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2eac-149">Advisor recommendations are updated hourly.</span></span>

### <a name="what-resources-does-advisor-provide-recommendations-for"></a><span data-ttu-id="b2eac-150">Advisor는 어떤 리소스에 대해 권장 사항을 제공하나요?</span><span class="sxs-lookup"><span data-stu-id="b2eac-150">What resources does Advisor provide recommendations for?</span></span>

<span data-ttu-id="b2eac-151">Advisor는 가상 컴퓨터, 가용성 집합, Application Gateway, App Services, SQL Server, SQL Database 및 Redis Cache에 대한 권장 사항을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b2eac-151">Advisor provides recommendations for virtual machines, availability sets, application gateways, App Services, SQL servers, SQL databases, and Redis Cache.</span></span>

### <a name="can-i-snooze-or-dismiss-a-recommendation"></a><span data-ttu-id="b2eac-152">권장 사항을 다시 알리거나 해제할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="b2eac-152">Can I snooze or dismiss a recommendation?</span></span>

<span data-ttu-id="b2eac-153">권장 사항을 다시 알리거나 해제하려면 **다시 알림** 단추 또는 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b2eac-153">To snooze or dismiss a recommendation, click the **Snooze** button or link.</span></span> <span data-ttu-id="b2eac-154">다시 알림 기간을 지정하거나, 권장 사항을 해제하려면 **안 함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b2eac-154">You can specify a snooze time period or select **Never** to dismiss the recommendation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2eac-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b2eac-155">Next steps</span></span>

<span data-ttu-id="b2eac-156">Advisor 권장 사항에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b2eac-156">To learn more about Advisor recommendations, see:</span></span>

* [<span data-ttu-id="b2eac-157">Advisor 시작</span><span class="sxs-lookup"><span data-stu-id="b2eac-157">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="b2eac-158">Advisor 고가용성 권장 사항</span><span class="sxs-lookup"><span data-stu-id="b2eac-158">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)
* [<span data-ttu-id="b2eac-159">Advisor 보안 권장 사항</span><span class="sxs-lookup"><span data-stu-id="b2eac-159">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)
* [<span data-ttu-id="b2eac-160">Advisor 성능 권장 사항</span><span class="sxs-lookup"><span data-stu-id="b2eac-160">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="b2eac-161">Advisor 비용 권장 사항</span><span class="sxs-lookup"><span data-stu-id="b2eac-161">Advisor Cost recommendations</span></span>](advisor-cost-recommendations.md)
