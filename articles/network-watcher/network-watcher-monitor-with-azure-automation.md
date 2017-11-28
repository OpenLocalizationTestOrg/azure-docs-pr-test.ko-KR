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
# <a name="monitor-vpn-gateways-with-network-watcher-troubleshooting"></a><span data-ttu-id="a33ce-103">Azure Network Watcher 문제 해결로 VPN Gateway 모니터링</span><span class="sxs-lookup"><span data-stu-id="a33ce-103">Monitor VPN gateways with Network Watcher troubleshooting</span></span>

<span data-ttu-id="a33ce-104">중요 한 tooprovide 신뢰할 수 있는 서비스 toocustomers는 네트워크 성능에 대 한 깊은 통찰력을 얻는입니다.</span><span class="sxs-lookup"><span data-stu-id="a33ce-104">Gaining deep insights on your network performance is critical tooprovide reliable services toocustomers.</span></span> <span data-ttu-id="a33ce-105">따라서 중요 한 toodetect 네트워크 중단 조건 신속 하 게 사용 되며 toomitigate hello 중단 조건 수정 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a33ce-105">It is therefore critical toodetect network outage conditions quickly and take corrective action toomitigate hello outage condition.</span></span> <span data-ttu-id="a33ce-106">Azure 자동화 tooimplement 있으며 runbook을 통해 프로그래밍 방식으로 작업을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a33ce-106">Azure Automation enables you tooimplement and run a task in a programmatic fashion through runbooks.</span></span> <span data-ttu-id="a33ce-107">Azure Automation을 사용하면 지속적인 자동 관리 네트워크 모니터링 및 경고를 수행하는 완벽한 작성법이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="a33ce-107">Using Azure Automation creates a perfect recipe for performing continuous and proactive network monitoring and alerting.</span></span>

## <a name="scenario"></a><span data-ttu-id="a33ce-108">시나리오</span><span class="sxs-lookup"><span data-stu-id="a33ce-108">Scenario</span></span>

<span data-ttu-id="a33ce-109">hello hello 이미지를 수행 하는 시나리오는 다중 계층 응용 프로그램와 VPN 게이트웨이와 터널을 사용 하 여 설정 프레미스 연결에 합니다.</span><span class="sxs-lookup"><span data-stu-id="a33ce-109">hello scenario in hello following image is a multi-tiered application, with on premises connectivity established using a VPN Gateway and tunnel.</span></span> <span data-ttu-id="a33ce-110">Hello VPN Gateway가 가동 되 고 실행 되는 중요 한 toohello 응용 프로그램 성능입니다.</span><span class="sxs-lookup"><span data-stu-id="a33ce-110">Ensuring hello VPN Gateway is up and running is critical toohello applications performance.</span></span>

<span data-ttu-id="a33ce-111">Runbook의 hello VPN 터널을 리소스 문제 해결 API toocheck hello를 사용 하 여 연결 터널 상태에 대 한 연결 상태에 대 한 스크립트 toocheck 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="a33ce-111">A runbook is created with a script toocheck for connection status of hello VPN tunnel, using hello Resource Troubleshooting API toocheck for connection tunnel status.</span></span> <span data-ttu-id="a33ce-112">Hello 상태가 비정상, 전자 메일 트리거 tooadministrators를 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a33ce-112">If hello status is not healthy, an email trigger is sent tooadministrators.</span></span>

![예제 시나리오][scenario]

<span data-ttu-id="a33ce-114">이 시나리오에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a33ce-114">This scenario will:</span></span>

- <span data-ttu-id="a33ce-115">Runbook 호출 hello 만들기 `Start-AzureRmNetworkWatcherResourceTroubleshooting` tootroubleshoot 연결 상태 cmdlet</span><span class="sxs-lookup"><span data-stu-id="a33ce-115">Create a runbook calling hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet tootroubleshoot connection status</span></span>
- <span data-ttu-id="a33ce-116">일정 toohello runbook을 연결</span><span class="sxs-lookup"><span data-stu-id="a33ce-116">Link a schedule toohello runbook</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a33ce-117">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="a33ce-117">Before you begin</span></span>

<span data-ttu-id="a33ce-118">이 시나리오를 시작 하기 전에 다음 필수 구성 요소는 hello가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a33ce-118">Before you start this scenario, you must have hello following pre-requisites:</span></span>

