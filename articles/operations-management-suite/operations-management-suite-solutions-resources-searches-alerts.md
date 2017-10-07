---
title: "aaaSaved 검색 및 OMS 솔루션에서 경고 | Microsoft Docs"
description: "OMS의 솔루션 hello 솔루션에 의해 수집 된 로그 분석 tooanalyze 데이터에 저장 된 검색을 일반적으로 포함 됩니다.  경고 toonotify hello 사용자 정의 되었거나 자동으로 응답 tooa 중요 한 문제에서 작업을 수행 합니다.  이 문서에서는 어떻게 toodefine 로그 분석 검색 및 경고는 ARM 서식 파일에 저장 관리 솔루션에 포함 될 수 있도록 설명 합니다."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 93d7c5bbf061473833ca6c0a8e4d8e10d923f3ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-log-analytics-saved-searches-and-alerts-toooms-management-solution-preview"></a>로그 분석 추가 저장 된 검색 및 알림 tooOMS 관리 솔루션 (미리 보기)

> [!NOTE]
> 현재 Preview로 제공되는 OMS의 사용자 지정 솔루션 만들기에 대한 예비 설명서입니다. 아래에 설명 된 모든 스키마 주체 toochange입니다.   


[OMS의 관리 솔루션](operations-management-suite-solutions.md) 는 일반적으로 포함 [저장 된 검색](../log-analytics/log-analytics-log-searches.md) hello 솔루션에 의해 수집 된 로그 분석 tooanalyze 데이터에서입니다.  정의할 수도 있습니다 [경고](../log-analytics/log-analytics-alerts.md) toonotify 사용자 hello 또는 자동으로 응답 tooa 중요 한 문제에서 작업을 수행 합니다.  이 문서에서는 toodefine 로그 분석 검색 및 경고를 저장 하는 방법을 설명는 [리소스 관리 템플릿](../resource-manager-template-walkthrough.md) 에 포함 될 수 있으므로 [관리 솔루션](operations-management-suite-solutions-creating.md)합니다.

> [!NOTE]
> hello 샘플이이 문서에서 사용 하 여 매개 변수 및 필수 또는 일반적인 toomanagement 솔루션 중 하나에 설명 된 있는 변수 [Operations Management Suite (OMS)에서 관리 솔루션 만들기](operations-management-suite-solutions-creating.md)  

## <a name="prerequisites"></a>필수 조건
이 문서에서는 하 이미 방법을 잘 알고 너무 가정[관리 솔루션을 만들어](operations-management-suite-solutions-creating.md) 와의 hello 구조는 [ARM 템플릿을](../resource-group-authoring-templates.md) 및 솔루션 파일입니다.


## <a name="log-analytics-workspace"></a>Log Analytics 작업 영역
Log Analytics의 모든 리소스는 [작업 영역](../log-analytics/log-analytics-manage-access.md)에 포함됩니다.  에 설명 된 대로 [OMS 작업 영역 및 자동화 계정](operations-management-suite-solutions.md#oms-workspace-and-automation-account) hello 작업 영역 hello 관리 솔루션에 포함 되어 있지 않지만 hello 솔루션을 설치 하기 전에 존재 해야 합니다.  사용할 수 없으면 hello 솔루션 설치 실패 합니다.

hello 이름이 hello 작업 영역의 각 로그 분석 리소스의 hello 이름입니다.  Hello 사용 하 여 hello 솔루션에서 이렇게 **작업 영역** hello 다음 savedsearch 리소스의 예제에서와 같이 매개 변수입니다.

    "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearchId'))]"


## <a name="saved-searches"></a>저장된 검색
포함 [저장 된 검색](../log-analytics/log-analytics-log-searches.md) 솔루션 tooallow 사용자 tooquery 데이터 솔루션에서 수집 합니다.  저장 된 검색 아래에 표시 될 **즐겨찾기** hello OMS 포털에서 및 **저장 된 검색** hello Azure 포털의에서.  각 경고에도 저장된 검색이 필요합니다.   

[로그 분석에 저장 된 검색](../log-analytics/log-analytics-log-searches.md) 리소스 유형의 `Microsoft.OperationalInsights/workspaces/savedSearches` 있고 hello 구조를 수행 합니다.  여기에 일반적인 변수 및 매개 변수 복사 하 고이 코드 조각은 솔루션 파일에 붙여 하 고 hello 매개 변수 이름을 변경할 수 있도록 합니다. 

    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
        ],
        "tags": { },
        "properties": {
            "etag": "*",
            "query": "[variables('SavedSearch').Query]",
            "displayName": "[variables('SavedSearch').DisplayName]",
            "category": "[variables('SavedSearch').Category]"
        }
    }



