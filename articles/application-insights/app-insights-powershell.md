---
title: "PowerShell 사용 하 여 Azure 응용 프로그램 정보 aaaAutomate | Microsoft Docs"
description: "Azure Resource Manager 템플릿을 사용하여 PowerShell에서 리소스, 경고 및 가용성 테스트 생성을 자동화합니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 9f73b87f-be63-4847-88c8-368543acad8b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/02/2017
ms.author: bwren
ms.openlocfilehash: ebd336eafba58a690a0e8ffbd1c74f7e93dbb682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
#  <a name="create-application-insights-resources-using-powershell"></a>PowerShell을 사용하여 Application Insights 리소스 만들기
이 문서에서는 생성 및 업데이트 tooautomate hello 하는 방법을 [Application Insights](app-insights-overview.md) Azure 리소스 관리를 사용 하 여 자동으로 리소스입니다. 예를 들어 빌드 프로세스의 일부로 이 작업을 수행할 수 있습니다. Hello 기본 Application Insights 리소스를 함께 만들 수 있습니다 [가용성 웹 테스트](app-insights-monitor-web-app-availability.md)를 설정, [경고](app-insights-alerts.md)설정 hello, [가격 체계](app-insights-pricing.md)를 만들고 다른 Azure 리소스입니다.

이러한 리소스에 대 한 JSON 서식 파일은 키 toocreating hello [Azure 리소스 관리자](../azure-resource-manager/powershell-azure-resource-manager.md)합니다. Hello 절차는 간단히 말하면: 기존 리소스;의 hello JSON 정의 다운로드 예: 이름; 특정 값을 매개 변수화 고 toocreate 새 리소스를 원할 때마다 hello 서식 파일을 실행 하십시오. 여러 리소스를 함께, 예를 들어 다음 하나에 모든 단계 toocreate, 가용성 테스트, 경고 및 연속 내보내기에 대 한 저장소는 응용 프로그램 모니터를 패키지할 수 있습니다. 여기에 설명 hello 매개 변수화의 몇 가지 미묘한 toosome 가지가 있습니다.

## <a name="one-time-setup"></a>일 회 설정
아직 Azure 구독에서 PowerShell을 사용한 적이 없을 경우:

Toorun hello 스크립트 저장할 hello 머신에서 hello Azure Powershell 모듈을 설치 합니다.

