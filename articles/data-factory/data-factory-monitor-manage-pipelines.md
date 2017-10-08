---
title: "aaaMonitor hello Azure 포털 및 PowerShell을 사용 하 여 파이프라인을 관리할 | Microsoft Docs"
description: "Toouse Azure 포털 및 Azure PowerShell toomonitor hello 하 고 hello Azure 데이터 팩터리 및 사용자가 만든 파이프라인을 관리 하는 방법에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 9b0fdc59-5bbe-44d1-9ebc-8be14d44def9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: spelluru
ms.openlocfilehash: a8d3c7943e79450895ff754f06a37fdad1cbef92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-azure-portal-and-powershell"></a><span data-ttu-id="ff4cf-103">모니터링 하 고 hello Azure 포털 및 PowerShell을 사용 하 여 Azure 데이터 팩터리 파이프라인 관리</span><span class="sxs-lookup"><span data-stu-id="ff4cf-103">Monitor and manage Azure Data Factory pipelines by using hello Azure portal and PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ff4cf-104">Azure 포털/Azure PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="ff4cf-104">Using Azure portal/Azure PowerShell</span></span>](data-factory-monitor-manage-pipelines.md)
> * [<span data-ttu-id="ff4cf-105">모니터링 및 관리 앱 사용</span><span class="sxs-lookup"><span data-stu-id="ff4cf-105">Using Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)


> [!IMPORTANT]
> <span data-ttu-id="ff4cf-106">hello 모니터링 및 관리 응용 프로그램 모니터링 및 데이터 파이프라인, 관리 및 문제 해결에 대 한 더 나은 지원을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-106">hello monitoring & management application provides a better support for monitoring and managing your data pipelines, and troubleshooting any issues.</span></span> <span data-ttu-id="ff4cf-107">Hello 응용 프로그램을 사용 하는 방법에 대 한 세부 정보를 참조 하십시오. [모니터링 하 고 hello 모니터링 및 관리 앱을 사용 하 여 데이터 팩터리 파이프라인 관리](data-factory-monitor-manage-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-107">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span> 


<span data-ttu-id="ff4cf-108">이 문서에서는 toomonitor를 관리 하 고 Azure 포털 및 PowerShell을 사용 하 여 파이프라인을 디버깅 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-108">This article describes how toomonitor, manage, and debug your pipelines by using Azure portal and PowerShell.</span></span> <span data-ttu-id="ff4cf-109">hello 문서에 대 한 정보도 toocreate 경고 및 가져오기 방법을 실패에 대 한 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-109">hello article also provides information on how toocreate alerts and get notified about failures.</span></span>

## <a name="understand-pipelines-and-activity-states"></a><span data-ttu-id="ff4cf-110">파이프라인 및 작업 상태 이해</span><span class="sxs-lookup"><span data-stu-id="ff4cf-110">Understand pipelines and activity states</span></span>
<span data-ttu-id="ff4cf-111">Azure 포털 hello를 사용 하 여 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-111">By using hello Azure portal, you can:</span></span>

* <span data-ttu-id="ff4cf-112">데이터 팩터리를 다이어그램으로 보기</span><span class="sxs-lookup"><span data-stu-id="ff4cf-112">View your data factory as a diagram.</span></span>
* <span data-ttu-id="ff4cf-113">파이프라인에서 활동 보기</span><span class="sxs-lookup"><span data-stu-id="ff4cf-113">View activities in a pipeline.</span></span>
* <span data-ttu-id="ff4cf-114">입력 및 출력 데이터 집합 보기</span><span class="sxs-lookup"><span data-stu-id="ff4cf-114">View input and output datasets.</span></span>

<span data-ttu-id="ff4cf-115">이 섹션에서는 또한 데이터 집합 조각 상태 tooanother 상태에서 전환 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-115">This section also describes how a dataset slice transitions from one state tooanother state.</span></span>   

### <a name="navigate-tooyour-data-factory"></a><span data-ttu-id="ff4cf-116">데이터 팩터리 tooyour 이동</span><span class="sxs-lookup"><span data-stu-id="ff4cf-116">Navigate tooyour data factory</span></span>
1. <span data-ttu-id="ff4cf-117">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-117">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ff4cf-118">클릭 **데이터 팩터리** hello hello 왼쪽 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-118">Click **Data factories** on hello menu on hello left.</span></span> <span data-ttu-id="ff4cf-119">표시 되지 않는 경우 클릭 **더 많은 서비스 >**, 클릭 하 고 **데이터 팩터리** hello에서 **인텔리전스 + 분석** 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-119">If you don't see it, click **More services >**, and then click **Data factories** under hello **INTELLIGENCE + ANALYTICS** category.</span></span>

   ![모두 찾아보기 -> 데이터 팩터리](./media/data-factory-monitor-manage-pipelines/browseall-data-factories.png)
3. <span data-ttu-id="ff4cf-121">Hello에 **데이터 팩터리** 블레이드, 관심이 선택 hello 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-121">On hello **Data factories** blade, select hello data factory that you're interested in.</span></span>

    ![데이터 팩터리 선택](./media/data-factory-monitor-manage-pipelines/select-data-factory.png)

   <span data-ttu-id="ff4cf-123">Hello 데이터 팩토리에 대 한 hello 홈 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-123">You should see hello home page for hello data factory.</span></span>

   ![데이터 팩터리 블레이드](./media/data-factory-monitor-manage-pipelines/data-factory-blade.png)

#### <a name="diagram-view-of-your-data-factory"></a><span data-ttu-id="ff4cf-125">데이터 팩터리의 다이어그램 뷰</span><span class="sxs-lookup"><span data-stu-id="ff4cf-125">Diagram view of your data factory</span></span>
<span data-ttu-id="ff4cf-126">hello **다이어그램** 데이터 팩터리의 유리 toomonitor의 단일 창 제공 뷰와 hello data factory와 해당 자산을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-126">hello **Diagram** view of a data factory provides a single pane of glass toomonitor and manage hello data factory and its assets.</span></span> <span data-ttu-id="ff4cf-127">toosee hello **다이어그램** 데이터 팩터리의 보려면 클릭 하십시오. **다이어그램** hello 데이터 팩토리에 대 한 hello 홈 페이지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-127">toosee hello **Diagram** view of your data factory, click **Diagram** on hello home page for hello data factory.</span></span>

![다이어그램 뷰](./media/data-factory-monitor-manage-pipelines/diagram-view.png)

<span data-ttu-id="ff4cf-129">확대/축소 지정, 축소, 확대/축소 toofit, 확대/축소 too100%, hello 다이어그램의 잠금 hello 레이아웃 및 자동으로 파이프라인 및 데이터 집합 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-129">You can zoom in, zoom out, zoom toofit, zoom too100%, lock hello layout of hello diagram, and automatically position pipelines and datasets.</span></span> <span data-ttu-id="ff4cf-130">Hello 데이터 계보 정보를 볼 수 있습니다 (즉, 선택한 항목의 업스트림 및 다운스트림 항목 표시).</span><span class="sxs-lookup"><span data-stu-id="ff4cf-130">You can also see hello data lineage information (that is, show upstream and downstream items of selected items).</span></span>

### <a name="activities-inside-a-pipeline"></a><span data-ttu-id="ff4cf-131">파이프라인 내부의 활동</span><span class="sxs-lookup"><span data-stu-id="ff4cf-131">Activities inside a pipeline</span></span>
1. <span data-ttu-id="ff4cf-132">Hello 파이프라인을 마우스 오른쪽 단추로 누른 **열려 파이프라인** toosee hello 활동에 대 한 입력 및 출력 데이터 집합 함께 hello에서 모든 활동 파이프라인.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-132">Right-click hello pipeline, and then click **Open pipeline** toosee all activities in hello pipeline, along with input and output datasets for hello activities.</span></span> <span data-ttu-id="ff4cf-133">이 기능은 사용자 파이프라인에 둘 이상의 활동이 포함 되어 단일 파이프라인의 toounderstand hello operational 계보 않으려는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-133">This feature is useful when your pipeline includes more than one activity and you want toounderstand hello operational lineage of a single pipeline.</span></span>

    ![파이프라인 열기 메뉴](./media/data-factory-monitor-manage-pipelines/open-pipeline-menu.png)     
2. <span data-ttu-id="ff4cf-135">다음 예제는 hello, hello 파이프라인에 입력 및 출력의 복사 작업을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-135">In hello following example, you see a copy activity in hello pipeline with an input and an output.</span></span> 

    ![파이프라인 내부의 활동](./media/data-factory-monitor-manage-pipelines/activities-inside-pipeline.png)
