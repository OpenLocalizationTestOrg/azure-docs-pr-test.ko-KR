---
title: "응용 프로그램에 대한 브랜딩 지침 | Microsoft Docs"
description: "Azure Active Directory의 개발자 중심 리소스에 대한 포괄적인 가이드"
services: active-directory
documentationcenter: dev-center-name
author: skwan
manager: mbaldwin
editor: 
ms.assetid: 72f4e464-1352-4a49-a18f-c37f58e7d5c4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: skwan
ms.custom: aaddev
ms.openlocfilehash: 4f6806cde52ce965a8f78a5cce8a24c3d1248594
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="branding-guidelines-for-applications"></a><span data-ttu-id="7507e-103">응용 프로그램에 대한 브랜딩 지침</span><span class="sxs-lookup"><span data-stu-id="7507e-103">Branding Guidelines for Applications</span></span>
<span data-ttu-id="7507e-104">이 항목에서는 Azure Active Directory(Azure AD)를 사용해 응용 프로그램을 개발할 때 사용해야 하는 브랜딩 지침에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-104">This topic discusses the branding guidelines you should use when developing applications with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="7507e-105">이 지침은 Azure AD에서 관리되는 회사 또는 학교 계정, 또는 개인 계정을 응용 프로그램을 등록하고 로그인하는 데 사용하려는 고객을 안내하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-105">These guidelines will help direct your customers when they want to use their work or school account, managed in Azure AD, or their personal account for sign-up and sign-in to your application.</span></span>

## <a name="personal-accounts-vs-work-or-school-accounts-from-microsoft"></a><span data-ttu-id="7507e-106">Microsoft의 개인 계정과 회사 또는 학교 계정</span><span class="sxs-lookup"><span data-stu-id="7507e-106">Personal accounts vs. work or school accounts from Microsoft</span></span>
<span data-ttu-id="7507e-107">Microsoft는 두 종류의 사용자 계정을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-107">Microsoft manages two kinds of user accounts:</span></span>

* <span data-ttu-id="7507e-108">**개인 계정** (이전의 Windows Live ID).</span><span class="sxs-lookup"><span data-stu-id="7507e-108">**Personal accounts** (formerly known as Windows Live ID).</span></span> <span data-ttu-id="7507e-109">이 계정은 *개인* 사용자와 Microsoft 사이의 관계를 나타내며 Microsoft의 소비자 장치 및 서비스에 액세스하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-109">These accounts represent the relationship between *individual* users and Microsoft, and are used to access consumer devices and services from Microsoft.</span></span> <span data-ttu-id="7507e-110">이 계정은 개인적인 용도를 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-110">These accounts are intended for personal use.</span></span>
* <span data-ttu-id="7507e-111">**회사 또는 학교 계정.**</span><span class="sxs-lookup"><span data-stu-id="7507e-111">**Work or school accounts.**</span></span> <span data-ttu-id="7507e-112">이 계정은 Azure Active Directory를 사용하는 조직을 대신하여 Microsoft에서 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-112">These accounts are managed by Microsoft on behalf of organizations that use Azure Active Directory.</span></span> <span data-ttu-id="7507e-113">이 계정은 Office 365 및 Microsoft의 다른 비즈니스 서비스에 로그인하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-113">These accounts are used to sign in to Office 365 and other business services from Microsoft.</span></span>

<span data-ttu-id="7507e-114">Microsoft 회사 또는 학교 계정은 일반적으로 회사, 학교, 정부 기관 등의 조직이 직원, 학생, 연방 직원 등의 최종 사용자에게 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-114">Microsoft work or school accounts are typically assigned to end users (employees, students, federal employees) by their organizations (company, school, government agency).</span></span> <span data-ttu-id="7507e-115">이 계정은 Azure AD 플랫폼을 통해 클라우드에서 직접 마스터되거나 온-프레미스 디렉터리(예: Windows Server Active Directory)에서 Azure AD로 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-115">These accounts are either mastered directly in the cloud, in the Azure AD platform, or synced to Azure AD from an on-premises directory, such as Windows Server Active Directory.</span></span> <span data-ttu-id="7507e-116">Microsoft는 회사 또는 학교 계정의 *보유자* 이지만, 이 계정을 소유하고 제어하는 것은 조직입니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-116">Microsoft is the *custodian* of the work or school accounts, but the accounts are owned and controlled by the organization.</span></span>

