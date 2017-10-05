---
title: "Azure Application Insights 내 Analytics 문제 해결 | Microsoft Docs"
description: "Application Insights Analytics에 문제가 있습니까? 여기에서 시작합니다. "
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 9bbd5859-3584-4d80-9b6d-d5910fa48baa
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/11/2016
ms.author: bwren
ms.openlocfilehash: 02df117908fc1790e8cfb9ec0a7218c1b8be856c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-analytics-in-application-insights"></a><span data-ttu-id="ee885-104">Application Insights의 Analytics 문제 해결</span><span class="sxs-lookup"><span data-stu-id="ee885-104">Troubleshoot Analytics in Application Insights</span></span>
<span data-ttu-id="ee885-105">[Application Insights Analytics](app-insights-analytics.md)에 문제가 있습니까?</span><span class="sxs-lookup"><span data-stu-id="ee885-105">Problems with [Application Insights Analytics](app-insights-analytics.md)?</span></span> <span data-ttu-id="ee885-106">여기에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ee885-106">Start here.</span></span> <span data-ttu-id="ee885-107">Analytics는 Azure Application Insights의 강력한 검색 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="ee885-107">Analytics is the powerful search tool of Azure Application Insights.</span></span>

## <a name="limits"></a><span data-ttu-id="ee885-108">제한</span><span class="sxs-lookup"><span data-stu-id="ee885-108">Limits</span></span>
* <span data-ttu-id="ee885-109">현재, 쿼리 결과는 지난 주의 데이터로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee885-109">At present, query results are limited to just over a week of past data.</span></span>
* <span data-ttu-id="ee885-110">테스트 브라우저: Chrome, Edge 및 Internet Explorer 최신 버전.</span><span class="sxs-lookup"><span data-stu-id="ee885-110">Browsers we test on: latest editions of Chrome, Edge, and Internet Explorer.</span></span>

## <a name="known-incompatible-browser-extensions"></a><span data-ttu-id="ee885-111">알려진 호환되지 않는 브라우저 확장</span><span class="sxs-lookup"><span data-stu-id="ee885-111">Known incompatible browser extensions</span></span>
* <span data-ttu-id="ee885-112">Ghostery</span><span class="sxs-lookup"><span data-stu-id="ee885-112">Ghostery</span></span>

<span data-ttu-id="ee885-113">확장을 사용하지 않도록 설정하거나 다른 브라우저를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ee885-113">Disable the extension or use a different browser.</span></span>

## <span data-ttu-id="ee885-114"><a name="e-a"></a> "예기치 않은 오류"</span><span class="sxs-lookup"><span data-stu-id="ee885-114"><a name="e-a"></a> "Unexpected error"</span></span>
![예기치 않은 오류 화면](./media/app-insights-analytics-troubleshooting/010.png)

<span data-ttu-id="ee885-116">포털 런타임에 내부 오류 발생 – 처리되지 않은 예외.</span><span class="sxs-lookup"><span data-stu-id="ee885-116">Internal error occurred during portal runtime – unhandled exception.</span></span>

* <span data-ttu-id="ee885-117">브라우저의 캐시를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="ee885-117">Clean the browser's cache.</span></span> 

## <span data-ttu-id="ee885-118"><a name="e-b"></a>403 ... 다시 로드하세요.</span><span class="sxs-lookup"><span data-stu-id="ee885-118"><a name="e-b"></a>403 ... please try to reload</span></span>
![403 ... 다시 로드하십시오.](./media/app-insights-analytics-troubleshooting/020.png)

<span data-ttu-id="ee885-120">인증 관련 오류 발생(인증 또는 액세스 토크 생성 시).</span><span class="sxs-lookup"><span data-stu-id="ee885-120">An authentication related error occurred (during authentication or during access token generation).</span></span> <span data-ttu-id="ee885-121">브라우저 설정을 변경해야 포털 복구가 가능할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee885-121">The portal may have no way to  recover without changing browser settings.</span></span>