각각의 저장된 된 검색의 hello 속성 hello 다음 표에 설명 되어 있습니다. 

| 속성 | 설명 |
|:--- |:--- |
| 카테고리 | hello 저장 된 검색에 대 한 hello 범주입니다.  모든 저장 된 검색에 동일한 솔루션은 종종를 공유 하는 hello 단일 범주 hello 콘솔에서 함께 그룹화 되어 있도록 합니다. |
| displayname | Hello에 대 한 이름 toodisplay hello 포털에서 검색을 저장 합니다. |
| 쿼리 | Toorun를 쿼리 합니다. |

> [!NOTE]
> JSON으로 해석할 수 없는 문자를 포함 하는 경우 hello 쿼리에서 toouse 이스케이프 문자를 할 수 있습니다.  예를 들어, 쿼리 되었으면 **유형: AzureActivity OperationName:"Microsoft.Compute/virtualMachines/write"**, hello 솔루션 파일에 쓸지 **유형: AzureActivity OperationName:\" Microsoft.Compute/virtualMachines/write\"**합니다.

## <a name="alerts"></a>경고
[Log Analytics 경고](../log-analytics/log-analytics-alerts.md)는 일정한 간격으로 저장된 검색을 실행하는 경고 규칙에 의해 만들어집니다.  지정 된 조건과 일치 하는 hello hello 쿼리 결과 경고 레코드 만들어지고 하나 이상의 동작이 실행 됩니다.  

경고 규칙 관리 솔루션에서은 다음 세 가지 서로 다른 리소스 hello 구성 됩니다.

- **저장된 검색.**  실행 되는 hello 로그 검색을 정의 합니다.  여러 경고 규칙이 하나의 저장된 검색을 공유할 수 있습니다.
- **일정.**  얼마나 자주 hello 로그 검색 해야 할 정의 합니다.  각 경고 규칙은 일정을 하나만 갖습니다.
- **경고 작업.**  각 경고 규칙의 형식 가진 하나의 작업 리소스 갖습니다 **경고** hello 경고 경고 레코드 생성 되 고 경고의 심각도 hello 시기에 대 한 hello 조건 등의 hello 세부 정보를 정의 하는 합니다.  hello 동작 리소스에서 필요에 따라 메일 및 runbook 응답을 정의 합니다.
- **웹후크 작업(선택 사항).**  Hello 경고 규칙은 여 webhook을 사용할지를 호출 하는 경우 프로그램의 추가적인 동작이 리소스 형식의 필요 **Webhook**합니다.    

저장된 검색 리소스는 위에 설명되어 있습니다.  hello 다른 리소스 다음과 같습니다.


### <a name="schedule-resource"></a>일정 리소스

저장된 검색은 하나 이상의 일정을 가질 수 있으며 각 일정은 별도의 경고 규칙을 나타냅니다. hello 일정 정의 얼마나 자주 hello 검색 실행 되 고 있는 hello를 통해 데이터를 검색 하는 시간 간격을 hello 합니다.  일정 리소스 유형의 `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` 있고 hello 구조를 수행 합니다. 여기에 일반적인 변수 및 매개 변수 복사 하 고이 코드 조각은 솔루션 파일에 붙여 하 고 hello 매개 변수 이름을 변경할 수 있도록 합니다. 


    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name)]"
        ],
        "properties": {
            "etag": "*",
            "interval": "[variables('Schedule').Interval]",
            "queryTimeSpan": "[variables('Schedule').TimeSpan]",
            "enabled": "[variables('Schedule').Enabled]"
        }
    }



다음 표에 hello 일정 리소스에 대 한 hello 속성 설명 합니다.

| 요소 이름 | 필수 | 설명 |
|:--|:--|:--|
| 사용       | 예 | Hello 경고가 생성 될 때 사용 되는지 여부를 지정 합니다. |
| interval      | 예 | Hello 쿼리를 실행 빈도 (분)에서입니다. |
| queryTimeSpan | 예 | 시간 (분)는 tooevaluate 결과 길이입니다. |

hello 일정 리소스 hello hello 일정 전에 만들어질 수 있도록 저장 된 검색에 의존 해야 합니다.


### <a name="actions"></a>작업
Hello로 지정 된 작업 리소스의 두 가지 **형식** 속성입니다.  일정에 따라 하나 필요로 **경고** hello 경고 규칙 및 경고를 만들 때 수행 되는 작업의 hello 세부 정보를 정의 하는 작업입니다.  포함 될 수도 있습니다는 **Webhook** hello 경고에서 여 webhook을 사용할지를 호출 해야 하는 경우 작업 합니다.  

