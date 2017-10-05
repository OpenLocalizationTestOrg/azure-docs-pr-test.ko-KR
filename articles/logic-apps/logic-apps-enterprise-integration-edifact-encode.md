---
title: "EDIFACT 메시지 인코딩 - Azure Logic Apps | Microsoft Docs"
description: "Azure Logic Apps의 엔터프라이즈 통합 팩에서 EDIFACT 메시지 인코더를 사용하여 EDI 유효성 검사 및 XML 생성"
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
ms.openlocfilehash: b8d577326d23ec45cb4a9ec0e450ebf7afd945f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="encode-edifact-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="8ddad-103">엔터프라이즈 통합 팩이 포함된 Azure Logic Apps에 대한 EDIFACT 메시지 인코딩</span><span class="sxs-lookup"><span data-stu-id="8ddad-103">Encode EDIFACT messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="8ddad-104">EDIFACT 메시지 인코딩 커넥터를 사용하여 EDI 및 파트너 관련 속성의 유효성을 검사하고 각 트랜잭션 집합에 XML 문서를 생성하고 기술 승인, 기능 승인 또는 둘 다를 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ddad-104">With the Encode EDIFACT message connector, you can validate EDI and partner-specific properties, generate an XML document for each transaction set, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="8ddad-105">이 커넥터를 사용하려면 논리 앱에서 기존 트리거에 커넥터를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ddad-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="8ddad-106">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="8ddad-106">Before you start</span></span>

<span data-ttu-id="8ddad-107">필요한 항목은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8ddad-107">Here's the items you need:</span></span>

