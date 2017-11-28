---
title: "aaaHow toostart 액세스 검토 | Microsoft Docs"
description: "어떻게 toocreate 대 한 액세스를 검토 하 여 hello Azure Privileged Identity Management 응용 프로그램으로 권한 있는 id에 알아봅니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 3e52b731-55f4-4c8a-ba87-9fd34033f52f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 24feac307f77c69b5d68d6ae0623dbcb52416b01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toostart-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="23337-103">어떻게 toostart 액세스에서에서 검토 하 고 Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="23337-103">How toostart an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="23337-104">사용자가 더 이상 필요 없는 권한 있는 액세스를 가진 경우 "오래된" 역할 할당이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="23337-104">Role assignments become "stale" when users have privileged access that they don't need anymore.</span></span> <span data-ttu-id="23337-105">순서 tooreduce hello는 관련 된 오래 된 역할은 위험, 권한 있는 역할 관리자가 사용자 지정 된 hello 역할을 정기적으로 검토 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="23337-105">In order tooreduce hello risk associated with these stale role assignments, privileged role administrators should regularly review hello roles that users have been given.</span></span> <span data-ttu-id="23337-106">이 문서에서는 Azure AD Privileged Identity Management (PIM)에서 액세스 검토를 시작 하기 위한 hello 단계를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="23337-106">This document covers hello steps for starting an access review in Azure AD Privileged Identity Management (PIM).</span></span>