작업 리소스의 형식은 `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`입니다.  

#### <a name="alert-actions"></a>경고 작업

모든 일정은 하나의 **경고** 작업을 갖게 됩니다.  이 hello 경고 및 알림 및 업데이트 관리 작업을 필요에 따라 hello 세부 정보를 정의 합니다.  알림을 보내는 전자 메일 tooone 또는 더 많은 주소입니다.  업데이트 관리 tooattempt tooremediate hello 검색 문제 Azure 자동화에서에서 runbook을 시작합니다.

경고 작업은 hello 구조를 수행 합니다.  여기에 일반적인 변수 및 매개 변수 복사 하 고이 코드 조각은 솔루션 파일에 붙여 하 고 hello 매개 변수 이름을 변경할 수 있도록 합니다. 



    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Alert').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
        ],
        "properties": {
            "etag": "*",
            "type": "Alert",
            "name": "[variables('Alert').Name]",
            "description": "[variables('Alert').Description]",
            "severity": "[variables('Alert').Severity]",
            "threshold": {
                "operator": "[variables('Alert').Threshold.Operator]",
                "value": "[variables('Alert').Threshold.Value]",
                "metricsTrigger": {
                    "triggerCondition": "[variables('Alert').Threshold.Trigger.Condition]",
                    "operator": "[variables('Alert').Trigger.Operator]",
                    "value": "[variables('Alert').Trigger.Value]"
                },
            },
            "emailNotification": {
                "recipients": [
                    "[variables('Alert').Recipients]"
                ],
                "subject": "[variables('Alert').Subject]"
            },
            "remediation": {
                "runbookName": "[variables('Alert').Remedition.RunbookName]",
                "webhookUri": "[variables('Alert').Remedition.WebhookUri]"
            }
        }
    }

다음 표에서 hello 경고 작업 리소스에 대 한 hello 속성 설명 합니다.

| 요소 이름 | 필수 | 설명 |
|:--|:--|:--|
| 유형 | 예 | Hello 작업 형식입니다.  경고 작업의 **경고**가 됩니다. |
| 이름 | 예 | Hello 경고에 대 한 표시 이름입니다.  Hello 경고 규칙에 대 한 hello 콘솔에 표시 되는 hello 이름입니다. |
| 설명 | 아니요 | Hello 경고의 선택적 설명입니다. |
| 심각도 | 예 | 다음 값에는 hello에서 hello 경고 레코드의 심각도:<br><br> **중요**<br>**Warning**<br>**정보 제공** |


##### <a name="threshold"></a>임계값
이 섹션은 필수입니다.  Hello 경고 임계값에 대 한 hello 속성을 정의합니다.

| 요소 이름 | 필수 | 설명 |
|:--|:--|:--|
| 연산자 | 예 | 다음 값에는 hello에서 hello 비교 연산자:<br><br>**gt = 보다 큼<br>lt = 보다 작음** |
| 값 | 예 | hello toocompare hello 결과 값입니다. |


##### <a name="metricstrigger"></a>MetricsTrigger
이 섹션은 선택 사항입니다.  미터법 경고에는 이 섹션을 포함해야 합니다.

> [!NOTE]
> 미터법 알림은 현재 공개 미리 보기 상태입니다. 

| 요소 이름 | 필수 | 설명 |
|:--|:--|:--|
| TriggerCondition | 예 | Hello 임계값 위반이 나 다음 값에는 hello에서 연속 된 위반의 총 용인지 여부를 지정 합니다.<br><br>**총<br>연속** |
| 연산자 | 예 | 다음 값에는 hello에서 hello 비교 연산자:<br><br>**gt = 보다 큼<br>lt = 보다 작음** |
| 값 | 예 | Hello hello 기준 시간 수가 met tootrigger hello 경고 이어야 합니다. |

##### <a name="throttling"></a>제한
이 섹션은 선택 사항입니다.  잠시 후 경고가 만들어지고에 대 한 규칙이 동일한 hello에서 toosuppress 경고를 발생 시킬 경우에이 섹션을 포함 합니다.

| 요소 이름 | 필수 | 설명 |
|:--|:--|:--|
| DurationInMinutes | 제한 요소가 포함된 경우 필수입니다. | 동일한 경고 규칙을 만들면 hello에서 후 분 toosuppress 경고 수입니다. |

##### <a name="emailnotification"></a>EmailNotification
 이 섹션은 경고 toosend 메일 tooone 또는 더 많은 수신자 hello 하려면 선택적 포함 합니다.

