---
title: "템플릿을 사용하여 Azure Event Hubs 네임스페이스 및 소비자 그룹 만들기 | Microsoft Docs"
description: "Azure Resource Manager 템플릿을 사용하여 이벤트 허브 및 소비자 그룹이 있는 Event Hubs 네임스페이스 만들기"
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 28bb4591-1fd7-444f-a327-4e67e8878798
ms.service: event-hubs
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/12/2017
ms.author: sethm;shvija
ms.openlocfilehash: eb9a80eec0326aaa605cb8b21aecbaeec94ff212
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-event-hubs-namespace-with-event-hub-and-consumer-group-using-an-azure-resource-manager-template"></a><span data-ttu-id="65e79-103">Azure Resource Manager 템플릿을 사용하여 이벤트 허브 및 소비자 그룹이 있는 Event Hubs 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="65e79-103">Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template</span></span>

<span data-ttu-id="65e79-104">이 문서에서는 Azure Resource Manager 템플릿을 사용하여 하나의 이벤트 허브 및 하나의 소비자 그룹이 있는 Event Hubs 형식의 네임스페이스를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="65e79-104">This article shows how to use an Azure Resource Manager template that creates a namespace of type Event Hubs, with one event hub and one consumer group.</span></span> <span data-ttu-id="65e79-105">또한 어떤 리소스를 배포할지 정의하는 방법 및 배포를 실행할 때 매개 변수를 지정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="65e79-105">The article shows how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="65e79-106">자체 배포를 위해 이 템플릿을 사용하거나 요구 사항에 맞게 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65e79-106">You can use this template for your own deployments, or customize it to meet your requirements</span></span>

<span data-ttu-id="65e79-107">템플릿 만들기에 대한 자세한 내용은 [Azure Resource Manager 템플릿 작성하기][Authoring Azure Resource Manager templates]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="65e79-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="65e79-108">전체 템플릿은 GitHub에서 [이벤트 허브 및 소비자 그룹 템플릿][Event Hub and consumer group template]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="65e79-108">For the complete template, see the [Event hub and consumer group template][Event Hub and consumer group template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="65e79-109">최신 템플릿을 확인하려면 [Azure 빠른 시작 템플릿][Azure Quickstart Templates] 갤러리를 방문하여 이벤트 허브를 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="65e79-109">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Event Hubs.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="65e79-110">배포할 항목</span><span class="sxs-lookup"><span data-stu-id="65e79-110">What will you deploy?</span></span>
<span data-ttu-id="65e79-111">이 템플릿을 사용하여 이벤트 허브 및 소비자 그룹이 있는 이벤트 허브 네임스페이스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="65e79-111">With this template, you will deploy an Event Hubs namespace with an event hub and a consumer group.</span></span>

<span data-ttu-id="65e79-112">[이벤트 허브](event-hubs-what-is-event-hubs.md) 는 짧은 대기 시간 및 높은 안정성으로 이벤트 및 원격 분석을 엄청난 규모의 Azure에 제공하는 데 사용되는 이벤트 ingestor 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="65e79-112">[Event Hubs](event-hubs-what-is-event-hubs.md) is an event processing service used to provide event and telemetry ingress to Azure at massive scale, with low latency and high reliability.</span></span>

