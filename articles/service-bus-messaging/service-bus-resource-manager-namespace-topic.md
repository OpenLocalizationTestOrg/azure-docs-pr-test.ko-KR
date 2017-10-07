---
title: "Azure 리소스 관리자 템플릿을 사용 하 여 aaaCreate Azure 서비스 버스 네임 스페이스 항목 구독 | Microsoft Docs"
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
ms.openlocfilehash: 9b5f7d8710e598b73c0a7ea3daf8c300f7fa9ecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-with-topic-and-subscription-using-an-azure-resource-manager-template"></a><span data-ttu-id="3ba44-103">Azure Resource Manager 템플릿을 사용하여 토픽 및 구독이 있는 서비스 버스 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="3ba44-103">Create a Service Bus namespace with topic and subscription using an Azure Resource Manager template</span></span>

<span data-ttu-id="3ba44-104">이 문서에서는 Azure 리소스 관리자 템플릿을 toouse를 만드는 방법을 서비스 버스 네임 스페이스, 항목 및 해당 네임 스페이스 내에서 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba44-104">This article shows how toouse an Azure Resource Manager template that creates a Service Bus namespace and a topic and subscription within that namespace.</span></span> <span data-ttu-id="3ba44-105">에 대해 설명 합니다 방법을 toodefine 리소스 배포 되 고 toodefine 매개 변수를 hello 배포를 실행 하는 경우 지정 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba44-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="3ba44-106">배포를 위한이 서식 파일을 사용 하거나 toomeet 사용자 지정할 수 있습니다 프로그램 요구 사항</span><span class="sxs-lookup"><span data-stu-id="3ba44-106">You can use this template for your own deployments, or customize it toomeet your requirements</span></span>

<span data-ttu-id="3ba44-107">템플릿을 만들기에 대한 자세한 내용은 [Azure Resource Manager 템플릿 작성][Authoring Azure Resource Manager templates]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3ba44-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="3ba44-108">Hello 전체 서식 파일에 대 한 참조 hello [항목 및 구독 포함 된 서비스 버스 네임 스페이스] [ Service Bus namespace with topic and subscription] 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3ba44-108">For hello complete template, see hello [Service Bus namespace with topic and subscription][Service Bus namespace with topic and subscription] template.</span></span>

> [!NOTE]
> <span data-ttu-id="3ba44-109">Azure 리소스 관리자 템플릿을 다음 hello 다운로드 및 배포에 사용할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba44-109">hello following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="3ba44-110">서비스 버스 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="3ba44-110">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="3ba44-111">큐가 있는 서비스 버스 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="3ba44-111">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="3ba44-112">큐 및 권한 부여 규칙이 있는 서비스 버스 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="3ba44-112">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="3ba44-113">토픽, 구독 및 규칙이 있는 Service Bus 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="3ba44-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="3ba44-114">hello 최신 템플릿용으로 toocheck 방문 hello [Azure 빠른 시작 템플릿] [ Azure Quickstart Templates] 갤러리 및 "서비스 버스."에 대 한 검색</span><span class="sxs-lookup"><span data-stu-id="3ba44-114">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="3ba44-115">배포할 항목</span><span class="sxs-lookup"><span data-stu-id="3ba44-115">What will you deploy?</span></span>

<span data-ttu-id="3ba44-116">이 템플릿을 사용하여 토픽 및 구독이 있는 서비스 버스 네임스페이스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba44-116">With this template, you will deploy a Service Bus namespace with topic and subscription.</span></span>

<span data-ttu-id="3ba44-117">[Service Bus 토픽 및 구독](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions)은 *게시/구독* 패턴으로 일 대 다 형태의 통신을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba44-117">[Service Bus topics and subscriptions](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span></span>

<span data-ttu-id="3ba44-118">toorun 배포를 자동으로 hello, hello 다음 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba44-118">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="3ba44-119">[![TooAzure 배포](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-and-subscription%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="3ba44-119">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-and-subscription%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="3ba44-120">매개 변수</span><span class="sxs-lookup"><span data-stu-id="3ba44-120">Parameters</span></span>

