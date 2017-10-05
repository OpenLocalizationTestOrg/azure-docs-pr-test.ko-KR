---
title: "Azure에서 템플릿을 사용하여 논리 앱 만들기 | Microsoft Docs"
description: "Azure Resource Manager 템플릿을 사용하여 워크플로를 정의하기 위한 논리 앱을 배포합니다."
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 7574cc7c-e5a1-4b7c-97f6-0cffb1a5d536
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2016
ms.author: LADocs; mandia
ms.openlocfilehash: 161adeacd6da2b15225c8a4ddae171e19e539967
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-logic-app-using-a-template"></a><span data-ttu-id="caa64-103">템플릿을 사용하여 논리 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="caa64-103">Create a Logic App using a template</span></span>
<span data-ttu-id="caa64-104">템플릿은 논리 앱 내에서 다양한 커넥터를 사용할 수 있는 빠른 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="caa64-104">Templates provide a quick way to use different connectors within a logic app.</span></span> <span data-ttu-id="caa64-105">Logic Apps에는 비즈니스 워크플로를 정의하는 데 사용할 수 있는 논리 앱을 만들 수 있도록 Azure Resource Manager 템플릿이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="caa64-105">Logic apps includes Azure Resource Manager templates for you to create a logic app that can be used to define business workflows.</span></span> <span data-ttu-id="caa64-106">배포할 리소스를 정의하고 논리 앱을 배포할 때 매개 변수를 정의하는 방법을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="caa64-106">You can define which resources are deployed, and how to define parameters when you deploy your logic app.</span></span> <span data-ttu-id="caa64-107">이 템플릿을 자체 비즈니스 시나리오에 사용하거나 요구 사항에 맞게 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="caa64-107">You can use this template for your own business scenarios, or customize it to meet your requirements.</span></span>

<span data-ttu-id="caa64-108">논리 앱 속성에 대한 자세한 내용은 [논리 앱 워크플로 관리 API](https://msdn.microsoft.com/library/azure/mt643788.aspx)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="caa64-108">For more details on the Logic app properties, see [Logic App Workflow Management API](https://msdn.microsoft.com/library/azure/mt643788.aspx).</span></span> 

<span data-ttu-id="caa64-109">정의 자체의 예는 [작성자 논리 앱 정의](logic-apps-author-definitions.md)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="caa64-109">For examples of the definition itself, see [Author Logic App definitions](logic-apps-author-definitions.md).</span></span> 

<span data-ttu-id="caa64-110">템플릿을 만드는 더 자세한 내용은 [Azure 리소스 관리자 템플릿 작성하기](../azure-resource-manager/resource-group-authoring-templates.md)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="caa64-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="caa64-111">전체 템플릿에 대해서는 [논리 앱 템플릿](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="caa64-111">For the complete template, see [Logic App template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).</span></span>

## <a name="what-you-deploy"></a><span data-ttu-id="caa64-112">배포할 내용</span><span class="sxs-lookup"><span data-stu-id="caa64-112">What you deploy</span></span>
<span data-ttu-id="caa64-113">이 서식 파일로 논리 앱을 배포합니다:</span><span class="sxs-lookup"><span data-stu-id="caa64-113">With this template, you deploy a logic app.</span></span>

<span data-ttu-id="caa64-114">배포를 자동으로 실행하려면 다음 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="caa64-114">To run the deployment automatically, select the following button:</span></span>  

<span data-ttu-id="caa64-115">[![Azure에 배포](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="caa64-115">[![Deploy to Azure](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="caa64-116">매개 변수</span><span class="sxs-lookup"><span data-stu-id="caa64-116">Parameters</span></span>
[!INCLUDE [app-service-logic-deploy-parameters](../../includes/app-service-logic-deploy-parameters.md)]

### <a name="testuri"></a><span data-ttu-id="caa64-117">testUri</span><span class="sxs-lookup"><span data-stu-id="caa64-117">testUri</span></span>
     "testUri": {
        "type": "string",
        "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
      }

## <a name="resources-to-deploy"></a><span data-ttu-id="caa64-118">배포할 리소스</span><span class="sxs-lookup"><span data-stu-id="caa64-118">Resources to deploy</span></span>
### <a name="logic-app"></a><span data-ttu-id="caa64-119">논리 앱</span><span class="sxs-lookup"><span data-stu-id="caa64-119">Logic app</span></span>
<span data-ttu-id="caa64-120">논리 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="caa64-120">Creates the logic app.</span></span>

<span data-ttu-id="caa64-121">템플릿은 논리 앱 이름에 대한 매개 변수 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="caa64-121">The templates uses a parameter value for the logic app name.</span></span> <span data-ttu-id="caa64-122">논리 앱의 위치를 리소스 그룹과 같은 위치로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="caa64-122">It sets the location of the logic app to the same location as the resource group.</span></span> 

<span data-ttu-id="caa64-123">이 특정 정의는 한 시간에 한 번 실행되며, **testUri** 매개 변수에서 지정된 위치를 ping합니다.</span><span class="sxs-lookup"><span data-stu-id="caa64-123">This particular definition runs once an hour, and pings the location specified in the **testUri** parameter.</span></span> 

    {
      "type": "Microsoft.Logic/workflows",
      "apiVersion": "2016-06-01",
      "name": "[parameters('logicAppName')]",
      "location": "[resourceGroup().location]",
      "tags": {
        "displayName": "LogicApp"
      },
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
      }
    }


## <a name="commands-to-run-deployment"></a><span data-ttu-id="caa64-124">배포 실행 명령</span><span class="sxs-lookup"><span data-stu-id="caa64-124">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="caa64-125">PowerShell</span><span class="sxs-lookup"><span data-stu-id="caa64-125">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="caa64-126">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="caa64-126">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -g ExampleDeployGroup



