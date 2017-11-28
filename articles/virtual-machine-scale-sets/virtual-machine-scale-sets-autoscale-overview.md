---
title: "aaaAutomatic 확장 및 가상 컴퓨터 크기 집합을 조정 | Microsoft Docs"
description: "진단 및 자동 크기 조정 리소스 tooautomatically 눈금 가상 컴퓨터 크기 집합의 사용에 대 한 알아봅니다."
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
ms.openlocfilehash: 25f54b693e3c991577238242008c262023ed479c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-automatic-scaling-and-virtual-machine-scale-sets"></a><span data-ttu-id="5fd08-103">어떻게 toouse 자동 크기 조정 및 가상 컴퓨터 크기 집합</span><span class="sxs-lookup"><span data-stu-id="5fd08-103">How toouse automatic scaling and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="5fd08-104">크기 집합의 가상 컴퓨터의 자동 크기 조정 작업은 hello 만들기 또는 삭제로 설정 하는 hello에 있는 컴퓨터의 필요한 toomatch 성능 요구 사항</span><span class="sxs-lookup"><span data-stu-id="5fd08-104">Automatic scaling of virtual machines in a scale set is hello creation or deletion of machines in hello set as needed toomatch performance requirements.</span></span> <span data-ttu-id="5fd08-105">응용 프로그램에 추가 리소스 tooenable 필요할 수 있습니다 hello 볼륨의 작업까지 확장 되면서 것 tooeffectively 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-105">As hello volume of work grows, an application may require additional resources tooenable it tooeffectively perform tasks.</span></span>

<span data-ttu-id="5fd08-106">자동 크기 조정은 관리 오버헤드를 줄이기 위해 자동화된 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-106">Automatic scaling is an automated process that helps ease management overhead.</span></span> <span data-ttu-id="5fd08-107">오버 헤드 줄이기 여 toocontinually 시스템 성능 모니터 필요 하거나 결정 하지 않는 방법을 toomanage 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-107">By reducing overhead, you don't need toocontinually monitor system performance or decide how toomanage resources.</span></span> <span data-ttu-id="5fd08-108">크기 조정은 탄력적인 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-108">Scaling is an elastic process.</span></span> <span data-ttu-id="5fd08-109">Hello 부하 증가 함에 따라 더 많은 리소스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-109">More resources can be added as hello load increases.</span></span> <span data-ttu-id="5fd08-110">있고 요청 감소도 리소스 제거 toominimize 비용 및 수 성능 수준을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-110">And as demand decreases, resources can be removed toominimize costs and maintain performance levels.</span></span>

<span data-ttu-id="5fd08-111">Azure 리소스 관리자 템플릿, Azure PowerShell, Azure CLI 또는 hello Azure 포털을 사용 하 여 설정 설명에 자동 크기 조정 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-111">Set up automatic scaling on a scale set by using an Azure Resource Manager template, Azure PowerShell, Azure CLI, or hello Azure portal.</span></span>

