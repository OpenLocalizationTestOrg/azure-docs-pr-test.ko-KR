---
title: "Azure CosmosDB: 분당 요청 단위(RU/m) | Microsoft Docs"
description: "분당 요청 단위를 활용하여 비용을 절감하는 방법을 알아봅니다."
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 72d60d5656ad664e42a848fc9b372cb09e49b888
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="request-units-per-minute-in-azure-cosmos-db"></a><span data-ttu-id="d018f-103">Azure Cosmos DB의 분당 요청 단위</span><span class="sxs-lookup"><span data-stu-id="d018f-103">Request units per minute in Azure Cosmos DB</span></span>

<span data-ttu-id="d018f-104">Azure Cosmos DB는 신속하고 예측 가능한 성능을 얻을 수 있고, 응용 프로그램 증가에 따라 효율적인 확장이 가능하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-104">Azure Cosmos DB is designed to help you achieve a fast, predictable performance and scale seamlessly along with your application’s growth.</span></span> <span data-ttu-id="d018f-105">초당 및 분당(RU/m) 단위 모두에서 Cosmos DB 컨테이너의 처리량을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-105">You can provision throughput on a Cosmos DB container at both, per-second and at per-minute (RU/m) granularities.</span></span> <span data-ttu-id="d018f-106">분당 단위로 프로비전된 처리량은 초당 단위로 발생하는 워크로드가 예기치 않게 급증하는 경우를 관리하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-106">The provisioned throughput at per-minute granularity is used to manage unexpected spikes in the workload occurring at a per-second granularity.</span></span> 

<span data-ttu-id="d018f-107">이 문서에서는 분당(RU/m) 요청 단위의 프로비전이 작동하는 방법에 대한 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-107">This article provides an overview of how the provisioning of Request Unit per Minute (RU/m) works.</span></span> <span data-ttu-id="d018f-108">예측할 수 없는 요구(특히 실행 데이터를 기반으로 분석을 실행해야 하는 경우) 및 급증하는 워크로드에 예측 가능한 성능을 제공하기 위해 RU/m을 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-108">The goal in mind with provisioning of RU/m is to provide a predictable performance around unpredictable needs (especially if you need to run analytics on top of your operational data) and spiky workloads.</span></span> <span data-ttu-id="d018f-109">고객이 편안하고 신속하게 확장할 수 있도록 프로비전에 더 많은 처리량을 사용할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-109">We want to have our customers consume more the throughput they provision so they can scale quickly with peace of mind.</span></span>

<span data-ttu-id="d018f-110">이 문서를 읽은 다음에는 다음과 같은 질문에 답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-110">After reading this article, you will be able to answer the following questions:</span></span>

* <span data-ttu-id="d018f-111">분당 요청 단위는 어떻게 작동하나요?</span><span class="sxs-lookup"><span data-stu-id="d018f-111">How does a Request Unit per Minute work?</span></span>
* <span data-ttu-id="d018f-112">분당 요청 단위 및 초당 요청 단위 간의 차이는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="d018f-112">What is the difference between Request Unit per Minute and Request Unit per Second?</span></span>
* <span data-ttu-id="d018f-113">RU/m을 프로비전하는 방법은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="d018f-113">How to provision RU/m?</span></span>
* <span data-ttu-id="d018f-114">어떤 시나리오에서 분당 요청 단위를 프로비전하는 것이 좋은가요?</span><span class="sxs-lookup"><span data-stu-id="d018f-114">Under which scenario shall I consider provisioning Request Unit per Minute?</span></span>
* <span data-ttu-id="d018f-115">비용과 성능을 최적화하도록 포털 메트릭을 사용하는 방법은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="d018f-115">How to use the portal metrics to optimize my cost and performance?</span></span>
* <span data-ttu-id="d018f-116">어떤 종류의 요청에서 RU/m 예산을 소비할 수 있는지 정의하나요?</span><span class="sxs-lookup"><span data-stu-id="d018f-116">Define which type of request can consume your RU/m budget?</span></span>

## <a name="provisioning-request-units-per-minute-rum"></a><span data-ttu-id="d018f-117">분당 요청 단위(RU/m) 프로비전</span><span class="sxs-lookup"><span data-stu-id="d018f-117">Provisioning request units per minute (RU/m)</span></span>

