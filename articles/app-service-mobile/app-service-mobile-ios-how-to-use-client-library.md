---
title: "Azure 모바일 앱에 iOS SDK를 사용하는 방법"
description: "Azure 모바일 앱에 iOS SDK를 사용하는 방법"
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
ms.openlocfilehash: 65817208e1b26fb5f9eb56d164f48b44d57dce56
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-ios-client-library-for-azure-mobile-apps"></a><span data-ttu-id="d87c4-103">Azure 모바일 앱용 iOS 클라이언트 라이브러리를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="d87c4-103">How to Use iOS Client Library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="d87c4-104">이 가이드에서는 최신 [Azure Mobile Apps iOS SDK][1]를 사용하여 일반적인 시나리오를 수행하는 방법을 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-104">This guide teaches you to perform common scenarios using the latest [Azure Mobile Apps iOS SDK][1].</span></span> <span data-ttu-id="d87c4-105">Azure 모바일 앱을 처음 접하는 경우 먼저 [Azure 모바일 앱 빠른 시작] 을 완료하여 백 엔드를 만들고, 테이블을 만든 다음 미리 빌드된 iOS Xcode 프로젝트를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-105">If you are new to Azure Mobile Apps, first complete [Azure Mobile Apps Quick Start] to create a backend, create a table, and download a pre-built iOS Xcode project.</span></span> <span data-ttu-id="d87c4-106">이 가이드에서는 클라이언트 쪽 iOS SDK에 초점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-106">In this guide, we focus on the client-side iOS SDK.</span></span> <span data-ttu-id="d87c4-107">백 엔드의 서버 쪽 SDK에 대한 자세한 내용은 서버 SDK 사용 방법을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d87c4-107">To learn more about the server-side SDK for the backend, see the Server SDK HOWTOs.</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="d87c4-108">참조 설명서</span><span class="sxs-lookup"><span data-stu-id="d87c4-108">Reference documentation</span></span>
<span data-ttu-id="d87c4-109">iOS 클라이언트 SDK에 대한 참조 설명서는 [Azure Mobile Apps iOS 클라이언트 참조][2](영문)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-109">The reference documentation for the iOS client SDK is located here: [Azure Mobile Apps iOS Client Reference][2].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="d87c4-110">지원되는 플랫폼</span><span class="sxs-lookup"><span data-stu-id="d87c4-110">Supported Platforms</span></span>
<span data-ttu-id="d87c4-111">iOS SDK는 iOS 버전 8.0 이상을 위한 Objective-C 프로젝트, Swift 2.2 프로젝트 및 Swift 2.3 프로젝트를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-111">The iOS SDK supports Objective-C projects, Swift 2.2 projects, and Swift 2.3 projects for iOS versions 8.0 or later.</span></span>

<span data-ttu-id="d87c4-112">"서버-흐름" 인증은 표시된 UI에 웹 보기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-112">The "server-flow" authentication uses a WebView for the presented UI.</span></span>  <span data-ttu-id="d87c4-113">장치가 웹 보기 UI를 표시할 수 없는 경우 제품 범위를 벗어나는 다른 인증 방법이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-113">If the device is not able to present a WebView UI, then another method of authentication is required that is outside the scope of the product.</span></span>  
<span data-ttu-id="d87c4-114">따라서 이 SDK는 Watch 유형 또는 그와 비슷하게 제한된 장치에는 적합하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-114">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span></span>

## <span data-ttu-id="d87c4-115"><a name="Setup"></a>설정 및 필수 조건</span><span class="sxs-lookup"><span data-stu-id="d87c4-115"><a name="Setup"></a>Setup and Prerequisites</span></span>
<span data-ttu-id="d87c4-116">이 가이드에서는 테이블과 함께 백 엔드를 만들었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-116">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="d87c4-117">이 가이드에서는 해당 테이블에 이러한 자습서의 테이블과 동일한 스키마가 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-117">This guide assumes that the table has the same schema as the tables in those tutorials.</span></span> <span data-ttu-id="d87c4-118">또한 이 가이드에서는 코드에서 `MicrosoftAzureMobile.framework`를 참조하고 `MicrosoftAzureMobile/MicrosoftAzureMobile.h`를 가져온다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-118">This guide also assumes that in your code, you reference `MicrosoftAzureMobile.framework` and import `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.</span></span>

## <span data-ttu-id="d87c4-119"><a name="create-client"></a>방법: 클라이언트 만들기</span><span class="sxs-lookup"><span data-stu-id="d87c4-119"><a name="create-client"></a>How to: Create Client</span></span>
<span data-ttu-id="d87c4-120">프로젝트에서 Azure 모바일 앱 백 엔드에 액세스하려면 `MSClient`를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-120">To access an Azure Mobile Apps backend in your project, create an `MSClient`.</span></span> <span data-ttu-id="d87c4-121">`AppUrl` 을 앱 URL로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-121">Replace `AppUrl` with the app URL.</span></span> <span data-ttu-id="d87c4-122">`gatewayURLString` 및 `applicationKey`는 비워둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-122">You may leave `gatewayURLString` and `applicationKey` empty.</span></span> <span data-ttu-id="d87c4-123">인증에 대한 게이트웨이를 설정하는 경우 `gatewayURLString` 을 게이트웨이 URL로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-123">If you set up a gateway for authentication, populate `gatewayURLString` with the gateway URL.</span></span>

<span data-ttu-id="d87c4-124">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-124">**Objective-C**:</span></span>

```
MSClient *client = [MSClient clientWithApplicationURLString:@"AppUrl"];
```

<span data-ttu-id="d87c4-125">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-125">**Swift**:</span></span>

```
let client = MSClient(applicationURLString: "AppUrl")
```


## <span data-ttu-id="d87c4-126"><a name="table-reference"></a>방법: 테이블 참조 만들기</span><span class="sxs-lookup"><span data-stu-id="d87c4-126"><a name="table-reference"></a>How to: Create Table Reference</span></span>
<span data-ttu-id="d87c4-127">데이터에 액세스하거나 데이터를 업데이트하려면 백 엔드 테이블에 대한 참조를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-127">To access or update data, create a reference to the backend table.</span></span> <span data-ttu-id="d87c4-128">`TodoItem` 을 테이블의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-128">Replace `TodoItem` with the name of your table</span></span>

