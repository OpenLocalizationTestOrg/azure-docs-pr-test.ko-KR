---
title: "인증 및 Azure MFA 서버 aaaRADIUS | Microsoft Docs"
description: "RADIUS 인증 및 Azure Multi-factor Authentication 서버를 배포 하는 데 도움이 되는 hello Azure multi-factor authentication 페이지입니다."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f4ba0fb2-2be9-477e-9bea-04c7340c8bce
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/26/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017, it-pro
ms.openlocfilehash: dac061b83f2657c67192a7aa9c5de63ffeffaaa8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-radius-authentication-with-azure-multi-factor-authentication-server"></a>Azure Multi-Factor Authentication 서버와 RADIUS 인증 통합
Azure MFA 서버 tooenable의 hello RADIUS 인증 섹션을 사용 하 고 RADIUS 인증을 구성 합니다. RADIUS는 표준 프로토콜 tooaccept 인증 요청 및 tooprocess 이러한 요청입니다. hello Azure Multi-factor Authentication 서버는 RADIUS 서버로 작동합니다. RADIUS 클라이언트 (VPN 어플라이언스)와 Active Directory (AD), LDAP 디렉터리, 또는 다른 RADIUS 서버 tooadd Azure Multi-factor Authentication 될 수 있는 인증 대상 사이 삽입 합니다. Azure Multi-factor Authentication (MFA) toofunction hello 클라이언트 서버 및 hello 인증 대상 모두와 통신할 수 있도록 hello Azure MFA 서버를 구성 해야 합니다. Azure MFA 서버 hello RADIUS 클라이언트의 요청을 수락 하며 hello 인증 대상에 대해 자격 증명의 유효성을 검사 하 Azure Multi-factor Authentication을 추가 및 응답 백 toohello RADIUS 클라이언트에 보냅니다. hello 인증 요청이 hello 기본 인증 및 hello Azure Multi-factor Authentication이 성공 하는 경우에 성공 합니다.

> [!NOTE]
> MFA 서버 hello PAP (암호 인증 프로토콜) 및 MSCHAPv2 지원 (Microsoft Challenge Handshake 인증 프로토콜)를 RADIUS 서버로 작동할 때 RADIUS 프로토콜을 통해.  Hello MFA 서버가 해당 프로토콜을 지 원하는 RADIUS 프록시 tooanother RADIUS 서버 역할을 하는 경우에 EAP (확장할 수 있는 인증 프로토콜)와 같은 다른 프로토콜을 사용할 수 있습니다.
>
> 이 구성에서는 단방향 SMS 및 OATH 토큰 hello와 MFA 서버를 시작할 수 없습니다. 대체 프로토콜을 사용 하 여 성공적인 RADIUS 챌린지 응답 하므로 작동 하지 않습니다.

![RADIUS 인증](./media/multi-factor-authentication-get-started-server-rdg/radius.png)

## <a name="add-a-radius-client"></a>RADIUS 클라이언트 추가
Windows 서버에 Azure Multi-factor Authentication 서버 설치 hello tooconfigure RADIUS 인증 합니다. Active Directory 환경에 있으면 hello 서버 hello 네트워크 내부 조인된 toohello 도메인 이어야 합니다. 다음 프로시저 tooconfigure hello Azure Multi-factor Authentication 서버 hello를 사용 합니다.

1. Azure Multi-factor Authentication 서버 hello hello 왼쪽된 메뉴에 hello RADIUS 인증 아이콘을 클릭 합니다.
2. Hello 확인 **RADIUS 인증 사용** 확인란을 선택 합니다.
3. Hello 클라이언트 탭에서 hello Azure MFA RADIUS 서비스가 비표준 포트에서 RADIUS 요청 toolisten 있어야 하는 경우 hello 인증 및 계정 포트를 변경 합니다.
4. **추가**를 클릭합니다.
5. Hello 어플라이언스/서버의 toohello Azure Multi-factor Authentication 서버, 프로그램 응용 프로그램 이름 (선택 사항) 및 공유 암호를 인증 하는 hello IP 주소를 입력 합니다.

  hello 응용 프로그램 이름은 Azure Multi-factor Authentication 보고서에 표시 되며 SMS 또는 모바일 앱 인증 메시지 내에서 표시 될 수 있습니다.

  두 hello Azure Multi-factor Authentication 서버에서 동일 및 어플라이언스/서버 hello 비밀 요구 toobe hello를 공유합니다.

