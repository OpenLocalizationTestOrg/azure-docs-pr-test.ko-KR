---
title: "Azure Mobile App(Xamarin.Forms)에 대해 오프라인 동기화 사용 | Microsoft Docs"
description: "앱 서비스 모바일 앱을 사용하여 Xamarin.Forms 응용 프로그램에서 오프라인 데이터를 캐시 및 동기화하는 방법을 알아봅니다."
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
ms.openlocfilehash: f2bed0a7124517319cc82405c4ab6b4d79aacfe1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="enable-offline-sync-for-your-xamarinforms-mobile-app"></a><span data-ttu-id="00bcf-103">Xamarin.Forms 모바일 앱에 대해 오프라인 동기화 사용</span><span class="sxs-lookup"><span data-stu-id="00bcf-103">Enable offline sync for your Xamarin.Forms mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="00bcf-104">개요</span><span class="sxs-lookup"><span data-stu-id="00bcf-104">Overview</span></span>
<span data-ttu-id="00bcf-105">이 자습서에서는 Xamarin.Forms용 Azure 모바일 앱의 오프라인 동기화 기능을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-105">This tutorial introduces the offline sync feature of Azure Mobile Apps for Xamarin.Forms.</span></span> <span data-ttu-id="00bcf-106">오프라인 동기화를 사용하면 최종 사용자는 네트워크에 연결되어 있지 않을 때도 모바일 앱과 데이터 보기, 추가 또는 수정과 같은 상호 작용을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-106">Offline sync allows end users to interact with a mobile app--viewing, adding, or modifying data--even when there is no network connection.</span></span> <span data-ttu-id="00bcf-107">변경 내용은 로컬 데이터베이스에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-107">Changes are stored in a local database.</span></span> <span data-ttu-id="00bcf-108">장치가 다시 온라인 상태가 되면 이러한 변경 내용이 원격 서비스와 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-108">Once the device is back online, these changes are synced with the remote service.</span></span>

<span data-ttu-id="00bcf-109">이 자습서는 [Xamarin iOS 앱 만들기] 자습서를 완료할 때 만든 Mobile Apps에 대한 Xamarin.Forms 빠른 시작 솔루션을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-109">This tutorial is based on the Xamarin.Forms quickstart solution for Mobile Apps that you create when you complete the tutorial [Create a Xamarin iOS app].</span></span> <span data-ttu-id="00bcf-110">Xamarin.Forms에 대한 빠른 시작 솔루션에는 사용하도록 설정해야 하는 오프라인 동기화를 지원하는 코드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-110">The quickstart solution for Xamarin.Forms contains the code to support offline sync, which just needs to be enabled.</span></span> <span data-ttu-id="00bcf-111">이 자습서에서는 빠른 시작 솔루션을 업데이트하여 Azure Mobile Apps의 오프라인 기능을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-111">In this tutorial, you update the quickstart solution to turn on the offline features of Azure Mobile Apps.</span></span> <span data-ttu-id="00bcf-112">또한 앱에서 오프라인 관련 코드를 중점적으로 다루겠습니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-112">We also highlight the offline-specific code in the app.</span></span> <span data-ttu-id="00bcf-113">다운로드한 빠른 시작 솔루션을 사용하지 않는 경우 프로젝트에 데이터 액세스 확장 패키지를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-113">If you do not use the downloaded quickstart solution, you must add the data access extension packages to your project.</span></span> <span data-ttu-id="00bcf-114">서버 확장 패키지에 대한 자세한 내용은 [Azure Mobile Apps용 .NET 백 엔드 서버 SDK 사용][1]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00bcf-114">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps][1].</span></span>

<span data-ttu-id="00bcf-115">오프라인 동기화 기능에 대한 자세한 내용은 [Azure 모바일 앱에서 오프라인 데이터 동기화][2] 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00bcf-115">To learn more about the offline sync feature, see the topic [Offline Data Sync in Azure Mobile Apps][2].</span></span>

