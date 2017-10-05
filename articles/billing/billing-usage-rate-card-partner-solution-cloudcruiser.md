---
title: "Cloud Cruiser 및 Microsoft Azure 청구 API 통합 | Microsoft Docs"
description: "경험으로 해당 제품에 Azure 청구 API를 통합하여 Microsoft Azure 청구 파트너 Cloud Cruiser에서 고유한 관점을 제공합니다.  Microsoft Azure 팩용 Cloud Cruiser를 사용/시도하는 데 관심을 두는 Azure 및 Cloud Cruiser 고객에게 특히 유용합니다."
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
ms.openlocfilehash: a05fe5e610f1f0ce216a4b84bf2873b0d081875d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="cloud-cruiser-and-microsoft-azure-billing-api-integration"></a><span data-ttu-id="f461e-104">클라우드 크루저 및 Microsoft Azure 청구 API 통합</span><span class="sxs-lookup"><span data-stu-id="f461e-104">Cloud Cruiser and Microsoft Azure Billing API Integration</span></span>
<span data-ttu-id="f461e-105">이 문서는 새로운 Microsoft Azure 청구 API로부터 수집한 정보를 Cloud Cruiser에서 워크플로 비용 시뮬레이션 및 분석에 사용할 수 있는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-105">This article describes how the information collected from the new Microsoft Azure Billing APIs can be used in Cloud Cruiser for workflow cost simulation and analysis.</span></span>

## <a name="azure-ratecard-api"></a><span data-ttu-id="f461e-106">Azure RateCard API</span><span class="sxs-lookup"><span data-stu-id="f461e-106">Azure RateCard API</span></span>
<span data-ttu-id="f461e-107">RateCard API는 Azure에서 환율 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-107">The RateCard API provides rate information from Azure.</span></span> <span data-ttu-id="f461e-108">적절한 자격 증명을 인증한 후에 제품 ID를 제공하면 연결 속도와 함께 Azure에서 사용할 수 있는 서비스에 대 한 메타데이터를 수집하는 API를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-108">After authenticating with the proper credentials, you can query the API to collect metadata about the services available on Azure, along with the rates associated with your Offer ID.</span></span>

<span data-ttu-id="f461e-109">다음은 A0(Windows) 인스턴스에 대한 가격을 표시하는 API의 샘플 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-109">The following is a sample response from the API showing the prices for the A0 (Windows) instance:</span></span>

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

### <a name="cloud-cruisers-interface-to-azure-ratecard-api"></a><span data-ttu-id="f461e-110">Azure RateCard API에 대한 클라우드 크루저의 인터페이스</span><span class="sxs-lookup"><span data-stu-id="f461e-110">Cloud Cruiser’s Interface to Azure RateCard API</span></span>
<span data-ttu-id="f461e-111">다른 방법으로 클라우드 크루저가 RateCard API 정보를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-111">Cloud Cruiser can leverage the RateCard API information in different ways.</span></span> <span data-ttu-id="f461e-112">이 문서에서 어떻게 IaaS를 워크로드 비용 시뮬레이션 및 분석을 만드는데 사용할 수 있는지 알아보겠습니다</span><span class="sxs-lookup"><span data-stu-id="f461e-112">For this article, we will show how it can be used to make IaaS workload cost simulation and analysis.</span></span>

<span data-ttu-id="f461e-113">이 사용 사례를 설명하기 위해 Microsoft Azure 팩(WAP)을 실행하는 여러 인스턴스의 워크로드를 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-113">To demonstrate this use case, imagine a workload of several instances running on Microsoft Azure Pack (WAP).</span></span> <span data-ttu-id="f461e-114">Azure에서 이 같은 워크로드를 시뮬레이션하고 이러한 마이그레이션을 수행하는 비용을 추정하는 것이 목표입니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-114">The goal is to simulate this same workload on Azure, and estimate the costs of doing such migration.</span></span> <span data-ttu-id="f461e-115">이 시뮬레이션을 만들기 위해 두 주요 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-115">In order to create this simulation, there are two main tasks to be performed:</span></span>

1. <span data-ttu-id="f461e-116">**RateCard API에서 수집한 서비스 정보 가져오기 및 처리하기.**</span><span class="sxs-lookup"><span data-stu-id="f461e-116">**Import and process the service information collected from the RateCard API.**</span></span> <span data-ttu-id="f461e-117">이 작업은 RateCard API에서 추출한 내용이 새 요금제로 변환되고 게시되는 워크북에서도 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-117">This task is also performed on the workbooks, where the extract from the RateCard API is transformed and published to a new rate plan.</span></span> <span data-ttu-id="f461e-118">이 새 요금제는 Azure 가격을 추정하는 시뮬레이션에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-118">This new rate plan will be used on the simulations to estimate the Azure prices.</span></span>
2. <span data-ttu-id="f461e-119">**IaaS에 대한 WAP 서비스 및 Azure 서비스 정규화.**</span><span class="sxs-lookup"><span data-stu-id="f461e-119">**Normalize WAP services and Azure services for IaaS.**</span></span> <span data-ttu-id="f461e-120">Azure 서비스가 인스턴스 크기(A0, A1, A2 등)에 기반한 반면 WAP 서비스는 기본적으로 개별 리소스(CPU, 메모리 크기, 디스크 크기 등)에 기반합니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-120">By default, WAP services are based on individual resources (CPU, Memory Size, Disk Size, etc.) while Azure services are based on instance size (A0, A1, A2, etc.).</span></span> <span data-ttu-id="f461e-121">이 첫 번째 작업은 Cloud Cruiser ETL 엔진이라는 호출된 워크북에 의해 수행되고 이러한 리소스를 Azure 인스턴스 서비스와 비슷한 인스턴스 크기로 묶을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-121">This first task can be performed by Cloud Cruiser’s ETL engine, called workbooks, where these resources can be bundled on instance sizes, analogous to Azure instance services.</span></span>

