---
title: "응용 프로그램에 대한 사용자 액세스를 제거하는 방법 | Microsoft Docs"
description: "응용 프로그램에 대한 사용자 액세스를 제거하는 방법 이해"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 497429e7bf62f7e1d67ea429d6b858725f843688
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-remove-a-users-access-to-an-application"></a><span data-ttu-id="bf25e-103">응용 프로그램에 대한 사용자 액세스를 제거하는 방법</span><span class="sxs-lookup"><span data-stu-id="bf25e-103">How to remove a user's access to an application</span></span>

<span data-ttu-id="bf25e-104">이 문서는 응용 프로그램에 대한 사용자 액세스를 제거하는 방법을 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf25e-104">This article help you to understand how to remove a user's access to an application.</span></span>

## <a name="i-want-to-remove-a-specific-users-or-groups-assignment-to-an-application"></a><span data-ttu-id="bf25e-105">응용 프로그램에 대한 특정 사용자 또는 그룹의 할당을 제거하려는 경우</span><span class="sxs-lookup"><span data-stu-id="bf25e-105">I want to remove a specific user’s or group’s assignment to an application</span></span>

<span data-ttu-id="bf25e-106">응용 프로그램에 대한 사용자 또는 그룹 할당을 제거하려면 [Azure Active Directory의 엔터프라이즈 앱에서 사용자 또는 그룹 할당 제거](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) 문서에 나열된 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="bf25e-106">To remove a user or group assignment to an application, follow the steps listed in the [Remove a user or group assignment from an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) article.</span></span>

<span data-ttu-id="bf25e-107">모든 사용자에 대해 응용 프로그램에 대한 모든 액세스를 비활성화하려는 경우</span><span class="sxs-lookup"><span data-stu-id="bf25e-107">.## I want to disable all access to an application for every user</span></span>

<span data-ttu-id="bf25e-108">응용 프로그램에 대한 모든 사용자 로그인을 비활성화하려면 [Azure Active Directory의 엔터프라이즈 앱에 대한 사용자 로그인 비활성화](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) 문서에 나열된 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="bf25e-108">To disable all user sign-ins to an application, follow the steps listed in the [Disable user sign-ins for an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) article.</span></span>

## <a name="i-want-to-delete-an-application-entirely"></a><span data-ttu-id="bf25e-109">응용 프로그램을 완전히 삭제하려는 경우</span><span class="sxs-lookup"><span data-stu-id="bf25e-109">I want to delete an application entirely</span></span>

<span data-ttu-id="bf25e-110">**응용 프로그램을 삭제**하려면 아래 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="bf25e-110">To **delete an application**, follow the instructions below:</span></span>

1.  <span data-ttu-id="bf25e-111">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 또는 **공동 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="bf25e-111">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="bf25e-112">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bf25e-112">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bf25e-113">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bf25e-113">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bf25e-114">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bf25e-114">Click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="bf25e-115">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="bf25e-115">Click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="bf25e-116">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf25e-116">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="bf25e-117">삭제하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bf25e-117">Select the application you want to delete.</span></span>

7.  <span data-ttu-id="bf25e-118">응용 프로그램이 로드되면 맨 위의 응용 프로그램 **개요** 블레이드에서 **삭제** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bf25e-118">Once the application loads, click **Delete** icon from the top application’s **Overview** blade.</span></span>

## <a name="i-want-to-disable-all-future-user-consent-operations-to-any-application"></a><span data-ttu-id="bf25e-119">모든 응용 프로그램에 대한 모든 이후 사용자 동의 작업을 비활성화하려는 경우</span><span class="sxs-lookup"><span data-stu-id="bf25e-119">I want to disable all future user consent operations to any application</span></span>

<span data-ttu-id="bf25e-120">전체 디렉터리에 대한 사용자 동의를 비활성화하면 모든 응용 프로그램에 대한 최종 사용자 동의를 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="bf25e-120">Disabling user consent for your entire directory prevent end users from consenting to any application.</span></span> <span data-ttu-id="bf25e-121">관리자는 여전히 사용자의 동작에 동의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf25e-121">Administrators can still consent on user’s behalves.</span></span> <span data-ttu-id="bf25e-122">응용 프로그램 동의 및 이 작업을 수행하거나 수행하지 않을 수 있는 이유에 대해 자세히 알아보려면 [사용자 및 관리자 동의 이해하기](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bf25e-122">To learn more about application consent, and why you may or may not wish to do this, read [Understanding user and admin consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span></span>

<span data-ttu-id="bf25e-123">**전체 디렉터리에서 모든 이후 사용자 동의 작업을 비활성화**하려면 아래의 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="bf25e-123">To **disable all future user consent operations in your entire directory**, follow the instructions below:</span></span>

1.  <span data-ttu-id="bf25e-124">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="bf25e-124">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="bf25e-125">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bf25e-125">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bf25e-126">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bf25e-126">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bf25e-127">탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bf25e-127">Click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="bf25e-128">**사용자 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bf25e-128">Click **User settings**.</span></span>

6.  <span data-ttu-id="bf25e-129">**사용자가 앱이 데이터에 액세스하도록 허용할 수 있음** 토글을 **아니요**로 설정하고 **저장** 단추를 클릭하여 모든 이후 사용자 동의 작업을 비활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="bf25e-129">Disable all future user consent operations by setting the **Users can allow apps to access their data** toggle to **No** and click the **Save** button.</span></span>


# <a name="next-steps"></a><span data-ttu-id="bf25e-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bf25e-130">Next steps</span></span>
[<span data-ttu-id="bf25e-131">앱에 대한 액세스 관리</span><span class="sxs-lookup"><span data-stu-id="bf25e-131">Managing access to apps</span></span>](active-directory-managing-access-to-apps.md)
