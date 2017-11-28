---
title: "기업 (B2B) 메시지-Azure 논리 앱에 대 한 aaaCreate 파트너 | Microsoft Docs"
description: "엔터프라이즈 통합 팩 hello 및 논리 앱 tooadd 파트너 tooyour 통합을 고려 하는 방법에 대해 알아봅니다"
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
ms.openlocfilehash: 8dc70a8f441fcf228ed178029dcdbac940d794b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-update-partners-in-business-to-business-agreements-in-your-workflow"></a><span data-ttu-id="220fc-103">워크플로에서 기업 간 규약에 파트너 추가 또는 업데이트</span><span class="sxs-lookup"><span data-stu-id="220fc-103">Add or update partners in business-to-business agreements in your workflow</span></span>

<span data-ttu-id="220fc-104">파트너는 B2B(기업 간) 트랜잭션에 참여하고 서로 메시지를 교환하는 주체입니다.</span><span class="sxs-lookup"><span data-stu-id="220fc-104">Partners are entities that participate in business-to-business (B2B) transactions and exchange messages between each other.</span></span> <span data-ttu-id="220fc-105">사용자와 이러한 트랜잭션의 다른 조직을 나타내는 파트너를 만들려면 서로 전송한 메시지를 식별하고 유효성을 확인하는 정보를 공유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="220fc-105">Before you can create partners that represent you and another organization in these transactions, you must both share information that identifies and validates messages sent by each other.</span></span> <span data-ttu-id="220fc-106">통합 계정 toorepresent에서 파트너를 만들 수 있습니다 이러한 세부 정보를 설명 하 고 준비 toostart 비즈니스 관계는 둘 다 있습니다.</span><span class="sxs-lookup"><span data-stu-id="220fc-106">After you discuss these details and are ready toostart your business relationship, you can create partners in your integration account toorepresent you both.</span></span>

## <a name="what-roles-do-partners-have-in-your-integration-account"></a><span data-ttu-id="220fc-107">파트너는 통합 계정에서 어떤 역할을 갖나요?</span><span class="sxs-lookup"><span data-stu-id="220fc-107">What roles do partners have in your integration account?</span></span>

<span data-ttu-id="220fc-108">파트너 간에 교환 되는 hello 메시지에 대 한 toodefine 세부 정보를 해당 파트너 간의 규약을 만들 있습니다.</span><span class="sxs-lookup"><span data-stu-id="220fc-108">toodefine details about hello messages exchanged between partners, you create agreements between those partners.</span></span> <span data-ttu-id="220fc-109">그러나 규약을 만들 수 있습니다, 전에 선택 하 여 두 개 이상의 파트너 tooyour 통합 계정을 추가한 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="220fc-109">However, before you can create an agreement, you must have added at least two partners tooyour integration account.</span></span> <span data-ttu-id="220fc-110">조직으로 hello hello 계약의 일부 여야 합니다. **호스트 파트너**합니다.</span><span class="sxs-lookup"><span data-stu-id="220fc-110">Your organization must be part of hello agreement as hello **host partner**.</span></span> <span data-ttu-id="220fc-111">다른 파트너 hello 또는 **게스트 파트너** 나타냅니다 hello 조직 사용자의 조직과 메시지 교환입니다.</span><span class="sxs-lookup"><span data-stu-id="220fc-111">hello other partner, or **guest partner** represents hello organization that exchanges messages with your organization.</span></span> <span data-ttu-id="220fc-112">hello 게스트 파트너는 다른 회사 또는 조직에서 부서도 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="220fc-112">hello guest partner can be another company, or even a department in your own organization.</span></span>

<span data-ttu-id="220fc-113">이러한 파트너를 추가한 후에 규약을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="220fc-113">After you add these partners, you can create an agreement.</span></span>

<span data-ttu-id="220fc-114">수신 및 송신 설정은 hello 관점에서의 호스팅 파트너 hello 방향입니다.</span><span class="sxs-lookup"><span data-stu-id="220fc-114">Receive and Send settings are oriented from hello point of view of hello Hosted Partner.</span></span> <span data-ttu-id="220fc-115">예를 들어 hello 설정을 받으며 규약이 hello 호스팅된 파트너에서 게스트 파트너로 보내는 메시지를 수신 하는 방법을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="220fc-115">For example, hello receive settings in an agreement determine how hello hosted partner receives messages sent from a guest partner.</span></span> <span data-ttu-id="220fc-116">마찬가지로, hello 계약에 hello 송신 설정은 호스팅된 hello 파트너 toohello 게스트 파트너로 메시지를 보내는 방법을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="220fc-116">Likewise, hello send settings on hello agreement indicate how hello hosted partner sends messages toohello guest partner.</span></span>

