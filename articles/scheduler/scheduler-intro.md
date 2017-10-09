---
title: "aaaWhat은 Azure 스케줄러는? | Microsoft Docs"
description: "Azure 스케줄러 있습니다 toodeclaratively hello 클라우드에서 toorun 동작에 설명 합니다. 그런 다음 해당 작업을 예약하고 자동으로 실행합니다."
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
ms.openlocfilehash: 062e25ae473510264dc0038198c05e7ac1e86210
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-scheduler"></a><span data-ttu-id="d5287-105">Azure 스케줄러 정의</span><span class="sxs-lookup"><span data-stu-id="d5287-105">What is Azure Scheduler?</span></span>
<span data-ttu-id="d5287-106">Azure 스케줄러 있습니다 toodeclaratively hello 클라우드에서 toorun 동작에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5287-106">Azure Scheduler allows you toodeclaratively describe actions toorun in hello cloud.</span></span> <span data-ttu-id="d5287-107">그런 다음 해당 작업을 예약하고 자동으로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d5287-107">It then schedules and runs those actions automatically.</span></span>  <span data-ttu-id="d5287-108">스케줄러가 작업을 사용 하 여 수행 [Azure 포털 hello](scheduler-get-started-portal.md), 코드, [REST API](https://msdn.microsoft.com/library/mt629143.aspx), 또는 Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d5287-108">Scheduler does this by using [hello Azure portal](scheduler-get-started-portal.md), code, [REST API](https://msdn.microsoft.com/library/mt629143.aspx), or Azure PowerShell.</span></span>

<span data-ttu-id="d5287-109">스케줄러는 예약된 작업을 만들고 유지 관리하며 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="d5287-109">Scheduler creates, maintains, and invokes scheduled work.</span></span>  <span data-ttu-id="d5287-110">스케줄러는 작업을 호스트하거나 코드를 실행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d5287-110">Scheduler does not host any workloads or run any code.</span></span> <span data-ttu-id="d5287-111">Azure, 온-프레미스 또는 다른 공급자를 통해 다른 곳에서 호스트되는 코드를 *호출*하기만 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5287-111">It only *invokes* code hosted elsewhere—in Azure, on-premises, or with another provider.</span></span> <span data-ttu-id="d5287-112">HTTP, HTTPS, 저장소 큐, 서비스 버스 큐 또는 서비스 버스 항목을 통해 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="d5287-112">It invokes via HTTP, HTTPS, a storage queue, a service bus queue, or a service bus topic.</span></span>

<span data-ttu-id="d5287-113">스케줄러 일정 [작업](scheduler-concepts-terms.md), 하나를 검토할 수, 및 일정 작업 toobe 실행 명확 하 게 하 고 안정적으로 작업 실행 결과 기록을 보관 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5287-113">Scheduler schedules [jobs](scheduler-concepts-terms.md), keeps a history of job execution results that one can review, and deterministically and reliably schedules workloads toobe run.</span></span> <span data-ttu-id="d5287-114">Azure WebJobs (Azure 앱 서비스의 웹 응용 프로그램 기능 hello의 일부) 및 기타 Azure 예약 기능 hello 백그라운드에서 스케줄러를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5287-114">Azure WebJobs (part of hello Web Apps feature in Azure App Service) and other Azure scheduling capabilities use Scheduler in hello background.</span></span> <span data-ttu-id="d5287-115">hello [스케줄러 REST API](https://msdn.microsoft.com/library/mt629143.aspx) 사용 하면 이러한 작업에 대 한 hello 통신을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5287-115">hello [Scheduler REST API](https://msdn.microsoft.com/library/mt629143.aspx) helps manage hello communication for these actions.</span></span> <span data-ttu-id="d5287-116">이와 같이 스케줄러는 [복잡한 일정 및 고급 되풀이](scheduler-advanced-complexity.md) 를 간편하게 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d5287-116">As such, Scheduler supports [complex schedules and advanced recurrence](scheduler-advanced-complexity.md) easily.</span></span>

<span data-ttu-id="d5287-117">스케줄러의 toohello 사용량을 활용 하는 몇 가지 시나리오가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5287-117">There are several scenarios that lend themselves toohello usage of Scheduler.</span></span> <span data-ttu-id="d5287-118">예:</span><span class="sxs-lookup"><span data-stu-id="d5287-118">For example:</span></span>

* <span data-ttu-id="d5287-119">*응용 프로그램 작업 되풀이:* 주기적으로 Twitter에서 피드로 데이터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="d5287-119">*Recurring application actions:* Periodically gathering data from Twitter into a feed.</span></span>
* <span data-ttu-id="d5287-120">*일별 유지 관리:* 일별 로그 잘라내기, 백업 수행 및 기타 유지 관리 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="d5287-120">*Daily maintenance:* Daily pruning of logs, performing backups, and other maintenance tasks.</span></span> <span data-ttu-id="d5287-121">예를 들어 관리자가 수도 tooback hello 데이터베이스를 오전 1 시에</span><span class="sxs-lookup"><span data-stu-id="d5287-121">For example, an administrator may choose tooback up hello database at 1:00 A.M.</span></span> <span data-ttu-id="d5287-122">매일 hello에 대 한 다음 9 개월입니다.</span><span class="sxs-lookup"><span data-stu-id="d5287-122">every day for hello next nine months.</span></span>

<span data-ttu-id="d5287-123">스케줄러에서는 toocreate, 업데이트, 삭제, 보기 및 작업 관리 및 [작업 컬렉션을](scheduler-concepts-terms.md) hello 포털 및 스크립트를 사용 하 여 프로그래밍 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5287-123">Scheduler allows you toocreate, update, delete, view, and manage jobs and [job collections](scheduler-concepts-terms.md) programmatically, by using scripts, and in hello portal.</span></span>

## <a name="see-also"></a><span data-ttu-id="d5287-124">참고 항목</span><span class="sxs-lookup"><span data-stu-id="d5287-124">See also</span></span>
 [<span data-ttu-id="d5287-125">Azure 스케줄러 개념, 용어 및 엔터티 계층 구조</span><span class="sxs-lookup"><span data-stu-id="d5287-125">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="d5287-126">Hello Azure 포털에서에서 스케줄러 사용 시작</span><span class="sxs-lookup"><span data-stu-id="d5287-126">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="d5287-127">Azure 스케줄러의 버전 및 요금 청구</span><span class="sxs-lookup"><span data-stu-id="d5287-127">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="d5287-128">일정을 toobuild 복잡 한 방법 및 Azure 스케줄러와 고급 되풀이</span><span class="sxs-lookup"><span data-stu-id="d5287-128">How toobuild complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="d5287-129">Azure 스케줄러 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="d5287-129">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="d5287-130">Azure 스케줄러 PowerShell cmdlet 참조</span><span class="sxs-lookup"><span data-stu-id="d5287-130">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="d5287-131">Azure 스케줄러 고가용성 및 안정성</span><span class="sxs-lookup"><span data-stu-id="d5287-131">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="d5287-132">Azure 스케줄러 제한, 기본값 및 오류 코드</span><span class="sxs-lookup"><span data-stu-id="d5287-132">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="d5287-133">Azure 스케줄러 아웃바운드 인증</span><span class="sxs-lookup"><span data-stu-id="d5287-133">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

