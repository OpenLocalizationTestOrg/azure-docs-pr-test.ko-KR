---
title: "역할 기반 액세스 제어 (RBAC) Azure PowerShell을 사용한 aaaManage | Microsoft Docs"
description: "어떻게 toomanage RBAC 역할, 역할, 할당 및 역할 할당 삭제를 포함 하 여 Azure PowerShell을 사용 합니다."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 9e225dba-9044-4b13-b573-2f30d77925a9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: fa44991113e75b345177867b0bede38de4373e04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control-with-azure-powershell"></a>Azure PowerShell을 사용하여 역할 기반 액세스 제어 관리
> [!div class="op_single_selector"]
> * [PowerShell](role-based-access-control-manage-access-powershell.md)
> * [Azure CLI](role-based-access-control-manage-access-azure-cli.md)
> * [REST API](role-based-access-control-manage-access-rest.md)

Hello Azure 포털 및 Azure 리소스 관리 API toomanage 액세스 tooyour 구독 세분화 된 수준에서 역할 기반 액세스 제어 (RBAC)를 사용할 수 있습니다. 이 기능을 특정 범위에서 일부 역할 toothem 할당 하 여 Active Directory 사용자, 그룹 또는 서비스 사용자에 대 한 액세스를 부여할 수 있습니다.

PowerShell toomanage RBAC를 사용 하려면 먼저 다음 필수 구성 요소는 hello:

* Azure PowerShell 버전 0.8.8 이상. Azure 구독으로 참조 tooinstall hello에 대 한 최신 정보 및 연결 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.
* Azure Resource Manager cmdlet. Hello 설치 [Azure 리소스 관리자 cmdlet](/powershell/azure/overview) PowerShell에서 합니다.

## <a name="list-roles"></a>역할 나열
### <a name="list-all-available-roles"></a>사용 가능한 모든 역할 나열
toolist RBAC 역할 할당 및 tooinspect hello 작업 toowhich 액세스를 부여 하는 데 사용할 수 있는 사용 `Get-AzureRmRoleDefinition`합니다.

```
Get-AzureRmRoleDefinition | FT Name, Description
```

![RBAC PowerShell - Get-AzureRmRoleDefinition - 스크린샷](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition1.png)

### <a name="list-actions-of-a-role"></a>역할의 작업 나열
사용 하 여 특정 역할에 대 한 toolist hello 작업 `Get-AzureRmRoleDefinition <role name>`합니다.

```
Get-AzureRmRoleDefinition Contributor | FL Actions, NotActions

(Get-AzureRmRoleDefinition "Virtual Machine Contributor").Actions
```

![RBAC PowerShell - 특정 역할에 대한 Get-AzureRmRoleDefinition - 스크린샷](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition2.png)

## <a name="see-who-has-access"></a>액세스 권한이 있는 사용자 확인
toolist RBAC 액세스 할당을 사용 하 여 `Get-AzureRmRoleAssignment`합니다.

### <a name="list-role-assignments-at-a-specific-scope"></a>특정 범위의 역할 할당 나열
지정 된 구독, 리소스 그룹 또는 리소스에 대 한 모든 hello 액세스 할당을 볼 수 있습니다. 예를 들어 toosee hello 사용 하 여 리소스 그룹에 대 한 모든 hello 활성 할당 `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`합니다.

```
Get-AzureRmRoleAssignment -ResourceGroupName Pharma-Sales-ProjectForcast | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell - 리소스 그룹에 대한 Get-AzureRmRoleAssignment - 스크린샷](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment1.png)

### <a name="list-roles-assigned-tooa-user"></a>할당 된 tooa 사용자 역할 나열
toolist tooa 할당 되는 모든 hello 역할이 지정 하 고 사용자 hello toowhich hello 사용자가 속한 toohello 그룹에 할당 된 사용 `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`합니다.

```
Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com | FL DisplayName, RoleDefinitionName, Scope

Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com -ExpandPrincipalGroups | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell - 사용자에 대한 Get-AzureRmRoleAssignment - 스크린샷](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment2.png)

