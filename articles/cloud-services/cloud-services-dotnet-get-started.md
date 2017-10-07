---
title: "Azure 클라우드 서비스 및 ASP.NET 시작: aaaGet | Microsoft Docs"
description: "자세한 내용은 방법 toocreate ASP.NET MVC 및 Azure를 사용 하 여 다중 계층 응용 프로그램입니다. hello 앱 웹 역할과 작업자 역할에는 클라우드 서비스에서 실행 됩니다. Entity Framework, SQL 데이터베이스 및 Azure 저장소 큐와 Blob를 사용합니다."
services: cloud-services, storage
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: d7aa440d-af4a-4f80-b804-cc46178df4f9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/15/2017
ms.author: adegeo
ms.openlocfilehash: 86271c29b79fad3f01f8ea0e88fd00c7aefc970c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cloud-services-and-aspnet"></a>Azure 클라우드 서비스 및 ASP.NET 시작

## <a name="overview"></a>개요
이 자습서에서는 어떻게 toocreate 프런트 엔드, ASP.NET mvc는 다층 계층.NET 응용 프로그램 및 tooan 배포 [Azure 클라우드 서비스](cloud-services-choose-me.md)합니다. 응용 프로그램에서는 hello [Azure SQL 데이터베이스](http://msdn.microsoft.com/library/azure/ee336279), hello [Azure Blob 서비스](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), 및 hello [Azure 큐 서비스](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern)합니다. 있습니다 수 [hello Visual Studio 프로젝트를 다운로드](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) hello MSDN 코드 갤러리에서에서 합니다.

표시 하는 hello 자습서 toobuild 및 실행 hello 응용 프로그램을 로컬로 어떻게 toodeploy 것 tooAzure 및 연속된 hello 클라우드 방법과 toobuild 처음부터 것입니다. 처음부터 작성 하 여 시작 하 고 닫을 수 테스트 hello 있고 원하는 경우 단계를 나중에 배포 합니다.

## <a name="contoso-ads-application"></a>Contoso Ads 응용 프로그램
hello 응용 프로그램에는 광고 게시판입니다. 사용자는 텍스트를 입력하고 이미지를 업로드하여 광고를 만듭니다. 축소판 이미지와 광고 목록을 볼 수 있습니다 및 광고 toosee hello 세부 정보를 선택할 때 hello에 전체 이미지를 볼 수 있습니다.

![광고 목록](./media/cloud-services-dotnet-get-started/list.png)

hello 응용 프로그램 hello를 사용 하 여 [큐 중심 작업 패턴](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff 부하 CPU를 많이 사용 hello 만드는 작업을 미리 보기 tooa 백 엔드 프로세스입니다.

## <a name="alternative-architecture-websites-and-webjobs"></a>대체 아키텍처: 웹 사이트 및 WebJobs
이 자습서에서는 어떻게 toorun 프런트 엔드 및 백 엔드는 Azure에서 클라우드 서비스입니다. 대신은 toorun hello에 프런트 엔드는 [Azure 웹 사이트](/services/web-sites/) hello를 사용 하 여 [WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226) hello 백 엔드에 대 한 (현재 미리 보기)의 기능입니다. 에서 WebJobs을 사용 하는 방법에 대 한 참조 [hello Azure WebJobs SDK 시작](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)합니다. 시나리오에 적합 하는 방법을 toochoose hello 서비스를 가장 하는 방법에 대 한 정보를 참조 하세요. [Azure 웹 사이트, 클라우드 서비스 및 가상 컴퓨터 비교](../app-service-web/choose-web-site-cloud-service-vm.md)합니다.

## <a name="what-youll-learn"></a>학습할 내용
* 어떻게 tooenable 시스템에 설치 하 여 Azure 개발 hello Azure SDK입니다.
* 어떻게 toocreate Visual Studio 클라우드 서비스 프로젝트는 ASP.NET MVC 웹 역할 및 작업자 역할입니다.
* 어떻게 tootest 클라우드 서비스 프로젝트를 로컬로 hello Azure 저장소 에뮬레이터를 사용 하 여 hello 합니다.
* 어떻게 toopublish hello 클라우드 프로젝트 tooan Azure 클라우드 서비스와 Azure 저장소 계정을 사용 하 여 테스트 합니다.
* Tooupload 파일 방법과 hello Azure Blob 서비스에 저장 합니다.
* 어떻게 toouse hello 계층 간 통신에 대 한 Azure 큐 서비스입니다.

## <a name="prerequisites"></a>필수 조건
hello 자습서 알고 있다고 가정 [클라우드 서비스를 Azure에 대 한 기본 개념](cloud-services-choose-me.md) 같은 *웹 역할* 및 *작업자 역할* 용어입니다.  또한 알고 있다고 가정 어떻게와 toowork [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) 또는 [Web Forms](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) Visual Studio의 프로젝트입니다. hello 예제 응용 프로그램 MVC를 사용 하지만 tooWeb Forms 대부분의 hello 자습서에도 적용 됩니다.

Azure 구독을 하지 않고 로컬 hello 앱을 실행할 수는 있지만 한 toodeploy hello 응용 프로그램 toohello 클라우드 필요 합니다. 계정이 없는 경우 [MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668)하거나 [무료 평가판을 등록](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668)할 수 있습니다.

hello 자습서 지침은 hello 제품을 다음 중 하나로 작동 합니다.

* Visual Studio 2013
* Visual Studio 2015
* Visual Studio 2017

다음 중 하나에 없을 경우 hello Azure SDK를 설치 하면 Visual Studio 자동으로 설치 될 수 있습니다.

## <a name="application-architecture"></a>응용 프로그램 아키텍처
hello 응용 프로그램을 Entity Framework Code First toocreate hello 테이블과 hello 데이터 액세스를 사용 하 여 SQL 데이터베이스에 광고를 저장 합니다. 각 광고에 대 한 hello 데이터베이스 저장소 두 Url에 대 한 전체 크기 이미지와 hello 미리 보기에 대 한 하나의 hello 합니다.

![광고 테이블](./media/cloud-services-dotnet-get-started/adtable.png)

사용자 이미지를 업로드 하면에 hello 이미지를 저장 웹 역할에서 프런트 엔드 실행 hello는 [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), toohello blob을 가리키는 URL 사용 하 여 hello 데이터베이스의 hello ad 정보를 저장 하 고 있습니다. At hello 동일 time, 메시지 tooan Azure 큐를 씁니다. 작업자 역할에서 정기적으로 실행 하는 백 엔드 프로세스는 새 메시지에 대 한 hello 큐를 폴링합니다. 새 메시지가 표시 되 면 hello 작업자 역할을 만들고 해당 이미지에 대 한 미리 보기 하며 업데이트 hello 해당 ad에 대 한 축소판 그림 URL 데이터베이스 필드 hello 다음 그림에 hello 응용 프로그램의 hello 부분 어떻게 상호 작용 합니다.

![Contoso Ads 아키텍처](./media/cloud-services-dotnet-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]

## <a name="download-and-run-hello-completed-solution"></a>다운로드 하 고 완료 하는 hello 솔루션 실행
1. 다운로드 하 고 hello 압축을 풀면 [솔루션 완료](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4)합니다.
2. Visual Studio를 시작합니다.
3. Hello에서 **파일** 메뉴 선택 **프로젝트 열기**hello 솔루션을 다운로드 한 toowhere 이동한 다음 hello 솔루션 파일을 엽니다.
4. CTRL + SHIFT + B toobuild hello 솔루션 키를 누릅니다.

    기본적으로 Visual Studio 자동으로 복원 hello에 포함 되지 않은 hello NuGet 패키지 콘텐츠를 *.zip* 파일입니다. Hello 패키지를 복원 하지 마십시오 하 여 수동으로 설치 거 toohello **솔루션에 대 한 NuGet 패키지 관리** hello를 클릭 하 고 대화 상자 **복원** hello 상단 오른쪽에 있는 단추입니다.
5. **솔루션 탐색기**, 다음 사항을 확인 **ContosoAdsCloudService** hello 시작 프로젝트로 선택 합니다.
6. Visual Studio 2015를 사용 하는 하거나 이상 hello 응용 프로그램에서 hello SQL Server 연결 문자열을 변경 *Web.config* hello ContosoAdsWeb 프로젝트의 파일과 hello에 *ServiceConfiguration.Local.cscfg* hello ContosoAdsCloudService 프로젝트의 파일입니다. 각각의 경우 "(localdb) \v11.0"를도 변경 "(localdb) \MSSQLLocalDB"입니다.
7. CTRL + f 5 toorun hello 응용 프로그램 키를 누릅니다.

    클라우드 서비스 프로젝트를 로컬로 실행할 때 Visual Studio hello Azure에서 자동으로 호출 *계산 에뮬레이터* 및 Azure *저장소 에뮬레이터*합니다. hello는 컴퓨터의 리소스 toosimulate hello 웹 역할 및 작업자 역할 환경을 사용 하 여 에뮬레이터를 계산 합니다. 사용 하 여 hello 저장소 에뮬레이터는 [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) 데이터베이스 toosimulate Azure 클라우드 저장소입니다.

    hello 처음으로 클라우드 서비스 프로젝트를 실행 하면 걸리는 1 분 정도를 에뮬레이터 toostart hello에 대 한 합니다. 에뮬레이터 시작이 완료 되 면 hello 기본 브라우저 toohello 응용 프로그램 홈 페이지를 엽니다.

    ![Contoso Ads 아키텍처](./media/cloud-services-dotnet-get-started/home.png)
8. **광고 만들기**를 클릭합니다.
9. 테스트 데이터를 입력 하 고 선택 된 *.jpg* tooupload, 이미지 및 클릭 **만들기**합니다.

    ![만들기 페이지](./media/cloud-services-dotnet-get-started/create.png)

    hello 앱 toohello 인덱스 페이지 까지일 처리 하는 아직 만들어지지 않은 때문에 새 ad hello에 대 한 미리 보기 표시 되지는 않습니다.
10. 잠시 기다린 후 toosee hello 축소판 그림 hello 인덱스 페이지를 새로 고 치세요.

     ![인덱스 페이지](./media/cloud-services-dotnet-get-started/list.png)
11. 클릭 **세부 정보** ad toosee hello 큰 이미지에 대 한 합니다.

     ![자세히 페이지](./media/cloud-services-dotnet-get-started/details.png)

연결 toohello 클라우드가 없는 로컬 컴퓨터에서 전체 hello 응용 프로그램을 실행 했으므로 있습니다. hello 저장소 에뮬레이터 hello 큐를 저장 하 고 blob 데이터는 SQL Server Express LocalDB 데이터베이스 및 hello 응용 프로그램에 다른 LocalDB 데이터베이스의 hello ad 데이터를 저장 합니다. Entity Framework Code First 자동으로 만들어진된 hello ad 데이터베이스 hello 것 처음으로 hello 웹 앱 tooaccess 시도 합니다.

다음 섹션 hello hello 클라우드에서 실행 될 때 큐, blob 및 hello 응용 프로그램 데이터베이스에 대 한 hello 솔루션 toouse Azure 클라우드 리소스를 구성 합니다. Toocontinue toorun 로컬로 려 해도 클라우드 저장소 및 데이터베이스 리소스를 사용할 경우에서 수행할 수 있습니다. 표시 하는 연결 문자열을 설정할 때의 문제만는 어떻게 toodo 합니다.

## <a name="deploy-hello-application-tooazure"></a>Hello 응용 프로그램 tooAzure 배포
작업 단계 toorun hello 응용 프로그램 hello 클라우드에서 다음 hello:

* Azure 클라우드 서비스를 만듭니다.
* Azure SQL 데이터베이스를 만듭니다.
* Azure 저장소 계정 만들기
* Azure에서 실행 될 때 솔루션 toouse hello Azure SQL 데이터베이스를 구성 합니다.
* Azure에서 실행 될 때 솔루션 toouse hello Azure 저장소 계정을 구성 합니다.
* Hello 프로젝트 tooyour Azure 클라우드 서비스를 배포 합니다.

### <a name="create-an-azure-cloud-service"></a>Azure 클라우드 서비스 만들기
Azure 클라우드 서비스는 hello 환경 hello 응용 프로그램에서 실행 됩니다.

1. 브라우저를 열고 hello [Azure 포털](https://portal.azure.com)합니다.
2. **새로 만들기 > Compute > Cloud Service**를 클릭합니다.

3. Hello DNS 이름 입력된 상자에 hello 클라우드 서비스에 대 한 URL 접두사를 입력 합니다.

    이 URL에 고유한 toobe 있습니다.  선택한 hello 접두사는 이미 사용 하는 경우 오류 메시지가 얻을 수 있습니다.
4. Hello 서비스에 대 한 새 리소스 그룹을 지정 합니다. 클릭 **새로 만들기** 다음 hello 리소스 그룹 입력된 상자에서 CS_contososadsRG 같은 이름을 입력 합니다.

5. Hello를 영역 toodeploy hello 응용 프로그램을 선택 합니다.

    이 필드는 클라우드 서비스가 호스팅될 데이터센터를 지정합니다. 프로덕션 응용 프로그램에 대 한 hello 지역 가장 가까운 tooyour 고객을 선택 합니다. 이 자습서에 대 한 hello 지역 가장 가까운 tooyou를 선택 합니다.
5. **만들기**를 클릭합니다.

    다음 이미지는 hello, 클라우드 서비스 URL CSvccontosoads.cloudapp.net hello로 만들어집니다.

    ![새 클라우드 서비스](./media/cloud-services-dotnet-get-started/newcs.png)

### <a name="create-an-azure-sql-database"></a>Azure SQL 데이터베이스 만들기
Hello 앱 hello 클라우드에서 실행 되 면 클라우드 기반 데이터베이스를 사용 합니다.

1. Hello에 [Azure 포털](https://portal.azure.com), 클릭 **새로 만들기 > 데이터베이스 > SQL 데이터베이스**합니다.
2. Hello에 **데이터베이스 이름** 상자에 입력 *contosoads*합니다.
3. Hello에 **리소스 그룹**, 클릭 **기존 항목 사용** 및 hello 클라우드 서비스에 사용 되는 선택 hello 리소스 그룹입니다.
4. Hello에서 이미지를 다음 클릭 **서버-필요한 설정 구성** 및 **새 서버 만들기**합니다.

    ![터널 toodatabase 서버](./media/cloud-services-dotnet-get-started/newdb.png)

    또는 이미 구독에는 서버가 있으면 해당 서버 hello 드롭 다운 목록에서 선택할 수 있습니다.
5. Hello에 **서버 이름** 상자에 입력 *csvccontosodbserver*합니다.

6. 관리자 **로그인 이름** 및 **암호**를 입력합니다.

    **새 서버 만들기**를 선택한 경우 여기에 기존 이름 및 암호를 입력하면 안됩니다. 새 이름 및 암호를 정의 하는 이제 toouse 나중 hello 데이터베이스에 액세스할 때 입력 합니다. 이전에 만든 서버를 선택한 경우 이미 만든 hello 암호 toohello 관리 사용자 계정에 대 한 라는 메시지가 표시 됩니다.
7. 선택 동일 hello **위치** hello 클라우드 서비스에 대해 선택한 합니다.

    Hello 클라우드 서비스와 데이터베이스가 서로 다른 데이터 센터에 있는 하는 경우 (지역), 지연이 증가할 및 hello 데이터 센터 외부 대역폭에 대 한 청구 됩니다. 데이터 센터 내부 대역폭은 무료입니다.
8. 확인 **허용 azure 서비스 tooaccess 서버**합니다.
9. 클릭 **선택** hello 새 서버에 대 한 합니다.

    ![새 SQL Database 서버](./media/cloud-services-dotnet-get-started/newdbserver.png)
10. **만들기**를 클릭합니다.

### <a name="create-an-azure-storage-account"></a>Azure 저장소 계정 만들기
Azure 저장소 계정을 hello 클라우드에서 큐 및 blob 데이터를 저장 하는 리소스를 제공 합니다.

실제 응용 프로그램에서는 일반적으로 응용 프로그램 데이터와 로깅 데이터를 위한 별도의 계정 및 테스트 데이터와 프로덕션 데이터를 위한 별도의 계정을 만듭니다. 이 자습서에서는 하나의 계정만 사용합니다.

1. Hello에 [Azure 포털](https://portal.azure.com), 클릭 **새로 만들기 > 저장소 > 저장소 계정-blob, 파일, 테이블, 큐**합니다.
2. Hello에 **이름** 상자에 URL 접두사를 입력 합니다.

    이 접두사 이름과 함께 hello 텍스트 hello 상자 아래 hello 고유 URL tooyour 저장소 계정이 됩니다. 다른 사용자가 입력 하는 hello 접두사를 이미 사용 하는 경우 해야 toochoose 접두사는 서로 다릅니다.
3. 집합 hello **배포 모델** 너무*클래식*합니다.

4. 집합 hello **복제** 드롭 다운 목록 너무**로컬 중복 저장소**합니다.

    저장소 계정에 대 한 지리적 복제를 사용 하는 경우 저장 된 hello 콘텐츠인지 복제 tooa 보조 데이터 센터 tooenable 장애 조치 hello 기본 위치에서 중요 재해가 발생 하는 경우. 지역에서 복제는 추가 비용을 발생시킬 수 있습니다. 테스트 및 개발 계정에 대 한 일반적으로 원하지 toopay 지리적 복제에 대 한 합니다. 자세한 내용은 [저장소 계정 만들기, 관리 또는 삭제](../storage/common/storage-create-storage-account.md)를 참조하세요

5. Hello에 **리소스 그룹**, 클릭 **기존 항목 사용** 및 hello 클라우드 서비스에 사용 되는 선택 hello 리소스 그룹입니다.
6. 집합 hello **위치** 드롭 다운 목록 toohello hello 클라우드 서비스에 대해 선택한 동일한 영역입니다.

    Hello 클라우드 서비스와 저장소 계정이 서로 다른 데이터 센터가 있는 경우 (지역), 지연이 증가할 및 hello 데이터 센터 외부 대역폭에 대 한 청구 됩니다. 데이터 센터 내부 대역폭은 무료입니다.

    Azure 선호도 그룹 메커니즘 toominimize hello 거리 간의 대기 시간을 줄일 수 있는 데이터 센터의 리소스를 제공 합니다. 이 자습서는 선호도 그룹을 사용하지 않습니다. 자세한 내용은 참조 [어떻게 tooCreate는 선호도 그룹을 Azure에서](http://msdn.microsoft.com/library/jj156209.aspx)합니다.
7. **만들기**를 클릭합니다.

    ![새 저장소 계정](./media/cloud-services-dotnet-get-started/newstorage.png)

    Hello 이미지에서 저장소 계정을 hello URL로 만든 `csvccontosoads.core.windows.net`합니다.

### <a name="configure-hello-solution-toouse-your-azure-sql-database-when-it-runs-in-azure"></a>Azure에서 실행 될 때 솔루션 toouse hello Azure SQL 데이터베이스 구성
웹 프로젝트 hello hello 작업자 역할 프로젝트 각각에 자체 데이터베이스 연결 문자열 및 Azure의 hello 응용 프로그램을 실행 하는 경우 toopoint toohello Azure SQL 데이터베이스 요구 각각.

사용 하 여 한 [f i g 변환](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) hello 웹 역할과 작업자 역할 hello에 대 한 클라우드 서비스 환경 설정에 대 한 합니다.

> [!NOTE]
> 이 섹션 및 hello 다음 섹션에서는 프로젝트 파일에 자격 증명을 저장 합니다. [중요한 데이터를 공개 소스 코드 리포지토리에 저장하지 마세요](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets)(영문).
>
>

1. Hello ContosoAdsWeb 프로젝트를 열고 hello *Web.Release.config* hello 응용 프로그램에 대 한 변환 파일 *Web.config* 파일을 포함 하는 hello 주석 블록을 삭제 한 `<connectionStrings>` 요소 및 붙여넣기 코드 대신에서 다음 번호입니다.

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="{connectionstring}"
        providerName="System.Data.SqlClient" xdt:Transform="SetAttributes" xdt:Locator="Match(name)"/>
    </connectionStrings>
    ```

    Hello 파일을 편집 하기 위해 열어 둡니다.
2. Hello에 [Azure 포털](https://portal.azure.com), 클릭 **SQL 데이터베이스** hello 왼쪽된 창에서이 자습서에서 만든 hello 데이터베이스를 클릭 한 다음 클릭 **연결 문자열 표시**합니다.

    ![연결 문자열 표시](./media/cloud-services-dotnet-get-started/showcs.png)

    hello 포털 hello 암호에 대 한 자리 표시자로의 연결 문자열을 표시합니다.

    ![연결 문자열](./media/cloud-services-dotnet-get-started/connstrings.png)
3. Hello에 *Web.Release.config* 변환 파일, 삭제 `{connectionstring}` 해당 위치 hello hello Azure 포털에서에서 ADO.NET 연결 문자열에에서 붙여 넣습니다.
4. Hello에 붙여 넣은 hello 연결 문자열에 *Web.Release.config* 변환 파일, 대체 `{your_password_here}` hello 새 SQL 데이터베이스에 대해 만든 hello 암호를 사용 합니다.
5. Hello 파일을 저장 합니다.  
6. 선택 하 고 hello 작업자 역할 프로젝트를 구성 하기 위한 단계를 수행 하는 hello에서 사용 하기 위해 (인용 부호를 둘러싼 hello) 없이 hello 연결 문자열을 복사 합니다.
7. **솔루션 탐색기**아래 **역할** hello 클라우드 서비스 프로젝트에서 마우스 오른쪽 단추로 클릭 **ContosoAdsWorker** 클릭 하 고 **속성**.

    ![역할 속성](./media/cloud-services-dotnet-get-started/rolepropertiesworker.png)
8. Hello 클릭 **설정을** 탭 합니다.
9. 변경 **서비스 구성** 너무**클라우드**합니다.
10. 선택 hello **값** hello에 대 한 필드 `ContosoAdsDbConnectionString` 설정과 hello hello 자습서의 이전 섹션에서 복사한 hello 연결 문자열을 붙여 넣습니다.

     ![작업자 역할의 데이터베이스 연결 문자열](./media/cloud-services-dotnet-get-started/workerdbcs.png)
11. 변경 내용을 저장합니다.  

### <a name="configure-hello-solution-toouse-your-azure-storage-account-when-it-runs-in-azure"></a>Azure에서 실행 될 때 솔루션 toouse hello Azure 저장소 계정 구성
Hello 웹 역할 프로젝트와 hello 작업자 역할 프로젝트에 대 한 azure 저장소 계정 연결 문자열 hello 클라우드 서비스 프로젝트에서 환경 설정에 저장 됩니다. 각 프로젝트에 대해 별도 집합이 설정 toobe hello 응용 프로그램을 로컬로 실행 될 때 사용 하 고 hello 클라우드에서 실행 되 면 합니다. 웹 및 작업자 역할 프로젝트에 대 한 hello 클라우드 환경 설정을 업데이트 합니다.

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 **ContosoAdsWeb** 아래 **역할** hello에 **ContosoAdsCloudService** 프로젝트를 마우스 클릭 **속성**합니다.

    ![역할 속성](./media/cloud-services-dotnet-get-started/roleproperties.png)
2. Hello 클릭 **설정을** 탭 합니다. Hello에 **서비스 구성** 드롭다운 목록 상자에서 선택 **클라우드**합니다.

    ![클라우드 구성](./media/cloud-services-dotnet-get-started/sccloud.png)
3. 선택 hello **StorageConnectionString** 항목을 확인할 수는 줄임표 (**...** ) hello 선의 hello 오른쪽 끝 단추를 클릭 합니다. Hello 줄임표 단추 tooopen hello 클릭 **저장소 계정 연결 문자열 만들기** 대화 상자.

    ![열린 연결 문자열 만들기 상자](./media/cloud-services-dotnet-get-started/opencscreate.png)
4. Hello에 **저장소 연결 문자열 만들기** 대화 상자를 클릭 **구독**, 이전에 만든 hello 저장소 계정을 선택 하 고 클릭 **확인**합니다. 아직 로그인하지 않은 경우 Azure 계정 자격 증명을 요구하는 메시지가 나타납니다.

    ![저장소 연결 문자열 만들기](./media/cloud-services-dotnet-get-started/createstoragecs.png)
5. 변경 내용을 저장합니다.
6. 다음과 같은 hello hello에 사용한 프로시저 `StorageConnectionString` 연결 문자열 tooset hello `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` 연결 문자열입니다.

    이 연결 문자열은 로깅에 사용됩니다.
7. 다음과 같은 hello hello에 사용한 프로시저 **ContosoAdsWeb** 역할 tooset hello에 대 한 연결 문자열 모두 **ContosoAdsWorker** 역할입니다. Tooset 반드시 **서비스 구성** 너무**클라우드**합니다.

Visual Studio UI hello를 사용 하 여 구성 해야 하는 hello 역할 환경 설정 hello hello ContosoAdsCloudService 프로젝트의 파일을 다음에 저장 됩니다.

* *ServiceDefinition.csdef* -hello 설정 이름을 정의 합니다.
* *ServiceConfiguration.Cloud.cscfg* -hello 클라우드에서 hello 응용 프로그램을 실행 하는 경우에 대 한 값을 제공 합니다.
* *ServiceConfiguration.Local.cscfg* -hello 앱 로컬로 실행 하는 경우에 대 한 값을 제공 합니다.

예를 들어 hello ServiceDefinition.csdef hello 정의 뒤에 포함 됩니다.

```xml
<ConfigurationSettings>
    <Setting name="StorageConnectionString" />
    <Setting name="ContosoAdsDbConnectionString" />
</ConfigurationSettings>
```

Hello 및 *ServiceConfiguration.Cloud.cscfg* Visual Studio에서 이러한 설정을 입력 한 hello 값을 포함 하는 파일입니다.

```xml
<Role name="ContosoAdsWorker">
    <Instances count="1" />
    <ConfigurationSettings>
        <Setting name="StorageConnectionString" value="{yourconnectionstring}" />
        <Setting name="ContosoAdsDbConnectionString" value="{yourconnectionstring}" />
        <!-- other settings not shown -->

    </ConfigurationSettings>
    <!-- other settings not shown -->

</Role>
```

hello `<Instances>` 설정은 Azure에서 실행 되는 hello 작업자 역할 코드는 가상 컴퓨터의 hello 수를 지정 합니다. hello [다음 단계](#next-steps) 섹션에는 클라우드 서비스를 확장 하는 방법에 대 한 링크 toomore 정보가 포함 됩니다.

### <a name="deploy-hello-project-tooazure"></a>Hello 프로젝트 tooAzure 배포
1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 hello **ContosoAdsCloudService** 클라우드 프로젝트를 클릭 한 **게시**합니다.

   ![게시 메뉴](./media/cloud-services-dotnet-get-started/pubmenu.png)
2. Hello에 **로그인** hello 단계의 **Azure 응용 프로그램 게시** 마법사를 클릭 하 여 **다음**합니다.

    ![로그인 단계](./media/cloud-services-dotnet-get-started/pubsignin.png)
3. Hello에 **설정** 단계 hello 마법사의 클릭 **다음**합니다.

    ![설정 단계](./media/cloud-services-dotnet-get-started/pubsettings.png)

    hello에서 기본 설정을 hello **고급** 탭이이 자습서에 대 한 세밀 하 게 됩니다. 고급 탭 hello에 대 한 정보를 참조 하십시오. [Azure 응용 프로그램 게시 마법사](http://msdn.microsoft.com/library/hh535756.aspx)합니다.
4. Hello에 **요약** 단계, 클릭 **게시**합니다.

    ![요약 단계](./media/cloud-services-dotnet-get-started/pubsummary.png)

   hello **Azure 활동 로그** 창이 Visual Studio에서 열립니다.
5. Hello 오른쪽 화살표 아이콘 tooexpand hello 배포 세부 정보를 클릭 합니다.

    hello 배포 자세한 toocomplete 또는 too5 분 정도 걸릴 수 있습니다.

    ![Azure 활동 로그 창](./media/cloud-services-dotnet-get-started/waal.png)
6. Hello 배포 상태가 완료 되 면 클릭 hello **웹 앱 URL** toostart hello 응용 프로그램입니다.
7. 이제 hello 응용 프로그램을 로컬로 실행할 때와 마찬가지로 만들기, 보기 및 일부 광고를 편집 하 여 hello 앱을 테스트할 수 있습니다.

> [!NOTE]
> 때 테스트 탭, 삭제 또는 hello 클라우드 서비스 완료 합니다. Hello 클라우드 서비스를 사용 하지 않는 경우에 가상 컴퓨터 리소스에 대 한 예약 되어 있으므로 요금이 발생 하는 것입니다. 또한 실행 중인 채로 두는 경우에는 누군가가 URL을 발견하면 광고를 만들고 볼 수 있습니다. Hello에 [Azure 포털](https://portal.azure.com), toohello 이동 **개요** 탭 클라우드 서비스를 클릭 한 다음 hello **삭제** hello hello 페이지 위쪽에 단추입니다. Tootemporarily 방지 다른 원한다 면 hello 사이트에 액세스할 수 없게, 클릭 **중지** 대신 합니다. 이 경우 요금이 tooaccrue를 계속 합니다. 유사한 프로시저 toodelete hello SQL 데이터베이스 및 저장소 계정을 더 이상 필요할 때 따를 수 없습니다.
>
>

## <a name="create-hello-application-from-scratch"></a>처음부터 hello 응용 프로그램 만들기
아직 다운로드 하지 않은 경우 [완료 hello 응용 프로그램](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4)를 지금 업데이트 합니다. Hello 새 프로젝트로 hello 다운로드 한 프로젝트에서 파일을 복사 합니다.

Hello Contoso 광고 응용 프로그램을 만드는 단계를 수행 하는 hello 포함 됩니다.

* 클라우드 서비스 Visual Studio 솔루션을 만듭니다.
* NuGet 패키지를 업데이트 및 추가합니다.
* 프로젝트 참조를 설정합니다.
* 연결 문자열을 구성합니다.
* 코드 파일을 추가합니다.

Hello 솔루션을 만든 후에 고유 toocloud 서비스 프로젝트 및 Azure blob 및 큐를 hello 코드를 검토 합니다.

### <a name="create-a-cloud-service-visual-studio-solution"></a>클라우드 서비스 Visual Studio 솔루션 만들기
1. Visual Studio에서 선택 **새 프로젝트** hello에서 **파일** 메뉴.
2. Hello hello의 왼쪽된 창에서 **새 프로젝트** 대화 상자에서 **Visual C#** 선택 **클라우드** 템플릿 hello 선택 **Azure클라우드서비스** 서식 파일입니다.
3. Hello 프로젝트 및 솔루션 ContosoAdsCloudService, 이름을 지정 하 고 클릭 **확인**합니다.

    ![새 프로젝트](./media/cloud-services-dotnet-get-started/newproject.png)
4. Hello에 **새 Azure 클라우드 서비스** 대화 상자에서 웹 역할과 작업자 역할을 추가 합니다. Hello 웹 역할 ContosoAdsWeb, 이름을 지정 하 고 hello 작업자 역할 ContosoAdsWorker 이름을 지정 합니다. (Hello 역할 hello 오른쪽 창 toochange hello 기본 이름에 hello 연필 아이콘을 사용 합니다.)

    ![새 클라우드 서비스 프로젝트](./media/cloud-services-dotnet-get-started/newcsproj.png)
5. Hello 표시 되 면 **새 ASP.NET 프로젝트** hello 웹 역할에 대 한 대화 상자 hello MVC 템플릿을 선택한 다음를 클릭 한 다음 **인증 변경**합니다.

    ![인증 변경](./media/cloud-services-dotnet-get-started/chgauth.png)
6. Hello에 **인증 변경** 대화 상자에서 선택 **인증 안 함**, 클릭 하 고 **확인**합니다.

    ![인증 없음](./media/cloud-services-dotnet-get-started/noauth.png)
7. Hello에 **새 ASP.NET 프로젝트** 대화 상자를 클릭 하 여 **확인**합니다.
8. **솔루션 탐색기**(중 하나가 아닙니다 hello 프로젝트), hello 솔루션을 마우스 오른쪽 단추로 클릭 하 고 선택 **추가-새 프로젝트**합니다.
9. Hello에 **새 프로젝트 추가** 대화 상자에서 선택 **Windows** 아래 **Visual C#** 왼쪽된 창의 hello와 hello 클릭 **클래스 라이브러리** 서식 파일입니다.  
10. 이름 hello 프로젝트 *ContosoAdsCommon*, 클릭 하 고 **확인**합니다.

    Tooreference hello Entity Framework 컨텍스트 및 hello 데이터 모델은 웹 및 작업자 역할 프로젝트에서 필요합니다. 대신 hello 웹 역할 프로젝트에 hello EF 관련 클래스를 정의 하 고 hello 작업자 역할 프로젝트에서 해당 프로젝트를 참조할 수 없습니다. 하지만 다른 방법인 hello 작업자 역할 프로젝트 참조 tooweb 어셈블리 필요 하지 않습니다는.

### <a name="update-and-add-nuget-packages"></a>NuGet 패키지 업데이트 및 추가
1. 열기 hello **NuGet 패키지 관리** hello 솔루션에 대 한 대화 상자.
2. Hello 창의 hello 위쪽 선택 **업데이트**합니다.
3. Hello에 대 한 확인 *WindowsAzure.Storage* 패키지 및 hello 목록에 있으면 선택한 선택 hello 웹 및 작업자 프로젝트 tooupdate에서 **업데이트**합니다.

    hello 저장소 클라이언트 라이브러리는 Visual Studio 프로젝트 템플릿 보다 더 자주 업데이트 됩니다 업데이트 새로 만든 프로젝트 요구 toobe에서 종종 해당 hello 버전을 확인할 수 있습니다.
4. Hello 창의 hello 위쪽 선택 **찾아보기**합니다.
5. Hello *EntityFramework* NuGet 패키지를 선택한 세 프로젝트 모두에 설치 합니다.
6. Hello *Microsoft.WindowsAzure.ConfigurationManager* NuGet 패키지 및 hello 작업자 역할 프로젝트에 설치 합니다.

### <a name="set-project-references"></a>프로젝트 참조 설정
1. Hello ContosoAdsWeb 프로젝트 참조 toohello ContosoAdsCommon 프로젝트를 설정 합니다. Hello ContosoAdsWeb 프로젝트를 마우스 오른쪽 단추로 누른 **참조** - **참조 추가**합니다. Hello에 **참조 관리자** 대화 상자에서 **등 프로젝트 솔루션** hello 왼쪽된 창에서 선택 **ContosoAdsCommon**, 클릭 하 고 **확인**.
2. Hello ContosoAdsWorker 프로젝트 참조 toohello ContosAdsCommon 프로젝트를 설정 합니다.

    ContosoAdsCommon은 hello Entity Framework 데이터 모델 및 컨텍스트 클래스를 사용해 프런트 엔드 및 백 엔드 모두 hello 포함 됩니다.
3. Hello ContosoAdsWorker 프로젝트에 대 한 참조를 너무 설정`System.Drawing`합니다.

    이 어셈블리는 hello 백 엔드 tooconvert 이미지 toothumbnails에서 사용 됩니다.

### <a name="configure-connection-strings"></a>연결 문자열 구성
이 섹션에서는 로컬 테스트를 위해 Azure Storage 및 SQL 연결 문자열을 구성합니다. hello 자습서의 앞부분에 나오는 hello 배포 지침 hello 응용 프로그램에서에서 실행 되 면 hello 클라우드 tooset hello 연결에 대 한 문자열 방법을 설명 합니다.

1. Hello ContosoAdsWeb 프로젝트, 열기 hello 응용 프로그램 Web.config 파일 및 insert hello 다음에 `connectionStrings` hello 다음 요소의 `configSections` 요소입니다.

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    Visual Studio 2015 이상을 사용하는 경우 "v11.0"을 "MSSQLLocalDB"로 바꿉니다.
2. 변경 내용을 저장합니다.
3. Hello ContosoAdsCloudService 프로젝트 ContosoAdsWeb 아래에서 마우스 오른쪽 단추로 클릭 **역할**, 클릭 하 고 **속성**합니다.

    ![역할 속성](./media/cloud-services-dotnet-get-started/roleproperties.png)
4. Hello에 **ContosAdsWeb [역할]** 속성 창의 hello 클릭 **설정** 탭을 클릭 한 다음 **설정 추가**합니다.

    둡니다 **서비스 구성** 도**모든 구성**합니다.
5. 이름이 *StorageConnectionString*인 설정을 추가합니다. 설정 **형식** 너무*ConnectionString*, 설정 및 **값** 너무*UseDevelopmentStorage = true*합니다.

    ![새 연결 문자열](./media/cloud-services-dotnet-get-started/scall.png)
6. 변경 내용을 저장합니다.
7. 에 따라 동일한 프로시저 tooadd hello ContosoAdsWorker 역할 속성에는 저장소 연결 문자열을 hello 합니다.
8. Hello에 여전히 **ContosoAdsWorker [역할]** 속성 창 다른 연결 문자열을 추가 합니다.

   * 이름: ContosoAdsDbConnectionString
   * 형식: String
   * 값: 붙여넣기 hello 동일 hello 웹 역할 프로젝트에 대해 사용 된 연결 문자열입니다. (다음 예제는 hello Visual Studio 2013 용입니다. 잊지 마십시오 toochange hello 데이터 원본을이 예제를 복사 하 고 Visual Studio 2015 이상이 사용 하는 경우.)

       ```
       Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;
       ```

### <a name="add-code-files"></a>코드 파일 추가
이 섹션에서는 hello 새 솔루션에 다운로드 한 hello 솔루션에서 코드 파일을 복사합니다. hello 다음 섹션에서는 표시 되며이 코드의 주요 부분에 설명 합니다.

tooadd 파일 tooa 프로젝트 또는 폴더, 마우스 오른쪽 단추로 클릭 hello 프로젝트 또는 폴더와 클릭 **추가** - **기존 항목**합니다. Hello 파일을 클릭 한 다음 선택 **추가**합니다. 기존 파일 tooreplace 사용할지 요청 되 면 클릭 **예**합니다.

1. Hello ContosoAdsCommon 프로젝트에서 삭제 hello *Class1.cs* 파일을 해당 위치 hello에 추가할 *Ad.cs* 및 *ContosoAdscontext.cs* hello에서 파일 프로젝트를 다운로드 합니다.
2. Hello ContosoAdsWeb 프로젝트 hello 파일 다운로드 hello 프로젝트에서 다음을 추가 합니다.

   * *Global.asax.cs*  
   * Hello에 *Views\Shared* 폴더:  *\_Layout.cshtml*합니다.
   * Hello에 *Views\Home* 폴더: *Index.cshtml*합니다.
   * Hello에 *컨트롤러* 폴더: *AdController.cs*합니다.
   * Hello에 *Views\Ad* 폴더 (먼저 hello 폴더 만들기): 5 *.cshtml* 파일입니다.
3. Hello ContosoAdsWorker 프로젝트에서 추가 *WorkerRole.cs* hello에서 프로젝트를 다운로드 합니다.

이제 작성 하 고 hello 자습서의 앞부분에서 설명 된 대로 hello 응용 프로그램을 실행할 수 있습니다 및 로컬 데이터베이스 및 저장소 에뮬레이터 리소스가 hello 앱 사용 합니다.

hello 다음 섹션에서는 코드를 설명 hello Azure 환경, blob 및 큐와 관련된 tooworking hello 합니다. 이 자습서에서는 설명 하지 않습니다 어떻게 toocreate MVC 컨트롤러 및 뷰를 스 캐 폴딩을 사용 하 여, toowrite Entity Framework 코드를 어떤 방식으로 SQL Server 데이터베이스 또는 ASP.NET 4.5에 비동기 프로그래밍의 hello 기본 합니다. 이러한 항목에 대 한 내용은 다음 리소스는 hello 참조:

* [MVC 5 시작](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [EF 6 및 MVC 5 시작](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc)
* [.NET 4.5에서 tooasynchronous 프로그래밍 소개](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async)합니다.

### <a name="contosoadscommon---adcs"></a>ContosoAdsCommon - Ad.cs
hello Ad.cs 파일 ad 범주에 대 한 enum과 ad 정보에 대 한 POCO 엔터티 클래스를 정의합니다.

```csharp
public enum Category
{
    Cars,
    [Display(Name="Real Estate")]
    RealEstate,
    [Display(Name = "Free Stuff")]
    FreeStuff
}

public class Ad
{
    public int AdId { get; set; }

    [StringLength(100)]
    public string Title { get; set; }

    public int Price { get; set; }

    [StringLength(1000)]
    [DataType(DataType.MultilineText)]
    public string Description { get; set; }

    [StringLength(1000)]
    [DisplayName("Full-size Image")]
    public string ImageURL { get; set; }

    [StringLength(1000)]
    [DisplayName("Thumbnail")]
    public string ThumbnailURL { get; set; }

    [DataType(DataType.Date)]
    [DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
    public DateTime PostedDate { get; set; }

    public Category? Category { get; set; }
    [StringLength(12)]
    public string Phone { get; set; }
}
```

### <a name="contosoadscommon---contosoadscontextcs"></a>ContosoAdsCommon - ContosoAdsContext.cs
hello ContosoAdsContext 클래스 hello Ad 클래스 Entity Framework는 SQL 데이터베이스에 저장 하는 DbSet 컬렉션에 사용 되도록 지정 합니다.

```csharp
public class ContosoAdsContext : DbContext
{
    public ContosoAdsContext() : base("name=ContosoAdsContext")
    {
    }
    public ContosoAdsContext(string connString)
        : base(connString)
    {
    }
    public System.Data.Entity.DbSet<Ad> Ads { get; set; }
}
```

hello 클래스에 두 명의 생성자입니다. 먼저 hello 그중에서 hello 웹 프로젝트에서 사용 하 고 hello Web.config 파일에 저장 된 연결 문자열의 hello 이름을 지정 합니다. hello 두 번째 생성자 Web.config 파일 없으므로 hello 작업자 역할 프로젝트에서 사용 하는 hello 실제 연결 문자열에 toopass가 있습니다. 했 듯이 여기서이 연결 문자열 저장 된 하 고 hello DbContext 클래스를 인스턴스화할 때 hello 코드 hello 연결 문자열을 검색 하는 어떻게 표시 됩니다.

### <a name="contosoadsweb---globalasaxcs"></a>ContosoAdsWeb - Global.asax.cs
Hello에서 호출 되는 코드 `Application_Start` 메서드 만듭니다는 *이미지* blob 컨테이너 및 *이미지* 아직 없는 경우 큐에 대기 합니다. 이렇게 하는 새 저장소 계정을 사용 하 여 시작 하거나 hello 저장소 에뮬레이터를 사용 하 여 새 컴퓨터에서 시작 때마다 hello 필요한 blob 컨테이너 및 큐가 자동으로 만들어집니다.

코드 가져옵니다 액세스 toohello 저장소 계정에서 hello hello 저장소 연결 문자열을 사용 하 여 hello *.cscfg* 파일입니다.

```csharp
var storageAccount = CloudStorageAccount.Parse
    (RoleEnvironment.GetConfigurationSettingValue("StorageConnectionString"));
```

그런 다음 참조 toohello 가져오고 *이미지* blob 컨테이너, 존재 하지 않는 액세스 hello 새 컨테이너에 대 한 권한을 설정 하는 경우 hello 컨테이너를 만듭니다. 기본적으로 새 컨테이너 스토리지 계정으로 클라이언트를 자격 증명 tooaccess blob만 허용합니다. hello 웹 사이트 지점 toohello 이미지 blob에 해당 Url을 사용 하 여 이미지를 표시할 수 있도록 blob toobe 공개를 hello 필요 합니다.

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
var imagesBlobContainer = blobClient.GetContainerReference("images");
if (imagesBlobContainer.CreateIfNotExists())
{
    imagesBlobContainer.SetPermissions(
        new BlobContainerPermissions
        {
            PublicAccess =BlobContainerPublicAccessType.Blob
        });
}
```

비슷한 코드 참조 toohello 가져옵니다 *이미지* 대기 및 새 큐를 만듭니다. 이런 경우 권한을 변경할 필요가 없습니다.

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
var imagesQueue = queueClient.GetQueueReference("images");
imagesQueue.CreateIfNotExists();
```

### <a name="contosoadsweb---layoutcshtml"></a>ContosoAdsWeb - \_Layout.cshtml
hello *_Layout.cshtml* 파일 hello 머리글 및 바닥글에 hello 응용 프로그램 이름을 설정 하 고 "광고" 메뉴 항목을 만듭니다.

### <a name="contosoadsweb---viewshomeindexcshtml"></a>ContosoAdsWeb - Views\Home\Index.cshtml
hello *Views\Home\Index.cshtml* 파일 hello 홈 페이지에서 범주 링크를 표시 합니다. hello의 hello 정수 값을 전달 하는 hello 링크 `Category` 쿼리 문자열 변수 toohello 광고 인덱스 페이지에는 열거형입니다.

```razor
<li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
<li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
<li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
<li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>
```

### <a name="contosoadsweb---adcontrollercs"></a>ContosoAdsWeb - AdController.cs
Hello에 *AdController.cs* 파일, hello 생성자 호출 hello `InitializeStorage` blob 및 큐를 사용 하기 위한 API를 제공 하는 메서드 toocreate Azure 저장소 클라이언트 라이브러리 개체입니다.

Hello 코드 참조 toohello 가져옵니다 다음 *이미지* 에서 이전에 본 것 처럼 컨테이너 blob *Global.asax.cs*합니다. 그 과정에서 웹앱에 해당하는 기본 [재시도 정책](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) (영문)을 설정합니다. hello 기본 지 수 백오프 재시도 정책을 일시적인 오류에 대 한 여러 번 시도에 1 분 보다 오랫동안 hello 웹 응용 프로그램 작동을 중지할 수 있습니다. 여기에 지정 된 hello 재시도 정책을 toothree 시도를 각 시도 후 3 초 동안 대기 합니다.

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesBlobContainer = blobClient.GetContainerReference("images");
```

비슷한 코드 참조 toohello 가져옵니다 *이미지* 큐입니다.

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesQueue = queueClient.GetQueueReference("images");
```

대부분의 hello 컨트롤러 코드는 DbContext 클래스를 사용 하 여 Entity Framework 데이터 모델을 사용 하기 위한 일반적인 합니다. 예외는 hello HttpPost `Create` 메서드 파일을 업로드 하 고 blob 저장소에 저장 합니다. hello 모델 바인더를 제공는 [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) toohello 메서드 개체입니다.

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<ActionResult> Create(
    [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
    HttpPostedFileBase imageFile)
```

Hello 사용자 파일 tooupload를 선택 하는 경우 hello 코드는 hello 파일을 업로드 하는 blob에 저장 및 toohello blob을 가리키는 URL로 hello Ad 데이터베이스 레코드를 업데이트 합니다.

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    blob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = blob.Uri.ToString();
}
```

hello 코드 업로드 hello지 않습니다 하는 hello `UploadAndSaveBlobAsync` 메서드. Hello blob, 업로드 및 저장 hello 파일에 대 한 GUID 이름을 만들고 참조 toohello 저장 된 blob를 반환 합니다.

```csharp
private async Task<CloudBlockBlob> UploadAndSaveBlobAsync(HttpPostedFileBase imageFile)
{
    string blobName = Guid.NewGuid().ToString() + Path.GetExtension(imageFile.FileName);
    CloudBlockBlob imageBlob = imagesBlobContainer.GetBlockBlobReference(blobName);
    using (var fileStream = imageFile.InputStream)
    {
        await imageBlob.UploadFromStreamAsync(fileStream);
    }
    return imageBlob;
}
```

Hello HttpPost 후 `Create` blob을 업로드 하는 메서드 및 업데이트 hello 데이터베이스, 해당 백 엔드 프로세스 이미지는 변환 tooa 축소판 그림에 대 한 준비 큐 메시지 tooinform 만듭니다.

```csharp
string queueMessageString = ad.AdId.ToString();
var queueMessage = new CloudQueueMessage(queueMessageString);
await queue.AddMessageAsync(queueMessage);
```

HttpPost hello에 대 한 코드 hello `Edit` 메서드는 점을 제외 하 고 hello 사용자가 새 이미지 파일을 선택 하는 경우 이미 존재 하는 모든 blob을 삭제 해야 합니다.

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    await DeleteAdBlobsAsync(ad);
    imageBlob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = imageBlob.Uri.ToString();
}
```

다음 예제에서는 hello 광고를 삭제 하면 blob을 삭제 하는 hello 코드를 보여 줍니다.

```csharp
private async Task DeleteAdBlobsAsync(Ad ad)
{
    if (!string.IsNullOrWhiteSpace(ad.ImageURL))
    {
        Uri blobUri = new Uri(ad.ImageURL);
        await DeleteAdBlobAsync(blobUri);
    }
    if (!string.IsNullOrWhiteSpace(ad.ThumbnailURL))
    {
        Uri blobUri = new Uri(ad.ThumbnailURL);
        await DeleteAdBlobAsync(blobUri);
    }
}
private static async Task DeleteAdBlobAsync(Uri blobUri)
{
    string blobName = blobUri.Segments[blobUri.Segments.Length - 1];
    CloudBlockBlob blobToDelete = imagesBlobContainer.GetBlockBlobReference(blobName);
    await blobToDelete.DeleteAsync();
}
```

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a>ContosoAdsWeb - Views\Ad\Index.cshtml 및 Details.cshtml
hello *Index.cshtml* 파일 축소판 그림 hello로 다른 ad 데이터를 표시 합니다.

```razor
<img src="@Html.Raw(item.ThumbnailURL)" />
```

hello *Details.cshtml* 파일 hello에 전체 이미지를 표시 합니다.

```razor
<img src="@Html.Raw(Model.ImageURL)" />
```

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a>ContosoAdsWeb - Views\Ad\Create.cshtml 및 Edit.cshtml
hello *Create.cshtml* 및 *Edit.cshtml* 파일 인코딩을 hello 컨트롤러 tooget hello를 사용 하도록 설정 하는 폼은 지정 `HttpPostedFileBase` 개체입니다.

```razor
@using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))
```

`<input>` 요소 파일 선택 대화 상자 hello 브라우저 tooprovide 알려 줍니다.

```razor
<input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />
```

### <a name="contosoadsworker---workerrolecs---onstart-method"></a>ContosoAdsWorker - WorkerRole.cs - OnStart 메서드
hello Azure 작업자 역할 환경 호출 hello `OnStart` hello에 대 한 메서드 `WorkerRole` hello 작업자 역할을 시작 하기 hello를 호출 하는 경우 클래스 `Run` 메서드 때 hello `OnStart` 메서드가 완료 된 합니다.

hello `OnStart` 메서드 hello에서 hello 데이터베이스 연결 문자열을 가져옵니다 *.cscfg* 파일을 toohello 엔터티 프레임 워크 DbContext 클래스를 전달 합니다. hello 공급자가 지정 된 toobe 않아도 되므로 hello SQLClient 공급자는 기본적으로 사용 됩니다.

```csharp
var dbConnString = CloudConfigurationManager.GetSetting("ContosoAdsDbConnectionString");
db = new ContosoAdsContext(dbConnString);
```

그 후 hello 메서드 참조 toohello 저장소 계정을 가져옵니다 하 고 없는 경우 hello blob 컨테이너 및 큐를 만듭니다. 에 대 한 hello 코드는 hello 웹 역할에서 이미 살펴본 비슷한 toowhat `Application_Start` 메서드.

### <a name="contosoadsworker---workerrolecs---run-method"></a>ContosoAdsWorker - WorkerRole.cs - Run 메서드
hello `Run` 메서드는 hello `OnStart` 메서드가 초기화 작업을 완료 합니다. hello 메서드는 새 큐 메시지를 감시 하 고 도착 했을 때 처리 하는 무한 루프를 실행 합니다.

```csharp
public override void Run()
{
    CloudQueueMessage msg = null;

    while (true)
    {
        try
        {
            msg = this.imagesQueue.GetMessage();
            if (msg != null)
            {
                ProcessQueueMessage(msg);
            }
            else
            {
                System.Threading.Thread.Sleep(1000);
            }
        }
        catch (StorageException e)
        {
            if (msg != null && msg.DequeueCount > 5)
            {
                this.imagesQueue.DeleteMessage(msg);
            }
            System.Threading.Thread.Sleep(5000);
        }
    }
}
```

Hello 루프를 반복할 때마다 큐 메시지가 없는 경우 hello 프로그램 초 동안 대기 합니다. 이렇게 하면 hello 작업자 역할을에서 과도 한 CPU 시간과 저장소 트랜잭션 비용을 발생 시 키 지 않습니다. Microsoft 고객 자문 팀 hello tooproduction를 배포 하 고 휴가 용으로 남겨 둔는 개발자에 게이 tooinclude 찾기에 대 한 이야기를 알려 줍니다. 그 얻었습니다 때 자신의 감독에 비해 hello 휴가 합니다.

경우에 따라 큐 메시지의 hello 콘텐츠 처리에서 오류가 발생합니다. 이 라고는 *포이즌 메시지*, 방금 오류를 기록 하 고 hello 루프를 다시 시작을 시도할 수 있습니다 머무르면서 tooprocess 해당 메시지와 합니다.  따라서 hello catch 블록이 포함 if 문을 toosee를 확인 하는 hello 앱 tooprocess 시도한 횟수 hello 현재 메시지 및 경과 했는데도 문제가 있다면 5 번 이상, hello 메시지 hello 큐에서 삭제 됩니다.

큐 메시지가 발견되는 경우 `ProcessQueueMessage`이(가) 호출됩니다.

```csharp
private void ProcessQueueMessage(CloudQueueMessage msg)
{
    var adId = int.Parse(msg.AsString);
    Ad ad = db.Ads.Find(adId);
    if (ad == null)
    {
        throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", adId.ToString()));
    }

    CloudBlockBlob inputBlob = this.imagesBlobContainer.GetBlockBlobReference(ad.ImageURL);

    string thumbnailName = Path.GetFileNameWithoutExtension(inputBlob.Name) + "thumb.jpg";
    CloudBlockBlob outputBlob = this.imagesBlobContainer.GetBlockBlobReference(thumbnailName);

    using (Stream input = inputBlob.OpenRead())
    using (Stream output = outputBlob.OpenWrite())
    {
        ConvertImageToThumbnailJPG(input, output);
        outputBlob.Properties.ContentType = "image/jpeg";
    }

    ad.ThumbnailURL = outputBlob.Uri.ToString();
    db.SaveChanges();

    this.imagesQueue.DeleteMessage(msg);
}
```

이 코드 hello 데이터베이스 tooget hello 이미지 URL을 읽고, hello 이미지 tooa 축소판 그림으로 변환, blob의 hello 축소판 그림을 저장, hello 축소판 blob URL으로 hello 데이터베이스를 업데이트 및 hello 큐 메시지를 삭제 합니다.

> [!NOTE]
> hello에 대 한 코드 hello `ConvertImageToThumbnailJPG` 메서드는 편의상 hello System.Drawing 네임 스페이스의 클래스를 사용 합니다. 그러나이 네임 스페이스의 hello 클래스는 Windows Forms 사용 하도록 설계 되었습니다. Windows 또는 ASP.NET 서비스에서 사용할 수 있도록 지원되지 않습니다. 이미지 처리 옵션에 대한 자세한 내용은 [동적 이미지 생성](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) 및 [이미지 크기 조정 세부 정보](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na)를 참조하세요.
>
>

## <a name="troubleshooting"></a>문제 해결
다음은 몇 가지 일반적인 오류가이 자습서에서는 hello 지침을 따라 하는 동안, 작동 하지 않는 경우와 방법을 tooresolve 해당 합니다.

### <a name="serviceruntimeroleenvironmentexception"></a>ServiceRuntime.RoleEnvironmentException
hello `RoleEnvironment` 개체 hello Azure 계산 에뮬레이터를 사용 하 여 로컬로 실행 하는 경우 또는 Azure에서 응용 프로그램을 실행 하면 Azure에서 제공 합니다.  을 로컬로 실행 하는 경우이 오류를 발생 hello 시작 프로젝트로 hello ContosoAdsCloudService 프로젝트를 설정 했는지 확인 합니다. 이 hello 프로젝트 toorun hello Azure 계산 에뮬레이터를 사용 하 여 설정 합니다.

Hello에 저장 되어 있는 tooget hello 연결 문자열 값은 hello 응용 프로그램에서는 hello에 대 한 Azure RoleEnvironment hello 중 하나가 *.cscfg* 파일,이 예외는 누락 된 연결 문자열입니다. Hello ContosoAdsWeb 프로젝트에서 클라우드 모두에 대 한 hello StorageConnectionString 설정 및 구성을 로컬를 생성 하 여 두 구성 모두에 대 한 연결 문자열 모두 hello ContosoAdsWorker 프로젝트에서 만든 되었는지 확인 합니다. 이렇게 하면 한 **모두 찾기** 검색 hello 전체 솔루션에서 StorageConnectionString에 대 한 표시 되어야 것 9 번 6 파일에 있습니다.

### <a name="cannot-override-tooport-xxx-new-port-below-minimum-allowed-value-8080-for-protocol-http"></a>Tooport xxx를 재정의할 수 없습니다. 프로토콜 http에 대한 최소 허용 값 8080 미만의 새 포트
Hello 웹 프로젝트에서 사용 하는 hello 포트 번호를 변경해 보십시오. Hello ContosoAdsWeb 프로젝트를 마우스 오른쪽 단추로 누른 **속성**합니다. Hello 클릭 **웹** 탭을 선택한 다음 hello에 hello 포트 번호를 변경 **프로젝트 Url** 설정 합니다.

Hello 문제를 해결할 수 있는 또 다른 방법은 hello 다음 섹션을 참조 하십시오.

### <a name="other-errors-when-running-locally"></a>로컬 실행 중 다른 오류
새로운 클라우드 기본적으로 서비스 프로젝트는 hello Azure compute emulator express toosimulate hello Azure 환경을 사용합니다. Hello 전체 계산 에뮬레이터의 경량 버전 이므로 일부 조건 hello에서 전체 에뮬레이터 hello express 버전에는 없는 될 때 작동 합니다.  

toochange 프로젝트 toouse hello 전체 에뮬레이터 hello hello ContosoAdsCloudService 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **속성**합니다. Hello에 **속성** 창을 클릭 hello **웹** 탭을 클릭 한 다음 hello **전체 에뮬레이터 사용** 라디오 단추입니다.

주문 toorun hello 응용 프로그램 hello 전체 에뮬레이터와 함께 관리자 권한으로 Visual Studio tooopen을 해야합니다.

## <a name="next-steps"></a>다음 단계
Contoso 광고 응용 프로그램 hello 의도적으로 유지 하는 간단한-시작 자습서에 대 한 합니다. 예를 들어, 구현 하지 않습니다 [종속성 주입](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) 또는 hello [리포지토리와의 단위 작업 패턴](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), 그렇지 않은 [로깅에 대 한 인터페이스를 사용 하 여](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), 를사용하지않습니다[ EF Code First 마이그레이션을](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage 데이터 모델이 변경 또는 [EF 연결 복원 력](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage 일시적인 네트워크 오류, 및 등입니다.

다음은 더 많은 실제 코딩 관행을 복잡 한 덜 복잡 한 toomore에서 나열 된는 방법을 보여 주는 몇 가지 클라우드 서비스 샘플 응용 프로그램입니다.

* [PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31)(영문). 개념상 비슷하지만 tooContoso 광고 하지만 더 많은 기능 및 구현 더 많은 실제 코딩 방법을 합니다.
* [테이블, 큐 및 Blob이 포함된 Azure 클라우드 서비스 다중 계층 응용 프로그램](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36)(영문). Azure 저장소 테이블 뿐만 아니라 Blob 및 큐를 소개합니다. .NET 용 hello Azure SDK의 이전 버전에 따라, 일부 수정 toowork hello 현재 버전으로 필요 합니다.
* [Microsoft Azure의 클라우드 서비스 기본 사항(영문)](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649). 다양 한 범위의 hello Microsoft Patterns and Practices 그룹에 의해 생성 되는 모범 사례를 보여 주는 포괄적인 샘플입니다.

Hello 클라우드에 대 한 개발에 대 한 일반 정보를 참조 하십시오. [Azure로 실제 클라우드 응용 프로그램 빌딩](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction)합니다.

한 비디오 지침은 tooAzure 저장소에 대 한 모범 사례 및 패턴, 참조 [Microsoft Azure 저장소 – 새로 만들기, 모범 사례 및 패턴 이란](http://channel9.msdn.com/Events/Build/2014/3-628)합니다.

자세한 내용은 다음 리소스는 hello 참조:

* [Azure 클라우드 서비스 1 부:](http://justazure.com/microsoft-azure-cloud-services-part-1-introduction/)
* [Toomanage 클라우드 서비스 하는 방법](cloud-services-how-to-manage.md)
* [Azure 저장소](/documentation/services/storage/)
* [어떻게 toochoose는 클라우드 서비스 공급자](https://azure.microsoft.com/overview/choosing-a-cloud-service-provider/)
