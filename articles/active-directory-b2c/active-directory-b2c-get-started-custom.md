---
title: "Azure Active Directory B2C: 사용자 지정 정책 시작 | Microsoft Docs"
description: "Azure Active Directory B2C 사용자 지정 정책을 사용 하 여 tooget 시작 하는 방법"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: joroja;parahk;gsacavdm
ms.openlocfilehash: 5ee133806395cddf18682769a6cad149889d82d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-get-started-with-custom-policies"></a><span data-ttu-id="cd658-103">Azure Active Directory B2C: 사용자 지정 정책 시작</span><span class="sxs-lookup"><span data-stu-id="cd658-103">Azure Active Directory B2C: Get started with custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="cd658-104">사용자 지정 정책을 "로컬 계정" 지원할 hello이이 문서의 단계를 완료 한 후 등록 또는 로그인 전자 메일 주소와 암호를 통해 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-104">After you complete hello steps in this article, your custom policy will support "local account" sign-up or sign-in via an email address and password.</span></span> <span data-ttu-id="cd658-105">또한 Facebook 또는 Azure Active Directory와 같은 추가 ID 공급자를 추가하는 환경도 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-105">You will also prepare your environment for adding identity providers (like Facebook or Azure Active Directory).</span></span> <span data-ttu-id="cd658-106">Hello (Azure AD) Azure Active Directory B2C Id 경험 프레임 워크의 다른 방법에 대 한 읽기 전에 이러한 단계를 사용 하는 toocomplete를 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-106">We encourage you toocomplete these steps before reading about other uses of hello Azure Active Directory (Azure AD) B2C Identity Experience Framework.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cd658-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="cd658-107">Prerequisites</span></span>

<span data-ttu-id="cd658-108">계속하기 전에 모든 사용자, 응용 프로그램, 정책 등을 위한 컨테이너인 Azure AD B2C 테넌트가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-108">Before proceeding, ensure that you have an Azure AD B2C tenant, which is a container for all your users, apps, policies, and more.</span></span> <span data-ttu-id="cd658-109">너무 필요 없는 경우 하나 이미,[Azure AD B2C 테 넌 트 만들기](active-directory-b2c-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-109">If you don't have one already, you need too[create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span> <span data-ttu-id="cd658-110">म 강력한 모든 개발자가 toocomplete hello Azure AD B2C 기본 제공 정책 연습 들이 고 계속 하기 전에 기본 제공 정책을 사용 하 여 응용 프로그램을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-110">We strongly encourage all developers toocomplete hello Azure AD B2C built-in policy walkthroughs and configure their applications with built-in policies before proceeding.</span></span> <span data-ttu-id="cd658-111">최소 변경 toohello 정책 이름 tooinvoke hello 사용자 지정 정책을 확인 한 후 응용 프로그램 두 가지 정책 유형을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-111">Your applications will work with both types of policies once you make a minor change toohello policy name tooinvoke hello custom policy.</span></span>

>[!NOTE]
><span data-ttu-id="cd658-112">사용자 지정 정책 편집 tooaccess, 올바른 Azure 구독과 연결 된 tooyour 테 넌 트가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-112">tooaccess custom policy editing, you need a valid Azure subscription linked tooyour tenant.</span></span> <span data-ttu-id="cd658-113">그렇지 않은 경우 [Azure AD B2C 테 넌 트 tooan Azure 구독 연결](active-directory-b2c-how-to-enable-billing.md) 또는 Azure 구독이 사용 되지 않는지, hello Id 경험 프레임 워크 단추를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-113">If you haven't [linked your Azure AD B2C tenant tooan Azure subscription](active-directory-b2c-how-to-enable-billing.md) or your Azure subscription is disabled, hello Identity Experience Framework button won't be available.</span></span>

## <a name="add-signing-and-encryption-keys-tooyour-b2c-tenant-for-use-by-custom-policies"></a><span data-ttu-id="cd658-114">사용자 지정 정책에 의해 서명 및 암호화 키 tooyour B2C 테 넌 트 사용 하기 위해 추가</span><span class="sxs-lookup"><span data-stu-id="cd658-114">Add signing and encryption keys tooyour B2C tenant for use by custom policies</span></span>

