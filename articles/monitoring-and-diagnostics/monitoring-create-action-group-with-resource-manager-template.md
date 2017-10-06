---
title: "리소스 관리자 템플릿으로 aaaCreate 동작 그룹 | Microsoft Docs"
description: "Azure 리소스 관리자 템플릿을 사용 하 여 toocreate 동작을 그룹화 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 9902b33cad99bd99b3deda0cf6f4ff12278c89c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-action-group-with-a-resource-manager-template"></a>리소스 관리자 템플릿을 사용하여 작업 그룹 만들기
이 문서에서는 어떻게 toouse는 [Azure 리소스 관리자 템플릿](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure 동작 그룹입니다. 템플릿을 사용하면 특정 유형의 경고에서 다시 사용할 수 있는 작업 그룹을 자동으로 설정할 수 있습니다. 이러한 동작 그룹 모든 hello 올바른 경고가 트리거될 때 당사자에 게 알림을 확인 합니다.

hello 기본 단계입니다.

1. 템플릿을 toocreate 동작 그룹을 hello 하는 방법을 설명 하는 JSON 파일을 만듭니다.

2. Hello 템플릿을 사용 하 여 배포 [는 배포 방법을](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy)합니다.

첫째, 설명 hello 작업 정의 hello 서식 파일에 하드 코드 하는 위치는 작업에 대 한 리소스 관리자 템플릿을 toocreate을 그룹화 하는 방법을 합니다. 둘째, 어떻게 toocreate로 hello webhook 구성 정보를 사용 하는 템플릿을 입력 매개 변수 hello 서식 파일을 배포할 때 설명 합니다.

## <a name="resource-manager-templates-for-an-action-group"></a>작업 그룹에 대한 리소스 관리자 템플릿

hello 형식의 리소스를 만들 리소스 관리자 템플릿을 사용 하 여 작업 그룹에는 toocreate `Microsoft.Insights/actionGroups`합니다. 그런 다음 모든 관련된 속성을 입력합니다. 다음은 작업 그룹을 만드는 두 가지 예제 템플릿입니다.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "actionGroupName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within hello Resource Group) for hello Action group."
      }
    },
    "actionGroupShortName": {
      "type": "string",
      "metadata": {
        "description": "Short name (maximum 12 characters) for hello Action group."
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
        "description": "Unique name (within hello Resource Group) for hello Action group."
      }
    },
    "actionGroupShortName": {
      "type": "string",
      "metadata": {
        "description": "Short name (maximum 12 characters) for hello Action group."
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


## <a name="next-steps"></a>다음 단계
* [작업 그룹](monitoring-action-groups.md)에 대해 자세히 알아보세요.
* [경고](monitoring-overview-alerts.md)에 대해 자세히 알아보세요.
* 자세한 내용은 방법 tooadd [리소스 관리자 템플릿을 사용 하 여 경고](monitoring-create-activity-log-alerts-with-resource-manager-template.md)합니다.
