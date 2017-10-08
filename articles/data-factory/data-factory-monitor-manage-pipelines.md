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
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-azure-portal-and-powershell"></a>모니터링 하 고 hello Azure 포털 및 PowerShell을 사용 하 여 Azure 데이터 팩터리 파이프라인 관리
> [!div class="op_single_selector"]
> * [Azure 포털/Azure PowerShell 사용](data-factory-monitor-manage-pipelines.md)
> * [모니터링 및 관리 앱 사용](data-factory-monitor-manage-app.md)


> [!IMPORTANT]
> hello 모니터링 및 관리 응용 프로그램 모니터링 및 데이터 파이프라인, 관리 및 문제 해결에 대 한 더 나은 지원을 제공 합니다. Hello 응용 프로그램을 사용 하는 방법에 대 한 세부 정보를 참조 하십시오. [모니터링 하 고 hello 모니터링 및 관리 앱을 사용 하 여 데이터 팩터리 파이프라인 관리](data-factory-monitor-manage-app.md)합니다. 


이 문서에서는 toomonitor를 관리 하 고 Azure 포털 및 PowerShell을 사용 하 여 파이프라인을 디버깅 하는 방법을 설명 합니다. hello 문서에 대 한 정보도 toocreate 경고 및 가져오기 방법을 실패에 대 한 알림을 받습니다.

## <a name="understand-pipelines-and-activity-states"></a>파이프라인 및 작업 상태 이해
Azure 포털 hello를 사용 하 여 다음을 수행할 수 있습니다.

* 데이터 팩터리를 다이어그램으로 보기
* 파이프라인에서 활동 보기
* 입력 및 출력 데이터 집합 보기

이 섹션에서는 또한 데이터 집합 조각 상태 tooanother 상태에서 전환 하는 방법을 설명 합니다.   

### <a name="navigate-tooyour-data-factory"></a>데이터 팩터리 tooyour 이동
1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. 클릭 **데이터 팩터리** hello hello 왼쪽 메뉴에 있습니다. 표시 되지 않는 경우 클릭 **더 많은 서비스 >**, 클릭 하 고 **데이터 팩터리** hello에서 **인텔리전스 + 분석** 범주입니다.

   ![모두 찾아보기 -> 데이터 팩터리](./media/data-factory-monitor-manage-pipelines/browseall-data-factories.png)
3. Hello에 **데이터 팩터리** 블레이드, 관심이 선택 hello 데이터 팩터리입니다.

    ![데이터 팩터리 선택](./media/data-factory-monitor-manage-pipelines/select-data-factory.png)

   Hello 데이터 팩토리에 대 한 hello 홈 페이지가 나타납니다.

   ![데이터 팩터리 블레이드](./media/data-factory-monitor-manage-pipelines/data-factory-blade.png)

#### <a name="diagram-view-of-your-data-factory"></a>데이터 팩터리의 다이어그램 뷰
hello **다이어그램** 데이터 팩터리의 유리 toomonitor의 단일 창 제공 뷰와 hello data factory와 해당 자산을 관리 합니다. toosee hello **다이어그램** 데이터 팩터리의 보려면 클릭 하십시오. **다이어그램** hello 데이터 팩토리에 대 한 hello 홈 페이지에 있습니다.

![다이어그램 뷰](./media/data-factory-monitor-manage-pipelines/diagram-view.png)

확대/축소 지정, 축소, 확대/축소 toofit, 확대/축소 too100%, hello 다이어그램의 잠금 hello 레이아웃 및 자동으로 파이프라인 및 데이터 집합 위치를 지정 합니다. Hello 데이터 계보 정보를 볼 수 있습니다 (즉, 선택한 항목의 업스트림 및 다운스트림 항목 표시).

### <a name="activities-inside-a-pipeline"></a>파이프라인 내부의 활동
1. Hello 파이프라인을 마우스 오른쪽 단추로 누른 **열려 파이프라인** toosee hello 활동에 대 한 입력 및 출력 데이터 집합 함께 hello에서 모든 활동 파이프라인. 이 기능은 사용자 파이프라인에 둘 이상의 활동이 포함 되어 단일 파이프라인의 toounderstand hello operational 계보 않으려는 경우에 유용 합니다.

    ![파이프라인 열기 메뉴](./media/data-factory-monitor-manage-pipelines/open-pipeline-menu.png)     
