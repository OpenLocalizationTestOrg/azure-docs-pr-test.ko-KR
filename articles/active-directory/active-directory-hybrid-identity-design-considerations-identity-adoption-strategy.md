---
title: "하이브리드 identity 채택 전략을 정의 하는 aaaAzure Active Directory 하이브리드 id 디자인 고려 사항-| Microsoft Docs"
description: "조건부 액세스 제어를 통해 Azure Active Directory hello 사용자를 인증할 때 및 toohello 응용 프로그램 액세스를 허용 하기 전에 선택 hello 특정 상태를 확인 합니다. 이러한 조건이 충족 되 면 hello 사용자가 인증 되 고 toohello 응용 프로그램 액세스를 허용 합니다."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: b92fa5a9-c04c-4692-b495-ff64d023792c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 9ffca675d0c714392adfcbbc4dcfad12fccbac78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="define-a-hybrid-identity-adoption-strategy"></a>하이브리드 ID 채택 전략 정의
이 태스크에서는 프로그램 하이브리드 id 솔루션 toomeet hello 비즈니스 요구 사항에서 설명한에 대 한 hello 하이브리드 identity 채택 전략을 정의 합니다.

* [비즈니스 요구 사항 결정](active-directory-hybrid-identity-design-considerations-business-needs.md)
* [디렉터리 동기화 요구 사항 결정](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)
* [Multi-Factor Authentication 요구 사항 결정](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)

## <a name="define-business-needs-strategy"></a>비즈니스 요구 사항 전략 정의
결정 hello 조직의 비즈니스 요구 사항을 해결 하는 hello 첫 번째 작업입니다.  신중하지 않으면 매우 광범위한 범위 변형이 발생할 수 있습니다.  시작 하는 hello에에서 단순하게 유지 하지만 tooplan 수용 한 hello 미래 변화를 용이 하 게 디자인을 항상 잊지 말고 수행 합니다.  간단한 디자인 또는 매우 복잡 한 될, Azure Active Directory는 Office 365, Microsoft 온라인 서비스와 클라우드 인식 응용 프로그램을 지 hello Microsoft Identity 플랫폼입니다.

## <a name="define-an-integration-strategy"></a>통합 전략 정의
Microsoft에는 클라우드 ID, 동기화된 ID 및 페더레이션된 ID는 3개의 주요 통합 시나리오가 있습니다.  이러한 통합 전략 중 하나를 채택하도록 계획해야 합니다.  다를 수 있습니다 및 hello 결정 사항은 하나를 선택에서 포함 될 수 있습니다 종류를 선택 하면 전략 hello 원하는 tooprovide 사용자 환경의 없으므로 이미 내부 hello 기존 인프라의 일부 이며 가장 비용 효과적인 hello 합니다.  

![](./media/hybrid-id-design-considerations/integration-scenarios.png)

위 그림 hello에 정의 된 hello 시나리오입니다.

* **Identities 클라우드**:이 hello 클라우드에서 전적으로 존재 하는 id입니다.  Azure AD의 hello 경우 Azure AD 디렉터리에 구체적으로 존재 합니다.
* **동기화**:이 온-프레미스 존재 하는 id 및 hello 클라우드입니다.  Azure AD Connect를 사용하여 기존 Azure AD 계정으로 이러한 사용자를 만들거나 조인합니다.  hello 사용자의 암호 해시 클라우드에서 동기화 되 hello 온-프레미스 환경 toohello에 암호 해시를 무엇 이라고 합니다.  동기화를 사용 하는 사용자 hello 온-프레미스 환경에서 비활성화 된 경우까지 걸릴 수 있으므로 too3 시간이 해당 계정 상태 tooshow에 대 한 Azure AD에서 hello 한 가지 주의할 점은입니다.  기한 toohello 동기화 시간 간격입니다.
* **페더레이션**: 이러한 id가 온-프레미스 및 클라우드 hello 합니다.  Azure AD Connect를 사용하여 기존 Azure AD 계정으로 이러한 사용자를 만들거나 조인합니다.  

> [!NOTE]
> Hello 동기화 옵션에 대 한 자세한 내용은 [Azure Active Directory와 온-프레미스 id 통합](connect/active-directory-aadconnect.md)합니다.
> 
> 

다음 표에서 hello hello 장점 및 단점 각 hello 전략에 따라 결정 하는 데 도움이 됩니다.

