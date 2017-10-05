---
title: "Resource Manager 템플릿을 사용하여 진단 설정 자동 활성화 | Microsoft Docs"
description: "Resource Manager 템플릿을 사용하여 이벤트 허브로 진단 로그 스트림을 활성화하거나 로그를 저장소 계정에 저장하는 진단 설정을 만드는 방법을 알아봅니다."
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
ms.openlocfilehash: dde2435e976bbd14ca35cccc714ea21dcc5817b7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="automatically-enable-diagnostic-settings-at-resource-creation-using-a-resource-manager-template"></a><span data-ttu-id="bfab5-103">Resource Manager 템플릿을 사용하여 리소스 생성 시 진단 설정 자동 활성화</span><span class="sxs-lookup"><span data-stu-id="bfab5-103">Automatically enable Diagnostic Settings at resource creation using a Resource Manager template</span></span>
<span data-ttu-id="bfab5-104">이 문서에서는 [Azure Resource Manager 템플릿](../azure-resource-manager/resource-group-authoring-templates.md) 을 사용하여 리소스 생성 시 리소스에서 진단 설정을 구성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bfab5-104">In this article we show how you can use an [Azure Resource Manager template](../azure-resource-manager/resource-group-authoring-templates.md) to configure Diagnostic Settings on a resource when it is created.</span></span> <span data-ttu-id="bfab5-105">그러면 이벤트 허브로 진단 로그 및 메트릭의 스트리밍을 자동으로 시작하거나, 리소스 생성 시 Log Analytics에 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfab5-105">This enables you to automatically start streaming your Diagnostic Logs and metrics to Event Hubs, archiving them in a Storage Account, or sending them to Log Analytics when a resource is created.</span></span>

<span data-ttu-id="bfab5-106">Resource Manager 템플릿을 사용하여 진단 로그를 활성화하는 방법은 리소스 형식에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="bfab5-106">The method for enabling Diagnostic Logs using a Resource Manager template depends on the resource type.</span></span>

