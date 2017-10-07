---
title: "Azure 리소스 tooprevent 변경 aaaLock | Microsoft Docs"
description: "모든 사용자 및 역할에 대해 잠금을 적용하여 사용자가 중요한 Azure 리소스를 업데이트하거나 삭제하지 못하도록 합니다."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 53c57e8f-741c-4026-80e0-f4c02638c98b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: 1f0d8911b2b129069bd2f01a9a4ec0a3cf700118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="lock-resources-tooprevent-unexpected-changes"></a>잠금 리소스 tooprevent 예기치 않은 변경 내용 
관리자로 서에서 할 수 있습니다 toolock 구독, 리소스 그룹 또는 리소스 tooprevent 다른 사용자가 조직 실수로 삭제 하거나 중요 한 리소스를 수정 합니다. 너무 hello 잠금 수준을 설정할 수 있습니다**CanNotDelete** 또는 **ReadOnly**합니다. 

* **CanNotDelete** 계속 권한이 있는 사용자가 읽고는 리소스를 수정할 수 있지만 hello 리소스를 삭제할 수는 없습니다 것을 의미 합니다. 
* **읽기 전용** 권한이 있는 사용자는 리소스를 읽을 수는 있지만 hello 리소스를 업데이트 하거나 삭제할 수는 없습니다 것을 의미 합니다. 이 잠금은 적용 하는 것은 hello에 의해 부여 된 사용자가 toohello 권한에 모든 권한 있는 비슷한 toorestricting **판독기** 역할입니다. 

## <a name="how-locks-are-applied"></a>잠금을 적용하는 방법

부모 범위에서 잠금을 적용 하면 해당 범위 내에서 모든 리소스 상속 hello 동일한 잠금. Hello 잠금 hello 부모에서 상속 하는 리소스도 나중에 추가 합니다. hello hello 상속에 가장 제한적인 잠금 우선 적용 됩니다.

역할 기반 액세스 제어와 달리 모든 사용자 및 역할에서 관리 잠금 tooapply 제한을 사용합니다. 사용자 및 역할에 대 한 사용 권한을 설정 하는 방법에 대 한 toolearn 참조 [Azure 역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md)합니다.

리소스 관리자 잠금을 적용 너무 전송 작업으로 구성 되는 hello 관리 평면에서 발생 하는 toooperations만`https://management.azure.com`합니다. hello 잠금 리소스에서 자신의 기능을 수행 하는 방법을 제한 하지 않습니다. 리소스 변경은 제한되지만 리소스 작업은 제한되지 않습니다. 예를 들어 SQL 데이터베이스에 대 한 읽기 전용 잠금을 못하도록 삭제 하거나 수정 하지만 hello 데이터베이스 때도 만들기, 업데이트 또는 hello 데이터베이스의에서 데이터를 삭제할 수 있습니다. 이러한 작업이 너무 보내지지 않기 때문에 데이터 트랜잭션이 허용 됩니다`https://management.azure.com`합니다.

적용 **ReadOnly** 처럼 보일 수도 있지만 일부 작업 읽기 작업에 추가 작업을 실제로 필요 하기 때문에 toounexpected 결과가 발생할 수 있습니다. 예를 들어 배치는 **ReadOnly** 저장소 계정에 대 한 잠금을 나열 hello 키의 모든 사용자가 방지 합니다. 키 작업 hello 키에 사용할 수 있는 반환 했기 때문에 POST 요청을 통해 처리 hello 목록 쓰기 작업입니다. 또 다른 예로, 배치는 **ReadOnly** 앱 서비스 리소스 수 없습니다 Visual Studio 서버 탐색기에서 상호 작용을 지 쓰기 권한이 필요 하기 때문에 hello 리소스에 대 한 파일을 표시 합니다.

## <a name="who-can-create-or-delete-locks-in-your-organization"></a>조직에서 잠금을 만들거나 삭제할 수 있는 사람
관리 잠금 toocreate 또는 delete 권한이 너무`Microsoft.Authorization/*` 또는 `Microsoft.Authorization/locks/*` 동작 합니다. Hello 기본 제공 역할 중만 **소유자** 및 **사용자 액세스 관리자에 게** 이러한 작업을 부여 됩니다.

