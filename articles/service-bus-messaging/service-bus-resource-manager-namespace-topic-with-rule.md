---
title: "Azure 서비스 버스 항목 구독 aaaCreate 및 Azure 리소스 관리자 템플릿을 사용 하 여 규칙 | Microsoft Docs"
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
ms.openlocfilehash: dbc46da8491aee4d0c73bd4db90c696008920df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-with-topic-subscription-and-rule-using-an-azure-resource-manager-template"></a><span data-ttu-id="00e10-103">Azure Resource Manager 템플릿을 사용하여 토픽, 구독 및 규칙이 있는 Service Bus 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="00e10-103">Create a Service Bus namespace with topic, subscription, and rule using an Azure Resource Manager template</span></span>

<span data-ttu-id="00e10-104">이 문서에서는 어떻게 toouse Azure 리소스 관리자 템플릿을으로 만드는 서비스 버스 네임 스페이스 항목, 구독 및 규칙 (필터) 합니다.</span><span class="sxs-lookup"><span data-stu-id="00e10-104">This article shows how toouse an Azure Resource Manager template that creates a Service Bus namespace with a topic, subscription, and rule (filter).</span></span> <span data-ttu-id="00e10-105">배웁니다 어떻게 toodefine 리소스 배포 되 고 toodefine 매개 변수를 hello 배포를 실행 하는 경우 지정 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="00e10-105">You learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="00e10-106">배포를 위한이 서식 파일을 사용 하거나 toomeet 사용자 지정할 수 있습니다 프로그램 요구 사항</span><span class="sxs-lookup"><span data-stu-id="00e10-106">You can use this template for your own deployments, or customize it toomeet your requirements</span></span>

<span data-ttu-id="00e10-107">템플릿 만들기에 대한 자세한 내용은 [Azure Resource Manager 템플릿 작성하기][Authoring Azure Resource Manager templates]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00e10-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="00e10-108">Azure 리소스 명명 규칙의 사례 및 패턴에 대한 자세한 내용은 [Azure 리소스에 대한 권장되는 명명 규칙][Recommended naming conventions for Azure resources]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00e10-108">For more information about practice and patterns on Azure resources naming conventions, see [Recommended naming conventions for Azure resources][Recommended naming conventions for Azure resources].</span></span>

<span data-ttu-id="00e10-109">Hello 전체 서식 파일에 대 한 참조 hello [항목, 구독 및 규칙으로 서비스 버스 네임 스페이스] [ Service Bus namespace with topic, subscription, and rule] 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="00e10-109">For hello complete template, see hello [Service Bus namespace with topic, subscription, and rule][Service Bus namespace with topic, subscription, and rule] template.</span></span>

> [!NOTE]
> <span data-ttu-id="00e10-110">Azure 리소스 관리자 템플릿을 다음 hello 다운로드 및 배포에 사용할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="00e10-110">hello following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="00e10-111">큐 및 권한 부여 규칙이 있는 서비스 버스 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="00e10-111">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="00e10-112">큐가 있는 서비스 버스 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="00e10-112">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="00e10-113">서비스 버스 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="00e10-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="00e10-114">토픽 및 구독이 있는 서비스 버스 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="00e10-114">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> 
> <span data-ttu-id="00e10-115">hello 최신 템플릿용으로 toocheck 방문 hello [Azure 빠른 시작 템플릿] [ Azure Quickstart Templates] 갤러리 및 서비스 버스에 대 한 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="00e10-115">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="00e10-116">배포할 항목</span><span class="sxs-lookup"><span data-stu-id="00e10-116">What will you deploy?</span></span>

<span data-ttu-id="00e10-117">이 템플릿을 사용하여 토픽, 구독 및 규칙(필터)이 있는 Service Bus 네임스페이스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="00e10-117">With this template, you deploy a Service Bus namespace with topic, subscription, and rule (filter).</span></span>

