---
title: "Azure Active Directory B2C: 사용자 지정 정책 시작 | Microsoft Docs"
description: "Azure Active Directory B2C 사용자 지정 정책을 시작하는 방법"
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
ms.openlocfilehash: 4f14dbf4b66f10290cd4f98d56a005f97cc6a207
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-get-started-with-custom-policies"></a><span data-ttu-id="22c71-103">Azure Active Directory B2C: 사용자 지정 정책 시작</span><span class="sxs-lookup"><span data-stu-id="22c71-103">Azure Active Directory B2C: Get started with custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="22c71-104">이 문서의 단계를 완료하면 사용자 지정 정책에서 이메일 주소와 암호를 통한 "로컬 계정" 등록 또는 로그인을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-104">After you complete the steps in this article, your custom policy will support "local account" sign-up or sign-in via an email address and password.</span></span> <span data-ttu-id="22c71-105">또한 Facebook 또는 Azure Active Directory와 같은 추가 ID 공급자를 추가하는 환경도 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-105">You will also prepare your environment for adding identity providers (like Facebook or Azure Active Directory).</span></span> <span data-ttu-id="22c71-106">Azure AD(Azure Active Directory ) B2C ID 경험 프레임워크의 다른 용도를 이해하려면 먼저 이 단계를 완료하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-106">We encourage you to complete these steps before reading about other uses of the Azure Active Directory (Azure AD) B2C Identity Experience Framework.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22c71-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="22c71-107">Prerequisites</span></span>

<span data-ttu-id="22c71-108">계속하기 전에 모든 사용자, 응용 프로그램, 정책 등을 위한 컨테이너인 Azure AD B2C 테넌트가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-108">Before proceeding, ensure that you have an Azure AD B2C tenant, which is a container for all your users, apps, policies, and more.</span></span> <span data-ttu-id="22c71-109">아직 없으면 [Azure AD B2C 테넌트를 만들어야 합니다](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="22c71-109">If you don't have one already, you need to [create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span> <span data-ttu-id="22c71-110">계속하기 전에 모든 개발자가 Azure AD B2C 기본 제공 정책 연습을 완료하고 기본 제공 정책으로 응용 프로그램을 구성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-110">We strongly encourage all developers to complete the Azure AD B2C built-in policy walkthroughs and configure their applications with built-in policies before proceeding.</span></span> <span data-ttu-id="22c71-111">정책 이름을 약간 변경하여 사용자 지정 정책을 호출하면 응용 프로그램이 두 유형의 정책 모두에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-111">Your applications will work with both types of policies once you make a minor change to the policy name to invoke the custom policy.</span></span>

>[!NOTE]
><span data-ttu-id="22c71-112">사용자 지정 정책 편집에 액세스하려면 테넌트와 연결된 유효한 Azure 구독이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-112">To access custom policy editing, you need a valid Azure subscription linked to your tenant.</span></span> <span data-ttu-id="22c71-113">[Azure AD B2C 테넌트를 Azure 구독에 연결](active-directory-b2c-how-to-enable-billing.md)하지 않았거나 Azure 구독을 사용할 수 없는 경우 ID 경험 프레임워크 단추를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-113">If you haven't [linked your Azure AD B2C tenant to an Azure subscription](active-directory-b2c-how-to-enable-billing.md) or your Azure subscription is disabled, the Identity Experience Framework button won't be available.</span></span>

## <a name="add-signing-and-encryption-keys-to-your-b2c-tenant-for-use-by-custom-policies"></a><span data-ttu-id="22c71-114">사용자 지정 정책에서 사용하도록 B2C 테넌트에 서명 및 암호화 키 추가</span><span class="sxs-lookup"><span data-stu-id="22c71-114">Add signing and encryption keys to your B2C tenant for use by custom policies</span></span>

