---
title: "Azure Active Directory에서 사용자에 대한 그룹 만들기 | Microsoft Docs"
description: "Azure Active Directory에서 그룹을 만들고 그룹에 멤버를 추가하는 방법"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6d3d37761a9fdf9bd9801396d45f2fcd47efb0be
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-group-and-add-members-in-azure-active-directory"></a><span data-ttu-id="e68bb-103">Azure Active Directory에서 그룹 만들기 및 멤버 추가</span><span class="sxs-lookup"><span data-stu-id="e68bb-103">Create a group and add members in Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e68bb-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e68bb-104">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="e68bb-105">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="e68bb-105">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="e68bb-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e68bb-106">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="e68bb-107">이 문서는 Azure Active Directory에서 새 그룹을 만들고 채우는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e68bb-107">This article explains how to create and populate a new group in Azure Active Directory.</span></span> <span data-ttu-id="e68bb-108">그룹을 사용하여 한 번에 많은 사용자 또는 장치에 라이선스 또는 사용 권한을 할당하는 등 관리 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e68bb-108">Use a group to perform management tasks such as assigning licenses or permissions to a number of users or devices at once.</span></span>

## <a name="how-do-i-create-a-group"></a><span data-ttu-id="e68bb-109">그룹을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="e68bb-109">How do I create a group?</span></span>
1. <span data-ttu-id="e68bb-110">디렉터리에 대한 전역 관리자인 계정으로 [Azure 포털](https://portal.azure.com) 에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e68bb-110">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="e68bb-111">**더 많은 서비스**를 선택하고 텍스트 상자에 **사용자 및 그룹**을 입력한 다음 **Enter**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e68bb-111">Select **More services**, enter **User and groups** in the text box, and then select **Enter**.</span></span>

   ![사용자 관리 열기](./media/active-directory-groups-create-azure-portal/search-user-management.png)
3. <span data-ttu-id="e68bb-113">**사용자 및 그룹** 블레이드에서 **모든 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e68bb-113">On the **Users and groups** blade, select **All groups**.</span></span>

   ![그룹 블레이드 열기](./media/active-directory-groups-create-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="e68bb-115">**사용자 및 그룹 - 모든 그룹** 블레이드에서 **추가** 명령을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e68bb-115">On the **Users and groups - All groups** blade, select the **Add** command.</span></span>

   ![추가 명령 선택](./media/active-directory-groups-create-azure-portal/add-group-command.png)
5. <span data-ttu-id="e68bb-117">**그룹** 블레이드에서 그룹에 대한 이름 및 설명을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e68bb-117">On the **Group** blade, add a name and description for the group.</span></span>
6. <span data-ttu-id="e68bb-118">그룹에 추가할 멤버를 선택하려면 **멤버 자격 유형** 상자에서 **할당**을 선택한 다음 **멤버**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e68bb-118">To select members to add to the group, select **Assigned** in the **Membership type** box, and then select **Members**.</span></span> <span data-ttu-id="e68bb-119">그룹의 구성원을 동적으로 관리하는 방법에 대한 자세한 내용은 [특성을 사용하여 그룹 멤버 자격에 대한 고급 규칙 만들기](active-directory-groups-dynamic-membership-azure-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e68bb-119">For more information about how to manage the membership of a group dynamically, see [Using attributes to create advanced rules for group membership](active-directory-groups-dynamic-membership-azure-portal.md).</span></span>

   ![추가할 멤버 선택](./media/active-directory-groups-create-azure-portal/select-members.png)
7. <span data-ttu-id="e68bb-121">**멤버** 블레이드에서 그룹에 추가할 하나 이상의 사용자 또는 장치를 선택하고 블레이드 아래쪽의 **선택** 단추를 선택하여 그룹에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e68bb-121">On the **Members** blade, select one or more users or devices to add to the group and select the **Select** button at the bottom of the blade to add them to the group.</span></span> <span data-ttu-id="e68bb-122">**사용자** 상자는 사용자 또는 장치 이름 부분에 대한 항목 일치를 기반으로 한 표시를 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="e68bb-122">The **User** box filters the display based on matching your entry to any part of a user or device name.</span></span> <span data-ttu-id="e68bb-123">와일드카드 문자는 해당 상자에서 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e68bb-123">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="e68bb-124">그룹에 멤버 추가를 마치면 **그룹** 블레이드에서 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e68bb-124">When you finish adding members to the group, select **Create** on the **Group** blade.</span></span>    

   ![그룹 확인 만들기](./media/active-directory-groups-create-azure-portal/create-group-confirmation.png)


## <a name="next-steps"></a><span data-ttu-id="e68bb-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e68bb-126">Next steps</span></span>
<span data-ttu-id="e68bb-127">이러한 문서는 Azure Active Directory에 대한 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e68bb-127">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="e68bb-128">기존 그룹 보기</span><span class="sxs-lookup"><span data-stu-id="e68bb-128">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="e68bb-129">그룹의 설정 관리</span><span class="sxs-lookup"><span data-stu-id="e68bb-129">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="e68bb-130">그룹의 멤버 관리</span><span class="sxs-lookup"><span data-stu-id="e68bb-130">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="e68bb-131">그룹의 멤버 자격 관리</span><span class="sxs-lookup"><span data-stu-id="e68bb-131">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="e68bb-132">그룹의 사용자에 대한 동적 규칙 관리</span><span class="sxs-lookup"><span data-stu-id="e68bb-132">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
