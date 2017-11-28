---
title: "aaaCloud 크루저 및 Microsoft Azure 청구 API 통합 | Microsoft Docs"
description: "Microsoft Azure 청구 파트너 클라우드 크루저에 hello Azure 청구 Api가 제품에 통합 경험에서에서 한 고유한 관점을 제공 합니다.  Microsoft Azure 팩용 Cloud Cruiser를 사용/시도하는 데 관심을 두는 Azure 및 Cloud Cruiser 고객에게 특히 유용합니다."
services: 
documentationcenter: 
author: BryanLa
manager: tonguyen
editor: 
tags: billing
ms.assetid: b65128cf-5d4d-4cbd-b81e-d3dceab44271
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 02/03/2017
ms.author: mobandyo;sirishap;bryanla
ms.openlocfilehash: 74cc19bdeed26c6684210736caa0cb365e8f8821
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-cruiser-and-microsoft-azure-billing-api-integration"></a><span data-ttu-id="e6037-104">클라우드 크루저 및 Microsoft Azure 청구 API 통합</span><span class="sxs-lookup"><span data-stu-id="e6037-104">Cloud Cruiser and Microsoft Azure Billing API Integration</span></span>
<span data-ttu-id="e6037-105">이 문서에서는 워크플로에 대 한 클라우드 크루저에서 새 Microsoft Azure 청구 Api를 사용할 수 있지만 hello에서 수집 된 hello 정보 시뮬레이션 및 분석 비용 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-105">This article describes how hello information collected from hello new Microsoft Azure Billing APIs can be used in Cloud Cruiser for workflow cost simulation and analysis.</span></span>

## <a name="azure-ratecard-api"></a><span data-ttu-id="e6037-106">Azure RateCard API</span><span class="sxs-lookup"><span data-stu-id="e6037-106">Azure RateCard API</span></span>
<span data-ttu-id="e6037-107">hello RateCard API는 Azure에서 환율 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-107">hello RateCard API provides rate information from Azure.</span></span> <span data-ttu-id="e6037-108">Hello 적절 한 자격 증명을 인증 후 프로그램을 제공 id.와 관련 된 hello 속도 함께 Azure에서 사용할 수 있는 hello 서비스에 대 한 hello API toocollect 메타 데이터를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-108">After authenticating with hello proper credentials, you can query hello API toocollect metadata about hello services available on Azure, along with hello rates associated with your Offer ID.</span></span>

<span data-ttu-id="e6037-109">hello 다음은 샘플 응답 (Windows) A0 hello에 대 한 hello 가격을 표시 하는 hello API에서 인스턴스:</span><span class="sxs-lookup"><span data-stu-id="e6037-109">hello following is a sample response from hello API showing hello prices for hello A0 (Windows) instance:</span></span>

    {
        "MeterId": "0e59ad56-03e5-4c3d-90d4-6670874d7e29",
        "MeterName": "Compute Hours",
        "MeterCategory": "Virtual Machines",
        "MeterSubCategory": "A0 VM (Windows)",
        "Unit": "Hours",
        "MeterRates":
        {
            "0": 0.029
        },
        "EffectiveDate": "2014-08-01T00:00:00Z",
        "IncludedQuantity": 0.0,
        "MeterStatus": "Active"
    },

### <a name="cloud-cruisers-interface-tooazure-ratecard-api"></a><span data-ttu-id="e6037-110">클라우드 크루저의 인터페이스 tooAzure RateCard API</span><span class="sxs-lookup"><span data-stu-id="e6037-110">Cloud Cruiser’s Interface tooAzure RateCard API</span></span>
<span data-ttu-id="e6037-111">클라우드 크루저 다양 한 방식에서 hello RateCard API 정보를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-111">Cloud Cruiser can leverage hello RateCard API information in different ways.</span></span> <span data-ttu-id="e6037-112">이 문서에 대 한 사용된 toomake IaaS 작업 부하 비용 시뮬레이션 및 분석 수 있는 방법을 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-112">For this article, we will show how it can be used toomake IaaS workload cost simulation and analysis.</span></span>

<span data-ttu-id="e6037-113">toodemonstrate 이러한 대/소문자를 사용 하 여 응용 프로그램, 작업 부하에서 Microsoft Azure 팩 WAP ()를 실행 하는 여러 인스턴스를 가정해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-113">toodemonstrate this use case, imagine a workload of several instances running on Microsoft Azure Pack (WAP).</span></span> <span data-ttu-id="e6037-114">hello 목표는 toosimulate에서 Azure 및 이러한 마이그레이션을 수행 하는 추정 hello 비용의 이와 같은 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-114">hello goal is toosimulate this same workload on Azure, and estimate hello costs of doing such migration.</span></span> <span data-ttu-id="e6037-115">순서로 toocreate이이 시뮬레이션을 수행 하는 두 가지 주요 작업 toobe:</span><span class="sxs-lookup"><span data-stu-id="e6037-115">In order toocreate this simulation, there are two main tasks toobe performed:</span></span>