<span data-ttu-id="d018f-118">두 번째 단위(RU/s)에서 Azure Cosmos DB를 프로비전할 때 처리량이 지정된 시간(초) 이내에 프로비전된 용량을 초과하지 않은 경우 요청이 짧은 대기 시간 동안 성공한다고 보증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-118">When you provision Azure Cosmos DB at the second granularity (RU/s), you get the guarantee that your request succeeds at a low latency if your throughput has not exceeded the capacity provisioned within that second.</span></span> <span data-ttu-id="d018f-119">RU/m에서 단위는 해당 시간(분) 이내에 요청이 성공한다고 보증하는 시간(분)입니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-119">With RU/m, the granularity is at the minute with the guarantee that your request succeeds within that minute.</span></span> <span data-ttu-id="d018f-120">버스팅 시스템에 비해 얻게 되는 성능은 예측할 수 있으며 이를 기반으로 사용자가 계획할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-120">Compared to bursting systems, we make sure that the performance you get is predictable and you can plan on it.</span></span>

<span data-ttu-id="d018f-121">분당 프로비전이 작동하는 방법은 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-121">The way per minute provisioning works is simple:</span></span>

* <span data-ttu-id="d018f-122">RU/s 외에도 RU/m의 경우 매시간 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-122">RU/m is billed hourly and in addition to RU/s.</span></span> <span data-ttu-id="d018f-123">자세한 내용은 Azure Cosmos DB [가격 책정 페이지](https://aka.ms/acdbpricing)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="d018f-123">For more details, please visit Azure Cosmos DB [pricing page](https://aka.ms/acdbpricing).</span></span>
* <span data-ttu-id="d018f-124">RU/m은 컬렉션 수준에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-124">RU/m can be enabled at collection level.</span></span> <span data-ttu-id="d018f-125">SDK(Node.js, Java 또는 .Net)를 통하거나 포털(MongoDB API 워크로드도 포함)을 통해 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-125">That can be done through the SDKs (Node.js, Java, or .Net) or through the portal (also include MongoDB API workloads)</span></span>
* <span data-ttu-id="d018f-126">RU/m을 사용하는 경우 100RU/s가 프로비전될 때마다 1,000RU/m이 프로비전됩니다(10배 비율).</span><span class="sxs-lookup"><span data-stu-id="d018f-126">When RU/m is enabled, for every 100 RU/s provisioned, you also get 1,000 RU/m provisioned (the ratio is 10x)</span></span>
* <span data-ttu-id="d018f-127">요청 단위는 지정된 시간(초) 이내에 분당 프로비전을 초과한 경우에만 지정된 시간(초)에서 RU/m 프로비전을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-127">At a given second, a request unit consumes your RU/m provisioning only if you have exceeded your per second provisioning within that second</span></span>
* <span data-ttu-id="d018f-128">60초(UTC)가 종료되면 분당 프로비전이 다시 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-128">Once the 60-second period (UTC) ends, the per minute provisioning is refilled</span></span>
* <span data-ttu-id="d018f-129">RU/m은 파티션당 최대 5,000RU/s로 프로비전된 컬렉션에 대해서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-129">RU/m can be enabled only for collections with a maximum provisioning of 5,000 RU/s per partition.</span></span> <span data-ttu-id="d018f-130">처리량 요구 사항을 확장하고 높은 수준의 파티션당 프로비전을 사용한 경우 경고 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-130">If you scale your throughput needs and have such a high level of provisioning per partition, you will get a warning message</span></span>

<span data-ttu-id="d018f-131">아래에서는 구체적인 예로 고객이 100kRU/m인 10kRU/s를 프로비전합니다. 그러면 100,000RU/m인 10,000RU/s을 프로비전한 컬렉션에서 90초 동안 최대(50kRU/s) 프로비전에 대한 비용의 73%를 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-131">Below is a concrete example, in which a customer can provision 10kRU/s with 100kRU/m, saving 73% in cost against provisioning for peak (at 50kRU/sec) through a 90-second period on a collection that has 10,000 RU/s and 100,000 RU/m provisioned:</span></span>

