---
title: "리소스 관리자 템플릿을 사용하여 작업 그룹 만들기 | Microsoft Docs"
description: "Azure 리소스 관리자 템플릿을 사용하여 작업 그룹을 만드는 방법을 알아봅니다."
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
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: 76bf353cac13f1c2169380f8dd3c1e163d4f3f41
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-action-group-with-a-resource-manager-template"></a><span data-ttu-id="569d7-103">리소스 관리자 템플릿을 사용하여 작업 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="569d7-103">Create an action group with a Resource Manager template</span></span>
<span data-ttu-id="569d7-104">이 문서에서는 [Azure 리소스 관리자 템플릿](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates)을 사용하여 작업 그룹을 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="569d7-104">This article shows you how to use an [Azure Resource Manager template](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) to configure action groups.</span></span> <span data-ttu-id="569d7-105">템플릿을 사용하면 특정 유형의 경고에서 다시 사용할 수 있는 작업 그룹을 자동으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="569d7-105">By using templates, you can automatically set up action groups that can be reused in certain types of alerts.</span></span> <span data-ttu-id="569d7-106">이러한 작업 그룹은 경고가 트리거될 때 올바른 당사자가 모두 알림을 받을 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="569d7-106">These action groups ensure that all the correct parties are notified when an alert is triggered.</span></span>

<span data-ttu-id="569d7-107">기본 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="569d7-107">The basic steps are:</span></span>

1. <span data-ttu-id="569d7-108">작업 그룹을 만드는 방법을 설명하는 JSON 파일로 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="569d7-108">Create a template as a JSON file that describes how to create the action group.</span></span>

2. <span data-ttu-id="569d7-109">[배포 방법](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy)을 사용하여 템플릿을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="569d7-109">Deploy the template by using [any deployment method](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span>

<span data-ttu-id="569d7-110">첫째, 작업 정의가 템플릿에 하드 코드된 작업 그룹에 대한 리소스 관리자 템플릿을 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="569d7-110">First, we describe how to create a Resource Manager template for an action group where the action definitions are hard-coded in the template.</span></span> <span data-ttu-id="569d7-111">둘째, 템플릿을 배포할 때 입력된 매개 변수로 웹후크 구성 정보를 사용하는 템플릿을 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="569d7-111">Second, we describe how to create a template that takes the webhook configuration information as input parameters when the template is deployed.</span></span>

## <a name="resource-manager-templates-for-an-action-group"></a><span data-ttu-id="569d7-112">작업 그룹에 대한 리소스 관리자 템플릿</span><span class="sxs-lookup"><span data-stu-id="569d7-112">Resource Manager templates for an action group</span></span>

<span data-ttu-id="569d7-113">리소스 관리자 템플릿을 사용하여 작업 그룹을 만들려면 `Microsoft.Insights/actionGroups` 종류의 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="569d7-113">To create an action group by using a Resource Manager template, you create a resource of the type `Microsoft.Insights/actionGroups`.</span></span> <span data-ttu-id="569d7-114">그런 다음 모든 관련된 속성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="569d7-114">Then you fill in all related properties.</span></span> <span data-ttu-id="569d7-115">다음은 작업 그룹을 만드는 두 가지 예제 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="569d7-115">Here are two sample templates that create an action group.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "actionGroupName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within the Resource Group) for the Action group."
      }
    },
    "actionGroupShortName": {
      "type": "string",
      "metadata": {
        "description": "Short name (maximum 12 characters) for the Action group."
      }
    }
  },
  "resources": [
    {
      "type": "Microsoft.Insights/actionGroups",
      "apiVersion": "2017-04-01",
      "name": "[parameters('actionGroupName')]",
      "location": "Global",
      "properties": {
        "groupShortName": "[parameters('actionGroupShortName')]",
        "enabled": true,
        "smsReceivers": [
          {
            "name": "contosoSMS",
            "countryCode": "1",
            "phoneNumber": "5555551212"
          },
          {
            "name": "contosoSMS2",
            "countryCode": "1",
            "phoneNumber": "5555552121"
          }
        ],
        "emailReceivers": [
          {
            "name": "contosoEmail",
            "emailAddress": "devops@contoso.com"
          },
          {
            "name": "contosoEmail2",
            "emailAddress": "devops2@contoso.com"
          }
        ],
        "webhookReceivers": [
          {
            "name": "contosoHook",
            "serviceUri": "http://requestb.in/1bq62iu1"
          },
          {
            "name": "contosoHook2",
            "serviceUri": "http://requestb.in/1bq62iu2"
          }
        ]
      }
    }
  ],
  "outputs":{
      "actionGroupId":{
          "type":"string",
          "value":"[resourceId('Microsoft.Insights/actionGroups',parameters('actionGroupName'))]"
      }
  }
}
```

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "actionGroupName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within the Resource Group) for the Action group."
      }
    },
    "actionGroupShortName": {
      "type": "string",
      "metadata": {
        "description": "Short name (maximum 12 characters) for the Action group."
      }
    },
    "webhookReceiverName": {
      "type": "string",
      "metadata": {
        "description": "Webhook receiver service URI."
      }
    },    
    "webhookServiceUri": {
      "type": "string",
      "metadata": {
        "description": "Webhook receiver service URI."
      }
    }    
  },
  "resources": [
    {
      "type": "Microsoft.Insights/actionGroups",
      "apiVersion": "2017-04-01",
      "name": "[parameters('actionGroupName')]",
      "location": "Global",
      "properties": {
        "groupShortName": "[parameters('actionGroupShortName')]",
        "enabled": true,
        "smsReceivers": [
        ],
        "emailReceivers": [
        ],
        "webhookReceivers": [
          {
            "name": "[parameters('webhookReceiverName')]",
            "serviceUri": "[parameters('webhookServiceUri')]"
          }
        ]
      }
    }
  ],
  "outputs":{
      "actionGroupResourceId":{
          "type":"string",
          "value":"[resourceId('Microsoft.Insights/actionGroups',parameters('actionGroupName'))]"
      }
  }
}
```


## <a name="next-steps"></a><span data-ttu-id="569d7-116">다음 단계</span><span class="sxs-lookup"><span data-stu-id="569d7-116">Next steps</span></span>
* <span data-ttu-id="569d7-117">[작업 그룹](monitoring-action-groups.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="569d7-117">Learn more about [action groups](monitoring-action-groups.md).</span></span>
* <span data-ttu-id="569d7-118">[경고](monitoring-overview-alerts.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="569d7-118">Learn more about [alerts](monitoring-overview-alerts.md).</span></span>
* <span data-ttu-id="569d7-119">[리소스 관리자 템플릿을 사용하여 경고](monitoring-create-activity-log-alerts-with-resource-manager-template.md)를 추가하는 방법을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="569d7-119">Learn how to add [alerts by using a Resource Manager template](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>
