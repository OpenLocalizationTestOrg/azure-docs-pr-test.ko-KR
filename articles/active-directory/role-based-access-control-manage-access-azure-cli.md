---
title: "Azure CLI를 사용하여 RBAC(역할 기반 액세스 제어) 관리 | Microsoft Docs"
description: "Azure 명령줄 인터페이스에서 역할 및 역할 작업을 나열하고, 구독 및 응용 프로그램 범위에 역할을 할당하여 RBAC(역할 기반 액세스 제어)를 관리하는 방법을 알아봅니다."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 3483ee01-8177-49e7-b337-4d5cb14f5e32
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: ad644de6d23950e699d99042d27381336626caab
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-role-based-access-control-with-the-azure-command-line-interface"></a><span data-ttu-id="696e9-103">Azure 명령줄 인터페이스를 사용하여 역할 기반 액세스 제어 관리</span><span class="sxs-lookup"><span data-stu-id="696e9-103">Manage Role-Based Access Control with the Azure command-line interface</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="696e9-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="696e9-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="696e9-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="696e9-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="696e9-106">REST API</span><span class="sxs-lookup"><span data-stu-id="696e9-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)


<span data-ttu-id="696e9-107">Azure 포털의 RBAC(역할 기반 액세스 제어) 및 Azure Resource Manager API를 사용하여 세밀한 수준에서 구독과 리소스에 대한 액세스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-107">You can use Role-Based Access Control (RBAC) in the Azure portal and Azure Resource Manager API to manage access to your subscription and resources at a fine-grained level.</span></span> <span data-ttu-id="696e9-108">이 기능을 통해 특정 범위에서 Active Directory 사용자, 그룹 또는 서비스 사용자에게 일부 역할을 할당하여 액세스 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles to them at a particular scope.</span></span>

<span data-ttu-id="696e9-109">Azure CLI(명령줄 인터페이스)를 사용하여 RBAC를 관리하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-109">Before you can use the Azure command-line interface (CLI) to manage RBAC, you must have the following prerequisites:</span></span>

