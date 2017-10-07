---
title: "hello.NET 백 엔드 서버 모바일 앱에 대 한 SDK와 aaaHow toowork | Microsoft Docs"
description: "Azure 앱 서비스 모바일 앱에 대 한와 toowork.NET 백 엔드 서버 SDK hello 하는 방법에 대해 알아봅니다."
keywords: "앱 서비스, Azure 앱 서비스, 모바일 앱, 모바일 서비스, 규모, 확장성, 앱 배포, Azure 앱 배포"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 0620554f-9590-40a8-9f47-61c48c21076b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2946c5ba4424565ac764e2ce5597bf42362fcedf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-hello-net-backend-server-sdk-for-azure-mobile-apps"></a>Azure 모바일 앱에 대 한 hello.NET 백 엔드 서버 SDK 사용
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

이 항목에서는 toouse 주요 Azure 앱 서비스 모바일 앱 시나리오에서.NET 백 엔드 서버 SDK hello 하는 방법을 보여 줍니다. hello Azure 모바일 앱 SDK를 사용 하면 모바일 클라이언트 및 ASP.NET 응용 프로그램에서 작동 합니다.

> [!TIP]
> hello [.NET 서버 Azure 모바일 앱에 대 한 SDK] [ 2] 은 GitHub의 오픈 소스입니다. hello 리포지토리 hello 전체 서버 SDK 단위 테스트 도구 모음 및 일부 샘플 프로젝트를 포함 하 여 모든 소스 코드를 포함 합니다.
>
>

## <a name="reference-documentation"></a>참조 설명서
hello 서버 SDK에 대 한 참조 설명서 hello은 여기에서 찾을: [Azure 모바일 앱.NET 참조][1]합니다.

## <a name="create-app"></a>방법: .NET 모바일 앱 백 엔드 만들기
새 프로젝트를 시작 하는 경우에 어느 hello를 사용 하 여 응용 프로그램 서비스 응용 프로그램을 만들 수 있습니다 [Azure 포털] 또는 Visual Studio입니다. Hello 응용 프로그램 서비스 응용 프로그램을 로컬로 실행 하거나 hello 프로젝트 tooyour 클라우드 기반 앱 서비스 모바일 앱을 게시할 수 있습니다.

