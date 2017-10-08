---
title: "Azure 자동화에서 runbook 사용 하 여 로그 분석 데이터 aaaCollecting | Microsoft Docs"
description: "로그 분석에서 분석할 hello OMS 리포지토리에 toocollect 데이터 Azure 자동화에서에서 runbook을 만들를 안내 과정을 단계별로 자습서입니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: operations-management-suite
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2017
ms.author: bwren
ms.openlocfilehash: e644dc3ef20fb1e930cae02e0fd44ccca31dc13d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-data-in-log-analytics-with-an-azure-automation-runbook"></a>Azure Automation Runbook을 사용하여 Log Analytics에서 데이터 수집
에이전트의 [데이터 원본](../log-analytics/log-analytics-data-sources.md)을 비롯한 다양한 원본에서 Log Analytics으로 대량의 데이터를 수집할 수 있고 [Azure에서 수집된 데이터](../log-analytics/log-analytics-azure-storage.md)도 가져올 수 있습니다.  Toocollect 데이터 필요한 되지 않는 이러한 표준 원본을 통해 액세스할 수 있는 경우에 시나리오가 있습니다.  이러한 경우 hello를 사용할 수 있습니다 [HTTP 데이터 수집기 API](../log-analytics/log-analytics-data-collector-api.md) 모든 REST API 클라이언트에서 toowrite 데이터 tooLog 분석 합니다.  일반적인 메서드 tooperform이 데이터 컬렉션에서 Azure 자동화에서 runbook을 사용 하 합니다.   

이 자습서를 만들고 toowrite 데이터 tooLog 분석 Azure 자동화에서에서 runbook 예약 hello 프로세스를 안내 합니다.


## <a name="prerequisites"></a>필수 조건
이 시나리오에는 Azure 구독에서 구성 된 리소스를 다음 hello가 필요 합니다.  둘 다 무료 계정일 수 있습니다.

- [Log Analytics 작업 영역](../log-analytics/log-analytics-get-started.md)
- [Azure Automation 계정](../automation/automation-offering-get-started.md)

## <a name="overview-of-scenario"></a>시나리오의 개요
이 자습서에서는 Automation 작업에 대한 정보를 수집하는 Runbook을 작성합니다.  Azure 자동화의 Runbook은 powershell을 구현 때문에 작성 하 고 hello Azure 자동화 편집기에서 스크립트를 테스트 하 여 시작 합니다.  Hello 필요한 정보를 수집 중인를 확인 한 후에 해당 데이터 tooLog 분석을 작성 하 고 hello 사용자 지정 데이터 형식을 확인 합니다.  마지막으로, 일정 toostart hello runbook을 정기적으로 만듭니다.

> [!NOTE]
> 이 runbook 하지 않고 Azure 자동화 toosend 작업 정보 tooLog 분석을 구성할 수 있습니다.  이 시나리오는 주로 사용 되는 toosupport hello 자습서 있으며 hello 데이터 tooa 테스트 작업 영역을 보내는 것이 좋습니다.  


