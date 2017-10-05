---
title: "Azure Active Directory에서 삭제된 Office 365 그룹 복원 | Microsoft Docs"
description: "Azure Active Directory에서 삭제된 그룹을 복원하고 복원 가능한 그룹을 보고 영구적으로 그룹을 삭제하는 방법"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: curtand
ms.openlocfilehash: 32d36ae96797a59bb47bf782ab038f21f231f046
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="restore-a-deleted-office-365-group-in-azure-active-directory"></a><span data-ttu-id="1b2b9-103">Azure Active Directory에서 삭제된 Office 365 그룹 복원</span><span class="sxs-lookup"><span data-stu-id="1b2b9-103">Restore a deleted Office 365 group in Azure Active Directory</span></span>

<span data-ttu-id="1b2b9-104">Azure AD(Azure Active Directory)에서 Office 365 그룹을 삭제하는 경우 삭제된 그룹은 유지되지만 삭제일로부터 30일 동안 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b2b9-104">When you delete an Office 365 group in the Azure Active Directory (Azure AD), the deleted group is retained but not visible for 30 days from the deletion date.</span></span> <span data-ttu-id="1b2b9-105">필요한 경우 그룹 및 해당 콘텐츠를 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b2b9-105">This is so that the group and its contents can be restored if needed.</span></span> <span data-ttu-id="1b2b9-106">이 기능은 Azure AD의 Office 365 그룹에만 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b2b9-106">This functionality is restricted exclusively to Office 365 groups in Azure AD.</span></span> <span data-ttu-id="1b2b9-107">보안 그룹 및 배포 그룹에는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1b2b9-107">It is not available for security groups and distribution groups.</span></span>

> [!NOTE] 
> <span data-ttu-id="1b2b9-108">`Remove-MsolGroup`을 사용하면 그룹이 영구적으로 제거되므로 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b2b9-108">Don't use `Remove-MsolGroup` because it purges the group permanently.</span></span> <span data-ttu-id="1b2b9-109">항상 `Remove-AzureADMSGroup`을 사용하여 O365 그룹을 삭제하세요.</span><span class="sxs-lookup"><span data-stu-id="1b2b9-109">Always use `Remove-AzureADMSGroup` to delete an O365 group.</span></span> 

<span data-ttu-id="1b2b9-110">그룹을 복원하는 데 필요한 사용 권한은 다음 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b2b9-110">The permissions required to restore a group can be any of the following:</span></span>

<span data-ttu-id="1b2b9-111">역할</span><span class="sxs-lookup"><span data-stu-id="1b2b9-111">Role</span></span>  | <span data-ttu-id="1b2b9-112">권한</span><span class="sxs-lookup"><span data-stu-id="1b2b9-112">Permissions</span></span> 
--------- | ---------
<span data-ttu-id="1b2b9-113">회사 관리자, 파트너 계층2 지원 및 InTune 서비스 관리자</span><span class="sxs-lookup"><span data-stu-id="1b2b9-113">Company Administrator, Partner Tier2 support, and InTune Service Admins</span></span> | <span data-ttu-id="1b2b9-114">모든 삭제된 Office 365 그룹을 복원할 수 있음</span><span class="sxs-lookup"><span data-stu-id="1b2b9-114">Can restore any deleted Office 365 group</span></span> 
<span data-ttu-id="1b2b9-115">사용자 계정 관리자 및 파트너 계층1 지원</span><span class="sxs-lookup"><span data-stu-id="1b2b9-115">User Account Administrator and Partner Tier1 support</span></span> | <span data-ttu-id="1b2b9-116">회사 관리자 역할에 할당된 것을 제외한 모든 삭제된 Office 365 그룹을 복원할 수 있음</span><span class="sxs-lookup"><span data-stu-id="1b2b9-116">Can restore any deleted Office 365 group except those assigned to the Company Administrator role</span></span> 
<span data-ttu-id="1b2b9-117">사용자</span><span class="sxs-lookup"><span data-stu-id="1b2b9-117">User</span></span> | <span data-ttu-id="1b2b9-118">소유했던 모든 삭제된 Office 365 그룹을 복원할 수 있음</span><span class="sxs-lookup"><span data-stu-id="1b2b9-118">Can restore any deleted Office 365 group that they owned</span></span> 