1. <span data-ttu-id="cd658-115">열기 hello **Id 경험 프레임 워크** 블레이드 Azure AD B2C 테 넌 트 설정에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-115">Open hello **Identity Experience Framework** blade in your Azure AD B2C tenant settings.</span></span>
2. <span data-ttu-id="cd658-116">선택 **정책 키** 테 넌 트에 사용할 수 있는 tooview hello 키입니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-116">Select **Policy Keys** tooview hello keys available in your tenant.</span></span>
3. <span data-ttu-id="cd658-117">B2C_1A_TokenSigningKeyContainer가 없으면 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-117">Create B2C_1A_TokenSigningKeyContainer if it does not exist:</span></span><br>
    <span data-ttu-id="cd658-118">a.</span><span class="sxs-lookup"><span data-stu-id="cd658-118">a.</span></span> <span data-ttu-id="cd658-119">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-119">Select **Add**.</span></span> <br>
    <span data-ttu-id="cd658-120">b.</span><span class="sxs-lookup"><span data-stu-id="cd658-120">b.</span></span> <span data-ttu-id="cd658-121">**생성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-121">Select **Generate**.</span></span><br>
    <span data-ttu-id="cd658-122">c.</span><span class="sxs-lookup"><span data-stu-id="cd658-122">c.</span></span> <span data-ttu-id="cd658-123">**이름**에는 `TokenSigningKeyContainer`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-123">For **Name**, use `TokenSigningKeyContainer`.</span></span> <br> 
    <span data-ttu-id="cd658-124">hello 접두사 `B2C_1A_` 자동으로 추가 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-124">hello prefix `B2C_1A_` might be added automatically.</span></span><br>
    <span data-ttu-id="cd658-125">d.</span><span class="sxs-lookup"><span data-stu-id="cd658-125">d.</span></span> <span data-ttu-id="cd658-126">**키 유형**에는 **RSA**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-126">For **Key type**, use **RSA**.</span></span><br>
    <span data-ttu-id="cd658-127">e.</span><span class="sxs-lookup"><span data-stu-id="cd658-127">e.</span></span> <span data-ttu-id="cd658-128">에 대 한 **날짜**, hello 기본값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-128">For **Dates**, use hello defaults.</span></span> <br>
    <span data-ttu-id="cd658-129">f.</span><span class="sxs-lookup"><span data-stu-id="cd658-129">f.</span></span> <span data-ttu-id="cd658-130">**키 사용**에는 **서명**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-130">For **Key usage**, use **Signature**.</span></span><br>
    <span data-ttu-id="cd658-131">g.</span><span class="sxs-lookup"><span data-stu-id="cd658-131">g.</span></span> <span data-ttu-id="cd658-132">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-132">Select **Create**.</span></span><br>
4. <span data-ttu-id="cd658-133">B2C_1A_TokenEncryptionKeyContainer가 없으면 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-133">Create B2C_1A_TokenEncryptionKeyContainer if it does not exist:</span></span><br>
 <span data-ttu-id="cd658-134">a.</span><span class="sxs-lookup"><span data-stu-id="cd658-134">a.</span></span> <span data-ttu-id="cd658-135">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-135">Select **Add**.</span></span><br>
 <span data-ttu-id="cd658-136">b.</span><span class="sxs-lookup"><span data-stu-id="cd658-136">b.</span></span> <span data-ttu-id="cd658-137">**생성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-137">Select **Generate**.</span></span><br>
 <span data-ttu-id="cd658-138">c.</span><span class="sxs-lookup"><span data-stu-id="cd658-138">c.</span></span> <span data-ttu-id="cd658-139">**이름**에는 `TokenEncryptionKeyContainer`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-139">For **Name**, use `TokenEncryptionKeyContainer`.</span></span> <br>
   <span data-ttu-id="cd658-140">hello 접두사 `B2C_1A`_를 자동으로 추가 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-140">hello prefix `B2C_1A`_ might be added automatically.</span></span><br>
 <span data-ttu-id="cd658-141">d.</span><span class="sxs-lookup"><span data-stu-id="cd658-141">d.</span></span> <span data-ttu-id="cd658-142">**키 유형**에는 **RSA**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-142">For **Key type**, use **RSA**.</span></span><br>
 <span data-ttu-id="cd658-143">e.</span><span class="sxs-lookup"><span data-stu-id="cd658-143">e.</span></span> <span data-ttu-id="cd658-144">에 대 한 **날짜**, hello 기본값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-144">For **Dates**, use hello defaults.</span></span><br>
 <span data-ttu-id="cd658-145">f.</span><span class="sxs-lookup"><span data-stu-id="cd658-145">f.</span></span> <span data-ttu-id="cd658-146">**키 사용**에는 **암호화**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-146">For **Key usage**, use **Encryption**.</span></span><br>
 <span data-ttu-id="cd658-147">g.</span><span class="sxs-lookup"><span data-stu-id="cd658-147">g.</span></span> <span data-ttu-id="cd658-148">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-148">Select **Create**.</span></span><br>
