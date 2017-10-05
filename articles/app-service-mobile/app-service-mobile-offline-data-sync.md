---
title: "Azure Mobile Apps에서 오프라인 데이터 동기화 | Microsoft Docs"
description: "Azure 모바일 앱에 대한 오프라인 데이터 동기화 기능의 개념 참조 및 개요"
documentationcenter: windows
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 982fb683-8884-40da-96e6-77eeca2500e3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 8e2bd755d14319f8c66f7ae7ec64fbd10801b39d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="offline-data-sync-in-azure-mobile-apps"></a><span data-ttu-id="98fdd-103">Azure 모바일 앱에서 오프라인 데이터 동기화</span><span class="sxs-lookup"><span data-stu-id="98fdd-103">Offline Data Sync in Azure Mobile Apps</span></span>
## <a name="what-is-offline-data-sync"></a><span data-ttu-id="98fdd-104">오프라인 데이터 동기화 정의</span><span class="sxs-lookup"><span data-stu-id="98fdd-104">What is offline data sync?</span></span>
<span data-ttu-id="98fdd-105">오프라인 데이터 동기화는 개발자가 네트워크 연결 없이 작동하는 앱을 쉽게 만들 수 있는 Azure Mobile Apps의 클라이언트 및 서버 SDK 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-105">Offline data sync is a client and server SDK feature of Azure Mobile Apps that makes it easy for developers to create apps that are functional without a network connection.</span></span>

<span data-ttu-id="98fdd-106">앱이 오프라인 모드일 때 여전히 데이터를 만들고 수정할 수 있으며 이는 로컬 저장소에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-106">When your app is in offline mode, you can still create and modify data, which are saved to a local store.</span></span> <span data-ttu-id="98fdd-107">앱이 다시 온라인 상태가 되면 로컬 변경 내용을 Azure 모바일 앱 백 엔드와 동기화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-107">When the app is back online, it can synchronize local changes with your Azure Mobile App backend.</span></span> <span data-ttu-id="98fdd-108">동일한 레코드가 클라이언트와 백 엔드 모두에서 변경될 때 기능은 충돌을 감지하는 지원을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-108">The feature also includes support for detecting conflicts when the same record is changed on both the client and the backend.</span></span> <span data-ttu-id="98fdd-109">충돌을 서버 또는 클라이언트에서 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-109">Conflicts can then be handled either on the server or the client.</span></span>

<span data-ttu-id="98fdd-110">오프라인 동기화의 몇 가지 혜택은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-110">Offline sync has several benefits:</span></span>

* <span data-ttu-id="98fdd-111">서버 데이터를 장치에 로컬로 캐시하여 앱 응답성 향상</span><span class="sxs-lookup"><span data-stu-id="98fdd-111">Improve app responsiveness by caching server data locally on the device</span></span>
* <span data-ttu-id="98fdd-112">네트워크 문제가 있는 경우 유용한 강력한 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="98fdd-112">Create robust apps that remain useful when there are network issues</span></span>
* <span data-ttu-id="98fdd-113">최종 사용자가 네트워크에 액세스할 수 없는 경우에도 데이터를 만들고 수정할 수 있도록 허용하여 네트워크에 연결되지 않은 시나리오까지 지원</span><span class="sxs-lookup"><span data-stu-id="98fdd-113">Allow end users to create and modify data even when there is no network access, supporting scenarios with little or no connectivity</span></span>
* <span data-ttu-id="98fdd-114">여러 장치 간에 데이터를 동기화하고 동일한 레코드를 두 개의 장치에서 수정할 때 충돌 감지</span><span class="sxs-lookup"><span data-stu-id="98fdd-114">Sync data across multiple devices and detect conflicts when the same record is modified by two devices</span></span>
* <span data-ttu-id="98fdd-115">지연 시간이 길거나 요금제인 네트워크에 대한 네트워크 사용 제한</span><span class="sxs-lookup"><span data-stu-id="98fdd-115">Limit network use on high-latency or metered networks</span></span>

<span data-ttu-id="98fdd-116">다음 자습서는 Azure 모바일 앱을 사용하여 모바일 클라이언트에 오프라인 동기화를 추가하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-116">The following tutorials show how to add offline sync to your mobile clients using Azure Mobile Apps:</span></span>

