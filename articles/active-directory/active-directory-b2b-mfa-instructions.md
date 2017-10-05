---
title: "Azure Active Directory B2B 공동 작업 사용자에 대한 조건부 액세스 | Microsoft Docs"
description: "Azure Active Directory B2B 공동 작업 기능은 회사 응용 프로그램에 대한 선택적 액세스를 위해 MFA(Multi-Factor Authentication)를 지원합니다."
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
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: d85f711d6551a68d1248ae8ec61e2ecc1ddc8ecd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="conditional-access-for-b2b-collaboration-users"></a><span data-ttu-id="69704-103">B2B 공동 작업 사용자에 대한 조건부 액세스</span><span class="sxs-lookup"><span data-stu-id="69704-103">Conditional access for B2B collaboration users</span></span>

## <a name="multi-factor-authentication-for-b2b-users"></a><span data-ttu-id="69704-104">B2B 사용자에 대한 다단계 인증</span><span class="sxs-lookup"><span data-stu-id="69704-104">Multi-factor authentication for B2B users</span></span>
<span data-ttu-id="69704-105">Azure AD B2B 공동 작업을 통해 조직에서는 B2B 사용자에 대한 MFA(Multi-Factor Authentication) 정책을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69704-105">With Azure AD B2B collaboration, organizations can enforce multi-factor authentication (MFA) policies for B2B users.</span></span> <span data-ttu-id="69704-106">조직의 전일제 직원과 구성원에 대해 이러한 정책을 사용하는 것과 같은 방법으로 이러한 정책을 테넌트, 앱 또는 개별 사용자 수준에서 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69704-106">These policies can be enforced at the tenant, app, or individual user level, the same way that they are enabled for full-time employees and members of the organization.</span></span> <span data-ttu-id="69704-107">MFA 정책은 리소스 조직에서 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="69704-107">MFA policies are enforced at the resource organization.</span></span>

<span data-ttu-id="69704-108">예제:</span><span class="sxs-lookup"><span data-stu-id="69704-108">Example:</span></span>
1. <span data-ttu-id="69704-109">회사 A의 관리자 또는 정보 근로자가 회사 B의 사용자를 회사 A의 *Foo* 응용 프로그램에 초대합니다.</span><span class="sxs-lookup"><span data-stu-id="69704-109">Admin or information worker in Company A invites user from company B to an application *Foo* in company A.</span></span>
2. <span data-ttu-id="69704-110">회사 A의 응용 프로그램 *Foo*는 액세스 시 MFA를 요구하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="69704-110">Application *Foo* in company A is configured to require MFA on access.</span></span>
3. <span data-ttu-id="69704-111">회사 B의 사용자가 회사 A 테넌트에서 *Foo* 앱에 액세스하려고 하면 MFA 챌린지를 완료하도록 요구됩니다.</span><span class="sxs-lookup"><span data-stu-id="69704-111">When the user from company B attempts to access app *Foo* in the company A tenant, they are asked to complete an MFA challenge.</span></span>
4. <span data-ttu-id="69704-112">사용자는 회사 A와 MFA를 설정할 수 있고 해당 MFA 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="69704-112">The user can set up their MFA with company A, and chooses their MFA option.</span></span>
5. <span data-ttu-id="69704-113">이러한 시나리오는 어떤 ID에도 잘 맞습니다(Azure AD 또는 회사 B의 사용자가 소셜 ID를 사용하여 인증을 받는 경우 MSA).</span><span class="sxs-lookup"><span data-stu-id="69704-113">This scenario works for any identity (Azure AD or MSA, for example, if users in Company B authenticate using social ID)</span></span>
6. <span data-ttu-id="69704-114">회사 A는 MFA를 지원하는 충분한 Azure AD 프리미엄 라이선스가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69704-114">Company A must have sufficient Premium Azure AD licenses that support MFA.</span></span> <span data-ttu-id="69704-115">회사 B의 사용자는 회사 A의 이 라이선스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="69704-115">The user from company B consumes this license from company A.</span></span>

<span data-ttu-id="69704-116">파트너 조직에 MFA 기능이 있더라도 초대하는 테넌시는 항상 파트너 조직 사용자의 MFA를 책임집니다.</span><span class="sxs-lookup"><span data-stu-id="69704-116">The inviting tenancy is always responsible for MFA for users from the partner organization, even if the partner organization has MFA capabilities.</span></span>

### <a name="setting-up-mfa-for-b2b-collaboration-users"></a><span data-ttu-id="69704-117">B2B 공동 작업 사용자에 대한 MFA 설정</span><span class="sxs-lookup"><span data-stu-id="69704-117">Setting up MFA for B2B collaboration users</span></span>
<span data-ttu-id="69704-118">B2B 공동 작업 사용자에 대한 MFA를 설정하는 작업이 얼마나 간단한지 알아보려면 다음 비디오를 시청하세요.</span><span class="sxs-lookup"><span data-stu-id="69704-118">To discover how easy it is to set up MFA for B2B collaboration users, see how in the following video:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-conditional-access-setup/Player]