* <span data-ttu-id="d018f-132">1초: RU/m 예산은 100,000으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-132">1st second: The RU/m budget is set at 100,000</span></span>
* <span data-ttu-id="d018f-133">3초: 해당 시간(초) 동안 소비하는 요청 단위는 11,010RU입니다. RU/s를 초과하는 1,010RU가 프로비전됩니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-133">3rd second: During that second the consumption of Request Unit was 11,010 RUs, 1,010 RUs above the RU/s provisioning.</span></span> <span data-ttu-id="d018f-134">따라서 1,010RU는 RU/m 예산에서 차감됩니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-134">Therefore, 1,010 RUs are deducted from the RU/m budget.</span></span> <span data-ttu-id="d018f-135">다음 57초 동안 RU/m 예산 중에 98,990RU를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-135">98,990 RUs are available for the next 57 seconds in the RU/m budget</span></span>
* <span data-ttu-id="d018f-136">29초: 해당 시간(초) 동안 급등이 발생(초당 프로비전보다 >4x 높음)했고 소비하는 요청 단위는 46,920RU였습니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-136">29th second: During that second, a large spike happened (>4x higher than provisioning per second) and the consumption of Request Unit was 46,920 RUs.</span></span> <span data-ttu-id="d018f-137">92,323RU(28초)에서 55,403RU(29초)로 떨어진 RU/m 예산에서 36,920RU가 차감됩니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-137">36,920 RUs are deducted from the RU/m budget that dropped from 92,323 RUs (28th second) to 55,403 RUs (29th second)</span></span>
* <span data-ttu-id="d018f-138">61초: RU/m 예산이 100,000RU로 다시 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-138">61st second: RU/m budget is set back to 100,000 RUs.</span></span>
 
![Azure Cosmos DB의 사용 및 프로비전을 보여 주는 그래프](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute.png)

## <a name="specifying-request-unit-capacity-with-rum"></a><span data-ttu-id="d018f-140">RU/m을 사용하여 요청 단위 용량 지정</span><span class="sxs-lookup"><span data-stu-id="d018f-140">Specifying request unit capacity with RU/m</span></span>

<span data-ttu-id="d018f-141">Azure Cosmos DB 컬렉션을 만들 때 컬렉션에 대해 예약하려는 초당 요청 단위 수(RU/s)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-141">When creating an Azure Cosmos DB collection, you specify the number of request units per second (RU per second) you want reserved for the collection.</span></span> <span data-ttu-id="d018f-142">RU/m을 추가할지를 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-142">You can also decide if you want to add RU per minute.</span></span> <span data-ttu-id="d018f-143">포털 또는 SDK를 통해 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-143">This can be done through the Portal or the SDK.</span></span> 

### <a name="through-the-portal"></a><span data-ttu-id="d018f-144">포털을 통해</span><span class="sxs-lookup"><span data-stu-id="d018f-144">Through the Portal</span></span>

<span data-ttu-id="d018f-145">분당 RU를 활성화 또는 비활성화하려면 컬렉션을 프로비전할 때 클릭해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-145">Enabling or disabling RU per minute simply requires a click when provisioning a collection.</span></span> 

 ![Azure Portal에서 RU/m 설정 방법을 보여 주는 스크린샷](./media/request-units-per-minute/azure-cosmos-db-request-unit-per-minute-portal.png)

### <a name="through-the-sdk"></a><span data-ttu-id="d018f-147">SDK를 통해</span><span class="sxs-lookup"><span data-stu-id="d018f-147">Through the SDK</span></span>
<span data-ttu-id="d018f-148">먼저 다음 SDK에만 RU/m을 사용할 수 있다는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-148">First, this is important to note that RU/m is only available for the following SDKs:</span></span>

* <span data-ttu-id="d018f-149">.Net 1.14.0</span><span class="sxs-lookup"><span data-stu-id="d018f-149">.Net 1.14.0</span></span>
* <span data-ttu-id="d018f-150">Java 1.11.0</span><span class="sxs-lookup"><span data-stu-id="d018f-150">Java 1.11.0</span></span>
* <span data-ttu-id="d018f-151">Node.js 1.12.0</span><span class="sxs-lookup"><span data-stu-id="d018f-151">Node.js 1.12.0</span></span>
* <span data-ttu-id="d018f-152">Python 2.2.0</span><span class="sxs-lookup"><span data-stu-id="d018f-152">Python 2.2.0</span></span>

