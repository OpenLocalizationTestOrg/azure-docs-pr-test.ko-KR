---
title: "서식 파일을 사용 하 여 Azure 이벤트 허브 네임 스페이스를 사용 하도록 설정한 Capture aaaCreate | Microsoft Docs"
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
ms.openlocfilehash: a43b4e8d690ae825047e8a9d609bfda89cf2a06f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-with-an-event-hub-and-enable-capture-using-an-azure-resource-manager-template"></a>Azure Resource Manager 템플릿을 사용하여 하나의 이벤트 허브가 있는 Event Hubs 네임스페이스를 만들고 캡처를 사용하도록 설정

이 문서에서는 어떻게 toouse Azure 리소스 관리자 템플릿을 만들어지는 이벤트 허브 네임 스페이스를 하나의 이벤트 허브 인스턴스 및 사용 hello [캡처 기능은](event-hubs-capture-overview.md) hello 이벤트 허브에 있습니다. hello 문서에서는 설명 방법을 toodefine 및 hello 배포를 실행할 때 toodefine 매개 변수를을 지정 하는 방법에 리소스를 배포 합니다. 배포를 위한이 서식 파일을 사용 하거나 toomeet 사용자 지정할 수 있습니다 프로그램 요구 사항입니다.

또한이 문서에서는 hello에 toospecify Azure 저장소 Blob 나 Azure Data Lake 저장소에 캡처할 이벤트를 기반으로 하는 방법을 보여 줍니다. 선택한 대상입니다.

템플릿 만들기에 대한 자세한 내용은 [Azure Resource Manager 템플릿 작성하기][Authoring Azure Resource Manager templates]를 참조하세요.

Azure 리소스 명명 규칙의 패턴 및 사례에 대한 자세한 내용은 [Azure 리소스 명명 규칙][Azure Resources naming conventions]을 참조하세요.

Hello 전체 템플릿 hello 다음 GitHub 링크를 클릭 합니다.

- [이벤트 허브를 사용 하도록 설정한 캡처 tooStorage 서식 파일][Event Hub and enable Capture tooStorage template] 
- [이벤트 허브를 사용 하도록 설정한 캡처 tooAzure 데이터 레이크 저장소 템플릿][Event Hub and enable Capture tooAzure Data Lake Store template]

> [!NOTE]
> hello 최신 템플릿용으로 toocheck 방문 hello [Azure 빠른 시작 템플릿] [ Azure Quickstart Templates] 갤러리 및 이벤트 허브에 대 한 검색 합니다.
> 
> 

## <a name="what-will-you-deploy"></a>배포할 항목

이 템플릿을 사용하면 하나의 이벤트 허브가 있는 Event Hubs 네임스페이스를 배포하고 [Event Hubs 캡처](event-hubs-capture-overview.md)도 사용할 수 있습니다.

[이벤트 허브](event-hubs-what-is-event-hubs.md) 낮은 대기 시간과 높은 안정성에 대량으로 사용 되는 서비스 tooprovide 이벤트 및 원격 분석 ingress tooAzure 처리 하는 이벤트입니다. 이벤트 허브 캡처를 사용 하면 tooautomatically hello 특정된 시간이 나 선택한 크기 간격 내에서 이벤트 허브 tooAzure Blob 저장소에 데이터 또는 Azure 데이터 레이크 저장소를 스트리밍 배달 합니다.

이벤트 허브 캡처 단추 tooenable Azure 저장소로 다음 hello를 클릭 합니다.

