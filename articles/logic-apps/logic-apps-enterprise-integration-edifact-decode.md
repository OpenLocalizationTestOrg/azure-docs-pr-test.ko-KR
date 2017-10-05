---
title: "EDIFACT 메시지 디코딩 - Azure Logic Apps | Microsoft Docs"
description: "Azure Logic Apps의 엔터프라이즈 통합 팩에서 EDIFACT 메시지 디코더를 사용하여 EDI 유효성 검사 및 승인 생성"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 0e61501d-21a2-4419-8c6c-88724d346e81
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: e3787b48037360bf6066ddce2bacba6842213b2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="decode-edifact-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="74194-103">엔터프라이즈 통합 팩이 포함된 Azure Logic Apps에 대한 EDIFACT 메시지 디코딩</span><span class="sxs-lookup"><span data-stu-id="74194-103">Decode EDIFACT messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="74194-104">EDIFACT 메시지 디코드 커넥터를 사용하여 유효성을 검사하고, EDI 및 파트너별 속성의 유효성을 검사하고, 교환을 트랜잭션 집합으로 분할하거나 전체 교환을 유지하고, 처리된 트랜잭션에 대한 승인을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74194-104">With the Decode EDIFACT message connector, you can validate EDI and partner-specific properties, split interchanges into transactions sets or preserve entire interchanges, and generate acknowledgments for processed transactions.</span></span> <span data-ttu-id="74194-105">이 커넥터를 사용하려면 논리 앱에서 기존 트리거에 커넥터를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74194-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="74194-106">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="74194-106">Before you start</span></span>

<span data-ttu-id="74194-107">필요한 항목은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="74194-107">Here's the items you need:</span></span>

