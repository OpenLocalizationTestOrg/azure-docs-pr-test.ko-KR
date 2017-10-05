---
title: "비-갤러리 응용 프로그램에 대해 암호 Single Sign-On을 구성하는 방법 | Microsoft Docs"
description: "Azure AD 응용 프로그램 갤러리에 없는 경우 보안 암호 기반 Single Sign-On에 대한 사용자 지정 비 갤러리 응용 프로그램을 구성하는 방법"
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
ms.openlocfilehash: f629ec99824199306ebf825901beaa99d83d434d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="32e34-103">비-갤러리 응용 프로그램에 대해 암호 Single Sign-On을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="32e34-103">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="32e34-104">Azure AD 응용 프로그램 갤러리 내에서 찾을 수 있는 선택 항목 외에도 원하는 응용 프로그램이 나열되어 있지 않은 경우 **비 갤러리 응용 프로그램**을 추가하는 옵션도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-104">In addition to the choices found within the Azure AD Application Gallery, you also have the option to add a **non-gallery application** when the application you want is not listed there.</span></span> <span data-ttu-id="32e34-105">이 기능을 사용하여 조직에 이미 있는 응용 프로그램 또는 [Azure AD 응용 프로그램 갤러리](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery)의 일부가 아닌 공급 업체에서 사용할 수 있는 타사 응용 프로그램을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-105">Using this capability, you can add any application that already exists in your organization, or any third-party application that you might use from a vendor who is not already part of the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span></span>

