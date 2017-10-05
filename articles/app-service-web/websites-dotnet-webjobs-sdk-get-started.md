---
title: "Azure App Service에서 .NET WebJob 만들기 | Microsoft Docs"
description: "ASP.NET MVC 및 Azure를 사용하여 다중 계층 앱을 만듭니다. 프런트 엔드는 Azure App Service의 웹앱에서 실행되고 백 엔드는 WebJob으로 실행됩니다. 앱에서는 Entity Framework, SQL 데이터베이스 및 Azure 저장소 큐와 Blob을 사용합니다."
services: app-service
documentationcenter: .net
author: tdykstra
manager: erikre
editor: mollybos
ms.assetid: 99cb9917-483a-45f8-a98d-07d19c68c753
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/14/2017
ms.author: glenga
ms.openlocfilehash: a20b13058caecff75af14957468f20e63a3325c9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-net-webjob-in-azure-app-service"></a>Azure 앱 서비스에서 .NET WebJob 만들기
이 자습서에서는 [WebJob SDK](websites-dotnet-webjobs-sdk.md)를 사용하는 간단한 다중 계층 ASP.NET MVC 5 응용 프로그램에 코드를 작성하는 방법을 보여줍니다.

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

[WebJobs SDK](websites-webjobs-resources.md) 목적은 WebJob이 이미지 처리, 큐 처리, RSS 집계, 파일 유지 관리, 전자 메일 보내기 등을 수행하는 일반적인 작업에 대해 작성하는 코드를 간소화하는 것입니다. WebJobs SDK에는 Azure 저장소 및 서비스 버스 작업, 작업 예약 및 오류 처리, 기타 여러 일반적인 시나리오를 위한 기본 제공 기능이 있습니다. 또한 확장이 가능하기 때문에 [확장을 위한 오픈 소스 리포지토리](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview)도 있습니다.

샘플 응용 프로그램은 광고 게시판입니다. 사용자는 광고에 대한 이미지를 업로드하고 백 엔드 과정은 이미지를 축소판 그림에 변환합니다. 광고 목록 페이지는 축소판 그림을 보여주고 광고 세부 정보 페이지는 전체 크기 이미지를 보여줍니다. 다음 스크린샷을 참조하세요.

![광고 목록](./media/websites-dotnet-webjobs-sdk-get-started/list.png)

이 샘플 응용 프로그램은 [Azure 큐](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) 및 [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage)과 함께 작동합니다. 이 자습서에서는 [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) 및 [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279)에 응용 프로그램을 배포하는 방법을 보여줍니다.

## <a id="prerequisites"></a>필수 조건
이 자습서에서는 Visual Studio에서 [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) 프로젝트를 작업하는 방법도 알고 있다고 가정합니다.

이 자습서는 원래 Visual Studio 2013용으로 작성되었지만 이후 버전의 Visual Studio에서 사용할 수 있습니다. Visual Studio 2015 또는 2017을 사용하는 경우 응용 프로그램을 로컬로 실행하기 전에 Web.config 및 App.config에서 SQL Server LocalDB 연결 문자열의 `Data Source` 부분을 `Data Source=(localdb)\v11.0`에서 `Data Source=(LocalDb)\MSSQLLocalDB`로 변경해야 합니다.

