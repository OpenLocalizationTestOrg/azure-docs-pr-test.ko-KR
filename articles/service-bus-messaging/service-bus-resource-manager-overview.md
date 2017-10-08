---
title: "Azure 리소스 관리자 템플릿을 사용 하 여 aaaCreate Azure 서비스 버스 리소스 | Microsoft Docs"
description: "서비스 버스 리소스의 Azure 리소스 관리자 템플릿 tooautomate hello 생성을 사용 하 여"
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
ms.openlocfilehash: e539902cae307b63ae7c332580e2064761331ec5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-service-bus-resources-using-azure-resource-manager-templates"></a><span data-ttu-id="fdf44-103">Azure Resource Manager 템플릿을 사용하여 서비스 버스 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="fdf44-103">Create Service Bus resources using Azure Resource Manager templates</span></span>

<span data-ttu-id="fdf44-104">이 문서에서는 설명 방법을 toocreate 및 Azure 리소스 관리자 템플릿, PowerShell 및 hello 서비스 버스 리소스 공급자를 사용 하 여 서비스 버스 리소스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdf44-104">This article describes how toocreate and deploy Service Bus resources using Azure Resource Manager templates, PowerShell, and hello Service Bus resource provider.</span></span>

<span data-ttu-id="fdf44-105">Azure 리소스 관리자 템플릿을 사용 솔루션 및 toospecify 매개 변수 및 변수를 사용 하면 다양 한 환경에 대 한 tooinput 값에 대 한 리소스 toodeploy hello를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdf44-105">Azure Resource Manager templates help you define hello resources toodeploy for a solution, and toospecify parameters and variables that enable you tooinput values for different environments.</span></span> <span data-ttu-id="fdf44-106">JSON 및 배포에 대 한 tooconstruct 값을 사용할 수 있는 식의 hello 템플릿은 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fdf44-106">hello template consists of JSON and expressions that you can use tooconstruct values for your deployment.</span></span> <span data-ttu-id="fdf44-107">Azure 리소스 관리자 템플릿 및 hello 템플릿 형식에 대 한 내용은 작성에 대 한 자세한 내용은 참조 [구조 및 Azure 리소스 관리자 템플릿 구문](../azure-resource-manager/resource-group-authoring-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fdf44-107">For detailed information about writing Azure Resource Manager templates, and a discussion of hello template format, see [structure and syntax of Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

> [!NOTE]
> <span data-ttu-id="fdf44-108">이 문서 표시의 예제를 어떻게 hello toouse Azure 리소스 관리자 toocreate 서비스 버스 네임 스페이스 및 메시징 엔터티 (큐).</span><span class="sxs-lookup"><span data-stu-id="fdf44-108">hello examples in this article show how toouse Azure Resource Manager toocreate a Service Bus namespace and messaging entity (queue).</span></span> <span data-ttu-id="fdf44-109">다른 서식 파일 예제에 대 한 방문 hello [Azure 빠른 시작 템플릿 갤러리] [ Azure Quickstart Templates gallery] "서비스 버스."에 대 한 검색</span><span class="sxs-lookup"><span data-stu-id="fdf44-109">For other template examples, visit hello [Azure Quickstart Templates gallery][Azure Quickstart Templates gallery] and search for "Service Bus."</span></span>
>
>

## <a name="service-bus-resource-manager-templates"></a><span data-ttu-id="fdf44-110">Service Bus Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="fdf44-110">Service Bus Resource Manager templates</span></span>

<span data-ttu-id="fdf44-111">이러한 Service Bus Azure Resource Manager 템플릿은 다운로드하여 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdf44-111">These Service Bus Azure Resource Manager templates are available for download and deployment.</span></span> <span data-ttu-id="fdf44-112">Hello 다음 GitHub에 대 한 링크 toohello 템플릿으로 개에 대 한 세부 정보에 대 한 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdf44-112">Click hello following links for details about each one, with links toohello templates on GitHub:</span></span>

* [<span data-ttu-id="fdf44-113">서비스 버스 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="fdf44-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
* [<span data-ttu-id="fdf44-114">큐가 있는 서비스 버스 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="fdf44-114">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
* [<span data-ttu-id="fdf44-115">토픽 및 구독이 있는 서비스 버스 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="fdf44-115">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
* [<span data-ttu-id="fdf44-116">큐 및 권한 부여 규칙이 있는 서비스 버스 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="fdf44-116">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
* [<span data-ttu-id="fdf44-117">토픽, 구독 및 규칙이 있는 Service Bus 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="fdf44-117">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)

## <a name="deploy-with-powershell"></a><span data-ttu-id="fdf44-118">PowerShell을 사용하여 배포 </span><span class="sxs-lookup"><span data-stu-id="fdf44-118">Deploy with PowerShell</span></span>

<span data-ttu-id="fdf44-119">hello 다음 절차에서는 Azure 리소스 관리자 템플릿을 toouse PowerShell toodeploy를 만드는 방법을 **표준** 서비스 버스 네임 스페이스 및 해당 네임 스페이스 내에서 큐를 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="fdf44-119">hello following procedure describes how toouse PowerShell toodeploy an Azure Resource Manager template that creates a **Standard** tier Service Bus namespace, and a queue within that namespace.</span></span> <span data-ttu-id="fdf44-120">Hello을 기반으로이 예제는 [큐와 서비스 버스 네임 스페이스 만들기](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) 템플릿.</span><span class="sxs-lookup"><span data-stu-id="fdf44-120">This example is based on hello [Create a Service Bus namespace with queue](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) template.</span></span> <span data-ttu-id="fdf44-121">hello 대략적인 워크플로 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fdf44-121">hello approximate workflow is as follows:</span></span>

1. <span data-ttu-id="fdf44-122">PowerShell을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="fdf44-122">Install PowerShell.</span></span>
2. <span data-ttu-id="fdf44-123">Hello 템플릿 및 매개 변수 파일 (옵션)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fdf44-123">Create hello template and (optionally) a parameter file.</span></span>
3. <span data-ttu-id="fdf44-124">PowerShell에서 tooyour Azure 계정에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdf44-124">In PowerShell, log in tooyour Azure account.</span></span>
4. <span data-ttu-id="fdf44-125">새 리소스 그룹이 아직 없으면 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fdf44-125">Create a new resource group if one does not exist.</span></span>
5. <span data-ttu-id="fdf44-126">Hello 배포를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdf44-126">Test hello deployment.</span></span>
6. <span data-ttu-id="fdf44-127">원하는 경우 hello 배포 모드를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdf44-127">If desired, set hello deployment mode.</span></span>
7. <span data-ttu-id="fdf44-128">Hello 템플릿을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdf44-128">Deploy hello template.</span></span>

<span data-ttu-id="fdf44-129">Azure Resource Manager 배포 템플릿에 대한 모든 내용은 [Azure Resource Manager 템플릿으로 리소스 배포][Deploy resources with Azure Resource Manager templates]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fdf44-129">For complete information about deploying Azure Resource Manager templates, see [Deploy resources with Azure Resource Manager templates][Deploy resources with Azure Resource Manager templates].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="fdf44-130">PowerShell 설치 </span><span class="sxs-lookup"><span data-stu-id="fdf44-130">Install PowerShell</span></span>

<span data-ttu-id="fdf44-131">Hello 지침에 따라 Azure PowerShell 설치 [Azure PowerShell 시작](/powershell/azure/get-started-azureps)합니다.</span><span class="sxs-lookup"><span data-stu-id="fdf44-131">Install Azure PowerShell by following hello instructions in [Getting started with Azure PowerShell](/powershell/azure/get-started-azureps).</span></span>

### <a name="create-a-template"></a><span data-ttu-id="fdf44-132">템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="fdf44-132">Create a template</span></span>

<span data-ttu-id="fdf44-133">복제 또는 복사 hello [201-servicebus--큐 만들기](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) GitHub에서 템플릿:</span><span class="sxs-lookup"><span data-stu-id="fdf44-133">Clone or copy hello [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) template from GitHub:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "type": "string",
            "metadata": {
                "description": "Name of hello Service Bus namespace"
            }
        },
        "serviceBusQueueName": {
            "type": "string",
            "metadata": {
                "description": "Name of hello Queue"
            }
        },
        "serviceBusApiVersion": {
            "type": "string",
            "defaultValue": "2015-08-01",
            "metadata": {
                "description": "Service Bus ApiVersion used by hello template"
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

### <a name="create-a-parameters-file-optional"></a><span data-ttu-id="fdf44-134">매개 변수 파일 만들기(옵션)</span><span class="sxs-lookup"><span data-stu-id="fdf44-134">Create a parameters file (optional)</span></span>

<span data-ttu-id="fdf44-135">toouse 선택적 매개 변수 파일을 복사 hello [201-servicebus--큐 만들기](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="fdf44-135">toouse an optional parameters file, copy hello [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) file.</span></span> <span data-ttu-id="fdf44-136">Hello 값의 대체 `serviceBusNamespaceName` hello 서비스 버스 네임 스페이스의 hello 이름으로이 배포에 toocreate을 hello 값의 대체 `serviceBusQueueName` toocreate hello 큐의 hello 이름으로 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdf44-136">Replace hello value of `serviceBusNamespaceName` with hello name of hello Service Bus namespace you want toocreate in this deployment, and replace hello value of `serviceBusQueueName` with hello name of hello queue you want toocreate.</span></span>

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

<span data-ttu-id="fdf44-137">자세한 내용은 참조 hello [매개 변수](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="fdf44-137">For more information, see hello [Parameters](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) topic.</span></span>

### <a name="log-in-tooazure-and-set-hello-azure-subscription"></a><span data-ttu-id="fdf44-138">TooAzure를 로그인 하 고 hello Azure 구독 설정</span><span class="sxs-lookup"><span data-stu-id="fdf44-138">Log in tooAzure and set hello Azure subscription</span></span>

<span data-ttu-id="fdf44-139">PowerShell 프롬프트에서 다음 명령을 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdf44-139">From a PowerShell prompt, run hello following command:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="fdf44-140">Tooyour Azure 계정에 증명된 toolog 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fdf44-140">You are prompted toolog on tooyour Azure account.</span></span> <span data-ttu-id="fdf44-141">로그온 한 후 다음 명령 tooview hello를 사용할 수 있는 구독 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdf44-141">After logging on, run hello following command tooview your available subscriptions.</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="fdf44-142">이 명령은 사용 가능한 Azure 구독 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="fdf44-142">This command returns a list of available Azure subscriptions.</span></span> <span data-ttu-id="fdf44-143">Hello 다음 명령을 실행 하 여 hello에 대 한 구독 현재 세션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdf44-143">Choose a subscription for hello current session by running hello following command.</span></span> <span data-ttu-id="fdf44-144">대체 `<YourSubscriptionId>` 원하는 toouse hello Azure 구독에 대 한 GUID hello로 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdf44-144">Replace `<YourSubscriptionId>` with hello GUID for hello Azure subscription you want toouse.</span></span>

```powershell
Set-AzureRmContext -SubscriptionID <YourSubscriptionId>
```

### <a name="set-hello-resource-group"></a><span data-ttu-id="fdf44-145">Hello 리소스 그룹 설정</span><span class="sxs-lookup"><span data-stu-id="fdf44-145">Set hello resource group</span></span>

<span data-ttu-id="fdf44-146">기존 리소스 그룹에서 hello로 새 리소스 그룹을 만들 수 없는 경우 * * 새로 AzureRmResourceGroup * * 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="fdf44-146">If you do not have an existing resource group, create a new resource group with hello **New-AzureRmResourceGroup ** command.</span></span> <span data-ttu-id="fdf44-147">Hello 이름 hello 리소스 그룹 및 toouse 원하는 위치를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdf44-147">Provide hello name of hello resource group and location you want toouse.</span></span> <span data-ttu-id="fdf44-148">예:</span><span class="sxs-lookup"><span data-stu-id="fdf44-148">For example:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyDemoRG -Location "West US"
```

<span data-ttu-id="fdf44-149">성공 하면 hello 새 리소스 그룹의 요약이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fdf44-149">If successful, a summary of hello new resource group is displayed.</span></span>

```powershell
ResourceGroupName : MyDemoRG
Location          : westus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/<GUID>/resourceGroups/MyDemoRG
```

### <a name="test-hello-deployment"></a><span data-ttu-id="fdf44-150">Hello 배포 테스트</span><span class="sxs-lookup"><span data-stu-id="fdf44-150">Test hello deployment</span></span>

<span data-ttu-id="fdf44-151">Hello를 실행 하 여 배포를 확인 `Test-AzureRmResourceGroupDeployment` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="fdf44-151">Validate your deployment by running hello `Test-AzureRmResourceGroupDeployment` cmdlet.</span></span> <span data-ttu-id="fdf44-152">Hello 배포를 테스트할 때는 하 듯 hello 배포를 실행할 때 매개 변수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdf44-152">When testing hello deployment, provide parameters exactly as you would when executing hello deployment.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="create-hello-deployment"></a><span data-ttu-id="fdf44-153">Hello 배포 만들기</span><span class="sxs-lookup"><span data-stu-id="fdf44-153">Create hello deployment</span></span>

<span data-ttu-id="fdf44-154">toocreate hello 새 배포를 hello 실행 `New-AzureRmResourceGroupDeployment` cmdlet hello 필요한 매개 변수 대화 상자가 나타나면를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdf44-154">toocreate hello new deployment, run hello `New-AzureRmResourceGroupDeployment` cmdlet, and provide hello necessary parameters when prompted.</span></span> <span data-ttu-id="fdf44-155">hello 매개 변수, 리소스 그룹 및 hello 경로 또는 URL toohello 템플릿 파일의 hello 이름이 배포에 대 한 이름을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdf44-155">hello parameters include a name for your deployment, hello name of your resource group, and hello path or URL toohello template file.</span></span> <span data-ttu-id="fdf44-156">경우 hello **모드** 매개 변수를 지정 하지 않으면 기본값인 hello **증분** 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fdf44-156">If hello **Mode** parameter is not specified, hello default value of **Incremental** is used.</span></span> <span data-ttu-id="fdf44-157">자세한 내용은 [증분 및 전체 배포](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fdf44-157">For more information, see [Incremental and complete deployments](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).</span></span>

<span data-ttu-id="fdf44-158">안녕하세요 명령 프롬프트에 다음 hello PowerShell 창에서 세 hello 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="fdf44-158">hello following command prompts you for hello three parameters in hello PowerShell window:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

<span data-ttu-id="fdf44-159">toospecify 매개 변수 파일 대신, 다음 명령을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdf44-159">toospecify a parameters file instead, use hello following command.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -TemplateParameterFile <path tooparameters file>\azuredeploy.parameters.json
```

<span data-ttu-id="fdf44-160">Hello 배포 cmdlet을 실행 하는 경우에 인라인 매개 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdf44-160">You can also use inline parameters when you run hello deployment cmdlet.</span></span> <span data-ttu-id="fdf44-161">hello 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fdf44-161">hello command is as follows:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -parameterName "parameterValue"
```

<span data-ttu-id="fdf44-162">toorun는 [완료](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) 배포, 집합 hello **모드** 매개 변수가 너무**완료**:</span><span class="sxs-lookup"><span data-stu-id="fdf44-162">toorun a [complete](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) deployment, set hello **Mode** parameter too**Complete**:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -Mode Complete -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="verify-hello-deployment"></a><span data-ttu-id="fdf44-163">Hello 배포 확인</span><span class="sxs-lookup"><span data-stu-id="fdf44-163">Verify hello deployment</span></span>
<span data-ttu-id="fdf44-164">Hello 리소스를 성공적으로 배포 하면 hello 배포의 요약 정보 hello PowerShell 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fdf44-164">If hello resources are deployed successfully, a summary of hello deployment is displayed in hello PowerShell window:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="fdf44-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fdf44-165">Next steps</span></span>
<span data-ttu-id="fdf44-166">이제는 Azure 리소스 관리자 템플릿을 배포 하기 위한 명령과 hello 기본 워크플로 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="fdf44-166">You've now seen hello basic workflow and commands for deploying an Azure Resource Manager template.</span></span> <span data-ttu-id="fdf44-167">더 자세한 정보에 대 한 링크를 따라 hello 방문.</span><span class="sxs-lookup"><span data-stu-id="fdf44-167">For more detailed information, visit hello following links:</span></span>

* <span data-ttu-id="fdf44-168">[Azure Resource Manager 개요][Azure Resource Manager overview]</span><span class="sxs-lookup"><span data-stu-id="fdf44-168">[Azure Resource Manager overview][Azure Resource Manager overview]</span></span>
* <span data-ttu-id="fdf44-169">[Resource Manager 템플릿과 Azure PowerShell로 리소스 배포][Deploy resources with Azure Resource Manager templates]</span><span class="sxs-lookup"><span data-stu-id="fdf44-169">[Deploy resources with Resource Manager templates and Azure PowerShell][Deploy resources with Azure Resource Manager templates]</span></span>
* [<span data-ttu-id="fdf44-170">Azure 리소스 관리자 템플릿 작성</span><span class="sxs-lookup"><span data-stu-id="fdf44-170">Authoring Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)

[Azure Resource Manager overview]: ../azure-resource-manager/resource-group-overview.md
[Deploy resources with Azure Resource Manager templates]: ../azure-resource-manager/resource-group-template-deploy.md
[Azure Quickstart Templates gallery]: https://azure.microsoft.com/documentation/templates/?term=service+bus
