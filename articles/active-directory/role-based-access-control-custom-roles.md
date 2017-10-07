---
title: "Azure RBAC에 대 한 사용자 지정 역할 aaaCreate | Microsoft Docs"
description: "자세한 내용은 방법 Azure 구독에서 보다 정확 하 게 id 관리를 위한 신속히 알아봅니다 액세스 제어를 사용한 toodefine 사용자 정의 역할입니다."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: e4206ea9-52c3-47ee-af29-f6eef7566fa5
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/11/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 60df12632ef6c086d5feeb1809196d7c4ee5e021
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-roles-for-azure-role-based-access-control"></a>Azure 역할 기반 액세스 제어의 사용자 지정 역할 만들기
Hello 기본 제공 역할 중 어떤 특정 액세스 요구 사항에 맞지 않을 경우 사용자 지정 역할 신속히 알아봅니다 액세스 제어 (RBAC)를 만듭니다. 사용 하 여 사용자 지정 역할을 만들 수 [Azure PowerShell](role-based-access-control-manage-access-powershell.md), [Azure 명령줄 인터페이스](role-based-access-control-manage-access-azure-cli.md) (CLI) 및 hello [REST API](role-based-access-control-manage-access-rest.md)합니다. 기본 제공 역할에서와 마찬가지로 사용자 지정 역할 toousers, 그룹 및 구독, 리소스 그룹 및 리소스 범위에서 응용 프로그램을 할당할 수 있습니다. 사용자 지정 역할은 Azure AD 테넌트에 저장되고 구독에서 공유할 수 있습니다.

각 테 넌 트 too2000 사용자 지정 역할을 만들 수 있습니다. 

hello 다음 예제는 모니터링 및 가상 컴퓨터를 다시 시작을 위한 사용자 지정 역할.

```
{
  "Name": "Virtual Machine Operator",
  "Id": "cadb4a5a-4e7a-47be-84db-05cad13b6769",
  "IsCustom": true,
  "Description": "Can monitor and restart virtual machines.",
  "Actions": [
    "Microsoft.Storage/*/read",
    "Microsoft.Network/*/read",
    "Microsoft.Compute/*/read",
    "Microsoft.Compute/virtualMachines/start/action",
    "Microsoft.Compute/virtualMachines/restart/action",
    "Microsoft.Authorization/*/read",
    "Microsoft.Resources/subscriptions/resourceGroups/read",
    "Microsoft.Insights/alertRules/*",
    "Microsoft.Insights/diagnosticSettings/*",
    "Microsoft.Support/*"
  ],
  "NotActions": [

  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624",
    "/subscriptions/34370e90-ac4a-4bf9-821f-85eeedeae1a2"
  ]
}
```
## <a name="actions"></a>작업
hello **동작** 사용자 지정 역할의 속성 지정 hello Azure 작업 toowhich hello 역할에 대 한 액세스 권한을 부여 합니다. Azure 리소스 공급자의 보안 개체 작업을 식별하는 작업 문자열 모음입니다. 작업 문자열의 hello 형식에 따라 `Microsoft.<ProviderName>/<ChildResourceType>/<action>`합니다. 와일드 카드를 포함 하는 작업 문자열 (\*) tooall 작업 hello 작업 문자열과 일치 하는 액세스를 허용 합니다. 예:

* `*/read`모든 Azure 리소스 공급자의 모든 리소스 종류에 대 한 tooread 작업 액세스를 부여 합니다.
* `Microsoft.Compute/*`tooall 작업 hello Microsoft.Compute 리소스 공급자에서 모든 리소스 종류에 대 한 액세스를 부여 합니다.
* `Microsoft.Network/*/read`Azure의 hello Microsoft.Network 리소스 공급자에서 모든 리소스 종류에 대 한 tooread 작업 액세스를 부여 합니다.
* `Microsoft.Compute/virtualMachines/*`가상 컴퓨터 및 해당 자식 리소스 형식의 tooall 작업 액세스를 부여 합니다.
* `Microsoft.Web/sites/restart/Action`부여는 toorestart 웹 사이트에 액세스 합니다.

사용 하 여 `Get-AzureRmProviderOperation` (PowerShell)에서 또는 `azure provider operations show` (Azure CLI)에서 Azure 리소스 공급자의 toolist 작업 합니다. 이러한 명령은 tooverify 작업 문자열 올바른지 및 tooexpand 와일드 카드 작업 문자열을 사용할 수도 있습니다.

```
Get-AzureRMProviderOperation Microsoft.Compute/virtualMachines/*/action | FT Operation, OperationName

Get-AzureRMProviderOperation Microsoft.Network/*
```

![PowerShell 스크린샷 - Get-AzureRMProviderOperation](./media/role-based-access-control-configure/1-get-azurermprovideroperation-1.png)

