Id를 관리할은 중요 hello 공용 클라우드에서 온-프레미스에서 그대로 있습니다. 이 toohelp, Azure는 여러 가지 다른 클라우드 identity 기술을 지원합니다. 대표적인 옵션은 다음과 같습니다.

* Hello 클라우드의 Azure 가상 컴퓨터를 사용 하 여 만든 가상 컴퓨터를 사용 하 여 Windows Server Active Directory (일반적으로 AD 방금 라고 함)를 실행할 수 있습니다. 이 방법을 합리적 tooextend Azure를 사용 하는 경우 온-프레미스 데이터 센터 hello 클라우드로입니다.
* 사용자가 single sign on 너무 toogive Azure Active Directory를 사용할 수 있습니다[Saas ()으로 소프트웨어](https://azure.microsoft.com/overview/what-is-saas/) 응용 프로그램입니다. 이 기술은 Microsoft Office 365에서 사용되며, Azure 또는 기타 클라우드 플랫폼에서 실행하는 응용 프로그램에서도 이 기술을 사용할 수 있습니다.
* Hello에서 실행 중인 응용 프로그램 클라우드 또는 온-프레미스 Azure Active Directory 액세스 제어 toolet 사용자가 Facebook, Google, Microsoft 및 기타 id 공급자의 id를 사용 하 여 로그인을 사용할 수 있습니다.

이 문서에서는 이러한 세 가지 옵션을 모두 설명합니다.

## <a name="table-of-contents"></a>목차
* [가상 컴퓨터에서 Windows Server Active Directory 실행](#adinvm)
* [Azure Active Directory 사용](#ad)
* [Azure Active Directory 액세스 제어 사용](#ac)

## <a name="adinvm"></a>가상 컴퓨터에서 Windows Server Active Directory 실행
Azure 가상 컴퓨터에서 Windows Server AD를 실행하는 것은 온-프레미스에서 실행하는 것과 비슷합니다. [그림 1](#fig1) 은 일반적인 실행 예시를 보여 줍니다.

![가상 컴퓨터 내의 Azure Active Directory](./media/identity/identity_01_ADinVM.png)

<a name="Fig1"></a>그림 1: Windows Server Active Directory가 Azure 가상 네트워크를 사용 하 여 연결 된 Azure 가상 컴퓨터 tooan 조직의 온-프레미스 데이터 센터에서 실행할 수 있습니다.

Hello이 예제에서는 Windows Server AD hello 플랫폼 IaaS 기술 Azure 가상 컴퓨터를 사용 하 여 만든 Vm에서 실행 됩니다. 이러한 Vm 및 기타 Azure 가상 네트워크를 사용 하 여 연결 된 가상 네트워크 tooan 온-프레미스 데이터 센터도 그룹화 됩니다. 확장 가상 사설망 (VPN) 연결을 통해 온-프레미스 네트워크 hello 상호 작용 하는 클라우드 가상 컴퓨터의 그룹 hello 가상 네트워크를 제거 합니다. 이러한 Azure 가상 컴퓨터 수행이에서는 또 다른 서브넷 toohello 온-프레미스 데이터 센터 같이 표시 됩니다. Hello 그림에서 볼 수 있듯이 해당 Vm의 두 실행 하 고 Windows Server AD 도메인 컨트롤러. hello hello 가상 네트워크의 다른 가상 컴퓨터 실행 중일 수 등과 같이 응용 프로그램, SharePoint, 개발 및 테스트와 같은 다른 방법으로 사용 되 고. 또한 hello 온-프레미스 데이터 센터에는 두 명의 Windows Server AD 도메인 컨트롤러 실행 중입니다.

가지 hello 클라우드로 온-프레미스에서 실행 하는 것의 연결 hello 도메인 컨트롤러에 대 한 몇 가지 옵션이 있습니다.

* 모든 도메인 컨트롤러를 단일 Active Directory 도메인에 할당할 수 있습니다.
* 별도 AD 도메인 온-프레미스의 만들기 및 hello의 일부인 hello 클라우드에서 동일한 포리스트에 있습니다.
* AD 포리스트가 있음 별도 hello 클라우드 및 온-프레미스에서 작성 한 다음 hello 포리스트 간 포리스트 트러스트 또는 Windows Server Active Directory Federation Services (AD FS) Azure에서 가상 컴퓨터에서 실행할 수도 있는 사용 하 여 연결 합니다.

어떤 방법을 선택 이루어집니다, 그리고 관리자가 온-프레미스 사용자의 인증 요청 필요한 경우에 toocloud 도메인 컨트롤러를 만들기 때문 hello 링크 toohello 클라우드는 온-프레미스 네트워크 보다 속도가 느립니다 가능성이 toobe 있는지 확인 해야 합니다. 연결 된 클라우드 및 온-프레미스 도메인 컨트롤러에서 다른 요소 tooconsider는 복제에 의해 발생 하는 hello 트래픽입니다. Hello 클라우드의 도메인 컨트롤러는 일반적으로 관리자 tooschedule 얼마나 자주 복제가 이루어집니다 수 있는 자체 AD 사이트에서. Azure 데이터 센터 외부로 전송 되지 바이트에 대 한 hello 관리자의 복제 선택 항목에 영향을 줄 수 있는으로 전송 되지만 트래픽에 대 한 요금이 청구 됩니다. Azure에서도 자체 DNS(도메인 이름 서비스)를 지원합니다. 다만 이 서비스에는 Active Directory에서 필요한 기능(동적 DNS 및 SRV 레코드 지원)이 빠져있습니다. 이 때문에 Azure에서 Windows Server AD를 실행 하려면 hello 클라우드에서 사용자 고유의 DNS 서버를 설정 합니다.

다양한 상황에서 Azure VM에서 Windows Server AD를 실행하는 것이 적합할 수 있습니다. 다음은 몇 가지 예입니다.

* Azure 가상 컴퓨터를 자체 데이터 센터의 확장으로 사용 하는 경우에 로컬 도메인 컨트롤러 toohandle 등 Windows 통합 인증 요청 또는 LDAP 쿼리를 필요로 하는 hello 클라우드에서 응용 프로그램을 실행할 수 있습니다. Active Directory와 SharePoint 자주 예를 들어 상호 작용 및 하므로 가능한 toorun 온-프레미스 디렉터리를 사용 하 여 Azure에 SharePoint 팜을 상태인 동안 hello 클라우드에서 도메인 컨트롤러 설정 크게 성능이 향상 됩니다. 하지만 (되지 않는다고 반드시 필요 중요 한 toorealize, 충분 한 응용 프로그램의 클라우드에서 온-프레미스 도메인 컨트롤러만 사용 하 여 hello 성공적으로 실행 됩니다.)
* 먼 지사에 hello 리소스 toorun 자체 도메인 컨트롤러를 가정 합니다. 사용자에 게 hello에서 toodomain 컨트롤러 hello world의 다른 쪽 인증 해야-로그인 느린가 오늘 합니다. Azure에서 Active Directory를 자세히 Microsoft 데이터 센터에서 실행이 속도를 높일 수 hello 지점에 더 많은 서버를 요구 하지 않고 있습니다.
* 재해 복구에 대 한 Azure를 사용 하는 조직 도메인 컨트롤러를 포함 하 여 hello 클라우드에서 활성 Vm 중 작은 부분만 유지 관리할 수 있습니다. 그런 다음 수에 준비 tooexpand이이 사이트 필요한 tootake로 다른 곳에서 오류에 대 한 합니다.

다른 경우도 있습니다. 예를 들어 모르겠으면 필요한 tooconnect hello 클라우드 tooan에서 Windows Server AD 온-프레미스 데이터 센터입니다. 예를 들어, 특정 사용자 집합을 제공 하는 SharePoint 팜을 toorun 하려는 경우 클라우드 기반 id 전적으로 사용자 로그인은 이들은 모두, Azure에서 독립 실행형 포리스트를 만들 수 있습니다. 원하는 바에 따라 다양하게 기술을 활용할 수 있습니다. Azure에서 Windows Server AD를 사용하는 방법에 대한 자세한 지침을 보려면 [여기를 참조하세요](http://msdn.microsoft.com/library/windowsazure/jj156090.aspx).

## <a name="ad"></a>Azure Active Directory 사용
SaaS 응용 프로그램이 점차 일반화되면서 당연한 질문이 제기되고 있습니다. 이러한 클라우드 기반 응용 프로그램에는 어떤 종류의 디렉터리 서비스를 사용해야 하나요? Microsoft의 응답 toothat 질문은 Azure Active Directory 합니다.

Hello 클라우드에서이 디렉터리 서비스를 사용 하기 위한 두 가지 기본 옵션이 있습니다.

* SaaS 응용 프로그램만 사용하는 개인 또는 조직은 Azure Active Directory를 단독 디렉터리 서비스로 사용할 수 있습니다.
* Windows Server Active Directory를 실행 하는 조직은 Active Directory의 온-프레미스 디렉터리 tooAzure 다음 toogive 사용 수 사용자에 게 single sign on tooSaaS 응용 프로그램입니다.

[그림 2](#fig2) hello에서는 Azure Active Directory가 있으면,이 두 옵션 중 첫 번째입니다.

![가상 컴퓨터 내의 Azure Active Directory](./media/identity/identity_02_AD.png)

<a name="fig2"></a>그림 2: Azure Active Directory 제공 조직의 사용자가 single sign on tooSaaS 응용 프로그램, Office 365를 포함 합니다.

Hello 그림에서 볼 수 있듯이 Azure AD는 다중 테 넌 트 서비스. 즉 동시에 많은 다른 조직의 사용자에 대한 디렉터리 정보 저장을 지원할 수 있습니다. 조직 A 사용자가이 예제에서는 tooaccess SaaS 응용 프로그램을 시도 하 고 있습니다. 이 응용 프로그램은 SharePoint Online과 같은 Office 365의 일부일 수 있으며, Microsoft 응용 프로그램이 아니어도 이 기술을 사용할 수도 있습니다. Azure AD hello SAML 2.0 프로토콜을 지원 하므로 모든 필요한 응용 프로그램에서 기능 toointeract hello를 사용 하 여이 업계 표준입니다. 사실 Azure AD를 사용하는 응용 프로그램은 Azure 데이터 센터가 아니어도 어느 데이터 센터에서나 실행할 수 있습니다.

SaaS 응용 프로그램 (1 단계)를 액세스 하는 hello 사용자 hello 프로세스가 시작 됩니다. toouse이 응용이 프로그램에서는 hello 사용자 Azure AD에서 발급 한 토큰을 제시 해야 합니다.

Hello 사용자를 식별 하는 정보를 포함 하는이 토큰 및 Azure AD에 의해 디지털로 서명 되어 있습니다. tooget hello 토큰 hello 사용자 인증 자신 tooAzure AD 사용자 이름 및 암호 (2 단계)를 제공 하 여 합니다. 필요한 hello 토큰을 반환 하는 azure AD에 다음 (3 단계).

이 토큰 toohello SaaS 응용 프로그램 (4 단계) hello 토큰 서명의 유효성을 검사 하 고 해당 내용 (5 단계)를 사용 하 여 전송 됩니다. Hello 응용 프로그램에서는 hello 토큰 toodecide 어떤 정보 hello 사용자 tooaccess 수 있는 권한이 포함 되어 hello id 정보를 사용 하는 일반적으로 아마도 다른 방법으로 합니다.

Hello 응용 프로그램 hello 토큰에 포함 된 내용을 보다 hello 사용자에 대 한 자세한 내용은 경우, (6 단계) hello Azure AD Graph API를 사용 하 여 Azure AD에서 직접 요청할 수 것입니다. Azure AD의 초기 버전 hello hello 디렉터리 스키마는 매우 간단: 사용자와 그룹 및 이들 사이에서 관계를 포함 합니다. 응용 프로그램 사용자 간에 연결에 대 한 정보 toolearn이 사용할 수 있습니다. 예를 들어, 응용 프로그램이 관리자에 게이 사용자의 toodecide 데이터의 허용 되는 액세스 toosome 청크 여부 tooknow 필요 합니다. 이 배울 것 hello Graph API를 통해 Azure AD를 쿼리하여 수 있습니다.

hello Graph API에는 모바일 장치를 비롯 한 대부분의 클라이언트에서 간단한 toouse 하므로 일반 RESTful 프로토콜을 사용 합니다. hello API는 OData를 더 유용한 방법으로 쿼리 언어 toolet 클라이언트 데이터 액세스 등을 추가 하 여 정의 된 hello 확장도 지원 합니다. (OData에 대한 자세한 정보는 [Introducing OData](http://download.microsoft.com/download/E/5/A/E5A59052-EE48-4D64-897B-5F7C608165B8/IntroducingOData.pdf)를 참조하세요.) Hello Graph API 사용된 toolearn 사용자 간의 관계에 대 한 일 수 있으므로 응용 프로그램을 (이 Graph API hello 라고 하는 이유)는 특정 조직에 대 한 Azure AD hello 스키마에 포함 된 hello 소셜 그래프를 이해할 수 있습니다. 및 자체 tooauthenticate tooAzure AD Graph API에 대 한 요청, 응용 프로그램에서 OAuth 2.0을 사용 합니다.

조직에서 Windows Server Active Directory를 사용 하지 않는-온-프레미스 서버 또는 도메인-없음이 있으며 Azure AD를 사용 하는 클라우드 응용 프로그램에만 전적으로 의존,이 클라우드 디렉터리에만 사용 하 여 가지게 hello 회사의 사용자가 single sign on tooall 그 중입니다. 이러한 시나리오가 많이 일반화되기는 했지만, 아직은 대부분 조직이 여전히 Windows Server Active Directory로 만들어진 온-프레미스 도메인을 사용합니다. Azure AD에 유용한 역할 tooplay로도 [그림 3](#fig3) 보여 줍니다.

![가상 컴퓨터에서 azure Active Directory](./media/identity/identity_03_AD.png)
<a id="fig3"></a>그림 3: 조직 페더레이션 할 수 있습니다 Windows Server Active Directory와 Azure Active Directory toogive 해당 사용자가 single sign on tooSaaS 응용 프로그램입니다.

이 시나리오에서는 조직 B의 사용자는 SaaS 응용 프로그램 tooaccess 하지 않고자 합니다. 이 작업을 수행한 그녀 전에 hello 조직의 디렉터리 관리자는 hello 그림 에서처럼 AD FS를 사용 하 여 Azure AD와 페더레이션 관계를 설정 해야 합니다. 이러한 관리자는 hello 조직의 온-프레미스 Windows Server AD 및 Azure AD 간의 데이터 동기화를 구성도 해야 합니다. 이 자동으로 사용자 및 그룹 정보에서에서 복사 hello 온-프레미스 디렉터리 tooAzure AD 합니다. 이렇게 하면 확인: hello 조직 hello 클라우드로 온-프레미스 디렉터리를 확장은 사실입니다. Windows Server AD 및 Azure AD에이 방식으로 결합 하는 사용 공간이 온-프레미스 않고 및 hello 클라우드에서 단일 엔터티로 관리할 수 있는 디렉터리 서비스 hello 조직 제공 합니다.

Azure AD toouse hello 사용자 먼저 로그인 tooher 온-프레미스 Active Directory 도메인 평소와 같이 (1 단계). Tooaccess hello SaaS 응용 프로그램 (2 단계)를 열려고 hello 페더레이션 프로세스 그녀는 (3 단계)이 응용이 프로그램에 대 한 토큰을 발급 하는 Azure AD에서 발생 합니다. 페더레이션 작동 방식에 대한 자세한 내용은 [Windows용 클레임 기반 ID: 기술 및 시나리오](http://www.davidchappell.com/writing/white_papers/Claims-Based_Identity_for_Windows_v3.0--Chappell.docx)를 참조하세요. 이 토큰이 이전에 hello 사용자를 식별 하는 정보를 포함 하 고 Azure AD에 의해 디지털로 서명 되어 있습니다. 이 토큰 toohello SaaS 응용 프로그램 (4 단계) hello 토큰 서명의 유효성을 검사 하 고 해당 내용 (5 단계)를 사용 하 여 전송 됩니다. Hello 이전 시나리오에서는 SaaS 응용 프로그램에서 사용할 수는 경우 Graph API toolearn이이 사용자에 대 한 자세한 hello hello 요소 이며 필요한 (6 단계).

오늘날 Azure AD가 온-프레미스 Windows Server AD의 완전한 대안은 아닙니다. 이미 설명한 것 처럼 hello 클라우드 디렉터리 훨씬 더 간단한 스키마를 않았으며 그룹 정책, 컴퓨터 및 LDAP에 대 한 지원에 대 한 hello 기능 toostore 정보 등도 누락 됩니다. (사실, Windows 컴퓨터에 구성 된 toolet 사용자만 Azure AD를 사용 하 여 tooit 로그인 일 수 없습니다-: 이것은 시나리오는 지원된 되지 않습니다.) 대신, Azure AD의 초기 목표 hello 별도 로그인을 유지 하지 않고 엔터프라이즈 사용자 hello 클라우드에서 응용 프로그램 액세스 하기 때문 등 해제 온-프레미스 디렉터리 관리자가 온-프레미스 디렉터리와 수동으로 동기화 모든 SaaS 응용 프로그램의 조직에서 사용 합니다. 하지만 시간이 지남에 따라이 클라우드 디렉터리 서비스 tooaddress 광범위 한 시나리오를 기대 합니다.

## <a name="ac"></a>Azure Active Directory 액세스 제어 사용
클라우드 기반 id 기술을 사용 하는 toosolve 다양 한 문제가 발생 될 수 있습니다. Azure Active Directory 사용자 제공할 수는 조직의 single sign on toomultiple SaaS 응용 프로그램 예. 하지만 다른 방법으로 hello 클라우드에서 identity 기술을 사용할 수도 있습니다.

가정, 예를 들어, 응용 프로그램에서 사용자에 게 여러에서 발급 한 토큰을 사용 하 여 로그인 toolet 하지 않고자 한다면 있는지 *id 공급자 (IdPs)*합니다. 현재 Facebook, Google, Microsoft 등 다양한 ID 공급자가 있으며, 대개 응용 프로그램에서는 사용자가 이러한 ID 중 하나를 사용하여 로그인할 수 있도록 해 줍니다. 해야 응용 프로그램 염려 하지 않아도 toomaintain 사용자 이름 및 암호는 작업의 목록이 이미 존재 하는 id에 의존 대신 수 하는 경우? 기존 id를 수락 하면 수명 간단 모두 사용자 이름 및 암호 tooremember 덜 하나 있는, 사용자에 대 한 사용자 이름 및 암호 목록을 더 이상 toomaintain 해야 하는 hello 응용 프로그램을 만드는 hello 사용자 없습니다.

그러나 ID 공급자는 모두 토큰을 발행하지만 표준을 따르는 것이 아니라 각 IdP마다 자체 형식이 있습니다. 또한 해당 토큰에 hello 정보는 또한 표준 없습니다. 예를 들어에서 발급 한 tooaccept 토큰 하지 않고자 한다면 응용 프로그램, Facebook, Google, 및 Microsoft는 문제에 직면 하 hello 챌린지 각 다른 형식의 toohandle 고유 코드를 작성 합니다.

그렇지만 꼭 고유 코드를 일일이 작성해야 할까요? ID 정보를 공통으로 표시하는 공동 단일 토큰 형식을 작성하는 매개자를 생성하면 이 방법은 수명 더 간단 하 게 hello 만드는 개발자를 위해 응용 프로그램을 지금 toohandle 한 종류만 토큰 하므로 합니다. Azure Active Directory 액세스 제어는 정확 하 게, 다양 한 토큰을 사용 하기 위한 중간자 hello 클라우드에서 제공 합니다. [그림 4](#fig4)에서 작동 과정을 확인하세요.

![가상 컴퓨터에서 azure Active Directory](./media/identity/identity_04_IdentityProviders.png)
<a id="fig4"></a>그림 4: Azure Active Directory 액세스 제어를 사용 하면 보다 쉽게 서로 다른 id 공급자가 발급 한 응용 프로그램 tooaccept id 토큰입니다.

사용자가 브라우저에서 tooaccess hello 응용 프로그램 hello 프로세스가 시작 됩니다. hello 응용 프로그램의 tooan 원하는의 IdP (리디렉션하고 해당 hello 응용 프로그램도 신뢰) 합니다. 그녀 인증 자신 toothis IdP로과 같은 사용자 이름 및 암호 (1 단계)를 입력 하 여 하 고 hello IdP 그녀의 (2 단계) 하는 방법에 대 한 정보를 포함 하는 토큰을 반환 합니다.

Hello 그림에서 볼 수 있듯이 액세스 제어는 Google, Yahoo, Facebook, (이전의 Windows Live ID), Microsoft 및 OpenID 공급자에서 만든 계정을 포함 하 여 다른 클라우드 기반 IdPs의 범위를 지원 합니다. 또한 Azure Active Directory를 사용하고 AD FS, Windows Server Active Directory와 페더레이션하여 생성된 ID를 지원합니다. hello 목표 IdPs hello 클라우드 또는 온-프레미스에서 실행 하는 여부 toocover hello 가장 일반적으로 사용 되는 id를 오늘 인 합니다.

Hello 사용자의 브라우저에는 IdP 토큰 그녀의 선택한 IdP에서,이 전송 토큰 tooAccess 컨트롤 (3 단계). 액세스 제어는 실제로이 IdP에서 발급 한 다음이 응용 프로그램에 대해 정의 된 toohello 규칙에 따라 새 토큰을 만드는 데 확인 hello 토큰을 확인 합니다. Azure Active Directory와 같은 액세스 제어는 다중 테 넌 트 서비스 있지만 hello 테 넌 트는 고객 조직 대신 응용 프로그램 않습니다. 각 응용 프로그램 hello 그림 에서처럼 자체 네임 스페이스를 가져올 수 있습니다 및 권한 부여 등에 대 한 다양 한 규칙을 정의할 수 있습니다.

각 응용 프로그램의 관리자가 이러한 규칙을 사용하여 다양한 IdP에서 제공한 토큰을 액세스 제어 토큰으로 변환하는 방법을 정의할 수 있습니다. 예를 들어 다른 IdP가 사용자 이름을 표시할 때 다른 유형을 사용하는 경우 액세스 제어 규칙에서 이러한 유형을 모두 공용 사용자 이름 유형으로 변환할 수 있습니다. 그런 다음 액세스 제어 toohello 응용 프로그램 (5 단계)를 제출이 새 토큰 백 toohello 브라우저 (4 단계)를 보냅니다. Hello 액세스 제어 토큰 있으면 hello 응용 프로그램은이 토큰이 실제로 액세스 제어에서 발급 한 다음 (6 단계)를 포함 하는 hello 정보를 사용 하 여 확인 합니다.

이 프로세스는 복잡 한 것 처럼 보일 수, 하는 동안 실제로 hello 응용 프로그램의 hello creator 더 간단 합니다. 서로 다른 정보를 포함 하는 다양 한 토큰을 처리 하지 않고 identities 여전히 친숙 한 정보로만 단일 토큰을 수신 하는 동안 여러 id 공급자에서 발급 한 hello 응용 프로그램에 사용할 수 있습니다. 또한 각 응용 프로그램 toobe 구성 tootrust 다양 한 IdPs를 요구 하지 않고 액세스 제어에서 이러한 트러스트 관계를 유지 관리 대신-응용 프로그램만 신뢰 해야 합니다.

동 점된 tooWindows은 액세스 제어 조건에 대해-Google 및 Facebook id만 허용 하는 Linux 응용 프로그램에서 사용할 수와 마찬가지로 살펴볼 것 합니다. 및 액세스 제어는 hello Azure Active Directory 제품군의 일부를 하는 경우에 있습니다 생각할 수 있으며 hello 이전 섹션에 설명 된 것에서 완전히 고유한 서비스로 합니다. Id를 가진 두 기술을 모두 작동 하는 동안 있습니다 (하지만 Microsoft 특정 시점에 toointegrate hello 두 필요 함을 설명한 내용이 나와 있습니다) 매우 다른 문제 해결 합니다.

ID 관련 작업은 대부분의 응용 프로그램에서 중요한 부분을 차지합니다. 액세스 제어의 hello ֲ toomake id 다양 한 id 공급자를 허용 하는 개발자가 toocreate 응용 프로그램 보다 쉽게 합니다. Hello 클라우드에서이 서비스를 배치 하 여 Microsoft 있게 되었습니다 모든 플랫폼에서 실행 되는 사용 가능한 tooany 응용 프로그램.

## <a name="about-hello-author"></a>작성자 hello에 대 한
David Chappell은 미국 캘리포니아주 샌프란시스코에 있는 Chappell & Associates([www.davidchappell.com](http://www.davidchappell.com))의 대표이다.

