---
title: "자동화 Runbook 된 Azure VM의 경고를 수정 하는 aaa\"| \"Microsoft Docs"
description: "이 문서는 Azure 자동화 runbook와 Azure 가상 컴퓨터 toointegrate 경고 하는 방법을 보여 줍니다. 하 고 문제를 자동 해결"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 1f7baa7f-7283-4a4f-9385-3f5cd1062c7f
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/14/2016
ms.author: csand;magoedte
ms.openlocfilehash: c226368a5c4c51fbfb331f4b97f7f2f239e701c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---remediate-azure-vm-alerts"></a><span data-ttu-id="64b6a-103">Azure 자동화 솔루션 - Azure VM 경고 수정</span><span class="sxs-lookup"><span data-stu-id="64b6a-103">Azure Automation scenario - remediate Azure VM alerts</span></span>
<span data-ttu-id="64b6a-104">Azure 자동화와 Azure 가상 컴퓨터 tooconfigure 가상 컴퓨터 (VM) 경고 toorun 자동화 runbook을 허용 하는 새로운 기능을 해제 했습니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-104">Azure Automation and Azure Virtual Machines have released a new feature allowing you tooconfigure Virtual Machine (VM) alerts toorun Automation runbooks.</span></span> <span data-ttu-id="64b6a-105">이 새 기능을 사용 하면 tooautomatically 응답 tooVM 경고를 다시 시작 또는 중지 hello VM과 같은 표준 관리를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-105">This new capability allows you tooautomatically perform standard remediation in response tooVM alerts, like restarting or stopping hello VM.</span></span>

<span data-ttu-id="64b6a-106">이전에 VM 경고 규칙을 만드는 동안 있었습니다 너무[자동화 webhook 지정](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) hello 경고가 트리거 되었을 때마다 순서 toorun hello runbook에서 runbook tooa 합니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-106">Previously, during VM alert rule creation you were able too[specify an Automation webhook](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) tooa runbook in order toorun hello runbook whenever hello alert triggered.</span></span> <span data-ttu-id="64b6a-107">그러나이 필요 하면 hello runbook 만들기, hello runbook에 대 한 hello webhook 만들기, 복사 하 여 경고 규칙을 만드는 동안 hello webhook을 붙여 및 toodo hello 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-107">However, this required you toodo hello work of creating hello runbook, creating hello webhook for hello runbook, and then copying and pasting hello webhook during alert rule creation.</span></span> <span data-ttu-id="64b6a-108">이 새 릴리스를 경고 규칙을 만드는 동안 목록에서 runbook을 직접 선택할 수 있으며 hello runbook을 실행 하거나 쉽게 계정 만들기를 자동화 계정을 선택할 수 있으므로 hello 프로세스는 훨씬 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-108">With this new release, hello process is much easier because you can directly choose a runbook from a list during alert rule creation, and you can choose an Automation account which will run hello runbook or easily create an account.</span></span>

<span data-ttu-id="64b6a-109">이 문서에서는 얼마나 쉬운지 tooset Azure VM 경고를 표시 하 고 hello 경고를 트리거하는 자동화 runbook toorun 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-109">In this article, we will show you how easy it is tooset up an Azure VM alert and configure an Automation runbook toorun whenever hello alert triggers.</span></span> <span data-ttu-id="64b6a-110">예제 시나리오는 hello 메모리 사용량 tooan 응용 프로그램에서 메모리 누수와 VM hello 인해 일부 임계값을 초과할 경우 VM을 다시 시작 하거나 CPU hello 사용자 시간이 지난 시간 동안 %1 하 고 사용 하지 않는 VM 중지 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-110">Example scenarios include restarting a VM when hello memory usage exceeds some threshold due tooan application on hello VM with a memory leak, or stopping a VM when hello CPU user time has been below 1% for past hour and is not in use.</span></span> <span data-ttu-id="64b6a-111">Hello 만들기를 자동화 하는 방법을 설명도 계정 자동화에서 서비스 사용자의 Azure 경고 재구성에서 하는 runbook의 hello 사용을 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-111">We’ll also explain how hello automated creation of a service principal in your Automation account simplifies hello use of runbooks in Azure alert remediation.</span></span>

