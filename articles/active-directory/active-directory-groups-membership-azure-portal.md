---
title: "그룹에 속한 Azure Active Directory tooin aaaManage hello 그룹 | Microsoft Docs"
description: "Azure Active Directory에서 그룹은 다른 그룹을 포함할 수 있습니다. 다음은 어떻게 toomanage 해당 구성원 자격."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e785c2d0-7724-47d4-a56e-c58280c08a14
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0a0a1967084de0968e1e802559f9cdfd7ca6ae4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-toowhich-groups-a-group-belongs-in-your-azure-active-directory-tenant"></a><span data-ttu-id="486eb-104">Azure Active Directory 테 넌 트에 그룹이 속한 toowhich 그룹 관리</span><span class="sxs-lookup"><span data-stu-id="486eb-104">Manage toowhich groups a group belongs in your Azure Active Directory tenant</span></span>
<span data-ttu-id="486eb-105">Azure Active Directory에서 그룹은 다른 그룹을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="486eb-105">Groups can contain other groups in Azure Active Directory.</span></span> <span data-ttu-id="486eb-106">다음은 어떻게 toomanage 해당 구성원 자격.</span><span class="sxs-lookup"><span data-stu-id="486eb-106">Here's how toomanage those memberships.</span></span>

## <a name="how-do-i-find-hello-groups-my-group-is-a-member-of"></a><span data-ttu-id="486eb-107">Hello 그룹 내 그룹의 구성원임을 찾으려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="486eb-107">How do I find hello groups my group is a member of?</span></span>
1. <span data-ttu-id="486eb-108">Toohello 로그인 [Azure 포털](https://portal.azure.com) hello 디렉터리에 대 한 전역 관리자 인 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="486eb-108">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="486eb-109">선택 **더 많은 서비스**, 입력 **사용자 및 그룹** 에 hello 텍스트 상자를 선택한 후 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="486eb-109">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![사용자 관리 열기](./media/active-directory-groups-membership-azure-portal/search-user-management.png)
3. <span data-ttu-id="486eb-111">Hello에 **사용자 및 그룹** 블레이드를 **모든 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="486eb-111">On hello **Users and groups** blade, select **All groups**.</span></span>

   ![Hello 그룹 블레이드 열기](./media/active-directory-groups-membership-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="486eb-113">Hello에 **사용자 및 그룹-모든 그룹** 블레이드에서 그룹을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="486eb-113">On hello **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="486eb-114">Hello에 **그룹- *groupname* ** 블레이드를 **그룹 구성원 자격**합니다.</span><span class="sxs-lookup"><span data-stu-id="486eb-114">On hello **Group - *groupname*** blade, select **Group memberships**.</span></span>

   ![Hello 그룹 멤버 자격 블레이드 열기](./media/active-directory-groups-membership-azure-portal/group-membership-blade.png)
6. <span data-ttu-id="486eb-116">tooadd hello에 다른 그룹의 구성원으로 그룹 **그룹-그룹 구성원 자격** 블레이드, 선택 hello **추가** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="486eb-116">tooadd your group as a member of another group, on hello **Group - Group memberships** blade, select hello **Add** command.</span></span>
7. <span data-ttu-id="486eb-117">Hello에서 그룹을 선택 **그룹 선택** 블레이드에서 하 고 다음 선택 hello **선택** hello hello 블레이드 맨 아래에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="486eb-117">Select a group from hello **Select Group** blade, and then select hello **Select** button at hello bottom of hello blade.</span></span> <span data-ttu-id="486eb-118">한 번에 그룹 tooonly 한 그룹을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="486eb-118">You can add your group tooonly one group at a time.</span></span> <span data-ttu-id="486eb-119">hello **사용자** 상자 필터 hello 일치 항목 tooany 부분은 사용자 또는 장치 이름 기준으로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="486eb-119">hello **User** box filters hello display based on matching your entry tooany part of a user or device name.</span></span> <span data-ttu-id="486eb-120">와일드카드 문자는 해당 상자에서 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="486eb-120">No wildcard characters are accepted in that box.</span></span>

   ![그룹 멤버 자격 추가](./media/active-directory-groups-membership-azure-portal/add-group-membership.png)
8. <span data-ttu-id="486eb-122">tooremove hello에 다른 그룹의 구성원으로 그룹 **그룹-그룹 구성원 자격** 블레이드에서 그룹을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="486eb-122">tooremove your group as a member of another group, on hello **Group - Group memberships** blade, select a group.</span></span>
9. <span data-ttu-id="486eb-123">Hello에 ***groupname*** 블레이드, 선택 hello **제거** 명령을 실행 하 고 hello 프롬프트에서 선택한 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="486eb-123">On hello ***groupname*** blade, select hello **Remove** command, and confirm your choice at hello prompt.</span></span>

   ![멤버 자격 제거 명령](./media/active-directory-groups-membership-azure-portal/remove-group-membership.png)
10. <span data-ttu-id="486eb-125">그룹에 대한 그룹 멤버 자격 변경을 마치면 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="486eb-125">When you finish changing group memberships for your group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="486eb-126">추가 정보</span><span class="sxs-lookup"><span data-stu-id="486eb-126">Additional information</span></span>
<span data-ttu-id="486eb-127">이러한 문서는 Azure Active Directory에 대한 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="486eb-127">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="486eb-128">기존 그룹 보기</span><span class="sxs-lookup"><span data-stu-id="486eb-128">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="486eb-129">새 그룹을 만들고 멤버 추가</span><span class="sxs-lookup"><span data-stu-id="486eb-129">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="486eb-130">그룹의 설정 관리</span><span class="sxs-lookup"><span data-stu-id="486eb-130">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="486eb-131">그룹의 멤버 관리</span><span class="sxs-lookup"><span data-stu-id="486eb-131">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="486eb-132">그룹의 사용자에 대한 동적 규칙 관리</span><span class="sxs-lookup"><span data-stu-id="486eb-132">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
