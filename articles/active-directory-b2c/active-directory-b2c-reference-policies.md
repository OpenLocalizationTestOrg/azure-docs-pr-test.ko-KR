---
title: "Azure Active Directory B2C: 기본 제공 정책 | Microsoft Docs"
description: "Azure Active Directory B2C의 확장 가능한 정책 프레임워크 및 다양한 정책 형식을 만드는 방법에 대한 항목"
services: active-directory-b2c
documentationcenter: 
author: sama
manager: mbaldwin
editor: PatAltimore
ms.assetid: 0d453e72-7f70-4aa2-953d-938d2814d5a9
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: sama
ms.openlocfilehash: daad3af089afdf76b930053728bb11a5cf4c2a92
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-built-in-policies"></a><span data-ttu-id="db3ef-103">Azure Active Directory B2C: 기본 제공 정책</span><span class="sxs-lookup"><span data-stu-id="db3ef-103">Azure Active Directory B2C: Built-in policies</span></span>


<span data-ttu-id="db3ef-104">Azure Active Directory(Azure AD) B2C의 확장할 수 있는 정책 프레임워크는 서비스의 핵심 장점입니다.</span><span class="sxs-lookup"><span data-stu-id="db3ef-104">The extensible policy framework of Azure Active Directory (Azure AD) B2C is the core strength of the service.</span></span> <span data-ttu-id="db3ef-105">정책은 등록, 로그인 또는 프로필 편집과 같은 소비자 ID 환경을 완벽하게 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="db3ef-105">Policies fully describe consumer identity experiences such as sign-up, sign-in, or profile editing.</span></span> <span data-ttu-id="db3ef-106">예를 들어 등록 정책을 사용하면 다음 설정을 구성하여 동작을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db3ef-106">For instance, a sign-up policy allows you to control behaviors by configuring the following settings:</span></span>

* <span data-ttu-id="db3ef-107">소비자가 응용 프로그램에 등록하는 데 사용할 수 있는 계정 유형(Facebook과 같은 소셜 계정 또는 이메일 주소와 같은 로컬 계정)</span><span class="sxs-lookup"><span data-stu-id="db3ef-107">Account types (social accounts such as Facebook or local accounts such as email addresses) that consumers can use to sign up for the application</span></span>
* <span data-ttu-id="db3ef-108">등록 시 소비자로부터 수집할 특성(예: 이름, 우편 번호 및 신발 크기)</span><span class="sxs-lookup"><span data-stu-id="db3ef-108">Attributes (for example, first name, postal code, and shoe size) to be collected from the consumer during sign-up</span></span>
* <span data-ttu-id="db3ef-109">Azure Multi-Factor Authentication 사용</span><span class="sxs-lookup"><span data-stu-id="db3ef-109">Use of Azure Multi-Factor Authentication</span></span>
* <span data-ttu-id="db3ef-110">모든 등록 페이지의 모양과 느낌</span><span class="sxs-lookup"><span data-stu-id="db3ef-110">The look and feel of all sign-up pages</span></span>
* <span data-ttu-id="db3ef-111">정책 실행이 완료될 때 응용 프로그램에서 받는 정보(토큰에서 클레임으로 매니페스트됨)</span><span class="sxs-lookup"><span data-stu-id="db3ef-111">Information (which manifests as claims in a token) that the application receives when the policy run finishes</span></span>

<span data-ttu-id="db3ef-112">테넌트에 다른 형식의 여러 정책을 만들고 필요에 따라 응용 프로그램에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db3ef-112">You can create multiple policies of different types in your tenant and use them in your applications as needed.</span></span> <span data-ttu-id="db3ef-113">응용 프로그램에 정책을 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db3ef-113">Policies can be reused across applications.</span></span> <span data-ttu-id="db3ef-114">이러한 유연성을 통해 개발자가 코드를 변경하지 않거나 최소로 변경하여 소비자 ID 환경을 정의하고 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db3ef-114">This flexibility enables developers to define and modify consumer identity experiences with minimal or no changes to their code.</span></span>

