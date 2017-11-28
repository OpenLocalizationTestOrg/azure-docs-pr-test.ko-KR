---
title: "Azure 모바일 앱 (Xamarin.Forms)에 대 한 오프 라인 동기화 aaaEnable | Microsoft Docs"
description: "자세한 내용은 방법 toouse 앱 서비스 모바일 앱 toocache 및 동기화 오프 라인 응용 프로그램에서 데이터 Xamarin.Forms"
documentationcenter: xamarin
author: ggailey777
manager: yochayk
editor: 
services: app-service\mobile
ms.assetid: acf0f874-3ea5-4410-bd22-b0e72140f3b5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/04/2016
ms.author: glenga
ms.openlocfilehash: 4b41404fc9507e82068fdf8aa612d57cbeb366bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-xamarinforms-mobile-app"></a><span data-ttu-id="8ad56-103">Xamarin.Forms 모바일 앱에 대해 오프라인 동기화 사용</span><span class="sxs-lookup"><span data-stu-id="8ad56-103">Enable offline sync for your Xamarin.Forms mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="8ad56-104">개요</span><span class="sxs-lookup"><span data-stu-id="8ad56-104">Overview</span></span>
<span data-ttu-id="8ad56-105">이 자습서에서는 Xamarin.Forms에 대 한 Azure 모바일 앱의 hello 오프 라인 동기화 기능을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-105">This tutorial introduces hello offline sync feature of Azure Mobile Apps for Xamarin.Forms.</span></span> <span data-ttu-id="8ad56-106">오프라인 동기화를 사용하면 최종 사용자는 네트워크에 연결되어 있지 않을 때도 모바일 앱과 데이터 보기, 추가 또는 수정과 같은 상호 작용을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-106">Offline sync allows end users to interact with a mobile app--viewing, adding, or modifying data--even when there is no network connection.</span></span> <span data-ttu-id="8ad56-107">변경 내용은 로컬 데이터베이스에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-107">Changes are stored in a local database.</span></span> <span data-ttu-id="8ad56-108">Hello 장치를 다시 온라인 상태가 되 면 이러한 변경 내용은 hello 원격 서비스와 동기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-108">Once hello device is back online, these changes are synced with hello remote service.</span></span>

<span data-ttu-id="8ad56-109">이 자습서는 자습서 [Xamarin iOS 앱 만들기]를 완료할 때 만드는 모바일 앱에 대 한 hello Xamarin.Forms 퀵 스타트 솔루션을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-109">This tutorial is based on hello Xamarin.Forms quickstart solution for Mobile Apps that you create when you complete the tutorial [Create a Xamarin iOS app].</span></span> <span data-ttu-id="8ad56-110">Xamarin.Forms에 대 한 퀵 스타트 솔루션 hello hello 코드 toosupport 수 오프 라인 동기화 toobe 사용 하도록 설정 하기만 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-110">hello quickstart solution for Xamarin.Forms contains hello code toosupport offline sync, which just needs toobe enabled.</span></span> <span data-ttu-id="8ad56-111">이 자습서에서는 Azure 모바일 앱의 hello 오프 라인 기능에 hello 퀵 스타트 솔루션 tooturn을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-111">In this tutorial, you update hello quickstart solution tooturn on hello offline features of Azure Mobile Apps.</span></span> <span data-ttu-id="8ad56-112">Hello 오프 라인 관련 코드가 hello 앱에도 강조 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-112">We also highlight hello offline-specific code in hello app.</span></span> <span data-ttu-id="8ad56-113">다운로드 한 hello 퀵 스타트 솔루션을 사용 하지 않으면 hello 데이터 액세스 확장 패키지 tooyour 프로젝트를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-113">If you do not use hello downloaded quickstart solution, you must add hello data access extension packages tooyour project.</span></span> <span data-ttu-id="8ad56-114">서버 확장 패키지에 대 한 자세한 내용은 참조 [Azure 모바일 앱에 대 한 hello.NET 백 엔드 서버 SDK에서 작동][1]합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-114">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps][1].</span></span>

