---
title: "템플릿을 사용하여 Azure Event Hubs 네임스페이스를 만들고 캡처를 사용하도록 설정 | Microsoft Docs"
description: "Azure Resource Manager 템플릿을 사용하여 하나의 이벤트 허브가 있는 Azure Event Hubs 네임스페이스를 만들고 캡처를 사용하도록 설정"
services: event-hubs
documentationcenter: .net
author: ShubhaVijayasarathy
manager: timlt
editor: 
ms.assetid: 8bdda6a2-5ff1-45e3-b696-c553768f1090
ms.service: event-hubs
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/28/2017
ms.author: sethm
ms.openlocfilehash: 19bbb51868e767aa1d15f4574628b7fd36607207
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-event-hubs-namespace-with-an-event-hub-and-enable-capture-using-an-azure-resource-manager-template"></a><span data-ttu-id="0ad4b-103">Azure Resource Manager 템플릿을 사용하여 하나의 이벤트 허브가 있는 Event Hubs 네임스페이스를 만들고 캡처를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="0ad4b-103">Create an Event Hubs namespace with an event hub and enable Capture using an Azure Resource Manager template</span></span>

<span data-ttu-id="0ad4b-104">이 문서에서는 Azure Resource Manager 템플릿을 사용하여 하나의 이벤트 허브 인스턴스가 있는 Event Hubs 네임스페이스를 만들고 해당 이벤트 허브에서 [캡처 기능](event-hubs-capture-overview.md)을 사용하도록 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-104">This article shows how to use an Azure Resource Manager template that creates an Event Hubs namespace, with one event hub instance, and also enables the [Capture feature](event-hubs-capture-overview.md) on the event hub.</span></span> <span data-ttu-id="0ad4b-105">또한 어떤 리소스를 배포할지 정의하는 방법 및 배포를 실행할 때 매개 변수를 지정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-105">The article describes how to define which resources are deployed, and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="0ad4b-106">배포를 위해 이 템플릿을 사용하거나 요구 사항에 맞게 사용자 지정을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="0ad4b-107">이 문서에는 선택한 대상에 따라 이벤트가 Azure Storage Blobs에 캡처되는지, 아니면 Azure Data Lake Store에 캡쳐되는지를 지정하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-107">This article also shows how to specify that events are captured into either Azure Storage Blobs or an Azure Data Lake Store, based on the destination you choose.</span></span>

<span data-ttu-id="0ad4b-108">템플릿 만들기에 대한 자세한 내용은 [Azure Resource Manager 템플릿 작성하기][Authoring Azure Resource Manager templates]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-108">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="0ad4b-109">Azure 리소스 명명 규칙의 패턴 및 사례에 대한 자세한 내용은 [Azure 리소스 명명 규칙][Azure Resources naming conventions]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-109">For more information about patterns and practices for Azure Resources naming conventions, see [Azure Resources naming conventions][Azure Resources naming conventions].</span></span>

<span data-ttu-id="0ad4b-110">전체 템플릿은 다음 GitHub 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-110">For the complete templates, click the following GitHub links:</span></span>

- <span data-ttu-id="0ad4b-111">[이벤트 허브 및 저장소 템플릿에 캡처 사용][Event Hub and enable Capture to Storage template]</span><span class="sxs-lookup"><span data-stu-id="0ad4b-111">[Event hub and enable Capture to Storage template][Event Hub and enable Capture to Storage template]</span></span> 
- <span data-ttu-id="0ad4b-112">[이벤트 허브 및 Azure Data Lake Store 템플릿에 캡처 사용][Event Hub and enable Capture to Azure Data Lake Store template]</span><span class="sxs-lookup"><span data-stu-id="0ad4b-112">[Event hub and enable Capture to Azure Data Lake Store template][Event Hub and enable Capture to Azure Data Lake Store template]</span></span>

> [!NOTE]
> <span data-ttu-id="0ad4b-113">최신 템플릿을 확인하려면 [Azure 빠른 시작 템플릿][Azure Quickstart Templates] 갤러리를 방문하여 이벤트 허브를 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-113">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Event Hubs.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="0ad4b-114">배포할 항목</span><span class="sxs-lookup"><span data-stu-id="0ad4b-114">What will you deploy?</span></span>

