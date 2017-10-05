---
title: "Azure Mobile Engagement 앱 만들기 | Microsoft Docs"
description: "Azure에서 새 Mobile Engagement 앱 컬렉션을 만들고 Mobile Engagement 포털을 사용하여 앱을 관리하기 시작하는 방법을 설명합니다."
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: b8aa1798-28c6-424c-a5b5-8a264d5a0ff0
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/10/2016
ms.author: piyushjo
ms.openlocfilehash: 47c1e122f6f38654cd63bb59e50e68803f76c83d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-mobile-engagement-app"></a><span data-ttu-id="29e5e-103">Azure Mobile Engagement 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="29e5e-103">Create an Azure Mobile Engagement App</span></span>
<span data-ttu-id="29e5e-104">이 문서에서는 **빨리 만들기** 메서드를 사용하여 새 **Azure Mobile Engagement** 앱을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="29e5e-104">This article shows how to use the **Quick Create** method to create a new **Azure Mobile Engagement** App.</span></span> <span data-ttu-id="29e5e-105">또한 문서는 앱을 모니터링하고 관리하기 위해 **Mobile Engagement** 포털을 탐색하는 방법도 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="29e5e-105">The article also shows how to navigate to your **Mobile Engagement** portal in order to start monitoring and managing your apps.</span></span> 

<span data-ttu-id="29e5e-106">앱에 대한 데이터를 수집하고 푸시 알림을 보낼 수 있기 위해 "기본 통합"의 최소 집합을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29e5e-106">Note that you must add a minimum set of "basic integration" in order to be able to collect data for your app and send push notifications.</span></span> <span data-ttu-id="29e5e-107">전체 통합 설명서는 [Mobile Engagement 통합](mobile-engagement-windows-store-integrate-engagement.md)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29e5e-107">The complete integration documentation can be found in the [Mobile Engagement integration](mobile-engagement-windows-store-integrate-engagement.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="29e5e-108">Azure Mobile Engagement 자습서를 완료하려면 활성 Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29e5e-108">To complete any Azure Mobile Engagement tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="29e5e-109">계정이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29e5e-109">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="29e5e-110">자세한 내용은 <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fwww.windowsazure.com%2Fen-us%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure 무료 평가판</a>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="29e5e-110">For details, see <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fwww.windowsazure.com%2Fen-us%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

## <a name="setup-mobile-engagement-for-your-mobile-app-in-azure"></a><span data-ttu-id="29e5e-111">Azure에서 모바일 앱용 Mobile Engagement 설정</span><span class="sxs-lookup"><span data-stu-id="29e5e-111">Setup Mobile Engagement for your mobile app in Azure</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a name="navigate-to-your-mobile-engagement-portal"></a><span data-ttu-id="29e5e-112">Mobile Engagement 포털로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="29e5e-112">Navigate to your Mobile Engagement portal</span></span>
<span data-ttu-id="29e5e-113">응용 프로그램을 모니터링하고 관리하기 시작하려면 위쪽 막대에서 **Engagement 포털** 단추를 클릭하여 Mobile Engagement 포털로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="29e5e-113">To start monitoring and managing your application, navigate to your Mobile Engagement portal by clicking the **Engagement portal** button in the top bar.</span></span>

<span data-ttu-id="29e5e-114">Mobile Engagement 포털에 위치하게 되면 세그먼트를 분석, 생성 및 관리하고 사용자에게 도달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29e5e-114">Once you are in the  Mobile Engagement portal, you can analyze, create and manage segments, reach out to the users, etc.:</span></span>    

* [<span data-ttu-id="29e5e-115">응용 프로그램에 대한 실시간 데이터 모니터링</span><span class="sxs-lookup"><span data-stu-id="29e5e-115">Monitor real time data about your application</span></span>](mobile-engagement-user-interface-monitor.md)
* [<span data-ttu-id="29e5e-116">응용 프로그램에 대한 기록 데이터 분석</span><span class="sxs-lookup"><span data-stu-id="29e5e-116">Analyze historical data about your application</span></span>](mobile-engagement-user-interface-analytics.md)
* [<span data-ttu-id="29e5e-117">사용자의 세그먼트를 만들고 관리하여 사용 패턴 식별</span><span class="sxs-lookup"><span data-stu-id="29e5e-117">Create and manage segments of users to identify usage patterns</span></span>](mobile-engagement-user-interface-segments.md)
* [<span data-ttu-id="29e5e-118">푸시 알림으로 응용 프로그램의 사용자에게 알림</span><span class="sxs-lookup"><span data-stu-id="29e5e-118">Reach out to the users of your application with push notifications</span></span>](mobile-engagement-user-interface-reach.md)

## <a name="see-also"></a><span data-ttu-id="29e5e-119">참고 항목</span><span class="sxs-lookup"><span data-stu-id="29e5e-119">See Also</span></span>
[<span data-ttu-id="29e5e-120">Mobile Engagement 전략 정의</span><span class="sxs-lookup"><span data-stu-id="29e5e-120">Define your Mobile Engagement strategy</span></span>](mobile-engagement-define-your-mobile-engagement-strategy.md)

<span data-ttu-id="29e5e-121">[Azure Mobile Engagement 시작](mobile-engagement-windows-store-dotnet-get-started.md) (페이지 맨 위에 있는 다른 모바일 플랫폼을 선택할 수 있습니다)</span><span class="sxs-lookup"><span data-stu-id="29e5e-121">[Get started with Azure Mobile Engagement](mobile-engagement-windows-store-dotnet-get-started.md) (you can select other mobile platforms at the top of the page).</span></span>

