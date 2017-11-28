---
title: "Azure 모바일 앱 (Android)에 대 한 aaaEnable 오프 라인 동기화"
description: "자세한 내용은 방법 toouse 앱 서비스 모바일 앱 toocache 및 동기화의에서 오프 라인 데이터 Android 응용 프로그램"
documentationcenter: android
author: ggailey777
manager: syntaxc4
services: app-service\mobile
ms.assetid: 32a8a079-9b3c-4faf-8588-ccff02097224
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 34508c7394610cf9127e1753637940826b8fd06a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-android-mobile-app"></a><span data-ttu-id="0044a-103">Android 모바일 앱에 대해 오프라인 동기화 사용</span><span class="sxs-lookup"><span data-stu-id="0044a-103">Enable offline sync for your Android mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="0044a-104">개요</span><span class="sxs-lookup"><span data-stu-id="0044a-104">Overview</span></span>
<span data-ttu-id="0044a-105">이 자습서에서는 Android 용 Azure 모바일 앱의 hello 오프 라인 동기화 기능을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0044a-105">This tutorial covers hello offline sync feature of Azure Mobile Apps for Android.</span></span> <span data-ttu-id="0044a-106">오프 라인 동기화 허용 모바일 앱과 함께 최종 사용자가 toointeract&mdash;보기, 추가 또는 데이터 수정&mdash;네트워크 연결이 없는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="0044a-106">Offline sync allows end users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="0044a-107">변경 내용은 로컬 데이터베이스에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="0044a-107">Changes are stored in a local database.</span></span> <span data-ttu-id="0044a-108">Hello 장치를 다시 온라인 상태가 되 면 hello 원격 백 엔드와 이러한 변경 내용이 동기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0044a-108">Once hello device is back online, these changes are synced with hello remote backend.</span></span>

<span data-ttu-id="0044a-109">Azure 모바일 앱의 첫 번째 사용 환경을 경우 먼저 hello 자습서를 완료 해야 [Android 앱 만들기]합니다.</span><span class="sxs-lookup"><span data-stu-id="0044a-109">If this is your first experience with Azure Mobile Apps, you should first complete hello tutorial [Create an Android App].</span></span> <span data-ttu-id="0044a-110">사용 하지 않는 경우 hello 퀵 스타트 서버 프로젝트를 다운로드, hello 데이터 액세스 확장 패키지 tooyour 프로젝트를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0044a-110">If you do not use hello downloaded quick start server project, you must add hello data access extension packages tooyour project.</span></span> <span data-ttu-id="0044a-111">서버 확장 패키지에 대 한 자세한 내용은 참조 [Azure 모바일 앱에 대 한 hello.NET 백 엔드 서버 SDK에서 작동](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0044a-111">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="0044a-112">hello 항목을 참조 하는 hello 오프 라인 동기화 기능에 대해 자세히 toolearn [Azure 모바일 앱에서 데이터 동기화를 오프 라인]합니다.</span><span class="sxs-lookup"><span data-stu-id="0044a-112">toolearn more about hello offline sync feature, see hello topic [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="update-hello-app-toosupport-offline-sync"></a><span data-ttu-id="0044a-113">Hello 앱 toosupport 오프 라인 동기화를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="0044a-113">Update hello app toosupport offline sync</span></span>
<span data-ttu-id="0044a-114">Tooand 쓰기에서 오프 라인 동기화와 함께 읽어는 *동기화 테이블* (hello를 사용 하 여 *IMobileServiceSyncTable* 인터페이스)에 포함 되어 있는 한 **SQLite** 장치에는 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="0044a-114">With offline sync, you read tooand write from a *sync table* (using hello *IMobileServiceSyncTable* interface), which is part of a **SQLite** database on your device.</span></span>

<span data-ttu-id="0044a-115">컴퓨터에 사용 된 hello 장치와 Azure 모바일 서비스 간의 toopush 및 끌어오기 변경은 *동기화 컨텍스트* (*MobileServiceClient.SyncContext*), hello 로컬 데이터베이스와 함께 초기화는 로컬로 toostore 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="0044a-115">toopush and pull changes between hello device and Azure Mobile Services, you use a *synchronization context* (*MobileServiceClient.SyncContext*), which you initialize with hello local database toostore data locally.</span></span>

1. <span data-ttu-id="0044a-116">`TodoActivity.java`, hello 기존 정의의 주석 `mToDoTable` hello 동기화 테이블 버전에서 주석 처리 제거:</span><span class="sxs-lookup"><span data-stu-id="0044a-116">In `TodoActivity.java`, comment out hello existing definition of `mToDoTable` and uncomment hello sync table version:</span></span>
   
        private MobileServiceSyncTable<ToDoItem> mToDoTable;
2. <span data-ttu-id="0044a-117">Hello에 `onCreate` 메서드를 기존 초기화 hello 주석 `mToDoTable` 이 정의 주석 처리 제거:</span><span class="sxs-lookup"><span data-stu-id="0044a-117">In hello `onCreate` method, comment out hello existing initialization of `mToDoTable` and uncomment this definition:</span></span>
   
        mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
3. <span data-ttu-id="0044a-118">`refreshItemsFromTable` hello 정의의 주석 `results` 이 정의 주석 처리 제거:</span><span class="sxs-lookup"><span data-stu-id="0044a-118">In `refreshItemsFromTable` comment out hello definition of `results` and uncomment this definition:</span></span>
   
        // Offline Sync
        final List<ToDoItem> results = refreshItemsFromMobileServiceTableSyncTable();
4. <span data-ttu-id="0044a-119">Hello 정의의 주석 `refreshItemsFromMobileServiceTable`합니다.</span><span class="sxs-lookup"><span data-stu-id="0044a-119">Comment out hello definition of `refreshItemsFromMobileServiceTable`.</span></span>
5. <span data-ttu-id="0044a-120">Hello 정의의 주석 처리 제거 `refreshItemsFromMobileServiceTableSyncTable`:</span><span class="sxs-lookup"><span data-stu-id="0044a-120">Uncomment hello definition of `refreshItemsFromMobileServiceTableSyncTable`:</span></span>
   
        private List<ToDoItem> refreshItemsFromMobileServiceTableSyncTable() throws ExecutionException, InterruptedException {
            //sync hello data
            sync().get();
            Query query = QueryOperations.field("complete").
                    eq(val(false));
            return mToDoTable.read(query).get();
        }
6. <span data-ttu-id="0044a-121">Hello 정의의 주석 처리 제거 `sync`:</span><span class="sxs-lookup"><span data-stu-id="0044a-121">Uncomment hello definition of `sync`:</span></span>
   
        private AsyncTask<Void, Void, Void> sync() {
            AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
                @Override
                protected Void doInBackground(Void... params) {
                    try {
                        MobileServiceSyncContext syncContext = mClient.getSyncContext();
                        syncContext.push().get();
                        mToDoTable.pull(null).get();
                    } catch (final Exception e) {
                        createAndShowDialogFromTask(e, "Error");
                    }
                    return null;
                }
            };
            return runAsyncTask(task);
        }

