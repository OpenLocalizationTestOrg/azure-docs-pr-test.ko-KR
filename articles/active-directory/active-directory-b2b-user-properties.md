---
title: "Azure Active Directory B2B 공동 작업 사용자 속성 | Microsoft Docs"
description: "Azure Active Directory B2B 공동 작업 사용자 속성은 구성 가능합니다."
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/25/2017
ms.author: sasubram
ms.openlocfilehash: 6e49cb202ed03bf50fb9ca34d34924cda434829c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="properties-of-an-azure-active-directory-b2b-collaboration-user"></a><span data-ttu-id="7548a-103">Azure Active Directory B2B 공동 작업 사용자 속성</span><span class="sxs-lookup"><span data-stu-id="7548a-103">Properties of an Azure Active Directory B2B collaboration user</span></span>

<span data-ttu-id="7548a-104">Azure AD(Azure Active Directory) B2B 공동 작업 사용자는 UserType이 Guest인 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-104">An Azure Active Directory (Azure AD) business-to-business (B2B) collaboration user is a user with UserType = Guest.</span></span> <span data-ttu-id="7548a-105">이 게스트 사용자는 일반적으로 파트너 조직에 소속되어 있으며, 기본적으로 초대 디렉터리에서 제한된 권한을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-105">This guest user typically is from a partner organization and has limited privileges in the inviting directory, by default.</span></span>

<span data-ttu-id="7548a-106">초대 조직의 요구에 따라 Azure AD B2B 공동 작업 사용자는 다음 계정 상태 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-106">Depending on the inviting organization's needs, an Azure AD B2B collaboration user can be in one of the following account states:</span></span>

- <span data-ttu-id="7548a-107">상태 1: Azure AD의 외부 인스턴스에 속하며 초대하는 조직의 게스트 사용자로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-107">State 1: Homed in an external instance of Azure AD and represented as a guest user in the inviting organization.</span></span> <span data-ttu-id="7548a-108">이 경우 B2B 사용자는 초대된 테넌트에 속한 Azure AD 계정을 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-108">In this case, the B2B user signs in by using an Azure AD account that belongs to the invited tenant.</span></span> <span data-ttu-id="7548a-109">파트너 조직이 Azure AD를 사용하지 않는 경우에도 Azure AD에서 게스트 사용자는 여전히 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-109">If the partner organization doesn't use Azure AD, the guest user in Azure AD is still created.</span></span> <span data-ttu-id="7548a-110">단, 본인의 초대를 사용해야 합니다. Azure AD에서는 해당 사용자의 전자 메일 주소를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-110">The requirements are that they redeem their invitation and Azure AD verifies their email address.</span></span> <span data-ttu-id="7548a-111">이것을 JIT(Just In Time) 테넌트 또는 “바이럴” 테넌트라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-111">This arrangement is also called a just-in-time (JIT) tenancy or a "viral" tenancy.</span></span>

- <span data-ttu-id="7548a-112">상태 2: Microsoft 계정에 속하고 호스트 조직의 게스트 사용자로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-112">State 2: Homed in a Microsoft account and represented as a guest user in the host organization.</span></span> <span data-ttu-id="7548a-113">이 경우 게스트 사용자는 Microsoft 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-113">In this case, the guest user signs in with a Microsoft account.</span></span> <span data-ttu-id="7548a-114">제안 상환 중에 초대된 사용자의 비 Microsoft 소셜 ID(google.com 또는 유사한 ID)가 Microsoft 계정으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-114">The invited user's social identity (google.com or similar), which is not a Microsoft account, is created as a Microsoft account during offer redemption.</span></span>

- <span data-ttu-id="7548a-115">상태 3: 호스트 조직의 온-프레미스 Active Directory에 속하며 호스트 조직의 Azure AD와 동기화와 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-115">State 3: Homed in the host organization's on-premises Active Directory and synced with the host organization's Azure AD.</span></span> <span data-ttu-id="7548a-116">이 릴리스에서는 PowerShell을 사용하여 수동으로 클라우드에 있는 이러한 사용자의 UserType을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-116">During this release, you must use PowerShell to manually change the UserType of such users in the cloud.</span></span>

- <span data-ttu-id="7548a-117">상태 4: UserType이 Guest이고 호스트 조직에서 관리하는 자격 증명을 사용하는 호스트 조직의 Azure AD에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-117">State 4: Homed in host organization's Azure AD with UserType = Guest and credentials that the host organization manages.</span></span>

  ![초대자의 이니셜 표시](media/active-directory-b2b-user-properties/redemption-diagram.png)


