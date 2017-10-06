---
title: "Azure AD Connect: 통과 인증 - 작동 방식? | Microsoft Docs"
description: "이 문서에서는 Azure Active Directory 통과 인증 작동 방식을 설명합니다."
services: active-directory
keywords: "Azure AD Connect 통과 인증, Active Directory 설치, Azure AD에 대한 필수 구성 요소, SSO, Single Sign-on"
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
ms.openlocfilehash: ffcebee572a9ba2840e81250651dea45599d65d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-technical-deep-dive"></a>Azure Active Directory 통과 인증: 기술 심층 분석

>[!IMPORTANT]
>Azure AD 통과 인증은 현재 미리 보기로 제공됩니다. 

## <a name="how-does-azure-active-directory-pass-through-authentication-work"></a>Azure Active Directory 통과 인증 작동 방식은?

사용자는 Azure Active Directory (Azure AD)에 의해 보호 되는 응용 프로그램에 toosign를 시도 하 고 hello hello 테 넌 트에서 통과 인증을 사용 하는 경우 다음 단계가 수행 됩니다.

1. hello 사용자가 tooaccess 응용 프로그램 (예를 들어 Outlook Web App-hello https://outlook.office365.com/owa/).
2. Hello 사용자 서명 되지 않은 경우 hello 사용자가 Azure AD 로그인 페이지로 리디렉션된 toohello 합니다.
3. hello 사용자 hello Azure AD 로그인 페이지에 자신의 사용자 이름과 암호를 입력 하 고 hello "로그인" 단추를 클릭 합니다.
4. Hello 로그인 요청을 수신한 경우에 azure AD hello 사용자 이름 및 암호 (공개 키를 사용 하 여 암호화) 큐에 배치 합니다.
5. 온-프레미스 통과 인증 에이전트 아웃 바운드 호출 toohello 큐를 만들고 hello 사용자 이름 및 암호화 된 암호를 검색 합니다.
6. hello 에이전트는 해당 개인 키를 사용 하 여 hello 암호를 해독 합니다.
7. 다음 hello 에이전트 hello 사용자 이름 및 암호 (유사한 메커니즘 toowhat Active Directory Federation Services에서 사용 됨)는 표준 Windows Api를 사용 하 여 Active Directory에 대해 유효성을 검사 합니다. hello username 수 hello 온-프레미스 기본 사용자 이름 중 하나 (일반적으로 `userPrincipalName`) 또는 Azure AD Connect에서 구성 하는 다른 특성 (라고 `Alternate ID`).
8. hello 온-프레미스 Active Directory 도메인 컨트롤러 (DC) 다음 hello 요청을 평가 하 고 반환 hello 적절 한 응답 (성공, 실패, 암호 만료 되었거나 사용자 차단) toohello 에이전트입니다.
9. hello 에이전트 차례로이 응답 백 tooAzure AD를 반환합니다.
10. Azure AD는 hello 응답을 평가 하 고 적절 하 게 toohello 사용자 응답-예를 들어 hello 사용자가 즉시 로그인 하거나 Multi-factor Authentication (MFA)에 대 한 요청.
11. Hello 사용자 로그인에 성공한 경우 hello 사용자는 수 tooaccess hello 응용 프로그램.

hello 다음 다이어그램에서는 모든 hello 구성 요소와 관련 된 hello 단계입니다.

![통과 인증](./media/active-directory-aadconnect-pass-through-authentication/pta2.png)

## <a name="next-steps"></a>다음 단계
- [**현재 제한 사항**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - 이 기능은 현재 미리 보기로 제공됩니다. 지원되는 시나리오와 지원되지 않는 시나리오를 알아봅니다.
- [**빠른 시작**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Azure AD 통과 인증을 작동하고 실행합니다.
- [**질문과 대답** ](active-directory-aadconnect-pass-through-authentication-faq.md) -toofrequently 질문과 대답을 제공 합니다.
- [**문제를 해결** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -tooresolve 공통 hello 기능으로 발급 하는 방법에 대해 알아봅니다.
- [**Azure AD 원활한 SSO**](active-directory-aadconnect-sso.md) - 이 보완 기능에 대해 자세히 알아봅니다.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 새로운 기능 요청을 제출합니다.
