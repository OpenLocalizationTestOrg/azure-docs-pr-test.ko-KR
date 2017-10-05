---
title: "Resource Manager로 배포된 가상 컴퓨터 백업 모니터링 | Microsoft Docs"
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
ms.openlocfilehash: b9dc3f52e5fc275bc56b9964f2115833f2dde42e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-alerts-for-azure-virtual-machine-backups"></a><span data-ttu-id="6d395-104">Azure 가상 컴퓨터 백업에 대한 경고 모니터링</span><span class="sxs-lookup"><span data-stu-id="6d395-104">Monitor alerts for Azure virtual machine backups</span></span>
<span data-ttu-id="6d395-105">경고는 이벤트 임계값을 만족하거나 초과한 서비스에서 나오는 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-105">Alerts are responses from the service that an event threshold has been met or surpassed.</span></span> <span data-ttu-id="6d395-106">문제가 시작되는 시기를 아는 것은 비즈니스 비용을 낮게 유지하는 데 중요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-106">Knowing when problems start can be critical to keeping business costs down.</span></span> <span data-ttu-id="6d395-107">일반적으로 경고는 일정에 따라 발생하지 않으므로 경고가 발생한 후 가능한 빨리 아는 것이 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-107">Alerts typically do not occur on a schedule, and so it is helpful to know as soon as possible after alerts occur.</span></span> <span data-ttu-id="6d395-108">예를 들어 백업 또는 복원 작업이 실패할 경우 실패의 5분 내에서 경고가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-108">For example, when a backup or restore job fails, an alert occurs within five minutes of the failure.</span></span> <span data-ttu-id="6d395-109">자격 증명 모음 대시보드의 백업 경고 타일에 중요 및 경고 수준 이벤트를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-109">In the vault dashboard, the Backup Alerts tile displays Critical and Warning-level events.</span></span> <span data-ttu-id="6d395-110">백업 경고 설정에서 모든 이벤트를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-110">In the Backup Alerts settings, you can view all events.</span></span> <span data-ttu-id="6d395-111">그러나 별개의 문제에 대해 작업하는 경우 경고가 발생하면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="6d395-111">But what do you do if an alert occurs when you are working on a separate issue?</span></span> <span data-ttu-id="6d395-112">경고가 발생하는 시기를 모르면 조금 불편할 수도 있고 데이터를 손상시킬 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-112">If you don't know when the alert happens, it could be a minor inconvenience, or it could compromise data.</span></span> <span data-ttu-id="6d395-113">정확한 담당자가 경고를 인식하게 하려면 경고가 발생할 때 전자 메일을 통해 경고 알림을 보내도록 서비스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-113">To make sure the correct people are aware of an alert - when it occurs, configure the service to send alert notifications via email.</span></span> <span data-ttu-id="6d395-114">전자 메일 알림 설정에 대한 자세한 내용은 [알림 구성](backup-azure-monitor-vms.md#configure-notifications)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d395-114">For details on setting up email notifications, see [Configure notifications](backup-azure-monitor-vms.md#configure-notifications).</span></span>

## <a name="how-do-i-find-information-about-the-alerts"></a><span data-ttu-id="6d395-115">경고에 대한 정보를 찾으려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="6d395-115">How do I find information about the alerts?</span></span>
<span data-ttu-id="6d395-116">경고를 발생시킨 이벤트에 관한 정보를 보려면 백업 경고 블레이드를 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-116">To view information about the event that threw an alert, you must open the Backup Alerts blade.</span></span> <span data-ttu-id="6d395-117">두 가지 방법으로: 즉, 자격 증명 모음 대시보드의 백업 경고 타일에서 또는 경고 및 이벤트 블레이드에서 백업 경고 블레이드를 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-117">There are two ways to open the Backup Alerts blade: either from the Backup Alerts tile in the vault dashboard, or from the Alerts and Events blade.</span></span>

<span data-ttu-id="6d395-118">백업 경고 타일에서 백업 경고 블레이드를 열려면:</span><span class="sxs-lookup"><span data-stu-id="6d395-118">To open the Backup Alerts blade from Backup Alerts tile:</span></span>

* <span data-ttu-id="6d395-119">자격 증명 모음 대시보드의 **백업 경고** 타일에서 **중요** 또는 **경고**를 클릭하여 해당 심각도 수준에서 작동할 수 있는 이벤트를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-119">On the **Backup Alerts** tile on the vault dashboard, click **Critical** or **Warning** to view the operational events for that severity level.</span></span>

    ![백업 경고 타일](./media/backup-azure-monitor-vms/backup-alerts-tile.png)

<span data-ttu-id="6d395-121">경고 및 이벤트 블레이드에서 백업 경고 블레이드를 열려면:</span><span class="sxs-lookup"><span data-stu-id="6d395-121">To open the Backup Alerts blade from the Alerts and Events blade:</span></span>

1. <span data-ttu-id="6d395-122">자격 증명 모음 대시보드에서 **모든 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-122">From the vault dashboard, click **All Settings**.</span></span> <span data-ttu-id="6d395-123">![모든 설정 단추](./media/backup-azure-monitor-vms/all-settings-button.png)</span><span class="sxs-lookup"><span data-stu-id="6d395-123">![All Settings button](./media/backup-azure-monitor-vms/all-settings-button.png)</span></span>
2. <span data-ttu-id="6d395-124">**설정** 블레이드에서 **경고 및 이벤트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-124">On the **Settings** blade, click **Alerts and Events**.</span></span> <span data-ttu-id="6d395-125">![경고 및 이벤트 단추](./media/backup-azure-monitor-vms/alerts-and-events-button.png)</span><span class="sxs-lookup"><span data-stu-id="6d395-125">![Alerts and Events button](./media/backup-azure-monitor-vms/alerts-and-events-button.png)</span></span>
3. <span data-ttu-id="6d395-126">**경고 및 이벤트** 블레이드에서 **백업 경고**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-126">On the **Alerts and Events** blade, click **Backup Alerts**.</span></span> <span data-ttu-id="6d395-127">![백업 경고 단추](./media/backup-azure-monitor-vms/backup-alerts.png)</span><span class="sxs-lookup"><span data-stu-id="6d395-127">![Backup Alerts button](./media/backup-azure-monitor-vms/backup-alerts.png)</span></span>

    <span data-ttu-id="6d395-128">**백업 경고** 블레이드가 열리고 필터링된 경고가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-128">The **Backup Alerts** blade opens and displays the filtered alerts.</span></span>

    ![백업 경고 타일](./media/backup-azure-monitor-vms/backup-alerts-critical.png)
4. <span data-ttu-id="6d395-130">특정 경고에 관한 세부 정보를 보려면 이벤트 목록에서 경고를 클릭하여 해당 **세부 정보** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-130">To view detailed information about a particular alert, from the list of events, click the alert to open its **Details** blade.</span></span>

    ![이벤트 세부 정보](./media/backup-azure-monitor-vms/audit-logs-event-detail.png)

    <span data-ttu-id="6d395-132">목록에 표시된 특성을 사용자 지정하려면 [추가 이벤트 특성 보기](backup-azure-monitor-vms.md#view-additional-event-attributes)</span><span class="sxs-lookup"><span data-stu-id="6d395-132">To customize the attributes displayed in the list, see [View additional event attributes](backup-azure-monitor-vms.md#view-additional-event-attributes)</span></span>

## <a name="configure-notifications"></a><span data-ttu-id="6d395-133">알림 구성</span><span class="sxs-lookup"><span data-stu-id="6d395-133">Configure notifications</span></span>
 <span data-ttu-id="6d395-134">지난 한 시간 동안 발생한 경고에 대해 또는 특정 유형의 이벤트가 발생할 때 전자 메일 알림을 보내도록 서비스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-134">You can configure the service to send email notifications for the alerts that occurred over the past hour, or when particular types of events occur.</span></span>

<span data-ttu-id="6d395-135">경고에 대한 전자 메일 알림을 설정하려면</span><span class="sxs-lookup"><span data-stu-id="6d395-135">To set up email notifications for alerts</span></span>

1. <span data-ttu-id="6d395-136">백업 경고 메뉴에서 **알림 구성**</span><span class="sxs-lookup"><span data-stu-id="6d395-136">On the Backup Alerts menu, click **Configure notifications**</span></span>

    ![백업 경고 메뉴](./media/backup-azure-monitor-vms/backup-alerts-menu.png)

    <span data-ttu-id="6d395-138">알림 구성 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-138">The Configure notifications blade opens.</span></span>

    ![알림 구성 블레이드](./media/backup-azure-monitor-vms/configure-notifications.png)
2. <span data-ttu-id="6d395-140">알림 구성 블레이드에서 전자 메일 알림에 대해 **켜기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-140">On the Configure notifications blade, for Email notifications, click **On**.</span></span>

    <span data-ttu-id="6d395-141">받는 사람 및 심각도 대화 상자에는 해당 정보가 필수이기 때문에 별표가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-141">The Recipients and Severity dialogs have a star next to them because that information is required.</span></span> <span data-ttu-id="6d395-142">최소 하나 이상의 전자 메일 주소를 제공하고 최소 하나 이상의 심각도를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-142">Provide at least one email address, and select at least one Severity.</span></span>
3. <span data-ttu-id="6d395-143">**받는 사람(전자 메일)** 대화 상자에 알림을 받을 전자 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-143">In the **Recipients (Email)** dialog, type the email addresses for who receive the notifications.</span></span> <span data-ttu-id="6d395-144">사용할 형식: username@domainname.com. 세미콜론(;)을 사용하여 여러 전자 메일 주소를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-144">Use the format: username@domainname.com. Separate multiple email addresses with a semicolon (;).</span></span>
4. <span data-ttu-id="6d395-145">**알림** 영역에서 **경고별**을 선택하여 지정된 경고가 발생하면 알림을 보내거나 **시간별 요약**을 선택하여 지난 한 시간 동안의 요약을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-145">In the **Notify** area, choose **Per Alert** to send notification when the specified alert occurs, or **Hourly Digest** to send a summary for the past hour.</span></span>
5. <span data-ttu-id="6d395-146">**심각도** 대화 상자에서 전자 메일 알림을 트리거할 수준을 하나 이상 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-146">In the **Severity** dialog, choose one or more levels that you want to trigger email notification.</span></span>
6. <span data-ttu-id="6d395-147">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-147">Click **Save**.</span></span>

   ### <a name="what-alert-types-are-available-for-azure-iaas-vm-backup"></a><span data-ttu-id="6d395-148">Azure IaaS VM 백업에 사용할 수 있는 경고 유형은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="6d395-148">What alert types are available for Azure IaaS VM backup?</span></span>
   | <span data-ttu-id="6d395-149">경고 수준</span><span class="sxs-lookup"><span data-stu-id="6d395-149">Alert Level</span></span> | <span data-ttu-id="6d395-150">전송되는 경고</span><span class="sxs-lookup"><span data-stu-id="6d395-150">Alerts sent</span></span> |
   | --- | --- |
   | <span data-ttu-id="6d395-151">중요</span><span class="sxs-lookup"><span data-stu-id="6d395-151">Critical</span></span> |<span data-ttu-id="6d395-152">백업 실패, 복구 실패</span><span class="sxs-lookup"><span data-stu-id="6d395-152">Backup failure, recovery failure</span></span> |
   | <span data-ttu-id="6d395-153">Warning</span><span class="sxs-lookup"><span data-stu-id="6d395-153">Warning</span></span> |<span data-ttu-id="6d395-154">없음</span><span class="sxs-lookup"><span data-stu-id="6d395-154">None</span></span> |
   | <span data-ttu-id="6d395-155">정보 제공</span><span class="sxs-lookup"><span data-stu-id="6d395-155">Informational</span></span> |<span data-ttu-id="6d395-156">없음</span><span class="sxs-lookup"><span data-stu-id="6d395-156">None</span></span> |

### <a name="are-there-situations-where-email-isnt-sent-even-if-notifications-are-configured"></a><span data-ttu-id="6d395-157">알림이 구성된 경우에도 전자 메일이 전송되지 않는 경우가 있습니까?</span><span class="sxs-lookup"><span data-stu-id="6d395-157">Are there situations where email isn't sent even if notifications are configured?</span></span>
<span data-ttu-id="6d395-158">알림이 제대로 구성되었더라도 경고가 전송되지 않는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-158">There are situations where an alert is not sent, even though the notifications have been properly configured.</span></span> <span data-ttu-id="6d395-159">이처럼 전자 메일 알림이 전송되지 않는 경우는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-159">In the following situations email notifications are not sent to avoid alert noise:</span></span>

* <span data-ttu-id="6d395-160">알림이 매시간 다이제스트로 구성되고 알림이 발생하고 한 시간 이내에 확인되는 경우.</span><span class="sxs-lookup"><span data-stu-id="6d395-160">If notifications are configured to Hourly Digest, and an alert is raised and resolved within the hour.</span></span>
* <span data-ttu-id="6d395-161">작업이 취소됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-161">The job is canceled.</span></span>
* <span data-ttu-id="6d395-162">백업 작업이 트리거된 다음 실패하고 다른 백업 작업이 진행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-162">A backup job is triggered and then fails, and another backup job is in progress.</span></span>
* <span data-ttu-id="6d395-163">리소스 관리자 활성화된 VM에 대한 예약된 백업 작업이 시작되지만 VM이 더 이상 존재하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-163">A scheduled backup job for a Resource Manager-enabled VM starts, but the VM no longer exists.</span></span>

## <a name="customize-your-view-of-events"></a><span data-ttu-id="6d395-164">이벤트 보기 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="6d395-164">Customize your view of events</span></span>
<span data-ttu-id="6d395-165">**감사 로그** 설정은 미리 정의된 필터 집합 및 작동 가능한 이벤트 정보를 표시하는 열과 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-165">The **Audit logs** setting comes with a pre-defined set of filters and columns showing operational event information.</span></span> <span data-ttu-id="6d395-166">**이벤트** 블레이드가 열릴 때 원하는 정보를 표시하도록 보기를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-166">You can customize the view so that when the **Events** blade opens, it shows you the information you want.</span></span>

1. <span data-ttu-id="6d395-167">[자격 증명 모음 대시보드](backup-azure-manage-vms.md#open-a-recovery-services-vault-in-the-dashboard)에서 **감사 로그**를 찾아보고 클릭하여 **이벤트** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-167">In the [vault dashboard](backup-azure-manage-vms.md#open-a-recovery-services-vault-in-the-dashboard), browse to and click **Audit Logs** to open the **Events** blade.</span></span>

    ![감사 로그](./media/backup-azure-monitor-vms/audit-logs-1606-1.png)

    <span data-ttu-id="6d395-169">**이벤트** 블레이드는 현재 자격 증명 모음에 대해서만 필터링되는 작동 이벤트에 열립니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-169">The **Events** blade opens to the operational events filtered just for the current vault.</span></span>

    ![감사 로그 필터](./media/backup-azure-monitor-vms/audit-logs-filter.png)

    <span data-ttu-id="6d395-171">블레이드에서는 지난 주에 발생한 중요, 오류, 경고 및 정보 이벤트의 목록을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-171">The blade shows the list of Critical, Error, Warning, and Informational events that occurred in the past week.</span></span> <span data-ttu-id="6d395-172">시간 범위는 **필터**에 설정된 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-172">The time span is a default value set in the **Filter**.</span></span> <span data-ttu-id="6d395-173">**이벤트** 블레이드에서는 이벤트가 발생했을 때 추적하는 가로 막대형 차트도 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-173">The **Events** blade also shows a bar chart tracking when the events occurred.</span></span> <span data-ttu-id="6d395-174">가로 막대형 차트를 표시하지 않으려는 경우 **이벤트** 메뉴에서 **차트 숨기기**를 클릭하여 차트를 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-174">If you don't want to see the bar chart, in the **Events** menu, click **Hide chart** to toggle off the chart.</span></span> <span data-ttu-id="6d395-175">이벤트의 기본 보기는 작업, 수준, 상태, 리소스 및 시간 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-175">The default view of Events shows Operation, Level, Status, Resource, and Time information.</span></span> <span data-ttu-id="6d395-176">추가 이벤트 특성의 표시에 대한 자세한 내용은 [이벤트 정보 확장](backup-azure-monitor-vms.md#view-additional-event-attributes)섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d395-176">For information about exposing additional Event attributes, see the section [expanding Event information](backup-azure-monitor-vms.md#view-additional-event-attributes).</span></span>
2. <span data-ttu-id="6d395-177">작동할 수 있는 이벤트에 대한 자세한 내용을 보려면 **작업** 열에서 작동할 수 있는 이벤트를 클릭하여 해당 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-177">For additional information on an operational event, in the **Operation** column, click an operational event to open its blade.</span></span> <span data-ttu-id="6d395-178">블레이드는 이벤트에 대한 자세한 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-178">The blade contains detailed information about the events.</span></span> <span data-ttu-id="6d395-179">이벤트는 상관 관계 ID 및 시간 범위에 발생한 이벤트 목록별로 그룹화됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-179">Events are grouped by their correlation ID and a list of the events that occurred in the Time span.</span></span>

    ![작업 세부 정보](./media/backup-azure-monitor-vms/audit-logs-details-window.png)
3. <span data-ttu-id="6d395-181">특정 이벤트에 대한 자세한 정보를 보려면 이벤트의 목록에서 이벤트를 클릭하여 해당 **세부 정보** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-181">To view detailed information about a particular event, from the list of events, click the event to open its **Details** blade.</span></span>

    ![이벤트 세부 정보](./media/backup-azure-monitor-vms/audit-logs-details-window-deep.png)

    <span data-ttu-id="6d395-183">이벤트 수준 정보는 정보에서 가져오는 만큼 자세합니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-183">The Event-level information is as detailed as the information gets.</span></span> <span data-ttu-id="6d395-184">각 이벤트에 대해 많은 정보를 보기를 선호하고 이러한 많은 정보를 **이벤트** 블레이드에 추가하려는 경우 [이벤트 정보 확장](backup-azure-monitor-vms.md#view-additional-event-attributes)섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d395-184">If you prefer seeing this much information about each event, and would like to add this much detail to the **Events** blade, see the section [expanding Event information](backup-azure-monitor-vms.md#view-additional-event-attributes).</span></span>

## <a name="customize-the-event-filter"></a><span data-ttu-id="6d395-185">이벤트 필터 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="6d395-185">Customize the event filter</span></span>
<span data-ttu-id="6d395-186">**필터** 를 사용하여 특정 블레이드에 나타나는 정보를 조정하거나 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-186">Use the **Filter** to adjust or choose the information that appears in a particular blade.</span></span> <span data-ttu-id="6d395-187">이벤트 정보를 필터링하려면:</span><span class="sxs-lookup"><span data-stu-id="6d395-187">To filter the event information:</span></span>

1. <span data-ttu-id="6d395-188">[자격 증명 모음 대시보드](backup-azure-manage-vms.md#open-a-recovery-services-vault-in-the-dashboard)에서 **감사 로그**를 찾아보고 클릭하여 **이벤트** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-188">In the [vault dashboard](backup-azure-manage-vms.md#open-a-recovery-services-vault-in-the-dashboard), browse to and click **Audit Logs** to open the **Events** blade.</span></span>

    ![감사 로그](./media/backup-azure-monitor-vms/audit-logs-1606-1.png)

    <span data-ttu-id="6d395-190">**이벤트** 블레이드는 현재 자격 증명 모음에 대해서만 필터링되는 작동 이벤트에 열립니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-190">The **Events** blade opens to the operational events filtered just for the current vault.</span></span>

    ![감사 로그 필터](./media/backup-azure-monitor-vms/audit-logs-filter.png)
2. <span data-ttu-id="6d395-192">**이벤트** 메뉴에서 **필터**를 클릭하여 해당 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-192">On the **Events** menu, click **Filter** to open that blade.</span></span>

    ![필터 블레이드 열기](./media/backup-azure-monitor-vms/audit-logs-filter-button.png)
3. <span data-ttu-id="6d395-194">**필터** 블레이드에서 **수준**, **시간 범위** 및 **호출자** 필터를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-194">On the **Filter** blade, adjust the **Level**, **Time span**, and **Caller** filters.</span></span> <span data-ttu-id="6d395-195">복구 서비스 자격 증명 모음에 대한 현재 정보를 제공하도록 설정되었기 때문에 다른 필터를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-195">The other filters are not available since they were set to provide the current information for the Recovery Services vault.</span></span>

    ![감사 로그 쿼리 세부 정보](./media/backup-azure-monitor-vms/filter-blade.png)

    <span data-ttu-id="6d395-197">이벤트의 **수준** 을 중요, 오류, 경고 또는 정보로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-197">You can specify the **Level** of event: Critical, Error, Warning, or Informational.</span></span> <span data-ttu-id="6d395-198">이벤트 수준의 조합을 선택할 수 있지만 하나 이상의 수준을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-198">You can choose any combination of event Levels, but you must have at least one Level selected.</span></span> <span data-ttu-id="6d395-199">수준을 설정하거나 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-199">Toggle the Level on or off.</span></span> <span data-ttu-id="6d395-200">**시간 범위** 필터를 사용하면 이벤트 캡처에 대한 시간의 길이를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-200">The **Time span** filter allows you to specify the length of time for capturing events.</span></span> <span data-ttu-id="6d395-201">사용자 지정 시간 범위를 사용하는 경우 시작 및 종료 시간을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-201">If you use a custom Time span, you can set the start and end times.</span></span>
4. <span data-ttu-id="6d395-202">필터를 사용하여 작업 로그를 쿼리할 준비가 되면 **업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-202">Once you are ready to query the operations logs using your filter, click **Update**.</span></span> <span data-ttu-id="6d395-203">**이벤트** 블레이드에 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-203">The results display in the **Events** blade.</span></span>

    ![작업 세부 정보](./media/backup-azure-monitor-vms/edited-list-of-events.png)

### <a name="view-additional-event-attributes"></a><span data-ttu-id="6d395-205">추가 이벤트 특성 보기</span><span class="sxs-lookup"><span data-stu-id="6d395-205">View additional event attributes</span></span>
<span data-ttu-id="6d395-206">**열** 단추를 사용하여 추가 이벤트 특성을 **이벤트** 블레이드의 목록에 나타나게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-206">Using the **Columns** button, you can enable additional event attributes to appear in the list on the **Events** blade.</span></span> <span data-ttu-id="6d395-207">이벤트의 기본 목록은 작업, 수준, 상태, 리소스 및 시간 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-207">The default list of events displays information for Operation, Level, Status, Resource, and Time.</span></span> <span data-ttu-id="6d395-208">추가 특성을 사용하려면:</span><span class="sxs-lookup"><span data-stu-id="6d395-208">To enable additional attributes:</span></span>

1. <span data-ttu-id="6d395-209">**이벤트** 블레이드에서 **열**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-209">On the **Events** blade, click **Columns**.</span></span>

    ![열 열기](./media/backup-azure-monitor-vms/audi-logs-column-button.png)

    <span data-ttu-id="6d395-211">**열 선택** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-211">The **Choose columns** blade opens.</span></span>

    ![열 블레이드](./media/backup-azure-monitor-vms/columns-blade.png)
2. <span data-ttu-id="6d395-213">특성을 선택하려면 확인란을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-213">To select the attribute, click the checkbox.</span></span> <span data-ttu-id="6d395-214">특성 확인란이 설정 및 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-214">The attribute checkbox toggles on and off.</span></span>
3. <span data-ttu-id="6d395-215">**이벤트** 블레이드의 특성 목록을 다시 설정하려면 **다시 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-215">Click **Reset** to reset the list of attributes in the **Events** blade.</span></span> <span data-ttu-id="6d395-216">목록에서 특성을 추가 또는 제거한 후 **재설정** 을 사용하여 이벤트 특성의 새 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-216">After adding or removing attributes from the list, use **Reset** to view the new list of Event attributes.</span></span>
4. <span data-ttu-id="6d395-217">**업데이트** 를 클릭하여 이벤트 특성의 데이터를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-217">Click **Update** to update the data in the Event attributes.</span></span> <span data-ttu-id="6d395-218">다음 표는 각 특성에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-218">The following table provides information about each attribute.</span></span>

| <span data-ttu-id="6d395-219">열 이름</span><span class="sxs-lookup"><span data-stu-id="6d395-219">Column name</span></span> | <span data-ttu-id="6d395-220">설명</span><span class="sxs-lookup"><span data-stu-id="6d395-220">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6d395-221">작업</span><span class="sxs-lookup"><span data-stu-id="6d395-221">Operation</span></span> |<span data-ttu-id="6d395-222">작업 이름</span><span class="sxs-lookup"><span data-stu-id="6d395-222">The name of the operation</span></span> |
| <span data-ttu-id="6d395-223">수준</span><span class="sxs-lookup"><span data-stu-id="6d395-223">Level</span></span> |<span data-ttu-id="6d395-224">작업 수준, 가능한 값: 정보, 경고, 오류 또는 중요</span><span class="sxs-lookup"><span data-stu-id="6d395-224">The level of the operation, values can be: Informational, Warning, Error, or Critical</span></span> |
| <span data-ttu-id="6d395-225">가동 상태</span><span class="sxs-lookup"><span data-stu-id="6d395-225">Status</span></span> |<span data-ttu-id="6d395-226">작업에 대한 설명이 포함된 상태</span><span class="sxs-lookup"><span data-stu-id="6d395-226">Descriptive state of the operation</span></span> |
| <span data-ttu-id="6d395-227">리소스</span><span class="sxs-lookup"><span data-stu-id="6d395-227">Resource</span></span> |<span data-ttu-id="6d395-228">리소스를 식별하는 URL. 리소스 ID라고도 함</span><span class="sxs-lookup"><span data-stu-id="6d395-228">URL that identifies the resource; also known as the resource ID</span></span> |
| <span data-ttu-id="6d395-229">Time</span><span class="sxs-lookup"><span data-stu-id="6d395-229">Time</span></span> |<span data-ttu-id="6d395-230">시간, 현재 시간부터 이벤트가 발생한 시간까지 측정</span><span class="sxs-lookup"><span data-stu-id="6d395-230">Time, measured from the current time, when the event occurred</span></span> |
| <span data-ttu-id="6d395-231">Caller</span><span class="sxs-lookup"><span data-stu-id="6d395-231">Caller</span></span> |<span data-ttu-id="6d395-232">이벤트를 호출하거나 트리거한 사람 또는 대상. 시스템 또는 사용자일 수 있음</span><span class="sxs-lookup"><span data-stu-id="6d395-232">Who or what called or triggered the event; can be the system, or a user</span></span> |
| <span data-ttu-id="6d395-233">Timestamp</span><span class="sxs-lookup"><span data-stu-id="6d395-233">Timestamp</span></span> |<span data-ttu-id="6d395-234">이벤트 트리거된 시간</span><span class="sxs-lookup"><span data-stu-id="6d395-234">The time when the event was triggered</span></span> |
| <span data-ttu-id="6d395-235">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="6d395-235">Resource Group</span></span> |<span data-ttu-id="6d395-236">연결된 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="6d395-236">The associated resource group</span></span> |
| <span data-ttu-id="6d395-237">리소스 종류</span><span class="sxs-lookup"><span data-stu-id="6d395-237">Resource Type</span></span> |<span data-ttu-id="6d395-238">리소스 관리자가 사용하는 내부 리소스 유형</span><span class="sxs-lookup"><span data-stu-id="6d395-238">The internal resource type used by Resource Manager</span></span> |
| <span data-ttu-id="6d395-239">구독 ID</span><span class="sxs-lookup"><span data-stu-id="6d395-239">Subscription ID</span></span> |<span data-ttu-id="6d395-240">연결된 구독 ID</span><span class="sxs-lookup"><span data-stu-id="6d395-240">The associated subscription ID</span></span> |
| <span data-ttu-id="6d395-241">Category</span><span class="sxs-lookup"><span data-stu-id="6d395-241">Category</span></span> |<span data-ttu-id="6d395-242">이벤트의 범주</span><span class="sxs-lookup"><span data-stu-id="6d395-242">Category of the event</span></span> |
| <span data-ttu-id="6d395-243">상관관계 ID</span><span class="sxs-lookup"><span data-stu-id="6d395-243">Correlation ID</span></span> |<span data-ttu-id="6d395-244">관련된 이벤트에 대한 일반적인 ID</span><span class="sxs-lookup"><span data-stu-id="6d395-244">Common ID for related events</span></span> |

## <a name="use-powershell-to-customize-alerts"></a><span data-ttu-id="6d395-245">PowerShell을 사용하여 경고 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="6d395-245">Use PowerShell to customize alerts</span></span>
<span data-ttu-id="6d395-246">포털에서 작업에 대한 사용자 지정 경고 알림을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-246">You can get custom alert notifications for the jobs in the portal.</span></span> <span data-ttu-id="6d395-247">다음 작업을 가져오려면 작업 로그 이벤트에서 PowerShell 기반 경고 규칙을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-247">To get these jobs, define PowerShell-based alert rules on the operational logs events.</span></span> <span data-ttu-id="6d395-248">*Azure PowerShell 버전 1.3.0 이상*을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-248">Use *PowerShell version 1.3.0 or later*.</span></span>

<span data-ttu-id="6d395-249">사용자 지정 알림을 정의하여 백업 실패에 대해 경고하려면 다음 스크립트와 같은 명령을 사용:</span><span class="sxs-lookup"><span data-stu-id="6d395-249">To define a custom notification to alert for backup failures, use a command like the following script:</span></span>

```
PS C:\> $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail contoso@microsoft.com
PS C:\> Add-AzureRmLogAlertRule -Name backupFailedAlert -Location "East US" -ResourceGroup RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US -OperationName Microsoft.RecoveryServices/recoveryServicesVault/Backup -Status Failed -TargetResourceId /subscriptions/86eeac34-eth9a-4de3-84db-7a27d121967e/resourceGroups/RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US/providers/Microsoft.RecoveryServices/vaults/trinadhVault -Actions $actionEmail
```

<span data-ttu-id="6d395-250">**ResourceId** : 감사 로그에서 ResourceId를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-250">**ResourceId** : You can get ResourceId from the Audit logs.</span></span> <span data-ttu-id="6d395-251">ResourceId는 작업 로그의 리소스 열에 제공된 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-251">The ResourceId is a URL provided in the Resource column of the Operation logs.</span></span>

<span data-ttu-id="6d395-252">**OperationName**: OperationName의 형식은 "Microsoft.RecoveryServices/recoveryServicesVault/*EventName*"이며, 여기서 *EventName*은 다음과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-252">**OperationName** : OperationName is in the format "Microsoft.RecoveryServices/recoveryServicesVault/*EventName*" where *EventName* can be:</span></span><br/>

* <span data-ttu-id="6d395-253">등록</span><span class="sxs-lookup"><span data-stu-id="6d395-253">Register</span></span> <br/>
* <span data-ttu-id="6d395-254">등록 취소 </span><span class="sxs-lookup"><span data-stu-id="6d395-254">Unregister</span></span> <br/>
* <span data-ttu-id="6d395-255">ConfigureProtection </span><span class="sxs-lookup"><span data-stu-id="6d395-255">ConfigureProtection</span></span> <br/>
* <span data-ttu-id="6d395-256">백업 </span><span class="sxs-lookup"><span data-stu-id="6d395-256">Backup</span></span> <br/>
* <span data-ttu-id="6d395-257">복원 </span><span class="sxs-lookup"><span data-stu-id="6d395-257">Restore</span></span> <br/>
* <span data-ttu-id="6d395-258">StopProtection </span><span class="sxs-lookup"><span data-stu-id="6d395-258">StopProtection</span></span> <br/>
* <span data-ttu-id="6d395-259">DeleteBackupData </span><span class="sxs-lookup"><span data-stu-id="6d395-259">DeleteBackupData</span></span> <br/>
* <span data-ttu-id="6d395-260">CreateProtectionPolicy </span><span class="sxs-lookup"><span data-stu-id="6d395-260">CreateProtectionPolicy</span></span> <br/>
* <span data-ttu-id="6d395-261">DeleteProtectionPolicy </span><span class="sxs-lookup"><span data-stu-id="6d395-261">DeleteProtectionPolicy</span></span> <br/>
* <span data-ttu-id="6d395-262">UpdateProtectionPolicy </span><span class="sxs-lookup"><span data-stu-id="6d395-262">UpdateProtectionPolicy</span></span> <br/>

<span data-ttu-id="6d395-263">**상태** : 지원되는 값은 시작함, 성공함 또는 실패함입니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-263">**Status** : Supported values are Started, Succeeded, or Failed.</span></span>

<span data-ttu-id="6d395-264">**ResourceGroup** : 리소스가 속한 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-264">**ResourceGroup** : This is the Resource Group to which the resource belongs.</span></span> <span data-ttu-id="6d395-265">생성된 로그에 리소스 그룹 열을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-265">You can add the Resource Group column to the generated logs.</span></span> <span data-ttu-id="6d395-266">리소스 그룹은 사용할 수 있는 이벤트 정보의 종류 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-266">Resource Group is one of the available types of event information.</span></span>

<span data-ttu-id="6d395-267">**이름** : 경고 규칙의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-267">**Name** : Name of the Alert Rule.</span></span>

<span data-ttu-id="6d395-268">**CustomEmail** : 경고 알림을 보낼 사용자 지정 메일 주소를 지정</span><span class="sxs-lookup"><span data-stu-id="6d395-268">**CustomEmail** : Specify the custom email address to which you want to send an alert notification</span></span>

<span data-ttu-id="6d395-269">**SendToServiceOwners** : 이 옵션은 구독의 모든 관리자 및 공동 관리자에게 경고 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-269">**SendToServiceOwners** : This option sends alert notifications to all administrators and co-administrators of the subscription.</span></span> <span data-ttu-id="6d395-270">**New-AzureRmAlertRuleEmail** cmdlet에 사용될 수 있음</span><span class="sxs-lookup"><span data-stu-id="6d395-270">It can be used in **New-AzureRmAlertRuleEmail** cmdlet</span></span>

### <a name="limitations-on-alerts"></a><span data-ttu-id="6d395-271">경고에 대한 제한</span><span class="sxs-lookup"><span data-stu-id="6d395-271">Limitations on Alerts</span></span>
<span data-ttu-id="6d395-272">이벤트 기반 경고에 다음과 같은 제한 사항이 적용됨:</span><span class="sxs-lookup"><span data-stu-id="6d395-272">Event-based alerts are subject to the following limitations:</span></span>

1. <span data-ttu-id="6d395-273">복구 서비스 자격 증명 모음의 모든 가상 컴퓨터에서 경고를 유발합니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-273">Alerts are triggered on all virtual machines in the Recovery Services vault.</span></span> <span data-ttu-id="6d395-274">복구 서비스 자격 증명 모음에서 가상 컴퓨터의 하위 집합에 대한 경고를 사용자 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-274">You cannot customize the alert for a subset of virtual machines in a Recovery Services vault.</span></span>
2. <span data-ttu-id="6d395-275">이 기능은 미리 보기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-275">This feature is in Preview.</span></span> [<span data-ttu-id="6d395-276">자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="6d395-276">Learn more</span></span>](../monitoring-and-diagnostics/insights-powershell-samples.md#create-metric-alerts)
3. <span data-ttu-id="6d395-277">"alerts-noreply@mail.windowsazure.com"에서 경고를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-277">Alerts are sent from "alerts-noreply@mail.windowsazure.com".</span></span> <span data-ttu-id="6d395-278">현재는 전자 메일 보낸 사람을 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-278">Currently you can't modify the email sender.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d395-279">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6d395-279">Next steps</span></span>
<span data-ttu-id="6d395-280">이벤트 로그를 사용하면 백업 작업에 대한 post-mortem 및 감사 지원이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-280">Event logs enable great post-mortem and audit support for the backup operations.</span></span> <span data-ttu-id="6d395-281">다음 작업이 기록됨:</span><span class="sxs-lookup"><span data-stu-id="6d395-281">The following operations are logged:</span></span>

* <span data-ttu-id="6d395-282">등록</span><span class="sxs-lookup"><span data-stu-id="6d395-282">Register</span></span>
* <span data-ttu-id="6d395-283">등록 취소</span><span class="sxs-lookup"><span data-stu-id="6d395-283">Unregister</span></span>
* <span data-ttu-id="6d395-284">보호 구성</span><span class="sxs-lookup"><span data-stu-id="6d395-284">Configure protection</span></span>
* <span data-ttu-id="6d395-285">백업(예약된 백업 및 주문형 백업 모두)</span><span class="sxs-lookup"><span data-stu-id="6d395-285">Backup (Both scheduled as well as on-demand backup)</span></span>
* <span data-ttu-id="6d395-286">복원</span><span class="sxs-lookup"><span data-stu-id="6d395-286">Restore</span></span>
* <span data-ttu-id="6d395-287">보호 중지</span><span class="sxs-lookup"><span data-stu-id="6d395-287">Stop protection</span></span>
* <span data-ttu-id="6d395-288">백업 데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="6d395-288">Delete backup data</span></span>
* <span data-ttu-id="6d395-289">정책 추가</span><span class="sxs-lookup"><span data-stu-id="6d395-289">Add policy</span></span>
* <span data-ttu-id="6d395-290">정책 삭제</span><span class="sxs-lookup"><span data-stu-id="6d395-290">Delete policy</span></span>
* <span data-ttu-id="6d395-291">정책 업데이트</span><span class="sxs-lookup"><span data-stu-id="6d395-291">Update policy</span></span>
* <span data-ttu-id="6d395-292">작업 취소</span><span class="sxs-lookup"><span data-stu-id="6d395-292">Cancel job</span></span>

<span data-ttu-id="6d395-293">Azure 서비스 전반에 걸쳐 이벤트, 작업 및 감사 로그에 대한 자세한 설명은 [이벤트 및 감사 로그 보기](../monitoring-and-diagnostics/insights-debugging-with-events.md)문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d395-293">For a broad explanation of events, operations, and audit logs across the Azure services, see the article, [View events and audit logs](../monitoring-and-diagnostics/insights-debugging-with-events.md).</span></span>

<span data-ttu-id="6d395-294">복구 지점에서 가상 컴퓨터를 다시 만드는 방법에 대한 내용은 [Azure VM 복원](backup-azure-restore-vms.md)을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-294">For information on re-creating a virtual machine from a recovery point, check out [Restore Azure VMs](backup-azure-restore-vms.md).</span></span> <span data-ttu-id="6d395-295">가상 컴퓨터를 보호하는 방법에 대한 정보가 필요한 경우 [먼저 보기: 복구 서비스 자격 증명 모음에 VM 백업](backup-azure-vms-first-look-arm.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d395-295">If you need information on protecting your virtual machines, see [First look: Back up VMs to a Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span> <span data-ttu-id="6d395-296">[Azure 가상 컴퓨터 백업 관리](backup-azure-manage-vms.md)문서에서 VM 백업에 대한 관리 작업에 관하여 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6d395-296">Learn about the management tasks for VM backups in the article, [Manage Azure virtual machine backups](backup-azure-manage-vms.md).</span></span>
