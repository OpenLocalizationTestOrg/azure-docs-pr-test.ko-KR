---
title: "Azure Privileged Identity Management 승인 워크플로 | Microsoft Docs"
description: "PIM(Privileged Identity Management)의 승인 워크플로에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: barclayn
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2017
ms.author: barclayn
ms.custom: pim
ms.openlocfilehash: cf6a9213fa0a1cba8725aabb42abe51b805ece7a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="approvals-preview"></a><span data-ttu-id="d6eb7-103">승인(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="d6eb7-103">Approvals (Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="d6eb7-104">개요</span><span class="sxs-lookup"><span data-stu-id="d6eb7-104">Overview</span></span>

<span data-ttu-id="d6eb7-105">PIM(Privileged Identity Management)에 대한 승인을 사용하면, 활성화에 대한 승인이 필요한 역할을 구성하고 하나 이상의 사용자 또는 그룹을 위임된 승인자로 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-105">With Approvals for Privileged Identity Management, you can configure roles to require approval for activation, and choose one or multiple users or groups as delegated approvers.</span></span> <span data-ttu-id="d6eb7-106">역할을 구성하고 승인자를 선택하는 방법을 알아보려면 계속 진행하세요.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-106">Keep reading to learn how to configure roles and select approvers.</span></span>

>[!NOTE]
<span data-ttu-id="d6eb7-107">이 기능은 아직 개발 중이므로 버그가 발생할 수 있음에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-107">Please keep in mind this feature is still in development, and you may encounter bugs.</span></span> <span data-ttu-id="d6eb7-108">텍스트 및 명명 규칙을 포함한 기능이 변경될 수 있으므로 최종본으로 간주해서는 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-108">The functionality, including text and naming conventions are subject to change, and should not be considered final.</span></span>


## <a name="key-terminology"></a><span data-ttu-id="d6eb7-109">주요 용어</span><span class="sxs-lookup"><span data-stu-id="d6eb7-109">Key Terminology</span></span>

<span data-ttu-id="d6eb7-110">*적격 역할 사용자* – 적법한 Azure AD 역할(역할에 대한 활성화 필요)로 할당된 조직 내 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-110">*Eligible Role User* – An eligible role user is a user within your organization that’s been assigned to an Azure AD role as eligible (role requires activation).</span></span>

<span data-ttu-id="d6eb7-111">*위임된 승인자* – 역할 활성화 요청에 대한 승인을 담당하는 Azure AD 내 하나 이상의 개인 또는 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-111">*Delegated Approver* – A delegated approver is one or multiple individuals or groups within your Azure AD who are responsible for approving requests for role activation.</span></span>

## <a name="scenarios"></a><span data-ttu-id="d6eb7-112">시나리오</span><span class="sxs-lookup"><span data-stu-id="d6eb7-112">Scenarios</span></span>

<span data-ttu-id="d6eb7-113">비공개 미리 보기에서 지원하는 시나리오는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-113">The private preview supports the following scenarios:</span></span>

<span data-ttu-id="d6eb7-114">**PRA(권한 있는 역할 관리자)는 다음을 수행할 수 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="d6eb7-114">**As a Privileged Role Administrator (PRA) you can:**</span></span>

-   [<span data-ttu-id="d6eb7-115">특정 역할에 대한 승인을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="d6eb7-115">enable approval for specific roles</span></span>](#enable-approval-for-specific-roles)

-   [<span data-ttu-id="d6eb7-116">요청을 승인할 승인자 사용자 및/또는 그룹 지정</span><span class="sxs-lookup"><span data-stu-id="d6eb7-116">specify approver users and/or groups to approve requests</span></span>](#specify-approver-users-and/or-groups-to-approve-requests)

-   [<span data-ttu-id="d6eb7-117">모든 권한 있는 역할에 대한 요청 및 승인 기록 보기</span><span class="sxs-lookup"><span data-stu-id="d6eb7-117">view request and approval history for all privileged roles</span></span>](#view-request-and-approval-history-for-all-privileged-roles)

<span data-ttu-id="d6eb7-118">**지정된 승인자는 다음을 수행할 수 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="d6eb7-118">**As a designated approver, you can:**</span></span>

-   [<span data-ttu-id="d6eb7-119">보류 중인 승인(요청) 보기</span><span class="sxs-lookup"><span data-stu-id="d6eb7-119">view pending approvals (requests)</span></span>](#view-pending-approvals-requests)

-   [<span data-ttu-id="d6eb7-120">역할 상승 요청(단일 및/또는 대량) 승인 또는 거부</span><span class="sxs-lookup"><span data-stu-id="d6eb7-120">approve or reject requests for role elevation (single and/or bulk)</span></span>](#approve-or-reject-requests-for-role-elevation-single-and/or-bulk)

-   [<span data-ttu-id="d6eb7-121">승인/거부에 대한 근거 제공</span><span class="sxs-lookup"><span data-stu-id="d6eb7-121">provide justification for my approval/rejection</span></span>](#provide-justification-for-my-approval/rejection) 

<span data-ttu-id="d6eb7-122">**적격 역할 사용자는 다음을 수행할 수 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="d6eb7-122">**As an Eligible Role User you can:**</span></span>

-   [<span data-ttu-id="d6eb7-123">승인이 필요한 역할의 활성화 요청</span><span class="sxs-lookup"><span data-stu-id="d6eb7-123">request activation of a role that requires approval</span></span>](#request-activation-of-a-role-that-requires-approval)

-   [<span data-ttu-id="d6eb7-124">활성화 요청 상태 보기</span><span class="sxs-lookup"><span data-stu-id="d6eb7-124">view the status of your request to activate</span></span>](#view-the-status-of-your-request-to-activate)

-   [<span data-ttu-id="d6eb7-125">활성화가 승인되면 Azure AD에서 작업 수행</span><span class="sxs-lookup"><span data-stu-id="d6eb7-125">complete your task in Azure AD if activation was approved</span></span>](#complete-your-task-in-azure-ad-if-activation-was-approved)

### <a name="navigation"></a><span data-ttu-id="d6eb7-126">탐색</span><span class="sxs-lookup"><span data-stu-id="d6eb7-126">Navigation</span></span>

<span data-ttu-id="d6eb7-127">승인을 지원하도록 탐색을 업데이트했습니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-127">We've updated the navigation to support approvals</span></span>

![](media/azure-ad-pim-approval-workflow/image001.png)

<span data-ttu-id="d6eb7-128">PIM 및 새로운 승인 설명서에 대한 정보는 기본 방문 페이지에서 편리하게 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-128">The default landing page provides convenient access to information about PIM and the new approvals documentation.</span></span>

![](media/azure-ad-pim-approval-workflow/image002.png)

<span data-ttu-id="d6eb7-129">또한 PIM의 모든 사용자를 위해 새로운 섹션, 즉 '내 감사 기록'을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-129">We’ve also added a new section for all users of PIM, ‘My Audit History’.</span></span> <span data-ttu-id="d6eb7-130">여기서는 ID와 관련된 모든 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-130">Here you can find all the information relevant to your identity.</span></span> <span data-ttu-id="d6eb7-131">여기에는 모든 보류 중 및 완료된 요청, 해결 요청에 대한 모든 결정 및 과거의 모든 역할 활성화가 편리하게 한 곳에 모여 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-131">This includes all your pending and completed requests, any decisions you’ve made about the requests you resolve, and all your past role activations in one convenient location.</span></span>

![](media/azure-ad-pim-approval-workflow/image003.png)

### <a name="enable-approval-for-specific-roles"></a><span data-ttu-id="d6eb7-132">특정 역할에 대한 승인을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="d6eb7-132">Enable approval for specific roles</span></span>

<span data-ttu-id="d6eb7-133">특정 역할에 대한 승인을 사용하려면 먼저 왼쪽 탐색 영역에서 [디렉터리 역할]을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-133">To enable approval for a specific role, first select Directory Roles from the left navigation.</span></span>

![](media/azure-ad-pim-approval-workflow/image004.png)

<span data-ttu-id="d6eb7-134">[디렉터리 역할] 왼쪽 탐색 영역에서 설정을 찾아서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-134">Find and select settings in the Directory Roles left navigation</span></span>

![](media/azure-ad-pim-approval-workflow/image006.png)

<span data-ttu-id="d6eb7-135">[권한 있는 역할]을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-135">Select privileged Roles:</span></span>

![](media/azure-ad-pim-approval-workflow/image009.png)

<span data-ttu-id="d6eb7-136">[승인 필요] 섹션에서 "사용"을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-136">Select “Enable” in the Require approval section:</span></span>

![](media/azure-ad-pim-approval-workflow/image011.png)

<span data-ttu-id="d6eb7-137">활성화되면 블레이드가 확장되어 다음 세부 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-137">Once enabled, the blade will expand to show the following details:</span></span>

![](media/azure-ad-pim-approval-workflow/image013.png)

>[!NOTE]
<span data-ttu-id="d6eb7-138">승인자를 지정하지 않으면 PRA가 기본 승인자가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-138">If you DO NOT specify any approvers, the PRA(s) become the default approver(s).</span></span> <span data-ttu-id="d6eb7-139">PRA는 이 역할에 대한 모든 활성화 요청을 승인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-139">PRA(s) would be required to approve ALL activation requests for this role.</span></span>

### <a name="specify-approver-users-andor-groups-to-approve-requests"></a><span data-ttu-id="d6eb7-140">요청을 승인할 승인자 사용자 및/또는 그룹 지정</span><span class="sxs-lookup"><span data-stu-id="d6eb7-140">Specify approver users and/or groups to approve requests</span></span>

<span data-ttu-id="d6eb7-141">승인을 위임하려면 "승인자 선택" 옵션을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-141">To delegate approval, click the option to “Select approvers”:</span></span>

![](media/azure-ad-pim-approval-workflow/image015.png)

<span data-ttu-id="d6eb7-142">[승인자 선택] 블레이드가 로드되면 위쪽의 검색 표시줄을 사용하거나 미리 채워진 목록에서 선택하여 특정 사용자 또는 그룹을 검색한 다음 완료되면 "선택"을 클릭하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-142">When the Select approvers blade loads, you may search for a specific user or group using the search bar at the top, or selecting from the pre-populated list, then click “Select” when finished:</span></span>

![](media/azure-ad-pim-approval-workflow/image017.png)

<span data-ttu-id="d6eb7-143">참고: 한 번에 여러 사용자 또는 그룹을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-143">Note: You may select multiple users or groups at a time.</span></span>

<span data-ttu-id="d6eb7-144">선택한 항목이 아래와 같이 선택한 승인자 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-144">Your selection will appear in the list of selected approvers as seen below:</span></span>

![](media/azure-ad-pim-approval-workflow/image019.png)

<span data-ttu-id="d6eb7-145">승인자를 제거하려면 해당 이름 옆에 있는 [제거] 단추를 클릭하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-145">To remove an approver, simply click the Remove button next to their name.</span></span>

<span data-ttu-id="d6eb7-146">추가 승인자를 추가하려면 프로세스를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-146">To add additional approvers, repeat the process.</span></span>

## <a name="view-request-and-approval-history-for-all-privileged-roles"></a><span data-ttu-id="d6eb7-147">모든 권한 있는 역할에 대한 요청 및 승인 기록 보기</span><span class="sxs-lookup"><span data-stu-id="d6eb7-147">View request and approval history for all privileged roles</span></span>

<span data-ttu-id="d6eb7-148">모든 권한 있는 역할에 대한 요청 및 승인 기록을 보려면 대시보드에서 [감사 기록]을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-148">To view request and approval history for all privileged roles, select Audit History from the dashboard:</span></span>

![](media/azure-ad-pim-approval-workflow/image021.png)

>[!NOTE]
<span data-ttu-id="d6eb7-149">[작업]별로 데이터를 정렬하고 "활성화 승인됨"을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-149">You can sort the data by Action, and look for “Activation Approved”</span></span>

### <a name="view-pending-approvals-requests"></a><span data-ttu-id="d6eb7-150">보류 중인 승인(요청) 보기</span><span class="sxs-lookup"><span data-stu-id="d6eb7-150">View pending approvals (requests)</span></span>

<span data-ttu-id="d6eb7-151">요청 승인이 보류 중일 때는 위임된 승인자가 전자 메일 알림을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-151">As a delegated approver, you’ll receive email notifications when a request is pending your approval.</span></span> <span data-ttu-id="d6eb7-152">PIM 포털에서 이러한 요청을 보려면 새로운 탐색 창의 대시보드에서 왼쪽 탐색 모음의 "보류 중 승인 요청" 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-152">To view these requests in the PIM portal, from the dashboard (in the new navigation) select the “Pending Approval Requests” tab in the left navigation bar.</span></span>

![](media/azure-ad-pim-approval-workflow/image023.png)

<span data-ttu-id="d6eb7-153">여기에서 승인 보류 중인 요청 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-153">From there, you’ll see a list of requests pending approval:</span></span>

![](media/azure-ad-pim-approval-workflow/image024.png)

### <a name="approve-or-reject-requests-for-role-elevation-single-andor-bulk"></a><span data-ttu-id="d6eb7-154">역할 상승 요청(단일 및/또는 대량) 승인 또는 거부</span><span class="sxs-lookup"><span data-stu-id="d6eb7-154">Approve or reject requests for role elevation (single and/or bulk)</span></span>

<span data-ttu-id="d6eb7-155">승인하거나 거부하려는 요청을 선택하고 결정에 해당하는 작업 모음의 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-155">Select the requests you wish to approve or deny, and click the button in the action bar that corresponds with your decision:</span></span>

![](media/azure-ad-pim-approval-workflow/image025.png)

### <a name="provide-justification-for-my-approvalrejection"></a><span data-ttu-id="d6eb7-156">승인/거부에 대한 근거 제공</span><span class="sxs-lookup"><span data-stu-id="d6eb7-156">Provide justification for my approval/rejection</span></span>

<span data-ttu-id="d6eb7-157">이 경우 한 번에 여러 요청을 승인하거나 거부할 수 있는 새 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-157">This will open a new blade to approve or deny multiple requests at once.</span></span> <span data-ttu-id="d6eb7-158">결정에 대한 근거를 입력하고, 아래쪽 또는 블레이드에서 승인(또는 거부)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-158">Enter a justification for your decision, and click approve (or deny) at the bottom or the blade:</span></span>

![](media/azure-ad-pim-approval-workflow/image029.png)

<span data-ttu-id="d6eb7-159">요청 프로세스가 완료되면 상태 기호에 사용자가 내린 결정이 반영됩니다(이 예에서는 승인 결정임).</span><span class="sxs-lookup"><span data-stu-id="d6eb7-159">When the request process is complete, the status symbol will reflect the decision you made (in this example, the decision is approve):</span></span>

![](media/azure-ad-pim-approval-workflow/image031.png)

### <a name="request-activation-of-a-role-that-requires-approval"></a><span data-ttu-id="d6eb7-160">승인이 필요한 역할의 활성화 요청</span><span class="sxs-lookup"><span data-stu-id="d6eb7-160">Request activation of a role that requires approval</span></span>

<span data-ttu-id="d6eb7-161">승인이 필요한 역할을 활성화하도록 요청하면 역할 활성화 프로세스가 동일하게 유지되기 때문에 이전 PIM 탐색 또는 새 탐색에서 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-161">Requesting activation of a role that requires approval may be initiated from either the old PIM navigation, or the new navigation, as the process for role activation remains the same.</span></span> <span data-ttu-id="d6eb7-162">활성화할 역할 목록에서 역할을 선택하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-162">Simply select a role from the list of roles to activate:</span></span>

![](media/azure-ad-pim-approval-workflow/image033.png)

<span data-ttu-id="d6eb7-163">권한 있는 역할에 Multi-Factor Authentication이 필요한 경우 먼저 해당 작업을 완료하도록 요구하는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-163">If a privileged role requires Multi-Factor Authentication, you’ll be prompted to complete that task first:</span></span>

![](media/azure-ad-pim-approval-workflow/image035.png)

<span data-ttu-id="d6eb7-164">해당 작업이 완료되면 [활성화]를 클릭하고 필요에 따라 근거를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-164">Once complete, click Activate and provide a justification (if required):</span></span>

![](media/azure-ad-pim-approval-workflow/image037.png)

<span data-ttu-id="d6eb7-165">승인 보류 중인 요청이라는 알림이 요청자에게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-165">The requestor will see a notification that the request is pending approval:</span></span>

![](media/azure-ad-pim-approval-workflow/image039.png)

### <a name="view-the-status-of-your-request-to-activate"></a><span data-ttu-id="d6eb7-166">활성화 요청 상태 보기</span><span class="sxs-lookup"><span data-stu-id="d6eb7-166">View the status of your request to activate</span></span>

<span data-ttu-id="d6eb7-167">보류 중인 활성화 요청의 상태 보기는 새 탐색에서 액세스해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-167">Viewing the status of a pending request to activate must be accessed from the new navigation.</span></span> <span data-ttu-id="d6eb7-168">왼쪽 탐색 모음에서 '내 요청' 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-168">From the left navigation bar, select the “My Requests” tab:</span></span>

![](media/azure-ad-pim-approval-workflow/image041.png)

<span data-ttu-id="d6eb7-169">요청 상태는 기본적으로 "보류 중"이지만 모든 요청 또는 거부된 요청을 표시하도록 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-169">The request state defaults to “Pending”, but you can toggle to see all or denied requests.</span></span>

### <a name="complete-your-task-in-azure-ad-if-activation-was-approved"></a><span data-ttu-id="d6eb7-170">활성화가 승인되면 Azure AD에서 작업 수행</span><span class="sxs-lookup"><span data-stu-id="d6eb7-170">Complete your task in Azure AD if activation was approved</span></span>

<span data-ttu-id="d6eb7-171">요청이 승인되면 해당 역할이 활성화되고 이 역할을 요구하는 작업을 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-171">Once the request is approved, the role is active and you may proceed with any work that requires this role.</span></span>

![](media/azure-ad-pim-approval-workflow/image043.png)

## <a name="next-steps"></a><span data-ttu-id="d6eb7-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d6eb7-172">Next steps</span></span>

<span data-ttu-id="d6eb7-173">Microsoft는 사용자의 의견을 소중하게 생각합니다.</span><span class="sxs-lookup"><span data-stu-id="d6eb7-173">Your feedback is valuable to us.</span></span> <span data-ttu-id="d6eb7-174">언제든지 자유롭게 사용자의 의견이나 피드백을 Microsoft와 함께 공유해 주세요!</span><span class="sxs-lookup"><span data-stu-id="d6eb7-174">Please feel free to share comments or feedback with us here!</span></span>