### <a name="list-classic-service-administrator-and-coadmin-role-assignments"></a>클래식 서비스 관리자 및 공동 관리자 역할 할당 나열
클래식 구독 관리자에 게 및 coadministrators에 대 한 toolist 액세스 할당을 사용 합니다.

    Get-AzureRmRoleAssignment -IncludeClassicAdministrators

## <a name="grant-access"></a>액세스 권한 부여
### <a name="search-for-object-ids"></a>개체 ID 검색
tooidentify 해야 역할 tooassign hello 개체 (사용자, 그룹 또는 응용 프로그램)와 hello 범위입니다.

Hello 구독 ID를 모르는 경우 hello에서 찾을 수 있습니다 **구독** 블레이드 hello Azure 포털에 있습니다. tooquery hello 구독 ID에 대 한 참조 toolearn [Get-azuresubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) msdn 합니다.

Azure AD 그룹에 대 한 tooget hello 개체 ID를 사용 합니다.

    Get-AzureRmADGroup -SearchString <group name in quotes>

tooget hello 개체 ID를 Azure AD 서비스 사용자 또는 응용 프로그램을 사용 합니다.

    Get-AzureRmADServicePrincipal -SearchString <service name in quotes>

### <a name="assign-a-role-tooan-application-at-hello-subscription-scope"></a>Hello 구독 범위에서 역할 tooan 응용 프로그램 할당
toogrant 액세스 tooan 응용 프로그램이 hello 구독 범위에서 사용 하 여:

    New-AzureRmRoleAssignment -ObjectId <application id> -RoleDefinitionName <role name> -Scope <subscription id>

![RBAC PowerShell - New-AzureRmRoleAssignment - 스크린샷](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment2.png)

### <a name="assign-a-role-tooa-user-at-hello-resource-group-scope"></a>Hello 리소스 그룹 범위에서 역할 tooa 사용자 지정
toogrant 액세스 tooa hello 리소스 그룹 범위에서 사용 하 여 사용자:

    New-AzureRmRoleAssignment -SignInName <email of user> -RoleDefinitionName <role name in quotes> -ResourceGroupName <resource group name>

![RBAC PowerShell - New-AzureRmRoleAssignment - 스크린샷](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment3.png)

### <a name="assign-a-role-tooa-group-at-hello-resource-scope"></a>Hello 리소스 범위에서 역할 tooa 그룹 할당
hello 리소스 범위에서 사용 하 여 toogrant 액세스 tooa 그룹:

    New-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name in quotes> -ResourceName <resource name> -ResourceType <resource type> -ParentResource <parent resource> -ResourceGroupName <resource group name>

![RBAC PowerShell - New-AzureRmRoleAssignment - 스크린샷](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment4.png)

## <a name="remove-access"></a>액세스 권한 제거
사용자, 그룹 및 응용 프로그램을 사용 하기 위해 tooremove 액세스:

    Remove-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name> -Scope <scope such as subscription id>

![RBAC PowerShell - Remove-AzureRmRoleAssignment - 스크린샷](./media/role-based-access-control-manage-access-powershell/3-remove-azure-rm-role-assignment.png)

## <a name="create-a-custom-role"></a>사용자 지정 역할 만들기
사용자 지정 역할 toocreate hello를 사용 하 여 ```New-AzureRmRoleDefinition``` 명령입니다. PSRoleDefinitionObject 또는 JSON 템플릿을 사용 하 여 hello 역할을 구성 하는 방법은 두 가지가 있습니다. 

## <a name="get-actions-for-a-resource-provider"></a>리소스 공급자에 대한 작업 가져오기
처음부터 사용자 정의 역할을 만드는 경우에 중요 한 tooknow 모든 hello hello 리소스 공급자에서 가능한 모든 작업.
사용 하 여 hello ```Get-AzureRMProviderOperation``` 명령 tooget이이 정보입니다.
예를 들어 toocheck 하려는 경우 가상 컴퓨터에 대 한 모든 hello 사용 가능한 작업에이 명령을 사용 합니다.

```
Get-AzureRMProviderOperation "Microsoft.Compute/virtualMachines/*" | FT OperationName, Operation , Description -AutoSize
```

