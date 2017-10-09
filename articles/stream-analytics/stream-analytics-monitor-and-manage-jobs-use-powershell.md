---
title: "aaaMonitor powershell 스트림 분석 작업을 관리 하 고 | Microsoft Docs"
description: "자세한 내용은 방법 toouse Azure PowerShell 및 cmdlet toomonitor 및 스트림 분석 작업을 관리 합니다."
keywords: "azure powershell, azure powershell cmdlet, powershell 명령, powershell 스크립팅"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 514f454e-d18c-4081-8304-ab48577e15e8
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 44abc82f1c44a5ebc1701badd6547b84dac239b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-stream-analytics-jobs-with-azure-powershell-cmdlets"></a>Azure PowerShell cmdlet을 사용하여 Stream Analytics 작업 모니터링 및 관리
자세한 내용은 어떻게 toomonitor 및 기본 스트림 분석 작업을 실행 하는 Azure PowerShell cmdlet 및 powershell 스크립트를 사용 하 여 스트림 분석 리소스를 관리 합니다.

## <a name="prerequisites-for-running-azure-powershell-cmdlets-for-stream-analytics"></a>Stream Analytics에 Azure PowerShell cmdlet을 실행하기 위한 필수 조건
* 구독에서 Azure 리소스 그룹을 만듭니다. hello 다음은 샘플 Azure PowerShell 스크립트입니다. Azure PowerShell 정보는 [Azure PowerShell 설치 및 구성](/powershell/azure/overview)을 참조하세요.  

Azure PowerShell 0.9.8:  

         # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group if you have more than one subscription on your account.
        Select-AzureSubscription -SubscriptionName <subscription name>

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>

Azure PowerShell 1.0.  

         # Log in tooyour Azure account
        Login-AzureRmAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group.
        Get-AzureRmSubscription –SubscriptionName “your sub” | Select-AzureRmSubscription

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureRmResourceProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureRMResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>



> [!NOTE]
> 프로그래밍 방식으로 만든 Stream Analytics 작업은 기본적으로 모니터링이 설정되어 있지 않습니다.  Hello toohello 작업 모니터 페이지를 탐색 하 여 Azure 포털에서에서 모니터링을 수동으로 설정할 수 있습니다 및 있습니다 또는 hello 사용 단추를 클릭 하에 있는 hello 단계에 따라 프로그래밍 방식으로이 수행할 수 있는 [Azure 스트림 분석-모니터 스트림 분석을 프로그래밍 방식으로 작업](stream-analytics-monitor-jobs.md)합니다.
> 
> 

## <a name="azure-powershell-cmdlets-for-stream-analytics"></a>Stream Analytics용 Azure PowerShell cmdlet
hello 다음 Azure PowerShell cmdlet 사용된 toomonitor 수 하 고 Azure 스트림 분석 작업을 관리할 수 있습니다. Azure PowerShell에는 여러 버전이 있습니다. 
**Azure powershell 0.9.8은 나열 된 hello 첫 번째 명령은 hello 예제에서 Azure PowerShell 1.0에 대 한 hello 두 번째 명령이입니다.** Azure PowerShell 1.0 hello 명령을 항상 "AzureRM" hello 명령에서입니다.

### <a name="get-azurestreamanalyticsjob--get-azurermstreamanalyticsjob"></a>Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob
Hello Azure 구독 또는 지정 된 리소스 그룹에 정의 된 모든 스트림 분석 작업 나열 하거나 리소스 그룹 내에서 특정 작업에 대 한 작업 정보를 가져옵니다.

**예 1**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsJob

Azure PowerShell 1.0.  

    Get-AzureRMStreamAnalyticsJob

이 PowerShell 명령을 hello Azure 구독에서에서 모든 hello 스트림 분석 작업에 대 한 정보를 반환합니다.

**예 2**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

Azure PowerShell 1.0.  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

이 PowerShell 명령은 기본 중앙 미국 StreamAnalytics hello 리소스 그룹에서 모든 hello 스트림 분석 작업에 대 한 정보를 반환합니다.

**예 3**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

Azure PowerShell 1.0.  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

이 PowerShell 명령은 hello 리소스 그룹 StreamAnalytics 기본-중앙 미국 StreamingJob hello 스트림 분석 작업에 대 한 정보를 반환합니다.

### <a name="get-azurestreamanalyticsinput--get-azurermstreamanalyticsinput"></a>Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput
지정된 된 스트림 분석 작업에 정의 된 hello 입력의 모든 나열 하거나 특정 입력에 대 한 정보를 가져옵니다.

**예 1**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

Azure PowerShell 1.0.  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

이 PowerShell 명령을 StreamingJob hello 작업에 정의 된 모든 hello 입력에 대 한 정보를 반환 합니다.

**예 2**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

