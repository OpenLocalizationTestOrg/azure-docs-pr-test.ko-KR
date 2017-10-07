---
title: "모바일 서비스 tooAzure 앱 서비스에서 aaaUpgrade"
description: "Tooeasily 모바일 서비스 응용 프로그램 tooan 앱 서비스 모바일 앱을 업그레이드 하는 방법에 대해 알아봅니다"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 9c0ac353-afb6-462b-ab94-d91b8247322f
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2b75a1b824e8ef0d36c9053f2f19af051479f928
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-existing-net-azure-mobile-service-tooapp-service"></a>프로그램 기존.NET Azure 모바일 서비스 tooApp 서비스 업그레이드
앱 서비스 모바일을 새로운 방식으로 toobuild 모바일 응용 프로그램 Microsoft Azure를 사용 하 여입니다. toolearn 더 참조 [모바일 앱 이란?]합니다.

이 항목에서는 설명 방법을 tooupgrade tooa Azure 모바일 서비스에서에서 기존.NET 백 엔드 응용 프로그램이 새 앱 서비스 모바일 앱. 이 업그레이드를 수행 하는 동안 기존 모바일 서비스 응용 프로그램 toooperate를 계속 수 있습니다.   Tooupgrade Node.js 백 엔드 응용 프로그램, 필요한 경우 너무 참조[Node.js 모바일 서비스를 업그레이드](app-service-mobile-node-backend-upgrading-from-mobile-services.md)합니다.

너무에 따라 청구 되며 앱 서비스 기능 액세스 tooall 모바일 백 엔드 응용 프로그램 서비스 업그레이드 tooAzure 인 경우에[앱 서비스 가격 책정], 모바일 서비스 가격 되지 않습니다.

