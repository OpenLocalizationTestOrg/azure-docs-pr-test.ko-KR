---
title: "솔루션을 미리 구성 된 유지 관리 aaaPredictive | Microsoft Docs"
description: "Hello Azure IoT Suite 예측 유지 관리에 대 한 설명을 미리 솔루션을 구성 합니다."
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
ms.openlocfilehash: 2d09801467d33db6b7d6333fa071aea2bf573f20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="predictive-maintenance-preconfigured-solution-overview"></a><span data-ttu-id="480a9-103">예측 정비 사전 구성 솔루션 개요</span><span class="sxs-lookup"><span data-stu-id="480a9-103">Predictive maintenance preconfigured solution overview</span></span>

<span data-ttu-id="480a9-104">hello *예측 유지 관리* [솔루션 미리 구성 된] [ lnk_preconfigured_solutions] hello 중 하나인 [Microsoft Azure IoT Suite] [ lnk_iot_suite] 솔루션 미리 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-104">hello *predictive maintenance* [preconfigured solution][lnk_preconfigured_solutions] is one of hello [Microsoft Azure IoT Suite][lnk_iot_suite] preconfigured solutions.</span></span> <span data-ttu-id="480a9-105">이 솔루션은 실시간 장치 원격 분석 컬렉션과 [Azure Machine Learning][lnk-machine-learning]을 사용하여 생성되는 예측 모델을 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-105">This solution integrates real-time device telemetry collection with a predictive model created using [Azure Machine Learning][lnk-machine-learning].</span></span>

<span data-ttu-id="480a9-106">Azure IoT Suite 신속 하 게 하 고 쉽게 tooand 모니터 자산 연결 하 고 사용할 수 실시간 대시보드 및 시각화에 대 한 원격 분석 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-106">With Azure IoT Suite, you can quickly and easily connect tooand monitor assets, and analyze telemetry in real time in dashboards and visualizations.</span></span> <span data-ttu-id="480a9-107">Hello 예측 유지 관리 솔루션에 hello 대시보드 및 시각화를 알려 효율성 드라이브 하 고 스트림을 수익을 향상 시킬 수 있는 새 인텔리전스 합니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-107">In hello predictive maintenance solution, hello dashboards and visualizations provide you with new intelligence that can drive efficiencies and enhance revenue streams.</span></span>

## <a name="hello-scenario"></a><span data-ttu-id="480a9-108">hello 시나리오</span><span class="sxs-lookup"><span data-stu-id="480a9-108">hello Scenario</span></span>

<span data-ttu-id="480a9-109">Fabrikam은 경쟁력 있는 가격으로 우수한 고객 경험을 제공하는 데 중점을 두고 있는 지역 항공사입니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-109">Fabrikam is a regional airline that focuses on great customer experience at competitive prices.</span></span> <span data-ttu-id="480a9-110">항공기 지연의 이유 중 하나는 정비 문제이며 항공 엔진 정비는 특히 어려운 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-110">One cause of flight delays is maintenance issues and aircraft engine maintenance is particularly challenging.</span></span> <span data-ttu-id="480a9-111">Fabrikam 안 엔진 실패 비행 중 해서든, 하므로 해당 엔진을 정기적으로 검사 하 고 tooa 계획에 따라 유지 관리 예약 됩니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-111">Fabrikam must avoid engine failure during flight at all costs, so it inspects its engines regularly and schedules maintenance according tooa plan.</span></span> <span data-ttu-id="480a9-112">그러나 엔진 착용 항상 하지 비행기 hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-112">However, aircraft engines don’t always wear hello same.</span></span> <span data-ttu-id="480a9-113">엔진에 대해 필요 이상의 정비를 수행하는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-113">Some unnecessary maintenance is performed on engines.</span></span> <span data-ttu-id="480a9-114">무엇보다, 정비가 수행될 때까지 항공기를 이륙할 수 없는 문제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-114">More importantly, issues arise which can ground an aircraft until maintenance is performed.</span></span> <span data-ttu-id="480a9-115">비행기 위치에 있는 오른쪽 기술자를 hello 또는 예비 부품을 사용할 수 없는 면 이러한 문제는 특히 비용이 증가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-115">If an aircraft is at a location where hello right technicians or spare parts are not available, these issues can be especially costly.</span></span>