### <a name="import-data-from-the-ratecard-api"></a><span data-ttu-id="f461e-122">RateCard API에서 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="f461e-122">Import data from the RateCard API</span></span>
<span data-ttu-id="f461e-123">클라우드 크루저 워크북은 RateCard API에서 정보를 수집하고 처리하는 자동화된 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-123">Cloud Cruiser workbooks provide an automated way to collect and process information from the RateCard API.</span></span>  <span data-ttu-id="f461e-124">ETL(추출-변환-로드) 워크북을 사용하면 클라우드 크루저 데이터베이스에서 데이터를 수집, 변환 및 게시하도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-124">ETL (extract-transform-load) workbooks allow you to configure the collection, transformation, and publishing of data into the Cloud Cruiser database.</span></span>

<span data-ttu-id="f461e-125">각 워크북은 하나 또는 여러 컬렉션을 가질 수 있으며, 이를 통해 사용 데이터를 보완하거나 보강하도록 다양한 소스의 정보를 상호 연결하여 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-125">Each workbook can have one or multiple collections, allowing you to correlate information from different sources to complement or augment the usage data.</span></span> <span data-ttu-id="f461e-126">다음 두 개의 스크린샷은, 기존 워크북에서 새 *컬렉션*을 만들고 RateCard API의 *컬렉션*으로 정보를 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-126">The following two screenshots show how to create a new *collection* in an existing workbook, and importing information into the *collection* from the RateCard API:</span></span>

<span data-ttu-id="f461e-127">![그림 1 - 새 컬렉션 만들기][1]</span><span class="sxs-lookup"><span data-stu-id="f461e-127">![Figure 1 - Creating a new collection][1]</span></span>

<span data-ttu-id="f461e-128">![그림 2 - 새 컬렉션에서 데이터 가져오기][2]</span><span class="sxs-lookup"><span data-stu-id="f461e-128">![Figure 2 - Import data from the new collection][2]</span></span>

<span data-ttu-id="f461e-129">워크북에 데이터를 가져온 후 데이터를 수정하고 모델화하여 여러 단계 및 변환 프로세스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-129">After importing the data into the workbook, it’s possible to create multiple steps and transformation processes, to modify and model the data.</span></span> <span data-ttu-id="f461e-130">이 예제에서 IaaS(Infrastructure-as-a-Service)에 관심이 있으므로 IaaS가 아닌 다른 서비스와 관련된 불필요한 행 또는 레코드를 제거하는 변환 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-130">For this example, since we are only interested in infrastructure-as-a-Service (IaaS) we can use the transformation steps to remove unnecessary rows, or records, related to services other than IaaS.</span></span>

<span data-ttu-id="f461e-131">아래 스크린샷은 RateCard API에서 수집된 데이터를 처리하는 데 사용되는 변환 단계를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-131">The following screenshot shows the transformation steps used to process the data collected from RateCard API:</span></span>

<span data-ttu-id="f461e-132">![그림 3 - RateCard API에서 수집된 데이터를 처리하는 변환 단계][3]</span><span class="sxs-lookup"><span data-stu-id="f461e-132">![Figure 3 - Transformation steps to process collected data from RateCard API][3]</span></span>

### <a name="defining-new-services-and-rate-plans"></a><span data-ttu-id="f461e-133">새로운 서비스 및 요금제 정의</span><span class="sxs-lookup"><span data-stu-id="f461e-133">Defining New Services and Rate Plans</span></span>
<span data-ttu-id="f461e-134">Cloud Cruiser에서 서비스를 정의하는 여러 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-134">There are different ways to define services on Cloud Cruiser.</span></span> <span data-ttu-id="f461e-135">옵션 중 하나는 사용 데이터에서 서비스를 가져오는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-135">One of the options is to import the services from the usage data.</span></span> <span data-ttu-id="f461e-136">이 메서드는 공급자가 서비스를 이미 정의한 경우에 공용 클라우드로 작업할 때 일반적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-136">This method is commonly used when working with public clouds, where the services are already defined by the provider.</span></span>

<span data-ttu-id="f461e-137">요금제는 유효 날짜 또는 다른 옵션과 함께 고객의 그룹에 따라 다양한 서비스에 적용할 수 있는 가격 또는 요금의 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-137">A Rate Plan is a set of rates or prices that can be applied to different services, based on effective dates, or group of customers, among other options.</span></span> <span data-ttu-id="f461e-138">요금제는 Cloud Cruiser에서 시뮬레이션 또는 "가상 분석" 시나리오를 만드는 데 사용하여 서비스의 변경이 워크로드의 총비용에 주는 영향을 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-138">Rate Plans can also be used on Cloud Cruiser to create simulation or “What-if” scenarios, to understand how changes in services can affect the total cost of a workload.</span></span>