<span data-ttu-id="d87c4-129">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-129">**Objective-C**:</span></span>

```
MSTable *table = [client tableWithName:@"TodoItem"];
```

<span data-ttu-id="d87c4-130">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-130">**Swift**:</span></span>

```
let table = client.tableWithName("TodoItem")
```


## <span data-ttu-id="d87c4-131"><a name="querying"></a>방법: 데이터 쿼리</span><span class="sxs-lookup"><span data-stu-id="d87c4-131"><a name="querying"></a>How to: Query Data</span></span>
<span data-ttu-id="d87c4-132">데이터베이스 쿼리를 만들려면 `MSTable` 개체를 쿼리합입니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-132">To create a database query, query the `MSTable` object.</span></span> <span data-ttu-id="d87c4-133">다음 쿼리는 `TodoItem` 의 모든 항목을 가져오며 각 항목의 텍스트를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-133">The following query gets all the items in `TodoItem` and logs the text of each item.</span></span>

<span data-ttu-id="d87c4-134">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-134">**Objective-C**:</span></span>

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

<span data-ttu-id="d87c4-135">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-135">**Swift**:</span></span>

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

## <span data-ttu-id="d87c4-136"><a name="filtering"></a>방법: 반환된 데이터 필터링</span><span class="sxs-lookup"><span data-stu-id="d87c4-136"><a name="filtering"></a>How to: Filter Returned Data</span></span>
<span data-ttu-id="d87c4-137">결과를 필터링하는 데 사용할 수 있는 많은 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-137">To filter results, there are many available options.</span></span>

<span data-ttu-id="d87c4-138">조건자를 사용하여 필터링하려면 `NSPredicate` 및 `readWithPredicate`을(를) 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-138">To filter using a predicate, use an `NSPredicate` and `readWithPredicate`.</span></span> <span data-ttu-id="d87c4-139">다음은 반환된 데이터를 필터링하여 불완전한 할 일 항목만 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-139">The following filters returned data to find only incomplete Todo items.</span></span>

<span data-ttu-id="d87c4-140">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-140">**Objective-C**:</span></span>

```
// Create a predicate that finds items where complete is false
NSPredicate * predicate = [NSPredicate predicateWithFormat:@"complete == NO"];
// Query the TodoItem table
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

<span data-ttu-id="d87c4-141">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-141">**Swift**:</span></span>

```
// Create a predicate that finds items where complete is false
let predicate =  NSPredicate(format: "complete == NO")
// Query the TodoItem table
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

## <span data-ttu-id="d87c4-142"><a name="query-object"></a>방법: MSQuery 사용</span><span class="sxs-lookup"><span data-stu-id="d87c4-142"><a name="query-object"></a>How to: Use MSQuery</span></span>
<span data-ttu-id="d87c4-143">복잡한 쿼리(정렬 및 페이징 포함)를 수행하려면 직접 또는 조건자를 사용하여 `MSQuery` 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-143">To perform a complex query (including sorting and paging), create an `MSQuery` object, directly or by using a predicate:</span></span>

<span data-ttu-id="d87c4-144">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-144">**Objective-C**:</span></span>

```
MSQuery *query = [table query];
MSQuery *query = [table queryWithPredicate: [NSPredicate predicateWithFormat:@"complete == NO"]];
```

<span data-ttu-id="d87c4-145">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-145">**Swift**:</span></span>

```
let query = table.query()
let query = table.queryWithPredicate(NSPredicate(format: "complete == NO"))
```

<span data-ttu-id="d87c4-146">`MSQuery` 를 사용하여 여러 쿼리 동작을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-146">`MSQuery` lets you control several query behaviors.</span></span>

* <span data-ttu-id="d87c4-147">결과의 순서 지정</span><span class="sxs-lookup"><span data-stu-id="d87c4-147">Specify order of results</span></span>
* <span data-ttu-id="d87c4-148">반환할 필드 제한</span><span class="sxs-lookup"><span data-stu-id="d87c4-148">Limit which fields to return</span></span>
* <span data-ttu-id="d87c4-149">반환할 레코드 수 제한</span><span class="sxs-lookup"><span data-stu-id="d87c4-149">Limit how many records to return</span></span>
* <span data-ttu-id="d87c4-150">응답의 총 수 지정</span><span class="sxs-lookup"><span data-stu-id="d87c4-150">Specify total count in response</span></span>
* <span data-ttu-id="d87c4-151">요청에서 사용자 지정 쿼리 문자열 매개 변수 지정</span><span class="sxs-lookup"><span data-stu-id="d87c4-151">Specify custom query string parameters in request</span></span>
* <span data-ttu-id="d87c4-152">추가 함수 적용</span><span class="sxs-lookup"><span data-stu-id="d87c4-152">Apply additional functions</span></span>

<span data-ttu-id="d87c4-153">개체에 `readWithCompletion`을 호출하여 `MSQuery` 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-153">Execute an `MSQuery` query by calling `readWithCompletion` on the object.</span></span>

## <span data-ttu-id="d87c4-154"><a name="sorting"></a>방법: MSQuery를 사용하여 데이터 정렬</span><span class="sxs-lookup"><span data-stu-id="d87c4-154"><a name="sorting"></a>How to: Sort Data with MSQuery</span></span>
<span data-ttu-id="d87c4-155">결과를 정렬하기 위해 예제를 살펴봅시다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-155">To sort results, let's look at an example.</span></span> <span data-ttu-id="d87c4-156">'text' 필드를 기준으로 오름차순으로 정렬한 다음 'complete' 필드를 기준으로 내림차순으로 정렬하려면 다음과 같이 `MSQuery` 를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-156">To sort by field 'text' ascending, then by 'complete' descending, invoke `MSQuery` like so:</span></span>

<span data-ttu-id="d87c4-157">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-157">**Objective-C**:</span></span>

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

<span data-ttu-id="d87c4-158">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-158">**Swift**:</span></span>

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


