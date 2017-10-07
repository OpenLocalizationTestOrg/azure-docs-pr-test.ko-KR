---
title: "Azure AD Connect: 통과 인증 - 질문과 대답 | Microsoft Docs"
description: "Azure Active Directory 통과 인증에 대 한 질문과 대답 toofrequently 합니다."
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
ms.date: 08/03/2017
ms.author: billmath
ms.openlocfilehash: 550e2599177682f8ea971a05485dd5ac12b9b072
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-frequently-asked-questions"></a>Azure Active Directory 통과 인증: 질문과 대답

이 문서에서는 Azure AD(Azure Active Directory) 통과 인증에 대한 질문과 대답을 다룹니다. 새로운 내용을 계속 확인해 주세요.

>[!IMPORTANT]
>hello 통과 인증 기능은 현재 미리 보기 중입니다.

## <a name="which-of-hello-azure-ad-sign-in-methods---pass-through-authentication-password-hash-synchronization-and-active-directory-federation-services-ad-fs---should-i-choose"></a>Hello Azure AD 로그인 방법이-통과 인증, 암호 해시 동기화 및 Active Directory Federation Services (AD FS)-중을 선택 해야 합니까?

온-프레미스 환경 및 조직 요구 사항에 따라 다릅니다. 이 문서는 [비교의 다양 한 Azure AD 로그인 방법이 hello](active-directory-aadconnect-user-signin.md)합니다.

## <a name="is-pass-through-authentication-a-free-feature"></a>통과 인증은 무료 기능인가요?

통과 인증 무료 기능이 며 toouse Azure AD의 유료 버전 필요가 없는 것입니다. Hello 기능이 일반 공급 하는 경우 무료에 남아 있습니다.

## <a name="is-pass-through-authentication-available-in-microsoft-cloud-germanyhttpwwwmicrosoftdecloud-deutschland-and-microsoft-azure-government-cloudhttpsazuremicrosoftcomfeaturesgov"></a>[Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) 및 [Microsoft Azure Government 클라우드](https://azure.microsoft.com/features/gov/)에서 통과 인증을 사용할 수 있나요?

아니요, 통과 인증을 Azure AD의 전세계 인스턴스 hello에에서에 사용할 수 있습니다.

## <a name="does-conditional-accessactive-directory-conditional-accessmd-work-with-pass-through-authentication"></a>[조건부 액세스](../active-directory-conditional-access.md)는 통과 인증에서 작동하나요?

예, Azure Multi-Factor Authentication을 비롯한 모든 조건부 액세스 기능이 통과 인증에서 작동합니다.

## <a name="does-pass-through-authentication-support-alternate-id-as-hello-username-instead-of-userprincipalname"></a>통과 인증 대신 "userPrincipalName" hello 사용자 이름으로 "Alternate ID"를 지원 합니까?

예. 통과 인증을 지원 `Alternate ID` hello와 같이 Azure AD Connect에서 구성 된 경우 사용자 이름으로 [여기](active-directory-aadconnect-get-started-custom.md)합니다. 모든 Office 365 응용 프로그램에서 `Alternate ID`를 지원하지는 않습니다. Hello 지원 정책 toohello 특정 한 응용 프로그램의 설명서를 참조 하십시오.

## <a name="does-password-hash-synchronization-act-as-a-fallback-toopass-through-authentication"></a>대체 tooPass 통해 인증 방법으로 암호 해시 동기화 작동지 않습니다?

