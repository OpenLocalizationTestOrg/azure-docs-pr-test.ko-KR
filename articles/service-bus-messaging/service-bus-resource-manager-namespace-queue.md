---
title: "aaaCreate Azure 서비스 버스 네임 스페이스 및 Azure 리소스 관리자 템플릿을 사용 하 여 큐 | Microsoft Docs"
description: "Azure Resource Manager 템플릿을 사용하여 서비스 버스 네임스페이스 및 큐 만들기"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a6bfb5fd-7b98-4588-8aa1-9d5f91b599b6
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: f230878b7c557bdd80d74da0de5a85ba4ee99ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-and-a-queue-using-an-azure-resource-manager-template"></a><span data-ttu-id="3d288-103">Azure Resource Manager 템플릿을 사용하여 서비스 버스 네임스페이스 및 큐 만들기</span><span class="sxs-lookup"><span data-stu-id="3d288-103">Create a Service Bus namespace and a queue using an Azure Resource Manager template</span></span>

<span data-ttu-id="3d288-104">이 문서에서는 Azure 리소스 관리자 템플릿을 toouse를 만드는 방법을 서비스 버스 네임 스페이스와 해당 네임 스페이스 내에서 큐 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d288-104">This article shows how toouse an Azure Resource Manager template that creates a Service Bus namespace and a queue within that namespace.</span></span> <span data-ttu-id="3d288-105">에 대해 설명 합니다 방법을 toodefine 리소스 배포 되 고 toodefine 매개 변수를 hello 배포를 실행 하는 경우 지정 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d288-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="3d288-106">배포를 위한이 서식 파일을 사용 하거나 toomeet 사용자 지정할 수 있습니다 프로그램 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3d288-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="3d288-107">템플릿을 만들기에 대한 자세한 내용은 [Azure Resource Manager 템플릿 작성][Authoring Azure Resource Manager templates]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d288-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="3d288-108">Hello 전체 서식 파일에 대 한 참조 hello [서비스 버스 네임 스페이스 및 큐 템플릿] [ Service Bus namespace and queue template] GitHub에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d288-108">For hello complete template, see hello [Service Bus namespace and queue template][Service Bus namespace and queue template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="3d288-109">Azure 리소스 관리자 템플릿을 다음 hello 다운로드 및 배포에 사용할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d288-109">hello following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="3d288-110">큐 및 권한 부여 규칙이 있는 서비스 버스 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="3d288-110">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="3d288-111">토픽 및 구독이 있는 서비스 버스 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="3d288-111">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="3d288-112">서비스 버스 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="3d288-112">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="3d288-113">토픽, 구독 및 규칙이 있는 Service Bus 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="3d288-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="3d288-114">hello 최신 템플릿용으로 toocheck 방문 hello [Azure 빠른 시작 템플릿] [ Azure Quickstart Templates] 갤러리 및 "서비스 버스."에 대 한 검색</span><span class="sxs-lookup"><span data-stu-id="3d288-114">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="3d288-115">배포할 항목</span><span class="sxs-lookup"><span data-stu-id="3d288-115">What will you deploy?</span></span>

<span data-ttu-id="3d288-116">이 템플릿으로 큐가 있는 서비스 버스 네임스페이스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="3d288-116">With this template, you will deploy a Service Bus namespace with a queue.</span></span>

<span data-ttu-id="3d288-117">[서비스 버스 큐](service-bus-queues-topics-subscriptions.md#queues) 제공 선입 선출 (FIFO) 메시지 배달 tooone 또는 자세한 경쟁 소비자입니다.</span><span class="sxs-lookup"><span data-stu-id="3d288-117">[Service Bus queues](service-bus-queues-topics-subscriptions.md#queues) offer First In, First Out (FIFO) message delivery tooone or more competing consumers.</span></span>

<span data-ttu-id="3d288-118">toorun 배포를 자동으로 hello, hello 다음 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d288-118">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="3d288-119">[![TooAzure 배포](./media/service-bus-resource-manager-namespace-queue/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-queue%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="3d288-119">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace-queue/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-queue%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="3d288-120">매개 변수</span><span class="sxs-lookup"><span data-stu-id="3d288-120">Parameters</span></span>

<span data-ttu-id="3d288-121">Azure 리소스 관리자와 정의한 매개 변수 값에 대 한 원하는 toospecify hello 서식 파일을 배포할 때.</span><span class="sxs-lookup"><span data-stu-id="3d288-121">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="3d288-122">hello 템플릿에 섹션이 포함 되어 `Parameters` hello 매개 변수 값이 모두 들어 있는입니다.</span><span class="sxs-lookup"><span data-stu-id="3d288-122">hello template includes a section called `Parameters` that contains all of hello parameter values.</span></span> <span data-ttu-id="3d288-123">에 배포 하는 hello 환경에 따라 또는 배포 하는 hello 프로젝트에 따라 달라 집니다는 해당 값에 대 한 매개 변수를 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d288-123">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="3d288-124">항상 유지 되는 값 동일 hello에 대 한 매개 변수를 정의 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3d288-124">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="3d288-125">각 매개 변수 값은 배포 된 hello 템플릿 toodefine hello 리소스에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d288-125">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="3d288-126">hello 템플릿은 매개 변수 뒤 hello를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d288-126">hello template defines hello following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="3d288-127">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="3d288-127">serviceBusNamespaceName</span></span>
<span data-ttu-id="3d288-128">서비스 버스 네임 스페이스 toocreate hello의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3d288-128">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string",
"metadata": { 
    "description": "Name of hello Service Bus namespace" 
    }
}
```

### <a name="servicebusqueuename"></a><span data-ttu-id="3d288-129">serviceBusQueueName</span><span class="sxs-lookup"><span data-stu-id="3d288-129">serviceBusQueueName</span></span>
<span data-ttu-id="3d288-130">hello 서비스 버스 네임 스페이스에서 만든 hello 큐의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3d288-130">hello name of hello queue created in hello Service Bus namespace.</span></span>

```json
"serviceBusQueueName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="3d288-131">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="3d288-131">serviceBusApiVersion</span></span>
<span data-ttu-id="3d288-132">hello hello 서식 파일의 서비스 버스 API 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="3d288-132">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a><span data-ttu-id="3d288-133">리소스 toodeploy</span><span class="sxs-lookup"><span data-stu-id="3d288-133">Resources toodeploy</span></span>
<span data-ttu-id="3d288-134">큐가 있는 **메시징**형식의 표준 서비스 버스 네임스페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3d288-134">Creates a standard Service Bus namespace of type **Messaging**, with a queue.</span></span>

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
            "name": "[parameters('serviceBusQueueName')]",
            "type": "Queues",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusQueueName')]",
            }
        }]
    }]
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="3d288-135">명령 toorun 배포</span><span class="sxs-lookup"><span data-stu-id="3d288-135">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="3d288-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3d288-136">PowerShell</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-queue/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="3d288-137">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3d288-137">Azure CLI</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-queue/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="3d288-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3d288-138">Next steps</span></span>
<span data-ttu-id="3d288-139">이제 작성 되었으며 Azure 리소스 관리자를 사용 하 여 리소스를 배포, 자세히 배울 방법 toomanage 이러한 문서를 확인 하 여 이러한 리소스:</span><span class="sxs-lookup"><span data-stu-id="3d288-139">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="3d288-140">PowerShell을 사용하여 서비스 버스 관리</span><span class="sxs-lookup"><span data-stu-id="3d288-140">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="3d288-141">서비스 버스 탐색기 hello 사용 하 여 서비스 버스 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="3d288-141">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace and queue template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus queues]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
