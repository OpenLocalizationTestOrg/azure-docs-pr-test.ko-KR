---
title: "데이터 파이프라인 모니터링 및 관리 - Azure | Microsoft Docs"
description: "모니터링 및 관리 앱을 사용하여 Azure Data Factory 및 파이프라인을 모니터링하고 관리하는 방법을 알아봅니다."
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
ms.openlocfilehash: d5a2d1f3d85b8a2212326cfcfd0ba5d80356b769
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-the-monitoring-and-management-app"></a><span data-ttu-id="f95ac-103">모니터링 및 관리 앱을 사용하여 Azure Data Factory 파이프라인 모니터링 및 관리</span><span class="sxs-lookup"><span data-stu-id="f95ac-103">Monitor and manage Azure Data Factory pipelines by using the Monitoring and Management app</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f95ac-104">Azure 포털/Azure PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="f95ac-104">Using Azure portal/Azure PowerShell</span></span>](data-factory-monitor-manage-pipelines.md)
> * [<span data-ttu-id="f95ac-105">모니터링 및 관리 앱 사용</span><span class="sxs-lookup"><span data-stu-id="f95ac-105">Using Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)
>
>

<span data-ttu-id="f95ac-106">이 문서는 모니터링 및 관리 앱을 사용하여 Data Factory 파이프라인을 모니터링하고 관리하고 디버그하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-106">This article describes how to use the Monitoring and Management app to monitor, manage, and debug your Data Factory pipelines.</span></span> <span data-ttu-id="f95ac-107">또한 경고를 생성하여 오류에 대한 알림을 받는 방법에 대한 정보도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-107">It also provides information on how to create alerts to get notified on failures.</span></span> <span data-ttu-id="f95ac-108">다음 비디오를 시청하여 응용 프로그램 사용을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-108">You can get started with using the application by watching the following video:</span></span>

> [!NOTE]
> <span data-ttu-id="f95ac-109">비디오에 표시된 사용자 인터페이스는 포털에 표시된 것과 정확하게 일치하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-109">The user interface shown in the video may not exactly match what you see in the portal.</span></span> <span data-ttu-id="f95ac-110">약간 더 오래되었지만 개념은 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-110">It's slightly older, but concepts remain the same.</span></span> 

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-Data-Factory-Monitoring-and-Managing-Big-Data-Piplines/player]
>

## <a name="launch-the-monitoring-and-management-app"></a><span data-ttu-id="f95ac-111">모니터링 및 관리 앱 시작</span><span class="sxs-lookup"><span data-stu-id="f95ac-111">Launch the Monitoring and Management app</span></span>
<span data-ttu-id="f95ac-112">모니터링 및 관리 앱을 시작하려면 사용자 데이터 팩터리의 **Data Factory** 블레이드에서 **모니터링 및 관리** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-112">To launch the Monitor and Management app, click the **Monitor & Manage** tile on the **Data Factory** blade for your data factory.</span></span>

![Data Factory 홈페이지의 모니터링 타일](./media/data-factory-monitor-manage-app/MonitoringAppTile.png)

<span data-ttu-id="f95ac-114">모니터링 및 관리 앱이 별도 창에 열리는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-114">You should see the Monitoring and Management app open in a separate window.</span></span>  

![모니터링 및 관리 앱](./media/data-factory-monitor-manage-app/AppLaunched.png)

> [!NOTE]
> <span data-ttu-id="f95ac-116">웹 브라우저가 "권한 부여..." 상태로 중지된 것을 확인하면 **Block third-party cookies and site data**(타사 쿠키 및 사이트 데이터 차단) 확인란 선택을 해제하거나 선택된 상태로 두고 **login.microsoftonline.com**에 대한 예외를 만든 다음 앱을 다시 열어봅니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-116">If you see that the web browser is stuck at "Authorizing...", clear the **Block third-party cookies and site data** check box--or keep it selected, create an exception for **login.microsoftonline.com**, and then try to open the app again.</span></span>


<span data-ttu-id="f95ac-117">가운데 창의 작업 창 목록에는 작업의 각 실행에 대한 작업 창이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-117">In the Activity Windows list in the middle pane, you see an activity window for each run of an activity.</span></span> <span data-ttu-id="f95ac-118">예를 들어 5시간 동안 매시간 실행되도록 예약된 작업이 있는 경우 5개의 데이터 조각과 연결된 5개 작업 창이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-118">For example, if you have the activity scheduled to run hourly for five hours, you see five activity windows associated with five data slices.</span></span> <span data-ttu-id="f95ac-119">아래쪽의 목록에 작업 창이 표시되지 않는 경우 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-119">If you don't see activity windows in the list at the bottom, do the following:</span></span>
 
- <span data-ttu-id="f95ac-120">맨 위에 있는 **시작 시간** 및 **종료 시간** 필터를 업데이트하여 파이프라인의 시작 및 종료 시간을 일치시킨 다음 **적용** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-120">Update the **start time** and **end time** filters at the top to match the start and end times of your pipeline, and then click the **Apply** button.</span></span>  
- <span data-ttu-id="f95ac-121">작업 창 목록은 자동으로 고쳐지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-121">The Activity Windows list is not automatically refreshed.</span></span> <span data-ttu-id="f95ac-122">**작업 창** 목록의 도구 모음에서 **새로 고침** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-122">Click the **Refresh** button on the toolbar in the **Activity Windows** list.</span></span>  

