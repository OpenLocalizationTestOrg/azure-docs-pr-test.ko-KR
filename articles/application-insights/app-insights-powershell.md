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
#  <a name="create-application-insights-resources-using-powershell"></a><span data-ttu-id="06bb4-103">PowerShell을 사용하여 Application Insights 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="06bb4-103">Create Application Insights resources using PowerShell</span></span>
<span data-ttu-id="06bb4-104">이 문서에서는 생성 및 업데이트 tooautomate hello 하는 방법을 [Application Insights](app-insights-overview.md) Azure 리소스 관리를 사용 하 여 자동으로 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-104">This article shows you how tooautomate hello creation and update of [Application Insights](app-insights-overview.md) resources automatically by using Azure Resource Management.</span></span> <span data-ttu-id="06bb4-105">예를 들어 빌드 프로세스의 일부로 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-105">You might, for example, do so as part of a build process.</span></span> <span data-ttu-id="06bb4-106">Hello 기본 Application Insights 리소스를 함께 만들 수 있습니다 [가용성 웹 테스트](app-insights-monitor-web-app-availability.md)를 설정, [경고](app-insights-alerts.md)설정 hello, [가격 체계](app-insights-pricing.md)를 만들고 다른 Azure 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-106">Along with hello basic Application Insights resource, you can create [availability web tests](app-insights-monitor-web-app-availability.md), set up [alerts](app-insights-alerts.md), set hello [pricing scheme](app-insights-pricing.md), and create other Azure resources.</span></span>

