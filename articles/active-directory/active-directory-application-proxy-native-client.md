---
title: "aaaPublish 네이티브 클라이언트 앱-Azure AD | Microsoft Docs"
description: "방법으로 Azure AD 응용 프로그램 프록시 커넥터 tooprovide 보안 된 원격 액세스 tooyour tooenable 네이티브 클라이언트 앱 toocommunicate 온-프레미스 응용 프로그램에 설명 합니다."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f0cae145-e346-4126-948f-3f699747b96e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 0ed2be217bf992f034d8321d5e66569b4cace24f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-native-client-apps-toointeract-with-proxy-applications"></a><span data-ttu-id="da6b4-103">어떻게 응용 프로그램 프록시와 tooenable 네이티브 클라이언트 앱 toointeract</span><span class="sxs-lookup"><span data-stu-id="da6b4-103">How tooenable native client apps toointeract with proxy Applications</span></span>

<span data-ttu-id="da6b4-104">또한 tooweb 응용 프로그램에서 Azure Active Directory 응용 프로그램 프록시 사용된 toopublish 네이티브 클라이언트 응용 프로그램 일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da6b4-104">In addition tooweb applications, Azure Active Directory Application Proxy can also be used toopublish native client apps.</span></span> <span data-ttu-id="da6b4-105">네이티브 클라이언트 앱은 장치에 설치되는 반면 웹앱은 브라우저를 통해 액세스되므로 웹앱과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="da6b4-105">Native client apps differ from web apps because they are installed on a device, while web apps are accessed through a browser.</span></span> 

<span data-ttu-id="da6b4-106">응용 프로그램 프록시는 표준 권한 부여 HTTP 헤더에서 전송된 Azure AD가 발급한 토큰을 수락하여 네이티브 클라이언트 앱을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="da6b4-106">Application Proxy supports native client apps by accepting Azure AD issued tokens that are sent in standard Authorize HTTP headers.</span></span>

![최종 사용자, Azure Active Directory 및 게시된 응용 프로그램 간의 관계](./media/active-directory-application-proxy-native-client/richclientflow.png)

