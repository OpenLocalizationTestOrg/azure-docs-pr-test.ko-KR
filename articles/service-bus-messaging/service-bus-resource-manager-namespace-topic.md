---
title: "Azure Resource Manager 템플릿을 사용하여 Azure Service Bus 네임스페이스 토픽 및 구독 만들기 | Microsoft Docs"
description: "Azure Resource Manager 템플릿을 사용하여 토픽 및 구독이 있는 서비스 버스 네임스페이스 만들기"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: d3d55200-5c60-4b5f-822d-59974cafff0e
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: 8dd48787e7b788d249085b3110484de1a2c1d265
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-bus-namespace-with-topic-and-subscription-using-an-azure-resource-manager-template"></a><span data-ttu-id="66b1b-103">Azure Resource Manager 템플릿을 사용하여 토픽 및 구독이 있는 서비스 버스 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="66b1b-103">Create a Service Bus namespace with topic and subscription using an Azure Resource Manager template</span></span>

<span data-ttu-id="66b1b-104">이 문서에서는 해당 네임스페이스 내에 Service Bus 네임스페이스와 토픽 및 구독을 만드는 Azure Resource Manager 템플릿을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="66b1b-104">This article shows how to use an Azure Resource Manager template that creates a Service Bus namespace and a topic and subscription within that namespace.</span></span> <span data-ttu-id="66b1b-105">어떤 리소스를 배포할지 정의하는 방법 및 배포를 실행할 때 매개 변수를 지정하는 방법을 알게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66b1b-105">You will learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="66b1b-106">자체 배포를 위해 이 템플릿을 사용하거나 요구 사항에 맞게 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66b1b-106">You can use this template for your own deployments, or customize it to meet your requirements</span></span>

<span data-ttu-id="66b1b-107">템플릿을 만들기에 대한 자세한 내용은 [Azure Resource Manager 템플릿 작성][Authoring Azure Resource Manager templates]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66b1b-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="66b1b-108">전체 템플릿은 [토픽 및 구독이 있는 Service Bus 네임스페이스][Service Bus namespace with topic and subscription] 템플릿을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66b1b-108">For the complete template, see the [Service Bus namespace with topic and subscription][Service Bus namespace with topic and subscription] template.</span></span>

> [!NOTE]
> <span data-ttu-id="66b1b-109">다음 Azure Resource Manager 템플릿은 다운로드하여 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66b1b-109">The following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="66b1b-110">서비스 버스 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="66b1b-110">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="66b1b-111">큐가 있는 서비스 버스 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="66b1b-111">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="66b1b-112">큐 및 권한 부여 규칙이 있는 서비스 버스 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="66b1b-112">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="66b1b-113">토픽, 구독 및 규칙이 있는 Service Bus 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="66b1b-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="66b1b-114">최신 템플릿을 확인하려면 Service Bus에 대한 [Azure 빠른 시작 템플릿][Azure Quickstart Templates] 갤러리에서 “Service Bus”를 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="66b1b-114">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="66b1b-115">배포할 항목</span><span class="sxs-lookup"><span data-stu-id="66b1b-115">What will you deploy?</span></span>

<span data-ttu-id="66b1b-116">이 템플릿을 사용하여 토픽 및 구독이 있는 서비스 버스 네임스페이스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="66b1b-116">With this template, you will deploy a Service Bus namespace with topic and subscription.</span></span>

