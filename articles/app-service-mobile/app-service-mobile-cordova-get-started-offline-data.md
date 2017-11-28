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
# <a name="enable-offline-sync-for-your-cordova-mobile-app"></a><span data-ttu-id="3d05c-103">Cordova 모바일 앱에 대해 오프라인 동기화 사용</span><span class="sxs-lookup"><span data-stu-id="3d05c-103">Enable offline sync for your Cordova mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

<span data-ttu-id="3d05c-104">이 자습서에서는 Cordova에 대 한 Azure 모바일 앱의 hello 오프 라인 동기화 기능을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-104">This tutorial introduces hello offline sync feature of Azure Mobile Apps for Cordova.</span></span> <span data-ttu-id="3d05c-105">오프 라인 동기화 허용 모바일 앱과 함께 최종 사용자가 toointeract&mdash;보기, 추가 또는 데이터 수정&mdash;네트워크 연결이 없는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-105">Offline sync allows end users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="3d05c-106">변경 내용은 로컬 데이터베이스에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-106">Changes are stored in a local database.</span></span>  <span data-ttu-id="3d05c-107">Hello 장치를 다시 온라인 상태가 되 면 이러한 변경 내용은 hello 원격 서비스와 동기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-107">Once hello device is back online, these changes are synced with hello remote service.</span></span>

<span data-ttu-id="3d05c-108">모바일 앱을 완료할 때 만드는 자습서를 hello에 대 한이 자습서 hello Cordova 퀵 스타트 솔루션 기반 [Apache Cordova 퀵 스타트]합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-108">This tutorial is based on hello Cordova quickstart solution for Mobile Apps that you create when you complete hello tutorial [Apache Cordova quick start].</span></span> <span data-ttu-id="3d05c-109">이 자습서에서는 hello 퀵 스타트 솔루션 tooadd 오프 라인 기능 Azure 모바일 앱의 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-109">In this tutorial, you update hello quickstart solution tooadd offline features of Azure Mobile Apps.</span></span>  <span data-ttu-id="3d05c-110">Hello 오프 라인 관련 코드가 hello 앱에도 강조 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-110">We also highlight hello offline-specific code in hello app.</span></span>

