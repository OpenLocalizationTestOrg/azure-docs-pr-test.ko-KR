---
title: "Visual Studio Team Services를 사용하여 응용 프로그램 부하 테스트 | Microsoft Docs"
description: "Visual Studio Team Services를 사용하여 Azure 서비스 패브릭 응용 프로그램에 스트레스 테스트를 실행하는 방법을 알아봅니다."
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
ms.openlocfilehash: e8e270ce865d4da3ee219958b308db2c1c89b11b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="load-test-your-application-by-using-visual-studio-team-services"></a><span data-ttu-id="9f21b-103">Visual Studio Team Services를 사용하여 응용 프로그램 부하 테스트</span><span class="sxs-lookup"><span data-stu-id="9f21b-103">Load test your application by using Visual Studio Team Services</span></span>
<span data-ttu-id="9f21b-104">이 문서는 Microsoft Visual Studio 부하 테스트 기능을 사용하여 응용 프로그램에 스트레스 테스트를 실행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-104">This article shows how to use Microsoft Visual Studio load test features to stress test an application.</span></span> <span data-ttu-id="9f21b-105">Azure 서비스 패브릭 상태 저장 서비스 백 엔드 및 상태 비저장 서비스 웹 프런트 엔드가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-105">It uses an Azure Service Fabric stateful service back end and a stateless service web front end.</span></span> <span data-ttu-id="9f21b-106">여기에 사용되는 예제 응용 프로그램은 항공기 위치 시뮬레이터입니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-106">The example application used here is an airplane location simulator.</span></span> <span data-ttu-id="9f21b-107">사용자는 항공기 ID, 출발 시간 및 도착 위치를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-107">You provide an airplane ID, departure time, and destination.</span></span> <span data-ttu-id="9f21b-108">응용 프로그램의 백 엔드는 요청을 처리하고 프런트 엔드는 지도에 조건에 일치하는 항공기를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-108">The application’s back end processes the requests, and the front end displays on a map the airplane that matches the criteria.</span></span>

<span data-ttu-id="9f21b-109">다음 다이어그램은 테스트를 수행할 서비스 패브릭 응용 프로그램을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-109">The following diagram illustrates the Service Fabric application that you'll be testing.</span></span>

![예제 비행기 위치 응용 프로그램의 다이어그램][0]

## <a name="prerequisites"></a><span data-ttu-id="9f21b-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9f21b-111">Prerequisites</span></span>
<span data-ttu-id="9f21b-112">시작하기 전에 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-112">Before getting started, you need to do the following:</span></span>

