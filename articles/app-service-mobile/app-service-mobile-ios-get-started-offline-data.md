---
title: "iOS 모바일 앱으로 오프라인 동기화 사용 | Microsoft Docs"
description: "Azure App Service Mobile Apps를 사용하여 iOS 응용 프로그램에서 오프라인 데이터를 캐시 및 동기화하는 방법을 알아봅니다."
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: eb5b9520-0f39-4a09-940a-dadb6d940db8
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 44c0d26b2d7d28322d436d4bda319d728c31a635
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="enable-offline-syncing-with-ios-mobile-apps"></a><span data-ttu-id="9b8de-103">iOS 모바일 앱으로 오프라인 동기화 사용</span><span class="sxs-lookup"><span data-stu-id="9b8de-103">Enable offline syncing with iOS mobile apps</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="9b8de-104">개요</span><span class="sxs-lookup"><span data-stu-id="9b8de-104">Overview</span></span>
<span data-ttu-id="9b8de-105">이 자습서는 iOS용 Azure App Service의 Mobile Apps 기능을 사용한 오프라인 동기화를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-105">This tutorial covers offline syncing with the Mobile Apps feature of Azure App Service for iOS.</span></span> <span data-ttu-id="9b8de-106">오프라인 동기화를 사용하면 네트워크에 연결되지 않은 경우에도 최종 사용자가 모바일 앱을 사용하여 데이터를 보거나, 추가하거나 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-106">With offline syncing end-users can interact with a mobile app to view, add, or modify data, even when they have no network connection.</span></span> <span data-ttu-id="9b8de-107">변경 내용은 로컬 데이터베이스에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-107">Changes are stored in a local database.</span></span> <span data-ttu-id="9b8de-108">장치가 다시 온라인 상태가 되면 변경 내용이 원격 백 엔드와 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-108">After the device is back online, the changes are synced with the remote back end.</span></span>