<span data-ttu-id="f461e-139">이 예제에서 Cloud Cruiser에서 새 서비스를 정의 하는 RateCard API의 서비스 정보를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-139">In this example, we will use the service information from the RateCard API to define new services in Cloud Cruiser.</span></span> <span data-ttu-id="f461e-140">같은 방법으로 Cloud Cruiser에서 새 요금제를 만들어서 서비스와 연결된 요금을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-140">In the same way, we can use the rates associated to the services to create a new Rate Plan on Cloud Cruiser.</span></span>

<span data-ttu-id="f461e-141">변환 프로세스가 끝날 때 새 단계를 만들고 새 서비스 및 요금으로 RateCard API에서 데이터를 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-141">At the end of the transformation process, it is possible to create a new step and publish the data from the RateCard API as new services and rates.</span></span>

<span data-ttu-id="f461e-142">![그림 4 - 새 서비스 및 요금 RateCard API에 데이터 게시][4]</span><span class="sxs-lookup"><span data-stu-id="f461e-142">![Figure 4 - Publishing the data from the RateCard API as new Services and Rates][4]</span></span>

### <a name="verify-azure-services-and-rates"></a><span data-ttu-id="f461e-143">Azure 서비스 및 요금 확인</span><span class="sxs-lookup"><span data-stu-id="f461e-143">Verify Azure Services and Rates</span></span>
<span data-ttu-id="f461e-144">서비스 및 요금을 게시한 후 Cloud Cruiser의 *서비스* 탭에서 가져온 서비스의 목록을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-144">After publishing the services and rates, you can verify the list of imported services in Cloud Cruiser’s *Services* tab:</span></span>

<span data-ttu-id="f461e-145">![그림 5 - 새로운 서비스 확인][5]</span><span class="sxs-lookup"><span data-stu-id="f461e-145">![Figure 5 - Verifying the new Services][5]</span></span>

<span data-ttu-id="f461e-146">*요금제* 탭에서 RateCard API에서 가져온 새 요금으로 "AzureSimulation"이라 불리는 새 요금제를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-146">On the *Rate Plans* tab, you can check the new rate plan called “AzureSimulation” with the rates imported from the RateCard API.</span></span>

<span data-ttu-id="f461e-147">![그림 6 - 새 요금제와 연결된 요금 확인][6]</span><span class="sxs-lookup"><span data-stu-id="f461e-147">![Figure 6 - Verifying the new Rate Plan and associated rates][6]</span></span>

### <a name="normalize-wap-and-azure-services"></a><span data-ttu-id="f461e-148">WAP 및 Azure 서비스 표준화</span><span class="sxs-lookup"><span data-stu-id="f461e-148">Normalize WAP and Azure Services</span></span>
<span data-ttu-id="f461e-149">기본적으로 WAP은 계산, 메모리 및 네트워크 리소스의 사용에 기반하여 사용 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-149">By default, WAP provides usage information based on the use of compute, memory, and network resources.</span></span> <span data-ttu-id="f461e-150">Cloud Cruiser에서 할당 또는 이러한 리소스의 요금제 사용에 직접 기반하여 서비스를 정의할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="f461e-150">In Cloud Cruiser, you can define your services based directly on the allocation or metered usage of these resources.</span></span> <span data-ttu-id="f461e-151">예를 들어 CPU 사용의 각 시간 당 기본 요금을 설정하거나 인스턴스에 할당된 메모리의 GB에 비용을 청구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-151">For example, you can set a basic rate for each hour of CPU usage, or charge the GB of memory allocated to an instance.</span></span>

<span data-ttu-id="f461e-152">이 예제에서 WAP와 Azure 간의 비용을 비교하기 위해 WAP의 리소스 사용을 번들로 집계한 다음 Azure 서비스에 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-152">For this example, in order to compare costs between WAP and Azure, we need to aggregate the resource usage on WAP into bundles, which can then be mapped to Azure services.</span></span> <span data-ttu-id="f461e-153">이 변환은 워크북에서 쉽게 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-153">This transformation can be implemented easily in the workbooks:</span></span>

<span data-ttu-id="f461e-154">![그림 7 - 서비스를 정규화하는 WAP 데이터 변환][7]</span><span class="sxs-lookup"><span data-stu-id="f461e-154">![Figure 7 - Transforming WAP data to normalize services][7]</span></span>

<span data-ttu-id="f461e-155">워크북에서 마지막 단계는 Cloud Cruiser 데이터베이스로 데이터를 게시하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-155">The last step at the workbook is to publish the data into the Cloud Cruiser database.</span></span> <span data-ttu-id="f461e-156">이 단계 동안 사용 데이터는 이제 서비스에 번들되고(Azure 서비스에 매핑) 요금을 만들어 기본 요금을 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-156">During this step, the usage data is now bundled into services (that map to the Azure Services) and tied to default rates to create the charges.</span></span>

<span data-ttu-id="f461e-157">워크북을 마친 후 Scheduler에서 작업을 추가하고 실행할 워크북에 대한 시간 및 빈도를 지정하여 데이터 처리를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-157">After finishing the workbook, you can automate the processing of the data, by adding a task on the scheduler and specifying the frequency and time for the workbook to run.</span></span>

