---
title: "aaaHow tooassign 사용자 및 그룹 tooan 응용 프로그램 | Microsoft Docs"
description: "응용 프로그램 toogrant 액세스 toohello 사용자 할당"
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
ms.openlocfilehash: e039a26e4b8f88ad747354859f1071b8f74b6789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooassign-users-and-groups-tooan-application"></a><span data-ttu-id="13ec6-103">어떻게 tooassign 사용자 및 그룹 tooan 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="13ec6-103">How tooassign users and groups tooan application</span></span>

<span data-ttu-id="13ec6-104">사용자가 특정 응용 프로그램에 대 한 아래 hello 중 하나를 수행을 먼저 toofirst **toohello 응용 프로그램에 할당** toogrant 액세스:</span><span class="sxs-lookup"><span data-stu-id="13ec6-104">Before your users can do any of hello below for a specific application, you need toofirst **assign them toohello application** toogrant them access:</span></span>

-   <span data-ttu-id="13ec6-105">응용 프로그램 액세스 **toohello 응용 프로그램의 URL을 직접 탐색** (라고도 SP에서 시작한 로그온).</span><span class="sxs-lookup"><span data-stu-id="13ec6-105">Access an application by **navigating toohello application’s URL directly** (also known as SP-initiated sign-on).</span></span>

-   <span data-ttu-id="13ec6-106">Hello를 사용 하 여 응용 프로그램에 액세스 **사용자 액세스 URL** 응용 프로그램에 **속성** 페이지 (라고도 IDP가 시작한 로그온).</span><span class="sxs-lookup"><span data-stu-id="13ec6-106">Access an application by using hello **User Access URL** on an application’s **Properties** page (also known as IDP-initiated sign on).</span></span>

