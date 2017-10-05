---
title: " 자동화 Runbook으로 Azure VM 경고 수정 | Microsoft Docs"
description: "이 문서에서는 Azure 가상 컴퓨터 경고를 Azure 자동화 runbook과 통합하고 문제를 자동 수정하는 방법을 보여 줍니다."
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
ms.openlocfilehash: 738959b8e1ee5da989bb996d1ce8148cbf912781
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario---remediate-azure-vm-alerts"></a><span data-ttu-id="c7b36-103">Azure 자동화 솔루션 - Azure VM 경고 수정</span><span class="sxs-lookup"><span data-stu-id="c7b36-103">Azure Automation scenario - remediate Azure VM alerts</span></span>
<span data-ttu-id="c7b36-104">Azure 자동화 및 Azure 가상 컴퓨터에 자동화 runbook을 실행하도록 가상 컴퓨터(VM) 경고를 구성할 수 있는 새로운 기능이 릴리스되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-104">Azure Automation and Azure Virtual Machines have released a new feature allowing you to configure Virtual Machine (VM) alerts to run Automation runbooks.</span></span> <span data-ttu-id="c7b36-105">이 새로운 기능을 통해 VM 경고에 대응하여 VM 재시작 또는 중지와 같은 일반 수정 작업을 자동으로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-105">This new capability allows you to automatically perform standard remediation in response to VM alerts, like restarting or stopping the VM.</span></span>

<span data-ttu-id="c7b36-106">이전에는 경고가 트리거될 때마다 runbook을 실행하기 위해 VM 경고 규칙 생성 중에 [자동화 webhook을 runbook으로 지정](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) 할 수 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-106">Previously, during VM alert rule creation you were able to [specify an Automation webhook](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) to a runbook in order to run the runbook whenever the alert triggered.</span></span> <span data-ttu-id="c7b36-107">그러나 이렇게 하려면 runbook을 만들고 runbook에 대한 webhook을 만든 후 경고 규칙 생성 중에 webhook을 복사하여 붙여넣어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-107">However, this required you to do the work of creating the runbook, creating the webhook for the runbook, and then copying and pasting the webhook during alert rule creation.</span></span> <span data-ttu-id="c7b36-108">새로운 릴리스에서는 경고 규칙 생성 중에 목록에서 runbook을 직접 선택할 수 있으며 runbook을 실행할 자동화 계정을 선택하고 계정을 쉽게 만들 수 있으므로 이 프로세스가 훨씬 쉬어집니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-108">With this new release, the process is much easier because you can directly choose a runbook from a list during alert rule creation, and you can choose an Automation account which will run the runbook or easily create an account.</span></span>

<span data-ttu-id="c7b36-109">이 문서에서는 Azure VM 경고를 설정하고 경고가 트리거될 때마다 실행하도록 자동화 runbook을 구성하는 과정이 얼마나 쉬운지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-109">In this article, we will show you how easy it is to set up an Azure VM alert and configure an Automation runbook to run whenever the alert triggers.</span></span> <span data-ttu-id="c7b36-110">예제 시나리오에는 VM에 있는 응용 프로그램의 메모리 누수로 인해 메모리 사용량이 임계값을 초과하는 경우 VM을 다시 시작하거나 지난 시간 동안 CPU 사용자 시간이 1% 미만이고 사용 중이지 않으면 VM을 중지하는 것이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-110">Example scenarios include restarting a VM when the memory usage exceeds some threshold due to an application on the VM with a memory leak, or stopping a VM when the CPU user time has been below 1% for past hour and is not in use.</span></span> <span data-ttu-id="c7b36-111">또한 자동화 계정에서 서비스 주체의 자동화된 생성이 Azure 경고 수정에서 runbook의 사용을 어떻게 간소화하는지도 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-111">We’ll also explain how the automated creation of a service principal in your Automation account simplifies the use of runbooks in Azure alert remediation.</span></span>

