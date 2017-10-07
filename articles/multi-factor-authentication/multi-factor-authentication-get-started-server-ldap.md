---
title: "aaaLDAP 인증 및 Azure MFA 서버 | Microsoft Docs"
description: "LDAP 인증 및 Azure Multi-factor Authentication 서버를 배포 하는 데 도움이 되는 hello Azure multi-factor authentication 페이지입니다."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: e1a68568-53d1-4365-9e41-50925ad00869
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: 17a26b57dbf6afa2fcfdb3d19c5b5ba2987a9f79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="ldap-authentication-and-azure-multi-factor-authentication-server"></a>LDAP 인증 및 Azure Multi-Factor Authentication 서버
기본적으로 hello Azure Multi-factor Authentication 서버는 구성 된 tooimport 또는 Active Directory에서 사용자를 동기화 합니다. 그러나 ADAM 디렉터리 또는 특정 Active Directory 도메인 컨트롤러와 같은 구성 된 toobind toodifferent LDAP 디렉터리 수 있습니다. LDAP, hello Azure Multi-factor Authentication 서버를 통해 연결 된 tooa 디렉터리 경우 LDAP 프록시 tooperform 인증 작동할 수 있습니다. Hello LDAP 바인딩을 RADIUS 대상으로 IIS 인증을 통해 사용자의 사전 인증에 사용 하거나 사용할 hello Azure MFA 사용자 포털에서 기본 인증을 위해 수도 있습니다.

Azure Multi-factor Authentication을 LDAP 프록시로 toouse hello LDAP 클라이언트 (예: VPN 어플라이언스, 응용 프로그램)와 LDAP 디렉터리 서버 hello hello Azure Multi-factor Authentication 서버를 삽입 합니다. Azure Multi-factor Authentication 서버 hello hello 클라이언트 서버 및 hello LDAP 디렉터리 모두와 구성 된 toocommunicate 이어야 합니다. 이 구성에서는 hello Azure Multi-factor Authentication 서버 클라이언트 서버 및 응용 프로그램의 LDAP 요청을 수락 하 고 toohello 대상 LDAP 디렉터리 서버 toovalidate hello 기본 자격 증명을 전달 합니다. Hello LDAP 디렉터리에 hello 기본 자격 증명 유효성을 검사 하는 경우 Azure Multi-factor Authentication 두 번째 id 확인을 수행 하 고 응답 백 toohello LDAP 클라이언트에 보냅니다. hello 전체 인증은 LDAP 서버 인증 hello 및 hello 두 번째 단계 인증 모두 성공 하는 경우에 성공 합니다.

## <a name="configure-ldap-authentication"></a>LDAP 인증 구성
Windows 서버에 Azure Multi-factor Authentication 서버 설치 hello tooconfigure LDAP 인증 합니다. 절차를 수행 하는 hello를 사용 합니다.

### <a name="add-an-ldap-client"></a>LDAP 클라이언트를 추가합니다.

1. Azure Multi-factor Authentication 서버 hello hello 왼쪽된 메뉴에 hello LDAP 인증 아이콘을 선택 합니다.
2. Hello 확인 **LDAP 인증 사용** 확인란을 선택 합니다.

   ![LDAP 인증](./media/multi-factor-authentication-get-started-server-ldap/ldap2.png)

3. Hello 클라이언트 탭에서 Azure Multi-factor Authentication LDAP 서비스 hello LDAP 요청에 대 한 표준 toonon 포트 toolisten 바인딩해야 하는 경우 hello TCP 포트 및 SSL 포트를 변경 합니다.
4. Hello에 SSL 인증서를 설치 해야 hello 클라이언트 toohello Azure Multi-factor Authentication 서버에서에서 toouse LDAPS를 사용 하도록 하려는 경우 MFA 서버와 같은 서버. 클릭 **찾아보기** 다음 toohello SSL 인증서 상자 고 hello 보안 연결에 대 한 인증서 toouse를 선택 합니다.
5. **추가**를 클릭합니다.
6. Hello LDAP 클라이언트 추가 대화 상자에서 hello 어플라이언스, 서버 또는 toohello 서버 및 응용 프로그램 이름 (옵션)를 인증 하는 응용 프로그램의 hello IP 주소를 입력 합니다. hello 응용 프로그램 이름은 Azure Multi-factor Authentication 보고서에 표시 되며 SMS 또는 모바일 앱 인증 메시지 내에서 표시 될 수 있습니다.
7. Hello 확인 **Azure Multi-factor Authentication 사용자 일치** 하면 모든 사용자가 낮거나 서버 hello 및 주체 tootwo 단계 확인으로 가져올 수 있습니다. 많은 수의 사용자가을 아직 가져오지 서버 hello에 2 단계 인증에서 제외 된 경우, hello 상자를 선택 합니다. 이 기능에 대 한 자세한 내용은 hello와 MFA 서버 도움말 파일을 참조 합니다.

이러한 단계 tooadd 추가 LDAP 클라이언트를 반복 합니다.

### <a name="configure-hello-ldap-directory-connection"></a>Hello LDAP 디렉터리 연결 구성

