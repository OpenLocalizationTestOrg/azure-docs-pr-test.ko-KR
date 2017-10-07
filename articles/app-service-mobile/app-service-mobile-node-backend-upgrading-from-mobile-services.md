---
title: "모바일 서비스 tooAzure 앱 서비스-Node.js에서 aaaUpgrade"
description: "Tooeasily 모바일 서비스 응용 프로그램 tooan 앱 서비스 모바일 앱을 업그레이드 하는 방법에 대해 알아봅니다"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: yochayk
editor: 
ms.assetid: c58f6df0-5aad-40a3-bddc-319c378218e3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: node
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 722cda244d4f633247827f58ea6f1397137ea600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-existing-nodejs-azure-mobile-service-tooapp-service"></a>기존 프로그램 Node.js Azure 모바일 서비스 tooApp 서비스 업그레이드
앱 서비스 모바일을 새로운 방식으로 toobuild 모바일 응용 프로그램 Microsoft Azure를 사용 하 여입니다. toolearn 더 참조 [모바일 앱 이란?]합니다.

이 항목에서는 설명 방법을 tooupgrade tooa Azure 모바일 서비스에서에서 기존 Node.js 백 엔드 응용 프로그램이 새 앱 서비스 모바일 앱. 이 업그레이드를 수행 하는 동안 기존 모바일 서비스 응용 프로그램 toooperate를 계속 수 있습니다.  Tooupgrade Node.js 백 엔드 응용 프로그램, 필요한 경우 너무 참조[.NET 모바일 서비스를 업그레이드](app-service-mobile-net-upgrading-from-mobile-services.md)합니다.

너무에 따라 청구 되며 앱 서비스 기능 액세스 tooall 모바일 백 엔드 응용 프로그램 서비스 업그레이드 tooAzure 인 경우에[앱 서비스 가격 책정], 모바일 서비스 가격 되지 않습니다.