## <a name="portal"></a>포털
[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="template"></a>템플릿
hello 다음 예제에서는 저장소 계정에 대 한 잠금을 만드는 템플릿을 hello 저장소 계정에는 tooapply hello 잠금은 매개 변수로 제공 됩니다. hello hello 잠금의 이름을 연결 하 여 만듭니다 hello 리소스 이름의 **/Microsoft.Authorization/** hello 잠금의 이름을 경우 hello 및 **myLock**합니다.

제공 된 hello 형식은 특정 toohello 리소스 형식이입니다. 저장소에 대 한 hello 유형 too"Microsoft.Storage/storageaccounts/providers/locks set"입니다.

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "lockedResource": {
          "type": "string"
        }
      },
      "resources": [
        {
          "name": "[concat(parameters('lockedResource'), '/Microsoft.Authorization/myLock')]",
          "type": "Microsoft.Storage/storageAccounts/providers/locks",
          "apiVersion": "2015-01-01",
          "properties": {
            "level": "CannotDelete"
          }
        }
      ]
    }

## <a name="powershell"></a>PowerShell
사용자 잠금 hello를 사용 하 여 Azure PowerShell을 사용 하 여 리소스를 배포 [새로 AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock) 명령입니다.

toolock 리소스에 hello 리소스의 hello 이름, 해당 리소스 종류 및 해당 리소스 그룹 이름을 제공 합니다.

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockSite `
  -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

toolock 리소스 그룹에는 hello 리소스 그룹의 hello 이름을 제공 합니다.

```powershell
New-AzureRmResourceLock -LockName LockGroup -LockLevel CanNotDelete `
  -ResourceGroupName exampleresourcegroup
```

잠금 사용 하는 방법에 대 한 정보 tooget [Get AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock)합니다. tooget 구독에서 모든 hello 잠금을 사용 합니다.

```powershell
Get-AzureRmResourceLock
```

tooget 리소스에 대 한 모든 잠금을 사용 합니다.

```powershell
Get-AzureRmResourceLock -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

tooget 리소스 그룹에 대 한 모든 잠금을 사용 합니다.

```powershell
Get-AzureRmResourceLock -ResourceGroupName exampleresourcegroup
```

Azure PowerShell 작업 잠금에 대 한와 같은 다른 명령에는 [집합 AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) tooupdate 잠금 및 [제거 AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) toodelete 잠금 합니다.

## <a name="azure-cli"></a>Azure CLI

사용자 잠금 hello를 사용 하 여 Azure CLI를 사용 하 여 리소스를 배포 [az 잠금을 만들](/cli/azure/lock#create) 명령입니다.

toolock 리소스에 hello 리소스의 hello 이름, 해당 리소스 종류 및 해당 리소스 그룹 이름을 제공 합니다.

```azurecli
az lock create --name LockSite --lock-type CanNotDelete \
  --resource-group exampleresourcegroup --resource-name examplesite \
  --resource-type Microsoft.Web/sites
```

toolock 리소스 그룹에는 hello 리소스 그룹의 hello 이름을 제공 합니다.

```azurecli
az lock create --name LockGroup --lock-type CanNotDelete \
  --resource-group exampleresourcegroup
```

잠금 사용 하는 방법에 대 한 정보 tooget [az 잠금 목록](/cli/azure/lock#list)합니다. tooget 구독에서 모든 hello 잠금을 사용 합니다.

```azurecli
az lock list
```

tooget 리소스에 대 한 모든 잠금을 사용 합니다.

```azurecli
az lock list --resource-group exampleresourcegroup --resource-name examplesite \
  --namespace Microsoft.Web --resource-type sites --parent ""
```

tooget 리소스 그룹에 대 한 모든 잠금을 사용 합니다.

```azurecli
az lock list --resource-group exampleresourcegroup
```

Azure CLI 작업 잠금에 대 한와 같은 다른 명령의 제공 [az 잠금 업데이트](/cli/azure/lock#update) tooupdate 잠금 및 [az 잠금 삭제](/cli/azure/lock#delete) toodelete 잠금 합니다.

## <a name="rest-api"></a>REST API
Hello 사용 하 여 배포 된 리소스를 잠글 수 [관리 잠금에 대 한 REST API](https://docs.microsoft.com/rest/api/resources/managementlocks)합니다. REST API hello toocreate 및 잠금 삭제 있으며 기존 잠금에 대 한 정보를 검색 합니다.

toocreate 잠금을 실행 하는 중:

    PUT https://management.azure.com/{scope}/providers/Microsoft.Authorization/locks/{lock-name}?api-version={api-version}

구독, 리소스 그룹 또는 리소스 hello 범위 수 있습니다. hello 잠금 이름이 원하는 작업이 무엇이 든 toocall hello 잠금. api-version에는 **2015-01-01**을 사용합니다.

Hello 요청 hello 잠금에 대 한 hello 속성을 지정 하는 JSON 개체를 포함 합니다.

    {
      "properties": {
        "level": "CanNotDelete",
        "notes": "Optional text notes."
      }
    } 

## <a name="next-steps"></a>다음 단계
* 리소스 잠금 작업에 대한 자세한 내용은 [Azure 리소스 잠금](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)
* 에서는 리소스를 논리적으로 구성 하는 방법에 대 한 toolearn 참조 [를 사용 하 여 태그 tooorganize 리소스](resource-group-using-tags.md)
* 리소스 그룹 리소스에 있는 toochange 참조 [리소스 toonew 리소스 그룹 이동](resource-group-move-resources.md)
* 사용자 지정된 정책을 사용하여 구독을 통해 제한 사항 및 규칙을 적용할 수 있습니다. 자세한 내용은 참조 [toomanage 리소스 사용 정책 및 액세스 제어](resource-manager-policy.md)합니다.
* 기업에서는 리소스 관리자 tooeffectively 사용 방법에 대 한 지침에 대 한 구독을 관리, 참조 [Azure enterprise 스 캐 폴드-규범적인 구독 거 버 넌 스](resource-manager-subscription-governance.md)합니다.

