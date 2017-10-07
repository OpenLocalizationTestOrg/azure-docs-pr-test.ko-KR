---
title: "Azure Active Directory B2B 공동 작업 사용자에 대 한 aaaConditional 액세스 | Microsoft Docs"
description: "Azure Active Directory B2B 공동 작업 대 한 선택적 액세스 tooyour 회사 응용 프로그램에 대 한 multi-factor authentication (MFA)를 지원"
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
ms.openlocfilehash: 3a05be4393f74ff8e87f32432a222a5fbac9af62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-for-b2b-collaboration-users"></a><span data-ttu-id="ea07c-103">B2B 공동 작업 사용자에 대한 조건부 액세스</span><span class="sxs-lookup"><span data-stu-id="ea07c-103">Conditional access for B2B collaboration users</span></span>

## <a name="multi-factor-authentication-for-b2b-users"></a><span data-ttu-id="ea07c-104">B2B 사용자에 대한 다단계 인증</span><span class="sxs-lookup"><span data-stu-id="ea07c-104">Multi-factor authentication for B2B users</span></span>
<span data-ttu-id="ea07c-105">Azure AD B2B 공동 작업을 통해 조직에서는 B2B 사용자에 대한 MFA(Multi-Factor Authentication) 정책을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea07c-105">With Azure AD B2B collaboration, organizations can enforce multi-factor authentication (MFA) policies for B2B users.</span></span> <span data-ttu-id="ea07c-106">이러한 정책이 적용 hello 테 넌 트, 앱 또는 개별 사용자 수준에서 hello 정규직 직원 및 hello 조직의 멤버에 대해 설정 된 동일한 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea07c-106">These policies can be enforced at hello tenant, app, or individual user level, hello same way that they are enabled for full-time employees and members of hello organization.</span></span> <span data-ttu-id="ea07c-107">Hello 리소스 조직에서 MFA 정책은 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea07c-107">MFA policies are enforced at hello resource organization.</span></span>

<span data-ttu-id="ea07c-108">예제:</span><span class="sxs-lookup"><span data-stu-id="ea07c-108">Example:</span></span>
1. <span data-ttu-id="ea07c-109">관리자 또는 정보 근로자 회사 A에서에서 B 사는 tooan 응용 프로그램에서 사용자를 초대 *Foo* 회사 A에서</span><span class="sxs-lookup"><span data-stu-id="ea07c-109">Admin or information worker in Company A invites user from company B tooan application *Foo* in company A.</span></span>
2. <span data-ttu-id="ea07c-110">응용 프로그램 *Foo* 회사 A는 구성 된 toorequire MFA 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea07c-110">Application *Foo* in company A is configured toorequire MFA on access.</span></span>
3. <span data-ttu-id="ea07c-111">B 사는에서 hello 사용자 tooaccess 응용 프로그램을 시도 하는 경우 *Foo* hello 회사는 테 넌 트에 toocomplete MFA 챌린지를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea07c-111">When hello user from company B attempts tooaccess app *Foo* in hello company A tenant, they are asked toocomplete an MFA challenge.</span></span>
4. <span data-ttu-id="ea07c-112">hello 사용자 회사 A가 MFA를 설정할 수 및가 자신의 MFA 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea07c-112">hello user can set up their MFA with company A, and chooses their MFA option.</span></span>
5. <span data-ttu-id="ea07c-113">이러한 시나리오는 어떤 ID에도 잘 맞습니다(Azure AD 또는 회사 B의 사용자가 소셜 ID를 사용하여 인증을 받는 경우 MSA).</span><span class="sxs-lookup"><span data-stu-id="ea07c-113">This scenario works for any identity (Azure AD or MSA, for example, if users in Company B authenticate using social ID)</span></span>
6. <span data-ttu-id="ea07c-114">회사 A는 MFA를 지원하는 충분한 Azure AD 프리미엄 라이선스가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea07c-114">Company A must have sufficient Premium Azure AD licenses that support MFA.</span></span> <span data-ttu-id="ea07c-115">B 사는에서 hello 사용자가 회사 A에서에서이 라이선스 사용</span><span class="sxs-lookup"><span data-stu-id="ea07c-115">hello user from company B consumes this license from company A.</span></span>

