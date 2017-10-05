---
title: "활동 로그 경고 만들기 | Microsoft Docs"
description: "활동 로그에서 특정 이벤트가 발생하면 SMS, 웹후크 및 전자 메일을 통해 알림을 받습니다."
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
ms.date: 08/03/2017
ms.author: johnkem
ms.openlocfilehash: 3885469ec0e1fcc31386dd0ad7fe6cb5d03ab28e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-activity-log-alerts"></a><span data-ttu-id="b67c8-103">활동 로그 경고 만들기</span><span class="sxs-lookup"><span data-stu-id="b67c8-103">Create activity log alerts</span></span>

## <a name="overview"></a><span data-ttu-id="b67c8-104">개요</span><span class="sxs-lookup"><span data-stu-id="b67c8-104">Overview</span></span>
<span data-ttu-id="b67c8-105">활동 로그 경고는 경고에 지정된 조건과 일치하는 새 활동 로그 이벤트가 발생한 경우에 활성화되는 경고입니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-105">Activity log alerts are alerts that activate when a new activity log event occurs that matches the conditions specified in the alert.</span></span> <span data-ttu-id="b67c8-106">이는 Azure 리소스이므로 Azure 리소스 관리자 템플릿을 사용하여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-106">They are Azure resources, so they can be created by using an Azure Resource Manager template.</span></span> <span data-ttu-id="b67c8-107">또한 Azure Portal에서 생성, 업데이트 또는 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-107">They also can be created, updated, or deleted in the Azure portal.</span></span> <span data-ttu-id="b67c8-108">이 문서에서는 활동 로그 경고에 대한 개념을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-108">This article introduces the concepts behind activity log alerts.</span></span> <span data-ttu-id="b67c8-109">그런 다음 Azure Portal을 사용하여 활동 로그 이벤트에 대한 경고를 설정하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-109">It then shows you how to use the Azure portal to set up an alert on activity log events.</span></span>

<span data-ttu-id="b67c8-110">일반적으로 다음과 같은 경우에 알림을 수신하도록 활동 로그 경고를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-110">Typically, you create activity log alerts to receive notifications when:</span></span>

* <span data-ttu-id="b67c8-111">Azure 구독의 리소스에서 특정 변경이 발생하는 경우. 특정 리소스 그룹 또는 리소스로 범위를 지정하기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-111">Specific changes occur on resources in your Azure subscription, often scoped to particular resource groups or resources.</span></span> <span data-ttu-id="b67c8-112">예를 들어 myProductionResourceGroup에서 가상 컴퓨터가 삭제되는 경우 알림을 받도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-112">For example, you might want to be notified when any virtual machine in myProductionResourceGroup is deleted.</span></span> <span data-ttu-id="b67c8-113">또는 새 규칙이 사용자 구독의 사용자에 할당되는 경우 알림을 받도록 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-113">Or, you might want to be notified if any new roles are assigned to a user in your subscription.</span></span>
* <span data-ttu-id="b67c8-114">서비스 상태 이벤트가 발생하는 경우.</span><span class="sxs-lookup"><span data-stu-id="b67c8-114">A service health event occurs.</span></span> <span data-ttu-id="b67c8-115">서비스 상태 이벤트가 구독에서 리소스에 적용되는 인시던트 및 유지 관리 이벤트의 알림을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-115">Service health events include notification of incidents and maintenance events that apply to resources in your subscription.</span></span>

<span data-ttu-id="b67c8-116">두 경우 모두 활동 로그 경고는 경고가 생성되는 구독의 이벤트만 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-116">In either case, an activity log alert monitors only for events in the subscription in which the alert is created.</span></span>

<span data-ttu-id="b67c8-117">활동 로그 이벤트에 대한 JSON 개체의 모든 최상위 속성에 따라 활동 로그 경고를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-117">You can configure an activity log alert based on any top-level property in the JSON object for an activity log event.</span></span> <span data-ttu-id="b67c8-118">그러나 포털에는 가장 일반적인 옵션만 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-118">However, the portal shows the most common options:</span></span>

