---
title: "Azure 모바일 앱(Android)용 오프라인 동기화 사용"
description: "앱 서비스 모바일 앱을 사용하여 Android 응용 프로그램에서 오프라인 데이터를 캐시 및 동기화하는 방법을 알아봅니다."
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
ms.openlocfilehash: 304323c1816302e8c1f68f36a029aee55e02c54e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="enable-offline-sync-for-your-android-mobile-app"></a><span data-ttu-id="fe179-103">Android 모바일 앱에 대해 오프라인 동기화 사용</span><span class="sxs-lookup"><span data-stu-id="fe179-103">Enable offline sync for your Android mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="fe179-104">개요</span><span class="sxs-lookup"><span data-stu-id="fe179-104">Overview</span></span>
<span data-ttu-id="fe179-105">이 자습서에서는 Android용 Azure 모바일 앱의 오프라인 동기화 기능을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fe179-105">This tutorial covers the offline sync feature of Azure Mobile Apps for Android.</span></span> <span data-ttu-id="fe179-106">오프라인 동기화를 사용하면 최종 사용자는 네트워크에 연결되어 있지 않을 때도 모바일 앱&mdash;데이터 보기, 추가 또는 수정&mdash;과 같은 상호 작용을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe179-106">Offline sync allows end users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="fe179-107">변경 내용은 로컬 데이터베이스에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe179-107">Changes are stored in a local database.</span></span> <span data-ttu-id="fe179-108">장치가 다시 온라인 상태가 되면 이러한 변경 내용이 원격 백 엔드와 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe179-108">Once the device is back online, these changes are synced with the remote backend.</span></span>

