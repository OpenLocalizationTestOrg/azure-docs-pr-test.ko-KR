---
title: "작업 로그를 사용 하 여 aaaTroubleshoot BizTalk 서비스 | Microsoft Docs"
description: "작업 로그를 사용하여 BizTalk 서비스의 문제를 해결합니다. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 1081a9c6-58cc-4a76-8ac8-11e5e7a6ea27
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 102779ed6e29784f190c28e4102a7d9670614914
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-troubleshoot-using-operation-logs"></a><span data-ttu-id="aa251-104">BizTalk 서비스: 작업 로그를 사용한 문제 해결</span><span class="sxs-lookup"><span data-stu-id="aa251-104">BizTalk Services: Troubleshoot using operation logs</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

## <a name="what-are-hello-operation-logs"></a><span data-ttu-id="aa251-105">Hello 작업 로그는 무엇입니까</span><span class="sxs-lookup"><span data-stu-id="aa251-105">What are hello Operation Logs</span></span>
<span data-ttu-id="aa251-106">작업 로그에는 hello tooview BizTalk 서비스를 포함 한, Azure 서비스에 대 한 작업 기록 로그 수 있는 Azure 클래식 포털에서에서 사용할 수 있는 관리 서비스 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="aa251-106">Operation Logs is a Management Services feature available in hello Azure classic portal that allows you tooview historical logs of operations performed on your Azure services, including BizTalk Services.</span></span> <span data-ttu-id="aa251-107">이렇게 하면 기록 데이터 tooview 관련 180 일 이전에 출시 BizTalk 서비스 구독에 대해 toomanagement 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa251-107">This enables you tooview historical data related toomanagement operations on your BizTalk Service subscription as far back as 180 days.</span></span>

