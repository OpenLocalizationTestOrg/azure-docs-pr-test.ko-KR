---
title: "B2B 엔터프라이즈 통합용 AS2 메시지 - Azure Logic Apps | Microsoft Docs"
description: "Azure Logic Apps과 B2B 엔터프라이즈 통합용 AS2 메시지 교환"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: c9b7e1a9-4791-474c-855f-988bd7bf4b7f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: LADocs; mandia
ms.openlocfilehash: 91b2f16611b88aa4b9395ca301d88042065ad9dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="exchange-as2-messages-for-enterprise-integration-with-logic-apps"></a><span data-ttu-id="ef281-103">논리 앱과 엔터프라이즈 통합용 AS2 메시지 교환</span><span class="sxs-lookup"><span data-stu-id="ef281-103">Exchange AS2 messages for enterprise integration with logic apps</span></span>

<span data-ttu-id="ef281-104">Azure Logic Apps의 AS2 메시지를 교환하기 전에 AS2 규약을 만들고 통합 계정에 해당 규약을 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-104">Before you can exchange AS2 messages for Azure Logic Apps, you must create an AS2 agreement and store that agreement in your integration account.</span></span> <span data-ttu-id="ef281-105">AS2 규약을 만드는 방법에 대한 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-105">Here are the steps for how to create an AS2 agreement.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="ef281-106">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="ef281-106">Before you start</span></span>

<span data-ttu-id="ef281-107">필요한 항목은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-107">Here's the items you need:</span></span>

* <span data-ttu-id="ef281-108">이미 정의되고 Azure 구독과 연결된 [통합 계정](../logic-apps/logic-apps-enterprise-integration-accounts.md)</span><span class="sxs-lookup"><span data-stu-id="ef281-108">An [integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md) that's already defined and associated with your Azure subscription</span></span>
* <span data-ttu-id="ef281-109">통합 계정에 정의되고 **비즈니스 ID** 아래에서 AS2 한정자를 사용하여 구성된 둘 이상의 [파트너](logic-apps-enterprise-integration-partners.md)</span><span class="sxs-lookup"><span data-stu-id="ef281-109">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account and configured with the AS2 qualifier under **Business Identities**</span></span>

> [!NOTE]
> <span data-ttu-id="ef281-110">규약을 만들 때 규약 파일의 내용이 규약 유형과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-110">When you create an agreement, the content in the agreement file must match the agreement type.</span></span>    

<span data-ttu-id="ef281-111">[통합 계정을 만들고](../logic-apps/logic-apps-enterprise-integration-accounts.md) [파트너를 추가](logic-apps-enterprise-integration-partners.md)한 후에 다음과 같은 단계에 따라 AS2 규약을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-111">After you [create an integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md) and [add partners](logic-apps-enterprise-integration-partners.md), you can create an AS2 agreement by following these steps.</span></span>

## <a name="create-an-as2-agreement"></a><span data-ttu-id="ef281-112">AS2 규약 만들기</span><span class="sxs-lookup"><span data-stu-id="ef281-112">Create an AS2 agreement</span></span>

