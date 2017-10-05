---
title: "네이티브 클라이언트 앱 게시 - Azure AD | Microsoft Docs"
description: "Azure AD 응용 프로그램 프록시 커넥터와 통신하는 네이티브 클라이언트 앱을 사용하여 온-프레미스 앱에 대한 보안된 원격 액세스를 제공하는 방법에 대해 설명합니다."
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
ms.openlocfilehash: bdaa5af6ff5331bc310499586615b48a864c3c5e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-enable-native-client-apps-to-interact-with-proxy-applications"></a><span data-ttu-id="90f69-103">네이티브 클라이언트 앱을 사용하여 프록시 응용 프로그램과 상호 작용하는 방법</span><span class="sxs-lookup"><span data-stu-id="90f69-103">How to enable native client apps to interact with proxy Applications</span></span>

<span data-ttu-id="90f69-104">웹 응용 프로그램뿐만 아니라 네이티브 클라이언트 앱을 게시하는 데 Azure Active Directory 응용 프로그램 프록시를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90f69-104">In addition to web applications, Azure Active Directory Application Proxy can also be used to publish native client apps.</span></span> <span data-ttu-id="90f69-105">네이티브 클라이언트 앱은 장치에 설치되는 반면 웹앱은 브라우저를 통해 액세스되므로 웹앱과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="90f69-105">Native client apps differ from web apps because they are installed on a device, while web apps are accessed through a browser.</span></span> 

<span data-ttu-id="90f69-106">응용 프로그램 프록시는 표준 권한 부여 HTTP 헤더에서 전송된 Azure AD가 발급한 토큰을 수락하여 네이티브 클라이언트 앱을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="90f69-106">Application Proxy supports native client apps by accepting Azure AD issued tokens that are sent in standard Authorize HTTP headers.</span></span>

![최종 사용자, Azure Active Directory 및 게시된 응용 프로그램 간의 관계](./media/active-directory-application-proxy-native-client/richclientflow.png)

