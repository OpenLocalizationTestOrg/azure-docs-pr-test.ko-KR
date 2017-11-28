---
title: "aaaHow toouse 셀프 서비스 응용 프로그램 액세스 | Microsoft Docs"
description: "셀프 서비스 응용 프로그램 액세스 tooallow 사용자 toofind 자신의 응용 프로그램 사용"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviewer: japere
ms.openlocfilehash: 03a44c20d544a6232fa802bcffaf70e5030ad3ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-self-service-application-access"></a><span data-ttu-id="194fa-103">Toouse 셀프 서비스 응용 프로그램 액세스 하는 방법</span><span class="sxs-lookup"><span data-stu-id="194fa-103">How toouse self-service application access</span></span>

<span data-ttu-id="194fa-104">사용자가 액세스 패널에서 응용 프로그램을 검색할 자체 수, 먼저 tooenable **셀프 서비스 응용 프로그램 액세스** tooallow 사용자 tooself 한다고 tooany 응용 프로그램-검색 및 액세스를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="194fa-104">Before your users can self-discover applications from their access panel, you need tooenable **Self-service application access** tooany applications that you wish tooallow users tooself-discover and request access to.</span></span>

<span data-ttu-id="194fa-105">이 기능은 수 있는 좋은 방법을 toosave 시간과 비용은 IT 그룹으로 이며 Azure Active Directory와 최신 응용 프로그램 배포의 일부로 작성 된 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="194fa-105">This feature is a great way for you toosave time and money as an IT group, and is highly recommended as part of a modern applications deployment with Azure Active Directory.</span></span>

<span data-ttu-id="194fa-106">이 기능을 사용하면 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="194fa-106">Using this feature, you can:</span></span>