<span data-ttu-id="7548a-119">이제 Azure AD에서 상태 1의 Azure AD B2B 공동 작업 사용자가 어떻게 보이는지 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-119">Now, let's see what an Azure AD B2B collaboration user in State 1 looks like in Azure AD.</span></span>

### <a name="before-invitation-redemption"></a><span data-ttu-id="7548a-120">초대 상환 전</span><span class="sxs-lookup"><span data-stu-id="7548a-120">Before invitation redemption</span></span>

![제안 상환 전](media/active-directory-b2b-user-properties/before-redemption.png)

### <a name="after-invitation-redemption"></a><span data-ttu-id="7548a-122">초대 상환 후</span><span class="sxs-lookup"><span data-stu-id="7548a-122">After invitation redemption</span></span>

![제안 상환 후](media/active-directory-b2b-user-properties/after-redemption.png)

## <a name="key-properties-of-the-azure-ad-b2b-collaboration-user"></a><span data-ttu-id="7548a-124">Azure AD B2B 공동 작업 사용자의 주요 속성</span><span class="sxs-lookup"><span data-stu-id="7548a-124">Key properties of the Azure AD B2B collaboration user</span></span>
### <a name="usertype"></a><span data-ttu-id="7548a-125">UserType</span><span class="sxs-lookup"><span data-stu-id="7548a-125">UserType</span></span>
<span data-ttu-id="7548a-126">이 속성은 사용자와 호스트 테넌트 사이의 관계를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-126">This property indicates the relationship of the user to the host tenancy.</span></span> <span data-ttu-id="7548a-127">이 속성에는 다음 두 가지 값이 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-127">This property can have two values:</span></span>
- <span data-ttu-id="7548a-128">구성원: 이 값은 호스트 조직의 직원과 조직의 급여 부서에 있는 사용자를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-128">Member: This value indicates an employee of the host organization and a user in the organization's payroll.</span></span> <span data-ttu-id="7548a-129">예를 들어 이 사용자는 내부 전용 사이트에 대한 액세스 권한을 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-129">For example, this user expects to have access to internal-only sites.</span></span> <span data-ttu-id="7548a-130">이 사용자는 외부 공동 작업자로 간주되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-130">This user would not be considered an external collaborator.</span></span>

- <span data-ttu-id="7548a-131">게스트: 이 값은 회사의 내부인으로 간주되지 않는 사용자(예: 외부 공동 작업자, 파트너, 고객 또는 유사한 사용자)를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-131">Guest: This value indicates a user who isn't considered internal to the company, such as an external collaborator, partner, customer, or similar user.</span></span> <span data-ttu-id="7548a-132">이러한 사용자는 CEO의 내부 메모를 수신하거나 회사 혜택을 받을 것으로 예상되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-132">Such a user wouldn't be expected to receive a CEO's internal memo, or receive company benefits, for example.</span></span>

  > [!NOTE]
  > <span data-ttu-id="7548a-133">UserType은 사용자가 로그인하는 방법, 사용자의 디렉터리 역할 등과 관계가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-133">The UserType has no relation to how the user signs in, the directory role of the user, and so on.</span></span> <span data-ttu-id="7548a-134">이 속성은 단순히 사용자와 호스트 조직 사이의 관계를 나타내며, 조직에서 이 속성에 속한 모든 정책을 시행할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-134">This property simply indicates the user's relationship to the host organization and allows the organization to enforce policies that depend on this property.</span></span>

### <a name="source"></a><span data-ttu-id="7548a-135">원본</span><span class="sxs-lookup"><span data-stu-id="7548a-135">Source</span></span>
<span data-ttu-id="7548a-136">이 속성은 사용자가 로그인하는 방법을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-136">This property indicates how the user signs in.</span></span>

- <span data-ttu-id="7548a-137">초대된 사용자: 이 사용자는 초대되었지만 초대를 아직 상환하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-137">Invited User: This user has been invited but has not yet redeemed an invitation.</span></span>

- <span data-ttu-id="7548a-138">외부 Active Directory: 이 사용자는 외부 조직에 속하며 다른 조직에 속한 Azure AD 계정을 사용하여 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-138">External Active Directory: This user is homed in an external organization and authenticates by using an Azure AD account that belongs to the other organization.</span></span> <span data-ttu-id="7548a-139">이 유형의 로그인은 상태 1에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-139">This type of sign-in corresponds to State 1.</span></span>

