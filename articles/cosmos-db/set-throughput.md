---
title: "Azure Cosmos DB에 대 한 aaaProvision 처리량 | Microsoft Docs"
description: "프로그램 Azure Cosmos DB containsers, 컬렉션, 그래프 및 테이블에 대 한 처리량 tooset 프로 비전 하는 방법을 알아봅니다."
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
ms.openlocfilehash: c143f4aace466b7109168a50e2eb80ddeca6400e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-throughput-for-azure-cosmos-db-containers"></a><span data-ttu-id="73c15-103">Azure Cosmos DB 컨테이너에 대한 처리량 설정</span><span class="sxs-lookup"><span data-stu-id="73c15-103">Set throughput for Azure Cosmos DB containers</span></span>

<span data-ttu-id="73c15-104">Hello Azure 포털에서에서 사용자 Azure Cosmos DB 컨테이너에 대 한 처리량을 설정 하거나 hello client Sdk를 사용 하 여 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73c15-104">You can set throughput for your Azure Cosmos DB containers in hello Azure portal or by using hello client SDKs.</span></span> 

<span data-ttu-id="73c15-105">다음 표에서 hello 컨테이너에 사용할 수 있는 hello 처리량을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="73c15-105">hello following table lists hello throughput available for containers:</span></span>

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p></p></td>
            <td valign="top"><p><span data-ttu-id="73c15-106"><strong>단일 파티션 컨테이너</strong></span><span class="sxs-lookup"><span data-stu-id="73c15-106"><strong>Single Partition Container</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="73c15-107"><strong>분할된 컨테이너</strong></span><span class="sxs-lookup"><span data-stu-id="73c15-107"><strong>Partitioned Container</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="73c15-108">최소 처리량</span><span class="sxs-lookup"><span data-stu-id="73c15-108">Minimum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="73c15-109">초당 요청 단위 400개</span><span class="sxs-lookup"><span data-stu-id="73c15-109">400 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="73c15-110">초당 요청 단위 2,500개</span><span class="sxs-lookup"><span data-stu-id="73c15-110">2,500 request units per second</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="73c15-111">최대 처리량</span><span class="sxs-lookup"><span data-stu-id="73c15-111">Maximum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="73c15-112">초당 요청 단위 10,000개</span><span class="sxs-lookup"><span data-stu-id="73c15-112">10,000 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="73c15-113">Unlimited</span><span class="sxs-lookup"><span data-stu-id="73c15-113">Unlimited</span></span></p></td>
        </tr>
    </tbody>
</table>

## <a name="tooset-hello-throughput-by-using-hello-azure-portal"></a><span data-ttu-id="73c15-114">hello Azure 포털을 사용 하 여 tooset hello 처리량</span><span class="sxs-lookup"><span data-stu-id="73c15-114">tooset hello throughput by using hello Azure portal</span></span>