| 요소 이름 | 필수 | 설명 |
|:--|:--|:--|
| 받는 사람 | 예 | 전자 메일의 쉼표로 구분 된 목록 hello 다음 예제에서에서와 같은 경고를 만들 때 toosend 알림을 해결 합니다.<br><br>**[ "recipient1@contoso.com", "recipient2@contoso.com" ]** |
| 제목 | 예 | Hello 메일의 제목 줄입니다. |
| 첨부 파일 | 아니요 | 첨부 파일은 현재 지원되지 않습니다.  이 요소를 포함하는 경우 **없음**이어야 합니다. |


##### <a name="remediation"></a>재구성
이 섹션은 선택 사항 응답 toohello 경고의 runbook toostart 하려는 경우이 포함 합니다. |

| 요소 이름 | 필수 | 설명 |
|:--|:--|:--|
| RunbookName | 예 | Hello runbook toostart의 이름입니다. |
| WebhookUri | 예 | Hello runbook에 대 한 hello webhook의 Uri입니다. |
| Expiry | 아니요 | Hello 수정 된 날짜와 시간에 만료 됩니다. |

#### <a name="webhook-actions"></a>웹후크 작업

Webhook 작업 URL을 호출 하 여 선택적으로 전송 되는 페이로드 toobe 제공 하는 프로세스를 시작 합니다. Azure 자동화 runbook 이외의 프로세스를 호출할 수 있는 webhook에 대 한 보관 점을 제외 하 고 서로 유사한 tooRemediation 동작입니다. 또한 hello 페이로드 배달 toobe toohello 원격 프로세스를 제공 하는 중 추가 옵션을 제공 합니다.

결제 경고가 됩니다 여 webhook을 사용할지를 호출 하는 경우의 형식과 동작 리소스는 필요 **Webhook** 더하기 toohello에 **경고** 작업 리소스입니다.  

    {
      "name": "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Webhook').Name)]",
      "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions/",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
      ],
      "properties": {
        "etag": "*",
        "type": "[variables('Alert').Webhook.Type]",
        "name": "[variables('Alert').Webhook.Name]",
        "webhookUri": "[variables('Alert').Webhook.webhookUri]",
        "customPayload": "[variables('Alert').Webhook.CustomPayLoad]"
      }
    }

다음 표에서 hello Webhook 작업 리소스에 대 한 hello 속성 설명 합니다.

| 요소 이름 | 필수 | 설명 |
|:--|:--|:--|
| type | 예 | Hello 작업 형식입니다.  웹후크 작업의 **웹후크**가 됩니다. |
| name | 예 | Hello 동작에 대 한 표시 이름입니다.  Hello 콘솔에 표시 되지 않습니다. |
| wehookUri | 예 | Hello webhook에 대 한 Uri입니다. |
| customPayload | 아니요 | 사용자 지정 페이로드 toobe toohello webhook을 전송 합니다. hello 형식 어떤 hello webhook 예상에 따라 달라 집니다. |




## <a name="sample"></a>샘플

다음은 hello 다음 리소스를 포함 하는 포함 하는 솔루션의 샘플입니다.

- 저장된 검색
- 일정
- 경고 작업
- 웹후크 작업

