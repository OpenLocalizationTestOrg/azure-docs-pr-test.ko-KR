---
title: "Azure RBAC에 대한 사용자 지정 역할 만들기 | Microsoft Docs"
description: "Azure 구독에 보다 정확한 ID 관리를 위해 Azure 역할 기반 액세스 제어로 사용자 지정 역할을 정의하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 8e72f2c8095d13c4b6df3c6576bd58806a3c0f2f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-custom-roles-for-azure-role-based-access-control"></a><span data-ttu-id="ade73-103">Azure 역할 기반 액세스 제어의 사용자 지정 역할 만들기</span><span class="sxs-lookup"><span data-stu-id="ade73-103">Create custom roles for Azure Role-Based Access Control</span></span>
<span data-ttu-id="ade73-104">특정 액세스 요구를 충족하는 기본 제공 역할이 없는 경우 Azure 역할 기반 액세스 제어(RBAC)에서 사용자 지정 역할을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ade73-104">Create a custom role in Azure Role-Based Access Control (RBAC) if none of the built-in roles meet your specific access needs.</span></span> <span data-ttu-id="ade73-105">[Azure PowerShell](role-based-access-control-manage-access-powershell.md), [Azure 명령줄 인터페이스](role-based-access-control-manage-access-azure-cli.md)(CLI) 및 [REST API](role-based-access-control-manage-access-rest.md)를 사용하여 사용자 지정 역할을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ade73-105">Custom roles can be created using [Azure PowerShell](role-based-access-control-manage-access-powershell.md), [Azure Command-Line Interface](role-based-access-control-manage-access-azure-cli.md) (CLI), and the [REST API](role-based-access-control-manage-access-rest.md).</span></span> <span data-ttu-id="ade73-106">기본 제공 역할과 마찬가지로 사용자 지정 역할을 사용자, 그룹 및 응용 프로그램에 구독, 리소스 그룹 및 리소스 범위에서 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ade73-106">Just like built-in roles, you can assign custom roles to users, groups, and applications at subscription, resource group, and resource scopes.</span></span> <span data-ttu-id="ade73-107">사용자 지정 역할은 Azure AD 테넌트에 저장되고 구독에서 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ade73-107">Custom roles are stored in an Azure AD tenant and can be shared across subscriptions.</span></span>

<span data-ttu-id="ade73-108">각 테넌트는 최대 2000개의 사용자 지정 역할을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ade73-108">Each tenant can create up to 2000 custom roles.</span></span> 

<span data-ttu-id="ade73-109">다음은 가상 컴퓨터의 모니터링 및 재시작을 위한 사용자 지정 역할에 관한 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="ade73-109">The following example shows a custom role for monitoring and restarting virtual machines:</span></span>

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
## <a name="actions"></a><span data-ttu-id="ade73-110">작업</span><span class="sxs-lookup"><span data-stu-id="ade73-110">Actions</span></span>
<span data-ttu-id="ade73-111">사용자 지정 역할의 **Actions** 속성은 해당 역할에 액세스 권한이 부여되는 Azure 작업을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ade73-111">The **Actions** property of a custom role specifies the Azure operations to which the role grants access.</span></span> <span data-ttu-id="ade73-112">Azure 리소스 공급자의 보안 개체 작업을 식별하는 작업 문자열 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="ade73-112">It is a collection of operation strings that identify securable operations of Azure resource providers.</span></span> <span data-ttu-id="ade73-113">작업 문자열은 `Microsoft.<ProviderName>/<ChildResourceType>/<action>` 형식을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="ade73-113">Operation strings follow the format of `Microsoft.<ProviderName>/<ChildResourceType>/<action>`.</span></span> <span data-ttu-id="ade73-114">와일드카드(\*)를 포함하는 작업 문자열은 작업 문자열과 일치하는 모든 작업에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="ade73-114">Operation strings that contain wildcards (\*) grant access to all operations that match the operation string.</span></span> <span data-ttu-id="ade73-115">예:</span><span class="sxs-lookup"><span data-stu-id="ade73-115">For instance:</span></span>

* <span data-ttu-id="ade73-116">`*/read` 는 모든 Azure 리소스 공급자의 모든 리소스 종류에 대한 읽기 작업의 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="ade73-116">`*/read` grants access to read operations for all resource types of all Azure resource providers.</span></span>
* <span data-ttu-id="ade73-117">`Microsoft.Compute/*`는 Microsoft.Compute 리소스 공급자에 있는 모든 리소스 종류의 모든 작업에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="ade73-117">`Microsoft.Compute/*` grants access to all operations for all resource types in the Microsoft.Compute resource provider.</span></span>
* <span data-ttu-id="ade73-118">`Microsoft.Network/*/read` 는 Azure의 Microsoft.Network 리소스 공급자에서 모든 리소스 종류에 대한 읽기 작업의 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="ade73-118">`Microsoft.Network/*/read` grants access to read operations for all resource types in the Microsoft.Network resource provider of Azure.</span></span>
* <span data-ttu-id="ade73-119">`Microsoft.Compute/virtualMachines/*` 는 가상 컴퓨터 및 해당 하위 리소스 종류의 모든 작업에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="ade73-119">`Microsoft.Compute/virtualMachines/*` grants access to all operations of virtual machines and its child resource types.</span></span>
* <span data-ttu-id="ade73-120">`Microsoft.Web/sites/restart/Action`은 웹 사이트를 다시 시작하기 위한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="ade73-120">`Microsoft.Web/sites/restart/Action` grants access to restart websites.</span></span>

