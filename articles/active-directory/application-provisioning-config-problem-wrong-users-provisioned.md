---
title: "aaaWrong 일련의 사용자를 프로 비전 된 Azure AD tooan 갤러리 응용 프로그램 | Microsoft Docs"
description: "예상한 것 보다 응용 프로그램 tooan 아웃 명의 다른 집합 되는 이유는 toofind 프로 비전 하는 방법을 알아봅니다"
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
ms.openlocfilehash: adb90b12a53fb3160ce2b73b2559df92b283438e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="wrong-set-of-users-are-being-provisioned-tooan-azure-ad-gallery-application"></a><span data-ttu-id="a88a0-103">잘못 된 일련의 사용자를 프로 비전 된 Azure AD tooan 갤러리 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="a88a0-103">Wrong set of users are being provisioned tooan Azure AD Gallery application</span></span>

<span data-ttu-id="a88a0-104">어떤 사용자가 프로 비전 된 toohello 앱은 기본적으로 있는 사용자 및 그룹 된 **할당** toohello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-104">Which users are provisioned toohello app is primarily driven by which users and groups have been **assigned** toohello application.</span></span>

<span data-ttu-id="a88a0-105">어떻게 toolearn 아래 hello 리소스를 사용 하 여 사용자와 그룹을 Azure Active Directory 내에서 tooan 응용 프로그램 할당 된 toocheck 합니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-105">Use hello resources below toolearn how toocheck which users and groups have been assigned tooan application within Azure Active Directory.</span></span>

## <a name="assign-a-user-directly-as-an-administrator"></a><span data-ttu-id="a88a0-106">관리자 권한으로 직접 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="a88a0-106">Assign a user directly as an administrator</span></span>

<span data-ttu-id="a88a0-107">tooassign 아래의 hello 단계를 직접 수행 하는 하나 이상의 사용자가 tooan 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="a88a0-107">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="a88a0-108">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="a88a0-108">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="a88a0-109">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-109">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a88a0-110">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-110">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a88a0-111">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-111">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a88a0-112">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-112">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="a88a0-113">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="a88a0-113">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="a88a0-114">원하는 사용자 toofrom hello 목록 tooassign hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-114">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="a88a0-115">Hello 응용 프로그램 로드 되 면 클릭 **사용자 및 그룹** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-115">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="a88a0-116">Hello 클릭 **추가** hello 위로 단추 **사용자 및 그룹** 목록 tooopen hello **할당 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-116">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="a88a0-117">hello 클릭 **사용자 및 그룹** hello에서 선택기 **할당 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-117">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="a88a0-118">Hello 입력 **전체 이름** 또는 **전자 메일 주소** hello에 할당 하려는 hello 사용자의 **이름 또는 전자 메일 주소로 검색을 통해** 검색 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-118">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="a88a0-119">Hello 위로 마우스를 가져가고 **사용자** hello 목록 tooreveal에는 **확인란**합니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-119">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="a88a0-120">Hello 확인란 다음 toohello 사용자의 프로필 사진 또는 로고 tooadd 사용자 toohello 클릭 **선택한** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-120">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="a88a0-121">**선택 사항:** 너무 원하는 경우**둘 이상의 사용자를 추가**, 다른 유형 **전체 이름** 또는 **전자 메일 주소** hello에 **이름으로 검색 전자 메일 주소 또는** 상자에서 검색 하 고이 사용자 toohello hello 확인란 tooadd 클릭 **선택한** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-121">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="a88a0-122">사용자 선택을 완료 했으면 클릭 hello **선택** 단추 tooadd 해당 사용자 및 그룹 toobe toohello 목록이 toohello 응용 프로그램을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-122">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="a88a0-123">**선택 사항:** hello 클릭 **역할 선택** hello에 선택 기가 **할당 추가** 블레이드 tooselect 역할 tooassign toohello 사용자가 선택한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-123">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="a88a0-124">Hello 클릭 **할당** 단추 tooassign hello 응용 프로그램 toohello 사용자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-124">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="a88a0-125">이면 프로 비전 응용 프로그램에 대해 이미 실행 되 고 구성 된 새 사용자는 약 10 분 내에 프로 비전 된 tooan 응용 프로그램 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-125">If provisioning is configured and already running for an app, new users should be provisioned tooan application in approximately 10 minutes.</span></span> <span data-ttu-id="a88a0-126">Hello 확인 **감사 로그** 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-126">Check hello **Audit Logs** for details.</span></span>

## <a name="assign-a-group-directly-tooan-application-as-an-administrator"></a><span data-ttu-id="a88a0-127">그룹 할당 관리자 권한으로 직접 tooan 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="a88a0-127">Assign a group directly tooan application as an administrator</span></span>

