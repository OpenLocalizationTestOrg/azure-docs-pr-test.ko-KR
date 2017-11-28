---
title: "미리 구성된 예측 유지 관리 솔루션 | Microsoft Docs"
description: "Azure IoT Suite 예측 정비 사전 구성 솔루션에 대한 설명입니다."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: b370b3d7-2ce5-4906-9818-3aeedd471ee3
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 8bad198488c4940a83eb32ec02122a91d47ca86c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="predictive-maintenance-preconfigured-solution-overview"></a><span data-ttu-id="08653-103">예측 정비 사전 구성 솔루션 개요</span><span class="sxs-lookup"><span data-stu-id="08653-103">Predictive maintenance preconfigured solution overview</span></span>

<span data-ttu-id="08653-104">*예측 정비* [사전 구성 솔루션][lnk_preconfigured_solutions]은 [Microsoft Azure IoT Suite][lnk_iot_suite] 사전 구성 솔루션 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="08653-104">The *predictive maintenance* [preconfigured solution][lnk_preconfigured_solutions] is one of the [Microsoft Azure IoT Suite][lnk_iot_suite] preconfigured solutions.</span></span> <span data-ttu-id="08653-105">이 솔루션은 실시간 장치 원격 분석 컬렉션과 [Azure Machine Learning][lnk-machine-learning]을 사용하여 생성되는 예측 모델을 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="08653-105">This solution integrates real-time device telemetry collection with a predictive model created using [Azure Machine Learning][lnk-machine-learning].</span></span>

<span data-ttu-id="08653-106">사용자는 Azure IoT Suite를 통해 신속하고 간편하게 연결되고 자산을 모니터링하며 실시간으로 원격 분석 데이터를 대시보드 및 시각적 개체로 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08653-106">With Azure IoT Suite, you can quickly and easily connect to and monitor assets, and analyze telemetry in real time in dashboards and visualizations.</span></span> <span data-ttu-id="08653-107">예측 유지 관리 솔루션에서 대시보드와 시각화는 효율을 증진하고 매출원을 향상시킬 수 있는 새로운 인텔리전스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="08653-107">In the predictive maintenance solution, the dashboards and visualizations provide you with new intelligence that can drive efficiencies and enhance revenue streams.</span></span>

## <a name="the-scenario"></a><span data-ttu-id="08653-108">시나리오</span><span class="sxs-lookup"><span data-stu-id="08653-108">The Scenario</span></span>

<span data-ttu-id="08653-109">Fabrikam은 경쟁력 있는 가격으로 우수한 고객 경험을 제공하는 데 중점을 두고 있는 지역 항공사입니다.</span><span class="sxs-lookup"><span data-stu-id="08653-109">Fabrikam is a regional airline that focuses on great customer experience at competitive prices.</span></span> <span data-ttu-id="08653-110">항공기 지연의 이유 중 하나는 정비 문제이며 항공 엔진 정비는 특히 어려운 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="08653-110">One cause of flight delays is maintenance issues and aircraft engine maintenance is particularly challenging.</span></span> <span data-ttu-id="08653-111">Fabrikam은 비행 중 엔진 고장은 어떻게 해서든 막아야 하기 때문에 엔진을 정기적으로 조사하고 계획에 따라 유지 관리 일정을 예약합니다.</span><span class="sxs-lookup"><span data-stu-id="08653-111">Fabrikam must avoid engine failure during flight at all costs, so it inspects its engines regularly and schedules maintenance according to a plan.</span></span> <span data-ttu-id="08653-112">하지만 항공기 엔진이 항상 동일하게 마모되는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="08653-112">However, aircraft engines don’t always wear the same.</span></span> <span data-ttu-id="08653-113">엔진에 대해 필요 이상의 정비를 수행하는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08653-113">Some unnecessary maintenance is performed on engines.</span></span> <span data-ttu-id="08653-114">무엇보다, 정비가 수행될 때까지 항공기를 이륙할 수 없는 문제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="08653-114">More importantly, issues arise which can ground an aircraft until maintenance is performed.</span></span> <span data-ttu-id="08653-115">적당한 기술자나 예비 부품이 없는 곳에 항공기가 있는 경우에는 특히 비용이 많이 드는 문제를 유발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08653-115">If an aircraft is at a location where the right technicians or spare parts are not available, these issues can be especially costly.</span></span>

