---
title: "Azure Active Directory B2C: 기본 제공 정책 | Microsoft Docs"
description: "방법 및 Azure Active Directory B2C의 hello 확장 가능한 정책 프레임 워크에서 항목 toocreate 다양 한 정책 유형"
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
ms.openlocfilehash: 24bb85eba30f888c6ea7d0401e05235e8eb6ea79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-built-in-policies"></a><span data-ttu-id="1dc4e-103">Azure Active Directory B2C: 기본 제공 정책</span><span class="sxs-lookup"><span data-stu-id="1dc4e-103">Azure Active Directory B2C: Built-in policies</span></span>


<span data-ttu-id="1dc4e-104">Azure Active Directory (Azure AD) B2C의 hello 확장 가능한 정책 프레임 워크는 hello 서비스의 핵심 강도 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc4e-104">hello extensible policy framework of Azure Active Directory (Azure AD) B2C is hello core strength of hello service.</span></span> <span data-ttu-id="1dc4e-105">정책은 등록, 로그인 또는 프로필 편집과 같은 소비자 ID 환경을 완벽하게 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc4e-105">Policies fully describe consumer identity experiences such as sign-up, sign-in, or profile editing.</span></span> <span data-ttu-id="1dc4e-106">예를 들어 등록 정책이 있습니다 toocontrol 동작을 hello 다음 설정을 구성 하 여:</span><span class="sxs-lookup"><span data-stu-id="1dc4e-106">For instance, a sign-up policy allows you toocontrol behaviors by configuring hello following settings:</span></span>

* <span data-ttu-id="1dc4e-107">계정 유형 (Facebook과 같은 소셜 계정) 또는 전자 메일 주소와 같은 로컬 계정 소비자가 hello 응용 프로그램에 대해 toosign를 사용할 수 있으며</span><span class="sxs-lookup"><span data-stu-id="1dc4e-107">Account types (social accounts such as Facebook or local accounts such as email addresses) that consumers can use toosign up for hello application</span></span>
* <span data-ttu-id="1dc4e-108">특성 (예: 이름, 우편 번호 및 신발 크기) toobe 등록 하는 동안 hello 소비자에서 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc4e-108">Attributes (for example, first name, postal code, and shoe size) toobe collected from hello consumer during sign-up</span></span>
* <span data-ttu-id="1dc4e-109">Azure Multi-Factor Authentication 사용</span><span class="sxs-lookup"><span data-stu-id="1dc4e-109">Use of Azure Multi-Factor Authentication</span></span>
* <span data-ttu-id="1dc4e-110">모든 등록 페이지의 hello 모양과 느낌</span><span class="sxs-lookup"><span data-stu-id="1dc4e-110">hello look and feel of all sign-up pages</span></span>
* <span data-ttu-id="1dc4e-111">Hello 정책 실행이 끝나면 응용 프로그램 hello 정보 (하는 토큰의 클레임으로 매니페스트) 받는</span><span class="sxs-lookup"><span data-stu-id="1dc4e-111">Information (which manifests as claims in a token) that hello application receives when hello policy run finishes</span></span>

<span data-ttu-id="1dc4e-112">테넌트에 다른 형식의 여러 정책을 만들고 필요에 따라 응용 프로그램에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dc4e-112">You can create multiple policies of different types in your tenant and use them in your applications as needed.</span></span> <span data-ttu-id="1dc4e-113">응용 프로그램에 정책을 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dc4e-113">Policies can be reused across applications.</span></span> <span data-ttu-id="1dc4e-114">이러한 유연성 개발자 toodefine 있으며 특정 소비자 identity 경험 최소 또는 변경 tootheir 코드 없이 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc4e-114">This flexibility enables developers toodefine and modify consumer identity experiences with minimal or no changes tootheir code.</span></span>

<span data-ttu-id="1dc4e-115">간단한 개발자 인터페이스를 통해 정책을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dc4e-115">Policies are available for use via a simple developer interface.</span></span> <span data-ttu-id="1dc4e-116">응용 프로그램 (hello 요청에서 정책 매개 변수를 전달)는 표준 HTTP 인증 요청을 사용 하 여 정책을 트리거하며 응답으로 사용자 지정된 토큰을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="1dc4e-116">Your application triggers a policy by using a standard HTTP authentication request (passing a policy parameter in hello request) and receives a customized token as response.</span></span> <span data-ttu-id="1dc4e-117">예를 들어 hello 등록 정책을 호출 하는 요청 및 로그인 정책을 호출 하는 요청 간의 유일한 차이점은 hello "p" 쿼리 문자열 매개 변수에서 사용 되는 hello 정책 이름:</span><span class="sxs-lookup"><span data-stu-id="1dc4e-117">For example, hello only difference between requests that invoke a sign-up policy and requests that invoke a sign-in policy is hello policy name that's used in hello "p" query string parameter:</span></span>

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

