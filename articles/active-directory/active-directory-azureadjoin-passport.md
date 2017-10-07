---
title: "Windows Hello 비즈니스 사용자와 Azure AD를 통해 암호 없이 aaaAuthenticating id | Microsoft Docs"
description: "비즈니스용 Windows Hello의 개요와 비즈니스용 Windows Hello를 배포하는 방법에 대한 추가 정보를 제공합니다."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: f907bb90-8776-46ca-9e12-279949af66ff
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 7c1c52e10b7ab7a89ec3226ffa7cf01896267871
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticating-identities-without-passwords-through-windows-hello-for-business"></a>비즈니스용 Windows Hello를 통해 암호 없이 ID 인증
hello 현재 암호로 인증 방법을 안전 충분 한 tookeep 사용자 않습니다. 사용자는 암호를 다시 사용하고 잊기도 합니다. 암호도 breachable, phishable, 발생 하기 쉬운 toocracks 및 추측할 수 있는 합니다. 어려운 tooremember 가져올 및 발생 하기 쉬운 tooattacks 좋아요 "[hello 해시 전달](https://technet.microsoft.com/dn785092.aspx)"입니다.

## <a name="about-windows-hello-for-business"></a>비즈니스용 Windows Hello 정보
비즈니스용 Windows Hello는 조직과 소비자를 위한 보안 방법으로, 암호 수준을 넘어서는 개인/공개 키 또는 인증서 기반 인증 방법입니다. 이러한 형식의 인증 암호 및 처리할 toobreaches, 도난을, 및 피싱을 대체할 수 있는 키 쌍 자격 증명에 의존 합니다.

 비즈니스용 Windows Hello 사용 하면 사용자 tooa Microsoft 계정, Windows Server Active Directory 계정, Microsoft Azure Active Directory (Azure AD) 계정 또는 빠른 IDentity 온라인 (FIDO) 인증을 지 원하는 타사 서비스를 인증 합니다. 초기 2 단계 확인 작업 후 Windows Hello 하는 동안 비즈니스 등록을 위한, 비즈니스용 Windows Hello hello 사용자의 장치에 설치 되어 및 hello 사용자 제스처 Windows Hello 또는 PIN을 설정 합니다. hello 사용자 hello 제스처 tooverify 자신의 id를 제공합니다. 다음 Windows Hello를 사용 하 여 비즈니스 tooauthenticate hello 사용자에 대 한 창과 tooaccess 보호 된 리소스 및 서비스 하는 데 도움이 됩니다.

스마트 카드 사용자 hello는 toosign toohello 장치에서 사용 하 여 같은 hello 개인 키 PIN, 생체 인식, 또는 원격 장치와 같은 "사용자 제스처"을 통해서만 사용할 활성화 됩니다. 이 정보는 연결 된 tooa 인증서 또는 비대칭 키 쌍으로 된. hello 개인 키가 하드웨어 attested hello 장치에 신뢰할 수 있는 TPM (플랫폼 모듈) 칩 경우. hello 개인 키를 벗어나지 hello 장치입니다.

hello 공개 키 (온-프레미스)에 대 한 Azure Active Directory 및 Windows Server Active Directory에 등록 됩니다. Id 공급자 (IDPs) hello 사용자 매핑 hello 공개 키로 hello 사용자 toohello 개인 키의 유효성을 검사 하 고 한 번 암호 otp (1), PhoneFactor, 또는 다른 알림 메커니즘을 통해 로그인 정보를 제공 합니다.

## <a name="why-enterprises-should-adopt-windows-hello-for-business"></a>기업에서 비즈니스용 Windows Hello를 도입해야 하는 이유
기업에서는 비즈니스용 Windows Hello를 사용하여 다음과 같은 방법으로 리소스를 좀 더 안전하게 관리할 수 있습니다.

* 하드웨어 기본 설정 옵션을 통해 Windows Hello 비즈니스를 설정합니다. 즉, TPM이 사용 가능한 경우 키가 TPM 1.2 또는 TPM 2.0에서 생성됩니다. TPM을 사용할 수 없는 소프트웨어 hello 키를 생성 합니다.
* Hello의 정의 hello 복잡성과 길이는 고정, 한 Hello 사용 조직에서 사용 되는지 여부.
* Windows Hello 비즈니스 toosupport 스마트 카드와 같은 시나리오에 대 한 사용 하 여 구성 신뢰 인증서 기반 합니다.

