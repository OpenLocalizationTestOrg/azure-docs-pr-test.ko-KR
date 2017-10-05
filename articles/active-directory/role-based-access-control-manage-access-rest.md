---
title: "REST를 사용한 역할 기반 액세스 제어 - Azure AD | Microsoft Docs"
description: "REST API를 사용하여 역할 기반 액세스 제어 관리"
services: active-directory
documentationcenter: na
author: andredm7
manager: femila
editor: 
ms.assetid: 1f90228a-7aac-4ea7-ad82-b57d222ab128
ms.service: active-directory
ms.workload: multiple
ms.tgt_pltfrm: rest-api
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: andredm
ms.openlocfilehash: a5c19fd87ce1ae3e199bf1dfc8cf82f5653baac2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-role-based-access-control-with-the-rest-api"></a><span data-ttu-id="3b488-103">REST API를 사용하여 역할 기반 액세스 제어 관리</span><span class="sxs-lookup"><span data-stu-id="3b488-103">Manage Role-Based Access Control with the REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3b488-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3b488-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="3b488-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3b488-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="3b488-106">REST API</span><span class="sxs-lookup"><span data-stu-id="3b488-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)

<span data-ttu-id="3b488-107">Azure Portal 및 Azure Resource Manager API의 RBAC(역할 기반 액세스 제어)를 사용하면 세밀한 수준에서 구독과 리소스에 대한 액세스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-107">Role-Based Access Control (RBAC) in the Azure portal and Azure Resource Manager API helps you manage access to your subscription and resources at a fine-grained level.</span></span> <span data-ttu-id="3b488-108">이 기능을 통해 특정 범위에서 Active Directory 사용자, 그룹 또는 서비스 사용자에게 일부 역할을 할당하여 액세스 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles to them at a particular scope.</span></span>

## <a name="list-all-role-assignments"></a><span data-ttu-id="3b488-109">모든 역할 할당 나열</span><span class="sxs-lookup"><span data-stu-id="3b488-109">List all role assignments</span></span>
<span data-ttu-id="3b488-110">지정된 범위 및 하위 범위에서 모든 역할 할당을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-110">Lists all the role assignments at the specified scope and subscopes.</span></span>

<span data-ttu-id="3b488-111">역할 할당을 나열하려면 범위에서 `Microsoft.Authorization/roleAssignments/read` 작업에 대한 액세스 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-111">To list role assignments, you must have access to `Microsoft.Authorization/roleAssignments/read` operation at the scope.</span></span> <span data-ttu-id="3b488-112">모든 기본 제공 역할에는 이 작업에 대한 액세스 권한이 부여되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-112">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="3b488-113">Azure 리소스에 대한 액세스 관리 및 역할 할당에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어](role-based-access-control-configure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b488-113">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="3b488-114">요청</span><span class="sxs-lookup"><span data-stu-id="3b488-114">Request</span></span>
<span data-ttu-id="3b488-115">다음 URI와 함께 **GET** 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-115">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments?api-version={api-version}&$filter={filter}

<span data-ttu-id="3b488-116">URI 내에서 다음을 대체하여 요청을 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-116">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="3b488-117">*{scope}* 를 역할 할당을 나열하려는 범위로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-117">Replace *{scope}* with the scope for which you wish to list the role assignments.</span></span> <span data-ttu-id="3b488-118">다음 예제에서는 서로 다른 수준에 대해 범위를 지정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-118">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="3b488-119">구독: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="3b488-119">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="3b488-120">리소스 그룹: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="3b488-120">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="3b488-121">리소스: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="3b488-121">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="3b488-122">*{api-version}* 을 2015-07-01로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-122">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="3b488-123">*{filter}* 를 역할 할당 목록을 필터링하기 위해 적용하려는 조건으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-123">Replace *{filter}* with the condition that you wish to apply to filter the role assignment list:</span></span>

   * <span data-ttu-id="3b488-124">하위 범위에서는 역할 할당을 포함시키지 않고 지정된 범위에 대해서만 역할 할당 나열: `atScope()`</span><span class="sxs-lookup"><span data-stu-id="3b488-124">List role assignments for only the specified scope, not including the role assignments at subscopes: `atScope()`</span></span>    
   * <span data-ttu-id="3b488-125">특정 사용자, 그룹 또는 응용 프로그램에 대해서만 역할 할당 나열: `principalId%20eq%20'{objectId of user, group, or service principal}'`</span><span class="sxs-lookup"><span data-stu-id="3b488-125">List role assignments for a specific user, group, or application: `principalId%20eq%20'{objectId of user, group, or service principal}'`</span></span>  
   * <span data-ttu-id="3b488-126">그룹에서 상속된 역할 할당을 포함하여 특정 사용자에 대한 역할 할당 나열 | `assignedTo('{objectId of user}')`</span><span class="sxs-lookup"><span data-stu-id="3b488-126">List role assignments for a specific user, including ones inherited from groups | `assignedTo('{objectId of user}')`</span></span>

### <a name="response"></a><span data-ttu-id="3b488-127">응답</span><span class="sxs-lookup"><span data-stu-id="3b488-127">Response</span></span>
<span data-ttu-id="3b488-128">상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="3b488-128">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7",
        "principalId": "2f9d4375-cbf1-48e8-83c9-2a0be4cb33fb",
        "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
        "createdOn": "2015-10-08T07:28:24.3905077Z",
        "updatedOn": "2015-10-08T07:28:24.3905077Z",
        "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
        "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleAssignments/baa6e199-ad19-4667-b768-623fde31aedd",
      "type": "Microsoft.Authorization/roleAssignments",
      "name": "baa6e199-ad19-4667-b768-623fde31aedd"
    }
  ],
  "nextLink": null
}

