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
# <a name="autoscale-using-guest-metrics-in-a-linux-scale-set-template"></a>Linux 확장 집합 템플릿에서 게스트 메트릭을 사용한 자동 크기 조정

두 가지 방법으로 Azure에서 Vm에서 수집 하 고 집합의 크기를 조정 하는 메트릭을: 일부 돌아와 hello에서 VM을 호스트 하 고 hello 게스트 VM에서에서 다른 사용자가 제공 합니다. 호스트 메트릭 필요 하지 않습니다 추가 설정 hello 호스트, VM에 의해 수집 되므로 있어도 되지만 대부분의 게스트 메트릭 us tooinstall hello [Windows Azure 진단 확장](../virtual-machines/windows/extensions-diagnostics-template.md) 또는 hello [Linux Azure 진단 확장](../virtual-machines/linux/diagnostic-extension.md) hello에 게스트 VM입니다. 하나의 공통 이유 toouse 게스트 메트릭 호스트 메트릭 대신는 게스트 메트릭을 선택 하 여 메트릭 호스트 메트릭 보다 제공입니다. 이러한 예로 메모리 소비 메트릭을 들 수 있습니다. 이 메트릭은 게스트 메트릭을 통해서만 사용할 수 있습니다. 나열 된 지원 hello 호스트 메트릭 [여기](../monitoring-and-diagnostics/monitoring-supported-metrics.md), 자주 사용 되는 게스트 메트릭을 나열 됩니다 [여기](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md)합니다. 이 문서에서는 어떻게 toomodify hello [실행 가능한 최소 소수 자릿수 템플릿을 설정](./virtual-machine-scale-sets-mvss-start.md) toouse 자동 크기 조정 규칙 Linux 크기 집합에 대 한 게스트 메트릭을 기반으로 합니다.

## <a name="change-hello-template-definition"></a>Hello 템플릿 정의 변경 합니다.

이 실행 가능한 최소 소수 자릿수 집합 템플릿을 볼 수 있습니다 [여기](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), hello Linux 크기 게스트 기반 자동 크기 조정이 집합을 배포 하기 위한 우리의 서식 파일을 볼 수 있습니다 및 [여기](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json)합니다. 이 서식 파일 사용 diff toocreate hello를 검토해 보겠습니다 (`git diff minimum-viable-scale-set existing-vnet`) 하나씩:

먼저, `storageAccountName` 및 `storageAccountSasToken`의 매개 변수를 추가합니다. hello 진단 에이전트에서 메트릭 데이터를 보관 하는 [테이블](../cosmos-db/table-storage-how-to-use-dotnet.md) 이 저장소 계정에서 합니다. 부터 hello Linux 진단 에이전트 버전 3.0, 저장소 액세스 키를 사용 하 여은 더 이상 지원 합니다. [SAS 토큰](../storage/common/storage-dotnet-shared-access-signature-part-1.md)을 사용해야 합니다.

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

다음으로 hello 크기 집합을 수정 했습니다 `extensionProfile` tooinclude hello 진단 확장 합니다. 이 구성에서는 hello 리소스 hello 눈금의 ID 집합에서 toocollect 메트릭을 지정으로 저장소 계정 및 SAS 토큰 toouse toostore hello 메트릭을 hello. 또한에 (이 경우 1 분 마다) hello 메트릭이 얼마나 자주 집계 되 고 있는 메트릭 tootrack이 사례 백분율 사용 되는 메모리의 지정 합니다. 이 구성 및 사용된 메모리 비율 외의 다른 메트릭에 대한 자세한 내용은 [이 설명서](../virtual-machines/linux/diagnostic-extension.md)를 참조하세요.

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

마지막으로 추가 된 `autoscaleSettings` 이러한 메트릭을 기준으로 리소스 tooconfigure 자동 크기 조정 합니다. 이 리소스에는 `dependsOn` hello 눈금을 참조 하는 절은 임시 설정할 tooensure tooautoscale 시도 하기 전에 hello 크기 집합에 있는 것입니다. Hello를 사용 하면 다른 메트릭 tooautoscale에 선택 म `counterSpecifier` hello로 진단 확장 구성 hello에서에서 `metricName` hello 자동 크기 조정 구성에서 합니다. 자동 크기 조정 구성에 대 한 자세한 내용은 참조 hello [자동 크기 조정에 대 한 유용한 정보](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) 및 hello [Azure 모니터 REST API 참조 설명서](https://msdn.microsoft.com/library/azure/dn931928.aspx)합니다.

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





## <a name="next-steps"></a>다음 단계

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
