---
title: "hello 액세스 패널에 나타나는 aaaHow 응용 프로그램 | Microsoft Docs"
description: "응용 프로그램은 hello 액세스 패널에에서 나타나지 않는 문제 해결"
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
ms.openlocfilehash: 14ee732c4ed5260cba878e949cf9d90877aee67e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-applications-appear-on-hello-access-panel"></a><span data-ttu-id="0bb63-103">Hello 액세스 패널에 응용 프로그램이 표시 하는 방법</span><span class="sxs-lookup"><span data-stu-id="0bb63-103">How applications appear on hello access panel</span></span>

<span data-ttu-id="0bb63-104">hello 액세스 패널은 작업으로는 사용할 수 있는 웹 기반 포털 또는 학교 계정을 Azure Active Directory (Azure AD) tooview 및 시작 클라우드 기반 응용 프로그램에서 해당 hello Azure AD 관리자가 부여 해 준에 대 한 액세스.</span><span class="sxs-lookup"><span data-stu-id="0bb63-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="0bb63-105">이러한 응용 프로그램 hello Azure AD 포털에서 hello 사용자를 대신 하 여 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="0bb63-106">admin 님 안녕하세요 hello 응용 프로그램 toohello 사용자 직접 또는 사용자가 hello 사용자의 액세스 패널에 표시 되는 hello 응용 프로그램에서 결과의 일부 tooa 그룹 프로 비전 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-106">hello admin can provision hello application toohello user directly or tooa group a user is part of resulting in hello application appearing on hello user’s Access Panel.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="0bb63-107">일반 toocheck를 먼저 문제</span><span class="sxs-lookup"><span data-stu-id="0bb63-107">General issues toocheck first</span></span>

-   <span data-ttu-id="0bb63-108">응용 프로그램 사용자 로부터 방금 제거한 hello 사용자 그룹의 멤버인 경우 다시 toosign 및 축소 hello 사용자의 액세스 패널에 몇 분 toosee 후 hello 응용 프로그램을 제거 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="0bb63-108">If an application was just removed from a user or group hello user is a member of, try toosign in and out again into hello user’s Access Panel after a few minutes toosee if hello application is removed.</span></span>

-   <span data-ttu-id="0bb63-109">사용자 또는 그룹 hello 사용자에서 라이선스가 제거 방금 되었으면는이 멤버는 변경 내용 toobe 수행에 대 한 hello 그룹의 hello 크기와 복잡성에 따라 시간이 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-109">If a license was just removed from a user or group hello user is a member of this may take a long time, depending on hello size and complexity of hello group for changes toobe made.</span></span> <span data-ttu-id="0bb63-110">Hello 액세스 패널에 로그인 하기 전에 추가 시간을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-110">Allow for extra time before signing into hello Access Panel.</span></span>

## <a name="problems-related-tooassigning-applications-toousers"></a><span data-ttu-id="0bb63-111">문제 관련된 tooassigning 응용 프로그램 toousers</span><span class="sxs-lookup"><span data-stu-id="0bb63-111">Problems related tooassigning applications toousers</span></span>

<span data-ttu-id="0bb63-112">사용자 표시 될 수는 응용 프로그램 액세스 패널에서은 이전에 할당 된 tooit 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-112">A user may be seeing an application on their Access Panel because they had been previously assigned tooit.</span></span> <span data-ttu-id="0bb63-113">다음은 몇 가지 방법으로 toocheck입니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-113">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="0bb63-114">사용자가 toohello 응용 프로그램을 할당 하는 경우 확인</span><span class="sxs-lookup"><span data-stu-id="0bb63-114">Check if a user is assigned toohello application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="0bb63-115">사용자 라이선스 인지 확인 toohello 응용 프로그램 관련</span><span class="sxs-lookup"><span data-stu-id="0bb63-115">Check if a user is under a license related toohello application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)


### <a name="check-if-a-user-is-assigned-toohello-application"></a><span data-ttu-id="0bb63-116">사용자가 toohello 응용 프로그램을 할당 하는 경우 확인</span><span class="sxs-lookup"><span data-stu-id="0bb63-116">Check if a user is assigned toohello application</span></span>