## <a name="create-an-alert-on-a-vm"></a><span data-ttu-id="64b6a-112">VM에서 경고 만들기</span><span class="sxs-lookup"><span data-stu-id="64b6a-112">Create an alert on a VM</span></span>
<span data-ttu-id="64b6a-113">Hello 단계 tooconfigure 경고 toolaunch runbook는 해당 임계값을 충족 하는 경우 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-113">Perform hello following steps tooconfigure an alert toolaunch a runbook when its threshold has been met.</span></span>

> [!NOTE]
> <span data-ttu-id="64b6a-114">이 릴리스에서는 V2 가상 컴퓨터만 지원하며 클래식 VM에 대한 지원은 곧 추가될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-114">With this release, we only support V2 virtual machines and support for classic VMs will be added soon.</span></span>  
> 
> 

1. <span data-ttu-id="64b6a-115">클릭 하 고 toohello Azure 포털에 로그인 **가상 컴퓨터**합니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-115">Log in toohello Azure portal and click **Virtual Machines**.</span></span>  
2. <span data-ttu-id="64b6a-116">가상 컴퓨터 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-116">Select one of your virtual machines.</span></span>  <span data-ttu-id="64b6a-117">hello 가상 컴퓨터 대시보드 블레이드 표시 되 고 hello **설정을** 블레이드 tooits 오른쪽입니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-117">hello virtual machine dashboard blade will appear and hello **Settings** blade tooits right.</span></span>  
3. <span data-ttu-id="64b6a-118">Hello에서 **설정** 블레이드 hello 모니터링 섹션 선택에서 **규칙 경고**합니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-118">From hello **Settings** blade, under hello Monitoring section select **Alert rules**.</span></span>
4. <span data-ttu-id="64b6a-119">Hello에 **규칙 경고** 블레이드에서 클릭 **추가 경고**합니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-119">On hello **Alert rules** blade, click **Add alert**.</span></span>

<span data-ttu-id="64b6a-120">Hello를 열어서이 **경고 규칙 추가** hello 경고에 대 한 hello 조건을 구성 하 고 이러한 옵션 중 하나 또는 모두 중에서 선택할 수 있습니다: toosomeone 전자 메일 보내기, webhook tooforward hello tooanother 경고 시스템을 사용 및/또는 응답 시도 tooremediate hello 문제에서 자동화 runbook을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-120">This opens up hello **Add an alert rule** blade, where you can configure hello conditions for hello alert and choose among one or all of these options: send email toosomeone, use a webhook tooforward hello alert tooanother system, and/or run an Automation runbook in response attempt tooremediate hello issue.</span></span>

## <a name="configure-a-runbook"></a><span data-ttu-id="64b6a-121">Runbook 구성</span><span class="sxs-lookup"><span data-stu-id="64b6a-121">Configure a runbook</span></span>
<span data-ttu-id="64b6a-122">tooconfigure hello VM에 대 한 경고 임계값이 충족 되 면 runbook toorun 선택 **자동화 Runbook**합니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-122">tooconfigure a runbook toorun when hello VM alert threshold is met, select **Automation Runbook**.</span></span> <span data-ttu-id="64b6a-123">Hello에 **runbook 구성** 블레이드에서 hello runbook toorun 및 hello 자동화 계정 toorun hello runbook에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-123">In hello **Configure runbook** blade, you can select hello runbook toorun and hello Automation account toorun hello runbook in.</span></span>

![자동화 runbook 구성 및 새 자동화 계정 만들기](media/automation-azure-vm-alert-integration/ConfigureRunbookNewAccount.png)