<span data-ttu-id="da6b4-108">Hello 인증은 담당 하 고 많은 클라이언트 환경, toopublish 네이티브 응용 프로그램을 지 원하는 Azure AD 인증 라이브러리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="da6b4-108">Use hello Azure AD Authentication Library, which takes care of authentication and supports many client environments, toopublish native applications.</span></span> <span data-ttu-id="da6b4-109">응용 프로그램 프록시 hello에 맞는 [네이티브 응용 프로그램 API tooWeb 시나리오](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)합니다.</span><span class="sxs-lookup"><span data-stu-id="da6b4-109">Application Proxy fits into hello [Native Application tooWeb API scenario](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span></span> <span data-ttu-id="da6b4-110">이 문서는 hello 4 단계로 toopublish 응용 프로그램 프록시 및 hello Azure AD 인증 라이브러리는 네이티브 응용 프로그램을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="da6b4-110">This article walks you through hello four steps toopublish a native application with Application Proxy and hello Azure AD Authentication Library.</span></span> 

## <a name="step-1-publish-your-application"></a><span data-ttu-id="da6b4-111">1단계: 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="da6b4-111">Step 1: Publish your application</span></span>
<span data-ttu-id="da6b4-112">다른 응용 프로그램 처럼 프록시 응용 프로그램을 게시 하 고 응용 프로그램 사용자 tooaccess 할당.</span><span class="sxs-lookup"><span data-stu-id="da6b4-112">Publish your proxy application as you would any other application and assign users tooaccess your application.</span></span> <span data-ttu-id="da6b4-113">자세한 내용은 [응용 프로그램 프록시를 사용하여 응용 프로그램 게시](active-directory-application-proxy-publish.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da6b4-113">For more information, see [Publish applications with Application Proxy](active-directory-application-proxy-publish.md).</span></span>

## <a name="step-2-configure-your-application"></a><span data-ttu-id="da6b4-114">2단계: 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="da6b4-114">Step 2: Configure your application</span></span>
<span data-ttu-id="da6b4-115">네이티브 응용 프로그램을 다음과 같이 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="da6b4-115">Configure your native application as follows:</span></span>

1. <span data-ttu-id="da6b4-116">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="da6b4-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="da6b4-117">너무 이동**Azure Active Directory** > **앱 등록**합니다.</span><span class="sxs-lookup"><span data-stu-id="da6b4-117">Navigate too**Azure Active Directory** > **App registrations**.</span></span>
3. <span data-ttu-id="da6b4-118">**새 응용 프로그램 등록**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da6b4-118">Select **New application registration**.</span></span>
4. <span data-ttu-id="da6b4-119">응용 프로그램을 선택에 대 한 이름을 지정 **네이티브** hello 응용 프로그램 형식으로 응용 프로그램에 대 한 hello 리디렉션 URI를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="da6b4-119">Specify a name for your application, select **Native** as hello application type, and provide hello Redirect URI for your application.</span></span> 

   ![새 앱 등록 만들기](./media/active-directory-application-proxy-native-client/create.png)
5. <span data-ttu-id="da6b4-121">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da6b4-121">Select **Create**.</span></span>

<span data-ttu-id="da6b4-122">새 앱 등록 만들기에 대한 자세한 정보는 [Azure Active Directory와 응용 프로그램 통합](.//develop/active-directory-integrating-applications.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da6b4-122">For more detailed information about creating a new app registration, see [Integrating applications with Azure Active Directory](.//develop/active-directory-integrating-applications.md).</span></span>


## <a name="step-3-grant-access-tooother-applications"></a><span data-ttu-id="da6b4-123">3 단계: 권한 부여 액세스 tooother 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="da6b4-123">Step 3: Grant access tooother applications</span></span>
<span data-ttu-id="da6b4-124">Hello 네이티브 응용 프로그램 노출 toobe tooother 디렉터리에서 응용 프로그램을 사용 하도록 설정:</span><span class="sxs-lookup"><span data-stu-id="da6b4-124">Enable hello native application toobe exposed tooother applications in your directory:</span></span>

1. <span data-ttu-id="da6b4-125">여전히 **앱 등록**, 선택 hello 방금 만든 새 네이티브 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="da6b4-125">Still in **App registrations**, select hello new native application that you just created.</span></span>
2. <span data-ttu-id="da6b4-126">**필요한 권한**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da6b4-126">Select **Required permissions**.</span></span>
3. <span data-ttu-id="da6b4-127">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da6b4-127">Select **Add**.</span></span>
4. <span data-ttu-id="da6b4-128">첫 번째 단계는 열기 hello **API 선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="da6b4-128">Open hello first step, **Select an API**.</span></span>
5. <span data-ttu-id="da6b4-129">Hello 검색 표시줄 toofind hello 응용 프로그램 프록시 앱 hello 첫 번째 섹션에 게시를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="da6b4-129">Use hello search bar toofind hello Application Proxy app that you published in hello first section.</span></span> <span data-ttu-id="da6b4-130">해당 앱을 선택한 다음 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da6b4-130">Choose that app, then click **Select**.</span></span> 

   ![Hello 프록시 응용 프로그램에 대 한 검색](./media/active-directory-application-proxy-native-client/select_api.png)
6. <span data-ttu-id="da6b4-132">열기 hello 두 번째 단계에서는 **사용 권한을 선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="da6b4-132">Open hello second step, **Select permissions**.</span></span>
7. <span data-ttu-id="da6b4-133">Hello 확인란 toogrant 네이티브 응용 프로그램 액세스 tooyour 프록시 응용 프로그램을 사용 하 고 클릭 **선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="da6b4-133">Use hello checkbox toogrant your native application access tooyour proxy application, then click **Select**.</span></span>

   ![권한 부여 액세스 tooproxy 응용 프로그램](./media/active-directory-application-proxy-native-client/select_perms.png)
8. <span data-ttu-id="da6b4-135">**완료**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da6b4-135">Select **Done**.</span></span>


## <a name="step-4-edit-hello-active-directory-authentication-library"></a><span data-ttu-id="da6b4-136">4 단계: Active Directory 인증 라이브러리 hello 편집</span><span class="sxs-lookup"><span data-stu-id="da6b4-136">Step 4: Edit hello Active Directory Authentication Library</span></span>
<span data-ttu-id="da6b4-137">Hello Active Directory 인증 라이브러리 (ADAL) tooinclude hello 텍스트 다음의 hello 인증 컨텍스트에서 hello 네이티브 응용 프로그램 코드를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="da6b4-137">Edit hello native application code in hello authentication context of hello Active Directory Authentication Library (ADAL) tooinclude hello following text:</span></span>

```
// Acquire Access Token from AAD for Proxy Application
AuthenticationContext authContext = new AuthenticationContext("https://login.microsoftonline.com/<Tenant ID>");
AuthenticationResult result = authContext.AcquireToken("< External Url of Proxy App >",
        "<App ID of hello Native app>",
        new Uri("<Redirect Uri of hello Native App>"),
        PromptBehavior.Never);

//Use hello Access Token tooaccess hello Proxy Application
HttpClient httpClient = new HttpClient();
httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
HttpResponseMessage response = await httpClient.GetAsync("< Proxy App API Url >");
```

<span data-ttu-id="da6b4-138">hello 변수 hello 샘플 코드에서 다음과 같이 교체 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da6b4-138">hello variables in hello sample code should be replaced as follows:</span></span>

* <span data-ttu-id="da6b4-139">**테 넌 트 ID** hello Azure 포털에서에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da6b4-139">**Tenant ID** can be found in hello Azure portal.</span></span> <span data-ttu-id="da6b4-140">너무 이동**Azure Active Directory** > **속성** 및 복사 hello 디렉터리 id입니다.</span><span class="sxs-lookup"><span data-stu-id="da6b4-140">Navigate too**Azure Active Directory** > **Properties** and copy hello Directory ID.</span></span> 
* <span data-ttu-id="da6b4-141">**외부 URL** hello 프록시 응용 프로그램에에서 입력 한 hello 프런트 엔드 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="da6b4-141">**External URL** is hello front-end URL you entered in hello Proxy Application.</span></span> <span data-ttu-id="da6b4-142">toofind 값이 이동 toohello **응용 프로그램 프록시** hello 프록시 응용 프로그램의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="da6b4-142">toofind this value, navigate toohello **Application proxy** section of hello proxy app.</span></span>
* <span data-ttu-id="da6b4-143">**앱 ID** hello의 네이티브 응용 프로그램에서 확인할 수 있습니다 hello **속성** hello 네이티브 응용 프로그램의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="da6b4-143">**App ID** of hello native app can be found on hello **Properties** page of hello native application.</span></span>
* <span data-ttu-id="da6b4-144">**Hello 네이티브 응용 프로그램의 URI 리디렉션** hello에서 확인할 수 있습니다 **리디렉션 Uri** hello 네이티브 응용 프로그램의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="da6b4-144">**Redirect URI of hello native app** can be found on hello **Redirect URIs** page of hello native application.</span></span>


## <a name="see-also"></a><span data-ttu-id="da6b4-145">참고 항목</span><span class="sxs-lookup"><span data-stu-id="da6b4-145">See also</span></span>

<span data-ttu-id="da6b4-146">Hello 네이티브 응용 프로그램 흐름에 대 한 자세한 내용은 참조 [네이티브 응용 프로그램 tooweb API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)</span><span class="sxs-lookup"><span data-stu-id="da6b4-146">For more information about hello native application flow, see [Native application tooweb API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)</span></span>

<span data-ttu-id="da6b4-147">Hello 최신 뉴스 및 업데이트에 대 한 체크 아웃 hello [응용 프로그램 프록시 블로그](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="da6b4-147">For hello latest news and updates, check out hello [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>