-   <span data-ttu-id="13ec6-107">[응용 프로그램 액세스 패널](https://myapps.microsoft.com/) 또는 모바일 응용 프로그램에 응용 프로그램이 나타나는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-107">See an application appear on their [Application Access Panel](https://myapps.microsoft.com/) or mobile application.</span></span>

-   <span data-ttu-id="13ec6-108">[Office 365 응용 프로그램 시작 관리자](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a)에 응용 프로그램이 나타나는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-108">See an application appear on their [Office 365 Application Launcher](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a).</span></span>

## <a name="methods-tooassign-applications-with-azure-active-directory"></a><span data-ttu-id="13ec6-109">Azure Active Directory와 메서드 tooassign 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="13ec6-109">Methods tooassign applications with Azure Active Directory</span></span> 

<span data-ttu-id="13ec6-110">Azure Active Directory로 응용 프로그램을 할당할 수 있는 3가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-110">There are 3 ways you can assign applications with Azure Active Directory:</span></span>

-   [<span data-ttu-id="13ec6-111">사용자 지정 관리자 권한으로 직접 tooan 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="13ec6-111">Assign a user directly tooan application as an administrator</span></span>](#assign-a-user-directly-as-an-administrator)

-   [<span data-ttu-id="13ec6-112">그룹 할당 관리자 권한으로 직접 tooan 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="13ec6-112">Assign a group directly tooan application as an administrator</span></span>](#assign-a-group-directly-to-an-application-as-an-administrator)

-   [<span data-ttu-id="13ec6-113">셀프 서비스 응용 프로그램 액세스 tooallow 사용자 toofind 자신의 응용 프로그램 사용</span><span class="sxs-lookup"><span data-stu-id="13ec6-113">Enable self-service application access tooallow users toofind their own applications</span></span>](#enable-self-service-application-access-to-allow-users-to-find-their-own-applications)

## <a name="assign-a-user-directly-as-an-administrator"></a><span data-ttu-id="13ec6-114">관리자 권한으로 직접 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="13ec6-114">Assign a user directly as an administrator</span></span>

<span data-ttu-id="13ec6-115">tooassign 아래의 hello 단계를 직접 수행 하는 하나 이상의 사용자가 tooan 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="13ec6-115">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="13ec6-116">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="13ec6-116">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="13ec6-117">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-117">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="13ec6-118">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-118">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="13ec6-119">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-119">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="13ec6-120">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-120">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="13ec6-121">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="13ec6-121">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="13ec6-122">원하는 사용자 toofrom hello 목록 tooassign hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-122">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="13ec6-123">Hello 응용 프로그램 로드 되 면 클릭 **사용자 및 그룹** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-123">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="13ec6-124">Hello 클릭 **추가** hello 위로 단추 **사용자 및 그룹** 목록 tooopen hello **할당 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-124">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="13ec6-125">hello 클릭 **사용자 및 그룹** hello에서 선택기 **할당 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-125">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="13ec6-126">Hello 입력 **전체 이름** 또는 **전자 메일 주소** hello에 할당 하려는 hello 사용자의 **이름 또는 전자 메일 주소로 검색을 통해** 검색 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-126">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="13ec6-127">Hello 위로 마우스를 가져가고 **사용자** hello 목록 tooreveal에는 **확인란**합니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-127">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="13ec6-128">Hello 확인란 다음 toohello 사용자의 프로필 사진 또는 로고 tooadd 사용자 toohello 클릭 **선택한** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-128">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="13ec6-129">**선택 사항:** 너무 원하는 경우**둘 이상의 사용자를 추가**, 다른 유형 **전체 이름** 또는 **전자 메일 주소** hello에 **이름으로 검색 전자 메일 주소 또는** 상자에서 검색 하 고이 사용자 toohello hello 확인란 tooadd 클릭 **선택한** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-129">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="13ec6-130">사용자 선택을 완료 했으면 클릭 hello **선택** 단추 tooadd 해당 사용자 및 그룹 toobe toohello 목록이 toohello 응용 프로그램을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-130">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="13ec6-131">**선택 사항:** hello 클릭 **역할 선택** hello에 선택 기가 **할당 추가** 블레이드 tooselect 역할 tooassign toohello 사용자가 선택한 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-131">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="13ec6-132">Hello 클릭 **할당** 단추 tooassign hello 응용 프로그램 toohello 사용자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-132">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="13ec6-133">시간의 짧은 기간 이후에 hello 사용자가 선택한 이러한 응용 프로그램을 사용 하 여 hello hello 솔루션 설명 섹션에 설명 된 방법 수 toolaunch 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-133">After a short period of time, hello users you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span>

## <a name="assign-a-group-directly-tooan-application-as-an-administrator"></a><span data-ttu-id="13ec6-134">그룹 할당 관리자 권한으로 직접 tooan 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="13ec6-134">Assign a group directly tooan application as an administrator</span></span>

<span data-ttu-id="13ec6-135">하나 이상의 tooassign 그룹 tooan 응용 프로그램을 직접 아래 hello 단계 수행:</span><span class="sxs-lookup"><span data-stu-id="13ec6-135">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="13ec6-136">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="13ec6-136">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="13ec6-137">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-137">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="13ec6-138">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-138">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="13ec6-139">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-139">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="13ec6-140">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-140">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="13ec6-141">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="13ec6-141">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="13ec6-142">원하는 사용자 toofrom hello 목록 tooassign hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-142">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="13ec6-143">Hello 응용 프로그램 로드 되 면 클릭 **사용자 및 그룹** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-143">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="13ec6-144">Hello 클릭 **추가** hello 위로 단추 **사용자 및 그룹** 목록 tooopen hello **할당 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-144">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="13ec6-145">hello 클릭 **사용자 및 그룹** hello에서 선택기 **할당 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-145">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="13ec6-146">Hello 입력 **전체 그룹 이름** hello에 할당 하려는 hello 그룹의 **이름 또는 전자 메일 주소로 검색을 통해** 검색 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-146">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="13ec6-147">Hello 위로 마우스를 가져가고 **그룹** hello 목록 tooreveal에는 **확인란**합니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-147">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="13ec6-148">Hello 확인란 다음 toohello 그룹의 프로필 사진 또는 로고 tooadd 사용자 toohello 클릭 **선택한** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-148">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="13ec6-149">**선택 사항:** 너무 원하는 경우**둘 이상의 그룹을 추가**, 다른 유형 **전체 그룹 이름** hello에 **이름 또는 전자 메일 주소로 검색을 통해** 검색 상자 이 그룹 toohello hello 확인란 tooadd 클릭 **선택한** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-149">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="13ec6-150">그룹을 선택 하면 완료 했으면 클릭 hello **선택** 단추 tooadd 해당 사용자 및 그룹 toobe toohello 목록이 toohello 응용 프로그램을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-150">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="13ec6-151">**선택 사항:** hello 클릭 **역할 선택** hello에 선택 기가 **할당 추가** 블레이드 tooselect 역할 tooassign toohello 그룹 선택 했습니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-151">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="13ec6-152">Hello 클릭 **할당** 단추 tooassign hello 응용 프로그램 toohello 선택 된 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-152">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="13ec6-153">시간의 짧은 기간 이후에 hello 사용자가 선택한 hello 그룹 내에서 이러한 응용 프로그램을 사용 하 여 hello hello 솔루션 설명 섹션에 설명 된 방법 수 toolaunch 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-153">After a short period of time, hello users within hello groups you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span> <span data-ttu-id="13ec6-154">동적 그룹인 경우 이러한 할당된 그룹 내 사용자에 대해 표시되는 이러한 할당에 약간의 추가 처리 지연이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-154">If these are dynamic groups, there may be some additional processing delay in these assignments appearing for users within these assigned groups.</span></span>

## <a name="enable-self-service-application-access-tooallow-users-toofind-their-own-applications"></a><span data-ttu-id="13ec6-155">셀프 서비스 응용 프로그램 액세스 tooallow 사용자 toofind 자신의 응용 프로그램 사용</span><span class="sxs-lookup"><span data-stu-id="13ec6-155">Enable self-service application access tooallow users toofind their own applications</span></span>

<span data-ttu-id="13ec6-156">셀프 서비스 응용 프로그램 액세스는 좋은 방법 tooallow 사용자 tooself-필요에 따라 hello 비즈니스 그룹 액세스 하도록 허용 tooapprove toothose 응용 프로그램, 응용 프로그램을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-156">Self-service application access is a great way tooallow users tooself-discover applications, optionally allow hello business group tooapprove access toothose applications.</span></span> <span data-ttu-id="13ec6-157">Hello 비즈니스 그룹 toomanage hello 자격 증명 toothose 사용자가 액세스 패널에서 응용 프로그램에 Single-sign 암호 오른쪽에 대 한 할당을 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-157">You can allow hello business group toomanage hello credentials assigned toothose users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="13ec6-158">tooenable 셀프 서비스 응용 프로그램 액세스 tooan 응용 프로그램, 다음 단계에 따라 hello:</span><span class="sxs-lookup"><span data-stu-id="13ec6-158">tooenable self-service application access tooan application, follow hello steps below:</span></span>

1.  <span data-ttu-id="13ec6-159">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="13ec6-159">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="13ec6-160">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-160">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="13ec6-161">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-161">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="13ec6-162">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-162">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="13ec6-163">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-163">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="13ec6-164">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="13ec6-164">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="13ec6-165">Tooenable 셀프 서비스 액세스 toofrom hello 목록을 사용 하려는 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-165">Select hello application you want tooenable Self-service access toofrom hello list.</span></span>

7.  <span data-ttu-id="13ec6-166">Hello 응용 프로그램 로드 되 면 클릭 **셀프 서비스** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-166">Once hello application loads, click **Self-service** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="13ec6-167">이 응용 프로그램에 대 한 셀프 서비스 응용 프로그램 액세스 tooenable hello 설정 **toorequest access toothis 응용 프로그램 사용자가 허용?** 너무 설정/해제**예입니다.**</span><span class="sxs-lookup"><span data-stu-id="13ec6-167">tooenable Self-service application access for this application, turn hello **Allow users toorequest access toothis application?** toggle too**Yes.**</span></span>

9.  <span data-ttu-id="13ec6-168">Tooselect hello 그룹 toowhich 요청 하는 사용자 액세스 toothis 응용 프로그램을 추가 하도록 hello 선택기 다음 toohello 레이블을 클릭 하는 다음으로, **toowhich 그룹은 할당 된 사용자를 추가할 수?** 그룹을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-168">Next, tooselect hello group toowhich users who request access toothis application should be added, click hello selector next toohello label **toowhich group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="13ec6-169">**선택 사항:** 원할 경우 toorequire 비즈니스 승인 사용자의 액세스가 허용 되기 전에 설정 hello **toothis 응용 프로그램 액세스 권한을 부여 하기 전에 승인 필요?** 너무 설정/해제**예**합니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-169">**Optional:** If you wish toorequire a business approval before users are allowed access, set hello **Require approval before granting access toothis application?** toggle too**Yes**.</span></span>

11. <span data-ttu-id="13ec6-170">**선택 사항:에 대 한 응용 프로그램에서 사용 하 여 암호 단일 로그인만** toothis 응용 프로그램 승인 된 사용자가을 전송 하는 이러한 비즈니스 승인자 toospecify hello 암호 tooallow 하려는 경우 설정 hello **승인자 tooset 허용 이 응용 프로그램에 대 한 사용자의 암호?**  너무 설정/해제**예**합니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-170">**Optional: For applications using password single-sign on only,** if you wish tooallow those business approvers toospecify hello passwords that are sent toothis application for approved users, set hello **Allow approvers tooset user’s passwords for this application?** toggle too**Yes**.</span></span>

12. <span data-ttu-id="13ec6-171">**선택 사항:** tooapprove access toothis 응용 프로그램 수 있는 toospecify hello 비즈니스 승인자 hello 선택기 다음 toohello 레이블을 클릭 **tooapprove 액세스 toothis 응용 프로그램이 허용 되는 사용자?** tooselect를 too10 개별 비즈니스 승인자 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-171">**Optional:** toospecify hello business approvers who are allowed tooapprove access toothis application, click hello selector next toohello label **Who is allowed tooapprove access toothis application?** tooselect up too10 individual business approvers.</span></span>

  >[!NOTE]
  ><span data-ttu-id="13ec6-172">그룹은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-172">Groups are not supported.</span></span>
  >
  >

13. <span data-ttu-id="13ec6-173">**선택 사항:** **역할을 표시 하는 응용 프로그램에 대 한**tooassign 승인 된 사용자가 셀프 서비스 tooa 역할 하려는 경우, hello 선택기 다음 toohello 클릭 **toowhich 역할이이 사용자가 할당 해야 응용 프로그램?**  tooselect hello 역할 toowhich 이러한 사용자만 할당 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-173">**Optional:** **For applications which expose roles**, if you wish tooassign self-service approved users tooa role, click hello selector next toohello **toowhich role should users be assigned in this application?** tooselect hello role toowhich these users should be assigned.</span></span>

14. <span data-ttu-id="13ec6-174">Hello 클릭 **저장** hello 블레이드 toofinish hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-174">Click hello **Save** button at hello top of hello blade toofinish.</span></span>

<span data-ttu-id="13ec6-175">셀프 서비스 응용 프로그램 구성을 완료 한 후 탐색할 수 tootheir [응용 프로그램 액세스 패널로](https://myapps.microsoft.com/) hello를 클릭 하 고 **+ 추가** 단추 toofind hello 앱 toowhich 사용 하도록 설정한 셀프 서비스 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-175">Once you complete Self-service application configuration, users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled Self-service access.</span></span> <span data-ttu-id="13ec6-176">비즈니스 승인자는 [응용 프로그램 액세스 패널](https://myapps.microsoft.com/)에서 알림을 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-176">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="13ec6-177">사용자가 승인을 해야 하는 액세스 tooan 응용 프로그램을 요청 하는 경우 사용자에 게 알리는 전자 메일을 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-177">You can enable an email notifying them when a user has requested access tooan application that requires their approval.</span></span> 

<span data-ttu-id="13ec6-178">이러한 승인은 즉 여러 승인자를 지정 하면 모든 단일 승인자 수 승인자 액세스 toohello 응용 프로그램이 단일 승인 워크플로만 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-178">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approver access toohello application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13ec6-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="13ec6-179">Next steps</span></span>
[<span data-ttu-id="13ec6-180">응용 프로그램 프록시 single sign on tooyour 앱을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ec6-180">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
