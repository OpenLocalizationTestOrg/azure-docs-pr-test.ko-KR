---
title: "Azure Active Directory에서 사용자 또는 그룹 tooan 엔터프라이즈 앱 aaaAssign | Microsoft Docs"
description: "어떻게 엔터프라이즈 앱 tooassign Azure Active Directory에서 사용자 또는 그룹 tooit tooselect"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 5817ad48-d916-492b-a8d0-2ade8c50a224
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 86c11f19892b9c947a5331677c17759178ed2806
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-a-user-or-group-tooan-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="4d95d-103">Azure Active Directory에서 사용자 또는 그룹 tooan 엔터프라이즈 앱 할당</span><span class="sxs-lookup"><span data-stu-id="4d95d-103">Assign a user or group tooan enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="4d95d-104">인지 쉽게 tooassign 사용자는 Azure Active Directory (Azure AD)의 그룹 tooyour 엔터프라이즈 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="4d95d-104">It's easy tooassign a user or a group tooyour enterprise applications in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="4d95d-105">Hello 디렉터리에 대 한 전역 관리자 여야 하며 hello 적절 한 사용 권한을 toomanage hello 엔터프라이즈 앱 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d95d-105">You must have hello appropriate permissions toomanage hello enterprise app, and you must be global admin for hello directory.</span></span>

## <a name="how-do-i-assign-user-access-tooan-enterprise-app"></a><span data-ttu-id="4d95d-106">사용자 액세스 tooan 엔터프라이즈 응용 프로그램을 할당 하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="4d95d-106">How do I assign user access tooan enterprise app?</span></span>
1. <span data-ttu-id="4d95d-107">Toohello 로그인 [Azure 포털](https://portal.azure.com) hello 디렉터리에 대 한 전역 관리자 인 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d95d-107">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="4d95d-108">선택 **더 많은 서비스**hello 텍스트 상자에 Azure Active Directory를 입력 한 다음 선택, **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="4d95d-108">Select **More services**, enter Azure Active Directory in hello text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="4d95d-109">Hello에 **Azure Active Directory- *디렉터리 이름***  블레이드 (관리 하는 hello 디렉터리에 대 한 즉, Azure AD hello 블레이드) 선택 **엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="4d95d-109">On hello **Azure Active Directory - *directoryname*** blade (that is, hello Azure AD blade for hello directory you are managing), select **Enterprise applications**.</span></span>

    ![엔터프라이즈 앱 열기](./media/active-directory-coreapps-assign-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="4d95d-111">Hello에 **엔터프라이즈 응용 프로그램** 블레이드를 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="4d95d-111">On hello **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="4d95d-112">관리할 수는 hello 앱 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d95d-112">You'll see a list of hello apps you can manage.</span></span>
5. <span data-ttu-id="4d95d-113">Hello에 **엔터프라이즈 응용 프로그램-모든 응용 프로그램** 블레이드에서 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d95d-113">On hello **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="4d95d-114">Hello에 ***appname*** 블레이드 (hello hello 제목에 선택 된 응용 프로그램의 hello 이름으로, 즉 hello 블레이드) 선택 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="4d95d-114">On hello ***appname*** blade (that is, hello blade with hello name of hello selected app in hello title), select **Users & Groups**.</span></span>

    ![모든 응용 프로그램 명령 hello 선택](./media/active-directory-coreapps-assign-user-azure-portal/select-app-users.png)
7. <span data-ttu-id="4d95d-116">Hello에 ***appname*** **-사용자 및 그룹 할당** 블레이드, 선택 hello **추가** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="4d95d-116">On hello ***appname*** **- User & Group Assignment** blade, select hello **Add** command.</span></span>
8. <span data-ttu-id="4d95d-117">Hello에 **할당 추가** 블레이드를 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="4d95d-117">On hello **Add Assignment** blade, select **Users and groups**.</span></span>

    ![사용자 또는 그룹 toohello 응용 프로그램 할당](./media/active-directory-coreapps-assign-user-azure-portal/assign-users.png)
9. <span data-ttu-id="4d95d-119">Hello에 **사용자 및 그룹** 블레이드, 선택 하나 이상의 사용자 또는 그룹 hello에서 나열 하 고 다음 hello 선택 **선택** hello hello 블레이드 맨 아래에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="4d95d-119">On hello **Users and groups** blade, select one or more users or groups from hello list and then select hello **Select** button at hello bottom of hello blade.</span></span>
10. <span data-ttu-id="4d95d-120">Hello에 **할당 추가** 블레이드를 **역할**합니다.</span><span class="sxs-lookup"><span data-stu-id="4d95d-120">On hello **Add Assignment** blade, select **Role**.</span></span> <span data-ttu-id="4d95d-121">그런 다음 hello **역할 선택** 블레이드에서 선택한 역할 tooapply toohello 사용자 또는 그룹을 선택한 다음 선택 hello **확인** hello hello 블레이드 맨 아래에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="4d95d-121">Then, on hello **Select Role** blade, select a role tooapply toohello selected users or groups, and then select hello **OK** button at hello bottom of hello blade.</span></span>
11. <span data-ttu-id="4d95d-122">Hello에 **할당 추가** 블레이드, 선택 hello **할당** hello hello 블레이드 맨 아래에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="4d95d-122">On hello **Add Assignment** blade, select hello **Assign** button at hello bottom of hello blade.</span></span> <span data-ttu-id="4d95d-123">hello 할당 사용자 또는 그룹에는이 엔터프라이즈 응용 프로그램에 대 한 hello 선택한 역할에 의해 정의 하는 hello 사용 권한을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="4d95d-123">hello assigned users or groups will have hello permissions defined by hello selected role for this enterprise app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d95d-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4d95d-124">Next steps</span></span>
* [<span data-ttu-id="4d95d-125">내 그룹 모두 보기</span><span class="sxs-lookup"><span data-stu-id="4d95d-125">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="4d95d-126">엔터프라이즈 앱에서 사용자 또는 그룹 할당 제거</span><span class="sxs-lookup"><span data-stu-id="4d95d-126">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="4d95d-127">엔터프라이즈 앱에 대한 사용자 로그인 비활성화</span><span class="sxs-lookup"><span data-stu-id="4d95d-127">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="4d95d-128">Hello 이름 변경 또는 엔터프라이즈 응용 프로그램에서의 로고</span><span class="sxs-lookup"><span data-stu-id="4d95d-128">Change hello name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
