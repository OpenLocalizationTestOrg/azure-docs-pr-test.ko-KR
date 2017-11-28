---
title: "내 응용 프로그램 목록에서 응용 프로그램 aaaUnexpected | Microsoft Docs"
description: "어떻게 toosee 테 넌 트의 모든 응용 프로그램이 고 응용 프로그램이 엔터프라이즈 응용 프로그램에서 모든 응용 프로그램 목록에 나타나는 방식을 이해"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 2f974046b655bc36a05f002c56511a8a988cd01c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-application-in-my-applications-list"></a><span data-ttu-id="2c758-103">내 응용 프로그램 목록에 예기치 않은 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="2c758-103">Unexpected application in my applications list</span></span>

<span data-ttu-id="2c758-104">이 문서가 도움이 응용 프로그램에 표시 되는 방식을 toounderstand 프로그램 **모든 응용 프로그램** 목록에서 **엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c758-104">This article help you toounderstand how applications appear in your **All Applications** list under **Enterprise Applications**.</span></span> 

## <a name="how-toosee-all-applications-in-your-tenant"></a><span data-ttu-id="2c758-105">어떻게 toosee 테 넌 트의 모든 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="2c758-105">How toosee all applications in your tenant</span></span>

<span data-ttu-id="2c758-106">toosee 모든 hello 테 넌 트에 응용 프로그램, toouse hello 필요한 **필터** tooshow 제어 **모든 응용 프로그램** hello에서 **모든 응용 프로그램** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="2c758-106">toosee all hello applications in your tenant, you need toouse hello **Filter** control tooshow **All Applications** under hello **All Applications** list.</span></span> <span data-ttu-id="2c758-107">toodo 다음,이 따라 hello 단계:</span><span class="sxs-lookup"><span data-stu-id="2c758-107">toodo this, follow hello steps below:</span></span>

1.  <span data-ttu-id="2c758-108">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="2c758-108">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="2c758-109">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c758-109">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2c758-110">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="2c758-110">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2c758-111">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c758-111">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2c758-112">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="2c758-112">click **All Applications** tooview a list of all your applications.</span></span>

6.  <span data-ttu-id="2c758-113">hello 사용 하 여 hello 클릭 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록**합니다.</span><span class="sxs-lookup"><span data-stu-id="2c758-113">click hello use hello **Filter** control at hello top of hello **All Applications List**.</span></span>

7.  <span data-ttu-id="2c758-114">Hello에 **필터** 블레이드, 집합 hello **표시** 옵션**모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="2c758-114">On hello **Filter** blade, set hello **Show** option too**All Applications.**</span></span>

## <a name="why-does-a-specific-application-appear-in-my-all-applications-list"></a><span data-ttu-id="2c758-115">내 모든 응용 프로그램 목록에 특정 응용 프로그램이 나타나는 이유는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="2c758-115">Why does a specific application appear in my all applications list?</span></span>

<span data-ttu-id="2c758-116">너무 필터링 할 때**모든 응용 프로그램**, hello **모든 응용 프로그램** **목록** 테 넌 트의 모든 서비스 사용자 개체를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2c758-116">When filtered too**All Applications**, hello **All Applications** **List** shows every Service Principal object in your tenant.</span></span> <span data-ttu-id="2c758-117">서비스 주체 개체는 다양한 방법으로 이 목록에 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c758-117">Service Principal objects can appear in this list in a various ways:</span></span>

1.  <span data-ttu-id="2c758-118">Hello 응용 프로그램 갤러리에서 모든 응용 프로그램을 추가 하는 경우 포함 하 여:</span><span class="sxs-lookup"><span data-stu-id="2c758-118">When you add any application from hello application gallery, including:</span></span>

   1. <span data-ttu-id="2c758-119">**Azure AD 갤러리 응용 프로그램** – Single Sign-On에 대해 Azure AD와 사전 통합된 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="2c758-119">**Azure AD Gallery Applications** – An application that has been pre-integrated for single sign-on with Azure AD.</span></span>

   2. <span data-ttu-id="2c758-120">**응용 프로그램 프록시 응용 프로그램** – tooprovide 보안 single sign-on tooexternally 원하는 온-프레미스 환경에서 실행 중인 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="2c758-120">**Application Proxy Applications** – An application running in your on-premises environment that you want tooprovide secure single-sign on tooexternally.</span></span>

   3. <span data-ttu-id="2c758-121">**사용자 지정 응용 프로그램 개발** – 조직에서 toodevelop 하지 않고자 한다면 응용 프로그램에 Azure AD 응용 프로그램 개발 플랫폼 hello 하지만 아직 존재 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c758-121">**Custom-developed Applications** – An application that your organization wishes toodevelop on hello Azure AD Application Development Platform, but that may not exist yet.</span></span>

   4. <span data-ttu-id="2c758-122">**비 갤러리 응용 프로그램** – 사용자의 응용 프로그램을 가져옵니다!</span><span class="sxs-lookup"><span data-stu-id="2c758-122">**Non-Gallery Applications** – Bring your own applications!</span></span> <span data-ttu-id="2c758-123">원하는 모든 웹 링크 또는 사용자 이름 및 암호 필드를 렌더링 하는 응용 프로그램에는 SAML 또는 OpenID Connect 프로토콜을 지원 또는 Azure ad에서 single sign-on toointegrate 복원할 SCIM를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c758-123">Any web link you want, or any application which renders a username and password field, supports SAML or OpenID Connect protocols, or supports SCIM which you wish toointegrate for single sign-on with Azure AD.</span></span>