## <a name="enable-offline-sync-functionality-in-the-quickstart-solution"></a><span data-ttu-id="00bcf-116">빠른 시작 솔루션에서 오프라인 동기화 기능 사용</span><span class="sxs-lookup"><span data-stu-id="00bcf-116">Enable offline sync functionality in the quickstart solution</span></span>
<span data-ttu-id="00bcf-117">오프라인 동기화 코드는 C# 전처리기 지시문을 사용하여 프로젝트에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-117">The offline sync code is included in the project by using C# preprocessor directives.</span></span> <span data-ttu-id="00bcf-118">**OFFLINE\_SYNC\_ENABLED** 기호가 정의된 경우 이러한 코드 경로는 빌드에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-118">When the **OFFLINE\_SYNC\_ENABLED** symbol is defined, these code paths are included in the build.</span></span> <span data-ttu-id="00bcf-119">Windows 앱의 경우 SQLite 플랫폼도 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-119">For Windows apps, you must also install the SQLite platform.</span></span>

1. <span data-ttu-id="00bcf-120">Visual Studio에서 솔루션 > **솔루션에 대한 NuGet 패키지 관리...**를 마우스 오른쪽 단추로 클릭한 후 솔루션의 모든 프로젝트에서 **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet 패키지를 검색하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-120">In Visual Studio, right-click the solution > **Manage NuGet Packages for Solution...**, then search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package for all projects in the solution.</span></span>
2. <span data-ttu-id="00bcf-121">솔루션 탐색기에서 이름에 **이식 가능** 이 있는 프로젝트(이식 가능한 클래스 라이브러리 프로젝트)에서 TodoItemManager.cs 파일을 연 후 다음 전처리기 지시문의 주석 처리를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-121">In the Solution Explorer, open the TodoItemManager.cs file from the project with **Portable** in the name, which is Portable Class Library project, then uncomment the following preprocessor directive:</span></span>

        #define OFFLINE_SYNC_ENABLED
3. <span data-ttu-id="00bcf-122">(선택 사항) Windows 장치를 지원하려면 다음 SQLite 런타임 패키지 중 하나를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-122">(Optional) To support Windows devices, install one of the following SQLite runtime packages:</span></span>

   * <span data-ttu-id="00bcf-123">**Windows 8.1 런타임:** [Windows 8.1][3]용 SQLite를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-123">**Windows 8.1 Runtime:** Install [SQLite for Windows 8.1][3].</span></span>
   * <span data-ttu-id="00bcf-124">**Windows Phone 8.1:** [Windows Phone 8.1][4]용 SQLite를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-124">**Windows Phone 8.1:** Install [SQLite for Windows Phone 8.1][4].</span></span>
   * <span data-ttu-id="00bcf-125">**유니버설 Windows 플랫폼:** [유니버설 Windows 플랫폼용 SQLite][5]를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-125">**Universal Windows Platform** Install [SQLite for the Universal Windows Universal][5].</span></span>

     <span data-ttu-id="00bcf-126">빠른 시작이 유니버설 Windows 프로젝트를 포함하지 않으면 유니버설 Windows 플랫폼은 Xamarin Forms으로 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-126">Although the quickstart does not contain a Universal Windows project, the Universal Windows platform is supported with Xamarin Forms.</span></span>
4. <span data-ttu-id="00bcf-127">(선택 사항) 각 Windows 앱 프로젝트에서 마우스 오른쪽 단추로 **참조** > **참조 추가...**를 클릭하고 **Windows** 폴더 > **확장**을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-127">(Optional) In each Windows app project, right-click **References** > **Add Reference...**, expand the **Windows** folder > **Extensions**.</span></span>
    <span data-ttu-id="00bcf-128">**Windows용 Visual C++ 2013 런타임** SDK와 함께 적절한 **Windows용 SQLite**를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-128">Enable the appropriate **SQLite for Windows** SDK along with the **Visual C++ 2013 Runtime for Windows** SDK.</span></span>
    <span data-ttu-id="00bcf-129">SQLite SDK 이름은 Windows 플랫폼마다 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-129">The SQLite SDK names vary slightly with each Windows platform.</span></span>