1. <span data-ttu-id="22c71-115">Azure AD B2C 테넌트 설정에서 **ID 경험 프레임워크** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-115">Open the **Identity Experience Framework** blade in your Azure AD B2C tenant settings.</span></span>
2. <span data-ttu-id="22c71-116">**정책 키**를 선택하여 테넌트에 사용 가능한 키를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-116">Select **Policy Keys** to view the keys available in your tenant.</span></span>
3. <span data-ttu-id="22c71-117">B2C_1A_TokenSigningKeyContainer가 없으면 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-117">Create B2C_1A_TokenSigningKeyContainer if it does not exist:</span></span><br>
    <span data-ttu-id="22c71-118">a.</span><span class="sxs-lookup"><span data-stu-id="22c71-118">a.</span></span> <span data-ttu-id="22c71-119">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-119">Select **Add**.</span></span> <br>
    <span data-ttu-id="22c71-120">b.</span><span class="sxs-lookup"><span data-stu-id="22c71-120">b.</span></span> <span data-ttu-id="22c71-121">**생성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-121">Select **Generate**.</span></span><br>
    <span data-ttu-id="22c71-122">c.</span><span class="sxs-lookup"><span data-stu-id="22c71-122">c.</span></span> <span data-ttu-id="22c71-123">**이름**에는 `TokenSigningKeyContainer`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-123">For **Name**, use `TokenSigningKeyContainer`.</span></span> <br> 
    <span data-ttu-id="22c71-124">`B2C_1A_` 접두사가 자동으로 추가될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-124">The prefix `B2C_1A_` might be added automatically.</span></span><br>
    <span data-ttu-id="22c71-125">d.</span><span class="sxs-lookup"><span data-stu-id="22c71-125">d.</span></span> <span data-ttu-id="22c71-126">**키 유형**에는 **RSA**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-126">For **Key type**, use **RSA**.</span></span><br>
    <span data-ttu-id="22c71-127">e.</span><span class="sxs-lookup"><span data-stu-id="22c71-127">e.</span></span> <span data-ttu-id="22c71-128">**날짜**에는 기본값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-128">For **Dates**, use the defaults.</span></span> <br>
    <span data-ttu-id="22c71-129">f.</span><span class="sxs-lookup"><span data-stu-id="22c71-129">f.</span></span> <span data-ttu-id="22c71-130">**키 사용**에는 **서명**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-130">For **Key usage**, use **Signature**.</span></span><br>
    <span data-ttu-id="22c71-131">g.</span><span class="sxs-lookup"><span data-stu-id="22c71-131">g.</span></span> <span data-ttu-id="22c71-132">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-132">Select **Create**.</span></span><br>
4. <span data-ttu-id="22c71-133">B2C_1A_TokenEncryptionKeyContainer가 없으면 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-133">Create B2C_1A_TokenEncryptionKeyContainer if it does not exist:</span></span><br>
 <span data-ttu-id="22c71-134">a.</span><span class="sxs-lookup"><span data-stu-id="22c71-134">a.</span></span> <span data-ttu-id="22c71-135">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-135">Select **Add**.</span></span><br>
 <span data-ttu-id="22c71-136">b.</span><span class="sxs-lookup"><span data-stu-id="22c71-136">b.</span></span> <span data-ttu-id="22c71-137">**생성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-137">Select **Generate**.</span></span><br>
 <span data-ttu-id="22c71-138">c.</span><span class="sxs-lookup"><span data-stu-id="22c71-138">c.</span></span> <span data-ttu-id="22c71-139">**이름**에는 `TokenEncryptionKeyContainer`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-139">For **Name**, use `TokenEncryptionKeyContainer`.</span></span> <br>
   <span data-ttu-id="22c71-140">`B2C_1A`_ 접두사가 자동으로 추가될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-140">The prefix `B2C_1A`_ might be added automatically.</span></span><br>
 <span data-ttu-id="22c71-141">d.</span><span class="sxs-lookup"><span data-stu-id="22c71-141">d.</span></span> <span data-ttu-id="22c71-142">**키 유형**에는 **RSA**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-142">For **Key type**, use **RSA**.</span></span><br>
 <span data-ttu-id="22c71-143">e.</span><span class="sxs-lookup"><span data-stu-id="22c71-143">e.</span></span> <span data-ttu-id="22c71-144">**날짜**에는 기본값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-144">For **Dates**, use the defaults.</span></span><br>
 <span data-ttu-id="22c71-145">f.</span><span class="sxs-lookup"><span data-stu-id="22c71-145">f.</span></span> <span data-ttu-id="22c71-146">**키 사용**에는 **암호화**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-146">For **Key usage**, use **Encryption**.</span></span><br>
 <span data-ttu-id="22c71-147">g.</span><span class="sxs-lookup"><span data-stu-id="22c71-147">g.</span></span> <span data-ttu-id="22c71-148">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-148">Select **Create**.</span></span><br>
