---
title: "Azure AD 갤러리 응용 프로그램에 잘못된 사용자 집합이 프로비전됨 | Microsoft Docs"
description: "예상한 것과 다른 사용자 집합이 응용 프로그램에 프로비전되는 이유를 파악하는 방법 알아보기"
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
ms.openlocfilehash: 85b533584c8ec15a23be32e20db7de583fced6a0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="wrong-set-of-users-are-being-provisioned-to-an-azure-ad-gallery-application"></a><span data-ttu-id="1f71e-103">Azure AD 갤러리 응용 프로그램에 잘못된 사용자 집합이 프로비전됨</span><span class="sxs-lookup"><span data-stu-id="1f71e-103">Wrong set of users are being provisioned to an Azure AD Gallery application</span></span>

<span data-ttu-id="1f71e-104">앱에 프로비전되는 사용자는 주로 응용 프로그램에 **할당**된 사용자 및 그룹에 따라 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-104">Which users are provisioned to the app is primarily driven by which users and groups have been **assigned** to the application.</span></span>

<span data-ttu-id="1f71e-105">아래 리소스를 사용하여 Azure Active Directory 내에서 응용 프로그램에 할당된 사용자 및 그룹을 확인하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-105">Use the resources below to learn how to check which users and groups have been assigned to an application within Azure Active Directory.</span></span>

## <a name="assign-a-user-directly-as-an-administrator"></a><span data-ttu-id="1f71e-106">관리자 권한으로 직접 사용자 할당</span><span class="sxs-lookup"><span data-stu-id="1f71e-106">Assign a user directly as an administrator</span></span>

<span data-ttu-id="1f71e-107">응용 프로그램에 하나 이상의 사용자를 직접 할당하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-107">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="1f71e-108">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-108">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1f71e-109">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-109">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1f71e-110">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-110">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1f71e-111">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-111">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1f71e-112">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-112">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="1f71e-113">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-113">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="1f71e-114">목록에서 사용자를 할당하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-114">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="1f71e-115">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-115">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1f71e-116">**사용자 및 그룹** 목록의 맨 위에서 **추가** 단추를 클릭하여 **할당 추가** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-116">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="1f71e-117">**할당 추가** 블레이드에서 **사용자 및 그룹** 선택기를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-117">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="1f71e-118">**이름 또는 전자 메일 주소로 검색** 검색 상자에 할당하려는 사용자의 **전체 이름** 또는 **전자 메일 주소**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-118">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="1f71e-119">목록의 **사용자** 위로 마우스를 이동하여 **확인란**을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-119">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="1f71e-120">사용자의 프로필 사진이나 로고 옆의 확인란을 클릭하여 사용자를 **선택됨** 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-120">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="1f71e-121">**선택 사항:** **둘 이상의 사용자를 추가**하려는 경우 **이름 또는 전자 메일 주소로 검색** 검색 상자에 다른 **전체 이름** 또는 **전자 메일 주소**를 입력하고 확인란을 클릭하여 이 사용자를 **선택됨** 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-121">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="1f71e-122">사용자 선택이 완료되면 **선택** 단추를 클릭하여 응용 프로그램에 할당되도록 사용자 및 그룹의 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-122">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="1f71e-123">**선택 사항:** **할당 추가** 블레이드에서 **역할 선택** 선택기를 클릭하여 선택한 사용자에게 할당할 역할을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-123">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="1f71e-124">**할당** 단추를 클릭하여 선택한 사용자에게 응용 프로그램을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-124">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="1f71e-125">앱에 대해 프로비저닝이 구성되어 있고 이미 실행되고 있으면 새 사용자는 약 10분 후에 응용 프로그램에 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-125">If provisioning is configured and already running for an app, new users should be provisioned to an application in approximately 10 minutes.</span></span> <span data-ttu-id="1f71e-126">자세한 내용은 **감사 로그**를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-126">Check the **Audit Logs** for details.</span></span>

## <a name="assign-a-group-directly-to-an-application-as-an-administrator"></a><span data-ttu-id="1f71e-127">관리자 권한으로 응용 프로그램에 직접 그룹 할당</span><span class="sxs-lookup"><span data-stu-id="1f71e-127">Assign a group directly to an application as an administrator</span></span>