<span data-ttu-id="0ad4b-115">이 템플릿을 사용하면 하나의 이벤트 허브가 있는 Event Hubs 네임스페이스를 배포하고 [Event Hubs 캡처](event-hubs-capture-overview.md)도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-115">With this template, you deploy an Event Hubs namespace with an event hub, and also enable [Event Hubs Capture](event-hubs-capture-overview.md).</span></span>

<span data-ttu-id="0ad4b-116">[이벤트 허브](event-hubs-what-is-event-hubs.md) 는 짧은 대기 시간 및 높은 안정성으로 이벤트 및 원격 분석을 엄청난 규모의 Azure에 제공하는 데 사용되는 이벤트 ingestor 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-116">[Event Hubs](event-hubs-what-is-event-hubs.md) is an event processing service used to provide event and telemetry ingress to Azure at massive scale, with low latency and high reliability.</span></span> <span data-ttu-id="0ad4b-117">Event Hubs 캡처를 사용하면 Event Hubs의 스트리밍 데이터를 지정한 시간이나 선택한 크기 간격 내에서 Azure Blob Storage 또는 Azure Data Lake Store에 자동으로 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-117">Event Hubs Capture enables you to automatically deliver the streaming data in Event Hubs to Azure Blob storage or Azure Data Lake Store, within a specified time or size interval of your choosing.</span></span>

<span data-ttu-id="0ad4b-118">Azure Storage로 Event Hubs 캡처를 사용하도록 설정하려면 다음 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-118">Click the following button to enable Event Hubs Capture into Azure Storage:</span></span>