* <span data-ttu-id="74194-108">Azure 계정의 경우 [무료 계정](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="74194-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="74194-109">[통합 계정](logic-apps-enterprise-integration-create-integration-account.md)이 이미 정의되고 Azure 구독과 연결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="74194-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="74194-110">EDIFACT 메시지 디코딩 커넥터를 사용하는 통합 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74194-110">You must have an integration account to use the Decode EDIFACT message connector.</span></span> 
* <span data-ttu-id="74194-111">통합 계정에 이미 정의된 둘 이상의 [파트너](logic-apps-enterprise-integration-partners.md)</span><span class="sxs-lookup"><span data-stu-id="74194-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="74194-112">통합 계정에 이미 정의된 [EDIFACT 규약](logic-apps-enterprise-integration-edifact.md)</span><span class="sxs-lookup"><span data-stu-id="74194-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span></span>

## <a name="decode-edifact-messages"></a><span data-ttu-id="74194-113">EDIFACT 메시지 디코딩</span><span class="sxs-lookup"><span data-stu-id="74194-113">Decode EDIFACT messages</span></span>

1. <span data-ttu-id="74194-114">[논리 앱 만들기](logic-apps-create-a-logic-app.md)</span><span class="sxs-lookup"><span data-stu-id="74194-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="74194-115">EDIFACT 메시지 디코딩 커넥터에는 트리거가 없으므로 요청 트리거와 마찬가지로 논리 앱을 시작하는 트리거를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74194-115">The Decode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="74194-116">Logic App Designer에서 트리거를 추가하고 작업을 논리 앱에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="74194-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3. <span data-ttu-id="74194-117">검색 상자에서 필터로 "EDIFACT"를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="74194-117">In the search box, enter "EDIFACT" as your filter.</span></span> <span data-ttu-id="74194-118">**EDIFACT 메시지 디코딩**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74194-118">Select **Decode EDIFACT Message**.</span></span>
   
    ![EDIFACT 검색](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage1.png)

3. <span data-ttu-id="74194-120">이전에 통합 계정에 연결을 만들지 않은 경우 이제 해당 연결을 만들라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="74194-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="74194-121">연결의 이름을 지정하고 연결하려는 통합 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74194-121">Name your connection, and select the integration account that you want to connect.</span></span>
   
    ![통합 계정 만들기](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage2.png)

    <span data-ttu-id="74194-123">별표가 있는 속성은 필수 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="74194-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="74194-124">속성</span><span class="sxs-lookup"><span data-stu-id="74194-124">Property</span></span> | <span data-ttu-id="74194-125">세부 정보</span><span class="sxs-lookup"><span data-stu-id="74194-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="74194-126">연결 이름 *</span><span class="sxs-lookup"><span data-stu-id="74194-126">Connection Name *</span></span> |<span data-ttu-id="74194-127">연결의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="74194-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="74194-128">통합 계정 *</span><span class="sxs-lookup"><span data-stu-id="74194-128">Integration Account *</span></span> |<span data-ttu-id="74194-129">통합 계정의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="74194-129">Enter a name for your integration account.</span></span> <span data-ttu-id="74194-130">통합 계정 및 논리 앱이 동일한 Azure 위치에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74194-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

4. <span data-ttu-id="74194-131">연결 만들기를 완료한 경우 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74194-131">When you're done to finish creating your connection, choose **Create**.</span></span> <span data-ttu-id="74194-132">연결 정보는 이 예제와 유사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74194-132">Your connection details should look similar to this example:</span></span>

    ![통합 계정 세부 정보](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage3.png)  

5. <span data-ttu-id="74194-134">이 예제와 같이 연결을 만든 후에 디코딩할 EDIFACT 플랫 파일 메시지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74194-134">After your connection is created, as shown in this example, select the EDIFACT flat file message to decode.</span></span>

    ![통합 계정 연결 생성](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage4.png)  

    <span data-ttu-id="74194-136">예:</span><span class="sxs-lookup"><span data-stu-id="74194-136">For example:</span></span>

    ![디코딩할 EDIFACT 플랫 파일 메시지를 선택합니다.](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage5.png)  

## <a name="edifact-decoder-details"></a><span data-ttu-id="74194-138">EDIFACT 디코더 세부 정보</span><span class="sxs-lookup"><span data-stu-id="74194-138">EDIFACT decoder details</span></span>

<span data-ttu-id="74194-139">EDIFACT 디코딩 커넥터는 다음과 같은 태스크를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="74194-139">The Decode EDIFACT connector performs these tasks:</span></span> 

* <span data-ttu-id="74194-140">거래 업체 규약에 대한 봉투의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="74194-140">Validates the envelope against trading partner agreement.</span></span>
* <span data-ttu-id="74194-141">보낸 사람 한정자와 식별자 및 받는 사람 한정자와 식별자를 일치시켜 규약을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="74194-141">Resolves the agreement by matching the sender qualifier & identifier and receiver qualifier & identifier.</span></span>
* <span data-ttu-id="74194-142">교환에 규약의 수신 설정 구성을 기반으로 하는 둘 이상의 트랜잭션이 있는 경우 여러 트랜잭션으로 교환을 분할합니다.</span><span class="sxs-lookup"><span data-stu-id="74194-142">Splits an interchange into multiple transactions when the interchange has more than one transaction based on the agreement's receive settings configuration.</span></span>
* <span data-ttu-id="74194-143">교환을 역어셈블합니다.</span><span class="sxs-lookup"><span data-stu-id="74194-143">Disassembles the interchange.</span></span>
* <span data-ttu-id="74194-144">다음을 포함하는 EDI 및 파트너 관련 속성의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="74194-144">Validates EDI and partner-specific properties including:</span></span>
  * <span data-ttu-id="74194-145">교환 봉투 구조의 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="74194-145">Validation of the interchange envelope structure</span></span>
  * <span data-ttu-id="74194-146">제어 스키마에 대한 봉투의 스키마 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="74194-146">Schema validation of the envelope against the control schema</span></span>
  * <span data-ttu-id="74194-147">메시지 스키마에 대한 트랜잭션 집합 데이터 요소의 스키마 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="74194-147">Schema validation of the transaction-set data elements against the message schema</span></span>
  * <span data-ttu-id="74194-148">트랜잭션 집합 데이터 요소에서 수행한 EDI 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="74194-148">EDI validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="74194-149">교환, 그룹 및 트랜잭션 집합 제어 번호가 중복되지 않았는지 확인합니다(구성된 경우).</span><span class="sxs-lookup"><span data-stu-id="74194-149">Verifies that the interchange, group, and transaction set control numbers are not duplicates (if configured)</span></span> 
  * <span data-ttu-id="74194-150">이전에 받은 교환에 대한 교환 제어 번호를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="74194-150">Checks the interchange control number against previously received interchanges.</span></span> 
  * <span data-ttu-id="74194-151">교환에 있는 다른 그룹 제어 번호에 대한 그룹 제어 번호를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="74194-151">Checks the group control number against other group control numbers in the interchange.</span></span> 
  * <span data-ttu-id="74194-152">해당 그룹의 다른 트랜잭션 집합 제어 번호에 대한 트랜잭션 집합 제어 번호를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="74194-152">Checks the transaction set control number against other transaction set control numbers in that group.</span></span>
* <span data-ttu-id="74194-153">교환을 트랜잭션 집합으로 분할하거나 전체 교환을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="74194-153">Splits the interchange into transaction sets, or preserves the entire interchange:</span></span>
  * <span data-ttu-id="74194-154">교환을 트랜잭션 집합으로 분할 - 오류 발생 시 트랜잭션 일시 중단: 교환을 트랜잭션 집합으로 분할하고 각 트랜잭션 집합을 구문 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="74194-154">Split Interchange as transaction sets - suspend transaction sets on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="74194-155">X12 디코드 작업은 유효성 검사에 실패한 트랜잭션 집합만 `badMessages`에 출력하고, 나머지 트랜잭션 집합은 `goodMessages`에 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="74194-155">The X12 Decode action outputs only those transaction sets that fail validation to `badMessages`, and outputs the remaining transactions sets to `goodMessages`.</span></span>
  * <span data-ttu-id="74194-156">교환을 트랜잭션 집합으로 분할 - 오류 발생 시 교환 일시 중단: 교환을 트랜잭션 집합으로 분할하고 각 트랜잭션 집합을 구문 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="74194-156">Split Interchange as transaction sets - suspend interchange on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="74194-157">교환에 포함된 하나 이상의 트랜잭션 집합이 유효성 검사에 실패할 경우 X12 디코드 작업은 해당 교환에 포함된 모든 트랜잭션 집합을 `badMessages`에 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="74194-157">If one or more transaction sets in the interchange fail validation, the X12 Decode action outputs all the transaction sets in that interchange to `badMessages`.</span></span>
  * <span data-ttu-id="74194-158">교환 유지- 오류 발생 시 트랜잭션 집합 일시 중단: 교환을 유지하고 일괄 처리된 전체 교환을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="74194-158">Preserve Interchange - suspend transaction sets on error: Preserve the interchange and process the entire batched interchange.</span></span> 
  <span data-ttu-id="74194-159">X12 디코드 작업은 유효성 검사에 실패한 트랜잭션 집합만 `badMessages`에 출력하고, 나머지 트랜잭션 집합은 `goodMessages`에 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="74194-159">The X12 Decode action outputs only those transaction sets that fail validation to `badMessages`, and outputs the remaining transactions sets to `goodMessages`.</span></span>
  * <span data-ttu-id="74194-160">교환 유지- 오류 발생 시 교환 일시 중단: 교환을 유지하고 일괄 처리된 전체 교환을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="74194-160">Preserve Interchange - suspend interchange on error: Preserve the interchange and process the entire batched interchange.</span></span> 
  <span data-ttu-id="74194-161">교환에 포함된 하나 이상의 트랜잭션 집합이 유효성 검사에 실패할 경우 X12 디코드 작업은 해당 교환에 포함된 모든 트랜잭션 집합을 `badMessages`에 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="74194-161">If one or more transaction sets in the interchange fail validation, the X12 Decode action outputs all the transaction sets in that interchange to `badMessages`.</span></span>
* <span data-ttu-id="74194-162">기술(제어) 및/또는 기능 승인을 생성합니다(구성된 경우).</span><span class="sxs-lookup"><span data-stu-id="74194-162">Generates a Technical (control) and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="74194-163">기술 승인 또는 제어 승인은 받은 교환 전체의 구문 검사 결과를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="74194-163">A Technical Acknowledgment or the CONTRL ACK reports the results of a syntactical check of the complete received interchange.</span></span>
  * <span data-ttu-id="74194-164">기능 승인은 수신된 교환 또는 그룹을 허용하거나 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="74194-164">A functional acknowledgment acknowledges accept or reject a received interchange or a group</span></span>

## <a name="view-swagger-file"></a><span data-ttu-id="74194-165">Swagger 파일 보기</span><span class="sxs-lookup"><span data-stu-id="74194-165">View Swagger file</span></span>
<span data-ttu-id="74194-166">EDIFACT 커넥터에 대 한 Swagger 세부 정보를 보려면 [EDIFACT](/connectors/edifact/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="74194-166">To view the Swagger details for the EDIFACT connector, see [EDIFACT](/connectors/edifact/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="74194-167">다음 단계</span><span class="sxs-lookup"><span data-stu-id="74194-167">Next steps</span></span>
[<span data-ttu-id="74194-168">엔터프라이즈 통합 팩에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="74194-168">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "엔터프라이즈 통합 팩에 대해 알아보기") 