모바일 기능 tooan 기존 프로젝트를 추가 하는 경우 참조 hello [다운로드 하 고 hello SDK 초기화](#install-sdk) 섹션.

### <a name="create-a-net-backend-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여.NET 백 엔드 만들기
hello를 수행 하거나 앱 서비스 모바일 백 엔드 toocreate [빠른 시작 자습서] [ 3] 하거나이 단계를 수행 합니다.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

Hello에 다시 *시작* 블레이드 아래 **API 테이블을 만들**, 선택 **C#** 으로 프로그램 **백 엔드 언어**합니다. 클릭 **다운로드**, 압축 된 프로젝트 파일 tooyour 로컬 컴퓨터에 압축을 풀고 Visual Studio에서 hello 솔루션을 엽니다.

### <a name="create-a-net-backend-using-visual-studio-2013-and-visual-studio-2015"></a>Visual Studio 2013 및 Visual Studio 2015를 사용하여 .NET 백 엔드 만들기
Hello 설치 [Azure SDK for.NET] [ 4] (2.9.0 버전 이상) toocreate Visual Studio에서 Azure 모바일 앱 프로젝트. Hello SDK를 설치한 경우 단계를 수행 하는 hello를 사용 하 여 ASP.NET 응용 프로그램을 만듭니다.

1. 열기 hello **새 프로젝트** 대화 (에서 *파일* > **새로** > **프로젝트...** ).
2. **템플릿** > **Visual C#**를 확장하고 **웹**을 선택합니다.
3. **ASP.NET 웹 응용 프로그램**을 선택합니다.
4. Hello 프로젝트 이름을 입력 합니다. 그런 후 **OK**를 클릭합니다.
5. *ASP.NET 4.5.2 템플릿*아래에서 **Azure Mobile App**을 선택합니다. 확인 **hello 클라우드의 호스트에에서** toocreate hello에 모바일 백 엔드 클라우드 toowhich이이 프로젝트를 게시할 수 있습니다.
6. **확인**을 클릭합니다.

## <a name="install-sdk"></a>방법: 다운로드 및 hello SDK를 초기화 합니다.
hello SDK는에서 사용할 수 있는 [NuGet.org]합니다. 이 패키지에 hello 필요한 기본 기능 tooget hello SDK를 사용 하 여 시작 합니다. tooinitialize SDK hello, tooperform 작업 hello에 필요한 **HttpConfiguration** 개체입니다.

### <a name="install-hello-sdk"></a>Hello SDK 설치
tooinstall hello SDK, Visual Studio의 hello 서버 프로젝트를 마우스 오른쪽 단추로 선택 **NuGet 패키지 관리**, hello에 대 한 검색 [Microsoft.Azure.Mobile.Server] 패키지 하 고, 한 다음 클릭  **설치**합니다.

### <a name="server-project-setup"></a>Hello 서버 프로젝트를 초기화 합니다.
.NET 백 엔드 서버 프로젝트에는 OWIN 시작 클래스를 포함 하 여 초기화 된 유사한 tooother ASP.NET 프로젝트는. Hello NuGet 패키지를 참조 한 확인 `Microsoft.Owin.Host.SystemWeb`합니다. tooadd Visual Studio에서이 클래스 단추로 클릭 하 여 서버 프로젝트 고 **추가** >
**새 항목**, 다음 **웹**  >  ** 일반** > **OWIN 시작 클래스**합니다.  클래스는 hello 특성을 다음으로 생성 됩니다.

    [assembly: OwinStartup(typeof(YourServiceName.YourStartupClassName))]

Hello에 `Configuration()` OWIN 시작 클래스를 사용 하 여의 메서드로 **HttpConfiguration** 개체 tooconfigure hello Azure 모바일 앱 환경입니다.
다음 예제는 hello 추가 된 기능이 없는 hello 서버 프로젝트를 초기화 합니다.

    // in OWIN startup class
    public void Configuration(IAppBuilder app)
    {
        HttpConfiguration config = new HttpConfiguration();

        new MobileAppConfiguration()
            // no added features
            .ApplyTo(config);

        app.UseWebApi(config);
    }

tooenable 개별 기능 hello에 확장 메서드를 호출 해야 **MobileAppConfiguration** 호출 하기 전에 개체 **ApplyTo**합니다. 예를 들어 hello 코드 다음 추가 hello 기본 라우팅합니다 hello 특성이 있는 tooall API 컨트롤러 `[MobileAppController]` 초기화 하는 동안:

    new MobileAppConfiguration()
        .MapApiControllers()
        .ApplyTo(config);

hello 서버 빠른 시작에서 Azure 포털 호출 hello **UseDefaultConfiguration()**합니다. 다음 단계를이 해당 toohello:

        new MobileAppConfiguration()
            .AddMobileAppHomeController()             // from hello Home package
            .MapApiControllers()
            .AddTables(                               // from hello Tables package
                new MobileAppTableConfiguration()
                    .MapTableControllers()
                    .AddEntityFramework()             // from hello Entity package
                )
            .AddPushNotifications()                   // from hello Notifications package
            .MapLegacyCrossDomainController()         // from hello CrossDomain package
            .ApplyTo(config);

사용 되는 hello 확장 방법은 다음과 같습니다.

* `AddMobileAppHomeController()`hello 기본 Azure 모바일 앱 홈 페이지를 제공합니다.
* `MapApiControllers()`hello로 데코 레이트 된 WebAPI 컨트롤러에 대 한 사용자 지정 API 기능을 제공 `[MobileAppController]` 특성입니다.
* `AddTables()`hello의 매핑을 제공 `/tables` 끝점 tootable 컨트롤러입니다.
* `AddTablesWithEntityFramework()`매핑 hello에 대 한 축약형 `/tables` Entity Framework를 사용 하 여 끝점 컨트롤러를 기반으로 합니다.
* `AddPushNotifications()`은(는) Notification Hubs에 대한 장치를 등록하는 간단한 방법을 제공합니다.
* `MapLegacyCrossDomainController()` 은(는) 로컬 개발을 위한 표준 CORS 헤더를 제공합니다.

### <a name="sdk-extensions"></a>SDK 확장
hello NuGet 기반 확장 패키지를 다음 응용 프로그램에서 사용할 수 있는 다양 한 모바일 기능을 제공 합니다. Hello를 사용 하 여 초기화 하는 동안 확장을 사용 하면 **MobileAppConfiguration** 개체입니다.

* [Microsoft.Azure.Mobile.Server.Quickstart] 지원 hello 기본 모바일 앱 설정 합니다. Hello 호출 하 여 추가 된 toohello 구성을 **UseDefaultConfiguration** 초기화 하는 동안 확장 메서드. 이 확장은 알림, 인증, 엔터티, 테이블, Crossdomain 및 홈 패키지와 같은 확장을 포함합니다. 이 패키지는 hello hello Azure 포털에서 사용할 수 있는 모바일 앱 빠른 시작에서 사용 됩니다.
* [Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) hello 기본 구현 *모바일 앱이 실행 되 고 페이지* hello 웹 사이트 루트에 대 한 합니다. Toohello 구성을 호출 하 여 추가 된 **AddMobileAppHomeController** 확장 메서드.
* [Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) 데이터 및 설정 접속 hello 데이터 파이프라인을 사용 하기 위한 클래스가 포함 됩니다. Hello를 호출 하 여 toohello 구성을 추가 **AddTables** 확장 메서드.
* [Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) hello Entity Framework hello SQL 데이터베이스에서에서 데이터를 tooaccess 수 있도록 합니다. Hello를 호출 하 여 toohello 구성을 추가 **AddTablesWithEntityFramework** 확장 메서드.
* [Microsoft.Azure.Mobile.Server.Authentication] toovalidate 토큰을 사용 하는 사용 하면 인증 및 집합 접속 hello OWIN 미들웨어입니다. Hello를 호출 하 여 toohello 구성을 추가 **AddAppServiceAuthentication** 및 **IAppBuilder**. **UseAppServiceAuthentication** 확장 메서드입니다.
* [Microsoft.Azure.Mobile.Server.Notifications] 푸시 알림을 사용할 수 있도록 하며 푸시 등록 끝점을 정의합니다. Hello를 호출 하 여 toohello 구성을 추가 **AddPushNotifications** 확장 메서드.
* [Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) 데이터 toolegacy 모바일 앱에서 웹 브라우저를 사용 하는 컨트롤러를 만듭니다. Toohello 구성을 호출 하 여 추가 된 **MapLegacyCrossDomainController** 확장 메서드.
* [Microsoft.Azure.Mobile.Server.Login] hello AppServiceLoginHandler.CreateToken() 메서드를 사용자 지정 인증 시나리오를 사용 하는 정적 메서드를 제공 합니다.

## <a name="publish-server-project"></a>방법: hello 서버 프로젝트 게시
이 섹션에서는 어떻게 toopublish.NET 백 엔드에서에서 프로젝트를 Visual Studio를 보여 줍니다. Git를 사용 하 여 백 엔드 프로젝트를 배포할 수도 있습니다 또는 hello에서 설명 하는 다른 방법 중 하나 hello [Azure 앱 서비스 배포 설명서](../app-service-web/web-sites-deploy.md)합니다.

1. Visual Studio에서 hello 프로젝트 toorestore NuGet 패키지를 다시 작성 합니다.
2. 솔루션 탐색기, 마우스 오른쪽 단추로 클릭 hello 프로젝트에서에서 클릭 **게시**합니다. hello 처음 게시할 때는 해야 toodefine 게시 프로필. 이미 정의된 프로필이 있을 때 프로필을 선택하고 **게시**를 클릭합니다.
3. 게시 대상 tooselect 묻는 메시지가 나타나면 클릭 **Microsoft Azure 앱 서비스** > **다음**, (필요한 경우) 한 다음 Azure 자격 증명으로 로그인 합니다.
   Visual Studio가 Azure에서 직접 게시 설정을 안전하게 다운로드하고 저장합니다.

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-1.png)
4. **구독**을 선택하고 **보기**에서 **리소스 형식**을 선택하며 **모바일 앱**을 확장하고 모바일 앱 백 엔드를 클릭한 다음 **확인**을 클릭합니다.

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-2.png)
5. Hello 확인을 클릭 하 고 게시 프로필 정보 **게시**합니다.

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-3.png)

    모바일 앱 백 엔드가 성공적으로 게시되면 성공했다는 것을 나타내는 방문 페이지가 표시됩니다.

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-success.png)

