---
title: "Azure Active Directory의 전용 그룹 | Microsoft Docs"
description: "전용된 그룹의 Azure Active Directory를 사용한 작업 방식 및 작성된 방법의 개요입니다."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 86158909-083a-41fe-8090-955e96ad1865
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: d9decd5de6a5bafc525edc5b04c82701185088ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="dedicated-groups-in-azure-active-directory"></a><span data-ttu-id="4b5c9-103">Azure Active Directory의 전용 그룹</span><span class="sxs-lookup"><span data-stu-id="4b5c9-103">Dedicated groups in Azure Active Directory</span></span>
<span data-ttu-id="4b5c9-104">Azure Active Directory(Azure AD)에서 전용 그룹 기능은 Azure AD 미리 정의된 그룹에 대한 멤버 자격을 자동으로 만들고 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="4b5c9-104">In Azure Active Directory (Azure AD), the dedicated groups feature automatically creates and populates membership for Azure AD predefined groups.</span></span> <span data-ttu-id="4b5c9-105">전용 그룹의 멤버를 Azure 클래식 포털, Windows PowerShell cmdlet 또는 프로그래밍 방식으로 추가하거나 제거할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4b5c9-105">Members of dedicated groups cannot be added or removed using the Azure classic portal, Windows PowerShell cmdlets, or programmatically.</span></span>

> [!NOTE]
> <span data-ttu-id="4b5c9-106">전용 그룹에는 할당된 Azure AD Premium 라이선스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4b5c9-106">Dedicated groups require that an Azure AD Premium license is assigned to</span></span>
>
> * <span data-ttu-id="4b5c9-107">그룹의 규칙을 관리하는 관리자</span><span class="sxs-lookup"><span data-stu-id="4b5c9-107">the administrator who manages the rule on a group</span></span>
> * <span data-ttu-id="4b5c9-108">규칙에 따라 그룹의 멤버로 선택된 모든 사용자</span><span class="sxs-lookup"><span data-stu-id="4b5c9-108">all users who are selected by the rule to be a member of the group</span></span>
>
>

<span data-ttu-id="4b5c9-109">**전용 그룹을 사용하도록 설정하려면**</span><span class="sxs-lookup"><span data-stu-id="4b5c9-109">**To enable dedicated groups**</span></span>

1. <span data-ttu-id="4b5c9-110">[Azure 클래식 포털](https://manage.windowsazure.com)에서 **Active Directory**를 선택한 다음 조직의 디렉터리를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4b5c9-110">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="4b5c9-111">**그룹** 탭을 선택하고 편집할 그룹을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4b5c9-111">Select the **Groups** tab, and then open the group you want to edit.</span></span>
3. <span data-ttu-id="4b5c9-112">**구성** 탭을 선택한 다음 **전용 그룹 사용**을 **예**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4b5c9-112">Select the **Configure** tab, and then set **Enable Dedicated Groups** to **Yes**.</span></span>

<span data-ttu-id="4b5c9-113">전용 그룹 사용 스위치가 **예**로 설정되면 **“모든 사용자” 그룹 사용** 스위치를 **예**로 설정하여 모든 사용자 전용 그룹을 자동으로 생성할 디렉터리를 추가로 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b5c9-113">Once the Enable Dedicated Groups switch is set to **Yes**, you can further enable the directory to automatically create the All Users dedicated group by setting the **Enable “All Users” Group** switch to **Yes**.</span></span> <span data-ttu-id="4b5c9-114">그런 다음 **“모든 사용자” 그룹에 표시 이름** 필드에 입력하여 이 전용 그룹의 이름을 편집할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b5c9-114">You can then also edit the name of this dedicated group by typing it in the **Display Name for “All Users” Group** field.</span></span>

<span data-ttu-id="4b5c9-115">디렉터리의 모든 사용자에게 동일한 사용 권한을 할당하려는 경우 모든 사용자 그룹을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b5c9-115">The All Users group can be used to assign the same permissions to all the users in your directory.</span></span> <span data-ttu-id="4b5c9-116">예를 들어 모든 사용자 전용 그룹에 대해 SaaS 응용 프로그램 액세스 권한을 할당하여 디렉터리의 모든 사용자에게 이 응용 프로그램에 대한 액세스를 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b5c9-116">For example, you can grant all users in your directory access to a SaaS application by assigning access for the All Users dedicated group to this application.</span></span>

<span data-ttu-id="4b5c9-117">전용 모든 사용자 그룹은 게스트 및 외부 사용자를 비롯하여 디렉터리의 모든 사용자를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4b5c9-117">The dedicated All Users group includes all users in the directory, including guests and external users.</span></span> <span data-ttu-id="4b5c9-118">외부 사용자를 제외한 그룹이 필요한 경우 아래와 같은 특성 기반 동적 규칙으로 그룹을 만들어 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b5c9-118">If you need a group that excludes external users, then you can accomplish this by creating a group with an attribute-based dynamic rule such as the following:</span></span>

                (user.userPrincipalName -notContains "#EXT#@")

<span data-ttu-id="4b5c9-119">모든 게스트를 제외한 그룹의 경우 아래와 같은 규칙을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4b5c9-119">For a group that excludes all Guests, use a rule such as the following:</span></span>

                (user.userType -ne "Guest")

<span data-ttu-id="4b5c9-120">동적 그룹 멤버 자격에 대한 *고급* 규칙(여러 비교를 포함할 수 있는 규칙)을 만드는 방법에 대해 자세히 알아보려면 [특성을 사용하여 고급 규칙 만들기](active-directory-accessmanagement-groups-with-advanced-rules.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4b5c9-120">To learn about how to create *advanced* rules (rules that can contain multiple comparisons) for dynamic group membership, see [Using attributes to create advanced rules](active-directory-accessmanagement-groups-with-advanced-rules.md).</span></span>

### <a name="next-steps"></a><span data-ttu-id="4b5c9-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4b5c9-121">Next steps</span></span>
<span data-ttu-id="4b5c9-122">이러한 문서는 Azure Active Directory에 대한 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4b5c9-122">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="4b5c9-123">Azure Active Directory 그룹을 사용하여 리소스에 대한 액세스 관리</span><span class="sxs-lookup"><span data-stu-id="4b5c9-123">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="4b5c9-124">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="4b5c9-124">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="4b5c9-125">Azure Active Directory란?</span><span class="sxs-lookup"><span data-stu-id="4b5c9-125">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="4b5c9-126">Azure Active Directory와 온-프레미스 ID 통합</span><span class="sxs-lookup"><span data-stu-id="4b5c9-126">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