<span data-ttu-id="3ba44-121">Azure 리소스 관리자와 정의한 매개 변수 값에 대 한 원하는 toospecify hello 서식 파일을 배포할 때.</span><span class="sxs-lookup"><span data-stu-id="3ba44-121">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="3ba44-122">hello 템플릿에 섹션이 포함 되어 `Parameters` hello 매개 변수 값이 모두 들어 있는입니다.</span><span class="sxs-lookup"><span data-stu-id="3ba44-122">hello template includes a section called `Parameters` that contains all of hello parameter values.</span></span> <span data-ttu-id="3ba44-123">에 배포 하는 hello 환경에 따라 또는 배포 하는 hello 프로젝트에 따라 달라 집니다는 해당 값에 대 한 매개 변수를 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba44-123">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="3ba44-124">항상 유지 되는 값 동일 hello에 대 한 매개 변수를 정의 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3ba44-124">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="3ba44-125">각 매개 변수 값은 배포 된 hello 템플릿 toodefine hello 리소스에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ba44-125">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="3ba44-126">hello 템플릿은 매개 변수 뒤 hello를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ba44-126">hello template defines hello following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="3ba44-127">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="3ba44-127">serviceBusNamespaceName</span></span>
<span data-ttu-id="3ba44-128">서비스 버스 네임 스페이스 toocreate hello의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3ba44-128">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a><span data-ttu-id="3ba44-129">serviceBusTopicName</span><span class="sxs-lookup"><span data-stu-id="3ba44-129">serviceBusTopicName</span></span>
<span data-ttu-id="3ba44-130">hello 서비스 버스 네임 스페이스에서 만든 hello 항목의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3ba44-130">hello name of hello topic created in hello Service Bus namespace.</span></span>

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a><span data-ttu-id="3ba44-131">serviceBusSubscriptionName</span><span class="sxs-lookup"><span data-stu-id="3ba44-131">serviceBusSubscriptionName</span></span>
<span data-ttu-id="3ba44-132">hello 서비스 버스 네임 스페이스에서 만든 구독에 hello의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3ba44-132">hello name of hello subscription created in hello Service Bus namespace.</span></span>

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="3ba44-133">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="3ba44-133">serviceBusApiVersion</span></span>
<span data-ttu-id="3ba44-134">hello hello 서식 파일의 서비스 버스 API 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="3ba44-134">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-toodeploy"></a><span data-ttu-id="3ba44-135">리소스 toodeploy</span><span class="sxs-lookup"><span data-stu-id="3ba44-135">Resources toodeploy</span></span>
<span data-ttu-id="3ba44-136">토픽 및 구독이 있는 **메시징**형식의 표준 서비스 버스 네임스페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3ba44-136">Creates a standard Service Bus namespace of type **Messaging**, with topic and subscription.</span></span>

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

## <a name="commands-toorun-deployment"></a><span data-ttu-id="3ba44-137">명령 toorun 배포</span><span class="sxs-lookup"><span data-stu-id="3ba44-137">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="3ba44-138">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ba44-138">PowerShell</span></span>
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="3ba44-139">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3ba44-139">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="3ba44-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3ba44-140">Next steps</span></span>
<span data-ttu-id="3ba44-141">이제 작성 되었으며 Azure 리소스 관리자를 사용 하 여 리소스를 배포, 자세히 배울 방법 toomanage 이러한 문서를 확인 하 여 이러한 리소스:</span><span class="sxs-lookup"><span data-stu-id="3ba44-141">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="3ba44-142">PowerShell을 사용하여 서비스 버스 관리</span><span class="sxs-lookup"><span data-stu-id="3ba44-142">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="3ba44-143">서비스 버스 탐색기 hello 사용 하 여 서비스 버스 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="3ba44-143">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus namespace with topic and subscription]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-and-subscription/
