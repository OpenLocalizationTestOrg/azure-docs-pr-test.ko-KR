---
title: "Azure Active Directory에서 그룹의 멤버 관리 | Microsoft Docs"
description: "Azure Active Directory의 그룹에서 사용자 및 장치를 추가 또는 제거하는 방법"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d399a97d-fd2a-4b2d-b73d-0975db83f41b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 044e88f95712e1cc5b5532f5492c78d711a8d858
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-group-membership-for-users-in-your-azure-active-directory-tenant"></a><span data-ttu-id="c3475-103">Azure Active Directory 테넌트의 사용자에 대한 그룹 멤버 자격 관리</span><span class="sxs-lookup"><span data-stu-id="c3475-103">Manage group membership for users in your Azure Active Directory tenant</span></span>
<span data-ttu-id="c3475-104">이 문서는 Azure AD(Azure Active Directory)에서 그룹의 멤버를 관리하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c3475-104">This article explains how to manage the members for a group in Azure Active Directory (Azure AD).</span></span>

## <a name="how-do-i-find-the-members-and-manage-them"></a><span data-ttu-id="c3475-105">어떻게 멤버를 찾고 관리하나요?</span><span class="sxs-lookup"><span data-stu-id="c3475-105">How do I find the members and manage them?</span></span>
1. <span data-ttu-id="c3475-106">디렉터리에 대한 전역 관리자인 계정으로 [Azure 포털](https://portal.azure.com) 에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c3475-106">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="c3475-107">**더 많은 서비스**를 선택하고 텍스트 상자에 **사용자 및 그룹**을 입력한 다음 **Enter**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c3475-107">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![사용자 관리 열기](./media/active-directory-groups-members-azure-portal/search-user-management.png)
3. <span data-ttu-id="c3475-109">**사용자 및 그룹** 블레이드에서 **모든 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c3475-109">On the **Users and groups** blade, select **All groups**.</span></span>

   ![그룹 블레이드 열기](./media/active-directory-groups-members-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="c3475-111">**사용자 및 그룹 - 모든 그룹** 블레이드에서 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c3475-111">On the **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="c3475-112">**그룹 - *groupname*** 블레이드에서 **멤버**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c3475-112">On the **Group - *groupname*** blade, select **Members**.</span></span>

   ![멤버 블레이드 열기](./media/active-directory-groups-members-azure-portal/view-group-members.png)
6. <span data-ttu-id="c3475-114">그룹에 멤버를 추가하려면 **그룹 - 멤버** 블레이드에서 **멤버 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c3475-114">To add members to the group, on the **Group - Members** blade, select **Add Members**.</span></span>

   ![멤버 추가 명령](./media/active-directory-groups-members-azure-portal/add-group-members-command.png)
7. <span data-ttu-id="c3475-116">**멤버** 블레이드에서 그룹에 추가할 하나 이상의 사용자 또는 장치를 선택하고 블레이드 아래쪽의 **선택** 단추를 선택하여 그룹에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c3475-116">On the **Members** blade, select one or more users or devices to add to the group and select the **Select** button at the bottom of the blade to add them to the group.</span></span> <span data-ttu-id="c3475-117">**사용자** 상자는 사용자 또는 장치 이름 부분에 대한 항목 일치를 기반으로 한 표시를 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="c3475-117">The **User** box filters the display based on matching your entry to any part of a user or device name.</span></span> <span data-ttu-id="c3475-118">와일드카드 문자는 해당 상자에서 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3475-118">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="c3475-119">그룹에서 멤버를 제거하려면 **그룹 - 멤버** 블레이드에서 멤버를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c3475-119">To remove members from the group, on the **Group - Members** blade, select a member.</span></span>
9. <span data-ttu-id="c3475-120">***membername*** 블레이드에서 **제거** 명령을 선택하고 프롬프트에서 선택 내용을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c3475-120">On the ***membername*** blade, select the **Remove** command, and confirm your choice at the prompt.</span></span>

   ![멤버 제거 명령](./media/active-directory-groups-members-azure-portal/remove-group-members-command.png)
10. <span data-ttu-id="c3475-122">그룹의 멤버 변경을 마치면 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c3475-122">When you finish changing members for the group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="c3475-123">추가 정보</span><span class="sxs-lookup"><span data-stu-id="c3475-123">Additional information</span></span>
<span data-ttu-id="c3475-124">이러한 문서는 Azure Active Directory에 대한 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c3475-124">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="c3475-125">기존 그룹 보기</span><span class="sxs-lookup"><span data-stu-id="c3475-125">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="c3475-126">새 그룹을 만들고 멤버 추가</span><span class="sxs-lookup"><span data-stu-id="c3475-126">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="c3475-127">그룹의 설정 관리</span><span class="sxs-lookup"><span data-stu-id="c3475-127">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="c3475-128">그룹의 멤버 자격 관리</span><span class="sxs-lookup"><span data-stu-id="c3475-128">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="c3475-129">그룹의 사용자에 대한 동적 규칙 관리</span><span class="sxs-lookup"><span data-stu-id="c3475-129">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
