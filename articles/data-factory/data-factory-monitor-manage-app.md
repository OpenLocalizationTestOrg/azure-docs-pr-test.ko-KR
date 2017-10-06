---
title: "aaaMonitor 및 데이터 파이프라인-Azure 관리 | Microsoft Docs"
description: "Toouse 모니터링 및 관리 앱 toomonitor hello 하 고 Azure 데이터 팩터리 및 파이프라인을 관리 하는 방법에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: f3f07bc4-6dc3-4d4d-ac22-0be62189d578
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: spelluru
ms.openlocfilehash: 5e4ef6ec5fb8ebc9bda0be7899a39a51d58403d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-monitoring-and-management-app"></a><span data-ttu-id="7784f-103">모니터링 하 고 hello 모니터링 및 관리 응용 프로그램을 사용 하 여 Azure 데이터 팩터리 파이프라인 관리</span><span class="sxs-lookup"><span data-stu-id="7784f-103">Monitor and manage Azure Data Factory pipelines by using hello Monitoring and Management app</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7784f-104">Azure 포털/Azure PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="7784f-104">Using Azure portal/Azure PowerShell</span></span>](data-factory-monitor-manage-pipelines.md)
> * [<span data-ttu-id="7784f-105">모니터링 및 관리 앱 사용</span><span class="sxs-lookup"><span data-stu-id="7784f-105">Using Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)
>
>

<span data-ttu-id="7784f-106">이 문서에서는 toouse를 모니터링 및 관리 앱 toomonitor hello, 관리 및 데이터 팩터리 파이프라인을 디버깅 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-106">This article describes how toouse hello Monitoring and Management app toomonitor, manage, and debug your Data Factory pipelines.</span></span> <span data-ttu-id="7784f-107">또한 toocreate tooget 오류에 대 한 알림 경고 하는 방법에 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-107">It also provides information on how toocreate alerts tooget notified on failures.</span></span> <span data-ttu-id="7784f-108">있습니다 수 시작 hello 응용 프로그램을 사용 하 여 다음 시청 hello 하 여 비디오:</span><span class="sxs-lookup"><span data-stu-id="7784f-108">You can get started with using hello application by watching hello following video:</span></span>

> [!NOTE]
> <span data-ttu-id="7784f-109">hello 사용자 인터페이스에에서 표시 된 것 hello 비디오 다 hello 포털에 표시 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-109">hello user interface shown in hello video may not exactly match what you see in hello portal.</span></span> <span data-ttu-id="7784f-110">하지만 약간 오래 된 개념 유지 hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-110">It's slightly older, but concepts remain hello same.</span></span> 

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-Data-Factory-Monitoring-and-Managing-Big-Data-Piplines/player]
>

## <a name="launch-hello-monitoring-and-management-app"></a><span data-ttu-id="7784f-111">Hello 모니터링 및 관리 앱 시작</span><span class="sxs-lookup"><span data-stu-id="7784f-111">Launch hello Monitoring and Management app</span></span>
<span data-ttu-id="7784f-112">toolaunch hello 모니터 및 관리 응용 프로그램 클릭 hello **모니터링 및 관리** hello 타일 **Data Factory** 블레이드 데이터 팩토리에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-112">toolaunch hello Monitor and Management app, click hello **Monitor & Manage** tile on hello **Data Factory** blade for your data factory.</span></span>

![타일을 hello Data Factory 홈 페이지에서 모니터링](./media/data-factory-monitor-manage-app/MonitoringAppTile.png)

<span data-ttu-id="7784f-114">별도 창에서 열고 hello 모니터링 및 관리 앱이 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-114">You should see hello Monitoring and Management app open in a separate window.</span></span>  

![모니터링 및 관리 앱](./media/data-factory-monitor-manage-app/AppLaunched.png)

> [!NOTE]
> <span data-ttu-id="7784f-116">해당 hello 웹 브라우저에서 "권한 부여..." 걸려 표시 되 면 hello의 선택을 취소 **타사 쿠키를 차단 하 고 사이트 데이터** 확인란-또는 선택한 상태가 유지에 대 한 예외를 만들려면 **login.microsoftonline.com** 후 tooopen hello 응용 프로그램을 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="7784f-116">If you see that hello web browser is stuck at "Authorizing...", clear hello **Block third-party cookies and site data** check box--or keep it selected, create an exception for **login.microsoftonline.com**, and then try tooopen hello app again.</span></span>


<span data-ttu-id="7784f-117">목록의 hello 활동 Windows hello 가운데 창에서 각 활동 실행에 대해 작업 창이 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-117">In hello Activity Windows list in hello middle pane, you see an activity window for each run of an activity.</span></span> <span data-ttu-id="7784f-118">예를 들어 5 시간에 대 한 예약 된 활동 toorun hello에 1 시간 마다 있는 5 개의 데이터 조각와 연결 된 5 개 활동 창 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-118">For example, if you have hello activity scheduled toorun hourly for five hours, you see five activity windows associated with five data slices.</span></span> <span data-ttu-id="7784f-119">활동 창 hello 맨 아래에 hello 목록에 보이지 않으면 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-119">If you don't see activity windows in hello list at hello bottom, do hello following:</span></span>
 
- <span data-ttu-id="7784f-120">업데이트 hello **시작 시간** 및 **종료 시간** hello 상위 toomatch hello에 대 한 필터 시작 및 종료 후 파이프라인의 시간을 누른 다음 hello **적용** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-120">Update hello **start time** and **end time** filters at hello top toomatch hello start and end times of your pipeline, and then click hello **Apply** button.</span></span>  
- <span data-ttu-id="7784f-121">hello 활동 창 목록은 자동으로 고쳐지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-121">hello Activity Windows list is not automatically refreshed.</span></span> <span data-ttu-id="7784f-122">Hello 클릭 **새로 고침** hello에 hello 도구 모음에서 단추 **활동 창** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-122">Click hello **Refresh** button on hello toolbar in hello **Activity Windows** list.</span></span>  