| 전략 | 장점 | 단점 |
| --- | --- | --- |
| **클라우드 ID** |소규모 조직에 대 한 보다 쉽게 toomanage 합니다. <br> 아무것도 tooinstall에-프레미스-No 추가 하드웨어가 필요<br>Hello 사용자 hello 퇴사 하는 경우 쉽게 사용할 수 없습니다. |Hello 클라우드에서 워크 로드에 액세스할 때 사용자가 toosign에 필요 합니다. <br> 암호 되거나 클라우드 및 온-프레미스 id 동일 hello 되지 않을 수 있습니다. |
| **동기화됨** |온-프레미스 암호는 온-프레미스 및 클라우드 디렉터리를 인증합니다  <br>소형, 중형 또는 대형 조직에 대해 보다 쉽게 toomanage <br>사용자는 일부 리소스에 대한 SSO(Single Sign-On)를 가질 수 있습니다  <br> 동기화에 대한 Microsoft의 기본 메서드 <br> 보다 쉽게 toomanage |일부 고객이 특정 회사의 정책은 인해 hello 사용 하 여 해당 디렉터리를 클라우드 하기 꺼려할 toosynchronize 될 수 있습니다. |
| **페더레이션** |사용자는 Single Sign-On(SSO)을 가질 수 있습니다  <br>사용자가 종료 모드로 들어가거나에서 hello 계정 수 수 즉시 해제 되 고 액세스가 해지<br> 동기화되어 수행할 수 없는 고급 시나리오를 지원합니다 |더 toosetup 단계 및 구성 <br> 더 높은 유지 관리 <br> Hello STS 인프라에 대 한 추가 하드웨어를 필요할 수 있습니다. <br> 추가 하드웨어 tooinstall hello 페더레이션 서버에 필요할 수 있습니다. 추가 소프트웨어는 AD FS에서 사용 되는 경우에 필요 <br> SSO에 대한 광범위한 설정이 필요 <br> 오류 hello 페더레이션 서버가 다운 된 경우의 중요 한 점은, 사용자 수 없습니다 tooauthenticate |

### <a name="client-experience"></a>클라이언트 환경
사용 하는 hello 전략 hello 사용자 로그인 환경에 따라 결정 됩니다.  hello 다음 표에서 제공 toobe 발생할 hello 사용자가 로그인 것을 예상 해야 대 한 정보와 함께 있습니다.  페더레이션된 ID 공급자가 모두 시나리오에서 SSO를 지원하지는 않습니다.

**도메인 가입된 개인 네트워크 응용 프로그램**:

|  | 동기화된 ID | 페더레이션된 ID |
| --- | --- | --- |
| 웹 브라우저 |폼 기반 인증 |single sign on, 경우에 따라 필요한 toosupply 조직 ID |
| Outlook |자격 증명 확인 |자격 증명 확인 |
| 비즈니스용 Skype(Lync) |자격 증명 확인 |Exchange에 대한 자격 증명을 확인하는 Lync용 Single Sign-On |
| Skydrive Pro |자격 증명 확인 |Single Sign On |
| Office Pro Plus 구독 |자격 증명 확인 |Single Sign On |

**외부 또는 신뢰할 수 없는 원본**:

|  | 동기화된 ID | 페더레이션된 ID |
| --- | --- | --- |
| 웹 브라우저 |폼 기반 인증 |폼 기반 인증 |
| Outlook, 비즈니스용 Skype(Lync), Skydrive Pro, Office 구독 |자격 증명 확인 |자격 증명 확인 |
| Exchange ActiveSync |자격 증명 확인 |Exchange에 대한 자격 증명을 확인하는 Lync용 Single Sign-On |
| 모바일 앱 |자격 증명 확인 |자격 증명 확인 |

Azure AD와 하나의 tooprovide 페더레이션 타사 IdP 또는 진행 중인 toouse 있다고 1 작업에서 결정 한, toobe 다음 hello 인식 지원 기능이 필요 합니다.

* 인증 tooAzure AD 및 관련된 응용 프로그램 hello Sp-lite 프로필에 대 한 호환 되는 SAML 2.0 공급자 지원할 수 있습니다.
* Auth tooOWA, SPO를 용이 하 게 하는 지원 수동 인증 등입니다.
* Exchange Online 클라이언트 hello SAML 2.0 향상 된 클라이언트 프로필 ECP ()를 통해 지원할 수 있습니다.

또한 어떤 기능을 사용할 수 없는지 알고 있어야 합니다.

* WS-트러스트/페더레이션이 지원되지 않으면 다른 모든 활성 클라이언트는 연결이 끊어집니다.
  * 즉, 없음 Lync 클라이언트, OneDrive 클라이언트, Office Mobile 이전 tooOffice 2016, Office 구독
