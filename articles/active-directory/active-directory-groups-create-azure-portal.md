---
title: "Azure Active Directory의 사용자에 대 한 그룹 aaaCreate | Microsoft Docs"
description: "어떻게 toocreate Azure Active Directory에서 그룹 구성원 toohello 그룹 추가"
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
ms.openlocfilehash: fc583a7f02ce50e7f3b2c8f97a9c032a3e2dc33a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-group-and-add-members-in-azure-active-directory"></a><span data-ttu-id="60b6c-103">Azure Active Directory에서 그룹 만들기 및 멤버 추가</span><span class="sxs-lookup"><span data-stu-id="60b6c-103">Create a group and add members in Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="60b6c-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="60b6c-104">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="60b6c-105">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="60b6c-105">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="60b6c-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="60b6c-106">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="60b6c-107">이 문서에서는 설명 어떻게 toocreate Azure Active Directory에 새 그룹을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="60b6c-107">This article explains how toocreate and populate a new group in Azure Active Directory.</span></span> <span data-ttu-id="60b6c-108">할당 하는 등 라이선스 또는 권한을 사용자 또는 장치 tooa 수가 한 번에 그룹 tooperform 관리 작업을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="60b6c-108">Use a group tooperform management tasks such as assigning licenses or permissions tooa number of users or devices at once.</span></span>

## <a name="how-do-i-create-a-group"></a><span data-ttu-id="60b6c-109">그룹을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="60b6c-109">How do I create a group?</span></span>
1. <span data-ttu-id="60b6c-110">Toohello 로그인 [Azure 포털](https://portal.azure.com) hello 디렉터리에 대 한 전역 관리자 인 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="60b6c-110">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="60b6c-111">선택 **더 많은 서비스**, 입력 **사용자 및 그룹** 에 hello 텍스트 상자를 선택한 후 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="60b6c-111">Select **More services**, enter **User and groups** in hello text box, and then select **Enter**.</span></span>

   ![사용자 관리 열기](./media/active-directory-groups-create-azure-portal/search-user-management.png)
3. <span data-ttu-id="60b6c-113">Hello에 **사용자 및 그룹** 블레이드를 **모든 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="60b6c-113">On hello **Users and groups** blade, select **All groups**.</span></span>

   ![Hello 그룹 블레이드 열기](./media/active-directory-groups-create-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="60b6c-115">Hello에 **사용자 및 그룹-모든 그룹** 블레이드, 선택 hello **추가** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="60b6c-115">On hello **Users and groups - All groups** blade, select hello **Add** command.</span></span>

   ![Hello 추가 명령을 선택 하면](./media/active-directory-groups-create-azure-portal/add-group-command.png)
5. <span data-ttu-id="60b6c-117">Hello에 **그룹** 블레이드에서 이름과 hello 그룹에 대 한 설명을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="60b6c-117">On hello **Group** blade, add a name and description for hello group.</span></span>
6. <span data-ttu-id="60b6c-118">tooselect 멤버 tooadd toohello 그룹에서 **Assigned** hello에 **멤버 자격 유형** 상자를 선택한 후 **멤버**합니다.</span><span class="sxs-lookup"><span data-stu-id="60b6c-118">tooselect members tooadd toohello group, select **Assigned** in hello **Membership type** box, and then select **Members**.</span></span> <span data-ttu-id="60b6c-119">어떻게 toomanage hello 그룹의 구성원이 동적으로 하는 방법에 대 한 자세한 내용은 참조 [toocreate 특성을 사용 하 여 고급 규칙 그룹 멤버 자격에 대 한](active-directory-groups-dynamic-membership-azure-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="60b6c-119">For more information about how toomanage hello membership of a group dynamically, see [Using attributes toocreate advanced rules for group membership](active-directory-groups-dynamic-membership-azure-portal.md).</span></span>

   ![멤버 tooadd 선택](./media/active-directory-groups-create-azure-portal/select-members.png)
7. <span data-ttu-id="60b6c-121">Hello에 **멤버** 블레이드, 하나를 선택 하거나 더 많은 사용자 또는 장치 tooadd toohello 그룹 및 선택 hello **선택** 단추 hello 블레이드 tooadd hello 맨 아래에 해당 toohello 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="60b6c-121">On hello **Members** blade, select one or more users or devices tooadd toohello group and select hello **Select** button at hello bottom of hello blade tooadd them toohello group.</span></span> <span data-ttu-id="60b6c-122">hello **사용자** 상자 필터 hello 일치 항목 tooany 부분은 사용자 또는 장치 이름 기준으로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="60b6c-122">hello **User** box filters hello display based on matching your entry tooany part of a user or device name.</span></span> <span data-ttu-id="60b6c-123">와일드카드 문자는 해당 상자에서 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="60b6c-123">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="60b6c-124">멤버 toohello 그룹 추가 마치면 선택 **만들기** hello에 **그룹** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="60b6c-124">When you finish adding members toohello group, select **Create** on hello **Group** blade.</span></span>    

   ![그룹 확인 만들기](./media/active-directory-groups-create-azure-portal/create-group-confirmation.png)


## <a name="next-steps"></a><span data-ttu-id="60b6c-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="60b6c-126">Next steps</span></span>
<span data-ttu-id="60b6c-127">이러한 문서는 Azure Active Directory에 대한 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="60b6c-127">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="60b6c-128">기존 그룹 보기</span><span class="sxs-lookup"><span data-stu-id="60b6c-128">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="60b6c-129">그룹의 설정 관리</span><span class="sxs-lookup"><span data-stu-id="60b6c-129">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="60b6c-130">그룹의 멤버 관리</span><span class="sxs-lookup"><span data-stu-id="60b6c-130">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="60b6c-131">그룹의 멤버 자격 관리</span><span class="sxs-lookup"><span data-stu-id="60b6c-131">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="60b6c-132">그룹의 사용자에 대한 동적 규칙 관리</span><span class="sxs-lookup"><span data-stu-id="60b6c-132">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
