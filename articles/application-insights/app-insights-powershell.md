---
title: "PowerShell 사용하여 Azure Application Insights 자동화 | Microsoft Docs"
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
ms.openlocfilehash: 88dbb9515300f847789bc889911cdeff5f5bdb53
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
#  <a name="create-application-insights-resources-using-powershell"></a><span data-ttu-id="1ffff-103">PowerShell을 사용하여 Application Insights 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="1ffff-103">Create Application Insights resources using PowerShell</span></span>
<span data-ttu-id="1ffff-104">이 문서에서는 Azure Resource Management를 사용하여 [Application Insights](app-insights-overview.md) 리소스의 생성 및 업데이트를 자동화하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-104">This article shows you how to automate the creation and update of [Application Insights](app-insights-overview.md) resources automatically by using Azure Resource Management.</span></span> <span data-ttu-id="1ffff-105">예를 들어 빌드 프로세스의 일부로 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-105">You might, for example, do so as part of a build process.</span></span> <span data-ttu-id="1ffff-106">기본 Application Insights 리소스와 함께 [가용성 웹 테스트](app-insights-monitor-web-app-availability.md)를 만들고, [경고](app-insights-alerts.md)를 설정하고, [가격 책정 계층](app-insights-pricing.md)을 설정하고, 기타 Azure 리소스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-106">Along with the basic Application Insights resource, you can create [availability web tests](app-insights-monitor-web-app-availability.md), set up [alerts](app-insights-alerts.md), set the [pricing scheme](app-insights-pricing.md), and create other Azure resources.</span></span>

<span data-ttu-id="1ffff-107">이러한 리소스를 만드는 데 핵심 사항은 [Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md)용 JSON 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-107">The key to creating these resources is JSON templates for [Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span> <span data-ttu-id="1ffff-108">간단히 말하면 절차는 다음과 같습니다. 기존 리소스의 JSON 정의를 다운로드하고, 이름과 같은 특정 값을 매개 변수화한 다음 새 리소스를 만들려고 할 때마다 템플릿을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-108">In a nutshell, the procedure is: download the JSON definitions of existing resources; parameterize certain values such as names; and then run the template whenever you want to create a new resource.</span></span> <span data-ttu-id="1ffff-109">여러 리소스를 함께 패키지하여 모두 한꺼번에 만들 수 있습니다(예: 가용성 테스트, 경고 및 연속 내보내기에 대한 저장소를 포함하는 앱 모니터).</span><span class="sxs-lookup"><span data-stu-id="1ffff-109">You can package several resources together, to create them all in one go - for example, an app monitor with availability tests, alerts, and storage for continuous export.</span></span> <span data-ttu-id="1ffff-110">일부 매개 변수화에 있는 약간의 미묘한 사항은 여기서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-110">There are some subtleties to some of the parameterizations, which we'll explain here.</span></span>

## <a name="one-time-setup"></a><span data-ttu-id="1ffff-111">일 회 설정</span><span class="sxs-lookup"><span data-stu-id="1ffff-111">One-time setup</span></span>
<span data-ttu-id="1ffff-112">아직 Azure 구독에서 PowerShell을 사용한 적이 없을 경우:</span><span class="sxs-lookup"><span data-stu-id="1ffff-112">If you haven't used PowerShell with your Azure subscription before:</span></span>

<span data-ttu-id="1ffff-113">스크립트를 실행하려는 컴퓨터에 Azure Powershell 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-113">Install the Azure Powershell module on the machine where you want to run the scripts:</span></span>

