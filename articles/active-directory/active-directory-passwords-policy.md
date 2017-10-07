---
title: "정책: Azure AD SSPR | Microsoft Docs"
description: "Azure AD 셀프 서비스 암호 재설정 정책 옵션"
services: active-directory
keywords: "Active Directory 암호 관리, 암호 관리, Azure AD 셀프 서비스 암호 재설정"
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
ms.openlocfilehash: af7cb13794bf3a9fee91d355f788aa5c2246e57c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="password-policies-and-restrictions-in-azure-active-directory"></a>Azure Active Directory에서 암호 정책 및 제한

이 문서에서는 hello 암호 정책 및 Azure AD 테 넌 트에 저장 된 사용자 계정과 관련 된 복잡성 요구 사항을 설명 합니다.

## <a name="administrator-password-policy-differences"></a>관리자 암호 정책 차이점

Microsoft는 모든 Azure 관리자 역할(예: 전역 관리자, 기술 지원팀 관리자, 암호 관리자 등)에 강력한 기본 암호 재설정 **두 개의 게이트** 정책을 적용합니다.

이 관리자가 보안 질문을 사용 하 여 사용 하지 않도록 설정 하 고 hello 다음을 적용 합니다.

두 가지 인증 데이터를 요구 하는 정책을 제어 두 (전자 메일 주소 **및** 전화 번호), hello 다음 상황에에서 적용 됩니다.

* 모든 Azure 관리자 역할
  * 기술 지원팀 관리자
  * 서비스 지원 관리자
  * 대금 청구 관리자
  * 파트너 계층1 지원
  * 파트너 계층2 지원
  * Exchange 서비스 관리자
  * Lync 서비스 관리자
  * 사용자 계정 관리자
  * 디렉터리 작성자
  * 전역 관리자/회사 관리자
  * SharePoint 서비스 관리자
  * 규정 준수 관리자
  * 응용 프로그램 관리자
  * 보안 관리자
  * 권한 있는 역할 관리자
  * Intune 서비스 관리자
  * 응용 프로그램 프록시 서비스 관리자
  * CRM 서비스 관리자
  * Power BI 서비스 관리자
  
* 평가판에서 30일 경과 **또는**
* 베니티 도메인이 있는 경우(contoso.com) **또는**
* Azure AD Connect가 온-프레미스 디렉터리에서 ID를 동기화하는 경우

### <a name="exceptions"></a>예외
인증 데이터의 한 부분을 요구 하는 하나의 게이트 정책이 (전자 메일 주소 **또는** 전화 번호), 상황에 따라 hello에 적용 됩니다.

* 첫 번째 30일 평가판 **또는**
* 베니티 도메인이 없는 경우(*.onmicrosoft.com) **및** Azure AD Connect가 ID를 동기화하지 않는 경우


## <a name="userprincipalname-policies-that-apply-tooall-user-accounts"></a>Tooall 사용자 계정에 적용 되는 UserPrincipalName 정책

모든 사용자 계정에 필요한 toosign tooAzure AD에서에서 자신의 계정과 연결 된 고유한 사용자 계정 이름 (UPN) 특성 값에 있어야 합니다. tooboth 적용 hello 정책을 윤곽선 아래 hello 표 온-프레미스 Active Directory 사용자 계정이 toohello 클라우드와 toocloud 전용 사용자 계정을 동기화 합니다.

| 속성 | UserPrincipalName 요구 사항 |
| --- | --- |
| 허용되는 문자 |<ul> <li>A-Z</li> <li>a-z</li><li>0-9</li> <li> 등 4가지 유형의 클러스터가 제공됩니다. - \_ ! \# ^ \~</li></ul> |
| 허용되지 않는 문자 |<ul> <li>모든 ' @' hello 도메인에서 사용자 이름을 hello를 구분 하는 문자입니다.</li> <li>마침표 문자를 포함할 수 없습니다 '.' 바로 이전 hello ' @' 기호</li></ul> |
| 길이 제약 조건 |<ul> <li>총 길이는 113자를 초과할 수 없습니다.</li><li>hello 하기 전에 64 자 ' @' 기호</li><li>hello 후 48 자 ' @' 기호</li></ul> |

