---
title: "aaaVertically 배율 Azure 가상 컴퓨터 크기 집합 | Microsoft Docs"
description: "Toovertically 응답 toomonitoring 알림 Azure 자동화에서 가상 컴퓨터를 확장 하는 방법을"
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
ms.openlocfilehash: 1cc35a805b6a5742252a89c21588ca451ff547a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="vertical-autoscale-with-virtual-machine-scale-sets"></a><span data-ttu-id="f7e15-103">가상 컴퓨터 규모 집합을 사용하여 수직 자동 규모 조정</span><span class="sxs-lookup"><span data-stu-id="f7e15-103">Vertical autoscale with Virtual Machine Scale sets</span></span>
<span data-ttu-id="f7e15-104">이 문서에서는 toovertically Azure를 확장 하는 방법을 설명 [가상 컴퓨터 크기 집합](https://azure.microsoft.com/services/virtual-machine-scale-sets/) 상관 없이 다시 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e15-104">This article describes how toovertically scale Azure [Virtual Machine Scale Sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/) with or without reprovisioning.</span></span> <span data-ttu-id="f7e15-105">Vm 크기 집합에 없는의 세로 배율에 대 한 참조 너무[Azure 자동화 인 Azure 가상 컴퓨터의 크기를 세로로 조정](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e15-105">For vertical scaling of VMs which are not in scale sets, refer too[Vertically scale Azure virtual machine with Azure Automation](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="f7e15-106">라고도 세로 배율, *수직* 및 *규모 축소*응답 tooa 작업에서 가상 컴퓨터 (VM) 크기를 늘리거나 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e15-106">Vertical scaling, also known as *scale up* and *scale down*, means increasing or decreasing virtual machine (VM) sizes in response tooa workload.</span></span> <span data-ttu-id="f7e15-107">이를 비교 [수평적 확장](virtual-machine-scale-sets-autoscale-overview.md), tooas 라고도 *확장할* 및 *으로 크기를 조정*hello Vm 수 hello 작업 부하에 따라 변경 하는, 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e15-107">Compare this with [horizontal scaling](virtual-machine-scale-sets-autoscale-overview.md), also referred tooas *scale out* and *scale in*, where hello number of VMs is altered depending on hello workload.</span></span>

<span data-ttu-id="f7e15-108">다시 프로비저닝이란 기존 VM을 제거하고 새 VM으로 바꾸는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e15-108">Reprovisioning means removing an existing VM and replacing it with a new one.</span></span> <span data-ttu-id="f7e15-109">VM 크기 집합에 있는 Vm의 hello 크기를 늘리거나 때 경우에 따라 tooresize 기존 Vm을 toodeploy 다른 경우에 필요 하는 동안 데이터를 유지 hello 새 크기의 새 Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="f7e15-109">When you increase or decrease hello size of VMs in a VM Scale Set, in some cases you want tooresize existing VMs and retain your data, while in other cases you need toodeploy new VMs of hello new size.</span></span> <span data-ttu-id="f7e15-110">이 문서에서는 두 경우를 모두 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e15-110">This document covers both cases.</span></span>

<span data-ttu-id="f7e15-111">수직 규모 조정이 유용할 수 있는 경우:</span><span class="sxs-lookup"><span data-stu-id="f7e15-111">Vertical scaling can be useful when:</span></span>

* <span data-ttu-id="f7e15-112">가상 컴퓨터에 만들어진 서비스는 잘 이용되지 않습니다(예를 들어 주말).</span><span class="sxs-lookup"><span data-stu-id="f7e15-112">A service built on virtual machines is under-utilized (for example at weekends).</span></span> <span data-ttu-id="f7e15-113">Hello VM 크기를 줄이는 한 월별 비용을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7e15-113">Reducing hello VM size can reduce monthly costs.</span></span>
* <span data-ttu-id="f7e15-114">추가 Vm을 만들지 않고 더 큰 요청 된 VM 크기 toocope 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e15-114">Increasing VM size toocope with larger demand without creating additional VMs.</span></span>

<span data-ttu-id="f7e15-115">세로 설정한 VM 크기 집합의 메트릭 기반된 경고에 따라 트리거되는 toobe 크기 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e15-115">You can set up vertical scaling toobe triggered based on metric based alerts from your VM Scale Set.</span></span> <span data-ttu-id="f7e15-116">Hello 경고가 활성화 될 때는 webhook 눈금 확장 될 수 있는 runbook 설정 위나 아래로 트리거가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e15-116">When hello alert is activated it fires a webhook that triggers a runbook which can scale your scale set up or down.</span></span> <span data-ttu-id="f7e15-117">수직 규모 조정을 다음과 같은 단계에 따라 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7e15-117">Vertical scaling can be configured by following these steps:</span></span>

1. <span data-ttu-id="f7e15-118">실행 기능을 사용하여 Azure 자동화 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f7e15-118">Create an Azure Automation account with run-as capability.</span></span>
2. <span data-ttu-id="f7e15-119">VM 규모 집합용 Azure 자동화 수직 규모 조정 Runbook을 구독으로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f7e15-119">Import Azure Automation Vertical Scale runbooks for VM Scale Sets into your subscription.</span></span>
3. <span data-ttu-id="f7e15-120">Webhook tooyour runbook을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e15-120">Add a webhook tooyour runbook.</span></span>
4. <span data-ttu-id="f7e15-121">VM 크기 집합 webhook 알림을 사용 하는 경고 tooyour를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e15-121">Add an alert tooyour VM Scale Set using a webhook notification.</span></span>

> [!NOTE]
> <span data-ttu-id="f7e15-122">수직 자동 규모 조정은 특정 범위의 VM 규모 이내에서만 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7e15-122">Vertical autoscaling can only take place within certain ranges of VM sizes.</span></span> <span data-ttu-id="f7e15-123">하나의 tooanother tooscale 결정 하기 전에 각 크기의 hello 사양을 비교 (값이 클수록 항상 나타내지 않는 더 큰 VM 크기).</span><span class="sxs-lookup"><span data-stu-id="f7e15-123">Compare hello specifications of each size before deciding tooscale from one tooanother (higher number does not always indicate bigger VM size).</span></span> <span data-ttu-id="f7e15-124">Hello 크기의 쌍을 따르는 사이의 tooscale를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7e15-124">You can choose tooscale between hello following pairs of sizes:</span></span>
> 
> | <span data-ttu-id="f7e15-125">VM 크기 조정 쌍</span><span class="sxs-lookup"><span data-stu-id="f7e15-125">VM sizes scaling pair</span></span> |  |
> | --- | --- |
> | <span data-ttu-id="f7e15-126">Standard_A0</span><span class="sxs-lookup"><span data-stu-id="f7e15-126">Standard_A0</span></span> |<span data-ttu-id="f7e15-127">Standard_A11</span><span class="sxs-lookup"><span data-stu-id="f7e15-127">Standard_A11</span></span> |
> | <span data-ttu-id="f7e15-128">Standard_D1</span><span class="sxs-lookup"><span data-stu-id="f7e15-128">Standard_D1</span></span> |<span data-ttu-id="f7e15-129">Standard_D14</span><span class="sxs-lookup"><span data-stu-id="f7e15-129">Standard_D14</span></span> |
> | <span data-ttu-id="f7e15-130">Standard_DS1</span><span class="sxs-lookup"><span data-stu-id="f7e15-130">Standard_DS1</span></span> |<span data-ttu-id="f7e15-131">Standard_DS14</span><span class="sxs-lookup"><span data-stu-id="f7e15-131">Standard_DS14</span></span> |
> | <span data-ttu-id="f7e15-132">Standard_D1v2</span><span class="sxs-lookup"><span data-stu-id="f7e15-132">Standard_D1v2</span></span> |<span data-ttu-id="f7e15-133">Standard_D15v2</span><span class="sxs-lookup"><span data-stu-id="f7e15-133">Standard_D15v2</span></span> |
> | <span data-ttu-id="f7e15-134">Standard_G1</span><span class="sxs-lookup"><span data-stu-id="f7e15-134">Standard_G1</span></span> |<span data-ttu-id="f7e15-135">Standard_G5</span><span class="sxs-lookup"><span data-stu-id="f7e15-135">Standard_G5</span></span> |
> | <span data-ttu-id="f7e15-136">Standard_GS1</span><span class="sxs-lookup"><span data-stu-id="f7e15-136">Standard_GS1</span></span> |<span data-ttu-id="f7e15-137">Standard_GS5</span><span class="sxs-lookup"><span data-stu-id="f7e15-137">Standard_GS5</span></span> |
> 
> 

## <a name="create-an-azure-automation-account-with-run-as-capability"></a><span data-ttu-id="f7e15-138">실행 기능을 사용하여 Azure 자동화 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="f7e15-138">Create an Azure Automation Account with run-as capability</span></span>
<span data-ttu-id="f7e15-139">hello가 가장 먼저 해야 toodo hello 사용 되는 runbook tooscale hello VM 크기 집합 인스턴스를 호스팅하는 Azure 자동화 계정 만들기.</span><span class="sxs-lookup"><span data-stu-id="f7e15-139">hello first thing you need toodo is create an Azure Automation account that will host hello runbooks used tooscale hello VM Scale Set instances.</span></span> <span data-ttu-id="f7e15-140">최근에 [Azure 자동화](https://azure.microsoft.com/services/automation/) 는 설정 hello 서비스 사용자를 위해 자동으로 실행 중인 hello runbook 사용자 대신에 매우 쉽게 hello "계정으로 실행" 기능을 소개 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f7e15-140">Recently [Azure Automation](https://azure.microsoft.com/services/automation/) introduced hello "Run As account" feature which makes setting up hello Service Principal for automatically running hello runbooks on a user's behalf very easy.</span></span> <span data-ttu-id="f7e15-141">자세한 내용은 아래 hello 기술 자료 문서에서이 내용을:</span><span class="sxs-lookup"><span data-stu-id="f7e15-141">You can read more about this in hello article below:</span></span>

* [<span data-ttu-id="f7e15-142">Azure 실행 계정으로 Runbook 인증</span><span class="sxs-lookup"><span data-stu-id="f7e15-142">Authenticate Runbooks with Azure Run As account</span></span>](../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-azure-automation-vertical-scale-runbooks-into-your-subscription"></a><span data-ttu-id="f7e15-143">구독으로 Azure 자동화 수직 규모 runbook 가져오기</span><span class="sxs-lookup"><span data-stu-id="f7e15-143">Import Azure Automation Vertical Scale runbooks into your subscription</span></span>
<span data-ttu-id="f7e15-144">hello runbook에는 VM 크기 집합이 hello Azure 자동화 Runbook 갤러리에에서 이미 게시 되어 toovertically 배율이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e15-144">hello runbooks needed toovertically scale your VM Scale Sets are already published in hello Azure Automation Runbook Gallery.</span></span> <span data-ttu-id="f7e15-145">이 문서의 단계를 tooimport hello에 따라 구독에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e15-145">tooimport them into your subscription follow hello steps in this article:</span></span>

* [<span data-ttu-id="f7e15-146">Azure 자동화용 Runbook 및 모듈 갤러리</span><span class="sxs-lookup"><span data-stu-id="f7e15-146">Runbook and module galleries for Azure Automation</span></span>](../automation/automation-runbook-gallery.md)

<span data-ttu-id="f7e15-147">Hello Runbook 메뉴에서 hello 찾아보기 갤러리 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e15-147">Choose hello Browse Gallery option from hello Runbooks menu:</span></span>

![가져온 Runbook toobe][runbooks]

<span data-ttu-id="f7e15-149">가져온 toobe 해야 하는 hello runbook이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7e15-149">hello runbooks that need toobe imported are shown.</span></span> <span data-ttu-id="f7e15-150">세로 배율 상관 없이 다시 프로 비전 하려는 여부에 따라 hello runbook을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e15-150">Select hello runbook based on whether you want vertical scaling with or without reprovisioning:</span></span>

![Runbook 갤러리][gallery]

## <a name="add-a-webhook-tooyour-runbook"></a><span data-ttu-id="f7e15-152">Webhook tooyour runbook 추가</span><span class="sxs-lookup"><span data-stu-id="f7e15-152">Add a webhook tooyour runbook</span></span>
<span data-ttu-id="f7e15-153">Hello runbook을 가져온 후 VM 크기 집합에서 발생 한 경고에 의해 트리거될 수 있으므로 tooadd webhook toohello runbook 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e15-153">Once you've imported hello runbooks you'll need tooadd a webhook toohello runbook so it can be triggered by an alert from a VM Scale Set.</span></span> <span data-ttu-id="f7e15-154">이 문서는 webhook Runbook에 대 한 만들기의 hello 세부 정보를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e15-154">hello details of creating a webhook for your Runbook are described in this article:</span></span>

* [<span data-ttu-id="f7e15-155">Azure 자동화 Webhook</span><span class="sxs-lookup"><span data-stu-id="f7e15-155">Azure Automation webhooks</span></span>](../automation/automation-webhooks.md)

> [!NOTE]
> <span data-ttu-id="f7e15-156">Hello 다음 섹션에서이 필요 하므로 hello webhook 대화 상자를 닫기 전에 hello webhook URI를 복사 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e15-156">Make sure you copy hello webhook URI before closing hello webhook dialog as you will need this in hello next section.</span></span>
> 
> 

## <a name="add-an-alert-tooyour-vm-scale-set"></a><span data-ttu-id="f7e15-157">VM 크기 집합 경고 tooyour 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="f7e15-157">Add an alert tooyour VM Scale Set</span></span>
<span data-ttu-id="f7e15-158">다음은 이러한는 PowerShell 스크립트를 표시 방법 tooadd는 경고 tooa VM 크기 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="f7e15-158">Below is a PowerShell script which shows how tooadd an alert tooa VM Scale Set.</span></span> <span data-ttu-id="f7e15-159">참조 hello 메트릭 toofire hello 경고의 문서 tooget hello 이름 다음 toohello: [Azure 모니터 자동 크기 조정에 대 한 일반 메트릭을](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e15-159">Refer toohello following article tooget hello name of hello metric toofire hello alert on: [Azure Monitor autoscaling common metrics](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span></span>

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
> <span data-ttu-id="f7e15-160">권장 tooconfigure 세로 배율 트리거 순서 tooavoid hello 알림에 대 한 적절 한 시간 창 및 연결 된 서비스 중단을 자주 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7e15-160">It is recommended tooconfigure a reasonable time window for hello alert in order tooavoid triggering vertical scaling, and any associated service interruption, too often.</span></span> <span data-ttu-id="f7e15-161">최소 20-30 분 이상 기간을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7e15-161">Consider a window of least 20-30 minutes or more.</span></span> <span data-ttu-id="f7e15-162">중단 tooavoid 필요한 경우 크기 조정 가로 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f7e15-162">Consider horizontal scaling if you need tooavoid any interruption.</span></span>
> 
> 

<span data-ttu-id="f7e15-163">Toocreate 경고 toohello 다음 문서를 참조 하는 방법에 대 한 자세한 내용은:</span><span class="sxs-lookup"><span data-stu-id="f7e15-163">For more information on how toocreate alerts refer toohello following articles:</span></span>

* [<span data-ttu-id="f7e15-164">Azure Monitor PowerShell 빠른 시작 샘플</span><span class="sxs-lookup"><span data-stu-id="f7e15-164">Azure Monitor PowerShell quick start samples</span></span>](../monitoring-and-diagnostics/insights-powershell-samples.md)
* [<span data-ttu-id="f7e15-165">Azure Monitor 플랫폼 간 CLI 빠른 시작 샘플</span><span class="sxs-lookup"><span data-stu-id="f7e15-165">Azure Monitor Cross-platform CLI quick start samples</span></span>](../monitoring-and-diagnostics/insights-cli-samples.md)

## <a name="summary"></a><span data-ttu-id="f7e15-166">요약</span><span class="sxs-lookup"><span data-stu-id="f7e15-166">Summary</span></span>
<span data-ttu-id="f7e15-167">이 문서에서 간단한 수직 규모 조정 예제를 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="f7e15-167">This article showed simple vertical scaling examples.</span></span> <span data-ttu-id="f7e15-168">자동화 계정, Runbook, Webhook, 경고 등 이러한 구성 요소를 사용하여 다양한 이벤트를 사용자 지정 작업 집합과 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7e15-168">With these building blocks - Automation account, runbooks, webhooks, alerts - you can connect a rich variety of events with a customized set of actions.</span></span>

[runbooks]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks.png
[gallery]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks-gallery.png