## <a name="review-the-client-sync-code"></a><span data-ttu-id="00bcf-130">클라이언트 동기화 코드 검토</span><span class="sxs-lookup"><span data-stu-id="00bcf-130">Review the client sync code</span></span>
<span data-ttu-id="00bcf-131">`#if OFFLINE_SYNC_ENABLED` 지시문 내의 자습서 코드에 이미 포함된 내용에 대한 간략한 개요입니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-131">Here is a brief overview of what is already included in the tutorial code inside the `#if OFFLINE_SYNC_ENABLED` directives.</span></span> <span data-ttu-id="00bcf-132">오프라인 동기화 기능은 이식 가능한 클래스 라이브러리 프로젝트의 TodoItemManager.cs 프로젝트 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-132">The offline sync functionality is in the TodoItemManager.cs project file in the Portable Class Library project.</span></span> <span data-ttu-id="00bcf-133">기능의 개념적 개요는 [Azure Mobile Apps에서 오프라인 데이터 동기화][2]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00bcf-133">For a conceptual overview of the feature, see [Offline Data Sync in Azure Mobile Apps][2].</span></span>

* <span data-ttu-id="00bcf-134">모든 테이블 작업을 수행하려면 먼저 로컬 저장소를 초기화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-134">Before any table operations can be performed, the local store must be initialized.</span></span> <span data-ttu-id="00bcf-135">로컬 저장소 데이터베이스는 다음 코드를 사용하여 **TodoItemManager** 클래스 생성자에서 초기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-135">The local store database is initialized in the **TodoItemManager** class constructor by using the following code:</span></span>

        var store = new MobileServiceSQLiteStore(OfflineDbPath);
        store.DefineTable<TodoItem>();

        //Initializes the SyncContext using the default IMobileServiceSyncHandler.
        this.client.SyncContext.InitializeAsync(store);

        this.todoTable = client.GetSyncTable<TodoItem>();

    <span data-ttu-id="00bcf-136">이 코드는 **MobileServiceSQLiteStore** 클래스를 사용하여 새로운 로컬 SQLite 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-136">This code creates a new local SQLite database using the **MobileServiceSQLiteStore** class.</span></span>

    <span data-ttu-id="00bcf-137">**DefineTable** 메서드는 제공된 형식의 필드와 일치하는 테이블을 로컬 저장소에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-137">The **DefineTable** method creates a table in the local store that matches the fields in the provided type.</span></span>  <span data-ttu-id="00bcf-138">이 형식은 원격 데이터베이스에 있는 열을 모두 포함하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-138">The type doesn't have to include all the columns that are in the remote database.</span></span> <span data-ttu-id="00bcf-139">열의 하위 집합 저장은 불가능합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-139">It is possible to store a subset of columns.</span></span>
* <span data-ttu-id="00bcf-140">**TodoItemManager**에서 **todoTable** 필드는 **IMobileServiceTable** 대신 **IMobileServiceSyncTable** 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-140">The **todoTable** field in **TodoItemManager** is an **IMobileServiceSyncTable** type instead of **IMobileServiceTable**.</span></span> <span data-ttu-id="00bcf-141">이 클래스는 모든 만들기, 읽기, 업데이트 및 삭제(CRUD) 테이블 작업에 대해 로컬 저장소 데이터베이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-141">This class uses the local database for all create, read, update, and delete (CRUD) table operations.</span></span> <span data-ttu-id="00bcf-142">**IMobileServiceSyncContext**에서 **PushAsync**를 호출하여 Mobile App 백 엔드에 해당 변경 내용을 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-142">You decide when those changes are pushed to the Mobile App backend by calling **PushAsync** on the **IMobileServiceSyncContext**.</span></span> <span data-ttu-id="00bcf-143">동기화 컨텍스트를 사용하면 모든 테이블의 변경 내용을 추적하고 밀어넣어서 테이블 관계를 보존할 수 있습니다. **PushAsync**를 호출하는 경우 클라이언트 앱을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-143">The sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when **PushAsync** is called.</span></span>

    <span data-ttu-id="00bcf-144">다음 **SyncAsync** 메서드는 모바일 앱 백 엔드와 동기화하기 위해 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-144">The following **SyncAsync** method is called to sync with the Mobile App backend:</span></span>

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
                        //Update failed, reverting to server's copy.
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

    <span data-ttu-id="00bcf-145">이 샘플에서는 기본 동기화 처리기와 함께 간단한 오류 처리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-145">This sample uses simple error handling with the default sync handler.</span></span> <span data-ttu-id="00bcf-146">실제 응용 프로그램에서는 사용자 지정 **IMobileServiceSyncHandler** 구현을 사용하여 네트워크 상태 및 서버 충돌과 같은 다양한 오류를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-146">A real application would handle the various errors like network conditions and server conflicts by using a custom **IMobileServiceSyncHandler** implementation.</span></span>