- <span data-ttu-id="7548a-140">Microsoft 계정: 이 사용자는 Microsoft 계정에 속하며 Microsoft 계정을 사용하여 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-140">Microsoft account: This user is homed in a Microsoft account and authenticates by using a Microsoft account.</span></span> <span data-ttu-id="7548a-141">이 유형의 로그인은 상태 2에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-141">This type of sign-in corresponds to State 2.</span></span>

- <span data-ttu-id="7548a-142">Windows Server Active Directory: 이 사용자는 이 조직에 속한 온-프레미스 Active Directory에서 로그인됩니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-142">Windows Server Active Directory: This user is signed in from on-premises Active Directory that belongs to this organization.</span></span> <span data-ttu-id="7548a-143">이 유형의 로그인은 상태 3에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-143">This type of sign-in corresponds to State 3.</span></span>

- <span data-ttu-id="7548a-144">Azure Active Directory: 이 사용자는 이 조직에 속한 Azure AD 계정을 사용하여 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-144">Azure Active Directory: This user authenticates by using an Azure AD account that belongs to this organization.</span></span> <span data-ttu-id="7548a-145">이 유형의 로그인은 상태 4에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-145">This type of sign-in corresponds to State 4.</span></span>
  > [!NOTE]
  > <span data-ttu-id="7548a-146">Source와 UserType은 독립적인 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-146">Source and UserType are independent properties.</span></span> <span data-ttu-id="7548a-147">Source의 값은 UserType에 대한 특정 값을 의미하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-147">A value of Source does not imply a particular value for UserType.</span></span>

## <a name="can-azure-ad-b2b-users-be-added-as-members-instead-of-guests"></a><span data-ttu-id="7548a-148">Azure AD B2B 사용자를 게스트 대신 구성원으로 추가할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="7548a-148">Can Azure AD B2B users be added as members instead of guests?</span></span>
<span data-ttu-id="7548a-149">일반적으로 Azure AD B2B 사용자와 게스트 사용자는 동의어입니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-149">Typically, an Azure AD B2B user and guest user are synonymous.</span></span> <span data-ttu-id="7548a-150">따라서 Azure AD B2B 공동 작업 사용자는 기본적으로 UserType = Guest인 사용자로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-150">Therefore, an Azure AD B2B collaboration user is added as a user with UserType = Guest by default.</span></span> <span data-ttu-id="7548a-151">그러나 경우에 따라 파트너 조직은 호스트 조직이 속한 더 큰 조직의 구성원일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-151">However, in some cases, the partner organization is a member of a larger organization to which the host organization also belongs.</span></span> <span data-ttu-id="7548a-152">만약 그렇다면 호스트 조직에서 파트너 조직의 사용자를 게스트가 아닌 구성원으로 처리하려 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-152">If so, the host organization might want to treat users in the partner organization as members instead of guests.</span></span> <span data-ttu-id="7548a-153">Azure AD B2B 초대 관리자 API를 사용하여 호스트 조직에 파트너 조직의 사용자를 구성원으로 추가하거나 초대합니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-153">Use the Azure AD B2B Invitation Manager APIs to add or invite a user from the partner organization to the host organization as a member.</span></span>

## <a name="filter-for-guest-users-in-the-directory"></a><span data-ttu-id="7548a-154">디렉터리의 게스트 사용자 필터링</span><span class="sxs-lookup"><span data-stu-id="7548a-154">Filter for guest users in the directory</span></span>

![게스트 사용자 필터링](media/active-directory-b2b-user-properties/filter-guest-users.png)

