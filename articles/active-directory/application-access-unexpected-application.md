---
title: "내 응용 프로그램 목록에 예기치 않은 응용 프로그램 | Microsoft Docs"
description: "테넌트에서 모든 응용 프로그램을 보는 방법 및 엔터프라이즈 응용 프로그램의 모든 응용 프로그램 목록에 응용 프로그램을 표시하는 방법 이해"
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
ms.openlocfilehash: 0f8136cb066fa6e3e4a8dd06e34b9f866e3916f6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="unexpected-application-in-my-applications-list"></a><span data-ttu-id="feff3-103">내 응용 프로그램 목록에 예기치 않은 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="feff3-103">Unexpected application in my applications list</span></span>

<span data-ttu-id="feff3-104">이 문서는 **엔터프라이즈 응용 프로그램**의 **모든 응용 프로그램** 목록에 응용 프로그램을 표시하는 방법을 이해할 수 있도록 돕습니다.</span><span class="sxs-lookup"><span data-stu-id="feff3-104">This article help you to understand how applications appear in your **All Applications** list under **Enterprise Applications**.</span></span> 

## <a name="how-to-see-all-applications-in-your-tenant"></a><span data-ttu-id="feff3-105">테넌트에서 모든 응용 프로그램을 보는 방법</span><span class="sxs-lookup"><span data-stu-id="feff3-105">How to see all applications in your tenant</span></span>

<span data-ttu-id="feff3-106">테넌트에서 모든 응용 프로그램을 보려면 **필터** 컨트롤을 사용하여 **모든 응용 프로그램** 목록에 **모든 응용 프로그램**을 표시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="feff3-106">To see all the applications in your tenant, you need to use the **Filter** control to show **All Applications** under the **All Applications** list.</span></span> <span data-ttu-id="feff3-107">이렇게 하려면 다음 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="feff3-107">To do this, follow the steps below:</span></span>

1.  <span data-ttu-id="feff3-108">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="feff3-108">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="feff3-109">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="feff3-109">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="feff3-110">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="feff3-110">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="feff3-111">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="feff3-111">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="feff3-112">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="feff3-112">click **All Applications** to view a list of all your applications.</span></span>

6.  <span data-ttu-id="feff3-113">**모든 응용 프로그램 목록**의 맨 위에 있는 **필터** 컨트롤을 사용하도록 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="feff3-113">click the use the **Filter** control at the top of the **All Applications List**.</span></span>

7.  <span data-ttu-id="feff3-114">**필터** 블레이드에서 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="feff3-114">On the **Filter** blade, set the **Show** option to **All Applications.**</span></span>

## <a name="why-does-a-specific-application-appear-in-my-all-applications-list"></a><span data-ttu-id="feff3-115">내 모든 응용 프로그램 목록에 특정 응용 프로그램이 나타나는 이유는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="feff3-115">Why does a specific application appear in my all applications list?</span></span>

<span data-ttu-id="feff3-116">**모든 응용 프로그램**으로 필터링한 경우 **모든 응용 프로그램** **목록**은 테넌트의 모든 서비스 주체 개체를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="feff3-116">When filtered to **All Applications**, the **All Applications** **List** shows every Service Principal object in your tenant.</span></span> <span data-ttu-id="feff3-117">서비스 주체 개체는 다양한 방법으로 이 목록에 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="feff3-117">Service Principal objects can appear in this list in a various ways:</span></span>

1.  <span data-ttu-id="feff3-118">다음을 포함하여 응용 프로그램 갤러리에서 모든 응용 프로그램을 추가하는 경우:</span><span class="sxs-lookup"><span data-stu-id="feff3-118">When you add any application from the application gallery, including:</span></span>

   1. <span data-ttu-id="feff3-119">**Azure AD 갤러리 응용 프로그램** – Single Sign-On에 대해 Azure AD와 사전 통합된 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="feff3-119">**Azure AD Gallery Applications** – An application that has been pre-integrated for single sign-on with Azure AD.</span></span>

   2. <span data-ttu-id="feff3-120">**응용 프로그램 프록시 응용 프로그램** – 외부로 보안 Single Sign-On을 제공하려는 온-프레미스 환경에서 실행 중인 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="feff3-120">**Application Proxy Applications** – An application running in your on-premises environment that you want to provide secure single-sign on to externally.</span></span>

   3. <span data-ttu-id="feff3-121">**사용자 지정 개발된 응용 프로그램** – 조직에서 Azure AD 응용 프로그램 개발 플랫폼에서 개발하고자 하지만 아직 존재하지 않을 수 있는 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="feff3-121">**Custom-developed Applications** – An application that your organization wishes to develop on the Azure AD Application Development Platform, but that may not exist yet.</span></span>

   4. <span data-ttu-id="feff3-122">**비 갤러리 응용 프로그램** – 사용자의 응용 프로그램을 가져옵니다!</span><span class="sxs-lookup"><span data-stu-id="feff3-122">**Non-Gallery Applications** – Bring your own applications!</span></span> <span data-ttu-id="feff3-123">원하는 모든 웹 링크 또는 사용자 이름 및 암호 필드를 렌더링하는 모든 응용 프로그램은 SAML 또는 OpenID Connect 프로토콜을 지원하거나 Single Sign-On에 대해 Azure AD와 통합하려는 SCIM을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="feff3-123">Any web link you want, or any application which renders a username and password field, supports SAML or OpenID Connect protocols, or supports SCIM which you wish to integrate for single sign-on with Azure AD.</span></span>

