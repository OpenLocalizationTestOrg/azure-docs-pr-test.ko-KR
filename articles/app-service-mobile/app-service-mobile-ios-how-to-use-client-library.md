---
title: "aaaHow tooUse iOS Azure 모바일 앱에 대 한 SDK"
description: "어떻게 tooUse iOS Azure 모바일 앱에 대 한 SDK"
services: app-service\mobile
documentationcenter: ios
author: ysxu
manager: yochayk
editor: 
ms.assetid: 4e8e45df-c36a-4a60-9ad4-393ec10b7eb9
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/01/2016
ms.author: yuaxu
ms.openlocfilehash: fa299ab3f152bad12d821832fa9fb5495d1fa296
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-ios-client-library-for-azure-mobile-apps"></a><span data-ttu-id="599d3-103">어떻게 tooUse iOS Azure 모바일 앱에 대 한 클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="599d3-103">How tooUse iOS Client Library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="599d3-104">이 가이드 최신 버전의 hello를 사용 하 여 tooperform 일반적인 시나리오에 설명 [Azure 모바일 앱 iOS SDK][1]합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-104">This guide teaches you tooperform common scenarios using hello latest [Azure Mobile Apps iOS SDK][1].</span></span> <span data-ttu-id="599d3-105">새로운 tooAzure 모바일 앱의 경우 먼저 완료 [Azure 모바일 앱 빠른 시작] toocreate을 백 엔드는 테이블을 만들고 미리 작성 된 iOS Xcode 프로젝트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-105">If you are new tooAzure Mobile Apps, first complete [Azure Mobile Apps Quick Start] toocreate a backend, create a table, and download a pre-built iOS Xcode project.</span></span> <span data-ttu-id="599d3-106">이 가이드에서는 hello 클라이언트 쪽 iOS SDK 집중 합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-106">In this guide, we focus on hello client-side iOS SDK.</span></span> <span data-ttu-id="599d3-107">에 대해 더 알아봅니다 toolearn hello 백 엔드에 대 한 서버 쪽 SDK hello 하 hello 서버 SDK, 방법을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="599d3-107">toolearn more about hello server-side SDK for hello backend, see hello Server SDK HOWTOs.</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="599d3-108">참조 설명서</span><span class="sxs-lookup"><span data-stu-id="599d3-108">Reference documentation</span></span>
<span data-ttu-id="599d3-109">hello hello iOS 클라이언트 SDK에 대 한 참조 설명서는 여기에서 찾을: [Azure 모바일 앱 iOS 클라이언트 참조][2]합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-109">hello reference documentation for hello iOS client SDK is located here: [Azure Mobile Apps iOS Client Reference][2].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="599d3-110">지원되는 플랫폼</span><span class="sxs-lookup"><span data-stu-id="599d3-110">Supported Platforms</span></span>
<span data-ttu-id="599d3-111">hello iOS SDK는 iOS 버전 8.0 이상에 대 한 프로젝트 Objective-c, Swift 2.2 프로젝트 및 Swift 2.3 프로젝트를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-111">hello iOS SDK supports Objective-C projects, Swift 2.2 projects, and Swift 2.3 projects for iOS versions 8.0 or later.</span></span>

<span data-ttu-id="599d3-112">hello "서버 흐름" 인증 UI를 표시 하는 hello에 대 한 보기를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-112">hello "server-flow" authentication uses a WebView for hello presented UI.</span></span>  <span data-ttu-id="599d3-113">Hello 장치가 아닌 경우 수 toopresent WebView UI를 다른 인증 방법이 필요 hello 제품의 외부 hello 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-113">If hello device is not able toopresent a WebView UI, then another method of authentication is required that is outside hello scope of hello product.</span></span>  
<span data-ttu-id="599d3-114">따라서 이 SDK는 Watch 유형 또는 그와 비슷하게 제한된 장치에는 적합하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-114">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span></span>

## <span data-ttu-id="599d3-115"><a name="Setup"></a>설정 및 필수 조건</span><span class="sxs-lookup"><span data-stu-id="599d3-115"><a name="Setup"></a>Setup and Prerequisites</span></span>
<span data-ttu-id="599d3-116">이 가이드에서는 테이블과 함께 백 엔드를 만들었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-116">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="599d3-117">이 가이드에서는 해당 hello 테이블 해당 자습서에 hello 테이블과 같은 스키마를 가진 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-117">This guide assumes that hello table has the same schema as hello tables in those tutorials.</span></span> <span data-ttu-id="599d3-118">또한 이 가이드에서는 코드에서 `MicrosoftAzureMobile.framework`를 참조하고 `MicrosoftAzureMobile/MicrosoftAzureMobile.h`를 가져온다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-118">This guide also assumes that in your code, you reference `MicrosoftAzureMobile.framework` and import `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.</span></span>

## <span data-ttu-id="599d3-119"><a name="create-client"></a>방법: 클라이언트 만들기</span><span class="sxs-lookup"><span data-stu-id="599d3-119"><a name="create-client"></a>How to: Create Client</span></span>
<span data-ttu-id="599d3-120">프로젝트에는 Azure 모바일 앱 백 엔드 tooaccess 만들기는 `MSClient`합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-120">tooaccess an Azure Mobile Apps backend in your project, create an `MSClient`.</span></span> <span data-ttu-id="599d3-121">대체 `AppUrl` hello 앱 url입니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-121">Replace `AppUrl` with hello app URL.</span></span> <span data-ttu-id="599d3-122">`gatewayURLString` 및 `applicationKey`는 비워둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-122">You may leave `gatewayURLString` and `applicationKey` empty.</span></span> <span data-ttu-id="599d3-123">인증에 대 한 게이트웨이 설정 하는 경우 채우기 `gatewayURLString` hello 게이트웨이 url입니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-123">If you set up a gateway for authentication, populate `gatewayURLString` with hello gateway URL.</span></span>

<span data-ttu-id="599d3-124">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="599d3-124">**Objective-C**:</span></span>

```
MSClient *client = [MSClient clientWithApplicationURLString:@"AppUrl"];
```

<span data-ttu-id="599d3-125">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="599d3-125">**Swift**:</span></span>

```
let client = MSClient(applicationURLString: "AppUrl")
```


## <span data-ttu-id="599d3-126"><a name="table-reference"></a>방법: 테이블 참조 만들기</span><span class="sxs-lookup"><span data-stu-id="599d3-126"><a name="table-reference"></a>How to: Create Table Reference</span></span>
<span data-ttu-id="599d3-127">tooaccess 또는 update 데이터 참조 toohello 백 엔드 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-127">tooaccess or update data, create a reference toohello backend table.</span></span> <span data-ttu-id="599d3-128">대체 `TodoItem` 테이블의 이름으로 hello와</span><span class="sxs-lookup"><span data-stu-id="599d3-128">Replace `TodoItem` with hello name of your table</span></span>

<span data-ttu-id="599d3-129">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="599d3-129">**Objective-C**:</span></span>

```
MSTable *table = [client tableWithName:@"TodoItem"];
```

<span data-ttu-id="599d3-130">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="599d3-130">**Swift**:</span></span>

```
let table = client.tableWithName("TodoItem")
```


## <span data-ttu-id="599d3-131"><a name="querying"></a>방법: 데이터 쿼리</span><span class="sxs-lookup"><span data-stu-id="599d3-131"><a name="querying"></a>How to: Query Data</span></span>
<span data-ttu-id="599d3-132">데이터베이스 쿼리 toocreate 쿼리 hello `MSTable` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-132">toocreate a database query, query hello `MSTable` object.</span></span> <span data-ttu-id="599d3-133">hello 다음 쿼리에서 모든 항목을 가져옵니다 hello `TodoItem` 로그 hello 각 항목의 텍스트 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-133">hello following query gets all hello items in `TodoItem` and logs hello text of each item.</span></span>