[![TooAzure 배포](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)

Hello Azure 데이터 레이크 저장소에 이벤트 허브 캡처 단추 tooenable 다음를 클릭 합니다.

[![TooAzure 배포](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)

## <a name="parameters"></a>매개 변수

Azure 리소스 관리자와 정의한 매개 변수 값에 대 한 원하는 toospecify hello 서식 파일을 배포할 때. hello 템플릿에 섹션이 포함 되어 `Parameters` 모든 hello 매개 변수 값이 들어 있는입니다. 에 배포 하는 hello 환경에 따라 또는 배포 하는 hello 프로젝트에 따라 달라 지는 해당 값에 대 한 매개 변수를 정의 해야 합니다. 동일한 값을 항상 유지 hello에 대 한 매개 변수를 정의 하지 않습니다. 각 매개 변수 값은 배포 된 hello 템플릿 toodefine hello 리소스에 사용 됩니다.

hello 템플릿은 매개 변수 뒤 hello를 정의 합니다.

### <a name="eventhubnamespacename"></a>eventHubNamespaceName

hello의 hello 이름 [이벤트 허브 네임 스페이스](event-hubs-create.md) toocreate 합니다.

```json
"eventHubNamespaceName":{  
     "type":"string",
     "metadata":{  
         "description":"Name of hello EventHub namespace"
      }
}
```

### <a name="eventhubname"></a>eventHubName

hello에서 만든 hello 이벤트 허브의 hello 이름 [이벤트 허브 네임 스페이스](event-hubs-create.md)합니다.

```json
"eventHubName":{  
    "type":"string",
    "metadata":{  
        "description":"Name of hello event hub"
    }
}
```

### <a name="messageretentionindays"></a>messageRetentionInDays

hello hello 이벤트 허브에서 일 tooretain hello 메시지 수입니다. 

```json
"messageRetentionInDays":{
    "type":"int",
    "defaultValue": 1,
    "minValue":"1",
    "maxValue":"7",
    "metadata":{
       "description":"How long tooretain hello data in event hub"
     }
 }
```

### <a name="partitioncount"></a>partitionCount

hello 이벤트 허브에 대 한 파티션 toocreate hello 수입니다.

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

### <a name="captureenabled"></a>captureEnabled

Hello 이벤트 허브에서 캡처를 사용 하도록 설정 합니다.

```json
"captureEnabled":{
    "type":"string",
    "defaultValue":"true",
    "allowedValues": [
    "false",
    "true"],
    "metadata":{
        "description":"Enable or disable hello Capture for your event hub"
    }
 }
```
### <a name="captureencodingformat"></a>captureEncodingFormat

hello 인코딩 형식을 tooserialize hello 이벤트 데이터를 지정 합니다.

```json
"captureEncodingFormat":{
    "type":"string",
    "defaultValue":"Avro",
    "allowedValues":[
    "Avro"],
    "metadata":{
        "description":"hello encoding format in which Capture serializes hello EventData"
    }
}
```

### <a name="capturetime"></a>captureTime

이벤트 허브 캡처 시작 되 hello 데이터 캡처는 hello 시간 간격입니다.

```json
"captureTime":{
    "type":"int",
    "defaultValue":300,
    "minValue":60,
    "maxValue":900,
    "metadata":{
         "description":"hello time window in seconds for hello capture"
    }
}
```

### <a name="capturesize"></a>captureSize
캡처 시작 되는 hello 데이터 캡처는 hello 크기 간격입니다.

```json
"captureSize":{
    "type":"int",
    "defaultValue":314572800,
    "minValue":10485760,
    "maxValue":524288000,
    "metadata":{
        "description":"hello size window in bytes for capture"
    }
}
```

###<a name="capturenameformat"></a>captureNameFormat

이벤트 허브 캡처 toowrite hello Avro 파일 사용 되는 hello 이름 형식입니다. 캡처 이름 형식은 `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}` 및 `{Second}` 필드를 포함해야 합니다. 구분 기호 유무에 관계 없이 정렬될 수 있습니다.
 
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

### <a name="apiversion"></a>apiVersion

hello 템플릿의 hello API 버전입니다.

```json
 "apiVersion":{  
    "type":"string",
    "defaultValue":"2015-08-01",
    "metadata":{  
        "description":"ApiVersion used by hello template"
    }
 }
```

Hello 매개 변수를 대상으로 Azure 저장소를 선택 하면 다음을 사용 합니다.

### <a name="destinationstorageaccountresourceid"></a>destinationStorageAccountResourceId

캡처는 tooyour 캡처는 Azure 저장소 계정 리소스 ID tooenable 원하는 저장소 계정이 필요 합니다.

```json
 "destinationStorageAccountResourceId":{
    "type":"string",
    "metadata":{
        "description":"Your existing Storage account resource ID where you want hello blobs be captured"
    }
 }
```

### <a name="blobcontainername"></a>blobContainerName

hello를 blob 컨테이너는 toocapture에 이벤트 데이터입니다.

```json
 "blobContainerName":{
    "type":"string",
    "metadata":{
        "description":"Your existing storage container in which you want hello blobs captured"
    }
}
```

Azure 데이터 레이크 저장소 대상으로 선택 하면 매개 변수 뒤 hello를 사용 합니다. 데이터 레이크 저장소 경로, tooCapture hello 이벤트 원하는에 권한을 설정 해야 합니다. tooset 사용 권한 참조 [이 여기서](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account)합니다.

###<a name="subscriptionid"></a>subscriptionId

Hello 이벤트 허브 네임 스페이스와 Azure 데이터 레이크 저장소에 대 한 구독 ID입니다. 이러한 두 리소스 hello 아래에 있어야 합니다. 같은 구독 id입니다.

```json
"subscriptionId": {
    "type": "string",
    "metadata": {
        "description": "Subscription Id of both Azure Data Lake Store and Event Hub namespace"
     }
 }
```

###<a name="datalakeaccountname"></a>dataLakeAccountName

hello Azure Data Lake 저장소 이름 hello에 대 한 이벤트를 캡처합니다.

```json
"dataLakeAccountName": {
    "type": "string",
    "metadata": {
        "description": "Azure Data Lake Store name"
    }
}
```

###<a name="datalakefolderpath"></a>dataLakeFolderPath

hello에 대 한 hello 대상 폴더 경로 이벤트를 캡처합니다.

```json
"dataLakeFolderPath": {
    "type": "string",
    "metadata": {
        "description": "Destination archive folder path"
    }
}
```

## <a name="resources-toodeploy-for-azure-storage-as-destination-toocaptured-events"></a>대상 toocaptured 이벤트로 Azure 저장소에 대 한 리소스 toodeploy

형식의 네임 스페이스를 만듭니다 **EventHubs**, 하나의 이벤트 허브와도 사용 tooAzure Blob 저장소를 캡처합니다.

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

## <a name="resources-toodeploy-for-azure-data-lake-store-as-destination"></a>대상으로 Azure 데이터 레이크 저장소에 대 한 리소스 toodeploy

형식의 네임 스페이스를 만듭니다 **EventHubs**, 하나의 이벤트 허브와도 캡처 tooAzure Data Lake 저장소를 사용 하도록 설정 합니다.

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

## <a name="commands-toorun-deployment"></a>명령 toorun 배포

[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a>PowerShell

Azure 저장소로 이벤트 허브 캡처 템플릿 tooenable 프로그램을 배포 합니다.
 
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json
```

Azure 데이터 레이크 저장소에 이벤트 허브 캡처 템플릿 tooenable 프로그램을 배포 합니다.

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json
```

## <a name="azure-cli"></a>Azure CLI

Azure Blob Storage를 대상으로 선택:

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json][]
```

Azure Data Lake Store를 대상으로 선택:

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json][]
```

## <a name="next-steps"></a>다음 단계

Hello를 통해 이벤트 허브 캡처를 구성할 수도 있습니다 [Azure 포털](https://portal.azure.com)합니다. 자세한 내용은 참조 [활성화 이벤트 허브 캡처를 사용 하 여 Azure 포털을 hello](event-hubs-capture-enable-through-portal.md)합니다.

Hello 다음 링크를 방문 하 여 이벤트 허브에 대 한 자세히 알아볼 수 있습니다.

* [이벤트 허브 개요](event-hubs-what-is-event-hubs.md)
* [이벤트 허브 만들기](event-hubs-create.md)
* [Event Hubs FAQ](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Azure Resources naming conventions]: https://azure.microsoft.com/documentation/articles/guidance-naming-conventions/
[Event hub and enable Capture tooStorage template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture
[Event hub and enable Capture tooAzure Data Lake Store template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture-for-adls