1. <span data-ttu-id="73c15-115">새 창에서 열고 hello [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="73c15-115">In a new window, open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="73c15-116">Hello 왼쪽된 모음에서 **Azure Cosmos DB**, 하거나 클릭 **더 서비스** hello 맨 아래에 다음 스크롤하여 너무**데이터베이스**, 클릭 하 고 **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="73c15-116">On hello left bar, click **Azure Cosmos DB**, or click **More Services** at hello bottom, then scroll too**Databases**, and then click **Azure Cosmos DB**.</span></span>
3. <span data-ttu-id="73c15-117">Cosmos DB 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="73c15-117">Select your Cosmos DB account.</span></span>
4. <span data-ttu-id="73c15-118">Hello 새 창에서 클릭 **데이터 탐색기 (미리 보기)** hello 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73c15-118">In hello new window, click **Data Explorer (Preview)** in hello navigation menu.</span></span>
5. <span data-ttu-id="73c15-119">Hello 새 창에서 데이터베이스와 컨테이너를 확장 한 다음 클릭 **배율 및 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="73c15-119">In hello new window, expand your database and container and then click **Scale & Settings**.</span></span>
6. <span data-ttu-id="73c15-120">Hello 새 창에서 hello에 hello 새 처리량 값을 입력 **처리량** 상자를 선택한 다음 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="73c15-120">In hello new window, type hello new throughput value in hello **Throughput** box, and then click **Save**.</span></span>

<a id="set-throughput-sdk"></a>

## <a name="tooset-hello-throughput-by-using-hello-documentdb-api-for-net"></a><span data-ttu-id="73c15-121">.NET 용 hello DocumentDB API를 사용 하 여 tooset hello 처리량</span><span class="sxs-lookup"><span data-stu-id="73c15-121">tooset hello throughput by using hello DocumentDB API for .NET</span></span>

```C#
//Fetch hello resource toobe updated
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set hello throughput toohello new value, for example 12,000 request units per second
offer = new OfferV2(offer, 12000);

//Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offer);
```

## <a name="throughput-faq"></a><span data-ttu-id="73c15-122">처리량 FAQ</span><span class="sxs-lookup"><span data-stu-id="73c15-122">Throughput FAQ</span></span>

<span data-ttu-id="73c15-123">**내 처리량 tooless 400RU/s 보다를 설정할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="73c15-123">**Can I set my throughput tooless than 400 RU/s?**</span></span>

<span data-ttu-id="73c15-124">400RU/s는 hello 최소 처리량 (2500 000RU/s는 분할 된 컬렉션에 대 한 최소 hello) Cosmos DB 단일 파티션 컬렉션에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73c15-124">400 RU/s is hello minimum throughput available on Cosmos DB single partition collections (2500 RU/s is hello minimum for partitioned collections).</span></span> <span data-ttu-id="73c15-125">단위 000RU/s 간격 100 개에 설정 되어 있지만 처리량 설정할 수 없습니다 too100 000RU/s 이나 값 400RU/s 보다 작은 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="73c15-125">Request units are set in 100 RU/s intervals, but throughput cannot be set too100 RU/s or any value smaller than 400 RU/s.</span></span> <span data-ttu-id="73c15-126">비용 효율적인 메서드 toodevelop 찾고 Cosmos DB를 테스트 하는 경우 무료 hello를 사용할 수 있습니다 [Azure Cosmos DB 에뮬레이터](local-emulator.md), 비용 없이 로컬로 배포할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="73c15-126">If you're looking for a cost effective method toodevelop and test Cosmos DB, you can use hello free [Azure Cosmos DB Emulator](local-emulator.md), which you can deploy locally at no cost.</span></span> 

<span data-ttu-id="73c15-127">**Hello MongoDB API를 사용 하 여 througput를 설정 하려면 어떻게 해야 합니까?**</span><span class="sxs-lookup"><span data-stu-id="73c15-127">**How do I set througput using hello MongoDB API?**</span></span>

<span data-ttu-id="73c15-128">MongoDB API 확장 tooset 처리량 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="73c15-128">There's no MongoDB API extension tooset throughput.</span></span> <span data-ttu-id="73c15-129">hello 좋습니다 toouse hello DocumentDB API와 같이 [.NET에 대 한 hello DocumentDB API를 사용 하 여 tooset hello 처리량](#set-throughput-sdk)합니다.</span><span class="sxs-lookup"><span data-stu-id="73c15-129">hello recommendation is toouse hello DocumentDB API, as shown in [tooset hello throughput by using hello DocumentDB API for .NET](#set-throughput-sdk).</span></span>

## <a name="next-steps"></a><span data-ttu-id="73c15-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="73c15-130">Next steps</span></span>

<span data-ttu-id="73c15-131">프로 비전 및 Cosmos DB와 함께 진행 중인 지구 단위에 대해 자세히 toolearn 참조 [분할과 Cosmos DB와 함께 크기 조정](partition-data.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="73c15-131">toolearn more about provisioning and going planet-scale with Cosmos DB, see [Partitioning and scaling with Cosmos DB](partition-data.md).</span></span>