<span data-ttu-id="db3ef-115">간단한 개발자 인터페이스를 통해 정책을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db3ef-115">Policies are available for use via a simple developer interface.</span></span> <span data-ttu-id="db3ef-116">응용 프로그램은 표준 HTTP 인증 요청을 사용하여 정책을 트리거하고(요청에 정책 매개 변수 전달) 사용자 지정 토큰을 응답으로 받습니다.</span><span class="sxs-lookup"><span data-stu-id="db3ef-116">Your application triggers a policy by using a standard HTTP authentication request (passing a policy parameter in the request) and receives a customized token as response.</span></span> <span data-ttu-id="db3ef-117">예를 들어 등록 정책을 호출하는 요청과 로그인 정책을 호출하는 요청 간의 유일한 차이점은 "p" 쿼리 문자열 매개 변수에 사용되는 정책 이름에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db3ef-117">For example, the only difference between requests that invoke a sign-up policy and requests that invoke a sign-in policy is the policy name that's used in the "p" query string parameter:</span></span>

```

https://login.microsoftonline.com/contosob2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e      // Your registered Application ID
&redirect_uri=https%3A%2F%2Flocalhost%3A44321%2F    // Your registered Reply URL, url encoded
&response_mode=form_post                            // 'query', 'form_post' or 'fragment'
&response_type=id_token
&scope=openid
&nonce=dummy
&state=12345                                        // Any value provided by your application
&p=b2c_1_siup                                       // Your sign-up policy

```

```

https://login.microsoftonline.com/contosob2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e      // Your registered Application ID
&redirect_uri=https%3A%2F%2Flocalhost%3A44321%2F    // Your registered Reply URL, url encoded
&response_mode=form_post                            // 'query', 'form_post' or 'fragment'
&response_type=id_token
&scope=openid
&nonce=dummy
&state=12345                                        // Any value provided by your application
&p=b2c_1_siin                                       // Your sign-in policy

```

