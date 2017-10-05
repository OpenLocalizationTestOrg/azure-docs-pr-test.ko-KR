---
title: "Azure 앱 서비스: 앱 서비스 응용 프로그램 크기 조정"
description: "앱 서비스에서 응용 프로그램 크기 조정의 다양한 측면을 알아봅니다."
keywords: "앱 서비스, Azure 앱 서비스, 규모, 확장성, 앱 서비스 계획, 앱 서비스 비용"
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: f403c971-4450-432b-8cea-3eeb426c0147
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/07/2016
ms.author: byvinyal
ms.openlocfilehash: 4ebaafe69fc1f91c7890611b14e8600df5c40cde
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-scaling-app-service-applications"></a><span data-ttu-id="63be7-104">Azure 앱 서비스: 앱 서비스 응용 프로그램 크기 조정</span><span class="sxs-lookup"><span data-stu-id="63be7-104">Azure App Service: Scaling App Service Applications</span></span>
<span data-ttu-id="63be7-105">Azure 앱 서비스에서 호스팅되는 응용 프로그램은 [대규모로 확장](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63be7-105">Applications hosted in Azure App Service can [achieve massive scale](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).</span></span>
<span data-ttu-id="63be7-106">하지만 응용 프로그램의 크기를 조정하는 작업은 "보편적으로 적용되는" 솔루션이 없는 복잡한 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="63be7-106">However, scaling an application is a complex problem that does not have a "one size fits all" solution.</span></span> <span data-ttu-id="63be7-107">응용 프로그램의 크기를 올바르게 조정하기 위해 응용 프로그램 성공에 기여하는 3가지 주요 영역이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63be7-107">To correctly scale your application there are 3 key areas that will contribute to your applications success:</span></span>

1. <span data-ttu-id="63be7-108">응용 프로그램 아키텍처와 약점 이해</span><span class="sxs-lookup"><span data-stu-id="63be7-108">Understanding your application architecture and its weaknesses.</span></span>
   * <span data-ttu-id="63be7-109">응용 프로그램이 상태 저장인가요?</span><span class="sxs-lookup"><span data-stu-id="63be7-109">Is your Application Stateful?</span></span> <span data-ttu-id="63be7-110">상태 비저장인가요?</span><span class="sxs-lookup"><span data-stu-id="63be7-110">Stateless?</span></span>
   * <span data-ttu-id="63be7-111">응용 프로그램의 모든 구성 요소는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="63be7-111">What are all the components of your application?</span></span>
     * <span data-ttu-id="63be7-112">응용 프로그램의 병목 지점은 어디인가요?</span><span class="sxs-lookup"><span data-stu-id="63be7-112">Where are the bottlenecks in the application?</span></span>
   * <span data-ttu-id="63be7-113">응용 프로그램에 부하가 걸리면 무엇부터 중단되나요?</span><span class="sxs-lookup"><span data-stu-id="63be7-113">When load is applied to your app, what will break first?</span></span>
2. <span data-ttu-id="63be7-114">예상된 부하 및 성능 요구 사항 이해</span><span class="sxs-lookup"><span data-stu-id="63be7-114">Understanding the expected load and performance requirements.</span></span>
   * <span data-ttu-id="63be7-115">응용 프로그램이 천 명의 사용자를 위한 것인가요? 아니면 백만 명의 사용자를 위한 것인가요?</span><span class="sxs-lookup"><span data-stu-id="63be7-115">Does the application need to serve one thousand users? or one million?</span></span>
   * <span data-ttu-id="63be7-116">트래픽이 단일 지리적 위치에서 생기나요? 아니면 전역적으로 생기나요?</span><span class="sxs-lookup"><span data-stu-id="63be7-116">Will traffic come from a single geographic location or globally?</span></span>
   * <span data-ttu-id="63be7-117">계절적 변동이 있나요? 트래픽 정점이 있나요?</span><span class="sxs-lookup"><span data-stu-id="63be7-117">Are there seasonal variations? traffic peaks?</span></span>
   * <span data-ttu-id="63be7-118">앱 응답 속도가 얼마나 빠른가요?</span><span class="sxs-lookup"><span data-stu-id="63be7-118">How fast should the app respond?</span></span> <span data-ttu-id="63be7-119">1초?</span><span class="sxs-lookup"><span data-stu-id="63be7-119">1 second?</span></span> <span data-ttu-id="63be7-120">1밀리초인가요?</span><span class="sxs-lookup"><span data-stu-id="63be7-120">1 millisecond?</span></span>
3. <span data-ttu-id="63be7-121">응용 프로그램 호스팅 플랫폼에 대한 이해 및 올바른 활용</span><span class="sxs-lookup"><span data-stu-id="63be7-121">Understanding and correctly leverage the platform hosting your app.</span></span>
   * <span data-ttu-id="63be7-122">내 목표 규모를 달성하기 위해 무슨 기능을 활용해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="63be7-122">What features should I leverage to achieve my scale goals?</span></span>

<span data-ttu-id="63be7-123">이 섹션에서는 모든 요소를 이해하고 장치에서 확장성 목표를 달성하는 데 필요한 App Service 기능을 활용하는 전략을 세울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63be7-123">This section will help you understand all the factors and help you devise a strategy that takes advantage of the necessary App Service features to achieve your scalability goals.</span></span>

[!INCLUDE [app-service-blueprint-scaling-app-service-applications](../../includes/app-service-blueprint-scaling-app-service-applications.md)]

