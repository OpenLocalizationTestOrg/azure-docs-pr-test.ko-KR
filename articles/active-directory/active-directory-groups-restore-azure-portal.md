---
title: "Azure Active Directory에서 삭제 된 Office 365 aaaRestore 그룹 | Microsoft Docs"
description: "Toorestore 삭제 된 그룹, 보기 복원 가능한 그룹 및 permamnently Azure Active Directory에서 그룹 삭제 방법"
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
ms.openlocfilehash: 4e6650d64aa19f0c909f1c511f48681de8032f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-deleted-office-365-group-in-azure-active-directory"></a><span data-ttu-id="aac04-103">Azure Active Directory에서 삭제된 Office 365 그룹 복원</span><span class="sxs-lookup"><span data-stu-id="aac04-103">Restore a deleted Office 365 group in Azure Active Directory</span></span>

<span data-ttu-id="aac04-104">Hello Azure Active Directory (Azure AD)에 있는 Office 365 그룹을 삭제 하면 삭제 hello 그룹은 유지 하지만 표시 되지 않아야 30 일 동안 hello 삭제 날짜에서.</span><span class="sxs-lookup"><span data-stu-id="aac04-104">When you delete an Office 365 group in hello Azure Active Directory (Azure AD), hello deleted group is retained but not visible for 30 days from hello deletion date.</span></span> <span data-ttu-id="aac04-105">이 소프트웨어는 필요에 따라 hello 그룹 및 해당 콘텐츠를 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac04-105">This is so that hello group and its contents can be restored if needed.</span></span> <span data-ttu-id="aac04-106">이 기능은 제한 된 Azure AD의 그룹을 단독으로 tooOffice 365 합니다.</span><span class="sxs-lookup"><span data-stu-id="aac04-106">This functionality is restricted exclusively tooOffice 365 groups in Azure AD.</span></span> <span data-ttu-id="aac04-107">보안 그룹 및 배포 그룹에는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="aac04-107">It is not available for security groups and distribution groups.</span></span>

> [!NOTE] 
> <span data-ttu-id="aac04-108">사용 하지 않는 `Remove-MsolGroup` hello 그룹을 영구적으로 제거 하기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac04-108">Don't use `Remove-MsolGroup` because it purges hello group permanently.</span></span> <span data-ttu-id="aac04-109">항상 사용 하 여 `Remove-AzureADMSGroup` toodelete는 O365 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="aac04-109">Always use `Remove-AzureADMSGroup` toodelete an O365 group.</span></span> 

<span data-ttu-id="aac04-110">hello 권한이 필요 toorestore 그룹 hello 다음 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac04-110">hello permissions required toorestore a group can be any of hello following:</span></span>

<span data-ttu-id="aac04-111">역할</span><span class="sxs-lookup"><span data-stu-id="aac04-111">Role</span></span>  | <span data-ttu-id="aac04-112">권한</span><span class="sxs-lookup"><span data-stu-id="aac04-112">Permissions</span></span> 
--------- | ---------
<span data-ttu-id="aac04-113">회사 관리자, 파트너 계층2 지원 및 InTune 서비스 관리자</span><span class="sxs-lookup"><span data-stu-id="aac04-113">Company Administrator, Partner Tier2 support, and InTune Service Admins</span></span> | <span data-ttu-id="aac04-114">모든 삭제된 Office 365 그룹을 복원할 수 있음</span><span class="sxs-lookup"><span data-stu-id="aac04-114">Can restore any deleted Office 365 group</span></span> 
<span data-ttu-id="aac04-115">사용자 계정 관리자 및 파트너 계층1 지원</span><span class="sxs-lookup"><span data-stu-id="aac04-115">User Account Administrator and Partner Tier1 support</span></span> | <span data-ttu-id="aac04-116">할당 된 해당 toohello 회사 관리자 역할을 제외한 모든 삭제 된 Office 365 그룹을 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac04-116">Can restore any deleted Office 365 group except those assigned toohello Company Administrator role</span></span> 
<span data-ttu-id="aac04-117">사용자</span><span class="sxs-lookup"><span data-stu-id="aac04-117">User</span></span> | <span data-ttu-id="aac04-118">소유했던 모든 삭제된 Office 365 그룹을 복원할 수 있음</span><span class="sxs-lookup"><span data-stu-id="aac04-118">Can restore any deleted Office 365 group that they owned</span></span> 


## <a name="view-hello-deleted-office-365-groups-that-are-available-toorestore"></a><span data-ttu-id="aac04-119">보기 hello toorestore 사용할 수 있는 Office 365 그룹 삭제</span><span class="sxs-lookup"><span data-stu-id="aac04-119">View hello deleted Office 365 groups that are available toorestore</span></span>
<span data-ttu-id="aac04-120">에 관심이 스토리 하지 아직 영구적으로 삭제 또는 cmdlet을 다음 hello hello 하나 사용 하는 tooview 삭제 hello 그룹 tooverify를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac04-120">hello following cmdlets can be used tooview hello deleted groups tooverify that hello one or ones you're interested in have not yet been permanently purged.</span></span> <span data-ttu-id="aac04-121">이러한 cmdlet hello의 일부인 [Azure AD PowerShell 모듈이](https://www.powershellgallery.com/packages/AzureAD/)합니다.</span><span class="sxs-lookup"><span data-stu-id="aac04-121">These cmdlets are part of hello [Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span></span> <span data-ttu-id="aac04-122">이 모듈에 대 한 자세한 내용은 hello에 있습니다 [Azure Active Directory PowerShell 버전 2](/powershell/azure/install-adv2?view=azureadps-2.0) 문서.</span><span class="sxs-lookup"><span data-stu-id="aac04-122">More information about this module can be found in hello [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0) article.</span></span>

