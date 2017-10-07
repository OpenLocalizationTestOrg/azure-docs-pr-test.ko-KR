---
title: "서비스 알림 aaaReceive 활동 로그 경고 | Microsoft Docs"
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
ms.openlocfilehash: dd35e8f39d2a522efdae4dfed20779c992c1dd27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-activity-log-alerts-on-service-notifications"></a><span data-ttu-id="e146c-103">서비스 알림에 대한 활동 로그 경고 만들기</span><span class="sxs-lookup"><span data-stu-id="e146c-103">Create activity log alerts on service notifications</span></span>
## <a name="overview"></a><span data-ttu-id="e146c-104">개요</span><span class="sxs-lookup"><span data-stu-id="e146c-104">Overview</span></span>
<span data-ttu-id="e146c-105">이 문서에서는 hello Azure 포털을 사용 하 여 활동 로그를 tooset 서비스 상태 알림에 대 한 경고 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-105">This article shows you how tooset up activity log alerts for service health notifications by using hello Azure portal.</span></span>  

<span data-ttu-id="e146c-106">Azure에서 서비스 상태 알림 tooyour Azure 구독을 보낼 때 경고를 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-106">You can receive an alert when Azure sends service health notifications tooyour Azure subscription.</span></span> <span data-ttu-id="e146c-107">에 기반 하는 hello 경고를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-107">You can configure hello alert based on:</span></span>

- <span data-ttu-id="e146c-108">서비스 상태 알림 (인시던트, 유지 관리, 정보 등)의 hello 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-108">hello class of service health notification (incident, maintenance, information, etc.).</span></span>
- <span data-ttu-id="e146c-109">영향을 받는 hello 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-109">hello service(s) affected.</span></span>
- <span data-ttu-id="e146c-110">영향을 받는 hello 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-110">hello region(s) affected.</span></span>
- <span data-ttu-id="e146c-111">hello 상태 (활성 및 해결) hello 알림입니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-111">hello status of hello notification (active vs. resolved).</span></span>
- <span data-ttu-id="e146c-112">hello 수준의 hello 알림 (정보, 경고, 오류).</span><span class="sxs-lookup"><span data-stu-id="e146c-112">hello level of hello notifications (informational, warning, error).</span></span>

<span data-ttu-id="e146c-113">구성할 수도 있습니다 hello 경고를 보낼 사용자:</span><span class="sxs-lookup"><span data-stu-id="e146c-113">You also can configure who hello alert should be sent to:</span></span>

