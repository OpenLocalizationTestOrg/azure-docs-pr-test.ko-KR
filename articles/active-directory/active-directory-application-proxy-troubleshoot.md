---
title: "응용 프로그램 프록시 aaaTroubleshoot | Microsoft Docs"
description: "표지 방법을 Azure AD 응용 프로그램 프록시에 tootroubleshoot 오류입니다."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 970caafb-40b8-483c-bb46-c8b032a4fb74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: H1Hack27Feb2017; it-pro
ms.openlocfilehash: d426708a2ee32da6674987b5794602ed984b06b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-application-proxy-problems-and-error-messages"></a>응용 프로그램 프록시 문제 및 오류 메시지 문제 해결
응용 프로그램 게시 또는 게시 된 응용 프로그램 액세스 하는 동안 오류가 발생 한 경우 hello 옵션 toosee Microsoft Azure AD 응용 프로그램 프록시 제대로 작동 하는 경우 다음을 확인 합니다.

* 열기 hello Windows 서비스 콘솔을 해당 hello 확인 **Microsoft AAD 응용 프로그램 프록시 커넥터** 서비스를 활성화 하 여 실행 합니다. 또한 hello 다음 이미지와 같이 toolook hello 응용 프로그램 프록시 서비스 속성 페이지에서를 참조할 수 있습니다.  
  ![Microsoft AAD 응용 프로그램 프록시 커넥터 속성 창 스크린샷](./media/active-directory-application-proxy-troubleshoot/connectorproperties.png)
