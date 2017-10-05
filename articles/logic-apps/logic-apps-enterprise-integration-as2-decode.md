---
title: "AS2 메시지 디코딩 - Azure Logic Apps | Microsoft Docs"
description: "Azure Logic Apps의 엔터프라이즈 통합 팩에 포함된 AS2 디코더를 사용하는 방법"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: a7920b2509fe368c6f7d55e17fe0bf0020c4562c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="decode-as2-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="a4e5d-103">엔터프라이즈 통합 팩이 포함된 Azure Logic Apps에 대한 AS2 메시지 디코딩</span><span class="sxs-lookup"><span data-stu-id="a4e5d-103">Decode AS2 messages for Azure Logic Apps with the Enterprise Integration Pack</span></span> 

<span data-ttu-id="a4e5d-104">메시지를 전송하는 동안 보안 및 안정성을 설정하려면 AS2 메시지 디코딩 커넥터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e5d-104">To establish security and reliability while transmitting messages, use the Decode AS2 message connector.</span></span> <span data-ttu-id="a4e5d-105">이 커넥터에서는 MDN(메시지 처리 알림)을 통해 디지털 서명, 암호 해독 및 승인을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e5d-105">This connector provides digital signing, decryption, and acknowledgements through Message Disposition Notifications (MDN).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="a4e5d-106">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="a4e5d-106">Before you start</span></span>

<span data-ttu-id="a4e5d-107">필요한 항목은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e5d-107">Here's the items you need:</span></span>

