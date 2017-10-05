---
title: "SQL 데이터베이스를 사용하는 웹앱을 프로비전"
description: "SQL 데이터베이스가 포함된 웹앱을 배포하는 Azure 리소스 관리자 템플릿을 사용합니다."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: fb9648e1-9bf2-4537-bc4a-ab8d4953168c
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2016
ms.author: cephalin
ms.openlocfilehash: cc34f684f8c50e95a62cb7b04fd2ddce5deb68d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="provision-a-web-app-with-a-sql-database"></a><span data-ttu-id="7a9fb-103">SQL 데이터베이스를 사용하는 웹앱을 프로비전</span><span class="sxs-lookup"><span data-stu-id="7a9fb-103">Provision a web app with a SQL Database</span></span>
<span data-ttu-id="7a9fb-104">이 항목에서는 웹앱 및 SQL 데이터베이스를 배포하는 Azure 리소스 관리자 템플릿을 만드는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="7a9fb-104">In this topic, you will learn how to create an Azure Resource Manager template that deploys a web app and SQL Database.</span></span> <span data-ttu-id="7a9fb-105">어떤 리소스를 배포할지 정의하는 방법 및 배포를 실행할 때 매개 변수를 지정하는 방법을 알게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a9fb-105">You will learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="7a9fb-106">배포를 위해 이 템플릿을 사용하거나 요구 사항에 맞게 사용자 지정을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a9fb-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="7a9fb-107">템플릿을 만드는 더 자세한 내용은 [Azure 리소스 관리자 템플릿 작성하기](../azure-resource-manager/resource-group-authoring-templates.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7a9fb-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="7a9fb-108">앱 배포에 대한 자세한 내용은 [Azure에서 예측 가능하도록 복잡한 응용 프로그램을 배포](app-service-deploy-complex-application-predictably.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7a9fb-108">For more information about deploying apps, see [Deploy a complex application predictably in Azure](app-service-deploy-complex-application-predictably.md).</span></span>

