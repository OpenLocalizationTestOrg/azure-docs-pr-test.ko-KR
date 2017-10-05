---
title: "Azure Resource Manager 템플릿을 사용하여 Service Bus 네임스페이스 만들기 | Microsoft Docs"
description: "Azure Resource Manager 템플릿을 사용하여 서비스 버스 네임스페이스 만들기"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: dc0d6482-6344-4cef-8644-d4573639f5e4
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: 8fff390919a1807995646dab322b4cbe56dd0268
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-bus-namespace-using-an-azure-resource-manager-template"></a><span data-ttu-id="83f2a-103">Azure Resource Manager 템플릿을 사용하여 서비스 버스 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="83f2a-103">Create a Service Bus namespace using an Azure Resource Manager template</span></span>

<span data-ttu-id="83f2a-104">이 문서에서는 표준/기본 SKU가 있는 **메시징** 형식의 Service Bus 네임스페이스를 만드는 Azure Resource Manager 템플릿을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="83f2a-104">This article describes how to use an Azure Resource Manager template that creates a Service Bus namespace of type **Messaging** with a Standard/Basic SKU.</span></span> <span data-ttu-id="83f2a-105">이 문서는 또한 배포의 실행에 대해 지정된 매개 변수도 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="83f2a-105">The article also defines the parameters that are specified for the execution of the deployment.</span></span> <span data-ttu-id="83f2a-106">배포를 위해 이 템플릿을 사용하거나 요구 사항에 맞게 사용자 지정을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83f2a-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="83f2a-107">템플릿을 만들기에 대한 자세한 내용은 [Azure Resource Manager 템플릿 작성][Authoring Azure Resource Manager templates]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="83f2a-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="83f2a-108">전체 템플릿은 GitHub에서 [Service Bus 네임스페이스 템플릿][Service Bus namespace template]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="83f2a-108">For the complete template, see the [Service Bus namespace template][Service Bus namespace template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="83f2a-109">다음 Azure Resource Manager 템플릿은 다운로드하여 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83f2a-109">The following Azure Resource Manager templates are available for download and deployment.</span></span> 
> 
> * [<span data-ttu-id="83f2a-110">큐가 있는 서비스 버스 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="83f2a-110">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="83f2a-111">토픽 및 구독이 있는 서비스 버스 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="83f2a-111">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="83f2a-112">큐 및 권한 부여 규칙이 있는 서비스 버스 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="83f2a-112">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="83f2a-113">토픽, 구독 및 규칙이 있는 Service Bus 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="83f2a-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="83f2a-114">최신 템플릿을 확인하려면 Service Bus에 대한 [Azure 빠른 시작 템플릿][Azure Quickstart Templates] 갤러리 및 검색을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="83f2a-114">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="83f2a-115">배포할 항목</span><span class="sxs-lookup"><span data-stu-id="83f2a-115">What will you deploy?</span></span>
<span data-ttu-id="83f2a-116">이 템플릿을 사용하여 [기본, 표준 또는 프리미엄](https://azure.microsoft.com/pricing/details/service-bus/) SKU가 있는 Service Bus 네임스페이스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="83f2a-116">With this template, you will deploy a Service Bus namespace with a [Basic, Standard, or Premium](https://azure.microsoft.com/pricing/details/service-bus/) SKU.</span></span>

<span data-ttu-id="83f2a-117">배포를 자동으로 실행하려면 다음 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="83f2a-117">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="83f2a-118">[![Azure에 배포](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="83f2a-118">[![Deploy to Azure](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="83f2a-119">매개 변수</span><span class="sxs-lookup"><span data-stu-id="83f2a-119">Parameters</span></span>
<span data-ttu-id="83f2a-120">Azure 리소스 관리자와 함께 템플릿을 배포할 때 지정하고자 하는 값으로 매개 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="83f2a-120">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="83f2a-121">템플릿은 모든 매개 변수 값이 포함된 `Parameters` 라는 섹션을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="83f2a-121">The template includes a section called `Parameters` that contains all of the parameter values.</span></span> <span data-ttu-id="83f2a-122">배포하는 프로젝트에 따라 또는 환경에 따라 달라지는 이러한 값에 대한 매개 변수를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83f2a-122">You should define a parameter for those values that will vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="83f2a-123">항상 동일하게 유지되는 값으로 매개 변수를 정의하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="83f2a-123">Do not define parameters for values that will always stay the same.</span></span> <span data-ttu-id="83f2a-124">각 매개 변수 값은 배포되는 리소스를 정의하는 템플릿에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="83f2a-124">Each parameter value is used in the template to define the resources that are deployed.</span></span>

<span data-ttu-id="83f2a-125">이 템플릿은 다음 매개 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="83f2a-125">This template defines the following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="83f2a-126">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="83f2a-126">serviceBusNamespaceName</span></span>
<span data-ttu-id="83f2a-127">만들 서비스 버스 네임스페이스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="83f2a-127">The name of the Service Bus namespace to create.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string",
"metadata": { 
    "description": "Name of the Service Bus namespace" 
    }
}
```

### <a name="servicebussku"></a><span data-ttu-id="83f2a-128">serviceBusSKU</span><span class="sxs-lookup"><span data-stu-id="83f2a-128">serviceBusSKU</span></span>
<span data-ttu-id="83f2a-129">만들 서비스 버스 [SKU](https://azure.microsoft.com/pricing/details/service-bus/) 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="83f2a-129">The name of the Service Bus [SKU](https://azure.microsoft.com/pricing/details/service-bus/) to create.</span></span>

```json
"serviceBusSku": { 
    "type": "string", 
    "allowedValues": [ 
        "Basic", 
        "Standard",
        "Premium" 
    ], 
    "defaultValue": "Standard", 
    "metadata": { 
        "description": "The messaging tier for service Bus namespace" 
    } 

```

<span data-ttu-id="83f2a-130">이 매개 변수에 허용되는 값(기본, 표준 또는 프리미엄)을 정의하고, 값이 지정되지 않은 경우에는 기본값(표준)을 할당하는 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="83f2a-130">The template defines the values that are permitted for this parameter (Basic, Standard, or Premium) and assigns a default value (Standard) if no value is specified.</span></span>

<span data-ttu-id="83f2a-131">Service Bus 가격에 대한 자세한 내용은 [Service Bus 가격 및 대금 청구][Service Bus pricing and billing]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="83f2a-131">For more information about Service Bus pricing, see [Service Bus pricing and billing][Service Bus pricing and billing].</span></span>

### <a name="servicebusapiversion"></a><span data-ttu-id="83f2a-132">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="83f2a-132">serviceBusApiVersion</span></span>
<span data-ttu-id="83f2a-133">템플릿의 서비스 버스 API 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="83f2a-133">The Service Bus API version of the template.</span></span>

```json
"serviceBusApiVersion": { 
       "type": "string", 
       "defaultValue": "2015-08-01", 
       "metadata": { 
           "description": "Service Bus ApiVersion used by the template" 
       } 
```

## <a name="resources-to-deploy"></a><span data-ttu-id="83f2a-134">배포할 리소스</span><span class="sxs-lookup"><span data-stu-id="83f2a-134">Resources to deploy</span></span>
### <a name="service-bus-namespace"></a><span data-ttu-id="83f2a-135">서비스 버스 네임스페이스</span><span class="sxs-lookup"><span data-stu-id="83f2a-135">Service Bus namespace</span></span>
<span data-ttu-id="83f2a-136">**메시징**형식의 표준 서비스 버스 네임스페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="83f2a-136">Creates a standard Service Bus namespace of type **Messaging**.</span></span>

```json
"resources": [
    {
        "apiVersion": "[parameters('serviceBusApiVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "kind": "Messaging",
        "sku": {
            "name": "StandardSku",
            "tier": "Standard"
        },
        "properties": {
        }
    }
]
```

## <a name="commands-to-run-deployment"></a><span data-ttu-id="83f2a-137">배포 실행 명령</span><span class="sxs-lookup"><span data-stu-id="83f2a-137">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="83f2a-138">PowerShell</span><span class="sxs-lookup"><span data-stu-id="83f2a-138">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName <resource-group-name> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

### <a name="azure-cli"></a><span data-ttu-id="83f2a-139">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="83f2a-139">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create <my-resource-group> <my-deployment-name> --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

## <a name="next-steps"></a><span data-ttu-id="83f2a-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="83f2a-140">Next steps</span></span>
<span data-ttu-id="83f2a-141">이제 Azure Resource Manager를 사용하여 리소스를 만들고 배포했으므로 다음 문서를 참조하여 이러한 리소스를 관리하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="83f2a-141">Now that you've created and deployed resources using Azure Resource Manager, learn how to manage these resources by reading these articles:</span></span>

* [<span data-ttu-id="83f2a-142">PowerShell을 사용하여 서비스 버스 관리</span><span class="sxs-lookup"><span data-stu-id="83f2a-142">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="83f2a-143">서비스 버스 탐색기로 서비스 버스 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="83f2a-143">Manage Service Bus resources with the Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace template]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-servicebus-create-namespace/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Service Bus pricing and billing]: service-bus-pricing-billing.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
