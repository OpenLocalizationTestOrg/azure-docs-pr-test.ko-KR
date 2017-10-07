---
title: "Azure 네트워크 감시자 문제 해결에 aaaMonitor VPN 게이트웨이 | Microsoft Docs"
description: "이 문서에서는 Azure Automation 및 Network Watcher로 온-프레미스 연결을 진단하는 방법을 설명합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: a607d0c862ea1be63c687717f0c5dc137db58a43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-vpn-gateways-with-network-watcher-troubleshooting"></a>Azure Network Watcher 문제 해결로 VPN Gateway 모니터링

중요 한 tooprovide 신뢰할 수 있는 서비스 toocustomers는 네트워크 성능에 대 한 깊은 통찰력을 얻는입니다. 따라서 중요 한 toodetect 네트워크 중단 조건 신속 하 게 사용 되며 toomitigate hello 중단 조건 수정 작업을 수행 합니다. Azure 자동화 tooimplement 있으며 runbook을 통해 프로그래밍 방식으로 작업을 실행 합니다. Azure Automation을 사용하면 지속적인 자동 관리 네트워크 모니터링 및 경고를 수행하는 완벽한 작성법이 만들어집니다.

## <a name="scenario"></a>시나리오

hello hello 이미지를 수행 하는 시나리오는 다중 계층 응용 프로그램와 VPN 게이트웨이와 터널을 사용 하 여 설정 프레미스 연결에 합니다. Hello VPN Gateway가 가동 되 고 실행 되는 중요 한 toohello 응용 프로그램 성능입니다.

Runbook의 hello VPN 터널을 리소스 문제 해결 API toocheck hello를 사용 하 여 연결 터널 상태에 대 한 연결 상태에 대 한 스크립트 toocheck 만들어집니다. Hello 상태가 비정상, 전자 메일 트리거 tooadministrators를 전송 됩니다.

![예제 시나리오][scenario]

이 시나리오에서는 다음을 수행합니다.

- Runbook 호출 hello 만들기 `Start-AzureRmNetworkWatcherResourceTroubleshooting` tootroubleshoot 연결 상태 cmdlet
- 일정 toohello runbook을 연결

## <a name="before-you-begin"></a>시작하기 전에

이 시나리오를 시작 하기 전에 다음 필수 구성 요소는 hello가 있어야 합니다.

- Azure에서 Azure Automation 계정. Hello 자동화 계정에는 hello 최신 모듈이 역시 hello AzureRM.Network 모듈 확인 하십시오. tooadd 해야 할 경우 hello 모듈 갤러리 hello AzureRM.Network 모듈은 사용할 수 있는 것 tooyour 자동화 계정.
- Azure Automation에 구성된 자격 증명 집합이 있어야 합니다. [Azure Automation 보안](../automation/automation-security-overview.md)에서 자세히 알아보세요.
- Azure Automation에 정의된 유효한 SMTP 서버(Office 365, 온-프레미스 전자 메일 또는 기타) 및 자격 증명
- Azure에 구성된 Virtual Network 게이트웨이입니다.
- 기존 컨테이너 toostore hello로 기존 저장소 계정에 기록 됩니다.

> [!NOTE]
> hello 이미지 앞에 표시 된 hello 인프라도 제공 되며이 문서에 포함 된 hello 단계를 통해 생성 되지 않습니다.

### <a name="create-hello-runbook"></a>Hello runbook 만들기

hello 첫 번째 단계 tooconfiguring hello 예제 toocreate hello runbook입니다. 이 예제에서는 실행 계정을 사용합니다. 실행 계정에 대 한 toolearn 방문 [Azure 실행 계정 사용 하 여 Runbook 인증](../automation/automation-sec-configure-azure-runas-account.md)

### <a name="step-1"></a>1단계

