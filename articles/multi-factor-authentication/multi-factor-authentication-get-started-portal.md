---
title: "Azure MFA 서버에 대 한 aaaUser 포털 | Microsoft Docs"
description: "Tooget Azure MFA 및 hello 사용자 포털을 시작 하는 방법을 설명 하는 hello Azure multi-factor authentication 페이지입니다."
services: multi-factor-authentication
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 06b419fa-3507-4980-96a4-d2e3960e1772
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: 0e36644c3d780249fb98d5da654e9d267c63561a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="user-portal-for-hello-azure-multi-factor-authentication-server"></a>Azure Multi-factor Authentication 서버 hello에 대 한 사용자 포털

hello 사용자 포털은 사용자가 tooenroll Azure Multi-factor Authentication (MFA)를 허용 하 고 자신의 계정을 관리할 수 있는 IIS 웹 사이트입니다. 사용자 전화 번호, PIN을 변경 또는 toobypass 자신의 다음 로그온 하는 동안 2 단계 인증을 선택 될 수 있습니다.

사용자가 자신의 일반 사용자 이름과 암호 toohello 사용자 포털에 로그인, 2 단계 확인 통화를 완료 하거나 보안 질문 toocomplete 인증 응답입니다. 사용자 등록이 허용 되는 경우 사용자가 자신의 전화 번호와 PIN hello 처음으로 로그인 할 포털에서 구성할 toohello 사용자.

사용자 포털 관리자를 설정 하 고 부여 된 사용 권한 tooadd 새 사용자와 기존 사용자 업데이트 될 수 있습니다.

사용자 환경에 따라 hello에 toodeploy hello 사용자 포털 경우가 동일한 서버 또는 다른 인터넷 연결 서버에 Azure Multi-factor Authentication 서버입니다.

![MFA 사용자 포털](./media/multi-factor-authentication-get-started-portal/portal.png)

> [!NOTE]
> hello 사용자 포털 에서만 Multi-factor Authentication 서버와 함께 제공 됩니다. Hello 클라우드에서 Multi-factor Authentication을 사용 하는 경우 사용자가 toohello 참조 [설치 2 단계 인증에 대 한 계정](./end-user/multi-factor-authentication-end-user-first-time.md) 또는 [2 단계 인증에 대 한 설정을 관리](./end-user/multi-factor-authentication-end-user-manage-settings.md)합니다.

## <a name="install-hello-web-service-sdk"></a>Hello 웹 서비스 SDK 설치

두 시나리오에서 경우 hello Azure Multi-factor Authentication 웹 서비스 SDK는 **하지** 전체 hello hello Azure Multi-factor Authentication (MFA) 서버에 이미 설치 되어 다음에 나오는 단계입니다.

1. Hello Multi-factor Authentication 서버 콘솔을 엽니다.
2. Toohello 이동 **웹 서비스 SDK** 선택 **웹 서비스 SDK 설치**합니다.
3. 전체 hello 설치 toochange 필요 하지 않으면 hello 기본값을 사용 하 여 몇 가지 이유로 합니다.
4. IIS에서 SSL 인증서 toohello 사이트는에 바인딩하십시오.

IIS 서버에서 SSL 인증서를 구성 하는 방법에 대 한 질문이 있으면 hello 문서 참조 [어떻게 tooSet IIS에서 SSL을](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis)합니다.

hello 웹 서비스 SDK가 SSL 인증서로 보호 되어야 합니다. 이 작업을 위해 자체 서명된 인증서를 사용해도 됩니다. Hello SSL 연결을 시작할 때 해당 인증서를 신뢰 있도록 hello 인증서를 hello hello 사용자 포털 웹 서버의 hello 로컬 컴퓨터 계정의 "신뢰할 수 있는 루트 인증 기관" 저장소로 가져옵니다.

![MFA 서버 구성 설정 웹 서비스 SDK](./media/multi-factor-authentication-get-started-portal/sdk.png)

## <a name="deploy-hello-user-portal-on-hello-same-server-as-hello-azure-multi-factor-authentication-server"></a>Hello에 hello 사용자 포털을 배포 hello Azure Multi-factor Authentication 서버와 동일한 서버

hello 다음 필수 구성 요소는 hello에 필요한 tooinstall hello 사용자 포털 **동일한 서버** 으로 Azure Multi-factor Authentication 서버 hello:

* ASP.NET 및 IIS 6 메타 베이스 호환성(IIS 7 이상)을 포함하는 IIS
* Hello 컴퓨터와 해당 하는 경우 도메인에 대 한 관리 권한이 있는 계정입니다. hello 계정 권한을 toocreate Active Directory 보안 그룹을 필요합니다.
* SSL 인증서로 hello 사용자 포털을 보호 합니다.
* SSL 인증서로 hello Azure Multi-factor Authentication 웹 서비스 SDK를 보호 합니다.

toodeploy는 사용자 포털에 따라 다음이 단계를 hello:

1. Hello Azure Multi-factor Authentication 서버 콘솔을 열고, hello 클릭 **사용자 포털** hello 아이콘 왼쪽 메뉴를 클릭 한 다음 **사용자 포털 설치**합니다.
2. 전체 hello 설치 toochange 필요 하지 않으면 hello 기본값을 사용 하 여 몇 가지 이유로 합니다.
3. SSL 인증서 toohello 사이트를 사용 하 여 IIS에 바인딩합니다

   > [!NOTE]
   > 이 SSL 인증서는 일반적으로 공개적으로 서명된 SSL 인증서입니다.

4. 모든 컴퓨터에서 웹 브라우저를 열고 hello 사용자 포털이 설치 된 toohello URL 이동 (예: https://mfa.contoso.com/MultiFactorAuth). 인증서 경고 또는 오류가 표시되지 않는지 확인합니다.

![MFA 서버 사용자 포털 설치](./media/multi-factor-authentication-get-started-portal/install.png)

IIS 서버에서 SSL 인증서를 구성 하는 방법에 대 한 질문이 있으면 hello 문서 참조 [어떻게 tooSet IIS에서 SSL을](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis)합니다.

## <a name="deploy-hello-user-portal-on-a-separate-server"></a>별도 서버 hello 사용자 포털 배포

Hello 사용자 포털을 설치 해야 hello 서버 Azure Multi-factor Authentication 서버 실행 되 고 있는 인터넷 없으면는 **별도, 인터넷 연결 서버**합니다.

조직에서 사용 hello 확인 방법 중 하나로 Microsoft Authenticator 앱 hello toodeploy hello 사용자 포털 자체 서버에서 완료 hello 요구 사항:

* V6.0를 사용 하 여 Azure Multi-factor Authentication 서버 hello의 이상.
* Microsoft 인터넷을 실행 하는 인터넷 연결 웹 서버에 hello 사용자 포털 설치 정보 서비스 (IIS) 6.x 이상이 있습니다.
* IIS를 사용 하는 경우 6.x ASP.NET v 2.0.50727 설치, 등록, 고도**허용**합니다.
* IIS 7.x 이상, IIS을 사용하는 경우 기본 인증, ASP.NET 및 IIS 6 메타 베이스 호환성을 포함합니다.
* SSL 인증서로 hello 사용자 포털을 보호 합니다.
* SSL 인증서로 hello Azure Multi-factor Authentication 웹 서비스 SDK를 보호 합니다.
* Hello 사용자 포털이 SSL을 통해 Azure Multi-factor Authentication 웹 서비스 SDK toohello를 연결할 수 있는지 확인 합니다.
* Hello 사용자 포털이 toohello Azure Multi-factor Authentication 웹 서비스 SDK에 인증할 수 있도록 hello 서비스 계정 자격 증명을 사용 하 여 hello "PhoneFactor Admins" 보안 그룹에 있습니다. Hello Azure Multi-factor Authentication 서버는 도메인에 가입 된 서버에서 실행 중인 경우이 서비스 계정 및 그룹이 Active Directory에 존재 해야 합니다. 이 서비스 계정 및 그룹 로컬로 존재 hello Azure Multi-factor Authentication 서버에서 조인 된 tooa 도메인이 아닌 경우.

Azure Multi-factor Authentication 서버 hello 아닌 서버에 hello 사용자 포털 설치 단계를 수행 하는 hello를 필요 합니다.

1. **MFA 서버 hello에**, 찾아보기 toohello 설치 경로 (예: C:\Program Files\multi-factor Authentication Server), 및 hello 파일 복사 **MultiFactorAuthenticationUserPortalSetup64** tooa 위치 액세스 가능한 toohello 인터넷 연결 서버를 설치할 것입니다.
2. **Hello 인터넷 연결 웹 서버에서**hello MultiFactorAuthenticationUserPortalSetup64 설치 파일을 관리자 권한으로 실행, 필요한 경우 사이트 hello 변경를 원하는 경우 hello 가상 디렉터리 tooa 짧은 이름을 변경 합니다.
3. IIS에서 SSL 인증서 toohello 사이트는에 바인딩하십시오.

   > [!NOTE]
   > 이 SSL 인증서는 일반적으로 공개적으로 서명된 SSL 인증서입니다.

4. 너무 찾아보기**C:\inetpub\wwwroot\MultiFactorAuth**
5. Hello Web.Config 파일을 메모장에서 편집

    * Hello 키를 찾을 **"USE_WEB_SERVICE_SDK"** 변경 **값 = "false"** 너무**값 = "true"**
    * Hello 키를 찾을 **"WEB_SERVICE_SDK_AUTHENTICATION_USERNAME"** 변경 **값 = ""** 너무**값 = "도메인 \ 사용자"** 여기서 도메인 \ 사용자는에 포함 되는 서비스 계정 "PhoneFactor Admins" 그룹입니다.
    * Hello 키를 찾을 **"WEB_SERVICE_SDK_AUTHENTICATION_PASSWORD"** 변경 **값 = ""** 너무**값 = "Password"** 여기서 p는 hello 서비스에 대 한 hello 암호 Hello 이전 줄에 입력 한 계정입니다.
    * Hello 식일 **https://www.contoso.com/MultiFactorAuthWebServiceSdk/PfWsSdk.asmx** 이 자리 표시자 URL toohello 2 단계에서 설치할 웹 서비스 SDK URL을 변경 합니다.
    * Hello Web.Config 파일을 저장 하 고 메모장을 닫습니다.

6. 모든 컴퓨터에서 웹 브라우저를 열고 hello 사용자 포털이 설치 된 toohello URL 이동 (예: https://mfa.contoso.com/MultiFactorAuth). 인증서 경고 또는 오류가 표시되지 않는지 확인합니다.

IIS 서버에서 SSL 인증서를 구성 하는 방법에 대 한 질문이 있으면 hello 문서 참조 [어떻게 tooSet IIS에서 SSL을](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis)합니다.

## <a name="configure-user-portal-settings-in-hello-azure-multi-factor-authentication-server"></a>Hello Azure Multi-factor Authentication 서버에서에서 사용자 포털 설정 구성

Hello 사용자 포털이 설치 되어 이제 tooconfigure hello Azure Multi-factor Authentication 서버 toowork hello 포털을 사용 해야 합니다.

1. Hello Azure Multi-factor Authentication 서버 콘솔에서 클릭 hello **사용자 포털** 아이콘입니다. Hello 설정 탭에서 hello URL toohello 사용자 포털 hello에 입력 **사용자 포털 URL** 텍스트 상자에 붙여넣습니다. 전자 메일 기능을 사용 하는 경우이 URL은 Azure Multi-factor Authentication 서버 hello로 가져올 때 toousers 전송 되는 hello 전자 메일에 포함 됩니다.
2. Hello 설정을 선택 hello 사용자 포털에서에서 toouse 되도록 합니다. 자신의 인증 방법을 확인 예를 들어 사용자에 게 toochoose 허용 되는 **tooselect 방법을 사용자가 사용할 수** hello 메서드 중에서 선택할 수와 함께 검사 됩니다.
3. Hello에 관리자를 있어야 사용자 정의 **관리자** 탭 합니다. 세분화 된 관리 권한을 hello 확인란 및 드롭다운을 사용 하 여 hello 추가/편집 상자에 만들 수 있습니다.

선택적 구성:
- **보안 질문** -정의에 나타나는 해당 환경 및 hello 언어에 대해 보안 질문을 승인 합니다.
- **전달된 세션** - MFA를 사용하여 양식 기반 웹 사이트에서 사용자 포털 통합을 구성합니다.
- **신뢰할 수 있는 Ip** -신뢰할 수 있는 Ip 또는 범위 목록에서 인증 하는 동안 사용자가 tooskip MFA를 허용 합니다.

![MFA 서버 사용자 포털 구성](./media/multi-factor-authentication-get-started-portal/config.png)

Azure Multi-factor Authentication 서버 사용자 포털 hello에 대 한 몇 가지 옵션을 제공합니다. hello 다음 표에서 이러한 옵션 및 용도 대 한 설명은 목록.

| 사용자 포털 설정 | 설명 |
|:--- |:--- |
| User Portal URL(사용자 포털 URL) | Hello 포털 호스팅되는지의 hello URL을 입력 합니다. |
| Primary authentication(기본 인증) | Toohello 포털에 로그인 할 때 인증 toouse hello 유형을 지정 합니다. Windows, Radius 또는 LDAP 인증 중 하나입니다. |
| 사용자가 toolog 허용 | Hello 사용자 포털에 대 한 hello 로그인 페이지에서 사용자가 tooenter 사용자 이름 및 암호를 허용 합니다. 이 옵션을 선택 하지 않으면 경우에 hello 상자가 회색으로 나타납니다. |
| Allow user enrollment(등록 허용) | Multi-factor Authentication에서 전화 번호와 같은 추가 정보를 묻는 tooa 설정 화면을 수행 하 여 사용자 tooenroll를 허용 합니다. 백업 전화 허용 사용자 toospecify 보조 전화 번호에 대 한 메시지를 표시 합니다. 제 3 자에 대 한 프롬프트 OATH 토큰 사용 하면 사용자 toospecify 타사 OATH 토큰입니다. |
| 사용자가 tooinitiate 일회성 바이패스 허용 | 사용자가 tooinitiate 일회성 바이패스를 허용 합니다. 사용자는이 옵션을 설정한 경우 걸리는 효과 hello hello 사용자가 로그인 하는 다음 번입니다. 바이패스에 대 한 프롬프트 hello 기본값인 300 초를 변경할 수 초 상자가 hello 사용자를 제공 합니다. 그렇지 않으면 hello 일회성 바이패스는만 300 초 동안 유효 합니다. |
| 사용자가 tooselect 메서드 허용 | 사용자가 toospecify 자신의 기본 연락 방법으로 허용 합니다. 전화 통화, 문자 메시지, 모바일 앱 또는 OATH 토큰 옵션 중 방법을 선택할 수 있습니다. |
| 사용자가 tooselect 언어 허용 | Toochange hello 언어 hello 전화 통화, 문자 메시지, 모바일 앱 또는 OATH 토큰에 사용 되는 사용자가 허용 합니다. |
| 사용자가 tooactivate 모바일 앱을 허용 합니다. | 정품 인증 코드 toocomplete hello 모바일 앱 활성화 프로세스 hello 서버 함께 사용 되는 사용자가 toogenerate를 허용 합니다.  장치를 활성화할 수 있습니다 hello 수를 설정할 수도 있습니다 hello 앱에서 1에서 10 사이입니다. |
| Use security questions for fallback(대체 방법으로 보안 질문 사용) | 2단계 검증에 실패한 경우 보안 질문을 허용합니다. Hello 성공적으로 대답 해야 하는 보안 질문 수를 지정할 수 있습니다. |
| 사용자가 tooassociate 타사 OATH 토큰을 허용 합니다. | 사용자가 toospecify 타사 OATH 토큰을 허용 합니다. |
| Use OATH token for fallback(대체 방법으로 OATH 토큰 사용) | 2 단계 확인이 완료 되는 경우 OATH 토큰의 hello 사용할 수 있도록 합니다. 분에서 hello 세션 제한 시간을 지정할 수도 있습니다. |
| 로깅 사용 | Hello 사용자 포털에 대 한 로깅을 사용 하도록 설정 합니다. hello 로그 파일은: C:\Program Files\multi-factor Authentication Server\Logs 합니다. |

이러한 설정은 활성화 되 고 toohello 사용자 포털 로그인 한 후 hello 포털에서 사용자 toohello 표시 됩니다.

![사용자 포털 설정](./media/multi-factor-authentication-get-started-portal/portalsettings.png)

### <a name="self-service-user-enrollment"></a>셀프 서비스 사용자 등록

사용자가 toosign 원하는 하 고 등록 하는 경우에 hello 선택 해야 **에 사용자가 toolog 허용** 및 **사용자 등록 허용** hello 설정 탭에서 옵션입니다. 선택한 hello 설정은 hello 사용자 로그인 환경에 영향을 기억 합니다.

예를 들어 사용자가 로그인 하면 hello에 대 한 사용자 포털 toohello 처음으로 이동 합니다 toohello Azure Multi-factor Authentication 사용자 설정 페이지. Azure Multi-factor Authentication을 구성 방식에 따라 hello 사용자 있습니다 수 tooselect 자신의 인증 방법 수 있습니다.

Hello 음성 통화 확인 방법을 선택 하거나 해당 방법을 미리 구성 된 toouse 되었습니다, 기본 전화 번호 및 해당 하는 경우 확장 hello 페이지 hello 사용자 tooenter 묻습니다. 또한 자산이 tooenter 예비 전화 번호를 허용 합니다.

![기본 및 백업 전화 번호 등록](./media/multi-factor-authentication-get-started-portal/backupphone.png)

Hello 사용자가 필요한 toouse PIN 인증 시에 모두 hello 페이지 프롬프트에 toocreate PIN을 사용 합니다. 전화 번호와 PIN (해당 하는 경우)를 입력 한 후 hello 클릭할 hello **지금 전화로 tooAuthenticate** 단추입니다. Azure Multi-factor Authentication 전화 통화 인증 toohello 사용자의 기본 전화 번호를 수행합니다. hello 사용자 hello 전화 통화에 답변 하 고 (있는 경우) PIN 입력 고 # toomove toohello hello 셀프 등록 프로세스의 다음 단계에서 키를 눌러 해야 합니다.

Hello 사용자 hello 문자 메시지 확인 방법 선택 하거나 해당 방법을 미리 구성 된 toouse 되었습니다를 hello 페이지 hello 사용자를 자신의 휴대폰 번호에 라는 메시지가 나타납니다. 이면 hello 사용자 필요한 toouse PIN 인증 시 hello 페이지도 묻습니다 tooenter PIN입니다.  자신의 전화 번호와 PIN (해당 하는 경우)를 입력 한 후 hello 클릭할 hello **지금 문자로 받기 tooAuthenticate** 단추입니다. Azure Multi-factor Authentication 된 SMS 확인 toohello 사용자의 휴대폰을 수행합니다. hello 사용자 hello 텍스트 메시지는 한-일회용 암호 otp (1) 된 다음 해당 OTP와 PIN (해당 하는 경우)으로 회신 toohello 메시지를 받습니다.

![사용자 포털 SMS](./media/multi-factor-authentication-get-started-portal/text.png)

Hello 사용자가 모바일 앱 확인 방법을 두 hello를 선택 하는 경우 hello 페이지 라는 hello 사용자 tooinstall hello Microsoft Authenticator 앱의 장치에서 메시지를 표시 하 고 활성화 코드를 생성 합니다. Hello 앱을 설치한 후 hello 사용자 hello 활성화 코드 생성 단추를 클릭 합니다.

> [!NOTE]
> toouse hello Microsoft Authenticator 앱 hello 사용자는 자신의 장치에서 푸시 알림을 설정 해야 합니다.

hello 페이지에는 다음 활성화 코드와 URL에 바코드 그림과 함께 표시 됩니다. 이면 hello 사용자 필요한 toouse PIN 인증 시 hello 페이지 또한 묻습니다 tooenter PIN입니다. hello 사용자 hello Microsoft Authenticator 앱에 hello 활성화 코드와 URL을 입력 하 고 또는 hello 바코드 스캐너 tooscan hello 바코드 그림을 사용 하 여, hello [활성화] 단추를 클릭 합니다.

Hello 활성화 완료 되 면 hello 클릭할 hello **지금 인증** 단추입니다. Azure Multi-factor Authentication 확인 toohello 사용자의 모바일 앱을 수행합니다. hello 사용자는 자신의 PIN (해당 하는 경우)을 입력 하 고 자신의 모바일 앱 toomove의 toohello hello 셀프 등록 프로세스의 다음 단계를 hello 인증 단추를 누릅니다 해야 합니다.

Hello 관리자가 hello Azure Multi-factor Authentication 서버 toocollect 보안 질문 및 답변을 구성한 경우 hello 사용자 toohello 보안 질문 페이지로 이동 됩니다. hello 사용자는 4 개의 보안 질문을 선택 하 고 선택한 tootheir 질문 응답을 제공 해야 합니다.

![사용자 포털 보안 질문](./media/multi-factor-authentication-get-started-portal/secq.png)

hello 이로써 사용자 셀프 등록이 완료 되며 hello 사용자가 toohello 사용자 포털에 로그인 합니다. 사용자는 로그인 다시 toohello 사용자 포털 hello 이후 toochange에서 언제 든 지 전화 번호, Pin, 인증 방법 및 본인 확인 질문 관리자가 허용 되는 해당 메서드를 변경 합니다.

## <a name="next-steps"></a>다음 단계

- [Hello Azure Multi-factor Authentication 서버 모바일 앱 웹 서비스를 배포 합니다.](multi-factor-authentication-get-started-server-webservice.md)
