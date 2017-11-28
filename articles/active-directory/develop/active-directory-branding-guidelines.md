---
title: "응용 프로그램에 대 한 지침이 aaaBranding | Microsoft Docs"
description: "포괄적인은 toodeveloper 지향 리소스를 Azure Active Directory에 대 한 가이드"
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
ms.openlocfilehash: e43f884c736a0dcb2e6e51293962ef1e2636ad70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="branding-guidelines-for-applications"></a><span data-ttu-id="21588-103">응용 프로그램에 대한 브랜딩 지침</span><span class="sxs-lookup"><span data-stu-id="21588-103">Branding Guidelines for Applications</span></span>
<span data-ttu-id="21588-104">이 항목에서는 hello 브랜딩 Azure Active Directory (Azure AD)와 응용 프로그램을 개발할 때 사용 해야 하는 지침을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="21588-104">This topic discusses hello branding guidelines you should use when developing applications with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="21588-105">이러한 지침은 원할 때 toouse 직장 또는 학교 계정, Azure AD에서 관리 되는 또는 개인 계정 등록 및 로그인 tooyour 응용 프로그램에 대 한 고객에 게 지시 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="21588-105">These guidelines will help direct your customers when they want toouse their work or school account, managed in Azure AD, or their personal account for sign-up and sign-in tooyour application.</span></span>

## <a name="personal-accounts-vs-work-or-school-accounts-from-microsoft"></a><span data-ttu-id="21588-106">Microsoft의 개인 계정과 회사 또는 학교 계정</span><span class="sxs-lookup"><span data-stu-id="21588-106">Personal accounts vs. work or school accounts from Microsoft</span></span>
<span data-ttu-id="21588-107">Microsoft는 두 종류의 사용자 계정을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="21588-107">Microsoft manages two kinds of user accounts:</span></span>

* <span data-ttu-id="21588-108">**개인 계정** (이전의 Windows Live ID).</span><span class="sxs-lookup"><span data-stu-id="21588-108">**Personal accounts** (formerly known as Windows Live ID).</span></span> <span data-ttu-id="21588-109">이러한 계정 간의 hello 관계를 나타내기 *개별* 사용자와 Microsoft, 및는 tooaccess 소비자 장치 및 Microsoft 서비스를에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="21588-109">These accounts represent hello relationship between *individual* users and Microsoft, and are used tooaccess consumer devices and services from Microsoft.</span></span> <span data-ttu-id="21588-110">이 계정은 개인적인 용도를 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="21588-110">These accounts are intended for personal use.</span></span>
* <span data-ttu-id="21588-111">**회사 또는 학교 계정.**</span><span class="sxs-lookup"><span data-stu-id="21588-111">**Work or school accounts.**</span></span> <span data-ttu-id="21588-112">이 계정은 Azure Active Directory를 사용하는 조직을 대신하여 Microsoft에서 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="21588-112">These accounts are managed by Microsoft on behalf of organizations that use Azure Active Directory.</span></span> <span data-ttu-id="21588-113">이러한 계정은 tooOffice 365 및 다른 비즈니스 서비스를 Microsoft에 사용 되는 toosign 됩니다.</span><span class="sxs-lookup"><span data-stu-id="21588-113">These accounts are used toosign in tooOffice 365 and other business services from Microsoft.</span></span>

<span data-ttu-id="21588-114">회사 또는 학교 계정을 일반적으로 Microsoft는 조직 (회사, 학교, 정부 기관)에서 tooend 사용자 (직원, 학생, 연방 직원)을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="21588-114">Microsoft work or school accounts are typically assigned tooend users (employees, students, federal employees) by their organizations (company, school, government agency).</span></span> <span data-ttu-id="21588-115">이러한 계정 중 하나에서 Azure AD hello 플랫폼 또는 Windows Server Active Directory 등의 온-프레미스 디렉터리에서 동기화 된 tooAzure AD hello 클라우드에서 직접 마스터 됩니다.</span><span class="sxs-lookup"><span data-stu-id="21588-115">These accounts are either mastered directly in hello cloud, in hello Azure AD platform, or synced tooAzure AD from an on-premises directory, such as Windows Server Active Directory.</span></span> <span data-ttu-id="21588-116">Microsoft는 hello *보유 하 고* hello 작업 또는 학교 계정 하지만 hello 계정을 소유 하 고 hello 조직에 의해 제어 됩니다.</span><span class="sxs-lookup"><span data-stu-id="21588-116">Microsoft is hello *custodian* of hello work or school accounts, but hello accounts are owned and controlled by hello organization.</span></span>