* Office toopassive 인증 하 게 전환 있도록 toosupport 순수 SAML 2.0 IdPs 아니라 지원 하 여 클라이언트 별로 수 있습니다

> [!NOTE]
> Hello hello 문서 http://aka.ms/ssoproviders 가장 업데이트 목록을 참조 하세요.
> 
> 

## <a name="define-synchronization-strategy"></a>동기화 전략 정의
이 작업에서는 hello 도구를 사용 하는 toosynchronize hello 조직의 온-프레미스 데이터 toohello 클라우드 및 기능을 정의 합니다 토폴로지를 사용 해야 합니다.  대부분의 조직에서는 Active Directory를 사용 하므로 위의 Azure AD Connect tooaddress hello 질문을 사용 하는 방법은 좀 더 자세히 제공 됩니다.  Active Directory가 없는 환경에서는 FIM 2010 r 2를 사용 하는 방법에 대 한 정보가 또는 MIM 2016 toohelp이이 전략을 계획 합니다.  그러나 Azure AD Connect의 이후 릴리스에서 지원 LDAP 디렉터리의 경우 일정에 따라 하므로,이 정보는 수 tooassist 수 있습니다.

### <a name="synchronization-tools"></a>동기화 도구
Hello 년 동안 몇 가지 동기화 도구가 존재 있고 다양 한 시나리오에 사용 합니다.  현재 Azure AD Connect의 지원 되는 모든 시나리오에 대 한 선택 이동 tootool을 hello 됩니다.  또한 AAD 동기화 및 DirSync은 여전히 있으며 사용자 환경에서 표시되기도 합니다. 

> [!NOTE]
> Hello 최신 내용은 hello 지원 기능에 대 한 각 도구의 [디렉터리 통합 도구 비교](active-directory-hybrid-identity-design-considerations-tools-comparison.md) 문서.  
> 
> 

### <a name="supported-topologies"></a>지원되는 토폴로지
동기화 전략을 정의할 때 사용 되는 hello 토폴로지를 결정 합니다. Hello 따라 토폴로지를 확인할 수는 2 단계에서 결정 된 정보는 적절 한 toouse hello입니다. hello 단일 포리스트, 단일 Azure AD 토폴로지는 가장 일반적인 hello 및 단일 Active Directory 포리스트 및 Azure AD의 단일 인스턴스 구성 됩니다.  이 toobe 대부분의 hello 시나리오에 사용 된 것 이며 예상 hello 토폴로지 아래 hello 그림에 나와 있는 것 처럼 Azure AD 빠른 연결 설치를 사용 하는 경우 합니다.

![](./media/hybrid-id-design-considerations/single-forest.png)단일 포리스트 시나리오 매우 일반적 이기 크고 작은 조직 toohave 그림 5에 표시 된 것 처럼 여러 포리스트가 있습니다.

> [!NOTE]
> 에 대 한 자세한 내용은 hello 다른 온-프레미스 및 Azure AD Connect 동기화와 함께 Azure AD 토폴로지 hello 문서를 읽어 보세요. [Azure AD Connect에 대 한 토폴로지](connect/active-directory-aadconnect-topologies.md)합니다.
> 
> 

![](./media/hybrid-id-design-considerations/multi-forest.png) 

다중 포리스트 시나리오

이 hello 경우에는 다음 다중 포리스트-단일 hello hello 다음 항목에 해당할 경우 Azure AD 토폴로지를 고려해 야 합니다.

* 사용자는 포리스트 전반에 걸쳐 1 id가-사용자 섹션 아래에 고유 하 게 식별 하는 hello이에서 자세히 설명 합니다.
* hello 사용자가 자신의 id의 위치를 가리키는 toohello 포리스트 인증
* UPN 및 소스 앵커(변경할 수 없는 ID)는 이 포리스트에서 들어옵니다.
* Azure AD Connect에서 액세스할 수 있는 모든 포리스트는 – 즉, toobe 도메인에 가입 하지 않아도 하 고이 용이 하 게이 경우에 DMZ에 배치할 수 있습니다.
* 사용자에게는 하나의 사서함만 있습니다.
* 사용자의 사서함을 호스팅하는 hello 포리스트에 hello hello Exchange GAL 주소 목록 ()에 표시 되는 특성에 대 한 최상의 데이터 품질
* Hello 사용자에 게 사서함이 없는 경우 모든 포리스트에 있습니다 toocontribute 사용 되는 이러한 값 수
* 연결 된 사서함이 있는 경우 다음 이기도 다른 계정에 사용 되는 다른 포리스트에 toosign에 합니다.