<span data-ttu-id="7a9fb-109">전체 서식 파일을 보려면 [SQL 데이터베이스 템플릿을 사용하는 웹앱](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-sql-database/azuredeploy.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7a9fb-109">For the complete template, see [Web App With SQL Database template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-sql-database/azuredeploy.json).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-deploy"></a><span data-ttu-id="7a9fb-110">배포할 내용</span><span class="sxs-lookup"><span data-stu-id="7a9fb-110">What you will deploy</span></span>
<span data-ttu-id="7a9fb-111">이 서식 파일에서 다음을 배포합니다:</span><span class="sxs-lookup"><span data-stu-id="7a9fb-111">In this template, you will deploy:</span></span>

* <span data-ttu-id="7a9fb-112">웹앱</span><span class="sxs-lookup"><span data-stu-id="7a9fb-112">a web app</span></span>
* <span data-ttu-id="7a9fb-113">SQL 데이터베이스 서버</span><span class="sxs-lookup"><span data-stu-id="7a9fb-113">SQL Database server</span></span>
* <span data-ttu-id="7a9fb-114">SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="7a9fb-114">SQL Database</span></span>
* <span data-ttu-id="7a9fb-115">자동 크기 조정 설정</span><span class="sxs-lookup"><span data-stu-id="7a9fb-115">AutoScale settings</span></span>
* <span data-ttu-id="7a9fb-116">경고 규칙</span><span class="sxs-lookup"><span data-stu-id="7a9fb-116">Alert rules</span></span>
* <span data-ttu-id="7a9fb-117">App Insights</span><span class="sxs-lookup"><span data-stu-id="7a9fb-117">App Insights</span></span>

<span data-ttu-id="7a9fb-118">배포를 자동으로 실행하려면 다음 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a9fb-118">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="7a9fb-119">[![Azure에 배포](./media/app-service-web-arm-with-sql-database-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-sql-database%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="7a9fb-119">[![Deploy to Azure](./media/app-service-web-arm-with-sql-database-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-sql-database%2Fazuredeploy.json)</span></span>

## <a name="parameters-to-specify"></a><span data-ttu-id="7a9fb-120">지정할 매개변수</span><span class="sxs-lookup"><span data-stu-id="7a9fb-120">Parameters to specify</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

### <a name="administratorlogin"></a><span data-ttu-id="7a9fb-121">administratorLogin</span><span class="sxs-lookup"><span data-stu-id="7a9fb-121">administratorLogin</span></span>
<span data-ttu-id="7a9fb-122">데이터베이스 서버 관리자에 사용할 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7a9fb-122">The account name to use for the database server administrator.</span></span>

    "administratorLogin": {
      "type": "string"
    }

### <a name="administratorloginpassword"></a><span data-ttu-id="7a9fb-123">administratorLoginPassword</span><span class="sxs-lookup"><span data-stu-id="7a9fb-123">administratorLoginPassword</span></span>
<span data-ttu-id="7a9fb-124">데이터베이스 서버 관리자에 사용할 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="7a9fb-124">The password to use for the database server administrator.</span></span>

    "administratorLoginPassword": {
      "type": "securestring"
    }

### <a name="databasename"></a><span data-ttu-id="7a9fb-125">databaseName</span><span class="sxs-lookup"><span data-stu-id="7a9fb-125">databaseName</span></span>
<span data-ttu-id="7a9fb-126">만들려는 새 데이터베이스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7a9fb-126">The name of the new database to create.</span></span>

    "databaseName": {
      "type": "string",
      "defaultValue": "sampledb"
    }

### <a name="collation"></a><span data-ttu-id="7a9fb-127">collation</span><span class="sxs-lookup"><span data-stu-id="7a9fb-127">collation</span></span>
<span data-ttu-id="7a9fb-128">문자의 적절한 사용을 제어하기 위해 사용하는 데이터베이스 데이터 정렬입니다.</span><span class="sxs-lookup"><span data-stu-id="7a9fb-128">The database collation to use for governing the proper use of characters.</span></span>

    "collation": {
      "type": "string",
      "defaultValue": "SQL_Latin1_General_CP1_CI_AS"
    }

### <a name="edition"></a><span data-ttu-id="7a9fb-129">edition</span><span class="sxs-lookup"><span data-stu-id="7a9fb-129">edition</span></span>
<span data-ttu-id="7a9fb-130">만들려는 데이터베이스의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="7a9fb-130">The type of database to create.</span></span>

    "edition": {
      "type": "string",
      "defaultValue": "Basic",
      "allowedValues": [
        "Basic",
        "Standard",
        "Premium"
      ],
      "metadata": {
        "description": "The type of database to create."
      }
    }

### <a name="maxsizebytes"></a><span data-ttu-id="7a9fb-131">maxSizeBytes</span><span class="sxs-lookup"><span data-stu-id="7a9fb-131">maxSizeBytes</span></span>
<span data-ttu-id="7a9fb-132">(바이트)는 데이터베이스의 최대 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="7a9fb-132">The maximum size, in bytes, for the database.</span></span>

    "maxSizeBytes": {
      "type": "string",
      "defaultValue": "1073741824"
    }

### <a name="requestedserviceobjectivename"></a><span data-ttu-id="7a9fb-133">requestedServiceObjectiveName</span><span class="sxs-lookup"><span data-stu-id="7a9fb-133">requestedServiceObjectiveName</span></span>
<span data-ttu-id="7a9fb-134">버전에 대한 성능 수준에 해당하는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7a9fb-134">The name corresponding to the performance level for edition.</span></span> 

    "requestedServiceObjectiveName": {
      "type": "string",
      "defaultValue": "Basic",
      "allowedValues": [
        "Basic",
        "S0",
        "S1",
        "S2",
        "P1",
        "P2",
        "P3"
      ],
      "metadata": {
        "description": "Describes the performance level for Edition"
      }
    }

## <a name="variables-for-names"></a><span data-ttu-id="7a9fb-135">이름에 대한 변수</span><span class="sxs-lookup"><span data-stu-id="7a9fb-135">Variables for names</span></span>
<span data-ttu-id="7a9fb-136">이 템플릿에는 템플릿에 사용되는 이름을 생성하는 변수가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a9fb-136">This template includes variables that construct names used in the template.</span></span> <span data-ttu-id="7a9fb-137">변수 값은 **uniqueString** 함수를 사용하여 리소스 그룹 id의 이름을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="7a9fb-137">The variable values use the **uniqueString** function to generate a name from the resource group id.</span></span>

    "variables": {
        "hostingPlanName": "[concat('hostingplan', uniqueString(resourceGroup().id))]",
        "webSiteName": "[concat('webSite', uniqueString(resourceGroup().id))]",
        "sqlserverName": "[concat('sqlserver', uniqueString(resourceGroup().id))]"
    },


## <a name="resources-to-deploy"></a><span data-ttu-id="7a9fb-138">배포할 리소스</span><span class="sxs-lookup"><span data-stu-id="7a9fb-138">Resources to deploy</span></span>
### <a name="sql-server-and-database"></a><span data-ttu-id="7a9fb-139">SQL Server 및 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="7a9fb-139">SQL Server and Database</span></span>
<span data-ttu-id="7a9fb-140">새 SQL Server 및 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7a9fb-140">Creates a new SQL Server and database.</span></span> <span data-ttu-id="7a9fb-141">서버 이름은 **serverName** 매개 변수에 지정되고 위치는 **serverLocation** 매개변수에 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a9fb-141">The name of the server is specified in the **serverName** parameter and the location specified in the **serverLocation** parameter.</span></span> <span data-ttu-id="7a9fb-142">새 서버를 만들 때 데이터베이스 서버 관리자용 로그인 이름 및 암호를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a9fb-142">When creating the new server, you must provide a login name and password for the database server administrator.</span></span> 

    {
      "name": "[variables('sqlserverName')]",
      "type": "Microsoft.Sql/servers",
      "location": "[resourceGroup().location]",
      "tags": {
        "displayName": "SqlServer"
      },
      "apiVersion": "2014-04-01-preview",
      "properties": {
        "administratorLogin": "[parameters('administratorLogin')]",
        "administratorLoginPassword": "[parameters('administratorLoginPassword')]"
      },
      "resources": [
        {
          "name": "[parameters('databaseName')]",
          "type": "databases",
          "location": "[resourceGroup().location]",
          "tags": {
            "displayName": "Database"
          },
          "apiVersion": "2014-04-01-preview",
          "dependsOn": [
            "[variables('sqlserverName')]"
          ],
          "properties": {
            "edition": "[parameters('edition')]",
            "collation": "[parameters('collation')]",
            "maxSizeBytes": "[parameters('maxSizeBytes')]",
            "requestedServiceObjectiveName": "[parameters('requestedServiceObjectiveName')]"
          }
        },
        {
          "type": "firewallrules",
          "apiVersion": "2014-04-01-preview",
          "dependsOn": [
            "[variables('sqlserverName')]"
          ],
          "location": "[resourceGroup().location]",
          "name": "AllowAllAzureIps",
          "properties": {
            "endIpAddress": "0.0.0.0",
            "startIpAddress": "0.0.0.0"
          }
        }
      ]
    },

[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="web-app"></a><span data-ttu-id="7a9fb-143">웹앱</span><span class="sxs-lookup"><span data-stu-id="7a9fb-143">Web app</span></span>
    {
      "apiVersion": "2015-08-01",
      "name": "[variables('webSiteName')]",
      "type": "Microsoft.Web/sites",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[variables('hostingPlanName')]"
      ],
      "tags": {
        "[concat('hidden-related:', resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName')))]": "empty",
        "displayName": "Website"
      },
      "properties": {
        "name": "[variables('webSiteName')]",
        "serverFarmId": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]"
      },
      "resources": [
        {
          "apiVersion": "2015-08-01",
          "type": "config",
          "name": "connectionstrings",
          "dependsOn": [
            "[variables('webSiteName')]"
          ],
          "properties": {
            "DefaultConnection": {
              "value": "[concat('Data Source=tcp:', reference(concat('Microsoft.Sql/servers/', variables('sqlserverName'))).fullyQualifiedDomainName, ',1433;Initial Catalog=', parameters('databaseName'), ';User Id=', parameters('administratorLogin'), '@', variables('sqlserverName'), ';Password=', parameters('administratorLoginPassword'), ';')]",
              "type": "SQLServer"
            }
          }
        }
      ]
    },