<span data-ttu-id="d018f-153">.NET SDK를 사용하여 3,000RU/s 및 30,000RU/m인 컬렉션을 만들기 위한 코드 조각은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-153">Here is a code snippet for creating a collection with 3,000 request units per second and 30,000 request units per minute using the .NET SDK:</span></span>

```csharp
// Create a collection with RU/m enabled
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

// Set the throughput to 3,000 request units per second which will give you 30,000 request units per minute as the RU/m budget
await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000, OfferEnableRUPerMinuteThroughput = true });
```

<span data-ttu-id="d018f-154">다음 코드 조각에서는 .NET SDK를 사용하여 RU/m을 프로비전하지 않고 컬렉션 처리량을 5,000RU/s로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-154">Here is a code snippet for changing the throughput of a collection to 5,000 request units per second without provisioning RU per minute using the .NET SDK:</span></span>

```csharp
// Get the current offer
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set the throughput to 5000 request units per second without RU/m enabled (the last parameter to OfferV2 constructor below)
OfferV2 offerV2 = new OfferV2(offer, 5000, false);

// Now persist these changes to the database by replacing the original resource
await client.ReplaceOfferAsync(offerV2);
```

## <a name="good-fit-scenarios"></a><span data-ttu-id="d018f-155">적합한 시나리오</span><span class="sxs-lookup"><span data-stu-id="d018f-155">Good fit scenarios</span></span>

<span data-ttu-id="d018f-156">이 섹션에서는 RU/m을 사용하기 위해 적합한 시나리오의 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-156">In this section, we provide an overview of scenarios that are a good fit for enabling request units per minute.</span></span>

<span data-ttu-id="d018f-157">**개발/테스트 환경:** 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-157">**Dev/Test environment:** Good fit.</span></span> <span data-ttu-id="d018f-158">개발 단계에서 다른 워크로드를 사용하여 응용 프로그램을 테스트하는 경우 RU/m은 이 단계에서 유연성을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-158">During the development stage, if you are testing your application with different workloads, RU/m can provide the flexibility at this stage.</span></span> <span data-ttu-id="d018f-159">반면 [에뮬레이터](local-emulator.md)는 추가 비용 없이 Azure Cosmos DB를 테스트할 수 있는 유용한 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-159">While the [emulator](local-emulator.md) is a great free tool to test Azure Cosmos DB.</span></span> <span data-ttu-id="d018f-160">그러나 클라우드 환경에서 시작하려는 경우 임시 성능 요구 사항에 맞게 RU/m에 뛰어난 유연성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-160">However if you want to start in a cloud environment, you will have a great flexibility with RU/m for your adhoc performance needs.</span></span> <span data-ttu-id="d018f-161">처음에는 성능 요구 사항에 대해 염려하지 않고 개발하는 데 많은 시간을 투자합니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-161">You will spend more time developing, less worrying about performance needs at first.</span></span> <span data-ttu-id="d018f-162">최소 RU/s를 프로비전하여 시작하고 RU/m을 사용하도록 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-162">We recommend starting with the minimum RU/s provisioning and enable RU/m.</span></span>

<span data-ttu-id="d018f-163">**예측할 수 없고 급증하는 분 단위 요구 사항:** 적합 – 비용 절감: 25-75%.</span><span class="sxs-lookup"><span data-stu-id="d018f-163">**Unpredictable, spiky, minute granularity needs:** Good fit – Savings: 25-75%.</span></span> <span data-ttu-id="d018f-164">RU/m이 크게 개선되었고 대부분의 프로덕션 시나리오가 해당 그룹에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-164">We have seen large improvement from RU/m and most production scenarios are into that group.</span></span> <span data-ttu-id="d018f-165">IoT 워크로드가 몇 분 동안 여러 번 급증하는 경우, 시스템에서 동시에 대량 삽입을 수행할 때 쿼리가 실행되는 경우, 급증하는 요구 사항을 처리하기 위한 추가 용량이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-165">If you have an IoT workload that has spike a few times in a minute, if you have queries running when your system makes mass insert at the same time, you will need extra capacity for handeling spiky needs.</span></span> <span data-ttu-id="d018f-166">아래의 단계별 접근 방식을 적용하여 리소스 요구 사항을 최적화하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-166">We recommend optimizing your resource needs by applying our step by step approach below.</span></span>

 ![5분 단위로 요청 사용을 보여 주는 그래프](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-consumption.png)
 
 <span data-ttu-id="d018f-168">*그림 - RU 사용 벤치마크*</span><span class="sxs-lookup"><span data-stu-id="d018f-168">*Figure - RU consumption benchmark*</span></span>

