---
title: "hello 클래식 포털에서 Azure AD 응용 프로그램 프록시 aaaEnable | Microsoft Docs"
description: "Hello Azure 클래식 포털에서에서 응용 프로그램 프록시를 설정 하 고 hello 역방향 프록시에 대 한 hello 커넥터를 설치 합니다."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: c7186f98-dd80-4910-92a4-a7b8ff6272b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/02/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 8be9416a61993e1b46a20152e172c5133e54c0a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-application-proxy-in-hello-classic-portal-and-download-connectors"></a>Hello 클래식 포털에서 응용 프로그램 프록시를 사용 하도록 설정 하 고 커넥터를 다운로드 합니다.
이 문서에서는 Azure AD의 hello 단계 tooenable 클라우드 디렉터리에 대 한 Microsoft Azure AD 응용 프로그램 프록시를 안내 합니다.

어떤 응용 프로그램 프록시 도와 작업을 수행할 수 있는 잘 모르는 경우에 대해 자세히 알아보세요 [어떻게 tooprovide 보안 원격 액세스 tooon 온-프레미스 응용 프로그램](active-directory-application-proxy-get-started.md)합니다.

## <a name="application-proxy-prerequisites"></a>응용 프로그램 프록시 필수 구성 요소
사용 하도록 설정 하 고 응용 프로그램 프록시 서비스를 사용할 수 있습니다, toohave가 필요 합니다.

* 사용자가 전역 관리자인 [Microsoft Azure AD 기본 또는 프리미엄 구독](active-directory-editions.md) 및 Azure AD 디렉터리입니다.
* Hello 응용 프로그램 프록시 커넥터를 설치할 수 있는 2016 또는 Windows Server 2012 r 2를 실행 하는 서버입니다. hello 서버 hello 클라우드에서 요청에 toohello 응용 프로그램 프록시 서비스를 보내고는 HTTP 또는 HTTPS 연결 toohello 응용 프로그램을 게시 하는 데 필요한 합니다.
  * 게시 된 응용 프로그램을 single sign on tooyour에 대 한이 컴퓨터를 도메인에 가입할 수 hello 동일한 AD 도메인에 게시 하는 hello 응용 프로그램으로 합니다. 자세한 내용은 [응용 프로그램 프록시를 사용하는 Single Sign-On](active-directory-application-proxy-sso-using-kcd.md)을 참조하세요.
* 조직에서 프록시를 사용 하는 경우 서버 tooconnect toohello 인터넷 읽을 [작업을 기존 온-프레미스 프록시 서버](application-proxy-working-with-proxy-servers.md) 방법에 대 한 자세한 내용은 tooconfigure 해당 합니다.

## <a name="open-your-ports"></a>포트 열기

tooprepare 환경을 Azure AD 응용 프로그램 프록시에 대 한 먼저 tooenable 통신 tooAzure 데이터 센터가 필요 합니다. Hello 경로에 방화벽이 있는 경우 것는 열려 있으므로 커넥터에서 HTTPS (TCP)를 만들 수는 hello toohello 응용 프로그램 프록시를 요청 해야 합니다.

