---
title: "DocumentDB API에 대 한 aaaAzure Cosmos DB 글로벌 메일 자습서 | Microsoft Docs"
description: "어떻게 DocumentDB API를 사용 하 여 toosetup Azure Cosmos DB 글로벌 메일 hello에 대해 알아봅니다."
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
ms.openlocfilehash: a1d5f01faa62407fbbc9c078ef4a9589a1a29219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-documentdb-api"></a><span data-ttu-id="8cbfd-104">어떻게 DocumentDB API를 사용 하 여 toosetup Azure Cosmos DB 글로벌 메일 hello</span><span class="sxs-lookup"><span data-stu-id="8cbfd-104">How toosetup Azure Cosmos DB global distribution using hello DocumentDB API</span></span>

<span data-ttu-id="8cbfd-105">이 문서에서는 toouse hello Azure 포털 toosetup Azure Cosmos DB 글로벌 배포 하 고 다음 hello DocumentDB API를 사용 하 여를 연결 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello DocumentDB API.</span></span>

<span data-ttu-id="8cbfd-106">이 문서에서는 다음 작업 hello를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="8cbfd-107">Hello Azure 포털을 사용 하 여 글로벌 배포를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="8cbfd-108">Hello를 사용 하 여 글로벌 배포를 구성 [DocumentDB Api](documentdb-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="8cbfd-108">Configure global distribution using hello [DocumentDB APIs](documentdb-introduction.md)</span></span>

<a id="portal"></a>
[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-documentdb-api"></a><span data-ttu-id="8cbfd-109">Hello DocumentDB API를 사용 하 여 tooa 기본 영역 연결</span><span class="sxs-lookup"><span data-stu-id="8cbfd-109">Connecting tooa preferred region using hello DocumentDB API</span></span>

<span data-ttu-id="8cbfd-110">순서 tootake 활용에 [글로벌 메일](distribute-data-globally.md), 클라이언트 응용 프로그램에서 hello tooperform 문서 작업을 사용 하는 기본 설정 목록은 영역 toobe 정렬를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-110">In order tootake advantage of [global distribution](distribute-data-globally.md), client applications can specify hello ordered preference list of regions toobe used tooperform document operations.</span></span> <span data-ttu-id="8cbfd-111">Hello 연결 정책을 설정 하 여이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-111">This can be done by setting hello connection policy.</span></span> <span data-ttu-id="8cbfd-112">Hello Azure Cosmos DB 계정 구성에 따라 현재 국가별 가용성 및 hello 기본 설정 목록 지정 hello 대부분 최적의 끝점 hello DocumentDB SDK tooperform 쓰기 및 읽기 작업에 의해 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-112">Based on hello Azure Cosmos DB account configuration, current regional availability and hello preference list specified, hello most optimal endpoint will be chosen by hello DocumentDB SDK tooperform write and read operations.</span></span>

<span data-ttu-id="8cbfd-113">이 기본 설정 목록은 hello DocumentDB Sdk를 사용 하는 연결을 초기화할 때 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-113">This preference list is specified when initializing a connection using hello DocumentDB SDKs.</span></span> <span data-ttu-id="8cbfd-114">hello Sdk에는 선택적 매개 변수 "PreferredLocations" 동의 Azure 지역의 정렬된 된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-114">hello SDKs accept an optional parameter "PreferredLocations" that is an ordered list of Azure regions.</span></span>

<span data-ttu-id="8cbfd-115">hello SDK에서는 모든 쓰기 toohello 현재 쓰기 지역 자동으로 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-115">hello SDK will automatically send all writes toohello current write region.</span></span>

<span data-ttu-id="8cbfd-116">모든 읽기 hello PreferredLocations 목록에서 첫 번째 사용 가능한 지역 toohello 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-116">All reads will be sent toohello first available region in hello PreferredLocations list.</span></span> <span data-ttu-id="8cbfd-117">Hello 요청이 실패할 경우 hello 클라이언트 hello 목록 toohello 다음 영역을 아래로 실패를 업데이트 하 고 등 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-117">If hello request fails, hello client will fail down hello list toohello next region, and so on.</span></span>

<span data-ttu-id="8cbfd-118">hello Sdk PreferredLocations에 지정 된 hello 지역에서 tooread를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-118">hello SDKs will only attempt tooread from hello regions specified in PreferredLocations.</span></span> <span data-ttu-id="8cbfd-119">따라서 예를 들어 3 개의 영역에서 데이터베이스 계정 hello를 사용할 수 있어도 hello 클라이언트만 두 hello 쓰기 이외의 영역에 대 한 지정 PreferredLocations 다음 읽기는 제공 장애 조치의 hello 경우에도 hello 쓰기 영역 외부로.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-119">So, for example, if hello Database Account is available in three regions, but hello client only specifies two of hello non-write regions for PreferredLocations, then no reads will be served out of hello write region, even in hello case of failover.</span></span>

<span data-ttu-id="8cbfd-120">hello 응용 프로그램 hello 현재 쓰기 끝점을 확인 하 고 확인 하는 중 두 가지 속성인 WriteEndpoint 및 ReadEndpoint SDK 버전 1.8 이상 사용할 수 있는 hello SDK가 선택한 끝점을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-120">hello application can verify hello current write endpoint and read endpoint chosen by hello SDK by checking two properties, WriteEndpoint and ReadEndpoint, available in SDK version 1.8 and above.</span></span>

<span data-ttu-id="8cbfd-121">Hello PreferredLocations 속성을 설정 하지 않으면 모든 요청은 hello 현재 쓰기 영역에서 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-121">If hello PreferredLocations property is not set, all requests will be served from hello current write region.</span></span>

## <a name="net-sdk"></a><span data-ttu-id="8cbfd-122">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="8cbfd-122">.NET SDK</span></span>
<span data-ttu-id="8cbfd-123">hello SDK 코드 변경 없이 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-123">hello SDK can be used without any code changes.</span></span> <span data-ttu-id="8cbfd-124">이 경우 SDK hello 자동으로 다이렉트 모두 읽기 및 toohello 현재 쓰기 영역을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-124">In this case, hello SDK automatically directs both reads and writes toohello current write region.</span></span>

<span data-ttu-id="8cbfd-125">Hello.NET SDK 1.8 이상 버전에서는 hello DocumentClient 생성자에 대 한 hello ConnectionPolicy 매개 변수에는 Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations 라는 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-125">In version 1.8 and later of hello .NET SDK, hello ConnectionPolicy parameter for hello DocumentClient constructor has a property called Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="8cbfd-126">이 속성은 컬렉션 `<string>` 형식이며 지역 이름 목록을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-126">This property is of type Collection `<string>` and should contain a list of region names.</span></span> <span data-ttu-id="8cbfd-127">hello에 대 한 hello 지역 이름 열당 hello 문자열 값에 형식을 지정할 [Azure 지역] [ regions] 처음으로 페이지를 앞 이나 뒤 hello 공백 없이 및 문자를 각각 마지막 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-127">hello string values are formatted per hello Region Name column on hello [Azure Regions][regions] page, with no spaces before or after hello first and last character respectively.</span></span>

<span data-ttu-id="8cbfd-128">hello 현재 쓰기 및 읽기 끝점 각각 DocumentClient.WriteEndpoint 및 DocumentClient.ReadEndpoint에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-128">hello current write and read endpoints are available in DocumentClient.WriteEndpoint and DocumentClient.ReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="8cbfd-129">hello 끝점에 대 한 hello Url 수명이 긴 상수로 간주 되지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-129">hello URLs for hello endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="8cbfd-130">hello 서비스는 언제 든 지 이러한 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-130">hello service may update these at any point.</span></span> <span data-ttu-id="8cbfd-131">hello SDK는이 변경 내용을 자동으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-131">hello SDK handles this change automatically.</span></span>
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

// connect tooDocDB
await docClient.OpenAsync().ConfigureAwait(false);
```

## <a name="nodejs-javascript-and-python-sdks"></a><span data-ttu-id="8cbfd-132">NodeJS, JavaScript 및 Python SDK</span><span class="sxs-lookup"><span data-stu-id="8cbfd-132">NodeJS, JavaScript, and Python SDKs</span></span>
<span data-ttu-id="8cbfd-133">hello SDK 코드 변경 없이 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-133">hello SDK can be used without any code changes.</span></span> <span data-ttu-id="8cbfd-134">이 경우 SDK는 자동으로 연결 하는 hello 모두 읽기 및 쓰기 toohello 현재 쓰기 지역.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-134">In this case, hello SDK will automatically direct both reads and writes toohello current write region.</span></span>

<span data-ttu-id="8cbfd-135">버전 1.8 및 각 SDK의 나중 hello ConnectionPolicy 매개 변수에서 hello DocumentClient 생성자 DocumentClient.ConnectionPolicy.PreferredLocations 라는 새 속성에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-135">In version 1.8 and later of each SDK, hello ConnectionPolicy parameter for hello DocumentClient constructor a new property called DocumentClient.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="8cbfd-136">이 매개 변수는 지역 이름 목록을 가지는 문자열 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-136">This is parameter is an array of strings that takes a list of region names.</span></span> <span data-ttu-id="8cbfd-137">hello에 대 한 hello 지역 이름 열당 hello 이름의 형식은 [Azure 지역] [ regions] 페이지.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-137">hello names are formatted per hello Region Name column in hello [Azure Regions][regions] page.</span></span> <span data-ttu-id="8cbfd-138">Hello 편의 개체 AzureDocuments.Regions에에서 미리 정의 된 hello 상수를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-138">You can also use hello predefined constants in hello convenience object AzureDocuments.Regions</span></span>

<span data-ttu-id="8cbfd-139">hello 현재 쓰기 및 읽기 끝점 각각 DocumentClient.getWriteEndpoint 및 DocumentClient.getReadEndpoint에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-139">hello current write and read endpoints are available in DocumentClient.getWriteEndpoint and DocumentClient.getReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="8cbfd-140">hello 끝점에 대 한 hello Url 수명이 긴 상수로 간주 되지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-140">hello URLs for hello endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="8cbfd-141">hello 서비스는 언제 든 지 이러한 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-141">hello service may update these at any point.</span></span> <span data-ttu-id="8cbfd-142">hello SDK는이 변경 내용을 자동으로 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-142">hello SDK will handle this change automatically.</span></span>
>
>

<span data-ttu-id="8cbfd-143">다음은 NodeJS/Javascript의 코드 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-143">Below is a code example for NodeJS/Javascript.</span></span> <span data-ttu-id="8cbfd-144">Hello Python 및 Java에 따라 동일한 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-144">Python and Java will follow hello same pattern.</span></span>

```java
// Creating a ConnectionPolicy object
var connectionPolicy = new DocumentBase.ConnectionPolicy();

// Setting read region selection preference, in hello following order -
// 1 - West US
// 2 - East US
// 3 - North Europe
connectionPolicy.PreferredLocations = ['West US', 'East US', 'North Europe'];

// initialize hello connection
var client = new DocumentDBClient(host, { masterKey: masterKey }, connectionPolicy);
```

## <a name="rest"></a><span data-ttu-id="8cbfd-145">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="8cbfd-145">REST</span></span>
<span data-ttu-id="8cbfd-146">데이터베이스 계정을 수 있게 된 여러 지역에서 되 면 클라이언트 hello 다음 URI에 GET 요청을 수행 하 여 가용성을 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-146">Once a database account has been made available in multiple regions, clients can query its availability by performing a GET request on hello following URI.</span></span>

    https://{databaseaccount}.documents.azure.com/

<span data-ttu-id="8cbfd-147">hello 서비스는 영역 및 hello 복제본에 대 한 자신의 해당 Azure Cosmos DB 끝점 Uri의 목록을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-147">hello service will return a list of regions and their corresponding Azure Cosmos DB endpoint URIs for hello replicas.</span></span> <span data-ttu-id="8cbfd-148">hello 현재 쓰기 지역 hello 응답에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-148">hello current write region will be indicated in hello response.</span></span> <span data-ttu-id="8cbfd-149">그런 다음 hello 클라이언트 hello 이후 모든 REST API 요청에 대 한 적절 한 끝점을 다음과 같이 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-149">hello client can then select hello appropriate endpoint for all further REST API requests as follows.</span></span>

<span data-ttu-id="8cbfd-150">예제 응답</span><span class="sxs-lookup"><span data-stu-id="8cbfd-150">Example response</span></span>

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


* <span data-ttu-id="8cbfd-151">모든 PUT, POST 및 DELETE 요청 다음에 야 toohello 표시 된 URI를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-151">All PUT, POST and DELETE requests must go toohello indicated write URI</span></span>
* <span data-ttu-id="8cbfd-152">모든 GETs 및 다른 읽기 전용 요청 (예: 쿼리) hello 클라이언트의 선택한 tooany 끝점 전환 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-152">All GETs and other read-only requests (for example queries) may go tooany endpoint of hello client’s choice</span></span>

<span data-ttu-id="8cbfd-153">쓰기 요청 tooread 전용 영역 HTTP 오류 코드 403 ("사용할 수 없음")와 함께 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-153">Write requests tooread-only regions will fail with HTTP error code 403 (“Forbidden”).</span></span>

<span data-ttu-id="8cbfd-154">Hello 쓰기 지역 후 변경 되 면 hello 클라이언트의 초기 검색 단계에서 후속 씁니다 toohello 이전 쓰기 지역 HTTP 오류 코드 403 ("사용할 수 없음")와 함께 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-154">If hello write region changes after hello client’s initial discovery phase, subsequent writes toohello previous write region will fail with HTTP error code 403 (“Forbidden”).</span></span> <span data-ttu-id="8cbfd-155">클라이언트 hello 다음 구해야 hello 지역 목록이 다시 tooget hello 업데이트 쓰기 영역 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-155">hello client should then GET hello list of regions again tooget hello updated write region.</span></span>

<span data-ttu-id="8cbfd-156">이것으로 끝이며, 이 자습서를 완료했습니다!</span><span class="sxs-lookup"><span data-stu-id="8cbfd-156">That's it, that completes this tutorial.</span></span> <span data-ttu-id="8cbfd-157">읽어 toomanage 전역적으로 복제 된 계정의 일관성 hello 하는 방법을 학습할 수 있는 [Azure Cosmos DB의 일관성 수준](consistency-levels.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-157">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="8cbfd-158">그리고 Azure Cosmos DB에서 전역 데이터베이스 복제가 작동하는 방법에 대한 자세한 내용은 [Azure Cosmos DB를 사용하여 전역적으로 데이터 배포](distribute-data-globally.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-158">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8cbfd-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8cbfd-159">Next steps</span></span>

<span data-ttu-id="8cbfd-160">이 자습서에서는 hello 다음 작업을 수행 하면:</span><span class="sxs-lookup"><span data-stu-id="8cbfd-160">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8cbfd-161">Hello Azure 포털을 사용 하 여 글로벌 배포를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-161">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="8cbfd-162">Hello DocumentDB Api를 사용 하 여 글로벌 배포를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-162">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="8cbfd-163">다음 자습서 toolearn toohello 이제 진행할 수 있습니다 어떻게 사용 하 여 로컬로 toodevelop hello Azure Cosmos DB의 로컬 에뮬레이터입니다.</span><span class="sxs-lookup"><span data-stu-id="8cbfd-163">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8cbfd-164">Hello 에뮬레이터를 사용 하 여 로컬 개발</span><span class="sxs-lookup"><span data-stu-id="8cbfd-164">Develop locally with hello emulator</span></span>](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