<span data-ttu-id="0bb63-117">toocheck 사용자 toohello 응용 프로그램에 지정 되 면 hello 아래의 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-117">toocheck if a user is assigned toohello application, follow hello steps below:</span></span>

1.  <span data-ttu-id="0bb63-118">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="0bb63-118">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="0bb63-119">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-119">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="0bb63-120">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-120">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="0bb63-121">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-121">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="0bb63-122">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-122">click **All Applications** tooview a list of all your applications.</span></span>

6.  <span data-ttu-id="0bb63-123">**검색** hello 응용 프로그램과의 hello 이름에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-123">**Search** for hello name of hello application in question.</span></span>

7.  <span data-ttu-id="0bb63-124">**사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-124">click **Users and groups**.</span></span>

8.  <span data-ttu-id="0bb63-125">이때 회원님의 사용자 toohello 응용 프로그램에 할당 된 경우 toosee를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-125">Check toosee if your user is assigned toohello application.</span></span>

  * <span data-ttu-id="0bb63-126">Hello 응용 프로그램에서 사용자가 tooremove hello **hello 행 클릭** hello 사용자를 선택 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-126">If you want tooremove hello user from hello application, **click hello row** of hello user and select **delete**.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-toohello-application"></a><span data-ttu-id="0bb63-127">사용자 라이선스 인지 확인 toohello 응용 프로그램 관련</span><span class="sxs-lookup"><span data-stu-id="0bb63-127">Check if a user is under a license related toohello application</span></span>

<span data-ttu-id="0bb63-128">toocheck 사용자의 라이선스를 다음 단계에 따라 hello 할당:</span><span class="sxs-lookup"><span data-stu-id="0bb63-128">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="0bb63-129">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="0bb63-129">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="0bb63-130">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-130">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="0bb63-131">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-131">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="0bb63-132">클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-132">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="0bb63-133">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-133">click **All users**.</span></span>

6.  <span data-ttu-id="0bb63-134">**검색** 에 관심이 있는 hello 사용자에 대 한 및 **hello 행 클릭** tooselect 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-134">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="0bb63-135">클릭 **라이선스** toosee 현재 어떤 라이선스 hello 사용자에 게 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-135">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

   * <span data-ttu-id="0bb63-136">Hello 사용자가 할당 된 tooan Office 라이선스 하는 경우 첫 번째 파티 Office 응용 프로그램 tooappear hello 사용자의 액세스 패널에 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-136">If hello user is assigned tooan Office license this enable First Party Office applications tooappear on hello user’s Access Panel.</span></span>

## <a name="problems-related-tooassigning-applications-toogroups"></a><span data-ttu-id="0bb63-137">문제 관련된 tooassigning 응용 프로그램 toogroups</span><span class="sxs-lookup"><span data-stu-id="0bb63-137">Problems related tooassigning applications toogroups</span></span>