1. <span data-ttu-id="e6037-116">**가져오기 및 프로세스 hello 서비스 정보 hello RateCard API에서에서 수집된 합니다.**</span><span class="sxs-lookup"><span data-stu-id="e6037-116">**Import and process hello service information collected from hello RateCard API.**</span></span> <span data-ttu-id="e6037-117">이 작업은 여기서 hello RateCard API에서에서 hello 추출은 변환 되 고 게시 된 tooa 새 요금 계획 hello 통합 문서에도 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-117">This task is also performed on hello workbooks, where hello extract from hello RateCard API is transformed and published tooa new rate plan.</span></span> <span data-ttu-id="e6037-118">이 새 요금 계획 hello 시뮬레이션 tooestimate에 사용 될 Azure 가격 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-118">This new rate plan will be used on hello simulations tooestimate hello Azure prices.</span></span>
2. <span data-ttu-id="e6037-119">**IaaS에 대한 WAP 서비스 및 Azure 서비스 정규화.**</span><span class="sxs-lookup"><span data-stu-id="e6037-119">**Normalize WAP services and Azure services for IaaS.**</span></span> <span data-ttu-id="e6037-120">Azure 서비스가 인스턴스 크기(A0, A1, A2 등)에 기반한 반면 WAP 서비스는 기본적으로 개별 리소스(CPU, 메모리 크기, 디스크 크기 등)에 기반합니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-120">By default, WAP services are based on individual resources (CPU, Memory Size, Disk Size, etc.) while Azure services are based on instance size (A0, A1, A2, etc.).</span></span> <span data-ttu-id="e6037-121">이 첫 번째 작업은 클라우드 크루저 ETL 엔진에서 실행, 인스턴스 크기를 유사한 tooAzure 인스턴스 서비스에서 이러한 리소스 묶을 수 있는 통합 문서를 호출 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-121">This first task can be performed by Cloud Cruiser’s ETL engine, called workbooks, where these resources can be bundled on instance sizes, analogous tooAzure instance services.</span></span>

### <a name="import-data-from-hello-ratecard-api"></a><span data-ttu-id="e6037-122">Hello RateCard API에서에서 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="e6037-122">Import data from hello RateCard API</span></span>
<span data-ttu-id="e6037-123">클라우드 크루저 통합 문서는 hello RateCard API에서에서 자동화 된 방식이 toocollect 및 프로세스 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-123">Cloud Cruiser workbooks provide an automated way toocollect and process information from hello RateCard API.</span></span>  <span data-ttu-id="e6037-124">ETL (추출-변환-로드) 통합 문서를 사용 하면 tooconfigure hello 컬렉션, 변환 및 데이터 게시 hello 클라우드 크루저 데이터베이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-124">ETL (extract-transform-load) workbooks allow you tooconfigure hello collection, transformation, and publishing of data into hello Cloud Cruiser database.</span></span>

<span data-ttu-id="e6037-125">각 통합 문서 하나 또는 여러 개의 컬렉션이 서로 다른 소스 toocomplement에서 toocorrelate 정보를 허용 하거나 hello 사용 현황 데이터를 보강할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-125">Each workbook can have one or multiple collections, allowing you toocorrelate information from different sources toocomplement or augment hello usage data.</span></span> <span data-ttu-id="e6037-126">두 개의 스크린 샷을 표시 방법을 다음 hello 새 toocreate *컬렉션* 기존 통합 문서 및 hello에 정보를 가져오는 중에 *컬렉션* hello RateCard API에서에서:</span><span class="sxs-lookup"><span data-stu-id="e6037-126">hello following two screenshots show how toocreate a new *collection* in an existing workbook, and importing information into hello *collection* from hello RateCard API:</span></span>

<span data-ttu-id="e6037-127">![그림 1 - 새 컬렉션 만들기][1]</span><span class="sxs-lookup"><span data-stu-id="e6037-127">![Figure 1 - Creating a new collection][1]</span></span>

<span data-ttu-id="e6037-128">![그림 2-hello 새 컬렉션에서 데이터 가져오기][2]</span><span class="sxs-lookup"><span data-stu-id="e6037-128">![Figure 2 - Import data from hello new collection][2]</span></span>

<span data-ttu-id="e6037-129">가능한 toocreate hello 통합 문서에 hello 데이터를 가져온 후는 여러 단계 및 변환 프로세스, toomodify 및 모델 hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-129">After importing hello data into hello workbook, it’s possible toocreate multiple steps and transformation processes, toomodify and model hello data.</span></span> <span data-ttu-id="e6037-130">이 예제에 대 한 인프라-as a Service hello 변환 단계 tooremove 불필요 한 행 또는 레코드를 사용할 수 있습니다 (IaaS)에 관심이, 이후 IaaS 이외의 tooservices를 관련 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-130">For this example, since we are only interested in infrastructure-as-a-Service (IaaS) we can use hello transformation steps tooremove unnecessary rows, or records, related tooservices other than IaaS.</span></span>

<span data-ttu-id="e6037-131">hello 다음 스크린샷은 RateCard API에서 수집 된 tooprocess hello 데이터를 사용 하는 hello 변환 단계:</span><span class="sxs-lookup"><span data-stu-id="e6037-131">hello following screenshot shows hello transformation steps used tooprocess hello data collected from RateCard API:</span></span>

<span data-ttu-id="e6037-132">![그림 3-변환 RateCard API에서 데이터 수집 tooprocess 단계][3]</span><span class="sxs-lookup"><span data-stu-id="e6037-132">![Figure 3 - Transformation steps tooprocess collected data from RateCard API][3]</span></span>

### <a name="defining-new-services-and-rate-plans"></a><span data-ttu-id="e6037-133">새로운 서비스 및 요금제 정의</span><span class="sxs-lookup"><span data-stu-id="e6037-133">Defining New Services and Rate Plans</span></span>
<span data-ttu-id="e6037-134">클라우드 크루저에는 다양 한 방법 toodefine 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-134">There are different ways toodefine services on Cloud Cruiser.</span></span> <span data-ttu-id="e6037-135">Hello 옵션 중 하나는 hello 사용 현황 데이터에서 tooimport hello 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-135">One of hello options is tooimport hello services from hello usage data.</span></span> <span data-ttu-id="e6037-136">이 메서드는 hello 서비스 hello 공급자가 이미 정의 되어 있는 공용 클라우드를 사용할 때 일반적으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-136">This method is commonly used when working with public clouds, where hello services are already defined by hello provider.</span></span>