## <a name="how-windows-hello-for-business-works"></a>비즈니스용 Windows Hello의 작동 방식
1. 키는은 TPM 또는 소프트웨어 hello 하드웨어에서 생성 됩니다. 많은 장치는 장치에 암호화 키를 통합 하 여 hello 하드웨어를 보호 하는 기본 제공 TPM 칩 있습니다. TPM 1.2 또는 TPM 2.0 키나 hello 생성 된 키에서 생성 된 인증서를 생성 합니다.
2. hello TPM에는 이러한 하드웨어 바인딩된 키 증명합니다.
3. 단일 잠금 해제 제스처 hello 장치 잠금을 해제합니다. 이 제스처 toomultiple 리소스에 액세스할 경우 허용 hello 장치는 도메인에 가입 된 또는 Azure AD에 가입 합니다.

## <a name="how-hello-windows-hello-for-business-lifecycle-works"></a>비즈니스 주기 Windows Hello hello 작동 방식
![비즈니스용 Windows Hello 수명 주기](./media/active-directory-azureadjoin/active-directory-azureadjoin-microsoft-passport.png)

hello 이전 다이어그램에서는 hello 개인/공개 키 쌍 및 hello id 공급자가 hello 유효성 검사 각 단계는 여기 자세히 설명되어 있습니다.

1. hello 사용자 여러 기본 제공 교정 메서드 (제스처, 실제 스마트 카드, 다단계 인증)를 통해 해당 id를 증명 하 고이 정보 tooan Identity 공급자 (IDP) Azure Active Directory와 같은 전송 또는 온-프레미스 Active Directory 합니다.
2. hello 장치 다음 hello 키를 만듭니다, 그리고 hello 키 증명,이 키의 공개 부분 hello를 사용, 스테이션 문과 함께 연결, 로그인 하면 및 toohello IDP tooregister hello 키를 보냅니다.
3. Hello IDP hello hello 키의 공개 부분을 등록 하는 즉시 hello IDP 과제 hello 키의 비공개 부분 hello와 장치 toosign을 hello 합니다.
4. IDP hello 다음 유효성을 검사 하 고 문제 hello hello 사용자와 hello 장치 액세스 hello 보호 된 리소스 수 있는 인증 토큰입니다. IDPs는 플랫폼 간 앱 작성 또는 사용 (JavaScript/Webcrypto Api)를 통해 지원 toocreate 브라우저를 Windows Hello가 사용자에 게 비즈니스 자격 증명에 대 한 합니다.

## <a name="hello-deployment-requirements-for-windows-hello-for-business"></a>비즈니스용 Windows Hello에 대 한 hello 배포 요구 사항
### <a name="at-hello-enterprise-level"></a>Hello 엔터프라이즈 수준
* hello 엔터프라이즈에 Azure 구독.

### <a name="at-hello-user-level"></a>Hello 사용자 수준
* hello 사용자의 컴퓨터는 Windows 10 Professional 또는 Enterprise를 실행 합니다.

자세한 배포 지침을 참조 하십시오. [hello 조직에서 비즈니스용 Windows Hello 사용](active-directory-azureadjoin-passport-deployment.md)합니다.

## <a name="additional-information"></a>추가 정보
* [Hello 엔터프라이즈용 Windows 10: 작업에 대 한 방법으로 toouse 장치](active-directory-azureadjoin-windows10-devices-overview.md)
* [Azure Active Directory Join을 통해 기능 10 tooWindows 장치 클라우드를 확장합니다.](active-directory-azureadjoin-user-upgrade.md)
* [Azure AD 조인에 대한 사용 시나리오에 대해 알아보기](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Windows 10 환경용에 대 한 AD 도메인에 가입 된 장치 tooAzure 연결](active-directory-azureadjoin-devices-group-policy.md)
* [Azure AD 조인 설정](active-directory-azureadjoin-setup.md)

