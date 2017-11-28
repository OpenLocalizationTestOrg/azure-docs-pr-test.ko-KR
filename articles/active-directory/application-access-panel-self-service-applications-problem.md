---
title: "셀프 서비스 응용 프로그램 액세스를 사용 하 여 aaaProblem | Microsoft Docs"
description: "문제 관련된 tooself 서비스 응용 프로그램 액세스 문제 해결"
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
ms.openlocfilehash: 2487be1df191a4e7fd0bcc0ebbe4ea62fae0fd5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-using-self-service-application-access"></a><span data-ttu-id="07ecf-103">셀프 서비스 응용 프로그램 액세스를 사용할 때 발생하는 문제</span><span class="sxs-lookup"><span data-stu-id="07ecf-103">Problem using self-service application access</span></span>

<span data-ttu-id="07ecf-104">셀프 서비스 응용 프로그램 액세스는 좋은 방법 tooallow 사용자 tooself-필요에 따라 hello 비즈니스 그룹 액세스 하도록 허용 tooapprove toothose 응용 프로그램, 응용 프로그램을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="07ecf-104">Self-service application access is a great way tooallow users tooself-discover applications, optionally allow hello business group tooapprove access toothose applications.</span></span> <span data-ttu-id="07ecf-105">Hello 비즈니스 그룹 toomanage hello 자격 증명 toothose 사용자가 액세스 패널에서 응용 프로그램에 Single-sign 암호 오른쪽에 대 한 할당을 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07ecf-105">You can allow hello business group toomanage hello credentials assigned toothose users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="07ecf-106">사용자가 액세스 패널에서 응용 프로그램을 검색할 자체 수, 먼저 tooenable **셀프 서비스 응용 프로그램 액세스** tooallow 사용자 tooself 한다고 tooany 응용 프로그램-검색 및 액세스를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="07ecf-106">Before your users can self-discover applications from their access panel, you need tooenable **Self-service application access** tooany applications that you wish tooallow users tooself-discover and request access to.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="07ecf-107">일반 toocheck를 먼저 문제</span><span class="sxs-lookup"><span data-stu-id="07ecf-107">General issues toocheck first</span></span>

-   <span data-ttu-id="07ecf-108">셀프 서비스 응용 프로그램 액세스가 올바르게 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="07ecf-108">Make sure self-service application access is configured correctly.</span></span> <span data-ttu-id="07ecf-109">"어떻게 tooconfigure 셀프 서비스 응용 프로그램 액세스"를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="07ecf-109">See “How tooconfigure self-service application access”.</span></span>

-   <span data-ttu-id="07ecf-110">Hello 사용자 또는 그룹 되어 있는지 확인 toorequest 셀프 서비스 응용 프로그램 액세스를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="07ecf-110">Make sure hello user or group has been enabled toorequest self-service application access.</span></span>