* <span data-ttu-id="696e9-110">Azure CLI 버전 0.8.8 이상을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="696e9-110">Azure CLI version 0.8.8 or later.</span></span> <span data-ttu-id="696e9-111">최신 버전을 설치하고 Azure 구독에 연결하려면 [Azure CLI 설치 및 구성 방법](../cli-install-nodejs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="696e9-111">To install the latest version and associate it with your Azure subscription, see [Install and Configure the Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="696e9-112">Azure CLI에서 Azure Resource Manager입니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-112">Azure Resource Manager in Azure CLI.</span></span> <span data-ttu-id="696e9-113">자세한 내용을 보려면 [리소스 관리자에서 Azure CLI 사용](../xplat-cli-azure-resource-manager.md) 으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-113">Go to [Using the Azure CLI with the Resource Manager](../xplat-cli-azure-resource-manager.md) for more details.</span></span>

## <a name="list-roles"></a><span data-ttu-id="696e9-114">역할 나열</span><span class="sxs-lookup"><span data-stu-id="696e9-114">List roles</span></span>
### <a name="list-all-available-roles"></a><span data-ttu-id="696e9-115">사용 가능한 모든 역할 나열</span><span class="sxs-lookup"><span data-stu-id="696e9-115">List all available roles</span></span>
<span data-ttu-id="696e9-116">사용 가능한 역할을 모두 사용하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-116">To list all available roles, use:</span></span>

        azure role list

<span data-ttu-id="696e9-117">다음 예제에서는 *사용 가능한 모든 역할*의 목록을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-117">The following example shows the list of *all available roles*.</span></span>

```
azure role list --json | jq '.[] | {"roleName":.properties.roleName, "description":.properties.description}'
```

![RBAC Azure 명령줄 - azure role list - 스크린샷](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-list.png)

### <a name="list-actions-of-a-role"></a><span data-ttu-id="696e9-119">역할의 작업 나열</span><span class="sxs-lookup"><span data-stu-id="696e9-119">List actions of a role</span></span>
<span data-ttu-id="696e9-120">역할의 작업을 나열하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-120">To list the actions of a role, use:</span></span>

    azure role show "<role name>"

<span data-ttu-id="696e9-121">다음 예제에서는 *참가자* 및 *가상 컴퓨터 참가자* 역할의 작업을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-121">The following example shows the actions of the *Contributor* and *Virtual Machine Contributor* roles.</span></span>

```
azure role show "contributor" --json | jq '.[] | {"Actions":.properties.permissions[0].actions,"NotActions":properties.permissions[0].notActions}'

azure role show "virtual machine contributor" --json | jq '.[] | .properties.permissions[0].actions'
```

![RBAC Azure 명령줄 - azure role show - 스크린샷](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-show.png)

## <a name="list-access"></a><span data-ttu-id="696e9-123">액세스 권한 나열</span><span class="sxs-lookup"><span data-stu-id="696e9-123">List access</span></span>
### <a name="list-role-assignments-effective-on-a-resource-group"></a><span data-ttu-id="696e9-124">리소스 그룹에 적용되는 역할 할당 나열</span><span class="sxs-lookup"><span data-stu-id="696e9-124">List role assignments effective on a resource group</span></span>
<span data-ttu-id="696e9-125">리소스 그룹에 존재하는 역할 할당을 나열하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-125">To list the role assignments that exist in a resource group, use:</span></span>

    azure role assignment list --resource-group <resource group name>

<span data-ttu-id="696e9-126">다음 예제에서는 *pharma-sales-projecforcast* 그룹에 있는 역할 할당을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-126">The following example shows the role assignments in the *pharma-sales-projecforcast* group.</span></span>

```
azure role assignment list --resource-group pharma-sales-projecforcast --json | jq '.[] | {"DisplayName":.properties.aADObject.displayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![RBAC Azure 명령줄 - 그룹별 azure role assignment list - 스크린샷](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-1.png)

### <a name="list-role-assignments-for-a-user"></a><span data-ttu-id="696e9-128">사용자에 대한 역할 할당 목록</span><span class="sxs-lookup"><span data-stu-id="696e9-128">List role assignments for a user</span></span>
<span data-ttu-id="696e9-129">특정 사용자에 대한 역할 할당 및 사용자 그룹에 할당된 할당을 나열하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-129">To list the role assignments for a specific user and the assignments that are assigned to a user's groups, use:</span></span>

    azure role assignment list --signInName <user email>

<span data-ttu-id="696e9-130">또한 명령을 수정하여 그룹에서 상속하는 역할 할당을 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-130">You can also see role assignments that are inherited from groups by modifying the command:</span></span>

    azure role assignment list --expandPrincipalGroups --signInName <user email>

<span data-ttu-id="696e9-131">다음 예제에서는 사용자 *sameert@aaddemo.com* 에 부여된 역할 할당을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-131">The following example shows the role assignments that are granted to the *sameert@aaddemo.com* user.</span></span> <span data-ttu-id="696e9-132">여기에는 사용자에게 직접 할당된 역할 및 그룹에서 상속된 역할이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-132">This includes roles that are assigned directly to the user and roles that are inherited from groups.</span></span>

```
azure role assignment list --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'

azure role assignment list --expandPrincipalGroups --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![RBAC Azure 명령줄 - 사용자별 azure role assignment list - 스크린샷](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-2.png)

## <a name="grant-access"></a><span data-ttu-id="696e9-134">액세스 권한 부여</span><span class="sxs-lookup"><span data-stu-id="696e9-134">Grant access</span></span>
<span data-ttu-id="696e9-135">할당할 역할을 식별한 후 액세스 권한을 부여하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-135">To grant access after you have identified the role that you want to assign, use:</span></span>

    azure role assignment create

### <a name="assign-a-role-to-group-at-the-subscription-scope"></a><span data-ttu-id="696e9-136">구독 범위에서 그룹에 역할 할당</span><span class="sxs-lookup"><span data-stu-id="696e9-136">Assign a role to group at the subscription scope</span></span>
<span data-ttu-id="696e9-137">구독 범위에서 그룹에 역할을 할당하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-137">To assign a role to a group at the subscription scope, use:</span></span>

    azure role assignment create --objectId  <group object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

<span data-ttu-id="696e9-138">다음 예제에서는 *구독* 범위에서 *Christine Koch 팀*에 *독자* 역할을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-138">The following example assigns the *Reader* role to *Christine Koch's Team* at the *subscription* scope.</span></span>

![RBAC Azure 명령줄 - 그룹별 azure role assignment create - 스크린샷](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-1.png)

### <a name="assign-a-role-to-an-application-at-the-subscription-scope"></a><span data-ttu-id="696e9-140">구독 범위에서 응용 프로그램에 역할 할당</span><span class="sxs-lookup"><span data-stu-id="696e9-140">Assign a role to an application at the subscription scope</span></span>
<span data-ttu-id="696e9-141">구독 범위에서 응용 프로그램에 역할을 할당하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-141">To assign a role to an application at the subscription scope, use:</span></span>

    azure role assignment create --objectId  <applications object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

<span data-ttu-id="696e9-142">다음 예제에서는 선택한 구독에서 *Azure AD* 응용 프로그램에 *참가자* 역할을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-142">The following example grants the *Contributor* role to an *Azure AD* application on the selected subscription.</span></span>

 ![RBAC Azure 명령줄 - 응용 프로그램별 azure role assignment create - 스크린샷](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-2.png)

### <a name="assign-a-role-to-a-user-at-the-resource-group-scope"></a><span data-ttu-id="696e9-144">리소스 그룹 범위에서 사용자에 역할 할당</span><span class="sxs-lookup"><span data-stu-id="696e9-144">Assign a role to a user at the resource group scope</span></span>
<span data-ttu-id="696e9-145">리소스 그룹 범위에서 사용자에 역할을 할당하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-145">To assign a role to a user at the resource group scope, use:</span></span>

    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>

<span data-ttu-id="696e9-146">다음 예제에서는 *Pharma-Sales-ProjectForcast* 리소스 그룹 범위에서 사용자 *samert@aaddemo.com*에 *가상 컴퓨터 참가자* 역할을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-146">The following example grants the *Virtual Machine Contributor* role to *samert@aaddemo.com* user at the *Pharma-Sales-ProjectForcast* resource group scope.</span></span>

![RBAC Azure 명령줄 - 사용자별 azure role assignment create - 스크린샷](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-3.png)

### <a name="assign-a-role-to-a-group-at-the-resource-scope"></a><span data-ttu-id="696e9-148">리소스 범위에서 그룹에 역할 할당</span><span class="sxs-lookup"><span data-stu-id="696e9-148">Assign a role to a group at the resource scope</span></span>
<span data-ttu-id="696e9-149">리소스 범위에서 그룹에 역할을 할당하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-149">To assign a role to a group at the resource scope, use:</span></span>

    azure role assignment create --objectId <group id> --role "<name of role>" --resource-name <resource group name> --resource-type <resource group type> --parent <resource group parent> --resource-group <resource group>

<span data-ttu-id="696e9-150">다음 예제에서는 *서브넷*에서 *Azure AD* 그룹에 *가상 컴퓨터 참가자* 역할을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-150">The following example grants the *Virtual Machine Contributor* role to an *Azure AD* group on a *subnet*.</span></span>

![RBAC Azure 명령줄 - 그룹별 azure role assignment create - 스크린샷](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-4.png)

## <a name="remove-access"></a><span data-ttu-id="696e9-152">액세스 권한 제거</span><span class="sxs-lookup"><span data-stu-id="696e9-152">Remove access</span></span>
<span data-ttu-id="696e9-153">역할 할당을 제거하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-153">To remove a role assignment, use:</span></span>

    azure role assignment delete --objectId <object id to from which to remove role> --roleName "<role name>"

<span data-ttu-id="696e9-154">다음 예제에서는 *Pharma-Sales-ProjectForcast* 리소스 그룹의 사용자 *sammert@aaddemo.com*에서 *가상 컴퓨터 참가자* 역할 할당을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-154">The following example removes the *Virtual Machine Contributor* role assignment from the *sammert@aaddemo.com* user on the *Pharma-Sales-ProjectForcast* resource group.</span></span>
<span data-ttu-id="696e9-155">그런 다음 구독의 그룹에서 역할 할당을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-155">The example then removes the role assignment from a group on the subscription.</span></span>

![RBAC Azure 명령줄 - azure role assignment delete - 스크린샷](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-assignment-delete.png)

## <a name="create-a-custom-role"></a><span data-ttu-id="696e9-157">사용자 지정 역할 만들기</span><span class="sxs-lookup"><span data-stu-id="696e9-157">Create a custom role</span></span>
<span data-ttu-id="696e9-158">사용자 지정 역할을 만들려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-158">To create a custom role, use:</span></span>

    azure role create --inputfile <file path>

<span data-ttu-id="696e9-159">다음 예제에서는 *Virtual Machine Operator*라는 사용자 지정 역할을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-159">The following example creates a custom role called *Virtual Machine Operator*.</span></span> <span data-ttu-id="696e9-160">사용자 지정 역할은 *Microsoft.Compute*, *Microsoft.Storage* 및 *Microsoft.Network* 리소스 공급자의 모든 읽기 작업에 대한 액세스 권한을 부여하고 가상 컴퓨터를 시작, 다시 시작 및 모니터링할 수 있는 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-160">This custom role grants access to all read operations of *Microsoft.Compute*, *Microsoft.Storage*, and *Microsoft.Network* resource providers and grants access to start, restart, and monitor virtual machines.</span></span> <span data-ttu-id="696e9-161">두 구독 모두에서 사용자 지정 역할을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-161">This custom role can be used in two subscriptions.</span></span> <span data-ttu-id="696e9-162">이 예제에서는 입력으로 JSON 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-162">This example uses a JSON file as an input.</span></span>

![JSON - 사용자 지정 역할 정의 - 스크린샷](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-1.png)

![RBAC Azure 명령줄 - azure role create - 스크린샷](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-2.png)

## <a name="modify-a-custom-role"></a><span data-ttu-id="696e9-165">사용자 지정 역할 수정</span><span class="sxs-lookup"><span data-stu-id="696e9-165">Modify a custom role</span></span>
<span data-ttu-id="696e9-166">사용자 지정 역할을 수정하려면 먼저 `azure role show` 명령을 사용하여 역할 정의를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-166">To modify a custom role, first use the `azure role show` command to retrieve role definition.</span></span> <span data-ttu-id="696e9-167">그런 다음 역할 정의 파일을 원하는 대로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-167">Second, make the desired changes to the role definition file.</span></span> <span data-ttu-id="696e9-168">마지막으로 `azure role set` 을 사용하여 수정한 역할 정의를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-168">Finally, use `azure role set` to save the modified role definition.</span></span>

    azure role set --inputfile <file path>

<span data-ttu-id="696e9-169">다음 예제에서는 **작업**에 *Microsoft.Insights/diagnosticSettings/* 작업을 추가하고 Virtual Machine Operator 사용자 지정 역할의 **AssignableScopes**에 Azure 구독을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-169">The following example adds the *Microsoft.Insights/diagnosticSettings/* operation to the **Actions**, and an Azure subscription to the **AssignableScopes** of the Virtual Machine Operator custom role.</span></span>

![JSON - 사용자 지정 역할 수정 정의 - 스크린샷](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set-1.png)

![RBAC Azure 명령줄 - azure role set - 스크린샷](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set2.png)

## <a name="delete-a-custom-role"></a><span data-ttu-id="696e9-172">사용자 지정 역할 삭제</span><span class="sxs-lookup"><span data-stu-id="696e9-172">Delete a custom role</span></span>
<span data-ttu-id="696e9-173">사용자 지정 역할을 삭제하려면 먼저 `azure role show` 명령을 사용하여 역할의 **ID** 를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-173">To delete a custom role, first use the `azure role show` command to determine the **ID** of the role.</span></span> <span data-ttu-id="696e9-174">그런 다음 `azure role delete` 명령을 사용하여 **ID**를 지정하여 역할을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-174">Then, use the `azure role delete` command to delete the role by specifying the **ID**.</span></span>

<span data-ttu-id="696e9-175">다음 예제에서는 *Virtual Machine Operator* 사용자 지정 역할을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-175">The following example removes the *Virtual Machine Operator* custom role.</span></span>

![RBAC Azure 명령줄 - azure role delete - 스크린샷](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-delete.png)

## <a name="list-custom-roles"></a><span data-ttu-id="696e9-177">사용자 지정 역할 나열</span><span class="sxs-lookup"><span data-stu-id="696e9-177">List custom roles</span></span>
<span data-ttu-id="696e9-178">범위에서 할당할 수 있는 역할을 나열하려면 `azure role list` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-178">To list the roles that are available for assignment at a scope, use the `azure role list` command.</span></span>

<span data-ttu-id="696e9-179">다음 명령에서는 선택한 구독에 할당할 수 있는 모든 역할을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-179">The following command lists all roles that are available for assignment in the selected subscription.</span></span>

```
azure role list --json | jq '.[] | {"name":.properties.roleName, type:.properties.type}'
```

![RBAC Azure 명령줄 - azure role list - 스크린샷](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list1.png)

<span data-ttu-id="696e9-181">다음 예제에서는 *Virtual Machine Operator* 사용자 지정 역할을 *Production4* 구독에서 사용할 수 없습니다. 이 구독이 해당 역할의 **AssignableScopes**에 없기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="696e9-181">In the following example, the *Virtual Machine Operator* custom role isn’t available in the *Production4* subscription because that subscription isn’t in the **AssignableScopes** of the role.</span></span>

```
azure role list --json | jq '.[] | if .properties.type == "CustomRole" then .properties.roleName else empty end'
```

![RBAC Azure 명령줄 - 사용자 지정 역할에 대한 azure role list - 스크린샷](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list2.png)

## <a name="next-steps"></a><span data-ttu-id="696e9-183">다음 단계</span><span class="sxs-lookup"><span data-stu-id="696e9-183">Next steps</span></span>
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]

