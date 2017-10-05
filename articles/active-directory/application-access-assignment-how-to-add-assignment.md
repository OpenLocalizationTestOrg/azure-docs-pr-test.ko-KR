---
title: "응용 프로그램에 사용자 및 그룹을 할당하는 방법 | Microsoft Docs"
description: "액세스 권한을 부여하도록 응용 프로그램에 사용자 할당"
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
ms.openlocfilehash: 61536612e0dd5102b8f5e911c350826846f5ed77
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-assign-users-and-groups-to-an-application"></a><span data-ttu-id="fc9b4-103">응용 프로그램에 사용자 및 그룹을 할당하는 방법</span><span class="sxs-lookup"><span data-stu-id="fc9b4-103">How to assign users and groups to an application</span></span>

<span data-ttu-id="fc9b4-104">사용자가 특정 응용 프로그램에 대해 아래의 작업을 수행할 수 있으려면 먼저 액세스 권한을 부여하도록 **응용 프로그램에 할당**해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-104">Before your users can do any of the below for a specific application, you need to first **assign them to the application** to grant them access:</span></span>

-   <span data-ttu-id="fc9b4-105">**응용 프로그램의 URL로 직접 이동**(SP 시작 로그온이라고도 함)하여 응용 프로그램에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-105">Access an application by **navigating to the application’s URL directly** (also known as SP-initiated sign-on).</span></span>

-   <span data-ttu-id="fc9b4-106">응용 프로그램의 **속성** 페이지에서 **사용자 액세스 URL**(IDP 시작 로그온이라고도 함)을 사용하여 응용 프로그램에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-106">Access an application by using the **User Access URL** on an application’s **Properties** page (also known as IDP-initiated sign on).</span></span>

