---
title: "Azure Application Insights에서 분석 aaaTroubleshoot | Microsoft Docs"
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
ms.openlocfilehash: e3be2fbc0237440d3b8a736484434a9f276296c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-analytics-in-application-insights"></a><span data-ttu-id="498d3-104">Application Insights의 Analytics 문제 해결</span><span class="sxs-lookup"><span data-stu-id="498d3-104">Troubleshoot Analytics in Application Insights</span></span>
<span data-ttu-id="498d3-105">[Application Insights Analytics](app-insights-analytics.md)에 문제가 있습니까?</span><span class="sxs-lookup"><span data-stu-id="498d3-105">Problems with [Application Insights Analytics](app-insights-analytics.md)?</span></span> <span data-ttu-id="498d3-106">여기에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="498d3-106">Start here.</span></span> <span data-ttu-id="498d3-107">분석은 Azure Application Insights의 hello 강력한 검색 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="498d3-107">Analytics is hello powerful search tool of Azure Application Insights.</span></span>

## <a name="limits"></a><span data-ttu-id="498d3-108">제한</span><span class="sxs-lookup"><span data-stu-id="498d3-108">Limits</span></span>
* <span data-ttu-id="498d3-109">현재, 쿼리 결과가 제한 toojust를 과거 데이터의 주 동안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="498d3-109">At present, query results are limited toojust over a week of past data.</span></span>
* <span data-ttu-id="498d3-110">테스트 브라우저: Chrome, Edge 및 Internet Explorer 최신 버전.</span><span class="sxs-lookup"><span data-stu-id="498d3-110">Browsers we test on: latest editions of Chrome, Edge, and Internet Explorer.</span></span>

## <a name="known-incompatible-browser-extensions"></a><span data-ttu-id="498d3-111">알려진 호환되지 않는 브라우저 확장</span><span class="sxs-lookup"><span data-stu-id="498d3-111">Known incompatible browser extensions</span></span>
* <span data-ttu-id="498d3-112">Ghostery</span><span class="sxs-lookup"><span data-stu-id="498d3-112">Ghostery</span></span>

<span data-ttu-id="498d3-113">Hello 확장을 사용 하지 않도록 설정 하거나 다른 브라우저를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="498d3-113">Disable hello extension or use a different browser.</span></span>

## <span data-ttu-id="498d3-114"><a name="e-a"></a> "예기치 않은 오류"</span><span class="sxs-lookup"><span data-stu-id="498d3-114"><a name="e-a"></a> "Unexpected error"</span></span>
![예기치 않은 오류 화면](./media/app-insights-analytics-troubleshooting/010.png)

<span data-ttu-id="498d3-116">포털 런타임에 내부 오류 발생 – 처리되지 않은 예외.</span><span class="sxs-lookup"><span data-stu-id="498d3-116">Internal error occurred during portal runtime – unhandled exception.</span></span>

* <span data-ttu-id="498d3-117">Hello 브라우저 캐시를 정리 합니다.</span><span class="sxs-lookup"><span data-stu-id="498d3-117">Clean hello browser's cache.</span></span> 

## <span data-ttu-id="498d3-118"><a name="e-b"></a>403... tooreload를 시도 하십시오</span><span class="sxs-lookup"><span data-stu-id="498d3-118"><a name="e-b"></a>403 ... please try tooreload</span></span>
![403... tooreload를 시도 하십시오](./media/app-insights-analytics-troubleshooting/020.png)

<span data-ttu-id="498d3-120">인증 관련 오류 발생(인증 또는 액세스 토크 생성 시).</span><span class="sxs-lookup"><span data-stu-id="498d3-120">An authentication related error occurred (during authentication or during access token generation).</span></span> <span data-ttu-id="498d3-121">hello 포털 너무 브라우저 설정을 변경 하지 않고 복구 방법이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="498d3-121">hello portal may have no way too recover without changing browser settings.</span></span>