> [!NOTE]
> <span data-ttu-id="64b6a-125">이 릴리스에 대 한 세 가지 runbook – hello 서비스에서 제공 하는 VM을 다시 시작, 중지 VM 또는 VM 제거에서 선택할 수 있습니다 (삭제) 합니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-125">For this release you can choose from three runbooks that hello service provides – Restart VM, Stop VM, or Remove VM (delete it).</span></span>  <span data-ttu-id="64b6a-126">다른 runbook 기능 tooselect hello 또는 위한 고유한 runbook 중 하나는 이후 버전에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-126">hello ability tooselect other runbooks or one of your own runbooks will be available in a future release.</span></span>
> 
> 

![Runbook toochoose](media/automation-azure-vm-alert-integration/RunbooksToChoose.png)

<span data-ttu-id="64b6a-128">Hello 3 사용 가능한 runbook 중 하나를 선택한 후 hello **자동화 계정** 드롭 다운 목록에 표시 되 고 자동화를 선택할 수 있습니다 계정 hello runbook으로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-128">After you select one of hello three available runbooks, hello **Automation account** drop-down list appears and you can select an automation account hello runbook will run as.</span></span> <span data-ttu-id="64b6a-129">Runbook의 hello 컨텍스트에서 toorun 필요는 [자동화 계정](automation-security-overview.md) Azure 구독에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-129">Runbooks need toorun in hello context of an [Automation account](automation-security-overview.md) that is in your Azure subscription.</span></span> <span data-ttu-id="64b6a-130">사용자가 이미 만든 자동화 계정을 선택하거나 사용자용으로 만들어진 새 자동화 계정을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-130">You can select an Automation account that you already created, or you can have a new Automation account created for you.</span></span>

<span data-ttu-id="64b6a-131">제공 되는 hello runbook tooAzure 서비스 사용자를 사용 하 여 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-131">hello runbooks that are provided authenticate tooAzure using a service principal.</span></span> <span data-ttu-id="64b6a-132">기존 자동화 계정 중 하나에 toorun hello runbook을 선택 하면에서는 자동으로 작성 됩니다 hello 서비스 보안 주체 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-132">If you choose toorun hello runbook in one of your existing Automation accounts, we will automatically create hello service principal for you.</span></span> <span data-ttu-id="64b6a-133">새 자동화 계정 toocreate를 선택 하면 다음를 자동으로 만듭니다 hello 계정과 hello 서비스 사용자.</span><span class="sxs-lookup"><span data-stu-id="64b6a-133">If you choose toocreate a new Automation account, then we will automatically create hello account and hello service principal.</span></span> <span data-ttu-id="64b6a-134">두 경우 모두 두 개의 자산을 만들게 됩니다 hello 라는 인증서 자산 자동화 계정에서에서 **AzureRunAsCertificate** 및 명명 된 연결 자산 **AzureRunAsConnection**합니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-134">In both cases, two assets will also be created in hello Automation account – a certificate asset named **AzureRunAsCertificate** and a connection asset named **AzureRunAsConnection**.</span></span> <span data-ttu-id="64b6a-135">hello runbook ´ ֲ **AzureRunAsConnection** hello VM에 대해 순서 tooperform hello 관리 동작에 azure tooauthenticate 합니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-135">hello runbooks will use **AzureRunAsConnection** tooauthenticate with Azure in order tooperform hello management action against hello VM.</span></span>

