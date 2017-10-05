---
title: "Log Analytics에서 Azure Automation 계정 연결 해제 | Microsoft Docs"
description: "이 문서에서는 OMS 작업 영역에서 Azure Automation 계정 연결을 해제하는 방법을 대략적으로 설명합니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: how-to-article
ms.date: 02/07/2017
ms.author: magoedte
ms.openlocfilehash: 56b09c2cfc14813b5efcb364c580787fec1bf639
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-unlink-your-automation-account-from-a-log-analytics-workspace"></a><span data-ttu-id="ea49e-103">Log Analytics에서 Automation 계정 연결을 해제하는 방법</span><span class="sxs-lookup"><span data-stu-id="ea49e-103">How to unlink your Automation account from a Log Analytics workspace</span></span>

<span data-ttu-id="ea49e-104">Azure Automation은 Log Analytics와 통합되어 모든 Automation 계정의 runbook 작업에 대한 사전 모니터링을 지원할 뿐만 아니라, Log Analytics에 의존하는 다음 솔루션을 가져올 때도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ea49e-104">Azure Automation integrates with Log Analytics to not only support proactive monitoring of your runbook jobs across all of your Automation accounts, but is also required when you import the following solutions that are dependent on Log Analytics:</span></span>

* [<span data-ttu-id="ea49e-105">업데이트 관리</span><span class="sxs-lookup"><span data-stu-id="ea49e-105">Update Management</span></span>](../operations-management-suite/oms-solution-update-management.md)
* [<span data-ttu-id="ea49e-106">변경 내용 추적</span><span class="sxs-lookup"><span data-stu-id="ea49e-106">Change Tracking</span></span>](../log-analytics/log-analytics-change-tracking.md)
* [<span data-ttu-id="ea49e-107">작업이 없는 동안 VM 시작/중지</span><span class="sxs-lookup"><span data-stu-id="ea49e-107">Start/Stop VMs during off-hours</span></span>](automation-solution-vm-management.md)
 
<span data-ttu-id="ea49e-108">Automation 계정을 Log Analytics에 더 이상 통합하지 않기로 결정할 경우 Azure Portal에서 직접 계정 연결을 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea49e-108">If you decide you no longer wish to integrate your Automation account with Log Analytics, you can unlink your account directly from the Azure portal.</span></span>  <span data-ttu-id="ea49e-109">계속하기 전에 앞에서 언급한 솔루션을 제거해야 합니다. 그러지 않으면이 프로세스가 계속 진행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ea49e-109">Before you proceed, you will first need to remove the solutions mentioned earlier, otherwise this process will be prevented from proceeding.</span></span>  <span data-ttu-id="ea49e-110">가져온 특정 솔루션에 대한 항목을 검토하여 제거에 필요한 단계를 이해하세요.</span><span class="sxs-lookup"><span data-stu-id="ea49e-110">Review the topic for the particular solution you have imported to understand the steps required to remove it.</span></span>  

<span data-ttu-id="ea49e-111">이러한 솔루션을 제거한 후에 다음 단계에 따라 Automation 계정 연결을 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea49e-111">After you remove these solutions you can perform the following steps to unlink your Automation account.</span></span>

## <a name="unlink-workspace"></a><span data-ttu-id="ea49e-112">작업 영역 연결 해제</span><span class="sxs-lookup"><span data-stu-id="ea49e-112">Unlink workspace</span></span>

1. <span data-ttu-id="ea49e-113">Azure Portal에서 Automation 계정을 열고 Automation 계정 블레이드의 계정 블레이드에서 **작업 영역 연결 해제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ea49e-113">From the Azure portal, open your Automation account, and in the Automation account blade, in the account blade, select **Unlink workspace**.</span></span><br><br> <span data-ttu-id="ea49e-114">![작업 영역 연결 해제 옵션](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span><span class="sxs-lookup"><span data-stu-id="ea49e-114">![Unlink workspace option](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span></span><br><br>  
2. <span data-ttu-id="ea49e-115">작업 영역 연결 해제 블레이드에서 **작업 영역 연결 해제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ea49e-115">On the Unlink workspace blade, click **Unlink worksapce**.</span></span><br><br> <span data-ttu-id="ea49e-116">![작업 영역 연결 해제 블레이드](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).</span><span class="sxs-lookup"><span data-stu-id="ea49e-116">![Unlink workspace blade](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).</span></span><br><br>  <span data-ttu-id="ea49e-117">계속할지 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="ea49e-117">You will receive a prompt verifying you wish to proceed.</span></span><br><br>
3. <span data-ttu-id="ea49e-118">Azure Automation이 Log Analytics에서 계정 연결을 끊으려고 하는 동안 메뉴의 **알림**에서 진행 상태를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea49e-118">While Azure Automation attempts to unlink the account your Log Analytics workspace, you can track the progress under **Notifications** from the menu.</span></span>

<span data-ttu-id="ea49e-119">업데이트 관리 솔루션을 사용한 경우 솔루션을 제거한 후 더 이상 필요하지 않은 다음 항목을 제거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea49e-119">If you used the Update Management solution, optionally you may want to remove the following items that are no longer needed after you remove the solution.</span></span>

* <span data-ttu-id="ea49e-120">업데이트 일정.</span><span class="sxs-lookup"><span data-stu-id="ea49e-120">Update schedules.</span></span>  <span data-ttu-id="ea49e-121">각 일정에는 사용자가 만든 업데이트 배포와 일치하는 이름이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea49e-121">Each will have names that match the update deployments you created)</span></span>

* <span data-ttu-id="ea49e-122">솔루션에 대해 생성된 Hybrid Worker 그룹.</span><span class="sxs-lookup"><span data-stu-id="ea49e-122">Hybrid worker groups created for the solution.</span></span>  <span data-ttu-id="ea49e-123">각 그룹에는 machine1.contoso.com_9ceb8108-26 c 9-4051-b6b3-227600d715c8과 비슷하게 이름이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea49e-123">Each will be named similarly to  machine1.contoso.com_9ceb8108-26c9-4051-b6b3-227600d715c8).</span></span>

<span data-ttu-id="ea49e-124">작업이 없는 동안 VM 시작/중지를 사용한 경우 솔루션을 제거한 후 더 이상 필요하지 않은 다음 항목을 제거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea49e-124">If you used the Start/Stop VMs during off-hours solution, optionally you may want to remove the following items that are no longer needed after you remove the solution.</span></span>

* <span data-ttu-id="ea49e-125">VM runbook 시작 및 중지 일정</span><span class="sxs-lookup"><span data-stu-id="ea49e-125">Start and stop VM runbook schedules</span></span> 
* <span data-ttu-id="ea49e-126">VM runbook 시작 및 중지</span><span class="sxs-lookup"><span data-stu-id="ea49e-126">Start and stop VM runbooks</span></span>
* <span data-ttu-id="ea49e-127">변수</span><span class="sxs-lookup"><span data-stu-id="ea49e-127">Variables</span></span>   

## <a name="next-steps"></a><span data-ttu-id="ea49e-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ea49e-128">Next steps</span></span>

<span data-ttu-id="ea49e-129">OMS Log Analytics와 통합되도록 Automation 계정을 다시 구성하려면 [Automation에서 Log Analytics로 작업 상태 및 작업 스트림 전달(OMS)](automation-manage-send-joblogs-log-analytics.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ea49e-129">To reconfigure your Automation account to integrate with OMS Log Analytics, see [Forward job status and job streams from Automation to Log Analytics (OMS)](automation-manage-send-joblogs-log-analytics.md).</span></span> 