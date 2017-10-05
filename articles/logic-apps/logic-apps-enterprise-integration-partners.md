---
title: "B2B(기업 간) 메시지에 대해 파트너 만들기 - Azure Logic Apps | Microsoft Docs"
description: "엔터프라이즈 통합 팩 및 Logic Apps와 통합 계정에 파트너를 추가하는 방법 알아보기"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: b179325c-a511-4c1b-9796-f7484b4f6873
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 950cb449b53f400f0f0f860caf5415bbb5212269
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="add-or-update-partners-in-business-to-business-agreements-in-your-workflow"></a><span data-ttu-id="04efe-103">워크플로에서 기업 간 규약에 파트너 추가 또는 업데이트</span><span class="sxs-lookup"><span data-stu-id="04efe-103">Add or update partners in business-to-business agreements in your workflow</span></span>

<span data-ttu-id="04efe-104">파트너는 B2B(기업 간) 트랜잭션에 참여하고 서로 메시지를 교환하는 주체입니다.</span><span class="sxs-lookup"><span data-stu-id="04efe-104">Partners are entities that participate in business-to-business (B2B) transactions and exchange messages between each other.</span></span> <span data-ttu-id="04efe-105">사용자와 이러한 트랜잭션의 다른 조직을 나타내는 파트너를 만들려면 서로 전송한 메시지를 식별하고 유효성을 확인하는 정보를 공유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efe-105">Before you can create partners that represent you and another organization in these transactions, you must both share information that identifies and validates messages sent by each other.</span></span> <span data-ttu-id="04efe-106">이러한 세부 정보를 확인하고 비즈니스 관계를 시작할 준비가 되면 통합 계정에 쌍방을 나타내는 파트너를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04efe-106">After you discuss these details and are ready to start your business relationship, you can create partners in your integration account to represent you both.</span></span>

## <a name="what-roles-do-partners-have-in-your-integration-account"></a><span data-ttu-id="04efe-107">파트너는 통합 계정에서 어떤 역할을 갖나요?</span><span class="sxs-lookup"><span data-stu-id="04efe-107">What roles do partners have in your integration account?</span></span>

<span data-ttu-id="04efe-108">파트너 간에 교환되는 메시지에 대한 세부 정보를 정의하려면 해당 파트너 간의 규약을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="04efe-108">To define details about the messages exchanged between partners, you create agreements between those partners.</span></span> <span data-ttu-id="04efe-109">그러나 규약을 만들기 전에 통합 계정에 둘 이상의 파트너를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efe-109">However, before you can create an agreement, you must have added at least two partners to your integration account.</span></span> <span data-ttu-id="04efe-110">조직은 **호스트 파트너**로서 규약에 속해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efe-110">Your organization must be part of the agreement as the **host partner**.</span></span> <span data-ttu-id="04efe-111">다른 파트너 또는 **게스트 파트너**는 사용자 조직과 메시지를 교환하는 조직을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="04efe-111">The other partner, or **guest partner** represents the organization that exchanges messages with your organization.</span></span> <span data-ttu-id="04efe-112">게스트 파트너는 다른 회사 또는 조직 내 다른 부서일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04efe-112">The guest partner can be another company, or even a department in your own organization.</span></span>

<span data-ttu-id="04efe-113">이러한 파트너를 추가한 후에 규약을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04efe-113">After you add these partners, you can create an agreement.</span></span>

<span data-ttu-id="04efe-114">수신 및 송신 설정은 호스트 파트너의 관점에서 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="04efe-114">Receive and Send settings are oriented from the point of view of the Hosted Partner.</span></span> <span data-ttu-id="04efe-115">예를 들어 규약의 수신 설정은 호스트 파트너가 게스트 파트너로부터 받은 메시지를 수신하는 방법을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="04efe-115">For example, the receive settings in an agreement determine how the hosted partner receives messages sent from a guest partner.</span></span> <span data-ttu-id="04efe-116">마찬가지로, 규약의 송신 설정은 호스트 파트너가 게스트 파트너에게 메시지를 보내는 방법을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="04efe-116">Likewise, the send settings on the agreement indicate how the hosted partner sends messages to the guest partner.</span></span>

