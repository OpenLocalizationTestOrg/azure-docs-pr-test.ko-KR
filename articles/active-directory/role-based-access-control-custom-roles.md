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
# <a name="create-custom-roles-for-azure-role-based-access-control"></a><span data-ttu-id="7c724-103">Azure 역할 기반 액세스 제어의 사용자 지정 역할 만들기</span><span class="sxs-lookup"><span data-stu-id="7c724-103">Create custom roles for Azure Role-Based Access Control</span></span>
<span data-ttu-id="7c724-104">Hello 기본 제공 역할 중 어떤 특정 액세스 요구 사항에 맞지 않을 경우 사용자 지정 역할 신속히 알아봅니다 액세스 제어 (RBAC)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7c724-104">Create a custom role in Azure Role-Based Access Control (RBAC) if none of hello built-in roles meet your specific access needs.</span></span> <span data-ttu-id="7c724-105">사용 하 여 사용자 지정 역할을 만들 수 [Azure PowerShell](role-based-access-control-manage-access-powershell.md), [Azure 명령줄 인터페이스](role-based-access-control-manage-access-azure-cli.md) (CLI) 및 hello [REST API](role-based-access-control-manage-access-rest.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7c724-105">Custom roles can be created using [Azure PowerShell](role-based-access-control-manage-access-powershell.md), [Azure Command-Line Interface](role-based-access-control-manage-access-azure-cli.md) (CLI), and hello [REST API](role-based-access-control-manage-access-rest.md).</span></span> <span data-ttu-id="7c724-106">기본 제공 역할에서와 마찬가지로 사용자 지정 역할 toousers, 그룹 및 구독, 리소스 그룹 및 리소스 범위에서 응용 프로그램을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c724-106">Just like built-in roles, you can assign custom roles toousers, groups, and applications at subscription, resource group, and resource scopes.</span></span> <span data-ttu-id="7c724-107">사용자 지정 역할은 Azure AD 테넌트에 저장되고 구독에서 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c724-107">Custom roles are stored in an Azure AD tenant and can be shared across subscriptions.</span></span>

<span data-ttu-id="7c724-108">각 테 넌 트 too2000 사용자 지정 역할을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c724-108">Each tenant can create up too2000 custom roles.</span></span> 

<span data-ttu-id="7c724-109">hello 다음 예제는 모니터링 및 가상 컴퓨터를 다시 시작을 위한 사용자 지정 역할.</span><span class="sxs-lookup"><span data-stu-id="7c724-109">hello following example shows a custom role for monitoring and restarting virtual machines:</span></span>

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
## <a name="actions"></a><span data-ttu-id="7c724-110">작업</span><span class="sxs-lookup"><span data-stu-id="7c724-110">Actions</span></span>
<span data-ttu-id="7c724-111">hello **동작** 사용자 지정 역할의 속성 지정 hello Azure 작업 toowhich hello 역할에 대 한 액세스 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c724-111">hello **Actions** property of a custom role specifies hello Azure operations toowhich hello role grants access.</span></span> <span data-ttu-id="7c724-112">Azure 리소스 공급자의 보안 개체 작업을 식별하는 작업 문자열 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="7c724-112">It is a collection of operation strings that identify securable operations of Azure resource providers.</span></span> <span data-ttu-id="7c724-113">작업 문자열의 hello 형식에 따라 `Microsoft.<ProviderName>/<ChildResourceType>/<action>`합니다.</span><span class="sxs-lookup"><span data-stu-id="7c724-113">Operation strings follow hello format of `Microsoft.<ProviderName>/<ChildResourceType>/<action>`.</span></span> <span data-ttu-id="7c724-114">와일드 카드를 포함 하는 작업 문자열 (\*) tooall 작업 hello 작업 문자열과 일치 하는 액세스를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c724-114">Operation strings that contain wildcards (\*) grant access tooall operations that match hello operation string.</span></span> <span data-ttu-id="7c724-115">예:</span><span class="sxs-lookup"><span data-stu-id="7c724-115">For instance:</span></span>

