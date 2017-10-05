---
title: "AS2 메시지 인코딩 - Azure Logic Apps | Microsoft Docs"
description: "Azure Logic Apps의 엔터프라이즈 통합 팩에 포함된 AS2 인코더를 사용하는 방법"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 332fb9e3-576c-4683-bd10-d177a0ebe9a3
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 7889bf9e4e02143b6bb4c797531afa54f8647ce5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="encode-as2-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="d6e98-103">엔터프라이즈 통합 팩이 포함된 Azure Logic Apps에 대한 AS2 메시지 인코딩</span><span class="sxs-lookup"><span data-stu-id="d6e98-103">Encode AS2 messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="d6e98-104">메시지를 전송하는 동안 보안 및 안정성을 설정하려면 AS2 메시지 인코딩 커넥터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e98-104">To establish security and reliability while transmitting messages, use the Encode AS2 message connector.</span></span> <span data-ttu-id="d6e98-105">이 커넥터에서는 MDN(메시지 처리 알림)을 통해 디지털 서명, 암호화 및 승인을 제공하며 부인 방지에 대한 지원도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e98-105">This connector provides digital signing, encryption, and acknowledgements through Message Disposition Notifications (MDN), which also leads to support for Non-Repudiation.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="d6e98-106">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="d6e98-106">Before you start</span></span>

<span data-ttu-id="d6e98-107">필요한 항목은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d6e98-107">Here's the items you need:</span></span>

* <span data-ttu-id="d6e98-108">Azure 계정의 경우 [무료 계정](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="d6e98-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="d6e98-109">[통합 계정](logic-apps-enterprise-integration-create-integration-account.md)이 이미 정의되고 Azure 구독과 연결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d6e98-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="d6e98-110">AS2 메시지 인코딩 커넥터를 사용하는 통합 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e98-110">You must have an integration account to use the Encode AS2 message connector.</span></span>
* <span data-ttu-id="d6e98-111">통합 계정에 이미 정의된 둘 이상의 [파트너](logic-apps-enterprise-integration-partners.md)</span><span class="sxs-lookup"><span data-stu-id="d6e98-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="d6e98-112">통합 계정에 이미 정의된 [AS2 규약](logic-apps-enterprise-integration-as2.md)</span><span class="sxs-lookup"><span data-stu-id="d6e98-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="encode-as2-messages"></a><span data-ttu-id="d6e98-113">AS2 메시지 인코딩</span><span class="sxs-lookup"><span data-stu-id="d6e98-113">Encode AS2 messages</span></span>

1. <span data-ttu-id="d6e98-114">[논리 앱 만들기](logic-apps-create-a-logic-app.md)</span><span class="sxs-lookup"><span data-stu-id="d6e98-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="d6e98-115">AS2 메시지 인코딩 커넥터에는 트리거가 없으므로 요청 트리거와 마찬가지로 논리 앱을 시작하는 트리거를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e98-115">The Encode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="d6e98-116">Logic App Designer에서 트리거를 추가하고 작업을 논리 앱에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e98-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="d6e98-117">검색 상자에서 필터에 "AS2"를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e98-117">In the search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="d6e98-118">**AS2 – AS2 메시지 인코딩**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e98-118">Select **AS2 - Encode AS2 message**.</span></span>
   
    !["AS2" 검색](./media/logic-apps-enterprise-integration-as2-encode/as2decodeimage1.png)

4. <span data-ttu-id="d6e98-120">이전에 통합 계정에 연결을 만들지 않은 경우 이제 해당 연결을 만들라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d6e98-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="d6e98-121">연결의 이름을 지정하고 연결하려는 통합 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e98-121">Name your connection, and select the integration account that you want to connect.</span></span> 
   
    ![통합 계정에 연결 만들기](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage1.png)  

    <span data-ttu-id="d6e98-123">별표가 있는 속성은 필수 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="d6e98-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="d6e98-124">속성</span><span class="sxs-lookup"><span data-stu-id="d6e98-124">Property</span></span> | <span data-ttu-id="d6e98-125">세부 정보</span><span class="sxs-lookup"><span data-stu-id="d6e98-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="d6e98-126">연결 이름 *</span><span class="sxs-lookup"><span data-stu-id="d6e98-126">Connection Name *</span></span> |<span data-ttu-id="d6e98-127">연결의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e98-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="d6e98-128">통합 계정 *</span><span class="sxs-lookup"><span data-stu-id="d6e98-128">Integration Account *</span></span> |<span data-ttu-id="d6e98-129">통합 계정의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e98-129">Enter a name for your integration account.</span></span> <span data-ttu-id="d6e98-130">통합 계정 및 논리 앱이 동일한 Azure 위치에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e98-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="d6e98-131">완료되면 연결 정보는 이 예제와 유사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e98-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="d6e98-132">연결 만들기를 완료하려면 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e98-132">To finish creating your connection, choose **Create**.</span></span>
   
    ![통합 연결 세부 정보](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage2.png)

6. <span data-ttu-id="d6e98-134">이 예제에 표시된 대로 연결을 만든 후에 규약에 구성된 대로 **AS2-From**, **AS2-To identifiers**에 대한 세부 정보를 제공하고 메시지 페이로드인 **본문**에 대한 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e98-134">After your connection is created, as shown in this example, provide details for **AS2-From**, **AS2-To identifiers** as configured in your agreement, and **Body**, which is the message payload.</span></span>
   
    ![필수 필드 제공](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage3.png)

## <a name="as2-encoder-details"></a><span data-ttu-id="d6e98-136">AS2 인코더 세부 정보</span><span class="sxs-lookup"><span data-stu-id="d6e98-136">AS2 encoder details</span></span>

<span data-ttu-id="d6e98-137">AS2 인코딩 커넥터는 다음과 같은 태스크를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d6e98-137">The Encode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="d6e98-138">AS2/HTTP 헤더 적용</span><span class="sxs-lookup"><span data-stu-id="d6e98-138">Applies AS2/HTTP headers</span></span>
* <span data-ttu-id="d6e98-139">나가는 메시지 서명(구성된 경우)</span><span class="sxs-lookup"><span data-stu-id="d6e98-139">Signs outgoing messages (if configured)</span></span>
* <span data-ttu-id="d6e98-140">나가는 메시지 암호화(구성된 경우)</span><span class="sxs-lookup"><span data-stu-id="d6e98-140">Encrypts outgoing messages (if configured)</span></span>
* <span data-ttu-id="d6e98-141">메시지 압축(구성된 경우)</span><span class="sxs-lookup"><span data-stu-id="d6e98-141">Compresses the message (if configured)</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="d6e98-142">이 샘플 사용해보기</span><span class="sxs-lookup"><span data-stu-id="d6e98-142">Try this sample</span></span>

<span data-ttu-id="d6e98-143">완벽하게 작동하는 논리 앱 및 샘플 AS2 시나리오를 배포하려면 [AS2 논리 앱 템플릿 및 시나리오](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6e98-143">To try deploying a fully operational logic app and sample AS2 scenario, see the [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="view-the-swagger"></a><span data-ttu-id="d6e98-144">swagger 보기</span><span class="sxs-lookup"><span data-stu-id="d6e98-144">View the swagger</span></span>
<span data-ttu-id="d6e98-145">[swagger 정보](/connectors/as2/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6e98-145">See the [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d6e98-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d6e98-146">Next steps</span></span>
[<span data-ttu-id="d6e98-147">엔터프라이즈 통합 팩에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="d6e98-147">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "엔터프라이즈 통합 팩에 대해 알아보기") 