* <span data-ttu-id="98fdd-117">[Android: 오프라인 동기화 사용]</span><span class="sxs-lookup"><span data-stu-id="98fdd-117">[Android: Enable offline sync]</span></span>
* [<span data-ttu-id="98fdd-118">Apache Cordova: 오프라인 동기화 사용</span><span class="sxs-lookup"><span data-stu-id="98fdd-118">Apache Cordova: Enable offline sync</span></span>](app-service-mobile-cordova-get-started-offline-data.md)
* <span data-ttu-id="98fdd-119">[iOS: 오프라인 동기화 사용]</span><span class="sxs-lookup"><span data-stu-id="98fdd-119">[iOS: Enable offline sync]</span></span>
* <span data-ttu-id="98fdd-120">[Xamarin iOS: 오프라인 동기화 사용]</span><span class="sxs-lookup"><span data-stu-id="98fdd-120">[Xamarin iOS: Enable offline sync]</span></span>
* <span data-ttu-id="98fdd-121">[Xamarin Android: 오프라인 동기화 사용]</span><span class="sxs-lookup"><span data-stu-id="98fdd-121">[Xamarin Android: Enable offline sync]</span></span>
* [<span data-ttu-id="98fdd-122">Xamarin.Forms: 오프라인 동기화 사용</span><span class="sxs-lookup"><span data-stu-id="98fdd-122">Xamarin.Forms: Enable offline sync</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)
* <span data-ttu-id="98fdd-123">[유니버설 Windows 플랫폼: 오프라인 동기화 사용]</span><span class="sxs-lookup"><span data-stu-id="98fdd-123">[Universal Windows Platform: Enable offline sync]</span></span>

## <a name="what-is-a-sync-table"></a><span data-ttu-id="98fdd-124">동기화 테이블 정의</span><span class="sxs-lookup"><span data-stu-id="98fdd-124">What is a sync table?</span></span>
<span data-ttu-id="98fdd-125">"/tables" 끝점에 액세스하는 데 Azure 모바일 클라이언트 SDK가 `IMobileServiceTable`(.NET 클라이언트 SDK) 또는 `MSTable`(iOS 클라이언트)와 같은 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-125">To access the "/tables" endpoint, the Azure Mobile client SDKs provide interfaces such as `IMobileServiceTable` (.NET client SDK) or `MSTable` (iOS client).</span></span> <span data-ttu-id="98fdd-126">이러한 API는 Azure 모바일 앱 백 엔드에 직접 연결하고 클라이언트 장치에 네트워크 연결이 없는 경우 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-126">These APIs connect directly to the Azure Mobile App backend and fail if the client device does not have a network connection.</span></span>

<span data-ttu-id="98fdd-127">오프라인 사용을 지원하려면 앱은 `IMobileServiceSyncTable`(.NET 클라이언트 SDK) 또는 `MSSyncTable`(iOS 클라이언트)과 같은 *동기화 테이블* API를 대신 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-127">To support offline use, your app should instead use the *sync table* APIs, such as `IMobileServiceSyncTable` (.NET client SDK) or `MSSyncTable` (iOS client).</span></span> <span data-ttu-id="98fdd-128">같은 CRUD 작업 모두(만들기, 읽기, 업데이트, 삭제)가 *로컬 저장소*에 읽거나 쓰는 것을 제외하고 동기화 테이블 API에 대해 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-128">All the same CRUD operations (Create, Read, Update, Delete) work against sync table APIs, except now they read from or write to a *local store*.</span></span> <span data-ttu-id="98fdd-129">모든 동기화 테이블 작업을 수행하려면 먼저 로컬 저장소를 초기화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-129">Before any sync table operations can be performed, the local store must be initialized.</span></span>

## <a name="what-is-a-local-store"></a><span data-ttu-id="98fdd-130">로컬 저장소 정의</span><span class="sxs-lookup"><span data-stu-id="98fdd-130">What is a local store?</span></span>
<span data-ttu-id="98fdd-131">로컬 저장소는 클라이언트 장치의 데이터 지속성 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-131">A local store is the data persistence layer on the client device.</span></span> <span data-ttu-id="98fdd-132">Azure Mobile Apps 클라이언트 SDK는 기본 로컬 저장소 구현을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-132">The Azure Mobile Apps client SDKs provide a default local store implementation.</span></span> <span data-ttu-id="98fdd-133">Windows, Xamarin 및 Android에서는 SQLite에 기반합니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-133">On Windows, Xamarin and Android, it is based on SQLite.</span></span> <span data-ttu-id="98fdd-134">iOS에서는 코어 데이터에 기반합니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-134">On iOS, it is based on Core Data.</span></span>