<span data-ttu-id="8ad56-115">hello 항목을 참조 하는 hello 오프 라인 동기화 기능에 대해 자세히 toolearn [Azure 모바일 앱에서 데이터 동기화를 오프 라인][2]합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-115">toolearn more about hello offline sync feature, see hello topic [Offline Data Sync in Azure Mobile Apps][2].</span></span>

## <a name="enable-offline-sync-functionality-in-hello-quickstart-solution"></a><span data-ttu-id="8ad56-116">Hello 퀵 스타트 솔루션의 오프 라인 동기화 기능을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="8ad56-116">Enable offline sync functionality in hello quickstart solution</span></span>
<span data-ttu-id="8ad56-117">hello 오프 라인 동기화 코드는 C# 전처리기 지시문을 사용 하 여 hello 프로젝트에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-117">hello offline sync code is included in hello project by using C# preprocessor directives.</span></span> <span data-ttu-id="8ad56-118">Hello 때 **오프 라인\_동기화\_ENABLED** 기호를 정의 이러한 코드 경로 hello 빌드에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-118">When hello **OFFLINE\_SYNC\_ENABLED** symbol is defined, these code paths are included in hello build.</span></span> <span data-ttu-id="8ad56-119">Windows 앱 용 hello SQLite 플랫폼도 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-119">For Windows apps, you must also install hello SQLite platform.</span></span>

1. <span data-ttu-id="8ad56-120">Visual Studio에서 hello 솔루션 탐색기에서 > **솔루션에 대 한 NuGet 패키지 관리...** 다음 검색 하 고 설치는 **Microsoft.Azure.Mobile.Client.SQLiteStore** hello 솔루션의 모든 프로젝트에 대 한 NuGet 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-120">In Visual Studio, right-click hello solution > **Manage NuGet Packages for Solution...**, then search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package for all projects in hello solution.</span></span>
2. <span data-ttu-id="8ad56-121">Hello 솔루션 탐색기에서에서 사용 하 여 hello 프로젝트에서 hello TodoItemManager.cs 파일을 열어 **휴대용** 이식 가능한 클래스 라이브러리 프로젝트는 hello 이름에 전처리기 지시문 다음 hello 그런 다음 아래:</span><span class="sxs-lookup"><span data-stu-id="8ad56-121">In hello Solution Explorer, open hello TodoItemManager.cs file from hello project with **Portable** in hello name, which is Portable Class Library project, then uncomment hello following preprocessor directive:</span></span>

        #define OFFLINE_SYNC_ENABLED
3. <span data-ttu-id="8ad56-122">(선택 사항) toosupport Windows 장치 hello SQLite 런타임 패키지를 다음 중 하나를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-122">(Optional) toosupport Windows devices, install one of hello following SQLite runtime packages:</span></span>

   * <span data-ttu-id="8ad56-123">**Windows 8.1 런타임:** [Windows 8.1][3]용 SQLite를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-123">**Windows 8.1 Runtime:** Install [SQLite for Windows 8.1][3].</span></span>
   * <span data-ttu-id="8ad56-124">**Windows Phone 8.1:** [Windows Phone 8.1][4]용 SQLite를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-124">**Windows Phone 8.1:** Install [SQLite for Windows Phone 8.1][4].</span></span>
   * <span data-ttu-id="8ad56-125">**유니버설 Windows 플랫폼** 설치 [유니버설 Windows 유니버설 hello에 대 한 SQLite][5]합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-125">**Universal Windows Platform** Install [SQLite for hello Universal Windows Universal][5].</span></span>

     <span data-ttu-id="8ad56-126">Hello 퀵 스타트 유니버설 Windows 프로젝트를 포함 하지 않으면 있지만 Xamarin forms hello 유니버설 Windows 플랫폼은 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-126">Although hello quickstart does not contain a Universal Windows project, hello Universal Windows platform is supported with Xamarin Forms.</span></span>