<span data-ttu-id="e6037-137">요금 계획의 집합이 적용 된 toodifferent 서비스를 유효한 날짜 또는 기타 옵션 중 고객 그룹을 기반 일 수 있는 가격 또는 속도입니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-137">A Rate Plan is a set of rates or prices that can be applied toodifferent services, based on effective dates, or group of customers, among other options.</span></span> <span data-ttu-id="e6037-138">요금 계획 클라우드 크루저 toocreate 시뮬레이션 또는 toounderstand, "what-if" 시나리오에 사용할 수도 있습니다 서비스에서 변경 작업의 총 비용 hello에 주는 영향입니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-138">Rate Plans can also be used on Cloud Cruiser toocreate simulation or “What-if” scenarios, toounderstand how changes in services can affect hello total cost of a workload.</span></span>

<span data-ttu-id="e6037-139">이 예제에서는 클라우드 크루저에 hello 서비스 정보 hello RateCard API toodefine 새로운 서비스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-139">In this example, we will use hello service information from hello RateCard API toodefine new services in Cloud Cruiser.</span></span> <span data-ttu-id="e6037-140">Hello 동일한 방식으로, 수 사용 하 여 관련 된 hello 속도 toohello toocreate 클라우드 크루저에 새 요금 계획 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-140">In hello same way, we can use hello rates associated toohello services toocreate a new Rate Plan on Cloud Cruiser.</span></span>

<span data-ttu-id="e6037-141">Hello 변환 프로세스의 hello 끝 가능한 toocreate 새 단계 이며 새 서비스와 속도 hello RateCard API의에서 hello 데이터를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-141">At hello end of hello transformation process, it is possible toocreate a new step and publish hello data from hello RateCard API as new services and rates.</span></span>

<span data-ttu-id="e6037-142">![그림 4-hello 데이터 hello RateCard API를에서 게시 하는 새로운 서비스와 속도][4]</span><span class="sxs-lookup"><span data-stu-id="e6037-142">![Figure 4 - Publishing hello data from hello RateCard API as new Services and Rates][4]</span></span>

### <a name="verify-azure-services-and-rates"></a><span data-ttu-id="e6037-143">Azure 서비스 및 요금 확인</span><span class="sxs-lookup"><span data-stu-id="e6037-143">Verify Azure Services and Rates</span></span>
<span data-ttu-id="e6037-144">Hello 서비스와 속도 게시 후 클라우드 크루저에서 가져온된 서비스 hello 목록을 확인할 수 있습니다 *서비스* 탭:</span><span class="sxs-lookup"><span data-stu-id="e6037-144">After publishing hello services and rates, you can verify hello list of imported services in Cloud Cruiser’s *Services* tab:</span></span>

<span data-ttu-id="e6037-145">![그림 5-새로운 서비스 hello 확인 하는 중][5]</span><span class="sxs-lookup"><span data-stu-id="e6037-145">![Figure 5 - Verifying hello new Services][5]</span></span>

<span data-ttu-id="e6037-146">Hello에 *속도 계획* 탭 hello 라는 "AzureSimulation" hello 요금으로 hello RateCard API에서에서 가져온는 새 요금 계획을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-146">On hello *Rate Plans* tab, you can check hello new rate plan called “AzureSimulation” with hello rates imported from hello RateCard API.</span></span>

<span data-ttu-id="e6037-147">![그림 6-새 요금 계획과 관련 된 요금이 hello 확인 하는 중][6]</span><span class="sxs-lookup"><span data-stu-id="e6037-147">![Figure 6 - Verifying hello new Rate Plan and associated rates][6]</span></span>

### <a name="normalize-wap-and-azure-services"></a><span data-ttu-id="e6037-148">WAP 및 Azure 서비스 표준화</span><span class="sxs-lookup"><span data-stu-id="e6037-148">Normalize WAP and Azure Services</span></span>
<span data-ttu-id="e6037-149">기본적으로 WAP hello 사용 하 여 계산, 메모리 및 네트워크 리소스에 따라 사용 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-149">By default, WAP provides usage information based on hello use of compute, memory, and network resources.</span></span> <span data-ttu-id="e6037-150">클라우드 크루저에 따라 서비스에 대해 직접 hello 할당 또는 이러한 리소스 사용 요금된을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-150">In Cloud Cruiser, you can define your services based directly on hello allocation or metered usage of these resources.</span></span> <span data-ttu-id="e6037-151">예를 들어 CPU 사용량의 시간별 또는 tooan 인스턴스에 할당 된 메모리의 충전 hello GB에 대 한 기본 비율을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-151">For example, you can set a basic rate for each hour of CPU usage, or charge hello GB of memory allocated tooan instance.</span></span>

<span data-ttu-id="e6037-152">예를 들어 WAP와 Azure 간의 순서 toocompare 비용에 매핑된 tooAzure 서비스 수 번들으로 tooaggregate hello 리소스 사용량 WAP에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-152">For this example, in order toocompare costs between WAP and Azure, we need tooaggregate hello resource usage on WAP into bundles, which can then be mapped tooAzure services.</span></span> <span data-ttu-id="e6037-153">Hello 통합 문서에이 변환은 쉽게 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-153">This transformation can be implemented easily in hello workbooks:</span></span>

