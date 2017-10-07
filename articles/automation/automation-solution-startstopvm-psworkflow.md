---
title: "Azure 자동화-PowerShell 워크플로로 aaaStarting 및 중지와 가상 컴퓨터 | Microsoft Docs"
description: "Runbook 중지 및 toostart 클래식 가상 컴퓨터를 포함 하 여 Azure 자동화 시나리오의 그래픽 버전입니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d380bd43-d45d-45af-a5b2-78e7f66263c3
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2016
ms.author: magoedte;bwren
redirect_url: https://docs.microsoft.com/azure/automation/automation-solution-vm-management
redirect_document_id: False
ms.openlocfilehash: 273631c7fc5ddb989b3bbdc82b470ac3af6ee482
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a>Azure 자동화 시나리오 - 가상 컴퓨터 시작 및 중지
이 Azure 자동화 시나리오 runbook toostart 및 중지 클래식 가상 컴퓨터를 포함합니다.  Hello 다음 중 하나에 대 한이 시나리오를 사용할 수 있습니다.  

* 사용자 환경에 수정 하지 않고 runbook을 hello를 사용 합니다.
* Hello runbook tooperform 사용자 지정 기능을 수정 합니다.  
* 전체 솔루션의 일부로 다른 runbook에서 hello runbook을 호출 합니다.
* 자습서 toolearn runbook 제작 개념으로 hello runbook을 사용 합니다.

> [!div class="op_single_selector"]
> * [그래픽](automation-solution-startstopvm-graphical.md)
> * [PowerShell 워크플로](automation-solution-startstopvm-psworkflow.md)
> 
> 

이 hello이이 시나리오의 PowerShell 워크플로 runbook 버전입니다. [그래픽 Runbook](automation-solution-startstopvm-graphical.md)을 사용하여 사용할 수도 있습니다.

## <a name="getting-hello-scenario"></a>Hello 시나리오를 가져오기
이 시나리오는 hello 다음 링크에서에서 다운로드할 수 있는 두 개의 PowerShell 워크플로 runbook으로 구성 됩니다.  Hello 참조 [그래픽 버전](automation-solution-startstopvm-graphical.md) 링크 toohello 그래픽 runbook에 대 한이 시나리오의 합니다.