```

## <a name="get-information-about-a-role-assignment"></a><span data-ttu-id="3b488-129">역할 할당에 대한 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="3b488-129">Get information about a role assignment</span></span>
<span data-ttu-id="3b488-130">역할 할당 식별자에서 지정한 단일 역할 할당에 대한 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-130">Gets information about a single role assignment specified by the role assignment identifier.</span></span>

<span data-ttu-id="3b488-131">역할 할당에 대한 정보를 가져오려면 `Microsoft.Authorization/roleAssignments/read` 작업에 대한 액세스 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-131">To get information about a role assignment, you must have access to `Microsoft.Authorization/roleAssignments/read` operation.</span></span> <span data-ttu-id="3b488-132">모든 기본 제공 역할에는 이 작업에 대한 액세스 권한이 부여되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-132">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="3b488-133">Azure 리소스에 대한 액세스 관리 및 역할 할당에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어](role-based-access-control-configure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b488-133">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="3b488-134">요청</span><span class="sxs-lookup"><span data-stu-id="3b488-134">Request</span></span>
<span data-ttu-id="3b488-135">다음 URI와 함께 **GET** 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-135">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="3b488-136">URI 내에서 다음을 대체하여 요청을 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-136">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="3b488-137">*{scope}* 를 역할 할당을 나열하려는 범위로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-137">Replace *{scope}* with the scope for which you wish to list the role assignments.</span></span> <span data-ttu-id="3b488-138">다음 예제에서는 서로 다른 수준에 대해 범위를 지정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-138">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="3b488-139">구독: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="3b488-139">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="3b488-140">리소스 그룹: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="3b488-140">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="3b488-141">리소스: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="3b488-141">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="3b488-142">*{role-assignment-id}* 를 역할 할당의 GUID 식별자로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-142">Replace *{role-assignment-id}* with the GUID identifier of the role assignment.</span></span>
3. <span data-ttu-id="3b488-143">*{api-version}* 을 2015-07-01로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-143">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="3b488-144">응답</span><span class="sxs-lookup"><span data-stu-id="3b488-144">Response</span></span>
<span data-ttu-id="3b488-145">상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="3b488-145">Status code: 200</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/b24988ac-6180-42a0-ab88-20f7382dd24c",
    "principalId": "672f1afa-526a-4ef6-819c-975c7cd79022",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "createdOn": "2015-10-05T08:36:26.4014813Z",
    "updatedOn": "2015-10-05T08:36:26.4014813Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleAssignments/196965ae-6088-4121-a92a-f1e33fdcc73e",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "196965ae-6088-4121-a92a-f1e33fdcc73e"
}

```

## <a name="create-a-role-assignment"></a><span data-ttu-id="3b488-146">역할 할당 만들기</span><span class="sxs-lookup"><span data-stu-id="3b488-146">Create a Role Assignment</span></span>
<span data-ttu-id="3b488-147">지정된 역할을 부여하는 지정된 보안 주체에 대해 지정된 범위에서 역할 할당을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-147">Create a role assignment at the specified scope for the specified principal granting the specified role.</span></span>

<span data-ttu-id="3b488-148">역할 할당을 만들려면 `Microsoft.Authorization/roleAssignments/write` 작업에 대한 액세스 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-148">To create a role assignment, you must have access to `Microsoft.Authorization/roleAssignments/write` operation.</span></span> <span data-ttu-id="3b488-149">기본 제공 역할의 경우 *소유자* 및 *사용자 액세스 관리자*에게만 이러한 작업의 권한이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-149">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="3b488-150">Azure 리소스에 대한 액세스 관리 및 역할 할당에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어](role-based-access-control-configure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b488-150">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="3b488-151">요청</span><span class="sxs-lookup"><span data-stu-id="3b488-151">Request</span></span>
<span data-ttu-id="3b488-152">다음 URI와 함께 **PUT** 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-152">Use the **PUT** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="3b488-153">URI 내에서 다음을 대체하여 요청을 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-153">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="3b488-154">*{scope}* 를 역할 할당을 만들려는 범위로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-154">Replace *{scope}* with the scope at which you wish to create the role assignments.</span></span> <span data-ttu-id="3b488-155">부모 범위에서 역할 할당을 만들 때 모든 자식 범위는 같은 역할 할당을 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-155">When you create a role assignment at a parent scope, all child scopes inherit the same role assignment.</span></span> <span data-ttu-id="3b488-156">다음 예제에서는 서로 다른 수준에 대해 범위를 지정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-156">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="3b488-157">구독: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="3b488-157">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="3b488-158">리소스 그룹: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="3b488-158">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>   
   * <span data-ttu-id="3b488-159">리소스: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="3b488-159">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="3b488-160">*{role-assignment-id}* 를 새 역할 할당의 GUID 식별자가 되는 새 GUID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-160">Replace *{role-assignment-id}* with a new GUID, which becomes the GUID identifier of the new role assignment.</span></span>
3. <span data-ttu-id="3b488-161">*{api-version}* 을 2015-07-01로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-161">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="3b488-162">요청 본문에 대해 다음과 같은 형식으로 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-162">For the request body, provide the values in the following format:</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b"
  }
}

