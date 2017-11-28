---
title: "iOS 모바일 앱 aaaEnable 오프 라인 동기화 | Microsoft Docs"
description: "자세한 내용은 방법 toouse Azure 앱 서비스 모바일 앱 toocache 및 동기화 오프 라인 iOS 응용 프로그램의 데이터입니다."
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
ms.openlocfilehash: 570ea7cf6694ab7317c977331038929b64508ad3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-syncing-with-ios-mobile-apps"></a><span data-ttu-id="e1909-103">iOS 모바일 앱으로 오프라인 동기화 사용</span><span class="sxs-lookup"><span data-stu-id="e1909-103">Enable offline syncing with iOS mobile apps</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="e1909-104">개요</span><span class="sxs-lookup"><span data-stu-id="e1909-104">Overview</span></span>
<span data-ttu-id="e1909-105">이 자습서에서는 iOS 용 Azure 앱 서비스의 hello 모바일 앱 기능을 오프 라인 상태와 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-105">This tutorial covers offline syncing with hello Mobile Apps feature of Azure App Service for iOS.</span></span> <span data-ttu-id="e1909-106">오프 라인 동기화 최종 사용자와 수 모바일 앱 tooview와 상호 작용, 추가 또는 네트워크 연결이 없을 때에 데이터를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-106">With offline syncing end-users can interact with a mobile app tooview, add, or modify data, even when they have no network connection.</span></span> <span data-ttu-id="e1909-107">변경 내용은 로컬 데이터베이스에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-107">Changes are stored in a local database.</span></span> <span data-ttu-id="e1909-108">Hello 장치를 다시 온라인 상태가 되 면 hello 원격 백 엔드에서 hello 변경 내용이 동기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-108">After hello device is back online, hello changes are synced with hello remote back end.</span></span>