1. <span data-ttu-id="1ffff-114">[Microsoft 웹 플랫폼 설치 관리자(v5 이상)](http://www.microsoft.com/web/downloads/platform.aspx)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-114">Install [Microsoft Web Platform Installer (v5 or higher)](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
2. <span data-ttu-id="1ffff-115">이를 사용하여 Microsoft Azure Powershell을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-115">Use it to install Microsoft Azure Powershell.</span></span>

## <a name="create-an-azure-resource-manager-template"></a><span data-ttu-id="1ffff-116">Azure Resource Manager 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="1ffff-116">Create an Azure Resource Manager template</span></span>
<span data-ttu-id="1ffff-117">새 .json 파일을 만듭니다. 이 예제에서는 `template1.json`입니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-117">Create a new .json file - let's call it `template1.json` in this example.</span></span> <span data-ttu-id="1ffff-118">아래 내용을 이 파일에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-118">Copy this content into it:</span></span>

```JSON
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "appName": {
                "type": "string",
                "metadata": {
                    "description": "Enter the application name."
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
                    "description": "Enter the application type."
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
                    "description": "Enter the application location."
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
                    "description": "Enter daily quota reset hour in UTC (0 to 23). Values outside the range will get a random reset hour."
                }
            },
            "warningThreshold": {
                "type": "int",
                "defaultValue": 90,
                "minValue": 1,
                "maxValue": 100,
                "metadata": {
                    "description": "Enter the % value of daily quota after which warning mail to be sent. "
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



## <a name="create-application-insights-resources"></a><span data-ttu-id="1ffff-119">Application Insights 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="1ffff-119">Create Application Insights resources</span></span>
1. <span data-ttu-id="1ffff-120">PowerShell에서 Azure에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-120">In PowerShell, sign in to Azure:</span></span>
   
    `Login-AzureRmAccount`
2. <span data-ttu-id="1ffff-121">다음과 같은 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-121">Run a command like this:</span></span>
   
    ```PS
   
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -appName myNewApp

    ``` 
   
   * <span data-ttu-id="1ffff-122">`-ResourceGroupName`은 새 리소스를 만들려는 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-122">`-ResourceGroupName` is the group where you want to create the new resources.</span></span>
   * <span data-ttu-id="1ffff-123">`-TemplateFile`은 사용자 지정 매개 변수 앞에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-123">`-TemplateFile` must occur before the custom parameters.</span></span>
   * <span data-ttu-id="1ffff-124">`-appName` 만들려는 리소스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-124">`-appName` The name of the resource to create.</span></span>

<span data-ttu-id="1ffff-125">다른 매개 변수를 추가할 수 있습니다. 템플릿의 매개 변수 섹션에서 해당 설명을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-125">You can add other parameters - you'll find their descriptions in the parameters section of the template.</span></span>

## <a name="to-get-the-instrumentation-key"></a><span data-ttu-id="1ffff-126">계측 키를 가져오려면</span><span class="sxs-lookup"><span data-stu-id="1ffff-126">To get the instrumentation key</span></span>
<span data-ttu-id="1ffff-127">응용 프로그램 리소스를 만든 후 계측 키가 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-127">After creating an application resource, you'll want the instrumentation key:</span></span> 

```PS
    $resource = Find-AzureRmResource -ResourceNameEquals "<YOUR APP NAME>" -ResourceType "Microsoft.Insights/components"
    $details = Get-AzureRmResource -ResourceId $resource.ResourceId
    $ikey = $details.Properties.InstrumentationKey
```


<a id="price"></a>
## <a name="set-the-price-plan"></a><span data-ttu-id="1ffff-128">가격 계획 설정</span><span class="sxs-lookup"><span data-stu-id="1ffff-128">Set the price plan</span></span>

<span data-ttu-id="1ffff-129">[가격 계획](app-insights-pricing.md)을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-129">You can set the [price plan](app-insights-pricing.md).</span></span>

<span data-ttu-id="1ffff-130">위의 템플릿을 사용하여 엔터프라이즈 가격 계획이 있는 앱 리소스를 만들려면</span><span class="sxs-lookup"><span data-stu-id="1ffff-130">To create an app resource with the Enterprise price plan, using the template above:</span></span>

```PS
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -priceCode 2 `
               -appName myNewApp
```

|<span data-ttu-id="1ffff-131">priceCode</span><span class="sxs-lookup"><span data-stu-id="1ffff-131">priceCode</span></span>|<span data-ttu-id="1ffff-132">계획</span><span class="sxs-lookup"><span data-stu-id="1ffff-132">plan</span></span>|
|---|---|
|<span data-ttu-id="1ffff-133">1</span><span class="sxs-lookup"><span data-stu-id="1ffff-133">1</span></span>|<span data-ttu-id="1ffff-134">Basic</span><span class="sxs-lookup"><span data-stu-id="1ffff-134">Basic</span></span>|
|<span data-ttu-id="1ffff-135">2</span><span class="sxs-lookup"><span data-stu-id="1ffff-135">2</span></span>|<span data-ttu-id="1ffff-136">Enterprise</span><span class="sxs-lookup"><span data-stu-id="1ffff-136">Enterprise</span></span>|

* <span data-ttu-id="1ffff-137">기본적인 Basic 가격 계획만 사용하려는 경우 템플릿에서 CurrentBillingFeatures 리소스를 생략해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-137">If you only want to use the default Basic price plan, you can omit the CurrentBillingFeatures resource from the template.</span></span>
* <span data-ttu-id="1ffff-138">구성 요소 리소스를 만든 후에 가격 계획을 변경하려는 경우 "microsoft.insights/components" 리소스를 생략하는 템플릿을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-138">If you want to change the price plan after the component resource has been created, you can use a template that omits the "microsoft.insights/components" resource.</span></span> <span data-ttu-id="1ffff-139">또한 청구 리소스에서 `dependsOn` 노드를 생략합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-139">Also, omit the `dependsOn` node from the billing resource.</span></span> 

<span data-ttu-id="1ffff-140">업데이트된 가격 계획을 확인하려면 브라우저에서 "기능+가격 책정" 블레이드를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-140">To verify the updated price plan, look at the "Features+pricing" blade in the browser.</span></span> <span data-ttu-id="1ffff-141">**브라우저 보기를 새로 고쳐** 최신 상태를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-141">**Refresh the browser view** to make sure you see the latest state.</span></span>



## <a name="add-a-metric-alert"></a><span data-ttu-id="1ffff-142">메트릭 경고 추가</span><span class="sxs-lookup"><span data-stu-id="1ffff-142">Add a metric alert</span></span>

<span data-ttu-id="1ffff-143">앱 리소스와 동시에 메트릭 경고를 설정하려면 다음과 같이 코드를 템플릿 파일에 병합합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-143">To set up a metric alert at the same time as your app resource, merge code like this into the template file:</span></span>

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
      // Ensure this resource is created after the app resource:
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

<span data-ttu-id="1ffff-144">템플릿을 호출할 때 선택적으로 이 매개 변수를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-144">When you invoke the template, you can optionally add this parameter:</span></span>

    `-responseTime 2`

<span data-ttu-id="1ffff-145">물론 다른 필드를 매개 변수화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-145">You can of course parameterize other fields.</span></span> 

<span data-ttu-id="1ffff-146">다른 경고 규칙의 형식 이름 및 구성 세부 정보를 찾으려면 수동으로 규칙을 만든 다음 [Azure Resource Manager](https://resources.azure.com/)에서 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-146">To find out the type names and configuration details of other alert rules, create a rule manually and then inspect it in [Azure Resource Manager](https://resources.azure.com/).</span></span> 


## <a name="add-an-availability-test"></a><span data-ttu-id="1ffff-147">가용성 테스트 추가</span><span class="sxs-lookup"><span data-stu-id="1ffff-147">Add an availability test</span></span>

<span data-ttu-id="1ffff-148">이 예는 ping 테스트(단일 페이지 테스트용)에 대한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-148">This example is for a ping test (to test a single page).</span></span>  

<span data-ttu-id="1ffff-149">가용성 테스트에는 테스트 자체와 실패를 알리는 경고 부분인 **두 부분이 있습니다**.</span><span class="sxs-lookup"><span data-stu-id="1ffff-149">**There are two parts** in an availability test: the test itself, and the alert that notifies you of failures.</span></span>

<span data-ttu-id="1ffff-150">다음 코드를 앱을 만드는 템플릿 파일에 병합합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-150">Merge the following code into the template file that creates the app.</span></span>

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
      // Availability test: part 1 configures the test
      //
      "name": "[variables('pingTestName')]",
      "type": "Microsoft.Insights/webtests",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]",
      // Ensure this is created after the app resource:
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
          "WebTest": "[concat('<WebTest   Name=\"', variables('pingTestName'), '\"   Enabled=\"True\"         CssProjectStructure=\"\"    CssIteration=\"\"  Timeout=\"120\"  WorkItemIds=\"\"         xmlns=\"http://microsoft.com/schemas/VisualStudio/TeamTest/2010\"         Description=\"\"  CredentialUserName=\"\"  CredentialPassword=\"\"         PreAuthenticate=\"True\"  Proxy=\"default\"  StopOnError=\"False\"         RecordedResultFile=\"\"  ResultsLocale=\"\">  <Items>  <Request Method=\"GET\"    Version=\"1.1\"  Url=\"', parameters('Url'),   '\" ThinkTime=\"0\"  Timeout=\"300\" ParseDependentRequests=\"True\"         FollowRedirects=\"True\" RecordResult=\"True\" Cache=\"False\"         ResponseTimeGoal=\"0\"  Encoding=\"utf-8\"  ExpectedHttpStatusCode=\"200\"         ExpectedResponseUrl=\"\" ReportingName=\"\" IgnoreHttpStatusCode=\"False\" />        </Items>  <ValidationRules> <ValidationRule  Classname=\"Microsoft.VisualStudio.TestTools.WebTesting.Rules.ValidationRuleFindText, Microsoft.VisualStudio.QualityTools.WebTestFramework, Version=10.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a\" DisplayName=\"Find Text\"         Description=\"Verifies the existence of the specified text in the response.\"         Level=\"High\"  ExectuionOrder=\"BeforeDependents\">  <RuleParameters>        <RuleParameter Name=\"FindText\" Value=\"',   parameters('pingText'), '\" />  <RuleParameter Name=\"IgnoreCase\" Value=\"False\" />  <RuleParameter Name=\"UseRegularExpression\" Value=\"False\" />  <RuleParameter Name=\"PassIfTextFound\" Value=\"True\" />  </RuleParameters> </ValidationRule>  </ValidationRules>  </WebTest>')]"
        },
        "SyntheticMonitorId": "[variables('pingTestName')]"
      }
    },

    {
      //
      // Availability test: part 2, the alert rule
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

<span data-ttu-id="1ffff-151">다른 테스트 위치의 코드를 검색하거나 좀 더 복잡한 웹 테스트의 생성을 자동화하려면 수동으로 예제를 만든 다음 [Azure Resource Manager](https://resources.azure.com/)에서 코드를 매개 변수화합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-151">To discover the codes for other test locations, or to automate the creation of more complex web tests, create an example manually and then parameterize the code from [Azure Resource Manager](https://resources.azure.com/).</span></span>

## <a name="add-more-resources"></a><span data-ttu-id="1ffff-152">리소스 추가</span><span class="sxs-lookup"><span data-stu-id="1ffff-152">Add more resources</span></span>

<span data-ttu-id="1ffff-153">다양한 종류의 다른 리소스의 생성을 자동화하려면 수동으로 예제를 만든 다음 [Azure Resource Manager](https://resources.azure.com/)에서 해당 코드를 복사하고 매개 변수화합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-153">To automate the creation of any other resource of any kind, create an example manually, and then copy and parameterize its code from [Azure Resource Manager](https://resources.azure.com/).</span></span> 

1. <span data-ttu-id="1ffff-154">[Azure 리소스 관리자](https://resources.azure.com/)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-154">Open [Azure Resource Manager](https://resources.azure.com/).</span></span> <span data-ttu-id="1ffff-155">`subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components`를 통해 응용 프로그램 리소스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-155">Navigate down through `subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components`, to your application resource.</span></span> 
   
    ![Azure 리소스 탐색기에서 탐색](./media/app-insights-powershell/01.png)
   
    <span data-ttu-id="1ffff-157">*구성 요소* 는 응용 프로그램을 표시하기 위한 기본 Application Insights 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-157">*Components* are the basic Application Insights resources for displaying applications.</span></span> <span data-ttu-id="1ffff-158">연결된 경고 규칙 및 가용성 웹 테스트에 대한 별도의 리소스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-158">There are separate resources for the associated alert rules and availability web tests.</span></span>
2. <span data-ttu-id="1ffff-159">구성 요소의 JSON을 `template1.json`의 적절한 위치에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-159">Copy the JSON of the component into the appropriate place in `template1.json`.</span></span>
3. <span data-ttu-id="1ffff-160">다음 속성을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-160">Delete these properties:</span></span>
   
   * `id`
   * `InstrumentationKey`
   * `CreationDate`
   * `TenantId`
4. <span data-ttu-id="1ffff-161">webtests 및 alertrules 섹션을 열고 개별 항목에 대한 JSON을 템플릿에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-161">Open the webtests and alertrules sections and copy the JSON for individual items into your template.</span></span> <span data-ttu-id="1ffff-162">(webtests 또는 alertrules 노드에서 복사하지 말고 그 아래에 있는 항목으로 이동)</span><span class="sxs-lookup"><span data-stu-id="1ffff-162">(Don't copy from the webtests or alertrules nodes: go into the items under them.)</span></span>
   
    <span data-ttu-id="1ffff-163">각 웹 테스트에는 연결된 경고 규칙이 있으므로 둘 다 복사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-163">Each web test has an associated alert rule, so you have to copy both of them.</span></span>
   
    <span data-ttu-id="1ffff-164">메트릭에 대한 경고를 포함할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-164">You can also include alerts on metrics.</span></span> <span data-ttu-id="1ffff-165">[메트릭 이름](app-insights-powershell-alerts.md#metric-names)</span><span class="sxs-lookup"><span data-stu-id="1ffff-165">[Metric names](app-insights-powershell-alerts.md#metric-names).</span></span>
5. <span data-ttu-id="1ffff-166">각 리소스에 다음 줄을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-166">Insert this line in each resource:</span></span>
   
    `"apiVersion": "2015-05-01",`

### <a name="parameterize-the-template"></a><span data-ttu-id="1ffff-167">템플릿 매개 변수화</span><span class="sxs-lookup"><span data-stu-id="1ffff-167">Parameterize the template</span></span>
<span data-ttu-id="1ffff-168">이제 특정 이름을 매개 변수로 대체해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-168">Now you have to replace the specific names with parameters.</span></span> <span data-ttu-id="1ffff-169">[템플릿을 매개 변수화](../azure-resource-manager/resource-group-authoring-templates.md)하려면 [도우미 함수 집합](../azure-resource-manager/resource-group-template-functions.md)을 사용하여 식을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-169">To [parameterize a template](../azure-resource-manager/resource-group-authoring-templates.md), you write expressions using a [set of helper functions](../azure-resource-manager/resource-group-template-functions.md).</span></span> 

<span data-ttu-id="1ffff-170">문자열의 일부만 매개 변수화할 수 없으므로 `concat()`을 사용하여 문자열을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-170">You can't parameterize just part of a string, so use `concat()` to build strings.</span></span>

<span data-ttu-id="1ffff-171">다음은 만들 수 있는 대체 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-171">Here are examples of the substitutions you'll want to make.</span></span> <span data-ttu-id="1ffff-172">각 대체가 여러 번 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-172">There are several occurrences of each substitution.</span></span> <span data-ttu-id="1ffff-173">템플릿에서 다른 사항이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-173">You might need others in your template.</span></span> <span data-ttu-id="1ffff-174">이러한 예제에서는 템플릿의 위쪽에서 정의한 매개 변수 및 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-174">These examples use the parameters and variables we defined at the top of the template.</span></span>

| <span data-ttu-id="1ffff-175">find</span><span class="sxs-lookup"><span data-stu-id="1ffff-175">find</span></span> | <span data-ttu-id="1ffff-176">대체</span><span class="sxs-lookup"><span data-stu-id="1ffff-176">replace with</span></span> |
| --- | --- |
| `"hidden-link:/subscriptions/.../components/MyAppName"` |`"[concat('hidden-link:',`<br/>` resourceId('microsoft.insights/components',` <br/> ` parameters('appName')))]"` |
| `"/subscriptions/.../alertrules/myAlertName-myAppName-subsId",` |`"[resourceId('Microsoft.Insights/alertrules', variables('alertRuleName'))]",` |
| `"/subscriptions/.../webtests/myTestName-myAppName",` |`"[resourceId('Microsoft.Insights/webtests', parameters('webTestName'))]",` |
| `"myWebTest-myAppName"` |`"[variables(testName)]"'` |
| `"myTestName-myAppName-subsId"` |`"[variables('alertRuleName')]"` |
| `"myAppName"` |`"[parameters('appName')]"` |
| <span data-ttu-id="1ffff-177">`"myappname"` (소문자)</span><span class="sxs-lookup"><span data-stu-id="1ffff-177">`"myappname"` (lower case)</span></span> |`"[toLower(parameters('appName'))]"` |
| `"<WebTest Name=\"myWebTest\" ...`<br/>` Url=\"http://fabrikam.com/home\" ...>"` |`[concat('<WebTest Name=\"',` <br/> `parameters('webTestName'),` <br/> `'\" ... Url=\"', parameters('Url'),` <br/> `'\"...>')]"`<br/><span data-ttu-id="1ffff-178">GUID 및 ID를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-178">Delete Guid and Id.</span></span> |

### <a name="set-dependencies-between-the-resources"></a><span data-ttu-id="1ffff-179">리소스 간의 종속성 설정</span><span class="sxs-lookup"><span data-stu-id="1ffff-179">Set dependencies between the resources</span></span>
<span data-ttu-id="1ffff-180">Azure에서는 엄격한 순서로 리소스를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-180">Azure should set up the resources in strict order.</span></span> <span data-ttu-id="1ffff-181">다음 설정 시작 전에 하나의 설정이 완료되게 하려면 종속성 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-181">To make sure one setup completes before the next begins, add dependency lines:</span></span>

* <span data-ttu-id="1ffff-182">가용성 테스트 리소스:</span><span class="sxs-lookup"><span data-stu-id="1ffff-182">In the availability test resource:</span></span>
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/components', parameters('appName'))]"],`
* <span data-ttu-id="1ffff-183">가용성 테스트에 대한 경고 리소스:</span><span class="sxs-lookup"><span data-stu-id="1ffff-183">In the alert resource for an availability test:</span></span>
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/webtests', variables('testName'))]"],`



## <a name="next-steps"></a><span data-ttu-id="1ffff-184">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1ffff-184">Next steps</span></span>
<span data-ttu-id="1ffff-185">다른 자동화 문서:</span><span class="sxs-lookup"><span data-stu-id="1ffff-185">Other automation articles:</span></span>

* <span data-ttu-id="1ffff-186">[Application Insights 리소스 만들기](app-insights-powershell-script-create-resource.md) - 템플릿을 사용하지 않는 빠른 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="1ffff-186">[Create an Application Insights resource](app-insights-powershell-script-create-resource.md) - quick method without using a template.</span></span>
* [<span data-ttu-id="1ffff-187">경고 설정</span><span class="sxs-lookup"><span data-stu-id="1ffff-187">Set up Alerts</span></span>](app-insights-powershell-alerts.md)
* [<span data-ttu-id="1ffff-188">웹 테스트 만들기</span><span class="sxs-lookup"><span data-stu-id="1ffff-188">Create web tests</span></span>](https://azure.microsoft.com/blog/creating-a-web-test-alert-programmatically-with-application-insights/)
* [<span data-ttu-id="1ffff-189">Application Insights에 Azure 진단 보내기</span><span class="sxs-lookup"><span data-stu-id="1ffff-189">Send Azure Diagnostics to Application Insights</span></span>](app-insights-powershell-azure-diagnostics.md)
* [<span data-ttu-id="1ffff-190">GitHub에서 Azure로 배포</span><span class="sxs-lookup"><span data-stu-id="1ffff-190">Deploy to Azure from GitHub</span></span>](http://blogs.msdn.com/b/webdev/archive/2015/09/16/deploy-to-azure-from-github-with-application-insights.aspx)
* [<span data-ttu-id="1ffff-191">릴리스 주석 만들기</span><span class="sxs-lookup"><span data-stu-id="1ffff-191">Create release annotations</span></span>](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1)