<span data-ttu-id="90f69-108">인증을 처리하고 다양한 클라이언트 환경을 지원하는 Azure AD 인증 라이브러리를 사용하여 네이티브 응용 프로그램을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="90f69-108">Use the Azure AD Authentication Library, which takes care of authentication and supports many client environments, to publish native applications.</span></span> <span data-ttu-id="90f69-109">응용 프로그램 프록시는 [Web API 시나리오에 대한 네이티브 응용 프로그램](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)에 맞습니다.</span><span class="sxs-lookup"><span data-stu-id="90f69-109">Application Proxy fits into the [Native Application to Web API scenario](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span></span> <span data-ttu-id="90f69-110">이 문서에서는 응용 프로그램 프록시 및 Azure AD 인증 라이브러리를 사용하여 네이티브 응용 프로그램을 게시하는 네 가지 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="90f69-110">This article walks you through the four steps to publish a native application with Application Proxy and the Azure AD Authentication Library.</span></span> 

## <a name="step-1-publish-your-application"></a><span data-ttu-id="90f69-111">1단계: 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="90f69-111">Step 1: Publish your application</span></span>
<span data-ttu-id="90f69-112">다른 응용 프로그램과 마찬가지로 프록시 응용 프로그램을 게시하고 응용 프로그램에 액세스하도록 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="90f69-112">Publish your proxy application as you would any other application and assign users to access your application.</span></span> <span data-ttu-id="90f69-113">자세한 내용은 [응용 프로그램 프록시를 사용하여 응용 프로그램 게시](active-directory-application-proxy-publish.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="90f69-113">For more information, see [Publish applications with Application Proxy](active-directory-application-proxy-publish.md).</span></span>

## <a name="step-2-configure-your-application"></a><span data-ttu-id="90f69-114">2단계: 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="90f69-114">Step 2: Configure your application</span></span>
<span data-ttu-id="90f69-115">네이티브 응용 프로그램을 다음과 같이 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="90f69-115">Configure your native application as follows:</span></span>

1. <span data-ttu-id="90f69-116">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="90f69-116">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="90f69-117">**Azure Active Directory** > **앱 등록**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="90f69-117">Navigate to **Azure Active Directory** > **App registrations**.</span></span>
3. <span data-ttu-id="90f69-118">**새 응용 프로그램 등록**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90f69-118">Select **New application registration**.</span></span>
4. <span data-ttu-id="90f69-119">응용 프로그램에 대한 이름을 지정하고 응용 프로그램 형식으로 **네이티브**를 선택하고 응용 프로그램에 대한 리디렉션 URI를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="90f69-119">Specify a name for your application, select **Native** as the application type, and provide the Redirect URI for your application.</span></span> 

   ![새 앱 등록 만들기](./media/active-directory-application-proxy-native-client/create.png)
5. <span data-ttu-id="90f69-121">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90f69-121">Select **Create**.</span></span>

<span data-ttu-id="90f69-122">새 앱 등록 만들기에 대한 자세한 정보는 [Azure Active Directory와 응용 프로그램 통합](.//develop/active-directory-integrating-applications.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="90f69-122">For more detailed information about creating a new app registration, see [Integrating applications with Azure Active Directory](.//develop/active-directory-integrating-applications.md).</span></span>


## <a name="step-3-grant-access-to-other-applications"></a><span data-ttu-id="90f69-123">3단계: 다른 응용 프로그램에 액세스 허용</span><span class="sxs-lookup"><span data-stu-id="90f69-123">Step 3: Grant access to other applications</span></span>
<span data-ttu-id="90f69-124">디렉터리에서 다른 응용 프로그램에 노출될 네이티브 응용 프로그램을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="90f69-124">Enable the native application to be exposed to other applications in your directory:</span></span>

1. <span data-ttu-id="90f69-125">여전히 **앱 등록**에서 방금 만든 새 네이티브 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90f69-125">Still in **App registrations**, select the new native application that you just created.</span></span>
2. <span data-ttu-id="90f69-126">**필요한 권한**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90f69-126">Select **Required permissions**.</span></span>
3. <span data-ttu-id="90f69-127">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90f69-127">Select **Add**.</span></span>
4. <span data-ttu-id="90f69-128">첫 번째 단계를 열고 **API를 선택합니다**.</span><span class="sxs-lookup"><span data-stu-id="90f69-128">Open the first step, **Select an API**.</span></span>
5. <span data-ttu-id="90f69-129">검색 표시줄을 사용하여 첫 번째 섹션에 게시한 응용 프로그램 프록시 앱을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="90f69-129">Use the search bar to find the Application Proxy app that you published in the first section.</span></span> <span data-ttu-id="90f69-130">해당 앱을 선택한 다음 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90f69-130">Choose that app, then click **Select**.</span></span> 

   ![프록시 앱 검색](./media/active-directory-application-proxy-native-client/select_api.png)
6. <span data-ttu-id="90f69-132">두 번째 단계를 열고 **권한을 선택합니다**.</span><span class="sxs-lookup"><span data-stu-id="90f69-132">Open the second step, **Select permissions**.</span></span>
7. <span data-ttu-id="90f69-133">확인란을 사용하여 프록시 응용 프로그램에 대한 네이티브 응용 프로그램 액세스 권한을 부여한 다음 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="90f69-133">Use the checkbox to grant your native application access to your proxy application, then click **Select**.</span></span>

   ![프록시 앱에 대한 액세스 권한 부여](./media/active-directory-application-proxy-native-client/select_perms.png)
8. <span data-ttu-id="90f69-135">**완료**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90f69-135">Select **Done**.</span></span>


## <a name="step-4-edit-the-active-directory-authentication-library"></a><span data-ttu-id="90f69-136">4단계: Active Directory 인증 라이브러리 편집</span><span class="sxs-lookup"><span data-stu-id="90f69-136">Step 4: Edit the Active Directory Authentication Library</span></span>
<span data-ttu-id="90f69-137">Active Directory 인증 라이브러리(ADAL)의 인증 컨텍스트에서 네이티브 응용 프로그램 코드를 편집하여 다음 텍스트를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="90f69-137">Edit the native application code in the authentication context of the Active Directory Authentication Library (ADAL) to include the following text:</span></span>

```
// Acquire Access Token from AAD for Proxy Application
AuthenticationContext authContext = new AuthenticationContext("https://login.microsoftonline.com/<Tenant ID>");
AuthenticationResult result = authContext.AcquireToken("< External Url of Proxy App >",
        "<App ID of the Native app>",
        new Uri("<Redirect Uri of the Native App>"),
        PromptBehavior.Never);

//Use the Access Token to access the Proxy Application
HttpClient httpClient = new HttpClient();
httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
HttpResponseMessage response = await httpClient.GetAsync("< Proxy App API Url >");
```

<span data-ttu-id="90f69-138">샘플 코드의 변수는 다음과 같이 대체되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90f69-138">The variables in the sample code should be replaced as follows:</span></span>

* <span data-ttu-id="90f69-139">**테넌트 ID**는 Azure Portal에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90f69-139">**Tenant ID** can be found in the Azure portal.</span></span> <span data-ttu-id="90f69-140">**Azure Active Directory** > **속성**으로 이동하고 디렉터리 ID를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="90f69-140">Navigate to **Azure Active Directory** > **Properties** and copy the Directory ID.</span></span> 
* <span data-ttu-id="90f69-141">**외부 URL**은 프록시 응용 프로그램에 입력한 프런트 엔드 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="90f69-141">**External URL** is the front-end URL you entered in the Proxy Application.</span></span> <span data-ttu-id="90f69-142">이 값을 찾으려면 프록시 앱의 **응용 프로그램 프록시** 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="90f69-142">To find this value, navigate to the **Application proxy** section of the proxy app.</span></span>
* <span data-ttu-id="90f69-143">네이티브 앱의 **앱 ID**는 네이티브 응용 프로그램의 **속성** 페이지에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90f69-143">**App ID** of the native app can be found on the **Properties** page of the native application.</span></span>
* <span data-ttu-id="90f69-144">**네이티브 앱의 리디렉션 URI**는 네이티브 응용 프로그램의 **리디렉션 URI** 페이지에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90f69-144">**Redirect URI of the native app** can be found on the **Redirect URIs** page of the native application.</span></span>


## <a name="see-also"></a><span data-ttu-id="90f69-145">참고 항목</span><span class="sxs-lookup"><span data-stu-id="90f69-145">See also</span></span>

<span data-ttu-id="90f69-146">네이티브 응용 프로그램 흐름에 대한 자세한 내용은 [Web API에 대한 네이티브 응용 프로그램](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="90f69-146">For more information about the native application flow, see [Native application to web API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)</span></span>

<span data-ttu-id="90f69-147">최신 뉴스 및 업데이트는 [응용 프로그램 프록시 블로그](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="90f69-147">For the latest news and updates, check out the [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>