<span data-ttu-id="e6037-154">![그림 7-WAP 데이터 toonormalize 서비스 변형][7]</span><span class="sxs-lookup"><span data-stu-id="e6037-154">![Figure 7 - Transforming WAP data toonormalize services][7]</span></span>

<span data-ttu-id="e6037-155">hello hello 통합 문서에서 마지막 단계는 hello 클라우드 크루저 데이터베이스로 toopublish hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-155">hello last step at hello workbook is toopublish hello data into hello Cloud Cruiser database.</span></span> <span data-ttu-id="e6037-156">이 단계 hello 사용 현황 데이터 (toohello Azure 서비스를 매핑할)는 서비스를 지금 제공 되 고 toodefault 세요 toocreate hello 요금을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-156">During this step, hello usage data is now bundled into services (that map toohello Azure Services) and tied toodefault rates toocreate hello charges.</span></span>

<span data-ttu-id="e6037-157">Hello 통합 문서를 완료 한 후 hello 스케줄러에서 작업을 추가 하 고 hello 빈도 및 통합 문서 toorun hello에 대 한 시간을 지정 하 여 hello hello 데이터 처리를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-157">After finishing hello workbook, you can automate hello processing of hello data, by adding a task on hello scheduler and specifying hello frequency and time for hello workbook toorun.</span></span>

<span data-ttu-id="e6037-158">![그림 8 - 워크북 예약][8]</span><span class="sxs-lookup"><span data-stu-id="e6037-158">![Figure 8 - Workbook scheduling][8]</span></span>

### <a name="create-reports-for-workload-cost-simulation-analysis"></a><span data-ttu-id="e6037-159">워크로드 비용 시뮬레이션 분석에 대한 보고서 만들기</span><span class="sxs-lookup"><span data-stu-id="e6037-159">Create Reports for Workload Cost Simulation Analysis</span></span>
<span data-ttu-id="e6037-160">수집 되는 hello 사용 요금 hello 클라우드 크루저 데이터베이스에 로드 된 후 hello 클라우드 크루저 Insights 모듈 toocreate hello 작업 부하 비용 시뮬레이션 원하는 म를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-160">After hello usage is collected and charges are loaded into hello Cloud Cruiser database, we can leverage hello Cloud Cruiser Insights module toocreate hello workload cost simulation that we desire.</span></span>

<span data-ttu-id="e6037-161">순서 toodemonstrate에이 시나리오에서는 만든 다음 보고서 hello:</span><span class="sxs-lookup"><span data-stu-id="e6037-161">In order toodemonstrate this scenario, we created hello following report:</span></span>

<span data-ttu-id="e6037-162">![비용 비교][9]</span><span class="sxs-lookup"><span data-stu-id="e6037-162">![Cost Comparison][9]</span></span>

<span data-ttu-id="e6037-163">hello 위쪽 그래프에는 서비스를 WAP (진한 파랑) 및 Azure (옅은 파란색) 각 특정 서비스에 대해 실행 중인 hello 워크 로드의 hello 가격을 비교 하 여 비용 비교를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-163">hello top graph shows a cost comparison by services, comparing hello price of running hello workload for each specific service between WAP (dark blue) and Azure (light blue).</span></span>

<span data-ttu-id="e6037-164">hello 아래쪽 그래프 hello 제품별로 부서에 있지만 동일한 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-164">hello bottom graph shows hello same data but broken down by department.</span></span> <span data-ttu-id="e6037-165">화면 표시에 대 한 각 부서 toorun hello 비용 프로그램 작업 WAP 및 Azure hello에 그 차이 hello 절약 모음 (녹색)와 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-165">This shows hello costs for each department toorun their workload on WAP and Azure, along with hello difference between them in hello Savings bar (green).</span></span>

## <a name="azure-usage-api"></a><span data-ttu-id="e6037-166">Azure 사용량 API</span><span class="sxs-lookup"><span data-stu-id="e6037-166">Azure Usage API</span></span>
### <a name="introduction"></a><span data-ttu-id="e6037-167">소개</span><span class="sxs-lookup"><span data-stu-id="e6037-167">Introduction</span></span>
<span data-ttu-id="e6037-168">Microsoft는 최근에 hello 구독자가 tooprogrammatically 끌어오기 소비량에 대 한 사용 현황 데이터 toogain 통찰에 허용 되는 Azure 사용량 API를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-168">Microsoft recently introduced hello Azure Usage API, allowing subscribers tooprogrammatically pull in usage data toogain insights into their consumption.</span></span> <span data-ttu-id="e6037-169">이 API를 통해 사용할 수 있는 다양 한 dataset hello 이용할 수 있는 클라우드 크루저 고객에 대 한 좋은 소식입니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-169">This is great news for Cloud Cruiser customers that can take advantage of hello richer dataset available through this API.</span></span>

<span data-ttu-id="e6037-170">클라우드 크루저 여러 가지 방법으로 hello 사용량 API와 hello 통합을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-170">Cloud Cruiser can leverage hello integration with hello Usage API in several ways.</span></span> <span data-ttu-id="e6037-171">hello 세분성 (시간별 사용량 정보) 및 hello api를 통해 사용할 수 있는 리소스 메타 데이터 정보에는 필요한 데이터 집합 toosupport 유연한 비용 정산 또는 비용 확인 모델 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-171">hello granularity (hourly usage information) and resource metadata information available through hello API provides hello necessary dataset toosupport flexible Showback or Chargeback models.</span></span> 

