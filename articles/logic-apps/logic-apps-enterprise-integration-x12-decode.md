---
title: "aaaDecode X12 메시지-Azure 논리 앱 | Microsoft Docs"
description: "EDI 유효성 검사 및 Azure 논리 앱에 대 한 hello 엔터프라이즈 통합 팩에서에서 X12 hello 메시지 디코더와 승인을 생성합니다"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 4fd48d2d-2008-4080-b6a1-8ae183b48131
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 1ffececca1ff835b319b64c85f86c421395833c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="decode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="40e8a-103">X12 디코딩할 엔터프라이즈 통합 팩 hello로 Azure 논리 앱에 대 한 메시지</span><span class="sxs-lookup"><span data-stu-id="40e8a-103">Decode X12 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="40e8a-104">Hello 디코드 X12 메시지 연결선 거래 업체 규약에 대 한 hello 봉투 (envelope) 유효성 검사, EDI 및 파트너 관련 속성의 유효성을 검사, 교환을 트랜잭션 집합으로 분할 또는 전체 교환을 유지 하 고 사용할 수 생성 처리 된 트랜잭션에 대 한 승인 합니다.</span><span class="sxs-lookup"><span data-stu-id="40e8a-104">With hello Decode X12 message connector, you can validate hello envelope against a trading partner agreement, validate EDI and partner-specific properties, split interchanges into transactions sets or preserve entire interchanges, and generate acknowledgments for processed transactions.</span></span> <span data-ttu-id="40e8a-105">toouse이이 커넥터를 트리거 논리 앱에서 기존 hello 커넥터 tooan 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40e8a-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="40e8a-106">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="40e8a-106">Before you start</span></span>

<span data-ttu-id="40e8a-107">다음은 필요한 hello 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="40e8a-107">Here's hello items you need:</span></span>