Azure PowerShell 1.0.  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

이 PowerShell 명령을 EntryStream StreamingJob hello 작업에 정의 된 명명 된 hello 입력에 대 한 정보를 반환 합니다.

### <a name="get-azurestreamanalyticsoutput--get-azurermstreamanalyticsoutput"></a>Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput
모든 지정된 된 스트림 분석 작업에 정의 된 hello 출력 나열 하거나 특정 출력에 대 한 정보를 가져옵니다.

**예 1**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

Azure PowerShell 1.0.  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

이 PowerShell 명령을 StreamingJob hello 작업에 정의 된 hello 출력에 대 한 정보를 반환 합니다.

**예 2**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

Azure PowerShell 1.0.  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

이 PowerShell 명령은 출력 StreamingJob hello 작업에 정의 된 명명 된 hello 출력에 대 한 정보를 반환 합니다.

### <a name="get-azurestreamanalyticsquota--get-azurermstreamanalyticsquota"></a>Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota
스트리밍 단위는 지정한 지역에서의 hello 할당량에 대 한 정보를 가져옵니다.

**예 1**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsQuota –Location "Central US" 

Azure PowerShell 1.0.  

    Get-AzureRMStreamAnalyticsQuota –Location "Central US" 

이 PowerShell 명령을 hello 중앙 미국 지역에 hello 할당량 및 스트리밍 단위 사용에 대 한 정보를 반환합니다.

### <a name="get-azurestreamanalyticstransformation--getazurermstreamanalyticstransformation"></a>Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation
Stream Analytics 작업에 정의된 특정 변환에 대한 정보를 가져옵니다.

**예 1**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

Azure PowerShell 1.0.  

    Get-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

이 PowerShell 명령을 StreamingJob StreamingJob hello 작업에서 호출 하는 hello 변환에 대 한 정보를 반환 합니다.

### <a name="new-azurestreamanalyticsinput--new-azurermstreamanalyticsinput"></a>New-AzureStreamAnalyticsInput | New-AzureRMStreamAnalyticsInput
Stream Analytics 작업 내에서 새 입력을 만들거나 지정한 기존 입력을 업데이트합니다.

hello hello 입력의 이름을 지정할 수 있습니다 hello 명령줄 또는 hello.json 파일에 있습니다. 모두 지정 된 경우 hello 명령줄의 hello 이름이 hello 파일에 하나 hello와 동일 hello 해야 합니다.

이미 존재 하는 입력 지정을 지정 하지 않는 경우 hello – Force 매개 변수 hello cmdlet 묻습니다 tooreplace 기존 입력 hello 여부.

Hello – Force 매개 변수 및 이름을 입력 하십시오. 기존, 확인 하지 않고 hello 입력 바뀝니다 지정을 지정 합니다.

Hello JSON 파일 구조와 내용을에 자세한 내용은 참조 toohello [입력 만들기 (Azure 스트림 분석)] [ msdn-rest-api-create-stream-analytics-input] hello 섹션 [스트림 분석 관리 REST API 참조 라이브러리][stream.analytics.rest.api.reference]합니다.

**예 1**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

Azure PowerShell 1.0.  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

이 PowerShell 명령은 Input.json hello 파일에서 새 입력을 만듭니다. 경우 hello 입력된 정의 파일에 지정 된 hello 이름 가진 기존 입력 이미 정의 되어 hello cmdlet은 메시지를 표시 여부 tooreplace 것입니다.

**예 2**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

Azure PowerShell 1.0.  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

이 PowerShell 명령을 EntryStream hello 작업에는 새 입력을 만듭니다. 경우이 이름 가진 기존 입력 이미 정의 되어 hello cmdlet은 메시지를 표시 여부 tooreplace 것입니다.

**예 3**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

Azure PowerShell 1.0.  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

이 PowerShell 명령은 hello 기존 입력된 소스 EntryStream hello 파일에서 정의 hello 사용 하 여 호출의 hello 정을 바꿉니다.

### <a name="new-azurestreamanalyticsjob--new-azurermstreamanalyticsjob"></a>New-AzureStreamAnalyticsJob | New-AzureRMStreamAnalyticsJob
Microsoft Azure에서 새 스트림 분석 작업을 만들거나 기존 지정 된 작업의 hello 정의 업데이트 합니다.

hello 작업의 hello 이름 hello 명령줄 또는 hello.json 파일에 지정할 수 있습니다. 모두 지정 된 경우 hello 명령줄의 hello 이름이 hello 파일에 하나 hello와 동일 hello 해야 합니다.

이미 존재 하는 작업 이름을 지정 하 고 지정 하지 않는 경우 hello – Force 매개 변수 hello cmdlet 묻습니다 tooreplace 기존 작업 hello 여부.