## <a name="set-up-scaling-by-using-resource-manager-templates"></a><span data-ttu-id="5fd08-112">리소스 관리자 템플릿을 사용하여 크기 조정 설정</span><span class="sxs-lookup"><span data-stu-id="5fd08-112">Set up scaling by using Resource Manager templates</span></span>
<span data-ttu-id="5fd08-113">각 응용 프로그램의 리소스를 개별적으로 배포하고 관리하는 대신, 모든 리소스를 하나의 조정된 작업으로 배포하는 템플릿을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-113">Rather than deploying and managing each resource of your application separately, use a template that deploys all resources in a single, coordinated operation.</span></span> <span data-ttu-id="5fd08-114">Hello 서식 파일에서 응용 프로그램 리소스 정의 되 고 다른 환경에 대해 배포 매개 변수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-114">In hello template, application resources are defined and deployment parameters are specified for different environments.</span></span> <span data-ttu-id="5fd08-115">JSON 및 배포에 대 한 tooconstruct 값을 사용할 수 있는 식의 hello 템플릿은 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-115">hello template consists of JSON and expressions that you can use tooconstruct values for your deployment.</span></span> <span data-ttu-id="5fd08-116">확인을 toolearn [제작 Azure 리소스 관리자 템플릿을](../azure-resource-manager/resource-group-authoring-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-116">toolearn more, look at [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="5fd08-117">Hello 템플릿 hello 용량 요소를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-117">In hello template, you specify hello capacity element:</span></span>

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 3
},
```

<span data-ttu-id="5fd08-118">용량은 hello 집합의 가상 컴퓨터의 hello 번호를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-118">Capacity identifies hello number of virtual machines in hello set.</span></span> <span data-ttu-id="5fd08-119">다른 값으로 서식 파일을 배포 하 여 hello 용량을 수동으로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-119">You can manually change hello capacity by deploying a template with a different value.</span></span> <span data-ttu-id="5fd08-120">템플릿 tooonly 변경 hello 용량을 배포 하는 경우 업데이트 하는 hello 용량으로 hello SKU 요소만을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-120">If you are deploying a template tooonly change hello capacity, you can include only hello SKU element with hello updated capacity.</span></span>

<span data-ttu-id="5fd08-121">hello 용량 크기 집합의 수 자동으로 조정 되도록 hello의 조합을 사용 하 여 **autoscaleSettings** 진단 확장을 리소스 및 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-121">hello capacity of your scale set can be automatically adjusted by using a combination of hello **autoscaleSettings** resource and hello diagnostics extension.</span></span>

### <a name="configure-hello-azure-diagnostics-extension"></a><span data-ttu-id="5fd08-122">Hello Azure 진단 확장 구성</span><span class="sxs-lookup"><span data-stu-id="5fd08-122">Configure hello Azure Diagnostics extension</span></span>
<span data-ttu-id="5fd08-123">자동 크기 조정에 수행할 수 메트릭 컬렉션 hello 크기 집합의 각 가상 컴퓨터에 성공한 경우.</span><span class="sxs-lookup"><span data-stu-id="5fd08-123">Automatic scaling can only be done if metrics collection is successful on each virtual machine in hello scale set.</span></span> <span data-ttu-id="5fd08-124">Azure 진단 확장 hello hello 자동 크기 조정 리소스의 hello 메트릭 컬렉션 요구 사항을 충족 하는 hello 모니터링 및 진단 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-124">hello Azure Diagnostics Extension provides hello monitoring and diagnostics capabilities that meets hello metrics collection needs of hello autoscale resource.</span></span> <span data-ttu-id="5fd08-125">Hello 리소스 관리자 서식 파일의 일부로 hello 확장을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-125">You can install hello extension as part of hello Resource Manager template.</span></span>

<span data-ttu-id="5fd08-126">이 예제에서는 hello 템플릿 tooconfigure hello 진단 확장에서 사용 되는 hello 변수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-126">This example shows hello variables that are used in hello template tooconfigure hello diagnostics extension:</span></span>

```json
"diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'saa')]",
"accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/', 'Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
"wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
"wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Thread Count\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
"wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
"wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
"wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
```

<span data-ttu-id="5fd08-127">매개 변수는 hello 템플릿이 배포 될 때 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-127">Parameters are provided when hello template is deployed.</span></span> <span data-ttu-id="5fd08-128">이 예에서 hello hello 저장소 계정의 이름입니다 (데이터 저장 됨)와 hello hello 크기 집합 (데이터를 수집 하는 위치)의 이름이 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-128">In this example, hello name of hello storage account (where data is stored) and hello name of hello scale set (where data is collected) are provided.</span></span> <span data-ttu-id="5fd08-129">또한이 Windows Server 예에서 hello Thread Count 성능 카운터에만 수집 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-129">Also in this Windows Server example, only hello Thread Count performance counter is collected.</span></span> <span data-ttu-id="5fd08-130">모든 Windows에서 사용 가능한 성능 카운터를 hello 또는 Linux 진단 정보를 사용 하는 toocollect 수 있습니다 hello 확장 구성에 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-130">All hello available performance counters in Windows or Linux can be used toocollect diagnostics information and can be included in hello extension configuration.</span></span>

<span data-ttu-id="5fd08-131">이 예제에서는 hello 템플릿에서 hello 확장의 hello 정을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-131">This example shows hello definition of hello extension in hello template:</span></span>

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

<span data-ttu-id="5fd08-132">Hello 진단 확장 실행 되 면 hello 데이터가 저장 되 고 지정 하는 hello 저장소 계정에는 테이블에 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-132">When hello diagnostics extension runs, hello data is stored and collected in a table, in hello storage account that you specify.</span></span> <span data-ttu-id="5fd08-133">Hello에 **WADPerformanceCounters** 테이블 hello 수집 된 데이터를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-133">In hello **WADPerformanceCounters** table, you can find hello collected data:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountBefore2.png)

### <a name="configure-hello-autoscalesettings-resource"></a><span data-ttu-id="5fd08-134">Hello autoScaleSettings 리소스 구성</span><span class="sxs-lookup"><span data-stu-id="5fd08-134">Configure hello autoScaleSettings resource</span></span>
<span data-ttu-id="5fd08-135">hello autoscaleSettings 리소스 tooincrease 또는 감소 hello 번호 hello 규모에 맞게 가상 컴퓨터의 설정 여부를 나타내는 hello 진단 확장 toodecide에서 hello 정보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-135">hello autoscaleSettings resource uses hello information from hello diagnostics extension toodecide whether tooincrease or decrease hello number of virtual machines in hello scale set.</span></span>

<span data-ttu-id="5fd08-136">이 예제에는 hello 서식 파일의 hello 리소스의 hello 구성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-136">This example shows hello configuration of hello resource in hello template:</span></span>

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

<span data-ttu-id="5fd08-137">Hello 위의 예에서 hello 자동 크기 조정 작업을 정의 하기 위한 두 개의 규칙이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-137">In hello example above, two rules are created for defining hello automatic scaling actions.</span></span> <span data-ttu-id="5fd08-138">첫 번째 규칙의 hello hello 확장 작업을 정의 하 고 두 번째 규칙의 hello hello에 대 한 크기 조정 작업을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-138">hello first rule defines hello scale-out action and hello second rule defines hello scale-in action.</span></span> <span data-ttu-id="5fd08-139">이러한 값은 hello 규칙에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-139">These values are provided in hello rules:</span></span>

| <span data-ttu-id="5fd08-140">규칙</span><span class="sxs-lookup"><span data-stu-id="5fd08-140">Rule</span></span> | <span data-ttu-id="5fd08-141">설명</span><span class="sxs-lookup"><span data-stu-id="5fd08-141">Description</span></span> |
| ---- | ----------- |
| <span data-ttu-id="5fd08-142">metricName</span><span class="sxs-lookup"><span data-stu-id="5fd08-142">metricName</span></span>        | <span data-ttu-id="5fd08-143">이 값 hello 진단 확장에 대 한 hello wadperfcounter 변수에 정의 된 hello 성능 카운터로 동일한 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-143">This value is hello same as hello performance counter that you defined in hello wadperfcounter variable for hello diagnostics extension.</span></span> <span data-ttu-id="5fd08-144">위의 hello 예제 hello 스레드 수가 카운터 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-144">In hello example above, hello Thread Count counter is used.</span></span>    |
| <span data-ttu-id="5fd08-145">metricResourceUri</span><span class="sxs-lookup"><span data-stu-id="5fd08-145">metricResourceUri</span></span> | <span data-ttu-id="5fd08-146">이 값은 hello 가상 컴퓨터 크기 집합의 hello 리소스 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-146">This value is hello resource identifier of hello virtual machine scale set.</span></span> <span data-ttu-id="5fd08-147">이 식별자는 hello 리소스 그룹의 이름을 hello, hello hello 리소스 공급자의 이름과 이름 hello hello 눈금 집합 tooscale 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-147">This identifier contains hello name of hello resource group, hello name of hello resource provider, and hello name of hello scale set tooscale.</span></span> |
| <span data-ttu-id="5fd08-148">timeGrain</span><span class="sxs-lookup"><span data-stu-id="5fd08-148">timeGrain</span></span>         | <span data-ttu-id="5fd08-149">이 값은 hello 메트릭을 수집 하는 hello 세분성입니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-149">This value is hello granularity of hello metrics that are collected.</span></span> <span data-ttu-id="5fd08-150">앞 예제는 hello, 1 분 간격으로 데이터를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-150">In hello preceding example, data is collected on an interval of one minute.</span></span> <span data-ttu-id="5fd08-151">이 값은 timeWindow와 함께 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-151">This value is used with timeWindow.</span></span> |
| <span data-ttu-id="5fd08-152">statistic</span><span class="sxs-lookup"><span data-stu-id="5fd08-152">statistic</span></span>         | <span data-ttu-id="5fd08-153">이 값 hello 메트릭은 결합된 tooaccommodate hello 자동 작업 크기 조정 방법을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-153">This value determines how hello metrics are combined tooaccommodate hello automatic scaling action.</span></span> <span data-ttu-id="5fd08-154">hello 가능한 값은: 평균, 최소값, 최대값입니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-154">hello possible values are: Average, Min, Max.</span></span> |
| <span data-ttu-id="5fd08-155">timeWindow</span><span class="sxs-lookup"><span data-stu-id="5fd08-155">timeWindow</span></span>        | <span data-ttu-id="5fd08-156">이 값은 hello 인스턴스 데이터를 수집 하는 시간 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-156">This value is hello range of time in which instance data is collected.</span></span> <span data-ttu-id="5fd08-157">5분에서 12시간 사이여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-157">It must be between 5 minutes and 12 hours.</span></span> |
| <span data-ttu-id="5fd08-158">timeAggregation</span><span class="sxs-lookup"><span data-stu-id="5fd08-158">timeAggregation</span></span>   | <span data-ttu-id="5fd08-159">이 값은 시간이 지남에 따라 수집 되는 hello 데이터를 결합 하는 방법을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-159">This value determines how hello data that is collected should be combined over time.</span></span> <span data-ttu-id="5fd08-160">hello 기본값은 평균입니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-160">hello default value is Average.</span></span> <span data-ttu-id="5fd08-161">hello 가능한 값은: 평균, 최소값, 최대값, 마지막, 합계, 개수입니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-161">hello possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span> |
| <span data-ttu-id="5fd08-162">operator</span><span class="sxs-lookup"><span data-stu-id="5fd08-162">operator</span></span>          | <span data-ttu-id="5fd08-163">이 값은 hello 연산자가 사용 되는 toocompare hello 메트릭 데이터와 hello 임계값입니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-163">This value is hello operator that is used toocompare hello metric data and hello threshold.</span></span> <span data-ttu-id="5fd08-164">hello 가능한 값은: Equals, NotEquals, 보다 큼, GreaterThanOrEqual, LessThan, LessThanOrEqual 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-164">hello possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span> |
| <span data-ttu-id="5fd08-165">threshold</span><span class="sxs-lookup"><span data-stu-id="5fd08-165">threshold</span></span>         | <span data-ttu-id="5fd08-166">이 값은 hello 크기 조정 작업을 트리거하는 hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-166">This value is hello value that triggers hello scale action.</span></span> <span data-ttu-id="5fd08-167">Hello에 대 한 hello 임계값 사이의 충분 한 차이가 있는지 tooprovide 될 **확장** 및 **눈금에서** 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-167">Be sure tooprovide a sufficient difference between hello threshold values for hello **scale-out** and **scale-in** actions.</span></span> <span data-ttu-id="5fd08-168">Hello 두 가지 동작 모두에 대해 같은 값으로 설정 하면 hello 시스템 예상 크기 조정 동작을 구현 하지 못하게 하는 상수 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-168">If you set hello same values for both actions, hello system anticipates constant change, which prevents it from implementing a scaling action.</span></span> <span data-ttu-id="5fd08-169">예를 들어 hello 예에서는 앞의 두 too600 스레드 설정 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-169">For example, setting both too600 threads in hello preceding example doesn't work.</span></span> |
| <span data-ttu-id="5fd08-170">direction</span><span class="sxs-lookup"><span data-stu-id="5fd08-170">direction</span></span>         | <span data-ttu-id="5fd08-171">이 값은 hello 임계값이 작업을 수행 하는 경우 수행 하는 hello 동작을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-171">This value determines hello action that is taken when hello threshold value is achieved.</span></span> <span data-ttu-id="5fd08-172">hello 가능한 값은 증가 또는 감소 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-172">hello possible values are Increase or Decrease.</span></span> |
| <span data-ttu-id="5fd08-173">type</span><span class="sxs-lookup"><span data-stu-id="5fd08-173">type</span></span>              | <span data-ttu-id="5fd08-174">이 값은 hello 유형의 동작을 발생 해야 하며 tooChangeCount 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-174">This value is hello type of action that should occur and must be set tooChangeCount.</span></span> |
| <span data-ttu-id="5fd08-175">값</span><span class="sxs-lookup"><span data-stu-id="5fd08-175">value</span></span>             | <span data-ttu-id="5fd08-176">이 값은 추가 tooor hello 크기 집합에서 제거 된 가상 컴퓨터의 hello 수입니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-176">This value is hello number of virtual machines that are added tooor removed from hello scale set.</span></span> <span data-ttu-id="5fd08-177">이 값은 1 이상이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-177">This value must be 1 or greater.</span></span> |
| <span data-ttu-id="5fd08-178">cooldown</span><span class="sxs-lookup"><span data-stu-id="5fd08-178">cooldown</span></span>          | <span data-ttu-id="5fd08-179">이 값은 hello 시간 toowait hello 마지막 크기 조정 작업 이후 hello 다음 작업이 발생 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="5fd08-179">This value is hello amount of time toowait since hello last scaling action before hello next action occurs.</span></span> <span data-ttu-id="5fd08-180">이 값은 1분에서 1주 사이여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-180">This value must be between one minute and one week.</span></span> |

<span data-ttu-id="5fd08-181">Hello 성능 카운터에 따라 사용 중이거나, hello hello 템플릿 구성 요소 중 일부가 다르게 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-181">Depending on hello performance counter, you are using, some of hello elements in hello template configuration are used differently.</span></span> <span data-ttu-id="5fd08-182">앞 예제는 hello, hello 성능 카운터는 스레드 수, hello 임계값은 확장 작업에 대 한 650 및 hello 임계값은 550 hello에 대 한 크기 조정 작업에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-182">In hello preceding example, hello performance counter is Thread Count, hello threshold value is 650 for a scale-out action, and hello threshold value is 550 for hello scale-in action.</span></span> <span data-ttu-id="5fd08-183">예: % Processor Time 카운터를 사용 하는 경우 hello 임계값 크기 조정 작업을 결정 하는 CPU 사용량의 toohello 비율을 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-183">If you use a counter such as %Processor Time, hello threshold value is set toohello percentage of CPU usage that determines a scaling action.</span></span>

<span data-ttu-id="5fd08-184">높은 로드와 같은 크기 조정 작업을 트리거할 때 hello 집합의 hello 용량이 hello 템플릿에서 hello 값에 따라 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-184">When a scaling action is triggered, such as a high load, hello capacity of hello set is increased based on hello value in hello template.</span></span> <span data-ttu-id="5fd08-185">예를 들어 눈금의 여기서 hello 용량 too3 설정 하 고 hello 크기 조정 값 too1 설정 되어를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-185">For example, in a scale set where hello capacity is set too3 and hello scale action value is set too1:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerBefore.png)

<span data-ttu-id="5fd08-186">현재 부하 원인을 hello 평균 스레드 개수 toogo 650의 hello 임계값 보다 큰 경우 hello:</span><span class="sxs-lookup"><span data-stu-id="5fd08-186">When hello current load causes hello average thread count toogo above hello threshold of 650:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountAfter.png)

<span data-ttu-id="5fd08-187">A **확장** 원인을 hello 1 씩 증가 하는 hello 집합 toobe의 용량을 뜻합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-187">A **scale-out** action is triggered that causes hello capacity of hello set toobe increased by one:</span></span>

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 4
},
```

