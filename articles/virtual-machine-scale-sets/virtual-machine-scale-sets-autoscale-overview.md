---
title: "자동 크기 조정 및 가상 컴퓨터 확장 집합 | Microsoft Docs"
description: "진단 및 자동 크기 조정 리소스를 사용하여 규모 집합의 가상 컴퓨터를 자동적으로 크기 조정하는 방법을 알아봅니다."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d29a3385-179e-4331-a315-daa7ea5701df
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: adegeo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 06ff9d9ae1dd8256f0d22c1a60ed6a85554f1f17
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-automatic-scaling-and-virtual-machine-scale-sets"></a><span data-ttu-id="9a6bb-103">자동 크기 조정 및 가상 컴퓨터 규모 집합 사용 방법</span><span class="sxs-lookup"><span data-stu-id="9a6bb-103">How to use automatic scaling and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="9a6bb-104">크기 집합에서 수행되는 가상 컴퓨터 자동 크기 조정은 성능 요구 사항에 일치하기 위해 필요에 따라 집합에서 컴퓨터를 만들거나 삭제하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-104">Automatic scaling of virtual machines in a scale set is the creation or deletion of machines in the set as needed to match performance requirements.</span></span> <span data-ttu-id="9a6bb-105">작업량이 증가하면 작업을 효과적으로 수행할 수 있도록 응용 프로그램에 추가 리소스가 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-105">As the volume of work grows, an application may require additional resources to enable it to effectively perform tasks.</span></span>

<span data-ttu-id="9a6bb-106">자동 크기 조정은 관리 오버헤드를 줄이기 위해 자동화된 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-106">Automatic scaling is an automated process that helps ease management overhead.</span></span> <span data-ttu-id="9a6bb-107">오버헤드를 줄이면 지속적으로 시스템 성능을 모니터링하거나 리소스 관리 방법을 결정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-107">By reducing overhead, you don't need to continually monitor system performance or decide how to manage resources.</span></span> <span data-ttu-id="9a6bb-108">크기 조정은 탄력적인 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-108">Scaling is an elastic process.</span></span> <span data-ttu-id="9a6bb-109">부하가 증가하면 더 많은 리소스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-109">More resources can be added as the load increases.</span></span> <span data-ttu-id="9a6bb-110">수요가 감소할 경우 비용을 최소화하고 성능 수준을 유지하기 위해 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-110">And as demand decreases, resources can be removed to minimize costs and maintain performance levels.</span></span>

<span data-ttu-id="9a6bb-111">Azure Resource Manager 템플릿, Azure PowerShell, Azure CLI 또는 Azure Portal을 사용하여 크기 집합에 자동 크기 조정을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-111">Set up automatic scaling on a scale set by using an Azure Resource Manager template, Azure PowerShell, Azure CLI, or the Azure portal.</span></span>