<span data-ttu-id="ade73-121">`Get-AzureRmProviderOperation`(PowerShell) 또는 `azure provider operations show`(Azure CLI)를 사용하여 Azure 리소스 공급자에 대한 작업을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="ade73-121">Use `Get-AzureRmProviderOperation` (in PowerShell) or `azure provider operations show` (in Azure CLI) to list operations of Azure resource providers.</span></span> <span data-ttu-id="ade73-122">이러한 명령을 사용하여 작업 문자열이 올바른지 확인하고 와일드카드 작업 문자열을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ade73-122">You may also use these commands to verify that an operation string is valid, and to expand wildcard operation strings.</span></span>

```
Get-AzureRMProviderOperation Microsoft.Compute/virtualMachines/*/action | FT Operation, OperationName

Get-AzureRMProviderOperation Microsoft.Network/*
```

![PowerShell 스크린샷 - Get-AzureRMProviderOperation](./media/role-based-access-control-configure/1-get-azurermprovideroperation-1.png)

```
azure provider operations show "Microsoft.Compute/virtualMachines/*/action" --js on | jq '.[] | .operation'

azure provider operations show "Microsoft.Network/*"
```

![<span data-ttu-id="ade73-124">Azure CLI 스크린샷 - azure 공급자 작업 표시 "Microsoft.Compute/virtualMachines/\*/action"</span><span class="sxs-lookup"><span data-stu-id="ade73-124">Azure CLI screenshot - azure provider operations show "Microsoft.Compute/virtualMachines/\*/action"</span></span> ](./media/role-based-access-control-configure/1-azure-provider-operations-show.png)

## <a name="notactions"></a><span data-ttu-id="ade73-125">NotActions</span><span class="sxs-lookup"><span data-stu-id="ade73-125">NotActions</span></span>
<span data-ttu-id="ade73-126">허용하려는 작업 집합을 제한된 작업을 제외하여 보다 쉽게 정의하는 경우 **NotActions** 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ade73-126">Use the **NotActions** property if the set of operations that you wish to allow is more easily defined by excluding restricted operations.</span></span> <span data-ttu-id="ade73-127">사용자 지정 역할로 부여되는 액세스 권한은 **Actions** 작업에서 **NotActions** 작업을 빼서 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="ade73-127">The access granted by a custom role is computed by subtracting the **NotActions** operations from the **Actions** operations.</span></span>

> [!NOTE]
> <span data-ttu-id="ade73-128">사용자에게 **NotActions**에서 작업을 제외하는 역할이 할당되고 동일한 작업에 대한 액세스 권한을 부여하는 두 번째 역할이 할당된 경우 사용자는 해당 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ade73-128">If a user is assigned a role that excludes an operation in **NotActions**, and is assigned a second role that grants access to the same operation, the user is allowed to perform that operation.</span></span> <span data-ttu-id="ade73-129">**NotActions** 는 거부 규칙이 아니며 특정 작업을 제외해야 할 경우 허용된 작업 집합을 만드는 편리한 방법일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="ade73-129">**NotActions** is not a deny rule – it is simply a convenient way to create a set of allowed operations when specific operations need to be excluded.</span></span>
>
>

## <a name="assignablescopes"></a><span data-ttu-id="ade73-130">AssignableScopes</span><span class="sxs-lookup"><span data-stu-id="ade73-130">AssignableScopes</span></span>
<span data-ttu-id="ade73-131">사용자 지정 역할의 **AssignableScopes** 속성은 사용자 지정 역할을 할당할 수 있는 범위(구독, 리소스 그룹 또는 리소스)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ade73-131">The **AssignableScopes** property of the custom role specifies the scopes (subscriptions, resource groups, or resources) within which the custom role is available for assignment.</span></span> <span data-ttu-id="ade73-132">역할이 필요한 구독 또는 리소스 그룹에만 사용자 지정 역할을 할당할 수 있도록 하고 그 외의 구독 또는 리소스 그룹에 대해서는 사용자 환경을 보다 깔끔하게 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ade73-132">You can make the custom role available for assignment in only the subscriptions or resource groups that require it, and not clutter user experience for the rest of the subscriptions or resource groups.</span></span>

<span data-ttu-id="ade73-133">유효한 할당 가능한 범위의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ade73-133">Examples of valid assignable scopes include:</span></span>