<span data-ttu-id="1dc4e-118">Hello 정책 프레임 워크에 대 한 자세한 내용은 참조 [Azure AD B2C에 hello Enterprise Mobility 및 보안 블로그에 대 한이 블로그 게시물](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc4e-118">For more information about hello policy framework, see [this blog post about Azure AD B2C on hello Enterprise Mobility and Security Blog](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx).</span></span>

## <a name="create-a-sign-up-or-sign-in-policy"></a><span data-ttu-id="1dc4e-119">등록 또는 로그인 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="1dc4e-119">Create a sign-up or sign-in policy</span></span>

<span data-ttu-id="1dc4e-120">이 정책은 단일 구성으로 등록 및 로그인 환경을 모두 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc4e-120">This policy handles both consumer sign-up & sign-in experiences with a single configuration.</span></span> <span data-ttu-id="1dc4e-121">소비자는 hello 오른쪽 경로 (등록 또는 로그인 hello 컨텍스트에 따라) 아래로 led 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1dc4e-121">Consumers are led down hello right path (sign-up or sign-in) depending on hello context.</span></span> <span data-ttu-id="1dc4e-122">또한 성공적인 로그인 ups 또는 로그인 시 받을 hello 응용 프로그램 토큰의 hello 내용을 설명 합니다.  Hello 등록 또는 로그인 시 정책에 대 한 코드 샘플은 [사용할 수 있는 여기](active-directory-b2c-devquickstarts-web-dotnet-susi.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc4e-122">It also describes hello contents of tokens that hello application will receive upon successful sign-ups or sign-ins.  A code sample for hello sign-up or sign-in policy is [available here](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span>  <span data-ttu-id="1dc4e-123">등록 정책 및 로그인 정책 대신 이 정책을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1dc4e-123">It is recommened that you use this policy over a sign-up policy and sign-in policy.</span></span>  

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

## <a name="create-a-sign-up-policy"></a><span data-ttu-id="1dc4e-124">등록 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="1dc4e-124">Create a sign-up policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-up-policy](../../includes/active-directory-b2c-create-sign-up-policy.md)]

## <a name="create-a-sign-in-policy"></a><span data-ttu-id="1dc4e-125">로그인 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="1dc4e-125">Create a sign-in policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-in-policy](../../includes/active-directory-b2c-create-sign-in-policy.md)]

## <a name="create-a-profile-editing-policy"></a><span data-ttu-id="1dc4e-126">프로필 편집 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="1dc4e-126">Create a profile editing policy</span></span>

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

## <a name="create-a-password-reset-policy"></a><span data-ttu-id="1dc4e-127">암호 재설정 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="1dc4e-127">Create a password reset policy</span></span>

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

## <a name="frequently-asked-questions"></a><span data-ttu-id="1dc4e-128">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="1dc4e-128">Frequently asked questions</span></span>

### <a name="how-do-i-link-a-sign-up-or-sign-in-policy-with-a-password-reset-policy"></a><span data-ttu-id="1dc4e-129">등록 또는 로그인 정책을 암호 재설정 정책과 연결하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="1dc4e-129">How do I link a sign-up or sign-in policy with a password reset policy?</span></span>
<span data-ttu-id="1dc4e-130">(로컬 계정)으로 등록 또는 로그인 시 정책을 만들 때 참조는 **암호를 잊으셨나요?** hello hello 환경의 첫 번째 페이지에서 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc4e-130">When you create a sign-up or sign-in policy (with local accounts), you see a **Forgot password?** link on hello first page of hello experience.</span></span> <span data-ttu-id="1dc4e-131">이 링크를 클릭해도 암호 재설정 정책이 자동으로 트리거되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1dc4e-131">Clicking this link doesn't automatically trigger a password reset policy.</span></span> 

<span data-ttu-id="1dc4e-132">대신, 오류 코드를 hello  **`AADB2C90118`**  tooyour 응용 프로그램에 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1dc4e-132">Instead, hello error code **`AADB2C90118`** is returned tooyour app.</span></span> <span data-ttu-id="1dc4e-133">응용 프로그램 특정 암호 재설정 정책을 호출 하 여 toohandle이 오류 코드가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc4e-133">Your app needs toohandle this error code by invoking a specific password reset policy.</span></span> <span data-ttu-id="1dc4e-134">자세한 내용은 참조는 [정책 연결의 hello 접근 방식을 보여 주는 샘플이](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI)합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc4e-134">For more information, see a [sample that demonstrates hello approach of linking policies](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI).</span></span>

### <a name="should-i-use-a-sign-up-or-sign-in-policy-or-a-sign-up-policy-and-a-sign-in-policy"></a><span data-ttu-id="1dc4e-135">등록 정책 또는 로그인 정책 또는 등록 정책 및 로그인 정책 중 어느 것을 사용해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="1dc4e-135">Should I use a sign-up or sign-in policy or a sign-up policy and a sign-in policy?</span></span>
<span data-ttu-id="1dc4e-136">등록 정책 및 로그인 정책에 대한 등록 정책이나 로그인 정책을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1dc4e-136">We recommend that you use a sign-up or sign-in policy over a sign-up policy and a sign-in policy.</span></span>  

<span data-ttu-id="1dc4e-137">hello 등록 또는 로그인 시 정책에 hello 로그인 정책 보다 더 많은 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dc4e-137">hello sign-up or sign-in policy has more capabilities than hello sign-in policy.</span></span> <span data-ttu-id="1dc4e-138">또한 하면 toouse 페이지 UI 사용자 지정 하 고 지역화를 위한 더 나은 지원 했습니다.</span><span class="sxs-lookup"><span data-stu-id="1dc4e-138">It also enables you toouse page UI customization and has better support for localization.</span></span> 

<span data-ttu-id="1dc4e-139">hello 로그인 정책 권장 toolocalize 정책에 필요 하지 않으면만 브랜딩에 대 한 보조 사용자 지정 기능을 사용 해야 및 암호 재설정에는 기본 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dc4e-139">hello sign-in policy is recommended if you don't need toolocalize your policies, only need minor customization capabilities for branding, and want password reset built into it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1dc4e-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1dc4e-140">Next steps</span></span>
* [<span data-ttu-id="1dc4e-141">토큰, 세션 및 Single Sign-On 구성</span><span class="sxs-lookup"><span data-stu-id="1dc4e-141">Token, session, and single sign-on configuration</span></span>](active-directory-b2c-token-session-sso.md)
* [<span data-ttu-id="1dc4e-142">소비자를 등록하는 동안 전자 메일 확인 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="1dc4e-142">Disable email verification during consumer sign-up</span></span>](active-directory-b2c-reference-disable-ev.md)