> [!NOTE]
> <span data-ttu-id="64b6a-136">hello 서비스 사용자 hello 구독 범위에서 만들어지고 hello 참가자 역할이 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-136">hello service principal is created in hello subscription scope and is assigned hello Contributor role.</span></span> <span data-ttu-id="64b6a-137">이 역할은 hello 계정 toohave 권한 toorun 자동화 runbook toomanage Azure Vm에 대 한 순서에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-137">This role is required in order for hello account toohave permission toorun Automation runbooks toomanage Azure VMs.</span></span>  <span data-ttu-id="64b6a-138">hello 생성 된 자동화 계정 및/또는 서비스 사용자의 일회성 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-138">hello creation of an Automaton account and/or service principal is a one-time event.</span></span> <span data-ttu-id="64b6a-139">를 만든 후에 다른 Azure VM 경고에 대 한 해당 계정 toorun runbook을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-139">Once they are created, you can use that account toorun runbooks for other Azure VM alerts.</span></span>
> 
> 

<span data-ttu-id="64b6a-140">클릭할 때 **확인** hello 경고 구성 되 고 hello 옵션 toocreate 새 자동화 계정에 선택한 경우 여 hello 서비스 사용자와 함께 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-140">When you click **OK** hello alert is configured and if you selected hello option toocreate a new Automation account, it is created along with hello service principal.</span></span>  <span data-ttu-id="64b6a-141">몇 초 정도 걸릴 수 있습니다이 toocomplete 합니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-141">This can take a few seconds toocomplete.</span></span>  

![Runbook 구성 중](media/automation-azure-vm-alert-integration/RunbookBeingConfigured.png)

<span data-ttu-id="64b6a-143">Hello에 표시 hello runbook의 hello 이름이 표시는 hello 구성이 완료 되 면 **경고 규칙 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-143">After hello configuration is completed you will see hello name of hello runbook appear in hello **Add an alert rule** blade.</span></span>

![Runbook 구성됨](media/automation-azure-vm-alert-integration/RunbookConfigured.png)

<span data-ttu-id="64b6a-145">클릭 **확인** hello에 **경고 규칙 추가** 블레이드에 대 한 hello 경고 규칙 생성 되 고 hello 가상 컴퓨터가 실행 중 상태인 경우 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-145">Click **OK** in hello **Add an alert rule** blade and hello alert rule will be created and activate if hello virtual machine is in a running state.</span></span>

### <a name="enable-or-disable-a-runbook"></a><span data-ttu-id="64b6a-146">Runbook 사용 또는 사용하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="64b6a-146">Enable or disable a runbook</span></span>
<span data-ttu-id="64b6a-147">경고에 대해 구성 된 runbook를 설정한 경우에 hello runbook 구성 제거 하지 않고 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-147">If you have a runbook configured for an alert, you can disable it without removing hello runbook configuration.</span></span> <span data-ttu-id="64b6a-148">이 tookeep hello 경고를 실행 하면 및 아마도 hello 경고 규칙의 일부를 테스트 한 후 나중에 다시 활성화 hello runbook입니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-148">This allows you tookeep hello alert running and perhaps test some of hello alert rules and then later re-enable hello runbook.</span></span>

## <a name="create-a-runbook-that-works-with-an-azure-alert"></a><span data-ttu-id="64b6a-149">Azure 경고를 사용하여 작동하는 Runbook 만들기</span><span class="sxs-lookup"><span data-stu-id="64b6a-149">Create a runbook that works with an Azure alert</span></span>
<span data-ttu-id="64b6a-150">Azure 경고 규칙의 일환으로 runbook을 선택 하면 hello runbook toohave 논리 toomanage hello 경고 하는 데이터가 필요 tooit 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-150">When you choose a runbook as part of an Azure alert rule, hello runbook needs toohave logic in it toomanage hello alert data that is passed tooit.</span></span>  <span data-ttu-id="64b6a-151">Runbook은 경고 규칙에서 구성 되 면 여 webhook을 사용할지 hello runbook;에 대해 생성 됩니다. 해당 webhook으로 사용 되는 toostart hello runbook 각 시간 hello 경고 트리거는입니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-151">When a runbook is configured in an alert rule, a webhook is created for hello runbook; that webhook is then used toostart hello runbook each time hello alert triggers.</span></span>  <span data-ttu-id="64b6a-152">hello 실제 호출 toostart hello runbook은 HTTP POST 요청 toohello webhook URL입니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-152">hello actual call toostart hello runbook is an HTTP POST request toohello webhook URL.</span></span> <span data-ttu-id="64b6a-153">hello POST 요청의 본문 hello 유용한 속성 관련된 toohello 경고를 포함 하는 형식이 JSON 개체를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-153">hello body of hello POST request contains a JSON-formated object that contains useful properties related toohello alert.</span></span>  <span data-ttu-id="64b6a-154">아래 보시 hello 경고 데이터는 구독 Id, 리소스 그룹 이름, resourceName, 및 resourceType와 같은 세부 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-154">As you can see below, hello alert data contains details like subscriptionID, resourceGroupName, resourceName, and resourceType.</span></span>