<span data-ttu-id="f95ac-123">이러한 단계를 테스트할 데이터 팩터리 응용 프로그램이 없는 경우 자습서: [데이터 팩터리를 사용하여 Blob Storage에서 SQL Database로 데이터 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-123">If you don't have a Data Factory application to test these steps with, do the tutorial: [copy data from Blob Storage to SQL Database using Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="understand-the-monitoring-and-management-app"></a><span data-ttu-id="f95ac-124">모니터링 및 관리 앱 이해</span><span class="sxs-lookup"><span data-stu-id="f95ac-124">Understand the Monitoring and Management app</span></span>
<span data-ttu-id="f95ac-125">왼쪽에 **리소스 탐색기**, **Monitoring Views**(모니터링 뷰) 및 **경고**라는 세 개의 탭이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-125">There are three tabs on the left: **Resource Explorer**, **Monitoring Views**, and **Alerts**.</span></span> <span data-ttu-id="f95ac-126">첫 번째 탭(**리소스 탐색기**)은 기본적으로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-126">The first tab (**Resource Explorer**) is selected by default.</span></span>

### <a name="resource-explorer"></a><span data-ttu-id="f95ac-127">리소스 탐색기</span><span class="sxs-lookup"><span data-stu-id="f95ac-127">Resource Explorer</span></span>
<span data-ttu-id="f95ac-128">다음이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-128">You see the following:</span></span>

* <span data-ttu-id="f95ac-129">왼쪽 창에 리소스 탐색기 **트리 뷰**.</span><span class="sxs-lookup"><span data-stu-id="f95ac-129">The Resource Explorer **tree view** in the left pane.</span></span>
* <span data-ttu-id="f95ac-130">가운데 창의 맨 위쪽에 **다이어그램 보기**.</span><span class="sxs-lookup"><span data-stu-id="f95ac-130">The **Diagram View** at the top in the middle pane.</span></span>
* <span data-ttu-id="f95ac-131">가운데 창의 아래쪽에 **활동 기간** 목록.</span><span class="sxs-lookup"><span data-stu-id="f95ac-131">The **Activity Windows** list at the bottom in the middle pane.</span></span>
* <span data-ttu-id="f95ac-132">오른쪽 창에 **속성**, **작업 창 탐색기** 및 **스크립트** 탭.</span><span class="sxs-lookup"><span data-stu-id="f95ac-132">The **Properties**, **Activity Window Explorer**, and **Script** tabs in the right pane.</span></span>

<span data-ttu-id="f95ac-133">리소스 탐색기에서 데이터 팩터리의 모든 리소스(파이프라인, 데이터 집합, 연결된 서비스)를 트리 뷰로 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-133">In Resource Explorer, you see all resources (pipelines, datasets, linked services) in the data factory in a tree view.</span></span> <span data-ttu-id="f95ac-134">리소스 탐색기에서 개체를 선택하는 경우:</span><span class="sxs-lookup"><span data-stu-id="f95ac-134">When you select an object in Resource Explorer:</span></span>

* <span data-ttu-id="f95ac-135">연결된 Data Factory 엔터티가 다이어그램 뷰에 강조 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-135">The associated Data Factory entity is highlighted in the Diagram View.</span></span>
* <span data-ttu-id="f95ac-136">[연관된 활동 기간](data-factory-scheduling-and-execution.md)이 아래쪽 활동 기간 목록에 강조 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-136">[Associated activity windows](data-factory-scheduling-and-execution.md) are highlighted in the Activity Windows list at the bottom.</span></span>  
* <span data-ttu-id="f95ac-137">선택한 개체의 속성이 오른쪽 창의 속성 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-137">The properties of the selected object are shown in the Properties window in the right pane.</span></span>
* <span data-ttu-id="f95ac-138">해당하는 경우 선택된 개체의 JSON 정의가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-138">The JSON definition of the selected object is shown, if applicable.</span></span> <span data-ttu-id="f95ac-139">예: 연결된 서비스, 데이터 집합 또는 파이프라인.</span><span class="sxs-lookup"><span data-stu-id="f95ac-139">For example: a linked service, a dataset, or a pipeline.</span></span>

![리소스 탐색기](./media/data-factory-monitor-manage-app/ResourceExplorer.png)

<span data-ttu-id="f95ac-141">활동 기간에 대한 자세한 개념 정보는 [예약 및 실행](data-factory-scheduling-and-execution.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f95ac-141">See the [Scheduling and Execution](data-factory-scheduling-and-execution.md) article for detailed conceptual information about activity windows.</span></span>

### <a name="diagram-view"></a><span data-ttu-id="f95ac-142">다이어그램 뷰</span><span class="sxs-lookup"><span data-stu-id="f95ac-142">Diagram View</span></span>
<span data-ttu-id="f95ac-143">데이터 팩터리의 다이어그램 뷰에는 데이터 팩터리와 그 자산을 모니터링하고 관리하기 위한 단일 창이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-143">The Diagram View of a data factory provides a single pane of glass to monitor and manage a data factory and its assets.</span></span> <span data-ttu-id="f95ac-144">다이어그램 뷰에서 Data Factory 엔터티(데이터 집합/파이프라인)를 선택하는 경우:</span><span class="sxs-lookup"><span data-stu-id="f95ac-144">When you select a Data Factory entity (dataset/pipeline) in the Diagram View:</span></span>

* <span data-ttu-id="f95ac-145">데이터 팩터리 엔터티가 트리 뷰에서 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-145">The data factory entity is selected in the tree view.</span></span>
* <span data-ttu-id="f95ac-146">연관된 활동 기간이 활동 기간 목록에 강조 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-146">The associated activity windows are highlighted in the Activity Windows list.</span></span>
* <span data-ttu-id="f95ac-147">선택한 개체의 속성이 속성 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-147">The properties of the selected object are shown in the Properties window.</span></span>

<span data-ttu-id="f95ac-148">파이프라인을 사용하도록 설정한 경우(일시 중지된 상태가 아님) 녹색 선으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-148">When the pipeline is enabled (not in a paused state), it's shown with a green line:</span></span>

![파이프라인 실행](./media/data-factory-monitor-manage-app/PipelineRunning.png)

<span data-ttu-id="f95ac-150">다이어그램 보기에서 선택하고 명령 모음에서 단추를 사용하여 파이프라인을 일시 중지, 다시 시작 또는 종료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-150">You can pause, resume, or terminate a pipeline by selecting it in the diagram view and using the buttons on the command bar.</span></span>

![명령 모음에서 일시 중지/다시 시작](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)
 
<span data-ttu-id="f95ac-152">다이어그램 뷰에 파이프라인에 대한 세 개의 명령 모음 단추가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-152">There are three command bar buttons for the pipeline in the Diagram View.</span></span> <span data-ttu-id="f95ac-153">두 번째 단추를 사용하여 파이프라인을 일시 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-153">You can use the second button to pause the pipeline.</span></span> <span data-ttu-id="f95ac-154">일시 중지할 경우 현재 실행 중인 활동을 종료하지 않고 완료될 때까지 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-154">Pausing doesn't terminate the currently running activities and lets them proceed to completion.</span></span> <span data-ttu-id="f95ac-155">세 번째 단추는 파이프라인을 일시 중지하고 실행 중인 기존의 활동을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-155">The third button pauses the pipeline and terminates its existing executing activities.</span></span> <span data-ttu-id="f95ac-156">첫 번째 단추는 파이프라인을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-156">The first button resumes the pipeline.</span></span> <span data-ttu-id="f95ac-157">파이프라인이 일시 중지되면 파이프라인 색이 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-157">When your pipeline is paused, the color of the pipeline changes.</span></span> <span data-ttu-id="f95ac-158">예를 들어, 일시 중지된 파이프라인은 다음 그림과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-158">For example, a paused pipeline looks like in the following image:</span></span> 

![파이프라인 일시 중지](./media/data-factory-monitor-manage-app/PipelinePaused.png)

<span data-ttu-id="f95ac-160">Ctrl 키를 사용하여 두 개 이상의 파이프라인을 다중 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-160">You can multi-select two or more pipelines by using the Ctrl key.</span></span> <span data-ttu-id="f95ac-161">명령 모음 단추를 사용하여 여러 파이프라인을 한 번에 일시 중지/다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-161">You can use the command bar buttons to pause/resume multiple pipelines at a time.</span></span>

<span data-ttu-id="f95ac-162">파이프라인을 마우스 오른쪽 단추로 클릭하고 파이프라인을 일시 중단, 다시 시작 또는 종료하는 옵션을 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-162">You can also right-click a pipeline and select options to suspend, resume, or terminate a pipeline.</span></span> 

![파이프라인에 대한 상황에 맞는 메뉴](./media/data-factory-monitor-manage-app/right-click-menu-for-pipeline.png)

<span data-ttu-id="f95ac-164">**파이프라인 열기** 옵션을 선택하여 파이프라인의 모든 작업을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-164">Click the **Open pipeline** option to see all the activities in the pipeline.</span></span> 

![파이프라인 열기 메뉴](./media/data-factory-monitor-manage-app/OpenPipelineMenu.png)

<span data-ttu-id="f95ac-166">열린 파이프라인 뷰에서 파이프라인의 모든 작업이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-166">In the opened pipeline view, you see all activities in the pipeline.</span></span> <span data-ttu-id="f95ac-167">이 예제에서는 하나의 작업, 복사 작업만이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-167">In this example, there is only one activity: Copy Activity.</span></span> 

![열린 파이프라인](./media/data-factory-monitor-manage-app/OpenedPipeline.png)

<span data-ttu-id="f95ac-169">이전 보기로 돌아가려면 맨 위에서 breadcrumb 메뉴의 데이터 팩터리 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-169">To go back to the previous view, click the data factory name in the breadcrumb menu at the top.</span></span>

<span data-ttu-id="f95ac-170">파이프라인 뷰에서 출력 데이터 집합을 선택할 경우 또는 출력 데이터 집합 위로 마우스를 이동하는 경우, 해당 데이터 집합에 대한 활동 기간 팝업 창이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-170">In the pipeline view, when you select an output dataset or when you move your mouse over the output dataset, you see the Activity Windows pop-up window for that dataset.</span></span>

![활동 기간 팝업 창](./media/data-factory-monitor-manage-app/ActivityWindowsPopup.png)

<span data-ttu-id="f95ac-172">활동 기간을 클릭하면 오른쪽 창의 **속성** 창에서 그에 대한 자세한 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-172">You can click an activity window to see details for it in the **Properties** window in the right pane.</span></span>

![활동 기간 속성](./media/data-factory-monitor-manage-app/ActivityWindowProperties.png)

<span data-ttu-id="f95ac-174">오른쪽 창에서 **활동 기간 탐색기** 탭으로 전환하여 자세한 내용을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-174">In the right pane, switch to the **Activity Window Explorer** tab to see more details.</span></span>

![작업 창 탐색기](./media/data-factory-monitor-manage-app/ActivityWindowExplorer.png)

<span data-ttu-id="f95ac-176">**Attempts**(시도) 섹션에서 활동의 각 실행 시도에 대한 **확인된 변수**도 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-176">You also see **resolved variables** for each run attempt for an activity in the **Attempts** section.</span></span>

![확인된 변수](./media/data-factory-monitor-manage-app/ResolvedVariables.PNG)

<span data-ttu-id="f95ac-178">**스크립트** 탭으로 전환하여 선택한 개체에 대한 JSON 스크립트 정의를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f95ac-178">Switch to the **Script** tab to see the JSON script definition for the selected object.</span></span>   

![스크립트 탭](./media/data-factory-monitor-manage-app/ScriptTab.png)

<span data-ttu-id="f95ac-180">세 위치에서 작업 창을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-180">You can see activity windows in three places:</span></span>

* <span data-ttu-id="f95ac-181">다이어그램 뷰에서 활동 기간 팝업(가운데 창).</span><span class="sxs-lookup"><span data-stu-id="f95ac-181">The Activity Windows pop-up in the Diagram View (middle pane).</span></span>
* <span data-ttu-id="f95ac-182">오른쪽 창에서 활동 기간 탐색기.</span><span class="sxs-lookup"><span data-stu-id="f95ac-182">The Activity Window Explorer in the right pane.</span></span>
* <span data-ttu-id="f95ac-183">아래쪽 창에서 활동 기간 목록.</span><span class="sxs-lookup"><span data-stu-id="f95ac-183">The Activity Windows list in the bottom pane.</span></span>

<span data-ttu-id="f95ac-184">활동 기간 팝업 및 활동 기간 탐색기에서 왼쪽 및 오른쪽 화살표를 사용하여 이전 주 및 다음 주로 스크롤할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-184">In the Activity Windows pop-up and Activity Window Explorer, you can scroll to the previous week and the next week by using the left and right arrows.</span></span>

![활동 기간 탐색기 왼쪽/오른쪽 화살표](./media/data-factory-monitor-manage-app/ActivityWindowExplorerLeftRightArrows.png)

<span data-ttu-id="f95ac-186">다이어그램 뷰의 아래쪽에 확대, 축소, 크기에 맞게, 100% 표시, 레이아웃 잠금 단추가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-186">At the bottom of the Diagram View, you see these buttons: Zoom In, Zoom Out, Zoom to Fit, Zoom 100%, Lock layout.</span></span> <span data-ttu-id="f95ac-187">**Lock layout**(레이아웃 잠금) 단추는 다이어그램 뷰에서 테이블 및 파이프라인을 실수로 이동하지 않도록 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-187">The **Lock layout** button prevents you from accidentally moving tables and pipelines in the Diagram View.</span></span> <span data-ttu-id="f95ac-188">기본적으로 해제된 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-188">It's on by default.</span></span> <span data-ttu-id="f95ac-189">기능을 해제하고 다이어그램에서 엔터티를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-189">You can turn it off and move entities around in the diagram.</span></span> <span data-ttu-id="f95ac-190">해제한 경우 마지막 단추를 사용하여 테이블 및 파이프라인을 자동으로 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-190">When you turn it off, you can use the last button to automatically position tables and pipelines.</span></span> <span data-ttu-id="f95ac-191">마우스 휠을 사용하여 확대하거나 축소할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-191">You can also zoom in or out by using the mouse wheel.</span></span>

![다이어그램 뷰 확대/축소 명령](./media/data-factory-monitor-manage-app/DiagramViewZoomCommands.png)

### <a name="activity-windows-list"></a><span data-ttu-id="f95ac-193">활동 기간 목록</span><span class="sxs-lookup"><span data-stu-id="f95ac-193">Activity Windows list</span></span>
<span data-ttu-id="f95ac-194">가운데 창의 맨 아래에 있는 활동 기간 목록에는 리소스 탐색기 또는 다이어그램 뷰에서 선택한 데이터 집합에 대한 모든 활동 기간이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-194">The Activity Windows list at the bottom of the middle pane displays all activity windows for the dataset that you selected in the Resource Explorer or the Diagram View.</span></span> <span data-ttu-id="f95ac-195">기본적으로 목록은 내림차순이며, 창 위쪽에 최신 활동 기간이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-195">By default, the list is in descending order, which means that you see the latest activity window at the top.</span></span>

![활동 기간 목록](./media/data-factory-monitor-manage-app/ActivityWindowsList.png)

<span data-ttu-id="f95ac-197">이 목록은 자동으로 새로 고쳐지지 않으며 수동으로 새로 고치려면 도구 모음에서 새로 고침 단추를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-197">This list doesn't refresh automatically, so use the refresh button on the toolbar to manually refresh it.</span></span>  

<span data-ttu-id="f95ac-198">활동 기간은 다음 상태 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-198">Activity windows can be in one of the following statuses:</span></span>

<table>
<tr>
    <th align="left"><span data-ttu-id="f95ac-199">가동 상태</span><span class="sxs-lookup"><span data-stu-id="f95ac-199">Status</span></span></th><th align="left"><span data-ttu-id="f95ac-200">하위 상태</span><span class="sxs-lookup"><span data-stu-id="f95ac-200">Substatus</span></span></th><th align="left"><span data-ttu-id="f95ac-201">설명</span><span class="sxs-lookup"><span data-stu-id="f95ac-201">Description</span></span></th>
</tr>
<tr>
    <td rowspan="8"><span data-ttu-id="f95ac-202">대기</span><span class="sxs-lookup"><span data-stu-id="f95ac-202">Waiting</span></span></td><td><span data-ttu-id="f95ac-203">ScheduleTime</span><span class="sxs-lookup"><span data-stu-id="f95ac-203">ScheduleTime</span></span></td><td><span data-ttu-id="f95ac-204">활동 기간을 실행할 시간이 아직 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-204">The time hasn't come for the activity window to run.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f95ac-205">DatasetDependencies</span><span class="sxs-lookup"><span data-stu-id="f95ac-205">DatasetDependencies</span></span></td><td><span data-ttu-id="f95ac-206">업스트림 종속성이 준비되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-206">The upstream dependencies aren't ready.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f95ac-207">ComputeResources</span><span class="sxs-lookup"><span data-stu-id="f95ac-207">ComputeResources</span></span></td><td><span data-ttu-id="f95ac-208">계산 리소스를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-208">The compute resources aren't available.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f95ac-209">ConcurrencyLimit</span><span class="sxs-lookup"><span data-stu-id="f95ac-209">ConcurrencyLimit</span></span></td> <td><span data-ttu-id="f95ac-210">모든 활동 인스턴스는 다른 작업 창을 실행하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-210">All the activity instances are busy running other activity windows.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f95ac-211">ActivityResume</span><span class="sxs-lookup"><span data-stu-id="f95ac-211">ActivityResume</span></span></td><td><span data-ttu-id="f95ac-212">활동이 일시 중지되어 재개될 때까지 활동 기간을 실행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-212">The activity is paused and can't run the activity windows until it's resumed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f95ac-213">Retry</span><span class="sxs-lookup"><span data-stu-id="f95ac-213">Retry</span></span></td><td><span data-ttu-id="f95ac-214">활동 실행을 다시 시도 중입니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-214">The activity execution is being retried.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f95ac-215">유효성 검사</span><span class="sxs-lookup"><span data-stu-id="f95ac-215">Validation</span></span></td><td><span data-ttu-id="f95ac-216">유효성 검사가 아직 시작되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-216">Validation hasn't started yet.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f95ac-217">ValidationRetry</span><span class="sxs-lookup"><span data-stu-id="f95ac-217">ValidationRetry</span></span></td><td><span data-ttu-id="f95ac-218">유효성 감사 다시 시도를 대기 중입니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-218">Validation is waiting to be retried.</span></span></td>
</tr>
<tr>
<tr>
<td rowspan="2"><span data-ttu-id="f95ac-219">InProgress</span><span class="sxs-lookup"><span data-stu-id="f95ac-219">InProgress</span></span></td><td><span data-ttu-id="f95ac-220">유효성 검사 중</span><span class="sxs-lookup"><span data-stu-id="f95ac-220">Validating</span></span></td><td><span data-ttu-id="f95ac-221">유효성 검사가 진행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-221">Validation is in progress.</span></span></td>
</tr>
<td>-</td>
<td><span data-ttu-id="f95ac-222">작업 창을 처리 중입니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-222">The activity window is being processed.</span></span></td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="f95ac-223">Failed</span><span class="sxs-lookup"><span data-stu-id="f95ac-223">Failed</span></span></td><td><span data-ttu-id="f95ac-224">TimedOut</span><span class="sxs-lookup"><span data-stu-id="f95ac-224">TimedOut</span></span></td><td><span data-ttu-id="f95ac-225">활동 실행이 활동에서 허용하는 것보다 오래 걸렸습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-225">The activity execution took longer than what is allowed by the activity.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f95ac-226">Canceled</span><span class="sxs-lookup"><span data-stu-id="f95ac-226">Canceled</span></span></td><td><span data-ttu-id="f95ac-227">활동 기간이 사용자 작업으로 인해 취소되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-227">The activity window was canceled by user action.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f95ac-228">유효성 검사</span><span class="sxs-lookup"><span data-stu-id="f95ac-228">Validation</span></span></td><td><span data-ttu-id="f95ac-229">유효성 검사가 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-229">Validation has failed.</span></span></td>
</tr>
<tr>
<td>-</td><td><span data-ttu-id="f95ac-230">활동 창이 생성되거나 유효성이 검사되지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-230">The activity window failed to be generated or validated.</span></span></td>
</tr>
<td><span data-ttu-id="f95ac-231">Ready</span><span class="sxs-lookup"><span data-stu-id="f95ac-231">Ready</span></span></td><td>-</td><td><span data-ttu-id="f95ac-232">작업 창을 사용할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-232">The activity window is ready for consumption.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f95ac-233">생략</span><span class="sxs-lookup"><span data-stu-id="f95ac-233">Skipped</span></span></td><td>-</td><td><span data-ttu-id="f95ac-234">활동 기간이 처리되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-234">The activity window wasn't processed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f95ac-235">없음</span><span class="sxs-lookup"><span data-stu-id="f95ac-235">None</span></span></td><td>-</td><td><span data-ttu-id="f95ac-236">활동 기간이 다른 상태와 함께 존재하는 데 사용되었지만 다시 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-236">An activity window used to exist with a different status, but has been reset.</span></span></td>
</tr>
</table>


<span data-ttu-id="f95ac-237">목록에서 활동 기간을 클릭하면 오른쪽에 있는 **속성** 창 또는 **활동 기간 탐색기**에 자세한 내용이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-237">When you click an activity window in the list, you see details about it in the **Activity Windows Explorer** or the **Properties** window on the right.</span></span>

![작업 창 탐색기](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-2.png)

### <a name="refresh-activity-windows"></a><span data-ttu-id="f95ac-239">작업 창 새로 고침</span><span class="sxs-lookup"><span data-stu-id="f95ac-239">Refresh activity windows</span></span>
<span data-ttu-id="f95ac-240">세부 정보는 자동으로 새로 고쳐지지 않으므로 명령 모음에서 새로 고침 단추(두 번째 단추)를 사용하여 수동으로 활동 기간 목록을 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-240">The details aren't automatically refreshed, so use the refresh button (the second button) on the command bar to manually refresh the activity windows list.</span></span>  

### <a name="properties-window"></a><span data-ttu-id="f95ac-241">속성 창</span><span class="sxs-lookup"><span data-stu-id="f95ac-241">Properties window</span></span>
<span data-ttu-id="f95ac-242">속성 창은 모니터링 및 관리 앱의 가장 오른쪽 창에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-242">The Properties window is in the right-most pane of the Monitoring and Management app.</span></span>

![속성 창](./media/data-factory-monitor-manage-app/PropertiesWindow.png)

<span data-ttu-id="f95ac-244">리소스 탐색기(트리 뷰), 다이어그램 뷰 또는 활동 기간 목록에서 선택한 항목에 대한 속성이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-244">It displays properties for the item that you selected in the Resource Explorer (tree view), Diagram View, or Activity Windows list.</span></span>

### <a name="activity-window-explorer"></a><span data-ttu-id="f95ac-245">작업 창 탐색기</span><span class="sxs-lookup"><span data-stu-id="f95ac-245">Activity Window Explorer</span></span>
<span data-ttu-id="f95ac-246">**활동 기간 탐색기** 창은 모니터링 및 관리 앱의 가장 오른쪽 창에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-246">The **Activity Window Explorer** window is in the right-most pane of the Monitoring and Management app.</span></span> <span data-ttu-id="f95ac-247">활동 기간 팝업 또는 활동 기간 목록에 선택된 활동 기간에 대한 세부 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-247">It displays details about the activity window that you selected in the Activity Windows pop-up window or the Activity Windows list.</span></span>

![작업 창 탐색기](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-3.png)

<span data-ttu-id="f95ac-249">위쪽의 일정 보기에서 클릭하여 다른 작업 창으로 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-249">You can switch to another activity window by clicking it in the calendar view at the top.</span></span> <span data-ttu-id="f95ac-250">또한 위쪽에서 왼쪽 화살표/오른쪽 화살표 단추를 사용하여 이전 주/다음 주의 활동 기간을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-250">You can also use the left arrow/right arrow buttons at the top to see activity windows from the previous week or the next week.</span></span>

<span data-ttu-id="f95ac-251">아래쪽 창에서 도구 모음 단추를 사용하여 활동 기간을 다시 실행하거나 창의 세부 정보를 새로 고칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-251">You can use the toolbar buttons in the bottom pane to rerun the activity window or refresh the details in the pane.</span></span>

### <a name="script"></a><span data-ttu-id="f95ac-252">스크립트</span><span class="sxs-lookup"><span data-stu-id="f95ac-252">Script</span></span>
<span data-ttu-id="f95ac-253">**스크립트** 탭을 사용하여 선택한 Data Factory 엔터티(연결된 서비스, 데이터 집합 또는 파이프라인)의 JSON 정의를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-253">You can use the **Script** tab to view the JSON definition of the selected Data Factory entity (linked service, dataset, or pipeline).</span></span>

![스크립트 탭](./media/data-factory-monitor-manage-app/ScriptTab.png)

## <a name="use-system-views"></a><span data-ttu-id="f95ac-255">시스템 뷰 사용</span><span class="sxs-lookup"><span data-stu-id="f95ac-255">Use system views</span></span>
<span data-ttu-id="f95ac-256">모니터링 및 관리 앱은 데이터 팩터리에 대해 최근/실패한/진행 중인 활동 기간을 보여주는 미리 작성된 시스템 뷰를 포함합니다(**Recent activity windows**(최근 활동 기간), **Failed activity windows**(실패한 활동 기간), **In-Progress activity windows**(진행 중인 활동 기간)).</span><span class="sxs-lookup"><span data-stu-id="f95ac-256">The Monitoring and Management app includes pre-built system views (**Recent activity windows**, **Failed activity windows**, **In-Progress activity windows**) that allow you to view recent/failed/in-progress activity windows for your data factory.</span></span>

<span data-ttu-id="f95ac-257">왼쪽에서 **모니터링 뷰** 탭을 클릭하여 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-257">Switch to the **Monitoring Views** tab on the left by clicking it.</span></span>

![모니터링 뷰 탭](./media/data-factory-monitor-manage-app/MonitoringViewsTab.png)

<span data-ttu-id="f95ac-259">현재는 지원되는 세 가지 시스템 뷰가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-259">Currently, there are three system views that are supported.</span></span> <span data-ttu-id="f95ac-260">(가운데 창의 맨 아래에 있는)활동 기간 목록에서 최근 활동 기간, 실패한 활동 기간 또는 진행 중인 활동 기간을 보려면 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-260">Select an option to see recent activity windows, failed activity windows, or in-progress activity windows in the Activity Windows list (at the bottom of the middle pane).</span></span>

<span data-ttu-id="f95ac-261">**Recent activity windows**(최근 활동 기간) 옵션을 선택하면 **마지막 시도 시간**의 내림차순으로 최근 활동 기간이 모두 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-261">When you select the **Recent activity windows** option, you see all recent activity windows in descending order of the **last attempt time**.</span></span>

<span data-ttu-id="f95ac-262">**실패한 작업 창** 뷰를 사용하여 목록에서 실패한 작업 창을 모두 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-262">You can use the **Failed activity windows** view to see all failed activity windows in the list.</span></span> <span data-ttu-id="f95ac-263">**속성** 창 또는 **활동 기간 탐색기**에서 이에 대한 자세한 내용을 보려면 목록에서 실패한 활동 기간을 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="f95ac-263">Select a failed activity window in the list to see details about it in the **Properties** window or the **Activity Window Explorer**.</span></span> <span data-ttu-id="f95ac-264">또한 실패한 작업 창에 대한 로그를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-264">You can also download any logs for a failed activity window.</span></span>

## <a name="sort-and-filter-activity-windows"></a><span data-ttu-id="f95ac-265">활동 기간 정렬 및 필터링</span><span class="sxs-lookup"><span data-stu-id="f95ac-265">Sort and filter activity windows</span></span>
<span data-ttu-id="f95ac-266">명령 모음에서 **시작 시간** 및 **종료 시간** 설정을 변경하여 작업 창을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-266">Change the **start time** and **end time** settings in the command bar to filter activity windows.</span></span> <span data-ttu-id="f95ac-267">시작 시간 및 종료 시간을 변경한 후에 활동 기간 목록을 새로 고치려면 종료 시간 옆에 있는 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-267">After you change the start time and end time, click the button next to the end time to refresh the Activity Windows list.</span></span>

![시작 및 종료 시간](./media/data-factory-monitor-manage-app/StartAndEndTimes.png)

> [!NOTE]
> <span data-ttu-id="f95ac-269">현재 모니터링 및 관리 앱의 모든 시간은 UTC 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-269">Currently, all times are in UTC format in the Monitoring and Management app.</span></span>
>
>

<span data-ttu-id="f95ac-270">**작업 창 목록**에서 열의 이름을 클릭합니다(예: 상태).</span><span class="sxs-lookup"><span data-stu-id="f95ac-270">In the **Activity Windows list**, click the name of a column (for example: Status).</span></span>

![활동 기간 목록 열 메뉴](./media/data-factory-monitor-manage-app/ActivityWindowsListColumnMenu.png)

<span data-ttu-id="f95ac-272">다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-272">You can do the following:</span></span>

* <span data-ttu-id="f95ac-273">오름차순으로 정렬.</span><span class="sxs-lookup"><span data-stu-id="f95ac-273">Sort in ascending order.</span></span>
* <span data-ttu-id="f95ac-274">내림차순으로 정렬.</span><span class="sxs-lookup"><span data-stu-id="f95ac-274">Sort in descending order.</span></span>
* <span data-ttu-id="f95ac-275">하나 이상의 값으로 필터링(준비, 대기 중 등).</span><span class="sxs-lookup"><span data-stu-id="f95ac-275">Filter by one or more values (Ready, Waiting, and so on).</span></span>

<span data-ttu-id="f95ac-276">열에 필터를 지정할 때 해당 열에 대해 사용하도록 설정된 필터 단추가 표시되어 열의 값이 필터링된 값임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-276">When you specify a filter on a column, you see the filter button enabled for that column, which indicates that the values in the column are filtered values.</span></span>

![활동 기간 목록의 열에서 필터링](./media/data-factory-monitor-manage-app/ActivityWindowsListFilterInColumn.png)

<span data-ttu-id="f95ac-278">동일한 팝업 창을 사용하여 필터를 지울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-278">You can use the same pop-up window to clear filters.</span></span> <span data-ttu-id="f95ac-279">활동 기간 목록에 대한 필터를 모두 지우려면 명령 모음에서 필터 지우기 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-279">To clear all filters for the Activity Windows list, click the clear filter button on the command bar.</span></span>

![활동 기간 목록의 모든 필터 지우기](./media/data-factory-monitor-manage-app/ClearAllFiltersActivityWindowsList.png)

## <a name="perform-batch-actions"></a><span data-ttu-id="f95ac-281">배치 작업 수행</span><span class="sxs-lookup"><span data-stu-id="f95ac-281">Perform batch actions</span></span>
### <a name="rerun-selected-activity-windows"></a><span data-ttu-id="f95ac-282">선택한 작업 창 다시 실행</span><span class="sxs-lookup"><span data-stu-id="f95ac-282">Rerun selected activity windows</span></span>
<span data-ttu-id="f95ac-283">활동 기간을 선택하고 첫 번째 명령 모음 단추의 아래쪽 화살표를 클릭한 다음 **다시 실행** / **Rerun with upstream in pipeline**(파이프라인에서 업스트림으로 다시 실행)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-283">Select an activity window, click the down arrow for the first command bar button, and select **Rerun** / **Rerun with upstream in pipeline**.</span></span> <span data-ttu-id="f95ac-284">**Rerun with upstream in pipeline**(파이프라인에서 업스트림으로 다시 실행) 옵션을 선택하면 모든 업스트림 활동 기간이 다시 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-284">When you select the **Rerun with upstream in pipeline** option, it reruns all upstream activity windows as well.</span></span>
    <span data-ttu-id="f95ac-285">![작업 창 다시 실행](./media/data-factory-monitor-manage-app/ReRunSlice.png)</span><span class="sxs-lookup"><span data-stu-id="f95ac-285">![Rerun an activity window](./media/data-factory-monitor-manage-app/ReRunSlice.png)</span></span>

<span data-ttu-id="f95ac-286">또한 목록에서 여러 개의 작업 창을 선택하고 동시에 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-286">You can also select multiple activity windows in the list and rerun them at the same time.</span></span> <span data-ttu-id="f95ac-287">상태를 기준으로 활동 기간을 필터링(예: **실패**)한 다음, 활동 기간에 실패를 일으키는 문제를 해결한 후에 실패한 활동 기간을 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-287">You might want to filter activity windows based on the status (for example: **Failed**)--and then rerun the failed activity windows after correcting the issue that causes the activity windows to fail.</span></span> <span data-ttu-id="f95ac-288">목록에서 작업 창을 필터링하는 자세한 내용은 다음 섹션을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-288">See the following section for details about filtering activity windows in the list.</span></span>  

### <a name="pauseresume-multiple-pipelines"></a><span data-ttu-id="f95ac-289">여러 파이프라인 일시 중지/다시 시작</span><span class="sxs-lookup"><span data-stu-id="f95ac-289">Pause/resume multiple pipelines</span></span>
<span data-ttu-id="f95ac-290">Ctrl 키를 사용하여 두 개 이상의 파이프라인을 다중 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-290">You can multiselect two or more pipelines by using the Ctrl key.</span></span> <span data-ttu-id="f95ac-291">명령 모음 단추(아래 이미지에 빨간색 사각형으로 강조 표시됨)를 사용하여 일시 중지/다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-291">You can use the command bar buttons (which are highlighted in the red rectangle in the following image) to pause/resume them.</span></span>

![명령 모음에서 일시 중지/다시 시작](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)

## <a name="create-alerts"></a><span data-ttu-id="f95ac-293">경고 만들기</span><span class="sxs-lookup"><span data-stu-id="f95ac-293">Create alerts</span></span>
<span data-ttu-id="f95ac-294">**경고** 페이지에서 경고를 만들고 기존 경고를 보기/편집/삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-294">The **Alerts** page lets you create an alert and view/edit/delete existing alerts.</span></span> <span data-ttu-id="f95ac-295">또한 경고를 사용하지 않거나/사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-295">You can also disable/enable an alert.</span></span> <span data-ttu-id="f95ac-296">경고 페이지를 보려면 **경고** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-296">To see the Alerts page, click the **Alerts** tab.</span></span>

![경고 탭](./media/data-factory-monitor-manage-app/AlertsTab.png)

### <a name="to-create-an-alert"></a><span data-ttu-id="f95ac-298">경고를 만들려면</span><span class="sxs-lookup"><span data-stu-id="f95ac-298">To create an alert</span></span>
1. <span data-ttu-id="f95ac-299">**경고 추가** 를 클릭하여 경고를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-299">Click **Add Alert** to add an alert.</span></span> <span data-ttu-id="f95ac-300">**세부 정보** 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-300">You see the **Details** page.</span></span>

    ![경고 만들기 - 세부 정보 페이지](./media/data-factory-monitor-manage-app/CreateAlertDetailsPage.png)
2. <span data-ttu-id="f95ac-302">경고에 대한 **이름** 및 **설명**을 지정하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-302">Specify the **Name** and **Description** for the alert, and click **Next**.</span></span> <span data-ttu-id="f95ac-303">**필터** 페이지를 참조해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-303">You should see the **Filters** page.</span></span>

    ![경고 만들기 - 필터 페이지](./media/data-factory-monitor-manage-app/CreateAlertFiltersPage.png)
3. <span data-ttu-id="f95ac-305">Data Factory 서비스에서 경고를 보낼 **이벤트**, **상태** 및 **하위 상태**(선택 사항)를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-305">Select the **event**, **status**, and **substatus** (optional) that you want to create a Data Factory service alert for, and click **Next**.</span></span> <span data-ttu-id="f95ac-306">**받는 사람** 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-306">You should see the **Recipients** page.</span></span>

    ![경고 만들기 - 받는 사람 페이지](./media/data-factory-monitor-manage-app/CreateAlertRecipientsPage.png)
4. <span data-ttu-id="f95ac-308">**Email subscription admins**(전자 메일 구독 관리자) 옵션을 선택하거나 **additional administrator email**(추가 관리자 전자 메일)을 입력한 다음 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-308">Select the **Email subscription admins** option and/or enter an **additional administrator email**, and click **Finish**.</span></span> <span data-ttu-id="f95ac-309">목록에서 경고가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-309">You should see the alert in the list.</span></span>

    ![경고 목록](./media/data-factory-monitor-manage-app/AlertsList.png)

<span data-ttu-id="f95ac-311">경고 목록에서 경고와 관련된 단추를 사용하여 경고를 편집/삭제/비활성화/활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-311">In the Alerts list, use the buttons that are associated with the alert to edit/delete/disable/enable an alert.</span></span>

### <a name="eventstatussubstatus"></a><span data-ttu-id="f95ac-312">이벤트/상태/하위 상태</span><span class="sxs-lookup"><span data-stu-id="f95ac-312">Event/status/substatus</span></span>
<span data-ttu-id="f95ac-313">다음 테이블은 사용 가능한 이벤트 및 상태(및 하위 상태) 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-313">The following table provides the list of available events and statuses (and substatuses).</span></span>

| <span data-ttu-id="f95ac-314">이벤트 이름</span><span class="sxs-lookup"><span data-stu-id="f95ac-314">Event name</span></span> | <span data-ttu-id="f95ac-315">가동 상태</span><span class="sxs-lookup"><span data-stu-id="f95ac-315">Status</span></span> | <span data-ttu-id="f95ac-316">하위 상태</span><span class="sxs-lookup"><span data-stu-id="f95ac-316">Substatus</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f95ac-317">작업 실행 시작</span><span class="sxs-lookup"><span data-stu-id="f95ac-317">Activity Run Started</span></span> |<span data-ttu-id="f95ac-318">Started</span><span class="sxs-lookup"><span data-stu-id="f95ac-318">Started</span></span> |<span data-ttu-id="f95ac-319">시작 중</span><span class="sxs-lookup"><span data-stu-id="f95ac-319">Starting</span></span> |
| <span data-ttu-id="f95ac-320">작업 실행 완료</span><span class="sxs-lookup"><span data-stu-id="f95ac-320">Activity Run Finished</span></span> |<span data-ttu-id="f95ac-321">Succeeded</span><span class="sxs-lookup"><span data-stu-id="f95ac-321">Succeeded</span></span> |<span data-ttu-id="f95ac-322">Succeeded</span><span class="sxs-lookup"><span data-stu-id="f95ac-322">Succeeded</span></span> |
| <span data-ttu-id="f95ac-323">작업 실행 완료</span><span class="sxs-lookup"><span data-stu-id="f95ac-323">Activity Run Finished</span></span> |<span data-ttu-id="f95ac-324">실패</span><span class="sxs-lookup"><span data-stu-id="f95ac-324">Failed</span></span> |<span data-ttu-id="f95ac-325">실패한 리소스 할당</span><span class="sxs-lookup"><span data-stu-id="f95ac-325">Failed Resource Allocation</span></span><br/><br/><span data-ttu-id="f95ac-326">실패한 실행</span><span class="sxs-lookup"><span data-stu-id="f95ac-326">Failed Execution</span></span><br/><br/><span data-ttu-id="f95ac-327">Timed Out</span><span class="sxs-lookup"><span data-stu-id="f95ac-327">Timed Out</span></span><br/><br/><span data-ttu-id="f95ac-328">Failed Validation</span><span class="sxs-lookup"><span data-stu-id="f95ac-328">Failed Validation</span></span><br/><br/><span data-ttu-id="f95ac-329">Abandoned</span><span class="sxs-lookup"><span data-stu-id="f95ac-329">Abandoned</span></span> |
| <span data-ttu-id="f95ac-330">주문형 HDI 클러스터 만들기 시작</span><span class="sxs-lookup"><span data-stu-id="f95ac-330">On-Demand HDI Cluster Create Started</span></span> |<span data-ttu-id="f95ac-331">Started</span><span class="sxs-lookup"><span data-stu-id="f95ac-331">Started</span></span> |-|
| <span data-ttu-id="f95ac-332">주문형 HDI 클러스터 성공적으로 생성</span><span class="sxs-lookup"><span data-stu-id="f95ac-332">On-Demand HDI Cluster Created Successfully</span></span> |<span data-ttu-id="f95ac-333">Succeeded</span><span class="sxs-lookup"><span data-stu-id="f95ac-333">Succeeded</span></span> |-|
| <span data-ttu-id="f95ac-334">주문형 HDI 클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="f95ac-334">On-Demand HDI Cluster Deleted</span></span> |<span data-ttu-id="f95ac-335">Succeeded</span><span class="sxs-lookup"><span data-stu-id="f95ac-335">Succeeded</span></span> |-|

### <a name="to-edit-delete-or-disable-an-alert"></a><span data-ttu-id="f95ac-336">경고를 편집, 삭제 또는 비활성화하려면</span><span class="sxs-lookup"><span data-stu-id="f95ac-336">To edit, delete, or disable an alert</span></span>

<span data-ttu-id="f95ac-337">다음 단추(빨간색으로 강조 표시됨)를 사용하여 경고를 편집, 삭제 또는 비활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="f95ac-337">Use the following buttons (highlighted in red) to edit, delete, or disable an alert.</span></span>

![경고 단추](./media/data-factory-monitor-manage-app/AlertButtons.png)
