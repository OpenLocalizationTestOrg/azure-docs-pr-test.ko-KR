---
title: "rest-Azure AD 액세스 제어 aaaRole 기반 | Microsoft Docs"
description: "Hello REST API로 역할 기반 액세스 제어 관리"
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
ms.openlocfilehash: ccd402fd4fe4583288076cac23753dd067694681
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control-with-hello-rest-api"></a><span data-ttu-id="004d7-103">Hello REST API로 역할 기반 액세스 제어 관리</span><span class="sxs-lookup"><span data-stu-id="004d7-103">Manage Role-Based Access Control with hello REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="004d7-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="004d7-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="004d7-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="004d7-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="004d7-106">REST API</span><span class="sxs-lookup"><span data-stu-id="004d7-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)

<span data-ttu-id="004d7-107">역할 기반 액세스 제어 (RBAC) hello Azure 포털에서에서 Azure 리소스 관리자 API 하면 쉽게 액세스 tooyour 구독 및 세분화 된 수준에서 리소스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-107">Role-Based Access Control (RBAC) in hello Azure portal and Azure Resource Manager API helps you manage access tooyour subscription and resources at a fine-grained level.</span></span> <span data-ttu-id="004d7-108">이 기능을 특정 범위에서 일부 역할 toothem 할당 하 여 Active Directory 사용자, 그룹 또는 서비스 사용자에 대 한 액세스를 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles toothem at a particular scope.</span></span>

## <a name="list-all-role-assignments"></a><span data-ttu-id="004d7-109">모든 역할 할당 나열</span><span class="sxs-lookup"><span data-stu-id="004d7-109">List all role assignments</span></span>
<span data-ttu-id="004d7-110">지정 된 hello에서 모든 hello 역할 할당 범위 및 subscopes 합니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-110">Lists all hello role assignments at hello specified scope and subscopes.</span></span>