<span data-ttu-id="65e79-113">배포를 자동으로 실행하려면 다음 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="65e79-113">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="65e79-114">[![Azure에 배포](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="65e79-114">[![Deploy to Azure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="65e79-115">매개 변수</span><span class="sxs-lookup"><span data-stu-id="65e79-115">Parameters</span></span>
<span data-ttu-id="65e79-116">Azure 리소스 관리자와 함께 템플릿을 배포할 때 지정하고자 하는 값으로 매개 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="65e79-116">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="65e79-117">템플릿은 모든 매개 변수 값이 포함된 `Parameters` 라는 섹션을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="65e79-117">The template includes a section called `Parameters` that contains all the parameter values.</span></span> <span data-ttu-id="65e79-118">배포하는 프로젝트에 따라 또는 환경에 따라 달라지는 이러한 값에 대한 매개 변수를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65e79-118">You should define a parameter for those values that will vary, based on the project you are deploying or based on the environment to which you are deploying.</span></span> <span data-ttu-id="65e79-119">항상 동일하게 유지되는 값으로 매개 변수를 정의하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="65e79-119">Do not define parameters for values that always stay the same.</span></span> <span data-ttu-id="65e79-120">템플릿의 각 매개 변수 값은 배포되는 리소스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="65e79-120">Each parameter value in the template defines the resources that are deployed.</span></span>

<span data-ttu-id="65e79-121">템플릿은 다음 매개 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="65e79-121">The template defines the following parameters:</span></span>

### <a name="eventhubnamespacename"></a><span data-ttu-id="65e79-122">eventHubNamespaceName</span><span class="sxs-lookup"><span data-stu-id="65e79-122">eventHubNamespaceName</span></span>
<span data-ttu-id="65e79-123">만들 이벤트 허브 네임스페이스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="65e79-123">The name of the Event Hubs namespace to create.</span></span>

```json
"eventHubNamespaceName": {
"type": "string"
}
```

### <a name="eventhubname"></a><span data-ttu-id="65e79-124">eventHubName</span><span class="sxs-lookup"><span data-stu-id="65e79-124">eventHubName</span></span>
<span data-ttu-id="65e79-125">Event Hubs 네임스페이스에서 만든 이벤트 허브의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="65e79-125">The name of the event hub created in the Event Hubs namespace.</span></span>

```json
"eventHubName": {
"type": "string"
}
```

### <a name="eventhubconsumergroupname"></a><span data-ttu-id="65e79-126">eventHubConsumerGroupName</span><span class="sxs-lookup"><span data-stu-id="65e79-126">eventHubConsumerGroupName</span></span>
<span data-ttu-id="65e79-127">이벤트 허브용으로 만든 소비자 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="65e79-127">The name of the consumer group created for the event hub.</span></span>

```json
"eventHubConsumerGroupName": {
"type": "string"
}
```

### <a name="apiversion"></a><span data-ttu-id="65e79-128">apiVersion</span><span class="sxs-lookup"><span data-stu-id="65e79-128">apiVersion</span></span>
<span data-ttu-id="65e79-129">템플릿의 API 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="65e79-129">The API version of the template.</span></span>

```json
"apiVersion": {
"type": "string"
}
```

## <a name="resources-to-deploy"></a><span data-ttu-id="65e79-130">배포할 리소스</span><span class="sxs-lookup"><span data-stu-id="65e79-130">Resources to deploy</span></span>
<span data-ttu-id="65e79-131">이벤트 허브 및 소비자 그룹이 있는 **EventHubs** 형식의 네임스페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="65e79-131">Creates a namespace of type **EventHubs**, with an event hub and a consumer group.</span></span>

```json
"resources":[  
      {  
         "apiVersion":"[variables('ehVersion')]",
         "name":"[parameters('namespaceName')]",
         "type":"Microsoft.EventHub/namespaces",
         "location":"[variables('location')]",
         "sku":{  
            "name":"Standard",
            "tier":"Standard"
         },
         "resources":[  
            {  
               "apiVersion":"[variables('ehVersion')]",
               "name":"[parameters('eventHubName')]",
               "type":"EventHubs",
               "dependsOn":[  
                  "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
               ],
               "properties":{  
                  "path":"[parameters('eventHubName')]"
               },
               "resources":[  
                  {  
                     "apiVersion":"[variables('ehVersion')]",
                     "name":"[parameters('consumerGroupName')]",
                     "type":"ConsumerGroups",
                     "dependsOn":[  
                        "[parameters('eventHubName')]"
                     ],
                     "properties":{  

                     }
                  }
               ]
            }
         ]
      }
   ],
```

## <a name="commands-to-run-deployment"></a><span data-ttu-id="65e79-132">배포 실행 명령</span><span class="sxs-lookup"><span data-stu-id="65e79-132">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="65e79-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="65e79-133">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json
```

## <a name="azure-cli"></a><span data-ttu-id="65e79-134">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="65e79-134">Azure CLI</span></span>
```cli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json][]
```

## <a name="next-steps"></a><span data-ttu-id="65e79-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="65e79-135">Next steps</span></span>
<span data-ttu-id="65e79-136">Event Hubs에 대한 자세한 내용은 다음 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="65e79-136">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="65e79-137">이벤트 허브 개요</span><span class="sxs-lookup"><span data-stu-id="65e79-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="65e79-138">이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="65e79-138">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="65e79-139">Event Hubs FAQ</span><span class="sxs-lookup"><span data-stu-id="65e79-139">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Using Azure PowerShell with Azure Resource Manager]: ../powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../xplat-cli-azure-resource-manager.md
[Event hub and consumer group template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-event-hubs-create-event-hub-and-consumer-group/
