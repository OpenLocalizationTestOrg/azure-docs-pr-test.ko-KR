---
title: "Azure AD Privileged Identity Management에서 aaaHow toouse hello 감사 로그 | Microsoft Docs"
description: "Toouse hello 감사 hello Azure Privileged Identity Management 확장에 로그인 하는 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 5d13a6dd-1fcb-4e76-82fb-cb2f4f0e4357
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 36987eaab9fe02c5dd7b4f4705e487299430745d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-audit-log-in-pim"></a><span data-ttu-id="bd96b-103">PIM의 hello 감사 로그를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="bd96b-103">Using hello audit log in PIM</span></span>
<span data-ttu-id="bd96b-104">지정 된 기간 내에서 모든 hello 사용자 할당 및 활성화 hello Privileged Identity Management (PIM) 감사 로그 toosee를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd96b-104">You can use hello Privileged Identity Management (PIM) audit log toosee all hello user assignments and activations within a given time period.</span></span> <span data-ttu-id="bd96b-105">테 넌 트 관리자, 최종 사용자 및 동기화 작업을 포함 하 여 활동의 toosee hello 완전 한 감사 내역을 원하는 경우에 hello을 사용할 수 있습니다 [Azure Active Directory 액세스 및 사용 보고서.](active-directory-view-access-usage-reports.md)</span><span class="sxs-lookup"><span data-stu-id="bd96b-105">If you want toosee hello full audit history of activity in your tenant, including administrator, end user, and synchronization activity, you can use hello [Azure Active Directory access and usage reports.](active-directory-view-access-usage-reports.md)</span></span>