<span data-ttu-id="e1909-109">모바일 앱의 첫 번째 사용 환경을 경우 먼저 hello 자습서를 완료 해야 [iOS 앱 만들기]합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-109">If this is your first experience with Mobile Apps, you should first complete hello tutorial [Create an iOS App].</span></span> <span data-ttu-id="e1909-110">다운로드 한 hello 서버 빠른 시작 프로젝트를 사용 하지 않는 경우에 hello 데이터 액세스 확장 패키지 tooyour 프로젝트를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-110">If you do not use hello downloaded quick-start server project, you must add hello data-access extension packages tooyour project.</span></span> <span data-ttu-id="e1909-111">서버 확장 패키지에 대 한 자세한 내용은 참조 [Azure 모바일 앱에 대 한 hello.NET 백 엔드 서버 SDK에서 작동](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-111">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="e1909-112">hello 오프 라인 동기화 기능에 대해 자세히 toolearn 참조 [모바일 앱에서 데이터 동기화를 오프 라인]합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-112">toolearn more about hello offline sync feature, see [Offline Data Sync in Mobile Apps].</span></span>

## <span data-ttu-id="e1909-113"><a name="review-sync"></a>Hello 클라이언트 동기화 코드를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-113"><a name="review-sync"></a>Review hello client sync code</span></span>
<span data-ttu-id="e1909-114">hello에 대 한 다운로드 한 hello client 프로젝트 [iOS 앱 만들기] 자습서 로컬 핵심 데이터를 기반으로 데이터베이스를 사용 하 여 오프 라인 동기화를 지 원하는 코드를 이미 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-114">hello client project that you downloaded for hello [Create an iOS App] tutorial already contains code that supports offline synchronization using a local Core Data-based database.</span></span> <span data-ttu-id="e1909-115">이 섹션에서는 이미 hello 자습서 코드에 포함 되어 요약 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-115">This section summarizes what is already included in hello tutorial code.</span></span> <span data-ttu-id="e1909-116">Hello 기능의 개념적인 개요를 참조 하십시오. [모바일 앱에서 데이터 동기화를 오프 라인]합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-116">For a conceptual overview of hello feature, see [Offline Data Sync in Mobile Apps].</span></span>

<span data-ttu-id="e1909-117">모바일 앱의 hello 오프 라인 데이터 동기화 기능을 사용 하 여, 최종 사용자에 게 상호 작용할 수 로컬 데이터베이스와 hello 네트워크에 액세스할 수 없는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-117">Using hello offline data-sync feature of Mobile Apps, end-users can interact with a local database even when hello network is inaccessible.</span></span> <span data-ttu-id="e1909-118">toouse의 hello 동기화 컨텍스트를 초기화 하면 응용 프로그램에서 이러한 기능을 `MSClient` 로컬 저장소를 참조 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-118">toouse these features in your app, you initialize hello sync context of `MSClient` and reference a local store.</span></span> <span data-ttu-id="e1909-119">Hello 통해 테이블을 참조 합니다 **MSSyncTable** 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-119">Then you reference your table through hello **MSSyncTable** interface.</span></span>

<span data-ttu-id="e1909-120">**QSTodoService.m** (Objective-c) 또는 **ToDoTableViewController.swift** (빠른) 구성 요소 개발자는 hello 멤버 유형을 hello **syncTable** 은  **MSSyncTable**합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-120">In **QSTodoService.m** (Objective-C) or **ToDoTableViewController.swift** (Swift), notice that hello type of hello member **syncTable** is **MSSyncTable**.</span></span> <span data-ttu-id="e1909-121">오프라인 동기화에는 **MSTable** 대신 이 동기화 테이블 인터페이스가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-121">Offline sync uses this sync table interface instead of **MSTable**.</span></span> <span data-ttu-id="e1909-122">동기화 테이블을 사용 하는 경우 모든 작업 toohello 로컬 저장소를 이동 하 고 명시적 푸시를 통한 원격 백 엔드 hello와만 동기화 및 끌어오기 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-122">When a sync table is used, all operations go toohello local store and are synchronized only with hello remote back end with explicit push and pull operations.</span></span>

 <span data-ttu-id="e1909-123">hello를 사용 하 여 참조 tooa 동기화 테이블 tooget **syncTableWithName** 메서드를 `MSClient`합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-123">tooget a reference tooa sync table, use hello **syncTableWithName** method on `MSClient`.</span></span> <span data-ttu-id="e1909-124">tooremove 오프 라인 동기화 기능을 사용 하 여 **tableWithName** 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-124">tooremove offline sync functionality, use **tableWithName** instead.</span></span>

<span data-ttu-id="e1909-125">모든 테이블 작업을 수행할 수 있습니다, 전에 hello 로컬 저장소를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-125">Before any table operations can be performed, hello local store must be initialized.</span></span> <span data-ttu-id="e1909-126">Hello 관련 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-126">Here is hello relevant code:</span></span>

* <span data-ttu-id="e1909-127">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="e1909-127">**Objective-C**.</span></span> <span data-ttu-id="e1909-128">Hello에 **QSTodoService.init** 메서드:</span><span class="sxs-lookup"><span data-stu-id="e1909-128">In hello **QSTodoService.init** method:</span></span>

   ```objc
   MSCoreDataStore *store = [[MSCoreDataStore alloc] initWithManagedObjectContext:context];
   self.client.syncContext = [[MSSyncContext alloc] initWithDelegate:nil dataSource:store callback:nil];
   ```    
* <span data-ttu-id="e1909-129">**Swift**.</span><span class="sxs-lookup"><span data-stu-id="e1909-129">**Swift**.</span></span> <span data-ttu-id="e1909-130">Hello에 **ToDoTableViewController.viewDidLoad** 메서드:</span><span class="sxs-lookup"><span data-stu-id="e1909-130">In hello **ToDoTableViewController.viewDidLoad** method:</span></span>

   ```swift
   let client = MSClient(applicationURLString: "http:// ...") // URI of hello Mobile App
   let managedObjectContext = (UIApplication.sharedApplication().delegate as! AppDelegate).managedObjectContext!
   self.store = MSCoreDataStore(managedObjectContext: managedObjectContext)
   client.syncContext = MSSyncContext(delegate: nil, dataSource: self.store, callback: nil)
   ```
   <span data-ttu-id="e1909-131">이 메서드는 hello를 사용 하 여 로컬 저장소를 만듭니다 `MSCoreDataStore` 인터페이스 hello 모바일 앱 SDK를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-131">This method creates a local store by using hello `MSCoreDataStore` interface, which hello Mobile Apps SDK provides.</span></span> <span data-ttu-id="e1909-132">또는 hello를 구현 하 여 서로 다른 로컬 저장소를 제공할 수 `MSSyncContextDataSource` 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-132">Alternatively, you can provide a different local store by implementing hello `MSSyncContextDataSource` protocol.</span></span> <span data-ttu-id="e1909-133">또한 첫 번째 매개 변수를 hello **MSSyncContext** 은 사용 되는 toospecify 충돌 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-133">Also, hello first parameter of **MSSyncContext** is used toospecify a conflict handler.</span></span> <span data-ttu-id="e1909-134">지났으므로 `nil`를 얻을 수 있는 hello 기본 충돌 처리기는 모든 충돌에 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-134">Because we have passed `nil`, we get hello default conflict handler, which fails on any conflict.</span></span>

<span data-ttu-id="e1909-135">이제 보겠습니다 hello 실제 동기화 작업을 수행 하 고 hello 원격 백 엔드에서 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-135">Now, let's perform hello actual sync operation, and get data from hello remote back end:</span></span>

* <span data-ttu-id="e1909-136">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="e1909-136">**Objective-C**.</span></span> <span data-ttu-id="e1909-137">`syncData`먼저 새 변경 내용을 푸시하고 다음 호출 **pullData** hello 원격 백 엔드에서 tooget 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-137">`syncData` first pushes new changes and then calls **pullData** tooget data from hello remote back end.</span></span> <span data-ttu-id="e1909-138">Hello 차례로 **pullData** 메서드는 쿼리와 일치 하는 새 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-138">In turn, hello **pullData** method gets new data that matches a query:</span></span>

   ```objc
   -(void)syncData:(QSCompletionBlock)completion
   {
       // Push all changes in hello sync context, and then pull new data.
       [self.client.syncContext pushWithCompletion:^(NSError *error) {
           [self logErrorIfNotNil:error];
           [self pullData:completion];
       }];
   }

   -(void)pullData:(QSCompletionBlock)completion
   {
       MSQuery *query = [self.syncTable query];

       // Pulls data from hello remote server into hello local table.
       // We're pulling all items and filtering in hello view.
       // Query ID is used for incremental sync.
       [self.syncTable pullWithQuery:query queryId:@"allTodoItems" completion:^(NSError *error) {
           [self logErrorIfNotNil:error];

           // Lets hello caller know that we have finished.
           if (completion != nil) {
               dispatch_async(dispatch_get_main_queue(), completion);
           }
       }];
   }
   ```
* <span data-ttu-id="e1909-139">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="e1909-139">**Swift**:</span></span>
   ```swift
   func onRefresh(sender: UIRefreshControl!) {
      UIApplication.sharedApplication().networkActivityIndicatorVisible = true

      self.table!.pullWithQuery(self.table?.query(), queryId: "AllRecords") {
          (error) -> Void in

          UIApplication.sharedApplication().networkActivityIndicatorVisible = false

          if error != nil {
              // A real application would handle various errors like network conditions,
              // server conflicts, etc via hello MSSyncContextDelegate
              print("Error: \(error!.description)")

              // We will discard our changes and keep hello server's copy for simplicity
              if let opErrors = error!.userInfo[MSErrorPushResultKey] as? Array<MSTableOperationError> {
                  for opError in opErrors {
                      print("Attempted operation tooitem \(opError.itemId)")
                      if (opError.operation == .Insert || opError.operation == .Delete) {
                          print("Insert/Delete, failed discarding changes")
                          opError.cancelOperationAndDiscardItemWithCompletion(nil)
                      } else {
                          print("Update failed, reverting tooserver's copy")
                          opError.cancelOperationAndUpdateItem(opError.serverItem!, completion: nil)
                      }
                  }
              }
          }
          self.refreshControl?.endRefreshing()
      }
   }
   ```

<span data-ttu-id="e1909-140">Objective C hello 버전에서에서 `syncData`를 먼저 호출 **pushWithCompletion** hello 동기화 컨텍스트에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-140">In hello Objective-C version, in `syncData`, we first call **pushWithCompletion** on hello sync context.</span></span> <span data-ttu-id="e1909-141">이 메서드는의 구성원 `MSSyncContext` (및 hello 동기화 테이블이 아니라 자체) 이므로 모든 테이블에서 변경 내용을 밀어냅니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-141">This method is a member of `MSSyncContext` (and not hello sync table itself) because it pushes changes across all tables.</span></span> <span data-ttu-id="e1909-142">로컬 (작업을 통해 CUD) 어떤 방식으로든에서 수정 된 레코드만 toohello 서버에 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-142">Only records that have been modified in some way locally (through CUD operations) are sent toohello server.</span></span> <span data-ttu-id="e1909-143">그런 다음 도우미 hello **pullData** 가 호출 되는 호출 **MSSyncTable.pullWithQuery** tooretrieve 원격 데이터 hello 로컬 데이터베이스에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-143">Then hello helper **pullData** is called, which calls **MSSyncTable.pullWithQuery** tooretrieve remote data and store it in hello local database.</span></span>

<span data-ttu-id="e1909-144">Hello Swift 버전에서 hello 푸시 작업에 반드시 필요 없기 때문에 호출이 없습니다 너무**pushWithCompletion**합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-144">In hello Swift version, because hello push operation was not strictly necessary, there is no call too**pushWithCompletion**.</span></span> <span data-ttu-id="e1909-145">푸시 작업을 수행 하는 hello 테이블에 대 한 동기화 컨텍스트 hello에에서 보류 중인 변경 내용을 없으면 끌어오기 항상 발급 푸시를 먼저 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-145">If there are any changes pending in hello sync context for hello table that is doing a push operation, pull always issues a push first.</span></span> <span data-ttu-id="e1909-146">그러나 여러 개의 동기화 테이블, 있는 경우 최상의 tooexplicitly 호출 푸시 tooensure를 일관 된 관련된 테이블 간에 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-146">However, if you have more than one sync table, it is best tooexplicitly call push tooensure that everything is consistent across related tables.</span></span>

<span data-ttu-id="e1909-147">Objective C hello 및 Swift 버전 모두에 hello를 사용할 수 있습니다 **pullWithQuery** 메서드 toospecify 쿼리 toofilter hello tooretrieve 원하는 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-147">In both hello Objective-C and Swift versions, you can use hello **pullWithQuery** method toospecify a query toofilter hello records you want tooretrieve.</span></span> <span data-ttu-id="e1909-148">이 예제에서는 hello 쿼리 검색 hello 원격에 있는 모든 레코드 `TodoItem` 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-148">In this example, hello query retrieves all records in hello remote `TodoItem` table.</span></span>

<span data-ttu-id="e1909-149">두 번째 매개 변수를 hello **pullWithQuery** 에 사용 되는 쿼리 id로 *증분 동기화*합니다. 증분 동기화 hello 레코드를 사용 하 여 hello 마지막 동기화 이후 수정 된 레코드만 검색 `UpdatedAt` 타임 스탬프 (호출 `updatedAt` hello 로컬 저장소에) hello 쿼리 ID의 논리적 쿼리마다 고유한 설명이 포함 된 문자열 이어야 합니다 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-149">hello second parameter of **pullWithQuery** is a query ID that is used for *incremental sync*. Incremental sync retrieves only records that were modified since hello last sync, using hello record's `UpdatedAt` time stamp (called `updatedAt` in hello local store.) hello query ID should be a descriptive string that is unique for each logical query in your app.</span></span> <span data-ttu-id="e1909-150">tooopt 증분 비동기화 전달 `nil` 대로 hello 쿼리 id입니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-150">tooopt out of incremental sync, pass `nil` as hello query ID.</span></span> <span data-ttu-id="e1909-151">이런 방법은 각각의 끌어오기 작업에서 모든 레코드가 검색되므로 비효율적일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-151">This approach can be potentially inefficient, because it retrieves all records on each pull operation.</span></span>

<span data-ttu-id="e1909-152">hello Objective C 응용 프로그램을 수정 또는 사용자 hello 새로 고침 제스처를 수행 하면 데이터를 추가 및 실행에 동기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-152">hello Objective-C app syncs when you modify or add data, when a user performs hello refresh gesture, and on launch.</span></span>

<span data-ttu-id="e1909-153">hello Swift 앱 hello 사용자 hello 새로 고침 제스처를 수행 하는 경우 및 실행에 동기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-153">hello Swift app syncs when hello user performs hello refresh gesture and on launch.</span></span>

<span data-ttu-id="e1909-154">Hello 앱 동기화 경우 언제 든 지 데이터 수정 (Objective-c) 또는 (Swift 및 Objective-c) hello 앱 시작 될 때마다 해당 hello 사용자가 온라인 상태 hello 앱 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-154">Because hello app syncs whenever data is modified (Objective-C) or whenever hello app starts (Objective-C and Swift), hello app assumes that hello user is online.</span></span> <span data-ttu-id="e1909-155">이후 섹션에서 오프 라인 상태일 경우에 사용자가 편집할 수 있도록 hello 앱을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-155">In a later section, you will update hello app so that users can edit even when they are offline.</span></span>

## <span data-ttu-id="e1909-156"><a name="review-core-data"></a>검토 hello 코어 데이터 모델</span><span class="sxs-lookup"><span data-stu-id="e1909-156"><a name="review-core-data"></a>Review hello Core Data model</span></span>
<span data-ttu-id="e1909-157">Hello 핵심 데이터 오프 라인 저장소를 사용 하면 데이터 모델의 특정 테이블 및 필드를 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-157">When you use hello Core Data offline store, you must define particular tables and fields in your data model.</span></span> <span data-ttu-id="e1909-158">hello 샘플 응용 프로그램에는 hello 정렬 형식 사용 하 여 데이터 모델을 이미 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-158">hello sample app already includes a data model with hello right format.</span></span> <span data-ttu-id="e1909-159">이 섹션에서는 연습 이러한 테이블 tooshow 용도입니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-159">In this section, we walk through these tables tooshow how they are used.</span></span>

<span data-ttu-id="e1909-160">**QSDataModel.xcdatamodeld**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-160">Open **QSDataModel.xcdatamodeld**.</span></span> <span data-ttu-id="e1909-161">4 개 테이블은 SDK에서 사용 되는 3 개의 hello 정의-및 자체 하나 hello 할 일에 사용 되는 항목:</span><span class="sxs-lookup"><span data-stu-id="e1909-161">Four tables are defined--three that are used by hello SDK and one that's used for hello to-do items themselves:</span></span>
  * <span data-ttu-id="e1909-162">MS_TableOperations: 트랙 hello toobe hello 서버와 동기화 해야 하는 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-162">MS_TableOperations: Tracks hello items that need toobe synchronized with hello server.</span></span>
  * <span data-ttu-id="e1909-163">MS_TableOperationErrors: 오프라인 동기화 중에 발생하는 모든 오류를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-163">MS_TableOperationErrors: Tracks any errors that happen during offline synchronization.</span></span>
  * <span data-ttu-id="e1909-164">MS_TableConfig: 트랙 hello hello 모든 끌어오기 작업에 대해 마지막 동기화 작업에 대 한 마지막 업데이트 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-164">MS_TableConfig: Tracks hello last updated time for hello last sync operation for all pull operations.</span></span>
  * <span data-ttu-id="e1909-165">TodoItem: hello 할 일 항목을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-165">TodoItem: Stores hello to-do items.</span></span> <span data-ttu-id="e1909-166">시스템 열 hello **createdAt**, **updatedAt**, 및 **버전** 선택적인 시스템 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-166">hello system columns **createdAt**, **updatedAt**, and **version** are optional system properties.</span></span>

> [!NOTE]
> <span data-ttu-id="e1909-167">모바일 앱 SDK hello로 시작 하는 열 이름을 예약 "**``**"입니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-167">hello Mobile Apps SDK reserves column names that begin with "**``**".</span></span> <span data-ttu-id="e1909-168">시스템 열 이외에 이 접두사를 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="e1909-168">Do not use this prefix with anything other than system columns.</span></span> <span data-ttu-id="e1909-169">그렇지 않으면 원격 백 엔드 hello를 사용 하는 경우 열 이름은 수정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-169">Otherwise, your column names are modified when you use hello remote back end.</span></span>
>
>

<span data-ttu-id="e1909-170">Hello 오프 라인 동기화 기능을 사용 하 여 hello 3 개의 시스템 테이블 및 hello 데이터 테이블을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-170">When you use hello offline sync feature, define hello three system tables and hello data table.</span></span>

### <a name="system-tables"></a><span data-ttu-id="e1909-171">시스템 테이블</span><span class="sxs-lookup"><span data-stu-id="e1909-171">System tables</span></span>

<span data-ttu-id="e1909-172">**MS_TableOperations**</span><span class="sxs-lookup"><span data-stu-id="e1909-172">**MS_TableOperations**</span></span>  

![MS_TableOperations 테이블 특성][defining-core-data-tableoperations-entity]

| <span data-ttu-id="e1909-174">특성</span><span class="sxs-lookup"><span data-stu-id="e1909-174">Attribute</span></span> | <span data-ttu-id="e1909-175">형식</span><span class="sxs-lookup"><span data-stu-id="e1909-175">Type</span></span> |
| --- | --- |
| <span data-ttu-id="e1909-176">id</span><span class="sxs-lookup"><span data-stu-id="e1909-176">id</span></span> | <span data-ttu-id="e1909-177">정수 64</span><span class="sxs-lookup"><span data-stu-id="e1909-177">Integer 64</span></span> |
| <span data-ttu-id="e1909-178">itemId</span><span class="sxs-lookup"><span data-stu-id="e1909-178">itemId</span></span> | <span data-ttu-id="e1909-179">String</span><span class="sxs-lookup"><span data-stu-id="e1909-179">String</span></span> |
| <span data-ttu-id="e1909-180">properties</span><span class="sxs-lookup"><span data-stu-id="e1909-180">properties</span></span> | <span data-ttu-id="e1909-181">이진 데이터</span><span class="sxs-lookup"><span data-stu-id="e1909-181">Binary Data</span></span> |
| <span data-ttu-id="e1909-182">테이블</span><span class="sxs-lookup"><span data-stu-id="e1909-182">table</span></span> | <span data-ttu-id="e1909-183">String</span><span class="sxs-lookup"><span data-stu-id="e1909-183">String</span></span> |
| <span data-ttu-id="e1909-184">tableKind</span><span class="sxs-lookup"><span data-stu-id="e1909-184">tableKind</span></span> | <span data-ttu-id="e1909-185">정수 16</span><span class="sxs-lookup"><span data-stu-id="e1909-185">Integer 16</span></span> |


<span data-ttu-id="e1909-186">**MS_TableOperationErrors**</span><span class="sxs-lookup"><span data-stu-id="e1909-186">**MS_TableOperationErrors**</span></span>

 ![MS_TableOperationErrors 테이블 특성][defining-core-data-tableoperationerrors-entity]

| <span data-ttu-id="e1909-188">특성</span><span class="sxs-lookup"><span data-stu-id="e1909-188">Attribute</span></span> | <span data-ttu-id="e1909-189">형식</span><span class="sxs-lookup"><span data-stu-id="e1909-189">Type</span></span> |
| --- | --- |
| <span data-ttu-id="e1909-190">id</span><span class="sxs-lookup"><span data-stu-id="e1909-190">id</span></span> |<span data-ttu-id="e1909-191">문자열</span><span class="sxs-lookup"><span data-stu-id="e1909-191">String</span></span> |
| <span data-ttu-id="e1909-192">operationId</span><span class="sxs-lookup"><span data-stu-id="e1909-192">operationId</span></span> |<span data-ttu-id="e1909-193">정수 64</span><span class="sxs-lookup"><span data-stu-id="e1909-193">Integer 64</span></span> |
| <span data-ttu-id="e1909-194">properties</span><span class="sxs-lookup"><span data-stu-id="e1909-194">properties</span></span> |<span data-ttu-id="e1909-195">이진 데이터</span><span class="sxs-lookup"><span data-stu-id="e1909-195">Binary Data</span></span> |
| <span data-ttu-id="e1909-196">tableKind</span><span class="sxs-lookup"><span data-stu-id="e1909-196">tableKind</span></span> |<span data-ttu-id="e1909-197">정수 16</span><span class="sxs-lookup"><span data-stu-id="e1909-197">Integer 16</span></span> |

 <span data-ttu-id="e1909-198">**MS_TableConfig**</span><span class="sxs-lookup"><span data-stu-id="e1909-198">**MS_TableConfig**</span></span>

 ![][defining-core-data-tableconfig-entity]

| <span data-ttu-id="e1909-199">특성</span><span class="sxs-lookup"><span data-stu-id="e1909-199">Attribute</span></span> | <span data-ttu-id="e1909-200">형식</span><span class="sxs-lookup"><span data-stu-id="e1909-200">Type</span></span> |
| --- | --- |
| <span data-ttu-id="e1909-201">id</span><span class="sxs-lookup"><span data-stu-id="e1909-201">id</span></span> |<span data-ttu-id="e1909-202">문자열</span><span class="sxs-lookup"><span data-stu-id="e1909-202">String</span></span> |
| <span data-ttu-id="e1909-203">key</span><span class="sxs-lookup"><span data-stu-id="e1909-203">key</span></span> |<span data-ttu-id="e1909-204">String</span><span class="sxs-lookup"><span data-stu-id="e1909-204">String</span></span> |
| <span data-ttu-id="e1909-205">keyType</span><span class="sxs-lookup"><span data-stu-id="e1909-205">keyType</span></span> |<span data-ttu-id="e1909-206">정수 64</span><span class="sxs-lookup"><span data-stu-id="e1909-206">Integer 64</span></span> |
| <span data-ttu-id="e1909-207">테이블</span><span class="sxs-lookup"><span data-stu-id="e1909-207">table</span></span> |<span data-ttu-id="e1909-208">String</span><span class="sxs-lookup"><span data-stu-id="e1909-208">String</span></span> |
| <span data-ttu-id="e1909-209">값</span><span class="sxs-lookup"><span data-stu-id="e1909-209">value</span></span> |<span data-ttu-id="e1909-210">문자열</span><span class="sxs-lookup"><span data-stu-id="e1909-210">String</span></span> |

### <a name="data-table"></a><span data-ttu-id="e1909-211">데이터 테이블</span><span class="sxs-lookup"><span data-stu-id="e1909-211">Data table</span></span>

<span data-ttu-id="e1909-212">**TodoItem**</span><span class="sxs-lookup"><span data-stu-id="e1909-212">**TodoItem**</span></span>

| <span data-ttu-id="e1909-213">특성</span><span class="sxs-lookup"><span data-stu-id="e1909-213">Attribute</span></span> | <span data-ttu-id="e1909-214">유형</span><span class="sxs-lookup"><span data-stu-id="e1909-214">Type</span></span> | <span data-ttu-id="e1909-215">참고</span><span class="sxs-lookup"><span data-stu-id="e1909-215">Note</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e1909-216">id</span><span class="sxs-lookup"><span data-stu-id="e1909-216">id</span></span> | <span data-ttu-id="e1909-217">문자열, 필수로 표시</span><span class="sxs-lookup"><span data-stu-id="e1909-217">String, marked required</span></span> |<span data-ttu-id="e1909-218">원격 저장소의 기본 키</span><span class="sxs-lookup"><span data-stu-id="e1909-218">Primary key in remote store</span></span> |
| <span data-ttu-id="e1909-219">complete</span><span class="sxs-lookup"><span data-stu-id="e1909-219">complete</span></span> | <span data-ttu-id="e1909-220">Boolean</span><span class="sxs-lookup"><span data-stu-id="e1909-220">Boolean</span></span> | <span data-ttu-id="e1909-221">할 일 항목 필드</span><span class="sxs-lookup"><span data-stu-id="e1909-221">To-do item field</span></span> |
| <span data-ttu-id="e1909-222">텍스트</span><span class="sxs-lookup"><span data-stu-id="e1909-222">text</span></span> |<span data-ttu-id="e1909-223">String</span><span class="sxs-lookup"><span data-stu-id="e1909-223">String</span></span> |<span data-ttu-id="e1909-224">할 일 항목 필드</span><span class="sxs-lookup"><span data-stu-id="e1909-224">To-do item field</span></span> |
| <span data-ttu-id="e1909-225">createdAt</span><span class="sxs-lookup"><span data-stu-id="e1909-225">createdAt</span></span> | <span data-ttu-id="e1909-226">Date</span><span class="sxs-lookup"><span data-stu-id="e1909-226">Date</span></span> | <span data-ttu-id="e1909-227">(선택 사항) 너무 매핑합니다**createdAt** 시스템 속성</span><span class="sxs-lookup"><span data-stu-id="e1909-227">(optional) Maps too**createdAt** system property</span></span> |
| <span data-ttu-id="e1909-228">updatedAt</span><span class="sxs-lookup"><span data-stu-id="e1909-228">updatedAt</span></span> | <span data-ttu-id="e1909-229">Date</span><span class="sxs-lookup"><span data-stu-id="e1909-229">Date</span></span> | <span data-ttu-id="e1909-230">(선택 사항) 너무 매핑합니다**updatedAt** 시스템 속성</span><span class="sxs-lookup"><span data-stu-id="e1909-230">(optional) Maps too**updatedAt** system property</span></span> |
| <span data-ttu-id="e1909-231">버전</span><span class="sxs-lookup"><span data-stu-id="e1909-231">version</span></span> | <span data-ttu-id="e1909-232">문자열</span><span class="sxs-lookup"><span data-stu-id="e1909-232">String</span></span> | <span data-ttu-id="e1909-233">(선택 사항) 사용 되는 toodetect 충돌, 지도 tooversion</span><span class="sxs-lookup"><span data-stu-id="e1909-233">(optional) Used toodetect conflicts, maps tooversion</span></span> |

## <span data-ttu-id="e1909-234"><a name="setup-sync"></a>Hello 응용 프로그램의 hello 동기화 동작을 변경</span><span class="sxs-lookup"><span data-stu-id="e1909-234"><a name="setup-sync"></a>Change hello sync behavior of hello app</span></span>
<span data-ttu-id="e1909-235">이 섹션에서는 응용 프로그램 시작 또는 삽입 하 고 항목을 업데이트 하는 경우에 동기화 되지 않는 되도록 hello 앱을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-235">In this section, you modify hello app so that it does not sync on app start or when you insert and update items.</span></span> <span data-ttu-id="e1909-236">Hello 새로 고침 제스처 단추 수행 될 때만 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-236">It syncs only when hello refresh gesture button is performed.</span></span>

<span data-ttu-id="e1909-237">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="e1909-237">**Objective-C**:</span></span>

1. <span data-ttu-id="e1909-238">**QSTodoListViewController.m**, hello 변경 **viewDidLoad** tooremove 메서드 호출을 너무 hello`[self refresh]` hello 메서드의 hello 끝입니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-238">In **QSTodoListViewController.m**, change hello **viewDidLoad** method tooremove hello call too`[self refresh]` at hello end of hello method.</span></span> <span data-ttu-id="e1909-239">이제 hello 데이터 응용 프로그램 시작 시 hello 서버와 동기화 되지 않은 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-239">Now hello data is not synced with hello server on app start.</span></span> <span data-ttu-id="e1909-240">대신,이 hello 로컬 저장소의 hello 내용으로 동기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-240">Instead, it's synced with hello contents of hello local store.</span></span>
2. <span data-ttu-id="e1909-241">**QSTodoService.m**, hello 정의를 수정할 `addItem` hello 항목을 삽입 한 후 동기화 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-241">In **QSTodoService.m**, modify hello definition of `addItem` so that it doesn't sync after hello item is inserted.</span></span> <span data-ttu-id="e1909-242">Hello 제거 `self syncData` 차단 하 고 hello 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-242">Remove hello `self syncData` block and replace it with hello following:</span></span>

   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```
3. <span data-ttu-id="e1909-243">Hello 정의를 수정할 `completeItem` 앞서 언급 했 듯이 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-243">Modify hello definition of `completeItem` as mentioned previously.</span></span> <span data-ttu-id="e1909-244">에 대 한 hello 블록을 제거 `self syncData` hello 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-244">Remove hello block for `self syncData` and replace it with hello following:</span></span>
   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```

<span data-ttu-id="e1909-245">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="e1909-245">**Swift**:</span></span>

<span data-ttu-id="e1909-246">`viewDidLoad`에 **ToDoTableViewController.swift**, 응용 프로그램 시작에서 동기화 할 toostop 여기에 표시 된 hello 두 줄 주석 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-246">In `viewDidLoad`, in **ToDoTableViewController.swift**, comment out hello two lines shown here, toostop syncing on app start.</span></span> <span data-ttu-id="e1909-247">이 문서 작성 hello 시 hello Swift Todo 앱 때 업데이트 되지 않는다 hello 서비스를 다른 사용자를 추가 하거나 항목을 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-247">At hello time of this writing, hello Swift Todo app does not update hello service when someone adds or completes an item.</span></span> <span data-ttu-id="e1909-248">응용 프로그램 시작에 대해서만 hello 서비스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-248">It updates hello service only on app start.</span></span>

   ```swift
  self.refreshControl?.beginRefreshing()
  self.onRefresh(self.refreshControl)
```

## <span data-ttu-id="e1909-249"><a name="test-app"></a>Hello 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="e1909-249"><a name="test-app"></a>Test hello app</span></span>
<span data-ttu-id="e1909-250">이 섹션에서는 tooan 잘못 된 URL toosimulate 오프 라인 시나리오를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-250">In this section, you connect tooan invalid URL toosimulate an offline scenario.</span></span> <span data-ttu-id="e1909-251">보유 하는 데이터 항목을 추가할 때 hello 로컬 핵심 데이터 저장, 하지만 hello 모바일 앱 백 엔드에서 동기화 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-251">When you add data items, they're held in hello local Core Data store, but they're not synced with hello mobile-app back end.</span></span>

1. <span data-ttu-id="e1909-252">hello 모바일 앱 URL을 변경 **QSTodoService.m** tooan 잘못 된 URL 및 다시 실행된 hello 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="e1909-252">Change hello mobile-app URL in **QSTodoService.m** tooan invalid URL, and run hello app again:</span></span>

   <span data-ttu-id="e1909-253">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="e1909-253">**Objective-C**.</span></span> <span data-ttu-id="e1909-254">QSTodoService.m:</span><span class="sxs-lookup"><span data-stu-id="e1909-254">In QSTodoService.m:</span></span>
   ```objc
   self.client = [MSClient clientWithApplicationURLString:@"https://sitename.azurewebsites.net.fail"];
   ```
   <span data-ttu-id="e1909-255">**Swift**.</span><span class="sxs-lookup"><span data-stu-id="e1909-255">**Swift**.</span></span> <span data-ttu-id="e1909-256">ToDoTableViewController.swift:</span><span class="sxs-lookup"><span data-stu-id="e1909-256">In ToDoTableViewController.swift:</span></span>
   ```swift
   let client = MSClient(applicationURLString: "https://sitename.azurewebsites.net.fail")
   ```
2. <span data-ttu-id="e1909-257">몇 가지 할 일 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-257">Add some to-do items.</span></span> <span data-ttu-id="e1909-258">Hello 시뮬레이터 (또는 앱 강제 닫기 hello)를 끝낸 후 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-258">Quit hello simulator (or forcibly close hello app), and then restart it.</span></span> <span data-ttu-id="e1909-259">변경 내용이 유지되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-259">Verify that your changes persist.</span></span>

3. <span data-ttu-id="e1909-260">원격 hello hello 내용을 보는 **TodoItem** 테이블:</span><span class="sxs-lookup"><span data-stu-id="e1909-260">View hello contents of hello remote **TodoItem** table:</span></span>
   * <span data-ttu-id="e1909-261">Node.js 백 엔드에 대 한 이동 toohello [Azure 포털](https://portal.azure.com/) 모바일 앱 백 엔드에서 클릭 **쉽게 테이블** > **TodoItem**합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-261">For a Node.js back end, go toohello [Azure portal](https://portal.azure.com/) and, in your mobile-app back end, click **Easy Tables** > **TodoItem**.</span></span>  
   * <span data-ttu-id="e1909-262">.NET 백 엔드의 경우 SQL Server Management Studio와 같은 SQL 도구나 Fiddler 또는 Postman 같은 REST 클라이언트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-262">For a .NET back end, use either a SQL tool, such as SQL Server Management Studio, or a REST client, such as Fiddler or Postman.</span></span>  

4. <span data-ttu-id="e1909-263">Hello 새 항목이 있는지 확인 하십시오 *하지* 된 hello 서버와 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-263">Verify that hello new items have *not* been synced with hello server.</span></span>

5. <span data-ttu-id="e1909-264">변경 hello URL 백 toohello의 하나를 수정 **QSTodoService.m**, 응용 프로그램을 다시 실행된 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-264">Change hello URL back toohello correct one in **QSTodoService.m**, and rerun hello app.</span></span>

6. <span data-ttu-id="e1909-265">항목 목록이 hello hello 새로 고침 제스처를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-265">Perform hello refresh gesture by pulling down hello list of items.</span></span>  
<span data-ttu-id="e1909-266">진행률 회전자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-266">A progress spinner is displayed.</span></span>

7. <span data-ttu-id="e1909-267">보기 hello **TodoItem** 다시 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-267">View hello **TodoItem** data again.</span></span> <span data-ttu-id="e1909-268">hello 새로운 기능과 변경 된 할 일 항목이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-268">hello new and changed to-do items should now be displayed.</span></span>

## <a name="summary"></a><span data-ttu-id="e1909-269">요약</span><span class="sxs-lookup"><span data-stu-id="e1909-269">Summary</span></span>
<span data-ttu-id="e1909-270">hello 사용 toosupport hello 오프 라인 동기화 기능을 `MSSyncTable` 인터페이스 및 초기화 `MSClient.syncContext` 로컬 저장소와 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-270">toosupport hello offline sync feature, we used hello `MSSyncTable` interface and initialized `MSClient.syncContext` with a local store.</span></span> <span data-ttu-id="e1909-271">이 경우 hello 로컬 저장소에서 핵심 데이터 기반 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="e1909-271">In this case, hello local store was a Core Data-based database.</span></span>

<span data-ttu-id="e1909-272">Hello로 몇 개의 테이블을 정의 해야 핵심 데이터 로컬 저장소를 사용 하면 [시스템 속성을 수정](#review-core-data)합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-272">When you use a Core Data local store, you must define several tables with hello [correct system properties](#review-core-data).</span></span>

<span data-ttu-id="e1909-273">hello 보통 만들기, 읽기, 업데이트 및 삭제 (CRUD) 작업 모바일 앱은 작동에 대 한 hello 앱에 여전히 설정 되어 있지만 hello 로컬 저장소에 대해 발생 하는 모든 hello 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1909-273">hello normal create, read, update, and delete (CRUD) operations for mobile apps work as if hello app is still connected, but all hello operations occur against hello local store.</span></span>

<span data-ttu-id="e1909-274">Hello hello 서버와 hello 로컬 저장소를 동기화 했습니다 때 사용한 **MSSyncTable.pullWithQuery** 메서드.</span><span class="sxs-lookup"><span data-stu-id="e1909-274">When we synchronized hello local store with hello server, we used hello **MSSyncTable.pullWithQuery** method.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e1909-275">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="e1909-275">Additional resources</span></span>
* <span data-ttu-id="e1909-276">[모바일 앱에서 데이터 동기화를 오프 라인]</span><span class="sxs-lookup"><span data-stu-id="e1909-276">[Offline Data Sync in Mobile Apps]</span></span>
* <span data-ttu-id="e1909-277">[클라우드 기능: Azure 모바일 서비스에서 오프 라인 동기화] \(hello 비디오 모바일 서비스에 대 한 이지만 비슷한 방법으로 모바일 앱을 오프 라인 동기화 작동 합니다.\)</span><span class="sxs-lookup"><span data-stu-id="e1909-277">[Cloud Cover: Offline Sync in Azure Mobile Services] \(hello video is about Mobile Services, but Mobile Apps offline sync works in a similar way.\)</span></span>

<!-- URLs. -->


[iOS 앱 만들기]: app-service-mobile-ios-get-started.md
[모바일 앱에서 데이터 동기화를 오프 라인]: app-service-mobile-offline-data-sync.md

[defining-core-data-tableoperationerrors-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperationerrors-entity.png
[defining-core-data-tableoperations-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperations-entity.png
[defining-core-data-tableconfig-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableconfig-entity.png
[defining-core-data-todoitem-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-todoitem-entity.png

[클라우드 기능: Azure 모바일 서비스에서 오프 라인 동기화]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/en-us/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/
