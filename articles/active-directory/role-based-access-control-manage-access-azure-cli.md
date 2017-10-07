---
title: "역할 기반 액세스 제어 (RBAC)와 Azure CLI aaaManage | Microsoft Docs"
description: "어떻게 toomanage 역할 기반 액세스 제어 (RBAC) hello Azure 명령줄로 인터페이스 목록 역할 및 역할 작업에 알아봅니다 toohello 구독 및 응용 프로그램 범위의 역할에 할당 하 여 합니다."
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
ms.openlocfilehash: 438418e5f6ee9b98908c9c264d516eb722a4e26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control-with-hello-azure-command-line-interface"></a><span data-ttu-id="9c829-103">Azure 명령줄 인터페이스 hello로 역할 기반 액세스 제어 관리</span><span class="sxs-lookup"><span data-stu-id="9c829-103">Manage Role-Based Access Control with hello Azure command-line interface</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9c829-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9c829-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="9c829-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9c829-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="9c829-106">REST API</span><span class="sxs-lookup"><span data-stu-id="9c829-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)


<span data-ttu-id="9c829-107">Hello Azure 포털 및 Azure 리소스 관리자 API toomanage 액세스 tooyour 구독 및 세분화 된 수준에서 리소스에서 역할 기반 액세스 제어 (RBAC)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c829-107">You can use Role-Based Access Control (RBAC) in hello Azure portal and Azure Resource Manager API toomanage access tooyour subscription and resources at a fine-grained level.</span></span> <span data-ttu-id="9c829-108">이 기능을 특정 범위에서 일부 역할 toothem 할당 하 여 Active Directory 사용자, 그룹 또는 서비스 사용자에 대 한 액세스를 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c829-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles toothem at a particular scope.</span></span>

<span data-ttu-id="9c829-109">Hello Azure CLI (명령줄 인터페이스) toomanage RBAC를 사용 하려면 먼저 다음 필수 구성 요소는 hello가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c829-109">Before you can use hello Azure command-line interface (CLI) toomanage RBAC, you must have hello following prerequisites:</span></span>