<span data-ttu-id="08653-116">Fabrikam 항공기의 엔진에는 비행 중에 엔진 상태를 모니터링하는 센서가 달려 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08653-116">The engines of Fabrikam’s aircraft are instrumented with sensors that monitor engine conditions during flight.</span></span> <span data-ttu-id="08653-117">Fabrikam은 비행 중 수집된 센서 데이터를 수집하는 예측 유지 관리 솔루션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="08653-117">Fabrikam uses the predictive maintenance solution to collect the sensor data collected during the flight.</span></span> <span data-ttu-id="08653-118">Fabrikam의 데이터 과학자들은 엔진 작동 및 고장 데이터를 다년간 축적한 후에 항공기 엔진의 잔여 수명(Remaining Useful Life, RUL)을 예측하는 방식을 모델링했습니다.</span><span class="sxs-lookup"><span data-stu-id="08653-118">After accumulating years of engine operational and failure data, Fabrikam’s data scientists have modeled a way to predict the Remaining Useful Life (RUL) of an aircraft engine.</span></span> <span data-ttu-id="08653-119">이 모델은 4개 엔진 센서의 데이터와 우발적인 고장으로 이어지는 엔진 마모 사이의 상관 관계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="08653-119">The model uses a correlation between data from four of the engine sensors and engine wear that leads to eventual failure.</span></span> <span data-ttu-id="08653-120">Fabrikam은 안전을 보장하기 위하여 정기적인 정밀 검사를 계속 수행하는 한편, 이 모델을 통해 비행이 끝날 때마다 각 엔진에 대한 RUL을 계산할 수 있게 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="08653-120">While Fabrikam continues to perform regular inspections to ensure safety, it can now use the models to compute the RUL for each engine after every flight.</span></span> <span data-ttu-id="08653-121">모델은 비행 중 엔진에서 수집한 원격 분석 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="08653-121">The model uses the telemetry collected from the engines during the flight.</span></span> <span data-ttu-id="08653-122">Fabrikam은 이제 향후 고장 시점을 예측하고 정비 및 수리를 사전에 계획할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08653-122">Fabrikam can now predict future points of failure and plan for maintenance and repair in advance.</span></span>

> [!NOTE]
> <span data-ttu-id="08653-123">솔루션 모델은 실제 엔진 마모 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="08653-123">The solution model uses actual engine wear data.</span></span>

<span data-ttu-id="08653-124">정비가 필요한 시점을 예측함으로써, Fabrikam은 비용을 줄이도록 운영을 최적화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08653-124">By predicting the point when maintenance is required, Fabrikam can optimize its operations to reduce costs.</span></span>

<span data-ttu-id="08653-125">유지 관리 코디네이터는 다음 작업을 수행하도록 스케줄러와 함께 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="08653-125">Maintenance coordinators work with schedulers to:</span></span>

- <span data-ttu-id="08653-126">특정 위치에서 중지하는 항공기와 일치하도록 유지 관리를 계획합니다.</span><span class="sxs-lookup"><span data-stu-id="08653-126">Plan maintenance to coincide with an aircraft stopping at a particular location.</span></span>
- <span data-ttu-id="08653-127">일정 중단 없이 항공기가 서비스되지 않을 충분한 시간을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="08653-127">Ensure sufficient time is available for the aircraft to be out of service without causing schedule disruption.</span></span>
- <span data-ttu-id="08653-128">대기 시간 없이 항공기를 충분히 정비할 수 있도록 기술자의 일정을 예약합니다.</span><span class="sxs-lookup"><span data-stu-id="08653-128">To schedule technicians to ensure that aircraft are serviced efficiently without wait time.</span></span>

<span data-ttu-id="08653-129">재고 관리자는 정비 계획을 수신하기 때문에 주문 공정 및 예비 부품 재고를 최적화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08653-129">Inventory control managers receive maintenance plans, so they can optimize their ordering process and spare parts inventory.</span></span>

<span data-ttu-id="08653-130">이러한 활동을 통하여 Fabrikam은 승객과 승무원의 안전을 보장하면서 항공기 지상 체류 시간을 최소화하고 운영비를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08653-130">These activities enable Fabrikam to minimize aircraft ground time and reduce operating costs while ensuring the safety of passengers and crew.</span></span>