* <span data-ttu-id="7c724-116">`*/read`모든 Azure 리소스 공급자의 모든 리소스 종류에 대 한 tooread 작업 액세스를 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c724-116">`*/read` grants access tooread operations for all resource types of all Azure resource providers.</span></span>
* <span data-ttu-id="7c724-117">`Microsoft.Compute/*`tooall 작업 hello Microsoft.Compute 리소스 공급자에서 모든 리소스 종류에 대 한 액세스를 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c724-117">`Microsoft.Compute/*` grants access tooall operations for all resource types in hello Microsoft.Compute resource provider.</span></span>
* <span data-ttu-id="7c724-118">`Microsoft.Network/*/read`Azure의 hello Microsoft.Network 리소스 공급자에서 모든 리소스 종류에 대 한 tooread 작업 액세스를 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c724-118">`Microsoft.Network/*/read` grants access tooread operations for all resource types in hello Microsoft.Network resource provider of Azure.</span></span>
* <span data-ttu-id="7c724-119">`Microsoft.Compute/virtualMachines/*`가상 컴퓨터 및 해당 자식 리소스 형식의 tooall 작업 액세스를 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c724-119">`Microsoft.Compute/virtualMachines/*` grants access tooall operations of virtual machines and its child resource types.</span></span>
* <span data-ttu-id="7c724-120">`Microsoft.Web/sites/restart/Action`부여는 toorestart 웹 사이트에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c724-120">`Microsoft.Web/sites/restart/Action` grants access toorestart websites.</span></span>

<span data-ttu-id="7c724-121">사용 하 여 `Get-AzureRmProviderOperation` (PowerShell)에서 또는 `azure provider operations show` (Azure CLI)에서 Azure 리소스 공급자의 toolist 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c724-121">Use `Get-AzureRmProviderOperation` (in PowerShell) or `azure provider operations show` (in Azure CLI) toolist operations of Azure resource providers.</span></span> <span data-ttu-id="7c724-122">이러한 명령은 tooverify 작업 문자열 올바른지 및 tooexpand 와일드 카드 작업 문자열을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c724-122">You may also use these commands tooverify that an operation string is valid, and tooexpand wildcard operation strings.</span></span>

```
Get-AzureRMProviderOperation Microsoft.Compute/virtualMachines/*/action | FT Operation, OperationName

Get-AzureRMProviderOperation Microsoft.Network/*
```

![PowerShell 스크린샷 - Get-AzureRMProviderOperation](./media/role-based-access-control-configure/1-get-azurermprovideroperation-1.png)

```
azure provider operations show "Microsoft.Compute/virtualMachines/*/action" --js on | jq '.[] | .operation'

azure provider operations show "Microsoft.Network/*"
```

![<span data-ttu-id="7c724-124">Azure CLI 스크린샷 - azure 공급자 작업 표시 "Microsoft.Compute/virtualMachines/\*/action"</span><span class="sxs-lookup"><span data-stu-id="7c724-124">Azure CLI screenshot - azure provider operations show "Microsoft.Compute/virtualMachines/\*/action"</span></span> ](./media/role-based-access-control-configure/1-azure-provider-operations-show.png)

## <a name="notactions"></a><span data-ttu-id="7c724-125">NotActions</span><span class="sxs-lookup"><span data-stu-id="7c724-125">NotActions</span></span>
<span data-ttu-id="7c724-126">사용 하 여 hello **NotActions** tooallow 원하는 작업 hello 집합은 제한 된 작업을 제외 하 여 보다 쉽게 정의 하는 경우 속성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c724-126">Use hello **NotActions** property if hello set of operations that you wish tooallow is more easily defined by excluding restricted operations.</span></span> <span data-ttu-id="7c724-127">hello 사용자 지정 역할에 의해 부여 된 액세스는 빼는 방식으로 계산 hello **NotActions** hello에서 작업 **동작** 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c724-127">hello access granted by a custom role is computed by subtracting hello **NotActions** operations from hello **Actions** operations.</span></span>