<span data-ttu-id="5fd08-188">hello 결과 가상 컴퓨터 크기 집합 toohello 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-188">hello result is a virtual machine is added toohello scale set:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerAfter.png)

<span data-ttu-id="5fd08-189">5 분의 쿨 다운 시간 hello 평균 hello 컴퓨터에는 스레드 수 유지 600 개 다른 컴퓨터를 추가한 toohello 집합.</span><span class="sxs-lookup"><span data-stu-id="5fd08-189">After a cooldown period of five minutes, if hello average number of threads on hello machines stays over 600, another machine is added toohello set.</span></span> <span data-ttu-id="5fd08-190">Hello 평균 스레드 수 유지 550 아래, hello 용량의 hello 크기 집합은 1 씩 감소 하 고 컴퓨터를 hello 집합에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-190">If hello average thread count stays below 550, hello capacity of hello scale set is reduced by one and a machine is removed from hello set.</span></span>

## <a name="set-up-scaling-using-azure-powershell"></a><span data-ttu-id="5fd08-191">Azure PowerShell을 사용하여 크기 조정 설정</span><span class="sxs-lookup"><span data-stu-id="5fd08-191">Set up scaling using Azure PowerShell</span></span>

<span data-ttu-id="5fd08-192">자동 크기 조정, 구성 PowerShell tooset를 사용 하는 예제 toosee 확인 [Azure 모니터 PowerShell 빠른 시작 예제](../monitoring-and-diagnostics/insights-powershell-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-192">toosee examples of using PowerShell tooset up autoscaling, look at [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md).</span></span>

## <a name="set-up-scaling-using-azure-cli"></a><span data-ttu-id="5fd08-193">Azure CLI를 사용하여 크기 조정 설정</span><span class="sxs-lookup"><span data-stu-id="5fd08-193">Set up scaling using Azure CLI</span></span>

<span data-ttu-id="5fd08-194">자동 크기 조정, 구성 tooset Azure CLI를 사용 하는 예제 toosee 확인 [Azure 모니터 플랫폼 간 CLI 빠른 시작 예제](../monitoring-and-diagnostics/insights-cli-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-194">toosee examples of using Azure CLI tooset up autoscaling, look at [Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md).</span></span>

## <a name="set-up-scaling-using-hello-azure-portal"></a><span data-ttu-id="5fd08-195">Hello Azure 포털을 사용 하 여 크기 조정 설정</span><span class="sxs-lookup"><span data-stu-id="5fd08-195">Set up scaling using hello Azure portal</span></span>

<span data-ttu-id="5fd08-196">사용 하는 예제 toosee hello 자동 크기 조정, 구성 하는 Azure 포털 tooset 조회에서 [hello Azure 포털을 사용 하 여 가상 컴퓨터 크기 집합을 만들](virtual-machine-scale-sets-portal-create.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-196">toosee an example of using hello Azure portal tooset up autoscaling, look at [Create a Virtual Machine Scale Set using hello Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

## <a name="investigate-scaling-actions"></a><span data-ttu-id="5fd08-197">크기 조정 작업 조사</span><span class="sxs-lookup"><span data-stu-id="5fd08-197">Investigate scaling actions</span></span>

* <span data-ttu-id="5fd08-198">**Azure 포털**</span><span class="sxs-lookup"><span data-stu-id="5fd08-198">**Azure portal**</span></span>  
<span data-ttu-id="5fd08-199">현재 제한 된 양의 hello 포털을 사용 하 여 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-199">You can currently get a limited amount of information using hello portal.</span></span>

* <span data-ttu-id="5fd08-200">**Azure 리소스 탐색기**</span><span class="sxs-lookup"><span data-stu-id="5fd08-200">**Azure Resource Explorer**</span></span>  
<span data-ttu-id="5fd08-201">이 도구는 hello hello 크기 집합의 현재 상태를 조사 하기 위한 최상의입니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-201">This tool is hello best for exploring hello current state of your scale set.</span></span> <span data-ttu-id="5fd08-202">이 경로 따라 하 고 hello 눈금의 hello 인스턴스 보기 설정 하 여 만든 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-202">Follow this path and you should see hello instance view of hello scale set that you created:</span></span>  
<span data-ttu-id="5fd08-203">**구독 > {사용자 구독} > resourceGroups > {사용자 리소스 그룹} > 공급자 > Microsoft.Compute > virtualMachineScaleSets > {사용자 확장 집합} > virtualMachines**</span><span class="sxs-lookup"><span data-stu-id="5fd08-203">**Subscriptions > {your subscription} > resourceGroups > {your resource group} > providers > Microsoft.Compute > virtualMachineScaleSets > {your scale set} > virtualMachines**</span></span>

* <span data-ttu-id="5fd08-204">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="5fd08-204">**Azure PowerShell**</span></span>  
<span data-ttu-id="5fd08-205">이 명령은 tooget 몇 가지 정보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-205">Use this command tooget some information:</span></span>

  ```powershell
  Get-AzureRmResource -name vmsstest1 -ResourceGroupName vmsstestrg1 -ResourceType Microsoft.Compute/virtualMachineScaleSets -ApiVersion 2015-06-15
  Get-Autoscalesetting -ResourceGroup rainvmss -DetailedOutput
  ```

* <span data-ttu-id="5fd08-206">Hello 눈금 집합 toomonitor 개별 프로세스에 hello 가상 컴퓨터에 원격으로 액세스할 수 있습니다 및 다른 컴퓨터는 것 처럼 toohello jumpbox 가상 컴퓨터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-206">Connect toohello jumpbox virtual machine just like you would any other machine and then you can remotely access hello virtual machines in hello scale set toomonitor individual processes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5fd08-207">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5fd08-207">Next Steps</span></span>
* <span data-ttu-id="5fd08-208">살펴보고 [가상 컴퓨터 크기 집합의 컴퓨터 크기를 자동으로 조정](virtual-machine-scale-sets-windows-autoscale.md) toosee toocreate 배율 설정 방법으로 구성 된 자동 크기 조정의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-208">Look at [Automatically scale machines in a Virtual Machine Scale Set](virtual-machine-scale-sets-windows-autoscale.md) toosee an example of how toocreate a scale set with automatic scaling configured.</span></span>

* <span data-ttu-id="5fd08-209">[Azure Monitor PowerShell 빠른 시작 샘플](../monitoring-and-diagnostics/insights-powershell-samples.md)에서 Azure Monitor 모니터링 기능 예제를 찾아보세요.</span><span class="sxs-lookup"><span data-stu-id="5fd08-209">Find examples of Azure Monitor monitoring features in [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md)</span></span>

* <span data-ttu-id="5fd08-210">알림 기능에 대 한 자세한 내용은 [Azure 모니터에서 자동 크기 조정 작업 toosend 전자 메일 및 webhook 경고 알림을 사용 하 여](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-210">Learn about notification features in [Use autoscale actions toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).</span></span>

* <span data-ttu-id="5fd08-211">너무 방법에 대 한 자세한 내용은[Azure 모니터에서 사용 하 여 감사 로그를 toosend webhook 및 전자 메일 경고 알림](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="5fd08-211">Learn about how too[Use audit logs toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>

* <span data-ttu-id="5fd08-212">[고급 자동 크기 조정 시나리오](virtual-machine-scale-sets-advanced-autoscale.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5fd08-212">Learn about [advanced autoscale scenarios](virtual-machine-scale-sets-advanced-autoscale.md).</span></span>
