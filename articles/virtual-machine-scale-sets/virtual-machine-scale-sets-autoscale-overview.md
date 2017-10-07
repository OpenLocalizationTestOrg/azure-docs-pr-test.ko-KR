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
# <a name="how-toouse-automatic-scaling-and-virtual-machine-scale-sets"></a>어떻게 toouse 자동 크기 조정 및 가상 컴퓨터 크기 집합
크기 집합의 가상 컴퓨터의 자동 크기 조정 작업은 hello 만들기 또는 삭제로 설정 하는 hello에 있는 컴퓨터의 필요한 toomatch 성능 요구 사항 응용 프로그램에 추가 리소스 tooenable 필요할 수 있습니다 hello 볼륨의 작업까지 확장 되면서 것 tooeffectively 작업을 수행 합니다.

자동 크기 조정은 관리 오버헤드를 줄이기 위해 자동화된 프로세스입니다. 오버 헤드 줄이기 여 toocontinually 시스템 성능 모니터 필요 하거나 결정 하지 않는 방법을 toomanage 리소스입니다. 크기 조정은 탄력적인 프로세스입니다. Hello 부하 증가 함에 따라 더 많은 리소스를 추가할 수 있습니다. 있고 요청 감소도 리소스 제거 toominimize 비용 및 수 성능 수준을 유지 합니다.

Azure 리소스 관리자 템플릿, Azure PowerShell, Azure CLI 또는 hello Azure 포털을 사용 하 여 설정 설명에 자동 크기 조정 설정 합니다.

## <a name="set-up-scaling-by-using-resource-manager-templates"></a>리소스 관리자 템플릿을 사용하여 크기 조정 설정
각 응용 프로그램의 리소스를 개별적으로 배포하고 관리하는 대신, 모든 리소스를 하나의 조정된 작업으로 배포하는 템플릿을 사용합니다. Hello 서식 파일에서 응용 프로그램 리소스 정의 되 고 다른 환경에 대해 배포 매개 변수를 지정 합니다. JSON 및 배포에 대 한 tooconstruct 값을 사용할 수 있는 식의 hello 템플릿은 구성 됩니다. 확인을 toolearn [제작 Azure 리소스 관리자 템플릿을](../azure-resource-manager/resource-group-authoring-templates.md)합니다.