아니요, 암호 해시 동기화는 일반 대체 tooPass 통해 인증 않습니다. [통과 인증이 현재 지원하지 않는 시나리오](active-directory-aadconnect-pass-through-authentication-current-limitations.md#unsupported-scenarios)에 대한 대체 방식으로만 사용됩니다. tooavoid 사용자 로그인 실패, 통과 인증을 구성 해야 [고가용성](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability)합니다.

## <a name="can-i-install-an-azure-ad-application-proxyactive-directory-application-proxy-get-startedmd-connector-on-hello-same-server-as-a-pass-through-authentication-agent"></a>설치할 수는 [Azure AD 응용 프로그램 프록시](../active-directory-application-proxy-get-started.md) 커넥터 hello에 통과 인증 에이전트와 동일한 서버?

예,이 구성은 사용 버전 hello 통과 인증 에이전트의 브랜딩 hello로 (1.5.193.0 버전 이상).

## <a name="what-versions-of-azure-ad-connect-and-pass-through-authentication-agent-do-you-need"></a>필요한 Azure AD Connect 및 통과 인증 에이전트 버전은 무엇인가요?

버전 1.1.486.0 필요 하거나 나중에 Azure AD Connect 및 1.5.58.0 하거나 나중에이 기능 toowork에 대 한 통과 인증 에이전트 hello에 대 한 합니다. 모든 소프트웨어가 Windows Server 2012 R2 이상을 실행하는 서버에 설치되어 있어야 합니다.

## <a name="what-happens-if-my-users-password-has-expired-and-they-try-toosign-in-using-pass-through-authentication"></a>내 사용자의 암호가 만료 된 경우 어떤 일이 생기 고 통과 인증을 사용 하 여 toosign 시도 하 시겠습니까?

구성한 경우 [암호 쓰기 저장](../active-directory-passwords-update-your-own-password.md) 특정 사용자에 대 한 있으며 hello 사용자가 통과 인증을 사용 하 여 로그인 하는 경우에 변경 하거나 암호를 재설정할 수 있습니다. hello 암호 쓰기 저장 tooon 온-프레미스 Active Directory 예상 대로 합니다.

그러나 특정 사용자에 대 한 암호 쓰기 저장 구성 되지 않은 경우 또는 경우 hello 권한이 없습니다. 올바른 Azure AD 라이선스가 할당, hello 사용자 hello 클라우드에서 자신의 암호를 업데이트할 수 없습니다. 암호가 만료된 경우에도 암호를 업데이트할 수 없습니다. hello이이 메시지가 대신 표시: "조직 tooupdate 허용 하지 않습니다이 사이트의 암호입니다. 조직에서 권장 하는 toohello 방법에 따라 업데이트 하거나 하십시오 도움이 필요한 경우 관리자에 게 문의 합니다. " hello 사용자 또는 관리자에 게 암호가 tooreset 자신의 온-프레미스 Active Directory에서 합니다.

## <a name="how-does-pass-through-authentication-protect-you-against-brute-force-password-attacks"></a>통과 인증을 통해 무차별 암호 대입 공격으로부터 사용자를 보호하려면 어떻게 할까요?

자세한 내용은 [이 문서](active-directory-aadconnect-pass-through-authentication-smart-lockout.md)를 참조하세요.

## <a name="what-do-pass-through-authentication-agents-communicate-over-ports-80-and-443"></a>통과 인증 에이전트가 포트 80 및 443을 통해 통신하는 것은 무엇인가요?

- hello 인증 에이전트는 모든 기능 작업에 대해 포트 443 통해 HTTPS 요청을 설정합니다.
- hello 인증 에이전트는 포트 80 toodownload SSL 인증서 해지 목록을 통해 HTTP 요청을 설정합니다.

     >[!NOTE]
     >에 대 한 최근 업데이트로 hello hello 기능에 필요한 포트 수를 줄였습니다. 이전 버전의 Azure AD Connect 또는 hello 인증 에이전트를 설정한 경우 이러한 포트도 열어 두고: 5671, 8080 / 9090, 9091, 9350, 9352 / 10100 10120 합니다.

## <a name="can-hello-pass-through-authentication-agents-communicate-over-an-outbound-web-proxy-server"></a>Hello 통과 인증 에이전트는 아웃 바운드 웹 프록시 서버를 통해 통신할 수 있습니까?

예. 를 온-프레미스 환경에서 WPAD (웹 프록시 자동 검색)을 사용할 인증 에이전트 자동으로 toolocate 시도 하 고 hello 네트워크에서 웹 프록시 서버를 사용 합니다.

## <a name="can-i-install-two-or-more-pass-through-authentication-agents-on-hello-same-server"></a>설치할 수 있는 두 개 또는 많은 통과 인증 에이전트에서 동일한 서버 hello?

아니요, 단일 서버에는 통과 인증 에이전트 하나만 설치할 수 있습니다. 고가용성을 위해 tooconfigure 통과 인증을 원하는 경우이 hello 지침에 따라 [문서](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability) 대신 합니다.

## <a name="i-already-use-active-directory-federation-services-ad-fs-for-azure-ad-sign-in-how-do-i-switch-it-toopass-through-authentication"></a>Azure AD 로그인에 AD FS(Active Directory Federation Services)를 이미 사용하고 있습니다. 전환 하는 방법 것 tooPass 통해 인증?

Hello Azure AD Connect 마법사를 사용 하 여 로그인 방법으로 AD FS를 구성한 경우 변경 hello 사용자 로그인 방법을 통해 tooPass 인증 합니다. 이러한 변경은 hello 테 넌 트에서 통과 인증을 사용 하도록 설정 하 고 변환 _모든_ 관리 되는 도메인을 페더레이션 도메인입니다. 테넌트의 모든 후속 로그인 요청은 통과 인증을 통해 처리됩니다. 현재 지원 되는 방법이 있으면 Azure AD Connect toouse 내에서 서로 다른 도메인의 AD FS 및 통과 인증 조합 합니다.

AD FS hello 로그인 방법으로 구성 된 경우 _외부_ hello Azure AD Connect 마법사 hello 사용자 로그인 메서드를 변경 ("hello"구성 하지 않으면"옵션)에서 tooPass 통해 인증 합니다. 이 변경으로 통과 인증 hello 테 넌 트에 있습니다. 그러나 모든 페더레이션 도메인 로그인에 대 한 AD FS toouse를 계속 합니다. 일부 또는 전체 이러한 페더레이션 도메인 tooManaged 도메인 PowerShell toomanually convert를 사용 하십시오. 그 후에는 관리되는 도메인(_이 도메인만 해당_)의 모든 로그인 요청이 통과 인증을 통해 처리됩니다.

>[!IMPORTANT]
>통과 인증은 클라우드 전용 Azure AD 사용자의 로그인을 처리하지 않습니다.

## <a name="can-i-use-pass-through-authentication-in-a-multi-forest-ad-environment"></a>다중 포리스트 AD 환경에서 통과 인증을 사용할 수 있나요?

예. AD 포리스트 간에 포리스트 트러스트가 있고 이름 접미사 라우팅이 제대로 구성된 경우 다중 포리스트 환경이 지원됩니다.

## <a name="do-pass-through-authentication-agents-provide-load-balancing-capability"></a>통과 인증 에이전트는 부하 분산 기능을 제공하나요?

아니요, 여러 개의 통과 인증 에이전트를 설치하면 [고가용성](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability)이 보장되지만 부하 분산 기능은 제공되지 않습니다. Hello 인증 에이전트 중 하나 또는 두 hello 대량의 hello 로그인 요청을 처리 될 수 있습니다.

암호 유효성 검사 요청 인증 에이전트 필요 toohandle hello을 간단 합니다. 따라서 대부분의 고객에서 최고 및 평균 부하는 총 두세 개의 인증 에이전트를 통해 쉽게 처리됩니다.

인증 에이전트 닫기 tooyour 도메인 컨트롤러 tooimprove 로그인 대기 시간을 설치 하는 것이 좋습니다.

## <a name="can-i-install-hello-first-pass-through-authentication-agent-on-a-server-other-than-hello-one-that-runs-azure-ad-connect"></a>Hello 설치할 수 있는 Azure AD Connect를 실행 되는 hello 이외의 서버에서 통과 인증 에이전트를 첫 번째?

아니요, 이 시나리오는 지원되지 _않습니다_.

## <a name="how-many-pass-through-authentication-agents-should-i-install"></a>설치해야 하는 통과 인증 에이전트 수는 몇 개인가요?

다음이 권장됩니다.

- 총 두세 개의 인증 에이전트를 설치합니다. 대부분의 고객은 이 구성으로 충분합니다.
- 대기 시간 로그인 tooimprove 도메인 컨트롤러에서 (또는 가능한 닫기 toothem) 인증 에이전트를 설치 합니다.
- 있습니다 (인증 에이전트는 설치 된 서버)가 해당 암호가 필요 toobe 유효성을 검사 하는 hello 사용자로 toohello 동일한 AD 포리스트를 추가 되었는지 확인 합니다.

>[!NOTE]
>테넌트당 인증 에이전트 12개로 지정된 시스템 제한이 있습니다.

## <a name="how-can-i-disable-pass-through-authentication"></a>통과 인증을 사용하지 않도록 설정하려면 어떻게 하나요?

Hello Azure AD Connect 마법사를 다시 실행 하 고 통과 인증 tooanother 메서드에서 hello 사용자 로그인 메서드를 변경 합니다. 이러한 변경 hello 테 넌 트에서 통과 인증을 사용 하지 않도록 하 고 hello 서버에서 hello 인증 에이전트를 제거 합니다. 다른 서버에서 toomanually 제거 hello 에이전트 인증 해야합니다.

## <a name="what-happens-when-i-uninstall-a-pass-through-authentication-agent"></a>통과 인증 에이전트를 제거하면 어떻게 되나요?

서버에서 통과 인증 에이전트를 제거 하면 toostop 로그인 요청을 수락 됩니다. 있는지 다른 테 넌 트에 로그인 사용자 주요 tooavoid이이 작업을 수행 하기 전에 실행 되는 인증 에이전트를 확인 합니다.

## <a name="next-steps"></a>다음 단계
- [**현재 제한 사항**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - 이 기능은 현재 미리 보기로 제공됩니다. 지원되는 시나리오와 지원되지 않는 시나리오를 알아봅니다.
- [**빠른 시작**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Azure AD 통과 인증을 작동하고 실행합니다.
- [**기술 심층 분석**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - 이 기능의 작동 방식을 이해합니다.
- [**문제를 해결** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -tooresolve 공통 hello 기능으로 발급 하는 방법에 대해 알아봅니다.
- [**Azure AD 원활한 SSO**](active-directory-aadconnect-sso.md) - 이 보완 기능에 대해 자세히 알아봅니다.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 새로운 기능 요청을 제출합니다.
