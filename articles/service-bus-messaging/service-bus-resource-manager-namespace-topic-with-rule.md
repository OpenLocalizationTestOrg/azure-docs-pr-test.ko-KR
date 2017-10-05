---
title: "Azure Resource Manager 템플릿을 사용하여 Service Bus 토픽 구독 및 규칙 만들기 | Microsoft Docs"
description: "Azure Resource Manager 템플릿을 사용하여 토픽, 구독 및 규칙이 있는 Service Bus 네임스페이스 만들기"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 9e0aaf58-0214-4bca-bd00-d29c08f9b1bc
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: 35e67d86b42358c4ce28b41beae1ee8e1896e939
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-bus-namespace-with-topic-subscription-and-rule-using-an-azure-resource-manager-template"></a><span data-ttu-id="6e505-103">Azure Resource Manager 템플릿을 사용하여 토픽, 구독 및 규칙이 있는 Service Bus 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="6e505-103">Create a Service Bus namespace with topic, subscription, and rule using an Azure Resource Manager template</span></span>

<span data-ttu-id="6e505-104">이 문서에서는 토픽, 구독 및 규칙(필터)이 있는 Service Bus 네임스페이스를 만드는 Azure Resource Manager 템플릿을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6e505-104">This article shows how to use an Azure Resource Manager template that creates a Service Bus namespace with a topic, subscription, and rule (filter).</span></span> <span data-ttu-id="6e505-105">어떤 리소스를 배포할지 정의하는 방법 및 배포를 실행할 때 매개 변수를 지정하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6e505-105">You learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="6e505-106">자체 배포를 위해 이 템플릿을 사용하거나 요구 사항에 맞게 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e505-106">You can use this template for your own deployments, or customize it to meet your requirements</span></span>

<span data-ttu-id="6e505-107">템플릿 만들기에 관한 자세한 내용은 [Azure Resource Manager 템플릿 작성][Authoring Azure Resource Manager templates]을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="6e505-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="6e505-108">Azure 리소스 명명 규칙의 사례 및 패턴에 대한 자세한 내용은 [Azure 리소스에 대한 권장되는 명명 규칙][Recommended naming conventions for Azure resources]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6e505-108">For more information about practice and patterns on Azure resources naming conventions, see [Recommended naming conventions for Azure resources][Recommended naming conventions for Azure resources].</span></span>

<span data-ttu-id="6e505-109">전체 템플릿은 [토픽, 구독 및 규칙이 있는 Service Bus 네임스페이스][Service Bus namespace with topic, subscription, and rule] 템플릿을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6e505-109">For the complete template, see the [Service Bus namespace with topic, subscription, and rule][Service Bus namespace with topic, subscription, and rule] template.</span></span>

> [!NOTE]
> <span data-ttu-id="6e505-110">다음 Azure Resource Manager 템플릿은 다운로드하여 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e505-110">The following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="6e505-111">큐 및 권한 부여 규칙이 있는 서비스 버스 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="6e505-111">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="6e505-112">큐가 있는 서비스 버스 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="6e505-112">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="6e505-113">서비스 버스 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="6e505-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="6e505-114">토픽 및 구독이 있는 서비스 버스 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="6e505-114">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> 
> <span data-ttu-id="6e505-115">최신 템플릿을 확인하려면 Service Bus에 대한 [Azure 빠른 시작 템플릿][Azure Quickstart Templates] 갤러리 및 검색을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="6e505-115">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="6e505-116">배포할 항목</span><span class="sxs-lookup"><span data-stu-id="6e505-116">What will you deploy?</span></span>

<span data-ttu-id="6e505-117">이 템플릿을 사용하여 토픽, 구독 및 규칙(필터)이 있는 Service Bus 네임스페이스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="6e505-117">With this template, you deploy a Service Bus namespace with topic, subscription, and rule (filter).</span></span>

