---
title: "Azure Active Directory에서 그룹에 대한 라이선스 문제 해결 | Microsoft Docs"
description: "Azure Active Directory 그룹 기반 라이선스를 사용할 때 라이선스 할당 문제를 식별하고 해결하는 방법"
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
ms.openlocfilehash: bfa951a897c9b383072c0d29c9a4266c163fe753
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="identify-and-resolve-license-assignment-problems-for-a-group-in-azure-active-directory"></a><span data-ttu-id="f55fd-104">Azure Active Directory에서 그룹에 대한 라이선스 문제 식별 및 해결</span><span class="sxs-lookup"><span data-stu-id="f55fd-104">Identify and resolve license assignment problems for a group in Azure Active Directory</span></span>

<span data-ttu-id="f55fd-105">Azure AD(Azure Active Directory)의 그룹 기반 라이선스에는 라이선스 오류 상태의 사용자에 대한 개념이 도입되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-105">Group-based licensing in Azure Active Directory (Azure AD) introduces the concept of users in a licensing error state.</span></span> <span data-ttu-id="f55fd-106">이 문서에서는 사용자가 이 상태가 되는 이유를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-106">In this article, we explain the reasons why users might end up in this state.</span></span>

<span data-ttu-id="f55fd-107">그룹 기반 라이선스를 사용하지 않고 개별 사용자에게 직접 라이선스를 할당하면 할당 작업이 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-107">When you assign licenses directly to individual users, without using group-based licensing, the assignment operation might fail.</span></span> <span data-ttu-id="f55fd-108">예를 들어 사용자에 대해 `Set-MsolUserLicense` PowerShell cmdlet을 실행하면 비즈니스 논리와 관련된 여러 가지 이유로 cmdlet이 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-108">For example, when you execute the PowerShell cmdlet `Set-MsolUserLicense` on a user, the cmdlet can fail for a number of reasons that are related to business logic.</span></span> <span data-ttu-id="f55fd-109">라이선스 수가 부족하거나 동시에 할당할 수 없는 두 서비스 간에 충돌이 있는 경우를 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-109">For example, there might be an insufficient number of licenses or a conflict between two service plans that can't be assigned at the same time.</span></span> <span data-ttu-id="f55fd-110">문제는 즉시 사용자에게 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-110">The problem is immediately reported back to you.</span></span>

<span data-ttu-id="f55fd-111">그룹 기반 라이선스를 사용하는 경우 같은 오류가 발생할 수 있지만 Azure AD 서비스에서 라이선스를 할당하면 문제가 백그라운드에서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-111">When you're using group-based licensing, the same errors can occur, but they happen in the background when the Azure AD service is assigning licenses.</span></span> <span data-ttu-id="f55fd-112">이러한 이유로 사용자에게 즉시 오류를 전달 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-112">For this reason, the errors can't be communicated to you immediately.</span></span> <span data-ttu-id="f55fd-113">대신 오류가 사용자 개체에 기록된 후 관리 포털을 통해 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-113">Instead, they're recorded on the user object and then reported via the administrative portal.</span></span> <span data-ttu-id="f55fd-114">사용자에게 라이선스를 부여하는 원래의 의도는 절대 없어지지 않지만 향후 조사 및 문제 해결을 위해 라이선스를 오류 상태로 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-114">Note that the original intent to license the user is never lost, but it's recorded in an error state for future investigation and resolution.</span></span>

## <a name="how-to-find-license-assignment-errors"></a><span data-ttu-id="f55fd-115">라이선스 할당 오류를 찾는 방법</span><span class="sxs-lookup"><span data-stu-id="f55fd-115">How to find license assignment errors</span></span>

1. <span data-ttu-id="f55fd-116">특정 그룹에서 오류 상태인 사용자를 찾으려면 그룹의 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-116">To find users in an error state in a specific group, open the blade for the group.</span></span> <span data-ttu-id="f55fd-117">오류 상태인 사용자가 있는 경우 **라이선스**에 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-117">Under **Licenses**, there will be a notification displayed if there are any users in an error state.</span></span>

