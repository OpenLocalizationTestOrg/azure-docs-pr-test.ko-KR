---
title: "Visual Studio Team Services를 사용 하 여 응용 프로그램을 테스트 하는 aaaLoad | Microsoft Docs"
description: "Toostress Visual Studio Team Services를 사용 하 여 Azure 서비스 패브릭 응용 프로그램을 테스트 하는 방법에 대해 알아봅니다."
services: service-fabric
documentationcenter: na
author: cawams
manager: timlt
editor: 
ms.assetid: fc743585-0d1b-483f-981d-493f4552ac07
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: cawa
ms.openlocfilehash: 663cf8db5e8f0a4d0d7f27b585645d7f776392f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="load-test-your-application-by-using-visual-studio-team-services"></a><span data-ttu-id="ce15a-103">Visual Studio Team Services를 사용하여 응용 프로그램 부하 테스트</span><span class="sxs-lookup"><span data-stu-id="ce15a-103">Load test your application by using Visual Studio Team Services</span></span>
<span data-ttu-id="ce15a-104">이 문서에서는 Microsoft Visual Studio 부하 테스트 기능 toostress toouse 응용 프로그램을 테스트 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-104">This article shows how toouse Microsoft Visual Studio load test features toostress test an application.</span></span> <span data-ttu-id="ce15a-105">Azure 서비스 패브릭 상태 저장 서비스 백 엔드 및 상태 비저장 서비스 웹 프런트 엔드가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-105">It uses an Azure Service Fabric stateful service back end and a stateless service web front end.</span></span> <span data-ttu-id="ce15a-106">hello 여기에 예제 응용 프로그램은 비행기 위치 시뮬레이터.</span><span class="sxs-lookup"><span data-stu-id="ce15a-106">hello example application used here is an airplane location simulator.</span></span> <span data-ttu-id="ce15a-107">사용자는 항공기 ID, 출발 시간 및 도착 위치를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-107">You provide an airplane ID, departure time, and destination.</span></span> <span data-ttu-id="ce15a-108">hello 백 엔드 응용 프로그램의 처리 hello 요청 하 고 hello 프런트 엔드 hello 조건과 일치 하는 지도 hello 비행기에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-108">hello application’s back end processes hello requests, and hello front end displays on a map hello airplane that matches hello criteria.</span></span>

<span data-ttu-id="ce15a-109">hello 다음 다이어그램에서는 보여줍니다 hello 서비스 패브릭 응용 프로그램을 테스트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-109">hello following diagram illustrates hello Service Fabric application that you'll be testing.</span></span>

![Hello 예제 비행기 위치 응용 프로그램의 다이어그램][0]

## <a name="prerequisites"></a><span data-ttu-id="ce15a-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ce15a-111">Prerequisites</span></span>
<span data-ttu-id="ce15a-112">시작 하기 전에 toodo hello 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-112">Before getting started, you need toodo hello following:</span></span>