```

| <span data-ttu-id="3b488-163">요소 이름</span><span class="sxs-lookup"><span data-stu-id="3b488-163">Element Name</span></span> | <span data-ttu-id="3b488-164">필수</span><span class="sxs-lookup"><span data-stu-id="3b488-164">Required</span></span> | <span data-ttu-id="3b488-165">형식</span><span class="sxs-lookup"><span data-stu-id="3b488-165">Type</span></span> | <span data-ttu-id="3b488-166">설명</span><span class="sxs-lookup"><span data-stu-id="3b488-166">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b488-167">roleDefinitionId</span><span class="sxs-lookup"><span data-stu-id="3b488-167">roleDefinitionId</span></span> |<span data-ttu-id="3b488-168">예</span><span class="sxs-lookup"><span data-stu-id="3b488-168">Yes</span></span> |<span data-ttu-id="3b488-169">문자열</span><span class="sxs-lookup"><span data-stu-id="3b488-169">String</span></span> |<span data-ttu-id="3b488-170">역할의 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-170">The identifier of the role.</span></span> <span data-ttu-id="3b488-171">식별자의 형식은 `{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span><span class="sxs-lookup"><span data-stu-id="3b488-171">The format of the identifier is: `{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span></span> |
| <span data-ttu-id="3b488-172">principalId</span><span class="sxs-lookup"><span data-stu-id="3b488-172">principalId</span></span> |<span data-ttu-id="3b488-173">예</span><span class="sxs-lookup"><span data-stu-id="3b488-173">Yes</span></span> |<span data-ttu-id="3b488-174">문자열</span><span class="sxs-lookup"><span data-stu-id="3b488-174">String</span></span> |<span data-ttu-id="3b488-175">역할을 할당할 Azure AD 보안 주체(사용자, 그룹 또는 서비스 사용자)의 objectId입니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-175">objectId of the Azure AD principal (user, group, or service principal) to which the role is assigned.</span></span> |

### <a name="response"></a><span data-ttu-id="3b488-176">응답</span><span class="sxs-lookup"><span data-stu-id="3b488-176">Response</span></span>
<span data-ttu-id="3b488-177">상태 코드: 201</span><span class="sxs-lookup"><span data-stu-id="3b488-177">Status code: 201</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND",
    "createdOn": "2015-12-16T00:27:19.6447515Z",
    "updatedOn": "2015-12-16T00:27:19.6447515Z",
    "createdBy": null,
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleAssignments/2e9e86c8-0e91-4958-b21f-20f51f27bab2",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "2e9e86c8-0e91-4958-b21f-20f51f27bab2"
}

```

## <a name="delete-a-role-assignment"></a><span data-ttu-id="3b488-178">역할 할당 삭제</span><span class="sxs-lookup"><span data-stu-id="3b488-178">Delete a Role Assignment</span></span>
<span data-ttu-id="3b488-179">지정된 범위에서 역할 할당을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-179">Delete a role assignment at the specified scope.</span></span>

<span data-ttu-id="3b488-180">역할 할당을 삭제하려면 `Microsoft.Authorization/roleAssignments/delete` 작업에 대한 액세스 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-180">To delete a role assignment, you must have access to the `Microsoft.Authorization/roleAssignments/delete` operation.</span></span> <span data-ttu-id="3b488-181">기본 제공 역할의 경우 *소유자* 및 *사용자 액세스 관리자*에게만 이러한 작업의 권한이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-181">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="3b488-182">Azure 리소스에 대한 액세스 관리 및 역할 할당에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어](role-based-access-control-configure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b488-182">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="3b488-183">요청</span><span class="sxs-lookup"><span data-stu-id="3b488-183">Request</span></span>
<span data-ttu-id="3b488-184">다음 URI와 함께 **DELETE** 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-184">Use the **DELETE** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="3b488-185">URI 내에서 다음을 대체하여 요청을 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-185">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="3b488-186">*{scope}* 를 역할 할당을 만들려는 범위로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-186">Replace *{scope}* with the scope at which you wish to create the role assignments.</span></span> <span data-ttu-id="3b488-187">다음 예제에서는 서로 다른 수준에 대해 범위를 지정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-187">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="3b488-188">구독: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="3b488-188">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="3b488-189">리소스 그룹: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="3b488-189">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="3b488-190">리소스: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="3b488-190">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="3b488-191">*{role-assignment-id}* 를 역할 할당 id GUID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-191">Replace *{role-assignment-id}* with the role assignment id GUID.</span></span>
3. <span data-ttu-id="3b488-192">*{api-version}* 을 2015-07-01로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-192">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="3b488-193">응답</span><span class="sxs-lookup"><span data-stu-id="3b488-193">Response</span></span>
<span data-ttu-id="3b488-194">상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="3b488-194">Status code: 200</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND",
    "createdOn": "2015-12-17T23:21:40.8921564Z",
    "updatedOn": "2015-12-17T23:21:40.8921564Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleAssignments/5eec22ee-ea5c-431e-8f41-82c560706fd2",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "5eec22ee-ea5c-431e-8f41-82c560706fd2"
}