![그룹, 오류 알림](media/active-directory-licensing-group-problem-resolution-azure-portal/group-error-notification.png)

2. <span data-ttu-id="f55fd-119">알림을 클릭하면 영향을 받는 모든 사용자 목록이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-119">Click the notification to open a list of all affected users.</span></span> <span data-ttu-id="f55fd-120">자세한 내용을 보려면 개별적으로 각 사용자를 클릭하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-120">You can click on each user individually to see more details.</span></span>

![그룹, 오류 상태인 사용자의 목록](media/active-directory-licensing-group-problem-resolution-azure-portal/list-of-users-with-errors.png)

3. <span data-ttu-id="f55fd-122">하나 이상의 오류를 포함하는 모든 그룹을 찾으려면 **Azure Active Directory** 블레이드에서 **라이선스** 및 **개요**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-122">To find all groups that contain at least one error, on the **Azure Active Directory** blade select **Licenses** and then **Overview**.</span></span> <span data-ttu-id="f55fd-123">일부 그룹에서 주의가 필요한 경우 정보 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-123">An info box is displayed when some groups require your attention.</span></span>

![개요, 오류 상태인 그룹에 대한 정보](media/active-directory-licensing-group-problem-resolution-azure-portal/group-errors-widget.png)

4. <span data-ttu-id="f55fd-125">오류가 발생한 모든 그룹의 목록을 보려면 상자를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-125">Click on the box to see a list of all groups with errors.</span></span> <span data-ttu-id="f55fd-126">자세한 내용은 각 그룹을 클릭하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-126">You can click each group for more details.</span></span>

![개요, 오류가 발생한 그룹의 목록](media/active-directory-licensing-group-problem-resolution-azure-portal/list-of-groups-with-errors.png)


<span data-ttu-id="f55fd-128">아래에서는 잠재적인 문제 및 문제 해결 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-128">Below is a description of each potential problem and the way to resolve it.</span></span>

## <a name="not-enough-licenses"></a><span data-ttu-id="f55fd-129">라이선스 부족</span><span class="sxs-lookup"><span data-stu-id="f55fd-129">Not enough licenses</span></span>

<span data-ttu-id="f55fd-130">**문제:** 그룹에 지정된 제품 중 하나에 사용 가능한 라이선스가 충분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-130">**Problem:** There aren't enough available licenses for one of the products that's specified in the group.</span></span> <span data-ttu-id="f55fd-131">제품에 대한 추가 라이선스를 구매하거나 다른 사용자 또는 그룹에서 사용하지 않는 라이선스를 해제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-131">You need to either purchase more licenses for the product, or free up unused licenses from other users or groups.</span></span>

<span data-ttu-id="f55fd-132">사용할 수 있는 라이선스 수를 확인하려면 **Azure Active Directory** > **라이선스** > **모든 제품**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-132">To see how many licenses are available, go to **Azure Active Directory** > **Licenses** > **All products**.</span></span>

<span data-ttu-id="f55fd-133">라이선스를 사용 중인 사용자와 그룹을 확인하려면 제품을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-133">To see which users and groups are consuming licenses, click a product.</span></span> <span data-ttu-id="f55fd-134">**사용이 허가된 사용자**에는 라이선스가 직접 할당되었거나 하나 이상의 그룹을 통해 할당된 모든 사용자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-134">Under **Licensed users**, you'll see all users who've had licenses assigned directly or via one or more groups.</span></span> <span data-ttu-id="f55fd-135">**사용이 허가된 그룹**에는 제품이 할당된 모든 그룹이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-135">Under **Licensed groups**, you'll see all groups that have that product assigned.</span></span>

<span data-ttu-id="f55fd-136">**PowerShell:** PowerShell cmdlet은 이 오류를 _CountViolation_으로 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-136">**PowerShell:** PowerShell cmdlets report this error as _CountViolation_.</span></span>

## <a name="conflicting-service-plans"></a><span data-ttu-id="f55fd-137">서비스 계획 충돌</span><span class="sxs-lookup"><span data-stu-id="f55fd-137">Conflicting service plans</span></span>