## <a name="create-an-alert-on-a-vm"></a><span data-ttu-id="c7b36-112">VM에서 경고 만들기</span><span class="sxs-lookup"><span data-stu-id="c7b36-112">Create an alert on a VM</span></span>
<span data-ttu-id="c7b36-113">해당 임계값을 충족하는 경우 runbook을 시작하도록 경고를 구성하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-113">Perform the following steps to configure an alert to launch a runbook when its threshold has been met.</span></span>

> [!NOTE]
> <span data-ttu-id="c7b36-114">이 릴리스에서는 V2 가상 컴퓨터만 지원하며 클래식 VM에 대한 지원은 곧 추가될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-114">With this release, we only support V2 virtual machines and support for classic VMs will be added soon.</span></span>  
> 
> 

1. <span data-ttu-id="c7b36-115">Azure 포털에 로그인하고 **가상 컴퓨터**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-115">Log in to the Azure portal and click **Virtual Machines**.</span></span>  
2. <span data-ttu-id="c7b36-116">가상 컴퓨터 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-116">Select one of your virtual machines.</span></span>  <span data-ttu-id="c7b36-117">가상 컴퓨터 대시보드 블레이드가 나타나고 **설정** 블레이드는 오른쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-117">The virtual machine dashboard blade will appear and the **Settings** blade to its right.</span></span>  
3. <span data-ttu-id="c7b36-118">**설정** 블레이드의 모니터링 섹션 아래에서 **경고 규칙**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-118">From the **Settings** blade, under the Monitoring section select **Alert rules**.</span></span>
4. <span data-ttu-id="c7b36-119">**경고 규칙** 블레이드에서 **경고 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-119">On the **Alert rules** blade, click **Add alert**.</span></span>

<span data-ttu-id="c7b36-120">그러면 **경고 규칙 추가** 블레이드가 열리고 여기에서 경고에 대한 조건을 구성할 수 있으며 옵션(누군가에게 전자 메일 보내기, webhook을 사용하여 경고를 다른 시스템에 전달, 문제를 수정하기 위한 시도로 자동화 runbook 실행) 중 하나 또는 모두 중에서 선택합니다</span><span class="sxs-lookup"><span data-stu-id="c7b36-120">This opens up the **Add an alert rule** blade, where you can configure the conditions for the alert and choose among one or all of these options: send email to someone, use a webhook to forward the alert to another system, and/or run an Automation runbook in response attempt to remediate the issue.</span></span>

## <a name="configure-a-runbook"></a><span data-ttu-id="c7b36-121">Runbook 구성</span><span class="sxs-lookup"><span data-stu-id="c7b36-121">Configure a runbook</span></span>
<span data-ttu-id="c7b36-122">VM 경고 임계값에 도달할 때 runbook이 실행되도록 구성하려면 **자동화 Runbook**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-122">To configure a runbook to run when the VM alert threshold is met, select **Automation Runbook**.</span></span> <span data-ttu-id="c7b36-123">**runbook 구성** 블레이드에서 실행할 runbook과 runbook을 실행할 자동화 계정을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-123">In the **Configure runbook** blade, you can select the runbook to run and the Automation account to run the runbook in.</span></span>

![자동화 runbook 구성 및 새 자동화 계정 만들기](media/automation-azure-vm-alert-integration/ConfigureRunbookNewAccount.png)

> [!NOTE]
> <span data-ttu-id="c7b36-125">이 릴리스에서는 서비스에서 제공하는 세 가지 runbook 중에서 선택할 수 있습니다. VM 다시 시작, VM 중지 또는 VM 제거(삭제)입니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-125">For this release you can choose from three runbooks that the service provides – Restart VM, Stop VM, or Remove VM (delete it).</span></span>  <span data-ttu-id="c7b36-126">다른 runbook을 선택하거나 사용자 고유의 runbook 중 하나를 선택하는 기능은 향후 릴리스에서 제공될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-126">The ability to select other runbooks or one of your own runbooks will be available in a future release.</span></span>
> 
> 

![Runbook 선택](media/automation-azure-vm-alert-integration/RunbooksToChoose.png)