## <a name="start-an-access-review"></a><span data-ttu-id="23337-107">액세스 검토 시작</span><span class="sxs-lookup"><span data-stu-id="23337-107">Start an access review</span></span>
> [!NOTE]
> <span data-ttu-id="23337-108">Hello Azure 포털에서에서 hello PIM 응용 프로그램 tooyour 대시보드를 추가 하지 않았다면, 참조의 hello 단계 [Azure Privileged Identity Management 시작 하기](active-directory-privileged-identity-management-getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="23337-108">If you haven't added hello PIM application tooyour dashboard in hello Azure portal, see hello steps in  [Getting Started with Azure Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)</span></span>
> 
> 

<span data-ttu-id="23337-109">Hello PIM 응용 프로그램 기본 페이지에서 세 가지 방법으로 toostart 액세스 검토</span><span class="sxs-lookup"><span data-stu-id="23337-109">From hello PIM application main page, there are three ways toostart an access review:</span></span>

* <span data-ttu-id="23337-110">**액세스 검토** > **추가**</span><span class="sxs-lookup"><span data-stu-id="23337-110">**Access reviews** > **Add**</span></span>
* <span data-ttu-id="23337-111">**역할** > **검토** 단추</span><span class="sxs-lookup"><span data-stu-id="23337-111">**Roles** > **Review** button</span></span>
* <span data-ttu-id="23337-112">Hello 역할 목록에서 선택 hello 특정 역할 toobe 검토 > **검토** 단추</span><span class="sxs-lookup"><span data-stu-id="23337-112">Select hello specific role toobe reviewed from hello roles list > **Review** button</span></span>

<span data-ttu-id="23337-113">Hello에 클릭할 때 **검토** 단추 hello **액세스 검토를 시작** 블레이드 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="23337-113">When you click on hello **Review** button, hello **Start an access review** blade appears.</span></span> <span data-ttu-id="23337-114">이 블레이드를 이름으로 하락 tooconfigure hello 검토 하는 및 제한 시간, 역할 tooreview 선택한는 hello 검토를 수행할지 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="23337-114">On this blade, you're going tooconfigure hello review with a name and time limit, choose a role tooreview, and decide who will perform hello review.</span></span>

![액세스 검토 시작 - 스크린 샷][1]

### <a name="configure-hello-review"></a><span data-ttu-id="23337-116">Hello 검토를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="23337-116">Configure hello review</span></span>
<span data-ttu-id="23337-117">toocreate 대 한 액세스를 검토 하 고 시작 및 종료 날짜 집합 tooname를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="23337-117">toocreate an access review, you need tooname it and set a start and end date.</span></span>

![검토 구성 - 스크린 샷][2]

<span data-ttu-id="23337-119">충분 한 시간 동안 사용자가 toocomplete 검토 hello의 hello 길이 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="23337-119">Make hello length of hello review long enough for users toocomplete it.</span></span> <span data-ttu-id="23337-120">Hello 종료 날짜 이전에 완료 일찍 hello 검토를 중지할 항상 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23337-120">If you finish before hello end date, you can always stop hello review early.</span></span>

### <a name="choose-a-role-tooreview"></a><span data-ttu-id="23337-121">역할 tooreview 선택</span><span class="sxs-lookup"><span data-stu-id="23337-121">Choose a role tooreview</span></span>
<span data-ttu-id="23337-122">각 검토는 오직 하나의 역할에 집중합니다.</span><span class="sxs-lookup"><span data-stu-id="23337-122">Each review focuses on only one role.</span></span> <span data-ttu-id="23337-123">특정 역할 블레이드에서 hello 액세스 검토를 시작 하지 않은 이제 toochoose 역할 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="23337-123">Unless you started hello access review from a specific role blade, you'll need toochoose a role now.</span></span>

1. <span data-ttu-id="23337-124">너무 이동**역할 구성원 자격 검토**</span><span class="sxs-lookup"><span data-stu-id="23337-124">Navigate too**Review role membership**</span></span>
   
    ![역할 멤버 자격 검토 - 스크린샷][3]
2. <span data-ttu-id="23337-126">Hello 목록에서 역할 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="23337-126">Choose one role from hello list.</span></span>

### <a name="decide-who-will-perform-hello-review"></a><span data-ttu-id="23337-127">hello 검토를 수행할지 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="23337-127">Decide who will perform hello review</span></span>
<span data-ttu-id="23337-128">검토를 수행하는 데 세 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23337-128">There are three options for performing a review.</span></span> <span data-ttu-id="23337-129">Hello 검토 toosomeone를 할당할 수 있습니다 다른 toocomplete 할 수 있는 것을 직접 또는 각 사용자가 자신의 액세스 검토 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23337-129">You can assign hello review toosomeone else toocomplete, you can do it yourself, or you can have each user review their own access.</span></span>

1. <span data-ttu-id="23337-130">너무 이동**검토자를 선택 합니다.**</span><span class="sxs-lookup"><span data-stu-id="23337-130">Navigate too**Select reviewers**</span></span>
   
    ![검토자 선택 - 스크린 샷][4]
2. <span data-ttu-id="23337-132">Hello 옵션 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="23337-132">Choose one of hello options:</span></span>
   
   * <span data-ttu-id="23337-133">**검토자 선택**: 액세스가 필요한 사용자를 알 수 없는 경우 이 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="23337-133">**Select reviewer**: Use this option when you don't know who needs access.</span></span> <span data-ttu-id="23337-134">이 옵션을 hello 검토 tooa 리소스 소유자 또는 관리자 toocomplete 그룹을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23337-134">With this option, you can assign hello review tooa resource owner or group manager toocomplete.</span></span>
   * <span data-ttu-id="23337-135">**Me**: 방법을 toopreview 사용 하려는 경우 유용 tooreview 수 없는 사용자를 대신 하 여 원하는 또는 access 작업을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="23337-135">**Me**: Useful if you want toopreview how access reviews work, or you want tooreview on behalf of people who can't.</span></span>
   * <span data-ttu-id="23337-136">**멤버 자체 검토**:이 옵션 toohave hello 사용자가 검토 자신의 역할 할당을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="23337-136">**Members review themselves**: Use this option toohave hello users review their own role assignments.</span></span>

### <a name="start-hello-review"></a><span data-ttu-id="23337-137">Hello 검토를 시작</span><span class="sxs-lookup"><span data-stu-id="23337-137">Start hello review</span></span>
<span data-ttu-id="23337-138">마지막으로 hello 옵션 toorequire 액세스를 승인 하는 경우 사용자가 이유를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="23337-138">Finally, you have hello option toorequire that users provide a reason if they approve their access.</span></span> <span data-ttu-id="23337-139">원하는 경우 hello 검토에 대 한 설명을 추가 하 고 선택 **시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="23337-139">Add a description of hello review if you like, and select **Start**.</span></span>

<span data-ttu-id="23337-140">고객을 위해 대기 하는 액세스 검토가 있다는 것을 표시 합니다. 따라서 사용자가 있는지 확인 [어떻게 tooperform 액세스 검토](active-directory-privileged-identity-management-how-to-perform-security-review.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="23337-140">Make sure you let your users know that there's an access review waiting for them, and show them [How tooperform an access review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

## <a name="manage-hello-access-review"></a><span data-ttu-id="23337-141">Hello 액세스 검토를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="23337-141">Manage hello access review</span></span>
<span data-ttu-id="23337-142">Hello 검토자가 검토 hello Azure AD PIM 대시보드에서에서 완료 된 것으로 hello 진행률을 추적할 수, access hello에서 섹션을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="23337-142">You can track hello progress as hello reviewers complete their reviews in hello Azure AD PIM dashboard, in hello access reviews section.</span></span> <span data-ttu-id="23337-143">액세스 권한이 없습니다.까지 hello 디렉터리에 변경 됩니다 [hello 검토 완료](active-directory-privileged-identity-management-how-to-complete-review.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="23337-143">No access rights will be changed in hello directory until [hello review completes](active-directory-privileged-identity-management-how-to-complete-review.md).</span></span>

<span data-ttu-id="23337-144">Hello 검토 기간이 끝나면 될 때까지 해당 검토 사용자 toocomplete를 알려줍니다 또는 중지 hello 검토 초기 hello 액세스 로부터 검토 섹션.</span><span class="sxs-lookup"><span data-stu-id="23337-144">Until hello review period is over, you can remind users toocomplete their review, or stop hello review early from hello access reviews section.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="pim-table-of-contents"></a><span data-ttu-id="23337-145">PIM 목차</span><span class="sxs-lookup"><span data-stu-id="23337-145">PIM Table of Contents</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_start_review.png
[2]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_configure.png
[3]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_role.png
[4]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_reviewers.png