<span data-ttu-id="f55fd-138">**문제:** 그룹에 지정된 제품 중 하나에 이미 다른 제품을 통해 사용자에게 할당된 다른 서비스 계획과 충돌하는 서비스 계획이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-138">**Problem:** One of the products that's specified in the group contains a service plan that conflicts with another service plan that's already assigned to the user via a different product.</span></span> <span data-ttu-id="f55fd-139">일부 서비스 계획은 관련된 다른 서비스 계획과 동일한 사용자에게 할당할 수 없는 방식으로 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-139">Some service plans are configured in a way that they can't be assigned to the same user as another related service plan.</span></span>

<span data-ttu-id="f55fd-140">아래 예제를 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="f55fd-140">Consider the following example.</span></span> <span data-ttu-id="f55fd-141">모든 계획을 사용하도록 설정된 Office 365 Enterprise **E1**의 라이선스가 한 사용자에게 직접 할당되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-141">A user has a license for Office 365 Enterprise **E1** assigned directly, with all the plans enabled.</span></span> <span data-ttu-id="f55fd-142">이 사용자는 Office 365 Enterprise **E3** 제품이 할당된 그룹에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-142">The user has been added to a group that has the Office 365 Enterprise **E3** product assigned to it.</span></span> <span data-ttu-id="f55fd-143">이 제품에는 E1에 포함된 계획과 중복될 수 없는 서비스 계획이 포함되어 있으므로 그룹 라이선스 할당은 "서비스 계획 충돌" 오류로 인해 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-143">This product contains service plans that can't overlap with the plans included in E1, so the group license assignment will fail with the “Conflicting service plans” error.</span></span> <span data-ttu-id="f55fd-144">이 예제에서 충돌하는 서비스 계획은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-144">In this example, the conflicting service plans are:</span></span>

-   <span data-ttu-id="f55fd-145">SharePoint Online(계획 2)은 SharePoint Online(계획 1)과 충돌합니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-145">SharePoint Online (Plan 2) conflicts with SharePoint Online (Plan 1).</span></span>
-   <span data-ttu-id="f55fd-146">Exchange Online(계획 2)은 Exchange Online(계획 1)과 충돌합니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-146">Exchange Online (Plan 2) conflicts with Exchange Online (Plan 1).</span></span>

<span data-ttu-id="f55fd-147">이 충돌을 해결하려면 사용자에게 직접 할당된 E1 라이선스에서 두 계획을 사용하지 않도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-147">To solve this conflict, you need to disable those two plans either on the E1 license that's directly assigned to the user.</span></span> <span data-ttu-id="f55fd-148">또는 전체 그룹 라이선스 할당을 수정하고 E3 라이선스에서 계획을 사용하지 않도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-148">Or, you need to modify the entire group license assignment and disable the plans in the E3 license.</span></span> <span data-ttu-id="f55fd-149">또는 E1 라이선스가 E3 라이선스의 컨텍스트에서 중복될 경우 사용자에게서 E1 라이선스를 제거하기로 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-149">Alternatively, you might decide to remove the E1 license from the user if it's redundant in the context of the E3 license.</span></span>

<span data-ttu-id="f55fd-150">충돌하는 제품 라이선스 문제를 해결하는 방법은 항상 관리자가 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-150">The decision about how to resolve conflicting product licenses always belongs to the administrator.</span></span> <span data-ttu-id="f55fd-151">Azure AD는 라이선스 충돌을 자동으로 해결하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-151">Azure AD doesn't automatically resolve license conflicts.</span></span>

<span data-ttu-id="f55fd-152">**PowerShell:** PowerShell cmdlet은 이 오류를 _MutuallyExclusiveViolation_으로 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-152">**PowerShell:** PowerShell cmdlets report this error as _MutuallyExclusiveViolation_.</span></span>

## <a name="other-products-depend-on-this-license"></a><span data-ttu-id="f55fd-153">기타 제품은 이 라이선스에 종속됨</span><span class="sxs-lookup"><span data-stu-id="f55fd-153">Other products depend on this license</span></span>