<span data-ttu-id="480a9-116">Fabrikam의 비행기의 hello 엔진 비행 중 엔진을 모니터링 하는 센서와 계측 됩니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-116">hello engines of Fabrikam’s aircraft are instrumented with sensors that monitor engine conditions during flight.</span></span> <span data-ttu-id="480a9-117">Fabrikam은 hello 비행 중 수집 된 hello 예측 유지 관리 솔루션 toocollect hello 센서 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-117">Fabrikam uses hello predictive maintenance solution toocollect hello sensor data collected during hello flight.</span></span> <span data-ttu-id="480a9-118">엔진 작업의 누적 년 후 오류 데이터, Fabrikam의 데이터 과학자는 방식으로 toopredict hello 남은 연수 (RUL) 비행기 엔진의 모델링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-118">After accumulating years of engine operational and failure data, Fabrikam’s data scientists have modeled a way toopredict hello Remaining Useful Life (RUL) of an aircraft engine.</span></span> <span data-ttu-id="480a9-119">hello 모델 데이터 hello 엔진 센서 중 4 개에서 및 tooeventual 실패 하는 엔진 마모 간의 상관 관계를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-119">hello model uses a correlation between data from four of hello engine sensors and engine wear that leads tooeventual failure.</span></span> <span data-ttu-id="480a9-120">Fabrikam tooperform 정기적 검사 tooensure 안전성을 계속 하는 동안 모든 비행 후 각 엔진에 대 한 hello 모델 toocompute hello RUL를 지금 사용할 수 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-120">While Fabrikam continues tooperform regular inspections tooensure safety, it can now use hello models toocompute hello RUL for each engine after every flight.</span></span> <span data-ttu-id="480a9-121">hello 모델 hello 비행 중 hello 엔진에서 수집 하는 hello 원격 분석을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-121">hello model uses hello telemetry collected from hello engines during hello flight.</span></span> <span data-ttu-id="480a9-122">Fabrikam은 이제 향후 고장 시점을 예측하고 정비 및 수리를 사전에 계획할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-122">Fabrikam can now predict future points of failure and plan for maintenance and repair in advance.</span></span>

> [!NOTE]
> <span data-ttu-id="480a9-123">hello 솔루션 모델 실제 엔진 마모 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-123">hello solution model uses actual engine wear data.</span></span>

<span data-ttu-id="480a9-124">Hello 지점 유지 관리에 필요한 경우를 예측 하 여 Fabrikam 작업 tooreduce 비용을 최적화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-124">By predicting hello point when maintenance is required, Fabrikam can optimize its operations tooreduce costs.</span></span>

<span data-ttu-id="480a9-125">유지 관리 코디네이터는 다음 작업을 수행하도록 스케줄러와 함께 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-125">Maintenance coordinators work with schedulers to:</span></span>

- <span data-ttu-id="480a9-126">특정 위치에서 중지 비행기와 toocoincide 유지 관리를 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-126">Plan maintenance toocoincide with an aircraft stopping at a particular location.</span></span>
- <span data-ttu-id="480a9-127">충분 한 시간 ´ ü ± 서비스 hello 비행기 toobe 일정 중단이 발생 하지 않고 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-127">Ensure sufficient time is available for hello aircraft toobe out of service without causing schedule disruption.</span></span>
- <span data-ttu-id="480a9-128">tooschedule 기술자 tooensure 비행기 대기 시간 없이 효율적으로 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-128">tooschedule technicians tooensure that aircraft are serviced efficiently without wait time.</span></span>

<span data-ttu-id="480a9-129">재고 관리자는 정비 계획을 수신하기 때문에 주문 공정 및 예비 부품 재고를 최적화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-129">Inventory control managers receive maintenance plans, so they can optimize their ordering process and spare parts inventory.</span></span>

<span data-ttu-id="480a9-130">이러한 작업 Fabrikam toominimize 비행기 명확 하 게 시간을 설정 하 고 승객 및 직원 일 동 hello 안전성을 보장 하면서 운영 비용을 절감 합니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-130">These activities enable Fabrikam toominimize aircraft ground time and reduce operating costs while ensuring hello safety of passengers and crew.</span></span>

