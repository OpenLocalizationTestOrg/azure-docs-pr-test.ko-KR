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
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-monitoring-and-management-app"></a>모니터링 하 고 hello 모니터링 및 관리 응용 프로그램을 사용 하 여 Azure 데이터 팩터리 파이프라인 관리
> [!div class="op_single_selector"]
> * [Azure 포털/Azure PowerShell 사용](data-factory-monitor-manage-pipelines.md)
> * [모니터링 및 관리 앱 사용](data-factory-monitor-manage-app.md)
>
>

이 문서에서는 toouse를 모니터링 및 관리 앱 toomonitor hello, 관리 및 데이터 팩터리 파이프라인을 디버깅 방법을 설명 합니다. 또한 toocreate tooget 오류에 대 한 알림 경고 하는 방법에 정보를 제공 합니다. 있습니다 수 시작 hello 응용 프로그램을 사용 하 여 다음 시청 hello 하 여 비디오:

> [!NOTE]
> hello 사용자 인터페이스에에서 표시 된 것 hello 비디오 다 hello 포털에 표시 된 것입니다. 하지만 약간 오래 된 개념 유지 hello 동일 합니다. 

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-Data-Factory-Monitoring-and-Managing-Big-Data-Piplines/player]
>

## <a name="launch-hello-monitoring-and-management-app"></a>Hello 모니터링 및 관리 앱 시작
toolaunch hello 모니터 및 관리 응용 프로그램 클릭 hello **모니터링 및 관리** hello 타일 **Data Factory** 블레이드 데이터 팩토리에 대 한 합니다.

![타일을 hello Data Factory 홈 페이지에서 모니터링](./media/data-factory-monitor-manage-app/MonitoringAppTile.png)

별도 창에서 열고 hello 모니터링 및 관리 앱이 표시 되어야 합니다.  

![모니터링 및 관리 앱](./media/data-factory-monitor-manage-app/AppLaunched.png)

> [!NOTE]
> 해당 hello 웹 브라우저에서 "권한 부여..." 걸려 표시 되 면 hello의 선택을 취소 **타사 쿠키를 차단 하 고 사이트 데이터** 확인란-또는 선택한 상태가 유지에 대 한 예외를 만들려면 **login.microsoftonline.com** 후 tooopen hello 응용 프로그램을 다시 시도 하십시오.


목록의 hello 활동 Windows hello 가운데 창에서 각 활동 실행에 대해 작업 창이 표시 합니다. 예를 들어 5 시간에 대 한 예약 된 활동 toorun hello에 1 시간 마다 있는 5 개의 데이터 조각와 연결 된 5 개 활동 창 참조 합니다. 활동 창 hello 맨 아래에 hello 목록에 보이지 않으면 다음 hello지 않습니다.
 
- 업데이트 hello **시작 시간** 및 **종료 시간** hello 상위 toomatch hello에 대 한 필터 시작 및 종료 후 파이프라인의 시간을 누른 다음 hello **적용** 단추입니다.  
- hello 활동 창 목록은 자동으로 고쳐지지 않습니다. Hello 클릭 **새로 고침** hello에 hello 도구 모음에서 단추 **활동 창** 목록입니다.  