6. Hello 확인 **Multi-factor Authentication 사용자 일치** 모든 사용자가 낮거나 서버 hello 및 주체 toomulti 2 단계 인증으로 가져올 경우 상자입니다. 많은 수의 사용자가을 아직 가져오지 서버 hello에 2 단계 인증에서 제외 될 경우, hello 상자를 선택 합니다.
7. Hello 확인 **대체 OATH 토큰 사용** 대체 toohello 대역의 전화 통화, SMS,으로 toouse OATH 암호 확인 모바일 앱에서 사용할 또는 푸시 알림 경우 상자입니다.
8. **확인**을 클릭합니다.

필요에 따라 많은 추가 RADIUS 클라이언트 8 tooadd-4 단계를 반복 합니다.

## <a name="configure-your-radius-client"></a>RADIUS 클라이언트 구성

1. Hello 클릭 **대상** 탭 합니다.
2. Azure MFA 서버 hello가 Active Directory 환경에 도메인 가입 서버에 설치 되어 Windows 도메인을 선택 합니다.
3. LDAP 디렉터리에 대해 사용자를 인증해야 하는 경우 **LDAP 바인딩**을 선택합니다.

  toouse LDAP 바인딩 hello 디렉터리 통합 아이콘을 클릭 하 고 hello 서버 바인딩할 수 tooyour 디렉터리 있도록 hello 설정 탭에서 hello LDAP 구성을 편집 합니다. Hello에서 LDAP를 구성 하기 위한 지침을 확인할 수 있습니다 [LDAP 프록시 구성 가이드](multi-factor-authentication-get-started-server-ldap.md)합니다.

4. 다른 RADIUS 서버에 대해 사용자를 인증해야 하는 경우 RADIUS 서버를 선택합니다.
5. 클릭 **추가** tooconfigure hello 서버 toowhich hello Azure MFA 서버는 프록시 hello RADIUS 요청 합니다.
6. Hello RADIUS 서버 추가 대화 상자에서 hello RADIUS 서버 및 공유 암호 hello IP 주소를 입력 합니다.

  두 hello Azure Multi-factor Authentication 서버에서 동일 하 고 RADIUS 서버 hello 비밀 요구 toobe hello를 공유합니다. Hello RADIUS 서버에서 다른 포트를 사용 하는 경우 hello 인증 포트와 계정 포트를 변경 합니다.

7. **확인**을 클릭합니다.
8. Hello Azure MFA 서버를 RADIUS 클라이언트로 추가 hello에 다른 RADIUS 서버로 tooit hello Azure MFA 서버에서에서 보낸 액세스 요청을 처리할 수 있도록 합니다. 동일한 hello Azure Multi-factor Authentication 서버에서에서 구성 된 비밀을 공유 하는 hello를 사용 합니다.

이러한 단계 tooadd RADIUS 서버를 더 반복한 hello 순서는 hello에 Azure MFA 서버를 호출 하 hello 구성 **위로 이동** 및 **아래로 이동** 단추입니다.

이 hello Azure Multi-factor Authentication 서버 구성이 완료 되었습니다. 서버 hello이 이제 hello 구성 된 클라이언트로부터 RADIUS 액세스 요청에 대 한 hello 구성 된 포트에서 수신 됩니다.   

## <a name="radius-client-configuration"></a>RADIUS 클라이언트 구성
tooconfigure hello RADIUS 클라이언트 hello 지침을 따르세요.

* hello RADIUS 서버 역할을 RADIUS toohello Azure Multi-factor Authentication 서버의 IP 주소를 통해 어플라이언스/서버 tooauthenticate 프로그램을 구성 합니다.
* 동일한 공유 암호를 이전에 구성 된 hello를 사용 합니다.
* 시간 toovalidate hello 사용자의 자격 증명 있도록 hello RADIUS 제한 시간 too30 ~ 60 초로 구성, 2 단계 인증을 수행, 해당 응답을 받 및 다음 toohello RADIUS 액세스 요청에 응답 합니다.
