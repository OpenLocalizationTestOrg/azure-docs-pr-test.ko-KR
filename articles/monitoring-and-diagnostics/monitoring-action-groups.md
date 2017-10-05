---
title: "Azure Portal에서 작업 그룹 만들기 및 관리 | Microsoft Docs"
description: "Azure Portal에서 작업 그룹을 만들고 관리하는 방법에 대해 알아봅니다."
author: anirudhcavale
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
ms.date: 05/15/2017
ms.author: ancav
ms.openlocfilehash: ea15705bf02d9773507c6cb59f2da4c1dd0f9d77
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-action-groups-in-the-azure-portal"></a><span data-ttu-id="a8b00-103">Azure Portal에서 작업 그룹 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="a8b00-103">Create and manage action groups in the Azure portal</span></span>
## <a name="overview"></a><span data-ttu-id="a8b00-104">개요</span><span class="sxs-lookup"><span data-stu-id="a8b00-104">Overview</span></span> ##
<span data-ttu-id="a8b00-105">이 문서에서는 Azure Portal에서 작업 그룹을 만들고 관리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a8b00-105">This article shows you how to create and manage action groups in the Azure portal.</span></span>

<span data-ttu-id="a8b00-106">작업 그룹을 사용하여 작업 목록을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8b00-106">You can configure a list of actions with action groups.</span></span> <span data-ttu-id="a8b00-107">그런 다음 이러한 그룹을 활동 로그 경고를 정의할 때 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8b00-107">These groups then can be used when you define activity log alerts.</span></span> <span data-ttu-id="a8b00-108">이러한 그룹은 사용자가 정의한 각 활동 로그 경고에서 다시 사용할 수 있습니다. 이를 통해 활동 로그 경고가 트리거될 때마다 동일한 작업이 수행되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b00-108">These groups can then be reused by each activity log alert you define, ensuring that the same actions are taken each time the activity log alert is triggered.</span></span>

<span data-ttu-id="a8b00-109">하나의 작업 그룹에는 각 작업 유형이 최대 10개 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8b00-109">An action group can have up to 10 of each action type.</span></span> <span data-ttu-id="a8b00-110">각 작업은 다음과 같은 속성으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8b00-110">Each action is made up of the following properties:</span></span>

* <span data-ttu-id="a8b00-111">**이름**: 작업 그룹 내의 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="a8b00-111">**Name**: A unique identifier within the action group.</span></span>  
* <span data-ttu-id="a8b00-112">**작업 유형**: SMS를 보내거나, 전자 메일을 보내거나, 웹후크를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b00-112">**Action type**: Send an SMS, send an email, or call a webhook.</span></span>  
* <span data-ttu-id="a8b00-113">**세부 정보**: 해당 전화 번호, 이메일 주소 또는 웹후크 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="a8b00-113">**Details**: The corresponding phone number, email address, or webhook URI.</span></span>