### <a name="autoscale"></a><span data-ttu-id="7a9fb-144">자동 크기 조정</span><span class="sxs-lookup"><span data-stu-id="7a9fb-144">AutoScale</span></span>
    {
      "apiVersion": "2014-04-01",
      "name": "[concat(variables('hostingPlanName'), '-', resourceGroup().name)]",
      "type": "Microsoft.Insights/autoscalesettings",
      "location": "[resourceGroup().location]",
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName')))]": "Resource",
        "displayName": "AutoScaleSettings"
      },
      "dependsOn": [
        "[variables('hostingPlanName')]"
      ],
      "properties": {
        "profiles": [
          {
            "name": "Default",
            "capacity": {
              "minimum": 1,
              "maximum": 2,
              "default": 1
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "CpuPercentage",
                  "metricResourceUri": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
                  "timeGrain": "PT1M",
                  "statistic": "Average",
                  "timeWindow": "PT10M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 80.0
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": 1,
                  "cooldown": "PT10M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "CpuPercentage",
                  "metricResourceUri": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
                  "timeGrain": "PT1M",
                  "statistic": "Average",
                  "timeWindow": "PT1H",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 60.0
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": 1,
                  "cooldown": "PT1H"
                }
              }
            ]
          }
        ],
        "enabled": false,
        "name": "[concat(variables('hostingPlanName'), '-', resourceGroup().name)]",
        "targetResourceUri": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]"
      }
    },


