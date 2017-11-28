---
title: "Graph API에 대 한 aaaAzure Cosmos DB 글로벌 메일 자습서 | Microsoft Docs"
description: "어떻게 Graph API를 사용 하 여 toosetup Azure Cosmos DB 글로벌 메일 hello에 대해 알아봅니다."
services: cosmos-db
keywords: "전역 배포, 그래프, Gremlin"
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: denlee
ms.openlocfilehash: 1629a31e12a18079f63e07c4909862b36b5f4c0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-graph-api"></a><span data-ttu-id="e18d8-104">어떻게 Graph API를 사용 하 여 toosetup Azure Cosmos DB 글로벌 메일 hello</span><span class="sxs-lookup"><span data-stu-id="e18d8-104">How toosetup Azure Cosmos DB global distribution using hello Graph API</span></span>

<span data-ttu-id="e18d8-105">이 문서에서는 toouse Azure 포털 toosetup Azure Cosmos DB 글로벌 메일 hello 하 한 다음 Graph API (미리 보기) hello를 사용 하 여를 연결 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="e18d8-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello Graph API (preview).</span></span>

<span data-ttu-id="e18d8-106">이 문서에서는 다음 작업 hello를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="e18d8-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="e18d8-107">Hello Azure 포털을 사용 하 여 글로벌 배포를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e18d8-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="e18d8-108">Hello를 사용 하 여 글로벌 배포를 구성 [그래프 Api](graph-introduction.md) (미리 보기)</span><span class="sxs-lookup"><span data-stu-id="e18d8-108">Configure global distribution using hello [Graph APIs](graph-introduction.md) (preview)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-graph-api-using-hello-net-sdk"></a><span data-ttu-id="e18d8-109">Hello.NET SDK를 사용 하 여 hello Graph API를 사용 하 여 tooa 기본 영역 연결</span><span class="sxs-lookup"><span data-stu-id="e18d8-109">Connecting tooa preferred region using hello Graph API using hello .NET SDK</span></span>

<span data-ttu-id="e18d8-110">hello Graph API는 확장 라이브러리 hello DocumentDB SDK 맨 위에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e18d8-110">hello Graph API is exposed as an extension library on top of hello DocumentDB SDK.</span></span>

<span data-ttu-id="e18d8-111">순서 tootake 활용에 [글로벌 메일](distribute-data-globally.md), 클라이언트 응용 프로그램에서 hello tooperform 문서 작업을 사용 하는 기본 설정 목록은 영역 toobe 정렬를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e18d8-111">In order tootake advantage of [global distribution](distribute-data-globally.md), client applications can specify hello ordered preference list of regions toobe used tooperform document operations.</span></span> <span data-ttu-id="e18d8-112">Hello 연결 정책을 설정 하 여이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e18d8-112">This can be done by setting hello connection policy.</span></span> <span data-ttu-id="e18d8-113">Hello Azure Cosmos DB 계정 구성에 따라 현재 국가별 가용성 및 hello 기본 설정 목록 지정 hello 대부분 최적의 끝점 hello SDK tooperform 쓰기에 의해 선택 되 고 읽기 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="e18d8-113">Based on hello Azure Cosmos DB account configuration, current regional availability and hello preference list specified, hello most optimal endpoint will be chosen by hello SDK tooperform write and read operations.</span></span>

<span data-ttu-id="e18d8-114">이 기본 설정 목록은 hello Sdk를 사용 하는 연결을 초기화할 때 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e18d8-114">This preference list is specified when initializing a connection using hello SDKs.</span></span> <span data-ttu-id="e18d8-115">hello Sdk에는 선택적 매개 변수 "PreferredLocations" 동의 Azure 지역의 정렬된 된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="e18d8-115">hello SDKs accept an optional parameter "PreferredLocations" that is an ordered list of Azure regions.</span></span>

* <span data-ttu-id="e18d8-116">**기록**: SDK에서는 자동으로 모든 전송 hello toohello 현재 쓰기 영역을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="e18d8-116">**Writes**: hello SDK will automatically send all writes toohello current write region.</span></span>
* <span data-ttu-id="e18d8-117">**읽고**:이, 모든 읽기 toohello 첫 번째 사용 가능한 지역 hello PreferredLocations 목록에 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="e18d8-117">**Reads**: All reads will be sent toohello first available region in hello PreferredLocations list.</span></span> <span data-ttu-id="e18d8-118">Hello 요청이 실패할 경우 hello 클라이언트 hello 목록 toohello 다음 영역을 아래로 실패를 업데이트 하 고 등 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e18d8-118">If hello request fails, hello client will fail down hello list toohello next region, and so on.</span></span> <span data-ttu-id="e18d8-119">hello Sdk PreferredLocations에 지정 된 hello 지역에서 tooread를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="e18d8-119">hello SDKs will only attempt tooread from hello regions specified in PreferredLocations.</span></span> <span data-ttu-id="e18d8-120">따라서 예를 들어 hello Cosmos DB 계정은 3 개의 영역에서 사용할 수 있어도 hello 클라이언트만 지정 hello 쓰기 이외의 영역 중 두 PreferredLocations에 대 한 다음 읽기는 제공 장애 조치의 hello 경우에도 hello 쓰기 영역 외부로.</span><span class="sxs-lookup"><span data-stu-id="e18d8-120">So, for example, if hello Cosmos DB account is available in three regions, but hello client only specifies two of hello non-write regions for PreferredLocations, then no reads will be served out of hello write region, even in hello case of failover.</span></span>

