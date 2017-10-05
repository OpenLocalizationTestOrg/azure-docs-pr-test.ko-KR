---
title: "Azure Advisor 보안 권장 사항 | Microsoft Docs"
description: "Azure Advisor를 사용하여 Azure 배포의 보안을 향상시킵니다."
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
ms.openlocfilehash: 53be05593c3733ccb27979a3a026414013125779
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="advisor-security-recommendations"></a><span data-ttu-id="23e6b-103">Advisor 보안 권장 사항 관리</span><span class="sxs-lookup"><span data-stu-id="23e6b-103">Advisor Security recommendations</span></span>

<span data-ttu-id="23e6b-104">Azure Advisor는 모든 Azure 리소스에 대한 권장 사항을 일관되고 통합된 보기로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="23e6b-104">Azure Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources.</span></span> <span data-ttu-id="23e6b-105">보안 권장 사항을 제공하기 위해 Azure Security Center와 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="23e6b-105">It integrates with Azure Security Center to bring you security recommendations.</span></span> <span data-ttu-id="23e6b-106">Advisor 대시보드의 **보안** 탭에서 보안 관련 권장 지침을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23e6b-106">You can get security recommendations from the **Security** tab on the Advisor dashboard.</span></span>

![Advisor 보안 단추](./media/advisor-security-recommendations/advisor-security-tab.png)

<span data-ttu-id="23e6b-108">보안 센터는 Azure 리소스의 보안에 대한 향상된 가시성과 제어권을 통해 위협을 예방하고 감지하며 위협에 대응하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="23e6b-108">Security Center helps you prevent, detect, and respond to threats with increased visibility into and control over the security of your Azure resources.</span></span> <span data-ttu-id="23e6b-109">여기서는 Azure 리소스의 보안 상태를 주기적으로 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="23e6b-109">It periodically analyzes the security state of your Azure resources.</span></span> <span data-ttu-id="23e6b-110">보안 센터가 잠재적인 보안 취약점을 식별하는 경우 권장 사항을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="23e6b-110">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span></span> <span data-ttu-id="23e6b-111">권장 사항은 필요한 컨트롤을 구성하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="23e6b-111">The recommendations guide you through the process of configuring the controls you need.</span></span> 

![Advisor 보안 탭](./media/advisor-security-recommendations/advisor-security-recommendations.png)

<span data-ttu-id="23e6b-113">보안 권장 사항에 대한 자세한 내용은 [Azure Security Center에서 보안 권장 사항 관리](https://azure.microsoft.com/en-us/documentation/articles/security-center-recommendations/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="23e6b-113">For more information about security recommendations, see [Managing security recommendations in Azure Security Center](https://azure.microsoft.com/en-us/documentation/articles/security-center-recommendations/).</span></span>

## <a name="how-to-access-security-recommendations-in-azure-advisor"></a><span data-ttu-id="23e6b-114">Azure Advisor에서 보안 권장 사항에 액세스하는 방법</span><span class="sxs-lookup"><span data-stu-id="23e6b-114">How to access Security recommendations in Azure Advisor</span></span>

1. <span data-ttu-id="23e6b-115">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="23e6b-115">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="23e6b-116">왼쪽 창에서 **더 많은 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="23e6b-116">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="23e6b-117">서비스 메뉴 창의 **모니터링 및 관리** 아래에서 **Azure Advisor**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="23e6b-117">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="23e6b-118">Advisor 대시보드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="23e6b-118">The Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="23e6b-119">Advisor 대시보드에서 **보안** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="23e6b-119">On the Advisor dashboard, click the **Security** tab.</span></span>

5. <span data-ttu-id="23e6b-120">권장 사항을 받아보려는 구독을 선택하고 **권장 사항 가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="23e6b-120">Select the subscription for which you want to receive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="23e6b-121">Advisor 권장 사항에 액세스하려면 먼저 Advisor에 *구독을 등록*해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="23e6b-121">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="23e6b-122">구독은 *구독 소유자*가 Advisor 대시보드를 시작하고 **권장 사항 가져오기** 단추를 클릭할 때 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="23e6b-122">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="23e6b-123">이 작업은 *한 번만* 수행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="23e6b-123">This is a *one-time operation*.</span></span> <span data-ttu-id="23e6b-124">구독이 등록된 후 구독, 리소스 그룹 또는 특정 리소스에 대한 *소유자*, *참여자* 또는 *리더*로 Advisor 권장 사항에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23e6b-124">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="23e6b-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="23e6b-125">Next steps</span></span>

<span data-ttu-id="23e6b-126">Advisor 권장 사항에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="23e6b-126">To learn more about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="23e6b-127">Advisor 소개</span><span class="sxs-lookup"><span data-stu-id="23e6b-127">Introduction to Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="23e6b-128">Advisor 시작</span><span class="sxs-lookup"><span data-stu-id="23e6b-128">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="23e6b-129">Advisor 비용 권장 사항</span><span class="sxs-lookup"><span data-stu-id="23e6b-129">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="23e6b-130">Advisor 성능 권장 사항</span><span class="sxs-lookup"><span data-stu-id="23e6b-130">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="23e6b-131">Advisor 고가용성 권장 사항</span><span class="sxs-lookup"><span data-stu-id="23e6b-131">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)


 