## <a name="referring-tooazure-ad-accounts-in-your-application"></a><span data-ttu-id="21588-117">응용 프로그램에서 참조 tooAzure AD 계정</span><span class="sxs-lookup"><span data-stu-id="21588-117">Referring tooAzure AD accounts in your application</span></span>
<span data-ttu-id="21588-118">Microsoft 노출 되는 것 최종 사용자에 게 toohello Azure hello Active Directory 브랜드 이름은 및 둘 다 표시 해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="21588-118">Microsoft doesn’t expose end-users toohello Azure or hello Active Directory brand names, and neither should you.</span></span>

* <span data-ttu-id="21588-119">사용자가 로그인 hello 조직 이름 및 가능한 한 로고를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="21588-119">Once users are signed in, you should use hello organization’s name and logo as much as possible.</span></span> <span data-ttu-id="21588-120">이것이 "조직"과 같은 일반적인 용어를 사용하는 것보다 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="21588-120">This is better than using generic terms like “your organization”.</span></span>
* <span data-ttu-id="21588-121">Tootheir 계정으로 참조 해야 사용자가 로그인 하지 않은 경우 "작업 또는 학교 계정" 및 사용 하 여 hello Microsoft 로고 tooconvey 이러한 계정은 Microsoft에서 관리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="21588-121">When users are not signed in, you should refer tootheir accounts as “Work or school accounts” and use hello Microsoft logo tooconvey that these accounts are managed by Microsoft.</span></span> <span data-ttu-id="21588-122">사용자에게 혼동을 줄 수 있는 "엔터프라이즈 계정", "비즈니스 계정" 또는 "회사 계정"과 같은 용어는 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="21588-122">Don’t use terms like “enterprise account”, “business account” or “corporate account” which create user confusion.</span></span>

## <a name="user-account-pictogram"></a><span data-ttu-id="21588-123">사용자 계정 픽토그램</span><span class="sxs-lookup"><span data-stu-id="21588-123">User account pictogram</span></span>
<span data-ttu-id="21588-124">이 지침의 이전 버전에서는 "파란색 배지" 픽토그램을 사용하도록 권장했습니다.</span><span class="sxs-lookup"><span data-stu-id="21588-124">In an earlier version of these guidelines, we recommended using a “blue badge” pictogram.</span></span> <span data-ttu-id="21588-125">사용자와 개발자의 의견에 따라 이제 hello 사용을 좋습니다 hello Microsoft 로고 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="21588-125">Based on user and developer feedback, we now recommend hello use of hello Microsoft logo instead.</span></span> <span data-ttu-id="21588-126">이렇게 하면 사용자가 이해 Office 365 또는 기타 Microsoft 비즈니스 서비스 toosign tooyour 응용 프로그램에서 사용 하는 hello 계정을 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21588-126">This will help users understand that they can reuse hello account they use with Office 365 or other Microsoft business services toosign in tooyour app.</span></span>

## <a name="signing-up-and-signing-in-with-azure-ad"></a><span data-ttu-id="21588-127">Azure AD를 사용한 등록 및 로그인</span><span class="sxs-lookup"><span data-stu-id="21588-127">Signing up and signing in with Azure AD</span></span>
<span data-ttu-id="21588-128">앱 등록 및 로그인에 대 한 별도 경로 표시 될 수 있습니다 및 다음 섹션 hello 두 시나리오 모두에 대 한 시각적 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="21588-128">Your app may present separate paths for sign-up and sign-in and hello following sections provide visual guidance for both scenarios.</span></span>

<span data-ttu-id="21588-129">**응용 프로그램 (예: 무료 tootrial 또는 freemium 모델) 최종 사용자 등록을 지 원하는 경우**: 표시할 수 있습니다는 **로그인** tooaccess 사용자가 회사 계정 또는 개인 계정으로 사용 하 여 앱을 허용 하는 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="21588-129">**If your app supports end user sign up (e.g. free tootrial or freemium model)**: You can show a **sign-in** button that allows users tooaccess your app with their work account or their personal account.</span></span> <span data-ttu-id="21588-130">Azure AD는 앱에 액세스 하는 처음으로 동의 프롬프트 hello를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="21588-130">Azure AD will show a consent prompt hello first time they access your app.</span></span>

