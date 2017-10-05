---
title: "테넌트 관리자 권한 상승 액세스 - Azure AD | Microsoft Docs"
description: "이 항목에서는 역할 기반 액세스 제어(RBAC)에 대한 기본 제공 역할에 대해 설명합니다."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
editor: rqureshi
ms.assetid: b547c5a5-2da2-4372-9938-481cb962d2d6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andredm
ms.openlocfilehash: bf64a92b359a6f68d84fa5ee17eda64ed6371990
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="elevate-access-as-a-tenant-admin-with-role-based-access-control"></a><span data-ttu-id="1387b-103">역할 기반 액세스 제어를 사용하여 테넌트 관리자로 액세스 권한 상승</span><span class="sxs-lookup"><span data-stu-id="1387b-103">Elevate access as a tenant admin with Role-Based Access Control</span></span>

<span data-ttu-id="1387b-104">역할 기반 액세스 제어를 통해 테넌트 관리자가 액세스에서 임시 권한이 상승되어 평소보다 높은 수준의 사용 권한을 부여받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1387b-104">Role-based Access Control helps tenant administrators get temporary elevations in access so that they can grant higher permissions than normal.</span></span> <span data-ttu-id="1387b-105">테넌트 관리자는 필요할 때 사용자 액세스 관리자 역할로 스스로의 권한을 높일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1387b-105">A tenant admin can elevate herself to the User Access Administrator role when needed.</span></span> <span data-ttu-id="1387b-106">해당 역할은 테넌트 관리자 사용 권한을 주어 "/" 범위에서 자신 또는 다른 사용자에게 역할을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="1387b-106">That role gives the tenant admin permissions to grant herself or others roles at the "/" scope.</span></span>

<span data-ttu-id="1387b-107">이 기능은 테넌트 관리자가 조직에 있는 모든 구독을 확인할 수 있도록 하기 때문에 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="1387b-107">This feature is important because it allows the tenant admin to see all the subscriptions that exist in an organization.</span></span> <span data-ttu-id="1387b-108">또한 자동화 앱(예: 송장 발행 및 감사)에서 모든 구독에 액세스하여 조직의 대금 청구 또는 자산 관리 상태를 정확하게 볼 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="1387b-108">It also allows for automation apps (like invoicing and auditing) to access all the subscriptions and provide an accurate view of the state of the organization for billing or asset management.</span></span>  

## <a name="how-to-use-elevateaccess-to-give-tenant-access"></a><span data-ttu-id="1387b-109">elevateAccess를 사용하여 테넌트 액세스 권한을 부여하는 방법</span><span class="sxs-lookup"><span data-stu-id="1387b-109">How to use elevateAccess to give tenant access</span></span>

<span data-ttu-id="1387b-110">기본 프로세스는 다음 단계로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="1387b-110">The basic process works with the following steps:</span></span>

1. <span data-ttu-id="1387b-111">REST를 사용하여 *elevateAccess*를 호출하면 "/" 범위에서 사용자 액세스 관리자 역할 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="1387b-111">Using REST, call *elevateAccess*, which grants you the User Access Administrator role at "/" scope.</span></span>

    ```
    POST https://management.azure.com/providers/Microsoft.Authorization/elevateAccess?api-version=2016-07-01
    ```

2. <span data-ttu-id="1387b-112">모든 범위의 모든 역할을 할당하는 [역할 할당](/rest/api/authorization/roleassignments)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1387b-112">Create a [role assignment](/rest/api/authorization/roleassignments) to assign any role at any scope.</span></span> <span data-ttu-id="1387b-113">다음 예제에서는 "/" 범위에서 읽기 권한자 역할을 할당하는 속성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1387b-113">The following example shows the properties for assigning the Reader role at "/" scope:</span></span>

    ```
    { "properties":{
    "roleDefinitionId": "providers/Microsoft.Authorization/roleDefinitions/acdd72a7338548efbd42f606fba81ae7",
    "principalId": "cbc5e050-d7cd-4310-813b-4870be8ef5bb",
    "scope": "/"
    },
    "id": "providers/Microsoft.Authorization/roleAssignments/64736CA0-56D7-4A94-A551-973C2FE7888B",
    "type": "Microsoft.Authorization/roleAssignments",
    "name": "64736CA0-56D7-4A94-A551-973C2FE7888B"
    }
    ```

3. <span data-ttu-id="1387b-114">사용자 액세스 관리자인 경우 "/" 범위에서 역할 할당을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1387b-114">While a User Access Admin, you can also delete role assignments at "/" scope.</span></span>

4. <span data-ttu-id="1387b-115">다시 필요할 때까지 사용자 액세스 관리자 권한을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="1387b-115">Revoke your User Access Admin privileges until they're needed again.</span></span>


## <a name="how-to-undo-the-elevateaccess-action"></a><span data-ttu-id="1387b-116">elevateAccess 작업을 취소하는 방법</span><span class="sxs-lookup"><span data-stu-id="1387b-116">How to undo the elevateAccess action</span></span>