4. <span data-ttu-id="8ad56-127">(선택 사항) 각 Windows 앱 프로젝트에서 마우스 오른쪽 단추로 클릭 **참조** > **참조 추가...** , hello 확장 **Windows** 폴더 > **확장**합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-127">(Optional) In each Windows app project, right-click **References** > **Add Reference...**, expand hello **Windows** folder > **Extensions**.</span></span>
    <span data-ttu-id="8ad56-128">적절 한 hello를 사용 하도록 설정 **Windows 용 SQLite** hello 함께 SDK **Visual c + + 2013 런타임 for Windows** SDK입니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-128">Enable hello appropriate **SQLite for Windows** SDK along with hello **Visual C++ 2013 Runtime for Windows** SDK.</span></span>
    <span data-ttu-id="8ad56-129">hello SQLite SDK 이름은 조금씩 각 Windows 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-129">hello SQLite SDK names vary slightly with each Windows platform.</span></span>

## <a name="review-hello-client-sync-code"></a><span data-ttu-id="8ad56-130">Hello 클라이언트 동기화 코드를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-130">Review hello client sync code</span></span>
<span data-ttu-id="8ad56-131">Hello 자습서 코드 hello 내에 이미 포함 된 항목의 간략 한 개요는 다음과 같습니다 `#if OFFLINE_SYNC_ENABLED` 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-131">Here is a brief overview of what is already included in hello tutorial code inside hello `#if OFFLINE_SYNC_ENABLED` directives.</span></span> <span data-ttu-id="8ad56-132">오프 라인 동기화 기능은 hello 이식 가능한 클래스 라이브러리 프로젝트의 hello TodoItemManager.cs 프로젝트 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-132">The offline sync functionality is in hello TodoItemManager.cs project file in hello Portable Class Library project.</span></span> <span data-ttu-id="8ad56-133">Hello 기능의 개념적인 개요를 참조 하십시오. [Azure 모바일 앱에서 데이터 동기화 오프 라인][2]합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-133">For a conceptual overview of hello feature, see [Offline Data Sync in Azure Mobile Apps][2].</span></span>

* <span data-ttu-id="8ad56-134">모든 테이블 작업을 수행할 수 있습니다, 전에 hello 로컬 저장소를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-134">Before any table operations can be performed, hello local store must be initialized.</span></span> <span data-ttu-id="8ad56-135">hello 로컬 저장소 데이터베이스에서에서 초기화 hello **TodoItemManager** 코드 다음 hello를 사용 하 여 클래스 생성자:</span><span class="sxs-lookup"><span data-stu-id="8ad56-135">hello local store database is initialized in hello **TodoItemManager** class constructor by using hello following code:</span></span>

        var store = new MobileServiceSQLiteStore(OfflineDbPath);
        store.DefineTable<TodoItem>();

        //Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
        this.client.SyncContext.InitializeAsync(store);

        this.todoTable = client.GetSyncTable<TodoItem>();

    <span data-ttu-id="8ad56-136">이 코드에서는 hello를 사용 하 여 새 로컬 SQLite 데이터베이스 **MobileServiceSQLiteStore** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-136">This code creates a new local SQLite database using hello **MobileServiceSQLiteStore** class.</span></span>

    <span data-ttu-id="8ad56-137">hello **DefineTable** 메서드 hello hello 제공 된 형식의 필드와 일치 하는 hello 로컬 저장소의 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-137">hello **DefineTable** method creates a table in hello local store that matches hello fields in hello provided type.</span></span>  <span data-ttu-id="8ad56-138">hello 형식 hello 원격 데이터베이스에 있는 모든 hello 열 tooinclude 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-138">hello type doesn't have tooinclude all hello columns that are in hello remote database.</span></span> <span data-ttu-id="8ad56-139">가능한 toostore 열의 하위 집합은</span><span class="sxs-lookup"><span data-stu-id="8ad56-139">It is possible toostore a subset of columns.</span></span>