기존 작업 이름을 지정 하 고 hello – Force 매개 변수를 지정 하는 경우 hello 작업 정의 확인 하지 않고 대체 됩니다.

Hello JSON 파일 구조와 내용을에 자세한 내용은 참조 toohello [스트림 분석 작업 만들기] [ msdn-rest-api-create-stream-analytics-job] hello 섹션 [스트림 분석 관리 REST API 참조 라이브러리][stream.analytics.rest.api.reference]합니다.

**예 1**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

Azure PowerShell 1.0.  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

이 PowerShell 명령을 JobDefinition.json에 hello 정의에서 새 작업을 만듭니다. Hello 작업 정의 파일에 지정 된 hello 이름 사용 하는 기존 작업은 이미 정의 하는 경우 hello cmdlet은 메시지를 표시 여부 tooreplace 것입니다.

**예 2**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

Azure PowerShell 1.0.  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

이 PowerShell 명령은 StreamingJob에 대 한 hello 작업 정을 바꿉니다.

### <a name="new-azurestreamanalyticsoutput--new-azurermstreamanalyticsoutput"></a>New-AzureStreamAnalyticsOutput | New-AzureRMStreamAnalyticsOutput
Stream Analytics 작업 내에서 새 출력을 만들거나 기존 출력을 업데이트합니다.  

hello 출력의 hello 이름 hello 명령줄 또는 hello.json 파일에 지정할 수 있습니다. 모두 지정 된 경우 hello 명령줄의 hello 이름이 hello 파일에 하나 hello와 동일 hello 해야 합니다.

이미 존재 하는 출력을 지정 하 고 지정 하지 않는 경우 hello – Force 매개 변수 hello cmdlet 묻습니다 tooreplace hello 기존 출력 여부.

기존 출력 이름, 확인 하지 않고 hello 출력 바뀝니다 지정 하 고 hello – Force 매개 변수를 지정 하는 경우.

Hello JSON 파일 구조와 내용을에 자세한 내용은 참조 toohello [출력 만들기 (Azure 스트림 분석)] [ msdn-rest-api-create-stream-analytics-output] hello 섹션 [스트림 분석 관리 REST API 참조 라이브러리][stream.analytics.rest.api.reference]합니다.

**예 1**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

Azure PowerShell 1.0.  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

이 PowerShell 명령을 StreamingJob hello 작업에서 "output" 라는 새 출력을 만듭니다. 이 이름 가진 기존 출력은 이미 정의 하는 경우 hello cmdlet은 메시지를 표시 여부 tooreplace 것입니다.

**예 2**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

Azure PowerShell 1.0.  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

이 PowerShell 명령은 "출력" StreamingJob hello 작업에 대 한 hello 정을 바꿉니다.

### <a name="new-azurestreamanalyticstransformation--new-azurermstreamanalyticstransformation"></a>New-AzureStreamAnalyticsTransformation | New-AzureRMStreamAnalyticsTransformation
스트림 분석 작업 내에서 새 변환을 만들거나 기존 변환 hello를 업데이트 합니다.

hello 변환의 hello 이름 hello 명령줄 또는 hello.json 파일에 지정할 수 있습니다. 모두 지정 된 경우 hello 명령줄의 hello 이름이 hello 파일에 하나 hello와 동일 hello 해야 합니다.

이미 존재 하는 변환 지정을 지정 하지 않는 경우 hello – Force 매개 변수 hello cmdlet 묻습니다 tooreplace 기존 변환 hello 여부.

기존 변환 이름을 지정 하 고 hello – Force 매개 변수를 지정 하는 경우 hello 변환 확인 하지 않고 대체 됩니다.

Hello JSON 파일 구조와 내용을에 자세한 내용은 참조 toohello [변환 만들기 (Azure 스트림 분석)] [ msdn-rest-api-create-stream-analytics-transformation] hello 섹션 [스트림 분석 관리 REST API 참조 라이브러리][stream.analytics.rest.api.reference]합니다.

**예 1**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

Azure PowerShell 1.0.  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

이 PowerShell 명령은 StreamingJobTransform hello 작업 StreamingJob에에서 이라는 새 변환을 만듭니다. 경우 기존 변환이 이미 정의 되어이 이름의 hello cmdlet은 메시지를 표시 여부 tooreplace 것입니다.

**예 2**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

Azure PowerShell 1.0.  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

 이 PowerShell 명령은 hello 작업 StreamingJob에서에서 StreamingJobTransform의 hello 정을 바꿉니다.

### <a name="remove-azurestreamanalyticsinput--remove-azurermstreamanalyticsinput"></a>Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput
Microsoft Azure의 Stream Analytics 작업에서 특정 입력을 비동기적으로 삭제합니다.  
지정 하는 경우 hello – Force 매개 변수를 입력 하는 hello 없이 삭제 됩니다 확인 합니다.

