---
title: "응용 프로그램 그룹 toomanage 액세스 tooSaaS aaaUsing | Microsoft Docs"
description: "어떻게 Azure Active Directory Premium 또는 Basic tooassign toouse 그룹 Azure Active Directory와 통합 된 tooSaaS 응용 프로그램에 액세스 합니다."
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
ms.openlocfilehash: f45ea4472b3d88e8ea514af3db31b4cc9ea68d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-a-group-toomanage-access-toosaas-applications"></a><span data-ttu-id="e3252-103">그룹 toomanage 액세스 tooSaaS 응용 프로그램을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e3252-103">Using a group toomanage access tooSaaS applications</span></span>
<span data-ttu-id="e3252-104">Azure Active Directory (Azure AD)를 사용 하 여 Azure AD Premium 또는 Azure AD Basic 라이선스를 그룹 tooassign access tooa SaaS 응용 프로그램을 Azure AD와 통합을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3252-104">Using Azure Active Directory (Azure AD) with an Azure AD Premium or Azure AD Basic license, you can use groups tooassign access tooa SaaS application that's integrated with Azure AD.</span></span> <span data-ttu-id="e3252-105">예를 들어 hello 마케팅 부서 toouse 5 개의 서로 다른 SaaS 응용 프로그램에 대 한 tooassign 액세스 하려는 경우 있습니다 hello 마케팅 부서의 hello 사용자가 포함 하는 그룹을 만든 다음 해당 그룹 toothese 5 개 SaaS 응용 프로그램을 hello 마케팅 부서에서 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e3252-105">For example, if you want tooassign access for hello marketing department toouse five different SaaS applications, you can create a group that contains hello users in hello marketing department, and then assign that group toothese five SaaS applications that are needed by hello marketing department.</span></span> <span data-ttu-id="e3252-106">이러한 방식으로 hello 마케팅 부서의 한 곳에서의 hello 멤버 자격을 관리 하 여 시간을 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3252-106">This way you can save time by managing hello membership of hello marketing department in one place.</span></span> <span data-ttu-id="e3252-107">사용자가 다음 때 할당 됩니다 toohello 응용 프로그램 hello 마케팅 그룹의 구성원으로 추가 되 고 할당 제거는 hello 응용 프로그램에서 hello 마케팅 그룹에서에서 제거 될 때.</span><span class="sxs-lookup"><span data-stu-id="e3252-107">Users then are assigned toohello application when they are added as members of hello marketing group, and have their assignments removed from hello application when they are removed from hello marketing group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e3252-108">Hello를 사용 하 여 Azure AD를 관리 하는 것이 좋습니다 [Azure AD 관리 센터](https://aad.portal.azure.com) hello에서 사용 하는 대신 Azure 포털 hello Azure 클래식 포털이이 문서에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3252-108">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> 

<span data-ttu-id="e3252-109">Hello Azure AD 응용 프로그램 갤러리 내에서 추가할 수 있는 수많은 응용 프로그램으로이 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3252-109">This capability can be used with hundreds of applications that you can add from within hello Azure AD Application Gallery.</span></span>

<span data-ttu-id="e3252-110">**그룹 tooa SaaS 응용 프로그램에 대 한 tooassign 액세스**</span><span class="sxs-lookup"><span data-stu-id="e3252-110">**tooassign access for a group tooa SaaS application**</span></span>

1. <span data-ttu-id="e3252-111">Hello에 [Azure 클래식 포털](https://manage.windowsazure.com)선택, **Active Directory** hello hello 왼쪽 탐색 모음에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3252-111">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory** on hello navigation bar on hello left hand side.</span></span>
2. <span data-ttu-id="e3252-112">선택 hello **디렉터리** 탭을 연 다음 hello 디렉터리 그룹 tooa SaaS 응용 프로그램에 대 한 액세스 tooassign 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3252-112">Select hello **Directory** tab, and then open hello directory in which you want tooassign access for a group tooa SaaS application.</span></span>
3. <span data-ttu-id="e3252-113">선택 hello **응용 프로그램** 탭 합니다. Hello 응용 프로그램 갤러리에서에서 추가 하는 응용 프로그램을 선택 하 고 클릭 hello **사용자 및 그룹** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3252-113">Select hello **Applications** tab. Select an application that you added from hello Application Gallery, and then click  hello **Users and Groups** tab.</span></span>
4. <span data-ttu-id="e3252-114">Hello에 **사용자 및 그룹** hello 탭 **부터는** 필드 hello 이름을 입력 hello 그룹 toowhich의 tooassign 액세스 한 다음 선택 hello hello 오른쪽 위에 있는 확인 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3252-114">On hello **Users and Groups** tab, in hello **Starting with** field, enter hello name of hello group toowhich you want tooassign access, and then select hello check mark in hello upper right.</span></span> <span data-ttu-id="e3252-115">그룹의 이름의 tootype hello 첫 번째 부분을 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3252-115">You only need tootype hello first part of a group's name.</span></span>
5. <span data-ttu-id="e3252-116">Hello 그룹을 선택 하 고 다음 hello 선택 **할당 액세스 권한** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e3252-116">Select hello group, then then select hello **Assign Access** button.</span></span> <span data-ttu-id="e3252-117">선택 **예** hello 확인 메시지가 표시 될 때입니다.</span><span class="sxs-lookup"><span data-stu-id="e3252-117">Select **Yes** when you see hello confirmation message.</span></span> <span data-ttu-id="e3252-118">이 이번에 중첩 된 그룹 멤버 자격 그룹 기반 할당 tooapplications에 대 한 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e3252-118">Nested group memberships are not supported for group-based assignment tooapplications at this time.</span></span>
6. <span data-ttu-id="e3252-119">직접 또는 그룹 멤버 자격에 따라 toohello 응용 프로그램에 할당 되는 사용자를 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3252-119">You can also see which users are assigned toohello application, either directly or by membership in a group.</span></span> <span data-ttu-id="e3252-120">toodo이, 변경 hello **드롭다운 '그룹'에서 표시** 너무**' 모든 사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="e3252-120">toodo this, change hello **Show dropdown from 'Groups'** too**'All Users'**.</span></span> <span data-ttu-id="e3252-121">hello 목록 hello 디렉터리 및 여부는 각 사용자가 할당 된 toohello 응용 프로그램에 사용자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3252-121">hello list shows users in hello directory and whether or not each user is assigned toohello application.</span></span> <span data-ttu-id="e3252-122">hello 할당 된 사용자에 게 할당 toohello 응용 프로그램 직접 (할당 유형이 '직접'으로 표시), 있는지 아니면 그룹 멤버 자격 (할당 유형이 '상속 됨'으로 표시) hello 목록 표시</span><span class="sxs-lookup"><span data-stu-id="e3252-122">hello list also shows whether hello assigned users are assigned toohello application directly (assignment type shown as 'Direct'), or by virtue of group membership (assignment type shown as 'Inherited.')</span></span>

> [!NOTE]
> <span data-ttu-id="e3252-123">Azure AD Premium 또는 Azure AD Basic 사용 하도록 설정한 후에 hello 사용자 및 그룹 탭을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3252-123">You can see hello Users and Groups tab only after you have enabled Azure AD Premium or Azure AD Basic.</span></span>
>
>

### <a name="next-steps"></a><span data-ttu-id="e3252-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e3252-124">Next steps</span></span>
<span data-ttu-id="e3252-125">이러한 문서는 Azure Active Directory에 대한 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e3252-125">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="e3252-126">Azure Active Directory 그룹을 사용 하 여 액세스 tooresources 관리</span><span class="sxs-lookup"><span data-stu-id="e3252-126">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="e3252-127">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="e3252-127">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="e3252-128">그룹 설정을 구성하는 Azure Active Directory cmdlets</span><span class="sxs-lookup"><span data-stu-id="e3252-128">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="e3252-129">Azure Active Directory란?</span><span class="sxs-lookup"><span data-stu-id="e3252-129">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="e3252-130">Azure Active Directory와 온-프레미스 ID 통합</span><span class="sxs-lookup"><span data-stu-id="e3252-130">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