* <span data-ttu-id="8ad56-140">hello **todoTable** 필드에 **TodoItemManager** 는 **IMobileServiceSyncTable** 형식 대신 **IMobileServiceTable**합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-140">hello **todoTable** field in **TodoItemManager** is an **IMobileServiceSyncTable** type instead of **IMobileServiceTable**.</span></span> <span data-ttu-id="8ad56-141">이 클래스는 hello 로컬 데이터베이스 모두에 대 한 만들기, 읽기, 업데이트 및 삭제 (CRUD) 테이블 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-141">This class uses hello local database for all create, read, update, and delete (CRUD) table operations.</span></span> <span data-ttu-id="8ad56-142">때 이러한 변경 내용을 밀어넣은 toohello 모바일 앱 백 엔드를 호출 하 여 결정 **PushAsync** hello에 **IMobileServiceSyncContext**합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-142">You decide when those changes are pushed toohello Mobile App backend by calling **PushAsync** on hello **IMobileServiceSyncContext**.</span></span> <span data-ttu-id="8ad56-143">hello 동기화 상황에 맞는 사용 하면 추적 하 고 클라이언트 응용 프로그램은 수정 될 때 모든 테이블의 변경 내용 밀어넣기 테이블 관계 보존 **PushAsync** 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-143">hello sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when **PushAsync** is called.</span></span>

    <span data-ttu-id="8ad56-144">hello 다음 **SyncAsync** 메서드는 hello 모바일 앱 백 엔드와 toosync:</span><span class="sxs-lookup"><span data-stu-id="8ad56-144">hello following **SyncAsync** method is called toosync with hello Mobile App backend:</span></span>

        public async Task SyncAsync()
        {
            ReadOnlyCollection<MobileServiceTableOperationError> syncErrors = null;

            try
            {
                await this.client.SyncContext.PushAsync();

                await this.todoTable.PullAsync(
                    "allTodoItems",
                    this.todoTable.CreateQuery());
            }
            catch (MobileServicePushFailedException exc)
            {
                if (exc.PushResult != null)
                {
                    syncErrors = exc.PushResult.Errors;
                }
            }

            // Simple error/conflict handling.
            if (syncErrors != null)
            {
                foreach (var error in syncErrors)
                {
                    if (error.OperationKind == MobileServiceTableOperationKind.Update && error.Result != null)
                    {
                        //Update failed, reverting tooserver's copy.
                        await error.CancelAndUpdateItemAsync(error.Result);
                    }
                    else
                    {
                        // Discard local change.
                        await error.CancelAndDiscardItemAsync();
                    }

                    Debug.WriteLine(@"Error executing sync operation. Item: {0} ({1}). Operation discarded.",
                        error.TableName, error.Item["id"]);
                }
            }
        }

    <span data-ttu-id="8ad56-145">이 샘플은 간단한 오류 처리 hello 기본 동기화 처리기를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-145">This sample uses simple error handling with hello default sync handler.</span></span> <span data-ttu-id="8ad56-146">실제 응용 프로그램 서버 및 네트워크 상태와 같은 다양 한 오류는 사용자 지정을 사용 하 여 충돌 하는 hello 처리 하는 것 **IMobileServiceSyncHandler** 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-146">A real application would handle hello various errors like network conditions and server conflicts by using a custom **IMobileServiceSyncHandler** implementation.</span></span>

