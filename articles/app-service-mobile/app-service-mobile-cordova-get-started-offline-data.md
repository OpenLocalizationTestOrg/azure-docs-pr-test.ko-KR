---
title: "Azure 모바일 응용 프로그램 (Cordova)에 대 한 오프 라인 동기화 aaaEnable | Microsoft Docs"
description: "자세한 내용은 방법 toouse 앱 서비스 모바일 앱 toocache 및 동기화 오프 라인 데이터 Cordova 응용 프로그램에서"
documentationcenter: cordova
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 1a3f685d-f79d-4f8b-ae11-ff96e79e9de9
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-cordova-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 4e6ae96c3d96dac8ebb3749354b83a04686831b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-cordova-mobile-app"></a>Cordova 모바일 앱에 대해 오프라인 동기화 사용
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

이 자습서에서는 Cordova에 대 한 Azure 모바일 앱의 hello 오프 라인 동기화 기능을 소개 합니다. 오프 라인 동기화 허용 모바일 앱과 함께 최종 사용자가 toointeract&mdash;보기, 추가 또는 데이터 수정&mdash;네트워크 연결이 없는 경우에 합니다. 변경 내용은 로컬 데이터베이스에 저장됩니다.  Hello 장치를 다시 온라인 상태가 되 면 이러한 변경 내용은 hello 원격 서비스와 동기화 됩니다.

모바일 앱을 완료할 때 만드는 자습서를 hello에 대 한이 자습서 hello Cordova 퀵 스타트 솔루션 기반 [Apache Cordova 퀵 스타트]합니다. 이 자습서에서는 hello 퀵 스타트 솔루션 tooadd 오프 라인 기능 Azure 모바일 앱의 업데이트합니다.  Hello 오프 라인 관련 코드가 hello 앱에도 강조 표시합니다.