### <a name="create-role-with-psroledefinitionobject"></a>PSRoleDefinitionObject를 사용하여 역할 만들기
PowerShell toocreate 사용자 지정 역할을 사용 하는 경우에 처음부터 다시 시작 하거나 hello 중 하나를 사용할 수 있습니다 [기본 제공 역할](role-based-access-built-in-roles.md) 시작 지점으로 합니다. 기본 제공 역할으로 시작 하 고 많은 권한을 가진 사용자 지정 하는이 섹션의 hello 예제입니다. Hello 특성 tooadd hello 편집 *동작*, *notActions*, 또는 *범위* 하 고 새 역할로 hello 변경 내용을 저장 합니다.

hello 다음 예제에서는 시작 hello로 *가상 컴퓨터 참가자* 역할 및 사용 하 여 사용자 지정 역할 해당 toocreate 호출 *가상 컴퓨터 연산자*합니다. 새 역할 hello 액세스 tooall 읽기 작업의 부여 *Microsoft.Compute*, *Microsoft.Storage*, 및 *Microsoft.Network* 리소스 공급자 및 부여 액세스 toostart, 다시 시작 하 고 가상 컴퓨터를 모니터링 합니다. 사용자 지정 역할 hello 두 구독에 사용할 수 있습니다.

```
$role = Get-AzureRmRoleDefinition "Virtual Machine Contributor"
$role.Id = $null
$role.Name = "Virtual Machine Operator"
$role.Description = "Can monitor and restart virtual machines."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Storage/*/read")
$role.Actions.Add("Microsoft.Network/*/read")
$role.Actions.Add("Microsoft.Compute/*/read")
$role.Actions.Add("Microsoft.Compute/virtualMachines/start/action")
$role.Actions.Add("Microsoft.Compute/virtualMachines/restart/action")
$role.Actions.Add("Microsoft.Authorization/*/read")
$role.Actions.Add("Microsoft.Resources/subscriptions/resourceGroups/read")
$role.Actions.Add("Microsoft.Insights/alertRules/*")
$role.Actions.Add("Microsoft.Support/*")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e")
$role.AssignableScopes.Add("/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624")
New-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Get-AzureRmRoleDefinition - 스크린샷](./media/role-based-access-control-manage-access-powershell/2-new-azurermroledefinition.png)

### <a name="create-role-with-json-template"></a>JSON 템플릿을 사용하여 역할 만들기
JSON 템플릿은 hello 사용자 지정 역할에 대 한 hello 원본 정의로 사용할 수 있습니다. hello 다음 예제에서는 toostorage 읽기 액세스를 허용 하 고 계산 리소스, toosupport, 액세스 및 해당 역할을 추가 하는 사용자 지정 역할 tootwo 구독 합니다. 새 파일을 만들 `C:\CustomRoles\customrole1.json` 다음 예제는 hello로 합니다. hello Id를 설정 해야 너무`null` 새 ID로 초기 역할 만들기에 자동으로 생성 됩니다. 

```
{
  "Name": "Custom Role 1",
  "Id": null,
  "IsCustom": true,
  "Description": "Allows for read access tooAzure storage and compute resources and access toosupport",
  "Actions": [
    "Microsoft.Compute/*/read",
    "Microsoft.Storage/*/read",
    "Microsoft.Support/*"
  ],
  "NotActions": [
  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624"
  ]
}
```
tooadd hello 역할 toohello 구독을 hello 다음 PowerShell 명령을 실행 합니다.
```
New-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="modify-a-custom-role"></a>사용자 지정 역할 수정
비슷한 toocreating 사용자 지정 역할을 PSRoleDefinitionObject hello 또는 JSON 템플릿을 사용 하 여 기존 사용자 지정 역할을 수정할 수 있습니다.

### <a name="modify-role-with-psroledefinitionobject"></a>PSRoleDefinitionObject를 사용하여 역할 수정
먼저, 사용 하 여 hello toomodify 사용자 지정 역할 `Get-AzureRmRoleDefinition` 명령 tooretrieve hello 역할 정의 합니다. 둘째, 변경 필요한 hello toohello 역할 정의 합니다. 마지막으로 hello를 사용 하 여 `Set-AzureRmRoleDefinition` 명령 toosave hello 역할 정의 수정 합니다.