<span data-ttu-id="480a9-131">toounderstand 어떻게 [Azure IoT Suite] [ lnk_iot_suite] hello 기능 고객 필요한 toorealize hello 가능성을 제공 하는지 검토이 예측 유지 관리의 [인포 그래픽] [lnk_infographic].</span><span class="sxs-lookup"><span data-stu-id="480a9-131">toounderstand how [Azure IoT Suite][lnk_iot_suite] provides hello capabilities customers need toorealize hello potential of predictive maintenance, review this [infographic][lnk_infographic].</span></span>

## <a name="how-hello-predictive-maintenance-solution-is-built"></a><span data-ttu-id="480a9-132">Hello 예측 유지 관리 솔루션 빌드 방법</span><span class="sxs-lookup"><span data-stu-id="480a9-132">How hello predictive maintenance solution is built</span></span>

<span data-ttu-id="480a9-133">hello 솔루션은 사용할 수 있는 기존 Azure 기계 학습 모델 템플릿 tooshow IoT Suite 서비스를 통해 수집 된 장치 원격 분석에서 작업 하는 이러한 기능 합니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-133">hello solution uses an existing Azure Machine Learning model available as a template tooshow these capabilities working from device telemetry collected through IoT Suite services.</span></span> <span data-ttu-id="480a9-134">Microsoft 만들었습니다는 [회귀 모델] [ lnk_regression_model] 공개적으로 사용할 수 있는 데이터를 기반으로 하는 비행기 엔진<sup>\[1\]</sup>, 단계별 및 toouse 모델 hello 하는 방법에 대 한 지침입니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-134">Microsoft has built a [regression model][lnk_regression_model] of an aircraft engine based on publically available data<sup>\[1\]</sup>, and step-by-step guidance on how toouse hello model.</span></span>

