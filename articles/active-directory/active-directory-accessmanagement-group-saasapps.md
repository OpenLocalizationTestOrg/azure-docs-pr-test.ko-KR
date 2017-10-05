---
title: "그룹을 사용하여 SaaS 응용 프로그램에 대한 액세스 관리| Microsoft Docs"
description: "Azure Active Directory Premium 또는 Basic에서 그룹을 사용하여 Azure Active Directory와 통합되는 SaaS 응용 프로그램에 대한 액세스 권한을 할당하는 방법입니다."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: ab8dee63-bedc-46ca-8852-234f5c16ae98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: it-pro;oldportal
ms.openlocfilehash: d350011ee9fc5ced9ddb16993f68d3c840a645a5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="using-a-group-to-manage-access-to-saas-applications"></a><span data-ttu-id="437fc-103">그룹을 사용하여 SaaS 응용 프로그램에 대한 액세스 관리</span><span class="sxs-lookup"><span data-stu-id="437fc-103">Using a group to manage access to SaaS applications</span></span>
<span data-ttu-id="437fc-104">Azure AD Premium 또는 Azure AD Basic 라이선스로 Azure Active Directory(Azure AD)를 사용하는 경우 그룹을 사용하여 Azure AD와 통합되는 SaaS 응용 프로그램에 액세스 권한을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="437fc-104">Using Azure Active Directory (Azure AD) with an Azure AD Premium or Azure AD Basic license, you can use groups to assign access to a SaaS application that's integrated with Azure AD.</span></span> <span data-ttu-id="437fc-105">예를 들어 5가지 SaaS 응용 프로그램을 사용하는 마케팅 부서에 대해 액세스 권한을 할당하려는 경우 마케팅 부서의 사용자가 포함된 그룹을 만든 다음 마케팅 부서에 필요한 이 5가지 SaaS 응용 프로그램에 해당 그룹을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="437fc-105">For example, if you want to assign access for the marketing department to use five different SaaS applications, you can create a group that contains the users in the marketing department, and then assign that group to these five SaaS applications that are needed by the marketing department.</span></span> <span data-ttu-id="437fc-106">이러한 방식으로 한 곳에서 마케팅 부서의 멤버 자격을 관리하여 시간을 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="437fc-106">This way you can save time by managing the membership of the marketing department in one place.</span></span> <span data-ttu-id="437fc-107">사용자는 마케팅 그룹 멤버로 추가되는 경우 응용 프로그램에 할당되고 마케팅 그룹에서 제거되면 응용 프로그램에서 할당이 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="437fc-107">Users then are assigned to the application when they are added as members of the marketing group, and have their assignments removed from the application when they are removed from the marketing group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="437fc-108">이 문서에서 참조되는 Azure 클래식 포털을 사용하는 대신 Azure Portal에서 [Azure AD 관리 센터](https://aad.portal.azure.com)를 사용하여 Azure AD를 관리하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="437fc-108">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> 

<span data-ttu-id="437fc-109">이 기능은 Azure AD 응용 프로그램 갤러리 내에서 추가할 수 있는 수많은 응용 프로그램과 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="437fc-109">This capability can be used with hundreds of applications that you can add from within the Azure AD Application Gallery.</span></span>

<span data-ttu-id="437fc-110">**그룹에 대해 SaaS 응용 프로그램 액세스 권한을 할당하려면**</span><span class="sxs-lookup"><span data-stu-id="437fc-110">**To assign access for a group to a SaaS application**</span></span>