<span data-ttu-id="e6037-172">이 자습서에서는 클라우드 크루저 hello 사용량 API 정보에서에서 얻을 수는 방법의 예로 제공할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-172">In this tutorial, we will present one example of how Cloud Cruiser can benefit from hello Usage API information.</span></span> <span data-ttu-id="e6037-173">보다 구체적으로, 우리는 Azure 리소스 그룹을 만들고, hello 계정 구조에 대 한 태그를 연결한 다음 hello 풀링 및 클라우드 크루저에 hello 태그 정보를 처리 하는 과정을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-173">More specifically, we will create a Resource Group on Azure, associate tags for hello account structure, then describe hello process of pulling and processing hello tag information into Cloud Cruiser.</span></span>

<span data-ttu-id="e6037-174">hello 최종 목표 toobe 수 toocreate 보고서 hello 하나, 고 비용 수 tooanalyze 하 고 hello 태그를 사용해 hello 계정 구조를 기반으로 사용할 수입니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-174">hello final goal is toobe able toocreate reports like hello following one, and be able tooanalyze cost and consumption based on hello account structure populated by hello tags.</span></span>

<span data-ttu-id="e6037-175">![그림 10 - 태그를 사용하는 명세 포함 보고서][10]</span><span class="sxs-lookup"><span data-stu-id="e6037-175">![Figure 10 - Report with breakdowns using tags][10]</span></span>

### <a name="microsoft-azure-tags"></a><span data-ttu-id="e6037-176">Microsoft Azure 태그</span><span class="sxs-lookup"><span data-stu-id="e6037-176">Microsoft Azure Tags</span></span>
<span data-ttu-id="e6037-177">hello Azure 사용량 API를 통해 사용할 수 있는 hello 데이터 소비 정보 뿐만 아니라 연결 된 모든 태그를 포함 하는 리소스 메타 데이터를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-177">hello data available through hello Azure Usage API includes not only consumption information, but also resource metadata including any tags associated with it.</span></span> <span data-ttu-id="e6037-178">태그에서는 리소스를 쉽게 tooorganize를 제공 하지만 필요 tooensure 순서 toobe 효과적인,입니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-178">Tags provide an easy way tooorganize your resources, but in order toobe effective, you need tooensure that:</span></span>

* <span data-ttu-id="e6037-179">태그는 프로 비전 시 올바르게 적용된 toohello 리소스</span><span class="sxs-lookup"><span data-stu-id="e6037-179">Tags are correctly applied toohello resources at provision time</span></span>
* <span data-ttu-id="e6037-180">태그는 hello 비용 확인/지불 거절 프로세스 tootie hello 사용 toohello 조직의 계정 구조에 제대로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-180">Tags are properly used on hello Showback/Chargeback process tootie hello usage toohello organization’s account structure.</span></span>

<span data-ttu-id="e6037-181">이러한 요구 사항을 모두 hello 프로 비전 또는 쪽 충전에 수동 프로세스 필요한 경우에 특히 하기는 어려울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-181">Both of these requirements can be challenging, especially when there is a manual process on hello provision or charging side.</span></span> <span data-ttu-id="e6037-182">태그를 잘못 입력 된, 잘못 되었거나 누락 되었음도 고객의 일반적인 불만 사항 때는 태그와 이러한 오류를 사용 하기 매우 어려운 측면 충전 hello에 수명 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-182">Mistyped, incorrect or even missing tags are common complaints from customers when using tags and these errors can make life on hello charging side very difficult.</span></span>

<span data-ttu-id="e6037-183">Hello로 새 Azure 사용량 API, 클라우드 크루저 리소스 태그 정보를 끌어오기 하 고 통합 문서를 호출 하는 정교한 ETL 도구를 통해 이러한 일반적인 태그 오류를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-183">With hello new Azure Usage API, Cloud Cruiser can pull resource tagging information, and through a sophisticated ETL tool called workbooks, fix these common tagging errors.</span></span> <span data-ttu-id="e6037-184">정규식과 상관 관계 데이터를 사용 하 여 변환을 통해 클라우드 크루저 잘못 태그가 지정 된 리소스를 식별 하 고 hello 소비자와 hello 리소스의 hello 올바른 연결을 보장 hello 올바른 태그를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-184">Through transformation using regular expressions and data correlation, Cloud Cruiser can identify incorrectly tagged resources and apply hello correct tags, ensuring hello correct association of hello resources with hello consumer.</span></span>

<span data-ttu-id="e6037-185">Hello 쪽 충전에서 클라우드 크루저 hello 비용 확인/지불 거절 프로세스를 자동화 하 고 hello 태그 정보 tootie hello 사용 toohello 적절 한 소비자 (부서, 부서, 프로젝트 등)을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-185">On hello charging side, Cloud Cruiser automates hello Showback/Chargeback process, and can leverage hello tag information tootie hello usage toohello appropriate consumer (Department, Division, Project, etc.).</span></span> <span data-ttu-id="e6037-186">이 자동화를 통해 효율을 대폭 향상할 수 있을 뿐 아니라 일관적이고 감사 가능한 과금 프로세스를 보장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-186">This automation provides a huge improvement and can ensure a consistent and auditable charging process.</span></span>

### <a name="creating-a-resource-group-with-tags-on-microsoft-azure"></a><span data-ttu-id="e6037-187">Microsoft Azure에서 태그를 사용하여 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="e6037-187">Creating a Resource Group with tags on Microsoft Azure</span></span>
<span data-ttu-id="e6037-188">hello이 자습서의 첫 번째 단계 toocreate hello Azure 포털에서에서 리소스 그룹은 다음 tooassociate toohello 리소스 새 태그를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-188">hello first step in this tutorial is toocreate a Resource Group in hello Azure portal, then create new tags tooassociate toohello resources.</span></span> <span data-ttu-id="e6037-189">예를 들어 만드는데 태그 hello: 부서, 환경, 소유자, 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="e6037-189">For this example, we will be creating hello following tags: Department, Environment, Owner, Project.</span></span>