```
azure provider operations show "Microsoft.Compute/virtualMachines/*/action" --js on | jq '.[] | .operation'

azure provider operations show "Microsoft.Network/*"
```

![Azure CLI 스크린샷 - azure 공급자 작업 표시 "Microsoft.Compute/virtualMachines/\*/action" ](./media/role-based-access-control-configure/1-azure-provider-operations-show.png)

## <a name="notactions"></a>NotActions
사용 하 여 hello **NotActions** tooallow 원하는 작업 hello 집합은 제한 된 작업을 제외 하 여 보다 쉽게 정의 하는 경우 속성을 사용 합니다. hello 사용자 지정 역할에 의해 부여 된 액세스는 빼는 방식으로 계산 hello **NotActions** hello에서 작업 **동작** 작업 합니다.

> [!NOTE]
> 사용자의 작업을 제외 하는 역할이 할당 하는 경우 **NotActions**, 액세스를 부여 하는 두 번째 역할 할당은 동일한 작업을 hello 사용자가 toohello tooperform 해당 작업을 허용 합니다. **NotActions** deny가 규칙 – 특정 작업 toobe 제외 해야 하는 경우 단순히 편리한 방법을 toocreate 허용 되는 작업의 집합에는 합니다.
>
>

## <a name="assignablescopes"></a>AssignableScopes
hello **AssignableScopes** hello 사용자 지정 역할의 속성을 사용자 지정 역할은 할당에 사용할 수 있는 hello 내 hello 범위 (구독, 리소스 그룹 또는 리소스)을 지정 합니다. Hello 사용자 지정 역할 할당에 사용할 수 있는 hello 구독만에서 만들거나 hello 나머지 hello 구독 또는 리소스 그룹에 대 한 리소스 그룹 및 사용자가 아닌 간단 하 게 표시 해야 하는 환경입니다.

유효한 할당 가능한 범위의 예는 다음과 같습니다.

* "/ 구독/c276fc76-9cd4-44c9-99a7-4fd71546436e", "/ 구독/e91d47c4-76f3-4271-a796-21b4ecfe3624"-두 구독에 할당에 사용할 수 있는 hello 역할을 만듭니다.
* "/ 구독/c276fc76-9cd4-44c9-99a7-4fd71546436e"-단일 구독에 할당에 사용할 수 있는 hello 역할을 만듭니다.
* "/ 구독/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/네트워크"-는 hello 역할 hello 네트워크 리소스 그룹에만 할당 될 수 있습니다.

> [!NOTE]
> 구독, 리소스 그룹 또는 리소스 ID를 적어도 하나 사용해야 합니다.
>
>

## <a name="custom-roles-access-control"></a>사용자 지정 역할 액세스 제어
hello **AssignableScopes** hello 사용자 지정 역할의 속성을 보고, 수정 및 hello 역할을 삭제할 수 있는 제어 합니다.

* 사용자 지정 역할을 만들 수 있는 사람
    구독, 리소스 그룹 및 리소스의 소유자(및 사용자 액세스 관리자)는 해당 범위에 사용할 사용자 지정 역할을 만들 수 있습니다.
    hello hello 역할을 만드는 사용자 필요한 toobe 수 tooperform `Microsoft.Authorization/roleDefinition/write` 모든 hello에 대 한 작업이 **AssignableScopes** hello 역할의 합니다.
* 사용자 지정 역할을 수정할 수 있는 사람
    구독, 리소스 그룹 및 리소스의 소유자(및 사용자 액세스 관리자)는 해당 범위에 사용자 지정 역할을 수정할 수 있습니다. 사용자에 게 필요 toobe 수 tooperform hello `Microsoft.Authorization/roleDefinition/write` 모든 hello에 대 한 작업이 **AssignableScopes** 사용자 지정 역할을 합니다.
* 사용자 지정 역할을 볼 수 있는 사용자는 누구인가요?
    Azure RBAC에서 모든 기본 제공 역할은 할당 가능한 역할을 볼 수 있습니다. Hello를 수행할 수 있는 사용자 `Microsoft.Authorization/roleDefinition/read` 작업 범위에서 해당 범위에서 할당에 사용할 수 있는 hello RBAC 역할을 볼 수 있습니다.

## <a name="see-also"></a>참고 항목
* [역할 기반 액세스 제어](role-based-access-control-configure.md): RBAC hello Azure 포털을에서 시작 합니다.
* Toomanage로 액세스 하는 방법에 대해 알아봅니다.
  * [PowerShell](role-based-access-control-manage-access-powershell.md)
  * [Azure CLI](role-based-access-control-manage-access-azure-cli.md)
  * [REST API](role-based-access-control-manage-access-rest.md)
* [기본 제공 역할](role-based-access-built-in-roles.md): RBAC에 기본적으로 제공 하는 hello 역할에 대 한 세부 정보를 가져옵니다.