LDAP 인증 구성된 tooreceive hello Azure Multi-factor Authentication을 사용 하는 경우 프록시 인증 toohello LDAP 디렉터리에 해당 해야 합니다. 따라서 hello 대상 탭만 표시 됩니다는 단일 옵션 toouse는 LDAP 대상을 회색입니다.

1. tooconfigure hello LDAP 디렉터리 연결 클릭 hello **디렉터리 통합** 아이콘입니다.
2. Hello 설정 탭 선택 hello **특정 LDAP 구성 사용** 라디오 단추입니다.
3. **편집…**을 선택합니다.
4. Hello LDAP 구성 편집 대화 상자에서 hello 필요한 정보 tooconnect toohello LDAP 디렉터리와 hello 필드를 채웁니다. Hello 필드 hello Azure Multi-factor Authentication 서버 도움말 파일에 포함 됩니다.

    ![디렉터리 통합](./media/multi-factor-authentication-get-started-server-ldap/ldap.png)

5. Hello를 클릭 하 여 hello LDAP 연결 테스트 **테스트** 단추입니다.
6. Hello LDAP 연결 테스트가 성공 하면 클릭 hello **확인** 단추입니다.
7. Hello 클릭 **필터** 탭 hello 서버는 미리 구성 된 tooload 컨테이너, 보안 그룹 및 Active Directory에서 사용자입니다. Tooa 다른 LDAP 디렉터리에 바인딩하는 경우 표시 되는 tooedit hello 필터 필요 합니다. Hello 클릭 **도움말** 필터에 대 한 자세한 내용은 링크 합니다.
8. Hello 클릭 **특성** 탭 hello 서버는 Active Directory에서 미리 구성 된 toomap 특성입니다.
9. Tooa 다른 LDAP 디렉터리 또는 toochange hello 미리 구성 된 특성 매핑을 바인딩하는 경우 클릭 **편집...**
10. Hello 속성 편집 대화 상자에서 디렉터리에 대 한 hello LDAP 특성 매핑을 수정 합니다. 특성 이름에 입력 하거나 hello를 클릭 하 여 선택한 수 **...** 단추 다음 tooeach 필드입니다. Hello 클릭 **도움말** 특성에 대 한 자세한 내용은 링크 합니다.
11. Hello 클릭 **확인** 단추입니다.
12. Hello 클릭 **회사 설정** 아이콘과 선택 hello **사용자 이름 확인** 탭 합니다.
13. TooActive 디렉터리 도메인에 가입 된 서버에서 연결 유지 hello **사용자 이름 일치에 사용 하 여 Windows 보안 식별자 (Sid)** 라디오 단추를 선택 합니다. 그렇지 않으면 hello **LDAP 고유 식별자 특성 사용 사용자 이름 일치에** 라디오 단추입니다. 

Hello 때 **LDAP 고유 식별자 특성 사용 사용자 이름 일치에** 라디오 단추가 선택 되어, Azure Multi-factor Authentication 서버 hello 시도 tooresolve hello LDAP 디렉터리의 각 사용자 이름 tooa 고유 식별자입니다. LDAP 검색 수행 hello 사용자 이름에서 디렉터리 통합 hello에 정의 된 특성-> 특성 탭 합니다. 사용자를 인증 하면 hello 사용자 이름은 해결된 toohello hello LDAP 디렉터리의 고유 식별자입니다. hello 고유 식별자는 일치 하는 hello 사용자 hello Azure Multi-factor Authentication 데이터 파일에 사용 됩니다. 이를 통해 대/소문자 구분 비교 및 길고 짧은 사용자 이름 형식 사용이 가능합니다.

다음이 단계를 완료 한 후 hello 로부터의 LDAP 액세스 요청에 대 한 hello 구성 된 포트에서 hello와 MFA 서버 수신 클라이언트, 그리고 역할으로 구성 하는 것에 대 한 프록시 인증에 대 한 LDAP 디렉터리 toohello 요청.

## <a name="configure-ldap-client"></a>LDAP 클라이언트 구성
tooconfigure hello LDAP 클라이언트 hello 지침을 따르세요.

* LDAP 디렉터리인 것 처럼 어플라이언스, 서버 또는 응용 프로그램 tooauthenticate LDAP toohello Azure Multi-factor Authentication 서버를 통해 구성 합니다. 사용 하 여 hello 동일 tooconnect 일반적으로 사용 하려는 설정을 직접 tooyour LDAP 디렉터리를 제외한 hello 서버 이름 또는 IP 주소는 Azure Multi-factor Authentication 서버 hello 됩니다.
* Hello LDAP 디렉터리와 시간 toovalidate hello 사용자의 자격 증명 있도록 hello LDAP 제한 시간 too30 ~ 60 초로 구성 hello 두 번째 단계 확인을 수행, 응답을 받아 및 toohello LDAP 액세스 요청에 응답 합니다.
* LDAPS를 사용 하는 경우 hello 어플라이언스 또는 hello LDAP 쿼리 서버 인증서를 신뢰 해야 hello SSL hello Azure Multi-factor Authentication 서버에 설치 합니다.

