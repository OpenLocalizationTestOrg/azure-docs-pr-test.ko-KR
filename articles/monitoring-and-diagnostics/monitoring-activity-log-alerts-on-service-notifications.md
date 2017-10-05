---
title: "서비스 알림에 대한 활동 로그 경고 수신 | Microsoft Docs"
description: "Azure 서비스가 발생할 때 SMS, 전자 메일 또는 웹후크를 통해 알림을 받습니다."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: johnkem
ms.openlocfilehash: bf6a98fd7e7e11764bef174f9efd0635fa7efe9a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-activity-log-alerts-on-service-notifications"></a><span data-ttu-id="5ef76-103">서비스 알림에 대한 활동 로그 경고 만들기</span><span class="sxs-lookup"><span data-stu-id="5ef76-103">Create activity log alerts on service notifications</span></span>
## <a name="overview"></a><span data-ttu-id="5ef76-104">개요</span><span class="sxs-lookup"><span data-stu-id="5ef76-104">Overview</span></span>
<span data-ttu-id="5ef76-105">이 문서에서는 Azure Portal을 사용하여 서비스 상태 알림에 대한 활동 로그 경고를 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5ef76-105">This article shows you how to set up activity log alerts for service health notifications by using the Azure portal.</span></span>  

<span data-ttu-id="5ef76-106">Azure에서 Azure 구독에 서비스 상태 알림을 전송할 때 경고를 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef76-106">You can receive an alert when Azure sends service health notifications to your Azure subscription.</span></span> <span data-ttu-id="5ef76-107">다음 항목에 따라 경고를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef76-107">You can configure the alert based on:</span></span>

- <span data-ttu-id="5ef76-108">서비스 상태 알림의 클래스(인시던트, 유지 관리, 정보 등)</span><span class="sxs-lookup"><span data-stu-id="5ef76-108">The class of service health notification (incident, maintenance, information, etc.).</span></span>
- <span data-ttu-id="5ef76-109">영향을 받는 서비스</span><span class="sxs-lookup"><span data-stu-id="5ef76-109">The service(s) affected.</span></span>
- <span data-ttu-id="5ef76-110">영향을 받는 하위 지역</span><span class="sxs-lookup"><span data-stu-id="5ef76-110">The region(s) affected.</span></span>
- <span data-ttu-id="5ef76-111">알림의 상태(활성 및 해결)</span><span class="sxs-lookup"><span data-stu-id="5ef76-111">The status of the notification (active vs. resolved).</span></span>
- <span data-ttu-id="5ef76-112">알림 수준(정보, 경고, 오류)</span><span class="sxs-lookup"><span data-stu-id="5ef76-112">The level of the notifications (informational, warning, error).</span></span>

<span data-ttu-id="5ef76-113">다음과 같이 경고를 받는 사람도 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef76-113">You also can configure who the alert should be sent to:</span></span>

