---
title: "B2B 엔터프라이즈 통합-Azure 논리 앱에 대 한 aaaAS2 메시지 | Microsoft Docs"
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
ms.openlocfilehash: 23f9d74dd0ad807e9cdaedb320d60496cfef9bc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="exchange-as2-messages-for-enterprise-integration-with-logic-apps"></a><span data-ttu-id="1ed72-103">논리 앱과 엔터프라이즈 통합용 AS2 메시지 교환</span><span class="sxs-lookup"><span data-stu-id="1ed72-103">Exchange AS2 messages for enterprise integration with logic apps</span></span>

<span data-ttu-id="1ed72-104">Azure Logic Apps의 AS2 메시지를 교환하기 전에 AS2 규약을 만들고 통합 계정에 해당 규약을 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-104">Before you can exchange AS2 messages for Azure Logic Apps, you must create an AS2 agreement and store that agreement in your integration account.</span></span> <span data-ttu-id="1ed72-105">다음은 방법에 대 한 hello 단계 toocreate AS2 계약입니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-105">Here are hello steps for how toocreate an AS2 agreement.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="1ed72-106">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="1ed72-106">Before you start</span></span>

<span data-ttu-id="1ed72-107">다음은 필요한 hello 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-107">Here's hello items you need:</span></span>

* <span data-ttu-id="1ed72-108">이미 정의되고 Azure 구독과 연결된 [통합 계정](../logic-apps/logic-apps-enterprise-integration-accounts.md)</span><span class="sxs-lookup"><span data-stu-id="1ed72-108">An [integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md) that's already defined and associated with your Azure subscription</span></span>
* <span data-ttu-id="1ed72-109">두 개 이상의 [파트너](logic-apps-enterprise-integration-partners.md) 이미 통합 계정에 정의 되 고 아래에서 AS2 hello 한정자를 사용 하 여 구성 **비즈니스 Id**</span><span class="sxs-lookup"><span data-stu-id="1ed72-109">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account and configured with hello AS2 qualifier under **Business Identities**</span></span>

> [!NOTE]
> <span data-ttu-id="1ed72-110">규약을 만들 때 hello 계약 파일의 hello 콘텐츠 hello 계약 형식과 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-110">When you create an agreement, hello content in hello agreement file must match hello agreement type.</span></span>    

<span data-ttu-id="1ed72-111">[통합 계정을 만들고](../logic-apps/logic-apps-enterprise-integration-accounts.md) [파트너를 추가](logic-apps-enterprise-integration-partners.md)한 후에 다음과 같은 단계에 따라 AS2 규약을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-111">After you [create an integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md) and [add partners](logic-apps-enterprise-integration-partners.md), you can create an AS2 agreement by following these steps.</span></span>

## <a name="create-an-as2-agreement"></a><span data-ttu-id="1ed72-112">AS2 규약 만들기</span><span class="sxs-lookup"><span data-stu-id="1ed72-112">Create an AS2 agreement</span></span>