## <a name="offline-sync-considerations"></a><span data-ttu-id="00bcf-147">오프라인 동기화 고려 사항</span><span class="sxs-lookup"><span data-stu-id="00bcf-147">Offline sync considerations</span></span>
<span data-ttu-id="00bcf-148">이 샘플에서 **SyncAsync** 메서드는 시작 시 동기화가 요청된 경우에만 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-148">In the sample, the **SyncAsync** method is only called on start-up and when a sync is requested.</span></span>  <span data-ttu-id="00bcf-149">Android 또는 iOS 앱에서 동기화를 시작하려면 항목 목록을 풀다운하고 Windows의 경우 **동기화** 단추를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-149">To initiate a sync in an Android or iOS app, pull down on the items list; for Windows, use the **Sync** button.</span></span> <span data-ttu-id="00bcf-150">실제 응용 프로그램에서는 네트워크 상태가 변경될 때 동기화가 트리거되도록 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-150">In a real-world application, you could also make the sync trigger when the network state changes.</span></span>

<span data-ttu-id="00bcf-151">끌어오기가 컨텍스트에 의해 추적되는 로컬 업데이트를 보류 중인 테이블에 대해 실행되는 경우 끌어오기 작업은 먼저 자동으로 컨텍스트 푸시를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-151">When a pull is executed against a table that has pending local updates tracked by the context, that pull operation automatically triggers a preceding context push.</span></span> <span data-ttu-id="00bcf-152">이 샘플에서 항목을 새로 고침, 추가 및 완료하는 경우 명시적인 **PushAsync** 호출을 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-152">When refreshing, adding, and completing items in this sample, you can omit the explicit **PushAsync** call.</span></span>

<span data-ttu-id="00bcf-153">제공된 코드에서 원격 TodoItem 테이블에 있는 모든 레코드를 쿼리하지만 쿼리 ID 및 쿼리를 **PushAsync**로 전달하여 레코드를 필터링할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-153">In the provided code, all records in the remote TodoItem table are queried, but it is also possible to filter records by passing a query id and query to **PushAsync**.</span></span> <span data-ttu-id="00bcf-154">자세한 내용은 [Azure Mobile Apps에서 오프라인 데이터 동기화][2]에서 *증분 동기화* 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00bcf-154">For more information, see the section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps][2].</span></span>

## <a name="run-the-client-app"></a><span data-ttu-id="00bcf-155">클라이언트 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-155">Run the client app</span></span>
<span data-ttu-id="00bcf-156">이제 오프라인 동기화를 사용하도록 설정하면 각 플랫폼에서 클라이언트 응용 프로그램을 한 번 이상 실행하여 로컬 저장소 데이터베이스를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-156">With offline sync now enabled, run the client application at least once on each platform to populate the local store database.</span></span> <span data-ttu-id="00bcf-157">나중에 앱이 오프라인인 동안 오프라인 시나리오를 시뮬레이션하고 로컬 저장소에 있는 데이터를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-157">Later, simulate an offline scenario and modify the data in the local store while the app is offline.</span></span>

