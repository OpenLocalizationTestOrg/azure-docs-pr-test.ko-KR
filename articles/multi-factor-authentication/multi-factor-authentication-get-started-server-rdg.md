---
title: "aaaRDG 및 RADIUS를 사용 하는 Azure MFA 서버 | Microsoft Docs"
description: "RD (원격 데스크톱) 게이트웨이 및 Azure Multi-factor Authentication 서버 RADIUS를 사용 하 여를 배포 하는 데 도움이 되는 hello Azure multi-factor authentication 페이지입니다."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f2354ac4-a3a7-48e5-a86d-84a9e5682b42
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/27/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: fd280e9b6ff90c82927cffe593c4f1fda7047842
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="remote-desktop-gateway-and-azure-multi-factor-authentication-server-using-radius"></a>RADIUS를 사용한 원격 데스크톱 게이트웨이 및 Azure Multi-Factor Authentication 서버
종종 RD (원격 데스크톱) 게이트웨이 hello 로컬 서비스 NPS (네트워크 정책) tooauthenticate 사용자를 사용합니다. 이 문서에서는 RADIUS tooroute 아웃 hello 원격 데스크톱 게이트웨이에서 요청 하는 방법을 설명 (을 통해 로컬 NPS hello) toohello Multi-factor Authentication 서버입니다. hello Azure MFA 및 RD 게이트웨이의 조합을 사용자가 액세스할 수 있음을 의미의 작업 환경 어디에서 든 강력한 인증을 수행 하는 중입니다. 

터미널 서비스에 대해 Windows 인증 Server 2012 r 2에 대 한 지원 되지 않으므로, MFA 서버와 RD 게이트웨이 및 RADIUS toointegrate를 사용 합니다. 

Hello RADIUS 요청을 프록시 hello 원격 데스크톱 게이트웨이 서버에서 NPS toohello 백업 하는 별도 서버에 hello Azure Multi-factor Authentication 서버를 설치 합니다. NPS hello 사용자 이름 및 암호 유효성을 검사 한 후 응답 toohello Multi-factor Authentication 서버를 반환 합니다. 그런 다음 MFA 서버 hello hello 2 단계 인증을 결과 toohello 게이트웨이 반환 합니다.

## <a name="prerequisites"></a>필수 조건

- 도메인에 가입된 Azure MFA 서버. 이미 설치 된 없다면 hello 단계에 따라 [Azure Multi-factor Authentication 서버 hello로 시작](multi-factor-authentication-get-started-server.md)합니다.
- 네트워크 정책 서비스를 인증하는 원격 데스크톱 게이트웨이.

## <a name="configure-hello-remote-desktop-gateway"></a>Hello 원격 데스크톱 게이트웨이 구성 합니다.
Hello RD 게이트웨이 toosend RADIUS 인증 tooan Azure Multi-factor Authentication 서버를 구성 합니다. 

1. RD 게이트웨이 관리자에서 hello 서버 이름을 마우스 오른쪽 단추로 클릭 하 고 선택 **속성**합니다.
2. Toohello 이동 **RD CAP 저장소** 탭을 선택한 **NPS를 실행 하는 중앙 서버**합니다. 
3. RADIUS 서버로 hello 이름 또는 각 서버의 IP 주소를 입력 하 여 하나 이상의 Azure Multi-factor Authentication 서버를 추가 합니다. 
4. 각 서버에 대한 공유 암호를 만듭니다.

## <a name="configure-nps"></a>NPS 구성
hello RD 게이트웨이 NPS toosend hello RADIUS 요청 tooAzure Multi-factor Authentication을 사용합니다. NPS tooconfigure 먼저 hello 제한 시간 설정을 변경한 tooprevent hello RD 게이트웨이 시간 초과 전에 hello 2 단계 확인을 완료 합니다. 그런 다음 MFA 서버에서 NPS tooreceive RADIUS 인증을 업데이트합니다. 다음 프로시저 tooconfigure NPS hello를 사용 합니다.

### <a name="modify-hello-timeout-policy"></a>Hello 제한 시간 정책 수정

1. NPS에서 열고 hello **RADIUS 클라이언트 및 서버** hello 선택한 열을 왼쪽의 메뉴 **원격 RADIUS 서버 그룹**합니다. 
2. 선택 hello **TS 게이트웨이 서버 그룹**합니다. 
3. Toohello 이동 **부하 분산** 탭 합니다. 
4. 두 hello 변경 **요청이 것으로 간주 되기 전에 응답 없이 시간 (초)을 삭제** 및 hello **서버가 사용할 수 없는 상태로 표시 된 경우 요청 사이의 시간 (초)** toobetween 30 및 60 시간 (초)입니다. (해당 hello 서버 여전히 제한 시간이 인증 중에 찾을 수 여기로 돌아와서 있으며 hello 시간 (초) 늘립니다.)
5. Toohello 이동 **인증/계정** 탭 하 고 hello RADIUS 포트가 일치 hello Multi-factor Authentication 서버에서 수신 대기 하는 hello 포트 지정 되어 있는지 확인 합니다.