```

## <a name="list-all-roles"></a><span data-ttu-id="3b488-195">모든 역할 나열</span><span class="sxs-lookup"><span data-stu-id="3b488-195">List all Roles</span></span>
<span data-ttu-id="3b488-196">지정된 범위에서 할당에 사용할 수 있는 모든 역할을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-196">Lists all the roles that are available for assignment at the specified scope.</span></span>

<span data-ttu-id="3b488-197">역할을 나열하려면 범위에서 `Microsoft.Authorization/roleDefinitions/read` 작업에 대한 액세스 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-197">To list roles, you must have access to `Microsoft.Authorization/roleDefinitions/read` operation at the scope.</span></span> <span data-ttu-id="3b488-198">모든 기본 제공 역할에는 이 작업에 대한 액세스 권한이 부여되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-198">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="3b488-199">Azure 리소스에 대한 액세스 관리 및 역할 할당에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어](role-based-access-control-configure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b488-199">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="3b488-200">요청</span><span class="sxs-lookup"><span data-stu-id="3b488-200">Request</span></span>
<span data-ttu-id="3b488-201">다음 URI와 함께 **GET** 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-201">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions?api-version={api-version}&$filter={filter}

<span data-ttu-id="3b488-202">URI 내에서 다음을 대체하여 요청을 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-202">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="3b488-203">*{scope}* 를 역할을 나열하려는 범위로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-203">Replace *{scope}* with the scope for which you wish to list the roles.</span></span> <span data-ttu-id="3b488-204">다음 예제에서는 서로 다른 수준에 대해 범위를 지정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-204">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="3b488-205">구독: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="3b488-205">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="3b488-206">리소스 그룹: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="3b488-206">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="3b488-207">리소스: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="3b488-207">Resource /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="3b488-208">*{api-version}* 을 2015-07-01로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-208">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="3b488-209">*{filter}* 를 역할 목록을 필터링하기 위해 적용할 조건으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-209">Replace *{filter}* with the condition that you wish to apply to filter the list of roles:</span></span>

   * <span data-ttu-id="3b488-210">지정된 범위 및 해당 자식 범위에서 할당에 사용할 수 있는 역할 나열: `atScopeAndBelow()`</span><span class="sxs-lookup"><span data-stu-id="3b488-210">List roles available for assignment at the specified scope and any of its child scopes: `atScopeAndBelow()`</span></span>
   * <span data-ttu-id="3b488-211">정확한 표시 이름을 사용하여 역할 검색: `roleName%20eq%20'{role-display-name}'`</span><span class="sxs-lookup"><span data-stu-id="3b488-211">Search for a role using exact display name: `roleName%20eq%20'{role-display-name}'`.</span></span> <span data-ttu-id="3b488-212">역할의 정확한 표시 이름에 대한 URL 인코딩 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-212">Use the URL encoded form of the exact display name of the role.</span></span> <span data-ttu-id="3b488-213">예를 들어, `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span><span class="sxs-lookup"><span data-stu-id="3b488-213">For instance, `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span></span>

### <a name="response"></a><span data-ttu-id="3b488-214">응답</span><span class="sxs-lookup"><span data-stu-id="3b488-214">Response</span></span>
<span data-ttu-id="3b488-215">상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="3b488-215">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access to them, and not the virtual network or storage account they\u2019re connected to.",
        "assignableScopes": [
          "/"
        ],
        "permissions": [
          {
            "actions": [
              "Microsoft.Authorization/*/read",
              "Microsoft.Compute/availabilitySets/*",
              "Microsoft.Compute/locations/*",
              "Microsoft.Compute/virtualMachines/*",
              "Microsoft.Compute/virtualMachineScaleSets/*",
              "Microsoft.Insights/alertRules/*",
              "Microsoft.Network/applicationGateways/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatRules/join/action",
              "Microsoft.Network/loadBalancers/read",
              "Microsoft.Network/locations/*",
              "Microsoft.Network/networkInterfaces/*",
              "Microsoft.Network/networkSecurityGroups/join/action",
              "Microsoft.Network/networkSecurityGroups/read",
              "Microsoft.Network/publicIPAddresses/join/action",
              "Microsoft.Network/publicIPAddresses/read",
              "Microsoft.Network/virtualNetworks/read",
              "Microsoft.Network/virtualNetworks/subnets/join/action",
              "Microsoft.Resources/deployments/*",
              "Microsoft.Resources/subscriptions/resourceGroups/read",
              "Microsoft.Storage/storageAccounts/listKeys/action",
              "Microsoft.Storage/storageAccounts/read",
              "Microsoft.Support/*"
            ],
            "notActions": []
          }
        ],
        "createdOn": "2015-06-02T00:18:27.3542698Z",
        "updatedOn": "2015-12-08T03:16:55.6170255Z",
        "createdBy": null,
        "updatedBy": null
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
      "type": "Microsoft.Authorization/roleDefinitions",
      "name": "9980e02c-c2be-4d73-94e8-173b1dc7cf3c"
    }
  ],
  "nextLink": null
}

```

