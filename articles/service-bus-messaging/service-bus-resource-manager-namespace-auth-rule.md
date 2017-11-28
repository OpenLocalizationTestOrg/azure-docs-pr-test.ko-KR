---
title: "Azure 리소스 관리자 템플릿을 사용 하 여 서비스 버스 권한 부여 규칙을 aaaCreate | Microsoft Docs"
description: "Azure Resource Manager 템플릿을 사용하여 네임스페이스 및 큐에 대한 서비스 버스 권한 부여 규칙 만들기"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 7f1443a0-5fa8-4d90-8637-1a977ef0b1f0
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: 48df97849281d3b47e9d722d4e821c874644be59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-authorization-rule-for-namespace-and-queue-using-an-azure-resource-manager-template"></a><span data-ttu-id="69a21-103">Azure Resource Manager 템플릿을 사용하여 네임스페이스 및 큐에 대한 서비스 버스 권한 부여 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="69a21-103">Create a Service Bus authorization rule for namespace and queue using an Azure Resource Manager template</span></span>

<span data-ttu-id="69a21-104">이 문서에서는 Azure 리소스 관리자 템플릿을 toouse를 만드는 방법을 [권한 부여 규칙](service-bus-authentication-and-authorization.md#shared-access-signature-authentication) 서비스 버스 네임 스페이스 및 큐에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="69a21-104">This article shows how toouse an Azure Resource Manager template that creates an [authorization rule](service-bus-authentication-and-authorization.md#shared-access-signature-authentication) for a Service Bus namespace and queue.</span></span> <span data-ttu-id="69a21-105">에 대해 설명 합니다 방법을 toodefine 리소스 배포 되 고 toodefine 매개 변수를 hello 배포를 실행 하는 경우 지정 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="69a21-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="69a21-106">배포를 위한이 서식 파일을 사용 하거나 toomeet 사용자 지정할 수 있습니다 프로그램 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="69a21-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="69a21-107">템플릿을 만들기에 대한 자세한 내용은 [Azure Resource Manager 템플릿 작성][Authoring Azure Resource Manager templates]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69a21-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="69a21-108">Hello 전체 서식 파일에 대 한 참조 hello [서비스 버스 권한 부여 규칙 템플릿] [ Service Bus auth rule template] GitHub에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="69a21-108">For hello complete template, see hello [Service Bus authorization rule template][Service Bus auth rule template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="69a21-109">Azure 리소스 관리자 템플릿을 다음 hello 다운로드 및 배포에 사용할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="69a21-109">hello following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="69a21-110">서비스 버스 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="69a21-110">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="69a21-111">큐가 있는 서비스 버스 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="69a21-111">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="69a21-112">토픽 및 구독이 있는 서비스 버스 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="69a21-112">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="69a21-113">토픽, 구독 및 규칙이 있는 Service Bus 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="69a21-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="69a21-114">hello 최신 템플릿용으로 toocheck 방문 hello [Azure 빠른 시작 템플릿] [ Azure Quickstart Templates] 갤러리 및 "서비스 버스."에 대 한 검색</span><span class="sxs-lookup"><span data-stu-id="69a21-114">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="69a21-115">배포할 항목</span><span class="sxs-lookup"><span data-stu-id="69a21-115">What will you deploy?</span></span>
<span data-ttu-id="69a21-116">이 템플릿을 사용하여 네임스페이스 및 메시징 엔터티(이 경우에는 큐)에 대한 서비스 버스 권한 부여 규칙을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="69a21-116">With this template, you will deploy a Service Bus authorization rule for a namespace and messaging entity (in this case, a queue).</span></span>

<span data-ttu-id="69a21-117">이 템플릿은 인증에 [SAS(공유 액세스 서명)](service-bus-sas.md)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="69a21-117">This template uses [Shared Access Signature (SAS)](service-bus-sas.md) for authentication.</span></span> <span data-ttu-id="69a21-118">SAS에는 응용 프로그램 tooauthenticate tooService를 hello 네임 스페이스 또는 메시징 엔터티 (큐 또는 항목)는 특정 권한이 연결 된 hello 구성 된 선택 키를 사용 하 여 버스 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69a21-118">SAS enables applications tooauthenticate tooService Bus using an access key configured on hello namespace, or on hello messaging entity (queue or topic) with which specific rights are associated.</span></span> <span data-ttu-id="69a21-119">그런 다음이 키 toogenerate 클라이언트 tooauthenticate tooService 버스에 사용할 수 있는 SAS 토큰을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69a21-119">You can then use this key toogenerate a SAS token that clients can in turn use tooauthenticate tooService Bus.</span></span>

<span data-ttu-id="69a21-120">toorun 배포를 자동으로 hello, hello 다음 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="69a21-120">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="69a21-121">[![TooAzure 배포](./media/service-bus-resource-manager-namespace-auth-rule/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F301-servicebus-create-authrule-namespace-and-queue%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="69a21-121">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace-auth-rule/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F301-servicebus-create-authrule-namespace-and-queue%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="69a21-122">매개 변수</span><span class="sxs-lookup"><span data-stu-id="69a21-122">Parameters</span></span>

<span data-ttu-id="69a21-123">Azure 리소스 관리자와 정의한 매개 변수 값에 대 한 원하는 toospecify hello 서식 파일을 배포할 때.</span><span class="sxs-lookup"><span data-stu-id="69a21-123">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="69a21-124">hello 템플릿에 섹션이 포함 되어 `Parameters` hello 매개 변수 값이 모두 들어 있는입니다.</span><span class="sxs-lookup"><span data-stu-id="69a21-124">hello template includes a section called `Parameters` that contains all of hello parameter values.</span></span> <span data-ttu-id="69a21-125">에 배포 하는 hello 환경에 따라 또는 배포 하는 hello 프로젝트에 따라 달라 집니다는 해당 값에 대 한 매개 변수를 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69a21-125">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="69a21-126">항상 유지 되는 값 동일 hello에 대 한 매개 변수를 정의 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69a21-126">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="69a21-127">각 매개 변수 값은 배포 된 hello 템플릿 toodefine hello 리소스에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69a21-127">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="69a21-128">hello 템플릿은 매개 변수 뒤 hello를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="69a21-128">hello template defines hello following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="69a21-129">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="69a21-129">serviceBusNamespaceName</span></span>
<span data-ttu-id="69a21-130">서비스 버스 네임 스페이스 toocreate hello의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="69a21-130">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="namespaceauthorizationrulename"></a><span data-ttu-id="69a21-131">namespaceAuthorizationRuleName</span><span class="sxs-lookup"><span data-stu-id="69a21-131">namespaceAuthorizationRuleName</span></span>
<span data-ttu-id="69a21-132">hello 네임 스페이스에 대 한 hello 권한 부여 규칙의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="69a21-132">hello name of hello authorization rule for hello namespace.</span></span>

```json
"namespaceAuthorizationRuleName ": {
"type": "string"
}
```

### <a name="servicebusqueuename"></a><span data-ttu-id="69a21-133">serviceBusQueueName</span><span class="sxs-lookup"><span data-stu-id="69a21-133">serviceBusQueueName</span></span>
<span data-ttu-id="69a21-134">서비스 버스 네임 스페이스 hello hello 큐의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="69a21-134">hello name of hello queue in hello Service Bus namespace.</span></span>

```json
"serviceBusQueueName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="69a21-135">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="69a21-135">serviceBusApiVersion</span></span>
<span data-ttu-id="69a21-136">hello hello 서식 파일의 서비스 버스 API 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="69a21-136">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a><span data-ttu-id="69a21-137">리소스 toodeploy</span><span class="sxs-lookup"><span data-stu-id="69a21-137">Resources toodeploy</span></span>
<span data-ttu-id="69a21-138">**메시징**형식의 표준 서비스 버스 네임스페이스와 네임스페이스 및 엔터티에 대한 서비스 버스 권한 부여 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69a21-138">Creates a standard Service Bus namespace of type **Messaging**, and a Service Bus authorization rule for namespace and entity.</span></span>

```json
"resources": [
        {
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusNamespaceName')]",
            "type": "Microsoft.ServiceBus/namespaces",
            "location": "[variables('location')]",
            "kind": "Messaging",
            "sku": {
                "name": "StandardSku",
                "tier": "Standard"
            },
            "resources": [
                {
                    "apiVersion": "[variables('sbVersion')]",
                    "name": "[parameters('serviceBusQueueName')]",
                    "type": "Queues",
                    "dependsOn": [
                        "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
                    ],
                    "properties": {
                        "path": "[parameters('serviceBusQueueName')]"
                    },
                    "resources": [
                        {
                            "apiVersion": "[variables('sbVersion')]",
                            "name": "[parameters('queueAuthorizationRuleName')]",
                            "type": "authorizationRules",
                            "dependsOn": [
                                "[parameters('serviceBusQueueName')]"
                            ],
                            "properties": {
                                "Rights": ["Listen"]
                            }
                        }
                    ]
                }
            ]
        }, {
            "apiVersion": "[variables('sbVersion')]",
            "name": "[variables('namespaceAuthRuleName')]",
            "type": "Microsoft.ServiceBus/namespaces/authorizationRules",
            "dependsOn": ["[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"],
            "location": "[resourceGroup().location]",
            "properties": {
                "Rights": ["Send"]
            }
        }
    ]
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="69a21-139">명령 toorun 배포</span><span class="sxs-lookup"><span data-stu-id="69a21-139">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="69a21-140">PowerShell</span><span class="sxs-lookup"><span data-stu-id="69a21-140">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="69a21-141">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="69a21-141">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="69a21-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="69a21-142">Next steps</span></span>
<span data-ttu-id="69a21-143">이제 작성 되었으며 Azure 리소스 관리자를 사용 하 여 리소스를 배포, 자세히 배울 방법 toomanage 이러한 문서를 확인 하 여 이러한 리소스:</span><span class="sxs-lookup"><span data-stu-id="69a21-143">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="69a21-144">PowerShell을 사용하여 서비스 버스 관리</span><span class="sxs-lookup"><span data-stu-id="69a21-144">Manage Service Bus with PowerShell</span></span>](service-bus-powershell-how-to-provision.md)
* [<span data-ttu-id="69a21-145">서비스 버스 탐색기 hello 사용 하 여 서비스 버스 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="69a21-145">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)
* [<span data-ttu-id="69a21-146">서비스 버스 인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="69a21-146">Service Bus authentication and authorization</span></span>](service-bus-authentication-and-authorization.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus auth rule template]: https://github.com/Azure/azure-quickstart-templates/blob/master/301-servicebus-create-authrule-namespace-and-queue/
