---
title: "aaaAzure 리소스 공급자 및 리소스 종류 | Microsoft Docs"
description: "리소스 관리자, 스키마 및 사용 가능한 API 버전을 지 원하는 hello 리소스 공급자 및 hello 리소스를 호스팅할 수 있는 hello 영역에 설명 합니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 3c7a6fe4-371a-40da-9ebe-b574f583305b
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: tomfitz
ms.openlocfilehash: 23db1d3808a20166f3b44ec801e1bcc46fbb9bd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-providers-and-types"></a>리소스 공급자 및 형식

리소스를 배포할 때는 hello 리소스 공급자 및 형식에 대 한 tooretrieve 정보가 자주 필요 합니다. 이 문서에서는 다음을 설명합니다.

* Azure의 모든 리소스 공급자 보기
* 리소스 공급자의 등록 상태 확인
* 리소스 공급자 등록
* 리소스 공급자에 대한 리소스 종류 보기
* 리소스 종류에 대한 유효한 위치 보기
* 리소스 종류에 대한 유효한 API 버전 보기

Hello 포털, PowerShell 또는 Azure CLI를 통해 이러한 단계를 수행할 수 있습니다.

## <a name="powershell"></a>PowerShell

toosee Azure 및 구독에 대 한 hello 등록 상태에서 모든 리소스 공급자를 사용합니다.

```powershell
Get-AzureRmResourceProvider -ListAvailable | Select-Object ProviderNamespace, RegistrationState
```

반환 결과는 다음과 비슷합니다.

```powershell
ProviderNamespace                RegistrationState
-------------------------------- ------------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

리소스 공급자 등록 중 hello 리소스 공급자에 구독 toowork을 구성 합니다. 등록에 대 한 hello 범위 항상 hello 구독입니다. 기본적으로 대부분의 리소스 공급자는 자동으로 등록됩니다. 할 수 있습니다 toomanually 일부 리소스 공급자를 등록 합니다. 리소스 공급자 tooregister 있어야 권한 tooperform hello `/register/action` hello 리소스 공급자에 대 한 작업입니다. 이 작업은 참가자 hello 및 소유자 역할에 포함 됩니다.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

반환 결과는 다음과 비슷합니다.

```powershell
ProviderNamespace : Microsoft.Batch
RegistrationState : Registering
ResourceTypes     : {batchAccounts, operations, locations, locations/quotas}
Locations         : {West Europe, East US, East US 2, West US...}
```

구독에 리소스 공급자의 리소스 종류가 아직 포함되어 있으면 해당 리소스 공급자를 등록 취소할 수 없습니다.

특정 리소스 공급자를 사용 하 여 toosee 정보:

```powershell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

반환 결과는 다음과 비슷합니다.

```powershell
{ProviderNamespace : Microsoft.Batch
RegistrationState : Registered
ResourceTypes     : {batchAccounts}
Locations         : {West Europe, East US, East US 2, West US...}

...
```

리소스 공급자에 대 한 toosee hello 리소스 형식을 사용 합니다.

```powershell
(Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes.ResourceTypeName
```

반환하는 내용은 다음과 같습니다.

```powershell
batchAccounts
operations
locations
locations/quotas
```

hello API 버전 tooa 버전의 hello 리소스 공급자가 릴리스되는 REST API 작업은 해당 합니다. 리소스 공급자를 통해 새로운 기능, 새 버전의 hello REST API를 해제 합니다. 

리소스 유형에 대 한 tooget hello 사용 가능한 API 버전을 사용 합니다.

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).ApiVersions
```

반환하는 내용은 다음과 같습니다.

```powershell
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

모든 지역에서 리소스 관리자가 지원 되지만 hello 리소스 배포한 모든 지역에서 지원 되지 않는 경우. 또한 hello 리소스를 지 원하는 일부 영역을 사용 하지 못하게 하는 구독에 제한 사항이 있을 수 있습니다. 

리소스 종류에 대 한 tooget hello 지원 위치를 사용 합니다.

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).Locations
```

반환하는 내용은 다음과 같습니다.

```powershell
West Europe
East US
East US 2
West US
...
```

## <a name="azure-cli"></a>Azure CLI
toosee Azure 및 구독에 대 한 hello 등록 상태에서 모든 리소스 공급자를 사용합니다.

```azurecli
az provider list --query "[].{Provider:namespace, Status:registrationState}" --out table
```

반환 결과는 다음과 비슷합니다.

```azurecli
Provider                         Status
-------------------------------- ----------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

리소스 공급자 등록 중 hello 리소스 공급자에 구독 toowork을 구성 합니다. 등록에 대 한 hello 범위 항상 hello 구독입니다. 기본적으로 대부분의 리소스 공급자는 자동으로 등록됩니다. 할 수 있습니다 toomanually 일부 리소스 공급자를 등록 합니다. 리소스 공급자 tooregister 있어야 권한 tooperform hello `/register/action` hello 리소스 공급자에 대 한 작업입니다. 이 작업은 참가자 hello 및 소유자 역할에 포함 됩니다.

```azurecli
az provider register --namespace Microsoft.Batch
```

등록이 진행 중인 메시지를 반환합니다.

구독에 리소스 공급자의 리소스 종류가 아직 포함되어 있으면 해당 리소스 공급자를 등록 취소할 수 없습니다.

