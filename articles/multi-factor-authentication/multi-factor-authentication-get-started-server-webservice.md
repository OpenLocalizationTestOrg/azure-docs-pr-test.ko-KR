---
title: "MFA 서버 모바일 앱 웹 서비스 aaaAzure | Microsoft Docs"
description: "hello Microsoft Authenticator 앱 대역의 인증 옵션을 추가로 제공합니다.  MFA 서버 toouse 푸시 알림 toousers hello 수 있습니다."
services: multi-factor-authentication
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 6c8d6fcc-70f4-4da4-9610-c76d66635b8b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: 4175b68fcbf85ec3fd53d8edf4e07306c75a4c71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-mobile-app-authentication-with-azure-multi-factor-authentication-server"></a>Azure Multi-Factor Authentication 서버를 사용하여 모바일 앱 인증 활성화

hello Microsoft Authenticator 앱 추가-대역외 확인 옵션을 제공합니다. 자동된 전화 통화 나 SMS toohello 사용자 로그인 하는 동안에 거는 대신 Azure Multi-factor Authentication hello 사용자의 스마트폰 또는 태블릿에 알림 toohello Microsoft Authenticator 앱을 푸시합니다. hello 사용자는 간단히 **확인** (또는 PIN을 입력 하 고 "인증"을 탭)에서 로그인 앱 toocomplete hello 합니다.

전화 수신을 신뢰할 수 없는 경우 2단계 인증에 모바일 앱을 사용하는 것이 좋습니다. OATH 토큰 생성기로 hello 앱을 사용 하는 경우 모든 네트워크 또는 인터넷 연결이 필요 하지 합니다.

사용자 환경에 따라 toodeploy hello 모바일 앱 웹 서비스에 hello 경우가 동일한 서버 또는 다른 인터넷 연결 서버에 Azure Multi-factor Authentication 서버입니다.

## <a name="requirements"></a>요구 사항

toouse hello Microsoft Authenticator 앱 hello 앱 통신할 수 있도록 성공적으로 모바일 앱 웹 서비스와 hello 다음이 필요 합니다.