### <a name="prepare-nps-tooreceive-authentications-from-hello-mfa-server"></a>Hello와 MFA 서버에서에서 NPS tooreceive 인증 준비

1. 마우스 오른쪽 단추로 클릭 **RADIUS 클라이언트** RADIUS 클라이언트와 서버 hello 왼쪽 열 및 선택에에서 아래 **새로**합니다.
2. Hello Azure Multi-factor Authentication 서버를 RADIUS 클라이언트로 추가 합니다. 친숙한 이름을 선택하고 공유 암호를 지정합니다.
3. 열기 hello **정책** hello 선택한 열을 왼쪽의 메뉴 **연결 요청 정책**합니다. RD 게이트웨이를 구성할 때 만든 TS 게이트웨이 권한 부여 정책이라는 정책이 있어야 합니다. 이 정책은 RADIUS 요청 toohello Multi-factor Authentication 서버를 전달합니다.
4. **TS 게이트웨이 권한 부여 정책**을 마우스 오른쪽 단추로 클릭하고 **복제 정책**을 선택합니다. 
5. Hello 새 정책 및 go toohello 열고 **조건** 탭 합니다.
6. Hello 클라이언트 이름이 Azure Multi-factor Authentication 서버 RADIUS 클라이언트 hello에 대 한 2 단계에서 설정한 hello 친숙 한 이름 일치 하는 조건을 추가 합니다. 
7. Toohello 이동 **설정** 탭을 선택한 **인증**합니다.
8. Hello 인증 공급자도 변경**이 서버에서 요청을 인증**합니다. 이 정책을 통해 NPS hello Azure MFA 서버에서에서 RADIUS 요청을 받으면, hello 인증이 RADIUS 요청 백 toohello 루프 상황을 발생 시키는 Azure Multi-factor Authentication 서버를 전송 하는 대신 로컬로 발생 합니다. 
9. 루프 조건 tooprevent hello hello에서 원래 정책 보다 위에 정렬 되는 새 정책을 hello 있는지 확인 **연결 요청 정책** 창.

## <a name="configure-azure-multi-factor-authentication"></a>Azure Multi-Factor Authentication 구성

hello Azure Multi-factor Authentication 서버는 RD 게이트웨이와 NPS 간의 RADIUS 프록시로 구성 됩니다.  Hello RD 게이트웨이 서버와에서 별개의 도메인에 가입 된 서버에 설치 되어야 합니다. 다음 프로시저 tooconfigure hello Azure Multi-factor Authentication 서버 hello를 사용 합니다.

1. Azure Multi-factor Authentication 서버 hello 열고 hello RADIUS 인증 아이콘을 선택 합니다. 
2. Hello 확인 **RADIUS 인증 사용** 확인란을 선택 합니다.
3. Hello 클라이언트 탭에서 hello 포트가 NPS에 구성 된 일치 해야 하 고 선택 **추가**합니다.
4. Hello RD 게이트웨이 서버 IP 주소, 응용 프로그램 이름 (선택 사항) 및 공유 암호를 추가 합니다. hello 공유 비밀 요구 toobe hello hello Azure Multi-factor Authentication 서버와 RD 게이트웨이 모두에서 동일 합니다.
3. Toohello 이동 **대상** 탭 및 선택 hello **RADIUS 서버** 라디오 단추입니다.
4. 선택 **추가** hello IP 주소, 공유 암호 및 hello NPS 서버의 포트를 입력 합니다. 중앙 NPS를 사용 하지 않는 hello RADIUS 클라이언트 및 RADIUS 대상은 같은 hello 됩니다. hello 공유 암호는 hello hello NPS 서버의 RADIUS 클라이언트 섹션에서에서 설정한 hello 일치 해야 합니다.

![RADIUS 인증](./media/multi-factor-authentication-get-started-server-rdg/radius.png)

## <a name="next-steps"></a>다음 단계

- Azure MFA 및 [IIS 웹앱](multi-factor-authentication-get-started-server-iis.md) 통합

- Hello에 대 한 답변을 얻을 [Azure Multi-factor Authentication FAQ](multi-factor-authentication-faq.md)
