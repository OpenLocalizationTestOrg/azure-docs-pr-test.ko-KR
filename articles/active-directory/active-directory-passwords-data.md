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
# <a name="deploy-password-reset-without-requiring-end-user-registration"></a>최종 사용자를 등록할 필요 없이 암호 재설정 배포

셀프 서비스 암호 재설정 (SSPR)를 배포 하려면 인증 데이터 toobe 존재 합니다. 일부 조직에는 사용자가 인증 데이터를 직접 입력 해도 되지만 대부분의 조직에서는 Active Directory의 기존 데이터와 toosynchronize. 가 적절 한 형식의 데이터가 온-프레미스 디렉터리에 구성 하는 경우 [기본 설정을 사용 하는 Azure AD Connect](./connect/active-directory-aadconnect-get-started-express.md), 데이터를 사용할 수 있는 tooAzure AD 하 수와 필요한 사용자 조작 없이 SSPR 합니다.

Hello 형식 + CountryCode PhoneNumber 예제에 전화 번호가 있어야: + 1 4255551234 toowork 제대로 합니다.

> [!NOTE]
> 암호 재설정은 전화 번호 확장을 지원하지 않습니다. Hello + 1 4255551234 X 12345 형식에도 확장 hello 전화를 건 전에 제거 됩니다.

## <a name="fields-populated"></a>채워진 필드

Hello 기본 설정을 사용 하 여 Azure AD Connect hello 뒤에서 매핑이 수행 됩니다.

| 온-프레미스 AD | Azure AD | Azure AD 인증 연락처 정보 |
| --- | --- | --- |
| telephoneNumber | 사무실 전화 | 대체 전화 |
| mobile | 휴대폰 | Phone |


## <a name="security-questions-and-answers"></a>보안 질문 및 답변