- <span data-ttu-id="b67c8-119">**범주**: 관리, 서비스 상태, 자동 크기 조정 및 권장 사항 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-119">**Category**: Administrative, Service Health, Autoscale, and Recommendation.</span></span> <span data-ttu-id="b67c8-120">자세한 내용은 [Azure 활동 로그 개요](./monitoring-overview-activity-logs.md#categories-in-the-activity-log)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b67c8-120">For more information, see [Overview of the Azure activity log](./monitoring-overview-activity-logs.md#categories-in-the-activity-log).</span></span> <span data-ttu-id="b67c8-121">서비스 상태 이벤트에 대한 자세한 내용은 [서비스 알림에서 활동 로그 경고 수신](./monitoring-activity-log-alerts-on-service-notifications.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b67c8-121">To learn more about service health events, see [Receive activity log alerts on service notifications](./monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
- <span data-ttu-id="b67c8-122">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="b67c8-122">**Resource group**</span></span>
- <span data-ttu-id="b67c8-123">**리소스**</span><span class="sxs-lookup"><span data-stu-id="b67c8-123">**Resource**</span></span>
- <span data-ttu-id="b67c8-124">**리소스 종류**</span><span class="sxs-lookup"><span data-stu-id="b67c8-124">**Resource type**</span></span>
- <span data-ttu-id="b67c8-125">**작업 이름**: 리소스 관리자 역할 기반 액세스 제어 작업 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-125">**Operation name**: The Resource Manager Role-Based Access Control operation name.</span></span>
- <span data-ttu-id="b67c8-126">**수준**: 이벤트의 심각도 수준(자세한 정보, 정보, 경고, 오류 또는 중요)입니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-126">**Level**: The severity level of the event (Verbose, Informational, Warning, Error, or Critical).</span></span>
- <span data-ttu-id="b67c8-127">**상태**: 이벤트의 상태로, 일반적으로 시작됨, 실패 또는 성공입니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-127">**Status**: The status of the event, typically Started, Failed, or Succeeded.</span></span>
- <span data-ttu-id="b67c8-128">**이벤트를 시작한 사람**: “호출자”로 알려져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-128">**Event initiated by**: Also known as the "caller."</span></span> <span data-ttu-id="b67c8-129">작업을 수행한 사용자의 이메일 주소 또는 Active Directory 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-129">The email address or Azure Active Directory identifier of the user who performed the operation.</span></span>

>[!NOTE]
><span data-ttu-id="b67c8-130">경고에서 앞에 나온 조건 중 둘 이상을 지정해야 하며, 하나는 범주에 해당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-130">You must specify at least two of the preceding criteria in your alert, with one being the category.</span></span> <span data-ttu-id="b67c8-131">활동 로그에서 이벤트가 생성될 때마다 활성화되는 경고를 만들 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-131">You may not create an alert that activates every time an event is created in the activity logs.</span></span>
>
>

<span data-ttu-id="b67c8-132">활동 로그 경고가 활성화되면 작업 그룹을 사용하여 작업 또는 알림을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-132">When an activity log alert is activated, it uses an action group to generate actions or notifications.</span></span> <span data-ttu-id="b67c8-133">작업 그룹은 이메일 주소, 웹후크 URL 또는 SMS 전화 번호와 같은 알림 수신자의 재사용 가능한 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-133">An action group is a reusable set of notification receivers, such as email addresses, webhook URLs, or SMS phone numbers.</span></span> <span data-ttu-id="b67c8-134">수신자를 여러 경고에서 참조하여 알림 채널을 집중화하고 그룹화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-134">The receivers can be referenced from multiple alerts to centralize and group your notification channels.</span></span> <span data-ttu-id="b67c8-135">활동 로그 경고를 정의하는 경우 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-135">When you define your activity log alert, you have two options.</span></span> <span data-ttu-id="b67c8-136">다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-136">You can:</span></span>

* <span data-ttu-id="b67c8-137">활동 로그 경고에서 기존 작업 그룹을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-137">Use an existing action group in your activity log alert.</span></span> 
* <span data-ttu-id="b67c8-138">새 작업 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-138">Create a new action group.</span></span> 

<span data-ttu-id="b67c8-139">작업 그룹에 대해 자세히 알아보려면 [Azure Portal에서 작업 그룹 만들기 및 관리](monitoring-action-groups.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b67c8-139">To learn more about action groups, see [Create and manage action groups in the Azure portal](monitoring-action-groups.md).</span></span>

<span data-ttu-id="b67c8-140">서비스 상태 알림에 대해 자세히 알아보려면 [서비스 상태 알림에서 활동 로그 경고 수신](monitoring-activity-log-alerts-on-service-notifications.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b67c8-140">To learn more about service health notifications, see [Receive activity log alerts on service health notifications](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>

## <a name="create-an-alert-on-an-activity-log-event-with-a-new-action-group-by-using-the-azure-portal"></a><span data-ttu-id="b67c8-141">Azure Portal을 사용하여 새 작업 그룹의 활동 로그 이벤트에 대한 경고 만들기</span><span class="sxs-lookup"><span data-stu-id="b67c8-141">Create an alert on an activity log event with a new action group by using the Azure portal</span></span>
1. <span data-ttu-id="b67c8-142">[포털](https://portal.azure.com)에서 **모니터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-142">In the [portal](https://portal.azure.com), select **Monitor**.</span></span>

    ![“모니터링” 서비스](./media/monitoring-activity-log-alerts/home-monitor.png)
2. <span data-ttu-id="b67c8-144">**활동 로그** 섹션에서 **경고**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-144">In the **Activity log** section, select **Alerts**.</span></span>

    ![“경고” 탭](./media/monitoring-activity-log-alerts/alerts-blades.png)
3. <span data-ttu-id="b67c8-146">**활동 로그 경고 추가**를 선택하고 필드를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-146">Select **Add activity log alert**, and fill in the fields.</span></span>

4. <span data-ttu-id="b67c8-147">**활동 로그 경고 이름** 상자에 이름을 입력하고 **설명**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-147">Enter a name in the **Activity log alert name** box, and select a **Description**.</span></span>

    ![“활동 로그 경고 추가” 명령](./media/monitoring-activity-log-alerts/add-activity-log-alert.png)

5. <span data-ttu-id="b67c8-149">**구독** 상자가 현재 구독으로 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-149">The **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="b67c8-150">이 구독은 작업 그룹이 저장되는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-150">This subscription is the one in which the action group is saved.</span></span> <span data-ttu-id="b67c8-151">이는 경고 리소스를 배포하고 활동 로그 이벤트를 모니터링하는 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-151">The alert resource is deployed to this subscription and monitors activity log events from it.</span></span>

    ![“활동 로그 경고 추가” 대화 상자](./media/monitoring-activity-log-alerts/activity-log-alert-new-action-group.png)

6. <span data-ttu-id="b67c8-153">경고 리소스가 만들어지는 **리소스 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-153">Select the **Resource group** in which the alert resource is created.</span></span> <span data-ttu-id="b67c8-154">이는 경고에 의해 모니터링되는 리소스 그룹이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-154">This is not the resource group that's monitored by the alert.</span></span> <span data-ttu-id="b67c8-155">대신 경고 리소스가 있는 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-155">Instead, it's the resource group where the alert resource is located.</span></span>

7. <span data-ttu-id="b67c8-156">필요에 따라 표시된 추가 필터를 수정하는 **이벤트 범주**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-156">Optionally, select an **Event category** to modify the additional filters that are shown.</span></span> <span data-ttu-id="b67c8-157">관리 이벤트의 경우 필터는 **리소스 그룹**, **리소스**, **리소스 종류**, **작업 이름**, **수준**, **상태** 및 **이벤트를 시작한 사람**을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-157">For Administrative events, the filters include **Resource group**, **Resource**, **Resource type**, **Operation name**, **Level**, **Status**, and **Event initiated by**.</span></span> <span data-ttu-id="b67c8-158">이러한 값이 이 경고가 모니터링해야 하는 이벤트를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-158">These values identify which events this alert should monitor.</span></span>

    >[!NOTE]
    ><span data-ttu-id="b67c8-159">경고에 앞에 나온 조건 중 하나 이상을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-159">You must specify at least one of the preceding criteria in your alert.</span></span> <span data-ttu-id="b67c8-160">활동 로그에서 이벤트가 생성될 때마다 활성화되는 경고를 만들 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-160">You may not create an alert that activates every time an event is created in the activity logs.</span></span>
    >
    >

8. <span data-ttu-id="b67c8-161">**작업 그룹 이름** 상자에 이름을 입력하고 **약식 이름** 상자에 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-161">Enter a name in the **Action group name** box, and enter a name in the **Short name** box.</span></span> <span data-ttu-id="b67c8-162">약식 이름은 이 그룹을 사용하여 알림을 보내는 경우 전체 작업 그룹 이름 대신 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-162">The short name is used in place of a full action group name when notifications are sent using this group.</span></span>

9.  <span data-ttu-id="b67c8-163">작업에 대해 다음 정보를 제공하여 작업 목록을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-163">Define a list of actions by providing the action’s:</span></span>

    <span data-ttu-id="b67c8-164">a.</span><span class="sxs-lookup"><span data-stu-id="b67c8-164">a.</span></span> <span data-ttu-id="b67c8-165">**이름**: 작업의 이름, 별칭 또는 식별자를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-165">**Name**: Enter the action’s name, alias, or identifier.</span></span>

    <span data-ttu-id="b67c8-166">b.</span><span class="sxs-lookup"><span data-stu-id="b67c8-166">b.</span></span> <span data-ttu-id="b67c8-167">**작업 유형**: SMS, 전자 메일 또는 웹후크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-167">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="b67c8-168">c.</span><span class="sxs-lookup"><span data-stu-id="b67c8-168">c.</span></span> <span data-ttu-id="b67c8-169">**세부 정보**: 작업 유형에 따라 전화 번호, 이메일 주소 또는 웹후크 URI를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-169">**Details**: Based on the action type, enter a phone number, email address, or webhook URI.</span></span>

10. <span data-ttu-id="b67c8-170">**확인**을 선택하여 경고를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-170">Select **OK** to create the alert.</span></span>

<span data-ttu-id="b67c8-171">경고가 완벽하게 전파되고 활성화되는 데에는 몇 분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-171">The alert takes a few minutes to fully propagate and then become active.</span></span> <span data-ttu-id="b67c8-172">새 이벤트가 경고의 조건과 일치하는 경우 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-172">It triggers when new events match the alert's criteria.</span></span>

<span data-ttu-id="b67c8-173">자세한 내용은 [활동 로그 경고에 사용된 웹후크 스키마 이해](monitoring-activity-log-alerts-webhook.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b67c8-173">For more information, see [Understand the webhook schema used in activity log alerts](monitoring-activity-log-alerts-webhook.md).</span></span>

>[!NOTE]
><span data-ttu-id="b67c8-174">이러한 단계에서 정의한 작업 그룹은 향후의 모든 경고 정의에 대해 기존 작업 그룹으로 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-174">The action group defined in these steps is reusable as an existing action group for all future alert definitions.</span></span>
>
>

## <a name="create-an-alert-on-an-activity-log-event-for-an-existing-action-group-by-using-the-azure-portal"></a><span data-ttu-id="b67c8-175">Azure Portal을 사용하여 기존 작업 그룹의 활동 로그 이벤트에 대한 경고 만들기</span><span class="sxs-lookup"><span data-stu-id="b67c8-175">Create an alert on an activity log event for an existing action group by using the Azure portal</span></span>
1. <span data-ttu-id="b67c8-176">이전 섹션의 1-7단계를 수행하여 활동 로그 경고를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-176">Follow steps 1 through 7 in the previous section to create your activity log alert.</span></span>

2. <span data-ttu-id="b67c8-177">**다음을 통해 알림**에서 **기존** 작업 그룹 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-177">Under **Notify via**, select the **Existing** action group button.</span></span> <span data-ttu-id="b67c8-178">목록에서 기존 작업 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-178">Select an existing action group from the list.</span></span>

3. <span data-ttu-id="b67c8-179">**확인**을 선택하여 경고를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-179">Select **OK** to create the alert.</span></span>

<span data-ttu-id="b67c8-180">경고가 완벽하게 전파되고 활성화되는 데에는 몇 분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-180">The alert takes a few minutes to fully propagate and then become active.</span></span> <span data-ttu-id="b67c8-181">새 이벤트가 경고의 조건과 일치하는 경우 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-181">It triggers when new events match the alert's criteria.</span></span>

## <a name="manage-your-alerts"></a><span data-ttu-id="b67c8-182">경고 관리</span><span class="sxs-lookup"><span data-stu-id="b67c8-182">Manage your alerts</span></span>

<span data-ttu-id="b67c8-183">경고를 만들면 모니터 블레이드의 경고 섹션에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-183">After you create an alert, it's visible in the Alerts section of the Monitor blade.</span></span> <span data-ttu-id="b67c8-184">관리하려는 경고를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-184">Select the alert you want to manage to:</span></span>

* <span data-ttu-id="b67c8-185">편집합니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-185">Edit it.</span></span>
* <span data-ttu-id="b67c8-186">삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-186">Delete it.</span></span>
* <span data-ttu-id="b67c8-187">해당 경고에 대한 알림 수신을 일시적으로 중지하거나 다시 시작하려면 사용 안 함 또는 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-187">Disable or enable it, if you want to temporarily stop or resume receiving notifications for the alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b67c8-188">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b67c8-188">Next steps</span></span>
- <span data-ttu-id="b67c8-189">[경고 개요](monitoring-overview-alerts.md)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="b67c8-189">Get an [overview of alerts](monitoring-overview-alerts.md).</span></span>
- <span data-ttu-id="b67c8-190">[알림 속도 제한](monitoring-alerts-rate-limiting.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="b67c8-190">Learn about [notification rate limiting](monitoring-alerts-rate-limiting.md).</span></span>
- <span data-ttu-id="b67c8-191">[활동 로그 경고 웹후크 스키마](monitoring-activity-log-alerts-webhook.md)를 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="b67c8-191">Review the [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>
- <span data-ttu-id="b67c8-192">[작업 그룹](monitoring-action-groups.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="b67c8-192">Learn more about [action groups](monitoring-action-groups.md).</span></span>  
- <span data-ttu-id="b67c8-193">[서비스 상태 알림](monitoring-service-notifications.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="b67c8-193">Learn about [service health notifications](monitoring-service-notifications.md).</span></span>
- <span data-ttu-id="b67c8-194">[구독의 모든 자동 크기 조정 엔진 작업을 모니터링하기 위한 활동 로그 경고](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-194">Create an [activity log alert to monitor all autoscale engine operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span></span>
- <span data-ttu-id="b67c8-195">[구독에서 실패한 모든 자동 크기 조정 규모 감축/규모 확장 작업을 모니터링하기 위한 활동 로그 경고](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b67c8-195">Create an [activity log alert to monitor all failed autoscale scale-in/scale-out operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span></span>
