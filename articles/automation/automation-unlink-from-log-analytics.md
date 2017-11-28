---
title: "Azure 자동화 계정 로그 분석에서 aaaUnlink | Microsoft Docs"
description: "이 문서는 어떻게 toounlink Azure 자동화는 OMS 작업 영역에서을 계정에 대 한 개요를 제공 합니다."
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
ms.openlocfilehash: 3ec0745673f6a872538d33023a7a1d2bb1d18ec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toounlink-your-automation-account-from-a-log-analytics-workspace"></a><span data-ttu-id="90205-103">어떻게 toounlink 자동화는 로그 분석 작업 영역에서을 계정합니다</span><span class="sxs-lookup"><span data-stu-id="90205-103">How toounlink your Automation account from a Log Analytics workspace</span></span>

<span data-ttu-id="90205-104">Azure 자동화 로그 분석 toonot만 지원 사전 모니터링 runbook 작업의 자동화 계정의 모든와 통합 되어 뿐만 아니라 필요한 hello 다음 로그 분석에 의존 하는 솔루션을 가져올 때:</span><span class="sxs-lookup"><span data-stu-id="90205-104">Azure Automation integrates with Log Analytics toonot only support proactive monitoring of your runbook jobs across all of your Automation accounts, but is also required when you import hello following solutions that are dependent on Log Analytics:</span></span>

* [<span data-ttu-id="90205-105">업데이트 관리</span><span class="sxs-lookup"><span data-stu-id="90205-105">Update Management</span></span>](../operations-management-suite/oms-solution-update-management.md)
* [<span data-ttu-id="90205-106">변경 내용 추적</span><span class="sxs-lookup"><span data-stu-id="90205-106">Change Tracking</span></span>](../log-analytics/log-analytics-change-tracking.md)
* [<span data-ttu-id="90205-107">작업이 없는 동안 VM 시작/중지</span><span class="sxs-lookup"><span data-stu-id="90205-107">Start/Stop VMs during off-hours</span></span>](automation-solution-vm-management.md)
 
<span data-ttu-id="90205-108">중단 toointegrate 자동화 계정 로그 분석을 결정 한 경우 hello Azure 포털에서 직접 계정 연결을 끊을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="90205-108">If you decide you no longer wish toointegrate your Automation account with Log Analytics, you can unlink your account directly from hello Azure portal.</span></span>  <span data-ttu-id="90205-109">계속 진행 하기 전에 앞에서 언급 한 tooremove hello 솔루션을 만들어야 합니다, 그리고 그렇지 않으면 진행에서이 프로세스를 시작 하지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="90205-109">Before you proceed, you will first need tooremove hello solutions mentioned earlier, otherwise this process will be prevented from proceeding.</span></span>  <span data-ttu-id="90205-110">필요한 toounderstand hello 단계 가져온 hello 특정 솔루션에 대 한 검토 hello 항목 tooremove 것입니다.</span><span class="sxs-lookup"><span data-stu-id="90205-110">Review hello topic for hello particular solution you have imported toounderstand hello steps required tooremove it.</span></span>  

<span data-ttu-id="90205-111">이러한 솔루션을 제거한 후에 다음 단계 toounlink hello 자동화 계정으로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90205-111">After you remove these solutions you can perform hello following steps toounlink your Automation account.</span></span>

## <a name="unlink-workspace"></a><span data-ttu-id="90205-112">작업 영역 연결 해제</span><span class="sxs-lookup"><span data-stu-id="90205-112">Unlink workspace</span></span>