## <a name="get-information-about-a-role"></a><span data-ttu-id="3b488-216">역할에 대한 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="3b488-216">Get information about a Role</span></span>
<span data-ttu-id="3b488-217">역할 정의 식별자에서 지정한 단일 역할에 대한 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-217">Gets information about a single role specified by the role definition identifier.</span></span> <span data-ttu-id="3b488-218">해당 표시 이름을 사용하여 단일 역할에 대한 정보를 가져오려면 [모든 역할 나열](role-based-access-control-manage-access-rest.md#list-all-roles)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b488-218">To get information about a single role using its display name, see [List all roles](role-based-access-control-manage-access-rest.md#list-all-roles).</span></span>

<span data-ttu-id="3b488-219">역할에 대한 정보를 가져오려면 `Microsoft.Authorization/roleDefinitions/read` 작업에 대한 액세스 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-219">To get information about a role, you must have access to `Microsoft.Authorization/roleDefinitions/read` operation.</span></span> <span data-ttu-id="3b488-220">모든 기본 제공 역할에는 이 작업에 대한 액세스 권한이 부여되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-220">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="3b488-221">Azure 리소스에 대한 액세스 관리 및 역할 할당에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어](role-based-access-control-configure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b488-221">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="3b488-222">요청</span><span class="sxs-lookup"><span data-stu-id="3b488-222">Request</span></span>
<span data-ttu-id="3b488-223">다음 URI와 함께 **GET** 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-223">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="3b488-224">URI 내에서 다음을 대체하여 요청을 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-224">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="3b488-225">*{scope}* 를 역할 할당을 나열하려는 범위로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-225">Replace *{scope}* with the scope for which you wish to list the role assignments.</span></span> <span data-ttu-id="3b488-226">다음 예제에서는 서로 다른 수준에 대해 범위를 지정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-226">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="3b488-227">구독: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="3b488-227">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="3b488-228">리소스 그룹: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="3b488-228">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="3b488-229">리소스: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="3b488-229">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="3b488-230">*{role-definition-id}* 를 역할 정의의 GUID 식별자로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-230">Replace *{role-definition-id}* with the GUID identifier of the role definition.</span></span>
3. <span data-ttu-id="3b488-231">*{api-version}* 을 2015-07-01로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-231">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="3b488-232">응답</span><span class="sxs-lookup"><span data-stu-id="3b488-232">Response</span></span>
<span data-ttu-id="3b488-233">상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="3b488-233">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access to them, and not the virtual network or storage account they\u2019re connected to.",
        "assignableScopes": [
          "/"
        ],
        "permissions": [
          {
            "actions": [
              "Microsoft.Authorization/*/read",
              "Microsoft.Compute/availabilitySets/*",
              "Microsoft.Compute/locations/*",
              "Microsoft.Compute/virtualMachines/*",
              "Microsoft.Compute/virtualMachineScaleSets/*",
              "Microsoft.Insights/alertRules/*",
              "Microsoft.Network/applicationGateways/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatRules/join/action",
              "Microsoft.Network/loadBalancers/read",
              "Microsoft.Network/locations/*",
              "Microsoft.Network/networkInterfaces/*",
              "Microsoft.Network/networkSecurityGroups/join/action",
              "Microsoft.Network/networkSecurityGroups/read",
              "Microsoft.Network/publicIPAddresses/join/action",
              "Microsoft.Network/publicIPAddresses/read",
              "Microsoft.Network/virtualNetworks/read",
              "Microsoft.Network/virtualNetworks/subnets/join/action",
              "Microsoft.Resources/deployments/*",
              "Microsoft.Resources/subscriptions/resourceGroups/read",
              "Microsoft.Storage/storageAccounts/listKeys/action",
              "Microsoft.Storage/storageAccounts/read",
              "Microsoft.Support/*"
            ],
            "notActions": []
          }
        ],
        "createdOn": "2015-06-02T00:18:27.3542698Z",
        "updatedOn": "2015-12-08T03:16:55.6170255Z",
        "createdBy": null,
        "updatedBy": null
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
      "type": "Microsoft.Authorization/roleDefinitions",
      "name": "9980e02c-c2be-4d73-94e8-173b1dc7cf3c"
    }
  ],
  "nextLink": null
}

```

## <a name="create-a-custom-role"></a><span data-ttu-id="3b488-234">사용자 지정 역할 만들기</span><span class="sxs-lookup"><span data-stu-id="3b488-234">Create a Custom Role</span></span>
<span data-ttu-id="3b488-235">사용자 지정 역할을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-235">Create a custom role.</span></span>

<span data-ttu-id="3b488-236">사용자 지정 역할을 만들려면 해당하는 모든 `AssignableScopes`에서 `Microsoft.Authorization/roleDefinitions/write` 작업에 대한 액세스 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-236">To create a custom role, you must have access to `Microsoft.Authorization/roleDefinitions/write` operation on all the `AssignableScopes`.</span></span> <span data-ttu-id="3b488-237">기본 제공 역할의 경우 *소유자* 및 *사용자 액세스 관리자*에게만 이러한 작업의 권한이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-237">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="3b488-238">Azure 리소스에 대한 액세스 관리 및 역할 할당에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어](role-based-access-control-configure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b488-238">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="3b488-239">요청</span><span class="sxs-lookup"><span data-stu-id="3b488-239">Request</span></span>
<span data-ttu-id="3b488-240">다음 URI와 함께 **PUT** 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-240">Use the **PUT** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="3b488-241">URI 내에서 다음을 대체하여 요청을 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-241">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="3b488-242">*{scope}*을 사용자 지정 역할의 첫 번째 *AssignableScope*으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-242">Replace *{scope}* with the first *AssignableScope* of the custom role.</span></span> <span data-ttu-id="3b488-243">다음 예제는 서로 다른 수준에 대한 범위를 지정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-243">The following examples show how to specify the scope for different levels.</span></span>

   * <span data-ttu-id="3b488-244">구독: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="3b488-244">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="3b488-245">리소스 그룹: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="3b488-245">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="3b488-246">리소스: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="3b488-246">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="3b488-247">*{role-definition-id}* 를 새 사용자 지정 역할의 GUID 식별자가 되는 새 GUID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-247">Replace *{role-definition-id}* with a new GUID, which becomes the GUID identifier of the new custom role.</span></span>
3. <span data-ttu-id="3b488-248">*{api-version}* 을 2015-07-01로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-248">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="3b488-249">요청 본문에 대해 다음과 같은 형식으로 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-249">For the request body, provide the values in the following format:</span></span>

```
{
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "properties": {
    "roleName": "Virtual Machine Operator",
    "description": "Lets you monitor virtual machines and restart them.",
    "type": "CustomRole",
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
  }
}