<span data-ttu-id="7784f-123">데이터 팩터리 응용 프로그램 tootest으로 이러한 단계에 없을 경우 자습서 hello지 않습니다: [Blob 저장소 tooSQL 데이터 팩터리를 사용 하 여 데이터베이스에서에서 데이터를 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-123">If you don't have a Data Factory application tootest these steps with, do hello tutorial: [copy data from Blob Storage tooSQL Database using Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="understand-hello-monitoring-and-management-app"></a><span data-ttu-id="7784f-124">Hello 모니터링 및 관리 응용 프로그램 이해</span><span class="sxs-lookup"><span data-stu-id="7784f-124">Understand hello Monitoring and Management app</span></span>
<span data-ttu-id="7784f-125">Hello 왼쪽에는 세 개의 탭: **리소스 탐색기**, **모니터링 보기**, 및 **경고**합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-125">There are three tabs on hello left: **Resource Explorer**, **Monitoring Views**, and **Alerts**.</span></span> <span data-ttu-id="7784f-126">hello 첫 번째 탭 (**리소스 탐색기**) 기본적으로 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-126">hello first tab (**Resource Explorer**) is selected by default.</span></span>

### <a name="resource-explorer"></a><span data-ttu-id="7784f-127">리소스 탐색기</span><span class="sxs-lookup"><span data-stu-id="7784f-127">Resource Explorer</span></span>
<span data-ttu-id="7784f-128">Hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-128">You see hello following:</span></span>

* <span data-ttu-id="7784f-129">리소스 탐색기 hello **트리 보기** hello 왼쪽된 창에서.</span><span class="sxs-lookup"><span data-stu-id="7784f-129">hello Resource Explorer **tree view** in hello left pane.</span></span>
* <span data-ttu-id="7784f-130">hello **다이어그램 보기** hello 가운데 창에서 hello 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-130">hello **Diagram View** at hello top in hello middle pane.</span></span>
* <span data-ttu-id="7784f-131">hello **활동 창** hello 가운데 창에서 hello 맨 아래에는 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-131">hello **Activity Windows** list at hello bottom in hello middle pane.</span></span>
* <span data-ttu-id="7784f-132">hello **속성**, **활동 창 탐색기**, 및 **스크립트** hello 오른쪽 창에서 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-132">hello **Properties**, **Activity Window Explorer**, and **Script** tabs in hello right pane.</span></span>

<span data-ttu-id="7784f-133">리소스 탐색기 트리 뷰에서 hello data factory에 모든 리소스 (파이프라인, 데이터 집합, 연결 된 서비스)를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-133">In Resource Explorer, you see all resources (pipelines, datasets, linked services) in hello data factory in a tree view.</span></span> <span data-ttu-id="7784f-134">리소스 탐색기에서 개체를 선택하는 경우:</span><span class="sxs-lookup"><span data-stu-id="7784f-134">When you select an object in Resource Explorer:</span></span>

* <span data-ttu-id="7784f-135">hello 관련 Data Factory 엔터티에 hello 다이어그램 보기에서에서 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-135">hello associated Data Factory entity is highlighted in hello Diagram View.</span></span>
* <span data-ttu-id="7784f-136">[활동 창에 연결 된](data-factory-scheduling-and-execution.md) hello 맨 아래에 hello 활동 창 목록에 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-136">[Associated activity windows](data-factory-scheduling-and-execution.md) are highlighted in hello Activity Windows list at hello bottom.</span></span>  
* <span data-ttu-id="7784f-137">hello 선택한 개체의 속성을 hello hello 오른쪽 창에서 hello 속성 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-137">hello properties of hello selected object are shown in hello Properties window in hello right pane.</span></span>
* <span data-ttu-id="7784f-138">hello hello 선택한 개체의 JSON 정의 표시 되며, 해당 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="7784f-138">hello JSON definition of hello selected object is shown, if applicable.</span></span> <span data-ttu-id="7784f-139">예: 연결된 서비스, 데이터 집합 또는 파이프라인.</span><span class="sxs-lookup"><span data-stu-id="7784f-139">For example: a linked service, a dataset, or a pipeline.</span></span>

![리소스 탐색기](./media/data-factory-monitor-manage-app/ResourceExplorer.png)

<span data-ttu-id="7784f-141">Hello 참조 [일정 예약 및 실행](data-factory-scheduling-and-execution.md) 활동 기간에 대 한 자세한 개념 정보는 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-141">See hello [Scheduling and Execution](data-factory-scheduling-and-execution.md) article for detailed conceptual information about activity windows.</span></span>

### <a name="diagram-view"></a><span data-ttu-id="7784f-142">다이어그램 뷰</span><span class="sxs-lookup"><span data-stu-id="7784f-142">Diagram View</span></span>
<span data-ttu-id="7784f-143">데이터 팩터리의 다이어그램 보기 hello 유리 toomonitor 단일 창을 제공 하 고 data factory와 해당 자산을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-143">hello Diagram View of a data factory provides a single pane of glass toomonitor and manage a data factory and its assets.</span></span> <span data-ttu-id="7784f-144">Hello 다이어그램 보기에서에서 데이터 팩터리 엔터티 (데이터 집합/파이프라인)을 선택 하면:</span><span class="sxs-lookup"><span data-stu-id="7784f-144">When you select a Data Factory entity (dataset/pipeline) in hello Diagram View:</span></span>

* <span data-ttu-id="7784f-145">데이터 팩터리 엔터티 hello hello 트리 보기에서 선택 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-145">hello data factory entity is selected in hello tree view.</span></span>
* <span data-ttu-id="7784f-146">hello 관련 활동 windows hello 활동 창 목록에 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-146">hello associated activity windows are highlighted in hello Activity Windows list.</span></span>
* <span data-ttu-id="7784f-147">hello 선택한 개체의 속성을 hello hello 속성 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-147">hello properties of hello selected object are shown in hello Properties window.</span></span>

<span data-ttu-id="7784f-148">Hello 파이프라인 (일시 중지 된 상태)에 없는 활성화 되 면 녹색 줄이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-148">When hello pipeline is enabled (not in a paused state), it's shown with a green line:</span></span>

![파이프라인 실행](./media/data-factory-monitor-manage-app/PipelineRunning.png)

<span data-ttu-id="7784f-150">일시 중지, 다시 시작 하거나 hello 다이어그램 보기에서 선택 하 고 hello 명령 모음에서 hello 단추를 사용 하 여 파이프라인을 종료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-150">You can pause, resume, or terminate a pipeline by selecting it in hello diagram view and using hello buttons on hello command bar.</span></span>

![Hello 명령 모음에서 일시 중지/다시 시작](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)
 
<span data-ttu-id="7784f-152">Hello 다이어그램 보기에서에서 hello 파이프라인에 대 한 세 가지 명령 모음 단추가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-152">There are three command bar buttons for hello pipeline in hello Diagram View.</span></span> <span data-ttu-id="7784f-153">Hello 두 번째 단추 toopause hello 파이프라인을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-153">You can use hello second button toopause hello pipeline.</span></span> <span data-ttu-id="7784f-154">일시 중지 하는 현재 활동을 실행 하는 hello를 종료 하지 않습니다 및 toocompletion 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-154">Pausing doesn't terminate hello currently running activities and lets them proceed toocompletion.</span></span> <span data-ttu-id="7784f-155">세 번째 단추 hello hello 파이프라인을 일시 중지 하 고 실행 되는 활동의 기존 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-155">hello third button pauses hello pipeline and terminates its existing executing activities.</span></span> <span data-ttu-id="7784f-156">첫 번째 단추 hello hello 파이프라인 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-156">hello first button resumes hello pipeline.</span></span> <span data-ttu-id="7784f-157">파이프라인 일시 중지 된 hello 파이프라인의 hello 색이 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-157">When your pipeline is paused, hello color of hello pipeline changes.</span></span> <span data-ttu-id="7784f-158">예를 들어, 일시 중지 된 파이프라인 같이 hello 다음 이미지에에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-158">For example, a paused pipeline looks like in hello following image:</span></span> 

![파이프라인 일시 중지](./media/data-factory-monitor-manage-app/PipelinePaused.png)

<span data-ttu-id="7784f-160">Hello Ctrl 키를 사용 하 여 여러 개 선택 하거나 둘 이상의 파이프라인 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-160">You can multi-select two or more pipelines by using hello Ctrl key.</span></span> <span data-ttu-id="7784f-161">한 번에 hello 명령 모음 단추 toopause/resume 여러 파이프라인을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-161">You can use hello command bar buttons toopause/resume multiple pipelines at a time.</span></span>

<span data-ttu-id="7784f-162">스키마는 파이프라인과 옵션 선택 toosuspend 다시 시작 또는 파이프라인을 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-162">You can also right-click a pipeline and select options toosuspend, resume, or terminate a pipeline.</span></span> 

![파이프라인에 대한 상황에 맞는 메뉴](./media/data-factory-monitor-manage-app/right-click-menu-for-pipeline.png)

<span data-ttu-id="7784f-164">Hello 클릭 **열려 파이프라인** toosee hello 파이프라인의 모든 hello 활동 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-164">Click hello **Open pipeline** option toosee all hello activities in hello pipeline.</span></span> 

![파이프라인 열기 메뉴](./media/data-factory-monitor-manage-app/OpenPipelineMenu.png)

<span data-ttu-id="7784f-166">열린 hello 파이프라인 보기에 hello 파이프라인의 모든 작업이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-166">In hello opened pipeline view, you see all activities in hello pipeline.</span></span> <span data-ttu-id="7784f-167">이 예제에서는 하나의 작업, 복사 작업만이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-167">In this example, there is only one activity: Copy Activity.</span></span> 

![열린 파이프라인](./media/data-factory-monitor-manage-app/OpenedPipeline.png)

<span data-ttu-id="7784f-169">toogo toohello 이전 뷰를 다시 hello 데이터 팩토리 이름이 hello 위쪽 hello 이동 경로 탐색 메뉴에서를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-169">toogo back toohello previous view, click hello data factory name in hello breadcrumb menu at hello top.</span></span>

<span data-ttu-id="7784f-170">Hello 파이프라인 보기에서 출력 데이터 집합 또는 hello 출력 데이터 집합 위로 마우스를 이동 하면 선택 하면 해당 데이터 집합에 대 한 hello 활동 창 팝업 창이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-170">In hello pipeline view, when you select an output dataset or when you move your mouse over hello output dataset, you see hello Activity Windows pop-up window for that dataset.</span></span>

![활동 기간 팝업 창](./media/data-factory-monitor-manage-app/ActivityWindowsPopup.png)

<span data-ttu-id="7784f-172">클릭할 수 있는 작업 창 toosee 세부 정보에 대 한 hello에 **속성** hello 오른쪽 창에서 창.</span><span class="sxs-lookup"><span data-stu-id="7784f-172">You can click an activity window toosee details for it in hello **Properties** window in hello right pane.</span></span>

![활동 기간 속성](./media/data-factory-monitor-manage-app/ActivityWindowProperties.png)

<span data-ttu-id="7784f-174">Hello 오른쪽 창에서 toohello 전환 **활동 Window 탐색기** toosee 자세한 세부 정보를 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-174">In hello right pane, switch toohello **Activity Window Explorer** tab toosee more details.</span></span>

![작업 창 탐색기](./media/data-factory-monitor-manage-app/ActivityWindowExplorer.png)

<span data-ttu-id="7784f-176">또한 참조 **변수 해결** hello에 있는 활동에 대 한 각 실행된 시도 대 한 **시도** 섹션.</span><span class="sxs-lookup"><span data-stu-id="7784f-176">You also see **resolved variables** for each run attempt for an activity in hello **Attempts** section.</span></span>

![확인된 변수](./media/data-factory-monitor-manage-app/ResolvedVariables.PNG)

<span data-ttu-id="7784f-178">Toohello 전환 **스크립트** toosee hello JSON 스크립트 hello 선택한 개체에 대 한 정의 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-178">Switch toohello **Script** tab toosee hello JSON script definition for hello selected object.</span></span>   

![스크립트 탭](./media/data-factory-monitor-manage-app/ScriptTab.png)

<span data-ttu-id="7784f-180">세 위치에서 작업 창을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-180">You can see activity windows in three places:</span></span>

* <span data-ttu-id="7784f-181">hello 활동 창 팝업 hello 다이어그램 보기 (가운데 창)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-181">hello Activity Windows pop-up in hello Diagram View (middle pane).</span></span>
* <span data-ttu-id="7784f-182">활동 창 탐색기 hello 오른쪽 창에서 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-182">hello Activity Window Explorer in hello right pane.</span></span>
* <span data-ttu-id="7784f-183">hello 아래쪽 창에 hello 활동 창 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-183">hello Activity Windows list in hello bottom pane.</span></span>

<span data-ttu-id="7784f-184">Hello 활동 창 팝업 및 활동 창 탐색기에 이전 주 toohello를 스크롤할 수 있습니다 및 hello를 사용 하 여 다음 주 hello 왼쪽 및 오른쪽 화살표입니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-184">In hello Activity Windows pop-up and Activity Window Explorer, you can scroll toohello previous week and hello next week by using hello left and right arrows.</span></span>

![활동 기간 탐색기 왼쪽/오른쪽 화살표](./media/data-factory-monitor-manage-app/ActivityWindowExplorerLeftRightArrows.png)

<span data-ttu-id="7784f-186">이러한 단추 hello 다이어그램 보기의 hello 맨 아래에 표시: 확대, 축소, 확대/축소 tooFit 잠금 레이아웃 100% 확대/축소 합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-186">At hello bottom of hello Diagram View, you see these buttons: Zoom In, Zoom Out, Zoom tooFit, Zoom 100%, Lock layout.</span></span> <span data-ttu-id="7784f-187">hello **잠금 레이아웃** 단추 실수로 hello 다이어그램 보기에서에서 테이블 및 파이프라인을 이동 하면 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-187">hello **Lock layout** button prevents you from accidentally moving tables and pipelines in hello Diagram View.</span></span> <span data-ttu-id="7784f-188">기본적으로 해제된 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-188">It's on by default.</span></span> <span data-ttu-id="7784f-189">해제 한 hello 다이어그램에 엔터티를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-189">You can turn it off and move entities around in hello diagram.</span></span> <span data-ttu-id="7784f-190">를 설정 하면 hello 마지막 단추 tooautomatically 위치 테이블 및 파이프라인을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-190">When you turn it off, you can use hello last button tooautomatically position tables and pipelines.</span></span> <span data-ttu-id="7784f-191">Hello 마우스 휠을 사용 하 여 in 또는 out을 확대할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-191">You can also zoom in or out by using hello mouse wheel.</span></span>

![다이어그램 뷰 확대/축소 명령](./media/data-factory-monitor-manage-app/DiagramViewZoomCommands.png)

### <a name="activity-windows-list"></a><span data-ttu-id="7784f-193">활동 기간 목록</span><span class="sxs-lookup"><span data-stu-id="7784f-193">Activity Windows list</span></span>
<span data-ttu-id="7784f-194">hello hello 가운데 창 맨 아래에 hello 활동 창 목록에는 hello 리소스 탐색기 또는 hello 다이어그램 보기에서 선택한 hello 데이터 집합에 대 한 모든 작업 창이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-194">hello Activity Windows list at hello bottom of hello middle pane displays all activity windows for hello dataset that you selected in hello Resource Explorer or hello Diagram View.</span></span> <span data-ttu-id="7784f-195">기본적으로 hello 목록은 내림차순으로 hello 위쪽 hello 최신 활동 창에 표시 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-195">By default, hello list is in descending order, which means that you see hello latest activity window at hello top.</span></span>

![활동 기간 목록](./media/data-factory-monitor-manage-app/ActivityWindowsList.png)

<span data-ttu-id="7784f-197">이 목록 새로 고칠 hello 도구 모음 toomanually에 hello 새로 고침 단추를 사용 하도록 자동으로 반영 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-197">This list doesn't refresh automatically, so use hello refresh button on hello toolbar toomanually refresh it.</span></span>  

<span data-ttu-id="7784f-198">활동 windows hello 다음 상태 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-198">Activity windows can be in one of hello following statuses:</span></span>

<table>
<tr>
    <th align="left"><span data-ttu-id="7784f-199">가동 상태</span><span class="sxs-lookup"><span data-stu-id="7784f-199">Status</span></span></th><th align="left"><span data-ttu-id="7784f-200">하위 상태</span><span class="sxs-lookup"><span data-stu-id="7784f-200">Substatus</span></span></th><th align="left"><span data-ttu-id="7784f-201">설명</span><span class="sxs-lookup"><span data-stu-id="7784f-201">Description</span></span></th>
</tr>
<tr>
    <td rowspan="8"><span data-ttu-id="7784f-202">대기</span><span class="sxs-lookup"><span data-stu-id="7784f-202">Waiting</span></span></td><td><span data-ttu-id="7784f-203">ScheduleTime</span><span class="sxs-lookup"><span data-stu-id="7784f-203">ScheduleTime</span></span></td><td><span data-ttu-id="7784f-204">hello에 활동 창 toorun hello에 대 한 대로 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-204">hello time hasn't come for hello activity window toorun.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="7784f-205">DatasetDependencies</span><span class="sxs-lookup"><span data-stu-id="7784f-205">DatasetDependencies</span></span></td><td><span data-ttu-id="7784f-206">업스트림 종속성 hello 준비 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-206">hello upstream dependencies aren't ready.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="7784f-207">ComputeResources</span><span class="sxs-lookup"><span data-stu-id="7784f-207">ComputeResources</span></span></td><td><span data-ttu-id="7784f-208">hello 계산 리소스를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-208">hello compute resources aren't available.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="7784f-209">ConcurrencyLimit</span><span class="sxs-lookup"><span data-stu-id="7784f-209">ConcurrencyLimit</span></span></td> <td><span data-ttu-id="7784f-210">모든 hello 활동 인스턴스는 다른 활동 창 실행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-210">All hello activity instances are busy running other activity windows.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="7784f-211">ActivityResume</span><span class="sxs-lookup"><span data-stu-id="7784f-211">ActivityResume</span></span></td><td><span data-ttu-id="7784f-212">hello 활동 일시 중지 및 다시 시작 될 때까지 활동 windows hello를 실행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-212">hello activity is paused and can't run hello activity windows until it's resumed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="7784f-213">Retry</span><span class="sxs-lookup"><span data-stu-id="7784f-213">Retry</span></span></td><td><span data-ttu-id="7784f-214">hello 활동 실행을 시도 하는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-214">hello activity execution is being retried.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="7784f-215">유효성 검사</span><span class="sxs-lookup"><span data-stu-id="7784f-215">Validation</span></span></td><td><span data-ttu-id="7784f-216">유효성 검사가 아직 시작되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-216">Validation hasn't started yet.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="7784f-217">ValidationRetry</span><span class="sxs-lookup"><span data-stu-id="7784f-217">ValidationRetry</span></span></td><td><span data-ttu-id="7784f-218">유효성 검사는 대기 중인 toobe 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-218">Validation is waiting toobe retried.</span></span></td>
</tr>
<tr>
<tr>
<td rowspan="2"><span data-ttu-id="7784f-219">InProgress</span><span class="sxs-lookup"><span data-stu-id="7784f-219">InProgress</span></span></td><td><span data-ttu-id="7784f-220">유효성 검사 중</span><span class="sxs-lookup"><span data-stu-id="7784f-220">Validating</span></span></td><td><span data-ttu-id="7784f-221">유효성 검사가 진행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-221">Validation is in progress.</span></span></td>
</tr>
<td>-</td>
<td><span data-ttu-id="7784f-222">hello 활동 창 처리 중입니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-222">hello activity window is being processed.</span></span></td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="7784f-223">실패</span><span class="sxs-lookup"><span data-stu-id="7784f-223">Failed</span></span></td><td><span data-ttu-id="7784f-224">TimedOut</span><span class="sxs-lookup"><span data-stu-id="7784f-224">TimedOut</span></span></td><td><span data-ttu-id="7784f-225">hello 활동 실행 hello 활동에 의해 허용 된 것 보다 더 오래 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-225">hello activity execution took longer than what is allowed by hello activity.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="7784f-226">Canceled</span><span class="sxs-lookup"><span data-stu-id="7784f-226">Canceled</span></span></td><td><span data-ttu-id="7784f-227">hello 활동 창 사용자 작업에 의해 취소 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-227">hello activity window was canceled by user action.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="7784f-228">유효성 검사</span><span class="sxs-lookup"><span data-stu-id="7784f-228">Validation</span></span></td><td><span data-ttu-id="7784f-229">유효성 검사가 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-229">Validation has failed.</span></span></td>
</tr>
<tr>
<td>-</td><td><span data-ttu-id="7784f-230">hello 활동 창 toobe 생성 하거나 유효성을 검사 하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-230">hello activity window failed toobe generated or validated.</span></span></td>
</tr>
<td><span data-ttu-id="7784f-231">Ready</span><span class="sxs-lookup"><span data-stu-id="7784f-231">Ready</span></span></td><td>-</td><td><span data-ttu-id="7784f-232">hello 활동 창이 준비가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-232">hello activity window is ready for consumption.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="7784f-233">생략</span><span class="sxs-lookup"><span data-stu-id="7784f-233">Skipped</span></span></td><td>-</td><td><span data-ttu-id="7784f-234">hello 활동 창 처리 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-234">hello activity window wasn't processed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="7784f-235">없음</span><span class="sxs-lookup"><span data-stu-id="7784f-235">None</span></span></td><td>-</td><td><span data-ttu-id="7784f-236">활동 창 tooexist 다른 상태와 함께 사용 되지만 다시 설정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-236">An activity window used tooexist with a different status, but has been reset.</span></span></td>
</tr>
</table>


<span data-ttu-id="7784f-237">Hello에서 항목에 대 한 정보를 참조 하는 활동 창의 hello 목록에서를 클릭 하면 **활동 Windows 탐색기** 또는 hello **속성** hello 오른쪽에 창입니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-237">When you click an activity window in hello list, you see details about it in hello **Activity Windows Explorer** or hello **Properties** window on hello right.</span></span>

![작업 창 탐색기](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-2.png)

### <a name="refresh-activity-windows"></a><span data-ttu-id="7784f-239">작업 창 새로 고침</span><span class="sxs-lookup"><span data-stu-id="7784f-239">Refresh activity windows</span></span>
<span data-ttu-id="7784f-240">hello 세부 정보를 자동으로 새로 아닌, hello 명령 모음 toomanually 새로 고침 hello 활동 창 목록에서는 hello 새로 고침 단추 (hello 두 번째 단추)를 사용 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-240">hello details aren't automatically refreshed, so use hello refresh button (hello second button) on hello command bar toomanually refresh hello activity windows list.</span></span>  

### <a name="properties-window"></a><span data-ttu-id="7784f-241">속성 창</span><span class="sxs-lookup"><span data-stu-id="7784f-241">Properties window</span></span>
<span data-ttu-id="7784f-242">속성 창 hello hello 모니터링 및 관리 응용 프로그램의 hello 맨 오른쪽 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-242">hello Properties window is in hello right-most pane of hello Monitoring and Management app.</span></span>

![속성 창](./media/data-factory-monitor-manage-app/PropertiesWindow.png)

<span data-ttu-id="7784f-244">Hello 리소스 탐색기 (트리 보기)에서 선택한 hello 항목의 속성을 표시 다이어그램 보기 또는 작업 창 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-244">It displays properties for hello item that you selected in hello Resource Explorer (tree view), Diagram View, or Activity Windows list.</span></span>

### <a name="activity-window-explorer"></a><span data-ttu-id="7784f-245">작업 창 탐색기</span><span class="sxs-lookup"><span data-stu-id="7784f-245">Activity Window Explorer</span></span>
<span data-ttu-id="7784f-246">hello **활동 창 탐색기** 창의 hello 모니터링 및 관리 응용 프로그램의 hello 맨 오른쪽 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-246">hello **Activity Window Explorer** window is in hello right-most pane of hello Monitoring and Management app.</span></span> <span data-ttu-id="7784f-247">Hello 활동 창 팝업 창이 나 hello 활동 창 목록에서 선택한 hello 활동 창에 대 한 세부 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-247">It displays details about hello activity window that you selected in hello Activity Windows pop-up window or hello Activity Windows list.</span></span>

![작업 창 탐색기](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-3.png)

<span data-ttu-id="7784f-249">Hello 위쪽 hello 일정 보기에서 클릭 하 여 tooanother 활동 창을 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-249">You can switch tooanother activity window by clicking it in hello calendar view at hello top.</span></span> <span data-ttu-id="7784f-250">이전 주 hello 상위 toosee 활동 windows hello에서에 hello 왼쪽된 화살표/오른쪽 화살표 단추를 사용 하거나 다음 주 hello 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-250">You can also use hello left arrow/right arrow buttons at hello top toosee activity windows from hello previous week or hello next week.</span></span>

<span data-ttu-id="7784f-251">Hello 아래쪽 창 toorerun hello 활동 창의 hello 도구 모음 단추를에서 사용 하거나 hello 창의 hello 세부 정보를 새로 고칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-251">You can use hello toolbar buttons in hello bottom pane toorerun hello activity window or refresh hello details in hello pane.</span></span>

### <a name="script"></a><span data-ttu-id="7784f-252">스크립트</span><span class="sxs-lookup"><span data-stu-id="7784f-252">Script</span></span>
<span data-ttu-id="7784f-253">Hello를 사용할 수 있습니다 **스크립트** 탭 tooview hello hello의 JSON 정의 데이터 팩터리의 엔터티 (연결 된 서비스, 데이터 집합 또는 파이프라인)를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-253">You can use hello **Script** tab tooview hello JSON definition of hello selected Data Factory entity (linked service, dataset, or pipeline).</span></span>

![스크립트 탭](./media/data-factory-monitor-manage-app/ScriptTab.png)

## <a name="use-system-views"></a><span data-ttu-id="7784f-255">시스템 뷰 사용</span><span class="sxs-lookup"><span data-stu-id="7784f-255">Use system views</span></span>
<span data-ttu-id="7784f-256">hello 모니터링 및 관리 응용 프로그램에 포함 되어 미리 작성 된 시스템 뷰 (**최근 활동 창**, **활동 창 실패**, **진행 중인 활동 창**)를 데이터 팩토리에 대 한 최근/실패/진행 중인 활동 창 tooview 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-256">hello Monitoring and Management app includes pre-built system views (**Recent activity windows**, **Failed activity windows**, **In-Progress activity windows**) that allow you tooview recent/failed/in-progress activity windows for your data factory.</span></span>

<span data-ttu-id="7784f-257">Toohello 전환 **모니터링 보기** 클릭 하 여 hello 왼쪽에 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-257">Switch toohello **Monitoring Views** tab on hello left by clicking it.</span></span>

![모니터링 뷰 탭](./media/data-factory-monitor-manage-app/MonitoringViewsTab.png)

<span data-ttu-id="7784f-259">현재는 지원되는 세 가지 시스템 뷰가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-259">Currently, there are three system views that are supported.</span></span> <span data-ttu-id="7784f-260">선택 옵션 toosee 최근 활동 창, 실패 한 작업으로 windows 또는 진행 중인 활동 창 (hello 맨 hello 가운데 창) 아래에 hello 활동 창 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-260">Select an option toosee recent activity windows, failed activity windows, or in-progress activity windows in hello Activity Windows list (at hello bottom of hello middle pane).</span></span>

<span data-ttu-id="7784f-261">Hello를 선택 하는 경우 **최근 활동 창** 모든 최근 활동 windows hello의 내림차순 표시 옵션을 **마지막 시도 시간**합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-261">When you select hello **Recent activity windows** option, you see all recent activity windows in descending order of hello **last attempt time**.</span></span>

<span data-ttu-id="7784f-262">Hello를 사용할 수 있습니다 **활동 창 실패** 실패 toosee 모든 활동 windows hello 목록에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-262">You can use hello **Failed activity windows** view toosee all failed activity windows in hello list.</span></span> <span data-ttu-id="7784f-263">Hello 목록 toosee 세부 정보에서 항목에 대 한 hello에 실패 한 작업 기간을 선택 합니다. **속성** 창이 나 hello **활동 창 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-263">Select a failed activity window in hello list toosee details about it in hello **Properties** window or hello **Activity Window Explorer**.</span></span> <span data-ttu-id="7784f-264">또한 실패한 작업 창에 대한 로그를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-264">You can also download any logs for a failed activity window.</span></span>

## <a name="sort-and-filter-activity-windows"></a><span data-ttu-id="7784f-265">활동 기간 정렬 및 필터링</span><span class="sxs-lookup"><span data-stu-id="7784f-265">Sort and filter activity windows</span></span>
<span data-ttu-id="7784f-266">변경 hello **시작 시간** 및 **종료 시간** hello 명령 모음 toofilter 활동 창에서에서 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-266">Change hello **start time** and **end time** settings in hello command bar toofilter activity windows.</span></span> <span data-ttu-id="7784f-267">Hello 시작 시간과 종료 시간을 변경한 후 hello 단추 다음 toohello 종료 시간 toorefresh hello 활동 창 목록을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-267">After you change hello start time and end time, click hello button next toohello end time toorefresh hello Activity Windows list.</span></span>

![시작 및 종료 시간](./media/data-factory-monitor-manage-app/StartAndEndTimes.png)

> [!NOTE]
> <span data-ttu-id="7784f-269">현재 모든 시간은 UTC 형식 hello 모니터링 및 관리 앱에는.</span><span class="sxs-lookup"><span data-stu-id="7784f-269">Currently, all times are in UTC format in hello Monitoring and Management app.</span></span>
>
>

<span data-ttu-id="7784f-270">Hello에 **활동 창 목록**, hello 열 이름을 클릭 하 여 (예: 상태).</span><span class="sxs-lookup"><span data-stu-id="7784f-270">In hello **Activity Windows list**, click hello name of a column (for example: Status).</span></span>

![활동 기간 목록 열 메뉴](./media/data-factory-monitor-manage-app/ActivityWindowsListColumnMenu.png)

<span data-ttu-id="7784f-272">작업을 수행할 수 hello 다음:</span><span class="sxs-lookup"><span data-stu-id="7784f-272">You can do hello following:</span></span>

* <span data-ttu-id="7784f-273">오름차순으로 정렬.</span><span class="sxs-lookup"><span data-stu-id="7784f-273">Sort in ascending order.</span></span>
* <span data-ttu-id="7784f-274">내림차순으로 정렬.</span><span class="sxs-lookup"><span data-stu-id="7784f-274">Sort in descending order.</span></span>
* <span data-ttu-id="7784f-275">하나 이상의 값으로 필터링(준비, 대기 중 등).</span><span class="sxs-lookup"><span data-stu-id="7784f-275">Filter by one or more values (Ready, Waiting, and so on).</span></span>

<span data-ttu-id="7784f-276">열에 필터를 지정 하면 hello hello 열의 값이 필터링 된 값 임을 나타냅니다. 해당 열에 대해 사용 하도록 설정 하는 hello 필터 단추가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-276">When you specify a filter on a column, you see hello filter button enabled for that column, which indicates that hello values in hello column are filtered values.</span></span>

![Hello 활동 창 목록의 열은 필터링](./media/data-factory-monitor-manage-app/ActivityWindowsListFilterInColumn.png)

<span data-ttu-id="7784f-278">에서는 동일한 팝업 창 tooclear 필터 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-278">You can use hello same pop-up window tooclear filters.</span></span> <span data-ttu-id="7784f-279">hello 활동 창 목록에 대 한 모든 필터 tooclear hello 명령 모음에서 hello 필터 지우기 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-279">tooclear all filters for hello Activity Windows list, click hello clear filter button on hello command bar.</span></span>

![Hello 활동 창 목록에 대 한 모든 필터 지우기](./media/data-factory-monitor-manage-app/ClearAllFiltersActivityWindowsList.png)

## <a name="perform-batch-actions"></a><span data-ttu-id="7784f-281">배치 작업 수행</span><span class="sxs-lookup"><span data-stu-id="7784f-281">Perform batch actions</span></span>
### <a name="rerun-selected-activity-windows"></a><span data-ttu-id="7784f-282">선택한 작업 창 다시 실행</span><span class="sxs-lookup"><span data-stu-id="7784f-282">Rerun selected activity windows</span></span>
<span data-ttu-id="7784f-283">활동을 선택 하 고 아래쪽 화살표 hello 첫 번째 명령 모음 단추에 대 한 hello를 클릭 한 다음이 선택 **다시 실행** / **파이프라인에서 업스트림와 다시 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-283">Select an activity window, click hello down arrow for hello first command bar button, and select **Rerun** / **Rerun with upstream in pipeline**.</span></span> <span data-ttu-id="7784f-284">Hello를 선택 하는 경우 **파이프라인에서 업스트림와 다시 실행** 옵션을 모두 업스트림 작업 windows를 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-284">When you select hello **Rerun with upstream in pipeline** option, it reruns all upstream activity windows as well.</span></span>
    <span data-ttu-id="7784f-285">![작업 창 다시 실행](./media/data-factory-monitor-manage-app/ReRunSlice.png)</span><span class="sxs-lookup"><span data-stu-id="7784f-285">![Rerun an activity window](./media/data-factory-monitor-manage-app/ReRunSlice.png)</span></span>

<span data-ttu-id="7784f-286">또한 hello 목록에 여러 활동 기간을 선택할 수 있으며 hello에 다시 실행 하십시오 동시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-286">You can also select multiple activity windows in hello list and rerun them at hello same time.</span></span> <span data-ttu-id="7784f-287">Toofilter 활동 windows hello 상태에 기반 할 수 있습니다 (예: **실패**)-다음 실패 hello 활동 windows hello 활동 windows toofail hello 문제를 해결 한 후 다시 실행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="7784f-287">You might want toofilter activity windows based on hello status (for example: **Failed**)--and then rerun hello failed activity windows after correcting hello issue that causes hello activity windows toofail.</span></span> <span data-ttu-id="7784f-288">Hello 다음 활동 windows hello 목록에서 필터링 하는 방법에 대 한 세부 정보 섹션을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="7784f-288">See hello following section for details about filtering activity windows in hello list.</span></span>  

### <a name="pauseresume-multiple-pipelines"></a><span data-ttu-id="7784f-289">여러 파이프라인 일시 중지/다시 시작</span><span class="sxs-lookup"><span data-stu-id="7784f-289">Pause/resume multiple pipelines</span></span>
<span data-ttu-id="7784f-290">Hello Ctrl 키를 사용 하 여 두 개 이상의 파이프라인을 다중 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-290">You can multiselect two or more pipelines by using hello Ctrl key.</span></span> <span data-ttu-id="7784f-291">(다음 이미지는 hello hello 빨간색 사각형으로 강조 표시 됩니다)는 hello 명령 모음 단추를 사용할 수 있습니다 toopause/다시 시작을 합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-291">You can use hello command bar buttons (which are highlighted in hello red rectangle in hello following image) toopause/resume them.</span></span>

![Hello 명령 모음에서 일시 중지/다시 시작](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)

## <a name="create-alerts"></a><span data-ttu-id="7784f-293">경고 만들기</span><span class="sxs-lookup"><span data-stu-id="7784f-293">Create alerts</span></span>
<span data-ttu-id="7784f-294">hello **경고** 페이지에서는 경고와 보기/편집/삭제 기존 경고를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-294">hello **Alerts** page lets you create an alert and view/edit/delete existing alerts.</span></span> <span data-ttu-id="7784f-295">또한 경고를 사용하지 않거나/사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-295">You can also disable/enable an alert.</span></span> <span data-ttu-id="7784f-296">toosee hello 경고 페이지에서 hello **경고** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-296">toosee hello Alerts page, click hello **Alerts** tab.</span></span>

![경고 탭](./media/data-factory-monitor-manage-app/AlertsTab.png)

### <a name="toocreate-an-alert"></a><span data-ttu-id="7784f-298">toocreate 경고</span><span class="sxs-lookup"><span data-stu-id="7784f-298">toocreate an alert</span></span>
1. <span data-ttu-id="7784f-299">클릭 **추가 경고** tooadd 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-299">Click **Add Alert** tooadd an alert.</span></span> <span data-ttu-id="7784f-300">Hello 참조 **세부 정보** 페이지.</span><span class="sxs-lookup"><span data-stu-id="7784f-300">You see hello **Details** page.</span></span>

    ![경고 만들기 - 세부 정보 페이지](./media/data-factory-monitor-manage-app/CreateAlertDetailsPage.png)
2. <span data-ttu-id="7784f-302">Hello 지정 **이름** 및 **설명** hello 알림과 클릭에 대 한 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-302">Specify hello **Name** and **Description** for hello alert, and click **Next**.</span></span> <span data-ttu-id="7784f-303">Hello 표시 되어야 **필터** 페이지.</span><span class="sxs-lookup"><span data-stu-id="7784f-303">You should see hello **Filters** page.</span></span>

    ![경고 만들기 - 필터 페이지](./media/data-factory-monitor-manage-app/CreateAlertFiltersPage.png)
3. <span data-ttu-id="7784f-305">선택 hello **이벤트**, **상태**, 및 **하위 상태** (선택 사항) 원하는 toocreate 데이터 팩터리 서비스에 대 한 경고 및 클릭 **다음**.</span><span class="sxs-lookup"><span data-stu-id="7784f-305">Select hello **event**, **status**, and **substatus** (optional) that you want toocreate a Data Factory service alert for, and click **Next**.</span></span> <span data-ttu-id="7784f-306">Hello 표시 되어야 **받는 사람에 게** 페이지.</span><span class="sxs-lookup"><span data-stu-id="7784f-306">You should see hello **Recipients** page.</span></span>

    ![경고 만들기 - 받는 사람 페이지](./media/data-factory-monitor-manage-app/CreateAlertRecipientsPage.png)
4. <span data-ttu-id="7784f-308">선택 hello **구독 관리자 전자 메일** 옵션 및/또는 입력 한 **추가 관리자 전자 메일**를 클릭 하 고 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-308">Select hello **Email subscription admins** option and/or enter an **additional administrator email**, and click **Finish**.</span></span> <span data-ttu-id="7784f-309">Hello 경고 hello 목록에 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-309">You should see hello alert in hello list.</span></span>

    ![경고 목록](./media/data-factory-monitor-manage-app/AlertsList.png)

<span data-ttu-id="7784f-311">Hello 경고 목록에서 hello 경고 tooedit/삭제/비활성화/활성화 경고와 관련 된 hello 단추를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-311">In hello Alerts list, use hello buttons that are associated with hello alert tooedit/delete/disable/enable an alert.</span></span>

### <a name="eventstatussubstatus"></a><span data-ttu-id="7784f-312">이벤트/상태/하위 상태</span><span class="sxs-lookup"><span data-stu-id="7784f-312">Event/status/substatus</span></span>
<span data-ttu-id="7784f-313">hello 다음 표에서 hello 목록을 사용할 수 있는 이벤트 및 상태 (및 하위 상태).</span><span class="sxs-lookup"><span data-stu-id="7784f-313">hello following table provides hello list of available events and statuses (and substatuses).</span></span>

| <span data-ttu-id="7784f-314">이벤트 이름</span><span class="sxs-lookup"><span data-stu-id="7784f-314">Event name</span></span> | <span data-ttu-id="7784f-315">가동 상태</span><span class="sxs-lookup"><span data-stu-id="7784f-315">Status</span></span> | <span data-ttu-id="7784f-316">하위 상태</span><span class="sxs-lookup"><span data-stu-id="7784f-316">Substatus</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7784f-317">작업 실행 시작</span><span class="sxs-lookup"><span data-stu-id="7784f-317">Activity Run Started</span></span> |<span data-ttu-id="7784f-318">Started</span><span class="sxs-lookup"><span data-stu-id="7784f-318">Started</span></span> |<span data-ttu-id="7784f-319">시작 중</span><span class="sxs-lookup"><span data-stu-id="7784f-319">Starting</span></span> |
| <span data-ttu-id="7784f-320">작업 실행 완료</span><span class="sxs-lookup"><span data-stu-id="7784f-320">Activity Run Finished</span></span> |<span data-ttu-id="7784f-321">Succeeded</span><span class="sxs-lookup"><span data-stu-id="7784f-321">Succeeded</span></span> |<span data-ttu-id="7784f-322">Succeeded</span><span class="sxs-lookup"><span data-stu-id="7784f-322">Succeeded</span></span> |
| <span data-ttu-id="7784f-323">작업 실행 완료</span><span class="sxs-lookup"><span data-stu-id="7784f-323">Activity Run Finished</span></span> |<span data-ttu-id="7784f-324">실패</span><span class="sxs-lookup"><span data-stu-id="7784f-324">Failed</span></span> |<span data-ttu-id="7784f-325">실패한 리소스 할당</span><span class="sxs-lookup"><span data-stu-id="7784f-325">Failed Resource Allocation</span></span><br/><br/><span data-ttu-id="7784f-326">실패한 실행</span><span class="sxs-lookup"><span data-stu-id="7784f-326">Failed Execution</span></span><br/><br/><span data-ttu-id="7784f-327">Timed Out</span><span class="sxs-lookup"><span data-stu-id="7784f-327">Timed Out</span></span><br/><br/><span data-ttu-id="7784f-328">Failed Validation</span><span class="sxs-lookup"><span data-stu-id="7784f-328">Failed Validation</span></span><br/><br/><span data-ttu-id="7784f-329">Abandoned</span><span class="sxs-lookup"><span data-stu-id="7784f-329">Abandoned</span></span> |
| <span data-ttu-id="7784f-330">주문형 HDI 클러스터 만들기 시작</span><span class="sxs-lookup"><span data-stu-id="7784f-330">On-Demand HDI Cluster Create Started</span></span> |<span data-ttu-id="7784f-331">Started</span><span class="sxs-lookup"><span data-stu-id="7784f-331">Started</span></span> |-|
| <span data-ttu-id="7784f-332">주문형 HDI 클러스터 성공적으로 생성</span><span class="sxs-lookup"><span data-stu-id="7784f-332">On-Demand HDI Cluster Created Successfully</span></span> |<span data-ttu-id="7784f-333">Succeeded</span><span class="sxs-lookup"><span data-stu-id="7784f-333">Succeeded</span></span> |-|
| <span data-ttu-id="7784f-334">주문형 HDI 클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="7784f-334">On-Demand HDI Cluster Deleted</span></span> |<span data-ttu-id="7784f-335">Succeeded</span><span class="sxs-lookup"><span data-stu-id="7784f-335">Succeeded</span></span> |-|

### <a name="tooedit-delete-or-disable-an-alert"></a><span data-ttu-id="7784f-336">tooedit, 삭제 또는 경고를 사용 하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="7784f-336">tooedit, delete, or disable an alert</span></span>

<span data-ttu-id="7784f-337">다음 (빨간색으로 강조 표시) 단추 tooedit, 삭제 또는 사용 안 함 경고 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7784f-337">Use hello following buttons (highlighted in red) tooedit, delete, or disable an alert.</span></span>

![경고 단추](./media/data-factory-monitor-manage-app/AlertButtons.png)
