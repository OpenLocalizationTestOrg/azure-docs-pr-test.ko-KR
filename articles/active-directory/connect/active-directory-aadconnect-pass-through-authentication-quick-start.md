---
title: "Azure AD 통과 인증 - 빠른 시작 | Microsoft Docs"
description: "이 문서에서는 Azure Active Directory (Azure AD) 통과 인증 tooget 시작 하는 방법을 설명 합니다."
services: active-directory
keywords: "Azure AD Connect 통과 인증, Active Directory 설치, Azure AD에 대한 필수 구성 요소, SSO, Single Sign-on"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: billmath
ms.openlocfilehash: d6d0f85fe144cf36cc94676f6592d37988b20647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-quick-start"></a>Azure Active Directory 통과 인증: 빠른 시작

## <a name="how-toodeploy-azure-ad-pass-through-authentication"></a>어떻게 toodeploy의 Azure AD 통과 인증

Azure Active Directory (Azure AD) 통과 인증 사용자 toosign tooboth 온-프레미스에 있으며이 사용 하 여 클라우드 기반 응용 프로그램에 동일한 암호 hello 합니다. 온-프레미스 Active Directory와 직접 비교해서 암호의 유효성을 검사하여 사용자를 로그인합니다.

>[!IMPORTANT]
>Azure AD 통과 인증은 현재 미리 보기로 제공됩니다. 이 기능은 미리 보기를 통해 사용 경우 확인 해야 hello 인증 에이전트의 미리 보기 버전을 업그레이드 하는 제공 된 hello 지침을 사용 하 여 [여기](./active-directory-aadconnect-pass-through-authentication-upgrade-preview-authentication-agents.md)합니다.

이러한 지침은 toodeploy 통과 인증 toofollow 필요합니다.

## <a name="step-1-check-prerequisites"></a>1단계: 필수 조건 확인

필수 구성 요소를 다음 해당 hello 적절 한지 확인 합니다.

### <a name="on-hello-azure-active-directory-admin-center"></a>Hello Azure Active Directory 관리 센터에서

1. Azure AD 테넌트에서 클라우드 전용 전역 관리자 계정을 만듭니다. 이러한 방식으로 온-프레미스 서비스 실패 하거나 사용할 수 없게 테 넌 트의 hello 구성을 관리할 수 있습니다. [클라우드 전용 전역 관리자 계정 추가](../active-directory-users-create-azure-portal.md)에 대해 자세히 알아봅니다. 이 단계를 수행 하면 잠기지 테 넌 트의 중요 한 tooensure입니다.
2. 하나 이상의 추가 [사용자 지정 도메인 이름](../active-directory-add-domain.md) tooyour Azure AD 테 넌 트입니다. 사용자는 이러한 도메인 이름 중 하나를 사용하여 로그인합니다.

### <a name="in-your-on-premises-environment"></a>온-프레미스 환경에서

1. Windows Server 2012 R2 또는 나중에 어떤 toorun에 Azure AD Connect를 실행 하는 서버를 식별 합니다. 해당 암호가 필요 toobe 유효성을 검사 하는 hello 사용자로 hello 서버 toohello 동일한 AD 포리스트를 추가 합니다.
2. Hello 설치 [최신 버전의 Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594) 이전 단계에서 식별 하는 hello 서버에 있습니다. 이미 Azure AD Connect를 실행 하는 경우 해당 hello 버전은 1.1.557.0 확인 이상.
3. Windows Server 2012 r 2를 실행 하는 추가 서버를 식별 하거나 나중에 독립 실행형 인증 에이전트는 어떤 toorun 합니다. hello 인증 에이전트 버전 toobe 1.5.193.0 필요 이상. 이 서버는 필요한 tooensure 고가용성 로그인 요청 합니다. 해당 암호가 필요 toobe 유효성을 검사 하는 hello 사용자로 hello 서버 toohello 동일한 AD 포리스트를 추가 합니다.
4. 서버와 Azure AD 간에 방화벽이 있으면 다음 항목 tooconfigure hello가 필요 합니다.
   - 인증 에이전트 만들 수 있음을 확인 **아웃 바운드** hello 다음 포트를 통해 AD tooAzure 요청:
   
   | 포트 번호 | 사용 방법 |
   | --- | --- |
   | **80** | Hello SSL 인증서를 확인 하는 동안 다운로드 인증서 해지 목록 (Crl) |
   | **443** | 서비스와의 모든 아웃바운드 통신 |
   
   Toooriginating 사용자에 따라 규칙을 적용 하는 방화벽, 네트워크 서비스로 실행 되는 Windows 서비스에서 트래픽에 대해 이러한 포트를 엽니다.
   - 허용 하는 경우 방화벽 또는 프록시 DNS 허용 목록을 허용 목록 연결 너무**\*. msappproxy.net** 및  **\*. servicebus.windows.net**합니다. 그렇지 않은 경우 액세스를 너무 허용[Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/details.aspx?id=41653)는 매주 업데이트 됩니다.
   - 인증 에이전트에서 액세스를 너무 해야**login.windows.net** 및 **login.microsoftonline.com** 초기 등록에 대 한을 열고 방화벽도 이러한 Url에 대 한 합니다.
   - 인증서 유효성 검사에 대 한 hello 다음 Url을 차단 해제: **mscrl.microsoft.com:80**, **crl.microsoft.com:80**, **ocsp.msocsp.com:80** 및  **www.microsoft.com:80**합니다. 이러한 URL은 다른 Microsoft 제품과의 인증서 유효성 검사에 사용되므로 이러한 URL을 이미 차단 해제했을 수 있습니다.

