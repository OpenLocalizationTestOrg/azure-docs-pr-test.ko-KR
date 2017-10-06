---
title: "aaaAzure IoT Suite 연결 팩터리 개요 | Microsoft Docs"
description: "Hello Azure IoT Suite에 대 한 설명을 팩터리 미리 구성 된 솔루션을 연결 합니다."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: dobett
ms.openlocfilehash: 929b5ed41ef7d82c9b4480d02aa3f0db38931919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-connected-factory-preconfigured-solution"></a><span data-ttu-id="0dcd7-103">연결 된 hello 미리 구성 하는 팩터리 솔루션 시작</span><span class="sxs-lookup"><span data-stu-id="0dcd7-103">Get started with hello connected factory preconfigured solution</span></span>

<span data-ttu-id="0dcd7-104">Azure IoT Suite [솔루션 미리 구성 된] [ lnk-preconfigured-solutions] 일반적인 IoT 비즈니스 시나리오를 구현 하는 여러 Azure IoT 서비스 toodeliver 종단 간 솔루션을 결합 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-104">Azure IoT Suite [preconfigured solutions][lnk-preconfigured-solutions] combine multiple Azure IoT services toodeliver end-to-end solutions that implement common IoT business scenarios.</span></span> <span data-ttu-id="0dcd7-105">hello *연결 된 팩터리* 미리 구성 된 솔루션 tooand 모니터 산업 장치를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-105">hello *connected factory* preconfigured solution connects tooand monitors your industrial devices.</span></span> <span data-ttu-id="0dcd7-106">장치 및 toodrive operational 생산성 및 수익에서 데이터의 hello 솔루션 tooanalyze hello 스트림을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-106">You can use hello solution tooanalyze hello stream of data from your devices and toodrive operational productivity and profitability.</span></span>

<span data-ttu-id="0dcd7-107">이 자습서에서는 tooprovision hello 팩터리를 연결 하는 방법을 솔루션 미리 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-107">This tutorial shows you how tooprovision hello connected factory preconfigured solution.</span></span> <span data-ttu-id="0dcd7-108">또한 안내 합니다 hello hello 미리 구성 된 솔루션의 기본 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-108">It also walks you through hello basic features of hello preconfigured solution.</span></span> <span data-ttu-id="0dcd7-109">이러한 기능 중 대부분 hello 솔루션에서 액세스할 수 있습니다 *대시보드* hello 미리 구성 된 솔루션의 일부로 배포 하는:</span><span class="sxs-lookup"><span data-stu-id="0dcd7-109">You can access many of these features from hello solution *dashboard* that deploys as part of hello preconfigured solution:</span></span>

![연결된 공장 미리 구성된 솔루션 대시보드][img-cf-home]

<span data-ttu-id="0dcd7-111">toocomplete이이 자습서에서는 활성 Azure 구독이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-111">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="0dcd7-112">계정이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="0dcd7-113">자세한 내용은 [Azure 무료 평가판][lnk_free_trial]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
> 
> 

## <a name="provision-hello-solution"></a><span data-ttu-id="0dcd7-114">프로 비전 hello 솔루션</span><span class="sxs-lookup"><span data-stu-id="0dcd7-114">Provision hello solution</span></span>

1. <span data-ttu-id="0dcd7-115">Azure 계정 자격 증명을 사용 하 여 tooazureiotsuite.com에 로그인 하 고 클릭 "**+**" toocreate 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-115">Log on tooazureiotsuite.com using your Azure account credentials, and click "**+**" toocreate a solution.</span></span>
2. <span data-ttu-id="0dcd7-116">클릭 **선택** hello에 **연결 된 팩터리** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-116">Click **Select** on hello **Connected factory** tile.</span></span>
3. <span data-ttu-id="0dcd7-117">미리 구성된 연결된 팩터리 솔루션에 대한 **솔루션 이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-117">Enter a **Solution name** for your connected factory preconfigured solution.</span></span>
4. <span data-ttu-id="0dcd7-118">선택 hello **구독** 및 **지역** toouse tooprovision hello 솔루션을 원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-118">Select hello **Subscription** and **Region** you want toouse tooprovision hello solution.</span></span>
5. <span data-ttu-id="0dcd7-119">클릭 **솔루션 만들기** toobegin hello를 프로 비전 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-119">Click **Create Solution** toobegin hello provisioning process.</span></span> <span data-ttu-id="0dcd7-120">이 프로세스는 일반적으로 몇 분 toorun을 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-120">This process typically takes several minutes toorun.</span></span>

### <a name="while-you-wait-for-hello-provisioning-process-toocomplete"></a><span data-ttu-id="0dcd7-121">프로비저닝 프로세스 toocomplete hello를 기다리는 동안</span><span class="sxs-lookup"><span data-stu-id="0dcd7-121">While you wait for hello provisioning process toocomplete</span></span>

1. <span data-ttu-id="0dcd7-122">솔루션에 hello 타일을 클릭 **프로 비전** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-122">Click hello tile for your solution with **Provisioning** status.</span></span>
2. <span data-ttu-id="0dcd7-123">공지 hello **상태를 프로 비전** Azure 구독에서 Azure 서비스 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-123">Notice hello **Provisioning states** as Azure services are deployed in your Azure subscription.</span></span>
3. <span data-ttu-id="0dcd7-124">프로 비전이 완료 되 면 hello 상태가 변경 될 너무**준비**합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-124">Once provisioning completes, hello status changes too**Ready**.</span></span>
4. <span data-ttu-id="0dcd7-125">Hello 오른쪽 창에 솔루션의 hello 타일 toosee hello 자세히를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-125">Click hello tile toosee hello details of your solution in hello right-hand pane.</span></span>