5. <span data-ttu-id="cd658-149">B2C_1A_FacebookSecret를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-149">Create B2C_1A_FacebookSecret.</span></span> <br>
<span data-ttu-id="cd658-150">Facebook 응용 프로그램 암호를 이미 있는 경우 정책 키 tooyour 테 넌 트로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-150">If you already have a Facebook application secret, add it as a policy key tooyour tenant.</span></span> <span data-ttu-id="cd658-151">그렇지 않으면 hello 키를 만들어야 자리 표시자 값으로 정책 유효성 검사를 통과 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-151">Otherwise, you must create hello key with a placeholder value so that your policies pass validation.</span></span><br>
 <span data-ttu-id="cd658-152">a.</span><span class="sxs-lookup"><span data-stu-id="cd658-152">a.</span></span> <span data-ttu-id="cd658-153">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-153">Select **Add**.</span></span><br>
 <span data-ttu-id="cd658-154">b.</span><span class="sxs-lookup"><span data-stu-id="cd658-154">b.</span></span> <span data-ttu-id="cd658-155">**옵션**에는 **수동**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-155">For **Options**, use **Manual**.</span></span><br>
 <span data-ttu-id="cd658-156">c.</span><span class="sxs-lookup"><span data-stu-id="cd658-156">c.</span></span> <span data-ttu-id="cd658-157">**이름**에는 `FacebookSecret`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-157">For **Name**, use `FacebookSecret`.</span></span> <br>
 <span data-ttu-id="cd658-158">hello 접두사 `B2C_1A_` 자동으로 추가 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-158">hello prefix `B2C_1A_` might be added automatically.</span></span><br>
 <span data-ttu-id="cd658-159">d.</span><span class="sxs-lookup"><span data-stu-id="cd658-159">d.</span></span> <span data-ttu-id="cd658-160">Hello에 **비밀** 상자를 여 FacebookSecret developers.facebook.com에서 입력 또는 `0` 자리 표시자로 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-160">In hello **Secret** box, enter your FacebookSecret from developers.facebook.com or `0` as a placeholder.</span></span> <span data-ttu-id="cd658-161">*Facebook 앱 ID가 아닙니다.*</span><span class="sxs-lookup"><span data-stu-id="cd658-161">*This is not your Facebook app ID.*</span></span> <br>
 <span data-ttu-id="cd658-162">e.</span><span class="sxs-lookup"><span data-stu-id="cd658-162">e.</span></span> <span data-ttu-id="cd658-163">**키 사용**에는 **서명**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-163">For **Key usage**, use **Signature**.</span></span> <br>
 <span data-ttu-id="cd658-164">f.</span><span class="sxs-lookup"><span data-stu-id="cd658-164">f.</span></span> <span data-ttu-id="cd658-165">**만들기**를 선택하고 이 만들기를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-165">Select **Create** and confirm creation.</span></span>

## <a name="register-identity-experience-framework-applications"></a><span data-ttu-id="cd658-166">ID 경험 프레임워크 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="cd658-166">Register Identity Experience Framework applications</span></span>

<span data-ttu-id="cd658-167">Azure AD B2C tooregister에 hello 엔진 toosign를에서 사용 되 고 사용자가 로그인 하는 두 개의 추가 응용 프로그램이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-167">Azure AD B2C requires you tooregister two extra applications that are used by hello engine toosign up and sign in users.</span></span>

>[!NOTE]
><span data-ttu-id="cd658-168">해당 사용에 대 한 로그인 로컬 계정을 사용 하 여 두 개의 응용 프로그램을 만들어야 합니다: IdentityExperienceFramework (웹 응용 프로그램) 및 (네이티브 응용 프로그램)와 ProxyIdentityExperienceFramework hello IdentityExperienceFramework 앱에서 권한을 위임 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-168">You must create two applications that enable sign-in using local accounts: IdentityExperienceFramework (a web app) and ProxyIdentityExperienceFramework (a native app) with delegated permission from hello IdentityExperienceFramework app.</span></span> <span data-ttu-id="cd658-169">로컬 계정은 테넌트에만 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-169">Local accounts exist only in your tenant.</span></span> <span data-ttu-id="cd658-170">사용자가 등록 고유한 전자 메일 주소/암호 조합 tooaccess 테 넌 트가 등록 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="cd658-170">Your users sign up with a unique email address/password combination tooaccess your tenant-registered applications.</span></span>

### <a name="create-hello-identityexperienceframework-application"></a><span data-ttu-id="cd658-171">Hello IdentityExperienceFramework 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="cd658-171">Create hello IdentityExperienceFramework application</span></span>