## <a name="test-hello-app"></a><span data-ttu-id="0044a-122">Hello 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="0044a-122">Test hello app</span></span>
<span data-ttu-id="0044a-123">이 섹션에서는 있습니다, WiFi에 대 한 hello 동작을 테스트 한 다음 해제 WiFi toocreate 오프 라인 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="0044a-123">In this section, you test hello behavior with WiFi on, and then turn off WiFi toocreate an offline scenario.</span></span>

<span data-ttu-id="0044a-124">Hello를 누를 때까지 로컬 SQLite 저장소 hello 중 동기화 되지 toohello 모바일 서비스에 유지 되도록 데이터 항목을 추가할 때 **새로 고침** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="0044a-124">When you add data items, they are held in hello local SQLite store, but not synced toohello mobile service until you press hello **Refresh** button.</span></span> <span data-ttu-id="0044a-125">다른 앱 데이터 동기화 toobe를 필요로 하는 경우에 관한 다른 요구 사항이 있을 수 있지만이 자습서에 명시적으로 요청할 hello 사용자는 데모 목적.</span><span class="sxs-lookup"><span data-stu-id="0044a-125">Other apps may have different requirements regarding when data needs toobe synchronized, but for demo purposes this tutorial has hello user explicitly request it.</span></span>

<span data-ttu-id="0044a-126">해당 단추를 누르면 새 백그라운드 태스크를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0044a-126">When you press that button, a new background task starts.</span></span> <span data-ttu-id="0044a-127">먼저 모든 변경 내용을 toohello 로컬 저장소 동기화 컨텍스트를 끌어오는 소스 모든 변경 테이블의에서 데이터를 Azure toohello 로컬 사용을 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="0044a-127">It first pushes all changes made toohello local store using synchronization context, then pulls all changed data from Azure toohello local table.</span></span>

