---
title: "Azure Active Directory의 조건부 액세스 모범 사례 | Microsoft Docs"
description: "조건부 액세스 정책을 구성할 때 알아야 할 사항과 수행하지 않아야 할 사항에 대해 자세히 알아봅니다."
services: active-directory
keywords: "앱에 조건부 액세스, Azure AD로 조건부 액세스, 회사 리소스에 대한 액세스 보호, 조건부 액세스 정책"
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
ms.openlocfilehash: 3e524c116479c1af6eb6a601c9b57d27a697c5a2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="best-practices-for-conditional-access-in-azure-active-directory"></a><span data-ttu-id="2bc01-104">Azure Active Directory의 조건부 액세스 모범 사례</span><span class="sxs-lookup"><span data-stu-id="2bc01-104">Best practices for conditional access in Azure Active Directory</span></span>

<span data-ttu-id="2bc01-105">이 항목에서는 조건부 액세스 정책을 구성할 때 알아야 할 사항과 수행하지 않아야 할 사항에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-105">This topic provides you with information about things you should know and what it is you should avoid doing when configuring conditional access policies.</span></span> <span data-ttu-id="2bc01-106">이 항목을 읽기 전에 [Azure Active Directory 조건부 액세스](active-directory-conditional-access-azure-portal.md)에 설명된 개념 및 용어에 익숙해져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-106">Before reading this topic, you should familiarize yourself with the concepts and the terminology outlined in [Conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal.md)</span></span>

## <a name="what-you-should-know"></a><span data-ttu-id="2bc01-107">알아야 할 사항</span><span class="sxs-lookup"><span data-stu-id="2bc01-107">What you should know</span></span>

### <a name="whats-required-to-make-a-policy-work"></a><span data-ttu-id="2bc01-108">정책을 작동하는 데 무엇이 필요한가요?</span><span class="sxs-lookup"><span data-stu-id="2bc01-108">What’s required to make a policy work?</span></span>

<span data-ttu-id="2bc01-109">새 정책을 만들 경우 선택된 사용자, 그룹, 앱 또는 액세스 제어가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-109">When you create a new policy, there are no users, groups, apps or access controls selected.</span></span>

![클라우드 앱](./media/active-directory-conditional-access-best-practices/02.png)


<span data-ttu-id="2bc01-111">정책이 작동되려면 다음을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-111">To make your policy work, you must configure the following:</span></span>


|<span data-ttu-id="2bc01-112">대상</span><span class="sxs-lookup"><span data-stu-id="2bc01-112">What</span></span>           | <span data-ttu-id="2bc01-113">방법</span><span class="sxs-lookup"><span data-stu-id="2bc01-113">How</span></span>                                  | <span data-ttu-id="2bc01-114">이유</span><span class="sxs-lookup"><span data-stu-id="2bc01-114">Why</span></span>|
|:--            | :--                                  | :-- |
|<span data-ttu-id="2bc01-115">**클라우드 앱**</span><span class="sxs-lookup"><span data-stu-id="2bc01-115">**Cloud apps**</span></span> |<span data-ttu-id="2bc01-116">앱을 하나 이상 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-116">You need to select one or more apps.</span></span>  | <span data-ttu-id="2bc01-117">조건부 액세스 정책의 목표는 권한 있는 사용자가 앱에 액세스하는 방법을 구체적으로 조정할 수 있도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-117">The goal of a conditional access policy is to enable you to fine-tune how authorized users can access your apps.</span></span>|
| <span data-ttu-id="2bc01-118">**사용자 및 그룹**</span><span class="sxs-lookup"><span data-stu-id="2bc01-118">**Users and groups**</span></span> | <span data-ttu-id="2bc01-119">선택한 클라우드 앱에 액세스할 수 있도록 허가된 사용자 또는 그룹을 하나 이상 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-119">You need to select at least one user or group that is authorized to access the cloud apps you have selected.</span></span> | <span data-ttu-id="2bc01-120">할당된 사용자와 그룹이 없는 조건부 액세스 정책은 트리거되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-120">A conditional access policy that has no users and groups assigned, is never triggered.</span></span> |
| <span data-ttu-id="2bc01-121">**액세스 제어**</span><span class="sxs-lookup"><span data-stu-id="2bc01-121">**Access controls**</span></span> | <span data-ttu-id="2bc01-122">하나 이상의 액세스 제어를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-122">You need to select at least one access control.</span></span> | <span data-ttu-id="2bc01-123">정책 프로세서는 조건이 충족될 경우 수행할 작업을 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-123">Your policy processor needs to know what to do if your conditions are satisfied.</span></span>|


