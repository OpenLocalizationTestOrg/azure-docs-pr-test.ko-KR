---
title: "aaaEncode X12 메시지-Azure 논리 앱 | Microsoft Docs"
description: "EDI 유효성을 검사 하 고 XML로 인코딩된 변환 x12 메시지 Azure 논리 앱에 대 한 인코더에 엔터프라이즈 통합 팩 hello 메시지"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: a01e9ca9-816b-479e-ab11-4a984f10f62d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 785dbd2c7c82463154732921e07e3586d2307840
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="encode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="03ff4-103">X12 인코딩 엔터프라이즈 통합 팩 hello로 Azure 논리 앱에 대 한 메시지</span><span class="sxs-lookup"><span data-stu-id="03ff4-103">Encode X12 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="03ff4-104">Hello X12 인코딩 메시지 연결선 EDI 및 파트너 관련 속성의 유효성을 검사를 hello 교환에 EDI 트랜잭션 집합 XML로 인코딩된 메시지를 변환 하 고 사용할 수 기술 승인, 기능 승인 또는 둘 다를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="03ff4-104">With hello Encode X12 message connector, you can validate EDI and partner-specific properties, convert XML-encoded messages into EDI transaction sets in hello interchange, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="03ff4-105">toouse이이 커넥터를 트리거 논리 앱에서 기존 hello 커넥터 tooan 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03ff4-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="03ff4-106">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="03ff4-106">Before you start</span></span>

<span data-ttu-id="03ff4-107">다음은 필요한 hello 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="03ff4-107">Here's hello items you need:</span></span>