3. <span data-ttu-id="ff4cf-137">Hello를 클릭 하 여 hello 데이터 팩터리의 백 toohello 홈 페이지를 탐색할 수 **Data factory** hello 왼쪽 위 모서리에 있는 이동 경로 탐색 hello에에서 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-137">You can navigate back toohello home page of hello data factory by clicking hello **Data factory** link in hello breadcrumb at hello top-left corner.</span></span>

    ![뒤로 toodata 공장 이동](./media/data-factory-monitor-manage-pipelines/navigate-back-to-data-factory.png)

### <a name="view-hello-state-of-each-activity-inside-a-pipeline"></a><span data-ttu-id="ff4cf-139">파이프라인 내 각 활동의 hello 상태 보기</span><span class="sxs-lookup"><span data-stu-id="ff4cf-139">View hello state of each activity inside a pipeline</span></span>
<span data-ttu-id="ff4cf-140">Hello 활동에 의해 생성 되는 hello 데이터 집합의 hello 상태를 확인 하 여 hello 활동의 현재 상태를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-140">You can view hello current state of an activity by viewing hello status of any of hello datasets that are produced by hello activity.</span></span>

<span data-ttu-id="ff4cf-141">Hello를 두 번 클릭 하 여 **OutputBlobTable** hello에 **다이어그램**, 파이프라인 내 다른 활동을 실행 하 여 생성 되는 모든 hello 분할 영역을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-141">By double-clicking hello **OutputBlobTable** in hello **Diagram**, you can see all hello slices that are produced by different activity runs inside a pipeline.</span></span> <span data-ttu-id="ff4cf-142">Hello 복사 활동 성공적으로 실행 hello에 대 한 마지막 8 시간 및 hello에서 hello 조각 생성 볼 수 있습니다 **준비** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-142">You can see that hello copy activity ran successfully for hello last eight hours and produced hello slices in hello **Ready** state.</span></span>  

![Hello 파이프라인의 상태](./media/data-factory-monitor-manage-pipelines/state-of-pipeline.png)

<span data-ttu-id="ff4cf-144">hello data factory에 hello 데이터 집합 분할 영역 hello 다음 상태 중 하나를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-144">hello dataset slices in hello data factory can have one of hello following statuses:</span></span>

<table>
<tr>
    <th align="left"><span data-ttu-id="ff4cf-145">시스템 상태</span><span class="sxs-lookup"><span data-stu-id="ff4cf-145">State</span></span></th><th align="left"><span data-ttu-id="ff4cf-146">하위 상태</span><span class="sxs-lookup"><span data-stu-id="ff4cf-146">Substate</span></span></th><th align="left"><span data-ttu-id="ff4cf-147">설명</span><span class="sxs-lookup"><span data-stu-id="ff4cf-147">Description</span></span></th>
</tr>
<tr>
    <td rowspan="8"><span data-ttu-id="ff4cf-148">대기</span><span class="sxs-lookup"><span data-stu-id="ff4cf-148">Waiting</span></span></td><td><span data-ttu-id="ff4cf-149">ScheduleTime</span><span class="sxs-lookup"><span data-stu-id="ff4cf-149">ScheduleTime</span></span></td><td><span data-ttu-id="ff4cf-150">hello에 조각 toorun hello에 대 한 대로 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-150">hello time hasn't come for hello slice toorun.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ff4cf-151">DatasetDependencies</span><span class="sxs-lookup"><span data-stu-id="ff4cf-151">DatasetDependencies</span></span></td><td><span data-ttu-id="ff4cf-152">업스트림 종속성 hello 준비 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-152">hello upstream dependencies aren't ready.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ff4cf-153">ComputeResources</span><span class="sxs-lookup"><span data-stu-id="ff4cf-153">ComputeResources</span></span></td><td><span data-ttu-id="ff4cf-154">hello 계산 리소스를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-154">hello compute resources aren't available.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ff4cf-155">ConcurrencyLimit</span><span class="sxs-lookup"><span data-stu-id="ff4cf-155">ConcurrencyLimit</span></span></td> <td><span data-ttu-id="ff4cf-156">모든 hello 활동 인스턴스는 다른 조각을 실행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-156">All hello activity instances are busy running other slices.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ff4cf-157">ActivityResume</span><span class="sxs-lookup"><span data-stu-id="ff4cf-157">ActivityResume</span></span></td><td><span data-ttu-id="ff4cf-158">hello 활동 일시 중지 되 고 hello 활동 재개 될 때까지 hello 분할 영역을 실행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-158">hello activity is paused and can't run hello slices until hello activity is resumed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ff4cf-159">Retry</span><span class="sxs-lookup"><span data-stu-id="ff4cf-159">Retry</span></span></td><td><span data-ttu-id="ff4cf-160">작업 실행을 다시 시도하는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-160">Activity execution is being retried.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ff4cf-161">유효성 검사</span><span class="sxs-lookup"><span data-stu-id="ff4cf-161">Validation</span></span></td><td><span data-ttu-id="ff4cf-162">유효성 검사가 아직 시작되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-162">Validation hasn't started yet.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ff4cf-163">ValidationRetry</span><span class="sxs-lookup"><span data-stu-id="ff4cf-163">ValidationRetry</span></span></td><td><span data-ttu-id="ff4cf-164">유효성 검사는 대기 중인 toobe 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-164">Validation is waiting toobe retried.</span></span></td>
</tr>
<tr>
<tr>
<td rowspan="2"><span data-ttu-id="ff4cf-165">InProgress</span><span class="sxs-lookup"><span data-stu-id="ff4cf-165">InProgress</span></span></td><td><span data-ttu-id="ff4cf-166">유효성 검사 중</span><span class="sxs-lookup"><span data-stu-id="ff4cf-166">Validating</span></span></td><td><span data-ttu-id="ff4cf-167">유효성 검사가 진행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-167">Validation is in progress.</span></span></td>
</tr>
<td>-</td>
<td><span data-ttu-id="ff4cf-168">hello 조각이 처리 중입니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-168">hello slice is being processed.</span></span></td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="ff4cf-169">실패</span><span class="sxs-lookup"><span data-stu-id="ff4cf-169">Failed</span></span></td><td><span data-ttu-id="ff4cf-170">TimedOut</span><span class="sxs-lookup"><span data-stu-id="ff4cf-170">TimedOut</span></span></td><td><span data-ttu-id="ff4cf-171">hello 활동 실행 hello 활동에 의해 허용 된 것 보다 더 오래 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-171">hello activity execution took longer than what is allowed by hello activity.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ff4cf-172">Canceled</span><span class="sxs-lookup"><span data-stu-id="ff4cf-172">Canceled</span></span></td><td><span data-ttu-id="ff4cf-173">hello 조각은 사용자 작업에 의해 취소 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-173">hello slice was canceled by user action.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ff4cf-174">유효성 검사</span><span class="sxs-lookup"><span data-stu-id="ff4cf-174">Validation</span></span></td><td><span data-ttu-id="ff4cf-175">유효성 검사가 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-175">Validation has failed.</span></span></td>
</tr>
<tr>
<td>-</td><td><span data-ttu-id="ff4cf-176">hello 조각 toobe 생성 및/또는 유효성을 검사 하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-176">hello slice failed toobe generated and/or validated.</span></span></td>
</tr>
<td><span data-ttu-id="ff4cf-177">Ready</span><span class="sxs-lookup"><span data-stu-id="ff4cf-177">Ready</span></span></td><td>-</td><td><span data-ttu-id="ff4cf-178">hello 조각이 소비에 대 한 준비 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-178">hello slice is ready for consumption.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ff4cf-179">생략</span><span class="sxs-lookup"><span data-stu-id="ff4cf-179">Skipped</span></span></td><td><span data-ttu-id="ff4cf-180">없음</span><span class="sxs-lookup"><span data-stu-id="ff4cf-180">None</span></span></td><td><span data-ttu-id="ff4cf-181">hello 조각을 처리 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-181">hello slice isn't being processed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ff4cf-182">없음</span><span class="sxs-lookup"><span data-stu-id="ff4cf-182">None</span></span></td><td>-</td><td><span data-ttu-id="ff4cf-183">분할 영역 tooexist 다른 상태와 함께 사용 되는 있지만 다시 설정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-183">A slice used tooexist with a different status, but it has been reset.</span></span></td>
</tr>
</table>



<span data-ttu-id="ff4cf-184">Hello에 분할 영역 항목을 클릭 하 여 분할 영역에 대 한 hello 세부 정보를 볼 수 있습니다 **최근에 업데이트 되는 분할 영역** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-184">You can view hello details about a slice by clicking a slice entry on hello **Recently Updated Slices** blade.</span></span>

![조각 세부 정보](./media/data-factory-monitor-manage-pipelines/slice-details.png)

