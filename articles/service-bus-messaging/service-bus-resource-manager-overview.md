---
title: "Azure Resource Manager 템플릿을 사용하여 Azure Service Bus 리소스 만들기 | Microsoft Docs"
description: "Azure Resource Manager 템플릿을 사용하여 자동으로 서비스 버스 리소스 만들기"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 24f6a207-0fa4-49cf-8a58-963f9e2fd655
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: c8142d8edfd3a527b13d655bac21acf5332f2d14
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-service-bus-resources-using-azure-resource-manager-templates"></a><span data-ttu-id="81d3c-103">Azure Resource Manager 템플릿을 사용하여 서비스 버스 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="81d3c-103">Create Service Bus resources using Azure Resource Manager templates</span></span>

<span data-ttu-id="81d3c-104">이 문서에서는 Azure Resource Manager 템플릿, PowerShell 및 Service Bus 리소스 공급자를 사용하여 Service Bus 리소스를 만들어 배포하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="81d3c-104">This article describes how to create and deploy Service Bus resources using Azure Resource Manager templates, PowerShell, and the Service Bus resource provider.</span></span>

<span data-ttu-id="81d3c-105">Azure Resource Manager 템플릿을 통해 솔루션에 사용할 리소스를 정의하고, 여러 환경의 값을 입력하는 데 사용할 수 있는 변수 및 매개 변수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="81d3c-105">Azure Resource Manager templates help you define the resources to deploy for a solution, and to specify parameters and variables that enable you to input values for different environments.</span></span> <span data-ttu-id="81d3c-106">템플릿은 배포에 대한 값을 생성하는 데 사용할 수 있는 식과 JSON으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="81d3c-106">The template consists of JSON and expressions that you can use to construct values for your deployment.</span></span> <span data-ttu-id="81d3c-107">Azure Resource Manager 템플릿 작성에 대한 자세한 내용과 템플릿 형식에 대한 논의는 [Azure Resource Manager 템플릿의 구조 및 구문](../azure-resource-manager/resource-group-authoring-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81d3c-107">For detailed information about writing Azure Resource Manager templates, and a discussion of the template format, see [structure and syntax of Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

> [!NOTE]
> <span data-ttu-id="81d3c-108">이 문서의 예제에서는 Azure Resource Manager를 사용하여 서비스 버스 네임스페이스와 메시징 엔터티(큐)를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="81d3c-108">The examples in this article show how to use Azure Resource Manager to create a Service Bus namespace and messaging entity (queue).</span></span> <span data-ttu-id="81d3c-109">다른 템플릿 예제는 [Azure 빠른 시작 템플릿 갤러리][Azure Quickstart Templates gallery]를 방문하고 "Service Bus"를 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="81d3c-109">For other template examples, visit the [Azure Quickstart Templates gallery][Azure Quickstart Templates gallery] and search for "Service Bus."</span></span>
>
>

## <a name="service-bus-resource-manager-templates"></a><span data-ttu-id="81d3c-110">Service Bus Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="81d3c-110">Service Bus Resource Manager templates</span></span>

<span data-ttu-id="81d3c-111">이러한 Service Bus Azure Resource Manager 템플릿은 다운로드하여 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81d3c-111">These Service Bus Azure Resource Manager templates are available for download and deployment.</span></span> <span data-ttu-id="81d3c-112">각각에 대한 자세한 내용은 GitHub의 템플릿에 대한 링크가 포함된 다음 링크를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="81d3c-112">Click the following links for details about each one, with links to the templates on GitHub:</span></span>

* [<span data-ttu-id="81d3c-113">서비스 버스 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="81d3c-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
* [<span data-ttu-id="81d3c-114">큐가 있는 서비스 버스 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="81d3c-114">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
* [<span data-ttu-id="81d3c-115">토픽 및 구독이 있는 서비스 버스 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="81d3c-115">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
* [<span data-ttu-id="81d3c-116">큐 및 권한 부여 규칙이 있는 서비스 버스 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="81d3c-116">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
* [<span data-ttu-id="81d3c-117">토픽, 구독 및 규칙이 있는 Service Bus 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="81d3c-117">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)

## <a name="deploy-with-powershell"></a><span data-ttu-id="81d3c-118">PowerShell을 사용하여 배포 </span><span class="sxs-lookup"><span data-stu-id="81d3c-118">Deploy with PowerShell</span></span>

<span data-ttu-id="81d3c-119">다음 절차에서는 **표준** 계층 Service Bus 네임스페이스와, 네임스페이스 안의 큐를 만드는 Azure Resource Manager 템플릿을 PowerShell을 사용하여 배포하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="81d3c-119">The following procedure describes how to use PowerShell to deploy an Azure Resource Manager template that creates a **Standard** tier Service Bus namespace, and a queue within that namespace.</span></span> <span data-ttu-id="81d3c-120">이 예제는 [큐가 있는 Service Bus 네임스페이스 만들기](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) 템플릿을 기초로 합니다.</span><span class="sxs-lookup"><span data-stu-id="81d3c-120">This example is based on the [Create a Service Bus namespace with queue](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) template.</span></span> <span data-ttu-id="81d3c-121">대략적인 워크플로 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="81d3c-121">The approximate workflow is as follows:</span></span>

1. <span data-ttu-id="81d3c-122">PowerShell을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="81d3c-122">Install PowerShell.</span></span>
2. <span data-ttu-id="81d3c-123">템플릿 및 매개 변수 파일(옵션)을 만듭니다. </span><span class="sxs-lookup"><span data-stu-id="81d3c-123">Create the template and (optionally) a parameter file.</span></span>
3. <span data-ttu-id="81d3c-124">PowerShell에서 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="81d3c-124">In PowerShell, log in to your Azure account.</span></span>
4. <span data-ttu-id="81d3c-125">새 리소스 그룹이 아직 없으면 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="81d3c-125">Create a new resource group if one does not exist.</span></span>
5. <span data-ttu-id="81d3c-126">배포를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="81d3c-126">Test the deployment.</span></span>
6. <span data-ttu-id="81d3c-127">원하는 경우 배포 모드를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="81d3c-127">If desired, set the deployment mode.</span></span>
7. <span data-ttu-id="81d3c-128">템플릿을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="81d3c-128">Deploy the template.</span></span>

<span data-ttu-id="81d3c-129">Azure Resource Manager 배포 템플릿에 대한 모든 내용은 [Azure Resource Manager 템플릿으로 리소스 배포][Deploy resources with Azure Resource Manager templates]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81d3c-129">For complete information about deploying Azure Resource Manager templates, see [Deploy resources with Azure Resource Manager templates][Deploy resources with Azure Resource Manager templates].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="81d3c-130">PowerShell 설치 </span><span class="sxs-lookup"><span data-stu-id="81d3c-130">Install PowerShell</span></span>

<span data-ttu-id="81d3c-131">[Azure PowerShell 시작하기](/powershell/azure/get-started-azureps)의 지침을 따라서 Azure PowerShell을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="81d3c-131">Install Azure PowerShell by following the instructions in [Getting started with Azure PowerShell](/powershell/azure/get-started-azureps).</span></span>

### <a name="create-a-template"></a><span data-ttu-id="81d3c-132">템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="81d3c-132">Create a template</span></span>

<span data-ttu-id="81d3c-133">GitHub에서 [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) 템플릿을 복제 또는 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="81d3c-133">Clone or copy the [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) template from GitHub:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "type": "string",
            "metadata": {
                "description": "Name of the Service Bus namespace"
            }
        },
        "serviceBusQueueName": {
            "type": "string",
            "metadata": {
                "description": "Name of the Queue"
            }
        },
        "serviceBusApiVersion": {
            "type": "string",
            "defaultValue": "2015-08-01",
            "metadata": {
                "description": "Service Bus ApiVersion used by the template"
            }
        }
    },
    "variables": {
        "location": "[resourceGroup().location]",
        "sbVersion": "[parameters('serviceBusApiVersion')]",
        "defaultSASKeyName": "RootManageSharedAccessKey",
        "authRuleResourceId": "[resourceId('Microsoft.ServiceBus/namespaces/authorizationRules', parameters('serviceBusNamespaceName'), variables('defaultSASKeyName'))]"
    },
    "resources": [{
        "apiVersion": "[variables('sbVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "kind": "Messaging",
        "sku": {
            "name": "StandardSku",
            "tier": "Standard"
        },
        "resources": [{
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusQueueName')]",
            "type": "Queues",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusQueueName')]"
            }
        }]
    }],
    "outputs": {
        "NamespaceConnectionString": {
            "type": "string",
            "value": "[listkeys(variables('authRuleResourceId'), variables('sbVersion')).primaryConnectionString]"
        },
        "SharedAccessPolicyPrimaryKey": {
            "type": "string",
            "value": "[listkeys(variables('authRuleResourceId'), variables('sbVersion')).primaryKey]"
        }
    }
}
```

### <a name="create-a-parameters-file-optional"></a><span data-ttu-id="81d3c-134">매개 변수 파일 만들기(옵션)</span><span class="sxs-lookup"><span data-stu-id="81d3c-134">Create a parameters file (optional)</span></span>

<span data-ttu-id="81d3c-135">옵션인 매개 변수 파일을 사용하려면 [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="81d3c-135">To use an optional parameters file, copy the [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) file.</span></span> <span data-ttu-id="81d3c-136">`serviceBusNamespaceName` 값을 이 배포에 만들려는 서비스 버스 네임스페이스의 이름으로 바꾸고, `serviceBusQueueName` 값을 만들려는 큐의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="81d3c-136">Replace the value of `serviceBusNamespaceName` with the name of the Service Bus namespace you want to create in this deployment, and replace the value of `serviceBusQueueName` with the name of the queue you want to create.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "value": "<myNamespaceName>"
        },
        "serviceBusQueueName": {
            "value": "<myQueueName>"
        },
        "serviceBusApiVersion": {
            "value": "2015-08-01"
        }
    }
}
```

<span data-ttu-id="81d3c-137">자세한 내용은 [매개 변수](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81d3c-137">For more information, see the [Parameters](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) topic.</span></span>

### <a name="log-in-to-azure-and-set-the-azure-subscription"></a><span data-ttu-id="81d3c-138">Azure에 로그인하고 Azure 구독 설정</span><span class="sxs-lookup"><span data-stu-id="81d3c-138">Log in to Azure and set the Azure subscription</span></span>

<span data-ttu-id="81d3c-139">PowerShell 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="81d3c-139">From a PowerShell prompt, run the following command:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="81d3c-140">Azure 계정에 로그온하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="81d3c-140">You are prompted to log on to your Azure account.</span></span> <span data-ttu-id="81d3c-141">로그온한 후 다음 명령을 실행하여 사용 가능한 구독을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="81d3c-141">After logging on, run the following command to view your available subscriptions.</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="81d3c-142">이 명령은 사용 가능한 Azure 구독 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="81d3c-142">This command returns a list of available Azure subscriptions.</span></span> <span data-ttu-id="81d3c-143">다음 명령을 실행하여 현재 세션에 대한 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="81d3c-143">Choose a subscription for the current session by running the following command.</span></span> <span data-ttu-id="81d3c-144">`<YourSubscriptionId>`는 사용할 Azure 구독의 GUID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="81d3c-144">Replace `<YourSubscriptionId>` with the GUID for the Azure subscription you want to use.</span></span>

```powershell
Set-AzureRmContext -SubscriptionID <YourSubscriptionId>
```

### <a name="set-the-resource-group"></a><span data-ttu-id="81d3c-145">리소스 그룹 설정</span><span class="sxs-lookup"><span data-stu-id="81d3c-145">Set the resource group</span></span>

<span data-ttu-id="81d3c-146">기존 리소스 그룹이 없는 경우 **New-AzureRmResourceGroup ** 명령을 사용하여 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="81d3c-146">If you do not have an existing resource group, create a new resource group with the **New-AzureRmResourceGroup ** command.</span></span> <span data-ttu-id="81d3c-147">사용할 리소스 그룹의 이름과 위치를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="81d3c-147">Provide the name of the resource group and location you want to use.</span></span> <span data-ttu-id="81d3c-148">예:</span><span class="sxs-lookup"><span data-stu-id="81d3c-148">For example:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyDemoRG -Location "West US"
```

<span data-ttu-id="81d3c-149">성공하면 새 리소스 그룹에 대한 요약이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="81d3c-149">If successful, a summary of the new resource group is displayed.</span></span>

```powershell
ResourceGroupName : MyDemoRG
Location          : westus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/<GUID>/resourceGroups/MyDemoRG
```

### <a name="test-the-deployment"></a><span data-ttu-id="81d3c-150">배포 테스트</span><span class="sxs-lookup"><span data-stu-id="81d3c-150">Test the deployment</span></span>

<span data-ttu-id="81d3c-151">`Test-AzureRmResourceGroupDeployment` cmdlet을 실행하여 배포의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="81d3c-151">Validate your deployment by running the `Test-AzureRmResourceGroupDeployment` cmdlet.</span></span> <span data-ttu-id="81d3c-152">배포를 테스트할 때는 배포를 실행할 때처럼 정확하게 매개 변수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="81d3c-152">When testing the deployment, provide parameters exactly as you would when executing the deployment.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json
```

### <a name="create-the-deployment"></a><span data-ttu-id="81d3c-153">배포 만들기</span><span class="sxs-lookup"><span data-stu-id="81d3c-153">Create the deployment</span></span>

<span data-ttu-id="81d3c-154">새 배포를 만들려면 `New-AzureRmResourceGroupDeployment` cmdlet을 실행하고 메시지가 표시되면 필요한 매개 변수를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="81d3c-154">To create the new deployment, run the `New-AzureRmResourceGroupDeployment` cmdlet, and provide the necessary parameters when prompted.</span></span> <span data-ttu-id="81d3c-155">매개 변수에는 배포 이름, 리소스 그룹 이름 및 템플릿 파일의 경로 또는 URL이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="81d3c-155">The parameters include a name for your deployment, the name of your resource group, and the path or URL to the template file.</span></span> <span data-ttu-id="81d3c-156">**Mode** 매개 변수가 지정되지 않은 경우 기본값 **Incremental**이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="81d3c-156">If the **Mode** parameter is not specified, the default value of **Incremental** is used.</span></span> <span data-ttu-id="81d3c-157">자세한 내용은 [증분 및 전체 배포](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81d3c-157">For more information, see [Incremental and complete deployments](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).</span></span>

<span data-ttu-id="81d3c-158">다음 명령은 PowerShell 창에서 세 매개 변수의 입력을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="81d3c-158">The following command prompts you for the three parameters in the PowerShell window:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json
```

<span data-ttu-id="81d3c-159">그 대신에 매개 변수 파일을 지정하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="81d3c-159">To specify a parameters file instead, use the following command.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json -TemplateParameterFile <path to parameters file>\azuredeploy.parameters.json
```

<span data-ttu-id="81d3c-160">배포 cmdlet을 실행하면 인라인 매개 변수를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81d3c-160">You can also use inline parameters when you run the deployment cmdlet.</span></span> <span data-ttu-id="81d3c-161">이 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="81d3c-161">The command is as follows:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json -parameterName "parameterValue"
```

<span data-ttu-id="81d3c-162">[전체](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) 배포를 실행하려면 **Mode** 매개 변수를 **Complete**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="81d3c-162">To run a [complete](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) deployment, set the **Mode** parameter to **Complete**:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -Mode Complete -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json
```

### <a name="verify-the-deployment"></a><span data-ttu-id="81d3c-163">배포 확인</span><span class="sxs-lookup"><span data-stu-id="81d3c-163">Verify the deployment</span></span>
<span data-ttu-id="81d3c-164">리소스가 성공적으로 배포되면 배포의 요약이 PowerShell 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="81d3c-164">If the resources are deployed successfully, a summary of the deployment is displayed in the PowerShell window:</span></span>

```powershell
DeploymentName    : MyDemoDeployment
ResourceGroupName : MyDemoRG
ProvisioningState : Succeeded
Timestamp         : 4/19/2016 10:38:30 PM
Mode              : Incremental
TemplateLink      :
Parameters        :
                    Name             Type                       Value
                    ===============  =========================  ==========
                    serviceBusNamespaceName  String             <namespaceName>
                    serviceBusQueueName  String                 <queueName>
                    serviceBusApiVersion  String                2015-08-01

```

## <a name="next-steps"></a><span data-ttu-id="81d3c-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="81d3c-165">Next steps</span></span>
<span data-ttu-id="81d3c-166">이제 Azure Resource Manager 템플릿 배포를 위한 기본 워크플로와 명령이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="81d3c-166">You've now seen the basic workflow and commands for deploying an Azure Resource Manager template.</span></span> <span data-ttu-id="81d3c-167">자세한 내용은 다음 링크를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="81d3c-167">For more detailed information, visit the following links:</span></span>

* <span data-ttu-id="81d3c-168">[Azure Resource Manager 개요][Azure Resource Manager overview]</span><span class="sxs-lookup"><span data-stu-id="81d3c-168">[Azure Resource Manager overview][Azure Resource Manager overview]</span></span>
* <span data-ttu-id="81d3c-169">[Resource Manager 템플릿과 Azure PowerShell로 리소스 배포][Deploy resources with Azure Resource Manager templates]</span><span class="sxs-lookup"><span data-stu-id="81d3c-169">[Deploy resources with Resource Manager templates and Azure PowerShell][Deploy resources with Azure Resource Manager templates]</span></span>
* [<span data-ttu-id="81d3c-170">Azure 리소스 관리자 템플릿 작성</span><span class="sxs-lookup"><span data-stu-id="81d3c-170">Authoring Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)

[Azure Resource Manager overview]: ../azure-resource-manager/resource-group-overview.md
[Deploy resources with Azure Resource Manager templates]: ../azure-resource-manager/resource-group-template-deploy.md
[Azure Quickstart Templates gallery]: https://azure.microsoft.com/documentation/templates/?term=service+bus