Azure AD 테 넌 트에 안전 하 게 저장 되 고 hello 통해 액세스할 수 있는 toousers만는 보안 질문 및 답변 [SSPR 등록 포털](https://aka.ms/ssprsetup)합니다. 관리자가 보거나 다른 사용자가 질문 및 답변의 hello 내용을 수정할 수 없습니다.

### <a name="what-happens-when-a-user-registers"></a>사용자가 등록하면 어떻게 되나요?

사용자가 등록할 때 다음 필드는 hello hello 등록 페이지에 설정 합니다.

* 인증 전화
* 인증 전자 메일
* 보안 질문 및 답변

에 대 한 값을 제공 하면 **휴대폰** 또는 **암호 확인용 메일**, 사용자가 즉시 사용할 수 있습니다 이러한 값 tooreset 암호, hello 서비스에 대 한 등록 되지 않은 경우에 합니다. 또한 사용자 hello에 대 한 처음으로 등록 하는 경우 해당 값을 볼 수 있으며 만들려는 경우 수정 합니다. 이러한 값이 hello에 영구 저장 해야 성공적으로 등록 될 **인증 전화** 및 **인증 전자 메일** 필드를 각각.

## <a name="set-and-read-authentication-data-using-powershell"></a>PowerShell을 사용하여 인증 데이터 설정 및 읽기

PowerShell을 사용 하 여 hello 다음 필드를 설정할 수 있습니다.

* 대체 전자 메일
* 휴대폰
* 사무실 전화 - 온-프레미스 디렉터리와 동기화하지 않는 경우에만 설정할 수 있습니다.

### <a name="using-powershell-v1"></a>PowerShell V1 사용

시작 tooget, 필요한 너무[다운로드 하 여 hello Azure AD PowerShell 모듈이 설치](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule)합니다. 설치 되어 있으면 tooconfigure 각 필드는 hello 단계를 따를 수 있습니다.

#### <a name="set-authentication-data-with-powershell-v1"></a>PowerShell V1을 사용하여 인증 데이터 설정

```
Connect-MsolService

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com")
Set-MsolUser -UserPrincipalName user@domain.com -MobilePhone "+1 1234567890"
Set-MsolUser -UserPrincipalName user@domain.com -PhoneNumber "+1 1234567890"

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com") -MobilePhone "+1 1234567890" -PhoneNumber "+1 1234567890"
```

#### <a name="read-authentication-data-with-powershellpowershell-v1"></a>PowerShell V1을 사용하여 인증 데이터 읽기

```
Connect-MsolService

Get-MsolUser -UserPrincipalName user@domain.com | select AlternateEmailAddresses
Get-MsolUser -UserPrincipalName user@domain.com | select MobilePhone
Get-MsolUser -UserPrincipalName user@domain.com | select PhoneNumber

Get-MsolUser | select DisplayName,UserPrincipalName,AlternateEmailAddresses,MobilePhone,PhoneNumber | Format-Table
```

#### <a name="authentication-phone-and-authentication-email-can-only-be-read-using-powershell-v1-using-hello-commands-that-follow"></a>인증 전화 및 인증 전자 메일 읽을 수만 있고 Powershell v 1을 사용 하 여 다음에 나오는 명령 hello를 사용 하 여

```
Connect-MsolService
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select PhoneNumber
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select Email
```

### <a name="using-powershell-v2"></a>PowerShell V2 사용

시작 tooget, 필요한 너무[다운로드 하 여 Azure AD V2 hello PowerShell 모듈 설치](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md)합니다. 설치 되어 있으면 tooconfigure 각 필드는 hello 단계를 따를 수 있습니다.

Install-module을 지 원하는 최신 버전의 PowerShell에서 신속 하 게 tooinstall (첫 번째 줄 hello 단순히 검사 toosee 이미 설치 되어 있는 경우) 이러한 명령을 실행 합니다.

```
Get-Module AzureADPreview
Install-Module AzureADPreview
Connect-AzureAD
```

#### <a name="set-authentication-data-with-powershell-v2"></a>PowerShell V2를 사용하여 인증 데이터 설정

```
Connect-AzureAD

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("email@domain.com")
Set-AzureADUser -ObjectId user@domain.com -Mobile "+1 2345678901"
Set-AzureADUser -ObjectId user@domain.com -TelephoneNumber "+1 1234567890"

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("emails@domain.com") -Mobile "+1 1234567890" -TelephoneNumber "+1 1234567890"
```

### <a name="read-authentication-data-with-powershell-v2"></a>PowerShell V2를 사용하여 인증 데이터 읽기

```
Connect-AzureAD

Get-AzureADUser -ObjectID user@domain.com | select otherMails
Get-AzureADUser -ObjectID user@domain.com | select Mobile
Get-AzureADUser -ObjectID user@domain.com | select TelephoneNumber

Get-AzureADUser | select DisplayName,UserPrincipalName,otherMails,Mobile,TelephoneNumber | Format-Table
```

## <a name="next-steps"></a>다음 단계

링크를 따라 hello Azure AD를 사용 하 여 다시 설정 하는 암호에 대 한 추가 정보를 제공 합니다.

* [**빠른 시작**](active-directory-passwords-getting-started.md) - Azure AD 셀프 서비스 암호 관리를 사용하여 운영 시작 
* [**라이선스**](active-directory-passwords-licensing.md) - Azure AD 라이선스 구성
* [**롤아웃** ](active-directory-passwords-best-practices.md) -계획 및 배포 ´ ֿ ´ hello 지침을 사용 하 여 SSPR tooyour 사용자
* [**사용자 지정** ](active-directory-passwords-customize.md) -hello SSPR 귀사에 대 한 경험의 hello 모양과 느낌을 사용자 지정 합니다.
* [**정책**](active-directory-passwords-policy.md) - Azure AD 암호 정책을 이해하고 설정
* [**보고**](active-directory-passwords-reporting.md) - 사용자가 SSPR 기능에 액세스하는 조건, 시간 및 위치 탐색
* [**기술 심층 분석** ](active-directory-passwords-how-it-works.md) -이동 hello 커튼 toounderstand 뒤 작동 방법
* [**질문과 대답**](active-directory-passwords-faq.md) - 어떤 방식으로? 그 이유는 무엇을? 어디서? 누가? 언제? -Tooask 항상 필요한 tooquestions 답변
* [**문제를 해결** ](active-directory-passwords-troubleshoot.md) -SSPR으로 보면 tooresolve 공통을 발급 하는 방법에 대해 알아봅니다