<span data-ttu-id="fe179-109">Azure 모바일 앱을 처음 사용하는 경우, 먼저 [Android 앱 만들기]자습서를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe179-109">If this is your first experience with Azure Mobile Apps, you should first complete the tutorial [Create an Android App].</span></span> <span data-ttu-id="fe179-110">다운로드한 빠른 시작 서버 프로젝트를 사용하지 않는 경우 프로젝트에 데이터 액세스 확장 패키지를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe179-110">If you do not use the downloaded quick start server project, you must add the data access extension packages to your project.</span></span> <span data-ttu-id="fe179-111">서버 확장 패키지에 대한 자세한 내용은 [Azure 모바일 앱용 .NET 백 엔드 서버 SDK 사용](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe179-111">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="fe179-112">오프라인 동기화 기능에 대한 자세한 내용은 [Azure 모바일 앱에서 오프라인 데이터 동기화]항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe179-112">To learn more about the offline sync feature, see the topic [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="update-the-app-to-support-offline-sync"></a><span data-ttu-id="fe179-113">오프라인 동기화를 지원하도록 앱 업데이트</span><span class="sxs-lookup"><span data-stu-id="fe179-113">Update the app to support offline sync</span></span>
<span data-ttu-id="fe179-114">오프라인 동기화를 통해 *IMobileServiceSyncTable* 인터페이스를 사용하여 장치의 **SQLite** 데이터베이스 일부인 *동기화 테이블*에서 읽고 씁니다.</span><span class="sxs-lookup"><span data-stu-id="fe179-114">With offline sync, you read to and write from a *sync table* (using the *IMobileServiceSyncTable* interface), which is part of a **SQLite** database on your device.</span></span>

<span data-ttu-id="fe179-115">장치와 Azure Mobile Services 간에 변경 내용을 푸시하거나 끌어오려면 데이터를 로컬로 저장하는 데 사용할 로컬 데이터베이스와 함께 초기화하는 *동기화 컨텍스트*(*MobileServiceClient.SyncContext*)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fe179-115">To push and pull changes between the device and Azure Mobile Services, you use a *synchronization context* (*MobileServiceClient.SyncContext*), which you initialize with the local database to store data locally.</span></span>

1. <span data-ttu-id="fe179-116">`TodoActivity.java`에서 `mToDoTable`의 기존 정의를 주석으로 처리하고 동기화 테이블 버전의 주석 처리를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="fe179-116">In `TodoActivity.java`, comment out the existing definition of `mToDoTable` and uncomment the sync table version:</span></span>
   
        private MobileServiceSyncTable<ToDoItem> mToDoTable;
2. <span data-ttu-id="fe179-117">`onCreate` 메서드에서 `mToDoTable`의 기존 초기화를 주석으로 처리하고 이 정의의 주석 처리를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="fe179-117">In the `onCreate` method, comment out the existing initialization of `mToDoTable` and uncomment this definition:</span></span>
   
        mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
3. <span data-ttu-id="fe179-118">`refreshItemsFromTable`에서 `results`의 정의를 주석으로 처리하고 이 정의의 주석 처리를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="fe179-118">In `refreshItemsFromTable` comment out the definition of `results` and uncomment this definition:</span></span>
   
        // Offline Sync
        final List<ToDoItem> results = refreshItemsFromMobileServiceTableSyncTable();
4. <span data-ttu-id="fe179-119">`refreshItemsFromMobileServiceTable`정의를 주석으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="fe179-119">Comment out the definition of `refreshItemsFromMobileServiceTable`.</span></span>
5. <span data-ttu-id="fe179-120">`refreshItemsFromMobileServiceTableSyncTable`정의의 주석 처리를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="fe179-120">Uncomment the definition of `refreshItemsFromMobileServiceTableSyncTable`:</span></span>
   
        private List<ToDoItem> refreshItemsFromMobileServiceTableSyncTable() throws ExecutionException, InterruptedException {
            //sync the data
            sync().get();
            Query query = QueryOperations.field("complete").
                    eq(val(false));
            return mToDoTable.read(query).get();
        }
6. <span data-ttu-id="fe179-121">`sync`정의의 주석 처리를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="fe179-121">Uncomment the definition of `sync`:</span></span>
   
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

## <a name="test-the-app"></a><span data-ttu-id="fe179-122">앱 테스트</span><span class="sxs-lookup"><span data-stu-id="fe179-122">Test the app</span></span>
<span data-ttu-id="fe179-123">이 섹션에서는 WiFi가 켜졌을 때의 동작을 테스트하고 WiFi를 끄고 오프라인 시나리오를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fe179-123">In this section, you test the behavior with WiFi on, and then turn off WiFi to create an offline scenario.</span></span>

<span data-ttu-id="fe179-124">데이터 항목을 추가하면 **새로 고침** 단추를 누를 때까지 모바일 서비스에 동기화되지 않고 로컬 SQLite 저장소에 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe179-124">When you add data items, they are held in the local SQLite store, but not synced to the mobile service until you press the **Refresh** button.</span></span> <span data-ttu-id="fe179-125">앱에 따라 데이터를 동기화해야 하는 경우에 대한 요구 사항이 다르지만 데모 목적으로 이 자습서에는 사용자가 명시적으로 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="fe179-125">Other apps may have different requirements regarding when data needs to be synchronized, but for demo purposes this tutorial has the user explicitly request it.</span></span>

<span data-ttu-id="fe179-126">해당 단추를 누르면 새 백그라운드 태스크를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="fe179-126">When you press that button, a new background task starts.</span></span> <span data-ttu-id="fe179-127">먼저 동기화 컨텍스트를 사용하여 로컬 저장소에 대한 모든 변경 내용을 푸시한 다음 Azure에서 로컬 테이블로 변경된 데이터를 모두 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="fe179-127">It first pushes all changes made to the local store using synchronization context, then pulls all changed data from Azure to the local table.</span></span>

### <a name="offline-testing"></a><span data-ttu-id="fe179-128">오프라인 테스트</span><span class="sxs-lookup"><span data-stu-id="fe179-128">Offline testing</span></span>
1. <span data-ttu-id="fe179-129">장치 또는 시뮬레이터를 *비행기 모드*로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="fe179-129">Place the device or simulator in *Airplane Mode*.</span></span> <span data-ttu-id="fe179-130">이렇게 하면 오프라인 시나리오가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe179-130">This creates an offline scenario.</span></span>
2. <span data-ttu-id="fe179-131">몇몇 *ToDo* 항목을 추가하거나 몇몇 항목을 완료로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="fe179-131">Add some *ToDo* items, or mark some items as complete.</span></span> <span data-ttu-id="fe179-132">장치 또는 시뮬레이터를 종료하거나 앱을 강제로 닫고 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="fe179-132">Quit the device or simulator (or forcibly close the app) and restart.</span></span> <span data-ttu-id="fe179-133">변경 내용은 로컬 SQLite 저장소에 보관되므로 변경 내용이 장치에서 지속되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fe179-133">Verify that your changes have been persisted on the device because they are held in the local SQLite store.</span></span>
3. <span data-ttu-id="fe179-134">*SQL Server Management Studio*와 같은 SQL 도구나 *Fiddler* 또는 *Postman*과 같은 REST 클라이언트를 사용하여 Azure *TodoItem* 테이블의 내용을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="fe179-134">View the contents of the Azure *TodoItem* table either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span> <span data-ttu-id="fe179-135">새 항목이 서버와 동기화되지 *않았는지* 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fe179-135">Verify that the new items have *not* been synced to the server</span></span>
   
       + <span data-ttu-id="fe179-136">Node.js 백 엔드의 경우 [Azure Portal](https://portal.azure.com/)로 이동하여 모바일 앱 백 엔드에서 **쉬운 테이블** > **TodoItem**을 클릭하여 `TodoItem` 테이블의 내용을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="fe179-136">For a Node.js backend, go to the [Azure portal](https://portal.azure.com/), and in your Mobile App backend click **Easy Tables** > **TodoItem** to view the contents of the `TodoItem` table.</span></span>
       + <span data-ttu-id="fe179-137">.NET 백 엔드의 경우 *SQL Server Management Studio*와 같은 SQL 도구나 *Fiddler* 또는 *Postman* 같은 REST 클라이언트를 사용하여 테이블 내용을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="fe179-137">For a .NET backend, view the table contents either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span>
4. <span data-ttu-id="fe179-138">장치 또는 시뮬레이터에서 WiFi를 켭니다.</span><span class="sxs-lookup"><span data-stu-id="fe179-138">Turn on WiFi in the device or simulator.</span></span> <span data-ttu-id="fe179-139">다음으로 **새로 고침** 단추를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="fe179-139">Next, press the **Refresh** button.</span></span>
5. <span data-ttu-id="fe179-140">TodoItem 데이터를 Azure 포털에 다시 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="fe179-140">View the TodoItem data again in the Azure portal.</span></span> <span data-ttu-id="fe179-141">이제 새 및 변경된 TodoItems가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="fe179-141">The new and changed TodoItems should now appear.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fe179-142">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="fe179-142">Additional Resources</span></span>
* <span data-ttu-id="fe179-143">[Azure 모바일 앱에서 오프라인 데이터 동기화]</span><span class="sxs-lookup"><span data-stu-id="fe179-143">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="fe179-144">[Cloud Cover: Azure Mobile Services에서 오프라인 동기화] \(참고: 비디오는 Mobile Services에 있지만 Azure Mobile Apps에서 비슷한 방식으로 오프라인 동기화가 작동합니다.\)</span><span class="sxs-lookup"><span data-stu-id="fe179-144">[Cloud Cover: Offline Sync in Azure Mobile Services] \(note: the video is on Mobile Services, but offline sync works in a similar way in Azure Mobile Apps\)</span></span>

<!-- URLs. -->

<span data-ttu-id="fe179-145">[Azure 모바일 앱에서 오프라인 데이터 동기화]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="fe179-145">[Offline Data Sync in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md</span></span>

<span data-ttu-id="fe179-146">[Android 앱 만들기]: app-service-mobile-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="fe179-146">[Create an Android App]: app-service-mobile-android-get-started.md</span></span>

<span data-ttu-id="fe179-147">[Cloud Cover: Azure Mobile Services에서 오프라인 동기화]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri</span><span class="sxs-lookup"><span data-stu-id="fe179-147">[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri</span></span>
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/

