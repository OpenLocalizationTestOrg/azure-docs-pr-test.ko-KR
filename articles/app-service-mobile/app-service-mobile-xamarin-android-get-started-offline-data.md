---
title: "Azure 모바일 앱 (Xamarin Android)에 대 한 aaaEnable 오프 라인 동기화"
description: "자세한 내용은 방법 toouse 앱 서비스 모바일 앱 toocache 및 동기화의에서 오프 라인 데이터 Xamarin Android 응용 프로그램"
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
ms.openlocfilehash: 216ba76ae49f583273cc61b63114a415eca2477b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-xamarinandroid-mobile-app"></a><span data-ttu-id="42593-103">Xamarin.Android 모바일 앱에 대해 오프라인 동기화 사용</span><span class="sxs-lookup"><span data-stu-id="42593-103">Enable offline sync for your Xamarin.Android mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="42593-104">개요</span><span class="sxs-lookup"><span data-stu-id="42593-104">Overview</span></span>
<span data-ttu-id="42593-105">이 자습서에서는 Xamarin.Android에 대 한 Azure 모바일 앱의 hello 오프 라인 동기화 기능을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="42593-105">This tutorial introduces hello offline sync feature of Azure Mobile Apps for Xamarin.Android.</span></span> <span data-ttu-id="42593-106">오프 라인 동기화 최종 사용자가 toointeract 보기, 추가 또는 네트워크 연결이 없는 경우에 데이터-수정-모바일 앱을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="42593-106">Offline sync allows end users toointeract with a mobile app--viewing, adding, or modifying data--even when there is no network connection.</span></span> <span data-ttu-id="42593-107">변경 내용은 로컬 데이터베이스에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="42593-107">Changes are stored in a local database.</span></span>
<span data-ttu-id="42593-108">Hello 장치를 다시 온라인 상태가 되 면 이러한 변경 내용은 hello 원격 서비스와 동기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="42593-108">Once hello device is back online, these changes are synced with hello remote service.</span></span>