<span data-ttu-id="9b8de-109">Mobile Apps를 처음 사용하는 경우, 먼저 [iOS 앱 만들기]자습서를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-109">If this is your first experience with Mobile Apps, you should first complete the tutorial [Create an iOS App].</span></span> <span data-ttu-id="9b8de-110">다운로드한 빠른 시작 서버 프로젝트를 사용하지 않는 경우 프로젝트에 데이터 액세스 확장 패키지를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-110">If you do not use the downloaded quick-start server project, you must add the data-access extension packages to your project.</span></span> <span data-ttu-id="9b8de-111">서버 확장 패키지에 대한 자세한 내용은 [Azure 모바일 앱용 .NET 백 엔드 서버 SDK 사용](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9b8de-111">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="9b8de-112">오프라인 동기화 기능에 대해 자세히 알아보려면 [Mobile Apps에서 오프라인 데이터 동기화]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9b8de-112">To learn more about the offline sync feature, see [Offline Data Sync in Mobile Apps].</span></span>

## <span data-ttu-id="9b8de-113"><a name="review-sync"></a>클라이언트 동기화 코드 검토</span><span class="sxs-lookup"><span data-stu-id="9b8de-113"><a name="review-sync"></a>Review the client sync code</span></span>
<span data-ttu-id="9b8de-114">[iOS 앱 만들기] 자습서용으로 다운로드한 클라이언트 프로젝트는 로컬 핵심 데이터 기반 데이터베이스를 사용하여 오프라인 동기화를 지원하는 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-114">The client project that you downloaded for the [Create an iOS App] tutorial already contains code that supports offline synchronization using a local Core Data-based database.</span></span> <span data-ttu-id="9b8de-115">이 섹션은 이미 자습서 코드에 포함된 내용에 대한 요약입니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-115">This section summarizes what is already included in the tutorial code.</span></span> <span data-ttu-id="9b8de-116">기능의 개념적 개요는 [Mobile Apps에서 오프라인 데이터 동기화]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9b8de-116">For a conceptual overview of the feature, see [Offline Data Sync in Mobile Apps].</span></span>

<span data-ttu-id="9b8de-117">Mobile Apps의 오프라인 데이터 동기화 기능을 사용하면 네트워크에 액세스할 수 없는 경우에도 로컬 데이터베이스를 조작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-117">Using the offline data-sync feature of Mobile Apps, end-users can interact with a local database even when the network is inaccessible.</span></span> <span data-ttu-id="9b8de-118">앱에서 이러한 기능을 사용하려면 `MSClient` 의 동기화 컨텍스트를 초기화하고 로컬 저장소를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-118">To use these features in your app, you initialize the sync context of `MSClient` and reference a local store.</span></span> <span data-ttu-id="9b8de-119">그런 다음 **MSSyncTable** 인터페이스를 통해 테이블을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-119">Then you reference your table through the **MSSyncTable** interface.</span></span>

<span data-ttu-id="9b8de-120">**QSTodoService.m**(Objective-C) 또는 **ToDoTableViewController.swift**(Swift)에서 **syncTable** 멤버 형식은 **MSSyncTable**입니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-120">In **QSTodoService.m** (Objective-C) or **ToDoTableViewController.swift** (Swift), notice that the type of the member **syncTable** is **MSSyncTable**.</span></span> <span data-ttu-id="9b8de-121">오프라인 동기화에는 **MSTable** 대신 이 동기화 테이블 인터페이스가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-121">Offline sync uses this sync table interface instead of **MSTable**.</span></span> <span data-ttu-id="9b8de-122">동기화 테이블이 사용되면 모든 작업이 로컬 저장소로 이동되고 명시적 밀어넣기 및 끌어오기 작업이 있는 원격 백 엔드와만 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-122">When a sync table is used, all operations go to the local store and are synchronized only with the remote back end with explicit push and pull operations.</span></span>

 <span data-ttu-id="9b8de-123">동기화 테이블에 대한 참조를 얻으려면 `MSClient`에서 **syncTableWithName** 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-123">To get a reference to a sync table, use the **syncTableWithName** method on `MSClient`.</span></span> <span data-ttu-id="9b8de-124">오프라인 동기화 기능을 제거하려면 대신 **tableWithName**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-124">To remove offline sync functionality, use **tableWithName** instead.</span></span>

<span data-ttu-id="9b8de-125">모든 테이블 작업을 수행하려면 먼저 로컬 저장소를 초기화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-125">Before any table operations can be performed, the local store must be initialized.</span></span> <span data-ttu-id="9b8de-126">관련 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-126">Here is the relevant code:</span></span>

* <span data-ttu-id="9b8de-127">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="9b8de-127">**Objective-C**.</span></span> <span data-ttu-id="9b8de-128">**QSTodoService.init** 메서드:</span><span class="sxs-lookup"><span data-stu-id="9b8de-128">In the **QSTodoService.init** method:</span></span>

   ```objc
   MSCoreDataStore *store = [[MSCoreDataStore alloc] initWithManagedObjectContext:context];
   self.client.syncContext = [[MSSyncContext alloc] initWithDelegate:nil dataSource:store callback:nil];
   ```    
* <span data-ttu-id="9b8de-129">**Swift**.</span><span class="sxs-lookup"><span data-stu-id="9b8de-129">**Swift**.</span></span> <span data-ttu-id="9b8de-130">**ToDoTableViewController.viewDidLoad** 메서드:</span><span class="sxs-lookup"><span data-stu-id="9b8de-130">In the **ToDoTableViewController.viewDidLoad** method:</span></span>

   ```swift
   let client = MSClient(applicationURLString: "http:// ...") // URI of the Mobile App
   let managedObjectContext = (UIApplication.sharedApplication().delegate as! AppDelegate).managedObjectContext!
   self.store = MSCoreDataStore(managedObjectContext: managedObjectContext)
   client.syncContext = MSSyncContext(delegate: nil, dataSource: self.store, callback: nil)
   ```
   <span data-ttu-id="9b8de-131">이 메서드는 Mobile Apps SDK에 제공되는 `MSCoreDataStore` 인터페이스를 사용하여 로컬 저장소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-131">This method creates a local store by using the `MSCoreDataStore` interface, which the Mobile Apps SDK provides.</span></span> <span data-ttu-id="9b8de-132">또는 `MSSyncContextDataSource` 프로토콜을 구현하여 다른 로컬 저장소를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-132">Alternatively, you can provide a different local store by implementing the `MSSyncContextDataSource` protocol.</span></span> <span data-ttu-id="9b8de-133">또한 **MSSyncContext**의 첫 번째 매개 변수는 충돌 처리기를 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-133">Also, the first parameter of **MSSyncContext** is used to specify a conflict handler.</span></span> <span data-ttu-id="9b8de-134">`nil`을 전달했으므로 충돌 발생 시 작업을 중단하는 기본 충돌 처리기를 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-134">Because we have passed `nil`, we get the default conflict handler, which fails on any conflict.</span></span>

<span data-ttu-id="9b8de-135">이제 실제 동기화 작업을 수행하여 원격 백 엔드에서 데이터를 가져와 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-135">Now, let's perform the actual sync operation, and get data from the remote back end:</span></span>

* <span data-ttu-id="9b8de-136">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="9b8de-136">**Objective-C**.</span></span> <span data-ttu-id="9b8de-137">`syncData`는 새 변경 내용을 푸시한 다음 **pullData**를 호출하여 원격 백 엔드에서 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-137">`syncData` first pushes new changes and then calls **pullData** to get data from the remote back end.</span></span> <span data-ttu-id="9b8de-138">그러면 **pullData** 메서드가 쿼리와 일치하는 새 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-138">In turn, the **pullData** method gets new data that matches a query:</span></span>

   ```objc
   -(void)syncData:(QSCompletionBlock)completion
   {
       // Push all changes in the sync context, and then pull new data.
       [self.client.syncContext pushWithCompletion:^(NSError *error) {
           [self logErrorIfNotNil:error];
           [self pullData:completion];
       }];
   }

   -(void)pullData:(QSCompletionBlock)completion
   {
       MSQuery *query = [self.syncTable query];

       // Pulls data from the remote server into the local table.
       // We're pulling all items and filtering in the view.
       // Query ID is used for incremental sync.
       [self.syncTable pullWithQuery:query queryId:@"allTodoItems" completion:^(NSError *error) {
           [self logErrorIfNotNil:error];

           // Lets the caller know that we have finished.
           if (completion != nil) {
               dispatch_async(dispatch_get_main_queue(), completion);
           }
       }];
   }
   ```
* <span data-ttu-id="9b8de-139">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="9b8de-139">**Swift**:</span></span>
   ```swift
   func onRefresh(sender: UIRefreshControl!) {
      UIApplication.sharedApplication().networkActivityIndicatorVisible = true

      self.table!.pullWithQuery(self.table?.query(), queryId: "AllRecords") {
          (error) -> Void in

          UIApplication.sharedApplication().networkActivityIndicatorVisible = false

          if error != nil {
              // A real application would handle various errors like network conditions,
              // server conflicts, etc via the MSSyncContextDelegate
              print("Error: \(error!.description)")

              // We will discard our changes and keep the server's copy for simplicity
              if let opErrors = error!.userInfo[MSErrorPushResultKey] as? Array<MSTableOperationError> {
                  for opError in opErrors {
                      print("Attempted operation to item \(opError.itemId)")
                      if (opError.operation == .Insert || opError.operation == .Delete) {
                          print("Insert/Delete, failed discarding changes")
                          opError.cancelOperationAndDiscardItemWithCompletion(nil)
                      } else {
                          print("Update failed, reverting to server's copy")
                          opError.cancelOperationAndUpdateItem(opError.serverItem!, completion: nil)
                      }
                  }
              }
          }
          self.refreshControl?.endRefreshing()
      }
   }
   ```

<span data-ttu-id="9b8de-140">Objective-C 버전의 `syncData`에서 먼저 동기화 컨텍스트에 대해 **pushWithCompletion**을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-140">In the Objective-C version, in `syncData`, we first call **pushWithCompletion** on the sync context.</span></span> <span data-ttu-id="9b8de-141">이 메서드는 모든 테이블에서 변경 내용을 푸시하므로 동기화 테이블 자체가 아닌 `MSSyncContext`의 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-141">This method is a member of `MSSyncContext` (and not the sync table itself) because it pushes changes across all tables.</span></span> <span data-ttu-id="9b8de-142">CUD 작업을 통해 로컬에서 수정된 레코드만 서버에 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-142">Only records that have been modified in some way locally (through CUD operations) are sent to the server.</span></span> <span data-ttu-id="9b8de-143">그런 후 다음 도우미 **pullData**가 호출됩니다. 이 도우미는 **MSSyncTable.pullWithQuery**를 호출하여 원격 데이터를 검색하고 로컬 데이터베이스에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-143">Then the helper **pullData** is called, which calls **MSSyncTable.pullWithQuery** to retrieve remote data and store it in the local database.</span></span>

<span data-ttu-id="9b8de-144">Swift 버전의 경우 푸시 작업이 꼭 필요하지 않기 때문에 **pushWithCompletion**에 대한 호출이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-144">In the Swift version, because the push operation was not strictly necessary, there is no call to **pushWithCompletion**.</span></span> <span data-ttu-id="9b8de-145">푸시 작업을 수행하는 테이블에 대한 동기화 컨텍스트에 보류 중인 변경 내용이 있는 경우 끌어오기가 항상 푸시 작업을 먼저 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-145">If there are any changes pending in the sync context for the table that is doing a push operation, pull always issues a push first.</span></span> <span data-ttu-id="9b8de-146">그러나 둘 이상의 동기화 테이블이 있는 경우 푸시를 명시적으로 호출하여 관련 테이블에서 모든 항목의 일관성을 유지하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-146">However, if you have more than one sync table, it is best to explicitly call push to ensure that everything is consistent across related tables.</span></span>

<span data-ttu-id="9b8de-147">Objective-C 버전과 Swift 버전 모두에서 **pullWithQuery** 메서드를 사용하여 쿼리를 지정하면 검색할 레코드를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-147">In both the Objective-C and Swift versions, you can use the **pullWithQuery** method to specify a query to filter the records you want to retrieve.</span></span> <span data-ttu-id="9b8de-148">이 예제에서 쿼리는 원격 `TodoItem` 테이블의 모든 레코드를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-148">In this example, the query retrieves all records in the remote `TodoItem` table.</span></span>

<span data-ttu-id="9b8de-149">**pullWithQuery**에 대한 두 번째 매개 변수는 *증분 동기화*에 사용되는 쿼리 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-149">The second parameter of **pullWithQuery** is a query ID that is used for *incremental sync*.</span></span> <span data-ttu-id="9b8de-150">증분 동기화는 레코드의 `UpdatedAt` 타임스탬프(로컬 저장소에서는 `updatedAt`이라고 함)를 사용하여 마지막 동기화 이후에 수정된 레코드만 검색합니다. 쿼리 ID는 앱의 각 논리 쿼리에 고유한 설명 문자열이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-150">Incremental sync retrieves only records that were modified since the last sync, using the record's `UpdatedAt` time stamp (called `updatedAt` in the local store.) The query ID should be a descriptive string that is unique for each logical query in your app.</span></span> <span data-ttu-id="9b8de-151">증분 동기화를 옵트아웃하려면 `nil`을 쿼리 ID로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-151">To opt out of incremental sync, pass `nil` as the query ID.</span></span> <span data-ttu-id="9b8de-152">이런 방법은 각각의 끌어오기 작업에서 모든 레코드가 검색되므로 비효율적일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-152">This approach can be potentially inefficient, because it retrieves all records on each pull operation.</span></span>

<span data-ttu-id="9b8de-153">Objective-C 앱은 데이터를 추가하거나 수정할 때 사용자가 새로 고침 제스처를 수행할 때 및 시작 시 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-153">The Objective-C app syncs when you modify or add data, when a user performs the refresh gesture, and on launch.</span></span>

<span data-ttu-id="9b8de-154">Swift 앱은 사용자가 새로 고침 제스처를 수행할 때 및 시작 시 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-154">The Swift app syncs when the user performs the refresh gesture and on launch.</span></span>

<span data-ttu-id="9b8de-155">데이터가 수정될 때마다(Objective-C) 또는 앱이 시작될 때마다(Objective-C 및 Swift) 앱이 동기화되므로 앱은 사용자가 온라인 상태인 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-155">Because the app syncs whenever data is modified (Objective-C) or whenever the app starts (Objective-C and Swift), the app assumes that the user is online.</span></span> <span data-ttu-id="9b8de-156">나중에 나오는 섹션에서는 사용자가 오프라인 상태일 때도 편집할 수 있도록 앱을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-156">In a later section, you will update the app so that users can edit even when they are offline.</span></span>

## <span data-ttu-id="9b8de-157"><a name="review-core-data"></a>핵심 데이터 모델 검토</span><span class="sxs-lookup"><span data-stu-id="9b8de-157"><a name="review-core-data"></a>Review the Core Data model</span></span>
<span data-ttu-id="9b8de-158">핵심 데이터 오프라인 저장소를 사용하는 경우 데이터 모델에서 특정 테이블 및 필드를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-158">When you use the Core Data offline store, you must define particular tables and fields in your data model.</span></span> <span data-ttu-id="9b8de-159">샘플 앱에는 이미 올바른 형식의 데이터 모델이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-159">The sample app already includes a data model with the right format.</span></span> <span data-ttu-id="9b8de-160">이 섹션에서는 이러한 테이블을 살펴보고 사용 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-160">In this section, we walk through these tables to show how they are used.</span></span>

<span data-ttu-id="9b8de-161">**QSDataModel.xcdatamodeld**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-161">Open **QSDataModel.xcdatamodeld**.</span></span> <span data-ttu-id="9b8de-162">SDK에 사용되는 테이블 3개 및 할 일 항목 자체에 사용되는 테이블 1개 등 테이블 4개가 정의되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-162">Four tables are defined--three that are used by the SDK and one that's used for the to-do items themselves:</span></span>
  * <span data-ttu-id="9b8de-163">MS_TableOperations: 서버와 동기화되어야 하는 항목 추적을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-163">MS_TableOperations: Tracks the items that need to be synchronized with the server.</span></span>
  * <span data-ttu-id="9b8de-164">MS_TableOperationErrors: 오프라인 동기화 중에 발생하는 모든 오류를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-164">MS_TableOperationErrors: Tracks any errors that happen during offline synchronization.</span></span>
  * <span data-ttu-id="9b8de-165">MS_TableConfig: 모든 끌어오기 작업에 대한 마지막 동기화 작업의 마지막 업데이트 시간을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-165">MS_TableConfig: Tracks the last updated time for the last sync operation for all pull operations.</span></span>
  * <span data-ttu-id="9b8de-166">TodoItem: 할 일 항목을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-166">TodoItem: Stores the to-do items.</span></span> <span data-ttu-id="9b8de-167">시스템 열 **createdAt**, **updatedAt** 및 **version**은 선택적 시스템 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-167">The system columns **createdAt**, **updatedAt**, and **version** are optional system properties.</span></span>

> [!NOTE]
> <span data-ttu-id="9b8de-168">Mobile Apps SDK는 "**``**"(으)로 시작하는 열 이름을 예약합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-168">The Mobile Apps SDK reserves column names that begin with "**``**".</span></span> <span data-ttu-id="9b8de-169">시스템 열 이외에 이 접두사를 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="9b8de-169">Do not use this prefix with anything other than system columns.</span></span> <span data-ttu-id="9b8de-170">그렇지 않으면 원격 백 엔드를 사용하는 경우 열 이름이 수정됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-170">Otherwise, your column names are modified when you use the remote back end.</span></span>
>
>

<span data-ttu-id="9b8de-171">오프라인 동기화 기능을 사용하는 경우 시스템 테이블 3개와 데이터 테이블을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-171">When you use the offline sync feature, define the three system tables and the data table.</span></span>

### <a name="system-tables"></a><span data-ttu-id="9b8de-172">시스템 테이블</span><span class="sxs-lookup"><span data-stu-id="9b8de-172">System tables</span></span>

<span data-ttu-id="9b8de-173">**MS_TableOperations**</span><span class="sxs-lookup"><span data-stu-id="9b8de-173">**MS_TableOperations**</span></span>  

![MS_TableOperations 테이블 특성][defining-core-data-tableoperations-entity]

| <span data-ttu-id="9b8de-175">특성</span><span class="sxs-lookup"><span data-stu-id="9b8de-175">Attribute</span></span> | <span data-ttu-id="9b8de-176">형식</span><span class="sxs-lookup"><span data-stu-id="9b8de-176">Type</span></span> |
| --- | --- |
| <span data-ttu-id="9b8de-177">id</span><span class="sxs-lookup"><span data-stu-id="9b8de-177">id</span></span> | <span data-ttu-id="9b8de-178">정수 64</span><span class="sxs-lookup"><span data-stu-id="9b8de-178">Integer 64</span></span> |
| <span data-ttu-id="9b8de-179">itemId</span><span class="sxs-lookup"><span data-stu-id="9b8de-179">itemId</span></span> | <span data-ttu-id="9b8de-180">String</span><span class="sxs-lookup"><span data-stu-id="9b8de-180">String</span></span> |
| <span data-ttu-id="9b8de-181">properties</span><span class="sxs-lookup"><span data-stu-id="9b8de-181">properties</span></span> | <span data-ttu-id="9b8de-182">이진 데이터</span><span class="sxs-lookup"><span data-stu-id="9b8de-182">Binary Data</span></span> |
| <span data-ttu-id="9b8de-183">테이블</span><span class="sxs-lookup"><span data-stu-id="9b8de-183">table</span></span> | <span data-ttu-id="9b8de-184">String</span><span class="sxs-lookup"><span data-stu-id="9b8de-184">String</span></span> |
| <span data-ttu-id="9b8de-185">tableKind</span><span class="sxs-lookup"><span data-stu-id="9b8de-185">tableKind</span></span> | <span data-ttu-id="9b8de-186">정수 16</span><span class="sxs-lookup"><span data-stu-id="9b8de-186">Integer 16</span></span> |


<span data-ttu-id="9b8de-187">**MS_TableOperationErrors**</span><span class="sxs-lookup"><span data-stu-id="9b8de-187">**MS_TableOperationErrors**</span></span>

 ![MS_TableOperationErrors 테이블 특성][defining-core-data-tableoperationerrors-entity]

| <span data-ttu-id="9b8de-189">특성</span><span class="sxs-lookup"><span data-stu-id="9b8de-189">Attribute</span></span> | <span data-ttu-id="9b8de-190">형식</span><span class="sxs-lookup"><span data-stu-id="9b8de-190">Type</span></span> |
| --- | --- |
| <span data-ttu-id="9b8de-191">id</span><span class="sxs-lookup"><span data-stu-id="9b8de-191">id</span></span> |<span data-ttu-id="9b8de-192">문자열</span><span class="sxs-lookup"><span data-stu-id="9b8de-192">String</span></span> |
| <span data-ttu-id="9b8de-193">operationId</span><span class="sxs-lookup"><span data-stu-id="9b8de-193">operationId</span></span> |<span data-ttu-id="9b8de-194">정수 64</span><span class="sxs-lookup"><span data-stu-id="9b8de-194">Integer 64</span></span> |
| <span data-ttu-id="9b8de-195">properties</span><span class="sxs-lookup"><span data-stu-id="9b8de-195">properties</span></span> |<span data-ttu-id="9b8de-196">이진 데이터</span><span class="sxs-lookup"><span data-stu-id="9b8de-196">Binary Data</span></span> |
| <span data-ttu-id="9b8de-197">tableKind</span><span class="sxs-lookup"><span data-stu-id="9b8de-197">tableKind</span></span> |<span data-ttu-id="9b8de-198">정수 16</span><span class="sxs-lookup"><span data-stu-id="9b8de-198">Integer 16</span></span> |

 <span data-ttu-id="9b8de-199">**MS_TableConfig**</span><span class="sxs-lookup"><span data-stu-id="9b8de-199">**MS_TableConfig**</span></span>

 ![][defining-core-data-tableconfig-entity]

| <span data-ttu-id="9b8de-200">특성</span><span class="sxs-lookup"><span data-stu-id="9b8de-200">Attribute</span></span> | <span data-ttu-id="9b8de-201">형식</span><span class="sxs-lookup"><span data-stu-id="9b8de-201">Type</span></span> |
| --- | --- |
| <span data-ttu-id="9b8de-202">id</span><span class="sxs-lookup"><span data-stu-id="9b8de-202">id</span></span> |<span data-ttu-id="9b8de-203">문자열</span><span class="sxs-lookup"><span data-stu-id="9b8de-203">String</span></span> |
| <span data-ttu-id="9b8de-204">key</span><span class="sxs-lookup"><span data-stu-id="9b8de-204">key</span></span> |<span data-ttu-id="9b8de-205">String</span><span class="sxs-lookup"><span data-stu-id="9b8de-205">String</span></span> |
| <span data-ttu-id="9b8de-206">keyType</span><span class="sxs-lookup"><span data-stu-id="9b8de-206">keyType</span></span> |<span data-ttu-id="9b8de-207">정수 64</span><span class="sxs-lookup"><span data-stu-id="9b8de-207">Integer 64</span></span> |
| <span data-ttu-id="9b8de-208">테이블</span><span class="sxs-lookup"><span data-stu-id="9b8de-208">table</span></span> |<span data-ttu-id="9b8de-209">String</span><span class="sxs-lookup"><span data-stu-id="9b8de-209">String</span></span> |
| <span data-ttu-id="9b8de-210">값</span><span class="sxs-lookup"><span data-stu-id="9b8de-210">value</span></span> |<span data-ttu-id="9b8de-211">문자열</span><span class="sxs-lookup"><span data-stu-id="9b8de-211">String</span></span> |

### <a name="data-table"></a><span data-ttu-id="9b8de-212">데이터 테이블</span><span class="sxs-lookup"><span data-stu-id="9b8de-212">Data table</span></span>

<span data-ttu-id="9b8de-213">**TodoItem**</span><span class="sxs-lookup"><span data-stu-id="9b8de-213">**TodoItem**</span></span>

| <span data-ttu-id="9b8de-214">특성</span><span class="sxs-lookup"><span data-stu-id="9b8de-214">Attribute</span></span> | <span data-ttu-id="9b8de-215">유형</span><span class="sxs-lookup"><span data-stu-id="9b8de-215">Type</span></span> | <span data-ttu-id="9b8de-216">참고</span><span class="sxs-lookup"><span data-stu-id="9b8de-216">Note</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9b8de-217">id</span><span class="sxs-lookup"><span data-stu-id="9b8de-217">id</span></span> | <span data-ttu-id="9b8de-218">문자열, 필수로 표시</span><span class="sxs-lookup"><span data-stu-id="9b8de-218">String, marked required</span></span> |<span data-ttu-id="9b8de-219">원격 저장소의 기본 키</span><span class="sxs-lookup"><span data-stu-id="9b8de-219">Primary key in remote store</span></span> |
| <span data-ttu-id="9b8de-220">complete</span><span class="sxs-lookup"><span data-stu-id="9b8de-220">complete</span></span> | <span data-ttu-id="9b8de-221">Boolean</span><span class="sxs-lookup"><span data-stu-id="9b8de-221">Boolean</span></span> | <span data-ttu-id="9b8de-222">할 일 항목 필드</span><span class="sxs-lookup"><span data-stu-id="9b8de-222">To-do item field</span></span> |
| <span data-ttu-id="9b8de-223">텍스트</span><span class="sxs-lookup"><span data-stu-id="9b8de-223">text</span></span> |<span data-ttu-id="9b8de-224">String</span><span class="sxs-lookup"><span data-stu-id="9b8de-224">String</span></span> |<span data-ttu-id="9b8de-225">할 일 항목 필드</span><span class="sxs-lookup"><span data-stu-id="9b8de-225">To-do item field</span></span> |
| <span data-ttu-id="9b8de-226">createdAt</span><span class="sxs-lookup"><span data-stu-id="9b8de-226">createdAt</span></span> | <span data-ttu-id="9b8de-227">Date</span><span class="sxs-lookup"><span data-stu-id="9b8de-227">Date</span></span> | <span data-ttu-id="9b8de-228">(옵션) **createdAt** 시스템 속성에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-228">(optional) Maps to **createdAt** system property</span></span> |
| <span data-ttu-id="9b8de-229">updatedAt</span><span class="sxs-lookup"><span data-stu-id="9b8de-229">updatedAt</span></span> | <span data-ttu-id="9b8de-230">Date</span><span class="sxs-lookup"><span data-stu-id="9b8de-230">Date</span></span> | <span data-ttu-id="9b8de-231">(옵션) **updatedAt** 시스템 속성에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-231">(optional) Maps to **updatedAt** system property</span></span> |
| <span data-ttu-id="9b8de-232">버전</span><span class="sxs-lookup"><span data-stu-id="9b8de-232">version</span></span> | <span data-ttu-id="9b8de-233">String</span><span class="sxs-lookup"><span data-stu-id="9b8de-233">String</span></span> | <span data-ttu-id="9b8de-234">(옵션) 충돌을 검색하는 데 사용되며 version에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-234">(optional) Used to detect conflicts, maps to version</span></span> |

## <span data-ttu-id="9b8de-235"><a name="setup-sync"></a>앱의 동기화 동작 변경</span><span class="sxs-lookup"><span data-stu-id="9b8de-235"><a name="setup-sync"></a>Change the sync behavior of the app</span></span>
<span data-ttu-id="9b8de-236">이 섹션에서는 앱 시작 시 또는 항목을 삽입하거나 업데이트할 때 동기화하지 않도록 앱을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-236">In this section, you modify the app so that it does not sync on app start or when you insert and update items.</span></span> <span data-ttu-id="9b8de-237">새로 고침 제스처 단추를 누를 때만 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-237">It syncs only when the refresh gesture button is performed.</span></span>

<span data-ttu-id="9b8de-238">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="9b8de-238">**Objective-C**:</span></span>

1. <span data-ttu-id="9b8de-239">**QSTodoListViewController.m**에서 **viewDidLoad** 메서드가 끝날 때 `[self refresh]` 호출을 제거하도록 이 메서드를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-239">In **QSTodoListViewController.m**, change the **viewDidLoad** method to remove the call to `[self refresh]` at the end of the method.</span></span> <span data-ttu-id="9b8de-240">이제 앱 시작 시 데이터가 서버와 동기화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-240">Now the data is not synced with the server on app start.</span></span> <span data-ttu-id="9b8de-241">대신 로컬 저장소의 콘텐츠와 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-241">Instead, it's synced with the contents of the local store.</span></span>
2. <span data-ttu-id="9b8de-242">**QSTodoService.m**에서 항목이 삽입된 후에 동기화되지 않도록 `addItem`의 정의를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-242">In **QSTodoService.m**, modify the definition of `addItem` so that it doesn't sync after the item is inserted.</span></span> <span data-ttu-id="9b8de-243">`self syncData` 블록을 제거하고 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-243">Remove the `self syncData` block and replace it with the following:</span></span>

   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```
3. <span data-ttu-id="9b8de-244">앞서 언급했듯이 `completeItem`의 정의를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-244">Modify the definition of `completeItem` as mentioned previously.</span></span> <span data-ttu-id="9b8de-245">`self syncData` 블록을 제거하고 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-245">Remove the block for `self syncData` and replace it with the following:</span></span>
   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```

<span data-ttu-id="9b8de-246">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="9b8de-246">**Swift**:</span></span>

<span data-ttu-id="9b8de-247">앱 시작 시 동기화를 중지하려면 `viewDidLoad`의 **ToDoTableViewController.swift**에서 여기 표시된 두 줄을 주석 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-247">In `viewDidLoad`, in **ToDoTableViewController.swift**, comment out the two lines shown here, to stop syncing on app start.</span></span> <span data-ttu-id="9b8de-248">이 문서를 작성할 당시에는 Swift Todo 앱이 누군가가 항목을 추가하거나 완료할 때는 서비스를 업데이트하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-248">At the time of this writing, the Swift Todo app does not update the service when someone adds or completes an item.</span></span> <span data-ttu-id="9b8de-249">앱 시작 시에만 서비스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-249">It updates the service only on app start.</span></span>

   ```swift
  self.refreshControl?.beginRefreshing()
  self.onRefresh(self.refreshControl)
```

## <span data-ttu-id="9b8de-250"><a name="test-app"></a>앱 테스트</span><span class="sxs-lookup"><span data-stu-id="9b8de-250"><a name="test-app"></a>Test the app</span></span>
<span data-ttu-id="9b8de-251">이 섹션에서는 잘못된 URL에 연결하여 오프라인 시나리오를 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-251">In this section, you connect to an invalid URL to simulate an offline scenario.</span></span> <span data-ttu-id="9b8de-252">데이터 항목을 추가하면 모바일 앱 백 엔드와 동기화되지 않고 로컬 핵심 데이터 저장소에 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-252">When you add data items, they're held in the local Core Data store, but they're not synced with the mobile-app back end.</span></span>

1. <span data-ttu-id="9b8de-253">**QSTodoService.m**의 모바일 앱 URL을 잘못된 URL로 변경하고 앱 다시 실행하기:</span><span class="sxs-lookup"><span data-stu-id="9b8de-253">Change the mobile-app URL in **QSTodoService.m** to an invalid URL, and run the app again:</span></span>

   <span data-ttu-id="9b8de-254">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="9b8de-254">**Objective-C**.</span></span> <span data-ttu-id="9b8de-255">QSTodoService.m:</span><span class="sxs-lookup"><span data-stu-id="9b8de-255">In QSTodoService.m:</span></span>
   ```objc
   self.client = [MSClient clientWithApplicationURLString:@"https://sitename.azurewebsites.net.fail"];
   ```
   <span data-ttu-id="9b8de-256">**Swift**.</span><span class="sxs-lookup"><span data-stu-id="9b8de-256">**Swift**.</span></span> <span data-ttu-id="9b8de-257">ToDoTableViewController.swift:</span><span class="sxs-lookup"><span data-stu-id="9b8de-257">In ToDoTableViewController.swift:</span></span>
   ```swift
   let client = MSClient(applicationURLString: "https://sitename.azurewebsites.net.fail")
   ```
2. <span data-ttu-id="9b8de-258">몇 가지 할 일 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-258">Add some to-do items.</span></span> <span data-ttu-id="9b8de-259">시뮬레이터를 끝내고(또는 강제로 앱 닫기) 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-259">Quit the simulator (or forcibly close the app), and then restart it.</span></span> <span data-ttu-id="9b8de-260">변경 내용이 유지되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-260">Verify that your changes persist.</span></span>

3. <span data-ttu-id="9b8de-261">원격 **TodoItem** 테이블의 내용 확인:</span><span class="sxs-lookup"><span data-stu-id="9b8de-261">View the contents of the remote **TodoItem** table:</span></span>
   * <span data-ttu-id="9b8de-262">Node.js 백 엔드의 경우 [Azure Portal](https://portal.azure.com/)로 이동하여 모바일 앱 백 엔드에서 **간편한 테이블** > **TodoItem**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-262">For a Node.js back end, go to the [Azure portal](https://portal.azure.com/) and, in your mobile-app back end, click **Easy Tables** > **TodoItem**.</span></span>  
   * <span data-ttu-id="9b8de-263">.NET 백 엔드의 경우 SQL Server Management Studio와 같은 SQL 도구나 Fiddler 또는 Postman 같은 REST 클라이언트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-263">For a .NET back end, use either a SQL tool, such as SQL Server Management Studio, or a REST client, such as Fiddler or Postman.</span></span>  

4. <span data-ttu-id="9b8de-264">새 항목이 서버와 동기화되지 *않았는지* 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-264">Verify that the new items have *not* been synced with the server.</span></span>

5. <span data-ttu-id="9b8de-265">**QSTodoService.m**에서 URL을 올바르게 다시 변경하고 앱을 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-265">Change the URL back to the correct one in **QSTodoService.m**, and rerun the app.</span></span>

6. <span data-ttu-id="9b8de-266">항목 목록을 아래로 끌어서 새로 고침 제스처를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-266">Perform the refresh gesture by pulling down the list of items.</span></span>  
<span data-ttu-id="9b8de-267">진행률 회전자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-267">A progress spinner is displayed.</span></span>

7. <span data-ttu-id="9b8de-268">**TodoItem** 데이터를 다시 봅니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-268">View the **TodoItem** data again.</span></span> <span data-ttu-id="9b8de-269">새로운 할 일 및 변경된 할 일 항목이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-269">The new and changed to-do items should now be displayed.</span></span>

## <a name="summary"></a><span data-ttu-id="9b8de-270">요약</span><span class="sxs-lookup"><span data-stu-id="9b8de-270">Summary</span></span>
<span data-ttu-id="9b8de-271">오프라인 동기화 기능을 지원하기 위해 `MSSyncTable` 인터페이스를 사용하고 로컬 저장소를 사용하여 `MSClient.syncContext`를 초기화했습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-271">To support the offline sync feature, we used the `MSSyncTable` interface and initialized `MSClient.syncContext` with a local store.</span></span> <span data-ttu-id="9b8de-272">이 경우 로컬 저장소는 핵심 데이터 기반 데이터베이스였습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-272">In this case, the local store was a Core Data-based database.</span></span>

<span data-ttu-id="9b8de-273">핵심 데이터 로컬 저장소를 사용할 경우 [올바른 시스템 속성](#review-core-data)을 사용하여 여러 테이블을 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-273">When you use a Core Data local store, you must define several tables with the [correct system properties](#review-core-data).</span></span>

<span data-ttu-id="9b8de-274">Mobile Apps에 대한 정상적인 만들기, 읽기, 업데이트 및 삭제(CRUD) 작업은 앱이 계속 연결되어 있는 것처럼 작동하지만 모든 작업은 로컬 저장소에 대해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-274">The normal create, read, update, and delete (CRUD) operations for mobile apps work as if the app is still connected, but all the operations occur against the local store.</span></span>

<span data-ttu-id="9b8de-275">로컬 저장소를 서버와 동기화할 때 **MSSyncTable.pullWithQuery** 메서드를 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8de-275">When we synchronized the local store with the server, we used the **MSSyncTable.pullWithQuery** method.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9b8de-276">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="9b8de-276">Additional resources</span></span>
* <span data-ttu-id="9b8de-277">[Mobile Apps에서 오프라인 데이터 동기화]</span><span class="sxs-lookup"><span data-stu-id="9b8de-277">[Offline Data Sync in Mobile Apps]</span></span>
* <span data-ttu-id="9b8de-278">[클라우드 커버: Azure Mobile Services에서 오프라인 동기화] \(비디오는 Mobile Services에 대한 내용이지만 Mobile Apps 오프라인 동기화도 유사한 방식으로 작동합니다.\)</span><span class="sxs-lookup"><span data-stu-id="9b8de-278">[Cloud Cover: Offline Sync in Azure Mobile Services] \(The video is about Mobile Services, but Mobile Apps offline sync works in a similar way.\)</span></span>

<!-- URLs. -->


<span data-ttu-id="9b8de-279">[iOS 앱 만들기]: app-service-mobile-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="9b8de-279">[Create an iOS App]: app-service-mobile-ios-get-started.md</span></span>
<span data-ttu-id="9b8de-280">[Mobile Apps에서 오프라인 데이터 동기화]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="9b8de-280">[Offline Data Sync in Mobile Apps]: app-service-mobile-offline-data-sync.md</span></span>

[defining-core-data-tableoperationerrors-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperationerrors-entity.png
[defining-core-data-tableoperations-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperations-entity.png
[defining-core-data-tableconfig-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableconfig-entity.png
[defining-core-data-todoitem-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-todoitem-entity.png

<span data-ttu-id="9b8de-281">[클라우드 커버: Azure Mobile Services에서 오프라인 동기화]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri</span><span class="sxs-lookup"><span data-stu-id="9b8de-281">[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri</span></span>
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/en-us/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/