## <a name="set-up-scaling-by-using-resource-manager-templates"></a><span data-ttu-id="9a6bb-112">리소스 관리자 템플릿을 사용하여 크기 조정 설정</span><span class="sxs-lookup"><span data-stu-id="9a6bb-112">Set up scaling by using Resource Manager templates</span></span>
<span data-ttu-id="9a6bb-113">각 응용 프로그램의 리소스를 개별적으로 배포하고 관리하는 대신, 모든 리소스를 하나의 조정된 작업으로 배포하는 템플릿을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-113">Rather than deploying and managing each resource of your application separately, use a template that deploys all resources in a single, coordinated operation.</span></span> <span data-ttu-id="9a6bb-114">템플릿에서 응용 프로그램 리소스를 정의하고 다양한 환경에 대한 배포 매개 변수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-114">In the template, application resources are defined and deployment parameters are specified for different environments.</span></span> <span data-ttu-id="9a6bb-115">템플릿은 배포에 대한 값을 생성하는 데 사용할 수 있는 식과 JSON으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-115">The template consists of JSON and expressions that you can use to construct values for your deployment.</span></span> <span data-ttu-id="9a6bb-116">자세한 내용은 [Azure Resource Manager 템플릿 작성](../azure-resource-manager/resource-group-authoring-templates.md)을 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-116">To learn more, look at [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="9a6bb-117">템플릿에서 용량 요소를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-117">In the template, you specify the capacity element:</span></span>

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 3
},
```

<span data-ttu-id="9a6bb-118">용량은 집합에 있는 가상 컴퓨터의 수를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-118">Capacity identifies the number of virtual machines in the set.</span></span> <span data-ttu-id="9a6bb-119">다른 값으로 템플릿을 배포하여 용량을 수동으로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-119">You can manually change the capacity by deploying a template with a different value.</span></span> <span data-ttu-id="9a6bb-120">단순히 용량을 변경하기 위해 템플릿을 배포하고 있는 경우 업데이트된 용량의 SKU 요소만을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-120">If you are deploying a template to only change the capacity, you can include only the SKU element with the updated capacity.</span></span>

<span data-ttu-id="9a6bb-121">**autoscaleSettings** 리소스와 진단 확장을 조합하여 확장 집합의 용량을 자동으로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-121">The capacity of your scale set can be automatically adjusted by using a combination of the **autoscaleSettings** resource and the diagnostics extension.</span></span>

### <a name="configure-the-azure-diagnostics-extension"></a><span data-ttu-id="9a6bb-122">Azure 진단 확장 구성</span><span class="sxs-lookup"><span data-stu-id="9a6bb-122">Configure the Azure Diagnostics extension</span></span>
<span data-ttu-id="9a6bb-123">규모 집합의 각 가상 컴퓨터에서 메트릭을 수집할 수 있는 경우에만 자동 크기 조정을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-123">Automatic scaling can only be done if metrics collection is successful on each virtual machine in the scale set.</span></span> <span data-ttu-id="9a6bb-124">Azure 진단 확장은 자동 크기 조정 리소스의 메트릭 수집 요구 사항을 충족하는 모니터링 및 진단 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-124">The Azure Diagnostics Extension provides the monitoring and diagnostics capabilities that meets the metrics collection needs of the autoscale resource.</span></span> <span data-ttu-id="9a6bb-125">리소스 관리자 템플릿의 일부로 확장을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-125">You can install the extension as part of the Resource Manager template.</span></span>

<span data-ttu-id="9a6bb-126">이 예제에서는 진단 확장을 구성하는 템플릿에 사용되는 변수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-126">This example shows the variables that are used in the template to configure the diagnostics extension:</span></span>

```json
"diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'saa')]",
"accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/', 'Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
"wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
"wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Thread Count\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
"wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
"wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
"wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
```

<span data-ttu-id="9a6bb-127">템플릿이 배포될 때 매개 변수가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-127">Parameters are provided when the template is deployed.</span></span> <span data-ttu-id="9a6bb-128">이 예제에서 데이터가 저장되는 저장소 계정 이름 및 데이터가 수집되는 확장 집합 이름이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-128">In this example, the name of the storage account (where data is stored) and the name of the scale set (where data is collected) are provided.</span></span> <span data-ttu-id="9a6bb-129">또한 이 Windows Server 예제에서는 Thread Count 성능 카운터가 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-129">Also in this Windows Server example, only the Thread Count performance counter is collected.</span></span> <span data-ttu-id="9a6bb-130">Windows 또는 Linux에 있는 모든 사용 가능한 성능 카운터가 진단 정보 수집에 사용될 수 있고 확장 구성에 포함될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-130">All the available performance counters in Windows or Linux can be used to collect diagnostics information and can be included in the extension configuration.</span></span>

<span data-ttu-id="9a6bb-131">이 예제에서는 템플릿의 확장 정의를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-131">This example shows the definition of the extension in the template:</span></span>

```json
"extensionProfile": {
  "extensions": [
    {
      "name": "Microsoft.Insights.VMDiagnosticsSettings",
      "properties": {
        "publisher": "Microsoft.Azure.Diagnostics",
        "type": "IaaSDiagnostics",
        "typeHandlerVersion": "1.5",
        "autoUpgradeMinorVersion": true,
        "settings": {
          "xmlCfg": "[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
          "storageAccount": "[variables('diagnosticsStorageAccountName')]"
        },
        "protectedSettings": {
          "storageAccountName": "[variables('diagnosticsStorageAccountName')]",
          "storageAccountKey": "[listkeys(variables('accountid'), variables('apiVersion')).key1]",
          "storageAccountEndPoint": "https://core.windows.net"
        }
      }
    }
  ]
}
```

<span data-ttu-id="9a6bb-132">진단 확장을 실행할 때 데이터는 지정한 저장소 계정에 위치한 테이블에 저장되고 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-132">When the diagnostics extension runs, the data is stored and collected in a table, in the storage account that you specify.</span></span> <span data-ttu-id="9a6bb-133">**WADPerformanceCounters** 테이블에서 수집된 데이터를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-133">In the **WADPerformanceCounters** table, you can find the collected data:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountBefore2.png)

### <a name="configure-the-autoscalesettings-resource"></a><span data-ttu-id="9a6bb-134">autoScaleSettings 리소스 구성</span><span class="sxs-lookup"><span data-stu-id="9a6bb-134">Configure the autoScaleSettings resource</span></span>
<span data-ttu-id="9a6bb-135">autoScaleSettings 리소스는 크기 집합에 있는 가상 컴퓨터의 수를 늘릴지 또는 줄일지를 결정하기 위해 진단 확장의 정보를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-135">The autoscaleSettings resource uses the information from the diagnostics extension to decide whether to increase or decrease the number of virtual machines in the scale set.</span></span>

<span data-ttu-id="9a6bb-136">이 예제에서는 템플릿의 리소스 구성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-136">This example shows the configuration of the resource in the template:</span></span>

```json
{
  "type": "Microsoft.Insights/autoscaleSettings",
  "apiVersion": "2015-04-01",
  "name": "[concat(parameters('resourcePrefix'),'as1')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
  ],
  "properties": {
    "enabled": true,
    "name": "[concat(parameters('resourcePrefix'),'as1')]",
    "profiles": [
      {
        "name": "Profile1",
        "capacity": {
          "minimum": "1",
          "maximum": "10",
          "default": "1"
        },
        "rules": [
          {
            "metricTrigger": {
              "metricName": "\\Processor(_Total)\\Thread Count",
              "metricNamespace": "",
              "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
              "timeGrain": "PT1M",
              "statistic": "Average",
              "timeWindow": "PT5M",
              "timeAggregation": "Average",
              "operator": "GreaterThan",
              "threshold": 650
            },
            "scaleAction": {
              "direction": "Increase",
              "type": "ChangeCount",
              "value": "1",
              "cooldown": "PT5M"
            }
          },
          {
            "metricTrigger": {
              "metricName": "\\Processor(_Total)\\Thread Count",
              "metricNamespace": "",
              "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
              "timeGrain": "PT1M",
              "statistic": "Average",
              "timeWindow": "PT5M",
              "timeAggregation": "Average",
              "operator": "LessThan",
              "threshold": 550
            },
            "scaleAction": {
              "direction": "Decrease",
              "type": "ChangeCount",
              "value": "1",
              "cooldown": "PT5M"
            }
          }
        ]
      }
    ],
    "targetResourceUri": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]"
  }
}
```

<span data-ttu-id="9a6bb-137">위의 예제에서는 자동 크기 조정 작업을 정의하기 위해 두 가지 규칙이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-137">In the example above, two rules are created for defining the automatic scaling actions.</span></span> <span data-ttu-id="9a6bb-138">첫 번째 규칙은 규모 확장 작업을 정의하고 두 번째 규칙은 규모 축소 작업을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-138">The first rule defines the scale-out action and the second rule defines the scale-in action.</span></span> <span data-ttu-id="9a6bb-139">다음 값이 규칙에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-139">These values are provided in the rules:</span></span>

| <span data-ttu-id="9a6bb-140">규칙</span><span class="sxs-lookup"><span data-stu-id="9a6bb-140">Rule</span></span> | <span data-ttu-id="9a6bb-141">설명</span><span class="sxs-lookup"><span data-stu-id="9a6bb-141">Description</span></span> |
| ---- | ----------- |
| <span data-ttu-id="9a6bb-142">metricName</span><span class="sxs-lookup"><span data-stu-id="9a6bb-142">metricName</span></span>        | <span data-ttu-id="9a6bb-143">이 값은 진단 확장에 대한 wadperfcounter 변수에 정의한 성능 카운터와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-143">This value is the same as the performance counter that you defined in the wadperfcounter variable for the diagnostics extension.</span></span> <span data-ttu-id="9a6bb-144">위의 예제에서는 스레드 수 카운터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-144">In the example above, the Thread Count counter is used.</span></span>    |
| <span data-ttu-id="9a6bb-145">metricResourceUri</span><span class="sxs-lookup"><span data-stu-id="9a6bb-145">metricResourceUri</span></span> | <span data-ttu-id="9a6bb-146">이 값은 가상 컴퓨터 확장 집합의 리소스 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-146">This value is the resource identifier of the virtual machine scale set.</span></span> <span data-ttu-id="9a6bb-147">이 식별자는 리소스 그룹 이름, 리소스 공급자 이름 및 크기 조정을 위한 규모 집합 이름을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-147">This identifier contains the name of the resource group, the name of the resource provider, and the name of the scale set to scale.</span></span> |
| <span data-ttu-id="9a6bb-148">timeGrain</span><span class="sxs-lookup"><span data-stu-id="9a6bb-148">timeGrain</span></span>         | <span data-ttu-id="9a6bb-149">이 값은 수집되는 메트릭의 세분성입니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-149">This value is the granularity of the metrics that are collected.</span></span> <span data-ttu-id="9a6bb-150">위의 예제에서는 1분 간격으로 데이터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-150">In the preceding example, data is collected on an interval of one minute.</span></span> <span data-ttu-id="9a6bb-151">이 값은 timeWindow와 함께 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-151">This value is used with timeWindow.</span></span> |
| <span data-ttu-id="9a6bb-152">statistic</span><span class="sxs-lookup"><span data-stu-id="9a6bb-152">statistic</span></span>         | <span data-ttu-id="9a6bb-153">이 값은 자동 크기 조정 작업을 수용하기 위해 메트릭을 결합하는 방법을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-153">This value determines how the metrics are combined to accommodate the automatic scaling action.</span></span> <span data-ttu-id="9a6bb-154">가능한 값은 평균, 최소, 최대입니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-154">The possible values are: Average, Min, Max.</span></span> |
| <span data-ttu-id="9a6bb-155">timeWindow</span><span class="sxs-lookup"><span data-stu-id="9a6bb-155">timeWindow</span></span>        | <span data-ttu-id="9a6bb-156">이 값은 인스턴스 데이터가 수집되는 시간 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-156">This value is the range of time in which instance data is collected.</span></span> <span data-ttu-id="9a6bb-157">5분에서 12시간 사이여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-157">It must be between 5 minutes and 12 hours.</span></span> |
| <span data-ttu-id="9a6bb-158">timeAggregation</span><span class="sxs-lookup"><span data-stu-id="9a6bb-158">timeAggregation</span></span>   | <span data-ttu-id="9a6bb-159">이 값은 시간이 지남에 따라 수집된 데이터가 결합되어야 하는 방법을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-159">This value determines how the data that is collected should be combined over time.</span></span> <span data-ttu-id="9a6bb-160">기본값은 평균입니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-160">The default value is Average.</span></span> <span data-ttu-id="9a6bb-161">가능한 값은 평균, 최소, 최대, 마지막, 합계, 개수입니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-161">The possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span> |
| <span data-ttu-id="9a6bb-162">operator</span><span class="sxs-lookup"><span data-stu-id="9a6bb-162">operator</span></span>          | <span data-ttu-id="9a6bb-163">이 값은 메트릭 데이터와 임계값을 비교하는 데 사용되는 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-163">This value is the operator that is used to compare the metric data and the threshold.</span></span> <span data-ttu-id="9a6bb-164">가능한 값은 Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual입니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-164">The possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span> |
| <span data-ttu-id="9a6bb-165">threshold</span><span class="sxs-lookup"><span data-stu-id="9a6bb-165">threshold</span></span>         | <span data-ttu-id="9a6bb-166">이 값은 크기 조정 작업을 트리거하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-166">This value is the value that triggers the scale action.</span></span> <span data-ttu-id="9a6bb-167">**규모 확장** 및 **규모 축소** 작업의 임계값 사이에 충분한 차이가 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-167">Be sure to provide a sufficient difference between the threshold values for the **scale-out** and **scale-in** actions.</span></span> <span data-ttu-id="9a6bb-168">두 작업에서 동일한 값을 설정하면 시스템은 차이가 일정하다고 예상하여 크기 조정 동작을 구현하지 못하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-168">If you set the same values for both actions, the system anticipates constant change, which prevents it from implementing a scaling action.</span></span> <span data-ttu-id="9a6bb-169">예를 들어 앞의 예제에서 두 값을 모두 스레드 600으로 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-169">For example, setting both to 600 threads in the preceding example doesn't work.</span></span> |
| <span data-ttu-id="9a6bb-170">direction</span><span class="sxs-lookup"><span data-stu-id="9a6bb-170">direction</span></span>         | <span data-ttu-id="9a6bb-171">이 값은 임계값이 달성되었을 때 수행되는 동작을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-171">This value determines the action that is taken when the threshold value is achieved.</span></span> <span data-ttu-id="9a6bb-172">가능한 값은 증가 또는 감소입니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-172">The possible values are Increase or Decrease.</span></span> |
| <span data-ttu-id="9a6bb-173">형식</span><span class="sxs-lookup"><span data-stu-id="9a6bb-173">type</span></span>              | <span data-ttu-id="9a6bb-174">이 값은 발생되어야 하는 동작의 유형이며 ChangeCount로 설정되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-174">This value is the type of action that should occur and must be set to ChangeCount.</span></span> |
| <span data-ttu-id="9a6bb-175">value</span><span class="sxs-lookup"><span data-stu-id="9a6bb-175">value</span></span>             | <span data-ttu-id="9a6bb-176">이 값은 확장 집합에서 추가되거나 제거된 가상 컴퓨터의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-176">This value is the number of virtual machines that are added to or removed from the scale set.</span></span> <span data-ttu-id="9a6bb-177">이 값은 1 이상이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-177">This value must be 1 or greater.</span></span> |
| <span data-ttu-id="9a6bb-178">cooldown</span><span class="sxs-lookup"><span data-stu-id="9a6bb-178">cooldown</span></span>          | <span data-ttu-id="9a6bb-179">이 값은 다음 작업이 발생하기 전에 마지막 크기 조정 작업 이후에 대기 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-179">This value is the amount of time to wait since the last scaling action before the next action occurs.</span></span> <span data-ttu-id="9a6bb-180">이 값은 1분에서 1주 사이여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-180">This value must be between one minute and one week.</span></span> |

<span data-ttu-id="9a6bb-181">사용하는 성능 카운터에 따라 템플릿 구성에서 일부 요소가 다르게 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-181">Depending on the performance counter, you are using, some of the elements in the template configuration are used differently.</span></span> <span data-ttu-id="9a6bb-182">다음 예제에서 성능 카운터는 Thread Count이며 규모 확장 작업에 대한 임계값은 650, 규모 축소 작업에 대한 임계값은 550입니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-182">In the preceding example, the performance counter is Thread Count, the threshold value is 650 for a scale-out action, and the threshold value is 550 for the scale-in action.</span></span> <span data-ttu-id="9a6bb-183">%Processor Time과 같은 카운터를 사용할 경우 크기 조정 작업을 판단하는 CPU 사용 백분율을 임계값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-183">If you use a counter such as %Processor Time, the threshold value is set to the percentage of CPU usage that determines a scaling action.</span></span>

<span data-ttu-id="9a6bb-184">크기 조정 작업을 트리거하는 경우 템플릿의 값을 기준으로 높은 부하와 같은 설정 용량이 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-184">When a scaling action is triggered, such as a high load, the capacity of the set is increased based on the value in the template.</span></span> <span data-ttu-id="9a6bb-185">예를 들어 용량이 3, 크기 조정 작업 값이 1로 설정된 규모 집합에서</span><span class="sxs-lookup"><span data-stu-id="9a6bb-185">For example, in a scale set where the capacity is set to 3 and the scale action value is set to 1:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerBefore.png)

<span data-ttu-id="9a6bb-186">현재 부하가 평균 스레드 수를 임계값인 650 이상으로 증가시키는 경우:</span><span class="sxs-lookup"><span data-stu-id="9a6bb-186">When the current load causes the average thread count to go above the threshold of 650:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountAfter.png)

<span data-ttu-id="9a6bb-187">집합의 용량을 1씩 증가시키는 **규모 확장** 작업을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-187">A **scale-out** action is triggered that causes the capacity of the set to be increased by one:</span></span>

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 4
},
```