<span data-ttu-id="98fdd-135">Windows Phone 또는 Windows 스토어 8.1에서 SQLite 기반 구현을 사용하려면 SQLite 확장을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-135">To use the SQLite-based implementation on Windows Phone or Windows Store 8.1, you need to install a SQLite extension.</span></span> <span data-ttu-id="98fdd-136">자세한 내용은 [유니버설 Windows 플랫폼: 오프라인 동기화 사용]을 참조하세요. Android 및 iOS은 장치 운영 체제 자체에서 SQLite의 버전으로 제공되므로 SQLite의 고유한 버전을 참조하는 데 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-136">For more information, see [Universal Windows Platform: Enable offline sync]. Android and iOS ship with a version of SQLite in the device operating system itself, so it is not necessary to reference your own version of SQLite.</span></span>

<span data-ttu-id="98fdd-137">또한 개발자는 자신의 로컬 저장소를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-137">Developers can also implement their own local store.</span></span> <span data-ttu-id="98fdd-138">예를 들어 모바일 클라이언트에서 암호화된 형식으로 데이터를 저장하려는 경우 암호화에 SQLCipher를 사용하는 로컬 저장소를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-138">For instance, if you wish to store data in an encrypted format on the mobile client, you can define a local store that uses SQLCipher for encryption.</span></span>

## <a name="what-is-a-sync-context"></a><span data-ttu-id="98fdd-139">동기화 컨텍스트 정의</span><span class="sxs-lookup"><span data-stu-id="98fdd-139">What is a sync context?</span></span>
<span data-ttu-id="98fdd-140">*동기화 컨텍스트*는 모바일 클라이언트 개체와 연결되고(예: `IMobileServiceClient` 또는 `MSClient`) 동기화 테이블에 적용된 변경 내용을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-140">A *sync context* is associated with a mobile client object (such as `IMobileServiceClient` or `MSClient`) and tracks changes that are made with sync tables.</span></span> <span data-ttu-id="98fdd-141">동기화 컨텍스트는 나중에 서버로 보내지는 정렬된 CUD(만들기, 업데이트, 삭제) 작업 목록을 관리하는 *작업 큐*를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-141">The sync context maintains an *operation queue*, which keeps an ordered list of CUD operations (Create, Update, Delete) that is later be sent to the server.</span></span>

<span data-ttu-id="98fdd-142">로컬 저장소는 [.NET 클라이언트 SDK]에서 `IMobileServicesSyncContext.InitializeAsync(localstore)`와 같은 초기화 메서드를 사용하여 동기화 컨텍스트와 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-142">A local store is associated with the sync context using an initialize method such as `IMobileServicesSyncContext.InitializeAsync(localstore)` in the [.NET client SDK].</span></span>

## <span data-ttu-id="98fdd-143"><a name="how-sync-works"></a>오프라인 동기화 작동 방법</span><span class="sxs-lookup"><span data-stu-id="98fdd-143"><a name="how-sync-works"></a>How offline synchronization works</span></span>
<span data-ttu-id="98fdd-144">동기화 테이블을 사용할 경우 클라이언트 코드는 로컬 변경이 Azure 모바일 앱 백 엔드와 동기화하는 시기를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-144">When using sync tables, your client code controls when local changes are synchronized with an Azure Mobile App backend.</span></span> <span data-ttu-id="98fdd-145">로컬 변경을 *푸시*하는 호출이 있을 때까지 백 엔드에 아무 것도 보내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-145">Nothing is sent to the backend until there is a call to *push* local changes.</span></span> <span data-ttu-id="98fdd-146">마찬가지로 로컬 저장소는 데이터 *끌어오기* 호출이 있을 때 새 데이터로 채워집니다</span><span class="sxs-lookup"><span data-stu-id="98fdd-146">Similarly, the local store is populated with new data only when there is a call to *pull* data.</span></span>