2. 다음 예제는 hello, hello 파이프라인에 입력 및 출력의 복사 작업을 볼 수 있습니다. 

    ![파이프라인 내부의 활동](./media/data-factory-monitor-manage-pipelines/activities-inside-pipeline.png)
3. Hello를 클릭 하 여 hello 데이터 팩터리의 백 toohello 홈 페이지를 탐색할 수 **Data factory** hello 왼쪽 위 모서리에 있는 이동 경로 탐색 hello에에서 링크 합니다.

    ![뒤로 toodata 공장 이동](./media/data-factory-monitor-manage-pipelines/navigate-back-to-data-factory.png)

### <a name="view-hello-state-of-each-activity-inside-a-pipeline"></a>파이프라인 내 각 활동의 hello 상태 보기
Hello 활동에 의해 생성 되는 hello 데이터 집합의 hello 상태를 확인 하 여 hello 활동의 현재 상태를 볼 수 있습니다.

Hello를 두 번 클릭 하 여 **OutputBlobTable** hello에 **다이어그램**, 파이프라인 내 다른 활동을 실행 하 여 생성 되는 모든 hello 분할 영역을 볼 수 있습니다. Hello 복사 활동 성공적으로 실행 hello에 대 한 마지막 8 시간 및 hello에서 hello 조각 생성 볼 수 있습니다 **준비** 상태입니다.  

![Hello 파이프라인의 상태](./media/data-factory-monitor-manage-pipelines/state-of-pipeline.png)

hello data factory에 hello 데이터 집합 분할 영역 hello 다음 상태 중 하나를 가질 수 있습니다.

<table>
<tr>
    <th align="left">시스템 상태</th><th align="left">하위 상태</th><th align="left">설명</th>
</tr>
<tr>
    <td rowspan="8">대기</td><td>ScheduleTime</td><td>hello에 조각 toorun hello에 대 한 대로 하지 않았습니다.</td>
</tr>
<tr>
<td>DatasetDependencies</td><td>업스트림 종속성 hello 준비 되지 않았습니다.</td>
</tr>
<tr>
<td>ComputeResources</td><td>hello 계산 리소스를 사용할 수 없습니다.</td>
</tr>
<tr>
<td>ConcurrencyLimit</td> <td>모든 hello 활동 인스턴스는 다른 조각을 실행 중입니다.</td>
</tr>
<tr>
<td>ActivityResume</td><td>hello 활동 일시 중지 되 고 hello 활동 재개 될 때까지 hello 분할 영역을 실행할 수 없습니다.</td>
</tr>
<tr>
<td>Retry</td><td>작업 실행을 다시 시도하는 중입니다.</td>
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
<td>hello 조각이 처리 중입니다.</td>
</tr>
<tr>
<td rowspan="4">실패</td><td>TimedOut</td><td>hello 활동 실행 hello 활동에 의해 허용 된 것 보다 더 오래 걸립니다.</td>
</tr>
<tr>
<td>Canceled</td><td>hello 조각은 사용자 작업에 의해 취소 되었습니다.</td>
</tr>
<tr>
<td>유효성 검사</td><td>유효성 검사가 실패했습니다.</td>
</tr>
<tr>
<td>-</td><td>hello 조각 toobe 생성 및/또는 유효성을 검사 하지 못했습니다.</td>
</tr>
<td>Ready</td><td>-</td><td>hello 조각이 소비에 대 한 준비 되었습니다.</td>
</tr>
<tr>
<td>생략</td><td>없음</td><td>hello 조각을 처리 되지 않습니다.</td>
</tr>
<tr>
<td>없음</td><td>-</td><td>분할 영역 tooexist 다른 상태와 함께 사용 되는 있지만 다시 설정 되었습니다.</td>
</tr>
</table>



Hello에 분할 영역 항목을 클릭 하 여 분할 영역에 대 한 hello 세부 정보를 볼 수 있습니다 **최근에 업데이트 되는 분할 영역** 블레이드입니다.