* <span data-ttu-id="ee885-122">브라우저에서 [타사 쿠키가 사용되도록 설정되어 있는지](#cookies) 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ee885-122">Verify [third party cookies are enabled](#cookies) in the browser.</span></span> 

## <span data-ttu-id="ee885-123"><a name="authentication"></a>403... 보안 영역 확인</span><span class="sxs-lookup"><span data-stu-id="ee885-123"><a name="authentication"></a>403 ... verify security zone</span></span>
![403... 보안 영역 확인](./media/app-insights-analytics-troubleshooting/030.png)

<span data-ttu-id="ee885-125">인증 관련 오류 발생(인증 또는 액세스 토크 생성 시).</span><span class="sxs-lookup"><span data-stu-id="ee885-125">An authentication related error occurred (during authentication or during access token generation).</span></span> <span data-ttu-id="ee885-126">브라우저 설정을 변경해야 포털 복구가 가능할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee885-126">The portal may have no way to  recover without changing browser settings.</span></span>

1. <span data-ttu-id="ee885-127">브라우저에서 [타사 쿠키가 사용되도록 설정되어 있는지](#cookies) 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ee885-127">Verify [third party cookies are enabled](#cookies) in the browser.</span></span> 
2. <span data-ttu-id="ee885-128">Analytics 포털을 여는 데 즐겨찾기, 책갈피, 타사 쿠키를 사용하였습니까?</span><span class="sxs-lookup"><span data-stu-id="ee885-128">Did you use a favorite, bookmark or saved link to open the Analytics portal?</span></span> <span data-ttu-id="ee885-129">링크를 저장할 때 사용한 자격 증명과 다른 것으로 로그인했습니까?</span><span class="sxs-lookup"><span data-stu-id="ee885-129">Are you signed in with different credentials than you used when you saved the link?</span></span>
3. <span data-ttu-id="ee885-130">비공개/시크릿 브라우저 창을 사용하세요(모든 해당 창을 닫은 후).</span><span class="sxs-lookup"><span data-stu-id="ee885-130">Try using an in-private/incognito browser window (after closing all such windows).</span></span> <span data-ttu-id="ee885-131">자격 증명을 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee885-131">You'll have to provide your credentials.</span></span> 
4. <span data-ttu-id="ee885-132">다른 (일반) 브라우저 창을 열고 [Azure](https://portal.azure.com)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ee885-132">Open another (ordinary) browser window and go to [Azure](https://portal.azure.com).</span></span> <span data-ttu-id="ee885-133">로그아웃합니다. 링크를 열고 올바른 자격 증명으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ee885-133">Sign out. Then open your link and sign in with the correct credentials.</span></span>
5. <span data-ttu-id="ee885-134">Edge와 Internet Explorer 사용자는 신뢰하는 영역 설정이 지원되지 않을 때 이 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee885-134">Edge and Internet Explorer users can also get this error when trusted zone settings are not supported.</span></span>
   
    <span data-ttu-id="ee885-135">[Analytics 포털](https://analytics.applicationinsights.io)과 [Azure Active Directory 포털](https://portal.azure.com)이 같은 보안 영역에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ee885-135">Verify both [Analytics portal](https://analytics.applicationinsights.io) and [Azure Active Directory portal](https://portal.azure.com) are in the same security zone:</span></span>
   
   * <span data-ttu-id="ee885-136">Internet Explorer에서 **인터넷 옵션**, **보안**, **신뢰할 수 있는 사이트**, **사이트**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ee885-136">In Internet Explorer, open **Internet Options**, **Security**, **Trusted sites**, **Sites**:</span></span>
     
     ![인터넷 옵션 대화 상자에서 신뢰할 수 있는 사이트에 사이트를 추가합니다.](./media/app-insights-analytics-troubleshooting/033.png)
     
     <span data-ttu-id="ee885-138">웹 사이트 목록에 다음 URL이 포함되어 있다면 다른 URL도 포함하세요.</span><span class="sxs-lookup"><span data-stu-id="ee885-138">In the Websites list, if any of the following URLs are included, make sure that the others are included also:</span></span>
     
     <span data-ttu-id="ee885-139">https://analytics.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="ee885-139">https://analytics.applicationinsights.io</span></span><br/>
     <span data-ttu-id="ee885-140">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="ee885-140">https://login.microsoftonline.com</span></span><br/>
     <span data-ttu-id="ee885-141">https://login.windows.net</span><span class="sxs-lookup"><span data-stu-id="ee885-141">https://login.windows.net</span></span>

## <span data-ttu-id="ee885-142"><a name="e-d"></a>404 ... 리소스를 찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="ee885-142"><a name="e-d"></a>404 ... Resource not found</span></span>
![404 ... 리소스를 찾을 수 없음](./media/app-insights-analytics-troubleshooting/040.png)

<span data-ttu-id="ee885-144">응용 프로그램 리소스가 Application Insights에서 삭제되어서 더는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ee885-144">Application resource was deleted from Application Insights and isn’t available anymore.</span></span> <span data-ttu-id="ee885-145">URL을 Analytics 페이지에 저장하면 이 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="ee885-145">This can happen if you saved the URL to the Analytics page.</span></span>

## <span data-ttu-id="ee885-146"><a name="e-e"></a>403 ... 권한 없음</span><span class="sxs-lookup"><span data-stu-id="ee885-146"><a name="e-e"></a>403 ... No authorization</span></span>
![403 ... 권한 없음](./media/app-insights-analytics-troubleshooting/050.png)

<span data-ttu-id="ee885-148">Analytics에서 이 응용 프로그램을 열 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ee885-148">You don't have permission to open this application in Analytics.</span></span>

* <span data-ttu-id="ee885-149">다른 사람에게 링크를 받았습니까?</span><span class="sxs-lookup"><span data-stu-id="ee885-149">Did you get the link from someone else?</span></span> <span data-ttu-id="ee885-150">[이 리소스 그룹의 독자 또는 참가자](app-insights-resources-roles-access-control.md)에 포함되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ee885-150">Ask them to make sure you are in the [readers or contributors for this resource group](app-insights-resources-roles-access-control.md).</span></span>
* <span data-ttu-id="ee885-151">다른 자격 증명으로 링크를 저장했습니까?</span><span class="sxs-lookup"><span data-stu-id="ee885-151">Did you save the link using different credentials?</span></span> <span data-ttu-id="ee885-152">[Azure 포털](https://portal.azure.com)을 열고 로그아웃한 다음, 다시 링크를 열고 올바른 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ee885-152">Open the [Azure portal](https://portal.azure.com), sign out, and then try this link again, providing the correct credentials.</span></span>

## <span data-ttu-id="ee885-153"><a name="html-storage"></a>403 ... HTML5 저장소</span><span class="sxs-lookup"><span data-stu-id="ee885-153"><a name="html-storage"></a>403 ... HTML5 Storage</span></span>
<span data-ttu-id="ee885-154">포털에서는 HTML5 localStorage와 sessionStorage를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ee885-154">Our portal uses HTML5 localStorage and sessionStorage.</span></span>

* <span data-ttu-id="ee885-155">Chrome: 설정, 개인 정보 보호, 콘텐츠 설정.</span><span class="sxs-lookup"><span data-stu-id="ee885-155">Chrome: Settings, privacy, content settings.</span></span>
* <span data-ttu-id="ee885-156">Internet Explorer: 인터넷 옵션, 고급 탭, 보안, DOM 저장소를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="ee885-156">Internet Explorer: Internet Options, Advanced tab, Security, Enable DOM Storage</span></span>

![403 ... HTML5 저장소를 사용하려고 합니다.](./media/app-insights-analytics-troubleshooting/060.png)

## <span data-ttu-id="ee885-158"><a name="e-g"></a>404 ... 구독을 찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="ee885-158"><a name="e-g"></a>404 ... Subscription not found</span></span>
![404 ... 구독을 찾을 수 없음](./media/app-insights-analytics-troubleshooting/070.png)

<span data-ttu-id="ee885-160">URL이 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ee885-160">The URL is invalid.</span></span> 

* <span data-ttu-id="ee885-161">[Application Insights 포털](https://portal.azure.com)에서 앱 리소스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ee885-161">Open the app resource in [Application Insights portal](https://portal.azure.com).</span></span> <span data-ttu-id="ee885-162">그런 다음 Analytics 단추를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ee885-162">Then use the Analytics button.</span></span>

## <span data-ttu-id="ee885-163"><a name="e-h"></a>404 ... 페이지가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ee885-163"><a name="e-h"></a>404 ... page doesn't exist</span></span>
![404 ... 페이지가 존재하지 않습니다.](./media/app-insights-analytics-troubleshooting/080.png)

<span data-ttu-id="ee885-165">URL이 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ee885-165">The URL is invalid.</span></span>

* <span data-ttu-id="ee885-166">[Application Insights 포털](https://portal.azure.com)에서 앱 리소스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ee885-166">Open the app resource in [Application Insights portal](https://portal.azure.com).</span></span> <span data-ttu-id="ee885-167">그런 다음 Analytics 단추를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ee885-167">Then use the Analytics button.</span></span>

## <span data-ttu-id="ee885-168"><a name="cookies"></a>타사 쿠키 사용</span><span class="sxs-lookup"><span data-stu-id="ee885-168"><a name="cookies"></a>Enable third-party cookies</span></span>
  <span data-ttu-id="ee885-169">[타사 쿠키를 사용하지 않도록 설정하는 방법](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers)을 참조하세요. 하지만 타사 쿠키를 **사용하도록 설정**해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee885-169">See [how to disable third party cookies](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), but notice we need to **enable** them.</span></span>


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

