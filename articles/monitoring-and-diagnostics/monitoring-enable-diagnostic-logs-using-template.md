---
title: "aaaAutomatically 리소스 관리자 템플릿을 사용 하 여 진단 설정을 사용 하도록 설정 | Microsoft Docs"
description: "에 대해 알아봅니다 어떻게 toouse 리소스 관리자 수 있게 해 주는 toostream 템플릿 toocreate 진단 설정에 진단 로그 tooEvent 허브 또는 저장소 계정에 저장 합니다."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: a8a88a8c-4a48-4df6-8f7e-d90634d39c57
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/14/2017
ms.author: johnkem
ms.openlocfilehash: 8f38731107029928029c6d940da7bd076fea5d49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-enable-diagnostic-settings-at-resource-creation-using-a-resource-manager-template"></a>Resource Manager 템플릿을 사용하여 리소스 생성 시 진단 설정 자동 활성화
이 문서에서는 사용 하는 방법을 보여줍니다는 [Azure 리소스 관리자 템플릿](../azure-resource-manager/resource-group-authoring-templates.md) 만들어질 때 리소스에 tooconfigure 진단 설정 합니다. 이렇게 하면 진단 로그 및 메트릭 tooEvent 허브를 저장소 계정에이 보관 하거나 리소스를 만들 때 분석 tooLog 보내는 스트리밍 tooautomatically 시작 합니다.

리소스 관리자 템플릿을 사용 하 여 진단 로그를 사용 하기 위한 hello 메서드 hello 리소스 종류에 따라 달라 집니다.

* **비-계산** 리소스(예를 들어, 네트워크 보안 그룹, 논리 앱, 자동화)는 [이 문서에 설명된 진단 설정](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings)을 사용합니다.
* **계산** hello를 사용 하는 리소스 (WAD/했다 기반) [WAD/했다 구성 파일을이 문서에 설명 된](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)합니다.

이 문서에서 설명 어떻게 두 방법 중 하나를 사용 하 여 tooconfigure 진단 합니다.

hello 기본 단계는 다음과 같습니다.

1. 템플릿을 toocreate 리소스 hello 하 고 진단 기능을 사용 하는 방법에 대해 설명 하는 JSON 파일을 만듭니다.
2. [배포 방법을 사용 하 여 hello 템플릿을 배포](../azure-resource-manager/resource-group-template-deploy.md)합니다.

다음 템플릿 hello 비계산 및 계산 리소스에 대 한 toogenerate 해야 하는 JSON 파일의 예로 제공 합니다.

## <a name="non-compute-resource-template"></a>비-계산 리소스 템플릿
비계산 리소스에 대 한 두 가지 toodo이 필요 합니다.

1. Hello 저장소 계정 이름, 서비스 버스 규칙 ID 및/또는 OMS 로그 분석 작업 영역 ID (로그 tooEvent 허브의 스트리밍 및/또는 분석 로그 tooLog 보내는 저장소 계정에 진단 로그의 보관 가능)에 대 한 매개 변수 toohello 매개 변수 blob을 추가 합니다.
   
    ```json
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of hello Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for hello Service Bus Namespace in which hello Event Hub should be created or streamed to."
      }
    },
    "workspaceId":{
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for hello Log Analytics workspace toowhich logs will be sent."
      }
    }
    ```
2. 진단 로그 tooenable 원하는 hello 리소스의 리소스 배열의 hello 형식의 리소스를 추가 `[resource namespace]/providers/diagnosticSettings`합니다.
   
    ```json
    "resources": [
      {
        "type": "providers/diagnosticSettings",
        "name": "Microsoft.Insights/service",
        "dependsOn": [
          "[/*resource Id for which Diagnostic Logs will be enabled>*/]"
        ],
        "apiVersion": "2015-07-01",
        "properties": {
          "storageAccountId": "[resourceId('Microsoft.Storage/storageAccounts', parameters('storageAccountName'))]",
          "serviceBusRuleId": "[parameters('serviceBusRuleId')]",
          "workspaceId": "[parameters('workspaceId')]",
          "logs": [ 
            {
              "category": "/* log category name */",
              "enabled": true,
              "retentionPolicy": {
                "days": 0,
                "enabled": false
              }
            }
          ],
          "metrics": [
            {
              "timeGrain": "PT1M",
              "enabled": true,
              "retentionPolicy": {
                "enabled": false,
                "days": 0
              }
            }
          ]
        }
      }
    ]
    ```