<span data-ttu-id="6e505-118">[Service Bus 토픽 및 구독](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions)은 *게시/구독* 패턴으로 일 대 다 형태의 통신을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6e505-118">[Service Bus topics and subscriptions](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span></span> <span data-ttu-id="6e505-119">토픽 및 구독을 사용하는 경우, 분산된 응용 프로그램의 구성 요소는 서로 직접 통신하지 않으며 대신 중간 단계로 사용되는 토픽을 통해 메시지를 교환합니다. 토픽 구독은 토픽에 전송된 메시지의 복사본을 받는 가상 큐와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="6e505-119">When using topics and subscriptions, components of a distributed application do not communicate directly with each other, instead they exchange messages via topic that acts as an intermediary.A subscription to a topic resembles a virtual queue that receives copies of messages that were sent to the topic.</span></span> <span data-ttu-id="6e505-120">구독에서 필터를 사용하여 토픽에 전송된 메시지 중 특정 토픽 구독 내에 표시되어야 하는 메시지를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e505-120">A filter on subscription enables you to specify which messages sent to a topic should appear within a specific topic subscription.</span></span>

## <a name="what-are-rules-filters"></a><span data-ttu-id="6e505-121">규칙(필터)란?</span><span class="sxs-lookup"><span data-stu-id="6e505-121">What are rules (filters)?</span></span>

<span data-ttu-id="6e505-122">대부분의 시나리오에서 특정 특성을 가진 메시지를 다른 방법으로 처리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e505-122">In many scenarios, messages that have specific characteristics must be processed in different ways.</span></span> <span data-ttu-id="6e505-123">이 기능을 사용하려면 구독을 구성하여 특정 속성을 갖는 메시지를 찾은 다음 해당 속성에 수정 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e505-123">To enable this, you can configure subscriptions to find messages that have specific properties and then perform modifications to those properties.</span></span> <span data-ttu-id="6e505-124">Service Bus 구독이 토픽으로 전송된 모든 메시지를 확인하지만 가상 구독 큐로 이러한 메시지의 하위 집합을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e505-124">Although Service Bus subscriptions see all messages sent to the topic, you can only copy a subset of those messages to the virtual subscription queue.</span></span> <span data-ttu-id="6e505-125">구독 필터를 사용하여 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6e505-125">This is accomplished using subscription filters.</span></span> <span data-ttu-id="6e505-126">규칙(필터)에 대한 자세한 내용은 [규칙 및 작업](service-bus-queues-topics-subscriptions.md#rules-and-actions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6e505-126">To learn more about rules (filters), see [Rules and actions](service-bus-queues-topics-subscriptions.md#rules-and-actions).</span></span>

<span data-ttu-id="6e505-127">배포를 자동으로 실행하려면 다음 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6e505-127">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="6e505-128">[![Azure에 배포](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="6e505-128">[![Deploy to Azure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="6e505-129">parameters</span><span class="sxs-lookup"><span data-stu-id="6e505-129">Parameters</span></span>

<span data-ttu-id="6e505-130">Azure Resource Manager와 함께 템플릿을 배포할 때 지정하고자 하는 값으로 매개 변수를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e505-130">With Azure Resource Manager, you should define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="6e505-131">템플릿은 모든 매개 변수 값이 포함된 `Parameters` 라는 섹션을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6e505-131">The template includes a section called `Parameters` that contains all the parameter values.</span></span> <span data-ttu-id="6e505-132">배포하는 프로젝트에 따라 또는 환경에 따라 달라지는 이러한 값에 대한 매개 변수를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e505-132">You should define a parameter for those values that vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="6e505-133">항상 동일하게 유지되는 값으로 매개 변수를 정의하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="6e505-133">Do not define parameters for values that always stay the same.</span></span> <span data-ttu-id="6e505-134">각 매개 변수 값은 배포되는 리소스를 정의하는 템플릿에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e505-134">Each parameter value is used in the template to define the resources that are deployed.</span></span>

<span data-ttu-id="6e505-135">템플릿은 다음 매개 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="6e505-135">The template defines the following parameters:</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="6e505-136">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="6e505-136">serviceBusNamespaceName</span></span>
<span data-ttu-id="6e505-137">만들 서비스 버스 네임스페이스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6e505-137">The name of the Service Bus namespace to create.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a><span data-ttu-id="6e505-138">serviceBusTopicName</span><span class="sxs-lookup"><span data-stu-id="6e505-138">serviceBusTopicName</span></span>
<span data-ttu-id="6e505-139">서비스 버스 네임스페이스에서 만든 토픽의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6e505-139">The name of the topic created in the Service Bus namespace.</span></span>

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a><span data-ttu-id="6e505-140">serviceBusSubscriptionName</span><span class="sxs-lookup"><span data-stu-id="6e505-140">serviceBusSubscriptionName</span></span>
<span data-ttu-id="6e505-141">서비스 버스 네임스페이스에서 만든 구독의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6e505-141">The name of the subscription created in the Service Bus namespace.</span></span>

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```
### <a name="servicebusrulename"></a><span data-ttu-id="6e505-142">serviceBusRuleName</span><span class="sxs-lookup"><span data-stu-id="6e505-142">serviceBusRuleName</span></span>
<span data-ttu-id="6e505-143">Service Bus 네임스페이스에서 만든 규칙(필터)의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6e505-143">The name of the rule(filter) created in the Service Bus namespace.</span></span>

```json
   "serviceBusRuleName": {
   "type": "string",
  }
```
### <a name="servicebusapiversion"></a><span data-ttu-id="6e505-144">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="6e505-144">serviceBusApiVersion</span></span>
<span data-ttu-id="6e505-145">템플릿의 서비스 버스 API 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="6e505-145">The Service Bus API version of the template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-to-deploy"></a><span data-ttu-id="6e505-146">배포할 리소스</span><span class="sxs-lookup"><span data-stu-id="6e505-146">Resources to deploy</span></span>
<span data-ttu-id="6e505-147">토픽, 구독 및 규칙이 있는 **메시징** 형식의 표준 Service Bus 네임스페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6e505-147">Creates a standard Service Bus namespace of type **Messaging**, with topic and subscription and rules.</span></span>

```json
 "resources": [{
        "apiVersion": "[variables('sbVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "sku": {
            "name": "Standard",
            "tier": "Standard"
        },
        "resources": [{
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusTopicName')]",
            "type": "Topics",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusTopicName')]"
            },
            "resources": [{
                "apiVersion": "[variables('sbVersion')]",
                "name": "[parameters('serviceBusSubscriptionName')]",
                "type": "Subscriptions",
                "dependsOn": [
                    "[parameters('serviceBusTopicName')]"
                ],
                "properties": {},
                "resources": [{
                    "apiVersion": "[variables('sbVersion')]",
                    "name": "[parameters('serviceBusRuleName')]",
                    "type": "Rules",
                    "dependsOn": [
                        "[parameters('serviceBusSubscriptionName')]"
                    ],
                    "properties": {
                        "filter": {
                            "sqlExpression": "StoreName = 'Store1'"
                        },
                        "action": {
                            "sqlExpression": "set FilterTag = 'true'"
                        }
                    }
                }]
            }]
        }]
    }]
