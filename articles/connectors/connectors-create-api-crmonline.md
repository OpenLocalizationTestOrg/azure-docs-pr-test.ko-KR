---
title: "Azure Logic Apps에서 Dynamics 365(온라인) 연결 | Microsoft Docs"
description: "Dynamics 365 커넥터가 제공하는 API를 통해 Dynamics 365(온라인) 엔터티를 관리하는 논리 앱 워크플로 만들기"
services: logic-apps
cloud: Azure Stack
author: Mattp123
manager: anneta
documentationcenter: 
tags: connectors
ms.assetid: 0dc2abef-7d2c-4a2d-87ca-fad21367d135
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: matp; LADocs
ms.openlocfilehash: d35647921ff540167a3a591fb489d3bab031a5c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-dynamics-365-from-logic-app-workflows"></a><span data-ttu-id="857b7-103">논리 앱 워크플로에서 Dynamics 365에 연결</span><span class="sxs-lookup"><span data-stu-id="857b7-103">Connect to Dynamics 365 from logic app workflows</span></span>

<span data-ttu-id="857b7-104">Logic Apps를 사용하여 Dynamics 365(온라인)에 연결하고 레코드를 만들고 항목을 업데이트하거나 레코드 목록을 반환하는 유용한 비즈니스 흐름을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-104">With Logic Apps, you can connect to Dynamics 365 (online) and create useful business flows that create records, update items, or return a list of records.</span></span> <span data-ttu-id="857b7-105">Dynamics 365 커넥터를 사용하면 다음과 같은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-105">With the Dynamics 365 connector, you can:</span></span>

* <span data-ttu-id="857b7-106">Dynamics 365(온라인)에서 가져온 데이터에 기반한 비즈니스 흐름을 구축합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-106">Build your business flow based on the data you get from Dynamics 365 (online).</span></span>
* <span data-ttu-id="857b7-107">이러한 작업을 사용하여 응답을 가져오고 출력을 다른 작업에 사용할 수 있도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-107">Use actions that get a response and then make the output available for other actions.</span></span> <span data-ttu-id="857b7-108">예를 들어 Dynamics 365(온라인)에서 항목이 업데이트되면 Office 365를 사용하여 메일을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-108">For example, when an item is updated in Dynamics 365 (online), you can send an email using Office 365.</span></span>

<span data-ttu-id="857b7-109">이 항목에서는 Dynamics 365에서 새 리드가 생성될 때마다 Dynamics 365에서 작업을 생성하는 논리 앱 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-109">This topic shows you how to create a logic app that creates a task in Dynamics 365 whenever a new lead is created in Dynamics 365.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="857b7-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="857b7-110">Prerequisites</span></span>
* <span data-ttu-id="857b7-111">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="857b7-111">An Azure account.</span></span>
* <span data-ttu-id="857b7-112">Dynamics 365(온라인) 계정.</span><span class="sxs-lookup"><span data-stu-id="857b7-112">A Dynamics 365 (online) account.</span></span>

## <a name="create-a-task-when-a-new-lead-is-created-in-dynamics-365"></a><span data-ttu-id="857b7-113">Dynamics 365에서 새 리드가 생성될 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="857b7-113">Create a task when a new lead is created in Dynamics 365</span></span>

