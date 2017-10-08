---
title: "Azure 리소스 관리자 템플릿을 사용 하 여 aaaCreate Azure 서비스 버스 리소스 | Microsoft Docs"
description: "서비스 버스 리소스의 Azure 리소스 관리자 템플릿 tooautomate hello 생성을 사용 하 여"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 24f6a207-0fa4-49cf-8a58-963f9e2fd655
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: e539902cae307b63ae7c332580e2064761331ec5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-service-bus-resources-using-azure-resource-manager-templates"></a>Azure Resource Manager 템플릿을 사용하여 서비스 버스 리소스 만들기

이 문서에서는 설명 방법을 toocreate 및 Azure 리소스 관리자 템플릿, PowerShell 및 hello 서비스 버스 리소스 공급자를 사용 하 여 서비스 버스 리소스를 배포 합니다.

Azure 리소스 관리자 템플릿을 사용 솔루션 및 toospecify 매개 변수 및 변수를 사용 하면 다양 한 환경에 대 한 tooinput 값에 대 한 리소스 toodeploy hello를 정의할 수 있습니다. JSON 및 배포에 대 한 tooconstruct 값을 사용할 수 있는 식의 hello 템플릿은 구성 됩니다. Azure 리소스 관리자 템플릿 및 hello 템플릿 형식에 대 한 내용은 작성에 대 한 자세한 내용은 참조 [구조 및 Azure 리소스 관리자 템플릿 구문](../azure-resource-manager/resource-group-authoring-templates.md)합니다.

> [!NOTE]
> 이 문서 표시의 예제를 어떻게 hello toouse Azure 리소스 관리자 toocreate 서비스 버스 네임 스페이스 및 메시징 엔터티 (큐). 다른 서식 파일 예제에 대 한 방문 hello [Azure 빠른 시작 템플릿 갤러리] [ Azure Quickstart Templates gallery] "서비스 버스."에 대 한 검색
>
>

## <a name="service-bus-resource-manager-templates"></a>Service Bus Resource Manager 템플릿

이러한 Service Bus Azure Resource Manager 템플릿은 다운로드하여 배포할 수 있습니다. Hello 다음 GitHub에 대 한 링크 toohello 템플릿으로 개에 대 한 세부 정보에 대 한 링크를 클릭 합니다.

* [서비스 버스 네임스페이스 만들기](service-bus-resource-manager-namespace.md)
* [큐가 있는 서비스 버스 네임스페이스 만들기](service-bus-resource-manager-namespace-queue.md)
* [토픽 및 구독이 있는 서비스 버스 네임스페이스 만들기](service-bus-resource-manager-namespace-topic.md)
* [큐 및 권한 부여 규칙이 있는 서비스 버스 네임스페이스 만들기](service-bus-resource-manager-namespace-auth-rule.md)
* [토픽, 구독 및 규칙이 있는 Service Bus 네임스페이스 만들기](service-bus-resource-manager-namespace-topic-with-rule.md)

## <a name="deploy-with-powershell"></a>PowerShell을 사용하여 배포 

hello 다음 절차에서는 Azure 리소스 관리자 템플릿을 toouse PowerShell toodeploy를 만드는 방법을 **표준** 서비스 버스 네임 스페이스 및 해당 네임 스페이스 내에서 큐를 계층입니다. Hello을 기반으로이 예제는 [큐와 서비스 버스 네임 스페이스 만들기](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) 템플릿. hello 대략적인 워크플로 다음과 같습니다.

1. PowerShell을 설치합니다.
2. Hello 템플릿 및 매개 변수 파일 (옵션)를 만듭니다.
3. PowerShell에서 tooyour Azure 계정에에서 로그인 합니다.
4. 새 리소스 그룹이 아직 없으면 만듭니다.
5. Hello 배포를 테스트 합니다.
6. 원하는 경우 hello 배포 모드를 설정 합니다.
7. Hello 템플릿을 배포 합니다.

Azure Resource Manager 배포 템플릿에 대한 모든 내용은 [Azure Resource Manager 템플릿으로 리소스 배포][Deploy resources with Azure Resource Manager templates]를 참조하세요.

### <a name="install-powershell"></a>PowerShell 설치 

Hello 지침에 따라 Azure PowerShell 설치 [Azure PowerShell 시작](/powershell/azure/get-started-azureps)합니다.

### <a name="create-a-template"></a>템플릿 만들기

복제 또는 복사 hello [201-servicebus--큐 만들기](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) GitHub에서 템플릿:

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "type": "string",
            "metadata": {
                "description": "Name of hello Service Bus namespace"
            }
        },
        "serviceBusQueueName": {
            "type": "string",
            "metadata": {
                "description": "Name of hello Queue"
            }
        },
        "serviceBusApiVersion": {
            "type": "string",
            "defaultValue": "2015-08-01",
            "metadata": {
                "description": "Service Bus ApiVersion used by hello template"
            }
        }
    },
    "variables": {
        "location": "[resourceGroup().location]",
        "sbVersion": "[parameters('serviceBusApiVersion')]",
        "defaultSASKeyName": "RootManageSharedAccessKey",
        "authRuleResourceId": "[resourceId('Microsoft.ServiceBus/namespaces/authorizationRules', parameters('serviceBusNamespaceName'), variables('defaultSASKeyName'))]"
    },
    "resources": [{
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
                "path": "[parameters('serviceBusQueueName')]"
            }
        }]
    }],
    "outputs": {
        "NamespaceConnectionString": {
            "type": "string",
            "value": "[listkeys(variables('authRuleResourceId'), variables('sbVersion')).primaryConnectionString]"
        },
        "SharedAccessPolicyPrimaryKey": {
            "type": "string",
            "value": "[listkeys(variables('authRuleResourceId'), variables('sbVersion')).primaryKey]"
        }
    }
}
```

### <a name="create-a-parameters-file-optional"></a>매개 변수 파일 만들기(옵션)

toouse 선택적 매개 변수 파일을 복사 hello [201-servicebus--큐 만들기](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) 파일입니다. Hello 값의 대체 `serviceBusNamespaceName` hello 서비스 버스 네임 스페이스의 hello 이름으로이 배포에 toocreate을 hello 값의 대체 `serviceBusQueueName` toocreate hello 큐의 hello 이름으로 원하는 합니다.

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "value": "<myNamespaceName>"
        },
        "serviceBusQueueName": {
            "value": "<myQueueName>"
        },
        "serviceBusApiVersion": {
            "value": "2015-08-01"
        }
    }
}
```

