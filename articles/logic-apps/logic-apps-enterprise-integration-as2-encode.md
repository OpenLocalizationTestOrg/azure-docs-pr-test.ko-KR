---
title: "aaaEncode AS2 메시지-Azure 논리 앱 | Microsoft Docs"
description: "Azure 논리 앱에 대 한 toouse hello 엔터프라이즈 통합 팩에서에서 AS2 인코더 hello 하는 방법"
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
ms.openlocfilehash: 2b372c416512ffa9ea5dc50ce0f767bfd8aefbc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="encode-as2-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="2da21-103">엔터프라이즈 통합 팩 hello로 Azure 논리 앱에 대 한 AS2 메시지를 인코딩</span><span class="sxs-lookup"><span data-stu-id="2da21-103">Encode AS2 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="2da21-104">tooestablish 보안 및 메시지를 전송 하는 동안 안정성 hello AS2 인코딩 메시지 연결선을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2da21-104">tooestablish security and reliability while transmitting messages, use hello Encode AS2 message connector.</span></span> <span data-ttu-id="2da21-105">이 커넥터는 디지털 서명, 암호화 및 승인을 통해 알림 MDN (Message Disposition), 또한 toosupport 거부 없음에 대 한 본질적를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2da21-105">This connector provides digital signing, encryption, and acknowledgements through Message Disposition Notifications (MDN), which also leads toosupport for Non-Repudiation.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="2da21-106">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="2da21-106">Before you start</span></span>

<span data-ttu-id="2da21-107">다음은 필요한 hello 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="2da21-107">Here's hello items you need:</span></span>