<span data-ttu-id="0bb63-138">사용자 표시 될 수는 응용 프로그램 액세스 패널에서 hello 응용 프로그램 할당 된 그룹의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-138">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned hello application.</span></span> <span data-ttu-id="0bb63-139">다음은 몇 가지 방법으로 toocheck입니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-139">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="0bb63-140">사용자의 그룹 구성원 자격 확인</span><span class="sxs-lookup"><span data-stu-id="0bb63-140">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="0bb63-141">사용자 tooa 라이선스를 할당 된 그룹의 구성원 인지 확인</span><span class="sxs-lookup"><span data-stu-id="0bb63-141">Check if a user is a member of a group assigned tooa license</span></span>](#check-if-a-user-is-a-member-of-a-group-assigned-to-a-license)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="0bb63-142">사용자의 그룹 구성원 자격 확인</span><span class="sxs-lookup"><span data-stu-id="0bb63-142">Check a user’s group memberships</span></span>

<span data-ttu-id="0bb63-143">toocheck 그룹의 구성원, 다음 단계에 따라 hello:</span><span class="sxs-lookup"><span data-stu-id="0bb63-143">toocheck a group’s membership, follow hello steps below:</span></span>

1.  <span data-ttu-id="0bb63-144">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="0bb63-144">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="0bb63-145">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-145">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="0bb63-146">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-146">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="0bb63-147">클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-147">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="0bb63-148">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-148">click **All users**.</span></span>

6.  <span data-ttu-id="0bb63-149">**검색** 에 관심이 있는 hello 사용자에 대 한 및 **hello 행 클릭** tooselect 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-149">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="0bb63-150">**그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-150">click **Groups.**</span></span>

8.  <span data-ttu-id="0bb63-151">이때 회원님의 사용자는 할당 된 그룹 toohello 응용 프로그램의 일부인 경우 toosee를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-151">Check toosee if your user is part of a Group assigned toohello application.</span></span>

   * <span data-ttu-id="0bb63-152">Hello 그룹에서 사용자가 tooremove hello **hello 행 클릭** hello 그룹 및 삭제를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-152">If you want tooremove hello user from hello group, **click hello row** of hello group and select delete.</span></span>

### <a name="check-if-a-user-is-a-member-of-a-group-assigned-tooa-license"></a><span data-ttu-id="0bb63-153">사용자 tooa 라이선스를 할당 된 그룹의 구성원 인지 확인</span><span class="sxs-lookup"><span data-stu-id="0bb63-153">Check if a user is a member of a group assigned tooa license</span></span>

1.  <span data-ttu-id="0bb63-154">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="0bb63-154">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="0bb63-155">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-155">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="0bb63-156">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-156">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="0bb63-157">클릭 **사용자 및 그룹** hello 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-157">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="0bb63-158">**모든 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-158">click **All users**.</span></span>

6.  <span data-ttu-id="0bb63-159">**검색** 에 관심이 있는 hello 사용자에 대 한 및 **hello 행 클릭** tooselect 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-159">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="0bb63-160">**그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-160">click **Groups.**</span></span>

8.  <span data-ttu-id="0bb63-161">특정 그룹의 hello 행을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-161">click hello row of a specific group.</span></span>

9.  <span data-ttu-id="0bb63-162">클릭 **라이선스** toosee 라이선스 hello 그룹 tooit에 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-162">click **Licenses** toosee which licenses hello group has assigned tooit.</span></span>

  * <span data-ttu-id="0bb63-163">Hello 그룹이 할당 된 tooan Office 라이선스 이면이 hello 사용자의 액세스 패널에 첫 번째 파티 Office 응용 프로그램 tooappear 특정로 설정 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-163">If hello group is assigned tooan Office license this may enable certain First Party Office applications tooappear on hello user’s Access Panel.</span></span>


## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a><span data-ttu-id="0bb63-164">이러한 문제 해결 단계 hello 하지 않는 경우 hello 문제 해결</span><span class="sxs-lookup"><span data-stu-id="0bb63-164">If these troubleshooting steps do not hello resolve hello issue</span></span>

<span data-ttu-id="0bb63-165">사용 가능한 경우 다음 정보는 hello로 지원 티켓을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0bb63-165">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="0bb63-166">상관 관계 오류 ID</span><span class="sxs-lookup"><span data-stu-id="0bb63-166">Correlation error ID</span></span>

-   <span data-ttu-id="0bb63-167">UPN(사용자 전자 메일 주소)</span><span class="sxs-lookup"><span data-stu-id="0bb63-167">UPN (user email address)</span></span>

-   <span data-ttu-id="0bb63-168">테넌트 ID</span><span class="sxs-lookup"><span data-stu-id="0bb63-168">Tenant ID</span></span>

-   <span data-ttu-id="0bb63-169">브라우저 종류</span><span class="sxs-lookup"><span data-stu-id="0bb63-169">Browser type</span></span>

-   <span data-ttu-id="0bb63-170">오류가 발생하는 동안 표준 시간대 및 시간/기간</span><span class="sxs-lookup"><span data-stu-id="0bb63-170">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="0bb63-171">Fiddler 추적</span><span class="sxs-lookup"><span data-stu-id="0bb63-171">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="0bb63-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0bb63-172">Next steps</span></span>
[<span data-ttu-id="0bb63-173">Azure Active Directory로 응용 프로그램 관리</span><span class="sxs-lookup"><span data-stu-id="0bb63-173">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