### <a name="alert-rules-for-status-codes-403-and-500s-high-cpu-and-http-queue-length"></a><span data-ttu-id="7a9fb-145">경고는 상태 코드 403 및 500's, 높은 CPU 사용률 및 HTTP 큐 길이를 규정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a9fb-145">Alert rules for status codes 403 and 500's, High CPU, and HTTP Queue Length</span></span>
    {
      "apiVersion": "2014-04-01",
      "name": "[concat('ServerErrors ', variables('webSiteName'))]",
      "type": "Microsoft.Insights/alertrules",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[variables('webSiteName')]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Web/sites', variables('webSiteName')))]": "Resource",
        "displayName": "ServerErrorsAlertRule"
      },
      "properties": {
        "name": "[concat('ServerErrors ', variables('webSiteName'))]",
        "description": "[concat(variables('webSiteName'), ' has some server errors, status code 5xx.')]",
        "isEnabled": false,
        "condition": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
          "dataSource": {
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[resourceId('Microsoft.Web/sites', variables('webSiteName'))]",
            "metricName": "Http5xx"
          },
          "operator": "GreaterThan",
          "threshold": 0.0,
          "windowSize": "PT5M"
        },
        "action": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
          "sendToServiceOwners": true,
          "customEmails": [ ]
        }
      }
    },
    {
      "apiVersion": "2014-04-01",
      "name": "[concat('ForbiddenRequests ', variables('webSiteName'))]",
      "type": "Microsoft.Insights/alertrules",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[variables('webSiteName')]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Web/sites', variables('webSiteName')))]": "Resource",
        "displayName": "ForbiddenRequestsAlertRule"
      },
      "properties": {
        "name": "[concat('ForbiddenRequests ', variables('webSiteName'))]",
        "description": "[concat(variables('webSiteName'), ' has some requests that are forbidden, status code 403.')]",
        "isEnabled": false,
        "condition": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
          "dataSource": {
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[resourceId('Microsoft.Web/sites', variables('webSiteName'))]",
            "metricName": "Http403"
          },
          "operator": "GreaterThan",
          "threshold": 0,
          "windowSize": "PT5M"
        },
        "action": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
          "sendToServiceOwners": true,
          "customEmails": [ ]
        }
      }
    },
    {
      "apiVersion": "2014-04-01",
      "name": "[concat('CPUHigh ', variables('hostingPlanName'))]",
      "type": "Microsoft.Insights/alertrules",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[variables('hostingPlanName')]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName')))]": "Resource",
        "displayName": "CPUHighAlertRule"
      },
      "properties": {
        "name": "[concat('CPUHigh ', variables('hostingPlanName'))]",
        "description": "[concat('The average CPU is high across all the instances of ', variables('hostingPlanName'))]",
        "isEnabled": false,
        "condition": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
          "dataSource": {
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
            "metricName": "CpuPercentage"
          },
          "operator": "GreaterThan",
          "threshold": 90,
          "windowSize": "PT15M"
        },
        "action": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
          "sendToServiceOwners": true,
          "customEmails": [ ]
        }
      }
    },
    {
      "apiVersion": "2014-04-01",
      "name": "[concat('LongHttpQueue ', variables('hostingPlanName'))]",
      "type": "Microsoft.Insights/alertrules",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[variables('hostingPlanName')]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName')))]": "Resource",
        "displayName": "AutoScaleSettings"
      },
      "properties": {
        "name": "[concat('LongHttpQueue ', variables('hostingPlanName'))]",
        "description": "[concat('The HTTP queue for the instances of ', variables('hostingPlanName'), ' has a large number of pending requests.')]",
        "isEnabled": false,
        "condition": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
          "dataSource": {
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[concat(resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', variables('hostingPlanName'))]",
            "metricName": "HttpQueueLength"
          },
          "operator": "GreaterThan",
          "threshold": 100.0,
          "windowSize": "PT5M"
        },
        "action": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
          "sendToServiceOwners": true,
          "customEmails": [ ]
        }
      }
    },