## <a name="convert-usertype"></a><span data-ttu-id="7548a-156">UserType 변환</span><span class="sxs-lookup"><span data-stu-id="7548a-156">Convert UserType</span></span>
<span data-ttu-id="7548a-157">현재 사용자는 PowerShell을 사용하여 UserType을 Member에서 Guest로 또는 그 반대로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-157">Currently, it is possible for users to convert UserType from Member to Guest and vice-versa by using PowerShell.</span></span> <span data-ttu-id="7548a-158">그러나 UserType 속성은 사용자와 조직 사이의 관계를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-158">However, the UserType property is supposed to represent the user's relationship to the organization.</span></span> <span data-ttu-id="7548a-159">따라서 이 속성의 값은 사용자와 조직의 관계가 변할 때에만 변해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-159">Therefore, the value of this property should change only if the relationship of the user to the organization changes.</span></span> <span data-ttu-id="7548a-160">사용자의 관계가 변경되면 UPN(사용자 계정 이름)을 변경해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="7548a-160">If the relationship of the user changes, should issues, like whether the user principal name (UPN) should change, be addressed?</span></span> <span data-ttu-id="7548a-161">사용자가 같은 리소스에 대한 액세스 권한을 계속 가져야 합니까?</span><span class="sxs-lookup"><span data-stu-id="7548a-161">Should the user continue to have access to the same resources?</span></span> <span data-ttu-id="7548a-162">사서함을 할당해야 합니까?와 같은 다른 질문에 답변해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-162">Should a mailbox be assigned?</span></span> <span data-ttu-id="7548a-163">따라서 PowerShell을 사용하여 UserType을 원자성 작업으로 변경하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-163">Therefore, we do not recommend changing the UserType by using PowerShell as an atomic activity.</span></span> <span data-ttu-id="7548a-164">뿐만 아니라 PowerShell을 사용하여 이 속성을 변경 불가능으로 만드는 경우 이 값에 의존하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-164">In addition, in case this property becomes immutable by using PowerShell, we do not recommend taking a dependency on this value.</span></span>

## <a name="remove-guest-user-limitations"></a><span data-ttu-id="7548a-165">게스트 사용자 제한 제거</span><span class="sxs-lookup"><span data-stu-id="7548a-165">Remove guest user limitations</span></span>
<span data-ttu-id="7548a-166">게스트 사용자에게 더 높은 권한을 부여하려는 경우가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-166">There may be cases where you want to give your guest users higher privileges.</span></span> <span data-ttu-id="7548a-167">게스트 사용자를 모든 역할에 추가하고 디렉터리에서 기본 게스트 사용자 제한을 제거하여 사용자에게 구성원과 동일한 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-167">You can add a guest user to any role and even remove the default guest user restrictions in the directory to give a user the same privileges as members.</span></span>

<span data-ttu-id="7548a-168">기본 게스트 사용자 제한을 해제하여 회사 디렉터리의 게스트 사용자에게 구성원과 동일한 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7548a-168">It is possible to turn off the default guest user limitations so that a guest user in the company directory is given the same permissions as a member user.</span></span>

![게스트 사용자 제한 제거](media/active-directory-b2b-user-properties/remove-guest-limitations.png)

## <a name="next-steps"></a><span data-ttu-id="7548a-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7548a-170">Next steps</span></span>

<span data-ttu-id="7548a-171">Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:</span><span class="sxs-lookup"><span data-stu-id="7548a-171">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="7548a-172">Azure AD B2B 공동 작업이란?</span><span class="sxs-lookup"><span data-stu-id="7548a-172">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="7548a-173">역할에 B2B 공동 작업 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="7548a-173">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="7548a-174">B2B 공동 작업 초대 위임</span><span class="sxs-lookup"><span data-stu-id="7548a-174">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="7548a-175">B2B 공동 작업 사용자 감사 및 보고</span><span class="sxs-lookup"><span data-stu-id="7548a-175">B2B collaboration user auditing and reporting</span></span>](active-directory-b2b-auditing-and-reporting.md)
* [<span data-ttu-id="7548a-176">동적 그룹 및 B2B 공동 작업</span><span class="sxs-lookup"><span data-stu-id="7548a-176">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="7548a-177">B2B 공동 작업 코드 및 PowerShell 샘플</span><span class="sxs-lookup"><span data-stu-id="7548a-177">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="7548a-178">B2B 공동 작업을 위한 SaaS 앱 구성</span><span class="sxs-lookup"><span data-stu-id="7548a-178">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="7548a-179">B2B 공동 작업 사용자 토큰</span><span class="sxs-lookup"><span data-stu-id="7548a-179">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="7548a-180">B2B 공동 작업 사용자 클레임 매핑</span><span class="sxs-lookup"><span data-stu-id="7548a-180">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="7548a-181">Office 365 외부 공유</span><span class="sxs-lookup"><span data-stu-id="7548a-181">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="7548a-182">B2B 공동 작업 현재 제한</span><span class="sxs-lookup"><span data-stu-id="7548a-182">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
