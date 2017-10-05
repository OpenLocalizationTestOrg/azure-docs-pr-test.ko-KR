---
title: "작업 로그를 사용하여 BizTalk 서비스 문제 해결 | Microsoft Docs"
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
ms.openlocfilehash: c0c83361f94ffd9c30d7fcc551ff4b85ad7d6fa5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="biztalk-services-troubleshoot-using-operation-logs"></a><span data-ttu-id="eb0fc-104">BizTalk 서비스: 작업 로그를 사용한 문제 해결</span><span class="sxs-lookup"><span data-stu-id="eb0fc-104">BizTalk Services: Troubleshoot using operation logs</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

## <a name="what-are-the-operation-logs"></a><span data-ttu-id="eb0fc-105">작업 로그의 정의</span><span class="sxs-lookup"><span data-stu-id="eb0fc-105">What are the Operation Logs</span></span>
<span data-ttu-id="eb0fc-106">작업 로그는 Azure 클래식 포털에서 사용할 수 있는 관리 서비스 기능으로서 BizTalk 서비스를 포함한 Azure 서비스에서 수행된 작업의 기록 로그를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb0fc-106">Operation Logs is a Management Services feature available in the Azure classic portal that allows you to view historical logs of operations performed on your Azure services, including BizTalk Services.</span></span> <span data-ttu-id="eb0fc-107">이렇게 하면 BizTalk 서비스 구독에서 180일 이전의 관리 작업과 관련된 기록 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb0fc-107">This enables you to view historical data related to management operations on your BizTalk Service subscription as far back as 180 days.</span></span>

