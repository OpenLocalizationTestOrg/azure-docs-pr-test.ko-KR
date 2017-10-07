---
title: "Azure Active Directory B2B 공동 작업 사용자의 aaaProperties | Microsoft Docs"
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
ms.openlocfilehash: 78709f64430ed4c14eadf4dc257f175c24698c5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="properties-of-an-azure-active-directory-b2b-collaboration-user"></a><span data-ttu-id="ec1e3-103">Azure Active Directory B2B 공동 작업 사용자 속성</span><span class="sxs-lookup"><span data-stu-id="ec1e3-103">Properties of an Azure Active Directory B2B collaboration user</span></span>

<span data-ttu-id="ec1e3-104">Azure AD(Azure Active Directory) B2B 공동 작업 사용자는 UserType이 Guest인 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-104">An Azure Active Directory (Azure AD) business-to-business (B2B) collaboration user is a user with UserType = Guest.</span></span> <span data-ttu-id="ec1e3-105">이 게스트 사용자는 파트너 조직에서 일반적으로 되며 제한 된 hello 기본적으로 디렉터리를 초대에 권한을 갖는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-105">This guest user typically is from a partner organization and has limited privileges in hello inviting directory, by default.</span></span>

<span data-ttu-id="ec1e3-106">조직의 요구를 초대 hello에 따라 Azure AD B2B 공동 작업 사용자 hello 계정 상태를 다음 중 하나에 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-106">Depending on hello inviting organization's needs, an Azure AD B2B collaboration user can be in one of hello following account states:</span></span>

- <span data-ttu-id="ec1e3-107">상태 1: Azure AD의 인스턴스 외부에 이며 조직 초대 hello에서 게스트 사용자로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-107">State 1: Homed in an external instance of Azure AD and represented as a guest user in hello inviting organization.</span></span> <span data-ttu-id="ec1e3-108">이 경우 hello B2B 사용자 초대 toohello 테 넌 트에 속하는 Azure AD 계정을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-108">In this case, hello B2B user signs in by using an Azure AD account that belongs toohello invited tenant.</span></span> <span data-ttu-id="ec1e3-109">Hello 파트너 조직에서 Azure AD를 사용 하지 않는 경우 Azure AD에서 게스트 사용자 hello 여전히 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-109">If hello partner organization doesn't use Azure AD, hello guest user in Azure AD is still created.</span></span> <span data-ttu-id="ec1e3-110">hello 요건은 자신의 초대를 교환 하 고 Azure AD가 전자 메일 주소를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-110">hello requirements are that they redeem their invitation and Azure AD verifies their email address.</span></span> <span data-ttu-id="ec1e3-111">이것을 JIT(Just In Time) 테넌트 또는 “바이럴” 테넌트라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-111">This arrangement is also called a just-in-time (JIT) tenancy or a "viral" tenancy.</span></span>

- <span data-ttu-id="ec1e3-112">상태 2: Microsoft 계정에 속한 이며 hello 호스트 조직에서 게스트 사용자로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-112">State 2: Homed in a Microsoft account and represented as a guest user in hello host organization.</span></span> <span data-ttu-id="ec1e3-113">이 경우 hello 게스트 사용자가 Microsoft 계정으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-113">In this case, hello guest user signs in with a Microsoft account.</span></span> <span data-ttu-id="ec1e3-114">hello 초대 사용자의 소셜 id (google.com 또는 유사한 곳), 상환 제공 하는 동안 Microsoft 계정으로 만들어집니다 Microsoft 계정 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-114">hello invited user's social identity (google.com or similar), which is not a Microsoft account, is created as a Microsoft account during offer redemption.</span></span>

- <span data-ttu-id="ec1e3-115">상태 3: hello 호스트 조직 온-프레미스 Active Directory에 속한 및 동기화 hello 호스트 조직의 azure AD.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-115">State 3: Homed in hello host organization's on-premises Active Directory and synced with hello host organization's Azure AD.</span></span> <span data-ttu-id="ec1e3-116">이 버전에서는 PowerShell toomanually 변경 hello 이러한 사용자의 UserType hello 클라우드에서 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-116">During this release, you must use PowerShell toomanually change hello UserType of such users in hello cloud.</span></span>

- <span data-ttu-id="ec1e3-117">상태 4: Azure 호스트 조직에에서 속한 AD UserType와 = 게스트 및 hello 호스트 조직에서 관리 하는 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-117">State 4: Homed in host organization's Azure AD with UserType = Guest and credentials that hello host organization manages.</span></span>

  ![hello 초대자 이니셜을 표시합니다.](media/active-directory-b2b-user-properties/redemption-diagram.png)