hello 다음 예제에서는 추가 hello `Microsoft.Insights/diagnosticSettings/*` 작업 toohello *가상 컴퓨터 연산자* 사용자 지정 역할입니다.

```
$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.Actions.Add("Microsoft.Insights/diagnosticSettings/*")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Set-AzureRmRoleDefinition - 스크린샷](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-1.png)

hello 다음 예제에서는 추가의 hello는 Azure 구독 toohello 할당 가능한 범위 *가상 컴퓨터 연산자* 사용자 지정 역할입니다.

```
Get-AzureRmSubscription - SubscriptionName Production3

$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.AssignableScopes.Add("/subscriptions/34370e90-ac4a-4bf9-821f-85eeedead1a2")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Set-AzureRmRoleDefinition - 스크린샷](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-2.png)

### <a name="modify-role-with-json-template"></a>JSON 템플릿을 사용하여 역할 수정
Hello 이전 JSON 템플릿을 사용 하는 기존 사용자 지정 역할 tooadd 수정 또는 제거 작업을 쉽게 있습니다. Hello JSON 템플릿을 업데이트 하 고 hello 다음 예제와 같이 hello 네트워킹에 대 한 읽기 작업을 추가 합니다. hello 서식 파일에 나열 하는 hello 정의 누적 적용 된 tooan 기존 정의 의미 hello 서식 파일에서 지정한 대로 정확 하 게 해당 hello 역할이 표시 되지 않습니다. Hello 역할의 hello ID 인 tooupdate hello Id 필드를 해야합니다. Hello 모를 경우이 값은 무엇을 사용할 수 있습니다 `Get-AzureRmRoleDefinition` cmdlet tooget이이 정보입니다.

```
{
  "Name": "Custom Role 1",
  "Id": "acce7ded-2559-449d-bcd5-e9604e50bad1",
  "IsCustom": true,
  "Description": "Allows for read access tooAzure storage and compute resources and access toosupport",
  "Actions": [
    "Microsoft.Compute/*/read",
    "Microsoft.Storage/*/read",
    "Microsoft.Network/*/read",
    "Microsoft.Support/*"
  ],
  "NotActions": [
  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624"
  ]
}
```

tooupdate hello 기존 역할을 hello 다음 PowerShell 명령을 실행 합니다.
```
Set-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="delete-a-custom-role"></a>사용자 지정 역할 삭제
사용자 지정 역할 toodelete hello를 사용 하 여 `Remove-AzureRmRoleDefinition` 명령입니다.

hello 다음 예제에서는 제거 hello *가상 컴퓨터 연산자* 사용자 지정 역할입니다.

```
Get-AzureRmRoleDefinition "Virtual Machine Operator"

Get-AzureRmRoleDefinition "Virtual Machine Operator" | Remove-AzureRmRoleDefinition
```

![RBAC PowerShell - Remove-AzureRmRoleDefinition - 스크린샷](./media/role-based-access-control-manage-access-powershell/4-remove-azurermroledefinition.png)

## <a name="list-custom-roles"></a>사용자 지정 역할 나열
toolist hello 역할 할당에 범위를 사용할 수 있는 hello를 사용 하 여 `Get-AzureRmRoleDefinition` 명령입니다.

다음 예에서는 hello hello 선택한 구독에 할당에 사용할 수 있는 모든 역할을 나열 합니다.

```
Get-AzureRmRoleDefinition | FT Name, IsCustom
```

![RBAC PowerShell - Get-AzureRmRoleDefinition - 스크린샷](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition-1.png)

다음 예제는 hello에서 hello *가상 컴퓨터 연산자* 사용자 지정 역할 hello에서는 사용할 수 없습니다. *Production4* 구독 hello에서 해당 구독에  **AssignableScopes** hello 역할의 합니다.

![RBAC PowerShell - Get-AzureRmRoleDefinition - 스크린샷](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition2.png)

## <a name="see-also"></a>참고 항목
* [Azure Resource Manager로 Azure PowerShell 사용](../powershell-azure-resource-manager.md)
  [!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]