<span data-ttu-id="06bb4-107">이러한 리소스에 대 한 JSON 서식 파일은 키 toocreating hello [Azure 리소스 관리자](../azure-resource-manager/powershell-azure-resource-manager.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-107">hello key toocreating these resources is JSON templates for [Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span> <span data-ttu-id="06bb4-108">Hello 절차는 간단히 말하면: 기존 리소스;의 hello JSON 정의 다운로드 예: 이름; 특정 값을 매개 변수화 고 toocreate 새 리소스를 원할 때마다 hello 서식 파일을 실행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="06bb4-108">In a nutshell, hello procedure is: download hello JSON definitions of existing resources; parameterize certain values such as names; and then run hello template whenever you want toocreate a new resource.</span></span> <span data-ttu-id="06bb4-109">여러 리소스를 함께, 예를 들어 다음 하나에 모든 단계 toocreate, 가용성 테스트, 경고 및 연속 내보내기에 대 한 저장소는 응용 프로그램 모니터를 패키지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-109">You can package several resources together, toocreate them all in one go - for example, an app monitor with availability tests, alerts, and storage for continuous export.</span></span> <span data-ttu-id="06bb4-110">여기에 설명 hello 매개 변수화의 몇 가지 미묘한 toosome 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-110">There are some subtleties toosome of hello parameterizations, which we'll explain here.</span></span>

## <a name="one-time-setup"></a><span data-ttu-id="06bb4-111">일 회 설정</span><span class="sxs-lookup"><span data-stu-id="06bb4-111">One-time setup</span></span>
<span data-ttu-id="06bb4-112">아직 Azure 구독에서 PowerShell을 사용한 적이 없을 경우:</span><span class="sxs-lookup"><span data-stu-id="06bb4-112">If you haven't used PowerShell with your Azure subscription before:</span></span>

<span data-ttu-id="06bb4-113">Toorun hello 스크립트 저장할 hello 머신에서 hello Azure Powershell 모듈을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-113">Install hello Azure Powershell module on hello machine where you want toorun hello scripts:</span></span>

1. <span data-ttu-id="06bb4-114">[Microsoft 웹 플랫폼 설치 관리자(v5 이상)](http://www.microsoft.com/web/downloads/platform.aspx)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-114">Install [Microsoft Web Platform Installer (v5 or higher)](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
2. <span data-ttu-id="06bb4-115">Microsoft Azure Powershell tooinstall 방법을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-115">Use it tooinstall Microsoft Azure Powershell.</span></span>

## <a name="create-an-azure-resource-manager-template"></a><span data-ttu-id="06bb4-116">Azure Resource Manager 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="06bb4-116">Create an Azure Resource Manager template</span></span>
<span data-ttu-id="06bb4-117">새 .json 파일을 만듭니다. 이 예제에서는 `template1.json`입니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-117">Create a new .json file - let's call it `template1.json` in this example.</span></span> <span data-ttu-id="06bb4-118">아래 내용을 이 파일에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-118">Copy this content into it:</span></span>

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



## <a name="create-application-insights-resources"></a><span data-ttu-id="06bb4-119">Application Insights 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="06bb4-119">Create Application Insights resources</span></span>
1. <span data-ttu-id="06bb4-120">PowerShell에서 tooAzure 로그인:</span><span class="sxs-lookup"><span data-stu-id="06bb4-120">In PowerShell, sign in tooAzure:</span></span>
   
    `Login-AzureRmAccount`
2. <span data-ttu-id="06bb4-121">다음과 같은 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-121">Run a command like this:</span></span>
   
    ```PS
   
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -appName myNewApp

    ``` 
   
   * <span data-ttu-id="06bb4-122">`-ResourceGroupName`toocreate hello 새 리소스를 원하는 hello 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-122">`-ResourceGroupName` is hello group where you want toocreate hello new resources.</span></span>
   * <span data-ttu-id="06bb4-123">`-TemplateFile`사용자 지정 매개 변수 hello 하기 전에 발생 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-123">`-TemplateFile` must occur before hello custom parameters.</span></span>
   * <span data-ttu-id="06bb4-124">`-appName`hello 리소스 toocreate의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-124">`-appName` hello name of hello resource toocreate.</span></span>

<span data-ttu-id="06bb4-125">다른 매개 변수를 추가할 수 있습니다-hello 템플릿의 hello 매개 변수 섹션에서 해당 설명을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-125">You can add other parameters - you'll find their descriptions in hello parameters section of hello template.</span></span>

## <a name="tooget-hello-instrumentation-key"></a><span data-ttu-id="06bb4-126">tooget hello 계측 키</span><span class="sxs-lookup"><span data-stu-id="06bb4-126">tooget hello instrumentation key</span></span>
<span data-ttu-id="06bb4-127">응용 프로그램 리소스를 만든 후 hello 계측 키를 해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-127">After creating an application resource, you'll want hello instrumentation key:</span></span> 

```PS
    $resource = Find-AzureRmResource -ResourceNameEquals "<YOUR APP NAME>" -ResourceType "Microsoft.Insights/components"
    $details = Get-AzureRmResource -ResourceId $resource.ResourceId
    $ikey = $details.Properties.InstrumentationKey
```


<a id="price"></a>
## <a name="set-hello-price-plan"></a><span data-ttu-id="06bb4-128">집합 hello 가격 계획</span><span class="sxs-lookup"><span data-stu-id="06bb4-128">Set hello price plan</span></span>

<span data-ttu-id="06bb4-129">Hello를 설정할 수 있습니다 [가격 계획](app-insights-pricing.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-129">You can set hello [price plan](app-insights-pricing.md).</span></span>

<span data-ttu-id="06bb4-130">toocreate hello Enterprise 가격 계획에 위의 hello 템플릿을 사용 하는 응용 프로그램 리소스:</span><span class="sxs-lookup"><span data-stu-id="06bb4-130">toocreate an app resource with hello Enterprise price plan, using hello template above:</span></span>

```PS
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -priceCode 2 `
               -appName myNewApp
```

|<span data-ttu-id="06bb4-131">priceCode</span><span class="sxs-lookup"><span data-stu-id="06bb4-131">priceCode</span></span>|<span data-ttu-id="06bb4-132">계획</span><span class="sxs-lookup"><span data-stu-id="06bb4-132">plan</span></span>|
|---|---|
|<span data-ttu-id="06bb4-133">1</span><span class="sxs-lookup"><span data-stu-id="06bb4-133">1</span></span>|<span data-ttu-id="06bb4-134">Basic</span><span class="sxs-lookup"><span data-stu-id="06bb4-134">Basic</span></span>|
|<span data-ttu-id="06bb4-135">2</span><span class="sxs-lookup"><span data-stu-id="06bb4-135">2</span></span>|<span data-ttu-id="06bb4-136">Enterprise</span><span class="sxs-lookup"><span data-stu-id="06bb4-136">Enterprise</span></span>|

* <span data-ttu-id="06bb4-137">만 toouse hello 기본 기본 가격 계획 들어 hello 템플릿에서 hello CurrentBillingFeatures 리소스를 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-137">If you only want toouse hello default Basic price plan, you can omit hello CurrentBillingFeatures resource from hello template.</span></span>
* <span data-ttu-id="06bb4-138">Hello 구성 요소 리소스를 만든 후 toochange hello 가격 계획을 하려는 경우에 hello "microsoft.insights/components" 리소스를 생략 하는 서식 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-138">If you want toochange hello price plan after hello component resource has been created, you can use a template that omits hello "microsoft.insights/components" resource.</span></span> <span data-ttu-id="06bb4-139">또한 hello 생략 `dependsOn` 리소스 청구 hello에서 노드.</span><span class="sxs-lookup"><span data-stu-id="06bb4-139">Also, omit hello `dependsOn` node from hello billing resource.</span></span> 

<span data-ttu-id="06bb4-140">tooverify는 업데이트 된 가격 계획 hello를 hello 브라우저에서 "기능 + 가격" hello 블레이드를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-140">tooverify hello updated price plan, look at hello "Features+pricing" blade in hello browser.</span></span> <span data-ttu-id="06bb4-141">**Hello 브라우저 보기를 새로 고칠** toomake hello 최신 상태를 볼 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-141">**Refresh hello browser view** toomake sure you see hello latest state.</span></span>



## <a name="add-a-metric-alert"></a><span data-ttu-id="06bb4-142">메트릭 경고 추가</span><span class="sxs-lookup"><span data-stu-id="06bb4-142">Add a metric alert</span></span>

<span data-ttu-id="06bb4-143">hello에 메트릭 경고를 tooset 동일한 hello 템플릿 파일에 다음과 같은 코드를 병합 하면 응용 프로그램 리소스로 시간:</span><span class="sxs-lookup"><span data-stu-id="06bb4-143">tooset up a metric alert at hello same time as your app resource, merge code like this into hello template file:</span></span>

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

<span data-ttu-id="06bb4-144">Hello 서식 파일을 호출 하는 경우이 매개 변수를 선택적으로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-144">When you invoke hello template, you can optionally add this parameter:</span></span>

    `-responseTime 2`

<span data-ttu-id="06bb4-145">물론 다른 필드를 매개 변수화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-145">You can of course parameterize other fields.</span></span> 

<span data-ttu-id="06bb4-146">hello 형식 이름 및 기타 경고 규칙의 구성 정보 toofind 규칙을 수동으로 만들고 검사에서 [Azure 리소스 관리자](https://resources.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-146">toofind out hello type names and configuration details of other alert rules, create a rule manually and then inspect it in [Azure Resource Manager](https://resources.azure.com/).</span></span> 


## <a name="add-an-availability-test"></a><span data-ttu-id="06bb4-147">가용성 테스트 추가</span><span class="sxs-lookup"><span data-stu-id="06bb4-147">Add an availability test</span></span>

<span data-ttu-id="06bb4-148">이 예제는 ping 테스트 (tootest 단일 페이지).</span><span class="sxs-lookup"><span data-stu-id="06bb4-148">This example is for a ping test (tootest a single page).</span></span>  

<span data-ttu-id="06bb4-149">**두 가지** 가용성 테스트에서: hello 테스트 자체를 및 실패를 알려 주는 hello 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-149">**There are two parts** in an availability test: hello test itself, and hello alert that notifies you of failures.</span></span>

<span data-ttu-id="06bb4-150">Hello 앱을 만드는 hello 템플릿 파일에 코드를 다음 hello를 병합 합니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-150">Merge hello following code into hello template file that creates hello app.</span></span>

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

<span data-ttu-id="06bb4-151">다른 테스트 위치 또는 보다 복잡 한 웹 테스트의 tooautomate hello 생성에 대 한 toodiscover hello 코드 예가 수동으로 만들고 다음 hello 코드에서 매개 변수화 [Azure 리소스 관리자](https://resources.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-151">toodiscover hello codes for other test locations, or tooautomate hello creation of more complex web tests, create an example manually and then parameterize hello code from [Azure Resource Manager](https://resources.azure.com/).</span></span>

## <a name="add-more-resources"></a><span data-ttu-id="06bb4-152">리소스 추가</span><span class="sxs-lookup"><span data-stu-id="06bb4-152">Add more resources</span></span>

<span data-ttu-id="06bb4-153">어떤 종류의 다른 리소스의 tooautomate hello 만들기 예제를 수동으로 만들 복사 하 고 해당 코드에서 매개 변수화 [Azure 리소스 관리자](https://resources.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-153">tooautomate hello creation of any other resource of any kind, create an example manually, and then copy and parameterize its code from [Azure Resource Manager](https://resources.azure.com/).</span></span> 

1. <span data-ttu-id="06bb4-154">[Azure 리소스 관리자](https://resources.azure.com/)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-154">Open [Azure Resource Manager](https://resources.azure.com/).</span></span> <span data-ttu-id="06bb4-155">아래쪽 탐색 `subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components`, tooyour 응용 프로그램 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-155">Navigate down through `subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components`, tooyour application resource.</span></span> 
   
    ![Azure 리소스 탐색기에서 탐색](./media/app-insights-powershell/01.png)
   
    <span data-ttu-id="06bb4-157">*구성 요소* hello 기본 Application Insights 리소스가 응용 프로그램을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-157">*Components* are hello basic Application Insights resources for displaying applications.</span></span> <span data-ttu-id="06bb4-158">Hello 관련 경고 규칙 및 가용성 웹 테스트에 대 한 별도 리소스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-158">There are separate resources for hello associated alert rules and availability web tests.</span></span>
2. <span data-ttu-id="06bb4-159">복사 hello hello 적절 한 위치에 hello 구성 요소는 JSON에 `template1.json`합니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-159">Copy hello JSON of hello component into hello appropriate place in `template1.json`.</span></span>
3. <span data-ttu-id="06bb4-160">다음 속성을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-160">Delete these properties:</span></span>
   
   * `id`
   * `InstrumentationKey`
   * `CreationDate`
   * `TenantId`
4. <span data-ttu-id="06bb4-161">Hello webtests 및 alertrules 섹션 열고 개별 항목에 대 한 JSON hello 서식 파일에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-161">Open hello webtests and alertrules sections and copy hello JSON for individual items into your template.</span></span> <span data-ttu-id="06bb4-162">(Hello webtests 또는 alertrules 노드에서 복사 하지 않음: 그 아래 hello 항목으로 이동 합니다.)</span><span class="sxs-lookup"><span data-stu-id="06bb4-162">(Don't copy from hello webtests or alertrules nodes: go into hello items under them.)</span></span>
   
    <span data-ttu-id="06bb4-163">각 웹 테스트에는 관련된 경고 규칙을 toocopy 그중에서 갖도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-163">Each web test has an associated alert rule, so you have toocopy both of them.</span></span>
   
    <span data-ttu-id="06bb4-164">메트릭에 대한 경고를 포함할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-164">You can also include alerts on metrics.</span></span> <span data-ttu-id="06bb4-165">[메트릭 이름](app-insights-powershell-alerts.md#metric-names)</span><span class="sxs-lookup"><span data-stu-id="06bb4-165">[Metric names](app-insights-powershell-alerts.md#metric-names).</span></span>
5. <span data-ttu-id="06bb4-166">각 리소스에 다음 줄을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-166">Insert this line in each resource:</span></span>
   
    `"apiVersion": "2015-05-01",`

### <a name="parameterize-hello-template"></a><span data-ttu-id="06bb4-167">Hello 서식 파일을 매개 변수화</span><span class="sxs-lookup"><span data-stu-id="06bb4-167">Parameterize hello template</span></span>
<span data-ttu-id="06bb4-168">이제 이름이 tooreplace hello 특정 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-168">Now you have tooreplace hello specific names with parameters.</span></span> <span data-ttu-id="06bb4-169">너무[서식 파일을 매개 변수화](../azure-resource-manager/resource-group-authoring-templates.md)를 사용 하 여 식을 작성 하는 [도우미 함수 집합이](../azure-resource-manager/resource-group-template-functions.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-169">too[parameterize a template](../azure-resource-manager/resource-group-authoring-templates.md), you write expressions using a [set of helper functions](../azure-resource-manager/resource-group-template-functions.md).</span></span> 

<span data-ttu-id="06bb4-170">문자열의 일부를 매개 변수화, 따라서 키를 사용할 수 없습니다 `concat()` toobuild 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-170">You can't parameterize just part of a string, so use `concat()` toobuild strings.</span></span>

<span data-ttu-id="06bb4-171">다음은 예제 toomake hello 동의어인 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-171">Here are examples of hello substitutions you'll want toomake.</span></span> <span data-ttu-id="06bb4-172">각 대체가 여러 번 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-172">There are several occurrences of each substitution.</span></span> <span data-ttu-id="06bb4-173">템플릿에서 다른 사항이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-173">You might need others in your template.</span></span> <span data-ttu-id="06bb4-174">이러한 예제는 hello 서식 파일의 hello 위쪽 hello 매개 변수 및 변수 정의 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-174">These examples use hello parameters and variables we defined at hello top of hello template.</span></span>

| <span data-ttu-id="06bb4-175">find</span><span class="sxs-lookup"><span data-stu-id="06bb4-175">find</span></span> | <span data-ttu-id="06bb4-176">대체</span><span class="sxs-lookup"><span data-stu-id="06bb4-176">replace with</span></span> |
| --- | --- |
| `"hidden-link:/subscriptions/.../components/MyAppName"` |`"[concat('hidden-link:',`<br/>` resourceId('microsoft.insights/components',` <br/> ` parameters('appName')))]"` |
| `"/subscriptions/.../alertrules/myAlertName-myAppName-subsId",` |`"[resourceId('Microsoft.Insights/alertrules', variables('alertRuleName'))]",` |
| `"/subscriptions/.../webtests/myTestName-myAppName",` |`"[resourceId('Microsoft.Insights/webtests', parameters('webTestName'))]",` |
| `"myWebTest-myAppName"` |`"[variables(testName)]"'` |
| `"myTestName-myAppName-subsId"` |`"[variables('alertRuleName')]"` |
| `"myAppName"` |`"[parameters('appName')]"` |
| <span data-ttu-id="06bb4-177">`"myappname"` (소문자)</span><span class="sxs-lookup"><span data-stu-id="06bb4-177">`"myappname"` (lower case)</span></span> |`"[toLower(parameters('appName'))]"` |
| `"<WebTest Name=\"myWebTest\" ...`<br/>` Url=\"http://fabrikam.com/home\" ...>"` |`[concat('<WebTest Name=\"',` <br/> `parameters('webTestName'),` <br/> `'\" ... Url=\"', parameters('Url'),` <br/> `'\"...>')]"`<br/><span data-ttu-id="06bb4-178">GUID 및 ID를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-178">Delete Guid and Id.</span></span> |

### <a name="set-dependencies-between-hello-resources"></a><span data-ttu-id="06bb4-179">Hello 리소스 간의 종속성을 설정</span><span class="sxs-lookup"><span data-stu-id="06bb4-179">Set dependencies between hello resources</span></span>
<span data-ttu-id="06bb4-180">Azure는 hello 리소스 엄격한 순서를 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-180">Azure should set up hello resources in strict order.</span></span> <span data-ttu-id="06bb4-181">hello 다음 시작 되기 전에 하나의 설치가 완료 된 있는지 toomake 종속성 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-181">toomake sure one setup completes before hello next begins, add dependency lines:</span></span>

* <span data-ttu-id="06bb4-182">Hello 사용 가능한 리소스를 테스트:</span><span class="sxs-lookup"><span data-stu-id="06bb4-182">In hello availability test resource:</span></span>
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/components', parameters('appName'))]"],`
* <span data-ttu-id="06bb4-183">Hello 가용성 테스트에 대 한 경고 리소스:</span><span class="sxs-lookup"><span data-stu-id="06bb4-183">In hello alert resource for an availability test:</span></span>
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/webtests', variables('testName'))]"],`



## <a name="next-steps"></a><span data-ttu-id="06bb4-184">다음 단계</span><span class="sxs-lookup"><span data-stu-id="06bb4-184">Next steps</span></span>
<span data-ttu-id="06bb4-185">다른 자동화 문서:</span><span class="sxs-lookup"><span data-stu-id="06bb4-185">Other automation articles:</span></span>

* <span data-ttu-id="06bb4-186">[Application Insights 리소스 만들기](app-insights-powershell-script-create-resource.md) - 템플릿을 사용하지 않는 빠른 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="06bb4-186">[Create an Application Insights resource](app-insights-powershell-script-create-resource.md) - quick method without using a template.</span></span>
* [<span data-ttu-id="06bb4-187">경고 설정</span><span class="sxs-lookup"><span data-stu-id="06bb4-187">Set up Alerts</span></span>](app-insights-powershell-alerts.md)
* [<span data-ttu-id="06bb4-188">웹 테스트 만들기</span><span class="sxs-lookup"><span data-stu-id="06bb4-188">Create web tests</span></span>](https://azure.microsoft.com/blog/creating-a-web-test-alert-programmatically-with-application-insights/)
* [<span data-ttu-id="06bb4-189">Azure 진단 tooApplication Insights 보내기</span><span class="sxs-lookup"><span data-stu-id="06bb4-189">Send Azure Diagnostics tooApplication Insights</span></span>](app-insights-powershell-azure-diagnostics.md)
* [<span data-ttu-id="06bb4-190">GitHub에서 tooAzure 배포</span><span class="sxs-lookup"><span data-stu-id="06bb4-190">Deploy tooAzure from GitHub</span></span>](http://blogs.msdn.com/b/webdev/archive/2015/09/16/deploy-to-azure-from-github-with-application-insights.aspx)
* [<span data-ttu-id="06bb4-191">릴리스 주석 만들기</span><span class="sxs-lookup"><span data-stu-id="06bb4-191">Create release annotations</span></span>](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1)