<span data-ttu-id="ec1e3-119">이제 Azure AD에서 상태 1의 Azure AD B2B 공동 작업 사용자가 어떻게 보이는지 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-119">Now, let's see what an Azure AD B2B collaboration user in State 1 looks like in Azure AD.</span></span>

### <a name="before-invitation-redemption"></a><span data-ttu-id="ec1e3-120">초대 상환 전</span><span class="sxs-lookup"><span data-stu-id="ec1e3-120">Before invitation redemption</span></span>

![제안 상환 전](media/active-directory-b2b-user-properties/before-redemption.png)

### <a name="after-invitation-redemption"></a><span data-ttu-id="ec1e3-122">초대 상환 후</span><span class="sxs-lookup"><span data-stu-id="ec1e3-122">After invitation redemption</span></span>

![제안 상환 후](media/active-directory-b2b-user-properties/after-redemption.png)

## <a name="key-properties-of-hello-azure-ad-b2b-collaboration-user"></a><span data-ttu-id="ec1e3-124">Hello Azure AD B2B 공동 작업 사용자의 키 속성</span><span class="sxs-lookup"><span data-stu-id="ec1e3-124">Key properties of hello Azure AD B2B collaboration user</span></span>
### <a name="usertype"></a><span data-ttu-id="ec1e3-125">UserType</span><span class="sxs-lookup"><span data-stu-id="ec1e3-125">UserType</span></span>
<span data-ttu-id="ec1e3-126">이 속성의 테 넌 트 사용자 toohello 호스트 hello hello 관계를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-126">This property indicates hello relationship of hello user toohello host tenancy.</span></span> <span data-ttu-id="ec1e3-127">이 속성에는 다음 두 가지 값이 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-127">This property can have two values:</span></span>
- <span data-ttu-id="ec1e3-128">멤버:이 값의 hello 호스트 조직 직원 및 사용자 hello 조직의 급여에 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-128">Member: This value indicates an employee of hello host organization and a user in hello organization's payroll.</span></span> <span data-ttu-id="ec1e3-129">예를 들어이 사용자는 toohave 액세스 toointernal 전용 사이트 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-129">For example, this user expects toohave access toointernal-only sites.</span></span> <span data-ttu-id="ec1e3-130">이 사용자는 외부 공동 작업자로 간주되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-130">This user would not be considered an external collaborator.</span></span>

- <span data-ttu-id="ec1e3-131">게스트:이 값은 사용자가 내부 toohello 회사 외부 공동 작업자, 파트너, 고객 또는 유사한 사용자와 같은 것으로 간주 되지 않습니다 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-131">Guest: This value indicates a user who isn't considered internal toohello company, such as an external collaborator, partner, customer, or similar user.</span></span> <span data-ttu-id="ec1e3-132">이러한 사용자가 될 예상된 tooreceive CEO의 내부 메모, 또는 예를 들어 회사 혜택을 받을입니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-132">Such a user wouldn't be expected tooreceive a CEO's internal memo, or receive company benefits, for example.</span></span>

  > [!NOTE]
  > <span data-ttu-id="ec1e3-133">hello UserType 없고 관계 toohow hello 사용자가 로그인에, hello 사용자 및 등의 hello 디렉터리 역할에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-133">hello UserType has no relation toohow hello user signs in, hello directory role of hello user, and so on.</span></span> <span data-ttu-id="ec1e3-134">이 속성 단순히 hello 사용자의 관계 toohello 호스트 조직 나타내고이 속성에 종속 된 tooenforce 정책을 hello 조직을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-134">This property simply indicates hello user's relationship toohello host organization and allows hello organization tooenforce policies that depend on this property.</span></span>

### <a name="source"></a><span data-ttu-id="ec1e3-135">원본</span><span class="sxs-lookup"><span data-stu-id="ec1e3-135">Source</span></span>
<span data-ttu-id="ec1e3-136">이 속성은 hello 사용자가 로그인 하는 방법을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-136">This property indicates how hello user signs in.</span></span>

- <span data-ttu-id="ec1e3-137">초대된 사용자: 이 사용자는 초대되었지만 초대를 아직 상환하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-137">Invited User: This user has been invited but has not yet redeemed an invitation.</span></span>

- <span data-ttu-id="ec1e3-138">외부 Active Directory:이 사용자는 외부 조직에서 홈 고 다른 조직의 toohello에 속하는 Azure AD 계정을 사용 하 여 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-138">External Active Directory: This user is homed in an external organization and authenticates by using an Azure AD account that belongs toohello other organization.</span></span> <span data-ttu-id="ec1e3-139">이 유형의 로그인 tooState 1 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-139">This type of sign-in corresponds tooState 1.</span></span>