데이터 팩터리 응용 프로그램 tootest으로 이러한 단계에 없을 경우 자습서 hello지 않습니다: [Blob 저장소 tooSQL 데이터 팩터리를 사용 하 여 데이터베이스에서에서 데이터를 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.

## <a name="understand-hello-monitoring-and-management-app"></a>Hello 모니터링 및 관리 응용 프로그램 이해
Hello 왼쪽에는 세 개의 탭: **리소스 탐색기**, **모니터링 보기**, 및 **경고**합니다. hello 첫 번째 탭 (**리소스 탐색기**) 기본적으로 선택 됩니다.

### <a name="resource-explorer"></a>리소스 탐색기
Hello 다음을 참조 합니다.

* 리소스 탐색기 hello **트리 보기** hello 왼쪽된 창에서.
* hello **다이어그램 보기** hello 가운데 창에서 hello 위쪽에 있습니다.
* hello **활동 창** hello 가운데 창에서 hello 맨 아래에는 목록입니다.
* hello **속성**, **활동 창 탐색기**, 및 **스크립트** hello 오른쪽 창에서 탭 합니다.

리소스 탐색기 트리 뷰에서 hello data factory에 모든 리소스 (파이프라인, 데이터 집합, 연결 된 서비스)를 볼 수 있습니다. 리소스 탐색기에서 개체를 선택하는 경우:

* hello 관련 Data Factory 엔터티에 hello 다이어그램 보기에서에서 강조 표시 됩니다.
* [활동 창에 연결 된](data-factory-scheduling-and-execution.md) hello 맨 아래에 hello 활동 창 목록에 강조 표시 됩니다.  
* hello 선택한 개체의 속성을 hello hello 오른쪽 창에서 hello 속성 창에 표시 됩니다.
* hello hello 선택한 개체의 JSON 정의 표시 되며, 해당 하는 경우. 예: 연결된 서비스, 데이터 집합 또는 파이프라인.

![리소스 탐색기](./media/data-factory-monitor-manage-app/ResourceExplorer.png)

Hello 참조 [일정 예약 및 실행](data-factory-scheduling-and-execution.md) 활동 기간에 대 한 자세한 개념 정보는 문서입니다.

### <a name="diagram-view"></a>다이어그램 뷰
데이터 팩터리의 다이어그램 보기 hello 유리 toomonitor 단일 창을 제공 하 고 data factory와 해당 자산을 관리 합니다. Hello 다이어그램 보기에서에서 데이터 팩터리 엔터티 (데이터 집합/파이프라인)을 선택 하면:

* 데이터 팩터리 엔터티 hello hello 트리 보기에서 선택 되어 있습니다.
* hello 관련 활동 windows hello 활동 창 목록에 강조 표시 됩니다.
* hello 선택한 개체의 속성을 hello hello 속성 창에 표시 됩니다.

Hello 파이프라인 (일시 중지 된 상태)에 없는 활성화 되 면 녹색 줄이 표시 됩니다.

![파이프라인 실행](./media/data-factory-monitor-manage-app/PipelineRunning.png)

일시 중지, 다시 시작 하거나 hello 다이어그램 보기에서 선택 하 고 hello 명령 모음에서 hello 단추를 사용 하 여 파이프라인을 종료할 수 있습니다.

![Hello 명령 모음에서 일시 중지/다시 시작](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)
 
Hello 다이어그램 보기에서에서 hello 파이프라인에 대 한 세 가지 명령 모음 단추가 있습니다. Hello 두 번째 단추 toopause hello 파이프라인을 사용할 수 있습니다. 일시 중지 하는 현재 활동을 실행 하는 hello를 종료 하지 않습니다 및 toocompletion 진행할 수 있습니다. 세 번째 단추 hello hello 파이프라인을 일시 중지 하 고 실행 되는 활동의 기존 종료 합니다. 첫 번째 단추 hello hello 파이프라인 다시 시작합니다. 파이프라인 일시 중지 된 hello 파이프라인의 hello 색이 변경 합니다. 예를 들어, 일시 중지 된 파이프라인 같이 hello 다음 이미지에에서 표시 됩니다. 

![파이프라인 일시 중지](./media/data-factory-monitor-manage-app/PipelinePaused.png)

Hello Ctrl 키를 사용 하 여 여러 개 선택 하거나 둘 이상의 파이프라인 할 수 있습니다. 한 번에 hello 명령 모음 단추 toopause/resume 여러 파이프라인을 사용할 수 있습니다.

스키마는 파이프라인과 옵션 선택 toosuspend 다시 시작 또는 파이프라인을 종료 합니다. 

![파이프라인에 대한 상황에 맞는 메뉴](./media/data-factory-monitor-manage-app/right-click-menu-for-pipeline.png)

Hello 클릭 **열려 파이프라인** toosee hello 파이프라인의 모든 hello 활동 옵션입니다. 

![파이프라인 열기 메뉴](./media/data-factory-monitor-manage-app/OpenPipelineMenu.png)

열린 hello 파이프라인 보기에 hello 파이프라인의 모든 작업이 표시 됩니다. 이 예제에서는 하나의 작업, 복사 작업만이 있습니다. 

![열린 파이프라인](./media/data-factory-monitor-manage-app/OpenedPipeline.png)

toogo toohello 이전 뷰를 다시 hello 데이터 팩토리 이름이 hello 위쪽 hello 이동 경로 탐색 메뉴에서를 클릭 합니다.

Hello 파이프라인 보기에서 출력 데이터 집합 또는 hello 출력 데이터 집합 위로 마우스를 이동 하면 선택 하면 해당 데이터 집합에 대 한 hello 활동 창 팝업 창이 표시 됩니다.

![활동 기간 팝업 창](./media/data-factory-monitor-manage-app/ActivityWindowsPopup.png)

클릭할 수 있는 작업 창 toosee 세부 정보에 대 한 hello에 **속성** hello 오른쪽 창에서 창.

![활동 기간 속성](./media/data-factory-monitor-manage-app/ActivityWindowProperties.png)

Hello 오른쪽 창에서 toohello 전환 **활동 Window 탐색기** toosee 자세한 세부 정보를 탭 합니다.

![작업 창 탐색기](./media/data-factory-monitor-manage-app/ActivityWindowExplorer.png)

또한 참조 **변수 해결** hello에 있는 활동에 대 한 각 실행된 시도 대 한 **시도** 섹션.

![확인된 변수](./media/data-factory-monitor-manage-app/ResolvedVariables.PNG)

Toohello 전환 **스크립트** toosee hello JSON 스크립트 hello 선택한 개체에 대 한 정의 탭 합니다.   

![스크립트 탭](./media/data-factory-monitor-manage-app/ScriptTab.png)

세 위치에서 작업 창을 확인할 수 있습니다.

* hello 활동 창 팝업 hello 다이어그램 보기 (가운데 창)에 있습니다.
* 활동 창 탐색기 hello 오른쪽 창에서 번호입니다.
* hello 아래쪽 창에 hello 활동 창 목록입니다.

Hello 활동 창 팝업 및 활동 창 탐색기에 이전 주 toohello를 스크롤할 수 있습니다 및 hello를 사용 하 여 다음 주 hello 왼쪽 및 오른쪽 화살표입니다.

![활동 기간 탐색기 왼쪽/오른쪽 화살표](./media/data-factory-monitor-manage-app/ActivityWindowExplorerLeftRightArrows.png)

이러한 단추 hello 다이어그램 보기의 hello 맨 아래에 표시: 확대, 축소, 확대/축소 tooFit 잠금 레이아웃 100% 확대/축소 합니다. hello **잠금 레이아웃** 단추 실수로 hello 다이어그램 보기에서에서 테이블 및 파이프라인을 이동 하면 메시지를 표시 합니다. 기본적으로 해제된 상태입니다. 해제 한 hello 다이어그램에 엔터티를 이동할 수 있습니다. 를 설정 하면 hello 마지막 단추 tooautomatically 위치 테이블 및 파이프라인을 사용할 수 있습니다. Hello 마우스 휠을 사용 하 여 in 또는 out을 확대할 수도 있습니다.

![다이어그램 뷰 확대/축소 명령](./media/data-factory-monitor-manage-app/DiagramViewZoomCommands.png)

### <a name="activity-windows-list"></a>활동 기간 목록
hello hello 가운데 창 맨 아래에 hello 활동 창 목록에는 hello 리소스 탐색기 또는 hello 다이어그램 보기에서 선택한 hello 데이터 집합에 대 한 모든 작업 창이 표시 됩니다. 기본적으로 hello 목록은 내림차순으로 hello 위쪽 hello 최신 활동 창에 표시 하는 것입니다.

![활동 기간 목록](./media/data-factory-monitor-manage-app/ActivityWindowsList.png)

이 목록 새로 고칠 hello 도구 모음 toomanually에 hello 새로 고침 단추를 사용 하도록 자동으로 반영 하지 않습니다.  

활동 windows hello 다음 상태 중 하나일 수 있습니다.

<table>
<tr>
    <th align="left">가동 상태</th><th align="left">하위 상태</th><th align="left">설명</th>
</tr>
<tr>
    <td rowspan="8">대기</td><td>ScheduleTime</td><td>hello에 활동 창 toorun hello에 대 한 대로 되지 않았습니다.</td>
</tr>
<tr>
<td>DatasetDependencies</td><td>업스트림 종속성 hello 준비 되지 않았습니다.</td>
</tr>
<tr>
<td>ComputeResources</td><td>hello 계산 리소스를 사용할 수 없습니다.</td>
</tr>
<tr>
<td>ConcurrencyLimit</td> <td>모든 hello 활동 인스턴스는 다른 활동 창 실행 중입니다.</td>
</tr>
<tr>
<td>ActivityResume</td><td>hello 활동 일시 중지 및 다시 시작 될 때까지 활동 windows hello를 실행할 수 없습니다.</td>
</tr>
<tr>
<td>Retry</td><td>hello 활동 실행을 시도 하는 중입니다.</td>
</tr>
<tr>
<td>유효성 검사</td><td>유효성 검사가 아직 시작되지 않았습니다.</td>
</tr>
<tr>
<td>ValidationRetry</td><td>유효성 검사는 대기 중인 toobe 다시 시도 합니다.</td>
</tr>
<tr>
<tr>
<td rowspan="2">InProgress</td><td>유효성 검사 중</td><td>유효성 검사가 진행 중입니다.</td>
</tr>
<td>-</td>
<td>hello 활동 창 처리 중입니다.</td>
</tr>
<tr>
<td rowspan="4">실패</td><td>TimedOut</td><td>hello 활동 실행 hello 활동에 의해 허용 된 것 보다 더 오래 걸립니다.</td>
</tr>
<tr>
<td>Canceled</td><td>hello 활동 창 사용자 작업에 의해 취소 되었습니다.</td>
</tr>
<tr>
<td>유효성 검사</td><td>유효성 검사가 실패했습니다.</td>
</tr>
<tr>
<td>-</td><td>hello 활동 창 toobe 생성 하거나 유효성을 검사 하지 못했습니다.</td>
</tr>
<td>Ready</td><td>-</td><td>hello 활동 창이 준비가 됩니다.</td>
</tr>
<tr>
<td>생략</td><td>-</td><td>hello 활동 창 처리 되지 않았습니다.</td>
</tr>
<tr>
<td>없음</td><td>-</td><td>활동 창 tooexist 다른 상태와 함께 사용 되지만 다시 설정 되었습니다.</td>
</tr>
</table>


Hello에서 항목에 대 한 정보를 참조 하는 활동 창의 hello 목록에서를 클릭 하면 **활동 Windows 탐색기** 또는 hello **속성** hello 오른쪽에 창입니다.

![작업 창 탐색기](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-2.png)

### <a name="refresh-activity-windows"></a>작업 창 새로 고침
hello 세부 정보를 자동으로 새로 아닌, hello 명령 모음 toomanually 새로 고침 hello 활동 창 목록에서는 hello 새로 고침 단추 (hello 두 번째 단추)를 사용 하도록 합니다.  

### <a name="properties-window"></a>속성 창
속성 창 hello hello 모니터링 및 관리 응용 프로그램의 hello 맨 오른쪽 창에 표시 됩니다.

![속성 창](./media/data-factory-monitor-manage-app/PropertiesWindow.png)

Hello 리소스 탐색기 (트리 보기)에서 선택한 hello 항목의 속성을 표시 다이어그램 보기 또는 작업 창 목록입니다.

### <a name="activity-window-explorer"></a>작업 창 탐색기
hello **활동 창 탐색기** 창의 hello 모니터링 및 관리 응용 프로그램의 hello 맨 오른쪽 창에 표시 됩니다. Hello 활동 창 팝업 창이 나 hello 활동 창 목록에서 선택한 hello 활동 창에 대 한 세부 정보를 표시 합니다.

![작업 창 탐색기](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-3.png)

Hello 위쪽 hello 일정 보기에서 클릭 하 여 tooanother 활동 창을 전환할 수 있습니다. 이전 주 hello 상위 toosee 활동 windows hello에서에 hello 왼쪽된 화살표/오른쪽 화살표 단추를 사용 하거나 다음 주 hello 수도 있습니다.

Hello 아래쪽 창 toorerun hello 활동 창의 hello 도구 모음 단추를에서 사용 하거나 hello 창의 hello 세부 정보를 새로 고칠 수 있습니다.

### <a name="script"></a>스크립트
Hello를 사용할 수 있습니다 **스크립트** 탭 tooview hello hello의 JSON 정의 데이터 팩터리의 엔터티 (연결 된 서비스, 데이터 집합 또는 파이프라인)를 선택 합니다.

![스크립트 탭](./media/data-factory-monitor-manage-app/ScriptTab.png)

## <a name="use-system-views"></a>시스템 뷰 사용
hello 모니터링 및 관리 응용 프로그램에 포함 되어 미리 작성 된 시스템 뷰 (**최근 활동 창**, **활동 창 실패**, **진행 중인 활동 창**)를 데이터 팩토리에 대 한 최근/실패/진행 중인 활동 창 tooview 허용 합니다.

Toohello 전환 **모니터링 보기** 클릭 하 여 hello 왼쪽에 탭 합니다.

![모니터링 뷰 탭](./media/data-factory-monitor-manage-app/MonitoringViewsTab.png)

현재는 지원되는 세 가지 시스템 뷰가 있습니다. 선택 옵션 toosee 최근 활동 창, 실패 한 작업으로 windows 또는 진행 중인 활동 창 (hello 맨 hello 가운데 창) 아래에 hello 활동 창 목록에 있습니다.

Hello를 선택 하는 경우 **최근 활동 창** 모든 최근 활동 windows hello의 내림차순 표시 옵션을 **마지막 시도 시간**합니다.

Hello를 사용할 수 있습니다 **활동 창 실패** 실패 toosee 모든 활동 windows hello 목록에서 볼 수 있습니다. Hello 목록 toosee 세부 정보에서 항목에 대 한 hello에 실패 한 작업 기간을 선택 합니다. **속성** 창이 나 hello **활동 창 탐색기**합니다. 또한 실패한 작업 창에 대한 로그를 다운로드할 수 있습니다.

## <a name="sort-and-filter-activity-windows"></a>활동 기간 정렬 및 필터링
변경 hello **시작 시간** 및 **종료 시간** hello 명령 모음 toofilter 활동 창에서에서 설정 합니다. Hello 시작 시간과 종료 시간을 변경한 후 hello 단추 다음 toohello 종료 시간 toorefresh hello 활동 창 목록을 클릭 합니다.

![시작 및 종료 시간](./media/data-factory-monitor-manage-app/StartAndEndTimes.png)

> [!NOTE]
> 현재 모든 시간은 UTC 형식 hello 모니터링 및 관리 앱에는.
>
>

Hello에 **활동 창 목록**, hello 열 이름을 클릭 하 여 (예: 상태).

![활동 기간 목록 열 메뉴](./media/data-factory-monitor-manage-app/ActivityWindowsListColumnMenu.png)

작업을 수행할 수 hello 다음:

* 오름차순으로 정렬.
* 내림차순으로 정렬.
* 하나 이상의 값으로 필터링(준비, 대기 중 등).

열에 필터를 지정 하면 hello hello 열의 값이 필터링 된 값 임을 나타냅니다. 해당 열에 대해 사용 하도록 설정 하는 hello 필터 단추가 표시 됩니다.

![Hello 활동 창 목록의 열은 필터링](./media/data-factory-monitor-manage-app/ActivityWindowsListFilterInColumn.png)

에서는 동일한 팝업 창 tooclear 필터 hello 합니다. hello 활동 창 목록에 대 한 모든 필터 tooclear hello 명령 모음에서 hello 필터 지우기 단추를 클릭 합니다.

![Hello 활동 창 목록에 대 한 모든 필터 지우기](./media/data-factory-monitor-manage-app/ClearAllFiltersActivityWindowsList.png)

## <a name="perform-batch-actions"></a>배치 작업 수행
### <a name="rerun-selected-activity-windows"></a>선택한 작업 창 다시 실행
활동을 선택 하 고 아래쪽 화살표 hello 첫 번째 명령 모음 단추에 대 한 hello를 클릭 한 다음이 선택 **다시 실행** / **파이프라인에서 업스트림와 다시 실행**합니다. Hello를 선택 하는 경우 **파이프라인에서 업스트림와 다시 실행** 옵션을 모두 업스트림 작업 windows를 다시 실행 합니다.
    ![작업 창 다시 실행](./media/data-factory-monitor-manage-app/ReRunSlice.png)

또한 hello 목록에 여러 활동 기간을 선택할 수 있으며 hello에 다시 실행 하십시오 동시 합니다. Toofilter 활동 windows hello 상태에 기반 할 수 있습니다 (예: **실패**)-다음 실패 hello 활동 windows hello 활동 windows toofail hello 문제를 해결 한 후 다시 실행 하십시오. Hello 다음 활동 windows hello 목록에서 필터링 하는 방법에 대 한 세부 정보 섹션을 참조 하십시오.  

### <a name="pauseresume-multiple-pipelines"></a>여러 파이프라인 일시 중지/다시 시작
Hello Ctrl 키를 사용 하 여 두 개 이상의 파이프라인을 다중 선택할 수 있습니다. (다음 이미지는 hello hello 빨간색 사각형으로 강조 표시 됩니다)는 hello 명령 모음 단추를 사용할 수 있습니다 toopause/다시 시작을 합니다.

![Hello 명령 모음에서 일시 중지/다시 시작](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)

## <a name="create-alerts"></a>경고 만들기
hello **경고** 페이지에서는 경고와 보기/편집/삭제 기존 경고를 만들 수 있습니다. 또한 경고를 사용하지 않거나/사용할 수 있습니다. toosee hello 경고 페이지에서 hello **경고** 탭 합니다.

![경고 탭](./media/data-factory-monitor-manage-app/AlertsTab.png)

### <a name="toocreate-an-alert"></a>toocreate 경고
1. 클릭 **추가 경고** tooadd 경고 합니다. Hello 참조 **세부 정보** 페이지.

    ![경고 만들기 - 세부 정보 페이지](./media/data-factory-monitor-manage-app/CreateAlertDetailsPage.png)
2. Hello 지정 **이름** 및 **설명** hello 알림과 클릭에 대 한 **다음**합니다. Hello 표시 되어야 **필터** 페이지.

    ![경고 만들기 - 필터 페이지](./media/data-factory-monitor-manage-app/CreateAlertFiltersPage.png)
3. 선택 hello **이벤트**, **상태**, 및 **하위 상태** (선택 사항) 원하는 toocreate 데이터 팩터리 서비스에 대 한 경고 및 클릭 **다음**. Hello 표시 되어야 **받는 사람에 게** 페이지.

    ![경고 만들기 - 받는 사람 페이지](./media/data-factory-monitor-manage-app/CreateAlertRecipientsPage.png)
4. 선택 hello **구독 관리자 전자 메일** 옵션 및/또는 입력 한 **추가 관리자 전자 메일**를 클릭 하 고 **마침**합니다. Hello 경고 hello 목록에 표시 되어야 합니다.

    ![경고 목록](./media/data-factory-monitor-manage-app/AlertsList.png)

Hello 경고 목록에서 hello 경고 tooedit/삭제/비활성화/활성화 경고와 관련 된 hello 단추를 사용 합니다.

### <a name="eventstatussubstatus"></a>이벤트/상태/하위 상태
hello 다음 표에서 hello 목록을 사용할 수 있는 이벤트 및 상태 (및 하위 상태).

| 이벤트 이름 | 가동 상태 | 하위 상태 |
| --- | --- | --- |
| 작업 실행 시작 |Started |시작 중 |
| 작업 실행 완료 |Succeeded |Succeeded |
| 작업 실행 완료 |실패 |실패한 리소스 할당<br/><br/>실패한 실행<br/><br/>Timed Out<br/><br/>Failed Validation<br/><br/>Abandoned |
| 주문형 HDI 클러스터 만들기 시작 |Started |-|
| 주문형 HDI 클러스터 성공적으로 생성 |Succeeded |-|
| 주문형 HDI 클러스터 삭제 |Succeeded |-|

### <a name="tooedit-delete-or-disable-an-alert"></a>tooedit, 삭제 또는 경고를 사용 하지 않도록 설정

다음 (빨간색으로 강조 표시) 단추 tooedit, 삭제 또는 사용 안 함 경고 hello를 사용 합니다.

![경고 단추](./media/data-factory-monitor-manage-app/AlertButtons.png)
