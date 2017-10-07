---
title: "Azure AD Connect: 통과 인증 | Microsoft 문서"
description: "이 문서에서는 Azure AD(Azure Active Directory) 통과 인증 및 이 통과 인증을 통해 사용자의 암호를 온-프레미스 Active Directory에 대해 유효성 검사하여 Azure AD 로그인을 허용하는 방법을 설명합니다."
services: active-directory
keywords: "Azure AD Connect 통과 인증의 정의, Active Directory 설치, Azure AD에 대한 필수 구성 요소, SSO, Single Sign-on"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: billmath
ms.openlocfilehash: 56cfb2c4f4afc7d46c926a392ae6ec01e96224d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="user-sign-in-with-azure-active-directory-pass-through-authentication"></a>Azure Active Directory 통과 인증으로 사용자 로그인

## <a name="what-is-azure-active-directory-pass-through-authentication"></a>Azure Active Directory 통과 인증이란?

Azure Active Directory (Azure AD) 통과 인증 사용자 toosign tooboth 온-프레미스에 있으며이 사용 하 여 클라우드 기반 응용 프로그램에 동일한 암호 hello 합니다. 이 기능은 사용자가 더 나은 환경을-적은 암호 tooremember 하나를 제공 하 고 사용자가 거의 tooforget 어떻게 하기 때문에 IT 기술 지원팀 비용 감소에 toosign 합니다. 사용자가 Azure AD를 사용하여 로그인할 때 이 기능은 온-프레미스 Active Directory에 대해 직접 사용자 암호의 유효성을 검사합니다.

이 기능은 대신 너무[Azure AD 암호 해시 동기화](active-directory-aadconnectsync-implement-password-synchronization.md)를 제공 하는 클라우드 인증 tooorganizations의 동일한 이점은 hello 합니다. 하지만, 특정 조직에서 보안 및 규정 준수 정책을 하지 허용 이러한 조직 toosend 사용자의 암호는 해시 된 폼 내부 경계가 외부에 합니다. 통과 인증은 그러한 조직의 hello 적합 한 솔루션입니다.

![Azure AD 통과 인증](./media/active-directory-aadconnect-pass-through-authentication/pta1.png)

통과 인증 hello로 결합할 수 있습니다 [원활한 Single Sign-on](active-directory-aadconnect-sso.md) 기능입니다. 이러한 방식으로 사용자가 회사 컴퓨터 사용자가 회사 네트워크 내부에서 응용 프로그램에 액세스 하는 경우, 이러한 tootype에 자신의 암호 toosign에 필요 하지 않습니다.

>[!IMPORTANT]
>Azure AD 통과 인증은 현재 미리 보기로 제공됩니다.

## <a name="key-benefits-of-using-azure-ad-pass-through-authentication"></a>Azure AD 통과 인증 사용의 주요 혜택

- *멋진 사용자 환경*
  - Hello를 사용 하는 사용자가 온-프레미스 및 클라우드 기반 응용 프로그램 모두에 동일한 암호 toosign 합니다.
  - 사용자가 시간이 절약 toohello 통하게 IT 기술 지원팀 암호 관련 문제를 해결 합니다.
  - 사용자가 צ ְ ײ [셀프 서비스 암호 관리](../active-directory-passwords-overview.md) hello 클라우드에서 작업 합니다.
- *쉬운 toodeploy & 관리*
  - 복잡한 온-프레미스 배포 또는 네트워크 구성에 대한 필요가 없습니다.
  - 필요한 경량 에이전트 toobe 방금 온-프레미스를 설치합니다.
  - 관리 오버헤드 없음 hello 에이전트 향상 및 버그 수정에 자동으로 받습니다.
- *보안*
  - 모든 형태의 hello 클라우드에서 온-프레미스 암호 저장 되지 않습니다.
  - hello 에이전트만 네트워크 내에서 아웃 바운드 연결을 만듭니다. 따라서 DMZ 라고도 하는 경계 네트워크에서는 요구 사항 tooinstall hello 에이전트가 없습니다.이 있습니다.
  - MFA(Multi-Factor Authentication)를 포함하여 [Azure AD 조건부 액세스 정책](../active-directory-conditional-access-azure-portal.md)을 사용하여 원활하게 작동하고, [무차별 암호 대입 공격을 필터링](active-directory-aadconnect-pass-through-authentication-smart-lockout.md)하여 사용자 계정을 보호합니다.
- *고가용성*
  - 여러 온-프레미스 서버 tooprovide 고가용성 로그인 요청에 추가 에이전트를 설치할 수 있습니다.

## <a name="feature-highlights"></a>주요 기능

- 모든 웹 브라우저 기반 응용 프로그램 및 [최신 인증](https://aka.ms/modernauthga)을 사용하는 Microsoft Office 클라이언트 응용 프로그램에 사용자 로그인을 지원합니다.
- 사용자 로그인 이름 hello 온-프레미스 기본 사용자 이름 중 하나가 될 수 있습니다 (`userPrincipalName`) 또는 Azure AD Connect에서 구성 하는 다른 특성 (라고 `Alternate ID`).
- hello 기능으로 원활 하 게 작동 [조건부 액세스](../active-directory-conditional-access.md) Multi-factor Authentication (MFA) toohelp 등의 기능 사용자가 보호 합니다.
- AD 포리스트 간에 포리스트 트러스트가 있고 이름 접미사 라우팅이 제대로 구성된 경우 다중 포리스트 환경이 지원됩니다.
- 사용 가능한 기능 및 모든 유료 버전의 Azure AD toouse 필요 하지 않습니다 것입니다.
- [Azure AD Connect](active-directory-aadconnect.md)를 통해 사용하도록 설정할 수 있습니다.
- 수신 대기 하 고 toopassword 유효성 검사 요청에 응답 하는 간단한 온-프레미스 에이전트를 사용 합니다.
- 여러 에이전트를 설치하면 로그인 요청의 고가용성을 제공합니다.
- 그 [보호](active-directory-aadconnect-pass-through-authentication-smart-lockout.md) 무차별 암호에 대 한 온-프레미스 계정 hello 클라우드에서 무차별 암호 대입 공격을 강제 합니다.

## <a name="next-steps"></a>다음 단계

- [**빠른 시작**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Azure AD 통과 인증을 작동하고 실행합니다.
- [**현재 제한 사항**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - 이 기능은 현재 미리 보기로 제공됩니다. 지원되는 시나리오와 지원되지 않는 시나리오를 알아봅니다.
- [**기술 심층 분석**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - 이 기능의 작동 방식을 이해합니다.
- [**질문과 대답** ](active-directory-aadconnect-pass-through-authentication-faq.md) -toofrequently 질문과 대답을 제공 합니다.
- [**문제를 해결** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -tooresolve 공통 hello 기능으로 발급 하는 방법에 대해 알아봅니다.
- [**Azure AD 원활한 SSO**](active-directory-aadconnect-sso.md) - 이 보완 기능에 대해 자세히 알아봅니다.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 새로운 기능 요청을 제출합니다.