## <a name="referring-to-azure-ad-accounts-in-your-application"></a><span data-ttu-id="7507e-117">응용 프로그램에서 Azure AD 계정 언급</span><span class="sxs-lookup"><span data-stu-id="7507e-117">Referring to Azure AD accounts in your application</span></span>
<span data-ttu-id="7507e-118">Microsoft는 Azure 또는 Active Directory 브랜드 이름에 최종 사용자를 노출하지 않으며 이 규칙을 강제합니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-118">Microsoft doesn’t expose end-users to the Azure or the Active Directory brand names, and neither should you.</span></span>

* <span data-ttu-id="7507e-119">사용자가 로그인되어 있으면 가능한 한 조직의 이름 및 로고를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-119">Once users are signed in, you should use the organization’s name and logo as much as possible.</span></span> <span data-ttu-id="7507e-120">이것이 "조직"과 같은 일반적인 용어를 사용하는 것보다 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-120">This is better than using generic terms like “your organization”.</span></span>
* <span data-ttu-id="7507e-121">사용자가 로그인되어 있지 않으면 사용자의 계정을 “회사 또는 학교 계정”으로 언급하고 이 계정을 Microsoft가 관리한다는 것을 전달하기 위해 Microsoft 로고를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-121">When users are not signed in, you should refer to their accounts as “Work or school accounts” and use the Microsoft logo to convey that these accounts are managed by Microsoft.</span></span> <span data-ttu-id="7507e-122">사용자에게 혼동을 줄 수 있는 "엔터프라이즈 계정", "비즈니스 계정" 또는 "회사 계정"과 같은 용어는 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="7507e-122">Don’t use terms like “enterprise account”, “business account” or “corporate account” which create user confusion.</span></span>

## <a name="user-account-pictogram"></a><span data-ttu-id="7507e-123">사용자 계정 픽토그램</span><span class="sxs-lookup"><span data-stu-id="7507e-123">User account pictogram</span></span>
<span data-ttu-id="7507e-124">이 지침의 이전 버전에서는 "파란색 배지" 픽토그램을 사용하도록 권장했습니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-124">In an earlier version of these guidelines, we recommended using a “blue badge” pictogram.</span></span> <span data-ttu-id="7507e-125">사용자와 개발자의 의견을 반영하여 이제 그 대신 Microsoft 로고를 사용할 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-125">Based on user and developer feedback, we now recommend the use of the Microsoft logo instead.</span></span> <span data-ttu-id="7507e-126">그러면 사용자들이 Office 365 또는 기타 Microsoft 비즈니스 서비스에 사용하는 계정을 앱 로그인에 다시 사용할 수 있다는 점을 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-126">This will help users understand that they can reuse the account they use with Office 365 or other Microsoft business services to sign in to your app.</span></span>

## <a name="signing-up-and-signing-in-with-azure-ad"></a><span data-ttu-id="7507e-127">Azure AD를 사용한 등록 및 로그인</span><span class="sxs-lookup"><span data-stu-id="7507e-127">Signing up and signing in with Azure AD</span></span>
<span data-ttu-id="7507e-128">앱의 등록 경로와 로그인 경로가 별도로 제공될 수 있으며, 다음 섹션에서는 두 시나리오에 대한 시각적인 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-128">Your app may present separate paths for sign-up and sign-in and the following sections provide visual guidance for both scenarios.</span></span>

<span data-ttu-id="7507e-129">**최종 사용자 등록을 지원하는 앱의 경우(예: 무료 평가판 또는 프리미엄(freemium) 모델)**: 사용자가 회사 또는 개인 계정을 사용하여 앱에 액세스하는 데 사용할 수 있는 **로그인** 단추를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-129">**If your app supports end user sign up (e.g. free to trial or freemium model)**: You can show a **sign-in** button that allows users to access your app with their work account or their personal account.</span></span> <span data-ttu-id="7507e-130">사용자가 처음으로 앱에 액세스할 때 Azure AD에서 동의하도록 요구하는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-130">Azure AD will show a consent prompt the first time they access your app.</span></span>

