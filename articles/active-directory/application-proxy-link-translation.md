---
title: "aaaTranslate 링크와 Azure AD 응용 프로그램 프록시 Url | Microsoft Docs"
description: "Azure AD 응용 프로그램 프록시 커넥터에 대 한 hello 기본 사항에 설명합니다."
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
ms.openlocfilehash: 7ec2b9fb01617067cf5d676037877bf72c19217b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="redirect-hardcoded-links-for-apps-published-with-azure-ad-application-proxy"></a><span data-ttu-id="608cd-103">Azure AD 응용 프로그램 프록시를 사용하여 게시된 앱에 대해 하드 코드된 링크 리디렉션</span><span class="sxs-lookup"><span data-stu-id="608cd-103">Redirect hardcoded links for apps published with Azure AD Application Proxy</span></span>

<span data-ttu-id="608cd-104">Azure AD 응용 프로그램 프록시는 원격 장애가 있거나가 자신의 장치에서 온-프레미스 앱 사용 가능한 toousers를 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-104">Azure AD Application Proxy makes your on-premises apps available toousers who are remote or on their own devices.</span></span> <span data-ttu-id="608cd-105">그러나 일부 응용 프로그램 hello HTML에에서 포함 된 로컬 링크와 함께 개발 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-105">Some apps, however, were developed with local links embedded in hello HTML.</span></span> <span data-ttu-id="608cd-106">이러한 링크는 hello 응용 프로그램을 원격으로 사용할 때 제대로 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-106">These links don't work correctly when hello app is used remotely.</span></span> <span data-ttu-id="608cd-107">여러 온-프레미스 응용 프로그램 지점 tooeach 다른을 사용 하는 경우 사용자가 hello 링크 tookeep hello에 있지 않는 경우 작업을 예상 합니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-107">When you have several on-premises applications point tooeach other, your users expect hello links tookeep working when they're not at hello office.</span></span> 

<span data-ttu-id="608cd-108">hello 가장 좋은 방법은 toomake 완료 되었는지 링크 작업 동일한 내부 hello 회사 네트워크 외부에 tooconfigure hello 앱 toobe의 외부 Url을 hello 내부 사이트의 Url로 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-108">hello best way toomake sure that links work hello same both inside and outside of your corporate network is tooconfigure hello external URLs of your apps toobe hello same as their internal URLs.</span></span> <span data-ttu-id="608cd-109">사용 하 여 [사용자 지정 도메인](active-directory-application-proxy-custom-domains.md) tooconfigure hello 기본 응용 프로그램 프록시 도메인이 아닌 회사 도메인 이름을 지정 하 여 외부 Url toohave 합니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-109">Use [custom domains](active-directory-application-proxy-custom-domains.md) tooconfigure your external URLs toohave your corporate domain name instead of hello default application proxy domain.</span></span>

<span data-ttu-id="608cd-110">테 넌 트의 사용자 지정 도메인을 사용할 수 없다면, 응용 프로그램 프록시 링크 변환 기능은 hello 위해 사용자에 관계 없이 작업 링크를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-110">If you can't use custom domains in your tenant, then hello link translation feature of Application Proxy keeps your links working no matter where your users are.</span></span> <span data-ttu-id="608cd-111">직접 매핑할 수 있습니다 toointernal 종단점 또는 포트를 가리키는 응용 프로그램이 있는 경우 이러한 내부 Url toohello 외부 응용 프로그램 프록시 Url을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-111">When you have apps that point directly toointernal endpoints or ports, you can map these internal URLs toohello published external Application Proxy URLs.</span></span> <span data-ttu-id="608cd-112">링크 변환을 사용하는 경우 응용 프로그램 프록시는 HTML, CSS를 통해 검색하고 게시되는 내부 링크에 대해 JavaScript 태그를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-112">When link translation is enabled, and Application Proxy searches through HTML, CSS, and select JavaScript tags for published internal links.</span></span> <span data-ttu-id="608cd-113">그런 다음 응용 프로그램 프록시 서비스 hello 변환 사용자가 중단 없이 환경을 얻을 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-113">Then hello Application Proxy service translates them so that your users get an uninterrupted experience.</span></span>

