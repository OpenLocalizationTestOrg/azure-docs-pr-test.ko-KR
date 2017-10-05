---
title: "DocumentDB API의 Azure Cosmos DB 전역 배포 자습서 | Microsoft Docs"
description: "DocumentDB API를 사용하여 Azure Cosmos DB 전역 배포를 설정하는 방법에 대해 알아봅니다."
services: cosmos-db
keywords: "전역 배포, DocumentDB"
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: f4d8efe9814bd28bb902567a23b541bc9b5414a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-setup-azure-cosmos-db-global-distribution-using-the-documentdb-api"></a><span data-ttu-id="edb91-104">DocumentDB API를 사용하여 Azure Cosmos DB 전역 배포를 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="edb91-104">How to setup Azure Cosmos DB global distribution using the DocumentDB API</span></span>

<span data-ttu-id="edb91-105">이 문서에서는 Azure Portal을 사용하여 Azure Cosmos DB 전역 배포를 설정한 다음 DocumentDB API를 사용하여 연결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-105">In this article, we show how to use the Azure portal to setup Azure Cosmos DB global distribution and then connect using the DocumentDB API.</span></span>

<span data-ttu-id="edb91-106">이 문서에서 다루는 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="edb91-107">Azure Portal을 사용하여 전역 배포 구성</span><span class="sxs-lookup"><span data-stu-id="edb91-107">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="edb91-108">[DocumentDB API](documentdb-introduction.md)를 사용하여 전역 배포 구성</span><span class="sxs-lookup"><span data-stu-id="edb91-108">Configure global distribution using the [DocumentDB APIs](documentdb-introduction.md)</span></span>

