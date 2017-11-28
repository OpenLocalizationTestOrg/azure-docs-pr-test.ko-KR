---
title: "aaaCreate hello Azure 포털에서에서 작업 그룹 및 관리 | Microsoft Docs"
description: "자세한 내용은 방법 toocreate hello Azure 포털에서에서 작업 그룹 및 관리 합니다."
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
ms.openlocfilehash: 97e0b22bea7787fff6856f895a7e6256c177efd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-action-groups-in-hello-azure-portal"></a><span data-ttu-id="7db22-103">Hello Azure 포털에서에서 작업 그룹 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="7db22-103">Create and manage action groups in hello Azure portal</span></span>
## <a name="overview"></a><span data-ttu-id="7db22-104">개요</span><span class="sxs-lookup"><span data-stu-id="7db22-104">Overview</span></span> ##
<span data-ttu-id="7db22-105">이 문서에서는 어떻게 toocreate hello Azure 포털에서에서 작업 그룹 및 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="7db22-105">This article shows you how toocreate and manage action groups in hello Azure portal.</span></span>

<span data-ttu-id="7db22-106">작업 그룹을 사용하여 작업 목록을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7db22-106">You can configure a list of actions with action groups.</span></span> <span data-ttu-id="7db22-107">그런 다음 이러한 그룹을 활동 로그 경고를 정의할 때 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7db22-107">These groups then can be used when you define activity log alerts.</span></span> <span data-ttu-id="7db22-108">이러한 그룹을 동일한 조치 hello 활동 로그 경고가 트리거될 때마다 해당 hello 보장 정의한 각 활동 로그 경고 하 여 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7db22-108">These groups can then be reused by each activity log alert you define, ensuring that hello same actions are taken each time hello activity log alert is triggered.</span></span>

<span data-ttu-id="7db22-109">작업 그룹의 각 작업 유형에 too10를 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7db22-109">An action group can have up too10 of each action type.</span></span> <span data-ttu-id="7db22-110">각 작업은 다음과 같은 속성 hello 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7db22-110">Each action is made up of hello following properties:</span></span>

* <span data-ttu-id="7db22-111">**이름**: hello 작업 그룹 내에서 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="7db22-111">**Name**: A unique identifier within hello action group.</span></span>  
* <span data-ttu-id="7db22-112">**작업 유형**: SMS를 보내거나, 전자 메일을 보내거나, 웹후크를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="7db22-112">**Action type**: Send an SMS, send an email, or call a webhook.</span></span>  
* <span data-ttu-id="7db22-113">**세부 정보**: 해당 전화 번호, 전자 메일 주소 또는 URI webhook hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="7db22-113">**Details**: hello corresponding phone number, email address, or webhook URI.</span></span>