* <span data-ttu-id="8ddad-108">Azure 계정의 경우 [무료 계정](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="8ddad-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="8ddad-109">[통합 계정](logic-apps-enterprise-integration-create-integration-account.md)이 이미 정의되고 Azure 구독과 연결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8ddad-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="8ddad-110">EDIFACT 메시지 인코딩 커넥터를 사용하는 통합 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ddad-110">You must have an integration account to use the Encode EDIFACT message connector.</span></span> 
* <span data-ttu-id="8ddad-111">통합 계정에 이미 정의된 둘 이상의 [파트너](logic-apps-enterprise-integration-partners.md)</span><span class="sxs-lookup"><span data-stu-id="8ddad-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="8ddad-112">통합 계정에 이미 정의된 [EDIFACT 규약](logic-apps-enterprise-integration-edifact.md)</span><span class="sxs-lookup"><span data-stu-id="8ddad-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span></span>

## <a name="encode-edifact-messages"></a><span data-ttu-id="8ddad-113">EDIFACT 메시지 인코딩</span><span class="sxs-lookup"><span data-stu-id="8ddad-113">Encode EDIFACT messages</span></span>

1. <span data-ttu-id="8ddad-114">[논리 앱 만들기](logic-apps-create-a-logic-app.md)</span><span class="sxs-lookup"><span data-stu-id="8ddad-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="8ddad-115">EDIFACT 메시지 인코딩 커넥터에는 트리거가 없으므로 요청 트리거와 마찬가지로 논리 앱을 시작하는 트리거를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ddad-115">The Encode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="8ddad-116">Logic App Designer에서 트리거를 추가하고 작업을 논리 앱에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8ddad-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="8ddad-117">검색 상자에서 필터로 "EDIFACT"를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8ddad-117">In the search box, enter "EDIFACT" as your filter.</span></span> <span data-ttu-id="8ddad-118">**규약 이름으로 EDIFACT 메시지 인코딩** 또는 **ID로 EDIFACT 메시지 인코딩** 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ddad-118">Select either **Encode EDIFACT Message by agreement name** or **Encode to EDIFACT message by identities**.</span></span>
   
    ![EDIFACT 검색](media/logic-apps-enterprise-integration-edifact-encode/edifactdecodeimage1.png)  

3. <span data-ttu-id="8ddad-120">이전에 통합 계정에 연결을 만들지 않은 경우 이제 해당 연결을 만들라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="8ddad-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="8ddad-121">연결의 이름을 지정하고 연결하려는 통합 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ddad-121">Name your connection, and select the integration account that you want to connect.</span></span>

    ![통합 계정 연결 만들기](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage1.png)  

    <span data-ttu-id="8ddad-123">별표가 있는 속성은 필수 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="8ddad-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="8ddad-124">속성</span><span class="sxs-lookup"><span data-stu-id="8ddad-124">Property</span></span> | <span data-ttu-id="8ddad-125">세부 정보</span><span class="sxs-lookup"><span data-stu-id="8ddad-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="8ddad-126">연결 이름 *</span><span class="sxs-lookup"><span data-stu-id="8ddad-126">Connection Name *</span></span> |<span data-ttu-id="8ddad-127">연결의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8ddad-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="8ddad-128">통합 계정 *</span><span class="sxs-lookup"><span data-stu-id="8ddad-128">Integration Account *</span></span> |<span data-ttu-id="8ddad-129">통합 계정의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8ddad-129">Enter a name for your integration account.</span></span> <span data-ttu-id="8ddad-130">통합 계정 및 논리 앱이 동일한 Azure 위치에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ddad-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="8ddad-131">완료되면 연결 정보는 이 예제와 유사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ddad-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="8ddad-132">연결 만들기를 완료하려면 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ddad-132">To finish creating your connection, choose **Create**.</span></span>

    ![통합 계정 연결 세부 사항](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage2.png)

    <span data-ttu-id="8ddad-134">새로운 연결이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="8ddad-134">Your connection is now created.</span></span>

    ![통합 계정 연결 생성](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage4.png)

#### <a name="encode-edifact-message-by-agreement-name"></a><span data-ttu-id="8ddad-136">규약 이름으로 EDIFACT 메시지 인코딩</span><span class="sxs-lookup"><span data-stu-id="8ddad-136">Encode EDIFACT Message by agreement name</span></span>

<span data-ttu-id="8ddad-137">규약 이름으로 EDIFACT 메시지를 인코딩하도록 선택한 경우  **규약의 이름** 목록을 열고 EDIFACT 규약 이름을 입력 또는 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ddad-137">If you chose to encode EDIFACT messages by agreement name, open the **Name of EDIFACT agreement** list, enter or select your EDIFACT agreement name.</span></span> <span data-ttu-id="8ddad-138">인코딩할 XML 메시지를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8ddad-138">Enter the XML message to encode.</span></span>

![인코딩할 EDIFACT 규약 이름 및 XML 메시지를 입력합니다.](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage6.png)

#### <a name="encode-edifact-message-by-identities"></a><span data-ttu-id="8ddad-140">ID로 EDIFACT 메시지 인코딩</span><span class="sxs-lookup"><span data-stu-id="8ddad-140">Encode EDIFACT Message by identities</span></span>

<span data-ttu-id="8ddad-141">ID로 EDIFACT 메시지를 인코딩하도록 선택한 경우 보낸 사람 식별자, 보낸 사람 한정자, 받는 사람 식별자 및 받는 사람 한정자를 EDIFACT 규약에 구성된 대로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8ddad-141">If you choose to encode EDIFACT messages by identities, enter the sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your EDIFACT agreement.</span></span> <span data-ttu-id="8ddad-142">인코딩할 XML 메시지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ddad-142">Select the XML message to encode.</span></span>

![보낸 사람 및 받는 사람에 대한 ID를 제공하고 인코딩할 XML 메시지를 선택합니다.](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage7.png)

## <a name="edifact-encode-details"></a><span data-ttu-id="8ddad-144">EDIFACT 인코딩 세부 정보</span><span class="sxs-lookup"><span data-stu-id="8ddad-144">EDIFACT Encode details</span></span>

<span data-ttu-id="8ddad-145">EDIFACT 인코딩 커넥터는 다음과 같은 태스크를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8ddad-145">The Encode EDIFACT connector performs these tasks:</span></span> 

* <span data-ttu-id="8ddad-146">보낸 사람 한정자와 식별자 및 받는 사람 한정자와 식별자를 일치시켜 규약을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8ddad-146">Resolve the agreement by matching the sender qualifier & identifier and receiver qualifier and identifier</span></span>
* <span data-ttu-id="8ddad-147">EDI 교환을 직렬화하며 XML로 인코딩된 메시지를 교환에서 EDI 트랜잭션 집합으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="8ddad-147">Serializes the EDI interchange, converting XML-encoded messages into EDI transaction sets in the interchange.</span></span>
* <span data-ttu-id="8ddad-148">트랜잭션 집합 헤더 및 트레일러 세그먼트를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="8ddad-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="8ddad-149">교환 제어 번호, 그룹 제어 번호 및 나가는 교환 각각에 대한 트랜잭션 집합 제어 번호를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="8ddad-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="8ddad-150">페이로드 데이터에서 구분 기호를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8ddad-150">Replaces separators in the payload data</span></span>
* <span data-ttu-id="8ddad-151">EDI 및 파트너 관련 속성의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="8ddad-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="8ddad-152">메시지 스키마에 대한 트랜잭션 집합 데이터 요소의 스키마 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="8ddad-152">Schema validation of the transaction-set data elements against the message schema.</span></span>
  * <span data-ttu-id="8ddad-153">트랜잭션 집합 데이터 요소에서 수행한 EDI 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="8ddad-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="8ddad-154">트랜잭션 집합 데이터 요소에서 수행한 확장된 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="8ddad-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="8ddad-155">각 트랜잭션 집합에 대한 XML 문서를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="8ddad-155">Generates an XML document for each transaction set.</span></span>
* <span data-ttu-id="8ddad-156">기술 및/또는 기능 승인을 요청합니다(구성된 경우).</span><span class="sxs-lookup"><span data-stu-id="8ddad-156">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="8ddad-157">기술 승인인 CONTRL 메시지는 교환 수신을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8ddad-157">As a technical acknowledgment, the CONTRL message indicates receipt of an interchange.</span></span>
  * <span data-ttu-id="8ddad-158">기능 승인인 CONTRL 메시지는 오류 또는 지원되지 않는 기능 목록과 함께 수신된 교환, 그룹 또는 메시지의 승인 또는 거부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8ddad-158">As a functional acknowledgment, the CONTRL message indicates acceptance or rejection of the received interchange, group, or message, with a list of errors or unsupported functionality</span></span>

## <a name="view-swagger-file"></a><span data-ttu-id="8ddad-159">Swagger 파일 보기</span><span class="sxs-lookup"><span data-stu-id="8ddad-159">View Swagger file</span></span>
<span data-ttu-id="8ddad-160">EDIFACT 커넥터에 대 한 Swagger 세부 정보를 보려면 [EDIFACT](/connectors/edifact/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8ddad-160">To view the Swagger details for the EDIFACT connector, see [EDIFACT](/connectors/edifact/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ddad-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8ddad-161">Next steps</span></span>
[<span data-ttu-id="8ddad-162">엔터프라이즈 통합 팩에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="8ddad-162">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "엔터프라이즈 통합 팩에 대해 알아보기") 