> [!NOTE]
> <span data-ttu-id="0dcd7-126">Hello 미리 구성 된 솔루션을 배포 하는 문제가 발생 하는 경우 검토 [hello azureiotsuite.com 사이트에 대 한 권한을] [ lnk-permissions] 및 hello [팩터리 FAQ 연결](iot-suite-faq-cf.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-126">If you encounter issues deploying hello preconfigured solution, review [Permissions on hello azureiotsuite.com site][lnk-permissions] and hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span> <span data-ttu-id="0dcd7-127">Hello 문제가 지속 되 면 hello에 서비스 티켓을 만들 [포털][lnk-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-127">If hello issues persist, create a service ticket on hello [portal][lnk-portal].</span></span>

<span data-ttu-id="0dcd7-128">솔루션에 대 한 목록에 없는 세부 정보 toosee 예상할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="0dcd7-128">Are there details you'd expect toosee that aren't listed for your solution?</span></span> <span data-ttu-id="0dcd7-129">[사용자 의견](https://feedback.azure.com/forums/321918-azure-iot)에 기능 제안을 보내주세요.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-129">Give us feature suggestions on [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="0dcd7-130">시나리오 개요</span><span class="sxs-lookup"><span data-stu-id="0dcd7-130">Scenario overview</span></span>

<span data-ttu-id="0dcd7-131">연결 하는 hello를 배포할 때 팩터리 솔루션 미리 구성 된, toostep 일반적인 산업 시나리오를 통해 사용할 수 있는 리소스와 미리 채워져 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-131">When you deploy hello connected factory preconfigured solution, it is prepopulated with resources that enable you toostep through a common industrial scenario.</span></span> <span data-ttu-id="0dcd7-132">이 시나리오에서는 여러 팩터리 연결 hello 데이터 값을 필요한 toocompute toohello 솔루션 보고서 전반적인 장비 효율성 (OEE) 및 핵심 성과 지표 (Kpi).</span><span class="sxs-lookup"><span data-stu-id="0dcd7-132">In this scenario, several factories connected toohello solution report hello data values required toocompute overall equipment efficiency (OEE) and key performance indicators (KPIs).</span></span> <span data-ttu-id="0dcd7-133">hello 다음 섹션에서는 방법을 보여 줍니다에:</span><span class="sxs-lookup"><span data-stu-id="0dcd7-133">hello following sections show you how to:</span></span>

* <span data-ttu-id="0dcd7-134">팩터리, 생산 라인, 스테이션 OEE 및 KPI 값 모니터링</span><span class="sxs-lookup"><span data-stu-id="0dcd7-134">Monitor factory, production lines, station OEE, and KPI values</span></span>
* <span data-ttu-id="0dcd7-135">Azure 시간 시계열 Insights를 사용 하 여 이러한 장치에서 생성 된 hello 원격 분석 데이터를 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-135">Analyze hello telemetry data generated from these devices using Azure Time Series Insights</span></span>
* <span data-ttu-id="0dcd7-136">작업을 수행할 경고 toofix 문제</span><span class="sxs-lookup"><span data-stu-id="0dcd7-136">Act on alerts toofix issues</span></span>

<span data-ttu-id="0dcd7-137">이 시나리오의 주요 기능은 수행할 수 있다는 이러한 모든 동작 원격으로 hello 솔루션 대시보드에서입니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-137">A key feature of this scenario is that you can perform all these actions remotely from hello solution dashboard.</span></span> <span data-ttu-id="0dcd7-138">물리적 액세스 toohello 장치 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-138">You do not need physical access toohello devices.</span></span>

## <a name="view-hello-solution-dashboard"></a><span data-ttu-id="0dcd7-139">Hello 솔루션 대시보드 보기</span><span class="sxs-lookup"><span data-stu-id="0dcd7-139">View hello solution dashboard</span></span>

<span data-ttu-id="0dcd7-140">hello 솔루션 대시보드 toomanage 배포 된 hello 솔루션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-140">hello solution dashboard enables you toomanage hello deployed solution.</span></span> <span data-ttu-id="0dcd7-141">전역 팩터리 구성의 계층적 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-141">It is a hierarchical representation of a global factory configuration.</span></span> <span data-ttu-id="0dcd7-142">예를 들어 OEE 및 KPI를 보고, 원격 분석 및 작업 경고에 대한 새 노드를 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-142">For example, you can view OEE and KPIs, publish new nodes for telemetry and action alerts.</span></span>

1. <span data-ttu-id="0dcd7-143">Hello 프로 비전이 완료 된 시점과 미리 구성 된 솔루션에 대 한 hello 타일 나타냅니다 **준비**, 선택 **시작** tooopen 새 탭에서 연결 된 팩터리 솔루션 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-143">When hello provisioning is complete and hello tile for your preconfigured solution indicates **Ready**, choose **Launch** tooopen your connected factory solution portal in a new tab.</span></span>

    ![미리 구성 하는 hello 솔루션 시작][img-launch-solution]

1. <span data-ttu-id="0dcd7-145">기본적으로 hello 솔루션 포털 표시 hello *대시보드*합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-145">By default, hello solution portal shows hello *dashboard*.</span></span> <span data-ttu-id="0dcd7-146">hello 포털의 toonavigate tooother 영역 hello hello 페이지의 왼쪽에 hello 메뉴를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-146">toonavigate tooother areas of hello portal, use hello menu on hello left-hand side of hello page.</span></span>

    ![연결된 공장 미리 구성된 솔루션 대시보드][cf-img-menu]

<span data-ttu-id="0dcd7-148">hello 대시보드 hello를 다음 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-148">hello dashboard displays hello following information:</span></span>

* <span data-ttu-id="0dcd7-149">A **팩터리 목록** hello 솔루션의 hello 상태, 위치 및 현재 프로덕션 구성을 보여 주는 패널입니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-149">A **Factory list** panel that shows hello status, location, and current production configuration in hello solution.</span></span> <span data-ttu-id="0dcd7-150">Hello 솔루션을 처음 실행할 때의 시뮬레이션 된 장치는 여러 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-150">When you first run hello solution, there are a number of simulated devices.</span></span> <span data-ttu-id="0dcd7-151">hello 생산 라인 시뮬레이션 3 명의 실제 OPC UA 생산 라인 당 시뮬레이션 된 작업을 수행 하 고는 서버 데이터를 공유로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-151">hello production line simulation is composed of three real OPC UA servers per production line that perform simulated tasks and share data.</span></span> <span data-ttu-id="0dcd7-152">OPC UA에 대 한 자세한 내용은 참조 hello [팩터리 FAQ 연결](iot-suite-faq-cf.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-152">For more information about OPC UA, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>
* <span data-ttu-id="0dcd7-153">A **지도** 각 장치의 표시 hello 위치 toohello 솔루션 연결 있는지 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-153">A **map** that displays hello location of each device connected toohello solution.</span></span> <span data-ttu-id="0dcd7-154">hello 솔루션 hello 맵에 hello Bing Maps API tooplot 정보를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-154">hello solution can use hello Bing Maps API tooplot information on hello map.</span></span> <span data-ttu-id="0dcd7-155">구독이 Bing Maps Enterprise API에 대해 설정된 경우 이 기능이 자동으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-155">If your subscription is enabled for Bing Maps Enterprise API, then this feature is used automatically.</span></span> <span data-ttu-id="0dcd7-156">그렇지 않은 경우 참조 hello [FAQ] [ lnk-faq] toolearn 어떻게 toomake hello 맵 동적입니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-156">If not, see hello [FAQ][lnk-faq] toolearn how toomake hello map dynamic.</span></span>
* <span data-ttu-id="0dcd7-157">원격 분석 또는 OEE/KPI 값이 특정 임계값을 초과할 때 생성되는 경고를 표시하는 **경고** 패널.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-157">An **Alerts** panel that displays alerts generated when a telemetry or OEE/KPI value exceeds a specific threshold.</span></span>
* <span data-ttu-id="0dcd7-158">**전반적인 장비 효율성** hello 전체 기업 또는 hello 공장/프로덕션에 대 한 hello OEE 값 선/있습니다 스테이션 표시 보고 패널입니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-158">An **Overall Equipment Efficiency** panel that shows hello OEE values for hello whole enterprise, or hello factory/production line/station you are viewing.</span></span> <span data-ttu-id="0dcd7-159">이 값은 hello 스테이션 보기 toohello 엔터프라이즈 수준에서 집계 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-159">This value is aggregated from hello station view toohello enterprise level.</span></span> <span data-ttu-id="0dcd7-160">hello OEE 그림 및 구성 요소의 추가로 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-160">hello OEE figure and its constituent elements can be further analyzed.</span></span>
* <span data-ttu-id="0dcd7-161">**핵심 성과 지표** 생성 된 단위 및 에너지 hello 전체 기업 또는 hello 공장/생산 라인에서 사용 하는 hello 수를 표시 하면 스테이션이 / 패널 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-161">**Key Performance Indicators** panel that displays hello number of units produced and energy used by hello whole enterprise or hello factory/production line/station you are viewing.</span></span> <span data-ttu-id="0dcd7-162">이러한 값은 스테이션 보기 toohello 엔터프라이즈 수준에서 집계 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-162">These values are aggregated from a station view toohello enterprise level.</span></span>

## <a name="view-factories"></a><span data-ttu-id="0dcd7-163">공장 보기</span><span class="sxs-lookup"><span data-stu-id="0dcd7-163">View factories</span></span>

<span data-ttu-id="0dcd7-164">hello *팩터리* 패널 hello 솔루션, 상태 및 현재 프로덕션 구성에서 모든 hello 팩터리의 지리적 위치 hello 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-164">hello *Factories* panel shows you hello geographical location of all hello factories in hello solution, their status, and current production configuration.</span></span> <span data-ttu-id="0dcd7-165">Hello 위치 목록에서 toohello hello 솔루션 계층 구조의 다른 수준을 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-165">From hello locations list, you can navigate toohello other levels in hello solution hierarchy.</span></span> <span data-ttu-id="0dcd7-166">hello 행 hello 목록에서 해당 위치의 hello에서는 생산 라인의 세부 정보를 연결 하는 하이퍼링크가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-166">hello rows in hello list are hyperlinks that link details of hello production lines at that location.</span></span> <span data-ttu-id="0dcd7-167">그런 다음 가능한 toodrill hello 생산 라인 세부 정보를 및 toohello 스테이션에 대 한 개요 정보 중단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-167">It is then possible toodrill into hello production line details and down toohello station level view.</span></span> <span data-ttu-id="0dcd7-168">필터 toohello 목록도 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-168">You can also apply a filter toohello list.</span></span>

![연결된 공장 미리 구성된 공장][cf-img-factories] 

1. <span data-ttu-id="0dcd7-170">hello **팩터리 패널** 표시 hello이 솔루션에 대 한 팩터리 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-170">hello **Factory panel** shows hello factory list for this solution.</span></span>

2. <span data-ttu-id="0dcd7-171">hello 팩터리 목록에는 처음 6 팩터리 hello를 프로 비전 프로세스에서 만든 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-171">hello factory list initially shows six factories created by hello provisioning process.</span></span> <span data-ttu-id="0dcd7-172">추가 시뮬레이션 및 물리적 장치 toohello 솔루션을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-172">You can add additional simulated and physical devices toohello solution.</span></span>

3. <span data-ttu-id="0dcd7-173">tooview hello 세부 정보는 팩터리의 hello 팩터리 목록의 hello 행을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-173">tooview hello details of a factory, click hello row in hello factory list.</span></span>

4. <span data-ttu-id="0dcd7-174">생산 라인의 tooview hello 세부 정보는 hello 목록의 hello 행을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-174">tooview hello details of a production line, click hello row in hello list.</span></span>

5. <span data-ttu-id="0dcd7-175">tooview hello 게시 hello 생산 라인에서 스테이션의 OPC UA 노드, hello 목록 hello 행을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-175">tooview hello published OPC UA nodes of a station on hello production line, click hello row in hello list.</span></span>

6. <span data-ttu-id="0dcd7-176">hello 스테이션에 특정 노드에서 tooview 세부 정보는 hello 목록의 hello 행을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-176">tooview details on a specific node in hello station, click hello row in hello list.</span></span> <span data-ttu-id="0dcd7-177">이 작업 시간 시계열 Insights 시각화가 포함 된 hello 컨텍스트 패널을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-177">This action launches hello context panel with Time Series Insights visualizations.</span></span> <span data-ttu-id="0dcd7-178">Hello 시간 계열 Insights 탐색기 환경에서 이러한 그래프 toodo 추가 분석을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-178">Click these graphs toodo further analysis in hello Time Series Insights explorer environment.</span></span>

## <a name="view-map"></a><span data-ttu-id="0dcd7-179">지도 보기</span><span class="sxs-lookup"><span data-stu-id="0dcd7-179">View map</span></span>

<span data-ttu-id="0dcd7-180">구독 액세스 toohello Bing Maps API 있으면 hello *팩터리* 지도 보면 hello 지리적 위치 및 모든 hello 팩터리의 상태 hello 솔루션에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-180">If your subscription has access toohello Bing Maps API, hello *Factories* map shows you hello geographical location and status of all hello factories in hello solution.</span></span> <span data-ttu-id="0dcd7-181">hello 위치 세부 정보로 toodrill hello 지도에 표시 하는 hello 위치를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-181">toodrill into hello location details, click hello locations displayed on hello map.</span></span>

![연결된 공장 미리 구성된 솔루션 지도][cf-img-map]

## <a name="view-alerts"></a><span data-ttu-id="0dcd7-183">경고 보기</span><span class="sxs-lookup"><span data-stu-id="0dcd7-183">View alerts</span></span>

<span data-ttu-id="0dcd7-184">hello **경고** 패널 표시 인해 생성 된 경고 tooa 값 또는 구성 된 임계값을 초과 하는 계산 된 OEE/KPI 값을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-184">hello **Alert** panel shows you alerts generated due tooa reported value or a calculated OEE/KPI value exceeding its configured threshold.</span></span> <span data-ttu-id="0dcd7-185">Hello 스테이션 개요 toohello 전역 보기에서 hello 계층의 각 수준에서이 패널에 경고가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-185">This panel displays alerts at each level of hello hierarchy, from hello station level view toohello global view.</span></span> <span data-ttu-id="0dcd7-186">hello 경고 hello 경고, 날짜, 시간, 위치 및 발생 수에 대 한 설명을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-186">hello alerts contain a description of hello alert, date, time, location, and number of occurrences.</span></span> <span data-ttu-id="0dcd7-187">Hello 시간 시계열 인 사이트 데이터를 사용 하 여 hello 경고를 발생 시킨 toohello 데이터에서 통찰력을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-187">You can gain insights in toohello data that caused hello alert using hello Time Series Insights data.</span></span> <span data-ttu-id="0dcd7-188">hello 시간 계열 Insights에서 데이터를 시각화할 해당 되는 경고를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-188">hello Time Series Insights data is visualized in hello alerts where applicable.</span></span> <span data-ttu-id="0dcd7-189">관리자 인 경우 hello 경고와 같은 기본 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-189">If you are an Administrator, you can take default actions on hello alerts such as:</span></span>

* <span data-ttu-id="0dcd7-190">닫기 hello 경고입니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-190">Close hello alert.</span></span>
* <span data-ttu-id="0dcd7-191">Hello 경고를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-191">Acknowledge hello alert.</span></span>

<span data-ttu-id="0dcd7-192">필요에 따라 좀 더 복잡한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-192">Optionally, you can take more complex actions.</span></span> <span data-ttu-id="0dcd7-193">예를 들어 hello 어셈블리의 압력 OPC UA 노드 hello에 대 한 있습니다 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-193">For example, for hello Pressure OPC UA Node of hello Assembly you could:</span></span>

* <span data-ttu-id="0dcd7-194">새 브라우저 창에서 웹 페이지에 지원 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-194">Show supporting information in a web page in a new browser window.</span></span>
* <span data-ttu-id="0dcd7-195">Hello 장치에서 OPC UA 메서드를 호출 하 여 hello 경고의 원인 hello를 완화 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-195">Mitigate hello cause of hello alert by calling an OPC UA method on hello device.</span></span>
* <span data-ttu-id="0dcd7-196">Hello 기본 작업의 hello 사용 가능성을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-196">Suppress hello availability of hello default actions.</span></span>

    ![연결된 공장 미리 구성된 솔루션 경고][cf-img-alerts]

> [!NOTE]
> <span data-ttu-id="0dcd7-198">이러한 경고는 hello 미리 구성 된 솔루션의 구성 파일에 지정 된 규칙에 의해 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-198">These alerts are generated by rules that are specified in a configuration file in hello preconfigured solution.</span></span> <span data-ttu-id="0dcd7-199">Hello OEE 또는 KPI 수치 또는 OPC UA 노드 값은 해당 구성 된 임계값을 초과 하는 경우 이러한 규칙에서 경고를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-199">These rules can generate alerts when hello OEE or KPI figures or OPC UA Node values are exceeding their configured threshold.</span></span>

1. <span data-ttu-id="0dcd7-200">hello **경고 패널** 이 솔루션에서 생성 된 경고를 hello 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-200">hello **Alerts panel** shows hello alerts generated in this solution.</span></span>

2. <span data-ttu-id="0dcd7-201">tooview hello 세부 정보는 경고의 hello 경고 패널에서 hello 경고를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-201">tooview hello details of an alert, click hello alert in hello alerts panel.</span></span>

3. <span data-ttu-id="0dcd7-202">toofurther는 hello 경고 데이터를 분석, hello 경고 패널 tooopen hello 시간 계열 Insights 탐색기 환경에서 hello 그래프를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-202">toofurther analyze hello alert data, click hello graph in hello alert panel tooopen hello Time Series Insights explorer environment.</span></span>

4. <span data-ttu-id="0dcd7-203">tooaddress hello 경고, hello 경고 패널에서 사용할 수 있는 몇 가지 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-203">tooaddress hello alert, several actions are available in hello alert panel.</span></span> <span data-ttu-id="0dcd7-204">Hello 적절 한 옵션을 선택 하 고 hello 클릭 동작 명령 단추를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-204">Choose hello appropriate option for you and click hello execute action command button.</span></span>

## <a name="view-overall-equipment-efficiency"></a><span data-ttu-id="0dcd7-205">설비 종합 효율 보기</span><span class="sxs-lookup"><span data-stu-id="0dcd7-205">View overall equipment efficiency</span></span>

<span data-ttu-id="0dcd7-206">OEE 세요 hello를 주요 제작과 관련 된 작업 매개 변수를 사용 하 여 hello 제조 프로세스의 효율성입니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-206">OEE rates hello efficiency of hello manufacturing process using a key production-related operational parameters.</span></span> <span data-ttu-id="0dcd7-207">OEE는 산업 표준 측정값 hello 가용성, 성능 급여 및 품질 비율을 곱하여 계산: OEE 가용성 x 성능 품질 x = 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-207">OEE is an industry standard measure calculated by multiplying hello availability rate, performance rate, and quality rate: OEE = availability x performance x quality.</span></span>

![연결된 공장 미리 구성된 솔루션 OEE][cf-img-oee]

1. <span data-ttu-id="0dcd7-209">tooview OEE hello 계층의 모든 수준에 대 한 필요한 toohello 특정 보기를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-209">tooview OEE for any level in hello hierarchy, navigate toohello specific view you require.</span></span> <span data-ttu-id="0dcd7-210">해당 보기에 대 한 hello OEE 각 hello OEE 백분율을 구성 하는 hello 요소와 함께 hello 패널에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-210">hello OEE for that view displays in hello panel along with each of hello elements that make up hello OEE percentage.</span></span>

2. <span data-ttu-id="0dcd7-211">toofurther는 hello OEE hello 계층 구조 데이터의 모든 수준에 대 한 분석 hello OEE, 가용성, 성능 또는 품질 백분율을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-211">toofurther analyze hello OEE for any level in hello hierarchy data, click either hello OEE, availability, performance, or quality percentage.</span></span> <span data-ttu-id="0dcd7-212">시간 시계열 Insights hello 지난 시간, 지난 24 시간 및 지난 7 일간의에서 데이터를 표시 하는 저전력된 시각화 컨텍스트 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-212">A context panel appears with Time Series Insights powered visualizations that shows data from hello last hour, last 24 hours, and last 7 days.</span></span>

    ![연결된 공장 미리 구성된 솔루션 TSI 시각화][cf-img-tsi-visualization]

3. <span data-ttu-id="0dcd7-214">toofurther는 hello 경고 데이터를 분석, hello 경고 패널에서 hello 그래프를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-214">toofurther analyze hello alert data, click hello graph in hello alert panel.</span></span> <span data-ttu-id="0dcd7-215">Hello 시간 계열 Insights 탐색기 환경을 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-215">This action opens hello Time Series Insights explorer environment.</span></span>

    ![연결된 공장 미리 구성된 솔루션 TSI 탐색기][cf-img-tsi-explorer]

## <a name="view-key-performance-indicators"></a><span data-ttu-id="0dcd7-217">핵심 성과 지표 보기</span><span class="sxs-lookup"><span data-stu-id="0dcd7-217">View Key Performance Indicators</span></span>

<span data-ttu-id="0dcd7-218">hello 솔루션은 두 가지 핵심 성과 지표를 제공 */h* 및 *에너지 소비량 kwh에서*합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-218">hello solution provides two key performance indicators, *units per hour* and *energy used in kWh*.</span></span>

![연결된 공장 미리 구성된 솔루션 KPI][cf-img-kpi]

1. <span data-ttu-id="0dcd7-220">매 시간 마다 또는 hello 계층의 모든 수준에 사용 되는 에너지 tooview 단위 필요한 toohello 특정 보기를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-220">tooview units per hour or energy used for any level in hello hierarchy, navigate toohello specific view you require.</span></span> <span data-ttu-id="0dcd7-221">시간 및 에너지 당 hello 단위가 hello 패널에서 표시를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-221">hello units per hour and energy used display in hello panel.</span></span>

2. <span data-ttu-id="0dcd7-222">매 시간 마다 또는 또한 hello 계층의 모든 수준에 사용 되는 에너지 tooanalyze 단위 클릭 hello 계기 hello에 **핵심 성과 지표** 패널입니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-222">tooanalyze units per hour or energy used for any level in hello hierarchy further, click hello gauge in hello **Key Performance Indicators** panel.</span></span> <span data-ttu-id="0dcd7-223">Tooview 데이터 hello 지난 시간, 지난 24 시간 및 지난 7 일 동안 hello에서 사용 하면 전원이 시간 시계열 Insights 시각화는 상황에 맞는 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-223">A context panel appears with Time Series Insights powered visualizations enabling you tooview data from hello last hour, hello last 24 hours, and last 7 days.</span></span>

## <a name="scenario-review"></a><span data-ttu-id="0dcd7-224">시나리오 검토</span><span class="sxs-lookup"><span data-stu-id="0dcd7-224">Scenario review</span></span>

<span data-ttu-id="0dcd7-225">이 시나리오에서는 팩터리 OEE 및 Kpi 값을 하 여 hello 대시보드에 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-225">In this scenario, you monitored your factories OEE and KPIs values, in hello dashboard.</span></span> <span data-ttu-id="0dcd7-226">그런 다음 사용 시간 시계열 Insights tooprovide 자세한 정보 toohelp 드릴 추가로 hello 원격 분석 데이터에 비정상 탐지 된 toohelp OEE 및 Kpi에 대 한 했습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-226">You then used Time Series Insights tooprovide more information toohelp drill further into hello telemetry data for OEE and KPIs toohelp with detecting anomalies.</span></span> <span data-ttu-id="0dcd7-227">또한 프로그램 팩터리와 함께 hello 경고 패널 tooview 문제를 사용 하 고 hello 작업 사용 가능한 tooyou tooresolve hello 경고를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-227">You also used hello alert panel tooview issues with your factories and you used hello actions available tooyou tooresolve hello alert.</span></span>

## <a name="other-features"></a><span data-ttu-id="0dcd7-228">기타 기능</span><span class="sxs-lookup"><span data-stu-id="0dcd7-228">Other features</span></span>

<span data-ttu-id="0dcd7-229">다음 섹션 hello hello 이전 시나리오에서 설명 되지 않은 연결 hello 팩터리 솔루션의 일부의 기능을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-229">hello following sections describe some additional features of hello connected factory solution that are not described in hello previous scenario.</span></span>

## <a name="apply-filters"></a><span data-ttu-id="0dcd7-230">필터 적용</span><span class="sxs-lookup"><span data-stu-id="0dcd7-230">Apply filters</span></span>

1. <span data-ttu-id="0dcd7-231">Hello 클릭 **펼침** toodisplay hello 팩터리 위치 패널 또는 hello 경고 패널에서 사용 가능한 필터 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-231">Click hello **chevron** toodisplay a list of available filters in either hello factory locations panel or hello alerts panel.</span></span>

2. <span data-ttu-id="0dcd7-232">사용자에 대 한 hello 필터 패널이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-232">hello filters panel is displayed for you.</span></span> 

    ![연결된 공장 미리 구성된 솔루션 필터][cf-img-alert-filter]

3. <span data-ttu-id="0dcd7-234">필요한 hello 필터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-234">Choose hello filter that you require.</span></span> <span data-ttu-id="0dcd7-235">Hello 필터 필드에 가능한 tootype 자유 텍스트 이기도합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-235">It is also possible tootype free text into hello filter fields.</span></span>

4. <span data-ttu-id="0dcd7-236">hello 필터를 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-236">hello filter is then applied for you.</span></span> <span data-ttu-id="0dcd7-237">hello 필터 상태가 hello 팩터리를 표시 하 고 테이블을 경고 하는 깔때기형 통해 hello 대시보드에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-237">hello filter state is also shown in hello dashboard via a funnel that displays in hello factories and alerts tables.</span></span>

    ![연결된 공장 미리 구성된 솔루션 필터][cf-img-alert-filter-funnel]

    > [!NOTE]
    > <span data-ttu-id="0dcd7-239">활성 필터 표시 hello OEE 및 KPI 값에는 영향을 주지 hello 내용만 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-239">An active filter does not affect hello displayed OEE and KPI values, it only filters hello list contents.</span></span>

5. <span data-ttu-id="0dcd7-240">필터를 tooclear는 hello 깔때기형을 클릭 하 고 hello 필터 컨텍스트 창에서 필터를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-240">tooclear a filter, click hello funnel and click filter in hello filter context panel.</span></span> <span data-ttu-id="0dcd7-241">텍스트 hello **모든** hello 팩터리에 표시 되 고 테이블의 경고를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-241">hello text **All** is displayed in hello factories and alerts tables.</span></span>

## <a name="browse-an-opc-ua-server"></a><span data-ttu-id="0dcd7-242">OPC UA 서버 찾아보기</span><span class="sxs-lookup"><span data-stu-id="0dcd7-242">Browse an OPC UA server</span></span>

<span data-ttu-id="0dcd7-243">Hello 미리 구성 된 솔루션을 배포 하면 자동으로 서버를 프로 비전 시뮬레이션 OPC UA hello 솔루션 브라우저를 통해 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-243">When you deploy hello preconfigured solution, you automatically provision simulated OPC UA servers that you can browse via hello solution browser.</span></span> <span data-ttu-id="0dcd7-244">이러한 서버는 *시뮬레이션된 OPC UA 서버*입니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-244">These servers are *simulated OPC UA servers*.</span></span> <span data-ttu-id="0dcd7-245">시뮬레이션 된 서버에 더 쉽게 있습니다 tooexperiment hello 필요 toodeploy real, 물리적 서버 없이 hello 미리 구성 된 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-245">Simulated servers make it easy for you tooexperiment with hello preconfigured solution without hello need toodeploy real, physical servers.</span></span> <span data-ttu-id="0dcd7-246">실제 OPC UA 서버 toohello 솔루션 tooconnect 않으려면 참조 hello [OPC UA 장치 연결 toohello 미리 구성 하는 팩터리 솔루션 연결] [ lnk-connect-cf] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-246">If you do want tooconnect a real OPC UA server toohello solution, see hello [Connect your OPC UA device toohello connected factory preconfigured solution][lnk-connect-cf] tutorial.</span></span>

1. <span data-ttu-id="0dcd7-247">Hello 클릭 **팩터리 아이콘** hello 대시보드 탐색 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-247">Click hello **factory icon** in hello dashboard navigation bar.</span></span>

    ![연결된 공장 미리 구성된 솔루션 서버 브라우저][cf-img-server-browser]

2. <span data-ttu-id="0dcd7-249">Hello 미리 구성 된 목록에서 hello 서버 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-249">Choose one of hello servers from hello preconfigured list.</span></span> <span data-ttu-id="0dcd7-250">이 목록은 미리 구성 하는 hello 솔루션에서 사용자에 대 한 배포 된 hello 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-250">This list shows hello servers that are deployed for you in hello preconfigured solution.</span></span>

    ![연결된 공장 미리 구성된 솔루션 서버 선택][cf-img-server-choice]

3. <span data-ttu-id="0dcd7-252">**연결**을 클릭하면 보안 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-252">Click **Connect**, a security dialog displays.</span></span> <span data-ttu-id="0dcd7-253">Hello 시뮬레이션 것이 안전 tooclick **진행**</span><span class="sxs-lookup"><span data-stu-id="0dcd7-253">For hello simulation, it is safe tooclick **Proceed**</span></span>

4. <span data-ttu-id="0dcd7-254">tooexpand hello hello 서버 트리의 노드 중 하나를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-254">tooexpand any of hello nodes in hello server tree, click it.</span></span> <span data-ttu-id="0dcd7-255">원격 분석을 게시하는 노드 옆에는 눈금 표시가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-255">Nodes that are publishing telemetry have a tick mark beside them.</span></span>

    ![연결된 공장 미리 구성된 솔루션 서버 트리][cf-img-server-tree]

5. <span data-ttu-id="0dcd7-257">항목 tooread를 마우스 오른쪽 단추로 클릭, 작성, 게시, 또는 해당 노드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-257">Right-click an item tooread, write, publish, or call that node.</span></span> <span data-ttu-id="0dcd7-258">hello 동작 사용 가능한 tooyou 사용 권한 및 hello 노드의 hello 특성에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-258">hello actions available tooyou depend on your permissions and hello attributes of hello node.</span></span> <span data-ttu-id="0dcd7-259">hello 옵션 toodisplays hello 특정 노드의 hello 값을 보여 주는 컨텍스트 패널을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-259">hello read option toodisplays a context panel showing hello value of hello specific node.</span></span> <span data-ttu-id="0dcd7-260">hello 새 값을 입력할 수 있는 상황에 맞는 패널 옵션 표시를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-260">hello write option displays a context panel where you can enter a new value.</span></span> <span data-ttu-id="0dcd7-261">hello 통화 옵션 hello 호출에 대 한 hello 매개 변수를 입력할 수 있는 노드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-261">hello call option displays a node where you can enter hello parameters for hello call.</span></span>

## <a name="publish-a-node"></a><span data-ttu-id="0dcd7-262">노드 게시</span><span class="sxs-lookup"><span data-stu-id="0dcd7-262">Publish a node</span></span>

<span data-ttu-id="0dcd7-263">검색할 때는 *시뮬레이션된 OPC UA 서버*를 선택할 수도 있습니다 toopublish 새 노드.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-263">When you browse a *simulated OPC UA server*, you can also choose toopublish new nodes.</span></span> <span data-ttu-id="0dcd7-264">Hello 솔루션의 이러한 노드 모두에서 hello 원격 분석을 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-264">You can analyze hello telemetry from these nodes in hello solution.</span></span> <span data-ttu-id="0dcd7-265">이러한 *OPC UA 서버 시뮬레이션* real, 물리적 장치를 배포 하지 않고 쉽게 tooexperiment hello 미리 구성 된 솔루션을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-265">These *simulated OPC UA servers* make it easy tooexperiment with hello preconfigured solution without deploying real, physical devices.</span></span>

1. <span data-ttu-id="0dcd7-266">OPC UA 서버 브라우저 트리에서 toopublish 한다고 hello에서 tooa 노드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-266">Browse tooa node in hello OPC UA server browser tree that you wish toopublish.</span></span>

2. <span data-ttu-id="0dcd7-267">Hello 노드를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-267">Right-click hello node.</span></span>

3. <span data-ttu-id="0dcd7-268">**게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-268">Choose **Publish**.</span></span>

    ![연결된 공장 노드 게시][cf-img-publish-node]

4. <span data-ttu-id="0dcd7-270">상황에 맞는 패널 표시 게시 하면 hello 지시 성공 했습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-270">A context panel appears which tells you that hello publish has succeeded.</span></span> <span data-ttu-id="0dcd7-271">hello 노드 옆에 확인 표시가 있는 hello 스테이션 수준 보기에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-271">hello node appears in hello station level view with a check mark beside it.</span></span>

    ![연결된 공장 미리 구성된 솔루션 게시 성공][cf-img-publish-success]

## <a name="command-and-control"></a><span data-ttu-id="0dcd7-273">명령 및 컨트롤</span><span class="sxs-lookup"><span data-stu-id="0dcd7-273">Command and control</span></span>

<span data-ttu-id="0dcd7-274">연결 된 팩터리 hello 명령 및 hello 클라우드에서 직접 업계 장치를 사용 하 여 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-274">hello connected factory allows you command and control your industry devices directly from hello cloud.</span></span> <span data-ttu-id="0dcd7-275">이 기능은 toorespond tooalerts hello 장치 생성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-275">You can use this feature toorespond tooalerts generated by hello device.</span></span> <span data-ttu-id="0dcd7-276">예를 들어 hello 클라우드에서 명령 toohello 장치를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-276">For example, you could send a command toohello device from hello cloud.</span></span> <span data-ttu-id="0dcd7-277">Hello에서 사용할 수 있는 명령 hello를 찾을 수 **StationCommands** hello OPC UA 서버 브라우저 트리에서에서 노드.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-277">You can find hello available commands in hello **StationCommands** node in hello OPC UA servers browser tree.</span></span> <span data-ttu-id="0dcd7-278">이 시나리오에서는 생산 라인 뮌헨에 hello 어셈블리 스테이션에 압력 릴리스 밸브를 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-278">In this scenario, you open a pressure release valve on hello assembly station of a production line in Munich.</span></span> <span data-ttu-id="0dcd7-279">toouse hello 명령 및 제어 기능에에서 있어야 hello **관리자** hello에 대 한 역할 미리 솔루션 배포를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-279">toouse hello command and control functionality, you must be in hello **Administrator** role for hello preconfigured solution deployment.</span></span>

1. <span data-ttu-id="0dcd7-280">Toohello 찾아보기 **StationCommands** hello OPC UA 서버 브라우저 트리에서에서 노드.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-280">Browse toohello **StationCommands** node in hello OPC UA server browser tree.</span></span>

2. <span data-ttu-id="0dcd7-281">사용 하 여 원하는 hello 명령을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-281">Choose hello command that you wish use.</span></span>

3. <span data-ttu-id="0dcd7-282">Hello 노드를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-282">Right-click hello node.</span></span>

4. <span data-ttu-id="0dcd7-283">**호출**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-283">Choose **Call**.</span></span>

    ![연결된 공장 미리 구성된 솔루션 명령 호출][cf-img-call-command]

5. <span data-ttu-id="0dcd7-285">상황에 맞는 패널 toocall에 대 한 중인 방법을 알려주는 및 적용 가능한 모든 매개 변수 세부 정보는 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-285">A context panel appears informing you which method you are about toocall and any parameter details is applicable.</span></span>

6. <span data-ttu-id="0dcd7-286">**호출**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-286">Choose **Call**.</span></span>

    ![연결된 공장 미리 구성된 솔루션 호출 컨텍스트][cf-img-call-context]

7. <span data-ttu-id="0dcd7-288">hello 컨텍스트 패널은 업데이트 된 tooinform hello 메서드를 호출 하면 성공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-288">hello context panel is updated tooinform you that hello method call succeeded.</span></span> <span data-ttu-id="0dcd7-289">Hello 호출의 결과로 업데이트는 hello 압력 노드의 hello 값을 읽어 성공 hello 호출을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-289">You can verify hello call succeeded by reading hello value of hello pressure node that updated as a result of hello call.</span></span>

    ![연결된 공장 미리 구성된 솔루션 호출 성공][cf-img-call-success]


## <a name="behind-hello-scenes"></a><span data-ttu-id="0dcd7-291">Hello 백그라운드</span><span class="sxs-lookup"><span data-stu-id="0dcd7-291">Behind hello scenes</span></span>

<span data-ttu-id="0dcd7-292">미리 구성 된 솔루션을 배포 하면 hello 배포 프로세스 hello 선택한 Azure 구독에서에서 여러 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-292">When you deploy a preconfigured solution, hello deployment process creates multiple resources in hello Azure subscription you selected.</span></span> <span data-ttu-id="0dcd7-293">Hello Azure에서에서 이러한 리소스를 볼 수 있습니다 [포털][lnk-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-293">You can view these resources in hello Azure [portal][lnk-portal].</span></span> <span data-ttu-id="0dcd7-294">hello 배포 프로세스 생성 한 **리소스 그룹** 미리 구성 된 솔루션에 대해 선택한 hello 이름을 기반으로 하는 이름의:</span><span class="sxs-lookup"><span data-stu-id="0dcd7-294">hello deployment process creates a **resource group** with a name based on hello name you choose for your preconfigured solution:</span></span>

![Hello Azure 포털에서에서 미리 구성 된 솔루션][img-cf-portal]

<span data-ttu-id="0dcd7-296">Hello hello 리소스 그룹의 리소스 목록에서 선택 하 여 각 리소스의 hello 설정을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-296">You can view hello settings of each resource by selecting it in hello list of resources in hello resource group.</span></span>

<span data-ttu-id="0dcd7-297">미리 구성 하는 hello 솔루션에 대 한 hello 소스 코드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-297">You can also view hello source code for hello preconfigured solution.</span></span> <span data-ttu-id="0dcd7-298">hello 미리 구성 하는 연결 된 팩터리 솔루션 소스 코드는에 hello [azure iot-연결-공장] [ lnk-cfgithub] GitHub 리포지토리:</span><span class="sxs-lookup"><span data-stu-id="0dcd7-298">hello connected factory preconfigured solution source code is in hello [azure-iot-connected-factory][lnk-cfgithub] GitHub repository:</span></span>

<span data-ttu-id="0dcd7-299">완료 되 면 hello에 Azure 구독에서 미리 구성 하는 hello 솔루션을 삭제할 수 있습니다 [azureiotsuite.com] [ lnk-azureiotsuite] 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-299">When you are done, you can delete hello preconfigured solution from your Azure subscription on hello [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="0dcd7-300">이 사이트 tooeasily 삭제를 hello 미리 구성 된 솔루션을 만든 경우 프로 비전 된 리소스를 hello 모두 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-300">This site enables you tooeasily delete all hello resources that were provisioned when you created hello preconfigured solution.</span></span>

> [!NOTE]
> <span data-ttu-id="0dcd7-301">모든 항목을 삭제 하는 tooensure 관련 toohello 미리 구성 된 솔루션, hello에 삭제 [azureiotsuite.com] [ lnk-azureiotsuite] 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-301">tooensure that you delete everything related toohello preconfigured solution, delete it on hello [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="0dcd7-302">Hello 포털에서 hello 리소스 그룹을 삭제 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-302">Do not delete hello resource group in hello portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0dcd7-303">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0dcd7-303">Next Steps</span></span>

<span data-ttu-id="0dcd7-304">미리 구성 된 솔루션을 배포한 했으므로 hello 다음 문서를 참조 하 여 IoT Suite 시작을 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd7-304">Now that you’ve deployed a working preconfigured solution, you can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="0dcd7-305">[연결된 공장 미리 구성된 솔루션 연습][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="0dcd7-305">[Connected factory preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="0dcd7-306">[장치 toohello 미리 구성 하는 연결 된 팩터리 솔루션 연결][lnk-connect-cf]</span><span class="sxs-lookup"><span data-stu-id="0dcd7-306">[Connect your device toohello Connected factory preconfigured solution][lnk-connect-cf]</span></span>
* <span data-ttu-id="0dcd7-307">[Hello azureiotsuite.com 사이트에 대 한 권한][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="0dcd7-307">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>

[img-cf-home]:media/iot-suite-connected-factory-overview/cf-dashboard.png
[img-launch-solution]: media/iot-suite-connected-factory-overview/launch-cf.png
[cf-img-menu]: media/iot-suite-connected-factory-overview/cf-dashboard-menu.png
[cf-img-factories]:media/iot-suite-connected-factory-overview/cf-dashboard-factory.png
[cf-img-map]:media/iot-suite-connected-factory-overview/cf-dashboard-map.png
[cf-img-alerts]:media/iot-suite-connected-factory-overview/cf-dashboard-alerts.png
[cf-img-oee]:media/iot-suite-connected-factory-overview/cf-dashboard-oee.png
[cf-img-kpi]:media/iot-suite-connected-factory-overview/cf-dashboard-kpi.png
[cf-img-tsi-visualization]:media/iot-suite-connected-factory-overview/cf-dashboard-tsi.png
[cf-img-tsi-explorer]:media/iot-suite-connected-factory-overview/tsi-explorer.png
[cf-img-server-browser]: media/iot-suite-connected-factory-overview/cf-dashboard-browser.png
[cf-img-server-choice]: media/iot-suite-connected-factory-overview/cf-select-server.png
[cf-img-server-tree]:media/iot-suite-connected-factory-overview/cf-server-tree.png
[cf-img-publish-node]:media/iot-suite-connected-factory-overview/cf-publish-node1.png
[cf-img-publish-success]:media/iot-suite-connected-factory-overview/cf-publish-success.png
[cf-img-call-command]:media/iot-suite-connected-factory-overview/cf-command-and-control-call.png
[cf-img-call-context]:media/iot-suite-connected-factory-overview/cf-command-and-control-call-button.png
[cf-img-call-success]:media/iot-suite-connected-factory-overview/cf-command-and-control-succeed.png
[img-cf-portal]:media/iot-suite-connected-factory-overview/cf-resource-group.png
[cf-img-alert-filter]:media/iot-suite-connected-factory-overview/cf-filter.png
[cf-img-alert-filter-funnel]:media/iot-suite-connected-factory-overview/cf-filter-funnel.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-portal]: http://portal.azure.com/
[lnk-cfgithub]: https://github.com/Azure/azure-iot-connected-factory
[lnk-rm-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[lnk-connect-cf]: iot-suite-connected-factory-gateway-deployment.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-faq]: iot-suite-faq.md