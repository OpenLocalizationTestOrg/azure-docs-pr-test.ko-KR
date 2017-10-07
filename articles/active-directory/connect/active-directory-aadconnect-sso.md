---
title: 'Azure AD Connect: Seamless Single Sign-On | Microsoft Docs'
description: "이 항목에는 Azure Active Directory (Azure AD) 원활한 Single Sign-on 및 있습니다 tooprovide true single sign on 사용자가 회사 네트워크 내부 회사 데스크톱 사용자에 대 한 허용 방법을 설명 합니다."
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
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 11c778c37ee39866dcc3a14ab648cfcd8e322e47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on"></a>Azure Active Directory Seamless Single Sign-On

## <a name="what-is-azure-active-directory-seamless-single-sign-on"></a>Azure Active Directory Seamless Single Sign-On이란?

Azure Active Directory 원활한 Single Sign-on (Azure AD 원활한 SSO) 사용자가 회사 장치 연결 된 tooyour 회사 네트워크에 있는 경우에 자동으로 서명 합니다. 사용 하도록 설정 하면 사용자 tootype tooAzure AD에서에서 자신의 암호 toosign에 필요 하지 않습니다 및 일반적으로 자신의 사용자 이름에도 입력 합니다. 이 기능은 모든 추가 온-프레미스 구성 요소 필요 없이 사용자가 쉽게 액세스할 tooyour 클라우드 기반 응용 프로그램 제공 합니다.

원활한 SSO 어느 hello 함께 사용할 [암호 해시 동기화](active-directory-aadconnectsync-implement-password-synchronization.md) 또는 [통과 인증](active-directory-aadconnect-pass-through-authentication.md) 로그인 방법이 있습니다.

![Seamless Single Sign-On](./media/active-directory-aadconnect-sso/sso1.png)

>[!IMPORTANT]
>Seamless SSO는 현재 미리 보기로 제공됩니다. 이 기능은 _하지_ 적용 가능한 tooActive Directory 페더레이션 서비스 (ADFS).

## <a name="key-benefits"></a>주요 이점

- *멋진 사용자 환경*
  - 사용자는 온-프레미스 및 클라우드 기반 응용 프로그램에 자동으로 로그인됩니다.
  - 사용자가 없는 tooenter 암호 반복 합니다.
- *쉬운 toodeploy & 관리*
  - 추가 구성 요소가 없습니다 온-프레미스 toomake이이 작업을 필요합니다.
  - 모든 클라우드 인증 방법, 즉 [암호 해시 동기화](active-directory-aadconnectsync-implement-password-synchronization.md) 또는 [통과 인증](active-directory-aadconnect-pass-through-authentication.md)과 함께 작동합니다.
  - Toosome 또는 그룹 정책을 사용 하 여 모든 사용자가 롤아웃 될 수 있습니다.
  - 모든 AD FS 인프라에 대 한 hello 필요 없이 Azure AD에 비-Windows 10 장치를 등록 합니다. 이 기능 요구에 따라 toouse 버전 2.1 이상 hello [작업 공간 연결 클라이언트](https://www.microsoft.com/download/details.aspx?id=53554)합니다.

## <a name="feature-highlights"></a>주요 기능

- 사용자 로그인 이름 hello 온-프레미스 기본 사용자 이름 중 하나가 될 수 있습니다 (`userPrincipalName`) 또는 Azure AD Connect에서 구성 하는 다른 특성 (`Alternate ID`). 원활한 SSO hello를 사용 하기 때문에 경우 작업을 사용 하 여 둘 다 `securityIdentifier` Azure AD에서 사용자 개체를 해당 하는 hello hello Kerberos 티켓 toolook 클레임입니다.
- Seamless SSO는 편의적인 기능입니다. 어떤 이유로 든 실패 한 경우 사용자 로그인 환경을 hello tooits 일반 동작-즉, hello 돌아갑니다 사용자 tooenter hello 로그인 페이지에서 암호를 요구 합니다.
- 응용 프로그램에 전달 하는 경우는 `domain_hint` (OpenID Connect 사용) 또는 `whr` (SAML) 매개 변수-테 넌 트를 식별 합니다. 또는 `login_hint` hello 사용자 식별 매개 변수-Azure AD 로그인 요청을에서 사용자가 자동으로 로그인 없이도 사용자 이름 또는 암호를 입력 합니다.
- Azure AD Connect를 통해 사용하도록 설정할 수 있습니다.
- 사용 가능한 기능 및 모든 유료 버전의 Azure AD toouse 필요 하지 않습니다 것입니다.
- Kerberos 인증이 가능한 플랫폼 및 브라우저에서 [최신 인증](https://aka.ms/modernauthga)을 지원하는 웹 브라우저 기반 클라이언트 및 Office 클라이언트에서 지원됩니다.

| OS\Browser |Internet Explorer|Edge|Google Chrome|Mozilla Firefox|Safari|
| --- | --- |--- | --- | --- | -- 
|Windows 10|예|아니요|예|예\*|해당 없음
|Windows 8.1|예|해당 없음|예|예\*|해당 없음
|Windows 8|예|해당 없음|예|예\*|해당 없음
|Windows 7|예|해당 없음|예|예\*|해당 없음
|Mac OS X|해당 없음|해당 없음|예\*|예\*|예\*

\*[추가 구성](active-directory-aadconnect-sso-quick-start.md#browser-considerations)이 필요합니다.

>[!IMPORTANT]
>에서는 최근에 롤백 가장자리 tooinvestigate에 대 한 지원 고객이 신고한 문제.

>[!NOTE]
>Windows 10 용 hello 좋습니다 toouse [Azure AD Join](../active-directory-azureadjoin-overview.md) hello 최적의 single sign on 환경을 Azure ad에 대 한 합니다.

## <a name="next-steps"></a>다음 단계

- [**빠른 시작**](active-directory-aadconnect-sso-quick-start.md) - Azure AD Seamless SSO를 준비하고 실행합니다.
- [**기술 심층 분석**](active-directory-aadconnect-sso-how-it-works.md) - 이 기능의 작동 방식을 이해합니다.
- [**질문과 대답** ](active-directory-aadconnect-sso-faq.md) -toofrequently 질문과 대답을 제공 합니다.
- [**문제를 해결** ](active-directory-aadconnect-troubleshoot-sso.md) -tooresolve 공통 hello 기능으로 발급 하는 방법에 대해 알아봅니다.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 새로운 기능 요청을 제출합니다.