<span data-ttu-id="f461e-158">![그림 8 - 워크북 예약][8]</span><span class="sxs-lookup"><span data-stu-id="f461e-158">![Figure 8 - Workbook scheduling][8]</span></span>

### <a name="create-reports-for-workload-cost-simulation-analysis"></a><span data-ttu-id="f461e-159">워크로드 비용 시뮬레이션 분석에 대한 보고서 만들기</span><span class="sxs-lookup"><span data-stu-id="f461e-159">Create Reports for Workload Cost Simulation Analysis</span></span>
<span data-ttu-id="f461e-160">사용량이 수집되고 Cloud Cruiser 데이터베이스에 요금이 로드된 후에, 원하는 워크로드 비용 시뮬레이션을 만들도록 Cloud Cruiser Insights 모듈을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-160">After the usage is collected and charges are loaded into the Cloud Cruiser database, we can leverage the Cloud Cruiser Insights module to create the workload cost simulation that we desire.</span></span>

<span data-ttu-id="f461e-161">이 시나리오를 설명하기 위해 다음 보고서를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-161">In order to demonstrate this scenario, we created the following report:</span></span>

<span data-ttu-id="f461e-162">![비용 비교][9]</span><span class="sxs-lookup"><span data-stu-id="f461e-162">![Cost Comparison][9]</span></span>

<span data-ttu-id="f461e-163">맨 위 그래프는 WAP(진한 파랑) 및 Azure(연한 파랑) 간의 각 서비스에 대해 워크로드를 실행하는 가격을 비교하는 서비스별 비용 비교를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-163">The top graph shows a cost comparison by services, comparing the price of running the workload for each specific service between WAP (dark blue) and Azure (light blue).</span></span>

<span data-ttu-id="f461e-164">맨 아래 그래프는 동일한 데이터를 보여주지만 부서별로 나뉘어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-164">The bottom graph shows the same data but broken down by department.</span></span> <span data-ttu-id="f461e-165">WAP 및 Azure에서 각 부서가 워크로드를 실행하는 비용과 함께 Savings(절감액) 막대(녹색)에 부서들간의 차이를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-165">This shows the costs for each department to run their workload on WAP and Azure, along with the difference between them in the Savings bar (green).</span></span>

## <a name="azure-usage-api"></a><span data-ttu-id="f461e-166">Azure 사용량 API</span><span class="sxs-lookup"><span data-stu-id="f461e-166">Azure Usage API</span></span>
### <a name="introduction"></a><span data-ttu-id="f461e-167">소개</span><span class="sxs-lookup"><span data-stu-id="f461e-167">Introduction</span></span>
<span data-ttu-id="f461e-168">Microsoft는 최근에 Azure 사용량 API를 도입했습니다. 이제 구독자는 사용량 데이터를 프로그래밍 방식으로 가져와서 소비량을 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-168">Microsoft recently introduced the Azure Usage API, allowing subscribers to programmatically pull in usage data to gain insights into their consumption.</span></span> <span data-ttu-id="f461e-169">클라우드 크루저 고객은 이 API를 통해 제공되는 풍부한 데이터 집합의 장점을 활용할 수 있게 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-169">This is great news for Cloud Cruiser customers that can take advantage of the richer dataset available through this API.</span></span>

<span data-ttu-id="f461e-170">클라우드 크루저는 사용량 API와의 통합을 다양한 방법으로 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-170">Cloud Cruiser can leverage the integration with the Usage API in several ways.</span></span> <span data-ttu-id="f461e-171">API를 통해 제공되는 세분성(시간당 사용량 정보) 및 리소스 메타데이터 정보는 유연한 쇼백 또는 차지백 모델을 지원하는 데 필요한 데이터 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-171">The granularity (hourly usage information) and resource metadata information available through the API provides the necessary dataset to support flexible Showback or Chargeback models.</span></span> 

<span data-ttu-id="f461e-172">이 자습서에서는 클라우드 크루저에 사용량 API 정보를 활용하는 예를 하나 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-172">In this tutorial, we will present one example of how Cloud Cruiser can benefit from the Usage API information.</span></span> <span data-ttu-id="f461e-173">보다 구체적으로 설명하자면, Azure에서 리소스 그룹을 만들고, 계정 구조에 대한 태그를 연결한 다음 Cloud Cruiser로 태그 정보를 가져와서 처리하는 과정을 설명할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-173">More specifically, we will create a Resource Group on Azure, associate tags for the account structure, then describe the process of pulling and processing the tag information into Cloud Cruiser.</span></span>

<span data-ttu-id="f461e-174">최종 목표는 아래와 같은 보고서를 만들고 태그로 채워진 계정 구조를 기반으로 비용 및 소비량을 분석할 수 있는 역량을 기르는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-174">The final goal is to be able to create reports like the following one, and be able to analyze cost and consumption based on the account structure populated by the tags.</span></span>

<span data-ttu-id="f461e-175">![그림 10 - 태그를 사용하는 명세 포함 보고서][10]</span><span class="sxs-lookup"><span data-stu-id="f461e-175">![Figure 10 - Report with breakdowns using tags][10]</span></span>