> [!NOTE]
> Hello 클라우드 및 온-프레미스에 있는 개체 "통해 연결 하는" 고유 식별자입니다. 디렉터리 동기화의 hello 컨텍스트에서이 고유 식별자는 참조 된 tooas hello SourceAnchor입니다. 이 Single Sign-on의 hello 컨텍스트에서 참조 tooas hello ImmutableId입니다. [Azure AD Connect에 대 한 개념을 디자인](connect/active-directory-aadconnect-design-concepts.md#sourceanchor) SourceAnchor의 hello 사용과 관련 자세한 고려 사항에 대 한 합니다.
> 
> 

위의 hello 충족 되지 않은 경우 둘 이상의 활성 계정 또는 둘 이상의 사서함이 있는 Azure AD Connect 하나를 선택 되 고 다른 hello 무시 됩니다.  사서함 하지만 다른 계정이 없으면 연결 하면 이러한 계정은 내보낸된 tooAzure AD 수 없습니다 및 해당 사용자 그룹의 구성원 됩니다.  떠 다릅니다 DirSync와 지난 hello 및 이러한 다중 포리스트 시나리오 의도적인 toobetter 지원 됩니다. 다중 포리스트 시나리오 아래 hello 그림에 표시 됩니다.

![](./media/hybrid-id-design-considerations/multiforest-multipleAzureAD.png) 

**다중 포리스트 여러 Azure AD 시나리오**

Azure AD Connect 동기화 서버와 Azure AD 디렉터리 간에 유지 되는 1:1 관계 toohave 하지만 조직에 대 한 Azure AD에는 단일 디렉터리는 지원 하지 않는 것이 좋습니다.  Azure AD의 각 인스턴스의 경우 Azure AD Connect의 설치가 필요합니다.  또한 Azure AD를 디자인 하 여 격리 되어 사용자가 Azure AD의 한 인스턴스에서 다른 인스턴스에서 수 toosee 사용자가 됩니다.

수 있으며 하나는 지원 되는 tooconnect 온-프레미스 Active Directory toomultiple Azure AD 디렉터리 아래 hello 그림에 나와 있는 것 처럼의 인스턴스:

![](./media/hybrid-id-design-considerations/single-forest-flitering.png) 

**단일 포리스트 필터링 시나리오**

순서 toodo hello 다음이 충족 되어야 합니다.

* Azure AD Connect Sync 서버가 필터링에 대해 구성되므로 각각 상호 배타적인 개체 집합이 있습니다.  이 예를 들어 각 서버 tooa 특정 도메인 이나 OU 범위를 지정 하 여 수행 합니다.
* 단일에서 DNS 도메인만 등록할 수 있도록 hello hello hello 사용자의 Upn 온-프레미스 AD에서 별도 네임 스페이스를 사용 해야 하는 Azure AD 디렉터리
* 사용자가 Azure AD의 인스턴스를 하나의 해당 인스턴스에서 수 toosee 사용자 수만 있습니다.  가 다른 인스턴스가 hello에 수 toosee 사용자 수
* Exchange를 사용 하도록 설정할 수 hello Azure AD 디렉터리 중 하나에 하이브리드 hello로 온-프레미스 AD
* 상호 배타적 toowrite 다시 적용 됩니다.  이렇게 하면 단일 온-프레미스 구성으로 가정되므로 일부 쓰기 저장 기능이 이 토폴로지로 지원되지 않습니다.  다음 내용이 포함됩니다.
  * 기본 구성으로 쓰기 저장 그룹화
  * 장치 쓰기 저장

Hello 다음은 지원 되지 않으며 구현으로 선택 되지 해야 유의 해야 합니다.

* 개체의 구성 된 toosynchronize 함께 사용할 수 없는 경우에 toohello 동일한 Azure AD 디렉터리를 연결 하는 여러 Azure AD Connect 동기화 서버 집합 지원된 toohave 않습니다.
* 지원 되지 않습니다 toosync hello 동일한 사용자 toomultiple Azure AD 디렉터리입니다. 
* 구성 변경으로 Azure AD tooappear 다른 Azure AD 디렉터리의 연결 하나로 toomake 사용자가 지원 되지 않는 toomake 이기도 합니다. 
* 지원 되지 않는 toomodify Azure AD Connect 동기화 tooconnect toomultiple Azure AD 디렉터리 이기도합니다.
* Azure AD 디렉터리는 설계상 격리되어 있습니다. 요소는 지원 되지 않는 toochange hello 구성 hello 디렉터리 간에 시도 toobuild 일반적이 고 통합 된 전체 주소 목록에서에서 다른 Azure AD 디렉터리에서 Azure AD Connect 동기화 tooread 데이터. 연락처 tooanother 만큼 지원 되지 않는 tooexport 사용자 이기도 온-프레미스 Azure AD Connect 동기화를 사용 하 여 AD 합니다.

> [!NOTE]
> 이 문서에서는 hello 끝점 (Fqdn, IPv4 및 IPv6 주소 범위)를 나열 조직 네트워크에 있는 컴퓨터에서 toohello 인터넷 연결를 제한 하는 경우에 포함 해야 하는 목록 및의 Internet Explorer 신뢰할 수 있는 사이트 영역에 아웃 바운드 허용 클라이언트 컴퓨터 tooensure 컴퓨터에 Office 365를 사용할 수 있습니다. 자세한 내용은 [Office 365 URL 및 IP 주소 범위](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2?ui=en-US&rs=en-US&ad=US)를 읽습니다.
> 
> 

## <a name="define-multi-factor-authentication-strategy"></a>Multi-Factor Authentication 전략 정의
이 작업에서는 다단계 인증 전략 toouse hello를 정의 합니다.  두 가지 다른 버전의 Azure Multi-Factor Authentication이 있습니다.  하나는 클라우드 기반 고 hello 다른 온-프레미스 Azure MFA 서버 hello를 사용 하 여 기반 합니다.  솔루션을 전략에 적절 한 hello는 hello 평가 않은 위의 확인할 수 있습니다 기반으로 합니다.  가장 좋은 디자인 옵션에는 회사의 보안 요구 사항을 충족 시킬 toodetermine 아래 hello 표를 사용 합니다.

Multi-Factor 설계 옵션:

| 자산 toosecure | Hello 클라우드에서 MFA | 온-프레미스에서 MFA |
| --- | --- | --- |
| Microsoft 앱 |yes |yes |
| Hello 응용 프로그램 갤러리에서 SaaS 응용 프로그램 |yes |yes |
| Azure AD 응용프로그램 프록시를 통해 IIS 응용프로그램 게시됨 |yes |yes |
| Hello Azure AD 응용 프로그램 프록시를 통해 게시 되지 않는 IIS 응용 프로그램 |no |yes |
| VPN 및 RDG와 같은 원격 액세스 |no |yes |

전략을 솔루션에 대해 합의 있을 수 있습니다, 경우에 사용자가 있는 위치에 대 한 toouse hello 평가가 위쪽에서 여전히 필요 합니다.  Hello 솔루션 toochange를 않을 수 있습니다.  이러한 사항을 결정할 때는 있습니다 tooassist 아래 hello 표를 사용 합니다.

| 사용자 위치 | 선호하는 설계 옵션 |
| --- | --- |
| Azure Active Directory |Hello 클라우드에서 다중 Authentication |
| Azure AD 및 AD FS로 페더레이션을 사용한 온-프레미스 AD |둘 다 |
| 암호 동기화 없이 Azure AD Connect를 사용하는 Azure AD 및 온-프레미스 AD |둘 다 |
| 암호 동기화와 함께 Azure AD Connect를 사용하는 Azure AD 및 온-프레미스 AD |둘 다 |
| 온-프레미스 AD |Multi-Factor Authentication 서버 |

> [!NOTE]
> 또한 선택한 hello multi-factor authentication 디자인 옵션 디자인에 필요한 hello 기능을 지원 하는지 확인 해야 합니다.  자세한 내용은 [hello multi-factor 보안 솔루션을 선택](../multi-factor-authentication/multi-factor-authentication-get-started.md#what-am-i-trying-to-secure)합니다.
> 
> 

## <a name="multi-factor-auth-provider"></a>Multi-Factor Auth 공급자
다단계 인증은 기본적으로 Azure Active Directory 테넌트가 있는 전역 관리자를 위해 사용할 수 있습니다. 그러나 원하는 사용자의 multi-factor authentication tooall tooextend 하거나 hello 관리 포털, 사용자 지정 인사말, 보고서 등 tooyour 전역 관리자 toobe 수 tootake 이점은 기능이 필요한 경우 다음 구입 하 고 구성 해야 Multi-factor Authentication 공급자입니다.

> [!NOTE]
> 또한 선택한 hello multi-factor authentication 디자인 옵션 디자인에 필요한 hello 기능을 지원 하는지 확인 해야 합니다. 
> 
> 

## <a name="next-steps"></a>다음 단계
[데이터 보호 요구 사항 결정](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md)

## <a name="see-also"></a>참고 항목
[디자인 고려 사항 개요](active-directory-hybrid-identity-design-considerations-overview.md)

