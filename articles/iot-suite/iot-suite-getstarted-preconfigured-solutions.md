---
title: "시작 aaaGet 미리 솔루션 구성 | Microsoft Docs"
description: "이 자습서 toolearn에 따라 Azure IoT Suite toodeploy 미리 솔루션을 구성 하는 방법입니다."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 6ab38d1a-b564-469e-8a87-e597aa51d0f7
ms.service: iot-suite
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: a7f46023d26b08de2e8ed48c34c5066a43e3fa38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-preconfigured-solutions"></a><span data-ttu-id="4778d-103">미리 구성 하는 hello 솔루션 시작</span><span class="sxs-lookup"><span data-stu-id="4778d-103">Get started with hello preconfigured solutions</span></span>

<span data-ttu-id="4778d-104">Azure IoT Suite [솔루션 미리 구성 된] [ lnk-preconfigured-solutions] 일반적인 IoT 비즈니스 시나리오를 구현 하는 여러 Azure IoT 서비스 toodeliver 종단 간 솔루션을 결합 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-104">Azure IoT Suite [preconfigured solutions][lnk-preconfigured-solutions] combine multiple Azure IoT services toodeliver end-to-end solutions that implement common IoT business scenarios.</span></span> <span data-ttu-id="4778d-105">hello *원격 모니터링* 미리 구성 된 솔루션 tooand 모니터 하는 장치를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-105">hello *remote monitoring* preconfigured solution connects tooand monitors your devices.</span></span> <span data-ttu-id="4778d-106">프로세스 toothat 데이터 스트림을 자동으로 응답 하 여 hello 솔루션 tooanalyze hello 데이터 스트림의 장치와 tooimprove 비즈니스 결과에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-106">You can use hello solution tooanalyze hello stream of data from your devices and tooimprove business outcomes by making processes respond automatically toothat stream of data.</span></span>

<span data-ttu-id="4778d-107">이 자습서에서는 tooprovision hello 원격 모니터링 솔루션 미리 방법을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-107">This tutorial shows you how tooprovision hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="4778d-108">또한 안내 합니다 hello hello 미리 구성 된 솔루션의 기본 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-108">It also walks you through hello basic features of hello preconfigured solution.</span></span> <span data-ttu-id="4778d-109">이러한 기능 중 대부분 hello 솔루션에서 액세스할 수 있습니다 *대시보드* hello 미리 구성 된 솔루션의 일부로 배포 하는:</span><span class="sxs-lookup"><span data-stu-id="4778d-109">You can access many of these features from hello solution *dashboard* that deploys as part of hello preconfigured solution:</span></span>

![미리 구성된 원격 모니터링 솔루션 대시보드][img-dashboard]

<span data-ttu-id="4778d-111">toocomplete이이 자습서에서는 활성 Azure 구독이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-111">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="4778d-112">계정이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="4778d-113">자세한 내용은 [Azure 무료 평가판][lnk_free_trial]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4778d-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

## <a name="scenario-overview"></a><span data-ttu-id="4778d-114">시나리오 개요</span><span class="sxs-lookup"><span data-stu-id="4778d-114">Scenario overview</span></span>

<span data-ttu-id="4778d-115">Hello 원격 모니터링 미리 구성 된 솔루션을 배포 하면 toostep 원격 일반적인 모니터링 시나리오를 통해 사용할 수 있는 리소스와 미리 입력 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-115">When you deploy hello remote monitoring preconfigured solution, it is prepopulated with resources that enable you toostep through a common remote monitoring scenario.</span></span> <span data-ttu-id="4778d-116">이 시나리오에서는 몇 가지 장치 연결 된 toohello 솔루션 예기치 않은 온도 값 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-116">In this scenario, several devices connected toohello solution are reporting unexpected temperature values.</span></span> <span data-ttu-id="4778d-117">hello 다음 섹션에서는 방법을 보여 줍니다에:</span><span class="sxs-lookup"><span data-stu-id="4778d-117">hello following sections show you how to:</span></span>

* <span data-ttu-id="4778d-118">예기치 않은 온도 값을 보내는 hello 장치를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-118">Identify hello devices sending unexpected temperature values.</span></span>
* <span data-ttu-id="4778d-119">이러한 장치를 구성 toosend 원격 분석은 더 자세한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-119">Configure these devices toosend more detailed telemetry.</span></span>
* <span data-ttu-id="4778d-120">이러한 장치에서 hello 펌웨어를 업데이트 하 여 hello 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-120">Fix hello problem by updating hello firmware on these devices.</span></span>
* <span data-ttu-id="4778d-121">액션 hello 문제가 해결 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-121">Verify that your action has resolved hello issue.</span></span>

<span data-ttu-id="4778d-122">이 시나리오의 주요 기능은 수행할 수 있다는 이러한 모든 동작 원격으로 hello 솔루션 대시보드에서입니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-122">A key feature of this scenario is that you can perform all these actions remotely from hello solution dashboard.</span></span> <span data-ttu-id="4778d-123">물리적 액세스 toohello 장치 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-123">You do not need physical access toohello devices.</span></span>

## <a name="view-hello-solution-dashboard"></a><span data-ttu-id="4778d-124">Hello 솔루션 대시보드 보기</span><span class="sxs-lookup"><span data-stu-id="4778d-124">View hello solution dashboard</span></span>

<span data-ttu-id="4778d-125">hello 솔루션 대시보드 toomanage 배포 된 hello 솔루션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-125">hello solution dashboard enables you toomanage hello deployed solution.</span></span> <span data-ttu-id="4778d-126">예를 들어 원격 분석 보기, 장치 추가 및 규칙 구성 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-126">For example, you can view telemetry, add devices, and configure rules.</span></span>

1. <span data-ttu-id="4778d-127">Hello 프로 비전이 완료 된 시점과 미리 구성 된 솔루션에 대 한 hello 타일 나타냅니다 **준비**, 선택 **시작** tooopen 새 탭에서 원격 모니터링 솔루션 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-127">When hello provisioning is complete and hello tile for your preconfigured solution indicates **Ready**, choose **Launch** tooopen your remote monitoring solution portal in a new tab.</span></span>

    ![미리 구성 하는 hello 솔루션 시작][img-launch-solution]

1. <span data-ttu-id="4778d-129">기본적으로 hello 솔루션 포털 표시 hello *대시보드*합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-129">By default, hello solution portal shows hello *dashboard*.</span></span> <span data-ttu-id="4778d-130">Hello 메뉴를 사용 하 여 hello hello 페이지의 왼쪽에 hello 솔루션 포털의 tooother 영역을 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-130">You can navigate tooother areas of hello solution portal using hello menu on hello left-hand side of hello page.</span></span>

    ![미리 구성된 원격 모니터링 솔루션 대시보드][img-menu]

<span data-ttu-id="4778d-132">hello 대시보드 hello를 다음 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-132">hello dashboard displays hello following information:</span></span>

