---
title: "Azure Active Directory에서 엔터프라이즈 앱에 사용자 또는 그룹 할당 | Microsoft Docs"
description: "Azure Active Directory에서 사용자 또는 그룹을 할당할 엔터프라이즈 앱을 선택하는 방법"
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
ms.openlocfilehash: ee784704ada9238b5cd048f99aaa4cb192ec7d57
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="assign-a-user-or-group-to-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="a1b80-103">Azure Active Directory에서 엔터프라이즈 앱에 사용자 또는 그룹 할당</span><span class="sxs-lookup"><span data-stu-id="a1b80-103">Assign a user or group to an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="a1b80-104">Azure AD(Azure Active Directory)에서 엔터프라이즈 응용 프로그램에 사용자 또는 그룹을 할당하는 것은 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="a1b80-104">It's easy to assign a user or a group to your enterprise applications in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="a1b80-105">엔터프라이즈 앱을 관리하려면 적절한 권한이 있어야 하고 해당 디렉터리에 대한 전역 관리자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b80-105">You must have the appropriate permissions to manage the enterprise app, and you must be global admin for the directory.</span></span>

## <a name="how-do-i-assign-user-access-to-an-enterprise-app"></a><span data-ttu-id="a1b80-106">엔터프라이즈 앱에 사용자 액세스를 어떻게 할당하나요?</span><span class="sxs-lookup"><span data-stu-id="a1b80-106">How do I assign user access to an enterprise app?</span></span>
1. <span data-ttu-id="a1b80-107">디렉터리에 대한 전역 관리자인 계정으로 [Azure 포털](https://portal.azure.com) 에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b80-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="a1b80-108">**더 많은 서비스**를 선택하고 텍스트 상자에서 Azure Active Directory를 입력한 다음 **Enter**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b80-108">Select **More services**, enter Azure Active Directory in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="a1b80-109">**Azure Active Directory - *directoryname*** 블레이드(즉, 관리 중인 디렉터리에 대한 Azure AD 블레이드)에서 **엔터프라이즈 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b80-109">On the **Azure Active Directory - *directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![엔터프라이즈 앱 열기](./media/active-directory-coreapps-assign-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="a1b80-111">**엔터프라이즈 응용 프로그램** 블레이드에서 **모든 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b80-111">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="a1b80-112">관리할 수 있는 앱의 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1b80-112">You'll see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="a1b80-113">**엔터프라이즈 응용 프로그램 - 모든 응용 프로그램** 블레이드에서 앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b80-113">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="a1b80-114">***appname*** 블레이드(즉, 제목에서 선택된 앱의 이름을 가진 블레이드)에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b80-114">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Users & Groups**.</span></span>

    ![모든 응용 프로그램 명령 선택](./media/active-directory-coreapps-assign-user-azure-portal/select-app-users.png)
7. <span data-ttu-id="a1b80-116">***appname*** **- 사용자 및 그룹 할당** 블레이드에서 **추가** 명령을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b80-116">On the ***appname*** **- User & Group Assignment** blade, select the **Add** command.</span></span>
8. <span data-ttu-id="a1b80-117">**할당 추가** 블레이드에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b80-117">On the **Add Assignment** blade, select **Users and groups**.</span></span>

    ![앱에 사용자 또는 그룹 할당](./media/active-directory-coreapps-assign-user-azure-portal/assign-users.png)
9. <span data-ttu-id="a1b80-119">**사용자 및 그룹** 블레이드의 목록에서 하나 이상의 사용자 또는 그룹을 선택한 다음 블레이드 맨 아래의 **선택** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b80-119">On the **Users and groups** blade, select one or more users or groups from the list and then select the **Select** button at the bottom of the blade.</span></span>
10. <span data-ttu-id="a1b80-120">**할당 추가** 블레이드에서 **역할**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b80-120">On the **Add Assignment** blade, select **Role**.</span></span> <span data-ttu-id="a1b80-121">그런 다음 **역할 선택** 블레이드에서 선택한 사용자 또는 그룹에 적용할 역할을 선택한 다음 블레이드 맨 아래의 **확인** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b80-121">Then, on the **Select Role** blade, select a role to apply to the selected users or groups, and then select the **OK** button at the bottom of the blade.</span></span>
11. <span data-ttu-id="a1b80-122">**할당 추가** 블레이드에서 블레이드 맨 아래의 **할당** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a1b80-122">On the **Add Assignment** blade, select the **Assign** button at the bottom of the blade.</span></span> <span data-ttu-id="a1b80-123">할당된 사용자 또는 그룹은 이 엔터프라이즈 앱에 대한 선택된 역할로 정의된 사용 권한을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="a1b80-123">The assigned users or groups will have the permissions defined by the selected role for this enterprise app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1b80-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a1b80-124">Next steps</span></span>
* [<span data-ttu-id="a1b80-125">내 그룹 모두 보기</span><span class="sxs-lookup"><span data-stu-id="a1b80-125">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="a1b80-126">엔터프라이즈 앱에서 사용자 또는 그룹 할당 제거</span><span class="sxs-lookup"><span data-stu-id="a1b80-126">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="a1b80-127">엔터프라이즈 앱에 대한 사용자 로그인 비활성화</span><span class="sxs-lookup"><span data-stu-id="a1b80-127">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="a1b80-128">엔터프라이즈 앱의 이름 또는 로고 변경</span><span class="sxs-lookup"><span data-stu-id="a1b80-128">Change the name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
