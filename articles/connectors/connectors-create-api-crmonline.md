---
title: "Azure 논리 앱에서 aaaConnect tooDynamics 365 (온라인) | Microsoft Docs"
description: "논리 hello hello Dynamics 365 커넥터에서 제공 하는 API 통해 Dynamics 365 (온라인) 엔터티를 관리 하는 응용 프로그램 워크플로 만들기"
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
ms.openlocfilehash: 183d7a6b8e5d2c0eecc70da0da3806e06c382df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toodynamics-365-from-logic-app-workflows"></a><span data-ttu-id="f6271-103">논리 앱 워크플로에서 tooDynamics 365 연결</span><span class="sxs-lookup"><span data-stu-id="f6271-103">Connect tooDynamics 365 from logic app workflows</span></span>

<span data-ttu-id="f6271-104">논리 앱 tooDynamics 365 (온라인)에 연결 하 고 레코드를 만들거나, 항목을 업데이트 하거나 레코드의 목록을 반환 하는 경우 유용한 비즈니스 흐름을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-104">With Logic Apps, you can connect tooDynamics 365 (online) and create useful business flows that create records, update items, or return a list of records.</span></span> <span data-ttu-id="f6271-105">Hello Dynamics 365 커넥터와 함께 다음 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-105">With hello Dynamics 365 connector, you can:</span></span>

* <span data-ttu-id="f6271-106">Dynamics 365 (온라인)에서 가져올 hello 데이터를 기반으로 비즈니스 흐름을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-106">Build your business flow based on hello data you get from Dynamics 365 (online).</span></span>
* <span data-ttu-id="f6271-107">응답 한 다음 다른 작업에 사용할 수 있는 hello 출력을 확인 하는 작업을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-107">Use actions that get a response and then make hello output available for other actions.</span></span> <span data-ttu-id="f6271-108">예를 들어 Dynamics 365(온라인)에서 항목이 업데이트되면 Office 365를 사용하여 메일을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-108">For example, when an item is updated in Dynamics 365 (online), you can send an email using Office 365.</span></span>

<span data-ttu-id="f6271-109">이 항목에서는 방법을 toocreate 논리 앱을 만드는 작업 Dynamics 365 Dynamics 365 새 잠재 고객 때마다 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-109">This topic shows you how toocreate a logic app that creates a task in Dynamics 365 whenever a new lead is created in Dynamics 365.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f6271-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f6271-110">Prerequisites</span></span>
* <span data-ttu-id="f6271-111">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="f6271-111">An Azure account.</span></span>
* <span data-ttu-id="f6271-112">Dynamics 365(온라인) 계정.</span><span class="sxs-lookup"><span data-stu-id="f6271-112">A Dynamics 365 (online) account.</span></span>

## <a name="create-a-task-when-a-new-lead-is-created-in-dynamics-365"></a><span data-ttu-id="f6271-113">Dynamics 365에서 새 리드가 생성될 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="f6271-113">Create a task when a new lead is created in Dynamics 365</span></span>