## <a name="migrate-vs-upgrade"></a>마이그레이션과 업그레이드 비교
[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

> [!TIP]
> 업그레이드를 진행하기 전에 [마이그레이션을 수행](app-service-mobile-migrating-from-mobile-services.md) 하는 것이 좋습니다. 이러한 방식으로 응용 프로그램의 두 버전 모두 넣을 수 있습니다에 동일한 앱 서비스 계획 hello 및 추가 비용 없이 발생 합니다.
>
>

### <a name="improvements-in-mobile-apps-net-server-sdk"></a>모바일 앱 .NET 서버 SDK에서 향상된 기능
새 toohello 업그레이드 [모바일 앱 SDK](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) hello 다음 이점을 제공 합니다.

* NuGet 종속성에서 유연성이 증가합니다. 호스팅 환경에 더 이상 hello 호환 되는 대체 버전을 사용할 수 있도록 고유한 버전의 NuGet 패키지를 제공 합니다. 그러나 중요 한 새 bugfixes 또는 보안 업데이트 toohello 모바일 서버 SDK 또는 종속성 경우에 서비스에 수동으로 업데이트 해야 합니다.
* 보다 융통성 있게 hello 모바일 SDK입니다. 기능을 명시적으로 제어할 수 있습니다 및 경로 설정, 인증, Api, 테이블 및 푸시 등록 끝점 hello 합니다. toolearn 더 참조 [어떻게 Azure 모바일 앱 용.NET 서버 SDK hello를 toouse](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)합니다.
* 다른 ASP.NET 프로젝트 형식 및 경로를 지원합니다. 이제 모바일 백 엔드 프로젝트와 동일한 프로젝트 hello에 MVC 및 Web API 컨트롤러를 호스트할 수 있습니다.
* 웹 및 모바일 앱에서 일반적인 인증 구성을 toouse 수 있게 해 주는 새 앱 서비스 인증 기능에 대 한 지원.

## <a name="overview"></a>기본 업그레이드 개요
대부분의 경우에서 업그레이드는 처럼 간단할 toohello 새 모바일 앱 서버 SDK를 전환 하 고 새 모바일 앱 인스턴스로 코드를 다시 게시 합니다. 그러나 고급 인증 시나리오 및 예약된 작업 사용과 같이 추가 구성이 필요한 일부 시나리오도 있습니다. 이러한 각 hello에 대해서는 나중에 섹션.

> [!TIP]
> 읽기 및 업그레이드를 시작 하기 전에이 항목의 나머지 부분 hello를 완전히 이해 하는 것이 좋습니다. 아래 설명선에 표시된 사용하는 기능을 모두 기록해 두세요.
>
>

hello 모바일 서비스 클라이언트 Sdk는 **하지** hello 새로운 모바일 앱 서버 SDK와 호환 됩니다. 앱에 대 한 서비스, 순서 tooprovide 지속적인 하지 변경 tooa 사이트에서는 현재 게시 된 클라이언트를 게시 해야 합니다. 대신 중복으로 제공한 새 모바일 앱을 만들어야 합니다. 이 응용 프로그램을 넣을 수 hello에서 동일한 앱 서비스 계획 tooavoid 재무 추가 비용 발생 합니다.

다음 두 가지 버전 hello 응용 프로그램의: 하나는 유지 되며 동일 hello 및 새 클라이언트 릴리스로 업그레이드할 때는 다른 및 대상 hello 와일드 카드, 및 hello에 게시 된 앱을 사용 합니다. 이동 하 고, 속도로 코드를 테스트할 수 있지만 그러면 만들면 버그 수정 사항이 적용 된 tooboth을 가져올 확인 해야 합니다. 원하는 수의 hello 와일드 카드에 클라이언트 앱 toohello 최신 버전 업데이트, 원하는 경우 hello 원래 마이그레이션된 응용 프로그램을 삭제할 수 있습니다 수 있다고 생각 되 면 합니다.

hello hello 업그레이드 프로세스에 대 한 전체 개요는 다음과 같습니다.

1. 새 모바일 앱 만들기
2. 업데이트 hello 프로젝트 toouse hello 새로운 서버 Sdk
3. 새 버전의 클라이언트 응용 프로그램 릴리스
4. (선택 사항) 원래 마이그레이션된 인스턴스 삭제

## <a name="mobile-app-version"></a>두 번째 응용 프로그램 인스턴스 만들기
hello 업그레이드할 때의 첫 번째 단계는 hello 새 버전의 응용 프로그램을 호스팅하려는 toocreate hello 모바일 응용 프로그램 리소스. 기존 모바일 서비스를 이미 마이그레이션한 경우 좋습니다 toocreate hello이이 버전과 동일한 호스팅 계획 합니다. 열기 hello [Azure 포털] tooyour 탐색 및 응용 프로그램 마이그레이션. 앱 서비스 계획에서 실행 되는 hello를 기록해 둡니다.

다음으로, 다음 hello hello 두 번째 응용 프로그램 인스턴스를 만들 [.NET 백 엔드 만들기 지침](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app)합니다. 때 선택 하면 앱 서비스 계획 또는 "계획 호스팅" 증명된 tooselect hello 마이그레이션된 응용 프로그램의 계획 합니다.

Toouse hello 동일한 데이터베이스와 알림 허브와 모바일 서비스에서 수행한 설정할 수 있습니다. 열어 이러한 값을 복사할 수는 있지만 [Azure 포털] toohello 원래 응용 프로그램 탐색을 클릭 하 고 **설정** > **응용 프로그램 설정**합니다. **연결 문자열**에서 `MS_NotificationHubConnectionString` 및 `MS_TableConnectionString`을 복사합니다. 새 업그레이드 사이트 tooyour 이동한 모든 기존 값 덮어쓰기에 붙여 넣습니다. 앱에 필요한 다른 응용 프로그램 설정에 이 프로세스를 반복합니다. 연결 문자열 및 응용 프로그램 설정을 hello에서 읽을 수는 마이그레이션된 서비스를 사용 하지 **구성** hello hello의 모바일 서비스 섹션의 탭 [Azure 클래식 포털]합니다.

응용 프로그램에 대 한 hello ASP.NET 프로젝트의 복사본을 만들고 tooyour 새 사이트를 게시 합니다. Hello 새 URL로 업데이트 하는 클라이언트 응용 프로그램의 복사본을 사용 하 여 예상 대로 작동 하는 것을 확인 합니다.

## <a name="updating-hello-server-project"></a>Hello 서버 프로젝트를 업데이트합니다.
모바일 앱 제공 새 [모바일 앱 서버 SDK] hello 많이 제공 하는 모바일 서비스 런타임 hello와 동일한 기능을 합니다. 첫째, 모든 참조 toohello 모바일 서비스 패키지를 제거 해야 합니다. Hello NuGet 패키지 관리자에서 검색 `WindowsAzure.MobileServices.Backend`합니다. 대부분의 앱에서 `WindowsAzure.MobileServices.Backend.Tables` 및 `WindowsAzure.MobileServices.Backend.Entity`를 포함하여 여러 패키지가 나타납니다. 이 경우 시작 hello 종속성 트리에서 hello 가장 낮은 패키지와 같은 `Entity`, 하 고 제거 합니다. 메시지가 표시되면 모든 종속 패키지를 제거하지 마십시오. `WindowsAzure.MobileServices.Backend` 자체를 제거할 때까지 이 프로세스를 반복합니다.

이 시점에서 더 이상 모바일 서비스 SDK를 참조하지 않는 프로젝트가 있습니다.

다음 참조 hello 모바일 앱 SDK를 추가 합니다. 이 업그레이드에 대 한 대부분의 개발자는 toodownload 원하고 hello 설치 `Microsoft.Azure.Mobile.Server.Quickstart` hello 전체 필요한 집합에서 끌어오고이으로 패키지 합니다.

Hello Sdk 간의 차이로 인해 발생 한 몇몇 컴파일러 오류가 이지만 hello이이 단원의 나머지 부분에 대해서는 설명를 쉽게 tooaddress 포함 됩니다.

### <a name="base-configuration"></a>기본 구성
그런 다음 WebApiConfig.cs에서

        // Use this class tooset configuration options for your mobile service
        ConfigOptions options = new ConfigOptions();

        // Use this class tooset WebAPI configuration options
        HttpConfiguration config = ServiceConfig.Initialize(new ConfigBuilder(options));

다음으로 바꿀 수 있습니다.

        HttpConfiguration config = new HttpConfiguration();
        new MobileAppConfiguration()
            .UseDefaultConfiguration()
        .ApplyTo(config);

> [!NOTE]
> 원할 경우 toolearn hello 새.NET 서버 SDK 및 앱에서 기능이 tooadd/제거 하는 방법에 대 한 hello를 참조 하십시오 [어떻게 toouse hello.NET 서버 SDK] 항목입니다.
>
>

응용 프로그램 정하는 경우 hello 인증 기능을 사용, tooregister OWIN 미들웨어 필요 합니다. 이 경우 새 OWIN 시작 클래스로 구성 코드 위의 hello를 이동 해야 합니다.

1. Hello NuGet 패키지 추가 `Microsoft.Owin.Host.SystemWeb` 프로젝트에 아직 포함 되지 않은 경우.
2. Visual Studio에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** -> **새 항목**을 선택합니다. **웹** -> **일반** -> **OWIN 시작 클래스**를 선택합니다.
3. MobileAppConfiguration에 대 한 코드 위의 hello 이동 `WebApiConfig.Register()` toohello `Configuration()` 새 시작 클래스의 메서드로 합니다.

있는지 hello 확인 `Configuration()` 메서드로 끝납니다.

        app.UseWebApi(config)
        app.UseAppServiceAuthentication(config);

아래의 hello full 인증 섹션에서 다루는 관련된 tooauthentication 추가 변경 내용이 있습니다.

### <a name="working-with-data"></a>데이터 작업
모바일 서비스에서 hello 모바일 응용 프로그램 이름 hello Entity Framework 설치 프로그램에서 hello 기본 스키마 이름으로 제공 됩니다.

동일 해야 하는 tooensure hello 참조 스키마 되 고 이전 처럼 응용 프로그램에 대 한 hello DbContext에서에서 tooset hello 스키마를 따르는 사용 하 여 hello:

        string schema = System.Configuration.ConfigurationManager.AppSettings.Get("MS_MobileServiceName");

MS_MobileServiceName 위에 hello 수행 하는 경우에 설정 되어 있는지 확인 하십시오. 또한 응용 프로그램이 이전에 사용자 지정한 경우 다른 스키마 이름을 제공할 수 있습니다.

### <a name="system-properties"></a>시스템 속성
#### <a name="naming"></a>이름 지정
Hello Azure 모바일 서비스 서버 SDK, 시스템 속성에에서 항상 포함 되는 두 개의 밑줄이 (`__`) hello 속성에 대 한 접두사:

* __createdAt
* __updatedAt
* __deleted
* __version

hello 모바일 서비스 클라이언트 Sdk가이 형식의 시스템 속성을 구문 분석 하기 위한 특수 논리가 합니다.

시스템 속성 Azure 모바일 앱에는 특수 한 서식을 지정 하 고 있는 hello 이름 다음에 더 이상:

* createdAt
* updatedAt
* deleted
* 버전

hello 모바일 앱 클라이언트 Sdk 사용 하 여 hello 새 시스템 속성 이름은 변경 되지 않으므로 tooclient 코드가 필요 합니다. 그러나 직접 있다면 tooyour 서비스를 호출한 REST을 만드는 다음 쿼리를 적절 하 게 변경 해야 합니다.

#### <a name="local-store"></a>로컬 저장소
시스템 속성 변경 내용을 toohello 이름을 hello 의미 모바일 서비스에 대 한 오프 라인 동기화 로컬 데이터베이스는 모바일 앱와 호환 되지 않습니다. 가능 하면 모바일 서비스 tooMobile 보류 중인 변경 내용이 후까지 앱 보냈습니다 toohello 서버에서에서 클라이언트 응용 프로그램을 업그레이드 하지 마십시오. 그런 다음 hello 업그레이드 된 응용 프로그램에는 새 데이터베이스 파일 이름을 사용 해야 합니다.

Hello 작업 큐에 오프 라인 변경 내용이 보류 중인 동안 tooMobile 모바일 서비스 응용 프로그램에서에서 업그레이드 되는 클라이언트 응용 프로그램 hello 시스템 데이터베이스에서 업데이트 된 toouse hello 새 열 이름 이어야 합니다. Ios, 이렇게 간단한 마이그레이션을 toochange hello 열 이름을 사용 하 여 합니다. Android 및 hello.NET 관리 되는 클라이언트에 데이터 개체 테이블에 대 한 사용자 지정 SQL toorename에 hello 열 작성 해야 합니다.

Ios, 사용자 데이터 엔터티 toomatch hello 다음에 대 한 핵심 데이터 스키마를 변경 해야 합니다. 속성을 hello 참고 `createdAt`, `updatedAt` 및 `version` 더 이상는 `ms_` 접두사:

| 특성 | 유형 | 참고 |
| --- | --- | --- |
| id |문자열, 필수로 표시 |원격 저장소의 기본 키 |
| createdAt |Date |(선택 사항) 지도 toocreatedAt 시스템 속성 |
| updatedAt |Date |(선택 사항) 지도 tooupdatedAt 시스템 속성 |
| 버전 |문자열 |(선택 사항) 사용 하는 toodetect 충돌, 지도 tooversion |

#### <a name="querying-system-properties"></a>시스템 속성 쿼리
Azure 모바일 서비스에서 시스템 속성은 전송 되지 기본적으로 하지만 쿼리 문자열 hello를 사용 하 여 요청 된 경우에 `__systemProperties`합니다. Azure 모바일 앱 시스템 속성은 한 반면 **항상 선택** 속하므로 hello 서버 SDK 개체 모델입니다.

이 변경 사항은 `MappedEntityDomainManager`의 확장과 같은 도메인 관리자의 사용자 지정 구현에 주로 영향을 줍니다. 모바일 서비스에서 클라이언트는 하지 모든 시스템 속성을 요청할 경우 가능한 toouse는 `MappedEntityDomainManager` 모든 속성이 실제로 매핑되지 않는 합니다. 그러나 Azure 모바일 앱에서 이러한 매핑되지 않은 속성은 가져오기 쿼리에서 오류를 발생시킵니다.

가장 쉬운 방법은 tooresolve hello 문제 hello에서 상속 되도록 toomodify 프로그램 Dto는 `ITableData` 대신 `EntityData`합니다. 그런 다음 추가 hello `[NotMapped]` 생략 해야 toohello 필드 특성입니다.

예를 들어 hello 다음 정의 `TodoItem` 시스템 속성이 없는:

    using System.ComponentModel.DataAnnotations.Schema;

    public class TodoItem : ITableData
    {
        public string Text { get; set; }

        public bool Complete { get; set; }

        public string Id { get; set; }

        [NotMapped]
        public DateTimeOffset? CreatedAt { get; set; }

        [NotMapped]
        public DateTimeOffset? UpdatedAt { get; set; }

        [NotMapped]
        public bool Deleted { get; set; }

        [NotMapped]
        public byte[] Version { get; set; }
    }

참고:에 오류가 발생 하는 경우 `NotMapped`, 참조 toohello 어셈블리 추가 `System.ComponentModel.DataAnnotations`합니다.

### <a name="cors"></a>CORS
모바일 서비스에는 ASP.NET CORS 솔루션 hello를 래핑하여 CORS에 대 한 지원이 포함 되어 있습니다. 이 배치 계층은 되었으므로 제거 toogive hello 개발자 자세히 제어할 직접 활용할 수 있습니다 [ASP.NET CORS 지원](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api)합니다.

hello 주 관련 CORS를 사용 하는 경우 영역은 해당 hello `eTag` 및 `Location` hello 클라이언트 Sdk toowork 되려면에서 제대로 헤더를 허용 해야 합니다.

### <a name="push-notifications"></a>푸시 알림
푸시에 대 한 hello 서버 SDK에서에서 누락 될 수 있는 hello 주 항목에는 hello PushRegistrationHandler 클래스입니다. 모바일 앱에서는 등록이 약간 다르게 처리되며, 기본적으로 태그 없는 등록이 사용됩니다. 사용자 지정 API를 통해 태그를 관리할 수 있습니다. Hello를 참조 하십시오 [태그에 대 한 등록](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags) 자세한 정보에 대 한 지침입니다.

### <a name="scheduled-jobs"></a>예약된 작업
.NET 백 엔드에 있는 모든 기존 작업 toobe 개별적으로 업그레이드할 필요 하므로 예약 된 작업은 모바일 앱에 빌드되지 않습니다. 한 가지 옵션은 예약된 된 toocreate [웹 작업] hello 모바일 응용 프로그램 코드 사이트에 있습니다. 또한 작업 코드를 보유 하는 컨트롤러를 설정 하 고 hello 구성 수 [Azure 스케줄러] toohit 예상 hello 일정에 따라 해당 끝점입니다.

### <a name="miscellaneous-changes"></a>기타 변경 내용
모바일 클라이언트에서 사용 될 수 있는 모든 ApiControllers 이제 hello 있어야 `[MobileAppController]` 특성입니다. 더 이상 영향을 받지 다른 ApiControllers toogo hello 모바일 포맷터를 기본적으로 포함 됩니다.

hello `ApiServices` 개체는 더 이상 hello SDK의 일부입니다. 모바일 앱 설정 tooaccess hello 다음을 사용할 수 있습니다.

    MobileAppSettingsDictionary settings = this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

마찬가지로, 로깅 이제 현재 hello 표준 ASP.NET 추적 쓰기:

    ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
    traceWriter.Info("Hello, World");  

## <a name="authentication"></a>인증 고려 사항
이제 모바일 서비스의 인증 구성 요소 hello hello 응용 프로그램 서비스 인증/권한 부여 기능으로 이동 되었습니다. 읽는 hello 하 여 사이트에 대 한이 기능을 사용 하는 방법에 대 한 학습할 수 있는 [추가 인증 tooyour 모바일 앱](app-service-mobile-ios-get-started-users.md) 항목입니다.

AAD, Facebook, Google, 등의 일부 공급자에 대 한 복사 응용 프로그램에서 수 tooleverage hello 기존 등록 해야 합니다. 단순히 toonavigate toohello id 공급자의 포털 필요 하 고 새 리디렉션 URL toohello 등록을 추가 합니다. Hello 클라이언트 ID와 암호가 있는 응용 프로그램 서비스 인증/권한 부여를 구성 합니다.

### <a name="controller-action-authorization"></a>컨트롤러 작업 권한 부여
Hello의 인스턴스를 모두 `[AuthorizeLevel(AuthorizationLevel.User)]` 특성에서 변경 된 toouse 이제 해야 표준 ASP.NET hello `[Authorize]` 특성입니다. 또한 컨트롤러는 다른 ASP.NET 응용 프로그램에서와 같이 이제 기본적으로 익명입니다.
Hello 중 하나를 사용 하 던 관리자 또는 응용 프로그램 등의 다른 AuthorizeLevel 옵션 걸어 이러한 사라지게 됩니다. 대신 공유 암호에 대 한 AuthorizationFilters를 설정 하거나 AAD 서비스 사용자 tooenable 서비스 간 호출을 안전 하 게 구성할 수 있습니다.

### <a name="getting-additional-user-information"></a>추가 사용자 정보 가져오기
Hello 통해 액세스 토큰을 포함 하 여 추가 사용자 정보를 얻을 수 `GetAppServiceIdentityAsync()` 메서드:

        FacebookCredentials creds = await this.User.GetAppServiceIdentityAsync<FacebookCredentials>();

또한 응용 프로그램은 데이터베이스에서이 저장 하는 등 사용자 Id에 종속성을 하는 경우 반드시 모바일 서비스와 앱 서비스 모바일 앱 간 사용자 Id를 hello toonote 서로 다릅니다. 여전히 hello Mobile Services 사용자 ID를 통해 얻을 수 있습니다. Hello ProviderCredentials 하위 클래스의 모든 사용자 Id 속성을 가집니다. 따라서 하기 전에 hello 예제에서 계속 실행 합니다.

        string mobileServicesUserId = creds.Provider + ":" + creds.UserId;

앱에서 모든 종속성에 사용자 Id 사용 하는 경우 반드시 활용 가능한 경우 id 공급자와 같은 등록 hello 합니다. 사용자 Id를 사용 하는 일반적으로 범위가 지정 된 toohello 응용 프로그램 등록 되므로 새 등록 소개 사용자 tootheir 데이터 일치 하는 문제가 발생할 수 있습니다.

### <a name="custom-authentication"></a>사용자 지정 인증
앱 사용자 지정 인증 솔루션을 사용 하는 경우 해당 hello 업그레이드 된 사이트에 액세스 toohello 시스템 있는지 toomake 해야 합니다. Hello hello에 대 한 사용자 지정 인증에 대 한 새 지침에 따라 [.NET 서버 SDK 개요] toointegrate 솔루션입니다. 미리 보기에서 여전히 hello 사용자 지정 인증 구성 요소가 인지 note 하십시오.

## <a name="updating-clients"></a>클라이언트 업데이트
작동하는 모바일 앱 백 엔드가 있으면 그것을 사용하는 클라이언트 응용 프로그램의 새 버전에서 작동할 수 있습니다. 모바일 앱도 hello 클라이언트 Sdk의 새 버전을 포함 하며, 유사한 toohello 서버 업그레이드 위의 tooremove 하기 전에 toohello 모바일 서비스 Sdk를 참조 하는 모든가 필요 hello 모바일 앱 버전을 설치 합니다.

Hello 버전 간의 주요 변경 내용은 hello 중 하나는 hello 생성자에 더 이상 응용 프로그램 키 필요입니다. 이제 단순히 전달 모바일 앱의 hello URL입니다. 예를 들어 hello.NET 클라이언트를 hello `MobileServiceClient` 생성자는 이제:

        public static MobileServiceClient MobileService = new MobileServiceClient(
            "https://contoso.azurewebsites.net", // URL of hello Mobile App
        );

설치에 대 한 읽을 수 새 Sdk hello 및 hello 아래 hello 링크를 통해 새 구조를 사용 하 여:

* [iOS 버전 3.0.0 이상](app-service-mobile-ios-how-to-use-client-library.md)
* [.NET(Windows/Xamarin) 버전 2.0.0 이상](app-service-mobile-dotnet-how-to-use-client-library.md)

응용 프로그램이 경우 개의 푸시 알림을 사용 하 여, hello 각 플랫폼에 대 한 특정 등록 지침을 기록해 대로 몇 가지 변경 사항이 있는 합니다.

Hello 새 클라이언트 버전 준비을 사용 하는 경우 사용해 업그레이드 된 서버 프로젝트에 대해 합니다. 확인 한 후 작동 하는지, 새 버전의 응용 프로그램 toocustomers 놓을 수 있습니다. 결국 고객이 있는 반면 기회 tooreceive 이러한 업데이트를 일단 응용 프로그램의 hello 모바일 서비스 버전을 삭제할 수 있습니다. 앱 서비스 모바일 앱 tooan 완전히 업그레이드이 시점에서 hello 최신 모바일 앱 서버 SDK를 사용 합니다.

<!-- URLs. -->

[Azure 포털]: https://portal.azure.com/
[Azure 클래식 포털]: https://manage.windowsazure.com/
[모바일 앱 이란?]: app-service-mobile-value-prop.md
[I already use web sites and mobile services – how does App Service help me?]: /en-us/documentation/articles/app-service-mobile-value-prop-migration-from-mobile-services
[모바일 앱 서버 SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server
[Create a Mobile App]: app-service-mobile-xamarin-ios-get-started.md
[Add push notifications tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-push.md
[Add authentication tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-users.md
[Azure 스케줄러]: /en-us/documentation/services/scheduler/
[웹 작업]: ../app-service-web/websites-webjobs-resources.md
[어떻게 toouse hello.NET 서버 SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Migrate from Mobile Services tooan App Service Mobile App]: app-service-mobile-migrating-from-mobile-services.md
[Migrate your existing Mobile Service tooApp Service]: app-service-mobile-migrating-from-mobile-services.md
[앱 서비스 가격 책정]: https://azure.microsoft.com/en-us/pricing/details/app-service/
[.NET 서버 SDK 개요]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
