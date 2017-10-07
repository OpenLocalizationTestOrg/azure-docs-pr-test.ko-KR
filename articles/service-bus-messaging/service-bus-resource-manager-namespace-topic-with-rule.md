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
# <a name="create-a-service-bus-namespace-with-topic-subscription-and-rule-using-an-azure-resource-manager-template"></a>Azure Resource Manager 템플릿을 사용하여 토픽, 구독 및 규칙이 있는 Service Bus 네임스페이스 만들기

이 문서에서는 어떻게 toouse Azure 리소스 관리자 템플릿을으로 만드는 서비스 버스 네임 스페이스 항목, 구독 및 규칙 (필터) 합니다. 배웁니다 어떻게 toodefine 리소스 배포 되 고 toodefine 매개 변수를 hello 배포를 실행 하는 경우 지정 된 합니다. 배포를 위한이 서식 파일을 사용 하거나 toomeet 사용자 지정할 수 있습니다 프로그램 요구 사항

템플릿 만들기에 대한 자세한 내용은 [Azure Resource Manager 템플릿 작성하기][Authoring Azure Resource Manager templates]를 참조하세요.

Azure 리소스 명명 규칙의 사례 및 패턴에 대한 자세한 내용은 [Azure 리소스에 대한 권장되는 명명 규칙][Recommended naming conventions for Azure resources]을 참조하세요.

Hello 전체 서식 파일에 대 한 참조 hello [항목, 구독 및 규칙으로 서비스 버스 네임 스페이스] [ Service Bus namespace with topic, subscription, and rule] 서식 파일입니다.

> [!NOTE]
> Azure 리소스 관리자 템플릿을 다음 hello 다운로드 및 배포에 사용할 수 있는 합니다.
> 
> * [큐 및 권한 부여 규칙이 있는 서비스 버스 네임스페이스 만들기](service-bus-resource-manager-namespace-auth-rule.md)
> * [큐가 있는 서비스 버스 네임스페이스 만들기](service-bus-resource-manager-namespace-queue.md)
> * [서비스 버스 네임스페이스 만들기](service-bus-resource-manager-namespace.md)
> * [토픽 및 구독이 있는 서비스 버스 네임스페이스 만들기](service-bus-resource-manager-namespace-topic.md)
> 
> hello 최신 템플릿용으로 toocheck 방문 hello [Azure 빠른 시작 템플릿] [ Azure Quickstart Templates] 갤러리 및 서비스 버스에 대 한 검색 합니다.
> 
> 

## <a name="what-will-you-deploy"></a>배포할 항목

이 템플릿을 사용하여 토픽, 구독 및 규칙(필터)이 있는 Service Bus 네임스페이스를 배포합니다.

[Service Bus 토픽 및 구독](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions)은 *게시/구독* 패턴으로 일 대 다 형태의 통신을 제공합니다. 배포 응용 프로그램의 구성 요소와 직접 통신 하지 않는 항목 및 구독을 사용할 때 대신 교환 하는 중간자 역할을 하는 항목을 통해 메시지입니다. 구독 tooa 항목 toohello 항목 보낸 메시지의 복사본을 받는 가상 큐와 유사 합니다. 구독에 대 한 필터 하면 toospecify 보낸 메시지 tooa 항목 특정 항목 구독 내에 표시 됩니다.

## <a name="what-are-rules-filters"></a>규칙(필터)란?

대부분의 시나리오에서 특정 특성을 가진 메시지를 다른 방법으로 처리해야 합니다. tooenable이를 특정 속성을 가진 및 다음 toothose 속성 수정 작업을 수행 하는 구독 toofind 메시지를 구성할 수 있습니다. 서비스 버스 구독 toohello 항목 보낸 모든 메시지를 볼 있지만만 해당 메시지 toohello 가상 구독 큐의 하위 집합을 복사할 수 있습니다. 구독 필터를 사용하여 수행합니다. 규칙 (필터)에 대해 자세히 toolearn 참조 [규칙 및 동작](service-bus-queues-topics-subscriptions.md#rules-and-actions)합니다.

toorun 배포를 자동으로 hello, hello 다음 단추를 클릭 합니다.

[![TooAzure 배포](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)

## <a name="parameters"></a>매개 변수

Azure 리소스 관리자와 매개 변수를 정의 해야 값에 대 한 원하는 toospecify hello 서식 파일을 배포할 때. hello 템플릿에 섹션이 포함 되어 `Parameters` 모든 hello 매개 변수 값이 들어 있는입니다. 에 배포 하는 hello 환경에 따라 또는 배포 하는 hello 프로젝트에 따라 달라 지는 해당 값에 대 한 매개 변수를 정의 해야 합니다. 동일한 값을 항상 유지 hello에 대 한 매개 변수를 정의 하지 않습니다. 각 매개 변수 값은 배포 된 hello 템플릿 toodefine hello 리소스에 사용 됩니다.

hello 템플릿 매개 변수 뒤 hello를 정의 합니다.

### <a name="servicebusnamespacename"></a>serviceBusNamespaceName
서비스 버스 네임 스페이스 toocreate hello의 hello 이름입니다.

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a>serviceBusTopicName
hello 서비스 버스 네임 스페이스에서 만든 hello 항목의 hello 이름입니다.

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a>serviceBusSubscriptionName
hello 서비스 버스 네임 스페이스에서 만든 구독에 hello의 hello 이름입니다.

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```
### <a name="servicebusrulename"></a>serviceBusRuleName
hello 서비스 버스 네임 스페이스에서 만든 hello rule(filter)의 hello 이름입니다.

```json
   "serviceBusRuleName": {
   "type": "string",
  }
```
### <a name="servicebusapiversion"></a>serviceBusApiVersion
hello hello 서식 파일의 서비스 버스 API 버전입니다.

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-toodeploy"></a>리소스 toodeploy
토픽, 구독 및 규칙이 있는 **메시징** 형식의 표준 Service Bus 네임스페이스를 만듭니다.

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

## <a name="commands-toorun-deployment"></a>명령 toorun 배포
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a>PowerShell
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="azure-cli"></a>Azure CLI
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="next-steps"></a>다음 단계
이제 작성 되었으며 Azure 리소스 관리자를 사용 하 여 리소스를 배포, 자세히 배울 방법 toomanage 이러한 문서를 확인 하 여 이러한 리소스:

* [Azure Service Bus 관리](service-bus-management-libraries.md)
* [PowerShell을 사용하여 서비스 버스 관리](service-bus-manage-with-ps.md)
* [서비스 버스 탐색기 hello 사용 하 여 서비스 버스 리소스 관리](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Recommended naming conventions for Azure resources]: ../guidance/guidance-naming-conventions.md
[Service Bus namespace with topic, subscription, and rule]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-subscription-rule/
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md