hello hello 진단 설정에 대 한 blob 속성 뒤에 오는 [이 문서에 설명 된 hello 형식](https://msdn.microsoft.com/library/azure/dn931931.aspx)합니다. 추가 hello `metrics` 속성을 사용 하면 제공 하는 동일한가 데이터를 출력 하는 tooalso 송신 리소스 메트릭을 toothese [hello 리소스에서는 Azure 모니터 메트릭을 지원](monitoring-supported-metrics.md)합니다.

논리 앱을 만들고 스트리밍 tooEvent 허브 및 저장소 계정에서에서 저장소를 설정 하는 전체 예제는 다음과 같습니다.

```json

{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "logicAppName": {
      "type": "string",
      "metadata": {
        "description": "Name of hello Logic App that will be created."
      }
    },
    "testUri": {
      "type": "string",
      "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
    },
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of hello Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for hello Service Bus Namespace in which hello Event Hub should be created or streamed to."
      }
    },
    "workspaceId": {
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for hello Log Analytics workspace toowhich logs will be sent."
      }
    }
  },
  "variables": {},
  "resources": [
    {
      "type": "Microsoft.Logic/workflows",
      "name": "[parameters('logicAppName')]",
      "apiVersion": "2016-06-01",
      "location": "[resourceGroup().location]",
      "properties": {
        "definition": {
          "$schema": "http://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {
            "testURI": {
              "type": "string",
              "defaultValue": "[parameters('testUri')]"
            }
          },
          "triggers": {
            "recurrence": {
              "type": "recurrence",
              "recurrence": {
                "frequency": "Hour",
                "interval": 1
              }
            }
          },
          "actions": {
            "http": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('testUri')"
              },
              "runAfter": {}
            }
          },
          "outputs": {}
        },
        "parameters": {}
      },
      "resources": [
        {
          "type": "providers/diagnosticSettings",
          "name": "Microsoft.Insights/service",
          "dependsOn": [
            "[resourceId('Microsoft.Logic/workflows', parameters('logicAppName'))]"
          ],
          "apiVersion": "2015-07-01",
          "properties": {
            "storageAccountId": "[resourceId('Microsoft.Storage/storageAccounts', parameters('storageAccountName'))]",
            "serviceBusRuleId": "[parameters('serviceBusRuleId')]",
            "workspaceId": "[parameters('workspaceId')]",
            "logs": [
              {
                "category": "WorkflowRuntime",
                "enabled": true,
                "retentionPolicy": {
                  "days": 0,
                  "enabled": false
                }
              }
            ],
            "metrics": [
              {
                "timeGrain": "PT1M",
                "enabled": true,
                "retentionPolicy": {
                  "enabled": false,
                  "days": 0
                }
              }
            ]
          }
        }
      ],
      "dependsOn": []
    }
  ]
}

```

## <a name="compute-resource-template"></a>계산 리소스 템플릿
예: 가상 컴퓨터 또는 서비스 패브릭 클러스터에 계산 리소스에 대 한 tooenable 진단 해야합니다.

1. Hello Azure 진단 확장 toohello VM 리소스 정의 추가 합니다.
2. 매개 변수로 저장소 계정 및/또는 이벤트 허브를 지정합니다.
3. Hello XMLCfg 속성을 모든 XML 문자를 올바르게 이스케이프 hello 내용의 WADCfg XML 파일을 추가 합니다.

> [!WARNING]
> 이 마지막 단계는 작업은 복잡할 tooget 오른쪽 될 수 있습니다. [이 문서를 참조 하십시오.](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) 분할이 이스케이프 되 고 올바르게 형식이 지정 하는 변수로 진단 구성 스키마를 hello 예에 대 한 합니다.
> 
> 

hello 예제를 비롯 한 전체 프로세스를 설명 [이 문서에서](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

## <a name="next-steps"></a>다음 단계
* [Azure 진단 로그에 대해 자세히 알아보기](monitoring-overview-of-diagnostic-logs.md)
* [Azure 진단 로그 tooEvent 허브 스트림](monitoring-stream-diagnostic-logs-to-event-hubs.md)

