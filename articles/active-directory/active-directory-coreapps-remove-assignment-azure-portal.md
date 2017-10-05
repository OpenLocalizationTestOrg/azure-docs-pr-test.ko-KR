---
title: "Azure Active Directory에서 엔터프라이즈 앱의 사용자 또는 그룹 할당 제거 | Microsoft Docs"
description: "Azure Active Directory에서 엔터프라이즈 앱의 사용자 또는 그룹의 액세스 할당을 제거하는 방법"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7b2d365b-ae92-477f-9702-353cc6acc5ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 02f122acfb53c2107e2b0af66c6195aa127a2c77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="remove-a-user-or-group-assignment-from-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="7ef3b-103">Azure Active Directory에서 엔터프라이즈 앱의 사용자 또는 그룹 할당 제거</span><span class="sxs-lookup"><span data-stu-id="7ef3b-103">Remove a user or group assignment from an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="7ef3b-104">Azure AD(Azure Active Directory)에서 엔터프라이즈 응용 프로그램 중 하나에 대해 할당된 액세스의 사용자 또는 그룹을 제거하는 것은 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="7ef3b-104">It's easy to remove a user or a group from being assigned access to one of your enterprise applications in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="7ef3b-105">엔터프라이즈 앱을 관리하려면 적절한 권한이 있어야 하고 해당 디렉터리에 대한 전역 관리자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef3b-105">You must have the appropriate permissions to manage the enterprise app, and you must be global admin for the directory.</span></span>

## <a name="how-do-i-remove-a-user-or-group-assignment"></a><span data-ttu-id="7ef3b-106">사용자 또는 그룹 할당을 제거하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="7ef3b-106">How do I remove a user or group assignment?</span></span>
1. <span data-ttu-id="7ef3b-107">디렉터리에 대한 전역 관리자인 계정으로 [Azure 포털](https://portal.azure.com) 에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef3b-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="7ef3b-108">**더 많은 서비스**를 선택하고 텍스트 상자에서 **Azure Active Directory**를 입력한 다음 **Enter**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef3b-108">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="7ef3b-109">**Azure Active Directory - *directoryname*** 블레이드(즉, 관리 중인 디렉터리에 대한 Azure AD 블레이드)에서 **엔터프라이즈 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef3b-109">On the **Azure Active Directory - *directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![엔터프라이즈 앱 열기](./media/active-directory-coreapps-remove-assignment-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="7ef3b-111">**엔터프라이즈 응용 프로그램** 블레이드에서 **모든 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef3b-111">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="7ef3b-112">관리할 수 있는 앱의 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ef3b-112">You'll see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="7ef3b-113">**엔터프라이즈 응용 프로그램 - 모든 응용 프로그램** 블레이드에서 앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef3b-113">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="7ef3b-114">***appname*** 블레이드(즉, 제목에서 선택된 앱의 이름을 가진 블레이드)에서 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef3b-114">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Users & Groups**.</span></span>

    ![사용자 또는 그룹 선택](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-app-users.png)
7. <span data-ttu-id="7ef3b-116">***appname*** **- 사용자 및 그룹 할당** 블레이드에서 하나 이상의 사용자 또는 그룹을 선택한 다음 **제거** 명령을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef3b-116">On the ***appname*** **- User & Group Assignment** blade, select one of more users or groups and then select the **Remove** command.</span></span> <span data-ttu-id="7ef3b-117">프롬프트에서 의사 결정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7ef3b-117">Confirm your decision at the prompt.</span></span>

    ![제거 명령 선택](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-users.png)

## <a name="next-steps"></a><span data-ttu-id="7ef3b-119">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7ef3b-119">Next steps</span></span>
* [<span data-ttu-id="7ef3b-120">내 그룹 모두 보기</span><span class="sxs-lookup"><span data-stu-id="7ef3b-120">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="7ef3b-121">엔터프라이즈 앱에 사용자 또는 그룹 할당</span><span class="sxs-lookup"><span data-stu-id="7ef3b-121">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="7ef3b-122">엔터프라이즈 앱에 대한 사용자 로그인 비활성화</span><span class="sxs-lookup"><span data-stu-id="7ef3b-122">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="7ef3b-123">엔터프라이즈 앱의 이름 또는 로고 변경</span><span class="sxs-lookup"><span data-stu-id="7ef3b-123">Change the name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