<span data-ttu-id="00e10-118">[Service Bus 토픽 및 구독](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions)은 *게시/구독* 패턴으로 일 대 다 형태의 통신을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="00e10-118">[Service Bus topics and subscriptions](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span></span> <span data-ttu-id="00e10-119">배포 응용 프로그램의 구성 요소와 직접 통신 하지 않는 항목 및 구독을 사용할 때 대신 교환 하는 중간자 역할을 하는 항목을 통해 메시지입니다. 구독 tooa 항목 toohello 항목 보낸 메시지의 복사본을 받는 가상 큐와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="00e10-119">When using topics and subscriptions, components of a distributed application do not communicate directly with each other, instead they exchange messages via topic that acts as an intermediary.A subscription tooa topic resembles a virtual queue that receives copies of messages that were sent toohello topic.</span></span> <span data-ttu-id="00e10-120">구독에 대 한 필터 하면 toospecify 보낸 메시지 tooa 항목 특정 항목 구독 내에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00e10-120">A filter on subscription enables you toospecify which messages sent tooa topic should appear within a specific topic subscription.</span></span>

## <a name="what-are-rules-filters"></a><span data-ttu-id="00e10-121">규칙(필터)란?</span><span class="sxs-lookup"><span data-stu-id="00e10-121">What are rules (filters)?</span></span>

<span data-ttu-id="00e10-122">대부분의 시나리오에서 특정 특성을 가진 메시지를 다른 방법으로 처리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00e10-122">In many scenarios, messages that have specific characteristics must be processed in different ways.</span></span> <span data-ttu-id="00e10-123">tooenable이를 특정 속성을 가진 및 다음 toothose 속성 수정 작업을 수행 하는 구독 toofind 메시지를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00e10-123">tooenable this, you can configure subscriptions toofind messages that have specific properties and then perform modifications toothose properties.</span></span> <span data-ttu-id="00e10-124">서비스 버스 구독 toohello 항목 보낸 모든 메시지를 볼 있지만만 해당 메시지 toohello 가상 구독 큐의 하위 집합을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00e10-124">Although Service Bus subscriptions see all messages sent toohello topic, you can only copy a subset of those messages toohello virtual subscription queue.</span></span> <span data-ttu-id="00e10-125">구독 필터를 사용하여 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="00e10-125">This is accomplished using subscription filters.</span></span> <span data-ttu-id="00e10-126">규칙 (필터)에 대해 자세히 toolearn 참조 [규칙 및 동작](service-bus-queues-topics-subscriptions.md#rules-and-actions)합니다.</span><span class="sxs-lookup"><span data-stu-id="00e10-126">toolearn more about rules (filters), see [Rules and actions](service-bus-queues-topics-subscriptions.md#rules-and-actions).</span></span>

<span data-ttu-id="00e10-127">toorun 배포를 자동으로 hello, hello 다음 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="00e10-127">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="00e10-128">[![TooAzure 배포](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="00e10-128">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="00e10-129">매개 변수</span><span class="sxs-lookup"><span data-stu-id="00e10-129">Parameters</span></span>

<span data-ttu-id="00e10-130">Azure 리소스 관리자와 매개 변수를 정의 해야 값에 대 한 원하는 toospecify hello 서식 파일을 배포할 때.</span><span class="sxs-lookup"><span data-stu-id="00e10-130">With Azure Resource Manager, you should define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="00e10-131">hello 템플릿에 섹션이 포함 되어 `Parameters` 모든 hello 매개 변수 값이 들어 있는입니다.</span><span class="sxs-lookup"><span data-stu-id="00e10-131">hello template includes a section called `Parameters` that contains all hello parameter values.</span></span> <span data-ttu-id="00e10-132">에 배포 하는 hello 환경에 따라 또는 배포 하는 hello 프로젝트에 따라 달라 지는 해당 값에 대 한 매개 변수를 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00e10-132">You should define a parameter for those values that vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="00e10-133">동일한 값을 항상 유지 hello에 대 한 매개 변수를 정의 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="00e10-133">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="00e10-134">각 매개 변수 값은 배포 된 hello 템플릿 toodefine hello 리소스에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00e10-134">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="00e10-135">hello 템플릿 매개 변수 뒤 hello를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="00e10-135">hello template defines hello following parameters:</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="00e10-136">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="00e10-136">serviceBusNamespaceName</span></span>
<span data-ttu-id="00e10-137">서비스 버스 네임 스페이스 toocreate hello의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="00e10-137">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a><span data-ttu-id="00e10-138">serviceBusTopicName</span><span class="sxs-lookup"><span data-stu-id="00e10-138">serviceBusTopicName</span></span>
<span data-ttu-id="00e10-139">hello 서비스 버스 네임 스페이스에서 만든 hello 항목의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="00e10-139">hello name of hello topic created in hello Service Bus namespace.</span></span>

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a><span data-ttu-id="00e10-140">serviceBusSubscriptionName</span><span class="sxs-lookup"><span data-stu-id="00e10-140">serviceBusSubscriptionName</span></span>
<span data-ttu-id="00e10-141">hello 서비스 버스 네임 스페이스에서 만든 구독에 hello의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="00e10-141">hello name of hello subscription created in hello Service Bus namespace.</span></span>

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```
### <a name="servicebusrulename"></a><span data-ttu-id="00e10-142">serviceBusRuleName</span><span class="sxs-lookup"><span data-stu-id="00e10-142">serviceBusRuleName</span></span>
<span data-ttu-id="00e10-143">hello 서비스 버스 네임 스페이스에서 만든 hello rule(filter)의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="00e10-143">hello name of hello rule(filter) created in hello Service Bus namespace.</span></span>

```json
   "serviceBusRuleName": {
   "type": "string",
  }
```
### <a name="servicebusapiversion"></a><span data-ttu-id="00e10-144">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="00e10-144">serviceBusApiVersion</span></span>
<span data-ttu-id="00e10-145">hello hello 서식 파일의 서비스 버스 API 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="00e10-145">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-toodeploy"></a><span data-ttu-id="00e10-146">리소스 toodeploy</span><span class="sxs-lookup"><span data-stu-id="00e10-146">Resources toodeploy</span></span>
<span data-ttu-id="00e10-147">토픽, 구독 및 규칙이 있는 **메시징** 형식의 표준 Service Bus 네임스페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00e10-147">Creates a standard Service Bus namespace of type **Messaging**, with topic and subscription and rules.</span></span>

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

## <a name="commands-toorun-deployment"></a><span data-ttu-id="00e10-148">명령 toorun 배포</span><span class="sxs-lookup"><span data-stu-id="00e10-148">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="00e10-149">PowerShell</span><span class="sxs-lookup"><span data-stu-id="00e10-149">PowerShell</span></span>
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="00e10-150">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="00e10-150">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="00e10-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="00e10-151">Next steps</span></span>
<span data-ttu-id="00e10-152">이제 작성 되었으며 Azure 리소스 관리자를 사용 하 여 리소스를 배포, 자세히 배울 방법 toomanage 이러한 문서를 확인 하 여 이러한 리소스:</span><span class="sxs-lookup"><span data-stu-id="00e10-152">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="00e10-153">Azure Service Bus 관리</span><span class="sxs-lookup"><span data-stu-id="00e10-153">Manage Azure Service Bus</span></span>](service-bus-management-libraries.md)
* [<span data-ttu-id="00e10-154">PowerShell을 사용하여 서비스 버스 관리</span><span class="sxs-lookup"><span data-stu-id="00e10-154">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="00e10-155">서비스 버스 탐색기 hello 사용 하 여 서비스 버스 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="00e10-155">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Recommended naming conventions for Azure resources]: ../guidance/guidance-naming-conventions.md
[Service Bus namespace with topic, subscription, and rule]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-subscription-rule/
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md

