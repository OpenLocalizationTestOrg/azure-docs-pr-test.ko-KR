---
title: "Azure AD Connect: Seamless Single Sign-On 문제 해결 | Microsoft Docs"
description: "이 항목에서는 설명 방법을 tootroubleshoot Azure Active Directory 원활한 Single Sign-on (Azure AD 원활한 SSO)."
services: active-directory
keywords: "Azure AD Connect의 정의, Active Directory 설치, Azure AD에 대한 필수 구성 요소, SSO, Single Sign-on"
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
ms.openlocfilehash: f1c1c11522f22d5bc742c126fff483c5b06e1f06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-active-directory-seamless-single-sign-on"></a>Azure Active Directory Seamless Single Sign-On 문제 해결

이 문서에서는 Azure AD Seamless Single Sign-On과 관련된 일반적인 문제에 대한 문제 해결 정보를 찾을 수 있습니다.

## <a name="known-issues"></a>알려진 문제

- 30개 이상의 AD 포리스트를 동기화하면 Azure AD Connect를 통해 Seamless SSO를 활성화할 수 없습니다. 문제를 해결할 수 있습니다 [수동으로 활성화 해야](#manual-reset-of-azure-ad-seamless-sso) 테 넌 트에 hello 기능입니다.
- "추가 Azure AD 서비스 Url (https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net) toohello"신뢰할 수 있는 사이트"hello 로컬 인트라넷 영역 대신 영역" **사용자가 로그인**합니다.
- Firefox 및 Edge의 개인 검색 모드에서는 Seamless SSO가 작동하지 않습니다. 또한 Internet Explorer에서 향상된 보호 모드가 켜져 있을 때도 마찬가지입니다.

>[!IMPORTANT]
>에서는 최근에 롤백 가장자리 tooinvestigate에 대 한 지원 고객이 신고한 문제.

## <a name="check-status-of-hello-feature"></a>Hello 기능의 상태를 확인 합니다.

Hello 원활한 SSO 기능을는 여전히 확인 **Enabled** 테 넌 트에 있습니다. Toohello 이동 하 여 상태를 확인할 수 있습니다 **Azure AD Connect** hello에 블레이드 [Azure Active Directory 관리 센터](https://aad.portal.azure.com/)합니다.

![Azure Active Directory 관리 센터 - Azure AD Connect 블레이드](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="sign-in-failure-reasons-on-hello-azure-active-directory-admin-center"></a>Hello Azure Active Directory 관리 센터에 로그인 실패 이유

원활한 SSO와 사용자 로그인 문제를 해결 하는 것이 좋습니다 toostart는 hello에 toolook [로그인 활동 보고서](../active-directory-reporting-activity-sign-ins.md) hello에 [Azure Active Directory 관리 센터](https://aad.portal.azure.com/)합니다.

![Azure Active Directory 관리 센터 - 로그인 보고서](./media/active-directory-aadconnect-sso/sso9.png)

너무 이동**Azure Active Directory** -> **로그인** hello에 [Azure Active Directory 관리 센터](https://aad.portal.azure.com/) 특정 사용자의 로그인 활동을 클릭 합니다. Hello에 대 한 확인 **로그인 오류 코드** 필드입니다. 해당 필드 tooa 실패 이유 및 다음 표에 hello를 사용 하는 확인의 hello 값을 매핑하십시오.

|로그인 오류 코드|로그인 실패 이유|해결 방법
| --- | --- | ---
| 81001 | 사용자의 Kerberos 티켓이 너무 큽니다. | 사용자의 그룹 멤버 자격 수를 줄이고 다시 시도합니다.
| 81002 | 없습니다 toovalidate 사용자의 Kerberos 티켓입니다. | [문제 해결 검사 목록](#troubleshooting-checklist)을 참조하세요.
| 81003 | 없습니다 toovalidate 사용자의 Kerberos 티켓입니다. | [문제 해결 검사 목록](#troubleshooting-checklist)을 참조하세요.
| 81004 | Kerberos 인증 시도가 실패했습니다. | [문제 해결 검사 목록](#troubleshooting-checklist)을 참조하세요.
| 81008 | 없습니다 toovalidate 사용자의 Kerberos 티켓입니다. | [문제 해결 검사 목록](#troubleshooting-checklist)을 참조하세요.
| 81009 | "Toovalidate 수 없습니다 사용자의 Kerberos 티켓입니다. | [문제 해결 검사 목록](#troubleshooting-checklist)을 참조하세요.
| 81010 | 원활한 SSO 없으므로 hello 사용자의 Kerberos 티켓이 만료 되었거나 올바르지 않습니다. | 사용자는 회사 네트워크 내부 도메인에 가입 된 장치에서 toosign에 필요합니다.
| 81011 | 없습니다 toofind 사용자 개체 hello 사용자의 Kerberos 티켓에 대 한 정보를 기반 합니다. | Azure AD에 Azure AD Connect toosynchronize 사용자 정보를 사용 합니다.
| 81012 | tooAzure AD에서에서 toosign hello 사용자는 hello 장치에 로그인 하는 hello 사용자와에서 다릅니다. | 다른 장치에서 로그인합니다.
| 81013 | 없습니다 toofind 사용자 개체 hello 사용자의 Kerberos 티켓에 대 한 정보를 기반 합니다. |Azure AD에 Azure AD Connect toosynchronize 사용자 정보를 사용 합니다. 

## <a name="troubleshooting-checklist"></a>문제 해결 검사 목록

다음 검사 목록 tootroubleshoot 원활한 SSO 문제 hello를 사용 합니다.

- Azure AD Connect에서 hello 원활한 SSO 기능 사용 하는지 확인 합니다. 모든 hello 있는지 확인 하는 경우 (예를 들어 인해 차단 tooa 포트) hello 기능을 사용할 수 없습니다 [필수](active-directory-aadconnect-sso-quick-start.md#step-1-check-prerequisites) 위치에 있습니다.
- 이러한 Azure AD 두 Url 모두 (https://autologon.microsoftazuread-sso.com 및 https://aadg.windows.net.nsatc.net)은 hello 사용자 인트라넷 영역 설정의 일부를 확인 합니다.
- 회사 장치 hello은 조인 된 toohello AD 도메인을 확인 합니다.
- Hello 사용자가 AD 도메인 계정을 사용 하 여 toohello 장치에서 로그를 확인 합니다.
- Hello 사용자의 계정이 설정 되어 있는지 AD 포리스트에서 원활한 SSO 된 위치에서 확인 하십시오.
- Hello 장치는 hello 회사 네트워크에 연결 되어 있는지 확인 합니다.
- Hello 장치 시간 hello Active Directory와 hello 도메인 컨트롤러의 시간과 동기화 되었는지 확인 하는 서로 5 분 이내.
- Hello를 사용 하 여 hello 장치에서 기존 Kerberos 티켓이 목록 **klist** 명령 프롬프트에서 명령을 합니다. Hello에 대 한 티켓을 발급 하는 경우 확인 `AZUREADSSOACCT` 컴퓨터 계정이 있는지 합니다. 사용자의 Kerberos 티켓은 일반적으로 12시간 동안 유효합니다. Active Directory에 다른 설정이 있을 수 있습니다.
- Hello를 사용 하 여 hello 장치에서 기존 Kerberos 티켓을 제거 **klist 제거** 명령을 실행 하 고 다시 시도 하십시오.
- toodetermine는 JavaScript 관련 문제가 있을 경우 로그를 검토 hello 콘솔 hello 브라우저 (아래에서 "개발자 도구")입니다.
- 검토 hello [도메인 컨트롤러 로그](#domain-controller-logs) 도 합니다.

### <a name="domain-controller-logs"></a>도메인 컨트롤러 로그

도메인 컨트롤러에서 성공 감사를 사용 하는 경우 다음 사용자가 원활 하 게 SSO를 사용 하 여 로그인 할 때마다 보안 항목은 hello 이벤트 로그에 기록 합니다. 다음 쿼리에서 hello를 사용 하 여 이러한 보안 이벤트를 찾을 수 있습니다 (이벤트 **4769** hello 컴퓨터 계정에 연결 된 **AzureADSSOAcc$**):

```
    <QueryList>
      <Query Id="0" Path="Security">
    <Select Path="Security">*[EventData[Data[@Name='ServiceName'] and (Data='AZUREADSSOACC$')]]</Select>
      </Query>
    </QueryList>
```

## <a name="manual-reset-of-hello-feature"></a>Hello 기능의 수동 다시 설정

도움이 되지 않는 문제 해결, 경우에 테 넌 트에 hello 기능을 수동으로 재설정할 수 있습니다. Azure AD Connect를 실행 중인 hello 온-프레미스 서버에서 다음이 단계를 따릅니다.

### <a name="step-1-import-hello-seamless-sso-powershell-module"></a>1 단계: hello 원활한 SSO PowerShell 모듈을 가져옵니다

1. 첫째, 다운로드 및 설치 hello [Microsoft Online Services 로그인 도우미](http://go.microsoft.com/fwlink/?LinkID=286152)합니다.
2. 다운로드 하 고 hello 설치 [Windows PowerShell 용 Azure Active Directory 모듈을 64 비트](http://go.microsoft.com/fwlink/p/?linkid=236297)합니다.
3. Toohello 이동 `%programfiles%\Microsoft Azure Active Directory Connect` 폴더입니다.
4. 이 명령을 사용 하 여 hello 원활한 SSO PowerShell 모듈 가져오기: `Import-Module .\AzureADSSO.psd1`합니다.

### <a name="step-2-get-hello-list-of-ad-forests-on-which-seamless-sso-has-been-enabled"></a>2 단계: AD 포리스트 원활한 SSO를 사용할 수 있는 hello 목록 가져오기

1. 관리자 권한으로 PowerShell을 실행합니다. PowerShell에서 `New-AzureADSSOAuthenticationContext`를 호출합니다. 메시지가 표시되면 테넌트의 전역 관리자 자격 증명을 입력합니다.
2. `Get-AzureADSSOStatus`를 호출합니다. 이 명령에이 기능이 설정 되는 AD 포리스트 ("hello"도메인 목록 보고) 목록 hello를 제공 합니다.

### <a name="step-3-disable-seamless-sso-for-each-ad-forest-that-it-was-set-it-up-on"></a>3단계: 사용하도록 설정된 각 AD 포리스트에 대한 Seamless SSO 비활성화

1. `$creds = Get-Credential`를 호출합니다. 메시지가 표시 되 면 hello AD 포리스트 의도 대 한 hello 도메인 관리자 자격 증명을 입력 합니다.
2. `Disable-AzureADSSOForest -OnPremCredentials $creds`를 호출합니다. 이 명령은 제거 hello `AZUREADSSOACCT` hello에서 컴퓨터 계정 온-프레미스 도메인 컨트롤러가 특정 AD 포리스트에 대 한 합니다.
3. 이전 단계에서 hello 기능을 설정 하는 각 AD 포리스트에 대 한 hello를 반복 합니다.

### <a name="step-4-enable-seamless-sso-for-each-ad-forest"></a>4단계: 각 AD 포리스트에 대한 Seamless SSO 활성화

1. `Enable-AzureADSSOForest`를 호출합니다. 메시지가 표시 되 면 hello AD 포리스트 의도 대 한 hello 도메인 관리자 자격 증명을 입력 합니다.
2. Hello 이전에 tooset hello 기능을 사용 하려는 각 AD 포리스트에 대 한 단계를 반복 합니다.

### <a name="step-5-enable-hello-feature-on-your-tenant"></a>5단계. 테 넌 트에 hello 기능 설정

호출 `Enable-AzureADSSO` hello에 "true"를 입력 `Enable: ` 프롬프트 tooturn 테 넌 트의 hello 기능입니다.