-   <span data-ttu-id="07ecf-111">셀프 서비스 응용 프로그램 액세스에 대 한 hello 올바른 위치를 방문 하는 hello 사용자가 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="07ecf-111">Make sure hello user is visiting hello correct place for self-service application access.</span></span> <span data-ttu-id="07ecf-112">사용자가 tootheir 탐색할 수 [응용 프로그램 액세스 패널로](https://myapps.microsoft.com/) hello를 클릭 하 고 **+ 추가** 단추 toofind hello 앱 toowhich 셀프 서비스 액세스 사용 하도록 설정한 합니다.</span><span class="sxs-lookup"><span data-stu-id="07ecf-112">users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled self-service access.</span></span>

-   <span data-ttu-id="07ecf-113">셀프 서비스 응용 프로그램 액세스를 최근에 구성 하는 경우 다시 toosign 및 축소 hello 사용자의 액세스 패널에 몇 분 toosee 후 hello 셀프 서비스 액세스 변경 이전에 표시 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="07ecf-113">If self-service application access was just recently configured, try toosign in and out again into hello user’s Access Panel after a few minutes toosee if hello self-service access changes have appeared.</span></span>

## <a name="how-tooconfigure-self-service-application-access"></a><span data-ttu-id="07ecf-114">Tooconfigure 셀프 서비스 응용 프로그램 액세스 하는 방법</span><span class="sxs-lookup"><span data-stu-id="07ecf-114">How tooconfigure self-service application access</span></span>

<span data-ttu-id="07ecf-115">tooenable 셀프 서비스 응용 프로그램 액세스 tooan 응용 프로그램, 다음 단계에 따라 hello:</span><span class="sxs-lookup"><span data-stu-id="07ecf-115">tooenable self-service application access tooan application, follow hello steps below:</span></span>

1.  <span data-ttu-id="07ecf-116">열기 hello [ **Azure 포털** ](https://portal.azure.com/) 로 로그인 한 **전역 관리자입니다.**</span><span class="sxs-lookup"><span data-stu-id="07ecf-116">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="07ecf-117">열기 hello **Azure Active Directory 확장** 클릭 하 여 **더 많은 서비스** hello hello 주 왼쪽 탐색 메뉴 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07ecf-117">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="07ecf-118">에 입력 **"Azure Active Directory**" hello 필터 검색 상자와 선택 hello **Azure Active Directory** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="07ecf-118">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="07ecf-119">클릭 **엔터프라이즈 응용 프로그램** hello Azure Active Directory 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="07ecf-119">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="07ecf-120">클릭 **모든 응용 프로그램** tooview 모든 응용 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="07ecf-120">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="07ecf-121">여기에 표시 하려는 hello 응용 프로그램을 표시 되지 않으면 hello를 사용 하 여 **필터** hello 위쪽 hello에 대 한 제어 **모든 응용 프로그램 목록** 및 집합 hello **표시** 옵션 **모든 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="07ecf-121">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="07ecf-122">Tooenable 셀프 서비스 액세스 toofrom hello 목록을 사용 하려는 hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="07ecf-122">Select hello application you want tooenable Self-service access toofrom hello list.</span></span>

7.  <span data-ttu-id="07ecf-123">Hello 응용 프로그램 로드 되 면 클릭 **셀프 서비스** hello 응용 프로그램의 왼쪽 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="07ecf-123">Once hello application loads, click **Self-service** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="07ecf-124">이 응용 프로그램에 대 한 셀프 서비스 응용 프로그램 액세스 tooenable hello 설정 **toorequest access toothis 응용 프로그램 사용자가 허용?** 너무 설정/해제**예입니다.**</span><span class="sxs-lookup"><span data-stu-id="07ecf-124">tooenable Self-service application access for this application, turn hello **Allow users toorequest access toothis application?** toggle too**Yes.**</span></span>

9.  <span data-ttu-id="07ecf-125">Tooselect hello 그룹 toowhich 요청 하는 사용자 액세스 toothis 응용 프로그램을 추가 하도록 hello 선택기 다음 toohello 레이블을 클릭 하는 다음으로, **toowhich 그룹은 할당 된 사용자를 추가할 수?** 그룹을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="07ecf-125">Next, tooselect hello group toowhich users who request access toothis application should be added, click hello selector next toohello label **toowhich group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="07ecf-126">**선택 사항:** 원할 경우 toorequire 비즈니스 승인 사용자의 액세스가 허용 되기 전에 설정 hello **toothis 응용 프로그램 액세스 권한을 부여 하기 전에 승인 필요?** 너무 설정/해제**예**합니다.</span><span class="sxs-lookup"><span data-stu-id="07ecf-126">**Optional:** If you wish toorequire a business approval before users are allowed access, set hello **Require approval before granting access toothis application?** toggle too**Yes**.</span></span>

11. <span data-ttu-id="07ecf-127">**선택 사항:에 대 한 응용 프로그램에서 사용 하 여 암호 단일 로그인만** toothis 응용 프로그램 승인 된 사용자가을 전송 하는 이러한 비즈니스 승인자 toospecify hello 암호 tooallow 하려는 경우 설정 hello **승인자 tooset 허용 이 응용 프로그램에 대 한 사용자의 암호?**  너무 설정/해제**예**합니다.</span><span class="sxs-lookup"><span data-stu-id="07ecf-127">**Optional: For applications using password single-sign on only,** if you wish tooallow those business approvers toospecify hello passwords that are sent toothis application for approved users, set hello **Allow approvers tooset user’s passwords for this application?** toggle too**Yes**.</span></span>

12. <span data-ttu-id="07ecf-128">**선택 사항:** tooapprove access toothis 응용 프로그램 수 있는 toospecify hello 비즈니스 승인자 hello 선택기 다음 toohello 레이블을 클릭 **tooapprove 액세스 toothis 응용 프로그램이 허용 되는 사용자?** tooselect를 too10 개별 비즈니스 승인자 합니다.</span><span class="sxs-lookup"><span data-stu-id="07ecf-128">**Optional:** toospecify hello business approvers who are allowed tooapprove access toothis application, click hello selector next toohello label **Who is allowed tooapprove access toothis application?** tooselect up too10 individual business approvers.</span></span>

 >[!NOTE]
 > <span data-ttu-id="07ecf-129">그룹은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="07ecf-129">Groups are not supported.</span></span>
 >
 >

13. <span data-ttu-id="07ecf-130">**선택 사항:** **역할을 표시 하는 응용 프로그램에 대 한**tooassign 승인 된 사용자가 셀프 서비스 tooa 역할 하려는 경우, hello 선택기 다음 toohello 클릭 **toowhich 역할이이 사용자가 할당 해야 응용 프로그램?**  tooselect hello 역할 toowhich 이러한 사용자만 할당 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07ecf-130">**Optional:** **For applications which expose roles**, if you wish tooassign self-service approved users tooa role, click hello selector next toohello **toowhich role should users be assigned in this application?** tooselect hello role toowhich these users should be assigned.</span></span>

14. <span data-ttu-id="07ecf-131">Hello 클릭 **저장** hello 블레이드 toofinish hello 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="07ecf-131">Click hello **Save** button at hello top of hello blade toofinish.</span></span>

<span data-ttu-id="07ecf-132">셀프 서비스 응용 프로그램 구성을 완료 한 후 탐색할 수 tootheir [응용 프로그램 액세스 패널로](https://myapps.microsoft.com/) hello를 클릭 하 고 **+ 추가** 단추 toofind hello 앱 toowhich 사용 하도록 설정한 셀프 서비스 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="07ecf-132">Once you complete Self-service application configuration, users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled Self-service access.</span></span> <span data-ttu-id="07ecf-133">비즈니스 승인자는 [응용 프로그램 액세스 패널](https://myapps.microsoft.com/)에서 알림을 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07ecf-133">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="07ecf-134">사용자가 승인을 해야 하는 액세스 tooan 응용 프로그램을 요청 하는 경우 사용자에 게 알리는 전자 메일을 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07ecf-134">You can enable an email notifying them when a user has requested access tooan application that requires their approval.</span></span> 

<span data-ttu-id="07ecf-135">이러한 승인은 단일 승인 워크플로만, 여러 승인자를 지정 하면 모든 단일 승인자 수 액세스 toohello 응용 프로그램이 승인 의미를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="07ecf-135">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approve access toohello application.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a><span data-ttu-id="07ecf-136">이러한 문제 해결 단계 hello 문제가 해결 되지 않는 경우</span><span class="sxs-lookup"><span data-stu-id="07ecf-136">If these troubleshooting steps do not resolve hello issue</span></span> 

<span data-ttu-id="07ecf-137">사용 가능한 경우 다음 정보는 hello로 지원 티켓을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="07ecf-137">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="07ecf-138">상관 관계 오류 ID</span><span class="sxs-lookup"><span data-stu-id="07ecf-138">Correlation error ID</span></span>

-   <span data-ttu-id="07ecf-139">UPN(사용자 전자 메일 주소)</span><span class="sxs-lookup"><span data-stu-id="07ecf-139">UPN (user email address)</span></span>

-   <span data-ttu-id="07ecf-140">TenantID</span><span class="sxs-lookup"><span data-stu-id="07ecf-140">TenantID</span></span>

-   <span data-ttu-id="07ecf-141">브라우저 종류</span><span class="sxs-lookup"><span data-stu-id="07ecf-141">Browser type</span></span>

-   <span data-ttu-id="07ecf-142">오류가 발생하는 동안 표준 시간대 및 시간/기간</span><span class="sxs-lookup"><span data-stu-id="07ecf-142">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="07ecf-143">Fiddler 추적</span><span class="sxs-lookup"><span data-stu-id="07ecf-143">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="07ecf-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="07ecf-144">Next steps</span></span>
[<span data-ttu-id="07ecf-145">셀프 서비스 그룹 관리를 위한 Azure Active Directory 설정</span><span class="sxs-lookup"><span data-stu-id="07ecf-145">Setting up Azure Active Directory for self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