<span data-ttu-id="1387b-117">*elevateAccess*를 호출하는 경우 해당 권한을 취소하려면 할당을 삭제해야 하므로 스스로 역할 할당을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1387b-117">When you call *elevateAccess* you create a role assignment for yourself, so to revoke those privileges you need to delete the assignment.</span></span>

1.  <span data-ttu-id="1387b-118">roleName = 사용자 액세스 관리자인 [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get)을 호출하여 사용자 액세스 관리자 역할의 GUID 이름을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1387b-118">Call [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) where roleName = User Access Administrator to determine the name GUID of the User Access Administrator role.</span></span> <span data-ttu-id="1387b-119">응답은 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1387b-119">The response should look like this:</span></span>

    ```
    {"value":[{"properties":{
    "roleName":"User Access Administrator",
    "type":"BuiltInRole",
    "description":"Lets you manage user access to Azure resources.",
    "assignableScopes":["/"],
    "permissions":[{"actions":["*/read","Microsoft.Authorization/*","Microsoft.Support/*"],"notActions":[]}],
    "createdOn":"0001-01-01T08:00:00.0000000Z",
    "updatedOn":"2016-05-31T23:14:04.6964687Z",
    "createdBy":null,
    "updatedBy":null},
    "id":"/providers/Microsoft.Authorization/roleDefinitions/18d7d88d-d35e-4fb5-a5c3-7773c20a72d9",
    "type":"Microsoft.Authorization/roleDefinitions",
    "name":"18d7d88d-d35e-4fb5-a5c3-7773c20a72d9"}],
    "nextLink":null}
    ```

    <span data-ttu-id="1387b-120">이 경우에 **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**인 *name* 매개 변수에서 GUID를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1387b-120">Save the GUID from the *name* parameter, in this case **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.</span></span>

2. <span data-ttu-id="1387b-121">principalId = 고유한 ObjectId인 [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get)를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="1387b-121">Call [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get) where principalId = your own ObjectId.</span></span> <span data-ttu-id="1387b-122">그러면 테넌트의 모든 할당을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="1387b-122">This lists all your assignments in the tenant.</span></span> <span data-ttu-id="1387b-123">범위가 "/"이고 RoleDefinitionId가 1단계에서 찾은 GUID 역할 이름으로 끝나는 할당을 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1387b-123">Look for the one where the scope is "/" and the RoleDefinitionId ends with the role name GUID you found in step 1.</span></span> <span data-ttu-id="1387b-124">역할 할당은 다음과 같야아 합니다.</span><span class="sxs-lookup"><span data-stu-id="1387b-124">The role assignment should look like this:</span></span>

    ```
    {"value":[{"properties":{
    "roleDefinitionId":"/providers/Microsoft.Authorization/roleDefinitions/18d7d88d-d35e-4fb5-a5c3-7773c20a72d9",
    "principalId":"{objectID}",
    "scope":"/",
    "createdOn":"2016-08-17T19:21:16.3422480Z",
    "updatedOn":"2016-08-17T19:21:16.3422480Z",
    "createdBy":"93ce6722-3638-4222-b582-78b75c5c6d65",
    "updatedBy":"93ce6722-3638-4222-b582-78b75c5c6d65"},
    "id":"/providers/Microsoft.Authorization/roleAssignments/e7dd75bc-06f6-4e71-9014-ee96a929d099",
    "type":"Microsoft.Authorization/roleAssignments",
    "name":"e7dd75bc-06f6-4e71-9014-ee96a929d099"}],
    "nextLink":null}
    ```

    <span data-ttu-id="1387b-125">이 경우에 **e7dd75bc-06f6-4e71-9014-ee96a929d099**인 *name* 매개 변수에서 GUID를 다시 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1387b-125">Again, save the GUID from the *name* parameter, in this case **e7dd75bc-06f6-4e71-9014-ee96a929d099**.</span></span>

3. <span data-ttu-id="1387b-126">마지막으로 roleAssignmentId = 2단계에서 찾은 GUID 이름인 [DELETE roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById)를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="1387b-126">Finally, call [DELETE roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) where roleAssignmentId = the name GUID you found in step 2.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1387b-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1387b-127">Next steps</span></span>

- <span data-ttu-id="1387b-128">[REST를 사용하여 역할 기반 액세스 제어를 관리](role-based-access-control-manage-access-rest.md)하는 방법에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="1387b-128">Learn more about [managing Role-Based Access Control with REST](role-based-access-control-manage-access-rest.md)</span></span>

- <span data-ttu-id="1387b-129">Azure Portal에서 [액세스 할당 관리](role-based-access-control-manage-assignments.md)</span><span class="sxs-lookup"><span data-stu-id="1387b-129">[Manage access assignments](role-based-access-control-manage-assignments.md) in the Azure portal</span></span>