-   <span data-ttu-id="194fa-107">사용자가 자체 hello에서 응용 프로그램을 검색할 수 있도록 [응용 프로그램 액세스 패널로](https://myapps.microsoft.com/) hello IT 하지 않고 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="194fa-107">Let users self-discover applications from hello [Application Access Panel](https://myapps.microsoft.com/) without bothering hello IT group.</span></span>

-   <span data-ttu-id="194fa-108">액세스를 요청한 사용자가 참조 하,이 대 한 액세스를 제거 하 고 hello 역할 toothem 할당을 관리할 수 있도록 해당 사용자가 tooa 미리 구성 된 그룹을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="194fa-108">Add those users tooa pre-configured group so you can see who has requested access, remove access, and manage hello roles assigned toothem.</span></span>

-   <span data-ttu-id="194fa-109">필요에 따라 비즈니스 승인자 tooapprove 응용 프로그램 액세스 요청을 허용 하므로 IT 그룹이 있어 hello를 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="194fa-109">Optionally allow a business approver tooapprove application access requests so hello IT group doesn’t have to.</span></span>

-   <span data-ttu-id="194fa-110">필요에 따라 too10 개인에 게 액세스 toothis 응용 프로그램을 승인 수를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="194fa-110">Optionally configure up too10 individuals who may approve access toothis application.</span></span>

-   <span data-ttu-id="194fa-111">필요에 따라 비즈니스 승인자 tooset hello 암호를 허용 사용자 צ ְ ײ toosign toohello 응용 프로그램에서는 hello 비즈니스 승인자 로부터 오른쪽 [응용 프로그램 액세스 패널](https://myapps.microsoft.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="194fa-111">Optionally allow a business approver tooset hello passwords those users can use toosign in toohello application, right from hello business approver’s [Application Access Panel](https://myapps.microsoft.com/).</span></span>

-   <span data-ttu-id="194fa-112">필요에 따라 자동으로 할당 된 셀프 서비스 사용자 tooan 응용 프로그램 역할을 직접 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="194fa-112">Optionally automatically assign self-service assigned users tooan application role directly.</span></span>

## <a name="enable-self-service-application-access-tooallow-users-toofind-their-own-applications"></a><span data-ttu-id="194fa-113">셀프 서비스 응용 프로그램 액세스 tooallow 사용자 toofind 자신의 응용 프로그램 사용</span><span class="sxs-lookup"><span data-stu-id="194fa-113">Enable self-service application access tooallow users toofind their own applications</span></span>

<span data-ttu-id="194fa-114">셀프 서비스 응용 프로그램 액세스는 좋은 방법 tooallow 사용자 tooself-필요에 따라 hello 비즈니스 그룹 액세스 하도록 허용 tooapprove toothose 응용 프로그램, 응용 프로그램을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="194fa-114">Self-service application access is a great way tooallow users tooself-discover applications, optionally allow hello business group tooapprove access toothose applications.</span></span> <span data-ttu-id="194fa-115">Hello 비즈니스 그룹 toomanage hello 자격 증명 toothose 사용자가 액세스 패널에서 응용 프로그램에 Single-sign 암호 오른쪽에 대 한 할당을 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="194fa-115">You can allow hello business group toomanage hello credentials assigned toothose users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="194fa-116">tooenable 셀프 서비스 응용 프로그램 액세스 tooan 응용 프로그램, 다음 단계에 따라 hello:</span><span class="sxs-lookup"><span data-stu-id="194fa-116">tooenable self-service application access tooan application, follow hello steps below:</span></span>

1.  <span data-ttu-id="194fa-117">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="194fa-117">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="194fa-118">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="194fa-118">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="194fa-119">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="194fa-119">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="194fa-120">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="194fa-120">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="194fa-121">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="194fa-121">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="194fa-122">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="194fa-122">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="194fa-123">Tooenable 셀프 서비스 액세스 toofrom hello 목록을 사용 하려는 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="194fa-123">Select hello application you want tooenable Self-service access toofrom hello list.</span></span>

7.  <span data-ttu-id="194fa-124">Hello 응용 프로그램 로드 되 면 클릭 **셀프 서비스** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="194fa-124">Once hello application loads, click **Self-service** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="194fa-125">이 응용 프로그램에 대 한 셀프 서비스 응용 프로그램 액세스 tooenable hello 설정 **toorequest access toothis 응용 프로그램 사용자가 허용?** 너무 설정/해제**예입니다.**</span><span class="sxs-lookup"><span data-stu-id="194fa-125">tooenable Self-service application access for this application, turn hello **Allow users toorequest access toothis application?** toggle too**Yes.**</span></span>

9.  <span data-ttu-id="194fa-126">Tooselect hello 그룹 toowhich 요청 하는 사용자 액세스 toothis 응용 프로그램을 추가 하도록 hello 선택기 다음 toohello 레이블을 클릭 하는 다음으로, **toowhich 그룹은 할당 된 사용자를 추가할 수?** 그룹을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="194fa-126">Next, tooselect hello group toowhich users who request access toothis application should be added, click hello selector next toohello label **toowhich group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="194fa-127">**선택 사항:** 원할 경우 toorequire 비즈니스 승인 사용자의 액세스가 허용 되기 전에 설정 hello **toothis 응용 프로그램 액세스 권한을 부여 하기 전에 승인 필요?** 너무 설정/해제**예**합니다.</span><span class="sxs-lookup"><span data-stu-id="194fa-127">**Optional:** If you wish toorequire a business approval before users are allowed access, set hello **Require approval before granting access toothis application?** toggle too**Yes**.</span></span>

11. <span data-ttu-id="194fa-128">**선택 사항:에 대 한 응용 프로그램에서 사용 하 여 암호 단일 로그인만** toothis 응용 프로그램 승인 된 사용자가을 전송 하는 이러한 비즈니스 승인자 toospecify hello 암호 tooallow 하려는 경우 설정 hello **승인자 tooset 허용 이 응용 프로그램에 대 한 사용자의 암호?**  너무 설정/해제**예**합니다.</span><span class="sxs-lookup"><span data-stu-id="194fa-128">**Optional: For applications using password single-sign on only,** if you wish tooallow those business approvers toospecify hello passwords that are sent toothis application for approved users, set hello **Allow approvers tooset user’s passwords for this application?** toggle too**Yes**.</span></span>

12. <span data-ttu-id="194fa-129">**선택 사항:** tooapprove access toothis 응용 프로그램 수 있는 toospecify hello 비즈니스 승인자 hello 선택기 다음 toohello 레이블을 클릭 **tooapprove 액세스 toothis 응용 프로그램이 허용 되는 사용자?** tooselect를 too10 개별 비즈니스 승인자 합니다.</span><span class="sxs-lookup"><span data-stu-id="194fa-129">**Optional:** toospecify hello business approvers who are allowed tooapprove access toothis application, click hello selector next toohello label **Who is allowed tooapprove access toothis application?** tooselect up too10 individual business approvers.</span></span>

   * <span data-ttu-id="194fa-130">그룹은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="194fa-130">Groups are not supported.</span></span>

13. <span data-ttu-id="194fa-131">**선택 사항:** **역할을 표시 하는 응용 프로그램에 대 한**tooassign 승인 된 사용자가 셀프 서비스 tooa 역할 하려는 경우, hello 선택기 다음 toohello 클릭 **toowhich 역할이이 사용자가 할당 해야 응용 프로그램?**  tooselect hello 역할 toowhich 이러한 사용자만 할당 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="194fa-131">**Optional:** **For applications which expose roles**, if you wish tooassign self-service approved users tooa role, click hello selector next toohello **toowhich role should users be assigned in this application?** tooselect hello role toowhich these users should be assigned.</span></span>

14. <span data-ttu-id="194fa-132">Hello 클릭 **저장** hello 블레이드 toofinish hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="194fa-132">Click hello **Save** button at hello top of hello blade toofinish.</span></span>

<span data-ttu-id="194fa-133">셀프 서비스 응용 프로그램 구성을 완료 한 후 탐색할 수 tootheir [응용 프로그램 액세스 패널로](https://myapps.microsoft.com/) hello를 클릭 하 고 **+ 추가** 단추 toofind hello 앱 toowhich 사용 하도록 설정한 셀프 서비스 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="194fa-133">Once you complete Self-service application configuration, users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled Self-service access.</span></span> <span data-ttu-id="194fa-134">비즈니스 승인자는 [응용 프로그램 액세스 패널](https://myapps.microsoft.com/)에서 알림을 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="194fa-134">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="194fa-135">사용자가 승인을 해야 하는 액세스 tooan 응용 프로그램을 요청 하는 경우 사용자에 게 알리는 전자 메일을 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="194fa-135">You can enable an email notifying them when a user has requested access tooan application that requires their approval.</span></span> 

<span data-ttu-id="194fa-136">이러한 승인은 단일 승인 워크플로만, 여러 승인자를 지정 하면 모든 단일 승인자 수 액세스 toohello 응용 프로그램이 승인 의미를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="194fa-136">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approve access toohello application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="194fa-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="194fa-137">Next steps</span></span>
[<span data-ttu-id="194fa-138">셀프 서비스 그룹 관리를 위한 Azure Active Directory 설정</span><span class="sxs-lookup"><span data-stu-id="194fa-138">Setting up Azure Active Directory for self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