![조각 세부 정보](./media/data-factory-monitor-manage-pipelines/slice-details.png)

Hello의 여러 행을 볼 hello 분할은 여러 번 실행 하는 경우 **활동 실행** 목록입니다. Hello에 실행 하는 hello 항목을 클릭 하 여 실행 하는 작업에 대 한 정보를 볼 수 **활동 실행** 목록입니다. hello 목록에 있는 경우 오류 메시지와 함께 모든 hello 로그 파일 표시 됩니다. 이 기능은 데이터 팩터리 tooleave 필요 없이 유용 tooview 및 디버그 로그에 설명 합니다.

![작업 실행 세부 정보](./media/data-factory-monitor-manage-pipelines/activity-run-details.png)

Hello 조각 hello에 없으면 **준비** 상태 hello 업스트림 슬라이스입니다. 준비 되지 않았습니다 hello 현재 조각 hello에서 실행할 수 없도록 차단 하 고 볼 수 있습니다 **준비 되지 않은 업스트림 슬라이스** 목록입니다. 에 조각의 경우이 기능은 유용 **대기** 상태를 하려면 toounderstand hello 업스트림 종속성을 조각 hello에서 대기 중입니다.

![준비되지 않은 업스트림 조각](./media/data-factory-monitor-manage-pipelines/upstream-slices-not-ready.png)

### <a name="dataset-state-diagram"></a>데이터 집합 상태 다이어그램
데이터 팩터리를 배포한 후 hello 파이프라인에는 유효한 활성 기간이 hello 데이터 집합에서 하나의 상태 tooanother 전환을 분리 합니다. 현재 hello 조각 상태 hello 상태 다이어그램 뒤를 따릅니다.

![상태 다이어그램](./media/data-factory-monitor-manage-pipelines/state-diagram.png)

hello 데이터 집합 상태 전환 흐름이 data factory에는 hello 다음: 대기에서-진행률/진행 중 (Validating)-> 준비/실패->.

hello 조각의 시작는 **대기** 사전 조건 toobe 실행 하기 전에 충족에 대 한 대기 상태입니다. 그런 다음 hello 활동이 실행을 시작 하 고 hello 조각 전환 되는 **진행 중인** 상태입니다. hello 활동 실행 성공 하거나 실패 수 있습니다. hello 조각으로 표시 되어 **준비** 또는 **실패**hello hello 실행 결과에 따라 합니다.

Hello에서 다시 분할 영역 toogo hello를 다시 설정할 수 있습니다 **준비** 또는 **실패** 상태 toohello **대기** 상태입니다. 표시할 수도 있습니다 hello 조각 상태 너무**Skip**, hello 활동을 실행 하 고 hello 분할 영역을 처리 하지 않고 방지 하는 합니다.

## <a name="pause-and-resume-pipelines"></a>파이프라인 일시 중지 및 다시 시작
Azure PowerShell을 사용하여 파이프라인을 관리할 수 있습니다. 예를 들어 Azure PowerShell cmdlet을 실행하여 파이프라인을 일시 중지하거나 다시 시작할 수 있습니다. 

> [!NOTE] 
> 일시 중지 및 재개 파이프라인 hello 다이어그램 보기를 지원 하지 않습니다. Toouse 사용자 인터페이스를 원하는 경우 hello 모니터링 하 고 응용 프로그램 관리를 사용 합니다. Hello 응용 프로그램을 사용 하는 방법에 대 한 세부 정보를 참조 하십시오. [모니터링 하 고 hello 모니터링 및 관리 앱을 사용 하 여 데이터 팩터리 파이프라인 관리](data-factory-monitor-manage-app.md) 문서. 

일시 중지/일시 중지 하 파이프라인 hello를 사용 하 여 **Suspend AzureRmDataFactoryPipeline** PowerShell cmdlet. 이 cmdlet은 하지 않으려면 toorun 파이프라인 문제가 해결 될 때까지 하는 경우에 유용 합니다. 

```powershell
Suspend-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
예:

```powershell
Suspend-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

Hello 파이프라인과 hello 문제를 해결 후 일시 중단 하는 hello 파이프라인 hello 다음 PowerShell 명령을 실행 하 여 다시 시작할 수 있습니다.