1.  <span data-ttu-id="ef281-113">[Azure Portal](http://portal.azure.com "Azure Portal")에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-113">Sign in to the [Azure portal](http://portal.azure.com "Azure portal").</span></span>  

2.  <span data-ttu-id="ef281-114">왼쪽 메뉴에서 **추가 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-114">From the left menu, select **More services**.</span></span> <span data-ttu-id="ef281-115">검색 상자에서 필터에 **통합**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-115">In the search box, enter **integration** as your filter.</span></span> <span data-ttu-id="ef281-116">결과 목록에서 **통합 계정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-116">In the results list, select **Integration Accounts**.</span></span>

    > [!TIP]
    > <span data-ttu-id="ef281-117">**추가 서비스**가 표시되지 않으면 먼저 메뉴를 확장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-117">If you don't see **More services**, you might have to expand the menu first.</span></span> <span data-ttu-id="ef281-118">축소된 메뉴의 맨 위에 있는 **메뉴 표시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-118">At the top of the collapsed menu, select **Show menu**.</span></span>

    ![추가 서비스, "통합"에 대해 필터링하고 "통합 계정"을 선택합니다.](./media/logic-apps-enterprise-integration-agreements/overview-1.png)

3. <span data-ttu-id="ef281-120">열린 **통합 계정** 블레이드에서 규약을 만들려는 통합 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-120">In the **Integration Accounts** blade that opens, select the integration account where you want to create the agreement.</span></span>
<span data-ttu-id="ef281-121">통합 계정이 표시되지 않으면 [먼저 만듭니다](../logic-apps/logic-apps-enterprise-integration-accounts.md "통합 계정에 대한 모든 정보") 를.</span><span class="sxs-lookup"><span data-stu-id="ef281-121">If you don't see any integration accounts, [create one first](../logic-apps/logic-apps-enterprise-integration-accounts.md "All about integration accounts").</span></span>  

    ![규약을 만들 통합 계정 선택](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="ef281-123">**규약** 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-123">Choose the **Agreements** tile.</span></span> <span data-ttu-id="ef281-124">규약 타일이 없는 경우 먼저 타일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-124">If you don't have an Agreements tile, add the tile first.</span></span>

    !["규약" 타일 선택](./media/logic-apps-enterprise-integration-agreements/agreement-1.png)

5. <span data-ttu-id="ef281-126">열린 [규약] 블레이드에서 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-126">In the Agreements blade that opens, choose **Add**.</span></span>

    !["추가" 선택](./media/logic-apps-enterprise-integration-agreements/agreement-2.png)

6. <span data-ttu-id="ef281-128">**추가** 아래에서 규약의 **이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-128">Under **Add**, enter a **Name** for your agreement.</span></span> <span data-ttu-id="ef281-129">**규약 유형**에 **AS2**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-129">For **Agreement type**, select **AS2**.</span></span> <span data-ttu-id="ef281-130">규약의 **호스트 파트너**, **호스트 ID**, **게스트 파트너** 및 **게스트 ID**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-130">Select the **Host Partner**, **Host Identity**, **Guest Partner**, and **Guest Identity** for your agreement.</span></span>

    ![규약 세부 정보 제공](./media/logic-apps-enterprise-integration-agreements/agreement-3.png)  

    | <span data-ttu-id="ef281-132">속성</span><span class="sxs-lookup"><span data-stu-id="ef281-132">Property</span></span> | <span data-ttu-id="ef281-133">설명</span><span class="sxs-lookup"><span data-stu-id="ef281-133">Description</span></span> |
    | --- | --- |
    | <span data-ttu-id="ef281-134">이름</span><span class="sxs-lookup"><span data-stu-id="ef281-134">Name</span></span> |<span data-ttu-id="ef281-135">규약 이름</span><span class="sxs-lookup"><span data-stu-id="ef281-135">Name of the agreement</span></span> |
    | <span data-ttu-id="ef281-136">규약 유형</span><span class="sxs-lookup"><span data-stu-id="ef281-136">Agreement Type</span></span> | <span data-ttu-id="ef281-137">AS2여야 함</span><span class="sxs-lookup"><span data-stu-id="ef281-137">Should be AS2</span></span> |
    | <span data-ttu-id="ef281-138">호스트 파트너</span><span class="sxs-lookup"><span data-stu-id="ef281-138">Host Partner</span></span> |<span data-ttu-id="ef281-139">규약에는 호스트 및 게스트 파트너가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-139">An agreement needs both a host and guest partner.</span></span> <span data-ttu-id="ef281-140">호스트 파트너는 규약을 구성하는 조직을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-140">The host partner represents the organization that configures the agreement.</span></span> |
    | <span data-ttu-id="ef281-141">호스트 ID</span><span class="sxs-lookup"><span data-stu-id="ef281-141">Host Identity</span></span> |<span data-ttu-id="ef281-142">호스트 파트너의 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-142">An identifier for the host partner</span></span> |
    | <span data-ttu-id="ef281-143">게스트 파트너</span><span class="sxs-lookup"><span data-stu-id="ef281-143">Guest Partner</span></span> |<span data-ttu-id="ef281-144">규약에는 호스트 및 게스트 파트너가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-144">An agreement needs both a host and guest partner.</span></span> <span data-ttu-id="ef281-145">게스트 파트너는 호스트 파트너와 함께 일하는 조직을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-145">The guest partner represents the organization that's doing business with the host partner.</span></span> |
    | <span data-ttu-id="ef281-146">게스트 ID</span><span class="sxs-lookup"><span data-stu-id="ef281-146">Guest Identity</span></span> |<span data-ttu-id="ef281-147">게스트 파트너의 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-147">An identifier for the guest partner</span></span> |
    | <span data-ttu-id="ef281-148">수신 설정</span><span class="sxs-lookup"><span data-stu-id="ef281-148">Receive Settings</span></span> |<span data-ttu-id="ef281-149">규약에서 받은 모든 메시지에 이러한 속성을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-149">These properties apply to all messages received by an agreement.</span></span> |
    | <span data-ttu-id="ef281-150">송신 설정</span><span class="sxs-lookup"><span data-stu-id="ef281-150">Send Settings</span></span> |<span data-ttu-id="ef281-151">규약에서 보낸 모든 메시지에 이러한 속성을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-151">These properties apply to all messages sent by an agreement.</span></span> |

## <a name="configure-how-your-agreement-handles-received-messages"></a><span data-ttu-id="ef281-152">규약에서 수신된 메시지를 처리하는 방법 구성</span><span class="sxs-lookup"><span data-stu-id="ef281-152">Configure how your agreement handles received messages</span></span>

<span data-ttu-id="ef281-153">규약 속성을 설정했으므로 규약이 이 계약을 통해 파트너로부터 받은 들어오는 메시지를 식별하고 처리하는 방법을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-153">Now that you've set the agreement properties, you can configure how this agreement identifies and handles incoming messages received from your partner through this agreement.</span></span>

1.  <span data-ttu-id="ef281-154">**추가** 아래에서 **수신 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-154">Under **Add**, select **Receive Settings**.</span></span>
<span data-ttu-id="ef281-155">사용자와 메시지를 교환하는 파트너와의 규약에 따라 이러한 속성을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-155">Configure these properties based on your agreement with the partner that exchanges messages with you.</span></span> <span data-ttu-id="ef281-156">속성 설명은 이 섹션에 있는 테이블을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef281-156">For property descriptions, see the table in this section.</span></span>

    !["수신 설정" 구성](./media/logic-apps-enterprise-integration-agreements/agreement-4.png)

2. <span data-ttu-id="ef281-158">필요에 따라 **메시지 속성 재정의**를 선택하여 들어오는 메시지의 속성을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-158">Optionally, you can override the properties of incoming messages by selecting **Override message properties**.</span></span>

3. <span data-ttu-id="ef281-159">들어오는 모든 메시지를 서명하도록 요구하려면 **메시지 서명 필요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-159">To require all incoming messages to be signed, select **Message should be signed**.</span></span> <span data-ttu-id="ef281-160">[인증서](../logic-apps/logic-apps-enterprise-integration-certificates.md) 목록에서 기존 **게스트 파트너 공용 인증서**를 선택하여 메시지에 대한 서명의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-160">From the **Certificate** list, select an existing [guest partner public certificate](../logic-apps/logic-apps-enterprise-integration-certificates.md) for validating the signature on the messages.</span></span> <span data-ttu-id="ef281-161">또는 인증서가 하나도 없는 경우 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-161">Or create the certificate, if you don't have one.</span></span>

4.  <span data-ttu-id="ef281-162">들어오는 모든 메시지를 암호화하도록 요구하려면 **메시지 암호화 필요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-162">To require all incoming messages to be encrypted, select **Message should be encrypted**.</span></span> <span data-ttu-id="ef281-163">**인증서** 목록에서 기존 [호스트 파트너 개인 인증서](../logic-apps/logic-apps-enterprise-integration-certificates.md)를 선택하여 들어오는 메시지를 암호 해독합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-163">From the **Certificate** list, select an existing [host partner private certificate](../logic-apps/logic-apps-enterprise-integration-certificates.md) for decrypting incoming messages.</span></span> <span data-ttu-id="ef281-164">또는 인증서가 하나도 없는 경우 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-164">Or create the certificate, if you don't have one.</span></span>

5. <span data-ttu-id="ef281-165">메시지를 압축하도록 요구하려면 **메시지 압축 필요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-165">To require messages to be compressed, select **Message should be compressed**.</span></span>

6. <span data-ttu-id="ef281-166">받은 메시지에 대한 동기 MDN(메시지 처리 알림)을 보내려면 **MDN 보내기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-166">To send a synchronous message disposition notification (MDN) for received messages, select **Send MDN**.</span></span>

7. <span data-ttu-id="ef281-167">받은 메시지에 대한 서명된 MDN을 보내려면 **서명된 MDN 보내기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-167">To send signed MDNs for received messages, select **Send signed MDN**.</span></span>

8. <span data-ttu-id="ef281-168">받은 메시지에 대한 비동기 MDN을 보내려면 **비동기 MDN 보내기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-168">To send asynchronous MDNs for received messages, select **Send asynchronous MDN**.</span></span>

9. <span data-ttu-id="ef281-169">작업을 마친 후에 **확인**을 선택하여 설정을 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-169">After you're done, make sure to save your settings by choosing **OK**.</span></span>

<span data-ttu-id="ef281-170">이제 규약은 선택한 설정에 맞는 들어오는 메시지를 처리할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-170">Now your agreement is ready to handle incoming messages that conform to your selected settings.</span></span>

| <span data-ttu-id="ef281-171">속성</span><span class="sxs-lookup"><span data-stu-id="ef281-171">Property</span></span> | <span data-ttu-id="ef281-172">설명</span><span class="sxs-lookup"><span data-stu-id="ef281-172">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ef281-173">메시지 속성 재정의</span><span class="sxs-lookup"><span data-stu-id="ef281-173">Override message properties</span></span> |<span data-ttu-id="ef281-174">받은 메시지의 속성을 재정의할 수 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-174">Indicates that properties in received messages can be overridden.</span></span> |
| <span data-ttu-id="ef281-175">메시지 서명 필요</span><span class="sxs-lookup"><span data-stu-id="ef281-175">Message should be signed</span></span> |<span data-ttu-id="ef281-176">메시지를 디지털로 서명하도록 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-176">Requires messages to be digitally signed.</span></span> <span data-ttu-id="ef281-177">서명 확인을 위한 게스트 파트너 공용 인증서를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-177">Configure the guest partner public certificate for signature verification.</span></span>  |
| <span data-ttu-id="ef281-178">메시지 암호화 필요</span><span class="sxs-lookup"><span data-stu-id="ef281-178">Message should be encrypted</span></span> |<span data-ttu-id="ef281-179">메시지를 암호화하도록 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-179">Requires messages to be encrypted.</span></span> <span data-ttu-id="ef281-180">암호화되지 않은 메시지는 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-180">Non-encrypted messages are rejected.</span></span> <span data-ttu-id="ef281-181">메시지 암호를 해독하기 위한 호스트 파트너 개인 인증서를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-181">Configure the host partner private certificate for decrypting the messages.</span></span>  |
| <span data-ttu-id="ef281-182">메시지 압축 필요</span><span class="sxs-lookup"><span data-stu-id="ef281-182">Message should be compressed</span></span> |<span data-ttu-id="ef281-183">메시지를 압축하도록 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-183">Requires messages to be compressed.</span></span> <span data-ttu-id="ef281-184">압축되지 않은 메시지는 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-184">Non-compressed messages are rejected.</span></span> |
| <span data-ttu-id="ef281-185">MDN 텍스트</span><span class="sxs-lookup"><span data-stu-id="ef281-185">MDN Text</span></span> |<span data-ttu-id="ef281-186">메시지 보낸 사람에게 보낼 기본 MDN(메시지 처리 알림)입니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-186">The default message disposition notification (MDN) to be sent to the message sender.</span></span> |
| <span data-ttu-id="ef281-187">MDN 전송</span><span class="sxs-lookup"><span data-stu-id="ef281-187">Send MDN</span></span> |<span data-ttu-id="ef281-188">MDN을 보내도록 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-188">Requires MDNs to be sent.</span></span> |
| <span data-ttu-id="ef281-189">서명된 MDN 전송</span><span class="sxs-lookup"><span data-stu-id="ef281-189">Send signed MDN</span></span> |<span data-ttu-id="ef281-190">MDN을 서명하도록 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-190">Requires MDNs to be signed.</span></span> |
| <span data-ttu-id="ef281-191">MIC 알고리즘</span><span class="sxs-lookup"><span data-stu-id="ef281-191">MIC Algorithm</span></span> |<span data-ttu-id="ef281-192">메시지 서명에 사용할 알고리즘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-192">Select the algorithm to use for signing messages.</span></span> |
| <span data-ttu-id="ef281-193">비동기 MDN 전송</span><span class="sxs-lookup"><span data-stu-id="ef281-193">Send asynchronous MDN</span></span> | <span data-ttu-id="ef281-194">메시지를 비동기적으로 보내도록 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-194">Requires messages to be sent asynchronously.</span></span> |
| <span data-ttu-id="ef281-195">URL</span><span class="sxs-lookup"><span data-stu-id="ef281-195">URL</span></span> | <span data-ttu-id="ef281-196">MDN을 보낼 URL을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-196">Specify the URL where to send the MDNs.</span></span> |

## <a name="configure-how-your-agreement-sends-messages"></a><span data-ttu-id="ef281-197">규약에서 메시지를 보내는 방법 구성</span><span class="sxs-lookup"><span data-stu-id="ef281-197">Configure how your agreement sends messages</span></span>

<span data-ttu-id="ef281-198">이 규약이 규약을 통해 파트너에게 보내는 메시지를 식별하고 처리하는 방법을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-198">You can configure how this agreement identifies and handles outgoing messages that you send to your partners through this agreement.</span></span>

1.  <span data-ttu-id="ef281-199">**추가** 아래에서 **송신 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-199">Under **Add**, select **Send Settings**.</span></span>
<span data-ttu-id="ef281-200">사용자와 메시지를 교환하는 파트너와의 규약에 따라 이러한 속성을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-200">Configure these properties based on your agreement with the partner that exchanges messages with you.</span></span> <span data-ttu-id="ef281-201">속성 설명은 이 섹션에 있는 테이블을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef281-201">For property descriptions, see the table in this section.</span></span>

    !["설정 보내기" 속성 설정](./media/logic-apps-enterprise-integration-agreements/agreement-51.png)

2. <span data-ttu-id="ef281-203">파트너에게 서명된 메시지를 보내려면 **메시지 서명 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-203">To send signed messages to your partner, select **Enable message signing**.</span></span> <span data-ttu-id="ef281-204">메시지에 서명하려면 **MIC Algorithm** 목록에서 *호스트 파트너 개인 인증서 MIC 알고리즘*을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-204">For signing the messages, in the **MIC Algorithm** list, select the *host partner private certificate MIC Algorithm*.</span></span> <span data-ttu-id="ef281-205">그리고 **인증서** 목록에서 기존 [호스트 파트너 개인 인증서](../logic-apps/logic-apps-enterprise-integration-certificates.md)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-205">And in the **Certificate** list, select an existing [host partner private certificate](../logic-apps/logic-apps-enterprise-integration-certificates.md).</span></span>

3. <span data-ttu-id="ef281-206">파트너에게 암호화된 메시지를 보내려면 **메시지 암호화 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-206">To send encrypted messages to the partner, select **Enable message encryption**.</span></span> <span data-ttu-id="ef281-207">메시지를 암호화하기 위해 **암호화 알고리즘** 목록에서 *게스트 파트너 공용 인증서 알고리즘*을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-207">For encrypting the messages, in the **Encryption Algorithm** list, select the *guest partner public certificate algorithm*.</span></span>
<span data-ttu-id="ef281-208">그리고 **인증서** 목록에서 기존 [게스트 파트너 공용 인증서](../logic-apps/logic-apps-enterprise-integration-certificates.md)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-208">And in the **Certificate** list, select an existing [guest partner public certificate](../logic-apps/logic-apps-enterprise-integration-certificates.md).</span></span>

4. <span data-ttu-id="ef281-209">메시지를 압축하려면 **메시지 압축 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-209">To compress the message, select **Enable message compression**.</span></span>

5. <span data-ttu-id="ef281-210">HTTP 콘텐츠 형식 헤더를 단일 줄로 펼치려면 **HTTP 헤더 펼침**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-210">To unfold the HTTP content-type header into a single line, select **Unfold HTTP headers**.</span></span>

6. <span data-ttu-id="ef281-211">보낸 메시지에 대한 동기 MDN을 받으려면 **MDN 요청**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-211">To receive synchronous MDNs for the sent messages, select **Request MDN**.</span></span>

7. <span data-ttu-id="ef281-212">보낸 메시지에 대한 서명된 MDN을 받으려면 **서명된 MDN 요청**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-212">To receive signed MDNs for the sent messages, select **Request signed MDN**.</span></span>

8. <span data-ttu-id="ef281-213">보낸 메시지에 대한 동기 MDN을 받으려면 **비동기 MDN 요청**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-213">To receive asynchronous MDNs for the sent messages, select **Request asynchronous MDN**.</span></span> <span data-ttu-id="ef281-214">이 옵션을 선택하면 MDN을 보낼 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-214">If you select this option, enter the URL for where to send the MDNs.</span></span>

9. <span data-ttu-id="ef281-215">NRR(수신 거부 없음)을 요구하려면 **NRR 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-215">To require non-repudiation of receipt, select **Enable NRR**.</span></span>  

10. <span data-ttu-id="ef281-216">MIC에서 사용할 알고리즘 형식을 지정하거나 AS2 메시지 또는 MDN의 나가는 헤더에서 서명하려면 **SHA2 알고리즘 형식**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-216">To specify algorithm format to use in the MIC or signing in the outgoing headers of the AS2 message or MDN, select **SHA2 Algorithm format**.</span></span>  

11. <span data-ttu-id="ef281-217">작업을 마친 후에 **확인**을 선택하여 설정을 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-217">After you're done, make sure to save your settings by choosing **OK**.</span></span>

<span data-ttu-id="ef281-218">이제 규약은 선택한 설정에 맞는 보내는 메시지를 처리할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-218">Now your agreement is ready to handle outgoing messages that conform to your selected settings.</span></span>

| <span data-ttu-id="ef281-219">속성</span><span class="sxs-lookup"><span data-stu-id="ef281-219">Property</span></span> | <span data-ttu-id="ef281-220">설명</span><span class="sxs-lookup"><span data-stu-id="ef281-220">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ef281-221">메시지 서명 사용</span><span class="sxs-lookup"><span data-stu-id="ef281-221">Enable message signing</span></span> |<span data-ttu-id="ef281-222">규약에서 보낸 모든 메시지를 서명하도록 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-222">Requires all messages that are sent from the agreement to be signed.</span></span> |
| <span data-ttu-id="ef281-223">MIC 알고리즘</span><span class="sxs-lookup"><span data-stu-id="ef281-223">MIC Algorithm</span></span> |<span data-ttu-id="ef281-224">메시지 서명에 사용할 알고리즘입니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-224">The algorithm to use for signing messages.</span></span> <span data-ttu-id="ef281-225">메시지에 서명하기 위한 호스트 파트너 개인 인증서 MIC 알고리즘을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-225">Configures the host partner private certificate MIC Algorithm for signing the messages.</span></span> |
| <span data-ttu-id="ef281-226">인증서</span><span class="sxs-lookup"><span data-stu-id="ef281-226">Certificate</span></span> |<span data-ttu-id="ef281-227">메시지 서명에 사용할 인증서를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-227">Select the certificate to use for signing messages.</span></span> <span data-ttu-id="ef281-228">메시지에 서명하기 위한 호스트 파트너 개인 인증서를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-228">Configures the host partner private certificate for signing the messages.</span></span> |
| <span data-ttu-id="ef281-229">메시지 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="ef281-229">Enable message encryption</span></span> |<span data-ttu-id="ef281-230">이 규약에서 보낸 모든 메시지를 암호화하도록 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-230">Requires encryption of all messages that are sent from this agreement.</span></span> <span data-ttu-id="ef281-231">메시지를 암호화하기 위한 게스트 파트너 공용 인증서 알고리즘을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-231">Configures the guest partner public certificate algorithm for encrypting the messages.</span></span> |
| <span data-ttu-id="ef281-232">암호화 알고리즘</span><span class="sxs-lookup"><span data-stu-id="ef281-232">Encryption Algorithm</span></span> |<span data-ttu-id="ef281-233">메시지 암호화에 사용할 암호화 알고리즘입니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-233">The encryption algorithm to use for message encryption.</span></span> <span data-ttu-id="ef281-234">메시지를 암호화하기 위한 게스트 파트너 공용 인증서를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-234">Configures the guest partner public certificate for encrypting the messages.</span></span> |
| <span data-ttu-id="ef281-235">인증서</span><span class="sxs-lookup"><span data-stu-id="ef281-235">Certificate</span></span> |<span data-ttu-id="ef281-236">메시지를 암호화하는 데 사용할 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-236">The certificate to use to encrypt messages.</span></span> <span data-ttu-id="ef281-237">메시지를 암호화하기 위한 게스트 파트너 개인 인증서를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-237">Configures the guest partner private certificate for encrypting the messages.</span></span> |
| <span data-ttu-id="ef281-238">메시지 압축 사용</span><span class="sxs-lookup"><span data-stu-id="ef281-238">Enable message compression</span></span> |<span data-ttu-id="ef281-239">이 규약에서 보낸 모든 메시지를 압축하도록 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-239">Requires compression of all messages that are sent from this agreement.</span></span> |
| <span data-ttu-id="ef281-240">HTTP 헤더 펼침</span><span class="sxs-lookup"><span data-stu-id="ef281-240">Unfold HTTP headers</span></span> |<span data-ttu-id="ef281-241">HTTP content-type 헤더를 한 줄에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-241">Places the HTTP content-type header onto a single line.</span></span> |
| <span data-ttu-id="ef281-242">MDN 요청</span><span class="sxs-lookup"><span data-stu-id="ef281-242">Request MDN</span></span> |<span data-ttu-id="ef281-243">이 규약에서 보낸 모든 메시지에 대한 MDN을 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-243">Requires an MDN for all messages that are sent from this agreement.</span></span> |
| <span data-ttu-id="ef281-244">서명된 MDN 요청</span><span class="sxs-lookup"><span data-stu-id="ef281-244">Request signed MDN</span></span> |<span data-ttu-id="ef281-245">이 규약으로 보내는 모든 MDN을 서명하도록 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-245">Requires all MDNs that are sent to this agreement to be signed.</span></span> |
| <span data-ttu-id="ef281-246">비동기 MDN 요청</span><span class="sxs-lookup"><span data-stu-id="ef281-246">Request asynchronous MDN</span></span> |<span data-ttu-id="ef281-247">이 규약으로 비동기 MDN을 보내도록 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-247">Requires asynchronous MDNs to be sent to this agreement.</span></span> |
| <span data-ttu-id="ef281-248">URL</span><span class="sxs-lookup"><span data-stu-id="ef281-248">URL</span></span> |<span data-ttu-id="ef281-249">MDN을 보낼 URL을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-249">Specify the URL where to send the MDNs.</span></span> |
| <span data-ttu-id="ef281-250">NRR 사용</span><span class="sxs-lookup"><span data-stu-id="ef281-250">Enable NRR</span></span> |<span data-ttu-id="ef281-251">지정된 대로 데이터를 받았다는 증명 정보를 제공하는 통신 특성인 NRR(수신 거부 없음)을 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-251">Requires non-repudiation of receipt (NRR), a communication attribute that provides evidence that the data was received as addressed.</span></span> |
| <span data-ttu-id="ef281-252">SHA2 알고리즘 형식</span><span class="sxs-lookup"><span data-stu-id="ef281-252">SHA2 Algorithm format</span></span> |<span data-ttu-id="ef281-253">MIC에서 사용할 알고리즘 형식을 선택하거나 AS2 메시지 또는 MDN의 나가는 헤더에 서명합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-253">Select algorithm format to use in the MIC or signing in the outgoing headers of the AS2 message or MDN</span></span> |

## <a name="find-your-created-agreement"></a><span data-ttu-id="ef281-254">생성된 규약 찾기</span><span class="sxs-lookup"><span data-stu-id="ef281-254">Find your created agreement</span></span>

1.  <span data-ttu-id="ef281-255">모든 규약 속성 설정을 완료한 후에 **추가** 블레이드에서 **확인**을 선택하여 규약 만들기를 완료하고 사용자 통합 계정 블레이드로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-255">After you finish setting all your agreement properties, on the **Add** blade, choose **OK** to finish creating your agreement and return to your integration account blade.</span></span>

    <span data-ttu-id="ef281-256">이제 새로 추가된 규약이 **규약** 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-256">Your newly added agreement now appears in your **Agreements** list.</span></span>

2.  <span data-ttu-id="ef281-257">또한 통합 계정 개요에서 규약을 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-257">You can also view your agreements in your integration account overview.</span></span> <span data-ttu-id="ef281-258">통합 사용자 계정 블레이드에서 **개요**를 선택한 다음 **규약** 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef281-258">On your integration account blade, choose **Overview**, then select the **Agreements** tile.</span></span> 

    ![모든 규약을 보려면 "규약" 타일을 선택합니다](./media/logic-apps-enterprise-integration-agreements/agreement-6.png)

## <a name="view-the-swagger"></a><span data-ttu-id="ef281-260">swagger 보기</span><span class="sxs-lookup"><span data-stu-id="ef281-260">View the swagger</span></span>
<span data-ttu-id="ef281-261">[swagger 정보](/connectors/as2/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef281-261">See the [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ef281-262">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ef281-262">Next steps</span></span>
* [<span data-ttu-id="ef281-263">엔터프라이즈 통합 팩에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="ef281-263">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "엔터프라이즈 통합 팩에 대해 알아보기")  
