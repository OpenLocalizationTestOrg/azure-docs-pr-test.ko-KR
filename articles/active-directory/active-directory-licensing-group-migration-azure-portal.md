---
title: "Azure Active Directory에서 그룹 사용이 허가 된 사용자가 개별 tooa aaaHow toomigrate | Microsoft Docs"
description: "개별 사용자 로부터 tooswitch toogroup 기반 Azure Active Directory를 사용 하 여 라이선스 라이센스 있음을"
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
ms.openlocfilehash: 25e5c760b7e632ba71edde10d937fe580aa6ed35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-licensed-users-tooa-group-for-licensing-in-azure-active-directory"></a><span data-ttu-id="52792-104">Azure Active Directory에서 라이선스에 대 한 tooadd 사용자 tooa 그룹 사용이 허가 된 방법</span><span class="sxs-lookup"><span data-stu-id="52792-104">How tooadd licensed users tooa group for licensing in Azure Active Directory</span></span>

<span data-ttu-id="52792-105">"직접 할당"; 통해 hello 조직에서 기존 배포 라이선스 toousers를 할 수 있습니다. 즉, PowerShell 스크립트 또는 기타 도구 tooassign 개별 사용자 라이선스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="52792-105">You may have existing licenses deployed toousers in hello organizations via “direct assignment”; that is, using PowerShell scripts or other tools tooassign individual user licenses.</span></span> <span data-ttu-id="52792-106">마이그레이션 할 toostart 조직에서 그룹 기반의 라이선스 toomanage 라이선스를 사용 하 여 원하는 경우 계획 tooseamlessly 라이선스 그룹을 기반으로 기존 솔루션을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="52792-106">If you would like toostart using group-based licensing toomanage licenses in your organization, you will need a migration plan tooseamlessly replace existing solutions with group-based licensing.</span></span>

<span data-ttu-id="52792-107">hello 가장 중요 한 사항은 tookeep에 주의 하 여 현재 할당 된 라이선스를 일시적으로 손실 되는 사용자가 마이그레이션 toogroup 기반 라이선스 발생 합니다는 상황을 피해 야 한다는입니다.</span><span class="sxs-lookup"><span data-stu-id="52792-107">hello most important thing tookeep in mind is that you should avoid a situation where migrating toogroup-based licensing will result in users temporarily losing their currently assigned licenses.</span></span> <span data-ttu-id="52792-108">라이선스 제거 될 수 있는 모든 프로세스를 수행할 수 및 액세스 tooservices과 데이터를 손실 하는 사용자의 tooremove hello 위험을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52792-108">Any process that may result in removal of licenses should be avoided tooremove hello risk of users losing access tooservices and their data.</span></span>

## <a name="recommended-migration-process"></a><span data-ttu-id="52792-109">권장 마이그레이션 프로세스</span><span class="sxs-lookup"><span data-stu-id="52792-109">Recommended migration process</span></span>

1. <span data-ttu-id="52792-110">사용자에 대한 라이선스 할당 및 제거를 관리하는 기존 자동화(예: PowerShell) 기능이 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="52792-110">You have existing automation (for example, PowerShell) managing license assignment and removal for users.</span></span> <span data-ttu-id="52792-111">이러한 기능은 실행 상태로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="52792-111">Leave it running as is.</span></span>

2. <span data-ttu-id="52792-112">새 라이선스 그룹 만들기 (또는 toouse 그룹화 기존 결정) 하 고 필요한 모든 사용자가 구성원으로 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="52792-112">Create a new licensing group (or decide which existing groups toouse) and make sure that all required users are added as members.</span></span>

3. <span data-ttu-id="52792-113">Toothose 그룹; hello 필요한 라이선스를 할당 합니다. 여기서의 목표 tooreflect hello 있어야 합니다. 라이선스 상태 같은 기존 자동화 (예를 들어 PowerShell) 적용 하는 toothose 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="52792-113">Assign hello required licenses toothose groups; your goal should be tooreflect hello same licensing state your existing automation (for example, PowerShell) is applying toothose users.</span></span>