- <span data-ttu-id="5ef76-114">기존 작업 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef76-114">Select an existing action group.</span></span>
- <span data-ttu-id="5ef76-115">새 작업 그룹을 만듭니다(향후 경고에 사용할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="5ef76-115">Create a new action group (that can be used for future alerts).</span></span>

<span data-ttu-id="5ef76-116">작업 그룹에 대해 자세히 알아보려면 [작업 그룹 만들기 및 관리](monitoring-action-groups.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ef76-116">To learn more about action groups, see [Create and manage action groups](monitoring-action-groups.md).</span></span>

<span data-ttu-id="5ef76-117">Azure 리소스 관리자 템플릿을 사용하여 서비스 상태 알림 경고를 구성하는 방법에 대한 자세한 내용은 [ 템플릿](monitoring-create-activity-log-alerts-with-resource-manager-template.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ef76-117">For information on how to configure service health notification alerts by using Azure Resource Manager templates, see [Resource Manager templates](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>

## <a name="create-an-alert-on-a-service-health-notification-for-a-new-action-group-by-using-the-azure-portal"></a><span data-ttu-id="5ef76-118">Azure Portal을 사용하여 새 작업 그룹에 대한 서비스 상태 알림의 경고 만들기</span><span class="sxs-lookup"><span data-stu-id="5ef76-118">Create an alert on a service health notification for a new action group by using the Azure portal</span></span>
1. <span data-ttu-id="5ef76-119">[포털](https://portal.azure.com)에서 **모니터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef76-119">In the [portal](https://portal.azure.com), select **Monitor**.</span></span>

    ![“모니터링” 서비스](./media/monitoring-activity-log-alerts-on-service-notifications/home-monitor.png)

2. <span data-ttu-id="5ef76-121">**활동 로그** 섹션에서 **경고**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef76-121">In the **Activity log** section, select **Alerts**.</span></span>

    ![“경고” 탭](./media/monitoring-activity-log-alerts-on-service-notifications/alerts-blades.png)

3. <span data-ttu-id="5ef76-123">**활동 로그 경고 추가**를 선택하고 필드를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef76-123">Select **Add activity log alert**, and fill in the fields.</span></span>

    ![“활동 로그 경고 추가” 명령](./media/monitoring-activity-log-alerts-on-service-notifications/add-activity-log-alert.png)

4. <span data-ttu-id="5ef76-125">**활동 로그 경고 이름** 상자에 이름을 입력하고 **설명**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef76-125">Enter a name in the **Activity log alert name** box, and provide a **Description**.</span></span>

    ![“활동 로그 경고 추가” 대화 상자](./media/monitoring-activity-log-alerts-on-service-notifications/activity-log-alert-service-notification-new-action-group.png)

5. <span data-ttu-id="5ef76-127">**구독** 상자가 현재 구독으로 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="5ef76-127">The **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="5ef76-128">이 구독은 활동 로그 경고를 저장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ef76-128">This subscription is used to save the activity log alert.</span></span> <span data-ttu-id="5ef76-129">경고 리소스가 이 구독에 배포되고 이에 대한 활동 로그에서 이벤트를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef76-129">The alert resource is deployed to this subscription and monitors events in the activity log for it.</span></span>

6. <span data-ttu-id="5ef76-130">경고 리소스가 만들어지는 **리소스 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef76-130">Select the **Resource group** in which the alert resource is created.</span></span> <span data-ttu-id="5ef76-131">이는 경고에 의해 모니터링되는 리소스 그룹이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="5ef76-131">This isn't the resource group that's monitored by the alert.</span></span> <span data-ttu-id="5ef76-132">대신 경고 리소스가 있는 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="5ef76-132">Instead, it's the resource group where the alert resource is located.</span></span>

7. <span data-ttu-id="5ef76-133">**이벤트 범주** 상자에서 **서비스 상태**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef76-133">In the **Event category** box, select **Service Health**.</span></span> <span data-ttu-id="5ef76-134">선택적으로 수신하려는 서비스 상태 알림의 **서비스**, **하위 지역**, **형식**, **상태** 및 **수준**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef76-134">Optionally, select the **Service**, **Region**, **Type**, **Status**, and **Level** of service health notifications that you want to receive.</span></span>

8. <span data-ttu-id="5ef76-135">**다음을 통해 경고**에서 **신규** 작업 그룹 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef76-135">Under **Alert via**, select the **New** action group button.</span></span> <span data-ttu-id="5ef76-136">**작업 그룹 이름** 상자에 이름을 입력하고 **약식 이름** 상자에 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef76-136">Enter a name in the **Action group name** box, and enter a name in the **Short name** box.</span></span> <span data-ttu-id="5ef76-137">약식 이름은 이 경고가 발생할 때 전송된 알림에서 참조됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ef76-137">The short name is referenced in the notifications that are sent when this alert fires.</span></span>

9. <span data-ttu-id="5ef76-138">받는 사람에 대한 다음 항목을 제공하여 받는 사람 목록을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef76-138">Define a list of receivers by providing the receiver's:</span></span>

    <span data-ttu-id="5ef76-139">a.</span><span class="sxs-lookup"><span data-stu-id="5ef76-139">a.</span></span> <span data-ttu-id="5ef76-140">**이름**: 받는 사람의 이름, 별칭 또는 식별자를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef76-140">**Name**: Enter the receiver’s name, alias, or identifier.</span></span>

    <span data-ttu-id="5ef76-141">b.</span><span class="sxs-lookup"><span data-stu-id="5ef76-141">b.</span></span> <span data-ttu-id="5ef76-142">**작업 유형**: SMS, 전자 메일 또는 웹후크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef76-142">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="5ef76-143">c.</span><span class="sxs-lookup"><span data-stu-id="5ef76-143">c.</span></span> <span data-ttu-id="5ef76-144">**세부 정보**: 선택한 작업 유형에 따라 전화 번호, 이메일 주소 또는 웹후크 URI를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef76-144">**Details**: Based on the action type chosen, enter a phone number, email address, or webhook URI.</span></span>

10. <span data-ttu-id="5ef76-145">**확인**을 선택하여 경고를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ef76-145">Select **OK** to create the alert.</span></span>

<span data-ttu-id="5ef76-146">몇 분 이내에 경고가 활성화되고 만들 때 지정한 조건에 따라 트리거를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef76-146">Within a few minutes, the alert is active and begins to trigger based on the conditions you specified during creation.</span></span>

<span data-ttu-id="5ef76-147">활동 로그 경고에 대한 웹후크 스키마 정보는 [Azure 활동 로그 경고에 대한 웹후크](monitoring-activity-log-alerts-webhook.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ef76-147">For information on the webhook schema for activity log alerts, see [Webhooks for Azure activity log alerts](monitoring-activity-log-alerts-webhook.md).</span></span>

>[!NOTE]
><span data-ttu-id="5ef76-148">이러한 단계에서 정의한 작업 그룹은 향후의 모든 경고 정의에 대해 기존 작업 그룹으로 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ef76-148">The action group defined in these steps is reusable as an existing action group for all future alert definitions.</span></span>
>
>

## <a name="create-an-alert-on-a-service-health-notification-for-an-existing-action-group-by-using-the-azure-portal"></a><span data-ttu-id="5ef76-149">Azure Portal을 사용하여 기존 작업 그룹에 대한 서비스 상태 알림의 경고 만들기</span><span class="sxs-lookup"><span data-stu-id="5ef76-149">Create an alert on a service health notification for an existing action group by using the Azure portal</span></span>

1. <span data-ttu-id="5ef76-150">이전 섹션의 1-7단계를 수행하여 서비스 상태 알림을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ef76-150">Follow steps 1 through 7 in the previous section to create your service health notification.</span></span> 

2. <span data-ttu-id="5ef76-151">**다음을 통해 경고**에서 **기존** 작업 그룹 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef76-151">Under **Alert via**, select the **Existing** action group button.</span></span> <span data-ttu-id="5ef76-152">적절한 작업 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef76-152">Select the appropriate action group.</span></span>

3. <span data-ttu-id="5ef76-153">**확인**을 선택하여 경고를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ef76-153">Select **OK** to create the alert.</span></span>

<span data-ttu-id="5ef76-154">몇 분 이내에 경고가 활성화되고 만들 때 지정한 조건에 따라 트리거를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef76-154">Within a few minutes, the alert is active and begins to trigger based on the conditions you specified during creation.</span></span>

## <a name="manage-your-alerts"></a><span data-ttu-id="5ef76-155">경고 관리</span><span class="sxs-lookup"><span data-stu-id="5ef76-155">Manage your alerts</span></span>

<span data-ttu-id="5ef76-156">경고를 만들면 **모니터** 블레이드의 **경고** 섹션에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ef76-156">After you create an alert, it's visible in the **Alerts** section of the **Monitor** blade.</span></span> <span data-ttu-id="5ef76-157">관리하려는 경고를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef76-157">Select the alert you want to manage to:</span></span>

* <span data-ttu-id="5ef76-158">편집합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef76-158">Edit it.</span></span>
* <span data-ttu-id="5ef76-159">삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef76-159">Delete it.</span></span>
* <span data-ttu-id="5ef76-160">해당 경고에 대한 알림 수신을 일시적으로 중지하거나 다시 시작하려면 사용 안 함 또는 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5ef76-160">Disable or enable it, if you want to temporarily stop or resume receiving notifications for the alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ef76-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5ef76-161">Next steps</span></span>
- <span data-ttu-id="5ef76-162">[서비스 상태 알림](monitoring-service-notifications.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="5ef76-162">Learn about [service health notifications](monitoring-service-notifications.md).</span></span>
- <span data-ttu-id="5ef76-163">[알림 속도 제한](monitoring-alerts-rate-limiting.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="5ef76-163">Learn about [notification rate limiting](monitoring-alerts-rate-limiting.md).</span></span>
- <span data-ttu-id="5ef76-164">[활동 로그 경고 웹후크 스키마](monitoring-activity-log-alerts-webhook.md)를 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="5ef76-164">Review the [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>
- <span data-ttu-id="5ef76-165">[활동 로그 경고의 개요](monitoring-overview-alerts.md)를 확인하고 경고를 받는 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="5ef76-165">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how to receive alerts.</span></span> 
- <span data-ttu-id="5ef76-166">[작업 그룹](monitoring-action-groups.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="5ef76-166">Learn more about [action groups](monitoring-action-groups.md).</span></span>