## <a name="define-table-controller"></a> 방법: 테이블 컨트롤러 정의
SQL 테이블 toomobile 클라이언트 테이블 컨트롤러 tooexpose를 정의 합니다.  테이블 컨트롤러를 구성하려면 세 단계가 필요합니다.

1. 데이터 전송 개체(DTO) 클래스를 만듭니다.
2. Hello 모바일 DbContext 클래스에에서 대 한 테이블 참조를 구성 합니다.
3. 테이블 컨트롤러를 만듭니다.

데이터 전송 개체(DTO)는 `EntityData`에서 상속하는 일반 C# 개체입니다.  예:

    public class TodoItem : EntityData
    {
        public string Text { get; set; }
        public bool Complete {get; set;}
    }

hello DTO는 hello SQL 데이터베이스 내에서 사용 되는 toodefine hello 테이블입니다.  toocreate hello 추가, 항목 데이터베이스는 `DbSet<>` 속성을 사용 하는 DbContext hello 합니다.  Azure 모바일 앱에 대 한 기본 프로젝트 템플릿에서 hello hello DbContext 라고 `Models\MobileServiceContext.cs`:

    public class MobileServiceContext : DbContext
    {
        private const string connectionStringName = "Name=MS_TableConnectionString";

        public MobileServiceContext() : base(connectionStringName)
        {

        }

        public DbSet<TodoItem> TodoItems { get; set; }

        protected override void OnModelCreating(DbModelBuilder modelBuilder)
        {
            modelBuilder.Conventions.Add(
                new AttributeToColumnAnnotationConvention<TableColumnAttribute, string>(
                    "ServiceColumnTable", (property, attributes) => attributes.Single().ColumnType.ToString()));
        }
    }