<span data-ttu-id="c7b36-128">세 가지 사용 가능한 runbook 중 하나를 선택한 후에는 **자동화 계정** 드롭다운 목록이 나타나고 runbook을 실행할 자동화 계정을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-128">After you select one of the three available runbooks, the **Automation account** drop-down list appears and you can select an automation account the runbook will run as.</span></span> <span data-ttu-id="c7b36-129">Runbook은 Azure 구독에 있는 [자동화 계정](automation-security-overview.md) 의 컨텍스트에서 실행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-129">Runbooks need to run in the context of an [Automation account](automation-security-overview.md) that is in your Azure subscription.</span></span> <span data-ttu-id="c7b36-130">사용자가 이미 만든 자동화 계정을 선택하거나 사용자용으로 만들어진 새 자동화 계정을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-130">You can select an Automation account that you already created, or you can have a new Automation account created for you.</span></span>

<span data-ttu-id="c7b36-131">제공된 runbook은 서비스 주체를 사용하여 Azure에 인증을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-131">The runbooks that are provided authenticate to Azure using a service principal.</span></span> <span data-ttu-id="c7b36-132">기존 자동화 계정 중 하나에서 runbook을 실행하도록 선택한 경우 서비스 주체가 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-132">If you choose to run the runbook in one of your existing Automation accounts, we will automatically create the service principal for you.</span></span> <span data-ttu-id="c7b36-133">새 자동화 계정을 만들도록 선택한 경우 계정 및 서비스 주체가 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-133">If you choose to create a new Automation account, then we will automatically create the account and the service principal.</span></span> <span data-ttu-id="c7b36-134">두 경우 모두 자동화 계정에 두 자산도 생성됩니다. **AzureRunAsCertificate**라는 인증서 자산과 **AzureRunAsConnection**이라는 연결 자산입니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-134">In both cases, two assets will also be created in the Automation account – a certificate asset named **AzureRunAsCertificate** and a connection asset named **AzureRunAsConnection**.</span></span> <span data-ttu-id="c7b36-135">runbook은 VM에 대한 관리 작업을 수행하기 위해 **AzureRunAsConnection**을 사용하여 Azure와 인증을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-135">The runbooks will use **AzureRunAsConnection** to authenticate with Azure in order to perform the management action against the VM.</span></span>

> [!NOTE]
> <span data-ttu-id="c7b36-136">서비스 주체는 구독 범위에 생성되고 참여자 역할에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-136">The service principal is created in the subscription scope and is assigned the Contributor role.</span></span> <span data-ttu-id="c7b36-137">계정에서 Azure VM을 관리하기 위해 자동화 runbook 실행 권한을 보유하려면 이 역할이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-137">This role is required in order for the account to have permission to run Automation runbooks to manage Azure VMs.</span></span>  <span data-ttu-id="c7b36-138">자동화 계정 생성 및/또는 서비스 주체는 일회성 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-138">The creation of an Automaton account and/or service principal is a one-time event.</span></span> <span data-ttu-id="c7b36-139">생성되었으면 다른 Azure VM 경고에 대해 runbook을 실행하는 데 해당 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-139">Once they are created, you can use that account to run runbooks for other Azure VM alerts.</span></span>
> 
> 

<span data-ttu-id="c7b36-140">**확인** 을 클릭하면 경고가 구성되고 새 자동화 계정을 만드는 옵션을 선택하면 서비스 주체와 함께 계정이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-140">When you click **OK** the alert is configured and if you selected the option to create a new Automation account, it is created along with the service principal.</span></span>  <span data-ttu-id="c7b36-141">완료하는 데 몇 초 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-141">This can take a few seconds to complete.</span></span>  

![Runbook 구성 중](media/automation-azure-vm-alert-integration/RunbookBeingConfigured.png)

<span data-ttu-id="c7b36-143">구성이 완료되면 runbook의 이름이 **경고 규칙 추가** 블레이드에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-143">After the configuration is completed you will see the name of the runbook appear in the **Add an alert rule** blade.</span></span>

