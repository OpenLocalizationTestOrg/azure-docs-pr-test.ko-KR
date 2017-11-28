---
title: "Azure AD SSPR 데이터 요구 사항 | Microsoft Docs"
description: "데이터 요구 사항에 대 한 Azure AD 셀프 서비스 암호 재설정 및 방법을 toosatisfy에"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: b68a1d7914dcd0bb4509d0e94914dc4309f4463a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-password-reset-without-requiring-end-user-registration"></a><span data-ttu-id="9e2a3-103">최종 사용자를 등록할 필요 없이 암호 재설정 배포</span><span class="sxs-lookup"><span data-stu-id="9e2a3-103">Deploy password reset without requiring end-user registration</span></span>

<span data-ttu-id="9e2a3-104">셀프 서비스 암호 재설정 (SSPR)를 배포 하려면 인증 데이터 toobe 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e2a3-104">Deploying Self-Service Password Reset (SSPR) requires authentication data toobe present.</span></span> <span data-ttu-id="9e2a3-105">일부 조직에는 사용자가 인증 데이터를 직접 입력 해도 되지만 대부분의 조직에서는 Active Directory의 기존 데이터와 toosynchronize.</span><span class="sxs-lookup"><span data-stu-id="9e2a3-105">Some organizations have their users enter their authentication data themselves, but many organizations prefer toosynchronize with existing data in Active Directory.</span></span> <span data-ttu-id="9e2a3-106">가 적절 한 형식의 데이터가 온-프레미스 디렉터리에 구성 하는 경우 [기본 설정을 사용 하는 Azure AD Connect](./connect/active-directory-aadconnect-get-started-express.md), 데이터를 사용할 수 있는 tooAzure AD 하 수와 필요한 사용자 조작 없이 SSPR 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e2a3-106">If you have properly formatted data in your on-premises directory, and configure [Azure AD Connect using express settings](./connect/active-directory-aadconnect-get-started-express.md), that data is made available tooAzure AD and SSPR with no user interaction required.</span></span>

<span data-ttu-id="9e2a3-107">Hello 형식 + CountryCode PhoneNumber 예제에 전화 번호가 있어야: + 1 4255551234 toowork 제대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e2a3-107">Any phone numbers must be in hello format +CountryCode PhoneNumber Example: +1 4255551234 toowork properly.</span></span>

> [!NOTE]
> <span data-ttu-id="9e2a3-108">암호 재설정은 전화 번호 확장을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9e2a3-108">Password reset does not support phone extensions.</span></span> <span data-ttu-id="9e2a3-109">Hello + 1 4255551234 X 12345 형식에도 확장 hello 전화를 건 전에 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e2a3-109">Even in hello +1 4255551234X12345 format, extensions are removed before hello call is placed.</span></span>

## <a name="fields-populated"></a><span data-ttu-id="9e2a3-110">채워진 필드</span><span class="sxs-lookup"><span data-stu-id="9e2a3-110">Fields populated</span></span>

<span data-ttu-id="9e2a3-111">Hello 기본 설정을 사용 하 여 Azure AD Connect hello 뒤에서 매핑이 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e2a3-111">If you use hello default settings in Azure AD Connect hello following mappings are made.</span></span>

| <span data-ttu-id="9e2a3-112">온-프레미스 AD</span><span class="sxs-lookup"><span data-stu-id="9e2a3-112">On-premises AD</span></span> | <span data-ttu-id="9e2a3-113">Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e2a3-113">Azure AD</span></span> | <span data-ttu-id="9e2a3-114">Azure AD 인증 연락처 정보</span><span class="sxs-lookup"><span data-stu-id="9e2a3-114">Azure AD Authentication contact info</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9e2a3-115">telephoneNumber</span><span class="sxs-lookup"><span data-stu-id="9e2a3-115">telephoneNumber</span></span> | <span data-ttu-id="9e2a3-116">사무실 전화</span><span class="sxs-lookup"><span data-stu-id="9e2a3-116">Office phone</span></span> | <span data-ttu-id="9e2a3-117">대체 전화</span><span class="sxs-lookup"><span data-stu-id="9e2a3-117">Alternate phone</span></span> |
| <span data-ttu-id="9e2a3-118">mobile</span><span class="sxs-lookup"><span data-stu-id="9e2a3-118">mobile</span></span> | <span data-ttu-id="9e2a3-119">휴대폰</span><span class="sxs-lookup"><span data-stu-id="9e2a3-119">Mobile phone</span></span> | <span data-ttu-id="9e2a3-120">Phone</span><span class="sxs-lookup"><span data-stu-id="9e2a3-120">Phone</span></span> |