<span data-ttu-id="21588-131">**관리자만 동의할 수 있는 권한을 요구하는 앱 또는 조직 라이선스가 필요한 앱의 경우**: 관리 취득과 사용자 로그인을 분리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="21588-131">**If your app requires permissions that only admins can consent to, or if your app requires organizational licensing**: You should separate admin acquisition from user sign in.</span></span> <span data-ttu-id="21588-132">hello **"이이 앱을 다운로드" 단추** 는에서 admins toosign 리디렉션 후 조직에서 사용자를 대신해 서 toogrant 동의 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="21588-132">hello **“get this app” button** will redirect admins toosign in then ask them toogrant consent on behalf of users in their organization.</span></span> <span data-ttu-id="21588-133">이 최종 사용자가 동의 프롬프트 tooyour 응용 프로그램을 표시 하지 않는 추가적인된 이점을 hello 했습니다.</span><span class="sxs-lookup"><span data-stu-id="21588-133">This has hello added benefit of suppressing end users consent prompts tooyour app.</span></span>

## <a name="visual-guidance-for-app-acquisition"></a><span data-ttu-id="21588-134">앱 구입에 대한 시각적 지침</span><span class="sxs-lookup"><span data-stu-id="21588-134">Visual guidance for app acquisition</span></span>
<span data-ttu-id="21588-135">"Hello 응용 프로그램 가져오기" 링크가 리디렉션하여 hello 사용자 toohello Azure AD 액세스 권한 부여 (권한 부여) 페이지, tooallow 조직의 관리자 tooauthorize 앱 toohave Microsoft에서 호스팅하는 tootheir 조직 데이터에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="21588-135">Your “get hello app” link must redirect hello user toohello Azure AD grant access (authorize) page, tooallow an organization’s administrator tooauthorize your app toohave access tootheir organization’s data that is hosted by Microsoft.</span></span> <span data-ttu-id="21588-136">Toorequest 액세스가 hello에 대해서는 설명에 대 한 내용은 [Azure Active Directory와 응용 프로그램 통합](active-directory-integrating-applications.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="21588-136">Details on how toorequest access are discussed in hello [Integrating Applications with Azure Active Directory](active-directory-integrating-applications.md) article.</span></span>

<span data-ttu-id="21588-137">Tooyour 응용 프로그램 관리자가 동의 후 tooadd 선택할 수 있는 것 tootheir 사용자의 Office 365 앱 시작 관리자 환경을 (및 hello waffle에서 액세스할 수 있는 [https://portal.office.com/myapps](https://portal.office.com/myapps)).</span><span class="sxs-lookup"><span data-stu-id="21588-137">After admins consent tooyour app, they can choose tooadd it tootheir users’ Office 365 app launcher experience (accessible from hello waffle and from [https://portal.office.com/myapps](https://portal.office.com/myapps)).</span></span> <span data-ttu-id="21588-138">이 기능은 tooadvertise을 원하는 경우 "이 앱 tooyour 조직 추가" 및 다음과 같은 단추 표시와 같은 용어를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21588-138">If you want tooadvertise this capability, you can use terms like “Add this app tooyour organization” and show a button like this:</span></span>

![응용 프로그램 종류 및 시나리오](./media/active-directory-branding-guidelines/add-to-my-org.png)

<span data-ttu-id="21588-140">그러나 단추에 의존하는 대신 설명 텍스트를 작성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="21588-140">However, we recommend that you write explanatory text instead of relying on buttons.</span></span> <span data-ttu-id="21588-141">예:</span><span class="sxs-lookup"><span data-stu-id="21588-141">For example:</span></span>

> <span data-ttu-id="21588-142">*이미 Office 365 또는 Microsoft의 다른 비즈니스 서비스를 사용 하는 경우 단순히 < your_app_name > 액세스 tooyour 조직 데이터를 부여할 수 있습니다. 기존 작업 계정 사용 하면 사용자가 tooaccess < your_app_name > 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="21588-142">*If you already use Office 365 or other business service from Microsoft, you can simply grant <your_app_name> access tooyour organization’s data. This will allow your users tooaccess <your_app_name> with their existing work accounts.*</span></span>
> 
> 

## <a name="visual-guidance-for-sign-in"></a><span data-ttu-id="21588-143">로그인에 대한 시각적 지침</span><span class="sxs-lookup"><span data-stu-id="21588-143">Visual guidance for sign-in</span></span>
<span data-ttu-id="21588-144">앱은 사용자 toohello 로그인에 끝점 toohello 프로토콜 toointegrate를 사용 하 여 Azure AD에 해당 하는 리디렉션하는 단추에 대 한 기호를 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="21588-144">Your app should display a sign in button that redirects users toohello sign-in endpoint that corresponds toohello protocol you use toointegrate with Azure AD.</span></span> <span data-ttu-id="21588-145">hello 섹션 뒤 해당 단추의 모양 내용에 대해 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="21588-145">hello following section provides details on what that button should look like.</span></span>

### <a name="pictogram-and-sign-in-with-microsoft"></a><span data-ttu-id="21588-146">픽토그램 및 “Microsoft 로그인”</span><span class="sxs-lookup"><span data-stu-id="21588-146">Pictogram and “Sign in with Microsoft”</span></span>
<span data-ttu-id="21588-147">Azure AD에 앱이 지원할 수 기타 id 공급자를 고유 하 게 나타내는 hello Microsoft 로고 및 hello "Sign in with Microsoft" 조건을 hello 연결의 것입니다.</span><span class="sxs-lookup"><span data-stu-id="21588-147">It’s hello association of hello Microsoft logo and hello “Sign in with Microsoft” terms that uniquely represents Azure AD amongst other identity providers your app may support.</span></span> <span data-ttu-id="21588-148">"Sign in with Microsoft"에 대 한 충분 한 공간이 없으면 확인 tooshorten 것 너무 "로그인" 됩니다.</span><span class="sxs-lookup"><span data-stu-id="21588-148">If you don’t have enough space for “Sign in with Microsoft,” it’s ok tooshorten it too“Sign in”.</span></span>

![응용 프로그램 종류 및 시나리오](./media/active-directory-branding-guidelines/sign-in-with-microsoft-light.png)

![응용 프로그램 종류 및 시나리오](./media/active-directory-branding-guidelines/sign-in-light.png)

<span data-ttu-id="21588-151">또한 hello 단추에 대 한 어둡게 색 구성표를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21588-151">You can also use a dark color scheme for hello buttons.</span></span>

![응용 프로그램 종류 및 시나리오](./media/active-directory-branding-guidelines/sign-in-with-microsoft-dark.png)

![응용 프로그램 종류 및 시나리오](./media/active-directory-branding-guidelines/sign-in-dark.png)

## <a name="branding-dos-and-donts"></a><span data-ttu-id="21588-154">브랜딩 관련 할 일과 하지 말아야 할 일</span><span class="sxs-lookup"><span data-stu-id="21588-154">Branding Do’s and Don’ts</span></span>
<span data-ttu-id="21588-155">**수행** hello "Sign in with Microsoft" 단추 tooprovide 추가 설명 toohelp 최종 사용자와 함께에서 "업무 또는 학교 계정"을 사용 하 여 인식 여부를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21588-155">**DO** use “work or school account” in combination with hello "Sign in with Microsoft" button tooprovide additional explanation toohelp end-users recognize whether they can use it.</span></span> <span data-ttu-id="21588-156">**권장 안 함** "엔터프라이즈 계정", "비즈니스 계정" 또는 "회사 계정"과 같은 다른 용어는 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="21588-156">**DON’T** use other terms such as “enterprise account”, “business account” or “corporate account.”</span></span>

<span data-ttu-id="21588-157">**권장 안 함** “Office 365 ID” 또는 “Azure ID”를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="21588-157">**DON’T** use “Office 365 ID” or “Azure ID”.</span></span> <span data-ttu-id="21588-158">Office 365 인증에 대 한 Azure AD를 사용 하지 않는 Microsoft에서 제공 하는 소비자의 hello 이름 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="21588-158">Office 365 is also hello name of a consumer offering from Microsoft which doesn’t use Azure AD for authentication.</span></span>

<span data-ttu-id="21588-159">**안 함** hello Microsoft 로고를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="21588-159">**DON’T** alter hello Microsoft logo.</span></span>

<span data-ttu-id="21588-160">**안 함** toohello 또는 Azure Active Directory 브랜드를 최종 사용자가 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="21588-160">**DON’T** expose end-users toohello Azure or Active Directory brands.</span></span> <span data-ttu-id="21588-161">그러나 해도 됩니다 toouse 이러한 단어와 함께 개발자, IT 전문가 및 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="21588-161">It’s ok however toouse these terms with developers, IT pros and admins.</span></span>

## <a name="navigation-dos-and-donts"></a><span data-ttu-id="21588-162">탐색 관련 할 일과 하지 말아야 할 일</span><span class="sxs-lookup"><span data-stu-id="21588-162">Navigation Do’s and Don’ts</span></span>
<span data-ttu-id="21588-163">**수행** 아웃 사용자 toosign는 방법을 제공 하 고 tooanother 사용자 계정 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="21588-163">**DO** provide a way for users toosign out and switch tooanother user account.</span></span> <span data-ttu-id="21588-164">대부분의 사람들은 Microsoft/Facebook/Google/Twitter의 단일 개인 계정을 가지고 있지만, 사람들은 종종 여러 조직과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="21588-164">While most people have a single personal account from Microsoft/Facebook/Google/Twitter, people are often associated with more than one organization.</span></span> <span data-ttu-id="21588-165">여러 명의 로그인한 사용자에 대한 지원이 곧 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="21588-165">Support for multiple signed-in users is coming soon.</span></span>