### <a name="b2b-users-mfa-experience-for-offer-redemption"></a><span data-ttu-id="69704-119">B2B 사용자는 제안 상환을 위해 MFA 환경을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="69704-119">B2B users MFA experience for offer redemption</span></span>
<span data-ttu-id="69704-120">다음 애니메이션을 통해 상환 환경을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69704-120">Check out the following animation to see the redemption experience:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/MFA-redemption/Player]

### <a name="mfa-reset-for-b2b-collaboration-users"></a><span data-ttu-id="69704-121">B2B 공동 작업 사용자에 대해 다시 설정된 MFA</span><span class="sxs-lookup"><span data-stu-id="69704-121">MFA reset for B2B collaboration users</span></span>
<span data-ttu-id="69704-122">현재 관리자는 다음 PowerShell cmdlet을 사용하여 B2B 공동 작업 사용자에게 다시 입증하도록 요구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69704-122">Currently, the admin can require B2B collaboration users to proof up again only by using the following PowerShell cmdlets:</span></span>

1. <span data-ttu-id="69704-123">Azure에 연결</span><span class="sxs-lookup"><span data-stu-id="69704-123">Connect to Azure AD</span></span>

  ```
  $cred = Get-Credential
  Connect-MsolService -Credential $cred
  ```
2. <span data-ttu-id="69704-124">증명 방법이 있는 모든 사용자 가져오기</span><span class="sxs-lookup"><span data-stu-id="69704-124">Get all users with proof up methods</span></span>

  ```
  Get-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```
  <span data-ttu-id="69704-125">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="69704-125">Here is an example:</span></span>

  ```
  PS C:\Users\tjwasserGet-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```

3. <span data-ttu-id="69704-126">특정 사용자에 대한 MFA 방법을 다시 설정하여 B2B 공동 작업 사용자가 증명 방법을 다시 설정하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="69704-126">Reset the MFA method for a specific user to require the B2B collaboration user to set proof-up methods again.</span></span> <span data-ttu-id="69704-127">예제:</span><span class="sxs-lookup"><span data-stu-id="69704-127">Example:</span></span>

  ```
  Reset-MsolStrongAuthenticationMethodByUpn -UserPrincipalName gsamoogle_gmail.com#EXT#@ WoodGroveAzureAD.onmicrosoft.com
  ```

### <a name="why-do-we-perform-mfa-at-the-resource-tenancy"></a><span data-ttu-id="69704-128">리소스 테넌트에서 MFA를 수행하는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="69704-128">Why do we perform MFA at the resource tenancy?</span></span>

<span data-ttu-id="69704-129">현재 릴리스에서 MFA는 예측이 가능하도록 하기 위해 항상 리소스 테넌트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69704-129">In the current release, MFA is always in the resource tenancy, for reasons of predictability.</span></span> <span data-ttu-id="69704-130">예를 들어 Contoso 사용자(Sally)가 Fabrikam에 초대되고 Fabrikam이 B2B 사용자에 대한 MFA를 사용하도록 설정했다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="69704-130">For example, let’s say a Contoso user (Sally) is invited to Fabrikam and Fabrikam has enabled MFA for B2B users.</span></span>

<span data-ttu-id="69704-131">Contoso에 App2가 아닌 App1에 대해서만 설정된 MFA 정책이 있는 경우 토큰의 Contoso MFA 클레임에서 다음 문제가 확인될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69704-131">If Contoso has MFA policy enabled for App1 but not App2, then if we look at the Contoso MFA claim in the token, we might see the following issue:</span></span>

* <span data-ttu-id="69704-132">1일: Contoso의 한 사용자에게 MFA가 있고 이 사용자가 App1에 액세스하는 경우 Fabrikam에 추가 MFA 프롬프트가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69704-132">Day 1: A user has MFA in Contoso and is accessing App1, then no additional MFA prompt is shown in Fabrikam.</span></span>

* <span data-ttu-id="69704-133">2일: 이 사용자는 Contoso의 App2에 액세스할 수 있지만 이제 Fabrikam에 액세스할 때 MFA에 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69704-133">Day 2: The user has accessed App 2 in Contoso, so now when accessing Fabrikam, they must register for MFA there.</span></span>

<span data-ttu-id="69704-134">이 프로세스는 혼동을 일으킬 수 있으며 로그인이 중단될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69704-134">This process can be confusing and could lead to drop in sign-in completions.</span></span>

<span data-ttu-id="69704-135">도한 Contoso에 MFA 기능이 있는 경우에도 Fabrikam에서 항상 Contoso MFA 정책을 신뢰하는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="69704-135">Moreover, even if Contoso has MFA capability, it is not always the case the Fabrikam would trust the Contoso MFA policy.</span></span>

<span data-ttu-id="69704-136">마지막으로 리소스 테넌트 MFA는 MSA 및 소셜 ID에도 적용되고 MFA가 설정되지 않은 파트너 조직에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="69704-136">Finally, resource tenant MFA also works for MSAs and social IDs and for partner orgs that do not have MFA set up.</span></span>

