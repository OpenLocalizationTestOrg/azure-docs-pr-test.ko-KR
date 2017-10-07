---
title: "webhook 사용 하 여 Azure 자동화 runbook aaaStarting | Microsoft Docs"
description: "에서 허용 하는 클라이언트 toostart runbook Azure 자동화에 대 한 HTTP 호출 webhook 합니다.  이 문서에서는 설명 방법을 toocreate는 webhook 방법과 toocall 하나의 toostart runbook입니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9b20237c-a593-4299-bbdc-35c47ee9e55d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: magoedte;bwren;sngun
ms.openlocfilehash: ca6cde66b3784ceb5d0bc5921cee87aea74cb150
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="starting-an-azure-automation-runbook-with-a-webhook"></a>웹후크를 사용하여 Azure Automation Runbook 시작
A *webhook* 사용 하면 특정 runbook toostart Azure 자동화에서 단일 HTTP 요청을 통해. 그러면 Visual Studio Team Services, GitHub, Microsoft Operations Management Suite 로그 분석 또는 사용자 지정 응용 프로그램 같은 외부 서비스 toostart runbook hello Azure 자동화 API를 사용 하 여 전체 솔루션을 구현 하지 않고 있습니다.  
![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)

runbook 시작의 webhook tooother 메서드를 비교할 수 [Azure 자동화에서 runbook 시작](automation-starting-a-runbook.md)

## <a name="details-of-a-webhook"></a>Webhook의 세부 정보
hello 다음 표에서 webhook에 대 한 구성 해야 하는 hello 속성.

| 속성 | 설명 |
|:--- |:--- |
| 이름 |이 사용자가 원하는 webhook에 대 한 이름을 노출 되지 않습니다. toohello 클라이언트를 제공할 수 있습니다.  하면 tooidentify hello Azure 자동화에서 runbook에 대 한만 사용 됩니다. <br>  모범 사례로, hello webhook 사용 하는 이름이 관련된 toohello 클라이언트를 지정 해야 합니다. |
| URL |hello webhook의 hello URL은 HTTP POST toostart hello runbook 호출 하는 클라이언트 hello 고유한 주소 toohello webhook을 연결 합니다.  Hello webhook을 만들 때 자동으로 생성 됩니다.  사용자 지정 URL은 지정할 수 없습니다. <br> <br>  hello URL hello runbook toobe 더 이상의 인증이 없는 제 3 자 시스템에 의해 호출을 허용 하는 보안 토큰을 포함 합니다. 따라서 암호처럼 취급해야 합니다.  보안상의 이유로 hello hello 시간 hello webhook에 Azure 포털의에서 URL이 만들어집니다 보기 hello만 할 수 있습니다. 나중에 사용할 안전한 위치에 hello URL에 유념 하십시오. |
| 만료 날짜 |각 webhook는 인증서처럼 만료 날짜가 있으며, 이 날짜가 되면 인증서를 더 이상 사용할 수 없습니다.  Hello webhook 만들어지면이 만료 날짜를 수정할 수 있습니다. |
| 사용 |webhook는 생성되었을 때 기본적으로 사용하도록 설정됩니다.  TooDisabled를 설정할 경우 클라이언트가 수 toouse 될 것입니다.  Hello를 설정할 수 있습니다 **Enabled** 속성이 hello webhook 또는 언제 든 지 한 번 만들 때 만들어집니다. |

### <a name="parameters"></a>매개 변수
webhook 해당 webhook hello runbook을 시작할 때 사용 되는 runbook 매개 변수의 값을 정의할 수 있습니다. hello webhook hello runbook의 모든 필수 매개 변수에 대 한 값을 포함 해야 하 고 선택적 매개 변수 값이 포함 될 수 있습니다. 매개 변수 값 구성 tooa webhook hello webhoook를 만든 후에 수정할 수 있습니다. 여러 연결 하는 webhook tooa 단일 runbook 각각 다른 매개 변수 값을 사용할 수 있습니다.

클라이언트는 webhook을 사용 하 여 runbook이 시작 되 면 hello webhook에 정의 된 hello 매개 변수 값을 재정의할 수 없습니다.  tooreceive 데이터 hello 클라이언트의 경우, runbook hello 라는 단일 매개 변수를 받아들일 수 **$WebhookData** 형식의 [object] 데이터를 포함 하는 hello 클라이언트 hello POST 요청에 포함 합니다.

![Webhookdata 속성](media/automation-webhooks/webhook-data-properties.png)

hello **$WebhookData** 개체 hello 다음과 같은 속성을 갖게 됩니다.

