---
title: "응용 프로그램이 액세스 패널에 표시되는 방식 | Microsoft Docs"
description: "응용 프로그램이 액세스 패널에 표시되는 문제 해결"
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
ms.reviewr: japere
ms.openlocfilehash: f8ccf2cf66b49940bc7f2b9f4764020efc04838e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-applications-appear-on-the-access-panel"></a><span data-ttu-id="9d4d1-103">응용 프로그램이 액세스 패널에 표시되는 방식</span><span class="sxs-lookup"><span data-stu-id="9d4d1-103">How applications appear on the access panel</span></span>

<span data-ttu-id="9d4d1-104">액세스 패널은 웹 기반 포털로 Azure AD(Azure Active Directory)에 회사 또는 학교 계정이 있는 사용자가 Azure AD 관리자를 통해 액세스 권한을 부여 받은 클라우드 기반 응용 프로그램을 보고 시작할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="9d4d1-105">이러한 응용 프로그램은 Azure AD 포털에서 사용자를 대신하여 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-105">These applications are configured on behalf of the user in the Azure AD portal.</span></span> <span data-ttu-id="9d4d1-106">관리자는 사용자에게 직접 또는 사용자가 사용자의 액세스 패널에 표시되는 응용 프로그램에서 결과의 일부인 그룹에 응용 프로그램을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-106">The admin can provision the application to the user directly or to a group a user is part of resulting in the application appearing on the user’s Access Panel.</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="9d4d1-107">먼저 확인할 일반적인 문제</span><span class="sxs-lookup"><span data-stu-id="9d4d1-107">General issues to check first</span></span>

-   <span data-ttu-id="9d4d1-108">응용 프로그램이 사용자 또는 사용자가 구성원인 그룹에서 제거된 경우 몇 분 후에 사용자의 액세스 패널에 로그인하고 다시 로그아웃하여 응용 프로그램이 제거되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-108">If an application was just removed from a user or group the user is a member of, try to sign in and out again into the user’s Access Panel after a few minutes to see if the application is removed.</span></span>

-   <span data-ttu-id="9d4d1-109">라이선스가 사용자 또는 사용자가 구성원인 그룹에서 제거된 경우 변경 사항이 만들어질 그룹의 크기 및 복잡성에 따라 시간이 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-109">If a license was just removed from a user or group the user is a member of this may take a long time, depending on the size and complexity of the group for changes to be made.</span></span> <span data-ttu-id="9d4d1-110">액세스 패널에 로그인하기 전에 잠시 여유 시간을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-110">Allow for extra time before signing into the Access Panel.</span></span>

## <a name="problems-related-to-assigning-applications-to-users"></a><span data-ttu-id="9d4d1-111">사용자의 응용 프로그램 할당과 관련된 문제</span><span class="sxs-lookup"><span data-stu-id="9d4d1-111">Problems related to assigning applications to users</span></span>

<span data-ttu-id="9d4d1-112">사용자는 이전에 할당되었기 때문에 액세스 패널에 응용 프로그램이 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-112">A user may be seeing an application on their Access Panel because they had been previously assigned to it.</span></span> <span data-ttu-id="9d4d1-113">다음은 확인할 몇 가지 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-113">Below are some ways to check:</span></span>

-   [<span data-ttu-id="9d4d1-114">사용자가 응용 프로그램에 할당되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="9d4d1-114">Check if a user is assigned to the application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="9d4d1-115">사용자가 응용 프로그램과 관련된 라이센스가 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="9d4d1-115">Check if a user is under a license related to the application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)


### <a name="check-if-a-user-is-assigned-to-the-application"></a><span data-ttu-id="9d4d1-116">사용자가 응용 프로그램에 할당되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="9d4d1-116">Check if a user is assigned to the application</span></span>

<span data-ttu-id="9d4d1-117">사용자가 응용 프로그램에 할당되었는지 확인하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-117">To check if a user is assigned to the application, follow the steps below:</span></span>

1.  <span data-ttu-id="9d4d1-118">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-118">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="9d4d1-119">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-119">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9d4d1-120">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-120">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9d4d1-121">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-121">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9d4d1-122">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-122">click **All Applications** to view a list of all your applications.</span></span>

6.  <span data-ttu-id="9d4d1-123">문제의 응용 프로그램 이름을 **검색**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-123">**Search** for the name of the application in question.</span></span>

7.  <span data-ttu-id="9d4d1-124">**사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-124">click **Users and groups**.</span></span>

8.  <span data-ttu-id="9d4d1-125">사용자가 응용 프로그램에 할당되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-125">Check to see if your user is assigned to the application.</span></span>

  * <span data-ttu-id="9d4d1-126">응용 프로그램에서 사용자를 제거하려는 경우 사용자의 **행을 클릭**하고 **삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-126">If you want to remove the user from the application, **click the row** of the user and select **delete**.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-to-the-application"></a><span data-ttu-id="9d4d1-127">사용자가 응용 프로그램과 관련된 라이센스가 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="9d4d1-127">Check if a user is under a license related to the application</span></span>

<span data-ttu-id="9d4d1-128">사용자의 할당된 라이선스를 확인하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-128">To check a user’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="9d4d1-129">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-129">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="9d4d1-130">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-130">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9d4d1-131">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-131">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9d4d1-132">탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-132">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="9d4d1-133">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-133">click **All users**.</span></span>

6.  <span data-ttu-id="9d4d1-134">관심이 있는 사용자를 **검색**하고 **행을 클릭**하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-134">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="9d4d1-135">**라이선스**를 클릭하여 사용자가 현재 할당된 라이선스를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-135">click **Licenses** to see which licenses the user currently has assigned.</span></span>

   * <span data-ttu-id="9d4d1-136">사용자가 Office 라이선스에 할당된 경우 사용자의 액세스 패널에 나타나도록 자사 Office 응용 프로그램을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-136">If the user is assigned to an Office license this enable First Party Office applications to appear on the user’s Access Panel.</span></span>

