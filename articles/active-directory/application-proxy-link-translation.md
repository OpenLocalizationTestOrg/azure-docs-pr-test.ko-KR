---
title: "Azure AD 앱 프록시 링크 및 URL 변환 | Microsoft Docs"
description: "Azure AD 응용 프로그램 프록시 커넥터에 대한 기본 사항을 제공합니다."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 57218346d236b376d2227e0ffaea6c6dd5ebe855
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="redirect-hardcoded-links-for-apps-published-with-azure-ad-application-proxy"></a><span data-ttu-id="f64b0-103">Azure AD 응용 프로그램 프록시를 사용하여 게시된 앱에 대해 하드 코드된 링크 리디렉션</span><span class="sxs-lookup"><span data-stu-id="f64b0-103">Redirect hardcoded links for apps published with Azure AD Application Proxy</span></span>

<span data-ttu-id="f64b0-104">Azure AD 응용 프로그램 프록시는 원격 사용자가 자신의 장치에서 온-프레미스 앱을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f64b0-104">Azure AD Application Proxy makes your on-premises apps available to users who are remote or on their own devices.</span></span> <span data-ttu-id="f64b0-105">그러나 일부 앱은 HTML에 포함된 로컬 링크와 함께 개발되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f64b0-105">Some apps, however, were developed with local links embedded in the HTML.</span></span> <span data-ttu-id="f64b0-106">이러한 링크는 앱이 원격으로 사용되는 경우 제대로 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f64b0-106">These links don't work correctly when the app is used remotely.</span></span> <span data-ttu-id="f64b0-107">서로 가리키도록 하는 여러 온-프레미스 응용 프로그램이 있는 경우 사용자는 사무실에 있지 않은 경우 작업을 계속하기 위한 링크를 예상합니다.</span><span class="sxs-lookup"><span data-stu-id="f64b0-107">When you have several on-premises applications point to each other, your users expect the links to keep working when they're not at the office.</span></span> 

<span data-ttu-id="f64b0-108">링크가 회사 네트워크의 내부와 외부에서 동일하게 작동하는지 확인하는 가장 좋은 방법은 앱의 외부 URL을 내부 URL과 동일하도록 구성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f64b0-108">The best way to make sure that links work the same both inside and outside of your corporate network is to configure the external URLs of your apps to be the same as their internal URLs.</span></span> <span data-ttu-id="f64b0-109">[사용자 지정 도메인](active-directory-application-proxy-custom-domains.md)을 사용하여 외부 URL이 기본 응용 프로그램 프록시 도메인 대신 회사 도메인 이름을 갖도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f64b0-109">Use [custom domains](active-directory-application-proxy-custom-domains.md) to configure your external URLs to have your corporate domain name instead of the default application proxy domain.</span></span>

<span data-ttu-id="f64b0-110">테넌트에서 사용자 지정 도메인을 사용할 수 없는 경우 응용 프로그램 프록시의 링크 변환 기능이 사용자가 어디에 있든지 관계 없이 작동되도록 링크를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="f64b0-110">If you can't use custom domains in your tenant, then the link translation feature of Application Proxy keeps your links working no matter where your users are.</span></span> <span data-ttu-id="f64b0-111">내부 끝점이나 포트를 직접 가리키는 앱을 사용하는 경우 이러한 내부 URL을 게시된 외부 응용 프로그램 프록시 URL에 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f64b0-111">When you have apps that point directly to internal endpoints or ports, you can map these internal URLs to the published external Application Proxy URLs.</span></span> <span data-ttu-id="f64b0-112">링크 변환을 사용하는 경우 응용 프로그램 프록시는 HTML, CSS를 통해 검색하고 게시되는 내부 링크에 대해 JavaScript 태그를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f64b0-112">When link translation is enabled, and Application Proxy searches through HTML, CSS, and select JavaScript tags for published internal links.</span></span> <span data-ttu-id="f64b0-113">그런 다음 응용 프로그램 프록시 서비스는 사용자가 중단 없는 환경을 얻을 수 있도록 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="f64b0-113">Then the Application Proxy service translates them so that your users get an uninterrupted experience.</span></span>

