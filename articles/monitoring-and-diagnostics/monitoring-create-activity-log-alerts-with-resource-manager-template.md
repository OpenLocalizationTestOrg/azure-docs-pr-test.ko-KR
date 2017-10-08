---
title: "리소스 관리자 템플릿 사용 하 여 활동 로그 경고 aaaCreate | Microsoft Docs"
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
ms.openlocfilehash: 0fb8aa037b9dce54ce35498622770955f2341bc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-activity-log-alert-with-a-resource-manager-template"></a>리소스 관리자 템플릿을 사용하여 활동 로그 경고 만들기
이 문서에서는 어떻게 toouse는 [Azure 리소스 관리자 템플릿](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure 활동 로그 경고 합니다. 템플릿을 사용하면 자동화된 배포 프로세스의 일부로 특정 활동 로그 이벤트 조건에 따라 많은 활성화하는 많은 경고를 쉽게 설정할 수 있습니다.

hello 기본 단계입니다.

1. 템플릿을 toocreate hello 활동 경고를 기록 하는 방법을 설명 하는 JSON 파일을 만듭니다.

2. Hello 템플릿을 사용 하 여 배포 [는 배포 방법을](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy)합니다.

## <a name="resource-manager-template-for-an-activity-log-alert"></a>활동 로그 경고에 대한 Resource Manager 템플릿
hello 형식의 리소스를 만들 리소스 관리자 템플릿을 사용 하 여 활동 로그 경고 toocreate `microsoft.insights/activityLogAlerts`합니다. 그런 다음 모든 관련된 속성을 입력합니다. 다음은 활동 로그 경고를 만드는 템플릿입니다.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "activityLogAlertName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within hello Resource Group) for hello Activity log alert."
      }
    },
    "activityLogAlertEnabled": {
      "type": "bool",
      "defaultValue": true,
      "metadata": {
        "description": "Indicates whether or not hello alert is enabled."
      }
    },
    "actionGroupResourceId": {
      "type": "string",
      "metadata": {
        "description": "Resource Id for hello Action group."
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

[Azure 빠른 시작 갤러리](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights)를 방문하여 활동 로그 경고 템플릿의 몇 가지 예제를 확인해 보세요.

## <a name="next-steps"></a>다음 단계
- [경고](monitoring-overview-alerts.md)에 대해 자세히 알아보세요.
- 자세한 내용은 방법 tooadd [리소스 관리자 템플릿을 사용 하 여 작업 그룹](monitoring-create-action-group-with-resource-manager-template.md)합니다.
- 너무 방법에 대해 알아봅니다[활동 로그 경고 toomonitor 구독에 대 한 모든 자동 크기 조정 엔진 작업을 만드는](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)합니다.
- 너무 방법에 대해 알아봅니다[활동 로그 경고 toomonitor 구독에 대 한 모든 실패 한 자동 크기 조정 눈금-/ 스케일 아웃 작업을 만들](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)합니다.
