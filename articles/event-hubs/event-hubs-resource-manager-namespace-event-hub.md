---
title: "템플릿을 사용 하는 Azure 이벤트 허브 네임 스페이스 및 소비자 그룹 aaaCreate | Microsoft Docs"
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
ms.openlocfilehash: 74b0d6b3fbe848705e2c20e628aa4e5269b53edb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-with-event-hub-and-consumer-group-using-an-azure-resource-manager-template"></a><span data-ttu-id="05340-103">Azure Resource Manager 템플릿을 사용하여 이벤트 허브 및 소비자 그룹이 있는 Event Hubs 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="05340-103">Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template</span></span>

<span data-ttu-id="05340-104">이 문서에서는 Azure 리소스 관리자 템플릿을 toouse를 만드는 방법을 이벤트 허브 형식의 네임 스페이스 하나의 이벤트 허브와 하나의 소비자 그룹.</span><span class="sxs-lookup"><span data-stu-id="05340-104">This article shows how toouse an Azure Resource Manager template that creates a namespace of type Event Hubs, with one event hub and one consumer group.</span></span> <span data-ttu-id="05340-105">hello 방법을 보여 줍니다 문서 toodefine 리소스 배포 되 고 toodefine 매개 변수를 hello 배포를 실행 하는 경우 지정 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="05340-105">hello article shows how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="05340-106">배포를 위한이 서식 파일을 사용 하거나 toomeet 사용자 지정할 수 있습니다 프로그램 요구 사항</span><span class="sxs-lookup"><span data-stu-id="05340-106">You can use this template for your own deployments, or customize it toomeet your requirements</span></span>