<span data-ttu-id="ff4cf-186">Hello의 여러 행을 볼 hello 분할은 여러 번 실행 하는 경우 **활동 실행** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-186">If hello slice has been executed multiple times, you see multiple rows in hello **Activity runs** list.</span></span> <span data-ttu-id="ff4cf-187">Hello에 실행 하는 hello 항목을 클릭 하 여 실행 하는 작업에 대 한 정보를 볼 수 **활동 실행** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-187">You can view details about an activity run by clicking hello run entry in hello **Activity runs** list.</span></span> <span data-ttu-id="ff4cf-188">hello 목록에 있는 경우 오류 메시지와 함께 모든 hello 로그 파일 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-188">hello list shows all hello log files, along with an error message if there is one.</span></span> <span data-ttu-id="ff4cf-189">이 기능은 데이터 팩터리 tooleave 필요 없이 유용 tooview 및 디버그 로그에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-189">This feature is useful tooview and debug logs without having tooleave your data factory.</span></span>

![작업 실행 세부 정보](./media/data-factory-monitor-manage-pipelines/activity-run-details.png)

<span data-ttu-id="ff4cf-191">Hello 조각 hello에 없으면 **준비** 상태 hello 업스트림 슬라이스입니다. 준비 되지 않았습니다 hello 현재 조각 hello에서 실행할 수 없도록 차단 하 고 볼 수 있습니다 **준비 되지 않은 업스트림 슬라이스** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-191">If hello slice isn't in hello **Ready** state, you can see hello upstream slices that aren't ready and are blocking hello current slice from executing in hello **Upstream slices that are not ready** list.</span></span> <span data-ttu-id="ff4cf-192">에 조각의 경우이 기능은 유용 **대기** 상태를 하려면 toounderstand hello 업스트림 종속성을 조각 hello에서 대기 중입니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-192">This feature is useful when your slice is in **Waiting** state and you want toounderstand hello upstream dependencies that hello slice is waiting on.</span></span>

![준비되지 않은 업스트림 조각](./media/data-factory-monitor-manage-pipelines/upstream-slices-not-ready.png)

### <a name="dataset-state-diagram"></a><span data-ttu-id="ff4cf-194">데이터 집합 상태 다이어그램</span><span class="sxs-lookup"><span data-stu-id="ff4cf-194">Dataset state diagram</span></span>
<span data-ttu-id="ff4cf-195">데이터 팩터리를 배포한 후 hello 파이프라인에는 유효한 활성 기간이 hello 데이터 집합에서 하나의 상태 tooanother 전환을 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-195">After you deploy a data factory and hello pipelines have a valid active period, hello dataset slices transition from one state tooanother.</span></span> <span data-ttu-id="ff4cf-196">현재 hello 조각 상태 hello 상태 다이어그램 뒤를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-196">Currently, hello slice status follows hello following state diagram:</span></span>

![상태 다이어그램](./media/data-factory-monitor-manage-pipelines/state-diagram.png)

<span data-ttu-id="ff4cf-198">hello 데이터 집합 상태 전환 흐름이 data factory에는 hello 다음: 대기에서-진행률/진행 중 (Validating)-> 준비/실패->.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-198">hello dataset state transition flow in data factory is hello following: Waiting -> In-Progress/In-Progress (Validating) -> Ready/Failed.</span></span>

<span data-ttu-id="ff4cf-199">hello 조각의 시작는 **대기** 사전 조건 toobe 실행 하기 전에 충족에 대 한 대기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-199">hello slice starts in a **Waiting** state, waiting for preconditions toobe met before it executes.</span></span> <span data-ttu-id="ff4cf-200">그런 다음 hello 활동이 실행을 시작 하 고 hello 조각 전환 되는 **진행 중인** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-200">Then, hello activity starts executing, and hello slice goes into an **In-Progress** state.</span></span> <span data-ttu-id="ff4cf-201">hello 활동 실행 성공 하거나 실패 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-201">hello activity execution might succeed or fail.</span></span> <span data-ttu-id="ff4cf-202">hello 조각으로 표시 되어 **준비** 또는 **실패**hello hello 실행 결과에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-202">hello slice is marked as **Ready** or **Failed**, based on hello result of hello execution.</span></span>

<span data-ttu-id="ff4cf-203">Hello에서 다시 분할 영역 toogo hello를 다시 설정할 수 있습니다 **준비** 또는 **실패** 상태 toohello **대기** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-203">You can reset hello slice toogo back from hello **Ready** or **Failed** state toohello **Waiting** state.</span></span> <span data-ttu-id="ff4cf-204">표시할 수도 있습니다 hello 조각 상태 너무**Skip**, hello 활동을 실행 하 고 hello 분할 영역을 처리 하지 않고 방지 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-204">You can also mark hello slice state too**Skip**, which prevents hello activity from executing and not processing hello slice.</span></span>

## <a name="pause-and-resume-pipelines"></a><span data-ttu-id="ff4cf-205">파이프라인 일시 중지 및 다시 시작</span><span class="sxs-lookup"><span data-stu-id="ff4cf-205">Pause and resume pipelines</span></span>
<span data-ttu-id="ff4cf-206">Azure PowerShell을 사용하여 파이프라인을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-206">You can manage your pipelines by using Azure PowerShell.</span></span> <span data-ttu-id="ff4cf-207">예를 들어 Azure PowerShell cmdlet을 실행하여 파이프라인을 일시 중지하거나 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-207">For example, you can pause and resume pipelines by running Azure PowerShell cmdlets.</span></span> 

> [!NOTE] 
> <span data-ttu-id="ff4cf-208">일시 중지 및 재개 파이프라인 hello 다이어그램 보기를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-208">hello diagram view does not support pausing and resuming pipelines.</span></span> <span data-ttu-id="ff4cf-209">Toouse 사용자 인터페이스를 원하는 경우 hello 모니터링 하 고 응용 프로그램 관리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-209">If you want toouse an user interface, use hello monitoring and managing application.</span></span> <span data-ttu-id="ff4cf-210">Hello 응용 프로그램을 사용 하는 방법에 대 한 세부 정보를 참조 하십시오. [모니터링 하 고 hello 모니터링 및 관리 앱을 사용 하 여 데이터 팩터리 파이프라인 관리](data-factory-monitor-manage-app.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-210">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md) article.</span></span> 

<span data-ttu-id="ff4cf-211">일시 중지/일시 중지 하 파이프라인 hello를 사용 하 여 **Suspend AzureRmDataFactoryPipeline** PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-211">You can pause/suspend pipelines by using hello **Suspend-AzureRmDataFactoryPipeline** PowerShell cmdlet.</span></span> <span data-ttu-id="ff4cf-212">이 cmdlet은 하지 않으려면 toorun 파이프라인 문제가 해결 될 때까지 하는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-212">This cmdlet is useful when you don’t want toorun your pipelines until an issue is fixed.</span></span> 

```powershell
Suspend-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
<span data-ttu-id="ff4cf-213">예:</span><span class="sxs-lookup"><span data-stu-id="ff4cf-213">For example:</span></span>

```powershell
Suspend-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

<span data-ttu-id="ff4cf-214">Hello 파이프라인과 hello 문제를 해결 후 일시 중단 하는 hello 파이프라인 hello 다음 PowerShell 명령을 실행 하 여 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-214">After hello issue has been fixed with hello pipeline, you can resume hello suspended pipeline by running hello following PowerShell command:</span></span>

```powershell
Resume-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
<span data-ttu-id="ff4cf-215">예:</span><span class="sxs-lookup"><span data-stu-id="ff4cf-215">For example:</span></span>

```powershell
Resume-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

## <a name="debug-pipelines"></a><span data-ttu-id="ff4cf-216">파이프라인 디버깅</span><span class="sxs-lookup"><span data-stu-id="ff4cf-216">Debug pipelines</span></span>
<span data-ttu-id="ff4cf-217">Azure Data Factory toodebug 있습니다에 대 한 다양 한 기능을 제공 하 고 hello Azure 포털 및 Azure PowerShell을 사용 하 여 파이프라인을 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-217">Azure Data Factory provides rich capabilities for you toodebug and troubleshoot pipelines by using hello Azure portal and Azure PowerShell.</span></span>

> <span data-ttu-id="ff4cf-218">[! NOTE}는 훨씬 더 쉽게 사용 하 여 오류 모니터링 hello tootroubleshot & 관리 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-218">[!NOTE} It is much easier tootroubleshot errors using hello Monitoring & Management App.</span></span> <span data-ttu-id="ff4cf-219">Hello 응용 프로그램을 사용 하는 방법에 대 한 세부 정보를 참조 하십시오. [모니터링 하 고 hello 모니터링 및 관리 앱을 사용 하 여 데이터 팩터리 파이프라인 관리](data-factory-monitor-manage-app.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-219">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md) article.</span></span> 