> [!NOTE]
> <span data-ttu-id="7c724-128">사용자의 작업을 제외 하는 역할이 할당 하는 경우 **NotActions**, 액세스를 부여 하는 두 번째 역할 할당은 동일한 작업을 hello 사용자가 toohello tooperform 해당 작업을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c724-128">If a user is assigned a role that excludes an operation in **NotActions**, and is assigned a second role that grants access toohello same operation, hello user is allowed tooperform that operation.</span></span> <span data-ttu-id="7c724-129">**NotActions** deny가 규칙 – 특정 작업 toobe 제외 해야 하는 경우 단순히 편리한 방법을 toocreate 허용 되는 작업의 집합에는 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c724-129">**NotActions** is not a deny rule – it is simply a convenient way toocreate a set of allowed operations when specific operations need toobe excluded.</span></span>
>
>

## <a name="assignablescopes"></a><span data-ttu-id="7c724-130">AssignableScopes</span><span class="sxs-lookup"><span data-stu-id="7c724-130">AssignableScopes</span></span>
<span data-ttu-id="7c724-131">hello **AssignableScopes** hello 사용자 지정 역할의 속성을 사용자 지정 역할은 할당에 사용할 수 있는 hello 내 hello 범위 (구독, 리소스 그룹 또는 리소스)을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c724-131">hello **AssignableScopes** property of hello custom role specifies hello scopes (subscriptions, resource groups, or resources) within which hello custom role is available for assignment.</span></span> <span data-ttu-id="7c724-132">Hello 사용자 지정 역할 할당에 사용할 수 있는 hello 구독만에서 만들거나 hello 나머지 hello 구독 또는 리소스 그룹에 대 한 리소스 그룹 및 사용자가 아닌 간단 하 게 표시 해야 하는 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="7c724-132">You can make hello custom role available for assignment in only hello subscriptions or resource groups that require it, and not clutter user experience for hello rest of hello subscriptions or resource groups.</span></span>

<span data-ttu-id="7c724-133">유효한 할당 가능한 범위의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7c724-133">Examples of valid assignable scopes include:</span></span>

* <span data-ttu-id="7c724-134">"/ 구독/c276fc76-9cd4-44c9-99a7-4fd71546436e", "/ 구독/e91d47c4-76f3-4271-a796-21b4ecfe3624"-두 구독에 할당에 사용할 수 있는 hello 역할을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7c724-134">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e”, “/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624” - makes hello role available for assignment in two subscriptions.</span></span>
* <span data-ttu-id="7c724-135">"/ 구독/c276fc76-9cd4-44c9-99a7-4fd71546436e"-단일 구독에 할당에 사용할 수 있는 hello 역할을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7c724-135">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e” - makes hello role available for assignment in a single subscription.</span></span>
* <span data-ttu-id="7c724-136">"/ 구독/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/네트워크"-는 hello 역할 hello 네트워크 리소스 그룹에만 할당 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c724-136">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network” - makes hello role available for assignment only in hello Network resource group.</span></span>

> [!NOTE]
> <span data-ttu-id="7c724-137">구독, 리소스 그룹 또는 리소스 ID를 적어도 하나 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c724-137">You must use at least one subscription, resource group, or resource ID.</span></span>
>
>

## <a name="custom-roles-access-control"></a><span data-ttu-id="7c724-138">사용자 지정 역할 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="7c724-138">Custom roles access control</span></span>
<span data-ttu-id="7c724-139">hello **AssignableScopes** hello 사용자 지정 역할의 속성을 보고, 수정 및 hello 역할을 삭제할 수 있는 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c724-139">hello **AssignableScopes** property of hello custom role also controls who can view, modify, and delete hello role.</span></span>