## <a name="offline-sync-considerations"></a><span data-ttu-id="8ad56-147">오프라인 동기화 고려 사항</span><span class="sxs-lookup"><span data-stu-id="8ad56-147">Offline sync considerations</span></span>
<span data-ttu-id="8ad56-148">Hello 샘플에서 hello **SyncAsync** 시작 및 동기화를 요청 하는 경우에 메서드가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-148">In hello sample, hello **SyncAsync** method is only called on start-up and when a sync is requested.</span></span>  <span data-ttu-id="8ad56-149">tooinitiate Android 또는 iOS 응용 프로그램에서는 hello 항목 목록;에 있는 풀 다운에서 동기화 windows hello를 사용 하 여 **동기화** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-149">tooinitiate a sync in an Android or iOS app, pull down on hello items list; for Windows, use hello **Sync** button.</span></span> <span data-ttu-id="8ad56-150">실제 응용 프로그램에서는 hello 네트워크 상태가 변경 될 때 hello 동기화 트리거 또한 되도록 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-150">In a real-world application, you could also make hello sync trigger when hello network state changes.</span></span>

<span data-ttu-id="8ad56-151">끌어오기 보류 중이 있는 테이블에 대해 실행 되 로컬에서 업데이트 이전 컨텍스트 푸시를 가져오는 작업을 자동으로 트리거 hello 컨텍스트별 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-151">When a pull is executed against a table that has pending local updates tracked by hello context, that pull operation automatically triggers a preceding context push.</span></span> <span data-ttu-id="8ad56-152">생략할 수 새로 고침,를 추가 하 고이 샘플에 있는 항목을 완료 하는 경우 명시적 hello **PushAsync** 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-152">When refreshing, adding, and completing items in this sample, you can omit hello explicit **PushAsync** call.</span></span>

<span data-ttu-id="8ad56-153">Hello 원격 TodoItem 테이블의 모든 레코드를 제공 하는 hello 코드에서 쿼리, 것 뿐만 아니라 가능한 toofilter 레코드는 쿼리 id 및 쿼리를 전달 하 여 너무**PushAsync**합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-153">In hello provided code, all records in hello remote TodoItem table are queried, but it is also possible toofilter records by passing a query id and query too**PushAsync**.</span></span> <span data-ttu-id="8ad56-154">자세한 내용은 hello 섹션을 참조 하십시오. *증분 동기화* 에 [Azure 모바일 앱에서 데이터 동기화 오프 라인][2]합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-154">For more information, see hello section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps][2].</span></span>

## <a name="run-hello-client-app"></a><span data-ttu-id="8ad56-155">Hello 클라이언트 앱 실행</span><span class="sxs-lookup"><span data-stu-id="8ad56-155">Run hello client app</span></span>
<span data-ttu-id="8ad56-156">이제 사용 하도록 설정 하는 오프 라인 동기화를 hello 클라이언트 응용 프로그램이 각 플랫폼 toopopulate hello 로컬 저장소 데이터베이스에서 한 번 이상 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-156">With offline sync now enabled, run hello client application at least once on each platform toopopulate hello local store database.</span></span> <span data-ttu-id="8ad56-157">나중 오프 라인 시나리오를 시뮬레이션 하 고 hello 앱 오프 라인 상태인 동안 hello 로컬 저장소의 hello 데이터를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-157">Later, simulate an offline scenario and modify hello data in hello local store while hello app is offline.</span></span>

## <a name="update-hello-sync-behavior-of-hello-client-app"></a><span data-ttu-id="8ad56-158">Hello 클라이언트 응용 프로그램의 hello 동기화 동작을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-158">Update hello sync behavior of hello client app</span></span>
<span data-ttu-id="8ad56-159">이 섹션에서는 백 엔드에 대 한 잘못 된 응용 프로그램 URL을 사용 하 여 hello 클라이언트 프로젝트 toosimulate 오프 라인 시나리오를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-159">In this section, modify hello client project toosimulate an offline scenario by using an invalid application URL for your backend.</span></span> <span data-ttu-id="8ad56-160">또는 해제할 수 있습니다 네트워크 연결 장치를 너무 이동 하 여 "비행기 모드입니다."</span><span class="sxs-lookup"><span data-stu-id="8ad56-160">Alternatively, you can turn off network connections by moving your device too"Airplane mode."</span></span>  <span data-ttu-id="8ad56-161">이러한 변경 내용은 hello 로컬 저장소에 보관 있고 동기화 되지를 추가 하거나 데이터 항목을 변경할 때 hello 연결이 다시 설정 될 때까지 toohello 백 엔드 데이터 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-161">When you add or change data items, these changes are held in hello local store, but not synced toohello backend data store until hello connection is re-established.</span></span>

