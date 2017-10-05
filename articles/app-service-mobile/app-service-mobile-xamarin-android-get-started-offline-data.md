---
title: "Azure 모바일 앱(Xamarin.Android)에 대해 오프라인 동기화 사용"
description: "앱 서비스 모바일 앱을 사용하여 Xamarin 안드로이드 응용 프로그램에서 오프라인 데이터를 캐시 및 동기화하는 방법을 알아봅니다."
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 91d59e4b-abaa-41f4-80cf-ee7933b32568
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 471433c7ef2f6f128210ed145f685b42b44eea92
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="enable-offline-sync-for-your-xamarinandroid-mobile-app"></a><span data-ttu-id="8ba78-103">Xamarin.Android 모바일 앱에 대해 오프라인 동기화 사용</span><span class="sxs-lookup"><span data-stu-id="8ba78-103">Enable offline sync for your Xamarin.Android mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="8ba78-104">개요</span><span class="sxs-lookup"><span data-stu-id="8ba78-104">Overview</span></span>
<span data-ttu-id="8ba78-105">이 자습서에서는 Xamarin.Android용 Azure 모바일 앱의 오프라인 동기화 기능을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-105">This tutorial introduces the offline sync feature of Azure Mobile Apps for Xamarin.Android.</span></span> <span data-ttu-id="8ba78-106">오프라인 동기화를 사용하면 최종 사용자는 네트워크에 연결되어 있지 않을 때도 모바일 앱과 데이터 보기, 추가 또는 수정과 같은 상호 작용을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-106">Offline sync allows end users to interact with a mobile app--viewing, adding, or modifying data--even when there is no network connection.</span></span> <span data-ttu-id="8ba78-107">변경 내용은 로컬 데이터베이스에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-107">Changes are stored in a local database.</span></span>
<span data-ttu-id="8ba78-108">장치가 다시 온라인 상태가 되면 이러한 변경 내용이 원격 서비스와 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-108">Once the device is back online, these changes are synced with the remote service.</span></span>

