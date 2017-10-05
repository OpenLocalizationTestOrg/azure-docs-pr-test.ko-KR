---
title: "Azure Active Directory에서 개별 라이선스 사용자를 그룹으로 마이그레이션하는 방법 | Microsoft Docs"
description: "Azure Active Directory를 사용하여 개별 라이선스 사용자를 그룹 기반 라이선스로 전환하는 방법"
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
ms.openlocfilehash: 6b77dd4e9a6d361a05382397e89b575896fdad84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-add-licensed-users-to-a-group-for-licensing-in-azure-active-directory"></a><span data-ttu-id="816a2-104">Azure Active Directory에서 라이선스에 대해 라이선스 사용자를 그룹에 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="816a2-104">How to add licensed users to a group for licensing in Azure Active Directory</span></span>

<span data-ttu-id="816a2-105">개별 사용자에게 라이선스를 할당하기 위해 "직접 할당"을 통해, 즉 PowerShell 스크립트 또는 기타 도구를 사용하여 조직의 사용자에게 기존 라이선스가 배포되었을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-105">You may have existing licenses deployed to users in the organizations via “direct assignment”; that is, using PowerShell scripts or other tools to assign individual user licenses.</span></span> <span data-ttu-id="816a2-106">조직에서 그룹 기반 라이선스를 사용하여 라이선스를 관리하려는 경우 기존 솔루션을 그룹 기반 라이선스로 원활하게 대체하기 위한 마이그레이션 계획이 필요하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-106">If you would like to start using group-based licensing to manage licenses in your organization, you will need a migration plan to seamlessly replace existing solutions with group-based licensing.</span></span>

<span data-ttu-id="816a2-107">가장 중요한 고려 사항은 그룹 기반 라이선스로의 마이그레이션으로 인해 사용자에게 현재 할당된 라이선스가 일시적으로 손실되는 상황을 피해야 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-107">The most important thing to keep in mind is that you should avoid a situation where migrating to group-based licensing will result in users temporarily losing their currently assigned licenses.</span></span> <span data-ttu-id="816a2-108">사용자가 서비스 및 해당 데이터에 액세스하지 못하는 일이 없도록 라이선스를 제거할 수 있는 프로세스는 피해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-108">Any process that may result in removal of licenses should be avoided to remove the risk of users losing access to services and their data.</span></span>

## <a name="recommended-migration-process"></a><span data-ttu-id="816a2-109">권장 마이그레이션 프로세스</span><span class="sxs-lookup"><span data-stu-id="816a2-109">Recommended migration process</span></span>

1. <span data-ttu-id="816a2-110">사용자에 대한 라이선스 할당 및 제거를 관리하는 기존 자동화(예: PowerShell) 기능이 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-110">You have existing automation (for example, PowerShell) managing license assignment and removal for users.</span></span> <span data-ttu-id="816a2-111">이러한 기능은 실행 상태로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-111">Leave it running as is.</span></span>

2. <span data-ttu-id="816a2-112">새 라이선스 그룹을 만들고(또는 사용할 기존 그룹 결정) 필요한 모든 사용자가 구성원으로 추가되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-112">Create a new licensing group (or decide which existing groups to use) and make sure that all required users are added as members.</span></span>

3. <span data-ttu-id="816a2-113">이러한 그룹에 필요한 라이선스를 할당합니다. 여기서의 기존 자동화(예: PowerShell)가 해당 사용자에게 적용하는 동일한 라이선스 상태가 반영되도록 하는 것이 목표입니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-113">Assign the required licenses to those groups; your goal should be to reflect the same licensing state your existing automation (for example, PowerShell) is applying to those users.</span></span>

