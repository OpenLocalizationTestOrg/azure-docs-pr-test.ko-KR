---
title: "aaaTenant 관리자 액세스-Azure AD 권한 상승 | Microsoft Docs"
description: "이 항목에서는 역할 기반 액세스 제어 (RBAC)에 대 한 역할에 기본 제공 hello를 설명 합니다."
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
ms.openlocfilehash: 7996f2af3277dc40e2a1766cc4a7862a2399cdef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="elevate-access-as-a-tenant-admin-with-role-based-access-control"></a><span data-ttu-id="368c3-103">역할 기반 액세스 제어를 사용하여 테넌트 관리자로 액세스 권한 상승</span><span class="sxs-lookup"><span data-stu-id="368c3-103">Elevate access as a tenant admin with Role-Based Access Control</span></span>

<span data-ttu-id="368c3-104">역할 기반 액세스 제어를 통해 테넌트 관리자가 액세스에서 임시 권한이 상승되어 평소보다 높은 수준의 사용 권한을 부여받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="368c3-104">Role-based Access Control helps tenant administrators get temporary elevations in access so that they can grant higher permissions than normal.</span></span> <span data-ttu-id="368c3-105">테 넌 트 관리자 승격할 수 있습니다 자신 toohello 사용자 액세스 관리자 역할이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="368c3-105">A tenant admin can elevate herself toohello User Access Administrator role when needed.</span></span> <span data-ttu-id="368c3-106">해당 역할은 hello 제공 자신 또는 다른 관리 권한을 toogrant 테 넌 트 hello에서 역할 "/" 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="368c3-106">That role gives hello tenant admin permissions toogrant herself or others roles at hello "/" scope.</span></span>

<span data-ttu-id="368c3-107">이 기능은 모든 hello 조직에 있는 구독 관리자 toosee hello 테 넌 트 수 있기 때문에 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="368c3-107">This feature is important because it allows hello tenant admin toosee all hello subscriptions that exist in an organization.</span></span> <span data-ttu-id="368c3-108">또한 앱 (예: 송장 및 감사) tooaccess 자동화에 대 한 모든 hello 구독을 허용 하 고 대금 청구 또는 자산 관리에 대 한 hello 조직 hello 상태의 정확 하 게 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="368c3-108">It also allows for automation apps (like invoicing and auditing) tooaccess all hello subscriptions and provide an accurate view of hello state of hello organization for billing or asset management.</span></span>  

## <a name="how-toouse-elevateaccess-toogive-tenant-access"></a><span data-ttu-id="368c3-109">Toouse elevateAccess toogive 액세스 테 넌 트 방식</span><span class="sxs-lookup"><span data-stu-id="368c3-109">How toouse elevateAccess toogive tenant access</span></span>

<span data-ttu-id="368c3-110">hello basic 프로세스 단계를 수행 하는 hello로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="368c3-110">hello basic process works with hello following steps:</span></span>

1. <span data-ttu-id="368c3-111">REST를 사용 하 여 호출 *elevateAccess*, 있습니다 hello 사용자 액세스 관리자 역할에 "/" 범위에 있는 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="368c3-111">Using REST, call *elevateAccess*, which grants you hello User Access Administrator role at "/" scope.</span></span>

    ```
    POST https://management.azure.com/providers/Microsoft.Authorization/elevateAccess?api-version=2016-07-01
    ```

2. <span data-ttu-id="368c3-112">만들기는 [역할 할당](/rest/api/authorization/roleassignments) tooassign 두 범위 모두에서 모든 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="368c3-112">Create a [role assignment](/rest/api/authorization/roleassignments) tooassign any role at any scope.</span></span> <span data-ttu-id="368c3-113">다음 예제는 hello 할당에 대 한 hello 속성에서 읽기 역할 hello "/" 범위를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="368c3-113">hello following example shows hello properties for assigning hello Reader role at "/" scope:</span></span>

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

3. <span data-ttu-id="368c3-114">사용자 액세스 관리자인 경우 "/" 범위에서 역할 할당을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="368c3-114">While a User Access Admin, you can also delete role assignments at "/" scope.</span></span>