1.  <span data-ttu-id="f6271-114">[TooAzure 로그인](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-114">[Sign in tooAzure](https://portal.azure.com).</span></span>

2.  <span data-ttu-id="f6271-115">Hello Azure 검색 상자에 입력 `Logic apps`, ENTER 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-115">In hello Azure search box, type `Logic apps`, and press ENTER.</span></span>

      ![논리 앱 찾기](./media/connectors-create-api-crmonline/find-logic-apps.png)

3.  <span data-ttu-id="f6271-117">**논리 앱** 아래에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-117">Under **Logic apps**, click **Add**.</span></span>

      ![LogicApp 추가](./media/connectors-create-api-crmonline/add-logic-app.png)

4.  <span data-ttu-id="f6271-119">toocreate hello 논리 앱 전체 hello **이름**, **구독**, **리소스 그룹**, 및 **위치** 필드를 선택한 다음 클릭 **만들**합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-119">toocreate hello logic app, complete hello **Name**, **Subscription**, **Resource Group**, and **Location** fields, and then click **Create**.</span></span>

5.  <span data-ttu-id="f6271-120">Hello 새 논리 앱을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-120">Select hello new logic app.</span></span> <span data-ttu-id="f6271-121">Hello를 받는 경우 **배포 성공** 알림을 클릭 **새로 고침**합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-121">When you receive hello **Deployment Succeeded** notification, click **Refresh**.</span></span>

6.  <span data-ttu-id="f6271-122">**배포 도구** 아래에서 **논리 앱 디자이너**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-122">Under **Development Tools**, click **Logic App Designer**.</span></span> <span data-ttu-id="f6271-123">Hello 템플릿 목록에서 클릭 **빈 논리 앱**합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-123">In hello template list, click **Blank Logic App**.</span></span>

7.  <span data-ttu-id="f6271-124">Hello 검색 상자에 입력 `Dynamics 365`합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-124">In hello search box, type `Dynamics 365`.</span></span> <span data-ttu-id="f6271-125">Hello Dynamics 365 트리거합니다 목록, 선택 **Dynamics 365-레코드를 만들 때**합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-125">From hello Dynamics 365 triggers list, select **Dynamics 365 – When a record is created**.</span></span>

8.  <span data-ttu-id="f6271-126">TooDynamics 365에서에서 증명된 toosign 인 경우 않으면 지금 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-126">If you are prompted toosign in tooDynamics 365, do so now.</span></span>

9.  <span data-ttu-id="f6271-127">다음 정보는 hello hello 트리거 세부 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-127">In hello trigger details, enter hello following information:</span></span>

  * <span data-ttu-id="f6271-128">**조직 이름**.</span><span class="sxs-lookup"><span data-stu-id="f6271-128">**Organization Name**.</span></span> <span data-ttu-id="f6271-129">Hello 논리 앱 toolisten를 원하는 hello Dynamics 365 인스턴스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-129">Select hello Dynamics 365 instance that you want hello logic app toolisten to.</span></span>

  * <span data-ttu-id="f6271-130">**엔터티 이름**.</span><span class="sxs-lookup"><span data-stu-id="f6271-130">**Entity Name**.</span></span> <span data-ttu-id="f6271-131">Toolisten를 원하는 hello 엔터티를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-131">Select hello entity that you want toolisten to.</span></span> <span data-ttu-id="f6271-132">이 이벤트는 트리거 toostart hello 논리 앱 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-132">This event acts as a trigger toostart hello logic app.</span></span> 
  <span data-ttu-id="f6271-133">이 연습에서는 **리드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-133">In this walkthrough, **Leads** is selected.</span></span>

  * <span data-ttu-id="f6271-134">**얼마나 자주 시겠습니까 toocheck 항목에 대 한?**</span><span class="sxs-lookup"><span data-stu-id="f6271-134">**How often do you want toocheck for items?**</span></span> <span data-ttu-id="f6271-135">이러한 값은 얼마나 자주 설정 hello 논리 앱 업데이트 관련된 toohello 트리거를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-135">These values set how often hello logic app checks for updates related toohello trigger.</span></span> <span data-ttu-id="f6271-136">hello 기본 설정은 3 분 마다 업데이트에 대 한 toocheck입니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-136">hello default setting is toocheck for updates every three minutes.</span></span>

    * <span data-ttu-id="f6271-137">**빈도**.</span><span class="sxs-lookup"><span data-stu-id="f6271-137">**Frequency**.</span></span> <span data-ttu-id="f6271-138">초, 분, 시간 또는 일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-138">Select seconds, minutes, hours, or days.</span></span>

    * <span data-ttu-id="f6271-139">**간격**.</span><span class="sxs-lookup"><span data-stu-id="f6271-139">**Interval**.</span></span> <span data-ttu-id="f6271-140">Hello 초, 분, 시간 또는 toopass hello 다음 검사 하기 전에 원하는 날짜 수를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-140">Enter hello number of seconds, minutes, hours, or days that you want toopass before hello next check.</span></span>

      ![논리 앱 트리거 세부 정보](./media/connectors-create-api-crmonline/trigger-details.png)

10. <span data-ttu-id="f6271-142">**새 단계**를 클릭한 다음 **작업 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-142">Click **New step**, and then click **Add an action**.</span></span>

11. <span data-ttu-id="f6271-143">Hello 검색 상자에 입력 `Dynamics 365`합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-143">In hello search box, type `Dynamics 365`.</span></span> <span data-ttu-id="f6271-144">Hello 작업 목록에서 선택 **Dynamics 365 – 새 레코드를 만들어**합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-144">From hello actions list, select **Dynamics 365 – Create a new record**.</span></span>

12. <span data-ttu-id="f6271-145">Hello 다음 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-145">Enter hello following information:</span></span>

    * <span data-ttu-id="f6271-146">**조직 이름**.</span><span class="sxs-lookup"><span data-stu-id="f6271-146">**Organization Name**.</span></span> <span data-ttu-id="f6271-147">Hello 흐름 toocreate hello 레코드 저장할 hello Dynamics 365 인스턴스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-147">Select hello Dynamics 365 instance where you want hello flow toocreate hello record.</span></span> 
    <span data-ttu-id="f6271-148">이 인스턴스가 동일한 hello toobe에 되어 있지 않습니다 공지에서 hello 이벤트가 트리거되면 여기서 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="f6271-148">Notice that this instance doesn’t have toobe hello same instance where hello event is triggered from.</span></span>

    * <span data-ttu-id="f6271-149">**엔터티 이름**.</span><span class="sxs-lookup"><span data-stu-id="f6271-149">**Entity Name**.</span></span> <span data-ttu-id="f6271-150">Hello 이벤트가 트리거될 때 않겠다고 toocreate 레코드 hello 엔터티를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-150">Select hello entity that you want toocreate a record when hello event is triggered.</span></span> 
    <span data-ttu-id="f6271-151">이 연습에서는 **작업**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-151">In this walkthrough, **Tasks** is selected.</span></span>

13. <span data-ttu-id="f6271-152">Hello에 클릭 **주체** 나타나는 상자.</span><span class="sxs-lookup"><span data-stu-id="f6271-152">Click in hello **Subject** box that appears.</span></span> <span data-ttu-id="f6271-153">Hello 동적 콘텐츠 나타나는 목록에서 이러한 필드 중 하나를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-153">From hello dynamic content list that appears, you can select either of these fields:</span></span>

    * <span data-ttu-id="f6271-154">**성**.</span><span class="sxs-lookup"><span data-stu-id="f6271-154">**Last Name**.</span></span> <span data-ttu-id="f6271-155">Hello 작업 레코드를 만들 때 hello 잠재 고객에 대 한 hello 성을 hello 작업에 대 한 hello 제목 필드에 삽입이 필드를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-155">Selecting this field inserts hello last name for hello lead into hello Subject field for hello task, when hello task record is created.</span></span>
    * <span data-ttu-id="f6271-156">**토픽**.</span><span class="sxs-lookup"><span data-stu-id="f6271-156">**Topic**.</span></span> <span data-ttu-id="f6271-157">Hello 작업에 대 한 hello 제목 필드에 hello 리드에이 필드 삽입 hello 항목 필드를 선택 때 hello 작업 레코드가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-157">Selecting this field inserts hello Topic field for hello lead into hello Subject field for hello task, when hello task record is created.</span></span> 
    <span data-ttu-id="f6271-158">클릭 **항목** tooadd 해당 toohello **주체** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-158">Click **Topic** tooadd that toohello **Subject** box.</span></span>

      ![논리 앱 새 레코드 만들기 세부 정보](./media/connectors-create-api-crmonline/create-record-details.png)

14. <span data-ttu-id="f6271-160">Hello 논리가 응용 프로그램 디자이너 도구 모음에서 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-160">On hello Logic App Designer toolbar, click **Save**.</span></span>

    ![논리 앱 디자이너 도구 모음 저장](./media/connectors-create-api-crmonline/designer-toolbar-save.png)

15. <span data-ttu-id="f6271-162">논리 앱 toostart hello 클릭 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-162">toostart hello Logic App, click **Run**.</span></span>

    ![논리 앱 디자이너 도구 모음 저장](./media/connectors-create-api-crmonline/designer-toolbar-run.png)

16. <span data-ttu-id="f6271-164">이제 Dynamics 365 for Sales에서 리드 레코드를 만들고 흐름이 어떻게 진행되는지 확인하세요!</span><span class="sxs-lookup"><span data-stu-id="f6271-164">Now create a lead record in Dynamics 365 for Sales and see your flow in action!</span></span>

## <a name="set-advanced-options-for-a-logic-app-step"></a><span data-ttu-id="f6271-165">논리 앱 단계에 대한 고급 옵션 설정</span><span class="sxs-lookup"><span data-stu-id="f6271-165">Set advanced options for a logic app step</span></span>

<span data-ttu-id="f6271-166">논리 앱 단계에서 toofilter 데이터 클릭 방법을 toospecify **고급 옵션 표시** 해당 단계에서 다음 필터 또는 추가 순서 쿼리에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-166">toospecify how toofilter data in a logic app step, click **Show advanced options** in that step, then add a filter or order by query.</span></span>

<span data-ttu-id="f6271-167">예를 들어 필터의 쿼리 tooget 유일한 활성 계정을 사용할 수 있으며 hello 계정 이름을 기준으로 정렬.</span><span class="sxs-lookup"><span data-stu-id="f6271-167">For example, you can use a filter query tooget only active accounts and order by hello account name.</span></span> <span data-ttu-id="f6271-168">tooperform이 작업을 hello OData 필터 쿼리 입력 `statuscode eq 1`를 선택 하 고 **계정 이름** hello 동적 콘텐츠 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-168">tooperform this task, enter hello OData filter query `statuscode eq 1`, and select **Account Name** from hello dynamic content list.</span></span> <span data-ttu-id="f6271-169">자세한 정보: [MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) 및 [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2)</span><span class="sxs-lookup"><span data-stu-id="f6271-169">More information: [MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) and [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2).</span></span>

![논리 앱 고급 옵션](./media/connectors-create-api-crmonline/advanced-options.png)

### <a name="best-practices-when-using-advanced-options"></a><span data-ttu-id="f6271-171">고급 옵션을 사용하는 경우 모범 사례</span><span class="sxs-lookup"><span data-stu-id="f6271-171">Best practices when using advanced options</span></span>

<span data-ttu-id="f6271-172">값 tooa 필드를 추가한 경우 값을 입력 하거나 hello 동적 콘텐츠 목록에서 값을 선택 하는지 여부를 hello 필드 형식이 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-172">When you add a value tooa field, you must match hello field type whether you type a value or select a value from hello dynamic content list.</span></span>

<span data-ttu-id="f6271-173">필드 형식</span><span class="sxs-lookup"><span data-stu-id="f6271-173">Field type</span></span>  |<span data-ttu-id="f6271-174">어떻게 toouse</span><span class="sxs-lookup"><span data-stu-id="f6271-174">How toouse</span></span>  |<span data-ttu-id="f6271-175">여기서 toofind</span><span class="sxs-lookup"><span data-stu-id="f6271-175">Where toofind</span></span>  |<span data-ttu-id="f6271-176">이름</span><span class="sxs-lookup"><span data-stu-id="f6271-176">Name</span></span>  |<span data-ttu-id="f6271-177">데이터 형식</span><span class="sxs-lookup"><span data-stu-id="f6271-177">Data type</span></span>  
---------|---------|---------|---------|---------
<span data-ttu-id="f6271-178">텍스트 필드</span><span class="sxs-lookup"><span data-stu-id="f6271-178">Text fields</span></span>|<span data-ttu-id="f6271-179">텍스트 필드에는 한 줄의 텍스트 또는 텍스트 형식 필드인 동적 콘텐츠가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-179">Text fields require a single line of text or dynamic content that is a text type field.</span></span> <span data-ttu-id="f6271-180">Hello 범주 및 하위 범주 필드를 포함 하는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-180">Examples include hello Category and Sub-Category fields.</span></span>|<span data-ttu-id="f6271-181">설정 > 사용자 지정 > 사용자 지정 hello 시스템 > 엔터티 > 작업 > 필드</span><span class="sxs-lookup"><span data-stu-id="f6271-181">Settings > Customizations > Customize hello System > Entities > Task > Fields</span></span> |<span data-ttu-id="f6271-182">카테고리</span><span class="sxs-lookup"><span data-stu-id="f6271-182">category</span></span> |<span data-ttu-id="f6271-183">한 줄의 텍스트</span><span class="sxs-lookup"><span data-stu-id="f6271-183">Single Line of Text</span></span>        
<span data-ttu-id="f6271-184">정수 필드</span><span class="sxs-lookup"><span data-stu-id="f6271-184">Integer fields</span></span> | <span data-ttu-id="f6271-185">일부 필드에는 정수 또는 정수 형식 필드인 동적 콘텐츠가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-185">Some fields require integer or dynamic content that is an integer type field.</span></span> <span data-ttu-id="f6271-186">이러한 예로 완료율, 기간이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-186">Examples include Percent Complete and Duration.</span></span> |<span data-ttu-id="f6271-187">설정 > 사용자 지정 > 사용자 지정 hello 시스템 > 엔터티 > 작업 > 필드</span><span class="sxs-lookup"><span data-stu-id="f6271-187">Settings > Customizations > Customize hello System > Entities > Task > Fields</span></span> |<span data-ttu-id="f6271-188">percentcomplete</span><span class="sxs-lookup"><span data-stu-id="f6271-188">percentcomplete</span></span> |<span data-ttu-id="f6271-189">정수</span><span class="sxs-lookup"><span data-stu-id="f6271-189">Whole Number</span></span>         
<span data-ttu-id="f6271-190">날짜 필드</span><span class="sxs-lookup"><span data-stu-id="f6271-190">Date fields</span></span> | <span data-ttu-id="f6271-191">일부 필드에 mm/dd/yyyy 형식 또는 날짜 형식 필드인 동적 콘텐츠가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-191">Some fields require a date entered in mm/dd/yyyy format or dynamic content that is a date type field.</span></span> <span data-ttu-id="f6271-192">이러한 예로 만든 날짜, 시작 날짜, 실제 시작, 마지막 보류 시간, 실제 종료, 기한 날짜가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-192">Examples include Created On, Start Date, Actual Start, Last on Hold Time, Actual End, and Due Date.</span></span> | <span data-ttu-id="f6271-193">설정 > 사용자 지정 > 사용자 지정 hello 시스템 > 엔터티 > 작업 > 필드</span><span class="sxs-lookup"><span data-stu-id="f6271-193">Settings > Customizations > Customize hello System > Entities > Task > Fields</span></span> |<span data-ttu-id="f6271-194">createdon</span><span class="sxs-lookup"><span data-stu-id="f6271-194">createdon</span></span> |<span data-ttu-id="f6271-195">날짜 및 시간</span><span class="sxs-lookup"><span data-stu-id="f6271-195">Date and Time</span></span>
<span data-ttu-id="f6271-196">레코드 ID와 조회 유형이 모두 필요한 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-196">Fields that require both a record ID and lookup type</span></span> |<span data-ttu-id="f6271-197">다른 엔터티 레코드를 참조 하는 일부 필드는 hello 레코드 ID와 hello 조회 유형을 모두 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-197">Some fields that reference another entity record require both hello record ID and hello lookup type.</span></span> |<span data-ttu-id="f6271-198">설정 > 사용자 지정 > 사용자 지정 hello 시스템 > 엔터티 > 계정 > 필드</span><span class="sxs-lookup"><span data-stu-id="f6271-198">Settings > Customizations > Customize hello System > Entities > Account > Fields</span></span>  | <span data-ttu-id="f6271-199">accountid</span><span class="sxs-lookup"><span data-stu-id="f6271-199">accountid</span></span>  | <span data-ttu-id="f6271-200">기본 키</span><span class="sxs-lookup"><span data-stu-id="f6271-200">Primary Key</span></span>

### <a name="more-examples-of-fields-that-require-both-a-record-id-and-lookup-type"></a><span data-ttu-id="f6271-201">레코드 ID와 조회 유형이 모두 필요한 필드의 추가 예</span><span class="sxs-lookup"><span data-stu-id="f6271-201">More examples of fields that require both a record ID and lookup type</span></span>
<span data-ttu-id="f6271-202">Hello 이전 테이블에 확장을 추가 예제 hello 동적 콘텐츠 목록에서 선택 된 값을 사용 하지 않는 필드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-202">Expanding on hello previous table, here are more examples of fields that don't work with values selected from hello dynamic content list.</span></span> <span data-ttu-id="f6271-203">대신, 이러한 필드 두 레코드 ID와 조회 종류 중 하나로 PowerApps의 hello 필드에 입력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-203">Instead, these fields require both a record ID and lookup type entered into hello fields in PowerApps.</span></span>  
* <span data-ttu-id="f6271-204">소유자 및 소유자 유형.</span><span class="sxs-lookup"><span data-stu-id="f6271-204">Owner and Owner Type.</span></span> <span data-ttu-id="f6271-205">hello 소유자 필드는 유효한 사용자 또는 팀 레코드 ID 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-205">hello Owner field must be a valid user or team record ID.</span></span> <span data-ttu-id="f6271-206">hello 소유자 유형 중 하나 여야 합니다 **systemusers** 또는 **팀**합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-206">hello Owner Type must be either **systemusers** or **teams**.</span></span>
* <span data-ttu-id="f6271-207">고객 및 고객 유형.</span><span class="sxs-lookup"><span data-stu-id="f6271-207">Customer and Customer Type.</span></span> <span data-ttu-id="f6271-208">hello 고객 필드 유효한 계정 이거나 문의 레코드 id입니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-208">hello Customer field must be a valid account or contact record ID.</span></span> <span data-ttu-id="f6271-209">hello 소유자 유형 중 하나 여야 합니다 **계정** 또는 **연락처**합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-209">hello Owner Type must be either **accounts** or **contacts**.</span></span>
* <span data-ttu-id="f6271-210">관련 항목 및 관련 유형.</span><span class="sxs-lookup"><span data-stu-id="f6271-210">Regarding and Regarding Type.</span></span> <span data-ttu-id="f6271-211">필드에 대 한 hello 계정 등, 올바른 레코드 ID 이거나 문의 레코드 id입니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-211">hello Regarding field must be a valid record ID, such as an account or contact record ID.</span></span> <span data-ttu-id="f6271-212">hello에 대 한 형식은 형식 이어야 합니다 hello 조회 hello 레코드에 대 한 같은 **계정** 또는 **연락처**합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-212">hello Regarding Type must be hello lookup type for hello record, such as **accounts** or **contacts**.</span></span>

<span data-ttu-id="f6271-213">hello 다음 작업 만들기 작업 추가 예제 toohello hello 작업의 필드에 대 한 추가 toohello 레코드 ID를 해당 하는 계정 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-213">hello following task creation action example adds an account record that corresponds toohello record ID adding it toohello regarding field of hello task.</span></span>

![흐름 recordId 및 계정 유형](./media/connectors-create-api-crmonline/recordid-type-account.png)

<span data-ttu-id="f6271-215">이 예제에서는 또한 hello 작업 tooa 특정 사용자를 할당 hello 사용자 레코드 ID를 기반</span><span class="sxs-lookup"><span data-stu-id="f6271-215">This example also assigns hello task tooa specific user based on hello user's record ID.</span></span>

![흐름 recordId 및 계정 유형](./media/connectors-create-api-crmonline/recordid-type-user.png)

<span data-ttu-id="f6271-217">toofind 레코드의 ID를 hello 다음 단원을 참조 하십시오: *hello 레코드 ID 찾기*</span><span class="sxs-lookup"><span data-stu-id="f6271-217">toofind a record's ID, see hello following section: *Find hello record ID*</span></span>

## <a name="find-hello-record-id"></a><span data-ttu-id="f6271-218">Hello 레코드 ID 찾기</span><span class="sxs-lookup"><span data-stu-id="f6271-218">Find hello record ID</span></span>

1. <span data-ttu-id="f6271-219">계정 레코드 등의 레코드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-219">Open a record, such as an account record.</span></span>

2. <span data-ttu-id="f6271-220">Hello 작업 도구 모음에서 클릭 **팝아웃** ![팝아웃 레코드](./media/connectors-create-api-crmonline/popout-record.png)합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-220">On hello actions toolbar, click **Pop Out** ![popout record](./media/connectors-create-api-crmonline/popout-record.png).</span></span>
<span data-ttu-id="f6271-221">또는 기본 전자 메일 프로그램에 toocopy hello 전체 URL hello 작업 도구 모음에서 클릭 **전자 메일 링크**합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-221">Alternatively, on hello actions toolbar, toocopy hello full URL into your default email program, click **EMAIL A LINK**.</span></span>

   <span data-ttu-id="f6271-222">hello 레코드 ID hello %7b 및 %7 d hello URL의 문자를 인코딩할 사이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-222">hello record ID is displayed in between hello %7b and %7d encoding characters of hello URL.</span></span>

   ![흐름 recordId 및 계정 유형](./media/connectors-create-api-crmonline/recordid.png)

## <a name="troubleshooting"></a><span data-ttu-id="f6271-224">문제 해결</span><span class="sxs-lookup"><span data-stu-id="f6271-224">Troubleshooting</span></span>
<span data-ttu-id="f6271-225">tootroubleshoot 논리 앱 hello 이벤트의 hello 상태 세부 정보 보기에서에서 실패 한 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-225">tootroubleshoot a failed step in a logic app, view hello status details of hello event.</span></span>

1. <span data-ttu-id="f6271-226">**논리 앱** 아래에서 논리 앱을 선택한 다음 **개요**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-226">Under **Logic Apps**, select your logic app, and then click **Overview**.</span></span> 

   <span data-ttu-id="f6271-227">hello 요약 영역에 표시 되 고 hello 논리 앱에 대 한 hello 실행 상태를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-227">hello Summary area is shown and provides hello run status for hello logic app.</span></span> 

   ![논리 앱 실행 상태](./media/connectors-create-api-crmonline/tshoot1.png)

2. <span data-ttu-id="f6271-229">tooview 모든 실패 한 실행에 대 한 자세한 내용을 보려면 클릭 hello 실패 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-229">tooview more information about any failed runs, click hello failed event.</span></span> <span data-ttu-id="f6271-230">실패 한 단계로 tooexpand 해당 단계를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-230">tooexpand a failed step, click that step.</span></span>

   ![실패한 단계 확장](./media/connectors-create-api-crmonline/tshoot2.png)

   <span data-ttu-id="f6271-232">hello 단계의 세부 사항을 표시 되며 hello hello 오류 원인을 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-232">hello step details appear and can help troubleshoot hello cause of hello failure.</span></span>

   ![실패한 단계 세부 정보](./media/connectors-create-api-crmonline/tshoot3.png)

<span data-ttu-id="f6271-234">논리 앱 문제 해결에 대한 자세한 내용은 [논리 앱 오류 진단](../logic-apps/logic-apps-diagnosing-failures.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f6271-234">For more information about troubleshooting logic apps, see [Diagnosing logic app failures](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="f6271-235">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="f6271-235">Connector-specific details</span></span>

<span data-ttu-id="f6271-236">모든 트리거 및 hello swagger에 정의 된 작업을 확인 하 고 hello에 어떠한 제한도 볼 [connector 세부 정보](/connectors/crm/)합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-236">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/crm/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f6271-237">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f6271-237">Next steps</span></span>
<span data-ttu-id="f6271-238">탐색에서 논리 앱에서 사용할 수 있는 다른 커넥터 hello 우리의 [Api 목록](apis-list.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f6271-238">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