<span data-ttu-id="2bc01-124">이러한 기본 요구 사항 외에도 대부분의 경우 조건도 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-124">In addition to these basic requirements, in many cases, you should also configure a condition.</span></span> <span data-ttu-id="2bc01-125">구성된 조건 없이도 정책이 작동할 수 있지만 조건은 앱에 대한 액세스 권한을 보다 구체적으로 조정하기 위한 구동 요인입니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-125">While a policy would also work without a configured condition, conditions are the driving factor for fine-tuning access to your apps.</span></span>


![클라우드 앱](./media/active-directory-conditional-access-best-practices/04.png)



### <a name="how-are-assignments-evaluated"></a><span data-ttu-id="2bc01-127">할당은 어떻게 평가됩니까?</span><span class="sxs-lookup"><span data-stu-id="2bc01-127">How are assignments evaluated?</span></span>

<span data-ttu-id="2bc01-128">모든 할당은 논리적으로 **and**가 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-128">All assignments are logically **ANDed**.</span></span> <span data-ttu-id="2bc01-129">할당을 둘 이상 구성한 경우 모든 할당이 충족되어야 정책을 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-129">If you have more than one assignment configured, to trigger a policy, all assignments must be satisfied.</span></span>  

<span data-ttu-id="2bc01-130">조직의 네트워크 외부에서 수행되는 모든 연결에 적용되는 위치 조건을 구성해야 하는 경우 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-130">If you need to configure a location condition that applies to all connections made from outside your organization's network, you can accomplish this by:</span></span>

- <span data-ttu-id="2bc01-131">**모든 위치** 포함</span><span class="sxs-lookup"><span data-stu-id="2bc01-131">Including **All locations**</span></span>
- <span data-ttu-id="2bc01-132">**모든 신뢰할 수 있는 IP** 제외</span><span class="sxs-lookup"><span data-stu-id="2bc01-132">Excluding **All trusted IPs**</span></span>

### <a name="what-happens-if-you-have-policies-in-the-azure-classic-portal-and-azure-portal-configured"></a><span data-ttu-id="2bc01-133">Azure 클래식 포털과 Azure Portal에서 정책을 구성하면 어떻게 됩니까?</span><span class="sxs-lookup"><span data-stu-id="2bc01-133">What happens if you have policies in the Azure classic portal and Azure portal configured?</span></span>  
<span data-ttu-id="2bc01-134">두 정책은 모두 Azure Active Directory에서 적용되며 모든 요구 사항을 충족하는 경우에만 사용자가 액세스 권한을 획득할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-134">Both policies are enforced by Azure Active Directory and the user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-you-have-policies-in-the-intune-silverlight-portal-and-the-azure-portal"></a><span data-ttu-id="2bc01-135">Intune Silverlight 포털과 Azure Portal에 정책이 있으면 어떻게 됩니까?</span><span class="sxs-lookup"><span data-stu-id="2bc01-135">What happens if you have policies in the Intune Silverlight portal and the Azure Portal?</span></span>
<span data-ttu-id="2bc01-136">두 정책은 모두 Azure Active Directory에서 적용되며 모든 요구 사항을 충족하는 경우에만 사용자가 액세스 권한을 획득할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-136">Both policies are enforced by Azure Active Directory and the user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-i-have-multiple-policies-for-the-same-user-configured"></a><span data-ttu-id="2bc01-137">동일한 사용자에 대해 여러 정책을 구성하면 어떻게 됩니까?</span><span class="sxs-lookup"><span data-stu-id="2bc01-137">What happens if I have multiple policies for the same user configured?</span></span>  
<span data-ttu-id="2bc01-138">Azure Active Directory는 모든 로그인에 대해 모든 정책을 평가하고, 사용자에게 액세스 권한을 부여하기 전에 모든 요구 사항이 충족되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-138">For every sign-in, Azure Active Directory evaluates all policies and ensures that all requirements are met before granted access to the user.</span></span>


