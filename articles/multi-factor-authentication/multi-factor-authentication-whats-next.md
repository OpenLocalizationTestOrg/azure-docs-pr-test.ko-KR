---
title: Azure MFA aaaConfigure | Microsoft Docs
description: "MFA를 다음 어떤 toodo를 설명 하는 hello Azure multi-factor authentication 페이지입니다.  보고서, 사기 행위 경고, 일회성 바이패스, 사용자 지정 음성 메시지, 캐시, 신뢰할 수 있는 ip 및 앱 암호를 포함합니다."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 75af734e-4b12-40de-aba4-b68d91064ae8
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/21/2017
ms.author: kgremban
ms.openlocfilehash: 7f6d0b0975a2c1da2de9b52e978b84475c79b218
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-settings"></a>Azure Multi-Factor Authentication 구성 설정
이 문서는 준비하고 실행 중인 Multi-Factor Authentication을 관리하는데 도움이 됩니다.  Azure Multi-factor Authentication을 최대한 활용 tooget hello 수 있는 다양 한 항목을 다룹니다.  모든 버전의 Azure Multi-Factor Authentication에서 이러한 모든 기능을 사용할 수는 없습니다.

| 기능 | 설명 | 
|:--- |:--- |
| [사기 행위 경고](#fraud-alert) |사기 경고를 구성 하 고 사용자가 사기 시도 tooaccess 해당 리소스를 보고할 수 있도록 설정할 수 있습니다. |
| [일회성 바이패스](#one-time-bypass) |일회성 바이패스는 multi-factor authentication "무시" 하 여 사용자 tooauthenticate를 단일 시간 수 있습니다. |
| [사용자 지정 음성 메시지](#custom-voice-messages) |사용자 지정 음성 메시지 허용 toouse 고유한 녹음/녹화 또는 multi-factor authentication greetings 합니다. |
| [캐싱](#caching-in-azure-multi-factor-authentication) |캐싱 사용 tooset 특정 기간 동안 있으므로 하 후속 인증 시도 자동으로 성공 합니다. |
| [신뢰할 수 있는 IP](#trusted-ips) |관리 되는 또는 페더레이션된 테 넌 트의 관리자는 사용자 hello 회사의 로컬 인트라넷에서 로그인에 대 한 신뢰할 수 있는 Ip toobypass 2 단계 인증을 사용할 수 있습니다. |
| [앱 암호](#app-passwords) |앱 암호에는 응용을 프로그램 인식 MFA toobypass 다단계 인증 하 고 있는 작업을 계속할 수 있습니다. |
| [기억된 장치 및 브라우저용 Multi-Factor Authentication 기억](#remember-multi-factor-authentication-for-devices-that-users-trust) |있습니다 tooremember 장치를 일 후 사용자가 MFA를 사용 하 여 로그인 성공적으로 설정 된 시간. |
| [선택 가능한 확인 방법](#selectable-verification-methods) |사용자가 toouse에 사용할 수 있는 toochoose hello 인증 방법을 있습니다. |

## <a name="access-hello-azure-mfa-management-portal"></a>Hello Azure MFA 관리 포털에 액세스

이 문서에 포함 된 hello 기능의 hello Azure Multi-factor Authentication 관리 포털에서에서 구성 됩니다. 두 가지 방법으로 tooaccess hello hello Azure 클래식 포털을 통해 MFA 관리 포털. Multi-factor Auth 공급자를 관리 하 여 hello 먼저 됩니다. 두 번째 hello은 hello MFA 서비스 설정을 통해 이루어집니다. 

### <a name="use-an-auth-provider"></a>인증 공급자 사용

사용량 기반 MFA에 대 한 Multi-factor Auth 공급자를 사용 하는 경우이 메서드 tooaccess hello 관리 포털을 사용 합니다.

tooaccess hello Azure Multi-factor Auth 공급자를 통해 MFA 관리 포털, 관리자 권한으로 Active Directory 옵션 선택 hello Azure 클래식 포털을 hello에 로그인 합니다. Hello 클릭 **Multi-factor Auth 공급자** 탭 한 다음 디렉터리를 선택 하 고, hello 클릭 **관리** hello 아래쪽 단추입니다.

### <a name="use-hello-mfa-service-settings-page"></a>Hello MFA 서비스 설정 페이지를 사용 하 여 

Multi-factor Auth 공급자 또는 Azure MFA를 설정한 경우 Azure AD Premium 또는 Enterprise Mobility + 보안 라이선스가 메서드 tooaccess hello MFA 서비스 설정 페이지를 사용 합니다.

tooaccess는 hello hello 관리자 권한으로 Azure 클래식 포털에 로그인 MFA 서비스 설정 페이지를 통해 MFA 관리 포털을 hello 고 hello Active Directory 옵션을 선택 합니다. 디렉터리를 클릭 하 고 클릭 hello **구성** 탭 합니다. Hello multi-factor authentication 섹션에서 선택 **서비스 설정 관리**합니다. Hello MFA 서비스 설정 페이지의 맨 아래 hello에 hello 클릭 **Go toohello 포털** 링크 합니다.


## <a name="fraud-alert"></a>사기 행위 경고
사기 경고를 구성 하 고 사용자가 사기 시도 tooaccess 해당 리소스를 보고할 수 있도록 설정할 수 있습니다.  사용자가 hello 모바일 앱 또는 전화 번호를 통해 사기 행위를 보고할 수 있습니다.

### <a name="set-up-fraud-alert"></a>사기 행위 경고 설정
1. 이 페이지의 hello 위쪽 hello 지침 당 toohello MFA 관리 포털을 탐색 합니다.
2. Hello Azure Multi-factor Authentication 관리 포털에서에서 클릭 **설정을** hello 구성 섹션에서.
3. Hello hello 설정 페이지의 사기 행위 경고 섹션에서 확인 hello **사용자가 toosubmit 사기 경고 허용** 확인란을 선택 합니다.
4. 선택 **저장** tooapply 변경 내용을 합니다. 

### <a name="configuration-options"></a>구성 옵션

- **사기 행위가 보고되면 사용자 차단** - 사용자가 사기 행위를 보고하면 해당 계정은 차단됩니다.
- **초기 한 인사말 중 사기 행위 tooReport 코드** -사용자가 # tooconfirm 2 단계 인증에 정상적으로 키를 누릅니다. Tooreport 사기 원하는 #를 누르기 전에 코드를 입력 합니다. 이 코드의 기본값은 **0**이지만, 사용자가 지정할 수 있습니다.

> [!NOTE]
> Microsoft의 기본 음성 인사말 사용자 toopress &#0; toosubmit 사기 행위 경고를 지시합니다. 원하는 toouse 0이 아닌 코드를 기록 하 고 적절 한 지침이 포함 된 사용자 고유의 사용자 지정 음성 인사말과 업로드 해야 합니다.

![사기 행위 경고 옵션 - 스크린샷](./media/multi-factor-authentication-whats-next/fraud.png)

### <a name="how-users-report-fraud"></a>사용자가 사기 행위를 보고하는 방법 
두 가지 방법으로 사기 행위 경고를 보고할 수 있습니다.  통해 또는 hello 모바일 앱 hello 전화를 통해.  

#### <a name="report-fraud-with-hello-mobile-app"></a>Hello 모바일 앱으로 사기 보고
1. 유효성 검사 tooyour 전화를 보낼 때 tooopen hello Microsoft Authenticator 앱을 선택 합니다.
2. 선택 **Deny** hello 알림입니다. 
3. **사기 행위 보고**를 선택합니다.
4. Hello 닫기는 응용 프로그램.

#### <a name="report-fraud-with-a-phone"></a>휴대폰으로 사기 행위 보고
1. 확인 전화가 tooyour 전화에 도달할 경우 전화를 합니다.  
2. tooreport 사기 (기본값은 0 임) hello 사기 코드를 입력 한 후 # 기호를 hello 합니다. 그러면 사기 행위 경고가 전송되었다는 알림이 표시됩니다.
3. Hello 통화를 종료 합니다.

### <a name="view-fraud-reports"></a>사기 행위 보고 보기
1. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.
2. Hello 왼쪽에서 Active Directory를 선택 합니다.
3. Hello 상위 선택에서 **Multi-factor Auth 공급자**합니다. 그러면 Multi-Factor Auth 공급자의 목록이 표시됩니다.
4. Multi-factor Auth 공급자를 선택 하 고 클릭 **관리** hello hello 페이지 맨 아래에 있습니다. hello Azure Multi-factor Authentication 관리 포털이 열립니다.
5. Hello 보고서를 보기에서 Azure Multi-factor Authentication 관리 포털에서 클릭 **사기 행위 경고**합니다.
6. Hello 보고서에 tooview 한다고 hello 날짜 범위를 지정 합니다. 사용자 이름, 전화 번호 및 hello 사용자의 상태를 지정할 수도 있습니다.
7. **실행**을 클릭합니다. 그러면 사기 행위 경고 보고서가 열립니다. 클릭 **tooCSV 내보내기** tooexport hello 보고서를 선택 합니다.

## <a name="one-time-bypass"></a>일회성 바이패스
일회성 바이패스 2 단계 인증을 수행 하지 않고 사용자 tooauthenticate를 단일 시간 수 있습니다. hello 바이패스는 일시적 이며 지정된 된 수의 시간 (초) 후에 만료 됩니다. 여기서 hello 모바일 앱 또는 전화를 받지 알림 또는 전화 통화의 경우 hello 사용자 hello 필요한 리소스에 액세스할 수 있도록 일회성 바이패스를 사용할 수 있습니다.

### <a name="create-a-one-time-bypass"></a>일회성 바이패스 만들기
1. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.
2. 이 페이지의 hello 위쪽 hello 지침 당 toohello MFA 관리 포털을 탐색 합니다.
3. Hello Azure Multi-factor Authentication 관리 포털에서에서 테 넌 트 또는 Azure MFA 공급자의 hello 이름에 표시 되 면 hello 엄청 한  **+**  다음 tooit hello 클릭  **+**  다른 MFA 서버 복제 그룹 및 hello Azure 기본 그룹을 참조 하십시오. Hello 적절 한 그룹을 선택 합니다.
4. 사용자 관리에서 **일회성 바이패스**를 클릭합니다.
5. Hello 일회성 바이패스 페이지에서 클릭 **새 일회성 바이패스**합니다.

  ![클라우드](./media/multi-factor-authentication-whats-next/create1.png)

6. Hello 사용자 이름을 입력, hello 수가 hello 바이패스 시간 (초)은 존재 하며, hello hello 바이패스에 대 한 설명입니다. **바이패스**를 클릭합니다.
7. hello 시간 제한 발효 되 즉시 하므로 hello 사용자의 요구 사항을 toosign 전에 hello 일회성 바이패스 만료 합니다. 

### <a name="view-hello-one-time-bypass-report"></a>보기 hello 일회성 바이패스 보고서
1. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.
2. Hello 왼쪽에서 Active Directory를 선택 합니다.
3. Hello 상위 선택에서 **Multi-factor Auth 공급자**합니다. 그러면 Multi-Factor Auth 공급자의 목록이 표시됩니다.
4. Multi-factor Auth 공급자를 선택 하 고 클릭 **관리** hello hello 페이지 맨 아래에 있습니다. hello Azure Multi-factor Authentication 관리 포털이 열립니다.
5. Hello 왼쪽에서 보고서를 보기 아래의 hello Azure Multi-factor Authentication 관리 포털에서 클릭 **일회성 바이패스**합니다.
6. Hello 보고서에 tooview 한다고 hello 날짜 범위를 지정 합니다. 사용자 이름, 전화 번호 및 hello 사용자의 상태를 지정할 수도 있습니다.
7. **실행**을 클릭합니다. 그러면 바이패스 보고서가 열립니다. 클릭 **tooCSV 내보내기** tooexport hello 보고서를 선택 합니다.

## <a name="custom-voice-messages"></a>사용자 지정 음성 메시지
사용자 지정 음성 메시지 허용 toouse 고유한 녹음/녹화 또는 greetings 2 단계 인증에 대 한 합니다. 이러한 추가 tooor tooreplace hello Microsoft 레코드에서 사용할 수 있습니다.

시작 하기 전에 hello 다음 고려해 야 합니다.

* 지원 되는 hello 파일 형식은.wav 및.mp3 됩니다.
* hello 파일 크기 제한은 5MB입니다.
* 인증 메시지 길이는 20초 미만이어야 합니다. 모든 것이 보다 긴 하면 hello 메시지 완료 되 면 발생 hello 확인 tootime 아웃 하기 전에 hello 사용자 응답 하지 않을 수 있습니다 hello 확인 toofail을 발생할 수 있습니다.

### <a name="set-up-a-custom-message"></a>사용자 지정 메시지 설정

사용자 지정 메시지는 두 개의 부분 toocreating 합니다. 첫째, hello 메시지를 업로드 하 고 켜기 사용자.

tooupload 사용자 지정 메시지:

1. 지원 되는 hello 파일 형식 중 하나를 사용 하 여 사용자 지정 음성 메시지를 만듭니다.
2. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.
3. 이 페이지의 hello 위쪽 hello 지침 당 toohello MFA 관리 포털을 탐색 합니다.
4. Hello Azure Multi-factor Authentication 관리 포털에서에서 클릭 **음성 메시지** hello 구성 섹션에서.
5. Hello 구성에서: 음성 메시지 페이지를 클릭 **새 음성 메시지**합니다.
   ![클라우드](./media/multi-factor-authentication-whats-next/custom1.png)
6. Hello 구성에서: 새 음성 메시지 페이지 클릭 **사운드 파일 관리**합니다.
   ![클라우드](./media/multi-factor-authentication-whats-next/custom2.png)
7. Hello 구성에서: 사운드 파일 페이지에서 클릭 **사운드 파일 업로드**합니다.
   ![클라우드](./media/multi-factor-authentication-whats-next/custom3.png)
8. Hello 구성에서: 사운드 파일 업로드를 클릭 **찾아보기** tooyour 음성 메시지를 이동를 클릭 하 고 **열려**합니다.
9. 설명을 추가하고 **업로드**를 클릭합니다.
10. 이 작업을 완료 메시지 hello 파일을 성공적으로 업로드 했는지 확인 합니다.

tooturn hello 메시지에 사용자를 위해:

1. Hello 왼쪽에서 클릭 **음성 메시지**합니다.
2. Hello 음성 메시지 섹션에서 클릭 **새 음성 메시지**합니다.
3. Hello 언어 드롭다운 목록에서에서 언어를 선택 합니다.
4. 이 메시지는 특정 응용 프로그램에 대 한 경우 hello 응용 프로그램 상자에서 지정 합니다.
5. Hello 메시지 유형 드롭다운 목록에서에서 새 사용자 지정 메시지로 재정의할 메시지 유형을 toobe를 hello를 선택 합니다.
6. 사운드 파일 드롭 다운 hello에서 업로드 한 사운드 파일이 hello hello 첫 번째 부분에서 선택 합니다.
7. **만들기**를 클릭합니다. 메시지는 성공적으로 음성 메시지를 만들었음을 확인합니다.
    ![클라우드](./media/multi-factor-authentication-whats-next/custom5.png)</center>

## <a name="caching-in-azure-multi-factor-authentication"></a>Azure Multi-Factor Authentication에서 캐싱
캐싱 사용 tooset 특정 기간 동안 있으므로 하 후속 인증 시도 기간 내에 자동으로 성공 합니다. 이 온-프레미스 시스템 VPN과 같은 hello 첫 번째 요청은 진행 중인 동안 여러 인증 요청을 보낼 때 주로 사용 됩니다. 그러면 hello 후속 요청 toosucceed 자동으로 hello 사용자 성공한 hello 첫 번째 확인 중입니다. 

캐싱은 로그인 tooAzure AD에 사용 되는 의도 된 toobe 하지입니다.

### <a name="set-up-caching"></a>캐싱 설정 
1. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.
2. 이 페이지의 hello 위쪽 hello 지침 당 toohello MFA 관리 포털을 탐색 합니다.
3. Hello Azure Multi-factor Authentication 관리 포털에서에서 클릭 **캐싱** hello 구성 섹션에서.
4. 캐싱 페이지 hello 구성에서 클릭 **새 캐시**합니다.
5. Hello 캐시 유형 및 hello 캐시 시간 (초)을 선택 합니다. **만들기**를 클릭합니다.

<center>![클라우드](./media/multi-factor-authentication-whats-next/cache.png)</center>

## <a name="trusted-ips"></a>신뢰할 수 있는 IP
신뢰할 수 있는 Ip는 관리 되는 또는 페더레이션된 테 넌 트의 관리자가 사용자 hello 회사의 로컬 인트라넷에서 로그인에 대 한 toobypass 2 단계 인증을 사용할 수 있는 Azure MFA의 기능입니다. 이 기능은 hello 정식 버전의 무료 버전 관리자를 위한 hello Azure Multi-factor Authentication을 사용할 수 있습니다. Tooget 정식 버전의 Azure Multi-factor Authentication을 hello 하는 방법에 대 한 세부 정보를 참조 하십시오. [Azure Multi-factor Authentication](multi-factor-authentication.md)합니다.

| Azure AD 테넌트의 유형 | 사용 가능한 신뢰할 수 있는 IP 옵션 |
|:--- |:--- |
| 관리 |<li>특정 IP 주소 범위 – 관리자는 hello 회사의 인트라넷에서 로그인 하는 사용자에 대 한 2 단계 인증을 바이패스할 수 있는 다양 한 IP 주소를 지정할 수 있습니다.</li> |
| 페더레이션 |<li>모든 페더레이션 사용자-사용자가 로그인 하는 모든 페더레이션에 hello 내 조직을 우회 하는 AD FS에서 발급 한 클레임을 사용 하 여 2 단계 인증 합니다.</li><br><li>특정 IP 주소 범위 – 관리자는 hello 회사의 인트라넷에서 로그인 하는 사용자에 대 한 2 단계 인증을 바이패스할 수 있는 다양 한 IP 주소를 지정할 수 있습니다. |

이 바이패스는 회사의 인트라넷 내부에서만 작동합니다. 예를 들어 모든 페더레이션된 사용자가 선택한 사용자가 외부 hello 회사의 인트라넷에서 로그인 하는 경우 해당 사용자에 게 tooauthenticate hello 사용자는 AD FS 클레임을 제시 하는 경우 2 단계 인증을 사용 하 여 합니다. 

**회사 네트워크 내부 최종 사용자 환경:**

신뢰할 수 있는 IP를 사용할 수 없는 경우 브라우저 흐름에 2단계 인증이 필요하고 이전 리치 클라이언트 앱에 앱 암호가 필요합니다. 

2 단계 확인을 신뢰할 수 있는 Ip를 사용 하는 경우 *하지* 브라우저 흐름의 경우에 필요한 및 앱 암호가 *하지* hello 사용자 이미를 만들지 않았는지는 이전 리치 클라이언트 앱에 필요한 프로그램 응용 프로그램 암호입니다. 앱 암호를 사용 중인 경우 필요합니다. 

**회사 네트워크 외부 최종 사용자 환경:**

신뢰할 수 있는 IP 사용 여부에 관계없이 브라우저 흐름에 2단계 인증이 필요하고 이전 리치 클라이언트 앱에 앱 암호가 필요합니다. 

### <a name="tooenable-trusted-ips"></a>tooenable 신뢰할 수 있는 Ip
1. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.
2. 이 문서의 hello 시작 시 hello 지침 당 toohello MFA 서비스 설정 페이지를 이동 합니다.
3. Trusted ips hello 서비스 설정 페이지는 두 가지 옵션이 있습니다.
   
   * **내 인트라넷에서 시작 된 페더레이션된 사용자의 요청에 대 한** – hello 확인란 합니다. Hello 회사 네트워크에서 로그인 하는 모든 페더레이션된 사용자는 AD FS에서 발급 한 클레임을 사용 하 여 2 단계 인증을 바이패스 합니다.
   * **특정 범위의 공용 Ip의 요청에 대 한** – CIDR 표기법을 사용 하 여 제공 하는 hello 텍스트 상자에 hello IP 주소를 입력 합니다. 예를 들어: hello 범위 xxx.xxx.xxx.1 –에서 IP 주소에 대 한 xxx.xxx.xxx.0/24 xxx.xxx.xxx.254 또는 단일 IP 주소에 대 한 xxx.xxx.xxx.xxx/32. Too50 IP 주소 범위를 입력할 수 있습니다. 이러한 IP 주소에서 로그인한 사용자는 2단계 인증을 바이패스합니다.
4. **Save**를 클릭합니다.
5. Hello 업데이트를 적용 한 후 클릭 **닫기**합니다.

![신뢰할 수 있는 IP](./media/multi-factor-authentication-whats-next/trustedips3.png)

## <a name="app-passwords"></a>앱 암호
Office 2010 이전 및 Apple 메일 등의 일부 앱은 2단계 인증을 지원하지 않습니다. 구성 된 tooaccept 두 번째 확인 되지 않습니다. toouse 이러한 앱을 기존 암호 대신 "응용 프로그램 암호" toouse 필요 합니다. hello 앱 암호는 hello 응용 프로그램 toobypass 2 단계 인증을 허용 하 고 작업을 계속 합니다.

> [!NOTE]
> Office 2013 클라이언트 hello에 대 한 최신 인증
> 
> Office 2013 클라이언트 (Outlook 포함) 및 최신 지원 최신 인증 프로토콜 사용된 toowork 2 단계 확인 하나일 수 있습니다. 이를 사용하면 이러한 클라이언트에 대한 앱 암호는 필요하지 않습니다.  자세한 내용은 [발표된 Office 2013 최신 인증 공개 미리 보기](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)를 참조하세요.

### <a name="important-things-tooknow-about-app-passwords"></a>앱 암호에 대 한 중요 한 사항이 tooknow
hello 다음은 중요 한 목록 प ् ल ि 알고 있어야 하는 것입니다.

* 앱 암호는 앱 당 한 번 입력 한 toobe를 하나만 있습니다. 사용자가 없습니다 그중에서 tookeep 추적 하 고 때마다를 입력 합니다.
* hello 실제 암호는 자동으로 생성 하 고 hello 사용자에서 제공 되지 않는 합니다. 이 hello 자동으로 생성 된 암호는 공격자가 tooguess 어려우므로 더 안전 때문입니다.
* 사용자당 40개의 암호로 제한되어 있습니다. 
* 암호를 캐시 하는 hello 조직 id 외부 hello 앱 암호에 알지 이후 실패 하기 시작 하는 데 수 온-프레미스 시나리오에서 사용 하 여 앱을 선택 합니다. 예로 온-프레미스 Exchange 전자 메일 않으며 hello 보관 된 메일은 hello 클라우드입니다. hello 동일한 암호가 작동 하지 않습니다.
* 사용자 계정에 Multi-Factor Authentication을 사용하도록 설정되었으면 대부분의 브라우저가 아닌 클라이언트(예: Outlook 및 Lync)에 앱 암호를 사용할 수 있지만, Windows PowerShell과 같은 브라우저가 아닌 응용 프로그램을 통해서는 사용자에게 관리 계정이 있어도 앱 암호를 사용하여 관리 작업을 수행할 수 없습니다.  서비스 계정을 강력한 암호 toorun PowerShell 스크립트를 만들고 2 단계 인증에 대 한 해당 계정을 사용 하지 않습니다 확인 합니다.

> [!WARNING]
> 앱 암호는 클라이언트가 온-프레미스 및 클라우드 자동 검색 끝점과 통신하는 하이브리드 환경에서는 작동하지 않습니다. 도메인 암호는 필수 tooauthenticate 온-프레미스 및 앱 암호는 필수 tooauthenticate hello 클라우드와 때문입니다.

### <a name="naming-guidance-for-app-passwords"></a>앱 암호에 대한 명명 지침
앱 암호 이름은 사용 하는 hello 장치를 반영 해야 합니다. 예를 들어 Outlook, Word 및 Excel 등의 브라우저 이외 앱이 있는 노트북을 사용하도록 설정한 경우 Laptop 이름을 딴 앱 암호를 하나 만들고 해당 앱 암호를 이러한 응용 프로그램에서 사용합니다. 그런 다음 다른 만들 앱 암호 Desktop에 대해 명명 된 hello 데스크톱 컴퓨터에서 동일한 응용 프로그램입니다. 

Microsoft는 응용 프로그램별로 하나의 앱 암호보다는 장치별로 하나의 앱 암호를 만드는 것을 권장합니다.

### <a name="federated-sso-app-passwords"></a>페더레이션된(SSO) 앱 암호
Azure AD는 온-프레미스 Windows Server Active Directory Domain Services(AD DS)로 페더레이션(Single Sign-On)을 지원합니다. 조직의 Azure AD와 페더레이션 되 고 Azure Multi-factor Authentication을 사용 하 여 toobe 하려는 다음 hello 앱 암호에 대 한 다음 정보는 중요 한 됩니다. 이 섹션에는 toofederated (SSO) 고객만 적용 됩니다.

* Azure AD에서 앱 암호를 확인하기 때문에 페더레이션을 바이패스합니다. 앱 암호를 설정할 때 페더레이션이 능동적으로 사용됩니다.
* 페더레이션된 (SSO) 사용자에서는 이동 하지 hello 수동 흐름과 달리 IdP (Id 공급자) toohello. hello 암호 hello 조직 id에 저장 됩니다. Hello 사용자가 회사 hello를 완료 하는 경우에 해당 정보를 실시간으로 DirSync를 사용 하 여 tooflow tooorganizational id에 있습니다. 계정 사용 안 함/삭제가 toothree 시간 toosync, Azure AD에 앱 암호 사용 안 함/삭제가 지연를 차지할 수 있습니다.
* 앱 암호를 사용할 경우 온-프레미스 클라이언트 액세스 제어 설정은 적용되지 않습니다.
* 온-프레미스 인증 로깅/감사 기능은 앱 암호에 사용할 수 없습니다
* 특정 고급 아키텍처 디자인은 클라이언트와 2단계 인증을 사용하는 경우 인증 위치에 따라 조직의 사용자 이름과 암호 및 앱 암호의 조합이 필요합니다. 온-프레미스 인프라에 대해 인증하는 클라이언트의 경우 조직의 사용자 이름과 암호를 사용합니다. Azure AD에 대해 인증 하는 클라이언트 hello 앱 암호를 사용 합니다.

  예를 들어 hello 다음으로 구성 된 아키텍처가 있다고 가정 합니다.

  * Azure AD를 사용하여 Active Directory의 온-프레미스 인스턴스를 페더레이션하고 있습니다
  * 온라인 Exchange를 사용하고 있습니다
  * 특별히 온-프레미스인 Lync를 사용하고 있습니다
  * Azure Multi-Factor Authentication을 사용하고 있습니다

  ![검사](./media/multi-factor-authentication-whats-next/federated.png)

  이러한 경우에 수행 해야 hello 다음:

  * 서명 하는 경우-tooLync를 사용 하 여 조직의 사용자 이름 및 암호.
  * TooExchange 온라인에 연결 하는 Outlook 클라이언트를 통해 tooaccess hello 주소록을 시도할 때 앱 암호를 사용 합니다.

### <a name="allow-app-password-creation"></a>앱 암호 만들기 허용
기본적으로 사용자가 앱 암호를 만들 수 없습니다. 이 기능을 사용하도록 설정해야 합니다. tooallow 사용자 기능 toocreate 앱 암호를 hello, 절차를 수행 하는 hello를 사용 하 여:

1. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.
2. 이 문서의 hello 시작 시 hello 지침 당 toohello MFA 서비스 설정 페이지를 이동 합니다.
3. 다음 너무 hello 라디오 단추를 선택**비 브라우저 앱에 사용자가 toocreate 앱 암호 toosign 허용**합니다.

![앱 암호 만들기](./media/multi-factor-authentication-whats-next/trustedips3.png)

### <a name="create-app-passwords"></a>앱 암호 만들기
사용자가 초기 등록을 하는 동안 앱 암호를 만들 수 있습니다. Toocreate 앱 암호 수 있게 해 주는 hello 등록 프로세스의 hello 끝에는 옵션을 제공 됩니다.

사용자 등록 후 앱 암호 hello Azure 포털 또는 hello Office 365 포털에서에서 해당 설정을 변경 하 여 만들 수도 있습니다. 사용자에 대한 자세한 내용과 세부 단계는 [Azure Multi-factor Authentication에서 앱 암호란](./end-user/multi-factor-authentication-end-user-app-passwords.md)을 참조하세요.

## <a name="remember-multi-factor-authentication-for-devices-that-users-trust"></a>사용자가 신뢰하는 장치에 대한 Multi-Factor Authentication 기억
사용자가 신뢰하는 장치 및 브라우저에 대한 Multi-Factor Authentication 기억은 모든 MFA 사용자에 대해 무료로 사용할 수 있는 기능입니다. Toogive 사용자 hello 옵션 허용 tooby 패스 MFA를 성공적으로 수행한 후 일 집합 번호에 대 한 MFA를 사용 합니다. Hello 횟수 사용자 hello에서 2 단계 인증을 수행할 수를 최소화 하 여 유용성을 향상 시킬 수 있습니다이 동일한 장치입니다.

그러나 계정 또는 장치가 손상된 경우 신뢰할 수 있는 장치의 MFA를 기억해두는 것이 보안에 도움이 될 수 있습니다. 회사 계정이 손상되거나 신뢰할 수 있는 장치를 분실 또는 도난당한 경우 [모든 장치에서 Multi-Factor Authentication을 복원](multi-factor-authentication-manage-users-and-devices.md#restore-mfa-on-all-remembered-devices-for-a-user)해야 합니다. 이 작업의 모든 장치에 신뢰할 수 있는 hello 상태를 취소 하 고 hello 사용자가 필요한 tooperform 2 단계 확인을 다시 합니다. Hello 지침이 포함 된 자신의 장치에 사용자가 toorestore MFA을 지시할 수 있습니다에 [2 단계 인증에 대 한 설정을 관리](./end-user/multi-factor-authentication-end-user-manage-settings.md#require-two-step-verification-again-on-a-device-youve-marked-as-trusted)

### <a name="how-it-works"></a>작동 방법

Multi-factor Authentication 사용자 체크 hello hello 브라우저에 영구 쿠키를 설정 하 여 작동 기억 "동안 다시 묻지 않음 **X** 일" 상자에 로그인 합니다. hello 않습니다 메시지가 MFA에 대 한 다시 해당 브라우저에서 hello 쿠키가 만료 될 때까지. Hello 사용자에서 다른 브라우저를가 경우 동일한 장치 또는 지웁니다 hello 싱크의 쿠키 증명된 tooverify 다시 됩니다. 

hello "동안 다시 묻지 않음 **X** 일" 최신 인증을 지원 하는지 여부 확인란 비 브라우저 앱에 표시 되지 않습니다. 이러한 앱에서는 1시간마다 새로운 액세스 토큰을 제공하는 새로 고침 토큰을 사용합니다. 새로 고침 토큰의 유효성을 검사 하는 경우 마지막 시간 2 단계 인증 hello Azure AD 검사 수행은 hello 구성 된 기간 (일)입니다. 

따라서 웹 앱 (일반적으로 표시 될 때마다)에서 인증 hello 수를 감소 MFA 신뢰할 수 있는 장치에 기억 하지만 증가 hello (일반적으로 메시지를 90 일 마다 반복 표시)는 최신 인증 클라이언트에 대 한 인증 수 합니다.

> [!NOTE]
>이 기능은 사용자가 Azure MFA 서버 hello 통해 AD FS에 대 한 2 단계 인증 또는 제 3 자 MFA 솔루션을 수행할 때 AD FS의 hello "로그인 유지" 기능을 통해 호환 되지 않습니다. AD FS에서 "로그인 유지"를 선택 하 고도 MFA에 대 한으로 신뢰할 수 있는 장치를 표시 하는 사용자가 하는 경우 hello "기억 MFA" 일 수가 지나면 수 tooverify 되지 합니다. Azure AD는 새로운 2 단계 인증을 요청 하지만 AD FS hello 원래 MFA 클레임 및 2 단계 확인을 다시 수행 하는 대신 날짜와 함께 토큰을 반환 합니다. 그러면 Azure AD 및 AD FS 간의 확인 루프가 해제 설정됩니다. 

### <a name="enable-remember-multi-factor-authentication"></a>Multi-Factor Authentication 기억 사용
1. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.
2. 이 문서의 hello 시작 시 hello 지침 당 toohello MFA 서비스 설정 페이지를 이동 합니다.
3. Hello 서비스 설정 페이지에서 사용자 장치 설정 관리, hello 확인 **신뢰 하는 장치에서 사용자가 tooremember 다단계 인증 허용** 상자입니다.
   ![장치 기억](./media/multi-factor-authentication-whats-next/remember.png)
4. Hello tooallow hello 신뢰할 수 있는 장치 toobypass 2 단계 인증 일 수를 설정 합니다. hello 기본값은 14 일입니다.
5. **Save**를 클릭합니다.
6. **닫기**를 클릭합니다.

### <a name="mark-a-device-as-trusted"></a>장치를 신뢰할 수 있음으로 표시

이 기능을 사용하면 사용자는 **다시 묻지 않음**을 선택하여 로그인할 때 장치를 신뢰할 수 있음으로 표시할 수 있습니다.

![다시 묻지 않음 - 스크린샷](./media/multi-factor-authentication-whats-next/trusted.png)

## <a name="selectable-verification-methods"></a>선택 가능한 확인 방법
사용자에 대해 어떤 인증 방법을 사용할지를 선택할 수 있습니다. hello 아래 표에서 각 방법에 간략하게 설명 합니다.

사용자가 MFA에 대 한 자신의 계정을 등록 하는 경우 사용 하도록 설정한 hello 옵션의 기본 설정된 확인 방법을 선택 합니다. 등록 프로세스에 대 한 hello 지침에 대해서는 [2 단계 인증에 대 한 내 계정 설정](multi-factor-authentication-end-user-first-time.md)

| 메서드 | 설명 |
|:--- |:--- |
| Toophone 호출 |자동 음성 전화를 겁니다. hello 사용자 답변 hello 호출 및 hello 전화 키패드 tooauthenticate 우물 정자 합니다. 이 전화 번호는 동기화 된 tooon 온-프레미스 Active Directory 없습니다. |
| 텍스트 메시지 toophone |확인 코드를 포함하는 문자 메시지를 보냅니다. hello 사용자는 hello 확인 코드 또는 hello 로그인 인터페이스에 tooenter hello 확인 코드 입력 정보 요청된 tooeither 회신 toohello 텍스트 메시지입니다. |
| 모바일 앱을 통한 알림 |푸시 알림 tooyour 휴대폰 이나 등록 된 장치에 보냅니다. hello 사용자 hello 알림을 보면서 선택 **확인** toocomplete 확인 합니다. <br>hello Microsoft Authenticator 앱에 사용할 수 있는 [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), 및 [IOS](http://go.microsoft.com/fwlink/?Linkid=825073)합니다. |
| 모바일 앱의 확인 코드 |hello Microsoft Authenticator 앱 30 초 마다 새 OATH 코드를 생성 합니다. hello 사용자가 hello 로그인 인터페이스에이 확인 코드를 입력 합니다.<br>hello Microsoft Authenticator 앱에 사용할 수 있는 [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), 및 [IOS](http://go.microsoft.com/fwlink/?Linkid=825073)합니다. |

### <a name="how-tooenabledisable-authentication-methods"></a>어떻게 tooenable/사용 안 함 인증 방법
1. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.
2. 이 문서의 hello 시작 시 hello 지침 당 toohello MFA 서비스 설정 페이지를 이동 합니다.
3. Hello 서비스 설정 페이지 확인 옵션 아래 선택/선택 취소할 toouse hello 옵션입니다.
   ![확인 옵션](./media/multi-factor-authentication-whats-next/authmethods.png)
4. **저장**을 클릭합니다.
5. **닫기**를 클릭합니다.