| Runbook | 링크 | 형식 | 설명 |
|:--- |:--- |:--- |:--- |
| Start-AzureVMs |[Azure 클래식 VM 시작](https://gallery.technet.microsoft.com/Start-Azure-Classic-VMs-86ef746b) |PowerShell 워크플로 |Azure 구독의 모든 기존 가상 컴퓨터 또는 특정 서비스 이름의 모든 가상 컴퓨터를 시작합니다. |
| Stop-AzureVMs |[Azure 클래식 VM 중지](https://gallery.technet.microsoft.com/Stop-Azure-Classic-VMs-7a4ae43e) |PowerShell 워크플로 |자동화 계정의 모든 가상 컴퓨터 또는 특정 서비스 이름의 모든 가상 컴퓨터를 중지합니다. |

## <a name="installing-and-configuring-hello-scenario"></a>설치 하 고 hello 시나리오를 구성 합니다.
### <a name="1-install-hello-runbooks"></a>1. Hello runbook을 설치 합니다.
Hello runbook에 다운로드 한 후에 가져올 수의 hello 절차를 사용 하 여 [Runbook 가져오기](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook)합니다.

### <a name="2-review-hello-description-and-requirements"></a>2. 검토 hello 설명 및 요구 사항
hello runbook에 대 한 설명과 필요한 자산을 포함 하는 주석 처리 된 도움말 텍스트를 포함 합니다.  가져올 수도 있습니다 hello이 문서에서 동일한 정보입니다.

### <a name="3-configure-assets"></a>3. 자산 구성
hello runbook 자산을 만들고 적절 한 값으로 채우는 해야 다음 hello를 요구 합니다.

| 자산 형식 | 자산 이름 | 설명 |
|:--- |:--- |:--- |:--- |
| 자격 증명 |AzureCredential |Azure 구독 hello 기관 toostart 및 중지할 가상 컴퓨터에 있는 계정의 자격 증명을 포함 합니다.  Hello에 다른 자격 증명 자산을 지정할 수 또는 **자격 증명** hello의 매개 변수 **Add-azureaccount** 활동입니다. |
| 변수 |AzureSubscriptionId |Azure 구독 hello 구독 ID를 포함합니다. |

## <a name="using-hello-scenario"></a>Hello 시나리오를 사용 하 여
### <a name="parameters"></a>매개 변수
hello runbook 매개 변수 뒤 hello가 있어야 합니다.  모든 필수 매개 변수에 대한 값을 제공해야 하며 요구 사항에 따라 다른 매개 변수에 대한 값을 선택적으로 제공할 수 있습니다.

| 매개 변수 | 형식 | 필수 | 설명 |
|:--- |:--- |:--- |:--- |
| ServiceName |string |아니요 |값이 제공되면 해당 서비스 이름의 모든 가상 컴퓨터가 시작되거나 중지됩니다.  값이 제공 하는 경우 다음 hello Azure 구독이 있는 모든 클래식 가상 컴퓨터의 시작 또는 중지 합니다. |
| AzureSubscriptionIdAssetName |string |아니요 |Hello의 hello 이름을 포함 [변수 자산](#installing-and-configuring-the-scenario) Azure 구독 hello 구독 ID가 포함 된 합니다.  값을 지정하지 않으면 *AzureSubscriptionId* 가 사용됩니다. |
| AzureCredentialAssetName |string |아니요 |Hello의 hello 이름을 포함 [자격 증명 자산](#installing-and-configuring-the-scenario) runbook toouse hello에 대 한 hello 자격 증명을 포함 하는 합니다.  값을 지정하지 않으면 *AzureCredential* 이 사용됩니다. |

### <a name="starting-hello-runbooks"></a>Hello runbook 시작
Hello 방법 중 하나를 사용할 수 있습니다 [Azure 자동화에서 runbook 시작](automation-starting-a-runbook.md) toostart이이 시나리오에서는 hello runbook 중 하나입니다.

Windows PowerShell toorun을 사용 하 여 다음 명령 예제는 hello **StartAzureVMs** toostart hello 서비스 이름으로 모든 가상 컴퓨터 *MyVMService*합니다.

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Start-AzureVMs" –Parameters $params

### <a name="output"></a>출력
hello runbook은 [메시지를 출력](automation-runbook-output-and-messages.md) 시작 hello 여부 각 가상 컴퓨터를 나타내는 또는 stop 명령이 성공적으로 전송 합니다.  각 runbook에 대 한 hello 출력 toodetermine hello 결과에서 특정 문자열을 찾을 수 있습니다.  hello 가능한 출력 문자열은 다음 표에 hello에 나열 됩니다.

| Runbook | 조건 | Message |
|:--- |:--- |:--- |
| Start-AzureVMs |가상 컴퓨터 이미 실행 중 |MyVM 이미 실행 중 |
| Start-AzureVMs |가상 컴퓨터에 대한 시작 요청이 성공적으로 제출됨 |MyVM 시작됨 |
| Start-AzureVMs |가상 컴퓨터에 대한 시작 요청 실패 |MyVM toostart를 실패 했습니다. |
| Stop-AzureVMs |가상 컴퓨터가 이미 중지됨 |MyVM 이미 중지됨 |
| Stop-AzureVMs |가상 컴퓨터에 대한 중지 요청이 성공적으로 제출됨 |MyVM 중지됨 |
| Stop-AzureVMs |가상 컴퓨터에 대한 중지 요청 실패 |MyVM toostop를 실패 했습니다. |

예를 들어 runbook에서 코드 조각을 다음 hello 시도 toostart hello 서비스 이름으로 모든 가상 컴퓨터 *MyServiceName*합니다.  요청 실패 시작 hello 중에 오류 동작을 수행할 수 있습니다.

    $results = Start-AzureVMs -ServiceName "MyServiceName"
    foreach ($result in $results) {
        if ($result -like "* has been started" ) {
            # Action tootake in case of success.
        }
        else {
            # Action tootake in case of error.
        }
    }


## <a name="detailed-breakdown"></a>자세한 분석
다음은이 시나리오에서는 hello runbook의 상세한 분석 합니다.  이 정보를 사용 하면 tooeither hello runbook 또는 임원의 정당한 toolearn 작성 직접 자동화 시나리오에 대 한 사용자 지정 합니다.

### <a name="parameters"></a>매개 변수
    param (
        [Parameter(Mandatory=$false)]
        [String]  $AzureCredentialAssetName = 'AzureCredential',

        [Parameter(Mandatory=$false)]
        [String] $AzureSubscriptionIdAssetName = 'AzureSubscriptionId',

        [Parameter(Mandatory=$false)]
        [String] $ServiceName
    )

hello 워크플로가 시작 hello에 대 한 hello 값을 가져오는 [입력 매개 변수](#using-the-scenario)합니다.  Hello 자산 이름을 입력 하지 않은 경우 기본 이름이 사용 됩니다.

### <a name="output"></a>출력
    # Returns strings with status messages
    [OutputType([String])]

이 줄 hello runbook의 hello 출력 문자열 되도록 선언 합니다.  이것은 필요 하지 않지만 hello runbook으로 사용 된 경우에 대 한 가장 좋은 방법은 [자식 runbook](automation-child-runbooks.md) 부모 runbook hello 출력을 파악할 수 있도록 tooexpect를 입력 합니다.

### <a name="authentication"></a>인증
    # Connect tooAzure and select hello subscription toowork against
    $Cred = Get-AutomationPSCredential -Name $AzureCredentialAssetName
    $null = Add-AzureAccount -Credential $Cred -ErrorAction Stop
    $SubId = Get-AutomationVariable -Name $AzureSubscriptionIdAssetName
    $null = Select-AzureSubscription -SubscriptionId $SubId -ErrorAction Stop

다음 줄 hello 설정 hello [자격 증명](automation-credentials.md) 및 hello 나머지 hello runbook에 사용할 Azure 구독.
사용 하 여 먼저 **Get-automationpscredential** hello Azure 구독에에서 액세스할 수 있는 자격 증명 hello toostart 및 중지할 가상 컴퓨터를 포함 하는 tooget hello 자산입니다. **추가 AzureAccount** 다음이 자산 tooset hello 자격 증명을 사용 합니다.  hello 출력 hello runbook 출력에 포함 되지 않도록 tooa 더미 변수가 할당 됩니다.  

hello 변수 자산 ID를 검색 한 다음 hello 구독과 **Get-automationvariable** 및 사용 하 여 설정 하는 hello 구독 **Select-azuresubscription**합니다.

### <a name="get-vms"></a>VM 가져오기
    # If there is a specific cloud service, then get all VMs in hello service,
    # otherwise get all VMs in hello subscription.
    if ($ServiceName)
    {
        $VMs = Get-AzureVM -ServiceName $ServiceName
    }
    else
    {
        $VMs = Get-AzureVM
    }

**Get-azurevm** 사용 되는 tooretrieve hello runbook은 작동 하는 hello 가상 컴퓨터입니다.  Hello에는 값을 제공 하는 경우 **ServiceName** 입력 해당 서비스 이름 가진 변수를 다음 유일한 hello 가상 컴퓨터를 검색 합니다.  **ServiceName** 을 비워두면 모든 가상 컴퓨터가 검색됩니다.

### <a name="startstop-virtual-machines-and-send-output"></a>가상 컴퓨터 시작/중지 및 출력 보내기
    # Start each of hello stopped VMs
    foreach ($VM in $VMs)
    {
        if ($VM.PowerState -eq "Started")
        {
            # hello VM is already started, so send notice
            Write-Output ($VM.InstanceName + " is already running")
        }
        else
        {
            # hello VM needs toobe started
            $StartRtn = Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName -ErrorAction Continue

            if ($StartRtn.OperationStatus -ne 'Succeeded')
            {
                # hello VM failed toostart, so send notice
                Write-Output ($VM.InstanceName + " failed toostart")
            }
            else
            {
                # hello VM started, so send notice
                Write-Output ($VM.InstanceName + " has been started")
            }
        }
    }

다음 줄 hello 각 가상 컴퓨터 단계별로 실행 합니다.  먼저 hello **PowerState** hello의 가상 컴퓨터는 선택 된 toosee 이미 있으면 실행 또는 hello runbook에 따른 중지 합니다.  Hello 대상 상태에 이미 있으면 hello runbook 끝나고 toooutput, 메시지가 전송 됩니다.  그렇지 않은 경우 다음 **Start-azurevm** 또는 **Stop-azurevm** hello 요청 저장된 tooa 변수의 hello 결과 함께 사용 되는 tooattempt toostart 또는 중지 hello 가상 컴퓨터가 있습니다.  메시지가는 성공적으로 전송 hello 요청 toostart 또는 중지 여부를 지정 toooutput 전송 됩니다.

## <a name="next-steps"></a>다음 단계
* 자식 runbook 작업에 대해 자세히 toolearn 참조 [Azure 자동화에서 자식 runbook](automation-child-runbooks.md)
* 에 대해 더 알아봅니다 toolearn 문제를 해결 하는 동안 runbook 실행 및 로깅 toohelp 메시지가 출력, 참조 [Runbook 출력 및 Azure 자동화에서 메시지](automation-runbook-output-and-messages.md)