- <span data-ttu-id="ec1e3-140">Microsoft 계정: 이 사용자는 Microsoft 계정에 속하며 Microsoft 계정을 사용하여 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-140">Microsoft account: This user is homed in a Microsoft account and authenticates by using a Microsoft account.</span></span> <span data-ttu-id="ec1e3-141">이 유형의 로그인 tooState 2 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-141">This type of sign-in corresponds tooState 2.</span></span>

- <span data-ttu-id="ec1e3-142">Windows Server Active Directory:이 사용자가 로그인 toothis 조직 속한 온-프레미스 Active Directory에서.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-142">Windows Server Active Directory: This user is signed in from on-premises Active Directory that belongs toothis organization.</span></span> <span data-ttu-id="ec1e3-143">이 유형의 로그인 tooState 3은 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-143">This type of sign-in corresponds tooState 3.</span></span>

- <span data-ttu-id="ec1e3-144">Azure Active Directory: toothis 조직에 속하는 Azure AD 계정을 사용 하 여이 사용자를 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-144">Azure Active Directory: This user authenticates by using an Azure AD account that belongs toothis organization.</span></span> <span data-ttu-id="ec1e3-145">이 유형의 로그인 tooState 4 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-145">This type of sign-in corresponds tooState 4.</span></span>
  > [!NOTE]
  > <span data-ttu-id="ec1e3-146">Source와 UserType은 독립적인 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-146">Source and UserType are independent properties.</span></span> <span data-ttu-id="ec1e3-147">Source의 값은 UserType에 대한 특정 값을 의미하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-147">A value of Source does not imply a particular value for UserType.</span></span>

## <a name="can-azure-ad-b2b-users-be-added-as-members-instead-of-guests"></a><span data-ttu-id="ec1e3-148">Azure AD B2B 사용자를 게스트 대신 구성원으로 추가할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="ec1e3-148">Can Azure AD B2B users be added as members instead of guests?</span></span>
<span data-ttu-id="ec1e3-149">일반적으로 Azure AD B2B 사용자와 게스트 사용자는 동의어입니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-149">Typically, an Azure AD B2B user and guest user are synonymous.</span></span> <span data-ttu-id="ec1e3-150">따라서 Azure AD B2B 공동 작업 사용자는 기본적으로 UserType = Guest인 사용자로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-150">Therefore, an Azure AD B2B collaboration user is added as a user with UserType = Guest by default.</span></span> <span data-ttu-id="ec1e3-151">그러나 경우에 따라 hello 파트너 조직의 대규모 조직 toowhich hello 호스트 조직의 구성원도 속합니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-151">However, in some cases, hello partner organization is a member of a larger organization toowhich hello host organization also belongs.</span></span> <span data-ttu-id="ec1e3-152">이 경우 hello 호스트 조직은 tootreat 게스트 대신 멤버로 hello 파트너 조직의 사용자가 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-152">If so, hello host organization might want tootreat users in hello partner organization as members instead of guests.</span></span> <span data-ttu-id="ec1e3-153">Azure AD B2B 초대 관리자 Api tooadd hello를 사용 하 여 또는 멤버로 hello 파트너 조직 toohello 호스트 조직에서 사용자를 초대 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-153">Use hello Azure AD B2B Invitation Manager APIs tooadd or invite a user from hello partner organization toohello host organization as a member.</span></span>

## <a name="filter-for-guest-users-in-hello-directory"></a><span data-ttu-id="ec1e3-154">Hello 디렉터리의 게스트 사용자에 대 한 필터</span><span class="sxs-lookup"><span data-stu-id="ec1e3-154">Filter for guest users in hello directory</span></span>

![게스트 사용자 필터링](media/active-directory-b2b-user-properties/filter-guest-users.png)