5. <span data-ttu-id="22c71-149">B2C_1A_FacebookSecret를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-149">Create B2C_1A_FacebookSecret.</span></span> <br>
<span data-ttu-id="22c71-150">Facebook 응용 프로그램 비밀이 이미 있을 경우 해당 비밀을 정책 키로 테넌트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-150">If you already have a Facebook application secret, add it as a policy key to your tenant.</span></span> <span data-ttu-id="22c71-151">그렇지 않으면 정책이 유효성 검사를 통과하도록 자리 표시자 값이 있는 키를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-151">Otherwise, you must create the key with a placeholder value so that your policies pass validation.</span></span><br>
 <span data-ttu-id="22c71-152">a.</span><span class="sxs-lookup"><span data-stu-id="22c71-152">a.</span></span> <span data-ttu-id="22c71-153">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-153">Select **Add**.</span></span><br>
 <span data-ttu-id="22c71-154">b.</span><span class="sxs-lookup"><span data-stu-id="22c71-154">b.</span></span> <span data-ttu-id="22c71-155">**옵션**에는 **수동**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-155">For **Options**, use **Manual**.</span></span><br>
 <span data-ttu-id="22c71-156">c.</span><span class="sxs-lookup"><span data-stu-id="22c71-156">c.</span></span> <span data-ttu-id="22c71-157">**이름**에는 `FacebookSecret`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-157">For **Name**, use `FacebookSecret`.</span></span> <br>
 <span data-ttu-id="22c71-158">`B2C_1A_` 접두사가 자동으로 추가될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-158">The prefix `B2C_1A_` might be added automatically.</span></span><br>
 <span data-ttu-id="22c71-159">d.</span><span class="sxs-lookup"><span data-stu-id="22c71-159">d.</span></span> <span data-ttu-id="22c71-160">**비밀** 상자에서 developers.facebook.com의 FacebookSecret 또는 `0`을 자리 표시자로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-160">In the **Secret** box, enter your FacebookSecret from developers.facebook.com or `0` as a placeholder.</span></span> <span data-ttu-id="22c71-161">*Facebook 앱 ID가 아닙니다.*</span><span class="sxs-lookup"><span data-stu-id="22c71-161">*This is not your Facebook app ID.*</span></span> <br>
 <span data-ttu-id="22c71-162">e.</span><span class="sxs-lookup"><span data-stu-id="22c71-162">e.</span></span> <span data-ttu-id="22c71-163">**키 사용**에는 **서명**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-163">For **Key usage**, use **Signature**.</span></span> <br>
 <span data-ttu-id="22c71-164">f.</span><span class="sxs-lookup"><span data-stu-id="22c71-164">f.</span></span> <span data-ttu-id="22c71-165">**만들기**를 선택하고 이 만들기를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-165">Select **Create** and confirm creation.</span></span>

## <a name="register-identity-experience-framework-applications"></a><span data-ttu-id="22c71-166">ID 경험 프레임워크 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="22c71-166">Register Identity Experience Framework applications</span></span>

<span data-ttu-id="22c71-167">Azure AD B2C에서는 엔진에서 사용자를 등록하고 로그인하는 데 사용하는 두 개의 추가 응용 프로그램을 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-167">Azure AD B2C requires you to register two extra applications that are used by the engine to sign up and sign in users.</span></span>

>[!NOTE]
><span data-ttu-id="22c71-168">로컬 계정을 사용하여 로그인할 수 있는 두 개의 응용 프로그램, 즉 IdentityExperienceFramework(웹앱) 및 IdentityExperienceFramework 앱에서 위임된 권한이 있는 ProxyIdentityExperienceFramework(네이티브 앱)를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-168">You must create two applications that enable sign-in using local accounts: IdentityExperienceFramework (a web app) and ProxyIdentityExperienceFramework (a native app) with delegated permission from the IdentityExperienceFramework app.</span></span> <span data-ttu-id="22c71-169">로컬 계정은 테넌트에만 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-169">Local accounts exist only in your tenant.</span></span> <span data-ttu-id="22c71-170">사용자는 고유한 이메일 주소/암호 조합으로 등록하여 테넌트에 등록된 응용 프로그램에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-170">Your users sign up with a unique email address/password combination to access your tenant-registered applications.</span></span>

### <a name="create-the-identityexperienceframework-application"></a><span data-ttu-id="22c71-171">IdentityExperienceFramework 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="22c71-171">Create the IdentityExperienceFramework application</span></span>