4. <span data-ttu-id="52792-114">라이선스 그룹에 적용 된 tooall 사용자 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="52792-114">Verify that licenses have been applied tooall users in those groups.</span></span> <span data-ttu-id="52792-115">각 그룹에 대해 hello 처리 상태를 확인 하 여 및 감사 로그를 확인 하 여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52792-115">This can be done by checking hello processing state on each group and by checking Audit Logs.</span></span>

  - <span data-ttu-id="52792-116">라이선스 세부 정보를 확인하여 개별 사용자를 부분적으로 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52792-116">You can spot check individual users by looking at their license details.</span></span> <span data-ttu-id="52792-117">그룹에서 동일한 라이선스가 할당 "직접" 및 "상속" hello가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="52792-117">You will see that they have hello same licenses assigned “directly” and “inherited” from groups.</span></span>

  - <span data-ttu-id="52792-118">너무 PowerShell 스크립트를 실행할 수[라이선스 toousers 할당 하는 방법을 확인](active-directory-licensing-group-advanced.md#use-powershell-to-see-who-has-inherited-and-direct-licenses)합니다.</span><span class="sxs-lookup"><span data-stu-id="52792-118">You can run a PowerShell script too[verify how licenses are assigned toousers](active-directory-licensing-group-advanced.md#use-powershell-to-see-who-has-inherited-and-direct-licenses).</span></span>

  - <span data-ttu-id="52792-119">Hello 동일한 제품 라이선스 할당 하면 toohello 사용자 직접적으로 그리고 그룹을 통해, 하나의 라이선스 hello 사용자가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="52792-119">When hello same product license is assigned toohello user both directly and through a group, only one license is consumed by hello user.</span></span> <span data-ttu-id="52792-120">따라서 추가 라이선스가 없습니다. 필요한 tooperform 마이그레이션 됩니다.</span><span class="sxs-lookup"><span data-stu-id="52792-120">Hence no additional licenses are required tooperform migration.</span></span>

5. <span data-ttu-id="52792-121">오류 상태의 사용자가 있는지 각 그룹을 확인하여 실패한 라이선스 할당이 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="52792-121">Verify that no license assignments failed by checking each group for users in error state.</span></span> <span data-ttu-id="52792-122">자세한 내용은 [그룹에 대한 라이선스 문제 식별 및 해결](active-directory-licensing-group-problem-resolution-azure-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="52792-122">For more information, see [Identifying and resolving license problems for a group](active-directory-licensing-group-problem-resolution-azure-portal.md).</span></span>

6. <span data-ttu-id="52792-123">Hello 원래 직접 할당; 제거 하는 것이 좋습니다. toodo 경우가 사용자의 하위 집합에서의 결과 먼저 hello toomonitor "물결"에서 점차적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="52792-123">Consider removing hello original direct assignments; you may want toodo it gradually, in “waves”, toomonitor hello outcome on a subset of users first.</span></span>

  <span data-ttu-id="52792-124">사용자에서는 원래 직접 할당 hello를 발생할 수 있습니다 하지만 hello 사용자가 해당 사용 허가 받은 그룹을 여전히 유지를 떠날 때 되 hello 원래 라이선스 원하지 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="52792-124">You could leave hello original direct assignments on users, but when hello users leave their licensed groups they will still retain hello original license, which is possibly not want you want.</span></span>

## <a name="an-example"></a><span data-ttu-id="52792-125">예제</span><span class="sxs-lookup"><span data-stu-id="52792-125">An example</span></span>

<span data-ttu-id="52792-126">우리 조직에는 1000명의 사용자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52792-126">We have an organization with 1,000 users.</span></span> <span data-ttu-id="52792-127">모든 사용자에게는 EMS(Enterprise Mobility + Security) 라이선스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="52792-127">All users require Enterprise Mobility + Security (EMS) licenses.</span></span> <span data-ttu-id="52792-128">200 명 hello 재무 부서에에서 있으며 Office 365 Enterprise E3 라이선스가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="52792-128">200 users are in hello Finance Department and require Office 365 Enterprise E3 licenses.</span></span> <span data-ttu-id="52792-129">온-프레미스에서 PowerShell 스크립트가 실행되고 있으며 사용자가 들어오고 나갈 때 라이선스를 추가 및 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="52792-129">We have a PowerShell script running on premises adding and removing licenses from users as they come and go.</span></span> <span data-ttu-id="52792-130">Azure AD에서 라이선스가 자동으로 관리 하므로 그룹 기반 라이선스와 tooreplace hello 스크립트를 주시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="52792-130">We want tooreplace hello script with group-based licensing so licenses are managed automatically by Azure AD.</span></span>

<span data-ttu-id="52792-131">Hello 마이그레이션 프로세스 수 모양을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="52792-131">Here is what hello migration process could look like:</span></span>

1. <span data-ttu-id="52792-132">Azure 포털 할당 hello EMS 라이선스 toohello hello를 사용 하 여 **모든 사용자에 게** Azure AD의 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="52792-132">Using hello Azure portal assign hello EMS license toohello **All users** group in Azure AD.</span></span> <span data-ttu-id="52792-133">Hello E3 라이선스 toohello 할당 **재무 부서** 모든 hello 필요한 사용자가 포함 된 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="52792-133">Assign hello E3 license toohello **Finance department** group that contains all hello required users.</span></span>

2. <span data-ttu-id="52792-134">각 그룹의 모든 사용자에 대한 라이선스 할당이 완료되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="52792-134">For each group, confirm that license assignment has completed for all users.</span></span> <span data-ttu-id="52792-135">각 그룹에 대 한 이동 toohello 블레이드 **라이선스**, hello hello 맨 hello 처리 상태를 확인 하 고 **라이선스** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="52792-135">Go toohello blade for each group, select **Licenses**, and check hello processing status at hello top of hello **Licenses** blade.</span></span>

  - <span data-ttu-id="52792-136">찾을 tooconfirm "최신 라이선스 변경 내용이 적용 된 tooall 사용자 되었습니다 없음"에 대 한 처리가 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="52792-136">Look for “Latest license changes have been applied tooall users" tooconfirm processing has completed.</span></span>

  - <span data-ttu-id="52792-137">해당 사용자의 라이선스가 성공적으로 할당되지 않았을 수 있다는 알림은 위쪽에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="52792-137">Look for a notification on top about any users for whom licenses may have not been successfully assigned.</span></span> <span data-ttu-id="52792-138">일부 사용자의 라이선스가 부족한가요?</span><span class="sxs-lookup"><span data-stu-id="52792-138">Did we run out of licenses for some users?</span></span> <span data-ttu-id="52792-139">일부 사용자에게 충돌하는 라이선스 SKU가 할당되어 상속 그룹이 라이선스를 할당하지 못하나요?</span><span class="sxs-lookup"><span data-stu-id="52792-139">Do some users have conflicting license SKUs that prevent them from inheriting group licenses?</span></span>

3. <span data-ttu-id="52792-140">지점 직접 hello 및 적용 된 그룹 라이선스 모두 포함 하는 일부 사용자가 tooverify를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="52792-140">Spot check some users tooverify that they have both hello direct and group licenses applied.</span></span> <span data-ttu-id="52792-141">사용자가 선택 이동 toohello 블레이드 **라이선스**, 라이선스 hello 상태를 검사할 합니다.</span><span class="sxs-lookup"><span data-stu-id="52792-141">Go toohello blade for a user, select **Licenses**, and examine hello state of licenses.</span></span>

  - <span data-ttu-id="52792-142">마이그레이션 중 예상 hello 사용자 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="52792-142">This is hello expected user state during migration:</span></span>

      ![예상되는 사용자 상태](media/active-directory-licensing-group-migration-azure-portal/expected-user-state.png)

  <span data-ttu-id="52792-144">이 hello이 사용자는 직접 및 상속 된 라이선스를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="52792-144">This confirms that hello user has both direct and inherited licenses.</span></span> <span data-ttu-id="52792-145">**EMS** 및 **E3**가 둘 다 할당되어 있는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52792-145">We see that both **EMS** and **E3** are assigned.</span></span>

  - <span data-ttu-id="52792-146">사용 하도록 설정 하는 hello 서비스에 대 한 각 라이선스 tooshow 세부 정보를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="52792-146">Select each license tooshow details about hello enabled services.</span></span> <span data-ttu-id="52792-147">직접 hello 및 라이선스 사용 그룹 hello 사용자에 대 한 동일한 서비스 계획을 정확 하 게 hello 사용된 toocheck 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52792-147">This can be used toocheck if hello direct and group licenses enable exactly hello same service plans for hello user.</span></span>

      ![서비스 계획 확인](media/active-directory-licensing-group-migration-azure-portal/check-service-plans.png)

4. <span data-ttu-id="52792-149">직접 및 그룹 라이선스가 동일한 것인지 확인한 후에 사용자에게서 직접 라이선스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52792-149">After confirming that both direct and group licenses are equivalent, you can start removing direct licenses from users.</span></span> <span data-ttu-id="52792-150">Hello 포털에서 개별 사용자에 대 한 제거 하 여이 테스트 하 고 대량에서 제거 하는 자동화 스크립트 toohave를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52792-150">You can test this by removing them for individual users in hello portal and then run automation scripts toohave them removed in bulk.</span></span> <span data-ttu-id="52792-151">hello hello 직접 라이선스를 갖고 있는 동일한 사용자 hello 포털을 통해 제거 됩니다. 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="52792-151">Here is an example of hello same user with hello direct licenses removed through hello portal.</span></span> <span data-ttu-id="52792-152">필름 hello 라이선스 상태 그대로 되지만 직접 할당을 더 이상 참조 했습니다.</span><span class="sxs-lookup"><span data-stu-id="52792-152">Notice that hello license state remains unchanged, but we no longer see direct assignments.</span></span>

  ![직접 라이선스 제거](media/active-directory-licensing-group-migration-azure-portal/direct-licenses-removed.png)


## <a name="next-steps"></a><span data-ttu-id="52792-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="52792-154">Next steps</span></span>

<span data-ttu-id="52792-155">그룹을 통해 라이선스 관리에 대 한 다른 시나리오에 대해 자세히 toolearn 읽기</span><span class="sxs-lookup"><span data-stu-id="52792-155">toolearn more about other scenarios for license management through groups, read</span></span>

* [<span data-ttu-id="52792-156">Azure Active Directory에서 tooa 그룹 라이선스 할당</span><span class="sxs-lookup"><span data-stu-id="52792-156">Assigning licenses tooa group in Azure Active Directory</span></span>](active-directory-licensing-group-assignment-azure-portal.md)
* [<span data-ttu-id="52792-157">Azure Active Directory의 그룹 기반 라이선스란?</span><span class="sxs-lookup"><span data-stu-id="52792-157">What is group-based licensing in Azure Active Directory?</span></span>](active-directory-licensing-whatis-azure-portal.md)
* [<span data-ttu-id="52792-158">Azure Active Directory에서 그룹에 대한 라이선스 문제 식별 및 해결</span><span class="sxs-lookup"><span data-stu-id="52792-158">Identifying and resolving license problems for a group in Azure Active Directory</span></span>](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [<span data-ttu-id="52792-159">Azure Active Directory 그룹 기반 라이선스 추가 시나리오</span><span class="sxs-lookup"><span data-stu-id="52792-159">Azure Active Directory group-based licensing additional scenarios</span></span>](active-directory-licensing-group-advanced.md)
