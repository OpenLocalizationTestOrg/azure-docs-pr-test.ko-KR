---
title: "RBAC를 사용하여 Azure Portal 대시보드 공유 | Microsoft Docs"
description: "이 문서에서는 역할 기반 액세스 제어를 사용하여 Azure Portal에서 대시보드를 공유하는 방법을 설명합니다."
services: azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 8908a6ce-ae0c-4f60-a0c9-b3acfe823365
ms.service: multiple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2016
ms.author: tomfitz
ms.openlocfilehash: ea0cf7ad074f95c2b49a92f9a8e32270a1d39b3a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="share-azure-dashboards-by-using-role-based-access-control"></a><span data-ttu-id="d5a3b-103">역할 기반 액세스 제어를 사용하여 Azure 대시보드 공유</span><span class="sxs-lookup"><span data-stu-id="d5a3b-103">Share Azure dashboards by using Role-Based Access Control</span></span>
<span data-ttu-id="d5a3b-104">대시보드를 구성한 후에는 이를 게시하고 조직 내의 다른 사용자와 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-104">After configuring a dashboard, you can publish it and share it with other users in your organization.</span></span> <span data-ttu-id="d5a3b-105">다른 사람이 Azure [역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md)를 사용하여 대시보드를 볼 수 있도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-105">You allow others to view your dashboard by using Azure [Role-Based Access Control](../active-directory/role-based-access-control-configure.md).</span></span> <span data-ttu-id="d5a3b-106">역할에 사용자 또는 사용자 그룹을 할당하고 해당 역할이 사용자가 게시된 대시보드를 보거나 수정할 수 있는지 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-106">You assign a user or group of users to a role, and that role defines whether those users can view or modify the published dashboard.</span></span> 

<span data-ttu-id="d5a3b-107">모든 게시된 대시보드는 Azure 리소스로 구현됩니다. 따라서 구독 내에서 관리 가능한 항목으로 존재하며 리소스 그룹에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-107">All published dashboards are implemented as Azure resources, which means they exist as manageable items within your subscription and are contained in a resource group.</span></span>  <span data-ttu-id="d5a3b-108">액세스 제어 관점에서 대시보드는 가상 컴퓨터 또는 저장소 계정과 같은 다른 리소스와 차이가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-108">From an access control perspective, dashboards are no different than other resources, such as a virtual machine or a storage account.</span></span>

> [!TIP]
> <span data-ttu-id="d5a3b-109">대시보드의 개별 타일은 표시하는 리소스에 따라 고유한 액세스 제어 요구 사항을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-109">Individual tiles on the dashboard enforce their own access control requirements based on the resources they display.</span></span>  <span data-ttu-id="d5a3b-110">그러므로 개별 타일에 있는 데이터를 보호하면서 광범위하게 공유할 수 있는 대시보드를 디자인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-110">Therefore, you can design a dashboard that is shared broadly while still protecting the data on individual tiles.</span></span>
> 
> 

## <a name="understanding-access-control-for-dashboards"></a><span data-ttu-id="d5a3b-111">대시보드에 대한 액세스 제어 이해</span><span class="sxs-lookup"><span data-stu-id="d5a3b-111">Understanding access control for dashboards</span></span>
<span data-ttu-id="d5a3b-112">RBAC(역할 기반 액세스 제어)를 사용하여 세 개의 다른 수준 범위로 역할에 사용자를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-112">With Role-Based Access Control (RBAC), you can assign users to roles at three different levels of scope:</span></span>

* <span data-ttu-id="d5a3b-113">subscription</span><span class="sxs-lookup"><span data-stu-id="d5a3b-113">subscription</span></span>
* <span data-ttu-id="d5a3b-114">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="d5a3b-114">resource group</span></span>
* <span data-ttu-id="d5a3b-115">resource</span><span class="sxs-lookup"><span data-stu-id="d5a3b-115">resource</span></span>

<span data-ttu-id="d5a3b-116">할당한 사용 권한은 구독에서 리소스까지 상속됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-116">The permissions you assign are inherited from subscription down to the resource.</span></span> <span data-ttu-id="d5a3b-117">게시된 대시보드는 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-117">The published dashboard is a resource.</span></span> <span data-ttu-id="d5a3b-118">따라서 게시된 대시보드에 대해서도 작동하는 구독의 역할에 할당된 사용자가 이미 있을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-118">Therefore, you may already have users assigned to roles for the subscription which also work for the published dashboard.</span></span> 