- <span data-ttu-id="a33ce-119">Azure에서 Azure Automation 계정.</span><span class="sxs-lookup"><span data-stu-id="a33ce-119">An Azure automation account in Azure.</span></span> <span data-ttu-id="a33ce-120">Hello 자동화 계정에는 hello 최신 모듈이 역시 hello AzureRM.Network 모듈 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="a33ce-120">Ensure that hello automation account has hello latest modules and also has hello AzureRM.Network module.</span></span> <span data-ttu-id="a33ce-121">tooadd 해야 할 경우 hello 모듈 갤러리 hello AzureRM.Network 모듈은 사용할 수 있는 것 tooyour 자동화 계정.</span><span class="sxs-lookup"><span data-stu-id="a33ce-121">hello AzureRM.Network module is available in hello module gallery if you need tooadd it tooyour automation account.</span></span>
- <span data-ttu-id="a33ce-122">Azure Automation에 구성된 자격 증명 집합이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a33ce-122">You must have a set of credentials configure in Azure Automation.</span></span> <span data-ttu-id="a33ce-123">[Azure Automation 보안](../automation/automation-security-overview.md)에서 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="a33ce-123">Learn more at [Azure Automation security](../automation/automation-security-overview.md)</span></span>
- <span data-ttu-id="a33ce-124">Azure Automation에 정의된 유효한 SMTP 서버(Office 365, 온-프레미스 전자 메일 또는 기타) 및 자격 증명</span><span class="sxs-lookup"><span data-stu-id="a33ce-124">A valid SMTP server (Office 365, your on-premises email or another) and credentials defined in Azure Automation</span></span>
- <span data-ttu-id="a33ce-125">Azure에 구성된 Virtual Network 게이트웨이입니다.</span><span class="sxs-lookup"><span data-stu-id="a33ce-125">A configured Virtual Network Gateway in Azure.</span></span>
- <span data-ttu-id="a33ce-126">기존 컨테이너 toostore hello로 기존 저장소 계정에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a33ce-126">An existing storage account with an existing container toostore hello logs in.</span></span>

> [!NOTE]
> <span data-ttu-id="a33ce-127">hello 이미지 앞에 표시 된 hello 인프라도 제공 되며이 문서에 포함 된 hello 단계를 통해 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a33ce-127">hello infrastructure depicted in hello preceding image is for illustration purposes and are not created with hello steps contained in this article.</span></span>

### <a name="create-hello-runbook"></a><span data-ttu-id="a33ce-128">Hello runbook 만들기</span><span class="sxs-lookup"><span data-stu-id="a33ce-128">Create hello runbook</span></span>

<span data-ttu-id="a33ce-129">hello 첫 번째 단계 tooconfiguring hello 예제 toocreate hello runbook입니다.</span><span class="sxs-lookup"><span data-stu-id="a33ce-129">hello first step tooconfiguring hello example is toocreate hello runbook.</span></span> <span data-ttu-id="a33ce-130">이 예제에서는 실행 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a33ce-130">This example uses a run-as account.</span></span> <span data-ttu-id="a33ce-131">실행 계정에 대 한 toolearn 방문 [Azure 실행 계정 사용 하 여 Runbook 인증](../automation/automation-sec-configure-azure-runas-account.md)</span><span class="sxs-lookup"><span data-stu-id="a33ce-131">toolearn about run-as accounts, visit [Authenticate Runbooks with Azure Run As account](../automation/automation-sec-configure-azure-runas-account.md)</span></span>

### <a name="step-1"></a><span data-ttu-id="a33ce-132">1단계</span><span class="sxs-lookup"><span data-stu-id="a33ce-132">Step 1</span></span>