### <a name="does-conditional-access-work-with-exchange-activesync"></a><span data-ttu-id="2bc01-139">조건부 액세스가 Exchange ActiveSync에서 작동합니까?</span><span class="sxs-lookup"><span data-stu-id="2bc01-139">Does conditional access work with Exchange ActiveSync?</span></span>

<span data-ttu-id="2bc01-140">예, 조건부 액세스 정책에서 Exchange ActiveSync를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-140">Yes, you can use Exchange ActiveSync in a conditional access policy.</span></span>


## <a name="what-you-should-avoid-doing"></a><span data-ttu-id="2bc01-141">금지해야 할 기능</span><span class="sxs-lookup"><span data-stu-id="2bc01-141">What you should avoid doing</span></span>

<span data-ttu-id="2bc01-142">조건부 액세스 프레임 워크는 훌륭한 구성 유연성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-142">The conditional access framework provides you with a great configuration flexibility.</span></span> <span data-ttu-id="2bc01-143">그러나 훌륭한 유연성은 잘못된 결과를 방지하기 위해 해제하기 전에 각 구성 정책을 신중하게 검토해야 한다는 것을 의미하기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-143">However, great flexibility  also means that you should carefully review each configuration policy prior to releasing it to avoid undesirable results.</span></span> <span data-ttu-id="2bc01-144">이 컨텍스트에서 **모든 사용자 / 그룹 / 응용 프로그램**등 완전한 집합에 영향을 미치는 할당에 특별한 주의를 기울여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-144">In this context, you should pay special attention to assignments affecting complete sets such as **all users / groups / cloud apps**.</span></span>

<span data-ttu-id="2bc01-145">사용자 환경에서 다음과 같은 구성을 피해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-145">In your environment, you should avoid the following configurations:</span></span>


<span data-ttu-id="2bc01-146">**모든 사용자에 대한 모든 클라우드 앱:**</span><span class="sxs-lookup"><span data-stu-id="2bc01-146">**For all users, all cloud apps:**</span></span>

- <span data-ttu-id="2bc01-147">**액세스 차단** - 이 구성은 사용자 전체 조직을 차단하므로 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-147">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>

- <span data-ttu-id="2bc01-148">**호환 장치가 필요** - 장치를 아직 등록하지 않은 사용자의 경우 이 정책은 Intune 포털에 대한 액세스를 비롯한 모든 액세스를 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-148">**Require compliant device** - For users that don't have enrolled their devices yet, this policy blocks all access including access to the Intune portal.</span></span> <span data-ttu-id="2bc01-149">등록된 장치가 없는 관리자의 경우 이 정책은 정책을 변경하기 위해 Azure Portal로 다시 돌아가지 않도록 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-149">If you are an administrator without an enrolled device, this policy blocks you from getting back into the Azure portal to change the policy.</span></span>

- <span data-ttu-id="2bc01-150">**도메인 가입 필요** - 이 정책 차단 액세스에도 도메인에 가입된 장치가 아직 없는 경우에 조직의 모든 사용자에 대한 액세스를 차단할 가능성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-150">**Require domain join** - This policy block access has also the potential to block access for all users in your organization if you don't have a domain-joined device yet.</span></span>


<span data-ttu-id="2bc01-151">**모든 사용자 경우 모든 클라우드 앱, 모든 장치 플랫폼은 다음과 같습니다.**</span><span class="sxs-lookup"><span data-stu-id="2bc01-151">**For all users, all cloud apps, all device platforms:**</span></span>

- <span data-ttu-id="2bc01-152">**액세스 차단** - 이 구성은 사용자 전체 조직을 차단하므로 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-152">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>


## <a name="common-scenarios"></a><span data-ttu-id="2bc01-153">일반적인 시나리오</span><span class="sxs-lookup"><span data-stu-id="2bc01-153">Common scenarios</span></span>

### <a name="requiring-multi-factor-authentication-for-apps"></a><span data-ttu-id="2bc01-154">앱에 다단계 인증 필요</span><span class="sxs-lookup"><span data-stu-id="2bc01-154">Requiring multi-factor authentication for apps</span></span>