<span data-ttu-id="e18d8-121">hello 응용 프로그램 hello 현재 쓰기 끝점을 확인 하 고 확인 하는 중 두 가지 속성인 WriteEndpoint 및 ReadEndpoint SDK 버전 1.8 이상 사용할 수 있는 hello SDK가 선택한 끝점을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e18d8-121">hello application can verify hello current write endpoint and read endpoint chosen by hello SDK by checking two properties, WriteEndpoint and ReadEndpoint, available in SDK version 1.8 and above.</span></span> <span data-ttu-id="e18d8-122">Hello PreferredLocations 속성을 설정 하지 않으면 모든 요청은 hello 현재 쓰기 영역에서 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e18d8-122">If hello PreferredLocations property is not set, all requests will be served from hello current write region.</span></span>

### <a name="using-hello-sdk"></a><span data-ttu-id="e18d8-123">Hello SDK를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e18d8-123">Using hello SDK</span></span>

<span data-ttu-id="e18d8-124">예를 들어.NET SDK hello를 hello `ConnectionPolicy` hello에 대 한 매개 변수 `DocumentClient` 생성자에 라는 속성이 `PreferredLocations`합니다.</span><span class="sxs-lookup"><span data-stu-id="e18d8-124">For example, in hello .NET SDK, hello `ConnectionPolicy` parameter for hello `DocumentClient` constructor has a property called `PreferredLocations`.</span></span> <span data-ttu-id="e18d8-125">이 속성에는 지역 이름 목록은 tooa 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e18d8-125">This property can be set tooa list of region names.</span></span> <span data-ttu-id="e18d8-126">에 대 한 hello 표시 이름이 [Azure 지역] [ regions] 의 일부로 지정할 수 있습니다 `PreferredLocations`합니다.</span><span class="sxs-lookup"><span data-stu-id="e18d8-126">hello display names for [Azure Regions][regions] can be specified as part of `PreferredLocations`.</span></span>

> [!NOTE]
> <span data-ttu-id="e18d8-127">hello 끝점에 대 한 hello Url 수명이 긴 상수로 간주 되지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e18d8-127">hello URLs for hello endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="e18d8-128">hello 서비스는 언제 든 지 이러한 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e18d8-128">hello service may update these at any point.</span></span> <span data-ttu-id="e18d8-129">hello SDK는이 변경 내용을 자동으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="e18d8-129">hello SDK handles this change automatically.</span></span>
>
>

```cs
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

// connect tooAzure Cosmos DB
await docClient.OpenAsync().ConfigureAwait(false);
```

<span data-ttu-id="e18d8-130">이것으로 끝이며, 이 자습서를 완료했습니다!</span><span class="sxs-lookup"><span data-stu-id="e18d8-130">That's it, that completes this tutorial.</span></span> <span data-ttu-id="e18d8-131">읽어 toomanage 전역적으로 복제 된 계정의 일관성 hello 하는 방법을 학습할 수 있는 [Azure Cosmos DB의 일관성 수준](consistency-levels.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e18d8-131">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="e18d8-132">그리고 Azure Cosmos DB에서 전역 데이터베이스 복제가 작동하는 방법에 대한 자세한 내용은 [Azure Cosmos DB를 사용하여 전역적으로 데이터 배포](distribute-data-globally.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e18d8-132">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e18d8-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e18d8-133">Next steps</span></span>

<span data-ttu-id="e18d8-134">이 자습서에서는 hello 다음 작업을 수행 하면:</span><span class="sxs-lookup"><span data-stu-id="e18d8-134">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e18d8-135">Hello Azure 포털을 사용 하 여 글로벌 배포를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e18d8-135">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="e18d8-136">Hello DocumentDB Api를 사용 하 여 글로벌 배포를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e18d8-136">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="e18d8-137">다음 자습서 toolearn toohello 이제 진행할 수 있습니다 어떻게 사용 하 여 로컬로 toodevelop hello Azure Cosmos DB의 로컬 에뮬레이터입니다.</span><span class="sxs-lookup"><span data-stu-id="e18d8-137">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e18d8-138">Hello 에뮬레이터를 사용 하 여 로컬 개발</span><span class="sxs-lookup"><span data-stu-id="e18d8-138">Develop locally with hello emulator</span></span>](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

