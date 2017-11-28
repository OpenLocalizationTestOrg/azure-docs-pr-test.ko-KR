---
title: "Azure Active Directory에서 엔터프라이즈 응용 프로그램에서 사용자 또는 그룹 할당 aaaRemove | Microsoft Docs"
description: "Tooremove hello Azure Active Directory에서 엔터프라이즈 응용 프로그램에서 사용자 또는 그룹의 할당에 액세스 하는 방법"
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
ms.openlocfilehash: c067ecf59b4dedfe8f848357ca8bd545bdc610eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="remove-a-user-or-group-assignment-from-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="4d2e3-103">Azure Active Directory에서 엔터프라이즈 앱의 사용자 또는 그룹 할당 제거</span><span class="sxs-lookup"><span data-stu-id="4d2e3-103">Remove a user or group assignment from an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="4d2e3-104">쉽게 tooremove 사용자 또는 그룹 액세스 tooone Azure Active Directory (Azure AD)에 엔터프라이즈 응용 프로그램의 할당 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4d2e3-104">It's easy tooremove a user or a group from being assigned access tooone of your enterprise applications in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="4d2e3-105">Hello 디렉터리에 대 한 전역 관리자 여야 하며 hello 적절 한 사용 권한을 toomanage hello 엔터프라이즈 앱 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d2e3-105">You must have hello appropriate permissions toomanage hello enterprise app, and you must be global admin for hello directory.</span></span>

## <a name="how-do-i-remove-a-user-or-group-assignment"></a><span data-ttu-id="4d2e3-106">사용자 또는 그룹 할당을 제거하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="4d2e3-106">How do I remove a user or group assignment?</span></span>
1. <span data-ttu-id="4d2e3-107">Toohello 로그인 [Azure 포털](https://portal.azure.com) hello 디렉터리에 대 한 전역 관리자 인 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d2e3-107">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="4d2e3-108">선택 **더 많은 서비스**, 입력 **Azure Active Directory** 에 hello 텍스트 상자를 선택한 후 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="4d2e3-108">Select **More services**, enter **Azure Active Directory** in hello text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="4d2e3-109">Hello에 **Azure Active Directory- *디렉터리 이름***  블레이드 (관리 하는 hello 디렉터리에 대 한 즉, Azure AD hello 블레이드) 선택 **엔터프라이즈 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="4d2e3-109">On hello **Azure Active Directory - *directoryname*** blade (that is, hello Azure AD blade for hello directory you are managing), select **Enterprise applications**.</span></span>

    ![엔터프라이즈 앱 열기](./media/active-directory-coreapps-remove-assignment-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="4d2e3-111">Hello에 **엔터프라이즈 응용 프로그램** 블레이드를 **모든 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="4d2e3-111">On hello **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="4d2e3-112">관리할 수는 hello 앱 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d2e3-112">You'll see a list of hello apps you can manage.</span></span>
5. <span data-ttu-id="4d2e3-113">Hello에 **엔터프라이즈 응용 프로그램-모든 응용 프로그램** 블레이드에서 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d2e3-113">On hello **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="4d2e3-114">Hello에 ***appname*** 블레이드 (hello hello 제목에 선택 된 응용 프로그램의 hello 이름으로, 즉 hello 블레이드) 선택 **사용자 및 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="4d2e3-114">On hello ***appname*** blade (that is, hello blade with hello name of hello selected app in hello title), select **Users & Groups**.</span></span>

    ![사용자 또는 그룹 선택](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-app-users.png)
7. <span data-ttu-id="4d2e3-116">Hello에 ***appname*** **-사용자 및 그룹 할당** 블레이드에서 이상의 사용자 또는 그룹 중 하나를 선택 하 고 다음 hello를 선택 **제거** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="4d2e3-116">On hello ***appname*** **- User & Group Assignment** blade, select one of more users or groups and then select hello **Remove** command.</span></span> <span data-ttu-id="4d2e3-117">Hello 프롬프트에 대 한 의사 결정을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d2e3-117">Confirm your decision at hello prompt.</span></span>

    ![Hello 제거 명령을 선택 하면](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-users.png)

## <a name="next-steps"></a><span data-ttu-id="4d2e3-119">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4d2e3-119">Next steps</span></span>
* [<span data-ttu-id="4d2e3-120">내 그룹 모두 보기</span><span class="sxs-lookup"><span data-stu-id="4d2e3-120">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="4d2e3-121">사용자 또는 그룹 tooan 엔터프라이즈 응용 프로그램 할당</span><span class="sxs-lookup"><span data-stu-id="4d2e3-121">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="4d2e3-122">엔터프라이즈 앱에 대한 사용자 로그인 비활성화</span><span class="sxs-lookup"><span data-stu-id="4d2e3-122">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="4d2e3-123">Hello 이름 변경 또는 엔터프라이즈 응용 프로그램에서의 로고</span><span class="sxs-lookup"><span data-stu-id="4d2e3-123">Change hello name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
