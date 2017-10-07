---
title: "Azure 논리 앱-aaaEncode EDIFACT 메시지 | Microsoft Docs"
description: "EDI 유효성을 검사 하 고 Azure 논리 앱에 대 한 hello 엔터프라이즈 통합 팩에서에서 EDIFACT 메시지 인코더와 XML을 생성"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 974ac339-d97a-4715-bc92-62d02281e900
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: b3799dbd2492adef597022d017cf28f5ceb1085c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="encode-edifact-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="9ff3e-103">엔터프라이즈 통합 팩 hello로 Azure 논리 앱에 대 한 EDIFACT 메시지 인코딩</span><span class="sxs-lookup"><span data-stu-id="9ff3e-103">Encode EDIFACT messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="9ff3e-104">Hello EDIFACT 인코딩 메시지 연결선 EDI 및 파트너 관련 속성의 유효성을 검사, 각 트랜잭션 집합에 대 한 XML 문서를 생성 하 고 사용할 수 기술 승인, 기능 승인 또는 둘 다를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3e-104">With hello Encode EDIFACT message connector, you can validate EDI and partner-specific properties, generate an XML document for each transaction set, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="9ff3e-105">toouse이이 커넥터를 트리거 논리 앱에서 기존 hello 커넥터 tooan 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3e-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="9ff3e-106">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="9ff3e-106">Before you start</span></span>

<span data-ttu-id="9ff3e-107">다음은 필요한 hello 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3e-107">Here's hello items you need:</span></span>

