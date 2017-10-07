---
title: "일반적인 Azure 배포 오류 aaaTroubleshoot | Microsoft Docs"
description: "설명 방법을 tooresolve 리소스 tooAzure Azure 리소스 관리자를 사용 하 여 배포할 때 일반적인 오류입니다."
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: "배포 오류를 azure 배포 tooazure 배포"
ms.assetid: c002a9be-4de5-4963-bd14-b54aa3d8fa59
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: tomfitz
ms.openlocfilehash: 8571e9941879eb5586e4258a785b6a09247da771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-common-azure-deployment-errors-with-azure-resource-manager"></a>Azure Resource Manager를 사용한 일반적인 Azure 배포 오류 해결
이 항목에서는 발생할 수 있는 일반적인 Azure 배포 오류 중 일부를 해결할 수 있는 방법에 대해 설명합니다.

hello 다음 오류 코드는이 항목에 설명 되어 있습니다.

* [AccountNameInvalid](#accountnameinvalid)
* [권한 부여 실패](#authorization-failed)
* [BadRequest](#badrequest)
* [DeploymentFailed](#deploymentfailed)
* [DisallowedOperation](#disallowedoperation)
* [InvalidContentLink](#invalidcontentlink)
* [InvalidTemplate](#invalidtemplate)
* [MissingSubscriptionRegistration](#noregisteredproviderfound)
* [NotFound](#notfound)
* [NoRegisteredProviderFound](#noregisteredproviderfound)
* [OperationNotAllowed](#quotaexceeded)
* [ParentResourceNotFound](#parentresourcenotfound)
* [QuotaExceeded](#quotaexceeded)
* [RequestDisallowedByPolicy](#requestdisallowedbypolicy)
* [ResourceNotFound](#notfound)
* [SkuNotAvailable](#skunotavailable)
* [StorageAccountAlreadyExists](#storagenamenotunique)
* [StorageAccountAlreadyTaken](#storagenamenotunique)

## <a name="deploymentfailed"></a>DeploymentFailed

Hello 오류 코드 toostart 문제 해결이 필요한 것만이 오류 코드는 일반적인 배포 오류를 나타냅니다. 실제로 hello 문제를 해결 하는 데 도움이 되는 hello 오류 코드는 일반적으로이 오류 보다 한 수준. 예를 들어 hello 다음 이미지에서는 hello **RequestDisallowedByPolicy** hello 배포 오류 아래에 있는 오류 코드입니다.

![오류 코드 표시](./media/resource-manager-common-deployment-errors/error-code.png)

## <a name="skunotavailable"></a>SkuNotAvailable

리소스 (일반적으로 가상 컴퓨터)을 배포할 때는 hello 다음과 같은 오류 코드 및 오류 메시지가 나타날 수 있습니다.

```
Code: SkuNotAvailable
Message: hello requested tier for resource '<resource>' is currently not available in location '<location>' 
for subscription '<subscriptionID>'. Please try another tier or deploy tooa different location.
```

Hello 리소스 (예: VM 크기) 선택한 SKU 선택한 hello 위치에 대해 사용할 수 없는 경우이 오류가 표시 됩니다. tooresolve이이 문제를 toodetermine Sku 사용할 수 있는 지역에 필요 합니다. PowerShell, hello 포털 또는 REST 작업 toofind에서는 사용 가능한 Sku입니다.

- PowerShell에서는 [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) 및 위치별 필터링을 사용합니다. Hello 최신 버전의 PowerShell이이 명령에 있어야 합니다.

  ```powershell
  Get-AzureRmComputeResourceSku | where {$_.Locations.Contains("southcentralus")}
  ```

  hello 결과 hello 위치에 대 한 Sku 목록 및 해당 SKU에 대 한 제한이 포함 됩니다.

  ```powershell
  ResourceType                Name      Locations Restriction                      Capability Value
  ------------                ----      --------- -----------                      ---------- -----
  availabilitySets         Classic southcentralus             MaximumPlatformFaultDomainCount     3
  availabilitySets         Aligned southcentralus             MaximumPlatformFaultDomainCount     3
  virtualMachines      Standard_A0 southcentralus
  virtualMachines      Standard_A1 southcentralus
  virtualMachines      Standard_A2 southcentralus
  ```

- toouse hello [포털](https://portal.azure.com)toohello 포털에 로그인 하 고 hello 인터페이스를 통해 리소스를 추가 합니다. Hello 참조 hello 값을 설정 하는 대로 해당 리소스에 대 한 사용 가능한 Sku입니다. Toocomplete hello 배포가 필요가 없습니다.

    ![사용 가능한 SKU](./media/resource-manager-common-deployment-errors/view-sku.png)

- 가상 컴퓨터에 대 한 toouse hello REST API 요청을 수행 하는 hello 보내기:

  ```HTTP 
  GET
  https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/skus?api-version=2016-03-30
  ```

  형식에 따라 hello에서 사용 가능한 Sku 및 지역 반환 합니다.

  ```json
  {
    "value": [
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A0",
        "tier": "Standard",
        "size": "A0",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A1",
        "tier": "Standard",
        "size": "A1",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      ...
    ]
  }    
  ```

전송할 수 없습니다 해당 지역 또는 비즈니스 요구를 충족 하는 대체 지역에 적합 한 SKU toofind 인 경우는 [SKU 요청](https://aka.ms/skurestriction) tooAzure 지원 합니다.

## <a name="disallowedoperation"></a>DisallowedOperation

```
Code: DisallowedOperation
Message: hello current subscription type is not permitted tooperform operations on any provider 
namespace. Please use a different subscription.
```

사용 중인 경우이 오류가 표시 되지 않는 구독 tooaccess Azure Active Directory 이외의 모든 Azure 서비스를 허용 합니다. Tooaccess hello 클래식 포털 필요 하지만 toodeploy 리소스 허용 되지 않는 경우 이러한 유형의 구독을 할 수 있습니다. tooresolve이이 문제를 toodeploy 리소스 권한 있는 구독을 사용 해야 합니다.  

tooview powershell을 사용할 수 있는 구독을 사용 합니다.

```powershell
Get-AzureRmSubscription
```

고 tooset hello 현재 구독을 사용 합니다.

```powershell
Set-AzureRmContext -SubscriptionName {subscription-name}
```

tooview Azure CLI 2.0을 사용할 수 있는 구독을 사용 합니다.

```azurecli
az account list
```

고 tooset hello 현재 구독을 사용 합니다.

```azurecli
az account set --subscription {subscription-name}
```

## <a name="invalidtemplate"></a>InvalidTemplate
이 오류로 인해 별도의 몇 가지 유형의 오류가 발생할 수 있습니다.

- 구문 오류

   Hello 실패 템플릿 유효성 검사를 나타내는 오류 메시지가 표시 되 면 서식 파일에서 구문 문제가 있을 수 있습니다.

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed
  ```

   이 오류 쉽게 toomake 않으므로 템플릿 식은 복잡 한 될 수 있습니다. 예를 들어 hello 저장소 계정에 대 한 다음 이름을 할당 대괄호로, 세 개의 함수, 세 가지 괄호, 작은따옴표, 집합이 하나 및 포함 한 속성:

  ```json
  "name": "[concat('storage', uniqueString(resourceGroup().id))]",
  ```

   일치 하는 구문 hello를 제공 하지 않는 경우 hello 템플릿 의도 보다 다른 값을 생성 합니다.

   이러한 종류의 오류를 받으면 hello 식 구문을 자세히 검토 합니다. [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) 또는 [Visual Studio Code](resource-manager-vs-code.md)와 같이 구문 오류에 대해 경고할 수 있는 JSON 편집기를 사용하는 것을 고려해 보세요.

- 잘못된 세그먼트 길이

   Hello 리소스 이름이 hello 형식이 잘못 되었습니다. 다른 잘못 된 템플릿 오류가 발생 합니다.

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed: 'hello template resource {resource-name}'
  for type {resource-type} has incorrect segment lengths.
  ```

   루트 수준 리소스 hello 리소스 종류에서 보다 hello 이름에 덜 하나의 세그먼트가 있어야 합니다. 각 세그먼트는 슬래시로 구분됩니다. 다음 예제는 hello, hello 형식에 두 세그먼트와 hello 이름에 하나의 세그먼트가 있으므로 **유효한 이름**합니다.

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "myHostingPlanName",
    ...
  }
  ```

   Hello 다음 예제는 하지만 **유효한 이름이 아닌** hello 있기 때문에 hello 종류로 동일한 세그먼트 수입니다.

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "appPlan/myHostingPlanName",
    ...
  }
  ```

   Hello 형식과 이름을 hello 자식 리소스에 대 한 동일한 세그먼트 수입니다. 이 세그먼트의이 수 때문에 합리적 hello 전체 이름 및 형식을 hello 자식에 대 한 hello 부모 이름 및 형식이 포함 됩니다. 따라서 hello 전체 이름을 아직 hello 전체 형식 보다 적은 하나의 세그먼트가 있습니다.

  ```json
  "resources": [
      {
          "type": "Microsoft.KeyVault/vaults",
          "name": "contosokeyvault",
          ...
          "resources": [
              {
                  "type": "secrets",
                  "name": "appPassword",
                  ...
              }
          ]
      }
  ]
  ```

   오른쪽 가져오는 hello 세그먼트는 리소스 공급자에서 적용 되는 리소스 관리자 유형의 번거로울 수 있습니다. 예를 들어 적용 리소스 잠금 tooa 웹 사이트는 4 개의 세그먼트를 포함 한 형식이 필요 합니다. 따라서 hello 이름은 세 세그먼트입니다.

  ```json
  {
      "type": "Microsoft.Web/sites/providers/locks",
      "name": "[concat(variables('siteName'),'/Microsoft.Authorization/MySiteLock')]",
      ...
  }
  ```

- 인덱스 복사는 사용할 수 없음

   문제가 발생 하면 **InvalidTemplate** hello를 적용 하는 동안 오류가 발생 했습니다. **복사** 이 요소를 지원 하지 않는 hello 서식 파일의 요소 tooa 부분입니다. Hello 복사 요소 tooa 리소스 종류만 적용할 수 있습니다. 리소스 형식 내에서 복사 tooa 속성을 적용할 수 없습니다. 예를 들어 복사 tooa 가상 컴퓨터를 적용 하지만 toohello OS 디스크는 가상 컴퓨터에 대해 적용할 수 없습니다. 경우에 따라 자식 리소스 tooa 부모 리소스 toocreate 복사본 루프를 변환할 수 있습니다. 복사 사용에 대한 자세한 내용은 [Azure Resource Manager에서 리소스의 여러 인스턴스 만들기](resource-group-create-multiple.md)를 참조하세요.

- 잘못된 매개 변수

   Hello 템플릿 매개 변수에 허용 되는 값을 지정 하는 경우 이러한 값 중 하나 하지 않은 값을 제공 하는 메시지와 비슷한 toohello를 다음 오류가 나타납니다.

  ```
  Code=InvalidTemplate;
  Message=Deployment template validation failed: 'hello provided value {parameter value}
  for hello template parameter {parameter name} is not valid. hello parameter value is not
  part of hello allowed values
  ``` 

   다시 확인 hello hello 서식 파일에 허용 되는 값 및 배포 하는 동안 매개 변수를 입력 합니다.

- 순환 종속성이 감지됨

   리소스의 종속 관계 hello 배포를 시작 하지 못하게 하는 방식으로 하는 경우이 오류가 표시 됩니다. 상호 종속성의 조합은 둘 이상의 리소스가 이미 대기 중인 다른 리소스를 기다리게 만듭니다. 예를 들어 리소스1은 리소스3에 종속되고, 리소스2는 리소스1에 종속되고, 리소스3은 리소스2에 종속됩니다. 일반적으로 이런 문제는 불필요한 종속성을 제거하여 해결할 수 있습니다. 

<a id="notfound" />
### <a name="notfound-and-resourcenotfound"></a>NotFound 및 ResourceNotFound
확인할 수 없는 리소스의 hello 이름을 포함 하는 서식 파일에, 다음과 같은 오류가 나타납니다.

```
Code=NotFound;
Message=Cannot find ServerFarm with name exampleplan.
```

Hello 서식 파일에는 리소스가 없습니다 toodeploy hello를 시도 하는 경우 종속성 tooadd 해야 할지 여부를 확인 합니다. 리소스 관리자는 가능한 경우 리소스를 병렬로 만들어 배포를 최적화합니다. 하나의 리소스를 다른 리소스 후 배포 해야 toouse hello **dependsOn** 요소에 대 한 종속성 a 템플릿 toocreate 프로그램에 다른 리소스 hello 합니다. 예를 들어 웹 응용 프로그램을 배포할 때는 hello 앱 서비스 계획 존재 해야 합니다. 리소스 관리자 hello에 리소스가 모두 만듭니다 hello 앱 서비스 계획에 따라 달라 집니다 해당 hello 웹 앱을 지정 하지 않은 경우 동일한 시간입니다. Tooset hello 웹 앱에 대 한 속성을 시도할 때 아직 존재 하지 않으므로 앱 서비스 계획의 리소스를 찾을 수 없으면 해당 hello 라는 오류가 나타납니다. Hello 종속성 hello 웹 응용 프로그램에서 설정 하 여이 오류를 방지 합니다.

```json
{
  "apiVersion": "2015-08-01",
  "type": "Microsoft.Web/sites",
  "dependsOn": [
    "[variables('hostingPlanName')]"
  ],
  ...
}
```

종속성 오류 문제 해결을 위한 제안 사항은 [배포 시퀀스 확인](#check-deployment-sequence)을 참조하세요.

Hello 리소스 하나에 배포 되 고 hello 보다 다른 리소스 그룹에 있는 경우이 오류를 참조 합니다. 이 경우 hello를 사용 하 여 [resourceId 함수](resource-group-template-functions-resource.md#resourceid) tooget hello hello 리소스의 정규화 된 이름입니다.

```json
"properties": {
    "name": "[parameters('siteName')]",
    "serverFarmId": "[resourceId('plangroup', 'Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
}
```

Toouse hello를 시도 하면 [참조](resource-group-template-functions-resource.md#reference) 또는 [Listkey](resource-group-template-functions-resource.md#listkeys) hello 다음 오류가 수신 해결할 수 없는 리소스를 사용 하는 함수:

```
Code=ResourceNotFound;
Message=hello Resource 'Microsoft.Storage/storageAccounts/{storage name}' under resource
group {resource group name} was not found.
```

Hello를 포함 하는 식에 대 한 확인 **참조** 함수입니다. Hello 매개 변수 값이 정확한 지 확인 합니다.

## <a name="parentresourcenotfound"></a>ParentResourceNotFound

하나의 리소스 부모 tooanother 리소스인 경우 hello 부모 리소스 hello 자식 리소스를 만들기 전에 존재 해야 합니다. 아직 존재 하지 않는 경우 hello 다음 오류가 나타납니다.

```
Code=ParentResourceNotFound;
Message=Can not perform requested operation on nested resource. Parent resource 'exampleserver' not found."
```

hello 자식 리소스의 hello 이름을 hello 부모 이름이 포함 됩니다. 예를 들어 SQL Database는 다음과 같이 정의될 수 있습니다.

```json
{
  "type": "Microsoft.Sql/servers/databases",
  "name": "[concat(variables('databaseServerName'), '/', parameters('databaseName'))]",
  ...
```

그러나 hello 부모 리소스에 대 한 종속성을 지정 하지 않으면 hello 자식 리소스 hello 부모 하기 전에 배포 얻을 수 있습니다. tooresolve이이 오류는 종속성을 포함 합니다.

```json
"dependsOn": [
    "[variables('databaseServerName')]"
]
```

<a id="storagenamenotunique" />

## <a name="storageaccountalreadyexists-and-storageaccountalreadytaken"></a>torageAccountAlreadyExists 및 StorageAccountAlreadyTaken
저장소 계정에는 Azure에서 고유 hello 리소스에 대 한 이름을 제공 해야 합니다. 고유한 이름을 제공하지 않으면 다음과 같은 오류 메시지가 표시됩니다.

```
Code=StorageAccountAlreadyTaken
Message=hello storage account named mystorage is already taken.
```

명명 규칙에 따라 hello의 hello 결과 함께 연결 하 여 고유한 이름을 만들 수 있습니다 [uniqueString](resource-group-template-functions-string.md#uniquestring) 함수입니다.

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]",
"type": "Microsoft.Storage/storageAccounts",
```

Hello로 저장소 계정을 배포 하는 경우 구독에서 기존 저장소 계정으로 이름을 동일 하지만 다른 위치를 제공, 나타내는 hello 저장소 계정이 다른 위치에 이미 오류가 발생 합니다. Hello 기존 저장소 계정을 삭제 하거나 제공 hello 기존 저장소 계정으로 같은 위치 hello 합니다.

## <a name="accountnameinvalid"></a>AccountNameInvalid
Hello 참조 **AccountNameInvalid** 금지 된 문자는 저장소 계정을 포함 하는 이름을 toogive를 시도 하는 동안 오류가 발생 했습니다. 저장소 계정 이름은 3자에서 24자 사이여야 하고 숫자 및 소문자만 사용해야 합니다. hello [uniqueString](resource-group-template-functions-string.md#uniquestring) 13 문자가 반환 됩니다. 접두사 toohello을 연결 하는 경우 **uniqueString** 결과 11 자 접두사를 입력이 있습니다.

## <a name="badrequest"></a>BadRequest

속성에 대해 잘못된 값을 제공하면 BadRequest 상태가 발생할 수 있습니다. 예를 들어 저장소 계정에 대 한 잘못 된 SKU 값을 제공 하는 경우 hello 배포가 실패 합니다. 속성에 대 한 유효한 값 toodetermine hello를 살펴보고 [REST API](/rest/api) 배포 하는 hello 리소스 유형에 대 한 합니다.

<a id="noregisteredproviderfound" />

## <a name="noregisteredproviderfound-and-missingsubscriptionregistration"></a>NoRegisteredProviderFound 및 MissingSubscriptionRegistration
리소스를 배포할 때는 hello 오류 코드 다음 수신 및 메시지 수 있습니다.

```
Code: NoRegisteredProviderFound
Message: No registered resource provider found for location {location}
and API version {api-version} for type {resource-type}.
```

또는 다음과 유사한 메시지가 나타날 수 있습니다.

```
Code: MissingSubscriptionRegistration
Message: hello subscription is not registered toouse namespace {resource-provider-namespace}
```

세 가지 이유 중 하나로 이러한 오류가 나타납니다.

1. 구독에 대 한 hello 리소스 공급자 등록 되지 않았습니다.
2. Hello 리소스 종류에 대해 지원 되지 않는 API 버전
3. 위치 hello 리소스 종류에 대해 지원 되지 않습니다

hello 지원 위치 및 API 버전에 대 한 제안을 hello 오류 메시지를 제공 해야 합니다. 사용자 템플릿 tooone hello의 변경할 수 있습니다 제안 된 값입니다. 대부분의 공급자는 전체 열이 아니라 hello를 사용 하는 Azure 포털 또는 hello 명령줄 인터페이스에 의해 자동으로 등록 됩니다. 하기 전에 특정 리소스 공급자를 사용 하지 않은 경우 해당 공급자 tooregister를 할 수 있습니다. PowerShell 또는 Azure CLI를 통해 리소스 공급자에 대해 자세히 확인할 수 있습니다.

**포털**

Hello 등록 상태를 확인 하 고 hello 포털을 통해 리소스 공급자 네임 스페이스를 등록할 수 있습니다.

1. 구독의 경우 **리소스 공급자**를 선택합니다.

   ![리소스 공급자 선택](./media/resource-manager-common-deployment-errors/select-resource-provider.png)

2. 리소스 공급자의 hello 목록을 확인 하 고 필요한 경우 선택 hello **등록** 링크 tooregister hello 리소스 공급자 toodeploy hello 유형의 려 합니다.

   ![리소스 공급자 나열](./media/resource-manager-common-deployment-errors/list-resource-providers.png)

**PowerShell**

toosee 등록 상태를 사용 하 여 **Get AzureRmResourceProvider**합니다.

```powershell
Get-AzureRmResourceProvider -ListAvailable
```

tooregister 공급자를 사용 하 여 **레지스터 AzureRmResourceProvider** hello 이름을 제공 하 고 원하는 tooregister hello 리소스 공급자의 합니다.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Cdn
```

특정 유형의 리소스에 대 한 tooget hello 지원 위치 사용 합니다.

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

tooget hello에 대 한 특정 유형의 리소스를 사용 하 여 지원 되는 API 버전:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).ApiVersions
```

**Azure CLI**

toosee hello 공급자가 등록 되어 있는지 여부를 사용 하 여 hello `azure provider list` 명령입니다.

```azurecli
az provider list
```

tooregister 리소스 공급자를 사용 하 여 hello `azure provider register` 명령을 실행 하 고 hello 지정 *네임 스페이스* tooregister 합니다.

```azurecli
az provider register --namespace Microsoft.Cdn
```

toosee hello 지원 위치 및 리소스 유형에 대 한 API 버전 사용 합니다.

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

<a id="quotaexceeded" />

## <a name="quotaexceeded-and-operationnotallowed"></a>QuotaExceeded 및 OperationNotAllowed
또한 배포가 리소스 그룹, 구독, 계정 및 기타 범위당 할당량을 초과할 경우 문제가 발생할 수 있습니다. 구독이 수 있지만 예를 들어 지역에 대 한 코어 toolimit hello 수를 구성 합니다. 가상 컴퓨터 크기를 허용 하는 hello 보다 더 많은 코어와 toodeploy을 시도 하면 오류가 발생 상자가 hello 할당량을 초과 했습니다.
전체 할당량 정보는 [Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../azure-subscription-service-limits.md)을 참조하세요.

tooexamine 구독 할당량 코어에 대 한 hello를 사용할 수 있습니다 `azure vm list-usage` hello Azure CLI 명령을 합니다. 다음 예제는 hello 무료 평가판 계정을 4에 대 한 해당 hello 코어 할당량을 보여 줍니다.

```azurecli
az vm list-usage --location "South Central US"
```

반환하는 내용은 다음과 같습니다.

```azurecli
[
  {
    "currentValue": 0,
    "limit": 2000,
    "name": {
      "localizedValue": "Availability Sets",
      "value": "availabilitySets"
    }
  },
  ...
]
```

미국 서 부 지역 hello에에서 5 개 이상의 코어를 만드는 템플릿을 배포 하는 경우 다음과 같은 배포 오류가 발생 합니다.

```
Code=OperationNotAllowed
Message=Operation results in exceeding quota limits of Core.
Maximum allowed: 4, Current in use: 4, Additional requested: 2.
```

PowerShell에서 hello를 사용할 수 있습니다 또는 **Get AzureRmVMUsage** cmdlet.

```powershell
Get-AzureRmVMUsage
```

반환하는 내용은 다음과 같습니다.

```powershell
...
CurrentValue : 0
Limit        : 4
Name         : {
                 "value": "cores",
                 "localizedValue": "Total Regional Cores"
               }
Unit         : null
...
```

이러한 경우 toohello 포털 이동 하 고 파일 지원 문제 tooraise toodeploy 넣을 hello 영역에 대 한 할당량 해야 합니다.

> [!NOTE]
> 리소스 그룹에 대 한 hello 할당량은 주의 하지 hello 전체 구독에 대 한 각 개별 지역에 대 한 합니다. Toodeploy 30 코어 West US에 필요한 경우 West US에 30 리소스 관리자 코어 tooask을 해야 합니다. Toodeploy 30 코어 hello 영역 toowhich 중 하나에서 필요한 경우 액세스를 권한이 모든 지역에서 30 리소스 관리자 코어를 요청 해야 합니다.
>
>

## <a name="invalidcontentlink"></a>InvalidContentLink
때 hello 오류 메시지가 나타납니다.

```
Code=InvalidContentLink
Message=Unable toodownload deployment content from ...
```

대개 toolink tooa 중첩 된 서식 파일을 사용할 수 없으면 시도 했습니다. 중첩 된 템플릿 hello에 대 한 제공 된 URI hello를 다시 확인 합니다. Hello 서식 파일에는 저장소 계정에 없는 경우 hello URI에 액세스할 수 있는지 확인 합니다. Toopass SAS 토큰을 할 수 있습니다. 자세한 내용은 [Azure 리소스 관리자에서 연결된 템플릿 사용](resource-group-linked-templates.md)을 참조하세요.

## <a name="requestdisallowedbypolicy"></a>RequestDisallowedByPolicy
구독에 배포 하는 동안 tooperform를 시도 하는 동작을 방지 하는 리소스 정책을 포함 하는 경우이 오류가 표시 됩니다. Hello 오류 메시지에서 hello 정책 식별자를 찾습니다.

```
Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'
```

**PowerShell**, 해당 정책 식별자 hello로 제공 **Id** 배포를 차단한 hello 정책에 대 한 매개 변수 tooretrieve 세부 정보입니다.

```powershell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

**Azure CLI**, hello 정책 정의의 hello 이름을 제공 합니다.

```azurecli
az policy definition show --name regionPolicyAssignment
```

자세한 내용은 다음 문서는 hello 참조:

- [RequestDisallowedByPolicy 오류](resource-manager-policy-requestdisallowedbypolicy-error.md)
- [정책 toomanage 리소스를 사용 하 고 액세스 제어](resource-manager-policy.md)합니다.

## <a name="authorization-failed"></a>권한 부여 실패
없기 때문에 hello 계정 또는 서비스 toodeploy hello 리소스를 시도 하 고 사용자 액세스 tooperform 해당 작업을 배포 하는 동안 오류가 나타날 수 있습니다. Azure Active Directory 또는 사용자 관리자 toocontrol 있는 id 고도로 정밀도 사용 하 여 어떤 리소스에 액세스할 수 있습니다. 예를 들어 계정은 toohello 읽기 역할에 할당 된 없는 경우 수 toocreate 리소스입니다. 이 경우 권한 부여에 실패했다는 오류 메시지가 표시됩니다.

역할 기반 액세스 제어에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md)를 참조하세요.


## <a name="next-steps"></a>다음 단계
* 작업을 감사 하는 방법에 대 한 toolearn 참조 [리소스 관리자와 작업을 감사](resource-group-audit.md)합니다.
* 배포 하는 동안 작업 toodetermine hello 오류에 대 한 toolearn 참조 [배포 작업을 보려면](resource-manager-deployment-operations.md)합니다.