```powershell
Resume-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
예:

```powershell
Resume-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

## <a name="debug-pipelines"></a>파이프라인 디버깅
Azure Data Factory toodebug 있습니다에 대 한 다양 한 기능을 제공 하 고 hello Azure 포털 및 Azure PowerShell을 사용 하 여 파이프라인을 해결 합니다.

> [! NOTE}는 훨씬 더 쉽게 사용 하 여 오류 모니터링 hello tootroubleshot & 관리 응용 프로그램입니다. Hello 응용 프로그램을 사용 하는 방법에 대 한 세부 정보를 참조 하십시오. [모니터링 하 고 hello 모니터링 및 관리 앱을 사용 하 여 데이터 팩터리 파이프라인 관리](data-factory-monitor-manage-app.md) 문서. 

### <a name="find-errors-in-a-pipeline"></a>파이프라인에서 오류 찾기
파이프라인에서 실패 하면 hello 활동 실행 hello hello 파이프라인에 의해 생성 되는 데이터 집합이 오류 상태에 hello 오류로 인해 합니다. 디버깅할 수 있으며 hello 다음 메서드를 사용 하 여 Azure Data Factory의 오류를 해결 합니다.

#### <a name="use-hello-azure-portal-toodebug-an-error"></a>Azure 포털 toodebug 오류가 hello를 사용 하 여
1. Hello에 **테이블** 블레이드에서 hello 있는 hello 문제 조각을 클릭 **상태** 도**실패**합니다.

   ![문제 조각이 있는 테이블 블레이드](./media/data-factory-monitor-manage-pipelines/table-blade-with-error.png)
2. Hello에 **데이터 조각을** 블레이드에서 hello 작업에 실패 한 실행을 클릭 합니다.

   ![오류가 있는 데이터 조각](./media/data-factory-monitor-manage-pipelines/dataslice-with-error.png)
3. Hello에 **활동 실행 정보** 블레이드에서 hello HDInsight 처리와 연결 된 hello 파일을 다운로드할 수 있습니다. 클릭 **다운로드** 상태/stderr toodownload hello 오류 로그 파일에 대 한 hello 오류에 대 한 세부 정보를 포함 합니다.

   ![오류가 있는 작업 실행 세부 정보 블레이드 ](./media/data-factory-monitor-manage-pipelines/activity-run-details-with-error.png)     

#### <a name="use-powershell-toodebug-an-error"></a>PowerShell toodebug 오류를 사용 하 여
1. **PowerShell**을 시작합니다.
2. Hello 실행 **Get AzureRmDataFactorySlice** toosee hello 조각 및 해당 상태 명령입니다. 조각을 hello 상태와 함께 표시 되어야 **실패**합니다.        

    ```powershell   
    Get-AzureRmDataFactorySlice [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime] <DateTime> [[-EndDateTime] <DateTime> ] [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```   
   예:

    ```powershell   
    Get-AzureRmDataFactorySlice -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime 2014-05-04 20:00:00
    ```

   **StartDateTime**을 파이프라인의 시작 시간으로 바꿉니다. 
3. 이제 hello 실행 **Get AzureRmDataFactoryRun** hello 조각에 대 한 hello 활동에 대 한 cmdlet tooget 세부 정보를 실행 합니다.

    ```powershell   
    Get-AzureRmDataFactoryRun [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime]
    <DateTime> [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```

    예:

    ```powershell   
    Get-AzureRmDataFactoryRun -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime "5/5/2014 12:00:00 AM"
    ```

    StartDateTime hello 값은 hello 이전 단계에서 기록해 놓은 hello 오류/문제가 조각에 대 한 hello 시작 시간입니다. hello 날짜 및 시간을 큰따옴표로 묶어야 합니다.