<span data-ttu-id="ea07c-116">hello 초대 테 넌 시는 hello 파트너 조직에는 MFA 기능이 하는 경우에 항상 hello 파트너 조직에서 사용자에 대 한 MFA 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea07c-116">hello inviting tenancy is always responsible for MFA for users from hello partner organization, even if hello partner organization has MFA capabilities.</span></span>

### <a name="setting-up-mfa-for-b2b-collaboration-users"></a><span data-ttu-id="ea07c-117">B2B 공동 작업 사용자에 대한 MFA 설정</span><span class="sxs-lookup"><span data-stu-id="ea07c-117">Setting up MFA for B2B collaboration users</span></span>
<span data-ttu-id="ea07c-118">B2B 공동 작업 사용자가 MFA tooset 것이 얼마나 쉬운지 toodiscover 방법은 참조 비디오 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="ea07c-118">toodiscover how easy it is tooset up MFA for B2B collaboration users, see how in hello following video:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-conditional-access-setup/Player]

### <a name="b2b-users-mfa-experience-for-offer-redemption"></a><span data-ttu-id="ea07c-119">B2B 사용자는 제안 상환을 위해 MFA 환경을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ea07c-119">B2B users MFA experience for offer redemption</span></span>
<span data-ttu-id="ea07c-120">다음 애니메이션 toosee hello 상환 경험 hello 확인해 보세요.</span><span class="sxs-lookup"><span data-stu-id="ea07c-120">Check out hello following animation toosee hello redemption experience:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/MFA-redemption/Player]

### <a name="mfa-reset-for-b2b-collaboration-users"></a><span data-ttu-id="ea07c-121">B2B 공동 작업 사용자에 대해 다시 설정된 MFA</span><span class="sxs-lookup"><span data-stu-id="ea07c-121">MFA reset for B2B collaboration users</span></span>
<span data-ttu-id="ea07c-122">현재 admin 님 안녕하세요 요구할 수 B2B 공동 작업 사용자 tooproof를 다시 hello 다음 PowerShell cmdlet을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="ea07c-122">Currently, hello admin can require B2B collaboration users tooproof up again only by using hello following PowerShell cmdlets:</span></span>

1. <span data-ttu-id="ea07c-123">TooAzure AD 연결</span><span class="sxs-lookup"><span data-stu-id="ea07c-123">Connect tooAzure AD</span></span>

  ```
  $cred = Get-Credential
  Connect-MsolService -Credential $cred
  ```
2. <span data-ttu-id="ea07c-124">증명 방법이 있는 모든 사용자 가져오기</span><span class="sxs-lookup"><span data-stu-id="ea07c-124">Get all users with proof up methods</span></span>

  ```
  Get-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```
  <span data-ttu-id="ea07c-125">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="ea07c-125">Here is an example:</span></span>

  ```
  PS C:\Users\tjwasserGet-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```

3. <span data-ttu-id="ea07c-126">특정 사용자 toorequire hello B2B 공동 작업 사용자 tooset 증명 방법에 대 한 hello MFA 메서드를 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea07c-126">Reset hello MFA method for a specific user toorequire hello B2B collaboration user tooset proof-up methods again.</span></span> <span data-ttu-id="ea07c-127">예제:</span><span class="sxs-lookup"><span data-stu-id="ea07c-127">Example:</span></span>

  ```
  Reset-MsolStrongAuthenticationMethodByUpn -UserPrincipalName gsamoogle_gmail.com#EXT#@ WoodGroveAzureAD.onmicrosoft.com
  ```

### <a name="why-do-we-perform-mfa-at-hello-resource-tenancy"></a><span data-ttu-id="ea07c-128">Hello 리소스 테 넌 트에 MFA를 수행 하려면 이유 म?</span><span class="sxs-lookup"><span data-stu-id="ea07c-128">Why do we perform MFA at hello resource tenancy?</span></span>

