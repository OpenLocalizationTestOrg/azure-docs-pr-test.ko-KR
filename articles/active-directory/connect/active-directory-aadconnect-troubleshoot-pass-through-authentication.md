---
title: "Azure AD Connect: 통과 인증 문제 해결 | Microsoft 문서"
description: "이 문서에서는 설명 방법을 tootroubleshoot Azure Active Directory (Azure AD) 통과 인증 합니다."
services: active-directory
keywords: "Azure AD Connect 통과 인증 문제 해결, Active Directory 설치, Azure AD에 필요한 구성 요소, SSO, Single Sign-on"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 87130952f660762f91b0a34b05287603b565639f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-active-directory-pass-through-authentication"></a>Azure Active Directory 통과 인증 문제 해결

이 문서에서는 Azure AD 통과 인증과 관련된 일반적인 문제에 대한 문제 해결 정보를 찾을 수 있습니다.

>[!IMPORTANT]
>통과 인증으로 사용자 로그인 문제에 직면 하, 경우 hello 기능을 사용 하지 않도록 설정 하거나 클라우드 전용 전역 관리자 계정 toofall 다시 필요 없이 통과 인증 에이전트를 제거 하지 마십시오. [클라우드 전용 전역 관리자 계정 추가](../active-directory-users-create-azure-portal.md)에 대해 자세히 알아봅니다. 이 단계를 수행하는 것이 중요하며 테넌트가 잠기지 않도록 합니다.

## <a name="general-issues"></a>일반적인 문제

### <a name="check-status-of-hello-feature-and-authentication-agents"></a>Hello 기능 및 인증 에이전트의 상태 확인