<span data-ttu-id="7db22-114">방법에 대 한 내용은 toouse Azure 리소스 관리자 템플릿 tooconfigure 동작 그룹 참조 [액션 그룹 리소스 관리자 템플릿](monitoring-create-action-group-with-resource-manager-template.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7db22-114">For information on how toouse Azure Resource Manager templates tooconfigure action groups, see [Action group Resource Manager templates](monitoring-create-action-group-with-resource-manager-template.md).</span></span>

## <a name="create-an-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="7db22-115">Hello Azure 포털을 사용 하 여 작업 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="7db22-115">Create an action group by using hello Azure portal</span></span> ##
1. <span data-ttu-id="7db22-116">Hello에 [포털](https://portal.azure.com)선택, **모니터**합니다.</span><span class="sxs-lookup"><span data-stu-id="7db22-116">In hello [portal](https://portal.azure.com), select **Monitor**.</span></span> <span data-ttu-id="7db22-117">hello **모니터** 블레이드 모든 모니터링 설정 및 하나의 뷰에 데이터를 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="7db22-117">hello **Monitor** blade consolidates all your monitoring settings and data in one view.</span></span>

    ![hello 서비스 "모니터 임계값"](./media/monitoring-action-groups/home-monitor.png)
2. <span data-ttu-id="7db22-119">Hello에 **활동 로그** 섹션에서 **동작 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="7db22-119">In hello **Activity log** section, select **Action groups**.</span></span>

    ![hello "작업 그룹" 탭](./media/monitoring-action-groups/action-groups-blade.png)
3. <span data-ttu-id="7db22-121">선택 **작업 그룹 추가**, 고 hello 필드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7db22-121">Select **Add action group**, and fill in hello fields.</span></span>

    ![hello "작업 그룹 추가" 명령](./media/monitoring-action-groups/add-action-group.png)
4. <span data-ttu-id="7db22-123">Hello에 이름을 입력 **동작 그룹 이름** hello에 이름을 입력 하 고 상자의 **약식 이름** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="7db22-123">Enter a name in hello **Action group name** box, and enter a name in hello **Short name** box.</span></span> <span data-ttu-id="7db22-124">hello 약식 이름은이 그룹을 사용 하 여 알림을 보내는 경우 전체 동작 그룹 이름 대신 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7db22-124">hello short name is used in place of a full action group name when notifications are sent using this group.</span></span>

      ![작업 그룹을 추가 하는 hello"대화 상자](./media/monitoring-action-groups/action-group-define.png)

5. <span data-ttu-id="7db22-126">hello **구독** 현재 구독과 autofills 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="7db22-126">hello **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="7db22-127">이 구독 하나 hello 저장 되는 hello 동작 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="7db22-127">This subscription is hello one in which hello action group is saved.</span></span>

6. <span data-ttu-id="7db22-128">선택 hello **리소스 그룹** hello 작업 그룹 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7db22-128">Select hello **Resource group** in which hello action group is saved.</span></span>

7. <span data-ttu-id="7db22-129">각 작업에 대해 다음 정보를 제공하여 작업 목록을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7db22-129">Define a list of actions by providing each action's:</span></span>

    <span data-ttu-id="7db22-130">a.</span><span class="sxs-lookup"><span data-stu-id="7db22-130">a.</span></span> <span data-ttu-id="7db22-131">**이름**: 이 작업에 대한 고유 식별자를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7db22-131">**Name**: Enter a unique identifier for this action.</span></span>

    <span data-ttu-id="7db22-132">b.</span><span class="sxs-lookup"><span data-stu-id="7db22-132">b.</span></span> <span data-ttu-id="7db22-133">**작업 유형**: SMS, 전자 메일 또는 웹후크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7db22-133">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="7db22-134">c.</span><span class="sxs-lookup"><span data-stu-id="7db22-134">c.</span></span> <span data-ttu-id="7db22-135">**세부 정보**: 전화 번호, 전자 메일 주소 또는 URI webhook 입력 hello 동작 형식을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7db22-135">**Details**: Based on hello action type, enter a phone number, email address, or webhook URI.</span></span>

8. <span data-ttu-id="7db22-136">선택 **확인** toocreate hello 동작 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="7db22-136">Select **OK** toocreate hello action group.</span></span>

## <a name="manage-your-action-groups"></a><span data-ttu-id="7db22-137">작업 그룹 관리</span><span class="sxs-lookup"><span data-stu-id="7db22-137">Manage your action groups</span></span> ##
<span data-ttu-id="7db22-138">Hello에 표시 되는 작업 그룹을 만든 후 **동작 그룹** hello 섹션 **모니터** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="7db22-138">After you create an action group, it's visible in hello **Action groups** section of hello **Monitor** blade.</span></span> <span data-ttu-id="7db22-139">Toomanage를 원하는 hello 동작 그룹을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7db22-139">Select hello action group you want toomanage to:</span></span>

* <span data-ttu-id="7db22-140">작업을 추가, 편집 또는 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="7db22-140">Add, edit, or remove actions.</span></span>
* <span data-ttu-id="7db22-141">Hello 동작 그룹을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="7db22-141">Delete hello action group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7db22-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7db22-142">Next steps</span></span> ##
* <span data-ttu-id="7db22-143">[SMS 경고 동작](monitoring-sms-alert-behavior.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="7db22-143">Learn more about [SMS alert behavior](monitoring-sms-alert-behavior.md).</span></span>  
* <span data-ttu-id="7db22-144">얻을 [hello 활동 로그 경고 webhook 스키마의](monitoring-activity-log-alerts-webhook.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7db22-144">Gain an [understanding of hello activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>  
* <span data-ttu-id="7db22-145">경고의 [속도 제한](monitoring-alerts-rate-limiting.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="7db22-145">Learn more about [rate limiting](monitoring-alerts-rate-limiting.md) on alerts.</span></span> 
* <span data-ttu-id="7db22-146">가져오기는 [활동 로그 경고의 개요](monitoring-overview-alerts.md), 알아봅니다 어떻게 tooreceive 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7db22-146">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how tooreceive alerts.</span></span>  
* <span data-ttu-id="7db22-147">너무 방법에 대해 알아봅니다[서비스 상태 알림 게시 될 때마다 경고를 구성](monitoring-activity-log-alerts-on-service-notifications.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7db22-147">Learn how too[configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
