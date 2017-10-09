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
# <a name="vertical-autoscale-with-virtual-machine-scale-sets"></a>가상 컴퓨터 규모 집합을 사용하여 수직 자동 규모 조정
이 문서에서는 toovertically Azure를 확장 하는 방법을 설명 [가상 컴퓨터 크기 집합](https://azure.microsoft.com/services/virtual-machine-scale-sets/) 상관 없이 다시 프로 비전 합니다. Vm 크기 집합에 없는의 세로 배율에 대 한 참조 너무[Azure 자동화 인 Azure 가상 컴퓨터의 크기를 세로로 조정](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

라고도 세로 배율, *수직* 및 *규모 축소*응답 tooa 작업에서 가상 컴퓨터 (VM) 크기를 늘리거나 의미 합니다. 이를 비교 [수평적 확장](virtual-machine-scale-sets-autoscale-overview.md), tooas 라고도 *확장할* 및 *으로 크기를 조정*hello Vm 수 hello 작업 부하에 따라 변경 하는, 합니다.

다시 프로비저닝이란 기존 VM을 제거하고 새 VM으로 바꾸는 것을 의미합니다. VM 크기 집합에 있는 Vm의 hello 크기를 늘리거나 때 경우에 따라 tooresize 기존 Vm을 toodeploy 다른 경우에 필요 하는 동안 데이터를 유지 hello 새 크기의 새 Vm입니다. 이 문서에서는 두 경우를 모두 설명합니다.

수직 규모 조정이 유용할 수 있는 경우:

* 가상 컴퓨터에 만들어진 서비스는 잘 이용되지 않습니다(예를 들어 주말). Hello VM 크기를 줄이는 한 월별 비용을 줄일 수 있습니다.
* 추가 Vm을 만들지 않고 더 큰 요청 된 VM 크기 toocope 증가 합니다.

세로 설정한 VM 크기 집합의 메트릭 기반된 경고에 따라 트리거되는 toobe 크기 조정 합니다. Hello 경고가 활성화 될 때는 webhook 눈금 확장 될 수 있는 runbook 설정 위나 아래로 트리거가 발생 합니다. 수직 규모 조정을 다음과 같은 단계에 따라 구성할 수 있습니다.

1. 실행 기능을 사용하여 Azure 자동화 계정을 만듭니다.
2. VM 규모 집합용 Azure 자동화 수직 규모 조정 Runbook을 구독으로 가져옵니다.
3. Webhook tooyour runbook을 추가 합니다.
4. VM 크기 집합 webhook 알림을 사용 하는 경고 tooyour를 추가 합니다.

> [!NOTE]
> 수직 자동 규모 조정은 특정 범위의 VM 규모 이내에서만 수행할 수 있습니다. 하나의 tooanother tooscale 결정 하기 전에 각 크기의 hello 사양을 비교 (값이 클수록 항상 나타내지 않는 더 큰 VM 크기). Hello 크기의 쌍을 따르는 사이의 tooscale를 선택할 수 있습니다.
> 
> | VM 크기 조정 쌍 |  |
> | --- | --- |
> | Standard_A0 |Standard_A11 |
> | Standard_D1 |Standard_D14 |
> | Standard_DS1 |Standard_DS14 |
> | Standard_D1v2 |Standard_D15v2 |
> | Standard_G1 |Standard_G5 |
> | Standard_GS1 |Standard_GS5 |
> 
> 

## <a name="create-an-azure-automation-account-with-run-as-capability"></a>실행 기능을 사용하여 Azure 자동화 계정 만들기
hello가 가장 먼저 해야 toodo hello 사용 되는 runbook tooscale hello VM 크기 집합 인스턴스를 호스팅하는 Azure 자동화 계정 만들기. 최근에 [Azure 자동화](https://azure.microsoft.com/services/automation/) 는 설정 hello 서비스 사용자를 위해 자동으로 실행 중인 hello runbook 사용자 대신에 매우 쉽게 hello "계정으로 실행" 기능을 소개 했습니다. 자세한 내용은 아래 hello 기술 자료 문서에서이 내용을:

* [Azure 실행 계정으로 Runbook 인증](../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-azure-automation-vertical-scale-runbooks-into-your-subscription"></a>구독으로 Azure 자동화 수직 규모 runbook 가져오기
hello runbook에는 VM 크기 집합이 hello Azure 자동화 Runbook 갤러리에에서 이미 게시 되어 toovertically 배율이 필요 합니다. 이 문서의 단계를 tooimport hello에 따라 구독에 해당 합니다.

* [Azure 자동화용 Runbook 및 모듈 갤러리](../automation/automation-runbook-gallery.md)

Hello Runbook 메뉴에서 hello 찾아보기 갤러리 옵션을 선택 합니다.

![가져온 Runbook toobe][runbooks]

가져온 toobe 해야 하는 hello runbook이 표시 됩니다. 세로 배율 상관 없이 다시 프로 비전 하려는 여부에 따라 hello runbook을 선택 합니다.

![Runbook 갤러리][gallery]

## <a name="add-a-webhook-tooyour-runbook"></a>Webhook tooyour runbook 추가
Hello runbook을 가져온 후 VM 크기 집합에서 발생 한 경고에 의해 트리거될 수 있으므로 tooadd webhook toohello runbook 야 합니다. 이 문서는 webhook Runbook에 대 한 만들기의 hello 세부 정보를 설명 합니다.

* [Azure 자동화 Webhook](../automation/automation-webhooks.md)

> [!NOTE]
> Hello 다음 섹션에서이 필요 하므로 hello webhook 대화 상자를 닫기 전에 hello webhook URI를 복사 하 고 있는지 확인 합니다.
> 
> 

## <a name="add-an-alert-tooyour-vm-scale-set"></a>VM 크기 집합 경고 tooyour 프로그램 추가
다음은 이러한는 PowerShell 스크립트를 표시 방법 tooadd는 경고 tooa VM 크기 집합입니다. 참조 hello 메트릭 toofire hello 경고의 문서 tooget hello 이름 다음 toohello: [Azure 모니터 자동 크기 조정에 대 한 일반 메트릭을](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md)합니다.

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
> 권장 tooconfigure 세로 배율 트리거 순서 tooavoid hello 알림에 대 한 적절 한 시간 창 및 연결 된 서비스 중단을 자주 있습니다. 최소 20-30 분 이상 기간을 고려해야 합니다. 중단 tooavoid 필요한 경우 크기 조정 가로 것이 좋습니다.
> 
> 

Toocreate 경고 toohello 다음 문서를 참조 하는 방법에 대 한 자세한 내용은:

* [Azure Monitor PowerShell 빠른 시작 샘플](../monitoring-and-diagnostics/insights-powershell-samples.md)
* [Azure Monitor 플랫폼 간 CLI 빠른 시작 샘플](../monitoring-and-diagnostics/insights-cli-samples.md)

## <a name="summary"></a>요약
이 문서에서 간단한 수직 규모 조정 예제를 살펴보았습니다. 자동화 계정, Runbook, Webhook, 경고 등 이러한 구성 요소를 사용하여 다양한 이벤트를 사용자 지정 작업 집합과 연결할 수 있습니다.

[runbooks]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks.png
[gallery]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks-gallery.png