자세한 내용은 참조 hello [매개 변수](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) 항목입니다.

### <a name="log-in-tooazure-and-set-hello-azure-subscription"></a>TooAzure를 로그인 하 고 hello Azure 구독 설정

PowerShell 프롬프트에서 다음 명령을 hello를 실행 합니다.

```powershell
Login-AzureRmAccount
```

Tooyour Azure 계정에 증명된 toolog 됩니다. 로그온 한 후 다음 명령 tooview hello를 사용할 수 있는 구독 실행 합니다.

```powershell
Get-AzureRMSubscription
```

이 명령은 사용 가능한 Azure 구독 목록을 반환합니다. Hello 다음 명령을 실행 하 여 hello에 대 한 구독 현재 세션을 선택 합니다. 대체 `<YourSubscriptionId>` 원하는 toouse hello Azure 구독에 대 한 GUID hello로 합니다.

```powershell
Set-AzureRmContext -SubscriptionID <YourSubscriptionId>
```

### <a name="set-hello-resource-group"></a>Hello 리소스 그룹 설정

기존 리소스 그룹에서 hello로 새 리소스 그룹을 만들 수 없는 경우 * * 새로 AzureRmResourceGroup * * 명령입니다. Hello 이름 hello 리소스 그룹 및 toouse 원하는 위치를 제공 합니다. 예:

```powershell
New-AzureRmResourceGroup -Name MyDemoRG -Location "West US"
```

성공 하면 hello 새 리소스 그룹의 요약이 표시 됩니다.

```powershell
ResourceGroupName : MyDemoRG
Location          : westus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/<GUID>/resourceGroups/MyDemoRG
```

### <a name="test-hello-deployment"></a>Hello 배포 테스트

Hello를 실행 하 여 배포를 확인 `Test-AzureRmResourceGroupDeployment` cmdlet. Hello 배포를 테스트할 때는 하 듯 hello 배포를 실행할 때 매개 변수를 제공 합니다.

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="create-hello-deployment"></a>Hello 배포 만들기

toocreate hello 새 배포를 hello 실행 `New-AzureRmResourceGroupDeployment` cmdlet hello 필요한 매개 변수 대화 상자가 나타나면를 제공 합니다. hello 매개 변수, 리소스 그룹 및 hello 경로 또는 URL toohello 템플릿 파일의 hello 이름이 배포에 대 한 이름을 포함 합니다. 경우 hello **모드** 매개 변수를 지정 하지 않으면 기본값인 hello **증분** 사용 됩니다. 자세한 내용은 [증분 및 전체 배포](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments)를 참조하세요.

안녕하세요 명령 프롬프트에 다음 hello PowerShell 창에서 세 hello 매개 변수:

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

toospecify 매개 변수 파일 대신, 다음 명령을 hello를 사용 합니다.

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -TemplateParameterFile <path tooparameters file>\azuredeploy.parameters.json
```

Hello 배포 cmdlet을 실행 하는 경우에 인라인 매개 변수를 사용할 수 있습니다. hello 명령은 다음과 같습니다.

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -parameterName "parameterValue"
```

toorun는 [완료](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) 배포, 집합 hello **모드** 매개 변수가 너무**완료**:

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -Mode Complete -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="verify-hello-deployment"></a>Hello 배포 확인
Hello 리소스를 성공적으로 배포 하면 hello 배포의 요약 정보 hello PowerShell 창에 표시 됩니다.

```powershell
DeploymentName    : MyDemoDeployment
ResourceGroupName : MyDemoRG
ProvisioningState : Succeeded
Timestamp         : 4/19/2016 10:38:30 PM
Mode              : Incremental
TemplateLink      :
Parameters        :
                    Name             Type                       Value
                    ===============  =========================  ==========
                    serviceBusNamespaceName  String             <namespaceName>
                    serviceBusQueueName  String                 <queueName>
                    serviceBusApiVersion  String                2015-08-01

```

## <a name="next-steps"></a>다음 단계
이제는 Azure 리소스 관리자 템플릿을 배포 하기 위한 명령과 hello 기본 워크플로 살펴보았습니다. 더 자세한 정보에 대 한 링크를 따라 hello 방문.

* [Azure Resource Manager 개요][Azure Resource Manager overview]
* [Resource Manager 템플릿과 Azure PowerShell로 리소스 배포][Deploy resources with Azure Resource Manager templates]
* [Azure 리소스 관리자 템플릿 작성](../azure-resource-manager/resource-group-authoring-templates.md)

[Azure Resource Manager overview]: ../azure-resource-manager/resource-group-overview.md
[Deploy resources with Azure Resource Manager templates]: ../azure-resource-manager/resource-group-template-deploy.md
[Azure Quickstart Templates gallery]: https://azure.microsoft.com/documentation/templates/?term=service+bus