Hello 템플릿 hello 용량 요소를 지정 합니다.

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 3
},
```

용량은 hello 집합의 가상 컴퓨터의 hello 번호를 식별합니다. 다른 값으로 서식 파일을 배포 하 여 hello 용량을 수동으로 변경할 수 있습니다. 템플릿 tooonly 변경 hello 용량을 배포 하는 경우 업데이트 하는 hello 용량으로 hello SKU 요소만을 포함할 수 있습니다.

hello 용량 크기 집합의 수 자동으로 조정 되도록 hello의 조합을 사용 하 여 **autoscaleSettings** 진단 확장을 리소스 및 hello 합니다.

### <a name="configure-hello-azure-diagnostics-extension"></a>Hello Azure 진단 확장 구성
자동 크기 조정에 수행할 수 메트릭 컬렉션 hello 크기 집합의 각 가상 컴퓨터에 성공한 경우. Azure 진단 확장 hello hello 자동 크기 조정 리소스의 hello 메트릭 컬렉션 요구 사항을 충족 하는 hello 모니터링 및 진단 기능을 제공 합니다. Hello 리소스 관리자 서식 파일의 일부로 hello 확장을 설치할 수 있습니다.

이 예제에서는 hello 템플릿 tooconfigure hello 진단 확장에서 사용 되는 hello 변수를 보여 줍니다.

```json
"diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'saa')]",
"accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/', 'Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
"wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
"wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Thread Count\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
"wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
"wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
"wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
```

매개 변수는 hello 템플릿이 배포 될 때 제공 됩니다. 이 예에서 hello hello 저장소 계정의 이름입니다 (데이터 저장 됨)와 hello hello 크기 집합 (데이터를 수집 하는 위치)의 이름이 제공 됩니다. 또한이 Windows Server 예에서 hello Thread Count 성능 카운터에만 수집 됩니다. 모든 Windows에서 사용 가능한 성능 카운터를 hello 또는 Linux 진단 정보를 사용 하는 toocollect 수 있습니다 hello 확장 구성에 포함 될 수 있습니다.

이 예제에서는 hello 템플릿에서 hello 확장의 hello 정을 보여 줍니다.

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

Hello 진단 확장 실행 되 면 hello 데이터가 저장 되 고 지정 하는 hello 저장소 계정에는 테이블에 수집 합니다. Hello에 **WADPerformanceCounters** 테이블 hello 수집 된 데이터를 찾을 수 있습니다.

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountBefore2.png)

### <a name="configure-hello-autoscalesettings-resource"></a>Hello autoScaleSettings 리소스 구성
hello autoscaleSettings 리소스 tooincrease 또는 감소 hello 번호 hello 규모에 맞게 가상 컴퓨터의 설정 여부를 나타내는 hello 진단 확장 toodecide에서 hello 정보를 사용 합니다.

이 예제에는 hello 서식 파일의 hello 리소스의 hello 구성을 보여 줍니다.

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

Hello 위의 예에서 hello 자동 크기 조정 작업을 정의 하기 위한 두 개의 규칙이 만들어집니다. 첫 번째 규칙의 hello hello 확장 작업을 정의 하 고 두 번째 규칙의 hello hello에 대 한 크기 조정 작업을 정의 합니다. 이러한 값은 hello 규칙에서 제공 됩니다.

| 규칙 | 설명 |
| ---- | ----------- |
| metricName        | 이 값 hello 진단 확장에 대 한 hello wadperfcounter 변수에 정의 된 hello 성능 카운터로 동일한 hello 됩니다. 위의 hello 예제 hello 스레드 수가 카운터 사용 됩니다.    |
| metricResourceUri | 이 값은 hello 가상 컴퓨터 크기 집합의 hello 리소스 식별자입니다. 이 식별자는 hello 리소스 그룹의 이름을 hello, hello hello 리소스 공급자의 이름과 이름 hello hello 눈금 집합 tooscale 포함 되어 있습니다. |
| timeGrain         | 이 값은 hello 메트릭을 수집 하는 hello 세분성입니다. 앞 예제는 hello, 1 분 간격으로 데이터를 수집 합니다. 이 값은 timeWindow와 함께 사용됩니다. |
| statistic         | 이 값 hello 메트릭은 결합된 tooaccommodate hello 자동 작업 크기 조정 방법을 결정 합니다. hello 가능한 값은: 평균, 최소값, 최대값입니다. |
| timeWindow        | 이 값은 hello 인스턴스 데이터를 수집 하는 시간 범위입니다. 5분에서 12시간 사이여야 합니다. |
| timeAggregation   | 이 값은 시간이 지남에 따라 수집 되는 hello 데이터를 결합 하는 방법을 결정 합니다. hello 기본값은 평균입니다. hello 가능한 값은: 평균, 최소값, 최대값, 마지막, 합계, 개수입니다. |
| operator          | 이 값은 hello 연산자가 사용 되는 toocompare hello 메트릭 데이터와 hello 임계값입니다. hello 가능한 값은: Equals, NotEquals, 보다 큼, GreaterThanOrEqual, LessThan, LessThanOrEqual 합니다. |
| threshold         | 이 값은 hello 크기 조정 작업을 트리거하는 hello 값입니다. Hello에 대 한 hello 임계값 사이의 충분 한 차이가 있는지 tooprovide 될 **확장** 및 **눈금에서** 동작 합니다. Hello 두 가지 동작 모두에 대해 같은 값으로 설정 하면 hello 시스템 예상 크기 조정 동작을 구현 하지 못하게 하는 상수 변경 합니다. 예를 들어 hello 예에서는 앞의 두 too600 스레드 설정 작동 하지 않습니다. |
| direction         | 이 값은 hello 임계값이 작업을 수행 하는 경우 수행 하는 hello 동작을 결정 합니다. hello 가능한 값은 증가 또는 감소 합니다. |
| type              | 이 값은 hello 유형의 동작을 발생 해야 하며 tooChangeCount 설정 해야 합니다. |
| 값             | 이 값은 추가 tooor hello 크기 집합에서 제거 된 가상 컴퓨터의 hello 수입니다. 이 값은 1 이상이어야 합니다. |
| cooldown          | 이 값은 hello 시간 toowait hello 마지막 크기 조정 작업 이후 hello 다음 작업이 발생 하기 전에. 이 값은 1분에서 1주 사이여야 합니다. |

Hello 성능 카운터에 따라 사용 중이거나, hello hello 템플릿 구성 요소 중 일부가 다르게 사용 됩니다. 앞 예제는 hello, hello 성능 카운터는 스레드 수, hello 임계값은 확장 작업에 대 한 650 및 hello 임계값은 550 hello에 대 한 크기 조정 작업에 대 한 합니다. 예: % Processor Time 카운터를 사용 하는 경우 hello 임계값 크기 조정 작업을 결정 하는 CPU 사용량의 toohello 비율을 설정 됩니다.

높은 로드와 같은 크기 조정 작업을 트리거할 때 hello 집합의 hello 용량이 hello 템플릿에서 hello 값에 따라 증가 합니다. 예를 들어 눈금의 여기서 hello 용량 too3 설정 하 고 hello 크기 조정 값 too1 설정 되어를 설정 합니다.

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerBefore.png)

현재 부하 원인을 hello 평균 스레드 개수 toogo 650의 hello 임계값 보다 큰 경우 hello:

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountAfter.png)

A **확장** 원인을 hello 1 씩 증가 하는 hello 집합 toobe의 용량을 뜻합니다.

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 4
},
```