```

## <a name="commands-to-run-deployment"></a><span data-ttu-id="6e505-148">배포 실행 명령</span><span class="sxs-lookup"><span data-stu-id="6e505-148">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="6e505-149">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6e505-149">PowerShell</span></span>
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="6e505-150">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6e505-150">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="6e505-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6e505-151">Next steps</span></span>
<span data-ttu-id="6e505-152">이제 Azure Resource Manager를 사용하여 리소스를 만들고 배포했으므로 다음 문서를 참조하여 이러한 리소스를 관리하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6e505-152">Now that you've created and deployed resources using Azure Resource Manager, learn how to manage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="6e505-153">Azure Service Bus 관리</span><span class="sxs-lookup"><span data-stu-id="6e505-153">Manage Azure Service Bus</span></span>](service-bus-management-libraries.md)
* [<span data-ttu-id="6e505-154">PowerShell을 사용하여 서비스 버스 관리</span><span class="sxs-lookup"><span data-stu-id="6e505-154">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="6e505-155">서비스 버스 탐색기로 서비스 버스 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="6e505-155">Manage Service Bus resources with the Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Recommended naming conventions for Azure resources]: ../guidance/guidance-naming-conventions.md
[Service Bus namespace with topic, subscription, and rule]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-subscription-rule/
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md