<span data-ttu-id="f55fd-154">**문제:** 그룹에 지정된 제품 중 하나에 다른 제품의 다른 서비스 계획이 작동하기 위해 사용되어야 하는 서비스 계획이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-154">**Problem:** One of the products that's specified in the group contains a service plan that must be enabled for another service plan, in another product, to function.</span></span> <span data-ttu-id="f55fd-155">이 오류는 Azure AD가 기본 서비스 계획을 제거하려고 시도할 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-155">This error occurs when Azure AD attempts to remove the underlying service plan.</span></span> <span data-ttu-id="f55fd-156">예를 들어 그룹에서 사용자가 제거된 결과로 이 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-156">For example, this can happen as a result of the user being removed from the group.</span></span>

<span data-ttu-id="f55fd-157">이 문제를 해결하려면 다른 메서드를 통해 필수 계획을 사용자에게 이미 할당하거나 해당 사용자에 대한 종속 서비스를 비활성화했는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-157">To solve this problem, you'll need to make sure that the required plan is still assigned to users through some other method, or that the dependent services are disabled for those users.</span></span> <span data-ttu-id="f55fd-158">그 후 해당 사용자에서 그룹 라이선스를 적절하게 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-158">After doing that, you can properly remove the group license from those users.</span></span>

<span data-ttu-id="f55fd-159">**PowerShell:** PowerShell cmdlet은 이 오류를 _DependencyViolation_으로 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-159">**PowerShell:** PowerShell cmdlets report this error as _DependencyViolation_.</span></span>

## <a name="usage-location-isnt-allowed"></a><span data-ttu-id="f55fd-160">사용 위치가 허용되지 않음</span><span class="sxs-lookup"><span data-stu-id="f55fd-160">Usage location isn't allowed</span></span>

<span data-ttu-id="f55fd-161">**문제:** 현지법 및 규정으로 인해 지역에 따라 일부 Microsoft 서비스가 제공되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-161">**Problem:** Some Microsoft services aren't available in all locations because of local laws and regulations.</span></span> <span data-ttu-id="f55fd-162">사용자에게 라이선스를 할당하려면 먼저 사용자에 대한 "사용 위치" 속성을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-162">Before you can assign a license to a user, you have to specify the “Usage location” property for the user.</span></span> <span data-ttu-id="f55fd-163">이 작업은 Azure Portal의 **사용자** > **프로필** > **설정**에서 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-163">You can do this under the **User** > **Profile** > **Settings** section in the Azure portal.</span></span>

<span data-ttu-id="f55fd-164">Azure AD가 사용 위치가 지원되지 않는 사용자에게 그룹 라이선스를 할당하려고 하면 작업이 실패하고 사용자에게 이 오류를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-164">When Azure AD attempts to assign a group license to a user whose usage location isn't supported, it will fail and record this error on the user.</span></span>

<span data-ttu-id="f55fd-165">이 문제를 해결하려면 라이선스가 부여된 그룹의 지원되지 않는 위치에서 사용자를 제거하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-165">To solve this problem, remove users from nonsupported locations from the licensed group.</span></span> <span data-ttu-id="f55fd-166">또는 현재 사용 위치 값이 실제 사용자의 위치를 나타내지 않는 경우에는 다음에 라이선스가 정확히 할당되도록 사용 위치 값을 수정하면 됩니다(새 위치가 지원되는 경우).</span><span class="sxs-lookup"><span data-stu-id="f55fd-166">Alternatively, if the current usage location values don't represent the actual user location, you can modify them so that the licenses are correctly assigned next time (if the new location is supported).</span></span>

<span data-ttu-id="f55fd-167">**PowerShell:** PowerShell cmdlet은 이 오류를 _ProhibitedInUsageLocationViolation_으로 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-167">**PowerShell:** PowerShell cmdlets report this error as _ProhibitedInUsageLocationViolation_.</span></span>

> [!NOTE]
> <span data-ttu-id="f55fd-168">Azure AD가 그룹 라이선스를 할당하면 사용 위치가 지정되지 않은 사용자는 디렉터리의 위치를 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-168">When Azure AD assigns group licenses, any users without a usage location specified inherit the location of the directory.</span></span> <span data-ttu-id="f55fd-169">현지법 및 규정을 준수하는 그룹 기반 라이선스를 사용하기 전에 관리자가 올바른 사용 위치 값을 사용자에게 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-169">We recommend that administrators set the correct usage location values on users before using group-based licensing to comply with local laws and regulations.</span></span>