* Azure Multi-Factor Authentication 서버 v6.0 이상
* Microsoft® [IIS(인터넷 정보 서비스) 7.x 이상](http://www.iis.net/)이 실행되는 인터넷 연결 웹 서버에 모바일 앱 웹 서비스 설치
* ASP.NET v4.0.30319 설치, 등록 및 tooAllowed 설정
* 필요한 역할 서비스에는 ASP.NET 및 IIS 6 메타베이스 호환성이 포함됩니다.
* 모바일 앱 웹 서비스는 공용 URL을 통해 액세스할 수 있음
* 모바일 앱 웹 서비스는 SSL 인증서로 보호됩니다.
* IIS에서 hello Azure Multi-factor Authentication 웹 서비스 SDK 설치 7.x 이상을 hello에 **hello Azure Multi-factor Authentication 서버와 동일한 서버**
* hello Azure Multi-factor Authentication 웹 서비스 SDK가 SSL 인증서로 보호 됩니다.
* 모바일 앱 웹 서비스가 SSL을 통해 Azure Multi-factor Authentication 웹 서비스 SDK toohello를 연결할 수 있습니다.
* 모바일 앱 웹 서비스 toohello Azure MFA 웹 서비스 SDK에 인증할 수 hello hello "PhoneFactor Admins" 보안 그룹의 구성원 인 서비스 계정 자격 증명을 사용 하 여 합니다. 이 서비스 계정 및 그룹 hello Azure Multi-factor Authentication 서버는 도메인에 가입 된 서버에 있으면 Active Directory에 존재 합니다. 이 서비스 계정 및 그룹 로컬로 존재 hello Azure Multi-factor Authentication 서버에서 조인 된 tooa 도메인이 아닌 경우.

## <a name="install-hello-mobile-app-web-service"></a>Hello 모바일 앱 웹 서비스 설치

Hello 모바일 앱 웹 서비스를 설치 하기 전에 다음 세부 정보는 hello 고려해 야 합니다.

* "PhoneFactor Admins" 그룹의 일부인 서비스 계정이 있어야 합니다. 이 계정은 hello 하나 hello와 동일 hello 사용자 포털 설치 하기 위해 사용할 수 있습니다.
* 유용한 tooopen hello 인터넷 연결 웹 서버에서 웹 브라우저 사용 되며 hello hello web.config 파일에 입력 한 웹 서비스 SDK의 toohello URL을 탐색 합니다. Hello 브라우저 toohello 웹 서비스를 성공적으로 가져올 수, 하는 경우 자격 증명을 묻는 해야 것입니다. Hello 사용자 이름 및 hello 파일에 표시 된 대로 정확히 hello web.config 파일에 입력 했던 암호를 입력 합니다. 인증서 경고 또는 오류가 표시되지 않는지 확인합니다.
* 역방향 프록시 또는 방화벽이 hello 모바일 앱 웹 서비스 웹 서버 앞에 있는 것을 SSL 오프 로드를 수행 하는 경우 hello 모바일 앱 웹 서비스가 사용할 수 있도록 http 대신 https hello 모바일 앱 웹 서비스 web.config 파일을 편집할 수 있습니다. SSL은 hello toohello 방화벽/역방향 프록시 모바일 앱에서에서 여전히 필요 합니다. 다음 키 toohello hello 추가 \<appSettings\> 섹션:

        <add key="SSL_REQUIRED" value="false"/>

### <a name="install-hello-web-service-sdk"></a>Hello 웹 서비스 SDK 설치

두 시나리오에서 경우 hello Azure Multi-factor Authentication 웹 서비스 SDK는 **하지** 전체 hello hello Azure Multi-factor Authentication (MFA) 서버에 이미 설치 되어 다음에 나오는 단계입니다.

1. Hello Multi-factor Authentication 서버 콘솔을 엽니다.
2. Toohello 이동 **웹 서비스 SDK** 선택 **웹 서비스 SDK 설치**합니다.
3. 전체 hello 설치 toochange 필요 하지 않으면 hello 기본값을 사용 하 여 몇 가지 이유로 합니다.
4. IIS에서 SSL 인증서 toohello 사이트는에 바인딩하십시오.

IIS 서버에서 SSL 인증서를 구성 하는 방법에 대 한 질문이 있으면 hello 문서 참조 [어떻게 tooSet IIS에서 SSL을](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis)합니다.

hello 웹 서비스 SDK가 SSL 인증서로 보호 되어야 합니다. 이 작업을 위해 자체 서명된 인증서를 사용해도 됩니다. Hello SSL 연결을 시작할 때 해당 인증서를 신뢰 있도록 hello 인증서를 hello hello 사용자 포털 웹 서버의 hello 로컬 컴퓨터 계정의 "신뢰할 수 있는 루트 인증 기관" 저장소로 가져옵니다.

![MFA 서버 구성 설정 웹 서비스 SDK](./media/multi-factor-authentication-get-started-server-webservice/sdk.png)

### <a name="install-hello-service"></a>Hello 서비스 설치

1. **MFA 서버 hello에**, toohello 설치 경로 찾습니다.
2. Toohello 이동 hello Azure MFA 서버는 설치 된 hello 기본 폴더는 **C:\Program Files\Azure Multi-factor Authentication**합니다.
3. Hello 설치 파일을 찾을 **MultiFactorAuthenticationMobileAppWebServiceSetup64**합니다. Hello 서버 경우 **하지** 복사 hello 설치 파일 toohello 인터넷 연결 서버 인터넷에 연결 합니다.
4. MFA 서버는 경우 hello **하지** 인터넷 스위치 toohello **인터넷 연결 서버**합니다.
5. Hello 실행 **MultiFactorAuthenticationMobileAppWebServiceSetup64** 관리자 권한으로 파일을 설치 하 고 필요한 경우 사이트 hello 변경 원하는 경우 hello 가상 디렉터리 tooa 짧은 이름을 변경 합니다.
6. 마무리 hello 설치 후 찾아볼 너무**C:\inetpub\wwwroot\MultiFactorAuthMobileAppWebService** (또는 hello 가상 디렉터리 이름에 따라 적절 한 디렉터리) hello Web.Config 파일을 편집 합니다.

   * Hello 키를 찾을 **"WEB_SERVICE_SDK_AUTHENTICATION_USERNAME"** 변경 **값 = ""** 너무**값 = "도메인 \ 사용자"** 여기서 도메인 \ 사용자는에 포함 되는 서비스 계정 "PhoneFactor Admins" 그룹입니다.
   * Hello 키를 찾을 **"WEB_SERVICE_SDK_AUTHENTICATION_PASSWORD"** 변경 **값 = ""** 너무**값 = "Password"** 여기서 p는 hello 서비스에 대 한 hello 암호 Hello 이전 줄에 입력 한 계정입니다.
   * Hello **pfMobile App Web Service_pfwssdk_PfWsSdk** 설정 하 고 hello 값에서 변경 **http://localhost:4898/PfWsSdk.asmx** toohello 웹 서비스 SDK의 URL (예: https://mfa.contoso.com/ MultiFactorAuthWebServiceSdk/PfWsSdk.asmx)입니다.
   * Hello Web.Config 파일을 저장 하 고 메모장을 닫습니다.

   > [!NOTE]
   > 이 연결에 SSL이 사용 되므로 참조 해야 하 여 웹 서비스 SDK hello **정규화 된 도메인 이름 (FQDN)** 및 **IP 주소가 아닌**합니다. hello SSL 인증서가 발급 된 hello FQDN에 대 한 및 hello 사용 되는 URL 이름과 일치 해야 hello hello 인증서입니다.

7. 모바일 앱 웹 서비스에서 설치 된 hello 웹 사이트는 공개적으로 서명 된 인증서로 바인딩되어 있지 이미, hello 인증서 hello 서버에 설치, IIS 관리자를 열고 고 hello 인증서 toohello 웹 사이트를 바인딩하십시오.
8. 모든 컴퓨터에서 웹 브라우저를 열고 모바일 앱 웹 서비스가 설치 된 toohello URL 이동 (예: https://mfa.contoso.com/MultiFactorAuthMobileAppWebService). 인증서 경고 또는 오류가 표시되지 않는지 확인합니다.

## <a name="configure-hello-mobile-app-settings-in-hello-azure-multi-factor-authentication-server"></a>Hello Azure Multi-factor Authentication 서버에서에서 hello 모바일 앱 설정 구성

Hello 모바일 앱 웹 서비스를 설치 해야 tooconfigure hello Azure Multi-factor Authentication 서버 toowork hello 포털을 사용 합니다.

1. Hello Multi-factor Authentication 서버 콘솔에서 hello 사용자 포털 아이콘을 클릭 합니다. 사용자에 게 toocontrol 허용 된 자신의 인증 방법을 확인 **모바일 앱** hello 설정 탭에서 아래 **tooselect 메서드 사용자가 허용**합니다. 이 기능을 사용 하도록 설정 하지 않으면 최종 사용자는 필요한 toocontact hello 모바일 앱에 대 한 지원 센터 toocomplete 활성화 합니다.
2. Hello 확인 **사용자 tooactivate 모바일 앱을 허용** 상자입니다.
3. Hello 확인 **사용자 등록 허용** 상자입니다.
4. Hello 클릭 **모바일 앱** 아이콘입니다.
5. MultiFactorAuthenticationMobileAppWebServiceSetup64를 설치할 때 생성 된 hello 가상 디렉터리와 사용 중인 hello URL 입력 (예: https://mfa.contoso.com/MultiFactorAuthMobileAppWebService/) hello 필드에  **모바일 앱 웹 서비스 URL:**합니다.
6. Hello 채울 **계정 이름** hello 회사 또는 조직 이름 toodisplay hello이이 계정에 대 한 모바일 응용 프로그램의 필드입니다.
   ![MFA 서버 구성 Mobile App 설정](./media/multi-factor-authentication-get-started-server-webservice/mobile.png)

## <a name="next-steps"></a>다음 단계

- [Azure Multi-Factor Authentication 및 타사 VPN을 사용한 고급 시나리오](multi-factor-authentication-advanced-vpn-configurations.md)