<span data-ttu-id="2bc01-155">대다수 사용 환경에서는 다른 앱보다 특히 높은 수준의 보호를 요구하는 앱이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-155">Many environments have apps requiring a higher level of protection than the others.</span></span>
<span data-ttu-id="2bc01-156">예를 들어 중요한 데이터에 액세스할 수 있는 앱의 경우가 여기에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-156">This is, for example, the case for apps that have access to sensitive data.</span></span>
<span data-ttu-id="2bc01-157">이러한 앱에 또 다른 보호 계층을 추가하려는 경우 사용자가 이러한 앱에 액세스할 때 다단계 인증을 요구하는 조건부 액세스 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-157">If you want to add another layer of protection to these apps, you can configure a conditional access policy that requires multi-factor authentication when users are accessing these apps.</span></span>


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a><span data-ttu-id="2bc01-158">신뢰할 수 없는 네트워크에서 액세스하기 위한 다단계 인증 필요</span><span class="sxs-lookup"><span data-stu-id="2bc01-158">Requiring multi-factor authentication for access from networks that are not trusted</span></span>

<span data-ttu-id="2bc01-159">이 시나리오는 다단계 인증에 대한 요구 사항을 추가하기 때문에 이전 시나리오와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-159">This scenario is similar to the previous scenario because it adds a requirement for multi-factor authentication.</span></span>
<span data-ttu-id="2bc01-160">그러나 주요 차이점은 이 요구 사항에 대한 조건에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-160">However, the main difference is the condition for this requirement.</span></span>  
<span data-ttu-id="2bc01-161">이전 시나리오는 중요한 데이터에 액세스할 수 있는 앱에 초점을 맞추었지만, 이 시나리오는 신뢰할 수 있는 위치에 초점을 맞추고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-161">While the focus of the previous scenario was on apps with access to sensitve data, the focus of this scenario is on trusted locations.</span></span>  
<span data-ttu-id="2bc01-162">즉 사용자가 신뢰할 수 없는 네트워크에서 앱에 액세스하는 경우 다단계 인증에 대한 요구 사항이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-162">In other words, you might have a requirement for multi-factor authentication if an app is accessed by a user from a network you don't trust.</span></span>


### <a name="only-trusted-devices-can-access-office-365-services"></a><span data-ttu-id="2bc01-163">신뢰할 수 있는 장치만 Office 365 서비스에 액세스 가능</span><span class="sxs-lookup"><span data-stu-id="2bc01-163">Only trusted devices can access Office 365 services</span></span>

<span data-ttu-id="2bc01-164">사용자 환경에서 Intune을 사용하는 경우 Azure 콘솔에서 조건부 액세스 정책 인터페이스를 즉시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-164">If you are using Intune in your environment, you can immediately start using the conditional access policy interface in the Azure console.</span></span>

<span data-ttu-id="2bc01-165">많은 Intune 고객이 조건부 액세스를 사용하여 신뢰할 수 있는 장치만 Office 365 서비스에 액세스할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-165">Many Intune customers are using conditional access to ensure that only trusted devices can access Office 365 services.</span></span> <span data-ttu-id="2bc01-166">즉 모바일 장치가 Intune에 등록되고 준수 정책 요구 사항을 충족하며 Windows PC가 온-프레미스 도메인에 가입되어 있음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-166">This means that mobile devices are enrolled with Intune and meet compliance policy requirements, and that Windows PCs are joined to an on-premises domain.</span></span> <span data-ttu-id="2bc01-167">주요 개선 사항은 각 Office 365 서비스마다 동일한 정책을 설정할 필요가 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-167">A key improvement is that you do not have to set the same policy for each of the Office 365 services.</span></span>  <span data-ttu-id="2bc01-168">즉, 새 정책을 만들 때 조건부 액세스로 보호하려는 각 Office 365 앱을 포함하도록 클라우드 앱을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="2bc01-168">When you create a new policy, configure the Cloud apps to include each of the O365 apps that you wish to protect with  with Conditional Access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2bc01-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2bc01-169">Next steps</span></span>

<span data-ttu-id="2bc01-170">조건부 액세스 정책을 구성하는 방법을 알아보려면 [Azure Active Directory에서 조건부 액세스 시작](active-directory-conditional-access-azure-portal-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2bc01-170">If you want to know how to configure a conditional access policy, see [Get started with conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).</span></span>