### <a name="microsoft-azure-tags"></a><span data-ttu-id="f461e-176">Microsoft Azure 태그</span><span class="sxs-lookup"><span data-stu-id="f461e-176">Microsoft Azure Tags</span></span>
<span data-ttu-id="f461e-177">Azure 사용량 API를 통해 제공되는 데이터는 소비량 정보뿐만 아니라 정보에 연결된 모든 태그를 비롯한 리소스 메타데이터도 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-177">The data available through the Azure Usage API includes not only consumption information, but also resource metadata including any tags associated with it.</span></span> <span data-ttu-id="f461e-178">태그는 리소스를 구성할 수 있는 간단한 방법을 제공하지만 효율성을 높이려면 다음 사항에 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-178">Tags provide an easy way to organize your resources, but in order to be effective, you need to ensure that:</span></span>

* <span data-ttu-id="f461e-179">프로비전 시 태그를 리소스에 올바르게 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-179">Tags are correctly applied to the resources at provision time</span></span>
* <span data-ttu-id="f461e-180">쇼백/차지백 프로세스에서 태그를 올바르게 사용하여 사용량을 조직의 계정 구조에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-180">Tags are properly used on the Showback/Chargeback process to tie the usage to the organization’s account structure.</span></span>

<span data-ttu-id="f461e-181">특히 프로비전 또는 과금 측면에서 수동 프로세스가 있는 경우 이러한 두 가지 요구 사항을 만족하기가 까다로울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-181">Both of these requirements can be challenging, especially when there is a manual process on the provision or charging side.</span></span> <span data-ttu-id="f461e-182">고객이 태그를 사용할 때 제기하는 가장 흔한 불만은 태그 철자 오류, 부정확한 태그 또는 태그 누락이며, 이러한 오류는 과금 업무를 매우 어렵게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-182">Mistyped, incorrect or even missing tags are common complaints from customers when using tags and these errors can make life on the charging side very difficult.</span></span>

<span data-ttu-id="f461e-183">새로운 Azure 사용량 API를 사용하면 Cloud Cruiser에서 리소스 태그 지정 정보를 가져오고, 워크북이라고 하는 정교한 ETL 도구를 통해 이러한 일반적인 태그 지정 오류를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-183">With the new Azure Usage API, Cloud Cruiser can pull resource tagging information, and through a sophisticated ETL tool called workbooks, fix these common tagging errors.</span></span> <span data-ttu-id="f461e-184">정규식과 데이터 상관관계를 사용하는 변환을 통해 Cloud Cruiser는 태그가 잘못 지정된 리소스를 식별하고, 올바른 태그를 적용하고, 리소스와 소비자를 올바르게 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-184">Through transformation using regular expressions and data correlation, Cloud Cruiser can identify incorrectly tagged resources and apply the correct tags, ensuring the correct association of the resources with the consumer.</span></span>

<span data-ttu-id="f461e-185">과금 측면에서 클라우드 크루저는 쇼백/차지백 프로세스를 자동화하고, 태그 정보를 활용하여 사용량을 올바른 소비자(부서, 분과, 프로젝트 등)에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-185">On the charging side, Cloud Cruiser automates the Showback/Chargeback process, and can leverage the tag information to tie the usage to the appropriate consumer (Department, Division, Project, etc.).</span></span> <span data-ttu-id="f461e-186">이 자동화를 통해 효율을 대폭 향상할 수 있을 뿐 아니라 일관적이고 감사 가능한 과금 프로세스를 보장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-186">This automation provides a huge improvement and can ensure a consistent and auditable charging process.</span></span>

### <a name="creating-a-resource-group-with-tags-on-microsoft-azure"></a><span data-ttu-id="f461e-187">Microsoft Azure에서 태그를 사용하여 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="f461e-187">Creating a Resource Group with tags on Microsoft Azure</span></span>
<span data-ttu-id="f461e-188">이 자습서의 첫 번째 단계는 Azure Portal에서 리소스 그룹을 만든 후 새 태그를 만들어서 리소스에 연결하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-188">The first step in this tutorial is to create a Resource Group in the Azure portal, then create new tags to associate to the resources.</span></span> <span data-ttu-id="f461e-189">이 예에서 우리가 만들 태그는 부서, 환경, 소유자, 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-189">For this example, we will be creating the following tags: Department, Environment, Owner, Project.</span></span>

<span data-ttu-id="f461e-190">아래는 태그가 연결된 샘플 리소스 그룹을 보여주는 스크린샷입니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-190">The screenshot below shows a sample Resource Group with the associated tags.</span></span>

<span data-ttu-id="f461e-191">![그림 11 - Azure 포털의 태그가 연결된 리소스 그룹l][11]</span><span class="sxs-lookup"><span data-stu-id="f461e-191">![Figure 11 - Resource Group with associated tags on Azure portal][11]</span></span>

<span data-ttu-id="f461e-192">다음 단계는 사용량 API에서 클라우드 크루저로 정보를 가져오는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-192">The next step is to pull the information from the Usage API into Cloud Cruiser.</span></span> <span data-ttu-id="f461e-193">현재 사용량 API는 JSON 형식으로 응답을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-193">The Usage API currently provides responses in JSON format.</span></span> <span data-ttu-id="f461e-194">다음은 검색되는 데이터 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-194">Here is a sample of the data retrieved:</span></span>

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


