---
title: "테이블 API에 대 한 aaaAzure Cosmos DB 글로벌 메일 자습서 | Microsoft Docs"
description: "어떻게 테이블 API를 사용 하 여 toosetup Azure Cosmos DB 글로벌 메일 hello에 대해 알아봅니다."
services: cosmos-db
keywords: "전역 배포, Table"
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
ms.openlocfilehash: d2a995e09c37f9449856aef2ab707e95eb8a540c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-table-api"></a><span data-ttu-id="10f7f-104">어떻게 테이블 API를 사용 하 여 toosetup Azure Cosmos DB 글로벌 메일 hello</span><span class="sxs-lookup"><span data-stu-id="10f7f-104">How toosetup Azure Cosmos DB global distribution using hello Table API</span></span>

<span data-ttu-id="10f7f-105">이 문서에서는 toouse hello Azure 포털 toosetup Azure Cosmos DB 글로벌 배포 하 고 다음 hello 테이블 API (미리 보기)를 사용 하 여를 연결 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="10f7f-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello Table API (preview).</span></span>

<span data-ttu-id="10f7f-106">이 문서에서는 다음 작업 hello를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="10f7f-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="10f7f-107">Hello Azure 포털을 사용 하 여 글로벌 배포를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="10f7f-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="10f7f-108">Hello를 사용 하 여 글로벌 배포를 구성 [테이블 API](table-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="10f7f-108">Configure global distribution using hello [Table API](table-introduction.md)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-table-api"></a><span data-ttu-id="10f7f-109">Hello 테이블 API를 사용 하 여 tooa 기본 영역 연결</span><span class="sxs-lookup"><span data-stu-id="10f7f-109">Connecting tooa preferred region using hello Table API</span></span>

<span data-ttu-id="10f7f-110">순서 tootake 활용에 [글로벌 메일](distribute-data-globally.md), 클라이언트 응용 프로그램에서 hello tooperform 문서 작업을 사용 하는 기본 설정 목록은 영역 toobe 정렬를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10f7f-110">In order tootake advantage of [global distribution](distribute-data-globally.md), client applications can specify hello ordered preference list of regions toobe used tooperform document operations.</span></span> <span data-ttu-id="10f7f-111">Hello 설정 하 여이 작업을 수행할 수 있습니다 `TablePreferredLocations` hello 미리 보기 Azure 저장소 SDK에 대 한 hello 응용 프로그램 구성에서 구성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="10f7f-111">This can be done by setting hello `TablePreferredLocations` configuration value in hello app config for hello preview Azure Storage SDK.</span></span> <span data-ttu-id="10f7f-112">Hello Azure Cosmos DB 계정 구성에 따라 현재 국가별 가용성 hello 기본 설정 목록 지정 hello 대부분 최적의 끝점 hello Azure 저장소 SDK tooperform에 의해 선택 될 지 고 읽고 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="10f7f-112">Based on hello Azure Cosmos DB account configuration, current regional availability and hello preference list specified, hello most optimal endpoint will be chosen by hello Azure Storage SDK tooperform write and read operations.</span></span>

<span data-ttu-id="10f7f-113">hello `TablePreferredLocations` 읽기에 대 한 기본 설정 (멀티 호 밍) 위치의 쉼표로 구분 된 목록에 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="10f7f-113">hello `TablePreferredLocations` should contain a comma-separated list of preferred (multi-homing) locations for reads.</span></span> <span data-ttu-id="10f7f-114">각 클라이언트 인스턴스에 대기 시간이 짧은 읽기에 대 한 hello 기본 설정 순서에 이러한 영역의 하위 집합을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10f7f-114">Each client instance can specify a subset of these regions in hello preferred order for low latency reads.</span></span> <span data-ttu-id="10f7f-115">사용 하 여 hello 영역 이름은 해당 [표시 이름을](https://msdn.microsoft.com/library/azure/gg441293.aspx), 예를 들어 `West US`합니다.</span><span class="sxs-lookup"><span data-stu-id="10f7f-115">hello regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span></span>

<span data-ttu-id="10f7f-116">모든 읽기 전송 될 첫 번째 사용 가능한 지역 toohello hello `TablePreferredLocations` 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="10f7f-116">All reads will be sent toohello first available region in hello `TablePreferredLocations` list.</span></span> <span data-ttu-id="10f7f-117">Hello 요청이 실패할 경우 hello 클라이언트 hello 목록 toohello 다음 영역을 아래로 실패를 업데이트 하 고 등 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10f7f-117">If hello request fails, hello client will fail down hello list toohello next region, and so on.</span></span>

<span data-ttu-id="10f7f-118">hello SDK는에 지정 된 hello 지역에서 tooread 시도 `TablePreferredLocations`합니다.</span><span class="sxs-lookup"><span data-stu-id="10f7f-118">hello SDK will only attempt tooread from hello regions specified in `TablePreferredLocations`.</span></span> <span data-ttu-id="10f7f-119">따라서 예를 들어 3 개의 영역에서 데이터베이스 계정 hello를 사용할 수 있지만 hello 클라이언트에 두 개의 항목을 지정 하는 경우 hello에 대 한 쓰기 이외의 영역 `TablePreferredLocations`, 읽기는 장애 조치의 hello 경우에도 hello 쓰기 영역 외부로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="10f7f-119">So, for example, if hello Database Account is available in three regions, but hello client only specifies two of hello non-write regions for `TablePreferredLocations`, then no reads will be served out of hello write region, even in hello case of failover.</span></span>

<span data-ttu-id="10f7f-120">hello SDK에서는 모든 쓰기 toohello 현재 쓰기 지역 자동으로 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="10f7f-120">hello SDK will automatically send all writes toohello current write region.</span></span>

<span data-ttu-id="10f7f-121">경우 hello `TablePreferredLocations` 속성이 설정 되지 않으면, 모든 요청 hello 현재 쓰기 영역에서 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10f7f-121">If hello `TablePreferredLocations` property is not set, all requests will be served from hello current write region.</span></span>

```xml
    <appSettings>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>           
    </appSettings>
```

<span data-ttu-id="10f7f-122">이것으로 끝이며, 이 자습서를 완료했습니다!</span><span class="sxs-lookup"><span data-stu-id="10f7f-122">That's it, that completes this tutorial.</span></span> <span data-ttu-id="10f7f-123">읽어 toomanage 전역적으로 복제 된 계정의 일관성 hello 하는 방법을 학습할 수 있는 [Azure Cosmos DB의 일관성 수준](consistency-levels.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="10f7f-123">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="10f7f-124">그리고 Azure Cosmos DB에서 전역 데이터베이스 복제가 작동하는 방법에 대한 자세한 내용은 [Azure Cosmos DB를 사용하여 전역적으로 데이터 배포](distribute-data-globally.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="10f7f-124">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="10f7f-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="10f7f-125">Next steps</span></span>

<span data-ttu-id="10f7f-126">이 자습서에서는 hello 다음 작업을 수행 하면:</span><span class="sxs-lookup"><span data-stu-id="10f7f-126">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="10f7f-127">Hello Azure 포털을 사용 하 여 글로벌 배포를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="10f7f-127">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="10f7f-128">Hello DocumentDB Api를 사용 하 여 글로벌 배포를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="10f7f-128">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="10f7f-129">다음 자습서 toolearn toohello 이제 진행할 수 있습니다 어떻게 사용 하 여 로컬로 toodevelop hello Azure Cosmos DB의 로컬 에뮬레이터입니다.</span><span class="sxs-lookup"><span data-stu-id="10f7f-129">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="10f7f-130">Hello 에뮬레이터를 사용 하 여 로컬 개발</span><span class="sxs-lookup"><span data-stu-id="10f7f-130">Develop locally with hello emulator</span></span>](local-emulator.md)