> [!NOTE]
> <a name="note"></a>이 자습서를 완료하려면 Azure 계정이 있어야 합니다.
>
> * [Azure 계정을 무료로 개설](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)할 수 있음: 유료 Azure 서비스를 사용해볼 수 있는 크레딧을 받게 되며 크레딧을 모두 사용한 후에도 계정을 유지하고 무료 Azure 서비스(예: 웹 서비스)를 사용할 수 있습니다. 설정을 명시적으로 변경하여 결제를 요청하지 않는 한 신용 카드로 결제되지 않습니다.
> * [Visual Studio 구독자에 대한 월별 Azure 크레딧을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)할 수 있음: Visual Studio 구독은 유료 Azure 서비스에 사용할 수 있는 크레딧을 매달 제공합니다.
>
> Azure 계정을 등록하기 전에 Azure App Service를 시작하려면 [App Service 체험](https://azure.microsoft.com/try/app-service/)으로 이동합니다. 여기서 App Service의 단기 시작 웹앱을 즉시 만들 수 있습니다. 신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.
>
>

## <a id="learn"></a>학습할 내용
이 자습서에서는 다음 작업의 수행 방법을 보여 줍니다.

* Azure SDK를 설치하여 사용자 컴퓨터에서 Azure를 개발할 수 있도록 지원(Visual Studio 2013 및 2015 사용자에만 해당)
* 연결된 웹 프로젝트를 배포할 때 Azure WebJob으로 자동 배포되는 콘솔 응용 프로그램 프로젝트를 만듭니다.
* 개발 컴퓨터에서 로컬로 WebJob SDK 백 엔드를 테스트합니다.
* 앱 서비스에서 웹앱에 있는 WebJob 백엔드로 응용 프로그램을 게시합니다.
* 파일을 업로드하고 Azure Blob 서비스에 저장합니다.
* Azure WebJob SDK를 사용하여 Azure 저장소 큐 및 Blob로 작업합니다.

## <a id="contosoads"></a>응용 프로그램 아키텍처
이 샘플 응용 프로그램에서는 [큐 중심 작업 패턴](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) 을 사용하여 미리 보기를 만드는 CPU 사용량이 많은 작업을 백 엔드 프로세스에 오프로드합니다.

앱은 Entity Framework Code First를 사용해 SQL 데이터베이스에 광고를 저장하여 테이블을 만들고 데이터에 액세스합니다. 광고별로 데이터베이스는 전체 크기 이미지용과 미리 보기용으로 두 개의 URL을 저장합니다.

![광고 테이블](./media/websites-dotnet-webjobs-sdk-get-started/adtable.png)

사용자가 이미지를 업로드하면 웹앱이 [Azure Blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage)에 이미지를 저장하며 Blob을 가리키는 URL을 사용하여 데이터베이스에 광고 정보를 저장합니다. 이와 동시에 Azure 큐에 메시지를 기록합니다. Azure WebJob으로 실행되는 백 엔드 프로세스에서 WebJob SDK는 큐에서 새 메시지를 폴링합니다. 새 메시지가 나타나면 WebJob은 해당 이미지의 미리 보기를 만들고 광고에 대한 미리 보기 URL 데이터베이스 필드를 업데이트합니다. 다음은 응용 프로그램의 여러 부분이 상호 작용하는 방법을 보여 주는 다이어그램입니다.

![Contoso Ads 아키텍처](./media/websites-dotnet-webjobs-sdk-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]  
자습서 지침은 2.7.1.NET 이후에 Azure SDK를 적용합니다.

## <a id="storage"></a>Azure 저장소 계정 만들기
Azure 저장소 계정은 큐 및 Blob 데이터를 클라우드에 저장하기 위한 리소스를 제공합니다. WebJob SDK에서 대시보드에 대한 로깅 데이터를 저장하기 위해서도 사용됩니다.

실제 응용 프로그램에서는 일반적으로 응용 프로그램 데이터와 로깅 데이터를 위한 별도의 계정 및 테스트 데이터와 프로덕션 데이터를 위한 별도의 계정을 만듭니다. 이 자습서에서는 하나의 계정만 사용합니다.

1. Visual Studio에서 **서버 탐색기** 창을 엽니다.
2. **Azure** 노드를 마우스 오른쪽 단추로 클릭하고 **Microsoft Azure 구독에 연결...**을 클릭합니다.
   
   ![Azure에 연결](./media/websites-dotnet-webjobs-sdk-get-started/connaz.png)

3. Azure 자격 증명을 사용하여 로그인합니다.
4. Azure 노드 아래에서 **저장소**를 마우스 오른쪽 단추로 클릭하고 **저장소 계정 만들기**를 클릭합니다.
   
   ![저장소 계정 만들기](./media/websites-dotnet-webjobs-sdk-get-started/createstor.png)
   
5. **저장소 계정 만들기** 대화 상자에서 저장소 계정의 이름을 입력합니다.

    이 이름은 고유해야 합니다(다른 Azure 저장소 계정이 동일한 이름을 사용할 수 없음). 입력한 이름이 이미 사용 중이면 변경할 수 있습니다.

    저장소 계정에 액세스하기 위한 URL은 *{name}*.core.windows.net입니다.
6. **지역 또는 선호도 그룹** 드롭다운 목록을 가장 가까운 지역으로 설정합니다.

    이 설정은 저장소 계정을 호스트할 Azure 데이터 센터를 지정합니다. 이 자습서의 경우 어떤 항목을 선택해도 두드러진 차이를 느낄 수 없습니다. 하지만 프로덕션 웹앱의 경우에는 대기 시간과 데이터 발신 요금을 최소화하기 위해 웹 서버와 저장소 계정을 동일한 지역에 두기 원할 것입니다. 나중에 만들게 될 웹앱은 대기 시간을 최소화하기 위해 웹앱에 액세스하는 브라우저에 가능한 한 가까워야 합니다.
7. **복제** 드롭다운 목록을 **로컬 중복**으로 설정합니다.

    저장소 계정에 대해 지역에서 복제를 사용하는 경우에는 저장된 콘텐츠가 보조 위치에 복제되어 기본 위치에서 주요 재해가 발생하는 경우 보조 데이터 센터로 장애 조치(Failover)할 수 있도록 합니다. 지역에서 복제는 추가 비용을 발생시킬 수 있습니다. 테스트 및 개발 계정의 경우 일반적으로 지역에서 복제 비용을 지불하지 않는 것이 좋습니다. 자세한 내용은 [저장소 계정 만들기, 관리 또는 삭제](../storage/common/storage-create-storage-account.md)를 참조하세요
8. **만들기**를 클릭합니다.

    ![새 저장소 계정](./media/websites-dotnet-webjobs-sdk-get-started/newstorage.png)

## <a id="download"></a>응용 프로그램 다운로드
1. [완료된 솔루션](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb)을 다운로드하고 압축 해제합니다.
2. Visual Studio를 시작합니다.
3. **파일** 메뉴에서 **열기 > 프로젝트/솔루션**을 선택하고 솔루션을 다운로드한 위치로 이동한 후 솔루션 파일을 엽니다.
4. Ctrl+Shift+B를 눌러 솔루션을 빌드합니다.

    기본적으로 Visual Studio는 *.zip* 파일에 포함되지 않은 NuGet 패키지 콘텐츠를 자동으로 복원합니다. 패키지가 복원되지 않는 경우 **솔루션의 NuGet 패키지 관리** 대화 상자로 이동하고 오른쪽 위에서 **복원** 단추를 클릭하여 수동으로 설치합니다.
5. **솔루션 탐색기**에서 시작 프로젝트로 **ContosoAdsWeb**이 선택되었는지 확인합니다.

## <a id="configurestorage"></a>저장소 계정을 사용하도록 응용 프로그램 구성
1. ContosoAdsWeb 프로젝트에서 응용 프로그램 *Web.config* 파일을 엽니다.

    이 파일에는 Blob 및 큐 사용을 위한 SQL 연결 문자열과 Azure 저장소 연결 문자열이 포함되어 있습니다.

    SQL 연결 문자열은 [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) 데이터베이스를 가리킵니다.

    저장소 연결 문자열은 저장소 계정 이름과 액세스 키에 대한 자리 표시자가 있는 예입니다. 이를 저장소 계정의 이름과 키가 포함된 연결 문자열로 바꿉니다.  

    ```
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
        <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
    </connectionStrings>
    ```
    저장소 연결 문자열 이름은 WebJob SDK에서 기본적으로 사용하는 이름인 AzureWebJobsStorage입니다. Azure 환경에서 하나의 연결 문자열 값만 설정하면 되도록, 여기서는 같은 이름이 사용됩니다.
2. **서버 탐색기**에서 **저장소** 노드 아래에 있는 저장소 계정을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.

    ![저장소 계정 속성 클릭](./media/websites-dotnet-webjobs-sdk-get-started/storppty.png)
3. **속성** 창에서 **저장소 계정 키**를 클릭하고 줄임표를 클릭합니다.

    ![저장소 계정 키](./media/websites-dotnet-webjobs-sdk-get-started/stor-account-keys.png)
4. **연결 문자열**을 복사합니다.

    ![저장소 계정 키 대화 상자](./media/websites-dotnet-webjobs-sdk-get-started/cpak.png)
5. *Web.config* 파일에서 저장소 연결 문자열을 방금 복사한 연결 문자열로 바꿉니다. 붙여 넣기 전에 따옴표를 포함하지 않고 따옴표 안의 모든 내용을 선택해야 합니다.
6. ContosoAdsWebJob 프로젝트에서 *App.config* 파일을 엽니다.

    이 파일에는 응용 프로그램 데이터를 위한 저장소 연결 문자열과 로깅을 위한 저장소 연결 문자열이 있습니다. 응용 프로그램 데이터와 로깅에 대한 별도의 저장소 계정을 사용할 수 있으며 [데이터에 대해 여러 저장소 계정](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs)을 사용할 수 있습니다. 이 자습서에서는 단일 저장소 계정을 사용합니다. 연결 문자열에는 저장소 계정 키의 자리 표시자가 있습니다.

    ```
    <configuration>
        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;"/>
    </connectionStrings>
        <startup>
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
    </startup>
    </configuration>

    ```

    기본적으로 WebJob SDK는 AzureWebJobsStorage 및 AzureWebJobsDashboard라는 연결 문자열을 찾습니다. 또는 [원하는 연결 문자열을 저장한 후 `JobHost` 개체에 명시적으로 전달할 수 있습니다](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).
7. 저장소 연결 문자열을 둘 다 앞에서 복사한 연결 문자열로 바꿉니다.
8. 변경 내용을 저장합니다.

## <a id="run"></a>로컬에서 응용 프로그램 실행
1. 응용 프로그램의 웹 프런트 엔드를 시작하려면 Ctrl+F5를 누릅니다.

    기본 브라우저는 홈 페이지로 열립니다. (웹 프로젝트를 시작 프로젝트로 만들었으므로 자동으로 실행됩니다.)

    ![Contoso Ads 홈 페이지](./media/websites-dotnet-webjobs-sdk-get-started/home.png)
2. 응용 프로그램의 WebJob 백 엔드를 시작하려면 **솔루션 탐색기**에서 ContosoAdsWebJob 프로젝트를 마우스 오른쪽 단추로 클릭하고 **디버그** > **새 인스턴스 시작**을 클릭합니다.

    콘솔 응용 프로그램 창이 열리고 WebJob SDK JobHost 개체의 실행이 시작되었음을 나타내는 로깅 메시지가 표시됩니다.

    ![백 엔드가 실행 중임을 나타내는 콘솔 응용 프로그램 창](./media/websites-dotnet-webjobs-sdk-get-started/backendrunning.png)
3. 브라우저에서 **광고 만들기**를 클릭합니다.
4. 일부 테스트 데이터를 입력하고 업로드할 이미지를 선택한 다음 **만들기**를 클릭합니다.

    ![만들기 페이지](./media/websites-dotnet-webjobs-sdk-get-started/create.png)

    앱이 인덱스 페이지로 이동하지만 아직 처리가 이루어지지 않았기 때문에 새 광고에 대한 미리 보기를 표시하지는 않습니다.

    잠시 후에 콘솔 응용 프로그램 창의 로깅 메시지에 큐 메시지가 수신되고 처리되었다는 정보가 표시됩니다.

    ![큐 메시지가 처리되었음을 나타내는 콘솔 응용 프로그램 창](./media/websites-dotnet-webjobs-sdk-get-started/backendlogs.png)
5. 콘솔 응용 프로그램 창에 로깅 메시지가 표시되면 인덱스 페이지를 새로 고쳐 미리 보기를 확인합니다.

    ![인덱스 페이지](./media/websites-dotnet-webjobs-sdk-get-started/list.png)
6. 광고에 해당하는 **자세히** 를 클릭하여 전체 크기 이미지를 표시합니다.

    ![자세히 페이지](./media/websites-dotnet-webjobs-sdk-get-started/details.png)

로컬 컴퓨터에서 응용 프로그램을 실행하고 있으며, 해당 응용 프로그램은 컴퓨터에 있는 SQL Server 데이터베이스를 사용하고 있지만 클라우드의 큐 및 Blob을 사용하고 있습니다. 다음 섹션에서는 클라우드 데이터베이스와 클라우드 Blob 및 큐를 사용하여 클라우드에서 응용 프로그램을 실행합니다.  

## <a id="runincloud"></a>클라우드에서 응용 프로그램 실행
클라우드에서 응용 프로그램을 실행하려면 다음 단계를 수행합니다.

* 웹앱에 배포합니다. Visual Studio는 앱 서비스의 새 웹앱 및 SQL 데이터베이스 인스턴스를 자동으로 만듭니다.
* Azure SQL 데이터베이스 및 저장소 계정을 사용하도록 웹앱을 구성합니다.

클라우드에서 실행되는 동안 일부 광고를 만든 후에는 WebJob SDK 대시보드를 확인하면서 이 대시보드가 제공해야 하는 풍부한 모니터링 기능을 확인할 것입니다.

### <a name="deploy-to-web-apps"></a>웹앱에 배포

1. 브라우저 및 콘솔 응용 프로그램 창을 닫습니다.
2. [SQL Database를 사용하여 Azure에 게시](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) 섹션의 단계를 따릅니다.
3. 배포 단계를 완료한 후 이 문서의 나머지 작업을 계속 수행합니다.

### <a name="configure-the-web-app-to-use-your-azure-sql-database-and-storage-account"></a>Azure SQL Database 및 저장소 계정을 사용하도록 웹앱 구성
[연결 문자열과 같은 민감한 정보를 소스 코드 리포지토리에 저장된 파일에 두지 않는 방식](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets)(영문)이 보안 모범 사례입니다. Azure에서 이 작업을 수행할 수 있습니다. 즉, Azure 환경에서 연결 문자열 및 기타 설정 값을 지정하면 앱이 Azure에서 실행될 때 ASP.NET 구성 API가 해당 값을 자동으로 선택합니다. **서버 탐색기**, Azure Portal, Windows PowerShell 또는 플랫폼 간 명령줄 인터페이스를 사용하여 Azure에서 이러한 값을 설정할 수 있습니다. 자세한 내용은 [응용 프로그램 문자열 및 연결 문자열 작동 방식](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)을 참조하세요.

이 섹션에서는 **서버 탐색기** 를 사용하여 Azure에서 연결 문자열 값을 설정합니다.

1. **서버 탐색기**의 **Azure > App Service > {리소스 그룹}**에서 웹앱을 마우스 오른쪽 단추로 클릭한 다음 **설정 보기**를 클릭합니다.

    **Azure 웹앱** 창이 **구성** 탭에서 열립니다.
2. DefaultConnection 연결 문자열의 이름을 [SQL Database를 사용하여 Azure에 게시](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) 문서에서 SQL Database를 구성할 때 선택한 이름으로 변경합니다.

    Azure는 연결된 데이터베이스로 이 웹앱을 만들 때 이 연결 문자열을 자동으로 만들기 때문에 이미 적절한 연결 문자열 값이 지정되어 있을 것입니다. 코드가 찾는 이름으로 변경하면 됩니다.
3. AzureWebJobsStorage 및 AzureWebJobsDashboard의 두 연결 문자열을 추가합니다. 데이터베이스 유형을 **사용자 지정**으로 설정하고 연결 문자열 값을 이전에 *Web.config* 및 *App.config* 파일에 사용했던 것과 동일한 값으로 설정합니다. 액세스 키만이 아니라 전체 연결 문자열을 포함해야 하며 따옴표는 제외합니다.

    이러한 연결 문자열은 WebJob SDK에서 응용 프로그램 데이터와 로깅에 각각 사용됩니다. 앞서 살펴본 것처럼 응용 프로그램 데이터용 연결 문자열은 웹 프런트 엔드 코드에도 사용됩니다.
4. **Save**를 클릭합니다.

    ![Azure 포털의 연결 문자열](./media/websites-dotnet-webjobs-sdk-get-started/azconnstr.png)
5. **서버 탐색기**에서 웹앱을 마우스 오른쪽 단추로 클릭하고 **중지**를 클릭합니다.
6. 웹앱이 중지된 후 웹앱을 마우스 오른쪽 단추로 다시 클릭하고 **시작**을 클릭합니다.

   WebJob은 게시될 때 자동으로 시작되지만 구성을 변경하면 중지됩니다. WebJob을 다시 시작하려면 [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715)에서 웹앱을 다시 시작하거나 WebJob을 다시 시작합니다. 일반적으로는 구성을 변경한 후에는 웹앱을 다시 시작하는 것이 좋습니다.
7. 주소 표시줄에 웹앱 URL이 표시되는 브라우저 창을 새로 고칩니다.

    홈 페이지가 나타납니다.
8. [응용 프로그램을 로컬로 실행](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally)했을 때처럼 광고를 만듭니다.

   처음에 미리 보기 없이 인덱스 페이지가 표시됩니다.
9. 몇 초 후에 페이지를 새로 고치면 미리 보기가 나타납니다.

   축소판 그림이 표시되지 않으면 WebJob을 다시 시작하기 위해 일 분 정도 대기해야 합니다. 잠시 후에도 페이지를 새로 고칠 때 축소판 그림이 여전히 표시되지 않으면 WebJob은 자동으로 시작되지 않을 수 있습니다. 이 경우 [Azure Portal](https://portal.azure.com/)의 **App Services** 블레이드로 이동하여 웹앱을 찾은 다음 **시작**을 클릭합니다.

### <a name="view-the-webjobs-sdk-dashboard"></a>WebJob SDK 대시보드 보기
1. [Azure Portal](https://portal.azure.com/)에서 **App Services 블레이드**를 선택하고 웹앱을 찾은 후 **WebJobs**를 선택합니다.
3. **로그** 탭을 선택합니다.

    ![로그 탭](./media/websites-dotnet-webjobs-sdk-get-started/log-tab.png)

    새 브라우저 탭에서 WebJob SDK 대시보드가 열립니다. 이 대시보드에는 WebJob이 실행 중이라고 표시되며 WebJob SDK가 트리거한 코드의 함수 목록이 표시됩니다.
4. 함수 중 하나를 클릭하여 실행에 대한 세부 정보를 확인합니다.

    ![WebJob SDK 대시보드](./media/websites-dotnet-webjobs-sdk-get-started/wjdashboardhome.png)

    ![WebJob SDK 대시보드](./media/websites-dotnet-webjobs-sdk-get-started/wjfunctiondetails.png)

    이 페이지의 **Replay Function(함수 재생)** 단추를 클릭하면 WebJob SDK 프레임워크가 해당 함수를 다시 호출하며 처음에 함수에 전달된 데이터를 변경할 기회가 제공됩니다.

> [!NOTE]
> 테스트를 마치면 웹앱, 저장소 계정 및 SQL Database 인스턴스를 삭제하는 것이 좋습니다. 웹앱은 무료이지만 SQL 저장소 계정 및 데이터베이스 인스턴스는 요금이 부과됩니다(크기가 작으므로 소량 부과됨). 또한 이 앱을 실행 중인 채로 두는 경우에는 누군가가 URL을 발견하면 광고를 만들고 볼 수 있습니다. 
>
>

### <a name="delete-your-web-app"></a>웹앱 삭제
포털에서 **App Services** 블레이드로 이동하여 웹앱을 찾아서 선택하고 **삭제**를 클릭합니다. 임시로 다른 사람이 웹 앱에 액세스하지 못하도록 하려면 대신 **중지** 를 클릭합니다. 이 경우에는 SQL 데이터베이스 및 저장소 계정에 대해 요금이 계속해서 발생합니다.

### <a name="delete-your-storage-account"></a>저장소 계정 삭제
저장소 계정을 삭제하려면 [저장소 계정 삭제](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account)를 참조하세요. 

### <a name="delete-your-database"></a>데이터베이스 삭제
SQL Database를 삭제하려면 [Azure SQL Database REST API](https://docs.microsoft.com/rest/api/sql/) 설명서를 참조하세요.

## <a id="create"></a>처음부터 응용 프로그램 만들기
이 섹션에서는 다음 작업을 수행합니다.

* 웹 프로젝트를 사용하여 Visual Studio 솔루션을 만듭니다.
* 프런트 엔드와 백 엔드 간에 공유되는 데이터 액세스 계층에 대한 클래스 라이브러리 프로젝트를 추가합니다.
* WebJob 배포를 설정한 상태로 백 엔드에 대한 콘솔 응용 프로그램 프로젝트를 추가합니다.
* NuGet 패키지를 추가합니다.
* 프로젝트 참조를 설정합니다.
* 자습서 이전 섹션에서 사용했던 다운로드한 응용 프로그램의 응용 프로그램 코드 및 구성 파일을 복사합니다.
* Azure Blob 및 큐와 WebJob SDK를 사용하는 코드 부분을 검토합니다.

### <a name="create-a-visual-studio-solution-with-a-web-project-and-class-library-project"></a>웹 프로젝트 및 클래스 라이브러리 프로젝트를 사용하여 Visual Studio 솔루션 만들기
1. Visual Studio에서 **파일** > **새로 만들기** > **프로젝트**를 선택합니다.
2. **새 프로젝트** 대화 상자에서 **Visual C#** > **웹** > **ASP.NET 웹 응용 프로그램(.NET Framework)**을 클릭합니다.
3. 프로젝트 이름을 ContosoAdsWeb으로, 솔루션 이름을 ContosoAdsWebJobsSDK로 지정하고(다운로드한 솔루션과 같은 폴더에 배치하는 경우에는 솔루션 이름 변경) **확인**을 클릭합니다.

    ![새 프로젝트](./media/websites-dotnet-webjobs-sdk-get-started/newproject.png)
4. **새 ASP.NET 웹 응용 프로그램** 대화 상자에서 MVC 템플릿을 선택하고 **인증 변경**을 선택합니다.

    ![인증 변경](./media/websites-dotnet-webjobs-sdk-get-started/chgauth.png)
5. **인증 변경** 대화 상자에서 **인증 없음**을 선택한 다음 **확인**을 클릭합니다.

    ![인증 없음](./media/websites-dotnet-webjobs-sdk-get-started/noauth.png)
6. **새 ASP.NET 웹 응용 프로그램** 대화 상자에서 **확인**을 클릭합니다.

    Visual Studio에서 솔루션 및 웹 프로젝트를 만듭니다.
7. **솔루션 탐색기**에서 솔루션(프로젝트 아님)을 마우스 오른쪽 단추로 클릭하고 **추가** > **새 프로젝트**를 선택합니다.
8. **새 프로젝트 추가** 대화 상자에서 **Visual C#** > **Windows 클래식 데스크톱** > **클래스 라이브러리(.NET Framework)** 템플릿을 선택합니다.  
9. 프로젝트의 이름을 *ContosoAdsCommon*으로 지정한 다음 **확인**을 클릭합니다.

    이 프로젝트에는 프런트 엔드 및 백 엔드 둘 다에서 사용할 Entity Framework 컨텍스트와 데이터 모델이 포함됩니다. 또는 웹 프로젝트에서 EF 관련 클래스를 정의하고 WebJob 프로젝트에서 이 프로젝트를 참조할 수 있습니다. 하지만 WebJob 프로젝트에는 필요 없는 웹 어셈블리 참조가 포함됩니다.

### <a name="add-a-console-application-project-that-has-webjobs-deployment-enabled"></a>WebJob 배포가 설정된 콘솔 응용 프로그램 프로젝트 추가
1. 웹 프로젝트(솔루션 또는 클래스 라이브러리 프로젝트 아님)를 마우스 오른쪽 단추로 클릭하고 **추가** > **New Azure WebJob Project(새 Azure WebJob 프로젝트)**를 사용하는 간단한 다중 계층 ASP.NET MVC 5 응용 프로그램에 코드를 작성하는 방법을 보여줍니다.

    ![New Azure WebJob Project(새 Azure WebJob 프로젝트) 프로젝트 메뉴 선택 항목](./media/websites-dotnet-webjobs-sdk-get-started/newawjp.png)
2. **Azure WebJob 추가** 대화 상자에서 **프로젝트 이름**과 **WebJob 이름**으로 ContosoAdsWebJob을 입력합니다. **WebJob 실행 모드**를 **계속 실행**으로 설정합니다.
3. **확인**을 클릭합니다.

   Visual Studio는 웹 프로젝트를 배포할 때마다 WebJob으로 배포되도록 구성된 콘솔 응용 프로그램을 만듭니다. 이렇게 하기 위해 프로젝트를 만든 후에 다음 작업을 수행했습니다.

   * WebJob 프로젝트 속성 폴더에 *webjob-publish-settings.json* 파일을 추가했습니다.
   * 웹 프로젝트 속성 폴더에 *webjobs-list.json* 파일을 추가했습니다.
   * WebJob 프로젝트에 Microsoft.Web.WebJobs.Publish NuGet 패키지를 설치했습니다.

   이러한 변경에 대한 자세한 내용은 [Visual Studio를 사용하여 WebJob을 배포하는 방법](websites-dotnet-deploy-webjobs.md)을 참조하세요.

### <a name="add-nuget-packages"></a>NuGet 패키지 추가
WebJob 프로젝트에 대한 new-project 템플릿이 WebJobs SDK NuGet 패키지 [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) 와 해당 종속성을 자동으로 설치합니다.

WebJob 프로젝트에서 자동으로 설치되는 WebJob SDK 종속성 중 하나는 Azure SCL(저장소 클라이언트 라이브러리)입니다. 그러나 Blob 및 큐 작업을 수행하려면 웹 프로젝트에 추가해야 합니다.

1. 솔루션에 대한 **NuGet 패키지 관리** 대화 상자를 엽니다.
2. 왼쪽 창에서 **설치된 패키지**을 선택합니다.
3. *Azure Storage* 패키지를 찾은 후 **관리**를 클릭합니다.
4. **프로젝트 선택** 상자에서 **ContosoAdsWeb** 확인란을 선택하고 **확인**을 클릭합니다.

    이러한 세 프로젝트는 SQL 데이터베이스의 데이터를 사용하기 위해 Entity Framework를 사용합니다.
5. 왼쪽 창에서 **온라인**을 선택합니다.
6. *EntityFramework* NuGet 패키지를 찾아 세 개의 프로젝트 모두에서 설치합니다.

### <a name="set-project-references"></a>프로젝트 참조 설정
웹 및 WebJob 프로젝트 둘 다에서 SQL 데이터베이스를 사용하므로 ContosoAdsCommon 프로젝트에 대한 참조가 필요합니다.

1. ContosoAdsWeb 프로젝트에서 ContosoAdsCommon 프로젝트에 대한 참조를 설정합니다. ContosoAdsWeb 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **추가** > **참조**를 사용하는 간단한 다중 계층 ASP.NET MVC 5 응용 프로그램에 코드를 작성하는 방법을 보여줍니다. 
2. **참조 관리자** 대화 상자에서 **프로젝트** > **솔루션** > **ContosoAdsCommon**을 차례로 선택한 후 **확인**을 클릭합니다.
   
    WebJob 프로젝트는 이미지를 사용하고 연결 문자열에 액세스하기 위해 참조가 필요합니다.

4. ContosoAdsWebJob 프로젝트에서 `System.Drawing` 및 `System.Configuration`에 대한 참조를 설정합니다.

### <a name="add-code-and-configuration-files"></a>코드 및 구성 파일 추가
이 자습서에 [스캐폴딩을 사용하여 MVC 컨트롤러 및 보기를 만드는 방법](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)(영문), [SQL Server 데이터베이스를 사용하는 Entity Framework 코드를 작성하는 방법](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc)(영문) 또는 [ASP.NET 4.5의 비동기 프로그래밍에 대한 기본 사항](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async)(영문)은 나와 있지 않습니다. 이 작업을 수행하려면 다운로드한 솔루션에서 새 솔루션으로 코드 및 구성 파일을 복사합니다. 이 작업을 수행한 후에는 다음 섹션에서 코드의 핵심 부분에 대한 설명을 확인할 수 있습니다.

프로젝트나 폴더에 파일을 추가하려면 프로젝트나 폴더를 마우스 오른쪽 단추로 클릭하고 **추가** > **기존 항목**를 사용하는 간단한 다중 계층 ASP.NET MVC 5 응용 프로그램에 코드를 작성하는 방법을 보여줍니다. 원하는 파일을 선택하고 **추가**를 클릭합니다. 기존 파일을 바꿀지 여부를 묻는 메시지가 나타나면 **예**를 클릭합니다.

1. ContosoAdsCommon 프로젝트에서 *Class1.cs* 파일을 삭제하고 그 자리에 다운로드한 프로젝트의 다음 파일을 추가합니다.

   * *Ad.cs*
   * *ContosoAdscontext.cs*
   * *BlobInformation.cs*
2. ContosoAdsWeb 프로젝트에 다운로드한 프로젝트에서 가져온 다음 파일을 추가합니다.

   * *Web.config*
   * *Global.asax.cs*  
   * *Controllers* 폴더: *AdController.cs*
   * *Views\Shared* 폴더: *_Layout.cshtml* 파일
   * *Views\Home* 폴더: *Index.cshtml*
   * *Views\Ad* 폴더(먼저 폴더 만들기): 5개의 *.cshtml* 파일
3. ContosoAdsWebJob 프로젝트에서 다운로드한 프로젝트에서 가져온 다음 파일을 추가합니다.

   * *App.config* (파일 형식 필터를 **모든 파일**로 변경)
   * *Program.cs*
   * *Functions.cs*

이제 자습서의 앞부분에 설명된 대로 응용 프로그램을 빌드, 실행 및 배포할 수 있습니다. 이 작업을 수행하기 전에 배포한 첫 번째 웹앱에서 여전히 실행되고 있는 WebJob을 중지합니다. 그렇지 않으면 모두가 동일한 저장소 계정을 사용하고 있으므로 해당 WebJob이 로컬로 만들어졌거나 새 웹앱에서 실행되고 있는 앱에 의해 만들어진 큐 메시지를 처리하게 됩니다.

## <a id="code"></a>응용 프로그램 코드 검토
다음 섹션에서는 WebJob SDK 및 Azure 저장소 Blob와 큐 작업과 관련된 코드에 대해 설명합니다.

> [!NOTE]
> WebJob SDK 관련 코드의 경우 [Program.cs 및 Functions.cs](#programcs) 섹션으로 이동합니다.
>
>

### <a name="contosoadscommon---adcs"></a>ContosoAdsCommon - Ad.cs
Ad.cs 파일은 광고 범주의 열거형 및 광고 정보에 대한 POCO 엔터티 클래스를 정의합니다.

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

### <a name="contosoadscommon---contosoadscontextcs"></a>ContosoAdsCommon - ContosoAdsContext.cs
ContosoAdsContext 클래스는 DbSet 컬렉션에서 Ad 클래스가 사용된다는 것을 지정하며, Entity Framework는 이를 SQL 데이터베이스에 저장합니다.

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

이 클래스에는 두 개의 생성자가 있습니다. 첫 번째 생성자는 웹 프로젝트에서 사용되며 Web.config 파일 또는 Azure 런타임 환경에 저장되는 연결 문자열의 이름을 지정합니다. 두 번째 생성자는 실제 연결 문자열을 전달할 수 있게 합니다. 이 과정은 WebJob 프로젝트에서 필요합니다. 여기에는 Web.config 파일이 없기 때문입니다. 앞에서 이 연결 문자열이 저장된 위치를 확인했으며, 이후에 코드가 DbContext 클래스를 인스턴스화할 때 연결 문자열을 검색하는 방법을 확인하게 될 것입니다.

### <a name="contosoadscommon---blobinformationcs"></a>ContosoAdsCommon - BlobInformation.cs
`BlobInformation` 클래스는 큐 메시지의 이미지 Blob에 대한 정보를 저장하는 데 사용됩니다.

        public class BlobInformation
        {
            public Uri BlobUri { get; set; }

            public string BlobName
            {
                get
                {
                    return BlobUri.Segments[BlobUri.Segments.Length - 1];
                }
            }
            public string BlobNameWithoutExtension
            {
                get
                {
                    return Path.GetFileNameWithoutExtension(BlobName);
                }
            }
            public int AdId { get; set; }
        }


### <a name="contosoadsweb---globalasaxcs"></a>ContosoAdsWeb - Global.asax.cs
`Application_Start` 메서드에서 호출되는 코드는 *images* Blob 컨테이너 및 *images* 큐를 만듭니다(아직 없는 경우). 따라서 새 저장소 계정을 사용하기 시작할 때마다 필수 Blob 컨테이너와 큐가 자동으로 만들어집니다.

이 코드는 *Web.config* 파일 또는 Azure 런타임 환경의 저장소 연결 문자열을 사용하여 저장소 계정에 액세스합니다.

        var storageAccount = CloudStorageAccount.Parse
            (ConfigurationManager.ConnectionStrings["AzureWebJobsStorage"].ToString());

그런 다음, *images* Blob 컨테이너에 대한 참조를 가져오고 컨테이너를 만들고(아직 없는 경우) 새 컨테이너에 대한 액세스 권한을 설정합니다. 기본적으로 새 컨테이너는 저장소 계정 자격 증명이 있는 클라이언트만 Blob에 액세스를 허용합니다. 이미지 Blob을 가리키는 URL을 사용하여 이미지를 표시할 수 있도록 웹앱은 Blob을 공개로 설정해야 합니다.

        var blobClient = storageAccount.CreateCloudBlobClient();
        var imagesBlobContainer = blobClient.GetContainerReference("images");
        if (imagesBlobContainer.CreateIfNotExists())
        {
            imagesBlobContainer.SetPermissions(
                new BlobContainerPermissions
                {
                    PublicAccess = BlobContainerPublicAccessType.Blob
                });
        }

비슷한 코드가 *thumbnailrequest* 큐에 대한 참조를 가져오고 새 큐를 만듭니다. 이 경우에는 권한을 변경할 필요가 없습니다.

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        var imagesQueue = queueClient.GetQueueReference("thumbnailrequest");
        imagesQueue.CreateIfNotExists();

### <a name="contosoadsweb---layoutcshtml"></a>ContosoAdsWeb - _Layout.cshtml
*_Layout.cshtml* 파일은 머리글과 바닥글에서 앱 이름을 설정하고 "Ads" 메뉴 항목을 만듭니다.

### <a name="contosoadsweb---viewshomeindexcshtml"></a>ContosoAdsWeb - Views\Home\Index.cshtml
*Views\Home\Index.cshtml* 파일은 홈페이지에 범주 링크를 표시합니다. 이 링크는 쿼리 문자열 변수의 `Category` 열거형 정수 값을 광고 인덱스 페이지에 전달합니다.

        <li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
        <li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
        <li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
        <li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>

### <a name="contosoadsweb---adcontrollercs"></a>ContosoAdsWeb - AdController.cs
*AdController.cs* 파일에서 생성자는 `InitializeStorage` 메서드를 호출하여 Blob 및 큐 작업을 위한 API를 제공하는 Azure Storage 클라이언트 라이브러리 개체를 만듭니다.

그런 다음 이 코드는 앞서 *Global.asax.cs*에서 확인한 *images* Blob 컨테이너에 대한 참조를 가져옵니다. 그 과정에서 웹앱에 해당하는 기본 [재시도 정책](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) (영문)을 설정합니다. 기본 지수 백오프 재시도 정책은 일시적 오류에 대해 반복적으로 재시도하는 경우 1분 넘게 웹앱을 중지시킬 수 있습니다. 여기에 지정된 재시도 정책은 각 시도 후 3초 동안 최대 3회까지 대기합니다.

        var blobClient = storageAccount.CreateCloudBlobClient();
        blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesBlobContainer = blobClient.GetContainerReference("images");

비슷한 코드가 *images* 큐에 대한 참조를 가져옵니다.

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesQueue = queueClient.GetQueueReference("blobnamerequest");

대부분의 컨트롤러 코드는 DbContext 클래스를 사용한 Entity Framework 데이터 모델 작업에 일반적입니다. 예외는 HttpPost `Create` 서드이며, 이 메서드는 파일을 업로드하고 Blob 저장소에 저장합니다. 모델 바인더는 메서드에 [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) 개체를 제공합니다.

        [HttpPost]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> Create(
            [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
            HttpPostedFileBase imageFile)

사용자가 업로드할 파일을 선택한 경우 코드는 파일을 업로드하고 Blob에 저장하며 광고 데이터베이스 레코드를 Blob을 가리키는 URL로 업데이트합니다.

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            blob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = blob.Uri.ToString();
        }

업로드를 수행하는 코드는 `UploadAndSaveBlobAsync` 메서드에 있습니다. Blob에 대한 GUID 이름을 만들고, 파일을 업로드 및 저장하며, 저장된 Blob에 대한 참조를 반환합니다.

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

HttpPost `Create` 메서드가 Blob을 업로드하고 데이터베이스를 업데이트한 후에는 이미지를 미리 보기로 변환할 수 있는 백 엔드 프로세스에 대해 알리는 큐 메시지를 만듭니다.

        BlobInformation blobInfo = new BlobInformation() { AdId = ad.AdId, BlobUri = new Uri(ad.ImageURL) };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        await thumbnailRequestQueue.AddMessageAsync(queueMessage);

HttpPost `Edit` 메서드의 코드도 비슷하지만, 사용자가 새 이미지 파일을 선택하면 이 광고에 대해 이미 존재하는 Blob을 삭제해야 한다는 점은 다릅니다.

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            await DeleteAdBlobsAsync(ad);
            imageBlob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = imageBlob.Uri.ToString();
        }

다음은 광고를 삭제하면 Blob를 삭제하는 코드입니다.

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

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a>ContosoAdsWeb - Views\Ad\Index.cshtml 및 Details.cshtml
*Index.cshtml* 파일은 다른 광고 데이터가 포함된 미리 보기를 표시합니다.

        <img  src="@Html.Raw(item.ThumbnailURL)" />

*Details.cshtml* 파일은 전체 크기 이미지를 표시합니다.

        <img src="@Html.Raw(Model.ImageURL)" />

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a>ContosoAdsWeb - Views\Ad\Create.cshtml 및 Edit.cshtml
*Create.cshtml* 및 *Edit.cshtml* 파일은 컨트롤러가 `HttpPostedFileBase` 개체를 가져올 수 있게 하는 양식 인코딩을 지정합니다.

        @using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))

`<input>` 요소는 파일 선택 대화 상자를 제공하도록 브라우저에 지시합니다.

        <input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />

### <a id="programcs"></a>ContosoAdsWebJob - Program.cs
WebJob이 시작되면 `Main` 메서드가 WebJob SDK `JobHost.RunAndBlock` 메서드를 호출하여 현재 스레드에서 트리거한 함수의 실행을 시작합니다.

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

### <a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - GenerateThumbnail 메서드
WebJob SDK는 큐 메시지가 수신될 때 이 메서드를 호출합니다. 이 메서드는 미리 보기를 만든 후 데이터베이스에 미리 보기 URL을 추가합니다.

        public static void GenerateThumbnail(
        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,
        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)
        {
            using (Stream output = outputBlob.OpenWrite())
            {
                ConvertImageToThumbnailJPG(input, output);
                outputBlob.Properties.ContentType = "image/jpeg";
            }

            // Entity Framework context class is not thread-safe, so it must
            // be instantiated and disposed within the function.
            using (ContosoAdsContext db = new ContosoAdsContext())
            {
                var id = blobInfo.AdId;
                Ad ad = db.Ads.Find(id);
                if (ad == null)
                {
                    throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", id.ToString()));
                }
                ad.ThumbnailURL = outputBlob.Uri.ToString();
                db.SaveChanges();
            }
        }

* `QueueTrigger` 특성은 thumbnailrequest 큐에 새 메시지가 수신될 때 WebJob SDK가 이 메서드를 호출하도록 합니다.

        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,

    큐 메시지의 `BlobInformation` 개체는 자동으로 `blobInfo` 매개 변수로 역직렬화됩니다. 이 메서드가 완료되면 큐 메시지가 삭제됩니다. 완료되기 전에 메서드가 실패하면 큐 메시지는 삭제되지 않고 10분의 임대 기간이 만료되면 선택하여 처리할 수 있게 메시지가 해제됩니다. 메시지가 항상 예외를 발생하는 경우에는 이 시퀀스가 무한 반복되지 않습니다. 메시지 처리 시도가 5회 연속으로 실패하면 메시지는 {queuename}-poison 큐로 이동됩니다. 최대 시도 횟수는 구성 가능합니다.
* 두 `Blob` 특성은 Blob에 바인딩된 개체를 제공합니다. 하나는 기존 이미지 Blob에 바인딩되고 다른 하나는 메서드가 만드는 새 축소판 그림 Blob에 바인딩됩니다.

        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)

    Blob 이름은 큐 메시지(`BlobName` 및 `BlobNameWithoutExtension`)에 수신된 `BlobInformation` 개체의 속성을 기반으로 합니다. 저장소 클라이언트 라이브러리의 전기능을 사용하려는 경우 `CloudBlockBlob` 클래스를 사용하여 Blob을 작동할 수 있습니다. `Stream` 개체 사용을 위해 작성한 코드를 다시 사용하려면 `Stream` 클래스를 사용할 수 있습니다.

WebJobs SDK 특성을 사용하는 함수를 작성하는 방법에 대한 자세한 내용은 다음 리소스를 참조하세요.

* [WebJobs SDK를 사용하여 Azure 큐 저장소로 작업하는 방법](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [WebJob SDK를 사용하여 Azure Blob 저장소로 작업하는 방법](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [WebJob SDK를 사용하여 Azure 테이블 저장소로 작업하는 방법](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [WebJob SDK를 사용하여 Azure 서비스 버스로 작업하는 방법](websites-dotnet-webjobs-sdk-service-bus.md)

> [!NOTE]
> * 웹앱이 여러 VM에서 실행되는 경우 여러 WebJob이 동시에 실행되며, 일부 시나리오에서 이렇게 하면 동일한 데이터를 여러 번 처리할 수 있습니다. 기본 제공 큐, blob 및 서비스 버스 트리거를 사용하는 경우 이는 문제가 되지 않습니다. SDK는 각 메시지 또는 blob에 대해 함수를 한 번만 처리하도록 합니다.
> * 정상 종료를 구현하는 방법에 대한 자세한 내용은 [정상 종료](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful)를 참조하세요.
> * `ConvertImageToThumbnailJPG` 메서드의 코드(표시되지 않음)는 간소화를 위해 `System.Drawing` 네임스페이스의 클래스를 사용합니다. 하지만 이 네임스페이스의 클래스는 Windows Forms에서 사용하도록 설계되었습니다. Windows 또는 ASP.NET 서비스에서 사용할 수 있도록 지원되지 않습니다. 이미지 처리 옵션에 대한 자세한 내용은 [동적 이미지 생성](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) 및 [이미지 크기 조정 세부 정보](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na)를 참조하세요.
>
>

## <a name="next-steps"></a>다음 단계
이 자습서에서는 백 엔드 처리를 위해 WebJob SDK를 사용하는 간단한 다중 계층 응용 프로그램을 살펴보았습니다. 이 섹션에서는 ASP.NET 다중 계층 응용 프로그램 및 Webjob에 대해 더 알아볼 몇 가지 제안을 제공합니다.

### <a name="missing-features"></a>누락된 기능
이 응용 프로그램은 시작 자습서용으로 단순하게 유지되었습니다. 실제 응용 프로그램에서는 [종속성 주입](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) 또는 [리포지토리 및 작업 단위 패턴](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo)을 구현하지 않고 [로깅용 인터페이스](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log)를 사용하며 데이터 모델 변경을 관리하는 데 [EF Code First 마이그레이션](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application)을 사용하고 일시적인 네트워크 오류를 관리하는 데 [EF 연결 복원](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application)을 사용합니다.

### <a name="scaling-webjobs"></a>WebJob 크기 조정
WebJob은 웹앱의 컨텍스트에서 실행되며 별도로 확장 가능하지 않습니다. 예를 들어 표준 웹앱의 인스턴스가 하나 있으면 실행 중인 백그라운드 프로세스 인스턴스가 하나만 있고 웹 콘텐츠를 제공하는 데 사용될 수 있는 일부 서버 리소스(CPU, 메모리 등)를 사용하고 있습니다.

트래픽이 하루 중 시간이나 주중 요일별로 다르고 수행해야 하는 백 엔드 처리가 대기될 수 있는 경우 트래픽이 낮은 시간에 WebJob이 실행되도록 예약할 수 있습니다. 부하가 여전히 해당 솔루션에 대해 너무 높은 경우 백 엔드를 해당 용도에 전용된 별도 웹앱에서 WebJob으로 실행할 수 있습니다. 그런 후 프런트 엔드 웹앱과는 별도로 백 엔드 웹앱을 확장할 수 있습니다.

자세한 내용은 [WebJob 확장](websites-webjobs-resources.md#scale)을 참조하세요.

### <a name="avoiding-web-app-timeout-shut-downs"></a>웹앱 시간 제한 종료 방지
WebJob이 항상 실행되고 웹앱의 모든 인스턴스에서 실행되도록 하려면 [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) 기능을 사용하도록 설정해야 합니다.

### <a name="using-the-webjobs-sdk-outside-of-webjobs"></a>WebJob 외부에서 WebJob SDK 사용
WebJob SDK를 사용하는 프로그램은 WebJob의 Azure에서 실행될 필요가 없습니다. 로컬에서 실행할 수 있고 클라우드 서비스 작업자 역할 또는 Windows 서비스와 같은 다른 환경에서도 실행할 수 있습니다. 하지만 WebJob SDK 대시보드에는 Azure 웹앱을 통해서만 액세스할 수 있습니다. 이 대시보드를 사용하려면 클래식 포털의 **구성** 탭에서 AzureWebJobsDashboard 연결 문자열을 설정하여 사용 중인 저장소 계정에 웹앱을 연결해야 합니다. 그런 후 다음 URL을 사용하여 대시보드로 이동할 수 있습니다.

https://{webappname}.scm.azurewebsites.net/azurejobs/#/functions

자세한 내용은 [WebJobs SDK를 사용한 로컬 개발을 위해 대시보드 가져오기](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx)(영문)를 참조하세요. 단 여기에는 이전 연결 문자열 이름이 표시됩니다.

### <a name="more-webjobs-documentation"></a>더 자세한 WebJob 설명서
자세한 내용은 [Azure WebJob 설명서 리소스](http://go.microsoft.com/fwlink/?LinkId=390226)를 참조하세요.