```

| <span data-ttu-id="3b488-250">요소 이름</span><span class="sxs-lookup"><span data-stu-id="3b488-250">Element Name</span></span> | <span data-ttu-id="3b488-251">필수</span><span class="sxs-lookup"><span data-stu-id="3b488-251">Required</span></span> | <span data-ttu-id="3b488-252">형식</span><span class="sxs-lookup"><span data-stu-id="3b488-252">Type</span></span> | <span data-ttu-id="3b488-253">설명</span><span class="sxs-lookup"><span data-stu-id="3b488-253">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b488-254">name</span><span class="sxs-lookup"><span data-stu-id="3b488-254">name</span></span> |<span data-ttu-id="3b488-255">예</span><span class="sxs-lookup"><span data-stu-id="3b488-255">Yes</span></span> |<span data-ttu-id="3b488-256">문자열</span><span class="sxs-lookup"><span data-stu-id="3b488-256">String</span></span> |<span data-ttu-id="3b488-257">사용자 지정 역할의 GUID 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-257">GUID identifier of the custom role.</span></span> |
| <span data-ttu-id="3b488-258">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="3b488-258">properties.roleName</span></span> |<span data-ttu-id="3b488-259">예</span><span class="sxs-lookup"><span data-stu-id="3b488-259">Yes</span></span> |<span data-ttu-id="3b488-260">문자열</span><span class="sxs-lookup"><span data-stu-id="3b488-260">String</span></span> |<span data-ttu-id="3b488-261">사용자 지정 역할의 표시 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-261">Display name of the custom role.</span></span> <span data-ttu-id="3b488-262">최대 128자입니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-262">Maximum size 128 characters.</span></span> |
| <span data-ttu-id="3b488-263">properties.description</span><span class="sxs-lookup"><span data-stu-id="3b488-263">properties.description</span></span> |<span data-ttu-id="3b488-264">아니요</span><span class="sxs-lookup"><span data-stu-id="3b488-264">No</span></span> |<span data-ttu-id="3b488-265">문자열</span><span class="sxs-lookup"><span data-stu-id="3b488-265">String</span></span> |<span data-ttu-id="3b488-266">사용자 지정 역할에 대한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-266">Description of the custom role.</span></span> <span data-ttu-id="3b488-267">최대 1024자입니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-267">Maximum size 1024 characters.</span></span> |
| <span data-ttu-id="3b488-268">properties.type</span><span class="sxs-lookup"><span data-stu-id="3b488-268">properties.type</span></span> |<span data-ttu-id="3b488-269">예</span><span class="sxs-lookup"><span data-stu-id="3b488-269">Yes</span></span> |<span data-ttu-id="3b488-270">문자열</span><span class="sxs-lookup"><span data-stu-id="3b488-270">String</span></span> |<span data-ttu-id="3b488-271">"CustomRole"로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-271">Set to "CustomRole."</span></span> |
| <span data-ttu-id="3b488-272">properties.permissions.actions</span><span class="sxs-lookup"><span data-stu-id="3b488-272">properties.permissions.actions</span></span> |<span data-ttu-id="3b488-273">예</span><span class="sxs-lookup"><span data-stu-id="3b488-273">Yes</span></span> |<span data-ttu-id="3b488-274">문자열[]</span><span class="sxs-lookup"><span data-stu-id="3b488-274">String[]</span></span> |<span data-ttu-id="3b488-275">사용자 지정 역할이 권한을 부여하는 작업을 지정하는 동작 문자열의 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-275">An array of action strings specifying the operations granted by the custom role.</span></span> |
| <span data-ttu-id="3b488-276">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="3b488-276">properties.permissions.notActions</span></span> |<span data-ttu-id="3b488-277">아니요</span><span class="sxs-lookup"><span data-stu-id="3b488-277">No</span></span> |<span data-ttu-id="3b488-278">문자열[]</span><span class="sxs-lookup"><span data-stu-id="3b488-278">String[]</span></span> |<span data-ttu-id="3b488-279">사용자 지정 역할이 권한을 부여하는 작업에서 제외할 작업을 지정하는 동작 문자열의 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-279">An array of action strings specifying the operations to exclude from the operations granted by the custom role.</span></span> |
| <span data-ttu-id="3b488-280">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="3b488-280">properties.assignableScopes</span></span> |<span data-ttu-id="3b488-281">예</span><span class="sxs-lookup"><span data-stu-id="3b488-281">Yes</span></span> |<span data-ttu-id="3b488-282">문자열[]</span><span class="sxs-lookup"><span data-stu-id="3b488-282">String[]</span></span> |<span data-ttu-id="3b488-283">사용자 지정 역할을 사용할 수 있는 범위의 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-283">An array of scopes in which the custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="3b488-284">응답</span><span class="sxs-lookup"><span data-stu-id="3b488-284">Response</span></span>
<span data-ttu-id="3b488-285">상태 코드: 201</span><span class="sxs-lookup"><span data-stu-id="3b488-285">Status code: 201</span></span>

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-18T00:10:51.4662695Z",
    "updatedOn": "2015-12-18T00:10:51.4662695Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7"
}

```