1.  <span data-ttu-id="857b7-114">[Azure에 로그인](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-114">[Sign in to Azure](https://portal.azure.com).</span></span>

2.  <span data-ttu-id="857b7-115">Azure 검색 상자에 `Logic apps`를 입력하고 ENTER 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-115">In the Azure search box, type `Logic apps`, and press ENTER.</span></span>

      ![논리 앱 찾기](./media/connectors-create-api-crmonline/find-logic-apps.png)

3.  <span data-ttu-id="857b7-117">**논리 앱** 아래에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-117">Under **Logic apps**, click **Add**.</span></span>

      ![LogicApp 추가](./media/connectors-create-api-crmonline/add-logic-app.png)

4.  <span data-ttu-id="857b7-119">논리 앱을 만들려면 **이름**, **구독**, **리소스 그룹** 및 **위치** 필드를 작성하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-119">To create the logic app, complete the **Name**, **Subscription**, **Resource Group**, and **Location** fields, and then click **Create**.</span></span>

5.  <span data-ttu-id="857b7-120">새 논리 앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-120">Select the new logic app.</span></span> <span data-ttu-id="857b7-121">**배포 성공** 알림이 수신되면 **새로 고침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-121">When you receive the **Deployment Succeeded** notification, click **Refresh**.</span></span>

6.  <span data-ttu-id="857b7-122">**배포 도구** 아래에서 **논리 앱 디자이너**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-122">Under **Development Tools**, click **Logic App Designer**.</span></span> <span data-ttu-id="857b7-123">템플릿 목록에서 **빈 논리 앱**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-123">In the template list, click **Blank Logic App**.</span></span>

7.  <span data-ttu-id="857b7-124">검색 상자에서 `Dynamics 365`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-124">In the search box, type `Dynamics 365`.</span></span> <span data-ttu-id="857b7-125">Dynamics 365 트리거 목록에서 **Dynamics 365 – 레코드가 만들어지는 경우**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-125">From the Dynamics 365 triggers list, select **Dynamics 365 – When a record is created**.</span></span>

8.  <span data-ttu-id="857b7-126">Dynamics 365에 로그인하라는 메시지가 나타나면 지금 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-126">If you are prompted to sign in to Dynamics 365, do so now.</span></span>

9.  <span data-ttu-id="857b7-127">트리거 세부 정보에서 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-127">In the trigger details, enter the following information:</span></span>

  * <span data-ttu-id="857b7-128">**조직 이름**.</span><span class="sxs-lookup"><span data-stu-id="857b7-128">**Organization Name**.</span></span> <span data-ttu-id="857b7-129">논리 앱에서 수신하려는 Dynamics 365 인스턴스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-129">Select the Dynamics 365 instance that you want the logic app to listen to.</span></span>

  * <span data-ttu-id="857b7-130">**엔터티 이름**.</span><span class="sxs-lookup"><span data-stu-id="857b7-130">**Entity Name**.</span></span> <span data-ttu-id="857b7-131">수신 대기할 엔터티를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-131">Select the entity that you want to listen to.</span></span> <span data-ttu-id="857b7-132">이 이벤트는 논리 앱을 시작하는 트리거 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-132">This event acts as a trigger to start the logic app.</span></span> 
  <span data-ttu-id="857b7-133">이 연습에서는 **리드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-133">In this walkthrough, **Leads** is selected.</span></span>

  * <span data-ttu-id="857b7-134">**얼마나 자주 항목을 확인하시겠습니까?**</span><span class="sxs-lookup"><span data-stu-id="857b7-134">**How often do you want to check for items?**</span></span> <span data-ttu-id="857b7-135">이 값은 논리 앱이 트리거와 관련된 업데이트를 확인하는 빈도를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-135">These values set how often the logic app checks for updates related to the trigger.</span></span> <span data-ttu-id="857b7-136">기본 설정은 3분마다 업데이트를 확인하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-136">The default setting is to check for updates every three minutes.</span></span>

    * <span data-ttu-id="857b7-137">**빈도**.</span><span class="sxs-lookup"><span data-stu-id="857b7-137">**Frequency**.</span></span> <span data-ttu-id="857b7-138">초, 분, 시간 또는 일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-138">Select seconds, minutes, hours, or days.</span></span>

    * <span data-ttu-id="857b7-139">**간격**.</span><span class="sxs-lookup"><span data-stu-id="857b7-139">**Interval**.</span></span> <span data-ttu-id="857b7-140">다음 확인 때까지 경과할 초, 분, 시간, 일수를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-140">Enter the number of seconds, minutes, hours, or days that you want to pass before the next check.</span></span>

      ![논리 앱 트리거 세부 정보](./media/connectors-create-api-crmonline/trigger-details.png)

10. <span data-ttu-id="857b7-142">**새 단계**를 클릭한 다음 **작업 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-142">Click **New step**, and then click **Add an action**.</span></span>

11. <span data-ttu-id="857b7-143">검색 상자에서 `Dynamics 365`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-143">In the search box, type `Dynamics 365`.</span></span> <span data-ttu-id="857b7-144">작업 목록에서 **Dynamics 365 – 새 레코드 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-144">From the actions list, select **Dynamics 365 – Create a new record**.</span></span>

12. <span data-ttu-id="857b7-145">다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-145">Enter the following information:</span></span>

    * <span data-ttu-id="857b7-146">**조직 이름**.</span><span class="sxs-lookup"><span data-stu-id="857b7-146">**Organization Name**.</span></span> <span data-ttu-id="857b7-147">흐름에서 레코드를 만들려는 Dynamics 365 인스턴스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-147">Select the Dynamics 365 instance where you want the flow to create the record.</span></span> 
    <span data-ttu-id="857b7-148">이 인스턴스는 이벤트가 트리거되는 인스턴스와 같을 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-148">Notice that this instance doesn’t have to be the same instance where the event is triggered from.</span></span>

    * <span data-ttu-id="857b7-149">**엔터티 이름**.</span><span class="sxs-lookup"><span data-stu-id="857b7-149">**Entity Name**.</span></span> <span data-ttu-id="857b7-150">이벤트가 트리거될 때 레코드를 만들려는 엔터티를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-150">Select the entity that you want to create a record when the event is triggered.</span></span> 
    <span data-ttu-id="857b7-151">이 연습에서는 **작업**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-151">In this walkthrough, **Tasks** is selected.</span></span>

13. <span data-ttu-id="857b7-152">나타나는 **주제** 상자를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-152">Click in the **Subject** box that appears.</span></span> <span data-ttu-id="857b7-153">나타나는 동적 콘텐츠 목록에서 이러한 필드 중 하나를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-153">From the dynamic content list that appears, you can select either of these fields:</span></span>

    * <span data-ttu-id="857b7-154">**성**.</span><span class="sxs-lookup"><span data-stu-id="857b7-154">**Last Name**.</span></span> <span data-ttu-id="857b7-155">이 필드를 선택하면 작업 레코드가 만들어질 때 리드의 성이 작업의 [제목] 필드에 삽입됩니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-155">Selecting this field inserts the last name for the lead into the Subject field for the task, when the task record is created.</span></span>
    * <span data-ttu-id="857b7-156">**토픽**.</span><span class="sxs-lookup"><span data-stu-id="857b7-156">**Topic**.</span></span> <span data-ttu-id="857b7-157">이 필드를 선택하면 작업 레코드가 만들어질 때 리드의 토픽 필드가 작업의 [제목] 필드에 삽입됩니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-157">Selecting this field inserts the Topic field for the lead into the Subject field for the task, when the task record is created.</span></span> 
    <span data-ttu-id="857b7-158">**토픽**을 클릭하여 **제목** 상자에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-158">Click **Topic** to add that to the **Subject** box.</span></span>

      ![논리 앱 새 레코드 만들기 세부 정보](./media/connectors-create-api-crmonline/create-record-details.png)

14. <span data-ttu-id="857b7-160">논리 앱 디자이너 도구 모음에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-160">On the Logic App Designer toolbar, click **Save**.</span></span>

    ![논리 앱 디자이너 도구 모음 저장](./media/connectors-create-api-crmonline/designer-toolbar-save.png)

15. <span data-ttu-id="857b7-162">논리 앱을 시작하려면 **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-162">To start the Logic App, click **Run**.</span></span>

    ![논리 앱 디자이너 도구 모음 저장](./media/connectors-create-api-crmonline/designer-toolbar-run.png)

16. <span data-ttu-id="857b7-164">이제 Dynamics 365 for Sales에서 리드 레코드를 만들고 흐름이 어떻게 진행되는지 확인하세요!</span><span class="sxs-lookup"><span data-stu-id="857b7-164">Now create a lead record in Dynamics 365 for Sales and see your flow in action!</span></span>

## <a name="set-advanced-options-for-a-logic-app-step"></a><span data-ttu-id="857b7-165">논리 앱 단계에 대한 고급 옵션 설정</span><span class="sxs-lookup"><span data-stu-id="857b7-165">Set advanced options for a logic app step</span></span>

<span data-ttu-id="857b7-166">논리 앱 단계에서 데이터를 필터링하는 방법을 지정하려면 해당 단계에서 **고급 옵션 표시**를 클릭한 후 쿼리로 필터 또는 주문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-166">To specify how to filter data in a logic app step, click **Show advanced options** in that step, then add a filter or order by query.</span></span>

<span data-ttu-id="857b7-167">예를 들어 필터 쿼리를 사용하여 계정 이름으로 활성 계정 및 주문만 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-167">For example, you can use a filter query to get only active accounts and order by the account name.</span></span> <span data-ttu-id="857b7-168">이 작업을 수행하려면 OData 필터 쿼리 `statuscode eq 1`을 입력하고 동적 콘텐츠 목록에서 **계정 이름**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-168">To perform this task, enter the OData filter query `statuscode eq 1`, and select **Account Name** from the dynamic content list.</span></span> <span data-ttu-id="857b7-169">자세한 정보: [MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) 및 [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2)</span><span class="sxs-lookup"><span data-stu-id="857b7-169">More information: [MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) and [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2).</span></span>

![논리 앱 고급 옵션](./media/connectors-create-api-crmonline/advanced-options.png)

### <a name="best-practices-when-using-advanced-options"></a><span data-ttu-id="857b7-171">고급 옵션을 사용하는 경우 모범 사례</span><span class="sxs-lookup"><span data-stu-id="857b7-171">Best practices when using advanced options</span></span>

<span data-ttu-id="857b7-172">필드에 값을 추가할 경우 값을 입력하거나 표시된 동적 콘텐츠 목록에서 선택하거나 어떤 방법에서든, 해당 필드 형식과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-172">When you add a value to a field, you must match the field type whether you type a value or select a value from the dynamic content list.</span></span>

<span data-ttu-id="857b7-173">필드 형식</span><span class="sxs-lookup"><span data-stu-id="857b7-173">Field type</span></span>  |<span data-ttu-id="857b7-174">사용 방법</span><span class="sxs-lookup"><span data-stu-id="857b7-174">How to use</span></span>  |<span data-ttu-id="857b7-175">찾는 위치</span><span class="sxs-lookup"><span data-stu-id="857b7-175">Where to find</span></span>  |<span data-ttu-id="857b7-176">이름</span><span class="sxs-lookup"><span data-stu-id="857b7-176">Name</span></span>  |<span data-ttu-id="857b7-177">데이터 형식</span><span class="sxs-lookup"><span data-stu-id="857b7-177">Data type</span></span>  
---------|---------|---------|---------|---------
<span data-ttu-id="857b7-178">텍스트 필드</span><span class="sxs-lookup"><span data-stu-id="857b7-178">Text fields</span></span>|<span data-ttu-id="857b7-179">텍스트 필드에는 한 줄의 텍스트 또는 텍스트 형식 필드인 동적 콘텐츠가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-179">Text fields require a single line of text or dynamic content that is a text type field.</span></span> <span data-ttu-id="857b7-180">이러한 예로 범주, 하위 범주 필드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-180">Examples include the Category and Sub-Category fields.</span></span>|<span data-ttu-id="857b7-181">설정 > 사용자 지정 > 시스템 사용자 지정 > 엔터티 > 작업 > 필드</span><span class="sxs-lookup"><span data-stu-id="857b7-181">Settings > Customizations > Customize the System > Entities > Task > Fields</span></span> |<span data-ttu-id="857b7-182">카테고리</span><span class="sxs-lookup"><span data-stu-id="857b7-182">category</span></span> |<span data-ttu-id="857b7-183">한 줄의 텍스트</span><span class="sxs-lookup"><span data-stu-id="857b7-183">Single Line of Text</span></span>        
<span data-ttu-id="857b7-184">정수 필드</span><span class="sxs-lookup"><span data-stu-id="857b7-184">Integer fields</span></span> | <span data-ttu-id="857b7-185">일부 필드에는 정수 또는 정수 형식 필드인 동적 콘텐츠가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-185">Some fields require integer or dynamic content that is an integer type field.</span></span> <span data-ttu-id="857b7-186">이러한 예로 완료율, 기간이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-186">Examples include Percent Complete and Duration.</span></span> |<span data-ttu-id="857b7-187">설정 > 사용자 지정 > 시스템 사용자 지정 > 엔터티 > 작업 > 필드</span><span class="sxs-lookup"><span data-stu-id="857b7-187">Settings > Customizations > Customize the System > Entities > Task > Fields</span></span> |<span data-ttu-id="857b7-188">percentcomplete</span><span class="sxs-lookup"><span data-stu-id="857b7-188">percentcomplete</span></span> |<span data-ttu-id="857b7-189">정수</span><span class="sxs-lookup"><span data-stu-id="857b7-189">Whole Number</span></span>         
<span data-ttu-id="857b7-190">날짜 필드</span><span class="sxs-lookup"><span data-stu-id="857b7-190">Date fields</span></span> | <span data-ttu-id="857b7-191">일부 필드에 mm/dd/yyyy 형식 또는 날짜 형식 필드인 동적 콘텐츠가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-191">Some fields require a date entered in mm/dd/yyyy format or dynamic content that is a date type field.</span></span> <span data-ttu-id="857b7-192">이러한 예로 만든 날짜, 시작 날짜, 실제 시작, 마지막 보류 시간, 실제 종료, 기한 날짜가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-192">Examples include Created On, Start Date, Actual Start, Last on Hold Time, Actual End, and Due Date.</span></span> | <span data-ttu-id="857b7-193">설정 > 사용자 지정 > 시스템 사용자 지정 > 엔터티 > 작업 > 필드</span><span class="sxs-lookup"><span data-stu-id="857b7-193">Settings > Customizations > Customize the System > Entities > Task > Fields</span></span> |<span data-ttu-id="857b7-194">createdon</span><span class="sxs-lookup"><span data-stu-id="857b7-194">createdon</span></span> |<span data-ttu-id="857b7-195">날짜 및 시간</span><span class="sxs-lookup"><span data-stu-id="857b7-195">Date and Time</span></span>
<span data-ttu-id="857b7-196">레코드 ID와 조회 유형이 모두 필요한 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-196">Fields that require both a record ID and lookup type</span></span> |<span data-ttu-id="857b7-197">다른 엔터티 레코드를 참조하는 일부 필드에는 레코드 ID와 조회 유형이 모두 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-197">Some fields that reference another entity record require both the record ID and the lookup type.</span></span> |<span data-ttu-id="857b7-198">설정 > 사용자 지정 > 시스템 사용자 지정 > 엔터티 > 계정 > 필드</span><span class="sxs-lookup"><span data-stu-id="857b7-198">Settings > Customizations > Customize the System > Entities > Account > Fields</span></span>  | <span data-ttu-id="857b7-199">accountid</span><span class="sxs-lookup"><span data-stu-id="857b7-199">accountid</span></span>  | <span data-ttu-id="857b7-200">기본 키</span><span class="sxs-lookup"><span data-stu-id="857b7-200">Primary Key</span></span>

### <a name="more-examples-of-fields-that-require-both-a-record-id-and-lookup-type"></a><span data-ttu-id="857b7-201">레코드 ID와 조회 유형이 모두 필요한 필드의 추가 예</span><span class="sxs-lookup"><span data-stu-id="857b7-201">More examples of fields that require both a record ID and lookup type</span></span>
<span data-ttu-id="857b7-202">이전 테이블을 확장하면 동적 콘텐츠 목록에서 선택한 값으로 작동하지 않는 필드의 예가 더 있습니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-202">Expanding on the previous table, here are more examples of fields that don't work with values selected from the dynamic content list.</span></span> <span data-ttu-id="857b7-203">대신, 이러한 필드에는 PowerApps의 필드에 입력된 레코드 ID와 조회 형식이 모두 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-203">Instead, these fields require both a record ID and lookup type entered into the fields in PowerApps.</span></span>  
* <span data-ttu-id="857b7-204">소유자 및 소유자 유형.</span><span class="sxs-lookup"><span data-stu-id="857b7-204">Owner and Owner Type.</span></span> <span data-ttu-id="857b7-205">[소유자] 필드에는 유효한 사용자 또는 팀 레코드 ID가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-205">The Owner field must be a valid user or team record ID.</span></span> <span data-ttu-id="857b7-206">[소유자 유형]은 **시스템 사용자** 또는 **팀**이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-206">The Owner Type must be either **systemusers** or **teams**.</span></span>
* <span data-ttu-id="857b7-207">고객 및 고객 유형.</span><span class="sxs-lookup"><span data-stu-id="857b7-207">Customer and Customer Type.</span></span> <span data-ttu-id="857b7-208">[고객] 필드는 유효한 계정 또는 연락처 레코드 ID여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-208">The Customer field must be a valid account or contact record ID.</span></span> <span data-ttu-id="857b7-209">소유자 유형은 **계정** 또는 **연락처**이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-209">The Owner Type must be either **accounts** or **contacts**.</span></span>
* <span data-ttu-id="857b7-210">관련 항목 및 관련 유형.</span><span class="sxs-lookup"><span data-stu-id="857b7-210">Regarding and Regarding Type.</span></span> <span data-ttu-id="857b7-211">[관련 항목] 필드는 계정 또는 연락처 레코드 ID 등의 유효한 레코드 ID여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-211">The Regarding field must be a valid record ID, such as an account or contact record ID.</span></span> <span data-ttu-id="857b7-212">[관련 항목 유형]은 **계정** 또는 **연락처** 등의 레코드에 대한 조회 유형이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-212">The Regarding Type must be the lookup type for the record, such as **accounts** or **contacts**.</span></span>

<span data-ttu-id="857b7-213">다음 작업 만들기 예에서는 작업의 관련 항목 필드에 추가하여 레코드 ID에 해당하는 계정 레코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-213">The following task creation action example adds an account record that corresponds to the record ID adding it to the regarding field of the task.</span></span>

![흐름 recordId 및 계정 유형](./media/connectors-create-api-crmonline/recordid-type-account.png)

<span data-ttu-id="857b7-215">이 예제에서는 사용자의 레코드 ID에 따라 특정 사용자에게 작업을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-215">This example also assigns the task to a specific user based on the user's record ID.</span></span>

![흐름 recordId 및 계정 유형](./media/connectors-create-api-crmonline/recordid-type-user.png)

<span data-ttu-id="857b7-217">레코드의 ID를 찾으려면 아래의 *레코드 ID 찾기* 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="857b7-217">To find a record's ID, see the following section: *Find the record ID*</span></span>

## <a name="find-the-record-id"></a><span data-ttu-id="857b7-218">레코드 ID 찾기</span><span class="sxs-lookup"><span data-stu-id="857b7-218">Find the record ID</span></span>

1. <span data-ttu-id="857b7-219">계정 레코드 등의 레코드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-219">Open a record, such as an account record.</span></span>

2. <span data-ttu-id="857b7-220">작업 도구 모음에서 **팝아웃** ![팝아웃 레코드](./media/connectors-create-api-crmonline/popout-record.png)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-220">On the actions toolbar, click **Pop Out** ![popout record](./media/connectors-create-api-crmonline/popout-record.png).</span></span>
<span data-ttu-id="857b7-221">또는, 작업 도구 모음에서 전체 URL을 기본 전자 메일 프로그램에 복사하려면 **전자 메일로 링크 보내기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-221">Alternatively, on the actions toolbar, to copy the full URL into your default email program, click **EMAIL A LINK**.</span></span>

   <span data-ttu-id="857b7-222">레코드 ID는 URL의 %7b ~ %7d개의 인코딩 문자로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-222">The record ID is displayed in between the %7b and %7d encoding characters of the URL.</span></span>

   ![흐름 recordId 및 계정 유형](./media/connectors-create-api-crmonline/recordid.png)

## <a name="troubleshooting"></a><span data-ttu-id="857b7-224">문제 해결</span><span class="sxs-lookup"><span data-stu-id="857b7-224">Troubleshooting</span></span>
<span data-ttu-id="857b7-225">논리 앱에서 실패한 단계의 문제를 해결하려면 이벤트의 상태 세부 정보를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="857b7-225">To troubleshoot a failed step in a logic app, view the status details of the event.</span></span>

1. <span data-ttu-id="857b7-226">**논리 앱** 아래에서 논리 앱을 선택한 다음 **개요**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-226">Under **Logic Apps**, select your logic app, and then click **Overview**.</span></span> 

   <span data-ttu-id="857b7-227">[요약] 영역이 표시되고 논리 앱에 대한 실행 상태를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-227">The Summary area is shown and provides the run status for the logic app.</span></span> 

   ![논리 앱 실행 상태](./media/connectors-create-api-crmonline/tshoot1.png)

2. <span data-ttu-id="857b7-229">실패한 실행에 대한 자세한 정보를 보려면 실패한 이벤트를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-229">To view more information about any failed runs, click the failed event.</span></span> <span data-ttu-id="857b7-230">실패한 단계를 확장하려면 해당 단계를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-230">To expand a failed step, click that step.</span></span>

   ![실패한 단계 확장](./media/connectors-create-api-crmonline/tshoot2.png)

   <span data-ttu-id="857b7-232">단계의 세부 정보가 표시되고 실패 원인의 문제 해결에 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-232">The step details appear and can help troubleshoot the cause of the failure.</span></span>

   ![실패한 단계 세부 정보](./media/connectors-create-api-crmonline/tshoot3.png)

<span data-ttu-id="857b7-234">논리 앱 문제 해결에 대한 자세한 내용은 [논리 앱 오류 진단](../logic-apps/logic-apps-diagnosing-failures.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="857b7-234">For more information about troubleshooting logic apps, see [Diagnosing logic app failures](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="857b7-235">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="857b7-235">Connector-specific details</span></span>

<span data-ttu-id="857b7-236">[커넥터 세부 정보](/connectors/crm/)에서 swagger에 정의된 모든 트리거 및 작업과 제한 사항도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="857b7-236">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/crm/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="857b7-237">다음 단계</span><span class="sxs-lookup"><span data-stu-id="857b7-237">Next steps</span></span>
<span data-ttu-id="857b7-238">[API 목록](apis-list.md)에서 Logic Apps의 사용 가능한 다른 커넥터를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="857b7-238">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