* <span data-ttu-id="98fdd-147">**푸시**: 푸시는 동기화 컨텍스트에 관한 작업이며 마지막 푸시 이후로 모든 CUD 변경을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-147">**Push**: Push is an operation on the sync context and sends all CUD changes since the last push.</span></span> <span data-ttu-id="98fdd-148">그렇지 않으면 작업이 잘못된 순서로 전송되기 때문에 개별 테이블의 변경 내용만을 보낼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-148">Note that it is not possible to send only an individual table's changes, because otherwise operations could be sent out of order.</span></span> <span data-ttu-id="98fdd-149">푸시는 Azure 모바일 앱 백 엔드에 일련의 REST 호출을 실행하여 차례로 서버 데이터베이스를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-149">Push executes a series of REST calls to your Azure Mobile App backend, which in turn modifies your server database.</span></span>
* <span data-ttu-id="98fdd-150">**끌어오기**: 끌어오기는 테이블 당 단위로 수행되고 서버 데이터의 하위 집합을 검색하는 쿼리로 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-150">**Pull**: Pull is performed on a per-table basis and can be customized with a query to retrieve only a subset of the server data.</span></span> <span data-ttu-id="98fdd-151">그런 다음 Azure 모바일 클라이언트 SDK는 로컬 저장소에 발생한 데이터를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-151">The Azure Mobile client SDKs then insert the resulting data into the local store.</span></span>
* <span data-ttu-id="98fdd-152">**암시적 푸시**: 끌어오기가 로컬 업데이트를 보류 중인 테이블에 대해 실행되는 경우 동기화 컨텍스트에서 `push()`를 먼저 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-152">**Implicit Pushes**: If a pull is executed against a table that has pending local updates, the pull first executes a `push()` on the sync context.</span></span> <span data-ttu-id="98fdd-153">이미 큐에 대기 중인 변경 내용과 서버의 새 데이터 간에 충돌을 최소화하는 데 이 푸시가 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-153">This push helps minimize conflicts between changes that are already queued and new data from the server.</span></span>
* <span data-ttu-id="98fdd-154">**증분 동기화**: 가져오기 작업의 첫 번째 매개 변수는 클라이언트에만 사용되는 *쿼리 이름* 입니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-154">**Incremental Sync**: the first parameter to the pull operation is a *query name* that is used only on the client.</span></span> <span data-ttu-id="98fdd-155">Null이 아닌 쿼리 이름을 사용할 경우 Azure 모바일 SDK는 *증분 동기화*를 수행합니다. 가져오기 작업이 결과 집합을 반환할 때마다 해당 결과 집합에서 최신 `updatedAt` timestamp는 SDK 로컬 시스템 테이블에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-155">If you use a non-null query name, the Azure Mobile SDK performs an *incremental sync*. Each time a pull operation returns a set of results, the latest `updatedAt` timestamp from that result set is stored in the SDK local system tables.</span></span> <span data-ttu-id="98fdd-156">후속 끌어오기 작업은 해당 timestamp 이후의 레코드만 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-156">Subsequent pull operations retrieve only records after that timestamp.</span></span>

  <span data-ttu-id="98fdd-157">증분 동기화를 사용하려면 서버가 의미 있는 `updatedAt` 값을 반환하고 이 필드의 정렬을 지원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-157">To use incremental sync, your server must return meaningful `updatedAt` values and must also support sorting by this field.</span></span> <span data-ttu-id="98fdd-158">그러나 SDK가 updatedAt 필드에서 자체 정렬를 추가하므로 고유의 `orderBy` 절을 가진 끌어오기 쿼리를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-158">However, since the SDK adds its own sort on the updatedAt field, you cannot use a pull query that has its own `orderBy` clause.</span></span>

  <span data-ttu-id="98fdd-159">쿼리 이름에 모든 문자열을 선택할 수 있지만 앱에서 각 논리 쿼리에 대해 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-159">The query name can be any string you choose, but it must be unique for each logical query in your app.</span></span>
  <span data-ttu-id="98fdd-160">그렇지 않은 경우 다른 끌어오기 작업이 동일한 증분 동기화 timestamp를 덮어쓰고 쿼리는 잘못된 결과를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-160">Otherwise, different pull operations could overwrite the same incremental sync timestamp and your queries can return incorrect results.</span></span>

  <span data-ttu-id="98fdd-161">쿼리에 매개 변수가 있으면 고유한 쿼리 이름을 만드는 한 가지 방법은 매개 변수 값을 통합하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-161">If the query has a parameter, one way to create a unique query name is to incorporate the parameter value.</span></span>
  <span data-ttu-id="98fdd-162">예를 들어 userid를 필터링할 경우 사용자 쿼리 이름은 C#으로 다음과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-162">For instance, if you are filtering on userid, your query name could be as follows (in C#):</span></span>

        await todoTable.PullAsync("todoItems" + userid,
            syncTable.Where(u => u.UserId == userid));

  <span data-ttu-id="98fdd-163">증분 동기화를 옵트아웃(opt out)하려면 `null`을 쿼리 ID로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-163">If you want to opt out of incremental sync, pass `null` as the query ID.</span></span> <span data-ttu-id="98fdd-164">이 경우 `PullAsync`에 대한 모든 호출에서 모든 레코드가 검색되므로 이는 잠재적으로 비효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-164">In this case, all records are retrieved on every call to `PullAsync`, which is potentially inefficient.</span></span>