<span data-ttu-id="ea07c-129">Hello 현재 릴리스에서 MFA는 hello 리소스 테 넌 트, 예측 가능성의 이유로 항상 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea07c-129">In hello current release, MFA is always in hello resource tenancy, for reasons of predictability.</span></span> <span data-ttu-id="ea07c-130">예를 들어 Contoso 사용자 (Sally)가 초대 된 tooFabrikam 고 Fabrikam B2B 사용자에 대 한 MFA를 활성화 가정해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="ea07c-130">For example, let’s say a Contoso user (Sally) is invited tooFabrikam and Fabrikam has enabled MFA for B2B users.</span></span>

<span data-ttu-id="ea07c-131">Contoso에는 MFA 정책 App1 있지만 하지 App2 사용 다음 hello Contoso MFA 클레임 hello 토큰에 표시 될 수 있습니다 보면 hello 문제 다음:</span><span class="sxs-lookup"><span data-stu-id="ea07c-131">If Contoso has MFA policy enabled for App1 but not App2, then if we look at hello Contoso MFA claim in hello token, we might see hello following issue:</span></span>

* <span data-ttu-id="ea07c-132">1일: Contoso의 한 사용자에게 MFA가 있고 이 사용자가 App1에 액세스하는 경우 Fabrikam에 추가 MFA 프롬프트가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ea07c-132">Day 1: A user has MFA in Contoso and is accessing App1, then no additional MFA prompt is shown in Fabrikam.</span></span>

* <span data-ttu-id="ea07c-133">2 일: hello 사용자가 액세스 Contoso에서 응용 프로그램 2 이제 Fabrikam에 액세스할 때, 있습니다 MFA에 대 한 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea07c-133">Day 2: hello user has accessed App 2 in Contoso, so now when accessing Fabrikam, they must register for MFA there.</span></span>

<span data-ttu-id="ea07c-134">이 프로세스 혼동 될 수 있으며 toodrop 완료가 로그인에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea07c-134">This process can be confusing and could lead toodrop in sign-in completions.</span></span>

<span data-ttu-id="ea07c-135">또한도 Contoso에 MFA 기능이 없는 경우 항상 hello 사례 hello Fabrikam에서 Contoso MFA 정책 hello를 신뢰 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea07c-135">Moreover, even if Contoso has MFA capability, it is not always hello case hello Fabrikam would trust hello Contoso MFA policy.</span></span>

<span data-ttu-id="ea07c-136">마지막으로 리소스 테넌트 MFA는 MSA 및 소셜 ID에도 적용되고 MFA가 설정되지 않은 파트너 조직에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea07c-136">Finally, resource tenant MFA also works for MSAs and social IDs and for partner orgs that do not have MFA set up.</span></span>

<span data-ttu-id="ea07c-137">따라서 B2B 사용자에 대 한 MFA에 대 한 hello 권장 tooalways hello 초대 테 넌 트에에서 MFA를 요구 사항은입니다.</span><span class="sxs-lookup"><span data-stu-id="ea07c-137">Therefore, hello recommendation for MFA for B2B users is tooalways require MFA in hello inviting tenant.</span></span> <span data-ttu-id="ea07c-138">이 요구 사항은 경우에 따라 MFA toodouble 될 수 있지만 hello 최종 사용자에 게 체험은 예측 가능한 hello 초대 테 넌 트에 액세스 하 때마다: Sally hello 초대 테 넌 트와 MFA를 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea07c-138">This requirement could lead toodouble MFA in some cases, but whenever accessing hello inviting tenant, hello end-users experience is predictable: Sally must register for MFA with hello inviting tenant.</span></span>

### <a name="device-based-location-based-and-risk-based-conditional-access-for-b2b-users"></a><span data-ttu-id="ea07c-139">B2B 사용자에 대한 장치 기반, 위치 기반 및 위험 기반 조건부 액세스</span><span class="sxs-lookup"><span data-stu-id="ea07c-139">Device-based, location-based, and risk-based conditional access for B2B users</span></span>