<span data-ttu-id="69704-137">따라서 B2B 사용자의 경우 항상 초대하는 테넌트의 MFA를 요구하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="69704-137">Therefore, the recommendation for MFA for B2B users is to always require MFA in the inviting tenant.</span></span> <span data-ttu-id="69704-138">이렇게 하면 MFA가 2개가 될 수도 있지만 초대하는 테넌트에 액세스할 때마다 최종 사용자 경험을 예측할 수 있습니다. Sally는 초대하는 테넌트를 사용하여 MFA에 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69704-138">This requirement could lead to double MFA in some cases, but whenever accessing the inviting tenant, the end-users experience is predictable: Sally must register for MFA with the inviting tenant.</span></span>

### <a name="device-based-location-based-and-risk-based-conditional-access-for-b2b-users"></a><span data-ttu-id="69704-139">B2B 사용자에 대한 장치 기반, 위치 기반 및 위험 기반 조건부 액세스</span><span class="sxs-lookup"><span data-stu-id="69704-139">Device-based, location-based, and risk-based conditional access for B2B users</span></span>

<span data-ttu-id="69704-140">Contoso에서 회사 데이터에 대한 장치 기반 조건부 액세스 정책을 적용할 수 있으면 Contoso에서 관리되지 않고 Contoso 장치 정책을 준수하지 않는 장치에서는 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="69704-140">When Contoso enables device-based conditional access policies for their corporate data, access is prevented from devices that are not managed by Contoso and not compliant with the Contoso device policies.</span></span>

<span data-ttu-id="69704-141">B2B 사용자의 장치가 Contoso에서 관리되지 않는 경우 이러한 정책이 적용된 컨텍스트가 무엇이든 파트너 조직 B2B 사용자의 액세스는 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="69704-141">If the B2B user’s device isn't managed by Contoso, access of B2B users from the partner organizations is blocked in whatever context these policies are enforced.</span></span> <span data-ttu-id="69704-142">그렇지만 Contoso는 장치 기반 조건부 액세스 정책에서 제외할 특정 파트너 사용자가 포함된 제외 목록을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69704-142">However, Contoso can create exclusion lists containing specific partner users to exclude them from the device-based conditional access policy.</span></span>

#### <a name="location-based-conditional-access-for-b2b"></a><span data-ttu-id="69704-143">B2B에 대한 위치 기반 조건부 액세스</span><span class="sxs-lookup"><span data-stu-id="69704-143">Location-based conditional access for B2B</span></span>

<span data-ttu-id="69704-144">초대하는 조직이 파트너 조직을 정의하는 신뢰할 수 있는 IP 주소 범위를 만들 수 있는 경우 위치 기반 조건부 액세스 정책을 B2B 사용자에게 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69704-144">Location-based conditional access policies can be enforced for B2B users if the inviting organization is able to create a trusted IP address range that defines their partner organizations.</span></span>

#### <a name="risk-based-conditional-access-for-b2b"></a><span data-ttu-id="69704-145">B2B에 대한 위험 기반 조건부 액세스</span><span class="sxs-lookup"><span data-stu-id="69704-145">Risk-based conditional access for B2B</span></span>

<span data-ttu-id="69704-146">위험 평가는 B2B 사용자의 홈 조직에서 수행되기 때문에 현재는 위험 기반 로그인 정책을 B2B 사용자에게 적용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="69704-146">Currently, risk-based sign-in policies cannot be applied to B2B users because the risk evaluation is performed at the B2B user’s home organization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69704-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="69704-147">Next steps</span></span>

<span data-ttu-id="69704-148">Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:</span><span class="sxs-lookup"><span data-stu-id="69704-148">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="69704-149">Azure AD B2B 공동 작업이란?</span><span class="sxs-lookup"><span data-stu-id="69704-149">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="69704-150">Azure Active Directory 관리자가 B2B 공동 작업 사용자를 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="69704-150">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="69704-151">정보 근로자가 B2B 공동 작업 사용자를 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="69704-151">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="69704-152">B2B 공동 작업 초대 전자 메일의 요소</span><span class="sxs-lookup"><span data-stu-id="69704-152">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="69704-153">B2B 공동 작업 초대 상환</span><span class="sxs-lookup"><span data-stu-id="69704-153">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="69704-154">Azure AD B2B 공동 작업 라이선스</span><span class="sxs-lookup"><span data-stu-id="69704-154">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="69704-155">Azure Active Directory B2B 공동 작업 문제 해결</span><span class="sxs-lookup"><span data-stu-id="69704-155">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="69704-156">Azure Active Directory B2B 공동 작업 자주 묻는 질문(FAQ)</span><span class="sxs-lookup"><span data-stu-id="69704-156">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="69704-157">Azure Active Directory B2B 공동 작업 API 및 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="69704-157">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="69704-158">초대 없이 B2B 공동 작업 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="69704-158">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="69704-159">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="69704-159">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