![Runbook 구성됨](media/automation-azure-vm-alert-integration/RunbookConfigured.png)

<span data-ttu-id="c7b36-145">**확인** in the **경고 규칙 추가** 을 클릭하면 경고 규칙이 생성되고 가상 컴퓨터가 실행 중 상태이면 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-145">Click **OK** in the **Add an alert rule** blade and the alert rule will be created and activate if the virtual machine is in a running state.</span></span>

### <a name="enable-or-disable-a-runbook"></a><span data-ttu-id="c7b36-146">Runbook 사용 또는 사용하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="c7b36-146">Enable or disable a runbook</span></span>
<span data-ttu-id="c7b36-147">경고에 대해 runbook을 구성한 경우 runbook 구성을 제거하지 않고 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-147">If you have a runbook configured for an alert, you can disable it without removing the runbook configuration.</span></span> <span data-ttu-id="c7b36-148">이렇게 하면 경고를 실행 상태로 유지하고 일부 경고 규칙을 테스트한 후 나중에 runbook을 다시 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-148">This allows you to keep the alert running and perhaps test some of the alert rules and then later re-enable the runbook.</span></span>

## <a name="create-a-runbook-that-works-with-an-azure-alert"></a><span data-ttu-id="c7b36-149">Azure 경고를 사용하여 작동하는 Runbook 만들기</span><span class="sxs-lookup"><span data-stu-id="c7b36-149">Create a runbook that works with an Azure alert</span></span>
<span data-ttu-id="c7b36-150">Azure 경고 규칙의 일환으로 Runbook을 선택하면 Runbook은 여기에 전달되는 경고 데이터를 관리하는 논리를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-150">When you choose a runbook as part of an Azure alert rule, the runbook needs to have logic in it to manage the alert data that is passed to it.</span></span>  <span data-ttu-id="c7b36-151">Runbook이 경고 규칙에 구성된 경우 웹후크가 Runbook에 생성됩니다.해당 웹후크는 경고가 트리거될 때마다 Runbook을 시작하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-151">When a runbook is configured in an alert rule, a webhook is created for the runbook; that webhook is then used to start the runbook each time the alert triggers.</span></span>  <span data-ttu-id="c7b36-152">Runbook을 시작하는 실제 호출은 웹후크 URL에 대한 HTTP POST 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-152">The actual call to start the runbook is an HTTP POST request to the webhook URL.</span></span> <span data-ttu-id="c7b36-153">POST 요청의 본문에는 경고와 관련된 유용한 속성을 포함하는 JSON으로 포맷된 개체가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-153">The body of the POST request contains a JSON-formated object that contains useful properties related to the alert.</span></span>  <span data-ttu-id="c7b36-154">아래에서 볼 수 있는 것처럼 경고 데이터는 subscriptionID, resourceGroupName, resourceName, 및 resourceType와 같은 세부 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-154">As you can see below, the alert data contains details like subscriptionID, resourceGroupName, resourceName, and resourceType.</span></span>

### <a name="example-of-alert-data"></a><span data-ttu-id="c7b36-155">경고 데이터의 예</span><span class="sxs-lookup"><span data-stu-id="c7b36-155">Example of Alert data</span></span>
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

<span data-ttu-id="c7b36-156">자동화 웹후크 서비스가 HTTP POST를 수신한 경우 경고 데이터를 추출하고 WebhookData Runbook 입력 매개 변수에서 Runbook에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-156">When the Automation webhook service receives the HTTP POST it extracts the alert data and passes it to the runbook in the WebhookData runbook input parameter.</span></span>  <span data-ttu-id="c7b36-157">다음은 WebhookData 매개 변수를 사용하고 경고 데이터를 추출하고 사용하여 경고를 트리거하는 Azure 리소스를 관리하는 방법을 보여 주는 샘플 Runbook입니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-157">Below is a sample runbook that shows how to use the WebhookData parameter and extract the alert data and use it to manage the Azure resource that triggered the alert.</span></span>