>[!NOTE]
><span data-ttu-id="608cd-114">hello 링크 변환 기능을 테 넌 트에 사용자 지정 도메인을 사용할 수 없습니다 어떤 이유 때문에 대 한 toohave hello가 앱에 대 한 동일한 내부 및 외부 Url입니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-114">hello link translation feature is for tenants that, for whatever reason, can't use custom domains toohave hello same internal and external URLs for their apps.</span></span> <span data-ttu-id="608cd-115">이 기능을 사용하도록 설정하기 전에 [Azure AD 응용 프로그램 프록시의 사용자 지정 도메인](active-directory-application-proxy-custom-domains.md)이 작동하는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="608cd-115">Before you enable this feature, see if [custom domains in Azure AD Application Proxy](active-directory-application-proxy-custom-domains.md) can work for you.</span></span>
>
><span data-ttu-id="608cd-116">SharePoint tooconfigure 링크 변환 사용 해야 하는 hello 응용 프로그램을 사용 하는 경우 참조 또는 [SharePoint 2013에 대 한 대체 액세스 매핑 구성](https://technet.microsoft.com/library/cc263208.aspx) 또 다른 방법은 toomapping 링크에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-116">Or, if hello application you need tooconfigure with link translation is SharePoint, see [Configure alternate access mappings for SharePoint 2013](https://technet.microsoft.com/library/cc263208.aspx) for another approach toomapping links.</span></span>

## <a name="how-link-translation-works"></a><span data-ttu-id="608cd-117">링크 변환의 작동 방식</span><span class="sxs-lookup"><span data-stu-id="608cd-117">How link translation works</span></span>

<span data-ttu-id="608cd-118">인증을 받은 후 프록시 서버 hello 전달 hello 응용 프로그램 데이터 toohello 사용자 응용 프로그램 프록시 하드 코드 된 링크에 대 한 hello 응용 프로그램 검색과 해당으로 바꿉니다 외부 Url을 게시.</span><span class="sxs-lookup"><span data-stu-id="608cd-118">After authentication, when hello proxy server passes hello application data toohello user, Application Proxy scans hello application for hardcoded links and replaces them with their respective, published external URLs.</span></span>

<span data-ttu-id="608cd-119">응용 프로그램 프록시는 응용 프로그램이 UTF-8에서 인코딩되는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-119">Application Proxy assumes that applications are encoded in UTF-8.</span></span> <span data-ttu-id="608cd-120">않은 hello 경우, hello 인코딩 유형을 지정 http 응답 헤더에 같은 `Content-Type:text/html;charset=utf-8`합니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-120">If that's not hello case, specify hello encoding type in an http response header, like `Content-Type:text/html;charset=utf-8`.</span></span>

### <a name="which-links-are-affected"></a><span data-ttu-id="608cd-121">영향을 받는 링크</span><span class="sxs-lookup"><span data-stu-id="608cd-121">Which links are affected?</span></span>

<span data-ttu-id="608cd-122">hello 링크 변환 기능은 응용 프로그램의 hello 본문에 코드 태그에 있는 링크에 대해서만 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-122">hello link translation feature only looks for links that are in code tags in hello body of an app.</span></span> <span data-ttu-id="608cd-123">응용 프로그램 프록시에는 헤더에서 쿠키 또는 URL을 변환하는 별도의 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-123">Application Proxy has a separate feature for translating cookies or URLs in headers.</span></span> 

<span data-ttu-id="608cd-124">온-프레미스 응용 프로그램에는 두 가지 일반적인 유형의 내부 링크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-124">There are two common types of internal links in on-premises applications:</span></span>

- <span data-ttu-id="608cd-125">**내부 링크 상대** 해당 지점 tooa 공유 리소스와 같은 로컬 파일 구조에서 `/claims/claims.html`합니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-125">**Relative internal links** that point tooa shared resource in a local file structure like `/claims/claims.html`.</span></span> <span data-ttu-id="608cd-126">이러한 링크는 자동으로 응용 프로그램 프록시를 통해 게시 하 고 toowork 또는 링크 변환 하지 않고 계속 하는 앱에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-126">These links automatically work in apps that are published through Application Proxy, and continue toowork with or without link translation.</span></span> 
- <span data-ttu-id="608cd-127">**하드 코드 된 내부 링크** tooother 온-프레미스와 같은 앱 `http://expenses` 게시 된 같은 파일 또는 `http://expenses/logo.jpg`합니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-127">**Hardcoded internal links** tooother on-premises apps like `http://expenses` or published files like `http://expenses/logo.jpg`.</span></span> <span data-ttu-id="608cd-128">hello 링크 변환 기능은 하드 코드 된 내부 링크를 작동 하 고 원격 사용자가 통해 toogo 필요한 toopoint toohello 외부 Url을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-128">hello link translation feature works on hardcoded internal links, and changes them toopoint toohello external URLs that remote users need toogo through.</span></span>

### <a name="how-do-apps-link-tooeach-other"></a><span data-ttu-id="608cd-129">앱 tooeach 다른 연결 방법</span><span class="sxs-lookup"><span data-stu-id="608cd-129">How do apps link tooeach other?</span></span>

<span data-ttu-id="608cd-130">링크 변환 hello 앱 별 수준에서 게 hello 사용자 환경 제어할 수 있도록 각 응용 프로그램에 대 한 활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-130">Link translation is enabled for each application, so that you have control over hello user experience at hello per-app level.</span></span> <span data-ttu-id="608cd-131">Hello 링크 하려는 경우에 응용 프로그램에 대 한 링크 변환 설정 *에서* 해당 앱 toobe 번역 링크 하지 *를* 앱.</span><span class="sxs-lookup"><span data-stu-id="608cd-131">Turn on link translation for an app when you want hello links *from* that app toobe translated, not links *to* that app.</span></span> 

<span data-ttu-id="608cd-132">예를 들어, 모든 다른 tooeach에 연결 하는 응용 프로그램 프록시를 통해 게시 된 세 개의 응용 프로그램을 해야: 이점과 비용을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-132">For example, suppose that you have three applications published through Application Proxy that all link tooeach other: Benefits, Expenses, and Travel.</span></span> <span data-ttu-id="608cd-133">그리고 응용 프로그램 프록시를 통해 게시되지 않은 네 번째 Feedback 앱이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-133">There's a fourth app, Feedback, that isn't published through Application Proxy.</span></span>

<span data-ttu-id="608cd-134">Hello 이점 앱에 대 한 링크 변환을 사용 하도록 설정 하면 hello 링크 tooExpenses 및 여행 해당 앱에 대 한 외부 Url 리디렉션된 toohello 하지만 외부 URL이 없습니다 있기 때문에 hello 링크 tooFeedback 리디렉션되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-134">When you enable link translation for hello Benefits app, hello links tooExpenses and Travel are redirected toohello external URLs for those apps, but hello link tooFeedback is not redirected because there is no external URL.</span></span> <span data-ttu-id="608cd-135">비용 및 여행 백 tooBenefits 그러한 두 응용 프로그램에 대 한 링크 변환이 설정 되어 있으므로 작동 하지 않는에서 링크를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-135">Links from Expenses and Travel back tooBenefits don't work, because link translation has not been enabled for those two apps.</span></span>

![앱에서 링크 변환을 사용 하는 이점 tooother 앱의 링크](./media/application-proxy-link-translation/one_app.png)

### <a name="which-links-arent-translated"></a><span data-ttu-id="608cd-137">변환되지 않는 링크</span><span class="sxs-lookup"><span data-stu-id="608cd-137">Which links aren't translated?</span></span>

<span data-ttu-id="608cd-138">일부 링크 없습니다 tooimprove 성능 및 보안을 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-138">tooimprove performance and security, some links aren't translated:</span></span>

- <span data-ttu-id="608cd-139">코드 태그 내부에 있지 않은 링크.</span><span class="sxs-lookup"><span data-stu-id="608cd-139">Links not inside of code tags.</span></span> 
- <span data-ttu-id="608cd-140">HTML, CSS 또는 JavaScript에 있지 않은 링크.</span><span class="sxs-lookup"><span data-stu-id="608cd-140">Links not in HTML, CSS, or JavaScript.</span></span> 
- <span data-ttu-id="608cd-141">다른 프로그램에서 연 내부 링크.</span><span class="sxs-lookup"><span data-stu-id="608cd-141">Internal links opened from other programs.</span></span> <span data-ttu-id="608cd-142">메일이나 인스턴트 메시지를 통해 전송되거나 다른 문서에 포함된 링크는 변환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-142">Links sent through email or instant message, or included in other documents, won't be translated.</span></span> <span data-ttu-id="608cd-143">hello 사용자 tooknow toogo toohello 외부 URL이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-143">hello users need tooknow toogo toohello external URL.</span></span>

<span data-ttu-id="608cd-144">이러한 두 시나리오 중 하나가 toosupport 해야 할 경우 사용 하 여 동일한 hello 링크 변환 하는 대신 내부 및 외부 Url입니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-144">If you need toosupport one of these two scenarios, use hello same internal and external URLs instead of link translation.</span></span>  

## <a name="enable-link-translation"></a><span data-ttu-id="608cd-145">링크 변환을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="608cd-145">Enable link translation</span></span>

<span data-ttu-id="608cd-146">링크 변환 시작은 단추를 클릭하는 것만큼 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-146">Getting started with link translation is as easy as clicking a button:</span></span>

1. <span data-ttu-id="608cd-147">Toohello 로그인 [Azure 포털](https://portal.azure.com) 관리자 권한으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-147">Sign in toohello [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="608cd-148">너무 이동**Azure Active Directory** > **엔터프라이즈 응용 프로그램** > **모든 응용 프로그램** > toomanage 선택 hello 앱 > **응용 프로그램 프록시**합니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-148">Go too**Azure Active Directory** > **Enterprise applications** > **All applications** > select hello app you want toomanage > **Application proxy**.</span></span>
3. <span data-ttu-id="608cd-149">설정 **응용 프로그램 본문에 Url 변환** 너무**예**합니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-149">Turn **Translate URLs in application body** too**Yes**.</span></span>

   ![응용 프로그램이 본문의 예 tootranslate Url 선택](./media/application-proxy-link-translation/select_yes.png)<span data-ttu-id="608cd-151">에서도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-151">.</span></span>
4. <span data-ttu-id="608cd-152">선택 **저장** tooapply 변경 내용을 합니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-152">Select **Save** tooapply your changes.</span></span>

<span data-ttu-id="608cd-153">이제 사용자가이 응용 프로그램에 액세스 하는 경우 hello 프록시 테 넌 트에 응용 프로그램 프록시를 통해 게시 된 내부 Url에 대 한 자동으로 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-153">Now, when your users access this application, hello proxy will automatically scan for internal URLs that have been published through Application Proxy on your tenant.</span></span>

## <a name="send-feedback"></a><span data-ttu-id="608cd-154">피드백 보내기</span><span class="sxs-lookup"><span data-stu-id="608cd-154">Send feedback</span></span>

<span data-ttu-id="608cd-155">원하는 도움말 toomake이 기능은 작업 모든 앱에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-155">We want your help toomake this feature work for all your apps.</span></span> <span data-ttu-id="608cd-156">HTML 및 CSS를 30 개 이상의 태그를 검색 하 고는 JavaScript의 경우 toosupport 고려 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-156">We search over 30 tags in HTML and CSS, and are considering which JavaScript cases toosupport.</span></span> <span data-ttu-id="608cd-157">번역 되지 되지 않은 생성 된 링크의 예를 사용 하는 경우 코드 조각에 너무 보낼[응용 프로그램 프록시 피드백](mailto:aadapfeedback@microsoft.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="608cd-157">If you have an example of generated links that aren't being translated, send a code snippet too[Application Proxy Feedback](mailto:aadapfeedback@microsoft.com).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="608cd-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="608cd-158">Next steps</span></span>
<span data-ttu-id="608cd-159">[사용자 지정 도메인을 사용 하 여 Azure AD 응용 프로그램 프록시](active-directory-application-proxy-custom-domains.md) toohave hello 동일한 내부 및 외부 URL</span><span class="sxs-lookup"><span data-stu-id="608cd-159">[Use custom domains with Azure AD Application Proxy](active-directory-application-proxy-custom-domains.md) toohave hello same internal and external URL</span></span>

[<span data-ttu-id="608cd-160">SharePoint 2013에 대한 대체 액세스 매핑 구성</span><span class="sxs-lookup"><span data-stu-id="608cd-160">Configure alternate access mappings for SharePoint 2013</span></span>](https://technet.microsoft.com/library/cc263208.aspx)