### <a name="find-errors-in-a-pipeline"></a><span data-ttu-id="ff4cf-220">파이프라인에서 오류 찾기</span><span class="sxs-lookup"><span data-stu-id="ff4cf-220">Find errors in a pipeline</span></span>
<span data-ttu-id="ff4cf-221">파이프라인에서 실패 하면 hello 활동 실행 hello hello 파이프라인에 의해 생성 되는 데이터 집합이 오류 상태에 hello 오류로 인해 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-221">If hello activity run fails in a pipeline, hello dataset that is produced by hello pipeline is in an error state because of hello failure.</span></span> <span data-ttu-id="ff4cf-222">디버깅할 수 있으며 hello 다음 메서드를 사용 하 여 Azure Data Factory의 오류를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-222">You can debug and troubleshoot errors in Azure Data Factory by using hello following methods.</span></span>

#### <a name="use-hello-azure-portal-toodebug-an-error"></a><span data-ttu-id="ff4cf-223">Azure 포털 toodebug 오류가 hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="ff4cf-223">Use hello Azure portal toodebug an error</span></span>
1. <span data-ttu-id="ff4cf-224">Hello에 **테이블** 블레이드에서 hello 있는 hello 문제 조각을 클릭 **상태** 도**실패**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-224">On hello **Table** blade, click hello problem slice that has hello **Status** set too**Failed**.</span></span>

   ![문제 조각이 있는 테이블 블레이드](./media/data-factory-monitor-manage-pipelines/table-blade-with-error.png)
2. <span data-ttu-id="ff4cf-226">Hello에 **데이터 조각을** 블레이드에서 hello 작업에 실패 한 실행을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-226">On hello **Data slice** blade, click hello activity run that failed.</span></span>

   ![오류가 있는 데이터 조각](./media/data-factory-monitor-manage-pipelines/dataslice-with-error.png)
3. <span data-ttu-id="ff4cf-228">Hello에 **활동 실행 정보** 블레이드에서 hello HDInsight 처리와 연결 된 hello 파일을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-228">On hello **Activity run details** blade, you can download hello files that are associated with hello HDInsight processing.</span></span> <span data-ttu-id="ff4cf-229">클릭 **다운로드** 상태/stderr toodownload hello 오류 로그 파일에 대 한 hello 오류에 대 한 세부 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-229">Click **Download** for Status/stderr toodownload hello error log file that contains details about hello error.</span></span>

   ![오류가 있는 작업 실행 세부 정보 블레이드 ](./media/data-factory-monitor-manage-pipelines/activity-run-details-with-error.png)     

#### <a name="use-powershell-toodebug-an-error"></a><span data-ttu-id="ff4cf-231">PowerShell toodebug 오류를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="ff4cf-231">Use PowerShell toodebug an error</span></span>
1. <span data-ttu-id="ff4cf-232">**PowerShell**을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-232">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="ff4cf-233">Hello 실행 **Get AzureRmDataFactorySlice** toosee hello 조각 및 해당 상태 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-233">Run hello **Get-AzureRmDataFactorySlice** command toosee hello slices and their statuses.</span></span> <span data-ttu-id="ff4cf-234">조각을 hello 상태와 함께 표시 되어야 **실패**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-234">You should see a slice with hello status of **Failed**.</span></span>        

    ```powershell   
    Get-AzureRmDataFactorySlice [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime] <DateTime> [[-EndDateTime] <DateTime> ] [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```   
   <span data-ttu-id="ff4cf-235">예:</span><span class="sxs-lookup"><span data-stu-id="ff4cf-235">For example:</span></span>

    ```powershell   
    Get-AzureRmDataFactorySlice -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime 2014-05-04 20:00:00
    ```

   <span data-ttu-id="ff4cf-236">**StartDateTime**을 파이프라인의 시작 시간으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-236">Replace **StartDateTime** with start time of your pipeline.</span></span> 
3. <span data-ttu-id="ff4cf-237">이제 hello 실행 **Get AzureRmDataFactoryRun** hello 조각에 대 한 hello 활동에 대 한 cmdlet tooget 세부 정보를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-237">Now, run hello **Get-AzureRmDataFactoryRun** cmdlet tooget details about hello activity run for hello slice.</span></span>

    ```powershell   
    Get-AzureRmDataFactoryRun [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime]
    <DateTime> [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```

    <span data-ttu-id="ff4cf-238">예:</span><span class="sxs-lookup"><span data-stu-id="ff4cf-238">For example:</span></span>

    ```powershell   
    Get-AzureRmDataFactoryRun -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime "5/5/2014 12:00:00 AM"
    ```

    <span data-ttu-id="ff4cf-239">StartDateTime hello 값은 hello 이전 단계에서 기록해 놓은 hello 오류/문제가 조각에 대 한 hello 시작 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-239">hello value of StartDateTime is hello start time for hello error/problem slice that you noted from hello previous step.</span></span> <span data-ttu-id="ff4cf-240">hello 날짜 및 시간을 큰따옴표로 묶어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-240">hello date-time should be enclosed in double quotes.</span></span>
4. <span data-ttu-id="ff4cf-241">Toohello 다음과 비슷한 hello 오류에 대 한 세부 정보를 사용 하 여 출력을 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-241">You should see output with details about hello error that is similar toohello following:</span></span>

    ```   
    Id                      : 841b77c9-d56c-48d1-99a3-8c16c3e77d39
    ResourceGroupName       : ADF
    DataFactoryName         : LogProcessingFactory3
    DatasetName               : EnrichedGameEventsTable
    ProcessingStartTime     : 10/10/2014 3:04:52 AM
    ProcessingEndTime       : 10/10/2014 3:06:49 AM
    PercentComplete         : 0
    DataSliceStart          : 5/5/2014 12:00:00 AM
    DataSliceEnd            : 5/6/2014 12:00:00 AM
    Status                  : FailedExecution
    Timestamp               : 10/10/2014 3:04:52 AM
    RetryAttempt            : 0
    Properties              : {}
    ErrorMessage            : Pig script failed with exit code '5'. See wasb://        adfjobs@spestore.blob.core.windows.net/PigQuery
                                    Jobs/841b77c9-d56c-48d1-99a3-
                8c16c3e77d39/10_10_2014_03_04_53_277/Status/stderr' for
                more details.
    ActivityName            : PigEnrichLogs
    PipelineName            : EnrichGameLogsPipeline
    Type                    :
    ```
5. <span data-ttu-id="ff4cf-242">Hello를 실행할 수 있습니다 **저장 AzureRmDataFactoryLog** hello hello 출력에서 참조 하 고 hello를 사용 하 여 hello 로그 파일을 다운로드 하는 Id 값을 사용 하 여 cmdlet **-DownloadLogsoption** hello cmdlet에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-242">You can run hello **Save-AzureRmDataFactoryLog** cmdlet with hello Id value that you see from hello output, and download hello log files by using hello **-DownloadLogsoption** for hello cmdlet.</span></span>

    ```powershell
    Save-AzureRmDataFactoryLog -ResourceGroupName "ADF" -DataFactoryName "LogProcessingFactory" -Id "841b77c9-d56c-48d1-99a3-8c16c3e77d39" -DownloadLogs -Output "C:\Test"
    ```

## <a name="rerun-failures-in-a-pipeline"></a><span data-ttu-id="ff4cf-243">파이프라인에서 실패한 항목 다시 실행</span><span class="sxs-lookup"><span data-stu-id="ff4cf-243">Rerun failures in a pipeline</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff4cf-244">보다 쉽게 tootroubleshoot 오류 및 사용 하 여 실패 한 조각을 다시 실행된 hello 모니터링 및 관리 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-244">It's easier tootroubleshoot errors and rerun failed slices by using hello Monitoring & Management App.</span></span> <span data-ttu-id="ff4cf-245">Hello 응용 프로그램을 사용 하는 방법에 대 한 세부 정보를 참조 하십시오. [모니터링 하 고 hello 모니터링 및 관리 앱을 사용 하 여 데이터 팩터리 파이프라인 관리](data-factory-monitor-manage-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-245">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span> 

### <a name="use-hello-azure-portal"></a><span data-ttu-id="ff4cf-246">Hello Azure 포털을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="ff4cf-246">Use hello Azure portal</span></span>
<span data-ttu-id="ff4cf-247">오류를 다시 실행할 수 toohello 오류 조각을 이동한 hello를 클릭 하 여 문제를 해결 하 고 파이프라인에서 오류가 발생 했습니다. 디버깅 후 **실행** hello 명령 모음에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-247">After you troubleshoot and debug failures in a pipeline, you can rerun failures by navigating toohello error slice and clicking hello **Run** button on hello command bar.</span></span>

![실패한 조각 다시 실행](./media/data-factory-monitor-manage-pipelines/rerun-slice.png)

<span data-ttu-id="ff4cf-249">경우에 hello 분할 영역에 유효성 검사 오류로 인해 실패 정책 (예를 들어 데이터 사용할 수 없는 경우), hello 오류를 수정 하 고 hello를 클릭 하 여 다시 유효성을 검사할 수 있습니다 **유효성 검사** hello 명령 모음에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-249">In case hello slice has failed validation because of a policy failure (for example, if data isn't available), you can fix hello failure and validate again by clicking hello **Validate** button on hello command bar.</span></span>