## <a name="password-policies-that-apply-only-toocloud-user-accounts"></a>Toocloud 사용자 계정에만 적용 되는 암호 정책

다음 표에서 hello 적용된 toouser 계정을 만들고 Azure AD에서 관리 되는 일 수 있는 hello 사용 가능 암호 정책 설정 설명 합니다.

| 속성 | 요구 사항 |
| --- | --- |
| 허용되는 문자 |<ul><li>A-Z</li><li>a-z</li><li>0-9</li> <li>@ # $ % ^ & * - _ ! + = [ ] { } &#124; \ : ‘ , . ? / ` ~ “ ( ) ;</li></ul> |
| 허용되지 않는 문자 |<ul><li>유니코드 문자</li><li>공백</li><li> **강력한 암호에만**: 점 문자를 포함할 수 없습니다 '.' 바로 이전 hello ' @' 기호</li></ul> |
| 암호 제한 |<ul><li>최소 8자 및 최대 16자</li><li>**강력한 암호에만**: 4 hello 다음 중에서 3 필요 합니다.<ul><li>소문자</li><li>대문자</li><li>숫자(0-9)</li><li>기호(위 암호 제한 참조)</li></ul></li></ul> |
| 암호 만료 기간 |<ul><li>기본값: **90**일 </li><li>값은 hello Azure Active Directory에 대 한 Windows PowerShell 모듈에서에서 Set-msolpasswordpolicy hello cmdlet을 사용 하 여 구성할 수 있습니다.</li></ul> |
| 암호 만료 알림 |<ul><li>기본값: **14**일(암호 만료 이전)</li><li>값은 hello Set-msolpasswordpolicy cmdlet을 사용 하 여 구성할 수 있습니다.</li></ul> |
| 암호 만료 |<ul><li>기본값: **false**일(사용 가능한 암호 만료임을 나타냄) </li><li>Hello Set-msoluser cmdlet을 사용 하 여 개별 사용자 계정에 대 한 값을 구성할 수 있습니다. </li></ul> |
| 암호 **변경** 기록 |암호를 **변경**한 경우 마지막 암호는 다시 **사용할 수 없습니다**. |
| 암호 **재설정** 기록 | 잊은 암호를 **다시 설정**하면 마지막 암호를 다시 사용**할 수도** 있습니다. |
| 계정 잠금 |10 개의 실패 한 로그인 시도 후 (잘못 된 암호) hello 사용자는 잠겨 1 분이 걸립니다. 더 이상 잘못 된 로그인 hello 사용자 잠금 기간을 높이기 위한 시도 합니다. |

## <a name="set-password-expiration-policies-in-azure-active-directory"></a>Azure Active Directory에서 암호 만료 정책 설정

Microsoft 클라우드 서비스에 대 한 전역 관리자 하지 tooexpire 사용자 암호를 Microsoft Azure Active Directory에 대 한 Windows PowerShell 모듈 tooset hello를 사용할 수 있습니다. Windows PowerShell cmdlet tooremove hello 제한 구성 또는 toosee 하지 tooexpire 설정 어떤 사용자 암호를 사용할 수 있습니다. 이 설명서에는 또한 id 및 디렉터리 서비스에 대 한 Microsoft Azure Active Directory를 사용 하는 Microsoft Intune 및 Office 365와 같은 tooother 공급자 적용 됩니다.

> [!NOTE]
> 암호만 toonot 만료에 디렉터리 동기화를 통해 동기화 되지 않은 사용자 계정을 구성할 수 있습니다. 디렉터리 동기화에 대한 자세한 내용은 [Azure AD와 AD 연결](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)을 참조하세요.
>
>

## <a name="set-or-check-password-policies-using-powershell"></a>PowerShell을 사용하여 암호 정책 설정 또는 확인

