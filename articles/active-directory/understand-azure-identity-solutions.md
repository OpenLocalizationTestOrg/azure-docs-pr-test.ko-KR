---
title: Azure Id aaaUnderstand | Microsoft Docs
description: "Microsoft Azure identity 솔루션 용어, 개념 및 결정에 대 한 있습니다 toomake hello 최상의 identity 거 버 넌 스 조직에 대 한 권장 사항에 대 한 기본적인 이해를 가져옵니다."
keywords: 
author: jeffgilb
manager: femila
ms.reviewer: jsnow
ms.author: jeffgilb
ms.date: 7/17/2017
ms.topic: article
ms.prod: 
ms.service: azure
ms.technology: 
ms.assetid: 
ms.custom: it-pro
ms.openlocfilehash: 4d9c90bd7a6bcc9637be3107998f9da5bd4cbdae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-identity-solutions"></a>Azure ID 솔루션 이해
Microsoft Azure AD(Azure Active Directory)는 디렉터리 서비스, ID 관리 및 응용 프로그램 액세스 관리를 제공하는 ID 및 액세스 관리 클라우드 솔루션입니다. Azure AD 신속 하 게 [single sign-on (SSO)를 사용 하면](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-sso) too1, hello에서 미리 통합 된 상용 및 사용자 지정 앱의 000 [Azure AD 응용 프로그램 갤러리](https://azure.microsoft.com/marketplace/active-directory/all/)합니다. 이러한 앱은 대부분 Office 365, Salesforce.com, Box, ServiceNow 및 Workday와 같이 이미 사용하고 있는 앱들입니다.

단일 Azure AD 디렉터리가 만들어질 때 자동으로 Azure 구독과 연결됩니다. Azure의 hello id 서비스,으로 다음 Azure AD 클라우드 기반 리소스에 대 한 모든 id 관리 및 액세스 제어 기능을 제공합니다. 이러한 리소스 다음과 사용자, 앱 및 그룹은 개별 테 넌 트 (조직)에 대 한 hello 다음 다이어그램에에서 나와 있는 것 처럼:

![Azure Active Directory](./media/understand-azure-identity-solutions/azure-ad.png)

Microsoft Azure를 제공 하며 제공 여러 가지 방법으로 tooleverage identity (IDaaS) 서비스로 다양 한 수준의 복잡성 toomeet 개별 조직 요구 합니다. 이 문서의 나머지 부분 hello는 하면 toomake hello 적합 하 고 hello 사용 가능한 옵션에서에 대 한 권장 사항 뿐만 아니라 기본적인 Azure id 용어 및 개념 이해 하도록 도와 줍니다.

## <a name="terms-tooknow"></a>용어 tooknow

조직에 Azure id 솔루션에서 결정할 수 있습니다, 전에 Azure id 서비스에 대해 이야기 하는 경우에 주로 사용 하는 hello 용어에 대 한 기본적인 이해를 해야 합니다.

|용어 tooknow| 설명|
|-----|-----|
|Azure 구독 |구독이 Azure 클라우드 서비스에 대 한 사용 되는 toopay 이므로 일반적으로 연결 된 tooa 신용 카드 있습니다. 여러 구독을 갖지만 구독 간 리소스 tooshare 어려울 수 있습니다.|
|Azure 테넌트 | Azure AD 테넌트는 단일 조직을 대표합니다. 조직이 Azure, Intune 또는 Office 365와 같은 Microsoft 클라우드 서비스 구독에 등록할 때 자동으로 생성되는 Azure AD의 신뢰할 수 있는 전용 인스턴스입니다. 테 넌 트 액세스 tooservices는 전용된 환경 (단일 테 넌 트) 또는 (다중 테 넌 트) 다른 조직과 공유 환경에서 얻을 수 있습니다.|
|Azure AD Directory | 각 Azure 테 넌 트는 전용, 신뢰할 수 있는 Azure AD 디렉터리 hello 테 넌 트의 사용자, 그룹 및 응용 프로그램을 포함 하는 합니다. 되기 테 넌 트 리소스에 대 한 사용 되는 tooperform id 및 액세스 관리 기능. 때문에 고유한 Azure AD 디렉터리가 자동으로 프로 비전 된 toorepresent Azure, Microsoft Intune 또는 Office 365와 같은 Microsoft 클라우드 서비스에 등록할 때는 조직, 경우에 따라 표시 hello 용어 *테 넌 트*, *Azure AD*, 및 *Azure AD 디렉터리* 같은 의미로 사용 됩니다. |
|사용자 지정 도메인 | 먼저 Microsoft 클라우드 서비스 구독에 등록할 때 테넌트(조직)에서는 *.onmicrosoft.com* 도메인 이름을 사용합니다. 그러나 대부분의 조직에는 사용 되는 toodo] 및 [최종 사용자가 tooaccess 회사 리소스 사용 하나 이상의 도메인 이름을 갖습니다. 않도록 hello 도메인 이름을 친숙 한 tooyour 사용자와 같은 사용자 지정 도메인 이름을 tooAzure AD를 추가할 수 있습니다  *alice@contoso.com*  대신  *alice@contoso.onmicrosoft.com* 합니다. |
|Azure AD 계정 | Azure AD 또는 Office 365와 같은 다른 Microsoft 클라우드 서비스를 사용하여 만들어진 ID입니다. Azure AD에 저장 하 고 액세스 가능한 tooany hello 조직의 클라우드 서비스 구독입니다. |
|Azure 구독 관리자| 계정 관리자에 게는 hello 사용자에 등록 또는 hello Azure 구독을 구입한입니다. Hello 사용 하 여 [r e 계정 센터](https://account.windowsazure.com/Home/Index) 구독을 만들고, 구독 취소, 구독에 대 한 hello 청구 변경, 변경 등의 다양 한 관리 작업 tooperform hello 서비스 관리자. |
|Azure AD 전역 관리자 | Azure AD 전역 관리자는 모든 권한 tooall Azure AD 관리 기능이 있습니다. Microsoft 클라우드 서비스 구독에 대 한 자동으로 등록 hello 사람이는 기본적으로 전역 관리자가 됩니다. 둘 이상의 전역 관리자를 가질 수 있지만 전역 관리자에 할당 [다른 관리자 역할 hello](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal) toousers 합니다. |
|Microsoft 계정 | Microsoft 계정 (개인적인 용도로 사용자가 만든) 액세스 tooconsumer 지향 Microsoft 제품을 제공 하 고 클라우드 서비스 (Hotmail) Outlook, OneDrive, Xbox LIVE, 또는 Office 365와 같은 합니다. 이러한 id는 생성 되 고 hello Microsoft에서 실행 하는 Microsoft 소비자 id 계정 시스템에에서 저장 합니다.|
|회사 또는 학교 계정 | (비즈니스/교육용 사용 하기 위해 관리자가 실행) 하는 회사 또는 학교 계정은 tooenterprise 비즈니스 수준 같은 Microsoft 클라우드 서비스, Azure, Intune 또는 Office 365 액세스를 제공 합니다.|


## <a name="concepts-toounderstand"></a>개념 toounderstand

이제 hello Azure id 기본 용어를 알고 해야 배웁니다 이러한에 대 한 자세한 정보 받을된 Azure id 서비스 결정을 내릴 수 있도록 Azure id 개념입니다.

|개념 toounderstand |설명|
|-----|-----|
|[Azure 구독과 Azure Active Directory의 연관 관계](https://docs.microsoft.com/azure/active-directory/active-directory-how-subscriptions-associated-directory) |모든 Azure 구독에 트러스트 관계를 Azure AD 디렉터리 tooauthenticate 사용자, 서비스 및 장치입니다. *여러 구독 hello 동일한 Azure AD 디렉터리를 트러스트할 수 있지만 구독에서 단일 신뢰만 Azure AD 디렉터리*합니다. 구독에 보다 가깝습니다 구독의 자식 리소스가 다른 Azure 리소스 (웹 사이트, 데이터베이스 및 등)와 hello 관계와 달리이 트러스트 관계가입니다. 구독이 만료 되는 경우 다음 Azure AD 이외의 hello 구독과 연결 된 액세스 tooresources 또한 중지 됩니다. 그러나 hello Azure AD 디렉터리 해당 디렉터리와 다른 구독을 연결 하 고 toomanage 테 넌 트 리소스를 계속할 수 있도록 azure에서 유지 됩니다.|
|[Azure AD 라이선스 작동 방식](https://docs.microsoft.com/azure/active-directory/active-directory-licensing-get-started-azure-portal) | 구매 또는 Enterprise Mobility Suite, Azure AD Premium 또는 Azure AD Basic에서는 디렉터리 활성화 hello 구독에서 유효 기간을 포함 하 여 업데이트 되 고 선불 라이선스. Hello 구독 옵션이 활성화 되 면 hello 서비스를 Azure AD 전역 관리자가 관리 하 고 사용이 허가 된 사용자가 사용할 수 있습니다. 구독 정보를 사용할 수 없거나 할당 된 라이선스의 hello 번호를 포함 하는 hello hello에서 Azure 포털에서에서 사용할 수 있는 **Azure Active Directory** > **라이선스** 블레이드입니다. 또한 가장 좋은 곳 toomanage 라이선스 할당 hello는이 합니다.|
|[Hello Azure 포털의에서 역할 기반 액세스 제어](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is)|Azure RBAC(역할 기반 액세스 제어)를 통해 Azure 리소스에 대한 세밀한 액세스 관리를 제공할 수 있습니다. 너무 많은 권한을 노출 하 고 tooattackers 계정 수 있습니다. 권한이 너무 적으면 직원이 업무를 효율적으로 수행할 수 없습니다. RBAC를 사용 하 여 권한을 부여할 수도 있습니다 직원 hello 정확한 필요한 tooall 리소스 그룹에 적용 되는 세 가지 기본 역할에 따라: 소유자, 참가자, 판독기입니다. Too2, 자신만의 000 만들 수 있습니다 [사용자 지정 RBAC 역할](https://docs.microsoft.com/azure/active-directory/role-based-access-control-custom-roles) toomeet 특정 필요 합니다. |
|[하이브리드 ID](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)|하이브리드 ID는 [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)를 사용하는 Azure AD에서 온-프레미스 AD DS(Windows Server Active Directory)를 통합하여 이뤄집니다. 이렇게 하면 Azure AD와 통합 하 여 사용자가 Office 365, Azure 및 온-프레미스 앱 또는 SaaS 응용 프로그램에 대 한 일반 id tooprovide 있습니다. 하이브리드 id 사용 하면 효율적으로 확장할 온-프레미스 환경 toohello 클라우드 id 및 액세스에 대 한 합니다.|

### <a name="hello-difference-between-windows-server-ad-ds-and-azure-ad"></a>Windows Server AD DS와 Azure AD의 hello 차이
Azure AD(Azure Active Directory)와 온-프레미스 Active Directory(Active Directory 도메인 서비스 또는 AD DS)는 디렉터리 데이터를 저장하고 사용자와 리소스 간의 통신(사용자 로그온 프로세스, 인증 및 디렉터리 검색 포함)을 관리하는 시스템입니다.

이미 온-프레미스 Windows Server Active Directory 도메인 서비스 (AD DS)에 대해 잘 알고 있다면 처음 도입 된 Windows 2000 Server hello id 서비스의 기본 개념을 이해할 것 합니다. 그러나 Azure AD hello 클라우드에서 도메인 컨트롤러가 아닌지 중요 toounderstand 이기도 합니다. 생각 toofully 변경을 인식 클라우드 기반 기능를 완전히 새로운 방식으로 하며 최신 위협 으로부터 조직을 보호 하는 Azure에서 identity (IDaaS) 서비스로 제공 하는 완전히 새로운 방법입니다. 

AD DS는 Windows Server의 서버 역할로, 물리적 컴퓨터 또는 가상 컴퓨터에 배포할 수 있습니다. 또한 X.500 기반 계층 구조를 갖습니다. DNS를 사용하여 개체를 찾고, LDAP를 사용하여 상호 작용할 수 있으며 인증에는 Kerberos를 주로 사용합니다. Active Directory 사용 하면 조직 구성 단위 (Ou) 및 그룹 정책 개체 (Gpo) 또한 toojoining 컴퓨터 toohello 도메인 및 트러스트 만들어집니다 도메인 간에 합니다.

IT는 AD DS를 사용하여 몇 년 간 자신의 보안 경계를 보호했지만 경계 없는 기업 지원 ID에는 직원, 고객 및 파트너에게 새로운 컨트롤 평면이 필요합니다. Azure AD는 ID 제어 평면입니다. 보안 hello 회사 방화벽 toohello 클라우드 Azure AD 사용자에 대 한 하나의 일반적인 id를 제공 하 여 회사 리소스 및 액세스를 보호 위치 밖으로 이동 했기 (온-프레미스 또는 클라우드에서 hello). 이렇게 하면 사용자가 hello 유연성 toosecurely 프로그램 tooget 거의 모든 장치에서 자신의 업무 필요한 액세스 hello 앱 있습니다. 기계 학습 기능 및 심층 분석 보고 원활한 위험 기반 데이터 보호 컨트롤과 해당 IT 요구 tookeep 회사 데이터의 보안도 제공 됩니다.

Azure AD는 다중 고객 공용 디렉터리 서비스이므로, Azure AD 내에서 클라우드 서버 및 응용 프로그램에 대해 Office 365와 같은 테넌트를 만들 수 있습니다. 사용자 및 그룹은 OU나 GPO 없는 플랫 구조로 만들어집니다. 인증은 SAML, WS-Federation 및 OAuth와 같은 프로토콜을 통해 수행됩니다. 가능한 tooquery Azure AD 있지만 LDAP를 사용 하는 대신 AD Graph API를 호출 하는 REST API를 사용 해야 합니다. 이러한 모든 기능은 HTTP 및 HTTPS를 통해 작동합니다.

### <a name="extend-office-365-management-and-security-capabilities"></a>Office 365 관리 및 보안 기능 확장
이미 Office 365를 사용하고 있나요? 전체 직원에 대 한 보안 생산성을 사용 하면 리소스에 Azure AD toosecure 사용 하는 기본 제공 Office 365 기능을 확장 하 여 여 디지털 변환에을 가속화할 수 있습니다. Azure AD를 사용 하는 경우 또한 tooOffice 365 기능을 보호할 수 있습니다 single sign on 모든 앱에 대 한 수 있도록 하는 하나의 id와 전체 응용 프로그램 포트폴리오. 장치 상태, 사용자, 위치, 응용 프로그램 및 위험에 기반하여 조건부 액세스 기능을 확장할 수 있습니다. MFA(Multi-Factor Authentication) 기능은 필요할 때 더 많은 보호를 제공합니다. 사용자 권한을 추가로 감시하고 주문형 Just-In-Time 관리 액세스를 제공합니다. 사용자에 게 생산성을 높이도록 되며 더 적은 기술 지원팀 티켓을 만들, 감사 toohello 셀프 서비스 기능은 Azure AD 응용 프로그램 액세스 요청을 잊어버린된 암호 다시 설정 및 그룹 만들기 및 관리와 같은 제공 합니다.

> [!TIP]
> Office 365와 Azure AD id 관리를 사용 하는 방법에 대 한 자세한 toolearn를 선택 하십시오. [Hello 전자책 가져오기](https://info.microsoft.com/Extend-Office-365-security-with-EMS.html)합니다.

## <a name="microsoft-azure-identity-solutions"></a>Microsoft Azure ID 솔루션

Microsoft Azure에서는 여러 가지 방법으로 toomanage 사용자의 id 유지 관리 됩니다 있는지 여부를 완벽 하 게 온-프레미스에만 클라우드에 hello 또는 위치 사이 있습니다. 이러한 옵션에는 Azure의 DIY(do-it-yourself) AD DS, Azure AD(Azure Active Directory), 하이브리드 ID 및 Azure AD Domain Services가 포함됩니다.

### <a name="do-it-yourself-diy-ad-ds"></a>DIY(do-it-yourself) AD DS
Hello 클라우드에서 적은 공간만 사용만 필요로 하는 회사에 대 한 **자체 (DIY) AD DS** Azure에서 사용할 수 있습니다. 이 옵션은 Azure에서 가상 컴퓨터(VM)로 배포하기에 적합한 많은 Windows Server AD DS 시나리오를 지원합니다. 예를 들어 도메인 컨트롤러는 원격 네트워크에 연결 된 toohello 먼 데이터 센터에서 실행 중인 Azure VM을 만들 수 있습니다. 여기에서 hello VM 수 toosupport 원격 사용자 로부터의 인증 요청 고 하면 인증 성능이 향상 됩니다. 이 옵션은 적은 수의 도메인 컨트롤러와 Azure에서 단일 가상 네트워크를 호스트 하 여 비용이 비교적 낮기 대체 toootherwise 비용이 많이 드는 재해 복구 사이트로 적합도 합니다. 마지막으로, 회사 Windows Server Active Directory hello 또는 toodeploy가 Windows Server AD DS 필요 하지만 hello 온-프레미스 네트워크에 대 한 종속성 없이 SharePoint와 같은 Azure에서 응용 프로그램 필요 수 있습니다. 이 경우 Azure toomeet hello SharePoint 서버 팜 요구 사항에 분리 된 포리스트를 배포할 수 있습니다. 연결 toohello 온-프레미스 네트워크 필요 toodeploy 네트워크 응용 프로그램 통해서도 및 hello 온-프레미스 Active Directory 합니다.

### <a name="azure-active-directory-azure-ad"></a>Azure AD(Azure Active Directory)
**Azure AD 독립 실행형**은 완전한 클라우드 기반 IDaaS(Identity and access management as a Service) 솔루션입니다. Azure AD 기능 toomanage 사용자 및 그룹의 강력한 집합을 제공합니다. 보안 액세스 tooon 온-프레미스 및 클라우드 응용 프로그램, saas () 응용 프로그램으로 Office 365 및 많은 타사 소프트웨어와 같은 Microsoft 웹 서비스를 포함 하 여 수 있습니다. Azure AD는 Free, Basic 및 Premium의 세 가지 버전으로 제공됩니다. Azure AD는 조직이 효율성 증폭 하 고 고급 보안 기능 hello 경계 방화벽 tooa 새 컨트롤 평면 Azure 기계 학습에서 보호 되 고 다른 이상의 보안을 확장 합니다.

### <a name="hybrid-identity"></a>하이브리드 ID
온-프레미스 또는 클라우드 기반 id 솔루션으로 사용할지를 보다는 많은 정방향 생각 Cio 및 장기적으로 사용 되는 회사의 예측을 시작 했습니다는 비즈니스를 확장 하는 온-프레미스 통해toohello클라우드디렉터리**하이브리드 id** 솔루션입니다. 하이브리드 id를 사용 하 여 글로벌 id를 가져오고 toohello 응용 프로그램 사용자가 안전 하 고 생산성에 대 한 액세스를 제공 하는 액세스 관리 솔루션 toodo 자신의 작업을 필요 합니다.

> [!TIP]
> 에 대해 더 알아봅니다 toolearn 계산 방법 Cio가 Azure Active Directory는 IT 전략의 가장 중요 한 부분은 다운로드 hello [CIO의 가이드 tooAzure Active Directory](https://aka.ms/AzureADCIOGuide)합니다.

### <a name="azure-ad-domain-services"></a>Azure AD Domain Services
**Azure AD 도메인 서비스** 네트워크 응용 프로그램 개발 및 테스트에 대 한 간단한 Azure VM 구성 제어 및 방법은 toomeet에 대 한 AD DS는 클라우드 기반 옵션 toouse 온-프레미스 id 요구 사항을 제공 합니다. Azure AD 도메인 서비스 toolift 다루지는지 않습니다 고 온-프레미스 AD DS 인프라 tooAzure Vm이 Azure AD 도메인 서비스에서 관리 합니다. 대신, hello Azure Vm 관리 되는 도메인에 사용 되는 toosupport hello 개발, 테스트 및 AD DS 인증 방법 toohello 클라우드를 필요로 하는 온-프레미스 응용 프로그램의 이동 해야 합니다.

## <a name="common-scenarios-and-recommendations"></a>일반적인 시나리오 및 권장 사항

Toowhich Azure id 옵션 각각에 대해 가장 적합 한 수 있으므로 권장 사항이 포함 된 몇 가지 일반적인 id 및 액세스 시나리오 다음과 같습니다.

|ID 시나리오| 권장 사항|
|-----|-----|
|내 조직에 대규모 투자에서 온-프레미스 Windows Server Active Directory, 했지만 tooextend identity toohello 클라우드 주시기 바랍니다.| 가장 널리 사용 되는 hello Azure id 솔루션은 [하이브리드 id](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview)합니다. 이미 만든 경우 투자 온-프레미스에서 AD DS, Azure AD Connect를 사용 하 여 identity toohello 클라우드를 쉽게 확장할 수 있습니다.|
|Hello 클라우드에서 비즈니스 탄생 했으며 하며 없는 투자 온-프레미스 id 솔루션에 있습니다.| [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) hello 적합 하지 않은 클라우드 전용 기업에 온-프레미스 투자 합니다.|
|응용 프로그램 개발 및 테스트에 대 한 간단한 Azure VM 구성 및 제어 toomeet 온-프레미스 id 요구 사항 필요합니다.|[Azure AD 도메인 서비스](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-overview) 간단한 Azure VM 구성 컨트롤에 대 한 AD DS toouse 필요 하거나 toodevelop 찾고 하거나 마이그레이션하는 경우 레거시, 디렉터리 인식 온-프레미스 응용 프로그램 toohello 클라우드 경우이 좋은 대안입니다.|  
|Azure에서 가상 컴퓨터를 몇 가지 toosupport 필요 한가요 하지만 회사는 여전히 과도 하 게 온-프레미스 Active Directory (AD DS)에 집중 합니다.|사용 하 여 [DIY AD DS](https://msdn.microsoft.com/library/azure/jj156090.aspx) toouse toosupport 몇 가지 가상 컴퓨터가 있어야 하 고 큰 AD DS 투자 온-프레미스에서 Azure Vm입니다. |

## <a name="where-can-i-learn-more"></a>자세한 내용을 알아보려면 어떤 정보를 참조해야 하나요?
모든 Azure AD에 대 한 자세한 내용은 유용한 리소스 온라인 toohelp 거죠를 개가 있습니다. 시작한 훌륭한 문서 tooget 목록은 다음과 같습니다.

* [Azure AD Connect를 사용하여 디렉터리를 하이브리드로 관리](active-directory-aadconnect.md)
* [연결된 적이 있는 세계에 대한 추가 보안](../multi-factor-authentication/multi-factor-authentication.md)
* [사용자 프로 비전 및 프로 비전 해제 tooSaaS Azure Active Directory와 응용 프로그램 자동화](active-directory-saas-app-provisioning.md)
* [Azure AD Reporting 시작](active-directory-reporting-getting-started.md)
* [어디에서나 암호 관리](active-directory-passwords.md)
* [Azure Active Directory로 응용 프로그램 액세스 및 Single Sign-On이란 무엇입니까?](active-directory-appssoaccess-whatis.md)
* [사용자 프로 비전 및 프로 비전 해제 tooSaaS Azure Active Directory와 응용 프로그램 자동화](active-directory-saas-app-provisioning.md)
* [어떻게 tooprovide 보안 원격 액세스 tooon 온-프레미스 응용 프로그램](active-directory-application-proxy-get-started.md)
* [Azure Active Directory 그룹을 사용 하 여 액세스 tooresources 관리](active-directory-manage-groups.md)
* [Microsoft Azure Active Directory 라이선스란?](active-directory-licensing-what-is.md)
* [조직 내에서 사용되고 있는 허용되지 않은 클라우드 앱을 검색하는 방법](active-directory-cloudappdiscovery-whatis.md)

## <a name="next-steps"></a>다음 단계

Azure id 개념과 hello 옵션 사용 가능한 tooyou를 이해 했으므로 hello 리소스 시작 tooget 구현 hello 옵션 선택 했으면 다음을 사용할 수 있습니다.

[Azure 하이브리드 ID 솔루션에 대한 자세한 정보](https://docs.microsoft.com/azure/active-directory/choose-hybrid-identity-solution)

[개념 환경의 Azure 증명에 대한 자세한 정보](https://aka.ms/aad-poc)

[프로덕션에서 Azure AD 배포](https://aka.ms/aad-onboard)