* <span data-ttu-id="498d3-122">확인 [제 3 자 쿠키가 활성화 되어](#cookies) hello 브라우저에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="498d3-122">Verify [third party cookies are enabled](#cookies) in hello browser.</span></span> 

## <span data-ttu-id="498d3-123"><a name="authentication"></a>403... 보안 영역 확인</span><span class="sxs-lookup"><span data-stu-id="498d3-123"><a name="authentication"></a>403 ... verify security zone</span></span>
![403... 보안 영역 확인](./media/app-insights-analytics-troubleshooting/030.png)

<span data-ttu-id="498d3-125">인증 관련 오류 발생(인증 또는 액세스 토크 생성 시).</span><span class="sxs-lookup"><span data-stu-id="498d3-125">An authentication related error occurred (during authentication or during access token generation).</span></span> <span data-ttu-id="498d3-126">hello 포털 너무 브라우저 설정을 변경 하지 않고 복구 방법이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="498d3-126">hello portal may have no way too recover without changing browser settings.</span></span>

1. <span data-ttu-id="498d3-127">확인 [제 3 자 쿠키가 활성화 되어](#cookies) hello 브라우저에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="498d3-127">Verify [third party cookies are enabled](#cookies) in hello browser.</span></span> 
2. <span data-ttu-id="498d3-128">즐겨찾기, 책갈피 또는 저장 된 링크 tooopen hello 분석 포털 사용 했나요?</span><span class="sxs-lookup"><span data-stu-id="498d3-128">Did you use a favorite, bookmark or saved link tooopen hello Analytics portal?</span></span> <span data-ttu-id="498d3-129">Hello 링크를 저장할 때 사용한 다른 자격 증명을 사용 하 여 서명?</span><span class="sxs-lookup"><span data-stu-id="498d3-129">Are you signed in with different credentials than you used when you saved hello link?</span></span>
3. <span data-ttu-id="498d3-130">비공개/시크릿 브라우저 창을 사용하세요(모든 해당 창을 닫은 후).</span><span class="sxs-lookup"><span data-stu-id="498d3-130">Try using an in-private/incognito browser window (after closing all such windows).</span></span> <span data-ttu-id="498d3-131">Tooprovide 자격 증명 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="498d3-131">You'll have tooprovide your credentials.</span></span> 
4. <span data-ttu-id="498d3-132">다른 (일반) 브라우저 창을 열고 다음 너무 이동[Azure](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="498d3-132">Open another (ordinary) browser window and go too[Azure](https://portal.azure.com).</span></span> <span data-ttu-id="498d3-133">로그아웃합니다. 다음 링크를 열고 hello 올바른 자격 증명을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="498d3-133">Sign out. Then open your link and sign in with hello correct credentials.</span></span>
5. <span data-ttu-id="498d3-134">Edge와 Internet Explorer 사용자는 신뢰하는 영역 설정이 지원되지 않을 때 이 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="498d3-134">Edge and Internet Explorer users can also get this error when trusted zone settings are not supported.</span></span>
   
    <span data-ttu-id="498d3-135">둘 다 확인 [분석 포털](https://analytics.applicationinsights.io) 및 [Azure Active Directory 포털](https://portal.azure.com) hello에 동일한 보안 영역:</span><span class="sxs-lookup"><span data-stu-id="498d3-135">Verify both [Analytics portal](https://analytics.applicationinsights.io) and [Azure Active Directory portal](https://portal.azure.com) are in hello same security zone:</span></span>
   
   * <span data-ttu-id="498d3-136">Internet Explorer에서 **인터넷 옵션**, **보안**, **신뢰할 수 있는 사이트**, **사이트**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="498d3-136">In Internet Explorer, open **Internet Options**, **Security**, **Trusted sites**, **Sites**:</span></span>
     
     ![인터넷 옵션 대화 상자에서 사이트를 추가 tooTrusted 사이트](./media/app-insights-analytics-troubleshooting/033.png)
     
     <span data-ttu-id="498d3-138">Hello 웹 사이트 목록에 hello 다음 Url 중 하나를 포함 해야 해당 hello 다른 사용자도 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="498d3-138">In hello Websites list, if any of hello following URLs are included, make sure that hello others are included also:</span></span>
     
     <span data-ttu-id="498d3-139">https://analytics.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="498d3-139">https://analytics.applicationinsights.io</span></span><br/>
     <span data-ttu-id="498d3-140">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="498d3-140">https://login.microsoftonline.com</span></span><br/>
     <span data-ttu-id="498d3-141">https://login.windows.net</span><span class="sxs-lookup"><span data-stu-id="498d3-141">https://login.windows.net</span></span>

## <span data-ttu-id="498d3-142"><a name="e-d"></a>404 ... 리소스를 찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="498d3-142"><a name="e-d"></a>404 ... Resource not found</span></span>
![404 ... 리소스를 찾을 수 없음](./media/app-insights-analytics-troubleshooting/040.png)

<span data-ttu-id="498d3-144">응용 프로그램 리소스가 Application Insights에서 삭제되어서 더는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="498d3-144">Application resource was deleted from Application Insights and isn’t available anymore.</span></span> <span data-ttu-id="498d3-145">이 hello URL toohello 분석 페이지를 저장 하는 경우 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="498d3-145">This can happen if you saved hello URL toohello Analytics page.</span></span>

## <span data-ttu-id="498d3-146"><a name="e-e"></a>403 ... 권한 없음</span><span class="sxs-lookup"><span data-stu-id="498d3-146"><a name="e-e"></a>403 ... No authorization</span></span>
![403 ... 권한 없음](./media/app-insights-analytics-troubleshooting/050.png)

<span data-ttu-id="498d3-148">사용 권한 tooopen이 응용이 프로그램에에서 없는 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="498d3-148">You don't have permission tooopen this application in Analytics.</span></span>

* <span data-ttu-id="498d3-149">어 hello 링크 다른 사람 으로부터?</span><span class="sxs-lookup"><span data-stu-id="498d3-149">Did you get hello link from someone else?</span></span> <span data-ttu-id="498d3-150">Hello에 있는지 toomake 달라고 [판독기나이 리소스 그룹에 대 한 참가자](app-insights-resources-roles-access-control.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="498d3-150">Ask them toomake sure you are in hello [readers or contributors for this resource group](app-insights-resources-roles-access-control.md).</span></span>
* <span data-ttu-id="498d3-151">다른 자격 증명을 사용 하 여 hello 링크 저장 하셨습니까?</span><span class="sxs-lookup"><span data-stu-id="498d3-151">Did you save hello link using different credentials?</span></span> <span data-ttu-id="498d3-152">열기 hello [Azure 포털](https://portal.azure.com), 로그 아웃 한 후 hello 올바른 자격 증명을 제공이 링크를 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="498d3-152">Open hello [Azure portal](https://portal.azure.com), sign out, and then try this link again, providing hello correct credentials.</span></span>

## <span data-ttu-id="498d3-153"><a name="html-storage"></a>403 ... HTML5 저장소</span><span class="sxs-lookup"><span data-stu-id="498d3-153"><a name="html-storage"></a>403 ... HTML5 Storage</span></span>
<span data-ttu-id="498d3-154">포털에서는 HTML5 localStorage와 sessionStorage를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="498d3-154">Our portal uses HTML5 localStorage and sessionStorage.</span></span>

* <span data-ttu-id="498d3-155">Chrome: 설정, 개인 정보 보호, 콘텐츠 설정.</span><span class="sxs-lookup"><span data-stu-id="498d3-155">Chrome: Settings, privacy, content settings.</span></span>
* <span data-ttu-id="498d3-156">Internet Explorer: 인터넷 옵션, 고급 탭, 보안, DOM 저장소를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="498d3-156">Internet Explorer: Internet Options, Advanced tab, Security, Enable DOM Storage</span></span>

![403... tooenable HTML5 저장소를 시도 하십시오.](./media/app-insights-analytics-troubleshooting/060.png)

## <span data-ttu-id="498d3-158"><a name="e-g"></a>404 ... 구독을 찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="498d3-158"><a name="e-g"></a>404 ... Subscription not found</span></span>
![404 ... 구독을 찾을 수 없음](./media/app-insights-analytics-troubleshooting/070.png)

<span data-ttu-id="498d3-160">hello URL이 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="498d3-160">hello URL is invalid.</span></span> 

* <span data-ttu-id="498d3-161">Hello 응용 프로그램 리소스에서 열고 [Application Insights 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="498d3-161">Open hello app resource in [Application Insights portal](https://portal.azure.com).</span></span> <span data-ttu-id="498d3-162">Hello 분석 단추를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="498d3-162">Then use hello Analytics button.</span></span>

## <span data-ttu-id="498d3-163"><a name="e-h"></a>404 ... 페이지가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="498d3-163"><a name="e-h"></a>404 ... page doesn't exist</span></span>
![404 ... 페이지가 존재하지 않습니다.](./media/app-insights-analytics-troubleshooting/080.png)

<span data-ttu-id="498d3-165">hello URL이 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="498d3-165">hello URL is invalid.</span></span>

* <span data-ttu-id="498d3-166">Hello 응용 프로그램 리소스에서 열고 [Application Insights 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="498d3-166">Open hello app resource in [Application Insights portal](https://portal.azure.com).</span></span> <span data-ttu-id="498d3-167">Hello 분석 단추를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="498d3-167">Then use hello Analytics button.</span></span>

## <span data-ttu-id="498d3-168"><a name="cookies"></a>타사 쿠키 사용</span><span class="sxs-lookup"><span data-stu-id="498d3-168"><a name="cookies"></a>Enable third-party cookies</span></span>
  <span data-ttu-id="498d3-169">참조 [toodisable는 타사 쿠키 방식을](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), 여기서 너무 필요 하지만**사용** 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="498d3-169">See [how toodisable third party cookies](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), but notice we need too**enable** them.</span></span>


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

