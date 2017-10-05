---
title: "Azure PowerShell을 사용하여 RBAC(역할 기반 액세스 제어) 관리 | Microsoft Docs"
description: "Azure PowerShell에서 역할을 나열하고, 역할을 할당하고, 역할 할당을 제거하는 등 RBAC를 관리하는 방법입니다."
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
ms.openlocfilehash: d7b11df21650b5cb27f9c3dd8306f8d12664185e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-role-based-access-control-with-azure-powershell"></a><span data-ttu-id="16940-103">Azure PowerShell을 사용하여 역할 기반 액세스 제어 관리</span><span class="sxs-lookup"><span data-stu-id="16940-103">Manage Role-Based Access Control with Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="16940-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="16940-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="16940-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="16940-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="16940-106">REST API</span><span class="sxs-lookup"><span data-stu-id="16940-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)

<span data-ttu-id="16940-107">Azure 포털의 RBAC(역할 기반 액세스 제어) 및 Azure 리소스 관리 API를 사용하여 세밀한 수준에서 구독에 대한 액세스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16940-107">You can use Role-Based Access Control (RBAC) in the Azure portal and Azure Resource Management API to manage access to your subscription at a fine-grained level.</span></span> <span data-ttu-id="16940-108">이 기능을 통해 특정 범위에서 Active Directory 사용자, 그룹 또는 서비스 사용자에게 일부 역할을 할당하여 액세스 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16940-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles to them at a particular scope.</span></span>

<span data-ttu-id="16940-109">PowerShell을 사용하여 RBAC를 관리하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="16940-109">Before you can use PowerShell to manage RBAC, you need the following prerequisites:</span></span>