1. <span data-ttu-id="8ad56-162">솔루션 탐색기 hello에서 hello에서 hello Constants.cs 프로젝트 파일을 엽니다 **휴대용** 의 hello 값을 변경 하 고 프로젝트 `ApplicationURL` toopoint tooan 잘못 된 URL:</span><span class="sxs-lookup"><span data-stu-id="8ad56-162">In hello Solution Explorer, open hello Constants.cs project file from hello **Portable** project and change hello value of `ApplicationURL` toopoint tooan invalid URL:</span></span>

        public static string ApplicationURL = @"https://your-service.azurewebsites.net/";
2. <span data-ttu-id="8ad56-163">Hello에서 열기 hello TodoItemManager.cs 파일 **휴대용** 프로젝트를 선택한 다음 추가 **catch** 기본 hello에 대 한 **예외** 클래스 toohello **try … catch** 블록 **SyncAsync**합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-163">Open hello TodoItemManager.cs file from hello **Portable** project, then add a **catch** for hello base **Exception** class toohello **try...catch** block in **SyncAsync**.</span></span> <span data-ttu-id="8ad56-164">이 **catch** 블록 같이 hello 예외 메시지 toohello 콘솔을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-164">This **catch** block writes hello exception message toohello console, as follows:</span></span>

            catch (Exception ex)
            {
                Console.Error.WriteLine(@"Exception: {0}", ex.Message);
            }
3. <span data-ttu-id="8ad56-165">빌드하고 hello 클라이언트 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-165">Build and run hello client app.</span></span>  <span data-ttu-id="8ad56-166">새 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-166">Add some new items.</span></span> <span data-ttu-id="8ad56-167">공지 예외가 hello 백 엔드와 각 시도 toosync에 대 한 hello 콘솔에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-167">Notice that an exception is logged in hello console for each attempt toosync with hello backend.</span></span> <span data-ttu-id="8ad56-168">이러한 ' 새 항목 toohello 모바일 백 엔드 푸시할 수 있습니다 때까지 hello 로컬 저장소에만 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-168">These new items exist only in hello local store until they can be pushed toohello mobile backend.</span></span> <span data-ttu-id="8ad56-169">클라이언트 응용 프로그램 hello는 연결 된 toohello 백 엔드를 지 원하는 모든 만들기, 읽기, 업데이트, 삭제 (CRUD) 작업 처럼 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-169">hello client app behaves as if it is connected toohello backend, supporting all create, read, update, delete (CRUD) operations.</span></span>
4. <span data-ttu-id="8ad56-170">Hello 응용 프로그램을 닫고 tooverify hello 새 항목이 만든 지속형된 toohello 로컬 저장소 지 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-170">Close hello app and restart it tooverify that hello new items you created are persisted toohello local store.</span></span>
5. <span data-ttu-id="8ad56-171">(선택 사항) Visual Studio tooview hello 데이터 hello 백 엔드 데이터베이스에 변경 되지 않은 Azure SQL 데이터베이스 테이블 toosee 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-171">(Optional) Use Visual Studio tooview your Azure SQL Database table toosee that hello data in hello backend database has not changed.</span></span>

    <span data-ttu-id="8ad56-172">Visual Studio에서 **서버 탐색기**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-172">In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="8ad56-173">tooyour 데이터베이스 이동 **Azure**->**SQL 데이터베이스**합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-173">Navigate tooyour database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="8ad56-174">데이터베이스를 마우스 오른쪽 단추로 클릭하고 **SQL Server 개체 탐색기에서 열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-174">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="8ad56-175">이제 tooyour SQL 데이터베이스 테이블 및 해당 콘텐츠를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-175">Now you can browse tooyour SQL database table and its contents.</span></span>