샘플 사용 하 여 hello [표준 솔루션 매개 변수](operations-management-suite-solutions-solution-file.md#parameters) 와 솔루션에 일반적으로 사용 되는 변수 hello 리소스 정의에서 toohardcoding 값을 반대로 합니다.

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0",
        "parameters": {
          "workspaceName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Log Analytics workspace"
            }
          },
          "accountName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Automation account"
            }
          },
          "workspaceregionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Log Analytics workspace"
            }
          },
          "regionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Automation account"
            }
          },
          "pricingTier": {
            "type": "string",
            "metadata": {
              "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
          },
          "recipients": {
            "type": "string",
            "metadata": {
              "Description": "List of recipients for hello email alert separated by semicolon"
            }
          }
        },
        "variables": {
          "SolutionName": "MySolution",
          "SolutionVersion": "1.0",
          "SolutionPublisher": "Contoso",
          "ProductName": "SampleSolution",
    
          "LogAnalyticsApiVersion": "2015-11-01-preview",
    
          "MySearch": {
            "displayName": "Error records by hour",
            "query": "Type=MyRecord_CL | measure avg(Rating_d) by Instance_s interval 60minutes",
            "category": "Samples",
            "name": "Samples-Count of data"
          },
          "MyAlert": {
            "Name": "[toLower(concat('myalert-',uniqueString(resourceGroup().id, deployment().name)))]",
            "DisplayName": "My alert rule",
            "Description": "Sample alert.  Fires when 3 error records found over hour interval.",
            "Severity": "Critical",
            "ThresholdOperator": "gt",
            "ThresholdValue": 3,
            "Schedule": {
              "Name": "[toLower(concat('myschedule-',uniqueString(resourceGroup().id, deployment().name)))]",
              "Interval": 15,
              "TimeSpan": 60
            },
            "MetricsTrigger": {
              "TriggerCondition": "Consecutive",
              "Operator": "gt",
              "Value": 3
            },
            "ThrottleMinutes": 60,
            "Notification": {
              "Recipients": [
                "[parameters('recipients')]"
              ],
              "Subject": "Sample alert"
            },
            "Remediation": {
              "RunbookName": "MyRemediationRunbook",
              "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=TluBFH3GpX4IEAnFoImoAWLTULkjD%2bTS0yscyrr7ogw%3d"
            },
            "Webhook": {
              "Name": "MyWebhook",
              "Uri": "https://MyService.com/webhook",
              "Payload": "{\"field1\":\"value1\",\"field2\":\"value2\"}"
            }
          }
        },
        "resources": [
          {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
            "location": "[parameters('workspaceRegionId')]",
            "tags": { },
            "type": "Microsoft.OperationsManagement/solutions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
            ],
            "properties": {
              "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
              "referencedResources": [
              ],
              "containedResources": [
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
              ]
            },
            "plan": {
              "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
              "Version": "[variables('SolutionVersion')]",
              "product": "[variables('ProductName')]",
              "publisher": "[variables('SolutionPublisher')]",
              "promotionCode": ""
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [ ],
            "tags": { },
            "properties": {
              "etag": "*",
              "query": "[variables('MySearch').query]",
              "displayName": "[variables('MySearch').displayName]",
              "category": "[variables('MySearch').category]"
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name)]"
            ],
            "properties": {
              "etag": "*",
              "interval": "[variables('MyAlert').Schedule.Interval]",
              "queryTimeSpan": "[variables('MyAlert').Schedule.TimeSpan]",
              "enabled": true
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/',  variables('MyAlert').Schedule.Name, '/',  variables('MyAlert').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/',  variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Alert",
              "Name": "[variables('MyAlert').DisplayName]",
              "Description": "[variables('MyAlert').Description]",
              "Severity": "[variables('MyAlert').Severity]",
              "Threshold": {
                "Operator": "[variables('MyAlert').ThresholdOperator]",
                "Value": "[variables('MyAlert').ThresholdValue]",
                "MetricsTrigger": {
                  "TriggerCondition": "[variables('MyAlert').MetricsTrigger.TriggerCondition]",
                  "Operator": "[variables('MyAlert').MetricsTrigger.Operator]",
                  "Value": "[variables('MyAlert').MetricsTrigger.Value]"
                }
              },
              "Throttling": {
                "DurationInMinutes": "[variables('MyAlert').ThrottleMinutes]"
              },
              "EmailNotification": {
                "Recipients": "[variables('MyAlert').Notification.Recipients]",
                "Subject": "[variables('MyAlert').Notification.Subject]",
                "Attachment": "None"
              },
              "Remediation": {
                "RunbookName": "[variables('MyAlert').Remediation.RunbookName]",
                "WebhookUri": "[variables('MyAlert').Remediation.WebhookUri]"
              }
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name, '/', variables('MyAlert').Webhook.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]",
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name, '/actions/',variables('MyAlert').Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Webhook",
              "Name": "[variables('MyAlert').Webhook.Name]",
              "WebhookUri": "[variables('MyAlert').Webhook.Uri]",
              "CustomPayload": "[variables('MyAlert').Webhook.Payload]"
            }
          }
        ]
    }


다음 매개 변수 파일 hello이이 솔루션에 대 한 샘플 값을 제공 합니다.

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "workspacename": {
                "value": "myWorkspace"
            },
            "accountName": {
                "value": "myAccount"
            },
            "workspaceregionId": {
                "value": "East US"
            },
            "regionId": {
                "value": "East US 2"
            },
            "pricingTier": {
                "value": "Free"
            },
            "recipients": {
                "value": "recipient1@contoso.com;recipient2@contoso.com"
            }
        }
    }


## <a name="next-steps"></a>다음 단계
* [뷰 추가](operations-management-suite-solutions-resources-views.md) tooyour 관리 솔루션입니다.
* [자동화 runbook 및 기타 리소스를 추가](operations-management-suite-solutions-resources-automation.md) tooyour 관리 솔루션입니다.