### <a name="import-data-from-the-usage-api-into-cloud-cruiser"></a><span data-ttu-id="f461e-195">사용량 API에서 클라우드 크루저로 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="f461e-195">Import data from the Usage API into Cloud Cruiser</span></span>
<span data-ttu-id="f461e-196">클라우드 크루저 워크북은 사용량 API에서 정보를 수집하고 처리하는 자동화된 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-196">Cloud Cruiser workbooks provide an automated way to collect and process information from the Usage API.</span></span> <span data-ttu-id="f461e-197">ETL(추출-변환-로드) 워크북을 사용하면 클라우드 크루저 데이터베이스에서 데이터를 수집, 변환 및 게시하도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-197">An ETL (extract-transform-load) workbook allows you to configure the collection, transformation, and publishing of data into the Cloud Cruiser database.</span></span>

<span data-ttu-id="f461e-198">각 워크북은 하나 또는 여러 컬렉션을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-198">Each workbook can have one or multiple collections.</span></span> <span data-ttu-id="f461e-199">이를 사용하여 사용 데이터를 보완하거나 보강할 다른 소스에서 정보를 상호 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-199">This allows you to correlate information from different sources to complement or augment the usage data.</span></span> <span data-ttu-id="f461e-200">이 예에서는 Azure 탬플릿 워크북에서 새 시트(*UsageAPI)*를 만들고 사용량 API의 정보를 가져오는 새 *컬렉션*을 설정할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-200">For this example, we will create a new sheet in the Azure template workbook (*UsageAPI)* and set a new *collection* to import information from the Usage API.</span></span>

<span data-ttu-id="f461e-201">![그림 3 - UsageAPI 시트로 가져온 사용량 API 데이터][12]</span><span class="sxs-lookup"><span data-stu-id="f461e-201">![Figure 3 - Usage API data imported into the UsageAPI sheet][12]</span></span>

<span data-ttu-id="f461e-202">이 워크북에는 Azure에서 서비스를 가져오는 시트(*ImportServices*)와 청구 API의 소비량 정보를 처리하는 시트(*PublishData*)가 이미 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-202">Notice that this workbook already has other sheets to import services from Azure (*ImportServices*), and process the consumption information from the Billing API (*PublishData*).</span></span>

<span data-ttu-id="f461e-203">다음은 사용량 API를 사용하여 *UsageAPI* 시트를 채우고 그 정보를 *PublishData* 시트에서 청구 API의 소비 데이터와 상호 연결하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-203">Next we will use the Usage API to populate the *UsageAPI* sheet, and correlate the information with the consumption data from the Billing API on the *PublishData* sheet.</span></span>

### <a name="processing-the-tag-information-from-the-usage-api"></a><span data-ttu-id="f461e-204">사용량 API의 태그 정보 처리</span><span class="sxs-lookup"><span data-stu-id="f461e-204">Processing the tag information from the Usage API</span></span>
<span data-ttu-id="f461e-205">워크북으로 데이터를 가져온 후에는 API의 정보를 처리할 수 있도록 *UsageAPI* 시트에서 변환 단계를 만들 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-205">After importing the data into the workbook, we will create transformation steps in the *UsageAPI* sheet in order to process the information from the API.</span></span> <span data-ttu-id="f461e-206">첫 번째 단계는 "JSON 분할" 프로세서를 사용하여 단일 필드에서 태그를 추출하고 각 태그(부서, 프로젝트, 소유자 및 환경)에 대한 필드를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-206">First step is to use a “JSON split” processor to extract the tags from a single field, then create fields for each one of them (Department, Project, Owner, and Environment).</span></span>

<span data-ttu-id="f461e-207">![그림 4 - 태그 정보에 대한 새 필드 만들기][13]</span><span class="sxs-lookup"><span data-stu-id="f461e-207">![Figure 4 - Create new fields for the tag information][13]</span></span>

<span data-ttu-id="f461e-208">"네트워킹" 서비스에는 태그 정보가 없습니다(노란색 상자). 하지만 *ResourceGroupName* 필드를 살펴보면 이 서비스가 동일한 리소스 그룹에 속한 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-208">Notice the “Networking” service is missing the tag information (yellow box), but we can verify that it is part of the same Resource Group by looking at the *ResourceGroupName* field.</span></span> <span data-ttu-id="f461e-209">이 리소스 그룹의 다른 리소스에 대한 태그를 갖고 있으므로 나중에 이 정보를 사용하여 누락된 태그를 이 리소스에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-209">Since we have the tags for the other resources from this Resource Group, we can use this information to apply the missing tags to this resource later in the process.</span></span>

<span data-ttu-id="f461e-210">다음 단계는 태그의 정보를 *ResourceGroupName*에 연결하는 조회 테이블을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-210">The next step is to create a lookup table associating the information from the tags to the *ResourceGroupName*.</span></span> <span data-ttu-id="f461e-211">이 조회 테이블은 다음 단계에서 태그 정보를 사용하여 소비량 데이터를 보강하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-211">This lookup table will be used on the next step to enrich the consumption data with tag information.</span></span>

