---
title: "Azure Cosmos DB에 대한 처리량 프로비전 | Microsoft Docs"
description: "Azure Cosmos DB 컨테이너, 컬렉션, 그래프 및 테이블에 대해 프로비전된 처리량을 설정하는 방법을 알아봅니다."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: f98def7f-f012-4592-be03-f6fa185e1b1e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: mimig
ms.openlocfilehash: d541bb19ba7e5ecb44c9fe91b1e232d4d9c2170e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="set-throughput-for-azure-cosmos-db-containers"></a><span data-ttu-id="db01a-103">Azure Cosmos DB 컨테이너에 대한 처리량 설정</span><span class="sxs-lookup"><span data-stu-id="db01a-103">Set throughput for Azure Cosmos DB containers</span></span>

<span data-ttu-id="db01a-104">Azure Portal 또는 클라이언트 SDK를 사용하여 Azure Cosmos DB 컨테이너에 대한 처리량을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db01a-104">You can set throughput for your Azure Cosmos DB containers in the Azure portal or by using the client SDKs.</span></span> 

<span data-ttu-id="db01a-105">다음 테이블에는 컨테이너에 사용할 수 있는 처리량이 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db01a-105">The following table lists the throughput available for containers:</span></span>

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p></p></td>
            <td valign="top"><p><span data-ttu-id="db01a-106"><strong>단일 파티션 컨테이너</strong></span><span class="sxs-lookup"><span data-stu-id="db01a-106"><strong>Single Partition Container</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="db01a-107"><strong>분할된 컨테이너</strong></span><span class="sxs-lookup"><span data-stu-id="db01a-107"><strong>Partitioned Container</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="db01a-108">최소 처리량</span><span class="sxs-lookup"><span data-stu-id="db01a-108">Minimum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="db01a-109">초당 요청 단위 400개</span><span class="sxs-lookup"><span data-stu-id="db01a-109">400 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="db01a-110">초당 요청 단위 2,500개</span><span class="sxs-lookup"><span data-stu-id="db01a-110">2,500 request units per second</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="db01a-111">최대 처리량</span><span class="sxs-lookup"><span data-stu-id="db01a-111">Maximum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="db01a-112">초당 요청 단위 10,000개</span><span class="sxs-lookup"><span data-stu-id="db01a-112">10,000 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="db01a-113">Unlimited</span><span class="sxs-lookup"><span data-stu-id="db01a-113">Unlimited</span></span></p></td>
        </tr>
    </tbody>
</table>

## <a name="to-set-the-throughput-by-using-the-azure-portal"></a><span data-ttu-id="db01a-114">Azure Portal을 사용하여 처리량을 설정하려면</span><span class="sxs-lookup"><span data-stu-id="db01a-114">To set the throughput by using the Azure portal</span></span>

1. <span data-ttu-id="db01a-115">새 창에서 [Azure Portal](https://portal.azure.com)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="db01a-115">In a new window, open the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="db01a-116">왼쪽 모음에서 **Azure Cosmos DB**를 클릭하거나 맨 아래에서 **더 많은 서비스**를 클릭한 다음 **데이터베이스**로 스크롤하고 **Azure Cosmos DB**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db01a-116">On the left bar, click **Azure Cosmos DB**, or click **More Services** at the bottom, then scroll to **Databases**, and then click **Azure Cosmos DB**.</span></span>
3. <span data-ttu-id="db01a-117">Cosmos DB 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db01a-117">Select your Cosmos DB account.</span></span>
4. <span data-ttu-id="db01a-118">새 창의 탐색 메뉴에서 **데이터 탐색기(미리 보기)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db01a-118">In the new window, click **Data Explorer (Preview)** in the navigation menu.</span></span>
5. <span data-ttu-id="db01a-119">새 창에서 데이터베이스와 컨테이너를 확장하고 **배율 및 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db01a-119">In the new window, expand your database and container and then click **Scale & Settings**.</span></span>
6. <span data-ttu-id="db01a-120">새 창에서 **처리량** 상자에 새 처리량 값을 입력하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="db01a-120">In the new window, type the new throughput value in the **Throughput** box, and then click **Save**.</span></span>

<a id="set-throughput-sdk"></a>

## <a name="to-set-the-throughput-by-using-the-documentdb-api-for-net"></a><span data-ttu-id="db01a-121">DocumentDB API for .NET을 사용하여 처리량을 설정하려면</span><span class="sxs-lookup"><span data-stu-id="db01a-121">To set the throughput by using the DocumentDB API for .NET</span></span>

```C#
//Fetch the resource to be updated
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set the throughput to the new value, for example 12,000 request units per second
offer = new OfferV2(offer, 12000);

//Now persist these changes to the database by replacing the original resource
await client.ReplaceOfferAsync(offer);
```

## <a name="throughput-faq"></a><span data-ttu-id="db01a-122">처리량 FAQ</span><span class="sxs-lookup"><span data-stu-id="db01a-122">Throughput FAQ</span></span>

<span data-ttu-id="db01a-123">**내 처리량을 400RU/s 미만으로 설정할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="db01a-123">**Can I set my throughput to less than 400 RU/s?**</span></span>

<span data-ttu-id="db01a-124">Cosmos DB 단일 파티션 컬렉션에서 사용할 수 있는 최소 처리량은 400RU/s이고 분할된 컬렉션에 대한 최소값은 2500RU/s입니다.</span><span class="sxs-lookup"><span data-stu-id="db01a-124">400 RU/s is the minimum throughput available on Cosmos DB single partition collections (2500 RU/s is the minimum for partitioned collections).</span></span> <span data-ttu-id="db01a-125">요청 단위는 100RU/s 간격으로 설정되어 있지만 처리량은 100RU/s 또는 400RU/s 미만인 값으로 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="db01a-125">Request units are set in 100 RU/s intervals, but throughput cannot be set to 100 RU/s or any value smaller than 400 RU/s.</span></span> <span data-ttu-id="db01a-126">Cosmos DB를 개발하고 테스트하는 비용 효과적인 방법을 찾으려는 경우 비용 없이 로컬에 배포할 수 있는 [Azure Cosmos DB 에뮬레이터](local-emulator.md)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db01a-126">If you're looking for a cost effective method to develop and test Cosmos DB, you can use the free [Azure Cosmos DB Emulator](local-emulator.md), which you can deploy locally at no cost.</span></span> 

<span data-ttu-id="db01a-127">**MongoDB API를 사용하여 처리량을 설정하려면 어떻게 해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="db01a-127">**How do I set througput using the MongoDB API?**</span></span>

<span data-ttu-id="db01a-128">처리량을 설정할 수 있는 MongoDB API 확장은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="db01a-128">There's no MongoDB API extension to set throughput.</span></span> <span data-ttu-id="db01a-129">[DocumentDB API for .NET을 사용하여 처리량을 설정하려면](#set-throughput-sdk)에 나와 있는 대로 DocumentDB API를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="db01a-129">The recommendation is to use the DocumentDB API, as shown in [To set the throughput by using the DocumentDB API for .NET](#set-throughput-sdk).</span></span>

## <a name="next-steps"></a><span data-ttu-id="db01a-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="db01a-130">Next steps</span></span>

<span data-ttu-id="db01a-131">Cosmos DB를 사용하여 프로비전을 수행하고 대규모로 크기를 조정하려면 [Cosmos DB로 분할 및 크기 조정](partition-data.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db01a-131">To learn more about provisioning and going planet-scale with Cosmos DB, see [Partitioning and scaling with Cosmos DB](partition-data.md).</span></span>