* <span data-ttu-id="16940-110">Azure PowerShell 버전 0.8.8 이상.</span><span class="sxs-lookup"><span data-stu-id="16940-110">Azure PowerShell version 0.8.8 or later.</span></span> <span data-ttu-id="16940-111">최신 버전을 설치하고 Azure 구독에 연결하려면 [Azure PowerShell 설치 및 구성하는 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16940-111">To install the latest version and associate it with your Azure subscription, see [how to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="16940-112">Azure Resource Manager cmdlet.</span><span class="sxs-lookup"><span data-stu-id="16940-112">Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="16940-113">PowerShell에서 [Azure Resource Manager cmdlet](/powershell/azure/overview) 을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="16940-113">Install the [Azure Resource Manager cmdlets](/powershell/azure/overview) in PowerShell.</span></span>

## <a name="list-roles"></a><span data-ttu-id="16940-114">역할 나열</span><span class="sxs-lookup"><span data-stu-id="16940-114">List roles</span></span>
### <a name="list-all-available-roles"></a><span data-ttu-id="16940-115">사용 가능한 모든 역할 나열</span><span class="sxs-lookup"><span data-stu-id="16940-115">List all available roles</span></span>
<span data-ttu-id="16940-116">할당할 수 있는 RBAC 역할을 나열하고 액세스 권한을 부여하는 작업을 검사하려면 `Get-AzureRmRoleDefinition`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="16940-116">To list RBAC roles that are available for assignment and to inspect the operations to which they grant access, use `Get-AzureRmRoleDefinition`.</span></span>

```
Get-AzureRmRoleDefinition | FT Name, Description
```

![RBAC PowerShell - Get-AzureRmRoleDefinition - 스크린샷](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition1.png)

### <a name="list-actions-of-a-role"></a><span data-ttu-id="16940-118">역할의 작업 나열</span><span class="sxs-lookup"><span data-stu-id="16940-118">List actions of a role</span></span>
<span data-ttu-id="16940-119">특정 역할을 작업을 나열하려면 `Get-AzureRmRoleDefinition <role name>`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="16940-119">To list the actions for a specific role, use `Get-AzureRmRoleDefinition <role name>`.</span></span>

```
Get-AzureRmRoleDefinition Contributor | FL Actions, NotActions

(Get-AzureRmRoleDefinition "Virtual Machine Contributor").Actions
```

![RBAC PowerShell - 특정 역할에 대한 Get-AzureRmRoleDefinition - 스크린샷](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition2.png)

## <a name="see-who-has-access"></a><span data-ttu-id="16940-121">액세스 권한이 있는 사용자 확인</span><span class="sxs-lookup"><span data-stu-id="16940-121">See who has access</span></span>
<span data-ttu-id="16940-122">RBAC 액세스 할당을 나열하려면 `Get-AzureRmRoleAssignment`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="16940-122">To list RBAC access assignments, use `Get-AzureRmRoleAssignment`.</span></span>

### <a name="list-role-assignments-at-a-specific-scope"></a><span data-ttu-id="16940-123">특정 범위의 역할 할당 나열</span><span class="sxs-lookup"><span data-stu-id="16940-123">List role assignments at a specific scope</span></span>
<span data-ttu-id="16940-124">지정된 구독, 리소스 그룹 또는 리소스에 대한 모든 액세스 할당을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16940-124">You can see all the access assignments for a specified subscription, resource group, or resource.</span></span> <span data-ttu-id="16940-125">예를 들어 리소스 그룹에 대한 모든 활성 할당을 확인하려면 `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="16940-125">For example, to see the all the active assignments for a resource group, use `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`.</span></span>

```
Get-AzureRmRoleAssignment -ResourceGroupName Pharma-Sales-ProjectForcast | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell - 리소스 그룹에 대한 Get-AzureRmRoleAssignment - 스크린샷](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment1.png)

### <a name="list-roles-assigned-to-a-user"></a><span data-ttu-id="16940-127">사용자에게 할당된 역할 나열</span><span class="sxs-lookup"><span data-stu-id="16940-127">List roles assigned to a user</span></span>
<span data-ttu-id="16940-128">지정된 사용자에게 할당된 역할 및 사용자가 속한 그룹에 할당된 역할을 모두 나열하려면 `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="16940-128">To list all the roles that are assigned to a specified user and the roles that are assigned to the groups to which the user belongs, use `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`.</span></span>

```
Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com | FL DisplayName, RoleDefinitionName, Scope

Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com -ExpandPrincipalGroups | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell - 사용자에 대한 Get-AzureRmRoleAssignment - 스크린샷](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment2.png)

### <a name="list-classic-service-administrator-and-coadmin-role-assignments"></a><span data-ttu-id="16940-130">클래식 서비스 관리자 및 공동 관리자 역할 할당 나열</span><span class="sxs-lookup"><span data-stu-id="16940-130">List classic service administrator and coadmin role assignments</span></span>
<span data-ttu-id="16940-131">클래식 구독 관리자 및 공동 관리자에 대한 액세스 할당을 나열하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="16940-131">To list access assignments for the classic subscription administrator and coadministrators, use:</span></span>

    Get-AzureRmRoleAssignment -IncludeClassicAdministrators

## <a name="grant-access"></a><span data-ttu-id="16940-132">액세스 권한 부여</span><span class="sxs-lookup"><span data-stu-id="16940-132">Grant access</span></span>
### <a name="search-for-object-ids"></a><span data-ttu-id="16940-133">개체 ID 검색</span><span class="sxs-lookup"><span data-stu-id="16940-133">Search for object IDs</span></span>
<span data-ttu-id="16940-134">역할을 할당하려면 개체(사용자, 그룹 또는 응용 프로그램)와 범위 둘 다를 식별해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16940-134">To assign a role, you need to identify both the object (user, group, or application) and the scope.</span></span>

<span data-ttu-id="16940-135">구독 ID를 모르는 경우 Azure 포털의 **구독** 블레이드에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16940-135">If you don't know the subscription ID, you can find it in the **Subscriptions** blade on the Azure portal.</span></span> <span data-ttu-id="16940-136">구독 ID를 쿼리하는 방법을 알아보려면 MSDN에서 [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16940-136">To learn how to query for the subscription ID, see [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) on MSDN.</span></span>

<span data-ttu-id="16940-137">Azure AD 그룹에 대한 개체 ID를 가져오려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="16940-137">To get the object ID for an Azure AD group, use:</span></span>

    Get-AzureRmADGroup -SearchString <group name in quotes>

<span data-ttu-id="16940-138">Azure AD 서비스 사용자 또는 응용 프로그램에 대한 개체 ID를 찾으려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="16940-138">To get the object ID for an Azure AD service principal or application, use:</span></span>

    Get-AzureRmADServicePrincipal -SearchString <service name in quotes>

### <a name="assign-a-role-to-an-application-at-the-subscription-scope"></a><span data-ttu-id="16940-139">구독 범위에서 응용 프로그램에 역할 할당</span><span class="sxs-lookup"><span data-stu-id="16940-139">Assign a role to an application at the subscription scope</span></span>
<span data-ttu-id="16940-140">구독 범위에서 응용 프로그램에 액세스 권한을 부여하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="16940-140">To grant access to an application at the subscription scope, use:</span></span>

    New-AzureRmRoleAssignment -ObjectId <application id> -RoleDefinitionName <role name> -Scope <subscription id>

![RBAC PowerShell - New-AzureRmRoleAssignment - 스크린샷](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment2.png)

### <a name="assign-a-role-to-a-user-at-the-resource-group-scope"></a><span data-ttu-id="16940-142">리소스 그룹 범위에서 사용자에 역할 할당</span><span class="sxs-lookup"><span data-stu-id="16940-142">Assign a role to a user at the resource group scope</span></span>
<span data-ttu-id="16940-143">리소스 그룹 범위에서 사용자에 액세스 권한을 부여하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="16940-143">To grant access to a user at the resource group scope, use:</span></span>

    New-AzureRmRoleAssignment -SignInName <email of user> -RoleDefinitionName <role name in quotes> -ResourceGroupName <resource group name>

![RBAC PowerShell - New-AzureRmRoleAssignment - 스크린샷](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment3.png)

### <a name="assign-a-role-to-a-group-at-the-resource-scope"></a><span data-ttu-id="16940-145">리소스 범위에서 그룹에 역할 할당</span><span class="sxs-lookup"><span data-stu-id="16940-145">Assign a role to a group at the resource scope</span></span>
<span data-ttu-id="16940-146">리소스 범위에서 그룹에 액세스 권한을 부여하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="16940-146">To grant access to a group at the resource scope, use:</span></span>

    New-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name in quotes> -ResourceName <resource name> -ResourceType <resource type> -ParentResource <parent resource> -ResourceGroupName <resource group name>

![RBAC PowerShell - New-AzureRmRoleAssignment - 스크린샷](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment4.png)

## <a name="remove-access"></a><span data-ttu-id="16940-148">액세스 권한 제거</span><span class="sxs-lookup"><span data-stu-id="16940-148">Remove access</span></span>
<span data-ttu-id="16940-149">사용자, 그룹 및 응용 프로그램의 액세스 권한을 제거하려면 다음을 사용합니다.:</span><span class="sxs-lookup"><span data-stu-id="16940-149">To remove access for users, groups, and applications, use:</span></span>

    Remove-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name> -Scope <scope such as subscription id>

![RBAC PowerShell - Remove-AzureRmRoleAssignment - 스크린샷](./media/role-based-access-control-manage-access-powershell/3-remove-azure-rm-role-assignment.png)

## <a name="create-a-custom-role"></a><span data-ttu-id="16940-151">사용자 지정 역할 만들기</span><span class="sxs-lookup"><span data-stu-id="16940-151">Create a custom role</span></span>
<span data-ttu-id="16940-152">사용자 지정 역할을 만들려면 ```New-AzureRmRoleDefinition``` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="16940-152">To create a custom role, use the ```New-AzureRmRoleDefinition``` command.</span></span> <span data-ttu-id="16940-153">역할을 구조화하는 방법에는 PSRoleDefinitionObject를 사용하거나 JSON 템플릿을 사용하는 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16940-153">There are two methods of structuring the role, using PSRoleDefinitionObject or a JSON template.</span></span> 

## <a name="get-actions-for-a-resource-provider"></a><span data-ttu-id="16940-154">리소스 공급자에 대한 작업 가져오기</span><span class="sxs-lookup"><span data-stu-id="16940-154">Get Actions for a Resource Provider</span></span>
<span data-ttu-id="16940-155">처음부터 사용자 지정 역할을 만드는 경우 리소스 공급자에서 가능한 모든 작업을 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16940-155">When You are creating custom roles from scratch, it is important to know all the possible operations from the resource providers.</span></span>
<span data-ttu-id="16940-156">```Get-AzureRMProviderOperation``` 명령을 사용하여 이 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="16940-156">Use the ```Get-AzureRMProviderOperation``` command to get this information.</span></span>
<span data-ttu-id="16940-157">예를 들어, 가상 컴퓨터에 사용 가능한 모든 작업을 확인하려는 경우 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="16940-157">For example, if you want to check all the available operations for virtual Machine use this command:</span></span>

```
Get-AzureRMProviderOperation "Microsoft.Compute/virtualMachines/*" | FT OperationName, Operation , Description -AutoSize
```

### <a name="create-role-with-psroledefinitionobject"></a><span data-ttu-id="16940-158">PSRoleDefinitionObject를 사용하여 역할 만들기</span><span class="sxs-lookup"><span data-stu-id="16940-158">Create role with PSRoleDefinitionObject</span></span>
<span data-ttu-id="16940-159">PowerShell을 사용하여 사용자 지정 역할을 만들 때는 처음부터 시작하거나 [기본 제공 역할](role-based-access-built-in-roles.md) 중 하나를 출발점으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16940-159">When you use PowerShell to create a custom role, you can start from scratch or use one of the [built-in roles](role-based-access-built-in-roles.md) as a starting point.</span></span> <span data-ttu-id="16940-160">이 섹션의 예제에서는 기본 제공 역할로 시작한 다음 추가 권한으로 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="16940-160">The example in this section starts with a built-in role and then customizes it with more privileges.</span></span> <span data-ttu-id="16940-161">속성을 편집하여 원하는 *Actions*, *notActions* 또는 *scopes*를 추가한 다음 변경 내용을 새 역할로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="16940-161">Edit the attributes to add the *Actions*, *notActions*, or *scopes* that you want, and then save the changes as a new role.</span></span>

<span data-ttu-id="16940-162">다음 예제에서는 *Virtual Machine Contributor* 역할로 시작한 후 이 역할을 사용하여 *Virtual Machine Operator*라는 사용자 지정 역할을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="16940-162">The following example starts with the *Virtual Machine Contributor* role and uses that to create a custom role called *Virtual Machine Operator*.</span></span> <span data-ttu-id="16940-163">새 역할은 *Microsoft.Compute*, *Microsoft.Storage* 및 *Microsoft.Network* 리소스 공급자의 모든 읽기 작업에 대한 액세스 권한을 부여하고 가상 컴퓨터를 시작, 다시 시작 및 모니터링할 수 있는 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="16940-163">The new role grants access to all read operations of *Microsoft.Compute*, *Microsoft.Storage*, and *Microsoft.Network* resource providers and grants access to start, restart, and monitor virtual machines.</span></span> <span data-ttu-id="16940-164">두 구독 모두에서 사용자 지정 역할을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16940-164">The custom role can be used in two subscriptions.</span></span>

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

### <a name="create-role-with-json-template"></a><span data-ttu-id="16940-166">JSON 템플릿을 사용하여 역할 만들기</span><span class="sxs-lookup"><span data-stu-id="16940-166">Create role with JSON template</span></span>
<span data-ttu-id="16940-167">JSON 템플릿을 사용자 지정 역할의 원본 정의로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16940-167">A JSON template can be used as the source definition for the custom role.</span></span> <span data-ttu-id="16940-168">다음 예제에서는 저장소 및 계산 리소스에 대한 읽기 액세스, 지원 액세스를 허용하고 해당 역할을 두 개의 구독에 추가하는 사용자 지정 역할을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="16940-168">The following example creates a custom role that allows read access to storage and compute resources, access to support, and adds that role to two subscriptions.</span></span> <span data-ttu-id="16940-169">다음 예제가 포함된 새 파일 `C:\CustomRoles\customrole1.json`을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="16940-169">Create a new file `C:\CustomRoles\customrole1.json` with the following example.</span></span> <span data-ttu-id="16940-170">초기 역할 생성 시 새 ID가 자동 생성되므로 Id를 `null`로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16940-170">The Id should be set to `null` on initial role creation as a new ID is generated automatically.</span></span> 

```
{
  "Name": "Custom Role 1",
  "Id": null,
  "IsCustom": true,
  "Description": "Allows for read access to Azure storage and compute resources and access to support",
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
<span data-ttu-id="16940-171">구독에 역할을 추가하려면 다음 PowerShell 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="16940-171">To add the role to the subscriptions, run the following PowerShell command:</span></span>
```
New-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="modify-a-custom-role"></a><span data-ttu-id="16940-172">사용자 지정 역할 수정</span><span class="sxs-lookup"><span data-stu-id="16940-172">Modify a custom role</span></span>
<span data-ttu-id="16940-173">사용자 지정 역할을 만들 때와 유사하게 PSRoleDefinitionObject 또는 JSON 템플릿을 사용하여 기존 사용자 지정 역할을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16940-173">Similar to creating a custom role, you can modify an existing custom role using either the PSRoleDefinitionObject or a JSON template.</span></span>

### <a name="modify-role-with-psroledefinitionobject"></a><span data-ttu-id="16940-174">PSRoleDefinitionObject를 사용하여 역할 수정</span><span class="sxs-lookup"><span data-stu-id="16940-174">Modify role with PSRoleDefinitionObject</span></span>
<span data-ttu-id="16940-175">사용자 지정 역할을 수정하려면 먼저 `Get-AzureRmRoleDefinition` 명령을 사용하여 역할 정의를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="16940-175">To modify a custom role, first, use the `Get-AzureRmRoleDefinition` command to retrieve the role definition.</span></span> <span data-ttu-id="16940-176">그런 다음 역할 정의를 원하는 대로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="16940-176">Second, make the desired changes to the role definition.</span></span> <span data-ttu-id="16940-177">마지막으로 `Set-AzureRmRoleDefinition` 명령을 사용하여 수정한 역할 정의를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="16940-177">Finally, use the `Set-AzureRmRoleDefinition` command to save the modified role definition.</span></span>

<span data-ttu-id="16940-178">다음 예제에서는 *Virtual Machine Operator* 사용자 지정 역할에 `Microsoft.Insights/diagnosticSettings/*` 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="16940-178">The following example adds the `Microsoft.Insights/diagnosticSettings/*` operation to the *Virtual Machine Operator* custom role.</span></span>

```
$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.Actions.Add("Microsoft.Insights/diagnosticSettings/*")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Set-AzureRmRoleDefinition - 스크린샷](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-1.png)

<span data-ttu-id="16940-180">다음 예제에서는 *Virtual Machine Operator* 사용자 지정 역할의 할당 가능한 범위에 Azure 구독을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="16940-180">The following example adds an Azure subscription to the assignable scopes of the *Virtual Machine Operator* custom role.</span></span>

```
Get-AzureRmSubscription - SubscriptionName Production3

$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.AssignableScopes.Add("/subscriptions/34370e90-ac4a-4bf9-821f-85eeedead1a2")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Set-AzureRmRoleDefinition - 스크린샷](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-2.png)

### <a name="modify-role-with-json-template"></a><span data-ttu-id="16940-182">JSON 템플릿을 사용하여 역할 수정</span><span class="sxs-lookup"><span data-stu-id="16940-182">Modify role with JSON template</span></span>
<span data-ttu-id="16940-183">이전 JSON 템플릿을 통해 기존 사용자 지정 역할을 손쉽게 수정하여 작업을 추가 또는 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16940-183">Using the previous JSON template, you can easily modify an existing custom role to add or remove Actions.</span></span> <span data-ttu-id="16940-184">다음 예에 표시된 것처럼 JSON 템플릿을 업데이트하고 네트워킹에 대한 읽기 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="16940-184">Update the JSON template and add the read action for networking as shown in the following example.</span></span> <span data-ttu-id="16940-185">템플릿에 나열된 정의는 기존 정의에 점증적으로 적용되지 않습니다. 즉, 템플릿에 지정한 것과 똑같이 역할이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="16940-185">The definitions listed in the template are not cumulatively applied to an existing definition, meaning that the role appears exactly as you specify in the template.</span></span> <span data-ttu-id="16940-186">또한 Id 필드를 역할의 ID로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16940-186">You also need to update the Id field with the ID of the role.</span></span> <span data-ttu-id="16940-187">이 값을 잘 모르는 경우 `Get-AzureRmRoleDefinition` cmdlet을 사용하여 이 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16940-187">If you aren't sure what this value is, you can use the `Get-AzureRmRoleDefinition` cmdlet to get this information.</span></span>

```
{
  "Name": "Custom Role 1",
  "Id": "acce7ded-2559-449d-bcd5-e9604e50bad1",
  "IsCustom": true,
  "Description": "Allows for read access to Azure storage and compute resources and access to support",
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

<span data-ttu-id="16940-188">기존 역할을 업데이트하려면 다음 PowerShell 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="16940-188">To update the existing role, run the following PowerShell command:</span></span>
```
Set-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="delete-a-custom-role"></a><span data-ttu-id="16940-189">사용자 지정 역할 삭제</span><span class="sxs-lookup"><span data-stu-id="16940-189">Delete a custom role</span></span>
<span data-ttu-id="16940-190">사용자 지정 역할을 삭제하려면 `Remove-AzureRmRoleDefinition` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="16940-190">To delete a custom role, use the `Remove-AzureRmRoleDefinition` command.</span></span>

<span data-ttu-id="16940-191">다음 예제에서는 *Virtual Machine Operator* 사용자 지정 역할을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="16940-191">The following example removes the *Virtual Machine Operator* custom role.</span></span>

```
Get-AzureRmRoleDefinition "Virtual Machine Operator"

Get-AzureRmRoleDefinition "Virtual Machine Operator" | Remove-AzureRmRoleDefinition
```

![RBAC PowerShell - Remove-AzureRmRoleDefinition - 스크린샷](./media/role-based-access-control-manage-access-powershell/4-remove-azurermroledefinition.png)

## <a name="list-custom-roles"></a><span data-ttu-id="16940-193">사용자 지정 역할 나열</span><span class="sxs-lookup"><span data-stu-id="16940-193">List custom roles</span></span>
<span data-ttu-id="16940-194">범위에서 할당할 수 있는 역할을 나열하려면 `Get-AzureRmRoleDefinition` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="16940-194">To list the roles that are available for assignment at a scope, use the `Get-AzureRmRoleDefinition` command.</span></span>

<span data-ttu-id="16940-195">다음 예제에서는 선택한 구독에 할당할 수 있는 모든 역할을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="16940-195">The following example lists all roles that are available for assignment in the selected subscription.</span></span>

```
Get-AzureRmRoleDefinition | FT Name, IsCustom
```

![RBAC PowerShell - Get-AzureRmRoleDefinition - 스크린샷](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition-1.png)

<span data-ttu-id="16940-197">다음 예제에서는 *Virtual Machine Operator* 사용자 지정 역할을 *Production4* 구독에서 사용할 수 없습니다. 이 구독이 해당 역할의 **AssignableScopes**에 없기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="16940-197">In the following example, the *Virtual Machine Operator* custom role isn’t available in the *Production4* subscription because that subscription isn’t in the **AssignableScopes** of the role.</span></span>

![RBAC PowerShell - Get-AzureRmRoleDefinition - 스크린샷](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition2.png)

## <a name="see-also"></a><span data-ttu-id="16940-199">참고 항목</span><span class="sxs-lookup"><span data-stu-id="16940-199">See also</span></span>
* <span data-ttu-id="16940-200">[Azure Resource Manager로 Azure PowerShell 사용](../powershell-azure-resource-manager.md)
  [!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]</span><span class="sxs-lookup"><span data-stu-id="16940-200">[Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md)
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]</span></span>