>[!NOTE]
><span data-ttu-id="f64b0-114">링크 변환 기능은 어떠한 이유로든 사용자 지정 도메인을 사용하여 앱에 대한 내부 및 외부 URL을 동일하게 지정할 수 없는 테넌트에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f64b0-114">The link translation feature is for tenants that, for whatever reason, can't use custom domains to have the same internal and external URLs for their apps.</span></span> <span data-ttu-id="f64b0-115">이 기능을 사용하도록 설정하기 전에 [Azure AD 응용 프로그램 프록시의 사용자 지정 도메인](active-directory-application-proxy-custom-domains.md)이 작동하는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="f64b0-115">Before you enable this feature, see if [custom domains in Azure AD Application Proxy](active-directory-application-proxy-custom-domains.md) can work for you.</span></span>
>
><span data-ttu-id="f64b0-116">또는 링크 변환으로 구성해야 하는 응용 프로그램이 SharePoint인 경우 링크 매핑에 대한 다른 방법으로 [SharePoint 2013에 대한 대체 액세스 매핑 구성](https://technet.microsoft.com/library/cc263208.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f64b0-116">Or, if the application you need to configure with link translation is SharePoint, see [Configure alternate access mappings for SharePoint 2013](https://technet.microsoft.com/library/cc263208.aspx) for another approach to mapping links.</span></span>

## <a name="how-link-translation-works"></a><span data-ttu-id="f64b0-117">링크 변환의 작동 방식</span><span class="sxs-lookup"><span data-stu-id="f64b0-117">How link translation works</span></span>

<span data-ttu-id="f64b0-118">인증 후 프록시 서버가 사용자에게 응용 프로그램 데이터를 전달하면 응용 프로그램 프록시는 응용 프로그램에서 하드 코드된 링크를 검색하여 게시된 해당 외부 URL로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f64b0-118">After authentication, when the proxy server passes the application data to the user, Application Proxy scans the application for hardcoded links and replaces them with their respective, published external URLs.</span></span>

<span data-ttu-id="f64b0-119">응용 프로그램 프록시는 응용 프로그램이 UTF-8에서 인코딩되는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f64b0-119">Application Proxy assumes that applications are encoded in UTF-8.</span></span> <span data-ttu-id="f64b0-120">그렇지 않은 경우 http 응답 헤더의 인코딩 형식을 `Content-Type:text/html;charset=utf-8`과 같이 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f64b0-120">If that's not the case, specify the encoding type in an http response header, like `Content-Type:text/html;charset=utf-8`.</span></span>

### <a name="which-links-are-affected"></a><span data-ttu-id="f64b0-121">영향을 받는 링크</span><span class="sxs-lookup"><span data-stu-id="f64b0-121">Which links are affected?</span></span>

<span data-ttu-id="f64b0-122">링크 변환 기능은 앱 본문의 코드 태그에 있는 링크만 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f64b0-122">The link translation feature only looks for links that are in code tags in the body of an app.</span></span> <span data-ttu-id="f64b0-123">응용 프로그램 프록시에는 헤더에서 쿠키 또는 URL을 변환하는 별도의 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f64b0-123">Application Proxy has a separate feature for translating cookies or URLs in headers.</span></span> 

<span data-ttu-id="f64b0-124">온-프레미스 응용 프로그램에는 두 가지 일반적인 유형의 내부 링크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f64b0-124">There are two common types of internal links in on-premises applications:</span></span>

- <span data-ttu-id="f64b0-125">**상대 내부 링크** - `/claims/claims.html` 같은 로컬 파일 구조에서 공유 리소스를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="f64b0-125">**Relative internal links** that point to a shared resource in a local file structure like `/claims/claims.html`.</span></span> <span data-ttu-id="f64b0-126">이러한 링크는 응용 프로그램 프록시를 통해 게시되는 앱에서 자동으로 작동하며 링크 변환과 관계없이 계속 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="f64b0-126">These links automatically work in apps that are published through Application Proxy, and continue to work with or without link translation.</span></span> 
- <span data-ttu-id="f64b0-127">**하드 코드된 내부 링크** - `http://expenses` 같은 다른 온-프레미스 앱이나 `http://expenses/logo.jpg` 같은 게시된 파일에 대한 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="f64b0-127">**Hardcoded internal links** to other on-premises apps like `http://expenses` or published files like `http://expenses/logo.jpg`.</span></span> <span data-ttu-id="f64b0-128">링크 변환 기능은 하드 코드된 내부 링크에서 작동하며 해당 링크를 원격 사용자가 통과해야 하는 외부 URL을 가리키도록 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f64b0-128">The link translation feature works on hardcoded internal links, and changes them to point to the external URLs that remote users need to go through.</span></span>

### <a name="how-do-apps-link-to-each-other"></a><span data-ttu-id="f64b0-129">앱이 서로 연결되는 방식</span><span class="sxs-lookup"><span data-stu-id="f64b0-129">How do apps link to each other?</span></span>

<span data-ttu-id="f64b0-130">링크 변환은 각 응용 프로그램에 대해 사용되므로 앱별 수준에서 사용자 환경을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f64b0-130">Link translation is enabled for each application, so that you have control over the user experience at the per-app level.</span></span> <span data-ttu-id="f64b0-131">변환할 앱의 *대상* 링크가 아니라 해당 앱의 *원본* 링크를 원하는 경우 앱에 대해 링크 변환을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f64b0-131">Turn on link translation for an app when you want the links *from* that app to be translated, not links *to* that app.</span></span> 

<span data-ttu-id="f64b0-132">예를 들어 응용 프로그램 프록시를 통해 게시된 세 개의 응용 프로그램 Benefits, Expenses 및 Travel이 있고 모두 서로 연결되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f64b0-132">For example, suppose that you have three applications published through Application Proxy that all link to each other: Benefits, Expenses, and Travel.</span></span> <span data-ttu-id="f64b0-133">그리고 응용 프로그램 프록시를 통해 게시되지 않은 네 번째 Feedback 앱이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f64b0-133">There's a fourth app, Feedback, that isn't published through Application Proxy.</span></span>

<span data-ttu-id="f64b0-134">Benefits 앱에 대해 링크 변환을 사용하도록 설정하면 Expenses 및 Travel에 대한 링크는 해당 앱에 대한 외부 URL로 리디렉션되지만 Feedback에 대한 링크는 외부 URL이 없기 때문에 리디렉션되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f64b0-134">When you enable link translation for the Benefits app, the links to Expenses and Travel are redirected to the external URLs for those apps, but the link to Feedback is not redirected because there is no external URL.</span></span> <span data-ttu-id="f64b0-135">Expenses 및 Travel에서 Benefits로 다시 링크는 작동하지 않는데, 이러한 두 앱에 대해서는 링크 변환이 설정되지 않았기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="f64b0-135">Links from Expenses and Travel back to Benefits don't work, because link translation has not been enabled for those two apps.</span></span>

![링크 변환을 설정한 경우 Benefits에서 다른 앱으로 링크](./media/application-proxy-link-translation/one_app.png)

### <a name="which-links-arent-translated"></a><span data-ttu-id="f64b0-137">변환되지 않는 링크</span><span class="sxs-lookup"><span data-stu-id="f64b0-137">Which links aren't translated?</span></span>

<span data-ttu-id="f64b0-138">성능 및 보안 향상을 위해 일부 링크는 변환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f64b0-138">To improve performance and security, some links aren't translated:</span></span>

- <span data-ttu-id="f64b0-139">코드 태그 내부에 있지 않은 링크.</span><span class="sxs-lookup"><span data-stu-id="f64b0-139">Links not inside of code tags.</span></span> 
- <span data-ttu-id="f64b0-140">HTML, CSS 또는 JavaScript에 있지 않은 링크.</span><span class="sxs-lookup"><span data-stu-id="f64b0-140">Links not in HTML, CSS, or JavaScript.</span></span> 
- <span data-ttu-id="f64b0-141">다른 프로그램에서 연 내부 링크.</span><span class="sxs-lookup"><span data-stu-id="f64b0-141">Internal links opened from other programs.</span></span> <span data-ttu-id="f64b0-142">메일이나 인스턴트 메시지를 통해 전송되거나 다른 문서에 포함된 링크는 변환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f64b0-142">Links sent through email or instant message, or included in other documents, won't be translated.</span></span> <span data-ttu-id="f64b0-143">사용자는 외부 URL로 이동됨을 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f64b0-143">The users need to know to go to the external URL.</span></span>

<span data-ttu-id="f64b0-144">이러한 두 시나리오 중 하나를 지원해야 하는 경우 링크 변환 대신 동일한 외부 및 외부 URL을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f64b0-144">If you need to support one of these two scenarios, use the same internal and external URLs instead of link translation.</span></span>  

## <a name="enable-link-translation"></a><span data-ttu-id="f64b0-145">링크 변환을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="f64b0-145">Enable link translation</span></span>

<span data-ttu-id="f64b0-146">링크 변환 시작은 단추를 클릭하는 것만큼 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="f64b0-146">Getting started with link translation is as easy as clicking a button:</span></span>

1. <span data-ttu-id="f64b0-147">관리자로 [Azure Portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f64b0-147">Sign in to the [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="f64b0-148">**Azure Active Directory** > **Enterprise 응용 프로그램** > **모든 응용 프로그램** > 관리할 앱 선택 > **응용 프로그램 프록시**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f64b0-148">Go to **Azure Active Directory** > **Enterprise applications** > **All applications** > select the app you want to manage > **Application proxy**.</span></span>
3. <span data-ttu-id="f64b0-149">**Translate URLs in application body**(응용 프로그램 본문의 URL 변환)를 **예**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f64b0-149">Turn **Translate URLs in application body** to **Yes**.</span></span>

   ![[예]를 선택하여 응용 프로그램 본문의 URL 변환](./media/application-proxy-link-translation/select_yes.png)<span data-ttu-id="f64b0-151">등 4가지 유형의 클러스터가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f64b0-151">.</span></span>
4. <span data-ttu-id="f64b0-152">**저장**을 선택하여 변경 내용을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="f64b0-152">Select **Save** to apply your changes.</span></span>

<span data-ttu-id="f64b0-153">이제 사용자가 이 응용 프로그램에 액세스하면 프록시는 테넌트에서 응용 프로그램 프록시를 통해 게시된 내부 URL을 자동으로 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="f64b0-153">Now, when your users access this application, the proxy will automatically scan for internal URLs that have been published through Application Proxy on your tenant.</span></span>

## <a name="send-feedback"></a><span data-ttu-id="f64b0-154">피드백 보내기</span><span class="sxs-lookup"><span data-stu-id="f64b0-154">Send feedback</span></span>

<span data-ttu-id="f64b0-155">이 기능이 모든 앱에서 작동하도록 하는 데 도움이 되도록 피드백을 보내 주세요.</span><span class="sxs-lookup"><span data-stu-id="f64b0-155">We want your help to make this feature work for all your apps.</span></span> <span data-ttu-id="f64b0-156">HTML 및 CSS에서 30개가 넘는 태그를 검색하고 지원할 JavaScript 케이스를 검토하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f64b0-156">We search over 30 tags in HTML and CSS, and are considering which JavaScript cases to support.</span></span> <span data-ttu-id="f64b0-157">생성된 링크 중 변환되지 않는 예가 있으면 [응용 프로그램 프록시 피드백](mailto:aadapfeedback@microsoft.com)으로 코드 조각을 보내 주세요.</span><span class="sxs-lookup"><span data-stu-id="f64b0-157">If you have an example of generated links that aren't being translated, send a code snippet to [Application Proxy Feedback](mailto:aadapfeedback@microsoft.com).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f64b0-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f64b0-158">Next steps</span></span>
<span data-ttu-id="f64b0-159">동일한 내부 및 외부 URL을 사용하도록 [Azure AD 응용 프로그램 프록시에서 사용자 지정 도메인 사용](active-directory-application-proxy-custom-domains.md)</span><span class="sxs-lookup"><span data-stu-id="f64b0-159">[Use custom domains with Azure AD Application Proxy](active-directory-application-proxy-custom-domains.md) to have the same internal and external URL</span></span>

[<span data-ttu-id="f64b0-160">SharePoint 2013에 대한 대체 액세스 매핑 구성</span><span class="sxs-lookup"><span data-stu-id="f64b0-160">Configure alternate access mappings for SharePoint 2013</span></span>](https://technet.microsoft.com/library/cc263208.aspx)