### <a name="example-of-alert-data"></a><span data-ttu-id="64b6a-155">경고 데이터의 예</span><span class="sxs-lookup"><span data-stu-id="64b6a-155">Example of Alert data</span></span>
```
{
    "WebhookName": "AzureAlertTest",
    "RequestBody": "{
    \"status\":\"Activated\",
    \"context\": {
        \"id\":\"/subscriptions/<subscriptionId>/resourceGroups/MyResourceGroup/providers/microsoft.insights/alertrules/AlertTest\",
        \"name\":\"AlertTest\",
        \"description\":\"\",
        \"condition\": {
            \"metricName\":\"CPU percentage guest OS\",
            \"metricUnit\":\"Percent\",
            \"metricValue\":\"4.26337916666667\",
            \"threshold\":\"1\",
            \"windowSize\":\"60\",
            \"timeAggregation\":\"Average\",
            \"operator\":\"GreaterThan\"},
        \"subscriptionId\":\<subscriptionID> \",
        \"resourceGroupName\":\"TestResourceGroup\",
        \"timestamp\":\"2016-04-24T23:19:50.1440170Z\",
        \"resourceName\":\"TestVM\",
        \"resourceType\":\"microsoft.compute/virtualmachines\",
        \"resourceRegion\":\"westus\",
        \"resourceId\":\"/subscriptions/<subscriptionId>/resourceGroups/TestResourceGroup/providers/Microsoft.Compute/virtualMachines/TestVM\",
        \"portalLink\":\"https://portal.azure.com/#resource/subscriptions/<subscriptionId>/resourceGroups/TestResourceGroup/providers/Microsoft.Compute/virtualMachines/TestVM\"
        },
    \"properties\":{}
    }",
    "RequestHeader": {
        "Connection": "Keep-Alive",
        "Host": "<webhookURL>"
    }
}
```

<span data-ttu-id="64b6a-156">Hello 자동화 webhook 서비스 hello HTTP POST를 받으면 hello 경고 데이터를 추출 하 고 hello WebhookData runbook 입력 매개 변수로 toohello runbook을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-156">When hello Automation webhook service receives hello HTTP POST it extracts hello alert data and passes it toohello runbook in hello WebhookData runbook input parameter.</span></span>  <span data-ttu-id="64b6a-157">다음은 toouse를 hello WebhookData 매개 변수 및 hello 경고 데이터를 추출 고 toomanage hello hello 경고를 트리거한 Azure 리소스 사용 방법을 보여 주는 샘플 runbook입니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-157">Below is a sample runbook that shows how toouse hello WebhookData parameter and extract hello alert data and use it toomanage hello Azure resource that triggered hello alert.</span></span>