<span data-ttu-id="3d05c-111">hello 항목을 참조 하는 hello 오프 라인 동기화 기능에 대해 자세히 toolearn [Azure 모바일 앱에서 데이터 동기화를 오프 라인]합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-111">toolearn more about hello offline sync feature, see hello topic [Offline Data Sync in Azure Mobile Apps].</span></span> <span data-ttu-id="3d05c-112">API 사용의 자세한 참조 hello [API 설명서](https://azure.github.io/azure-mobile-apps-js-client)합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-112">For details of API usage, see hello [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

## <a name="add-offline-sync-toohello-quickstart-solution"></a><span data-ttu-id="3d05c-113">오프 라인 동기화 toohello 퀵 스타트 솔루션 추가</span><span class="sxs-lookup"><span data-stu-id="3d05c-113">Add offline sync toohello quickstart solution</span></span>
<span data-ttu-id="3d05c-114">hello 오프 라인 동기화 코드 toohello 앱을 추가 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-114">hello offline sync code must be added toohello app.</span></span> <span data-ttu-id="3d05c-115">오프 라인 동기화 hello cordova sqlite 저장소 플러그 인을 자동으로 가져옵니다 추가 tooyour 앱 hello Azure 모바일 앱 플러그 인 hello 프로젝트에 포함 된 경우 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-115">Offline sync requires hello cordova-sqlite-storage plugin, which automatically gets added tooyour app when hello Azure Mobile Apps plugin is included in hello project.</span></span> <span data-ttu-id="3d05c-116">hello 퀵 스타트 프로젝트는 모두 이러한 플러그인을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-116">hello Quickstart project includes both of these plugins.</span></span>

1. <span data-ttu-id="3d05c-117">Visual Studio의 솔루션 탐색기에서 index.js 열고 hello 코드 다음 바꾸기</span><span class="sxs-lookup"><span data-stu-id="3d05c-117">In Visual Studio's Solution Explorer, open index.js and replace hello following code</span></span>

        var client,            // Connection toohello Azure Mobile App backend
           todoItemTable;      // Reference tooa table endpoint on backend

    <span data-ttu-id="3d05c-118">바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-118">with this code:</span></span>

        var client,            // Connection toohello Azure Mobile App backend
           todoItemTable,      // Reference tooa table endpoint on backend
           syncContext;        // Reference toooffline data sync context

2. <span data-ttu-id="3d05c-119">코드 다음 hello를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-119">Next, replace hello following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');

    <span data-ttu-id="3d05c-120">바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-120">with this code:</span></span>

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

    <span data-ttu-id="3d05c-121">hello 이전 코드 추가 hello 로컬 저장소를 초기화 및 사용 되는 hello 열 값과 일치 하는 로컬 테이블을 정의 하면 Azure에서 백 엔드 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-121">hello preceding code additions initialize hello local store and define a local table that matches hello column values used in your Azure back end.</span></span> <span data-ttu-id="3d05c-122">(않아도 tooinclude이이 코드의 모든 열 값입니다.)  hello `version` 필드 hello 모바일 백 엔드가 유지 관리 하 고 충돌 해결에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-122">(You don't need tooinclude all column values in this code.)  hello `version` field is maintained by hello mobile backend and is used for conflict resolution.</span></span>

    <span data-ttu-id="3d05c-123">호출 하 여 참조 toohello 동기화 컨텍스트를 가져올 **getSyncContext**합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-123">You get a reference toohello sync context by calling **getSyncContext**.</span></span> <span data-ttu-id="3d05c-124">hello 동기화 상황에 맞는 사용 하면 추적 하 고 클라이언트 응용 프로그램은 수정 될 때 모든 테이블의 변경 내용 밀어넣기 테이블 관계 보존 `.push()` 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-124">hello sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when `.push()` is called.</span></span>

3. <span data-ttu-id="3d05c-125">Hello 응용 프로그램 URL tooyour 모바일 앱 응용 프로그램 URL을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-125">Update hello application URL tooyour Mobile App application URL.</span></span>

4. <span data-ttu-id="3d05c-126">다음으로 이 코드를</span><span class="sxs-lookup"><span data-stu-id="3d05c-126">Next, replace this code:</span></span>

        todoItemTable = client.getTable('todoitem'); // todoitem is hello table name

    <span data-ttu-id="3d05c-127">바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-127">with this code:</span></span>

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

    <span data-ttu-id="3d05c-128">hello 앞의 코드 hello 동기화 컨텍스트를 초기화를 호출 합니다 (getTable) 대신 getSyncTable tooget 참조 toohello 로컬 테이블.</span><span class="sxs-lookup"><span data-stu-id="3d05c-128">hello preceding code initializes hello sync context and then calls getSyncTable (instead of getTable) tooget a reference toohello local table.</span></span>

    <span data-ttu-id="3d05c-129">이 코드에서는 hello 로컬 데이터베이스 모두에 대 한 만들기, 읽기, 업데이트 및 삭제 (CRUD) 테이블 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-129">This code uses hello local database for all create, read, update, and delete (CRUD) table operations.</span></span>

    <span data-ttu-id="3d05c-130">이 샘플에서는 동기화 충돌의 간단한 오류를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-130">This sample performs simple error handling on sync conflicts.</span></span> <span data-ttu-id="3d05c-131">실제 응용 프로그램 처리 하는 것 hello 네트워크 상태, 서버 충돌 등과 같은 다양 한 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-131">A real application would handle hello various errors like network conditions, server conflicts, and others.</span></span> <span data-ttu-id="3d05c-132">코드 예제를 보려면 참조 hello [오프 라인 동기화 샘플]합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-132">For code examples, see hello [offline sync sample].</span></span>

5. <span data-ttu-id="3d05c-133">다음으로,이 함수 tooperform hello 실제 동기화를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-133">Next, add this function tooperform hello actual sync.</span></span>

        function syncBackend() {

          // Sync local store tooAzure table when app loads, or when login complete.
          syncContext.push().then(function () {
              // Push completed

          });

          // Pull items from hello Azure table after syncing tooAzure.
          syncContext.pull(new WindowsAzure.Query('todoitem'));
        }

    <span data-ttu-id="3d05c-134">Toopush toohello 모바일 앱 백 엔드를 호출 하 여 변경 될 때 결정 **syncContext.push()**합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-134">You decide when toopush changes toohello Mobile App backend by calling **syncContext.push()**.</span></span> <span data-ttu-id="3d05c-135">예를 들어, 호출할 수 있습니다 **syncBackend** 단추 이벤트 처리기 동률된 tooa 동기화 단추에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-135">For example, you could call **syncBackend** in a button event handler tied tooa sync button.</span></span>

## <a name="offline-sync-considerations"></a><span data-ttu-id="3d05c-136">오프라인 동기화 고려 사항</span><span class="sxs-lookup"><span data-stu-id="3d05c-136">Offline sync considerations</span></span>

<span data-ttu-id="3d05c-137">Hello 샘플에서 hello **푸시** 방식의 **syncContext** 로그인에 대 한 콜백 함수 hello에서에서 응용 프로그램 시작에만 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-137">In hello sample, hello **push** method of **syncContext** is only called on app startup in hello callback function for login.</span></span>  <span data-ttu-id="3d05c-138">실제 응용 프로그램에서이 동기화 기능을 수동으로 트리거할 또는 hello 네트워크 상태가 변경 될 때 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-138">In a real-world application, you could also make this sync functionality triggered manually or when hello network state changes.</span></span>

<span data-ttu-id="3d05c-139">끌어오기 보류 중이 있는 테이블에 대해 실행 된 로컬에서 업데이트 밀어넣기를 가져오는 작업을 자동으로 트리거 hello 컨텍스트별 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-139">When a pull is executed against a table that has pending local updates tracked by hello context, that pull operation automatically triggers a push.</span></span> <span data-ttu-id="3d05c-140">생략할 수 새로 고침,를 추가 하 고이 샘플에 있는 항목을 완료 하는 경우 명시적 hello **푸시** 중복 될 수 있으므로 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-140">When refreshing, adding, and completing items in this sample, you can omit hello explicit **push** call, since it may be redundant.</span></span>

<span data-ttu-id="3d05c-141">Hello 원격 todoItem 테이블의 모든 레코드를 제공 하는 hello 코드에서 쿼리, 것 뿐만 아니라 가능한 toofilter 레코드는 쿼리 id 및 쿼리를 전달 하 여 너무**푸시**합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-141">In hello provided code, all records in hello remote todoItem table are queried, but it is also possible toofilter records by passing a query id and query too**push**.</span></span> <span data-ttu-id="3d05c-142">자세한 내용은 hello 섹션을 참조 하십시오. *증분 동기화* 에 [Azure 모바일 앱에서 데이터 동기화를 오프 라인]합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-142">For more information, see hello section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="optional-disable-authentication"></a><span data-ttu-id="3d05c-143">(선택 사항)인증 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="3d05c-143">(Optional) Disable authentication</span></span>

<span data-ttu-id="3d05c-144">하지 않는 tooset 오프 라인 동기화를 테스트 하기 전에 인증을, 로그인에 대 한 hello 콜백 함수를 주석 처리 하지만 내부에서 코드를 hello 둡니다 hello 콜백 함수 주석 처리가 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-144">If you don't want tooset up authentication before testing offline sync, comment out hello callback function for login, but leave hello code inside hello callback function uncommented.</span></span>  <span data-ttu-id="3d05c-145">Hello 로그인 줄을 주석 후 hello 코드가 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-145">After commenting out hello login lines, hello code follows:</span></span>

      // Login toohello service.
      // client.login('twitter')
      //    .then(function () {
        syncContext.initialize(store).then(function () {
          // Leave hello rest of hello code in this callback function  uncommented.
                ...
        });
      // }, handleError);

<span data-ttu-id="3d05c-146">이제 hello 앱와 동기화 hello Azure 백 엔드 hello 응용 프로그램을 실행 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="3d05c-146">Now, hello app syncs with hello Azure backend when you run hello app.</span></span>

## <a name="run-hello-client-app"></a><span data-ttu-id="3d05c-147">Hello 클라이언트 앱 실행</span><span class="sxs-lookup"><span data-stu-id="3d05c-147">Run hello client app</span></span>
<span data-ttu-id="3d05c-148">이제 사용 하도록 설정 하는 오프 라인 동기화를 hello 로컬 저장소 데이터베이스를 채우는 각 플랫폼에서 hello 클라이언트 응용 프로그램을 한 번 이상 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-148">With offline sync now enabled, you can run hello client application at least once on each platform to populate hello local store database.</span></span> <span data-ttu-id="3d05c-149">나중 오프 라인 시나리오를 시뮬레이션 하 고 hello 앱 오프 라인 상태인 동안 hello 로컬 저장소의 hello 데이터를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-149">Later, simulate an offline scenario and modify hello data in hello local store while hello app is offline.</span></span>

## <a name="optional-test-hello-sync-behavior"></a><span data-ttu-id="3d05c-150">(선택 사항) Hello 동기화 동작 테스트</span><span class="sxs-lookup"><span data-stu-id="3d05c-150">(Optional) Test hello sync behavior</span></span>
<span data-ttu-id="3d05c-151">이 섹션에서는 백 엔드에 대 한 잘못 된 응용 프로그램 URL을 사용 하 여 hello 클라이언트 프로젝트 toosimulate 오프 라인 시나리오를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-151">In this section, you modify hello client project toosimulate an offline scenario by using an invalid application URL for your backend.</span></span> <span data-ttu-id="3d05c-152">를 추가 하거나 데이터 항목을 변경 하는 경우 이러한 변경 내용은 로컬 저장소에 보관 됩니다 있지만 hello 연결이 다시 설정 될 때까지 동기화 된 toohello 백 엔드 데이터 저장소 되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-152">When you add or change data items, these changes are held in the local store, but are not synced toohello backend data store until hello connection is re-established.</span></span>

1. <span data-ttu-id="3d05c-153">솔루션 탐색기 hello hello index.js 프로젝트 파일을 열고 hello 응용 프로그램 URL toopoint 코드 다음 hello와 같은 잘못 된 URL로 변경:</span><span class="sxs-lookup"><span data-stu-id="3d05c-153">In hello Solution Explorer, open hello index.js project file and change hello application URL toopoint to  an invalid URL, like hello following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net-fail');

2. <span data-ttu-id="3d05c-154">Index.html에서 CSP hello 업데이트 `<meta>` 요소 hello 같은 잘못 된 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-154">In index.html, update hello CSP `<meta>` element with hello same invalid URL.</span></span>

        <meta http-equiv="Content-Security-Policy" content="default-src 'self' data: gap: http://yourmobileapp.azurewebsites.net-fail; style-src 'self'; media-src *">

3. <span data-ttu-id="3d05c-155">빌드 및 hello 클라이언트 응용 프로그램을 실행 및 확인 hello 앱에서 로그인 한 후 백 엔드 hello와 동기화 하려고 할 때 예외가 hello 콘솔에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-155">Build and run hello client app and notice that an exception is logged in hello console when hello app attempts to sync with hello backend after login.</span></span> <span data-ttu-id="3d05c-156">추가 하는 모든 새 항목 toohello 모바일 백 엔드를 푸시 될 때까지 hello 로컬 저장소에만 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-156">Any new items you add exist only in hello local store until they are pushed toohello mobile backend.</span></span> <span data-ttu-id="3d05c-157">hello 클라이언트 응용 프로그램 연결된 toohello 백 엔드는 처럼 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-157">hello client app behaves as if it is connected toohello backend.</span></span>

4. <span data-ttu-id="3d05c-158">Hello 응용 프로그램을 닫고 tooverify hello 새 항목이 만든 지속형된 toohello 로컬 저장소 지 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-158">Close hello app and restart it tooverify that hello new items you created are persisted toohello local store.</span></span>

5. <span data-ttu-id="3d05c-159">(선택 사항) Visual Studio tooview hello 데이터 hello 백 엔드 데이터베이스에 변경 되지 않은 Azure SQL 데이터베이스 테이블 toosee 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-159">(Optional) Use Visual Studio tooview your Azure SQL Database table toosee that hello data in hello backend database has not changed.</span></span>

    <span data-ttu-id="3d05c-160">Visual Studio에서 **서버 탐색기**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-160">In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="3d05c-161">tooyour 데이터베이스 이동 **Azure**->**SQL 데이터베이스**합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-161">Navigate tooyour database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="3d05c-162">데이터베이스를 마우스 오른쪽 단추로 클릭하고 **SQL Server 개체 탐색기에서 열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-162">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="3d05c-163">이제 tooyour SQL 데이터베이스 테이블 및 해당 콘텐츠를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-163">Now you can browse tooyour SQL database table and its contents.</span></span>

## <a name="optional-test-hello-reconnection-tooyour-mobile-backend"></a><span data-ttu-id="3d05c-164">(선택 사항) Hello 재연결 tooyour 모바일 백 엔드를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-164">(Optional) Test hello reconnection tooyour mobile backend</span></span>

<span data-ttu-id="3d05c-165">이 섹션에서는 hello 앱 toohello 수 모바일 백을 온라인 상태로 돌아오는 hello 앱을 시뮬레이션에 다시 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-165">In this section, you reconnect hello app toohello mobile backend, which simulates hello app coming back to an online state.</span></span> <span data-ttu-id="3d05c-166">에 로그인 할 때 데이터는 동기화 된 tooyour 모바일 백 엔드입니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-166">When you log in, data is synced tooyour mobile backend.</span></span>

1. <span data-ttu-id="3d05c-167">Index.js를 다시 열고 하 고 hello 응용 프로그램 URL을 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-167">Reopen index.js and restore hello application URL.</span></span>
2. <span data-ttu-id="3d05c-168">Index.html을 다시 열고 hello CSP에에서 hello 응용 프로그램 URL을 수정 `<meta>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-168">Reopen index.html and correct hello application URL in hello CSP `<meta>` element.</span></span>
3. <span data-ttu-id="3d05c-169">다시 작성 하 고 hello 클라이언트 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-169">Rebuild and run hello client app.</span></span> <span data-ttu-id="3d05c-170">hello 앱 로그인 후 hello 모바일 앱 백 엔드와 toosync을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-170">hello app attempts toosync with hello mobile app backend after login.</span></span> <span data-ttu-id="3d05c-171">예외가 발생 하지 않을 hello 디버그 콘솔 로그인 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-171">Verify that no exceptions are logged in hello debug console.</span></span>
4. <span data-ttu-id="3d05c-172">(선택 사항) 보기 hello SQL Server 개체 탐색기 또는 Fiddler와 같은 나머지 도구를 사용 하 여 데이터를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-172">(Optional) View hello updated data using either SQL Server Object Explorer or a REST tool like Fiddler.</span></span> <span data-ttu-id="3d05c-173">공지 hello 데이터 hello 백 엔드 데이터베이스 hello 로컬 저장소와 동기화 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-173">Notice hello data has been synchronized between hello backend database and hello local store.</span></span>

    <span data-ttu-id="3d05c-174">고 hello 데이터 hello 데이터베이스 hello 로컬 저장소와 동기화 된 앱 끊어져도 추가한 hello 항목이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-174">Notice hello data has been synchronized between hello database and hello local store and contains hello items you added while your app was disconnected.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3d05c-175">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="3d05c-175">Additional resources</span></span>
* <span data-ttu-id="3d05c-176">[Azure 모바일 앱에서 데이터 동기화를 오프 라인]</span><span class="sxs-lookup"><span data-stu-id="3d05c-176">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="3d05c-177">[Visual Studio Tools for Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="3d05c-177">[Visual Studio Tools for Apache Cordova]</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d05c-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3d05c-178">Next steps</span></span>
* <span data-ttu-id="3d05c-179">Hello에 대 한 충돌 해결 등의 오프 라인 동기화 기능을 더 높은 수준의 검토 [오프 라인 동기화 샘플]</span><span class="sxs-lookup"><span data-stu-id="3d05c-179">Review more advanced offline sync features such as conflict resolution in hello [offline sync sample]</span></span>
* <span data-ttu-id="3d05c-180">Hello 오프 라인 동기화 hello에 대 한 API 참조 검토 [API 설명서](https://azure.github.io/azure-mobile-apps-js-client)합니다.</span><span class="sxs-lookup"><span data-stu-id="3d05c-180">Review hello offline sync API reference in hello [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

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