특정 리소스 공급자를 사용 하 여 toosee 정보:

```azurecli
az provider show --namespace Microsoft.Batch
```

반환 결과는 다음과 비슷합니다.

```azurecli
{
    "id": "/subscriptions/####-####/providers/Microsoft.Batch",
    "namespace": "Microsoft.Batch",
    "registrationsState": "Registering",
    "resourceTypes:" [
        ...
    ]
}
```

리소스 공급자에 대 한 toosee hello 리소스 형식을 사용 합니다.

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[*].resourceType" --out table
```

반환하는 내용은 다음과 같습니다.

```azurecli
Result
---------------
batchAccounts
operations
locations
locations/quotas
```

hello API 버전 tooa 버전의 hello 리소스 공급자가 릴리스되는 REST API 작업은 해당 합니다. 리소스 공급자를 통해 새로운 기능, 새 버전의 hello REST API를 해제 합니다. 

리소스 유형에 대 한 tooget hello 사용 가능한 API 버전을 사용 합니다.

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].apiVersions | [0]" --out table
```

반환하는 내용은 다음과 같습니다.

```azurecli
Result
---------------
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

모든 지역에서 리소스 관리자가 지원 되지만 hello 리소스 배포한 모든 지역에서 지원 되지 않는 경우. 또한 hello 리소스를 지 원하는 일부 영역을 사용 하지 못하게 하는 구독에 제한 사항이 있을 수 있습니다. 

리소스 종류에 대 한 tooget hello 지원 위치를 사용 합니다.

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].locations | [0]" --out table
```

반환하는 내용은 다음과 같습니다.

```azurecli
Result
---------------
West Europe
East US
East US 2
West US
...
```

## <a name="portal"></a>포털

Azure 및 구독에 대 한 hello 등록 상태에서 모든 리소스 공급자 선택 toosee **구독**합니다.

![구독 선택](./media/resource-manager-supported-services/select-subscriptions.png)

Hello 구독 tooview를 선택 합니다.

![구독 지정](./media/resource-manager-supported-services/subscription.png)

선택 **리소스 공급자** 및 사용 가능한 리소스 공급자의 뷰 hello 목록입니다.

![리소스 공급자 보기](./media/resource-manager-supported-services/show-resource-providers.png)

리소스 공급자 등록 중 hello 리소스 공급자에 구독 toowork을 구성 합니다. 등록에 대 한 hello 범위 항상 hello 구독입니다. 기본적으로 대부분의 리소스 공급자는 자동으로 등록됩니다. 할 수 있습니다 toomanually 일부 리소스 공급자를 등록 합니다. 리소스 공급자 tooregister 있어야 권한 tooperform hello `/register/action` hello 리소스 공급자에 대 한 작업입니다. 이 작업은 참가자 hello 및 소유자 역할에 포함 됩니다. 리소스 공급자 tooregister 선택 **등록**합니다.

![리소스 공급자 등록](./media/resource-manager-supported-services/register-provider.png)

구독에 리소스 공급자의 리소스 종류가 아직 포함되어 있으면 해당 리소스 공급자를 등록 취소할 수 없습니다.

특정 리소스 공급자에 대 한 정보 toosee 선택 **더 많은 서비스**합니다.

![추가 서비스 선택](./media/resource-manager-supported-services/more-services.png)

검색할 **리소스 탐색기** hello 사용 가능한 옵션에서 선택 합니다.

![리소스 탐색기 선택](./media/resource-manager-supported-services/select-resource-explorer.png)

**공급자**를 선택합니다.

![공급자 선택](./media/resource-manager-supported-services/select-providers.png)

리소스 공급자 선택 hello 및 리소스 tooview 한다는 것을 입력 합니다.

![리소스 종류 선택](./media/resource-manager-supported-services/select-resource-type.png)

모든 지역에서 리소스 관리자가 지원 되지만 hello 리소스 배포한 모든 지역에서 지원 되지 않는 경우. 또한 hello 리소스를 지 원하는 일부 영역을 사용 하지 못하게 하는 구독에 제한 사항이 있을 수 있습니다. hello 리소스 탐색기 hello 리소스 유형에 대 한 유효한 위치가 표시 됩니다.

![위치 표시](./media/resource-manager-supported-services/show-locations.png)

hello API 버전 tooa 버전의 hello 리소스 공급자가 릴리스되는 REST API 작업은 해당 합니다. 리소스 공급자를 통해 새로운 기능, 새 버전의 hello REST API를 해제 합니다. 리소스 탐색기 hello hello 리소스 종류에 대해 유효한 API 버전을 표시합니다.

![API 버전 표시](./media/resource-manager-supported-services/show-api-versions.png)

## <a name="next-steps"></a>다음 단계
* 리소스 관리자 템플릿을 만드는 방법에 대해 toolearn 참조 [제작 Azure 리소스 관리자 템플릿을](resource-group-authoring-templates.md)합니다.
* 리소스를 배포 하는 방법에 대 한 toolearn 참조 [Azure 리소스 관리자 템플릿 사용 하 여 응용 프로그램 배포](resource-group-template-deploy.md)합니다.
* 리소스 공급자에 대 한 tooview hello 작업 참조 [Azure REST API](/rest/api/)합니다.