2.  <span data-ttu-id="2c758-124">Azure Active Directory와 통합된 타<sup>사</sup> 응용 프로그램에 등록하거나 로그인하는 경우.</span><span class="sxs-lookup"><span data-stu-id="2c758-124">When signing up for, or signing in to, a 3<sup>rd</sup> party application integrated with Azure Active Directory.</span></span> <span data-ttu-id="2c758-125">한 가지 예로 [Smartsheet](https://app.smartsheet.com/b/home) 또는 [DocuSign](https://www.docusign.net/member/MemberLogin.aspx)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c758-125">One example of this is [Smartsheet](https://app.smartsheet.com/b/home) or [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).</span></span>

3.  <span data-ttu-id="2c758-126">에 등록, 라이선스 tooa 사용자 또는 그룹 tooa 첫 번째 파티 응용을 추가 하거나 때와 같은 [Microsoft Office 365](http://products.office.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c758-126">When signing up for, or adding a license tooa user or a group tooa first party application, like [Microsoft Office 365](http://products.office.com/).</span></span>

4.  <span data-ttu-id="2c758-127">Hello를 사용 하 여 개발 된 응용 프로그램을 만들어 새 응용 프로그램 등록을 추가 하면 [응용 프로그램 레지스트리](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c758-127">When you add a new application registration by creating a custom-developed application using hello [Application Registry](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).</span></span>

5.  <span data-ttu-id="2c758-128">Hello를 사용 하 여 개발 된 응용 프로그램을 만들어 새 응용 프로그램 등록을 추가 하면 [V2.0 응용 프로그램 등록 포털](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c758-128">When you add a new application registration by creating a custom-developed application using hello [V2.0 Application Registration Portal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).</span></span>

6.  <span data-ttu-id="2c758-129">Visual Studio의 [ASP.net 인증 방법](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) 또는 [연결된 서비스](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx)를 사용하여 개발 중인 응용 프로그램을 추가하는 경우.</span><span class="sxs-lookup"><span data-stu-id="2c758-129">When you add an application you’re developing using Visual Studio’s [ASP.net Authentication Methods](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) or [Connected Services](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx).</span></span>

7.  <span data-ttu-id="2c758-130">Hello를 사용 하 여 서비스 사용자 개체를 만들 때 [Azure AD PowerShell 모듈이](/powershell/azure/install-adv2?view=azureadps-2.0)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c758-130">When you create a service principal object using hello [Azure AD PowerShell Module](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

8.  <span data-ttu-id="2c758-131">때 있습니다 [tooan 응용 프로그램 동의](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) 테 넌 트의 관리자 toouse 데이터로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c758-131">When you [consent tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) as an administrator toouse data in your tenant.</span></span>

9.  <span data-ttu-id="2c758-132">경우는 [사용자가 tooan 응용 프로그램을 승인](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toouse 데이터 테 넌 트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c758-132">When a [user consents tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toouse data in your tenant.</span></span>

10. <span data-ttu-id="2c758-133">테넌트에 데이터를 저장하는 특정 서비스를 활성화하는 경우.</span><span class="sxs-lookup"><span data-stu-id="2c758-133">When you enable certain services that store data in your tenant.</span></span> <span data-ttu-id="2c758-134">이 한 가지 예로 모델링 되는 암호 재설정 서비스 보안 주체 toostore로 암호 재설정 정책을 안전 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c758-134">One example of this is Password Reset, which is modeled as a service principal toostore your password reset policy securely.</span></span>

<span data-ttu-id="2c758-135">tooget 앱 tooyour 디렉터리를 추가 하는 방법을 대 한 자세한 내용은 읽기 [응용 프로그램을 AD tooAzure 추가 방법과 이유](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c758-135">tooget more details on how apps are added tooyour directory, read [How and why applications are added tooAzure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).</span></span>

## <a name="i-want-tooremove-a-specific-users-or-groups-assignment-tooan-application"></a><span data-ttu-id="2c758-136">특정 사용자 또는 그룹의 할당 tooan 응용 프로그램 tooremove 원합니다</span><span class="sxs-lookup"><span data-stu-id="2c758-136">I want tooremove a specific user’s or group’s assignment tooan application</span></span>

<span data-ttu-id="2c758-137">hello에 나열 된 hello 단계를 수행 하는 사용자 또는 그룹 할당 tooan 응용, tooremove [에서 Azure Active Directory에서 엔터프라이즈 응용 프로그램에서 사용자 또는 그룹 할당을 제거할](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) 문서.</span><span class="sxs-lookup"><span data-stu-id="2c758-137">tooremove a user or group assignment tooan application, follow hello steps listed in hello [Remove a user or group assignment from an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) article.</span></span>

## <a name="i-want-toodisable-all-access-tooan-application-for-every-user"></a><span data-ttu-id="2c758-138">모든 사용자에 대 한 모든 액세스 tooan 응용 프로그램이 toodisable 원합니다</span><span class="sxs-lookup"><span data-stu-id="2c758-138">I want toodisable all access tooan application for every user</span></span>

<span data-ttu-id="2c758-139">toodisable 모든 사용자 로그인 tooan 응용 프로그램 hello에 나열 된 hello 단계를 수행 [Azure Active Directory에서 엔터프라이즈 응용 프로그램에 대 한 사용자 로그인을 사용 하지 않도록 설정](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) 문서.</span><span class="sxs-lookup"><span data-stu-id="2c758-139">toodisable all user sign-ins tooan application, follow hello steps listed in hello [Disable user sign-ins for an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) article.</span></span>

## <a name="i-want-toodelete-an-application-entirely"></a><span data-ttu-id="2c758-140">응용 프로그램 toodelete를 완전히 낮음</span><span class="sxs-lookup"><span data-stu-id="2c758-140">I want toodelete an application entirely</span></span>

<span data-ttu-id="2c758-141">너무**응용 프로그램을 삭제할**, 아래 hello 지침에 따라:</span><span class="sxs-lookup"><span data-stu-id="2c758-141">too**delete an application**, follow hello instructions below:</span></span>

1.  <span data-ttu-id="2c758-142">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자** 또는 **공동 관리자**</span><span class="sxs-lookup"><span data-stu-id="2c758-142">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="2c758-143">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c758-143">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2c758-144">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="2c758-144">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2c758-145">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c758-145">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2c758-146">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="2c758-146">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="2c758-147">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="2c758-147">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="2c758-148">원하는 toodelete hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c758-148">Select hello application you want toodelete.</span></span>

7.  <span data-ttu-id="2c758-149">Hello 응용 프로그램 로드 되 면 클릭 **삭제** hello 최고 응용 프로그램에서 아이콘 **개요** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="2c758-149">Once hello application loads, click **Delete** icon from hello top application’s **Overview** blade.</span></span>

## <a name="i-want-toodisable-all-future-user-consent-operations-tooany-application"></a><span data-ttu-id="2c758-150">모든 향후 사용자 동의 작업 tooany 응용 프로그램 toodisable 원합니다</span><span class="sxs-lookup"><span data-stu-id="2c758-150">I want toodisable all future user consent operations tooany application</span></span>

<span data-ttu-id="2c758-151">전체 디렉터리 승인 tooany 응용 프로그램에서 최종 사용자가 방지에 대 한 사용자 동의 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c758-151">Disabling user consent for your entire directory prevent end users from consenting tooany application.</span></span> <span data-ttu-id="2c758-152">관리자는 여전히 사용자의 동작에 동의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c758-152">Administrators can still consent on user’s behalves.</span></span> <span data-ttu-id="2c758-153">응용 프로그램에 대해 자세히 toolearn 동의 및 이유 있거나 하지 않을 toodo이,이 읽기 [이해 사용자 및 관리자 동의](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c758-153">toolearn more about application consent, and why you may or may not wish toodo this, read [Understanding user and admin consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span></span>

<span data-ttu-id="2c758-154">너무**전체 디렉터리의 모든 이후 사용자 동의 작업을 사용 하지 않도록 설정**, 아래 hello 지침에 따라:</span><span class="sxs-lookup"><span data-stu-id="2c758-154">too**disable all future user consent operations in your entire directory**, follow hello instructions below:</span></span>

1.  <span data-ttu-id="2c758-155">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="2c758-155">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2c758-156">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c758-156">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2c758-157">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="2c758-157">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2c758-158">클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c758-158">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="2c758-159">**사용자 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2c758-159">click **User settings**.</span></span>

6.  <span data-ttu-id="2c758-160">Hello 설정 하 여 모든 이후 사용자 동의 작업을 사용 하지 않도록 설정 **사용자가 앱 tooaccess 데이터 허용 수** 너무 설정/해제**아니요** hello를 클릭 하 고 **저장** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2c758-160">Disable all future user consent operations by setting hello **Users can allow apps tooaccess their data** toggle too**No** and click hello **Save** button.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c758-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2c758-161">Next steps</span></span>
[<span data-ttu-id="2c758-162">Azure Active Directory로 응용 프로그램 관리</span><span class="sxs-lookup"><span data-stu-id="2c758-162">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