1. <span data-ttu-id="22c71-172">[Azure Portal](https://portal.azure.com)에서 [Azure AD B2C 테넌트의 컨텍스트로 전환합니다](active-directory-b2c-navigate-to-b2c-context.md).</span><span class="sxs-lookup"><span data-stu-id="22c71-172">In the [Azure portal](https://portal.azure.com), switch into the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md).</span></span>
2. <span data-ttu-id="22c71-173">**Azure Active Directory** 블레이드를 엽니다(**Azure AD B2C** 블레이드가 아님).</span><span class="sxs-lookup"><span data-stu-id="22c71-173">Open the **Azure Active Directory** blade (not the **Azure AD B2C** blade).</span></span> <span data-ttu-id="22c71-174">**더 많은 서비스**를 선택하여 찾을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-174">You might need to select **More Services** to find it.</span></span>
3. <span data-ttu-id="22c71-175">**앱 등록**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-175">Select **App registrations**.</span></span>
4. <span data-ttu-id="22c71-176">**새 응용 프로그램 등록**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-176">Select **New application registration**.</span></span>
   * <span data-ttu-id="22c71-177">**이름**에는 `IdentityExperienceFramework`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-177">For **Name**, use `IdentityExperienceFramework`.</span></span>
   * <span data-ttu-id="22c71-178">**응용 프로그램 종류**에는 **웹앱/API**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-178">For **Application type**, use **Web app/API**.</span></span>
   * <span data-ttu-id="22c71-179">**로그온 URL**에는 `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`을 사용합니다. 여기서 `yourtenant`는 Azure AD B2C 테넌트 도메인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-179">For **Sign-on URL**, use `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`, where `yourtenant` is your Azure AD B2C tenant domain name.</span></span>
5. <span data-ttu-id="22c71-180">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-180">Select **Create**.</span></span>
6. <span data-ttu-id="22c71-181">만들어졌으면 새로 만든 **IdentityExperienceFramework** 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-181">Once it is created, select the newly created application **IdentityExperienceFramework**.</span></span><br>
   * <span data-ttu-id="22c71-182">**속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-182">Select **Properties**.</span></span><br>
   * <span data-ttu-id="22c71-183">응용 프로그램 ID를 복사하여 나중에 사용할 수 있도록 저장해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-183">Copy the application ID and save it for later.</span></span>

### <a name="create-the-proxyidentityexperienceframework-application"></a><span data-ttu-id="22c71-184">ProxyIdentityExperienceFramework 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="22c71-184">Create the ProxyIdentityExperienceFramework application</span></span>

1. <span data-ttu-id="22c71-185">**앱 등록**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-185">Select **App registrations**.</span></span>
1. <span data-ttu-id="22c71-186">**새 응용 프로그램 등록**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-186">Select **New application registration**.</span></span>
   * <span data-ttu-id="22c71-187">**이름**에는 `ProxyIdentityExperienceFramework`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-187">For **Name**, use `ProxyIdentityExperienceFramework`.</span></span>
   * <span data-ttu-id="22c71-188">**응용 프로그램 종류**에는 **네이티브**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-188">For **Application type**, use **Native**.</span></span>
   * <span data-ttu-id="22c71-189">**리디렉션 URI**에는 `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`을 사용합니다. 여기서 `yourtenant`는 Azure AD B2C 테넌트입니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-189">For **Redirect URI**, use `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`, where `yourtenant` is your Azure AD B2C tenant.</span></span>
1. <span data-ttu-id="22c71-190">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-190">Select **Create**.</span></span>
1. <span data-ttu-id="22c71-191">만들어졌으면 **ProxyIdentityExperienceFramework** 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-191">Once it has been created, select the application **ProxyIdentityExperienceFramework**.</span></span><br>
   * <span data-ttu-id="22c71-192">**속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-192">Select **Properties**.</span></span> <br>
   * <span data-ttu-id="22c71-193">응용 프로그램 ID를 복사하여 나중에 사용할 수 있도록 저장해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-193">Copy the application ID and save it for later.</span></span>
1. <span data-ttu-id="22c71-194">**필요한 권한**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-194">Select **Required permissions**.</span></span>
1. <span data-ttu-id="22c71-195">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-195">Select **Add**.</span></span>
1. <span data-ttu-id="22c71-196">**API 선택**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-196">Select **Select an API**.</span></span>
1. <span data-ttu-id="22c71-197">IdentityExperienceFramework라는 이름을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-197">Search for the name IdentityExperienceFramework.</span></span> <span data-ttu-id="22c71-198">결과에서 **IdentityExperienceFramework**를 선택하고 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-198">Select **IdentityExperienceFramework** in the results, and then click **Select**.</span></span>
1. <span data-ttu-id="22c71-199">**IdentityExperienceFramework 액세스** 옆의 확인란을 선택한 다음 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-199">Select the check box next to **Access IdentityExperienceFramework**, and then click **Select**.</span></span>
1. <span data-ttu-id="22c71-200">**완료**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-200">Select **Done**.</span></span>
1. <span data-ttu-id="22c71-201">**권한 부여**을 선택하고 **예**를 선택하여 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-201">Select **Grant Permissions**, and then confirm by selecting **Yes**.</span></span>

## <a name="download-starter-pack-and-modify-policies"></a><span data-ttu-id="22c71-202">시작 팩 다운로드 및 정책 수정</span><span class="sxs-lookup"><span data-stu-id="22c71-202">Download starter pack and modify policies</span></span>

<span data-ttu-id="22c71-203">사용자 지정 정책은 Azure AD B2C 테넌트에 업로드해야 하는 일련의 XML 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-203">Custom policies are a set of XML files that need to be uploaded to your Azure AD B2C tenant.</span></span> <span data-ttu-id="22c71-204">Microsoft는 사용자의 신속한 진행을 위해 시작 팩을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-204">We provide starter packs to get you going quickly.</span></span> <span data-ttu-id="22c71-205">다음 목록의 시작 팩 각각에는 설명한 시나리오를 수행하는 데 필요한 최소한의 기술 프로필 및 사용자 경험이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-205">Each starter pack in the following list contains the smallest number of technical profiles and user journeys needed to achieve the scenarios described:</span></span>
 * <span data-ttu-id="22c71-206">LocalAccounts -</span><span class="sxs-lookup"><span data-stu-id="22c71-206">LocalAccounts.</span></span> <span data-ttu-id="22c71-207">로컬 계정만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-207">Enables the use of local accounts only.</span></span>
 * <span data-ttu-id="22c71-208">SocialAccounts -</span><span class="sxs-lookup"><span data-stu-id="22c71-208">SocialAccounts.</span></span> <span data-ttu-id="22c71-209">소셜(또는 페더레이션) 계정만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-209">Enables the use of social (or federated) accounts only.</span></span>
 * <span data-ttu-id="22c71-210">**SocialAndLocalAccounts** -</span><span class="sxs-lookup"><span data-stu-id="22c71-210">**SocialAndLocalAccounts**.</span></span> <span data-ttu-id="22c71-211">이 파일은 연습을 위해 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-211">We use this file for the walkthrough.</span></span>
 * <span data-ttu-id="22c71-212">SocialAndLocalAccountsWithMFA -</span><span class="sxs-lookup"><span data-stu-id="22c71-212">SocialAndLocalAccountsWithMFA.</span></span> <span data-ttu-id="22c71-213">소셜, 로컬 및 Multi-Factor Authentication 옵션이 여기에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-213">Social, local, and Multi-Factor Authentication options are included here.</span></span>

<span data-ttu-id="22c71-214">시작 팩 각각에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-214">Each starter pack contains:</span></span>

* <span data-ttu-id="22c71-215">정책의 [기본 파일](active-directory-b2c-overview-custom.md#policy-files) -</span><span class="sxs-lookup"><span data-stu-id="22c71-215">The [base file](active-directory-b2c-overview-custom.md#policy-files) of the policy.</span></span> <span data-ttu-id="22c71-216">기본 파일에 몇 가지 수정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-216">Few modifications are required to the base.</span></span>
* <span data-ttu-id="22c71-217">정책의 [확장 파일](active-directory-b2c-overview-custom.md#policy-files) -</span><span class="sxs-lookup"><span data-stu-id="22c71-217">The [extension file](active-directory-b2c-overview-custom.md#policy-files) of the policy.</span></span>  <span data-ttu-id="22c71-218">이 파일은 구성이 대부분 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-218">This file is where most configuration changes are made.</span></span>
* <span data-ttu-id="22c71-219">[신뢰 당사자 파일](active-directory-b2c-overview-custom.md#policy-files)은 응용 프로그램에서 호출하는 작업 관련 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-219">[Relying party files](active-directory-b2c-overview-custom.md#policy-files) are task-specific files called by your application.</span></span>

>[!NOTE]
><span data-ttu-id="22c71-220">XML 편집기에서 유효성 검사를 지원하는 경우 시작 팩의 루트 디렉터리에 있는 TrustFrameworkPolicy_0.3.0.0.xsd XML 스키마에 대해 파일의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-220">If your XML editor supports validation, validate the files against the TrustFrameworkPolicy_0.3.0.0.xsd XML schema that is located in the root directory of the starter pack.</span></span> <span data-ttu-id="22c71-221">업로드하기 전에 XML 스키마 유효성 검사가 오류를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-221">XML schema validation identifies errors before uploading.</span></span>

 <span data-ttu-id="22c71-222">이제 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-222">Let's get started:</span></span>

1. <span data-ttu-id="22c71-223">GitHub에서 active-directory-b2c-custom-policy-starterpack을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-223">Download active-directory-b2c-custom-policy-starterpack from GitHub.</span></span> <span data-ttu-id="22c71-224">[.zip 파일을 다운로드](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/archive/master.zip)하거나 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-224">[Download the .zip file](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/archive/master.zip) or run</span></span>

    ```console
    git clone https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack
    ```
2. <span data-ttu-id="22c71-225">SocialAndLocalAccounts 폴더를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-225">Open the SocialAndLocalAccounts folder.</span></span>  <span data-ttu-id="22c71-226">이 폴더의 기본 파일(TrustFrameworkBase.xml)에는 로컬 및 소셜/회사 계정 모두에 필요한 콘텐츠가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-226">The base file (TrustFrameworkBase.xml) in this folder contains content needed for both local and social/corporate accounts.</span></span> <span data-ttu-id="22c71-227">소셜 콘텐츠는 로컬 계정을 가져오고 실행하기 위한 단계를 방해하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-227">The social content does not interfere with the steps for getting local accounts up and running.</span></span>
3. <span data-ttu-id="22c71-228">TrustFrameworkBase.xml을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-228">Open TrustFrameworkBase.xml.</span></span> <span data-ttu-id="22c71-229">XML 편집기가 필요하면 간단한 플랫폼 간 편집기인 [Visual Studio Code를 사용해 보세요](https://code.visualstudio.com/download).</span><span class="sxs-lookup"><span data-stu-id="22c71-229">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
4. <span data-ttu-id="22c71-230">`TrustFrameworkPolicy` 루트 요소에서 `TenantId` 및 `PublicPolicyUri` 특성을 업데이트하여 `yourtenant.onmicrosoft.com`을 Azure AD B2C 테넌트의 도메인 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-230">In the root `TrustFrameworkPolicy` element, update the `TenantId` and `PublicPolicyUri` attributes, replacing `yourtenant.onmicrosoft.com` with the domain name of your Azure AD B2C tenant:</span></span>
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
   ><span data-ttu-id="22c71-231">`PolicyId`는 포털에 표시되는 정책 이름이며, 다른 정책 파일에서 이 정책 파일을 참조하는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-231">`PolicyId` is the policy name that you see in the portal and the name by which this policy file is referenced by other policy files.</span></span>

5. <span data-ttu-id="22c71-232">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-232">Save the file.</span></span>
6. <span data-ttu-id="22c71-233">TrustFrameworkExtensions.xml을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-233">Open TrustFrameworkExtensions.xml.</span></span> <span data-ttu-id="22c71-234">`yourtenant.onmicrosoft.com`을 Azure AD B2C 테넌트로 동일하게 두 번 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-234">Make the same two changes by replacing `yourtenant.onmicrosoft.com` with your Azure AD B2C tenant.</span></span> <span data-ttu-id="22c71-235">`<TenantId>` 요소에서 동일하게 총 세 번 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-235">Make the same replacement in the `<TenantId>` element for a total of three changes.</span></span> <span data-ttu-id="22c71-236">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-236">Save the file.</span></span>
7. <span data-ttu-id="22c71-237">SignUpOrSignIn.xml을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-237">Open SignUpOrSignIn.xml.</span></span> <span data-ttu-id="22c71-238">세 위치에 있는 `yourtenant.onmicrosoft.com`을 Azure AD B2C 테넌트로 바꿔 동일하게 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-238">Make the same changes by replacing `yourtenant.onmicrosoft.com` with your Azure AD B2C tenant in three places.</span></span> <span data-ttu-id="22c71-239">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-239">Save the file.</span></span>
8. <span data-ttu-id="22c71-240">암호 재설정 및 프로필 편집 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-240">Open the password reset and profile edit files.</span></span> <span data-ttu-id="22c71-241">각 파일의 세 위치에 있는 `yourtenant.onmicrosoft.com`을 Azure AD B2C 테넌트로 바꿔 동일하게 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-241">Make the same changes by replacing `yourtenant.onmicrosoft.com` with your Azure AD B2C tenant in three places in each file.</span></span> <span data-ttu-id="22c71-242">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-242">Save the files.</span></span>

### <a name="add-the-application-ids-to-your-custom-policy"></a><span data-ttu-id="22c71-243">사용자 지정 정책에 응용 프로그램 ID 추가</span><span class="sxs-lookup"><span data-stu-id="22c71-243">Add the application IDs to your custom policy</span></span>
<span data-ttu-id="22c71-244">확장 파일(`TrustFrameworkExtensions.xml`)에 응용 프로그램 ID를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-244">Add the application IDs to the extensions file (`TrustFrameworkExtensions.xml`):</span></span>

1. <span data-ttu-id="22c71-245">확장 파일(TrustFrameworkExtensions.xml)을 열고 `<TechnicalProfile Id="login-NonInteractive">` 요소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-245">In the extensions file (TrustFrameworkExtensions.xml), find the element `<TechnicalProfile Id="login-NonInteractive">`.</span></span>
2. <span data-ttu-id="22c71-246">`IdentityExperienceFrameworkAppId`의 두 인스턴스를 이전에 만든 ID 경험 프레임워크의 응용 프로그램 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-246">Replace both instances of `IdentityExperienceFrameworkAppId` with the application ID of the Identity Experience Framework application that you created earlier.</span></span> <span data-ttu-id="22c71-247">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-247">Here is an example:</span></span>

   ```xml
   <Item Key="client_id">8322dedc-cbf4-43bc-8bb6-141d16f0f489</Item>
   ```
3. <span data-ttu-id="22c71-248">`ProxyIdentityExperienceFrameworkAppId`의 두 인스턴스를 이전에 만든 프록시 ID 경험 프레임워크 응용 프로그램의 응용 프로그램 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-248">Replace both instances of `ProxyIdentityExperienceFrameworkAppId` with the application ID of the Proxy Identity Experience Framework application that you created earlier.</span></span>
4. <span data-ttu-id="22c71-249">확장 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-249">Save your extensions file.</span></span>

## <a name="upload-the-policies-to-your-tenant"></a><span data-ttu-id="22c71-250">테넌트에 정책 업로드</span><span class="sxs-lookup"><span data-stu-id="22c71-250">Upload the policies to your tenant</span></span>

1. <span data-ttu-id="22c71-251">[Azure Portal](https://portal.azure.com)에서 [Azure AD B2C 테넌트의 컨텍스트](active-directory-b2c-navigate-to-b2c-context.md)로 전환하고 **Azure AD B2C** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-251">In the [Azure portal](https://portal.azure.com), switch into the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open the **Azure AD B2C** blade.</span></span>
2. <span data-ttu-id="22c71-252">**ID 경험 프레임워크**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-252">Select **Identity Experience Framework**.</span></span>
3. <span data-ttu-id="22c71-253">**정책 업로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-253">Select **Upload Policy**.</span></span>

    >[!WARNING]
    ><span data-ttu-id="22c71-254">다음과 같은 순서로 사용자 지정 정책 파일을 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-254">The custom policy files must be uploaded in the following order:</span></span>

1. <span data-ttu-id="22c71-255">TrustFrameworkBase.xml을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-255">Upload TrustFrameworkBase.xml.</span></span>
2. <span data-ttu-id="22c71-256">TrustFrameworkExtensions.xml을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-256">Upload TrustFrameworkExtensions.xml.</span></span>
3. <span data-ttu-id="22c71-257">SignUpOrSignin.xml을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-257">Upload SignUpOrSignin.xml.</span></span>
4. <span data-ttu-id="22c71-258">다른 정책 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-258">Upload your other policy files.</span></span>

<span data-ttu-id="22c71-259">파일이 업로드되면 정책 파일의 이름 앞에 `B2C_1A_`가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-259">When a file is uploaded, the name of the policy file is prepended with `B2C_1A_`.</span></span>

## <a name="test-the-custom-policy-by-using-run-now"></a><span data-ttu-id="22c71-260">지금 실행을 사용하여 사용자 지정 정책 테스트</span><span class="sxs-lookup"><span data-stu-id="22c71-260">Test the custom policy by using Run Now</span></span>

1. <span data-ttu-id="22c71-261">**Azure AD B2C 설정**을 열고 **ID 경험 프레임워크**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-261">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="22c71-262">**지금 실행**을 사용하려면 하나 이상의 응용 프로그램이 테넌트에 미리 등록되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-262">**Run now** requires at least one application to be preregistered on the tenant.</span></span> <span data-ttu-id="22c71-263">응용 프로그램은 Azure AD B2C의 **응용 프로그램** 메뉴 선택 항목 또는 ID 경험 프레임워크를 통해 기본 제공 정책과 사용자 지정 정책을 모두 호출하여 B2C 테넌트에 등록되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-263">Applications must be registered in the B2C tenant, either by using the **Applications** menu selection in Azure AD B2C or by using the Identity Experience Framework to invoke both built-in and custom policies.</span></span> <span data-ttu-id="22c71-264">응용 프로그램당 한 번만 등록하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-264">Only one registration per application is needed.</span></span><br><br>
   <span data-ttu-id="22c71-265">응용 프로그램을 등록하는 방법은 Azure AD B2C [시작](active-directory-b2c-get-started.md) 문서 또는 [응용 프로그램 등록](active-directory-b2c-app-registration.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="22c71-265">To learn how to register applications, see the Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or the [Application registration](active-directory-b2c-app-registration.md) article.</span></span>  

2. <span data-ttu-id="22c71-266">업로드한 B2C_1A_signup_signin RP(신뢰 당사자) 사용자 지정 정책을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-266">Open B2C_1A_signup_signin, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="22c71-267">**지금 실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-267">Select **Run now**.</span></span>

3. <span data-ttu-id="22c71-268">전자 메일 주소를 사용하여 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-268">You should be able to sign up using an email address.</span></span>

4. <span data-ttu-id="22c71-269">동일한 계정으로 로그인하여 올바르게 구성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-269">Sign in with the same account to confirm that you have the correct configuration.</span></span>

>[!NOTE]
><span data-ttu-id="22c71-270">로그인이 실패하는 것은 일반적으로 잘못 구성된 IdentityExperienceFramework 앱 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-270">A common cause of sign-in failure is an improperly configured IdentityExperienceFramework app.</span></span>


## <a name="next-steps"></a><span data-ttu-id="22c71-271">다음 단계</span><span class="sxs-lookup"><span data-stu-id="22c71-271">Next steps</span></span>

### <a name="add-facebook-as-an-identity-provider"></a><span data-ttu-id="22c71-272">Facebook을 ID 공급자로 추가</span><span class="sxs-lookup"><span data-stu-id="22c71-272">Add Facebook as an identity provider</span></span>
<span data-ttu-id="22c71-273">Facebook을 설정하려면:</span><span class="sxs-lookup"><span data-stu-id="22c71-273">To set up Facebook:</span></span>
1. <span data-ttu-id="22c71-274">[developers.facebook.com에서 Facebook 응용 프로그램을 구성합니다](active-directory-b2c-setup-fb-app.md).</span><span class="sxs-lookup"><span data-stu-id="22c71-274">[Configure a Facebook application in developers.facebook.com](active-directory-b2c-setup-fb-app.md).</span></span>
2. <span data-ttu-id="22c71-275">[Azure AD B2C 테넌트에 Facebook 응용 프로그램 비밀을 추가합니다](#add-signing-and-encryption-keys-to-your-b2c-tenant-for-use-by-custom-policies).</span><span class="sxs-lookup"><span data-stu-id="22c71-275">[Add the Facebook application secret to your Azure AD B2C tenant](#add-signing-and-encryption-keys-to-your-b2c-tenant-for-use-by-custom-policies).</span></span>
3. <span data-ttu-id="22c71-276">TrustFrameworkExtensions 정책 파일에서 `client_id` 값을 Facebook 응용 프로그램 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-276">In the TrustFrameworkExtensions policy file, replace the value of `client_id` with the Facebook application ID:</span></span>

   ```xml
   <TechnicalProfile Id="Facebook-OAUTH">
     <Metadata>
     <!--Replace the value of client_id in this technical profile with the Facebook app ID"-->
       <Item Key="client_id">00000000000000</Item>
   ```
4. <span data-ttu-id="22c71-277">테넌트에 TrustFrameworkExtensions.xml 정책 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-277">Upload the TrustFrameworkExtensions.xml policy file to your tenant.</span></span>
5. <span data-ttu-id="22c71-278">**지금 실행**을 사용하여 테스트하거나 등록된 응용 프로그램에서 바로 정책을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-278">Test by using **Run now** or by invoking the policy directly from your registered application.</span></span>

### <a name="add-azure-active-directory-as-an-identity-provider"></a><span data-ttu-id="22c71-279">Azure Active Directory를 ID 공급자로 추가</span><span class="sxs-lookup"><span data-stu-id="22c71-279">Add Azure Active Directory as an identity provider</span></span>
<span data-ttu-id="22c71-280">이 시작 가이드에서 사용된 기본 파일에는 이미 다른 ID 공급자를 추가하는 데 필요한 내용 일부가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22c71-280">The base file used in this getting started guide already contains some of the content that you need for adding other identity providers.</span></span> <span data-ttu-id="22c71-281">로그인 설정에 대한 자세한 내용은 [Azure Active Directory B2C: Azure AD 계정을 사용하여 로그인](active-directory-b2c-setup-aad-custom.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="22c71-281">For information on setting up sign-ins, see the [Azure Active Directory B2C: Sign in by using Azure AD accounts](active-directory-b2c-setup-aad-custom.md) article.</span></span>

<span data-ttu-id="22c71-282">ID 경험 프레임워크를 사용하는 Azure AD B2C의 사용자 지정 정책에 대한 개요는 [Azure Active Directory B2C: 사용자 지정 정책](active-directory-b2c-overview-custom.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="22c71-282">For an overview of custom policies in Azure AD B2C that use the Identity Experience Framework, see the [Azure Active Directory B2C: Custom policies](active-directory-b2c-overview-custom.md) article.</span></span> 
