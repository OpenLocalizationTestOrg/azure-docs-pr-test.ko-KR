---
title: "Azure AD Connect: Seamless Single Sign-On Single Sign-On - FAQ(질문과 대답) | Microsoft Docs"
description: "대답 toofrequently 묻는 질문에 대 한 Azure Active Directory 원활한 Single Sign-on입니다."
services: active-directory
keywords: "Azure AD Connect의 정의, Active Directory 설치, Azure AD에 대한 필수 구성 요소, SSO, Single Sign-on"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: e91e7950670633c08c180ece873f7451fa19eef8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-frequently-asked-questions"></a>Azure Active Directory Seamless Single Sign-On: FAQ(질문과 대답)

이 문서에서는 Azure Active Directory Seamless SSO(Seamless Single Sign-On)에 대한 질문과 대답을 다룹니다. 새로운 내용을 계속 확인해 주세요.

>[!IMPORTANT]
>hello 원활한 SSO 기능은 현재 미리 보기 중입니다.

## <a name="what-sign-in-methods-do-seamless-sso-work-with"></a>Seamless SSO에서 사용되는 로그인 방법은 무엇인가요?

원활한 SSO 어느 hello 함께 사용할 [암호 해시 동기화](active-directory-aadconnectsync-implement-password-synchronization.md) 또는 [통과 인증](active-directory-aadconnect-pass-through-authentication.md) 로그인 방법이 있습니다. 그러나 AD FS(Active Directory Federation Services)에는 이 기능을 사용할 수 없습니다.

## <a name="is-seamless-sso-a-free-feature"></a>Seamless SSO는 평가판 체험 기능인가요?

원활한 SSO 무료 기능이 며 toouse Azure AD의 유료 버전 필요가 없는 것입니다. Hello 기능이 일반 공급 하는 경우 무료에 남아 있습니다.

## <a name="what-applications-take-advantage-of-domainhint-or-loginhint-parameter-capability-of-seamless-sso"></a>Seamless SSO의 `domain_hint` 또는 `login_hint` 매개 변수 기능을 활용하는 응용 프로그램은 무엇인가요?

Hello 목록은 이러한 매개 변수 및 hello 하지는 보내는 응용 프로그램을 컴파일 hello 과정에는 것입니다. 에 관심이 있는 응용 프로그램의 경우에 hello 설명 섹션에 알려 주십시오.

## <a name="does-seamless-sso-support-alternate-id-as-hello-username-instead-of-userprincipalname"></a>원활한 SSO ¿ø `Alternate ID` 사용자 이름 대신 hello 대로 `userPrincipalName`?

예. 원활한 SSO 지원 `Alternate ID` hello와 같이 Azure AD Connect에서 구성 된 경우 사용자 이름으로 [여기](active-directory-aadconnect-get-started-custom.md)합니다. 모든 Office 365 응용 프로그램에서 `Alternate ID`를 지원하지는 않습니다. Hello 지원 정책 toohello 특정 한 응용 프로그램의 설명서를 참조 하십시오.

## <a name="i-want-tooregister-non-windows-10-devices-with-azure-ad-without-using-ad-fs-can-i-use-seamless-sso-instead"></a>AD FS를 사용 하지 않고 Azure AD 사용 하 여 비-Windows 10 장치 tooregister 하겠습니다. Seamless SSO를 대신 사용할 수 있나요?