<span data-ttu-id="d5a3b-119">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-119">Here is an example.</span></span>  <span data-ttu-id="d5a3b-120">Azure 구독을 보유하고 구독의 **소유자**, **참여자** 또는 **읽기 권한자** 역할에 할당된 팀의 여러 멤버가 있다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-120">Let's say you have an Azure subscription and various members of your team have been assigned the roles of **owner**, **contributor**, or **reader** for the subscription.</span></span> <span data-ttu-id="d5a3b-121">소유자 또는 참여자인 사용자는 구독 내에서 대시보드를 나열, 보기, 만들기, 수정 또는 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-121">Users who are owners or contributors are able to list, view, create, modify, or delete dashboards within the subscription.</span></span>  <span data-ttu-id="d5a3b-122">읽기 권한자인 사용자는 대시보드를 나열 및 볼 수 있지만 수정 또는 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-122">Users who are readers are able to list and view dashboards, but cannot modify or delete them.</span></span>  <span data-ttu-id="d5a3b-123">읽기 권한자 액세스를 보유한 사용자는 게시된 대시보드에 대한 로컬 편집을 만들 수 있지만(예: 문제 해결 시) 해당 변경 내용을 서버로 다시 게시할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-123">Users with reader access are able to make local edits to a published dashboard (such as, when troubleshooting an issue), but are not able to publish those changes back to the server.</span></span>  <span data-ttu-id="d5a3b-124">대시보드의 개인 복사본을 직접 만들 수 있는 옵션을 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-124">They will have the option to make a private copy of the dashboard for themselves</span></span>

<span data-ttu-id="d5a3b-125">그러나 여러 대시보드를 포함하는 리소스 그룹 또는 개별 대시보드에 대한 사용 권한을 할당할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-125">However, you could also assign permissions to the resource group that contains several dashboards or to an individual dashboard.</span></span> <span data-ttu-id="d5a3b-126">예를 들어, 사용자 그룹이 구독에 걸친 제한된 사용 권한을 갖지만 특정 대시보드에 더 큰 액세스 권한을 가져야 한다고 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-126">For example, you may decide that a group of users should have limited permissions across the subscription but greater access to a particular dashboard.</span></span> <span data-ttu-id="d5a3b-127">해당 대시보드에 대한 역할에 해당 사용자를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-127">You assign those users to a role for that dashboard.</span></span> 

