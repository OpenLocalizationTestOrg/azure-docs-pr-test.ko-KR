---
title: "Azure Active Directory에서 Office 365 그룹 만료 미리 보기 | Microsoft Docs"
description: "Azure Active Directory에서 Office 365 그룹에 대한 만료를 설정하는 방법(미리 보기)"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: it-pro
ms.openlocfilehash: 8a43df84fd050d7b4bd8d937b8c55e744cb805d3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-office-365-groups-expiration-preview"></a><span data-ttu-id="d60fb-103">Office 365 그룹 만료 구성(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="d60fb-103">Configure Office 365 groups expiration (preview)</span></span>

<span data-ttu-id="d60fb-104">이제 선택하는 모든 Office 365 그룹에 대한 만료를 설정하여 Office 365 그룹의 수명 주기를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d60fb-104">You can now manage the lifecycle of Office 365 groups by setting expiration for any Office 365 groups that you select.</span></span> <span data-ttu-id="d60fb-105">이 만료가 설정되면 해당 그룹의 소유자는 그룹이 여전히 필요한 경우 해당 그룹을 갱신할지 묻는 메시지를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="d60fb-105">Once this expiration is set, owners of those groups are asked to renew their groups if they still need the groups.</span></span> <span data-ttu-id="d60fb-106">갱신되지 않은 Office 365 그룹은 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="d60fb-106">Any Office 365 group that is not renewed will be deleted.</span></span> <span data-ttu-id="d60fb-107">삭제된 Office 365 그룹은 그룹 소유자 또는 관리자에 의해 30일 이내로 복원될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d60fb-107">Any Office 365 group that was deleted can be restored within 30 days by the group owners or the administrator.</span></span>  


> [!NOTE]
> <span data-ttu-id="d60fb-108">Office 365 그룹에 대해서만 만료를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d60fb-108">You can set expiration for only Office 365 groups.</span></span>
>
> <span data-ttu-id="d60fb-109">O365 그룹에 대한 만료 설정에는 할당된 Azure AD Premium 라이선스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d60fb-109">Setting expiration for O365 groups requires that an Azure AD Premium license is assigned to</span></span>
>   - <span data-ttu-id="d60fb-110">테넌트에 대한 만료 설정을 구성하는 관리자</span><span class="sxs-lookup"><span data-stu-id="d60fb-110">The administrator who configures the expiration settings for the tenant</span></span>
>   - <span data-ttu-id="d60fb-111">이 설정에 대해 선택한 그룹의 모든 멤버</span><span class="sxs-lookup"><span data-stu-id="d60fb-111">All members of the groups selected for this setting</span></span>

## <a name="set-office-365-groups-expiration"></a><span data-ttu-id="d60fb-112">Office 365 그룹 만료 설정</span><span class="sxs-lookup"><span data-stu-id="d60fb-112">Set Office 365 groups expiration</span></span>