> [!NOTE]
> <span data-ttu-id="aa251-108">이 기능은 등, 최대 백업 hello 서비스 시작 되었을 때와 같은 BizTalk 서비스에서 관리 작업에 대 한 로그를 캡처합니다만.</span><span class="sxs-lookup"><span data-stu-id="aa251-108">This feature only captures logs for management operations on BizTalk Services, such as when hello service was started, backed up, and so on.</span></span> <span data-ttu-id="aa251-109">Hello Azure 클래식 포털에서에서 또는 hello를 사용 하 여 수행 여부에 관계 없이 이러한 작업은 추적 [BizTalk 서비스 REST Api](http://msdn.microsoft.com/library/azure/dn232347.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="aa251-109">Such operations are tracked irrespective of whether they are performed from hello Azure classic portal or by using hello [BizTalk Service REST APIs](http://msdn.microsoft.com/library/azure/dn232347.aspx).</span></span> <span data-ttu-id="aa251-110">관리 서비스를 사용하여 추적된 작업의 전체 목록을 보려면 [Azure 관리 서비스를 사용하여 추적된 작업](#bizops)를 사용하여 수행되었는지 여부에 관계없이 추적됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa251-110">For a complete list of operations that are tracked using Management Services, see [Operations Tracked Using Azure Management Services](#bizops).</span></span><br/><br/>
> <span data-ttu-id="aa251-111">활동 관련된 tooBizTalk 서비스 런타임 (예: 메시지 브리지에 의해 처리 됩니다.)에 대 한 hello 로그 캡처하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="aa251-111">This does not capture hello logs for activities related tooBizTalk Service runtime (such as message processed by bridges, and so on.).</span></span> <span data-ttu-id="aa251-112">tooview 이러한 로그를 사용 하 여 hello hello BizTalk 서비스 포털에서 뷰를 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa251-112">tooview these logs, use hello Tracking view from hello BizTalk Services portal.</span></span> <span data-ttu-id="aa251-113">자세한 내용은 [메시지 추적](http://msdn.microsoft.com/library/azure/hh949805.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aa251-113">For more information, see [Tracking Messages](http://msdn.microsoft.com/library/azure/hh949805.aspx).</span></span>
> 
> 

## <a name="view-biztalk-services-operation-logs"></a><span data-ttu-id="aa251-114">BizTalk 서비스 작업 로그 보기</span><span class="sxs-lookup"><span data-stu-id="aa251-114">View BizTalk Services Operation Logs</span></span>
1. <span data-ttu-id="aa251-115">Hello Azure 클래식 포털에서에서 선택 **관리 서비스**를 선택한 후 hello **작업 로그** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa251-115">In hello Azure classic portal, select **Management Services**, and then select hello **Operation Logs** tab.</span></span>
2. <span data-ttu-id="aa251-116">구독, 날짜 범위, 서비스 유형 (예: BizTalk 서비스), 서비스 이름 또는 (Succeeded, Failed) hello 작업의 상태와 같은 다른 매개 변수를 기준으로 하는 hello 로그를 필터링 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa251-116">You can filter hello logs based on different parameters like subscription, date range, service type (e.g. BizTalk Services), service name, or status of hello operation (Succeeded, Failed).</span></span>
3. <span data-ttu-id="aa251-117">선택 hello 확인 표시 tooview hello 필터링 된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="aa251-117">Select hello checkmark tooview hello filtered list.</span></span> <span data-ttu-id="aa251-118">hello 다음 그림에 나와 활동 관련된 tootestbiztalkservice: ![작업 로그를 보려면][ViewLogs]</span><span class="sxs-lookup"><span data-stu-id="aa251-118">hello following image shows activities related tootestbiztalkservice: ![View operation logs][ViewLogs]</span></span> 
4. <span data-ttu-id="aa251-119">특정 작업에 대해 자세히 tooview hello 행을 선택 하 고 클릭 **세부 정보** hello 맨 아래에 hello 작업 표시줄에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa251-119">tooview more about a specific operation, select hello row, and click **Details** in hello task bar at hello bottom.</span></span>

## <span data-ttu-id="aa251-120"><a name="bizops"></a>Azure 관리 서비스를 사용하여 추적된 작업</span><span class="sxs-lookup"><span data-stu-id="aa251-120"><a name="bizops"></a>Operations Tracked Using Azure Management Services</span></span>
<span data-ttu-id="aa251-121">hello 다음 표에 나타난 hello Azure 관리 서비스를 사용 하 여 추적 되는 hello 작업.</span><span class="sxs-lookup"><span data-stu-id="aa251-121">hello following table lists hello operations that are tracked using hello Azure Management Services:</span></span>

| <span data-ttu-id="aa251-122">작업 이름</span><span class="sxs-lookup"><span data-stu-id="aa251-122">Operation Name</span></span> | <span data-ttu-id="aa251-123">작업</span><span class="sxs-lookup"><span data-stu-id="aa251-123">Task</span></span> |
| --- | --- |
| <span data-ttu-id="aa251-124">CreateBizTalkService</span><span class="sxs-lookup"><span data-stu-id="aa251-124">CreateBizTalkService</span></span> |<span data-ttu-id="aa251-125">작업 toocreate 새 BizTalk 서비스</span><span class="sxs-lookup"><span data-stu-id="aa251-125">Operation toocreate a new BizTalk Service</span></span> |
| <span data-ttu-id="aa251-126">DeleteBizTalkService</span><span class="sxs-lookup"><span data-stu-id="aa251-126">DeleteBizTalkService</span></span> |<span data-ttu-id="aa251-127">작업 toodelete BizTalk 서비스</span><span class="sxs-lookup"><span data-stu-id="aa251-127">Operation toodelete a BizTalk Service</span></span> |
| <span data-ttu-id="aa251-128">RestartBizTalkService</span><span class="sxs-lookup"><span data-stu-id="aa251-128">RestartBizTalkService</span></span> |<span data-ttu-id="aa251-129">작업 toorestart BizTalk 서비스</span><span class="sxs-lookup"><span data-stu-id="aa251-129">Operation toorestart a BizTalk Service</span></span> |
| <span data-ttu-id="aa251-130">StartBizTalkService</span><span class="sxs-lookup"><span data-stu-id="aa251-130">StartBizTalkService</span></span> |<span data-ttu-id="aa251-131">작업 toostart BizTalk 서비스</span><span class="sxs-lookup"><span data-stu-id="aa251-131">Operation toostart a BizTalk Service</span></span> |
| <span data-ttu-id="aa251-132">StopBizTalkService</span><span class="sxs-lookup"><span data-stu-id="aa251-132">StopBizTalkService</span></span> |<span data-ttu-id="aa251-133">작업 toostop BizTalk 서비스</span><span class="sxs-lookup"><span data-stu-id="aa251-133">Operation toostop a BizTalk Service</span></span> |
| <span data-ttu-id="aa251-134">DisableBizTalkService</span><span class="sxs-lookup"><span data-stu-id="aa251-134">DisableBizTalkService</span></span> |<span data-ttu-id="aa251-135">작업 toodisable BizTalk 서비스</span><span class="sxs-lookup"><span data-stu-id="aa251-135">Operation toodisable a BizTalk Service</span></span> |
| <span data-ttu-id="aa251-136">EnableBizTalkService</span><span class="sxs-lookup"><span data-stu-id="aa251-136">EnableBizTalkService</span></span> |<span data-ttu-id="aa251-137">작업 tooenable BizTalk 서비스</span><span class="sxs-lookup"><span data-stu-id="aa251-137">Operation tooenable a BizTalk Service</span></span> |
| <span data-ttu-id="aa251-138">BackupBizTalkService</span><span class="sxs-lookup"><span data-stu-id="aa251-138">BackupBizTalkService</span></span> |<span data-ttu-id="aa251-139">BizTalk 서비스를 tooback 작업</span><span class="sxs-lookup"><span data-stu-id="aa251-139">Operation tooback up a BizTalk Service</span></span> |
| <span data-ttu-id="aa251-140">RestoreBizTalkService</span><span class="sxs-lookup"><span data-stu-id="aa251-140">RestoreBizTalkService</span></span> |<span data-ttu-id="aa251-141">작업 toorestore 지정 된 백업에서 BizTalk 서비스</span><span class="sxs-lookup"><span data-stu-id="aa251-141">Operation toorestore a BizTalk Service from specified backup</span></span> |
| <span data-ttu-id="aa251-142">SuspendBizTalkService</span><span class="sxs-lookup"><span data-stu-id="aa251-142">SuspendBizTalkService</span></span> |<span data-ttu-id="aa251-143">작업 toosuspend BizTalk 서비스</span><span class="sxs-lookup"><span data-stu-id="aa251-143">Operation toosuspend a BizTalk Service</span></span> |
| <span data-ttu-id="aa251-144">ResumeBizTalkService</span><span class="sxs-lookup"><span data-stu-id="aa251-144">ResumeBizTalkService</span></span> |<span data-ttu-id="aa251-145">작업 tooresume BizTalk 서비스</span><span class="sxs-lookup"><span data-stu-id="aa251-145">Operation tooresume a BizTalk Service</span></span> |
| <span data-ttu-id="aa251-146">ScaleBizTalkService</span><span class="sxs-lookup"><span data-stu-id="aa251-146">ScaleBizTalkService</span></span> |<span data-ttu-id="aa251-147">BizTalk service 위나 아래로 이동 작업 tooscale</span><span class="sxs-lookup"><span data-stu-id="aa251-147">Operation tooscale a BizTalk Service up or down</span></span> |
| <span data-ttu-id="aa251-148">ConfigUpdateBizTalkService</span><span class="sxs-lookup"><span data-stu-id="aa251-148">ConfigUpdateBizTalkService</span></span> |<span data-ttu-id="aa251-149">BizTalk 서비스의 작업 tooupdate hello 구성</span><span class="sxs-lookup"><span data-stu-id="aa251-149">Operation tooupdate hello configuration of a BizTalk Service</span></span> |
| <span data-ttu-id="aa251-150">ServiceUpdateBizTalkService</span><span class="sxs-lookup"><span data-stu-id="aa251-150">ServiceUpdateBizTalkService</span></span> |<span data-ttu-id="aa251-151">작업 tooupgrade 하거나 BizTalk 서비스 tooa 다른 버전 다운 그레이드</span><span class="sxs-lookup"><span data-stu-id="aa251-151">Operation tooupgrade or downgrade a BizTalk Service tooa different version</span></span> |
| <span data-ttu-id="aa251-152">PurgeBackupBizTalkService</span><span class="sxs-lookup"><span data-stu-id="aa251-152">PurgeBackupBizTalkService</span></span> |<span data-ttu-id="aa251-153">Hello 보존 기간이 hello BizTalk 서비스의 작업 toopurge 백업</span><span class="sxs-lookup"><span data-stu-id="aa251-153">Operation toopurge backups of hello BizTalk Service outside hello retention period</span></span> |

## <a name="see-also"></a><span data-ttu-id="aa251-154">참고 항목</span><span class="sxs-lookup"><span data-stu-id="aa251-154">See Also</span></span>
* [<span data-ttu-id="aa251-155">BizTalk 서비스 백업</span><span class="sxs-lookup"><span data-stu-id="aa251-155">Backup BizTalk Service</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [<span data-ttu-id="aa251-156">백업에서 BizTalk 서비스 복원</span><span class="sxs-lookup"><span data-stu-id="aa251-156">Restore BizTalk Service from Backup</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [<span data-ttu-id="aa251-157">BizTalk 서비스: Developer, Basic, Standard 및 Premium Editions 차트</span><span class="sxs-lookup"><span data-stu-id="aa251-157">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [<span data-ttu-id="aa251-158">BizTalk 서비스: Azure 클래식 포털을 사용하여 프로비전</span><span class="sxs-lookup"><span data-stu-id="aa251-158">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [<span data-ttu-id="aa251-159">BizTalk 서비스: 프로비저닝 상태 차트</span><span class="sxs-lookup"><span data-stu-id="aa251-159">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [<span data-ttu-id="aa251-160">BizTalk 서비스: 대시보드, 모니터 및 크기 조정 탭</span><span class="sxs-lookup"><span data-stu-id="aa251-160">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [<span data-ttu-id="aa251-161">BizTalk 서비스: 제한</span><span class="sxs-lookup"><span data-stu-id="aa251-161">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [<span data-ttu-id="aa251-162">BizTalk 서비스: 발급자 이름 및 발급자 키</span><span class="sxs-lookup"><span data-stu-id="aa251-162">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [<span data-ttu-id="aa251-163">Azure BizTalk 서비스 SDK를 hello 어떻게 사용 하 여 시작 합니까</span><span class="sxs-lookup"><span data-stu-id="aa251-163">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[ViewLogs]: ./media/biztalk-troubleshoot-using-ops-logs/Operation-Logs.png