## <a name="security-questions-and-answers"></a><span data-ttu-id="9e2a3-121">보안 질문 및 답변</span><span class="sxs-lookup"><span data-stu-id="9e2a3-121">Security questions and answers</span></span>

<span data-ttu-id="9e2a3-122">Azure AD 테 넌 트에 안전 하 게 저장 되 고 hello 통해 액세스할 수 있는 toousers만는 보안 질문 및 답변 [SSPR 등록 포털](https://aka.ms/ssprsetup)합니다.</span><span class="sxs-lookup"><span data-stu-id="9e2a3-122">Security questions and answers are stored securely in your Azure AD tenant and are only accessible toousers via hello [SSPR registration portal](https://aka.ms/ssprsetup).</span></span> <span data-ttu-id="9e2a3-123">관리자가 보거나 다른 사용자가 질문 및 답변의 hello 내용을 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9e2a3-123">Administrators can't see or modify hello contents of another users questions and answers.</span></span>

### <a name="what-happens-when-a-user-registers"></a><span data-ttu-id="9e2a3-124">사용자가 등록하면 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="9e2a3-124">What happens when a user registers</span></span>

<span data-ttu-id="9e2a3-125">사용자가 등록할 때 다음 필드는 hello hello 등록 페이지에 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e2a3-125">When a user registers, hello registration page sets hello following fields:</span></span>

* <span data-ttu-id="9e2a3-126">인증 전화</span><span class="sxs-lookup"><span data-stu-id="9e2a3-126">Authentication Phone</span></span>
* <span data-ttu-id="9e2a3-127">인증 전자 메일</span><span class="sxs-lookup"><span data-stu-id="9e2a3-127">Authentication Email</span></span>
* <span data-ttu-id="9e2a3-128">보안 질문 및 답변</span><span class="sxs-lookup"><span data-stu-id="9e2a3-128">Security Questions and Answers</span></span>

<span data-ttu-id="9e2a3-129">에 대 한 값을 제공 하면 **휴대폰** 또는 **암호 확인용 메일**, 사용자가 즉시 사용할 수 있습니다 이러한 값 tooreset 암호, hello 서비스에 대 한 등록 되지 않은 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e2a3-129">If you have provided a value for **Mobile Phone** or **Alternate Email**, users can immediately use those values tooreset their passwords, even if they haven't registered for hello service.</span></span> <span data-ttu-id="9e2a3-130">또한 사용자 hello에 대 한 처음으로 등록 하는 경우 해당 값을 볼 수 있으며 만들려는 경우 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e2a3-130">In addition, users see those values when registering for hello first time, and modify them if they wish.</span></span> <span data-ttu-id="9e2a3-131">이러한 값이 hello에 영구 저장 해야 성공적으로 등록 될 **인증 전화** 및 **인증 전자 메일** 필드를 각각.</span><span class="sxs-lookup"><span data-stu-id="9e2a3-131">After they successfully register, these values will be persisted in hello **Authentication Phone** and **Authentication Email** fields, respectively.</span></span>

## <a name="set-and-read-authentication-data-using-powershell"></a><span data-ttu-id="9e2a3-132">PowerShell을 사용하여 인증 데이터 설정 및 읽기</span><span class="sxs-lookup"><span data-stu-id="9e2a3-132">Set and read authentication data using PowerShell</span></span>

<span data-ttu-id="9e2a3-133">PowerShell을 사용 하 여 hello 다음 필드를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e2a3-133">hello following fields can be set using PowerShell</span></span>

* <span data-ttu-id="9e2a3-134">대체 전자 메일</span><span class="sxs-lookup"><span data-stu-id="9e2a3-134">Alternate Email</span></span>
* <span data-ttu-id="9e2a3-135">휴대폰</span><span class="sxs-lookup"><span data-stu-id="9e2a3-135">Mobile Phone</span></span>
* <span data-ttu-id="9e2a3-136">사무실 전화 - 온-프레미스 디렉터리와 동기화하지 않는 경우에만 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e2a3-136">Office Phone - Can only be set if not synchronizing with an on-premises directory</span></span>

### <a name="using-powershell-v1"></a><span data-ttu-id="9e2a3-137">PowerShell V1 사용</span><span class="sxs-lookup"><span data-stu-id="9e2a3-137">Using PowerShell V1</span></span>

<span data-ttu-id="9e2a3-138">시작 tooget, 필요한 너무[다운로드 하 여 hello Azure AD PowerShell 모듈이 설치](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule)합니다.</span><span class="sxs-lookup"><span data-stu-id="9e2a3-138">tooget started, you need too[download and install hello Azure AD PowerShell module](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span></span> <span data-ttu-id="9e2a3-139">설치 되어 있으면 tooconfigure 각 필드는 hello 단계를 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e2a3-139">Once you have it installed, you can follow hello steps that follow tooconfigure each field.</span></span>

#### <a name="set-authentication-data-with-powershell-v1"></a><span data-ttu-id="9e2a3-140">PowerShell V1을 사용하여 인증 데이터 설정</span><span class="sxs-lookup"><span data-stu-id="9e2a3-140">Set Authentication Data with PowerShell V1</span></span>

```
Connect-MsolService

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com")
Set-MsolUser -UserPrincipalName user@domain.com -MobilePhone "+1 1234567890"
Set-MsolUser -UserPrincipalName user@domain.com -PhoneNumber "+1 1234567890"

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com") -MobilePhone "+1 1234567890" -PhoneNumber "+1 1234567890"
```

#### <a name="read-authentication-data-with-powershellpowershell-v1"></a><span data-ttu-id="9e2a3-141">PowerShell V1을 사용하여 인증 데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="9e2a3-141">Read Authentication Data with PowerShellPowerShell V1</span></span>

```
Connect-MsolService

Get-MsolUser -UserPrincipalName user@domain.com | select AlternateEmailAddresses
Get-MsolUser -UserPrincipalName user@domain.com | select MobilePhone
Get-MsolUser -UserPrincipalName user@domain.com | select PhoneNumber

Get-MsolUser | select DisplayName,UserPrincipalName,AlternateEmailAddresses,MobilePhone,PhoneNumber | Format-Table
```

#### <a name="authentication-phone-and-authentication-email-can-only-be-read-using-powershell-v1-using-hello-commands-that-follow"></a><span data-ttu-id="9e2a3-142">인증 전화 및 인증 전자 메일 읽을 수만 있고 Powershell v 1을 사용 하 여 다음에 나오는 명령 hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="9e2a3-142">Authentication Phone and Authentication Email can only be read using Powershell V1 using hello commands that follow</span></span>

```
Connect-MsolService
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select PhoneNumber
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select Email
```

### <a name="using-powershell-v2"></a><span data-ttu-id="9e2a3-143">PowerShell V2 사용</span><span class="sxs-lookup"><span data-stu-id="9e2a3-143">Using PowerShell V2</span></span>

<span data-ttu-id="9e2a3-144">시작 tooget, 필요한 너무[다운로드 하 여 Azure AD V2 hello PowerShell 모듈 설치](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9e2a3-144">tooget started, you need too[download and install hello Azure AD V2 PowerShell module](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md).</span></span> <span data-ttu-id="9e2a3-145">설치 되어 있으면 tooconfigure 각 필드는 hello 단계를 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e2a3-145">Once you have it installed, you can follow hello steps that follow tooconfigure each field.</span></span>

<span data-ttu-id="9e2a3-146">Install-module을 지 원하는 최신 버전의 PowerShell에서 신속 하 게 tooinstall (첫 번째 줄 hello 단순히 검사 toosee 이미 설치 되어 있는 경우) 이러한 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e2a3-146">tooinstall quickly from recent versions of PowerShell that support Install-Module, run these commands (hello first line simply checks toosee if it's installed already):</span></span>

```
Get-Module AzureADPreview
Install-Module AzureADPreview
Connect-AzureAD
```

#### <a name="set-authentication-data-with-powershell-v2"></a><span data-ttu-id="9e2a3-147">PowerShell V2를 사용하여 인증 데이터 설정</span><span class="sxs-lookup"><span data-stu-id="9e2a3-147">Set Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("email@domain.com")
Set-AzureADUser -ObjectId user@domain.com -Mobile "+1 2345678901"
Set-AzureADUser -ObjectId user@domain.com -TelephoneNumber "+1 1234567890"

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("emails@domain.com") -Mobile "+1 1234567890" -TelephoneNumber "+1 1234567890"
```

### <a name="read-authentication-data-with-powershell-v2"></a><span data-ttu-id="9e2a3-148">PowerShell V2를 사용하여 인증 데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="9e2a3-148">Read Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Get-AzureADUser -ObjectID user@domain.com | select otherMails
Get-AzureADUser -ObjectID user@domain.com | select Mobile
Get-AzureADUser -ObjectID user@domain.com | select TelephoneNumber

Get-AzureADUser | select DisplayName,UserPrincipalName,otherMails,Mobile,TelephoneNumber | Format-Table
```

## <a name="next-steps"></a><span data-ttu-id="9e2a3-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9e2a3-149">Next steps</span></span>

<span data-ttu-id="9e2a3-150">링크를 따라 hello Azure AD를 사용 하 여 다시 설정 하는 암호에 대 한 추가 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e2a3-150">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="9e2a3-151">[**빠른 시작**](active-directory-passwords-getting-started.md) - Azure AD 셀프 서비스 암호 관리를 사용하여 운영 시작</span><span class="sxs-lookup"><span data-stu-id="9e2a3-151">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="9e2a3-152">[**라이선스**](active-directory-passwords-licensing.md) - Azure AD 라이선스 구성</span><span class="sxs-lookup"><span data-stu-id="9e2a3-152">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="9e2a3-153">[**롤아웃** ](active-directory-passwords-best-practices.md) -계획 및 배포 ´ ֿ ´ hello 지침을 사용 하 여 SSPR tooyour 사용자</span><span class="sxs-lookup"><span data-stu-id="9e2a3-153">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="9e2a3-154">[**사용자 지정** ](active-directory-passwords-customize.md) -hello SSPR 귀사에 대 한 경험의 hello 모양과 느낌을 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e2a3-154">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="9e2a3-155">[**정책**](active-directory-passwords-policy.md) - Azure AD 암호 정책을 이해하고 설정</span><span class="sxs-lookup"><span data-stu-id="9e2a3-155">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="9e2a3-156">[**보고**](active-directory-passwords-reporting.md) - 사용자가 SSPR 기능에 액세스하는 조건, 시간 및 위치 탐색</span><span class="sxs-lookup"><span data-stu-id="9e2a3-156">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="9e2a3-157">[**기술 심층 분석** ](active-directory-passwords-how-it-works.md) -이동 hello 커튼 toounderstand 뒤 작동 방법</span><span class="sxs-lookup"><span data-stu-id="9e2a3-157">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="9e2a3-158">[**질문과 대답**](active-directory-passwords-faq.md) - 어떤 방식으로?</span><span class="sxs-lookup"><span data-stu-id="9e2a3-158">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="9e2a3-159">그 이유는</span><span class="sxs-lookup"><span data-stu-id="9e2a3-159">Why?</span></span> <span data-ttu-id="9e2a3-160">무엇을?</span><span class="sxs-lookup"><span data-stu-id="9e2a3-160">What?</span></span> <span data-ttu-id="9e2a3-161">어디서?</span><span class="sxs-lookup"><span data-stu-id="9e2a3-161">Where?</span></span> <span data-ttu-id="9e2a3-162">누가?</span><span class="sxs-lookup"><span data-stu-id="9e2a3-162">Who?</span></span> <span data-ttu-id="9e2a3-163">언제?</span><span class="sxs-lookup"><span data-stu-id="9e2a3-163">When?</span></span> <span data-ttu-id="9e2a3-164">-Tooask 항상 필요한 tooquestions 답변</span><span class="sxs-lookup"><span data-stu-id="9e2a3-164">- Answers tooquestions you always wanted tooask</span></span>
* <span data-ttu-id="9e2a3-165">[**문제를 해결** ](active-directory-passwords-troubleshoot.md) -SSPR으로 보면 tooresolve 공통을 발급 하는 방법에 대해 알아봅니다</span><span class="sxs-lookup"><span data-stu-id="9e2a3-165">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>
