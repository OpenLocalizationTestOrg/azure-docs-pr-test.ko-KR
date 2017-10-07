---
title: "인증 및 Azure MFA 서버 aaaIIS | Microsoft Docs"
description: "IIS 인증 및 Azure Multi-factor Authentication 서버를 배포 하는 데 도움이 되는 hello Azure multi-factor authentication 페이지입니다."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d1bf1c8a-2c10-4ae6-9f4b-75f0c3df43eb
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/16/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017,it-pro
ms.openlocfilehash: 74bd39c2644e2bca0880baea3824cad4c9215111
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-for-iis-web-apps"></a>IIS 웹앱용 Azure Multi-Factor Authentication 서버 구성

Hello Azure Multi-factor Authentication (MFA) 서버 tooenable의 hello IIS 인증 섹션을 사용 하 고 Microsoft IIS 웹 응용 프로그램과 통합에 대 한 IIS 인증을 구성 합니다. Azure MFA 서버 hello toohello IIS 웹 서버 tooadd Azure Multi-factor Authentication 수행 되는 요청을 필터링 할 수 있는 플러그 인을 설치 합니다. hello IIS 플러그 인은 양식 기반 인증 및 Windows HTTP 통합 인증에 대 한 지원 합니다. Ip는 또한 2 단계 인증에서 내부 IP 주소 구성된 tooexempt 수 신뢰할 수 있습니다.

![IIS 인증](./media/multi-factor-authentication-get-started-server-iis/iis.png)

## <a name="using-form-based-iis-authentication-with-azure-multi-factor-authentication-server"></a>Azure Multi-Factor Authentication 서버에서 양식 기반 IIS 인증 사용
IIS 웹 양식 기반 인증을 사용 하는 응용 프로그램, IIS 웹 서버 hello에 hello Azure Multi-factor Authentication 서버를 설치 및 구성 toosecure 절차를 수행 하는 hello 당 서버 hello:

1. Azure Multi-factor Authentication 서버 hello hello 왼쪽된 메뉴에 hello IIS 인증 아이콘을 클릭 합니다.
2. Hello 클릭 **양식 기반** 탭 합니다.
3. **추가**를 클릭합니다.
4. toodetect 사용자 이름, 암호 및 도메인 변수에서 자동으로 로그인 URL (예: https://localhost/contoso/auth/login.aspx) hello hello 양식 기반 웹 사이트 대화 상자에서를 입력 하 고 클릭 **확인**합니다.
5. Hello 확인 **Multi-factor Authentication 사용자 일치** 모든 사용자가 낮거나 서버 hello 및 주체 toomulti 2 단계 인증으로 가져올 경우 상자입니다. 많은 수의 사용자가 아직으로 가져오지 않은 서버 hello multi-factor authentication에서 제외 될 경우, hello 상자를 선택 합니다.
6. Hello 페이지 변수를 자동으로 검색할 수 없는 경우 클릭 **수동으로 지정** hello 양식 기반 웹 사이트 대화 상자에서.
7. Hello 양식 기반 웹 사이트 대화 상자에서 hello URL toohello 로그인 페이지 hello 제출 URL 필드에 입력 하 고 응용 프로그램 이름 (옵션)을 입력 합니다. hello 응용 프로그램 이름은 Azure Multi-factor Authentication 보고서에 표시 되며 SMS 또는 모바일 앱 인증 메시지 내에서 표시 될 수 있습니다.
8. Hello 올바른 요청 형식을 선택 합니다. 이 설정은 너무**POST 또는 GET** 대부분의 웹 응용 프로그램에 대 한 합니다.
9. (Hello 로그인 페이지에 표시) 하는 경우 hello 사용자 이름 변수, 암호 변수 및 도메인 변수를 입력 합니다. hello toofind hello 이름 입력 상자, 웹 브라우저에서 toohello 로그인 페이지 탐색, hello 페이지를 마우스 오른쪽 단추로 클릭 및 선택 **소스 보기**합니다.
10. Hello 확인 **Azure Multi-factor Authentication 사용자 일치** 모든 사용자가 낮거나 서버 hello 및 주체 toomulti 2 단계 인증으로 가져올 경우 상자입니다. 많은 수의 사용자가 아직으로 가져오지 않은 서버 hello multi-factor authentication에서 제외 될 경우, hello 상자를 선택 합니다.
11. 클릭 **고급** tooreview 고급 설정을 포함 하 여:

  - 사용자 지정 거부 페이지 파일 선택
  - 쿠키를 사용 하 여 일정 기간에 대 한 캐시 성공한 인증 toohello 웹 사이트
  - Windows 도메인, LDAP 디렉터리에 대해 tooauthenticate hello 기본 자격 증명을 선택 합니다. 또는 RADIUS 서버입니다.

12. 클릭 **확인** tooreturn toohello 양식 기반 웹 사이트 대화 상자.
13. **확인**을 클릭합니다.
14. URL을 한 번 hello 및 페이지 변수가 검색 또는 입력, hello 웹 사이트 데이터가 양식 기반 패널 hello에 표시 합니다.

## <a name="using-integrated-windows-authentication-with-azure-multi-factor-authentication-server"></a>Azure Multi-Factor Authentication 서버에서 Windows 통합 인증 사용
toosecure IIS 웹 Windows HTTP 통합 인증을 사용 하는 응용 프로그램, Azure MFA 서버 hello hello IIS 웹 서버에서 다음 구성 단계를 수행 하는 hello와 서버 hello:

1. Azure Multi-factor Authentication 서버 hello hello 왼쪽된 메뉴에 hello IIS 인증 아이콘을 클릭 합니다.
2. Hello 클릭 **HTTP** 탭 합니다.
3. **추가**를 클릭합니다.
4. Hello 기준 URL 추가 대화 상자에서 hello 웹 사이트 (예: http://localhost/owa) HTTP 인증을 수행 하는 위치에 대 한 hello URL을 입력 하 고 응용 프로그램 이름 (옵션)를 제공 합니다. hello 응용 프로그램 이름은 Azure Multi-factor Authentication 보고서에 표시 되며 SMS 또는 모바일 앱 인증 메시지 내에서 표시 될 수 있습니다.
5. 조정 hello 유휴 시간 제한 및 최대 세션 횟수 hello 기본값이 충분 하지 않은 경우.
6. Hello 확인 **Multi-factor Authentication 사용자 일치** 모든 사용자가 낮거나 서버 hello 및 주체 toomulti 2 단계 인증으로 가져올 경우 상자입니다. 많은 수의 사용자가 아직으로 가져오지 않은 서버 hello multi-factor authentication에서 제외 될 경우, hello 상자를 선택 합니다.
7. Hello 확인 **쿠키 캐시** 원하는 경우 상자입니다.
8. **확인**을 클릭합니다.

## <a name="enable-iis-plug-ins-for-azure-multi-factor-authentication-server"></a>Azure Multi-Factor Authentication 서버에 대해 IIS 플러그인 사용
구성한 후 양식 기반 hello 또는 HTTP 인증 Url과 설정, 여기서 hello Azure Multi-factor Authentication IIS 플러그 인을 로드 하 여 IIS에서 사용 하는 위치를 환영 합니다. 절차를 수행 하는 hello를 사용 합니다.

1. IIS 6에서 실행 하는 경우 클릭 hello **ISAPI** 탭 합니다. 웹 응용 프로그램 hello 선택 hello 웹 사이트 (예: 기본 웹 사이트 아래) 실행 tooenable hello Azure Multi-factor Authentication ISAPI 필터 플러그 인 해당 사이트에 대 한 합니다.
2. 이상에서 IIS 7을 실행 하는 경우 클릭 hello **네이티브 모듈** 탭 합니다. Hello 서버, 웹 사이트 또는 응용 프로그램 tooenable hello hello 원하는 수준에서 IIS 플러그 인을 선택 합니다.
3. Hello 클릭 **사용 하도록 설정 하는 IIS 인증** hello hello 화면 위쪽에 상자입니다. Azure Multi-factor Authentication이 hello 선택한 IIS 응용 프로그램을 보호 합니다. 사용자가 서버 hello로 가져왔는지 확인 하십시오.

## <a name="trusted-ips"></a>신뢰할 수 있는 IP
hello 신뢰할 수 있는 Ip 사용 하면 특정 IP 주소나 서브넷에서 생성 되는 웹 사이트 요청에 대 한 Azure Multi-factor Authentication 사용자가 toobypass. 예를 들어 Azure Multi-factor Authentication에서 사용자가 tooexempt hello 사무실에서 로그인 해 있는 동안 좋습니다. 이 경우 신뢰할 수 있는 Ip 항목으로 hello office 서브넷을 지정 합니다. 신뢰할 수 있는 ip 주소로 tooconfigure 절차를 수행 하는 hello를 사용 합니다.

1. Hello IIS 인증 섹션에서에서 클릭 hello **신뢰할 수 있는 Ip** 탭 합니다.
2. **추가**를 클릭합니다.
3. Hello 신뢰할 수 있는 Ip 추가 대화 상자가 나타나면 선택 hello **단일 IP**, **IP 범위**, 또는 **서브넷** 라디오 단추입니다.
4. Hello IP 주소, IP 주소 범위 또는 허용 목록 이어야 하는 서브넷을 입력 합니다. 네트워크 마스크를 적절 한 서브넷, 선택 hello를 입력 하 고 클릭 **확인**합니다. hello 화이트 리스트 이제 추가 되었습니다.
