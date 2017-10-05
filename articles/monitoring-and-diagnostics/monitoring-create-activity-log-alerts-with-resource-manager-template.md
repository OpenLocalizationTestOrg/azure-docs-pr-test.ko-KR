---
title: "리소스 관리자 템플릿을 사용하여 활동 로그 경고 만들기 | Microsoft Docs"
description: "Azure 리소스가 만들어질 때 알림을 받습니다."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: ancav
ms.openlocfilehash: 92076c7fe1f867919b7e02abf79cf0fb74fb7eb4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-activity-log-alert-with-a-resource-manager-template"></a><span data-ttu-id="48693-103">리소스 관리자 템플릿을 사용하여 활동 로그 경고 만들기</span><span class="sxs-lookup"><span data-stu-id="48693-103">Create an activity log alert with a Resource Manager template</span></span>
<span data-ttu-id="48693-104">이 문서에서는 [Azure 리소스 관리자 템플릿](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates)을 사용하여 활동 로그 경고를 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="48693-104">This article shows you how to use an [Azure Resource Manager template](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) to configure activity log alerts.</span></span> <span data-ttu-id="48693-105">템플릿을 사용하면 자동화된 배포 프로세스의 일부로 특정 활동 로그 이벤트 조건에 따라 많은 활성화하는 많은 경고를 쉽게 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48693-105">By using templates, you can easily set up many alerts that activate based on specific activity log event conditions as part of your automated deployment process.</span></span>

<span data-ttu-id="48693-106">기본 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="48693-106">The basic steps are:</span></span>

1. <span data-ttu-id="48693-107">활동 로그 경고를 만드는 방법을 설명하는 JSON 파일로 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="48693-107">Create a template as a JSON file that describes how to create the activity log alert.</span></span>

2. <span data-ttu-id="48693-108">[배포 방법](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy)을 사용하여 템플릿을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="48693-108">Deploy the template by using [any deployment method](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span>

## <a name="resource-manager-template-for-an-activity-log-alert"></a><span data-ttu-id="48693-109">활동 로그 경고에 대한 Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="48693-109">Resource Manager template for an activity log alert</span></span>
<span data-ttu-id="48693-110">리소스 관리자 템플릿을 사용하여 활동 로그 경고를 만들려면 `microsoft.insights/activityLogAlerts` 유형의 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="48693-110">To create an activity log alert by using a Resource Manager template, you create a resource of the type `microsoft.insights/activityLogAlerts`.</span></span> <span data-ttu-id="48693-111">그런 다음 모든 관련된 속성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="48693-111">Then you fill in all related properties.</span></span> <span data-ttu-id="48693-112">다음은 활동 로그 경고를 만드는 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="48693-112">Here's a template that creates an activity log alert.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "activityLogAlertName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within the Resource Group) for the Activity log alert."
      }
    },
    "activityLogAlertEnabled": {
      "type": "bool",
      "defaultValue": true,
      "metadata": {
        "description": "Indicates whether or not the alert is enabled."
      }
    },
    "actionGroupResourceId": {
      "type": "string",
      "metadata": {
        "description": "Resource Id for the Action group."
      }
    }
  },
  "resources": [   
    {
      "type": "Microsoft.Insights/activityLogAlerts",
      "apiVersion": "2017-04-01",
      "name": "[parameters('activityLogAlertName')]",      
      "location": "Global",
      "properties": {
        "enabled": "[parameters('activityLogAlertEnabled')]",
        "scopes": [
            "[subscription().id]"
        ],        
        "condition": {
          "allOf": [
            {
              "field": "category",
              "equals": "Administrative"
            },
            {
              "field": "operationName",
              "equals": "Microsoft.Resources/deployments/write"
            },
            {
              "field": "resourceType",
              "equals": "Microsoft.Resources/deployments"
            }
          ] 
        },
        "actions": {
          "actionGroups": 
          [
            {
              "actionGroupId": "[parameters('actionGroupResourceId')]"
            }
          ]
        }
      }
    }
  ]
}
```

<span data-ttu-id="48693-113">[Azure 빠른 시작 갤러리](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights)를 방문하여 활동 로그 경고 템플릿의 몇 가지 예제를 확인해 보세요.</span><span class="sxs-lookup"><span data-stu-id="48693-113">Visit our [Azure Quickstart gallery](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights) for some examples of activity log alert templates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48693-114">다음 단계</span><span class="sxs-lookup"><span data-stu-id="48693-114">Next steps</span></span>
- <span data-ttu-id="48693-115">[경고](monitoring-overview-alerts.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="48693-115">Learn more about [alerts](monitoring-overview-alerts.md).</span></span>
- <span data-ttu-id="48693-116">[ 템플릿을 사용하여 작업 그룹](monitoring-create-action-group-with-resource-manager-template.md)을 추가하는 방법을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="48693-116">Learn how to add [action groups by using a Resource Manager template](monitoring-create-action-group-with-resource-manager-template.md).</span></span>
- <span data-ttu-id="48693-117">[구독의 모든 자동 크기 조정 엔진 작업을 모니터링하기 위한 활동 로그 경고를 만드는](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert) 방법을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="48693-117">Learn how to [create an activity log alert to monitor all autoscale engine operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span></span>
- <span data-ttu-id="48693-118">[구독에서 실패한 모든 자동 크기 조정 규모 감축/규모 확장 작업을 모니터링하기 위한 활동 로그 경고를 만드는](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert) 방법을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="48693-118">Learn how to [create an activity log alert to monitor all failed autoscale scale-in/scale-out operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span></span>