## <a name="navigate-toohello-audit-log"></a><span data-ttu-id="bd96b-106">Toohello 감사 로그를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd96b-106">Navigate toohello audit log</span></span>
<span data-ttu-id="bd96b-107">Hello에서 [Azure 포털](https://portal.azure.com) 대시보드, 선택 hello **Azure AD Privileged Identity Management** 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="bd96b-107">From hello [Azure portal](https://portal.azure.com) dashboard, select hello **Azure AD Privileged Identity Management** app.</span></span> <span data-ttu-id="bd96b-108">여기에서 클릭 하 여 hello 감사 로그에 액세스 **권한 있는 역할을 관리할** > **감사 기록** hello PIM 대시보드에.</span><span class="sxs-lookup"><span data-stu-id="bd96b-108">From there, access hello audit log by clicking **Manage privileged roles** > **Audit history** in hello PIM dashboard.</span></span>

## <a name="hello-audit-log-graph"></a><span data-ttu-id="bd96b-109">hello 감사 로그 그래프</span><span class="sxs-lookup"><span data-stu-id="bd96b-109">hello audit log graph</span></span>
<span data-ttu-id="bd96b-110">선 그래프의 hello 감사 로그 tooview hello 총 활성화 수, 하루에 최대 활성화 및 하루 평균 정품 인증을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd96b-110">You can use hello audit log tooview hello total activations, max activations per day, and average activations per day in a line graph.</span></span>  <span data-ttu-id="bd96b-111">또한 hello 감사 기록에 역할이 둘 이상 있는 경우 역할별 hello 데이터 필터링 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd96b-111">You can also filter hello data by role if there is more than one role in hello audit history.</span></span>

<span data-ttu-id="bd96b-112">사용 하 여 hello **시간**, **동작**, 및 **역할** 단추 toosort hello 로그 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd96b-112">Use hello **time**, **action**, and **role** buttons toosort hello log.</span></span>

## <a name="hello-audit-log-list"></a><span data-ttu-id="bd96b-113">hello 감사 로그 목록</span><span class="sxs-lookup"><span data-stu-id="bd96b-113">hello audit log list</span></span>
<span data-ttu-id="bd96b-114">hello hello 감사 로그 목록에 열이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd96b-114">hello columns in hello audit log list are:</span></span>

* <span data-ttu-id="bd96b-115">**요청자에 게** -hello 요청한 사용자에 게 역할 활성화 hello 또는 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd96b-115">**Requestor** - hello user who requested hello role activation or change.</span></span>  <span data-ttu-id="bd96b-116">"Azure 시스템" hello 값을 사용 하는 경우 자세한 내용은 hello Azure 감사 로그를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd96b-116">If hello value is "Azure System", check hello Azure audit log for more information.</span></span>
* <span data-ttu-id="bd96b-117">**사용자** -hello 사용자를 활성화 하거나 tooa 역할을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd96b-117">**User** - hello user who is activating or assigned tooa role.</span></span>
* <span data-ttu-id="bd96b-118">**역할** -hello 역할 할당 또는 hello 사용자가 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd96b-118">**Role** - hello role assigned or activated by hello user.</span></span>
* <span data-ttu-id="bd96b-119">**동작** -hello 요청자에 의해 수행 된 hello 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd96b-119">**Action** - hello actions taken by hello requestor.</span></span> <span data-ttu-id="bd96b-120">여기에는 할당, 할당 해제, 활성화 또는 비활성화가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd96b-120">This can include assignment, unassignment, activation, or deactivation.</span></span>
* <span data-ttu-id="bd96b-121">**시간** -hello 동작이 발생 한 경우.</span><span class="sxs-lookup"><span data-stu-id="bd96b-121">**Time** - when hello action occurred.</span></span>
* <span data-ttu-id="bd96b-122">**추론** -텍스트 활성화 하는 동안 hello 이유 필드에 입력 된 경우에 여기 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd96b-122">**Reasoning** - if any text was entered into hello reason field during activation, it will show up here.</span></span>
* <span data-ttu-id="bd96b-123">**만료** - 역할의 활성화에만 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd96b-123">**Expiration** - only relevant for activation of roles.</span></span>

## <a name="filter-hello-audit-log"></a><span data-ttu-id="bd96b-124">Hello 감사 로그를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd96b-124">Filter hello audit log</span></span>
<span data-ttu-id="bd96b-125">Hello를 클릭 하 여 hello 감사 로그에 표시 되는 hello 정보를 필터링 할 수 있습니다 **필터** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="bd96b-125">You can filter hello information that shows up in hello audit log by clicking hello **Filter** button.</span></span>  <span data-ttu-id="bd96b-126">hello **업데이트 차트 매개 변수 블레이드** 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd96b-126">hello **Update chart parameters blade** will appear.</span></span>

<span data-ttu-id="bd96b-127">Hello 필터를 설정한 후 클릭 **업데이트** hello 로그에서 toofilter hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="bd96b-127">After you set hello filters, click **Update** toofilter hello data in hello log.</span></span>  <span data-ttu-id="bd96b-128">Hello 데이터가 바로 표시 되지 않으면, hello 페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="bd96b-128">If hello data doesn't appear right away, refresh hello page.</span></span>

### <a name="change-hello-date-range"></a><span data-ttu-id="bd96b-129">Hello 날짜 범위를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd96b-129">Change hello date range</span></span>
<span data-ttu-id="bd96b-130">사용 하 여 hello **오늘**, **지난 주**, **지난 달**, 또는 **사용자 지정** hello 감사 로그의 toochange hello 시간 범위는 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="bd96b-130">Use hello **Today**, **Past Week**, **Past Month**, or **Custom** buttons toochange hello time range of hello audit log.</span></span>

<span data-ttu-id="bd96b-131">Hello를 선택 하는 경우 **사용자 지정** 단추를 제공 됩니다는 **에서** 날짜 필드와 **를** 날짜 필드 toospecify hello 로그에 대 한 날짜 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="bd96b-131">When you choose hello **Custom** button, you will be given a **From** date field and a **To** date field toospecify a range of dates for hello log.</span></span>  <span data-ttu-id="bd96b-132">MM/DD/YYYY 형식으로 hello 날짜를 입력 하거나 hello 클릭 **달력** 아이콘 hello 날짜는 달력에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd96b-132">You can either enter hello dates in MM/DD/YYYY format or click on hello **calendar** icon and choose hello date from a calendar.</span></span>

### <a name="change-hello-roles-included-in-hello-log"></a><span data-ttu-id="bd96b-133">Hello 로그에 포함 된 hello 역할 변경</span><span class="sxs-lookup"><span data-stu-id="bd96b-133">Change hello roles included in hello log</span></span>
<span data-ttu-id="bd96b-134">선택 하거나 선택 취소할 hello **역할** 로그 hello에서 다음 tooeach 역할 tooinclude 확인란을 선택 하거나 제외 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd96b-134">Check or uncheck hello **Role** checkbox next tooeach role tooinclude or exclude it from hello log.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="bd96b-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bd96b-135">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