* <span data-ttu-id="4778d-133">각 장치의 hello 위치를 표시 하는 지도 toohello 솔루션을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-133">A map that displays hello location of each device connected toohello solution.</span></span> <span data-ttu-id="4778d-134">Hello 솔루션을 처음 실행할 때에 25 시뮬레이션 된 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-134">When you first run hello solution, there are 25 simulated devices.</span></span> <span data-ttu-id="4778d-135">hello 시뮬레이션 된 장치는 구현 Azure WebJobs로 되며 hello 솔루션 hello Bing Maps API tooplot 정보를 사용 하 여 hello 지도에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-135">hello simulated devices are implemented as Azure WebJobs, and hello solution uses hello Bing Maps API tooplot information on hello map.</span></span> <span data-ttu-id="4778d-136">Hello 참조 [FAQ] [ lnk-faq] toolearn 어떻게 toomake hello 맵 동적입니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-136">See hello [FAQ][lnk-faq] toolearn how toomake hello map dynamic.</span></span>
* <span data-ttu-id="4778d-137">**원격 분석 기록** 패널은 선택한 장치의 습도 및 온도 원격 분석을 거의 실시간으로 나타내고 최고, 최저 및 평균 습도와 같은 집계 데이터를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-137">A **Telemetry History** panel that plots humidity and temperature telemetry from a selected device in near real time and displays aggregate data such as maximum, minimum, and average humidity.</span></span>
* <span data-ttu-id="4778d-138">원격 분석 값이 임계값을 초과하면 **알람 기록** 패널에 최근 경보 이벤트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-138">An **Alarm History** panel that shows recent alarm events when a telemetry value has exceeded a threshold.</span></span> <span data-ttu-id="4778d-139">미리 구성 하는 hello 솔루션에서 만든 추가 toohello 예제에서 사용자 고유의 경보를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-139">You can define your own alarms in addition toohello examples created by hello preconfigured solution.</span></span>
* <span data-ttu-id="4778d-140">**작업** 패널은 예약된 작업에 대한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-140">A **Jobs** panel that displays information about scheduled jobs.</span></span> <span data-ttu-id="4778d-141">**관리 작업** 페이지에서 사용자 고유의 작업을 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-141">You can schedule your own jobs on **Management jobs** page.</span></span>

## <a name="view-alarms"></a><span data-ttu-id="4778d-142">알람 보기</span><span class="sxs-lookup"><span data-stu-id="4778d-142">View alarms</span></span>

<span data-ttu-id="4778d-143">5 개 장치 예상된 원격 분석 값 보다 높은 보고 hello 경보 기록 패널 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-143">hello alarm history panel shows you that five devices are reporting higher than expected telemetry values.</span></span>

![Hello 솔루션 대시보드에서 TODO 경보 기록][img-alarms]