### <a name="example-runbook"></a><span data-ttu-id="64b6a-158">예제 Runbook</span><span class="sxs-lookup"><span data-stu-id="64b6a-158">Example runbook</span></span>
```
#  This runbook will restart an ARM (V2) VM in response tooan Azure VM alert.

[OutputType("PSAzureOperationResponse")]

param ( [object] $WebhookData )

if ($WebhookData)
{
    # Get hello data object from WebhookData
    $WebhookBody = (ConvertFrom-Json -InputObject $WebhookData.RequestBody)

    # Assure that hello alert status is 'Activated' (alert condition went from false tootrue)
    # and not 'Resolved' (alert condition went from true toofalse)
    if ($WebhookBody.status -eq "Activated")
    {
        # Get hello info needed tooidentify hello VM
        $AlertContext = [object] $WebhookBody.context
        $ResourceName = $AlertContext.resourceName
        $ResourceType = $AlertContext.resourceType
        $ResourceGroupName = $AlertContext.resourceGroupName
        $SubId = $AlertContext.subscriptionId

        # Assure that this is hello expected resource type
        Write-Verbose "ResourceType: $ResourceType"
        if ($ResourceType -eq "microsoft.compute/virtualmachines")
        {
            # This is an ARM (V2) VM

            # Authenticate tooAzure with service principal and certificate
            $ConnectionAssetName = "AzureRunAsConnection"
            $Conn = Get-AutomationConnection -Name $ConnectionAssetName
            if ($Conn -eq $null) {
                throw "Could not retrieve connection asset: $ConnectionAssetName. Check that this asset exists in hello Automation account."
            }
            Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint | Write-Verbose
            Set-AzureRmContext -SubscriptionId $SubId -ErrorAction Stop | Write-Verbose

            # Restart hello VM
            Restart-AzureRmVM -Name $ResourceName -ResourceGroupName $ResourceGroupName
        } else {
            Write-Error "$ResourceType is not a supported resource type for this runbook."
        }
    } else {
        # hello alert status was not 'Activated' so no action taken
        Write-Verbose ("No action taken. Alert status: " + $WebhookBody.status)
    }
} else {
    Write-Error "This runbook is meant toobe started from an Azure alert only."
}
```

## <a name="summary"></a><span data-ttu-id="64b6a-159">요약</span><span class="sxs-lookup"><span data-stu-id="64b6a-159">Summary</span></span>
<span data-ttu-id="64b6a-160">Azure VM에 대 한 경고를 구성 하는 경우 해야 자동화를 구성 하는 hello 기능 tooeasily hello 경고를 트리거할 때 runbook tooautomatically 업데이트 관리 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-160">When you configure an alert on an Azure VM, you now have hello ability tooeasily configure an Automation runbook tooautomatically perform remediation action when hello alert triggers.</span></span> <span data-ttu-id="64b6a-161">이 릴리스에 대 한 runbook toorestart에서 선택할 수 있습니다 하 고 중지 또는 경고 시나리오에 따라 VM을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-161">For this release, you can choose from runbooks toorestart, stop, or delete a VM depending on your alert scenario.</span></span> <span data-ttu-id="64b6a-162">이 경고를 트리거할 때 자동으로 수행 될 hello 작업 (알림, 문제 해결, 업데이트 관리)를 제어 하는 경우 시나리오를 지원할 뿐 hello 시작입니다.</span><span class="sxs-lookup"><span data-stu-id="64b6a-162">This is just hello beginning of enabling scenarios where you control hello actions (notification, troubleshooting, remediation) that will be taken automatically when an alert triggers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64b6a-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="64b6a-163">Next Steps</span></span>
* <span data-ttu-id="64b6a-164">그래픽 runbook 시작 tooget 참조 [내 첫 번째 그래픽 runbook](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="64b6a-164">tooget started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span>
* <span data-ttu-id="64b6a-165">PowerShell 워크플로 runbook 시작 tooget 참조 [내 첫 번째 PowerShell 워크플로 runbook](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="64b6a-165">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="64b6a-166">runbook 형식이, 장점 및 제한 사항에 대해 자세히 toolearn 참조 [Azure 자동화 runbook 형식](automation-runbook-types.md)</span><span class="sxs-lookup"><span data-stu-id="64b6a-166">toolearn more about runbook types, their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md)</span></span>