1. <span data-ttu-id="cd658-172">Hello에 [Azure 포털](https://portal.azure.com), hello를 전환 [Azure AD B2C 테 넌 트의 상황에 맞는](active-directory-b2c-navigate-to-b2c-context.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-172">In hello [Azure portal](https://portal.azure.com), switch into hello [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md).</span></span>
2. <span data-ttu-id="cd658-173">열기 hello **Azure Active Directory** 블레이드 (하지 hello **Azure AD B2C** 블레이드)입니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-173">Open hello **Azure Active Directory** blade (not hello **Azure AD B2C** blade).</span></span> <span data-ttu-id="cd658-174">Tooselect 해야 **더 서비스** toofind 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-174">You might need tooselect **More Services** toofind it.</span></span>
3. <span data-ttu-id="cd658-175">**앱 등록**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-175">Select **App registrations**.</span></span>
4. <span data-ttu-id="cd658-176">**새 응용 프로그램 등록**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-176">Select **New application registration**.</span></span>
   * <span data-ttu-id="cd658-177">**이름**에는 `IdentityExperienceFramework`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-177">For **Name**, use `IdentityExperienceFramework`.</span></span>
   * <span data-ttu-id="cd658-178">**응용 프로그램 종류**에는 **웹앱/API**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-178">For **Application type**, use **Web app/API**.</span></span>
   * <span data-ttu-id="cd658-179">**로그온 URL**에는 `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`을 사용합니다. 여기서 `yourtenant`는 Azure AD B2C 테넌트 도메인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-179">For **Sign-on URL**, use `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`, where `yourtenant` is your Azure AD B2C tenant domain name.</span></span>
5. <span data-ttu-id="cd658-180">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-180">Select **Create**.</span></span>
6. <span data-ttu-id="cd658-181">을 만든 후 hello 새로 만든 응용 프로그램을 선택 합니다. **IdentityExperienceFramework**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-181">Once it is created, select hello newly created application **IdentityExperienceFramework**.</span></span><br>
   * <span data-ttu-id="cd658-182">**속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-182">Select **Properties**.</span></span><br>
   * <span data-ttu-id="cd658-183">Hello 응용 프로그램 ID를 복사 하 고 나중에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-183">Copy hello application ID and save it for later.</span></span>

### <a name="create-hello-proxyidentityexperienceframework-application"></a><span data-ttu-id="cd658-184">Hello ProxyIdentityExperienceFramework 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="cd658-184">Create hello ProxyIdentityExperienceFramework application</span></span>

1. <span data-ttu-id="cd658-185">**앱 등록**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-185">Select **App registrations**.</span></span>
1. <span data-ttu-id="cd658-186">**새 응용 프로그램 등록**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-186">Select **New application registration**.</span></span>
   * <span data-ttu-id="cd658-187">**이름**에는 `ProxyIdentityExperienceFramework`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-187">For **Name**, use `ProxyIdentityExperienceFramework`.</span></span>
   * <span data-ttu-id="cd658-188">**응용 프로그램 종류**에는 **네이티브**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-188">For **Application type**, use **Native**.</span></span>
   * <span data-ttu-id="cd658-189">**리디렉션 URI**에는 `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`을 사용합니다. 여기서 `yourtenant`는 Azure AD B2C 테넌트입니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-189">For **Redirect URI**, use `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`, where `yourtenant` is your Azure AD B2C tenant.</span></span>
1. <span data-ttu-id="cd658-190">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-190">Select **Create**.</span></span>
1. <span data-ttu-id="cd658-191">를 만든 후 hello 응용 프로그램을 선택 합니다. **ProxyIdentityExperienceFramework**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-191">Once it has been created, select hello application **ProxyIdentityExperienceFramework**.</span></span><br>
   * <span data-ttu-id="cd658-192">**속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-192">Select **Properties**.</span></span> <br>
   * <span data-ttu-id="cd658-193">Hello 응용 프로그램 ID를 복사 하 고 나중에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-193">Copy hello application ID and save it for later.</span></span>
1. <span data-ttu-id="cd658-194">**필요한 권한**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-194">Select **Required permissions**.</span></span>
1. <span data-ttu-id="cd658-195">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-195">Select **Add**.</span></span>
1. <span data-ttu-id="cd658-196">**API 선택**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-196">Select **Select an API**.</span></span>
1. <span data-ttu-id="cd658-197">IdentityExperienceFramework hello 이름에 대 한 검색입니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-197">Search for hello name IdentityExperienceFramework.</span></span> <span data-ttu-id="cd658-198">선택 **IdentityExperienceFramework** 에 결과 얻으려면 hello 및 클릭 **선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-198">Select **IdentityExperienceFramework** in hello results, and then click **Select**.</span></span>
1. <span data-ttu-id="cd658-199">다음 너무 hello 확인란을 선택한**액세스 IdentityExperienceFramework**, 클릭 하 고 **선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-199">Select hello check box next too**Access IdentityExperienceFramework**, and then click **Select**.</span></span>
1. <span data-ttu-id="cd658-200">**완료**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-200">Select **Done**.</span></span>
1. <span data-ttu-id="cd658-201">**권한 부여**을 선택하고 **예**를 선택하여 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-201">Select **Grant Permissions**, and then confirm by selecting **Yes**.</span></span>

## <a name="download-starter-pack-and-modify-policies"></a><span data-ttu-id="cd658-202">시작 팩 다운로드 및 정책 수정</span><span class="sxs-lookup"><span data-stu-id="cd658-202">Download starter pack and modify policies</span></span>

<span data-ttu-id="cd658-203">사용자 지정 정책은 업로드 toobe tooyour Azure AD B2C 테 넌 트를 필요로 하는 XML 파일의 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-203">Custom policies are a set of XML files that need toobe uploaded tooyour Azure AD B2C tenant.</span></span> <span data-ttu-id="cd658-204">스타터 팩 tooget 제공 신속 하 게 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-204">We provide starter packs tooget you going quickly.</span></span> <span data-ttu-id="cd658-205">Hello 목록 다음의 각 스타터 팩 hello 가장 적은 수의 기술 프로필에 포함 및 사용자 친구에 설명 된 tooachieve hello 시나리오 필요:</span><span class="sxs-lookup"><span data-stu-id="cd658-205">Each starter pack in hello following list contains hello smallest number of technical profiles and user journeys needed tooachieve hello scenarios described:</span></span>
 * <span data-ttu-id="cd658-206">LocalAccounts -</span><span class="sxs-lookup"><span data-stu-id="cd658-206">LocalAccounts.</span></span> <span data-ttu-id="cd658-207">Hello 로컬 계정에만 사용할을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-207">Enables hello use of local accounts only.</span></span>
 * <span data-ttu-id="cd658-208">SocialAccounts -</span><span class="sxs-lookup"><span data-stu-id="cd658-208">SocialAccounts.</span></span> <span data-ttu-id="cd658-209">Hello 소셜 (또는 페더레이션) 계정에만 사용할을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-209">Enables hello use of social (or federated) accounts only.</span></span>
 * <span data-ttu-id="cd658-210">**SocialAndLocalAccounts** -</span><span class="sxs-lookup"><span data-stu-id="cd658-210">**SocialAndLocalAccounts**.</span></span> <span data-ttu-id="cd658-211">Hello 연습에이 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-211">We use this file for hello walkthrough.</span></span>
 * <span data-ttu-id="cd658-212">SocialAndLocalAccountsWithMFA -</span><span class="sxs-lookup"><span data-stu-id="cd658-212">SocialAndLocalAccountsWithMFA.</span></span> <span data-ttu-id="cd658-213">소셜, 로컬 및 Multi-Factor Authentication 옵션이 여기에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-213">Social, local, and Multi-Factor Authentication options are included here.</span></span>

<span data-ttu-id="cd658-214">시작 팩 각각에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-214">Each starter pack contains:</span></span>

* <span data-ttu-id="cd658-215">hello [기본 파일](active-directory-b2c-overview-custom.md#policy-files) hello 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-215">hello [base file](active-directory-b2c-overview-custom.md#policy-files) of hello policy.</span></span> <span data-ttu-id="cd658-216">몇 가지 수정이 필요한 toohello 기본 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-216">Few modifications are required toohello base.</span></span>
* <span data-ttu-id="cd658-217">hello [확장 파일](active-directory-b2c-overview-custom.md#policy-files) hello 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-217">hello [extension file](active-directory-b2c-overview-custom.md#policy-files) of hello policy.</span></span>  <span data-ttu-id="cd658-218">이 파일은 구성이 대부분 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-218">This file is where most configuration changes are made.</span></span>
* <span data-ttu-id="cd658-219">[신뢰 당사자 파일](active-directory-b2c-overview-custom.md#policy-files)은 응용 프로그램에서 호출하는 작업 관련 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-219">[Relying party files](active-directory-b2c-overview-custom.md#policy-files) are task-specific files called by your application.</span></span>

>[!NOTE]
><span data-ttu-id="cd658-220">XML 편집기에서 유효성 검사를 지 원하는 경우 hello 스타터 팩 hello 루트 디렉터리에 있는 hello TrustFrameworkPolicy_0.3.0.0.xsd XML 스키마에 대해 hello 파일의 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-220">If your XML editor supports validation, validate hello files against hello TrustFrameworkPolicy_0.3.0.0.xsd XML schema that is located in hello root directory of hello starter pack.</span></span> <span data-ttu-id="cd658-221">업로드하기 전에 XML 스키마 유효성 검사가 오류를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-221">XML schema validation identifies errors before uploading.</span></span>

 <span data-ttu-id="cd658-222">이제 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-222">Let's get started:</span></span>

1. <span data-ttu-id="cd658-223">GitHub에서 active-directory-b2c-custom-policy-starterpack을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-223">Download active-directory-b2c-custom-policy-starterpack from GitHub.</span></span> <span data-ttu-id="cd658-224">[Hello.zip 파일을 다운로드](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/archive/master.zip) 또는 실행</span><span class="sxs-lookup"><span data-stu-id="cd658-224">[Download hello .zip file](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/archive/master.zip) or run</span></span>

    ```console
    git clone https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack
    ```
2. <span data-ttu-id="cd658-225">Hello SocialAndLocalAccounts 폴더를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-225">Open hello SocialAndLocalAccounts folder.</span></span>  <span data-ttu-id="cd658-226">hello 기본 파일 (TrustFrameworkBase.xml)이이 폴더에 로컬 및 사회/회사 계정에 필요한 콘텐츠를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-226">hello base file (TrustFrameworkBase.xml) in this folder contains content needed for both local and social/corporate accounts.</span></span> <span data-ttu-id="cd658-227">로컬 계정 시작 및 실행에 대 한 hello 단계 hello 소셜 콘텐츠 방해 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-227">hello social content does not interfere with hello steps for getting local accounts up and running.</span></span>
3. <span data-ttu-id="cd658-228">TrustFrameworkBase.xml을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-228">Open TrustFrameworkBase.xml.</span></span> <span data-ttu-id="cd658-229">XML 편집기가 필요하면 간단한 플랫폼 간 편집기인 [Visual Studio Code를 사용해 보세요](https://code.visualstudio.com/download).</span><span class="sxs-lookup"><span data-stu-id="cd658-229">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
4. <span data-ttu-id="cd658-230">Hello 루트에 `TrustFrameworkPolicy` 요소, 업데이트 hello `TenantId` 및 `PublicPolicyUri` 대체 특성 `yourtenant.onmicrosoft.com` 된 Azure AD B2C 테 넌 트의 도메인 이름이 hello:</span><span class="sxs-lookup"><span data-stu-id="cd658-230">In hello root `TrustFrameworkPolicy` element, update hello `TenantId` and `PublicPolicyUri` attributes, replacing `yourtenant.onmicrosoft.com` with hello domain name of your Azure AD B2C tenant:</span></span>
   ```xml
    <TrustFrameworkPolicy
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:xsd="http://www.w3.org/2001/XMLSchema"
    xmlns="http://schemas.microsoft.com/online/cpim/schemas/2013/06"
    PolicySchemaVersion="0.3.0.0"
    TenantId="yourtenant.onmicrosoft.com"
    PolicyId="B2C_1A_TrustFrameworkBase"
    PublicPolicyUri="http://yourtenant.onmicrosoft.com">
    ```
   >[!NOTE]
   ><span data-ttu-id="cd658-231">`PolicyId`이 정책 파일은 다른 정책 파일에서 참조 하는 기준인 hello 이름과 hello 정책 이름을 hello 포털에서 볼 수 있는 경우</span><span class="sxs-lookup"><span data-stu-id="cd658-231">`PolicyId` is hello policy name that you see in hello portal and hello name by which this policy file is referenced by other policy files.</span></span>

5. <span data-ttu-id="cd658-232">Hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-232">Save hello file.</span></span>
6. <span data-ttu-id="cd658-233">TrustFrameworkExtensions.xml을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-233">Open TrustFrameworkExtensions.xml.</span></span> <span data-ttu-id="cd658-234">Hello 같은 두 가지 사항을 변경 대체 하 여 `yourtenant.onmicrosoft.com` Azure AD B2C 테 넌 트와 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-234">Make hello same two changes by replacing `yourtenant.onmicrosoft.com` with your Azure AD B2C tenant.</span></span> <span data-ttu-id="cd658-235">동일한 hello 확인 hello에서 대체 `<TenantId>` 총 3 개의 변경 내용에 대 한 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-235">Make hello same replacement in hello `<TenantId>` element for a total of three changes.</span></span> <span data-ttu-id="cd658-236">Hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-236">Save hello file.</span></span>
7. <span data-ttu-id="cd658-237">SignUpOrSignIn.xml을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-237">Open SignUpOrSignIn.xml.</span></span> <span data-ttu-id="cd658-238">동일 하 게 hello 변경 대체 하 여 `yourtenant.onmicrosoft.com` 다음 세 위치에 Azure AD B2C 테 넌 트와 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-238">Make hello same changes by replacing `yourtenant.onmicrosoft.com` with your Azure AD B2C tenant in three places.</span></span> <span data-ttu-id="cd658-239">Hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-239">Save hello file.</span></span>
8. <span data-ttu-id="cd658-240">열기 hello 암호 다시 설정 하 고 프로필 파일을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-240">Open hello password reset and profile edit files.</span></span> <span data-ttu-id="cd658-241">동일 하 게 hello 변경 대체 하 여 `yourtenant.onmicrosoft.com` 각 파일에 다음 세 위치에 Azure AD B2C 테 넌 트와 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-241">Make hello same changes by replacing `yourtenant.onmicrosoft.com` with your Azure AD B2C tenant in three places in each file.</span></span> <span data-ttu-id="cd658-242">Hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-242">Save hello files.</span></span>

### <a name="add-hello-application-ids-tooyour-custom-policy"></a><span data-ttu-id="cd658-243">Hello tooyour 사용자 지정 정책 응용 프로그램 Id를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-243">Add hello application IDs tooyour custom policy</span></span>
<span data-ttu-id="cd658-244">Hello 응용 프로그램 Id toohello 확장 파일에 추가 (`TrustFrameworkExtensions.xml`):</span><span class="sxs-lookup"><span data-stu-id="cd658-244">Add hello application IDs toohello extensions file (`TrustFrameworkExtensions.xml`):</span></span>

1. <span data-ttu-id="cd658-245">Hello 요소 찾기 (TrustFrameworkExtensions.xml) 하는 hello 확장 파일에서 `<TechnicalProfile Id="login-NonInteractive">`합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-245">In hello extensions file (TrustFrameworkExtensions.xml), find hello element `<TechnicalProfile Id="login-NonInteractive">`.</span></span>
2. <span data-ttu-id="cd658-246">모두 `IdentityExperienceFrameworkAppId` hello 이전에 만든 Id 경험 프레임 워크 응용 프로그램의 hello 응용 프로그램 id입니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-246">Replace both instances of `IdentityExperienceFrameworkAppId` with hello application ID of hello Identity Experience Framework application that you created earlier.</span></span> <span data-ttu-id="cd658-247">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-247">Here is an example:</span></span>

   ```xml
   <Item Key="client_id">8322dedc-cbf4-43bc-8bb6-141d16f0f489</Item>
   ```
3. <span data-ttu-id="cd658-248">모두 `ProxyIdentityExperienceFrameworkAppId` hello 이전에 만든 프록시 Id 경험 프레임 워크 응용 프로그램의 hello 응용 프로그램 id입니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-248">Replace both instances of `ProxyIdentityExperienceFrameworkAppId` with hello application ID of hello Proxy Identity Experience Framework application that you created earlier.</span></span>
4. <span data-ttu-id="cd658-249">확장 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-249">Save your extensions file.</span></span>

## <a name="upload-hello-policies-tooyour-tenant"></a><span data-ttu-id="cd658-250">Hello 정책 tooyour 테 넌 트에 업로드</span><span class="sxs-lookup"><span data-stu-id="cd658-250">Upload hello policies tooyour tenant</span></span>

1. <span data-ttu-id="cd658-251">Hello에 [Azure 포털](https://portal.azure.com), hello를 전환 [Azure AD B2C 테 넌 트의 상황에 맞는](active-directory-b2c-navigate-to-b2c-context.md), 및 열기 hello **Azure AD B2C** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-251">In hello [Azure portal](https://portal.azure.com), switch into hello [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open hello **Azure AD B2C** blade.</span></span>
2. <span data-ttu-id="cd658-252">**ID 경험 프레임워크**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-252">Select **Identity Experience Framework**.</span></span>
3. <span data-ttu-id="cd658-253">**정책 업로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-253">Select **Upload Policy**.</span></span>

    >[!WARNING]
    ><span data-ttu-id="cd658-254">순서에 따라 hello에 hello 사용자 지정 정책 파일을 업로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-254">hello custom policy files must be uploaded in hello following order:</span></span>

1. <span data-ttu-id="cd658-255">TrustFrameworkBase.xml을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-255">Upload TrustFrameworkBase.xml.</span></span>
2. <span data-ttu-id="cd658-256">TrustFrameworkExtensions.xml을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-256">Upload TrustFrameworkExtensions.xml.</span></span>
3. <span data-ttu-id="cd658-257">SignUpOrSignin.xml을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-257">Upload SignUpOrSignin.xml.</span></span>
4. <span data-ttu-id="cd658-258">다른 정책 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-258">Upload your other policy files.</span></span>

<span data-ttu-id="cd658-259">파일을 업로드 하면 hello hello 정책 파일의 붙습니다 `B2C_1A_`합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-259">When a file is uploaded, hello name of hello policy file is prepended with `B2C_1A_`.</span></span>

## <a name="test-hello-custom-policy-by-using-run-now"></a><span data-ttu-id="cd658-260">지금 실행에 사용 하 여 hello 사용자 지정 정책 테스트</span><span class="sxs-lookup"><span data-stu-id="cd658-260">Test hello custom policy by using Run Now</span></span>

1. <span data-ttu-id="cd658-261">열기 **Azure AD B2C 설정** 너무 이동**Id 경험 프레임 워크**합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-261">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="cd658-262">**지금 실행** hello 테 넌 트에 응용 프로그램이 하나 이상 toobe 미리 등록 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-262">**Run now** requires at least one application toobe preregistered on hello tenant.</span></span> <span data-ttu-id="cd658-263">Hello를 사용 하 여 hello B2C 테 넌 트에서 응용 프로그램을 등록 해야 **응용 프로그램** 메뉴 선택 Azure AD B2C 또는 Id 경험 프레임 워크 tooinvoke hello를 사용 하 여 기본 및 사용자 지정 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-263">Applications must be registered in hello B2C tenant, either by using hello **Applications** menu selection in Azure AD B2C or by using hello Identity Experience Framework tooinvoke both built-in and custom policies.</span></span> <span data-ttu-id="cd658-264">응용 프로그램당 한 번만 등록하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-264">Only one registration per application is needed.</span></span><br><br>
   <span data-ttu-id="cd658-265">toolearn tooregister 응용 프로그램을 확인 하려면 어떻게 해야 Azure AD B2C hello [시작](active-directory-b2c-get-started.md) 문서 또는 hello [응용 프로그램 등록](active-directory-b2c-app-registration.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="cd658-265">toolearn how tooregister applications, see hello Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or hello [Application registration](active-directory-b2c-app-registration.md) article.</span></span>  

2. <span data-ttu-id="cd658-266">업로드 하는 신뢰 당사자 (RP) 사용자 지정 정책 hello를 B2C_1A_signup_signin 열고 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-266">Open B2C_1A_signup_signin, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="cd658-267">**지금 실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-267">Select **Run now**.</span></span>

3. <span data-ttu-id="cd658-268">전자 메일 주소를 사용 하 여 수 toosign 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-268">You should be able toosign up using an email address.</span></span>

4. <span data-ttu-id="cd658-269">동일한 계정 tooconfirm 해야 하는 hello 사용 하 여 로그인 hello 올바른 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-269">Sign in with hello same account tooconfirm that you have hello correct configuration.</span></span>

>[!NOTE]
><span data-ttu-id="cd658-270">로그인이 실패하는 것은 일반적으로 잘못 구성된 IdentityExperienceFramework 앱 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-270">A common cause of sign-in failure is an improperly configured IdentityExperienceFramework app.</span></span>


## <a name="next-steps"></a><span data-ttu-id="cd658-271">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cd658-271">Next steps</span></span>

### <a name="add-facebook-as-an-identity-provider"></a><span data-ttu-id="cd658-272">Facebook을 ID 공급자로 추가</span><span class="sxs-lookup"><span data-stu-id="cd658-272">Add Facebook as an identity provider</span></span>
<span data-ttu-id="cd658-273">Facebook tooset:</span><span class="sxs-lookup"><span data-stu-id="cd658-273">tooset up Facebook:</span></span>
1. <span data-ttu-id="cd658-274">[developers.facebook.com에서 Facebook 응용 프로그램을 구성합니다](active-directory-b2c-setup-fb-app.md).</span><span class="sxs-lookup"><span data-stu-id="cd658-274">[Configure a Facebook application in developers.facebook.com](active-directory-b2c-setup-fb-app.md).</span></span>
2. <span data-ttu-id="cd658-275">[Hello Facebook 응용 프로그램 보안 tooyour Azure AD B2C 테 넌 트 추가](#add-signing-and-encryption-keys-to-your-b2c-tenant-for-use-by-custom-policies)합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-275">[Add hello Facebook application secret tooyour Azure AD B2C tenant](#add-signing-and-encryption-keys-to-your-b2c-tenant-for-use-by-custom-policies).</span></span>
3. <span data-ttu-id="cd658-276">Hello TrustFrameworkExtensions 정책 파일에서의 hello 값 대체 `client_id` hello Facebook 응용 프로그램 id:</span><span class="sxs-lookup"><span data-stu-id="cd658-276">In hello TrustFrameworkExtensions policy file, replace hello value of `client_id` with hello Facebook application ID:</span></span>

   ```xml
   <TechnicalProfile Id="Facebook-OAUTH">
     <Metadata>
     <!--Replace hello value of client_id in this technical profile with hello Facebook app ID"-->
       <Item Key="client_id">00000000000000</Item>
   ```
4. <span data-ttu-id="cd658-277">Hello TrustFrameworkExtensions.xml 정책 파일 tooyour 테 넌 트를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-277">Upload hello TrustFrameworkExtensions.xml policy file tooyour tenant.</span></span>
5. <span data-ttu-id="cd658-278">사용 하 여 테스트 **지금 실행** hello 정책을 등록 된 응용 프로그램에서 직접 호출 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-278">Test by using **Run now** or by invoking hello policy directly from your registered application.</span></span>

### <a name="add-azure-active-directory-as-an-identity-provider"></a><span data-ttu-id="cd658-279">Azure Active Directory를 ID 공급자로 추가</span><span class="sxs-lookup"><span data-stu-id="cd658-279">Add Azure Active Directory as an identity provider</span></span>
<span data-ttu-id="cd658-280">이 시작된 가이드에서 이미 사용 하는 hello 기본 파일 기타 id 공급자를 추가 하는 데 필요한 hello 콘텐츠 중 일부를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd658-280">hello base file used in this getting started guide already contains some of hello content that you need for adding other identity providers.</span></span> <span data-ttu-id="cd658-281">로그인 설정에 대 한 자세한 내용은 참조 hello [Azure Active Directory B2C: Azure AD 계정을 사용 하 여 로그인](active-directory-b2c-setup-aad-custom.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="cd658-281">For information on setting up sign-ins, see hello [Azure Active Directory B2C: Sign in by using Azure AD accounts](active-directory-b2c-setup-aad-custom.md) article.</span></span>

<span data-ttu-id="cd658-282">Hello Id 경험 프레임 워크를 사용 하는 Azure AD B2C의 사용자 지정 정책 개요를 보려면 hello [Azure Active Directory B2C: 사용자 지정 정책의](active-directory-b2c-overview-custom.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="cd658-282">For an overview of custom policies in Azure AD B2C that use hello Identity Experience Framework, see hello [Azure Active Directory B2C: Custom policies](active-directory-b2c-overview-custom.md) article.</span></span> 