Azure SDK를 설치 하는 hello를 사용 하도록 설정한 경우 다음과 같은 템플릿 테이블 컨트롤러를 만들 이제 있습니다.

1. 안녕하세요 Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가** > **컨트롤러 중...** .
2. 선택 hello **Azure 모바일 앱 테이블 컨트롤러** 클릭 한 다음 옵션을 **추가**합니다.
3. Hello에 **컨트롤러 추가** 대화 상자:
   * Hello에 **모델 클래스** 드롭다운을 선택 하면 새 DTO 합니다.
   * Hello에 **DbContext** 드롭다운에서 선택 hello 모바일 서비스 DbContext 클래스입니다.
   * hello 컨트롤러 이름이 생성 됩니다.
4. **추가**를 클릭합니다.

hello 퀵 스타트 서버 프로젝트에 단순에 대 한 예가 포함 되어 **TodoItemController**합니다.

### <a name="adjust-pagesize"></a>방법: hello 테이블 페이징 크기 조정
기본적으로 Azure 모바일 앱은 요청당 50개의 레코드를 반환합니다.  페이징은 hello 클라이언트 사용 너무 오래 동안 UI 스레드와 hello 서버 효율적인 사용자 환경을 보장 되도록 합니다. toochange hello 테이블 페이징 크기 증가 hello 서버 쪽 "허용 되는 쿼리 크기" 고 hello 클라이언트 쪽 페이지 크기 hello 서버 쪽 "허용 쿼리 크기"는 hello를 사용 하 여 `EnableQuery` 특성:

    [EnableQuery(PageSize = 500)]

Hello PageSize는 hello 클라이언트에서 요청한 hello 크기 보다 크거나 같은 hello를 확인 합니다.  Hello 클라이언트 페이지 크기 변경에 대 한 내용은 toohello 특정 클라이언트 방법 문서를 참조 하십시오.

## <a name="how-to-define-a-custom-api-controller"></a>방법: 사용자 지정 API 컨트롤러 정의
사용자 지정 API 컨트롤러 hello 끝점을 노출 하 여 hello 가장 기본적인 기능 tooyour 모바일 앱 백 엔드를 제공 합니다. Hello [MobileAppController] 특성을 사용 하 여 모바일 전용 API 컨트롤러를 등록할 수 있습니다. hello `MobileAppController` 특성 hello 경로 등록 hello 모바일 앱 JSON serializer를 설정 하 고 설정 [클라이언트 버전을 확인](app-service-mobile-client-and-server-versioning.md)합니다.

1. Visual Studio를 마우스 오른쪽 단추로 클릭 안녕하세요 Controllers 폴더를 클릭 한 다음 **추가** > **컨트롤러**선택, **Web API 2 컨트롤러&mdash;빈** 및 클릭 **추가**합니다.
2. `CustomController`와 같은 **컨트롤러 이름**을 제공하고 **추가**를 클릭합니다.
3. Hello 새 컨트롤러 클래스 파일에서 추가 hello 다음 문을 사용 하 여:

        using Microsoft.Azure.Mobile.Server.Config;
4. Hello 적용 **[MobileAppController]** hello 다음 예제와 같이 toohello API 컨트롤러 클래스 정의 특성:

        [MobileAppController]
        public class CustomController : ApiController
        {
              //...
        }
5. App_Start/Startup.MobileApp.cs 파일에서 추가 호출 toohello **MapApiControllers** hello 다음 예제와 같이 확장 메서드를:

        new MobileAppConfiguration()
            .MapApiControllers()
            .ApplyTo(config);

Hello를 사용할 수도 있습니다 `UseDefaultConfiguration()` 확장 메서드 대신 `MapApiControllers()`합니다. **MobileAppControllerAttribute** 가 적용되지 않는 모든 컨트롤러는 클라이언트에서 여전히 액세스할 수 있지만 모든 모바일 앱 클라이언트 SDK로 올바르게 사용되지 않을 수 있습니다.

## <a name="how-to-work-with-authentication"></a>방법: 인증으로 작업
앱 서비스 인증을 사용 하 여 azure 모바일 앱 / 권한 부여 toosecure 모바일 백 엔드 합니다.  이 섹션에서는 tooperform hello.NET 백 엔드 서버 프로젝트의 인증 관련 작업을 수행 합니다.