## <a name="update-hello-client-app-tooreconnect-your-mobile-backend"></a><span data-ttu-id="8ad56-176">클라이언트 응용 프로그램 tooreconnect hello 모바일 백 엔드 업데이트</span><span class="sxs-lookup"><span data-stu-id="8ad56-176">Update hello client app tooreconnect your mobile backend</span></span>
<span data-ttu-id="8ad56-177">이 섹션에서는 hello 앱 toohello 수 모바일 백엔드 tooan 온라인 상태로 돌아오는 hello 앱을 시뮬레이션 다시 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-177">In this section, reconnect hello app toohello mobile backend, which simulates hello app coming back tooan online state.</span></span> <span data-ttu-id="8ad56-178">Hello 새로 고침 제스처를 수행 하는 경우 데이터는 동기화 된 tooyour 모바일 백 엔드 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-178">When you perform hello refresh gesture, data is synced tooyour mobile backend.</span></span>

1. <span data-ttu-id="8ad56-179">Constants.cs를 다시 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-179">Reopen Constants.cs.</span></span> <span data-ttu-id="8ad56-180">올바른 hello `applicationURL` toopoint toohello URL을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-180">Correct hello `applicationURL` toopoint toohello correct URL.</span></span>
2. <span data-ttu-id="8ad56-181">다시 작성 하 고 hello 클라이언트 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-181">Rebuild and run hello client app.</span></span> <span data-ttu-id="8ad56-182">hello 응용 프로그램을 시작한 후 hello 모바일 앱 백 엔드와 toosync을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-182">hello app attempts toosync with hello mobile app backend after launching.</span></span> <span data-ttu-id="8ad56-183">예외가 발생 하지 않을 hello 디버그 콘솔 로그인 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-183">Verify that no exceptions are logged in hello debug console.</span></span>
3. <span data-ttu-id="8ad56-184">(선택 사항) 업데이트 된 SQL Server 개체 탐색기 또는 Fiddler와 같은 나머지 도구를 사용 하 여 데이터를 보기 hello 또는 [우체부][6]합니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-184">(Optional) View hello updated data using either SQL Server Object Explorer or a REST tool like Fiddler or [Postman][6].</span></span> <span data-ttu-id="8ad56-185">공지 hello 데이터 hello 백 엔드 데이터베이스 hello 로컬 저장소와 동기화 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-185">Notice hello data has been synchronized between hello backend database and hello local store.</span></span>

    <span data-ttu-id="8ad56-186">고 hello 데이터 hello 데이터베이스 hello 로컬 저장소와 동기화 된 앱 끊어져도 추가한 hello 항목이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ad56-186">Notice hello data has been synchronized between hello database and hello local store and contains hello items you added while your app was disconnected.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8ad56-187">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="8ad56-187">Additional Resources</span></span>
* <span data-ttu-id="8ad56-188">[Azure Mobile Apps에서 오프라인 데이터 동기화][2]</span><span class="sxs-lookup"><span data-stu-id="8ad56-188">[Offline Data Sync in Azure Mobile Apps][2]</span></span>
* <span data-ttu-id="8ad56-189">[Azure Mobile Apps .NET SDK 사용 방법][8]</span><span class="sxs-lookup"><span data-stu-id="8ad56-189">[Azure Mobile Apps .NET SDK HOWTO][8]</span></span>

<!-- URLs. -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: app-service-mobile-offline-data-sync.md
[3]: http://go.microsoft.com/fwlink/p/?LinkID=716919
[4]: http://go.microsoft.com/fwlink/p/?LinkID=716920
[5]: http://sqlite.org/2016/sqlite-uwp-3120200.vsix
[6]: https://www.getpostman.com/
[7]: http://www.telerik.com/fiddler
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