<span data-ttu-id="004d7-111">toolist 역할 할당을 액세스할 수 있어야 너무`Microsoft.Authorization/roleAssignments/read` hello 범위에서 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-111">toolist role assignments, you must have access too`Microsoft.Authorization/roleAssignments/read` operation at hello scope.</span></span> <span data-ttu-id="004d7-112">모든 hello 기본 제공 역할 toothis 작업 액세스 권한이 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-112">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="004d7-113">Azure 리소스에 대한 액세스 관리 및 역할 할당에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어](role-based-access-control-configure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="004d7-113">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="004d7-114">요청</span><span class="sxs-lookup"><span data-stu-id="004d7-114">Request</span></span>
<span data-ttu-id="004d7-115">사용 하 여 hello **가져오기** URI 뒤 hello로 메서드:</span><span class="sxs-lookup"><span data-stu-id="004d7-115">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments?api-version={api-version}&$filter={filter}

<span data-ttu-id="004d7-116">Hello URI 내에서 다음 대체 toocustomize hello 요청 확인:</span><span class="sxs-lookup"><span data-stu-id="004d7-116">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="004d7-117">대체 *{scope}* hello 범위를 원하는 toolist hello 역할 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-117">Replace *{scope}* with hello scope for which you wish toolist hello role assignments.</span></span> <span data-ttu-id="004d7-118">다음 예제는 hello toospecify 서로 다른 수준에 대 한 범위를 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-118">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="004d7-119">구독: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="004d7-119">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="004d7-120">리소스 그룹: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="004d7-120">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="004d7-121">리소스: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="004d7-121">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="004d7-122">*{api-version}* 을 2015-07-01로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-122">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="004d7-123">대체 *{filter}* tooapply toofilter hello 역할 할당 목록을 원하는 hello 조건:</span><span class="sxs-lookup"><span data-stu-id="004d7-123">Replace *{filter}* with hello condition that you wish tooapply toofilter hello role assignment list:</span></span>

   * <span data-ttu-id="004d7-124">만 hello에 대 한 역할 할당 목록을 subscopes에서 hello 역할 할당을 포함 하지 않는 범위를 지정 합니다.`atScope()`</span><span class="sxs-lookup"><span data-stu-id="004d7-124">List role assignments for only hello specified scope, not including hello role assignments at subscopes: `atScope()`</span></span>    
   * <span data-ttu-id="004d7-125">특정 사용자, 그룹 또는 응용 프로그램에 대해서만 역할 할당 나열: `principalId%20eq%20'{objectId of user, group, or service principal}'`</span><span class="sxs-lookup"><span data-stu-id="004d7-125">List role assignments for a specific user, group, or application: `principalId%20eq%20'{objectId of user, group, or service principal}'`</span></span>  
   * <span data-ttu-id="004d7-126">그룹에서 상속된 역할 할당을 포함하여 특정 사용자에 대한 역할 할당 나열 | `assignedTo('{objectId of user}')`</span><span class="sxs-lookup"><span data-stu-id="004d7-126">List role assignments for a specific user, including ones inherited from groups | `assignedTo('{objectId of user}')`</span></span>

### <a name="response"></a><span data-ttu-id="004d7-127">응답</span><span class="sxs-lookup"><span data-stu-id="004d7-127">Response</span></span>
<span data-ttu-id="004d7-128">상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="004d7-128">Status code: 200</span></span>

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

## <a name="get-information-about-a-role-assignment"></a><span data-ttu-id="004d7-129">역할 할당에 대한 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="004d7-129">Get information about a role assignment</span></span>
<span data-ttu-id="004d7-130">Hello 역할 할당 id에서 지정한 단일 역할 할당에 대 한 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-130">Gets information about a single role assignment specified by hello role assignment identifier.</span></span>

<span data-ttu-id="004d7-131">역할 할당에 대 한 tooget 정보를 액세스할 수 있어야 너무`Microsoft.Authorization/roleAssignments/read` 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-131">tooget information about a role assignment, you must have access too`Microsoft.Authorization/roleAssignments/read` operation.</span></span> <span data-ttu-id="004d7-132">모든 hello 기본 제공 역할 toothis 작업 액세스 권한이 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-132">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="004d7-133">Azure 리소스에 대한 액세스 관리 및 역할 할당에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어](role-based-access-control-configure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="004d7-133">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="004d7-134">요청</span><span class="sxs-lookup"><span data-stu-id="004d7-134">Request</span></span>
<span data-ttu-id="004d7-135">사용 하 여 hello **가져오기** URI 뒤 hello로 메서드:</span><span class="sxs-lookup"><span data-stu-id="004d7-135">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="004d7-136">Hello URI 내에서 다음 대체 toocustomize hello 요청 확인:</span><span class="sxs-lookup"><span data-stu-id="004d7-136">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="004d7-137">대체 *{scope}* hello 범위를 원하는 toolist hello 역할 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-137">Replace *{scope}* with hello scope for which you wish toolist hello role assignments.</span></span> <span data-ttu-id="004d7-138">다음 예제는 hello toospecify 서로 다른 수준에 대 한 범위를 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-138">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="004d7-139">구독: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="004d7-139">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="004d7-140">리소스 그룹: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="004d7-140">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="004d7-141">리소스: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="004d7-141">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="004d7-142">대체 *{역할 할당 id}* hello 역할 할당의 hello GUID 식별자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-142">Replace *{role-assignment-id}* with hello GUID identifier of hello role assignment.</span></span>
3. <span data-ttu-id="004d7-143">*{api-version}* 을 2015-07-01로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-143">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="004d7-144">응답</span><span class="sxs-lookup"><span data-stu-id="004d7-144">Response</span></span>
<span data-ttu-id="004d7-145">상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="004d7-145">Status code: 200</span></span>

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

## <a name="create-a-role-assignment"></a><span data-ttu-id="004d7-146">역할 할당 만들기</span><span class="sxs-lookup"><span data-stu-id="004d7-146">Create a Role Assignment</span></span>
<span data-ttu-id="004d7-147">역할 만들기 hello 지정한 보안 주체 권한을 부여 hello 지정 된 역할에 대 한 할당 hello에 범위를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-147">Create a role assignment at hello specified scope for hello specified principal granting hello specified role.</span></span>

<span data-ttu-id="004d7-148">역할 할당 toocreate 권한이 너무`Microsoft.Authorization/roleAssignments/write` 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-148">toocreate a role assignment, you must have access too`Microsoft.Authorization/roleAssignments/write` operation.</span></span> <span data-ttu-id="004d7-149">Hello 기본 제공 역할 중만 *소유자* 및 *사용자 액세스 관리자에 게* 액세스 toothis 작업 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-149">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="004d7-150">Azure 리소스에 대한 액세스 관리 및 역할 할당에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어](role-based-access-control-configure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="004d7-150">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="004d7-151">요청</span><span class="sxs-lookup"><span data-stu-id="004d7-151">Request</span></span>
<span data-ttu-id="004d7-152">사용 하 여 hello **배치** URI 뒤 hello로 메서드:</span><span class="sxs-lookup"><span data-stu-id="004d7-152">Use hello **PUT** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="004d7-153">Hello URI 내에서 다음 대체 toocustomize hello 요청 확인:</span><span class="sxs-lookup"><span data-stu-id="004d7-153">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="004d7-154">대체 *{scope}* hello 범위를 원하는 toocreate hello 역할 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-154">Replace *{scope}* with hello scope at which you wish toocreate hello role assignments.</span></span> <span data-ttu-id="004d7-155">모든 자식 범위 상속 hello 부모 범위에서 역할 할당을 만들 때 동일한 역할 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-155">When you create a role assignment at a parent scope, all child scopes inherit hello same role assignment.</span></span> <span data-ttu-id="004d7-156">다음 예제는 hello toospecify 서로 다른 수준에 대 한 범위를 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-156">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="004d7-157">구독: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="004d7-157">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="004d7-158">리소스 그룹: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="004d7-158">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>   
   * <span data-ttu-id="004d7-159">리소스: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="004d7-159">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="004d7-160">대체 *{역할 할당 id}* hello 새 역할 할당의 GUID 식별자 hello 새 GUID를 가진 됩니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-160">Replace *{role-assignment-id}* with a new GUID, which becomes hello GUID identifier of hello new role assignment.</span></span>
3. <span data-ttu-id="004d7-161">*{api-version}* 을 2015-07-01로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-161">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="004d7-162">Hello 요청 본문에 대 한 형식에 따라 hello에 hello 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-162">For hello request body, provide hello values in hello following format:</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b"
  }
}