<span data-ttu-id="0ad4b-119">[![Azure에 배포](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="0ad4b-119">[![Deploy to Azure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)</span></span>

<span data-ttu-id="0ad4b-120">Azure Data Lake Store로 Event Hubs 캡처를 사용하도록 설정하려면 다음 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-120">Click the following button to enable Event Hubs Capture into Azure Data Lake Store:</span></span>

<span data-ttu-id="0ad4b-121">[![Azure에 배포](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="0ad4b-121">[![Deploy to Azure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="0ad4b-122">매개 변수</span><span class="sxs-lookup"><span data-stu-id="0ad4b-122">Parameters</span></span>

<span data-ttu-id="0ad4b-123">Azure 리소스 관리자와 함께 템플릿을 배포할 때 지정하고자 하는 값으로 매개 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-123">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="0ad4b-124">템플릿은 모든 매개 변수 값이 포함된 `Parameters` 라는 섹션을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-124">The template includes a section called `Parameters` that contains all the parameter values.</span></span> <span data-ttu-id="0ad4b-125">배포하는 프로젝트에 따라 또는 환경에 따라 달라지는 이러한 값에 대한 매개 변수를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-125">You should define a parameter for those values that vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="0ad4b-126">항상 동일하게 유지되는 값으로 매개 변수를 정의하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-126">Do not define parameters for values that always stay the same.</span></span> <span data-ttu-id="0ad4b-127">각 매개 변수 값은 배포되는 리소스를 정의하는 템플릿에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-127">Each parameter value is used in the template to define the resources that are deployed.</span></span>

<span data-ttu-id="0ad4b-128">템플릿은 다음 매개 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-128">The template defines the following parameters.</span></span>

### <a name="eventhubnamespacename"></a><span data-ttu-id="0ad4b-129">eventHubNamespaceName</span><span class="sxs-lookup"><span data-stu-id="0ad4b-129">eventHubNamespaceName</span></span>

<span data-ttu-id="0ad4b-130">만들 [Event Hubs 네임스페이스](event-hubs-create.md)의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-130">The name of the [Event Hubs namespace](event-hubs-create.md) to create.</span></span>

```json
"eventHubNamespaceName":{  
     "type":"string",
     "metadata":{  
         "description":"Name of the EventHub namespace"
      }
}
```

### <a name="eventhubname"></a><span data-ttu-id="0ad4b-131">eventHubName</span><span class="sxs-lookup"><span data-stu-id="0ad4b-131">eventHubName</span></span>

<span data-ttu-id="0ad4b-132">[Event Hubs 네임스페이스](event-hubs-create.md)에서 만든 이벤트 허브의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-132">The name of the event hub created in the [Event Hubs namespace](event-hubs-create.md).</span></span>

```json
"eventHubName":{  
    "type":"string",
    "metadata":{  
        "description":"Name of the event hub"
    }
}
```

### <a name="messageretentionindays"></a><span data-ttu-id="0ad4b-133">messageRetentionInDays</span><span class="sxs-lookup"><span data-stu-id="0ad4b-133">messageRetentionInDays</span></span>

<span data-ttu-id="0ad4b-134">이벤트 허브에서 메시지를 보관할 기간(일수)입니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-134">The number of days to retain the messages in the event hub.</span></span> 

```json
"messageRetentionInDays":{
    "type":"int",
    "defaultValue": 1,
    "minValue":"1",
    "maxValue":"7",
    "metadata":{
       "description":"How long to retain the data in event hub"
     }
 }
```

### <a name="partitioncount"></a><span data-ttu-id="0ad4b-135">partitionCount</span><span class="sxs-lookup"><span data-stu-id="0ad4b-135">partitionCount</span></span>

<span data-ttu-id="0ad4b-136">이벤트 허브에서 만들 파티션 수입니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-136">The number of partitions to create in the event hub.</span></span>

```json
"partitionCount":{
    "type":"int",
    "defaultValue":2,
    "minValue":2,
    "maxValue":32,
    "metadata":{
        "description":"Number of partitions chosen"
    }
 }
```

### <a name="captureenabled"></a><span data-ttu-id="0ad4b-137">captureEnabled</span><span class="sxs-lookup"><span data-stu-id="0ad4b-137">captureEnabled</span></span>

<span data-ttu-id="0ad4b-138">이벤트 허브에서 캡처를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-138">Enable Capture on the event hub.</span></span>

```json
"captureEnabled":{
    "type":"string",
    "defaultValue":"true",
    "allowedValues": [
    "false",
    "true"],
    "metadata":{
        "description":"Enable or disable the Capture for your event hub"
    }
 }
```
### <a name="captureencodingformat"></a><span data-ttu-id="0ad4b-139">captureEncodingFormat</span><span class="sxs-lookup"><span data-stu-id="0ad4b-139">captureEncodingFormat</span></span>

<span data-ttu-id="0ad4b-140">이벤트 데이터를 직렬화하기 위해 지정하는 인코딩 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-140">The encoding format you specify to serialize the event data.</span></span>

```json
"captureEncodingFormat":{
    "type":"string",
    "defaultValue":"Avro",
    "allowedValues":[
    "Avro"],
    "metadata":{
        "description":"The encoding format in which Capture serializes the EventData"
    }
}
```

### <a name="capturetime"></a><span data-ttu-id="0ad4b-141">captureTime</span><span class="sxs-lookup"><span data-stu-id="0ad4b-141">captureTime</span></span>

<span data-ttu-id="0ad4b-142">Event Hubs 캡처를 통해 데이터를 캡처하기 시작하는 시간 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-142">The time interval in which Event Hubs Capture starts capturing the data.</span></span>

```json
"captureTime":{
    "type":"int",
    "defaultValue":300,
    "minValue":60,
    "maxValue":900,
    "metadata":{
         "description":"the time window in seconds for the capture"
    }
}
```

### <a name="capturesize"></a><span data-ttu-id="0ad4b-143">captureSize</span><span class="sxs-lookup"><span data-stu-id="0ad4b-143">captureSize</span></span>
<span data-ttu-id="0ad4b-144">캡처를 통해 데이터를 캡처하기 시작하는 크기 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-144">The size interval at which Capture starts capturing the data.</span></span>

```json
"captureSize":{
    "type":"int",
    "defaultValue":314572800,
    "minValue":10485760,
    "maxValue":524288000,
    "metadata":{
        "description":"The size window in bytes for capture"
    }
}
```

###<a name="capturenameformat"></a><span data-ttu-id="0ad4b-145">captureNameFormat</span><span class="sxs-lookup"><span data-stu-id="0ad4b-145">captureNameFormat</span></span>

<span data-ttu-id="0ad4b-146">Avro 파일을 쓰기 위해 Event Hubs 캡처에 의해 사용되는 이름 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-146">The name format used by Event Hubs Capture to write the Avro files.</span></span> <span data-ttu-id="0ad4b-147">캡처 이름 형식은 `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}` 및 `{Second}` 필드를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-147">Note that a Capture name format must contain `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}`, and `{Second}` fields.</span></span> <span data-ttu-id="0ad4b-148">구분 기호 유무에 관계 없이 정렬될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-148">These can be arranged in any order, with or without delimiters.</span></span>
 
```json
"captureNameFormat": {
      "type": "string",
      "defaultValue": "{Namespace}/{EventHub}/{PartitionId}/{Year}/{Month}/{Day}/{Hour}/{Minute}/{Second}",
      "metadata": {
        "description": "A Capture Name Format must contain {Namespace}, {EventHub}, {PartitionId}, {Year}, {Month}, {Day}, {Hour}, {Minute} and {Second} fields. These can be arranged in any order with or without delimeters. E.g.  Prod_{EventHub}/{Namespace}\\{PartitionId}_{Year}_{Month}/{Day}/{Hour}/{Minute}/{Second}"
      }
    }
  }
```

### <a name="apiversion"></a><span data-ttu-id="0ad4b-149">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0ad4b-149">apiVersion</span></span>

<span data-ttu-id="0ad4b-150">템플릿의 API 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-150">The API version of the template.</span></span>

```json
 "apiVersion":{  
    "type":"string",
    "defaultValue":"2015-08-01",
    "metadata":{  
        "description":"ApiVersion used by the template"
    }
 }
```

<span data-ttu-id="0ad4b-151">Azure Storage를 대상으로 선택한 경우 다음 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-151">Use the following parameters if you choose Azure Storage as your destination.</span></span>

### <a name="destinationstorageaccountresourceid"></a><span data-ttu-id="0ad4b-152">destinationStorageAccountResourceId</span><span class="sxs-lookup"><span data-stu-id="0ad4b-152">destinationStorageAccountResourceId</span></span>

<span data-ttu-id="0ad4b-153">원하는 Storage 계정에 캡처하도록 설정하기 위해 캡처에 Azure Storage 계정 리소스 ID가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-153">Capture requires an Azure Storage account resource ID to enable capturing to your desired Storage account.</span></span>

```json
 "destinationStorageAccountResourceId":{
    "type":"string",
    "metadata":{
        "description":"Your existing Storage account resource ID where you want the blobs be captured"
    }
 }
```

### <a name="blobcontainername"></a><span data-ttu-id="0ad4b-154">blobContainerName</span><span class="sxs-lookup"><span data-stu-id="0ad4b-154">blobContainerName</span></span>

<span data-ttu-id="0ad4b-155">이벤트 데이터를 캡처할 BLOB 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-155">The blob container in which to capture your event data.</span></span>

```json
 "blobContainerName":{
    "type":"string",
    "metadata":{
        "description":"Your existing storage container in which you want the blobs captured"
    }
}
```

<span data-ttu-id="0ad4b-156">Azure Data Lake Store를 대상으로 선택한 경우 다음 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-156">Use the following parameters if you choose Azure Data Lake Store as your destination.</span></span> <span data-ttu-id="0ad4b-157">이벤트를 캡처하려는 Data Lake Store 경로에서 사용 권한을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-157">You must set permissions on your Data Lake Store path, in which you want to Capture the event.</span></span> <span data-ttu-id="0ad4b-158">사용 권한을 설정하려면 [이 문서](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-158">To set permissions, see [this article](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account).</span></span>

###<a name="subscriptionid"></a><span data-ttu-id="0ad4b-159">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="0ad4b-159">subscriptionId</span></span>

<span data-ttu-id="0ad4b-160">Event Hubs 네임스페이스와 Azure Data Lake Store에 대한 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-160">Subscription ID for the Event Hubs namespace and Azure Data Lake Store.</span></span> <span data-ttu-id="0ad4b-161">이러한 두 리소스가 동일한 구독 ID에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-161">Both these resources must be under the same subscription ID.</span></span>

```json
"subscriptionId": {
    "type": "string",
    "metadata": {
        "description": "Subscription Id of both Azure Data Lake Store and Event Hub namespace"
     }
 }
```

###<a name="datalakeaccountname"></a><span data-ttu-id="0ad4b-162">dataLakeAccountName</span><span class="sxs-lookup"><span data-stu-id="0ad4b-162">dataLakeAccountName</span></span>

<span data-ttu-id="0ad4b-163">캡처된 이벤트에 대한 Azure Data Lake Store 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-163">The Azure Data Lake Store name for the captured events.</span></span>

```json
"dataLakeAccountName": {
    "type": "string",
    "metadata": {
        "description": "Azure Data Lake Store name"
    }
}
```

###<a name="datalakefolderpath"></a><span data-ttu-id="0ad4b-164">dataLakeFolderPath</span><span class="sxs-lookup"><span data-stu-id="0ad4b-164">dataLakeFolderPath</span></span>

<span data-ttu-id="0ad4b-165">캡처된 이벤트에 대한 대상 폴더 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-165">The destination folder path for the captured events.</span></span>

```json
"dataLakeFolderPath": {
    "type": "string",
    "metadata": {
        "description": "Destination archive folder path"
    }
}
```

## <a name="resources-to-deploy-for-azure-storage-as-destination-to-captured-events"></a><span data-ttu-id="0ad4b-166">캡처된 이벤트에 대한 대상으로 Azure Storage에 배포할 리소스</span><span class="sxs-lookup"><span data-stu-id="0ad4b-166">Resources to deploy for Azure Storage as destination to captured events</span></span>

<span data-ttu-id="0ad4b-167">하나의 이벤트 허브가 있는 **EventHubs** 형식의 네임스페이스를 만들고 Azure Blob Storage에 캡처를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-167">Creates a namespace of type **EventHubs**, with one event hub, and also enables Capture to Azure Blob Storage.</span></span>

```json
"resources":[  
      {  
         "apiVersion":"[variables('ehVersion')]",
         "name":"[parameters('eventHubNamespaceName')]",
         "type":"Microsoft.EventHub/Namespaces",
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
                  "[concat('Microsoft.EventHub/namespaces/', parameters('eventHubNamespaceName'))]"
               ],
               "properties":{  
                  "path":"[parameters('eventHubName')]",
                  "MessageRetentionInDays":"[parameters('messageRetentionInDays')]",
                  "PartitionCount":"[parameters('partitionCount')]",
                  "CaptureDescription":{
                        "enabled":"[parameters('captureEnabled')]",
                        "encoding":"[parameters('captureEncodingFormat')]",
                        "intervalInSeconds":"[parameters('captureTime')]",
                        "sizeLimitInBytes":"[parameters('captureSize')]",
                        "destination":{
                            "name":"EventHubCapture.AzureBlockBlob",
                            "properties":{
                                "StorageAccountResourceId":"[parameters('destinationStorageAccountResourceId')]",
                                "BlobContainer":"[parameters('blobContainerName')]"
                            }
                        } 
                  }

               }

            }
         ]
      }
   ]
```

## <a name="resources-to-deploy-for-azure-data-lake-store-as-destination"></a><span data-ttu-id="0ad4b-168">Azure Data Lake Store에 대상으로 배포할 리소스</span><span class="sxs-lookup"><span data-stu-id="0ad4b-168">Resources to deploy for Azure Data Lake Store as destination</span></span>

<span data-ttu-id="0ad4b-169">하나의 이벤트 허브가 있는 **EventHubs** 형식의 네임스페이스를 만들고 Azure Data Lake Store에 캡처를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-169">Creates a namespace of type **EventHubs**, with one event hub, and also enables Capture to Azure Data Lake Store.</span></span>

```json
 "resources": [
        {
            "apiVersion": "2015-08-01",
            "name": "[parameters('namespaceName')]",
            "type": "Microsoft.EventHub/Namespaces",
            "location": "[variables('location')]",
            "sku": {
                "name": "Standard",
                "tier": "Standard"
            },
            "resources": [
                {
                    "apiVersion": "2015-08-01",
                    "name": "[parameters('eventHubName')]",
                    "type": "EventHubs",
                    "dependsOn": [
                        "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
                    ],
                    "properties": {
                        "path": "[parameters('eventHubName')]",
                        "ArchiveDescription": {
                            "enabled": "true",
                            "encoding": "[parameters('archiveEncodingFormat')]",
                            "intervalInSeconds": "[parameters('archiveTime')]",
                            "sizeLimitInBytes": "[parameters('archiveSize')]",
                            "destination": {
                                "name": "EventHubArchive.AzureDataLake",
                                "properties": {
                                    "DataLakeSubscriptionId": "[parameters('subscriptionId')]",
                                    "DataLakeAccountName": "[parameters('dataLakeAccountName')]",
                                    "DataLakeFolderPath": "[parameters('dataLakeFolderPath')]",
                                    "ArchiveNameFormat": "[parameters('archiveNameFormat')]"
                                }
                            }
                        }
                    }
                }
            ]
        }
    ]
```

## <a name="commands-to-run-deployment"></a><span data-ttu-id="0ad4b-170">배포 실행 명령</span><span class="sxs-lookup"><span data-stu-id="0ad4b-170">Commands to run deployment</span></span>

[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="0ad4b-171">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0ad4b-171">PowerShell</span></span>

<span data-ttu-id="0ad4b-172">템플릿을 배포하여 Azure Storage로 Event Hubs 캡처를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-172">Deploy your template to enable Event Hubs Capture into Azure Storage:</span></span>
 
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json
```

<span data-ttu-id="0ad4b-173">템플릿을 배포하여 Azure Data Lake Store로 Event Hubs 캡처를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-173">Deploy your template to enable Event Hubs Capture into Azure Data Lake Store:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json
```

## <a name="azure-cli"></a><span data-ttu-id="0ad4b-174">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0ad4b-174">Azure CLI</span></span>

<span data-ttu-id="0ad4b-175">Azure Blob Storage를 대상으로 선택:</span><span class="sxs-lookup"><span data-stu-id="0ad4b-175">Choosing Azure Blob Storage as destination:</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json][]
```

<span data-ttu-id="0ad4b-176">Azure Data Lake Store를 대상으로 선택:</span><span class="sxs-lookup"><span data-stu-id="0ad4b-176">Choosing Azure Data Lake Store as destination:</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json][]
```

## <a name="next-steps"></a><span data-ttu-id="0ad4b-177">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0ad4b-177">Next steps</span></span>

<span data-ttu-id="0ad4b-178">[Azure Portal](https://portal.azure.com)을 통해 Event Hubs 캡처를 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-178">You can also configure Event Hubs Capture via the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="0ad4b-179">자세한 내용은 [Azure Portal을 사용하여 Event Hubs 캡처를 사용하도록 설정](event-hubs-capture-enable-through-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-179">For more information, see [Enable Event Hubs Capture using the Azure portal](event-hubs-capture-enable-through-portal.md).</span></span>

<span data-ttu-id="0ad4b-180">Event Hubs에 대한 자세한 내용은 다음 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0ad4b-180">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="0ad4b-181">이벤트 허브 개요</span><span class="sxs-lookup"><span data-stu-id="0ad4b-181">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="0ad4b-182">이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="0ad4b-182">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="0ad4b-183">Event Hubs FAQ</span><span class="sxs-lookup"><span data-stu-id="0ad4b-183">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Azure Resources naming conventions]: https://azure.microsoft.com/documentation/articles/guidance-naming-conventions/
[Event hub and enable Capture to Storage template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture
[Event hub and enable Capture to Azure Data Lake Store template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture-for-adls