### <a name="adding-the-tag-information-to-the-consumption-data"></a><span data-ttu-id="f461e-212">소비량 데이터에 태그 정보 추가</span><span class="sxs-lookup"><span data-stu-id="f461e-212">Adding the tag information to the consumption data</span></span>
<span data-ttu-id="f461e-213">이제 청구 API의 소비량 정보를 처리하는 *PublishData* 시트로 넘어가서, 태그에서 추출한 필드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-213">Now we can jump to the *PublishData* sheet, which processes the consumption information from the Billing API, and add the fields extracted from the tags.</span></span> <span data-ttu-id="f461e-214">이 프로세스는 이전 단계에서 만든 조회 테이블을 확인 하여 수행됩니다. 조회에 대한 키로 *ResourceGroupName*을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-214">This process is performed by looking at the lookup table created on the previous step, using the *ResourceGroupName* as the key for the lookups.</span></span>

<span data-ttu-id="f461e-215">![그림 5 - 조회 정보로 계정 구조 채우기][14]</span><span class="sxs-lookup"><span data-stu-id="f461e-215">![Figure 5 - Populating the account structure with the information from the lookups][14]</span></span>

<span data-ttu-id="f461e-216">"네트워킹" 서비스에 대한 올바른 계정 구조 필드를 적용하여 태그 누락 문제를 해결했습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-216">Notice that the appropriate account structure fields for the “Networking” service were applied, fixing the issue with the missing tags.</span></span> <span data-ttu-id="f461e-217">또한 보고서에서 쉽게 구분할 수 있도록 대상 리소스 그룹이 아닌 리소스의 계정 구조 필드를 "기타"로 채웠습니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-217">We also populated the account structure fields for resources other than our target Resource Group with “Other”, in order to differentiate them on the reports.</span></span>

<span data-ttu-id="f461e-218">이제 사용량 데이터를 게시하는 단계를 추가하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-218">Now we just need to add a step to publish the usage data.</span></span> <span data-ttu-id="f461e-219">이 단계에서는 요금제에 정의된 각 서비스의 적절한 요금을 사용량 정보에 적용할 것이며, 그 결과로 얻은 요금은 데이터베이스에 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-219">During this step, the appropriate rates for each service defined on our Rate Plan will be applied to the usage information, with the resulting charge loaded into the database.</span></span>

<span data-ttu-id="f461e-220">무엇보다도 이 프로세스를 한 번만 진행하면 된다는 점이 가장 큰 장점입니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-220">The best part is that you only have to go through this process once.</span></span> <span data-ttu-id="f461e-221">워크북이 완성되면 스케줄러에 워크북을 추가하기만 하면 예약된 일정에 따라 매시간 또는 매일 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-221">When the workbook is completed, you just need to add it to the scheduler and it will run hourly or daily at the scheduled time.</span></span> <span data-ttu-id="f461e-222">이제 데이터를 분석하여 클라우드 사용량에 대한 의미 있는 정보를 얻고 싶다면 새 보고서를 만들거나 기존 보고서를 사용자 지정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-222">Then it’s just a matter of creating new reports, or customizing existing ones, in order to analyze the data to get meaningful insights from your cloud usage.</span></span>

