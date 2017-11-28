---
title: "Azure 웹 앱에 대 한 aaaApplication 성능 Faq | Microsoft Docs"
description: "가용성, 성능 및 Azure 앱 서비스의 hello 웹 응용 프로그램 기능에 대 한 응용 프로그램 문제에 대 한 질문과 대답 toofrequently를 가져옵니다."
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 7f2383743079e4c630fd548b0efd9993029afe11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="application-performance-faqs-for-web-apps-in-azure"></a><span data-ttu-id="ad8d1-103">Azure의 Web Apps에 대한 응용 프로그램 성능 FAQ</span><span class="sxs-lookup"><span data-stu-id="ad8d1-103">Application performance FAQs for Web Apps in Azure</span></span>

<span data-ttu-id="ad8d1-104">이 문서는 hello에 대 한 응용 프로그램 성능 문제에 대 한 질문과 대답 (Faq) 답변 toofrequently 되어 [Azure 앱 서비스의 웹 응용 프로그램 기능](https://azure.microsoft.com/services/app-service/web/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-104">This article has answers toofrequently asked questions (FAQs) about application performance issues for hello [Web Apps feature of Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-is-my-app-slow"></a><span data-ttu-id="ad8d1-105">내 앱이 느린 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="ad8d1-105">Why is my app slow?</span></span>

<span data-ttu-id="ad8d1-106">여러 요소로 tooslow 앱 성능 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-106">Multiple factors might contribute tooslow app performance.</span></span> <span data-ttu-id="ad8d1-107">자세한 문제 해결 단계는 [느린 웹앱 성능 문제 해결](app-service-web-troubleshoot-performance-degradation.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-107">For detailed troubleshooting steps, see [Troubleshoot slow web app performance](app-service-web-troubleshoot-performance-degradation.md).</span></span>

## <a name="how-do-i-troubleshoot-a-high-cpu-consumption-scenario"></a><span data-ttu-id="ad8d1-108">높은 CPU 사용 시나리오의 문제는 어떻게 해결하나요?</span><span class="sxs-lookup"><span data-stu-id="ad8d1-108">How do I troubleshoot a high CPU-consumption scenario?</span></span>

<span data-ttu-id="ad8d1-109">일부 높은 CPU 사용 시나리오의 경우 앱에는 실제로 더 많은 컴퓨팅 리소스가 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-109">In some high CPU-consumption scenarios, your app might truly require more computing resources.</span></span> <span data-ttu-id="ad8d1-110">이 경우 hello 응용 프로그램에 필요한 모든 hello 리소스 가져옵니다 하므로 tooa 더 높은 서비스 계층을 확장 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-110">In that case, consider scaling tooa higher service tier so hello application gets all hello resources it needs.</span></span> <span data-ttu-id="ad8d1-111">다른 경우에 높은 CPU 사용은 잘못된 반복이나 코딩 사례로 인해 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-111">Other times, high CPU consumption might be caused by a bad loop or by a coding practice.</span></span> <span data-ttu-id="ad8d1-112">CPU 사용 증가를 트리거하는 항목을 파악하는 프로세스는 두 부분으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-112">Getting insight into what's triggering increased CPU consumption is a two-part process.</span></span> <span data-ttu-id="ad8d1-113">먼저 프로세스 덤프를 만들고 hello 프로세스 덤프를 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-113">First, create a process dump, and then analyze hello process dump.</span></span> <span data-ttu-id="ad8d1-114">자세한 내용은 [Capture and analyze a dump file for high CPU consumption for Web Apps](https://blogs.msdn.microsoft.com/asiatech/2016/01/20/how-to-capture-dump-when-intermittent-high-cpu-happens-on-azure-web-app/)(Web Apps의 높은 CPU 사용에 대한 덤프 파일 캡처 및 분석)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-114">For more information, see [Capture and analyze a dump file for high CPU consumption for Web Apps](https://blogs.msdn.microsoft.com/asiatech/2016/01/20/how-to-capture-dump-when-intermittent-high-cpu-happens-on-azure-web-app/).</span></span>

## <a name="how-do-i-troubleshoot-a-high-memory-consumption-scenario"></a><span data-ttu-id="ad8d1-115">높은 메모리 사용 시나리오의 문제는 어떻게 해결하나요?</span><span class="sxs-lookup"><span data-stu-id="ad8d1-115">How do I troubleshoot a high memory-consumption scenario?</span></span>

<span data-ttu-id="ad8d1-116">일부 높은 메모리 사용 시나리오의 경우 앱에는 실제로 더 많은 컴퓨팅 리소스가 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-116">In some high memory-consumption scenarios, your app might truly require more computing resources.</span></span> <span data-ttu-id="ad8d1-117">이 경우 hello 응용 프로그램에 필요한 모든 hello 리소스 가져옵니다 하므로 tooa 더 높은 서비스 계층을 확장 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-117">In that case, consider scaling tooa higher service tier so hello application gets all hello resources it needs.</span></span> <span data-ttu-id="ad8d1-118">다른 시간 hello 코드의 버그 메모리 누수가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-118">Other times, a bug in hello code might cause a memory leak.</span></span> <span data-ttu-id="ad8d1-119">코딩 사례가 메모리 사용을 증가시킬 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-119">A coding practice also might increase memory consumption.</span></span> <span data-ttu-id="ad8d1-120">높은 메모리 사용을 트리거하는 항목을 파악하는 프로세스는 두 부분으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-120">Getting insight into what's triggering high memory consumption is a two-part process.</span></span> <span data-ttu-id="ad8d1-121">먼저 프로세스 덤프를 만들고 hello 프로세스 덤프를 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-121">First, create a process dump, and then analyze hello process dump.</span></span> <span data-ttu-id="ad8d1-122">Hello Azure 사이트 확장 갤러리에서에서 충돌 진단 도구 모두 다음이 단계를 효율적으로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-122">Crash Diagnoser from hello Azure Site Extension Gallery can efficiently perform both these steps.</span></span> <span data-ttu-id="ad8d1-123">자세한 내용은 [Capture and analyze a dump file for intermittent high memory for Web Apps](https://blogs.msdn.microsoft.com/asiatech/2016/02/02/how-to-capture-and-analyze-dump-for-intermittent-high-memory-on-azure-web-app/)(Web Apps의 간헐적 높은 메모리에 대한 덤프 파일 캡처 및 분석)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-123">For more information, see [Capture and analyze a dump file for intermittent high memory for Web Apps](https://blogs.msdn.microsoft.com/asiatech/2016/02/02/how-to-capture-and-analyze-dump-for-intermittent-high-memory-on-azure-web-app/).</span></span>

## <a name="how-do-i-automate-app-service-web-apps-by-using-powershell"></a><span data-ttu-id="ad8d1-124">PowerShell를 사용하여 App Service Web Apps를 어떻게 자동화할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="ad8d1-124">How do I automate App Service web apps by using PowerShell?</span></span>

<span data-ttu-id="ad8d1-125">PowerShell cmdlet toomanage를 사용할 수 있으며 앱 서비스 웹 앱을 유지 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-125">You can use PowerShell cmdlets toomanage and maintain App Service web apps.</span></span> <span data-ttu-id="ad8d1-126">이라는 블로그 게시물에서 [PowerShell을 사용 하 여 Azure 앱 서비스에서 호스팅되는 웹 응용 프로그램을 자동화](https://blogs.msdn.microsoft.com/puneetgupta/2016/03/21/automating-webapps-hosted-in-azure-app-service-through-powershell-arm-way/), 설명 방법을 toouse Azure 리소스 관리자 기반 PowerShell cmdlet tooautomate 일반적인 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-126">In our blog post [Automate web apps hosted in Azure App Service by using PowerShell](https://blogs.msdn.microsoft.com/puneetgupta/2016/03/21/automating-webapps-hosted-in-azure-app-service-through-powershell-arm-way/), we describe how toouse Azure Resource Manager-based PowerShell cmdlets tooautomate common tasks.</span></span> <span data-ttu-id="ad8d1-127">hello 블로그 게시물에는 다음과 같은 다양 한 웹 앱 관리 작업에 대 한 샘플 코드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-127">hello blog post also has sample code for various web apps management tasks.</span></span> <span data-ttu-id="ad8d1-128">모든 App Service Web Apps cmdlet에 대한 설명과 구문은 [AzureRM.Websites](https://docs.microsoft.com/powershell/module/azurerm.websites/?view=azurermps-4.0.0)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-128">For descriptions and syntax for all App Service web apps cmdlets, see [AzureRM.Websites](https://docs.microsoft.com/powershell/module/azurerm.websites/?view=azurermps-4.0.0).</span></span>

## <a name="how-do-i-view-my-web-apps-event-logs"></a><span data-ttu-id="ad8d1-129">내 웹앱의 이벤트 로그는 어떻게 볼 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="ad8d1-129">How do I view my web app's event logs?</span></span>

<span data-ttu-id="ad8d1-130">tooview 웹 앱의 이벤트를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-130">tooview your web app's event logs:</span></span>

1. <span data-ttu-id="ad8d1-131">Tooyour 로그인 [Kudu 웹 사이트](https://*yourwebsitename*.scm.azurewebsites.net)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-131">Sign in tooyour [Kudu website](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
2. <span data-ttu-id="ad8d1-132">Hello 메뉴에서 선택 **디버그 콘솔** > **CMD**합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-132">In hello menu, select **Debug Console** > **CMD**.</span></span>
3. <span data-ttu-id="ad8d1-133">선택 hello **LogFiles** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-133">Select hello **LogFiles** folder.</span></span>
4. <span data-ttu-id="ad8d1-134">tooview 이벤트 로그 선택 hello 연필 아이콘 옆 너무**eventlog.xml**합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-134">tooview event logs, select hello pencil icon next too**eventlog.xml**.</span></span>
5. <span data-ttu-id="ad8d1-135">hello PowerShell cmdlet을 실행 하는 toodownload hello 로그 `Save-AzureWebSiteLog -Name webappname`합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-135">toodownload hello logs, run hello PowerShell cmdlet `Save-AzureWebSiteLog -Name webappname`.</span></span>

## <a name="how-do-i-capture-a-user-mode-memory-dump-of-my-web-app"></a><span data-ttu-id="ad8d1-136">내 웹앱의 사용자 모드 메모리 덤프는 어떻게 캡처할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="ad8d1-136">How do I capture a user-mode memory dump of my web app?</span></span>

<span data-ttu-id="ad8d1-137">웹 응용 프로그램의 사용자 모드 메모리 덤프 toocapture:</span><span class="sxs-lookup"><span data-stu-id="ad8d1-137">toocapture a user-mode memory dump of your web app:</span></span>

1. <span data-ttu-id="ad8d1-138">Tooyour 로그인 [Kudu 웹 사이트](https://*yourwebsitename*.scm.azurewebsites.net)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-138">Sign in tooyour [Kudu website](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
2. <span data-ttu-id="ad8d1-139">선택 hello **프로세스 탐색기** 메뉴.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-139">Select hello **Process Explorer** menu.</span></span>
3. <span data-ttu-id="ad8d1-140">마우스 오른쪽 단추로 클릭 hello **w3wp.exe** 프로세스 또는 WebJob 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-140">Right-click hello **w3wp.exe** process or your WebJob process.</span></span>
4. <span data-ttu-id="ad8d1-141">**Download Memory Dump**(메모리 덤프 다운로드) > **Full Dump**(전체 덤프)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-141">Select **Download Memory Dump** > **Full Dump**.</span></span>

## <a name="how-do-i-view-process-level-info-for-my-web-app"></a><span data-ttu-id="ad8d1-142">내 웹앱의 프로세스 수준 정보는 어떻게 볼 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="ad8d1-142">How do I view process-level info for my web app?</span></span>

<span data-ttu-id="ad8d1-143">웹앱에 대한 프로세스 수준 정보를 보는 데는 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-143">You have two options for viewing process-level information for your web app:</span></span>

*   <span data-ttu-id="ad8d1-144">Azure 포털 hello에서:</span><span class="sxs-lookup"><span data-stu-id="ad8d1-144">In hello Azure portal:</span></span>
    1. <span data-ttu-id="ad8d1-145">열기 hello **프로세스 탐색기** hello 웹 앱에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-145">Open hello **Process Explorer** for hello web app.</span></span>
    2. <span data-ttu-id="ad8d1-146">toosee hello 세부 정보 선택 hello **w3wp.exe** 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-146">toosee hello details, select hello **w3wp.exe** process.</span></span>
*   <span data-ttu-id="ad8d1-147">Hello Kudu 콘솔:</span><span class="sxs-lookup"><span data-stu-id="ad8d1-147">In hello Kudu console:</span></span>
    1. <span data-ttu-id="ad8d1-148">Tooyour 로그인 [Kudu 웹 사이트](https://*yourwebsitename*.scm.azurewebsites.net)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-148">Sign in tooyour [Kudu website](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
    2. <span data-ttu-id="ad8d1-149">선택 hello **프로세스 탐색기** 메뉴.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-149">Select hello **Process Explorer** menu.</span></span>
    3. <span data-ttu-id="ad8d1-150">Hello에 대 한 **w3wp.exe** 프로세스를 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-150">For hello **w3wp.exe** process, select **Properties**.</span></span>

## <a name="when-i-browse-toomy-app-i-see-error-403---this-web-app-is-stopped-how-do-i-resolve-this"></a><span data-ttu-id="ad8d1-151">"오류 403-웹 앱이 중지 되었습니다." 참조 toomy 응용 프로그램을 검색 하는 경우</span><span class="sxs-lookup"><span data-stu-id="ad8d1-151">When I browse toomy app, I see "Error 403 - This web app is stopped."</span></span> <span data-ttu-id="ad8d1-152">이 문제를 해결하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="ad8d1-152">How do I resolve this?</span></span>

<span data-ttu-id="ad8d1-153">이 오류는 세 가지 조건으로 인해 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-153">Three conditions can cause this error:</span></span>

* <span data-ttu-id="ad8d1-154">hello 웹 앱에는 청구 제한에 도달 했습니다 및 사이트가 비활성화 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-154">hello web app has reached a billing limit and your site has been disabled.</span></span>
* <span data-ttu-id="ad8d1-155">웹 앱 hello hello 포털에서 중지 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-155">hello web app has been stopped in hello portal.</span></span>
* <span data-ttu-id="ad8d1-156">웹 앱 hello tooa 무료 또는 공유 규모 서비스 계획 적용 될 수 있는 리소스 할당량 한도 도달 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-156">hello web app has reached a resource quota limit that might apply tooa Free or Shared scale service plan.</span></span>

<span data-ttu-id="ad8d1-157">toosee의 단계를 hello 오류 및 tooresolve hello 문제, 따라 hello 원인을 [웹 앱: "오류 403-이 웹 앱이 중지 되었습니다."](https://blogs.msdn.microsoft.com/waws/2016/01/05/azure-web-apps-error-403-this-web-app-is-stopped/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-157">toosee what is causing hello error and tooresolve hello issue, follow hello steps in [Web Apps: "Error 403 – This web app is stopped"](https://blogs.msdn.microsoft.com/waws/2016/01/05/azure-web-apps-error-403-this-web-app-is-stopped/).</span></span>

## <a name="where-can-i-learn-more-about-quotas-and-limits-for-various-app-service-plans"></a><span data-ttu-id="ad8d1-158">다양한 App Service 계획의 할당량 및 한도에 대한 자세한 내용은 어디서 알아볼 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="ad8d1-158">Where can I learn more about quotas and limits for various App Service plans?</span></span>

<span data-ttu-id="ad8d1-159">할당량 및 한도에 대한 자세한 내용은 [App Service 한도](../azure-subscription-service-limits.md#app-service-limits)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-159">For information about quotas and limits, see [App Service limits](../azure-subscription-service-limits.md#app-service-limits).</span></span> 

## <a name="how-do-i-decrease-hello-response-time-for-hello-first-request-after-idle-time"></a><span data-ttu-id="ad8d1-160">유휴 시간 후 hello 첫 번째 요청에 대 한 hello 응답 시간을 줄일 하는 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="ad8d1-160">How do I decrease hello response time for hello first request after idle time?</span></span>

<span data-ttu-id="ad8d1-161">기본적으로 웹앱은 일정 기간 유휴 상태인 경우 언로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-161">By default, web apps are unloaded if they are idle for a set period of time.</span></span> <span data-ttu-id="ad8d1-162">이러한 방식으로 hello 시스템 리소스를 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-162">This way, hello system can conserve resources.</span></span> <span data-ttu-id="ad8d1-163">hello 단점은 hello 응답 toohello 첫 번째 요청이 hello 웹 응용 프로그램 로드 된 후 깁니다, tooallow 웹 응용 프로그램 tooload hello 및 응답을 처리 하는 시작입니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-163">hello downside is that hello response toohello first request after hello web app is unloaded is longer, tooallow hello web app tooload and start serving responses.</span></span> <span data-ttu-id="ad8d1-164">기본 및 표준 서비스 계획에서 설정할 수 있습니다 hello **Always On** 설정 tookeep hello 앱을 항상 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-164">In Basic and Standard service plans, you can turn on hello **Always On** setting tookeep hello app always loaded.</span></span> <span data-ttu-id="ad8d1-165">이렇게 하면 로드 시간이 더 hello 앱이 유휴 상태 후 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-165">This eliminates longer load times after hello app is idle.</span></span> <span data-ttu-id="ad8d1-166">toochange hello **Always On** 설정:</span><span class="sxs-lookup"><span data-stu-id="ad8d1-166">toochange hello **Always On** setting:</span></span>

1. <span data-ttu-id="ad8d1-167">Azure 포털 hello tooyour 웹 응용 프로그램을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-167">In hello Azure portal, go tooyour web app.</span></span>
2. <span data-ttu-id="ad8d1-168">**응용 프로그램 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-168">Select **Application settings**.</span></span>
3. <span data-ttu-id="ad8d1-169">**무중단**에 대해 **켜기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-169">For **Always On**, select **On**.</span></span>

## <a name="how-do-i-turned-on-failed-request-tracing"></a><span data-ttu-id="ad8d1-170">실패한 요청 추적을 어떻게 켰나요?</span><span class="sxs-lookup"><span data-stu-id="ad8d1-170">How do I turned on failed request tracing?</span></span>

<span data-ttu-id="ad8d1-171">실패 한 요청 추적에 tooturn:</span><span class="sxs-lookup"><span data-stu-id="ad8d1-171">tooturn on failed request tracing:</span></span>

1. <span data-ttu-id="ad8d1-172">Azure 포털 hello tooyour 웹 응용 프로그램을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-172">In hello Azure portal, go tooyour web app.</span></span>
3. <span data-ttu-id="ad8d1-173">**모든 설정** > **진단 로그**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-173">Select **All Settings** > **Diagnostics Logs**.</span></span>
4. <span data-ttu-id="ad8d1-174">**실패한 요청 추적**에 대해 **켜기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-174">For **Failed Request Tracing**, select **On**.</span></span>
5. <span data-ttu-id="ad8d1-175">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-175">Select **Save**.</span></span>
6. <span data-ttu-id="ad8d1-176">Hello 웹 앱 블레이드 선택 **도구**합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-176">On hello web app blade, select **Tools**.</span></span>
7. <span data-ttu-id="ad8d1-177">**Visual Studio Online**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-177">Select **Visual Studio Online**.</span></span>
8. <span data-ttu-id="ad8d1-178">Hello 설정이 되지 않은 경우 **에**선택, **에**합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-178">If hello setting is not **On**, select **On**.</span></span>
9. <span data-ttu-id="ad8d1-179">**이동**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-179">Select **Go**.</span></span>
10. <span data-ttu-id="ad8d1-180">**Web.config**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-180">Select **Web.config**.</span></span>
11. <span data-ttu-id="ad8d1-181">System.webServer,이 구성은 (toocapture 특정 URL)를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-181">In system.webServer, add this configuration (toocapture a specific URL):</span></span>

    ```
    <system.webServer>
    <tracing> <traceFailedRequests>
    <remove path="*api*" />
    <add path="*api*">
    <traceAreas>
    <add provider="ASP" verbosity="Verbose" />
    <add provider="ASPNET" areas="Infrastructure,Module,Page,AppServices" verbosity="Verbose" />
    <add provider="ISAPI Extension" verbosity="Verbose" />
    <add provider="WWW Server" areas="Authentication,Security,Filter,StaticFile,CGI,Compression, Cache,RequestNotifications,Module,FastCGI" verbosity="Verbose" />
    </traceAreas>
    <failureDefinitions statusCodes="200-999" />
    </add> </traceFailedRequests>
    </tracing>
    ```
12. <span data-ttu-id="ad8d1-182">tootroubleshoot 속도가 느린 성능 문제를 (hello 캡처 요청에는 30 초 이상 소요 되) 하는 경우이 구성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-182">tootroubleshoot slow-performance issues, add this configuration (if hello capturing request is taking more than 30 seconds):</span></span>
    ```
    <system.webServer>
    <tracing> <traceFailedRequests>
    <remove path="*" />
    <add path="*">
    <traceAreas> <add provider="ASP" verbosity="Verbose" />
    <add provider="ASPNET" areas="Infrastructure,Module,Page,AppServices" verbosity="Verbose" />
    <add provider="ISAPI Extension" verbosity="Verbose" />
    <add provider="WWW Server" areas="Authentication,Security,Filter,StaticFile,CGI,Compression, Cache,RequestNotifications,Module,FastCGI" verbosity="Verbose" />
    </traceAreas>
    <failureDefinitions timeTaken="00:00:30" statusCodes="200-999" />
    </add> </traceFailedRequests>
    </tracing>
    ```
13. <span data-ttu-id="ad8d1-183">toodownload hello 실패 요청 추적을 hello [포털](https://portal.azure.com)이동, tooyour 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-183">toodownload hello failed request traces, in hello [portal](https://portal.azure.com), go tooyour website.</span></span>
15. <span data-ttu-id="ad8d1-184">**도구** > **Kudu** > **이동**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-184">Select **Tools** > **Kudu** > **Go**.</span></span>
18. <span data-ttu-id="ad8d1-185">Hello 메뉴에서 선택 **디버그 콘솔** > **CMD**합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-185">In hello menu, select **Debug Console** > **CMD**.</span></span>
19. <span data-ttu-id="ad8d1-186">선택 hello **LogFiles** 폴더 및로 시작 하는 이름으로 선택한 후 hello 폴더 **W3SVC**합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-186">Select hello **LogFiles** folder, and then select hello folder with a name that starts with **W3SVC**.</span></span>
20. <span data-ttu-id="ad8d1-187">toosee hello XML 파일 선택 hello 연필 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-187">toosee hello XML file, select hello pencil icon.</span></span>

## <a name="i-see-hello-message-worker-process-requested-recycle-due-toopercent-memory-limit-how-do-i-address-this-issue"></a><span data-ttu-id="ad8d1-188">Hello 메시지 표시 "작업자 프로세스가 재생을 요청 due too'Percent 메모리 ' 제한 합니다."</span><span class="sxs-lookup"><span data-stu-id="ad8d1-188">I see hello message "Worker Process requested recycle due too'Percent Memory' limit."</span></span> <span data-ttu-id="ad8d1-189">이 문제를 어떻게 해결하나요?</span><span class="sxs-lookup"><span data-stu-id="ad8d1-189">How do I address this issue?</span></span>

<span data-ttu-id="ad8d1-190">hello 사용 가능한 메모리의 최대 크기는 32 비트 프로세스에 대 한 (64 비트 운영 체제) 에서도 2GB입니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-190">hello maximum available amount of memory for a 32-bit process (even on a 64-bit operating system) is 2 GB.</span></span> <span data-ttu-id="ad8d1-191">기본적으로 hello 작업자 프로세스가 too32 비트 앱 서비스에서 (레거시 웹 응용 프로그램과 호환성)에 대 한 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-191">By default, hello worker process is set too32-bit in App Service (for compatibility with legacy web applications).</span></span>

<span data-ttu-id="ad8d1-192">웹 작업자 역할에서 사용할 수 있는 추가 메모리 hello 수 있도록 too64 비트 프로세스를 전환 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-192">Consider switching too64-bit processes so you can take advantage of hello additional memory available in your Web Worker role.</span></span> <span data-ttu-id="ad8d1-193">이렇게 하면 웹앱 다시 시작이 트리거되므로 이에 따라 일정이 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-193">This triggers a web app restart, so schedule accordingly.</span></span>

<span data-ttu-id="ad8d1-194">또한 64비트 환경에는 기본 또는 표준 서비스 계획이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-194">Also note that a 64-bit environment requires a Basic or Standard service plan.</span></span> <span data-ttu-id="ad8d1-195">무료 및 공유 계획은 항상 32비트 환경에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-195">Free and Shared plans always run in a 32-bit environment.</span></span>

<span data-ttu-id="ad8d1-196">자세한 내용은 [Azure 앱 서비스에서 웹 앱 구성](https://docs.microsoft.com/azure/app-service-web/web-sites-configure)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-196">For more information, see [Configure web apps in App Service](https://docs.microsoft.com/azure/app-service-web/web-sites-configure).</span></span>

## <a name="why-does-my-request-time-out-after-240-seconds"></a><span data-ttu-id="ad8d1-197">240초 후 요청 시간이 초과되는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="ad8d1-197">Why does my request time out after 240 seconds?</span></span>

<span data-ttu-id="ad8d1-198">Azure Load Balancer에는 4분의 기본 유휴 시간 제한 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-198">Azure Load Balancer has a default idle timeout setting of four minutes.</span></span> <span data-ttu-id="ad8d1-199">이 설정은 일반적으로 웹 요청에 대한 합리적인 응답 시간 제한입니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-199">This is generally a reasonable response time limit for a web request.</span></span> <span data-ttu-id="ad8d1-200">웹앱에 백그라운드 처리가 필요한 경우 Azure WebJobs를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-200">If your web app requires background processing, we recommend using Azure WebJobs.</span></span> <span data-ttu-id="ad8d1-201">hello Azure 웹 앱 WebJobs를 호출할 수 있습니다 및 백그라운드 처리가 완료 될 때 알림을 받으려면 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-201">hello Azure web app can call WebJobs and be notified when background processing is finished.</span></span> <span data-ttu-id="ad8d1-202">큐 및 트리거를 포함하여 WebJobs를 사용하기 위한 여러 방법 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-202">You can choose from multiple methods for using WebJobs, including queues and triggers.</span></span>

<span data-ttu-id="ad8d1-203">WebJobs는 백그라운드에서 처리되도록 디자인됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-203">WebJobs is designed for background processing.</span></span> <span data-ttu-id="ad8d1-204">WebJob에서 원하는 만큼 백그라운드 처리를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-204">You can do as much background processing as you want in a WebJob.</span></span> <span data-ttu-id="ad8d1-205">WebJobs에 대한 자세한 내용은 [WebJob으로 백그라운드 작업 실행](https://docs.microsoft.com/azure/app-service-web/web-sites-create-web-jobs)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-205">For more information about WebJobs, see [Run background tasks with WebJobs](https://docs.microsoft.com/azure/app-service-web/web-sites-create-web-jobs).</span></span>

## <a name="aspnet-core-applications-that-are-hosted-in-app-service-sometimes-stop-responding-how-do-i-fix-this-issue"></a><span data-ttu-id="ad8d1-206">App Service에서 호스트되는 ASP.NET Core 응용 프로그램이 때때로 응답을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-206">ASP.NET Core applications that are hosted in App Service sometimes stop responding.</span></span> <span data-ttu-id="ad8d1-207">이 문제를 어떻게 해결하나요?</span><span class="sxs-lookup"><span data-stu-id="ad8d1-207">How do I fix this issue?</span></span>

<span data-ttu-id="ad8d1-208">이전 알려진된 문제로 [Kestrel 버전](https://github.com/aspnet/KestrelHttpServer/issues/1182) toointermittently 중지 응답 앱 서비스에서 호스팅되는 ASP.NET Core 1.0 응용 프로그램을 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-208">A known issue with an earlier [Kestrel version](https://github.com/aspnet/KestrelHttpServer/issues/1182) might cause an ASP.NET Core 1.0 app that's hosted in App Service toointermittently stop responding.</span></span> <span data-ttu-id="ad8d1-209">이 메시지가 표시 될 수 있습니다: "hello" 지정 된 CGI 응용 프로그램 오류 및 hello 종료 서버 hello 프로세스에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-209">You also might see this message: "hello specified CGI Application encountered an error and hello server terminated hello process."</span></span>

<span data-ttu-id="ad8d1-210">이 문제는 Kestrel 버전 1.0.2에서 해결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-210">This issue is fixed in Kestrel version 1.0.2.</span></span> <span data-ttu-id="ad8d1-211">이 버전은 hello ASP.NET Core 1.0.3 업데이트에에서 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-211">This version is included in hello ASP.NET Core 1.0.3 update.</span></span> <span data-ttu-id="ad8d1-212">tooresolve이 문제를 응용 프로그램 종속성 toouse Kestrel 1.0.2 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-212">tooresolve this issue, make sure you update your app dependencies toouse Kestrel 1.0.2.</span></span> <span data-ttu-id="ad8d1-213">Hello 블로그 게시물에 설명 되어 있는 두 가지 해결 방법 중 하나를 사용할 수 또는 [앱 서비스 웹 응용 프로그램에서 ASP.NET Core 1.0 느린 성능 문제](https://blogs.msdn.microsoft.com/waws/2016/12/11/asp-net-core-slow-perf-issues-on-azure-websites)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-213">Alternatively, you can use one of two workarounds that are described in hello blog post [ASP.NET Core 1.0 slow perf issues in App Service web apps](https://blogs.msdn.microsoft.com/waws/2016/12/11/asp-net-core-slow-perf-issues-on-azure-websites).</span></span>


## <a name="i-cant-find-my-log-files-in-hello-file-structure-of-my-web-app-how-can-i-find-them"></a><span data-ttu-id="ad8d1-214">웹 응용 프로그램의 hello 파일 구조에서 로그 파일 내 없을 때</span><span class="sxs-lookup"><span data-stu-id="ad8d1-214">I can't find my log files in hello file structure of my web app.</span></span> <span data-ttu-id="ad8d1-215">어떻게 찾을 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="ad8d1-215">How can I find them?</span></span>

<span data-ttu-id="ad8d1-216">앱 서비스의 hello 로컬 캐시 기능을 사용 하 여 hello 로그 파일의 hello 폴더 구조 및 데이터 폴더 응용 프로그램 서비스 인스턴스에 대 한 영향을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-216">If you use hello Local Cache feature of App Service, hello folder structure of hello LogFiles and Data folders for your App Service instance are affected.</span></span> <span data-ttu-id="ad8d1-217">로컬 캐시를 사용 하면 하위 폴더는 hello 저장소 로그 파일 및 데이터 폴더에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-217">When Local Cache is used, subfolders are created in hello storage LogFiles and Data folders.</span></span> <span data-ttu-id="ad8d1-218">hello 하위 폴더 사용 이름 지정 패턴 "고유 식별자" + 타임 스탬프 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-218">hello subfolders use hello naming pattern "unique identifier" + time stamp.</span></span> <span data-ttu-id="ad8d1-219">각 하위 폴더는 hello에 웹 앱이 실행 중이거나 실행 tooa VM 인스턴스를 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-219">Each subfolder corresponds tooa VM instance in which hello web app is running or has run.</span></span>

<span data-ttu-id="ad8d1-220">toodetermine 로컬 캐시를 사용 하는 여부 확인 앱 서비스 **응용 프로그램 설정** 탭 합니다. 로컬 캐시를 사용 하는 경우 앱 설정 hello `WEBSITE_LOCAL_CACHE_OPTION` 너무 설정`Always`합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-220">toodetermine whether you are using Local Cache, check your App Service **Application settings** tab. If Local Cache is being used, hello app setting `WEBSITE_LOCAL_CACHE_OPTION` is set too`Always`.</span></span> <span data-ttu-id="ad8d1-221">로컬 캐시에 대 한 자세한 내용은 참조 hello [응용 프로그램 서비스 로컬 캐시 개요](https://docs.microsoft.com/azure/app-service/app-service-local-cache)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-221">For more information about Local Cache, see hello [App Service Local Cache overview](https://docs.microsoft.com/azure/app-service/app-service-local-cache).</span></span>

<span data-ttu-id="ad8d1-222">로컬 캐시를 사용하고 있지 않고 이 문제가 발생하지 않으면 지원 요청을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-222">If you are not using Local Cache and are experiencing this issue, submit a support request.</span></span>

## <a name="i-see-hello-message-an-attempt-was-made-tooaccess-a-socket-in-a-way-forbidden-by-its-access-permissions-how-do-i-resolve-this"></a><span data-ttu-id="ad8d1-223">Hello 메시지 표시 "시도 된 tooaccess 소켓 액세스 권한에 의해 방식으로 수행 합니다."</span><span class="sxs-lookup"><span data-stu-id="ad8d1-223">I see hello message "An attempt was made tooaccess a socket in a way forbidden by its access permissions."</span></span> <span data-ttu-id="ad8d1-224">이 문제를 해결하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="ad8d1-224">How do I resolve this?</span></span>

<span data-ttu-id="ad8d1-225">이 오류는 일반적으로 hello hello VM 인스턴스에서 아웃 바운드 TCP 연결을 사용 하는 경우에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-225">This error typically occurs if hello outbound TCP connections on hello VM instance are exhausted.</span></span> <span data-ttu-id="ad8d1-226">앱 서비스에서 각 VM 인스턴스에 대해 설정할 수 있는 아웃 바운드 연결의 최대 수 hello에 대 한 한도가 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-226">In App Service, limits are enforced for hello maximum number of outbound connections that can be made for each VM instance.</span></span> <span data-ttu-id="ad8d1-227">자세한 내용은 [Cross-VM numerical limits](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox#cross-vm-numerical-limits)(VM 간 숫자 제한)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-227">For more information, see [Cross-VM numerical limits](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox#cross-vm-numerical-limits).</span></span>

<span data-ttu-id="ad8d1-228">또한이 오류 응용 프로그램에서 tooaccess 로컬 주소를 시도 하는 경우에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-228">This error also might occur if you try tooaccess a local address from your application.</span></span> <span data-ttu-id="ad8d1-229">자세한 내용은 [Local address requests](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox#local-address-requests)(로컬 주소 요청)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-229">For more information, see [Local address requests](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox#local-address-requests).</span></span>

<span data-ttu-id="ad8d1-230">웹 앱의 아웃 바운드 연결에 대 한 자세한 내용은 hello 블로그에 대 한 게시물을 참조 하십시오. [연결 tooAzure 웹 사이트를 나가는](http://www.freekpaans.nl/2015/08/starving-outgoing-connections-on-windows-azure-web-sites/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-230">For more information about outbound connections in your web app, see hello blog post about [outgoing connections tooAzure websites](http://www.freekpaans.nl/2015/08/starving-outgoing-connections-on-windows-azure-web-sites/).</span></span>

## <a name="how-do-i-use-visual-studio-tooremote-debug-my-app-service-web-app"></a><span data-ttu-id="ad8d1-231">Visual Studio tooremote 디버그 앱 서비스 웹 응용 프로그램으로 사용 방법</span><span class="sxs-lookup"><span data-stu-id="ad8d1-231">How do I use Visual Studio tooremote debug my App Service web app?</span></span>

<span data-ttu-id="ad8d1-232">Visual Studio를 사용 하 여 웹 응용 프로그램 참조 하는 toodebug 방법을 보여 주는 자세한 연습은 [앱 서비스 웹 앱을 디버그 하는 원격](https://blogs.msdn.microsoft.com/benjaminperkins/2016/09/22/remote-debug-your-azure-app-service-web-app/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad8d1-232">For a detailed walkthrough that shows you how toodebug your web app by using Visual Studio, see [Remote debug your App Service web app](https://blogs.msdn.microsoft.com/benjaminperkins/2016/09/22/remote-debug-your-azure-app-service-web-app/).</span></span>
