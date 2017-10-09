점차 쉽게 사용할 수 있도록 클라우드 기술 및 도구가 발전하고 있으므로 조직에서는 생산성을 위해 [SaaS(Software as a Service)](https://azure.microsoft.com/overview/what-is-saas/) 응용 프로그램을 더 많이 사용하고 있습니다. SaaS 앱의 hello 수까지 확장 되면서 hello 관리자 toomanage 계정 및 액세스 권한을에 까다로운 되 고에 대 한 hello 사용자 tooremember 서로 다른 암호. 이러한 응용 프로그램을 개별적으로 관리하면 추가 작업이 필요하고 보안 수준이 저하됩니다.

* Toouse 경향이 많은 암호 tookeep 트랙 직원 보안 수준이 낮은 메서드 tooremember hello를 사용 하거나 암호를 적어에 동일한 암호 여러 계정 간에 합니다.
* 직원이 입사하거나 퇴사하는 경우 해당 직원의 모든 계정을 개별적으로 프로비전하거나 프로비전 해제해야 합니다.
* 또한 수행 하지 않고 작업을 위해 SaaS 앱을 사용 하 여 직원을 시작할 수 있습니다 it 부서에서, 만들고 있는 즉 hello IT 관리자가 시스템에서 자신의 계정을 승인 하지 않은 및 모니터링 되지 않습니다.  

이러한 모든 문제에 대한 해결책은 SSO(Single Sign-On)입니다. 가장 간단한 방법은 toomanage 여러 앱 hello에 하 고 사용자가 일관 된 로그온 환경을 제공 합니다. Azure Active Directory (Azure AD) 강력한 SSO 솔루션을 제공 하 고 많은 사용 가능한 미리 통합 된 응용 프로그램이, 관리자에 대 한 자습서와 tooquickly 새 응용 프로그램을 설정 하 고 사용자가 프로 비전을 시작 합니다.

## <a name="how-does-azure-active-directory-integrate-apps"></a>Azure Active Directory가 앱과 통합되는 방식
Azure AD toointegrate을 사용 하면 앱 및 프로 비전 된 계정입니다. 이 작업은 두 가지 방법 중 하나를 통해 수행할 수 있습니다.

* Hello 앱이 hello 응용 프로그램 갤러리에서에서 미리 통합 된 경우, 해당 포털 tooset 앱을 통해 이동 하 고 hello 설정을 tooallow SSO 구성 수 있습니다. 모든 갤러리 앱에 대 한 시작할 수 있습니다 다음 hello 간단한 단계별 지침을 설명 hello 응용 프로그램 갤러리 및 hello Azure 포털 tooenable single sign on을 표시 합니다.
* Hello 앱 갤러리 hello에 없는 경우 설정할 수 있습니다 여전히 대부분의 응용 프로그램을 Azure ad는 사용자 지정 응용 프로그램으로. 이 좀 더 기술적인 전문 지식을 tooconfigure가 필요합니다. SAML 2.0을 페더레이션된 앱으로 지원하는 모든 응용 프로그램 또는 HTML 기반 로그인 페이지가 암호 SSO 앱으로 있는 모든 응용 프로그램을 추가할 수 있습니다.

Hello에 있는 사용자가 만든 자신의 계정을 의해 관리 되지 않는 SaaS 앱에 대 한 IT hello [Cloud App Discovery](../articles/active-directory/active-directory-cloudappdiscovery-whatis.md) 도구는 솔루션을 제공 합니다. 이 도구는 hello 웹 트래픽 tooidentify 각각 사용 하는 사용자 수가 hello 및 hello 조직 전체에서 사용 중인 어떤 응용 프로그램을 모니터링 합니다. IT 앱 hello 사용자가 선호 하 고 SSO에 대 한 Azure AD로 어떤 toointegrate 결정이 정보 toolearn를 사용할 수 있습니다.  

Azure AD에 응용 프로그램을 통합 하는 경우에 hello 사용자가 설정 된 응용 프로그램 identities tootheir 해당 Azure AD id를 매핑할 수 있습니다.  

