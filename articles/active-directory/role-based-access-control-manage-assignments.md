---
title: "Azure 리소스 액세스 권한 할당 보기 | Microsoft Docs"
description: "Azure Portal에서 모든 사용자 또는 그룹에 대한 모든 역할 기반 액세스 제어 할당 보기 및 관리"
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
editor: jeffsta
ms.assetid: e6f9e657-8ee3-4eec-a21c-78fe1b52a005
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: andredm
ms.openlocfilehash: 72c695d08bdf5de003d51ffb0768184e1e4d00ba
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="view-access-assignments-for-users-and-groups-in-the-azure-portal"></a><span data-ttu-id="ce467-103">Azure Portal에서 사용자 및 그룹에 대한 액세스 권한 할당 보기</span><span class="sxs-lookup"><span data-stu-id="ce467-103">View access assignments for users and groups in the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ce467-104">사용자 또는 그룹에 따른 액세스 관리</span><span class="sxs-lookup"><span data-stu-id="ce467-104">Manage access by user or group</span></span>](role-based-access-control-manage-assignments.md)
> * [<span data-ttu-id="ce467-105">리소스에 따른 액세스 관리</span><span class="sxs-lookup"><span data-stu-id="ce467-105">Manage access by resource</span></span>](role-based-access-control-configure.md)

<span data-ttu-id="ce467-106">Azure AD(Azure Active Directory)의 RBAC(역할 기반 액세스 제어)로 Azure 리소스에 대한 액세스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce467-106">With role-based access control (RBAC) in the Azure Active Directory (Azure AD), you can manage access to your Azure resources.</span></span> 

<span data-ttu-id="ce467-107">두 가지 방법으로 사용 권한을 제한할 수 있기 때문에 RBAC를 사용하여 할당된 액세스 권한은 세분화됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce467-107">Access assigned with RBAC is fine-grained because there are two ways you can restrict the permissions:</span></span>

* <span data-ttu-id="ce467-108">**범위:** RBAC 역할 할당은 특정 구독, 리소스 그룹 또는 리소스로 범위가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce467-108">**Scope:** RBAC role assignments are scoped to a specific subscription, resource group, or resource.</span></span> <span data-ttu-id="ce467-109">단일 리소스에 대한 액세스 권한을 가진 사용자는 동일한 구독에서 다른 리소스에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ce467-109">A user given access to a single resource cannot access any other resources in the same subscription.</span></span>
* <span data-ttu-id="ce467-110">**역할:** 할당의 범위 내에서 역할을 할당하면 액세스 권한이 더 좁아집니다.</span><span class="sxs-lookup"><span data-stu-id="ce467-110">**Role:** Within the scope of the assignment, access is narrowed even further by assigning a role.</span></span> <span data-ttu-id="ce467-111">역할은 소유자와 같이 높은 수준일 수도 있고 가상 컴퓨터 판독기와 같이 특정될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce467-111">Roles can be high-level, like owner, or specific, like virtual machine reader.</span></span>

<span data-ttu-id="ce467-112">역할은 할당에 대한 범위인 구독, 리소스 그룹 또는 리소스 내에서만 할당될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce467-112">Roles can only be assigned from within the subscription, resource group, or resource that is the scope for the assignment.</span></span> <span data-ttu-id="ce467-113">하지만 지정된 사용자나 그룹에 대한 모든 액세스 권한 할당은 단일 위치에서만 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce467-113">But you can view all the access assignments for a given user or group in a single place.</span></span> <span data-ttu-id="ce467-114">각 구독에서 최대 2000개의 역할 할당을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce467-114">You can have up to 2000 role assignments in each subscription.</span></span> 

<span data-ttu-id="ce467-115">[역할 할당을 사용하여 Azure 구독 리소스에 대한 액세스를 관리](role-based-access-control-configure.md)하는 방법에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ce467-115">Get more information about how to [Use role assignments to manage access to your Azure subscription resources](role-based-access-control-configure.md).</span></span>

