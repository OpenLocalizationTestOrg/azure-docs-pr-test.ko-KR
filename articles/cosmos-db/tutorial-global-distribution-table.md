---
title: "Table API의 Azure Cosmos DB 전역 배포 자습서 | Microsoft Docs"
description: "Table API를 사용하여 Azure Cosmos DB 전역 배포를 설정하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 63c9e530a4982e2e6e478fea56e015fc77851e1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-setup-azure-cosmos-db-global-distribution-using-the-table-api"></a><span data-ttu-id="85d42-104">Table API를 사용하여 Azure Cosmos DB 전역 배포를 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="85d42-104">How to setup Azure Cosmos DB global distribution using the Table API</span></span>

<span data-ttu-id="85d42-105">이 문서에서는 Azure Portal을 사용하여 Azure Cosmos DB 전역 배포를 설정한 다음 Table API(미리 보기)를 사용하여 연결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="85d42-105">In this article, we show how to use the Azure portal to setup Azure Cosmos DB global distribution and then connect using the Table API (preview).</span></span>

<span data-ttu-id="85d42-106">이 문서에서 다루는 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="85d42-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="85d42-107">Azure Portal을 사용하여 전역 배포 구성</span><span class="sxs-lookup"><span data-stu-id="85d42-107">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="85d42-108">[Table API](table-introduction.md)를 사용하여 전역 배포 구성</span><span class="sxs-lookup"><span data-stu-id="85d42-108">Configure global distribution using the [Table API](table-introduction.md)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-to-a-preferred-region-using-the-table-api"></a><span data-ttu-id="85d42-109">Table API를 사용하여 기본 설정 지역에 연결</span><span class="sxs-lookup"><span data-stu-id="85d42-109">Connecting to a preferred region using the Table API</span></span>

<span data-ttu-id="85d42-110">[전역 배포](distribute-data-globally.md)를 활용하기 위해 클라이언트 응용 프로그램은 문서 작업을 수행하는 데 사용할 정렬된 기본 지역 목록을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85d42-110">In order to take advantage of [global distribution](distribute-data-globally.md), client applications can specify the ordered preference list of regions to be used to perform document operations.</span></span> <span data-ttu-id="85d42-111">이렇게 하려면 미리 보기 Azure Storage SDK의 앱 구성에서 `TablePreferredLocations` 구성 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="85d42-111">This can be done by setting the `TablePreferredLocations` configuration value in the app config for the preview Azure Storage SDK.</span></span> <span data-ttu-id="85d42-112">Azure Storage SDK에서 Azure Cosmos DB 계정 구성, 현재 지역 가용성 및 지정된 기본 설정 목록을 기반으로 하여 쓰기 및 읽기 작업을 수행하는 데 가장 적합한 끝점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85d42-112">Based on the Azure Cosmos DB account configuration, current regional availability and the preference list specified, the most optimal endpoint will be chosen by the Azure Storage SDK to perform write and read operations.</span></span>

<span data-ttu-id="85d42-113">`TablePreferredLocations`에는 읽기에 대해 기본 설정된(멀티 홈) 위치를 쉼표로 구분한 목록이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85d42-113">The `TablePreferredLocations` should contain a comma-separated list of preferred (multi-homing) locations for reads.</span></span> <span data-ttu-id="85d42-114">각 클라이언트 인스턴스는 대기 시간이 짧은 읽기에 대해 기본 설정된 순서대로 이러한 지역의 하위 집합을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85d42-114">Each client instance can specify a subset of these regions in the preferred order for low latency reads.</span></span> <span data-ttu-id="85d42-115">지역 이름은 [표시 이름](https://msdn.microsoft.com/library/azure/gg441293.aspx)(예: `West US`)을 사용하여 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85d42-115">The regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span></span>

<span data-ttu-id="85d42-116">모든 읽기는 `TablePreferredLocations` 목록에서 사용 가능한 첫 번째 지역으로 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="85d42-116">All reads will be sent to the first available region in the `TablePreferredLocations` list.</span></span> <span data-ttu-id="85d42-117">요청이 실패하면 클라이언트는 목록의 다음 지역으로 옮겨갑니다.</span><span class="sxs-lookup"><span data-stu-id="85d42-117">If the request fails, the client will fail down the list to the next region, and so on.</span></span>

<span data-ttu-id="85d42-118">SDK는 `TablePreferredLocations`에 지정된 지역에서만 읽기를 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="85d42-118">The SDK will only attempt to read from the regions specified in `TablePreferredLocations`.</span></span> <span data-ttu-id="85d42-119">예를 들어 데이터베이스 계정이 세 지역에서 사용할 수 있지만, 클라이언트에서 `TablePreferredLocations`에 대해 쓰기에 해당하지 않는 영역 두 개만 지정하면 장애 조치 시에도 쓰기 지역에서 읽기를 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85d42-119">So, for example, if the Database Account is available in three regions, but the client only specifies two of the non-write regions for `TablePreferredLocations`, then no reads will be served out of the write region, even in the case of failover.</span></span>

<span data-ttu-id="85d42-120">SDK는 현재 쓰기 지역에 모든 쓰기를 자동 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="85d42-120">The SDK will automatically send all writes to the current write region.</span></span>

<span data-ttu-id="85d42-121">`TablePreferredLocations` 속성이 설정되지 않으면 모든 요청이 현재 쓰기 지역에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="85d42-121">If the `TablePreferredLocations` property is not set, all requests will be served from the current write region.</span></span>

```xml
    <appSettings>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>           
    </appSettings>
```

<span data-ttu-id="85d42-122">이것으로 끝이며, 이 자습서를 완료했습니다!</span><span class="sxs-lookup"><span data-stu-id="85d42-122">That's it, that completes this tutorial.</span></span> <span data-ttu-id="85d42-123">[Azure Cosmos DB의 일관성 수준](consistency-levels.md)을 참조하여 전역적으로 복제한 계정의 일관성을 관리하는 방법에 대해 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85d42-123">You can learn how to manage the consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="85d42-124">그리고 Azure Cosmos DB에서 전역 데이터베이스 복제가 작동하는 방법에 대한 자세한 내용은 [Azure Cosmos DB를 사용하여 전역적으로 데이터 배포](distribute-data-globally.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85d42-124">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="85d42-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="85d42-125">Next steps</span></span>

<span data-ttu-id="85d42-126">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="85d42-126">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="85d42-127">Azure Portal을 사용하여 전역 배포 구성</span><span class="sxs-lookup"><span data-stu-id="85d42-127">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="85d42-128">DocumentDB API를 사용하여 전역 배포 구성</span><span class="sxs-lookup"><span data-stu-id="85d42-128">Configure global distribution using the DocumentDB APIs</span></span>

<span data-ttu-id="85d42-129">이제 다음 자습서로 진행하여 Azure Cosmos DB 로컬 에뮬레이터를 사용하여 로컬로 개발하는 방법에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85d42-129">You can now proceed to the next tutorial to learn how to develop locally using the Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="85d42-130">에뮬레이터를 사용하여 로컬로 개발</span><span class="sxs-lookup"><span data-stu-id="85d42-130">Develop locally with the emulator</span></span>](local-emulator.md)