## <a name="what-happens-when-theres-more-than-one-product-license-on-a-group"></a><span data-ttu-id="f55fd-170">한 그룹에 두 개 이상의 제품 라이선스가 있으면 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="f55fd-170">What happens when there's more than one product license on a group?</span></span>

<span data-ttu-id="f55fd-171">한 그룹에 두 개 이상의 제품 라이선스를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-171">You can assign more than one product license to a group.</span></span> <span data-ttu-id="f55fd-172">예를 들어 그룹에 Office 365 Enterprise E3 및 Enterprise Mobility + Security를 할당하면 해당 사용자에 대해 포함된 모든 서비스를 쉽게 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-172">For example, you can assign Office 365 Enterprise E3 and Enterprise Mobility + Security to a group to easily enable all included services for users.</span></span>

<span data-ttu-id="f55fd-173">Azure AD는 그룹에 지정된 모든 라이선스를 각 사용자에게 할당하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-173">Azure AD attempts to assign all licenses that are specified in the group to each user.</span></span> <span data-ttu-id="f55fd-174">Azure AD는 비즈니스 논리 문제(예를 들어 라이선스가 부족하거나 사용자에 대해 사용하도록 설정된 다른 서비스와 충돌이 있는 경우)로 인해 제품 중 하나를 할당할 수 없는 경우 그룹의 다른 라이선스를 할당하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-174">If Azure AD can't assign one of the products because of business logic problems (for example, if there aren't enough licenses for all, or if there are conflicts with other services that are enabled on the user), it won't assign the other licenses in the group either.</span></span>

<span data-ttu-id="f55fd-175">할당이 실패한 사용자를 확인하고 이로 인해 영향을 받는 제품을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-175">You'll be able to see the users who failed to get assigned failed and check which products have been affected by this.</span></span>

## <a name="license-assignment-fails-silently-for-a-user-due-to-duplicate-proxy-addresses-in-exchange-online"></a><span data-ttu-id="f55fd-176">Exchange Online의 중복된 프록시 주소 때문에 라이선스 할당이 자동으로 실패함</span><span class="sxs-lookup"><span data-stu-id="f55fd-176">License assignment fails silently for a user due to duplicate proxy addresses in Exchange Online</span></span>

<span data-ttu-id="f55fd-177">Exchange Online을 사용 중인 경우 테넌트의 일부 사용자가 동일한 프록시 주소 값으로 올바르게 구성되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-177">If you are using Exchange Online, some users in your tenant may be incorrectly configured with the same proxy address value.</span></span> <span data-ttu-id="f55fd-178">그룹 기반 라이선스가 이러한 사용자에게 라이선스를 할당하려고 하면 실패하며 오류는 기록되지 않습니다(위에 설명된 다른 오류 경우와 다름) 이 기능의 미리 보기 버전이 제한되어 있기 때문입니다. 이 문제는 *일반 공급* 이전에 해결될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-178">When group-based licensing tries to assign a license to such a user, it will fail and will not record an error (unlike in the other error cases described above) - this is a limitation in the preview version of this feature and we are going to address it before *General Availability*.</span></span>

