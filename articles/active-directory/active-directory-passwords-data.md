---
title: "Azure AD SSPR 데이터 요구 사항 | Microsoft Docs"
description: "Azure AD 셀프 서비스 암호 재설정의 데이터 요구 사항 및 충족 방법"
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
ms.openlocfilehash: 2d1afd2d1265b371e0d311ed70fffbc55874b0a7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-password-reset-without-requiring-end-user-registration"></a><span data-ttu-id="8a4de-103">최종 사용자를 등록할 필요 없이 암호 재설정 배포</span><span class="sxs-lookup"><span data-stu-id="8a4de-103">Deploy password reset without requiring end-user registration</span></span>

<span data-ttu-id="8a4de-104">SSPR(셀프 서비스 암호 재설정)을 배포하려면 인증 데이터가 존재해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4de-104">Deploying Self-Service Password Reset (SSPR) requires authentication data to be present.</span></span> <span data-ttu-id="8a4de-105">일부 조직에서는 해당 사용자가 해당 인증 데이터를 입력하도록 하지만 대부분의 조직에서는 Active Directory에서 기존 데이터와 동기화하는 것을 선호합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4de-105">Some organizations have their users enter their authentication data themselves, but many organizations prefer to synchronize with existing data in Active Directory.</span></span> <span data-ttu-id="8a4de-106">온-프레미스 디렉터리에 적절한 형식의 데이터가 있고 [빠른 설정을 사용하여 Azure AD Connect](./connect/active-directory-aadconnect-get-started-express.md)를 구성하는 경우 사용자 조작 없이 Azure AD 및 SSPR에 해당 데이터를 사용할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a4de-106">If you have properly formatted data in your on-premises directory, and configure [Azure AD Connect using express settings](./connect/active-directory-aadconnect-get-started-express.md), that data is made available to Azure AD and SSPR with no user interaction required.</span></span>

<span data-ttu-id="8a4de-107">전화 번호가 제대로 작동하려면 +국가 코드 전화 번호 형식이어야 합니다(예: +1 4255551234).</span><span class="sxs-lookup"><span data-stu-id="8a4de-107">Any phone numbers must be in the format +CountryCode PhoneNumber Example: +1 4255551234 to work properly.</span></span>

> [!NOTE]
> <span data-ttu-id="8a4de-108">암호 재설정은 전화 번호 확장을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4de-108">Password reset does not support phone extensions.</span></span> <span data-ttu-id="8a4de-109">+1 4255551234X12345 형식에서도 전화를 걸지 전에 확장이 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a4de-109">Even in the +1 4255551234X12345 format, extensions are removed before the call is placed.</span></span>

## <a name="fields-populated"></a><span data-ttu-id="8a4de-110">채워진 필드</span><span class="sxs-lookup"><span data-stu-id="8a4de-110">Fields populated</span></span>

<span data-ttu-id="8a4de-111">Azure AD Connect에서 기본 설정을 사용하는 경우 다음 매핑이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a4de-111">If you use the default settings in Azure AD Connect the following mappings are made.</span></span>

| <span data-ttu-id="8a4de-112">온-프레미스 AD</span><span class="sxs-lookup"><span data-stu-id="8a4de-112">On-premises AD</span></span> | <span data-ttu-id="8a4de-113">Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a4de-113">Azure AD</span></span> | <span data-ttu-id="8a4de-114">Azure AD 인증 연락처 정보</span><span class="sxs-lookup"><span data-stu-id="8a4de-114">Azure AD Authentication contact info</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8a4de-115">telephoneNumber</span><span class="sxs-lookup"><span data-stu-id="8a4de-115">telephoneNumber</span></span> | <span data-ttu-id="8a4de-116">사무실 전화</span><span class="sxs-lookup"><span data-stu-id="8a4de-116">Office phone</span></span> | <span data-ttu-id="8a4de-117">대체 전화</span><span class="sxs-lookup"><span data-stu-id="8a4de-117">Alternate phone</span></span> |
| <span data-ttu-id="8a4de-118">mobile</span><span class="sxs-lookup"><span data-stu-id="8a4de-118">mobile</span></span> | <span data-ttu-id="8a4de-119">휴대폰</span><span class="sxs-lookup"><span data-stu-id="8a4de-119">Mobile phone</span></span> | <span data-ttu-id="8a4de-120">Phone</span><span class="sxs-lookup"><span data-stu-id="8a4de-120">Phone</span></span> |