* <span data-ttu-id="7c724-140">사용자 지정 역할을 만들 수 있는 사람</span><span class="sxs-lookup"><span data-stu-id="7c724-140">Who can create a custom role?</span></span>
    <span data-ttu-id="7c724-141">구독, 리소스 그룹 및 리소스의 소유자(및 사용자 액세스 관리자)는 해당 범위에 사용할 사용자 지정 역할을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c724-141">Owners (and User Access Administrators) of subscriptions, resource groups, and resources can create custom roles for use in those scopes.</span></span>
    <span data-ttu-id="7c724-142">hello hello 역할을 만드는 사용자 필요한 toobe 수 tooperform `Microsoft.Authorization/roleDefinition/write` 모든 hello에 대 한 작업이 **AssignableScopes** hello 역할의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c724-142">hello user creating hello role needs toobe able tooperform `Microsoft.Authorization/roleDefinition/write` operation on all hello **AssignableScopes** of hello role.</span></span>
* <span data-ttu-id="7c724-143">사용자 지정 역할을 수정할 수 있는 사람</span><span class="sxs-lookup"><span data-stu-id="7c724-143">Who can modify a custom role?</span></span>
    <span data-ttu-id="7c724-144">구독, 리소스 그룹 및 리소스의 소유자(및 사용자 액세스 관리자)는 해당 범위에 사용자 지정 역할을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c724-144">Owners (and User Access Administrators) of subscriptions, resource groups, and resources can modify custom roles in those scopes.</span></span> <span data-ttu-id="7c724-145">사용자에 게 필요 toobe 수 tooperform hello `Microsoft.Authorization/roleDefinition/write` 모든 hello에 대 한 작업이 **AssignableScopes** 사용자 지정 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c724-145">Users need toobe able tooperform hello `Microsoft.Authorization/roleDefinition/write` operation on all hello **AssignableScopes** of a custom role.</span></span>
* <span data-ttu-id="7c724-146">사용자 지정 역할을 볼 수 있는 사용자는 누구인가요?</span><span class="sxs-lookup"><span data-stu-id="7c724-146">Who can view custom roles?</span></span>
    <span data-ttu-id="7c724-147">Azure RBAC에서 모든 기본 제공 역할은 할당 가능한 역할을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c724-147">All built-in roles in Azure RBAC allow viewing of roles that are available for assignment.</span></span> <span data-ttu-id="7c724-148">Hello를 수행할 수 있는 사용자 `Microsoft.Authorization/roleDefinition/read` 작업 범위에서 해당 범위에서 할당에 사용할 수 있는 hello RBAC 역할을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c724-148">Users who can perform hello `Microsoft.Authorization/roleDefinition/read` operation at a scope can view hello RBAC roles that are available for assignment at that scope.</span></span>

## <a name="see-also"></a><span data-ttu-id="7c724-149">참고 항목</span><span class="sxs-lookup"><span data-stu-id="7c724-149">See also</span></span>
* <span data-ttu-id="7c724-150">[역할 기반 액세스 제어](role-based-access-control-configure.md): RBAC hello Azure 포털을에서 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c724-150">[Role Based Access Control](role-based-access-control-configure.md): Get started with RBAC in hello Azure portal.</span></span>
* <span data-ttu-id="7c724-151">Toomanage로 액세스 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7c724-151">Learn how toomanage access with:</span></span>
  * [<span data-ttu-id="7c724-152">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7c724-152">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
  * [<span data-ttu-id="7c724-153">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7c724-153">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
  * [<span data-ttu-id="7c724-154">REST API</span><span class="sxs-lookup"><span data-stu-id="7c724-154">REST API</span></span>](role-based-access-control-manage-access-rest.md)
* <span data-ttu-id="7c724-155">[기본 제공 역할](role-based-access-built-in-roles.md): RBAC에 기본적으로 제공 하는 hello 역할에 대 한 세부 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7c724-155">[Built-in roles](role-based-access-built-in-roles.md): Get details about hello roles that come standard in RBAC.</span></span>
