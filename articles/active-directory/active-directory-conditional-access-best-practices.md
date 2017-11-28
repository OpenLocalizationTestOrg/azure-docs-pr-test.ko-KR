---
title: "Azure Active Directory의 조건부 액세스에 대 한 aaaBest 사례 | Microsoft Docs"
description: "조건부 액세스 정책을 구성할 때 알아야 할 사항과 수행하지 않아야 할 사항에 대해 자세히 알아봅니다."
services: active-directory
keywords: "조건부 액세스 tooapps, Azure AD 사용 하 여 조건부 액세스 조건부 액세스 정책 toocompany 리소스 액세스 보안"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 4952f8746a2e583380b3bb99cfe2fbdae1c07b08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-conditional-access-in-azure-active-directory"></a><span data-ttu-id="47ab6-104">Azure Active Directory의 조건부 액세스 모범 사례</span><span class="sxs-lookup"><span data-stu-id="47ab6-104">Best practices for conditional access in Azure Active Directory</span></span>

<span data-ttu-id="47ab6-105">이 항목에서는 조건부 액세스 정책을 구성할 때 알아야 할 사항과 수행하지 않아야 할 사항에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="47ab6-105">This topic provides you with information about things you should know and what it is you should avoid doing when configuring conditional access policies.</span></span> <span data-ttu-id="47ab6-106">이 항목을 읽기 전에 알아야 할 hello 개념 및 용어 hello에 설명 된 [Azure Active Directory의 조건부 액세스](active-directory-conditional-access-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="47ab6-106">Before reading this topic, you should familiarize yourself with hello concepts and hello terminology outlined in [Conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal.md)</span></span>

## <a name="what-you-should-know"></a><span data-ttu-id="47ab6-107">알아야 할 사항</span><span class="sxs-lookup"><span data-stu-id="47ab6-107">What you should know</span></span>

### <a name="whats-required-toomake-a-policy-work"></a><span data-ttu-id="47ab6-108">Toomake 정책 작업에 필요한 항목</span><span class="sxs-lookup"><span data-stu-id="47ab6-108">What’s required toomake a policy work?</span></span>

<span data-ttu-id="47ab6-109">새 정책을 만들 경우 선택된 사용자, 그룹, 앱 또는 액세스 제어가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="47ab6-109">When you create a new policy, there are no users, groups, apps or access controls selected.</span></span>

![클라우드 앱](./media/active-directory-conditional-access-best-practices/02.png)


<span data-ttu-id="47ab6-111">toomake 정책상 작업, hello 다음을 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47ab6-111">toomake your policy work, you must configure hello following:</span></span>


|<span data-ttu-id="47ab6-112">대상</span><span class="sxs-lookup"><span data-stu-id="47ab6-112">What</span></span>           | <span data-ttu-id="47ab6-113">방법</span><span class="sxs-lookup"><span data-stu-id="47ab6-113">How</span></span>                                  | <span data-ttu-id="47ab6-114">이유</span><span class="sxs-lookup"><span data-stu-id="47ab6-114">Why</span></span>|
|:--            | :--                                  | :-- |
|<span data-ttu-id="47ab6-115">**클라우드 앱**</span><span class="sxs-lookup"><span data-stu-id="47ab6-115">**Cloud apps**</span></span> |<span data-ttu-id="47ab6-116">Tooselect 앱을 하나 이상 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="47ab6-116">You need tooselect one or more apps.</span></span>  | <span data-ttu-id="47ab6-117">조건부 액세스 정책의 hello ֲ tooenable 있습니다 toofine 조정 권한이 있는 사용자가 앱에 액세스할 수 있는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="47ab6-117">hello goal of a conditional access policy is tooenable you toofine-tune how authorized users can access your apps.</span></span>|
| <span data-ttu-id="47ab6-118">**사용자 및 그룹**</span><span class="sxs-lookup"><span data-stu-id="47ab6-118">**Users and groups**</span></span> | <span data-ttu-id="47ab6-119">Tooselect 하나 이상 필요한 사용자 또는 그룹을 선택한 tooaccess hello 클라우드 앱 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="47ab6-119">You need tooselect at least one user or group that is authorized tooaccess hello cloud apps you have selected.</span></span> | <span data-ttu-id="47ab6-120">할당된 사용자와 그룹이 없는 조건부 액세스 정책은 트리거되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="47ab6-120">A conditional access policy that has no users and groups assigned, is never triggered.</span></span> |
| <span data-ttu-id="47ab6-121">**액세스 제어**</span><span class="sxs-lookup"><span data-stu-id="47ab6-121">**Access controls**</span></span> | <span data-ttu-id="47ab6-122">하나 이상의 tooselect 필요한 액세스 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="47ab6-122">You need tooselect at least one access control.</span></span> | <span data-ttu-id="47ab6-123">정책 프로세서 조건을 충족 하는 경우 어떤 toodo tooknow를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="47ab6-123">Your policy processor needs tooknow what toodo if your conditions are satisfied.</span></span>|


<span data-ttu-id="47ab6-124">더하기 toothese 기본 요구 사항은 대부분의 경우에서에 조건을 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47ab6-124">In addition toothese basic requirements, in many cases, you should also configure a condition.</span></span> <span data-ttu-id="47ab6-125">정책 구성 된 조건 없이 작동, 동안 tooyour 앱 액세스를 미세 조정에 대 한 주요 요인인 hello 조건은입니다.</span><span class="sxs-lookup"><span data-stu-id="47ab6-125">While a policy would also work without a configured condition, conditions are hello driving factor for fine-tuning access tooyour apps.</span></span>


![클라우드 앱](./media/active-directory-conditional-access-best-practices/04.png)



### <a name="how-are-assignments-evaluated"></a><span data-ttu-id="47ab6-127">할당은 어떻게 평가됩니까?</span><span class="sxs-lookup"><span data-stu-id="47ab6-127">How are assignments evaluated?</span></span>

<span data-ttu-id="47ab6-128">모든 할당은 논리적으로 **and**가 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="47ab6-128">All assignments are logically **ANDed**.</span></span> <span data-ttu-id="47ab6-129">둘 이상의 할당을 구성 tootrigger을 정책에 있는 경우에 모든 할당을 충족 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47ab6-129">If you have more than one assignment configured, tootrigger a policy, all assignments must be satisfied.</span></span>  

<span data-ttu-id="47ab6-130">조직의 네트워크 외부에서 만든 tooall 연결 적용 되는 위치 조건을 tooconfigure 해야 할 경우이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47ab6-130">If you need tooconfigure a location condition that applies tooall connections made from outside your organization's network, you can accomplish this by:</span></span>

- <span data-ttu-id="47ab6-131">**모든 위치** 포함</span><span class="sxs-lookup"><span data-stu-id="47ab6-131">Including **All locations**</span></span>
- <span data-ttu-id="47ab6-132">**모든 신뢰할 수 있는 IP** 제외</span><span class="sxs-lookup"><span data-stu-id="47ab6-132">Excluding **All trusted IPs**</span></span>

### <a name="what-happens-if-you-have-policies-in-hello-azure-classic-portal-and-azure-portal-configured"></a><span data-ttu-id="47ab6-133">Hello Azure 클래식 포털에서에서 정책 및 Azure 포털이 구성 되어 있는 경우 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="47ab6-133">What happens if you have policies in hello Azure classic portal and Azure portal configured?</span></span>  
<span data-ttu-id="47ab6-134">및이 두 정책은 Azure Active Directory에서 적용 되는 모든 요구 사항을 충족 하는 경우에 hello 사용자 액세스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="47ab6-134">Both policies are enforced by Azure Active Directory and hello user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-you-have-policies-in-hello-intune-silverlight-portal-and-hello-azure-portal"></a><span data-ttu-id="47ab6-135">Hello Intune Silverlight 포털에에서 정책과 hello Azure 포털에 있는 경우 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="47ab6-135">What happens if you have policies in hello Intune Silverlight portal and hello Azure Portal?</span></span>
<span data-ttu-id="47ab6-136">및이 두 정책은 Azure Active Directory에서 적용 되는 모든 요구 사항을 충족 하는 경우에 hello 사용자 액세스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="47ab6-136">Both policies are enforced by Azure Active Directory and hello user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-i-have-multiple-policies-for-hello-same-user-configured"></a><span data-ttu-id="47ab6-137">여러 정책을 같은 사용자 구성 hello에 대 한이 있는 경우 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="47ab6-137">What happens if I have multiple policies for hello same user configured?</span></span>  
<span data-ttu-id="47ab6-138">모든 로그인에 대 한 Azure Active Directory 모든 정책을 평가 하 고 부여한 액세스 toohello 사용자 하기 전에 모든 요구 사항이 충족 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="47ab6-138">For every sign-in, Azure Active Directory evaluates all policies and ensures that all requirements are met before granted access toohello user.</span></span>


### <a name="does-conditional-access-work-with-exchange-activesync"></a><span data-ttu-id="47ab6-139">조건부 액세스가 Exchange ActiveSync에서 작동합니까?</span><span class="sxs-lookup"><span data-stu-id="47ab6-139">Does conditional access work with Exchange ActiveSync?</span></span>

<span data-ttu-id="47ab6-140">예, 조건부 액세스 정책에서 Exchange ActiveSync를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47ab6-140">Yes, you can use Exchange ActiveSync in a conditional access policy.</span></span>


## <a name="what-you-should-avoid-doing"></a><span data-ttu-id="47ab6-141">금지해야 할 기능</span><span class="sxs-lookup"><span data-stu-id="47ab6-141">What you should avoid doing</span></span>

<span data-ttu-id="47ab6-142">hello 조건부 액세스 프레임 워크 구성 뛰어난 유연성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="47ab6-142">hello conditional access framework provides you with a great configuration flexibility.</span></span> <span data-ttu-id="47ab6-143">그러나 뛰어난 유연성도 의미 각 구성 정책 이전 tooreleasing 주의 깊게 검토 해야 하기 tooavoid 잘못 된 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="47ab6-143">However, great flexibility  also means that you should carefully review each configuration policy prior tooreleasing it tooavoid undesirable results.</span></span> <span data-ttu-id="47ab6-144">이 컨텍스트에서 사용할 때 특히 주의 tooassignments와 같은 집합 전체에 영향을 주는 기울여야 **모든 사용자 / 그룹 / 클라우드 앱**합니다.</span><span class="sxs-lookup"><span data-stu-id="47ab6-144">In this context, you should pay special attention tooassignments affecting complete sets such as **all users / groups / cloud apps**.</span></span>

<span data-ttu-id="47ab6-145">사용자 환경에는 구성을 따르고 hello를 피해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47ab6-145">In your environment, you should avoid hello following configurations:</span></span>


<span data-ttu-id="47ab6-146">**모든 사용자에 대한 모든 클라우드 앱:**</span><span class="sxs-lookup"><span data-stu-id="47ab6-146">**For all users, all cloud apps:**</span></span>

- <span data-ttu-id="47ab6-147">**액세스 차단** - 이 구성은 사용자 전체 조직을 차단하므로 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="47ab6-147">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>

- <span data-ttu-id="47ab6-148">**준수 장치 필요** -사용자에 대 한 하지 않는 등록 장치를 아직이 정책은 액세스 toohello Intune 포털을 포함 한 모든 액세스를 차단 합니다.</span><span class="sxs-lookup"><span data-stu-id="47ab6-148">**Require compliant device** - For users that don't have enrolled their devices yet, this policy blocks all access including access toohello Intune portal.</span></span> <span data-ttu-id="47ab6-149">등록된 된 장치가 없는 관리자 인 경우이 정책은 hello Azure 포털 toochange hello 정책에는 도달에서 차단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47ab6-149">If you are an administrator without an enrolled device, this policy blocks you from getting back into hello Azure portal toochange hello policy.</span></span>

- <span data-ttu-id="47ab6-150">**도메인 가입을 요구** -이 정책 블록 액세스도 hello 잠재적인 tooblock에 대 한 권한이 모든 사용자가 조직에는 도메인에 가입 된 장치 아직 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="47ab6-150">**Require domain join** - This policy block access has also hello potential tooblock access for all users in your organization if you don't have a domain-joined device yet.</span></span>


<span data-ttu-id="47ab6-151">**모든 사용자 경우 모든 클라우드 앱, 모든 장치 플랫폼은 다음과 같습니다.**</span><span class="sxs-lookup"><span data-stu-id="47ab6-151">**For all users, all cloud apps, all device platforms:**</span></span>

- <span data-ttu-id="47ab6-152">**액세스 차단** - 이 구성은 사용자 전체 조직을 차단하므로 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="47ab6-152">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>


## <a name="common-scenarios"></a><span data-ttu-id="47ab6-153">일반적인 시나리오</span><span class="sxs-lookup"><span data-stu-id="47ab6-153">Common scenarios</span></span>

### <a name="requiring-multi-factor-authentication-for-apps"></a><span data-ttu-id="47ab6-154">앱에 다단계 인증 필요</span><span class="sxs-lookup"><span data-stu-id="47ab6-154">Requiring multi-factor authentication for apps</span></span>

<span data-ttu-id="47ab6-155">많은 환경 다른 hello 보다 더 높은 수준의 보호를 요구 하는 앱에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="47ab6-155">Many environments have apps requiring a higher level of protection than hello others.</span></span>
<span data-ttu-id="47ab6-156">이 경우, 예를 들어 hello toosensitive 데이터에 액세스 된 응용 프로그램에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="47ab6-156">This is, for example, hello case for apps that have access toosensitive data.</span></span>
<span data-ttu-id="47ab6-157">보호 toothese 앱의 다른 레이어 tooadd을 원하는 경우 사용자가 이러한 앱에 액세스 하는 다단계 인증을 요구 하는 조건부 액세스 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47ab6-157">If you want tooadd another layer of protection toothese apps, you can configure a conditional access policy that requires multi-factor authentication when users are accessing these apps.</span></span>


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a><span data-ttu-id="47ab6-158">신뢰할 수 없는 네트워크에서 액세스하기 위한 다단계 인증 필요</span><span class="sxs-lookup"><span data-stu-id="47ab6-158">Requiring multi-factor authentication for access from networks that are not trusted</span></span>

<span data-ttu-id="47ab6-159">이 시나리오는 multi-factor authentication에 대해 요구 사항을 추가 하기 때문에 비슷한 toohello 이전 시나리오는입니다.</span><span class="sxs-lookup"><span data-stu-id="47ab6-159">This scenario is similar toohello previous scenario because it adds a requirement for multi-factor authentication.</span></span>
<span data-ttu-id="47ab6-160">그러나 hello 주요 차이점은이 요구 사항에 대 한 hello 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="47ab6-160">However, hello main difference is hello condition for this requirement.</span></span>  
<span data-ttu-id="47ab6-161">Hello 이전 시나리오의 hello 포커스 toosensitve 데이터 액세스를 사용 하 여 앱에 때 hello이이 시나리오는 신뢰할 수 있는 위치에.</span><span class="sxs-lookup"><span data-stu-id="47ab6-161">While hello focus of hello previous scenario was on apps with access toosensitve data, hello focus of this scenario is on trusted locations.</span></span>  
<span data-ttu-id="47ab6-162">즉 사용자가 신뢰할 수 없는 네트워크에서 앱에 액세스하는 경우 다단계 인증에 대한 요구 사항이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47ab6-162">In other words, you might have a requirement for multi-factor authentication if an app is accessed by a user from a network you don't trust.</span></span>


### <a name="only-trusted-devices-can-access-office-365-services"></a><span data-ttu-id="47ab6-163">신뢰할 수 있는 장치만 Office 365 서비스에 액세스 가능</span><span class="sxs-lookup"><span data-stu-id="47ab6-163">Only trusted devices can access Office 365 services</span></span>

<span data-ttu-id="47ab6-164">사용자 환경에서 Intune을 사용 하는 경우 hello Azure 콘솔에서에서 조건부 액세스 정책 인터페이스 hello 사용을 즉시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47ab6-164">If you are using Intune in your environment, you can immediately start using hello conditional access policy interface in hello Azure console.</span></span>

<span data-ttu-id="47ab6-165">많은 Intune 고객 신뢰할 수 있는 장치에만 Office 365 서비스에 액세스할 수 있도록 조건부 액세스 tooensure를 사용 중입니다.</span><span class="sxs-lookup"><span data-stu-id="47ab6-165">Many Intune customers are using conditional access tooensure that only trusted devices can access Office 365 services.</span></span> <span data-ttu-id="47ab6-166">이 의미 있고 Windows Pc 조인된 tooan 온-프레미스 도메인은 모바일 장치는 Intune에 등록 된 및 규정 준수 정책 요구 사항을 충족 합니다.</span><span class="sxs-lookup"><span data-stu-id="47ab6-166">This means that mobile devices are enrolled with Intune and meet compliance policy requirements, and that Windows PCs are joined tooan on-premises domain.</span></span> <span data-ttu-id="47ab6-167">주요한 개선 사항은 하지 않았는지 tooset 각 hello Office 365 서비스에 대해 같은 정책 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="47ab6-167">A key improvement is that you do not have tooset hello same policy for each of hello Office 365 services.</span></span>  <span data-ttu-id="47ab6-168">새 정책을 만들 때 hello 클라우드 앱 tooinclude 각와 tooprotect 조건부 액세스를 사용 하 여 원하는 hello O365 앱을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="47ab6-168">When you create a new policy, configure hello Cloud apps tooinclude each of hello O365 apps that you wish tooprotect with  with Conditional Access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="47ab6-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="47ab6-169">Next steps</span></span>

<span data-ttu-id="47ab6-170">Tooknow tooconfigure 조건부 액세스 정책을 참조 하는 방법을 원하면 [Azure Active Directory의 조건부 액세스 시작](active-directory-conditional-access-azure-portal-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="47ab6-170">If you want tooknow how tooconfigure a conditional access policy, see [Get started with conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).</span></span>