<span data-ttu-id="9a6bb-188">결과적으로 확장 집합에 가상 컴퓨터가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-188">The result is a virtual machine is added to the scale set:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerAfter.png)

<span data-ttu-id="9a6bb-189">5분의 휴지 기간 후 컴퓨터의 평균 스레드 수가 600개 이상으로 유지되는 경우 집합에 다른 컴퓨터가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-189">After a cooldown period of five minutes, if the average number of threads on the machines stays over 600, another machine is added to the set.</span></span> <span data-ttu-id="9a6bb-190">평균 스레드 수가 550개 미만으로 유지되는 경우 규모 집합의 용량이 1씩 감소하며 집합에서 컴퓨터 하나가 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-190">If the average thread count stays below 550, the capacity of the scale set is reduced by one and a machine is removed from the set.</span></span>

## <a name="set-up-scaling-using-azure-powershell"></a><span data-ttu-id="9a6bb-191">Azure PowerShell을 사용하여 크기 조정 설정</span><span class="sxs-lookup"><span data-stu-id="9a6bb-191">Set up scaling using Azure PowerShell</span></span>

<span data-ttu-id="9a6bb-192">PowerShell을 사용하여 자동 크기 조정을 설정하는 예제를 보려면 [Azure Monitor PowerShell 빠른 시작 샘플](../monitoring-and-diagnostics/insights-powershell-samples.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-192">To see examples of using PowerShell to set up autoscaling, look at [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md).</span></span>

## <a name="set-up-scaling-using-azure-cli"></a><span data-ttu-id="9a6bb-193">Azure CLI를 사용하여 크기 조정 설정</span><span class="sxs-lookup"><span data-stu-id="9a6bb-193">Set up scaling using Azure CLI</span></span>

<span data-ttu-id="9a6bb-194">Azure CLI를 사용하여 자동 크기 조정을 설정하는 예제를 보려면 [Azure Monitor 플랫폼 간 CLI 빠른 시작 샘플](../monitoring-and-diagnostics/insights-cli-samples.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-194">To see examples of using Azure CLI to set up autoscaling, look at [Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md).</span></span>

## <a name="set-up-scaling-using-the-azure-portal"></a><span data-ttu-id="9a6bb-195">Azure Portal을 사용하여 크기 조정 설정</span><span class="sxs-lookup"><span data-stu-id="9a6bb-195">Set up scaling using the Azure portal</span></span>

<span data-ttu-id="9a6bb-196">Azure Portal을 사용하여 자동 크기 조정을 설정하는 예제를 보려면 [Azure Portal을 사용하여 Virtual Machine Scale Set 만들기](virtual-machine-scale-sets-portal-create.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-196">To see an example of using the Azure portal to set up autoscaling, look at [Create a Virtual Machine Scale Set using the Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

## <a name="investigate-scaling-actions"></a><span data-ttu-id="9a6bb-197">크기 조정 작업 조사</span><span class="sxs-lookup"><span data-stu-id="9a6bb-197">Investigate scaling actions</span></span>

* <span data-ttu-id="9a6bb-198">**Azure 포털**</span><span class="sxs-lookup"><span data-stu-id="9a6bb-198">**Azure portal**</span></span>  
<span data-ttu-id="9a6bb-199">포털을 사용하여 현재 제한된 양의 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-199">You can currently get a limited amount of information using the portal.</span></span>

* <span data-ttu-id="9a6bb-200">**Azure 리소스 탐색기**</span><span class="sxs-lookup"><span data-stu-id="9a6bb-200">**Azure Resource Explorer**</span></span>  
<span data-ttu-id="9a6bb-201">확장 집합의 현재 상태를 탐색하는 데 가장 적합한 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-201">This tool is the best for exploring the current state of your scale set.</span></span> <span data-ttu-id="9a6bb-202">이 경로를 따르고 사용자가 만든 규모 집합의 인스턴스 보기가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-202">Follow this path and you should see the instance view of the scale set that you created:</span></span>  
<span data-ttu-id="9a6bb-203">**구독 > {사용자 구독} > resourceGroups > {사용자 리소스 그룹} > 공급자 > Microsoft.Compute > virtualMachineScaleSets > {사용자 확장 집합} > virtualMachines**</span><span class="sxs-lookup"><span data-stu-id="9a6bb-203">**Subscriptions > {your subscription} > resourceGroups > {your resource group} > providers > Microsoft.Compute > virtualMachineScaleSets > {your scale set} > virtualMachines**</span></span>

* <span data-ttu-id="9a6bb-204">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="9a6bb-204">**Azure PowerShell**</span></span>  
<span data-ttu-id="9a6bb-205">이 명령을 사용하여 몇 가지 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-205">Use this command to get some information:</span></span>

  ```powershell
  Get-AzureRmResource -name vmsstest1 -ResourceGroupName vmsstestrg1 -ResourceType Microsoft.Compute/virtualMachineScaleSets -ApiVersion 2015-06-15
  Get-Autoscalesetting -ResourceGroup rainvmss -DetailedOutput
  ```

* <span data-ttu-id="9a6bb-206">다른 컴퓨터와 마찬가지로 jumpbox 가상 컴퓨터에 연결한 다음 개별 프로세스를 모니터링하도록 규모 집합의 가상 컴퓨터에 원격으로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-206">Connect to the jumpbox virtual machine just like you would any other machine and then you can remotely access the virtual machines in the scale set to monitor individual processes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a6bb-207">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9a6bb-207">Next Steps</span></span>
* <span data-ttu-id="9a6bb-208">구성된 자동 크기 조정을 사용하여 크기 집합을 만드는 방법에 대한 예제를 보려면 [가상 컴퓨터 크기 집합에서 자동으로 컴퓨터 크기 조정](virtual-machine-scale-sets-windows-autoscale.md) 을 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-208">Look at [Automatically scale machines in a Virtual Machine Scale Set](virtual-machine-scale-sets-windows-autoscale.md) to see an example of how to create a scale set with automatic scaling configured.</span></span>

* <span data-ttu-id="9a6bb-209">[Azure Monitor PowerShell 빠른 시작 샘플](../monitoring-and-diagnostics/insights-powershell-samples.md)에서 Azure Monitor 모니터링 기능 예제를 찾아보세요.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-209">Find examples of Azure Monitor monitoring features in [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md)</span></span>

* <span data-ttu-id="9a6bb-210">[크기 자동 조정 작업을 사용하여 Azure Monitor에서 전자 메일 및 웹후크 경고 알림 보내기](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)에서 알림 기능에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-210">Learn about notification features in [Use autoscale actions to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).</span></span>

* <span data-ttu-id="9a6bb-211">[감사 로그를 사용하여 Azure Monitor에서 전자 메일 및 웹후크 경고 알림을 보내는](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md) 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-211">Learn about how to [Use audit logs to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>

* <span data-ttu-id="9a6bb-212">[고급 자동 크기 조정 시나리오](virtual-machine-scale-sets-advanced-autoscale.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9a6bb-212">Learn about [advanced autoscale scenarios](virtual-machine-scale-sets-advanced-autoscale.md).</span></span>