### <a name="offline-testing"></a><span data-ttu-id="0044a-128">오프라인 테스트</span><span class="sxs-lookup"><span data-stu-id="0044a-128">Offline testing</span></span>
1. <span data-ttu-id="0044a-129">현재 위치 hello 장치 또는 시뮬레이터에서 *비행기 모드*합니다.</span><span class="sxs-lookup"><span data-stu-id="0044a-129">Place hello device or simulator in *Airplane Mode*.</span></span> <span data-ttu-id="0044a-130">이렇게 하면 오프라인 시나리오가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0044a-130">This creates an offline scenario.</span></span>
2. <span data-ttu-id="0044a-131">몇몇 *ToDo* 항목을 추가하거나 몇몇 항목을 완료로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0044a-131">Add some *ToDo* items, or mark some items as complete.</span></span> <span data-ttu-id="0044a-132">Hello 장치 또는 시뮬레이터 (또는 앱 강제 닫기 hello)를 종료 하 고 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="0044a-132">Quit hello device or simulator (or forcibly close hello app) and restart.</span></span> <span data-ttu-id="0044a-133">변경 내용을 유지 되기 때문에 hello 장치에 보관 되어 있는지 확인 하십시오. hello 로컬 SQLite 저장소에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0044a-133">Verify that your changes have been persisted on hello device because they are held in hello local SQLite store.</span></span>
3. <span data-ttu-id="0044a-134">Hello Azure의 hello 내용을 보는 *TodoItem* 와 같은 SQL 도구를 사용 하 여 테이블 *SQL Server Management Studio*, 또는와 같은 REST 클라이언트 *Fiddler* 또는  *우체부*합니다.</span><span class="sxs-lookup"><span data-stu-id="0044a-134">View hello contents of hello Azure *TodoItem* table either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span> <span data-ttu-id="0044a-135">Hello 새 항목이 있는지 확인 하십시오 *하지* 동기화 된 toohello 서버 되었습니다</span><span class="sxs-lookup"><span data-stu-id="0044a-135">Verify that hello new items have *not* been synced toohello server</span></span>
   
       + <span data-ttu-id="0044a-136">Node.js 백 엔드에 대 한 이동 toohello [Azure 포털](https://portal.azure.com/), 모바일 앱에서 백 엔드를 클릭 하 고 **쉽게 테이블** > **TodoItem** tooview hello 내용의 hello `TodoItem` 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="0044a-136">For a Node.js backend, go toohello [Azure portal](https://portal.azure.com/), and in your Mobile App backend click **Easy Tables** > **TodoItem** tooview hello contents of hello `TodoItem` table.</span></span>
       + <span data-ttu-id="0044a-137">.NET 백 엔드에 대 한 뷰 hello 테이블 내용을 SQL 도구를 사용 하 여 같은 *SQL Server Management Studio*, 또는와 같은 REST 클라이언트 *Fiddler* 또는 *우체부*합니다.</span><span class="sxs-lookup"><span data-stu-id="0044a-137">For a .NET backend, view hello table contents either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span>
4. <span data-ttu-id="0044a-138">Hello 장치 또는 시뮬레이터에서 WiFi를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0044a-138">Turn on WiFi in hello device or simulator.</span></span> <span data-ttu-id="0044a-139">다음으로 hello를 눌러 **새로 고침** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="0044a-139">Next, press hello **Refresh** button.</span></span>
5. <span data-ttu-id="0044a-140">Hello Azure 포털에에서 다시 hello TodoItem 데이터를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="0044a-140">View hello TodoItem data again in hello Azure portal.</span></span> <span data-ttu-id="0044a-141">hello 새로운 기능과 변경 된 TodoItems 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0044a-141">hello new and changed TodoItems should now appear.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0044a-142">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="0044a-142">Additional Resources</span></span>
* <span data-ttu-id="0044a-143">[Azure 모바일 앱에서 데이터 동기화를 오프 라인]</span><span class="sxs-lookup"><span data-stu-id="0044a-143">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="0044a-144">[클라우드 기능: Azure 모바일 서비스에서 오프 라인 동기화] \(참고: hello 비디오는 모바일 서비스에 있지만 Azure 모바일 앱에 비슷한 방식으로 작동 하는 오프 라인 동기화\)</span><span class="sxs-lookup"><span data-stu-id="0044a-144">[Cloud Cover: Offline Sync in Azure Mobile Services] \(note: hello video is on Mobile Services, but offline sync works in a similar way in Azure Mobile Apps\)</span></span>

<!-- URLs. -->

[Azure 모바일 앱에서 데이터 동기화를 오프 라인]: app-service-mobile-offline-data-sync.md

[Android 앱 만들기]: app-service-mobile-android-get-started.md

[클라우드 기능: Azure 모바일 서비스에서 오프 라인 동기화]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/