* <span data-ttu-id="9f21b-113">Visual Studio Team Services 계정을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-113">Get a Visual Studio Team Services account.</span></span> <span data-ttu-id="9f21b-114">[Visual Studio Team Services](https://www.visualstudio.com)에서 무료로 계정을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-114">You can get one for free at [Visual Studio Team Services](https://www.visualstudio.com).</span></span>
* <span data-ttu-id="9f21b-115">Visual Studio 2013 또는 Visual Studio 2015를 확보하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-115">Get and install Visual Studio 2013 or Visual Studio 2015.</span></span> <span data-ttu-id="9f21b-116">이 문서는 Visual Studio 2015 Enterprise Edition을 사용하지만 Visual Studio 2013 및 기타 버전도 유사하게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-116">This article uses Visual Studio 2015 Enterprise edition, but Visual Studio 2013 and other editions should work similarly.</span></span>
* <span data-ttu-id="9f21b-117">스테이징 환경에 응용 프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-117">Deploy your application to a staging environment.</span></span> <span data-ttu-id="9f21b-118">자세한 내용은 [Visual Studio를 사용하여 원격 클러스터에 응용 프로그램을 배포하는 방법(영문)](service-fabric-publish-app-remote-cluster.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f21b-118">See [How to deploy applications to a remote cluster using Visual Studio](service-fabric-publish-app-remote-cluster.md) for information about this.</span></span>
* <span data-ttu-id="9f21b-119">응용 프로그램 사용 패턴을 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-119">Understand your application’s usage pattern.</span></span> <span data-ttu-id="9f21b-120">이 정보는 부하 패턴을 시뮬레이션하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-120">This information is used to simulate the load pattern.</span></span>
* <span data-ttu-id="9f21b-121">부하 테스트의 목표를 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-121">Understand the goal for your load testing.</span></span> <span data-ttu-id="9f21b-122">이것은 부하 테스트 결과를 해석하고 분석하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-122">This helps you interpret and analyze the load test results.</span></span>

## <a name="create-and-run-the-web-performance-and-load-test-project"></a><span data-ttu-id="9f21b-123">웹 성능 및 부하 테스트 프로젝트 만들기 및 실행</span><span class="sxs-lookup"><span data-stu-id="9f21b-123">Create and run the Web Performance and Load Test project</span></span>
### <a name="create-a-web-performance-and-load-test-project"></a><span data-ttu-id="9f21b-124">웹 성능 및 부하 테스트 만들기</span><span class="sxs-lookup"><span data-stu-id="9f21b-124">Create a Web Performance and Load Test project</span></span>
1. <span data-ttu-id="9f21b-125">Visual Studio 2015를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-125">Open Visual Studio 2015.</span></span> <span data-ttu-id="9f21b-126">메뉴 모음에서 **파일** > **새로 만들기** > **프로젝트**를 선택하여 **새 프로젝트** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-126">Choose **File** > **New** > **Project** on the menu bar to open the **New Project** dialog box.</span></span>
2. <span data-ttu-id="9f21b-127">**Visual C#** 노드를 확장하고 **테스트** > **웹 성능 및 부하 테스트 프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-127">Expand the **Visual C#** node and choose **Test** > **Web Performance and Load Test project**.</span></span> <span data-ttu-id="9f21b-128">프로젝트 이름을 부여하고 **확인** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-128">Give the project a name and then choose the **OK** button.</span></span>

    ![새 프로젝트 대화 상자의 스크린샷][1]

    <span data-ttu-id="9f21b-130">솔루션 탐색기에서 새로운 웹 성능 및 부하 테스트 프로젝트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-130">You should see a new Web Performance and Load Test project in Solution Explorer.</span></span>

    ![새 프로젝트를 보여 주는 솔루션 탐색기의 스크린샷][2]

### <a name="record-a-web-performance-test"></a><span data-ttu-id="9f21b-132">웹 성능 테스트 기록</span><span class="sxs-lookup"><span data-stu-id="9f21b-132">Record a web performance test</span></span>
1. <span data-ttu-id="9f21b-133">.webtest 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-133">Open the .webtest project.</span></span>
2. <span data-ttu-id="9f21b-134">**기록 추가** 아이콘을 선택하여 사용자 브라우저에서 기록 세션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-134">Choose the **Add Recording** icon to start a recording session in your browser.</span></span>

    ![브라우저에서 기록 추가 아이콘의 스크린샷][3]

    ![브라우저에서 기록 단추의 스크린샷][4]
3. <span data-ttu-id="9f21b-137">서비스 패브릭 응용 프로그램으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-137">Browse to the Service Fabric application.</span></span> <span data-ttu-id="9f21b-138">기록 패널에 웹 요청이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-138">The recording panel should show the web requests.</span></span>

    ![기록 패널에서 웹 요청의 스크린샷][5]
4. <span data-ttu-id="9f21b-140">사용자가 수행할 것으로 예상하는 작업 시퀀스를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-140">Perform a sequence of actions that you expect the users to perform.</span></span> <span data-ttu-id="9f21b-141">이 작업은 부하를 생성하는 패턴으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-141">These actions are used as a pattern to generate the load.</span></span>
5. <span data-ttu-id="9f21b-142">완료되면 **중지** 단추를 선택하여 기록을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-142">When you're done, choose the **Stop** button to stop recording.</span></span>

    ![중지 단추의 스크린샷][6]

    <span data-ttu-id="9f21b-144">Visual Studio의 .webtest 프로젝트가 일련의 요청으로 캡처되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-144">The .webtest project in Visual Studio should have captured a series of requests.</span></span> <span data-ttu-id="9f21b-145">동적 매개 변수가 자동으로 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-145">Dynamic parameters are replaced automatically.</span></span> <span data-ttu-id="9f21b-146">이 때, 테스트 시나리오에 속하지 않는 중복된 종속 요청 또는 여분의 요청을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-146">At this point, you can delete any extra, repeated dependency requests that are not part of your test scenario.</span></span>
6. <span data-ttu-id="9f21b-147">프로젝트를 저장한 후 **테스트 실행** 명령을 선택하여 로컬에서 웹 성능 테스트를 실행하고 모든 것이 올바르게 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-147">Save the project and then choose the **Run Test** command to run the web performance test locally and make sure everything works correctly.</span></span>

    ![테스트 실행 명령의 스크린샷][7]

### <a name="parameterize-the-web-performance-test"></a><span data-ttu-id="9f21b-149">웹 성능 테스트 매개 변수화</span><span class="sxs-lookup"><span data-stu-id="9f21b-149">Parameterize the web performance test</span></span>
<span data-ttu-id="9f21b-150">웹 성능 테스트를 코딩된 웹 성능 테스트로 변환한 후 코드를 편집하여 웹 성능 테스트를 매개 변수화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-150">You can parameterize the web performance test by converting it to a coded web performance test and then editing the code.</span></span> <span data-ttu-id="9f21b-151">또는 테스트가 데이터를 통해 반복되도록 웹 성능 테스트를 데이터 목록에 바인딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-151">As an alternative, you can bind the web performance test to a data list so that the test iterates through the data.</span></span> <span data-ttu-id="9f21b-152">웹 성능 테스트를 코딩된 테스트로 변환하는 방법에 대한 자세한 내용은 [코딩된 웹 성능 테스트 생성 및 실행](https://msdn.microsoft.com/library/ms182552.aspx) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f21b-152">See [Generate and run a coded web performance test](https://msdn.microsoft.com/library/ms182552.aspx) for details about how to convert the web performance test to a coded test.</span></span> <span data-ttu-id="9f21b-153">웹 성능 테스트에 데이터를 바인딩하는 방법에 대한 정보는 [웹 성능 테스트에 데이터 소스 추가](https://msdn.microsoft.com/library/ms243142.aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f21b-153">See [Add a data source to a web performance test](https://msdn.microsoft.com/library/ms243142.aspx) for information about how to bind data to a web performance test.</span></span>

<span data-ttu-id="9f21b-154">이 예제에서는 항공기 ID를 생성된 GUID로 대체하고 여러 지역에 항공편을 보내는 요청을 추가할 수 있도록 웹 성능 테스트를 코딩된 테스트로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-154">For this example, we'll convert the web performance test to a coded test so you can replace the airplane ID with a generated GUID and add more requests to send flights to different locations.</span></span>

### <a name="create-a-load-test-project"></a><span data-ttu-id="9f21b-155">부하 테스트 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="9f21b-155">Create a load test project</span></span>
<span data-ttu-id="9f21b-156">부하 테스트 프로젝트는 추가적으로 지정되는 부하 테스트 설정과 함께 웹 성능 테스트 및 단위 테스트로 설명되는 하나 이상의 시나리오로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-156">A load test project is composed of one or more scenarios described by the web performance test and unit test, along with additional specified load test settings.</span></span> <span data-ttu-id="9f21b-157">다음 단계는 부하 테스트 프로젝트를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-157">The following steps show how to create a load test project:</span></span>

1. <span data-ttu-id="9f21b-158">웹 성능 및 부하 테스트 프로젝트의 바로 가기 메뉴에서 **추가** > **부하 테스트**에서 무료로 계정을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-158">On the shortcut menu of your Web Performance and Load Test project, choose **Add** > **Load Test**.</span></span> <span data-ttu-id="9f21b-159">**부하 테스트** 마법사에서 **다음** 단추를 선택하여 테스트 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-159">In the **Load Test** wizard, choose the **Next** button to configure the test settings.</span></span>
2. <span data-ttu-id="9f21b-160">**부하 패턴** 섹션에서 일정 사용자 부하를 원하는지 사용자 몇 명으로 시작하여 시간이 지나면서 사용자를 늘리는 단계 부하를 원하는지 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-160">In the **Load Pattern** section, choose whether you want a constant user load or a step load, which starts with a few users and increases the users over time.</span></span>

    <span data-ttu-id="9f21b-161">사용자 부하에 대한 예측이 믿을만하고 현재 시스템의 성능을 보려면 **일정 부하**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-161">If you have a good estimate of the amount of user load and want to see how the current system performs, choose **Constant Load**.</span></span> <span data-ttu-id="9f21b-162">테스트의 목표가 다양한 부하에 대해 시스템 성능이 일관적으로 수행되는지를 파악하는 것이라면 **단계 부하**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-162">If your goal is to learn whether the system performs consistently under various loads, choose **Step Load**.</span></span>
3. <span data-ttu-id="9f21b-163">**테스트 조합** 섹션에서 **추가** 단추를 선택한 후 부하 테스트에 포함할 테스트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-163">In the **Test Mix** section, choose the **Add** button and then select the test that you want to include in the load test.</span></span> <span data-ttu-id="9f21b-164">**분포** 열을 사용하여 각 테스트에 실행할 총 테스트의 백분율을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-164">You can use the **Distribution** column to specify the percentage of total tests run for each test.</span></span>
4. <span data-ttu-id="9f21b-165">**실행 설정** 섹션에서 부하 테스트 지속 시간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-165">In the **Run Settings** section, specify the load test duration.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9f21b-166">**테스트 반복** 옵션은 Visual Studio를 사용하여 로컬에서 부하 테스트를 실행하는 경우에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-166">The **Test Iterations** option is available only when you run a load test locally using Visual Studio.</span></span>
   >
   >
5. <span data-ttu-id="9f21b-167">**실행 설정**의 **위치** 섹션에서 부하 테스트 요청이 생성되는 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-167">In the **Location** section of **Run Settings**, specify the location where load test requests are generated.</span></span> <span data-ttu-id="9f21b-168">마법사가 Team Services 계정에 로그인하라는 메시지를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-168">The wizard may prompt you to log in to your Team Services account.</span></span> <span data-ttu-id="9f21b-169">로그인한 다음 지리적 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-169">Log in and then choose a geographic location.</span></span> <span data-ttu-id="9f21b-170">완료되면 **마침** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-170">When you're done, choose the **Finish** button.</span></span>
6. <span data-ttu-id="9f21b-171">부하 테스트를 만든 후에 에서 무료로 계정을 등록할 수 있습니다.loadtest 프로젝트를 열어서 현재 실행 설정을 선택합니다(예: **실행 설정** > **실행 설정1 [Active]**에서 무료로 계정을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-171">After the load test is created, open the .loadtest project and choose the current run setting, such as **Run Settings** > **Run Settings1 [Active]**.</span></span> <span data-ttu-id="9f21b-172">그러면 **속성** 창에 실행 설정이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-172">This opens the run settings in the **Properties** window.</span></span>
7. <span data-ttu-id="9f21b-173">**실행 설정** 속성 창의 **결과** 섹션에, **타이밍 정보 저장소** 설정의 기본 값이 **없음**으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-173">In the **Results** section of the **Run Settings** properties window, the **Timing Details Storage** setting should have **None** as its default value.</span></span> <span data-ttu-id="9f21b-174">부하 테스트 결과에 대해 자세한 정보를 보려면 이 값을 **모든 개인 정보** 로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-174">Change this value to **All Individual Details** to get more information on the load test results.</span></span> <span data-ttu-id="9f21b-175">Visual Studio Team Services에 연결하여 부하 테스트를 실행하는 방법을 자세히 보려면 [부하 테스트](https://www.visualstudio.com/load-testing.aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f21b-175">See [Load Testing](https://www.visualstudio.com/load-testing.aspx) for more information on how to connect to Visual Studio Team Services and run a load test.</span></span>

### <a name="run-the-load-test-by-using-visual-studio-team-services"></a><span data-ttu-id="9f21b-176">Visual Studio Team Services를 사용하여 부하 테스트 실행</span><span class="sxs-lookup"><span data-stu-id="9f21b-176">Run the load test by using Visual Studio Team Services</span></span>
<span data-ttu-id="9f21b-177">**부하 테스트 실행** 명령을 선택하여 테스트 실행을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-177">Choose the **Run Load Test** command to start the test run.</span></span>

![부하 테스트 실행 명령의 스크린샷][8]

## <a name="view-and-analyze-the-load-test-results"></a><span data-ttu-id="9f21b-179">부하 테스트 보기 및 분석</span><span class="sxs-lookup"><span data-stu-id="9f21b-179">View and analyze the load test results</span></span>
<span data-ttu-id="9f21b-180">부하 테스트가 진행됨에 따라서 성능 정보가 그래프로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-180">As the load test progresses, the performance information is graphed.</span></span> <span data-ttu-id="9f21b-181">다음과 유사한 그래프가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-181">You should see something similar to the following graph.</span></span>

![부하 테스트 결과에 대한 성능 그래프의 스크린샷][9]

1. <span data-ttu-id="9f21b-183">페이지 맨 위 근처에서 **보고서 다운로드** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-183">Choose the **Download report** link near the top of the page.</span></span> <span data-ttu-id="9f21b-184">보고서를 다운로드한 후에 **보고서 보기** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-184">After the report is downloaded, choose the **View report** button.</span></span>

    <span data-ttu-id="9f21b-185">**그래프** 탭에 다양한 성능 카운터의 그래프가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-185">On the **Graph** tab you can see graphs for various performance counters.</span></span> <span data-ttu-id="9f21b-186">**요약** 탭에 전반적인 테스트 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-186">On the **Summary** tab, the overall test results appear.</span></span> <span data-ttu-id="9f21b-187">**테이블** 탭은 성공한 테스트와 실패한 테스트의 총 수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-187">The **Tables** tab shows the total number of passed and failed load tests.</span></span>
2. <span data-ttu-id="9f21b-188">**테스트** > **실패** 및 **오류** > **개수** 열에서 숫자 링크를 선택하여 오류 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-188">Choose the number links on the **Test** > **Failed** and the **Errors** > **Count** columns to see error details.</span></span>

    <span data-ttu-id="9f21b-189">**세부 정보** 탭에 실패한 요청의 가상 사용자 및 테스트 시나리오 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-189">The **Detail** tab shows virtual user and test scenario information for failed requests.</span></span> <span data-ttu-id="9f21b-190">이 데이터는 가상 테스트에 여러 시나리오가 포함된 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-190">This data can be useful if the load test includes multiple scenarios.</span></span>

<span data-ttu-id="9f21b-191">부하 테스트 결과를 보는 방법에 대한 자세한 내용은 [부하 테스트 분석기의 그래프 보기에서 부하 테스트 결과 분석(영문)](https://www.visualstudio.com/load-testing.aspx) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f21b-191">See [Analyzing Load Test Results in the Graphs View of the Load Test Analyzer](https://www.visualstudio.com/load-testing.aspx) for more information on viewing load test results.</span></span>

## <a name="automate-your-load-test"></a><span data-ttu-id="9f21b-192">부하 테스트 자동화</span><span class="sxs-lookup"><span data-stu-id="9f21b-192">Automate your load test</span></span>
<span data-ttu-id="9f21b-193">Visual Studio Team Services 부하 테스트에는 Team Services 계정으로 부하 테스트를 관리하고 결과를 분석할 수 있도록 하는 API가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f21b-193">Visual Studio Team Services Load Test provides APIs to help you manage load tests and analyze results in a Team Services account.</span></span> <span data-ttu-id="9f21b-194">자세한 내용은 [클라우드 부하 테스트 REST API(영문)](http://blogs.msdn.com/b/visualstudioalm/archive/2014/11/03/cloud-load-testing-rest-apis-are-here.aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f21b-194">See [Cloud Load Testing Rest APIs](http://blogs.msdn.com/b/visualstudioalm/archive/2014/11/03/cloud-load-testing-rest-apis-are-here.aspx) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9f21b-195">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9f21b-195">Next steps</span></span>
* [<span data-ttu-id="9f21b-196">로컬 컴퓨터 개발 설정에서의 모니터링 및 진단 서비스</span><span class="sxs-lookup"><span data-stu-id="9f21b-196">Monitoring and diagnosing services in a local machine development setup</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

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