* <span data-ttu-id="a4e5d-108">Azure 계정의 경우 [무료 계정](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="a4e5d-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="a4e5d-109">[통합 계정](logic-apps-enterprise-integration-create-integration-account.md)이 이미 정의되고 Azure 구독과 연결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e5d-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="a4e5d-110">AS2 메시지 디코딩 커넥터를 사용하는 통합 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e5d-110">You must have an integration account to use the Decode AS2 message connector.</span></span>
* <span data-ttu-id="a4e5d-111">통합 계정에 이미 정의된 둘 이상의 [파트너](logic-apps-enterprise-integration-partners.md)</span><span class="sxs-lookup"><span data-stu-id="a4e5d-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="a4e5d-112">통합 계정에 이미 정의된 [AS2 규약](logic-apps-enterprise-integration-as2.md)</span><span class="sxs-lookup"><span data-stu-id="a4e5d-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="decode-as2-messages"></a><span data-ttu-id="a4e5d-113">AS2 메시지 디코딩</span><span class="sxs-lookup"><span data-stu-id="a4e5d-113">Decode AS2 messages</span></span>

1. <span data-ttu-id="a4e5d-114">[논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)</span><span class="sxs-lookup"><span data-stu-id="a4e5d-114">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="a4e5d-115">AS2 메시지 디코딩 커넥터에는 트리거가 없으므로 요청 트리거와 마찬가지로 논리 앱을 시작하는 트리거를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e5d-115">The Decode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="a4e5d-116">Logic App Designer에서 트리거를 추가하고 작업을 논리 앱에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e5d-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="a4e5d-117">검색 상자에서 필터에 "AS2"를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e5d-117">In the search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="a4e5d-118">**AS2 – AS2 메시지 디코딩**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e5d-118">Select **AS2 - Decode AS2 message**.</span></span>
   
    !["AS2" 검색](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage1.png)

4. <span data-ttu-id="a4e5d-120">이전에 통합 계정에 연결을 만들지 않은 경우 이제 해당 연결을 만들라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a4e5d-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="a4e5d-121">연결의 이름을 지정하고 연결하려는 통합 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e5d-121">Name your connection, and select the integration account that you want to connect.</span></span>
   
    ![통합 연결 만들기](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage2.png)

    <span data-ttu-id="a4e5d-123">별표가 있는 속성은 필수 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="a4e5d-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="a4e5d-124">속성</span><span class="sxs-lookup"><span data-stu-id="a4e5d-124">Property</span></span> | <span data-ttu-id="a4e5d-125">세부 정보</span><span class="sxs-lookup"><span data-stu-id="a4e5d-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="a4e5d-126">연결 이름 *</span><span class="sxs-lookup"><span data-stu-id="a4e5d-126">Connection Name *</span></span> |<span data-ttu-id="a4e5d-127">연결의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e5d-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="a4e5d-128">통합 계정 *</span><span class="sxs-lookup"><span data-stu-id="a4e5d-128">Integration Account *</span></span> |<span data-ttu-id="a4e5d-129">통합 계정의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e5d-129">Enter a name for your integration account.</span></span> <span data-ttu-id="a4e5d-130">통합 계정 및 논리 앱이 동일한 Azure 위치에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e5d-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="a4e5d-131">완료되면 연결 정보는 이 예제와 유사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e5d-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="a4e5d-132">연결 만들기를 완료하려면 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e5d-132">To finish creating your connection, choose **Create**.</span></span>

    ![통합 연결 세부 정보](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage3.png)

6. <span data-ttu-id="a4e5d-134">이 예제와 같이 연결을 만든 후에 요청 출력에서 **본문** 및 **헤더**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e5d-134">After your connection is created, as shown in this example, select **Body** and **Headers** from the Request outputs.</span></span>
   
    ![통합 연결 생성](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage4.png) 

    <span data-ttu-id="a4e5d-136">예:</span><span class="sxs-lookup"><span data-stu-id="a4e5d-136">For example:</span></span>

    ![요청 출력에서 본문 및 헤더를 선택합니다.](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage5.png) 

## <a name="as2-decoder-details"></a><span data-ttu-id="a4e5d-138">AS2 디코더 세부 정보</span><span class="sxs-lookup"><span data-stu-id="a4e5d-138">AS2 decoder details</span></span>

<span data-ttu-id="a4e5d-139">AS2 디코딩 커넥터는 다음과 같은 태스크를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e5d-139">The Decode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="a4e5d-140">AS2/HTTP 헤더 처리</span><span class="sxs-lookup"><span data-stu-id="a4e5d-140">Processes AS2/HTTP headers</span></span>
* <span data-ttu-id="a4e5d-141">서명 확인(구성된 경우)</span><span class="sxs-lookup"><span data-stu-id="a4e5d-141">Verifies the signature (if configured)</span></span>
* <span data-ttu-id="a4e5d-142">메시지 암호 해독(구성된 경우)</span><span class="sxs-lookup"><span data-stu-id="a4e5d-142">Decrypts the messages (if configured)</span></span>
* <span data-ttu-id="a4e5d-143">메시지 압축 해제(구성된 경우)</span><span class="sxs-lookup"><span data-stu-id="a4e5d-143">Decompresses the message (if configured)</span></span>
* <span data-ttu-id="a4e5d-144">원본 아웃바운드 메시지와 함께 수신된 MDN 조정</span><span class="sxs-lookup"><span data-stu-id="a4e5d-144">Reconciles a received MDN with the original outbound message</span></span>
* <span data-ttu-id="a4e5d-145">부인 방지 데이터베이스에서 레코드 업데이트 및 연결</span><span class="sxs-lookup"><span data-stu-id="a4e5d-145">Updates and correlates records in the non-repudiation database</span></span>
* <span data-ttu-id="a4e5d-146">AS2 상태 보고에 대한 레코드 작성</span><span class="sxs-lookup"><span data-stu-id="a4e5d-146">Writes records for AS2 status reporting</span></span>
* <span data-ttu-id="a4e5d-147">출력 페이로드 콘텐츠는 base64로 인코딩됨</span><span class="sxs-lookup"><span data-stu-id="a4e5d-147">The output payload contents are base64 encoded</span></span>
* <span data-ttu-id="a4e5d-148">MDN이 필요한지 여부 및 MDN을 AS2 규약의 구성에 따라 동기화해야 하는지 또는 비동기화해야 하는지 결정</span><span class="sxs-lookup"><span data-stu-id="a4e5d-148">Determines whether an MDN is required, and whether the MDN should be synchronous or asynchronous based on configuration in AS2 agreement</span></span>
* <span data-ttu-id="a4e5d-149">(규약 구성에 따라)동기 또는 비동기 MDN 생성</span><span class="sxs-lookup"><span data-stu-id="a4e5d-149">Generates a synchronous or asynchronous MDN (based on agreement configurations)</span></span>
* <span data-ttu-id="a4e5d-150">MDN에 대한 상관 관계 토큰과 속성 설정</span><span class="sxs-lookup"><span data-stu-id="a4e5d-150">Sets the correlation tokens and properties on the MDN</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="a4e5d-151">이 샘플 사용해보기</span><span class="sxs-lookup"><span data-stu-id="a4e5d-151">Try this sample</span></span>

<span data-ttu-id="a4e5d-152">완벽하게 작동하는 논리 앱 및 샘플 AS2 시나리오를 배포하려면 [AS2 논리 앱 템플릿 및 시나리오](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a4e5d-152">To try deploying a fully operational logic app and sample AS2 scenario, see the [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="view-the-swagger"></a><span data-ttu-id="a4e5d-153">swagger 보기</span><span class="sxs-lookup"><span data-stu-id="a4e5d-153">View the swagger</span></span>
<span data-ttu-id="a4e5d-154">[swagger 정보](/connectors/as2/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a4e5d-154">See the [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a4e5d-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a4e5d-155">Next steps</span></span>
[<span data-ttu-id="a4e5d-156">엔터프라이즈 통합 팩에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="a4e5d-156">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md) 