> [!TIP]
> <span data-ttu-id="f55fd-179">일부 사용자가 라이선스를 받지 못했으며 해당 사용자에 대해 기록된 오류가 없는 경우 먼저 중복된 프록시 주소를 갖고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-179">If you notice that some users did not receive a license and there is no error recorded on those users, first check if they have duplicate proxy address.</span></span>
> <span data-ttu-id="f55fd-180">Exchange Online에 대해 다음 PowerShell cmdlet을 실행하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-180">This can be done by executing the following PowerShell cmdlet against Exchange Online:</span></span>
```
Run Get-Recipient | where {$_.EmailAddresses -match "user@contoso.onmicrosoft.com"} | fL Name, RecipientType,emailaddresses
```
> <span data-ttu-id="f55fd-181">[이 문서](https://support.microsoft.com/help/3042584/-proxy-address-address-is-already-being-used-error-message-in-exchange-online)에는 [원격 PowerShell을 사용하여 Exchange Online에 연결하는 방법](https://technet.microsoft.com/library/jj984289.aspx)에 대한 정보 등, 이 문제에 대한 자세한 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-181">[This article](https://support.microsoft.com/help/3042584/-proxy-address-address-is-already-being-used-error-message-in-exchange-online) contains more details about this problem, including information on [how to connect to Exchange Online using remote PowerShell](https://technet.microsoft.com/library/jj984289.aspx).</span></span>

<span data-ttu-id="f55fd-182">영향을 받는 사용자에 대해 프록시 주소 문제가 해결된 후에 그룹에 대해 강제로 라이선스 처리를 수행하여 라이선스가 다시 적용될 수 있게 하세요.</span><span class="sxs-lookup"><span data-stu-id="f55fd-182">After proxy address problems have been resolved for the affected users, make sure to force license processing on the group to make sure licenses can now be applied again.</span></span>

## <a name="how-do-you-force-license-processing-in-a-group-to-resolve-errors"></a><span data-ttu-id="f55fd-183">오류를 해결하기 위해 그룹의 라이선스를 강제로 처리하는 방법</span><span class="sxs-lookup"><span data-stu-id="f55fd-183">How do you force license processing in a group to resolve errors?</span></span>

<span data-ttu-id="f55fd-184">오류를 해결하기 위해 수행한 단계에 따라 그룹의 처리를 수동으로 트리거하여 사용자 상태를 업데이트해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-184">Depending on what steps you've taken to resolve errors, it might be necessary to manually trigger processing of a group to update the user state.</span></span>

<span data-ttu-id="f55fd-185">예를 들어 사용자에게서 직접 라이선스 할당을 제거하여 라이선스를 확보한 경우 모든 사용자 구성원에게 완전한 사용 권한을 부여하기 위해 이전에 실패한 그룹 처리를 트리거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-185">For example, if you freed up some licenses by removing direct license assignments from users, you'll need to trigger processing of groups that previously failed to fully license all user members.</span></span> <span data-ttu-id="f55fd-186">이렇게 하려면 그룹 블레이드를 찾은 후 **라이선스**를 선택하고 도구 모음에서 **다시 처리** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f55fd-186">To do that, find the group blade, open **Licenses**, and select the **Reprocess** button in the toolbar.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f55fd-187">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f55fd-187">Next steps</span></span>

<span data-ttu-id="f55fd-188">그룹을 통한 라이선스 관리에 대한 기타 시나리오에 대해 자세히 알아보려면 다음 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f55fd-188">To learn more about other scenarios for license management through groups, see the following:</span></span>

* [<span data-ttu-id="f55fd-189">Azure Active Directory에서 그룹에 라이선스 할당</span><span class="sxs-lookup"><span data-stu-id="f55fd-189">Assigning licenses to a group in Azure Active Directory</span></span>](active-directory-licensing-group-assignment-azure-portal.md)
* [<span data-ttu-id="f55fd-190">Azure Active Directory의 그룹 기반 라이선스란?</span><span class="sxs-lookup"><span data-stu-id="f55fd-190">What is group-based licensing in Azure Active Directory?</span></span>](active-directory-licensing-whatis-azure-portal.md)
* [<span data-ttu-id="f55fd-191">Azure Active Directory에서 개별 라이선스 사용자를 그룹 기반 라이선스로 마이그레이션하는 방법</span><span class="sxs-lookup"><span data-stu-id="f55fd-191">How to migrate individual licensed users to group-based licensing in Azure Active Directory</span></span>](active-directory-licensing-group-migration-azure-portal.md)
* [<span data-ttu-id="f55fd-192">Azure Active Directory 그룹 기반 라이선스 추가 시나리오</span><span class="sxs-lookup"><span data-stu-id="f55fd-192">Azure Active Directory group-based licensing additional scenarios</span></span>](active-directory-licensing-group-advanced.md)
