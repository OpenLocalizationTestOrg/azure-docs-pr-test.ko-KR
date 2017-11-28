---
title: "Linux 확장 집합 템플릿에서 게스트 메트릭을 사용하여 Azure 자동 크기 조정 사용 | Microsoft Docs"
description: "자세한 내용은 방법 tooautoscale 게스트 메트릭을 사용 하 여 Linux 가상 컴퓨터 크기 집합 서식 파일에"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: na
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: negat
ms.openlocfilehash: 7afbef943a5f15c7a72dcf7114f46d521c504424
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="autoscale-using-guest-metrics-in-a-linux-scale-set-template"></a><span data-ttu-id="30b04-103">Linux 확장 집합 템플릿에서 게스트 메트릭을 사용한 자동 크기 조정</span><span class="sxs-lookup"><span data-stu-id="30b04-103">Autoscale using guest metrics in a Linux scale set template</span></span>

<span data-ttu-id="30b04-104">두 가지 방법으로 Azure에서 Vm에서 수집 하 고 집합의 크기를 조정 하는 메트릭을: 일부 돌아와 hello에서 VM을 호스트 하 고 hello 게스트 VM에서에서 다른 사용자가 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b04-104">There are two types of metrics in Azure that are gathered from VMs and scale sets: some come from hello host VM and others come from hello guest VM.</span></span> <span data-ttu-id="30b04-105">호스트 메트릭 필요 하지 않습니다 추가 설정 hello 호스트, VM에 의해 수집 되므로 있어도 되지만 대부분의 게스트 메트릭 us tooinstall hello [Windows Azure 진단 확장](../virtual-machines/windows/extensions-diagnostics-template.md) 또는 hello [Linux Azure 진단 확장](../virtual-machines/linux/diagnostic-extension.md) hello에 게스트 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="30b04-105">Host metrics do not require additional setup because they are collected by hello host VM, whereas guest metrics require us tooinstall hello [Windows Azure Diagnostics extension](../virtual-machines/windows/extensions-diagnostics-template.md) or hello [Linux Azure Diagnostics extension](../virtual-machines/linux/diagnostic-extension.md) in hello guest VM.</span></span> <span data-ttu-id="30b04-106">하나의 공통 이유 toouse 게스트 메트릭 호스트 메트릭 대신는 게스트 메트릭을 선택 하 여 메트릭 호스트 메트릭 보다 제공입니다.</span><span class="sxs-lookup"><span data-stu-id="30b04-106">One common reason toouse guest metrics instead of host metrics is that guest metrics provide a larger selection of metrics than host metrics.</span></span> <span data-ttu-id="30b04-107">이러한 예로 메모리 소비 메트릭을 들 수 있습니다. 이 메트릭은 게스트 메트릭을 통해서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30b04-107">One such example is memory-consumption metrics, which are only available via guest metrics.</span></span> <span data-ttu-id="30b04-108">나열 된 지원 hello 호스트 메트릭 [여기](../monitoring-and-diagnostics/monitoring-supported-metrics.md), 자주 사용 되는 게스트 메트릭을 나열 됩니다 [여기](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="30b04-108">hello supported host metrics are listed [here](../monitoring-and-diagnostics/monitoring-supported-metrics.md), and commonly used guest metrics are listed [here](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span></span> <span data-ttu-id="30b04-109">이 문서에서는 어떻게 toomodify hello [실행 가능한 최소 소수 자릿수 템플릿을 설정](./virtual-machine-scale-sets-mvss-start.md) toouse 자동 크기 조정 규칙 Linux 크기 집합에 대 한 게스트 메트릭을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b04-109">This article shows how toomodify hello [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) toouse autoscale rules based on guest metrics for Linux scale sets.</span></span>

## <a name="change-hello-template-definition"></a><span data-ttu-id="30b04-110">Hello 템플릿 정의 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b04-110">Change hello template definition</span></span>

<span data-ttu-id="30b04-111">이 실행 가능한 최소 소수 자릿수 집합 템플릿을 볼 수 있습니다 [여기](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), hello Linux 크기 게스트 기반 자동 크기 조정이 집합을 배포 하기 위한 우리의 서식 파일을 볼 수 있습니다 및 [여기](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="30b04-111">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying hello Linux scale set with guest-based autoscale can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json).</span></span> <span data-ttu-id="30b04-112">이 서식 파일 사용 diff toocreate hello를 검토해 보겠습니다 (`git diff minimum-viable-scale-set existing-vnet`) 하나씩:</span><span class="sxs-lookup"><span data-stu-id="30b04-112">Let's examine hello diff used toocreate this template (`git diff minimum-viable-scale-set existing-vnet`) piece by piece:</span></span>

<span data-ttu-id="30b04-113">먼저, `storageAccountName` 및 `storageAccountSasToken`의 매개 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="30b04-113">First, we add parameters for `storageAccountName` and `storageAccountSasToken`.</span></span> <span data-ttu-id="30b04-114">hello 진단 에이전트에서 메트릭 데이터를 보관 하는 [테이블](../cosmos-db/table-storage-how-to-use-dotnet.md) 이 저장소 계정에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b04-114">hello diagnostics agent will store metric data in a [table](../cosmos-db/table-storage-how-to-use-dotnet.md) in this storage account.</span></span> <span data-ttu-id="30b04-115">부터 hello Linux 진단 에이전트 버전 3.0, 저장소 액세스 키를 사용 하 여은 더 이상 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b04-115">As of hello Linux Diagnostics Agent version 3.0, using a storage access key is no longer supported.</span></span> <span data-ttu-id="30b04-116">[SAS 토큰](../storage/common/storage-dotnet-shared-access-signature-part-1.md)을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b04-116">We must use a [SAS Token](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>

```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "storageAccountName": {
+      "type": "string"
+    },
+    "storageAccountSasToken": {
+      "type": "securestring"
     }
   },
```

<span data-ttu-id="30b04-117">다음으로 hello 크기 집합을 수정 했습니다 `extensionProfile` tooinclude hello 진단 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b04-117">Next, we modify hello scale set `extensionProfile` tooinclude hello diagnostics extension.</span></span> <span data-ttu-id="30b04-118">이 구성에서는 hello 리소스 hello 눈금의 ID 집합에서 toocollect 메트릭을 지정으로 저장소 계정 및 SAS 토큰 toouse toostore hello 메트릭을 hello.</span><span class="sxs-lookup"><span data-stu-id="30b04-118">In this configuration, we specify hello resource ID of hello scale set toocollect metrics from, as well as hello storage account and SAS token toouse toostore hello metrics.</span></span> <span data-ttu-id="30b04-119">또한에 (이 경우 1 분 마다) hello 메트릭이 얼마나 자주 집계 되 고 있는 메트릭 tootrack이 사례 백분율 사용 되는 메모리의 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b04-119">We also specify how frequently hello metrics are aggregated (in this case every minute) and which metrics tootrack (in this case percent used memory).</span></span> <span data-ttu-id="30b04-120">이 구성 및 사용된 메모리 비율 외의 다른 메트릭에 대한 자세한 내용은 [이 설명서](../virtual-machines/linux/diagnostic-extension.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30b04-120">For more detailed information on this configuration and metrics other than percent used memory, see [this documentation](../virtual-machines/linux/diagnostic-extension.md).</span></span>

```diff
                 }
               }
             ]
+          },
+          "extensionProfile": {
+            "extensions": [
+              {
+                "name": "LinuxDiagnosticExtension",
+                "properties": {
+                  "publisher": "Microsoft.Azure.Diagnostics",
+                  "type": "LinuxDiagnostic",
+                  "typeHandlerVersion": "3.0",
+                  "settings": {
+                    "StorageAccount": "[parameters('storageAccountName')]",
+                    "ladCfg": {
+                      "diagnosticMonitorConfiguration": {
+                        "performanceCounters": {
+                          "sinks": "WADMetricJsonBlob",
+                          "performanceCounterConfiguration": [
+                            {
+                              "unit": "percent",
+                              "type": "builtin",
+                              "class": "memory",
+                              "counter": "percentUsedMemory",
+                              "counterSpecifier": "/builtin/memory/percentUsedMemory",
+                              "condition": "IsAggregate=TRUE"
+                            }
+                          ]
+                        },
+                        "metrics": {
+                          "metricAggregation": [
+                            {
+                              "scheduledTransferPeriod": "PT1M"
+                            }
+                          ],
+                          "resourceId": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]"
+                        }
+                      }
+                    }
+                  },
+                  "protectedSettings": {
+                    "storageAccountName": "[parameters('storageAccountName')]",
+                    "storageAccountSasToken": "[parameters('storageAccountSasToken')]",
+                    "sinksConfig": {
+                      "sink": [
+                        {
+                          "name": "WADMetricJsonBlob",
+                          "type": "JsonBlob"
+                        }
+                      ]
+                    }
+                  }
+                }
+              }
+            ]
           }
         }
       }
```

<span data-ttu-id="30b04-121">마지막으로 추가 된 `autoscaleSettings` 이러한 메트릭을 기준으로 리소스 tooconfigure 자동 크기 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b04-121">Finally, we add an `autoscaleSettings` resource tooconfigure autoscale based on these metrics.</span></span> <span data-ttu-id="30b04-122">이 리소스에는 `dependsOn` hello 눈금을 참조 하는 절은 임시 설정할 tooensure tooautoscale 시도 하기 전에 hello 크기 집합에 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="30b04-122">This resource has a `dependsOn` clause that references hello scale set tooensure that hello scale set exists before attempting tooautoscale it.</span></span> <span data-ttu-id="30b04-123">Hello를 사용 하면 다른 메트릭 tooautoscale에 선택 म `counterSpecifier` hello로 진단 확장 구성 hello에서에서 `metricName` hello 자동 크기 조정 구성에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="30b04-123">If we choose a different metric tooautoscale on, we would use hello `counterSpecifier` from hello diagnostics extension configuration as hello `metricName` in hello autoscale configuration.</span></span> <span data-ttu-id="30b04-124">자동 크기 조정 구성에 대 한 자세한 내용은 참조 hello [자동 크기 조정에 대 한 유용한 정보](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) 및 hello [Azure 모니터 REST API 참조 설명서](https://msdn.microsoft.com/library/azure/dn931928.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="30b04-124">For more information on autoscale configuration, see hello [autoscale best practices](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) and hello [Azure Monitor REST API reference documentation](https://msdn.microsoft.com/library/azure/dn931928.aspx).</span></span>

```diff
+    },
+    {
+      "type": "Microsoft.Insights/autoscaleSettings",
+      "apiVersion": "2015-04-01",
+      "name": "guestMetricsAutoscale",
+      "location": "[resourceGroup().location]",
+      "dependsOn": [
+        "Microsoft.Compute/virtualMachineScaleSets/myScaleSet"
+      ],
+      "properties": {
+        "name": "guestMetricsAutoscale",
+        "targetResourceUri": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]",
+        "enabled": true,
+        "profiles": [
+          {
+            "name": "Profile1",
+            "capacity": {
+              "minimum": "1",
+              "maximum": "10",
+              "default": "3"
+            },
+            "rules": [
+              {
+                "metricTrigger": {
+                  "metricName": "/builtin/memory/percentUsedMemory",
+                  "metricNamespace": "",
+                  "metricResourceUri": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]",
+                  "timeGrain": "PT1M",
+                  "statistic": "Average",
+                  "timeWindow": "PT5M",
+                  "timeAggregation": "Average",
+                  "operator": "GreaterThan",
+                  "threshold": 60
+                },
+                "scaleAction": {
+                  "direction": "Increase",
+                  "type": "ChangeCount",
+                  "value": "1",
+                  "cooldown": "PT1M"
+                }
+              },
+              {
+                "metricTrigger": {
+                  "metricName": "/builtin/memory/percentUsedMemory",
+                  "metricNamespace": "",
+                  "metricResourceUri": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]",
+                  "timeGrain": "PT1M",
+                  "statistic": "Average",
+                  "timeWindow": "PT5M",
+                  "timeAggregation": "Average",
+                  "operator": "LessThan",
+                  "threshold": 30
+                },
+                "scaleAction": {
+                  "direction": "Decrease",
+                  "type": "ChangeCount",
+                  "value": "1",
+                  "cooldown": "PT1M"
+                }
+              }
+            ]
+          }
+        ]
+      }
     }
   ]
 }
```





## <a name="next-steps"></a><span data-ttu-id="30b04-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="30b04-125">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