4. Toohello 다음과 비슷한 hello 오류에 대 한 세부 정보를 사용 하 여 출력을 표시 되어야 합니다.

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
5. Hello를 실행할 수 있습니다 **저장 AzureRmDataFactoryLog** hello hello 출력에서 참조 하 고 hello를 사용 하 여 hello 로그 파일을 다운로드 하는 Id 값을 사용 하 여 cmdlet **-DownloadLogsoption** hello cmdlet에 대 한 합니다.

    ```powershell
    Save-AzureRmDataFactoryLog -ResourceGroupName "ADF" -DataFactoryName "LogProcessingFactory" -Id "841b77c9-d56c-48d1-99a3-8c16c3e77d39" -DownloadLogs -Output "C:\Test"
    ```

## <a name="rerun-failures-in-a-pipeline"></a>파이프라인에서 실패한 항목 다시 실행

> [!IMPORTANT]
> 보다 쉽게 tootroubleshoot 오류 및 사용 하 여 실패 한 조각을 다시 실행된 hello 모니터링 및 관리 응용 프로그램. Hello 응용 프로그램을 사용 하는 방법에 대 한 세부 정보를 참조 하십시오. [모니터링 하 고 hello 모니터링 및 관리 앱을 사용 하 여 데이터 팩터리 파이프라인 관리](data-factory-monitor-manage-app.md)합니다. 

### <a name="use-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여
오류를 다시 실행할 수 toohello 오류 조각을 이동한 hello를 클릭 하 여 문제를 해결 하 고 파이프라인에서 오류가 발생 했습니다. 디버깅 후 **실행** hello 명령 모음에서 단추입니다.

![실패한 조각 다시 실행](./media/data-factory-monitor-manage-pipelines/rerun-slice.png)

경우에 hello 분할 영역에 유효성 검사 오류로 인해 실패 정책 (예를 들어 데이터 사용할 수 없는 경우), hello 오류를 수정 하 고 hello를 클릭 하 여 다시 유효성을 검사할 수 있습니다 **유효성 검사** hello 명령 모음에서 단추입니다.

![오류 수정 및 유효성 검사](./media/data-factory-monitor-manage-pipelines/fix-error-and-validate.png)