시작 tooget, 필요한 너무[다운로드 하 여 hello Azure AD PowerShell 모듈이 설치](https://docs.microsoft.com/powershell/module/Azuread/?view=azureadps-2.0)합니다. 설치 되어 있으면 각 필드 tooconfigure 아래 hello 단계를 따를 수 있습니다.

### <a name="how-toocheck-expiration-policy-for-a-password"></a>방식 암호 만료 정책을 toocheck
1. 회사 관리자 자격 증명을 사용 하 여 PowerShell tooWindows를 연결 합니다.
2. Hello 다음 명령 중 하나를 실행 합니다.

   * toosee 만료는 단일 사용자의 암호가 toonever에 설정 되어 있는지 여부, hello cmdlet hello 사용자 계정 이름 (UPN)을 사용 하 여 다음을 실행 (예를 들어 aprilr@contoso.onmicrosoft.com) 또는 사용자 ID를 환영 toocheck hello 사용자의 원하는:`Get-MSOLUser -UserPrincipalName <user ID> | Select PasswordNeverExpires`
   * toosee 모든 사용자에 대 한 설정을 "암호 사용 기간 제한 없음" hello, hello 다음 cmdlet을 실행 합니다.`Get-MSOLUser | Select UserPrincipalName, PasswordNeverExpires`

### <a name="set-a-password-tooexpire"></a>암호 tooexpire 설정

1. 회사 관리자 자격 증명을 사용 하 여 PowerShell tooWindows를 연결 합니다.
2. Hello 다음 명령 중 하나를 실행 합니다.

   * 사용자의 tooset hello 암호 hello 암호가 만료 되 면 hello cmdlet hello 사용자 계정 이름 (UPN)을 사용 하 여 다음을 실행 또는 되도록 hello hello 사용자의 사용자 ID:`Set-MsolUser -UserPrincipalName <user ID> -PasswordNeverExpires $false`
   * hello 조직의 모든 사용자의 tooset hello 암호 만료 될 수 있도록 hello cmdlet을 다음 사용 합니다.`Get-MSOLUser | Set-MsolUser -PasswordNeverExpires $false`

### <a name="set-a-password-toonever-expire"></a>암호 toonever 세트가 만료

1. 회사 관리자 자격 증명을 사용 하 여 PowerShell tooWindows를 연결 합니다.
2. Hello 다음 명령 중 하나를 실행 합니다.

   * 한 명의 사용자 toonever의 tooset hello 암호 만료, hello cmdlet hello 사용자 계정 이름 (UPN)을 사용 하 여 다음을 실행 또는 hello hello 사용자의 사용자 ID:`Set-MsolUser -UserPrincipalName <user ID> -PasswordNeverExpires $true`
   * 모든 조직 toonever hello 사용자의 tooset hello 암호 만료, hello 다음 cmdlet을 실행 합니다.`Get-MSOLUser | Set-MsolUser -PasswordNeverExpires $true`

## <a name="next-steps"></a>다음 단계

링크를 따라 hello Azure AD를 사용 하 여 다시 설정 하는 암호에 대 한 추가 정보를 제공 합니다.

* [**빠른 시작**](active-directory-passwords-getting-started.md) - Azure AD 셀프 서비스 암호 관리를 사용하여 운영 시작 
* [**라이선스**](active-directory-passwords-licensing.md) - Azure AD 라이선스 구성
* [**데이터** ](active-directory-passwords-data.md) -hello 필요한 데이터를 이해 하 고 암호 관리에 대 한 사용 방법
* [**롤아웃** ](active-directory-passwords-best-practices.md) -계획 및 배포 ´ ֿ ´ hello 지침을 사용 하 여 SSPR tooyour 사용자
* [**사용자 지정** ](active-directory-passwords-customize.md) -hello SSPR 귀사에 대 한 경험의 hello 모양과 느낌을 사용자 지정 합니다.
* [**보고**](active-directory-passwords-reporting.md) - 사용자가 SSPR 기능에 액세스하는 조건, 시간 및 위치 탐색
* [**기술 심층 분석** ](active-directory-passwords-how-it-works.md) -이동 hello 커튼 toounderstand 뒤 작동 방법
* [**질문과 대답**](active-directory-passwords-faq.md) - 어떤 방식으로? 그 이유는 무엇을? 어디서? 누가? 언제? -Tooask 항상 필요한 tooquestions 답변
* [**문제를 해결** ](active-directory-passwords-troubleshoot.md) -SSPR으로 보면 tooresolve 공통을 발급 하는 방법에 대해 알아봅니다