-   <span data-ttu-id="fc9b4-107">[응용 프로그램 액세스 패널](https://myapps.microsoft.com/) 또는 모바일 응용 프로그램에 응용 프로그램이 나타나는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-107">See an application appear on their [Application Access Panel](https://myapps.microsoft.com/) or mobile application.</span></span>

-   <span data-ttu-id="fc9b4-108">[Office 365 응용 프로그램 시작 관리자](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a)에 응용 프로그램이 나타나는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-108">See an application appear on their [Office 365 Application Launcher](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a).</span></span>

## <a name="methods-to-assign-applications-with-azure-active-directory"></a><span data-ttu-id="fc9b4-109">Azure Active Directory로 응용 프로그램을 할당하는 방법</span><span class="sxs-lookup"><span data-stu-id="fc9b4-109">Methods to assign applications with Azure Active Directory</span></span> 

<span data-ttu-id="fc9b4-110">Azure Active Directory로 응용 프로그램을 할당할 수 있는 3가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-110">There are 3 ways you can assign applications with Azure Active Directory:</span></span>

-   [<span data-ttu-id="fc9b4-111">관리자 권한으로 응용 프로그램에 직접 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="fc9b4-111">Assign a user directly to an application as an administrator</span></span>](#assign-a-user-directly-as-an-administrator)

-   [<span data-ttu-id="fc9b4-112">관리자 권한으로 응용 프로그램에 직접 그룹 할당</span><span class="sxs-lookup"><span data-stu-id="fc9b4-112">Assign a group directly to an application as an administrator</span></span>](#assign-a-group-directly-to-an-application-as-an-administrator)

-   [<span data-ttu-id="fc9b4-113">셀프 서비스 응용 프로그램 액세스를 활성화하여 사용자가 자신의 응용 프로그램을 찾을 수 있도록 함</span><span class="sxs-lookup"><span data-stu-id="fc9b4-113">Enable self-service application access to allow users to find their own applications</span></span>](#enable-self-service-application-access-to-allow-users-to-find-their-own-applications)

## <a name="assign-a-user-directly-as-an-administrator"></a><span data-ttu-id="fc9b4-114">관리자 권한으로 직접 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="fc9b4-114">Assign a user directly as an administrator</span></span>

<span data-ttu-id="fc9b4-115">응용 프로그램에 하나 이상의 사용자를 직접 할당하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-115">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="fc9b4-116">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-116">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fc9b4-117">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-117">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fc9b4-118">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-118">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fc9b4-119">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-119">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="fc9b4-120">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-120">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="fc9b4-121">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-121">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="fc9b4-122">목록에서 사용자를 할당하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-122">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="fc9b4-123">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-123">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="fc9b4-124">**사용자 및 그룹** 목록의 맨 위에서 **추가** 단추를 클릭하여 **할당 추가** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-124">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="fc9b4-125">**할당 추가** 블레이드에서 **사용자 및 그룹** 선택기를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-125">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="fc9b4-126">**이름 또는 전자 메일 주소로 검색** 검색 상자에 할당하려는 사용자의 **전체 이름** 또는 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-126">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="fc9b4-127">목록의 **사용자** 위로 마우스를 이동하여 **확인란**을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-127">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="fc9b4-128">사용자의 프로필 사진이나 로고 옆의 확인란을 클릭하여 사용자를 **선택됨** 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-128">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="fc9b4-129">**선택 사항:** **둘 이상의 사용자를 추가**하려는 경우 **이름 또는 전자 메일 주소로 검색** 검색 상자에 다른 **전체 이름** 또는 **전자 메일 주소**를 입력하고 확인란을 클릭하여 이 사용자를 **선택됨** 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-129">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="fc9b4-130">사용자 선택이 완료되면 **선택** 단추를 클릭하여 응용 프로그램에 할당되도록 사용자 및 그룹의 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-130">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="fc9b4-131">**선택 사항:** **할당 추가** 블레이드에서 **역할 선택** 선택기를 클릭하여 선택한 사용자에게 할당할 역할을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-131">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="fc9b4-132">**할당** 단추를 클릭하여 선택한 사용자에게 응용 프로그램을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-132">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="fc9b4-133">잠시 후 선택한 사용자는 솔루션 설명 섹션에 설명된 메서드를 사용하여 이러한 응용 프로그램을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-133">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span></span>

## <a name="assign-a-group-directly-to-an-application-as-an-administrator"></a><span data-ttu-id="fc9b4-134">관리자 권한으로 응용 프로그램에 직접 그룹 할당</span><span class="sxs-lookup"><span data-stu-id="fc9b4-134">Assign a group directly to an application as an administrator</span></span>

<span data-ttu-id="fc9b4-135">응용 프로그램에 하나 이상의 그룹을 직접 할당하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-135">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="fc9b4-136">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-136">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fc9b4-137">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-137">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fc9b4-138">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-138">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fc9b4-139">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-139">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="fc9b4-140">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-140">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="fc9b4-141">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-141">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="fc9b4-142">목록에서 사용자를 할당하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-142">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="fc9b4-143">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-143">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="fc9b4-144">**사용자 및 그룹** 목록의 맨 위에서 **추가** 단추를 클릭하여 **할당 추가** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-144">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="fc9b4-145">**할당 추가** 블레이드에서 **사용자 및 그룹** 선택기를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-145">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="fc9b4-146">**이름 또는 메일 주소로 검색** 검색 상자에 할당하려는 그룹의 **전체 그룹 이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-146">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="fc9b4-147">목록의 **그룹** 위로 마우스를 이동하여 **확인란**을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-147">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="fc9b4-148">그룹의 프로필 사진이나 로고 옆의 확인란을 클릭하여 사용자를 **선택됨** 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-148">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="fc9b4-149">**선택 사항:** **둘 이상의 그룹을 추가**하려는 경우 **이름 또는 메일 주소로 검색** 검색 상자에 다른 **전체 그룹 이름**을 입력하고 확인란을 클릭하여 이 그룹을 **선택됨** 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-149">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="fc9b4-150">그룹 선택이 완료되면 **선택** 단추를 클릭하여 응용 프로그램에 할당되도록 사용자 및 그룹의 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-150">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="fc9b4-151">**선택 사항:** **할당 추가** 블레이드에서 **역할 선택** 선택기를 클릭하여 선택한 그룹에 할당할 역할을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-151">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="fc9b4-152">**할당** 단추를 클릭하여 선택한 그룹에 응용 프로그램을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-152">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="fc9b4-153">잠시 후 선택한 그룹 내 사용자는 솔루션 설명 섹션에 설명된 메서드를 사용하여 이러한 응용 프로그램을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-153">After a short period of time, the users within the groups you have selected be able to launch these applications using the methods described in the solution description section.</span></span> <span data-ttu-id="fc9b4-154">동적 그룹인 경우 이러한 할당된 그룹 내 사용자에 대해 표시되는 이러한 할당에 약간의 추가 처리 지연이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-154">If these are dynamic groups, there may be some additional processing delay in these assignments appearing for users within these assigned groups.</span></span>

## <a name="enable-self-service-application-access-to-allow-users-to-find-their-own-applications"></a><span data-ttu-id="fc9b4-155">셀프 서비스 응용 프로그램 액세스를 활성화하여 사용자가 자신의 응용 프로그램을 찾을 수 있도록 함</span><span class="sxs-lookup"><span data-stu-id="fc9b4-155">Enable self-service application access to allow users to find their own applications</span></span>

<span data-ttu-id="fc9b4-156">셀프 서비스 응용 프로그램 액세스는 사용자가 응용 프로그램을 직접 검색하도록 하고 경우에 따라 비즈니스 그룹이 해당 응용 프로그램에 대한 액세스를 승인하도록 허용하는 유용한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-156">Self-service application access is a great way to allow users to self-discover applications, optionally allow the business group to approve access to those applications.</span></span> <span data-ttu-id="fc9b4-157">비즈니스 그룹이 해당 액세스 패널에서 암호 Single Sign-On 응용 프로그램 권한에 대해 해당 사용자에게 할당된 자격 증명을 관리하도록 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-157">You can allow the business group to manage the credentials assigned to those users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="fc9b4-158">응용 프로그램에 대한 셀프 서비스 응용 프로그램 액세스를 사용하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-158">To enable self-service application access to an application, follow the steps below:</span></span>

1.  <span data-ttu-id="fc9b4-159">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-159">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fc9b4-160">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-160">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fc9b4-161">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-161">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fc9b4-162">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-162">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="fc9b4-163">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-163">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="fc9b4-164">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-164">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="fc9b4-165">셀프 서비스 액세스를 활성화하려는 응용 프로그램을 목록에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-165">Select the application you want to enable Self-service access to from the list.</span></span>

7.  <span data-ttu-id="fc9b4-166">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **셀프 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-166">Once the application loads, click **Self-service** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="fc9b4-167">이 응용 프로그램에 대한 셀프 서비스 응용 프로그램 액세스를 활성화하려면 **사용자가 이 응용 프로그램에 대한 액세스를 요청하도록 허용하시겠습니까?** 토글을 **예**로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-167">To enable Self-service application access for this application, turn the **Allow users to request access to this application?** toggle to **Yes.**</span></span>

9.  <span data-ttu-id="fc9b4-168">다음으로 이 응용 프로그램에 대한 액세스를 요청하는 사용자에 추가되어야 하는 그룹을 선택하려면 레이블 **할당된 사용자는 어느 그룹에 추가되어야 합니까?** 옆의 선택기를 클릭하고 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-168">Next, to select the group to which users who request access to this application should be added, click the selector next to the label **To which group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="fc9b4-169">**선택 사항:** 사용자의 액세스를 허용하기 전에 비즈니스 승인을 필요로 하려는 경우 **이 응용 프로그램에 대한 액세스를 부여하기 전에 승인이 필요합니까?** 토글을 **예**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-169">**Optional:** If you wish to require a business approval before users are allowed access, set the **Require approval before granting access to this application?** toggle to **Yes**.</span></span>

11. <span data-ttu-id="fc9b4-170">**선택 사항: 암호 Single Sign-On만을 사용하는 응용 프로그램의 경우** 해당 비즈니스 승인자가 승인된 사용자에 대한 이 응용 프로그램에 전송되는 암호를 지정하도록 허용하려는 경우 **승인자가 이 응용 프로그램에 대한 사용자의 암호를 설정하도록 허용하시겠습니까?** 토글을 **예**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-170">**Optional: For applications using password single-sign on only,** if you wish to allow those business approvers to specify the passwords that are sent to this application for approved users, set the **Allow approvers to set user’s passwords for this application?** toggle to **Yes**.</span></span>

12. <span data-ttu-id="fc9b4-171">**선택 사항:** 이 응용 프로그램에 대한 액세스를 승인할 수 있는 비즈니스 승인자를 지정하려면 레이블 **이 응용 프로그램에 대한 액세스는 누가 승인할 수 있습니까?** 옆의 선택기를 클릭하여 최대 10명의 개별 비즈니스 승인자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-171">**Optional:** To specify the business approvers who are allowed to approve access to this application, click the selector next to the label **Who is allowed to approve access to this application?** to select up to 10 individual business approvers.</span></span>

  >[!NOTE]
  ><span data-ttu-id="fc9b4-172">그룹은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-172">Groups are not supported.</span></span>
  >
  >

13. <span data-ttu-id="fc9b4-173">**선택 사항:** **역할을 표시하는 응용 프로그램의 경우** 셀프 서비스 승인된 사용자를 역할에 할당하려는 경우 **사용자를 이 응용 프로그램의 어떤 역할에 할당하시겠습니까?** 옆의 선택기를 클릭하여 이 사용자를 할당해야 하는 역할을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-173">**Optional:** **For applications which expose roles**, if you wish to assign self-service approved users to a role, click the selector next to the **To which role should users be assigned in this application?** to select the role to which these users should be assigned.</span></span>

14. <span data-ttu-id="fc9b4-174">블레이드의 위쪽에서 **저장** 단추를 클릭하여 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-174">Click the **Save** button at the top of the blade to finish.</span></span>

<span data-ttu-id="fc9b4-175">셀프 서비스 응용 프로그램 구성을 완료한 후 사용자는 [응용 프로그램 액세스 패널](https://myapps.microsoft.com/)로 이동하고 **+ 추가** 단추를 클릭하여 셀프 서비스 액세스를 활성화한 앱을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-175">Once you complete Self-service application configuration, users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled Self-service access.</span></span> <span data-ttu-id="fc9b4-176">비즈니스 승인자는 [응용 프로그램 액세스 패널](https://myapps.microsoft.com/)에서 알림을 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-176">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="fc9b4-177">사용자가 승인이 필요한 응용 프로그램에 대한 액세스를 요청한 경우 비즈니스 승인자에게 알리는 메일을 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-177">You can enable an email notifying them when a user has requested access to an application that requires their approval.</span></span> 

<span data-ttu-id="fc9b4-178">이러한 승인은 단일 승인 워크플로만 지원합니다. 즉, 여러 승인자를 지정하는 경우 모든 단일 승인자는 응용 프로그램에 대한 액세스를 승인합니다.</span><span class="sxs-lookup"><span data-stu-id="fc9b4-178">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approver access to the application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fc9b4-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fc9b4-179">Next steps</span></span>
[<span data-ttu-id="fc9b4-180">응용 프로그램 프록시를 사용하여 앱에 Single Sign-On 제공</span><span class="sxs-lookup"><span data-stu-id="fc9b4-180">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