### <a name="next-steps"></a><span data-ttu-id="f461e-223">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f461e-223">Next Steps</span></span>
* <span data-ttu-id="f461e-224">Cloud Cruiser 워크북 및 보고서를 만드는 방법에 대한 자세한 지침은 Cloud Cruiser 온라인 [설명서](http://docs.cloudcruiser.com/) (유효한 로그인 필요)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="f461e-224">For detailed instructions on creating Cloud Cruiser workbooks and reports, please refer to Cloud Cruiser’s online [documentation](http://docs.cloudcruiser.com/) (valid login required).</span></span>  <span data-ttu-id="f461e-225">Cloud Cruiser에 대한 자세한 내용은 [info@cloudcruiser.com](mailto:info@cloudcruiser.com)에 연결하는 조회 테이블을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-225">For more information about Cloud Cruiser, please contact [info@cloudcruiser.com](mailto:info@cloudcruiser.com).</span></span>
* <span data-ttu-id="f461e-226">Azure 리소스 사용 및 RateCard API에 대한 개요는 [Microsoft Azure 리소스 소비에 대한 통찰력 얻기](billing-usage-rate-card-overview.md)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="f461e-226">See [Gain insights into your Microsoft Azure resource consumption](billing-usage-rate-card-overview.md) for an overview of the Azure Resource Usage and RateCard APIs.</span></span>
* <span data-ttu-id="f461e-227">두 API에 대한 정보는 [Azure 청구 REST API 참조](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c)를 확인하십시오. 이는 Azure Resource Manager에서 제공하는 API 집합의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="f461e-227">Check out the [Azure Billing REST API Reference](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) for more information on both APIs, which are part of the set of APIs provided by the Azure Resource Manager.</span></span>
* <span data-ttu-id="f461e-228">샘플 코드를 곧바로 시작하려면 [Azure 코드 샘플](https://azure.microsoft.com/documentation/samples/?term=billing)의 Microsoft Azure 청구 API 코드 샘플을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="f461e-228">If you would like to dive right into the sample code, check out our Microsoft Azure Billing API Code Samples on [Azure Code Samples](https://azure.microsoft.com/documentation/samples/?term=billing).</span></span>

### <a name="learn-more"></a><span data-ttu-id="f461e-229">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="f461e-229">Learn More</span></span>
* <span data-ttu-id="f461e-230">Azure 리소스 관리자에 대한 자세한 내용은 [Azure 리소스 관리자 개요](../azure-resource-manager/resource-group-overview.md)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="f461e-230">See the [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md) article to learn more about the Azure Resource Manager.</span></span>

<!--Image references-->

<span data-ttu-id="f461e-231">[1]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Create-New-Workbook-Collection.png "그림 1-새 컬렉션 만들기"</span><span class="sxs-lookup"><span data-stu-id="f461e-231">[1]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Create-New-Workbook-Collection.png "Figure 1 - Creating a new collection"</span></span>
<span data-ttu-id="f461e-232">[2]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Import-Data-From-RateCard.png "그림 2-새 컬렉션에서 데이터 가져오기"</span><span class="sxs-lookup"><span data-stu-id="f461e-232">[2]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Import-Data-From-RateCard.png "Figure 2 - Import data from the new collection"</span></span>
<span data-ttu-id="f461e-233">[3]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Transformation-Steps-Process-RateCard-Data.png "그림 3-RateCard API에서 수집된 데이터를 처리하는 변환 단계"</span><span class="sxs-lookup"><span data-stu-id="f461e-233">[3]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Transformation-Steps-Process-RateCard-Data.png "Figure 3 - Transformation steps to process collected data from RateCard API"</span></span>
<span data-ttu-id="f461e-234">[4]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Publish-RateCard-Data-New-Services-Rates.png "그림 4-새 서비스 및 요금 RateCard API에 데이터 게시"</span><span class="sxs-lookup"><span data-stu-id="f461e-234">[4]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Publish-RateCard-Data-New-Services-Rates.png "Figure 4 - Publishing the data from the RateCard API as new Services and Rates"</span></span>
<span data-ttu-id="f461e-235">[5]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Verify-Azure-Services-And-Pricing1.png "그림 5-새로운 서비스 확인"</span><span class="sxs-lookup"><span data-stu-id="f461e-235">[5]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Verify-Azure-Services-And-Pricing1.png "Figure 5 - Verifying the new Services"</span></span>
<span data-ttu-id="f461e-236">[6]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Verify-Azure-Services-And-Pricing2.png "그림 6-새 요금제와 연결된 요금 확인"</span><span class="sxs-lookup"><span data-stu-id="f461e-236">[6]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Verify-Azure-Services-And-Pricing2.png "Figure 6 - Verifying the new Rate Plan and associated rates"</span></span>
<span data-ttu-id="f461e-237">[7]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Transforming-WAP-Normalize-Services.png "그림 7-서비스를 정규화하는 WAP 데이터 변환"</span><span class="sxs-lookup"><span data-stu-id="f461e-237">[7]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Transforming-WAP-Normalize-Services.png "Figure 7 - Transforming WAP data to normalize services"</span></span>
<span data-ttu-id="f461e-238">[8]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Workbook-Scheduling.png "그림 8- 워크북 예약"</span><span class="sxs-lookup"><span data-stu-id="f461e-238">[8]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Workbook-Scheduling.png "Figure 8 - Workbook scheduling"</span></span>
<span data-ttu-id="f461e-239">[9]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Workload-Cost-Simulation-Report.png "그림 9- 워크로드 비용 비교 시나리오에 대한 예제 보고서"</span><span class="sxs-lookup"><span data-stu-id="f461e-239">[9]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Workload-Cost-Simulation-Report.png "Figure 9 - Sample Report for the Workload cost comparison scenario"</span></span>
<span data-ttu-id="f461e-240">[10]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/1_ReportWithTags.png "그림 10 - 태그를 사용하는 명세 포함 보고서"</span><span class="sxs-lookup"><span data-stu-id="f461e-240">[10]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/1_ReportWithTags.png "Figure 10 - Report with breakdowns using tags"</span></span>
<span data-ttu-id="f461e-241">[11]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/2_ResourceGroupsWithTags.png "그림 11 - Azure 포털의 태그가 연결된 리소스 그룹"</span><span class="sxs-lookup"><span data-stu-id="f461e-241">[11]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/2_ResourceGroupsWithTags.png "Figure 11 - Resource Group with associated tags on Azure portal"</span></span>
<span data-ttu-id="f461e-242">[12]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/3_ImportIntoUsageAPISheet.png "그림 12 - UsageAPI 시트로 가져온 사용량 API 데이터"</span><span class="sxs-lookup"><span data-stu-id="f461e-242">[12]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/3_ImportIntoUsageAPISheet.png "Figure 12 - Usage API data imported into the UsageAPI sheet"</span></span>
<span data-ttu-id="f461e-243">[13]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/4_NewTagField.png "그림 13 - 태그 정보에 대한 새 필드 만들기"</span><span class="sxs-lookup"><span data-stu-id="f461e-243">[13]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/4_NewTagField.png "Figure 13 - Create new fields for the tag information"</span></span>
<span data-ttu-id="f461e-244">[14]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/5_PopulateAccountStructure.png "그림 14 - 조회 정보로 계정 구조 채우기"</span><span class="sxs-lookup"><span data-stu-id="f461e-244">[14]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/5_PopulateAccountStructure.png "Figure 14 - Populating the account structure with the information from the lookups"</span></span>