> [!NOTE]
> <span data-ttu-id="eb0fc-108">이 기능은 서비스가 시작되었을 경우, 백업되었을 경우 등과 같은 BizTalk 서비스의 관리 작업에 대한 로그만 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="eb0fc-108">This feature only captures logs for management operations on BizTalk Services, such as when the service was started, backed up, and so on.</span></span> <span data-ttu-id="eb0fc-109">이러한 작업은 Azure 클래식 포털에서 수행되었는지 또는 [BizTalk 서비스 REST API](http://msdn.microsoft.com/library/azure/dn232347.aspx)를 사용하여 수행되었는지 여부에 관계없이 추적됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb0fc-109">Such operations are tracked irrespective of whether they are performed from the Azure classic portal or by using the [BizTalk Service REST APIs](http://msdn.microsoft.com/library/azure/dn232347.aspx).</span></span> <span data-ttu-id="eb0fc-110">관리 서비스를 사용하여 추적된 작업의 전체 목록을 보려면 [Azure 관리 서비스를 사용하여 추적된 작업](#bizops)를 사용하여 수행되었는지 여부에 관계없이 추적됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb0fc-110">For a complete list of operations that are tracked using Management Services, see [Operations Tracked Using Azure Management Services](#bizops).</span></span><br/><br/>
> <span data-ttu-id="eb0fc-111">BizTalk 서비스 런타임과 관련된 작업(예: 브리지에서 처리하는 메시지 등)에 대한 로그는 캡처하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eb0fc-111">This does not capture the logs for activities related to BizTalk Service runtime (such as message processed by bridges, and so on.).</span></span> <span data-ttu-id="eb0fc-112">이러한 로그를 보려면 BizTalk 서비스 포털에서 추적 뷰를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="eb0fc-112">To view these logs, use the Tracking view from the BizTalk Services portal.</span></span> <span data-ttu-id="eb0fc-113">자세한 내용은 [메시지 추적](http://msdn.microsoft.com/library/azure/hh949805.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eb0fc-113">For more information, see [Tracking Messages](http://msdn.microsoft.com/library/azure/hh949805.aspx).</span></span>
> 
> 

## <a name="view-biztalk-services-operation-logs"></a><span data-ttu-id="eb0fc-114">BizTalk 서비스 작업 로그 보기</span><span class="sxs-lookup"><span data-stu-id="eb0fc-114">View BizTalk Services Operation Logs</span></span>
1. <span data-ttu-id="eb0fc-115">Azure 클래식 포털에서 **관리 서비스**를 선택한 다음 **작업 로그** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eb0fc-115">In the Azure classic portal, select **Management Services**, and then select the **Operation Logs** tab.</span></span>
2. <span data-ttu-id="eb0fc-116">구독, 날짜 범위, 서비스 종류(예: BizTalk 서비스), 서비스 이름 또는 상태(작업 상태, 예: 성공, 실패)와 같은 다양한 매개 변수를 기준으로 로그를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb0fc-116">You can filter the logs based on different parameters like subscription, date range, service type (e.g. BizTalk Services), service name, or status of the operation (Succeeded, Failed).</span></span>
3. <span data-ttu-id="eb0fc-117">확인 표시를 선택하여 필터링된 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="eb0fc-117">Select the checkmark to view the filtered list.</span></span> <span data-ttu-id="eb0fc-118">다음 그림은 testbiztalkservice와 관련된 작업을 보여 줍니다. ![작업 로그 보기][ViewLogs]</span><span class="sxs-lookup"><span data-stu-id="eb0fc-118">The following image shows activities related to testbiztalkservice: ![View operation logs][ViewLogs]</span></span> 
4. <span data-ttu-id="eb0fc-119">특정 작업에 대한 자세한 내용을 보려면 아래쪽의 작업 표시줄에서 **세부 정보** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eb0fc-119">To view more about a specific operation, select the row, and click **Details** in the task bar at the bottom.</span></span>

## <span data-ttu-id="eb0fc-120"><a name="bizops"></a>Azure 관리 서비스를 사용하여 추적된 작업</span><span class="sxs-lookup"><span data-stu-id="eb0fc-120"><a name="bizops"></a>Operations Tracked Using Azure Management Services</span></span>
<span data-ttu-id="eb0fc-121">다음 표에서는 Azure 관리 서비스를 사용하여 추적된 작업의 목록을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="eb0fc-121">The following table lists the operations that are tracked using the Azure Management Services:</span></span>

| <span data-ttu-id="eb0fc-122">작업 이름</span><span class="sxs-lookup"><span data-stu-id="eb0fc-122">Operation Name</span></span> | <span data-ttu-id="eb0fc-123">작업</span><span class="sxs-lookup"><span data-stu-id="eb0fc-123">Task</span></span> |
| --- | --- |
| <span data-ttu-id="eb0fc-124">CreateBizTalkService</span><span class="sxs-lookup"><span data-stu-id="eb0fc-124">CreateBizTalkService</span></span> |<span data-ttu-id="eb0fc-125">새 BizTalk 서비스를 만드는 작업</span><span class="sxs-lookup"><span data-stu-id="eb0fc-125">Operation to create a new BizTalk Service</span></span> |
| <span data-ttu-id="eb0fc-126">DeleteBizTalkService</span><span class="sxs-lookup"><span data-stu-id="eb0fc-126">DeleteBizTalkService</span></span> |<span data-ttu-id="eb0fc-127">BizTalk 서비스를 삭제하는 작업</span><span class="sxs-lookup"><span data-stu-id="eb0fc-127">Operation to delete a BizTalk Service</span></span> |
| <span data-ttu-id="eb0fc-128">RestartBizTalkService</span><span class="sxs-lookup"><span data-stu-id="eb0fc-128">RestartBizTalkService</span></span> |<span data-ttu-id="eb0fc-129">BizTalk 서비스를 다시 시작하는 작업</span><span class="sxs-lookup"><span data-stu-id="eb0fc-129">Operation to restart a BizTalk Service</span></span> |
| <span data-ttu-id="eb0fc-130">StartBizTalkService</span><span class="sxs-lookup"><span data-stu-id="eb0fc-130">StartBizTalkService</span></span> |<span data-ttu-id="eb0fc-131">BizTalk 서비스를 시작하는 작업</span><span class="sxs-lookup"><span data-stu-id="eb0fc-131">Operation to start a BizTalk Service</span></span> |
| <span data-ttu-id="eb0fc-132">StopBizTalkService</span><span class="sxs-lookup"><span data-stu-id="eb0fc-132">StopBizTalkService</span></span> |<span data-ttu-id="eb0fc-133">BizTalk 서비스를 중지하는 작업</span><span class="sxs-lookup"><span data-stu-id="eb0fc-133">Operation to stop a BizTalk Service</span></span> |
| <span data-ttu-id="eb0fc-134">DisableBizTalkService</span><span class="sxs-lookup"><span data-stu-id="eb0fc-134">DisableBizTalkService</span></span> |<span data-ttu-id="eb0fc-135">BizTalk 서비스를 사용하지 않도록 설정하는 작업</span><span class="sxs-lookup"><span data-stu-id="eb0fc-135">Operation to disable a BizTalk Service</span></span> |
| <span data-ttu-id="eb0fc-136">EnableBizTalkService</span><span class="sxs-lookup"><span data-stu-id="eb0fc-136">EnableBizTalkService</span></span> |<span data-ttu-id="eb0fc-137">BizTalk 서비스를 사용하도록 설정하는 작업</span><span class="sxs-lookup"><span data-stu-id="eb0fc-137">Operation to enable a BizTalk Service</span></span> |
| <span data-ttu-id="eb0fc-138">BackupBizTalkService</span><span class="sxs-lookup"><span data-stu-id="eb0fc-138">BackupBizTalkService</span></span> |<span data-ttu-id="eb0fc-139">BizTalk 서비스를 백업하는 작업</span><span class="sxs-lookup"><span data-stu-id="eb0fc-139">Operation to back up a BizTalk Service</span></span> |
| <span data-ttu-id="eb0fc-140">RestoreBizTalkService</span><span class="sxs-lookup"><span data-stu-id="eb0fc-140">RestoreBizTalkService</span></span> |<span data-ttu-id="eb0fc-141">BizTalk 서비스를 지정된 백업에서 복원하는 작업</span><span class="sxs-lookup"><span data-stu-id="eb0fc-141">Operation to restore a BizTalk Service from specified backup</span></span> |
| <span data-ttu-id="eb0fc-142">SuspendBizTalkService</span><span class="sxs-lookup"><span data-stu-id="eb0fc-142">SuspendBizTalkService</span></span> |<span data-ttu-id="eb0fc-143">BizTalk 서비스를 일시 중단하는 작업</span><span class="sxs-lookup"><span data-stu-id="eb0fc-143">Operation to suspend a BizTalk Service</span></span> |
| <span data-ttu-id="eb0fc-144">ResumeBizTalkService</span><span class="sxs-lookup"><span data-stu-id="eb0fc-144">ResumeBizTalkService</span></span> |<span data-ttu-id="eb0fc-145">BizTalk 서비스를 다시 시작하는 작업</span><span class="sxs-lookup"><span data-stu-id="eb0fc-145">Operation to resume a BizTalk Service</span></span> |
| <span data-ttu-id="eb0fc-146">ScaleBizTalkService</span><span class="sxs-lookup"><span data-stu-id="eb0fc-146">ScaleBizTalkService</span></span> |<span data-ttu-id="eb0fc-147">BizTalk 서비스의 규모를 확장하거나 축소하는 작업</span><span class="sxs-lookup"><span data-stu-id="eb0fc-147">Operation to scale a BizTalk Service up or down</span></span> |
| <span data-ttu-id="eb0fc-148">ConfigUpdateBizTalkService</span><span class="sxs-lookup"><span data-stu-id="eb0fc-148">ConfigUpdateBizTalkService</span></span> |<span data-ttu-id="eb0fc-149">BizTalk 서비스의 구성을 업데이트하는 작업</span><span class="sxs-lookup"><span data-stu-id="eb0fc-149">Operation to update the configuration of a BizTalk Service</span></span> |
| <span data-ttu-id="eb0fc-150">ServiceUpdateBizTalkService</span><span class="sxs-lookup"><span data-stu-id="eb0fc-150">ServiceUpdateBizTalkService</span></span> |<span data-ttu-id="eb0fc-151">BizTalk 서비스를 다른 버전으로 업그레이드하거나 다운그레이드하는 작업</span><span class="sxs-lookup"><span data-stu-id="eb0fc-151">Operation to upgrade or downgrade a BizTalk Service to a different version</span></span> |
| <span data-ttu-id="eb0fc-152">PurgeBackupBizTalkService</span><span class="sxs-lookup"><span data-stu-id="eb0fc-152">PurgeBackupBizTalkService</span></span> |<span data-ttu-id="eb0fc-153">보존 기간이 지난 BizTalk 서비스의 백업을 삭제하는 작업</span><span class="sxs-lookup"><span data-stu-id="eb0fc-153">Operation to purge backups of the BizTalk Service outside the retention period</span></span> |

## <a name="see-also"></a><span data-ttu-id="eb0fc-154">참고 항목</span><span class="sxs-lookup"><span data-stu-id="eb0fc-154">See Also</span></span>
* [<span data-ttu-id="eb0fc-155">BizTalk 서비스 백업</span><span class="sxs-lookup"><span data-stu-id="eb0fc-155">Backup BizTalk Service</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [<span data-ttu-id="eb0fc-156">백업에서 BizTalk 서비스 복원</span><span class="sxs-lookup"><span data-stu-id="eb0fc-156">Restore BizTalk Service from Backup</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [<span data-ttu-id="eb0fc-157">BizTalk 서비스: Developer, Basic, Standard 및 Premium Editions 차트</span><span class="sxs-lookup"><span data-stu-id="eb0fc-157">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [<span data-ttu-id="eb0fc-158">BizTalk 서비스: Azure 클래식 포털을 사용하여 프로비전</span><span class="sxs-lookup"><span data-stu-id="eb0fc-158">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [<span data-ttu-id="eb0fc-159">BizTalk 서비스: 프로비저닝 상태 차트</span><span class="sxs-lookup"><span data-stu-id="eb0fc-159">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [<span data-ttu-id="eb0fc-160">BizTalk 서비스: 대시보드, 모니터 및 크기 조정 탭</span><span class="sxs-lookup"><span data-stu-id="eb0fc-160">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [<span data-ttu-id="eb0fc-161">BizTalk 서비스: 제한</span><span class="sxs-lookup"><span data-stu-id="eb0fc-161">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [<span data-ttu-id="eb0fc-162">BizTalk 서비스: 발급자 이름 및 발급자 키</span><span class="sxs-lookup"><span data-stu-id="eb0fc-162">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [<span data-ttu-id="eb0fc-163">Azure BizTalk 서비스 SDK로 시작하는 방법</span><span class="sxs-lookup"><span data-stu-id="eb0fc-163">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[ViewLogs]: ./media/biztalk-troubleshoot-using-ops-logs/Operation-Logs.png