### <a name="use-azure-powershell"></a>Azure PowerShell 사용
Hello를 사용 하 여 오류를 다시 실행할 수 있습니다 **집합 AzureRmDataFactorySliceStatus** cmdlet. Hello 참조 [집합 AzureRmDataFactorySliceStatus](https://msdn.microsoft.com/library/mt603522.aspx) 구문과 hello cmdlet에 대 한 기타 세부 정보에 대 한 항목입니다.

**예제:**

hello 다음 설정 하는 예제 테이블 'DAWikiAggregatedData' too'Waiting hello에 대 한 모든 분할 영역의 hello 상태 ' hello Azure 데이터 팩터리에서 'WikiADF'.

'업데이트 유형' hello too'UpstreamInPipeline 설정 ', 즉, hello 테이블에 대 한 각 조각과 모든 hello 종속 (업스트림) 테이블의 상태 too'Waiting를 설정 하 는'. 이 매개 변수는 '개별'에 대 한 다른 가능한 값을 hello 합니다.

```powershell
Set-AzureRmDataFactorySliceStatus -ResourceGroupName ADF -DataFactoryName WikiADF -DatasetName DAWikiAggregatedData -Status Waiting -UpdateType UpstreamInPipeline -StartDateTime 2014-05-21T16:00:00 -EndDateTime 2014-05-21T20:00:00
```

## <a name="create-alerts"></a>경고 만들기
Azure는 Azure 리소스(예: 데이터 팩터리)가 생성, 업데이트 또는 삭제될 때 사용자 이벤트를 기록합니다. 이러한 이벤트에 경고를 만들 수 있습니다. Data Factory toocapture 다양 한 메트릭을 사용 하 여 및 메트릭에 대해 경고를 만들 수 있습니다. 실시간 모니터링을 위한 이벤트와 기록을 목적으로 하는 메트릭을 사용하는 것이 좋습니다.

### <a name="alerts-on-events"></a>이벤트에 대한 경고
Azure 이벤트는 Azure 리소스에서 일어나는 일에 대한 유용한 통찰력을 제공합니다. Azure Data Factory를 사용하면 다음 경우에 이벤트가 생성됩니다.

* 데이터 팩터리가 생성, 업데이트 또는 삭제될 때
* 데이터 처리("실행")가 시작/완료될 때
* 주문형 HDInsight 클러스터가 생성 또는 제거될 때

이러한 사용자 이벤트에 경고를 만들 수 있으며 toosend 전자 메일 알림 toohello 관리자 및 coadministrators hello 구독을 구성 합니다. 또한 hello 조건이 충족 되 면 전자 메일 알림을 tooreceive 해야 하는 사용자의 추가 전자 메일 주소를 지정할 수 있습니다. 이 기능은 실패에 대 한 알림 tooget을 데이터 팩터리 toocontinuously 모니터 않을 때 유용 합니다.

> [!NOTE]
> 현재 hello 포털 이벤트에 대해 경고를 표시 하지 않습니다. 사용 하 여 hello [모니터링 및 관리 앱](data-factory-monitor-manage-app.md) toosee 모든 경고 합니다.


#### <a name="specify-an-alert-definition"></a>경고 정의 지정:
toospecify 경고 정의 hello 작업에서 알림을 받는 toobe을 설명 하는 JSON 파일을 만듭니다. 다음 예제는 hello, hello 경고 hello RunFinished 작업에 대 한 전자 메일 알림을 보냅니다. 특정 toobe, hello 데이터 팩터리에서 실행 완료 된 후에 실행 하는 hello 실패 하는 경우 전자 메일 알림이 전송 됩니다 (상태 = FailedExecution).

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

제거할 수 있습니다 **하위 상태** hello toobe 특정 오류에서 경고를 표시 하지 않으려면 JSON 정의에서 합니다.

이 예제에서는 구독에서 모든 데이터 팩터리에 hello 경고를 설정합니다. 데이터 팩터리를 지정할 수 hello 경고 toobe 특정 데이터 팩터리에 대 한 설정 하려는 경우 **resourceUri** hello에 **dataSource**:

```JSON
"resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>"
```

hello 다음 표에서 hello 목록이 사용 가능한 작업 및 상태 (및 하위 상태).

| 작업 이름 | 가동 상태 | 하위 상태 |
| --- | --- | --- |
| RunStarted |Started |Starting |
| RunFinished |Failed / Succeeded |FailedResourceAllocation<br/><br/>Succeeded<br/><br/>FailedExecution<br/><br/>TimedOut<br/><br/><Canceled<br/><br/>FailedValidation<br/><br/>Abandoned |
| OnDemandClusterCreateStarted |Started | |
| OnDemandClusterCreateSuccessful |Succeeded | |
| OnDemandClusterDeleted |Succeeded | |

참조 [경고 규칙 만들기](https://msdn.microsoft.com/library/azure/dn510366.aspx) hello 예제에 사용 되는 hello JSON 요소에 대 한 세부 정보에 대 한 합니다.

#### <a name="deploy-hello-alert"></a>Hello 경고를 배포 합니다.
toodeploy hello 경고를 사용 하 여 hello Azure PowerShell cmdlet **새로 AzureRmResourceGroupDeployment**hello 다음 예제에에서 나온 것 처럼:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\ADFAlertFailedSlice.json  
```

리소스 그룹 배포 hello 성공적으로 완료 되 면 hello 메시지에 따라 표시 됩니다.

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
> Hello를 사용할 수 있습니다 [경고 규칙 만들기](https://msdn.microsoft.com/library/azure/dn510366.aspx) REST API toocreate 경고 규칙입니다. hello JSON 페이로드는 비슷한 toohello JSON의 예입니다.  


#### <a name="retrieve-hello-list-of-azure-resource-group-deployments"></a>Azure 리소스 그룹 배포의 hello 목록 검색
hello cmdlet을 사용 하 여의 Azure 리소스 그룹 배포를 배포 하는 tooretrieve hello 목록이 **Get AzureRmResourceGroupDeployment**hello 다음 예제에에서 나온 것 처럼:

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

#### <a name="troubleshoot-user-events"></a>사용자 이벤트 문제 해결
1. Hello를 클릭 한 후 생성 되는 모든 hello 이벤트를 볼 수 **메트릭 및 작업** 바둑판식으로 배열입니다.

    ![메트릭 및 작업 타일](./media/data-factory-monitor-manage-pipelines/metrics-and-operations-tile.png)
2. Hello 클릭 **이벤트** toosee hello 이벤트 바둑판식으로 배열 합니다.

    ![이벤트 타일](./media/data-factory-monitor-manage-pipelines/events-tile.png)
3. Hello에 **이벤트** 블레이드에서 등, 필터링 된 이벤트 및 이벤트에 대 한 세부 정보를 볼 수 있습니다.

    ![이벤트 블레이드](./media/data-factory-monitor-manage-pipelines/events-blade.png)
4. 클릭는 **작업** 하면 오류가 발생 하는 hello 작업 목록에 있습니다.

    ![작업 선택](./media/data-factory-monitor-manage-pipelines/select-operation.png)
5. 클릭는 **오류** hello 오류에 대 한 이벤트 toosee 세부 정보입니다.

    ![이벤트 오류](./media/data-factory-monitor-manage-pipelines/operation-error-event.png)

참조 [Azure Insight cmdlet](https://msdn.microsoft.com/library/mt282452.aspx) tooadd를 사용할 수 있는 PowerShell cmdlet에 대 한 가져오기 또는 경고를 제거 합니다. 다음은 hello를 사용 하 여의 몇 가지 예제 **Get AlertRule** cmdlet:

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

Hello g e t-h 명령 toosee 세부 정보 및 hello Get AlertRule cmdlet에 대 한 예제를 실행 합니다.

```powershell
get-help Get-AlertRule -detailed
```

```powershell
get-help Get-AlertRule -examples
```


Hello 경고 생성 이벤트에 표시 되 면 hello 포털 블레이드 있지만 하지 않는 전자 메일 알림이 제공, hello 전자 메일 주소를 지정 하는 외부 보낸 사람 으로부터 tooreceive 전자 메일 설정 되어 있는지 확인 합니다. hello 경고 메일 전자 메일 설정에 의해 차단 될 수 있습니다.

### <a name="alerts-on-metrics"></a>메트릭에 대한 경고
Data Factory에서 다양한 메트릭을 캡처하고 메트릭에 대한 경고를 만들 수 있습니다. 모니터링 및 데이터 팩터리에서 조각 hello에 대 한 메트릭을 다음 hello에 경고를 만들 수 있습니다.

* **실패한 실행**
* **성공한 실행**

이러한 메트릭 유용 및 tooget hello data factory에 전체 실패 및 성공에 대 한 개요를 실행 하는 데 도움이 됩니다. 메트릭은 조각을 실행할 때마다 내보내집니다. Hello 시간의 hello 맨 이러한 메트릭에 집계 되 고 tooyour 저장소 계정 푸시됩니다. tooenable 메트릭을 저장소 계정을 설정 합니다.

#### <a name="enable-metrics"></a>메트릭 사용
tooenable 메트릭을 클릭 hello에서 hello 다음 **Data Factory** 블레이드:

**모니터링** > **메트릭** > **진단 설정** > **진단**

![진단 링크](./media/data-factory-monitor-manage-pipelines/diagnostics-link.png)

Hello에 **진단** 블레이드에서 클릭 **에**hello 저장소 계정을 선택 하 고 클릭 **저장**합니다.

![진단 블레이드](./media/data-factory-monitor-manage-pipelines/diagnostics-blade.png)

Hello 메트릭 toobe hello에 대 한 tooone 시간 걸릴 수도 있습니다 **모니터링** 블레이드에서 메트릭을 집계 1 시간 마다 발생 하기 때문에 있습니다.

### <a name="set-up-an-alert-on-metrics"></a>메트릭에 대한 경고 설정:
Hello 클릭 **Data Factory 메트릭** 타일:

![데이터 팩터리 메트릭 타일](./media/data-factory-monitor-manage-pipelines/data-factory-metrics-tile.png)

Hello에 **메트릭을** 블레이드에서 클릭 **+ 추가 경고** hello 도구 모음입니다.
![데이터 팩터리 메트릭 블레이드 > 경고 추가](./media/data-factory-monitor-manage-pipelines/add-alert.png)

Hello에 **경고 규칙 추가** 페이지 수행 단계에 따라 hello 하 고 클릭 **확인**합니다.

* Hello 경고에 대 한 이름을 입력 하십시오 (예: "하지 못했다는 경고가").
* Hello 경고에 대 한 설명을 입력 하십시오 (예: "는 오류 발생 시 전자 메일 보내기").
* 메트릭을 선택합니다("실패한 실행" 대 "성공한 실행").
* 조건 및 임계값을 지정합니다.   
* Hello 기간을 지정 합니다.
* Tooowners, 참가자 및 독자 전자 메일을 보낼지 여부를 지정 합니다.

![데이터 팩터리 메트릭 블레이드 > 경고 규칙 추가](./media/data-factory-monitor-manage-pipelines/add-an-alert-rule.png)

Hello 경고 규칙은 성공적으로 추가 하 고 hello 블레이드를 닫습니다 hello hello 새 경고를 표시 **메트릭을** 블레이드입니다.

![데이터 팩터리 메트릭 블레이드 > 새 경고 추가됨](./media/data-factory-monitor-manage-pipelines/failed-alert-in-metric-blade.png)

또한 표시 hello hello 동안의 경고 수 **규칙 경고** 바둑판식으로 배열입니다. Hello 클릭 **규칙 경고** 바둑판식으로 배열입니다.

![데이터 팩터리 메트릭 블레이드 - 경고 규칙](./media/data-factory-monitor-manage-pipelines/alert-rules-tile-rules.png)

Hello에 **규칙 경고** 블레이드에서 모든 기존 경고를 참조 하십시오. 경고를 tooadd 클릭 **추가 경고** hello 도구 모음에서 합니다.

![경고 규칙 블레이드](./media/data-factory-monitor-manage-pipelines/alert-rules-blade.png)

### <a name="alert-notifications"></a>경고 알림
Hello 조건이 일치 하는 hello 경고 규칙이 hello 경고가 활성화 될 알리는 전자 메일을 구하십시오. Hello 문제가 해결 되 고 hello 경고 조건이 더 이상 일치 하지 않습니다, 후 hello 경고가 해결 된 라고 표시 된 전자 메일을 가져옵니다.

이 동작은 경고 규칙을 충족하는 모든 오류에 대해 알림이 전송되는 이벤트와는 다릅니다.

### <a name="deploy-alerts-by-using-powershell"></a>PowerShell을 사용하여 경고 배포
동일한 메트릭을 hello에 대 한 경고를 배포할 수 이벤트에 대 한 방법으로 합니다.

**경고 정의**

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

대체 *subscriptionId*, *resourceGroupName*, 및 *dataFactoryName* 적절 한 값으로 hello 샘플에서입니다.

*metricName*은 현재 두 가지 값을 지원합니다.

* FailedRuns
* SuccessfulRuns

**Hello 경고를 배포 합니다.**

toodeploy hello 경고를 사용 하 여 hello Azure PowerShell cmdlet **새로 AzureRmResourceGroupDeployment**hello 다음 예제에에서 나온 것 처럼:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\FailedRunsGreaterThan5.json
```

배포가 완료되면 다음과 같은 메시지가 표시됩니다.

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

Hello를 사용할 수도 있습니다 **추가 AlertRule** cmdlet toodeploy 경고 규칙입니다. Hello 참조 [추가 AlertRule](https://msdn.microsoft.com/library/mt282468.aspx) 세부 정보 및 예에 대 한 항목입니다.  

## <a name="move-a-data-factory-tooa-different-resource-group-or-subscription"></a>데이터 팩터리 tooa 다른 리소스 그룹 또는 구독 이동
Hello를 사용 하 여 데이터 팩터리 tooa 다른 리소스 그룹 또는 다른 구독을 이동할 수 **이동** 명령 모음 단추 데이터 팩터리의 hello 홈 페이지에 있습니다.

![데이터 팩터리 이동](./media/data-factory-monitor-manage-pipelines/MoveDataFactory.png)

(예: 경고 hello 데이터 팩터리와 연결 된), 관련 된 모든 리소스가 hello 데이터 팩터리와 함께 이동할 수도 있습니다.

![리소스 이동 대화 상자](./media/data-factory-monitor-manage-pipelines/MoveResources.png)