<span data-ttu-id="480a9-135">이 템플릿에서 만든 hello 회귀 모델을 사용 하는 hello Azure IoT 예측 유지 관리 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-135">hello Azure IoT predictive maintenance solution uses hello regression model created from this template.</span></span> <span data-ttu-id="480a9-136">hello 모델을 Azure 구독에 배포 하 고 자동으로 생성 된 API를 통해 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-136">hello model is deployed into your Azure subscription and exposed through an automatically generated API.</span></span> <span data-ttu-id="480a9-137">hello 테스트 (총 100)의 4를 나타내는 데이터의 하위 집합을 포함 하는 hello 솔루션 엔진 및 총 21) (의 4 hello 센서 데이터 스트림을 합니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-137">hello solution includes a subset of hello testing data representing 4 (of 100 total) engines and hello 4 (of 21 total) sensor data streams.</span></span> <span data-ttu-id="480a9-138">이 데이터는 충분히 tooprovide hello 학습 된 모델에서 올바른 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-138">This data is sufficient tooprovide an accurate result from hello trained model.</span></span>

<span data-ttu-id="480a9-139">*\[1\] A. Saxena and K. Goebel(2008). "Turbofan 엔진 성능 저하 시뮬레이션 데이터 집합", NASA Ames Prognostics Data Repository(http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*</span><span class="sxs-lookup"><span data-stu-id="480a9-139">*\[1\] A. Saxena and K. Goebel (2008). "Turbofan Engine Degradation Simulation Data Set", NASA Ames Prognostics Data Repository (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*</span></span>

## <a name="get-started-with-predictive-maintenance"></a><span data-ttu-id="480a9-140">예측 유지 관리 시작</span><span class="sxs-lookup"><span data-stu-id="480a9-140">Get started with predictive maintenance</span></span>

<span data-ttu-id="480a9-141">이 자습서 tooprovision 예측 유지 관리 솔루션을 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-141">This tutorial shows you how tooprovision hello predictive maintenance solution.</span></span> <span data-ttu-id="480a9-142">또한 안내 합니다 hello hello 예측 유지 관리 솔루션의 기본 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-142">It also walks you through hello basic features of hello predictive maintenance solution.</span></span> <span data-ttu-id="480a9-143">이러한 기능 중 대부분 hello 미리 구성 된 솔루션과 함께 배포 하는 hello 솔루션 대시보드를 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-143">You can access many of these features through hello solution dashboard that deploys along with hello preconfigured solution.</span></span>

<span data-ttu-id="480a9-144">toocomplete이이 자습서에서는 활성 Azure 구독이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-144">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="480a9-145">계정이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-145">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="480a9-146">자세한 내용은 [Azure 무료 평가판][lnk_free_trial]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="480a9-146">For details, see [Azure Free Trial][lnk_free_trial].</span></span>

1. <span data-ttu-id="480a9-147">너무 로그온[azureiotsuite.com] [ lnk-azureiotsuite] Azure를 사용 하 여 계정 자격 증명을 누르고  **+**  toocreate 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-147">Log on too[azureiotsuite.com][lnk-azureiotsuite] using your Azure account credentials, and click **+** toocreate a solution.</span></span>
1. <span data-ttu-id="480a9-148">클릭 **선택** hello **예측 유지 관리** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-148">Click **Select** hello **Predictive maintenance** tile.</span></span>
1. <span data-ttu-id="480a9-149">예측 정비 사전 구성 솔루션에 **솔루션 이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-149">Enter a **Solution name** for your predictive maintenance preconfigured solution.</span></span>
1. <span data-ttu-id="480a9-150">선택 hello **지역** 및 **구독** toouse tooprovision hello 솔루션을 원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-150">Select hello **Region** and **Subscription** you want toouse tooprovision hello solution.</span></span>
1. <span data-ttu-id="480a9-151">클릭 **솔루션 만들기** toobegin hello를 프로 비전 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-151">Click **Create Solution** toobegin hello provisioning process.</span></span> <span data-ttu-id="480a9-152">이 프로세스는 일반적으로 몇 분 toorun을 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-152">This process typically takes several minutes toorun.</span></span>

### <a name="wait-for-hello-provisioning-process-toocomplete"></a><span data-ttu-id="480a9-153">프로비저닝 프로세스 toocomplete hello에 대 한 대기</span><span class="sxs-lookup"><span data-stu-id="480a9-153">Wait for hello provisioning process toocomplete</span></span>

1. <span data-ttu-id="480a9-154">솔루션에 hello 타일을 클릭 **프로 비전** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-154">Click hello tile for your solution with **Provisioning** status.</span></span>
1. <span data-ttu-id="480a9-155">공지 hello **상태를 프로 비전** Azure 구독에서 Azure 서비스 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-155">Notice hello **Provisioning states** as Azure services are deployed in your Azure subscription.</span></span>
1. <span data-ttu-id="480a9-156">프로 비전이 완료 되 면 hello 상태가 변경 될 너무**준비**합니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-156">Once provisioning completes, hello status changes too**Ready**.</span></span>
1. <span data-ttu-id="480a9-157">Hello 오른쪽 창에 솔루션의 hello 타일 toosee hello 자세히를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-157">Click hello tile toosee hello details of your solution in hello right-hand pane.</span></span> <span data-ttu-id="480a9-158">이 창의 hello 솔루션 대시보드 및 액세스 hello 기계 학습 작업 영역을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-158">From this pane, you can launch hello solution dashboard and access hello Machine Learning workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="480a9-159">Hello 미리 구성 된 솔루션을 배포 하는 문제가 발생 하는 경우 검토 [hello azureiotsuite.com 사이트에 대 한 권한을] [ lnk-permissions] 및 hello [FAQ] [ lnk-faq].</span><span class="sxs-lookup"><span data-stu-id="480a9-159">If you encounter issues deploying hello preconfigured solution, review [Permissions on hello azureiotsuite.com site][lnk-permissions] and hello [FAQ][lnk-faq].</span></span> <span data-ttu-id="480a9-160">Hello 문제가 지속 되 면 hello에 서비스 티켓을 만들 [포털][lnk-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-160">If hello issues persist, create a service ticket on hello [portal][lnk-portal].</span></span>

<span data-ttu-id="480a9-161">솔루션에 대 한 목록에 없는 세부 정보 toosee 예상할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="480a9-161">Are there details you'd expect toosee that aren't listed for your solution?</span></span> <span data-ttu-id="480a9-162">[사용자 의견](https://feedback.azure.com/forums/321918-azure-iot)에 기능 제안을 보내주세요.</span><span class="sxs-lookup"><span data-stu-id="480a9-162">Give us feature suggestions on [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span></span>

## <a name="view-hello-solution"></a><span data-ttu-id="480a9-163">보기 hello 솔루션</span><span class="sxs-lookup"><span data-stu-id="480a9-163">View hello solution</span></span>

<span data-ttu-id="480a9-164">이 섹션에서는 UI hello 솔루션을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-164">This section guides you through hello solution UI.</span></span>

### <a name="predictive-maintenance-dashboard"></a><span data-ttu-id="480a9-165">대시보드에서 예측 유지 관리</span><span class="sxs-lookup"><span data-stu-id="480a9-165">Predictive Maintenance Dashboard</span></span>

<span data-ttu-id="480a9-166">PowerBI JavaScript 컨트롤을 사용 하는 hello 웹 응용 프로그램에서이 페이지 (hello 참조 [powerbi-visuals 리포지토리][lnk-powerbi]) toovisualize:</span><span class="sxs-lookup"><span data-stu-id="480a9-166">This page in hello web application uses PowerBI JavaScript controls (see hello [PowerBI-visuals repository][lnk-powerbi]) toovisualize:</span></span>

* <span data-ttu-id="480a9-167">hello blob 저장소에 hello 스트림 분석 작업의 데이터를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-167">hello output data from hello Stream Analytics jobs in blob storage.</span></span>
* <span data-ttu-id="480a9-168">비행기 엔진 당 hello RUL 및 주기 수입니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-168">hello RUL and cycle count per aircraft engine.</span></span>

### <a name="observing-hello-behavior-of-hello-cloud-solution"></a><span data-ttu-id="480a9-169">Hello 클라우드 솔루션의 hello 동작을 관찰합니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-169">Observing hello behavior of hello cloud solution</span></span>

<span data-ttu-id="480a9-170">Hello Azure 포털에서 toohello 리소스 그룹 이동 hello 솔루션 이름이 선택한 tooview 프로 비전 된 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-170">In hello Azure portal, navigate toohello resource group with hello solution name you chose tooview your provisioned resources.</span></span>

![][img-resource-group]

<span data-ttu-id="480a9-171">Hello 미리 구성 된 솔루션의 프로 비전 할 때 전자 메일 링크 toohello 기계 학습 작업 영역에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-171">When you provision hello preconfigured solution, you receive an email with a link toohello Machine Learning workspace.</span></span> <span data-ttu-id="480a9-172">Hello에서 toohello 기계 학습 작업 영역을 탐색할 수 있습니다 [azureiotsuite.com] [ lnk-azureiotsuite] 프로 비전 된 솔루션에 대 한 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-172">You can also navigate toohello Machine Learning workspace from hello [azureiotsuite.com][lnk-azureiotsuite] page for your provisioned solution.</span></span> <span data-ttu-id="480a9-173">타일은 hello 솔루션은 hello 하는 경우이 페이지에서 사용할 수 **준비** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-173">A tile is available on this page when hello solution is in hello **Ready** state.</span></span>

![][img-machine-learning]

<span data-ttu-id="480a9-174">Hello 솔루션 포털에서 해당 hello 샘플이 프로 비전 되어 4 개의 시뮬레이션 된 장치 toorepresent 두 비행기 각각 4 개의 센서 비행기 당 두 개의 엔진으로 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-174">In hello solution portal, you can see that hello sample is provisioned with four simulated devices toorepresent two aircraft with two engines per aircraft, each with four sensors.</span></span> <span data-ttu-id="480a9-175">Toohello 솔루션 포털을 처음 표시할 때 hello 시뮬레이션 중지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-175">When you first navigate toohello solution portal, hello simulation is stopped.</span></span>

![][img-simulation-stopped]

<span data-ttu-id="480a9-176">클릭 **시뮬레이션 시작** toobegin hello 시뮬레이션 합니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-176">Click **Start simulation** toobegin hello simulation.</span></span> <span data-ttu-id="480a9-177">센서 기록, RUL, 주기 및 RUL hello 기록 hello 대시보드를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-177">hello sensor history, RUL, Cycles, and RUL history populate hello dashboard.</span></span>

![][img-simulation-running]

<span data-ttu-id="480a9-178">RUL 160 (예시 목적을 위해 선택 대 한 임의의 임계값) 보다 작은 경우 RUL 표시할 경고 기호 다음 toohello를 hello 솔루션 포털에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-178">When RUL is less than 160 (an arbitrary threshold chosen for demonstration purposes), hello solution portal displays a warning symbol next toohello RUL display.</span></span> <span data-ttu-id="480a9-179">hello 솔루션 포털에는 hello 비행기 엔진 노란색으로 강조 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-179">hello solution portal also highlights hello aircraft engine in yellow.</span></span> <span data-ttu-id="480a9-180">Hello RUL 값 전반적으로 일반 하향 추세를 포함 하는 방법 사항을 참고 하십시오. 하지만 다음과 같은 toobounce 및 축소 합니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-180">Notice how hello RUL values have a general downward trend overall, but tend toobounce up and down.</span></span> <span data-ttu-id="480a9-181">이 동작은 hello 다양 한 주기 길이 및 hello 모델 정확도에서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-181">This behavior results from hello varying cycle lengths and hello model accuracy.</span></span>

![][img-simulation-warning]

<span data-ttu-id="480a9-182">hello 전체 시뮬레이션 약 35 분 toocomplete 148 주기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-182">hello full simulation takes around 35 minutes toocomplete 148 cycles.</span></span> <span data-ttu-id="480a9-183">약 5 분에서 처음으로 hello에 대 한 hello 160 RUL 임계값을 충족 하 고 두 엔진에서 약 8 분 hello 임계값에 도달 합니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-183">hello 160 RUL threshold is met for hello first time at around 5 minutes and both engines hit hello threshold at around 8 minutes.</span></span>

<span data-ttu-id="480a9-184">hello 시뮬레이션 148 사이클 hello 전체 데이터 집합을 실행 하 고 최종 RUL 및 주기 값에 settles.</span><span class="sxs-lookup"><span data-stu-id="480a9-184">hello simulation runs through hello complete dataset for 148 cycles and settles on final RUL and cycle values.</span></span>

<span data-ttu-id="480a9-185">언제 든 hello 시뮬레이션을 중지할 수 있습니다 지점 하지만 클릭 하면 **시작 시뮬레이션** 재생 hello hello 데이터 집합의 hello 시작에서 시뮬레이션 합니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-185">You can stop hello simulation at any point, but clicking **Start Simulation** replays hello simulation from hello start of hello dataset.</span></span>

## <a name="next-steps"></a><span data-ttu-id="480a9-186">다음 단계</span><span class="sxs-lookup"><span data-stu-id="480a9-186">Next steps</span></span>

<span data-ttu-id="480a9-187">Azure IoT 예측 유지 관리 시나리오, 읽기를 사용 하는 방법에 대 한 자세한 toolearn [hello 사물 인터넷에서에서 값을 캡처할][lnk_capture_value]합니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-187">toolearn more about how Azure IoT enables predictive maintenance scenarios, read [Capture value from hello Internet of Things][lnk_capture_value].</span></span>

<span data-ttu-id="480a9-188">수행 된 [연습] [ lnk-predictive-walkthrough] hello 예측 유지 관리 솔루션의 합니다.</span><span class="sxs-lookup"><span data-stu-id="480a9-188">Take a [walkthrough][lnk-predictive-walkthrough] of hello predictive maintenance solution.</span></span>

<span data-ttu-id="480a9-189">탐색할 수도 있습니다 hello 중 일부 다른 기능 및 hello IoT Suite 미리 구성 된 솔루션의 기능:</span><span class="sxs-lookup"><span data-stu-id="480a9-189">You can also explore some of hello other features and capabilities of hello IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="480a9-190">[IoT Suite에 대한 질문과 대답][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="480a9-190">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="480a9-191">[Hello 접지에서 IoT 보안][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="480a9-191">[IoT security from hello ground up][lnk-security-groundup]</span></span>

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