## <a name="update-the-sync-behavior-of-the-client-app"></a><span data-ttu-id="00bcf-158">클라이언트 앱의 동기화 동작 업데이트</span><span class="sxs-lookup"><span data-stu-id="00bcf-158">Update the sync behavior of the client app</span></span>
<span data-ttu-id="00bcf-159">이 섹션에서 백엔드에 잘못된 응용 프로그램 URL을 사용하여 오프라인 시나리오를 시뮬레이션하도록 클라이언트 프로젝트를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-159">In this section, modify the client project to simulate an offline scenario by using an invalid application URL for your backend.</span></span> <span data-ttu-id="00bcf-160">또는 "비행기 모드"로 장치를 전환하여 네트워크 연결을 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-160">Alternatively, you can turn off network connections by moving your device to "Airplane mode."</span></span>  <span data-ttu-id="00bcf-161">데이터 항목을 추가하거나 변경하는 경우 이러한 변경 내용은 로컬 저장소에 보관되지만 연결이 다시 설정될 때까지 백 엔드 데이터 저장소에 동기화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-161">When you add or change data items, these changes are held in the local store, but not synced to the backend data store until the connection is re-established.</span></span>

1. <span data-ttu-id="00bcf-162">솔루션 탐색기에서 **이식 가능** 프로젝트의 Constants.cs 프로젝트 파일을 열고 `ApplicationURL` 값이 다음과 같은 잘못된 URL을 가리키도록 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-162">In the Solution Explorer, open the Constants.cs project file from the **Portable** project and change the value of `ApplicationURL` to point to an invalid URL:</span></span>

        public static string ApplicationURL = @"https://your-service.azurewebsites.net/";
2. <span data-ttu-id="00bcf-163">**이식 가능** 프로젝트에서 TodoItemManager.cs 파일을 연 후 기본 **Exception** 클래스의 **catch**를 **SyncAsync**의 **try...catch** 블록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-163">Open the TodoItemManager.cs file from the **Portable** project, then add a **catch** for the base **Exception** class to the **try...catch** block in **SyncAsync**.</span></span> <span data-ttu-id="00bcf-164">이 **catch** 블록은 예외 메시지를 다음과 같이 콘솔에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-164">This **catch** block writes the exception message to the console, as follows:</span></span>

            catch (Exception ex)
            {
                Console.Error.WriteLine(@"Exception: {0}", ex.Message);
            }
3. <span data-ttu-id="00bcf-165">클라이언트 앱을 빌드 및 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-165">Build and run the client app.</span></span>  <span data-ttu-id="00bcf-166">새 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-166">Add some new items.</span></span> <span data-ttu-id="00bcf-167">백 엔드와 동기화하려는 각 시도에 대해 콘솔에 로그인된 예외를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-167">Notice that an exception is logged in the console for each attempt to sync with the backend.</span></span> <span data-ttu-id="00bcf-168">이러한 새 항목은 모바일 백 엔드에 푸시할 수 있을 때까지 로컬 저장소에만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-168">These new items exist only in the local store until they can be pushed to the mobile backend.</span></span> <span data-ttu-id="00bcf-169">클라이언트 앱은 백 엔드에 연결된 것처럼 동작하며 모든 CRUD(만들기, 읽기, 업데이트, 삭제) 작업을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-169">The client app behaves as if it is connected to the backend, supporting all create, read, update, delete (CRUD) operations.</span></span>
4. <span data-ttu-id="00bcf-170">앱을 닫았다가 다시 시작하여 만든 새 항목이 로컬 저장소에 유지되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-170">Close the app and restart it to verify that the new items you created are persisted to the local store.</span></span>
5. <span data-ttu-id="00bcf-171">(선택 사항) Azure SQL 데이터베이스 테이블을 보는 Visual Studio를 사용하여 백 엔드 데이터베이스에서 데이터가 변경되지 않았음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-171">(Optional) Use Visual Studio to view your Azure SQL Database table to see that the data in the backend database has not changed.</span></span>

    <span data-ttu-id="00bcf-172">Visual Studio에서 **서버 탐색기**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-172">In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="00bcf-173">**Azure**->**SQL Databases**에 있는 데이터베이스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-173">Navigate to your database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="00bcf-174">데이터베이스를 마우스 오른쪽 단추로 클릭하고 **SQL Server 개체 탐색기에서 열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-174">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="00bcf-175">이제 SQL 데이터베이스 테이블 및 콘텐츠를 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-175">Now you can browse to your SQL database table and its contents.</span></span>