<span data-ttu-id="8ba78-109">이 자습서에서는 자습서 [Xamarin Android 앱 만들기]에서 클라이언트 프로젝트를 업데이트하여 Azure Mobile App의 오프라인 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-109">In this tutorial, you update the client project from the tutorial [Create a Xamarin Android app] to support the offline features of Azure Mobile Apps.</span></span> <span data-ttu-id="8ba78-110">다운로드한 빠른 시작 서버 프로젝트를 사용하지 않는 경우 프로젝트에 데이터 액세스 확장 패키지를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-110">If you do not use the downloaded quick start server project, you must add the data access extension packages to your project.</span></span> <span data-ttu-id="8ba78-111">서버 확장 패키지에 대한 자세한 내용은 [Azure 모바일 앱용 .NET 백 엔드 서버 SDK 사용](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8ba78-111">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="8ba78-112">오프라인 동기화 기능에 대한 자세한 내용은 [증분 동기화]항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8ba78-112">To learn more about the offline sync feature, see the topic [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="update-the-client-app-to-support-offline-features"></a><span data-ttu-id="8ba78-113">오프라인 기능을 지원하도록 클라이언트 앱 업데이트</span><span class="sxs-lookup"><span data-stu-id="8ba78-113">Update the client app to support offline features</span></span>
<span data-ttu-id="8ba78-114">Azure 모바일 앱 오프라인 기능을 사용하면 오프라인 시나리오에서 로컬 데이터베이스를 조작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-114">Azure Mobile App offline features allow you to interact with a local database when you are in an offline scenario.</span></span> <span data-ttu-id="8ba78-115">앱에서 이러한 기능을 사용하려면 로컬 저장소에서 [SyncContext]를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-115">To use these features in your app, you initialize a [SyncContext] to a local store.</span></span> <span data-ttu-id="8ba78-116">그런 다음 [IMobileServiceSyncTable][IMobileServiceSyncTable] 인터페이스를 통해 테이블을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-116">Then reference your table through the [IMobileServiceSyncTable][IMobileServiceSyncTable] interface.</span></span> <span data-ttu-id="8ba78-117">SQLite는 장치의 로컬 저장소로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-117">SQLite is used as the local store on the device.</span></span>

1. <span data-ttu-id="8ba78-118">Visual Studio에서 [Xamarin Android 앱 만들기] 자습서에서 완료한 프로젝트에서 NuGet 패키지 관리자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-118">In Visual Studio, open the NuGet package manager in the project that you completed in the [Create a Xamarin Android app] tutorial.</span></span>  <span data-ttu-id="8ba78-119">**Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet 패키지를 검색하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-119">Search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package.</span></span>
2. <span data-ttu-id="8ba78-120">ToDoActivity.cs 파일을 열고 `#define OFFLINE_SYNC_ENABLED` 정의의 주석 처리를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-120">Open the ToDoActivity.cs file and uncomment the `#define OFFLINE_SYNC_ENABLED` definition.</span></span>
3. <span data-ttu-id="8ba78-121">Visual Studio에서 **F5** 키를 눌러 클라이언트 앱을 다시 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-121">In Visual Studio, press the **F5** key to rebuild and run the client app.</span></span> <span data-ttu-id="8ba78-122">오프라인 동기화를 활성화하기 전에 수행한 것과 동일하게 앱이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-122">The app works the same as it did before you enabled offline sync.</span></span> <span data-ttu-id="8ba78-123">그러나 로컬 데이터베이스는 이제 오프라인 시나리오에서 사용할 수 있는 데이터로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-123">However, the local database is now populated with data that can be used in an offline scenario.</span></span>

## <span data-ttu-id="8ba78-124"><a name="update-sync"></a>앱을 업데이트하여 백 엔드에서 분리</span><span class="sxs-lookup"><span data-stu-id="8ba78-124"><a name="update-sync"></a>Update the app to disconnect from the backend</span></span>
<span data-ttu-id="8ba78-125">이 섹션에서는 모바일 앱 백 엔드에 대한 연결을 끊고 오프라인 상황을 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-125">In this section, you break the connection to your Mobile App backend to simulate an offline situation.</span></span> <span data-ttu-id="8ba78-126">데이터 항목을 추가하면 예외 처리기는 앱이 오프라인 모드임을 사용자에게 알립니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-126">When you add data items, your exception handler tells you that the app is in offline mode.</span></span> <span data-ttu-id="8ba78-127">이 상태에서 로컬 저장소에 추가된 새 항목은 푸시가 연결된 상태에서 실행될 경우 Mobile App 백 엔드에 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-127">In this state, new items added in the local store and are synced to the mobile app backend when a push is executed in a connected state.</span></span>

1. <span data-ttu-id="8ba78-128">공유 프로젝트에서 ToDoActivity.cs를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-128">Edit ToDoActivity.cs in the shared project.</span></span> <span data-ttu-id="8ba78-129">잘못된 URL을 가리키도록 **applicationURL**을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-129">Change the **applicationURL** to point to an invalid URL:</span></span>

         const string applicationURL = @"https://your-service.azurewebsites.fail";

    <span data-ttu-id="8ba78-130">장치에서 Wi-Fi 및 셀룰러 네트워크를 사용하지 않도록 설정하여 오프라인 동작을 시연하거나 비행기 모드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-130">You can also demonstrate offline behavior by disabling wifi and cellular networks on the device or using airplane mode.</span></span>
2. <span data-ttu-id="8ba78-131">**F5** 를 눌러 응용 프로그램을 빌드 및 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-131">Press **F5** to build and run the app.</span></span> <span data-ttu-id="8ba78-132">앱을 시작하는 경우 동기화는 새로 고침에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-132">Notice your sync failed on refresh when the app launched.</span></span>
3. <span data-ttu-id="8ba78-133">새 항목을 입력하고 **저장** 을 클릭할 때마다 푸시가 [CancelledByNetworkError] 상태로 실패하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-133">Enter new items and notice that push fails with a [CancelledByNetworkError] status each time you click **Save**.</span></span> <span data-ttu-id="8ba78-134">그러나 새 todo 항목은 모바일 앱 백 엔드에 푸시할 수 있을 때까지 로컬 저장소에 위치합니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-134">However, the new todo items exist in the local store until they can be pushed to the mobile app backend.</span></span>  <span data-ttu-id="8ba78-135">프로덕션 앱에서 이러한 예외를 무시하는 경우 클라이언트 앱은 모바일 앱 백 엔드에 연결된 것처럼 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-135">In a production app, if you suppress these exceptions the client app behaves as if it's still connected to the mobile app backend.</span></span>
4. <span data-ttu-id="8ba78-136">앱을 닫았다가 다시 시작하여 만든 새 항목이 로컬 저장소에 유지되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-136">Close the app and restart it to verify that the new items you created are persisted to the local store.</span></span>
5. <span data-ttu-id="8ba78-137">(옵션) Visual Studio에서 **서버 탐색기**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-137">(Optional) In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="8ba78-138">**Azure**->**SQL Databases**에 있는 데이터베이스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-138">Navigate to your database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="8ba78-139">데이터베이스를 마우스 오른쪽 단추로 클릭하고 **SQL Server 개체 탐색기에서 열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-139">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="8ba78-140">이제 SQL 데이터베이스 테이블 및 콘텐츠를 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-140">Now you can browse to your SQL database table and its contents.</span></span> <span data-ttu-id="8ba78-141">백 엔드 데이터베이스의 데이터가 변경되지 않은 것을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-141">Verify that the data in the backend database has not changed.</span></span>
6. <span data-ttu-id="8ba78-142">(옵션) Fiddler 또는 Postman과 같은 REST 도구를 사용하여 `https://<your-mobile-app-backend-name>.azurewebsites.net/tables/TodoItem`형식의 GET 쿼리를 통해 모바일 백 엔드를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-142">(Optional) Use a REST tool such as Fiddler or Postman to query your mobile backend, using a GET query in the form `https://<your-mobile-app-backend-name>.azurewebsites.net/tables/TodoItem`.</span></span>

## <span data-ttu-id="8ba78-143"><a name="update-online-app"></a>모바일 앱 백 엔드를 다시 연결하도록 앱 업데이트</span><span class="sxs-lookup"><span data-stu-id="8ba78-143"><a name="update-online-app"></a>Update the app to reconnect your Mobile App backend</span></span>
<span data-ttu-id="8ba78-144">이 섹션에서는 앱을 Mobile App 백 엔드에 다시 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-144">In this section, reconnect the app to the mobile app backend.</span></span> <span data-ttu-id="8ba78-145">응용 프로그램을 처음 실행하는 경우 `OnCreate` 이벤트 처리기는 `OnRefreshItemsSelected`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-145">When you first run the application, the `OnCreate` event handler calls `OnRefreshItemsSelected`.</span></span> <span data-ttu-id="8ba78-146">차례로 `SyncAsync`가 호출되고 백 엔드 데이터베이스와 로컬 저장소가 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-146">This method calls `SyncAsync` to sync your local store with the backend database.</span></span>

1. <span data-ttu-id="8ba78-147">공유 프로젝트에서 ToDoActivity.cs를 열고 **applicationURL**의 변경 내용을 되돌립니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-147">Open ToDoActivity.cs in the shared project, and revert your change of the **applicationURL** property.</span></span>
2. <span data-ttu-id="8ba78-148">**F5** 를 눌러 앱을 다시 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-148">Press the **F5** key to rebuild and run the app.</span></span> <span data-ttu-id="8ba78-149">앱은 푸시 및 끌어오기 작업을 사용하여 `OnRefreshItemsSelected` 메서드가 실행되면 로컬 변경 내용을 Azure Mobile App 백 엔드와 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-149">The app syncs your local changes with the Azure Mobile App backend using push and pull operations when the `OnRefreshItemsSelected` method executes.</span></span>
3. <span data-ttu-id="8ba78-150">(선택 사항) SQL Server 개체 탐색기 또는 Fiddler와 같은 REST 도구를 사용하여 업데이트된 데이터를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-150">(Optional) View the updated data using either SQL Server Object Explorer or a REST tool like Fiddler.</span></span> <span data-ttu-id="8ba78-151">Azure 모바일 앱 백 엔드 데이터베이스와 로컬 저장소 간에 데이터는 동기화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-151">Notice the data has been synchronized between the Azure Mobile App backend database and the local store.</span></span>
4. <span data-ttu-id="8ba78-152">앱에서 로컬 저장소에서 완료할 몇 개 항목 옆의 확인란을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-152">In the app, click the check box beside a few items to complete them in the local store.</span></span>

   <span data-ttu-id="8ba78-153">`CheckItem`은 `SyncAsync`를 호출하여 Mobile App 백 엔드와 전체 항목을 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-153">`CheckItem` calls `SyncAsync` to sync each completed item with the Mobile App backend.</span></span> <span data-ttu-id="8ba78-154">`SyncAsync` 는 푸시와 끌어오기를 둘 다 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-154">`SyncAsync` calls both push and pull.</span></span> <span data-ttu-id="8ba78-155">**클라이언트가 변경한 테이블에 대해 끌어오기를 실행할 때마다 푸시도 항상 자동으로 실행됩니다**.</span><span class="sxs-lookup"><span data-stu-id="8ba78-155">**Whenever you execute a pull against a table that the client has made changes to, a push is always executed automatically**.</span></span> <span data-ttu-id="8ba78-156">따라서 로컬 저장소의 모든 테이블 및 관계가 동기화된 상태로 유지될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-156">This ensures all tables in the local store along with relationships remain consistent.</span></span> <span data-ttu-id="8ba78-157">이 동작으로 예기치 않은 푸시가 발생할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-157">This behavior may result in an unexpected push.</span></span> <span data-ttu-id="8ba78-158">이 동작에 대한 자세한 내용은 [증분 동기화]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8ba78-158">For more information on this behavior, see [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="review-the-client-sync-code"></a><span data-ttu-id="8ba78-159">클라이언트 동기화 코드 검토</span><span class="sxs-lookup"><span data-stu-id="8ba78-159">Review the client sync code</span></span>
<span data-ttu-id="8ba78-160">자습서 [Xamarin Android 앱 만들기] 를 완료한 경우 다운로드한 Xamarin 클라이언트 프로젝트는 로컬 SQLite 데이터베이스를 사용하여 오프라인 동기화를 지원하는 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-160">The Xamarin client project that you downloaded when you completed the tutorial [Create a Xamarin Android app] already contains code supporting offline synchronization using a local SQLite database.</span></span> <span data-ttu-id="8ba78-161">이미 자습서 코드에 포함된 내용에 대한 간략한 개요입니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-161">Here is a brief overview of what is already included in the tutorial code.</span></span> <span data-ttu-id="8ba78-162">기능의 개념적 개요는 [증분 동기화]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8ba78-162">For a conceptual overview of the feature, see [Offline Data Sync in Azure Mobile Apps].</span></span>

* <span data-ttu-id="8ba78-163">모든 테이블 작업을 수행하려면 먼저 로컬 저장소를 초기화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-163">Before any table operations can be performed, the local store must be initialized.</span></span> <span data-ttu-id="8ba78-164">`ToDoActivity.OnCreate()`가 `ToDoActivity.InitLocalStoreAsync()`를 실행하는 경우 로컬 저장소 데이터베이스를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-164">The local store database is initialized when `ToDoActivity.OnCreate()` executes `ToDoActivity.InitLocalStoreAsync()`.</span></span> <span data-ttu-id="8ba78-165">이 메서드는 Azure Mobile App 클라이언트 SDK에서 제공하는 `MobileServiceSQLiteStore` 클래스를 사용하여 로컬 SQLite 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-165">This method creates a local SQLite database using the `MobileServiceSQLiteStore` class provided by the Azure Mobile Apps client SDK.</span></span>

    <span data-ttu-id="8ba78-166">`DefineTable` 메서드는 제공된 형식(이 경우 `ToDoItem`)의 필드와 일치하는 테이블을 로컬 저장소에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-166">The `DefineTable` method creates a table in the local store that matches the fields in the provided type, `ToDoItem` in this case.</span></span> <span data-ttu-id="8ba78-167">이 형식은 원격 데이터베이스에 있는 열을 모두 포함하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-167">The type doesn't have to include all the columns that are in the remote database.</span></span> <span data-ttu-id="8ba78-168">열의 하위 집합 저장은 불가능합니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-168">It is possible to store just a subset of columns.</span></span>

        // ToDoActivity.cs
        private async Task InitLocalStoreAsync()
        {
            // new code to initialize the SQLite store
            string path = Path.Combine(System.Environment
                .GetFolderPath(System.Environment.SpecialFolder.Personal), localDbFilename);

            if (!File.Exists(path))
            {
                File.Create(path).Dispose();
            }

            var store = new MobileServiceSQLiteStore(path);
            store.DefineTable<ToDoItem>();

            // Uses the default conflict handler, which fails on conflict
            // To use a different conflict handler, pass a parameter to InitializeAsync.
            // For more details, see http://go.microsoft.com/fwlink/?LinkId=521416.
            await client.SyncContext.InitializeAsync(store);
        }
* <span data-ttu-id="8ba78-169">`ToDoActivity`의 `toDoTable` 멤버는 `IMobileServiceTable` 대신 `IMobileServiceSyncTable` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-169">The `toDoTable` member of `ToDoActivity` is of the `IMobileServiceSyncTable` type instead of `IMobileServiceTable`.</span></span> <span data-ttu-id="8ba78-170">IMobileServiceSyncTable은 모든 만들기, 읽기, 업데이트 및 삭제(CRUD) 테이블 작업을 로컬 저장소 데이터베이스로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-170">The IMobileServiceSyncTable directs all create, read, update, and delete (CRUD) table operations to the local store database.</span></span>

    <span data-ttu-id="8ba78-171">`IMobileServiceSyncContext.PushAsync()`를 호출하여 변경 내용이 Azure Mobile App 백 엔드로 푸시될 때를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-171">You decide when changes are pushed to the Azure Mobile App backend by calling `IMobileServiceSyncContext.PushAsync()`.</span></span> <span data-ttu-id="8ba78-172">동기화 컨텍스트를 사용하면 모든 테이블의 변경 내용을 추적하고 밀어넣어서 테이블 관계를 보존할 수 있습니다. `PushAsync`를 호출하는 경우 클라이언트 앱을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-172">The sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when `PushAsync` is called.</span></span>

    <span data-ttu-id="8ba78-173">제공되는 코드는 `ToDoActivity.SyncAsync()` 를 호출하여 todoitem목록이 새로 고쳐지거나 todoitem이 더해지거나 완료될 때마다 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-173">The provided code calls `ToDoActivity.SyncAsync()` to sync whenever the todoitem list is refreshed or a todoitem is added or completed.</span></span> <span data-ttu-id="8ba78-174">로컬 변경이 수행될 때마다 코드가 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-174">The code syncs after every local change.</span></span>

    <span data-ttu-id="8ba78-175">제공된 코드에서 원격 `TodoItem` 테이블에 있는 모든 레코드를 쿼리하지만 쿼리 ID 및 쿼리를 `PushAsync`로 전달하여 레코드를 필터링할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ba78-175">In the provided code, all records in the remote `TodoItem` table are queried, but it is also possible to filter records by passing a query id and query to `PushAsync`.</span></span> <span data-ttu-id="8ba78-176">자세한 내용은 *Azure 모바일 앱에서 오프라인 데이터 동기화* 에서 [증분 동기화]섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8ba78-176">For more information, see the section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps].</span></span>

        // ToDoActivity.cs
        private async Task SyncAsync()
        {
            try {
                await client.SyncContext.PushAsync();
                await toDoTable.PullAsync("allTodoItems", toDoTable.CreateQuery()); // query ID is used for incremental sync
            } catch (Java.Net.MalformedURLException) {
                CreateAndShowDialog (new Exception ("There was an error creating the Mobile Service. Verify the URL"), "Error");
            } catch (Exception e) {
                CreateAndShowDialog (e, "Error");
            }
        }

## <a name="additional-resources"></a><span data-ttu-id="8ba78-177">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="8ba78-177">Additional Resources</span></span>
* <span data-ttu-id="8ba78-178">[증분 동기화]</span><span class="sxs-lookup"><span data-stu-id="8ba78-178">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="8ba78-179">[Azure Mobile Apps .NET SDK 사용 방법][8]</span><span class="sxs-lookup"><span data-stu-id="8ba78-179">[Azure Mobile Apps .NET SDK HOWTO][8]</span></span>

<!-- URLs. -->
<span data-ttu-id="8ba78-180">[Xamarin Android 앱 만들기]: ../app-service-mobile-xamarin-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="8ba78-180">[Create a Xamarin Android app]: ../app-service-mobile-xamarin-android-get-started.md</span></span>
<span data-ttu-id="8ba78-181">[증분 동기화]: ../app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="8ba78-181">[Offline Data Sync in Azure Mobile Apps]: ../app-service-mobile-offline-data-sync.md</span></span>

<!-- Images -->

<!-- URLs. -->
<span data-ttu-id="8ba78-182">[Xamarin Android 앱 만들기]: app-service-mobile-xamarin-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="8ba78-182">[Create a Xamarin Android app]: app-service-mobile-xamarin-android-get-started.md</span></span>
<span data-ttu-id="8ba78-183">[Azure 모바일 앱에서 오프라인 데이터 동기화]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="8ba78-183">[Offline Data Sync in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md</span></span>
[Xamarin Studio]: http://xamarin.com/download
[Xamarin extension]: http://xamarin.com/visual-studio
<span data-ttu-id="8ba78-184">[SyncContext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient.synccontext(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="8ba78-184">[SyncContext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient.synccontext(v=azure.10).aspx</span></span>
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