## <a name="step-2-enable-exchange-activesync-support-optional"></a>2단계: Exchange ActiveSync 지원 활성화(선택 사항)

이러한 지침은 tooenable Exchange ActiveSync 지원을 수행 합니다.

1. 사용 하 여 [Exchange PowerShell](https://technet.microsoft.com/library/mt587043(v=exchg.150).aspx) 다음 명령을 toorun hello:
```
Get-OrganizationConfig | fl per*
```

2. Hello의 hello 값을 확인 `PerTenantSwitchToESTSEnabled` 설정 합니다. Hello 값이 **true**, 테 넌 트 올바르게 구성 되어-이 일반적으로 대부분의 고객에 대 한 hello 사례입니다. Hello 값이 **false**실행 hello 다음 명령을:
```
Set-OrganizationConfig -PerTenantSwitchToESTSEnabled:$true
```

3. Hello의 해당 hello 값을 확인 `PerTenantSwitchToESTSEnabled` 이제 설정은 너무**true**합니다. Toohello 다음 단계로 이동 하기 전에 시간을 기다립니다.

이 단계 동안 문제가 발생하면 자세한 정보는 [문제 해결 가이드](active-directory-aadconnect-troubleshoot-pass-through-authentication.md#exchange-activesync-configuration-issues)를 확인하세요.

## <a name="step-3-enable-hello-feature"></a>3 단계: hello 기능 사용

[Azure AD Connect](active-directory-aadconnect.md)를 통해 통과 인증을 사용하도록 설정할 수 있습니다.

>[!IMPORTANT]
>Hello Azure AD Connect 기본 또는 스테이징 서버에서 통과 인증을 사용할 수 있습니다. Hello 주 서버에서 사용 하는 것이 좋습니다.

를 설치 하는 hello에 대 한 Azure AD Connect 처음으로 하는 경우 선택 hello [사용자 지정 설치 경로가](active-directory-aadconnect-get-started-custom.md)합니다. Hello에 **사용자 로그인** 페이지에서 선택 **통과 인증** 메서드의 기호 hello으로 합니다. Hello에 설치 되어 통과 인증 에이전트를 성공적으로 완료 되 면 Azure AD Connect와 같은 서버. 또한 hello 통과 인증 기능은 테 넌 트에 사용 됩니다.

![Azure AD Connect - 사용자 로그인](./media/active-directory-aadconnect-sso/sso3.png)

Azure AD Connect를 이미 설치한 경우 (hello를 사용 하 여 [express 설치](active-directory-aadconnect-get-started-express.md) 또는 hello [사용자 지정 설치](active-directory-aadconnect-get-started-custom.md) 경로)을 선택 **변경 사용자 로그인 페이지** Azure AD에서 연결 하 고 클릭 **다음**합니다. 다음 선택 **통과 인증** 메서드의 기호 hello으로 합니다. Hello에 설치 되어 통과 인증 에이전트를 성공적으로 완료 되 면 Azure AD Connect 및 hello 기능으로 동일한 서버를 테 넌 트에 사용할 수 있습니다.

![Azure AD Connect - 사용자 로그인 변경](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

>[!IMPORTANT]
>통과 인증은 테넌트 수준 기능입니다. 로그인에서 사용자에 대 한 영향을 켜서 _모든_ hello 테 넌 트의 도메인을 관리 합니다. 인증 tooPass 통해 AD FS에서에서 전환 하는 경우에 AD FS 인프라를 종료 하기 전에 12 시간 이상 기다리는-이 대기 시간은 tooensure 사용자는 전환 중 tooExchange ActiveSync 로그인 유지할 수 있는 것이 좋습니다.

## <a name="step-4-test-hello-feature"></a>4 단계: hello 기능 테스트

이러한 지침은 tooverify 통과 인증을 올바르게 설정 했는지를 수행 합니다.

1. Toohello 로그인 [Azure Active Directory 관리 센터](https://aad.portal.azure.com) 테 넌 트에 대 한 hello 전역 관리자 자격 증명을 사용 합니다.
2. 선택 **Azure Active Directory** hello 왼쪽 탐색 모음에 있습니다.
3. **Azure AD Connect**를 선택합니다.
4. 해당 hello 확인 **통과 인증** 기능으로 표시 **Enabled**합니다.
5. **통과 인증**을 선택합니다. 이 블레이드는 hello 서버 인증 에이전트 설치 되는 위치를 나열 합니다.

![Azure Active Directory 관리 센터 - Azure AD Connect 블레이드](./media/active-directory-aadconnect-pass-through-authentication/pta7.png)

![Azure Active Directory 관리 센터 - 통과 인증 블레이드](./media/active-directory-aadconnect-pass-through-authentication/pta8.png)

이 단계에서는, 테넌트에 있는 모든 관리되는 도메인의 사용자가 통과 인증을 사용하여 로그인할 수 있습니다. 그러나 페더레이션된 도메인의 사용자가 toosign Active Directory Federation Services (AD FS) 또는 이전에 구성 된 페더레이션 공급자를 사용 하 여 계속 합니다. 페더레이션된 toomanaged에서 도메인을 변환 하는 경우 해당 도메인의 모든 사용자가 자동으로 시작 통과 인증을 사용 하 여 로그인 합니다. 클라우드 전용 사용자 hello 통과 인증 기능에 의해 영향을 받지 않습니다.

## <a name="step-5-ensure-high-availability"></a>5단계: 고가용성 보장

프로덕션 환경에서 통과 인증 toodeploy 하려는 경우 독립 실행형 인증 에이전트를 설치 해야 합니다. 서버에이 두 번째 인증 에이전트를 설치 _다른_ 하나의 실행 중인 Azure AD Connect hello 및 첫 번째 인증 에이전트 hello 보다 합니다. 이렇게 설치하면 로그인 요청의 고가용성이 제공됩니다. 이러한 지침은 toodeploy 독립 실행형 인증 에이전트를 수행 합니다.

1. **Hello hello 인증 에이전트의 최신 버전을 다운로드 (1.5.193.0 버전 이상)**: toohello 로그인 [Azure Active Directory 관리 센터](https://aad.portal.azure.com) 테 넌 트의 전역 관리자 자격 증명을 사용 합니다.
2. 선택 **Azure Active Directory** hello 왼쪽 탐색 모음에 있습니다.
3. **Azure AD Connect**를 선택하고 **통과 인증**을 선택합니다. **에이전트 다운로드**를 선택합니다.
4. Hello 클릭 **조건에 동의 및 다운로드** 단추입니다.
5. **Hello hello 인증 에이전트의 최신 버전을 설치**: hello 앞 단계에서에서 다운로드 한 실행 hello를 실행 합니다. 메시지가 표시되면 테넌트의 전역 관리자 자격 증명을 입력합니다.

![Azure Active Directory 관리 센터 - 인증 에이전트 다운로드 버튼](./media/active-directory-aadconnect-pass-through-authentication/pta9.png)

![Azure Active Directory 관리 센터 - 에이전트 다운로드 블레이드](./media/active-directory-aadconnect-pass-through-authentication/pta10.png)

>[!NOTE]
>다운로드할 수 있습니다 인증 에이전트에서 hello [여기](https://aka.ms/getauthagent)합니다. 검토 하 고 hello 인증 에이전트를 승인 하는 확인 [서비스 약관](https://aka.ms/authagenteula) _전에_ 설치 합니다.

## <a name="next-steps"></a>다음 단계
- [**현재 제한 사항**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - 이 기능은 현재 미리 보기로 제공됩니다. 지원되는 시나리오와 지원되지 않는 시나리오를 알아봅니다.
- [**기술 심층 분석**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - 이 기능의 작동 방식을 이해합니다.
- [**질문과 대답** ](active-directory-aadconnect-pass-through-authentication-faq.md) -toofrequently 질문과 대답을 제공 합니다.
- [**문제를 해결** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -tooresolve 공통 hello 기능으로 발급 하는 방법에 대해 알아봅니다.
- [**Azure AD 원활한 SSO**](active-directory-aadconnect-sso.md) - 이 보완 기능에 대해 자세히 알아봅니다.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 새로운 기능 요청을 제출합니다.