4. <span data-ttu-id="816a2-114">해당 그룹의 모든 사용자에게 라이선스가 적용되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-114">Verify that licenses have been applied to all users in those groups.</span></span> <span data-ttu-id="816a2-115">이를 위해 각 그룹의 처리 상태를 확인하고 감사 로그를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-115">This can be done by checking the processing state on each group and by checking Audit Logs.</span></span>

  - <span data-ttu-id="816a2-116">라이선스 세부 정보를 확인하여 개별 사용자를 부분적으로 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-116">You can spot check individual users by looking at their license details.</span></span> <span data-ttu-id="816a2-117">이를 통해 이러한 사용자에게 동일한 라이선스가 "직접" 할당되고 그룹에서 "상속"되었음을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-117">You will see that they have the same licenses assigned “directly” and “inherited” from groups.</span></span>

  - <span data-ttu-id="816a2-118">PowerShell 스크립트를 실행하여 [사용자에게 라이선스가 할당된 방법을 확인](active-directory-licensing-group-advanced.md#use-powershell-to-see-who-has-inherited-and-direct-licenses)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-118">You can run a PowerShell script to [verify how licenses are assigned to users](active-directory-licensing-group-advanced.md#use-powershell-to-see-who-has-inherited-and-direct-licenses).</span></span>

  - <span data-ttu-id="816a2-119">동일한 제품 라이선스가 사용자에게 직접 방법과 그룹을 통한 방법으로 모두 할당되어도 해당 사용자에게는 라이선스가 하나만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-119">When the same product license is assigned to the user both directly and through a group, only one license is consumed by the user.</span></span> <span data-ttu-id="816a2-120">따라서 추가 라이선스에 대해 마이그레이션을 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-120">Hence no additional licenses are required to perform migration.</span></span>

5. <span data-ttu-id="816a2-121">오류 상태의 사용자가 있는지 각 그룹을 확인하여 실패한 라이선스 할당이 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-121">Verify that no license assignments failed by checking each group for users in error state.</span></span> <span data-ttu-id="816a2-122">자세한 내용은 [그룹에 대한 라이선스 문제 식별 및 해결](active-directory-licensing-group-problem-resolution-azure-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="816a2-122">For more information, see [Identifying and resolving license problems for a group](active-directory-licensing-group-problem-resolution-azure-portal.md).</span></span>

6. <span data-ttu-id="816a2-123">원래의 직접 할당을 제거하는 것을 고려합니다. 이러한 작업을 점차적으로 “단계별”로 진행하면서 사용자의 일부에 대한 결과를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-123">Consider removing the original direct assignments; you may want to do it gradually, in “waves”, to monitor the outcome on a subset of users first.</span></span>

  <span data-ttu-id="816a2-124">사용자에 대한 원래의 직접 할당을 그대로 둘 수 있지만 사용자가 라이선스 그룹을 나가게 되어도 원래 라이선스가 계속 유지되며 이러한 상황을 원치 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-124">You could leave the original direct assignments on users, but when the users leave their licensed groups they will still retain the original license, which is possibly not want you want.</span></span>

## <a name="an-example"></a><span data-ttu-id="816a2-125">예제</span><span class="sxs-lookup"><span data-stu-id="816a2-125">An example</span></span>

<span data-ttu-id="816a2-126">우리 조직에는 1000명의 사용자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-126">We have an organization with 1,000 users.</span></span> <span data-ttu-id="816a2-127">모든 사용자에게는 EMS(Enterprise Mobility + Security) 라이선스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-127">All users require Enterprise Mobility + Security (EMS) licenses.</span></span> <span data-ttu-id="816a2-128">200명의 사용자는 재무 부서에 속하며 Office 365 Enterprise E3 라이선스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-128">200 users are in the Finance Department and require Office 365 Enterprise E3 licenses.</span></span> <span data-ttu-id="816a2-129">온-프레미스에서 PowerShell 스크립트가 실행되고 있으며 사용자가 들어오고 나갈 때 라이선스를 추가 및 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-129">We have a PowerShell script running on premises adding and removing licenses from users as they come and go.</span></span> <span data-ttu-id="816a2-130">이 스크립트를 그룹 기반 라이선스로 바꾸어 Azure AD에서 라이선스를 자동으로 관리하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-130">We want to replace the script with group-based licensing so licenses are managed automatically by Azure AD.</span></span>

<span data-ttu-id="816a2-131">마이그레이션 프로세스는 다음과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-131">Here is what the migration process could look like:</span></span>

1. <span data-ttu-id="816a2-132">Azure Portal을 사용하여 Azure AD의 **모든 사용자** 그룹에 EMS 라이선스를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-132">Using the Azure portal assign the EMS license to the **All users** group in Azure AD.</span></span> <span data-ttu-id="816a2-133">모든 필수 사용자가 포함된 **재무 부서** 그룹에 E3 라이선스를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-133">Assign the E3 license to the **Finance department** group that contains all the required users.</span></span>

2. <span data-ttu-id="816a2-134">각 그룹의 모든 사용자에 대한 라이선스 할당이 완료되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-134">For each group, confirm that license assignment has completed for all users.</span></span> <span data-ttu-id="816a2-135">각 그룹에 대한 블레이드로 이동하고 **라이선스**를 선택한 후 **라이선스** 블레이드 맨 위에서 처리 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-135">Go to the blade for each group, select **Licenses**, and check the processing status at the top of the **Licenses** blade.</span></span>

  - <span data-ttu-id="816a2-136">처리가 완료되었으면 "최신 라이선스 변경 내용이 모든 사용자에게 할당됨"이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-136">Look for “Latest license changes have been applied to all users" to confirm processing has completed.</span></span>

  - <span data-ttu-id="816a2-137">해당 사용자의 라이선스가 성공적으로 할당되지 않았을 수 있다는 알림은 위쪽에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-137">Look for a notification on top about any users for whom licenses may have not been successfully assigned.</span></span> <span data-ttu-id="816a2-138">일부 사용자의 라이선스가 부족한가요?</span><span class="sxs-lookup"><span data-stu-id="816a2-138">Did we run out of licenses for some users?</span></span> <span data-ttu-id="816a2-139">일부 사용자에게 충돌하는 라이선스 SKU가 할당되어 상속 그룹이 라이선스를 할당하지 못하나요?</span><span class="sxs-lookup"><span data-stu-id="816a2-139">Do some users have conflicting license SKUs that prevent them from inheriting group licenses?</span></span>

3. <span data-ttu-id="816a2-140">일부 사용자를 검토하여 직접 및 그룹 라이선스가 모두 할당되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-140">Spot check some users to verify that they have both the direct and group licenses applied.</span></span> <span data-ttu-id="816a2-141">사용자에 대한 블레이드로 이동한 후 **라이선스**를 선택하고 라이선스 상태를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-141">Go to the blade for a user, select **Licenses**, and examine the state of licenses.</span></span>

  - <span data-ttu-id="816a2-142">다음은 마이그레이션 중에 예상되는 사용자 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-142">This is the expected user state during migration:</span></span>

      ![예상되는 사용자 상태](media/active-directory-licensing-group-migration-azure-portal/expected-user-state.png)

  <span data-ttu-id="816a2-144">이 경우 사용자에게 직접 및 상속된 라이선스가 모두 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-144">This confirms that the user has both direct and inherited licenses.</span></span> <span data-ttu-id="816a2-145">**EMS** 및 **E3**가 둘 다 할당되어 있는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-145">We see that both **EMS** and **E3** are assigned.</span></span>

  - <span data-ttu-id="816a2-146">각 라이선스를 선택하여 사용하도록 설정된 서비스에 대한 세부 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-146">Select each license to show details about the enabled services.</span></span> <span data-ttu-id="816a2-147">이를 통해 직접 및 그룹 라이선스가 해당 사용자의 정확히 동일한 서비스 계획을 사용하도록 설정하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-147">This can be used to check if the direct and group licenses enable exactly the same service plans for the user.</span></span>

      ![서비스 계획 확인](media/active-directory-licensing-group-migration-azure-portal/check-service-plans.png)

4. <span data-ttu-id="816a2-149">직접 및 그룹 라이선스가 동일한 것인지 확인한 후에 사용자에게서 직접 라이선스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-149">After confirming that both direct and group licenses are equivalent, you can start removing direct licenses from users.</span></span> <span data-ttu-id="816a2-150">포털에 있는 개별 사용자에게서 라이선스를 제거하여 테스트한 다음 자동화 스크립트를 실행하여 대량으로 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-150">You can test this by removing them for individual users in the portal and then run automation scripts to have them removed in bulk.</span></span> <span data-ttu-id="816a2-151">포털을 통해 같은 사용자에게서 직접 라이선스를 제거하는 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-151">Here is an example of the same user with the direct licenses removed through the portal.</span></span> <span data-ttu-id="816a2-152">라이선스 상태는 변경되지 않지만 직접 할당은 더 이상 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="816a2-152">Notice that the license state remains unchanged, but we no longer see direct assignments.</span></span>

  ![직접 라이선스 제거](media/active-directory-licensing-group-migration-azure-portal/direct-licenses-removed.png)


## <a name="next-steps"></a><span data-ttu-id="816a2-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="816a2-154">Next steps</span></span>

<span data-ttu-id="816a2-155">그룹을 통한 라이선스 관리에 대한 기타 시나리오에 대해 자세히 알아보려면 이 문서를 읽어 보세요.</span><span class="sxs-lookup"><span data-stu-id="816a2-155">To learn more about other scenarios for license management through groups, read</span></span>

* [<span data-ttu-id="816a2-156">Azure Active Directory에서 그룹에 라이선스 할당</span><span class="sxs-lookup"><span data-stu-id="816a2-156">Assigning licenses to a group in Azure Active Directory</span></span>](active-directory-licensing-group-assignment-azure-portal.md)
* [<span data-ttu-id="816a2-157">Azure Active Directory의 그룹 기반 라이선스란?</span><span class="sxs-lookup"><span data-stu-id="816a2-157">What is group-based licensing in Azure Active Directory?</span></span>](active-directory-licensing-whatis-azure-portal.md)
* [<span data-ttu-id="816a2-158">Azure Active Directory에서 그룹에 대한 라이선스 문제 식별 및 해결</span><span class="sxs-lookup"><span data-stu-id="816a2-158">Identifying and resolving license problems for a group in Azure Active Directory</span></span>](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [<span data-ttu-id="816a2-159">Azure Active Directory 그룹 기반 라이선스 추가 시나리오</span><span class="sxs-lookup"><span data-stu-id="816a2-159">Azure Active Directory group-based licensing additional scenarios</span></span>](active-directory-licensing-group-advanced.md)