<span data-ttu-id="7507e-131">**관리자만 동의할 수 있는 권한을 요구하는 앱 또는 조직 라이선스가 필요한 앱의 경우**: 관리 취득과 사용자 로그인을 분리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-131">**If your app requires permissions that only admins can consent to, or if your app requires organizational licensing**: You should separate admin acquisition from user sign in.</span></span> <span data-ttu-id="7507e-132">**"이 앱 가져오기" 단추** 는 관리자에게 로그인하도록 리디렉션한 다음 조직의 사용자를 대신하여 동의하도록 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-132">The **“get this app” button** will redirect admins to sign in then ask them to grant consent on behalf of users in their organization.</span></span> <span data-ttu-id="7507e-133">이 기능은 최종 사용자 동의를 요청하는 메시지를 표시하지 않게 하는 기능을 앱에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-133">This has the added benefit of suppressing end users consent prompts to your app.</span></span>

## <a name="visual-guidance-for-app-acquisition"></a><span data-ttu-id="7507e-134">앱 구입에 대한 시각적 지침</span><span class="sxs-lookup"><span data-stu-id="7507e-134">Visual guidance for app acquisition</span></span>
<span data-ttu-id="7507e-135">"앱 가져오기" 링크는 Azure AD 액세스 권한 부여(권한 부여) 페이지로 사용자를 리디렉션해야 합니다. 그러면 조직 관리자가 앱이 Microsoft에서 호스트되는 조직 데이터에 액세스할 수 있게 승인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-135">Your “get the app” link must redirect the user to the Azure AD grant access (authorize) page, to allow an organization’s administrator to authorize your app to have access to their organization’s data that is hosted by Microsoft.</span></span> <span data-ttu-id="7507e-136">액세스 권한을 요청하는 방법에 대한 자세한 내용은 [Azure Active Directory와 응용 프로그램 통합](active-directory-integrating-applications.md) 항목에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-136">Details on how to request access are discussed in the [Integrating Applications with Azure Active Directory](active-directory-integrating-applications.md) article.</span></span>