* <span data-ttu-id="bfab5-107">**비-계산** 리소스(예를 들어, 네트워크 보안 그룹, 논리 앱, 자동화)는 [이 문서에 설명된 진단 설정](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bfab5-107">**Non-Compute** resources (for example, Network Security Groups, Logic Apps, Automation) use [Diagnostic Settings described in this article](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span></span>
* <span data-ttu-id="bfab5-108"><seg>
  **계산** 리소스(WAD/LAD 기반)는 [이 문서에 설명된 WAD/LAD 구성 파일](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)을 사용합니다..</seg></span><span class="sxs-lookup"><span data-stu-id="bfab5-108">**Compute** (WAD/LAD-based) resources use the [WAD/LAD configuration file described in this article](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span></span>

<span data-ttu-id="bfab5-109">이 문서에서는 두 방법 중 하나를 사용하여 진단을 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="bfab5-109">In this article we describe how to configure diagnostics using either method.</span></span>

<span data-ttu-id="bfab5-110">기본적인 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bfab5-110">The basic steps are as follows:</span></span>

1. <span data-ttu-id="bfab5-111">리소스를 만들고 진단을 활성화하는 방법을 설명하는 JSON 파일로 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bfab5-111">Create a template as a JSON file that describes how to create the resource and enable diagnostics.</span></span>
2. <span data-ttu-id="bfab5-112">[배포 방법을 사용하여 템플릿을 배포합니다](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="bfab5-112">[Deploy the template using any deployment method](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

<span data-ttu-id="bfab5-113">다음은 비-계산 및 계산 리소스에 대해 생성해야 하는 템플릿 JSON 파일의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="bfab5-113">Below we give an example of the template JSON file you need to generate for non-Compute and Compute resources.</span></span>

## <a name="non-compute-resource-template"></a><span data-ttu-id="bfab5-114">비-계산 리소스 템플릿</span><span class="sxs-lookup"><span data-stu-id="bfab5-114">Non-Compute resource template</span></span>
<span data-ttu-id="bfab5-115">비-계산 리소스 템플릿의 경우 두 가지 작업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bfab5-115">For non-Compute resources, you will need to do two things:</span></span>

1. <span data-ttu-id="bfab5-116">저장소 계정 이름, 서비스 버스 규칙 ID 및/또는 OMS Log Analytics 작업 영역 ID(저장소 계정에 진단 로그 보관 활성화, 이벤트 허브에 로그 스트리밍 및/또는 Log Analytics에 로그 보내기)에 대한 매개 변수 blob에 매개 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bfab5-116">Add parameters to the parameters blob for the storage account name, service bus rule ID, and/or OMS Log Analytics workspace ID (enabling archival of Diagnostic Logs in a storage account, streaming of logs to Event Hubs, and/or sending logs to Log Analytics).</span></span>
   
    ```json
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of the Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for the Service Bus Namespace in which the Event Hub should be created or streamed to."
      }
    },
    "workspaceId":{
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for the Log Analytics workspace to which logs will be sent."
      }
    }
    ```
2. <span data-ttu-id="bfab5-117">진단 로그를 활성화할 리소스의 리소스 배열에서 `[resource namespace]/providers/diagnosticSettings`형식으로 리소스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bfab5-117">In the resources array of the resource for which you want to enable Diagnostic Logs, add a resource of type `[resource namespace]/providers/diagnosticSettings`.</span></span>
   
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

<span data-ttu-id="bfab5-118">진단 설정에 대한 속성 Blob는 [이 문서에 설명된 형식](https://msdn.microsoft.com/library/azure/dn931931.aspx)을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="bfab5-118">The properties blob for the Diagnostic Setting follows [the format described in this article](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span> <span data-ttu-id="bfab5-119">`metrics` 속성을 추가하면 [리소스는 Azure Monitor 메트릭스를 지원합니다](monitoring-supported-metrics.md)를 표시하고 리소스 메트릭을 이러한 동일한 출력으로 보낼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfab5-119">Adding the `metrics` property will enable you to also send resource metrics to these same outputs, provided that [the resource supports Azure Monitor metrics](monitoring-supported-metrics.md).</span></span>

<span data-ttu-id="bfab5-120">다음은 Logic App을 만들고 Event Hubs로 스트리밍 및 저장소 계정에 저장을 설정하는 전체 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="bfab5-120">Here is a full example that creates a Logic App and turns on streaming to Event Hubs and storage in a storage account.</span></span>

```json

{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "logicAppName": {
      "type": "string",
      "metadata": {
        "description": "Name of the Logic App that will be created."
      }
    },
    "testUri": {
      "type": "string",
      "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
    },
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of the Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for the Service Bus Namespace in which the Event Hub should be created or streamed to."
      }
    },
    "workspaceId": {
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for the Log Analytics workspace to which logs will be sent."
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

## <a name="compute-resource-template"></a><span data-ttu-id="bfab5-121">계산 리소스 템플릿</span><span class="sxs-lookup"><span data-stu-id="bfab5-121">Compute resource template</span></span>
<span data-ttu-id="bfab5-122">계산 리소스(예: 가상 컴퓨터 또는 서비스 패브릭 클러스터)에서 진단을 활성화하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="bfab5-122">To enable diagnostics on a Compute resource, for example a Virtual Machine or Service Fabric cluster, you need to:</span></span>

1. <span data-ttu-id="bfab5-123">Azure 진단 확장을 VM 리소스 정의에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bfab5-123">Add the Azure Diagnostics extension to the VM resource definition.</span></span>
2. <span data-ttu-id="bfab5-124">매개 변수로 저장소 계정 및/또는 이벤트 허브를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bfab5-124">Specify a storage account and/or event hub as a parameter.</span></span>
3. <span data-ttu-id="bfab5-125">모든 XML 문자를 올바르게 이스케이프하여 WADCfg XML 파일의 내용을 XMLCfg 속성에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bfab5-125">Add the contents of your WADCfg XML file into the XMLCfg property, escaping all XML characters properly.</span></span>

> [!WARNING]
> <span data-ttu-id="bfab5-126">이 마지막 단계는 이해하기 어려울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfab5-126">This last step can be tricky to get right.</span></span> <span data-ttu-id="bfab5-127">[이 문서를 참조](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) 하세요.</span><span class="sxs-lookup"><span data-stu-id="bfab5-127">[See this article](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) for an example that splits the Diagnostics Configuration Schema into variables that are escaped and formatted correctly.</span></span>
> 
> 

<span data-ttu-id="bfab5-128">샘플을 포함한 전체 과정은 [이 문서](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfab5-128">The entire process, including samples, is described [in this document](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bfab5-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bfab5-129">Next Steps</span></span>
* [<span data-ttu-id="bfab5-130">Azure 진단 로그에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="bfab5-130">Read more about Azure Diagnostic Logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
* [<span data-ttu-id="bfab5-131">이벤트 허브로 Azure 진단 로그 스트림</span><span class="sxs-lookup"><span data-stu-id="bfab5-131">Stream Azure Diagnostic Logs to Event Hubs</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)