<span data-ttu-id="05340-107">템플릿 만들기에 대한 자세한 내용은 [Azure Resource Manager 템플릿 작성하기][Authoring Azure Resource Manager templates]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="05340-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="05340-108">Hello 전체 서식 파일에 대 한 참조 hello [이벤트 허브 및 소비자 그룹 템플릿] [ Event Hub and consumer group template] GitHub에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05340-108">For hello complete template, see hello [Event hub and consumer group template][Event Hub and consumer group template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="05340-109">hello 최신 템플릿용으로 toocheck 방문 hello [Azure 빠른 시작 템플릿] [ Azure Quickstart Templates] 갤러리 및 이벤트 허브에 대 한 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="05340-109">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Event Hubs.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="05340-110">배포할 항목</span><span class="sxs-lookup"><span data-stu-id="05340-110">What will you deploy?</span></span>
<span data-ttu-id="05340-111">이 템플릿을 사용하여 이벤트 허브 및 소비자 그룹이 있는 이벤트 허브 네임스페이스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="05340-111">With this template, you will deploy an Event Hubs namespace with an event hub and a consumer group.</span></span>

<span data-ttu-id="05340-112">[이벤트 허브](event-hubs-what-is-event-hubs.md) 낮은 대기 시간과 높은 안정성에 대량으로 사용 되는 서비스 tooprovide 이벤트 및 원격 분석 ingress tooAzure 처리 하는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="05340-112">[Event Hubs](event-hubs-what-is-event-hubs.md) is an event processing service used tooprovide event and telemetry ingress tooAzure at massive scale, with low latency and high reliability.</span></span>

<span data-ttu-id="05340-113">toorun 배포를 자동으로 hello, hello 다음 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="05340-113">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="05340-114">[![TooAzure 배포](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="05340-114">[![Deploy tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="05340-115">매개 변수</span><span class="sxs-lookup"><span data-stu-id="05340-115">Parameters</span></span>
<span data-ttu-id="05340-116">Azure 리소스 관리자와 정의한 매개 변수 값에 대 한 원하는 toospecify hello 서식 파일을 배포할 때.</span><span class="sxs-lookup"><span data-stu-id="05340-116">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="05340-117">hello 템플릿에 섹션이 포함 되어 `Parameters` 모든 hello 매개 변수 값이 들어 있는입니다.</span><span class="sxs-lookup"><span data-stu-id="05340-117">hello template includes a section called `Parameters` that contains all hello parameter values.</span></span> <span data-ttu-id="05340-118">Hello 프로젝트를 배포 하는 기반 또는 배포 하는 hello 환경 toowhich에 따라 달라 집니다는 해당 값에 대 한 매개 변수를 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05340-118">You should define a parameter for those values that will vary, based on hello project you are deploying or based on hello environment toowhich you are deploying.</span></span> <span data-ttu-id="05340-119">동일한 값을 항상 유지 hello에 대 한 매개 변수를 정의 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05340-119">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="05340-120">배포 된 hello 리소스를 정의 하는 hello 서식 파일에서 각 매개 변수 값입니다.</span><span class="sxs-lookup"><span data-stu-id="05340-120">Each parameter value in hello template defines hello resources that are deployed.</span></span>

<span data-ttu-id="05340-121">hello 템플릿 매개 변수 뒤 hello를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="05340-121">hello template defines hello following parameters:</span></span>

### <a name="eventhubnamespacename"></a><span data-ttu-id="05340-122">eventHubNamespaceName</span><span class="sxs-lookup"><span data-stu-id="05340-122">eventHubNamespaceName</span></span>
<span data-ttu-id="05340-123">이벤트 허브 네임 스페이스 toocreate hello의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="05340-123">hello name of hello Event Hubs namespace toocreate.</span></span>

```json
"eventHubNamespaceName": {
"type": "string"
}
```

### <a name="eventhubname"></a><span data-ttu-id="05340-124">eventHubName</span><span class="sxs-lookup"><span data-stu-id="05340-124">eventHubName</span></span>
<span data-ttu-id="05340-125">hello 이벤트 허브 네임 스페이스에서 만든 hello 이벤트 허브의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="05340-125">hello name of hello event hub created in hello Event Hubs namespace.</span></span>

```json
"eventHubName": {
"type": "string"
}
```

### <a name="eventhubconsumergroupname"></a><span data-ttu-id="05340-126">eventHubConsumerGroupName</span><span class="sxs-lookup"><span data-stu-id="05340-126">eventHubConsumerGroupName</span></span>
<span data-ttu-id="05340-127">hello 이벤트 허브에 대 한 만든 hello 소비자 그룹의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="05340-127">hello name of hello consumer group created for hello event hub.</span></span>

```json
"eventHubConsumerGroupName": {
"type": "string"
}
```

### <a name="apiversion"></a><span data-ttu-id="05340-128">apiVersion</span><span class="sxs-lookup"><span data-stu-id="05340-128">apiVersion</span></span>
<span data-ttu-id="05340-129">hello 템플릿의 hello API 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="05340-129">hello API version of hello template.</span></span>

```json
"apiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a><span data-ttu-id="05340-130">리소스 toodeploy</span><span class="sxs-lookup"><span data-stu-id="05340-130">Resources toodeploy</span></span>
<span data-ttu-id="05340-131">이벤트 허브 및 소비자 그룹이 있는 **EventHubs** 형식의 네임스페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05340-131">Creates a namespace of type **EventHubs**, with an event hub and a consumer group.</span></span>

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

## <a name="commands-toorun-deployment"></a><span data-ttu-id="05340-132">명령 toorun 배포</span><span class="sxs-lookup"><span data-stu-id="05340-132">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="05340-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="05340-133">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json
```

## <a name="azure-cli"></a><span data-ttu-id="05340-134">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="05340-134">Azure CLI</span></span>
```cli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json][]
```

## <a name="next-steps"></a><span data-ttu-id="05340-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="05340-135">Next steps</span></span>
<span data-ttu-id="05340-136">Hello 다음 링크를 방문 하 여 이벤트 허브에 대 한 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05340-136">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="05340-137">이벤트 허브 개요</span><span class="sxs-lookup"><span data-stu-id="05340-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="05340-138">이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="05340-138">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="05340-139">Event Hubs FAQ</span><span class="sxs-lookup"><span data-stu-id="05340-139">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Using Azure PowerShell with Azure Resource Manager]: ../powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../xplat-cli-azure-resource-manager.md
[Event hub and consumer group template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-event-hubs-create-event-hub-and-consumer-group/
