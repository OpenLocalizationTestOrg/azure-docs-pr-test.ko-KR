---
title: "Azure AD Connect: 통과 인증 - 미리 보기 인증 에이전트 업그레이드 | Microsoft Docs"
description: "이 문서에서는 설명 방법을 tooupgrade Azure Active Directory (Azure AD) 통과 인증 구성 합니다."
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
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 1695326b182278944e9f1584da72b18862b6ef27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-upgrade-preview-authentication-agents"></a>Azure Active Directory 통과 인증: 미리 보기 인증 에이전트 업그레이드

## <a name="overview"></a>개요

이 문서는 미리 보기를 통해 Azure AD 통과 인증을 사용하는 고객을 위한 것입니다. 에서는 최근에 업그레이드 된 (및 브랜딩) hello 인증 에이전트 소프트웨어입니다. Too_manually_ 업그레이드 미리 보기 인증 에이전트 온-프레미스 서버에 설치 해야 합니다. 이 수동 업그레이드는 일회성 작업입니다. 이후의 모든 업데이트 tooAuthentication 에이전트는 자동입니다. hello 이유 tooupgrade는 다음과 같습니다.

- 모든 추가 보안 또는 버그 수정 인증 에이전트의 미리 보기 버전 hello 수신 되지 않습니다.
-   고가용성을 위해 다른 서버에 인증 에이전트의 hello 미리 보기 버전을 설치할 수 없습니다.

## <a name="check-versions-of-your-authentication-agents"></a>인증 에이전트의 버전 확인

### <a name="step-1-check-where-your-authentication-agents-are-installed"></a>1단계: 인증 에이전트가 설치된 위치 확인

이러한 단계 toocheck를 수행 하 고 인증 에이전트가 설치 되어 있는 키를 누릅니다.

