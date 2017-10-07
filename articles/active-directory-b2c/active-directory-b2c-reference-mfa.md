---
title: 'Azure Active Directory B2C: Multi-Factor Authentication | Microsoft Docs'
description: "Tooenable 소비자 용 응용 프로그램에서 다단계 인증 보안을 유지 방법으로 Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 53ef86c4-1586-45dc-9952-dbbd62f68afc
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 29beb1e6ab5d8ab5a65f9c5c068d9e71c60418dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-enable-multi-factor-authentication-in-your-consumer-facing-applications"></a>Azure Active Directory B2C: 소비자 지향 응용 프로그램에서 Multi-Factor Authentication 사용
Azure (Azure AD) Active Directory B2C에 직접 통합 [Azure Multi-factor Authentication](../multi-factor-authentication/multi-factor-authentication.md) 소비자 용 응용 프로그램에서 보안 toosign 접속 및 로그인 경험의 두 번째 계층을 추가할 수 있습니다. 이 작업을 한 줄의 코드도 작성하지 않고 수행할 수 있습니다. 현재 전화 통화 및 문자 메시지를 확인을 지원합니다. 이미 등록 및 로그인 정책을 만든 경우에도 다단계 인증을 사용할 수 있습니다.

> [!NOTE]
> 단지 기존 정책을 편집하지 않고 등록 및 로그인 정책을 만들 때 다단계 인증을 사용할 수도 있습니다.
> 
> 

이 기능을 통해 hello 다음과 같은 시나리오를 처리 하는 응용 프로그램:

* Multi-factor Authentication tooaccess 응용 프로그램을 하나 필요 하지 않지만 tooaccess 필요 않은 다른 합니다. 예를 들면 hello 소비자 소셜 또는 로컬 계정 사용 하 여 자동 보험 응용 프로그램에 로그인 할 수 있지만 hello 홈 보험 응용 프로그램에 액세스 등록 전에 hello에 동일한 hello 전화 번호를 확인 해야 디렉터리입니다.
* Multi-factor Authentication tooaccess 응용 프로그램을 일반적으로 필요 하지 않습니다 하지만 그 안에 tooaccess hello 중요 부분 필요지 않습니다. 예를 들어 hello 소비자 tooa 금융 소셜 또는 로컬 계정 및 계좌 잔액을 확인, 응용 프로그램에에서 서명할 수 있지만 실시간 전송 하기 전에 hello 전화 번호를 확인 해야 합니다.

## <a name="modify-your-sign-up-policy-tooenable-multi-factor-authentication"></a>Multi-factor Authentication에 등록 정책 tooenable 수정
1. [이러한 단계 toonavigate toohello B2C 기능 블레이드 hello Azure 포털에 따라](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)합니다.
2. **등록 정책**을 클릭합니다.
3. 등록 정책 (예: "B2C_1_SiUp") tooopen 클릭 것입니다.
4. 클릭 **multi-factor authentication** hello 설정 **상태** 너무**ON**합니다. **확인**을 클릭합니다.
5. 클릭 **저장** hello hello 블레이드 위쪽에 있습니다.

Hello 정책 tooverify hello 소비자 경험에 hello "지금 실행" 기능을 사용할 수 있습니다. Hello 다음을 확인 합니다.

Hello Multi-factor Authentication 단계 발생 하기 전에 소비자 계정은 디렉터리에 생성 합니다. Hello 단계 중 hello 소비자에 게 tooprovide 자신의 전화 번호 하 고 확인을 묻습니다. Hello 전화 번호 유효성 확인이 성공 하는 경우 연결 toohello 소비자 계정을 나중에 사용할 수 있습니다. Hello 소비자 취소 또는 삭제 하는 경우에 자신이 질문할 수 tooverify 전화 번호를 다시 중 hello 다음 로그인 (Multi-factor Authentication과 함께 사용).

## <a name="modify-your-sign-in-policy-tooenable-multi-factor-authentication"></a>Multi-factor Authentication 사용자 로그인 정책 tooenable 수정
1. [이러한 단계 toonavigate toohello B2C 기능 블레이드 hello Azure 포털에 따라](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)합니다.
2. **로그인 정책**을 클릭합니다.
3. 로그인 정책 (예: "B2C_1_SiIn") tooopen 클릭 것입니다. 클릭 **편집** hello hello 블레이드 위쪽에 있습니다.
4. 클릭 **multi-factor authentication** hello 설정 **상태** 너무**ON**합니다. **확인**을 클릭합니다.
5. 클릭 **저장** hello hello 블레이드 위쪽에 있습니다.

Hello 정책 tooverify hello 소비자 경험에 hello "지금 실행" 기능을 사용할 수 있습니다. Hello 다음을 확인 합니다.

Toohello 소비자 계정, 자신이 tooverify 요청는 hello 소비자가 로그인 할 때 (공유 또는 로컬 계정 사용), 확인 된 전화 번호를 연결 된 경우 것입니다. 전화 번호가 없으면 연결 된 hello 소비자 tooprovide 하나를 요청 하 고 확인 합니다. 성공 확인 hello 전화 번호는 연결 된 toohello 소비자 계정을 나중에 사용할 수 있습니다.

## <a name="multi-factor-authentication-on-other-policies"></a>기타 정책에서 Multi-Factor Authentication
위의 등록 및 로그인 정책에 대 한 설명 된 대로 것도 가능 tooenable multi-factor authentication에 등록 하거나 정책 로그인 및 암호 재설정 정책을 합니다. 정책을 편집하는 프로필에서 곧 지원됩니다.