* <span data-ttu-id="98fdd-165">**제거**: `IMobileServiceSyncTable.PurgeAsync`를 사용하여 로컬 저장소의 내용을 지울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-165">**Purging**: You can clear the contents of the local store using `IMobileServiceSyncTable.PurgeAsync`.</span></span>
  <span data-ttu-id="98fdd-166">제거는 클라이언트 데이터베이스에서 오래된 데이터가 있는 경우 또는 모든 보류 중인 변경 내용을 취소하려는 경우에 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-166">Purging may be necessary if you have stale data in the client database, or if you wish to discard all pending changes.</span></span>

  <span data-ttu-id="98fdd-167">제거는 로컬 저장소에서 테이블을 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-167">A purge clears a table from the local store.</span></span> <span data-ttu-id="98fdd-168">서버 데이터베이스와 동기화 보류 중인 작업이 있는 경우 *강제 제거* 매개 변수를 설정하지 않으면 제거가 예외를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-168">If there are operations awaiting synchronization with the server database, the purge throws an exception unless the *force purge* parameter is set.</span></span>

  <span data-ttu-id="98fdd-169">클라이언트에서 오래된 데이터의 예로 "todo 목록" 예에서 장치1이 완료되지 않은 항목을 끌어온다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-169">As an example of stale data on the client, suppose in the "todo list" example, Device1 only pulls items that are not completed.</span></span> <span data-ttu-id="98fdd-170">todoitem "우유 구매"가 다른 장치에 의해 서버에서 완료되었다고 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-170">A todoitem "Buy milk" is marked completed on the server by another device.</span></span> <span data-ttu-id="98fdd-171">그러나 장치1은 완료 표시된 항목을 가져오기 때문에 아직 "우유 구매" todoitem을 로컬 저장소에 가지고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-171">However, Device1 still has the "Buy milk" todoitem in local store because it is only pulling items that are not marked complete.</span></span> <span data-ttu-id="98fdd-172">제거는 이 오래된 항목을 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="98fdd-172">A purge clears this stale item.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98fdd-173">다음 단계</span><span class="sxs-lookup"><span data-stu-id="98fdd-173">Next steps</span></span>
* <span data-ttu-id="98fdd-174">[iOS: 오프라인 동기화 사용]</span><span class="sxs-lookup"><span data-stu-id="98fdd-174">[iOS: Enable offline sync]</span></span>
* <span data-ttu-id="98fdd-175">[Xamarin iOS: 오프라인 동기화 사용]</span><span class="sxs-lookup"><span data-stu-id="98fdd-175">[Xamarin iOS: Enable offline sync]</span></span>
* <span data-ttu-id="98fdd-176">[Xamarin Android: 오프라인 동기화 사용]</span><span class="sxs-lookup"><span data-stu-id="98fdd-176">[Xamarin Android: Enable offline sync]</span></span>
* <span data-ttu-id="98fdd-177">[유니버설 Windows 플랫폼: 오프라인 동기화 사용]</span><span class="sxs-lookup"><span data-stu-id="98fdd-177">[Universal Windows Platform: Enable offline sync]</span></span>

<!-- Links -->
[.NET 클라이언트 SDK]: app-service-mobile-dotnet-how-to-use-client-library.md
[Android: 오프라인 동기화 사용]: app-service-mobile-android-get-started-offline-data.md
[iOS: 오프라인 동기화 사용]: app-service-mobile-ios-get-started-offline-data.md
[Xamarin iOS: 오프라인 동기화 사용]: app-service-mobile-xamarin-ios-get-started-offline-data.md
[Xamarin Android: 오프라인 동기화 사용]: app-service-mobile-xamarin-android-get-started-offline-data.md
[유니버설 Windows 플랫폼: 오프라인 동기화 사용]: app-service-mobile-windows-store-dotnet-get-started-offline-data.md