<span data-ttu-id="d018f-169">**편안함:** 적합 – 비용 절감: 10-20%.</span><span class="sxs-lookup"><span data-stu-id="d018f-169">**Peace of mind:** Good fit – Savings: 10-20%.</span></span> <span data-ttu-id="d018f-170">잠재적인 급증 및 제한에 대해 염려하지 않고 싶으신가요?</span><span class="sxs-lookup"><span data-stu-id="d018f-170">Sometimes, you just want to have peace of mind and not worry about potential peaks and throttling.</span></span> <span data-ttu-id="d018f-171">이 기능이 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-171">This feature is the right one for you.</span></span> <span data-ttu-id="d018f-172">이 경우에 RU/m을 사용하도록 설정하고 초당 프로비전을 약간 낮추는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-172">In that case, we recommend enabling RU/m and slightly lower your per second provisioning.</span></span> <span data-ttu-id="d018f-173">프로비전을 적극적으로 최적화하려고 하지 않기 때문에 이 경우는 위에서 설명한 경우와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-173">This case is different from the above as you will not try to optimize aggressively your provisioning.</span></span> <span data-ttu-id="d018f-174">오히려 사용 중인 "0 제한"에 가깝습니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-174">This is more of a “Zero Throttling” mindset you are in.</span></span>

<span data-ttu-id="d018f-175">임시 요구 사항을 포함한 주요 작업: 경우에 따라 임시 작업 또는 중요하지 않은 작업에서 예산을 사용하지 않도록 주요 작업만 RU/m 예산에 액세스할 수 있게 허용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-175">Critical operations with adhoc needs: We sometimes recommend to only let critical operations access RU/m budget so the budget doesn’t get consume by adhoc or less important operations.</span></span> <span data-ttu-id="d018f-176">이는 아래 섹션에서 쉽게 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-176">That can be easily defined in the section below.</span></span>

## <a name="using-the-portal-metrics-to-optimize-cost-and-performance"></a><span data-ttu-id="d018f-177">비용과 성능을 최적화하도록 포털 메트릭 사용</span><span class="sxs-lookup"><span data-stu-id="d018f-177">Using the portal metrics to optimize cost and performance</span></span>

<span data-ttu-id="d018f-178">**몇 주 이내에 처리량 요구를 최적화하기 위해 RU/m 사용을 모니터링하는 콘텐츠가 더 발전될 예정입니다.**</span><span class="sxs-lookup"><span data-stu-id="d018f-178">**In the coming weeks, we will further develop the content around monitoring RUs minute consumption to optimize your throughput needs.**</span></span>

<span data-ttu-id="d018f-179">포털 메트릭을 통해 RU/m에 대해 사용하는 일반적인 RU/s의 양을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-179">Through the portal metrics, you can see how much of regular RU seconds you consume versus RU minutes.</span></span> <span data-ttu-id="d018f-180">이러한 메트릭을 모니터링하면 프로비전을 최적화하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-180">Monitoring these metrics should help you optimize your provisioning.</span></span> 

<span data-ttu-id="d018f-181">사용자에게 이익이 되도록 RU/m을 사용하는 방법에 대한 단계별 접근 방식을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-181">We recommend a step by step approach on how to use RU/m to your advantage.</span></span> <span data-ttu-id="d018f-182">각 단계에서 워크로드(시간, 일 심지어 주일 수 있음)의 전체 주기를 나타내는 RU 사용의 개요를 보고 프로비전한 부분을 활용하는 방법에 대한 통찰력을 얻어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-182">For each step, you should have an overview of the RU consumption representing a full cycle of your workload (it could be hours, days, or even weeks) and get insights on the utilization of what you provision.</span></span>