* [방법: 인증 tooa 서버 프로젝트를 추가 합니다.](#add-auth)
* [방법: 응용 프로그램에 사용자 지정 인증 사용](#custom-auth)
* [방법: 인증된 사용자 정보 검색](#user-info)
* [방법: 인증된 사용자에 대한 데이터 액세스 제한](#authorize)

### <a name="add-auth"></a>방법: 인증 tooa 서버 프로젝트를 추가 합니다.
Hello를 확장 하 여 인증 tooyour 서버 프로젝트를 추가할 수 있습니다 **MobileAppConfiguration** 개체 및 OWIN 미들웨어를 구성 합니다. Hello를 설치 하는 경우 [Microsoft.Azure.Mobile.Server.Quickstart] 패키지 및 호출 hello **UseDefaultConfiguration** 확장 메서드를 toostep 3을 건너뛸 수 있습니다.

1. Visual Studio에서 설치 hello [Microsoft.Azure.Mobile.Server.Authentication] 패키지 합니다.
2. Hello Startup.cs 프로젝트 파일에서 다음 hello hello 시작 시 코드 줄을 hello 추가 **구성** 메서드:

        app.UseAppServiceAuthentication(config);

    이 OWIN 미들웨어 구성 요소 관련 hello 앱 서비스 게이트웨이에서 발급 한 토큰의 유효성을 검사 합니다.
3. Hello 추가 `[Authorize]` 특성 tooany 컨트롤러 또는 인증을 요구 하는 메서드.

방법에 대 한 toolearn tooauthenticate 클라이언트 tooyour 모바일 앱 백 엔드 참조 [추가 인증 tooyour 앱](app-service-mobile-ios-get-started-users.md)합니다.

### <a name="custom-auth"></a>방법: 응용 프로그램에 사용자 지정 인증 사용
Toouse hello 응용 프로그램 서비스 인증/권한 부여 공급자 중 하나를 싶지 않은 경우 로그인 하는 시스템을 구현할 수 있습니다. Hello 설치 [Microsoft.Azure.Mobile.Server.Login] tooassist 인증 토큰 생성 된 패키지입니다.  사용자 자격 증명의 유효성 검사를 위한 고유 코드를 제공합니다. 예를 들어 데이터베이스의 솔트되고 해시된 암호를 기준으로 검사할 수 있습니다. Hello 아래의 예제에서는 hello `isValidAssertion()` 메서드 (다른 곳에서 정의 됨)는 이러한 검사 합니다.

사용자 지정 인증 hello는 ApiController 만들고 노출 하 여 노출 됩니다 `register` 및 `login` 동작 합니다. hello 클라이언트 hello 사용자 로부터 사용자 지정 UI toocollect hello 정보를 사용 해야 합니다.  hello 정보가 다음 표준 HTTP POST로 제출 된 toohello API 호출 되었습니다. Hello를 사용 하 여 토큰이 발급 될 hello 서버 hello 어설션에 유효성 검사, 일단 `AppServiceLoginHandler.CreateToken()` 메서드.  hello ApiController **하지 않아야** hello를 사용 하 여 `[MobileAppController]` 특성입니다.

예제 `login` 작업:

        public IHttpActionResult Post([FromBody] JObject assertion)
        {
            if (isValidAssertion(assertion)) // user-defined function, checks against a database
            {
                JwtSecurityToken token = AppServiceLoginHandler.CreateToken(new Claim[] { new Claim(JwtRegisteredClaimNames.Sub, assertion["username"]) },
                    mySigningKey,
                    myAppURL,
                    myAppURL,
                    TimeSpan.FromHours(24) );
                return Ok(new LoginResult()
                {
                    AuthenticationToken = token.RawData,
                    User = new LoginResultUser() { UserId = userName.ToString() }
                });
            }
            else // user assertion was not valid
            {
                return this.Request.CreateUnauthorizedResponse();
            }
        }

앞 예제는 hello, LoginResult 및 LoginResultUser은 필수 속성을 노출 하는 직렬화 가능 개체입니다. hello 클라이언트에서 로그인 응답 toobe hello 폼의 JSON 개체로 반환 합니다.

        {
            "authenticationToken": "<token>",
            "user": {
                "userId": "<userId>"
            }
        }

hello `AppServiceLoginHandler.CreateToken()` 메서드를 포함 한 *대상 그룹* 및 *발급자* 매개 변수입니다. 이러한 매개 변수를 모두 hello HTTPS 체계를 사용 하 여 응용 프로그램 루트의 toohello URL 설정 됩니다. 마찬가지로 설정 해야 *secretKey* 응용 프로그램의 toobe hello 값의 키를 서명 합니다. Hello를 사용 하는 toomint 키 수 있으며 사용자를 가장할 때 서명 클라이언트에서 키를 배포 하지 마십시오. Hello 서명 hello를 참조 하 여 응용 프로그램 서비스에서 호스트 하는 동안 키를 가져올 수 있습니다 *웹 사이트\_AUTH\_서명\_키* 환경 변수입니다. 로컬 디버깅 컨텍스트에서 필요한 경우 hello 지침 hello에 따라 [인증을 사용 하 여 로컬 디버깅](#local-debug) tooretrieve hello 키 섹션 및 응용 프로그램 설정으로 저장 합니다.

hello 발급 된 토큰 다른 클레임 및 만료 날짜를 포함할 수도 있습니다.  최소한, hello 발급 된 토큰 주제를 포함 해야 합니다 (**sub**) 클레임입니다.

Hello 표준 클라이언트를 지원할 수 있습니다 `loginAsync()` hello 인증 경로 오버 로드 하 여 메서드.  클라이언트 hello 호출 하는 경우 `client.loginAsync('custom');` 에 toolog, 프로그램 경로가 있어야 `/.auth/login/custom`합니다.  사용 하 여 hello 사용자 지정 인증 컨트롤러에 대 한 hello 경로 설정할 수 있습니다 `MapHttpRoute()`:

    config.Routes.MapHttpRoute("custom", ".auth/login/custom", new { controller = "CustomAuth" });

> [!TIP]
> Hello를 사용 하 여 `loginAsync()` 방식이 사용 되므로 해당 hello 인증 토큰이 연결 된 tooevery 후속 호출 toohello 서비스입니다.
>
>

### <a name="user-info"></a>방법: 인증된 사용자 정보 검색
사용자가 앱 서비스에 의해 인증, 사용자 ID 및 기타 정보.NET 백 엔드 코드를 할당 하는 hello를 액세스할 수 있습니다. hello 사용자 정보 hello 백 엔드에 대 한 권한 부여 결정에 사용할 수 있습니다. hello 다음 코드 가져오는 hello 사용자 ID를 요청과 연결 된 같습니다.

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

hello SID hello 공급자 특정 사용자 ID에서 파생 되 고 지정 된 사용자와 로그인 공급자에 대 한 정적이 합니다.  hello SID 잘못 된 인증 토큰에 대 한 null입니다.

또한 앱 서비스는 로그인 공급자에서 특정 클레임을 요청할 수 있습니다. 각 ID 공급자는 ID 공급자 SDK를 사용하여 자세한 정보를 제공할 수 있습니다.  예를 들어 친구 정보에 대 한 hello Facebook Graph API를 사용할 수 있습니다.  Hello 공급자 블레이드에서 hello Azure 포털에서에서 요청 된 클레임을 지정할 수 있습니다. 일부 클레임 hello id 공급자와 추가 구성이 필요합니다.

hello 다음 호출 hello 코드 **GetAppServiceIdentityAsync** 확장 메서드 tooget hello 로그인 자격 증명을 hello Facebook Graph API에 대 한 hello 액세스 토큰 필요한 toomake 요청 포함:

    // Get hello credentials for hello logged-in user.
    var credentials =
        await this.User
        .GetAppServiceIdentityAsync<FacebookCredentials>(this.Request);

    if (credentials.Provider == "Facebook")
    {
        // Create a query string with hello Facebook access token.
        var fbRequestUrl = "https://graph.facebook.com/me/feed?access_token="
            + credentials.AccessToken;

        // Create an HttpClient request.
        var client = new System.Net.Http.HttpClient();

        // Request hello current user info from Facebook.
        var resp = await client.GetAsync(fbRequestUrl);
        resp.EnsureSuccessStatusCode();

        // Do something here with hello Facebook user information.
        var fbInfo = await resp.Content.ReadAsStringAsync();
    }

사용 하 여 추가 대해 문을 `System.Security.Principal` tooprovide hello **GetAppServiceIdentityAsync** 확장 메서드.

### <a name="authorize"></a>방법: 인증된 사용자에 대한 데이터 액세스 제한
Hello 이전 단원의 tooretrieve 인증된 된 사용자의 사용자 ID를 hello 하는 방법을 배웠습니다. 액세스 toodata 및이 값에 따라 기타 리소스를 제한할 수 있습니다. 예를 들어 사용자 Id 열 tootables를 추가 하 고 hello hello 사용자 ID 기준으로 쿼리 결과 필터링 tooauthorized 사용자만 데이터를 반환 하는 간단한 방법을 toolimit입니다. hello 다음 코드 행을 반환 데이터 hello SID hello UserId hello TodoItem 테이블의 열 값과 일치 하는 경우에:

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

    // Only return data rows that belong toohello current user.
    return Query().Where(t => t.UserId == sid);

hello `Query()` 메서드가 반환 되는 `IQueryable` LINQ toohandle 필터링 하 여 조작할 수 있습니다.

## <a name="how-to-add-push-notifications-tooa-server-project"></a>방법: 푸시 알림을 tooa 서버 프로젝트를 추가 합니다.
Hello를 확장 하 여 푸시 알림 tooyour 서버 프로젝트를 추가 **MobileAppConfiguration** 개체와 알림 허브 클라이언트 만들기.

1. Visual Studio에서 hello 서버 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **NuGet 패키지 관리**, 검색할 `Microsoft.Azure.Mobile.Server.Notifications`, 클릭 **설치**합니다.
2. 이 단계 tooinstall hello 반복 `Microsoft.Azure.NotificationHubs` hello 알림 허브 클라이언트 라이브러리를 포함 하는 패키지입니다.
3. App_Start/Startup.MobileApp.cs에 추가 호출 toohello **AddPushNotifications()** 초기화 하는 동안 확장 메서드:

        new MobileAppConfiguration()
            // other features...
            .AddPushNotifications()
            .ApplyTo(config);
4. 알림 허브 클라이언트를 만드는 코드를 다음 hello를 추가 합니다.

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            config.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

이제 hello 알림 허브 클라이언트 toosend 푸시 알림을 tooregistered 장치를 사용할 수 있습니다. 자세한 내용은 참조 [추가 푸시 알림 tooyour 앱](app-service-mobile-ios-get-started-push.md)합니다. 알림 허브에 대해 자세히 toolearn 참조 [알림 허브 개요](../notification-hubs/notification-hubs-push-notification-overview.md)합니다.

## <a name="tags"></a>방법: 태그를 사용하여 대상 지정 푸시 활성화
알림 허브를 사용 하면 대상으로 지정 된 알림을 toospecific 등록 태그를 사용 하 여 보낼 수 있습니다. 여러 태그가 자동으로 만들어집니다.

* hello 설치 ID는 특정 장치를 식별합니다.
* hello 사용자 Id에 따라 인증 hello SID 특정 사용자를 식별 합니다.

ID는 hello에서 액세스할 수 있습니다 설치 hello **installationId** hello 속성 **MobileServiceClient**합니다.  hello 다음 예제에서는 설치 ID tooadd를 사용 하는 방법을 태그 tooa 특정 설치를 알림 허브에서:

    hub.PatchInstallation("my-installation-id", new[]
    {
        new PartialUpdateOperation
        {
            Operation = UpdateOperationType.Add,
            Path = "/tags",
            Value = "{my-tag}"
        }
    });

푸시 알림 등록 하는 동안 hello 클라이언트에서 제공 하는 태그는 hello 설치를 만들 때 hello 백 엔드에서 무시 됩니다. 클라이언트 tooadd tooenable 태그 toohello 설치, 패턴 앞 hello를 사용 하 여 태그를 추가 하는 사용자 지정 API를 만들어야 합니다.

참조 [클라이언트 추가 푸시 알림 태그] [ 5] 예제를 보려면 hello 앱 서비스 모바일 앱 완료 된 quickstart 샘플에 있습니다.

## <a name="push-user"></a>방법: 사용자를 인증 하는 송신 푸시 알림을 tooan
인증된 된 사용자 푸시 알림에 등록, 사용자 ID 태그 toohello 등록 자동으로 추가 됩니다. 이 태그를 사용 하 여 푸시 알림 tooall 장치가 해당 사용자가 등록 되어 보낼 수 있습니다. hello 다음 코드 hello 요청을 만드는 사용자의 SID 가져오고 해당 사용자에 대 한 템플릿 푸시 알림 tooevery 장치 등록을 보냅니다.

    // Get hello current user SID and create a tag for hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;
    string userTag = "_UserId:" + sid;

    // Build a dictionary for hello template with hello item message text.
    var notification = new Dictionary<string, string> { { "message", item.Text } };

    // Send a template notification toohello user ID.
    await hub.SendTemplateNotificationAsync(notification, userTag);

인증된 클라이언트의 푸시 알림을 등록할 때 등록을 시도하기 전에 인증이 완료되었는지 확인합니다. 자세한 내용은 참조 [toousers 푸시] [ 6] .NET 백 엔드에 대 한 hello 앱 서비스 모바일 앱 완료 된 quickstart 샘플에 있습니다.

## <a name="how-to-debug-and-troubleshoot-hello-net-server-sdk"></a>방법: 디버그 및.NET 서버 SDK hello 문제 해결
Azure 앱 서비스는 ASP.NET 응용 프로그램에 대한 여러 디버깅 및 문제 해결 기술을 제공합니다.

* [Azure 앱 서비스 모니터링](../app-service-web/web-sites-monitor.md)
* [Azure 앱 서비스에 진단 로그 사용](../app-service-web/web-sites-enable-diagnostic-log.md)
* [Visual Studio에서 Azure 앱 서비스 문제 해결](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)

### <a name="logging"></a>로깅
Hello 표준 ASP.NET 추적 쓰기를 사용 하 여 tooApp 서비스 진단 로그를 작성할 수 있습니다. Toohello 로그를 작성 하려면 먼저 모바일 앱 백엔드에 진단을 활성화 해야 합니다.

tooenable 진단 및 쓰기 toohello 로그:

1. Hello 단계에 따라 [어떻게 tooenable 진단](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag)합니다.
2. Hello 다음 추가 문을 사용 하 여 코드 파일에:

        using System.Web.Http.Tracing;
3. 추적 기록기 toowrite를 hello.NET 백 엔드 toohello 진단 로그에서 다음과 같이 만듭니다.

        ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
        traceWriter.Info("Hello, World");
4. 서버 프로젝트를 다시 게시 하 고 hello 모바일 앱 백 엔드 tooexecute hello 코드 경로 hello 로깅 사용 하 여 액세스 키를 누릅니다.
5. 다운로드 하 고에 설명 된 대로 hello 로그 평가 [하는 방법: 로그를 다운로드](../app-service-web/web-sites-enable-diagnostic-log.md#download)합니다.

### <a name="local-debug"></a>인증을 사용하여 로컬 디버깅
응용 프로그램을 실행할 수 tootest toohello 클라우드 가격표를 게시 하기 전에 변경 되는 로컬입니다. 대부분의 Azure Mobile Apps 백 엔드의 경우 Visual Studio에 있는 동안 *F5* 를 누릅니다. 그러나 인증을 사용할 때 몇 가지 추가 고려 사항이 있습니다.

클라우드 기반 모바일 앱으로 응용 프로그램 서비스 인증/권한 부여 구성 되어 있어야 하 고 클라이언트 hello 대체 로그인 호스트로 지정 하는 hello 클라우드 끝점 있어야 합니다. 필요한 hello 특별 한 단계에 대 한 클라이언트 플랫폼에 대 한 hello 설명서를 참조 하십시오.

모바일 백 엔드에 [Microsoft.Azure.Mobile.Server.Authentication] 을 설치했는지 확인합니다. 그런 다음 응용 프로그램의 OWIN 시작 클래스에서 후 hello 다음 추가 `MobileAppConfiguration` 적용된 tooyour 되었습니다 `HttpConfiguration`:

        app.UseAppServiceAuthentication(new AppServiceAuthenticationOptions()
        {
            SigningKey = ConfigurationManager.AppSettings["authSigningKey"],
            ValidAudiences = new[] { ConfigurationManager.AppSettings["authAudience"] },
            ValidIssuers = new[] { ConfigurationManager.AppSettings["authIssuer"] },
            TokenHandler = config.GetAppServiceTokenHandler()
        });

앞 예제는 hello, hello를 구성 해야 *authAudience* 및 *authIssuer* Web.config 내에서 응용 프로그램 설정 파일 tooeach hello HTTPS를 사용 하 여 응용 프로그램 루트의 url 체계입니다. 마찬가지로 설정 해야 *authSigningKey* 응용 프로그램의 toobe hello 값의 키를 서명 합니다.
tooobtain hello 서명 키:

1. Hello 내에서 tooyour 앱 이동 [Azure 포털]
2. **도구**, **Kudu**, **이동**을 클릭합니다.
3. Hello Kudu 관리 사이트에서 클릭 **환경**합니다.
4. 에 대 한 hello 식일 *웹 사이트\_AUTH\_서명\_키*합니다.

서명 키 hello 사용 하 여 hello *authSigningKey* 로컬 응용 프로그램 config에 매개 변수입니다.  모바일 백 엔드는 이제 장착된 toovalidate 토큰을 로컬로 실행 하는 경우 hello 클라이언트 hello 클라우드 기반 끝점에서 hello 토큰을 가져옵니다.

[1]: https://msdn.microsoft.com/library/azure/dn961176.aspx
[2]: https://github.com/Azure/azure-mobile-apps-net-server
[3]: app-service-mobile-ios-get-started.md
[4]: https://azure.microsoft.com/downloads/
[5]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#client-added-push-notification-tags
[6]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#push-to-users
[Azure 포털]: https://portal.azure.com
[NuGet.org]: http://www.nuget.org/
[Microsoft.Azure.Mobile.Server]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/
[Microsoft.Azure.Mobile.Server.Quickstart]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Quickstart/
[Microsoft.Azure.Mobile.Server.Authentication]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/
[Microsoft.Azure.Mobile.Server.Login]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Login/
[Microsoft.Azure.Mobile.Server.Notifications]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Notifications/
[MapHttpAttributeRoutes]: https://msdn.microsoft.com/library/dn479134(v=vs.118).aspx