<span data-ttu-id="ea07c-140">Contoso 회사 데이터에 대 한 장치 기반 조건부 액세스 정책을 사용 하면 때 Contoso 및 hello Contoso 장치 정책을 준수 하지 않으면 관리 되지 않는 장치에서 액세스할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea07c-140">When Contoso enables device-based conditional access policies for their corporate data, access is prevented from devices that are not managed by Contoso and not compliant with hello Contoso device policies.</span></span>

<span data-ttu-id="ea07c-141">Hello B2B 사용자의 장치는 Contoso에 의해 관리 되지, 이러한 정책이 적용 된 모든 컨텍스트에서 hello 파트너 조직에서 B2B 사용자의 액세스 차단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea07c-141">If hello B2B user’s device isn't managed by Contoso, access of B2B users from hello partner organizations is blocked in whatever context these policies are enforced.</span></span> <span data-ttu-id="ea07c-142">그러나 Contoso 장치 기반 조건부 액세스 정책에서 hello 특정 파트너 사용자 tooexclude를 포함 하는 목록을 제외를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea07c-142">However, Contoso can create exclusion lists containing specific partner users tooexclude them from hello device-based conditional access policy.</span></span>

#### <a name="location-based-conditional-access-for-b2b"></a><span data-ttu-id="ea07c-143">B2B에 대한 위치 기반 조건부 액세스</span><span class="sxs-lookup"><span data-stu-id="ea07c-143">Location-based conditional access for B2B</span></span>

<span data-ttu-id="ea07c-144">위치 기반 조건부 액세스 정책은 수 toocreate 파트너 조직을 정의 하는 신뢰할 수 있는 IP 주소 범위는 하는 hello 초대 조직 B2B 사용자에 대 한 적용 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea07c-144">Location-based conditional access policies can be enforced for B2B users if hello inviting organization is able toocreate a trusted IP address range that defines their partner organizations.</span></span>

#### <a name="risk-based-conditional-access-for-b2b"></a><span data-ttu-id="ea07c-145">B2B에 대한 위험 기반 조건부 액세스</span><span class="sxs-lookup"><span data-stu-id="ea07c-145">Risk-based conditional access for B2B</span></span>

<span data-ttu-id="ea07c-146">현재 로그인 위험 기반 정책 hello 위험 평가 hello B2B 사용자의 홈 조직에서 수행 되기 때문에 적용 된 tooB2B 사용자 일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ea07c-146">Currently, risk-based sign-in policies cannot be applied tooB2B users because hello risk evaluation is performed at hello B2B user’s home organization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea07c-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ea07c-147">Next steps</span></span>

<span data-ttu-id="ea07c-148">Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:</span><span class="sxs-lookup"><span data-stu-id="ea07c-148">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="ea07c-149">Azure AD B2B 공동 작업이란?</span><span class="sxs-lookup"><span data-stu-id="ea07c-149">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="ea07c-150">Azure Active Directory 관리자가 B2B 공동 작업 사용자를 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="ea07c-150">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="ea07c-151">정보 근로자가 B2B 공동 작업 사용자를 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="ea07c-151">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="ea07c-152">hello B2B 공동 작업 초대 메일의 hello 요소</span><span class="sxs-lookup"><span data-stu-id="ea07c-152">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="ea07c-153">B2B 공동 작업 초대 상환</span><span class="sxs-lookup"><span data-stu-id="ea07c-153">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="ea07c-154">Azure AD B2B 공동 작업 라이선스</span><span class="sxs-lookup"><span data-stu-id="ea07c-154">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="ea07c-155">Azure Active Directory B2B 공동 작업 문제 해결</span><span class="sxs-lookup"><span data-stu-id="ea07c-155">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="ea07c-156">Azure Active Directory B2B 공동 작업 자주 묻는 질문(FAQ)</span><span class="sxs-lookup"><span data-stu-id="ea07c-156">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="ea07c-157">Azure Active Directory B2B 공동 작업 API 및 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="ea07c-157">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="ea07c-158">초대 없이 B2B 공동 작업 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="ea07c-158">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="ea07c-159">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="ea07c-159">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