## <a name="update-the-client-app-to-reconnect-your-mobile-backend"></a><span data-ttu-id="00bcf-176">모바일 백 엔드를 다시 연결하도록 클라이언트 앱 업데이트</span><span class="sxs-lookup"><span data-stu-id="00bcf-176">Update the client app to reconnect your mobile backend</span></span>
<span data-ttu-id="00bcf-177">이 섹션에서는 앱을 모바일 백 엔드에 다시 연결하여 다시 온라인 상태로 전환되는 앱을 시뮬레이트합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-177">In this section, reconnect the app to the mobile backend, which simulates the app coming back to an online state.</span></span> <span data-ttu-id="00bcf-178">새로 고침 제스처를 수행하면 데이터가 모바일 백 엔드에 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-178">When you perform the refresh gesture, data is synced to your mobile backend.</span></span>

1. <span data-ttu-id="00bcf-179">Constants.cs를 다시 엽니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-179">Reopen Constants.cs.</span></span> <span data-ttu-id="00bcf-180">올바른 URL을 가리키도록 `applicationURL` 를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-180">Correct the `applicationURL` to point to the correct URL.</span></span>
2. <span data-ttu-id="00bcf-181">클라이언트 앱을 다시 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-181">Rebuild and run the client app.</span></span> <span data-ttu-id="00bcf-182">앱을 시작한 후에 모바일 앱 백 엔드와 동기화하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-182">The app attempts to sync with the mobile app backend after launching.</span></span> <span data-ttu-id="00bcf-183">디버그 콘솔에 기록된 예외가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-183">Verify that no exceptions are logged in the debug console.</span></span>
3. <span data-ttu-id="00bcf-184">(선택 사항) SQL Server 개체 탐색기 또는 Fiddler나 [Postman][6] 같은 REST 도구를 사용하여 업데이트된 데이터를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-184">(Optional) View the updated data using either SQL Server Object Explorer or a REST tool like Fiddler or [Postman][6].</span></span> <span data-ttu-id="00bcf-185">백 엔드 데이터베이스와 로컬 저장소의 데이터가 동기화된 것을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-185">Notice the data has been synchronized between the backend database and the local store.</span></span>

    <span data-ttu-id="00bcf-186">데이터베이스와 로컬 저장소 간에 데이터가 동기화되었으며 앱의 연결이 끊어진 동안 추가한 항목을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="00bcf-186">Notice the data has been synchronized between the database and the local store and contains the items you added while your app was disconnected.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="00bcf-187">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="00bcf-187">Additional Resources</span></span>
* <span data-ttu-id="00bcf-188">[Azure Mobile Apps에서 오프라인 데이터 동기화][2]</span><span class="sxs-lookup"><span data-stu-id="00bcf-188">[Offline Data Sync in Azure Mobile Apps][2]</span></span>
* <span data-ttu-id="00bcf-189">[Azure Mobile Apps .NET SDK 사용 방법][8]</span><span class="sxs-lookup"><span data-stu-id="00bcf-189">[Azure Mobile Apps .NET SDK HOWTO][8]</span></span>

<!-- URLs. -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: app-service-mobile-offline-data-sync.md
[3]: http://go.microsoft.com/fwlink/p/?LinkID=716919
[4]: http://go.microsoft.com/fwlink/p/?LinkID=716920
[5]: http://sqlite.org/2016/sqlite-uwp-3120200.vsix
[6]: https://www.getpostman.com/
[7]: http://www.telerik.com/fiddler
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