<span data-ttu-id="e6037-190">아래의 스크린 샷은 hello hello로 리소스 그룹 관련 태그 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-190">hello screenshot below shows a sample Resource Group with hello associated tags.</span></span>

<span data-ttu-id="e6037-191">![그림 11 - Azure 포털의 태그가 연결된 리소스 그룹l][11]</span><span class="sxs-lookup"><span data-stu-id="e6037-191">![Figure 11 - Resource Group with associated tags on Azure portal][11]</span></span>

<span data-ttu-id="e6037-192">hello 다음 단계에는 클라우드 크루저 hello 사용량 API의에서 toopull hello 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-192">hello next step is toopull hello information from hello Usage API into Cloud Cruiser.</span></span> <span data-ttu-id="e6037-193">hello 사용량 API는 현재 JSON 형식의 응답을에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-193">hello Usage API currently provides responses in JSON format.</span></span> <span data-ttu-id="e6037-194">검색 된 hello 데이터의 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-194">Here is a sample of hello data retrieved:</span></span>

    {
      "id": "/subscriptions/bb678b04-0e48-4b44-XXXX-XXXXXXX/providers/Microsoft.Commerce/UsageAggregates/Daily_BRSDT_20150623_0000",
      "name": "Daily_BRSDT_20150623_0000",
      "type": "Microsoft.Commerce/UsageAggregate",
      "properties":
      {
        "subscriptionId": "bb678b04-0e48-4b44-XXXX-XXXXXXXXX",
        "usageStartTime": "2015-06-22T00:00:00+00:00",
        "usageEndTime": "2015-06-23T00:00:00+00:00",
        "meterName": "Compute Hours",
        "meterRegion": "",
        "meterCategory": "Virtual Machines",
        "meterSubCategory": "Standard_D1 VM (Non-Windows)",
        "unit": "Hours",
        "instanceData": "{\"Microsoft.Resources\":{\"resourceUri\":\"/subscriptions/bb678b04-0e48-4b44-XXXX-XXXXXXXX/resourceGroups/DEMOUSAGEAPI/providers/Microsoft.Compute/virtualMachines/MyDockerVM\",\"location\":\"eastus\",\"tags\":{\"Department\":\"Sales\",\"Project\":\"Demo Usage API\",\"Environment\":\"Test\",\"Owner\":\"RSE\"},\"additionalInfo\":{\"ImageType\":\"Canonical\",\"ServiceType\":\"Standard_D1\"}}}",
        "meterId": "e60caf26-9ba0-413d-a422-6141f58081d6",
        "infoFields": {},
        "quantity": 8

      },
    },


### <a name="import-data-from-hello-usage-api-into-cloud-cruiser"></a><span data-ttu-id="e6037-195">Hello 사용량 API에서에서 데이터를 클라우드 크루저 가져오기</span><span class="sxs-lookup"><span data-stu-id="e6037-195">Import data from hello Usage API into Cloud Cruiser</span></span>
<span data-ttu-id="e6037-196">클라우드 크루저 통합 문서는 hello 사용량 API에서에서 자동화 된 방식이 toocollect 및 프로세스 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-196">Cloud Cruiser workbooks provide an automated way toocollect and process information from hello Usage API.</span></span> <span data-ttu-id="e6037-197">ETL (추출-변환-로드) 통합을 사용 하면 tooconfigure hello 컬렉션, 변환 및 데이터 게시 hello 클라우드 크루저 데이터베이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-197">An ETL (extract-transform-load) workbook allows you tooconfigure hello collection, transformation, and publishing of data into hello Cloud Cruiser database.</span></span>

<span data-ttu-id="e6037-198">각 워크북은 하나 또는 여러 컬렉션을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-198">Each workbook can have one or multiple collections.</span></span> <span data-ttu-id="e6037-199">이렇게 하면 서로 다른 소스 toocomplement 또는 업그레이드 hello 사용 현황 데이터의 toocorrelate 정보가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-199">This allows you toocorrelate information from different sources toocomplement or augment hello usage data.</span></span> <span data-ttu-id="e6037-200">이 예에서는 새 시트에서에서 만들 hello Azure 템플릿의 통합 문서 (*UsageAPI)* 새 설정 *컬렉션* hello 사용량 API에서에서 tooimport 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-200">For this example, we will create a new sheet in hello Azure template workbook (*UsageAPI)* and set a new *collection* tooimport information from hello Usage API.</span></span>

<span data-ttu-id="e6037-201">![그림 3-hello UsageAPI 시트로 가져온 API 사용 현황 데이터][12]</span><span class="sxs-lookup"><span data-stu-id="e6037-201">![Figure 3 - Usage API data imported into hello UsageAPI sheet][12]</span></span>

<span data-ttu-id="e6037-202">이 통합 문서 이미에 다른 시트를 Azure에서 tooimport 서비스 (*ImportServices*), hello 청구 API에서에서 hello 소비 정보를 처리 하 고 (*PublishData*).</span><span class="sxs-lookup"><span data-stu-id="e6037-202">Notice that this workbook already has other sheets tooimport services from Azure (*ImportServices*), and process hello consumption information from hello Billing API (*PublishData*).</span></span>