<span data-ttu-id="42593-109">Hello 자습서에서 hello 클라이언트 프로젝트를 업데이트 하면이 자습서에서는 [Xamarin Android 앱 만들기] toosupport hello Azure 모바일 앱의 오프 라인 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="42593-109">In this tutorial, you update hello client project from hello tutorial [Create a Xamarin Android app] toosupport hello offline features of Azure Mobile Apps.</span></span> <span data-ttu-id="42593-110">사용 하지 않는 경우 hello 퀵 스타트 서버 프로젝트를 다운로드, hello 데이터 액세스 확장 패키지 tooyour 프로젝트를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="42593-110">If you do not use hello downloaded quick start server project, you must add hello data access extension packages tooyour project.</span></span> <span data-ttu-id="42593-111">서버 확장 패키지에 대 한 자세한 내용은 참조 [Azure 모바일 앱에 대 한 hello.NET 백 엔드 서버 SDK에서 작동](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="42593-111">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="42593-112">hello 항목을 참조 하는 hello 오프 라인 동기화 기능에 대해 자세히 toolearn [Azure 모바일 앱에서 데이터 동기화를 오프 라인]합니다.</span><span class="sxs-lookup"><span data-stu-id="42593-112">toolearn more about hello offline sync feature, see hello topic [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="update-hello-client-app-toosupport-offline-features"></a><span data-ttu-id="42593-113">Hello 클라이언트 응용 프로그램 toosupport 오프 라인 기능 업데이트</span><span class="sxs-lookup"><span data-stu-id="42593-113">Update hello client app toosupport offline features</span></span>
<span data-ttu-id="42593-114">Azure 모바일 앱 오프 라인 기능을 사용 하면 로컬 데이터베이스와 toointeract 오프 라인 시나리오는 경우.</span><span class="sxs-lookup"><span data-stu-id="42593-114">Azure Mobile App offline features allow you toointeract with a local database when you are in an offline scenario.</span></span> <span data-ttu-id="42593-115">toouse 응용 프로그램에서 이러한 기능을 초기화 한 [SyncContext] tooa 로컬 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="42593-115">toouse these features in your app, you initialize a [SyncContext] tooa local store.</span></span> <span data-ttu-id="42593-116">그런 다음 [IMobileServiceSyncTable] [IMobileServiceSyncTable] hello 통해 테이블을 참조할 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="42593-116">Then reference your table through hello [IMobileServiceSyncTable][IMobileServiceSyncTable] interface.</span></span> <span data-ttu-id="42593-117">SQLite는 hello hello 장치의 로컬 저장소로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="42593-117">SQLite is used as hello local store on hello device.</span></span>

1. <span data-ttu-id="42593-118">Visual Studio에서 hello에서 완료 된 hello 프로젝트의 hello NuGet 패키지 관리자를 열고 [Xamarin Android 앱 만들기] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="42593-118">In Visual Studio, open hello NuGet package manager in hello project that you completed in hello [Create a Xamarin Android app] tutorial.</span></span>  <span data-ttu-id="42593-119">검색 하 고 hello 설치 **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="42593-119">Search for and install hello **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package.</span></span>
2. <span data-ttu-id="42593-120">Hello ToDoActivity.cs 파일을 열고 hello를 주석 처리 제거 `#define OFFLINE_SYNC_ENABLED` 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="42593-120">Open hello ToDoActivity.cs file and uncomment hello `#define OFFLINE_SYNC_ENABLED` definition.</span></span>
3. <span data-ttu-id="42593-121">Visual Studio에서 hello 키를 누릅니다. **F5** toorebuild 있고 실행된 hello 클라이언트 응용 프로그램 키입니다.</span><span class="sxs-lookup"><span data-stu-id="42593-121">In Visual Studio, press hello **F5** key toorebuild and run hello client app.</span></span> <span data-ttu-id="42593-122">hello 앱 hello 오프 라인 동기화를 사용 하도록 설정 하기 전과 같은 방법으로 작동 합니다. 그러나 hello 로컬 데이터베이스 이제 오프 라인 시나리오에서 사용할 수 있는 데이터로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="42593-122">hello app works hello same as it did before you enabled offline sync. However, hello local database is now populated with data that can be used in an offline scenario.</span></span>

## <span data-ttu-id="42593-123"><a name="update-sync"></a>Hello 백 엔드에서 hello 앱 toodisconnect 업데이트</span><span class="sxs-lookup"><span data-stu-id="42593-123"><a name="update-sync"></a>Update hello app toodisconnect from hello backend</span></span>
<span data-ttu-id="42593-124">이 섹션에서는 hello 연결 tooyour 모바일 앱 백 엔드 toosimulate 오프 라인 상황을 중단합니다.</span><span class="sxs-lookup"><span data-stu-id="42593-124">In this section, you break hello connection tooyour Mobile App backend toosimulate an offline situation.</span></span> <span data-ttu-id="42593-125">데이터 항목을 추가할 때 예외 처리기 hello 이러한 앱은 오프 라인 모드에서 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="42593-125">When you add data items, your exception handler tells you that hello app is in offline mode.</span></span> <span data-ttu-id="42593-126">이 상태에서 로컬 hello에 추가 된 새 항목 저장 하 고 hello 모바일 앱 백 엔드에서 푸시를 연결된 된 상태에서 실행 될 때 동기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="42593-126">In this state, new items added in hello local store and are synced to hello mobile app backend when a push is executed in a connected state.</span></span>

1. <span data-ttu-id="42593-127">ToDoActivity.cs hello 공유 프로젝트에 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="42593-127">Edit ToDoActivity.cs in hello shared project.</span></span> <span data-ttu-id="42593-128">변경 hello **applicationURL** toopoint tooan 잘못 된 URL:</span><span class="sxs-lookup"><span data-stu-id="42593-128">Change hello **applicationURL** toopoint tooan invalid URL:</span></span>

         const string applicationURL = @"https://your-service.azurewebsites.fail";

    <span data-ttu-id="42593-129">또한 wifi 및 hello 장치의 셀룰러 네트워크를 사용 하지 않도록 설정 하거나 비행기 모드를 사용 하 여 오프 라인 동작을 보여줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42593-129">You can also demonstrate offline behavior by disabling wifi and cellular networks on hello device or using airplane mode.</span></span>
2. <span data-ttu-id="42593-130">키를 눌러 **F5** hello 앱 toobuild 및 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="42593-130">Press **F5** toobuild and run hello app.</span></span> <span data-ttu-id="42593-131">응용 프로그램을 시작할 때 hello 새로 고침에 실패 했습니다. 동기화를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="42593-131">Notice your sync failed on refresh when hello app launched.</span></span>
3. <span data-ttu-id="42593-132">새 항목을 입력하고 **저장** 을 클릭할 때마다 푸시가 [CancelledByNetworkError] 상태로 실패하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="42593-132">Enter new items and notice that push fails with a [CancelledByNetworkError] status each time you click **Save**.</span></span> <span data-ttu-id="42593-133">그러나 새 할 일 항목 hello toohello 모바일 앱 백 엔드에서 푸시할 수 있습니다 때까지 hello 로컬 저장소에 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="42593-133">However, hello new todo items exist in hello local store until they can be pushed toohello mobile app backend.</span></span>  <span data-ttu-id="42593-134">프로덕션 hello 클라이언트 응용 프로그램 처럼 동작에 여전히 이러한 예외를 표시 하지 않는 경우 앱 toohello 모바일 앱 백 엔드 연결 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42593-134">In a production app, if you suppress these exceptions hello client app behaves as if it's still connected toohello mobile app backend.</span></span>
4. <span data-ttu-id="42593-135">Hello 응용 프로그램을 닫고 tooverify hello 새 항목이 만든 지속형된 toohello 로컬 저장소 지 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="42593-135">Close hello app and restart it tooverify that hello new items you created are persisted toohello local store.</span></span>
5. <span data-ttu-id="42593-136">(옵션) Visual Studio에서 **서버 탐색기**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="42593-136">(Optional) In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="42593-137">tooyour 데이터베이스 이동 **Azure**->**SQL 데이터베이스**합니다.</span><span class="sxs-lookup"><span data-stu-id="42593-137">Navigate tooyour database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="42593-138">데이터베이스를 마우스 오른쪽 단추로 클릭하고 **SQL Server 개체 탐색기에서 열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="42593-138">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="42593-139">이제 tooyour SQL 데이터베이스 테이블 및 해당 콘텐츠를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42593-139">Now you can browse tooyour SQL database table and its contents.</span></span> <span data-ttu-id="42593-140">Hello 백 엔드 데이터베이스의 hello 데이터가 변경 되지 않았음을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="42593-140">Verify that hello data in hello backend database has not changed.</span></span>
6. <span data-ttu-id="42593-141">(선택 사항) 양식에서 GET 쿼리를 사용 하 여 모바일 백 엔드 Fiddler 또는 우체부 tooquery 같은 REST 도구를 사용 하 여 `https://<your-mobile-app-backend-name>.azurewebsites.net/tables/TodoItem`합니다.</span><span class="sxs-lookup"><span data-stu-id="42593-141">(Optional) Use a REST tool such as Fiddler or Postman tooquery your mobile backend, using a GET query in the form `https://<your-mobile-app-backend-name>.azurewebsites.net/tables/TodoItem`.</span></span>

## <span data-ttu-id="42593-142"><a name="update-online-app"></a>모바일 앱 백 엔드 hello 앱 tooreconnect 업데이트</span><span class="sxs-lookup"><span data-stu-id="42593-142"><a name="update-online-app"></a>Update hello app tooreconnect your Mobile App backend</span></span>
<span data-ttu-id="42593-143">이 섹션에서는 앱 toohello 모바일 앱 백 엔드에서 hello를 다시 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="42593-143">In this section, reconnect hello app toohello mobile app backend.</span></span> <span data-ttu-id="42593-144">Hello 응용 프로그램을 처음 실행할 때 hello `OnCreate` 이벤트 처리기 호출 `OnRefreshItemsSelected`합니다.</span><span class="sxs-lookup"><span data-stu-id="42593-144">When you first run hello application, hello `OnCreate` event handler calls `OnRefreshItemsSelected`.</span></span> <span data-ttu-id="42593-145">이 메서드를 호출 `SyncAsync` toosync 로컬 hello 백 엔드 데이터베이스에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="42593-145">This method calls `SyncAsync` toosync your local store with hello backend database.</span></span>

1. <span data-ttu-id="42593-146">ToDoActivity.cs hello 공유 프로젝트에서 열고 hello의 변경 내용이 되돌릴 **applicationURL** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="42593-146">Open ToDoActivity.cs in hello shared project, and revert your change of hello **applicationURL** property.</span></span>
2. <span data-ttu-id="42593-147">키를 눌러 hello **F5** 키 toorebuild 및 실행된 hello 앱.</span><span class="sxs-lookup"><span data-stu-id="42593-147">Press hello **F5** key toorebuild and run hello app.</span></span> <span data-ttu-id="42593-148">hello 앱 로컬 변경 내용이와 동기화 때 hello 밀어넣기 및 끌어오기 작업을 사용 하 여 hello Azure 모바일 앱 백 엔드에서 `OnRefreshItemsSelected` 메서드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="42593-148">hello app syncs your local changes with hello Azure Mobile App backend using push and pull operations when hello `OnRefreshItemsSelected` method executes.</span></span>
3. <span data-ttu-id="42593-149">(선택 사항) 보기 hello SQL Server 개체 탐색기 또는 Fiddler와 같은 나머지 도구를 사용 하 여 데이터를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="42593-149">(Optional) View hello updated data using either SQL Server Object Explorer or a REST tool like Fiddler.</span></span> <span data-ttu-id="42593-150">공지 hello 데이터 hello Azure 모바일 앱 백 엔드 데이터베이스 hello 로컬 저장소와 동기화 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="42593-150">Notice hello data has been synchronized between hello Azure Mobile App backend database and hello local store.</span></span>
4. <span data-ttu-id="42593-151">Hello 응용 프로그램에서 hello 확인을 클릭 box 몇 가지 항목 toocomplete 옆에 있는 hello 로컬 저장소에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42593-151">In hello app, click hello check box beside a few items toocomplete them in hello local store.</span></span>

   <span data-ttu-id="42593-152">`CheckItem`호출 `SyncAsync` hello 모바일 앱 백 엔드와 toosync 각 완료 된 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="42593-152">`CheckItem` calls `SyncAsync` toosync each completed item with hello Mobile App backend.</span></span> <span data-ttu-id="42593-153">`SyncAsync` 는 푸시와 끌어오기를 둘 다 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="42593-153">`SyncAsync` calls both push and pull.</span></span> <span data-ttu-id="42593-154">**테이블에 대해 끌어오기를 실행할 때마다 해당 hello 클라이언트에 대 한 변경 내용이, 밀어넣기는 항상 자동으로 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="42593-154">**Whenever you execute a pull against a table that hello client has made changes to, a push is always executed automatically**.</span></span> <span data-ttu-id="42593-155">따라서 로컬 저장소의 모든 테이블 및 관계가 동기화된 상태로 유지될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42593-155">This ensures all tables in the local store along with relationships remain consistent.</span></span> <span data-ttu-id="42593-156">이 동작으로 예기치 않은 푸시가 발생할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42593-156">This behavior may result in an unexpected push.</span></span> <span data-ttu-id="42593-157">이 동작에 대한 자세한 내용은 [Azure 모바일 앱에서 데이터 동기화를 오프 라인]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="42593-157">For more information on this behavior, see [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="review-hello-client-sync-code"></a><span data-ttu-id="42593-158">Hello 클라이언트 동기화 코드를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="42593-158">Review hello client sync code</span></span>
<span data-ttu-id="42593-159">hello 자습서를 완료 하는 경우 다운로드 한 hello Xamarin 클라이언트 프로젝트 [Xamarin Android 앱 만들기] 이미 로컬 SQLite 데이터베이스를 사용 하 여 오프 라인 동기화를 지 원하는 코드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="42593-159">hello Xamarin client project that you downloaded when you completed hello tutorial [Create a Xamarin Android app] already contains code supporting offline synchronization using a local SQLite database.</span></span> <span data-ttu-id="42593-160">Hello 자습서 코드에 이미 포함 된 항목의 간략 한 개요는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="42593-160">Here is a brief overview of what is already included in hello tutorial code.</span></span> <span data-ttu-id="42593-161">Hello 기능의 개념적인 개요를 참조 하십시오. [Azure 모바일 앱에서 데이터 동기화를 오프 라인]합니다.</span><span class="sxs-lookup"><span data-stu-id="42593-161">For a conceptual overview of hello feature, see [Offline Data Sync in Azure Mobile Apps].</span></span>

* <span data-ttu-id="42593-162">모든 테이블 작업을 수행할 수 있습니다, 전에 hello 로컬 저장소를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="42593-162">Before any table operations can be performed, hello local store must be initialized.</span></span> <span data-ttu-id="42593-163">hello 로컬 저장소 데이터베이스 초기화 될 때 `ToDoActivity.OnCreate()` 실행 `ToDoActivity.InitLocalStoreAsync()`합니다.</span><span class="sxs-lookup"><span data-stu-id="42593-163">hello local store database is initialized when `ToDoActivity.OnCreate()` executes `ToDoActivity.InitLocalStoreAsync()`.</span></span> <span data-ttu-id="42593-164">이 메서드가 만드는 hello를 사용 하 여 로컬 SQLite 데이터베이스 `MobileServiceSQLiteStore` hello Azure 모바일 앱 클라이언트 SDK에서 제공 되는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="42593-164">This method creates a local SQLite database using hello `MobileServiceSQLiteStore` class provided by hello Azure Mobile Apps client SDK.</span></span>

    <span data-ttu-id="42593-165">hello `DefineTable` 메서드가 제공 하는 hello 형식의 hello 필드와 일치 하는 hello 로컬 저장소의 테이블을 만들어 `ToDoItem` 이 경우.</span><span class="sxs-lookup"><span data-stu-id="42593-165">hello `DefineTable` method creates a table in hello local store that matches hello fields in hello provided type, `ToDoItem` in this case.</span></span> <span data-ttu-id="42593-166">hello 형식 hello 원격 데이터베이스에 있는 모든 hello 열 tooinclude 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="42593-166">hello type doesn't have tooinclude all hello columns that are in hello remote database.</span></span> <span data-ttu-id="42593-167">가능한 toostore 열의 하위 집합만 이며</span><span class="sxs-lookup"><span data-stu-id="42593-167">It is possible toostore just a subset of columns.</span></span>

        // ToDoActivity.cs
        private async Task InitLocalStoreAsync()
        {
            // new code tooinitialize hello SQLite store
            string path = Path.Combine(System.Environment
                .GetFolderPath(System.Environment.SpecialFolder.Personal), localDbFilename);

            if (!File.Exists(path))
            {
                File.Create(path).Dispose();
            }

            var store = new MobileServiceSQLiteStore(path);
            store.DefineTable<ToDoItem>();

            // Uses hello default conflict handler, which fails on conflict
            // toouse a different conflict handler, pass a parameter tooInitializeAsync.
            // For more details, see http://go.microsoft.com/fwlink/?LinkId=521416.
            await client.SyncContext.InitializeAsync(store);
        }
* <span data-ttu-id="42593-168">hello `toDoTable` 소속 `ToDoActivity` hello의 `IMobileServiceSyncTable` 형식 대신 `IMobileServiceTable`합니다.</span><span class="sxs-lookup"><span data-stu-id="42593-168">hello `toDoTable` member of `ToDoActivity` is of hello `IMobileServiceSyncTable` type instead of `IMobileServiceTable`.</span></span> <span data-ttu-id="42593-169">hello IMobileServiceSyncTable 모든 만들기, 읽기, 업데이트 및 삭제 (CRUD) 테이블 작업 toohello 로컬 저장소 데이터베이스에 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="42593-169">hello IMobileServiceSyncTable directs all create, read, update, and delete (CRUD) table operations toohello local store database.</span></span>

    <span data-ttu-id="42593-170">변경 내용은 호출 하 여 Azure 모바일 앱 백 엔드에서 toohello는 전달 때 결정 `IMobileServiceSyncContext.PushAsync()`합니다.</span><span class="sxs-lookup"><span data-stu-id="42593-170">You decide when changes are pushed toohello Azure Mobile App backend by calling `IMobileServiceSyncContext.PushAsync()`.</span></span> <span data-ttu-id="42593-171">hello 동기화 상황에 맞는 사용 하면 추적 하 고 클라이언트 응용 프로그램은 수정 될 때 모든 테이블의 변경 내용 밀어넣기 테이블 관계 보존 `PushAsync` 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="42593-171">hello sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when `PushAsync` is called.</span></span>

    <span data-ttu-id="42593-172">제공 된 hello 코드 호출 `ToDoActivity.SyncAsync()` toosync hello todoitem 목록이 새로 고쳐진 또는 todoitem이 추가 되거나 완료 될 때마다 합니다.</span><span class="sxs-lookup"><span data-stu-id="42593-172">hello provided code calls `ToDoActivity.SyncAsync()` toosync whenever hello todoitem list is refreshed or a todoitem is added or completed.</span></span> <span data-ttu-id="42593-173">로컬 변경할 때마다 hello 코드 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="42593-173">hello code syncs after every local change.</span></span>

    <span data-ttu-id="42593-174">제공 된 hello 코드에서 개체의 모든 레코드 hello 원격 `TodoItem` 테이블을 쿼리하여 것 뿐만 아니라 가능한 toofilter 레코드는 쿼리 id 및 쿼리를 전달 하 여 너무`PushAsync`합니다.</span><span class="sxs-lookup"><span data-stu-id="42593-174">In hello provided code, all records in hello remote `TodoItem` table are queried, but it is also possible toofilter records by passing a query id and query too`PushAsync`.</span></span> <span data-ttu-id="42593-175">자세한 내용은 hello 섹션을 참조 하십시오. *증분 동기화* 에 [Azure 모바일 앱에서 데이터 동기화를 오프 라인]합니다.</span><span class="sxs-lookup"><span data-stu-id="42593-175">For more information, see hello section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps].</span></span>

        // ToDoActivity.cs
        private async Task SyncAsync()
        {
            try {
                await client.SyncContext.PushAsync();
                await toDoTable.PullAsync("allTodoItems", toDoTable.CreateQuery()); // query ID is used for incremental sync
            } catch (Java.Net.MalformedURLException) {
                CreateAndShowDialog (new Exception ("There was an error creating hello Mobile Service. Verify hello URL"), "Error");
            } catch (Exception e) {
                CreateAndShowDialog (e, "Error");
            }
        }

## <a name="additional-resources"></a><span data-ttu-id="42593-176">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="42593-176">Additional Resources</span></span>
* <span data-ttu-id="42593-177">[Azure 모바일 앱에서 데이터 동기화를 오프 라인]</span><span class="sxs-lookup"><span data-stu-id="42593-177">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="42593-178">[Azure Mobile Apps .NET SDK 사용 방법][8]</span><span class="sxs-lookup"><span data-stu-id="42593-178">[Azure Mobile Apps .NET SDK HOWTO][8]</span></span>

<!-- URLs. -->
[Xamarin Android 앱 만들기]: ../app-service-mobile-xamarin-android-get-started.md
[Azure 모바일 앱에서 데이터 동기화를 오프 라인]: ../app-service-mobile-offline-data-sync.md

<!-- Images -->

<!-- URLs. -->
[Xamarin Android 앱 만들기]: app-service-mobile-xamarin-android-get-started.md
[Azure 모바일 앱에서 오프라인 데이터 동기화]: app-service-mobile-offline-data-sync.md
[Xamarin Studio]: http://xamarin.com/download
[Xamarin extension]: http://xamarin.com/visual-studio
[SyncContext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient.synccontext(v=azure.10).aspx
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