```

| <span data-ttu-id="004d7-163">요소 이름</span><span class="sxs-lookup"><span data-stu-id="004d7-163">Element Name</span></span> | <span data-ttu-id="004d7-164">필수</span><span class="sxs-lookup"><span data-stu-id="004d7-164">Required</span></span> | <span data-ttu-id="004d7-165">형식</span><span class="sxs-lookup"><span data-stu-id="004d7-165">Type</span></span> | <span data-ttu-id="004d7-166">설명</span><span class="sxs-lookup"><span data-stu-id="004d7-166">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="004d7-167">roleDefinitionId</span><span class="sxs-lookup"><span data-stu-id="004d7-167">roleDefinitionId</span></span> |<span data-ttu-id="004d7-168">예</span><span class="sxs-lookup"><span data-stu-id="004d7-168">Yes</span></span> |<span data-ttu-id="004d7-169">문자열</span><span class="sxs-lookup"><span data-stu-id="004d7-169">String</span></span> |<span data-ttu-id="004d7-170">hello 역할의 hello 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-170">hello identifier of hello role.</span></span> <span data-ttu-id="004d7-171">hello hello 식별자의 형식은 다음과 같습니다.`{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span><span class="sxs-lookup"><span data-stu-id="004d7-171">hello format of hello identifier is: `{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span></span> |
| <span data-ttu-id="004d7-172">principalId</span><span class="sxs-lookup"><span data-stu-id="004d7-172">principalId</span></span> |<span data-ttu-id="004d7-173">예</span><span class="sxs-lookup"><span data-stu-id="004d7-173">Yes</span></span> |<span data-ttu-id="004d7-174">문자열</span><span class="sxs-lookup"><span data-stu-id="004d7-174">String</span></span> |<span data-ttu-id="004d7-175">hello Azure AD 보안 주체 (사용자, 그룹 또는 서비스 사용자)의 objectId toowhich hello 역할 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-175">objectId of hello Azure AD principal (user, group, or service principal) toowhich hello role is assigned.</span></span> |

### <a name="response"></a><span data-ttu-id="004d7-176">응답</span><span class="sxs-lookup"><span data-stu-id="004d7-176">Response</span></span>
<span data-ttu-id="004d7-177">상태 코드: 201</span><span class="sxs-lookup"><span data-stu-id="004d7-177">Status code: 201</span></span>

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

## <a name="delete-a-role-assignment"></a><span data-ttu-id="004d7-178">역할 할당 삭제</span><span class="sxs-lookup"><span data-stu-id="004d7-178">Delete a Role Assignment</span></span>
<span data-ttu-id="004d7-179">Delete hello에서 역할 할당 범위를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-179">Delete a role assignment at hello specified scope.</span></span>

<span data-ttu-id="004d7-180">역할 할당 toodelete 있어야 액세스 toohello `Microsoft.Authorization/roleAssignments/delete` 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-180">toodelete a role assignment, you must have access toohello `Microsoft.Authorization/roleAssignments/delete` operation.</span></span> <span data-ttu-id="004d7-181">Hello 기본 제공 역할 중만 *소유자* 및 *사용자 액세스 관리자에 게* 액세스 toothis 작업 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-181">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="004d7-182">Azure 리소스에 대한 액세스 관리 및 역할 할당에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어](role-based-access-control-configure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="004d7-182">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="004d7-183">요청</span><span class="sxs-lookup"><span data-stu-id="004d7-183">Request</span></span>
<span data-ttu-id="004d7-184">사용 하 여 hello **삭제** URI 뒤 hello로 메서드:</span><span class="sxs-lookup"><span data-stu-id="004d7-184">Use hello **DELETE** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="004d7-185">Hello URI 내에서 다음 대체 toocustomize hello 요청 확인:</span><span class="sxs-lookup"><span data-stu-id="004d7-185">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="004d7-186">대체 *{scope}* hello 범위를 원하는 toocreate hello 역할 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-186">Replace *{scope}* with hello scope at which you wish toocreate hello role assignments.</span></span> <span data-ttu-id="004d7-187">다음 예제는 hello toospecify 서로 다른 수준에 대 한 범위를 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-187">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="004d7-188">구독: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="004d7-188">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="004d7-189">리소스 그룹: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="004d7-189">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="004d7-190">리소스: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="004d7-190">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="004d7-191">대체 *{역할 할당 id}* hello 역할 할당 id GUID 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-191">Replace *{role-assignment-id}* with hello role assignment id GUID.</span></span>
3. <span data-ttu-id="004d7-192">*{api-version}* 을 2015-07-01로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-192">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="004d7-193">응답</span><span class="sxs-lookup"><span data-stu-id="004d7-193">Response</span></span>
<span data-ttu-id="004d7-194">상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="004d7-194">Status code: 200</span></span>

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

## <a name="list-all-roles"></a><span data-ttu-id="004d7-195">모든 역할 나열</span><span class="sxs-lookup"><span data-stu-id="004d7-195">List all Roles</span></span>
<span data-ttu-id="004d7-196">지정 된 hello에 대 한 할당에 사용할 수 있는 모든 hello 역할이 나열 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-196">Lists all hello roles that are available for assignment at hello specified scope.</span></span>

<span data-ttu-id="004d7-197">toolist 역할 권한이 너무`Microsoft.Authorization/roleDefinitions/read` hello 범위에서 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-197">toolist roles, you must have access too`Microsoft.Authorization/roleDefinitions/read` operation at hello scope.</span></span> <span data-ttu-id="004d7-198">모든 hello 기본 제공 역할 toothis 작업 액세스 권한이 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-198">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="004d7-199">Azure 리소스에 대한 액세스 관리 및 역할 할당에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어](role-based-access-control-configure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="004d7-199">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="004d7-200">요청</span><span class="sxs-lookup"><span data-stu-id="004d7-200">Request</span></span>
<span data-ttu-id="004d7-201">사용 하 여 hello **가져오기** URI 뒤 hello로 메서드:</span><span class="sxs-lookup"><span data-stu-id="004d7-201">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions?api-version={api-version}&$filter={filter}

<span data-ttu-id="004d7-202">Hello URI 내에서 다음 대체 toocustomize hello 요청 확인:</span><span class="sxs-lookup"><span data-stu-id="004d7-202">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="004d7-203">대체 *{scope}* hello 범위를 원하는 toolist hello 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-203">Replace *{scope}* with hello scope for which you wish toolist hello roles.</span></span> <span data-ttu-id="004d7-204">다음 예제는 hello toospecify 서로 다른 수준에 대 한 범위를 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-204">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="004d7-205">구독: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="004d7-205">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="004d7-206">리소스 그룹: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="004d7-206">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="004d7-207">리소스: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="004d7-207">Resource /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="004d7-208">*{api-version}* 을 2015-07-01로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-208">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="004d7-209">대체 *{filter}* 역할 목록이 toofilter hello tooapply 한다고 hello 조건:</span><span class="sxs-lookup"><span data-stu-id="004d7-209">Replace *{filter}* with hello condition that you wish tooapply toofilter hello list of roles:</span></span>

   * <span data-ttu-id="004d7-210">할당 hello에 사용할 수 있는 목록 역할 범위 및 해당 하위 범위 중 하나를 지정:`atScopeAndBelow()`</span><span class="sxs-lookup"><span data-stu-id="004d7-210">List roles available for assignment at hello specified scope and any of its child scopes: `atScopeAndBelow()`</span></span>
   * <span data-ttu-id="004d7-211">정확한 표시 이름을 사용하여 역할 검색: `roleName%20eq%20'{role-display-name}'`</span><span class="sxs-lookup"><span data-stu-id="004d7-211">Search for a role using exact display name: `roleName%20eq%20'{role-display-name}'`.</span></span> <span data-ttu-id="004d7-212">Hello 역할의 정확한 표시 이름으로 hello hello URL 인코딩 형식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-212">Use hello URL encoded form of hello exact display name of hello role.</span></span> <span data-ttu-id="004d7-213">예를 들어, `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span><span class="sxs-lookup"><span data-stu-id="004d7-213">For instance, `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span></span>

### <a name="response"></a><span data-ttu-id="004d7-214">응답</span><span class="sxs-lookup"><span data-stu-id="004d7-214">Response</span></span>
<span data-ttu-id="004d7-215">상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="004d7-215">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access toothem, and not hello virtual network or storage account they\u2019re connected to.",
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

## <a name="get-information-about-a-role"></a><span data-ttu-id="004d7-216">역할에 대한 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="004d7-216">Get information about a Role</span></span>
<span data-ttu-id="004d7-217">Hello 역할 정의 id에서 지정한 단일 역할에 대 한 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-217">Gets information about a single role specified by hello role definition identifier.</span></span> <span data-ttu-id="004d7-218">표시 이름을 사용 하 여 단일 역할에 대 한 tooget 정보 참조 [모든 역할을 나열](role-based-access-control-manage-access-rest.md#list-all-roles)합니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-218">tooget information about a single role using its display name, see [List all roles](role-based-access-control-manage-access-rest.md#list-all-roles).</span></span>

<span data-ttu-id="004d7-219">역할에 대 한 tooget 정보를 액세스할 수 있어야 너무`Microsoft.Authorization/roleDefinitions/read` 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-219">tooget information about a role, you must have access too`Microsoft.Authorization/roleDefinitions/read` operation.</span></span> <span data-ttu-id="004d7-220">모든 hello 기본 제공 역할 toothis 작업 액세스 권한이 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-220">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="004d7-221">Azure 리소스에 대한 액세스 관리 및 역할 할당에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어](role-based-access-control-configure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="004d7-221">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="004d7-222">요청</span><span class="sxs-lookup"><span data-stu-id="004d7-222">Request</span></span>
<span data-ttu-id="004d7-223">사용 하 여 hello **가져오기** URI 뒤 hello로 메서드:</span><span class="sxs-lookup"><span data-stu-id="004d7-223">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="004d7-224">Hello URI 내에서 다음 대체 toocustomize hello 요청 확인:</span><span class="sxs-lookup"><span data-stu-id="004d7-224">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="004d7-225">대체 *{scope}* hello 범위를 원하는 toolist hello 역할 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-225">Replace *{scope}* with hello scope for which you wish toolist hello role assignments.</span></span> <span data-ttu-id="004d7-226">다음 예제는 hello toospecify 서로 다른 수준에 대 한 범위를 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-226">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="004d7-227">구독: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="004d7-227">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="004d7-228">리소스 그룹: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="004d7-228">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="004d7-229">리소스: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="004d7-229">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="004d7-230">대체 *{역할 정의 id}* hello 역할 정의의 hello GUID 식별자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-230">Replace *{role-definition-id}* with hello GUID identifier of hello role definition.</span></span>
3. <span data-ttu-id="004d7-231">*{api-version}* 을 2015-07-01로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-231">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="004d7-232">응답</span><span class="sxs-lookup"><span data-stu-id="004d7-232">Response</span></span>
<span data-ttu-id="004d7-233">상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="004d7-233">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access toothem, and not hello virtual network or storage account they\u2019re connected to.",
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

## <a name="create-a-custom-role"></a><span data-ttu-id="004d7-234">사용자 지정 역할 만들기</span><span class="sxs-lookup"><span data-stu-id="004d7-234">Create a Custom Role</span></span>
<span data-ttu-id="004d7-235">사용자 지정 역할을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-235">Create a custom role.</span></span>

<span data-ttu-id="004d7-236">사용자 지정 역할 toocreate 권한이 너무`Microsoft.Authorization/roleDefinitions/write` 모든 hello에 대 한 작업이 `AssignableScopes`합니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-236">toocreate a custom role, you must have access too`Microsoft.Authorization/roleDefinitions/write` operation on all hello `AssignableScopes`.</span></span> <span data-ttu-id="004d7-237">Hello 기본 제공 역할 중만 *소유자* 및 *사용자 액세스 관리자에 게* 액세스 toothis 작업 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-237">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="004d7-238">Azure 리소스에 대한 액세스 관리 및 역할 할당에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어](role-based-access-control-configure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="004d7-238">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="004d7-239">요청</span><span class="sxs-lookup"><span data-stu-id="004d7-239">Request</span></span>
<span data-ttu-id="004d7-240">사용 하 여 hello **배치** URI 뒤 hello로 메서드:</span><span class="sxs-lookup"><span data-stu-id="004d7-240">Use hello **PUT** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="004d7-241">Hello URI 내에서 다음 대체 toocustomize hello 요청 확인:</span><span class="sxs-lookup"><span data-stu-id="004d7-241">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="004d7-242">대체 *{scope}* hello로 첫 번째 *AssignableScope* hello 사용자 지정 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-242">Replace *{scope}* with hello first *AssignableScope* of hello custom role.</span></span> <span data-ttu-id="004d7-243">다음 예제는 hello toospecify 서로 다른 수준에 대 한 범위를 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-243">hello following examples show how toospecify hello scope for different levels.</span></span>

   * <span data-ttu-id="004d7-244">구독: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="004d7-244">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="004d7-245">리소스 그룹: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="004d7-245">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="004d7-246">리소스: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="004d7-246">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="004d7-247">대체 *{역할 정의 id}* hello GUID 식별자 hello 새 사용자 지정 역할의 새 GUID를 가진 됩니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-247">Replace *{role-definition-id}* with a new GUID, which becomes hello GUID identifier of hello new custom role.</span></span>
3. <span data-ttu-id="004d7-248">*{api-version}* 을 2015-07-01로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-248">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="004d7-249">Hello 요청 본문에 대 한 형식에 따라 hello에 hello 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-249">For hello request body, provide hello values in hello following format:</span></span>

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

| <span data-ttu-id="004d7-250">요소 이름</span><span class="sxs-lookup"><span data-stu-id="004d7-250">Element Name</span></span> | <span data-ttu-id="004d7-251">필수</span><span class="sxs-lookup"><span data-stu-id="004d7-251">Required</span></span> | <span data-ttu-id="004d7-252">형식</span><span class="sxs-lookup"><span data-stu-id="004d7-252">Type</span></span> | <span data-ttu-id="004d7-253">설명</span><span class="sxs-lookup"><span data-stu-id="004d7-253">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="004d7-254">name</span><span class="sxs-lookup"><span data-stu-id="004d7-254">name</span></span> |<span data-ttu-id="004d7-255">예</span><span class="sxs-lookup"><span data-stu-id="004d7-255">Yes</span></span> |<span data-ttu-id="004d7-256">문자열</span><span class="sxs-lookup"><span data-stu-id="004d7-256">String</span></span> |<span data-ttu-id="004d7-257">사용자 지정 역할 hello의 GUID 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-257">GUID identifier of hello custom role.</span></span> |
| <span data-ttu-id="004d7-258">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="004d7-258">properties.roleName</span></span> |<span data-ttu-id="004d7-259">예</span><span class="sxs-lookup"><span data-stu-id="004d7-259">Yes</span></span> |<span data-ttu-id="004d7-260">문자열</span><span class="sxs-lookup"><span data-stu-id="004d7-260">String</span></span> |<span data-ttu-id="004d7-261">Hello 사용자 지정 역할의 표시 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-261">Display name of hello custom role.</span></span> <span data-ttu-id="004d7-262">최대 128자입니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-262">Maximum size 128 characters.</span></span> |
| <span data-ttu-id="004d7-263">properties.description</span><span class="sxs-lookup"><span data-stu-id="004d7-263">properties.description</span></span> |<span data-ttu-id="004d7-264">아니요</span><span class="sxs-lookup"><span data-stu-id="004d7-264">No</span></span> |<span data-ttu-id="004d7-265">문자열</span><span class="sxs-lookup"><span data-stu-id="004d7-265">String</span></span> |<span data-ttu-id="004d7-266">Hello 사용자 지정 역할의 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-266">Description of hello custom role.</span></span> <span data-ttu-id="004d7-267">최대 1024자입니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-267">Maximum size 1024 characters.</span></span> |
| <span data-ttu-id="004d7-268">properties.type</span><span class="sxs-lookup"><span data-stu-id="004d7-268">properties.type</span></span> |<span data-ttu-id="004d7-269">예</span><span class="sxs-lookup"><span data-stu-id="004d7-269">Yes</span></span> |<span data-ttu-id="004d7-270">문자열</span><span class="sxs-lookup"><span data-stu-id="004d7-270">String</span></span> |<span data-ttu-id="004d7-271">도 "CustomRole."</span><span class="sxs-lookup"><span data-stu-id="004d7-271">Set too"CustomRole."</span></span> |
| <span data-ttu-id="004d7-272">properties.permissions.actions</span><span class="sxs-lookup"><span data-stu-id="004d7-272">properties.permissions.actions</span></span> |<span data-ttu-id="004d7-273">예</span><span class="sxs-lookup"><span data-stu-id="004d7-273">Yes</span></span> |<span data-ttu-id="004d7-274">문자열[]</span><span class="sxs-lookup"><span data-stu-id="004d7-274">String[]</span></span> |<span data-ttu-id="004d7-275">동작의 배열을 지정 하 여 hello 작업 hello 사용자 지정 역할에 의해 부여 된 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-275">An array of action strings specifying hello operations granted by hello custom role.</span></span> |
| <span data-ttu-id="004d7-276">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="004d7-276">properties.permissions.notActions</span></span> |<span data-ttu-id="004d7-277">아니요</span><span class="sxs-lookup"><span data-stu-id="004d7-277">No</span></span> |<span data-ttu-id="004d7-278">문자열[]</span><span class="sxs-lookup"><span data-stu-id="004d7-278">String[]</span></span> |<span data-ttu-id="004d7-279">Hello 작업 tooexclude hello 사용자 지정 역할에 의해 부여 된 hello 작업에서 지정 하는 동작 문자열의 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-279">An array of action strings specifying hello operations tooexclude from hello operations granted by hello custom role.</span></span> |
| <span data-ttu-id="004d7-280">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="004d7-280">properties.assignableScopes</span></span> |<span data-ttu-id="004d7-281">예</span><span class="sxs-lookup"><span data-stu-id="004d7-281">Yes</span></span> |<span data-ttu-id="004d7-282">문자열[]</span><span class="sxs-lookup"><span data-stu-id="004d7-282">String[]</span></span> |<span data-ttu-id="004d7-283">배열 범위는 hello 사용자 지정 역할을 사용할 수입니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-283">An array of scopes in which hello custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="004d7-284">응답</span><span class="sxs-lookup"><span data-stu-id="004d7-284">Response</span></span>
<span data-ttu-id="004d7-285">상태 코드: 201</span><span class="sxs-lookup"><span data-stu-id="004d7-285">Status code: 201</span></span>

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

## <a name="update-a-custom-role"></a><span data-ttu-id="004d7-286">사용자 지정 역할 업데이트</span><span class="sxs-lookup"><span data-stu-id="004d7-286">Update a Custom Role</span></span>
<span data-ttu-id="004d7-287">사용자 지정 역할을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-287">Modify a custom role.</span></span>

<span data-ttu-id="004d7-288">사용자 지정 역할 toomodify 권한이 너무`Microsoft.Authorization/roleDefinitions/write` 모든 hello에 대 한 작업이 `AssignableScopes`합니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-288">toomodify a custom role, you must have access too`Microsoft.Authorization/roleDefinitions/write` operation on all hello `AssignableScopes`.</span></span> <span data-ttu-id="004d7-289">Hello 기본 제공 역할 중만 *소유자* 및 *사용자 액세스 관리자에 게* 액세스 toothis 작업 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-289">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="004d7-290">Azure 리소스에 대한 액세스 관리 및 역할 할당에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어](role-based-access-control-configure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="004d7-290">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="004d7-291">요청</span><span class="sxs-lookup"><span data-stu-id="004d7-291">Request</span></span>
<span data-ttu-id="004d7-292">사용 하 여 hello **배치** URI 뒤 hello로 메서드:</span><span class="sxs-lookup"><span data-stu-id="004d7-292">Use hello **PUT** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="004d7-293">Hello URI 내에서 다음 대체 toocustomize hello 요청 확인:</span><span class="sxs-lookup"><span data-stu-id="004d7-293">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="004d7-294">대체 *{scope}* hello로 첫 번째 *AssignableScope* hello 사용자 지정 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-294">Replace *{scope}* with hello first *AssignableScope* of hello custom role.</span></span> <span data-ttu-id="004d7-295">다음 예제는 hello toospecify 서로 다른 수준에 대 한 범위를 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-295">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="004d7-296">구독: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="004d7-296">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="004d7-297">리소스 그룹: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="004d7-297">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="004d7-298">리소스: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="004d7-298">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="004d7-299">대체 *{역할 정의 id}* hello 사용자 지정 역할의 hello GUID 식별자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-299">Replace *{role-definition-id}* with hello GUID identifier of hello custom role.</span></span>
3. <span data-ttu-id="004d7-300">*{api-version}* 을 2015-07-01로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-300">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="004d7-301">Hello 요청 본문에 대 한 형식에 따라 hello에 hello 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-301">For hello request body, provide hello values in hello following format:</span></span>

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

| <span data-ttu-id="004d7-302">요소 이름</span><span class="sxs-lookup"><span data-stu-id="004d7-302">Element Name</span></span> | <span data-ttu-id="004d7-303">필수</span><span class="sxs-lookup"><span data-stu-id="004d7-303">Required</span></span> | <span data-ttu-id="004d7-304">형식</span><span class="sxs-lookup"><span data-stu-id="004d7-304">Type</span></span> | <span data-ttu-id="004d7-305">설명</span><span class="sxs-lookup"><span data-stu-id="004d7-305">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="004d7-306">name</span><span class="sxs-lookup"><span data-stu-id="004d7-306">name</span></span> |<span data-ttu-id="004d7-307">예</span><span class="sxs-lookup"><span data-stu-id="004d7-307">Yes</span></span> |<span data-ttu-id="004d7-308">문자열</span><span class="sxs-lookup"><span data-stu-id="004d7-308">String</span></span> |<span data-ttu-id="004d7-309">사용자 지정 역할 hello의 GUID 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-309">GUID identifier of hello custom role.</span></span> |
| <span data-ttu-id="004d7-310">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="004d7-310">properties.roleName</span></span> |<span data-ttu-id="004d7-311">예</span><span class="sxs-lookup"><span data-stu-id="004d7-311">Yes</span></span> |<span data-ttu-id="004d7-312">문자열</span><span class="sxs-lookup"><span data-stu-id="004d7-312">String</span></span> |<span data-ttu-id="004d7-313">사용자 지정 역할을 업데이트 하는 hello의 표시 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-313">Display name of hello updated custom role.</span></span> |
| <span data-ttu-id="004d7-314">properties.description</span><span class="sxs-lookup"><span data-stu-id="004d7-314">properties.description</span></span> |<span data-ttu-id="004d7-315">아니요</span><span class="sxs-lookup"><span data-stu-id="004d7-315">No</span></span> |<span data-ttu-id="004d7-316">문자열</span><span class="sxs-lookup"><span data-stu-id="004d7-316">String</span></span> |<span data-ttu-id="004d7-317">Hello 설명 사용자 지정 역할을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-317">Description of hello updated custom role.</span></span> |
| <span data-ttu-id="004d7-318">properties.type</span><span class="sxs-lookup"><span data-stu-id="004d7-318">properties.type</span></span> |<span data-ttu-id="004d7-319">예</span><span class="sxs-lookup"><span data-stu-id="004d7-319">Yes</span></span> |<span data-ttu-id="004d7-320">문자열</span><span class="sxs-lookup"><span data-stu-id="004d7-320">String</span></span> |<span data-ttu-id="004d7-321">도 "CustomRole."</span><span class="sxs-lookup"><span data-stu-id="004d7-321">Set too"CustomRole."</span></span> |
| <span data-ttu-id="004d7-322">properties.permissions.actions</span><span class="sxs-lookup"><span data-stu-id="004d7-322">properties.permissions.actions</span></span> |<span data-ttu-id="004d7-323">예</span><span class="sxs-lookup"><span data-stu-id="004d7-323">Yes</span></span> |<span data-ttu-id="004d7-324">문자열[]</span><span class="sxs-lookup"><span data-stu-id="004d7-324">String[]</span></span> |<span data-ttu-id="004d7-325">Hello 작업 toowhich hello를 지정 하는 동작 문자열의 배열 액세스를 부여 하는 사용자 지정 역할을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-325">An array of action strings specifying hello operations toowhich hello updated custom role grants access.</span></span> |
| <span data-ttu-id="004d7-326">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="004d7-326">properties.permissions.notActions</span></span> |<span data-ttu-id="004d7-327">아니요</span><span class="sxs-lookup"><span data-stu-id="004d7-327">No</span></span> |<span data-ttu-id="004d7-328">문자열[]</span><span class="sxs-lookup"><span data-stu-id="004d7-328">String[]</span></span> |<span data-ttu-id="004d7-329">동작의 배열을 지정 하 여 hello 작업 tooexclude는 hello 부여 사용자 지정 역할을 업데이트 하는 hello 작업에서 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-329">An array of action strings specifying hello operations tooexclude from hello operations which hello updated custom role grants.</span></span> |
| <span data-ttu-id="004d7-330">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="004d7-330">properties.assignableScopes</span></span> |<span data-ttu-id="004d7-331">예</span><span class="sxs-lookup"><span data-stu-id="004d7-331">Yes</span></span> |<span data-ttu-id="004d7-332">문자열[]</span><span class="sxs-lookup"><span data-stu-id="004d7-332">String[]</span></span> |<span data-ttu-id="004d7-333">배열 범위는 hello 업데이트 된 사용자 지정 역할을 사용할 수입니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-333">An array of scopes in which hello updated custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="004d7-334">응답</span><span class="sxs-lookup"><span data-stu-id="004d7-334">Response</span></span>
<span data-ttu-id="004d7-335">상태 코드: 201</span><span class="sxs-lookup"><span data-stu-id="004d7-335">Status code: 201</span></span>

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

## <a name="delete-a-custom-role"></a><span data-ttu-id="004d7-336">사용자 지정 역할 삭제</span><span class="sxs-lookup"><span data-stu-id="004d7-336">Delete a Custom Role</span></span>
<span data-ttu-id="004d7-337">사용자 지정 역할을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-337">Delete a custom role.</span></span>

<span data-ttu-id="004d7-338">사용자 지정 역할 toodelete 권한이 너무`Microsoft.Authorization/roleDefinitions/delete` 모든 hello에 대 한 작업이 `AssignableScopes`합니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-338">toodelete a custom role, you must have access too`Microsoft.Authorization/roleDefinitions/delete` operation on all hello `AssignableScopes`.</span></span> <span data-ttu-id="004d7-339">Hello 기본 제공 역할 중만 *소유자* 및 *사용자 액세스 관리자에 게* 액세스 toothis 작업 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-339">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="004d7-340">Azure 리소스에 대한 액세스 관리 및 역할 할당에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어](role-based-access-control-configure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="004d7-340">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="004d7-341">요청</span><span class="sxs-lookup"><span data-stu-id="004d7-341">Request</span></span>
<span data-ttu-id="004d7-342">사용 하 여 hello **삭제** URI 뒤 hello로 메서드:</span><span class="sxs-lookup"><span data-stu-id="004d7-342">Use hello **DELETE** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="004d7-343">Hello URI 내에서 다음 대체 toocustomize hello 요청 확인:</span><span class="sxs-lookup"><span data-stu-id="004d7-343">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="004d7-344">대체 *{scope}* hello 범위 원하는 toodelete hello 역할 정의입니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-344">Replace *{scope}* with hello scope at which you wish toodelete hello role definition.</span></span> <span data-ttu-id="004d7-345">다음 예제는 hello toospecify 서로 다른 수준에 대 한 범위를 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-345">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="004d7-346">구독: /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="004d7-346">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="004d7-347">리소스 그룹: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="004d7-347">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="004d7-348">리소스: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="004d7-348">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="004d7-349">대체 *{역할 정의 id}* hello hello 사용자 지정 역할의 역할 정의 id GUID 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-349">Replace *{role-definition-id}* with hello GUID role definition id of hello custom role.</span></span>
3. <span data-ttu-id="004d7-350">*{api-version}* 을 2015-07-01로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="004d7-350">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="004d7-351">응답</span><span class="sxs-lookup"><span data-stu-id="004d7-351">Response</span></span>
<span data-ttu-id="004d7-352">상태 코드: 200</span><span class="sxs-lookup"><span data-stu-id="004d7-352">Status code: 200</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="004d7-353">다음 단계</span><span class="sxs-lookup"><span data-stu-id="004d7-353">Next steps</span></span>

[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]