* <span data-ttu-id="9c829-110">Azure CLI 버전 0.8.8 이상을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="9c829-110">Azure CLI version 0.8.8 or later.</span></span> <span data-ttu-id="9c829-111">Azure 구독으로 참조 tooinstall hello에 대 한 최신 정보 및 연결 [설치 및 구성 hello Azure CLI](../cli-install-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c829-111">tooinstall hello latest version and associate it with your Azure subscription, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="9c829-112">Azure CLI에서 Azure Resource Manager입니다.</span><span class="sxs-lookup"><span data-stu-id="9c829-112">Azure Resource Manager in Azure CLI.</span></span> <span data-ttu-id="9c829-113">너무 이동[hello 리소스 관리자를 사용 하 여 hello Azure CLI](../xplat-cli-azure-resource-manager.md) 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c829-113">Go too[Using hello Azure CLI with hello Resource Manager](../xplat-cli-azure-resource-manager.md) for more details.</span></span>

## <a name="list-roles"></a><span data-ttu-id="9c829-114">역할 나열</span><span class="sxs-lookup"><span data-stu-id="9c829-114">List roles</span></span>
### <a name="list-all-available-roles"></a><span data-ttu-id="9c829-115">사용 가능한 모든 역할 나열</span><span class="sxs-lookup"><span data-stu-id="9c829-115">List all available roles</span></span>
<span data-ttu-id="9c829-116">toolist 모든 사용 가능한 역할을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c829-116">toolist all available roles, use:</span></span>

        azure role list

<span data-ttu-id="9c829-117">hello 다음 예제에서는 hello 목록이 표시 *모든 사용 가능한 역할*합니다.</span><span class="sxs-lookup"><span data-stu-id="9c829-117">hello following example shows hello list of *all available roles*.</span></span>

```
azure role list --json | jq '.[] | {"roleName":.properties.roleName, "description":.properties.description}'
```

![RBAC Azure 명령줄 - azure role list - 스크린샷](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-list.png)

### <a name="list-actions-of-a-role"></a><span data-ttu-id="9c829-119">역할의 작업 나열</span><span class="sxs-lookup"><span data-stu-id="9c829-119">List actions of a role</span></span>
<span data-ttu-id="9c829-120">역할을 사용 하 여 toolist hello 작업의 경우:</span><span class="sxs-lookup"><span data-stu-id="9c829-120">toolist hello actions of a role, use:</span></span>

    azure role show "<role name>"

<span data-ttu-id="9c829-121">hello 다음 예제에서는 작업을 보여 주는 hello의 hello *참가자* 및 *가상 컴퓨터 참가자* 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="9c829-121">hello following example shows hello actions of hello *Contributor* and *Virtual Machine Contributor* roles.</span></span>

```
azure role show "contributor" --json | jq '.[] | {"Actions":.properties.permissions[0].actions,"NotActions":properties.permissions[0].notActions}'

azure role show "virtual machine contributor" --json | jq '.[] | .properties.permissions[0].actions'
```

![RBAC Azure 명령줄 - azure role show - 스크린샷](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-show.png)

## <a name="list-access"></a><span data-ttu-id="9c829-123">액세스 권한 나열</span><span class="sxs-lookup"><span data-stu-id="9c829-123">List access</span></span>
### <a name="list-role-assignments-effective-on-a-resource-group"></a><span data-ttu-id="9c829-124">리소스 그룹에 적용되는 역할 할당 나열</span><span class="sxs-lookup"><span data-stu-id="9c829-124">List role assignments effective on a resource group</span></span>
<span data-ttu-id="9c829-125">사용 하 여 리소스 그룹에 있는 toolist hello 역할 할당:</span><span class="sxs-lookup"><span data-stu-id="9c829-125">toolist hello role assignments that exist in a resource group, use:</span></span>

    azure role assignment list --resource-group <resource group name>

<span data-ttu-id="9c829-126">hello 다음 예제에서는 hello 역할 할당 hello *pharma-sales-projecforcast* 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="9c829-126">hello following example shows hello role assignments in hello *pharma-sales-projecforcast* group.</span></span>

```
azure role assignment list --resource-group pharma-sales-projecforcast --json | jq '.[] | {"DisplayName":.properties.aADObject.displayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![RBAC Azure 명령줄 - 그룹별 azure role assignment list - 스크린샷](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-1.png)

### <a name="list-role-assignments-for-a-user"></a><span data-ttu-id="9c829-128">사용자에 대한 역할 할당 목록</span><span class="sxs-lookup"><span data-stu-id="9c829-128">List role assignments for a user</span></span>
<span data-ttu-id="9c829-129">특정 사용자에 대 한 toolist hello 역할 할당 및 tooa 사용자 그룹을 할당 하는 hello 할당 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c829-129">toolist hello role assignments for a specific user and hello assignments that are assigned tooa user's groups, use:</span></span>

    azure role assignment list --signInName <user email>

<span data-ttu-id="9c829-130">또한 hello 명령을 수정 하 여 그룹에서 상속 되는 역할 할당을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c829-130">You can also see role assignments that are inherited from groups by modifying hello command:</span></span>

    azure role assignment list --expandPrincipalGroups --signInName <user email>

<span data-ttu-id="9c829-131">hello 다음 보여 주는 예제 toohello 부여 된 hello 역할 할당  *sameert@aaddemo.com*  사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="9c829-131">hello following example shows hello role assignments that are granted toohello *sameert@aaddemo.com* user.</span></span> <span data-ttu-id="9c829-132">여기에 그룹에서 상속 된 역할과 toohello 사용자 직접 할당 된 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c829-132">This includes roles that are assigned directly toohello user and roles that are inherited from groups.</span></span>

```
azure role assignment list --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'

azure role assignment list --expandPrincipalGroups --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![RBAC Azure 명령줄 - 사용자별 azure role assignment list - 스크린샷](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-2.png)

## <a name="grant-access"></a><span data-ttu-id="9c829-134">액세스 권한 부여</span><span class="sxs-lookup"><span data-stu-id="9c829-134">Grant access</span></span>
<span data-ttu-id="9c829-135">toogrant 액세스 tooassign hello 역할을 식별 한 후 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="9c829-135">toogrant access after you have identified hello role that you want tooassign, use:</span></span>

    azure role assignment create

### <a name="assign-a-role-toogroup-at-hello-subscription-scope"></a><span data-ttu-id="9c829-136">Hello 구독 범위에서 역할 toogroup 할당</span><span class="sxs-lookup"><span data-stu-id="9c829-136">Assign a role toogroup at hello subscription scope</span></span>
<span data-ttu-id="9c829-137">tooassign hello 구독 범위에서 사용 하 여 역할 tooa 그룹:</span><span class="sxs-lookup"><span data-stu-id="9c829-137">tooassign a role tooa group at hello subscription scope, use:</span></span>

    azure role assignment create --objectId  <group object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

<span data-ttu-id="9c829-138">hello 다음 예제에서는 할당 hello *판독기* 역할 너무*Christine Koch 팀* hello에 *구독* 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="9c829-138">hello following example assigns hello *Reader* role too*Christine Koch's Team* at hello *subscription* scope.</span></span>

![RBAC Azure 명령줄 - 그룹별 azure role assignment create - 스크린샷](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-1.png)

### <a name="assign-a-role-tooan-application-at-hello-subscription-scope"></a><span data-ttu-id="9c829-140">Hello 구독 범위에서 역할 tooan 응용 프로그램 할당</span><span class="sxs-lookup"><span data-stu-id="9c829-140">Assign a role tooan application at hello subscription scope</span></span>
<span data-ttu-id="9c829-141">tooassign hello 구독 범위에서 사용 하 여 역할 tooan 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="9c829-141">tooassign a role tooan application at hello subscription scope, use:</span></span>

    azure role assignment create --objectId  <applications object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

<span data-ttu-id="9c829-142">hello 다음 예제에서는 부여 hello *참가자* 역할 tooan *Azure AD* hello에 대 한 응용 프로그램 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c829-142">hello following example grants hello *Contributor* role tooan *Azure AD* application on hello selected subscription.</span></span>

 ![RBAC Azure 명령줄 - 응용 프로그램별 azure role assignment create - 스크린샷](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-2.png)

### <a name="assign-a-role-tooa-user-at-hello-resource-group-scope"></a><span data-ttu-id="9c829-144">Hello 리소스 그룹 범위에서 역할 tooa 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="9c829-144">Assign a role tooa user at hello resource group scope</span></span>
<span data-ttu-id="9c829-145">tooassign hello 리소스 그룹 범위에서 사용 하 여 역할 tooa 사용자:</span><span class="sxs-lookup"><span data-stu-id="9c829-145">tooassign a role tooa user at hello resource group scope, use:</span></span>

    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>

<span data-ttu-id="9c829-146">hello 다음 예제에서는 부여 hello *가상 컴퓨터 참가자* 역할 너무 *samert@aaddemo.com*  hello에 사용자 *Pharma-Sales-ProjectForcast* 리소스 그룹 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="9c829-146">hello following example grants hello *Virtual Machine Contributor* role too*samert@aaddemo.com* user at hello *Pharma-Sales-ProjectForcast* resource group scope.</span></span>

![RBAC Azure 명령줄 - 사용자별 azure role assignment create - 스크린샷](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-3.png)

### <a name="assign-a-role-tooa-group-at-hello-resource-scope"></a><span data-ttu-id="9c829-148">Hello 리소스 범위에서 역할 tooa 그룹 할당</span><span class="sxs-lookup"><span data-stu-id="9c829-148">Assign a role tooa group at hello resource scope</span></span>
<span data-ttu-id="9c829-149">tooassign hello 리소스 범위에서 사용 하 여 역할 tooa 그룹:</span><span class="sxs-lookup"><span data-stu-id="9c829-149">tooassign a role tooa group at hello resource scope, use:</span></span>

    azure role assignment create --objectId <group id> --role "<name of role>" --resource-name <resource group name> --resource-type <resource group type> --parent <resource group parent> --resource-group <resource group>

<span data-ttu-id="9c829-150">hello 다음 예제에서는 부여 hello *가상 컴퓨터 참가자* 역할 tooan *Azure AD* 그룹에 *서브넷*합니다.</span><span class="sxs-lookup"><span data-stu-id="9c829-150">hello following example grants hello *Virtual Machine Contributor* role tooan *Azure AD* group on a *subnet*.</span></span>

![RBAC Azure 명령줄 - 그룹별 azure role assignment create - 스크린샷](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-4.png)

## <a name="remove-access"></a><span data-ttu-id="9c829-152">액세스 권한 제거</span><span class="sxs-lookup"><span data-stu-id="9c829-152">Remove access</span></span>
<span data-ttu-id="9c829-153">tooremove 역할 할당을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c829-153">tooremove a role assignment, use:</span></span>

    azure role assignment delete --objectId <object id toofrom which tooremove role> --roleName "<role name>"

<span data-ttu-id="9c829-154">hello 다음 예제에서는 제거 hello *가상 컴퓨터 참가자* hello에서 역할 할당  *sammert@aaddemo.com*  hello에 대 한 사용자 *Pharma-Sales-ProjectForcast* 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="9c829-154">hello following example removes hello *Virtual Machine Contributor* role assignment from hello *sammert@aaddemo.com* user on hello *Pharma-Sales-ProjectForcast* resource group.</span></span>
<span data-ttu-id="9c829-155">hello 예제는 다음 hello 구독에 있는 그룹에서 hello 역할 할당을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="9c829-155">hello example then removes hello role assignment from a group on hello subscription.</span></span>

![RBAC Azure 명령줄 - azure role assignment delete - 스크린샷](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-assignment-delete.png)

## <a name="create-a-custom-role"></a><span data-ttu-id="9c829-157">사용자 지정 역할 만들기</span><span class="sxs-lookup"><span data-stu-id="9c829-157">Create a custom role</span></span>
<span data-ttu-id="9c829-158">사용자 지정 역할 toocreate 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c829-158">toocreate a custom role, use:</span></span>

    azure role create --inputfile <file path>

<span data-ttu-id="9c829-159">hello 다음 예제에서는 라는 사용자 지정 역할 *가상 컴퓨터 연산자*합니다.</span><span class="sxs-lookup"><span data-stu-id="9c829-159">hello following example creates a custom role called *Virtual Machine Operator*.</span></span> <span data-ttu-id="9c829-160">이 사용자 지정 역할 액세스 tooall 읽기 작업의 부여 *Microsoft.Compute*, *Microsoft.Storage*, 및 *Microsoft.Network* 리소스 공급자 및 부여 액세스 toostart, 다시 시작 하 고 가상 컴퓨터를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c829-160">This custom role grants access tooall read operations of *Microsoft.Compute*, *Microsoft.Storage*, and *Microsoft.Network* resource providers and grants access toostart, restart, and monitor virtual machines.</span></span> <span data-ttu-id="9c829-161">두 구독 모두에서 사용자 지정 역할을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c829-161">This custom role can be used in two subscriptions.</span></span> <span data-ttu-id="9c829-162">이 예제에서는 입력으로 JSON 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9c829-162">This example uses a JSON file as an input.</span></span>

![JSON - 사용자 지정 역할 정의 - 스크린샷](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-1.png)

![RBAC Azure 명령줄 - azure role create - 스크린샷](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-2.png)

## <a name="modify-a-custom-role"></a><span data-ttu-id="9c829-165">사용자 지정 역할 수정</span><span class="sxs-lookup"><span data-stu-id="9c829-165">Modify a custom role</span></span>
<span data-ttu-id="9c829-166">사용자 지정 역할 toomodify 먼저 사용 하 여 hello `azure role show` 명령 tooretrieve 역할 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c829-166">toomodify a custom role, first use hello `azure role show` command tooretrieve role definition.</span></span> <span data-ttu-id="9c829-167">둘째, hello 원하는 변경 내용을 toohello 역할 정의 파일을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c829-167">Second, make hello desired changes toohello role definition file.</span></span> <span data-ttu-id="9c829-168">마지막으로 사용 하 여 `azure role set` toosave hello 역할 정의 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c829-168">Finally, use `azure role set` toosave hello modified role definition.</span></span>

    azure role set --inputfile <file path>

<span data-ttu-id="9c829-169">hello 다음 예제에서는 추가 hello *Microsoft.Insights/diagnosticSettings/* 작업 toohello **동작**, 및 Azure 구독 toohello **AssignableScopes**hello 가상 컴퓨터 운영자에 대 한 사용자 지정 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c829-169">hello following example adds hello *Microsoft.Insights/diagnosticSettings/* operation toohello **Actions**, and an Azure subscription toohello **AssignableScopes** of hello Virtual Machine Operator custom role.</span></span>

![JSON - 사용자 지정 역할 수정 정의 - 스크린샷](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set-1.png)

![RBAC Azure 명령줄 - azure role set - 스크린샷](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set2.png)

## <a name="delete-a-custom-role"></a><span data-ttu-id="9c829-172">사용자 지정 역할 삭제</span><span class="sxs-lookup"><span data-stu-id="9c829-172">Delete a custom role</span></span>
<span data-ttu-id="9c829-173">사용자 지정 역할 toodelete 먼저 사용 하 여 hello `azure role show` 명령 toodetermine hello **ID** hello 역할의 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c829-173">toodelete a custom role, first use hello `azure role show` command toodetermine hello **ID** of hello role.</span></span> <span data-ttu-id="9c829-174">그런 다음 사용 하는 hello `azure role delete` hello를 지정 하 여 명령 toodelete hello 역할 **ID**합니다.</span><span class="sxs-lookup"><span data-stu-id="9c829-174">Then, use hello `azure role delete` command toodelete hello role by specifying hello **ID**.</span></span>

<span data-ttu-id="9c829-175">hello 다음 예제에서는 제거 hello *가상 컴퓨터 연산자* 사용자 지정 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="9c829-175">hello following example removes hello *Virtual Machine Operator* custom role.</span></span>

![RBAC Azure 명령줄 - azure role delete - 스크린샷](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-delete.png)

## <a name="list-custom-roles"></a><span data-ttu-id="9c829-177">사용자 지정 역할 나열</span><span class="sxs-lookup"><span data-stu-id="9c829-177">List custom roles</span></span>
<span data-ttu-id="9c829-178">toolist hello 역할 할당에 범위를 사용할 수 있는 hello를 사용 하 여 `azure role list` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="9c829-178">toolist hello roles that are available for assignment at a scope, use hello `azure role list` command.</span></span>

<span data-ttu-id="9c829-179">다음 명령을 hello hello 선택한 구독에 할당에 사용할 수 있는 모든 역할을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c829-179">hello following command lists all roles that are available for assignment in hello selected subscription.</span></span>

```
azure role list --json | jq '.[] | {"name":.properties.roleName, type:.properties.type}'
```

![RBAC Azure 명령줄 - azure role list - 스크린샷](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list1.png)

<span data-ttu-id="9c829-181">다음 예제는 hello에서 hello *가상 컴퓨터 연산자* 사용자 지정 역할 hello에서는 사용할 수 없습니다. *Production4* 구독 hello에서 해당 구독에  **AssignableScopes** hello 역할의 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c829-181">In hello following example, hello *Virtual Machine Operator* custom role isn’t available in hello *Production4* subscription because that subscription isn’t in hello **AssignableScopes** of hello role.</span></span>

```
azure role list --json | jq '.[] | if .properties.type == "CustomRole" then .properties.roleName else empty end'
```

![RBAC Azure 명령줄 - 사용자 지정 역할에 대한 azure role list - 스크린샷](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list2.png)

## <a name="next-steps"></a><span data-ttu-id="9c829-183">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9c829-183">Next steps</span></span>
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]

