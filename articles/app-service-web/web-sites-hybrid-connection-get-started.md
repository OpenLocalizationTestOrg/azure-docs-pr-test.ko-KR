---
title: "aaaAccess 온-프레미스 하이브리드 연결을 사용 하 여 Azure 앱 서비스의 리소스"
description: "Azure 앱 서비스의 웹 앱과 정적 TCP 포트를 사용하는 온-프레미스 리소스 간의 연결 만들기"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: a46ed26b-df8e-4fc3-8e05-2d002a6ee508
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: cephalin
ms.openlocfilehash: de7c57b94f4bd6250a93757817178e8455daae4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="access-on-premises-resources-using-hybrid-connections-in-azure-app-service"></a>Azure 앱 서비스에서 하이브리드 연결을 사용하여 온-프레미스 리소스에 액세스
SQL Server, MySQL, HTTP 웹 Api 및 대부분의 사용자 지정 웹 서비스와 같은 정적 TCP 포트를 사용 하는 Azure 앱 서비스 앱 tooany 온-프레미스 리소스를 연결할 수 있습니다. 이 문서에서는 어떻게 toocreate 응용 프로그램 서비스와 온-프레미스 SQL Server 데이터베이스 간의 하이브리드 연결 합니다.

> [!NOTE]
> hello 하이브리드 연결 기능은의 hello 웹 응용 프로그램 부분은 hello에만 사용할 수 있는 [Azure 포털](https://portal.azure.com)합니다. BizTalk 서비스의 연결 toocreate 참조 [하이브리드 연결](http://go.microsoft.com/fwlink/p/?LinkID=397274)합니다. 
> 
> 이 콘텐츠에 Azure 앱 서비스에서 tooMobile 앱도 적용 됩니다. 
> 
> 

## <a name="prerequisites"></a>필수 조건
* Azure 구독. 무료 구독에 대해서는 [Azure 1개월 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요. 
  
    Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다. 신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.
* toouse 온-프레미스 SQL Server 또는 SQL Server Express 데이터베이스 하이브리드 연결 된 TCP/IP toobe 고정 포트에서 사용 하도록 설정 해야 합니다. SQL Server의 기본 인스턴스는 고정 포트 1433을 사용하므로 권장됩니다. 설치 및 하이브리드 연결 사용 하기 위해 SQL Server Express를 구성에 대 한 자세한 내용은 참조 하십시오. [연결 tooan 온-프레미스 SQL Server 하이브리드 연결을 사용 하 여 Azure 웹 사이트에서](http://go.microsoft.com/fwlink/?LinkID=397979)합니다.
* 에이 문서의 뒷부분에 설명 하는 hello 온-프레미스 하이브리드 연결 관리자 에이전트를 설치 하는 hello 컴퓨터:
  
  * 포트 5671 통해 수 tooconnect tooAzure 이어야 합니다.
  * 수 tooreach hello 있어야 *hostname*:*portnumber* 온-프레미스 리소스의 합니다. 

> [!NOTE]
> 이 문서의 단계 hello hello 브라우저 hello 온-프레미스 하이브리드 연결 에이전트를 호스트 하는 hello 컴퓨터에서 사용 하는 것을 가정 합니다.
> 
> 

## <a name="create-a-web-app-in-hello-azure-portal"></a>Hello Azure 포털에서에서 웹 앱 만들기
> [!NOTE]
> 이미 만든 웹 응용 프로그램 또는 모바일 앱 백 엔드에서 hello이이 자습서에 대 한 toouse 되도록 하는 Azure 포털에서 있습니다 건너뛰어 너무[하이브리드 연결을 만들고 BizTalk 서비스](#CreateHC) 하 고 여기에서 시작 합니다.
> 
> 

1. Hello의 왼쪽된 위 모서리 hello에에서 [Azure 포털](https://portal.azure.com), 클릭 **새로** > **웹 + 모바일** > **웹 앱**합니다.
   
    ![새 웹 앱][NewWebsite]
2. Hello에 **웹 앱** 블레이드에서 URL을 입력 하 고 클릭 **만들기**합니다. 
   
    ![웹 사이트 이름][WebsiteCreationBlade]
3. 몇 분 후 hello 웹 응용 프로그램이 만들어지고 해당 웹 앱 블레이드 나타납니다. hello 블레이드는 사이트를 관리할 수 있는 수직으로 스크롤 가능한 한 대시보드입니다.
   
    ![실행 중인 웹 사이트][WebSiteRunningBlade]
4. tooverify hello 사이트는 라이브, hello를 클릭할 수 있는 **찾아보기** 아이콘 toodisplay hello 기본 페이지입니다.
   
    ![웹 앱 찾아보기 toosee를 클릭 합니다.][Browse]
   
    ![기본 웹 앱 페이지][DefaultWebSitePage]

다음으로 hello 웹 앱에 대 한 BizTalk 서비스 및 하이브리드 연결을 만듭니다.

<a name="CreateHC"></a>

## <a name="create-a-hybrid-connection-and-a-biztalk-service"></a>하이브리드 연결 및 BizTalk 서비스 만들기
1. 웹앱 블레이드에서 **모든 설정** > **네트워킹** > **하이브리드 연결 끝점 구성**을 차례로 클릭합니다.
   
    ![하이브리드 연결][CreateHCHCIcon]
2. Hello 하이브리드 연결 블레이드에서 클릭 **추가**합니다.
   
    <!-- ![Add a hybrid connnection][CreateHCAddHC]
   -->
3. hello **하이브리드 연결을 추가할** 블레이드를 엽니다.  첫 번째 하이브리드 연결 이므로, hello **새 하이브리드 연결** 옵션은 미리 선택 하 고 hello **하이브리드 연결** 블레이드에서 열립니다.
   
    ![하이브리드 연결 만들기][TwinCreateHCBlades]
   
    Hello에 **만들기 하이브리드 연결 블레이드**:
   
   * 에 대 한 **이름**, hello 연결에 대 한 이름을 제공 합니다.
   * 에 대 한 **Hostname**, 리소스를 호스트 하는 hello 온-프레미스 컴퓨터의 hello 이름을 입력 합니다.
   * 에 대 한 **포트**, 온-프레미스 리소스 (SQL Server 기본 인스턴스의 경우 1433)를 사용 하는 hello 포트 번호를 입력 합니다.
   * **Biz Talk 서비스**
4. hello **BizTalk 서비스 만들기** 블레이드를 엽니다. BizTalk 서비스를 hello에 대 한 이름을 입력 한 다음 클릭 **확인**합니다.
   
    ![BizTalk 서비스 만들기][CreateHCCreateBTS]
   
    hello **BizTalk 서비스 만들기** 블레이드를 닫고 toohello 반환될지 **하이브리드 연결** 블레이드입니다.
5. Hello 만들기 하이브리드 연결 블레이드에서 클릭 **확인**합니다. 
   
    ![확인 클릭][CreateBTScomplete]
6. Hello 프로세스가 완료 되 면 hello 포털의에서 알림 영역 hello hello 연결이 성공적으로 생성 된 알려 줍니다.
   
    <!--- TODO
   
    Everything fails at this step. I can't create a BizTalk service in hello dogfood portal. I switch toohello classic portal
    (full portal) and created hello BizTalk service but it doesn't seem toolet you connnect them - When you finish the
    Create hybrid conn step, you get hello following error
    Failed toocreate hybrid connection RelecIoudHC. hello 
    resource type could not be found in hello namespace 
    'Microsoft.BizTaIkServices for api version 2014-06-01'.
   
    hello error indicates it couldn't find hello type, not hello instance.
    ![Success notification][CreateHCSuccessNotification]
    -->
7. Hello 웹 앱의 블레이드에서 hello **하이브리드 연결** 아이콘은 이제 1 하이브리드 연결을 이미 만들었다고 보여줍니다.
   
    ![1개의 하이브리드 연결 생성됨][CreateHCOneConnectionCreated]

이 시점에서 hello 클라우드 하이브리드 연결 인프라의 중요 한 부분을 완료 했습니다. 이제 해당하는 온-프레미스 부분을 만듭니다.

<a name="InstallHCM"></a>

## <a name="install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a>Hello 온-프레미스 하이브리드 연결 관리자 toocomplete hello 연결 설치
1. Hello 웹 앱 블레이드 클릭 **모든 설정을** > **네트워킹** > **하이브리드 연결 끝점 구성**합니다. 
   
    ![하이브리드 연결 아이콘][HCIcon]
2. Hello에 **하이브리드 연결** 블레이드, hello **상태** hello에 대 한 열 최근에 추가 하 고 끝점 **연결 되어 있지 않은**합니다. Hello 연결 tooconfigure 클릭 것입니다.
   
    ![연결되지 않음][NotConnected]
   
    hello 하이브리드 연결 블레이드를 엽니다.
   
    ![NotConnectedBlade][NotConnectedBlade]
3. Hello 블레이드에서 클릭 **수신기 설치**합니다.
   
    ![수신기 설정 클릭][ClickListenerSetup]
4. hello **하이브리드 연결 속성** 블레이드를 엽니다. 아래 **온-프레미스 하이브리드 연결 관리자**, 선택 **tooinstall 여기를 클릭**합니다.
   
    ![Tooinstall 여기를 클릭합니다][ClickToInstallHCM]
5. Hello 응용 프로그램 실행 보안 경고 대화 상자에서 선택 **실행** toocontinue 합니다.
   
    ![실행 toocontinue 선택][ApplicationRunWarning]
6. Hello에 **사용자 계정 컨트롤** 대화 상자에서 선택 **예**합니다.
   
   ![예 선택][UAC]
7. hello 하이브리드 연결 관리자 다운로드 되어 자동으로 설치 됩니다. 
   
    ![설치][HCMInstalling]
8. Hello 설치 완료 되 면 클릭 **닫기**합니다.
   
    ![닫기 클릭][HCMInstallComplete]
   
    Hello에 **하이브리드 연결** 블레이드, hello **상태** 열 이제 표시 **연결 됨**합니다. 
   
    ![연결됨 상태][HCStatusConnected]

이제 hello 하이브리드 연결 인프라에 완료 되 면이 사용 하는 하이브리드 응용 프로그램을 만들 수 있습니다. 

> [!NOTE]
> hello 다음 섹션에서는 방법을 보여 줍니다 toouse 하이브리드 모바일 앱.NET 백 엔드 프로젝트와 연결 합니다.
> 
> 

## <a name="configure-hello-mobile-app-net-backend-project-tooconnect-toohello-sql-server-database"></a>Hello 모바일 앱을.NET 백 엔드 프로젝트 tooconnect toohello SQL Server 데이터베이스 구성
앱 서비스에서 모바일 앱 .NET 백 엔드 프로젝트는 추가 모바일 앱 SDK가 설치되고 초기화된 ASP.NET 웹앱입니다. toouse 해야 웹 응용 프로그램을 모바일 앱 백 엔드를 [다운로드 하 고 hello 모바일 앱을.NET 백 엔드 SDK 초기화](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk)합니다.  

모바일 앱에 대 한도 hello 온-프레미스 데이터베이스에 대 한 연결 문자열 toodefine 필요 하 고 hello 백 엔드 toouse이이 연결을 수정 합니다. 

1. 모바일 앱을.NET 백 엔드에 대 한 Web.config 파일을 열고 hello Visual Studio의 솔루션 탐색기에서 찾을 hello **connectionStrings** 섹션에서 어떤 지점 toohello 온-프레미스 SQL, hello 다음과 같은 새 SqlClient 항목 추가 서버 데이터베이스:
   
        <add name="OnPremisesDBConnection"
         connectionString="Data Source=OnPremisesServer,1433;
         Initial Catalog=OnPremisesDB;
         User ID=HybridConnectionLogin;
         Password=<**secure_password**>;
         MultipleActiveResultSets=True"
         providerName="System.Data.SqlClient" />
   
    Tooreplace 기억 `<**secure_password**>` hello 암호에 대해 생성 된이 문자열의 *HybridConnectionLogin*합니다.
2. 클릭 **저장** Visual Studio toosave hello Web.config 파일에 있습니다.
   
   > [!NOTE]
   > 이 연결 설정은 hello 로컬 컴퓨터에서 실행할 때 사용 됩니다. Azure에서 실행 하는 경우이 설정은 hello 포털에 정의 된 hello 연결 설정으로 재정의 됩니다.
   > 
   > 
3. Hello 확장 **모델** 폴더 및 끝나는 열기 hello 데이터 모델 파일을 *Context.cs*합니다.
4. Hello 수정 **DbContext** 인스턴스 생성자 toopass hello 값 `OnPremisesDBConnection` toohello 기본 **DbContext** 생성자, 다음 코드 조각 비슷한 toohello:
   
        public class hybridService1Context : DbContext
        {
            public hybridService1Context()
                : base("OnPremisesDBConnection")
            {
            }
        }
   
    hello 서비스 hello 새 연결 toohello SQL Server 데이터베이스를 사용 합니다.

## <a name="update-hello-mobile-app-backend-toouse-hello-on-premises-connection-string"></a>Hello 모바일 앱 백 엔드 toouse hello 온-프레미스 연결 문자열 업데이트
다음으로, Azure에서 사용할 수 있도록이 새 연결 문자열에 대 한 tooadd 앱 설정이 필요 합니다.  

1. Hello에 다시 [Azure 포털](https://portal.azure.com) hello 웹 앱 백 엔드 코드에서 모바일 앱에 대 한 클릭 **모든 설정을**, 다음 **응용 프로그램 설정**합니다.
2. Hello에 **웹 앱 설정** 블레이드에서 너무 아래로 스크롤하여**연결 문자열** 는 새로 추가 **SQL Server** 라는 연결 문자열 `OnPremisesDBConnection` 같은값으로`Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.
   
    대체 `<**secure_password**>` hello 온-프레미스 데이터베이스에 대 한 보안 암호를 사용 합니다.
   
    ![온-프레미스 데이터베이스에 대한 연결 문자열](./media/web-sites-hybrid-connection-get-started/set-sql-server-database-connection.png)
3. 키를 눌러 **저장** 방금 만든 toosave hello 하이브리드 연결 및 연결 문자열입니다.

이 시점에서 hello 서버 프로젝트를 다시 게시 하 고 기존 모바일 앱 클라이언트에 hello 새 연결을 테스트할 수 있습니다. 데이터에서 읽이 되며 hello 하이브리드 연결을 사용 하 여 toohello 온-프레미스 데이터베이스를 작성 합니다.

<a name="NextSteps"></a>

## <a name="next-steps"></a>다음 단계
* 하이브리드 연결을 사용 하 여 ASP.NET 웹 응용 프로그램을 만드는 방법에 대 한 정보를 참조 하십시오. [연결 tooan 온-프레미스 SQL Server 하이브리드 연결을 사용 하 여 Azure 웹 사이트에서](http://go.microsoft.com/fwlink/?LinkID=397979)합니다. 

### <a name="additional-resources"></a>추가 리소스
[하이브리드 연결 개요](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[Josh Twist가 소개하는 하이브리드 연결(채널 9 비디오)(영문)](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[하이브리드 연결 웹 사이트](https://azure.microsoft.com/services/biztalk-services/)

[BizTalk 서비스: 대시보드, 모니터, 확장, 구성 및 하이브리드 연결 탭](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[원활한 응용 프로그램 이식성으로 실시간 하이브리드 연결 클라우드 구축(채널 9 비디오)(영문)](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[연결 tooan 온-프레미스 하이브리드 연결 (Channel 9 비디오)를 사용 하 여 Azure 모바일 서비스에서 SQL Server](http://channel9.msdn.com/Series/Windows-Azure-Mobile-Services/Connect-to-an-on-premises-SQL-Server-from-Azure-Mobile-Services-using-Hybrid-Connections)

## <a name="whats-changed"></a>변경된 내용
* 웹 사이트 tooApp 서비스에서에서 변경 사항 참조 가이드 toohello: [기존 Azure 서비스에 대 한 해당 영향 및 Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- IMAGES -->
[New]:./media/web-sites-hybrid-connection-get-started/B01New.png
[NewWebsite]:./media/web-sites-hybrid-connection-get-started/B02NewWebsite.png
[WebsiteCreationBlade]:./media/web-sites-hybrid-connection-get-started/B03WebsiteCreationBlade.png
[WebSiteRunningBlade]:./media/web-sites-hybrid-connection-get-started/B04WebSiteRunningBlade.png
[Browse]:./media/web-sites-hybrid-connection-get-started/B05Browse.png
[DefaultWebSitePage]:./media/web-sites-hybrid-connection-get-started/B06DefaultWebSitePage.png
[CreateHCHCIcon]:./media/web-sites-hybrid-connection-get-started/C01CreateHCHCIcon.png
[CreateHCAddHC]:./media/web-sites-hybrid-connection-get-started/C02CreateHCAddHC.png
[TwinCreateHCBlades]:./media/web-sites-hybrid-connection-get-started/C03TwinCreateHCBlades.png
[CreateHCCreateBTS]:./media/web-sites-hybrid-connection-get-started/C04CreateHCCreateBTS.png
[CreateBTScomplete]:./media/web-sites-hybrid-connection-get-started/C05CreateBTScomplete.png
[CreateHCSuccessNotification]:./media/web-sites-hybrid-connection-get-started/C06CreateHCSuccessNotification.png
[CreateHCOneConnectionCreated]:./media/web-sites-hybrid-connection-get-started/C07CreateHCOneConnectionCreated.png
[HCIcon]:./media/web-sites-hybrid-connection-get-started/D01HCIcon.png
[NotConnected]:./media/web-sites-hybrid-connection-get-started/D02NotConnected.png
[NotConnectedBlade]:./media/web-sites-hybrid-connection-get-started/D03NotConnectedBlade.png
[ClickListenerSetup]:./media/web-sites-hybrid-connection-get-started/D04ClickListenerSetup.png
[ClickToInstallHCM]:./media/web-sites-hybrid-connection-get-started/D05ClickToInstallHCM.png
[ApplicationRunWarning]:./media/web-sites-hybrid-connection-get-started/D06ApplicationRunWarning.png
[UAC]:./media/web-sites-hybrid-connection-get-started/D07UAC.png
[HCMInstalling]:./media/web-sites-hybrid-connection-get-started/D08HCMInstalling.png
[HCMInstallComplete]:./media/web-sites-hybrid-connection-get-started/D09HCMInstallComplete.png
[HCStatusConnected]:./media/web-sites-hybrid-connection-get-started/D10HCStatusConnected.png
