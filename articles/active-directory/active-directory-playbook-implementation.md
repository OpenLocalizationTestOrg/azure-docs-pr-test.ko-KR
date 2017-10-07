---
title: "Active Directory PoC 플레이 북 구현 aaaAzure | Microsoft Docs"
description: "ID 및 액세스 관리 시나리오를 탐색하고 신속하게 구현"
services: active-directory
keywords: "Azure Active Directory, 플레이 북, 개념 증명, PoC"
documentationcenter: 
author: dstefanMSFT
manager: asuthar
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/12/2017
ms.author: dstefan
ms.openlocfilehash: 4d61f1432d5f1c15cd88fda4824cf1c1de64c712
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-implementation"></a>Azure Active Directory 개념 증명 플레이 북: 구현

## <a name="foundation---syncing-ad-tooazure-ad"></a>파운데이션-AD tooAzure AD를 동기화 하는 중 

하이브리드 id에는 대부분의 온-프레미스 디렉터리에 이미 있는 hello 엔터프라이즈 고객에 대 한 hello foundation입니다. hello 여기 ´ ֲ ° toointentionally로 시간이 더 적게 소요 여기 hello 실제 id 및 액세스 시나리오의 가능한 tooshow hello 값으로. 

| 시나리오 | 구성 요소| 
| --- | --- |  
| [온-프레미스 identity toohello 클라우드 확장](#extending-your-on-premises-identity-to-the-cloud) | [디렉터리 동기화 - 암호 해시 동기화](active-directory-playbook-building-blocks.md#directory-synchronization---password-hash-sync-phs---new-installation) <br/>**참고**: Azure AD Connect DirSync/ADSync 또는 이전 버전이 이미 있는 경우 이 단계는 선택 사항입니다. 이 가이드의 일부 시나리오는 최신 버전의 Azure AD Connect가 필요할 수 있습니다.  <br/>[브랜딩](active-directory-playbook-building-blocks.md#branding) | 
| [그룹을 사용하여 Azure AD 라이선스 할당](#assigning-azure-ad-licenses-using-groups) | [그룹 기반 라이선스](active-directory-playbook-building-blocks.md#group-based-licensing) |


### <a name="extending-your-on-premises-identity-toohello-cloud"></a>온-프레미스 identity toohello 클라우드 확장 

1. Bob은 contoso Active Directory 관리자에 게 있습니다. 그는 일련의 사용자에 대 한 서비스로 hello 요구 사항 tooenable id를 가져옵니다. Azure AD Connect 마법사 실행 후 hello hello 클라우드에서 사용할 수 있는 hello 대상 사용자의 id입니다. 
2. Bob 묻고 Susie hello 대상 사용자 중 한 명 tooaccess Azure Active Directory 액세스 패널 hello 그녀 인증할 수 있는지 확인 합니다. Susie는 브랜드가 지정된 로그인 페이지와 향후 응용 프로그램 액세스를 허용할 준비가 되어 있는 빈 액세스 패널을 확인합니다.

### <a name="assigning-azure-ad-licenses-using-groups"></a>그룹을 사용하여 Azure AD 라이선스 할당 

1. Bob hello Azure AD 전역 관리자 이며 hello Azure AD의 초기 배포의 일부로 tooallocate Azure AD 라이선스 tooa 특정 사용자 집합을 원합니다.
2. Bob 파일럿 사용자 hello에 대 한 그룹을 만듭니다. 
3. Hello 라이선스 toohello 그룹을 할당 하는 Bob
4. Susie hello 정보 근로자 중 하나는 자신의 업무의 일환으로 toohello 보안 그룹에 추가 했습니다.
5. 일정 시간이 지난 후 Susie 액세스 toohello Azure AD premium 라이선스가 있습니다. 이렇게 하면 hello POC 시나리오 중 나중에 있습니다.

## <a name="theme---lots-of-apps-one-identity"></a>테마 - 다수의 앱, 하나의 ID

| 시나리오 | 구성 요소| 
| --- | --- |  
| [SaaS 응용 프로그램 통합 - 페더레이션된 SSO](#integrate-saas-applications---federated-sso) | [SaaS 페더레이션된 SSO 구성](active-directory-playbook-building-blocks.md#saas-federated-sso-configuration) <br/>[그룹 - 위임된 소유권](active-directory-playbook-building-blocks.md#groups---delegated-ownership) |
| [SaaS 응용 프로그램 통합 - 암호 SSO](#integrate-saas-applications---password-sso) | [SaaS 암호 SSO 구성](active-directory-playbook-building-blocks.md#saas-password-sso-configuration) |
| [SSO 및 ID 수명 주기 이벤트](#sso-and-identity-lifecycle-events) | [SaaS 및 ID 수명 주기](active-directory-playbook-building-blocks.md#saas-and-identity-lifecycle) |
| [보안 액세스 tooShared 계정](#secure-access-to-shared-accounts) | [SaaS 공유 계정 구성](active-directory-playbook-building-blocks.md#saas-shared-accounts-configuration) |
| [원격 액세스 tooOn 온-프레미스 응용 프로그램 보안](#secure-remote-access-to-on-premises-applications) | [앱 프록시 구성](active-directory-playbook-building-blocks.md#app-proxy-configuration) |
| [LDAP identities tooAzure AD를 동기화 합니다.](#synchronize-ldap-identities-to-azure-ad) |  [일반 LDAP 커넥터 구성](active-directory-playbook-building-blocks.md#generic-ldap-connector-configuration) |

### <a name="integrate-saas-applications---federated-sso"></a>SaaS 응용 프로그램 통합 - 페더레이션된 SSO 

1. Bob hello Azure AD 전역 관리자 이며 hello 마케팅 부서 tooenable 액세스 tootheir ServiceNow 인스턴스에서에서 요청을 받습니다. Bob가 Azure AD 설명서의 단계별 자습서는 hello를 찾아 그 다음에 오는 및 대리자 hello 사용자 toohello 앱 tooKevin, 마케팅 팀의 hello 헤드의 할당 합니다. 
2. Kevin은 ServiceNow 자격의 hello 소유자로 로그인 하 고 Susie toohello 응용 프로그램에 할당 됩니다. Kevin은 Susie의 프로필이 ServiceNow에서 자동으로 생성된 것도 확인합니다.
3. Susie는 hello 마케팅 부서에서 정보 근로자입니다. 그녀 tooazure AD 및 찾습니다 그녀 그 tooin myapps 포털 할당 된 모든 SaaS 응용 프로그램에 기록 합니다. 여기에서 원활 하 게 액세스 tooServiceNow을 가져옵니다 했습니다.
4. hello 마케팅 부서 tooaudit ServiceNow에 액세스 하려고 합니다. Bob은 활동 보고서를 다운로드하여 Kevin과 전자 메일을 통해 공유합니다.  

### <a name="sso-and-identity-lifecycle-events"></a>SSO 및 ID 수명 주기 이벤트

1. Susie 휴가 걸리며 회사 정책에 의해 hello 온-프레미스 AD 계정은 임시 사용 안 함입니다. Susie 지금 로그인 할 수 없는 tooAzure AD와 ServiceNow 액세스할 수 없습니다. 
2. Susie는 tooSales 마케팅에서 측면 방향 이동을 하면 있습니다. Kevin은 그녀의 액세스 권한을 ServiceNow에서 이동합니다. Hello azure ad myapps를 로그인으로 Susie 하 고 hello ServiceNow 타일을 더 이상 발견 됩니다. 10분 후 Kevin은 ServiceNow 관리 콘솔에서 계정이 비활성화되었다고 Susie에게 알려줍니다.

### <a name="integrate-saas-applications---password-sso"></a>SaaS 응용 프로그램 통합 - 암호 SSO

1. Bob은 액세스 tooAtlassian HipChat을 구성합니다. HipChat의 암호 SSO 통합 및 권한 부여 액세스 tooSusie
2. Susie는 toohello myapps 포털에 기록 되 고 링크 toodownload hello 영업 관리자를 다운로드 하는 Azure AD IE 브라우저 확장이 표시
3. 클릭하면 HipChat 사용자 이름 및 암호 자격 증명을 묻는 메시지가 표시됩니다. 이 작업은 일회성 작업 및 액세스 tooHipChat 관련 된 것을 완료 한 후
4. 몇 일이 지난 후 Susie가 myapps 포털을 열어서 HipChat을 다시 클릭합니다. 이번에는 원활하게 액세스합니다.
5. Kevin, hello HipChat 응용 프로그램 소유자 tooaudit hello 응용 프로그램에 액세스 하려고 합니다. Bob이 감사 보고서를 다운로드하여 Kevin과 전자 메일을 통해 공유합니다. 

### <a name="secure-access-tooshared-accounts"></a>보안 액세스 tooShared 계정 

1. Bob은 hello 판매 팀의 멤버에 대 한 보강이 toosecure 공유 hello Twitter 핸들입니다. 그 Twitter SSO 응용 프로그램으로 추가 하 고 hello 판매 팀의 toohello 보안 그룹을 할당 합니다. Hello 자격 증명 toohello 공유 계정 지정 된 하 고 hello 시스템에 제공 했습니다. 
2. Twitter 자격 증명을 공유 하는 toomultiple 사용자 모르게 인해 신뢰할 수 있는 더 이상입니다. Bob 자동 롤오버를 hello Twitter 암호의 수 있습니다.
3. Susie, hello 판매 팀의 멤버인 toohello myapps 포털에 로그인 되 고 링크 toodownload hello Azure AD IE 브라우저 확장을 표시 합니다. 이것을 설치합니다.
4. 그녀는 클릭 하면 get tooTwitter 직접 액세스 합니다. 그녀는 hello 암호를 모릅니다.
5. Arnold는 hello 영업 팀의 일부 이기도 합니다. 그에 관계 없이 동일한 환경을 Susie로 3-4 단계에서 hello
6. hello 판매 부서 tooaudit Twitter에 액세스 하려고 합니다. Bob은 활동 보고서를 다운로드하여 Kevin과 전자 메일을 통해 공유합니다. 

### <a name="secure-remote-access-tooon-premises-applications"></a>원격 액세스 tooOn 온-프레미스 응용 프로그램 보안

1. Bob hello Azure AD 전역 관리자 않았다는 tooenable 직원 tooaccess 몇 가지 유용한 온-프레미스 리소스를 원격으로 작업 하는 동안 hello 비용에 따른 응용 프로그램과 같은 다양 한 요청 됩니다. 그 뒤에 오는 hello [응용 프로그램 프록시 설명서](active-directory-application-proxy-enable.md) tooinstall 커넥터 및 비용에 따른 응용 프로그램 프록시 응용 프로그램으로 게시 합니다. 
2. Bob 원격 액세스 해야 하는 hello 직원 중 Susie을 hello 외부 비용에 따른 응용 프로그램 URL을 공유 합니다. 그녀 hello 링크에 액세스 하 고를 AAD에 대 한 인증 한 후 그녀 되어 수 tooaccess hello 비용에 따른 앱 toobe 생산성 계속 원격으로 작업 시. 
3. Bob은 toopublish 추가 온-프레미스 응용 프로그램을 사용 하 여 동일한 프로세스 및 필요에 따라 액세스 toousers 제공 hello를 계속 합니다. 조건부 액세스 및 hello에 대 한 multi-factor authentication 추가 게시 하는 보다 중요 한 응용 프로그램, tooensure 추가 보안 합니다.

### <a name="synchronize-ldap-identities-tooazure-ad"></a>LDAP identities tooAzure AD를 동기화 합니다.

1. Bob의 회사는 ID 인프라가 복잡합니다. 대부분의 hello 사용자가 내 Windows Server Active Directory 도메인 서비스 (추가)를 유지 관리 됩니다. 그 중 일부는 ADLDS(Active Directory Lightweight Directory Services) 내 HR 시스템에서 관리됩니다.
2. Bob은 모든 사용자 (도 여기에 없는 ADDS)에 대 한 액세스 tooSaaS 앱을 사용 하도록 설정 해야 합니다.
3. Azure AD Connect에서 ADLDS에서 일반 LDAP 커넥터 toopull 데이터를 구성 하는 Bob 합니다.
4. Bob 만들므로 동기화 규칙 LDAP 사용자 메타 버스 및 tooAzure AD로 채워집니다.
5. LDAP 사용자인 Susie가 동기화된 ID를 사용하여 자신의 SaaS에 액세스합니다.



> [!IMPORTANT] 
> 이 작업은 FIM/MIM 사용 경험이 요구되는 고급 구성입니다. 프로덕션에 사용되는 경우 이 구성에 대한 질문이 있으면 [프리미어 지원](https://support.microsoft.com/premier)을 참고하는 것이 좋습니다.



## <a name="theme---increase-your-security"></a>테마 - 보안 향상 

| 시나리오 | 구성 요소| 
| --- | --- |  
| [관리자 계정 액세스 보안](#secure-administrator-account-access) | [전화를 통한 Azure MFA](active-directory-playbook-building-blocks.md#azure-multi-factor-authentication-with-phone-calls) |
| [응용 프로그램에 대한 보안 액세스](#secure-access-to-applications) | [SaaS 응용 프로그램에 대한 조건부 액세스](active-directory-playbook-building-blocks.md#mfa-conditional-access-for-saas-applications) |
| [JIT(Just-In-Time) 관리를 사용하도록 설정](#enable-just-in-time-jit-administration) | [Privileged Identity Management](active-directory-playbook-building-blocks.md#privileged-identity-management-pim) |
| [위험 기반 ID 보호](#protect-identities-based-on-risk) | [위험 이벤트 검색](active-directory-playbook-building-blocks.md#discovering-risk-events) <br/>[로그인 위험 정책 배포](active-directory-playbook-building-blocks.md#deploying-sign-in-risk-policies) |
| [인증서 기반 인증을 사용하여 암호 없이 인증](#authenticate-without-passwords-using-certificate-based-authentication) | [인증 기반 인증서 구성](active-directory-playbook-building-blocks.md#configuring-certificate-based-authentication)

### <a name="secure-administrator-account-access"></a>관리자 계정 액세스 보안

1. Bob는 hello Azure AD 전역 관리자입니다. 그는 hello 서비스의 공동 관리자로 Stuart 확인 했습니다. 
2. Bob은 tooalways MFA tooimprove hello 보안 상태를 요구 하는 Stuart의 계정 구성
3. Stuart 로그인 toohello Azure 포털 및 tooregister 야 한다는 알림이 자신의 전화 번호 toocontinue hello 로그인
4. 후속 로그인 Stuart에서 다단계 인증으로 보호 됨 및 이제를 받고 전화 통화 tooverify 하 여 해당 id입니다.

### <a name="secure-access-tooapplications"></a>보안 액세스 tooapplications

1. Kevin은 ServiceNow hello 비즈니스 소유자를입니다. 이제 hello 회사 외부 hello 회사 네트워크에 액세스할 때 MFA 사용 하는 해당 사용자가 toologin를 원합니다.
2. Bob이 Azure AD 전역 관리자는 조건부 액세스 정책 toohello ServiceNow 응용 프로그램 tooenable MFA 외부 액세스에 대 한 추가
3. Susie, 우리의 정보 근로자 내 앱 포털에 로그인 하 고 hello ServiceNow 타일을 클릭 합니다. 그녀에게 이제 MFA가 요구됩니다.

### <a name="enable-just-in-time-jit-administration"></a>JIT(Just-In-Time) 관리를 사용하도록 설정

1. Bob과 Stuart는 Azure AD 전역 관리자입니다. 또한 hello hello 사용량 tookeep 레코드의 권한 있는 역할 및 tooenable JIT 액세스 toohello 관리 역할 하려고 합니다.
2. Bob PIM hello Azure AD 테 넌 트에 있으며 특정 hello 보안 관리자가 됩니다. 영구 tooeligible를에서 자신 및 Stuart의 전역 관리자 역할 멤버 자격 둘 다 변경 합니다.
3. Bob과 Stuart의 tooAzure AD 변경 하나를 실행 하기 전에 hello Azure 포털을 통해 해당 역할을 활성화 필요 지금 구성 합니다. 

### <a name="protect-identities-based-on-risk"></a>위험 기반 ID 보호 

1. 정보 근로자 Susie가 Tor 브라우저에서 로그인을 시도합니다. 
2. Hello Azure AD identity protection 대시보드를 확인 하 고 익명 IP 주소에서 Susie의 로그인에 게 표시 하는 Bob. hello 보안 팀에서 이러한 toochallenge MFA 사용자가 액세스 하려는 경우
3. Bob 보통 또는 높은 위험 이벤트에 대 한 Azure AD Identity Protection 정책 toochallenge MFA를 사용 하도록 설정
4. 시간이 지나고 Susie가 Tor 브라우저에서 다시 로그인합니다. 이 이번에 그녀 나타납니다 hello MFA 챌린지

### <a name="authenticate-without-passwords-using-certificate-based-authentication"></a>인증서 기반 인증을 사용하여 암호 없이 인증

1. Bob은 응용 프로그램에 대한 인증 요소로 암호 사용을 금지하는 금융 기관의 전역 관리자입니다.
2. Bob이 ADFS 및 Azure AD에서 인증서 인증을 강제 적용합니다.
3. 이 응용 프로그램에 액세스 하는 동안 Susie tooauthenticate 인증서를 사용 하 라는 메시지가 표시

## <a name="theme---scale-with-self-service"></a>테마 - 셀프 서비스에 맞게 크기 조정

| 시나리오 | 구성 요소| 
| --- | --- |  
| [셀프 서비스 암호 재설정](#self-service-password-reset) | [셀프 서비스 암호 재설정](active-directory-playbook-building-blocks.md#self-service-password-reset) |
| [셀프 서비스 액세스 tooApplications](#self-service-access-to-applications) | [셀프 서비스 액세스 tooApplications](active-directory-playbook-building-blocks.md#self-service-access-to-application-management) |

### <a name="self-service-password-reset"></a>셀프 서비스 암호 재설정 

1. Bob은 hello Azure AD 전역 관리자 및 사용 셀프 서비스 암호 관리 tooa 하위 집합 Susie 하 여 사용자. 
2. Susie toomyapps 포털 및 메시지 tooregister 참조에 그녀의 보안 정보에 대 한 로그가 이후 암호 다시 설정 이벤트입니다.
3. 며칠이 지나서 Susie가 암호를 잊어버리고 Azure AD 포털을 통해 암호를 재설정합니다.

### <a name="self-service-access-tooapplications"></a>셀프 서비스 액세스 tooApplications 

1. Kevin은 ServiceNow hello 비즈니스 소유자를입니다. 사용자가 너무 "등록"에 대 한 한 번에 모두 추가 하는 대신 필요에 따라 원하는
2. Hello ServiceNow 응용 프로그램 tooenable를 수정 하는 Bob, Azure AD 전역 관리자는 셀프 서비스 요청
3. Susie, 우리의 정보 근로자가 내 앱 포털에 로그인 하 고 클릭 "더 많은 응용 프로그램 추가" 단추 hello 및 응용 프로그램을 권장 하는 hello 중 하나로 ServiceNow를 참조 하십시오. 그런 다음 그녀 백 toomy 앱 포털 탐색 하 고 hello ServiceNow 응용 프로그램을 참조 하십시오.

[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]