![오류 수정 및 유효성 검사](./media/data-factory-monitor-manage-pipelines/fix-error-and-validate.png)

### <a name="use-azure-powershell"></a><span data-ttu-id="ff4cf-251">Azure PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="ff4cf-251">Use Azure PowerShell</span></span>
<span data-ttu-id="ff4cf-252">Hello를 사용 하 여 오류를 다시 실행할 수 있습니다 **집합 AzureRmDataFactorySliceStatus** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-252">You can rerun failures by using hello **Set-AzureRmDataFactorySliceStatus** cmdlet.</span></span> <span data-ttu-id="ff4cf-253">Hello 참조 [집합 AzureRmDataFactorySliceStatus](https://msdn.microsoft.com/library/mt603522.aspx) 구문과 hello cmdlet에 대 한 기타 세부 정보에 대 한 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-253">See hello [Set-AzureRmDataFactorySliceStatus](https://msdn.microsoft.com/library/mt603522.aspx) topic for syntax and other details about hello cmdlet.</span></span>

<span data-ttu-id="ff4cf-254">**예제:**</span><span class="sxs-lookup"><span data-stu-id="ff4cf-254">**Example:**</span></span>

<span data-ttu-id="ff4cf-255">hello 다음 설정 하는 예제 테이블 'DAWikiAggregatedData' too'Waiting hello에 대 한 모든 분할 영역의 hello 상태 ' hello Azure 데이터 팩터리에서 'WikiADF'.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-255">hello following example sets hello status of all slices for hello table 'DAWikiAggregatedData' too'Waiting' in hello Azure data factory 'WikiADF'.</span></span>

<span data-ttu-id="ff4cf-256">'업데이트 유형' hello too'UpstreamInPipeline 설정 ', 즉, hello 테이블에 대 한 각 조각과 모든 hello 종속 (업스트림) 테이블의 상태 too'Waiting를 설정 하 는'.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-256">hello 'UpdateType' is set too'UpstreamInPipeline', which means that statuses of each slice for hello table and all hello dependent (upstream) tables are set too'Waiting'.</span></span> <span data-ttu-id="ff4cf-257">이 매개 변수는 '개별'에 대 한 다른 가능한 값을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-257">hello other possible value for this parameter is 'Individual'.</span></span>

```powershell
Set-AzureRmDataFactorySliceStatus -ResourceGroupName ADF -DataFactoryName WikiADF -DatasetName DAWikiAggregatedData -Status Waiting -UpdateType UpstreamInPipeline -StartDateTime 2014-05-21T16:00:00 -EndDateTime 2014-05-21T20:00:00
```

## <a name="create-alerts"></a><span data-ttu-id="ff4cf-258">경고 만들기</span><span class="sxs-lookup"><span data-stu-id="ff4cf-258">Create alerts</span></span>
<span data-ttu-id="ff4cf-259">Azure는 Azure 리소스(예: 데이터 팩터리)가 생성, 업데이트 또는 삭제될 때 사용자 이벤트를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-259">Azure logs user events when an Azure resource (for example, a data factory) is created, updated, or deleted.</span></span> <span data-ttu-id="ff4cf-260">이러한 이벤트에 경고를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-260">You can create alerts on these events.</span></span> <span data-ttu-id="ff4cf-261">Data Factory toocapture 다양 한 메트릭을 사용 하 여 및 메트릭에 대해 경고를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-261">You can use Data Factory toocapture various metrics and create alerts on metrics.</span></span> <span data-ttu-id="ff4cf-262">실시간 모니터링을 위한 이벤트와 기록을 목적으로 하는 메트릭을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-262">We recommend that you use events for real-time monitoring and use metrics for historical purposes.</span></span>

### <a name="alerts-on-events"></a><span data-ttu-id="ff4cf-263">이벤트에 대한 경고</span><span class="sxs-lookup"><span data-stu-id="ff4cf-263">Alerts on events</span></span>
<span data-ttu-id="ff4cf-264">Azure 이벤트는 Azure 리소스에서 일어나는 일에 대한 유용한 통찰력을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-264">Azure events provide useful insights into what is happening in your Azure resources.</span></span> <span data-ttu-id="ff4cf-265">Azure Data Factory를 사용하면 다음 경우에 이벤트가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-265">When you're using Azure Data Factory, events are generated when:</span></span>

* <span data-ttu-id="ff4cf-266">데이터 팩터리가 생성, 업데이트 또는 삭제될 때</span><span class="sxs-lookup"><span data-stu-id="ff4cf-266">A data factory is created, updated, or deleted.</span></span>
* <span data-ttu-id="ff4cf-267">데이터 처리("실행")가 시작/완료될 때</span><span class="sxs-lookup"><span data-stu-id="ff4cf-267">Data processing (as "runs") has started or completed.</span></span>
* <span data-ttu-id="ff4cf-268">주문형 HDInsight 클러스터가 생성 또는 제거될 때</span><span class="sxs-lookup"><span data-stu-id="ff4cf-268">An on-demand HDInsight cluster is created or removed.</span></span>

<span data-ttu-id="ff4cf-269">이러한 사용자 이벤트에 경고를 만들 수 있으며 toosend 전자 메일 알림 toohello 관리자 및 coadministrators hello 구독을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-269">You can create alerts on these user events and configure them toosend email notifications toohello administrator and coadministrators of hello subscription.</span></span> <span data-ttu-id="ff4cf-270">또한 hello 조건이 충족 되 면 전자 메일 알림을 tooreceive 해야 하는 사용자의 추가 전자 메일 주소를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-270">In addition, you can specify additional email addresses of users who need tooreceive email notifications when hello conditions are met.</span></span> <span data-ttu-id="ff4cf-271">이 기능은 실패에 대 한 알림 tooget을 데이터 팩터리 toocontinuously 모니터 않을 때 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-271">This feature is useful when you want tooget notified on failures and don’t want toocontinuously monitor your data factory.</span></span>

> [!NOTE]
> <span data-ttu-id="ff4cf-272">현재 hello 포털 이벤트에 대해 경고를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-272">Currently, hello portal doesn't show alerts on events.</span></span> <span data-ttu-id="ff4cf-273">사용 하 여 hello [모니터링 및 관리 앱](data-factory-monitor-manage-app.md) toosee 모든 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-273">Use hello [Monitoring and Management app](data-factory-monitor-manage-app.md) toosee all alerts.</span></span>


#### <a name="specify-an-alert-definition"></a><span data-ttu-id="ff4cf-274">경고 정의 지정:</span><span class="sxs-lookup"><span data-stu-id="ff4cf-274">Specify an alert definition</span></span>
<span data-ttu-id="ff4cf-275">toospecify 경고 정의 hello 작업에서 알림을 받는 toobe을 설명 하는 JSON 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-275">toospecify an alert definition, you create a JSON file that describes hello operations that you want toobe alerted on.</span></span> <span data-ttu-id="ff4cf-276">다음 예제는 hello, hello 경고 hello RunFinished 작업에 대 한 전자 메일 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-276">In hello following example, hello alert sends an email notification for hello RunFinished operation.</span></span> <span data-ttu-id="ff4cf-277">특정 toobe, hello 데이터 팩터리에서 실행 완료 된 후에 실행 하는 hello 실패 하는 경우 전자 메일 알림이 전송 됩니다 (상태 = FailedExecution).</span><span class="sxs-lookup"><span data-stu-id="ff4cf-277">toobe specific, an email notification is sent when a run in hello data factory has completed and hello run has failed (Status = FailedExecution).</span></span>

```JSON
{
    "contentVersion": "1.0.0.0",
     "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters": {},
    "resources":
    [
        {
            "name": "ADFAlertsSlice",
            "type": "microsoft.insights/alertrules",
            "apiVersion": "2014-04-01",
            "location": "East US",
            "properties":
            {
                "name": "ADFAlertsSlice",
                "description": "One or more of hello data slices for hello Azure Data Factory has failed processing.",
                "isEnabled": true,
                "condition":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.ManagementEventRuleCondition",
                    "dataSource":
                    {
                        "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleManagementEventDataSource",
                        "operationName": "RunFinished",
                        "status": "Failed",
                        "subStatus": "FailedExecution"   
                    }
                },
                "action":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails": [ "<your alias>@contoso.com" ]
                }
            }
        }
    ]
}
```

<span data-ttu-id="ff4cf-278">제거할 수 있습니다 **하위 상태** hello toobe 특정 오류에서 경고를 표시 하지 않으려면 JSON 정의에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-278">You can remove **subStatus** from hello JSON definition if you don’t want toobe alerted on a specific failure.</span></span>

<span data-ttu-id="ff4cf-279">이 예제에서는 구독에서 모든 데이터 팩터리에 hello 경고를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-279">This example sets up hello alert for all data factories in your subscription.</span></span> <span data-ttu-id="ff4cf-280">데이터 팩터리를 지정할 수 hello 경고 toobe 특정 데이터 팩터리에 대 한 설정 하려는 경우 **resourceUri** hello에 **dataSource**:</span><span class="sxs-lookup"><span data-stu-id="ff4cf-280">If you want hello alert toobe set up for a particular data factory, you can specify data factory **resourceUri** in hello **dataSource**:</span></span>

```JSON
"resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>"
```

<span data-ttu-id="ff4cf-281">hello 다음 표에서 hello 목록이 사용 가능한 작업 및 상태 (및 하위 상태).</span><span class="sxs-lookup"><span data-stu-id="ff4cf-281">hello following table provides hello list of available operations and statuses (and substatuses).</span></span>

| <span data-ttu-id="ff4cf-282">작업 이름</span><span class="sxs-lookup"><span data-stu-id="ff4cf-282">Operation name</span></span> | <span data-ttu-id="ff4cf-283">가동 상태</span><span class="sxs-lookup"><span data-stu-id="ff4cf-283">Status</span></span> | <span data-ttu-id="ff4cf-284">하위 상태</span><span class="sxs-lookup"><span data-stu-id="ff4cf-284">Substatus</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ff4cf-285">RunStarted</span><span class="sxs-lookup"><span data-stu-id="ff4cf-285">RunStarted</span></span> |<span data-ttu-id="ff4cf-286">Started</span><span class="sxs-lookup"><span data-stu-id="ff4cf-286">Started</span></span> |<span data-ttu-id="ff4cf-287">Starting</span><span class="sxs-lookup"><span data-stu-id="ff4cf-287">Starting</span></span> |
| <span data-ttu-id="ff4cf-288">RunFinished</span><span class="sxs-lookup"><span data-stu-id="ff4cf-288">RunFinished</span></span> |<span data-ttu-id="ff4cf-289">Failed / Succeeded</span><span class="sxs-lookup"><span data-stu-id="ff4cf-289">Failed / Succeeded</span></span> |<span data-ttu-id="ff4cf-290">FailedResourceAllocation</span><span class="sxs-lookup"><span data-stu-id="ff4cf-290">FailedResourceAllocation</span></span><br/><br/><span data-ttu-id="ff4cf-291">Succeeded</span><span class="sxs-lookup"><span data-stu-id="ff4cf-291">Succeeded</span></span><br/><br/><span data-ttu-id="ff4cf-292">FailedExecution</span><span class="sxs-lookup"><span data-stu-id="ff4cf-292">FailedExecution</span></span><br/><br/><span data-ttu-id="ff4cf-293">TimedOut</span><span class="sxs-lookup"><span data-stu-id="ff4cf-293">TimedOut</span></span><br/><br/><span data-ttu-id="ff4cf-294"><Canceled</span><span class="sxs-lookup"><span data-stu-id="ff4cf-294"><Canceled</span></span><br/><br/><span data-ttu-id="ff4cf-295">FailedValidation</span><span class="sxs-lookup"><span data-stu-id="ff4cf-295">FailedValidation</span></span><br/><br/><span data-ttu-id="ff4cf-296">Abandoned</span><span class="sxs-lookup"><span data-stu-id="ff4cf-296">Abandoned</span></span> |
| <span data-ttu-id="ff4cf-297">OnDemandClusterCreateStarted</span><span class="sxs-lookup"><span data-stu-id="ff4cf-297">OnDemandClusterCreateStarted</span></span> |<span data-ttu-id="ff4cf-298">Started</span><span class="sxs-lookup"><span data-stu-id="ff4cf-298">Started</span></span> | |
| <span data-ttu-id="ff4cf-299">OnDemandClusterCreateSuccessful</span><span class="sxs-lookup"><span data-stu-id="ff4cf-299">OnDemandClusterCreateSuccessful</span></span> |<span data-ttu-id="ff4cf-300">Succeeded</span><span class="sxs-lookup"><span data-stu-id="ff4cf-300">Succeeded</span></span> | |
| <span data-ttu-id="ff4cf-301">OnDemandClusterDeleted</span><span class="sxs-lookup"><span data-stu-id="ff4cf-301">OnDemandClusterDeleted</span></span> |<span data-ttu-id="ff4cf-302">Succeeded</span><span class="sxs-lookup"><span data-stu-id="ff4cf-302">Succeeded</span></span> | |

<span data-ttu-id="ff4cf-303">참조 [경고 규칙 만들기](https://msdn.microsoft.com/library/azure/dn510366.aspx) hello 예제에 사용 되는 hello JSON 요소에 대 한 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-303">See [Create Alert Rule](https://msdn.microsoft.com/library/azure/dn510366.aspx) for details about hello JSON elements that are used in hello example.</span></span>

#### <a name="deploy-hello-alert"></a><span data-ttu-id="ff4cf-304">Hello 경고를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-304">Deploy hello alert</span></span>
<span data-ttu-id="ff4cf-305">toodeploy hello 경고를 사용 하 여 hello Azure PowerShell cmdlet **새로 AzureRmResourceGroupDeployment**hello 다음 예제에에서 나온 것 처럼:</span><span class="sxs-lookup"><span data-stu-id="ff4cf-305">toodeploy hello alert, use hello Azure PowerShell cmdlet **New-AzureRmResourceGroupDeployment**, as shown in hello following example:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\ADFAlertFailedSlice.json  
```

<span data-ttu-id="ff4cf-306">리소스 그룹 배포 hello 성공적으로 완료 되 면 hello 메시지에 따라 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-306">After hello resource group deployment has finished successfully, you see hello following messages:</span></span>

```
VERBOSE: 7:00:48 PM - Template is valid.
WARNING: 7:00:48 PM - hello StorageAccountName parameter is no longer used and will be removed in a future release.
Please update scripts tooremove this parameter.
VERBOSE: 7:00:49 PM - Create template deployment 'ADFAlertFailedSlice'.
VERBOSE: 7:00:57 PM - Resource microsoft.insights/alertrules 'ADFAlertsSlice' provisioning status is succeeded

DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

> [!NOTE]
> <span data-ttu-id="ff4cf-307">Hello를 사용할 수 있습니다 [경고 규칙 만들기](https://msdn.microsoft.com/library/azure/dn510366.aspx) REST API toocreate 경고 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-307">You can use hello [Create Alert Rule](https://msdn.microsoft.com/library/azure/dn510366.aspx) REST API toocreate an alert rule.</span></span> <span data-ttu-id="ff4cf-308">hello JSON 페이로드는 비슷한 toohello JSON의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-308">hello JSON payload is similar toohello JSON example.</span></span>  


#### <a name="retrieve-hello-list-of-azure-resource-group-deployments"></a><span data-ttu-id="ff4cf-309">Azure 리소스 그룹 배포의 hello 목록 검색</span><span class="sxs-lookup"><span data-stu-id="ff4cf-309">Retrieve hello list of Azure resource group deployments</span></span>
<span data-ttu-id="ff4cf-310">hello cmdlet을 사용 하 여의 Azure 리소스 그룹 배포를 배포 하는 tooretrieve hello 목록이 **Get AzureRmResourceGroupDeployment**hello 다음 예제에에서 나온 것 처럼:</span><span class="sxs-lookup"><span data-stu-id="ff4cf-310">tooretrieve hello list of deployed Azure resource group deployments, use hello cmdlet **Get-AzureRmResourceGroupDeployment**, as shown in hello following example:</span></span>

```powershell
Get-AzureRmResourceGroupDeployment -ResourceGroupName adf
```

```
DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

#### <a name="troubleshoot-user-events"></a><span data-ttu-id="ff4cf-311">사용자 이벤트 문제 해결</span><span class="sxs-lookup"><span data-stu-id="ff4cf-311">Troubleshoot user events</span></span>
1. <span data-ttu-id="ff4cf-312">Hello를 클릭 한 후 생성 되는 모든 hello 이벤트를 볼 수 **메트릭 및 작업** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-312">You can see all hello events that are generated after clicking hello **Metrics and operations** tile.</span></span>

    ![메트릭 및 작업 타일](./media/data-factory-monitor-manage-pipelines/metrics-and-operations-tile.png)
2. <span data-ttu-id="ff4cf-314">Hello 클릭 **이벤트** toosee hello 이벤트 바둑판식으로 배열 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-314">Click hello **Events** tile toosee hello events.</span></span>

    ![이벤트 타일](./media/data-factory-monitor-manage-pipelines/events-tile.png)
3. <span data-ttu-id="ff4cf-316">Hello에 **이벤트** 블레이드에서 등, 필터링 된 이벤트 및 이벤트에 대 한 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-316">On hello **Events** blade, you can see details about events, filtered events, and so on.</span></span>

    ![이벤트 블레이드](./media/data-factory-monitor-manage-pipelines/events-blade.png)
4. <span data-ttu-id="ff4cf-318">클릭는 **작업** 하면 오류가 발생 하는 hello 작업 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-318">Click an **Operation** in hello operations list that causes an error.</span></span>

    ![작업 선택](./media/data-factory-monitor-manage-pipelines/select-operation.png)
5. <span data-ttu-id="ff4cf-320">클릭는 **오류** hello 오류에 대 한 이벤트 toosee 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-320">Click an **Error** event toosee details about hello error.</span></span>

    ![이벤트 오류](./media/data-factory-monitor-manage-pipelines/operation-error-event.png)

<span data-ttu-id="ff4cf-322">참조 [Azure Insight cmdlet](https://msdn.microsoft.com/library/mt282452.aspx) tooadd를 사용할 수 있는 PowerShell cmdlet에 대 한 가져오기 또는 경고를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-322">See [Azure Insight cmdlets](https://msdn.microsoft.com/library/mt282452.aspx) for PowerShell cmdlets that you can use tooadd, get, or remove alerts.</span></span> <span data-ttu-id="ff4cf-323">다음은 hello를 사용 하 여의 몇 가지 예제 **Get AlertRule** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ff4cf-323">Here are a few examples of using hello **Get-AlertRule** cmdlet:</span></span>

```powershell
get-alertrule -res $resourceGroup -n ADFAlertsSlice -det
```

```
Properties :
Action      : Microsoft.Azure.Management.Insights.Models.RuleEmailAction
Condition   :
DataSource :
EventName             :
Category              :
Level                 :
OperationName         : RunFinished
ResourceGroupName     :
ResourceProviderName  :
ResourceId            :
Status                : Failed
SubStatus             : FailedExecution
Claims                : Microsoft.Azure.Management.Insights.Models.RuleManagementEventClaimsDataSource
Condition      :
Description : One or more of hello data slices for hello Azure Data Factory has failed processing.
Status      : Enabled
Name:       : ADFAlertsSlice
Tags       :
$type          : Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage
Id: /subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/ADFAlertsSlice
Location   : West US
Name       : ADFAlertsSlice
```

```powershell
Get-AlertRule -res $resourceGroup
```
```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0

Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest3
Location   : West US
Name       : FailedExecutionRunsWest3
```

```powershell
Get-AlertRule -res $resourceGroup -Name FailedExecutionRunsWest0
```

```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0
```

<span data-ttu-id="ff4cf-324">Hello g e t-h 명령 toosee 세부 정보 및 hello Get AlertRule cmdlet에 대 한 예제를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-324">Run hello following get-help commands toosee details and examples for hello Get-AlertRule cmdlet.</span></span>

```powershell
get-help Get-AlertRule -detailed
```

```powershell
get-help Get-AlertRule -examples
```


<span data-ttu-id="ff4cf-325">Hello 경고 생성 이벤트에 표시 되 면 hello 포털 블레이드 있지만 하지 않는 전자 메일 알림이 제공, hello 전자 메일 주소를 지정 하는 외부 보낸 사람 으로부터 tooreceive 전자 메일 설정 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-325">If you see hello alert generation events on hello portal blade but you don't receive email notifications, check whether hello email address that is specified is set tooreceive emails from external senders.</span></span> <span data-ttu-id="ff4cf-326">hello 경고 메일 전자 메일 설정에 의해 차단 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-326">hello alert emails might have been blocked by your email settings.</span></span>

### <a name="alerts-on-metrics"></a><span data-ttu-id="ff4cf-327">메트릭에 대한 경고</span><span class="sxs-lookup"><span data-stu-id="ff4cf-327">Alerts on metrics</span></span>
<span data-ttu-id="ff4cf-328">Data Factory에서 다양한 메트릭을 캡처하고 메트릭에 대한 경고를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-328">In Data Factory, you can capture various metrics and create alerts on metrics.</span></span> <span data-ttu-id="ff4cf-329">모니터링 및 데이터 팩터리에서 조각 hello에 대 한 메트릭을 다음 hello에 경고를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-329">You can monitor and create alerts on hello following metrics for hello slices in your data factory:</span></span>

* <span data-ttu-id="ff4cf-330">**실패한 실행**</span><span class="sxs-lookup"><span data-stu-id="ff4cf-330">**Failed Runs**</span></span>
* <span data-ttu-id="ff4cf-331">**성공한 실행**</span><span class="sxs-lookup"><span data-stu-id="ff4cf-331">**Successful Runs**</span></span>

<span data-ttu-id="ff4cf-332">이러한 메트릭 유용 및 tooget hello data factory에 전체 실패 및 성공에 대 한 개요를 실행 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-332">These metrics are useful and help you tooget an overview of overall failed and successful runs in hello data factory.</span></span> <span data-ttu-id="ff4cf-333">메트릭은 조각을 실행할 때마다 내보내집니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-333">Metrics are emitted every time there is a slice run.</span></span> <span data-ttu-id="ff4cf-334">Hello 시간의 hello 맨 이러한 메트릭에 집계 되 고 tooyour 저장소 계정 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-334">At hello beginning of hello hour, these metrics are aggregated and pushed tooyour storage account.</span></span> <span data-ttu-id="ff4cf-335">tooenable 메트릭을 저장소 계정을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-335">tooenable metrics, set up a storage account.</span></span>

#### <a name="enable-metrics"></a><span data-ttu-id="ff4cf-336">메트릭 사용</span><span class="sxs-lookup"><span data-stu-id="ff4cf-336">Enable metrics</span></span>
<span data-ttu-id="ff4cf-337">tooenable 메트릭을 클릭 hello에서 hello 다음 **Data Factory** 블레이드:</span><span class="sxs-lookup"><span data-stu-id="ff4cf-337">tooenable metrics, click hello following from hello **Data Factory** blade:</span></span>

<span data-ttu-id="ff4cf-338">**모니터링** > **메트릭** > **진단 설정** > **진단**</span><span class="sxs-lookup"><span data-stu-id="ff4cf-338">**Monitoring** > **Metric** > **Diagnostic settings** > **Diagnostics**</span></span>

![진단 링크](./media/data-factory-monitor-manage-pipelines/diagnostics-link.png)

<span data-ttu-id="ff4cf-340">Hello에 **진단** 블레이드에서 클릭 **에**hello 저장소 계정을 선택 하 고 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-340">On hello **Diagnostics** blade, click **On**, select hello storage account, and click **Save**.</span></span>

![진단 블레이드](./media/data-factory-monitor-manage-pipelines/diagnostics-blade.png)

<span data-ttu-id="ff4cf-342">Hello 메트릭 toobe hello에 대 한 tooone 시간 걸릴 수도 있습니다 **모니터링** 블레이드에서 메트릭을 집계 1 시간 마다 발생 하기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-342">It might take up tooone hour for hello metrics toobe visible on hello **Monitoring** blade because metrics aggregation happens hourly.</span></span>

### <a name="set-up-an-alert-on-metrics"></a><span data-ttu-id="ff4cf-343">메트릭에 대한 경고 설정:</span><span class="sxs-lookup"><span data-stu-id="ff4cf-343">Set up an alert on metrics</span></span>
<span data-ttu-id="ff4cf-344">Hello 클릭 **Data Factory 메트릭** 타일:</span><span class="sxs-lookup"><span data-stu-id="ff4cf-344">Click hello **Data Factory metrics** tile:</span></span>

![데이터 팩터리 메트릭 타일](./media/data-factory-monitor-manage-pipelines/data-factory-metrics-tile.png)

<span data-ttu-id="ff4cf-346">Hello에 **메트릭을** 블레이드에서 클릭 **+ 추가 경고** hello 도구 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-346">On hello **Metric** blade, click **+ Add alert** on hello toolbar.</span></span>
<span data-ttu-id="ff4cf-347">![데이터 팩터리 메트릭 블레이드 > 경고 추가](./media/data-factory-monitor-manage-pipelines/add-alert.png)</span><span class="sxs-lookup"><span data-stu-id="ff4cf-347">![Data factory metric blade > Add alert](./media/data-factory-monitor-manage-pipelines/add-alert.png)</span></span>

<span data-ttu-id="ff4cf-348">Hello에 **경고 규칙 추가** 페이지 수행 단계에 따라 hello 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-348">On hello **Add an alert rule** page, do hello following steps, and click **OK**.</span></span>

* <span data-ttu-id="ff4cf-349">Hello 경고에 대 한 이름을 입력 하십시오 (예: "하지 못했다는 경고가").</span><span class="sxs-lookup"><span data-stu-id="ff4cf-349">Enter a name for hello alert (example: "failed alert").</span></span>
* <span data-ttu-id="ff4cf-350">Hello 경고에 대 한 설명을 입력 하십시오 (예: "는 오류 발생 시 전자 메일 보내기").</span><span class="sxs-lookup"><span data-stu-id="ff4cf-350">Enter a description for hello alert (example: "send an email when a failure occurs").</span></span>
* <span data-ttu-id="ff4cf-351">메트릭을 선택합니다("실패한 실행" 대 "성공한 실행").</span><span class="sxs-lookup"><span data-stu-id="ff4cf-351">Select a metric ("Failed Runs" vs. "Successful Runs").</span></span>
* <span data-ttu-id="ff4cf-352">조건 및 임계값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-352">Specify a condition and a threshold value.</span></span>   
* <span data-ttu-id="ff4cf-353">Hello 기간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-353">Specify hello period of time.</span></span>
* <span data-ttu-id="ff4cf-354">Tooowners, 참가자 및 독자 전자 메일을 보낼지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-354">Specify whether an email should be sent tooowners, contributors, and readers.</span></span>

![데이터 팩터리 메트릭 블레이드 > 경고 규칙 추가](./media/data-factory-monitor-manage-pipelines/add-an-alert-rule.png)

<span data-ttu-id="ff4cf-356">Hello 경고 규칙은 성공적으로 추가 하 고 hello 블레이드를 닫습니다 hello hello 새 경고를 표시 **메트릭을** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-356">After hello alert rule is added successfully, hello blade closes and you see hello new alert on hello **Metric** blade.</span></span>

![데이터 팩터리 메트릭 블레이드 > 새 경고 추가됨](./media/data-factory-monitor-manage-pipelines/failed-alert-in-metric-blade.png)

<span data-ttu-id="ff4cf-358">또한 표시 hello hello 동안의 경고 수 **규칙 경고** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-358">You should also see hello number of alerts in hello **Alert rules** tile.</span></span> <span data-ttu-id="ff4cf-359">Hello 클릭 **규칙 경고** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-359">Click hello **Alert rules** tile.</span></span>

![데이터 팩터리 메트릭 블레이드 - 경고 규칙](./media/data-factory-monitor-manage-pipelines/alert-rules-tile-rules.png)

<span data-ttu-id="ff4cf-361">Hello에 **규칙 경고** 블레이드에서 모든 기존 경고를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-361">On hello **Alerts rules** blade, you see any existing alerts.</span></span> <span data-ttu-id="ff4cf-362">경고를 tooadd 클릭 **추가 경고** hello 도구 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-362">tooadd an alert, click **Add alert** on hello toolbar.</span></span>

![경고 규칙 블레이드](./media/data-factory-monitor-manage-pipelines/alert-rules-blade.png)

### <a name="alert-notifications"></a><span data-ttu-id="ff4cf-364">경고 알림</span><span class="sxs-lookup"><span data-stu-id="ff4cf-364">Alert notifications</span></span>
<span data-ttu-id="ff4cf-365">Hello 조건이 일치 하는 hello 경고 규칙이 hello 경고가 활성화 될 알리는 전자 메일을 구하십시오.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-365">After hello alert rule matches hello condition, you should get an email that says hello alert is activated.</span></span> <span data-ttu-id="ff4cf-366">Hello 문제가 해결 되 고 hello 경고 조건이 더 이상 일치 하지 않습니다, 후 hello 경고가 해결 된 라고 표시 된 전자 메일을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-366">After hello issue is resolved and hello alert condition doesn’t match anymore, you get an email that says hello alert is resolved.</span></span>

<span data-ttu-id="ff4cf-367">이 동작은 경고 규칙을 충족하는 모든 오류에 대해 알림이 전송되는 이벤트와는 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-367">This behavior is different than events where a notification is sent on every failure that an alert rule qualifies for.</span></span>

### <a name="deploy-alerts-by-using-powershell"></a><span data-ttu-id="ff4cf-368">PowerShell을 사용하여 경고 배포</span><span class="sxs-lookup"><span data-stu-id="ff4cf-368">Deploy alerts by using PowerShell</span></span>
<span data-ttu-id="ff4cf-369">동일한 메트릭을 hello에 대 한 경고를 배포할 수 이벤트에 대 한 방법으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-369">You can deploy alerts for metrics hello same way that you do for events.</span></span>

<span data-ttu-id="ff4cf-370">**경고 정의**</span><span class="sxs-lookup"><span data-stu-id="ff4cf-370">**Alert definition**</span></span>

```JSON
{
    "contentVersion" : "1.0.0.0",
    "$schema" : "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters" : {},
    "resources" : [
    {
            "name" : "FailedRunsGreaterThan5",
            "type" : "microsoft.insights/alertrules",
            "apiVersion" : "2014-04-01",
            "location" : "East US",
            "properties" : {
                "name" : "FailedRunsGreaterThan5",
                "description" : "Failed Runs greater than 5",
                "isEnabled" : true,
                "condition" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.ThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
                    "dataSource" : {
                        "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
                        "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
                        "resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName
>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>",
                        "metricName" : "FailedRuns"
                    },
                    "threshold" : 5.0,
                    "windowSize" : "PT3H",
                    "timeAggregation" : "Total"
                },
                "action" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails" : ["abhinav.gpt@live.com"]
                }
            }
        }
    ]
}
```

<span data-ttu-id="ff4cf-371">대체 *subscriptionId*, *resourceGroupName*, 및 *dataFactoryName* 적절 한 값으로 hello 샘플에서입니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-371">Replace *subscriptionId*, *resourceGroupName*, and *dataFactoryName* in hello sample with appropriate values.</span></span>

<span data-ttu-id="ff4cf-372">*metricName*은 현재 두 가지 값을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-372">*metricName* currently supports two values:</span></span>

* <span data-ttu-id="ff4cf-373">FailedRuns</span><span class="sxs-lookup"><span data-stu-id="ff4cf-373">FailedRuns</span></span>
* <span data-ttu-id="ff4cf-374">SuccessfulRuns</span><span class="sxs-lookup"><span data-stu-id="ff4cf-374">SuccessfulRuns</span></span>

<span data-ttu-id="ff4cf-375">**Hello 경고를 배포 합니다.**</span><span class="sxs-lookup"><span data-stu-id="ff4cf-375">**Deploy hello alert**</span></span>

<span data-ttu-id="ff4cf-376">toodeploy hello 경고를 사용 하 여 hello Azure PowerShell cmdlet **새로 AzureRmResourceGroupDeployment**hello 다음 예제에에서 나온 것 처럼:</span><span class="sxs-lookup"><span data-stu-id="ff4cf-376">toodeploy hello alert, use hello Azure PowerShell cmdlet **New-AzureRmResourceGroupDeployment**, as shown in hello following example:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\FailedRunsGreaterThan5.json
```

<span data-ttu-id="ff4cf-377">배포가 완료되면 다음과 같은 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-377">You should see following message after a successful deployment:</span></span>

```
VERBOSE: 12:52:47 PM - Template is valid.
VERBOSE: 12:52:48 PM - Create template deployment 'FailedRunsGreaterThan5'.
VERBOSE: 12:52:55 PM - Resource microsoft.insights/alertrules 'FailedRunsGreaterThan5' provisioning status is succeeded


DeploymentName    : FailedRunsGreaterThan5
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 7/27/2015 7:52:56 PM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           
```

<span data-ttu-id="ff4cf-378">Hello를 사용할 수도 있습니다 **추가 AlertRule** cmdlet toodeploy 경고 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-378">You can also use hello **Add-AlertRule** cmdlet toodeploy an alert rule.</span></span> <span data-ttu-id="ff4cf-379">Hello 참조 [추가 AlertRule](https://msdn.microsoft.com/library/mt282468.aspx) 세부 정보 및 예에 대 한 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-379">See hello [Add-AlertRule](https://msdn.microsoft.com/library/mt282468.aspx) topic for details and examples.</span></span>  

## <a name="move-a-data-factory-tooa-different-resource-group-or-subscription"></a><span data-ttu-id="ff4cf-380">데이터 팩터리 tooa 다른 리소스 그룹 또는 구독 이동</span><span class="sxs-lookup"><span data-stu-id="ff4cf-380">Move a data factory tooa different resource group or subscription</span></span>
<span data-ttu-id="ff4cf-381">Hello를 사용 하 여 데이터 팩터리 tooa 다른 리소스 그룹 또는 다른 구독을 이동할 수 **이동** 명령 모음 단추 데이터 팩터리의 hello 홈 페이지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-381">You can move a data factory tooa different resource group or a different subscription by using hello **Move** command bar button on hello home page of your data factory.</span></span>

![데이터 팩터리 이동](./media/data-factory-monitor-manage-pipelines/MoveDataFactory.png)

<span data-ttu-id="ff4cf-383">(예: 경고 hello 데이터 팩터리와 연결 된), 관련 된 모든 리소스가 hello 데이터 팩터리와 함께 이동할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff4cf-383">You can also move any related resources (such as alerts that are associated with hello data factory), along with hello data factory.</span></span>

![리소스 이동 대화 상자](./media/data-factory-monitor-manage-pipelines/MoveResources.png)