* 이벤트 뷰어를 열고 **응용 프로그램 및 서비스 로그** > **Microsoft** > **AadApplicationProxy** > **커넥터** > **관리**에서 응용 프로그램 프록시 커넥터 이벤트를 찾습니다.
* 필요에 따라 자세한 로그도 사용할 수 있는 [응용 프로그램 프록시 커넥터 세션 로그 hello 켜기](application-proxy-understand-connectors.md#under-the-hood)합니다.

Hello Azure AD 문제 해결 도구에 대 한 자세한 내용은 참조 [도구 toovalidate 커넥터 네트워킹 필수 구성 요소 문제 해결](https://blogs.technet.microsoft.com/applicationproxyblog/2015/09/03/troubleshooting-tool-to-validate-connector-networking-prerequisites)합니다.

## <a name="hello-page-is-not-rendered-correctly"></a>hello 페이지가 제대로 렌더링 되지 않습니다.
특정 오류 메시지를 수신하지 않고도 응용 프로그램 렌더링 또는 기능이 제대로 이뤄지지 않는 문제가 있을 수 있습니다. 이 hello 문서 경로 게시 하지만 hello 응용 프로그램에 해당 경로 외부에 있는 콘텐츠에 필요한 경우 발생할 수 있습니다.

예를 들어 hello 경로 https://yourapp/app를 게시 하는 경우 https://yourapp/media의 이미지를 호출 하는 hello 응용 프로그램은 렌더링 되지 않습니다. Hello 가장 높은 수준 경로 tooinclude 모든 관련 콘텐츠를 사용 하 여 hello 응용 프로그램을 게시 하는 있는지 확인 합니다. 이 예에서는 http://yourapp/입니다.

Hello 블로그 게시물을 참조 경로 tooinclude 참조 콘텐츠를 변경 했지만 여전히 hello 경로에서 하위 링크에 사용자가 tooland 필요 [hello Azure AD 액세스 패널 및 Office 365 응용 프로그램에서 응용 프로그램 프록시 응용 프로그램에 대 한 설정 hello 오른쪽 링크 시작 관리자](https://blogs.technet.microsoft.com/applicationproxyblog/2016/04/06/setting-the-right-link-for-application-proxy-applications-in-the-azure-ad-access-panel-and-office-365-app-launcher/)합니다.

## <a name="connector-errors"></a>커넥터 오류

사용 하 여 hello [Azure AD 응용 프로그램 프록시 커넥터 포트 테스트 도구](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify 커넥터 hello 응용 프로그램 프록시 서비스에 연결할 수 있습니다. 여기에 최소한 hello 중앙 미국 지역과 hello 지역 가장 가까운 tooyou는 모두 녹색 확인 표시가 있는지를 확인 합니다. 그 외의 항목에도 녹색 확인 표시가 있으면 복원력이 더 뛰어난 것입니다. 

Hello 커넥터 마법사 설치 하는 동안 등록에 실패 하면 hello 실패에 대 한 tooview hello 이유는 두 가지가 있습니다. 아래 hello 이벤트 로그를 확인 하거나 **응용 프로그램 및 서비스 Logs\Microsoft\AadApplicationProxy\Connector\Admin**, 다음 Windows PowerShell 명령이 실행된 하는 hello 또는:

    Get-EventLog application –source “Microsoft AAD Application Proxy Connector” –EntryType “Error” –Newest 1

Hello 이벤트 로그에서 hello 커넥터 오류를 찾은 후이 테이블의 일반적인 오류 tooresolve hello 문제를 사용 합니다.

| 오류 | 권장되는 단계 |
| ----- | ----------------- |
| 커넥터 등록 실패: hello Azure 관리 포털에서에서 응용 프로그램 프록시 및 Active Directory 사용자 이름과 암호를 올바르게 입력 했는지를 사용할 수 있는지 확인 합니다. 오류: '하나 이상의 오류가 발생했습니다.' | TooAzure AD에에서 로그인 하지 않고 hello 등록 창을 닫은 경우 hello 커넥터 마법사를 다시 실행 하 고 hello 커넥터를 등록 합니다. <br><br> Hello 등록 창이 열리고 toolog에서 허용 하지 않고 바로 닫힐, 경우에이 오류가 발생할 것 됩니다. 시스템에 네트워킹 오류가 있을 때 이 오류가 발생합니다. 브라우저 tooa 공용 웹 사이트에서 가능한 tooconnect 하며 hello 포트가에 지정 된 대로 열려 있는지 확인 [응용 프로그램 프록시 사전 요구 사항](active-directory-application-proxy-enable.md)합니다. |
| Hello 등록 창에 명확한 오류가 표시 됩니다. 설치를 진행할 수 없습니다. | 이 오류를 참조 하는 경우 다음 hello 창이 닫힙니다 hello 잘못 된 사용자 이름 또는 암호 입력 했습니다. 다시 시도하세요. |
| 커넥터 등록 실패: hello Azure 관리 포털에서에서 응용 프로그램 프록시 및 Active Directory 사용자 이름과 암호를 올바르게 입력 했는지를 사용할 수 있는지 확인 합니다. 오류: ' AADSTS50059: 테 넌 트 식별 정보 없음 hello 요청 중 하나에서 찾을 수 없거나 사용 권한에 포함 된 모든 주 URI 못한 자격 증명 및 검색 서비스에서 제공 합니다. | Toosign 고치려는 tooaccess Microsoft 계정과 hello 디렉터리의 hello 조직 ID에 속하는 도메인이 아닌를 사용 하 여 시도 합니다. 해당 admin 님 안녕하세요 hello의 일부 인지 확인 hello 테 넌 트 도메인, 예를 들어 도메인 이름이 같은 경우 hello Azure AD 도메인 contoso.com admin 님 안녕하세요 되어야 admin@contoso.com합니다. |
| PowerShell 스크립트를 실행 하기 위한 tooretrieve hello 현재 실행 정책을 실패 했습니다. | Hello 커넥터 설치에 실패 하면 toomake PowerShell 실행 정책을 사용할 수 있는지 확인 합니다. <br><br>1. Hello 그룹 정책 편집기를 엽니다.<br>2. 너무 이동**컴퓨터 구성** > **관리 템플릿** > **Windows 구성 요소**  >   **Windows PowerShell** 두 번 클릭 하 고 **Turn on Script Execution**합니다.<br>3. hello 실행 정책을 tooeither를 설정할 수 있습니다 **구성 되어 있지** 또는 **Enabled**합니다. 경우 너무 설정**Enabled**, 있는지 확인 하는 옵션, tooeither hello 실행 정책을 설정 **로컬 스크립트 및 원격 서명 된 스크립트 허용** 또는 너무**모든 스크립트 허용**합니다. |
| 커넥터는 toodownload hello 구성을 하지 못했습니다. | hello 커넥터의 클라이언트 인증서 인증을 위해 사용 되는 만료 되었습니다. 프록시 뒤 커넥터를 설치 하는 hello 있는 경우에 발생할 수 있습니다. 이 경우 hello 커넥터 hello 인터넷에 액세스할 수 없습니다 및 됩니다 수 tooprovide 응용 프로그램 tooremote 사용자입니다. Hello를 사용 하 여 수동으로 신뢰 갱신 `Register-AppProxyConnector` Windows powershell에서 cmdlet. 커넥터는 프록시를 경우 필요한 toogrant 인터넷 액세스 toohello 커넥터 계정 "네트워크 서비스" 및 "로컬 시스템" 이 위해서는 toohello 프록시 액세스 권한을 부여 하 여 또는 프록시 hello toobypass을 설정 하 여 합니다. |
| 커넥터 등록 실패: Active Directory tooregister hello 커넥터의 전역 관리자가 있는지 확인 합니다. 오류: ' hello 등록 요청이 거부 되었습니다.' | hello 별칭을 사용 하 여 toolog 중 어느 것에이 도메인의 관리자 하지 않습니다. Hello 사용자의 도메인을 소유 하는 hello 디렉터리에 대해 커넥터가 항상 설치 됩니다. Hello 관리자 계정으로 toosign 고치려는 전역 권한을 toohello Azure AD 테 넌 트에 있는지 확인 합니다. |

## <a name="kerberos-errors"></a>Kerberos 오류

이 표에 일반적인 hello Kerberos 설정 및 구성 하는 있으며 해결을 위한 제안을 포함 하는 오류입니다.

| 오류 | 권장되는 단계 |
| ----- | ----------------- |
| PowerShell 스크립트를 실행 하기 위한 tooretrieve hello 현재 실행 정책을 실패 했습니다. | Hello 커넥터 설치에 실패 하면 toomake PowerShell 실행 정책을 사용할 수 있는지 확인 합니다.<br><br>1. Hello 그룹 정책 편집기를 엽니다.<br>2. 너무 이동**컴퓨터 구성** > **관리 템플릿** > **Windows 구성 요소**  >   **Windows PowerShell** 두 번 클릭 하 고 **Turn on Script Execution**합니다.<br>3. hello 실행 정책을 tooeither를 설정할 수 있습니다 **구성 되어 있지** 또는 **Enabled**합니다. 경우 너무 설정**Enabled**, 있는지 확인 하는 옵션, tooeither hello 실행 정책을 설정 **로컬 스크립트 및 원격 서명 된 스크립트 허용** 또는 너무**모든 스크립트 허용**합니다. |
| 12008-azure AD 초과 hello 최대 허용 된 Kerberos 인증 시도 횟수 toohello 백 엔드 서버입니다. | 이 오류를 Azure AD 간에 잘못 된 구성이 나타내고 백 엔드 hello 수 응용 프로그램 서버 또는 두 컴퓨터 모두에서 날짜 및 시간 구성에 문제가 있습니다. Azure AD에서 만든 hello Kerberos 티켓을 거부 하는 hello 백 엔드 서버. 확인 Azure AD와 hello 백 엔드 응용 프로그램 서버가 올바르게 구성 되어 있습니다. Hello Azure AD에서 hello 날짜 및 시간 구성 및 hello 백 엔드 응용 프로그램 서버 동기화 해야 합니다. |
| 13016-azure AD 토큰 또는 액세스 쿠키 hello hello 가장자리에 UPN이 hello 사용자 대신 Kerberos 티켓을 검색할 수 없습니다. | Hello STS 구성에 문제가 있습니다. Hello STS에서에서 UPN 클레임 hello 구성을 수정 합니다. |
| 13019-azure AD는 hello 다음 일반 API 오류로 인해 hello 사용자 대신 Kerberos 티켓을 검색할 수 없습니다. | 이 이벤트는 Azure AD 간에 잘못 된 구성이 나타낼 수 있습니다 및 hello 도메인 컨트롤러 서버 또는 두 컴퓨터 모두에서 날짜 및 시간 구성에 문제가 있습니다. hello 도메인 컨트롤러는 Azure AD에서 만든 hello Kerberos 티켓을 거부 합니다. 확인 Azure AD 및 hello 백 엔드 응용 프로그램 서버가 제대로 구성, 특히 SPN hello 구성 합니다. Hello Azure AD 도메인에 가입 toohello 인지 확인 동일한 도메인 도메인 컨트롤러를 hello 도메인 컨트롤러 tooensure hello으로 트러스트를 설정 Azure AD와 합니다. Hello Azure AD에서 hello 날짜 및 시간 구성 및 hello 도메인 컨트롤러 동기화 해야 합니다. |
| 13020-hello 백 엔드 서버 SPN이 정의 되어 있지 않으므로 azure AD hello 사용자 대신 Kerberos 티켓을 검색할 수 없습니다. | 이 이벤트는 Azure AD 간에 잘못 된 구성이 나타낼 수 있습니다 및 hello 도메인 컨트롤러 서버 또는 두 컴퓨터 모두에서 날짜 및 시간 구성에 문제가 있습니다. hello 도메인 컨트롤러는 Azure AD에서 만든 hello Kerberos 티켓을 거부 합니다. 확인 Azure AD 및 hello 백 엔드 응용 프로그램 서버가 제대로 구성, 특히 SPN hello 구성 합니다. Hello Azure AD 도메인에 가입 toohello 인지 확인 동일한 도메인 도메인 컨트롤러를 hello 도메인 컨트롤러 tooensure hello으로 트러스트를 설정 Azure AD와 합니다. Hello Azure AD에서 hello 날짜 및 시간 구성 및 hello 도메인 컨트롤러 동기화 해야 합니다. |
| 13022-azure AD는 hello 백 엔드 서버 응답 HTTP 401 오류와 함께 tooKerberos 인증 시도 하기 때문에 hello 사용자를 인증할 수 없습니다. | 이 이벤트를 Azure AD 간에 잘못 된 구성이 나타내고 백 엔드 hello 수 응용 프로그램 서버 또는 두 컴퓨터 모두에서 날짜 및 시간 구성에 문제가 있습니다. Azure AD에서 만든 hello Kerberos 티켓을 거부 하는 hello 백 엔드 서버. 확인 Azure AD와 hello 백 엔드 응용 프로그램 서버가 올바르게 구성 되어 있습니다. Hello Azure AD에서 hello 날짜 및 시간 구성 및 hello 백 엔드 응용 프로그램 서버 동기화 해야 합니다. |

## <a name="end-user-errors"></a>최종 사용자 오류

이 목록에서는 tooaccess hello 응용 프로그램을 시도 하며 실패 하는 경우 최종 사용자가 발생할 수 있는 오류를 설명 합니다. 

| 오류 | 권장되는 단계 |
| ----- | ----------------- |
| hello 웹 사이트는 hello 페이지를 표시할 수 없습니다. | 이때 회원님의 사용자 tooaccess hello 앱 hello 응용 프로그램이 IWA 응용 프로그램인 경우 게시 하려고 할 때이 오류가 발생할 수 있습니다. hello이 응용이 프로그램 올바르지 않을 수에 대 한 SPN을 정의 합니다. IWA 앱에 대 한 hello이 응용이 프로그램에 대해 구성 된 SPN이 올바른지 확인 합니다. |
| hello 웹 사이트는 hello 페이지를 표시할 수 없습니다. | 이때 회원님의 사용자 tooaccess hello 앱 hello 응용 프로그램이 OWA 응용 프로그램인 경우 게시 하려고 할 때이 오류가 발생할 수 있습니다. Hello 다음 중 하나 때문일 수 있습니다.<br><li>이 응용 프로그램이 잘못 되었습니다. hello SPN을 정의 합니다. 이 응용 프로그램에 대해 구성 된 SPN 해당 hello 올바른지 확인 합니다.</li><li>hello, 적합 한 회사 계정이 toosign 또는 hello 사용자가 게스트 사용자 하지 않고 tooaccess hello 응용 프로그램을 시도한 hello 사용자 Microsoft 계정을 사용 합니다. 확인 되었는지 hello 사용자가 로그인 일치 hello hello의 도메인을 자신의 회사 계정을 사용 하 여 응용 프로그램을 게시 합니다. Microsoft 계정 사용자 및 게스트가 IWA 응용 프로그램에 액세스할 수 없습니다.</li><li>hello tooaccess hello 응용 프로그램을 시도한 사용자 hello 온-프레미스 쪽에서이 응용 프로그램에 대해 올바르게 정의 되지 않았습니다. Hello 온-프레미스 컴퓨터에서이 백엔드 응용 프로그램에 대해 정의 된 대로이 사용자에 hello 적절 한 권한이 있는지 확인 합니다. |
| 이 회사 앱에 액세스할 수 없습니다. 사용자는 인증된 되지 않았습니다. tooaccess이 응용이 프로그램입니다. 권한 부여에 실패했습니다. Access toothis 응용 프로그램으로 있는지 tooassign hello 사용자를 확인 합니다. | 사용자가 tooaccess hello 앱에서 회사 계정 toosign 해당 하는 대신 Microsoft 계정을 사용 하는 경우 게시 하려고 할 때이 오류가 발생할 수 있습니다. 게스트 사용자에게 이 오류가 발생할 수도 있습니다. Microsoft 계정 사용자 및 게스트가 IWA 응용 프로그램에 액세스할 수 없습니다. 확인 되었는지 hello 사용자가 로그인 일치 hello hello의 도메인을 자신의 회사 계정을 사용 하 여 응용 프로그램을 게시 합니다.<br><br>이 응용 프로그램에 대 한 hello 사용자를 할당 하지 않았을 수 있습니다. Toohello 이동 **응용 프로그램** 탭 아래에서 **사용자 및 그룹**,이 사용자 또는 사용자 그룹 toothis 응용 프로그램을 할당 합니다. |
| 현재 이 회사 앱에 액세스할 수 없습니다. 다시 시도해 보세요... hello 커넥터 시간이 초과 되었습니다. | 사용자가 tooaccess hello 앱 hello 온-프레미스 쪽에서이 응용 프로그램에 대해 올바르게 정의 되지 않은 경우 게시 하려고 할 때이 오류가 발생할 수 있습니다. Hello 온-프레미스 컴퓨터에서이 백엔드 응용 프로그램에 대해 정의 된 사용자가 있는 hello 적절 한 권한이 있는지 확인 합니다. |
| 이 회사 앱에 액세스할 수 없습니다. 사용자는 인증된 되지 않았습니다. tooaccess이 응용이 프로그램입니다. 권한 부여에 실패했습니다. 해당 hello 사용자에 게 Azure Active Directory Premium 또는 Basic에 대 한 라이선스가 있는지 확인 합니다. | 사용자가 tooaccess hello 앱 hello 구독자의 관리자가 Premium/Basic 라이선스와 명시적으로 지정 하지 않은 경우 게시 하려고 할 때이 오류가 발생할 수 있습니다. Toohello 구독자의 Active Directory 이동 **라이선스** 탭 하 고이 사용자 또는 사용자 그룹이 Premium 또는 Basic 라이선스가 할당 되어 있는지 확인 합니다. |

## <a name="my-error-wasnt-listed-here"></a>내 오류가 여기에 나열되지 않았습니다.

오류 또는이 문제 해결 가이드에 나열 되지 않은 Azure AD 응용 프로그램 프록시에 문제가 발생 하면 항목에 대 한 toohear를 하겠습니다. 전자 메일 tooour 보내기 [피드백 팀](mailto:aadapfeedback@microsoft.com) 실제로 발생 하는 hello 오류 hello 세부 정보와 함께 합니다.

## <a name="see-also"></a>참고 항목
* [Azure Active Directory에 대한 응용 프로그램 프록시 사용](active-directory-application-proxy-enable.md)
* [응용 프로그램 프록시를 사용하여 응용 프로그램 게시](active-directory-application-proxy-publish.md)
* [Single Sign-On 사용](active-directory-application-proxy-sso-using-kcd.md)
* [조건부 액세스 사용](active-directory-application-proxy-conditional-access.md)


<!--Image references-->
[1]: ./media/active-directory-application-proxy-troubleshoot/connectorproperties.png
[2]: ./media/active-directory-application-proxy-troubleshoot/sessionlog.png
