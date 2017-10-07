---
title: "Azure AD Connect: 연결 문제 해결 | Microsoft Docs"
description: "Azure AD Connect와 tootroubleshoot 연결을 발급 하는 방법에 대해 설명 합니다."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 3aa41bb5-6fcb-49da-9747-e7a3bd780e64
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 60d6b7c4ad8a3ab907c20e598ec9443f115df287
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-connectivity-issues-with-azure-ad-connect"></a>Azure AD Connect 연결 문제 해결
이 문서는 Azure AD Connect와 Azure AD 간의 연결의 작동 방식 및 어떻게 tootroubleshoot 연결 문제를 설명 합니다. 이러한 문제는 가능성이 가장 높은 toobe 프록시 서버는 환경에서 표시 합니다.

## <a name="troubleshoot-connectivity-issues-in-hello-installation-wizard"></a>Hello 설치 마법사에 대 한 연결 문제 해결
Azure AD Connect 인증에 대 한 최신 인증 (hello ADAL 라이브러리를 사용 하 여) 사용 합니다. hello 설치 마법사 및 적절 한 hello 동기화 엔진이 machine.config toobe 이러한 두 열은.NET 응용 프로그램 때문에 제대로 구성 해야 합니다.

이 문서에서는 Fabrikam tooAzure AD 해당 프록시를 통해 연결 하는 방법을 보여 줍니다. 프록시 서버 hello fabrikamproxy 이름이 고 포트 8080을 사용 하는 합니다.