hello 항목을 참조 하는 hello 오프 라인 동기화 기능에 대해 자세히 toolearn [Azure 모바일 앱에서 데이터 동기화를 오프 라인]합니다. API 사용의 자세한 참조 hello [API 설명서](https://azure.github.io/azure-mobile-apps-js-client)합니다.

## <a name="add-offline-sync-toohello-quickstart-solution"></a>오프 라인 동기화 toohello 퀵 스타트 솔루션 추가
hello 오프 라인 동기화 코드 toohello 앱을 추가 되어야 합니다. 오프 라인 동기화 hello cordova sqlite 저장소 플러그 인을 자동으로 가져옵니다 추가 tooyour 앱 hello Azure 모바일 앱 플러그 인 hello 프로젝트에 포함 된 경우 필요 합니다. hello 퀵 스타트 프로젝트는 모두 이러한 플러그인을 포함 합니다.

1. Visual Studio의 솔루션 탐색기에서 index.js 열고 hello 코드 다음 바꾸기

        var client,            // Connection toohello Azure Mobile App backend
           todoItemTable;      // Reference tooa table endpoint on backend

    바꿉니다.

        var client,            // Connection toohello Azure Mobile App backend
           todoItemTable,      // Reference tooa table endpoint on backend
           syncContext;        // Reference toooffline data sync context

2. 코드 다음 hello를 다음으로 바꿉니다.

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');

    바꿉니다.

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');
        var store = new WindowsAzure.MobileServiceSqliteStore('store.db');

        store.defineTable({
          name: 'todoitem',
          columnDefinitions: {
              id: 'string',
              text: 'string',
              complete: 'boolean',
              version: 'string'
          }
        });

        // Get hello sync context from hello client
        syncContext = client.getSyncContext();

    hello 이전 코드 추가 hello 로컬 저장소를 초기화 및 사용 되는 hello 열 값과 일치 하는 로컬 테이블을 정의 하면 Azure에서 백 엔드 합니다. (않아도 tooinclude이이 코드의 모든 열 값입니다.)  hello `version` 필드 hello 모바일 백 엔드가 유지 관리 하 고 충돌 해결에 사용 됩니다.

    호출 하 여 참조 toohello 동기화 컨텍스트를 가져올 **getSyncContext**합니다. hello 동기화 상황에 맞는 사용 하면 추적 하 고 클라이언트 응용 프로그램은 수정 될 때 모든 테이블의 변경 내용 밀어넣기 테이블 관계 보존 `.push()` 라고 합니다.

3. Hello 응용 프로그램 URL tooyour 모바일 앱 응용 프로그램 URL을 업데이트 합니다.

4. 다음으로 이 코드를

        todoItemTable = client.getTable('todoitem'); // todoitem is hello table name

    바꿉니다.

        // Initialize hello sync context with hello store
        syncContext.initialize(store).then(function () {

        // Get hello local table reference.
        todoItemTable = client.getSyncTable('todoitem');

        syncContext.pushHandler = {
            onConflict: function (pushError) {
                // Handle hello conflict.
                console.log("Sync conflict! " + pushError.getError().message);
                // Update failed, revert tooserver's copy.
                pushError.cancelAndDiscard();
              },
              onError: function (pushError) {
                  // Handle hello error
                  // In hello simulated offline state, you get "Sync error! Unexpected connection failure."
                  console.log("Sync error! " + pushError.getError().message);
              }
        };

        // Call a function tooperform hello actual sync
        syncBackend();

        // Refresh hello todoItems
        refreshDisplay();

        // Wire up hello UI Event Handler for hello Add Item
        $('#add-item').submit(addItemHandler);
        $('#refresh').on('click', refreshDisplay);

    hello 앞의 코드 hello 동기화 컨텍스트를 초기화를 호출 합니다 (getTable) 대신 getSyncTable tooget 참조 toohello 로컬 테이블.

    이 코드에서는 hello 로컬 데이터베이스 모두에 대 한 만들기, 읽기, 업데이트 및 삭제 (CRUD) 테이블 작업 합니다.

    이 샘플에서는 동기화 충돌의 간단한 오류를 처리합니다. 실제 응용 프로그램 처리 하는 것 hello 네트워크 상태, 서버 충돌 등과 같은 다양 한 오류입니다. 코드 예제를 보려면 참조 hello [오프 라인 동기화 샘플]합니다.

5. 다음으로,이 함수 tooperform hello 실제 동기화를 추가 합니다.

        function syncBackend() {

          // Sync local store tooAzure table when app loads, or when login complete.
          syncContext.push().then(function () {
              // Push completed

          });

          // Pull items from hello Azure table after syncing tooAzure.
          syncContext.pull(new WindowsAzure.Query('todoitem'));
        }

    Toopush toohello 모바일 앱 백 엔드를 호출 하 여 변경 될 때 결정 **syncContext.push()**합니다. 예를 들어, 호출할 수 있습니다 **syncBackend** 단추 이벤트 처리기 동률된 tooa 동기화 단추에 있습니다.

## <a name="offline-sync-considerations"></a>오프라인 동기화 고려 사항

Hello 샘플에서 hello **푸시** 방식의 **syncContext** 로그인에 대 한 콜백 함수 hello에서에서 응용 프로그램 시작에만 호출 됩니다.  실제 응용 프로그램에서이 동기화 기능을 수동으로 트리거할 또는 hello 네트워크 상태가 변경 될 때 할 수도 있습니다.

끌어오기 보류 중이 있는 테이블에 대해 실행 된 로컬에서 업데이트 밀어넣기를 가져오는 작업을 자동으로 트리거 hello 컨텍스트별 추적 합니다. 생략할 수 새로 고침,를 추가 하 고이 샘플에 있는 항목을 완료 하는 경우 명시적 hello **푸시** 중복 될 수 있으므로 호출 합니다.

Hello 원격 todoItem 테이블의 모든 레코드를 제공 하는 hello 코드에서 쿼리, 것 뿐만 아니라 가능한 toofilter 레코드는 쿼리 id 및 쿼리를 전달 하 여 너무**푸시**합니다. 자세한 내용은 hello 섹션을 참조 하십시오. *증분 동기화* 에 [Azure 모바일 앱에서 데이터 동기화를 오프 라인]합니다.

## <a name="optional-disable-authentication"></a>(선택 사항)인증 사용 안 함

하지 않는 tooset 오프 라인 동기화를 테스트 하기 전에 인증을, 로그인에 대 한 hello 콜백 함수를 주석 처리 하지만 내부에서 코드를 hello 둡니다 hello 콜백 함수 주석 처리가 제거 합니다.  Hello 로그인 줄을 주석 후 hello 코드가 따릅니다.

      // Login toohello service.
      // client.login('twitter')
      //    .then(function () {
        syncContext.initialize(store).then(function () {
          // Leave hello rest of hello code in this callback function  uncommented.
                ...
        });
      // }, handleError);

이제 hello 앱와 동기화 hello Azure 백 엔드 hello 응용 프로그램을 실행 하는 경우.

## <a name="run-hello-client-app"></a>Hello 클라이언트 앱 실행
이제 사용 하도록 설정 하는 오프 라인 동기화를 hello 로컬 저장소 데이터베이스를 채우는 각 플랫폼에서 hello 클라이언트 응용 프로그램을 한 번 이상 실행할 수 있습니다. 나중 오프 라인 시나리오를 시뮬레이션 하 고 hello 앱 오프 라인 상태인 동안 hello 로컬 저장소의 hello 데이터를 수정 합니다.

## <a name="optional-test-hello-sync-behavior"></a>(선택 사항) Hello 동기화 동작 테스트
이 섹션에서는 백 엔드에 대 한 잘못 된 응용 프로그램 URL을 사용 하 여 hello 클라이언트 프로젝트 toosimulate 오프 라인 시나리오를 수정 합니다. 를 추가 하거나 데이터 항목을 변경 하는 경우 이러한 변경 내용은 로컬 저장소에 보관 됩니다 있지만 hello 연결이 다시 설정 될 때까지 동기화 된 toohello 백 엔드 데이터 저장소 되지는 않습니다.

1. 솔루션 탐색기 hello hello index.js 프로젝트 파일을 열고 hello 응용 프로그램 URL toopoint 코드 다음 hello와 같은 잘못 된 URL로 변경:

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net-fail');

2. Index.html에서 CSP hello 업데이트 `<meta>` 요소 hello 같은 잘못 된 URL입니다.

        <meta http-equiv="Content-Security-Policy" content="default-src 'self' data: gap: http://yourmobileapp.azurewebsites.net-fail; style-src 'self'; media-src *">

3. 빌드 및 hello 클라이언트 응용 프로그램을 실행 및 확인 hello 앱에서 로그인 한 후 백 엔드 hello와 동기화 하려고 할 때 예외가 hello 콘솔에 기록 됩니다. 추가 하는 모든 새 항목 toohello 모바일 백 엔드를 푸시 될 때까지 hello 로컬 저장소에만 존재 합니다. hello 클라이언트 응용 프로그램 연결된 toohello 백 엔드는 처럼 동작 합니다.

4. Hello 응용 프로그램을 닫고 tooverify hello 새 항목이 만든 지속형된 toohello 로컬 저장소 지 다시 시작 합니다.

5. (선택 사항) Visual Studio tooview hello 데이터 hello 백 엔드 데이터베이스에 변경 되지 않은 Azure SQL 데이터베이스 테이블 toosee 프로그램을 사용 합니다.

    Visual Studio에서 **서버 탐색기**를 엽니다. tooyour 데이터베이스 이동 **Azure**->**SQL 데이터베이스**합니다. 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **SQL Server 개체 탐색기에서 열기**를 선택합니다. 이제 tooyour SQL 데이터베이스 테이블 및 해당 콘텐츠를 이동할 수 있습니다.

## <a name="optional-test-hello-reconnection-tooyour-mobile-backend"></a>(선택 사항) Hello 재연결 tooyour 모바일 백 엔드를 테스트 합니다.

이 섹션에서는 hello 앱 toohello 수 모바일 백을 온라인 상태로 돌아오는 hello 앱을 시뮬레이션에 다시 연결 합니다. 에 로그인 할 때 데이터는 동기화 된 tooyour 모바일 백 엔드입니다.

1. Index.js를 다시 열고 하 고 hello 응용 프로그램 URL을 복원 합니다.
2. Index.html을 다시 열고 hello CSP에에서 hello 응용 프로그램 URL을 수정 `<meta>` 요소입니다.
3. 다시 작성 하 고 hello 클라이언트 응용 프로그램을 실행 합니다. hello 앱 로그인 후 hello 모바일 앱 백 엔드와 toosync을 시도합니다. 예외가 발생 하지 않을 hello 디버그 콘솔 로그인 되어 있는지 확인 합니다.
4. (선택 사항) 보기 hello SQL Server 개체 탐색기 또는 Fiddler와 같은 나머지 도구를 사용 하 여 데이터를 업데이트 합니다. 공지 hello 데이터 hello 백 엔드 데이터베이스 hello 로컬 저장소와 동기화 되었습니다.

    고 hello 데이터 hello 데이터베이스 hello 로컬 저장소와 동기화 된 앱 끊어져도 추가한 hello 항목이 포함 됩니다.

## <a name="additional-resources"></a>추가 리소스
* [Azure 모바일 앱에서 데이터 동기화를 오프 라인]
* [Visual Studio Tools for Apache Cordova]

## <a name="next-steps"></a>다음 단계
* Hello에 대 한 충돌 해결 등의 오프 라인 동기화 기능을 더 높은 수준의 검토 [오프 라인 동기화 샘플]
* Hello 오프 라인 동기화 hello에 대 한 API 참조 검토 [API 설명서](https://azure.github.io/azure-mobile-apps-js-client)합니다.

<!-- ##Summary -->

<!-- Images -->

<!-- URLs. -->
[Apache Cordova 퀵 스타트]: app-service-mobile-cordova-get-started.md
[오프 라인 동기화 샘플]: https://github.com/Azure-Samples/app-service-mobile-cordova-client-conflict-handling
[Azure 모바일 앱에서 데이터 동기화를 오프 라인]: app-service-mobile-offline-data-sync.md
[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Adding Authentication]: app-service-mobile-cordova-get-started-users.md
[authentication]: app-service-mobile-cordova-get-started-users.md
[Work with hello .NET backend server SDK for Azure Mobile Apps]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Visual Studio Community 2015]: http://www.visualstudio.com/
[Visual Studio Tools for Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