hello 결과 가상 컴퓨터 크기 집합 toohello 추가 됩니다.

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerAfter.png)

5 분의 쿨 다운 시간 hello 평균 hello 컴퓨터에는 스레드 수 유지 600 개 다른 컴퓨터를 추가한 toohello 집합. Hello 평균 스레드 수 유지 550 아래, hello 용량의 hello 크기 집합은 1 씩 감소 하 고 컴퓨터를 hello 집합에서 제거 됩니다.

## <a name="set-up-scaling-using-azure-powershell"></a>Azure PowerShell을 사용하여 크기 조정 설정

자동 크기 조정, 구성 PowerShell tooset를 사용 하는 예제 toosee 확인 [Azure 모니터 PowerShell 빠른 시작 예제](../monitoring-and-diagnostics/insights-powershell-samples.md)합니다.

## <a name="set-up-scaling-using-azure-cli"></a>Azure CLI를 사용하여 크기 조정 설정

자동 크기 조정, 구성 tooset Azure CLI를 사용 하는 예제 toosee 확인 [Azure 모니터 플랫폼 간 CLI 빠른 시작 예제](../monitoring-and-diagnostics/insights-cli-samples.md)합니다.

## <a name="set-up-scaling-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 크기 조정 설정

사용 하는 예제 toosee hello 자동 크기 조정, 구성 하는 Azure 포털 tooset 조회에서 [hello Azure 포털을 사용 하 여 가상 컴퓨터 크기 집합을 만들](virtual-machine-scale-sets-portal-create.md)합니다.

## <a name="investigate-scaling-actions"></a>크기 조정 작업 조사

* **Azure 포털**  
현재 제한 된 양의 hello 포털을 사용 하 여 정보를 얻을 수 있습니다.

* **Azure 리소스 탐색기**  
이 도구는 hello hello 크기 집합의 현재 상태를 조사 하기 위한 최상의입니다. 이 경로 따라 하 고 hello 눈금의 hello 인스턴스 보기 설정 하 여 만든 표시 되어야 합니다.  
**구독 > {사용자 구독} > resourceGroups > {사용자 리소스 그룹} > 공급자 > Microsoft.Compute > virtualMachineScaleSets > {사용자 확장 집합} > virtualMachines**

* **Azure PowerShell**  
이 명령은 tooget 몇 가지 정보를 사용 합니다.

  ```powershell
  Get-AzureRmResource -name vmsstest1 -ResourceGroupName vmsstestrg1 -ResourceType Microsoft.Compute/virtualMachineScaleSets -ApiVersion 2015-06-15
  Get-Autoscalesetting -ResourceGroup rainvmss -DetailedOutput
  ```

* Hello 눈금 집합 toomonitor 개별 프로세스에 hello 가상 컴퓨터에 원격으로 액세스할 수 있습니다 및 다른 컴퓨터는 것 처럼 toohello jumpbox 가상 컴퓨터를 연결 합니다.

## <a name="next-steps"></a>다음 단계
* 살펴보고 [가상 컴퓨터 크기 집합의 컴퓨터 크기를 자동으로 조정](virtual-machine-scale-sets-windows-autoscale.md) toosee toocreate 배율 설정 방법으로 구성 된 자동 크기 조정의 예입니다.

* [Azure Monitor PowerShell 빠른 시작 샘플](../monitoring-and-diagnostics/insights-powershell-samples.md)에서 Azure Monitor 모니터링 기능 예제를 찾아보세요.

* 알림 기능에 대 한 자세한 내용은 [Azure 모니터에서 자동 크기 조정 작업 toosend 전자 메일 및 webhook 경고 알림을 사용 하 여](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)합니다.

* 너무 방법에 대 한 자세한 내용은[Azure 모니터에서 사용 하 여 감사 로그를 toosend webhook 및 전자 메일 경고 알림](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)

* [고급 자동 크기 조정 시나리오](virtual-machine-scale-sets-advanced-autoscale.md)에 대해 자세히 알아봅니다.