## <a name="convert-usertype"></a><span data-ttu-id="ec1e3-156">UserType 변환</span><span class="sxs-lookup"><span data-stu-id="ec1e3-156">Convert UserType</span></span>
<span data-ttu-id="ec1e3-157">현재 있기 사용자 tooconvert UserType 멤버 tooGuest 그 반대로 줄에서 PowerShell을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-157">Currently, it is possible for users tooconvert UserType from Member tooGuest and vice-versa by using PowerShell.</span></span> <span data-ttu-id="ec1e3-158">그러나 hello UserType 속성 toorepresent hello 사용자의 관계 toohello 조직이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-158">However, hello UserType property is supposed toorepresent hello user's relationship toohello organization.</span></span> <span data-ttu-id="ec1e3-159">따라서이 속성의 값 hello hello 사용자 toohello 조직의 hello 관계가 변경 하는 경우에 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-159">Therefore, hello value of this property should change only if hello relationship of hello user toohello organization changes.</span></span> <span data-ttu-id="ec1e3-160">Hello 사용자의 hello 관계 변경 되 면 hello 사용자 계정 이름 (UPN) 변경 해야 하는지 여부와 같은 문제를 해결 해야?</span><span class="sxs-lookup"><span data-stu-id="ec1e3-160">If hello relationship of hello user changes, should issues, like whether hello user principal name (UPN) should change, be addressed?</span></span> <span data-ttu-id="ec1e3-161">Hello 사용자 toohave 액세스 toohello 계속 동일한 리소스?</span><span class="sxs-lookup"><span data-stu-id="ec1e3-161">Should hello user continue toohave access toohello same resources?</span></span> <span data-ttu-id="ec1e3-162">사서함을 할당해야 합니까?와 같은 다른 질문에 답변해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-162">Should a mailbox be assigned?</span></span> <span data-ttu-id="ec1e3-163">따라서 원자성 활동으로 PowerShell을 사용 하 여 hello UserType을 변경 하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-163">Therefore, we do not recommend changing hello UserType by using PowerShell as an atomic activity.</span></span> <span data-ttu-id="ec1e3-164">뿐만 아니라 PowerShell을 사용하여 이 속성을 변경 불가능으로 만드는 경우 이 값에 의존하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-164">In addition, in case this property becomes immutable by using PowerShell, we do not recommend taking a dependency on this value.</span></span>

## <a name="remove-guest-user-limitations"></a><span data-ttu-id="ec1e3-165">게스트 사용자 제한 제거</span><span class="sxs-lookup"><span data-stu-id="ec1e3-165">Remove guest user limitations</span></span>
<span data-ttu-id="ec1e3-166">사례 toogive 게스트 사용자가 더 높은 권한이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-166">There may be cases where you want toogive your guest users higher privileges.</span></span> <span data-ttu-id="ec1e3-167">게스트 사용자 tooany 역할을 추가 하 고도 hello 디렉터리 toogive에 hello 기본 게스트 사용자 제한을 구성원으로 권한을 동일 사용자 hello 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-167">You can add a guest user tooany role and even remove hello default guest user restrictions in hello directory toogive a user hello same privileges as members.</span></span>

<span data-ttu-id="ec1e3-168">Hello 회사 디렉터리에 게스트 사용자에 게 제공할 수 있도록 가능한 tooturn hello 기본 게스트 사용자 제한이 해제는 hello 구성원 사용자와 같은 권한을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec1e3-168">It is possible tooturn off hello default guest user limitations so that a guest user in hello company directory is given hello same permissions as a member user.</span></span>

![게스트 사용자 제한 제거](media/active-directory-b2b-user-properties/remove-guest-limitations.png)

## <a name="next-steps"></a><span data-ttu-id="ec1e3-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ec1e3-170">Next steps</span></span>

<span data-ttu-id="ec1e3-171">Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:</span><span class="sxs-lookup"><span data-stu-id="ec1e3-171">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="ec1e3-172">Azure AD B2B 공동 작업이란?</span><span class="sxs-lookup"><span data-stu-id="ec1e3-172">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="ec1e3-173">B2B 공동 작업 사용자 tooa 역할 추가</span><span class="sxs-lookup"><span data-stu-id="ec1e3-173">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="ec1e3-174">B2B 공동 작업 초대 위임</span><span class="sxs-lookup"><span data-stu-id="ec1e3-174">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="ec1e3-175">B2B 공동 작업 사용자 감사 및 보고</span><span class="sxs-lookup"><span data-stu-id="ec1e3-175">B2B collaboration user auditing and reporting</span></span>](active-directory-b2b-auditing-and-reporting.md)
* [<span data-ttu-id="ec1e3-176">동적 그룹 및 B2B 공동 작업</span><span class="sxs-lookup"><span data-stu-id="ec1e3-176">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="ec1e3-177">B2B 공동 작업 코드 및 PowerShell 샘플</span><span class="sxs-lookup"><span data-stu-id="ec1e3-177">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="ec1e3-178">B2B 공동 작업을 위한 SaaS 앱 구성</span><span class="sxs-lookup"><span data-stu-id="ec1e3-178">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="ec1e3-179">B2B 공동 작업 사용자 토큰</span><span class="sxs-lookup"><span data-stu-id="ec1e3-179">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="ec1e3-180">B2B 공동 작업 사용자 클레임 매핑</span><span class="sxs-lookup"><span data-stu-id="ec1e3-180">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="ec1e3-181">Office 365 외부 공유</span><span class="sxs-lookup"><span data-stu-id="ec1e3-181">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="ec1e3-182">B2B 공동 작업 현재 제한</span><span class="sxs-lookup"><span data-stu-id="ec1e3-182">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