<span data-ttu-id="e6037-203">그런 다음 사용 하 여 hello 사용량 API toopopulate hello *UsageAPI* 시트 및 hello hello 청구 API에서에서 hello 소비 데이터와 상호 연결 시키고 hello 정보 *PublishData* 시트입니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-203">Next we will use hello Usage API toopopulate hello *UsageAPI* sheet, and correlate hello information with hello consumption data from hello Billing API on hello *PublishData* sheet.</span></span>

### <a name="processing-hello-tag-information-from-hello-usage-api"></a><span data-ttu-id="e6037-204">사용량 API hello에서 처리 hello 태그 정보</span><span class="sxs-lookup"><span data-stu-id="e6037-204">Processing hello tag information from hello Usage API</span></span>
<span data-ttu-id="e6037-205">Hello 통합 문서에 hello 데이터를 가져온 후 변환 단계에서에서 만들 hello *UsageAPI* 시트로 hello API에서에서 주문 tooprocess hello 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-205">After importing hello data into hello workbook, we will create transformation steps in hello *UsageAPI* sheet in order tooprocess hello information from hello API.</span></span> <span data-ttu-id="e6037-206">첫 번째 단계는 toouse "JSON 분할" 프로세서 tooextract hello 단일 필드에서 태그를 삽입 한 다음 각 (부서, 프로젝트, 소유자 및 환경) 중 하나에 대 한 필드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-206">First step is toouse a “JSON split” processor tooextract hello tags from a single field, then create fields for each one of them (Department, Project, Owner, and Environment).</span></span>

<span data-ttu-id="e6037-207">![그림 4-hello 태그 정보에 대 한 새 필드 만들기][13]</span><span class="sxs-lookup"><span data-stu-id="e6037-207">![Figure 4 - Create new fields for hello tag information][13]</span></span>

<span data-ttu-id="e6037-208">공지 hello "네트워킹" 서비스 (노란색 상자) hello 태그 정보가 없습니다 hello의 일부 인지 확인할 수 있지만 hello 확인 하 여 동일한 리소스 그룹 *ResourceGroupName* 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-208">Notice hello “Networking” service is missing hello tag information (yellow box), but we can verify that it is part of hello same Resource Group by looking at hello *ResourceGroupName* field.</span></span> <span data-ttu-id="e6037-209">이 리소스 그룹에서 다른 리소스 hello에 대 한 hello 태그 했기 때문에이 정보 tooapply hello hello 프로세스의 뒷부분에 나오는 태그 toothis 리소스가 없습니다를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-209">Since we have hello tags for hello other resources from this Resource Group, we can use this information tooapply hello missing tags toothis resource later in hello process.</span></span>

<span data-ttu-id="e6037-210">hello 다음 단계는 toocreate는 조회 테이블 연결 hello 정보에서 태그 toohello hello *ResourceGroupName*합니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-210">hello next step is toocreate a lookup table associating hello information from hello tags toohello *ResourceGroupName*.</span></span> <span data-ttu-id="e6037-211">이 조회 테이블 hello 다음 단계 tooenrich hello 소비 데이터에 태그 정보로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-211">This lookup table will be used on hello next step tooenrich hello consumption data with tag information.</span></span>

### <a name="adding-hello-tag-information-toohello-consumption-data"></a><span data-ttu-id="e6037-212">Hello 태그 정보 toohello 소비 데이터 추가</span><span class="sxs-lookup"><span data-stu-id="e6037-212">Adding hello tag information toohello consumption data</span></span>
<span data-ttu-id="e6037-213">Toohello로 바로 이동할 수 이제 *PublishData* 시트에서 어느 프로세스가 hello 청구 API에서에서 사용 정보를 hello 및 hello 태그에서 추출 된 hello 필드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-213">Now we can jump toohello *PublishData* sheet, which processes hello consumption information from hello Billing API, and add hello fields extracted from hello tags.</span></span> <span data-ttu-id="e6037-214">이 프로세스는 hello를 사용 하 여 hello 이전 단계에서 만든 hello 조회 테이블을 확인 하 여 수행 됩니다 *ResourceGroupName* hello hello 조회 키로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-214">This process is performed by looking at hello lookup table created on hello previous step, using hello *ResourceGroupName* as hello key for hello lookups.</span></span>

<span data-ttu-id="e6037-215">![그림 5-hello hello 조회 정보로 hello 계정 구조 채우기][14]</span><span class="sxs-lookup"><span data-stu-id="e6037-215">![Figure 5 - Populating hello account structure with hello information from hello lookups][14]</span></span>

<span data-ttu-id="e6037-216">태그 누락 hello로 hello 문제를 해결 hello "네트워킹" 서비스에 대 한 적절 한 계정 구조 필드 hello 적용 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-216">Notice that hello appropriate account structure fields for hello “Networking” service were applied, fixing hello issue with hello missing tags.</span></span> <span data-ttu-id="e6037-217">"기타"를이 대상 리소스 그룹 이외의 리소스에 대 한 hello 계정 구조체 필드를 채울 우리, 순서 toodifferentiate에 hello에 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-217">We also populated hello account structure fields for resources other than our target Resource Group with “Other”, in order toodifferentiate them on hello reports.</span></span>

<span data-ttu-id="e6037-218">이제 방금 tooadd 단계 toopublish hello 사용 현황 데이터 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-218">Now we just need tooadd a step toopublish hello usage data.</span></span> <span data-ttu-id="e6037-219">이 단계에서는 요금제에 정의 된 각 서비스에 대 한 적절 한 속도 hello hello 데이터베이스에 로드 하는 hello 결과 충전에 적용 된 toohello 사용 정보가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-219">During this step, hello appropriate rates for each service defined on our Rate Plan will be applied toohello usage information, with hello resulting charge loaded into hello database.</span></span>