<span data-ttu-id="32e34-106">비 갤러리 응용 프로그램을 추가한 후 [Azure Portal](https://portal.azure.com/)의 엔터프라이즈 응용 프로그램에서 **Single Sign-On** 탐색 항목을 선택하여 이 응용 프로그램이 사용하는 Single Sign-On 메서드를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-106">Once you add a non-gallery application, you can then configure the Single sign-on method this application uses by selecting the **Single Sign-on** navigation item on an Enterprise Application in the [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="32e34-107">사용할 수 있는 Single Sign-On 방법 중 하나는 [암호 기반 Single Sign-On](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-107">One of the Single Sign-on methods available to you is the [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span></span> <span data-ttu-id="32e34-108">**비 갤러리 응용 프로그램 추가** 경험으로 사전 통합된 응용 프로그램의 집합에 없는 경우에도 HTML 기반 사용자 이름 및 암호 입력 필드를 렌더링하는 모든 응용 프로그램을 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-108">With the **add a non-gallery application** experience, you can integrate any application that renders an HTML-based username and password input field, even if it is not in our set of pre-integrated applications.</span></span>

<span data-ttu-id="32e34-109">이 기능이 작동하는 방법은 사용자 이름 및 암호 입력 필드를 자동으로 감지하고 특정 응용 프로그램 인스턴스에 대해 안전하게 저장할 수 있도록 하는 액세스 패널 확장의 일부인 페이지 스크랩 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-109">The way this works is by a page scraping technology that is part of the Access Panel extension that allows us to auto-detect username and password input fields, store them securely for your specific application instance.</span></span> <span data-ttu-id="32e34-110">그런 다음 사용자가 응용 프로그램 액세스 패널에서 해당 응용 프로그램으로 이동할 때 사용자 이름 및 암호를 해당 필드에 안전하게 재생합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-110">Then securely replay usernames and passwords to those fields when a user navigates to that application on the application access panel.</span></span>

<span data-ttu-id="32e34-111">모든 종류의 응용 프로그램을 Azure AD로 신속하게 통합하는 것은 좋은 방법이며 다음을 가능하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-111">This is a great way to get started integrating any kind of application into Azure AD quickly, and allows you to:</span></span>

-   <span data-ttu-id="32e34-112">HTML 사용자 이름 및 암호 입력 필드를 렌더링하는 한 Azure AD 테넌트와 **전세계 모든 응용 프로그램** 통합</span><span class="sxs-lookup"><span data-stu-id="32e34-112">Integrate **any application in the world** with your Azure AD tenant, so long as it renders an HTML username and password input field</span></span>

-   <span data-ttu-id="32e34-113">Azure AD와 통합한 응용 프로그램에 대한 사용자 이름 및 암호를 안전하게 저장 및 재생하여 **사용자에 대한 Single Sign-On** 활성화</span><span class="sxs-lookup"><span data-stu-id="32e34-113">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for the application you’ve integrated with Azure AD</span></span>

-   <span data-ttu-id="32e34-114">모든 응용 프로그램에 대한 **입력 필드 자동 감지** 및 자동 감지가 찾지 못하는 경우 액세스 패널 브라우저 확장을 사용하여 이러한 필드를 수동으로 검색할 수 있도록 함</span><span class="sxs-lookup"><span data-stu-id="32e34-114">**Auto-detect input** fields for any application and allow you to manually detect those fields using the Access Panel Browser Extension, in case auto-detection does not find them</span></span>

-   <span data-ttu-id="32e34-115">로그인하는 데 사용자 이름 및 암호 필드 이상을 필요로 하는 응용 프로그램에 대해 **여러 로그인 필드를 필요로 하는 응용 프로그램 지원**</span><span class="sxs-lookup"><span data-stu-id="32e34-115">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields to sign in</span></span>

-   <span data-ttu-id="32e34-116">사용자가 자격 증명을 입력하는 경우 [응용 프로그램 액세스 패널](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)에 표시되는 사용자 이름 및 암호 입력 필드의 **레이블 사용자 지정**</span><span class="sxs-lookup"><span data-stu-id="32e34-116">**Customize the labels** of the username and password input fields your users see on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span></span>

-   <span data-ttu-id="32e34-117">**사용자**가 [응용 프로그램 액세스 패널](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)에 수동으로 입력하는 모든 기존 응용 프로그램 계정에 대한 자신의 사용자 이름 및 암호를 제공하도록 허용</span><span class="sxs-lookup"><span data-stu-id="32e34-117">Allow your **users** to provide their own usernames and passwords for any existing application accounts they are typing in manually on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span></span>

-   <span data-ttu-id="32e34-118">**비즈니스 그룹의 멤버**가 [셀프 서비스 응용 프로그램 액세스](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) 기능을 사용하여 사용자에게 할당된 사용자 이름 및 암호를 지정하도록 허용</span><span class="sxs-lookup"><span data-stu-id="32e34-118">Allow a **member of the business group** to specify the usernames and passwords assigned to a user by using the [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span></span>

-   <span data-ttu-id="32e34-119">**관리자**가 [응용 프로그램에 사용자를 할당](#_How_to_configure_1)할 때 자격 증명 업데이트 기능을 사용하여 사용자에게 할당된 사용자 이름 및 암호를 지정하도록 허용</span><span class="sxs-lookup"><span data-stu-id="32e34-119">Allow an **administrator** to specify the usernames and passwords assigned to a user by using the Update Credentials feature when [assigning a user to an application](#_How_to_configure_1)</span></span>

-   <span data-ttu-id="32e34-120">**관리자**가 [응용 프로그램에 그룹을 할당](#assign-an-application-to-a-group-directly)할 때 자격 증명 업데이트 기능을 사용하여 사용자 그룹에서 사용하는 공유된 사용자 이름 및 암호를 지정하도록 허용</span><span class="sxs-lookup"><span data-stu-id="32e34-120">Allow an **administrator** to specify the shared username or password used by a group of people by using the Update Credentials feature when [assigning a group to an application](#assign-an-application-to-a-group-directly)</span></span>

<span data-ttu-id="32e34-121">아래는 **비 갤러리 응용 프로그램 추가** 경험을 사용하여 추가하는 모든 응용 프로그램에 [암호 기반 Single Sign-On](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work)을 활성화할 수 있는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-121">Below describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) to any application that you add using the **add a non-gallery application** experience.</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="32e34-122">필요한 단계 개요</span><span class="sxs-lookup"><span data-stu-id="32e34-122">Overview of steps required</span></span>

<span data-ttu-id="32e34-123">Azure AD 갤러리에서 응용 프로그램을 구성하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-123">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="32e34-124">비갤러리 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="32e34-124">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="32e34-125">암호 Single Sign-On에 대한 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="32e34-125">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="32e34-126">사용자 또는 그룹에 응용 프로그램 할당</span><span class="sxs-lookup"><span data-stu-id="32e34-126">Assign the application to a user or a group</span></span>](#assign-the-application-to-a-user-or-a-group)

    -   [<span data-ttu-id="32e34-127">응용 프로그램에 사용자를 직접 할당</span><span class="sxs-lookup"><span data-stu-id="32e34-127">Assign a user to an application directly</span></span>](#assign-a-user-to-an-application-directly)

    -   [<span data-ttu-id="32e34-128">그룹에 응용 프로그램을 직접 할당</span><span class="sxs-lookup"><span data-stu-id="32e34-128">Assign an application to a group directly</span></span>](#assign-an-application-to-a-group-directly)

## <a name="add-a-non-gallery-application"></a><span data-ttu-id="32e34-129">비 갤러리 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="32e34-129">Add a non-gallery application</span></span>

<span data-ttu-id="32e34-130">Azure AD 갤러리에서 응용 프로그램을 추가하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-130">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="32e34-131">[Azure Portal](https://portal.azure.com)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-131">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="32e34-132">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-132">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="32e34-133">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-133">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="32e34-134">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-134">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="32e34-135">**엔터프라이즈 응용 프로그램** 블레이드의 오른쪽 위 모서리에서 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-135">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="32e34-136">**비갤러리 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-136">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="32e34-137">**이름** 텍스트 상자에 응용 프로그램의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-137">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="32e34-138">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-138">Select **Add.**</span></span>

<span data-ttu-id="32e34-139">짧은 시간 후에 응용 프로그램의 구성 블레이드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-139">After a short period, you be able to see the application’s configuration blade.</span></span>

## <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="32e34-140">암호 Single Sign-On에 대한 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="32e34-140">Configure the application for password single sign-on</span></span>

<span data-ttu-id="32e34-141">응용 프로그램에 Single Sign-On을 구성하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-141">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="32e34-142">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-142">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="32e34-143">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-143">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="32e34-144">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-144">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="32e34-145">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-145">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="32e34-146">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-146">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="32e34-147">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-147">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="32e34-148">Single Sign-On을 구성하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-148">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="32e34-149">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **Single Sign-On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-149">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="32e34-150">**암호 기반 로그온** 모드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-150">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="32e34-151">**로그온 URL**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-151">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="32e34-152">사용자가 로그인하기 위해 사용자 이름과 암호를 입력하는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-152">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="32e34-153">URL에서 로그인 필드가 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-153">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="32e34-154">응용 프로그램에 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-154">Assign users to the application.</span></span>

11. <span data-ttu-id="32e34-155">또한 사용자의 행을 선택하고 **자격 증명 업데이트**를 클릭하고 사용자를 대신하여 사용자 이름 및 암호를 입력하여 사용자를 대신하여 자격 증명을 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-155">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="32e34-156">그렇지 않으면 사용자는 시작할 때 자격 증명을 입력하라는 메시지를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-156">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="assign-a-user-to-an-application-directly"></a><span data-ttu-id="32e34-157">응용 프로그램에 사용자를 직접 할당</span><span class="sxs-lookup"><span data-stu-id="32e34-157">Assign a user to an application directly</span></span>

<span data-ttu-id="32e34-158">응용 프로그램에 하나 이상의 사용자를 직접 할당하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-158">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="32e34-159">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-159">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="32e34-160">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-160">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="32e34-161">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-161">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="32e34-162">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-162">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="32e34-163">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-163">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="32e34-164">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-164">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="32e34-165">목록에서 사용자를 할당하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-165">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="32e34-166">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-166">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="32e34-167">**사용자 및 그룹** 목록의 맨 위에서 **추가** 단추를 클릭하여 **할당 추가** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-167">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="32e34-168">**할당 추가** 블레이드에서 **사용자 및 그룹** 선택기를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-168">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="32e34-169">**이름 또는 전자 메일 주소로 검색** 검색 상자에 할당하려는 사용자의 **전체 이름** 또는 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-169">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="32e34-170">목록의 **사용자** 위로 마우스를 이동하여 **확인란**을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-170">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="32e34-171">사용자의 프로필 사진이나 로고 옆의 확인란을 클릭하여 사용자를 **선택됨** 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-171">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="32e34-172">**선택 사항:** **둘 이상의 사용자를 추가**하려는 경우 **이름 또는 전자 메일 주소로 검색** 검색 상자에 다른 **전체 이름** 또는 **전자 메일 주소**를 입력하고 확인란을 클릭하여 이 사용자를 **선택됨** 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-172">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="32e34-173">사용자 선택이 완료되면 **선택** 단추를 클릭하여 응용 프로그램에 할당되도록 사용자 및 그룹의 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-173">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="32e34-174">**선택 사항:** **할당 추가** 블레이드에서 **역할 선택** 선택기를 클릭하여 선택한 사용자에게 할당할 역할을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-174">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="32e34-175">**할당** 단추를 클릭하여 선택한 사용자에게 응용 프로그램을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-175">Click the **Assign** button to assign the application to the selected users.</span></span>

## <a name="assign-an-application-to-a-group-directly"></a><span data-ttu-id="32e34-176">그룹에 응용 프로그램을 직접 할당</span><span class="sxs-lookup"><span data-stu-id="32e34-176">Assign an application to a group directly</span></span>

<span data-ttu-id="32e34-177">응용 프로그램에 하나 이상의 그룹을 직접 할당하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-177">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="32e34-178">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-178">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="32e34-179">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-179">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="32e34-180">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-180">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="32e34-181">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-181">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="32e34-182">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-182">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="32e34-183">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-183">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="32e34-184">목록에서 사용자를 할당하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-184">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="32e34-185">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-185">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="32e34-186">**사용자 및 그룹** 목록의 맨 위에서 **추가** 단추를 클릭하여 **할당 추가** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-186">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="32e34-187">**할당 추가** 블레이드에서 **사용자 및 그룹** 선택기를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-187">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="32e34-188">**이름 또는 메일 주소로 검색** 검색 상자에 할당하려는 그룹의 **전체 그룹 이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-188">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="32e34-189">목록의 **그룹** 위로 마우스를 이동하여 **확인란**을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-189">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="32e34-190">그룹의 프로필 사진이나 로고 옆의 확인란을 클릭하여 사용자를 **선택됨** 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-190">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="32e34-191">**선택 사항:** **둘 이상의 그룹을 추가**하려는 경우 **이름 또는 메일 주소로 검색** 검색 상자에 다른 **전체 그룹 이름**을 입력하고 확인란을 클릭하여 이 그룹을 **선택됨** 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-191">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="32e34-192">그룹 선택이 완료되면 **선택** 단추를 클릭하여 응용 프로그램에 할당되도록 사용자 및 그룹의 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-192">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="32e34-193">**선택 사항:** **할당 추가** 블레이드에서 **역할 선택** 선택기를 클릭하여 선택한 그룹에 할당할 역할을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-193">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="32e34-194">**할당** 단추를 클릭하여 선택한 그룹에 응용 프로그램을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-194">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="32e34-195">짧은 시간 후 선택한 사용자는 액세스 패널에서 이러한 응용 프로그램을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32e34-195">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="32e34-196">다음 단계</span><span class="sxs-lookup"><span data-stu-id="32e34-196">Next steps</span></span>
[<span data-ttu-id="32e34-197">응용 프로그램 프록시를 사용하여 앱에 Single Sign-On 제공</span><span class="sxs-lookup"><span data-stu-id="32e34-197">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