1.  <span data-ttu-id="1ed72-113">Toohello 로그인 [Azure 포털](http://portal.azure.com "Azure 포털")합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-113">Sign in toohello [Azure portal](http://portal.azure.com "Azure portal").</span></span>  

2.  <span data-ttu-id="1ed72-114">Hello 왼쪽된 메뉴에서 선택 **더 많은 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-114">From hello left menu, select **More services**.</span></span> <span data-ttu-id="1ed72-115">Hello 검색 상자에 입력 **통합** 필터로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-115">In hello search box, enter **integration** as your filter.</span></span> <span data-ttu-id="1ed72-116">Hello 결과 목록에서 선택 **통합 계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-116">In hello results list, select **Integration Accounts**.</span></span>

    > [!TIP]
    > <span data-ttu-id="1ed72-117">표시 되지 않으면 **더 많은 서비스**, 먼저 tooexpand hello 메뉴를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-117">If you don't see **More services**, you might have tooexpand hello menu first.</span></span> <span data-ttu-id="1ed72-118">축소 된 hello 메뉴의 hello 위쪽 선택 **표시 메뉴**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-118">At hello top of hello collapsed menu, select **Show menu**.</span></span>

    ![추가 서비스, "통합"에 대해 필터링하고 "통합 계정"을 선택합니다.](./media/logic-apps-enterprise-integration-agreements/overview-1.png)

3. <span data-ttu-id="1ed72-120">Hello에 **통합 계정** 블레이드 열리면 toocreate hello 계약 원하는 선택 hello 통합 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-120">In hello **Integration Accounts** blade that opens, select hello integration account where you want toocreate hello agreement.</span></span>
<span data-ttu-id="1ed72-121">통합 계정이 표시되지 않으면 [먼저 만듭니다](../logic-apps/logic-apps-enterprise-integration-accounts.md "통합 계정에 대한 모든 정보") 를.</span><span class="sxs-lookup"><span data-stu-id="1ed72-121">If you don't see any integration accounts, [create one first](../logic-apps/logic-apps-enterprise-integration-accounts.md "All about integration accounts").</span></span>  

    ![여기서 toocreate hello 계약 hello 통합 계정 선택](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="1ed72-123">Hello 선택 **계약** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-123">Choose hello **Agreements** tile.</span></span> <span data-ttu-id="1ed72-124">계약 타일 없다면 먼저 hello 타일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-124">If you don't have an Agreements tile, add hello tile first.</span></span>

    !["규약" 타일 선택](./media/logic-apps-enterprise-integration-agreements/agreement-1.png)

5. <span data-ttu-id="1ed72-126">열리면 hello 계약 블레이드에서 선택 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-126">In hello Agreements blade that opens, choose **Add**.</span></span>

    !["추가" 선택](./media/logic-apps-enterprise-integration-agreements/agreement-2.png)

6. <span data-ttu-id="1ed72-128">**추가** 아래에서 규약의 **이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-128">Under **Add**, enter a **Name** for your agreement.</span></span> <span data-ttu-id="1ed72-129">**규약 유형**에 **AS2**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-129">For **Agreement type**, select **AS2**.</span></span> <span data-ttu-id="1ed72-130">선택 hello **호스트 파트너**, **호스트 Id**, **게스트 파트너**, 및 **게스트 Identity** 의 계약에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-130">Select hello **Host Partner**, **Host Identity**, **Guest Partner**, and **Guest Identity** for your agreement.</span></span>

    ![규약 세부 정보 제공](./media/logic-apps-enterprise-integration-agreements/agreement-3.png)  

    | <span data-ttu-id="1ed72-132">속성</span><span class="sxs-lookup"><span data-stu-id="1ed72-132">Property</span></span> | <span data-ttu-id="1ed72-133">설명</span><span class="sxs-lookup"><span data-stu-id="1ed72-133">Description</span></span> |
    | --- | --- |
    | <span data-ttu-id="1ed72-134">이름</span><span class="sxs-lookup"><span data-stu-id="1ed72-134">Name</span></span> |<span data-ttu-id="1ed72-135">Hello 계약의 이름</span><span class="sxs-lookup"><span data-stu-id="1ed72-135">Name of hello agreement</span></span> |
    | <span data-ttu-id="1ed72-136">규약 유형</span><span class="sxs-lookup"><span data-stu-id="1ed72-136">Agreement Type</span></span> | <span data-ttu-id="1ed72-137">AS2여야 함</span><span class="sxs-lookup"><span data-stu-id="1ed72-137">Should be AS2</span></span> |
    | <span data-ttu-id="1ed72-138">호스트 파트너</span><span class="sxs-lookup"><span data-stu-id="1ed72-138">Host Partner</span></span> |<span data-ttu-id="1ed72-139">규약에는 호스트 및 게스트 파트너가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-139">An agreement needs both a host and guest partner.</span></span> <span data-ttu-id="1ed72-140">hello 호스트 파트너에는 hello 규약을 구성 하는 hello 조직을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-140">hello host partner represents hello organization that configures hello agreement.</span></span> |
    | <span data-ttu-id="1ed72-141">호스트 ID</span><span class="sxs-lookup"><span data-stu-id="1ed72-141">Host Identity</span></span> |<span data-ttu-id="1ed72-142">Hello 호스트 파트너에 대 한 식별자</span><span class="sxs-lookup"><span data-stu-id="1ed72-142">An identifier for hello host partner</span></span> |
    | <span data-ttu-id="1ed72-143">게스트 파트너</span><span class="sxs-lookup"><span data-stu-id="1ed72-143">Guest Partner</span></span> |<span data-ttu-id="1ed72-144">규약에는 호스트 및 게스트 파트너가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-144">An agreement needs both a host and guest partner.</span></span> <span data-ttu-id="1ed72-145">hello 게스트 파트너에는 hello 호스트 파트너와 비즈니스를 수행 하는 hello 조직을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-145">hello guest partner represents hello organization that's doing business with hello host partner.</span></span> |
    | <span data-ttu-id="1ed72-146">게스트 ID</span><span class="sxs-lookup"><span data-stu-id="1ed72-146">Guest Identity</span></span> |<span data-ttu-id="1ed72-147">Hello 게스트 파트너에 대 한 식별자</span><span class="sxs-lookup"><span data-stu-id="1ed72-147">An identifier for hello guest partner</span></span> |
    | <span data-ttu-id="1ed72-148">수신 설정</span><span class="sxs-lookup"><span data-stu-id="1ed72-148">Receive Settings</span></span> |<span data-ttu-id="1ed72-149">이러한 속성에는 계약에 의해 수신 된 tooall 메시지 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-149">These properties apply tooall messages received by an agreement.</span></span> |
    | <span data-ttu-id="1ed72-150">송신 설정</span><span class="sxs-lookup"><span data-stu-id="1ed72-150">Send Settings</span></span> |<span data-ttu-id="1ed72-151">이러한 속성에는 규약을 전송한 tooall 메시지 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-151">These properties apply tooall messages sent by an agreement.</span></span> |

## <a name="configure-how-your-agreement-handles-received-messages"></a><span data-ttu-id="1ed72-152">규약에서 수신된 메시지를 처리하는 방법 구성</span><span class="sxs-lookup"><span data-stu-id="1ed72-152">Configure how your agreement handles received messages</span></span>

<span data-ttu-id="1ed72-153">Hello 규약 속성을 설정한 했으므로 본이 계약 식별 하 고 본이 계약을 통해 파트너 로부터 받은 들어오는 메시지를 처리 하는 방법을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-153">Now that you've set hello agreement properties, you can configure how this agreement identifies and handles incoming messages received from your partner through this agreement.</span></span>

1.  <span data-ttu-id="1ed72-154">**추가** 아래에서 **수신 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-154">Under **Add**, select **Receive Settings**.</span></span>
<span data-ttu-id="1ed72-155">와 함께 메시지를 교환 하는 hello 파트너 계약에 따라 이러한 속성을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-155">Configure these properties based on your agreement with hello partner that exchanges messages with you.</span></span> <span data-ttu-id="1ed72-156">속성 설명은이 섹션의 hello 표를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-156">For property descriptions, see hello table in this section.</span></span>

    !["수신 설정" 구성](./media/logic-apps-enterprise-integration-agreements/agreement-4.png)

2. <span data-ttu-id="1ed72-158">필요에 따라 들어오는 메시지의 hello 속성을 선택 하 여 재정의할 수 있습니다 **메시지 속성 재정의**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-158">Optionally, you can override hello properties of incoming messages by selecting **Override message properties**.</span></span>

3. <span data-ttu-id="1ed72-159">toorequire 모든 들어오는 메시지 toobe 서명, 선택 **메시지 서명 필요**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-159">toorequire all incoming messages toobe signed, select **Message should be signed**.</span></span> <span data-ttu-id="1ed72-160">Hello에서 **인증서** 목록에서 기존 [게스트 파트너 공용 인증서](../logic-apps/logic-apps-enterprise-integration-certificates.md) hello 메시지에 hello 서명을 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-160">From hello **Certificate** list, select an existing [guest partner public certificate](../logic-apps/logic-apps-enterprise-integration-certificates.md) for validating hello signature on hello messages.</span></span> <span data-ttu-id="1ed72-161">하거나 없는 경우 hello 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-161">Or create hello certificate, if you don't have one.</span></span>

4.  <span data-ttu-id="1ed72-162">암호화 된 모든 들어오는 메시지의 toobe 선택 toorequire **메시지 암호화**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-162">toorequire all incoming messages toobe encrypted, select **Message should be encrypted**.</span></span> <span data-ttu-id="1ed72-163">Hello에서 **인증서** 목록에서 기존 [호스트 파트너 개인 인증서](../logic-apps/logic-apps-enterprise-integration-certificates.md) 들어오는 메시지의 암호를 해독 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-163">From hello **Certificate** list, select an existing [host partner private certificate](../logic-apps/logic-apps-enterprise-integration-certificates.md) for decrypting incoming messages.</span></span> <span data-ttu-id="1ed72-164">하거나 없는 경우 hello 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-164">Or create hello certificate, if you don't have one.</span></span>

5. <span data-ttu-id="1ed72-165">압축 toorequire 메시지 toobe 선택 **메시지 압축 필요**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-165">toorequire messages toobe compressed, select **Message should be compressed**.</span></span>

6. <span data-ttu-id="1ed72-166">받은 메시지에 대 한 동기 메시지 처리 알림 (MDN) toosend 선택 **MDN 보내기**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-166">toosend a synchronous message disposition notification (MDN) for received messages, select **Send MDN**.</span></span>

7. <span data-ttu-id="1ed72-167">받은 메시지에 Mdn을 등록 하는 toosend **서명 된 MDN 보내기**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-167">toosend signed MDNs for received messages, select **Send signed MDN**.</span></span>

8. <span data-ttu-id="1ed72-168">toosend 비동기 Mdn 메시지를 받는 선택 **비동기 MDN 보내기**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-168">toosend asynchronous MDNs for received messages, select **Send asynchronous MDN**.</span></span>

9. <span data-ttu-id="1ed72-169">을 마친 후 확인 되었는지 toosave 설정을 선택 하 여 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-169">After you're done, make sure toosave your settings by choosing **OK**.</span></span>

<span data-ttu-id="1ed72-170">계약에는 들어오는 준비 toohandle tooyour 따르는 메시지만 선택한 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-170">Now your agreement is ready toohandle incoming messages that conform tooyour selected settings.</span></span>

| <span data-ttu-id="1ed72-171">속성</span><span class="sxs-lookup"><span data-stu-id="1ed72-171">Property</span></span> | <span data-ttu-id="1ed72-172">설명</span><span class="sxs-lookup"><span data-stu-id="1ed72-172">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1ed72-173">메시지 속성 재정의</span><span class="sxs-lookup"><span data-stu-id="1ed72-173">Override message properties</span></span> |<span data-ttu-id="1ed72-174">받은 메시지의 속성을 재정의할 수 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-174">Indicates that properties in received messages can be overridden.</span></span> |
| <span data-ttu-id="1ed72-175">메시지 서명 필요</span><span class="sxs-lookup"><span data-stu-id="1ed72-175">Message should be signed</span></span> |<span data-ttu-id="1ed72-176">디지털 서명 메시지 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-176">Requires messages toobe digitally signed.</span></span> <span data-ttu-id="1ed72-177">서명 확인에 대 한 hello 게스트 파트너 공용 인증서를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-177">Configure hello guest partner public certificate for signature verification.</span></span>  |
| <span data-ttu-id="1ed72-178">메시지 암호화 필요</span><span class="sxs-lookup"><span data-stu-id="1ed72-178">Message should be encrypted</span></span> |<span data-ttu-id="1ed72-179">암호화 메시지 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-179">Requires messages toobe encrypted.</span></span> <span data-ttu-id="1ed72-180">암호화되지 않은 메시지는 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-180">Non-encrypted messages are rejected.</span></span> <span data-ttu-id="1ed72-181">Hello 메시지를 암호 해독을 위한 hello 호스트 파트너 개인 인증서를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-181">Configure hello host partner private certificate for decrypting hello messages.</span></span>  |
| <span data-ttu-id="1ed72-182">메시지 압축 필요</span><span class="sxs-lookup"><span data-stu-id="1ed72-182">Message should be compressed</span></span> |<span data-ttu-id="1ed72-183">압축 메시지 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-183">Requires messages toobe compressed.</span></span> <span data-ttu-id="1ed72-184">압축되지 않은 메시지는 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-184">Non-compressed messages are rejected.</span></span> |
| <span data-ttu-id="1ed72-185">MDN 텍스트</span><span class="sxs-lookup"><span data-stu-id="1ed72-185">MDN Text</span></span> |<span data-ttu-id="1ed72-186">hello 기본 메시지 처리 알림 (MDN) toobe toohello 메시지 보낸 사람에 게를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-186">hello default message disposition notification (MDN) toobe sent toohello message sender.</span></span> |
| <span data-ttu-id="1ed72-187">MDN 전송</span><span class="sxs-lookup"><span data-stu-id="1ed72-187">Send MDN</span></span> |<span data-ttu-id="1ed72-188">전송 Mdn toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-188">Requires MDNs toobe sent.</span></span> |
| <span data-ttu-id="1ed72-189">서명된 MDN 전송</span><span class="sxs-lookup"><span data-stu-id="1ed72-189">Send signed MDN</span></span> |<span data-ttu-id="1ed72-190">서명 된 Mdn toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-190">Requires MDNs toobe signed.</span></span> |
| <span data-ttu-id="1ed72-191">MIC 알고리즘</span><span class="sxs-lookup"><span data-stu-id="1ed72-191">MIC Algorithm</span></span> |<span data-ttu-id="1ed72-192">메시지 서명을 위한 알고리즘 toouse hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-192">Select hello algorithm toouse for signing messages.</span></span> |
| <span data-ttu-id="1ed72-193">비동기 MDN 전송</span><span class="sxs-lookup"><span data-stu-id="1ed72-193">Send asynchronous MDN</span></span> | <span data-ttu-id="1ed72-194">비동기적으로 전송 하는 메시지 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-194">Requires messages toobe sent asynchronously.</span></span> |
| <span data-ttu-id="1ed72-195">URL</span><span class="sxs-lookup"><span data-stu-id="1ed72-195">URL</span></span> | <span data-ttu-id="1ed72-196">여기서 toosend hello Mdn hello URL을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-196">Specify hello URL where toosend hello MDNs.</span></span> |

## <a name="configure-how-your-agreement-sends-messages"></a><span data-ttu-id="1ed72-197">규약에서 메시지를 보내는 방법 구성</span><span class="sxs-lookup"><span data-stu-id="1ed72-197">Configure how your agreement sends messages</span></span>

<span data-ttu-id="1ed72-198">본이 계약 식별 하 고 본이 계약을 통해 tooyour 파트너를 전송 하는 보내는 메시지를 처리 하는 방법을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-198">You can configure how this agreement identifies and handles outgoing messages that you send tooyour partners through this agreement.</span></span>

1.  <span data-ttu-id="1ed72-199">**추가** 아래에서 **송신 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-199">Under **Add**, select **Send Settings**.</span></span>
<span data-ttu-id="1ed72-200">와 함께 메시지를 교환 하는 hello 파트너 계약에 따라 이러한 속성을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-200">Configure these properties based on your agreement with hello partner that exchanges messages with you.</span></span> <span data-ttu-id="1ed72-201">속성 설명은이 섹션의 hello 표를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-201">For property descriptions, see hello table in this section.</span></span>

    ![Hello "송신 설정" 속성 설정](./media/logic-apps-enterprise-integration-agreements/agreement-51.png)

2. <span data-ttu-id="1ed72-203">toosend 서명 된 메시지 tooyour 파트너에서 선택 **메시지 서명 사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-203">toosend signed messages tooyour partner, select **Enable message signing**.</span></span> <span data-ttu-id="1ed72-204">Hello에 hello 메시지 서명을 위한 **MIC 알고리즘** 목록, 선택 hello *호스트 파트너 개인 인증서 MIC 알고리즘*합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-204">For signing hello messages, in hello **MIC Algorithm** list, select hello *host partner private certificate MIC Algorithm*.</span></span> <span data-ttu-id="1ed72-205">및 hello **인증서** 목록에서 기존 [호스트 파트너 개인 인증서](../logic-apps/logic-apps-enterprise-integration-certificates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-205">And in hello **Certificate** list, select an existing [host partner private certificate](../logic-apps/logic-apps-enterprise-integration-certificates.md).</span></span>

3. <span data-ttu-id="1ed72-206">toosend 암호화 된 메시지 toohello 파트너에서 선택 **메시지 암호화 사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-206">toosend encrypted messages toohello partner, select **Enable message encryption**.</span></span> <span data-ttu-id="1ed72-207">Hello에 hello 메시지를 암호화 하기 위한 **암호화 알고리즘** 목록, 선택 hello *게스트 파트너 공용 인증서 알고리즘*합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-207">For encrypting hello messages, in hello **Encryption Algorithm** list, select hello *guest partner public certificate algorithm*.</span></span>
<span data-ttu-id="1ed72-208">및 hello **인증서** 목록에서 기존 [게스트 파트너 공용 인증서](../logic-apps/logic-apps-enterprise-integration-certificates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-208">And in hello **Certificate** list, select an existing [guest partner public certificate](../logic-apps/logic-apps-enterprise-integration-certificates.md).</span></span>

4. <span data-ttu-id="1ed72-209">선택 toocompress hello 메시지 **메시지 압축 사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-209">toocompress hello message, select **Enable message compression**.</span></span>

5. <span data-ttu-id="1ed72-210">선택 단일 줄으로 toounfold hello HTTP content-type 헤더 **HTTP 헤더 펼침**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-210">toounfold hello HTTP content-type header into a single line, select **Unfold HTTP headers**.</span></span>

6. <span data-ttu-id="1ed72-211">tooreceive hello에 대 한 동기 Mdn 메시지를 보낸 **MDN 요청**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-211">tooreceive synchronous MDNs for hello sent messages, select **Request MDN**.</span></span>

7. <span data-ttu-id="1ed72-212">전송 hello 메시지에 Mdn을 등록 하는 tooreceive **서명 된 MDN 요청**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-212">tooreceive signed MDNs for hello sent messages, select **Request signed MDN**.</span></span>

8. <span data-ttu-id="1ed72-213">tooreceive hello에 대 한 비동기 Mdn 메시지를 보낸 **비동기 MDN 요청**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-213">tooreceive asynchronous MDNs for hello sent messages, select **Request asynchronous MDN**.</span></span> <span data-ttu-id="1ed72-214">이 옵션을 선택 하는 경우 여기서 toosend hello Mdn에 대 한 hello URL을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-214">If you select this option, enter hello URL for where toosend hello MDNs.</span></span>

9. <span data-ttu-id="1ed72-215">toorequire 비 거부 수신 선택 **NRR**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-215">toorequire non-repudiation of receipt, select **Enable NRR**.</span></span>  

10. <span data-ttu-id="1ed72-216">MIC hello에 toospecify 알고리즘 형식 toouse 하거나 hello AS2 메시지나 MDN을의 헤더를 나가는 hello 로그인 선택 **SHA2 알고리즘 형식**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-216">toospecify algorithm format toouse in hello MIC or signing in hello outgoing headers of hello AS2 message or MDN, select **SHA2 Algorithm format**.</span></span>  

11. <span data-ttu-id="1ed72-217">을 마친 후 확인 되었는지 toosave 설정을 선택 하 여 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-217">After you're done, make sure toosave your settings by choosing **OK**.</span></span>

<span data-ttu-id="1ed72-218">이제 규약 준비 toohandle 보내는 tooyour 선택 설정을 준수 하는 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-218">Now your agreement is ready toohandle outgoing messages that conform tooyour selected settings.</span></span>

| <span data-ttu-id="1ed72-219">속성</span><span class="sxs-lookup"><span data-stu-id="1ed72-219">Property</span></span> | <span data-ttu-id="1ed72-220">설명</span><span class="sxs-lookup"><span data-stu-id="1ed72-220">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1ed72-221">메시지 서명 사용</span><span class="sxs-lookup"><span data-stu-id="1ed72-221">Enable message signing</span></span> |<span data-ttu-id="1ed72-222">Hello 계약 toobe 서명에서 보낸 모든 메시지가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-222">Requires all messages that are sent from hello agreement toobe signed.</span></span> |
| <span data-ttu-id="1ed72-223">MIC 알고리즘</span><span class="sxs-lookup"><span data-stu-id="1ed72-223">MIC Algorithm</span></span> |<span data-ttu-id="1ed72-224">hello 메시지 서명을 위한 알고리즘 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-224">hello algorithm toouse for signing messages.</span></span> <span data-ttu-id="1ed72-225">Hello 메시지 서명을 위한 hello 호스트 파트너 개인 인증서 MIC 알고리즘을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-225">Configures hello host partner private certificate MIC Algorithm for signing hello messages.</span></span> |
| <span data-ttu-id="1ed72-226">인증서</span><span class="sxs-lookup"><span data-stu-id="1ed72-226">Certificate</span></span> |<span data-ttu-id="1ed72-227">메시지 서명을 위한 인증서 toouse hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-227">Select hello certificate toouse for signing messages.</span></span> <span data-ttu-id="1ed72-228">Hello 메시지 서명을 위한 hello 호스트 파트너 개인 인증서를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-228">Configures hello host partner private certificate for signing hello messages.</span></span> |
| <span data-ttu-id="1ed72-229">메시지 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="1ed72-229">Enable message encryption</span></span> |<span data-ttu-id="1ed72-230">이 규약에서 보낸 모든 메시지를 암호화하도록 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-230">Requires encryption of all messages that are sent from this agreement.</span></span> <span data-ttu-id="1ed72-231">Hello 메시지를 암호화 하기 위한 hello 게스트 파트너 공용 인증서 알고리즘을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-231">Configures hello guest partner public certificate algorithm for encrypting hello messages.</span></span> |
| <span data-ttu-id="1ed72-232">암호화 알고리즘</span><span class="sxs-lookup"><span data-stu-id="1ed72-232">Encryption Algorithm</span></span> |<span data-ttu-id="1ed72-233">메시지 암호화에 대 한 암호화 알고리즘 toouse를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-233">hello encryption algorithm toouse for message encryption.</span></span> <span data-ttu-id="1ed72-234">Hello 메시지를 암호화 하기 위한 hello 게스트 파트너 공용 인증서를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-234">Configures hello guest partner public certificate for encrypting hello messages.</span></span> |
| <span data-ttu-id="1ed72-235">인증서</span><span class="sxs-lookup"><span data-stu-id="1ed72-235">Certificate</span></span> |<span data-ttu-id="1ed72-236">hello 인증서 toouse tooencrypt 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-236">hello certificate toouse tooencrypt messages.</span></span> <span data-ttu-id="1ed72-237">Hello 메시지를 암호화 하기 위한 hello 게스트 파트너 개인 인증서를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-237">Configures hello guest partner private certificate for encrypting hello messages.</span></span> |
| <span data-ttu-id="1ed72-238">메시지 압축 사용</span><span class="sxs-lookup"><span data-stu-id="1ed72-238">Enable message compression</span></span> |<span data-ttu-id="1ed72-239">이 규약에서 보낸 모든 메시지를 압축하도록 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-239">Requires compression of all messages that are sent from this agreement.</span></span> |
| <span data-ttu-id="1ed72-240">HTTP 헤더 펼침</span><span class="sxs-lookup"><span data-stu-id="1ed72-240">Unfold HTTP headers</span></span> |<span data-ttu-id="1ed72-241">Hello HTTP content-type 헤더를 한 줄에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-241">Places hello HTTP content-type header onto a single line.</span></span> |
| <span data-ttu-id="1ed72-242">MDN 요청</span><span class="sxs-lookup"><span data-stu-id="1ed72-242">Request MDN</span></span> |<span data-ttu-id="1ed72-243">이 규약에서 보낸 모든 메시지에 대한 MDN을 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-243">Requires an MDN for all messages that are sent from this agreement.</span></span> |
| <span data-ttu-id="1ed72-244">서명된 MDN 요청</span><span class="sxs-lookup"><span data-stu-id="1ed72-244">Request signed MDN</span></span> |<span data-ttu-id="1ed72-245">Toobe 서명 toothis 계약 전송 되는 모든 Mdn 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-245">Requires all MDNs that are sent toothis agreement toobe signed.</span></span> |
| <span data-ttu-id="1ed72-246">비동기 MDN 요청</span><span class="sxs-lookup"><span data-stu-id="1ed72-246">Request asynchronous MDN</span></span> |<span data-ttu-id="1ed72-247">비동기 Mdn 전송 toobe toothis 동의가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-247">Requires asynchronous MDNs toobe sent toothis agreement.</span></span> |
| <span data-ttu-id="1ed72-248">URL</span><span class="sxs-lookup"><span data-stu-id="1ed72-248">URL</span></span> |<span data-ttu-id="1ed72-249">여기서 toosend hello Mdn hello URL을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-249">Specify hello URL where toosend hello MDNs.</span></span> |
| <span data-ttu-id="1ed72-250">NRR 사용</span><span class="sxs-lookup"><span data-stu-id="1ed72-250">Enable NRR</span></span> |<span data-ttu-id="1ed72-251">해결 되었으며 수신 비 거부 수신 (NRR) hello 데이터 증거를 제공 하는 통신 특성이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-251">Requires non-repudiation of receipt (NRR), a communication attribute that provides evidence that hello data was received as addressed.</span></span> |
| <span data-ttu-id="1ed72-252">SHA2 알고리즘 형식</span><span class="sxs-lookup"><span data-stu-id="1ed72-252">SHA2 Algorithm format</span></span> |<span data-ttu-id="1ed72-253">MIC hello 또는 hello AS2 메시지 또는 MDN의 헤더를 나가는 hello 로그인에서 알고리즘 형식 toouse를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-253">Select algorithm format toouse in hello MIC or signing in hello outgoing headers of hello AS2 message or MDN</span></span> |

## <a name="find-your-created-agreement"></a><span data-ttu-id="1ed72-254">생성된 규약 찾기</span><span class="sxs-lookup"><span data-stu-id="1ed72-254">Find your created agreement</span></span>

1.  <span data-ttu-id="1ed72-255">Hello에서 모든 규약 속성을 설정 하는 것이 마친 후 **추가** 블레이드에서 선택 **확인** toofinish 계약 및 반환 tooyour 통합 계정 블레이드 만들기.</span><span class="sxs-lookup"><span data-stu-id="1ed72-255">After you finish setting all your agreement properties, on hello **Add** blade, choose **OK** toofinish creating your agreement and return tooyour integration account blade.</span></span>

    <span data-ttu-id="1ed72-256">이제 새로 추가된 규약이 **규약** 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-256">Your newly added agreement now appears in your **Agreements** list.</span></span>

2.  <span data-ttu-id="1ed72-257">또한 통합 계정 개요에서 규약을 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-257">You can also view your agreements in your integration account overview.</span></span> <span data-ttu-id="1ed72-258">통합 계정 블레이드를 사용 하 여 선택 **개요**을 선택한 후 hello **계약** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-258">On your integration account blade, choose **Overview**, then select hello **Agreements** tile.</span></span> 

    ![모든 동의 "계약" 타일 tooview 선택](./media/logic-apps-enterprise-integration-agreements/agreement-6.png)

## <a name="view-hello-swagger"></a><span data-ttu-id="1ed72-260">Hello swagger 보기</span><span class="sxs-lookup"><span data-stu-id="1ed72-260">View hello swagger</span></span>
<span data-ttu-id="1ed72-261">Hello 참조 [세부 정보를 swagger](/connectors/as2/)합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed72-261">See hello [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1ed72-262">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1ed72-262">Next steps</span></span>
* [<span data-ttu-id="1ed72-263">엔터프라이즈 통합 팩 hello에 대 한 자세한</span><span class="sxs-lookup"><span data-stu-id="1ed72-263">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "엔터프라이즈 통합 팩에 대 한 자세한 정보")  