1. Toohello 로그인 [Azure Active Directory 관리 센터](https://aad.portal.azure.com) 테 넌 트에 대 한 hello 전역 관리자 자격 증명을 사용 합니다.
2. 선택 **Azure Active Directory** hello 왼쪽 탐색 모음에 있습니다.
3. **Azure AD Connect**를 선택합니다. 
4. **통과 인증**을 선택합니다. 이 블레이드는 hello 서버 인증 에이전트 설치 되는 위치를 나열 합니다.

![Azure Active Directory 관리 센터 - 통과 인증 블레이드](./media/active-directory-aadconnect-pass-through-authentication/pta8.png)

### <a name="step-2-check-hello-versions-of-your-authentication-agents"></a>2 단계: 인증 에이전트의 hello 버전 확인

toocheck hello 버전 hello 앞 단계에서에서 식별 된 각 서버에서 사용자 인증 에이전트의 다음이 지침을 따르십시오.

1. 너무 이동**제어판-> 프로그램-> 프로그램 및 기능** hello 온-프레미스 서버에 있습니다.
2. 에 대 한 항목이 없는 경우 "**Microsoft Azure AD Connect 인증 Agent**", tootake이이 서버에 대 한 어떤 작업도 필요 하지 않습니다.
3. 에 대 한 항목이 없는 경우 "**Microsoft Azure AD 응용 프로그램 프록시 커넥터**", 버전 1.5.132.0 toomanually 필요한 이전에이 서버에서 업그레이드 합니다.

![인증 에이전트의 미리 보기 버전](./media/active-directory-aadconnect-pass-through-authentication/pta6.png)

## <a name="best-practices-toofollow-before-starting-hello-upgrade"></a>유용한 정보 hello 업그레이드를 시작 하기 전에 toofollow

업그레이드 하기 전에 갖추어야 할 hello 다음 위치에 항목:

1. **클라우드 전용 전역 관리자 계정 만들기**: 클라우드 전용 전역 관리자 계정 toouse 통과 인증 에이전트 제대로 작동 하지 않는 긴급 상황에서 필요 없이 업그레이드 하지 마십시오. [클라우드 전용 전역 관리자 계정 추가](../active-directory-users-create-azure-portal.md)에 대해 자세히 알아봅니다. 이 단계를 수행하는 것이 중요하며 테넌트가 잠기지 않도록 합니다.
2.  **고가용성을 보장**: 완료 하지 않으면 이전에 두 번째 독립 실행형 인증 에이전트 tooprovide 고가용성 로그인 요청에 대 한 이러한를 사용 하 여 설치 [지침](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability)합니다.

## <a name="upgrading-hello-authentication-agent-on-your-azure-ad-connect-server"></a>Azure AD Connect 서버 hello 인증 에이전트를 업그레이드합니다.

Hello에 hello 인증 에이전트를 업그레이드 하기 전에 Azure AD Connect를 업그레이드 해야 동일한 서버입니다. 주 및 스테이징 Azure AD Connect 서버 모두에서 다음 단계를 따릅니다.

1. **Azure AD Connect를 업그레이드**: 여기 [문서](./active-directory-aadconnect-upgrade-previous-version.md) toohello 최신 Azure AD Connect 버전을 업그레이드 하 고 있습니다.
2. **Hello 미리 보기 버전의 hello 인증 에이전트 제거**: 다운로드 [이 PowerShell 스크립트](https://aka.ms/rmpreviewagent) hello 서버에서 관리자 권한으로 실행 합니다.
3. **Hello hello 인증 에이전트의 최신 버전을 다운로드 (1.5.193.0 버전 이상)**: toohello 로그인 [Azure Active Directory 관리 센터](https://aad.portal.azure.com) 테 넌 트의 전역 관리자 자격 증명을 사용 합니다. **Azure Active Directory -> Azure AD Connect -> 통과 인증 -> 에이전트 다운로드**를 선택합니다. 서비스의 hello 조건에 동의 하 고 hello hello 인증 에이전트의 최신 버전을 다운로드 합니다.
4. **Hello hello 인증 에이전트의 최신 버전을 설치**: 실행 가능한 실행 hello 3 단계에서에서 다운로드 합니다. 메시지가 표시되면 테넌트의 전역 관리자 자격 증명을 입력합니다.
5. **Hello 최신 버전 설치 되었는지 확인**: 위에 나와 있는 것 처럼 너무 이동**제어판-> 프로그램-> 프로그램 및 기능** 에 대 한 항목이 있는지 확인 하 고 "**Microsoft Azure AD Connect 인증 에이전트**"입니다.

>[!NOTE]
>Hello에 hello 통과 인증 블레이드를 확인 하는 경우 [Azure Active Directory 관리 센터](https://aad.portal.azure.com) hello 이전 단계를 완료 한 후 서버-hello를 표시 하는 하나의 항목만 당 두 개의 인증 에이전트 항목이 표시 됩니다 로 인증 에이전트 **활성** hello 다른으로 고 **비활성**합니다. _예상된_ 동작입니다. hello **비활성** 항목 몇 일 후 자동으로 삭제 됩니다.

## <a name="upgrading-hello-authentication-agent-on-other-servers"></a>다른 서버에 hello 인증 에이전트를 업그레이드합니다.

(여기서 Azure AD Connect 설치 되지 않음) 다른 서버에서 이러한 단계 tooupgrade 인증 에이전트를 따릅니다.

1. **Hello 미리 보기 버전의 hello 인증 에이전트 제거**: 다운로드 [이 PowerShell 스크립트](https://aka.ms/rmpreviewagent) hello 서버에서 관리자 권한으로 실행 합니다.
2. **Hello hello 인증 에이전트의 최신 버전을 다운로드 (1.5.193.0 버전 이상)**: toohello 로그인 [Azure Active Directory 관리 센터](https://aad.portal.azure.com) 테 넌 트의 전역 관리자 자격 증명을 사용 합니다. **Azure Active Directory -> Azure AD Connect -> 통과 인증 -> 에이전트 다운로드**를 선택합니다. 서비스의 hello 조건에 동의 하 고 hello 최신 버전을 다운로드 합니다.
3. **Hello hello 인증 에이전트의 최신 버전을 설치**: 2 단계에서에서 다운로드 한 실행 hello를 실행 합니다. 메시지가 표시되면 테넌트의 전역 관리자 자격 증명을 입력합니다.
4. **Hello 최신 버전 설치 되었는지 확인**: 위에 나와 있는 것 처럼 너무 이동**제어판-> 프로그램-> 프로그램 및 기능** 이라고 하는 항목 인지 확인 하 고 **Microsoft Azure AD Connect 인증 에이전트**합니다.

>[!NOTE]
>Hello에 hello 통과 인증 블레이드를 확인 하는 경우 [Azure Active Directory 관리 센터](https://aad.portal.azure.com) hello 이전 단계를 완료 한 후 서버-hello를 표시 하는 하나의 항목만 당 두 개의 인증 에이전트 항목이 표시 됩니다 로 인증 에이전트 **활성** hello 다른으로 고 **비활성**합니다. _예상된_ 동작입니다. hello **비활성** 항목 몇 일 후 자동으로 삭제 됩니다.

## <a name="next-steps"></a>다음 단계
- [**문제를 해결** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -tooresolve 공통 hello 기능으로 발급 하는 방법에 대해 알아봅니다.