<span data-ttu-id="a8b00-114">Azure 리소스 관리자 템플릿을 사용하여 작업 그룹을 구성하는 방법에 대한 자세한 내용은 [작업 그룹 리소스 관리자 템플릿](monitoring-create-action-group-with-resource-manager-template.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8b00-114">For information on how to use Azure Resource Manager templates to configure action groups, see [Action group Resource Manager templates](monitoring-create-action-group-with-resource-manager-template.md).</span></span>

## <a name="create-an-action-group-by-using-the-azure-portal"></a><span data-ttu-id="a8b00-115">Azure Portal을 사용하여 작업 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="a8b00-115">Create an action group by using the Azure portal</span></span> ##
1. <span data-ttu-id="a8b00-116">[포털](https://portal.azure.com)에서 **모니터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b00-116">In the [portal](https://portal.azure.com), select **Monitor**.</span></span> <span data-ttu-id="a8b00-117">**모니터** 블레이드는 모든 모니터링 설정 및 데이터를 하나의 뷰에 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b00-117">The **Monitor** blade consolidates all your monitoring settings and data in one view.</span></span>

    ![“모니터링” 서비스](./media/monitoring-action-groups/home-monitor.png)
2. <span data-ttu-id="a8b00-119">**활동 로그** 섹션에서 **작업 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b00-119">In the **Activity log** section, select **Action groups**.</span></span>

    ![“작업 그룹” 탭](./media/monitoring-action-groups/action-groups-blade.png)
3. <span data-ttu-id="a8b00-121">**작업 그룹 추가**를 선택하고 필드를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b00-121">Select **Add action group**, and fill in the fields.</span></span>

    ![“작업 그룹 추가” 명령](./media/monitoring-action-groups/add-action-group.png)
4. <span data-ttu-id="a8b00-123">**작업 그룹 이름** 상자에 이름을 입력하고 **약식 이름** 상자에 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b00-123">Enter a name in the **Action group name** box, and enter a name in the **Short name** box.</span></span> <span data-ttu-id="a8b00-124">약식 이름은 이 그룹을 사용하여 알림을 보내는 경우 전체 작업 그룹 이름 대신 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8b00-124">The short name is used in place of a full action group name when notifications are sent using this group.</span></span>

      ![“작업 그룹 추가” 대화 상자](./media/monitoring-action-groups/action-group-define.png)

5. <span data-ttu-id="a8b00-126">**구독** 상자가 현재 구독으로 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="a8b00-126">The **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="a8b00-127">이 구독은 작업 그룹이 저장되는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="a8b00-127">This subscription is the one in which the action group is saved.</span></span>

6. <span data-ttu-id="a8b00-128">작업 그룹이 저장되는 **리소스 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b00-128">Select the **Resource group** in which the action group is saved.</span></span>

7. <span data-ttu-id="a8b00-129">각 작업에 대해 다음 정보를 제공하여 작업 목록을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b00-129">Define a list of actions by providing each action's:</span></span>

    <span data-ttu-id="a8b00-130">a.</span><span class="sxs-lookup"><span data-stu-id="a8b00-130">a.</span></span> <span data-ttu-id="a8b00-131">**이름**: 이 작업에 대한 고유 식별자를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b00-131">**Name**: Enter a unique identifier for this action.</span></span>

    <span data-ttu-id="a8b00-132">b.</span><span class="sxs-lookup"><span data-stu-id="a8b00-132">b.</span></span> <span data-ttu-id="a8b00-133">**작업 유형**: SMS, 전자 메일 또는 웹후크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b00-133">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="a8b00-134">c.</span><span class="sxs-lookup"><span data-stu-id="a8b00-134">c.</span></span> <span data-ttu-id="a8b00-135">**세부 정보**: 작업 유형에 따라 전화 번호, 이메일 주소 또는 웹후크 URI를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b00-135">**Details**: Based on the action type, enter a phone number, email address, or webhook URI.</span></span>

8. <span data-ttu-id="a8b00-136">**확인**을 선택하여 작업 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a8b00-136">Select **OK** to create the action group.</span></span>

## <a name="manage-your-action-groups"></a><span data-ttu-id="a8b00-137">작업 그룹 관리</span><span class="sxs-lookup"><span data-stu-id="a8b00-137">Manage your action groups</span></span> ##
<span data-ttu-id="a8b00-138">작업 그룹을 만들면 **모니터** 블레이드의 **작업 그룹** 섹션에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8b00-138">After you create an action group, it's visible in the **Action groups** section of the **Monitor** blade.</span></span> <span data-ttu-id="a8b00-139">관리하려는 작업 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b00-139">Select the action group you want to manage to:</span></span>

* <span data-ttu-id="a8b00-140">작업을 추가, 편집 또는 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b00-140">Add, edit, or remove actions.</span></span>
* <span data-ttu-id="a8b00-141">작업 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b00-141">Delete the action group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8b00-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a8b00-142">Next steps</span></span> ##
* <span data-ttu-id="a8b00-143">[SMS 경고 동작](monitoring-sms-alert-behavior.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="a8b00-143">Learn more about [SMS alert behavior](monitoring-sms-alert-behavior.md).</span></span>  
* <span data-ttu-id="a8b00-144">[활동 로그 경고 웹후크 스키마의 이해](monitoring-activity-log-alerts-webhook.md)를 확인해 보세요.</span><span class="sxs-lookup"><span data-stu-id="a8b00-144">Gain an [understanding of the activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>  
* <span data-ttu-id="a8b00-145">경고의 [속도 제한](monitoring-alerts-rate-limiting.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="a8b00-145">Learn more about [rate limiting](monitoring-alerts-rate-limiting.md) on alerts.</span></span> 
* <span data-ttu-id="a8b00-146">[활동 로그 경고의 개요](monitoring-overview-alerts.md)를 확인하고 경고를 받는 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="a8b00-146">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how to receive alerts.</span></span>  
* <span data-ttu-id="a8b00-147">[서비스 상태 알림이 게시될 때마다 경고를 구성](monitoring-activity-log-alerts-on-service-notifications.md)하는 방법을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="a8b00-147">Learn how to [configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
