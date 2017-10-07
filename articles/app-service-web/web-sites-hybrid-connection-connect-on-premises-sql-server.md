---
title: "aaaConnect 하이브리드 연결을 사용 하 여 Azure 앱 서비스의 웹 앱에서 tooon 온-프레미스 SQL Server"
description: "Microsoft Azure에 웹 응용 프로그램을 만들고 tooan 온-프레미스 SQL Server 데이터베이스 연결"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: 2b4e0539-1a0b-4aa1-8a69-b4b053c3b2e5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2016
ms.author: cephalin
ms.openlocfilehash: 2e8f8f7e0b9733cfb0433697615faba4358c6023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooon-premises-sql-server-from-a-web-app-in-azure-app-service-using-hybrid-connections"></a>하이브리드 연결을 사용 하 여 Azure 앱 서비스의 웹 앱에서 tooon 온-프레미스 SQL Server 연결
하이브리드 연결은 연결 수 [Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714) 정적 TCP 포트를 사용 하는 웹 응용 프로그램 tooon 온-프레미스 리소스입니다. 지원되는 리소스로는 Microsoft SQL Server, MySQL, HTTP 웹 API, App Service, 대부분의 사용자 지정 웹 서비스가 있습니다.

이 자습서에 설명 합니다 방법을 toocreate 앱 서비스 웹 앱 hello에 [Azure 포털](http://go.microsoft.com/fwlink/?LinkId=529715), hello 새 하이브리드 연결 기능을 사용 하 여 hello 웹 응용 프로그램 tooyour 로컬 온-프레미스 SQL Server 데이터베이스를 연결, 간단한 ASP.NET 만들기 hello 하이브리드 연결을 사용 하 고 hello 응용 프로그램 toohello 앱 서비스 웹 앱을 배포 하는 응용 프로그램입니다. Azure에서 웹 응용 프로그램을 완료 하는 hello 온 프레미스에 있는 멤버 자격 데이터베이스에 사용자 자격 증명을 저장 합니다. hello 자습서에서는 Azure 또는 ASP.NET을 사용 하 여 이전 본 경험이 없는 사용자 가정 합니다.

> [!NOTE]
> Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다. 신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.
> 
> hello 하이브리드 연결 기능은의 hello 웹 응용 프로그램 부분은 hello에만 사용할 수 있는 [Azure 포털](https://portal.azure.com)합니다. BizTalk 서비스의 연결 toocreate 참조 [하이브리드 연결](http://go.microsoft.com/fwlink/p/?LinkID=397274)합니다.  
> 
> 

## <a name="prerequisites"></a>필수 조건
toocomplete이이 자습서에서는 다음 제품 hello 필요 합니다. 모두 무료 버전으로 사용 가능할 수 있으므로, Azure용 개발을 완전히 무료로 시작할 수 있습니다.

* **Azure 구독** - 무료 구독에 대해서는 [Azure 무료 평가](/pricing/free-trial/)를 참조하세요.
* **Visual Studio 2013** -toodownload Visual Studio 2013의 무료 평가판 버전 참조 [Visual Studio 다운로드](http://www.visualstudio.com/downloads/download-visual-studio-vs)합니다. 계속하기 전에 이 제품을 설치하세요.
* **Microsoft .NET Framework 3.5 서비스 팩 1** - 운영 체제가 Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7 또는 Windows Server 2008 R2인 경우 제어판 > 프로그램 및 기능 > Windows 기능 사용/사용 안 함에서 이 제품을 사용하도록 설정할 수 있습니다. 그렇지 않으면 hello에서 다운로드할 수 [Microsoft 다운로드 센터](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22)합니다.
* **SQL Server 2014 Express with Tools** -Microsoft SQL Server Express를 무료로 다운로드 hello에 [Microsoft 웹 플랫폼 데이터베이스 페이지](http://www.microsoft.com/web/platform/database.aspx)합니다. Hello 선택 **Express** (LocalDB) 버전입니다. hello **Express with Tools** 버전에 사용 하는이 자습서에서는 SQL Server Management Studio에 포함 되어 있습니다.
* **SQL Server Management Studio Express** -이 앞에서 설명한 도구 다운로드와 함께 SQL Server 2014 Express hello에 포함 된 하지만 tooinstall 해야 할 경우 것을 별도로 다운로드 하 수 hello에서 설치 [SQL Server Express 다운로드 페이지](http://www.microsoft.com/web/platform/database.aspx)합니다.

hello 자습서는 Azure 구독을 Visual Studio 2013을 설치 해야 하 고 설치 하거나.NET Framework 3.5를 사용 하도록 설정 했으면 있다고 가정 합니다. hello 자습서 hello Azure 하이브리드 연결에 사용할 수 있는 구성에서 SQL Server 2014 Express tooinstall (정적 TCP 포트를 기본 인스턴스)을 기능 하는 방법을 보여 줍니다. Hello 자습서를 시작 하기 전에 SQL Server가 설치 되지 않은 경우 위에서 언급 한 hello 위치에서 SQL Server 2014 Express with Tools를 다운로드 합니다.

### <a name="notes"></a>참고 사항
toouse 온-프레미스 SQL Server 또는 SQL Server Express 데이터베이스 하이브리드 연결 된 TCP/IP toobe 고정 포트에서 사용 하도록 설정 해야 합니다. SQL Server의 기본 인스턴스에서는 고정 포트 1433을 사용하는 반면 명명된 인스턴스에서는 이 포트를 사용하지 않습니다.

hello 온-프레미스 하이브리드 연결 관리자 에이전트를 설치 하는 hello 컴퓨터:

* 통해 아웃 바운드 연결 tooAzure 있어야 합니다.

| 포트 | 이유 |
| --- | --- |
| 80 |**필요하며** 선택적으로 데이터 연결에 필요합니다. |
| 443 |**선택사항** 입니다. 아웃 바운드 연결 too443 사용할 수 없는 경우 TCP 포트 80이 사용 됩니다. |
| 5671 및 9352 |**권장** 하지만 선택사항입니다. 이 모드를 사용하면 일반적으로 더 높은 처리량을 얻을 수 있습니다. 아웃 바운드 연결 toothese 포트를 사용할 수 없는 경우에 TCP 포트 443 사용 됩니다. |

* 수 tooreach hello 있어야 *hostname*:*portnumber* 온-프레미스 리소스의 합니다.

이 문서의 단계 hello hello 브라우저 hello 온-프레미스 하이브리드 연결 에이전트를 호스트 하는 hello 컴퓨터에서 사용 하는 것을 가정 합니다.

구성에서 하 고 위에서 설명한 hello 조건을 충족 하는 환경에서 설치 된 SQL Server를 이미 있는 경우에 바로 이동 하 고으로 시작할 수 있습니다 [온-프레미스 SQL Server 데이터베이스를 만들](#CreateSQLDB)합니다.

<a name="InstallSQL"></a>

## <a name="a-install-sql-server-express-enable-tcpip-and-create-a-sql-server-database-on-premises"></a>A. SQL Server Express 설치, TCP/IP 사용 및 SQL Server 데이터베이스 온-프레미스 만들기
이 섹션 tooinstall SQL Server Express에서 TCP/IP를 활성화 하 고 웹 응용 프로그램은 Azure 포털 hello로 작동할 수 있도록 데이터베이스를 만들 하는 방법을 보여줍니다.

### <a name="install-sql-server-express"></a>SQL Server Express 설치
1. SQL Server Express tooinstall hello 실행 **SQLEXPRWT_x64_ENU.exe** 또는 **SQLEXPR_x86_ENU.exe** 다운로드 한 파일입니다. hello SQL Server 설치 센터 마법사가 나타납니다.
   
    ![SQL Server 설치][SQLServerInstall]
2. 선택 **새 SQL Server 독립 실행형 설치 또는 추가 기능 tooan 기존 설치**합니다. Toohello에 도달할 때까지 hello 기본 선택 항목 및 설정을 적용 하는 hello 지침에 따라 **인스턴스 구성** 페이지.
3. Hello에 **인스턴스 구성** 페이지에서 선택 **기본 인스턴스**합니다.
   
    ![기본 인스턴스 선택][ChooseDefaultInstance]
   
    기본적으로 SQL Server의 기본 인스턴스 hello 하는 어떤 hello 하이브리드 연결 기능을 사용 하려면 정적 포트 1433에서 SQL Server 클라이언트의 요청에 대 한 수신 합니다. 명명된 인스턴스는 하이브리드 연결에서 지원하지 않는 동적 포트 및 UDP를 사용합니다.
4. Hello에 hello 기본값을 적용 **서버 구성** 페이지.
5. Hello에 **데이터베이스 엔진 구성** 페이지의 **인증 모드**, 선택 **혼합 모드 (SQL Server 인증 및 Windows 인증)**, 제공 암호입니다.
   
    ![혼합 모드 선택][ChooseMixedMode]
   
    이 자습서에서는 SQL Server 인증을 사용합니다. 사용자가 제공한 있는지 tooremember hello 암호 때문일 나중에 필요 합니다.
6. Hello 마법사 toocomplete hello 설치 hello 나머지 단계별로 실행 합니다.

### <a name="enable-tcpip"></a>TCP/IP 사용
TCP/IP tooenable SQL Server Express를 설치할 때 설치 된 SQL Server 구성 관리자를 사용 합니다. Hello 단계에 따라 [SQL Server에 대 한 TCP/IP 네트워크 프로토콜을 사용 하도록 설정](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) 계속 하기 전에.

<a name="CreateSQLDB"></a>

### <a name="create-a-sql-server-database-on-premises"></a>SQL Server 데이터베이스 온-프레미스
Visual Studio 웹 응용 프로그램을 사용하려면 Azure에서 액세스할 수 있는 멤버 자격 데이터베이스가 필요합니다. 이렇게 하려면 SQL Server 또는 SQL Server Express 데이터베이스 (하지 hello LocalDB 데이터베이스 기본적으로 MVC 템플릿을 사용 하 여 hello)를 해야 하므로 다음 hello 멤버 자격 데이터베이스를 만들 수 있습니다.

1. SQL Server Management Studio에서 toohello 방금 설치 된 SQL Server를 연결 합니다. (경우 hello **tooServer 연결** 너무 이동 대화 상자를 자동으로 나타나지 않으면**개체 탐색기** hello 왼쪽된 창에서 클릭 **연결**, 클릭하고**데이터베이스 엔진**.) ![TooServer 연결][SSMSConnectToServer]
   
    **서버 유형**으로 **데이터베이스 엔진**을 선택합니다. 에 대 한 **서버 이름**를 사용할 수 있습니다 **localhost** hello의 또는 이름을 사용 하는 hello 컴퓨터. 선택 **SQL Server 인증**, 다음 hello sa 사용자 이름 및 이전에 만든 hello 암호를 사용 하 여 로그인 합니다.
2. toocreate SQL Server Management Studio를 사용 하 여 새 데이터베이스를 마우스 오른쪽 단추로 클릭 **데이터베이스** 에 개체 탐색기, 마우스 클릭 **새 데이터베이스**합니다.
   
    ![새 데이터베이스 만들기][SSMScreateNewDB]
3. Hello에 **새 데이터베이스** 대화 상자에서 MembershipDB hello 데이터베이스 이름에 대 한 입력 한 다음 클릭 **확인**합니다.
   
    ![데이터베이스 이름 입력][SSMSprovideDBname]
   
    만들지 않으면 모든 변경 내용을 toohello 데이터베이스가 시점에서 참고 합니다. hello 멤버 자격 정보 실행 하면 웹 응용 프로그램에 나중에 자동으로 추가할 수 됩니다.
4. 확장 하는 경우 개체 탐색기에서 **데이터베이스**, 해당 hello 멤버 자격 데이터베이스를 만든 표시 됩니다.
   
    ![MembershipDB 생성됨][SSMSMembershipDBCreated]

<a name="CreateSite"></a>

## <a name="b-create-a-web-app-in-hello-azure-portal"></a>B. Hello Azure 포털에서에서 웹 앱 만들기
> [!NOTE]
> 이미 hello이이 자습서에 대 한 toouse 되도록 하는 Azure 포털에서 웹 응용 프로그램을 만들었으면 있습니다 건너뛰어 너무[하이브리드 연결을 만들고 BizTalk 서비스](#CreateHC) 하 고 여기에서 계속 합니다.
> 
> 

1. Hello에 [Azure 포털](https://portal.azure.com), 클릭 **새로** > **웹 + 모바일** > **웹 앱**합니다.
   
    ![새 단추][New]
2. 웹 앱을 구성하고 **만들기**를 클릭합니다.
   
    ![웹 사이트 이름][WebsiteCreationBlade]
3. 몇 분 후 hello 웹 응용 프로그램이 만들어지고 해당 웹 앱 블레이드 나타납니다. hello 블레이드는 웹 앱을 관리할 수 있는 수직으로 스크롤 가능한 한 대시보드입니다.
   
    ![실행 중인 웹 사이트][WebSiteRunningBlade]
   
    tooverify hello 웹 앱이 라이브, hello를 클릭할 수 있는 **찾아보기** 아이콘 toodisplay hello 기본 페이지입니다.

다음으로 hello 웹 앱에 대 한 BizTalk 서비스 및 하이브리드 연결을 만듭니다.

<a name="CreateHC"></a>

## <a name="c-create-a-hybrid-connection-and-a-biztalk-service"></a>C. 하이브리드 연결 및 BizTalk 서비스 만들기
1. 다시 포털 hello에 toosettings 이동 하 고 클릭 **네트워킹** > **하이브리드 연결 끝점 구성**합니다.
   
    ![하이브리드 연결][CreateHCHCIcon]
2. Hello 하이브리드 연결 블레이드에서 클릭 **추가** > **새 하이브리드 연결**합니다.
3. Hello에 **하이브리드 연결** 블레이드:
   
   * 에 대 한 **이름**, hello 연결에 대 한 이름을 제공 합니다.
   * 에 대 한 **Hostname**, SQL Server 호스트 컴퓨터의 hello 컴퓨터 이름을 입력 합니다.
   * 에 대 한 **포트**, 1433 (SQL Server에 대 한 hello 기본 포트)을 입력 합니다.
   * 클릭 **BizTalk 서비스** > **새 BizTalk 서비스** hello BizTalk 서비스에 대 한 이름을 입력 합니다.
     
     ![하이브리드 연결 만들기][TwinCreateHCBlades]
4. **확인** 을 두 번 클릭합니다.
   
    Hello 프로세스가 완료 되 면 hello **알림** 영역 녹색 깜박입니다 **성공** 및 hello **하이브리드 연결** 블레이드는 hello 새 하이브리드 연결을 표시 합니다. 상태를 hello **연결 되어 있지 않은**합니다.
   
    ![1개의 하이브리드 연결 생성됨][CreateHCOneConnectionCreated]

이 시점에서 hello 클라우드 하이브리드 연결 인프라의 중요 한 부분을 완료 했습니다. 이제 해당하는 온-프레미스 부분을 만듭니다.

<a name="InstallHCM"></a>

## <a name="d-install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a>D. Hello 온-프레미스 하이브리드 연결 관리자 toocomplete hello 연결 설치
[!INCLUDE [app-service-hybrid-connections-manager-install](../../includes/app-service-hybrid-connections-manager-install.md)]

Hello 하이브리드 연결 인프라에 완료 되 면 이제 웹 응용 프로그램을 사용 하 여 만들어집니다.

<a name="CreateASPNET"></a>

## <a name="e-create-a-basic-aspnet-web-project-edit-hello-database-connection-string-and-run-hello-project-locally"></a>E. 기본 ASP.NET 웹 프로젝트를 만듭니다 hello 데이터베이스 연결 문자열을 편집 하 고 hello 프로젝트를 로컬로 실행
### <a name="create-a-basic-aspnet-project"></a>기본 ASP.NET 프로젝트 만들기
1. Hello에 Visual Studio에서 **파일** 메뉴에서 새 프로젝트를 만듭니다.
   
    ![새 Visual Studio 프로젝트][HCVSNewProject]
2. Hello에 **템플릿** hello 섹션 **새 프로젝트** 대화 상자에서 **웹** 선택 **ASP.NET 웹 응용 프로그램**, 를클릭한다음 **정상**합니다.
   
    ![ASP.NET 웹 응용 프로그램 선택][HCVSChooseASPNET]
3. Hello에 **새 ASP.NET 프로젝트** 대화 상자에서 선택 **MVC**, 클릭 하 고 **확인**합니다.
   
    ![MVC 선택][HCVSChooseMVC]
4. Hello 프로젝트를 만든 hello 응용 프로그램 추가 정보 페이지가 표시 됩니다. Hello 웹 프로젝트를 아직 실행 하지 마십시오.
   
    ![추가 정보 페이지][HCVSReadmePage]

### <a name="edit-hello-database-connection-string-for-hello-application"></a>Hello 응용 프로그램에 대 한 hello 데이터베이스 연결 문자열 편집
이 단계에서는 응용 프로그램에 알리는 hello 연결 문자열을 편집할 위치 toofind 로컬 SQL Server Express 데이터베이스입니다. hello 연결 문자열은 hello 응용 프로그램에 대 한 구성 정보를 포함 하는 hello 응용 프로그램의 Web.config 파일에 있습니다.

> [!NOTE]
> 응용 프로그램에서 SQL Server Express 및 하지 hello 하나 Visual Studio의 기본 LocalDB에서에서 만든 hello 데이터베이스를 사용 하는 tooensure는 프로젝트를 실행 하기 전에이 단계를 완료 합니다.
> 
> 

1. 솔루션 탐색기에서 hello Web.config 파일을 두 번 클릭 합니다.
   
    ![Web.config][HCVSChooseWebConfig]
2. Hello 편집 **connectionStrings** 섹션 toopoint toohello SQL Server 데이터베이스에 다음 예제는 hello의 hello 구문 다음 로컬 컴퓨터에:
   
    ![연결 문자열][HCVSConnectionString]
   
    Hello 연결 문자열을 작성할 때 염두 hello 다음에 유의 하십시오.
   
   * 명명 된 인스턴스 (예를 들어 YourServer\SQLEXPRESS) 기본 인스턴스 대신 tooa을 연결 하는 경우에 SQL Server toouse 정적 포트를 구성 해야 합니다. 정적 포트를 구성 하는 방법에 대 한 정보를 참조 하십시오. [어떻게 특정 포트에서 SQL Server toolisten tooconfigure](http://support.microsoft.com/kb/823938)합니다. 기본적으로, 명명된 인스턴는 하이브리드 연결에서 지원되지 않는 UDP 및 동적 포트를 사용합니다.
   * Hello를 지정 하는 것이 좋습니다. 로컬 SQL Server TCP 설정 개이고 hello 올바른 포트를 사용 하는 확인할 수 있도록 hello 연결 문자열에 포트 (1433 hello 예제에서와 같이 기본적으로).
   * Toouse SQL Server 인증 tooconnect, 연결 문자열에 hello 사용자 ID와 암호를 지정 해야 합니다.
3. 클릭 **저장** Visual Studio toosave hello Web.config 파일에 있습니다.

### <a name="run-hello-project-locally-and-register-a-new-user"></a>Hello 프로젝트를 로컬로 실행 하 고 새 사용자 등록
1. 디버그 아래의 hello 찾아보기 단추를 클릭 하 여 새 웹 프로젝트를 로컬로 실행 이제 합니다. 이 예에서는 Internet Explorer를 사용합니다.
   
    ![프로젝트 실행][HCVSRunProject]
2. Hello hello 기본 웹 페이지의 오른쪽 위에, 선택 **등록** tooregister 새 계정:
   
    ![새 계정 등록][HCVSRegisterLocally]
3. 사용자 이름 및 암호를 입력합니다.
   
    ![사용자 이름 및 암호를 입력합니다.][HCVSCreateNewAccount]
   
    이 응용 프로그램에 대 한 hello 멤버 자격 정보를 보유 하는 로컬 SQL Server에 데이터베이스를 자동으로 만듭니다. Hello 테이블 중 하나 (**dbo입니다. AspNetUsers**) 보류 웹 hello 방금 입력 한 것 처럼 응용 프로그램 사용자 자격 증명입니다. Hello 자습서의 뒷부분에서이 테이블에 표시 됩니다.
4. Hello 기본 웹 페이지의 hello 브라우저 창을 닫습니다. Visual Studio에서 hello 응용 프로그램을 중지합니다.

Hello 다음 단계를 toopublish hello 응용 프로그램 tooAzure는 이제 하 고 테스트 합니다.

<a name="PubNTest"></a>

## <a name="f-publish-hello-web-application-tooazure-and-test-it"></a>F. 웹 응용 프로그램 tooAzure hello를 게시 하 고 테스트
프로그램 응용 프로그램 tooyour 앱 서비스 웹 앱을 게시 toosee hello 하이브리드 연결을 이전에 구성한는 방법을 테스트 하는 이제 tooconnect 사용 되는 로컬 컴퓨터에 웹 앱 toohello 데이터베이스 되 고 있습니다.

### <a name="publish-hello-web-application"></a>Hello 웹 응용 프로그램 게시
1. Hello hello Azure 포털의에서 앱 서비스 웹 앱에 대 한 게시 프로필을 다운로드할 수 있습니다. 웹 앱에 대 한 hello 블레이드에서 클릭 **Get 게시 프로필**, hello 파일 tooyour 컴퓨터를 저장 합니다.
   
    ![게시 프로필 다운로드][PortalDownloadPublishProfile]
   
    이제 이 파일을 Visual Studio 웹 응용 프로그램으로 가져옵니다.
2. Visual Studio에서 솔루션 탐색기에서 hello 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다.
   
    ![게시 선택][HCVSRightClickProjectSelectPublish]
3. Hello에 **웹 게시** 대화 상자의 hello에서 **프로필** 탭에서 선택 **가져오기**합니다.
   
    ![가져오기][HCVSPublishWebDialogImport]
4. 찾아보기 tooyour 게시 프로필 다운로드를 선택한 다음 클릭 **확인**합니다.
   
    ![Tooprofile 찾아보기][HCVSBrowseToImportPubProfile]
5. 게시 정보를 가져와서 hello에 표시 **연결** hello 대화 상자의 탭 합니다.
   
    ![게시 클릭][HCVSClickPublish]
   
    **게시**를 클릭합니다.
   
    게시 완료 되 면 브라우저를 시작 하 고 않는다는 점을 제외 하면 이제 hello Azure 클라우드 동시에 이제 친숙 한 ASP.NET 응용 프로그램-표시 됩니다!

다음으로 라이브 웹 응용 프로그램 toosee 하이브리드 연결에서에서 사용할 동작입니다.

### <a name="test-hello-completed-web-application-on-azure"></a>테스트 hello Azure에서 웹 응용 프로그램을 완료
1. Hello 위에 Azure에서 웹 페이지의 오른쪽 선택 **로그인**합니다.
   
    ![로그인 테스트][HCTestLogIn]
2. 이제 웹 앱을 앱 서비스 tooyour 웹 응용 프로그램의 멤버 자격 데이터베이스를 로컬 컴퓨터를 연결 합니다. tooverify hello hello 로컬에 입력 한 동일한 자격 증명 이전 데이터베이스를 사용 하 여이 로그 합니다.
   
    ![Hello 인사][HCTestHelloContoso]
3. toofurther 새 하이브리드 연결을 테스트 하 고, 로그 오프 Azure 웹 응용 프로그램, 다른 사용자로 등록 합니다. 새 사용자 이름 및 암호를 입력한 다음 **등록**을 클릭합니다.
   
    ![다른 사용자 테스트 등록][HCTestRegisterRelecloud]
4. tooverify hello 새 사용자의 자격 증명 하이브리드 연결을 통해 로컬 데이터베이스에 저장 되어 있는 로컬 컴퓨터에 SQL Management Studio를 엽니다. 개체 탐색기에서 확장 hello **MembershipDB** 데이터베이스를 선택한 다음 확장 **테이블**합니다. 마우스 오른쪽 단추로 클릭 hello **dbo입니다. AspNetUsers** 멤버 자격 테이블을 선택 **상위 1000 개 행 선택** tooview hello 결과입니다.
   
    ![Hello 결과 보기][HCTestSSMSTree]
5. 로컬 멤버 자격 테이블에는 이제 두 계정-로컬에서 만든 hello 및 hello hello Azure 클라우드에서에서 만든 하나 표시 됩니다. Azure의 하이브리드 연결 기능을 통해 온-프레미스 데이터베이스 tooyour hello 클라우드에서 만든 hello 저장 되었습니다.
   
    ![온-프레미스 데이터베이스에 등록된 사용자][HCTestShowMemberDb]

이제 만들고 hello Azure 클라우드의에서 웹 앱 및 온-프레미스 SQL Server 데이터베이스 간의 하이브리드 연결을 사용 하 여 ASP.NET 웹 응용 프로그램을 배포 합니다. 축하합니다.

## <a name="see-also"></a>참고 항목
[하이브리드 연결 개요](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[Josh Twist가 소개하는 하이브리드 연결(채널 9 비디오)(영문)](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[하이브리드 연결 개요](/services/biztalk-services/)

[BizTalk 서비스: 대시보드, 모니터, 확장, 구성 및 하이브리드 연결 탭](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[원활한 응용 프로그램 이식성으로 실시간 하이브리드 연결 클라우드 구축(채널 9 비디오)(영문)](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[Azure App Service에서 하이브리드 연결을 사용하여 온-프레미스 리소스에 액세스](web-sites-hybrid-connection-get-started.md)

[ASP.NET ID 개요(영문)](http://www.asp.net/identity)

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

<!-- IMAGES -->
[SQLServerInstall]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A01SQLServerInstall.png
[ChooseDefaultInstance]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A02ChooseDefaultInstance.png
[ChooseMixedMode]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A03ChooseMixedMode.png
[SSMSConnectToServer]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A04SSMSConnectToServer.png
[SSMScreateNewDB]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A05SSMScreateNewDBlh.png
[SSMSprovideDBname]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A06SSMSprovideDBname.png
[SSMSMembershipDBCreated]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A07SSMSMembershipDBCreated.png
[New]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B01New.png
[NewWebsite]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B02NewWebsite.png
[WebsiteCreationBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B03WebsiteCreationBlade.png
[WebSiteRunningBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B04WebSiteRunningBlade.png
[Browse]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B05Browse.png
[DefaultWebSitePage]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B06DefaultWebSitePage.png
[CreateHCHCIcon]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C01CreateHCHCIcon.png
[CreateHCAddHC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C02CreateHCAddHC.png
[TwinCreateHCBlades]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C03TwinCreateHCBlades.png
[CreateHCCreateBTS]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C04CreateHCCreateBTS.png
[CreateBTScomplete]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C05CreateBTScomplete.png
[CreateHCSuccessNotification]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C06CreateHCSuccessNotification.png
[CreateHCOneConnectionCreated]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C07CreateHCOneConnectionCreated.png
[HCIcon]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D01HCIcon.png
[NotConnected]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D02NotConnected.png
[NotConnectedBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D03NotConnectedBlade.png
[ClickListenerSetup]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D04ClickListenerSetup.png
[ClickToInstallHCM]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D05ClickToInstallHCM.png
[ApplicationRunWarning]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D06ApplicationRunWarning.png
[UAC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D07UAC.png
[HCMInstalling]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D08HCMInstalling.png
[HCMInstallComplete]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D09HCMInstallComplete.png
[HCStatusConnected]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D10HCStatusConnected.png
[HCVSNewProject]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E01HCVSNewProject.png
[HCVSChooseASPNET]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E02HCVSChooseASPNET.png
[HCVSChooseMVC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E03HCVSChooseMVC.png
[HCVSReadmePage]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E04HCVSReadmePage.png
[HCVSChooseWebConfig]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E05HCVSChooseWebConfig.png
[HCVSConnectionString]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E06HCVSConnectionString.png
[HCVSRunProject]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E06HCVSRunProject.png
[HCVSRegisterLocally]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E07HCVSRegisterLocally.png
[HCVSCreateNewAccount]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E08HCVSCreateNewAccount.png
[PortalDownloadPublishProfile]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F01PortalDownloadPublishProfile.png
[HCVSPublishProfileInDownloadsFolder]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F02HCVSPublishProfileInDownloadsFolder.png
[HCVSRightClickProjectSelectPublish]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F03HCVSRightClickProjectSelectPublish.png
[HCVSPublishWebDialogImport]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F04HCVSPublishWebDialogImport.png
[HCVSBrowseToImportPubProfile]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F05HCVSBrowseToImportPubProfile.png
[HCVSClickPublish]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F06HCVSClickPublish.png
[HCTestLogIn]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F07HCTestLogIn.png
[HCTestHelloContoso]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F08HCTestHelloContoso.png
[HCTestRegisterRelecloud]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F09HCTestRegisterRelecloud.png
[HCTestSSMSTree]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F10HCTestSSMSTree.png
[HCTestShowMemberDb]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F11HCTestShowMemberDb.png
