---
title: "aaaMonitor 리소스 관리자를 통해 배포 된 가상 컴퓨터 백업을 | Microsoft Docs"
description: "Resource Manager로 배포된 가상 컴퓨터 백업에서 이벤트 및 경고를 모니터링합니다. 경고에 기반한 전자 메일을 보냅니다."
services: backup
documentationcenter: dev-center-name
author: markgalioto
manager: carmonm
editor: 
ms.assetid: fed32015-2db2-44f8-b204-d89f6fd1bea2
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/21/2016
ms.author: markgal;trinadhk;giridham;
ms.openlocfilehash: bf45cbaa05621b2365c26bafa1bd8223a444c1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-alerts-for-azure-virtual-machine-backups"></a><span data-ttu-id="5e064-104">Azure 가상 컴퓨터 백업에 대한 경고 모니터링</span><span class="sxs-lookup"><span data-stu-id="5e064-104">Monitor alerts for Azure virtual machine backups</span></span>
<span data-ttu-id="5e064-105">알림은 이벤트 임계값 도달 하거나 초과 되었는지는 hello 서비스의 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-105">Alerts are responses from hello service that an event threshold has been met or surpassed.</span></span> <span data-ttu-id="5e064-106">경우 문제가 시작 될 수 있습니다 중요 한 tookeeping 아래로 영업 비용을 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-106">Knowing when problems start can be critical tookeeping business costs down.</span></span> <span data-ttu-id="5e064-107">경고 일반적으로 일정에 따라 발생 하지 않습니다. 그리고 따라서 유용한 tooknow 최대한 빨리 후 경고가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-107">Alerts typically do not occur on a schedule, and so it is helpful tooknow as soon as possible after alerts occur.</span></span> <span data-ttu-id="5e064-108">예를 들어, 백업 또는 복원 작업이 실패 한 hello 실패 후 5 분 이내 경고 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-108">For example, when a backup or restore job fails, an alert occurs within five minutes of hello failure.</span></span> <span data-ttu-id="5e064-109">Hello 자격 증명 모음 대시보드 백업 경고 타일 hello 위험 및 경고 수준 이벤트를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-109">In hello vault dashboard, hello Backup Alerts tile displays Critical and Warning-level events.</span></span> <span data-ttu-id="5e064-110">Hello 백업 알림 설정에서 모든 이벤트를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-110">In hello Backup Alerts settings, you can view all events.</span></span> <span data-ttu-id="5e064-111">그러나 별개의 문제에 대해 작업하는 경우 경고가 발생하면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="5e064-111">But what do you do if an alert occurs when you are working on a separate issue?</span></span> <span data-ttu-id="5e064-112">Hello 경고가 발생할 때를 모르는 경우 부 불편 이거나 데이터를 손상 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-112">If you don't know when hello alert happens, it could be a minor inconvenience, or it could compromise data.</span></span> <span data-ttu-id="5e064-113">발생할 때 전자 메일을 통해 hello 서비스 toosend 경고 알림 구성 toomake 있는지 hello 올바른의 사람들이 가장 잘-경고를 인식 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-113">toomake sure hello correct people are aware of an alert - when it occurs, configure hello service toosend alert notifications via email.</span></span> <span data-ttu-id="5e064-114">전자 메일 알림 설정에 대한 자세한 내용은 [알림 구성](backup-azure-monitor-vms.md#configure-notifications)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5e064-114">For details on setting up email notifications, see [Configure notifications](backup-azure-monitor-vms.md#configure-notifications).</span></span>

## <a name="how-do-i-find-information-about-hello-alerts"></a><span data-ttu-id="5e064-115">Hello 경고에 대 한 정보를 찾으려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="5e064-115">How do I find information about hello alerts?</span></span>
<span data-ttu-id="5e064-116">tooview 정보 경고를 발생 시킨 hello 이벤트에 대 한 hello 백업 경고 블레이드 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-116">tooview information about hello event that threw an alert, you must open hello Backup Alerts blade.</span></span> <span data-ttu-id="5e064-117">두 가지 방법으로 tooopen hello 백업 경고 블레이드는: hello 경고 및 이벤트 블레이드 또는 hello 백업 경고 hello 자격 증명 모음 대시보드 타일에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-117">There are two ways tooopen hello Backup Alerts blade: either from hello Backup Alerts tile in hello vault dashboard, or from hello Alerts and Events blade.</span></span>

<span data-ttu-id="5e064-118">백업 경고에서 tooopen hello 백업 경고 블레이드 타일:</span><span class="sxs-lookup"><span data-stu-id="5e064-118">tooopen hello Backup Alerts blade from Backup Alerts tile:</span></span>

* <span data-ttu-id="5e064-119">Hello에 **백업 경고** hello 자격 증명 모음 대시보드에서 타일을 클릭 하 여 **위험** 또는 **경고** tooview hello에 대 한 해당 심각도 수준의 작업 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-119">On hello **Backup Alerts** tile on hello vault dashboard, click **Critical** or **Warning** tooview hello operational events for that severity level.</span></span>

    ![백업 경고 타일](./media/backup-azure-monitor-vms/backup-alerts-tile.png)

<span data-ttu-id="5e064-121">hello 백업 경고 블레이드를 tooopen hello 경고 및 이벤트 블레이드에서:</span><span class="sxs-lookup"><span data-stu-id="5e064-121">tooopen hello Backup Alerts blade from hello Alerts and Events blade:</span></span>

1. <span data-ttu-id="5e064-122">Hello 자격 증명 모음 대시보드에서 클릭 **모든 설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-122">From hello vault dashboard, click **All Settings**.</span></span> <span data-ttu-id="5e064-123">![모든 설정 단추](./media/backup-azure-monitor-vms/all-settings-button.png)</span><span class="sxs-lookup"><span data-stu-id="5e064-123">![All Settings button](./media/backup-azure-monitor-vms/all-settings-button.png)</span></span>
2. <span data-ttu-id="5e064-124">Hello에 **설정** 블레이드에서 클릭 **경고 및 이벤트**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-124">On hello **Settings** blade, click **Alerts and Events**.</span></span> <span data-ttu-id="5e064-125">![경고 및 이벤트 단추](./media/backup-azure-monitor-vms/alerts-and-events-button.png)</span><span class="sxs-lookup"><span data-stu-id="5e064-125">![Alerts and Events button](./media/backup-azure-monitor-vms/alerts-and-events-button.png)</span></span>
3. <span data-ttu-id="5e064-126">Hello에 **경고 및 이벤트** 블레이드에서 클릭 **백업 경고**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-126">On hello **Alerts and Events** blade, click **Backup Alerts**.</span></span> <span data-ttu-id="5e064-127">![백업 경고 단추](./media/backup-azure-monitor-vms/backup-alerts.png)</span><span class="sxs-lookup"><span data-stu-id="5e064-127">![Backup Alerts button](./media/backup-azure-monitor-vms/backup-alerts.png)</span></span>

    <span data-ttu-id="5e064-128">hello **백업 경고** 블레이드가 열리고 표시 hello 필터링 된 경고입니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-128">hello **Backup Alerts** blade opens and displays hello filtered alerts.</span></span>

    ![백업 경고 타일](./media/backup-azure-monitor-vms/backup-alerts-critical.png)
4. <span data-ttu-id="5e064-130">tooview 세부 정보 클릭 hello 경고 tooopen hello 이벤트 목록에서 특정 경고에 대 한 해당 **세부 정보** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-130">tooview detailed information about a particular alert, from hello list of events, click hello alert tooopen its **Details** blade.</span></span>

    ![이벤트 세부 정보](./media/backup-azure-monitor-vms/audit-logs-event-detail.png)

    <span data-ttu-id="5e064-132">hello 목록에 표시 된 toocustomize hello 특성 참조 [추가 이벤트 특성을 보려면](backup-azure-monitor-vms.md#view-additional-event-attributes)</span><span class="sxs-lookup"><span data-stu-id="5e064-132">toocustomize hello attributes displayed in hello list, see [View additional event attributes](backup-azure-monitor-vms.md#view-additional-event-attributes)</span></span>

## <a name="configure-notifications"></a><span data-ttu-id="5e064-133">알림 구성</span><span class="sxs-lookup"><span data-stu-id="5e064-133">Configure notifications</span></span>
 <span data-ttu-id="5e064-134">지난 시간, 또는 특정 유형의 이벤트가 발생할 때 hello에 따라 발생 한 hello 경고에 대 한 hello 서비스 toosend 전자 메일 알림을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-134">You can configure hello service toosend email notifications for hello alerts that occurred over hello past hour, or when particular types of events occur.</span></span>

<span data-ttu-id="5e064-135">경고에 대 한 전자 메일 알림 구성 함으로써 tooset</span><span class="sxs-lookup"><span data-stu-id="5e064-135">tooset up email notifications for alerts</span></span>

1. <span data-ttu-id="5e064-136">Hello 백업 경고 메뉴를 클릭 **알림 구성**</span><span class="sxs-lookup"><span data-stu-id="5e064-136">On hello Backup Alerts menu, click **Configure notifications**</span></span>

    ![백업 경고 메뉴](./media/backup-azure-monitor-vms/backup-alerts-menu.png)

    <span data-ttu-id="5e064-138">hello 구성 알림을 블레이드에서가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-138">hello Configure notifications blade opens.</span></span>

    ![알림 구성 블레이드](./media/backup-azure-monitor-vms/configure-notifications.png)
2. <span data-ttu-id="5e064-140">전자 메일 알림에 대 한 hello 구성 알림 블레이드에서 클릭 **에**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-140">On hello Configure notifications blade, for Email notifications, click **On**.</span></span>

    <span data-ttu-id="5e064-141">받는 사람에 게 hello 및 심각도 대화 상자 별모양 다음 toothem 해당 정보가 필요 하기 때문에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-141">hello Recipients and Severity dialogs have a star next toothem because that information is required.</span></span> <span data-ttu-id="5e064-142">최소 하나 이상의 전자 메일 주소를 제공하고 최소 하나 이상의 심각도를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-142">Provide at least one email address, and select at least one Severity.</span></span>
3. <span data-ttu-id="5e064-143">Hello에 **받는 사람 (전자 메일)** 대화 상자에서 hello 알림의 받을 사람에 대 한 hello 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-143">In hello **Recipients (Email)** dialog, type hello email addresses for who receive hello notifications.</span></span> <span data-ttu-id="5e064-144">형식을 사용 하 여 hello: username@domainname.com합니다. 세미콜론(;)을 사용하여 여러 전자 메일 주소를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-144">Use hello format: username@domainname.com. Separate multiple email addresses with a semicolon (;).</span></span>
4. <span data-ttu-id="5e064-145">Hello에 **알림** 영역에서 선택 **당 경고** 경고가 발생할 때 hello toosend 알림 지정 또는 **시간별 다이제스트** toosend hello 지난 시간에 대 한 요약입니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-145">In hello **Notify** area, choose **Per Alert** toosend notification when hello specified alert occurs, or **Hourly Digest** toosend a summary for hello past hour.</span></span>
5. <span data-ttu-id="5e064-146">Hello에 **심각도** 대화 상자에서 하나 이상의 수준 tootrigger 되도록 전자 메일 알림을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-146">In hello **Severity** dialog, choose one or more levels that you want tootrigger email notification.</span></span>
6. <span data-ttu-id="5e064-147">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-147">Click **Save**.</span></span>

   ### <a name="what-alert-types-are-available-for-azure-iaas-vm-backup"></a><span data-ttu-id="5e064-148">Azure IaaS VM 백업에 사용할 수 있는 경고 유형은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="5e064-148">What alert types are available for Azure IaaS VM backup?</span></span>
   | <span data-ttu-id="5e064-149">경고 수준</span><span class="sxs-lookup"><span data-stu-id="5e064-149">Alert Level</span></span> | <span data-ttu-id="5e064-150">전송되는 경고</span><span class="sxs-lookup"><span data-stu-id="5e064-150">Alerts sent</span></span> |
   | --- | --- |
   | <span data-ttu-id="5e064-151">중요</span><span class="sxs-lookup"><span data-stu-id="5e064-151">Critical</span></span> |<span data-ttu-id="5e064-152">백업 실패, 복구 실패</span><span class="sxs-lookup"><span data-stu-id="5e064-152">Backup failure, recovery failure</span></span> |
   | <span data-ttu-id="5e064-153">Warning</span><span class="sxs-lookup"><span data-stu-id="5e064-153">Warning</span></span> |<span data-ttu-id="5e064-154">없음</span><span class="sxs-lookup"><span data-stu-id="5e064-154">None</span></span> |
   | <span data-ttu-id="5e064-155">정보 제공</span><span class="sxs-lookup"><span data-stu-id="5e064-155">Informational</span></span> |<span data-ttu-id="5e064-156">없음</span><span class="sxs-lookup"><span data-stu-id="5e064-156">None</span></span> |

### <a name="are-there-situations-where-email-isnt-sent-even-if-notifications-are-configured"></a><span data-ttu-id="5e064-157">알림이 구성된 경우에도 전자 메일이 전송되지 않는 경우가 있습니까?</span><span class="sxs-lookup"><span data-stu-id="5e064-157">Are there situations where email isn't sent even if notifications are configured?</span></span>
<span data-ttu-id="5e064-158">Hello 알림이 올바르게 구성 된 경우에 경고가 전송 되지 않습니다, 하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-158">There are situations where an alert is not sent, even though hello notifications have been properly configured.</span></span> <span data-ttu-id="5e064-159">Hello에 다음과 같은 경우 전자 메일 알림이 tooavoid 경고 노이즈를 전송 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-159">In hello following situations email notifications are not sent tooavoid alert noise:</span></span>

* <span data-ttu-id="5e064-160">알림은 구성된 tooHourly 다이제스트 하 고 경고가 발생 되 고 hello 시간이 내의 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-160">If notifications are configured tooHourly Digest, and an alert is raised and resolved within hello hour.</span></span>
* <span data-ttu-id="5e064-161">hello 작업이 취소 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-161">hello job is canceled.</span></span>
* <span data-ttu-id="5e064-162">백업 작업이 트리거된 다음 실패하고 다른 백업 작업이 진행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-162">A backup job is triggered and then fails, and another backup job is in progress.</span></span>
* <span data-ttu-id="5e064-163">리소스 관리자 사용 VM에 대 한 예약된 된 백업 작업 시작 되지만 VM hello 더 이상 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-163">A scheduled backup job for a Resource Manager-enabled VM starts, but hello VM no longer exists.</span></span>

## <a name="customize-your-view-of-events"></a><span data-ttu-id="5e064-164">이벤트 보기 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="5e064-164">Customize your view of events</span></span>
<span data-ttu-id="5e064-165">hello **감사 로그** 필터 및 열 작업 이벤트 정보를 보여 주는 미리 정의 된 집합과 함께 설정을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-165">hello **Audit logs** setting comes with a pre-defined set of filters and columns showing operational event information.</span></span> <span data-ttu-id="5e064-166">Hello 보기를 사용자 지정할 수 있도록 때 hello **이벤트** 블레이드를 열고, 보여줍니다 hello 원하는 정보.</span><span class="sxs-lookup"><span data-stu-id="5e064-166">You can customize hello view so that when hello **Events** blade opens, it shows you hello information you want.</span></span>

1. <span data-ttu-id="5e064-167">Hello에 [자격 증명 모음 대시보드](backup-azure-manage-vms.md#open-a-recovery-services-vault-in-the-dashboard), 찾아보기 tooand 클릭 **감사 로그** tooopen hello **이벤트** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-167">In hello [vault dashboard](backup-azure-manage-vms.md#open-a-recovery-services-vault-in-the-dashboard), browse tooand click **Audit Logs** tooopen hello **Events** blade.</span></span>

    ![감사 로그](./media/backup-azure-monitor-vms/audit-logs-1606-1.png)

    <span data-ttu-id="5e064-169">hello **이벤트** 블레이드 hello 현재 자격 증명 모음에 대 한 필터링 toohello 작동 관련 이벤트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-169">hello **Events** blade opens toohello operational events filtered just for hello current vault.</span></span>

    ![감사 로그 필터](./media/backup-azure-monitor-vms/audit-logs-filter.png)

    <span data-ttu-id="5e064-171">hello 블레이드 hello 목록으로 표시 중요, 오류, 경고 및 정보 제공 이벤트를 발생 한 hello 지난 주의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-171">hello blade shows hello list of Critical, Error, Warning, and Informational events that occurred in hello past week.</span></span> <span data-ttu-id="5e064-172">hello 시간 범위는 hello에 설정 된 기본 값 **필터**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-172">hello time span is a default value set in hello **Filter**.</span></span> <span data-ttu-id="5e064-173">hello **이벤트** 블레이드 또한 hello 이벤트 발생 했을 때 추적 가로 막대형 차트를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-173">hello **Events** blade also shows a bar chart tracking when hello events occurred.</span></span> <span data-ttu-id="5e064-174">Hello에 toosee hello 가로 막대형 차트를 표시 하지 않으려는 경우 **이벤트** 메뉴를 클릭 **숨기기 차트** tootoggle hello 차트 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-174">If you don't want toosee hello bar chart, in hello **Events** menu, click **Hide chart** tootoggle off hello chart.</span></span> <span data-ttu-id="5e064-175">이벤트의 hello 기본 보기에는 작업, 수준, 상태, 리소스 및 시간 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-175">hello default view of Events shows Operation, Level, Status, Resource, and Time information.</span></span> <span data-ttu-id="5e064-176">추가 이벤트 속성을 노출 하는 방법에 대 한 내용은 hello 섹션을 참조 하십시오. [이벤트 정보를 확장](backup-azure-monitor-vms.md#view-additional-event-attributes)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-176">For information about exposing additional Event attributes, see hello section [expanding Event information](backup-azure-monitor-vms.md#view-additional-event-attributes).</span></span>
2. <span data-ttu-id="5e064-177">Operational 이벤트, hello에 대 한 자세한 내용은 **작업** 열에서 작업 이벤트 tooopen 해당 블레이드를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-177">For additional information on an operational event, in hello **Operation** column, click an operational event tooopen its blade.</span></span> <span data-ttu-id="5e064-178">hello 블레이드 hello 이벤트에 대 한 자세한 정보가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-178">hello blade contains detailed information about hello events.</span></span> <span data-ttu-id="5e064-179">이벤트는 hello 시간 범위에서 발생 하는 hello 이벤트의 목록과 해당 상관 관계 ID로 그룹화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-179">Events are grouped by their correlation ID and a list of hello events that occurred in hello Time span.</span></span>

    ![작업 세부 정보](./media/backup-azure-monitor-vms/audit-logs-details-window.png)
3. <span data-ttu-id="5e064-181">tooview 세부 정보 클릭 hello 이벤트 tooopen hello 이벤트 목록에서 특정 이벤트에 대 한 해당 **세부 정보** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-181">tooview detailed information about a particular event, from hello list of events, click hello event tooopen its **Details** blade.</span></span>

    ![이벤트 세부 정보](./media/backup-azure-monitor-vms/audit-logs-details-window-deep.png)

    <span data-ttu-id="5e064-183">hello 이벤트 수준 정보는 자세한 hello 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-183">hello Event-level information is as detailed as hello information gets.</span></span> <span data-ttu-id="5e064-184">각 이벤트에 대 한이 많은 정보를 보려면 고 tooadd 있을 것이 훨씬에 대해 자세히 설명 toohello **이벤트** 블레이드에서 hello 섹션을 참조 [이벤트 정보를 확장](backup-azure-monitor-vms.md#view-additional-event-attributes)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-184">If you prefer seeing this much information about each event, and would like tooadd this much detail toohello **Events** blade, see hello section [expanding Event information](backup-azure-monitor-vms.md#view-additional-event-attributes).</span></span>

## <a name="customize-hello-event-filter"></a><span data-ttu-id="5e064-185">Hello 이벤트 필터를 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="5e064-185">Customize hello event filter</span></span>
<span data-ttu-id="5e064-186">사용 하 여 hello **필터** tooadjust 하거나 특정 블레이드에 표시 되는 hello 정보를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-186">Use hello **Filter** tooadjust or choose hello information that appears in a particular blade.</span></span> <span data-ttu-id="5e064-187">toofilter hello 이벤트 정보:</span><span class="sxs-lookup"><span data-stu-id="5e064-187">toofilter hello event information:</span></span>

1. <span data-ttu-id="5e064-188">Hello에 [자격 증명 모음 대시보드](backup-azure-manage-vms.md#open-a-recovery-services-vault-in-the-dashboard), 찾아보기 tooand 클릭 **감사 로그** tooopen hello **이벤트** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-188">In hello [vault dashboard](backup-azure-manage-vms.md#open-a-recovery-services-vault-in-the-dashboard), browse tooand click **Audit Logs** tooopen hello **Events** blade.</span></span>

    ![감사 로그](./media/backup-azure-monitor-vms/audit-logs-1606-1.png)

    <span data-ttu-id="5e064-190">hello **이벤트** 블레이드 hello 현재 자격 증명 모음에 대 한 필터링 toohello 작동 관련 이벤트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-190">hello **Events** blade opens toohello operational events filtered just for hello current vault.</span></span>

    ![감사 로그 필터](./media/backup-azure-monitor-vms/audit-logs-filter.png)
2. <span data-ttu-id="5e064-192">Hello에 **이벤트** 메뉴를 클릭 하 여 **필터** tooopen 해당 블레이드에 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-192">On hello **Events** menu, click **Filter** tooopen that blade.</span></span>

    ![필터 블레이드 열기](./media/backup-azure-monitor-vms/audit-logs-filter-button.png)
3. <span data-ttu-id="5e064-194">Hello에 **필터** 블레이드에서 hello 조정 **수준**, **시간 범위**, 및 **호출자** 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-194">On hello **Filter** blade, adjust hello **Level**, **Time span**, and **Caller** filters.</span></span> <span data-ttu-id="5e064-195">hello 다른 필터 사용할 수 없는 이후 hello 복구 서비스 자격 증명 모음에 대 한 tooprovide hello에 대 한 현재 정보를 설정 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-195">hello other filters are not available since they were set tooprovide hello current information for hello Recovery Services vault.</span></span>

    ![감사 로그 쿼리 세부 정보](./media/backup-azure-monitor-vms/filter-blade.png)

    <span data-ttu-id="5e064-197">Hello를 지정할 수 있습니다 **수준** 이벤트의: 중요, 오류, 경고 또는 정보 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-197">You can specify hello **Level** of event: Critical, Error, Warning, or Informational.</span></span> <span data-ttu-id="5e064-198">이벤트 수준의 조합을 선택할 수 있지만 하나 이상의 수준을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-198">You can choose any combination of event Levels, but you must have at least one Level selected.</span></span> <span data-ttu-id="5e064-199">Hello 수준을 켜거나 끕니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-199">Toggle hello Level on or off.</span></span> <span data-ttu-id="5e064-200">hello **시간 범위** 필터 이벤트 캡처를 위한 시간의 toospecify hello 길이 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-200">hello **Time span** filter allows you toospecify hello length of time for capturing events.</span></span> <span data-ttu-id="5e064-201">사용자 지정 시간 범위를 사용 하는 경우 hello 시작을 설정할 수 있으며 종료 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-201">If you use a custom Time span, you can set hello start and end times.</span></span>
4. <span data-ttu-id="5e064-202">필터를 사용 하 여 준비 tooquery hello 작업 로그의 후 클릭 **업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-202">Once you are ready tooquery hello operations logs using your filter, click **Update**.</span></span> <span data-ttu-id="5e064-203">hello 결과 hello에 있는 표시 **이벤트** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-203">hello results display in hello **Events** blade.</span></span>

    ![작업 세부 정보](./media/backup-azure-monitor-vms/edited-list-of-events.png)

### <a name="view-additional-event-attributes"></a><span data-ttu-id="5e064-205">추가 이벤트 특성 보기</span><span class="sxs-lookup"><span data-stu-id="5e064-205">View additional event attributes</span></span>
<span data-ttu-id="5e064-206">Hello를 사용 하 여 **열** 단추를 추가 이벤트 특성 tooappear hello hello 목록에서 사용 하도록 설정할 수 **이벤트** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-206">Using hello **Columns** button, you can enable additional event attributes tooappear in hello list on hello **Events** blade.</span></span> <span data-ttu-id="5e064-207">이벤트의 hello 기본 목록에는 작업, 수준, 상태, 리소스 및 시간에 대 한 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-207">hello default list of events displays information for Operation, Level, Status, Resource, and Time.</span></span> <span data-ttu-id="5e064-208">tooenable 추가 속성:</span><span class="sxs-lookup"><span data-stu-id="5e064-208">tooenable additional attributes:</span></span>

1. <span data-ttu-id="5e064-209">Hello에 **이벤트** 블레이드에서 클릭 **열**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-209">On hello **Events** blade, click **Columns**.</span></span>

    ![열 열기](./media/backup-azure-monitor-vms/audi-logs-column-button.png)

    <span data-ttu-id="5e064-211">hello **열 선택** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-211">hello **Choose columns** blade opens.</span></span>

    ![열 블레이드](./media/backup-azure-monitor-vms/columns-blade.png)
2. <span data-ttu-id="5e064-213">tooselect hello 특성을 hello 확인란을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-213">tooselect hello attribute, click hello checkbox.</span></span> <span data-ttu-id="5e064-214">hello 특성 확인란을 설정 및 해제를 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-214">hello attribute checkbox toggles on and off.</span></span>
3. <span data-ttu-id="5e064-215">클릭 **재설정** tooreset hello hello에 특성 목록을 **이벤트** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-215">Click **Reset** tooreset hello list of attributes in hello **Events** blade.</span></span> <span data-ttu-id="5e064-216">추가 하거나 또는 hello 목록에서 특성 제거를 사용 하 여 **재설정** tooview hello 이벤트 특성의 새 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-216">After adding or removing attributes from hello list, use **Reset** tooview hello new list of Event attributes.</span></span>
4. <span data-ttu-id="5e064-217">클릭 **업데이트** hello 이벤트 특성의 tooupdate hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-217">Click **Update** tooupdate hello data in hello Event attributes.</span></span> <span data-ttu-id="5e064-218">다음 표에서 hello 각 특성에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-218">hello following table provides information about each attribute.</span></span>

| <span data-ttu-id="5e064-219">열 이름</span><span class="sxs-lookup"><span data-stu-id="5e064-219">Column name</span></span> | <span data-ttu-id="5e064-220">설명</span><span class="sxs-lookup"><span data-stu-id="5e064-220">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5e064-221">작업</span><span class="sxs-lookup"><span data-stu-id="5e064-221">Operation</span></span> |<span data-ttu-id="5e064-222">hello 작업의 hello 이름</span><span class="sxs-lookup"><span data-stu-id="5e064-222">hello name of hello operation</span></span> |
| <span data-ttu-id="5e064-223">Level</span><span class="sxs-lookup"><span data-stu-id="5e064-223">Level</span></span> |<span data-ttu-id="5e064-224">수준 hello hello 작업의 값이 될 수 있습니다: 정보, 경고, 오류 또는 위험</span><span class="sxs-lookup"><span data-stu-id="5e064-224">hello level of hello operation, values can be: Informational, Warning, Error, or Critical</span></span> |
| <span data-ttu-id="5e064-225">가동 상태</span><span class="sxs-lookup"><span data-stu-id="5e064-225">Status</span></span> |<span data-ttu-id="5e064-226">Hello 작업의 설명이 포함 된 상태</span><span class="sxs-lookup"><span data-stu-id="5e064-226">Descriptive state of hello operation</span></span> |
| <span data-ttu-id="5e064-227">리소스</span><span class="sxs-lookup"><span data-stu-id="5e064-227">Resource</span></span> |<span data-ttu-id="5e064-228">Hello 리소스를 식별 하는 URL 라고도 hello 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-228">URL that identifies hello resource; also known as hello resource ID</span></span> |
| <span data-ttu-id="5e064-229">Time</span><span class="sxs-lookup"><span data-stu-id="5e064-229">Time</span></span> |<span data-ttu-id="5e064-230">시간에서에서 측정 한 hello hello 이벤트가 발생 한 경우 현재 시간</span><span class="sxs-lookup"><span data-stu-id="5e064-230">Time, measured from hello current time, when hello event occurred</span></span> |
| <span data-ttu-id="5e064-231">Caller</span><span class="sxs-lookup"><span data-stu-id="5e064-231">Caller</span></span> |<span data-ttu-id="5e064-232">참여 율이 또는; hello 이벤트를 트리거한 또는 호출 hello 시스템 또는 사용자 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-232">Who or what called or triggered hello event; can be hello system, or a user</span></span> |
| <span data-ttu-id="5e064-233">Timestamp</span><span class="sxs-lookup"><span data-stu-id="5e064-233">Timestamp</span></span> |<span data-ttu-id="5e064-234">hello 이벤트가 트리거된 경우 hello 시간</span><span class="sxs-lookup"><span data-stu-id="5e064-234">hello time when hello event was triggered</span></span> |
| <span data-ttu-id="5e064-235">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="5e064-235">Resource Group</span></span> |<span data-ttu-id="5e064-236">hello 관련된 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="5e064-236">hello associated resource group</span></span> |
| <span data-ttu-id="5e064-237">리소스 종류</span><span class="sxs-lookup"><span data-stu-id="5e064-237">Resource Type</span></span> |<span data-ttu-id="5e064-238">리소스 관리자에서 사용 하는 hello 내부 리소스 종류</span><span class="sxs-lookup"><span data-stu-id="5e064-238">hello internal resource type used by Resource Manager</span></span> |
| <span data-ttu-id="5e064-239">구독 ID</span><span class="sxs-lookup"><span data-stu-id="5e064-239">Subscription ID</span></span> |<span data-ttu-id="5e064-240">hello 연결 된 구독 ID</span><span class="sxs-lookup"><span data-stu-id="5e064-240">hello associated subscription ID</span></span> |
| <span data-ttu-id="5e064-241">Category</span><span class="sxs-lookup"><span data-stu-id="5e064-241">Category</span></span> |<span data-ttu-id="5e064-242">Hello 이벤트 범주</span><span class="sxs-lookup"><span data-stu-id="5e064-242">Category of hello event</span></span> |
| <span data-ttu-id="5e064-243">상관관계 ID</span><span class="sxs-lookup"><span data-stu-id="5e064-243">Correlation ID</span></span> |<span data-ttu-id="5e064-244">관련된 이벤트에 대한 일반적인 ID</span><span class="sxs-lookup"><span data-stu-id="5e064-244">Common ID for related events</span></span> |

## <a name="use-powershell-toocustomize-alerts"></a><span data-ttu-id="5e064-245">PowerShell toocustomize 경고를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="5e064-245">Use PowerShell toocustomize alerts</span></span>
<span data-ttu-id="5e064-246">Hello 작업에 대 한 사용자 지정 경고 알림을 hello 포털에서 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-246">You can get custom alert notifications for hello jobs in hello portal.</span></span> <span data-ttu-id="5e064-247">이러한 작업을 tooget operational hello에 대 한 규칙 이벤트를 기록 하는 PowerShell 기반 경고를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-247">tooget these jobs, define PowerShell-based alert rules on hello operational logs events.</span></span> <span data-ttu-id="5e064-248">*Azure PowerShell 버전 1.3.0 이상*을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-248">Use *PowerShell version 1.3.0 or later*.</span></span>

<span data-ttu-id="5e064-249">백업 실패에 대 한 사용자 지정 알림 tooalert toodefine 다음 스크립트는 hello 같은 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-249">toodefine a custom notification tooalert for backup failures, use a command like hello following script:</span></span>

```
PS C:\> $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail contoso@microsoft.com
PS C:\> Add-AzureRmLogAlertRule -Name backupFailedAlert -Location "East US" -ResourceGroup RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US -OperationName Microsoft.RecoveryServices/recoveryServicesVault/Backup -Status Failed -TargetResourceId /subscriptions/86eeac34-eth9a-4de3-84db-7a27d121967e/resourceGroups/RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US/providers/Microsoft.RecoveryServices/vaults/trinadhVault -Actions $actionEmail
```

<span data-ttu-id="5e064-250">**ResourceId** : 감사 로그 hello에서 ResourceId를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-250">**ResourceId** : You can get ResourceId from hello Audit logs.</span></span> <span data-ttu-id="5e064-251">hello ResourceId은 hello 작업 로그의 hello 리소스 열에서 제공 되는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-251">hello ResourceId is a URL provided in hello Resource column of hello Operation logs.</span></span>

<span data-ttu-id="5e064-252">**OperationName** : OperationName hello 형식입니다 "Microsoft.RecoveryServices/recoveryServicesVault/*EventName*" 여기서 *EventName* 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-252">**OperationName** : OperationName is in hello format "Microsoft.RecoveryServices/recoveryServicesVault/*EventName*" where *EventName* can be:</span></span><br/>

* <span data-ttu-id="5e064-253">등록</span><span class="sxs-lookup"><span data-stu-id="5e064-253">Register</span></span> <br/>
* <span data-ttu-id="5e064-254">등록 취소 </span><span class="sxs-lookup"><span data-stu-id="5e064-254">Unregister</span></span> <br/>
* <span data-ttu-id="5e064-255">ConfigureProtection </span><span class="sxs-lookup"><span data-stu-id="5e064-255">ConfigureProtection</span></span> <br/>
* <span data-ttu-id="5e064-256">백업 </span><span class="sxs-lookup"><span data-stu-id="5e064-256">Backup</span></span> <br/>
* <span data-ttu-id="5e064-257">복원 </span><span class="sxs-lookup"><span data-stu-id="5e064-257">Restore</span></span> <br/>
* <span data-ttu-id="5e064-258">StopProtection </span><span class="sxs-lookup"><span data-stu-id="5e064-258">StopProtection</span></span> <br/>
* <span data-ttu-id="5e064-259">DeleteBackupData </span><span class="sxs-lookup"><span data-stu-id="5e064-259">DeleteBackupData</span></span> <br/>
* <span data-ttu-id="5e064-260">CreateProtectionPolicy </span><span class="sxs-lookup"><span data-stu-id="5e064-260">CreateProtectionPolicy</span></span> <br/>
* <span data-ttu-id="5e064-261">DeleteProtectionPolicy </span><span class="sxs-lookup"><span data-stu-id="5e064-261">DeleteProtectionPolicy</span></span> <br/>
* <span data-ttu-id="5e064-262">UpdateProtectionPolicy </span><span class="sxs-lookup"><span data-stu-id="5e064-262">UpdateProtectionPolicy</span></span> <br/>

<span data-ttu-id="5e064-263">**상태** : 지원되는 값은 시작함, 성공함 또는 실패함입니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-263">**Status** : Supported values are Started, Succeeded, or Failed.</span></span>

<span data-ttu-id="5e064-264">**ResourceGroup** : hello toowhich hello 리소스 속한 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-264">**ResourceGroup** : This is hello Resource Group toowhich hello resource belongs.</span></span> <span data-ttu-id="5e064-265">Hello 리소스 그룹 열 toohello 생성 된 로그를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-265">You can add hello Resource Group column toohello generated logs.</span></span> <span data-ttu-id="5e064-266">리소스 그룹에는 이벤트 정보의 hello 사용 가능한 형식 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-266">Resource Group is one of hello available types of event information.</span></span>

<span data-ttu-id="5e064-267">**이름** : hello 경고 규칙의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-267">**Name** : Name of hello Alert Rule.</span></span>

<span data-ttu-id="5e064-268">**CustomEmail** : hello 사용자 지정 전자 메일 주소 toowhich toosend 경고 알림을 원하는 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-268">**CustomEmail** : Specify hello custom email address toowhich you want toosend an alert notification</span></span>

<span data-ttu-id="5e064-269">**SendToServiceOwners** :이 옵션 경고 알림 tooall 관리자와 hello 구독의 공동 관리자를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-269">**SendToServiceOwners** : This option sends alert notifications tooall administrators and co-administrators of hello subscription.</span></span> <span data-ttu-id="5e064-270">**New-AzureRmAlertRuleEmail** cmdlet에 사용될 수 있음</span><span class="sxs-lookup"><span data-stu-id="5e064-270">It can be used in **New-AzureRmAlertRuleEmail** cmdlet</span></span>

### <a name="limitations-on-alerts"></a><span data-ttu-id="5e064-271">경고에 대한 제한</span><span class="sxs-lookup"><span data-stu-id="5e064-271">Limitations on Alerts</span></span>
<span data-ttu-id="5e064-272">이벤트 기반 경고는 다음과 같은 제한을 주체 toohello:</span><span class="sxs-lookup"><span data-stu-id="5e064-272">Event-based alerts are subject toohello following limitations:</span></span>

1. <span data-ttu-id="5e064-273">복구 서비스 자격 증명 모음에 hello에서 모든 가상 컴퓨터에 경고가 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-273">Alerts are triggered on all virtual machines in hello Recovery Services vault.</span></span> <span data-ttu-id="5e064-274">복구 서비스 자격 증명 모음에서 가상 컴퓨터의 하위 집합에 대 한 hello 경고를 사용자 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-274">You cannot customize hello alert for a subset of virtual machines in a Recovery Services vault.</span></span>
2. <span data-ttu-id="5e064-275">이 기능은 미리 보기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-275">This feature is in Preview.</span></span> [<span data-ttu-id="5e064-276">자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="5e064-276">Learn more</span></span>](../monitoring-and-diagnostics/insights-powershell-samples.md#create-metric-alerts)
3. <span data-ttu-id="5e064-277">"alerts-noreply@mail.windowsazure.com"에서 경고를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-277">Alerts are sent from "alerts-noreply@mail.windowsazure.com".</span></span> <span data-ttu-id="5e064-278">현재 hello 전자 메일 보낸 사람을 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-278">Currently you can't modify hello email sender.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e064-279">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5e064-279">Next steps</span></span>
<span data-ttu-id="5e064-280">이벤트 로그 훌륭한 사후를 사용 하도록 설정 하 고 hello 백업 작업에 대 한 지원을 감사 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-280">Event logs enable great post-mortem and audit support for hello backup operations.</span></span> <span data-ttu-id="5e064-281">작업을 수행 하는 hello 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-281">hello following operations are logged:</span></span>

* <span data-ttu-id="5e064-282">등록</span><span class="sxs-lookup"><span data-stu-id="5e064-282">Register</span></span>
* <span data-ttu-id="5e064-283">등록 취소</span><span class="sxs-lookup"><span data-stu-id="5e064-283">Unregister</span></span>
* <span data-ttu-id="5e064-284">보호 구성</span><span class="sxs-lookup"><span data-stu-id="5e064-284">Configure protection</span></span>
* <span data-ttu-id="5e064-285">백업(예약된 백업 및 주문형 백업 모두)</span><span class="sxs-lookup"><span data-stu-id="5e064-285">Backup (Both scheduled as well as on-demand backup)</span></span>
* <span data-ttu-id="5e064-286">복원</span><span class="sxs-lookup"><span data-stu-id="5e064-286">Restore</span></span>
* <span data-ttu-id="5e064-287">보호 중지</span><span class="sxs-lookup"><span data-stu-id="5e064-287">Stop protection</span></span>
* <span data-ttu-id="5e064-288">백업 데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="5e064-288">Delete backup data</span></span>
* <span data-ttu-id="5e064-289">정책 추가</span><span class="sxs-lookup"><span data-stu-id="5e064-289">Add policy</span></span>
* <span data-ttu-id="5e064-290">정책 삭제</span><span class="sxs-lookup"><span data-stu-id="5e064-290">Delete policy</span></span>
* <span data-ttu-id="5e064-291">정책 업데이트</span><span class="sxs-lookup"><span data-stu-id="5e064-291">Update policy</span></span>
* <span data-ttu-id="5e064-292">작업 취소</span><span class="sxs-lookup"><span data-stu-id="5e064-292">Cancel job</span></span>

<span data-ttu-id="5e064-293">이벤트, 작업 및 hello에서 감사 로그에 대 한 광범위 한 설명은 Azure 서비스 hello 문서 참조 [ग द ृ 및 감사 로그](../monitoring-and-diagnostics/insights-debugging-with-events.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-293">For a broad explanation of events, operations, and audit logs across hello Azure services, see hello article, [View events and audit logs](../monitoring-and-diagnostics/insights-debugging-with-events.md).</span></span>

<span data-ttu-id="5e064-294">복구 지점에서 가상 컴퓨터를 다시 만드는 방법에 대한 내용은 [Azure VM 복원](backup-azure-restore-vms.md)을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="5e064-294">For information on re-creating a virtual machine from a recovery point, check out [Restore Azure VMs](backup-azure-restore-vms.md).</span></span> <span data-ttu-id="5e064-295">가상 컴퓨터 보호에 대 한 정보를 보려면 참고 [소개: Vm tooa 복구 서비스 자격 증명 모음에 백업](backup-azure-vms-first-look-arm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-295">If you need information on protecting your virtual machines, see [First look: Back up VMs tooa Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span> <span data-ttu-id="5e064-296">VM 백업 hello 문서에 대 한 hello 관리 작업에 대 한 자세한 내용은 [관리 Azure 가상 컴퓨터 백업을](backup-azure-manage-vms.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e064-296">Learn about hello management tasks for VM backups in hello article, [Manage Azure virtual machine backups](backup-azure-manage-vms.md).</span></span>