1. <span data-ttu-id="90205-113">Hello Azure 포털에서에서 자동화 계정을 열고 hello 자동화 계정 블레이드에서 hello 계정 블레이드 선택 **작업 공간 연결을 해제**합니다.</span><span class="sxs-lookup"><span data-stu-id="90205-113">From hello Azure portal, open your Automation account, and in hello Automation account blade, in hello account blade, select **Unlink workspace**.</span></span><br><br> <span data-ttu-id="90205-114">![작업 영역 연결 해제 옵션](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span><span class="sxs-lookup"><span data-stu-id="90205-114">![Unlink workspace option](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span></span><br><br>  
2. <span data-ttu-id="90205-115">Hello 연결 끊기 작업 영역 블레이드 클릭 **worksapce 연결 끊기**합니다.</span><span class="sxs-lookup"><span data-stu-id="90205-115">On hello Unlink workspace blade, click **Unlink worksapce**.</span></span><br><br> <span data-ttu-id="90205-116">![작업 영역 연결 해제 블레이드](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).</span><span class="sxs-lookup"><span data-stu-id="90205-116">![Unlink workspace blade](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).</span></span><br><br>  <span data-ttu-id="90205-117">원하는 tooproceed 확인 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="90205-117">You will receive a prompt verifying you wish tooproceed.</span></span><br><br>
3. <span data-ttu-id="90205-118">Azure 자동화는 toounlink hello 계정 로그 분석 작업 영역을 가져오려고 하는 동안에 아래 hello 진행률을 추적할 수 **알림** hello 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="90205-118">While Azure Automation attempts toounlink hello account your Log Analytics workspace, you can track hello progress under **Notifications** from hello menu.</span></span>

<span data-ttu-id="90205-119">Hello 업데이트 관리 솔루션을 사용 하는 경우 필요에 따라 좋습니다 tooremove hello 다음 hello 솔루션을 제거한 후 더 이상 필요 없는 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="90205-119">If you used hello Update Management solution, optionally you may want tooremove hello following items that are no longer needed after you remove hello solution.</span></span>

* <span data-ttu-id="90205-120">업데이트 일정.</span><span class="sxs-lookup"><span data-stu-id="90205-120">Update schedules.</span></span>  <span data-ttu-id="90205-121">각각 만든 hello 업데이트 배포를 일치 하는 이름을 갖습니다)</span><span class="sxs-lookup"><span data-stu-id="90205-121">Each will have names that match hello update deployments you created)</span></span>

* <span data-ttu-id="90205-122">하이브리드 작업자 그룹 hello 솔루션에 대 한 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="90205-122">Hybrid worker groups created for hello solution.</span></span>  <span data-ttu-id="90205-123">각각 지정 됩니다. 마찬가지로 너무 machine1.contoso.com_9ceb8108-26 c 9-4051-b6b3-227600d715c8).</span><span class="sxs-lookup"><span data-stu-id="90205-123">Each will be named similarly too machine1.contoso.com_9ceb8108-26c9-4051-b6b3-227600d715c8).</span></span>

<span data-ttu-id="90205-124">업무 시간 이후 솔루션 중 hello 시작/중지 Vm에 사용한, 필요에 따라 경우 tooremove hello 다음 hello 솔루션을 제거한 후 더 이상 필요 없는 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="90205-124">If you used hello Start/Stop VMs during off-hours solution, optionally you may want tooremove hello following items that are no longer needed after you remove hello solution.</span></span>

* <span data-ttu-id="90205-125">VM runbook 시작 및 중지 일정</span><span class="sxs-lookup"><span data-stu-id="90205-125">Start and stop VM runbook schedules</span></span> 
* <span data-ttu-id="90205-126">VM runbook 시작 및 중지</span><span class="sxs-lookup"><span data-stu-id="90205-126">Start and stop VM runbooks</span></span>
* <span data-ttu-id="90205-127">변수</span><span class="sxs-lookup"><span data-stu-id="90205-127">Variables</span></span>   

## <a name="next-steps"></a><span data-ttu-id="90205-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="90205-128">Next steps</span></span>

<span data-ttu-id="90205-129">tooreconfigure OMS 로그 분석을 하 여 자동화 계정 toointegrate 참조 [자동화 tooLog 분석 (OMS)에서 작업 상태 및 작업 스트림 전달](automation-manage-send-joblogs-log-analytics.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="90205-129">tooreconfigure your Automation account toointegrate with OMS Log Analytics, see [Forward job status and job streams from Automation tooLog Analytics (OMS)](automation-manage-send-joblogs-log-analytics.md).</span></span> 
