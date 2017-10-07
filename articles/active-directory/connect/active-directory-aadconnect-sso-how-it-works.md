---
title: "Azure AD Connect: Seamless Single Sign-On - 작동 방식 | Microsoft Docs"
description: "이 문서에서는 hello Azure Active Directory 원활한 Single Sign-on 기능이 어떻게 작동 하는지 설명 합니다."
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
ms.openlocfilehash: 17ce35b32832d241068ab878cf7aac42deab74ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-technical-deep-dive"></a>Azure Active Directory Seamless Single Sign-On: 기술 심층 분석

이 문서에 hello Azure Active Directory 원활한 Single Sign-on (SSO 원활한) 기능이 어떻게 작동 하는지 기술 세부 정보를 제공 합니다.

>[!IMPORTANT]
>hello 원활한 SSO 기능은 현재 미리 보기 중입니다.

## <a name="how-does-seamless-sso-work"></a>Seamless SSO 작동 방식

이 섹션에는 두 개의 부분 tooit에 있습니다.
1. hello 설치할 hello 원활한 SSO 기능 수 있습니다.
2. 단일 사용자 로그인 트랜잭션이 Seamless SSO와 작동하는 방식

### <a name="how-does-set-up-work"></a>기능을 설정하는 방식

Seamless SSO는 [여기](active-directory-aadconnect-sso-quick-start.md)서 보여 주듯이 Azure AD Connect를 통해 사용하도록 설정할 수 있습니다. Hello 기능을 사용 하는 동안 다음 단계는 hello 발생 합니다.
- 온-프레미스 AD(Active Directory)에 Azure AD를 나타내는`AZUREADSSOACCT`라는 컴퓨터 계정이 만들어집니다.
- hello 컴퓨터 계정의 Kerberos 암호 해독 키를 Azure AD와 안전 하 게 공유 됩니다.
- 또한 두 개의 Kerberos 서비스 사용자 이름 (Spn) toorepresent Azure AD에는 로그인 시 사용 되는 두 개의 Url은 생성 됩니다.

>[!NOTE]
> 각 AD 포리스트에 만들어집니다 hello 컴퓨터 계정과 Kerberos Spn hello tooAzure AD 동기화 (Azure AD Connect를 사용 하 여) 중이 고 해당 사용자에 대 한 원활한 SSO 합니다. Hello 이동 `AZUREADSSOACCT` 컴퓨터 계정 tooan OU (조직 단위) 다른 컴퓨터 계정에 관리 되는 저장된 tooensure 있는 hello 동일한 방식으로 삭제 되지 않습니다.

>[!IMPORTANT]
>항상 좋습니다 있습니다 [hello Kerberos 암호 해독 키를 롤오버할](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) 의 hello `AZUREADSSOACCT` 컴퓨터 계정이 적어도 30 일 마다입니다.

### <a name="how-does-sign-in-with-seamless-sso-work"></a>Seamless SSO로 로그인하는 방식

Hello 설정 완료 되 면 원활한 SSO 통합 IWA (Windows 인증)를 사용 하는 hello 동일한 방식으로 다른 로그인을 사용할 수 있습니다. hello 흐름은 다음과 같습니다.

1. hello 사용자가 tooaccess 응용 프로그램 (예를 들어 Outlook Web App-hello https://outlook.office365.com/owa/) 회사 네트워크 내부 도메인에 가입 된 회사 장치에서 합니다.
2. Hello 사용자 서명 되지 않은 경우 hello 사용자가 Azure AD 로그인 페이지로 리디렉션된 toohello 합니다.

  >[!NOTE]
  >Hello Azure AD 로그인 요청에 포함 된 경우는 `domain_hint` (테 넌 트-예를 들어, 식별 contoso.onmicrosoft.com) 또는 `login_hint` (hello 사용자-예를 들어 식별 user@contoso.onmicrosoft.com 또는 user@contoso.com) 매개 변수를 다음 2 단계를 건너뜁니다.

3. hello hello Azure AD 로그인 페이지에 사용자 이름에 사용자 형식입니다.
4. JavaScript를 사용 하 여 hello 백그라운드에서 Azure AD 문제를 제기 hello 브라우저 tooprovide 401 권한 없는 응답을 통해 Kerberos 티켓입니다.
5. hello 브라우저 요청 차례로 hello에 대 한 티켓을 Active Directory에서 `AZUREADSSOACCT` 컴퓨터 계정 (Azure AD를 나타냄).
6. Active Directory hello 컴퓨터 계정을 찾아 hello 컴퓨터 계정 암호를 사용 하 여 암호화 하는 Kerberos 티켓 toohello 브라우저를 반환 합니다.
7. Active Directory tooAzure AD에서에서 가져온 hello Kerberos 티켓을 전달 하는 hello 브라우저 (hello 중 하나에서 [Azure AD Url에는 이전에 toohello 브라우저의 인트라넷 영역 설정 추가](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature)).
8. Azure AD 해독 hello Kerberos 티켓을 hello hello 회사 장치에 로그인 하는 hello 사용자 id를 포함 하는 hello를 사용 하 여 이전에 공유 키.
9. 을 평가한 후 Azure AD 토큰 백 toohello 응용 프로그램을 반환 하거나 hello 사용자 tooperform 다단계 인증과 같은 추가 증명을 요청 하십시오.
10. Hello 사용자 로그인에 성공한 경우 hello 사용자는 수 tooaccess hello 응용 프로그램.

hello 다음 다이어그램에서는 모든 hello 구성 요소와 관련 된 hello 단계입니다.

![Seamless Single Sign-On](./media/active-directory-aadconnect-sso/sso2.png)

원활한 SSO는 실패 한 경우 로그인 환경 hello tooits 일반 동작-즉, hello 대체 되므로 편의적, 사용자가 자신의 암호 toosign에 tooenter 해야 합니다.

## <a name="next-steps"></a>다음 단계

- [**빠른 시작**](active-directory-aadconnect-sso-quick-start.md) - Azure AD Seamless SSO를 준비하고 실행합니다.
- [**질문과 대답** ](active-directory-aadconnect-sso-faq.md) -toofrequently 질문과 대답을 제공 합니다.
- [**문제를 해결** ](active-directory-aadconnect-troubleshoot-sso.md) -tooresolve 공통 hello 기능으로 발급 하는 방법에 대해 알아봅니다.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 새로운 기능 요청을 제출합니다.