Hello에 자동화 tooAzure 이동 [Azure 포털](https://portal.azure.com) 클릭 **Runbook**

![자동화 계정 개요][1]

### <a name="step-2"></a>2단계

클릭 **runbook을 추가할** hello runbook의 toostart hello 생성 프로세스입니다.

![Runbook 블레이드][2]

### <a name="step-3"></a>3단계

아래 **빠른 생성**, 클릭 **새 runbook을 만들** toocreate hello runbook입니다.

![Runbook 추가 블레이드][3]

### <a name="step-4"></a>4단계

이 단계에서는 받을 hello runbook 이름, hello 예제에서 호출 **Get VPNGatewayStatus**합니다. 중요 한 toogive hello runbook 설명이 포함 된 이름이 되며 표준 PowerShell 명명 표준을 따르기 된 이름을 지정 하는 것이 좋습니다. 이 예제에 대 한 hello runbook 유형을 **PowerShell**, hello 다른 옵션은 PowerShell 워크플로, 그래픽 및 그래픽 PowerShell 워크플로 합니다.

![Runbook 블레이드][4]

### <a name="step-5"></a>5단계

이 단계에서는 hello runbook 만들어지고, 다음 코드 예제는 hello 모든 hello hello 예제에 필요한 코드를 제공 합니다. hello 코드에 포함 된 항목 hello \<값\> toobe 구독에서 hello 값으로 대체 해야 합니다.

클릭으로 사용 하 여 hello 다음 코드 **저장**

```PowerShell
# Set these variables toohello proper values for your environment
$o365AutomationCredential = "<Office 365 account>"
$fromEmail = "<from email address>"
$toEmail = "<tooemail address>"
$smtpServer = "<smtp.office365.com>"
$smtpPort = 587
$runAsConnectionName = "<AzureRunAsConnection>"
$subscriptionId = "<subscription id>"
$region = "<Azure region>"
$vpnConnectionName = "<vpn connection name>"
$vpnConnectionResourceGroup = "<resource group name>"
$storageAccountName = "<storage account name>"
$storageAccountResourceGroup = "<resource group name>"
$storageAccountContainer = "<container name>"

# Get credentials for Office 365 account
$cred = Get-AutomationPSCredential -Name $o365AutomationCredential

# Get hello connection "AzureRunAsConnection "
$servicePrincipalConnection=Get-AutomationConnection -Name $runAsConnectionName

"Logging in tooAzure..."
Add-AzureRmAccount `
    -ServicePrincipal `
    -TenantId $servicePrincipalConnection.TenantId `
    -ApplicationId $servicePrincipalConnection.ApplicationId `
    -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
"Setting context tooa specific subscription"
Set-AzureRmContext -SubscriptionId $subscriptionId

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $region }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name $vpnConnectionName -ResourceGroupName $vpnConnectionResourceGroup
$sa = Get-AzureRmStorageAccount -Name $storageAccountName -ResourceGroupName $storageAccountResourceGroup 
$storagePath = "$($sa.PrimaryEndpoints.Blob)$($storageAccountContainer)"
$result = Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath $storagePath

if($result.code -ne "Healthy")
    {
        $body = "Connection for $($connection.name) is: $($result.code) `n$($result.results[0].summary) `nView hello logs at $($storagePath) toolearn more."
        Write-Output $body
        $subject = "$($connection.name) Status"
        Send-MailMessage `
        -too$toEmail `
        -Subject $subject `
        -Body $body `
        -UseSsl `
        -Port $smtpPort `
        -SmtpServer $smtpServer `
        -From $fromEmail `
        -BodyAsHtml `
        -Credential $cred
    }
else
    {
    Write-Output ("Connection Status is: $($result.code)")
    }
```

### <a name="step-6"></a>6단계

일정에 따라 해야 hello runbook을 저장 한 후 tooit tooautomate hello runbook의 시작 부분 hello를 연결 합니다. toostart hello 프로세스 클릭 **일정**합니다.

![6단계][6]

## <a name="link-a-schedule-toohello-runbook"></a>일정 toohello runbook을 연결

새 일정이 생성되어야 합니다. 클릭 **일정 tooyour runbook을 연결**합니다.

![7단계][7]

### <a name="step-1"></a>1단계

Hello에 **일정** 블레이드에서 클릭 **새 일정을 만들려면**

![8단계][8]

### <a name="step-2"></a>2단계

Hello에 **새 일정** 블레이드 채우기 hello 일정 정보입니다. 설정할 수 있는 hello 값 hello 목록 뒤에 있습니다.

- **이름** -hello hello 일정의 이름입니다.
- **설명** -hello 일정에 대 한 설명을 합니다.
- **시작** -이 값은 날짜, 시간 및 hello 시간 hello 일정 트리거를 구성 하는 표준 시간대의 조합입니다.
- **되풀이** -hello 일정 반복이이 값을 결정 합니다.  유효한 값은 **한 번** 또는 **되풀이**입니다.
- **되풀이 모든** -hello 시간, 일, 주 또는 월의 hello 일정 되풀이 간격입니다.
- **만료 설정** -hello 값 hello 일정 또는 만료 되어야 하는 경우를 결정 합니다. 너무 설정할 수 있습니다**예** 또는 **아니요**합니다. 유효한 날짜 및 시간 toobe 예 선택 하면 제공 됩니다.

> [!NOTE]
> 다른 간격으로 (즉, 15, 30, hello 시간 후 45 분) 여러 일정을 만들어야 합니다 toohave 매시간 보다 더 자주 실행 하는 runbook, 필요한 경우

![9단계][9]

### <a name="step-3"></a>3단계

Toosave hello 일정 toohello runbook 저장을 클릭 합니다.

![10단계][10]

## <a name="next-steps"></a>다음 단계

사용자가 이해 하는 방법에 했으므로 tootrigger 패킷 VM 경고에 방문 하 여 캡처 하는 방법을 알아보려면 Azure 자동화 된 toointegrate 네트워크 감시자 해결 [Azure 네트워크 감시자경고트리거된패킷캡처만들기](network-watcher-alert-triggered-packet-capture.md).

<!-- images -->
[scenario]: ./media/network-watcher-monitor-with-azure-automation/scenario.png
[1]: ./media/network-watcher-monitor-with-azure-automation/figure1.png
[2]: ./media/network-watcher-monitor-with-azure-automation/figure2.png
[3]: ./media/network-watcher-monitor-with-azure-automation/figure3.png
[4]: ./media/network-watcher-monitor-with-azure-automation/figure4.png
[5]: ./media/network-watcher-monitor-with-azure-automation/figure5.png
[6]: ./media/network-watcher-monitor-with-azure-automation/figure6.png
[7]: ./media/network-watcher-monitor-with-azure-automation/figure7.png
[8]: ./media/network-watcher-monitor-with-azure-automation/figure8.png
[9]: ./media/network-watcher-monitor-with-azure-automation/figure9.png
[10]: ./media/network-watcher-monitor-with-azure-automation/figure10.png
