---
title: "Azure 모바일 앱에 대해 오프라인 동기화 사용(Cordova) | Microsoft Docs"
description: "앱 서비스 모바일 앱을 사용하여 Cordova 응용 프로그램에서 오프라인 데이터를 캐시 및 동기화하는 방법을 알아봅니다."
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
ms.openlocfilehash: 45e80ca672dfdb6defc6e5c1aac3d29f5479125c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="enable-offline-sync-for-your-cordova-mobile-app"></a><span data-ttu-id="3f1bf-103">Cordova 모바일 앱에 대해 오프라인 동기화 사용</span><span class="sxs-lookup"><span data-stu-id="3f1bf-103">Enable offline sync for your Cordova mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

<span data-ttu-id="3f1bf-104">이 자습서에서는 Cordova용 Azure 모바일 앱의 오프라인 동기화 기능을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-104">This tutorial introduces the offline sync feature of Azure Mobile Apps for Cordova.</span></span> <span data-ttu-id="3f1bf-105">오프라인 동기화를 사용하면 최종 사용자는 네트워크에 연결되어 있지 않을 때도 모바일 앱&mdash;데이터 보기, 추가 또는 수정&mdash;과 같은 상호 작용을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-105">Offline sync allows end users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="3f1bf-106">변경 내용은 로컬 데이터베이스에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-106">Changes are stored in a local database.</span></span>  <span data-ttu-id="3f1bf-107">장치가 다시 온라인 상태가 되면 이러한 변경 내용이 원격 서비스와 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-107">Once the device is back online, these changes are synced with the remote service.</span></span>

<span data-ttu-id="3f1bf-108">이 자습서는 [Apache Cordova 빠른 시작]자습서를 완료할 때 만든 모바일 앱에 대한 Cordova 빠른 시작 솔루션을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-108">This tutorial is based on the Cordova quickstart solution for Mobile Apps that you create when you complete the tutorial [Apache Cordova quick start].</span></span> <span data-ttu-id="3f1bf-109">이 자습서에서는 빠른 시작 솔루션을 업데이트하여 Azure Mobile Apps의 오프라인 기능을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-109">In this tutorial, you update the quickstart solution to add offline features of Azure Mobile Apps.</span></span>  <span data-ttu-id="3f1bf-110">또한 앱에서 오프라인 관련 코드를 중점적으로 다루겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-110">We also highlight the offline-specific code in the app.</span></span>