## <a name="update-a-custom-role"></a><span data-ttu-id="3b488-286">사용자 지정 역할 업데이트</span><span class="sxs-lookup"><span data-stu-id="3b488-286">Update a Custom Role</span></span>
<span data-ttu-id="3b488-287">사용자 지정 역할을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-287">Modify a custom role.</span></span>

<span data-ttu-id="3b488-288">사용자 지정 역할을 수정하려면 해당하는 모든 `AssignableScopes`에서 `Microsoft.Authorization/roleDefinitions/write` 작업에 대한 액세스 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-288">To modify a custom role, you must have access to `Microsoft.Authorization/roleDefinitions/write` operation on all the `AssignableScopes`.</span></span> <span data-ttu-id="3b488-289">기본 제공 역할의 경우 *소유자* 및 *사용자 액세스 관리자*에게만 이러한 작업의 권한이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-289">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="3b488-290">Azure 리소스에 대한 액세스 관리 및 역할 할당에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어](role-based-access-control-configure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b488-290">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="3b488-291">요청</span><span class="sxs-lookup"><span data-stu-id="3b488-291">Request</span></span>
<span data-ttu-id="3b488-292">다음 URI와 함께 **PUT** 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-292">Use the **PUT** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="3b488-293">URI 내에서 다음을 대체하여 요청을 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-293">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="3b488-294">*{scope}*을 사용자 지정 역할의 첫 번째 *AssignableScope*으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-294">Replace *{scope}* with the first *AssignableScope* of the custom role.</span></span> <span data-ttu-id="3b488-295">다음 예제에서는 서로 다른 수준에 대해 범위를 지정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-295">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="3b488-296">구독: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="3b488-296">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="3b488-297">리소스 그룹: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="3b488-297">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="3b488-298">리소스: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="3b488-298">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="3b488-299">*{role-definition-id}* 를 사용자 지정 역할의 GUID 식별자로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-299">Replace *{role-definition-id}* with the GUID identifier of the custom role.</span></span>
3. <span data-ttu-id="3b488-300">*{api-version}* 을 2015-07-01로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-300">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="3b488-301">요청 본문에 대해 다음과 같은 형식으로 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-301">For the request body, provide the values in the following format:</span></span>

```
{
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "properties": {
    "roleName": "Virtual Machine Operator",
    "description": "Lets you monitor virtual machines and restart them.",
    "type": "CustomRole",
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
  }
}

```

| <span data-ttu-id="3b488-302">요소 이름</span><span class="sxs-lookup"><span data-stu-id="3b488-302">Element Name</span></span> | <span data-ttu-id="3b488-303">필수</span><span class="sxs-lookup"><span data-stu-id="3b488-303">Required</span></span> | <span data-ttu-id="3b488-304">형식</span><span class="sxs-lookup"><span data-stu-id="3b488-304">Type</span></span> | <span data-ttu-id="3b488-305">설명</span><span class="sxs-lookup"><span data-stu-id="3b488-305">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b488-306">name</span><span class="sxs-lookup"><span data-stu-id="3b488-306">name</span></span> |<span data-ttu-id="3b488-307">예</span><span class="sxs-lookup"><span data-stu-id="3b488-307">Yes</span></span> |<span data-ttu-id="3b488-308">문자열</span><span class="sxs-lookup"><span data-stu-id="3b488-308">String</span></span> |<span data-ttu-id="3b488-309">사용자 지정 역할의 GUID 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-309">GUID identifier of the custom role.</span></span> |
| <span data-ttu-id="3b488-310">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="3b488-310">properties.roleName</span></span> |<span data-ttu-id="3b488-311">예</span><span class="sxs-lookup"><span data-stu-id="3b488-311">Yes</span></span> |<span data-ttu-id="3b488-312">문자열</span><span class="sxs-lookup"><span data-stu-id="3b488-312">String</span></span> |<span data-ttu-id="3b488-313">업데이트된 사용자 지정 역할의 표시 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-313">Display name of the updated custom role.</span></span> |
| <span data-ttu-id="3b488-314">properties.description</span><span class="sxs-lookup"><span data-stu-id="3b488-314">properties.description</span></span> |<span data-ttu-id="3b488-315">아니요</span><span class="sxs-lookup"><span data-stu-id="3b488-315">No</span></span> |<span data-ttu-id="3b488-316">문자열</span><span class="sxs-lookup"><span data-stu-id="3b488-316">String</span></span> |<span data-ttu-id="3b488-317">업데이트된 사용자 지정 역할의 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-317">Description of the updated custom role.</span></span> |
| <span data-ttu-id="3b488-318">properties.type</span><span class="sxs-lookup"><span data-stu-id="3b488-318">properties.type</span></span> |<span data-ttu-id="3b488-319">예</span><span class="sxs-lookup"><span data-stu-id="3b488-319">Yes</span></span> |<span data-ttu-id="3b488-320">문자열</span><span class="sxs-lookup"><span data-stu-id="3b488-320">String</span></span> |<span data-ttu-id="3b488-321">"CustomRole"로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-321">Set to "CustomRole."</span></span> |
| <span data-ttu-id="3b488-322">properties.permissions.actions</span><span class="sxs-lookup"><span data-stu-id="3b488-322">properties.permissions.actions</span></span> |<span data-ttu-id="3b488-323">예</span><span class="sxs-lookup"><span data-stu-id="3b488-323">Yes</span></span> |<span data-ttu-id="3b488-324">문자열[]</span><span class="sxs-lookup"><span data-stu-id="3b488-324">String[]</span></span> |<span data-ttu-id="3b488-325">업데이트된 사용자 지정 역할이 액세스 권한을 부여하는 작업을 지정하는 동작 문자열의 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-325">An array of action strings specifying the operations to which the updated custom role grants access.</span></span> |
| <span data-ttu-id="3b488-326">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="3b488-326">properties.permissions.notActions</span></span> |<span data-ttu-id="3b488-327">아니요</span><span class="sxs-lookup"><span data-stu-id="3b488-327">No</span></span> |<span data-ttu-id="3b488-328">문자열[]</span><span class="sxs-lookup"><span data-stu-id="3b488-328">String[]</span></span> |<span data-ttu-id="3b488-329">업데이트된 사용자 지정 역할이 권한을 부여하는 작업에서 제외할 작업을 지정하는 동작 문자열의 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-329">An array of action strings specifying the operations to exclude from the operations which the updated custom role grants.</span></span> |
| <span data-ttu-id="3b488-330">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="3b488-330">properties.assignableScopes</span></span> |<span data-ttu-id="3b488-331">예</span><span class="sxs-lookup"><span data-stu-id="3b488-331">Yes</span></span> |<span data-ttu-id="3b488-332">문자열[]</span><span class="sxs-lookup"><span data-stu-id="3b488-332">String[]</span></span> |<span data-ttu-id="3b488-333">업데이트된 사용자 지정 역할을 사용할 수 있는 범위의 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-333">An array of scopes in which the updated custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="3b488-334">응답</span><span class="sxs-lookup"><span data-stu-id="3b488-334">Response</span></span>
<span data-ttu-id="3b488-335">상태 코드: 201</span><span class="sxs-lookup"><span data-stu-id="3b488-335">Status code: 201</span></span>

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-18T00:10:51.4662695Z",
    "updatedOn": "2015-12-18T00:10:51.4662695Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7"
}