* <span data-ttu-id="ade73-134">"/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e", "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624" - 두 개의 구독에 역할을 할당할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ade73-134">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e”, “/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624” - makes the role available for assignment in two subscriptions.</span></span>
* <span data-ttu-id="ade73-135">"/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e" - 단일 구독에 역할을 할당할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ade73-135">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e” - makes the role available for assignment in a single subscription.</span></span>
* <span data-ttu-id="ade73-136">"/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network" - 네트워크 리소스 그룹에만 역할을 할당할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ade73-136">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network” - makes the role available for assignment only in the Network resource group.</span></span>

> [!NOTE]
> <span data-ttu-id="ade73-137">구독, 리소스 그룹 또는 리소스 ID를 적어도 하나 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ade73-137">You must use at least one subscription, resource group, or resource ID.</span></span>
>
>

## <a name="custom-roles-access-control"></a><span data-ttu-id="ade73-138">사용자 지정 역할 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="ade73-138">Custom roles access control</span></span>
<span data-ttu-id="ade73-139">사용자 지정 역할의 **AssignableScopes** 속성으로 해당 역할을 보고 수정하며 삭제할 수 있는 사용자를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="ade73-139">The **AssignableScopes** property of the custom role also controls who can view, modify, and delete the role.</span></span>

* <span data-ttu-id="ade73-140">사용자 지정 역할을 만들 수 있는 사람</span><span class="sxs-lookup"><span data-stu-id="ade73-140">Who can create a custom role?</span></span>
    <span data-ttu-id="ade73-141">구독, 리소스 그룹 및 리소스의 소유자(및 사용자 액세스 관리자)는 해당 범위에 사용할 사용자 지정 역할을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ade73-141">Owners (and User Access Administrators) of subscriptions, resource groups, and resources can create custom roles for use in those scopes.</span></span>
    <span data-ttu-id="ade73-142">역할을 만드는 사용자는 역할의 모든 **AssignableScopes**에서 `Microsoft.Authorization/roleDefinition/write` 작업을 수행할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ade73-142">The user creating the role needs to be able to perform `Microsoft.Authorization/roleDefinition/write` operation on all the **AssignableScopes** of the role.</span></span>
* <span data-ttu-id="ade73-143">사용자 지정 역할을 수정할 수 있는 사람</span><span class="sxs-lookup"><span data-stu-id="ade73-143">Who can modify a custom role?</span></span>
    <span data-ttu-id="ade73-144">구독, 리소스 그룹 및 리소스의 소유자(및 사용자 액세스 관리자)는 해당 범위에 사용자 지정 역할을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ade73-144">Owners (and User Access Administrators) of subscriptions, resource groups, and resources can modify custom roles in those scopes.</span></span> <span data-ttu-id="ade73-145">사용자는 사용자 지정 역할의 모든 **AssignableScopes**에서 `Microsoft.Authorization/roleDefinition/write` 작업을 수행해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ade73-145">Users need to be able to perform the `Microsoft.Authorization/roleDefinition/write` operation on all the **AssignableScopes** of a custom role.</span></span>
* <span data-ttu-id="ade73-146">사용자 지정 역할을 볼 수 있는 사용자는 누구인가요?</span><span class="sxs-lookup"><span data-stu-id="ade73-146">Who can view custom roles?</span></span>
    <span data-ttu-id="ade73-147">Azure RBAC에서 모든 기본 제공 역할은 할당 가능한 역할을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ade73-147">All built-in roles in Azure RBAC allow viewing of roles that are available for assignment.</span></span> <span data-ttu-id="ade73-148">범위에서 `Microsoft.Authorization/roleDefinition/read` 작업을 수행할 수 있는 사용자는 해당 범위에서 할당 가능한 RBAC 역할을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ade73-148">Users who can perform the `Microsoft.Authorization/roleDefinition/read` operation at a scope can view the RBAC roles that are available for assignment at that scope.</span></span>

## <a name="see-also"></a><span data-ttu-id="ade73-149">참고 항목</span><span class="sxs-lookup"><span data-stu-id="ade73-149">See also</span></span>
* <span data-ttu-id="ade73-150">[역할 기반 액세스 제어](role-based-access-control-configure.md): Azure 포털에서 RBAC를 통해 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ade73-150">[Role Based Access Control](role-based-access-control-configure.md): Get started with RBAC in the Azure portal.</span></span>
* <span data-ttu-id="ade73-151">다음을 사용하여 액세스를 관리하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ade73-151">Learn how to manage access with:</span></span>
  * [<span data-ttu-id="ade73-152">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ade73-152">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
  * [<span data-ttu-id="ade73-153">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ade73-153">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
  * [<span data-ttu-id="ade73-154">REST API</span><span class="sxs-lookup"><span data-stu-id="ade73-154">REST API</span></span>](role-based-access-control-manage-access-rest.md)
* <span data-ttu-id="ade73-155">[기본 제공 역할](role-based-access-built-in-roles.md): RBAC에서 표준이 되는 역할에 대한 세부 정보를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="ade73-155">[Built-in roles](role-based-access-built-in-roles.md): Get details about the roles that come standard in RBAC.</span></span>