<span data-ttu-id="3f1bf-111">오프라인 동기화 기능에 대한 자세한 내용은 [증분 동기화]항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-111">To learn more about the offline sync feature, see the topic [Offline Data Sync in Azure Mobile Apps].</span></span> <span data-ttu-id="3f1bf-112">API 사용에 대한 자세한 내용은 [API 설명서](https://azure.github.io/azure-mobile-apps-js-client)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-112">For details of API usage, see the [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

## <a name="add-offline-sync-to-the-quickstart-solution"></a><span data-ttu-id="3f1bf-113">오프라인 동기화를 빠른 시작 솔루션에 추가</span><span class="sxs-lookup"><span data-stu-id="3f1bf-113">Add offline sync to the quickstart solution</span></span>
<span data-ttu-id="3f1bf-114">오프라인 동기화 코드를 앱에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-114">The offline sync code must be added to the app.</span></span> <span data-ttu-id="3f1bf-115">오프라인 동기화에는 cordova-sqlite-storage 플러그 인이 필요하며 이는 Azure 모바일 앱 플러그 인이 프로젝트에 포함될 때 앱에 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-115">Offline sync requires the cordova-sqlite-storage plugin, which automatically gets added to your app when the Azure Mobile Apps plugin is included in the project.</span></span> <span data-ttu-id="3f1bf-116">빠른 시작 프로젝트에는 이러한 플러그 인이 모두 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-116">The Quickstart project includes both of these plugins.</span></span>

1. <span data-ttu-id="3f1bf-117">Visual Studio의 솔루션 탐색기에서 index.js를 열고 다음 코드를 이 코드로 </span><span class="sxs-lookup"><span data-stu-id="3f1bf-117">In Visual Studio's Solution Explorer, open index.js and replace the following code</span></span>

        var client,            // Connection to the Azure Mobile App backend
           todoItemTable;      // Reference to a table endpoint on backend

    <span data-ttu-id="3f1bf-118">바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-118">with this code:</span></span>

        var client,            // Connection to the Azure Mobile App backend
           todoItemTable,      // Reference to a table endpoint on backend
           syncContext;        // Reference to offline data sync context

2. <span data-ttu-id="3f1bf-119">다음으로 다음 코드를</span><span class="sxs-lookup"><span data-stu-id="3f1bf-119">Next, replace the following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');

    <span data-ttu-id="3f1bf-120">바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-120">with this code:</span></span>

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

        // Get the sync context from the client
        syncContext = client.getSyncContext();

    <span data-ttu-id="3f1bf-121">이전 코드를 추가하면 로컬 저장소를 초기화하고 Azure 백 엔드에서 사용되는 열 값과 일치하는 로컬 테이블을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-121">The preceding code additions initialize the local store and define a local table that matches the column values used in your Azure back end.</span></span> <span data-ttu-id="3f1bf-122">(이 코드에 모든 열 값을 포함할 필요가 없습니다.)  `version` 필드는 모바일 백 엔드에 의해 유지 관리되며 충돌 해결에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-122">(You don't need to include all column values in this code.)  The `version` field is maintained by the mobile backend and is used for conflict resolution.</span></span>

    <span data-ttu-id="3f1bf-123">**getSyncContext**를 호출하여 동기화 컨텍스트에 대한 참조를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-123">You get a reference to the sync context by calling **getSyncContext**.</span></span> <span data-ttu-id="3f1bf-124">동기화 컨텍스트를 사용하면 모든 테이블의 변경 내용을 추적하고 밀어넣어서 테이블 관계를 보존할 수 있습니다. `.push()`를 호출하는 경우 클라이언트 앱을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-124">The sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when `.push()` is called.</span></span>

3. <span data-ttu-id="3f1bf-125">응용 프로그램 URL을 모바일 앱 응용 프로그램 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-125">Update the application URL to your Mobile App application URL.</span></span>

4. <span data-ttu-id="3f1bf-126">다음으로 이 코드를</span><span class="sxs-lookup"><span data-stu-id="3f1bf-126">Next, replace this code:</span></span>

        todoItemTable = client.getTable('todoitem'); // todoitem is the table name

    <span data-ttu-id="3f1bf-127">바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-127">with this code:</span></span>

        // Initialize the sync context with the store
        syncContext.initialize(store).then(function () {

        // Get the local table reference.
        todoItemTable = client.getSyncTable('todoitem');

        syncContext.pushHandler = {
            onConflict: function (pushError) {
                // Handle the conflict.
                console.log("Sync conflict! " + pushError.getError().message);
                // Update failed, revert to server's copy.
                pushError.cancelAndDiscard();
              },
              onError: function (pushError) {
                  // Handle the error
                  // In the simulated offline state, you get "Sync error! Unexpected connection failure."
                  console.log("Sync error! " + pushError.getError().message);
              }
        };

        // Call a function to perform the actual sync
        syncBackend();

        // Refresh the todoItems
        refreshDisplay();

        // Wire up the UI Event Handler for the Add Item
        $('#add-item').submit(addItemHandler);
        $('#refresh').on('click', refreshDisplay);

    <span data-ttu-id="3f1bf-128">이전 코드에서 동기화 컨텍스트를 초기화하고 getSyncTable(getTable 대신)을 호출하여 로컬 테이블에 대한 참조를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-128">The preceding code initializes the sync context and then calls getSyncTable (instead of getTable) to get a reference to the local table.</span></span>

    <span data-ttu-id="3f1bf-129">이 코드는 모든 만들기, 읽기, 업데이트 및 삭제(CRUD) 테이블 작업에 대해 로컬 저장소 데이터베이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-129">This code uses the local database for all create, read, update, and delete (CRUD) table operations.</span></span>

    <span data-ttu-id="3f1bf-130">이 샘플에서는 동기화 충돌의 간단한 오류를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-130">This sample performs simple error handling on sync conflicts.</span></span> <span data-ttu-id="3f1bf-131">실제 응용 프로그램에서는 네트워크 상태, 서버 충돌 및 기타와 같은 다양한 오류를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-131">A real application would handle the various errors like network conditions, server conflicts, and others.</span></span> <span data-ttu-id="3f1bf-132">코드 예제는 [오프라인 동기화 샘플]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-132">For code examples, see the [offline sync sample].</span></span>

5. <span data-ttu-id="3f1bf-133">다음으로, 이 함수를 추가하여 실제 동기화를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-133">Next, add this function to perform the actual sync.</span></span>

        function syncBackend() {

          // Sync local store to Azure table when app loads, or when login complete.
          syncContext.push().then(function () {
              // Push completed

          });

          // Pull items from the Azure table after syncing to Azure.
          syncContext.pull(new WindowsAzure.Query('todoitem'));
        }

    <span data-ttu-id="3f1bf-134">**syncContext.push()**를 호출하여 모바일 앱 백 엔드에 대한 변경 내용을 푸시할 시점을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-134">You decide when to push changes to the Mobile App backend by calling **syncContext.push()**.</span></span> <span data-ttu-id="3f1bf-135">예를 들어 동기화 단추에 연결된 단추 이벤트 처리기에서 **syncBackend**를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-135">For example, you could call **syncBackend** in a button event handler tied to a sync button.</span></span>

## <a name="offline-sync-considerations"></a><span data-ttu-id="3f1bf-136">오프라인 동기화 고려 사항</span><span class="sxs-lookup"><span data-stu-id="3f1bf-136">Offline sync considerations</span></span>

<span data-ttu-id="3f1bf-137">이 샘플에서 **syncContext**의 **푸시** 메서드는 로그인의 콜백 함수에서 앱 시작 시에만 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-137">In the sample, the **push** method of **syncContext** is only called on app startup in the callback function for login.</span></span>  <span data-ttu-id="3f1bf-138">실제 응용 프로그램에서는 네트워크 상태가 변경될 때 수동으로 트리거되는 이 동기화 기능을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-138">In a real-world application, you could also make this sync functionality triggered manually or when the network state changes.</span></span>

<span data-ttu-id="3f1bf-139">끌어오기가 컨텍스트에 의해 추적되는 로컬 업데이트를 보류 중인 테이블에 대해 실행되는 경우 끌어오기 작업은 자동으로 푸시를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-139">When a pull is executed against a table that has pending local updates tracked by the context, that pull operation automatically triggers a push.</span></span> <span data-ttu-id="3f1bf-140">이 샘플에서 항목을 새로 고침, 추가 및 완료하는 경우 명시적인 **push** 호출이 중복될 수 있으므로 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-140">When refreshing, adding, and completing items in this sample, you can omit the explicit **push** call, since it may be redundant.</span></span>

<span data-ttu-id="3f1bf-141">제공된 코드에서 원격 todoItem 테이블에 있는 모든 레코드를 쿼리하지만 쿼리 ID 및 쿼리를 **푸시**로 전달하여 레코드를 필터링할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-141">In the provided code, all records in the remote todoItem table are queried, but it is also possible to filter records by passing a query id and query to **push**.</span></span> <span data-ttu-id="3f1bf-142">자세한 내용은 *Azure 모바일 앱에서 오프라인 데이터 동기화* 에서 [증분 동기화]섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-142">For more information, see the section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="optional-disable-authentication"></a><span data-ttu-id="3f1bf-143">(선택 사항)인증 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="3f1bf-143">(Optional) Disable authentication</span></span>

<span data-ttu-id="3f1bf-144">오프라인 동기화를 테스트하기 전에 인증을 설정하지 않으려는 경우 로그인의 호출 함수를 주석 처리하지만 호출 함수 내에 있는 코드의 주석 처리를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-144">If you don't want to set up authentication before testing offline sync, comment out the callback function for login, but leave the code inside the callback function uncommented.</span></span>  <span data-ttu-id="3f1bf-145">로그인 줄을 주석 처리한 후 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-145">After commenting out the login lines, the code follows:</span></span>

      // Login to the service.
      // client.login('twitter')
      //    .then(function () {
        syncContext.initialize(store).then(function () {
          // Leave the rest of the code in this callback function  uncommented.
                ...
        });
      // }, handleError);

<span data-ttu-id="3f1bf-146">이제 앱을 실행하면 Azure 백 엔드와 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-146">Now, the app syncs with the Azure backend when you run the app.</span></span>

## <a name="run-the-client-app"></a><span data-ttu-id="3f1bf-147">클라이언트 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-147">Run the client app</span></span>
<span data-ttu-id="3f1bf-148">오프라인 동기화를 사용하도록 설정하면 각 플랫폼에서 클라이언트 응용 프로그램을 한 번 이상 실행하여 로컬 저장소 데이터베이스를 채울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-148">With offline sync now enabled, you can run the client application at least once on each platform to populate the local store database.</span></span> <span data-ttu-id="3f1bf-149">나중에 앱이 오프라인인 동안 오프라인 시나리오를 시뮬레이션하고 로컬 저장소에 있는 데이터를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-149">Later, simulate an offline scenario and modify the data in the local store while the app is offline.</span></span>

## <a name="optional-test-the-sync-behavior"></a><span data-ttu-id="3f1bf-150">(선택 사항)동기화 동작 테스트</span><span class="sxs-lookup"><span data-stu-id="3f1bf-150">(Optional) Test the sync behavior</span></span>
<span data-ttu-id="3f1bf-151">이 섹션에서 백 엔드에 잘못된 응용 프로그램 URL을 사용하여 오프라인 시나리오를 시뮬레이트하도록 클라이언트 프로젝트를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-151">In this section, you modify the client project to simulate an offline scenario by using an invalid application URL for your backend.</span></span> <span data-ttu-id="3f1bf-152">데이터 항목을 추가하거나 변경하는 경우 이러한 변경 내용은 로컬 저장소에 보관되지만 연결이 다시 설정될 때까지 백 엔드 데이터 저장소에 동기화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-152">When you add or change data items, these changes are held in the local store, but are not synced to the backend data store until the connection is re-established.</span></span>

1. <span data-ttu-id="3f1bf-153">솔루션 탐색기에서 index.js 프로젝트 파일을 열고 다음 코드와 같은 잘못된 URL을 가리키는 응용 프로그램 URL을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-153">In the Solution Explorer, open the index.js project file and change the application URL to point to  an invalid URL, like the following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net-fail');

2. <span data-ttu-id="3f1bf-154">index.html에서 동일하게 잘못된 URL을 포함하는 CSP `<meta>` 요소를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-154">In index.html, update the CSP `<meta>` element with the same invalid URL.</span></span>

        <meta http-equiv="Content-Security-Policy" content="default-src 'self' data: gap: http://yourmobileapp.azurewebsites.net-fail; style-src 'self'; media-src *">

3. <span data-ttu-id="3f1bf-155">클라이언트 앱을 빌드 및 실행하면 앱이 로그인한 후에 백 엔드와 동기화하려는 경우 예외가 콘솔에 로그인됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-155">Build and run the client app and notice that an exception is logged in the console when the app attempts to sync with the backend after login.</span></span> <span data-ttu-id="3f1bf-156">추가한 새 항목은 모바일 백 엔드에 푸시할 때까지 로컬 저장소에만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-156">Any new items you add exist only in the local store until they are pushed to the mobile backend.</span></span> <span data-ttu-id="3f1bf-157">클라이언트 앱은 백 엔드에 연결된 것처럼 동작합니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-157">The client app behaves as if it is connected to the backend.</span></span>

4. <span data-ttu-id="3f1bf-158">앱을 닫았다가 다시 시작하여 만든 새 항목이 로컬 저장소에 유지되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-158">Close the app and restart it to verify that the new items you created are persisted to the local store.</span></span>

5. <span data-ttu-id="3f1bf-159">(선택 사항) Azure SQL 데이터베이스 테이블을 보는 Visual Studio를 사용하여 백 엔드 데이터베이스에서 데이터가 변경되지 않았음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-159">(Optional) Use Visual Studio to view your Azure SQL Database table to see that the data in the backend database has not changed.</span></span>

    <span data-ttu-id="3f1bf-160">Visual Studio에서 **서버 탐색기**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-160">In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="3f1bf-161">**Azure**->**SQL Databases**에 있는 데이터베이스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-161">Navigate to your database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="3f1bf-162">데이터베이스를 마우스 오른쪽 단추로 클릭하고 **SQL Server 개체 탐색기에서 열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-162">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="3f1bf-163">이제 SQL 데이터베이스 테이블 및 콘텐츠를 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-163">Now you can browse to your SQL database table and its contents.</span></span>

## <a name="optional-test-the-reconnection-to-your-mobile-backend"></a><span data-ttu-id="3f1bf-164">(선택 사항)모바일 백 엔드에 대한 다시 연결 테스트</span><span class="sxs-lookup"><span data-stu-id="3f1bf-164">(Optional) Test the reconnection to your mobile backend</span></span>

<span data-ttu-id="3f1bf-165">이 섹션에서는 앱을 모바일 백 엔드에 다시 연결하여 다시 온라인 상태로 전환되는 앱을 시뮬레이트합니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-165">In this section, you reconnect the app to the mobile backend, which simulates the app coming back to an online state.</span></span> <span data-ttu-id="3f1bf-166">로그인할 때 데이터가 모바일 백 엔드에 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-166">When you log in, data is synced to your mobile backend.</span></span>

1. <span data-ttu-id="3f1bf-167">index.js를 다시 열고 응용 프로그램 URL을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-167">Reopen index.js and restore the application URL.</span></span>
2. <span data-ttu-id="3f1bf-168">index.html을 다시 열고 CSP `<meta>` 요소에서 응용 프로그램 URL을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-168">Reopen index.html and correct the application URL in the CSP `<meta>` element.</span></span>
3. <span data-ttu-id="3f1bf-169">클라이언트 앱을 다시 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-169">Rebuild and run the client app.</span></span> <span data-ttu-id="3f1bf-170">로그인한 후에 앱이 모바일 앱 백 엔드와 동기화하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-170">The app attempts to sync with the mobile app backend after login.</span></span> <span data-ttu-id="3f1bf-171">디버그 콘솔에 기록된 예외가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-171">Verify that no exceptions are logged in the debug console.</span></span>
4. <span data-ttu-id="3f1bf-172">(선택 사항) SQL Server 개체 탐색기 또는 Fiddler와 같은 REST 도구를 사용하여 업데이트된 데이터를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-172">(Optional) View the updated data using either SQL Server Object Explorer or a REST tool like Fiddler.</span></span> <span data-ttu-id="3f1bf-173">백 엔드 데이터베이스와 로컬 저장소의 데이터가 동기화된 것을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-173">Notice the data has been synchronized between the backend database and the local store.</span></span>

    <span data-ttu-id="3f1bf-174">데이터베이스와 로컬 저장소 간에 데이터가 동기화되었으며 앱의 연결이 끊어진 동안 추가한 항목을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-174">Notice the data has been synchronized between the database and the local store and contains the items you added while your app was disconnected.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3f1bf-175">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="3f1bf-175">Additional resources</span></span>
* <span data-ttu-id="3f1bf-176">[증분 동기화]</span><span class="sxs-lookup"><span data-stu-id="3f1bf-176">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="3f1bf-177">[Visual Studio Tools for Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="3f1bf-177">[Visual Studio Tools for Apache Cordova]</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f1bf-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3f1bf-178">Next steps</span></span>
* <span data-ttu-id="3f1bf-179">[오프라인 동기화 샘플]에서 충돌 해결과 같은 고급 오프라인 동기화 기능 검토</span><span class="sxs-lookup"><span data-stu-id="3f1bf-179">Review more advanced offline sync features such as conflict resolution in the [offline sync sample]</span></span>
* <span data-ttu-id="3f1bf-180">[API 설명서](https://azure.github.io/azure-mobile-apps-js-client)에서 오프라인 동기화 API 참조를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="3f1bf-180">Review the offline sync API reference in the [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

<!-- ##Summary -->

<!-- Images -->

<!-- URLs. -->
<span data-ttu-id="3f1bf-181">[Apache Cordova 빠른 시작]: app-service-mobile-cordova-get-started.md</span><span class="sxs-lookup"><span data-stu-id="3f1bf-181">[Apache Cordova quick start]: app-service-mobile-cordova-get-started.md</span></span>
<span data-ttu-id="3f1bf-182">[오프라인 동기화 샘플]: https://github.com/Azure-Samples/app-service-mobile-cordova-client-conflict-handling</span><span class="sxs-lookup"><span data-stu-id="3f1bf-182">[offline sync sample]: https://github.com/Azure-Samples/app-service-mobile-cordova-client-conflict-handling</span></span>
<span data-ttu-id="3f1bf-183">[증분 동기화]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="3f1bf-183">[Offline Data Sync in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md</span></span>
[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Adding Authentication]: app-service-mobile-cordova-get-started-users.md
[authentication]: app-service-mobile-cordova-get-started-users.md
[Work with the .NET backend server SDK for Azure Mobile Apps]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Visual Studio Community 2015]: http://www.visualstudio.com/
<span data-ttu-id="3f1bf-184">[Visual Studio Tools for Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx</span><span class="sxs-lookup"><span data-stu-id="3f1bf-184">[Visual Studio Tools for Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx</span></span>
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