<span data-ttu-id="1f71e-128">응용 프로그램에 하나 이상의 그룹을 직접 할당하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-128">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="1f71e-129">[**Azure Portal**](https://portal.azure.com/)을 열고 **전역 관리자** 권한으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-129">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1f71e-130">왼쪽 주 탐색 메뉴의 맨 아래에서 **추가 서비스**를 클릭하여 **Azure Active Directory 확장**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-130">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1f71e-131">필터 검색 상자에 **“Azure Active Directory**”를 입력하고 **Azure Active Directory** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-131">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1f71e-132">Azure Active Directory 왼쪽 탐색 메뉴에서 **엔터프라이즈 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-132">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1f71e-133">**모든 응용 프로그램**을 클릭하여 모든 응용 프로그램의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-133">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="1f71e-134">여기에 표시하려는 응용 프로그램이 표시되지 않으면 **모든 응용 프로그램 목록**의 맨 위에서 **필터** 컨트롤을 사용하고 **표시** 옵션을 **모든 응용 프로그램**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-134">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="1f71e-135">목록에서 사용자를 할당하려는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-135">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="1f71e-136">응용 프로그램이 로드되면 응용 프로그램의 왼쪽 탐색 메뉴에서 **사용자 및 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-136">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1f71e-137">**사용자 및 그룹** 목록의 맨 위에서 **추가** 단추를 클릭하여 **할당 추가** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-137">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="1f71e-138">**할당 추가** 블레이드에서 **사용자 및 그룹** 선택기를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-138">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="1f71e-139">**이름 또는 메일 주소로 검색** 검색 상자에 할당하려는 그룹의 **전체 그룹 이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-139">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="1f71e-140">목록의 **그룹** 위로 마우스를 이동하여 **확인란**을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-140">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="1f71e-141">그룹의 프로필 사진이나 로고 옆의 확인란을 클릭하여 사용자를 **선택됨** 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-141">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="1f71e-142">**선택 사항:** **둘 이상의 그룹을 추가**하려는 경우 **이름 또는 메일 주소로 검색** 검색 상자에 다른 **전체 그룹 이름**을 입력하고 확인란을 클릭하여 이 그룹을 **선택됨** 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-142">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="1f71e-143">그룹 선택이 완료되면 **선택** 단추를 클릭하여 응용 프로그램에 할당되도록 사용자 및 그룹의 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-143">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="1f71e-144">**선택 사항:** **할당 추가** 블레이드에서 **역할 선택** 선택기를 클릭하여 선택한 그룹에 할당할 역할을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-144">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="1f71e-145">**할당** 단추를 클릭하여 선택한 그룹에 응용 프로그램을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-145">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="1f71e-146">앱에 대해 프로비저닝이 구성되어 있고 이미 실행되고 있으면 그룹 내에 포함된 새 사용자는 약 10분 후에 응용 프로그램에 프로비전되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-146">If provisioning is configured and already running for an app, new users contained within the group should be provisioned to an application in approximately 10 minutes.</span></span> <span data-ttu-id="1f71e-147">자세한 내용은 **감사 로그**를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-147">Check the **Audit Logs** for details.</span></span>

>[!IMPORTANT]
><span data-ttu-id="1f71e-148">일부 응용 프로그램에 대해 지원되는 경우, 구성원 외에 그룹 이름 및 그룹 세부 정보 프로비전.</span><span class="sxs-lookup"><span data-stu-id="1f71e-148">Provisioning of the group name and group details, in addition to the members, if supported for some applications.</span></span> <span data-ttu-id="1f71e-149">**프로비전** 탭에 표시된 그룹 개체의 **Mapping**(매핑)을 사용하거나 사용하지 않도록 설정하여 이 기능을 사용하거나 사용하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-149">You can enable or disable this functionality by enabling or disabling the **Mapping** for group objects shown in the **Provisioning** tab.</span></span> 
>
>

<span data-ttu-id="1f71e-150">그룹 프로비전을 사용하는 경우 특성 매핑을 검토하여 “일치하는 ID”에 적절한 필드를 사용하는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="1f71e-150">If provisioning groups is enabled, be sure to review the attribute mappings to ensure an appropriate field is being used for the “matching ID”.</span></span> <span data-ttu-id="1f71e-151">이는 표시 이름이나 메일 별칭일 수 있습니다. Azure AD에 일치하는 속성이 비어 있거나 그룹에 대해 입력되어 있지 않은 경우 그룹 및 구성원이 프로비전되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1f71e-151">This can be the display name or email alias, as the group and its members not be provisioned if the matching property is empty or not populated for a group in Azure AD.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f71e-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1f71e-152">Next steps</span></span>
[<span data-ttu-id="1f71e-153">Azure Active Directory를 사용하여 SaaS 응용 프로그램의 사용자를 자동으로 프로비저닝 및 프로비저닝 해제</span><span class="sxs-lookup"><span data-stu-id="1f71e-153">Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory</span></span>](active-directory-saas-app-provisioning.md)