4. <span data-ttu-id="368c3-115">다시 필요할 때까지 사용자 액세스 관리자 권한을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="368c3-115">Revoke your User Access Admin privileges until they're needed again.</span></span>


## <a name="how-tooundo-hello-elevateaccess-action"></a><span data-ttu-id="368c3-116">Tooundo는 elevateAccess 동작 hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="368c3-116">How tooundo hello elevateAccess action</span></span>

<span data-ttu-id="368c3-117">호출 하는 경우 *elevateAccess* toorevoke 것 권한 수 있으므로 필요한 toodelete hello 할당, 자신에 대 한 역할 할당을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="368c3-117">When you call *elevateAccess* you create a role assignment for yourself, so toorevoke those privileges you need toodelete hello assignment.</span></span>

1.  <span data-ttu-id="368c3-118">호출 [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) 여기서 roleName = 사용자 액세스 관리자에 게 toodetermine hello 이름 hello 사용자 액세스 관리자 역할의 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="368c3-118">Call [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) where roleName = User Access Administrator toodetermine hello name GUID of hello User Access Administrator role.</span></span> <span data-ttu-id="368c3-119">hello 응답은 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="368c3-119">hello response should look like this:</span></span>

    ```
    {"value":[{"properties":{
    "roleName":"User Access Administrator",
    "type":"BuiltInRole",
    "description":"Lets you manage user access tooAzure resources.",
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

    <span data-ttu-id="368c3-120">Hello에서 GUID hello 저장 *이름* 매개 변수를이 경우 **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**합니다.</span><span class="sxs-lookup"><span data-stu-id="368c3-120">Save hello GUID from hello *name* parameter, in this case **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.</span></span>

2. <span data-ttu-id="368c3-121">principalId = 고유한 ObjectId인 [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get)를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="368c3-121">Call [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get) where principalId = your own ObjectId.</span></span> <span data-ttu-id="368c3-122">Hello 테 넌 트의 모든 할당을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="368c3-122">This lists all your assignments in hello tenant.</span></span> <span data-ttu-id="368c3-123">여기서는 hello 범위 hello 하나 찾습니다 "/" hello 역할과 hello RoleDefinitionId 끝 1 단계에서 찾은 GUID 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="368c3-123">Look for hello one where hello scope is "/" and hello RoleDefinitionId ends with hello role name GUID you found in step 1.</span></span> <span data-ttu-id="368c3-124">hello 역할 할당은 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="368c3-124">hello role assignment should look like this:</span></span>

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

    <span data-ttu-id="368c3-125">Hello에서 hello GUID를 다시 저장 *이름* 매개 변수를이 경우 **e7dd75bc-06f6-4e71-9014-ee96a929d099**합니다.</span><span class="sxs-lookup"><span data-stu-id="368c3-125">Again, save hello GUID from hello *name* parameter, in this case **e7dd75bc-06f6-4e71-9014-ee96a929d099**.</span></span>

3. <span data-ttu-id="368c3-126">마지막으로 호출 [DELETE roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) 여기서 roleAssignmentId = hello 이름 2 단계에서 찾은 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="368c3-126">Finally, call [DELETE roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) where roleAssignmentId = hello name GUID you found in step 2.</span></span>

## <a name="next-steps"></a><span data-ttu-id="368c3-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="368c3-127">Next steps</span></span>

- <span data-ttu-id="368c3-128">[REST를 사용하여 역할 기반 액세스 제어를 관리](role-based-access-control-manage-access-rest.md)하는 방법에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="368c3-128">Learn more about [managing Role-Based Access Control with REST](role-based-access-control-manage-access-rest.md)</span></span>

- <span data-ttu-id="368c3-129">[관리 액세스 할당](role-based-access-control-manage-assignments.md) hello Azure 포털에서</span><span class="sxs-lookup"><span data-stu-id="368c3-129">[Manage access assignments](role-based-access-control-manage-assignments.md) in hello Azure portal</span></span>
