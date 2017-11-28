---
title: "Azure 앱 서비스: 앱 서비스 응용 프로그램 크기 조정"
description: "Hello의 장단점 앱 서비스의 응용 프로그램을 확장에 대해 알아봅니다."
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
ms.openlocfilehash: d8cd12f73915a916a75d46da2f751a40d567b189
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-scaling-app-service-applications"></a><span data-ttu-id="188d6-104">Azure 앱 서비스: 앱 서비스 응용 프로그램 크기 조정</span><span class="sxs-lookup"><span data-stu-id="188d6-104">Azure App Service: Scaling App Service Applications</span></span>
<span data-ttu-id="188d6-105">Azure 앱 서비스에서 호스팅되는 응용 프로그램은 [대규모로 확장](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="188d6-105">Applications hosted in Azure App Service can [achieve massive scale](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).</span></span>
<span data-ttu-id="188d6-106">하지만 응용 프로그램의 크기를 조정하는 작업은 "보편적으로 적용되는" 솔루션이 없는 복잡한 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="188d6-106">However, scaling an application is a complex problem that does not have a "one size fits all" solution.</span></span> <span data-ttu-id="188d6-107">응용 프로그램을 확장 하는 toocorrectly 3 주요 영역을 가장 기본적 주지 tooyour 응용 프로그램 성공:</span><span class="sxs-lookup"><span data-stu-id="188d6-107">toocorrectly scale your application there are 3 key areas that will contribute tooyour applications success:</span></span>

1. <span data-ttu-id="188d6-108">응용 프로그램 아키텍처와 약점 이해</span><span class="sxs-lookup"><span data-stu-id="188d6-108">Understanding your application architecture and its weaknesses.</span></span>
   * <span data-ttu-id="188d6-109">응용 프로그램이 상태 저장인가요?</span><span class="sxs-lookup"><span data-stu-id="188d6-109">Is your Application Stateful?</span></span> <span data-ttu-id="188d6-110">상태 비저장인가요?</span><span class="sxs-lookup"><span data-stu-id="188d6-110">Stateless?</span></span>
   * <span data-ttu-id="188d6-111">응용 프로그램의 모든 hello 구성 요소는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="188d6-111">What are all hello components of your application?</span></span>
     * <span data-ttu-id="188d6-112">Hello 응용 프로그램의 hello 병목 상태를 어디 입니까?</span><span class="sxs-lookup"><span data-stu-id="188d6-112">Where are hello bottlenecks in hello application?</span></span>
   * <span data-ttu-id="188d6-113">부하는 적용 된 tooyour 앱 첫 번째 끊긴다는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="188d6-113">When load is applied tooyour app, what will break first?</span></span>
2. <span data-ttu-id="188d6-114">이해 hello 부하 및 성능 요구 사항을 예상 합니다.</span><span class="sxs-lookup"><span data-stu-id="188d6-114">Understanding hello expected load and performance requirements.</span></span>
   * <span data-ttu-id="188d6-115">Tooserve 하나 천 사용자 hello 응용 프로그램에 필요 합니까? 또는 1 백만?</span><span class="sxs-lookup"><span data-stu-id="188d6-115">Does hello application need tooserve one thousand users? or one million?</span></span>
   * <span data-ttu-id="188d6-116">트래픽이 단일 지리적 위치에서 생기나요? 아니면 전역적으로 생기나요?</span><span class="sxs-lookup"><span data-stu-id="188d6-116">Will traffic come from a single geographic location or globally?</span></span>
   * <span data-ttu-id="188d6-117">계절적 변동이 있나요? 트래픽 정점이 있나요?</span><span class="sxs-lookup"><span data-stu-id="188d6-117">Are there seasonal variations? traffic peaks?</span></span>
   * <span data-ttu-id="188d6-118">Hello 응용 프로그램 응답 속도</span><span class="sxs-lookup"><span data-stu-id="188d6-118">How fast should hello app respond?</span></span> <span data-ttu-id="188d6-119">1초?</span><span class="sxs-lookup"><span data-stu-id="188d6-119">1 second?</span></span> <span data-ttu-id="188d6-120">1밀리초인가요?</span><span class="sxs-lookup"><span data-stu-id="188d6-120">1 millisecond?</span></span>
3. <span data-ttu-id="188d6-121">이해 및 제대로 활용 하 여 hello 플랫폼 호스팅 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="188d6-121">Understanding and correctly leverage hello platform hosting your app.</span></span>
   * <span data-ttu-id="188d6-122">기능의 해야 tooachieve 내 눈금 목표를 활용 하나요?</span><span class="sxs-lookup"><span data-stu-id="188d6-122">What features should I leverage tooachieve my scale goals?</span></span>

<span data-ttu-id="188d6-123">이 섹션은 모든 hello 요인과 hello 필요한 앱 서비스 기능 tooachieve 확장성 목표를 활용 하는 전략을 고안 도움말을 이해 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="188d6-123">This section will help you understand all hello factors and help you devise a strategy that takes advantage of hello necessary App Service features tooachieve your scalability goals.</span></span>

[!INCLUDE [app-service-blueprint-scaling-app-service-applications](../../includes/app-service-blueprint-scaling-app-service-applications.md)]