<span data-ttu-id="599d3-134">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="599d3-134">**Objective-C**:</span></span>

```
[table readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) { // error is nil if no error occured
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) { // items is NSArray of records that match query
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

<span data-ttu-id="599d3-135">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="599d3-135">**Swift**:</span></span>

```
table.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <span data-ttu-id="599d3-136"><a name="filtering"></a>방법: 반환된 데이터 필터링</span><span class="sxs-lookup"><span data-stu-id="599d3-136"><a name="filtering"></a>How to: Filter Returned Data</span></span>
<span data-ttu-id="599d3-137">toofilter 결과 사용할 수 있는 여러 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-137">toofilter results, there are many available options.</span></span>

<span data-ttu-id="599d3-138">조건자를 사용 하 여 사용 하 여 toofilter는 `NSPredicate` 및 `readWithPredicate`합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-138">toofilter using a predicate, use an `NSPredicate` and `readWithPredicate`.</span></span> <span data-ttu-id="599d3-139">hello 다음 반환 된 데이터 toofind만 불완전 한 일 항목을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-139">hello following filters returned data toofind only incomplete Todo items.</span></span>

<span data-ttu-id="599d3-140">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="599d3-140">**Objective-C**:</span></span>

```
// Create a predicate that finds items where complete is false
NSPredicate * predicate = [NSPredicate predicateWithFormat:@"complete == NO"];
// Query hello TodoItem table
[table readWithPredicate:predicate completion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

<span data-ttu-id="599d3-141">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="599d3-141">**Swift**:</span></span>

```
// Create a predicate that finds items where complete is false
let predicate =  NSPredicate(format: "complete == NO")
// Query hello TodoItem table
table.readWithPredicate(predicate) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <span data-ttu-id="599d3-142"><a name="query-object"></a>방법: MSQuery 사용</span><span class="sxs-lookup"><span data-stu-id="599d3-142"><a name="query-object"></a>How to: Use MSQuery</span></span>
<span data-ttu-id="599d3-143">(정렬 및 포함 페이징), 복잡 한 쿼리를 만들 tooperform는 `MSQuery` 개체를 직접 또는 조건자를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="599d3-143">tooperform a complex query (including sorting and paging), create an `MSQuery` object, directly or by using a predicate:</span></span>

<span data-ttu-id="599d3-144">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="599d3-144">**Objective-C**:</span></span>

```
MSQuery *query = [table query];
MSQuery *query = [table queryWithPredicate: [NSPredicate predicateWithFormat:@"complete == NO"]];
```

<span data-ttu-id="599d3-145">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="599d3-145">**Swift**:</span></span>

```
let query = table.query()
let query = table.queryWithPredicate(NSPredicate(format: "complete == NO"))
```

<span data-ttu-id="599d3-146">`MSQuery` 를 사용하여 여러 쿼리 동작을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-146">`MSQuery` lets you control several query behaviors.</span></span>

* <span data-ttu-id="599d3-147">결과의 순서 지정</span><span class="sxs-lookup"><span data-stu-id="599d3-147">Specify order of results</span></span>
* <span data-ttu-id="599d3-148">어떤 필드 tooreturn 제한</span><span class="sxs-lookup"><span data-stu-id="599d3-148">Limit which fields tooreturn</span></span>
* <span data-ttu-id="599d3-149">레코드 tooreturn 제한</span><span class="sxs-lookup"><span data-stu-id="599d3-149">Limit how many records tooreturn</span></span>
* <span data-ttu-id="599d3-150">응답의 총 수 지정</span><span class="sxs-lookup"><span data-stu-id="599d3-150">Specify total count in response</span></span>
* <span data-ttu-id="599d3-151">요청에서 사용자 지정 쿼리 문자열 매개 변수 지정</span><span class="sxs-lookup"><span data-stu-id="599d3-151">Specify custom query string parameters in request</span></span>
* <span data-ttu-id="599d3-152">추가 함수 적용</span><span class="sxs-lookup"><span data-stu-id="599d3-152">Apply additional functions</span></span>

<span data-ttu-id="599d3-153">실행 프로그램 `MSQuery` 호출 하 여 쿼리 `readWithCompletion` hello 개체에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-153">Execute an `MSQuery` query by calling `readWithCompletion` on hello object.</span></span>

## <span data-ttu-id="599d3-154"><a name="sorting"></a>방법: MSQuery를 사용하여 데이터 정렬</span><span class="sxs-lookup"><span data-stu-id="599d3-154"><a name="sorting"></a>How to: Sort Data with MSQuery</span></span>
<span data-ttu-id="599d3-155">toosort 결과 예를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-155">toosort results, let's look at an example.</span></span> <span data-ttu-id="599d3-156">필드 'text' 오름차순 다음 'complete' 내림차순으로 toosort 호출 `MSQuery` 같이:</span><span class="sxs-lookup"><span data-stu-id="599d3-156">toosort by field 'text' ascending, then by 'complete' descending, invoke `MSQuery` like so:</span></span>

<span data-ttu-id="599d3-157">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="599d3-157">**Objective-C**:</span></span>

