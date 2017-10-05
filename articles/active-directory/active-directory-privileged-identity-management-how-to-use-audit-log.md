---
title: "Azure AD Privileged Identity Management에서 감사 로그를 사용하는 방법 | Microsoft Docs"
description: "Azure 권한 있는 ID 관리 확장에서 감사 로그를 사용하는 방법을 알아봅니다."
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
ms.openlocfilehash: 7d9a5255a64d46c1388d328a606b3f297d61262b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-audit-log-in-pim"></a><span data-ttu-id="99588-103">PIM에서 감사 로그 사용</span><span class="sxs-lookup"><span data-stu-id="99588-103">Using the audit log in PIM</span></span>
<span data-ttu-id="99588-104">Azure Privileged Identity Management(PIM) 감사 로그를 사용하여 지정된 기간 내의 모든 사용자 할당 및 활성화를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99588-104">You can use the Privileged Identity Management (PIM) audit log to see all the user assignments and activations within a given time period.</span></span> <span data-ttu-id="99588-105">테넌트에서 관리자, 최종 사용자 및 동기화 작업을 비롯한 활동의 전체 감사 기록을 보려는 경우 [Azure Active Directory 액세스 및 사용 보고서](active-directory-view-access-usage-reports.md)</span><span class="sxs-lookup"><span data-stu-id="99588-105">If you want to see the full audit history of activity in your tenant, including administrator, end user, and synchronization activity, you can use the [Azure Active Directory access and usage reports.](active-directory-view-access-usage-reports.md)</span></span>