## <a name="1-install-data-collector-api-module"></a>1. 데이터 수집기 API 모듈 설치
모든 [hello HTTP 데이터 수집기 API에서에서 요청](../log-analytics/log-analytics-data-collector-api.md#create-a-request) 권한 부여 헤더를 포함 하 고 적절 하 게 지정 해야 합니다.  Runbook에서이 수행할 수 있지만이 프로세스를 간소화 하는 모듈을 사용 하 여 필요한 코드의 hello 양을 줄일 수 있습니다.  사용할 수 있는 하나의 모듈은 [OMSIngestionAPI 모듈](https://www.powershellgallery.com/packages/OMSIngestionAPI) hello PowerShell 갤러리에에서 있습니다.

toouse는 [모듈](../automation/automation-integration-modules.md) runbook에서는 설치 해야 자동화 계정에서 합니다.  동일한 계정을 사용 하 여 수 hello에서 모든 runbook hello hello 모듈의 함수입니다.  Automation 계정에서 **자산** > **모듈** > **모듈 추가**를 선택하여 새 모듈을 설치할 수 있습니다.  

hello PowerShell 갤러리 하지만 제공 빠른 옵션 toodeploy 모듈 직접 tooyour 자동화 계정이 자습서에 대 한 해당 옵션을 사용할 수 있도록 합니다.  

![OMSIngestionAPI 모듈](media/operations-management-suite-runbook-datacollect/OMSIngestionAPI.png)

1. 너무 이동[PowerShell 갤러리](https://www.powershellgallery.com/)합니다.
2. **OMSIngestionAPI**를 검색합니다.
3. Hello 클릭 **tooAzure 자동화 배포** 단추입니다.
4. 자동화 계정을 선택 하 고 클릭 **확인** tooinstall hello 모듈입니다.


## <a name="2-create-automation-variables"></a>2. Automation 변수 만들기
[Automation 변수](..\automation\automation-variables.md)는 Automation 계정의 모든 Runbook에서 사용할 수 있는 값을 포함합니다.  Runbook 자세히 만드는 유연한 toochange를 허용 하 여 이러한 값을 편집 하지 않고도 실제 runbook hello 합니다. Hello HTTP 데이터 수집기 API의에서 모든 요청 hello ID와 키의 hello OMS 작업 영역을 차지 하며 변수 자산은 이상적인 toostore이이 정보입니다.  

![variables](media/operations-management-suite-runbook-datacollect/variables.png)

1. Hello Azure 포털에서에서 tooyour 자동화 계정을 이동 합니다.
2. **공유 리소스**에서 **변수**를 선택합니다.
2. 클릭 **변수 추가** 다음 표에 hello에 hello 두 변수를 만듭니다.

| 속성 | 작업 영역 ID 값 | 작업 영역 키 값 |
|:--|:--|:--|
| 이름 | WorkspaceId | WorkspaceKey |
| 유형 | 문자열 | 문자열 |
| 값 | 로그 분석 작업의 작업 영역 ID hello에 붙여 넣습니다. | 주 가상 컴퓨터 또는 보조 키의 로그 분석 작업 영역 hello를 사용 하 여 붙여 넣습니다. |
| 암호화 | 아니요 | 예 |



## <a name="3-create-runbook"></a>3. runbook 만들기

Azure 자동화 편집기를 편집 하 고 runbook을 테스트할 수 있는 hello 포털에 있습니다.  Hello 옵션 toouse hello 스크립트 편집기 toowork와 있는 [PowerShell 직접](../automation/automation-edit-textual-runbook.md) 또는 [그래픽 runbook을 만들](../automation/automation-graphical-authoring-intro.md)합니다.  이 자습서에서는 PowerShell 스크립트를 사용합니다. 

![Runbook 편집](media/operations-management-suite-runbook-datacollect/edit-runbook.png)

1. Tooyour 자동화 계정을 이동 합니다.  
2. **Runbook** > **Runbook 추가** > **새 Runbook 만들기**를 클릭합니다.
3. Hello runbook 이름에 대 한 입력 **수집-자동화 작업**합니다.  Hello runbook 형식 선택 **PowerShell**합니다.
4. 클릭 **만들기** toocreate hello runbook 및 시작 hello 편집기입니다.
5. 복사한 hello hello runbook에 코드를 다음을 붙여 넣습니다.  Hello 코드 설명 hello 스크립트에서 toohello 메모를 참조 하십시오.
    
        # Get information required for hello automation account from parameter values when hello runbook is started.
        Param
        (
            [Parameter(Mandatory = $True)]
            [string]$resourceGroupName,
            [Parameter(Mandatory = $True)]
            [string]$automationAccountName
        )
        
        # Authenticate toohello Automation account using hello Azure connection created when hello Automation account was created.
        # Code copied from hello runbook AzureAutomationTutorial.
        $connectionName = "AzureRunAsConnection"
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         
        Add-AzureRmAccount `
            -ServicePrincipal `
            -TenantId $servicePrincipalConnection.TenantId `
            -ApplicationId $servicePrincipalConnection.ApplicationId `
            -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
        
        # Set hello $VerbosePreference variable so that we get verbose output in test environment.
        $VerbosePreference = "Continue"
        
        # Get information required for Log Analytics workspace from Automation variables.
        $customerId = Get-AutomationVariable -Name 'WorkspaceID'
        $sharedKey = Get-AutomationVariable -Name 'WorkspaceKey'
        
        # Set hello name of hello record type.
        $logType = "AutomationJob"
        
        # Get hello jobs from hello past hour.
        $jobs = Get-AzureRmAutomationJob -ResourceGroupName $resourceGroupName -AutomationAccountName $automationAccountName -StartTime (Get-Date).AddHours(-1)
        
        if ($jobs -ne $null) {
            # Convert hello job data toojson
            $body = $jobs | ConvertTo-Json
        
            # Write hello body tooverbose output so we can inspect it if verbose logging is on for hello runbook.
            Write-Verbose $body
        
            # Send hello data tooLog Analytics.
            Send-OMSAPIIngestionFile -customerId $customerId -sharedKey $sharedKey -body $body -logType $logType -TimeStampField CreationTime
        }


## <a name="4-test-runbook"></a>4. Runbook 테스트
Azure 자동화 너무 환경이 포함 되어[runbook을 테스트](../automation/automation-testing-runbook.md) 게시 하기 전에.  Hello runbook에서 수집 하는 hello 데이터를 검사할 수 있으며를 쓰는지 tooLog 분석 게시 하기 전에 예상 대로 tooproduction 확인 수 있습니다. 
 
![Runbook 테스트](media/operations-management-suite-runbook-datacollect/test-runbook.png)

6. 클릭 **저장** toosave hello runbook입니다.
1. 클릭 **테스트 창** hello 테스트 환경에서 tooopen hello runbook입니다.
3. Runbook에 매개 변수가 있으므로 증명된 tooenter 값에 대 한 것입니다.  Hello 리소스 그룹의 hello 이름을 입력 하 고 hello 자동화 계정에서 진행 중인 toocollect 작업 정보입니다.
4. 클릭 **시작** toohello hello runbook을 시작 합니다.
3. hello runbook의 상태로 시작 됩니다 **큐 대기** 너무 상태가 되기 전에**실행**합니다.  
3. hello runbook에 대 한 json 형식으로 수집 하는 hello 작업 자세한 출력을 표시 되어야 합니다.  작업이 목록에 없으면 다음 되었을 수 있습니다 지난 1 시간 동안 hello에 hello 자동화 계정에서 만든 작업이 없습니다.  Hello 자동화 계정의 모든 runbook을 시작 해 보십시오 하 고 hello 테스트를 다시 수행 합니다.
4. Hello 출력 명령 tooLog 분석을 게시 하는 hello의 모든 오류를 표시 하지 않음을 확인 합니다.  메시지와 비슷한 toohello 다음이 있어야 합니다.

    ![POST 출력](media/operations-management-suite-runbook-datacollect/post-output.png)

## <a name="5-verify-records-in-log-analytics"></a>5. Log Analytics의 레코드 확인
테스트에서는 hello runbook이 완료 된 hello 출력 성공적으로 받았음을 확인 되 면 hello 레코드를 사용 하 여 만든 있는지 확인할 수 있습니다는 [로그 분석에서 로그 검색](../log-analytics/log-analytics-log-searches.md)합니다.

![로그 출력](media/operations-management-suite-runbook-datacollect/log-output.png)

1. Hello Azure 포털에서에서 로그 분석 작업 영역을 선택 합니다.
2. **로그 검색**을 클릭합니다.
3. 다음 명령을 형식 hello `Type=AutomationJob_CL` hello 검색 단추를 클릭 합니다. Note hello 레코드 종류에는 hello 스크립트에 지정 되지 않은 _CL 포함 됩니다.  해당 접미사는 자동으로 추가 된 toohello 로그 형식 tooindicate는 사용자 지정 로그 형식입니다.
4. 해당 hello runbook이 예상 대로 작동 나타내는 반환 하는 하나 이상의 레코드가 표시 됩니다.


## <a name="6-publish-hello-runbook"></a>6. Hello runbook을 게시
Toopublish 해당 hello runbook이 제대로 작동을 확인 한 후 해야 되므로 프로덕션 환경에서 실행할 수 있습니다.  Tooedit 계속 하 고 hello 게시 된 버전을 수정 하지 않고 hello runbook을 테스트할 수 있습니다.  

![Runbook 게시](media/operations-management-suite-runbook-datacollect/publish-runbook.png)

1. Tooyour 자동화 계정을 반환 합니다.
2. **Runbook**을 클릭하고 **Collect-Automation-jobs**를 선택합니다.
3. **편집**, **게시**를 차례로 클릭합니다.
4. 클릭 **예** 묻는 tooverify toooverwrite hello를 이전에 사용할 버전을 게시 하는 경우.

## <a name="7-set-logging-options"></a>7. 로깅 옵션 설정 
테스트를 위해 수 tooview 있었습니다 [자세한 정보를 출력](../automation/automation-runbook-output-and-messages.md#message-streams) hello 스크립트에 hello $VerbosePreference 변수를 설정 합니다.  프로덕션 hello runbook에 대 한 tooset hello 로깅 속성 tooview 자세한 정보를 출력 하려는 경우 필요 합니다.  이 자습서에 사용 된 hello runbook에 대 한 hello json 데이터 분석 tooLog 송신할이 표시 됩니다.

![로깅 및 추적](media/operations-management-suite-runbook-datacollect/logging.png)

1. Runbook에 대 한 hello 속성에서 선택 **로깅 및 추적** 아래 **Runbook 설정**합니다.
2. 에 대 한 hello 설정을 변경 **상세 레코드를 기록** 너무**에**합니다.
3. **Save**를 클릭합니다.

## <a name="8-schedule-runbook"></a>8. Runbook 예약
hello 가장 일반적인 방법은 toostart 모니터링 데이터를 수집 하는 runbook은 tooschedule 것 toorun 자동으로 합니다.  만들어서이 작업을 수행는 [Azure 자동화의 일정](../automation/automation-schedules.md) 및 tooyour runbook을 연결 합니다.

![Runbook 예약](media/operations-management-suite-runbook-datacollect/schedule-runbook.png)

1. Runbook에 대 한 hello 속성에서 선택 **일정** 아래 **리소스**합니다.
2. 클릭 **일정을 추가할** > **일정 tooyour runbook을 연결** > **새 일정을 만들려면**합니다.
5. Hello hello 일정 및 클릭에 대 한 값을 뒤에 형식 **만들기**합니다.

| 속성 | 값 |
|:--|:--|
| 이름 | AutomationJobs-Hourly |
| Starts | 언제 든 지 5 분 이상 지난 hello 현재 시간을 선택 합니다. |
| 되풀이 | Recurring |
| Recur every | 1시간 |
| Set expiration | 아니요 |

Hello 일정을 만든 후 tooset hello 매개 변수 값이이 일정 hello runbook 시작 될 때마다 사용 해야 합니다.

6. **매개 변수 및 실행 설정 구성**을 클릭합니다.
7. **ResourceGroupName** 및 **AutomationAccountName**에 대한 값을 입력합니다.
8. **확인**을 클릭합니다. 

## <a name="9-verify-runbook-starts-on-schedule"></a>9. Runbook이 일정에 맞게 시작되는지 확인
Runbook이 시작될 때마다 [작업이 만들어지고](../automation/automation-runbook-execution.md) 모든 출력이 로깅됩니다.  사실, 이들은 runbook hello 동일한 작업을 수집 하는 hello입니다.  Hello 일정에 대 한 hello 시작 시간 경과 된 후 hello hello runbook 작업을 확인 하 여 예상 대로 해당 hello runbook 시작을 확인할 수 있습니다.

![작업](media/operations-management-suite-runbook-datacollect/jobs.png)

1. Runbook에 대 한 hello 속성에서 선택 **작업** 아래 **리소스**합니다.
2. 시작 된 각 시간 hello runbook에 대 한 작업 목록이 표시 됩니다.
3. 세부 정보 hello 작업 tooview 중 하나를 클릭 합니다.
4. 클릭 **모든 로그** tooview hello 로그 및 hello runbook에서 출력 합니다.
5. Toohello 아래쪽 toofind 아래 항목 비슷한 toohello 이미지를 스크롤하십시오.<br>![자세한 정보 표시](media/operations-management-suite-runbook-datacollect/verbose.png)
6. 이 항목을 클릭 tooview hello tooLog 분석 보낸 json 데이터를 자세히 설명 합니다.



## <a name="next-steps"></a>다음 단계
- 사용 하 여 [뷰 디자이너](../log-analytics/log-analytics-view-designer.md) 표시 뷰 toocreate hello toohello 로그 분석 저장소 수집한 데이터입니다.
- runbook을 패키지는 [관리 솔루션](operations-management-suite-solutions-creating.md) toodistribute toocustomers 합니다.
- [Log Analytics](https://docs.microsoft.com/azure/log-analytics/)에 대해 자세히 알아보기
- [Azure Automation](https://docs.microsoft.com/azure/automation/)에 대해 자세히 알아보기
- Hello에 대 한 자세한 [HTTP 데이터 수집기 API](../log-analytics/log-analytics-data-collector-api.md)합니다.
