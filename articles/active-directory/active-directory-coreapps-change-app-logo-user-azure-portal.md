---
title: "Azure Active Directory에서 엔터프라이즈 앱의 이름 또는 로고 변경 | Microsoft Docs"
description: "Azure Active Directory에서 사용자 지정 엔터프라이즈 앱에 대한 이름 또는 로고를 변경하는 방법"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d01303ce-e6cb-4f3b-a4d6-ec29dfd68146
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 3e44e876dcbac704a9809ae5b3957bf94be21c48
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-name-or-logo-of-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="3d8f5-103">Azure Active Directory에서 엔터프라이즈 앱의 이름 또는 로고 변경</span><span class="sxs-lookup"><span data-stu-id="3d8f5-103">Change the name or logo of an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="3d8f5-104">Azure AD(Azure Active Directory)에서 사용자 정의 엔터프라이즈 응용 프로그램에 대한 이름 또는 로고를 변경하는 것은 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="3d8f5-104">It's easy to change the name or logo for a custom enterprise application in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="3d8f5-105">이러한 변경을 수행하려면 적절한 권한이 있고 사용자 지정 앱에 대한 작성자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d8f5-105">You must have the appropriate permissions to make these changes, and you must be the creator of the custom app.</span></span>

## <a name="how-do-i-change-an-enterprise-apps-name-or-logo"></a><span data-ttu-id="3d8f5-106">엔터프라이즈 앱의 이름 또는 로고를 변경하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="3d8f5-106">How do I change an enterprise app's name or logo?</span></span>
1. <span data-ttu-id="3d8f5-107">디렉터리에 대한 전역 관리자인 계정으로 [Azure 포털](https://portal.azure.com) 에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="3d8f5-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="3d8f5-108">**더 많은 서비스**를 선택하고 텍스트 상자에서 **Azure Active Directory**를 입력한 다음 **Enter**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3d8f5-108">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="3d8f5-109">**Azure Active Directory - *directoryname*** 블레이드(즉, 관리 중인 디렉터리에 대한 Azure AD 블레이드)에서 **엔터프라이즈 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3d8f5-109">On the **Azure Active Directory - *directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![엔터프라이즈 앱 열기](./media/active-directory-coreapps-change-app-logo-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="3d8f5-111">**엔터프라이즈 응용 프로그램** 블레이드에서 **모든 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3d8f5-111">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="3d8f5-112">관리할 수 있는 앱의 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d8f5-112">You'll see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="3d8f5-113">**엔터프라이즈 응용 프로그램 - 모든 응용 프로그램** 블레이드에서 앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3d8f5-113">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="3d8f5-114">***appname*** 블레이드, 즉 제목에서 선택된 앱의 이름을 사용한 블레이드에서 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3d8f5-114">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Properties**.</span></span>

    ![속성 명령 선택](./media/active-directory-coreapps-change-app-logo-azure-portal/select-app.png)
7. <span data-ttu-id="3d8f5-116">***appname*** **- 속성** 블레이드에서 새 로고로 사용하거나 앱 이름 또는 둘 다를 편집할 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="3d8f5-116">On the ***appname*** **- Properties** blade, browse for a file to use as a new logo, or edit the app name, or both.</span></span>

    ![앱 로고 또는 nameproperties 명령 변경](./media/active-directory-coreapps-change-app-logo-azure-portal/change-logo.png)
8. <span data-ttu-id="3d8f5-118">**저장** 명령을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3d8f5-118">Select the **Save** command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d8f5-119">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3d8f5-119">Next steps</span></span>
* [<span data-ttu-id="3d8f5-120">내 그룹 모두 보기</span><span class="sxs-lookup"><span data-stu-id="3d8f5-120">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="3d8f5-121">엔터프라이즈 앱에 사용자 또는 그룹 할당</span><span class="sxs-lookup"><span data-stu-id="3d8f5-121">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="3d8f5-122">엔터프라이즈 앱에서 사용자 또는 그룹 할당 제거</span><span class="sxs-lookup"><span data-stu-id="3d8f5-122">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="3d8f5-123">엔터프라이즈 앱에 대한 사용자 로그인 비활성화</span><span class="sxs-lookup"><span data-stu-id="3d8f5-123">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