1. 열기 hello 다음 포트가 너무**아웃 바운드** 트래픽:

   | 포트 번호 | 사용 방법 |
   | --- | --- |
   | 80 | Hello SSL 인증서를 확인 하는 동안 다운로드 인증서 해지 목록 (Crl) |
   | 443 | 응용 프로그램 프록시 서비스 hello로 모든 아웃 바운드 통신 |

   방화벽에는 toooriginating 사용자에 따라 트래픽을 강제 적용을 네트워크 서비스로 실행 되는 Windows 서비스에서 들어오는 트래픽에 대해 이러한 포트를 엽니다.

   > [!IMPORTANT]
   > hello 반영 되어 1.5.132.0 커넥터 버전에 대 한 hello 포트 요구 사항 및 새 합니다. 이전 커넥터 버전을 계속 해야 하는 경우 또한 해야 포트 다음 tooenable hello: 5671, 8080, 9090, 9091, 9350, 9352, 및 10100 – 10120 합니다.
   >
   >커넥터 toohello 최신 버전을 업데이트 하는 방법에 대 한 정보를 참조 하십시오. [이해 Azure AD 응용 프로그램 프록시 커넥터](application-proxy-understand-connectors.md#automatic-updates)합니다.

2. 방화벽 또는 프록시 DNS 허용 목록이 허용 하는 경우 허용 목록 연결 toomsappproxy.net 및 servicebus.windows.net 수 있습니다. Tooallow 액세스 toohello 필요 그렇지 않은 경우 [Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/details.aspx?id=41653)는 매주 업데이트 됩니다.

3. 사용 하 여 hello [Azure AD 응용 프로그램 프록시 커넥터 포트 테스트 도구](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify 커넥터 hello 응용 프로그램 프록시 서비스에 연결할 수 있습니다. 여기에 최소한 hello 중앙 미국 지역과 hello 지역 가장 가까운 tooyou는 모두 녹색 확인 표시가 있는지를 확인 합니다. 그 외의 항목에도 녹색 확인 표시가 있으면 복원력이 더 뛰어난 것입니다.

## <a name="enable-application-proxy-in-azure-ad"></a>Azure AD에서 응용 프로그램 프록시를 사용하도록 설정
1. Hello에 관리자 권한으로 로그인 [Azure 클래식 포털](https://manage.windowsazure.com/)합니다.
2. 디렉터리 tooActive 이동한 다음 응용 프로그램 프록시 tooenable 원하는 hello 디렉터리를 선택 합니다.

    ![Active Directory - 아이콘](./media/active-directory-application-proxy-enable/ad_icon.png)
3. 선택 **구성** hello 디렉터리 페이지에서 너무 아래로 스크롤하여 및**응용 프로그램 프록시**합니다.
4. 설정/해제 **이 디렉터리에 대 한 응용 프로그램 프록시 서비스 사용** 너무**Enabled**합니다.

    ![응용 프로그램 프록시 사용](./media/active-directory-application-proxy-enable/app_proxy_enable.png)
5. **지금 다운로드**를 선택합니다. hello **Azure AD 응용 프로그램 프록시 커넥터 다운로드** 열립니다. Hello 사용 조건을 읽고 동의 클릭 **다운로드** hello 커넥터에 대 한 toosave hello Windows Installer 파일 (.exe).

## <a name="install-and-register-hello-connector"></a>설치 하 고 hello 커넥터 등록
1. 실행 **AADApplicationProxyConnectorInstaller.exe** hello 서버에 따라 toohello 필수 구성 요소를 준비 합니다.
2. Hello 마법사 tooinstall의 hello 지침을 따릅니다.
3. 설치 하는 동안 Azure AD 테 넌 트의 응용 프로그램 프록시 hello로 증명된 tooregister hello 커넥터 됩니다.

   * Azure AD 전역 관리자 자격 증명을 제공합니다. 전역 관리자 테넌트는 Microsoft Azure 자격 증명과 다를 수 있습니다.
   * Admin 님 안녕하세요 hello 커넥터가 레지스터 hello 설정한 같은 디렉터리는 응용 프로그램 프록시 서비스 hello 있는지 확인 합니다. 예를 들어 hello 테 넌 트 도메인이 contoso.com 이면 admin 님 안녕하세요 해야 admin@contoso.com 또는 해당 도메인에 다른 별칭입니다.
   * 경우 **IE 보안 강화 구성** 너무 설정**에** hello 서버 hello 등록 화면이 차단 될 수 있습니다. hello 오류 메시지의 지침에 따라 hello tooallow 액세스 합니다. Internet Explorer 보안 강화가 해제되어 있는지 확인하세요.
   * 커넥터 등록에 실패한 경우 [응용 프로그램 프록시 문제 해결](active-directory-application-proxy-troubleshoot.md)을 참조하세요.  
4. Hello 설치가 완료 되 면 두 개의 새로운 서비스가 tooyour 서버를 추가 됩니다.

   * **Microsoft AAD 응용 프로그램 프록시 커넥터** 에서 연결 사용

     * **Microsoft AAD 응용 프로그램 프록시 커넥터 업데이터**는 자동화된 업데이트 서비스입니다. 정기적으로 새 버전의 hello 커넥터에 대 한 확인 하 고 필요에 따라 hello 커넥터를 업데이트 합니다.

     ![앱 프록시 커넥터 서비스 - 스크린샷](./media/active-directory-application-proxy-enable/app_proxy_services.png)
5. 클릭 **마침** hello 설치 창에서.

커넥터에 대 한 정보는 [Azure AD 응용 프로그램 프록시 커넥터 이해](application-proxy-understand-connectors.md)를 참조하세요.

고가용성을 위해 커넥터를 두 개 이상 배포해야 합니다. toodeploy 자세한 커넥터 반복 2와 3 단계. 각 커넥터는 별도로 등록되어야 합니다.

Toouninstall hello 커넥터 원한다 면 hello 커넥터 서비스와 hello 업데이트 프로그램 서비스를 모두 제거 합니다. 컴퓨터 toofully 제거 hello 서비스를 다시 시작 합니다.

## <a name="next-steps"></a>다음 단계
이제 준비가 너무[응용 프로그램 프록시는 응용 프로그램 게시](active-directory-application-proxy-publish.md)합니다.

별도 네트워크 또는 서로 다른 위치에 있는 응용 프로그램의 경우 논리 단위로 커넥터 그룹 tooorganize hello 다른 커넥터를 사용할 수 있습니다. [응용 프로그램 프록시 커넥터 작업](active-directory-application-proxy-connectors.md)에 대해 자세히 알아봅니다.