## <span data-ttu-id="d87c4-159"><a name="selecting"></a><a name="parameters"></a>방법: MSQuery를 사용하여 필드 제한 및 쿼리 문자열 매개 변수 확장</span><span class="sxs-lookup"><span data-stu-id="d87c4-159"><a name="selecting"></a><a name="parameters"></a>How to: Limit Fields and Expand Query String Parameters with MSQuery</span></span>
<span data-ttu-id="d87c4-160">쿼리에서 반환되는 필드를 제한하려면 **selectFields** 속성에서 필드의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-160">To limit fields to be returned in a query, specify the names of the fields in the **selectFields** property.</span></span> <span data-ttu-id="d87c4-161">이 예는 텍스트 필드와 완료된 필드만 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-161">This example returns only the text and completed fields:</span></span>

<span data-ttu-id="d87c4-162">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-162">**Objective-C**:</span></span>

```
query.selectFields = @[@"text", @"complete"];
```

<span data-ttu-id="d87c4-163">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-163">**Swift**:</span></span>

```
query.selectFields = ["text", "complete"]
```

<span data-ttu-id="d87c4-164">서버 요청에서 추가 쿼리 문자열 매개 변수를 포함하려면(예: 사용자 지정 서버 쪽 스크립트가 이를 사용하기 때문) 다음과 같이 `query.parameters` 을(를) 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-164">To include additional query string parameters in the server request (for example, because a custom server-side script uses them), populate `query.parameters` like so:</span></span>

<span data-ttu-id="d87c4-165">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-165">**Objective-C**:</span></span>

```
query.parameters = @{
    @"myKey1" : @"value1",
    @"myKey2" : @"value2",
};
```

<span data-ttu-id="d87c4-166">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-166">**Swift**:</span></span>

```
query.parameters = ["myKey1": "value1", "myKey2": "value2"]
```

## <span data-ttu-id="d87c4-167"><a name="paging"></a>방법: 페이지 크기 구성</span><span class="sxs-lookup"><span data-stu-id="d87c4-167"><a name="paging"></a>How to: Configure Page Size</span></span>
<span data-ttu-id="d87c4-168">Azure Mobile Apps의 페이지 크기는 백 엔드 테이블에서 한 번에 가져오는 레코드의 수를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-168">With Azure Mobile Apps, the page size controls the number of records that are pulled at a time from the backend tables.</span></span> <span data-ttu-id="d87c4-169">`pull` 데이터에 대한 호출은 끌어올 레코드가 더 이상 없을 때까지 이 페이지 크기에 따라 데이터를 일괄 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-169">A call to `pull` data would then batch up data, based on this page size, until there are no more records to pull.</span></span>

<span data-ttu-id="d87c4-170">아래와 같이 **MSPullSettings**를 사용하여 페이지 크기를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-170">It's possible to configure a page size using **MSPullSettings** as shown below.</span></span> <span data-ttu-id="d87c4-171">기본 페이지 크기는 50이고 아래 예제에서는 3으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-171">The default page size is 50, and the example below changes it to 3.</span></span>

<span data-ttu-id="d87c4-172">성능상의 이유로 다른 페이지 크기를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-172">You could configure a different page size for performance reasons.</span></span> <span data-ttu-id="d87c4-173">작은 데이터 레코드 수가 많은 경우 페이지 크기가 크면 서버 왕복 횟수를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-173">If you have a large number of small data records, a high page size reduces the number of server round-trips.</span></span>

<span data-ttu-id="d87c4-174">이 설정은 클라이언트 쪽의 페이지 크기만 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-174">This setting controls only the page size on the client side.</span></span> <span data-ttu-id="d87c4-175">클라이언트가 Mobile Apps 백 엔드에서 지원하는 것보다 큰 페이지 크기를 지원하도록 요청하는 경우 백 엔드에서 지원하도록 구성된 최대 페이지 크기로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-175">If the client asks for a larger page size than the Mobile Apps backend supports, the page size is capped at the maximum the backend is configured to support.</span></span>

<span data-ttu-id="d87c4-176">또한 이 설정은 *바이트 크기*가 아니라 데이터 레코드의 *수*입니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-176">This setting is also the *number* of data records, not the *byte size*.</span></span>