<span data-ttu-id="66b1b-117">[Service Bus 토픽 및 구독](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions)은 *게시/구독* 패턴으로 일 대 다 형태의 통신을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="66b1b-117">[Service Bus topics and subscriptions](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span></span>

<span data-ttu-id="66b1b-118">배포를 자동으로 실행하려면 다음 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="66b1b-118">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="66b1b-119">[![Azure에 배포](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-and-subscription%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="66b1b-119">[![Deploy to Azure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-and-subscription%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="66b1b-120">매개 변수</span><span class="sxs-lookup"><span data-stu-id="66b1b-120">Parameters</span></span>

<span data-ttu-id="66b1b-121">Azure 리소스 관리자와 함께 템플릿을 배포할 때 지정하고자 하는 값으로 매개 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="66b1b-121">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="66b1b-122">템플릿은 모든 매개 변수 값이 포함된 `Parameters` 라는 섹션을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="66b1b-122">The template includes a section called `Parameters` that contains all of the parameter values.</span></span> <span data-ttu-id="66b1b-123">배포하는 프로젝트에 따라 또는 환경에 따라 달라지는 이러한 값에 대한 매개 변수를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66b1b-123">You should define a parameter for those values that will vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="66b1b-124">항상 동일하게 유지되는 값으로 매개 변수를 정의하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="66b1b-124">Do not define parameters for values that will always stay the same.</span></span> <span data-ttu-id="66b1b-125">각 매개 변수 값은 배포되는 리소스를 정의하는 템플릿에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="66b1b-125">Each parameter value is used in the template to define the resources that are deployed.</span></span>

<span data-ttu-id="66b1b-126">템플릿은 다음 매개 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="66b1b-126">The template defines the following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="66b1b-127">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="66b1b-127">serviceBusNamespaceName</span></span>
<span data-ttu-id="66b1b-128">만들 서비스 버스 네임스페이스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="66b1b-128">The name of the Service Bus namespace to create.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a><span data-ttu-id="66b1b-129">serviceBusTopicName</span><span class="sxs-lookup"><span data-stu-id="66b1b-129">serviceBusTopicName</span></span>
<span data-ttu-id="66b1b-130">서비스 버스 네임스페이스에서 만든 토픽의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="66b1b-130">The name of the topic created in the Service Bus namespace.</span></span>

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a><span data-ttu-id="66b1b-131">serviceBusSubscriptionName</span><span class="sxs-lookup"><span data-stu-id="66b1b-131">serviceBusSubscriptionName</span></span>
<span data-ttu-id="66b1b-132">서비스 버스 네임스페이스에서 만든 구독의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="66b1b-132">The name of the subscription created in the Service Bus namespace.</span></span>

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="66b1b-133">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="66b1b-133">serviceBusApiVersion</span></span>
<span data-ttu-id="66b1b-134">템플릿의 서비스 버스 API 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="66b1b-134">The Service Bus API version of the template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-to-deploy"></a><span data-ttu-id="66b1b-135">배포할 리소스</span><span class="sxs-lookup"><span data-stu-id="66b1b-135">Resources to deploy</span></span>
<span data-ttu-id="66b1b-136">토픽 및 구독이 있는 **메시징**형식의 표준 서비스 버스 네임스페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="66b1b-136">Creates a standard Service Bus namespace of type **Messaging**, with topic and subscription.</span></span>

```json
"resources ": [{
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
            "name": "[parameters('serviceBusTopicName')]",
            "type": "Topics",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusTopicName')]",
            },
            "resources": [{
                "apiVersion": "[variables('sbVersion')]",
                "name": "[parameters('serviceBusSubscriptionName')]",
                "type": "Subscriptions",
                "dependsOn": [
                    "[parameters('serviceBusTopicName')]"
                ],
                "properties": {}
            }]
        }]
    }]
```

## <a name="commands-to-run-deployment"></a><span data-ttu-id="66b1b-137">배포 실행 명령</span><span class="sxs-lookup"><span data-stu-id="66b1b-137">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="66b1b-138">PowerShell</span><span class="sxs-lookup"><span data-stu-id="66b1b-138">PowerShell</span></span>
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="66b1b-139">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="66b1b-139">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="66b1b-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="66b1b-140">Next steps</span></span>
<span data-ttu-id="66b1b-141">이제 Azure Resource Manager를 사용하여 리소스를 만들고 배포했으므로 다음 문서를 참조하여 이러한 리소스를 관리하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="66b1b-141">Now that you've created and deployed resources using Azure Resource Manager, learn how to manage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="66b1b-142">PowerShell을 사용하여 서비스 버스 관리</span><span class="sxs-lookup"><span data-stu-id="66b1b-142">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="66b1b-143">서비스 버스 탐색기로 서비스 버스 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="66b1b-143">Manage Service Bus resources with the Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus namespace with topic and subscription]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-and-subscription/