## <a name="migrate-vs-upgrade"></a>마이그레이션과 업그레이드 비교
[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

> [!TIP]
> 업그레이드를 진행하기 전에 [마이그레이션을 수행](app-service-mobile-migrating-from-mobile-services.md) 하는 것이 좋습니다. 이러한 방식으로 응용 프로그램의 두 버전 모두 넣을 수 있습니다에 동일한 앱 서비스 계획 hello 및 추가 비용 없이 발생 합니다.
>
>

### <a name="improvements-in-mobile-apps-nodejs-server-sdk"></a>모바일 앱 Node.js 서버 SDK에서 향상된 기능
새 toohello 업그레이드 [모바일 앱 SDK](https://www.npmjs.com/package/azure-mobile-apps) 효과적으로 개선 되었습니다.:

* Hello에 따라 [프레임 워크 Express](http://expressjs.com/en/index.html), hello 새 노드 SDK는 간단한 오면 새 노드 버전이 함께 tookeep를 디자인 하 고 있습니다. Hello Express 미들웨어 응용 프로그램 동작을 사용자 지정할 수 있습니다.
* 성능 향상 toohello 모바일 서비스 SDK를 비교합니다.
* 웹 사이트와 모바일 백 엔드; 함께 호스트할 수 있습니다. 마찬가지로, 쉽게 tooadd hello Azure Mobile SDK tooany 기존 express.v4 응용 프로그램입니다.
* 플랫폼 간 및 로컬 개발을 위한 기본 제공 hello 모바일 앱 SDK 개발 하 고 Windows, Linux 및 OSX 플랫폼에서 로컬로 실행 합니다. 이제는 쉽게 toouse 일반적인 노드 개발 기술 실행 같은 [Mocha](https://mochajs.org/) 이전 toodeployment 테스트 합니다.

## <a name="overview"></a>기본 업그레이드 개요
tooaid Node.js 백 엔드 Azure 앱 서비스를 업그레이드할 때의 호환성 패키지를 제공 했습니다.  업그레이드 후 배포 된 tooa 새 앱 서비스 사이트 일 수 있는 niew 사이트를 해야 합니다.

hello 모바일 서비스 클라이언트 Sdk는 **하지** hello 새로운 모바일 앱 서버 SDK와 호환 됩니다. 앱에 대 한 서비스, 순서 tooprovide 지속적인 하지 변경 tooa 사이트에서는 현재 게시 된 클라이언트를 게시 해야 합니다. 대신 중복으로 제공한 새 모바일 앱을 만들어야 합니다. 이 응용 프로그램을 넣을 수 hello에서 동일한 앱 서비스 계획 tooavoid 재무 추가 비용 발생 합니다.

다음 두 가지 버전 hello 응용 프로그램의: 동일 hello 상태를 유지 하는 하나 및 hello 와일드에 게시 된 앱을 하는 데 사용 하 고 그런 다음 업그레이드할 수 있는 다른 및 새 클라이언트와 대상 해제 합니다. 이동 하 고, 속도로 코드를 테스트할 수 있지만 그러면 만들면 버그 수정 사항이 적용 된 tooboth을 가져올 확인 해야 합니다. 실생활에서 클라이언트 응용 프로그램의 수가 toohello 최신 버전 업데이트, 원하는 경우 hello 원래 마이그레이션된 응용 프로그램을 삭제할 수 있습니다 수 있다고 생각 되 면 합니다. Hello 모바일 앱으로 동일한 앱 서비스 계획에서 호스팅되는 경우 모든 추가 금전적 비용이 부과 되지 않습니다 것입니다.

hello hello 업그레이드 프로세스에 대 한 전체 개요는 다음과 같습니다.

1. 기존(마이그레이션된) Azure 모바일 서비스를 다운로드합니다.
2. Hello 프로젝트 tooan Azure 모바일 앱으로 변환 hello 호환성 패키지를 사용 하 여 합니다.
3. 모든 차이(예: 인증 설정)를 수정합니다.
4. 배포 프로그램 변환 된 Azure 모바일 앱 프로젝트 tooa 새 앱 서비스입니다.
5. 사용 하 여 새로운 모바일 앱 hello는 클라이언트 응용 프로그램의 새 버전을 출시 하 합니다.
6. (선택 사항) 원래 마이그레이션된 모바일 서비스 앱 삭제

삭제는 원래 마이그레이션된 모바일 서비스에 트래픽이 표시되지 않을 때 발생할 수 있습니다.

## <a name="install-npm-package"></a>Hello 필수 조건을 설치합니다
로컬 컴퓨터에 [노드]를 설치해야 합니다.  또한 hello 호환성 패키지를 설치 해야 합니다.  노드를 설치한 후에 hello 새 cmd 또는 PowerShell 프롬프트에서 다음 명령을 실행할 수 있습니다.

```npm i -g azure-mobile-apps-compatibility```

## <a name="obtain-ams-scripts"></a> Azure 모바일 서비스 스크립트 가져오기
* Toohello 로그인 [Azure 포털]합니다.
* **모든 리소스** 또는 **앱 서비스**를 사용하여 모바일 서비스 사이트를 찾습니다.
* Hello 사이트 내에서 클릭 **도구** -> **Kudu** -> **이동** tooopen hello Kudu 사이트입니다.
* 클릭 **디버그 콘솔** -> **PowerShell** tooopen hello 디버그 콘솔.
* 너무 이동`site/wwwroot/App_Data/config` 각 디렉터리를 차례로 클릭 하 여
* Hello 다운로드 아이콘 다음 toohello 클릭 `scripts` 디렉터리입니다.

ZIP 형식에서 hello 스크립트 다운로드 합니다.  로컬 컴퓨터에 새 디렉터리를 만들고 hello 압축 풀기 `scripts.ZIP` hello 디렉터리 내의 파일입니다.  `scripts` 디렉터리를 만듭니다.

## <a name="scaffold-app"></a>스 캐 폴드 hello 새 Azure 모바일 앱 백 엔드
Hello hello 스크립트 디렉터리를 포함 하는 hello 디렉터리에서 다음 명령을 실행 합니다.

```scaffold-mobile-app scripts out```

Hello에 스 캐 폴드 Azure 모바일 앱 백 엔드 만들어집니다 `out` 디렉터리입니다.  것이 좋습니다 toocheck hello 필요 하지는 않지만 `out` 디렉터리를 소스 코드 리포지토리를 선택 합니다.

## <a name="deploy-ama-app"></a> Azure 모바일 앱 백 엔드 배포
배포 하는 동안 toodo hello 다음이 필요 합니다.

1. Hello에서 새로운 모바일 앱을 만들 [Azure 포털]합니다.
2. Hello 실행 `createViews.sql` 로 스크립트에 연결 된 데이터베이스입니다.
3. 링크 hello 데이터베이스에 연결 된 tooyour 모바일 서비스 tooyour 새 앱 서비스입니다.
4. 다른 리소스 (예: 알림 허브) toohello 연결 새 앱 서비스입니다.
5. 생성 된 hello 코드 tooyour 새 사이트를 배포 합니다.

### <a name="create-a-new-mobile-app"></a>새 모바일 앱 만들기
1. Hello에 로그인 [Azure 포털]합니다.
2. **+새로 만들기** > **웹 + 모바일** > **모바일 앱**을 클릭한 다음 모바일 앱 백 엔드에 대한 이름을 제공합니다.
3. Hello에 대 한 **리소스 그룹**기존 리소스 그룹을 선택 하거나 새로 만듭니다 (앱 이름이 같은 hello를 사용 하 여.)

    다른 앱 서비스 계획을 선택하거나 새 앱 서비스 계획을 만들 수 있습니다. 앱 서비스 계획 및 toocreate 새 계획에 다른 가격 책정 계층 하 고 원하는 위치에서 참조 하는 방법에 대 한 자세한 [Azure 앱 서비스 계획 심도 깊은 개요](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)합니다.
4. Hello에 대 한 **앱 서비스 계획**, hello 기본 계획 (hello에 [표준 계층](https://azure.microsoft.com/pricing/details/app-service/))을 선택 합니다. 또한 다른 계획을 선택하거나 [새 계획을 만들 수 있습니다](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md#create-an-app-service-plan). hello 앱 서비스 계획의 설정에 따라 결정 hello [위치, 기능, 비용 및 계산 리소스](https://azure.microsoft.com/pricing/details/app-service/) 연결 된 앱입니다.

    Hello 계획을 결정 한 다음 클릭 **만들기**합니다. Hello 모바일 앱 백 엔드를 만듭니다.

### <a name="run-createviewssql"></a>CreateViews.SQL을 실행합니다.
라는 파일을 포함 하는 hello 스 캐 폴드 앱 `createViews.sql`합니다.  이 스크립트는 대상 데이터베이스에 대해 실행되어야 합니다.  hello 대상 데이터베이스에 대 한 연결 문자열 hello hello에서 마이그레이션된 모바일 서비스에서 가져올 수 있습니다 **설정** 아래 블레이드 **연결 문자열**합니다.  `MS_TableConnectionString`(이)라고 합니다.

SQL Server Management Studio 또는 Visual Studio 내에서 이 스크립트를 실행할 수 있습니다.

### <a name="link-hello-database-tooyour-app-service"></a>링크 hello 데이터베이스 tooyour 앱 서비스
Hello 기존 데이터베이스 tooyour 응용 프로그램 서비스 링크:

* Hello에 [Azure 포털], 응용 프로그램 서비스를 엽니다.
* **모든 설정** -> **데이터 연결**을 선택합니다.
* **+ 추가**를 클릭합니다.
* Hello 드롭다운 목록에서에서 선택 **SQL 데이터베이스**
* **SQL Database** 아래에서 기존 데이터베이스를 선택한 다음 **선택**을 클릭합니다.
* 아래 **연결 문자열**, hello 데이터베이스에 대 한 hello 사용자 이름 및 암호를 입력 한 다음 클릭 **확인**합니다.
* Hello에 **데이터 연결 추가** 블레이드에서 클릭 **확인**합니다.

마이그레이션된 모바일 서비스에 hello 대상 데이터베이스에 대 한 연결 문자열 hello를 확인 하 여 hello 사용자 이름 및 암호를 찾을 수 있습니다.

### <a name="set-up-authentication"></a>인증 설정
Azure 모바일 앱 hello 서비스 내에서 Azure Active Directory, Facebook, Google, Microsoft 및 Twitter 인증을 tooconfigure 있습니다.  사용자 지정 인증 toobe 개별적으로 개발 해야 합니다.  Hello에 대 한 참조 [인증의 개념] 설명서 및 [인증 퀵 스타트] 자세한 정보에 대 한 설명서입니다.  

## <a name="updating-clients"></a>모바일 클라이언트 업데이트
작동하는 모바일 앱 백 엔드가 있으면 그것을 사용하는 클라이언트 응용 프로그램의 새 버전에서 작동할 수 있습니다. 모바일 앱도 hello 클라이언트 Sdk의 새 버전을 포함 하며, 유사한 toohello 서버 업그레이드 위의 tooremove 하기 전에 toohello 모바일 서비스 Sdk를 참조 하는 모든가 필요 모바일 앱 버전을 설치 합니다.

Hello 버전 간의 주요 변경 내용은 hello 중 하나는 hello 생성자에 더 이상 응용 프로그램 키 필요입니다.
이제 단순히 전달 모바일 앱의 hello URL입니다. 예를 들어 hello.NET 클라이언트를 hello `MobileServiceClient` 생성자는 이제:

        public static MobileServiceClient MobileService = new MobileServiceClient(
            "https://contoso.azurewebsites.net" // URL of hello Mobile App
        );

설치에 대 한 읽을 수 새 Sdk hello 및 hello 아래 hello 링크를 통해 새 구조를 사용 하 여:

* [Android 버전 2.2 이상](app-service-mobile-android-how-to-use-client-library.md)
* [iOS 버전 3.0.0 이상](app-service-mobile-ios-how-to-use-client-library.md)
* [.NET(Windows/Xamarin) 버전 2.0.0 이상](app-service-mobile-dotnet-how-to-use-client-library.md)
* [Apache Cordova 버전 2.0 이상](app-service-mobile-cordova-how-to-use-client-library.md)

응용 프로그램이 경우 개의 푸시 알림을 사용 하 여, hello 각 플랫폼에 대 한 특정 등록 지침을 기록해 대로 몇 가지 변경 사항이 있는 합니다.

Hello 새 클라이언트 버전 준비을 사용 하는 경우 사용해 업그레이드 된 서버 프로젝트에 대해 합니다. 확인 한 후 작동 하는지, 새 버전의 응용 프로그램 toocustomers 놓을 수 있습니다. 결국 고객이 있는 반면 기회 tooreceive 이러한 업데이트를 일단 응용 프로그램의 hello 모바일 서비스 버전을 삭제할 수 있습니다. 앱 서비스 모바일 앱 tooan 완전히 업그레이드이 시점에서 hello 최신 모바일 앱 서버 SDK를 사용 합니다.

<!-- URLs. -->

[Azure 포털]: https://portal.azure.com/
[Azure classic portal]: https://manage.windowsazure.com/
[모바일 앱 이란?]: app-service-mobile-value-prop.md
[I already use web sites and mobile services – how does App Service help me?]: /en-us/documentation/articles/app-service-mobile-value-prop-migration-from-mobile-services
[Mobile App Server SDK]: https://www.npmjs.com/package/azure-mobile-apps
[Create a Mobile App]: app-service-mobile-xamarin-ios-get-started.md
[Add push notifications tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-push.md
[Add authentication tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-users.md
[Azure Scheduler]: /en-us/documentation/services/scheduler/
[Web Job]: ../app-service-web/websites-webjobs-resources.md
[How toouse hello .NET server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Migrate from Mobile Services tooan App Service Mobile App]: app-service-mobile-migrating-from-mobile-services.md
[Migrate your existing Mobile Service tooApp Service]: app-service-mobile-migrating-from-mobile-services.md
[앱 서비스 가격 책정]: https://azure.microsoft.com/en-us/pricing/details/app-service/
[.NET server SDK overview]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[인증의 개념]: ../app-service/app-service-authentication-overview.md
[인증 퀵 스타트]: app-service-mobile-auth.md

[Azure 포털]: https://portal.azure.com/
[OData]: http://www.odata.org
[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[basicapp sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app
[todo sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo
[samples directory on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
[QueryJS]: https://github.com/Azure/queryjs
[Node.js Tools 1.1 for Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1
[mssql Node.js package]: https://www.npmjs.com/package/mssql
[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx
[ExpressJS Middleware]: http://expressjs.com/guide/using-middleware.html
[Winston]: https://github.com/winstonjs/winston
