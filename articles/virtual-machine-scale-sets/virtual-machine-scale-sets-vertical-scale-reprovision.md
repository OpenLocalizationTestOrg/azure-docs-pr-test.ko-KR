---
title: "Azure 가상 컴퓨터 확장 집합을 수직으로 규모 조정 | Microsoft Docs"
description: "Azure 자동화를 사용하여 모니터링 경고에 대한 응답으로 가상 컴퓨터를 수직으로 확장하는 방법"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: madhana
editor: 
tags: azure-resource-manager
ms.assetid: 16b17421-6b8f-483e-8a84-26327c44e9d3
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 08/03/2016
ms.author: guybo
ms.openlocfilehash: 9159a5a9041864fe06785829121233379c46bb03
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="vertical-autoscale-with-virtual-machine-scale-sets"></a><span data-ttu-id="2dc6d-103">가상 컴퓨터 규모 집합을 사용하여 수직 자동 규모 조정</span><span class="sxs-lookup"><span data-stu-id="2dc6d-103">Vertical autoscale with Virtual Machine Scale sets</span></span>
<span data-ttu-id="2dc6d-104">이 문서에서는 다시 프로비저닝을 사용하거나 사용하지 않고 Azure [가상 컴퓨터 규모 집합](https://azure.microsoft.com/services/virtual-machine-scale-sets/) 을 수직으로 확장하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2dc6d-104">This article describes how to vertically scale Azure [Virtual Machine Scale Sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/) with or without reprovisioning.</span></span> <span data-ttu-id="2dc6d-105">규모 집합에 있지 않은 VM의 수직 규모 조정에 대해서는 [Azure 자동화를 사용하여 Azure 가상 컴퓨터를 수직으로 확장](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2dc6d-105">For vertical scaling of VMs which are not in scale sets, refer to [Vertically scale Azure virtual machine with Azure Automation](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="2dc6d-106">일명 *강화* 및 *규모 축소*라고도 하는 수직 규모 조정이란 워크로드에 따라 가상 컴퓨터(VM) 규모를 늘리거나 줄이는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="2dc6d-106">Vertical scaling, also known as *scale up* and *scale down*, means increasing or decreasing virtual machine (VM) sizes in response to a workload.</span></span> <span data-ttu-id="2dc6d-107">이 작업을 가상 컴퓨터 수가 워크로드에 따라 변경되는 일명 *규모 확장* 및 *규모 감축*이라고도 하는 [수평 규모 조정](virtual-machine-scale-sets-autoscale-overview.md)과 비교해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="2dc6d-107">Compare this with [horizontal scaling](virtual-machine-scale-sets-autoscale-overview.md), also referred to as *scale out* and *scale in*, where the number of VMs is altered depending on the workload.</span></span>

<span data-ttu-id="2dc6d-108">다시 프로비저닝이란 기존 VM을 제거하고 새 VM으로 바꾸는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="2dc6d-108">Reprovisioning means removing an existing VM and replacing it with a new one.</span></span> <span data-ttu-id="2dc6d-109">VM 규모 집합에서 VM의 규모를 늘리거나 줄이는 경우 기존 VM을 규모 변경하고 데이터를 보존하기를 원하는 경우도 있고 새 규모의 새 VM을 배포해야 하는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dc6d-109">When you increase or decrease the size of VMs in a VM Scale Set, in some cases you want to resize existing VMs and retain your data, while in other cases you need to deploy new VMs of the new size.</span></span> <span data-ttu-id="2dc6d-110">이 문서에서는 두 경우를 모두 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2dc6d-110">This document covers both cases.</span></span>

<span data-ttu-id="2dc6d-111">수직 규모 조정이 유용할 수 있는 경우:</span><span class="sxs-lookup"><span data-stu-id="2dc6d-111">Vertical scaling can be useful when:</span></span>

* <span data-ttu-id="2dc6d-112">가상 컴퓨터에 만들어진 서비스는 잘 이용되지 않습니다(예를 들어 주말).</span><span class="sxs-lookup"><span data-stu-id="2dc6d-112">A service built on virtual machines is under-utilized (for example at weekends).</span></span> <span data-ttu-id="2dc6d-113">VM 규모를 줄이면 월간 비용을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dc6d-113">Reducing the VM size can reduce monthly costs.</span></span>
* <span data-ttu-id="2dc6d-114">VM 규모를 늘리면 추가 VM을 만들지 않고 더 큰 수요를 충족할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dc6d-114">Increasing VM size to cope with larger demand without creating additional VMs.</span></span>

<span data-ttu-id="2dc6d-115">VM 규모 집합에서 메트릭 기반 경고를 바탕으로 수직 규모 조정을 트리거하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dc6d-115">You can set up vertical scaling to be triggered based on metric based alerts from your VM Scale Set.</span></span> <span data-ttu-id="2dc6d-116">경고가 활성화될 때 규모를 확장하거나 축소할 수 있는 Runbook을 트리거하는 Webhook가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="2dc6d-116">When the alert is activated it fires a webhook that triggers a runbook which can scale your scale set up or down.</span></span> <span data-ttu-id="2dc6d-117">수직 규모 조정을 다음과 같은 단계에 따라 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dc6d-117">Vertical scaling can be configured by following these steps:</span></span>

1. <span data-ttu-id="2dc6d-118">실행 기능을 사용하여 Azure 자동화 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2dc6d-118">Create an Azure Automation account with run-as capability.</span></span>
2. <span data-ttu-id="2dc6d-119">VM 규모 집합용 Azure 자동화 수직 규모 조정 Runbook을 구독으로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2dc6d-119">Import Azure Automation Vertical Scale runbooks for VM Scale Sets into your subscription.</span></span>
3. <span data-ttu-id="2dc6d-120">Webhook을 Runbook에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2dc6d-120">Add a webhook to your runbook.</span></span>
4. <span data-ttu-id="2dc6d-121">Webhook 알림을 사용하여 VM 규모 집합에 경고를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2dc6d-121">Add an alert to your VM Scale Set using a webhook notification.</span></span>

> [!NOTE]
> <span data-ttu-id="2dc6d-122">수직 자동 규모 조정은 특정 범위의 VM 규모 이내에서만 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dc6d-122">Vertical autoscaling can only take place within certain ranges of VM sizes.</span></span> <span data-ttu-id="2dc6d-123">서로 크기를 조정하도록 결정하기 전에 각 크기의 사양을 비교합니다(값이 큰 경우에도 VM 크기가 더 크지 않을 수 있음).</span><span class="sxs-lookup"><span data-stu-id="2dc6d-123">Compare the specifications of each size before deciding to scale from one to another (higher number does not always indicate bigger VM size).</span></span> <span data-ttu-id="2dc6d-124">다음 규모 쌍 범위로 규모 조정하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dc6d-124">You can choose to scale between the following pairs of sizes:</span></span>
> 
> | <span data-ttu-id="2dc6d-125">VM 크기 조정 쌍</span><span class="sxs-lookup"><span data-stu-id="2dc6d-125">VM sizes scaling pair</span></span> |  |
> | --- | --- |
> | <span data-ttu-id="2dc6d-126">Standard_A0</span><span class="sxs-lookup"><span data-stu-id="2dc6d-126">Standard_A0</span></span> |<span data-ttu-id="2dc6d-127">Standard_A11</span><span class="sxs-lookup"><span data-stu-id="2dc6d-127">Standard_A11</span></span> |
> | <span data-ttu-id="2dc6d-128">Standard_D1</span><span class="sxs-lookup"><span data-stu-id="2dc6d-128">Standard_D1</span></span> |<span data-ttu-id="2dc6d-129">Standard_D14</span><span class="sxs-lookup"><span data-stu-id="2dc6d-129">Standard_D14</span></span> |
> | <span data-ttu-id="2dc6d-130">Standard_DS1</span><span class="sxs-lookup"><span data-stu-id="2dc6d-130">Standard_DS1</span></span> |<span data-ttu-id="2dc6d-131">Standard_DS14</span><span class="sxs-lookup"><span data-stu-id="2dc6d-131">Standard_DS14</span></span> |
> | <span data-ttu-id="2dc6d-132">Standard_D1v2</span><span class="sxs-lookup"><span data-stu-id="2dc6d-132">Standard_D1v2</span></span> |<span data-ttu-id="2dc6d-133">Standard_D15v2</span><span class="sxs-lookup"><span data-stu-id="2dc6d-133">Standard_D15v2</span></span> |
> | <span data-ttu-id="2dc6d-134">Standard_G1</span><span class="sxs-lookup"><span data-stu-id="2dc6d-134">Standard_G1</span></span> |<span data-ttu-id="2dc6d-135">Standard_G5</span><span class="sxs-lookup"><span data-stu-id="2dc6d-135">Standard_G5</span></span> |
> | <span data-ttu-id="2dc6d-136">Standard_GS1</span><span class="sxs-lookup"><span data-stu-id="2dc6d-136">Standard_GS1</span></span> |<span data-ttu-id="2dc6d-137">Standard_GS5</span><span class="sxs-lookup"><span data-stu-id="2dc6d-137">Standard_GS5</span></span> |
> 
> 

## <a name="create-an-azure-automation-account-with-run-as-capability"></a><span data-ttu-id="2dc6d-138">실행 기능을 사용하여 Azure 자동화 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="2dc6d-138">Create an Azure Automation Account with run-as capability</span></span>
<span data-ttu-id="2dc6d-139">가장 먼저 해야 할 일은 VM 규모 집합 인스턴스의 규모를 조정하는 데 사용하는 Runbook을 호스트할 Azure 자동화 계정을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2dc6d-139">The first thing you need to do is create an Azure Automation account that will host the runbooks used to scale the VM Scale Set instances.</span></span> <span data-ttu-id="2dc6d-140">최근 [Azure 자동화](https://azure.microsoft.com/services/automation/) 에서는 사용자 대신 Runbook을 자동으로 매우 쉽게 실행하기 위한 서비스 주체를 설정하는 "실행 계정" 기능을 도입했습니다.</span><span class="sxs-lookup"><span data-stu-id="2dc6d-140">Recently [Azure Automation](https://azure.microsoft.com/services/automation/) introduced the "Run As account" feature which makes setting up the Service Principal for automatically running the runbooks on a user's behalf very easy.</span></span> <span data-ttu-id="2dc6d-141">이에 대한 자세한 내용은 아래 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2dc6d-141">You can read more about this in the article below:</span></span>

* [<span data-ttu-id="2dc6d-142">Azure 실행 계정으로 Runbook 인증</span><span class="sxs-lookup"><span data-stu-id="2dc6d-142">Authenticate Runbooks with Azure Run As account</span></span>](../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-azure-automation-vertical-scale-runbooks-into-your-subscription"></a><span data-ttu-id="2dc6d-143">구독으로 Azure 자동화 수직 규모 runbook 가져오기</span><span class="sxs-lookup"><span data-stu-id="2dc6d-143">Import Azure Automation Vertical Scale runbooks into your subscription</span></span>
<span data-ttu-id="2dc6d-144">VM 규모 집합을 수직으로 확장하는 데 필요한 Runbook은 Azure 자동화 Runbook 갤러리에 이미 게시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dc6d-144">The runbooks needed to vertically scale your VM Scale Sets are already published in the Azure Automation Runbook Gallery.</span></span> <span data-ttu-id="2dc6d-145">이들을 구독으로 가져오려면 이 문서의 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="2dc6d-145">To import them into your subscription follow the steps in this article:</span></span>

* [<span data-ttu-id="2dc6d-146">Azure 자동화용 Runbook 및 모듈 갤러리</span><span class="sxs-lookup"><span data-stu-id="2dc6d-146">Runbook and module galleries for Azure Automation</span></span>](../automation/automation-runbook-gallery.md)

<span data-ttu-id="2dc6d-147">Runbook 메뉴에서 갤러리 찾아보기 옵션을 선택:</span><span class="sxs-lookup"><span data-stu-id="2dc6d-147">Choose the Browse Gallery option from the Runbooks menu:</span></span>

![가져올 Runbook][runbooks]

<span data-ttu-id="2dc6d-149">가져와야 하는 Runbook이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2dc6d-149">The runbooks that need to be imported are shown.</span></span> <span data-ttu-id="2dc6d-150">수직 규모 조정 시 다시 프로비저닝을 사용할지 여부에 따라 Runbook을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2dc6d-150">Select the runbook based on whether you want vertical scaling with or without reprovisioning:</span></span>

![Runbook 갤러리][gallery]

## <a name="add-a-webhook-to-your-runbook"></a><span data-ttu-id="2dc6d-152">Runbook에 Webhook 추가</span><span class="sxs-lookup"><span data-stu-id="2dc6d-152">Add a webhook to your runbook</span></span>
<span data-ttu-id="2dc6d-153">Runbook을 가져온 후 VM 규모 집합에서 경고에 의해 트리거될 수 있도록 Runbook에 Webhook를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2dc6d-153">Once you've imported the runbooks you'll need to add a webhook to the runbook so it can be triggered by an alert from a VM Scale Set.</span></span> <span data-ttu-id="2dc6d-154">Runbook에 대한 Webhook를 만드는 자세한 방법을 이 문서에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2dc6d-154">The details of creating a webhook for your Runbook are described in this article:</span></span>

* [<span data-ttu-id="2dc6d-155">Azure 자동화 Webhook</span><span class="sxs-lookup"><span data-stu-id="2dc6d-155">Azure Automation webhooks</span></span>](../automation/automation-webhooks.md)

> [!NOTE]
> <span data-ttu-id="2dc6d-156">다음 섹션에서 필요하므로 Webhook URI 대화 상자를 닫기 전에 Webhook를 복사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dc6d-156">Make sure you copy the webhook URI before closing the webhook dialog as you will need this in the next section.</span></span>
> 
> 

## <a name="add-an-alert-to-your-vm-scale-set"></a><span data-ttu-id="2dc6d-157">VM 규모 집합에 경고 추가</span><span class="sxs-lookup"><span data-stu-id="2dc6d-157">Add an alert to your VM Scale Set</span></span>
<span data-ttu-id="2dc6d-158">다음은 VM 규모 집합에 경고를 추가하는 방법을 보여 주는 PowerShell 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="2dc6d-158">Below is a PowerShell script which shows how to add an alert to a VM Scale Set.</span></span> <span data-ttu-id="2dc6d-159">[Azure Monitor 자동 크기 조정 공용 메트릭](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md)문서를 참조하여 경고를 시작할 메트릭의 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2dc6d-159">Refer to the following article to get the name of the metric to fire the alert on: [Azure Monitor autoscaling common metrics](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span></span>

```
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail user@contoso.com
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri <uri-of-the-webhook>
$threshold = <value-of-the-threshold>
$rg = <resource-group-name>
$id = <resource-id-to-add-the-alert-to>
$location = <location-of-the-resource>
$alertName = <name-of-the-resource>
$metricName = <metric-to-fire-the-alert-on>
$timeWindow = <time-window-in-hh:mm:ss-format>
$condition = <condition-for-the-threshold> # Other valid values are LessThanOrEqual, GreaterThan, GreaterThanOrEqual
$description = <description-for-the-alert>

Add-AzureRmMetricAlertRule  -Name  $alertName `
                            -Location  $location `
                            -ResourceGroup $rg `
                            -TargetResourceId $id `
                            -MetricName $metricName `
                            -Operator  $condition `
                            -Threshold $threshold `
                            -WindowSize  $timeWindow `
                            -TimeAggregationOperator Average `
                            -Actions $actionEmail, $actionWebhook `
                            -Description $description
```

> [!NOTE]
> <span data-ttu-id="2dc6d-160">수직 규모 조정 및 너무 잦은 연결 서비스 중단을 방지하기 위해 경고에 대한 합리적인 기간을 구성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2dc6d-160">It is recommended to configure a reasonable time window for the alert in order to avoid triggering vertical scaling, and any associated service interruption, too often.</span></span> <span data-ttu-id="2dc6d-161">최소 20-30 분 이상 기간을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dc6d-161">Consider a window of least 20-30 minutes or more.</span></span> <span data-ttu-id="2dc6d-162">중단을 방지하기 위해 필요한 경우 수평 규모 조정을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="2dc6d-162">Consider horizontal scaling if you need to avoid any interruption.</span></span>
> 
> 

<span data-ttu-id="2dc6d-163">경고를 만드는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2dc6d-163">For more information on how to create alerts refer to the following articles:</span></span>

* [<span data-ttu-id="2dc6d-164">Azure Monitor PowerShell 빠른 시작 샘플</span><span class="sxs-lookup"><span data-stu-id="2dc6d-164">Azure Monitor PowerShell quick start samples</span></span>](../monitoring-and-diagnostics/insights-powershell-samples.md)
* [<span data-ttu-id="2dc6d-165">Azure Monitor 플랫폼 간 CLI 빠른 시작 샘플</span><span class="sxs-lookup"><span data-stu-id="2dc6d-165">Azure Monitor Cross-platform CLI quick start samples</span></span>](../monitoring-and-diagnostics/insights-cli-samples.md)

## <a name="summary"></a><span data-ttu-id="2dc6d-166">요약</span><span class="sxs-lookup"><span data-stu-id="2dc6d-166">Summary</span></span>
<span data-ttu-id="2dc6d-167">이 문서에서 간단한 수직 규모 조정 예제를 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="2dc6d-167">This article showed simple vertical scaling examples.</span></span> <span data-ttu-id="2dc6d-168">자동화 계정, Runbook, Webhook, 경고 등 이러한 구성 요소를 사용하여 다양한 이벤트를 사용자 지정 작업 집합과 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dc6d-168">With these building blocks - Automation account, runbooks, webhooks, alerts - you can connect a rich variety of events with a customized set of actions.</span></span>

[runbooks]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks.png
[gallery]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks-gallery.png