<a id="portal"></a>
[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-to-a-preferred-region-using-the-documentdb-api"></a><span data-ttu-id="edb91-109">DocumentDB API를 사용하여 기본 설정 지역에 연결</span><span class="sxs-lookup"><span data-stu-id="edb91-109">Connecting to a preferred region using the DocumentDB API</span></span>

<span data-ttu-id="edb91-110">[전역 배포](distribute-data-globally.md)를 활용하기 위해 클라이언트 응용 프로그램은 문서 작업을 수행하는 데 사용할 정렬된 기본 지역 목록을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-110">In order to take advantage of [global distribution](distribute-data-globally.md), client applications can specify the ordered preference list of regions to be used to perform document operations.</span></span> <span data-ttu-id="edb91-111">이는 연결 정책을 설정하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-111">This can be done by setting the connection policy.</span></span> <span data-ttu-id="edb91-112">DocumentDB SDK에서 Azure Cosmos DB 계정 구성, 현재 지역 가용성 및 지정된 기본 설정 목록을 기반으로 하여 쓰기 및 읽기 작업을 수행하는 데 가장 적합한 끝점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-112">Based on the Azure Cosmos DB account configuration, current regional availability and the preference list specified, the most optimal endpoint will be chosen by the DocumentDB SDK to perform write and read operations.</span></span>

<span data-ttu-id="edb91-113">이 기본 설정 목록은 DocumentDB SDK를 사용하여 연결을 초기화할 때 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-113">This preference list is specified when initializing a connection using the DocumentDB SDKs.</span></span> <span data-ttu-id="edb91-114">SDK는 Azure 지역의 정렬된 목록인 "PreferredLocations"라는 선택적 매개 변수를 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-114">The SDKs accept an optional parameter "PreferredLocations" that is an ordered list of Azure regions.</span></span>

<span data-ttu-id="edb91-115">SDK는 현재 쓰기 지역에 모든 쓰기를 자동 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-115">The SDK will automatically send all writes to the current write region.</span></span>

<span data-ttu-id="edb91-116">모든 읽기는 PreferredLocations 목록에서 첫 번째 사용 가능한 지역으로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-116">All reads will be sent to the first available region in the PreferredLocations list.</span></span> <span data-ttu-id="edb91-117">요청이 실패하면 클라이언트는 목록의 다음 지역으로 옮겨갑니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-117">If the request fails, the client will fail down the list to the next region, and so on.</span></span>

<span data-ttu-id="edb91-118">SDK는 PreferredLocations에 지정된 지역에서만 읽기를 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-118">The SDKs will only attempt to read from the regions specified in PreferredLocations.</span></span> <span data-ttu-id="edb91-119">따라서 가령 데이터베이스 계정이 3개 지역에서 사용할 수 있지만 클라이언트는 PreferredLocations에 쓰기에 해당하지 않는 지역 중 두 가지만 지정했다면, 장애 조치 시에도 쓰기 지역에서 읽기를 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-119">So, for example, if the Database Account is available in three regions, but the client only specifies two of the non-write regions for PreferredLocations, then no reads will be served out of the write region, even in the case of failover.</span></span>

<span data-ttu-id="edb91-120">응용 프로그램은 두 가지 속성(WirteEndpoint 및 ReadEndpoint)을 확인하여 SDK가 선택한 현재의 쓰기 끝점과 읽기 끝점을 확인할 수 있습니다. SDK 버전 1.8 이상부터 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-120">The application can verify the current write endpoint and read endpoint chosen by the SDK by checking two properties, WriteEndpoint and ReadEndpoint, available in SDK version 1.8 and above.</span></span>

<span data-ttu-id="edb91-121">PreferredLocations 속성이 설정되지 않는다면 모든 요청은 현재 쓰기 지역에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-121">If the PreferredLocations property is not set, all requests will be served from the current write region.</span></span>

## <a name="net-sdk"></a><span data-ttu-id="edb91-122">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="edb91-122">.NET SDK</span></span>
<span data-ttu-id="edb91-123">SDK는 코드 변경 없이 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-123">The SDK can be used without any code changes.</span></span> <span data-ttu-id="edb91-124">이 경우 SDK는 읽기와 쓰기를 현재 쓰기 하위 지역에 자동으로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-124">In this case, the SDK automatically directs both reads and writes to the current write region.</span></span>

<span data-ttu-id="edb91-125">.NET SDK의 1.8 버전 이상에서 DocumentClient 생성자의 ConnectionPolicy 매개 변수는 Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations라는 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-125">In version 1.8 and later of the .NET SDK, the ConnectionPolicy parameter for the DocumentClient constructor has a property called Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="edb91-126">이 속성은 컬렉션 `<string>` 형식이며 지역 이름 목록을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-126">This property is of type Collection `<string>` and should contain a list of region names.</span></span> <span data-ttu-id="edb91-127">문자열 값은 [Azure 지역][regions] 페이지의 지역 이름 열에 따라 서식이 지정되고 첫 글자와 마지막 글자 앞/뒤에 공백이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-127">The string values are formatted per the Region Name column on the [Azure Regions][regions] page, with no spaces before or after the first and last character respectively.</span></span>

<span data-ttu-id="edb91-128">현재 읽기 및 쓰기 끝점은 각각 DocumentClient.WriteEndpoint와 DocumentClient.ReadEndpoint에서 이용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-128">The current write and read endpoints are available in DocumentClient.WriteEndpoint and DocumentClient.ReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="edb91-129">끝점의 URL은 수명이 긴 상수로 간주하지 말아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-129">The URLs for the endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="edb91-130">서비스는 언제든지 이 URL을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-130">The service may update these at any point.</span></span> <span data-ttu-id="edb91-131">SDK가 이런 변경 내용을 자동으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-131">The SDK handles this change automatically.</span></span>
>
>

```csharp
// Getting endpoints from application settings or other configuration location
Uri accountEndPoint = new Uri(Properties.Settings.Default.GlobalDatabaseUri);
string accountKey = Properties.Settings.Default.GlobalDatabaseKey;
  
ConnectionPolicy connectionPolicy = new ConnectionPolicy();

//Setting read region selection preference
connectionPolicy.PreferredLocations.Add(LocationNames.WestUS); // first preference
connectionPolicy.PreferredLocations.Add(LocationNames.EastUS); // second preference
connectionPolicy.PreferredLocations.Add(LocationNames.NorthEurope); // third preference

// initialize connection
DocumentClient docClient = new DocumentClient(
    accountEndPoint,
    accountKey,
    connectionPolicy);

// connect to DocDB
await docClient.OpenAsync().ConfigureAwait(false);
```

## <a name="nodejs-javascript-and-python-sdks"></a><span data-ttu-id="edb91-132">NodeJS, JavaScript 및 Python SDK</span><span class="sxs-lookup"><span data-stu-id="edb91-132">NodeJS, JavaScript, and Python SDKs</span></span>
<span data-ttu-id="edb91-133">SDK는 코드 변경 없이 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-133">The SDK can be used without any code changes.</span></span> <span data-ttu-id="edb91-134">이 경우 SDK는 읽기와 쓰기를 현재 쓰기 지역에 자동으로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-134">In this case, the SDK will automatically direct both reads and writes to the current write region.</span></span>

<span data-ttu-id="edb91-135">각 SDK의 1.8 버전 이상에서 DocumentClient 생성자의 ConnectionPolicy 매개 변수에는 DocumentClient.ConnectionPolicy.PreferredLocations라는 새로운 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-135">In version 1.8 and later of each SDK, the ConnectionPolicy parameter for the DocumentClient constructor a new property called DocumentClient.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="edb91-136">이 매개 변수는 지역 이름 목록을 가지는 문자열 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-136">This is parameter is an array of strings that takes a list of region names.</span></span> <span data-ttu-id="edb91-137">이름은 [Azure 지역][regions] 페이지의 지역 이름 열에 따라 서식이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-137">The names are formatted per the Region Name column in the [Azure Regions][regions] page.</span></span> <span data-ttu-id="edb91-138">또한, 편의 개체 AzureDocuments.Regions에 사전 지정된 상수를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-138">You can also use the predefined constants in the convenience object AzureDocuments.Regions</span></span>

<span data-ttu-id="edb91-139">현재 쓰기 및 읽기 끝점은 각각 DocumentClient.getWriteEndpoint와 DocumentClient.getReadEndpoint에서 이용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-139">The current write and read endpoints are available in DocumentClient.getWriteEndpoint and DocumentClient.getReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="edb91-140">끝점의 URL은 수명이 긴 상수로 간주하지 말아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-140">The URLs for the endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="edb91-141">서비스는 언제든지 이 URL을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-141">The service may update these at any point.</span></span> <span data-ttu-id="edb91-142">SDK가 이런 변경 내용을 자동으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-142">The SDK will handle this change automatically.</span></span>
>
>

<span data-ttu-id="edb91-143">다음은 NodeJS/Javascript의 코드 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-143">Below is a code example for NodeJS/Javascript.</span></span> <span data-ttu-id="edb91-144">Python과 Java도 같은 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-144">Python and Java will follow the same pattern.</span></span>

```java
// Creating a ConnectionPolicy object
var connectionPolicy = new DocumentBase.ConnectionPolicy();

// Setting read region selection preference, in the following order -
// 1 - West US
// 2 - East US
// 3 - North Europe
connectionPolicy.PreferredLocations = ['West US', 'East US', 'North Europe'];

// initialize the connection
var client = new DocumentDBClient(host, { masterKey: masterKey }, connectionPolicy);
```

## <a name="rest"></a><span data-ttu-id="edb91-145">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="edb91-145">REST</span></span>
<span data-ttu-id="edb91-146">데이터베이스 계정을 여러 지역에서 이용할 수 있게 되면 클라이언트는 다음 URI에서 GET 요청을 수행하여 가용성을 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-146">Once a database account has been made available in multiple regions, clients can query its availability by performing a GET request on the following URI.</span></span>

    https://{databaseaccount}.documents.azure.com/

<span data-ttu-id="edb91-147">서비스에서 복제본에 대한 지역 목록과 해당 Azure Cosmos DB 끝점 URI를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-147">The service will return a list of regions and their corresponding Azure Cosmos DB endpoint URIs for the replicas.</span></span> <span data-ttu-id="edb91-148">현재 쓰기 지역이 응답에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-148">The current write region will be indicated in the response.</span></span> <span data-ttu-id="edb91-149">클라이언트는 다음과 같이 모든 추가 REST API 요청에 알맞은 끝점을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-149">The client can then select the appropriate endpoint for all further REST API requests as follows.</span></span>

<span data-ttu-id="edb91-150">예제 응답</span><span class="sxs-lookup"><span data-stu-id="edb91-150">Example response</span></span>

    {
        "_dbs": "//dbs/",
        "media": "//media/",
        "writableLocations": [
            {
                "Name": "West US",
                "DatabaseAccountEndpoint": "https://globaldbexample-westus.documents.azure.com:443/"
            }
        ],
        "readableLocations": [
            {
                "Name": "East US",
                "DatabaseAccountEndpoint": "https://globaldbexample-eastus.documents.azure.com:443/"
            }
        ],
        "MaxMediaStorageUsageInMB": 2048,
        "MediaStorageUsageInMB": 0,
        "ConsistencyPolicy": {
            "defaultConsistencyLevel": "Session",
            "maxStalenessPrefix": 100,
            "maxIntervalInSeconds": 5
        },
        "addresses": "//addresses/",
        "id": "globaldbexample",
        "_rid": "globaldbexample.documents.azure.com",
        "_self": "",
        "_ts": 0,
        "_etag": null
    }


* <span data-ttu-id="edb91-151">모든 PUT, POST 및 DELETE 요청은 표시된 쓰기 URI로 이동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-151">All PUT, POST and DELETE requests must go to the indicated write URI</span></span>
* <span data-ttu-id="edb91-152">모든 GET과 다른 읽기 전용 요청(예: 쿼리)은 클라이언트가 선택한 끝점으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-152">All GETs and other read-only requests (for example queries) may go to any endpoint of the client’s choice</span></span>

<span data-ttu-id="edb91-153">읽기 전용 지역에 대한 쓰기 요청은 HTTP 오류 코드 403(“사용 권한 없음”)과 함께 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-153">Write requests to read-only regions will fail with HTTP error code 403 (“Forbidden”).</span></span>

<span data-ttu-id="edb91-154">클라이언트의 최초 검색 단계 이후에 쓰기 지역이 변경되면 나중에 이전 쓰기 지역에 쓰려고 하면 HTTP 오류 코드 403(“사용 권한 없음”)과 함께 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-154">If the write region changes after the client’s initial discovery phase, subsequent writes to the previous write region will fail with HTTP error code 403 (“Forbidden”).</span></span> <span data-ttu-id="edb91-155">클라이언트는 업데이트된 쓰기 지역을 가져오려면 지역 목록을 다시 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-155">The client should then GET the list of regions again to get the updated write region.</span></span>

<span data-ttu-id="edb91-156">이것으로 끝이며, 이 자습서를 완료했습니다!</span><span class="sxs-lookup"><span data-stu-id="edb91-156">That's it, that completes this tutorial.</span></span> <span data-ttu-id="edb91-157">[Azure Cosmos DB의 일관성 수준](consistency-levels.md)을 참조하여 전역적으로 복제한 계정의 일관성을 관리하는 방법에 대해 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-157">You can learn how to manage the consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="edb91-158">그리고 Azure Cosmos DB에서 전역 데이터베이스 복제가 작동하는 방법에 대한 자세한 내용은 [Azure Cosmos DB를 사용하여 전역적으로 데이터 배포](distribute-data-globally.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="edb91-158">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="edb91-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="edb91-159">Next steps</span></span>

<span data-ttu-id="edb91-160">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-160">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="edb91-161">Azure Portal을 사용하여 전역 배포 구성</span><span class="sxs-lookup"><span data-stu-id="edb91-161">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="edb91-162">DocumentDB API를 사용하여 전역 배포 구성</span><span class="sxs-lookup"><span data-stu-id="edb91-162">Configure global distribution using the DocumentDB APIs</span></span>

<span data-ttu-id="edb91-163">이제 다음 자습서로 진행하여 Azure Cosmos DB 로컬 에뮬레이터를 사용하여 로컬로 개발하는 방법에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edb91-163">You can now proceed to the next tutorial to learn how to develop locally using the Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="edb91-164">에뮬레이터를 사용하여 로컬로 개발</span><span class="sxs-lookup"><span data-stu-id="edb91-164">Develop locally with the emulator</span></span>](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