### <a name="app-insights"></a><span data-ttu-id="7a9fb-146">App Insights</span><span class="sxs-lookup"><span data-stu-id="7a9fb-146">App Insights</span></span>
    {
      "apiVersion": "2014-04-01",
      "name": "[concat('AppInsights', variables('webSiteName'))]",
      "type": "Microsoft.Insights/components",
      "location": "Central US",
      "dependsOn": [
        "[variables('webSiteName')]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Web/sites', variables('webSiteName')))]": "Resource",
        "displayName": "AppInsightsComponent"
      },
      "properties": {
        "ApplicationId": "[variables('webSiteName')]"
      }
    }

## <a name="commands-to-run-deployment"></a><span data-ttu-id="7a9fb-147">배포 실행 명령</span><span class="sxs-lookup"><span data-stu-id="7a9fb-147">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="7a9fb-148">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7a9fb-148">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-sql-database/azuredeploy.json

### <a name="azure-cli"></a><span data-ttu-id="7a9fb-149">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7a9fb-149">Azure CLI</span></span>

    azure config mode arm
    azure group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-sql-database/azuredeploy.json

### <a name="azure-cli-20"></a><span data-ttu-id="7a9fb-150">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="7a9fb-150">Azure CLI 2.0</span></span>

    az resource deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-sql-database/azuredeploy.json --parameters '@azuredeploy.parameters.json'

> [!NOTE]
> <span data-ttu-id="7a9fb-151">JSON 파일의 매개 변수의 내용은 [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-sql-database/azuredeploy.parameters.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7a9fb-151">For content of the parameters JSON file, see [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-sql-database/azuredeploy.parameters.json).</span></span>
>
>