해당 hello 통과 인증 기능은 아직 확인 **Enabled** 인증 에이전트의 테 넌 트 및 hello 상태를 보여 줍니다. **활성**, 아닌 **비활성**합니다. Toohello 이동 하 여 상태를 확인할 수 있습니다 **Azure AD Connect** hello에 블레이드 [Azure Active Directory 관리 센터](https://aad.portal.azure.com/)합니다.

![Azure Active Directory 관리 센터 - Azure AD Connect 블레이드](./media/active-directory-aadconnect-pass-through-authentication/pta7.png)

![Azure Active Directory 관리 센터 - 통과 인증 블레이드](./media/active-directory-aadconnect-pass-through-authentication/pta11.png)

### <a name="user-facing-sign-in-error-messages"></a>사용자 관련 로그인 오류 메시지

Hello 사용자가 없습니다 toosign 통과 인증을 사용 하 여, hello hello Azure AD 로그인 화면에 다음 사용자 용 오류 중 하나가 표시 될 수 있습니다. 

|오류|설명|해결 방법
| --- | --- | ---
|AADSTS80001|없습니다 tooconnect tooActive 디렉터리|에이전트 서버는 해당 암호가 필요 toobe 유효성을 검사 하는 hello 사용자로 hello 동일한 AD 포리스트의 구성원 수 tooconnect tooActive 디렉터리 되어 있는지 확인 합니다.  
|AADSTS8002|시간 초과가 발생 연결 tooActive 디렉터리|Tooensure Active Directory를 사용할 수 및 toorequests hello 에이전트 로부터 응답을 확인 합니다.
|AADSTS80004|toohello 에이전트 전달 hello 사용자 이름이 잘못 되었습니다.|Hello 사용자가 올바른 사용자 hello 사용 하 여 toosign 시도 확인 합니다.
|AADSTS80005|유효성 검사 중 예측할 수 없는 WebException 발생|일시적인 오류입니다. Hello 요청을 다시 시도 합니다. Toofail 계속 하는 경우 Microsoft 지원에 문의 합니다.
|AADSTS80007|Active Directory와 통신 중 오류 발생|자세한 내용은 hello 에이전트 로그를 확인 하 고 Active Directory가 예상 대로 작동 하는지 확인 합니다.

### <a name="sign-in-failure-reasons-on-hello-azure-active-directory-admin-center"></a>Hello Azure Active Directory 관리 센터에 로그인 실패 이유

Hello 확인 하 여 사용자 로그인 관련 문제를 해결 [로그인 활동 보고서](../active-directory-reporting-activity-sign-ins.md) hello에 [Azure Active Directory 관리 센터](https://aad.portal.azure.com/)합니다.

![Azure Active Directory 관리 센터 - 로그인 보고서](./media/active-directory-aadconnect-pass-through-authentication/pta4.png)

너무 이동**Azure Active Directory** -> **로그인** hello에 [Azure Active Directory 관리 센터](https://aad.portal.azure.com/) 특정 사용자의 로그인 활동을 클릭 합니다. Hello에 대 한 확인 **로그인 오류 코드** 필드입니다. 해당 필드 tooa 실패 이유 및 다음 표에 hello를 사용 하는 확인의 hello 값을 매핑하십시오.

|로그인 오류 코드|로그인 실패 이유|해결 방법
| --- | --- | ---
| 50144 | 사용자의 Active Directory 암호가 만료되었습니다. | 온-프레미스 Active Directory에서 hello 사용자의 암호를 다시 설정 합니다.
| 80001 | 사용할 수 있는 인증 에이전트가 없습니다. | 인증 에이전트를 설치하고 등록합니다.
| 80002 | 인증 에이전트의 암호 유효성 검사 요청 시간이 초과되었습니다. | Active Directory hello 인증 에이전트에서에서 연결할 수 있는지 확인 하십시오.
| 80003 | 인증 에이전트에서 받은 응답이 잘못되었습니다. | 여러 사용자 간에 일관 되 게 재현할 수 있는 hello 문제가 발생 하면 Active Directory 구성을 확인 합니다.
| 80004 | 로그인 요청에 잘못된 UPN(사용자 계정 이름)이 사용되었습니다. | 올바른 사용자 이름 hello 사용 하 여 hello 사용자 toosign를 요청 합니다.
| 80005 | 인증 에이전트: 오류가 발생했습니다. | 일시적인 오류입니다. 나중에 다시 시도하십시오.
| 80007 | 인증 에이전트 수 없습니다 tooconnect tooActive 디렉터리입니다. | Active Directory hello 인증 에이전트에서에서 연결할 수 있는지 확인 하십시오.
| 80010 | 인증 에이전트 수 없습니다 toodecrypt 암호입니다. | Hello 문제는 일관 되 게 재현할 수 있는 경우 설치 하 고 새 인증 에이전트에 등록 합니다. 및 현재 hello를 제거 합니다. 
| 80011 | 인증 에이전트 수 없습니다 tooretrieve 암호 해독 키입니다. | Hello 문제는 일관 되 게 재현할 수 있는 경우 설치 하 고 새 인증 에이전트에 등록 합니다. 및 현재 hello를 제거 합니다.

## <a name="authentication-agent-installation-issues"></a>인증 에이전트 설치 문제

### <a name="an-unexpected-error-occurred"></a>예기치 않은 오류가 발생함

[에이전트 로그를 수집](#collecting-pass-through-authentication-agent-logs) hello 서버 및 해당 문제에 대해 Microsoft 지원에 문의 하십시오.

## <a name="authentication-agent-registration-issues"></a>인증 에이전트 등록 문제

### <a name="registration-of-hello-authentication-agent-failed-due-tooblocked-ports"></a>Tooblocked 포트 인해 hello 인증 에이전트를 등록 하지 못했습니다.

어떤 hello에 인증 에이전트 설치가 완료 된 후 해당 hello 서버 Url 및 포트에 나열 된 서비스와 통신할 수 확인 [여기](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-1-check-prerequisites)합니다.

### <a name="registration-of-hello-authentication-agent-failed-due-tootoken-or-account-authorization-errors"></a>권한 부여 오류 tootoken 또는 계정 인해 hello 인증 에이전트를 등록 하지 못했습니다.

모든 Azure AD Connect 또는 독립 실행형 인증 에이전트 설치 및 등록 작업에는 클라우드 전용 전역 관리자 계정을 사용해야 합니다. MFA 활성화 전역 관리자 계정, 알려진된 문제는 해결 방법으로 MFA 일시적으로 (만 toocomplete hello 작업)를 해제 합니다.

### <a name="an-unexpected-error-occurred"></a>예기치 않은 오류가 발생함

[에이전트 로그를 수집](#collecting-pass-through-authentication-agent-logs) hello 서버 및 해당 문제에 대해 Microsoft 지원에 문의 하십시오.

## <a name="authentication-agent-uninstallation-issues"></a>인증 에이전트 제거 문제

### <a name="warning-message-when-uninstalling-azure-ad-connect"></a>Azure AD Connect 제거 시 나타나는 경고 메시지

통과 인증을 테 넌 트에 사용할 수 있고 toouninstall Azure AD Connect를 시도 하는 경우 아래와 같은 경고 메시지가 hello 표시: "사용자 됩니다 수에서 toosign tooAzure AD 다른 통과 인증 에이전트 없는 경우 다른 서버에 설치 합니다. "

설치 프로그램 인지 확인 [높은 사용 가능한](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability) Azure AD Connect tooavoid 주요 사용자 로그인을 제거 하기 전에.

## <a name="issues-with-enabling-hello-feature"></a>Hello 기능을 사용 하면 문제

### <a name="enabling-hello-feature-failed-because-there-were-no-authentication-agents-available"></a>인증 에이전트가 없습니다 없었기 때문에 hello 기능을 사용 하도록 설정 하지 못했습니다.

Toohave 필요한 하나 이상의 활성 인증 에이전트 tooenable 통과 인증 테 넌 트에 있습니다. Azure AD Connect 또는 독립 실행형 인증 에이전트를 설치하여 인증 에이전트를 설치할 수 있습니다.

### <a name="enabling-hello-feature-failed-due-tooblocked-ports"></a>Tooblocked 포트 hello 기능을 사용 하면 실패 했습니다.

Azure AD Connect가 설치 된 해당 hello 서버 Url 및 포트에 나열 된 서비스와 통신할 수 확인 [여기](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-1-check-prerequisites)합니다.

### <a name="enabling-hello-feature-failed-due-tootoken-or-account-authorization-errors"></a>Tootoken 또는 계정 권한 부여 오류 hello 기능을 사용 하면 실패 했습니다.

Hello 기능을 사용 하면 클라우드 전용 전역 관리자 계정을 사용 하는 것을 확인 합니다. Multi-factor authentication (MFA) 알려진 문제가-전역 관리자 계정, 사용 하도록 설정 해결 방법으로 MFA 일시적으로 (만 toocomplete hello 작업)를 해제 합니다.

## <a name="exchange-activesync-configuration-issues"></a>Exchange ActiveSync 구성 문제

통과 인증에 대 한 Exchange ActiveSync 지원을 구성 하는 경우 이들은 hello 일반적인 문제입니다.

### <a name="exchange-powershell-issue"></a>Exchange PowerShell 문제

Hello 표시 되 면 "**'PerTenantSwitchToESTSEnabled' 매개 변수 이름과 일치 하는 매개 변수를 찾을 수 없습니다\.**" hello를 실행 하는 동안 오류가 발생 했습니다. `Set-OrganizationConfig` Exchange PowerShell 명령를 Microsoft 지원에 문의 합니다.

### <a name="exchange-activesync-not-working"></a>Exchange ActiveSync가 작동하지 않음

hello 구성에서는 일부 시간 tootake 효과 가져와서-hello 시간 동안 사용자 환경에 따라 달라 집니다. 오랜 시간 동안 hello 상황이 지속 되 면 Microsoft 지원에 문의 합니다.

## <a name="collecting-pass-through-authentication-agent-logs"></a>통과 인증 에이전트 로그 수집

수 있는의 hello 형식에 따라 통과 인증 에이전트 로그에 대 한 서로 다른 위치에서 toolook이 필요 합니다.

### <a name="authentication-agent-event-logs"></a>인증 에이전트 이벤트 로그

오류 관련 toohello 인증 에이전트를 hello hello 서버에서 응용 프로그램 이벤트 뷰어를 열고 확인에서 **응용 프로그램 및 서비스 Logs\Microsoft\AzureAdConnect\AuthenticationAgent\Admin**합니다.

자세한 분석을 위해 hello "세션" 로그를 사용 하도록 설정 합니다. 정상적인 작업 중에 사용할 수는이 로그와 hello 인증 에이전트를 실행 하지 마십시오 문제 해결에 대해서만 사용 합니다. hello 로그 다시 비활성화 된 후에 hello 로그 내용을 표시 됩니다.

### <a name="detailed-trace-logs"></a>자세한 추적 로그

추적 로그에 대 한 tootroubleshoot 사용자 로그인 실패, 확인 **%programdata%\Microsoft\Azure AD 연결 인증 Agent\Trace\\**합니다. 이러한 로그는 특정 사용자 로그인에 실패 한 이유 hello 통과 인증 기능을 사용 하 여 하는 이유를 포함 합니다. 이러한 오류는 또한 hello 앞에 표시 된 매핑된 toohello 로그인 실패 이유 [테이블](#sign-in-failure-reasons-on-the-Azure-portal)합니다. 다음은 로그 항목의 예제입니다.

```
    AzureADConnectAuthenticationAgentService.exe Error: 0 : Passthrough Authentication request failed. RequestId: 'df63f4a4-68b9-44ae-8d81-6ad2d844d84e'. Reason: '1328'.
        ThreadId=5
        DateTime=xxxx-xx-xxTxx:xx:xx.xxxxxxZ
```

다음 명령을 실행 중인 hello hello 명령 프롬프트를 열어 hello 오류 (이 예에서는 앞에 오는 hello 경우 ' 1328')의 설명이 포함 된 세부 정보를 가져올 수 있습니다 (참고: 대신 '1328' hello 실제 오류 번호에서 로그를 볼 수 있는):

`Net helpmsg 1328`

![통과 인증](./media/active-directory-aadconnect-pass-through-authentication/pta3.png)

### <a name="domain-controller-logs"></a>도메인 컨트롤러 로그

감사 로깅이 설정 된 경우 도메인 컨트롤러의 hello 보안 로그에서 추가 정보를 찾을 수 있습니다. 간단한 방법을 tooquery 로그인 전송 된 요청을 통과 인증 에이전트에는 다음과 같습니다.

```
    <QueryList>
    <Query Id="0" Path="Security">
    <Select Path="Security">*[EventData[Data[@Name='ProcessName'] and (Data='C:\Program Files\Microsoft Azure AD Connect Authentication Agent\AzureADConnectAuthenticationAgentService.exe')]]</Select>
    </Query>
    </QueryList>
```

### <a name="performance-monitor-counters"></a>성능 모니터 카운터

또 다른 방법은 toomonitor 인증 에이전트는 각 서버 hello 인증 에이전트를 설치한 tootrack 특정 성능 모니터 카운터입니다. 다음 전역 카운터를 사용 하 여 hello (**# 설명 인증**, **#PTA 실패 한 인증** 및 **#PTA 성공한 인증**) 및 오류 카운터 (**# 설명 인증 오류**):

![통과 인증 성능 모니터 카운터](./media/active-directory-aadconnect-pass-through-authentication/pta12.png)

>[!IMPORTANT]
>통과 인증은 여러 인증 에이전트를 사용하여 고가용성을 제공하지만 부하 분산 기능은 제공하지 _않습니다_. 구성에 따라 모든 인증 에이전트는 요청과 _동일한_ 수를 수신하지 _않습니다_. 특정 인증 에이전트는 트래픽을 전혀 수신하지 않을 수도 있습니다.