<span data-ttu-id="db3ef-118">정책 프레임워크에 대한 자세한 내용은 [Enterprise Mobility 및 보안 블로그의 Azure AD B2C에 대한 블로그 게시물](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db3ef-118">For more information about the policy framework, see [this blog post about Azure AD B2C on the Enterprise Mobility and Security Blog](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx).</span></span>

## <a name="create-a-sign-up-or-sign-in-policy"></a><span data-ttu-id="db3ef-119">등록 또는 로그인 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="db3ef-119">Create a sign-up or sign-in policy</span></span>

<span data-ttu-id="db3ef-120">이 정책은 단일 구성으로 등록 및 로그인 환경을 모두 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="db3ef-120">This policy handles both consumer sign-up & sign-in experiences with a single configuration.</span></span> <span data-ttu-id="db3ef-121">소비자는 컨텍스트에 따라 올바른 경로(등록 또는 로그인)를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="db3ef-121">Consumers are led down the right path (sign-up or sign-in) depending on the context.</span></span> <span data-ttu-id="db3ef-122">또한 성공적인 등록 또는 로그인 시 응용 프로그램에서 수신할 토큰 내용도 설명합니다.  등록 또는 로그인 정책에 대한 코드 샘플은 [여기에서 사용할 수 있습니다](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="db3ef-122">It also describes the contents of tokens that the application will receive upon successful sign-ups or sign-ins.  A code sample for the sign-up or sign-in policy is [available here](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span>  <span data-ttu-id="db3ef-123">등록 정책 및 로그인 정책 대신 이 정책을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="db3ef-123">It is recommened that you use this policy over a sign-up policy and sign-in policy.</span></span>  

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

## <a name="create-a-sign-up-policy"></a><span data-ttu-id="db3ef-124">등록 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="db3ef-124">Create a sign-up policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-up-policy](../../includes/active-directory-b2c-create-sign-up-policy.md)]

## <a name="create-a-sign-in-policy"></a><span data-ttu-id="db3ef-125">로그인 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="db3ef-125">Create a sign-in policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-in-policy](../../includes/active-directory-b2c-create-sign-in-policy.md)]

## <a name="create-a-profile-editing-policy"></a><span data-ttu-id="db3ef-126">프로필 편집 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="db3ef-126">Create a profile editing policy</span></span>

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

## <a name="create-a-password-reset-policy"></a><span data-ttu-id="db3ef-127">암호 재설정 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="db3ef-127">Create a password reset policy</span></span>

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

## <a name="frequently-asked-questions"></a><span data-ttu-id="db3ef-128">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="db3ef-128">Frequently asked questions</span></span>

### <a name="how-do-i-link-a-sign-up-or-sign-in-policy-with-a-password-reset-policy"></a><span data-ttu-id="db3ef-129">등록 또는 로그인 정책을 암호 재설정 정책과 연결하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="db3ef-129">How do I link a sign-up or sign-in policy with a password reset policy?</span></span>
<span data-ttu-id="db3ef-130">등록 또는 로그인 정책을 만드는 경우(로컬 계정 사용) 환경의 첫 번째 페이지에서 **암호 찾기** 링크가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="db3ef-130">When you create a sign-up or sign-in policy (with local accounts), you see a **Forgot password?** link on the first page of the experience.</span></span> <span data-ttu-id="db3ef-131">이 링크를 클릭해도 암호 재설정 정책이 자동으로 트리거되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="db3ef-131">Clicking this link doesn't automatically trigger a password reset policy.</span></span> 

<span data-ttu-id="db3ef-132">대신 **`AADB2C90118`** 오류 코드가 앱에 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="db3ef-132">Instead, the error code **`AADB2C90118`** is returned to your app.</span></span> <span data-ttu-id="db3ef-133">앱에서 특정 암호 재설정 정책을 호출하여 이 오류 코드를 처리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db3ef-133">Your app needs to handle this error code by invoking a specific password reset policy.</span></span> <span data-ttu-id="db3ef-134">자세한 내용은 [정책을 연결하는 방법을 보여 주는 샘플](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db3ef-134">For more information, see a [sample that demonstrates the approach of linking policies](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI).</span></span>

### <a name="should-i-use-a-sign-up-or-sign-in-policy-or-a-sign-up-policy-and-a-sign-in-policy"></a><span data-ttu-id="db3ef-135">등록 정책 또는 로그인 정책 또는 등록 정책 및 로그인 정책 중 어느 것을 사용해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="db3ef-135">Should I use a sign-up or sign-in policy or a sign-up policy and a sign-in policy?</span></span>
<span data-ttu-id="db3ef-136">등록 정책 및 로그인 정책에 대한 등록 정책이나 로그인 정책을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="db3ef-136">We recommend that you use a sign-up or sign-in policy over a sign-up policy and a sign-in policy.</span></span>  

<span data-ttu-id="db3ef-137">등록 정책 또는 로그인 정책에는 로그인 정책보다 많은 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db3ef-137">The sign-up or sign-in policy has more capabilities than the sign-in policy.</span></span> <span data-ttu-id="db3ef-138">또한 페이지 UI 사용자 지정 기능을 사용할 수 있으며 지역화를 더 효율적으로 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="db3ef-138">It also enables you to use page UI customization and has better support for localization.</span></span> 

<span data-ttu-id="db3ef-139">정책을 지역화할 필요가 없고, 브랜딩에 대한 약간의 사용자 지정 기능만 필요하고, 암호 재설정을 기본 제공하려는 경우에는 로그인 정책을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="db3ef-139">The sign-in policy is recommended if you don't need to localize your policies, only need minor customization capabilities for branding, and want password reset built into it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="db3ef-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="db3ef-140">Next steps</span></span>
* [<span data-ttu-id="db3ef-141">토큰, 세션 및 Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="db3ef-141">Token, session, and single sign-on configuration</span></span>](active-directory-b2c-token-session-sso.md)
* [<span data-ttu-id="db3ef-142">소비자를 등록하는 동안 전자 메일 확인 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="db3ef-142">Disable email verification during consumer sign-up</span></span>](active-directory-b2c-reference-disable-ev.md)