## <a name="how-toocreate-a-partner"></a><span data-ttu-id="220fc-117">어떻게 toocreate 파트너?</span><span class="sxs-lookup"><span data-stu-id="220fc-117">How toocreate a partner?</span></span>

1. <span data-ttu-id="220fc-118">Hello Azure 포털에서에서 선택 **찾아보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="220fc-118">In hello Azure portal, select **Browse**.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. <span data-ttu-id="220fc-119">Hello 필터 검색 상자에 입력 **통합**을 선택한 후 **통합 계정** hello 결과 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="220fc-119">In hello filter search box, enter **integration**, then select **Integration Accounts** in hello results list.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. <span data-ttu-id="220fc-120">Hello 통합 계정을 저장할 tooadd 파트너를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="220fc-120">Select hello integration account where you want tooadd your partners.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="220fc-121">선택 hello **파트너** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="220fc-121">Select hello **Partners** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-1.png)

5. <span data-ttu-id="220fc-122">Hello 파트너 블레이드에서 선택 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="220fc-122">In hello Partners blade, choose **Add**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-2.png)

6. <span data-ttu-id="220fc-123">파트너의 이름을 입력하고 **한정자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="220fc-123">Enter a name for your partner, then select a **Qualifier**.</span></span> <span data-ttu-id="220fc-124">마지막으로 입력 한 **값** toohelp 앱에 제공 되는 문서를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="220fc-124">Finally, enter a **Value** toohelp identify documents that come into your apps.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-3.png)

7. <span data-ttu-id="220fc-125">파트너 만들기 프로세스에 선택 hello에 대 한 toosee hello 진행률 *벨* 알림 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="220fc-125">toosee hello progress for your partner creation process, select hello *bell* notification icon.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-4.png)

8. <span data-ttu-id="220fc-126">새 파트너 성공적으로 tooconfirm 추가, 선택 hello **파트너** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="220fc-126">tooconfirm that your new partners were successfully added, select hello **Partners** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-5.png)

    <span data-ttu-id="220fc-127">Hello 파트너 타일을 선택한 후 hello 파트너 블레이드에서 새로 추가 된 파트너에도 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="220fc-127">After you select hello Partners tile, you'll also see  newly added partners in hello Partners blade.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-6.png)

## <a name="how-tooedit-existing-partners-in-your-integration-account"></a><span data-ttu-id="220fc-128">통합 계정에서 파트너 tooedit 기존 방법</span><span class="sxs-lookup"><span data-stu-id="220fc-128">How tooedit existing partners in your integration account</span></span>

1. <span data-ttu-id="220fc-129">선택 hello **파트너** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="220fc-129">Select hello **Partners** tile.</span></span>
2. <span data-ttu-id="220fc-130">Hello 파트너 블레이드를 연 후 tooedit hello 파트너를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="220fc-130">After hello Partners blade opens, select hello partner you want tooedit.</span></span>
3. <span data-ttu-id="220fc-131">Hello에 **업데이트 파트너** 타일을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="220fc-131">On hello **Update Partner** tile, make your changes.</span></span>
4. <span data-ttu-id="220fc-132">을 마친 후에 선택할 **저장**, toocancel 변경 내용을 선택 또는 **취소**합니다.</span><span class="sxs-lookup"><span data-stu-id="220fc-132">After you're done, choose **Save**, or toocancel your changes, select **Discard**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/edit-1.png)

## <a name="how-toodelete-a-partner"></a><span data-ttu-id="220fc-133">어떻게 toodelete 파트너</span><span class="sxs-lookup"><span data-stu-id="220fc-133">How toodelete a partner</span></span>

1. <span data-ttu-id="220fc-134">선택 hello **파트너** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="220fc-134">Select hello **Partners** tile.</span></span>
2. <span data-ttu-id="220fc-135">Hello 파트너 블레이드를 연 후 toodelete hello 파트너를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="220fc-135">After hello Partner blade opens, select hello partner that you want toodelete.</span></span>
3. <span data-ttu-id="220fc-136">**삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="220fc-136">Choose **Delete**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/delete-1.png)

## <a name="next-steps"></a><span data-ttu-id="220fc-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="220fc-137">Next steps</span></span>
* [<span data-ttu-id="220fc-138">규약에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="220fc-138">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "엔터프라이즈 통합 규약에 대해 알아보기")  