**예 1**

Azure PowerShell 0.9.8:  

    Remove-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

Azure PowerShell 1.0.  

    Remove-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

제거 hello 입력된 EventStream StreamingJob hello 작업에서이 PowerShell 명령입니다.  

### <a name="remove-azurestreamanalyticsjob--remove-azurermstreamanalyticsjob"></a>Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob
Microsoft Azure에서 특정 Stream Analytics 작업을 비동기적으로 삭제합니다.  
지정 하는 경우 hello – Force 매개 변수 hello 작업 됩니다 확인 과정 없이 삭제 합니다.

**예 1**

Azure PowerShell 0.9.8:  

    Remove-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

Azure PowerShell 1.0.  

    Remove-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

이 PowerShell 명령을 hello 작업 StreamingJob을 제거 합니다.  

### <a name="remove-azurestreamanalyticsoutput--remove-azurermstreamanalyticsoutput"></a>Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput
Microsoft Azure의 Stream Analytics 작업에서 특정 출력을 비동기적으로 삭제합니다.  
지정 하는 경우 hello – Force 매개 변수 hello 출력 됩니다 확인 과정 없이 삭제 합니다.

**예 1**

Azure PowerShell 0.9.8:  

    Remove-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

Azure PowerShell 1.0.  

    Remove-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

이 PowerShell 명령 제거 hello StreamingJob hello 작업에서 출력을 출력 합니다.  

### <a name="start-azurestreamanalyticsjob--start-azurermstreamanalyticsjob"></a>Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob
Microsoft Azure에 Stream Analytics 작업을 비동기적으로 배포하고 시작합니다.

**예 1**

Azure PowerShell 0.9.8:  

    Start-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

Azure PowerShell 1.0.  

    Start-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

이 PowerShell 명령을 시작 작업을 사용자 지정 출력 시작 시간이 StreamingJob 설정 tooDecember 12, 2012, 12시 12분: 12 hello UTC입니다.

### <a name="stop-azurestreamanalyticsjob--stop-azurermstreamanalyticsjob"></a>Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob
Microsoft Azure에서 실행 중인 Stream Analytics 작업을 비동기적으로 중지하고 사용하던 리소스를 할당 취소합니다. hello 작업 정 및 메타 데이터는 계속 사용할 수 hello Azure 포털 및 관리 Api 모두를 통해 구독 내에서 hello 작업 수 편집 하 고 다시 시작 되도록 합니다. Hello 중지 상태에 있는 작업에 대 한 청구 되지 됩니다.

**예 1**

Azure PowerShell 0.9.8:  

    Stop-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

Azure PowerShell 1.0.  

    Stop-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

이 PowerShell 명령을 StreamingJob hello 작업을 중지합니다.  

### <a name="test-azurestreamanalyticsinput--test-azurermstreamanalyticsinput"></a>Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput
스트림 분석 tooconnect tooa의 테스트 hello 기능은 입력을 지정 합니다.

**예 1**

Azure PowerShell 0.9.8:  

    Test-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

Azure PowerShell 1.0.  

    Test-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

이 PowerShell 명령 테스트 hello 연결 상태는 hello EntryStream StreamingJob에를 입력 합니다.  

### <a name="test-azurestreamanalyticsoutput--test-azurermstreamanalyticsoutput"></a>Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput
스트림 분석 tooconnect tooa의 테스트 hello 기능은 출력을 지정 합니다.

**예 1**

Azure PowerShell 0.9.8:  

    Test-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

Azure PowerShell 1.0.  

    Test-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

이 PowerShell 명령 테스트 hello 연결 상태는 hello StreamingJob에서 출력을 출력 합니다.  

## <a name="get-support"></a>지원 받기
추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요. 

## <a name="next-steps"></a>다음 단계
* [스트림 분석 소개 tooAzure](stream-analytics-introduction.md)
* [Azure Stream Analytics 사용 시작](stream-analytics-real-time-fraud-detection.md)
* [Azure  Stream Analytics 작업 규모 지정](stream-analytics-scale-jobs.md)
* [Azure  Stream Analytics 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics 관리 REST API 참조](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[msdn-switch-azuremode]: http://msdn.microsoft.com/library/dn722470.aspx
[powershell-install]: http://azure.microsoft.com/documentation/articles/powershell-install-configure/
[msdn-rest-api-create-stream-analytics-job]: https://msdn.microsoft.com/library/dn834994.aspx
[msdn-rest-api-create-stream-analytics-input]: https://msdn.microsoft.com/library/dn835010.aspx
[msdn-rest-api-create-stream-analytics-output]: https://msdn.microsoft.com/library/dn835015.aspx
[msdn-rest-api-create-stream-analytics-transformation]: https://msdn.microsoft.com/library/dn835007.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