> [!NOTE]
> <span data-ttu-id="4778d-145">이러한 경보 hello 미리 구성 된 솔루션에 포함 된 규칙에 의해 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-145">These alarms are generated by a rule that is included in hello preconfigured solution.</span></span> <span data-ttu-id="4778d-146">장치에서 보낸 hello 온도 값 60을 초과 하는 경우이 규칙에서 경고를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-146">This rule generates an alert when hello temperature value sent by a device exceeds 60.</span></span> <span data-ttu-id="4778d-147">선택 하 여 사용자 고유의 규칙 및 동작을 정의할 수 있습니다 [규칙](#add-a-rule) 및 [동작](#add-an-action) hello 왼쪽 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-147">You can define your own rules and actions by choosing [Rules](#add-a-rule) and [Actions](#add-an-action) in hello left-hand menu.</span></span>

## <a name="view-devices"></a><span data-ttu-id="4778d-148">장치 보기</span><span class="sxs-lookup"><span data-stu-id="4778d-148">View devices</span></span>

<span data-ttu-id="4778d-149">hello *장치* hello 솔루션에 모든 hello 등록 된 장치 목록에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-149">hello *devices* list shows all hello registered devices in hello solution.</span></span> <span data-ttu-id="4778d-150">Hello 장치 목록을 확인 하 고 장치 메타 데이터를 편집할 수에서 추가 또는 장치를 제거 하 고 장치에서 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-150">From hello device list you can view and edit device metadata, add or remove devices, and invoke methods on devices.</span></span> <span data-ttu-id="4778d-151">필터링 하거나 정렬할 수 hello hello 장치 목록에는 장치 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-151">You can filter and sort hello list of devices in hello device list.</span></span> <span data-ttu-id="4778d-152">Hello 장치 목록에 표시 되는 hello 열을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-152">You can also customize hello columns shown in hello device list.</span></span>

1. <span data-ttu-id="4778d-153">선택 **장치** 이 솔루션에 대 한 tooshow hello 장치 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-153">Choose **Devices** tooshow hello device list for this solution.</span></span>

   ![Hello hello 솔루션 포털에서 장치 목록 보기][img-devicelist]

1. <span data-ttu-id="4778d-155">hello 장치 목록에는 처음 25 개의 시뮬레이션 된 장치 hello를 프로 비전 프로세스에서 만든 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-155">hello device list initially shows 25 simulated devices created by hello provisioning process.</span></span> <span data-ttu-id="4778d-156">추가 시뮬레이션 및 물리적 장치 toohello 솔루션을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-156">You can add additional simulated and physical devices toohello solution.</span></span>

1. <span data-ttu-id="4778d-157">장치의 tooview hello 세부 hello 장치 목록에 장치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-157">tooview hello details of a device, choose a device in hello device list.</span></span>

   ![Hello 솔루션 포털에서 hello 장치 세부 정보 보기][img-devicedetails]

<span data-ttu-id="4778d-159">hello **장치 세부 정보** 패널에 6 개의 섹션이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-159">hello **Device Details** panel contains six sections:</span></span>

* <span data-ttu-id="4778d-160">링크는 사용 하면 toocustomize hello 장치 아이콘, hello 장치를 사용 하지 않도록 설정, 규칙을 추가, 메서드를 호출 하거나 명령을 보내의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-160">A collection of links that enable you toocustomize hello device icon, disable hello device, add a rule, invoke a method, or send a command.</span></span> <span data-ttu-id="4778d-161">명령(장치-클라우드 메시지) 및 메서드(직접 메서드)의 비교는 [클라우드-장치 통신 지침][lnk-c2d-guidance]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4778d-161">For a comparison of commands (device-to-cloud messages) and methods (direct methods), see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>
* <span data-ttu-id="4778d-162">hello **로 이중 장치-태그** 섹션에서는 hello 장치에 대 한 tooedit 태그 값입니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-162">hello **Device Twin - Tags** section enables you tooedit tag values for hello device.</span></span> <span data-ttu-id="4778d-163">Hello 장치 목록에 태그 값을 표시할 수 있으며 태그 값 toofilter hello 장치 목록을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-163">You can display tag values in hello device list and use tag values toofilter hello device list.</span></span>
* <span data-ttu-id="4778d-164">hello **장치로 이중-원하는 속성** 섹션에서는 tooset 속성 값 toobe 전송 toohello 장치 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-164">hello **Device Twin - Desired Properties** section enables you tooset property values toobe sent toohello device.</span></span>
* <span data-ttu-id="4778d-165">hello **장치로 이중-보고 속성** 섹션 hello 장치에서 전송 하는 속성 값을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-165">hello **Device Twin - Reported Properties** section shows property values sent from hello device.</span></span>
* <span data-ttu-id="4778d-166">hello **장치 속성** id 및 인증 키가 섹션 hello id 레지스트리에 hello 장치 등의 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-166">hello **Device Properties** section shows information from hello identity registry such as hello device id and authentication keys.</span></span>
* <span data-ttu-id="4778d-167">hello **최근 작업** 섹션 최근에 대상 지정이 장치는 모든 작업에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-167">hello **Recent Jobs** section shows information about any jobs that have recently targeted this device.</span></span>

## <a name="filter-hello-device-list"></a><span data-ttu-id="4778d-168">필터 hello 장치 목록</span><span class="sxs-lookup"><span data-stu-id="4778d-168">Filter hello device list</span></span>

<span data-ttu-id="4778d-169">필터 toodisplay 전송 하는 예기치 않은 온도 값 장치에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-169">You can use a filter toodisplay only those devices that are sending unexpected temperature values.</span></span> <span data-ttu-id="4778d-170">hello를 포함 하는 미리 구성 된 솔루션 모니터링 원격 hello **비정상 장치** 평균 온도 값이 60 보다 큰 tooshow 장치를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-170">hello remote monitoring preconfigured solution includes hello **Unhealthy devices** filter tooshow devices with a mean temperature value greater than 60.</span></span> <span data-ttu-id="4778d-171">[직접 필터를 만들 수](#add-a-filter)도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-171">You can also [create your own filters](#add-a-filter).</span></span>

1. <span data-ttu-id="4778d-172">선택 **필터를 저장 하는 열기** toodisplay 사용 가능한 필터 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-172">Choose **Open saved filter** toodisplay a list of available filters.</span></span> <span data-ttu-id="4778d-173">그런 다음 선택 **비정상 장치** tooapply hello 필터:</span><span class="sxs-lookup"><span data-stu-id="4778d-173">Then choose **Unhealthy devices** tooapply hello filter:</span></span>

    ![필터 hello 목록 표시][img-unhealthy-filter]

1. <span data-ttu-id="4778d-175">hello 장치 이제 목록은 평균 온도 값이 있는 장치만 60 보다 큰입니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-175">hello device list now shows only devices with a mean temperature value greater than 60.</span></span>

    ![정상이 아닌 장치를 보여 주는 hello 필터링 된 장치 목록 보기][img-filtered-unhealthy-list]

## <a name="update-desired-properties"></a><span data-ttu-id="4778d-177">desired 속성 업데이트</span><span class="sxs-lookup"><span data-stu-id="4778d-177">Update desired properties</span></span>

<span data-ttu-id="4778d-178">이제 수정이 필요할 수 있는 장치 집합을 식별했습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-178">You have now identified a set of devices that may need remediation.</span></span> <span data-ttu-id="4778d-179">그러나 15 초의 hello 데이터 주파수 명확한 진단 hello 문제에 대 한 충분 한지 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-179">However, you decide that hello data frequency of 15 seconds is not sufficient for a clear diagnosis of hello issue.</span></span> <span data-ttu-id="4778d-180">더 많은 데이터 포인트 toobetter는 hello 문제를 진단 hello 원격 분석 주파수 toofive 초 tooprovide 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-180">Changing hello telemetry frequency toofive seconds tooprovide you with more data points toobetter diagnose hello issue.</span></span> <span data-ttu-id="4778d-181">Hello 솔루션 포털에서이 구성 변경 tooyour 원격 장치에 푸시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-181">You can push this configuration change tooyour remote devices from hello solution portal.</span></span> <span data-ttu-id="4778d-182">한 번 hello 영향을 평가 하 고 hello 결과 hello 변경을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-182">You can make hello change once, evaluate hello impact, and then act on hello results.</span></span>

<span data-ttu-id="4778d-183">이러한 단계 toorun hello를 변경 하는 작업에 따라 **TelemetryInterval** hello 영향을 받는 장치에 대 한 속성이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-183">Follow these steps toorun a job that changes hello **TelemetryInterval** desired property for hello affected devices.</span></span> <span data-ttu-id="4778d-184">Hello 장치가 새 hello를 수신 하는 경우 **TelemetryInterval** 5 초 마다 15 초 마다 대신 자신의 구성 toosend 원격 분석 변경할 속성 값:</span><span class="sxs-lookup"><span data-stu-id="4778d-184">When hello devices receive hello new **TelemetryInterval** property value, they change their configuration toosend telemetry every five seconds instead of every 15 seconds:</span></span>

1. <span data-ttu-id="4778d-185">비정상 장치 목록이 hello를 hello 장치 목록에 표시 하는 동안 선택 **작업 스케줄러**, 다음 **장치로 이중 편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-185">While you are showing hello list of unhealthy devices in hello device list, choose **Job Scheduler**, then **Edit Device Twin**.</span></span>

1. <span data-ttu-id="4778d-186">Hello 작업 호출 **변경 원격 분석 간격**합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-186">Call hello job **Change telemetry interval**.</span></span>

1. <span data-ttu-id="4778d-187">Hello의 hello 값 변경 **원하는 속성** 이름 **원하는 합니다. Config.TelemetryInterval** toofive 초입니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-187">Change hello value of hello **Desired Property** name **desired.Config.TelemetryInterval** toofive seconds.</span></span>

1. <span data-ttu-id="4778d-188">**예약**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-188">Choose **Schedule**.</span></span>

    ![Hello TelemetryInterval 속성 toofive 초를 변경 합니다.][img-change-interval]

1. <span data-ttu-id="4778d-190">Hello에 hello 작업의 hello 진행률을 모니터링할 수 있습니다 **관리 작업** hello 포털의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-190">You can monitor hello progress of hello job on hello **Management Jobs** page in hello portal.</span></span>

> [!NOTE]
> <span data-ttu-id="4778d-191">Hello를 사용 하 여 개별 장치에 대 한 toochange 원하는 속성 값을 원하는 경우 **원하는 속성이** hello 섹션인 **장치 세부 정보** 작업을 실행 하는 대신 패널입니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-191">If you want toochange a desired property value for an individual device, use hello **Desired Properties** section in hello **Device Details** panel instead of running a job.</span></span>

<span data-ttu-id="4778d-192">Hello의 hello 값을 설정 하는이 작업 **TelemetryInterval** 모든 hello hello 필터에 의해 선택 되는 장치에 대 한 속성 hello 장치로 이중에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-192">This job sets hello value of hello **TelemetryInterval** desired property in hello device twin for all hello devices selected by hello filter.</span></span> <span data-ttu-id="4778d-193">hello 장치 hello 장치로 이중에서이 값을 검색 하 고 해당 명령의 동작은 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-193">hello devices retrieve this value from hello device twin and update their behavior.</span></span> <span data-ttu-id="4778d-194">검색 하 고 장치로 이중에서 원하는 속성을 처리 하는 장치 때 hello 해당 하는 보고 되는 값 속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-194">When a device retrieves and processes a desired property from a device twin, it sets hello corresponding reported value property.</span></span>

## <a name="invoke-methods"></a><span data-ttu-id="4778d-195">메서드 호출</span><span class="sxs-lookup"><span data-stu-id="4778d-195">Invoke methods</span></span>

<span data-ttu-id="4778d-196">Hello 작업이 실행 되는 동안 임을 알 있습니다 hello 비정상 장치 목록에서 이러한 모든 장치 (버전 1.6 보다 작음) 이전 펌웨어 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-196">While hello job runs, you notice in hello list of unhealthy devices that all these devices have old (less than version 1.6) firmware versions.</span></span>

![보기 hello 보고 hello 비정상 장치에 대 한 펌웨어 버전][img-old-firmware]

<span data-ttu-id="4778d-198">펌웨어 버전이 예기치 않은 hello의 근본 원인을 hello 수 있습니다 다른 정상 장치 최근에 업데이트 된 tooversion 2.0 했는지 알고 있으므로 온도 값입니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-198">This firmware version may be hello root cause of hello unexpected temperature values because you know that other healthy devices were recently updated tooversion 2.0.</span></span> <span data-ttu-id="4778d-199">Hello 기본 제공을 사용할 수 있습니다 **이전 펌웨어 장치** tooidentify 이전 펌웨어 버전으로 모든 장치를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-199">You can use hello built-in **Old firmware devices** filter tooidentify any devices with old firmware versions.</span></span> <span data-ttu-id="4778d-200">Hello 포털에서 원격으로 업데이트할 수 있습니다 여전히 이전 펌웨어 버전을 실행 하는 모든 hello 장치:</span><span class="sxs-lookup"><span data-stu-id="4778d-200">From hello portal, you can then remotely update all hello devices still running old firmware versions:</span></span>

1. <span data-ttu-id="4778d-201">선택 **필터를 저장 하는 열기** toodisplay 사용 가능한 필터 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-201">Choose **Open saved filter** toodisplay a list of available filters.</span></span> <span data-ttu-id="4778d-202">그런 다음 선택 **이전 펌웨어 장치** tooapply hello 필터:</span><span class="sxs-lookup"><span data-stu-id="4778d-202">Then choose **Old firmware devices** tooapply hello filter:</span></span>

    ![필터 hello 목록 표시][img-old-filter]

1. <span data-ttu-id="4778d-204">hello 장치 목록에는 이제 이전 펌웨어 버전으로는 장치에만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-204">hello device list now shows only devices with old firmware versions.</span></span> <span data-ttu-id="4778d-205">이 목록에 hello hello로 식별 되는 5 개 장치 **비정상 장치** 필터 및 3 개의 추가 장치:</span><span class="sxs-lookup"><span data-stu-id="4778d-205">This list includes hello five devices identified by hello **Unhealthy devices** filter and three additional devices:</span></span>

    ![오래 된 장치를 보여 주는 hello 필터링 된 장치 목록 보기][img-filtered-old-list]

1. <span data-ttu-id="4778d-207">**작업 스케줄러**, **메서드 호출**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-207">Choose **Job Scheduler**, then **Invoke Method**.</span></span>

1. <span data-ttu-id="4778d-208">설정 **작업 이름** 너무**펌웨어 업데이트 tooversion 2.0**합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-208">Set **Job Name** too**Firmware update tooversion 2.0**.</span></span>

1. <span data-ttu-id="4778d-209">선택 **InitiateFirmwareUpdate** hello로 **메서드**합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-209">Choose **InitiateFirmwareUpdate** as hello **Method**.</span></span>

1. <span data-ttu-id="4778d-210">집합 hello **FwPackageUri** 매개 변수가 너무**https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-210">Set hello **FwPackageUri** parameter too**https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.</span></span>

1. <span data-ttu-id="4778d-211">**예약**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-211">Choose **Schedule**.</span></span> <span data-ttu-id="4778d-212">hello 기본값 hello 작업 toorun 이제은입니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-212">hello default is for hello job toorun now.</span></span>

    ![선택한 hello 장치 tooupdate hello 펌웨어 작업 만들기][img-method-update]

> [!NOTE]
> <span data-ttu-id="4778d-214">개별 장치에 대 한 메서드에 tooinvoke 선택 **메서드** hello에 **장치 세부 정보** 작업을 실행 하는 대신 패널입니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-214">If you want tooinvoke a method on an individual device, choose **Methods** in hello **Device Details** panel instead of running a job.</span></span>

<span data-ttu-id="4778d-215">이 작업 호출 hello **InitiateFirmwareUpdate** hello 필터에 의해 선택 되는 모든 hello 장치에서 직접적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-215">This job invokes hello **InitiateFirmwareUpdate** direct method on all hello devices selected by hello filter.</span></span> <span data-ttu-id="4778d-216">장치는 tooIoT 허브 즉시 응답을 비동기적으로 hello 펌웨어 업데이트 프로세스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-216">Devices respond immediately tooIoT Hub and then initiate hello firmware update process asynchronously.</span></span> <span data-ttu-id="4778d-217">hello 장치 hello 스크린샷을 보려면 다음 그림과 같이 hello 펌웨어 업데이트 프로세스를 통해 보고 된 속성 값에 대 한 상태 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-217">hello devices provide status information about hello firmware update process through reported property values, as shown in hello following screenshots.</span></span> <span data-ttu-id="4778d-218">Hello 선택 **새로 고침** hello 장치 및 작업 목록에서 아이콘 tooupdate hello 정보:</span><span class="sxs-lookup"><span data-stu-id="4778d-218">Choose hello **Refresh** icon tooupdate hello information in hello device and job lists:</span></span>

<span data-ttu-id="4778d-219">![Hello 펌웨어 업데이트 목록 실행을 표시 하는 작업 목록이][img-update-1]
![펌웨어 업데이트 상태를 표시 하는 장치 목록][img-update-2]
![작업 목록 표시 된 hello 펌웨어 업데이트 목록 완료][img-update-3]</span><span class="sxs-lookup"><span data-stu-id="4778d-219">![Job list showing hello firmware update list running][img-update-1]
![Device list showing firmware update status][img-update-2]
![Job list showing hello firmware update list complete][img-update-3]</span></span>

> [!NOTE]
> <span data-ttu-id="4778d-220">프로덕션 환경에서 지정 된 유지 관리 기간 동안 작업 toorun를 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-220">In a production environment, you can schedule jobs toorun during a designated maintenance window.</span></span>

## <a name="scenario-review"></a><span data-ttu-id="4778d-221">시나리오 검토</span><span class="sxs-lookup"><span data-stu-id="4778d-221">Scenario review</span></span>

<span data-ttu-id="4778d-222">이 시나리오에서는 일부 hello 경보 기록 hello 대시보드 및 필터를 사용 하 여 원격 장치도 잠재적인 문제를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-222">In this scenario, you identified a potential issue with some of your remote devices using hello alarm history on hello dashboard and a filter.</span></span> <span data-ttu-id="4778d-223">하 한 다음 사용 하는 hello 필터와 작업 tooremotely 구성 hello 장치 tooprovide 자세한 정보 toohelp hello 문제를 진단 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-223">You then used hello filter and a job tooremotely configure hello devices tooprovide more information toohelp diagnose hello issue.</span></span> <span data-ttu-id="4778d-224">마지막으로 사용한 작업 tooschedule 유지 관리 및 필터와 hello 영향을 받는 장치에 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-224">Finally, you used a filter and a job tooschedule maintenance on hello affected devices.</span></span> <span data-ttu-id="4778d-225">Toohello 대시보드를 반환 하는 경우 솔루션에 장치에서 오는 모든 경보 더 이상 없는지 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-225">If you return toohello dashboard, you can check that there are no longer any alarms coming from devices in your solution.</span></span> <span data-ttu-id="4778d-226">필터를 사용할 수 있습니다 및 더 이상 비정상 장치가 펌웨어 hello tooverify 솔루션의 모든 hello 장치에서 최신 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-226">You can use a filter tooverify that hello firmware is up-to-date on all hello devices in your solution and that there are no more unhealthy devices:</span></span>

![모든 장치의 펌웨어가 최신이라는 것을 보여주는 필터][img-updated]

![모든 장치가 정상이라는 것을 보여주는 필터][img-healthy]

## <a name="other-features"></a><span data-ttu-id="4778d-229">기타 기능</span><span class="sxs-lookup"><span data-stu-id="4778d-229">Other features</span></span>

<span data-ttu-id="4778d-230">hello 다음 단원에서는 hello 이전 시나리오의 일부로 설명 되지 않은 hello 원격 모니터링 미리 구성 된 솔루션의 몇 가지 추가 기능.</span><span class="sxs-lookup"><span data-stu-id="4778d-230">hello following sections describe some additional features of hello remote monitoring preconfigured solution that are not described as part of hello previous scenario.</span></span>

### <a name="customize-columns"></a><span data-ttu-id="4778d-231">열 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="4778d-231">Customize columns</span></span>

<span data-ttu-id="4778d-232">선택 하 여 hello 장치 목록에 표시 되는 hello 정보를 사용자 지정할 수 있습니다 **열 편집기**합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-232">You can customize hello information shown in hello device list by choosing **Column editor**.</span></span> <span data-ttu-id="4778d-233">reported 속성 및 태그 값을 표시하는 열을 추가 및 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-233">You can add and remove columns that display reported property and tag values.</span></span> <span data-ttu-id="4778d-234">또한 열의 순서를 변경하고 이름을 바꿀 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-234">You can also reorder and rename columns:</span></span>

   ![열 편집기 이온 hello 장치 목록][img-columneditor]

### <a name="customize-hello-device-icon"></a><span data-ttu-id="4778d-236">Hello 장치 아이콘을 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="4778d-236">Customize hello device icon</span></span>

<span data-ttu-id="4778d-237">Hello에서 hello 장치 목록에 표시 된 hello 장치 아이콘을 사용자 지정할 수 있습니다 **장치 세부 정보** 패널 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-237">You can customize hello device icon displayed in hello device list from hello **Device Details** panel as follows:</span></span>

1. <span data-ttu-id="4778d-238">Hello 연필 아이콘 tooopen hello 선택 **이미지 편집** 장치에 대 한 패널:</span><span class="sxs-lookup"><span data-stu-id="4778d-238">Choose hello pencil icon tooopen hello **Edit image** panel for a device:</span></span>

   ![장치 이미지 편집기 열기][img-startimageedit]

1. <span data-ttu-id="4778d-240">새 이미지를 업로드 하거나 hello 기존 이미지 중 하나를 사용 하 여 다음 선택 및 **저장**:</span><span class="sxs-lookup"><span data-stu-id="4778d-240">Either upload a new image or use one of hello existing images and then choose **Save**:</span></span>

   ![장치 이미지 편집기 편집][img-imageedit]

1. <span data-ttu-id="4778d-242">hello 이제 선택한 이미지에에서 표시 hello **아이콘** hello 장치에 대 한 열입니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-242">hello image you selected now displays in hello **Icon** column for hello device.</span></span>

> [!NOTE]
> <span data-ttu-id="4778d-243">hello 이미지 blob 저장소에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-243">hello image is stored in blob storage.</span></span> <span data-ttu-id="4778d-244">태그 hello 장치로 이중에 링크 toohello 이미지를 blob 저장소에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-244">A tag in hello device twin contains a link toohello image in blob storage.</span></span>

### <a name="add-a-device"></a><span data-ttu-id="4778d-245">장치 추가</span><span class="sxs-lookup"><span data-stu-id="4778d-245">Add a device</span></span>

<span data-ttu-id="4778d-246">Hello 미리 구성 된 솔루션을 배포 하면 자동으로 장치를 프로 비전 25 샘플 hello 장치 목록에 표시 될 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-246">When you deploy hello preconfigured solution, you automatically provision 25 sample devices that you can see in hello device list.</span></span> <span data-ttu-id="4778d-247">이러한 장치는 Azure WebJob에서 실행되는 *시뮬레이션된 장치* 입니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-247">These devices are *simulated devices* running in an Azure WebJob.</span></span> <span data-ttu-id="4778d-248">시뮬레이션 된 장치에 더 쉽게 있습니다 tooexperiment hello 필요 toodeploy real, 실제 장치 없이 hello 미리 구성 된 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-248">Simulated devices make it easy for you tooexperiment with hello preconfigured solution without hello need toodeploy real, physical devices.</span></span> <span data-ttu-id="4778d-249">실제 장치 toohello 솔루션 tooconnect 않으려면 참조 hello [원격 미리 구성 된 솔루션을 모니터링 하 여 장치 toohello 연결] [ lnk-connect-rm] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-249">If you do want tooconnect a real device toohello solution, see hello [Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm] tutorial.</span></span>

<span data-ttu-id="4778d-250">hello 다음 단계 방법을 보여 줍니다 tooadd 시뮬레이션 된 장치 toohello 솔루션:</span><span class="sxs-lookup"><span data-stu-id="4778d-250">hello following steps show you how tooadd a simulated device toohello solution:</span></span>

1. <span data-ttu-id="4778d-251">뒤로 toohello 장치 목록을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-251">Navigate back toohello device list.</span></span>

1. <span data-ttu-id="4778d-252">장치 tooadd 선택 **+ A 장치 추가** hello 하단 왼쪽된 모서리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-252">tooadd a device, choose **+ Add A Device** in hello bottom left corner.</span></span>

   ![장치 미리 구성 된 toohello 솔루션 추가][img-adddevice]

1. <span data-ttu-id="4778d-254">선택 **새로 추가** hello에 **시뮬레이션 된 장치** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-254">Choose **Add New** on hello **Simulated Device** tile.</span></span>

   ![대시보드에서 새 장치 세부 정보 설정][img-addnew]

   <span data-ttu-id="4778d-256">또한 toocreating 새 시뮬레이션 된 장치에에서 추가할 수도 있습니다는 물리적 장치 toocreate를 선택 하는 경우는 **사용자 지정 장치**합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-256">In addition toocreating a new simulated device, you can also add a physical device if you choose toocreate a **Custom Device**.</span></span> <span data-ttu-id="4778d-257">물리적 장치 toohello 솔루션 연결에 대해 자세히 toolearn 참조 [IoT Suite 원격 미리 구성 된 솔루션을 모니터링 하 여 장치 toohello 연결][lnk-connect-rm]합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-257">toolearn more about connecting physical devices toohello solution, see [Connect your device toohello IoT Suite remote monitoring preconfigured solution][lnk-connect-rm].</span></span>

1. <span data-ttu-id="4778d-258">**나만의 장치 ID 정의**를 선택하고 **mydevice_01**처럼 고유한 장치 ID 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-258">Select **Let me define my own Device ID**, and enter a unique device ID name such as **mydevice_01**.</span></span>

1. <span data-ttu-id="4778d-259">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-259">Choose **Create**.</span></span>

   ![새 장치 저장][img-definedevice]

1. <span data-ttu-id="4778d-261">3 단계에서 **시뮬레이션 된 장치를 추가할**, 선택 **수행** tooreturn toohello 장치 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-261">In step 3 of **Add a simulated device**, choose **Done** tooreturn toohello device list.</span></span>

1. <span data-ttu-id="4778d-262">장치를 볼 수 있습니다 **실행** hello 장치 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-262">You can view your device **Running** in hello device list.</span></span>

    ![장치 목록에서 새 장치 보기][img-runningnew]

1. <span data-ttu-id="4778d-264">ְ ײ hello hello 대시보드에서 새 장치에서 원격 분석을 시뮬레이션 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-264">You can also view hello simulated telemetry from your new device on hello dashboard:</span></span>

    ![새 장치에서 원격 분석 보기][img-runningnew-2]

### <a name="disable-and-delete-a-device"></a><span data-ttu-id="4778d-266">장치 비활성화 및 삭제</span><span class="sxs-lookup"><span data-stu-id="4778d-266">Disable and delete a device</span></span>

<span data-ttu-id="4778d-267">장치를 비활성화할 수 있으며, 비활성화된 후에는 파일을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-267">You can disable a device, and after it is disabled you can remove it:</span></span>

![장치 비활성화 및 제거][img-disable]

### <a name="add-a-rule"></a><span data-ttu-id="4778d-269">규칙 추가</span><span class="sxs-lookup"><span data-stu-id="4778d-269">Add a rule</span></span>

<span data-ttu-id="4778d-270">방금 추가한 hello 새 장치에 대 한 규칙이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-270">There are no rules for hello new device you just added.</span></span> <span data-ttu-id="4778d-271">이 섹션에서는 47도 초과 하는 장치 온도 hello hello 새 보고 경보를 트리거하는 규칙을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-271">In this section, you add a rule that triggers an alarm when hello temperature reported by hello new device exceeds 47 degrees.</span></span> <span data-ttu-id="4778d-272">시작 하기 전에 표시 hello 대시보드에서 hello 새 장치에 대 한 원격 분석 기록을 hello hello 장치 온도 45도 초과 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-272">Before you start, notice that hello telemetry history for hello new device on hello dashboard shows hello device temperature never exceeds 45 degrees.</span></span>

1. <span data-ttu-id="4778d-273">뒤로 toohello 장치 목록을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-273">Navigate back toohello device list.</span></span>

1. <span data-ttu-id="4778d-274">hello에 새 장치를 선택 하는 hello 장치에 대 한 규칙 tooadd **장치 목록**, 선택한 후 **규칙 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-274">tooadd a rule for hello device, select your new device in hello **Devices List**, and then choose **Add rule**.</span></span>

1. <span data-ttu-id="4778d-275">사용 하는 규칙을 만들 **온도** hello 데이터 필드와 사용으로 **AlarmTemp** hello hello 온도 47도 초과 하는 경우 출력로:</span><span class="sxs-lookup"><span data-stu-id="4778d-275">Create a rule that uses **Temperature** as hello data field and uses **AlarmTemp** as hello output when hello temperature exceeds 47 degrees:</span></span>

    ![장치 규칙 추가][img-adddevicerule]

1. <span data-ttu-id="4778d-277">변경 내용을 선택 toosave **저장 및 규칙 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-277">toosave your changes, choose **Save and View Rules**.</span></span>

1. <span data-ttu-id="4778d-278">선택 **명령을** hello 새 장치에 대 한 hello 장치 세부 정보 창에서.</span><span class="sxs-lookup"><span data-stu-id="4778d-278">Choose **Commands** in hello device details pane for hello new device.</span></span>

    ![장치 규칙 추가][img-adddevicerule2]

1. <span data-ttu-id="4778d-280">선택 **ChangeSetPointTemp** hello 명령 목록 및 집합에서 **SetPointTemp** too45 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-280">Select **ChangeSetPointTemp** from hello command list and set **SetPointTemp** too45.</span></span> <span data-ttu-id="4778d-281">그런 다음 **명령 보내기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-281">Then choose **Send Command**:</span></span>

    ![장치 규칙 추가][img-adddevicerule3]

1. <span data-ttu-id="4778d-283">뒤로 toohello 대시보드를 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-283">Navigate back toohello dashboard.</span></span> <span data-ttu-id="4778d-284">짧은 시간 후 hello에 새 항목이 표시 됩니다 **경보 기록** hello 47도 임계값을 초과 하는 hello 온도 새 장치에서 보고 하는 경우 창:</span><span class="sxs-lookup"><span data-stu-id="4778d-284">After a short time, you will see a new entry in hello **Alarm History** pane when hello temperature reported by your new device exceeds hello 47-degree threshold:</span></span>

    ![장치 규칙 추가][img-adddevicerule4]

1. <span data-ttu-id="4778d-286">검토 하 고 hello에서 모든 규칙을 편집할 수 **규칙** hello 대시보드 페이지의:</span><span class="sxs-lookup"><span data-stu-id="4778d-286">You can review and edit all your rules on hello **Rules** page of hello dashboard:</span></span>

    ![장치 규칙 나열][img-rules]

1. <span data-ttu-id="4778d-288">검토 하 고 hello에서 응답 tooa 규칙에서 수행할 수 있는 모든 hello 동작을 편집할 수 **동작** hello 대시보드 페이지의:</span><span class="sxs-lookup"><span data-stu-id="4778d-288">You can review and edit all hello actions that can be taken in response tooa rule on hello **Actions** page of hello dashboard:</span></span>

    ![장치 작업 나열][img-actions]

> [!NOTE]
> <span data-ttu-id="4778d-290">전자 메일 메시지를 보낼 수 있는 가능한 toodefine 작업 인지에 대 한 응답 tooa SMS 규칙 또는 통해 업무의 시스템과 통합는 [논리 앱][lnk-logic-apps]합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-290">It is possible toodefine actions that can send an email message or SMS in response tooa rule or integrate with a line-of-business system through a [Logic App][lnk-logic-apps].</span></span> <span data-ttu-id="4778d-291">자세한 내용은 참조 hello [솔루션을 미리 구성 된 Azure IoT Suite 원격 모니터링 논리 앱 연결 tooyour][lnk-logicapptutorial]합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-291">For more information, see hello [Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapptutorial].</span></span>

### <a name="manage-filters"></a><span data-ttu-id="4778d-292">필터 관리</span><span class="sxs-lookup"><span data-stu-id="4778d-292">Manage filters</span></span>

<span data-ttu-id="4778d-293">Hello 장치 목록에서 생성, 저장 및 필터 toodisplay 장치 연결 된 tooyour 허브의 사용자 지정된 목록을 다시 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-293">In hello device list, you can create, save, and reload filters toodisplay a customized list of devices connected tooyour hub.</span></span> <span data-ttu-id="4778d-294">toocreate 필터:</span><span class="sxs-lookup"><span data-stu-id="4778d-294">toocreate a filter:</span></span>

1. <span data-ttu-id="4778d-295">장치의 hello 목록 위의 hello 편집 필터 아이콘을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-295">Choose hello edit filter icon above hello list of devices:</span></span>

    ![필터 편집기 열기 hello][img-editfiltericon]

1. <span data-ttu-id="4778d-297">Hello에 **필터 편집기**, hello 필드, 연산자 및 값 toofilter hello 장치 목록에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-297">In hello **Filter editor**, add hello fields, operators, and values toofilter hello device list.</span></span> <span data-ttu-id="4778d-298">여러 절 toorefine 필터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-298">You can add multiple clauses toorefine your filter.</span></span> <span data-ttu-id="4778d-299">선택 **필터** tooapply hello 필터:</span><span class="sxs-lookup"><span data-stu-id="4778d-299">Choose **Filter** tooapply hello filter:</span></span>

    ![필터 만들기][img-filtereditor]

1. <span data-ttu-id="4778d-301">이 예제에서는 제조업체 및 모델 번호 hello 목록 필터링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-301">In this example, hello list is filtered by manufacturer and model number:</span></span>

    ![필터링된 목록][img-filterelist]

1. <span data-ttu-id="4778d-303">toosave에 사용자 지정 이름을 필터 선택 hello **다른 이름으로 저장** 아이콘:</span><span class="sxs-lookup"><span data-stu-id="4778d-303">toosave your filter with a custom name, choose hello **Save as** icon:</span></span>

    ![필터 저장][img-savefilter]

1. <span data-ttu-id="4778d-305">이전에 저장 한 필터 tooreapply 선택 hello **필터를 저장 하는 열기** 아이콘:</span><span class="sxs-lookup"><span data-stu-id="4778d-305">tooreapply a filter you saved previously, choose hello **Open saved filter** icon:</span></span>

    ![필터 열기][img-openfilter]

<span data-ttu-id="4778d-307">장치 ID, 장치 상태, desired 속성, reported 속성 및 태그를 기준으로 필터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-307">You can create filters based on device id, device state, desired properties, reported properties, and tags.</span></span> <span data-ttu-id="4778d-308">Hello에 고유한 사용자 지정 태그 tooa 장치를 추가한 **태그** hello 섹션 **장치 세부 정보** 패널 또는 여러 장치에서 작업 tooupdate 태그를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-308">You add your own custom tags tooa device in hello **Tags** section of hello **Device Details** panel, or run a job tooupdate tags on multiple devices.</span></span>

> [!NOTE]
> <span data-ttu-id="4778d-309">Hello에 **필터 편집기**, hello를 사용할 수 있습니다 **고급 뷰** tooedit hello 쿼리 텍스트 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-309">In hello **Filter editor**, you can use hello **Advanced view** tooedit hello query text directly.</span></span>

### <a name="commands"></a><span data-ttu-id="4778d-310">명령</span><span class="sxs-lookup"><span data-stu-id="4778d-310">Commands</span></span>

<span data-ttu-id="4778d-311">Hello에서 **장치 세부 정보** 패널 toohello 장치 명령을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-311">From hello **Device Details** panel, you can send commands toohello device.</span></span> <span data-ttu-id="4778d-312">장치를 처음 시작할 때 hello에 대 한 정보 toohello 솔루션을 지원 명령을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-312">When a device first starts, it sends information about hello commands it supports toohello solution.</span></span> <span data-ttu-id="4778d-313">명령 및 메서드 hello 차이점의 논의 알려면 [Azure IoT Hub 클라우드-장치 옵션][lnk-c2d-guidance]합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-313">For a discussion of hello differences between commands and methods, see [Azure IoT Hub cloud-to-device options][lnk-c2d-guidance].</span></span>

1. <span data-ttu-id="4778d-314">선택 **명령을** hello에 **장치 세부 정보** hello 선택한 장치에 대 한 패널:</span><span class="sxs-lookup"><span data-stu-id="4778d-314">Choose **Commands** in hello **Device Details** panel for hello selected device:</span></span>

   ![대시보드의 장치 명령][img-devicecommands]

1. <span data-ttu-id="4778d-316">선택 **PingDevice** hello 명령 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-316">Select **PingDevice** from hello command list.</span></span>

1. <span data-ttu-id="4778d-317">**명령 보내기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-317">Choose **Send Command**.</span></span>

1. <span data-ttu-id="4778d-318">Hello hello 명령 기록에서 hello 명령 상태를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-318">You can see hello status of hello command in hello command history.</span></span>

   ![대시보드의 명령 상태][img-pingcommand]

<span data-ttu-id="4778d-320">보내는 각 명령의 hello 상태를 추적 하는 hello 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-320">hello solution tracks hello status of each command it sends.</span></span> <span data-ttu-id="4778d-321">Hello 결과 처음 **보류 중인**합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-321">Initially hello result is **Pending**.</span></span> <span data-ttu-id="4778d-322">Hello 결과 너무 설정 hello 장치를 보고할 때 서버 hello 명령 실행에,**성공**합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-322">When hello device reports that it has executed hello command, hello result is set too**Success**.</span></span>

## <a name="behind-hello-scenes"></a><span data-ttu-id="4778d-323">Hello 백그라운드</span><span class="sxs-lookup"><span data-stu-id="4778d-323">Behind hello scenes</span></span>

<span data-ttu-id="4778d-324">미리 구성 된 솔루션을 배포 하면 hello 배포 프로세스 hello 선택한 Azure 구독에서에서 여러 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-324">When you deploy a preconfigured solution, hello deployment process creates multiple resources in hello Azure subscription you selected.</span></span> <span data-ttu-id="4778d-325">Hello Azure에서에서 이러한 리소스를 볼 수 있습니다 [포털][lnk-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-325">You can view these resources in hello Azure [portal][lnk-portal].</span></span> <span data-ttu-id="4778d-326">hello 배포 프로세스 생성 한 **리소스 그룹** 미리 구성 된 솔루션에 대해 선택한 hello 이름을 기반으로 하는 이름의:</span><span class="sxs-lookup"><span data-stu-id="4778d-326">hello deployment process creates a **resource group** with a name based on hello name you choose for your preconfigured solution:</span></span>

![Hello Azure 포털에서에서 미리 구성 된 솔루션][img-portal]

<span data-ttu-id="4778d-328">Hello hello 리소스 그룹의 리소스 목록에서 선택 하 여 각 리소스의 hello 설정을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-328">You can view hello settings of each resource by selecting it in hello list of resources in hello resource group.</span></span>

<span data-ttu-id="4778d-329">미리 구성 하는 hello 솔루션에 대 한 hello 소스 코드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-329">You can also view hello source code for hello preconfigured solution.</span></span> <span data-ttu-id="4778d-330">원격 소스 코드를 미리 구성 된 솔루션을 모니터링 하는 hello hello 중인 [azure iot-원격 액세스 모니터링] [ lnk-rmgithub] GitHub 리포지토리:</span><span class="sxs-lookup"><span data-stu-id="4778d-330">hello remote monitoring preconfigured solution source code is in hello [azure-iot-remote-monitoring][lnk-rmgithub] GitHub repository:</span></span>

* <span data-ttu-id="4778d-331">hello **DeviceAdministration** 폴더 hello 대시보드에 대 한 hello 소스 코드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-331">hello **DeviceAdministration** folder contains hello source code for hello dashboard.</span></span>
* <span data-ttu-id="4778d-332">hello **시뮬레이터** 폴더 hello 시뮬레이션 된 장치에 대 한 hello 소스 코드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-332">hello **Simulator** folder contains hello source code for hello simulated device.</span></span>
* <span data-ttu-id="4778d-333">hello **EventProcessor** 폴더 hello 들어오는 원격 분석을 처리 하는 hello 백 엔드 프로세스에 대 한 hello 소스 코드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-333">hello **EventProcessor** folder contains hello source code for hello back-end process that handles hello incoming telemetry.</span></span>

<span data-ttu-id="4778d-334">완료 되 면 hello에 Azure 구독에서 미리 구성 하는 hello 솔루션을 삭제할 수 있습니다 [azureiotsuite.com] [ lnk-azureiotsuite] 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-334">When you are done, you can delete hello preconfigured solution from your Azure subscription on hello [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="4778d-335">이 사이트 tooeasily 삭제를 hello 미리 구성 된 솔루션을 만든 경우 프로 비전 된 리소스를 hello 모두 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-335">This site enables you tooeasily delete all hello resources that were provisioned when you created hello preconfigured solution.</span></span>

> [!NOTE]
> <span data-ttu-id="4778d-336">모든 항목을 삭제 하는 tooensure 관련 toohello 미리 구성 된 솔루션, hello에 삭제 [azureiotsuite.com] [ lnk-azureiotsuite] 사이트와 hello 포털에서 hello 리소스 그룹을 삭제 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-336">tooensure that you delete everything related toohello preconfigured solution, delete it on hello [azureiotsuite.com][lnk-azureiotsuite] site and do not delete hello resource group in hello portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4778d-337">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4778d-337">Next Steps</span></span>

<span data-ttu-id="4778d-338">미리 구성 된 솔루션을 배포한 했으므로 hello 다음 문서를 참조 하 여 IoT Suite 시작을 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4778d-338">Now that you’ve deployed a working preconfigured solution, you can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="4778d-339">[미리 구성된 원격 모니터링 솔루션 연습][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="4778d-339">[Remote monitoring preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="4778d-340">[원격 미리 구성 된 솔루션을 모니터링 하 여 장치 toohello 연결][lnk-connect-rm]</span><span class="sxs-lookup"><span data-stu-id="4778d-340">[Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm]</span></span>
* <span data-ttu-id="4778d-341">[Hello azureiotsuite.com 사이트에 대 한 권한][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="4778d-341">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>

[img-launch-solution]: media/iot-suite-getstarted-preconfigured-solutions/launch.png
[img-dashboard]: media/iot-suite-getstarted-preconfigured-solutions/dashboard.png
[img-menu]: media/iot-suite-getstarted-preconfigured-solutions/menu.png
[img-devicelist]: media/iot-suite-getstarted-preconfigured-solutions/devicelist.png
[img-alarms]: media/iot-suite-getstarted-preconfigured-solutions/alarms.png
[img-devicedetails]: media/iot-suite-getstarted-preconfigured-solutions/devicedetails.png
[img-devicecommands]: media/iot-suite-getstarted-preconfigured-solutions/devicecommands.png
[img-pingcommand]: media/iot-suite-getstarted-preconfigured-solutions/pingcommand.png
[img-adddevice]: media/iot-suite-getstarted-preconfigured-solutions/adddevice.png
[img-addnew]: media/iot-suite-getstarted-preconfigured-solutions/addnew.png
[img-definedevice]: media/iot-suite-getstarted-preconfigured-solutions/definedevice.png
[img-runningnew]: media/iot-suite-getstarted-preconfigured-solutions/runningnew.png
[img-runningnew-2]: media/iot-suite-getstarted-preconfigured-solutions/runningnew2.png
[img-rules]: media/iot-suite-getstarted-preconfigured-solutions/rules.png
[img-adddevicerule]: media/iot-suite-getstarted-preconfigured-solutions/addrule.png
[img-adddevicerule2]: media/iot-suite-getstarted-preconfigured-solutions/addrule2.png
[img-adddevicerule3]: media/iot-suite-getstarted-preconfigured-solutions/addrule3.png
[img-adddevicerule4]: media/iot-suite-getstarted-preconfigured-solutions/addrule4.png
[img-actions]: media/iot-suite-getstarted-preconfigured-solutions/actions.png
[img-portal]: media/iot-suite-getstarted-preconfigured-solutions/portal.png
[img-disable]: media/iot-suite-getstarted-preconfigured-solutions/solutionportal_08.png
[img-columneditor]: media/iot-suite-getstarted-preconfigured-solutions/columneditor.png
[img-startimageedit]: media/iot-suite-getstarted-preconfigured-solutions/imagedit1.png
[img-imageedit]: media/iot-suite-getstarted-preconfigured-solutions/imagedit2.png
[img-editfiltericon]: media/iot-suite-getstarted-preconfigured-solutions/editfiltericon.png
[img-filtereditor]: media/iot-suite-getstarted-preconfigured-solutions/filtereditor.png
[img-filterelist]: media/iot-suite-getstarted-preconfigured-solutions/filteredlist.png
[img-savefilter]: media/iot-suite-getstarted-preconfigured-solutions/savefilter.png
[img-openfilter]:  media/iot-suite-getstarted-preconfigured-solutions/openfilter.png
[img-unhealthy-filter]: media/iot-suite-getstarted-preconfigured-solutions/unhealthyfilter.png
[img-filtered-unhealthy-list]: media/iot-suite-getstarted-preconfigured-solutions/unhealthylist.png
[img-change-interval]: media/iot-suite-getstarted-preconfigured-solutions/changeinterval.png
[img-old-firmware]: media/iot-suite-getstarted-preconfigured-solutions/noticeold.png
[img-old-filter]: media/iot-suite-getstarted-preconfigured-solutions/oldfilter.png
[img-filtered-old-list]: media/iot-suite-getstarted-preconfigured-solutions/oldlist.png
[img-method-update]: media/iot-suite-getstarted-preconfigured-solutions/methodupdate.png
[img-update-1]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate1.png
[img-update-2]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate2.png
[img-update-3]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate3.png
[img-updated]: media/iot-suite-getstarted-preconfigured-solutions/updated.png
[img-healthy]: media/iot-suite-getstarted-preconfigured-solutions/healthy.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-logic-apps]: https://azure.microsoft.com/documentation/services/app-service/logic/
[lnk-portal]: http://portal.azure.com/
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-logicapptutorial]: iot-suite-logic-apps-tutorial.md
[lnk-rm-walkthrough]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-faq]: iot-suite-faq.md