### <a name="example-runbook"></a><span data-ttu-id="c7b36-158">예제 Runbook</span><span class="sxs-lookup"><span data-stu-id="c7b36-158">Example runbook</span></span>
```
#  This runbook will restart an ARM (V2) VM in response to an Azure VM alert.

[OutputType("PSAzureOperationResponse")]

param ( [object] $WebhookData )

if ($WebhookData)
{
    # Get the data object from WebhookData
    $WebhookBody = (ConvertFrom-Json -InputObject $WebhookData.RequestBody)

    # Assure that the alert status is 'Activated' (alert condition went from false to true)
    # and not 'Resolved' (alert condition went from true to false)
    if ($WebhookBody.status -eq "Activated")
    {
        # Get the info needed to identify the VM
        $AlertContext = [object] $WebhookBody.context
        $ResourceName = $AlertContext.resourceName
        $ResourceType = $AlertContext.resourceType
        $ResourceGroupName = $AlertContext.resourceGroupName
        $SubId = $AlertContext.subscriptionId

        # Assure that this is the expected resource type
        Write-Verbose "ResourceType: $ResourceType"
        if ($ResourceType -eq "microsoft.compute/virtualmachines")
        {
            # This is an ARM (V2) VM

            # Authenticate to Azure with service principal and certificate
            $ConnectionAssetName = "AzureRunAsConnection"
            $Conn = Get-AutomationConnection -Name $ConnectionAssetName
            if ($Conn -eq $null) {
                throw "Could not retrieve connection asset: $ConnectionAssetName. Check that this asset exists in the Automation account."
            }
            Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint | Write-Verbose
            Set-AzureRmContext -SubscriptionId $SubId -ErrorAction Stop | Write-Verbose

            # Restart the VM
            Restart-AzureRmVM -Name $ResourceName -ResourceGroupName $ResourceGroupName
        } else {
            Write-Error "$ResourceType is not a supported resource type for this runbook."
        }
    } else {
        # The alert status was not 'Activated' so no action taken
        Write-Verbose ("No action taken. Alert status: " + $WebhookBody.status)
    }
} else {
    Write-Error "This runbook is meant to be started from an Azure alert only."
}
```

## <a name="summary"></a><span data-ttu-id="c7b36-159">요약</span><span class="sxs-lookup"><span data-stu-id="c7b36-159">Summary</span></span>
<span data-ttu-id="c7b36-160">Azure VM에서 경고를 구성할 경우 경고가 트리거될 때 수정 작업을 자동으로 수행하도록 이제 자동화 runbook을 쉽게 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-160">When you configure an alert on an Azure VM, you now have the ability to easily configure an Automation runbook to automatically perform remediation action when the alert triggers.</span></span> <span data-ttu-id="c7b36-161">이 릴리스에서는 경고 시나리오에 따라 runbook에서 VM을 다시 시작, 중지 또는 삭제하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-161">For this release, you can choose from runbooks to restart, stop, or delete a VM depending on your alert scenario.</span></span> <span data-ttu-id="c7b36-162">이 릴리스는 경고가 트리거될 때 자동으로 수행하는 동작(알림, 문제 해결, 수정)을 제어하는 시나리오를 실현하는 시작일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="c7b36-162">This is just the beginning of enabling scenarios where you control the actions (notification, troubleshooting, remediation) that will be taken automatically when an alert triggers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7b36-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c7b36-163">Next Steps</span></span>
* <span data-ttu-id="c7b36-164">그래픽 Runbook을 시작하려면 [내 첫 번째 그래픽 Runbook](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="c7b36-164">To get started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span>
* <span data-ttu-id="c7b36-165">PowerShell 워크플로 Runbook을 시작하려면 [내 첫 번째 PowerShell 워크플로 Runbook](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="c7b36-165">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="c7b36-166">Runbook 형식, 해당 장점 및 제한 사항에 대해 자세히 알아보려면 [Azure 자동화 Runbook 형식](automation-runbook-types.md)</span><span class="sxs-lookup"><span data-stu-id="c7b36-166">To learn more about runbook types, their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md)</span></span>