<span data-ttu-id="d018f-183">이 방법을 사용하는 원칙은 아래 성능 조건과 일치하는 프로비전 지점에 최대한 가깝게 처리량을 프로비전하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-183">The principle behind this approach is to make your throughput provisioning as close as possible to a provisioning point that matches your performance criteria below.</span></span> 

![5분 단위로 요청 사용을 보여 주는 그래프](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-adjust-provisioning.png)
 
<span data-ttu-id="d018f-185">워크로드에 대한 최적의 프로비전 지점을 이해하려면 다음 항목을 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-185">To understand the optimal provisioning point for your workload, you need to understand:</span></span>

* <span data-ttu-id="d018f-186">소비 패턴: 아니요, 자주 사용하지 않거나 지속적으로 급증하나요?</span><span class="sxs-lookup"><span data-stu-id="d018f-186">Consumption patterns: no, infrequent or sustained spikes?</span></span> <span data-ttu-id="d018f-187">작은(평균 2배), 중간 또는 크게(평균 10배 이상) 급증하나요?</span><span class="sxs-lookup"><span data-stu-id="d018f-187">Small (2x average), medium, or large (>10x average) spikes?</span></span>
* <span data-ttu-id="d018f-188">제한된 요청 백분율: 약간의 제한이 있는 경우에도 편하게 생각하나요?</span><span class="sxs-lookup"><span data-stu-id="d018f-188">Percent of throttled requests: do you feel comfortable if you have a bit of throttling?</span></span> <span data-ttu-id="d018f-189">그렇다면, 얼마나 그런가요?</span><span class="sxs-lookup"><span data-stu-id="d018f-189">If so, by how much?</span></span> 

<span data-ttu-id="d018f-190">목표를 식별하면 최적의 프로비전에 가까워질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-190">Once you have identified what your goals are, you will be able to get closer to the optimal provisioning.</span></span>

<span data-ttu-id="d018f-191">사용자를 돕기 위해 RU/m 사용에 따라 프로비전을 최적화하는 방법에 대한 전반적인 지침을 제공하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-191">To assist you, we want to provide an overall guidance on how to optimize your provisioning based on your RU/m consumption.</span></span> <span data-ttu-id="d018f-192">이 설명서는 모든 종류의 워크로드에 적용되지 않지만 비공개 미리 보기 정보를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-192">This guidance doesn’t apply to all kind of workloads but is based on the private preview knowledge.</span></span> <span data-ttu-id="d018f-193">자세히 알아보면 이러한 기준을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-193">We might change such baselines as we learn more:</span></span>

|<span data-ttu-id="d018f-194">RU/m % 사용률</span><span class="sxs-lookup"><span data-stu-id="d018f-194">RU/m % utilization</span></span>|<span data-ttu-id="d018f-195">RU/m의 사용률 수준</span><span class="sxs-lookup"><span data-stu-id="d018f-195">Degree of utilization of RU/m</span></span>|<span data-ttu-id="d018f-196">프로비전하기 위해 권장되는 작업</span><span class="sxs-lookup"><span data-stu-id="d018f-196">Recommended actions for provisioning</span></span>|
|---|---|---|
|<span data-ttu-id="d018f-197">0-1%</span><span class="sxs-lookup"><span data-stu-id="d018f-197">0-1%</span></span>|<span data-ttu-id="d018f-198">과소 사용률</span><span class="sxs-lookup"><span data-stu-id="d018f-198">Under utilization</span></span>|<span data-ttu-id="d018f-199">더 많은 RU/m을 사용하는 낮은 RU/s</span><span class="sxs-lookup"><span data-stu-id="d018f-199">Lower RU/s to consume more RU/m</span></span>|
|<span data-ttu-id="d018f-200">1-10%</span><span class="sxs-lookup"><span data-stu-id="d018f-200">1-10%</span></span>|<span data-ttu-id="d018f-201">정상 사용</span><span class="sxs-lookup"><span data-stu-id="d018f-201">Healthy use</span></span>|<span data-ttu-id="d018f-202">동일한 프로비전 수준 유지</span><span class="sxs-lookup"><span data-stu-id="d018f-202">Keep the same provisioning level</span></span>|
|<span data-ttu-id="d018f-203">10% 이상</span><span class="sxs-lookup"><span data-stu-id="d018f-203">Above 10%</span></span>|<span data-ttu-id="d018f-204">과도 사용률</span><span class="sxs-lookup"><span data-stu-id="d018f-204">Over utilization</span></span>|<span data-ttu-id="d018f-205">RU/s를 증가시켜 RU/m 사용 감소</span><span class="sxs-lookup"><span data-stu-id="d018f-205">Increase RU/s to rely less on RU/m</span></span>|