## <a name="problems-related-to-assigning-applications-to-groups"></a><span data-ttu-id="9d4d1-137">그룹에 응용 프로그램 할당과 관련된 문제</span><span class="sxs-lookup"><span data-stu-id="9d4d1-137">Problems related to assigning applications to groups</span></span>

<span data-ttu-id="9d4d1-138">사용자는 응용 프로그램이 할당된 그룹에 속해 있으므로 액세스 패널에 응용 프로그램이 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-138">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned the application.</span></span> <span data-ttu-id="9d4d1-139">다음은 확인할 몇 가지 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-139">Below are some ways to check:</span></span>

-   [<span data-ttu-id="9d4d1-140">사용자의 그룹 멤버 자격 확인</span><span class="sxs-lookup"><span data-stu-id="9d4d1-140">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="9d4d1-141">사용자가 라이선스에 할당된 그룹의 멤버인지 확인</span><span class="sxs-lookup"><span data-stu-id="9d4d1-141">Check if a user is a member of a group assigned to a license</span></span>](#check-if-a-user-is-a-member-of-a-group-assigned-to-a-license)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="9d4d1-142">사용자의 그룹 멤버 자격 확인</span><span class="sxs-lookup"><span data-stu-id="9d4d1-142">Check a user’s group memberships</span></span>

<span data-ttu-id="9d4d1-143">그룹의 멤버 자격을 확인하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-143">To check a group’s membership, follow the steps below:</span></span>

1.  <span data-ttu-id="9d4d1-144">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-144">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="9d4d1-145">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-145">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9d4d1-146">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-146">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9d4d1-147">탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-147">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="9d4d1-148">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-148">click **All users**.</span></span>

6.  <span data-ttu-id="9d4d1-149">관심이 있는 사용자를 **검색**하고 **행을 클릭**하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-149">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="9d4d1-150">**그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-150">click **Groups.**</span></span>

8.  <span data-ttu-id="9d4d1-151">사용자가 응용 프로그램에 할당된 그룹에 속하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-151">Check to see if your user is part of a Group assigned to the application.</span></span>

   * <span data-ttu-id="9d4d1-152">그룹에서 사용자를 제거하려는 경우 그룹의 **행을 클릭**하고 삭제를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-152">If you want to remove the user from the group, **click the row** of the group and select delete.</span></span>

### <a name="check-if-a-user-is-a-member-of-a-group-assigned-to-a-license"></a><span data-ttu-id="9d4d1-153">사용자가 라이선스에 할당된 그룹의 멤버인지 확인</span><span class="sxs-lookup"><span data-stu-id="9d4d1-153">Check if a user is a member of a group assigned to a license</span></span>

1.  <span data-ttu-id="9d4d1-154">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-154">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="9d4d1-155">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-155">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9d4d1-156">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-156">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9d4d1-157">탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-157">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="9d4d1-158">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-158">click **All users**.</span></span>

6.  <span data-ttu-id="9d4d1-159">관심이 있는 사용자를 **검색**하고 **행을 클릭**하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-159">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="9d4d1-160">**그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-160">click **Groups.**</span></span>

8.  <span data-ttu-id="9d4d1-161">특정 그룹의 행을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-161">click the row of a specific group.</span></span>

9.  <span data-ttu-id="9d4d1-162">**라이선스**를 클릭하여 그룹이 할당된 라이선스를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-162">click **Licenses** to see which licenses the group has assigned to it.</span></span>

  * <span data-ttu-id="9d4d1-163">그룹이 Office 라이선스에 할당된 경우 사용자의 액세스 패널에 나타나도록 특정 자사 Office 응용 프로그램을 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-163">If the group is assigned to an Office license this may enable certain First Party Office applications to appear on the user’s Access Panel.</span></span>


## <a name="if-these-troubleshooting-steps-do-not-the-resolve-the-issue"></a><span data-ttu-id="9d4d1-164">이러한 문제 해결 단계가 문제를 해결하지 않는 경우</span><span class="sxs-lookup"><span data-stu-id="9d4d1-164">If these troubleshooting steps do not the resolve the issue</span></span>

<span data-ttu-id="9d4d1-165">사용할 수 있는 경우 다음 정보로 지원 티켓을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9d4d1-165">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="9d4d1-166">상관 관계 오류 ID</span><span class="sxs-lookup"><span data-stu-id="9d4d1-166">Correlation error ID</span></span>

-   <span data-ttu-id="9d4d1-167">UPN(사용자 전자 메일 주소)</span><span class="sxs-lookup"><span data-stu-id="9d4d1-167">UPN (user email address)</span></span>

-   <span data-ttu-id="9d4d1-168">테넌트 ID</span><span class="sxs-lookup"><span data-stu-id="9d4d1-168">Tenant ID</span></span>

-   <span data-ttu-id="9d4d1-169">브라우저 종류</span><span class="sxs-lookup"><span data-stu-id="9d4d1-169">Browser type</span></span>

-   <span data-ttu-id="9d4d1-170">오류가 발생하는 동안 표준 시간대 및 시간/기간</span><span class="sxs-lookup"><span data-stu-id="9d4d1-170">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="9d4d1-171">Fiddler 추적</span><span class="sxs-lookup"><span data-stu-id="9d4d1-171">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d4d1-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9d4d1-172">Next steps</span></span>
[<span data-ttu-id="9d4d1-173">Azure Active Directory로 응용 프로그램 관리</span><span class="sxs-lookup"><span data-stu-id="9d4d1-173">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