2.1 이상 hello 버전 필요한이 시나리오는 예, [작업 공간 연결 클라이언트](https://www.microsoft.com/download/details.aspx?id=53554)합니다.

## <a name="how-can-i-roll-over-hello-kerberos-decryption-key-of-hello-azureadssoacct-computer-account"></a>Hello의 hello Kerberos 암호 해독 키를 통해 롤백될 수는 어떻게 `AZUREADSSOACCT` 컴퓨터 계정을?

Toofrequently hello의 hello Kerberos 암호 해독 키를 롤오버할 반드시 `AZUREADSSOACCT` 컴퓨터 계정 (Azure AD를 나타냄) 온-프레미스에서 만든 AD 포리스트가 있습니다.

>[!IMPORTANT]
>배포 하기 hello Kerberos 암호 해독 키를 통해 30 일 마다 적어도 하는 것이 좋습니다.

Azure AD Connect를 실행 중인 hello 온-프레미스 서버에서 다음이 단계를 따릅니다.

### <a name="step-1-get-list-of-ad-forests-where-seamless-sso-has-been-enabled"></a>1단계. Seamless SSO가 사용하도록 설정된 AD 포리스트 목록을 가져옵니다.

1. 첫째, 다운로드 및 설치 hello [Microsoft Online Services 로그인 도우미](http://go.microsoft.com/fwlink/?LinkID=286152)합니다.
2. 다운로드 하 고 hello 설치 [Windows PowerShell 용 Azure Active Directory 모듈을 64 비트](http://go.microsoft.com/fwlink/p/?linkid=236297)합니다.
3. Toohello 이동 `%programfiles%\Microsoft Azure Active Directory Connect` 폴더입니다.
4. 이 명령을 사용 하 여 hello 원활한 SSO PowerShell 모듈 가져오기: `Import-Module .\AzureADSSO.psd1`합니다.
5. 관리자 권한으로 PowerShell을 실행합니다. PowerShell에서 `New-AzureADSSOAuthenticationContext`를 호출합니다. 이 명령은 팝업 tooenter를 제공 해야 테 넌 트의 전역 관리자 자격 증명입니다.
6. `Get-AzureADSSOStatus`를 호출합니다. 이 명령에이 기능이 설정 되는 AD 포리스트 ("hello"도메인 목록 보고) 목록 hello를 제공 합니다.

### <a name="step-2-update-hello-kerberos-decryption-key-on-each-ad-forest-that-it-was-set-it-up-on"></a>2단계. 설정 된 것 각 AD 포리스트에서 hello Kerberos 암호 해독 키를 업데이트 합니다.

1. `$creds = Get-Credential`를 호출합니다. 메시지가 표시 되 면 hello AD 포리스트 의도 대 한 hello 도메인 관리자 자격 증명을 입력 합니다.
2. `Update-AzureADSSOForest -OnPremCredentials $creds`를 호출합니다. 이 명령은 업데이트 hello hello에 대 한 Kerberos 암호 해독 키 `AZUREADSSOACCT` 이 특정 AD 포리스트의 컴퓨터 계정 및 Azure AD에서 업데이트 합니다.
3. 이전 단계에서 hello 기능을 설정 하는 각 AD 포리스트에 대 한 hello를 반복 합니다.

>[!IMPORTANT]
>확인을 _하지_ hello 실행 `Update-AzureADSSOForest` 명령을 한 번 이상. 그렇지 않으면 hello 기능 hello 시간 사용자의 Kerberos 티켓 만료 되 고 온-프레미스 Active Directory에서 발급 될 때까지 작동 하지 않습니다.

## <a name="how-can-i-disable-seamless-sso"></a>Seamless SSO를 사용하지 않으려면 어떻게 해야 하나요?

Seamless SSO는 Azure AD Connect를 통해 사용하지 않도록 설정할 수 있습니다.

Azure AD Connect를 실행하고 “사용자 로그인 페이지 변경”(Change user sign-in page)을 선택하고 “다음”을 클릭합니다. 그런 다음 hello "Enable single sign on" 옵션의 선택을 취소 합니다. Hello 마법사를 계속 합니다. Hello 마법사를 완료 한 후 테 넌 트에 원활한 SSO 비활성화 됩니다.

그러나 화면에 다음과 같은 메시지가 표시됩니다.

"Single sign on 이제 사용 하지 않으면 없지만 추가적인 수동 단계 tooperform에 순서 toocomplete 정리 합니다. 자세한 정보”

toocomplete 프로세스 hello Azure AD Connect를 실행 중인 hello 온-프레미스 서버에 수동 단계를 수행 하십시오.

### <a name="step-1-get-list-of-ad-forests-where-seamless-sso-has-been-enabled"></a>1단계. Seamless SSO가 사용하도록 설정된 AD 포리스트 목록을 가져옵니다.

1. 첫째, 다운로드 및 설치 hello [Microsoft Online Services 로그인 도우미](http://go.microsoft.com/fwlink/?LinkID=286152)합니다.
2. 다운로드 하 고 hello 설치 [Windows PowerShell 용 Azure Active Directory 모듈을 64 비트](http://go.microsoft.com/fwlink/p/?linkid=236297)합니다.
3. Toohello 이동 `%programfiles%\Microsoft Azure Active Directory Connect` 폴더입니다.
4. 이 명령을 사용 하 여 hello 원활한 SSO PowerShell 모듈 가져오기: `Import-Module .\AzureADSSO.psd1`합니다.
5. 관리자 권한으로 PowerShell을 실행합니다. PowerShell에서 `New-AzureADSSOAuthenticationContext`를 호출합니다. 이 명령은 팝업 tooenter를 제공 해야 테 넌 트의 전역 관리자 자격 증명입니다.
6. `Get-AzureADSSOStatus`를 호출합니다. 이 명령에이 기능이 설정 되는 AD 포리스트 ("hello"도메인 목록 보고) 목록 hello를 제공 합니다.

### <a name="step-2-manually-delete-hello-azureadssoacct-computer-account-from-each-ad-forest-that-you-see-listed"></a>2단계. Hello를 수동으로 삭제 `AZUREADSSOACCT` 나열 하는 각 AD 포리스트에서에서 컴퓨터 계정입니다.

## <a name="next-steps"></a>다음 단계

- [**빠른 시작**](active-directory-aadconnect-sso-quick-start.md) - Azure AD Seamless SSO를 준비하고 실행합니다.
- [**기술 심층 분석**](active-directory-aadconnect-sso-how-it-works.md) - 이 기능의 작동 방식을 이해합니다.
- [**문제를 해결** ](active-directory-aadconnect-troubleshoot-sso.md) -tooresolve 공통 hello 기능으로 발급 하는 방법에 대해 알아봅니다.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 새로운 기능 요청을 제출합니다.