먼저 다음 해야 toomake 있는지 [ **machine.config** ](active-directory-aadconnect-prerequisites.md#connectivity) 올바르게 구성 되어 있습니다.  
![machineconfig](./media/active-directory-aadconnect-troubleshoot-connectivity/machineconfig.png)

> [!NOTE]
> 일부 타사 블로그에서 것는 변경 내용이 toomiiserver.exe.config 대신 있는지 설명 합니다. 그러나이 파일은 초기 설치 중 맞으면 hello와 시스템 간에 첫 번째 업그레이드에도 모든 업그레이드에 덮어씁니다. 이런 이유로 hello 좋습니다 tooupdate machine.config 대신.
>
>

hello 프록시 서버가 필요한 hello Url 열려 있어야 합니다. hello 공식 목록에 설명 되어 [Office 365 Url 및 IP 주소 범위](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)합니다.

이러한 Url의 다음 표에 hello 전혀 hello 절대 완전 최소 toobe 수 tooconnect tooAzure AD 않습니다. 이 목록은 비밀번호 쓰기 저장 또는 Azure AD Connect Health와 같은 선택적 기능은 포함하지 않습니다. 것 문서화 여기 toohelp hello 초기 구성에 대 한 문제를 해결 합니다.

| URL | 포트 | 설명 |
| --- | --- | --- |
| mscrl.microsoft.com |HTTP/80 |사용 되는 toodownload CRL을 나열합니다. |
| \*.verisign.com |HTTP/80 |사용 되는 toodownload CRL을 나열합니다. |
| \*.entrust.com |HTTP/80 |사용 되는 toodownload CRL MFA에 대해 나열합니다. |
| \*.windows.net |HTTPS/443 |TooAzure AD에서에서 사용 되는 toosign 합니다. |
| secure.aadcdn.microsoftonline-p.com |HTTPS/443 |MFA에 사용됩니다. |
| \*.microsoftonline.com |HTTPS/443 |Azure AD 디렉터리와 가져오기/내보내기 데이터 tooconfigure를 사용 합니다. |

## <a name="errors-in-hello-wizard"></a>Hello 마법사의 오류
hello 설치 마법사는 두 가지 서로 다른 보안 컨텍스트를 사용 합니다. Hello 페이지 **tooAzure AD 연결**, 현재 로그인 한 사용자 hello를 사용 합니다. Hello 페이지 **구성**, toohello를 변경 [hello 동기화 엔진에 대 한 hello 서비스 실행 계정](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account)합니다. Hello에 주로 나타납니다는 문제가 있는 경우 **tooAzure AD 연결** hello 프록시 구성을 전역 이므로 hello 마법사의 페이지입니다.

될 hello는 hello 설치 마법사에서 발생 하는 hello 가장 일반적인 오류입니다.

### <a name="hello-installation-wizard-has-not-been-correctly-configured"></a>설치 마법사 hello 올바르게 구성 되지 않았습니다.
이 오류는 hello 마법사 자체 hello 프록시를 연결할 수 없는 경우에 나타납니다.  
![nomachineconfig](./media/active-directory-aadconnect-troubleshoot-connectivity/nomachineconfig.png)

* 이 오류를 표시 하는 경우 확인 hello [machine.config](active-directory-aadconnect-prerequisites.md#connectivity) 올바르게 구성 되어 있습니다.
* 올바른를 검색 하는 경우 hello 단계에 따라 [프록시 연결을 확인](#verify-proxy-connectivity) toosee hello 마법사도 외부 hello 문제가 있는 경우.

### <a name="a-microsoft-account-is-used"></a>Microsoft 계정이 사용됨
**학교 또는 조직 계정**이 아닌 **Microsoft 계정**을 사용하면 일반 오류가 발생합니다.  
![Microsoft 계정이 사용됨](./media/active-directory-aadconnect-troubleshoot-connectivity/unknownerror.png)

### <a name="hello-mfa-endpoint-cannot-be-reached"></a>hello MFA 끝점에 연결할 수 없습니다.
이 오류가 나타나면 경우 hello 끝점 **https://secure.aadcdn.microsoftonline-p.com** 에 연결할 수 없습니다 전역 관리자가 MFA를 사용 하도록 설정 하 고 있습니다.  
![nomachineconfig](./media/active-directory-aadconnect-troubleshoot-connectivity/nomicrosoftonlinep.png)

* 이 오류를 표시 하는 경우 해당 hello 끝점 확인 **secure.aadcdn.microsoftonline p.com** toohello 프록시 추가 되었습니다.

### <a name="hello-password-cannot-be-verified"></a>hello 암호를 확인할 수 없습니다.
이 오류가 나타나는 hello 설치 마법사는 광고를 tooAzure 있지만 hello 암호 자체 연결에 성공 하는 경우를 확인할 수 없습니다.  
![badpassword](./media/active-directory-aadconnect-troubleshoot-connectivity/badpassword.png)

* Hello 암호는 임시 암호 이며 변경 해야? 올바른 암호를 실제로 hello 인가요? 다른 컴퓨터에 Azure AD Connect 서버 hello 보다 toohttps://login.microsoftonline.com에서 toosign 시도 하 고 사용할 수 있는 hello 계정 확인 합니다.

### <a name="verify-proxy-connectivity"></a>프록시 연결 확인
tooverify hello Azure AD Connect 서버에 실제 hello 프록시 및 인터넷에 연결 하는 경우 사용 하 여 몇 가지 PowerShell toosee hello 프록시 허용 하는 웹 요청 여부. PowerShell 프롬프트에서 `Invoke-WebRequest -Uri https://adminwebservice.microsoftonline.com/ProvisioningService.svc`를 실행합니다. (기술적으로 hello 첫 번째 호출은 toohttps://login.microsoftonline.com와이 URI도 작동 하지만 hello 다른 URI는 더 빠른 toorespond.)

PowerShell에서 machine.config toocontact hello 프록시 hello 구성을 사용합니다. netsh winhttp/hello 설정에는 이러한 cmdlet 영향을 주지 않아야 합니다.

성공 상태 얻어야 hello 프록시 올바르게 구성 하는 경우: ![proxy200](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequest200.png)

표시 되 면 **없습니다 tooconnect toohello 원격 서버**, 다음 PowerShell hello 프록시를 사용 하지 않고 직접 호출 toomake 시도 또는 DNS가 올바르게 구성 되지 않습니다. 있는지 hello 확인 **machine.config** 파일이 올바르게 구성 되어 있습니다.
![unabletoconnect](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequestunable.png)

Hello 프록시 올바르게 구성 되지 않은 경우 오류가 발생: ![proxy200](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequest403.png)
![proxy407](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequest407.png)

| 오류 | 오류 텍스트 | 주석 |
| --- | --- | --- |
| 403 |사용할 수 없음 |hello 프록시가 아직 열려 있지 hello 요청 된 URL에 대 한 합니다. Hello 프록시 구성을 다시 방문 하 고 있는지 hello [Url](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2) 열려 있습니다. |
| 407 |프록시 인증 필요 |hello 프록시 서버에 로그인 하는 데 필요 하 고 제공 되지 않았습니다. 프록시 서버에 인증이 필요한 경우 있는지 toohave hello machine.config에 구성 된이 설정을 확인 합니다. 또한 hello 서비스 계정 및 hello 마법사를 실행 하는 hello 사용자에 대 한 도메인 계정을 사용 하 고 있는지 확인 합니다. |

## <a name="hello-communication-pattern-between-azure-ad-connect-and-azure-ad"></a>Azure AD Connect와 Azure AD 간의 hello 통신 패턴
위의 모든 단계를 수행했는데도 여전히 연결할 수 없다면 이제 네트워크 로그를 살펴봅니다. 이 섹션에는 일반적이고 성공적인 연결 패턴이 나와 있습니다. Hello 네트워크 로그를 읽을 때 무시할 수 있는 일반적인 빨간색 herrings는 목록도 됩니다.

* 호출 toohttps://dc.services.visualstudio.com이 있습니다. 필요한 toohave hello 설치 toosucceed 및 이러한 호출에 대 한 hello 프록시에 열려이 URL을 무시할 수는 없습니다.
* Dns 확인 hello DNS 이름 공간 nsatc.net 및 microsoftonline.com에 포함 되지 않은 다른 네임 스페이스의 실제 호스트 toobe hello를 나열 하는 것이 표시 됩니다. 그러나 hello 실제 서버 이름에 모든 웹 서비스 요청 하지는 않으며 이러한 Url toohello 프록시 tooadd를 갖지.
* hello 끝점 adminwebservice 및 provisioningapi 검색 끝점에는 toofind hello 실제 끝점 toouse를 사용 합니다. 이러한 끝점은 사용자의 하위 지역에 따라 다릅니다.

### <a name="reference-proxy-logs"></a>참조 프록시 로그
덤프 다음과 같습니다 (중복 항목 toohello 제거 된 동일한 끝점)는 실제 프록시 로그 및 hello 설치 마법사 페이지에서 어디에서 찍은 합니다. 이 섹션은 고유한 프록시 및 네트워크 로그에 대한 참조로 사용할 수 있습니다. 실제 끝점 hello 사용자 환경에서 다를 수 있습니다 (특히 해당 Url에서 *기울임꼴*).

**TooAzure AD 연결**

| Time | URL |
| --- | --- |
| 1/11/2016 8:31 |connect://login.microsoftonline.com:443 |
| 1/11/2016 8:31 |connect://adminwebservice.microsoftonline.com:443 |
| 1/11/2016 8:32 |connect://*bba800-anchor*.microsoftonline.com:443 |
| 1/11/2016 8:32 |connect://login.microsoftonline.com:443 |
| 1/11/2016 8:33 |connect://provisioningapi.microsoftonline.com:443 |
| 1/11/2016 8:33 |connect://*bwsc02-relay*.microsoftonline.com:443 |

**구성**

| Time | URL |
| --- | --- |
| 1/11/2016 8:43 |connect://login.microsoftonline.com:443 |
| 1/11/2016 8:43 |connect://*bba800-anchor*.microsoftonline.com:443 |
| 1/11/2016 8:43 |connect://login.microsoftonline.com:443 |
| 1/11/2016 8:44 |connect://adminwebservice.microsoftonline.com:443 |
| 1/11/2016 8:44 |connect://*bba900-anchor*.microsoftonline.com:443 |
| 1/11/2016 8:44 |connect://login.microsoftonline.com:443 |
| 1/11/2016 8:44 |connect://adminwebservice.microsoftonline.com:443 |
| 1/11/2016 8:44 |connect://*bba800-anchor*.microsoftonline.com:443 |
| 1/11/2016 8:44 |connect://login.microsoftonline.com:443 |
| 1/11/2016 8:46 |connect://provisioningapi.microsoftonline.com:443 |
| 1/11/2016 8:46 |connect://*bwsc02-relay*.microsoftonline.com:443 |

**초기 동기화**

| Time | URL |
| --- | --- |
| 1/11/2016 8:48 |connect://login.windows.net:443 |
| 1/11/2016 8:49 |connect://adminwebservice.microsoftonline.com:443 |
| 1/11/2016 8:49 |connect://*bba900-anchor*.microsoftonline.com:443 |
| 1/11/2016 8:49 |connect://*bba800-anchor*.microsoftonline.com:443 |

## <a name="authentication-errors"></a>인증 오류
이 섹션에서는 ADAL (Azure AD Connect에서 사용 되는 hello 인증 라이브러리) 및 PowerShell에서 반환 될 수 있는 오류를 설명 합니다. hello 오류 설명에 다음 단계를 이해 하는 데 도움이 됩니다.

### <a name="invalid-grant"></a>잘못된 권한 부여
잘못된 사용자 이름 또는 암호 자세한 내용은 참조 [hello 암호를 확인할 수 없는](#the-password-cannot-be-verified)합니다.

### <a name="unknown-user-type"></a>알 수 없는 사용자 유형
Azure AD 디렉터리를 찾거나 해결할 수 없습니다. 확인 되지 않은 도메인의 사용자 이름 가진 toologin 시키면 미정?

### <a name="user-realm-discovery-failed"></a>사용자 영역 검색에 실패했습니다
네트워크 또는 프록시 구성 문제 hello 네트워크에 연결할 수 없습니다. 참조 [hello 설치 마법사에 대 한 연결 문제를 해결](#troubleshoot-connectivity-issues-in-the-installation-wizard)합니다.

### <a name="user-password-expired"></a>사용자 암호가 만료되었습니다
자격 증명이 만료되었습니다. 암호를 변경합니다.

### <a name="authorizationfailure"></a>AuthorizationFailure
알 수 없는 문제

### <a name="authentication-cancelled"></a>인증이 취소되었습니다
hello multi-factor authentication (MFA) 챌린지를 취소 했습니다.

### <a name="connecttomsonline"></a>ConnectToMSOnline
인증에 성공했지만 Azure AD PowerShell에 인증 문제가 있습니다.

### <a name="azurerolemissing"></a>AzureRoleMissing
인증이 성공했습니다. 전역 관리자가 아닙니다.

### <a name="privilegedidentitymanagement"></a>PrivilegedIdentityManagement
인증이 성공했습니다. Privileged Identity Management를 사용하며 현재 전역 관리자가 아닙니다. 자세한 내용은 [Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md)를 참조하세요.

### <a name="companyinfounavailable"></a>CompanyInfoUnavailable
인증이 성공했습니다. Azure AD에서 회사 정보를 검색할 수 없습니다.

### <a name="retrievedomains"></a>RetrieveDomains
인증이 성공했습니다. Azure AD에서 도메인 정보를 검색할 수 없습니다.

### <a name="unexpected-exception"></a>예기치 않은 예외
Hello 설치 마법사에 예기치 않은 오류가 표시 되 고 Toouse를 시도 하는 경우에 발생할 수 있습니다는 **Microsoft 계정** 아닌 **학교 또는 조직 계정**합니다.

## <a name="troubleshooting-steps-for-previous-releases"></a>이전 릴리스에 대한 문제 해결 단계입니다.
릴리스와의 빌드 번호 1.1.105.0 (2016 년 2 월에 릴리스된)로 시작 hello 로그인 도우미 사용이 중지 되었습니다. 이 섹션 및 hello 구성 해야 더 이상 필요할 수 있지만, 참조로 유지 됩니다.

Hello 단일-로그인 도우미 toowork, winhttp은 구성 해야 합니다. 이 구성은 [**netsh**](active-directory-aadconnect-prerequisites.md#connectivity)를 사용하여 수행할 수 있습니다.  
![netsh](./media/active-directory-aadconnect-troubleshoot-connectivity/netsh.png)

### <a name="hello-sign-in-assistant-has-not-been-correctly-configured"></a>hello 로그인 도우미 올바르게 구성 되지 않았습니다.
이 오류는 hello 로그인 도우미 hello 프록시에 연결할 수 없습니다 또는 hello 프록시 hello 요청 수 없는 경우 나타납니다.
![nonetsh](./media/active-directory-aadconnect-troubleshoot-connectivity/nonetsh.png)

* 이 오류를 표시 하는 경우에 hello 프록시 구성을 확인 [netsh](active-directory-aadconnect-prerequisites.md#connectivity) 올바른지 확인 합니다.
  ![netshshow](./media/active-directory-aadconnect-troubleshoot-connectivity/netshshow.png)
* 올바른를 검색 하는 경우 hello 단계에 따라 [프록시 연결을 확인](#verify-proxy-connectivity) toosee hello 마법사도 외부 hello 문제가 있는 경우.

## <a name="next-steps"></a>다음 단계
[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.