## <a name="how-to-create-a-partner"></a><span data-ttu-id="04efe-117">파트너를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="04efe-117">How to create a partner?</span></span>

1. <span data-ttu-id="04efe-118">Azure Portal에서 **찾아보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="04efe-118">In the Azure portal, select **Browse**.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. <span data-ttu-id="04efe-119">필터 검색 상자에 **통합**을 입력하고 결과 목록에서 **통합 계정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="04efe-119">In the filter search box, enter **integration**, then select **Integration Accounts** in the results list.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. <span data-ttu-id="04efe-120">파트너를 추가할 통합 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="04efe-120">Select the integration account where you want to add your partners.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="04efe-121">**파트너** 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="04efe-121">Select the **Partners** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-1.png)

5. <span data-ttu-id="04efe-122">파트너 블레이드에서 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="04efe-122">In the Partners blade, choose **Add**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-2.png)

6. <span data-ttu-id="04efe-123">파트너의 이름을 입력하고 **한정자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="04efe-123">Enter a name for your partner, then select a **Qualifier**.</span></span> <span data-ttu-id="04efe-124">마지막으로 앱에 들어오는 문서를 식별하는 데 도움이 되는 **값**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="04efe-124">Finally, enter a **Value** to help identify documents that come into your apps.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-3.png)

7. <span data-ttu-id="04efe-125">파트너 생성 프로세스의 진행 상태를 확인하려면 *벨* 알림 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="04efe-125">To see the progress for your partner creation process, select the *bell* notification icon.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-4.png)

8. <span data-ttu-id="04efe-126">새 파트너가 성공적으로 추가되었는지 확인하려면 **파트너** 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="04efe-126">To confirm that your new partners were successfully added, select the **Partners** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-5.png)

    <span data-ttu-id="04efe-127">파트너 타일을 선택한 후에 새로 추가된 파트너가 파트너 블레이드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="04efe-127">After you select the Partners tile, you'll also see  newly added partners in the Partners blade.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-6.png)

## <a name="how-to-edit-existing-partners-in-your-integration-account"></a><span data-ttu-id="04efe-128">통합 계정에서 기존 파트너를 편집하는 방법</span><span class="sxs-lookup"><span data-stu-id="04efe-128">How to edit existing partners in your integration account</span></span>

1. <span data-ttu-id="04efe-129">**파트너** 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="04efe-129">Select the **Partners** tile.</span></span>
2. <span data-ttu-id="04efe-130">파트너 블레이드가 열리면 편집할 파트너를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="04efe-130">After the Partners blade opens, select the partner you want to edit.</span></span>
3. <span data-ttu-id="04efe-131">**파트너 업데이트** 타일에서 필요한 내용을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="04efe-131">On the **Update Partner** tile, make your changes.</span></span>
4. <span data-ttu-id="04efe-132">작업을 마친 후에 **저장**을 선택하고, 변경 내용을 취소하려면 **취소**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="04efe-132">After you're done, choose **Save**, or to cancel your changes, select **Discard**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/edit-1.png)

## <a name="how-to-delete-a-partner"></a><span data-ttu-id="04efe-133">파트너 삭제 방법</span><span class="sxs-lookup"><span data-stu-id="04efe-133">How to delete a partner</span></span>

1. <span data-ttu-id="04efe-134">**파트너** 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="04efe-134">Select the **Partners** tile.</span></span>
2. <span data-ttu-id="04efe-135">파트너 블레이드가 열리면 삭제할 파트너를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="04efe-135">After the Partner blade opens, select the partner that you want to delete.</span></span>
3. <span data-ttu-id="04efe-136">**삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="04efe-136">Choose **Delete**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/delete-1.png)

## <a name="next-steps"></a><span data-ttu-id="04efe-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="04efe-137">Next steps</span></span>
* [<span data-ttu-id="04efe-138">규약에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="04efe-138">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "엔터프라이즈 통합 규약에 대해 알아보기")  