1. [Microsoft 웹 플랫폼 설치 관리자(v5 이상)](http://www.microsoft.com/web/downloads/platform.aspx)를 설치합니다.
2. Microsoft Azure Powershell tooinstall 방법을 사용 합니다.

## <a name="create-an-azure-resource-manager-template"></a>Azure Resource Manager 템플릿 만들기
새 .json 파일을 만듭니다. 이 예제에서는 `template1.json`입니다. 아래 내용을 이 파일에 복사합니다.

```JSON
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "appName": {
                "type": "string",
                "metadata": {
                    "description": "Enter hello application name."
                }
            },
            "appType": {
                "type": "string",
                "defaultValue": "web",
                "allowedValues": [
                    "web",
                    "java",
                    "HockeyAppBridge",
                    "other"
                ],
                "metadata": {
                    "description": "Enter hello application type."
                }
            },
            "appLocation": {
                "type": "string",
                "defaultValue": "East US",
                "allowedValues": [
                    "South Central US",
                    "West Europe",
                    "East US",
                    "North Europe"
                ],
                "metadata": {
                    "description": "Enter hello application location."
                }
            },
            "priceCode": {
                "type": "int",
                "defaultValue": 1,
                "allowedValues": [
                    1,
                    2
                ],
                "metadata": {
                    "description": "1 = Basic, 2 = Enterprise"
                }
            },
            "dailyQuota": {
                "type": "int",
                "defaultValue": 100,
                "minValue": 1,
                "metadata": {
                    "description": "Enter daily quota in GB."
                }
            },
            "dailyQuotaResetTime": {
                "type": "int",
                "defaultValue": 24,
                "metadata": {
                    "description": "Enter daily quota reset hour in UTC (0 too23). Values outside hello range will get a random reset hour."
                }
            },
            "warningThreshold": {
                "type": "int",
                "defaultValue": 90,
                "minValue": 1,
                "maxValue": 100,
                "metadata": {
                    "description": "Enter hello % value of daily quota after which warning mail toobe sent. "
                }
            }
        },
        "variables": {
            "priceArray": [
                "Basic",
                "Application Insights Enterprise"
            ],
            "pricePlan": "[take(variables('priceArray'),parameters('priceCode'))]",
            "billingplan": "[concat(parameters('appName'),'/', variables('pricePlan')[0])]"
        },
        "resources": [
            {
                "type": "microsoft.insights/components",
                "kind": "[parameters('appType')]",
                "name": "[parameters('appName')]",
                "apiVersion": "2014-04-01",
                "location": "[parameters('appLocation')]",
                "tags": {},
                "properties": {
                    "ApplicationId": "[parameters('appName')]"
                },
                "dependsOn": []
            },
            {
                "name": "[variables('billingplan')]",
                "type": "microsoft.insights/components/CurrentBillingFeatures",
                "location": "[parameters('appLocation')]",
                "apiVersion": "2015-05-01",
                "dependsOn": [
                    "[resourceId('microsoft.insights/components', parameters('appName'))]"
                ],
                "properties": {
                    "CurrentBillingFeatures": "[variables('pricePlan')]",
                    "DataVolumeCap": {
                        "Cap": "[parameters('dailyQuota')]",
                        "WarningThreshold": "[parameters('warningThreshold')]",
                        "ResetTime": "[parameters('dailyQuotaResetTime')]"
                    }
                }
            }
        ]
    }
```



## <a name="create-application-insights-resources"></a>Application Insights 리소스 만들기
1. PowerShell에서 tooAzure 로그인:
   
    `Login-AzureRmAccount`
2. 다음과 같은 명령을 실행합니다.
   
    ```PS
   
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -appName myNewApp

    ``` 
   
   * `-ResourceGroupName`toocreate hello 새 리소스를 원하는 hello 그룹입니다.
   * `-TemplateFile`사용자 지정 매개 변수 hello 하기 전에 발생 해야 합니다.
   * `-appName`hello 리소스 toocreate의 hello 이름입니다.

다른 매개 변수를 추가할 수 있습니다-hello 템플릿의 hello 매개 변수 섹션에서 해당 설명을 찾을 수 있습니다.

## <a name="tooget-hello-instrumentation-key"></a>tooget hello 계측 키
응용 프로그램 리소스를 만든 후 hello 계측 키를 해도 됩니다. 

```PS
    $resource = Find-AzureRmResource -ResourceNameEquals "<YOUR APP NAME>" -ResourceType "Microsoft.Insights/components"
    $details = Get-AzureRmResource -ResourceId $resource.ResourceId
    $ikey = $details.Properties.InstrumentationKey
```


<a id="price"></a>
## <a name="set-hello-price-plan"></a>집합 hello 가격 계획

Hello를 설정할 수 있습니다 [가격 계획](app-insights-pricing.md)합니다.

toocreate hello Enterprise 가격 계획에 위의 hello 템플릿을 사용 하는 응용 프로그램 리소스:

```PS
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -priceCode 2 `
               -appName myNewApp
```

|priceCode|계획|
|---|---|
|1|Basic|
|2|Enterprise|

* 만 toouse hello 기본 기본 가격 계획 들어 hello 템플릿에서 hello CurrentBillingFeatures 리소스를 생략할 수 있습니다.
* Hello 구성 요소 리소스를 만든 후 toochange hello 가격 계획을 하려는 경우에 hello "microsoft.insights/components" 리소스를 생략 하는 서식 파일을 사용할 수 있습니다. 또한 hello 생략 `dependsOn` 리소스 청구 hello에서 노드. 

tooverify는 업데이트 된 가격 계획 hello를 hello 브라우저에서 "기능 + 가격" hello 블레이드를 확인 합니다. **Hello 브라우저 보기를 새로 고칠** toomake hello 최신 상태를 볼 수 있어야 합니다.



## <a name="add-a-metric-alert"></a>메트릭 경고 추가

hello에 메트릭 경고를 tooset 동일한 hello 템플릿 파일에 다음과 같은 코드를 병합 하면 응용 프로그램 리소스로 시간:

```JSON
{
    parameters: { ... // existing parameters ...
            "responseTime": {
              "type": "int",
              "defaultValue": 3,
              "minValue": 1,
              "metadata": {
                "description": "Enter response time threshold in seconds."
              }
    },
    variables: { ... // existing variables ...
      // Alert names must be unique within resource group.
      "responseAlertName": "[concat('ResponseTime-', toLower(parameters('appName')))]"
    }, 
    resources: { ... // existing resources ...
     {
      //
      // Metric alert on response time
      //
      "name": "[variables('responseAlertName')]",
      "type": "Microsoft.Insights/alertrules",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]",
      // Ensure this resource is created after hello app resource:
      "dependsOn": [
        "[resourceId('Microsoft.Insights/components', parameters('appName'))]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Insights/components', parameters('appName')))]": "Resource"
      },
      "properties": {
        "name": "[variables('responseAlertName')]",
        "description": "response time alert",
        "isEnabled": true,
        "condition": {
          "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.ThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
          "odata.type": "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
          "dataSource": {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[resourceId('microsoft.insights/components', parameters('appName'))]",
            "metricName": "request.duration"
          },
          "threshold": "[parameters('responseTime')]", //seconds
          "windowSize": "PT15M" // Take action if changed state for 15 minutes
        },
        "actions": [
          {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
            "sendToServiceOwners": true,
            "customEmails": []
          }
        ]
      }
    }
}
```

Hello 서식 파일을 호출 하는 경우이 매개 변수를 선택적으로 추가할 수 있습니다.

    `-responseTime 2`

물론 다른 필드를 매개 변수화할 수 있습니다. 

hello 형식 이름 및 기타 경고 규칙의 구성 정보 toofind 규칙을 수동으로 만들고 검사에서 [Azure 리소스 관리자](https://resources.azure.com/)합니다. 


## <a name="add-an-availability-test"></a>가용성 테스트 추가

이 예제는 ping 테스트 (tootest 단일 페이지).  

**두 가지** 가용성 테스트에서: hello 테스트 자체를 및 실패를 알려 주는 hello 경고 합니다.

Hello 앱을 만드는 hello 템플릿 파일에 코드를 다음 hello를 병합 합니다.

```JSON
{
    parameters: { ... // existing parameters here ...
      "pingURL": { "type": "string" },
      "pingText": { "type": "string" , defaultValue: ""}
    },
    variables: { ... // existing variables here ...
      "pingTestName":"[concat('PingTest-', toLower(parameters('appName')))]",
      "pingAlertRuleName": "[concat('PingAlert-', toLower(parameters('appName')), '-', subscription().subscriptionId)]"
    },
    resources: { ... // existing resources here ...
    { //
      // Availability test: part 1 configures hello test
      //
      "name": "[variables('pingTestName')]",
      "type": "Microsoft.Insights/webtests",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]",
      // Ensure this is created after hello app resource:
      "dependsOn": [
        "[resourceId('Microsoft.Insights/components', parameters('appName'))]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Insights/components', parameters('appName')))]": "Resource"
      },
      "properties": {
        "Name": "[variables('pingTestName')]",
        "Description": "Basic ping test",
        "Enabled": true,
        "Frequency": 900, // 15 minutes
        "Timeout": 120, // 2 minutes
        "Kind": "ping", // single URL test
        "RetryEnabled": true,
        "Locations": [
          {
            "Id": "us-va-ash-azr"
          },
          {
            "Id": "emea-nl-ams-azr"
          },
          {
            "Id": "apac-jp-kaw-edge"
          }
        ],
        "Configuration": {
          "WebTest": "[concat('<WebTest   Name=\"', variables('pingTestName'), '\"   Enabled=\"True\"         CssProjectStructure=\"\"    CssIteration=\"\"  Timeout=\"120\"  WorkItemIds=\"\"         xmlns=\"http://microsoft.com/schemas/VisualStudio/TeamTest/2010\"         Description=\"\"  CredentialUserName=\"\"  CredentialPassword=\"\"         PreAuthenticate=\"True\"  Proxy=\"default\"  StopOnError=\"False\"         RecordedResultFile=\"\"  ResultsLocale=\"\">  <Items>  <Request Method=\"GET\"    Version=\"1.1\"  Url=\"', parameters('Url'),   '\" ThinkTime=\"0\"  Timeout=\"300\" ParseDependentRequests=\"True\"         FollowRedirects=\"True\" RecordResult=\"True\" Cache=\"False\"         ResponseTimeGoal=\"0\"  Encoding=\"utf-8\"  ExpectedHttpStatusCode=\"200\"         ExpectedResponseUrl=\"\" ReportingName=\"\" IgnoreHttpStatusCode=\"False\" />        </Items>  <ValidationRules> <ValidationRule  Classname=\"Microsoft.VisualStudio.TestTools.WebTesting.Rules.ValidationRuleFindText, Microsoft.VisualStudio.QualityTools.WebTestFramework, Version=10.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a\" DisplayName=\"Find Text\"         Description=\"Verifies hello existence of hello specified text in hello response.\"         Level=\"High\"  ExectuionOrder=\"BeforeDependents\">  <RuleParameters>        <RuleParameter Name=\"FindText\" Value=\"',   parameters('pingText'), '\" />  <RuleParameter Name=\"IgnoreCase\" Value=\"False\" />  <RuleParameter Name=\"UseRegularExpression\" Value=\"False\" />  <RuleParameter Name=\"PassIfTextFound\" Value=\"True\" />  </RuleParameters> </ValidationRule>  </ValidationRules>  </WebTest>')]"
        },
        "SyntheticMonitorId": "[variables('pingTestName')]"
      }
    },

    {
      //
      // Availability test: part 2, hello alert rule
      //
      "name": "[variables('pingAlertRuleName')]",
      "type": "Microsoft.Insights/alertrules",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]", 
      "dependsOn": [
        "[resourceId('Microsoft.Insights/webtests', variables('pingTestName'))]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Insights/components', parameters('appName')))]": "Resource",
        "[concat('hidden-link:', resourceId('Microsoft.Insights/webtests', variables('pingTestName')))]": "Resource"
      },
      "properties": {
        "name": "[variables('pingAlertRuleName')]",
        "description": "alert for web test",
        "isEnabled": true,
        "condition": {
          "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.LocationThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
          "odata.type": "Microsoft.Azure.Management.Insights.Models.LocationThresholdRuleCondition",
          "dataSource": {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[resourceId('microsoft.insights/webtests', variables('pingTestName'))]",
            "metricName": "GSMT_AvRaW"
          },
          "windowSize": "PT15M", // Take action if changed state for 15 minutes
          "failedLocationCount": 2
        },
        "actions": [
          {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
            "sendToServiceOwners": true,
            "customEmails": []
          }
        ]
      }
    }
}
```

다른 테스트 위치 또는 보다 복잡 한 웹 테스트의 tooautomate hello 생성에 대 한 toodiscover hello 코드 예가 수동으로 만들고 다음 hello 코드에서 매개 변수화 [Azure 리소스 관리자](https://resources.azure.com/)합니다.

## <a name="add-more-resources"></a>리소스 추가

어떤 종류의 다른 리소스의 tooautomate hello 만들기 예제를 수동으로 만들 복사 하 고 해당 코드에서 매개 변수화 [Azure 리소스 관리자](https://resources.azure.com/)합니다. 

1. [Azure 리소스 관리자](https://resources.azure.com/)를 엽니다. 아래쪽 탐색 `subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components`, tooyour 응용 프로그램 리소스입니다. 
   
    ![Azure 리소스 탐색기에서 탐색](./media/app-insights-powershell/01.png)
   
    *구성 요소* hello 기본 Application Insights 리소스가 응용 프로그램을 표시 합니다. Hello 관련 경고 규칙 및 가용성 웹 테스트에 대 한 별도 리소스가 있습니다.
2. 복사 hello hello 적절 한 위치에 hello 구성 요소는 JSON에 `template1.json`합니다.
3. 다음 속성을 삭제합니다.
   
   * `id`
   * `InstrumentationKey`
   * `CreationDate`
   * `TenantId`
4. Hello webtests 및 alertrules 섹션 열고 개별 항목에 대 한 JSON hello 서식 파일에 복사 합니다. (Hello webtests 또는 alertrules 노드에서 복사 하지 않음: 그 아래 hello 항목으로 이동 합니다.)
   
    각 웹 테스트에는 관련된 경고 규칙을 toocopy 그중에서 갖도록 합니다.
   
    메트릭에 대한 경고를 포함할 수도 있습니다. [메트릭 이름](app-insights-powershell-alerts.md#metric-names)
5. 각 리소스에 다음 줄을 삽입합니다.
   
    `"apiVersion": "2015-05-01",`

### <a name="parameterize-hello-template"></a>Hello 서식 파일을 매개 변수화
이제 이름이 tooreplace hello 특정 매개 변수를 사용 합니다. 너무[서식 파일을 매개 변수화](../azure-resource-manager/resource-group-authoring-templates.md)를 사용 하 여 식을 작성 하는 [도우미 함수 집합이](../azure-resource-manager/resource-group-template-functions.md)합니다. 

문자열의 일부를 매개 변수화, 따라서 키를 사용할 수 없습니다 `concat()` toobuild 문자열입니다.

다음은 예제 toomake hello 동의어인 대체 합니다. 각 대체가 여러 번 발생합니다. 템플릿에서 다른 사항이 필요할 수 있습니다. 이러한 예제는 hello 서식 파일의 hello 위쪽 hello 매개 변수 및 변수 정의 사용 합니다.

| find | 대체 |
| --- | --- |
| `"hidden-link:/subscriptions/.../components/MyAppName"` |`"[concat('hidden-link:',`<br/>` resourceId('microsoft.insights/components',` <br/> ` parameters('appName')))]"` |
| `"/subscriptions/.../alertrules/myAlertName-myAppName-subsId",` |`"[resourceId('Microsoft.Insights/alertrules', variables('alertRuleName'))]",` |
| `"/subscriptions/.../webtests/myTestName-myAppName",` |`"[resourceId('Microsoft.Insights/webtests', parameters('webTestName'))]",` |
| `"myWebTest-myAppName"` |`"[variables(testName)]"'` |
| `"myTestName-myAppName-subsId"` |`"[variables('alertRuleName')]"` |
| `"myAppName"` |`"[parameters('appName')]"` |
| `"myappname"` (소문자) |`"[toLower(parameters('appName'))]"` |
| `"<WebTest Name=\"myWebTest\" ...`<br/>` Url=\"http://fabrikam.com/home\" ...>"` |`[concat('<WebTest Name=\"',` <br/> `parameters('webTestName'),` <br/> `'\" ... Url=\"', parameters('Url'),` <br/> `'\"...>')]"`<br/>GUID 및 ID를 삭제합니다. |

### <a name="set-dependencies-between-hello-resources"></a>Hello 리소스 간의 종속성을 설정
Azure는 hello 리소스 엄격한 순서를 설정 해야 합니다. hello 다음 시작 되기 전에 하나의 설치가 완료 된 있는지 toomake 종속성 줄을 추가 합니다.

* Hello 사용 가능한 리소스를 테스트:
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/components', parameters('appName'))]"],`
* Hello 가용성 테스트에 대 한 경고 리소스:
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/webtests', variables('testName'))]"],`



## <a name="next-steps"></a>다음 단계
다른 자동화 문서:

* [Application Insights 리소스 만들기](app-insights-powershell-script-create-resource.md) - 템플릿을 사용하지 않는 빠른 방법입니다.
* [경고 설정](app-insights-powershell-alerts.md)
* [웹 테스트 만들기](https://azure.microsoft.com/blog/creating-a-web-test-alert-programmatically-with-application-insights/)
* [Azure 진단 tooApplication Insights 보내기](app-insights-powershell-azure-diagnostics.md)
* [GitHub에서 tooAzure 배포](http://blogs.msdn.com/b/webdev/archive/2015/09/16/deploy-to-azure-from-github-with-application-insights.aspx)
* [릴리스 주석 만들기](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1)