1. <span data-ttu-id="437fc-111">[Azure 클래식 포털](https://manage.windowsazure.com)의 왼쪽 탐색 모음에서 **Active Directory** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="437fc-111">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory** on the navigation bar on the left hand side.</span></span>
2. <span data-ttu-id="437fc-112">**디렉터리** 탭을 선택한 후 그룹에 대해 SaaS 응용 프로그램 액세스 권한을 할당할 디렉터리를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="437fc-112">Select the **Directory** tab, and then open the directory in which you want to assign access for a group to a SaaS application.</span></span>
3. <span data-ttu-id="437fc-113">**응용 프로그램** 탭을 선택합니다. 응용 프로그램 갤러리에서 추가한 응용 프로그램을 선택한 다음 **사용자 및 그룹** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="437fc-113">Select the **Applications** tab. Select an application that you added from the Application Gallery, and then click  the **Users and Groups** tab.</span></span>
4. <span data-ttu-id="437fc-114">**시작** 필드의 **사용자 및 그룹** 탭에 액세스 권한을 할당할 그룹의 이름을 입력하고 오른쪽 위에 있는 확인 표시를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="437fc-114">On the **Users and Groups** tab, in the **Starting with** field, enter the name of the group to which you want to assign access, and then select the check mark in the upper right.</span></span> <span data-ttu-id="437fc-115">그룹 이름의 처음 부분만 입력하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="437fc-115">You only need to type the first part of a group's name.</span></span>
5. <span data-ttu-id="437fc-116">그룹을 선택한 후 **액세스 권한 할당** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="437fc-116">Select the group, then then select the **Assign Access** button.</span></span> <span data-ttu-id="437fc-117">확인 메시지가 표시되면 **예** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="437fc-117">Select **Yes** when you see the confirmation message.</span></span> <span data-ttu-id="437fc-118">중첩 그룹 구성원은 이번 응용 프로그램에 대한 그룹 기반 할당에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="437fc-118">Nested group memberships are not supported for group-based assignment to applications at this time.</span></span>
6. <span data-ttu-id="437fc-119">직접 또는 그룹의 멤버 자격을 통해 응용 프로그램에 할당된 사용자도 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="437fc-119">You can also see which users are assigned to the application, either directly or by membership in a group.</span></span> <span data-ttu-id="437fc-120">이 작업을 수행하려면 **'그룹'에서 드롭다운 표시**를 **'모든 사용자**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="437fc-120">To do this, change the **Show dropdown from 'Groups'** to **'All Users'**.</span></span> <span data-ttu-id="437fc-121">목록은 디렉터리의 사용자와 각 사용자가 응용 프로그램에 할당되었는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="437fc-121">The list shows users in the directory and whether or not each user is assigned to the application.</span></span> <span data-ttu-id="437fc-122">목록은 할당된 사용자가 응용 프로그램에 직접 할당되었는지(할당 형식이 '직접'으로 표시됨) 그룹 멤버 자격에 의해 할당되었는지(할당 형식이 '상속'으로 표시됨) 여부를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="437fc-122">The list also shows whether the assigned users are assigned to the application directly (assignment type shown as 'Direct'), or by virtue of group membership (assignment type shown as 'Inherited.')</span></span>

> [!NOTE]
> <span data-ttu-id="437fc-123">Azure AD Premium 또는 Azure AD Basic을 사용하도록 설정한 후에 사용자 및 그룹 탭을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="437fc-123">You can see the Users and Groups tab only after you have enabled Azure AD Premium or Azure AD Basic.</span></span>
>
>

### <a name="next-steps"></a><span data-ttu-id="437fc-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="437fc-124">Next steps</span></span>
<span data-ttu-id="437fc-125">이러한 문서는 Azure Active Directory에 대한 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="437fc-125">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="437fc-126">Azure Active Directory 그룹을 사용하여 리소스에 대한 액세스 관리</span><span class="sxs-lookup"><span data-stu-id="437fc-126">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="437fc-127">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="437fc-127">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="437fc-128">그룹 설정을 구성하는 Azure Active Directory cmdlets</span><span class="sxs-lookup"><span data-stu-id="437fc-128">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="437fc-129">Azure Active Directory란?</span><span class="sxs-lookup"><span data-stu-id="437fc-129">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="437fc-130">Azure Active Directory와 온-프레미스 ID 통합</span><span class="sxs-lookup"><span data-stu-id="437fc-130">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