## <a name="security-questions-and-answers"></a><span data-ttu-id="8a4de-121">보안 질문 및 답변</span><span class="sxs-lookup"><span data-stu-id="8a4de-121">Security questions and answers</span></span>

<span data-ttu-id="8a4de-122">보안 질문 및 답변은 Azure AD 테넌트에 안전하게 저장되며 사용자가 [SSPR 등록 포털](https://aka.ms/ssprsetup)을 통해서만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4de-122">Security questions and answers are stored securely in your Azure AD tenant and are only accessible to users via the [SSPR registration portal](https://aka.ms/ssprsetup).</span></span> <span data-ttu-id="8a4de-123">관리자는 다른 사용자의 질문 및 답변의 내용을 보거나 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4de-123">Administrators can't see or modify the contents of another users questions and answers.</span></span>

### <a name="what-happens-when-a-user-registers"></a><span data-ttu-id="8a4de-124">사용자가 등록하면 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="8a4de-124">What happens when a user registers</span></span>

<span data-ttu-id="8a4de-125">사용자가 등록하면 등록 페이지에서 다음 필드를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4de-125">When a user registers, the registration page sets the following fields:</span></span>

* <span data-ttu-id="8a4de-126">인증 전화</span><span class="sxs-lookup"><span data-stu-id="8a4de-126">Authentication Phone</span></span>
* <span data-ttu-id="8a4de-127">인증 전자 메일</span><span class="sxs-lookup"><span data-stu-id="8a4de-127">Authentication Email</span></span>
* <span data-ttu-id="8a4de-128">보안 질문 및 답변</span><span class="sxs-lookup"><span data-stu-id="8a4de-128">Security Questions and Answers</span></span>

<span data-ttu-id="8a4de-129">**휴대폰** 또는 **대체 전자 메일**에 대한 값을 제공하면, 서비스에 등록하지 않은 사용자도 해당 값을 사용하여 자신의 암호를 즉시 재설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4de-129">If you have provided a value for **Mobile Phone** or **Alternate Email**, users can immediately use those values to reset their passwords, even if they haven't registered for the service.</span></span> <span data-ttu-id="8a4de-130">또한 사용자는 처음으로 등록할 때 해당 값을 볼 수 있고, 원하는 경우에는 값을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4de-130">In addition, users see those values when registering for the first time, and modify them if they wish.</span></span> <span data-ttu-id="8a4de-131">등록을 완료한 후에는 **인증 전화** 및 **인증 전자 메일** 필드에 해당하는 값이 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a4de-131">After they successfully register, these values will be persisted in the **Authentication Phone** and **Authentication Email** fields, respectively.</span></span>

## <a name="set-and-read-authentication-data-using-powershell"></a><span data-ttu-id="8a4de-132">PowerShell을 사용하여 인증 데이터 설정 및 읽기</span><span class="sxs-lookup"><span data-stu-id="8a4de-132">Set and read authentication data using PowerShell</span></span>

<span data-ttu-id="8a4de-133">PowerShell을 사용하여 다음 필드를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4de-133">The following fields can be set using PowerShell</span></span>

* <span data-ttu-id="8a4de-134">대체 전자 메일</span><span class="sxs-lookup"><span data-stu-id="8a4de-134">Alternate Email</span></span>
* <span data-ttu-id="8a4de-135">휴대폰</span><span class="sxs-lookup"><span data-stu-id="8a4de-135">Mobile Phone</span></span>
* <span data-ttu-id="8a4de-136">사무실 전화 - 온-프레미스 디렉터리와 동기화하지 않는 경우에만 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4de-136">Office Phone - Can only be set if not synchronizing with an on-premises directory</span></span>

### <a name="using-powershell-v1"></a><span data-ttu-id="8a4de-137">PowerShell V1 사용</span><span class="sxs-lookup"><span data-stu-id="8a4de-137">Using PowerShell V1</span></span>

<span data-ttu-id="8a4de-138">시작하려면 [Azure AD PowerShell 모듈을 다운로드하고 설치](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4de-138">To get started, you need to [download and install the Azure AD PowerShell module](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span></span> <span data-ttu-id="8a4de-139">설치를 완료한 후에는 다음 단계에 따라서 각 필드를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4de-139">Once you have it installed, you can follow the steps that follow to configure each field.</span></span>

#### <a name="set-authentication-data-with-powershell-v1"></a><span data-ttu-id="8a4de-140">PowerShell V1을 사용하여 인증 데이터 설정</span><span class="sxs-lookup"><span data-stu-id="8a4de-140">Set Authentication Data with PowerShell V1</span></span>

```
Connect-MsolService

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com")
Set-MsolUser -UserPrincipalName user@domain.com -MobilePhone "+1 1234567890"
Set-MsolUser -UserPrincipalName user@domain.com -PhoneNumber "+1 1234567890"

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com") -MobilePhone "+1 1234567890" -PhoneNumber "+1 1234567890"
```

#### <a name="read-authentication-data-with-powershellpowershell-v1"></a><span data-ttu-id="8a4de-141">PowerShell V1을 사용하여 인증 데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="8a4de-141">Read Authentication Data with PowerShellPowerShell V1</span></span>

```
Connect-MsolService

Get-MsolUser -UserPrincipalName user@domain.com | select AlternateEmailAddresses
Get-MsolUser -UserPrincipalName user@domain.com | select MobilePhone
Get-MsolUser -UserPrincipalName user@domain.com | select PhoneNumber

Get-MsolUser | select DisplayName,UserPrincipalName,AlternateEmailAddresses,MobilePhone,PhoneNumber | Format-Table
```

#### <a name="authentication-phone-and-authentication-email-can-only-be-read-using-powershell-v1-using-the-commands-that-follow"></a><span data-ttu-id="8a4de-142">다음과 같은 명령을 사용하는 PowerShell V1을 사용해야만 인증 전화 및 인증 전자 메일을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a4de-142">Authentication Phone and Authentication Email can only be read using Powershell V1 using the commands that follow</span></span>

```
Connect-MsolService
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select PhoneNumber
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select Email
```

### <a name="using-powershell-v2"></a><span data-ttu-id="8a4de-143">PowerShell V2 사용</span><span class="sxs-lookup"><span data-stu-id="8a4de-143">Using PowerShell V2</span></span>

<span data-ttu-id="8a4de-144">시작하려면 [Azure AD V2 PowerShell 모듈을 다운로드하고 설치](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4de-144">To get started, you need to [download and install the Azure AD V2 PowerShell module](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md).</span></span> <span data-ttu-id="8a4de-145">설치를 완료한 후에는 다음 단계에 따라서 각 필드를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4de-145">Once you have it installed, you can follow the steps that follow to configure each field.</span></span>

<span data-ttu-id="8a4de-146">Install-Module을 지원하는 최신 버전의 PowerShell을 신속하게 설치하려면 다음 명령을 실행합니다(첫 번째 줄은 해당 항목이 이미 설치되어 있는지 확인함).</span><span class="sxs-lookup"><span data-stu-id="8a4de-146">To install quickly from recent versions of PowerShell that support Install-Module, run these commands (the first line simply checks to see if it's installed already):</span></span>

```
Get-Module AzureADPreview
Install-Module AzureADPreview
Connect-AzureAD
```

#### <a name="set-authentication-data-with-powershell-v2"></a><span data-ttu-id="8a4de-147">PowerShell V2를 사용하여 인증 데이터 설정</span><span class="sxs-lookup"><span data-stu-id="8a4de-147">Set Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("email@domain.com")
Set-AzureADUser -ObjectId user@domain.com -Mobile "+1 2345678901"
Set-AzureADUser -ObjectId user@domain.com -TelephoneNumber "+1 1234567890"

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("emails@domain.com") -Mobile "+1 1234567890" -TelephoneNumber "+1 1234567890"
```

### <a name="read-authentication-data-with-powershell-v2"></a><span data-ttu-id="8a4de-148">PowerShell V2를 사용하여 인증 데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="8a4de-148">Read Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Get-AzureADUser -ObjectID user@domain.com | select otherMails
Get-AzureADUser -ObjectID user@domain.com | select Mobile
Get-AzureADUser -ObjectID user@domain.com | select TelephoneNumber

Get-AzureADUser | select DisplayName,UserPrincipalName,otherMails,Mobile,TelephoneNumber | Format-Table
```

## <a name="next-steps"></a><span data-ttu-id="8a4de-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8a4de-149">Next steps</span></span>

<span data-ttu-id="8a4de-150">다음 링크는 Azure AD를 사용한 암호 재설정에 대한 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8a4de-150">The following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="8a4de-151">[**빠른 시작**](active-directory-passwords-getting-started.md) - Azure AD 셀프 서비스 암호 관리를 사용하여 운영 시작</span><span class="sxs-lookup"><span data-stu-id="8a4de-151">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="8a4de-152">[**라이선스**](active-directory-passwords-licensing.md) - Azure AD 라이선스 구성</span><span class="sxs-lookup"><span data-stu-id="8a4de-152">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="8a4de-153">[**롤아웃**](active-directory-passwords-best-practices.md) - 여기서 제공하는 지침을 사용하여 배포 계획을 세우고 사용자에게 SSPR 배포</span><span class="sxs-lookup"><span data-stu-id="8a4de-153">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR to your users using the guidance found here</span></span>
* <span data-ttu-id="8a4de-154">[**사용자 지정**](active-directory-passwords-customize.md) - 회사 SSPR 경험의 모양과 느낌을 사용자 지정.</span><span class="sxs-lookup"><span data-stu-id="8a4de-154">[**Customize**](active-directory-passwords-customize.md) - Customize the look and feel of the SSPR experience for your company.</span></span>
* <span data-ttu-id="8a4de-155">[**정책**](active-directory-passwords-policy.md) - Azure AD 암호 정책을 이해하고 설정</span><span class="sxs-lookup"><span data-stu-id="8a4de-155">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="8a4de-156">[**보고**](active-directory-passwords-reporting.md) - 사용자가 SSPR 기능에 액세스하는 조건, 시간 및 위치 탐색</span><span class="sxs-lookup"><span data-stu-id="8a4de-156">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="8a4de-157">[**기술 심층 분석**](active-directory-passwords-how-it-works.md) - 작동 방식을 이해하기 위해 심층 분석</span><span class="sxs-lookup"><span data-stu-id="8a4de-157">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind the curtain to understand how it works</span></span>
* <span data-ttu-id="8a4de-158">[**질문과 대답**](active-directory-passwords-faq.md) - 어떤 방식으로?</span><span class="sxs-lookup"><span data-stu-id="8a4de-158">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="8a4de-159">그 이유는</span><span class="sxs-lookup"><span data-stu-id="8a4de-159">Why?</span></span> <span data-ttu-id="8a4de-160">무엇을?</span><span class="sxs-lookup"><span data-stu-id="8a4de-160">What?</span></span> <span data-ttu-id="8a4de-161">어디서?</span><span class="sxs-lookup"><span data-stu-id="8a4de-161">Where?</span></span> <span data-ttu-id="8a4de-162">누가?</span><span class="sxs-lookup"><span data-stu-id="8a4de-162">Who?</span></span> <span data-ttu-id="8a4de-163">언제?</span><span class="sxs-lookup"><span data-stu-id="8a4de-163">When?</span></span> <span data-ttu-id="8a4de-164">- 많은 분들이 항상 묻는 질문에 대한 답변입니다.</span><span class="sxs-lookup"><span data-stu-id="8a4de-164">- Answers to questions you always wanted to ask</span></span>
* <span data-ttu-id="8a4de-165">[**문제 해결**](active-directory-passwords-troubleshoot.md) - SSPR의 일반적인 문제 해결 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="8a4de-165">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how to resolve common issues that we see with SSPR</span></span>