## <a name="view-access-assignments"></a><span data-ttu-id="ce467-116">액세스 권한 할당 보기</span><span class="sxs-lookup"><span data-stu-id="ce467-116">View access assignments</span></span>
<span data-ttu-id="ce467-117">단일 사용자 또는 그룹에 대한 액세스 권한 할당을 살펴보려면 [Azure Portal](http://portal.azure.com)의 Azure Active directory에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ce467-117">To look up the access assignments for a single user or group, start in Azure Active Directory in the [Azure portal](http://portal.azure.com).</span></span>

1. <span data-ttu-id="ce467-118">**Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ce467-118">Select **Azure Active Directory**.</span></span> <span data-ttu-id="ce467-119">이 옵션이 탐색 목록에 표시되지 않는 경우 **추가 서비스**를 선택한 다음 아래로 스크롤하여 **Azure Active Directory**를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ce467-119">If this option is not visible on your navigation list, select **More Services** and then scroll down to find **Azure Active Directory**.</span></span>
2. <span data-ttu-id="ce467-120">**사용자 및 그룹** 및 **모든 사용자** 또는 **모든 그룹**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ce467-120">Select **Users and Groups**, and then either **All users** or **All groups**.</span></span> <span data-ttu-id="ce467-121">이 예제에서는 개별 사용자에게 집중합니다.</span><span class="sxs-lookup"><span data-stu-id="ce467-121">For this example, we focus on individual users.</span></span>
    <span data-ttu-id="ce467-122">![Azure Active Directory에서 사용자 및 그룹 관리 - 스크린샷](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)</span><span class="sxs-lookup"><span data-stu-id="ce467-122">![Manage users and groups in Azure Active Directory - screenshot](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)</span></span>
3. <span data-ttu-id="ce467-123">이름 또는 사용자 이름별로 사용자를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="ce467-123">Search for the user by name or username.</span></span>
4. <span data-ttu-id="ce467-124">사용자 블레이드에서 **Azure 리소스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ce467-124">Select **Azure resources** on the user blade.</span></span> <span data-ttu-id="ce467-125">해당 사용자에 대한 모든 액세스 권한 할당이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce467-125">All the access assignments for that user appear.</span></span>

### <a name="read-permissions-to-view-assignments"></a><span data-ttu-id="ce467-126">할당을 보는 읽기 사용 권한</span><span class="sxs-lookup"><span data-stu-id="ce467-126">Read permissions to view assignments</span></span>
<span data-ttu-id="ce467-127">이 페이지에서는 읽을 수 있는 사용 권한이 있는 액세스 권한 할당만 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ce467-127">This page only shows the access assignments that you have permission to read.</span></span> <span data-ttu-id="ce467-128">예를 들어 구독 A에 대한 읽기 액세스 권한이 있으며 Azure 리소스 블레이드로 이동하여 사용자의 할당을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ce467-128">For example, you have read access to subscription A and go to the Azure resources blade to check a user's assignments.</span></span> <span data-ttu-id="ce467-129">구독 A에 대한 액세스 권한 할당을 확인할 수 있지만 구독 B에 대한 액세스 권한 할당이 있는지 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ce467-129">You can see her access assignments for subscription A, but can't see that she also has access assignments on subscription B.</span></span>

## <a name="delete-access-assignments"></a><span data-ttu-id="ce467-130">액세스 권한 할당 삭제</span><span class="sxs-lookup"><span data-stu-id="ce467-130">Delete access assignments</span></span>
<span data-ttu-id="ce467-131">이 블레이드에서 사용자 또는 그룹에 직접 할당된 액세스 권한 할당을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce467-131">From this blade, you can delete access assignments that were assigned directly to a user or group.</span></span> <span data-ttu-id="ce467-132">액세스 권한 할당이 부모 그룹에서 상속된 경우 리소스 또는 구독으로 이동하고 거기에서 할당을 관리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce467-132">If the access assignment was inherited from a parent group, you need to go to the resource or subscription and manage the assignment there.</span></span>

1. <span data-ttu-id="ce467-133">사용자 또는 그룹에 대한 모든 액세스 권한 할당 목록에서 삭제하려는 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ce467-133">From the list of all the access assignments for a user or group, select the one you want to delete.</span></span>
2. <span data-ttu-id="ce467-134">**제거** 및 **예**를 차례로 선택하고 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ce467-134">Select **Remove** and then **Yes** to confirm.</span></span>
    <span data-ttu-id="ce467-135">![액세스 권한 할당 제거 - 스크린샷](./media/role-based-access-control-manage-assignments/delete_assignment.png)</span><span class="sxs-lookup"><span data-stu-id="ce467-135">![Remove access assignment - screenshot](./media/role-based-access-control-manage-assignments/delete_assignment.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce467-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ce467-136">Next steps</span></span>

* <span data-ttu-id="ce467-137">[역할 할당을 사용하여 Azure 구독 리소스에 대한 액세스를 관리](role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="ce467-137">Get started with Role-Based Access Control to [Use role assignments to manage access to your Azure subscription resources](role-based-access-control-configure.md)</span></span>
* <span data-ttu-id="ce467-138">[RBAC 기본 제공 역할](role-based-access-built-in-roles.md)</span><span class="sxs-lookup"><span data-stu-id="ce467-138">See the [RBAC built-in roles](role-based-access-built-in-roles.md)</span></span>