## <a name="view-the-deleted-office-365-groups-that-are-available-to-restore"></a><span data-ttu-id="1b2b9-119">복원할 수 있는 삭제된 Office 365 그룹 보기</span><span class="sxs-lookup"><span data-stu-id="1b2b9-119">View the deleted Office 365 groups that are available to restore</span></span>
<span data-ttu-id="1b2b9-120">다음 cmdlet을 사용하여 관심 있는 그룹이 영구적으로 제거되었는지 확인하기 위해 삭제된 그룹을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b2b9-120">The following cmdlets can be used to view the deleted groups to verify that the one or ones you're interested in have not yet been permanently purged.</span></span> <span data-ttu-id="1b2b9-121">이러한 cmdlet은 [Azure AD PowerShell 모듈](https://www.powershellgallery.com/packages/AzureAD/)에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b2b9-121">These cmdlets are part of the [Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span></span> <span data-ttu-id="1b2b9-122">이 모듈에 대한 자세한 정보는 [Azure Active Directory PowerShell 버전 2](/powershell/azure/install-adv2?view=azureadps-2.0) 문서에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b2b9-122">More information about this module can be found in the [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0) article.</span></span>

1.  <span data-ttu-id="1b2b9-123">다음 cmdlet을 실행하여 여전히 복원할 수 있는 테넌트의 모든 삭제된 Office 365 그룹을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1b2b9-123">Run the following cmdlet to display all deleted Office 365 groups in your tenant that are still available to restore.</span></span>
  ```
  Get-AzureADMSDeletedGroup
  ```

2.  <span data-ttu-id="1b2b9-124">또는 특정 그룹의 objectID를 아는 경우(및 1단계의 cmdlet에서 가져올 수 있는 경우) 다음 cmdlet을 실행하여 삭제된 특정 그룹이 영구적으로 제거되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1b2b9-124">Alternately, if you know the objectID of a specific group (and you can get it from the cmdlet in step 1), run the following cmdlet to verify that the specific deleted group has not yet been permanently purged.</span></span>
  ```
  Get-AzureADMSDeletedGroup –Id <objectId>
  ```



## <a name="how-to-restore-your-deleted-office-365-group"></a><span data-ttu-id="1b2b9-125">삭제된 Office 365 그룹을 복원하는 방법</span><span class="sxs-lookup"><span data-stu-id="1b2b9-125">How to restore your deleted Office 365 group</span></span>
<span data-ttu-id="1b2b9-126">그룹을 복원할 수 있는지 확인한 후 다음 단계 중 하나를 사용하여 삭제된 그룹을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="1b2b9-126">Once you have verified that the group is still available to restore, restore the deleted group with one of the following steps.</span></span> <span data-ttu-id="1b2b9-127">그룹에 문서, SP 사이트 또는 기타 영구 개체가 포함된 경우 그룹 및 해당 내용을 완전히 복원하는 데 최대 24시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b2b9-127">If the group contains documents, SP sites, or other persistent objects, it might take up to 24 hours to fully restore a group and its contents.</span></span>

1.  <span data-ttu-id="1b2b9-128">다음 cmdlet을 실행하여 그룹 및 해당 내용을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="1b2b9-128">Run the following cmdlet to restore the group and its contents.</span></span>
  
  ```
  Restore-AzureADMSDeletedDirectoryObject –Id <objectId>
  ``` 

<span data-ttu-id="1b2b9-129">또는 다음 cmdlet을 실행하여 삭제된 그룹을 영구적으로 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b2b9-129">Alternatively, the following cmdlet can be run to permanently remove the deleted group.</span></span>
  ```
  Remove-AzureADMSDeletedDirectoryObject –Id <objectId>
  ```

## <a name="how-do-you-know-this-worked"></a><span data-ttu-id="1b2b9-130">작동되었는지 어떻게 알 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="1b2b9-130">How do you know this worked?</span></span>
<span data-ttu-id="1b2b9-131">Office 365 그룹을 성공적으로 복원했는지 확인하려면 `Get-AzureADGroup –ObjectId <objectId>` cmdlet을 실행하여 그룹에 대한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1b2b9-131">To verify that you’ve successfully restored an Office 365 group, run the `Get-AzureADGroup –ObjectId <objectId>` cmdlet to display information about the group.</span></span> <span data-ttu-id="1b2b9-132">복원 후 요청이 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b2b9-132">After the restore request is completed:</span></span>
- <span data-ttu-id="1b2b9-133">그룹은 Exchange의 왼쪽 탐색 모음에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b2b9-133">The group will appear in the Left nav bar on Exchange</span></span>
- <span data-ttu-id="1b2b9-134">그룹에 대한 계획은 Planner에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b2b9-134">The plan for the group will appear in Planner</span></span>
- <span data-ttu-id="1b2b9-135">모든 Sharepoint 사이트와 모든 해당 콘텐츠를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b2b9-135">Any Sharepoint sites and all of their contents will be available</span></span>
- <span data-ttu-id="1b2b9-136">Office 365 그룹을 지원하는 Exchange 끝점 및 다른 Office 365 워크로드 중 하나에서 그룹에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b2b9-136">The group can be accessed from any of the Exchange endpoints and other Office 365 workloads that support Office 365 groups</span></span>


## <a name="next-steps"></a><span data-ttu-id="1b2b9-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1b2b9-137">Next steps</span></span>
<span data-ttu-id="1b2b9-138">이러한 문서는 Azure Active Directory 그룹에 대한 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1b2b9-138">These articles provide additional information on Azure Active Directory groups.</span></span>

* [<span data-ttu-id="1b2b9-139">기존 그룹 보기</span><span class="sxs-lookup"><span data-stu-id="1b2b9-139">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="1b2b9-140">그룹의 설정 관리</span><span class="sxs-lookup"><span data-stu-id="1b2b9-140">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="1b2b9-141">그룹의 멤버 관리</span><span class="sxs-lookup"><span data-stu-id="1b2b9-141">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="1b2b9-142">그룹의 멤버 자격 관리</span><span class="sxs-lookup"><span data-stu-id="1b2b9-142">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="1b2b9-143">그룹의 사용자에 대한 동적 규칙 관리</span><span class="sxs-lookup"><span data-stu-id="1b2b9-143">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