1.  <span data-ttu-id="aac04-123">모든 cmdlet toodisplay 다음 실행된 hello toorestore 계속 사용할 수 있는 테 넌 트에 Office 365 그룹을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="aac04-123">Run hello following cmdlet toodisplay all deleted Office 365 groups in your tenant that are still available toorestore.</span></span>
  ```
  Get-AzureADMSDeletedGroup
  ```

2.  <span data-ttu-id="aac04-124">또는 알고 있는 경우 특정 그룹의 hello objectID (1 단계에서 hello cmdlet에서 가져올 수 있습니다), 삭제 된 특정 그룹 hello cmdlet tooverify 다음 실행된 hello 하지 아직 영구적으로 삭제 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="aac04-124">Alternately, if you know hello objectID of a specific group (and you can get it from hello cmdlet in step 1), run hello following cmdlet tooverify that hello specific deleted group has not yet been permanently purged.</span></span>
  ```
  Get-AzureADMSDeletedGroup –Id <objectId>
  ```



## <a name="how-toorestore-your-deleted-office-365-group"></a><span data-ttu-id="aac04-125">어떻게 toorestore 삭제 된 Office 365 그룹</span><span class="sxs-lookup"><span data-stu-id="aac04-125">How toorestore your deleted Office 365 group</span></span>
<span data-ttu-id="aac04-126">그 hello 그룹은 여전히 사용할 수 있는 toorestore를 확인 한 후 복원 hello hello 다음 단계 중 하나가 지정 된 그룹을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="aac04-126">Once you have verified that hello group is still available toorestore, restore hello deleted group with one of hello following steps.</span></span> <span data-ttu-id="aac04-127">Hello에 포함 된 문서, SP 사이트 또는 다른 영구 개체는 그룹 및 해당 내용을 too24 시간 toofully 복원을 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac04-127">If hello group contains documents, SP sites, or other persistent objects, it might take up too24 hours toofully restore a group and its contents.</span></span>

1.  <span data-ttu-id="aac04-128">실행 hello 다음 cmdlet toorestore hello 그룹 및 해당 내용을 합니다.</span><span class="sxs-lookup"><span data-stu-id="aac04-128">Run hello following cmdlet toorestore hello group and its contents.</span></span>
  
  ```
  Restore-AzureADMSDeletedDirectoryObject –Id <objectId>
  ``` 

<span data-ttu-id="aac04-129">또는 hello 다음 cmdlet 실행할 수 toopermanently 삭제 hello 그룹을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="aac04-129">Alternatively, hello following cmdlet can be run toopermanently remove hello deleted group.</span></span>
  ```
  Remove-AzureADMSDeletedDirectoryObject –Id <objectId>
  ```

## <a name="how-do-you-know-this-worked"></a><span data-ttu-id="aac04-130">작동되었는지 어떻게 알 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="aac04-130">How do you know this worked?</span></span>
<span data-ttu-id="aac04-131">hello를 실행 하는 Office 365 그룹을 성공적으로 복원 했습니다 tooverify `Get-AzureADGroup –ObjectId <objectId>` hello 그룹에 대 한 cmdlet toodisplay 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="aac04-131">tooverify that you’ve successfully restored an Office 365 group, run hello `Get-AzureADGroup –ObjectId <objectId>` cmdlet toodisplay information about hello group.</span></span> <span data-ttu-id="aac04-132">Hello 복원 후 요청 완료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aac04-132">After hello restore request is completed:</span></span>
- <span data-ttu-id="aac04-133">hello 그룹 교환에 hello 왼쪽된 탐색 모음에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="aac04-133">hello group will appear in hello Left nav bar on Exchange</span></span>
- <span data-ttu-id="aac04-134">hello 계획 hello 그룹에 대 한 계획에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="aac04-134">hello plan for hello group will appear in Planner</span></span>
- <span data-ttu-id="aac04-135">모든 Sharepoint 사이트와 모든 해당 콘텐츠를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac04-135">Any Sharepoint sites and all of their contents will be available</span></span>
- <span data-ttu-id="aac04-136">hello 그룹 hello Exchange 끝점 및 Office 365 그룹을 지 원하는 다른 Office 365 작업 중 하나에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aac04-136">hello group can be accessed from any of hello Exchange endpoints and other Office 365 workloads that support Office 365 groups</span></span>


## <a name="next-steps"></a><span data-ttu-id="aac04-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="aac04-137">Next steps</span></span>
<span data-ttu-id="aac04-138">이러한 문서는 Azure Active Directory 그룹에 대한 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="aac04-138">These articles provide additional information on Azure Active Directory groups.</span></span>

* [<span data-ttu-id="aac04-139">기존 그룹 보기</span><span class="sxs-lookup"><span data-stu-id="aac04-139">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="aac04-140">그룹의 설정 관리</span><span class="sxs-lookup"><span data-stu-id="aac04-140">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="aac04-141">그룹의 멤버 관리</span><span class="sxs-lookup"><span data-stu-id="aac04-141">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="aac04-142">그룹의 멤버 자격 관리</span><span class="sxs-lookup"><span data-stu-id="aac04-142">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="aac04-143">그룹의 사용자에 대한 동적 규칙 관리</span><span class="sxs-lookup"><span data-stu-id="aac04-143">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