* <span data-ttu-id="40e8a-108">Azure 계정의 경우 [무료 계정](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="40e8a-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="40e8a-109">[통합 계정](logic-apps-enterprise-integration-create-integration-account.md)이 이미 정의되고 Azure 구독과 연결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="40e8a-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="40e8a-110">통합 계정 toouse hello 디코드 X12 메시지 연결선이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40e8a-110">You must have an integration account toouse hello Decode X12 message connector.</span></span>
* <span data-ttu-id="40e8a-111">통합 계정에 이미 정의된 둘 이상의 [파트너](logic-apps-enterprise-integration-partners.md)</span><span class="sxs-lookup"><span data-stu-id="40e8a-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="40e8a-112">통합 계정에 이미 정의된 [X12 규약](logic-apps-enterprise-integration-x12.md)</span><span class="sxs-lookup"><span data-stu-id="40e8a-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span></span>

## <a name="decode-x12-messages"></a><span data-ttu-id="40e8a-113">X12 디코딩 메시지</span><span class="sxs-lookup"><span data-stu-id="40e8a-113">Decode X12 messages</span></span>

1. <span data-ttu-id="40e8a-114">[논리 앱 만들기](logic-apps-create-a-logic-app.md)</span><span class="sxs-lookup"><span data-stu-id="40e8a-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="40e8a-115">hello 디코드 X12 메시지 연결선은 트리거, 갖고 있지 않으므로 요청 트리거와 마찬가지로 논리 앱을 시작 하는 트리거를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40e8a-115">hello Decode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="40e8a-116">Hello 논리가 응용 프로그램 디자이너에서에서 트리거를 추가 하 고 작업 tooyour 논리 앱을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="40e8a-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="40e8a-117">Hello 검색 상자에 필터에 대 한 "x12"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="40e8a-117">In hello search box, enter "x12" for your filter.</span></span> <span data-ttu-id="40e8a-118">**X12 - X12 메시지 디코딩**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40e8a-118">Select **X12 - Decode X12 message**.</span></span>
   
    !["x12" 검색](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage1.png)  

3. <span data-ttu-id="40e8a-120">직접 만들지 않은 경우 이전에 모든 연결이 tooyour 통합 계정, 메시지가 toocreate 지금 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="40e8a-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="40e8a-121">사용자의 연결 이름을 지정 하 고 원하는 tooconnect hello 통합 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="40e8a-121">Name your connection, and select hello integration account that you want tooconnect.</span></span> 

    ![통합 계정 연결 세부 사항 제공](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage4.png)

    <span data-ttu-id="40e8a-123">별표가 있는 속성은 필수 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="40e8a-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="40e8a-124">속성</span><span class="sxs-lookup"><span data-stu-id="40e8a-124">Property</span></span> | <span data-ttu-id="40e8a-125">세부 정보</span><span class="sxs-lookup"><span data-stu-id="40e8a-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="40e8a-126">연결 이름 *</span><span class="sxs-lookup"><span data-stu-id="40e8a-126">Connection Name *</span></span> |<span data-ttu-id="40e8a-127">연결의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="40e8a-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="40e8a-128">통합 계정 *</span><span class="sxs-lookup"><span data-stu-id="40e8a-128">Integration Account *</span></span> |<span data-ttu-id="40e8a-129">통합 계정의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="40e8a-129">Enter a name for your integration account.</span></span> <span data-ttu-id="40e8a-130">통합 계정 및 논리 앱 hello에 있는지 확인 동일한 Azure 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="40e8a-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="40e8a-131">완료 되 면 연결 정보가 이와 유사한 toothis 예가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40e8a-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="40e8a-132">연결을 만드는 toofinish 선택 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="40e8a-132">toofinish creating your connection, choose **Create**.</span></span>
   
    ![통합 계정 연결 세부 사항](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage5.png) 

6. <span data-ttu-id="40e8a-134">연결을 만든 후이 예제에 나와 있는 것 처럼, X12 hello 플랫 파일 메시지 toodecode를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="40e8a-134">After your connection is created, as shown in this example, select hello X12 flat file message toodecode.</span></span>

    ![통합 계정 연결 생성](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage6.png) 

    <span data-ttu-id="40e8a-136">예:</span><span class="sxs-lookup"><span data-stu-id="40e8a-136">For example:</span></span>

    ![디코딩할 X12 플랫 파일 메시지를 선택합니다.](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage7.png) 

## <a name="x12-decode-details"></a><span data-ttu-id="40e8a-138">X12 디코딩 세부 정보</span><span class="sxs-lookup"><span data-stu-id="40e8a-138">X12 Decode details</span></span>

<span data-ttu-id="40e8a-139">hello X12 디코드 커넥터 이러한 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="40e8a-139">hello X12 Decode connector performs these tasks:</span></span>

* <span data-ttu-id="40e8a-140">거래 업체 규약에 대 한 hello 봉투 (envelope)의 유효성을 검사합니다</span><span class="sxs-lookup"><span data-stu-id="40e8a-140">Validates hello envelope against trading partner agreement</span></span>
* <span data-ttu-id="40e8a-141">EDI 및 파트너 관련 속성의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="40e8a-141">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="40e8a-142">EDI 구조 유효성 검사 및 확장된 스키마 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="40e8a-142">EDI structural validation, and extended schema validation</span></span>
  * <span data-ttu-id="40e8a-143">유효성 검사 hello 교환 봉투 (envelope)의 hello 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="40e8a-143">Validation of hello structure of hello interchange envelope.</span></span>
  * <span data-ttu-id="40e8a-144">Hello 컨트롤 스키마에 대해 hello 봉투 (envelope)의 스키마 유효성 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="40e8a-144">Schema validation of hello envelope against hello control schema.</span></span>
  * <span data-ttu-id="40e8a-145">스키마 유효성 검사 hello 메시지 스키마에 대해 hello 트랜잭션 집합 데이터 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="40e8a-145">Schema validation of hello transaction-set data elements against hello message schema.</span></span>
  * <span data-ttu-id="40e8a-146">트랜잭션 집합 데이터 요소에서 수행한 EDI 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="40e8a-146">EDI validation performed on transaction-set data elements</span></span> 
* <span data-ttu-id="40e8a-147">Hello 교환, 그룹 및 트랜잭션 집합 컨트롤 번호가 중복 되지 않은 확인</span><span class="sxs-lookup"><span data-stu-id="40e8a-147">Verifies that hello interchange, group, and transaction set control numbers are not duplicates</span></span>
  * <span data-ttu-id="40e8a-148">이전에 받은 교환 기준 hello 교환 컨트롤 번호를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="40e8a-148">Checks hello interchange control number against previously received interchanges.</span></span>
  * <span data-ttu-id="40e8a-149">Hello 교환에서 다른 그룹 컨트롤 번호에 대 한 hello 그룹 컨트롤 번호를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="40e8a-149">Checks hello group control number against other group control numbers in hello interchange.</span></span>
  * <span data-ttu-id="40e8a-150">해당 그룹의 다른 트랜잭션 집합 컨트롤 번호에 대 한 hello 트랜잭션 집합 컨트롤 번호를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="40e8a-150">Checks hello transaction set control number against other transaction set control numbers in that group.</span></span>
* <span data-ttu-id="40e8a-151">Hello 교환을 트랜잭션 집합으로 분할 또는 hello 전체 교환 유지:</span><span class="sxs-lookup"><span data-stu-id="40e8a-151">Splits hello interchange into transaction sets, or preserves hello entire interchange:</span></span>
  * <span data-ttu-id="40e8a-152">교환을 트랜잭션 집합으로 분할 - 오류 발생 시 트랜잭션 일시 중단: 교환을 트랜잭션 집합으로 분할하고 각 트랜잭션 집합을 구문 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="40e8a-152">Split Interchange as transaction sets - suspend transaction sets on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="40e8a-153">hello X12 디코드 작업 출력 너무 유효성 검사에 실패 하는 해당 트랜잭션 집합만`badMessages`, 남은 트랜잭션 hello 설정 너무 출력`goodMessages`합니다.</span><span class="sxs-lookup"><span data-stu-id="40e8a-153">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="40e8a-154">교환을 트랜잭션 집합으로 분할 - 오류 발생 시 교환 일시 중단: 교환을 트랜잭션 집합으로 분할하고 각 트랜잭션 집합을 구문 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="40e8a-154">Split Interchange as transaction sets - suspend interchange on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="40e8a-155">하나 이상의 트랜잭션 집합이 hello 교환 실패 유효성 검사를 하는 경우 X12 hello 디코드 작업 출력 모든 hello 트랜잭션 집합만 해당 교환의 너무`badMessages`합니다.</span><span class="sxs-lookup"><span data-stu-id="40e8a-155">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span>
  * <span data-ttu-id="40e8a-156">교환 유지-오류 발생 시 트랜잭션 집합 일시 중단: Preserve hello 교환 및 프로세스 hello 전체 일괄 처리 교환 합니다.</span><span class="sxs-lookup"><span data-stu-id="40e8a-156">Preserve Interchange - suspend transaction sets on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="40e8a-157">hello X12 디코드 작업 출력 너무 유효성 검사에 실패 하는 해당 트랜잭션 집합만`badMessages`, 남은 트랜잭션 hello 설정 너무 출력`goodMessages`합니다.</span><span class="sxs-lookup"><span data-stu-id="40e8a-157">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="40e8a-158">교환 유지-오류 발생 시 교환 일시 중단: Preserve hello 교환 및 프로세스 hello 전체 일괄 처리 교환 합니다.</span><span class="sxs-lookup"><span data-stu-id="40e8a-158">Preserve Interchange - suspend interchange on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="40e8a-159">하나 이상의 트랜잭션 집합이 hello 교환 실패 유효성 검사를 하는 경우 X12 hello 디코드 작업 출력 모든 hello 트랜잭션 집합만 해당 교환의 너무`badMessages`합니다.</span><span class="sxs-lookup"><span data-stu-id="40e8a-159">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span> 
* <span data-ttu-id="40e8a-160">기술 및/또는 기능 승인을 생성합니다(구성된 경우).</span><span class="sxs-lookup"><span data-stu-id="40e8a-160">Generates a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="40e8a-161">기술 승인은 헤더 유효성 검사의 결과로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="40e8a-161">A Technical Acknowledgment generates as a result of header validation.</span></span> <span data-ttu-id="40e8a-162">hello 기술 승인을 교환 헤더 및 트레일러 hello 주소 수신기의 hello 처리의 hello 상태를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="40e8a-162">hello technical acknowledgment reports hello status of hello processing of an interchange header and trailer by hello address receiver.</span></span>
  * <span data-ttu-id="40e8a-163">기능 승인은 본문 유효성 검사의 결과로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="40e8a-163">A Functional Acknowledgment generates as a result of body validation.</span></span> <span data-ttu-id="40e8a-164">hello 기능 승인은 문서를 받은 hello를 처리 하는 동안 발생 한 각 오류</span><span class="sxs-lookup"><span data-stu-id="40e8a-164">hello functional acknowledgment reports each error encountered while processing hello received document</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="40e8a-165">Hello swagger 보기</span><span class="sxs-lookup"><span data-stu-id="40e8a-165">View hello swagger</span></span>
<span data-ttu-id="40e8a-166">Hello 참조 [세부 정보를 swagger](/connectors/x12/)합니다.</span><span class="sxs-lookup"><span data-stu-id="40e8a-166">See hello [swagger details](/connectors/x12/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="40e8a-167">다음 단계</span><span class="sxs-lookup"><span data-stu-id="40e8a-167">Next steps</span></span>
[<span data-ttu-id="40e8a-168">엔터프라이즈 통합 팩 hello에 대 한 자세한</span><span class="sxs-lookup"><span data-stu-id="40e8a-168">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "엔터프라이즈 통합 팩에 대 한 자세한 정보") 