```
[query orderByAscending:@"text"];
[query orderByDescending:@"complete"];
[query readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

<span data-ttu-id="599d3-158">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="599d3-158">**Swift**:</span></span>

```
query.orderByAscending("text")
query.orderByDescending("complete")
query.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```


## <span data-ttu-id="599d3-159"><a name="selecting"></a><a name="parameters"></a>방법: MSQuery를 사용하여 필드 제한 및 쿼리 문자열 매개 변수 확장</span><span class="sxs-lookup"><span data-stu-id="599d3-159"><a name="selecting"></a><a name="parameters"></a>How to: Limit Fields and Expand Query String Parameters with MSQuery</span></span>
<span data-ttu-id="599d3-160">hello에 hello 필드의 hello 이름을 지정 하는 쿼리에서 반환 된 toolimit 필드 toobe **selectFields** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-160">toolimit fields toobe returned in a query, specify hello names of hello fields in hello **selectFields** property.</span></span> <span data-ttu-id="599d3-161">이 예에서는 hello 텍스트 및 완료 된 필드를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-161">This example returns only hello text and completed fields:</span></span>

<span data-ttu-id="599d3-162">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="599d3-162">**Objective-C**:</span></span>

```
query.selectFields = @[@"text", @"complete"];
```

<span data-ttu-id="599d3-163">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="599d3-163">**Swift**:</span></span>

```
query.selectFields = ["text", "complete"]
```

<span data-ttu-id="599d3-164">서버 hello에에서 tooinclude 추가 쿼리 문자열 매개 변수 (예를 들어 있기 때문에 요청 하는 사용자 지정 서버 쪽 스크립트 사용)를 채울 `query.parameters` 같이:</span><span class="sxs-lookup"><span data-stu-id="599d3-164">tooinclude additional query string parameters in hello server request (for example, because a custom server-side script uses them), populate `query.parameters` like so:</span></span>

<span data-ttu-id="599d3-165">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="599d3-165">**Objective-C**:</span></span>

```
query.parameters = @{
    @"myKey1" : @"value1",
    @"myKey2" : @"value2",
};
```

<span data-ttu-id="599d3-166">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="599d3-166">**Swift**:</span></span>

```
query.parameters = ["myKey1": "value1", "myKey2": "value2"]
```

## <span data-ttu-id="599d3-167"><a name="paging"></a>방법: 페이지 크기 구성</span><span class="sxs-lookup"><span data-stu-id="599d3-167"><a name="paging"></a>How to: Configure Page Size</span></span>
<span data-ttu-id="599d3-168">Azure 모바일 앱으로 hello 페이지 크기 컨트롤 hello 백 엔드 테이블에서 한 번에는 찾아볼 수 있는 레코드 수가 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-168">With Azure Mobile Apps, hello page size controls hello number of records that are pulled at a time from hello backend tables.</span></span> <span data-ttu-id="599d3-169">호출을 통해서도`pull` 데이터는 다음 없습니다 자세한 레코드 toopull 없을 때까지이 페이지 크기에 따라 데이터를 일괄 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-169">A call too`pull` data would then batch up data, based on this page size, until there are no more records toopull.</span></span>

<span data-ttu-id="599d3-170">가능한 tooconfigure 사용 하 여 페이지 크기는 **MSPullSettings** 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-170">It's possible tooconfigure a page size using **MSPullSettings** as shown below.</span></span> <span data-ttu-id="599d3-171">hello 기본 페이지 크기는 50, 한 hello 감시할 다시 too3입니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-171">hello default page size is 50, and hello example below changes it too3.</span></span>

<span data-ttu-id="599d3-172">성능상의 이유로 다른 페이지 크기를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-172">You could configure a different page size for performance reasons.</span></span> <span data-ttu-id="599d3-173">많은 수의 작은 데이터 레코드를 설정한 경우 높은 페이지 크기는 hello 서버 왕복 횟수를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-173">If you have a large number of small data records, a high page size reduces hello number of server round-trips.</span></span>

<span data-ttu-id="599d3-174">이 설정은 hello 클라이언트 쪽에서만 hello 페이지 크기를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-174">This setting controls only hello page size on hello client side.</span></span> <span data-ttu-id="599d3-175">Hello 페이지 크기는 hello 클라이언트 hello 모바일 앱 백 엔드 지 원하는 것 보다 더 큰 페이지 크기에 대 한 요청을 하면 구성 된 toosupport는 hello 최대 hello 백 엔드 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-175">If hello client asks for a larger page size than hello Mobile Apps backend supports, hello page size is capped at hello maximum hello backend is configured toosupport.</span></span>

<span data-ttu-id="599d3-176">이 설정은 hello 이기도 *번호* 데이터 레코드의 하지 hello *바이트 크기*합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-176">This setting is also hello *number* of data records, not hello *byte size*.</span></span>

<span data-ttu-id="599d3-177">Hello 클라이언트 페이지 크기를 늘리면 hello 서버의 hello 페이지 크기를 늘려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-177">If you increase hello client page size, you should also increase hello page size on hello server.</span></span> <span data-ttu-id="599d3-178">참조 ["방법: hello 테이블 페이징 크기 조정"](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) hello 단계 toodo이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-178">See ["How to: Adjust hello table paging size"](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for hello steps toodo this.</span></span>

<span data-ttu-id="599d3-179">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="599d3-179">**Objective-C**:</span></span>

```
  MSPullSettings *pullSettings = [[MSPullSettings alloc] initWithPageSize:3];
  [table  pullWithQuery:query queryId:@nil settings:pullSettings
                        completion:^(NSError * _Nullable error) {
                               if(error) {
                    NSLog(@"ERROR %@", error);
                }
                           }];