<span data-ttu-id="7507e-137">관리자가 앱에 동의한 후에는 사용자의 Office 365 앱 시작 관리자 환경(와플 및 [https://portal.office.com/myapps](https://portal.office.com/myapps)에서 액세스 가능)에 앱을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-137">After admins consent to your app, they can choose to add it to their users’ Office 365 app launcher experience (accessible from the waffle and from [https://portal.office.com/myapps](https://portal.office.com/myapps)).</span></span> <span data-ttu-id="7507e-138">이 기능을 보급하려는 경우 "조직에 이 앱 추가"와 같은 용어를 사용하고 다음과 같은 단추를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-138">If you want to advertise this capability, you can use terms like “Add this app to your organization” and show a button like this:</span></span>

![응용 프로그램 종류 및 시나리오](./media/active-directory-branding-guidelines/add-to-my-org.png)

<span data-ttu-id="7507e-140">그러나 단추에 의존하는 대신 설명 텍스트를 작성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-140">However, we recommend that you write explanatory text instead of relying on buttons.</span></span> <span data-ttu-id="7507e-141">예:</span><span class="sxs-lookup"><span data-stu-id="7507e-141">For example:</span></span>

> <span data-ttu-id="7507e-142">*미 Office 365 또는Microsoft의 다른 비즈니스 서비스를 사용하는 경우 조직의 데이터에 대한 <your_app_name> 액세스 권한을 부여하면 됩니다. 이렇게 하면 사용자들이 기존 회사 계정으로 <your_app_name>에 액세스할 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="7507e-142">*If you already use Office 365 or other business service from Microsoft, you can simply grant <your_app_name> access to your organization’s data. This will allow your users to access <your_app_name> with their existing work accounts.*</span></span>
> 
> 

## <a name="visual-guidance-for-sign-in"></a><span data-ttu-id="7507e-143">로그인에 대한 시각적 지침</span><span class="sxs-lookup"><span data-stu-id="7507e-143">Visual guidance for sign-in</span></span>
<span data-ttu-id="7507e-144">앱은 Azure AD와 통합하는 데 사용하는 프로토콜에 해당하는 로그인 끝점으로 사용자를 리디렉션하는 로그인 단추를 표시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-144">Your app should display a sign in button that redirects users to the sign-in endpoint that corresponds to the protocol you use to integrate with Azure AD.</span></span> <span data-ttu-id="7507e-145">다음 섹션에서는 이 단추의 모양을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-145">The following section provides details on what that button should look like.</span></span>

### <a name="pictogram-and-sign-in-with-microsoft"></a><span data-ttu-id="7507e-146">픽토그램 및 “Microsoft 로그인”</span><span class="sxs-lookup"><span data-stu-id="7507e-146">Pictogram and “Sign in with Microsoft”</span></span>
<span data-ttu-id="7507e-147">Microsoft 로고와 앱이 지원하는 다른 ID 공급자 중에서 Azure AD를 고유하게 나타내는 “Microsoft 로그인”이라는 일반 용어를 결합한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-147">It’s the association of the Microsoft logo and the “Sign in with Microsoft” terms that uniquely represents Azure AD amongst other identity providers your app may support.</span></span> <span data-ttu-id="7507e-148">공간이 부족하여 "Microsoft 로그인"을 사용할 수 없는 경우에는 "로그인"으로 줄여도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-148">If you don’t have enough space for “Sign in with Microsoft,” it’s ok to shorten it to “Sign in”.</span></span>

![응용 프로그램 종류 및 시나리오](./media/active-directory-branding-guidelines/sign-in-with-microsoft-light.png)

![응용 프로그램 종류 및 시나리오](./media/active-directory-branding-guidelines/sign-in-light.png)

<span data-ttu-id="7507e-151">단추에 어두운 색 구성표를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-151">You can also use a dark color scheme for the buttons.</span></span>

![응용 프로그램 종류 및 시나리오](./media/active-directory-branding-guidelines/sign-in-with-microsoft-dark.png)

![응용 프로그램 종류 및 시나리오](./media/active-directory-branding-guidelines/sign-in-dark.png)

## <a name="branding-dos-and-donts"></a><span data-ttu-id="7507e-154">브랜딩 관련 할 일과 하지 말아야 할 일</span><span class="sxs-lookup"><span data-stu-id="7507e-154">Branding Do’s and Don’ts</span></span>
<span data-ttu-id="7507e-155">**권장** 최종 사용자가 단추를 사용할 수 있는지 여부를 인식할 수 있도록, 추가 설명을 제공하기 위해 "회사 또는 학교 계정"을 "Microsoft 로그인" 단추와 함께 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-155">**DO** use “work or school account” in combination with the "Sign in with Microsoft" button to provide additional explanation to help end-users recognize whether they can use it.</span></span> <span data-ttu-id="7507e-156">**권장 안 함** "엔터프라이즈 계정", "비즈니스 계정" 또는 "회사 계정"과 같은 다른 용어는 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-156">**DON’T** use other terms such as “enterprise account”, “business account” or “corporate account.”</span></span>

<span data-ttu-id="7507e-157">**권장 안 함** “Office 365 ID” 또는 “Azure ID”를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-157">**DON’T** use “Office 365 ID” or “Azure ID”.</span></span> <span data-ttu-id="7507e-158">Office 365는 인증을 위해 Azure AD를 사용하지 않는 Microsoft 소비자 서비스의 이름이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-158">Office 365 is also the name of a consumer offering from Microsoft which doesn’t use Azure AD for authentication.</span></span>

<span data-ttu-id="7507e-159">**권장 안 함** Microsoft 로고를 변경하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-159">**DON’T** alter the Microsoft logo.</span></span>

<span data-ttu-id="7507e-160">**장 안 함** Azure 또는 Active Directory에 최종 사용자를 노출하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-160">**DON’T** expose end-users to the Azure or Active Directory brands.</span></span> <span data-ttu-id="7507e-161">그러나 개발자, IT 전문가, 관리자에 대해서는 이 용어를 사용해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-161">It’s ok however to use these terms with developers, IT pros and admins.</span></span>

## <a name="navigation-dos-and-donts"></a><span data-ttu-id="7507e-162">탐색 관련 할 일과 하지 말아야 할 일</span><span class="sxs-lookup"><span data-stu-id="7507e-162">Navigation Do’s and Don’ts</span></span>
<span data-ttu-id="7507e-163">**권장** 사용자가 로그아웃한 후 다른 사용자 계정으로 전환하는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-163">**DO** provide a way for users to sign out and switch to another user account.</span></span> <span data-ttu-id="7507e-164">대부분의 사람들은 Microsoft/Facebook/Google/Twitter의 단일 개인 계정을 가지고 있지만, 사람들은 종종 여러 조직과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-164">While most people have a single personal account from Microsoft/Facebook/Google/Twitter, people are often associated with more than one organization.</span></span> <span data-ttu-id="7507e-165">여러 명의 로그인한 사용자에 대한 지원이 곧 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="7507e-165">Support for multiple signed-in users is coming soon.</span></span>