<span data-ttu-id="e6037-220">hello 최상의 부분은 있다고 toogo이이 프로세스를 통해 한 번입니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-220">hello best part is that you only have toogo through this process once.</span></span> <span data-ttu-id="e6037-221">Tooadd 하기만 hello 통합 문서 완료 되 면 그 매일 다음 시간 hello에 예약 된 시간 또는 toohello 스케줄러 고 1 시간 마다 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-221">When hello workbook is completed, you just need tooadd it toohello scheduler and it will run hourly or daily at hello scheduled time.</span></span> <span data-ttu-id="e6037-222">이면 새 보고서를 만들거나 순서 tooanalyze hello 데이터 tooget 의미 있는 insights에서 클라우드 사용으로 인해 기존의 것을 사용자 지정의 문제만 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-222">Then it’s just a matter of creating new reports, or customizing existing ones, in order tooanalyze hello data tooget meaningful insights from your cloud usage.</span></span>

### <a name="next-steps"></a><span data-ttu-id="e6037-223">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e6037-223">Next Steps</span></span>
* <span data-ttu-id="e6037-224">TooCloud 크루저 상대의 온라인 클라우드 크루저 통합 문서 및 보고서를 만드는 방법에 대 한 자세한 지침을 참조 하십시오에 대 한 [설명서](http://docs.cloudcruiser.com/) (유효한 로그인 필요).</span><span class="sxs-lookup"><span data-stu-id="e6037-224">For detailed instructions on creating Cloud Cruiser workbooks and reports, please refer tooCloud Cruiser’s online [documentation](http://docs.cloudcruiser.com/) (valid login required).</span></span>  <span data-ttu-id="e6037-225">Cloud Cruiser에 대한 자세한 내용은 [info@cloudcruiser.com](mailto:info@cloudcruiser.com)에 연결하는 조회 테이블을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-225">For more information about Cloud Cruiser, please contact [info@cloudcruiser.com](mailto:info@cloudcruiser.com).</span></span>
* <span data-ttu-id="e6037-226">참조 [Microsoft Azure 리소스 소비량에 대 한 이해력](billing-usage-rate-card-overview.md) hello Azure 리소스 사용량 및 RateCard Api에 대 한 개요입니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-226">See [Gain insights into your Microsoft Azure resource consumption](billing-usage-rate-card-overview.md) for an overview of hello Azure Resource Usage and RateCard APIs.</span></span>
* <span data-ttu-id="e6037-227">체크 아웃 hello [Azure 청구 REST API 참조](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) 두 Api에 대 한 자세한 내용은 hello hello Azure 리소스 관리자에서 제공 된 Api 집합이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-227">Check out hello [Azure Billing REST API Reference](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) for more information on both APIs, which are part of hello set of APIs provided by hello Azure Resource Manager.</span></span>
* <span data-ttu-id="e6037-228">Hello 샘플 코드에 바로 toodive 하려는 경우에 Microsoft Azure 청구 API 코드 샘플 확인해 [Azure 코드 예제](https://azure.microsoft.com/documentation/samples/?term=billing)합니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-228">If you would like toodive right into hello sample code, check out our Microsoft Azure Billing API Code Samples on [Azure Code Samples](https://azure.microsoft.com/documentation/samples/?term=billing).</span></span>

### <a name="learn-more"></a><span data-ttu-id="e6037-229">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="e6037-229">Learn More</span></span>
* <span data-ttu-id="e6037-230">Hello 참조 [Azure 리소스 관리자 개요](../azure-resource-manager/resource-group-overview.md) hello Azure 리소스 관리자에 대 한 자세한 문서 toolearn 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6037-230">See hello [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md) article toolearn more about hello Azure Resource Manager.</span></span>

<!--Image references-->

[1]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Create-New-Workbook-Collection.png "그림 1-새 컬렉션 만들기"
[2]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Import-Data-From-RateCard.png "그림 2-hello 새 컬렉션에서 데이터 가져오기"
[3]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Transformation-Steps-Process-RateCard-Data.png "그림 3-변환 RateCard API에서 데이터 수집 tooprocess 단계"
[4]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Publish-RateCard-Data-New-Services-Rates.png "그림 4-hello 데이터 hello RateCard API를에서 게시 하는 새로운 서비스와 속도"
[5]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Verify-Azure-Services-And-Pricing1.png "그림 5-새로운 서비스 hello 확인 하는 중"
[6]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Verify-Azure-Services-And-Pricing2.png "그림 6-새 요금 계획과 관련 된 요금이 hello 확인 하는 중"
[7]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Transforming-WAP-Normalize-Services.png "그림 7-WAP 데이터 toonormalize 서비스 변형"
[8]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Workbook-Scheduling.png "그림 8- 워크북 예약"
[9]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Workload-Cost-Simulation-Report.png "그림 9-hello 작업 부하 비용 비교 시나리오를 위한 예제 보고서"
[10]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/1_ReportWithTags.png "그림 10 - 태그를 사용하는 명세 포함 보고서"
[11]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/2_ResourceGroupsWithTags.png "그림 11 - Azure 포털의 태그가 연결된 리소스 그룹"
[12]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/3_ImportIntoUsageAPISheet.png "그림 12-hello UsageAPI 시트로 가져온 API 사용 현황 데이터"
[13]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/4_NewTagField.png "그림 13-hello 태그 정보에 대 한 새 필드 만들기"
[14]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/5_PopulateAccountStructure.png "그림 14-hello hello 조회 정보로 hello 계정 구조 채우기"
