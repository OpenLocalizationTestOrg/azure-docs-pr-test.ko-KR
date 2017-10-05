---
title: "그룹을 사용하는 액세스 관리의 다음 단계 | Microsoft Docs"
description: "보안 그룹 관리에 대한 고급 방법과 이러한 그룹을 사용하여 리소스에 대한 액세스를 관리하는 방법입니다."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 44350a3c-8ea1-4da1-aaac-7fc53933dd21
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 82fbeb379e90add09f7c569111053f6e9b1bc9c5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="managing-owners-for-a-group"></a><span data-ttu-id="28115-103">그룹에 대한 소유자 관리</span><span class="sxs-lookup"><span data-stu-id="28115-103">Managing owners for a group</span></span>
<span data-ttu-id="28115-104">리소스 소유자가 Azure AD 그룹에 리소스에 대한 액세스 권한을 할당하면 그룹의 멤버 자격은 그룹 소유자에 의해 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="28115-104">Once a resource owner has assigned access to a resource to an Azure AD group, the membership of the group is managed by the group owner.</span></span> <span data-ttu-id="28115-105">실질적으로 리소스 소유자는 사용자를 해당 리소스에 할당할 권한을 그룹 소유자에게 위임합니다.</span><span class="sxs-lookup"><span data-stu-id="28115-105">The resource owner effectively delegates the permission to assign users to the resource to the owner of the group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="28115-106">이 문서에서 참조되는 Azure 클래식 포털을 사용하는 대신 Azure Portal에서 [Azure AD 관리 센터](https://aad.portal.azure.com)를 사용하여 Azure AD를 관리하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="28115-106">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> 

## <a name="assigning-group-ownership"></a><span data-ttu-id="28115-107">그룹 소유권 할당</span><span class="sxs-lookup"><span data-stu-id="28115-107">Assigning group ownership</span></span>
<span data-ttu-id="28115-108">**그룹에 소유자를 추가하려면**</span><span class="sxs-lookup"><span data-stu-id="28115-108">**To add an owner to a group**</span></span>

1. <span data-ttu-id="28115-109">[Azure 클래식 포털](https://manage.windowsazure.com)에서 **Active Directory**를 선택한 다음 조직의 디렉터리를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="28115-109">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="28115-110">**그룹** 탭을 선택하고 소유자를 추가할 편집할 그룹을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="28115-110">Select the **Groups** tab, and then open the group that you want to add owners to.</span></span>
3. <span data-ttu-id="28115-111">**소유자 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="28115-111">Select **Add Owners**.</span></span>
4. <span data-ttu-id="28115-112">**소유자 추가** 페이지에서 이 그룹의 소유자로 추가할 사용자를 선택하고 이 이름이 **선택 항목** 창에 추가되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="28115-112">On the **Add owners** page, select the user that you want to add as the owner of this group, and make sure this name is added to the **Selected** pane.</span></span>

<span data-ttu-id="28115-113">**그룹에서 소유자를 제거하려면**</span><span class="sxs-lookup"><span data-stu-id="28115-113">**To remove an owner from a group**</span></span>

1. <span data-ttu-id="28115-114">[Azure 클래식 포털](https://manage.windowsazure.com)에서 **Active Directory**를 선택한 다음 조직의 디렉터리를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="28115-114">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="28115-115">**그룹** 탭을 선택하고 소유자를 제거할 그룹을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="28115-115">Select the **Groups** tab, and then open the group that you want to remove an owner from.</span></span>
3. <span data-ttu-id="28115-116">**소유자** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="28115-116">Select the **Owners** tab.</span></span>
4. <span data-ttu-id="28115-117">이 그룹에서 제거할 소유자를 선택한 후 **제거**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="28115-117">Select the owner that you want to remove from this group, and then select **Remove**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="28115-118">추가 정보</span><span class="sxs-lookup"><span data-stu-id="28115-118">Additional information</span></span>
<span data-ttu-id="28115-119">이러한 문서는 Azure Active Directory에 대한 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="28115-119">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="28115-120">Azure Active Directory 그룹을 사용하여 리소스에 대한 액세스 관리</span><span class="sxs-lookup"><span data-stu-id="28115-120">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="28115-121">그룹 설정을 구성하는 Azure Active Directory cmdlet</span><span class="sxs-lookup"><span data-stu-id="28115-121">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="28115-122">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="28115-122">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="28115-123">Azure Active Directory란?</span><span class="sxs-lookup"><span data-stu-id="28115-123">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="28115-124">Azure Active Directory와 온-프레미스 ID 통합</span><span class="sxs-lookup"><span data-stu-id="28115-124">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
