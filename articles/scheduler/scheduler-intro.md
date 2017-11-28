---
title: "Azure 스케줄러 정의 | Microsoft Docs"
description: "Azure 스케줄러를 사용하면 클라우드에서 실행할 작업을 선언적으로 설명할 수 있습니다. 그런 다음 해당 작업을 예약하고 자동으로 실행합니다."
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 52aa6ae1-4c3d-43fb-81b0-6792c84bcfae
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: a3bf1aacd6978499d7ef77cbcb451a06b857ac38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-azure-scheduler"></a><span data-ttu-id="6ad70-105">Azure 스케줄러 정의</span><span class="sxs-lookup"><span data-stu-id="6ad70-105">What is Azure Scheduler?</span></span>
<span data-ttu-id="6ad70-106">Azure 스케줄러를 사용하면 클라우드에서 실행할 작업을 선언적으로 설명할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ad70-106">Azure Scheduler allows you to declaratively describe actions to run in the cloud.</span></span> <span data-ttu-id="6ad70-107">그런 다음 해당 작업을 예약하고 자동으로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6ad70-107">It then schedules and runs those actions automatically.</span></span>  <span data-ttu-id="6ad70-108">스케줄러에서는 [Azure 포털](scheduler-get-started-portal.md), 코드, [REST API](https://msdn.microsoft.com/library/mt629143.aspx) 또는 Azure PowerShell을 사용하여 이를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6ad70-108">Scheduler does this by using [the Azure portal](scheduler-get-started-portal.md), code, [REST API](https://msdn.microsoft.com/library/mt629143.aspx), or Azure PowerShell.</span></span>

<span data-ttu-id="6ad70-109">스케줄러는 예약된 작업을 만들고 유지 관리하며 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="6ad70-109">Scheduler creates, maintains, and invokes scheduled work.</span></span>  <span data-ttu-id="6ad70-110">스케줄러는 작업을 호스트하거나 코드를 실행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6ad70-110">Scheduler does not host any workloads or run any code.</span></span> <span data-ttu-id="6ad70-111">Azure, 온-프레미스 또는 다른 공급자를 통해 다른 곳에서 호스트되는 코드를 *호출*하기만 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ad70-111">It only *invokes* code hosted elsewhere—in Azure, on-premises, or with another provider.</span></span> <span data-ttu-id="6ad70-112">HTTP, HTTPS, 저장소 큐, 서비스 버스 큐 또는 서비스 버스 항목을 통해 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="6ad70-112">It invokes via HTTP, HTTPS, a storage queue, a service bus queue, or a service bus topic.</span></span>

<span data-ttu-id="6ad70-113">스케줄러는 [작업](scheduler-concepts-terms.md)을 예약하고, 사용자가 검토할 수 있는 작업 실행 결과의 기록을 유지하고, 실행할 작업을 명확하고 안정적으로 예약합니다.</span><span class="sxs-lookup"><span data-stu-id="6ad70-113">Scheduler schedules [jobs](scheduler-concepts-terms.md), keeps a history of job execution results that one can review, and deterministically and reliably schedules workloads to be run.</span></span> <span data-ttu-id="6ad70-114">Azure WebJobs(Azure 앱 서비스에서 웹앱 기능의 일부) 및 다른 Azure 일정 기능은 백그라운드에서 스케줄러를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6ad70-114">Azure WebJobs (part of the Web Apps feature in Azure App Service) and other Azure scheduling capabilities use Scheduler in the background.</span></span> <span data-ttu-id="6ad70-115">[스케줄러 REST API](https://msdn.microsoft.com/library/mt629143.aspx) 는 이러한 작업에 대한 통신을 관리하도록 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="6ad70-115">The [Scheduler REST API](https://msdn.microsoft.com/library/mt629143.aspx) helps manage the communication for these actions.</span></span> <span data-ttu-id="6ad70-116">이와 같이 스케줄러는 [복잡한 일정 및 고급 되풀이](scheduler-advanced-complexity.md) 를 간편하게 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6ad70-116">As such, Scheduler supports [complex schedules and advanced recurrence](scheduler-advanced-complexity.md) easily.</span></span>

<span data-ttu-id="6ad70-117">스케줄러를 사용하는 여러 가지 시나리오가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ad70-117">There are several scenarios that lend themselves to the usage of Scheduler.</span></span> <span data-ttu-id="6ad70-118">예:</span><span class="sxs-lookup"><span data-stu-id="6ad70-118">For example:</span></span>

* <span data-ttu-id="6ad70-119">*응용 프로그램 작업 되풀이:* 주기적으로 Twitter에서 피드로 데이터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="6ad70-119">*Recurring application actions:* Periodically gathering data from Twitter into a feed.</span></span>
* <span data-ttu-id="6ad70-120">*일별 유지 관리:* 일별 로그 잘라내기, 백업 수행 및 기타 유지 관리 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="6ad70-120">*Daily maintenance:* Daily pruning of logs, performing backups, and other maintenance tasks.</span></span> <span data-ttu-id="6ad70-121">예, 관리자 오전 1 시에 데이터베이스를 백업 하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ad70-121">For example, an administrator may choose to back up the database at 1:00 A.M.</span></span> <span data-ttu-id="6ad70-122">다음 9 개월 동안 매일입니다.</span><span class="sxs-lookup"><span data-stu-id="6ad70-122">every day for the next nine months.</span></span>

<span data-ttu-id="6ad70-123">스케줄러를 사용하면 포털에서 스크립트를 통해 작업 및 [작업 컬렉션](scheduler-concepts-terms.md) 을 프로그래밍 방식으로 만들고, 업데이트하고, 삭제하고, 보고, 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ad70-123">Scheduler allows you to create, update, delete, view, and manage jobs and [job collections](scheduler-concepts-terms.md) programmatically, by using scripts, and in the portal.</span></span>

## <a name="see-also"></a><span data-ttu-id="6ad70-124">참고 항목</span><span class="sxs-lookup"><span data-stu-id="6ad70-124">See also</span></span>
 [<span data-ttu-id="6ad70-125">Azure 스케줄러 개념, 용어 및 엔터티 계층 구조</span><span class="sxs-lookup"><span data-stu-id="6ad70-125">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="6ad70-126">Azure 포털에서 스케줄러 사용 시작</span><span class="sxs-lookup"><span data-stu-id="6ad70-126">Get started using Scheduler in the Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="6ad70-127">Azure 스케줄러의 버전 및 요금 청구</span><span class="sxs-lookup"><span data-stu-id="6ad70-127">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="6ad70-128">Azure 스케줄러를 사용하여 복잡한 일정 및 고급 되풀이를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="6ad70-128">How to build complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="6ad70-129">Azure 스케줄러 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="6ad70-129">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="6ad70-130">Azure 스케줄러 PowerShell cmdlet 참조</span><span class="sxs-lookup"><span data-stu-id="6ad70-130">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="6ad70-131">Azure 스케줄러 고가용성 및 안정성</span><span class="sxs-lookup"><span data-stu-id="6ad70-131">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="6ad70-132">Azure 스케줄러 제한, 기본값 및 오류 코드</span><span class="sxs-lookup"><span data-stu-id="6ad70-132">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="6ad70-133">Azure 스케줄러 아웃바운드 인증</span><span class="sxs-lookup"><span data-stu-id="6ad70-133">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