## <a name="navigate-to-the-audit-log"></a><span data-ttu-id="99588-106">감사 로그로 이동</span><span class="sxs-lookup"><span data-stu-id="99588-106">Navigate to the audit log</span></span>
<span data-ttu-id="99588-107">[Azure Portal](https://portal.azure.com) 대시보드에서 **Azure AD Privileged Identity Management** 앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="99588-107">From the [Azure portal](https://portal.azure.com) dashboard, select the **Azure AD Privileged Identity Management** app.</span></span> <span data-ttu-id="99588-108">여기에서 PIM 대시보드에 **권한 있는 역할 관리** > **감사 기록**을 클릭하여 감사 로그에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="99588-108">From there, access the audit log by clicking **Manage privileged roles** > **Audit history** in the PIM dashboard.</span></span>

## <a name="the-audit-log-graph"></a><span data-ttu-id="99588-109">감사 로그 그래프</span><span class="sxs-lookup"><span data-stu-id="99588-109">The audit log graph</span></span>
<span data-ttu-id="99588-110">감사 로그를 사용하여 전체 활성화, 일일 최대 활성화, 일일 평균 활성화를 선 그래프로 보도록 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99588-110">You can use the audit log to view the total activations, max activations per day, and average activations per day in a line graph.</span></span>  <span data-ttu-id="99588-111">감사 기록에 역할이 둘 이상인 경우 역할별로 데이터를 필터링할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99588-111">You can also filter the data by role if there is more than one role in the audit history.</span></span>

<span data-ttu-id="99588-112">**시간**, **작업** 및 **역할** 단추를 사용하여 로그를 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="99588-112">Use the **time**, **action**, and **role** buttons to sort the log.</span></span>

## <a name="the-audit-log-list"></a><span data-ttu-id="99588-113">감사 로그 목록</span><span class="sxs-lookup"><span data-stu-id="99588-113">The audit log list</span></span>
<span data-ttu-id="99588-114">감사 로그 목록의 열은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="99588-114">The columns in the audit log list are:</span></span>

* <span data-ttu-id="99588-115">**요청자** - 역할 활성화 또는 변경을 요청한 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="99588-115">**Requestor** - the user who requested the role activation or change.</span></span>  <span data-ttu-id="99588-116">값이 "Azure 시스템"인 경우 Azure 감사 로그에서 자세한 내용을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="99588-116">If the value is "Azure System", check the Azure audit log for more information.</span></span>
* <span data-ttu-id="99588-117">**사용자** - 활성화되어 있거나 역할에 할당된 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="99588-117">**User** - the user who is activating or assigned to a role.</span></span>
* <span data-ttu-id="99588-118">**역할** - 사용자가 할당하거나 활성화한 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="99588-118">**Role** - the role assigned or activated by the user.</span></span>
* <span data-ttu-id="99588-119">**작업** - 요청자가 수행하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="99588-119">**Action** - the actions taken by the requestor.</span></span> <span data-ttu-id="99588-120">여기에는 할당, 할당 해제, 활성화 또는 비활성화가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99588-120">This can include assignment, unassignment, activation, or deactivation.</span></span>
* <span data-ttu-id="99588-121">**Time** - 작업이 발생한 시간.</span><span class="sxs-lookup"><span data-stu-id="99588-121">**Time** - when the action occurred.</span></span>
* <span data-ttu-id="99588-122">**Reasoning** - 활성화 중에 reason(이유) 필드에 입력한 텍스트가 있는 경우 여기에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="99588-122">**Reasoning** - if any text was entered into the reason field during activation, it will show up here.</span></span>
* <span data-ttu-id="99588-123">**만료** - 역할의 활성화에만 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99588-123">**Expiration** - only relevant for activation of roles.</span></span>

## <a name="filter-the-audit-log"></a><span data-ttu-id="99588-124">감사 로그 필터링</span><span class="sxs-lookup"><span data-stu-id="99588-124">Filter the audit log</span></span>
<span data-ttu-id="99588-125">**필터** 단추를 클릭하여 감사 로그에 표시되는 정보를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99588-125">You can filter the information that shows up in the audit log by clicking the **Filter** button.</span></span>  <span data-ttu-id="99588-126">**Update chart parameters blade** (차트 매개 변수 업데이트 블레이드)가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="99588-126">The **Update chart parameters blade** will appear.</span></span>

<span data-ttu-id="99588-127">필터를 설정한 후 **업데이트** 를 클릭하여 로그의 데이터를 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="99588-127">After you set the filters, click **Update** to filter the data in the log.</span></span>  <span data-ttu-id="99588-128">데이터가 바로 표시되지 않으면 페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="99588-128">If the data doesn't appear right away, refresh the page.</span></span>

### <a name="change-the-date-range"></a><span data-ttu-id="99588-129">날짜 범위 변경</span><span class="sxs-lookup"><span data-stu-id="99588-129">Change the date range</span></span>
<span data-ttu-id="99588-130">**오늘**, **지난 주**, **지난 달**, **사용자 지정** 단추를 사용하여 감사 로그의 시간 범위를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="99588-130">Use the **Today**, **Past Week**, **Past Month**, or **Custom** buttons to change the time range of the audit log.</span></span>

<span data-ttu-id="99588-131">**사용자 지정** 단추를 선택하면 로그에 대해 날짜 범위를 지정하도록 **시작** 날짜 필드와 **끝** 날짜 필드가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="99588-131">When you choose the **Custom** button, you will be given a **From** date field and a **To** date field to specify a range of dates for the log.</span></span>  <span data-ttu-id="99588-132">MM/DD/YYYY 형식으로 날짜를 입력하거나 **달력** 아이콘을 클릭하여 달력에서 날짜를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99588-132">You can either enter the dates in MM/DD/YYYY format or click on the **calendar** icon and choose the date from a calendar.</span></span>

### <a name="change-the-roles-included-in-the-log"></a><span data-ttu-id="99588-133">로그에 포함된 역할 변경</span><span class="sxs-lookup"><span data-stu-id="99588-133">Change the roles included in the log</span></span>
<span data-ttu-id="99588-134">로그에 포함시키거나 제외한 각 역할의 옆에 있는 **역할** 확인란을 선택 또는 선택 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="99588-134">Check or uncheck the **Role** checkbox next to each role to include or exclude it from the log.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="99588-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="99588-135">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