- <span data-ttu-id="e146c-114">기존 작업 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-114">Select an existing action group.</span></span>
- <span data-ttu-id="e146c-115">새 작업 그룹을 만듭니다(향후 경고에 사용할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="e146c-115">Create a new action group (that can be used for future alerts).</span></span>

<span data-ttu-id="e146c-116">동작 그룹에 대해 자세히 toolearn 참조 [만들기 동작 그룹 및 관리](monitoring-action-groups.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-116">toolearn more about action groups, see [Create and manage action groups](monitoring-action-groups.md).</span></span>

<span data-ttu-id="e146c-117">Azure 리소스 관리자 템플릿을 사용 하 여 tooconfigure 서비스 상태 알림 경고 하는 방법에 대 한 정보를 참조 하십시오. [리소스 관리자 템플릿을](monitoring-create-activity-log-alerts-with-resource-manager-template.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-117">For information on how tooconfigure service health notification alerts by using Azure Resource Manager templates, see [Resource Manager templates](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>

## <a name="create-an-alert-on-a-service-health-notification-for-a-new-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="e146c-118">Hello Azure 포털을 사용 하 여 새 작업 그룹에 대 한 서비스 상태 알림 경고 만들기</span><span class="sxs-lookup"><span data-stu-id="e146c-118">Create an alert on a service health notification for a new action group by using hello Azure portal</span></span>
1. <span data-ttu-id="e146c-119">Hello에 [포털](https://portal.azure.com)선택, **모니터**합니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-119">In hello [portal](https://portal.azure.com), select **Monitor**.</span></span>

    ![hello 서비스 "모니터 임계값"](./media/monitoring-activity-log-alerts-on-service-notifications/home-monitor.png)

2. <span data-ttu-id="e146c-121">Hello에 **활동 로그** 섹션에서 **경고**합니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-121">In hello **Activity log** section, select **Alerts**.</span></span>

    ![hello "경고" 탭](./media/monitoring-activity-log-alerts-on-service-notifications/alerts-blades.png)

3. <span data-ttu-id="e146c-123">선택 **추가 활동 로그 경고**, 고 hello 필드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-123">Select **Add activity log alert**, and fill in hello fields.</span></span>

    ![hello "추가 활동 로그 경고" 명령](./media/monitoring-activity-log-alerts-on-service-notifications/add-activity-log-alert.png)

4. <span data-ttu-id="e146c-125">Hello에 이름을 입력 **활동 로그 경고 이름** 고 제공 된 **설명**합니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-125">Enter a name in hello **Activity log alert name** box, and provide a **Description**.</span></span>

    ![hello "활동 로그 경고 추가" 대화 상자](./media/monitoring-activity-log-alerts-on-service-notifications/activity-log-alert-service-notification-new-action-group.png)

5. <span data-ttu-id="e146c-127">hello **구독** 현재 구독과 autofills 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-127">hello **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="e146c-128">이 구독에 사용 되는 toosave hello 활동 로그 경고입니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-128">This subscription is used toosave hello activity log alert.</span></span> <span data-ttu-id="e146c-129">hello 경고 리소스에 대 한 hello 활동 로그에서 배포 된 toothis 구독 및 모니터 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-129">hello alert resource is deployed toothis subscription and monitors events in hello activity log for it.</span></span>

6. <span data-ttu-id="e146c-130">선택 hello **리소스 그룹** 는 hello 경고 리소스가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-130">Select hello **Resource group** in which hello alert resource is created.</span></span> <span data-ttu-id="e146c-131">이것은 hello 경고에서 모니터링 하는 hello 리소스 그룹 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-131">This isn't hello resource group that's monitored by hello alert.</span></span> <span data-ttu-id="e146c-132">만으로도 hello 경고 리소스 위치한 hello 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-132">Instead, it's hello resource group where hello alert resource is located.</span></span>

7. <span data-ttu-id="e146c-133">Hello에 **이벤트 범주** 상자 **서비스 상태**합니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-133">In hello **Event category** box, select **Service Health**.</span></span> <span data-ttu-id="e146c-134">필요에 따라 hello 선택 **서비스**, **지역**, **형식**, **상태**, 및 **수준** 서비스의 상태 알림 tooreceive 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-134">Optionally, select hello **Service**, **Region**, **Type**, **Status**, and **Level** of service health notifications that you want tooreceive.</span></span>

8. <span data-ttu-id="e146c-135">아래 **를 통해 경고**선택, hello **새로 만들기** 작업 그룹 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-135">Under **Alert via**, select hello **New** action group button.</span></span> <span data-ttu-id="e146c-136">Hello에 이름을 입력 **동작 그룹 이름** hello에 이름을 입력 하 고 상자의 **약식 이름** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-136">Enter a name in hello **Action group name** box, and enter a name in hello **Short name** box.</span></span> <span data-ttu-id="e146c-137">hello 약식 이름은이 경고가 발생할 때 보낸 hello 알림을에서 참조 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-137">hello short name is referenced in hello notifications that are sent when this alert fires.</span></span>

9. <span data-ttu-id="e146c-138">Hello 수신기를 제공 하 여 수신기의 목록을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-138">Define a list of receivers by providing hello receiver's:</span></span>

    <span data-ttu-id="e146c-139">a.</span><span class="sxs-lookup"><span data-stu-id="e146c-139">a.</span></span> <span data-ttu-id="e146c-140">**이름**: hello 수신기의 이름, 별칭 또는 식별자를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-140">**Name**: Enter hello receiver’s name, alias, or identifier.</span></span>

    <span data-ttu-id="e146c-141">b.</span><span class="sxs-lookup"><span data-stu-id="e146c-141">b.</span></span> <span data-ttu-id="e146c-142">**작업 유형**: SMS, 전자 메일 또는 웹후크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-142">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="e146c-143">c.</span><span class="sxs-lookup"><span data-stu-id="e146c-143">c.</span></span> <span data-ttu-id="e146c-144">**세부 정보**: 전화 번호, 전자 메일 주소 또는 URI webhook 입력 선택 hello 동작 형식을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-144">**Details**: Based on hello action type chosen, enter a phone number, email address, or webhook URI.</span></span>

10. <span data-ttu-id="e146c-145">선택 **확인** toocreate hello 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-145">Select **OK** toocreate hello alert.</span></span>

<span data-ttu-id="e146c-146">몇 분 안에 hello 경고가 활성 이며 tootrigger를 만들 때 지정한 hello 조건에 따라 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-146">Within a few minutes, hello alert is active and begins tootrigger based on hello conditions you specified during creation.</span></span>

<span data-ttu-id="e146c-147">활동 로그 경고에 대 한 webhook 스키마 hello에 대 한 자세한 내용은 참조 하십시오. [Webhook에 대 한 Azure 활동 로그 경고](monitoring-activity-log-alerts-webhook.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-147">For information on hello webhook schema for activity log alerts, see [Webhooks for Azure activity log alerts](monitoring-activity-log-alerts-webhook.md).</span></span>

>[!NOTE]
><span data-ttu-id="e146c-148">다음이 단계에 정의 된 hello 동작 그룹은 모든 이후 경고 정의 대 한 기존 작업 그룹으로 다시 사용할 수 있는입니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-148">hello action group defined in these steps is reusable as an existing action group for all future alert definitions.</span></span>
>
>

## <a name="create-an-alert-on-a-service-health-notification-for-an-existing-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="e146c-149">Hello Azure 포털을 사용 하 여 기존 작업 그룹에 대 한 서비스 상태 알림 경고 만들기</span><span class="sxs-lookup"><span data-stu-id="e146c-149">Create an alert on a service health notification for an existing action group by using hello Azure portal</span></span>

1. <span data-ttu-id="e146c-150">서비스 상태 알림-7 이전 섹션 toocreate hello에에서 1 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-150">Follow steps 1 through 7 in hello previous section toocreate your service health notification.</span></span> 

2. <span data-ttu-id="e146c-151">아래 **를 통해 경고**선택, hello **기존** 작업 그룹 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-151">Under **Alert via**, select hello **Existing** action group button.</span></span> <span data-ttu-id="e146c-152">Hello 적절 한 작업 그룹을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-152">Select hello appropriate action group.</span></span>

3. <span data-ttu-id="e146c-153">선택 **확인** toocreate hello 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-153">Select **OK** toocreate hello alert.</span></span>

<span data-ttu-id="e146c-154">몇 분 안에 hello 경고가 활성 이며 tootrigger를 만들 때 지정한 hello 조건에 따라 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-154">Within a few minutes, hello alert is active and begins tootrigger based on hello conditions you specified during creation.</span></span>

## <a name="manage-your-alerts"></a><span data-ttu-id="e146c-155">경고 관리</span><span class="sxs-lookup"><span data-stu-id="e146c-155">Manage your alerts</span></span>

<span data-ttu-id="e146c-156">Hello에 표시 되는 경고를 만든 후 **경고** hello 섹션 **모니터** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-156">After you create an alert, it's visible in hello **Alerts** section of hello **Monitor** blade.</span></span> <span data-ttu-id="e146c-157">toomanage hello 경고를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-157">Select hello alert you want toomanage to:</span></span>

* <span data-ttu-id="e146c-158">편집합니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-158">Edit it.</span></span>
* <span data-ttu-id="e146c-159">삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-159">Delete it.</span></span>
* <span data-ttu-id="e146c-160">또는 tootemporarily 중지 하거나 재개 hello 경고에 대 한 알림을 수신 하는 경우, 사용 안 함.</span><span class="sxs-lookup"><span data-stu-id="e146c-160">Disable or enable it, if you want tootemporarily stop or resume receiving notifications for hello alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e146c-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e146c-161">Next steps</span></span>
- <span data-ttu-id="e146c-162">[서비스 상태 알림](monitoring-service-notifications.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="e146c-162">Learn about [service health notifications](monitoring-service-notifications.md).</span></span>
- <span data-ttu-id="e146c-163">[알림 속도 제한](monitoring-alerts-rate-limiting.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="e146c-163">Learn about [notification rate limiting](monitoring-alerts-rate-limiting.md).</span></span>
- <span data-ttu-id="e146c-164">검토 hello [활동 로그 경고 webhook 스키마](monitoring-activity-log-alerts-webhook.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-164">Review hello [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>
- <span data-ttu-id="e146c-165">가져오기는 [활동 로그 경고의 개요](monitoring-overview-alerts.md), 알아봅니다 어떻게 tooreceive 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e146c-165">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how tooreceive alerts.</span></span> 
- <span data-ttu-id="e146c-166">[작업 그룹](monitoring-action-groups.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="e146c-166">Learn more about [action groups](monitoring-action-groups.md).</span></span>