<span data-ttu-id="a88a0-128">하나 이상의 tooassign 그룹 tooan 응용 프로그램을 직접 아래 hello 단계 수행:</span><span class="sxs-lookup"><span data-stu-id="a88a0-128">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="a88a0-129">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="a88a0-129">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="a88a0-130">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-130">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a88a0-131">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-131">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a88a0-132">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-132">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a88a0-133">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-133">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="a88a0-134">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="a88a0-134">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="a88a0-135">원하는 사용자 toofrom hello 목록 tooassign hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-135">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="a88a0-136">Hello 응용 프로그램 로드 되 면 클릭 **사용자 및 그룹** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-136">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="a88a0-137">Hello 클릭 **추가** hello 위로 단추 **사용자 및 그룹** 목록 tooopen hello **할당 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-137">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="a88a0-138">hello 클릭 **사용자 및 그룹** hello에서 선택기 **할당 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-138">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="a88a0-139">Hello 입력 **전체 그룹 이름** hello에 할당 하려는 hello 그룹의 **이름 또는 전자 메일 주소로 검색을 통해** 검색 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-139">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="a88a0-140">Hello 위로 마우스를 가져가고 **그룹** hello 목록 tooreveal에는 **확인란**합니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-140">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="a88a0-141">Hello 확인란 다음 toohello 그룹의 프로필 사진 또는 로고 tooadd 사용자 toohello 클릭 **선택한** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-141">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="a88a0-142">**선택 사항:** 너무 원하는 경우**둘 이상의 그룹을 추가**, 다른 유형 **전체 그룹 이름** hello에 **이름 또는 전자 메일 주소로 검색을 통해** 검색 상자 이 그룹 toohello hello 확인란 tooadd 클릭 **선택한** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-142">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="a88a0-143">그룹을 선택 하면 완료 했으면 클릭 hello **선택** 단추 tooadd 해당 사용자 및 그룹 toobe toohello 목록이 toohello 응용 프로그램을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-143">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="a88a0-144">**선택 사항:** hello 클릭 **역할 선택** hello에 선택 기가 **할당 추가** 블레이드 tooselect 역할 tooassign toohello 그룹 선택 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-144">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="a88a0-145">Hello 클릭 **할당** 단추 tooassign hello 응용 프로그램 toohello 선택 된 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-145">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="a88a0-146">프로 비전 하는 것은 응용 프로그램에 대해 이미 실행 되 고 구성 된, 하는 경우 hello 그룹 내에 포함 된 새 사용자는 약 10 분 내에 프로 비전 된 tooan 응용 프로그램 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-146">If provisioning is configured and already running for an app, new users contained within hello group should be provisioned tooan application in approximately 10 minutes.</span></span> <span data-ttu-id="a88a0-147">Hello 확인 **감사 로그** 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-147">Check hello **Audit Logs** for details.</span></span>

>[!IMPORTANT]
><span data-ttu-id="a88a0-148">프로 비전 하 고 그룹 이름을 hello 일부 응용 프로그램에 대 한 지원 되는 경우 추가 toohello 멤버에서 세부 정보를 그룹화 합니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-148">Provisioning of hello group name and group details, in addition toohello members, if supported for some applications.</span></span> <span data-ttu-id="a88a0-149">Hello를 사용 하지 않도록 설정 하거나 설정 하 여이 기능을 해제 하거나 설정할 수 있습니다 **매핑** hello에 표시 된 그룹 개체에 대 한 **프로 비전** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-149">You can enable or disable this functionality by enabling or disabling hello **Mapping** for group objects shown in hello **Provisioning** tab.</span></span> 
>
>

<span data-ttu-id="a88a0-150">그룹을 프로 비전을 사용 하는 경우 tooreview hello 특성 매핑을 tooensure를 적절 한 필드 "일치 하는 ID" hello에 사용 되 고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-150">If provisioning groups is enabled, be sure tooreview hello attribute mappings tooensure an appropriate field is being used for hello “matching ID”.</span></span> <span data-ttu-id="a88a0-151">이 hello 표시 이름 또는 전자 메일 별칭, hello 그룹 및 해당 멤버를 프로 비전 할 여부 hello 일치 하는 속성이 비어 있으면으로 채워진 그룹에 대 한 Azure AD에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="a88a0-151">This can be hello display name or email alias, as hello group and its members not be provisioned if hello matching property is empty or not populated for a group in Azure AD.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a88a0-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a88a0-152">Next steps</span></span>
[<span data-ttu-id="a88a0-153">사용자 프로 비전 및 프로 비전 해제 tooSaaS Azure Active Directory와 응용 프로그램 자동화</span><span class="sxs-lookup"><span data-stu-id="a88a0-153">Automate User Provisioning and Deprovisioning tooSaaS Applications with Azure Active Directory</span></span>](active-directory-saas-app-provisioning.md)