* <span data-ttu-id="9ff3e-108">Azure 계정의 경우 [무료 계정](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="9ff3e-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="9ff3e-109">[통합 계정](logic-apps-enterprise-integration-create-integration-account.md)이 이미 정의되고 Azure 구독과 연결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3e-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="9ff3e-110">통합 계정 toouse hello EDIFACT 인코딩 메시지 연결선이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3e-110">You must have an integration account toouse hello Encode EDIFACT message connector.</span></span> 
* <span data-ttu-id="9ff3e-111">통합 계정에 이미 정의된 둘 이상의 [파트너](logic-apps-enterprise-integration-partners.md)</span><span class="sxs-lookup"><span data-stu-id="9ff3e-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="9ff3e-112">통합 계정에 이미 정의된 [EDIFACT 규약](logic-apps-enterprise-integration-edifact.md)</span><span class="sxs-lookup"><span data-stu-id="9ff3e-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span></span>

## <a name="encode-edifact-messages"></a><span data-ttu-id="9ff3e-113">EDIFACT 메시지 인코딩</span><span class="sxs-lookup"><span data-stu-id="9ff3e-113">Encode EDIFACT messages</span></span>

1. <span data-ttu-id="9ff3e-114">[논리 앱 만들기](logic-apps-create-a-logic-app.md)</span><span class="sxs-lookup"><span data-stu-id="9ff3e-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="9ff3e-115">hello EDIFACT 인코딩 메시지 연결선은 트리거, 갖고 있지 않으므로 요청 트리거와 마찬가지로 논리 앱을 시작 하는 트리거를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3e-115">hello Encode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="9ff3e-116">Hello 논리가 응용 프로그램 디자이너에서에서 트리거를 추가 하 고 작업 tooyour 논리 앱을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3e-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="9ff3e-117">Hello 검색 상자에 필터로 "EDIFACT"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3e-117">In hello search box, enter "EDIFACT" as your filter.</span></span> <span data-ttu-id="9ff3e-118">선택 **계약 이름으로 EDIFACT 메시지 인코딩** 또는 **identities 하 여 인코딩 tooEDIFACT 메시지**합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3e-118">Select either **Encode EDIFACT Message by agreement name** or **Encode tooEDIFACT message by identities**.</span></span>
   
    ![EDIFACT 검색](media/logic-apps-enterprise-integration-edifact-encode/edifactdecodeimage1.png)  

3. <span data-ttu-id="9ff3e-120">직접 만들지 않은 경우 이전에 모든 연결이 tooyour 통합 계정, 메시지가 toocreate 지금 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3e-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="9ff3e-121">사용자의 연결 이름을 지정 하 고 원하는 tooconnect hello 통합 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3e-121">Name your connection, and select hello integration account that you want tooconnect.</span></span>

    ![통합 계정 연결 만들기](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage1.png)  

    <span data-ttu-id="9ff3e-123">별표가 있는 속성은 필수 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3e-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="9ff3e-124">속성</span><span class="sxs-lookup"><span data-stu-id="9ff3e-124">Property</span></span> | <span data-ttu-id="9ff3e-125">세부 정보</span><span class="sxs-lookup"><span data-stu-id="9ff3e-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="9ff3e-126">연결 이름 *</span><span class="sxs-lookup"><span data-stu-id="9ff3e-126">Connection Name *</span></span> |<span data-ttu-id="9ff3e-127">연결의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3e-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="9ff3e-128">통합 계정 *</span><span class="sxs-lookup"><span data-stu-id="9ff3e-128">Integration Account *</span></span> |<span data-ttu-id="9ff3e-129">통합 계정의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3e-129">Enter a name for your integration account.</span></span> <span data-ttu-id="9ff3e-130">통합 계정 및 논리 앱 hello에 있는지 확인 동일한 Azure 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3e-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="9ff3e-131">완료 되 면 연결 정보가 이와 유사한 toothis 예가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3e-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="9ff3e-132">연결을 만드는 toofinish 선택 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3e-132">toofinish creating your connection, choose **Create**.</span></span>

    ![통합 계정 연결 세부 사항](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage2.png)

    <span data-ttu-id="9ff3e-134">새로운 연결이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3e-134">Your connection is now created.</span></span>

    ![통합 계정 연결 생성](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage4.png)

#### <a name="encode-edifact-message-by-agreement-name"></a><span data-ttu-id="9ff3e-136">규약 이름으로 EDIFACT 메시지 인코딩</span><span class="sxs-lookup"><span data-stu-id="9ff3e-136">Encode EDIFACT Message by agreement name</span></span>

<span data-ttu-id="9ff3e-137">를 선택한 경우 tooencode EDIFACT 메시지 계약 이름으로 열고 hello **이름의 EDIFACT 규약** 목록, 입력 또는 EDIFACT 계약 이름을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3e-137">If you chose tooencode EDIFACT messages by agreement name, open hello **Name of EDIFACT agreement** list, enter or select your EDIFACT agreement name.</span></span> <span data-ttu-id="9ff3e-138">XML 메시지 tooencode hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3e-138">Enter hello XML message tooencode.</span></span>

![XML 메시지 tooencode 및 EDIFACT 계약 이름 입력](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage6.png)

#### <a name="encode-edifact-message-by-identities"></a><span data-ttu-id="9ff3e-140">ID로 EDIFACT 메시지 인코딩</span><span class="sxs-lookup"><span data-stu-id="9ff3e-140">Encode EDIFACT Message by identities</span></span>

<span data-ttu-id="9ff3e-141">를 선택 하면 tooencode EDIFACT 메시지 identities 하 여 hello 보낸 사람 식별자, 보낸 사람 한정자, 받는 사람 식별자 및 받는 사람 한정자 EDIFACT 규약에 구성 된 대로 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3e-141">If you choose tooencode EDIFACT messages by identities, enter hello sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your EDIFACT agreement.</span></span> <span data-ttu-id="9ff3e-142">XML 메시지 tooencode hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3e-142">Select hello XML message tooencode.</span></span>

![XML 메시지 tooencode 선택, 발신자와 수신자에 대 한 id를 제공 합니다.](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage7.png)

## <a name="edifact-encode-details"></a><span data-ttu-id="9ff3e-144">EDIFACT 인코딩 세부 정보</span><span class="sxs-lookup"><span data-stu-id="9ff3e-144">EDIFACT Encode details</span></span>

<span data-ttu-id="9ff3e-145">hello EDIFACT 인코딩 커넥터 이러한 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3e-145">hello Encode EDIFACT connector performs these tasks:</span></span> 

* <span data-ttu-id="9ff3e-146">Hello 보낸 사람 한정자 및 식별자, 받는 사람 한정자 및 식별자를 비교 하 여 hello 규약을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3e-146">Resolve hello agreement by matching hello sender qualifier & identifier and receiver qualifier and identifier</span></span>
* <span data-ttu-id="9ff3e-147">Hello 교환에 EDI 트랜잭션 집합 XML로 인코딩된 메시지 변환 hello EDI 교환으로 직렬화 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3e-147">Serializes hello EDI interchange, converting XML-encoded messages into EDI transaction sets in hello interchange.</span></span>
* <span data-ttu-id="9ff3e-148">트랜잭션 집합 헤더 및 트레일러 세그먼트를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3e-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="9ff3e-149">교환 제어 번호, 그룹 제어 번호 및 나가는 교환 각각에 대한 트랜잭션 집합 제어 번호를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3e-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="9ff3e-150">Hello 페이로드 데이터에는 구분 기호를 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3e-150">Replaces separators in hello payload data</span></span>
* <span data-ttu-id="9ff3e-151">EDI 및 파트너 관련 속성의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3e-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="9ff3e-152">스키마 유효성 검사 hello 메시지 스키마에 대해 hello 트랜잭션 집합 데이터 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3e-152">Schema validation of hello transaction-set data elements against hello message schema.</span></span>
  * <span data-ttu-id="9ff3e-153">트랜잭션 집합 데이터 요소에서 수행한 EDI 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="9ff3e-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="9ff3e-154">트랜잭션 집합 데이터 요소에서 수행한 확장된 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="9ff3e-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="9ff3e-155">각 트랜잭션 집합에 대한 XML 문서를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3e-155">Generates an XML document for each transaction set.</span></span>
* <span data-ttu-id="9ff3e-156">기술 및/또는 기능 승인을 요청합니다(구성된 경우).</span><span class="sxs-lookup"><span data-stu-id="9ff3e-156">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="9ff3e-157">기술 승인으로 CONTRL 메시지 hello는 교환 수신을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3e-157">As a technical acknowledgment, hello CONTRL message indicates receipt of an interchange.</span></span>
  * <span data-ttu-id="9ff3e-158">기능 승인으로 CONTRL 메시지 hello의 수락 또는 거부 hello 받은 교환, 그룹 또는 메시지를 오류 또는 지원 되지 않는 기능 목록이 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3e-158">As a functional acknowledgment, hello CONTRL message indicates acceptance or rejection of hello received interchange, group, or message, with a list of errors or unsupported functionality</span></span>

## <a name="view-swagger-file"></a><span data-ttu-id="9ff3e-159">Swagger 파일 보기</span><span class="sxs-lookup"><span data-stu-id="9ff3e-159">View Swagger file</span></span>
<span data-ttu-id="9ff3e-160">tooview hello Swagger hello EDIFACT 커넥터에 대 한 내용은 [EDIFACT](/connectors/edifact/)합니다.</span><span class="sxs-lookup"><span data-stu-id="9ff3e-160">tooview hello Swagger details for hello EDIFACT connector, see [EDIFACT](/connectors/edifact/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ff3e-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9ff3e-161">Next steps</span></span>
[<span data-ttu-id="9ff3e-162">엔터프라이즈 통합 팩 hello에 대 한 자세한</span><span class="sxs-lookup"><span data-stu-id="9ff3e-162">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "엔터프라이즈 통합 팩에 대 한 자세한 정보") 