<span data-ttu-id="08653-131">[Azure IoT Suite][lnk_iot_suite]가 고객에게 필요한 기능을 제공하는 방식을 이해하려면 예측 정비의 잠재력을 깨달을 필요가 있습니다. 이 내용은 [infographic][lnk_infographic]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="08653-131">To understand how [Azure IoT Suite][lnk_iot_suite] provides the capabilities customers need to realize the potential of predictive maintenance, review this [infographic][lnk_infographic].</span></span>

## <a name="how-the-predictive-maintenance-solution-is-built"></a><span data-ttu-id="08653-132">예측 정비 솔루션이 구축되는 방식</span><span class="sxs-lookup"><span data-stu-id="08653-132">How the predictive maintenance solution is built</span></span>

<span data-ttu-id="08653-133">솔루션은 템플릿으로 사용할 수 있는 기존의 Azure Machine Learning을 사용하여 IoT Suite 서비스를 통해 수집되는 장치 원격 분석에서 작동하는 이러한 기능을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="08653-133">The solution uses an existing Azure Machine Learning model available as a template to show these capabilities working from device telemetry collected through IoT Suite services.</span></span> <span data-ttu-id="08653-134">Microsoft는 공개적으로 사용 가능한 데이터<sup>\[1\]</sup>을 기반으로 하는 항공기 엔진의 [회귀 모델][lnk_regression_model] 및 해당 모델을 사용하는 방법에 대한 단계별 지침을 구축했습니다.</span><span class="sxs-lookup"><span data-stu-id="08653-134">Microsoft has built a [regression model][lnk_regression_model] of an aircraft engine based on publically available data<sup>\[1\]</sup>, and step-by-step guidance on how to use the model.</span></span>

<span data-ttu-id="08653-135">Azure IoT 예측 유지 관리 솔루션은 이 템플릿에서 만든 회귀 모델을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="08653-135">The Azure IoT predictive maintenance solution uses the regression model created from this template.</span></span> <span data-ttu-id="08653-136">모델은 Azure 구독에 배포되고 자동으로 생성된 API를 통해 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="08653-136">The model is deployed into your Azure subscription and exposed through an automatically generated API.</span></span> <span data-ttu-id="08653-137">이 솔루션은 4개(총 100개 중)의 엔진을 나타내는 테스트 데이터의 하위 집합과 4개(총 21개 중)의 센서 데이터 스트림을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="08653-137">The solution includes a subset of the testing data representing 4 (of 100 total) engines and the 4 (of 21 total) sensor data streams.</span></span> <span data-ttu-id="08653-138">이 데이터는 학습된 모델을 통해 정확한 결과를 제공하는 데 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="08653-138">This data is sufficient to provide an accurate result from the trained model.</span></span>

