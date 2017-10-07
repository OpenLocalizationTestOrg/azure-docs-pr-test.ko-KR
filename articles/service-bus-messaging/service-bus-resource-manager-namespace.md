---
title: "Azure 리소스 관리자 템플릿을 사용 하 여 서비스 버스 네임 스페이스 aaaCreate | Microsoft Docs"
description: "Azure 리소스 관리자 템플릿 toocreate 서비스 버스 네임 스페이스를 사용 하 여"
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
ms.openlocfilehash: fddf370affe761a734991ae9b60c1e5825e54ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-using-an-azure-resource-manager-template"></a>Azure Resource Manager 템플릿을 사용하여 서비스 버스 네임스페이스 만들기

이 문서에서는 Azure 리소스 관리자 템플릿을 toouse를 만드는 방법을 형식의 서비스 버스 네임 스페이스 설명 **메시징** Standard/Basic SKU와 합니다. 또한 hello 문서 hello 배포의 hello 실행에 대해 지정 된 hello 매개 변수를 정의 합니다. 배포를 위한이 서식 파일을 사용 하거나 toomeet 사용자 지정할 수 있습니다 프로그램 요구 사항입니다.

템플릿을 만들기에 대한 자세한 내용은 [Azure Resource Manager 템플릿 작성][Authoring Azure Resource Manager templates]을 참조하세요.

Hello 전체 서식 파일에 대 한 참조 hello [서비스 버스 네임 스페이스 템플릿] [ Service Bus namespace template] GitHub에서 합니다.

> [!NOTE]
> Azure 리소스 관리자 템플릿을 다음 hello 다운로드 및 배포에 사용할 수 있는 합니다. 
> 
> * [큐가 있는 서비스 버스 네임스페이스 만들기](service-bus-resource-manager-namespace-queue.md)
> * [토픽 및 구독이 있는 서비스 버스 네임스페이스 만들기](service-bus-resource-manager-namespace-topic.md)
> * [큐 및 권한 부여 규칙이 있는 서비스 버스 네임스페이스 만들기](service-bus-resource-manager-namespace-auth-rule.md)
> * [토픽, 구독 및 규칙이 있는 Service Bus 네임스페이스 만들기](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> hello 최신 템플릿용으로 toocheck 방문 hello [Azure 빠른 시작 템플릿] [ Azure Quickstart Templates] 갤러리 및 서비스 버스에 대 한 검색 합니다.
> 
> 

## <a name="what-will-you-deploy"></a>배포할 항목
이 템플릿을 사용하여 [기본, 표준 또는 프리미엄](https://azure.microsoft.com/pricing/details/service-bus/) SKU가 있는 Service Bus 네임스페이스를 배포합니다.

toorun 배포를 자동으로 hello, hello 다음 단추를 클릭 합니다.

[![TooAzure 배포](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)

## <a name="parameters"></a>매개 변수
Azure 리소스 관리자와 정의한 매개 변수 값에 대 한 원하는 toospecify hello 서식 파일을 배포할 때. hello 템플릿에 섹션이 포함 되어 `Parameters` hello 매개 변수 값이 모두 들어 있는입니다. 에 배포 하는 hello 환경에 따라 또는 배포 하는 hello 프로젝트에 따라 달라 집니다는 해당 값에 대 한 매개 변수를 정의 해야 합니다. 항상 유지 되는 값 동일 hello에 대 한 매개 변수를 정의 하지 않습니다. 각 매개 변수 값은 배포 된 hello 템플릿 toodefine hello 리소스에 사용 됩니다.

이 템플릿은 매개 변수 뒤 hello를 정의 합니다.

### <a name="servicebusnamespacename"></a>serviceBusNamespaceName
서비스 버스 네임 스페이스 toocreate hello의 hello 이름입니다.

```json
"serviceBusNamespaceName": {
"type": "string",
"metadata": { 
    "description": "Name of hello Service Bus namespace" 
    }
}
```

### <a name="servicebussku"></a>serviceBusSKU
서비스 버스 hello의 hello 이름 [SKU](https://azure.microsoft.com/pricing/details/service-bus/) toocreate 합니다.

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
        "description": "hello messaging tier for service Bus namespace" 
    } 

```

hello 템플릿이 매개이 변수 (예: Basic, Standard 또는 Premium)에 허용 되는 hello 값을 정의 하 고 값을 지정 하는 경우 기본값 (표준)를 할당 합니다.

Service Bus 가격에 대한 자세한 내용은 [Service Bus 가격 및 대금 청구][Service Bus pricing and billing]를 참조하세요.

### <a name="servicebusapiversion"></a>serviceBusApiVersion
hello hello 서식 파일의 서비스 버스 API 버전입니다.

```json
"serviceBusApiVersion": { 
       "type": "string", 
       "defaultValue": "2015-08-01", 
       "metadata": { 
           "description": "Service Bus ApiVersion used by hello template" 
       } 
```

## <a name="resources-toodeploy"></a>리소스 toodeploy
### <a name="service-bus-namespace"></a>서비스 버스 네임스페이스
**메시징**형식의 표준 서비스 버스 네임스페이스를 만듭니다.

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

## <a name="commands-toorun-deployment"></a>명령 toorun 배포
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName <resource-group-name> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

### <a name="azure-cli"></a>Azure CLI
```azurecli
azure config mode arm

azure group deployment create <my-resource-group> <my-deployment-name> --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

## <a name="next-steps"></a>다음 단계
이제 작성 되었으며 Azure 리소스 관리자를 사용 하 여 리소스를 배포, 자세히 배울 방법 toomanage 이러한 문서를 참조 하 여 이러한 리소스:

* [PowerShell을 사용하여 서비스 버스 관리](service-bus-manage-with-ps.md)
* [서비스 버스 탐색기 hello 사용 하 여 서비스 버스 리소스 관리](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace template]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-servicebus-create-namespace/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Service Bus pricing and billing]: service-bus-pricing-billing.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