1. <span data-ttu-id="d60fb-113">Azure AD 테넌트에서 전역 관리자인 계정으로 [Azure AD 관리 센터](https://aad.portal.azure.com)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d60fb-113">Open the [Azure AD admin center](https://aad.portal.azure.com) with an account that is a global administrator in your Azure AD tenant.</span></span>

2. <span data-ttu-id="d60fb-114">Azure AD를 열고 **사용자 및 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d60fb-114">Open Azure AD, select **Users and groups**.</span></span>

3. <span data-ttu-id="d60fb-115">**그룹 설정**을 선택한 다음 **만료**를 선택하여 만료 설정을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d60fb-115">Select **Group settings** and then select **Expiration** to open the expiration settings.</span></span>
  
  ![만료 블레이드](./media/active-directory-groups-lifecycle-azure-portal/expiration-settings.png)

4. <span data-ttu-id="d60fb-117">**만료** 블레이드에서 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d60fb-117">On the **Expiration** blade, you can:</span></span>

  * <span data-ttu-id="d60fb-118">일 단위로 그룹 수명을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d60fb-118">Set the group lifetime in days.</span></span> <span data-ttu-id="d60fb-119">미리 설정된 값 중 하나 또는 사용자 지정 값을 선택할 수 있습니다(31일 이상이어야 함).</span><span class="sxs-lookup"><span data-stu-id="d60fb-119">You could select one of the preset values, or a custom value (should be 31 days or more).</span></span> 
  * <span data-ttu-id="d60fb-120">그룹에 소유자가 없는 경우 갱신 및 만료 알림이 전송되어야 하는 전자 메일 주소를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d60fb-120">Specify an email address where the renewal and expiration notifications should be sent when a group has no owner.</span></span> 
  * <span data-ttu-id="d60fb-121">만료되는 Office 365 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d60fb-121">Select which Office 365 groups expire.</span></span> <span data-ttu-id="d60fb-122">**모든** Office 365 그룹에 대한 만료를 설정할 수 있고, Office 365 그룹 중에서 선택하거나 모든 그룹에 대해 만료를 비활성화하도록 선택하지 **않을** 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d60fb-122">You can enable expiration for **All** Office 365 groups, you can select from among the Office 365 groups, or you select **None** to disable expiration for all groups.</span></span>
  * <span data-ttu-id="d60fb-123">완료되면 **저장**을 선택하여 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d60fb-123">Save your settings when you're done by selecting **Save**.</span></span>

<span data-ttu-id="d60fb-124">PowerShell 통해 Office 365 그룹에 대한 만료를 구성하는 Microsoft PowerShell 모듈을 다운로드하고 설치하는 방법에 대한 지침은 [Azure Active Directory V2 PowerShell 모듈 - 공개 미리 보기 릴리스 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d60fb-124">For instructions on how to download and install the Microsoft PowerShell module to configure expiration for Office 365 groups via PowerShell, see [Azure Active Directory V2 PowerShell Module - Public Preview Release 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137).</span></span>

<span data-ttu-id="d60fb-125">이와 같은 전자 메일 알림은 그룹의 만료 30일, 15일 및 1일 전에 Office 365 그룹 소유자에게 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="d60fb-125">Email notifications such as this one are sent to the Office 365 group owners 30 days, 15 days, and 1 day prior to expiration of the group.</span></span>

![만료 전자 메일 알림](./media/active-directory-groups-lifecycle-azure-portal/expiration-notification.png)

<span data-ttu-id="d60fb-127">그룹 소유자는 **그룹 갱신**을 선택하여 Office 365 그룹을 갱신하거나 **그룹으로 이동**을 선택하여 구성원과 그룹에 대한 기타 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d60fb-127">The group owner can then select **Renew group** to renew the Office 365 group, or can select **Go to group** to see the members and other details about the group.</span></span>

<span data-ttu-id="d60fb-128">그룹이 만료되면 그룹은 만료 날짜 1일 후에 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="d60fb-128">When a group expires, the group is deleted one day after the expiration date.</span></span> <span data-ttu-id="d60fb-129">Office 365 그룹의 만료 및 후속 삭제에 대해 알려주는 이와 같은 전자 메일 알림은 Office 365 그룹 소유자에게 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="d60fb-129">An email notification such as this one is sent to the Office 365 group owners informing them about the expiration and subsequent deletion of their Office 365 group.</span></span>

![그룹 삭제 전자 메일 알림](./media/active-directory-groups-lifecycle-azure-portal/deletion-notification.png)

<span data-ttu-id="d60fb-131">[Azure Active Directory에서 삭제된 Office 365 그룹 복원](https://docs.microsoft.com/azure/active-directory/active-directory-groups-restore-azure-portal)에서 설명된 대로 **그룹 복원**을 선택하거나 PowerShell cmdlet을 사용하여 그룹을 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d60fb-131">The group can be restored by selecting **Restore group** or by using PowerShell cmdlets, as described in [Restore a deleted Office 365 group in Azure Active Directory] (https://docs.microsoft.com/azure/active-directory/active-directory-groups-restore-azure-portal).</span></span>
    
<span data-ttu-id="d60fb-132">복원하는 그룹에 문서, SharePoint 사이트 또는 기타 영구 개체가 포함된 경우 그룹 및 해당 내용을 완전히 복원하는 데 최대 24시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d60fb-132">If the group you're restoring contains documents, SharePoint sites, or other persistent objects, it might take up to 24 hours to fully restore the group and its contents.</span></span>

> [!NOTE]
> * <span data-ttu-id="d60fb-133">만료 설정을 배포하는 경우 만료 기간보다 오래된 일부 그룹이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d60fb-133">When deploying the expiration settings, there might be some groups that are older than the expiration window.</span></span> <span data-ttu-id="d60fb-134">이러한 그룹은 즉시 삭제되지 않지만 만료까지 30일로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="d60fb-134">These groups are not be immediately deleted, but are set to 30 days until expiration.</span></span> <span data-ttu-id="d60fb-135">하루 이내로 첫 번째 갱신 알림 전자 메일이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="d60fb-135">The first renewal notification email is sent out within a day.</span></span> <span data-ttu-id="d60fb-136">예를 들어 그룹 A가 400일 전에 만들어졌으며 만료 기간은 180일로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="d60fb-136">For example, Group A was created 400 days ago, and the expiration interval is set to 180 days.</span></span> <span data-ttu-id="d60fb-137">만료 설정을 적용하면 그룹 A는 소유자가 갱신하지 않는 한 삭제되기 전에 30일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d60fb-137">When you apply expiration settings, Group A has 30 days before it is deleted, unless the owner renews it.</span></span>
> * <span data-ttu-id="d60fb-138">동적 그룹이 삭제되고 복원되는 경우 새 그룹으로 표시되며 규칙에 따라 다시 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="d60fb-138">When a dynamic group is deleted and restored, it is seen as a new group and re-populated according to the rule.</span></span> <span data-ttu-id="d60fb-139">이 프로세스는 최대 24시간까지 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d60fb-139">This process might take up to 24 hours.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d60fb-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d60fb-140">Next steps</span></span>
<span data-ttu-id="d60fb-141">이러한 문서는 Azure AD 그룹에 대한 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d60fb-141">These articles provide additional information on Azure AD groups.</span></span>

* [<span data-ttu-id="d60fb-142">기존 그룹 보기</span><span class="sxs-lookup"><span data-stu-id="d60fb-142">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="d60fb-143">그룹의 설정 관리</span><span class="sxs-lookup"><span data-stu-id="d60fb-143">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="d60fb-144">그룹의 멤버 관리</span><span class="sxs-lookup"><span data-stu-id="d60fb-144">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="d60fb-145">그룹의 멤버 자격 관리</span><span class="sxs-lookup"><span data-stu-id="d60fb-145">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="d60fb-146">그룹의 사용자에 대한 동적 규칙 관리</span><span class="sxs-lookup"><span data-stu-id="d60fb-146">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