| 속성 | 설명 |
|:--- |:--- |
| WebhookName |hello webhook의 hello 이름입니다. |
| RequestHeader |Hello 들어오는 POST 요청의 hello 헤더를 포함 하는 해시 테이블입니다. |
| RequestBody |hello 들어오는 POST 요청의 본문 hello입니다.  문자열, JSON, XML 또는 인코딩된 데이터와 같은 서식을 유지합니다. hello runbook toowork 예상 되는 hello 데이터 형식으로 작성 되어야 합니다. |

Hello webhook 필요한 toosupport hello의 구성이 **$WebhookData** 매개 변수를 hello runbook tooaccept 필요 없는 것입니다.  Hello runbook hello 매개 변수를 정의 하지 않으면, hello 클라이언트에서 보낸 hello 요청의 세부 정보는 무시 됩니다.

Hello webhook을 만들 때 $WebhookData에 대 한 값을 지정 하면 해당 값은 재정의할 수 hello webhook hello 클라이언트가 POST 요청을 hello 데이터로 hello runbook을 시작할 때 hello 클라이언트 hello 요청 본문에 데이터를 포함 하지 않는 경우에 합니다.  webhook 이외의 메서드를 사용 하 여 $WebhookData를 가진 runbook을 시작 하는 경우에 hello runbook에서 인식 됩니다 $Webhookdata에 대 한 값을 제공할 수 있습니다.  이 값은 hello로 개체 여야 합니다. 동일한 [속성](#details-of-a-webhook) 으로 $Webhookdata는 webhook로 전달 하는 실제 WebhookData 작업 했던 마치 함께 해당 hello runbook 제대로 작동할 수 있도록 합니다.

예를 들어 경우 hello hello Azure 포털에서에서 runbook을 다음 시작 하 고 toopass WebhookData WebhookData 개체 이므로 테스트를 위해 몇 가지 예제를 사용할 것 전달 되어야 JSON으로 hello UI에에서 있습니다.

![UI에서의 WebhookData 매개 변수](media/automation-webhooks/WebhookData-parameter-from-UI.png)

Runbook hello 다음 hello WebhookData 매개 변수에 대 한 속성이 있는 경우 위의 hello에 대 한:

1. WebhookName: *MyWebhook*
2. RequestHeader: *From=Test User*
3. RequestBody: *[“VM1”, “VM2”]*

Hello 다음 hello WebhookData 매개 변수에 대 한 UI hello에 대 한 JSON 값을 전달 합니다.  

* {"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}

![UI에서 WebhookData 매개 변수 시작](media/automation-webhooks/Start-WebhookData-parameter-from-UI.png)

> [!NOTE]
> 모든 입력된 매개 변수 값 hello hello runbook 작업으로 기록 됩니다.  즉, 모든 hello 클라이언트가 hello webhook 요청에 제공 된 입력 액세스 toohello 자동화 작업으로 기록 되 고 사용 가능한 tooanyone 됩니다.  따라서 webhook 호출에 중요한 정보를 포함할 때는 주의해야 합니다.
>

## <a name="security"></a>보안
webhook의 hello 보안 toobe 호출을 허용 하는 보안 토큰을 포함 하는 URL의 hello 개인 정보에 의존 합니다. Azure 자동화 toohello 올바른 URL 구성으로 hello 요청에서 인증이 수행 하지 않습니다. 이러한 이유로 webhook 쓰일 수 없습니다는 다른 방법이 hello 요청 유효성 검사를 사용 하지 않고 매우 중요 한 기능을 수행 하는 runbook에 대 한 합니다.

호출 했는 webhook hello를 확인 하 여 hello runbook toodetermine 내에서 논리를 포함할 수 **WebhookName** $WebhookData hello 매개 변수 속성. hello runbook 수 추가 유효성 검사를 수행할 hello에 특정 한 정보를 검색 하 여 **RequestHeader** 또는 **RequestBody** 속성입니다.

또 다른 전략은 toohave hello runbook webhook 요청을 받았을 때 외부는 상태의 일부 유효성 검사를 수행 합니다.  예를 들어 새 커밋 tooa GitHub 리포지토리 있을 때마다 GitHub에 의해 호출 되는 runbook을 살펴보세요.  hello runbook에는 계속 하기 전에 새 커밋 실제로 발생 tooGitHub toovalidate를 연결할 수도 있습니다.

## <a name="creating-a-webhook"></a>webhook 만들기
다음 프로시저 toocreate hello Azure 포털에서에서 새 연결 하는 webhook tooa runbook hello를 사용 합니다.

1. Hello에서 **Runbook 블레이드에서** hello Azure 포털에서에서 클릭 webhook hello hello runbook tooview 해당 세부 정보 블레이드에서 시작 됩니다.
2. 클릭 **Webhook** hello 블레이드 tooopen hello의 hello 위쪽 **추가 Webhook** 블레이드입니다. <br>
   ![Webhooks 단추](media/automation-webhooks/webhooks-button.png)
3. 클릭 **새 webhook 만들기** tooopen hello **만들기 webhook 블레이드**합니다.
4. 지정 된 **이름**, **만료 날짜** hello webhook 및 사용 여부에 대 한 합니다. 이러한 속성에 대한 자세한 내용은 [webhook 세부 정보](#details-of-a-webhook) 를 참조하십시오.
5. Ctrl + C toocopy hello URL의 webhook hello와 hello 복사 아이콘을 클릭 합니다.  그런 다음 안전한 곳에 기록합니다.  **Hello webhook을 만든 후 다시 hello URL를 검색할 수 없습니다.** <br>
   ![Webhook URL](media/automation-webhooks/copy-webhook-url.png)
6. 클릭 **매개 변수** tooprovide hello runbook 매개 변수 값입니다.  Hello runbook은 필수 매개 변수를 다음 됩니다 수 toocreate hello webhook 값을 제공 하지 않는 한 합니다.
7. 클릭 **만들기** toocreate hello webhook 합니다.

## <a name="using-a-webhook"></a>webhook 사용
만들어진 후 webhook toouse 클라이언트 응용 프로그램 hello webhook에 대 한 hello URL 인 HTTP POST를 실행 해야 합니다.  형식에 따라 hello hello webhook의 hello 구문이 됩니다.

    http://<Webhook Server>/token?=<Token Value>

hello 클라이언트 hello hello POST 요청에서 반환 코드를 다음 중 하나를 받게 됩니다.  

| 코드 | 텍스트 | 설명 |
|:--- |:--- |:--- |
| 202 |수락됨 |hello 요청이 수락 되었음 및 hello runbook 성공적으로 대기 합니다. |
| 400 |잘못된 요청 |hello 다음 이유 중 하나에 대 한 hello 요청이 수락 되지 않았습니다. <ul> <li>hello webhook은 만료 되었습니다.</li> <li>hello webhook 비활성화 되어 있습니다.</li> <li>hello URL에 hello 토큰이 잘못 되었습니다.</li>  </ul> |
| 404 |찾을 수 없음 |hello 다음 이유 중 하나에 대 한 hello 요청이 수락 되지 않았습니다. <ul> <li>hello webhook은 찾을 수 없습니다.</li> <li>hello runbook은 찾을 수 없습니다.</li> <li>hello 계정은 찾을 수 없습니다.</li>  </ul> |
| 500 |내부 서버 오류 |hello URL 올바르지만 오류가 발생 했습니다.  Hello 요청을 다시 전송 하십시오. |

Hello webhook 응답 hello 작업 id를 JSON 형식에 다음과 같이 포함 hello 요청은 성공 하는 것으로 가정 합니다. 단일 작업 id를 포함 합니다 있지만 hello JSON 형식 잠재적인 향상 될 수 있습니다.

    {"JobIds":["<JobId>"]}  

hello 클라이언트 hello runbook 작업이 완료 될 때 또는 hello webhook에서의 완료 상태를 확인할 수 없습니다.  와 같은 다른 방법으로 hello 작업 id를 사용 하는이 정보를 확인할 수 [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) 또는 hello [Azure 자동화 API](https://msdn.microsoft.com/library/azure/mt163826.aspx)합니다.

### <a name="example"></a>예제
다음 예제는 hello는 webhook을 Windows PowerShell toostart runbook을 사용 합니다.  HTTP 요청을 만들 수 있는 모든 언어는 webhook를 사용할 수 있습니다. Windows PowerShell은 예제로 여기에서 사용됩니다.

hello runbook hello hello 요청 본문의 JSON으로 서식이 지정 된 가상 컴퓨터의 목록에 있어야 합니다. Hello 요청의 hello 헤더에서 시작 되 고 hello runbook 및 hello 날짜 및 시간에 시작 되 게 하는 방법에 대 한 정보도 포함 됩니다.      

    $uri = "https://s1events.azure-automation.net/webhooks?token=8ud0dSrSo%2fvHWpYbklW%3c8s0GrOKJZ9Nr7zqcS%2bIQr4c%3d"
    $headers = @{"From"="user@contoso.com";"Date"="05/28/2015 15:47:00"}

    $vms  = @(
                @{ Name="vm01";ServiceName="vm01"},
                @{ Name="vm02";ServiceName="vm02"}
            )
    $body = ConvertTo-Json -InputObject $vms

    $response = Invoke-RestMethod -Method Post -Uri $uri -Headers $headers -Body $body
    $jobid = ConvertFrom-Json $response


hello 다음 그림에 나와 hello 헤더 정보 (사용 하는 [Fiddler](http://www.telerik.com/fiddler) 추적)에서이 요청 합니다. 여기에 HTTP 요청의 표준 헤더 추가 toohello에 사용자 지정 날짜 및 추가 하는 헤더에서 합니다.  이러한 각 값은 hello에서 사용할 수 있는 toohello runbook **RequestHeaders** 속성 **WebhookData**합니다.

![Webhook 단추](media/automation-webhooks/webhook-request-headers.png)

hello 다음 그림에 나와 hello hello 요청 본문 (사용 하 여는 [Fiddler](http://www.telerik.com/fiddler) 추적) hello에서 사용할 수 있는 toohello runbook 즉 **RequestBody** 속성 **WebhookData**합니다. 기 때문에 해당 hello hello 요청 본문에 포함 된 hello 형식을 JSON으로 형식이 있습니다.     

![Webhook 단추](media/automation-webhooks/webhook-request-body.png)

hello 다음 그림은 hello 요청 Windows PowerShell 및 hello 결과 응답에서 보내는입니다.  hello 작업 id는 hello 응답 및 tooa 변환 된 문자열에서 추출 됩니다.

![Webhook 단추](media/automation-webhooks/webhook-request-response.png)

hello 다음 샘플 runbook hello 이전 예제에서는 요청을 수락 하 고 hello 요청 본문에 지정 된 hello 가상 컴퓨터를 시작 합니다.

    workflow Test-StartVirtualMachinesFromWebhook
    {
        param (
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {

            # Collect properties of WebhookData
            $WebhookName     =     $WebhookData.WebhookName
            $WebhookHeaders =     $WebhookData.RequestHeader
            $WebhookBody     =     $WebhookData.RequestBody

            # Collect individual headers. VMList converted from JSON.
            $From = $WebhookHeaders.From
            $VMList = ConvertFrom-Json -InputObject $WebhookBody
            Write-Output "Runbook started from webhook $WebhookName by $From."

            # Authenticate tooAzure resources
            $Cred = Get-AutomationPSCredential -Name 'MyAzureCredential'
            Add-AzureAccount -Credential $Cred

            # Start each virtual machine
            foreach ($VM in $VMList)
            {
                $VMName = $VM.Name
                Write-Output "Starting $VMName"
                Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName
            }
        }
        else {
            Write-Error "Runbook mean toobe started only from webhook."
        }
    }


## <a name="starting-runbooks-in-response-tooazure-alerts"></a>응답 tooAzure 경고에서 runbook 시작
Webhook 사용이 가능한 runbook 수 사용된 tooreact 너무[Azure 경고](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)합니다. 성능, 가용성 및 사용 하 여 hello Azure 경고 사용 같은 hello 통계를 수집 하 여 Azure의에서 리소스를 모니터링할 수 있습니다. 모니터링 메트릭이나 이벤트를 기반으로 Azure 리소스에 대한 경고를 받을 수 있습니다. 현재 자동화 계정은 메트릭만 지원합니다. 할당 hello 임계값 또는 hello 구성 된 이벤트는 트리거되지 다음 알림을 toohello 서비스 관리자 또는 공동 관리자 tooresolve hello 경고, 메트릭에 대 한 자세한 내용은 전송 되 고 이벤트 너무 참조 하십시오 지정 된 메트릭 hello 값을 초과 하는 경우[ Azure 경고](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)합니다.

외에도 Azure 경고를 사용 하 여 알림 시스템으로, runbook에 대 한 응답 tooalerts 시작 수 있습니다. Azure 자동화로 Azure 경고 hello 기능 toorun webhook 사용이 가능한 runbook을 제공합니다. 메트릭 초과 하는 경우 hello hello 경고 규칙이 활성화 되 고 트리거 hello 차례로 hello runbook을 실행 하는 자동화 webhook 임계값을 구성 합니다.

![Webhook](media/automation-webhooks/webhook-alert.jpg)

### <a name="alert-context"></a>경고 컨텍스트
이 컴퓨터의 CPU 사용률은 hello 주요 성능 메트릭 중 하나, 가상 컴퓨터와 같은 Azure 리소스를 가정해 봅니다. 이면 hello CPU 사용률이 100% 또는 특정 시간 보다 긴 기간 동안 toorestart hello 가상 컴퓨터 toofix hello 문제를 할 수 있습니다. 경고 규칙 toohello 가상 컴퓨터를 구성 하 여 해결할 수이 고이 규칙은 메트릭으로 CPU 비율 지정 됩니다. 예를 들어 CPU 백분율 여기 바로 수행 되지만 tooyour Azure를 구성할 수 있는 다른 많은 메트릭 리소스 및 hello 가상 컴퓨터를 다시 시작 되는 작업은이 문제를 toofix 수행 hello runbook tootake 다른 동작을 구성할 수 있습니다.

이 hello 경고 규칙이 활성화 되 고 트리거 hello webhook 사용이 가능한 runbook을 hello 경고 컨텍스트 toohello runbook을 보냅니다. [경고 컨텍스트](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) 포함 하 여 세부 정보를 포함 **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** 및 **타임 스탬프** hello runbook tooidentify hello 리소스에 있는 것을 받겠습니다 동작에 대 한 필요한 합니다. 상황에 맞는 hello의 hello 본문 부분에 포함 되어 경고 **WebhookData** 보낸된 toohello runbook 개체를 사용 하 여 액세스할 수 있습니다 **Webhook.RequestBody** 속성

### <a name="example"></a>예제
구독과 연결에는 Azure 가상 컴퓨터 만들기는 [toomonitor CPU 비율 메트릭을 경고](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)합니다. Hello 경고를 만드는 동안 hello webhook를 만드는 동안 생성 된 hello webhook URL이 hello 인 hello webhook 필드를 채울 있는지를 확인 합니다.

hello 다음 샘플 runbook이 트리거되 hello 경고 규칙이 활성화 되 고 hello runbook tooidentify hello 리소스에 있는 것을 받겠습니다 작업에 필요한 hello 경고 컨텍스트 매개 변수를 수집 합니다.

    workflow Invoke-RunbookUsingAlerts
    {
        param (      
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {   
            # Collect properties of WebhookData.
            $WebhookName    =   $WebhookData.WebhookName
            $WebhookBody    =   $WebhookData.RequestBody
            $WebhookHeaders =   $WebhookData.RequestHeader

            # Outputs information on hello webhook name that called This
            Write-Output "This runbook was started from webhook $WebhookName."


            # Obtain hello WebhookBody containing hello AlertContext
            $WebhookBody = (ConvertFrom-Json -InputObject $WebhookBody)
            Write-Output "`nWEBHOOK BODY"
            Write-Output "============="
            Write-Output $WebhookBody

            # Obtain hello AlertContext     
            $AlertContext = [object]$WebhookBody.context

            # Some selected AlertContext information
            Write-Output "`nALERT CONTEXT DATA"
            Write-Output "==================="
            Write-Output $AlertContext.name
            Write-Output $AlertContext.subscriptionId
            Write-Output $AlertContext.resourceGroupName
            Write-Output $AlertContext.resourceName
            Write-Output $AlertContext.resourceType
            Write-Output $AlertContext.resourceId
            Write-Output $AlertContext.timestamp

            # Act on hello AlertContext data, in our case restarting hello VM.
            # Authenticate tooyour Azure subscription using Organization ID toobe able toorestart that Virtual Machine.
            $cred = Get-AutomationPSCredential -Name "MyAzureCredential"
            Add-AzureAccount -Credential $cred
            Select-AzureSubscription -subscriptionName "Visual Studio Ultimate with MSDN"

            #Check hello status property of hello VM
            Write-Output "Status of VM before taking action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
            Write-Output "Restarting VM"

            # Restart hello VM by passing VM name and Service name which are same in this case
            Restart-AzureVM -ServiceName $AlertContext.resourceName -Name $AlertContext.resourceName
            Write-Output "Status of VM after alert is active and takes action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
        }
        else  
        {
            Write-Error "This runbook is meant tooonly be started from a webhook."  
        }  
    }



## <a name="next-steps"></a>다음 단계
* 다양 한 방법 toostart runbook에 대 한 세부 정보를 참조 하십시오. [Runbook 시작](automation-starting-a-runbook.md)합니다.
* Runbook 작업의 상태 보기 hello에 대 한 자세한 내용은 참조 너무[Azure 자동화에서 Runbook 실행](automation-runbook-execution.md)합니다.
* toouse Azure 자동화 tootake 작업 Azure 경고를 확인 하려면 어떻게 해야 toolearn [자동화 Runbook과 Azure VM 경고 재구성](automation-azure-vm-alert-integration.md)합니다.