<span data-ttu-id="08653-139">*\[1\] A. Saxena and K. Goebel(2008). "Turbofan 엔진 성능 저하 시뮬레이션 데이터 집합", NASA Ames Prognostics Data Repository(http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*</span><span class="sxs-lookup"><span data-stu-id="08653-139">*\[1\] A. Saxena and K. Goebel (2008). "Turbofan Engine Degradation Simulation Data Set", NASA Ames Prognostics Data Repository (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*</span></span>

## <a name="get-started-with-predictive-maintenance"></a><span data-ttu-id="08653-140">예측 유지 관리 시작</span><span class="sxs-lookup"><span data-stu-id="08653-140">Get started with predictive maintenance</span></span>

<span data-ttu-id="08653-141">이 자습서에서는 예측 유지 관리 솔루션을 프로비전하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="08653-141">This tutorial shows you how to provision the predictive maintenance solution.</span></span> <span data-ttu-id="08653-142">또한 예측 유지 관리 솔루션의 기본 기능을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="08653-142">It also walks you through the basic features of the predictive maintenance solution.</span></span> <span data-ttu-id="08653-143">미리 구성된 솔루션과 함께 배포한 솔루션 대시보드를 통해 이러한 기능 다수에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08653-143">You can access many of these features through the solution dashboard that deploys along with the preconfigured solution.</span></span>

<span data-ttu-id="08653-144">이 자습서를 완료하려면 활성 Azure 구독이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="08653-144">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="08653-145">계정이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08653-145">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="08653-146">자세한 내용은 [Azure 무료 평가판][lnk_free_trial]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="08653-146">For details, see [Azure Free Trial][lnk_free_trial].</span></span>

1. <span data-ttu-id="08653-147">Azure 계정 자격 증명을 사용하여 [azureiotsuite.com][lnk-azureiotsuite]에 로그온한 다음 **+**를 클릭하여 솔루션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="08653-147">Log on to [azureiotsuite.com][lnk-azureiotsuite] using your Azure account credentials, and click **+** to create a solution.</span></span>
1. <span data-ttu-id="08653-148">**예측 유지 관리** 타일 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="08653-148">Click **Select** the **Predictive maintenance** tile.</span></span>
1. <span data-ttu-id="08653-149">예측 정비 사전 구성 솔루션에 **솔루션 이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="08653-149">Enter a **Solution name** for your predictive maintenance preconfigured solution.</span></span>
1. <span data-ttu-id="08653-150">솔루션을 프로비전하는 데 사용할 **지역** 및 **구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="08653-150">Select the **Region** and **Subscription** you want to use to provision the solution.</span></span>
1. <span data-ttu-id="08653-151">**솔루션 만들기** 를 클릭하여 프로비전 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="08653-151">Click **Create Solution** to begin the provisioning process.</span></span> <span data-ttu-id="08653-152">일반적으로 이 프로세스는 실행하는 데 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="08653-152">This process typically takes several minutes to run.</span></span>

### <a name="wait-for-the-provisioning-process-to-complete"></a><span data-ttu-id="08653-153">프로비전 프로세스가 완료될 때까지 대기</span><span class="sxs-lookup"><span data-stu-id="08653-153">Wait for the provisioning process to complete</span></span>

1. <span data-ttu-id="08653-154">**프로비전** 상태인 솔루션 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="08653-154">Click the tile for your solution with **Provisioning** status.</span></span>
1. <span data-ttu-id="08653-155">Azure 서비스가 Azure 구독에 배포될 때 **프로비전 상태** 입니다.</span><span class="sxs-lookup"><span data-stu-id="08653-155">Notice the **Provisioning states** as Azure services are deployed in your Azure subscription.</span></span>
1. <span data-ttu-id="08653-156">프로비전이 완료되면 **준비**상태로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="08653-156">Once provisioning completes, the status changes to **Ready**.</span></span>
1. <span data-ttu-id="08653-157">타일을 클릭하여 오른쪽 창에 솔루션의 세부 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="08653-157">Click the tile to see the details of your solution in the right-hand pane.</span></span> <span data-ttu-id="08653-158">이 창에서 솔루션 대시보드를 실행하고 Machine Learning 작업 영역에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08653-158">From this pane, you can launch the solution dashboard and access the Machine Learning workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="08653-159">미리 구성된 솔루션을 배포하는 데 문제가 발생하면 [azureiotsuite.com 사이트에 대한 사용 권한][lnk-permissions] 및 [FAQ][lnk-faq]를 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="08653-159">If you encounter issues deploying the preconfigured solution, review [Permissions on the azureiotsuite.com site][lnk-permissions] and the [FAQ][lnk-faq].</span></span> <span data-ttu-id="08653-160">문제가 지속되면 [포털][lnk-portal]에서 서비스 티켓을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="08653-160">If the issues persist, create a service ticket on the [portal][lnk-portal].</span></span>

<span data-ttu-id="08653-161">목록에는 없지만 솔루션에 대해 참조하고 싶은 세부 정보가 있나요?</span><span class="sxs-lookup"><span data-stu-id="08653-161">Are there details you'd expect to see that aren't listed for your solution?</span></span> <span data-ttu-id="08653-162">[사용자 의견](https://feedback.azure.com/forums/321918-azure-iot)에 기능 제안을 보내주세요.</span><span class="sxs-lookup"><span data-stu-id="08653-162">Give us feature suggestions on [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span></span>

## <a name="view-the-solution"></a><span data-ttu-id="08653-163">솔루션 보기</span><span class="sxs-lookup"><span data-stu-id="08653-163">View the solution</span></span>

<span data-ttu-id="08653-164">이 섹션에서는 솔루션 UI를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="08653-164">This section guides you through the solution UI.</span></span>

### <a name="predictive-maintenance-dashboard"></a><span data-ttu-id="08653-165">대시보드에서 예측 유지 관리</span><span class="sxs-lookup"><span data-stu-id="08653-165">Predictive Maintenance Dashboard</span></span>

<span data-ttu-id="08653-166">웹 응용 프로그램의 이 페이지는 PowerBI JavaScript 제어를 사용하여([PowerBI 시각 효과 리포지토리][lnk-powerbi]를 참조) 다음을 시각화합니다.</span><span class="sxs-lookup"><span data-stu-id="08653-166">This page in the web application uses PowerBI JavaScript controls (see the [PowerBI-visuals repository][lnk-powerbi]) to visualize:</span></span>

* <span data-ttu-id="08653-167">Blob Storage의 Stream Analytics 작업에서 출력 데이터.</span><span class="sxs-lookup"><span data-stu-id="08653-167">The output data from the Stream Analytics jobs in blob storage.</span></span>
* <span data-ttu-id="08653-168">항공기 엔진 당 RUL 및 주기 수.</span><span class="sxs-lookup"><span data-stu-id="08653-168">The RUL and cycle count per aircraft engine.</span></span>

### <a name="observing-the-behavior-of-the-cloud-solution"></a><span data-ttu-id="08653-169">클라우드 솔루션의 동작 관찰</span><span class="sxs-lookup"><span data-stu-id="08653-169">Observing the behavior of the cloud solution</span></span>

<span data-ttu-id="08653-170">Azure 포털에서 선택한 솔루션 이름을 가진 리소스 그룹으로 이동하여 프로비전된 리소스를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08653-170">In the Azure portal, navigate to the resource group with the solution name you chose to view your provisioned resources.</span></span>

![][img-resource-group]

<span data-ttu-id="08653-171">미리 구성된 솔루션을 프로비전할 때 기계 학습 작업 영역에 대한 링크가 포함된 전자 메일을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="08653-171">When you provision the preconfigured solution, you receive an email with a link to the Machine Learning workspace.</span></span> <span data-ttu-id="08653-172">또한 프로비전된 솔루션에 대한 [azureiotsuite.com][lnk-azureiotsuite] 페이지에서 Machine Learning 작업 영역으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08653-172">You can also navigate to the Machine Learning workspace from the [azureiotsuite.com][lnk-azureiotsuite] page for your provisioned solution.</span></span> <span data-ttu-id="08653-173">솔루션이 **준비** 상태일 때 이 페이지에 타일이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="08653-173">A tile is available on this page when the solution is in the **Ready** state.</span></span>

![][img-machine-learning]

<span data-ttu-id="08653-174">솔루션 포털에서 항공기 당 2개의 엔진, 엔진 당 4개의 센서가 있는 2대의 항공기를 나타내는 네 가지의 시뮬레이션된 장치를 사용하여 샘플이 프로비전된 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08653-174">In the solution portal, you can see that the sample is provisioned with four simulated devices to represent two aircraft with two engines per aircraft, each with four sensors.</span></span> <span data-ttu-id="08653-175">솔루션 포털로 먼저 이동할 때 시뮬레이션이 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="08653-175">When you first navigate to the solution portal, the simulation is stopped.</span></span>

![][img-simulation-stopped]

<span data-ttu-id="08653-176">**시뮬레이션 시작**을 클릭하여 시뮬레이션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="08653-176">Click **Start simulation** to begin the simulation.</span></span> <span data-ttu-id="08653-177">센서 기록, RUL, 주기 및 RUL 기록으로 대시보드가 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="08653-177">The sensor history, RUL, Cycles, and RUL history populate the dashboard.</span></span>

![][img-simulation-running]

<span data-ttu-id="08653-178">RUL이 160(데모 목적으로 선택한 임의의 임계값) 미만인 경우, 솔루션 포털은 RUL 표시 옆에 경고 기호를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="08653-178">When RUL is less than 160 (an arbitrary threshold chosen for demonstration purposes), the solution portal displays a warning symbol next to the RUL display.</span></span> <span data-ttu-id="08653-179">또한 솔루션 포털은 항공기 엔진을 노란색으로 강조 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="08653-179">The solution portal also highlights the aircraft engine in yellow.</span></span> <span data-ttu-id="08653-180">RUL 값이 전반적으로 일반 하향 추세를 갖지만 아래 위로 요동치는 경향이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08653-180">Notice how the RUL values have a general downward trend overall, but tend to bounce up and down.</span></span> <span data-ttu-id="08653-181">이 동작은 다양한 주기 길이 및 모델 정확도로 인해 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="08653-181">This behavior results from the varying cycle lengths and the model accuracy.</span></span>

![][img-simulation-warning]

<span data-ttu-id="08653-182">전체 시뮬레이션이 148 주기를 완료하려면 약 35분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="08653-182">The full simulation takes around 35 minutes to complete 148 cycles.</span></span> <span data-ttu-id="08653-183">160 RUL 임계값은 처음 약 5분이 지나서 도달하고 두 엔진은 약 8분이 지나서 임계값에 도달합니다.</span><span class="sxs-lookup"><span data-stu-id="08653-183">The 160 RUL threshold is met for the first time at around 5 minutes and both engines hit the threshold at around 8 minutes.</span></span>

<span data-ttu-id="08653-184">시뮬레이션은 148주기 동안 전체 데이터 집합을 실행하고 최종 RUL 및 주기 값에 도달합니다.</span><span class="sxs-lookup"><span data-stu-id="08653-184">The simulation runs through the complete dataset for 148 cycles and settles on final RUL and cycle values.</span></span>

<span data-ttu-id="08653-185">언제든 시뮬레이션을 중지할 수 있지만 **시뮬레이션 시작** 을 클릭하면 데이터 집합의 처음부터 시뮬레이션을 재생합니다.</span><span class="sxs-lookup"><span data-stu-id="08653-185">You can stop the simulation at any point, but clicking **Start Simulation** replays the simulation from the start of the dataset.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08653-186">다음 단계</span><span class="sxs-lookup"><span data-stu-id="08653-186">Next steps</span></span>

<span data-ttu-id="08653-187">Azure IoT가 예측 정비 시나리오를 가능하게 하는 방식에 대해 자세히 알아보려면, [사물 인터넷에서 값 캡처][lnk_capture_value]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="08653-187">To learn more about how Azure IoT enables predictive maintenance scenarios, read [Capture value from the Internet of Things][lnk_capture_value].</span></span>

<span data-ttu-id="08653-188">예측 유지 관리 솔루션을 [연습][lnk-predictive-walkthrough]합니다.</span><span class="sxs-lookup"><span data-stu-id="08653-188">Take a [walkthrough][lnk-predictive-walkthrough] of the predictive maintenance solution.</span></span>

<span data-ttu-id="08653-189">미리 구성된 IoT Suite 솔루션의 몇 가지 다른 기능 및 기능을 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08653-189">You can also explore some of the other features and capabilities of the IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="08653-190">[IoT Suite에 대한 질문과 대답][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="08653-190">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="08653-191">[처음부터 IoT 보안을 고려][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="08653-191">[IoT security from the ground up][lnk-security-groundup]</span></span>

[img-resource-group]: media/iot-suite-predictive-overview/resource-group.png
[img-simulation-stopped]: media/iot-suite-predictive-overview/simulation-stopped.png
[img-simulation-running]: media/iot-suite-predictive-overview/simulation-running.png
[img-simulation-warning]: media/iot-suite-predictive-overview/simulation-warning.png
[img-machine-learning]: media/iot-suite-predictive-overview/machine-learning.png

[lnk-powerbi]: https://www.github.com/Microsoft/PowerBI-visuals
[lnk-predictive-walkthrough]: iot-suite-predictive-walkthrough.md
[lnk_preconfigured_solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk_iot_suite]: iot-suite-overview.md
[lnk_infographic]: https://www.microsoft.com/server-cloud/predictivemaintenance/Index.html
[lnk_regression_model]: http://gallery.cortanaanalytics.com/Collection/Predictive-Maintenance-Template-3

[lnk_capture_value]: http://download.microsoft.com/download/0/7/D/07D394CE-185D-4B96-AC3C-9B61179F7080/Capture_value_from_the_Internet%20of%20Things_with_Predictive_Maintenance.PDF
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-permissions]: iot-suite-permissions.md
[lnk-portal]: http://portal.azure.com/
[lnk-machine-learning]: https://azure.microsoft.com/services/machine-learning/