* <span data-ttu-id="2da21-108">Azure 계정의 경우 [무료 계정](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="2da21-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="2da21-109">[통합 계정](logic-apps-enterprise-integration-create-integration-account.md)이 이미 정의되고 Azure 구독과 연결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2da21-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="2da21-110">통합 계정 toouse hello AS2 인코딩 메시지 연결선이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2da21-110">You must have an integration account toouse hello Encode AS2 message connector.</span></span>
* <span data-ttu-id="2da21-111">통합 계정에 이미 정의된 둘 이상의 [파트너](logic-apps-enterprise-integration-partners.md)</span><span class="sxs-lookup"><span data-stu-id="2da21-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="2da21-112">통합 계정에 이미 정의된 [AS2 규약](logic-apps-enterprise-integration-as2.md)</span><span class="sxs-lookup"><span data-stu-id="2da21-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="encode-as2-messages"></a><span data-ttu-id="2da21-113">AS2 메시지 인코딩</span><span class="sxs-lookup"><span data-stu-id="2da21-113">Encode AS2 messages</span></span>

1. <span data-ttu-id="2da21-114">[논리 앱 만들기](logic-apps-create-a-logic-app.md)</span><span class="sxs-lookup"><span data-stu-id="2da21-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="2da21-115">hello AS2 인코딩 메시지 연결선은 트리거, 갖고 있지 않으므로 요청 트리거와 마찬가지로 논리 앱을 시작 하는 트리거를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2da21-115">hello Encode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="2da21-116">Hello 논리가 응용 프로그램 디자이너에서에서 트리거를 추가 하 고 작업 tooyour 논리 앱을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2da21-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="2da21-117">Hello 검색 상자에 필터에 대 한 "AS2"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2da21-117">In hello search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="2da21-118">**AS2 – AS2 메시지 인코딩**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2da21-118">Select **AS2 - Encode AS2 message**.</span></span>
   
    !["AS2" 검색](./media/logic-apps-enterprise-integration-as2-encode/as2decodeimage1.png)

4. <span data-ttu-id="2da21-120">직접 만들지 않은 경우 이전에 모든 연결이 tooyour 통합 계정, 메시지가 toocreate 지금 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="2da21-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="2da21-121">사용자의 연결 이름을 지정 하 고 원하는 tooconnect hello 통합 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2da21-121">Name your connection, and select hello integration account that you want tooconnect.</span></span> 
   
    ![연결 toointegration 계정 만들기](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage1.png)  

    <span data-ttu-id="2da21-123">별표가 있는 속성은 필수 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="2da21-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="2da21-124">속성</span><span class="sxs-lookup"><span data-stu-id="2da21-124">Property</span></span> | <span data-ttu-id="2da21-125">세부 정보</span><span class="sxs-lookup"><span data-stu-id="2da21-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="2da21-126">연결 이름 *</span><span class="sxs-lookup"><span data-stu-id="2da21-126">Connection Name *</span></span> |<span data-ttu-id="2da21-127">연결의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2da21-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="2da21-128">통합 계정 *</span><span class="sxs-lookup"><span data-stu-id="2da21-128">Integration Account *</span></span> |<span data-ttu-id="2da21-129">통합 계정의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2da21-129">Enter a name for your integration account.</span></span> <span data-ttu-id="2da21-130">통합 계정 및 논리 앱 hello에 있는지 확인 동일한 Azure 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="2da21-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="2da21-131">완료 되 면 연결 정보가 이와 유사한 toothis 예가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2da21-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="2da21-132">연결을 만드는 toofinish 선택 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="2da21-132">toofinish creating your connection, choose **Create**.</span></span>
   
    ![통합 연결 세부 정보](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage2.png)

6. <span data-ttu-id="2da21-134">연결을 만든 후이 예제에 나와 있는 것 처럼에 대 한 세부 정보를 제공 **AS2-에서**, **AS2 tooidentifiers** 프로그램 계약에 구성 된 대로 및 **본문**, 즉 hello 메시지 페이로드입니다.</span><span class="sxs-lookup"><span data-stu-id="2da21-134">After your connection is created, as shown in this example, provide details for **AS2-From**, **AS2-tooidentifiers** as configured in your agreement, and **Body**, which is hello message payload.</span></span>
   
    ![필수 필드 제공](./media/logic-apps-enterprise-integration-as2-encode/as2encodeimage3.png)

## <a name="as2-encoder-details"></a><span data-ttu-id="2da21-136">AS2 인코더 세부 정보</span><span class="sxs-lookup"><span data-stu-id="2da21-136">AS2 encoder details</span></span>

<span data-ttu-id="2da21-137">hello AS2 인코딩 커넥터 이러한 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2da21-137">hello Encode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="2da21-138">AS2/HTTP 헤더 적용</span><span class="sxs-lookup"><span data-stu-id="2da21-138">Applies AS2/HTTP headers</span></span>
* <span data-ttu-id="2da21-139">나가는 메시지 서명(구성된 경우)</span><span class="sxs-lookup"><span data-stu-id="2da21-139">Signs outgoing messages (if configured)</span></span>
* <span data-ttu-id="2da21-140">나가는 메시지 암호화(구성된 경우)</span><span class="sxs-lookup"><span data-stu-id="2da21-140">Encrypts outgoing messages (if configured)</span></span>
* <span data-ttu-id="2da21-141">(구성 된 경우) hello 메시지 압축</span><span class="sxs-lookup"><span data-stu-id="2da21-141">Compresses hello message (if configured)</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="2da21-142">이 샘플 사용해보기</span><span class="sxs-lookup"><span data-stu-id="2da21-142">Try this sample</span></span>

<span data-ttu-id="2da21-143">완벽 하 게 작동 논리 앱과 샘플 AS2 시나리오의 배포 tootry 참조 hello [AS2 논리 앱 템플릿 및 시나리오](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2da21-143">tootry deploying a fully operational logic app and sample AS2 scenario, see hello [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="2da21-144">Hello swagger 보기</span><span class="sxs-lookup"><span data-stu-id="2da21-144">View hello swagger</span></span>
<span data-ttu-id="2da21-145">Hello 참조 [세부 정보를 swagger](/connectors/as2/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2da21-145">See hello [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="2da21-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2da21-146">Next steps</span></span>
[<span data-ttu-id="2da21-147">엔터프라이즈 통합 팩 hello에 대 한 자세한</span><span class="sxs-lookup"><span data-stu-id="2da21-147">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "엔터프라이즈 통합 팩에 대 한 자세한 정보") 