## <a name="publish-dashboard"></a><span data-ttu-id="d5a3b-128">대시보드 게시</span><span class="sxs-lookup"><span data-stu-id="d5a3b-128">Publish dashboard</span></span>
<span data-ttu-id="d5a3b-129">구독에 사용자 그룹과 공유할 대시보드의 구성을 완료한 경우를 가정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-129">Let's suppose you have finished configuring a dashboard that you want to share with a group of users in your subscription.</span></span> <span data-ttu-id="d5a3b-130">다음 단계에서는 저장소 관리자라는 사용자 지정된 그룹을 설명하지만 원하는 모든 그룹에 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-130">The steps below depict a customized group called Storage Managers, but you can name your group whatever you would like.</span></span> <span data-ttu-id="d5a3b-131">Active Directory 그룹을 만들고 해당 그룹에 사용자를 추가하는 방법에 대한 정보는 [Azure Active Directory에서 그룹 관리](../active-directory/active-directory-accessmanagement-manage-groups.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-131">For information about creating an Active Directory group and adding users to that group, see [Managing groups in Azure Active Directory](../active-directory/active-directory-accessmanagement-manage-groups.md).</span></span>

1. <span data-ttu-id="d5a3b-132">대시보드에서 **공유**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-132">In the dashboard, select **Share**.</span></span>
   
     ![공유 선택](./media/azure-portal-dashboard-share-access/select-share.png)
2. <span data-ttu-id="d5a3b-134">액세스를 할당하기 전에 대시보드를 게시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-134">Before assigning access, you must publish the dashboard.</span></span> <span data-ttu-id="d5a3b-135">기본적으로 대시보드는 **대시보드**라는 리소스 그룹에 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-135">By default, the dashboard will be published to a resource group named **dashboards**.</span></span> <span data-ttu-id="d5a3b-136">**게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-136">Select **Publish**.</span></span>
   
     ![게시](./media/azure-portal-dashboard-share-access/publish.png)

<span data-ttu-id="d5a3b-138">대시보드가 이제 게시되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-138">Your dashboard is now published.</span></span> <span data-ttu-id="d5a3b-139">구독에서 상속된 사용 권한이 적절한 경우 작업을 더 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-139">If the permissions inherited from the subscription are suitable, you do not need to do anything more.</span></span> <span data-ttu-id="d5a3b-140">조직에서 다른 사용자가 해당 구독 수준 역할에 따라 대시보드에 액세스하고 대시보드를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-140">Other users in your organization will be able to access and modify the dashboard based on their subscription level role.</span></span> <span data-ttu-id="d5a3b-141">그러나 이 자습서에서는 해당 대시보드에 대한 역할에 사용자 그룹을 할당하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-141">However, for this tutorial, let's assign a group of users to a role for that dashboard.</span></span>

## <a name="assign-access-to-a-dashboard"></a><span data-ttu-id="d5a3b-142">대시보드에 액세스 할당</span><span class="sxs-lookup"><span data-stu-id="d5a3b-142">Assign access to a dashboard</span></span>
1. <span data-ttu-id="d5a3b-143">대시보드를 게시한 후에 **사용자 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-143">After publishing the dashboard, select **Manage users**.</span></span>
   
     ![사용자 관리](./media/azure-portal-dashboard-share-access/manage-users.png)
2. <span data-ttu-id="d5a3b-145">이 대시보드에 대한 역할을 이미 할당한 기존 사용자의 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-145">You will see a list of existing users that are already assigned a role for this dashboard.</span></span> <span data-ttu-id="d5a3b-146">기존 사용자 목록은 아래 이미지와 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-146">Your list of existing users will be different than the image below.</span></span> <span data-ttu-id="d5a3b-147">대부분의 경우 할당은 구독에서 상속됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-147">Most likely, the assignments are inherited from the subscription.</span></span> <span data-ttu-id="d5a3b-148">새 사용자 또는 그룹을 추가하려면 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-148">To add a new user or group, select **Add**.</span></span>
   
     ![사용자 추가](./media/azure-portal-dashboard-share-access/existing-users.png)
3. <span data-ttu-id="d5a3b-150">부여하려는 사용 권한을 나타내는 역할을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-150">Select the role that represents the permissions you would like to grant.</span></span> <span data-ttu-id="d5a3b-151">이 예에서는 **참가자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-151">For this example, select **Contributor**.</span></span>
   
     ![역할 선택](./media/azure-portal-dashboard-share-access/select-role.png)
4. <span data-ttu-id="d5a3b-153">역할에 할당하려는 사용자 또는 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-153">Select the user or group that you wish to assign to the role.</span></span> <span data-ttu-id="d5a3b-154">목록에 원하는 사용자 또는 그룹이 표시되지 않으면 검색 상자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-154">If you do not see the user or group you are looking for in the list, use the search box.</span></span> <span data-ttu-id="d5a3b-155">사용 가능한 그룹 목록은 Active Directory에서 만든 그룹에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-155">Your list of available groups will depend on the groups you have created in your Active Directory.</span></span>
   
     ![사용자 선택](./media/azure-portal-dashboard-share-access/select-user.png) 
5. <span data-ttu-id="d5a3b-157">사용자 또는 그룹을 추가했으면 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-157">When you have finished adding users or groups, select **OK**.</span></span> 
6. <span data-ttu-id="d5a3b-158">새 할당은 사용자 목록에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-158">The new assignment is added to the list of users.</span></span> <span data-ttu-id="d5a3b-159">해당 **액세스**는 **상속됨**이 아닌 **할당**으로 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-159">Notice that its **Access** is listed as **Assigned** rather than **Inherited**.</span></span>
   
     ![할당된 역할](./media/azure-portal-dashboard-share-access/assigned-roles.png)

## <a name="next-steps"></a><span data-ttu-id="d5a3b-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d5a3b-161">Next steps</span></span>
* <span data-ttu-id="d5a3b-162">역할의 목록은 [RBAC: 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-162">For a list of roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="d5a3b-163">리소스 관리에 관한 자세한 내용은 [포털을 통한 Azure 리소스 관리](resource-group-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d5a3b-163">To learn about managing resources, see [Manage Azure resources through portal](resource-group-portal.md).</span></span>

