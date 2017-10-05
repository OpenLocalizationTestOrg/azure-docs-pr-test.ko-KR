---
title: "Azure Active Directory에서 그룹에 라이선스 할당 | Microsoft Docs"
description: "Azure Active Directory 그룹 기반 라이선스를 사용하여 사용자에게 라이선스를 할당하는 방법"
services: active-directory
keywords: "Azure AD 라이선스"
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/05/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 42b18eab9cb419e6ada72ba72dc8be8d7f7b2eed
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="assign-licenses-to-users-by-group-membership-in-azure-active-directory"></a><span data-ttu-id="987a2-104">Azure Active Directory에서 그룹 멤버 자격별로 사용자에게 라이선스 할당</span><span class="sxs-lookup"><span data-stu-id="987a2-104">Assign licenses to users by group membership in Azure Active Directory</span></span>

<span data-ttu-id="987a2-105">이 문서에서는 Azure Active Directory (Azure AD)에서 사용자 그룹에 제품 라이선스를 할당하고 올바르게 허가를 받았는지 확인하는 과정을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-105">This article walks you through assigning product licenses to a group of users in Azure Active Directory (Azure AD) and then verifying that they're licensed correctly.</span></span>

<span data-ttu-id="987a2-106">이 예에서는 테넌트에 **HR 부서**라는 보안 그룹이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-106">In this example, the tenant contains a security group called **HR Department**.</span></span> <span data-ttu-id="987a2-107">이 그룹에는 인사 부서의 모든 멤버(약 1,000명의 사용자)이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-107">This group includes all members of the human resources department (around 1,000 users).</span></span> <span data-ttu-id="987a2-108">사용자가 부서 전체에 Office 365 Enterprise E3 라이선스를 할당하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-108">You want to assign Office 365 Enterprise E3 licenses to the entire department.</span></span> <span data-ttu-id="987a2-109">제품에 포함된 Yammer Enterprise 서비스는 해당 부서에서 사용할 준비를 갖출 때까지 일시적으로 사용하지 않도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-109">The Yammer Enterprise service that's included in the product must be temporarily disabled until the department is ready to start using it.</span></span> <span data-ttu-id="987a2-110">또한 동일한 사용자 그룹에 Enterprise Mobility + Security 라이선스를 배포하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-110">You also want to deploy Enterprise Mobility + Security licenses to the same group of users.</span></span>

> [!NOTE]
> <span data-ttu-id="987a2-111">일부 Microsoft 서비스는 모든 위치에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-111">Some Microsoft services are not available in all locations.</span></span> <span data-ttu-id="987a2-112">사용자에게 라이선스를 할당하려면 먼저 관리자가 해당 사용자에 대해 사용 위치 속성을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-112">Before a license can be assigned to a user, the administrator has to specify the Usage location property on the user.</span></span>

> <span data-ttu-id="987a2-113">그룹 라이선스 할당의 경우 사용 위치가 지정되지 않은 사용자는 디렉터리의 위치를 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-113">For group license assignment, any users without a usage location specified will inherit the location of the directory.</span></span> <span data-ttu-id="987a2-114">여러 위치에 사용자가 있는 경우 항상 Azure AD에서 사용자 만들기 흐름의 일부로(예: AAD Connect 구성을 통해) 사용 위치를 설정하는 것이 좋습니다. 이렇게 하면 라이선스 할당의 결과가 항상 정확하고 허용되지 않은 위치에서 사용자에게 서비스가 제공되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-114">If you have users in multiple locations, we recommend that you always set usage location as part of your user creation flow in Azure AD (e.g. via AAD Connect configuration) - that will ensure the result of license assignment is always correct and users do not receive services in locations that are not allowed.</span></span>

## <a name="step-1-assign-the-required-licenses"></a><span data-ttu-id="987a2-115">1단계: 필요한 라이선스 할당</span><span class="sxs-lookup"><span data-stu-id="987a2-115">Step 1: Assign the required licenses</span></span>