* <span data-ttu-id="ce15a-113">Visual Studio Team Services 계정을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-113">Get a Visual Studio Team Services account.</span></span> <span data-ttu-id="ce15a-114">[Visual Studio Team Services](https://www.visualstudio.com)에서 무료로 계정을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-114">You can get one for free at [Visual Studio Team Services](https://www.visualstudio.com).</span></span>
* <span data-ttu-id="ce15a-115">Visual Studio 2013 또는 Visual Studio 2015를 확보하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-115">Get and install Visual Studio 2013 or Visual Studio 2015.</span></span> <span data-ttu-id="ce15a-116">이 문서는 Visual Studio 2015 Enterprise Edition을 사용하지만 Visual Studio 2013 및 기타 버전도 유사하게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-116">This article uses Visual Studio 2015 Enterprise edition, but Visual Studio 2013 and other editions should work similarly.</span></span>
* <span data-ttu-id="ce15a-117">스테이징 환경에 응용 프로그램 tooa를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-117">Deploy your application tooa staging environment.</span></span> <span data-ttu-id="ce15a-118">참조 [toodeploy 응용 프로그램 tooa 원격 클러스터 Visual Studio를 사용 하는 방법을](service-fabric-publish-app-remote-cluster.md) 이 대 한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-118">See [How toodeploy applications tooa remote cluster using Visual Studio](service-fabric-publish-app-remote-cluster.md) for information about this.</span></span>
* <span data-ttu-id="ce15a-119">응용 프로그램 사용 패턴을 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-119">Understand your application’s usage pattern.</span></span> <span data-ttu-id="ce15a-120">이 정보는 사용 되는 toosimulate hello 부하 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-120">This information is used toosimulate hello load pattern.</span></span>
* <span data-ttu-id="ce15a-121">부하 테스트에 대 한 hello 목표를 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-121">Understand hello goal for your load testing.</span></span> <span data-ttu-id="ce15a-122">이 해석 하 고 hello 부하 테스트 결과 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-122">This helps you interpret and analyze hello load test results.</span></span>

## <a name="create-and-run-hello-web-performance-and-load-test-project"></a><span data-ttu-id="ce15a-123">만들기 및 hello 웹 성능 및 부하 테스트 프로젝트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-123">Create and run hello Web Performance and Load Test project</span></span>
### <a name="create-a-web-performance-and-load-test-project"></a><span data-ttu-id="ce15a-124">웹 성능 및 부하 테스트 만들기</span><span class="sxs-lookup"><span data-stu-id="ce15a-124">Create a Web Performance and Load Test project</span></span>
1. <span data-ttu-id="ce15a-125">Visual Studio 2015를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-125">Open Visual Studio 2015.</span></span> <span data-ttu-id="ce15a-126">선택 **파일** > **새로** > **프로젝트** hello 메뉴 모음 tooopen hello에 **새 프로젝트** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="ce15a-126">Choose **File** > **New** > **Project** on hello menu bar tooopen hello **New Project** dialog box.</span></span>
2. <span data-ttu-id="ce15a-127">Hello 확장 **Visual C#** 노드 선택 **테스트** > **웹 성능 및 부하 테스트 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-127">Expand hello **Visual C#** node and choose **Test** > **Web Performance and Load Test project**.</span></span> <span data-ttu-id="ce15a-128">Hello 프로젝트 이름을 지정 하 고 hello를 눌러 **확인** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-128">Give hello project a name and then choose hello **OK** button.</span></span>

    ![Hello 새 프로젝트 대화 상자 스크린 샷][1]

    <span data-ttu-id="ce15a-130">솔루션 탐색기에서 새로운 웹 성능 및 부하 테스트 프로젝트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-130">You should see a new Web Performance and Load Test project in Solution Explorer.</span></span>

    ![Hello 새 프로젝트를 나타내는 솔루션 탐색기의 스크린 샷][2]

### <a name="record-a-web-performance-test"></a><span data-ttu-id="ce15a-132">웹 성능 테스트 기록</span><span class="sxs-lookup"><span data-stu-id="ce15a-132">Record a web performance test</span></span>
1. <span data-ttu-id="ce15a-133">열기 hello.webtest 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-133">Open hello .webtest project.</span></span>
2. <span data-ttu-id="ce15a-134">Hello 선택 **기록 추가** 아이콘 toostart 브라우저에서 세션 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-134">Choose hello **Add Recording** icon toostart a recording session in your browser.</span></span>

    ![브라우저에서 hello 기록 추가 아이콘의 스크린 샷][3]

    ![브라우저에서 hello 레코드 단추 스크린 샷][4]
3. <span data-ttu-id="ce15a-137">Toohello 서비스 패브릭 응용 프로그램을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-137">Browse toohello Service Fabric application.</span></span> <span data-ttu-id="ce15a-138">hello 기록 패널을 hello 웹 요청을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-138">hello recording panel should show hello web requests.</span></span>

    ![패널을 기록 하는 hello에서 웹 요청의 스크린 샷][5]
4. <span data-ttu-id="ce15a-140">일련의 hello 사용자 tooperform 예상 하는 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-140">Perform a sequence of actions that you expect hello users tooperform.</span></span> <span data-ttu-id="ce15a-141">이러한 작업은 패턴 toogenerate hello 부하로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-141">These actions are used as a pattern toogenerate hello load.</span></span>
5. <span data-ttu-id="ce15a-142">완료 되 면 선택 hello **중지** 단추 toostop 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-142">When you're done, choose hello **Stop** button toostop recording.</span></span>

    ![Hello 중지 단추 스크린 샷][6]

    <span data-ttu-id="ce15a-144">Visual Studio에서 hello.webtest 프로젝트는 일련의 요청을 캡처해야 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-144">hello .webtest project in Visual Studio should have captured a series of requests.</span></span> <span data-ttu-id="ce15a-145">동적 매개 변수가 자동으로 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-145">Dynamic parameters are replaced automatically.</span></span> <span data-ttu-id="ce15a-146">이 때, 테스트 시나리오에 속하지 않는 중복된 종속 요청 또는 여분의 요청을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-146">At this point, you can delete any extra, repeated dependency requests that are not part of your test scenario.</span></span>
6. <span data-ttu-id="ce15a-147">Hello 프로젝트를 저장 하 고 hello를 눌러 **테스트 실행** 명령 toorun hello 웹 성능 테스트를 로컬로 및 모든 것이 올바르게 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-147">Save hello project and then choose hello **Run Test** command toorun hello web performance test locally and make sure everything works correctly.</span></span>

    ![테스트 실행 명령 hello 스크린 샷][7]

### <a name="parameterize-hello-web-performance-test"></a><span data-ttu-id="ce15a-149">Hello 웹 성능 테스트를 매개 변수화</span><span class="sxs-lookup"><span data-stu-id="ce15a-149">Parameterize hello web performance test</span></span>
<span data-ttu-id="ce15a-150">Tooa 코딩 된 웹 성능 테스트를 변환 하 고 다음 hello 코드를 편집 하 여 hello 웹 성능 테스트 매개 변수화 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-150">You can parameterize hello web performance test by converting it tooa coded web performance test and then editing hello code.</span></span> <span data-ttu-id="ce15a-151">대신 hello 테스트 반복 hello 데이터 있도록 hello 웹 성능 테스트 tooa 데이터 목록에 바인딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-151">As an alternative, you can bind hello web performance test tooa data list so that hello test iterates through hello data.</span></span> <span data-ttu-id="ce15a-152">참조 [생성 및 코딩 된 웹 성능 테스트를 실행](https://msdn.microsoft.com/library/ms182552.aspx) tooconvert hello 웹 성능 테스트 tooa 테스트를 코딩 하는 방법에 대 한 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-152">See [Generate and run a coded web performance test](https://msdn.microsoft.com/library/ms182552.aspx) for details about how tooconvert hello web performance test tooa coded test.</span></span> <span data-ttu-id="ce15a-153">참조 [데이터 소스 tooa 웹 성능 테스트 추가](https://msdn.microsoft.com/library/ms243142.aspx) toobind 데이터 tooa 웹 성능 방법에 대 한 정보에 대 한 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-153">See [Add a data source tooa web performance test](https://msdn.microsoft.com/library/ms243142.aspx) for information about how toobind data tooa web performance test.</span></span>

<span data-ttu-id="ce15a-154">예를 들어 hello 비행기 ID 생성 된 GUID로 바꿉니다 하 고 더 많은 요청 toosend 내리지 않는 항공편 toodifferent 위치를 추가할 수 있도록 hello 웹 성능 테스트 tooa 코딩 된 테스트를 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-154">For this example, we'll convert hello web performance test tooa coded test so you can replace hello airplane ID with a generated GUID and add more requests toosend flights toodifferent locations.</span></span>

### <a name="create-a-load-test-project"></a><span data-ttu-id="ce15a-155">부하 테스트 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="ce15a-155">Create a load test project</span></span>
<span data-ttu-id="ce15a-156">부하 테스트 프로젝트는 hello 웹 성능 테스트 및 단위 테스트를 추가로 지정 된 부하 테스트 설정에서 설명 하는 하나 이상의 시나리오가 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-156">A load test project is composed of one or more scenarios described by hello web performance test and unit test, along with additional specified load test settings.</span></span> <span data-ttu-id="ce15a-157">단계를 수행 하는 hello toocreate 부하 프로젝트를 테스트 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-157">hello following steps show how toocreate a load test project:</span></span>

1. <span data-ttu-id="ce15a-158">Hello 웹 성능 및 부하 테스트 프로젝트의 바로 가기 메뉴에서 선택 **추가** > **부하 테스트**합니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-158">On hello shortcut menu of your Web Performance and Load Test project, choose **Add** > **Load Test**.</span></span> <span data-ttu-id="ce15a-159">Hello에 **부하 테스트** 마법사 hello 선택 **다음** tooconfigure hello 테스트 설정 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-159">In hello **Load Test** wizard, choose hello **Next** button tooconfigure hello test settings.</span></span>
2. <span data-ttu-id="ce15a-160">Hello에 **부하 패턴** 섹션에서 원하는 상수 사용자 부하 또는 적은 수의 사용자로 시작 하는 단계 부하 및 증가 시간에 따라 사용자가 hello 여부를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-160">In hello **Load Pattern** section, choose whether you want a constant user load or a step load, which starts with a few users and increases hello users over time.</span></span>

    <span data-ttu-id="ce15a-161">좋은 예측 하는 사용자 부하의 양은 hello toosee hello 현재 시스템 수행 하는 방법을 사용할 경우 수도 **상수 로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-161">If you have a good estimate of hello amount of user load and want toosee how hello current system performs, choose **Constant Load**.</span></span> <span data-ttu-id="ce15a-162">여기서의 목표 toolearn hello 시스템 다양 한 로드 상태에서 일관성 있게 수행 하는지 여부를 선택 **단계 부하**합니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-162">If your goal is toolearn whether hello system performs consistently under various loads, choose **Step Load**.</span></span>
3. <span data-ttu-id="ce15a-163">Hello에 **테스트 조합** 섹션에서 hello **추가** tooinclude hello 부하 테스트에 원하는 단추를 선택한 후 hello 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-163">In hello **Test Mix** section, choose hello **Add** button and then select hello test that you want tooinclude in hello load test.</span></span> <span data-ttu-id="ce15a-164">Hello를 사용할 수 있습니다 **배포** 각 테스트에 대해 실행 되는 총 테스트 백분율로 toospecify hello 열입니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-164">You can use hello **Distribution** column toospecify hello percentage of total tests run for each test.</span></span>
4. <span data-ttu-id="ce15a-165">Hello에 **실행 설정** 섹션 hello 부하 테스트 지속 시간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-165">In hello **Run Settings** section, specify hello load test duration.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ce15a-166">hello **테스트 반복** 옵션은 Visual Studio를 사용 하 여 로컬로 부하 테스트를 실행할 때에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-166">hello **Test Iterations** option is available only when you run a load test locally using Visual Studio.</span></span>
   >
   >
5. <span data-ttu-id="ce15a-167">Hello에 **위치** 섹션 **실행 설정**, 부하 테스트 요청이 생성 되는 hello 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-167">In hello **Location** section of **Run Settings**, specify hello location where load test requests are generated.</span></span> <span data-ttu-id="ce15a-168">hello 마법사 tooyour Team Services 계정에에서 toolog을 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-168">hello wizard may prompt you toolog in tooyour Team Services account.</span></span> <span data-ttu-id="ce15a-169">로그인한 다음 지리적 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-169">Log in and then choose a geographic location.</span></span> <span data-ttu-id="ce15a-170">완료 되 면 선택 hello **마침** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-170">When you're done, choose hello **Finish** button.</span></span>
6. <span data-ttu-id="ce15a-171">Hello 부하 테스트를 만든 후 hello.loadtest 프로젝트를 열고 hello 같은 현재 실행 설정 선택 **실행 설정** > **설정 1 실행 [Active]**합니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-171">After hello load test is created, open hello .loadtest project and choose hello current run setting, such as **Run Settings** > **Run Settings1 [Active]**.</span></span> <span data-ttu-id="ce15a-172">Hello에서 실행 하는 hello 설정을 열립니다 **속성** 창.</span><span class="sxs-lookup"><span data-stu-id="ce15a-172">This opens hello run settings in hello **Properties** window.</span></span>
7. <span data-ttu-id="ce15a-173">Hello에 **결과** hello 섹션 **실행 설정** 속성 창, hello **타이밍 정보 저장소** 설정이 있어야 **None** 으로 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-173">In hello **Results** section of hello **Run Settings** properties window, hello **Timing Details Storage** setting should have **None** as its default value.</span></span> <span data-ttu-id="ce15a-174">이 값도 변경**모든 개인 정보** tooget hello 부하 테스트 결과에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-174">Change this value too**All Individual Details** tooget more information on hello load test results.</span></span> <span data-ttu-id="ce15a-175">참조 [부하 테스트](https://www.visualstudio.com/load-testing.aspx) tooconnect tooVisual Studio Team Services 및 실행 부하를 테스트 하는 방법에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-175">See [Load Testing](https://www.visualstudio.com/load-testing.aspx) for more information on how tooconnect tooVisual Studio Team Services and run a load test.</span></span>

### <a name="run-hello-load-test-by-using-visual-studio-team-services"></a><span data-ttu-id="ce15a-176">Visual Studio Team Services를 사용 하 여 hello 부하 테스트 실행</span><span class="sxs-lookup"><span data-stu-id="ce15a-176">Run hello load test by using Visual Studio Team Services</span></span>
<span data-ttu-id="ce15a-177">Hello 선택 **부하 테스트 실행** 명령 toostart hello 테스트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-177">Choose hello **Run Load Test** command toostart hello test run.</span></span>

![부하 테스트 실행 명령 hello 스크린 샷][8]

## <a name="view-and-analyze-hello-load-test-results"></a><span data-ttu-id="ce15a-179">Hello 부하 테스트 결과 확인 및 분석</span><span class="sxs-lookup"><span data-stu-id="ce15a-179">View and analyze hello load test results</span></span>
<span data-ttu-id="ce15a-180">부하 테스트 진행 됨에 따라 hello로, hello 성능 정보를 그래프로 표현 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-180">As hello load test progresses, hello performance information is graphed.</span></span> <span data-ttu-id="ce15a-181">다음 그래프는 다음과 유사한 toohello를 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-181">You should see something similar toohello following graph.</span></span>

![부하 테스트 결과에 대한 성능 그래프의 스크린샷][9]

1. <span data-ttu-id="ce15a-183">Hello 선택 **보고서 다운로드** hello 페이지의 hello 위쪽에 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-183">Choose hello **Download report** link near hello top of hello page.</span></span> <span data-ttu-id="ce15a-184">Hello 보고서를 다운로드 한 후 선택 hello **보고서를 볼** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-184">After hello report is downloaded, choose hello **View report** button.</span></span>

    <span data-ttu-id="ce15a-185">Hello에 **그래프** 탭 다양 한 성능 카운터에 대 한 그래프를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-185">On hello **Graph** tab you can see graphs for various performance counters.</span></span> <span data-ttu-id="ce15a-186">Hello에 **요약** 탭 hello 전체 테스트 결과가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-186">On hello **Summary** tab, hello overall test results appear.</span></span> <span data-ttu-id="ce15a-187">hello **테이블** 탭 hello 성공한 요청과 실패 한 부하 테스트의 총 수를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-187">hello **Tables** tab shows hello total number of passed and failed load tests.</span></span>
2. <span data-ttu-id="ce15a-188">Hello에 대 한 hello 숫자 링크 선택 **테스트** > **실패** 및 hello **오류** > **Count** 열 toosee 오류 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-188">Choose hello number links on hello **Test** > **Failed** and hello **Errors** > **Count** columns toosee error details.</span></span>

    <span data-ttu-id="ce15a-189">hello **세부** 탭 실패 한 요청에 대 한 가상 사용자 및 테스트 시나리오 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-189">hello **Detail** tab shows virtual user and test scenario information for failed requests.</span></span> <span data-ttu-id="ce15a-190">이 데이터는 hello 부하 테스트에 여러 시나리오에 포함 된 경우에 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-190">This data can be useful if hello load test includes multiple scenarios.</span></span>

<span data-ttu-id="ce15a-191">참조 [부하 테스트 결과 분석 hello hello 부하 테스트 분석기의 그래프 보기에서에서](https://www.visualstudio.com/load-testing.aspx) 부하 보기에 대 한 자세한 내용은 테스트 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-191">See [Analyzing Load Test Results in hello Graphs View of hello Load Test Analyzer](https://www.visualstudio.com/load-testing.aspx) for more information on viewing load test results.</span></span>

## <a name="automate-your-load-test"></a><span data-ttu-id="ce15a-192">부하 테스트 자동화</span><span class="sxs-lookup"><span data-stu-id="ce15a-192">Automate your load test</span></span>
<span data-ttu-id="ce15a-193">Visual Studio Team Services 부하 테스트 Api toohelp 부하 테스트를 관리 하는 Team Services 계정에는 결과 분석을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce15a-193">Visual Studio Team Services Load Test provides APIs toohelp you manage load tests and analyze results in a Team Services account.</span></span> <span data-ttu-id="ce15a-194">자세한 내용은 [클라우드 부하 테스트 REST API(영문)](http://blogs.msdn.com/b/visualstudioalm/archive/2014/11/03/cloud-load-testing-rest-apis-are-here.aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ce15a-194">See [Cloud Load Testing Rest APIs](http://blogs.msdn.com/b/visualstudioalm/archive/2014/11/03/cloud-load-testing-rest-apis-are-here.aspx) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce15a-195">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ce15a-195">Next steps</span></span>
* [<span data-ttu-id="ce15a-196">로컬 컴퓨터 개발 설정에서의 모니터링 및 진단 서비스</span><span class="sxs-lookup"><span data-stu-id="ce15a-196">Monitoring and diagnosing services in a local machine development setup</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[0]: ./media/service-fabric-vso-load-test/OverviewDiagram.png
[1]: ./media/service-fabric-vso-load-test/NewProjectDialog.png
[2]: ./media/service-fabric-vso-load-test/Project.png
[3]: ./media/service-fabric-vso-load-test/AddRecording.png
[4]: ./media/service-fabric-vso-load-test/AddRecording2.png
[5]: ./media/service-fabric-vso-load-test/ActionSequence.png
[6]: ./media/service-fabric-vso-load-test/StopRecording.png
[7]: ./media/service-fabric-vso-load-test/RunTest.png
[8]: ./media/service-fabric-vso-load-test/RunTest2.png
[9]: ./media/service-fabric-vso-load-test/Graph.png