```


<span data-ttu-id="599d3-180">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="599d3-180">**Swift**:</span></span>

```
let pullSettings = MSPullSettings(pageSize: 3)
table.pullWithQuery(query, queryId:nil, settings: pullSettings) { (error) in
    if let err = error {
        print("ERROR ", err)
    }
}
```

## <span data-ttu-id="599d3-181"><a name="inserting"></a>방법: 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="599d3-181"><a name="inserting"></a>How to: Insert Data</span></span>
<span data-ttu-id="599d3-182">tooinsert 새 테이블 행을 만듭니다는 `NSDictionary` 호출 `table insert`합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-182">tooinsert a new table row, create a `NSDictionary` and invoke `table insert`.</span></span> <span data-ttu-id="599d3-183">경우 [동적 스키마] 은 활성화 hello Azure 앱 서비스 모바일 백 엔드를 자동으로 생성 hello를 기반으로 새 열 `NSDictionary`합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-183">If [Dynamic Schema] is enabled, hello Azure App Service mobile backend automatically generates new columns based on hello `NSDictionary`.</span></span>

<span data-ttu-id="599d3-184">경우 `id` 을 제공 하지 않으면 새 고유 ID를 자동으로 생성 하는 hello 백 엔드</span><span class="sxs-lookup"><span data-stu-id="599d3-184">If `id` is not provided, hello backend automatically generates a new unique ID.</span></span> <span data-ttu-id="599d3-185">사용자 고유의 제공 `id` toouse 전자 메일 주소, 사용자 이름, 또는 사용자 고유의 사용자 지정 값을 id입니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-185">Provide your own `id` toouse email addresses, usernames, or your own custom values as ID.</span></span> <span data-ttu-id="599d3-186">고유한 ID를 제공하면 조인 및 비즈니스 지향적인 데이터베이스 논리가 쉬을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-186">Providing your own ID may ease joins and business-oriented database logic.</span></span>

<span data-ttu-id="599d3-187">hello `result` hello 삽입 된 새 항목을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-187">hello `result` contains hello new item that was inserted.</span></span> <span data-ttu-id="599d3-188">사용자 서버 논리에 따라 추가 있을 수 있습니다 또는 수정 된 데이터 비교 toowhat toohello 서버에 전달 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-188">Depending on your server logic, it may have additional or modified data compared toowhat was passed toohello server.</span></span>

<span data-ttu-id="599d3-189">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="599d3-189">**Objective-C**:</span></span>

```
NSDictionary *newItem = @{@"id": @"custom-id", @"text": @"my new item", @"complete" : @NO};
[table insert:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="599d3-190">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="599d3-190">**Swift**:</span></span>

```
let newItem = ["id": "custom-id", "text": "my new item", "complete": false]
table.insert(newItem) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

## <span data-ttu-id="599d3-191"><a name="modifying"></a>방법: 데이터 수정</span><span class="sxs-lookup"><span data-stu-id="599d3-191"><a name="modifying"></a>How to: Modify Data</span></span>
<span data-ttu-id="599d3-192">기존 행 tooupdate 수정 항목 및 호출 `update`:</span><span class="sxs-lookup"><span data-stu-id="599d3-192">tooupdate an existing row, modify an item and call `update`:</span></span>

<span data-ttu-id="599d3-193">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="599d3-193">**Objective-C**:</span></span>

```
NSMutableDictionary *newItem = [oldItem mutableCopy]; // oldItem is NSDictionary
[newItem setValue:@"Updated text" forKey:@"text"];
[table update:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="599d3-194">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="599d3-194">**Swift**:</span></span>

```
if let newItem = oldItem.mutableCopy() as? NSMutableDictionary {
    newItem["text"] = "Updated text"
    table2.update(newItem as [NSObject: AnyObject], completion: { (result, error) -> Void in
        if let err = error {
            print("ERROR ", err)
        } else if let item = result {
            print("Todo Item: ", item["text"])
        }
    })
}
```

<span data-ttu-id="599d3-195">Hello 행 ID 및 업데이트 하는 hello 필드 입력 또는:</span><span class="sxs-lookup"><span data-stu-id="599d3-195">Alternatively, supply hello row ID and hello updated field:</span></span>

<span data-ttu-id="599d3-196">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="599d3-196">**Objective-C**:</span></span>

```
[table update:@{@"id":@"custom-id", @"text":"my EDITED item"} completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="599d3-197">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="599d3-197">**Swift**:</span></span>

```
table.update(["id": "custom-id", "text": "my EDITED item"]) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

<span data-ttu-id="599d3-198">최소한 hello `id` 로 업데이트할 때 특성을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-198">At minimum, hello `id` attribute must be set when making updates.</span></span>

## <span data-ttu-id="599d3-199"><a name="deleting"></a>방법: Blob 삭제</span><span class="sxs-lookup"><span data-stu-id="599d3-199"><a name="deleting"></a>How to: Delete Data</span></span>
<span data-ttu-id="599d3-200">항목을 toodelete 호출 `delete` hello 항목:</span><span class="sxs-lookup"><span data-stu-id="599d3-200">toodelete an item, invoke `delete` with hello item:</span></span>

<span data-ttu-id="599d3-201">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="599d3-201">**Objective-C**:</span></span>

```
[table delete:item completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

<span data-ttu-id="599d3-202">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="599d3-202">**Swift**:</span></span>

```
table.delete(newItem as [NSObject: AnyObject]) { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

<span data-ttu-id="599d3-203">또는 행 ID를 제공하여 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-203">Alternatively, delete by providing a row ID:</span></span>

<span data-ttu-id="599d3-204">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="599d3-204">**Objective-C**:</span></span>

```
[table deleteWithId:@"37BBF396-11F0-4B39-85C8-B319C729AF6D" completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

<span data-ttu-id="599d3-205">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="599d3-205">**Swift**:</span></span>

```
table.deleteWithId("37BBF396-11F0-4B39-85C8-B319C729AF6D") { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

<span data-ttu-id="599d3-206">최소한 hello `id` 을 삭제 하는 경우 특성을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-206">At minimum, hello `id` attribute must be set when making deletes.</span></span>

## <span data-ttu-id="599d3-207"><a name="customapi"></a>방법: 사용자 지정 API 호출</span><span class="sxs-lookup"><span data-stu-id="599d3-207"><a name="customapi"></a>How to: Call Custom API</span></span>
<span data-ttu-id="599d3-208">사용자 지정 API를 사용하여 백 엔드 기능을 노출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-208">With a custom API, you can expose any backend functionality.</span></span> <span data-ttu-id="599d3-209">Toomap tooa 테이블 작업이 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-209">It doesn't have toomap tooa table operation.</span></span> <span data-ttu-id="599d3-210">메시징를 보다 상세하게 할 경우에 마찬가지 수 뿐만 아니라 읽기/set 헤더 및 hello 응답 본문 형식을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-210">Not only do you gain more control over messaging, you can even read/set headers and change hello response body format.</span></span> <span data-ttu-id="599d3-211">hello 백 엔드에 사용자 지정 API toocreate 읽으려면 어떻게 toolearn [사용자 지정 Api](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)</span><span class="sxs-lookup"><span data-stu-id="599d3-211">toolearn how toocreate a custom API on hello backend, read [Custom APIs](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)</span></span>

<span data-ttu-id="599d3-212">사용자 지정 API toocall 호출 `MSClient.invokeAPI`합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-212">toocall a custom API, call `MSClient.invokeAPI`.</span></span> <span data-ttu-id="599d3-213">hello 요청 및 응답 콘텐츠를 JSON으로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-213">hello request and response content are treated as JSON.</span></span> <span data-ttu-id="599d3-214">toouse 다른 미디어 유형에 [사용의 다른 오버 로드를 hello `invokeAPI` ] [ 5]합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-214">toouse other media types, [use hello other overload of `invokeAPI`][5].</span></span>  <span data-ttu-id="599d3-215">toomake는 `GET` 대신의 요청에 대 한 `POST` 집합 매개 변수를 요청 `HTTPMethod` 너무`"GET"` 및 매개 변수 `body` 너무`nil` (없으므로 GET 요청 메시지의 본문입니다.) 사용자 지정 API가 다른 HTTP 동사를 지원하는 경우 `HTTPMethod`을(를) 적절하게 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-215">toomake a `GET` request instead of a `POST` request, set parameter `HTTPMethod` too`"GET"` and parameter `body` too`nil` (since GET requests do not have message bodies.) If your custom API supports other HTTP verbs, change `HTTPMethod` appropriately.</span></span>

<span data-ttu-id="599d3-216">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="599d3-216">**Objective-C**:</span></span>

```
[self.client invokeAPI:@"sendEmail"
                  body:@{ @"contents": @"Hello world!" }
            HTTPMethod:@"POST"
            parameters:@{ @"to": @"bill@contoso.com", @"subject" : @"Hi!" }
               headers:nil
            completion: ^(NSData *result, NSHTTPURLResponse *response, NSError *error) {
                if(error) {
                    NSLog(@"ERROR %@", error);
                } else {
                    // Do something with result
                }
            }];
```

<span data-ttu-id="599d3-217">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="599d3-217">**Swift**:</span></span>

```
client.invokeAPI("sendEmail",
            body: [ "contents": "Hello World" ],
            HTTPMethod: "POST",
            parameters: [ "to": "bill@contoso.com", "subject" : "Hi!" ],
            headers: nil)
            {
                (result, response, error) -> Void in
                if let err = error {
                    print("ERROR ", err)
                } else if let res = result {
                          // Do something with result
                }
        }
```

## <span data-ttu-id="599d3-218"><a name="templates"></a>방법: 레지스터 푸시 템플릿 toosend 플랫폼 간 알림</span><span class="sxs-lookup"><span data-stu-id="599d3-218"><a name="templates"></a>How to: Register push templates toosend cross-platform notifications</span></span>
<span data-ttu-id="599d3-219">tooregister 템플릿을 사용 하 여 템플릿을 전달 프로그램 **client.push registerDeviceToken** 클라이언트 응용 프로그램에서 메서드.</span><span class="sxs-lookup"><span data-stu-id="599d3-219">tooregister templates, pass templates with your **client.push registerDeviceToken** method in your client app.</span></span>

<span data-ttu-id="599d3-220">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="599d3-220">**Objective-C**:</span></span>

```
[client.push registerDeviceToken:deviceToken template:iOSTemplate completion:^(NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    }
}];
```

<span data-ttu-id="599d3-221">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="599d3-221">**Swift**:</span></span>

```
    client.push?.registerDeviceToken(NSData(), template: iOSTemplate, completion: { (error) in
        if let err = error {
            print("ERROR ", err)
        }
    })
```

<span data-ttu-id="599d3-222">템플릿을은 NSDictionary 형식의 이며 형식에 따라 hello에 템플릿이 여러 개 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-222">Your templates are of type NSDictionary and can contain multiple templates in hello following format:</span></span>

<span data-ttu-id="599d3-223">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="599d3-223">**Objective-C**:</span></span>

```
NSDictionary *iOSTemplate = @{ @"templateName": @{ @"body": @{ @"aps": @{ @"alert": @"$(message)" } } } };
```

<span data-ttu-id="599d3-224">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="599d3-224">**Swift**:</span></span>

```
let iOSTemplate = ["templateName": ["body": ["aps": ["alert": "$(message)"]]]]
```

<span data-ttu-id="599d3-225">모든 태그는 보안에 대 한 hello 요청에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-225">All tags are stripped from hello request for security.</span></span>  <span data-ttu-id="599d3-226">tooadd 태그 tooinstallations 또는 설치에서 템플릿을 참조 하십시오. [Azure 모바일 앱에 대 한 hello.NET 백 엔드 서버 SDK에서 작동][4]합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-226">tooadd tags tooinstallations or templates within installations, see [Work with hello .NET backend server SDK for Azure Mobile Apps][4].</span></span>  <span data-ttu-id="599d3-227">등록 된 이러한 템플릿을 사용 하 여 toosend 알림 작업할 [알림 허브 Api][3]합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-227">toosend notifications using these registered templates, work with [Notification Hubs APIs][3].</span></span>

## <span data-ttu-id="599d3-228"><a name="errors"></a>방법: 오류 처리</span><span class="sxs-lookup"><span data-stu-id="599d3-228"><a name="errors"></a>How to: Handle Errors</span></span>
<span data-ttu-id="599d3-229">Hello 완성 블록에 포함 되어 Azure 앱 서비스 모바일 백 엔드를 호출 하는 경우는 `NSError` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-229">When you call an Azure App Service mobile backend, hello completion block contains an `NSError` parameter.</span></span> <span data-ttu-id="599d3-230">오류가 발생하면 이 매개 변수는 null이 아닌 값입니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-230">When an error occurs, this parameter is non-nil.</span></span> <span data-ttu-id="599d3-231">코드에서이 매개 변수를 확인 하 고 hello 앞에 코드 조각에서에서와 같이 필요에 따라 hello 오류를 처리 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-231">In your code, you should check this parameter and handle hello error as needed, as demonstrated in hello preceding code snippets.</span></span>

<span data-ttu-id="599d3-232">hello 파일 [ `<WindowsAzureMobileServices/MSError.h>` ] [ 6] hello 상수를 정의 `MSErrorResponseKey`, `MSErrorRequestKey`, 및 `MSErrorServerItemKey`합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-232">hello file [`<WindowsAzureMobileServices/MSError.h>`][6] defines hello constants `MSErrorResponseKey`, `MSErrorRequestKey`, and `MSErrorServerItemKey`.</span></span> <span data-ttu-id="599d3-233">tooget 더 많은 데이터가 관련 toohello 오류:</span><span class="sxs-lookup"><span data-stu-id="599d3-233">tooget more data related toohello error:</span></span>

<span data-ttu-id="599d3-234">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="599d3-234">**Objective-C**:</span></span>

```
NSDictionary *serverItem = [error.userInfo objectForKey:MSErrorServerItemKey];
```

<span data-ttu-id="599d3-235">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="599d3-235">**Swift**:</span></span>

```
let serverItem = error.userInfo[MSErrorServerItemKey]
```

<span data-ttu-id="599d3-236">또한 hello 파일 각 오류 코드에 대 한 상수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-236">In addition, hello file defines constants for each error code:</span></span>

<span data-ttu-id="599d3-237">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="599d3-237">**Objective-C**:</span></span>

```
if (error.code == MSErrorPreconditionFailed) {
```

<span data-ttu-id="599d3-238">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="599d3-238">**Swift**:</span></span>

```
if (error.code == MSErrorPreconditionFailed) {
```

## <span data-ttu-id="599d3-239"><a name="adal"></a>방법: Active Directory 인증 라이브러리 hello로 사용자를 인증</span><span class="sxs-lookup"><span data-stu-id="599d3-239"><a name="adal"></a>How to: Authenticate users with hello Active Directory Authentication Library</span></span>
<span data-ttu-id="599d3-240">Hello Active Directory 인증 라이브러리 (ADAL) toosign 사용자가 Azure Active Directory를 사용 하 여 응용 프로그램에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-240">You can use hello Active Directory Authentication Library (ADAL) toosign users into your application using Azure Active Directory.</span></span> <span data-ttu-id="599d3-241">클라이언트 흐름 인증 id 공급자 SDK를 사용 하는 것이 좋습니다 toousing hello `loginWithProvider:completion:` 메서드.</span><span class="sxs-lookup"><span data-stu-id="599d3-241">Client flow authentication using an identity provider SDK is preferable toousing hello `loginWithProvider:completion:` method.</span></span>  <span data-ttu-id="599d3-242">클라이언트 흐름 인증은 UX 느낌을 그대로 제공하고 추가 사용자 지정을 허용하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-242">Client flow authentication provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="599d3-243">다음 hello 하 여 AAD 로그인에 대 한 모바일 앱 백 엔드 구성 [tooconfigure Active Directory 로그인에 대 한 서비스 응용 프로그램 방법] [ 7] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-243">Configure your mobile app backend for AAD sign-in by following hello [How tooconfigure App Service for Active Directory login][7] tutorial.</span></span> <span data-ttu-id="599d3-244">네이티브 클라이언트 응용 프로그램 등록 되었는지 toocomplete hello 선택적 단계를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-244">Make sure toocomplete hello optional step of registering a native client application.</span></span> <span data-ttu-id="599d3-245">Ios의 경우 해당 hello 리디렉션 URI는 hello 폼의 권장 `<app-scheme>://<bundle-id>`합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-245">For iOS, we recommend that hello redirect URI is of hello form `<app-scheme>://<bundle-id>`.</span></span> <span data-ttu-id="599d3-246">자세한 내용은 참조 hello [ADAL iOS 퀵 스타트][8]합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-246">For more information, see hello [ADAL iOS quickstart][8].</span></span>
2. <span data-ttu-id="599d3-247">Cocoapods를 사용하여 ADAL을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-247">Install ADAL using Cocoapods.</span></span> <span data-ttu-id="599d3-248">다음 정의 대체 Podfile tooinclude hello 편집 **귀하가 프로젝트** Xcode 프로젝트의 hello 이름의:</span><span class="sxs-lookup"><span data-stu-id="599d3-248">Edit your Podfile tooinclude hello following definition, replacing **YOUR-PROJECT** with hello name of your Xcode project:</span></span>

        source 'https://github.com/CocoaPods/Specs.git'
        link_with ['YOUR-PROJECT']
        xcodeproj 'YOUR-PROJECT'

   <span data-ttu-id="599d3-249">및 Pod hello:</span><span class="sxs-lookup"><span data-stu-id="599d3-249">and hello Pod:</span></span>

        pod 'ADALiOS'
3. <span data-ttu-id="599d3-250">실행 하는 hello 터미널을 사용 하 여 `pod install` hello 디렉터리에서 프로젝트를 포함 하 고 다음 생성 된 hello hello 프로젝트가 아닌 Xcode 작업 영역을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-250">Using hello Terminal, run `pod install` from hello directory containing your project, and then open hello generated Xcode workspace (not hello project).</span></span>
4. <span data-ttu-id="599d3-251">다음 코드 tooyour 응용 프로그램, 사용 중인 toohello 언어에 따라 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-251">Add hello following code tooyour application, according toohello language you are using.</span></span> <span data-ttu-id="599d3-252">각 코드에서 다음과 같이 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-252">In each, make these replacements:</span></span>

   * <span data-ttu-id="599d3-253">대체 **INSERT-기관-여기** hello 테 넌 트 응용 프로그램을 프로 비전 하는 hello 이름의 합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-253">Replace **INSERT-AUTHORITY-HERE** with hello name of hello tenant in which you provisioned your application.</span></span> <span data-ttu-id="599d3-254">형식은 https://login.microsoftonline.com/contoso.onmicrosoft.com이어야 합니다. Hello [Azure 클래식 포털]에서 Azure Active Directory의 hello 도메인 탭에서이 값을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-254">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com. This value can be copied from hello Domain tab in your Azure Active Directory in hello [Azure classic portal].</span></span>
   * <span data-ttu-id="599d3-255">대체 **리소스 ID 여기 삽입** 모바일 앱 백 엔드에 대 한 hello 클라이언트 ID로 합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-255">Replace **INSERT-RESOURCE-ID-HERE** with hello client ID for your mobile app backend.</span></span> <span data-ttu-id="599d3-256">Hello에서 클라이언트 ID를 가져올 수 **고급** 탭의 **Azure Active Directory 설정** hello 포털에서입니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-256">You can obtain the client ID from hello **Advanced** tab under **Azure Active Directory Settings** in hello portal.</span></span>
   * <span data-ttu-id="599d3-257">대체 **클라이언트 ID 여기 삽입** hello 네이티브 클라이언트 응용 프로그램에서 복사한 hello 클라이언트 ID로 합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-257">Replace **INSERT-CLIENT-ID-HERE** with hello client ID you copied from hello native client application.</span></span>
   * <span data-ttu-id="599d3-258">대체 **리디렉션 URI 여기 삽입** 웹 사이트와 */.auth/login/done* hello HTTPS 체계를 사용 하 여 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-258">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using hello HTTPS scheme.</span></span> <span data-ttu-id="599d3-259">이 값은 형태가 됩니다 너무*https://contoso.azurewebsites.net/.auth/login/done*합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-259">This value should be similar too*https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

<span data-ttu-id="599d3-260">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="599d3-260">**Objective-C**:</span></span>

    #import <ADALiOS/ADAuthenticationContext.h>
    #import <ADALiOS/ADAuthenticationSettings.h>
    // ...
    - (void) authenticate:(UIViewController*) parent
               completion:(void (^) (MSUser*, NSError*))completionBlock;
    {
        NSString *authority = @"INSERT-AUTHORITY-HERE";
        NSString *resourceId = @"INSERT-RESOURCE-ID-HERE";
        NSString *clientId = @"INSERT-CLIENT-ID-HERE";
        NSURL *redirectUri = [[NSURL alloc]initWithString:@"INSERT-REDIRECT-URI-HERE"];
        ADAuthenticationError *error;
        ADAuthenticationContext *authContext = [ADAuthenticationContext authenticationContextWithAuthority:authority error:&error];
        authContext.parentController = parent;
        [ADAuthenticationSettings sharedInstance].enableFullScreen = YES;
        [authContext acquireTokenWithResource:resourceId
                                     clientId:clientId
                                  redirectUri:redirectUri
                              completionBlock:^(ADAuthenticationResult *result) {
                                  if (result.status != AD_SUCCEEDED)
                                  {
                                      completionBlock(nil, result.error);;
                                  }
                                  else
                                  {
                                      NSDictionary *payload = @{
                                                                @"access_token" : result.tokenCacheStoreItem.accessToken
                                                                };
                                      [client loginWithProvider:@"aad" token:payload completion:completionBlock];
                                  }
                              }];
    }


<span data-ttu-id="599d3-261">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="599d3-261">**Swift**:</span></span>

    // add hello following imports tooyour bridging header:
    //        #import <ADALiOS/ADAuthenticationContext.h>
    //        #import <ADALiOS/ADAuthenticationSettings.h>

    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let authority = "INSERT-AUTHORITY-HERE"
        let resourceId = "INSERT-RESOURCE-ID-HERE"
        let clientId = "INSERT-CLIENT-ID-HERE"
        let redirectUri = NSURL(string: "INSERT-REDIRECT-URI-HERE")
        var error: AutoreleasingUnsafeMutablePointer<ADAuthenticationError?> = nil
        let authContext = ADAuthenticationContext(authority: authority, error: error)
        authContext.parentController = parent
        ADAuthenticationSettings.sharedInstance().enableFullScreen = true
        authContext.acquireTokenWithResource(resourceId, clientId: clientId, redirectUri: redirectUri) { (result) in
                if result.status != AD_SUCCEEDED {
                    completion(nil, result.error)
                }
                else {
                    let payload: [String: String] = ["access_token": result.tokenCacheStoreItem.accessToken]
                    client.loginWithProvider("aad", token: payload, completion: completion)
                }
            }
    }

## <span data-ttu-id="599d3-262"><a name="facebook-sdk"></a>방법: iOS 용 hello Facebook SDK로 사용자를 인증</span><span class="sxs-lookup"><span data-stu-id="599d3-262"><a name="facebook-sdk"></a>How to: Authenticate users with hello Facebook SDK for iOS</span></span>
<span data-ttu-id="599d3-263">Facebook을 사용 하 여 응용 프로그램에 iOS toosign 사용자를 위한 hello Facebook SDK를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-263">You can use hello Facebook SDK for iOS toosign users into your application using Facebook.</span></span>  <span data-ttu-id="599d3-264">선호 toousing hello은 클라이언트 흐름 인증을 사용 하 여 `loginWithProvider:completion:` 메서드.</span><span class="sxs-lookup"><span data-stu-id="599d3-264">Using a client flow authentication is preferable toousing hello `loginWithProvider:completion:` method.</span></span>  <span data-ttu-id="599d3-265">원래의 UX 느낌을 제공 하 고 추가 사용자 지정을 허용 하는 hello 클라이언트 흐름 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-265">hello client flow authentication provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="599d3-266">Facebook 로그인에 대 한 모바일 앱 백 엔드에 따라 구성의 [tooconfigure Facebook 로그인에 대 한 서비스 응용 프로그램 방법] [ 9] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-266">Configure your mobile app backend for Facebook sign-in by following the [How tooconfigure App Service for Facebook login][9] tutorial.</span></span>
2. <span data-ttu-id="599d3-267">다음 hello 하 여 iOS 용 hello Facebook SDK 설치 [Facebook SDK for iOS-시작] [ 10] 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-267">Install hello Facebook SDK for iOS by following hello [Facebook SDK for iOS - Getting Started][10] documentation.</span></span> <span data-ttu-id="599d3-268">응용 프로그램을 만드는 대신 hello iOS 플랫폼 tooyour 기존 등록을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-268">Instead of creating an app, you can add hello iOS platform tooyour existing registration.</span></span>
3. <span data-ttu-id="599d3-269">Facebook의 설명서는 hello 응용 프로그램 대리자에에서 일부 Objective C 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-269">Facebook's documentation includes some Objective-C code in hello App Delegate.</span></span> <span data-ttu-id="599d3-270">사용 중인 경우 **Swift**, hello 다음 AppDelegate.swift에 대 한 번역을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-270">If you are using **Swift**, you can use hello following translations for AppDelegate.swift:</span></span>

        // Add hello following import tooyour bridging header:
        //        #import <FBSDKCoreKit/FBSDKCoreKit.h>

        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            FBSDKApplicationDelegate.sharedInstance().application(application, didFinishLaunchingWithOptions: launchOptions)
            // Add any custom logic here.
            return true
        }

        func application(application: UIApplication, openURL url: NSURL, sourceApplication: String?, annotation: AnyObject?) -> Bool {
            let handled = FBSDKApplicationDelegate.sharedInstance().application(application, openURL: url, sourceApplication: sourceApplication, annotation: annotation)
            // Add any custom logic here.
            return handled
        }
4. <span data-ttu-id="599d3-271">또한 tooadding에서 `FBSDKCoreKit.framework` tooyour 프로젝트를 너무 한 참조도 추가`FBSDKLoginKit.framework` hello에서 같은 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-271">In addition tooadding `FBSDKCoreKit.framework` tooyour project, also add a reference too`FBSDKLoginKit.framework` in hello same way.</span></span>
5. <span data-ttu-id="599d3-272">다음 코드 tooyour 응용 프로그램, 사용 중인 toohello 언어에 따라 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-272">Add hello following code tooyour application, according toohello language you are using.</span></span>

<span data-ttu-id="599d3-273">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="599d3-273">**Objective-C**:</span></span>

    #import <FBSDKLoginKit/FBSDKLoginKit.h>
    #import <FBSDKCoreKit/FBSDKAccessToken.h>
    // ...
    - (void) authenticate:(UIViewController*) parent
               completion:(void (^) (MSUser*, NSError*)) completionBlock;
    {        
        FBSDKLoginManager *loginManager = [[FBSDKLoginManager alloc] init];
        [loginManager
         logInWithReadPermissions: @[@"public_profile"]
         fromViewController:parent
         handler:^(FBSDKLoginManagerLoginResult *result, NSError *error) {
             if (error) {
                 completionBlock(nil, error);
             } else if (result.isCancelled) {
                 completionBlock(nil, error);
             } else {
                 NSDictionary *payload = @{
                                           @"access_token":result.token.tokenString
                                           };
                 [client loginWithProvider:@"facebook" token:payload completion:completionBlock];
             }
         }];
    }

<span data-ttu-id="599d3-274">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="599d3-274">**Swift**:</span></span>

    // Add hello following imports tooyour bridging header:
    //        #import <FBSDKLoginKit/FBSDKLoginKit.h>
    //        #import <FBSDKCoreKit/FBSDKAccessToken.h>

    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let loginManager = FBSDKLoginManager()
        loginManager.logInWithReadPermissions(["public_profile"], fromViewController: parent) { (result, error) in
            if (error != nil) {
                completion(nil, error)
            }
            else if result.isCancelled {
                completion(nil, error)
            }
            else {
                let payload: [String: String] = ["access_token": result.token.tokenString]
                client.loginWithProvider("facebook", token: payload, completion: completion)
            }
        }
    }

## <span data-ttu-id="599d3-275"><a name="twitter-fabric"></a>방법: iOS용 Twitter Fabric을 사용하여 사용자 인증</span><span class="sxs-lookup"><span data-stu-id="599d3-275"><a name="twitter-fabric"></a>How to: Authenticate users with Twitter Fabric for iOS</span></span>
<span data-ttu-id="599d3-276">Twitter를 사용 하 여 응용 프로그램에 iOS toosign 사용자에 대 한 패브릭을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-276">You can use Fabric for iOS toosign users into your application using Twitter.</span></span> <span data-ttu-id="599d3-277">흐름 인증 클라이언트는 것이 좋습니다 toousing hello `loginWithProvider:completion:` 메서드를 더 UX 느낌을 제공 하며 추가 사용자 지정을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-277">Client Flow authentication is preferable toousing hello `loginWithProvider:completion:` method, as it provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="599d3-278">Twitter 로그인에 대 한 모바일 앱 백 엔드 hello를 수행 하 여 구성 [tooconfigure Twitter 로그인에 대 한 서비스 응용 프로그램 방법](app-service-mobile-how-to-configure-twitter-authentication.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-278">Configure your mobile app backend for Twitter sign-in by following hello [How tooconfigure App Service for Twitter login](app-service-mobile-how-to-configure-twitter-authentication.md) tutorial.</span></span>
2. <span data-ttu-id="599d3-279">다음 hello 하 여 패브릭 tooyour 프로젝트 추가 [iOS-시작에 대 한 패브릭] 설명서 및 TwitterKit를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-279">Add Fabric tooyour project by following hello [Fabric for iOS - Getting Started] documentation and setting up TwitterKit.</span></span>

   > [!NOTE]
   > <span data-ttu-id="599d3-280">기본적으로 패브릭은 사용자를 위해 Twitter 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-280">By default, Fabric creates a Twitter application for you.</span></span> <span data-ttu-id="599d3-281">Hello 소비자 키와 이전 코드 조각 다음 hello를 사용 하 여 만든 소비자 암호를 등록 하 여 응용 프로그램을 만드는 것을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-281">You can avoid creating an application by registering hello Consumer Key and Consumer Secret you created earlier using hello following code snippets.</span></span>    <span data-ttu-id="599d3-282">또는 hello 소비자 키를 대체할 수 있습니다 및 hello에서 tooApp 서비스 hello로 값을 제공 하는 소비자 암호 값을 참조 [패브릭 대시보드]합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-282">Alternatively, you can replace hello Consumer Key and Consumer Secret values that you provide tooApp Service with hello values you see in hello [Fabric Dashboard].</span></span> <span data-ttu-id="599d3-283">이 옵션을 선택 하면 값이 될 있는지 tooset hello 콜백 URL tooa 자리 표시자와 같은 `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-283">If you choose this option, be sure tooset hello callback URL tooa placeholder value, such as `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.</span></span>
   >
   >

    <span data-ttu-id="599d3-284">Toouse 앞에서 만든 hello 비밀을 선택 하면 다음 응용 프로그램 대리자 코드 tooyour hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-284">If you choose toouse hello secrets you created earlier, add hello following code tooyour App Delegate:</span></span>

    <span data-ttu-id="599d3-285">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="599d3-285">**Objective-C**:</span></span>

        #import <Fabric/Fabric.h>
        #import <TwitterKit/TwitterKit.h>
        // ...
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
            [[Twitter sharedInstance] startWithConsumerKey:@"your_key" consumerSecret:@"your_secret"];
            [Fabric with:@[[Twitter class]]];
            // Add any custom logic here.
            return YES;
        }

    <span data-ttu-id="599d3-286">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="599d3-286">**Swift**:</span></span>

        import Fabric
        import TwitterKit
        // ...
        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            Twitter.sharedInstance().startWithConsumerKey("your_key", consumerSecret: "your_secret")
            Fabric.with([Twitter.self])
            // Add any custom logic here.
            return true
        }
3. <span data-ttu-id="599d3-287">다음 코드 tooyour 응용 프로그램, 사용 중인 toohello 언어에 따라 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-287">Add hello following code tooyour application, according toohello language you are using.</span></span>

<span data-ttu-id="599d3-288">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="599d3-288">**Objective-C**:</span></span>

    #import <TwitterKit/TwitterKit.h>
    // ...
    - (void)authenticate:(UIViewController*)parent completion:(void (^) (MSUser*, NSError*))completionBlock
    {
        [[Twitter sharedInstance] logInWithCompletion:^(TWTRSession *session, NSError *error) {
            if (session) {
                NSDictionary *payload = @{
                                            @"access_token":session.authToken,
                                            @"access_token_secret":session.authTokenSecret
                                        };
                [client loginWithProvider:@"twitter" token:payload completion:completionBlock];
            } else {
                completionBlock(nil, error);
            }
        }];
    }

<span data-ttu-id="599d3-289">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="599d3-289">**Swift**:</span></span>

    import TwitterKit
    // ...
    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let client = self.table!.client
        Twitter.sharedInstance().logInWithCompletion { session, error in
            if (session != nil) {
                let payload: [String: String] = ["access_token": session!.authToken, "access_token_secret": session!.authTokenSecret]
                client.loginWithProvider("twitter", token: payload, completion: completion)
            } else {
                completion(nil, error)
            }
        }
    }

## <span data-ttu-id="599d3-290"><a name="google-sdk"></a>방법: iOS 용 Google 로그인 SDK hello로 사용자를 인증</span><span class="sxs-lookup"><span data-stu-id="599d3-290"><a name="google-sdk"></a>How to: Authenticate users with hello Google Sign-In SDK for iOS</span></span>
<span data-ttu-id="599d3-291">Google 계정을 사용 하 여 응용 프로그램에 iOS toosign 사용자를 위한 hello Google 로그인 SDK를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-291">You can use hello Google Sign-In SDK for iOS toosign users into your application using a Google account.</span></span>  <span data-ttu-id="599d3-292">Google에 변경 내용을 tootheir OAuth 보안 정책을 최근에 발표 했습니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-292">Google recently announced changes tootheir OAuth security policies.</span></span>  <span data-ttu-id="599d3-293">이러한 정책 변경 내용은 향후 hello에서 Google SDK의 hello 사용을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-293">These policy changes will require hello use of the Google SDK in hello future.</span></span>

1. <span data-ttu-id="599d3-294">다음 hello 여 Google 로그인에 대 한 모바일 앱 백 엔드 구성 [tooconfigure Google 로그인에 대 한 서비스 응용 프로그램 방법](app-service-mobile-how-to-configure-google-authentication.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-294">Configure your mobile app backend for Google sign-in by following hello [How tooconfigure App Service for Google login](app-service-mobile-how-to-configure-google-authentication.md) tutorial.</span></span>
2. <span data-ttu-id="599d3-295">다음 hello 하 여 iOS 용 hello Google SDK 설치 [Google 로그인 iOS-에 대 한 통합을 시작](https://developers.google.com/identity/sign-in/ios/start-integrating) 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-295">Install hello Google SDK for iOS by following hello [Google Sign-In for iOS - Start integrating](https://developers.google.com/identity/sign-in/ios/start-integrating) documentation.</span></span> <span data-ttu-id="599d3-296">Hello "인증를 사용 하 여 백 엔드" 섹션을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-296">You may skip hello "Authenticate with a Backend Server" section.</span></span>
3. <span data-ttu-id="599d3-297">Hello tooyour 대리자의 다음 추가 `signIn:didSignInForUser:withError:` 메서드를 사용 하는 toohello 언어에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-297">Add hello following tooyour delegate's `signIn:didSignInForUser:withError:` method, according toohello language you are using.</span></span>

<span data-ttu-id="599d3-298">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="599d3-298">**Objective-C**:</span></span>

        NSDictionary *payload = @{
                                  @"id_token":user.authentication.idToken,
                                  @"authorization_code":user.serverAuthCode
                                  };

        [client loginWithProvider:@"google" token:payload completion:^(MSUser *user, NSError *error) {
            // ...
        }];

<span data-ttu-id="599d3-299">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="599d3-299">**Swift**:</span></span>

        let payload: [String: String] = ["id_token": user.authentication.idToken, "authorization_code": user.serverAuthCode]
        client.loginWithProvider("google", token: payload) { (user, error) in
            // ...
        }

1. <span data-ttu-id="599d3-300">Hello 너무 후에 추가 하 고 있는지 확인`application:didFinishLaunchingWithOptions:` 응용 프로그램에서 대리자를 해당 사용한 tooconfigure 앱 서비스 1 단계에서 ID 같습니다 "SERVER_CLIENT_ID" hello 경로로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-300">Make sure you also add hello following too`application:didFinishLaunchingWithOptions:` in your app delegate, replacing "SERVER_CLIENT_ID" with hello same ID that you used tooconfigure App Service in step 1.</span></span>

<span data-ttu-id="599d3-301">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="599d3-301">**Objective-C**:</span></span>

         [GIDSignIn sharedInstance].serverClientID = @"SERVER_CLIENT_ID";

 <span data-ttu-id="599d3-302">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="599d3-302">**Swift**:</span></span>

        GIDSignIn.sharedInstance().serverClientID = "SERVER_CLIENT_ID"


1. <span data-ttu-id="599d3-303">Hello hello를 구현 하는 UIViewController 코드 tooyour 응용 프로그램에 따라 추가 `GIDSignInUIDelegate` 프로토콜을 사용 하는 toohello 언어에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-303">Add hello following code tooyour application in a UIViewController that implements hello `GIDSignInUIDelegate` protocol, according toohello language you are using.</span></span>  <span data-ttu-id="599d3-304">로그인을 다시 하기 전에 로그 아웃 하 고 승인 대화 상자 표시 필요 없는 tooenter 자격 증명 다시 있지만 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-304">You are signed out before being signed in again, and although you don't need tooenter your credentials again, you see a consent dialog.</span></span>  <span data-ttu-id="599d3-305">Hello 세션 토큰이 만료 된 경우에이 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="599d3-305">Only call this method when hello session token has expired.</span></span>

   <span data-ttu-id="599d3-306">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="599d3-306">**Objective-C**:</span></span>

       #import <Google/SignIn.h>
       // ...
       - (void)authenticate
       {
               [GIDSignIn sharedInstance].uiDelegate = self;
               [[GIDSignIn sharedInstance] signOut];
               [[GIDSignIn sharedInstance] signIn];
        }

   <span data-ttu-id="599d3-307">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="599d3-307">**Swift**:</span></span>

       // ...
       func authenticate() {
           GIDSignIn.sharedInstance().uiDelegate = self
           GIDSignIn.sharedInstance().signOut()
           GIDSignIn.sharedInstance().signIn()
       }

<!-- Anchors. -->

[What is Mobile Services]: #what-is
[Concepts]: #concepts
[Setup and Prerequisites]: #Setup
[How to: Create hello Mobile Services client]: #create-client
[How to: Create a table reference]: #table-reference
[How to: Query data from a mobile service]: #querying
[Filter returned data]: #filtering
[Sort returned data]: #sorting
[Return data in pages]: #paging
[Select specific columns]: #selecting
[How to: Bind data toohello user interface]: #binding
[How to: Insert data into a mobile service]: #inserting
[How to: Modify data in a mobile service]: #modifying
[How to: Authenticate users]: #authentication
[Cache authentication tokens]: #caching-tokens
[How to: Upload images and large files]: #blobs
[How to: Handle errors]: #errors
[How to: Design unit tests]: #unit-testing
[How to: Customize hello client]: #customizing
[Customize request headers]: #custom-headers
[Customize data type serialization]: #custom-serialization
[Next Steps]: #next-steps
[How to: Use MSQuery]: #query-object

<!-- Images. -->

<!-- URLs. -->
[Azure 모바일 앱 빠른 시작]: app-service-mobile-ios-get-started.md

[Add Mobile Services tooExisting App]: /develop/mobile/tutorials/get-started-data
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Validate and modify data in Mobile Services by using server scripts]: /develop/mobile/tutorials/validate-modify-and-augment-data-ios
[Mobile Services SDK]: https://go.microsoft.com/fwLink/p/?LinkID=266533
[Authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[iOS SDK]: https://developer.apple.com/xcode

[Handling Expired Tokens]: http://go.microsoft.com/fwlink/p/?LinkId=301955
[Live Connect SDK]: http://go.microsoft.com/fwlink/p/?LinkId=301960
[Permissions]: http://msdn.microsoft.com/library/windowsazure/jj193161.aspx
[Service-side Authorization]: mobile-services-javascript-backend-service-side-authorization.md
[Use scripts tooauthorize users]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
[동적 스키마]: http://go.microsoft.com/fwlink/p/?LinkId=296271
[How to: access custom parameters]: /develop/mobile/how-to-guides/work-with-server-scripts#access-headers
[Create a table]: http://msdn.microsoft.com/library/windowsazure/jj193162.aspx
[NSDictionary object]: http://go.microsoft.com/fwlink/p/?LinkId=301965
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[CLI toomanage Mobile Services tables]: /cli/azure/get-started-with-az-cli2
[Conflict-Handler]: mobile-services-ios-handling-conflicts-offline-data.md#add-conflict-handling

[패브릭 대시보드]: https://www.fabric.io/home
[iOS-시작에 대 한 패브릭]: https://docs.fabric.io/ios/fabric/getting-started.html
[1]: https://github.com/Azure/azure-mobile-apps-ios-client/blob/master/README.md#ios-client-sdk
[2]: http://azure.github.io/azure-mobile-apps-ios-client/
[3]: https://msdn.microsoft.com/library/azure/dn495101.aspx
[4]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags
[5]: http://azure.github.io/azure-mobile-services/iOS/v3/Classes/MSClient.html#//api/name/invokeAPI:data:HTTPMethod:parameters:headers:completion:
[6]: https://github.com/Azure/azure-mobile-services/blob/master/sdk/iOS/src/MSError.h
[7]: app-service-mobile-how-to-configure-active-directory-authentication.md
[8]: ../active-directory/active-directory-devquickstarts-ios.md
[9]: app-service-mobile-how-to-configure-facebook-authentication.md
[10]: https://developers.facebook.com/docs/ios/getting-started