1. <span data-ttu-id="987a2-116">관리자 계정으로 [**Azure Portal**](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-116">Sign in to the [**Azure portal**](https://portal.azure.com) with an Administrator account.</span></span> <span data-ttu-id="987a2-117">라이선스를 관리하려면 계정은 전역 관리자 역할 또는 사용자 계정 관리자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-117">To manage licenses, the account must be a global administrator role or user account administrator.</span></span>

2. <span data-ttu-id="987a2-118">왼쪽 탐색 창에서 **더 많은 서비스**를 선택하고 **Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-118">Select **More services** in the left navigation pane, and then select **Azure Active Directory**.</span></span> <span data-ttu-id="987a2-119">이 블레이드를 즐겨찾기에 추가하거나 포털 대시보드에 고정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-119">You can add this blade to Favorites or pin it to the portal dashboard.</span></span>

3. <span data-ttu-id="987a2-120">**Azure Active Directory** 블레이드에서 **라이선스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-120">On the **Azure Active Directory** blade, select **Licenses**.</span></span> <span data-ttu-id="987a2-121">이렇게 하면 테넌트에서 사용이 허가된 모든 제품을 보고 관리할 수 있는 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-121">This opens a blade where you can see and manage all licensable products in the tenant.</span></span>

4. <span data-ttu-id="987a2-122">**모든 제품**에서 제품 이름을 선택하여 Office 365 Enterprise E3 및 Enterprise Mobility + Security를 둘 다 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-122">Under **All products**, select both Office 365 Enterprise E3 and Enterprise Mobility + Security by selecting the product names.</span></span> <span data-ttu-id="987a2-123">할당을 시작하려면 블레이드 맨 위에 있는 **할당**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-123">To start the assignment, select **Assign** at the top of the blade.</span></span>

   ![모든 제품, 라이선스 할당](media/active-directory-licensing-group-assignment-azure-portal/all-products-assign.png)

5. <span data-ttu-id="987a2-125">**라이선스 할당** 블레이드에서 **사용자 및 그룹**을 클릭하여 **사용자 및 그룹** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-125">On the **Assign license** blade, click **Users and groups** to open the **Users and groups** blade.</span></span> <span data-ttu-id="987a2-126">그룹 이름 *HR Department*를 검색하고 그룹을 선택한 후 블레이드 맨 아래에서 **선택**을 클릭하여 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-126">Search for the group name *HR Department*, select the group, and then be sure to confirm by clicking **Select** at the bottom of the blade.</span></span>

   ![그룹 선택](media/active-directory-licensing-group-assignment-azure-portal/select-a-group.png)

6. <span data-ttu-id="987a2-128">**라이선스 할당** 블레이드에서 **할당 옵션(선택 사항)**을 클릭하여 앞서 선택한 두 가지 제품에 포함된 모든 서비스 계획을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-128">On the **Assign license** blade, click **Assignment options (optional)**, which displays all service plans included in the two products that we selected previously.</span></span> <span data-ttu-id="987a2-129">**Yammer Enterprise**를 찾은 후 **해제**하여 제품 라이선스에서 해당 서비스를 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-129">Find **Yammer Enterprise** and turn it **Off** to disable that service from the product license.</span></span> <span data-ttu-id="987a2-130">**할당 옵션** 맨 아래에서 **확인**을 클릭하여 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-130">Confirm by clicking **OK** at the bottom of **Assignment options**.</span></span>

   ![할당 옵션](media/active-directory-licensing-group-assignment-azure-portal/assignment-options.png)

7. <span data-ttu-id="987a2-132">할당을 완료하려면 **라이선스 할당** 블레이드 맨 아래에서 **할당**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-132">To complete the assignment, on the **Assign license** blade, click **Assign** at the bottom of the blade.</span></span>

8. <span data-ttu-id="987a2-133">오른쪽 위 모서리에 프로세스의 상태와 결과를 보여 주는 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-133">A notification is displayed in the upper-right corner that shows the status and outcome of the process.</span></span> <span data-ttu-id="987a2-134">그룹에 대한 할당을 완료할 수 없으면(예를 들어 그룹의 기존 라이선스 때문에) 알림을 클릭하여 실패 세부 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-134">If the assignment to the group couldn't be completed (for example, because of pre-existing licenses in the group), click the notification to view details of the failure.</span></span>

<span data-ttu-id="987a2-135">이제 HR Department 그룹의 라이선스 템플릿이 지정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-135">We've now specified a license template for the HR Department group.</span></span> <span data-ttu-id="987a2-136">Azure AD에서 해당 그룹의 모든 기존 멤버를 처리하기 위한 백그라운드 프로세스가 시작되었습니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-136">A background process in Azure AD has been started to process all existing members of that group.</span></span> <span data-ttu-id="987a2-137">이 초기 작업은 그룹의 현재 크기에 따라 약간 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-137">This initial operation might take some time, depending on the current size of the group.</span></span> <span data-ttu-id="987a2-138">다음 단계에서는 프로세스가 완료되었는지와 문제 해결을 위해 추가적인 관리가 필요한지를 확인하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-138">In the next step, we'll describe how to verify that the process has finished and determine if further attention is required to resolve problems.</span></span>

> [!NOTE]
> <span data-ttu-id="987a2-139">대체 위치인 Azure AD의 **사용자 및 그룹**에서 동일한 할당을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-139">You can start the same assignment from an alternative location: **Users and groups** in Azure AD.</span></span> <span data-ttu-id="987a2-140">**Azure Active Directory** > **사용자 및 그룹** > **모든 그룹**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-140">Go to **Azure Active Directory** > **Users and groups** > **All groups**.</span></span> <span data-ttu-id="987a2-141">그 후 그룹을 찾아서 선택한 다음 **라이선스** 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-141">Then find the group, select it, and go to the **Licenses** tab.</span></span> <span data-ttu-id="987a2-142">블레이드 위쪽의 **할당** 단추를 클릭하면 라이선스 할당 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-142">The **Assign** button on top of the blade opens the license assignment blade.</span></span>

## <a name="step-2-verify-that-the-initial-assignment-has-finished"></a><span data-ttu-id="987a2-143">2단계: 초기 할당이 완료되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="987a2-143">Step 2: Verify that the initial assignment has finished</span></span>

1. <span data-ttu-id="987a2-144">**Azure Active Directory** > **사용자 및 그룹** > **모든 그룹**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-144">Go to **Azure Active Directory** > **Users and groups** > **All groups**.</span></span> <span data-ttu-id="987a2-145">그런 다음 라이선스가 할당된 **HR Department** 그룹을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-145">Then find the **HR Department** group that licenses were assigned to.</span></span>

2. <span data-ttu-id="987a2-146">**HR Department** 그룹 블레이드에서 **라이선스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-146">On the **HR Department** group blade, select **Licenses**.</span></span> <span data-ttu-id="987a2-147">그러면 사용자에게 라이선스가 완전히 할당되었는지, 확인해야 할 오류가 있는지 신속하게 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-147">This lets you quickly confirm if licenses have been fully assigned to users and if there are any errors that you need to look into.</span></span> <span data-ttu-id="987a2-148">다음과 같은 정보가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-148">The following information is available:</span></span>

   - <span data-ttu-id="987a2-149">현재 그룹에 할당된 제품 라이선스의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-149">List of product licenses that are currently assigned to the group.</span></span> <span data-ttu-id="987a2-150">사용하도록 설정된 특정 서비스를 표시하고 변경을 수행할 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-150">Select an entry to show the specific services that have been enabled and to make changes.</span></span>

   - <span data-ttu-id="987a2-151">그룹의 최신 라이선스 변경 상태(모든 사용자 구성원에 대해 변경 내용을 처리 중인지 아니면 처리가 완료되었는지).</span><span class="sxs-lookup"><span data-stu-id="987a2-151">Status of the latest license changes that were made to the group (if the changes are being processed or if processing has finished for all user members).</span></span>

   - <span data-ttu-id="987a2-152">라이선스를 할당할 수 없어서 오류 상태인 사용자에 대한 정보.</span><span class="sxs-lookup"><span data-stu-id="987a2-152">Information about users who are in an error state because licenses couldn't be assigned to them.</span></span>

   ![할당 옵션](media/active-directory-licensing-group-assignment-azure-portal/assignment-errors.png)

3. <span data-ttu-id="987a2-154">라이선스처리에 대한 자세한 내용은 **Azure Active Directory** > **사용자 및 그룹** > *그룹 이름* > **감사 로그**를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="987a2-154">See more detailed information about license processing under **Azure Active Directory** > **Users and groups** > *group name* > **Audit logs**.</span></span> <span data-ttu-id="987a2-155">다음 활동에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="987a2-155">Note the following activities:</span></span>

   - <span data-ttu-id="987a2-156">활동: **사용자에게 그룹 기반 라이선스 할당 시작**.</span><span class="sxs-lookup"><span data-stu-id="987a2-156">Activity: **Start applying group based license to users**.</span></span> <span data-ttu-id="987a2-157">시스템이 그룹에 대한 라이선스 할당 변경을 선택하고 모든 사용자 멤버에게 적용하기 시작하면 로깅됩니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-157">This is logged when the system picks up the license-assignment change on the group and starts applying it to all user members.</span></span> <span data-ttu-id="987a2-158">수행된 변경 내용에 대한 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-158">It contains information about the change that was made.</span></span>

   - <span data-ttu-id="987a2-159">활동: **사용자에게 그룹 기반 라이선스 할당 완료**.</span><span class="sxs-lookup"><span data-stu-id="987a2-159">Activity: **Finish applying group based license to users**.</span></span> <span data-ttu-id="987a2-160">시스템이 그룹의 모든 사용자에 대한 처리를 완료하면 로깅됩니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-160">This is logged when the system finishes processing all users in the group.</span></span> <span data-ttu-id="987a2-161">성공적으로 처리된 사용자 수와 그룹 라이선스를 할당하지 못한 사용자 수에 대한 요약 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-161">It contains a summary of how many users were successfully processed and how many users couldn't be assigned group licenses.</span></span>

   <span data-ttu-id="987a2-162">[이 섹션을 읽고](./active-directory-licensing-group-advanced.md#use-audit-logs-to-monitor-group-based-licensing-activity) 감사 로그를 사용하여 그룹 기반 라이선스에 의한 변경 내용을 분석하는 방법에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="987a2-162">[Read this section](./active-directory-licensing-group-advanced.md#use-audit-logs-to-monitor-group-based-licensing-activity) to learn more about how audit logs can be used to analyze changes made by group-based licensing.</span></span>

## <a name="step-3-check-for-license-problems-and-resolve-them"></a><span data-ttu-id="987a2-163">3단계: 라이선스 문제 확인 및 해결</span><span class="sxs-lookup"><span data-stu-id="987a2-163">Step 3: Check for license problems and resolve them</span></span>

1. <span data-ttu-id="987a2-164">**Azure Active Directory** > **사용자 및 그룹** > **모든 그룹**으로 이동한 후 라이선스가 할당된 **HR Department** 그룹을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-164">Go to **Azure Active Directory** > **Users and groups** > **All groups**, and find the **HR Department** group that licenses were assigned to.</span></span>
2. <span data-ttu-id="987a2-165">**HR Department** 그룹 블레이드에서 **라이선스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-165">On the **HR Department** group blade, select **Licenses**.</span></span> <span data-ttu-id="987a2-166">블레이드 맨 위에 라이선스를 할당하지 못한 사용자가 10명이라는 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-166">The notification on top of the blade shows that there are 10 users that licenses couldn't be assigned to.</span></span> <span data-ttu-id="987a2-167">이 알림을 클릭하면 이 그룹에서 라이선스 오류 상태인 모든 사용자 목록이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-167">Clicking it opens a list of all users in a licensing-error state for this group.</span></span>
3. <span data-ttu-id="987a2-168">**할당 실패** 열에는 두 제품 라이선스 모두 사용자에게 할당하지 못했다는 내용이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-168">The **Failed assignments** column tells us that both product licenses couldn't be assigned to the users.</span></span> <span data-ttu-id="987a2-169">**상위 실패 원인** 열에는 실패의 원인이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-169">The **Top reason for failure** column contains the cause of the failure.</span></span> <span data-ttu-id="987a2-170">이 예에서는 **충돌하는 서비스 계획**이 실패의 원인입니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-170">In this case, it's **Conflicting service plans**.</span></span>

   ![할당 실패](media/active-directory-licensing-group-assignment-azure-portal/failed-assignments.png)

4. <span data-ttu-id="987a2-172">사용자를 선택하여 **라이선스** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-172">Select a user to open the **Licenses** blade.</span></span> <span data-ttu-id="987a2-173">이 블레이드에는 현재 사용자에게 할당된 모든 라이선스가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-173">This blade shows all licenses that are currently assigned to the user.</span></span> <span data-ttu-id="987a2-174">이 예에서는 사용자에게 **키오스크 사용자** 그룹에서 상속된 Office 365 Enterprise E1 라이선스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-174">In this example, the user has the Office 365 Enterprise E1 license that was inherited from the **Kiosk users** group.</span></span> <span data-ttu-id="987a2-175">이 라이선스는 시스템에서 **HR Department** 그룹에 적용하려고 하는 E3 라이선스와 충돌합니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-175">This conflicts with the E3 license that the system tried to apply from the **HR Department** group.</span></span> <span data-ttu-id="987a2-176">결과적으로 해당 그룹의 어떠한 라이선스도 사용자에게 할당되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-176">As a result, none of the licenses from that group has been assigned to the user.</span></span>

   ![사용자의 라이선스 보기](media/active-directory-licensing-group-assignment-azure-portal/user-license-view.png)

5. <span data-ttu-id="987a2-178">이 충돌을 해결하기 위해 **키오스크 사용자** 그룹에서 해당 사용자를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-178">To solve this conflict, remove the user from the **Kiosk users** group.</span></span> <span data-ttu-id="987a2-179">Azure AD에서 변경 내용을 처리한 후에 **HR Department** 라이선스가 올바르게 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="987a2-179">After Azure AD processes the change, the **HR Department** licenses are correctly assigned.</span></span>

   ![잘못 할당된 라이선스](media/active-directory-licensing-group-assignment-azure-portal/license-correctly-assigned.png)

## <a name="next-steps"></a><span data-ttu-id="987a2-181">다음 단계</span><span class="sxs-lookup"><span data-stu-id="987a2-181">Next steps</span></span>

<span data-ttu-id="987a2-182">그룹의 라이선스를 관리할 수 있는 기능 집합에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="987a2-182">To learn more about the feature set for license management through groups, see the following articles:</span></span>

* [<span data-ttu-id="987a2-183">Azure Active Directory의 그룹 기반 라이선스란?</span><span class="sxs-lookup"><span data-stu-id="987a2-183">What is group-based licensing in Azure Active Directory?</span></span>](active-directory-licensing-whatis-azure-portal.md)
* [<span data-ttu-id="987a2-184">Azure Active Directory에서 그룹에 대한 라이선스 문제 식별 및 해결</span><span class="sxs-lookup"><span data-stu-id="987a2-184">Identifying and resolving license problems for a group in Azure Active Directory</span></span>](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [<span data-ttu-id="987a2-185">Azure Active Directory에서 개별 라이선스 사용자를 그룹 기반 라이선스로 마이그레이션하는 방법</span><span class="sxs-lookup"><span data-stu-id="987a2-185">How to migrate individual licensed users to group-based licensing in Azure Active Directory</span></span>](active-directory-licensing-group-migration-azure-portal.md)
* [<span data-ttu-id="987a2-186">Azure Active Directory 그룹 기반 라이선스 추가 시나리오</span><span class="sxs-lookup"><span data-stu-id="987a2-186">Azure Active Directory group-based licensing additional scenarios</span></span>](active-directory-licensing-group-advanced.md)