```

## <a name="delete-a-custom-role"></a><span data-ttu-id="3b488-336">사용자 지정 역할 삭제</span><span class="sxs-lookup"><span data-stu-id="3b488-336">Delete a Custom Role</span></span>
<span data-ttu-id="3b488-337">사용자 지정 역할을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-337">Delete a custom role.</span></span>

<span data-ttu-id="3b488-338">사용자 지정 역할을 삭제하려면 해당하는 모든 `AssignableScopes`에서 `Microsoft.Authorization/roleDefinitions/delete` 작업에 대한 액세스 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-338">To delete a custom role, you must have access to `Microsoft.Authorization/roleDefinitions/delete` operation on all the `AssignableScopes`.</span></span> <span data-ttu-id="3b488-339">기본 제공 역할의 경우 *소유자* 및 *사용자 액세스 관리자*에게만 이러한 작업의 권한이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-339">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="3b488-340">Azure 리소스에 대한 액세스 관리 및 역할 할당에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어](role-based-access-control-configure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b488-340">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="3b488-341">요청</span><span class="sxs-lookup"><span data-stu-id="3b488-341">Request</span></span>
<span data-ttu-id="3b488-342">다음 URI와 함께 **DELETE** 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-342">Use the **DELETE** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="3b488-343">URI 내에서 다음을 대체하여 요청을 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-343">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="3b488-344">*{scope}* 를 역할 정의를 삭제하려는 범위로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-344">Replace *{scope}* with the scope at which you wish to delete the role definition.</span></span> <span data-ttu-id="3b488-345">다음 예제에서는 서로 다른 수준에 대해 범위를 지정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-345">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="3b488-346">구독: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="3b488-346">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="3b488-347">리소스 그룹: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="3b488-347">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="3b488-348">리소스: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="3b488-348">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="3b488-349">*{role-definition-id}* 를 사용자 지정 역할의 GUID 역할 정의 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-349">Replace *{role-definition-id}* with the GUID role definition id of the custom role.</span></span>
3. <span data-ttu-id="3b488-350">*{api-version}* 을 2015-07-01로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3b488-350">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="3b488-351">응답</span><span class="sxs-lookup"><span data-stu-id="3b488-351">Response</span></span>
<span data-ttu-id="3b488-352">상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="3b488-352">Status code: 200</span></span>

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-16T00:07:02.9236555Z",
    "updatedOn": "2015-12-16T00:07:02.9236555Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/0bd62a70-e1b8-4e0b-a7c2-75cab365c95b",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "0bd62a70-e1b8-4e0b-a7c2-75cab365c95b"
}

```

## <a name="next-steps"></a><span data-ttu-id="3b488-353">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3b488-353">Next steps</span></span>

[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]