<span data-ttu-id="d87c4-177">클라이언트 페이지 크기를 늘리면 서버에서 페이지 크기도 늘려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-177">If you increase the client page size, you should also increase the page size on the server.</span></span> <span data-ttu-id="d87c4-178">이 작업을 수행하는 단계는 ["방법: 테이블 페이징 크기 조정"](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d87c4-178">See ["How to: Adjust the table paging size"](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for the steps to do this.</span></span>

<span data-ttu-id="d87c4-179">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-179">**Objective-C**:</span></span>

```
  MSPullSettings *pullSettings = [[MSPullSettings alloc] initWithPageSize:3];
  [table  pullWithQuery:query queryId:@nil settings:pullSettings
                        completion:^(NSError * _Nullable error) {
                               if(error) {
                    NSLog(@"ERROR %@", error);
                }
                           }];
```


<span data-ttu-id="d87c4-180">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-180">**Swift**:</span></span>

```
let pullSettings = MSPullSettings(pageSize: 3)
table.pullWithQuery(query, queryId:nil, settings: pullSettings) { (error) in
    if let err = error {
        print("ERROR ", err)
    }
}
```

## <span data-ttu-id="d87c4-181"><a name="inserting"></a>방법: 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="d87c4-181"><a name="inserting"></a>How to: Insert Data</span></span>
<span data-ttu-id="d87c4-182">새 테이블 행을 삽입하려면 `NSDictionary`를 만들고 `table insert`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-182">To insert a new table row, create a `NSDictionary` and invoke `table insert`.</span></span> <span data-ttu-id="d87c4-183">[동적 스키마]를 사용하는 경우 Azure App Service 모바일 백 엔드는 `NSDictionary`에 따라 새 열을 자동으로 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-183">If [Dynamic Schema] is enabled, the Azure App Service mobile backend automatically generates new columns based on the `NSDictionary`.</span></span>

<span data-ttu-id="d87c4-184">`id` 이(가) 제공되지 않는 경우 백 엔드는 고유한 새 ID를 자동으로 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-184">If `id` is not provided, the backend automatically generates a new unique ID.</span></span> <span data-ttu-id="d87c4-185">고유한 `id` 을(를) 제공하여 이메일 주소, 사용자 이름을 사용하거나 고유한 사용자 지정 값을 ID로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-185">Provide your own `id` to use email addresses, usernames, or your own custom values as ID.</span></span> <span data-ttu-id="d87c4-186">고유한 ID를 제공하면 조인 및 비즈니스 지향적인 데이터베이스 논리가 쉬을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-186">Providing your own ID may ease joins and business-oriented database logic.</span></span>

<span data-ttu-id="d87c4-187">`result` 에는 삽입된 새 항목이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-187">The `result` contains the new item that was inserted.</span></span> <span data-ttu-id="d87c4-188">서버 논리에 따라, 서버에 전달된 데이터와 비교했을 때 추가된 또는 수정된 데이터가 있을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-188">Depending on your server logic, it may have additional or modified data compared to what was passed to the server.</span></span>

<span data-ttu-id="d87c4-189">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-189">**Objective-C**:</span></span>

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

<span data-ttu-id="d87c4-190">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-190">**Swift**:</span></span>

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

## <span data-ttu-id="d87c4-191"><a name="modifying"></a>방법: 데이터 수정</span><span class="sxs-lookup"><span data-stu-id="d87c4-191"><a name="modifying"></a>How to: Modify Data</span></span>
<span data-ttu-id="d87c4-192">기존 행을 업데이트하려면 항목을 수정하고 `update`을(를) 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-192">To update an existing row, modify an item and call `update`:</span></span>

<span data-ttu-id="d87c4-193">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-193">**Objective-C**:</span></span>

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

<span data-ttu-id="d87c4-194">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-194">**Swift**:</span></span>

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

<span data-ttu-id="d87c4-195">또는 행 ID와 업데이트된 필드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-195">Alternatively, supply the row ID and the updated field:</span></span>

<span data-ttu-id="d87c4-196">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-196">**Objective-C**:</span></span>

```
[table update:@{@"id":@"custom-id", @"text":"my EDITED item"} completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="d87c4-197">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-197">**Swift**:</span></span>

```
table.update(["id": "custom-id", "text": "my EDITED item"]) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

<span data-ttu-id="d87c4-198">최소한 업데이트할 때에는 `id` 특성이 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-198">At minimum, the `id` attribute must be set when making updates.</span></span>

## <span data-ttu-id="d87c4-199"><a name="deleting"></a>방법: Blob 삭제</span><span class="sxs-lookup"><span data-stu-id="d87c4-199"><a name="deleting"></a>How to: Delete Data</span></span>
<span data-ttu-id="d87c4-200">항목을 삭제하려면 항목과 함께 `delete` 을(를) 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-200">To delete an item, invoke `delete` with the item:</span></span>

<span data-ttu-id="d87c4-201">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-201">**Objective-C**:</span></span>

```
[table delete:item completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

<span data-ttu-id="d87c4-202">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-202">**Swift**:</span></span>

```
table.delete(newItem as [NSObject: AnyObject]) { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

<span data-ttu-id="d87c4-203">또는 행 ID를 제공하여 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-203">Alternatively, delete by providing a row ID:</span></span>

<span data-ttu-id="d87c4-204">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-204">**Objective-C**:</span></span>

```
[table deleteWithId:@"37BBF396-11F0-4B39-85C8-B319C729AF6D" completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

<span data-ttu-id="d87c4-205">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-205">**Swift**:</span></span>

```
table.deleteWithId("37BBF396-11F0-4B39-85C8-B319C729AF6D") { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

<span data-ttu-id="d87c4-206">최소한 삭제할 때에는 `id` 특성이 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-206">At minimum, the `id` attribute must be set when making deletes.</span></span>

## <span data-ttu-id="d87c4-207"><a name="customapi"></a>방법: 사용자 지정 API 호출</span><span class="sxs-lookup"><span data-stu-id="d87c4-207"><a name="customapi"></a>How to: Call Custom API</span></span>
<span data-ttu-id="d87c4-208">사용자 지정 API를 사용하여 백 엔드 기능을 노출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-208">With a custom API, you can expose any backend functionality.</span></span> <span data-ttu-id="d87c4-209">테이블 작업에 매핑할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-209">It doesn't have to map to a table operation.</span></span> <span data-ttu-id="d87c4-210">더 효율적으로 메시징을 제어할 수 있으며 헤더의 읽기/설정 및 응답의 본문 형식을 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-210">Not only do you gain more control over messaging, you can even read/set headers and change the response body format.</span></span> <span data-ttu-id="d87c4-211">백 엔드에서 사용자 지정 API를 만드는 방법에 대한 자세한 내용은 [사용자 지정 API](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)</span><span class="sxs-lookup"><span data-stu-id="d87c4-211">To learn how to create a custom API on the backend, read [Custom APIs](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)</span></span>

<span data-ttu-id="d87c4-212">사용자 지정 API를 호출하려면 `MSClient.invokeAPI`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-212">To call a custom API, call `MSClient.invokeAPI`.</span></span> <span data-ttu-id="d87c4-213">요청 및 응답 콘텐츠는 JSON으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-213">The request and response content are treated as JSON.</span></span> <span data-ttu-id="d87c4-214">다른 미디어 유형을 사용하려면 [의 다른 오버로드를 사용`invokeAPI`][5]합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-214">To use other media types, [use the other overload of `invokeAPI`][5].</span></span>  <span data-ttu-id="d87c4-215">`POST` 요청 대신 `GET` 요청을 하려면 GET 요청에는 메시지의 본문이 없기 때문에 매개 변수를 `HTTPMethod`에서 `"GET"` 및 `body`에서 `nil`으로 설정합니다. 사용자 지정 API가 다른 HTTP 동사를 지원하는 경우 `HTTPMethod`을(를) 적절하게 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-215">To make a `GET` request instead of a `POST` request, set parameter `HTTPMethod` to `"GET"` and parameter `body` to `nil` (since GET requests do not have message bodies.) If your custom API supports other HTTP verbs, change `HTTPMethod` appropriately.</span></span>

<span data-ttu-id="d87c4-216">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-216">**Objective-C**:</span></span>

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

<span data-ttu-id="d87c4-217">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-217">**Swift**:</span></span>

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

## <span data-ttu-id="d87c4-218"><a name="templates"></a>방법: 플랫폼 간 알림을 보내기 위해 푸시 템플릿 등록</span><span class="sxs-lookup"><span data-stu-id="d87c4-218"><a name="templates"></a>How to: Register push templates to send cross-platform notifications</span></span>
<span data-ttu-id="d87c4-219">템플릿을 등록하려면 클라이언트 앱에서 **client.push registerDeviceToken** 메서드를 사용하여 템플릿을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-219">To register templates, pass templates with your **client.push registerDeviceToken** method in your client app.</span></span>

<span data-ttu-id="d87c4-220">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-220">**Objective-C**:</span></span>

```
[client.push registerDeviceToken:deviceToken template:iOSTemplate completion:^(NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    }
}];
```

<span data-ttu-id="d87c4-221">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-221">**Swift**:</span></span>

```
    client.push?.registerDeviceToken(NSData(), template: iOSTemplate, completion: { (error) in
        if let err = error {
            print("ERROR ", err)
        }
    })
```

<span data-ttu-id="d87c4-222">템플릿은 NSDictionary 형식이며 다음 형식으로 여러 템플릿을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-222">Your templates are of type NSDictionary and can contain multiple templates in the following format:</span></span>

<span data-ttu-id="d87c4-223">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-223">**Objective-C**:</span></span>

```
NSDictionary *iOSTemplate = @{ @"templateName": @{ @"body": @{ @"aps": @{ @"alert": @"$(message)" } } } };
```

<span data-ttu-id="d87c4-224">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-224">**Swift**:</span></span>

```
let iOSTemplate = ["templateName": ["body": ["aps": ["alert": "$(message)"]]]]
```

<span data-ttu-id="d87c4-225">보안을 위해 요청에서 모든 태그가 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-225">All tags are stripped from the request for security.</span></span>  <span data-ttu-id="d87c4-226">설치에 태그를 추가하거나 설치 내에 템플릿을 추가하려면 [Azure Mobile Apps용 .NET 백 엔드 서버 SDK 사용][4]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d87c4-226">To add tags to installations or templates within installations, see [Work with the .NET backend server SDK for Azure Mobile Apps][4].</span></span>  <span data-ttu-id="d87c4-227">이러한 등록된 템플릿을 사용하여 알림을 보내려면 [Notification Hubs API][3]로 작업하세요.</span><span class="sxs-lookup"><span data-stu-id="d87c4-227">To send notifications using these registered templates, work with [Notification Hubs APIs][3].</span></span>

## <span data-ttu-id="d87c4-228"><a name="errors"></a>방법: 오류 처리</span><span class="sxs-lookup"><span data-stu-id="d87c4-228"><a name="errors"></a>How to: Handle Errors</span></span>
<span data-ttu-id="d87c4-229">Azure App Service 모바일 백 엔드를 호출할 때 완료 블록에 `NSError` 매개 변수가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-229">When you call an Azure App Service mobile backend, the completion block contains an `NSError` parameter.</span></span> <span data-ttu-id="d87c4-230">오류가 발생하면 이 매개 변수는 null이 아닌 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-230">When an error occurs, this parameter is non-nil.</span></span> <span data-ttu-id="d87c4-231">앞의 코드 조각에서 보여준 것처럼, 코드에서 이 매개 변수를 확인하고 필요한 경우 오류를 처리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-231">In your code, you should check this parameter and handle the error as needed, as demonstrated in the preceding code snippets.</span></span>

<span data-ttu-id="d87c4-232">[`<WindowsAzureMobileServices/MSError.h>`][6] 파일은 `MSErrorResponseKey`, `MSErrorRequestKey` 및 `MSErrorServerItemKey` 상수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-232">The file [`<WindowsAzureMobileServices/MSError.h>`][6] defines the constants `MSErrorResponseKey`, `MSErrorRequestKey`, and `MSErrorServerItemKey`.</span></span> <span data-ttu-id="d87c4-233">오류와 관련된 데이터를 더 가져오는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-233">To get more data related to the error:</span></span>

<span data-ttu-id="d87c4-234">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-234">**Objective-C**:</span></span>

```
NSDictionary *serverItem = [error.userInfo objectForKey:MSErrorServerItemKey];
```

<span data-ttu-id="d87c4-235">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-235">**Swift**:</span></span>

```
let serverItem = error.userInfo[MSErrorServerItemKey]
```

<span data-ttu-id="d87c4-236">또한 이 파일은 각 오류 코드에 대한 상수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-236">In addition, the file defines constants for each error code:</span></span>

<span data-ttu-id="d87c4-237">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-237">**Objective-C**:</span></span>

```
if (error.code == MSErrorPreconditionFailed) {
```

<span data-ttu-id="d87c4-238">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-238">**Swift**:</span></span>

```
if (error.code == MSErrorPreconditionFailed) {
```

## <span data-ttu-id="d87c4-239"><a name="adal"></a>방법: Active Directory 인증 라이브러리를 사용하여 사용자 인증</span><span class="sxs-lookup"><span data-stu-id="d87c4-239"><a name="adal"></a>How to: Authenticate users with the Active Directory Authentication Library</span></span>
<span data-ttu-id="d87c4-240">Azure Active Directory를 사용하여 응용 프로그램에 사용자가 로그인하려면 Active Directory 인증 라이브러리(ADAL)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-240">You can use the Active Directory Authentication Library (ADAL) to sign users into your application using Azure Active Directory.</span></span> <span data-ttu-id="d87c4-241">ID 공급자 SDK를 사용하는 클라이언트 흐름 인증이 `loginWithProvider:completion:` 메서드보다 선호도가 높습니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-241">Client flow authentication using an identity provider SDK is preferable to using the `loginWithProvider:completion:` method.</span></span>  <span data-ttu-id="d87c4-242">클라이언트 흐름 인증은 UX 느낌을 그대로 제공하고 추가 사용자 지정을 허용하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-242">Client flow authentication provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="d87c4-243">[Active Directory 로그인에 App Service를 구성하는 방법][7] 자습서를 수행하여 AAD 로그인에 모바일 앱 백 엔드를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-243">Configure your mobile app backend for AAD sign-in by following the [How to configure App Service for Active Directory login][7] tutorial.</span></span> <span data-ttu-id="d87c4-244">네이티브 클라이언트 응용 프로그램을 등록하는 선택적 단계를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-244">Make sure to complete the optional step of registering a native client application.</span></span> <span data-ttu-id="d87c4-245">iOS의 경우 권장하는 리디렉션 URI는 `<app-scheme>://<bundle-id>` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-245">For iOS, we recommend that the redirect URI is of the form `<app-scheme>://<bundle-id>`.</span></span> <span data-ttu-id="d87c4-246">자세한 내용은 [ADAL iOS 빠른 시작][8]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d87c4-246">For more information, see the [ADAL iOS quickstart][8].</span></span>
2. <span data-ttu-id="d87c4-247">Cocoapods를 사용하여 ADAL을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-247">Install ADAL using Cocoapods.</span></span> <span data-ttu-id="d87c4-248">다음 정의를 포함하도록 Podfile을 편집합니다. 이때 **YOUR-PROJECT**를 Xcode 프로젝트의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-248">Edit your Podfile to include the following definition, replacing **YOUR-PROJECT** with the name of your Xcode project:</span></span>

        source 'https://github.com/CocoaPods/Specs.git'
        link_with ['YOUR-PROJECT']
        xcodeproj 'YOUR-PROJECT'

   <span data-ttu-id="d87c4-249">및 Pod:</span><span class="sxs-lookup"><span data-stu-id="d87c4-249">and the Pod:</span></span>

        pod 'ADALiOS'
3. <span data-ttu-id="d87c4-250">터미널을 사용하여 프로젝트를 포함하는 디렉터리에서 `pod install`을 실행한 다음 생성된 Xcode 작업 영역(프로젝트 아님)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-250">Using the Terminal, run `pod install` from the directory containing your project, and then open the generated Xcode workspace (not the project).</span></span>
4. <span data-ttu-id="d87c4-251">사용하는 언어에 따라 응용 프로그램에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-251">Add the following code to your application, according to the language you are using.</span></span> <span data-ttu-id="d87c4-252">각 코드에서 다음과 같이 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-252">In each, make these replacements:</span></span>

   * <span data-ttu-id="d87c4-253">**INSERT-AUTHORITY-HERE** 를 응용 프로그램이 프로비전된 테넌트의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-253">Replace **INSERT-AUTHORITY-HERE** with the name of the tenant in which you provisioned your application.</span></span> <span data-ttu-id="d87c4-254">형식은 https://login.microsoftonline.com/contoso.onmicrosoft.com이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-254">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com.</span></span> <span data-ttu-id="d87c4-255">이 값은 [Azure 클래식 포털]의 Azure Active Directory에 있는 도메인 탭에서 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-255">This value can be copied from the Domain tab in your Azure Active Directory in the [Azure classic portal].</span></span>
   * <span data-ttu-id="d87c4-256">**INSERT-RESOURCE-ID-HERE** 를 모바일 앱 백 엔드에 대한 클라이언트 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-256">Replace **INSERT-RESOURCE-ID-HERE** with the client ID for your mobile app backend.</span></span> <span data-ttu-id="d87c4-257">포털의 Azure **Active Directory 설정**에 있는 **고급** 탭에서 클라이언트 ID를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-257">You can obtain the client ID from the **Advanced** tab under **Azure Active Directory Settings** in the portal.</span></span>
   * <span data-ttu-id="d87c4-258">**INSERT-CLIENT-ID-HERE** 를 네이티브 클라이언트 응용 프로그램에서 복사한 클라이언트 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-258">Replace **INSERT-CLIENT-ID-HERE** with the client ID you copied from the native client application.</span></span>
   * <span data-ttu-id="d87c4-259">HTTPS 체계를 사용하여 **INSERT-REDIRECT-URI-HERE** 를 사이트의 */.auth/login/done* 끝점으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-259">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using the HTTPS scheme.</span></span> <span data-ttu-id="d87c4-260">이 값은 *https://contoso.azurewebsites.net/.auth/login/done*과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-260">This value should be similar to *https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

<span data-ttu-id="d87c4-261">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-261">**Objective-C**:</span></span>

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


<span data-ttu-id="d87c4-262">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-262">**Swift**:</span></span>

    // add the following imports to your bridging header:
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

## <span data-ttu-id="d87c4-263"><a name="facebook-sdk"></a>방법: iOS용 Facebook SDK를 사용하여 사용자 인증</span><span class="sxs-lookup"><span data-stu-id="d87c4-263"><a name="facebook-sdk"></a>How to: Authenticate users with the Facebook SDK for iOS</span></span>
<span data-ttu-id="d87c4-264">Facebook을 사용하여 응용 프로그램에 사용자를 로그인하도록 iOS용 Facebook SDK를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-264">You can use the Facebook SDK for iOS to sign users into your application using Facebook.</span></span>  <span data-ttu-id="d87c4-265">클라이언트 흐름 인증이 `loginWithProvider:completion:` 메서드보다 선호도가 높습니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-265">Using a client flow authentication is preferable to using the `loginWithProvider:completion:` method.</span></span>  <span data-ttu-id="d87c4-266">클라이언트 흐름 인증은 UX 느낌을 그대로 제공하고 추가 사용자 지정을 허용하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-266">The client flow authentication provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="d87c4-267">[Facebook 로그인에 App Service를 구성하는 방법][9] 자습서를 수행하여 Facebook 로그인에 모바일 앱 백 엔드를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-267">Configure your mobile app backend for Facebook sign-in by following the [How to configure App Service for Facebook login][9] tutorial.</span></span>
2. <span data-ttu-id="d87c4-268">[iOS용 Facebook SDK - 시작][10] 설명서에 따라 iOS용 Facebook SDK를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-268">Install the Facebook SDK for iOS by following the [Facebook SDK for iOS - Getting Started][10] documentation.</span></span> <span data-ttu-id="d87c4-269">앱을 만드는 대신 기존 등록에 iOS 플랫폼을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-269">Instead of creating an app, you can add the iOS platform to your existing registration.</span></span>
3. <span data-ttu-id="d87c4-270">Facebook의 설명서는 앱 대리자에서 일부 Objective-C 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-270">Facebook's documentation includes some Objective-C code in the App Delegate.</span></span> <span data-ttu-id="d87c4-271">**Swift**를 사용 중인 경우 AppDelegate.swift에 다음 번역을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-271">If you are using **Swift**, you can use the following translations for AppDelegate.swift:</span></span>

        // Add the following import to your bridging header:
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
4. <span data-ttu-id="d87c4-272">또한 프로젝트에 `FBSDKCoreKit.framework`을 추가하는 것 외에도 같은 방식으로 `FBSDKLoginKit.framework`에 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-272">In addition to adding `FBSDKCoreKit.framework` to your project, also add a reference to `FBSDKLoginKit.framework` in the same way.</span></span>
5. <span data-ttu-id="d87c4-273">사용하는 언어에 따라 응용 프로그램에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-273">Add the following code to your application, according to the language you are using.</span></span>

<span data-ttu-id="d87c4-274">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-274">**Objective-C**:</span></span>

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

<span data-ttu-id="d87c4-275">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-275">**Swift**:</span></span>

    // Add the following imports to your bridging header:
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

## <span data-ttu-id="d87c4-276"><a name="twitter-fabric"></a>방법: iOS용 Twitter Fabric을 사용하여 사용자 인증</span><span class="sxs-lookup"><span data-stu-id="d87c4-276"><a name="twitter-fabric"></a>How to: Authenticate users with Twitter Fabric for iOS</span></span>
<span data-ttu-id="d87c4-277">Twitter를 사용하여 응용 프로그램에 사용자를 로그인하도록 iOS용 Fabric을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-277">You can use Fabric for iOS to sign users into your application using Twitter.</span></span> <span data-ttu-id="d87c4-278">클라이언트 흐름 인증은 UX 느낌을 그대로 제공하고 추가 사용자 지정을 허용하기에 `loginWithProvider:completion:` 메서드보다 선호도가 높습니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-278">Client Flow authentication is preferable to using the `loginWithProvider:completion:` method, as it provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="d87c4-279">다음으로 [Twitter 로그인에 앱 서비스를 구성하는 방법](app-service-mobile-how-to-configure-twitter-authentication.md) 자습서를 수행하여 Twitter 로그인에 모바일 앱 백 엔드를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-279">Configure your mobile app backend for Twitter sign-in by following the [How to configure App Service for Twitter login](app-service-mobile-how-to-configure-twitter-authentication.md) tutorial.</span></span>
2. <span data-ttu-id="d87c4-280">[iOS용 Fabric - 시작] 설명서를 수행하고 TwitterKit를 설정하여 프로젝트에 Fabric을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-280">Add Fabric to your project by following the [Fabric for iOS - Getting Started] documentation and setting up TwitterKit.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d87c4-281">기본적으로 패브릭은 사용자를 위해 Twitter 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-281">By default, Fabric creates a Twitter application for you.</span></span> <span data-ttu-id="d87c4-282">다음 코드 조각을 사용하여 이전에 만든 소비자 키 및 소비자 암호를 등록하면 응용 프로그램을 만들지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-282">You can avoid creating an application by registering the Consumer Key and Consumer Secret you created earlier using the following code snippets.</span></span>    <span data-ttu-id="d87c4-283">또는 [패브릭 대시보드]에 표시되는 값으로 앱 서비스를 제공하는 소비자 키 및 소비자 암호 값을 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-283">Alternatively, you can replace the Consumer Key and Consumer Secret values that you provide to App Service with the values you see in the [Fabric Dashboard].</span></span> <span data-ttu-id="d87c4-284">이 옵션을 선택하면 콜백 URL을 `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`와 같은 자리 표시자 값으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-284">If you choose this option, be sure to set the callback URL to a placeholder value, such as `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.</span></span>
   >
   >

    <span data-ttu-id="d87c4-285">이전에 만든 암호를 사용하도록 선택한 경우 앱 대리자에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-285">If you choose to use the secrets you created earlier, add the following code to your App Delegate:</span></span>

    <span data-ttu-id="d87c4-286">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-286">**Objective-C**:</span></span>

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

    <span data-ttu-id="d87c4-287">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-287">**Swift**:</span></span>

        import Fabric
        import TwitterKit
        // ...
        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            Twitter.sharedInstance().startWithConsumerKey("your_key", consumerSecret: "your_secret")
            Fabric.with([Twitter.self])
            // Add any custom logic here.
            return true
        }
3. <span data-ttu-id="d87c4-288">사용하는 언어에 따라 응용 프로그램에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-288">Add the following code to your application, according to the language you are using.</span></span>

<span data-ttu-id="d87c4-289">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-289">**Objective-C**:</span></span>

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

<span data-ttu-id="d87c4-290">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-290">**Swift**:</span></span>

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

## <span data-ttu-id="d87c4-291"><a name="google-sdk"></a>방법: iOS용 Google 로그인 SDK를 사용하여 사용자 인증</span><span class="sxs-lookup"><span data-stu-id="d87c4-291"><a name="google-sdk"></a>How to: Authenticate users with the Google Sign-In SDK for iOS</span></span>
<span data-ttu-id="d87c4-292">Google 로그인을 사용하여 응용 프로그램에 사용자를 로그인하도록 iOS용 Google 로그인 SDK를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-292">You can use the Google Sign-In SDK for iOS to sign users into your application using a Google account.</span></span>  <span data-ttu-id="d87c4-293">최근에 Google에서 OAuth 보안 정책 변경 소식을 발표했습니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-293">Google recently announced changes to their OAuth security policies.</span></span>  <span data-ttu-id="d87c4-294">정책이 변경됨에 따라 향후에는 Google SDK를 사용해야 할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-294">These policy changes will require the use of the Google SDK in the future.</span></span>

1. <span data-ttu-id="d87c4-295">다음으로 [Google 로그인에 App Service를 구성하는 방법](app-service-mobile-how-to-configure-google-authentication.md) 자습서를 수행하여 Google 로그인에 모바일 앱 백 엔드를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-295">Configure your mobile app backend for Google sign-in by following the [How to configure App Service for Google login](app-service-mobile-how-to-configure-google-authentication.md) tutorial.</span></span>
2. <span data-ttu-id="d87c4-296">[iOS용 Google 로그인 - 통합 시작](https://developers.google.com/identity/sign-in/ios/start-integrating) 설명서에 따라 iOS용 Google SDK를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-296">Install the Google SDK for iOS by following the [Google Sign-In for iOS - Start integrating](https://developers.google.com/identity/sign-in/ios/start-integrating) documentation.</span></span> <span data-ttu-id="d87c4-297">"백 엔드 서버를 사용하여 인증" 섹션은 건너뛰어도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-297">You may skip the "Authenticate with a Backend Server" section.</span></span>
3. <span data-ttu-id="d87c4-298">사용하는 언어에 따라 대리자의 `signIn:didSignInForUser:withError:` 메서드에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-298">Add the following to your delegate's `signIn:didSignInForUser:withError:` method, according to the language you are using.</span></span>

<span data-ttu-id="d87c4-299">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-299">**Objective-C**:</span></span>

        NSDictionary *payload = @{
                                  @"id_token":user.authentication.idToken,
                                  @"authorization_code":user.serverAuthCode
                                  };

        [client loginWithProvider:@"google" token:payload completion:^(MSUser *user, NSError *error) {
            // ...
        }];

<span data-ttu-id="d87c4-300">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-300">**Swift**:</span></span>

        let payload: [String: String] = ["id_token": user.authentication.idToken, "authorization_code": user.serverAuthCode]
        client.loginWithProvider("google", token: payload) { (user, error) in
            // ...
        }

1. <span data-ttu-id="d87c4-301">또한 다음을 앱 대리자의 `application:didFinishLaunchingWithOptions:`에 추가하여 "SERVER_CLIENT_ID"를 1단계에서 App Service를 구성하는 데 사용된 동일한 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-301">Make sure you also add the following to `application:didFinishLaunchingWithOptions:` in your app delegate, replacing "SERVER_CLIENT_ID" with the same ID that you used to configure App Service in step 1.</span></span>

<span data-ttu-id="d87c4-302">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-302">**Objective-C**:</span></span>

         [GIDSignIn sharedInstance].serverClientID = @"SERVER_CLIENT_ID";

 <span data-ttu-id="d87c4-303">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-303">**Swift**:</span></span>

        GIDSignIn.sharedInstance().serverClientID = "SERVER_CLIENT_ID"


1. <span data-ttu-id="d87c4-304">사용하는 언어에 따라 다음 코드를 `GIDSignInUIDelegate` 프로토콜을 구현하는 UIViewController의 응용 프로그램에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-304">Add the following code to your application in a UIViewController that implements the `GIDSignInUIDelegate` protocol, according to the language you are using.</span></span>  <span data-ttu-id="d87c4-305">로그아웃되었다가 다시 로그인되며, 자격 증명을 다시 입력할 필요는 없지만 동의 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-305">You are signed out before being signed in again, and although you don't need to enter your credentials again, you see a consent dialog.</span></span>  <span data-ttu-id="d87c4-306">세션 토큰이 만료된 경우에만 이 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="d87c4-306">Only call this method when the session token has expired.</span></span>

   <span data-ttu-id="d87c4-307">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-307">**Objective-C**:</span></span>

       #import <Google/SignIn.h>
       // ...
       - (void)authenticate
       {
               [GIDSignIn sharedInstance].uiDelegate = self;
               [[GIDSignIn sharedInstance] signOut];
               [[GIDSignIn sharedInstance] signIn];
        }

   <span data-ttu-id="d87c4-308">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="d87c4-308">**Swift**:</span></span>

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
[How to: Create the Mobile Services client]: #create-client
[How to: Create a table reference]: #table-reference
[How to: Query data from a mobile service]: #querying
[Filter returned data]: #filtering
[Sort returned data]: #sorting
[Return data in pages]: #paging
[Select specific columns]: #selecting
[How to: Bind data to the user interface]: #binding
[How to: Insert data into a mobile service]: #inserting
[How to: Modify data in a mobile service]: #modifying
[How to: Authenticate users]: #authentication
[Cache authentication tokens]: #caching-tokens
[How to: Upload images and large files]: #blobs
[How to: Handle errors]: #errors
[How to: Design unit tests]: #unit-testing
[How to: Customize the client]: #customizing
[Customize request headers]: #custom-headers
[Customize data type serialization]: #custom-serialization
[Next Steps]: #next-steps
[How to: Use MSQuery]: #query-object

<!-- Images. -->

<!-- URLs. -->
<span data-ttu-id="d87c4-309">[Azure 모바일 앱 빠른 시작]: app-service-mobile-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="d87c4-309">[Azure Mobile Apps Quick Start]: app-service-mobile-ios-get-started.md</span></span>

[Add Mobile Services to Existing App]: /develop/mobile/tutorials/get-started-data
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Validate and modify data in Mobile Services by using server scripts]: /develop/mobile/tutorials/validate-modify-and-augment-data-ios
[Mobile Services SDK]: https://go.microsoft.com/fwLink/p/?LinkID=266533
[Authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[iOS SDK]: https://developer.apple.com/xcode

[Handling Expired Tokens]: http://go.microsoft.com/fwlink/p/?LinkId=301955
[Live Connect SDK]: http://go.microsoft.com/fwlink/p/?LinkId=301960
[Permissions]: http://msdn.microsoft.com/library/windowsazure/jj193161.aspx
[Service-side Authorization]: mobile-services-javascript-backend-service-side-authorization.md
[Use scripts to authorize users]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
<span data-ttu-id="d87c4-310">[동적 스키마]: http://go.microsoft.com/fwlink/p/?LinkId=296271</span><span class="sxs-lookup"><span data-stu-id="d87c4-310">[Dynamic Schema]: http://go.microsoft.com/fwlink/p/?LinkId=296271</span></span>
[How to: access custom parameters]: /develop/mobile/how-to-guides/work-with-server-scripts#access-headers
[Create a table]: http://msdn.microsoft.com/library/windowsazure/jj193162.aspx
[NSDictionary object]: http://go.microsoft.com/fwlink/p/?LinkId=301965
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[CLI to manage Mobile Services tables]: /cli/azure/get-started-with-az-cli2
[Conflict-Handler]: mobile-services-ios-handling-conflicts-offline-data.md#add-conflict-handling

<span data-ttu-id="d87c4-311">[패브릭 대시보드]: https://www.fabric.io/home</span><span class="sxs-lookup"><span data-stu-id="d87c4-311">[Fabric Dashboard]: https://www.fabric.io/home</span></span>
<span data-ttu-id="d87c4-312">[iOS용 Fabric - 시작]: https://docs.fabric.io/ios/fabric/getting-started.html</span><span class="sxs-lookup"><span data-stu-id="d87c4-312">[Fabric for iOS - Getting Started]: https://docs.fabric.io/ios/fabric/getting-started.html</span></span>
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