* <span data-ttu-id="03ff4-108">Azure 계정의 경우 [무료 계정](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="03ff4-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="03ff4-109">[통합 계정](logic-apps-enterprise-integration-create-integration-account.md)이 이미 정의되고 Azure 구독과 연결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="03ff4-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="03ff4-110">통합 계정 toouse hello X12 인코딩 메시지 연결선이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03ff4-110">You must have an integration account toouse hello Encode X12 message connector.</span></span>
* <span data-ttu-id="03ff4-111">통합 계정에 이미 정의된 둘 이상의 [파트너](logic-apps-enterprise-integration-partners.md)</span><span class="sxs-lookup"><span data-stu-id="03ff4-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="03ff4-112">통합 계정에 이미 정의된 [X12 규약](logic-apps-enterprise-integration-x12.md)</span><span class="sxs-lookup"><span data-stu-id="03ff4-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span></span>

## <a name="encode-x12-messages"></a><span data-ttu-id="03ff4-113">X12 메시지 인코딩</span><span class="sxs-lookup"><span data-stu-id="03ff4-113">Encode X12 messages</span></span>

1. <span data-ttu-id="03ff4-114">[논리 앱 만들기](logic-apps-create-a-logic-app.md)</span><span class="sxs-lookup"><span data-stu-id="03ff4-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="03ff4-115">hello X12 인코딩 메시지 연결선은 트리거, 갖고 있지 않으므로 요청 트리거와 마찬가지로 논리 앱을 시작 하는 트리거를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03ff4-115">hello Encode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="03ff4-116">Hello 논리가 응용 프로그램 디자이너에서에서 트리거를 추가 하 고 작업 tooyour 논리 앱을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="03ff4-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="03ff4-117">Hello 검색 상자에 필터에 대 한 "x12"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="03ff4-117">In hello search box, enter "x12" for your filter.</span></span> <span data-ttu-id="03ff4-118">선택 **X12-tooX12 메시지 계약 이름으로 인코딩** 또는 **X12-identities 여 tooX12 메시지 인코딩**합니다.</span><span class="sxs-lookup"><span data-stu-id="03ff4-118">Select either **X12 - Encode tooX12 message by agreement name** or **X12 - Encode tooX12 message by identities**.</span></span>
   
    !["x12" 검색](./media/logic-apps-enterprise-integration-x12-encode/x12decodeimage1.png) 

3. <span data-ttu-id="03ff4-120">직접 만들지 않은 경우 이전에 모든 연결이 tooyour 통합 계정, 메시지가 toocreate 지금 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="03ff4-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="03ff4-121">사용자의 연결 이름을 지정 하 고 원하는 tooconnect hello 통합 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="03ff4-121">Name your connection, and select hello integration account that you want tooconnect.</span></span> 
   
    ![통합 계정 연결](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage1.png)

    <span data-ttu-id="03ff4-123">별표가 있는 속성은 필수 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="03ff4-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="03ff4-124">속성</span><span class="sxs-lookup"><span data-stu-id="03ff4-124">Property</span></span> | <span data-ttu-id="03ff4-125">세부 정보</span><span class="sxs-lookup"><span data-stu-id="03ff4-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="03ff4-126">연결 이름 *</span><span class="sxs-lookup"><span data-stu-id="03ff4-126">Connection Name *</span></span> |<span data-ttu-id="03ff4-127">연결의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="03ff4-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="03ff4-128">통합 계정 *</span><span class="sxs-lookup"><span data-stu-id="03ff4-128">Integration Account *</span></span> |<span data-ttu-id="03ff4-129">통합 계정의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="03ff4-129">Enter a name for your integration account.</span></span> <span data-ttu-id="03ff4-130">통합 계정 및 논리 앱 hello에 있는지 확인 동일한 Azure 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="03ff4-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="03ff4-131">완료 되 면 연결 정보가 이와 유사한 toothis 예가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="03ff4-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="03ff4-132">연결을 만드는 toofinish 선택 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="03ff4-132">toofinish creating your connection, choose **Create**.</span></span>

    ![통합 계정 연결 생성](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage2.png)

    <span data-ttu-id="03ff4-134">새로운 연결이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="03ff4-134">Your connection is now created.</span></span>

    ![통합 계정 연결 세부 사항](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage3.png) 

#### <a name="encode-x12-messages-by-agreement-name"></a><span data-ttu-id="03ff4-136">규약 이름으로 X12 메시지 인코딩</span><span class="sxs-lookup"><span data-stu-id="03ff4-136">Encode X12 messages by agreement name</span></span>

<span data-ttu-id="03ff4-137">계약 이름으로 tooencode X12 메시지를 선택 하는 경우 열 hello **X12의 이름을 계약** 목록를 입력 하거나 선택 하면 기존 X12 계약입니다.</span><span class="sxs-lookup"><span data-stu-id="03ff4-137">If you chose tooencode X12 messages by agreement name, open hello **Name of X12 agreement** list, enter or select your existing X12 agreement.</span></span> <span data-ttu-id="03ff4-138">XML 메시지 tooencode hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="03ff4-138">Enter hello XML message tooencode.</span></span>

![입력 X12 계약 이름 및 XML 메시지 tooencode](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage4.png)

#### <a name="encode-x12-messages-by-identities"></a><span data-ttu-id="03ff4-140">ID로 X12 메시지 인코딩</span><span class="sxs-lookup"><span data-stu-id="03ff4-140">Encode X12 messages by identities</span></span>

<span data-ttu-id="03ff4-141">Identities 여 tooencode X12 메시지를 선택 하는 경우 입력 hello 보낸 사람 식별자, 보낸 사람 한정자, 받는 사람 식별자 및 받는 사람 한정자 프로그램 X12에 구성 된 대로 계약입니다.</span><span class="sxs-lookup"><span data-stu-id="03ff4-141">If you choose tooencode X12 messages by identities, enter hello sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your X12 agreement.</span></span> <span data-ttu-id="03ff4-142">XML 메시지 tooencode hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="03ff4-142">Select hello XML message tooencode.</span></span>
   
![XML 메시지 tooencode 선택, 발신자와 수신자에 대 한 id를 제공 합니다.](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage5.png) 

## <a name="x12-encode-details"></a><span data-ttu-id="03ff4-144">X12 인코딩 세부 정보</span><span class="sxs-lookup"><span data-stu-id="03ff4-144">X12 Encode details</span></span>

<span data-ttu-id="03ff4-145">hello X12 인코딩 커넥터 이러한 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="03ff4-145">hello X12 Encode connector performs these tasks:</span></span>

* <span data-ttu-id="03ff4-146">보낸 사람 및 받는 사람 컨텍스트 속성을 일치시켜 규약을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="03ff4-146">Agreement resolution by matching sender and receiver context properties.</span></span>
* <span data-ttu-id="03ff4-147">Hello 교환에 EDI 트랜잭션 집합 XML로 인코딩된 메시지 변환 hello EDI 교환으로 직렬화 합니다.</span><span class="sxs-lookup"><span data-stu-id="03ff4-147">Serializes hello EDI interchange, converting XML-encoded messages into EDI transaction sets in hello interchange.</span></span>
* <span data-ttu-id="03ff4-148">트랜잭션 집합 헤더 및 트레일러 세그먼트를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="03ff4-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="03ff4-149">교환 제어 번호, 그룹 제어 번호 및 나가는 교환 각각에 대한 트랜잭션 집합 제어 번호를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="03ff4-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="03ff4-150">Hello 페이로드 데이터에는 구분 기호를 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="03ff4-150">Replaces separators in hello payload data</span></span>
* <span data-ttu-id="03ff4-151">EDI 및 파트너 관련 속성의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="03ff4-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="03ff4-152">Hello 메시지 스키마에 대 한 hello 트랜잭션 집합 데이터 요소의 스키마 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="03ff4-152">Schema validation of hello transaction-set data elements against hello message Schema</span></span>
  * <span data-ttu-id="03ff4-153">트랜잭션 집합 데이터 요소에서 수행한 EDI 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="03ff4-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="03ff4-154">트랜잭션 집합 데이터 요소에서 수행한 확장된 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="03ff4-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="03ff4-155">기술 및/또는 기능 승인을 요청합니다(구성된 경우).</span><span class="sxs-lookup"><span data-stu-id="03ff4-155">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="03ff4-156">기술 승인은 헤더 유효성 검사의 결과로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="03ff4-156">A Technical Acknowledgment generates as a result of header validation.</span></span> <span data-ttu-id="03ff4-157">hello 기술 승인을 교환 헤더 및 트레일러 hello 주소 수신기의 hello 처리의 hello 상태를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="03ff4-157">hello technical acknowledgment reports hello status of hello processing of an interchange header and trailer by hello address receiver</span></span>
  * <span data-ttu-id="03ff4-158">기능 승인은 본문 유효성 검사의 결과로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="03ff4-158">A Functional Acknowledgment generates as a result of body validation.</span></span> <span data-ttu-id="03ff4-159">hello 기능 승인은 문서를 받은 hello를 처리 하는 동안 발생 한 각 오류</span><span class="sxs-lookup"><span data-stu-id="03ff4-159">hello functional acknowledgment reports each error encountered while processing hello received document</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="03ff4-160">Hello swagger 보기</span><span class="sxs-lookup"><span data-stu-id="03ff4-160">View hello swagger</span></span>
<span data-ttu-id="03ff4-161">Hello 참조 [세부 정보를 swagger](/connectors/x12/)합니다.</span><span class="sxs-lookup"><span data-stu-id="03ff4-161">See hello [swagger details](/connectors/x12/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="03ff4-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="03ff4-162">Next steps</span></span>
[<span data-ttu-id="03ff4-163">엔터프라이즈 통합 팩 hello에 대 한 자세한</span><span class="sxs-lookup"><span data-stu-id="03ff4-163">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "엔터프라이즈 통합 팩에 대 한 자세한 정보") 