2.  <span data-ttu-id="feff3-124">Azure Active Directory와 통합된 타<sup>사</sup> 응용 프로그램에 등록하거나 로그인하는 경우.</span><span class="sxs-lookup"><span data-stu-id="feff3-124">When signing up for, or signing in to, a 3<sup>rd</sup> party application integrated with Azure Active Directory.</span></span> <span data-ttu-id="feff3-125">한 가지 예로 [Smartsheet](https://app.smartsheet.com/b/home) 또는 [DocuSign](https://www.docusign.net/member/MemberLogin.aspx)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="feff3-125">One example of this is [Smartsheet](https://app.smartsheet.com/b/home) or [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).</span></span>

3.  <span data-ttu-id="feff3-126">[Microsoft Office 365](http://products.office.com/)와 같은 자사 응용 프로그램에 대한 라이선스를 사용자 또는 그룹에 등록 또는 추가하는 경우.</span><span class="sxs-lookup"><span data-stu-id="feff3-126">When signing up for, or adding a license to a user or a group to a first party application, like [Microsoft Office 365](http://products.office.com/).</span></span>

4.  <span data-ttu-id="feff3-127">[응용 프로그램 레지스트리](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration)를 사용하여 사용자 지정 개발된 응용 프로그램을 만들어 새 응용 프로그램 등록을 추가하는 경우.</span><span class="sxs-lookup"><span data-stu-id="feff3-127">When you add a new application registration by creating a custom-developed application using the [Application Registry](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).</span></span>

5.  <span data-ttu-id="feff3-128">[V2.0 응용 프로그램 레지스트리 포털](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal)을 사용하여 사용자 지정 개발된 응용 프로그램을 만들어 새 응용 프로그램 등록을 추가하는 경우.</span><span class="sxs-lookup"><span data-stu-id="feff3-128">When you add a new application registration by creating a custom-developed application using the [V2.0 Application Registration Portal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).</span></span>

6.  <span data-ttu-id="feff3-129">Visual Studio의 [ASP.net 인증 방법](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) 또는 [연결된 서비스](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx)를 사용하여 개발 중인 응용 프로그램을 추가하는 경우.</span><span class="sxs-lookup"><span data-stu-id="feff3-129">When you add an application you’re developing using Visual Studio’s [ASP.net Authentication Methods](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) or [Connected Services](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx).</span></span>

7.  <span data-ttu-id="feff3-130">[Azure AD PowerShell 모듈](/powershell/azure/install-adv2?view=azureadps-2.0)을 사용하여 서비스 주체 개체를 만드는 경우.</span><span class="sxs-lookup"><span data-stu-id="feff3-130">When you create a service principal object using the [Azure AD PowerShell Module](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

8.  <span data-ttu-id="feff3-131">테넌트의 데이터를 사용하도록 관리자 권한으로 [응용 프로그램에 동의](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent)하는 경우.</span><span class="sxs-lookup"><span data-stu-id="feff3-131">When you [consent to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) as an administrator to use data in your tenant.</span></span>

9.  <span data-ttu-id="feff3-132">테넌트의 데이터를 사용하도록 [사용자가 응용 프로그램에 동의](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent)하는 경우.</span><span class="sxs-lookup"><span data-stu-id="feff3-132">When a [user consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) to use data in your tenant.</span></span>

10. <span data-ttu-id="feff3-133">테넌트에 데이터를 저장하는 특정 서비스를 활성화하는 경우.</span><span class="sxs-lookup"><span data-stu-id="feff3-133">When you enable certain services that store data in your tenant.</span></span> <span data-ttu-id="feff3-134">한 가지 예는 암호 재설정 정책을 안전하게 저장하도록 서비스 주체로 모델링되는 암호 재설정입니다.</span><span class="sxs-lookup"><span data-stu-id="feff3-134">One example of this is Password Reset, which is modeled as a service principal to store your password reset policy securely.</span></span>

<span data-ttu-id="feff3-135">앱을 디렉터리에 추가하는 방법에 대한 자세한 내용은 [응용 프로그램을 Azure AD에 추가하는 방법 및 이유](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="feff3-135">To get more details on how apps are added to your directory, read [How and why applications are added to Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).</span></span>

## <a name="i-want-to-remove-a-specific-users-or-groups-assignment-to-an-application"></a><span data-ttu-id="feff3-136">응용 프로그램에 대한 특정 사용자 또는 그룹의 할당을 제거하려는 경우</span><span class="sxs-lookup"><span data-stu-id="feff3-136">I want to remove a specific user’s or group’s assignment to an application</span></span>

<span data-ttu-id="feff3-137">응용 프로그램에 대한 사용자 또는 그룹 할당을 제거하려면 [Azure Active Directory의 엔터프라이즈 앱에서 사용자 또는 그룹 할당 제거](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) 문서에 나열된 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="feff3-137">To remove a user or group assignment to an application, follow the steps listed in the [Remove a user or group assignment from an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) article.</span></span>

## <a name="i-want-to-disable-all-access-to-an-application-for-every-user"></a><span data-ttu-id="feff3-138">모든 사용자에 대해 응용 프로그램에 대한 모든 액세스를 비활성화하려는 경우</span><span class="sxs-lookup"><span data-stu-id="feff3-138">I want to disable all access to an application for every user</span></span>

<span data-ttu-id="feff3-139">응용 프로그램에 대한 모든 사용자 로그인을 비활성화하려면 [Azure Active Directory의 엔터프라이즈 앱에 대한 사용자 로그인 비활성화](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) 문서에 나열된 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="feff3-139">To disable all user sign-ins to an application, follow the steps listed in the [Disable user sign-ins for an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) article.</span></span>

## <a name="i-want-to-delete-an-application-entirely"></a><span data-ttu-id="feff3-140">응용 프로그램을 완전히 삭제하려는 경우</span><span class="sxs-lookup"><span data-stu-id="feff3-140">I want to delete an application entirely</span></span>

<span data-ttu-id="feff3-141">**응용 프로그램을 삭제**하려면 아래 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="feff3-141">To **delete an application**, follow the instructions below:</span></span>

1.  <span data-ttu-id="feff3-142">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="feff3-142">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="feff3-143">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="feff3-143">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="feff3-144">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="feff3-144">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="feff3-145">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="feff3-145">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="feff3-146">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="feff3-146">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="feff3-147">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="feff3-147">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="feff3-148">삭제하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="feff3-148">Select the application you want to delete.</span></span>

7.  <span data-ttu-id="feff3-149">응용 프로그램이 로드되면 맨 위의 응용 프로그램 **개요** 블레이드에서 **삭제** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="feff3-149">Once the application loads, click **Delete** icon from the top application’s **Overview** blade.</span></span>

## <a name="i-want-to-disable-all-future-user-consent-operations-to-any-application"></a><span data-ttu-id="feff3-150">모든 응용 프로그램에 대한 모든 이후 사용자 동의 작업을 비활성화하려는 경우</span><span class="sxs-lookup"><span data-stu-id="feff3-150">I want to disable all future user consent operations to any application</span></span>

<span data-ttu-id="feff3-151">전체 디렉터리에 대한 사용자 동의를 비활성화하면 모든 응용 프로그램에 대한 최종 사용자 동의를 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="feff3-151">Disabling user consent for your entire directory prevent end users from consenting to any application.</span></span> <span data-ttu-id="feff3-152">관리자는 여전히 사용자의 동작에 동의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="feff3-152">Administrators can still consent on user’s behalves.</span></span> <span data-ttu-id="feff3-153">응용 프로그램 동의 및 이 작업을 수행하거나 수행하지 않을 수 있는 이유에 대해 자세히 알아보려면 [사용자 및 관리자 동의 이해하기](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="feff3-153">To learn more about application consent, and why you may or may not wish to do this, read [Understanding user and admin consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span></span>

<span data-ttu-id="feff3-154">**전체 디렉터리에서 모든 이후 사용자 동의 작업을 비활성화**하려면 아래의 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="feff3-154">To **disable all future user consent operations in your entire directory**, follow the instructions below:</span></span>

1.  <span data-ttu-id="feff3-155">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="feff3-155">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="feff3-156">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="feff3-156">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="feff3-157">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="feff3-157">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="feff3-158">탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="feff3-158">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="feff3-159">**사용자 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="feff3-159">click **User settings**.</span></span>

6.  <span data-ttu-id="feff3-160">**사용자가 앱이 데이터에 액세스하도록 허용할 수 있음** 토글을 **아니요**로 설정하고 **저장** 단추를 클릭하여 모든 이후 사용자 동의 작업을 비활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="feff3-160">Disable all future user consent operations by setting the **Users can allow apps to access their data** toggle to **No** and click the **Save** button.</span></span>

## <a name="next-steps"></a><span data-ttu-id="feff3-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="feff3-161">Next steps</span></span>
[<span data-ttu-id="feff3-162">Azure Active Directory로 응용 프로그램 관리</span><span class="sxs-lookup"><span data-stu-id="feff3-162">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