<span data-ttu-id="a33ce-133">Hello에 자동화 tooAzure 이동 [Azure 포털](https://portal.azure.com) 클릭 **Runbook**</span><span class="sxs-lookup"><span data-stu-id="a33ce-133">Navigate tooAzure Automation in hello [Azure portal](https://portal.azure.com) and click **Runbooks**</span></span>

![자동화 계정 개요][1]

### <a name="step-2"></a><span data-ttu-id="a33ce-135">2단계</span><span class="sxs-lookup"><span data-stu-id="a33ce-135">Step 2</span></span>

<span data-ttu-id="a33ce-136">클릭 **runbook을 추가할** hello runbook의 toostart hello 생성 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="a33ce-136">Click **Add a runbook** toostart hello creation process of hello runbook.</span></span>

![Runbook 블레이드][2]

### <a name="step-3"></a><span data-ttu-id="a33ce-138">3단계</span><span class="sxs-lookup"><span data-stu-id="a33ce-138">Step 3</span></span>

<span data-ttu-id="a33ce-139">아래 **빠른 생성**, 클릭 **새 runbook을 만들** toocreate hello runbook입니다.</span><span class="sxs-lookup"><span data-stu-id="a33ce-139">Under **Quick Create**, click **Create a new runbook** toocreate hello runbook.</span></span>

![Runbook 추가 블레이드][3]

### <a name="step-4"></a><span data-ttu-id="a33ce-141">4단계</span><span class="sxs-lookup"><span data-stu-id="a33ce-141">Step 4</span></span>

<span data-ttu-id="a33ce-142">이 단계에서는 받을 hello runbook 이름, hello 예제에서 호출 **Get VPNGatewayStatus**합니다.</span><span class="sxs-lookup"><span data-stu-id="a33ce-142">In this step, we give hello runbook a name, in hello example it is called **Get-VPNGatewayStatus**.</span></span> <span data-ttu-id="a33ce-143">중요 한 toogive hello runbook 설명이 포함 된 이름이 되며 표준 PowerShell 명명 표준을 따르기 된 이름을 지정 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a33ce-143">It is important toogive hello runbook a descriptive name, and recommended giving it a name that follows standard PowerShell naming standards.</span></span> <span data-ttu-id="a33ce-144">이 예제에 대 한 hello runbook 유형을 **PowerShell**, hello 다른 옵션은 PowerShell 워크플로, 그래픽 및 그래픽 PowerShell 워크플로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a33ce-144">hello runbook type for this example is **PowerShell**, hello other options are Graphical, PowerShell workflow, and Graphical PowerShell workflow.</span></span>

![Runbook 블레이드][4]

### <a name="step-5"></a><span data-ttu-id="a33ce-146">5단계</span><span class="sxs-lookup"><span data-stu-id="a33ce-146">Step 5</span></span>

<span data-ttu-id="a33ce-147">이 단계에서는 hello runbook 만들어지고, 다음 코드 예제는 hello 모든 hello hello 예제에 필요한 코드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a33ce-147">In this step hello runbook is created, hello following code example provides all hello code needed for hello example.</span></span> <span data-ttu-id="a33ce-148">hello 코드에 포함 된 항목 hello \<값\> toobe 구독에서 hello 값으로 대체 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a33ce-148">hello items in hello code that contain \<value\> need toobe replaced with hello values from your subscription.</span></span>

<span data-ttu-id="a33ce-149">클릭으로 사용 하 여 hello 다음 코드 **저장**</span><span class="sxs-lookup"><span data-stu-id="a33ce-149">Use hello following code as click **Save**</span></span>

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

### <a name="step-6"></a><span data-ttu-id="a33ce-150">6단계</span><span class="sxs-lookup"><span data-stu-id="a33ce-150">Step 6</span></span>

<span data-ttu-id="a33ce-151">일정에 따라 해야 hello runbook을 저장 한 후 tooit tooautomate hello runbook의 시작 부분 hello를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a33ce-151">Once hello runbook is saved, a schedule must be linked tooit tooautomate hello start of hello runbook.</span></span> <span data-ttu-id="a33ce-152">toostart hello 프로세스 클릭 **일정**합니다.</span><span class="sxs-lookup"><span data-stu-id="a33ce-152">toostart hello process, click **Schedule**.</span></span>

![6단계][6]

## <a name="link-a-schedule-toohello-runbook"></a><span data-ttu-id="a33ce-154">일정 toohello runbook을 연결</span><span class="sxs-lookup"><span data-stu-id="a33ce-154">Link a schedule toohello runbook</span></span>

<span data-ttu-id="a33ce-155">새 일정이 생성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a33ce-155">A new schedule must be created.</span></span> <span data-ttu-id="a33ce-156">클릭 **일정 tooyour runbook을 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="a33ce-156">Click **Link a schedule tooyour runbook**.</span></span>

![7단계][7]

### <a name="step-1"></a><span data-ttu-id="a33ce-158">1단계</span><span class="sxs-lookup"><span data-stu-id="a33ce-158">Step 1</span></span>

<span data-ttu-id="a33ce-159">Hello에 **일정** 블레이드에서 클릭 **새 일정을 만들려면**</span><span class="sxs-lookup"><span data-stu-id="a33ce-159">On hello **Schedule** blade, click **Create a new schedule**</span></span>

![8단계][8]

### <a name="step-2"></a><span data-ttu-id="a33ce-161">2단계</span><span class="sxs-lookup"><span data-stu-id="a33ce-161">Step 2</span></span>

<span data-ttu-id="a33ce-162">Hello에 **새 일정** 블레이드 채우기 hello 일정 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="a33ce-162">On hello **New Schedule** blade fill out hello schedule information.</span></span> <span data-ttu-id="a33ce-163">설정할 수 있는 hello 값 hello 목록 뒤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a33ce-163">hello values that can be set are in hello following list:</span></span>

- <span data-ttu-id="a33ce-164">**이름** -hello hello 일정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a33ce-164">**Name** - hello friendly name of hello schedule.</span></span>
- <span data-ttu-id="a33ce-165">**설명** -hello 일정에 대 한 설명을 합니다.</span><span class="sxs-lookup"><span data-stu-id="a33ce-165">**Description** - A description of hello schedule.</span></span>
- <span data-ttu-id="a33ce-166">**시작** -이 값은 날짜, 시간 및 hello 시간 hello 일정 트리거를 구성 하는 표준 시간대의 조합입니다.</span><span class="sxs-lookup"><span data-stu-id="a33ce-166">**Starts** - This value is a combination of date, time, and time zone that make up hello time hello schedule triggers.</span></span>
- <span data-ttu-id="a33ce-167">**되풀이** -hello 일정 반복이이 값을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a33ce-167">**Recurrence** - This value determines hello schedules repetition.</span></span>  <span data-ttu-id="a33ce-168">유효한 값은 **한 번** 또는 **되풀이**입니다.</span><span class="sxs-lookup"><span data-stu-id="a33ce-168">Valid values are **Once** or **Recurring**.</span></span>
- <span data-ttu-id="a33ce-169">**되풀이 모든** -hello 시간, 일, 주 또는 월의 hello 일정 되풀이 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="a33ce-169">**Recur every** - hello recurrence interval of hello schedule in hours, days, weeks, or months.</span></span>
- <span data-ttu-id="a33ce-170">**만료 설정** -hello 값 hello 일정 또는 만료 되어야 하는 경우를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a33ce-170">**Set Expiration** - hello value determines if hello schedule should expire or not.</span></span> <span data-ttu-id="a33ce-171">너무 설정할 수 있습니다**예** 또는 **아니요**합니다.</span><span class="sxs-lookup"><span data-stu-id="a33ce-171">Can be set too**Yes** or **No**.</span></span> <span data-ttu-id="a33ce-172">유효한 날짜 및 시간 toobe 예 선택 하면 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a33ce-172">A valid date and time are toobe provided if yes is chosen.</span></span>

> [!NOTE]
> <span data-ttu-id="a33ce-173">다른 간격으로 (즉, 15, 30, hello 시간 후 45 분) 여러 일정을 만들어야 합니다 toohave 매시간 보다 더 자주 실행 하는 runbook, 필요한 경우</span><span class="sxs-lookup"><span data-stu-id="a33ce-173">If you need toohave a runbook run more often than every hour, multiple schedules must be created at different intervals (that is, 15, 30, 45 minutes after hello hour)</span></span>

![9단계][9]

### <a name="step-3"></a><span data-ttu-id="a33ce-175">3단계</span><span class="sxs-lookup"><span data-stu-id="a33ce-175">Step 3</span></span>

<span data-ttu-id="a33ce-176">Toosave hello 일정 toohello runbook 저장을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a33ce-176">Click Save toosave hello schedule toohello runbook.</span></span>

![10단계][10]

## <a name="next-steps"></a><span data-ttu-id="a33ce-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a33ce-178">Next steps</span></span>

<span data-ttu-id="a33ce-179">사용자가 이해 하는 방법에 했으므로 tootrigger 패킷 VM 경고에 방문 하 여 캡처 하는 방법을 알아보려면 Azure 자동화 된 toointegrate 네트워크 감시자 해결 [Azure 네트워크 감시자경고트리거된패킷캡처만들기](network-watcher-alert-triggered-packet-capture.md).</span><span class="sxs-lookup"><span data-stu-id="a33ce-179">Now that you have an understanding on how toointegrate Network Watcher troubleshooting with Azure Automation, learn how tootrigger packet captures on VM alerts by visiting [Create an alert triggered packet capture with Azure Network Watcher](network-watcher-alert-triggered-packet-capture.md).</span></span>

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