## <a name="select-which-operations-can-consume-the-rum-budget"></a><span data-ttu-id="d018f-206">RU/m 예산을 사용할 수 있는 작업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-206">Select which operations can consume the RU/m budget</span></span>

<span data-ttu-id="d018f-207">요청 수준에서 RU/m 예산을 활성화/비활성화하여 작업 형식에 관계 없이 요청을 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-207">At request level, you can also enable/disable RU/m budget to serve the request irrespective of operation type.</span></span> <span data-ttu-id="d018f-208">일반적으로 프로비전된 RU/s 예산을 사용하고 요청이 RU/m 예산을 사용할 수 없는 경우 이 요청이 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-208">If regular provisioned RUs/sec budget is consumed and the request cannot consume the RU/m budget, this request will be throttled.</span></span> <span data-ttu-id="d018f-209">RU/m 처리량 예산이 활성화된 경우 기본적으로 모든 요청은 RU/m 예산에서 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-209">By default, any request is served by RU/m budget if RU/m throughput budget is activated.</span></span> 

<span data-ttu-id="d018f-210">CRUD 및 쿼리 작업에 DocumentDB API를 사용하여 RU/m 예산을 비활성화하기 위한 코드 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-210">Here is a code snippet for disabling RU/m budget using the DocumentDB API for CRUD and query operations.</span></span>

```csharp
// In order to disable any CRUD request for RU/m, set DisableRUPerMinuteUsage to true in RequestOptions
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    new Document { Id = "Cosmos DB" },
    new RequestOptions { DisableRUPerMinuteUsage = true });
// In order to disable any query request for RU/m, set DisableRUPerMinuteOnRequest to true in RequestOptions
FeedOptions feedOptions = new FeedOptions();
feedOptions.DisableRUPerMinuteUsage = true;
var query = client.CreateDocumentQuery<Book>(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    "select * from c",feedOptions).AsDocumentQuery();
```

## <a name="next-steps"></a><span data-ttu-id="d018f-211">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d018f-211">Next steps</span></span>

<span data-ttu-id="d018f-212">이 문서에서는 Azure Cosmos DB에서 분할이 작동하는 방식, 분할된 컬렉션을 만드는 방법 및 응용 프로그램에 적합한 파티션 키를 선택하는 방법을 설명했습니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-212">In this article, we've described how partitioning works in Azure Cosmos DB, how you can create partitioned collections, and how you can pick a good partition key for your application.</span></span>

* <span data-ttu-id="d018f-213">Azure Cosmos DB를 사용하여 규모 및 성능 테스트를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-213">Perform scale and performance testing with Azure Cosmos DB.</span></span> <span data-ttu-id="d018f-214">샘플에 대해서는 [Azure Cosmos DB를 사용한 성능 및 규모 테스트](performance-testing.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d018f-214">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) for a sample.</span></span>
* <span data-ttu-id="d018f-215">[SDK](documentdb-sdk-dotnet.md) 또는 [REST API](/rest/api/documentdb/)를 사용하여 코딩을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d018f-215">Get started coding with the [SDKs](documentdb-sdk-dotnet.md) or the [REST API](/rest/api/documentdb/).</span></span>
* <span data-ttu-id="d018f-216">Azure Cosmos DB에서 [프로비전된 처리량](request-units.md)에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="d018f-216">Learn about [provisioned throughput](request-units.md) in Azure Cosmos DB</span></span> 

