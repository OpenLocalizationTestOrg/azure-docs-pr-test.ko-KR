---
title: "Azure MFA NPS 확장 hello에 대 한 오류 코드 aaaTroubleshoot | Microsoft Docs"
description: "일반적인 오류 메시지에 대 한 구체적인 해결 방법으로 Azure Multi-factor Authentication에 대 한 hello NPS 확장 문제 해결 도움말을 보려면"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 8b602954364c6e9f801d86edca6432bd8446c58b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-error-messages-from-hello-nps-extension-for-azure-multi-factor-authentication"></a>Azure Multi-factor Authentication에 대 한 hello NPS 확장에서에서 오류 메시지를 해결 합니다.

Azure Multi-factor Authentication에 대 한 hello NPS 확장을 사용 하 여 오류를 발생 하는 경우이 문서 tooreach 해상도 더 빠르게 사용 합니다. 

## <a name="troubleshooting-steps-for-common-errors"></a>일반적인 오류에 대한 문제 해결 단계

| 오류 코드 | 문제 해결 단계 |
| ---------- | --------------------- |
| **CONTACT_SUPPORT** | [지원에 문의](#contact-microsoft-support), hello 목록은 로그를 수집 하기 위한 단계를 알려주십시오. Hello 오류, 테 넌 트 id 및 사용자 계정 이름 (UPN)을 포함 하 여 이전에 발생 한 시간에 대 한 수 만큼 정보를 제공 합니다. |
| **CLIENT_CERT_INSTALL_ERROR** | Hello 클라이언트 인증서 설치 하거나 테 넌 트와 연결 된 방식에 문제가 있을 수 있습니다. Hello 지침에 따라 [문제 해결 hello MFA NPS 확장](multi-factor-authentication-nps-extension.md#troubleshooting) tooinvestigate 클라이언트 인증서 문제입니다. |
| **ESTS_TOKEN_ERROR** | Hello 지침에 따라 [문제 해결 hello MFA NPS 확장](multi-factor-authentication-nps-extension.md#troubleshooting) tooinvestigate 클라이언트 인증서 및 ADAL 문제 토큰입니다. |
| **HTTPS_COMMUNICATION_ERROR** | hello NPS 서버는 Azure MFA에서 없습니다 tooreceive 응답입니다. 방화벽에 대 한 트래픽 tooand https://adnotifications.windowsazure.com에서 열린 간에 양방향 한지 확인 |
| **HTTP_CONNECT_ERROR** | Hello NPS 확장을 실행 하는 hello 서버 https://adnotifications.windowsazure.com 및 https://login.microsoftonline.com/ 연결할 수 있는지를 확인 합니다. 해당 사이트가 로드되지 않으면 해당 서버의 연결 문제를 해결합니다. |
| **REGISTRY_CONFIG_ERROR** | 때문일 수 있습니다 hello 응용 프로그램에 대 한 hello 레지스트리 키가 누락 hello [PowerShell 스크립트](multi-factor-authentication-nps-extension.md#install-the-nps-extension) 설치 후 실행 되지 않았습니다. hello 오류 메시지는 hello 누락 된 키를 포함 해야 합니다. HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\AzureMfa hello 키를 갖고 있는지 확인 합니다. |
| **REQUEST_FORMAT_ERROR** <br> Radius 요청에 필수 Radius userName\Identifier 특성이 없습니다. NPS가 RADIUS 요청을 수신하는지 확인합니다. | 이 오류는 일반적으로 설치 문제를 반영합니다. NPS 확장 hello RADIUS 요청을 받을 수 있는 NPS 서버에 설치 되어야 합니다. RRAS 및 RDG와 같은 서비스에 대한 종속성으로 설치된 NPS 서버가 radius 요청을 수신하지 않습니다. Hello 인증 요청에서 hello 세부 정보를 읽을 수 없기 때문에 이러한 설치 및 아웃 오류를 통해 설치 하는 경우에 NPS 확장 작동 하지 않습니다. |
| **REQUEST_MISSING_CODE** | Hello 보조 인증 방법을 사용 하는 hello NPS와 NAS 서버 간의 hello 암호 암호화 프로토콜을 지원 하는지 확인 합니다. **PAP** hello 클라우드에서 Azure MFA의 모든 hello 인증 방법을 지원: 전화 통화, 단방향 문자 메시지, 모바일 앱 알림 및 모바일 앱 확인 코드입니다. **CHAPV2** 및 **EAP**는 전화 통화 및 모바일 앱 알림을 지원합니다. |
| **USERNAME_CANONICALIZATION_ERROR** | Hello 사용자가 온-프레미스 Active Directory 인스턴스를 사용 하 여에 존재 하 고 해당 hello NPS 서비스에 사용 권한을 tooaccess hello 디렉터리를 확인 합니다. 포리스트 간 트러스트를 사용하는 경우 [지원 서비스](#contact-microsoft-support) 추가 지원을 요청하세요. |


   

### <a name="alternate-login-id-errors"></a>대체 로그인 ID 오류

| 오류 코드 | 오류 메시지 | 문제 해결 단계 |
| ---------- | ------------- | --------------------- |
| **ALTERNATE_LOGIN_ID_ERROR** | 오류: userObjectSid 조회 실패 | 온-프레미스 Active Directory 인스턴스에서 해당 hello 사용자의 존재를 확인 합니다. 포리스트 간 트러스트를 사용하는 경우 [지원 서비스](#contact-microsoft-support) 추가 지원을 요청하세요. |
| **ALTERNATE_LOGIN_ID_ERROR** | 오류: 대체 LoginId 조회 실패 | LDAP_ALTERNATE_LOGINID_ATTRIBUTE tooa 설정 되어 있는지 확인 [유효한 active directory 특성](https://msdn.microsoft.com/library/ms675090(v=vs.85).aspx)합니다. <br><br> LDAP_LOOKUP_FORESTS 비어 있지 않은 값으로 지정 된 또는 LDAP_FORCE_GLOBAL_CATALOG tooTrue, 설정, 글로벌 카탈로그를 구성한 경우를 해당 hello AlternateLoginId 특성은 tooit 추가 확인 합니다. <br><br> LDAP_LOOKUP_FORESTS을 비어 있지 않은 값으로 구성 된 경우 hello 값이 올바른지 확인 합니다. 둘 이상의 포리스트 이름 이면 hello 이름은 공백 없이 세미콜론으로 구분 되어야 합니다. <br><br> 이러한 단계는 hello 문제를 해결 하지 않는 경우 [지원에 문의](#contact-microsoft-support) 도움이 더 필요 합니다. |
| **ALTERNATE_LOGIN_ID_ERROR** | 오류: 대체 LoginId 값이 비어 있음 | 해당 hello AlternateLoginId 특성 hello 사용자에 대해 구성 되었는지 확인 합니다. |


## <a name="errors-your-users-may-encounter"></a>사용자에게 발생할 수 있는 오류

| 오류 코드 | 오류 메시지 | 문제 해결 단계 |
| ---------- | ------------- | --------------------- |
| **AccessDenied** | 호출자에 게 테 넌 트 hello 사용자에 대 한 액세스 권한을 toodo 인증이 없습니다. | 여부 hello 테 넌 트 도메인과 hello 사용자 계정 이름 (UPN)의 hello 도메인은 hello 동일 확인 합니다. 예를 들어 있는지 확인 하는 user@contoso.com tooauthenticate toohello Contoso 테 넌 트를 시도 합니다. UPN hello Azure의 hello 테 넌 트에 대 한 유효한 사용자를 나타냅니다. |
| **AuthenticationMethodNotConfigured** | hello 지정 hello 사용자에 대 한 인증 방법 구성 되지 않았습니다. | 추가 하거나 toohello 지침에 따라 자신의 인증 방법을 확인 하는 hello 사용자에 게 [2 단계 인증에 대 한 설정을 관리](./end-user/multi-factor-authentication-end-user-manage-settings.md)합니다. |
| **AuthenticationMethodNotSupported** | 지정된 인증 방법이 지원되지 않습니다. | 이 오류를 포함하는 모든 로그를 수집하고 [지원 서비스에 문의](#contact-microsoft-support)합니다. 에 지원을 문의할 때 hello 사용자 이름 및 hello 오류를 발생 시킨 hello 보조 확인 메서드를 제공 합니다. |
| **BecAccessDenied** | 아마도 hello username hello 테 넌 트에 정의 되지 않은 경우, MSODS Bec 호출 반환 액세스가 거부 되었습니다. | hello 사용자는 Active Directory 온-프레미스에 있지만 Azure AD에서 AD Connect로 동기화 되지 않은 합니다. 또는 hello 사용자가 hello 테 넌 트에 없습니다. Hello 사용자 tooAzure AD를 추가 하 고 toohello 지침에 따라 자신의 확인 방법을 추가 [2 단계 인증에 대 한 설정을 관리](./end-user/multi-factor-authentication-end-user-manage-settings.md)합니다. |
| **InvalidFormat** 또는 **StrongAuthenticationServiceInvalidParameter** | hello 전화 번호 형식이 인식할 수 없는 서식 | Hello 사용자가 인증 전화 번호를 수정 하도록 합니다. |
| **InvalidSession** | hello는 세션이 유효 하지 않거나 만료 된 경우 지정 된 | hello 세션 3 분 toocomplete 이상 수행 했습니다. 해당 hello 사용자가 hello 확인 코드를 입력 하거나 hello 인증 요청을 시작 후 3 분 안에 toohello 앱 알림에 응답을 확인 합니다. Hello 문제를 해결 하지 못하면 하는 클라이언트, NAS 서버, NPS 서버 hello Azure MFA 끝점 사이의 네트워크 대기 시간은 없습니다 지 확인 합니다.  |
| **NoDefaultAuthenticationMethodIsConfigured** | 기본 인증 방법은 hello 사용자에 대해 구성 된 | 추가 하거나 toohello 지침에 따라 자신의 인증 방법을 확인 하는 hello 사용자에 게 [2 단계 인증에 대 한 설정을 관리](./end-user/multi-factor-authentication-end-user-manage-settings.md)합니다. 해당 hello 사용자가 기본 인증 방법 선택 하 고 구성 자신의 계정에 대 한 해당 메서드를 확인 합니다. |
| **OathCodePinIncorrect** | 잘못된 코드 및 PIN을 입력했습니다. | 이 오류는 hello NPS 확장에에서 필요 하지 않습니다. 이 오류가 발생하는 경우 [지원 서비스](#contact-microsoft-support)에서 문제 해결을 위한 지원을 받습니다. |
| **ProofDataNotFound** | 지정 된 hello에 대 한 증명 데이터 구성 되지 않았습니다. 인증 방법입니다. | 다른 본인 확인 방법을 시도 또는 toohello 지침에 따라 새 확인 방법을 추가 hello 사용자에 게 [2 단계 인증에 대 한 설정을 관리](./end-user/multi-factor-authentication-end-user-manage-settings.md)합니다. Hello 계속 하면이 오류는 확인 방법을 올바르게 설정 되어 있는지 확인 하는 toosee 경우 [지원에 문의](#contact-microsoft-support)합니다. |
| **SMSAuthFailedWrongCodePinEntered** | 잘못된 코드 및 PIN을 입력했습니다. (OneWaySMS) | 이 오류는 hello NPS 확장에에서 필요 하지 않습니다. 이 오류가 발생하는 경우 [지원 서비스](#contact-microsoft-support)에서 문제 해결을 위한 지원을 받습니다. |
| **TenantIsBlocked** | 테넌트가 차단되었습니다. | [지원에 문의](#contact-microsoft-support) hello Azure 포털의에서 속성 페이지 hello Azure AD에서에서 디렉터리 ID를 가진 합니다. |
| **UserNotFound** | hello 지정 된 사용자를 찾을 수 없습니다. | hello 테 넌 트를 더 이상 Azure AD에서 활성으로 표시 합니다. 확인 된 구독을 활성화 했다가 hello 있는 첫 번째 파티 앱 필요 합니다. 또한 hello 인증서가 여전히 유효 하 고 hello 서비스 사용자에서 등록 및 hello 인증서 주체에 테 넌 트 hello 예상 대로 되어 있는지 확인 합니다. |

## <a name="messages-your-users-may-encounter-that-arent-errors"></a>사용자에게 표시될 수 있는 오류가 아닌 메시지

경우에 따라 인증 요청이 실패했기 때문에 Multi-Factor Authentication에서 메시지가 표시될 수 있습니다. 이러한 구성의 hello 제품에 오류가 아니지만 의도적인 경고 설명 하는 이유는 인증 요청은 거부 되었습니다.

| 오류 코드 | 오류 메시지 | 권장되는 단계 | 
| ---------- | ------------- | ----------------- |
| **OathCodeIncorrect** | 잘못된 코드를 입력했거나 OATH 코드가 올바르지 않습니다. | 오류가 아닙니다. 사용자가 잘못된 코드를 입력했습니다. | hello 사용자 hello 잘못 된 코드를 입력 합니다. 새 코드를 요청하거나 다시 로그인하여 다시 시도하도록 합니다. | 
| **SMSAuthFailedMaxAllowedCodeRetryReached** | 허용되는 최대 코드 다시 시도 횟수에 도달했습니다. | hello 사용자 너무 여러 번 hello 확인 시도를 실패 했습니다. 설정에 따라 이제 관리자가 차단 해제 toobe를 할 수 있습니다.  |
| **SMSAuthFailedWrongCodeEntered** | 잘못된 코드를 입력했거나 텍스트 메시지 OTP가 올바르지 않습니다. | hello 사용자 hello 잘못 된 코드를 입력 합니다. 새 코드를 요청하거나 다시 로그인하여 다시 시도하도록 합니다. |

## <a name="errors-that-require-support"></a>지원이 필요한 오류

이러한 오류 중 하나가 발생하면 [지원 서비스에 문의](#contact-microsoft-support)하여 진단 도움을 받는 것이 좋습니다. 이러한 오류를 해결할 수 있는 표준 단계는 없습니다. 지원에 연락할 수행 하는 경우에 최대한 tooan 오류를 발생 시킨 hello 단계에 대 한 많은 정보 및 테 넌 트 정보로 있는지 tooinclude 수 있습니다.

| 오류 코드 | 오류 메시지 |
| ---------- | ------------- |
| **InvalidParameter** | 요청은 null이 아니어야 합니다. |
| **InvalidParameter** | ReplicationScope:{0}의 경우 ObjectId는 null 또는 공백이 아니어야 합니다 |
| **InvalidParameter** | CompanyName 길이의 hello \{0} \ hello 최대 허용된 길이 {1 \} 보다 길면 |
| **InvalidParameter** | UserPrincipalName은 null 또는 공백이 아니어야 합니다. |
| **InvalidParameter** | hello 제공 TenantId가 올바른 형식이 아닙니다. |
| **InvalidParameter** | SessionId는 null 또는 공백이 아니어야 합니다. |
| **InvalidParameter** | 요청 또는 Msod에서 ProofData를 확인할 수 없습니다. 알 수 없는 hello ProofData입니다. |
| **InternalError** |  |
| **OathCodePinIncorrect** |  |
| **VersionNotSupported** |  |
| **MFAPinNotSetup** |  |

## <a name="next-steps"></a>다음 단계

### <a name="troubleshoot-user-accounts"></a>사용자 계정 문제 해결

사용자에게 [2단계 인증 문제가 발생하면](./end-user/multi-factor-authentication-end-user-troubleshoot.md) 문제를 자체 진단하도록 도와주세요. 

### <a name="contact-microsoft-support"></a>Microsoft 지원에 문의

추가 지원이 필요한 경우 [Azure Multi-Factor Authentication 서버 지원](https://support.microsoft.com/oas/default.aspx?prid=14947)을 통해 지원 전문가에게 문의하세요. 문의하는 경우 가능한 문제에 대한 많은 정보를 제공해주시면 도움이 됩니다. 정보를 제공할 수 있습니다는 hello 오류를 보여 준다는 사실을 알았습니다 및 디버그 로그는 hello 사용자의 특정 오류 코드를 hello 특정 세션 ID hello ID hello hello 오류를 언급 했 듯이 여기서 hello 페이지를 포함 됩니다.

toocollect 디버그 로그 지원 진단에 대 한 단계를 수행 하는 hello를 사용 합니다. 

1. 관리자 명령 프롬프트를 열고 다음 명령을 실행합니다.

   ```
   Mkdir c:\NPS
   Cd NPS
   netsh trace start Scenario=NetConnection capture=yes tracefile=c:\NPS\nettrace.etl
   logman create trace "NPSExtension" -ow -o c:\NPS\NPSExtension.etl -p {7237ED00-E119-430B-AB0F-C63360C8EE81} 0xffffffffffffffff 0xff -nb 16 16 -bs 1024 -mode Circular -f bincirc -max 4096 -ets
   logman update trace "NPSExtension" -p {EC2E6D3A-C958-4C76-8EA4-0262520886FF} 0xffffffffffffffff 0xff -ets
   ```

2. Hello 문제를 재현

3. 이러한 명령 사용 하 여 hello 추적을 중지 합니다.

   ```
   logman stop "NPSExtension" -ets
   netsh trace stop
   wevtutil epl AuthNOptCh C:\NPS\%computername%_AuthNOptCh.evtx
   wevtutil epl AuthZOptCh C:\NPS\%computername%_AuthZOptCh.evtx
   wevtutil epl AuthZAdminCh C:\NPS\%computername%_AuthZAdminCh.evtx
   Start .
   ```

4. Hello C:\NPS 폴더의 내용을 hello zip 압축 hello 파일 toohello 지원 케이스를 연결 합니다.


