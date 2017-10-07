---
title: "aaaDecode AS2 메시지-Azure 논리 앱 | Microsoft Docs"
description: "Azure 논리 앱에 대 한 toouse hello 엔터프라이즈 통합 팩의에서 AS2 디코더에서 hello 하는 방법"
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
ms.openlocfilehash: 2406e5ec68e0906700fad97d60cb83ef0d106cd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="decode-as2-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="d0be3-103">엔터프라이즈 통합 팩 hello로 Azure 논리 앱에 대 한 AS2 메시지를 디코딩</span><span class="sxs-lookup"><span data-stu-id="d0be3-103">Decode AS2 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span> 

<span data-ttu-id="d0be3-104">tooestablish 보안 및 메시지를 전송 하는 동안 안정성 hello 디코딩할 AS2 메시지 연결선을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0be3-104">tooestablish security and reliability while transmitting messages, use hello Decode AS2 message connector.</span></span> <span data-ttu-id="d0be3-105">이 커넥터에서는 MDN(메시지 처리 알림)을 통해 디지털 서명, 암호 해독 및 승인을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d0be3-105">This connector provides digital signing, decryption, and acknowledgements through Message Disposition Notifications (MDN).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="d0be3-106">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="d0be3-106">Before you start</span></span>

<span data-ttu-id="d0be3-107">다음은 필요한 hello 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="d0be3-107">Here's hello items you need:</span></span>

* <span data-ttu-id="d0be3-108">Azure 계정의 경우 [무료 계정](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="d0be3-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="d0be3-109">[통합 계정](logic-apps-enterprise-integration-create-integration-account.md)이 이미 정의되고 Azure 구독과 연결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d0be3-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="d0be3-110">통합 계정 toouse hello 디코딩할 AS2 메시지 연결선이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0be3-110">You must have an integration account toouse hello Decode AS2 message connector.</span></span>
* <span data-ttu-id="d0be3-111">통합 계정에 이미 정의된 둘 이상의 [파트너](logic-apps-enterprise-integration-partners.md)</span><span class="sxs-lookup"><span data-stu-id="d0be3-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="d0be3-112">통합 계정에 이미 정의된 [AS2 규약](logic-apps-enterprise-integration-as2.md)</span><span class="sxs-lookup"><span data-stu-id="d0be3-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="decode-as2-messages"></a><span data-ttu-id="d0be3-113">AS2 메시지 디코딩</span><span class="sxs-lookup"><span data-stu-id="d0be3-113">Decode AS2 messages</span></span>

1. <span data-ttu-id="d0be3-114">[논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)</span><span class="sxs-lookup"><span data-stu-id="d0be3-114">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="d0be3-115">hello 디코딩할 AS2 메시지 연결선 요청 트리거와 마찬가지로 논리 앱을 시작 하는 트리거를 추가 해야 하므로 트리거, 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d0be3-115">hello Decode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="d0be3-116">Hello 논리가 응용 프로그램 디자이너에서에서 트리거를 추가 하 고 작업 tooyour 논리 앱을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0be3-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="d0be3-117">Hello 검색 상자에 필터에 대 한 "AS2"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0be3-117">In hello search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="d0be3-118">**AS2 – AS2 메시지 디코딩**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d0be3-118">Select **AS2 - Decode AS2 message**.</span></span>
   
    !["AS2" 검색](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage1.png)

4. <span data-ttu-id="d0be3-120">직접 만들지 않은 경우 이전에 모든 연결이 tooyour 통합 계정, 메시지가 toocreate 지금 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0be3-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="d0be3-121">사용자의 연결 이름을 지정 하 고 원하는 tooconnect hello 통합 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0be3-121">Name your connection, and select hello integration account that you want tooconnect.</span></span>
   
    ![통합 연결 만들기](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage2.png)

    <span data-ttu-id="d0be3-123">별표가 있는 속성은 필수 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="d0be3-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="d0be3-124">속성</span><span class="sxs-lookup"><span data-stu-id="d0be3-124">Property</span></span> | <span data-ttu-id="d0be3-125">세부 정보</span><span class="sxs-lookup"><span data-stu-id="d0be3-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="d0be3-126">연결 이름 *</span><span class="sxs-lookup"><span data-stu-id="d0be3-126">Connection Name *</span></span> |<span data-ttu-id="d0be3-127">연결의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d0be3-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="d0be3-128">통합 계정 *</span><span class="sxs-lookup"><span data-stu-id="d0be3-128">Integration Account *</span></span> |<span data-ttu-id="d0be3-129">통합 계정의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d0be3-129">Enter a name for your integration account.</span></span> <span data-ttu-id="d0be3-130">통합 계정 및 논리 앱 hello에 있는지 확인 동일한 Azure 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="d0be3-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="d0be3-131">완료 되 면 연결 정보가 이와 유사한 toothis 예가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0be3-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="d0be3-132">연결을 만드는 toofinish 선택 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="d0be3-132">toofinish creating your connection, choose **Create**.</span></span>

    ![통합 연결 세부 정보](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage3.png)

6. <span data-ttu-id="d0be3-134">연결을 만든 후이 예제에 나와 있는 것 처럼, 선택 **본문** 및 **헤더** hello에서 출력을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0be3-134">After your connection is created, as shown in this example, select **Body** and **Headers** from hello Request outputs.</span></span>
   
    ![통합 연결 생성](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage4.png) 

    <span data-ttu-id="d0be3-136">예:</span><span class="sxs-lookup"><span data-stu-id="d0be3-136">For example:</span></span>

    ![요청 출력에서 본문 및 헤더를 선택합니다.](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage5.png) 

## <a name="as2-decoder-details"></a><span data-ttu-id="d0be3-138">AS2 디코더 세부 정보</span><span class="sxs-lookup"><span data-stu-id="d0be3-138">AS2 decoder details</span></span>

<span data-ttu-id="d0be3-139">hello AS2 디코딩 커넥터 이러한 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d0be3-139">hello Decode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="d0be3-140">AS2/HTTP 헤더 처리</span><span class="sxs-lookup"><span data-stu-id="d0be3-140">Processes AS2/HTTP headers</span></span>
* <span data-ttu-id="d0be3-141">(구성 된 경우) hello 서명을 확인합니다</span><span class="sxs-lookup"><span data-stu-id="d0be3-141">Verifies hello signature (if configured)</span></span>
* <span data-ttu-id="d0be3-142">Hello 메시지 암호를 해독 (구성 된 경우)</span><span class="sxs-lookup"><span data-stu-id="d0be3-142">Decrypts hello messages (if configured)</span></span>
* <span data-ttu-id="d0be3-143">Hello 메시지 압축을 푸는 (구성 된 경우)</span><span class="sxs-lookup"><span data-stu-id="d0be3-143">Decompresses hello message (if configured)</span></span>
* <span data-ttu-id="d0be3-144">Hello 원래 아웃 바운드 메시지와 함께 수신된 된 MDN을 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="d0be3-144">Reconciles a received MDN with hello original outbound message</span></span>
* <span data-ttu-id="d0be3-145">업데이트 되 고 hello 비 거부 데이터베이스에 있는 레코드를 상호 연결</span><span class="sxs-lookup"><span data-stu-id="d0be3-145">Updates and correlates records in hello non-repudiation database</span></span>
* <span data-ttu-id="d0be3-146">AS2 상태 보고에 대한 레코드 작성</span><span class="sxs-lookup"><span data-stu-id="d0be3-146">Writes records for AS2 status reporting</span></span>
* <span data-ttu-id="d0be3-147">hello 출력 페이로드 내용이 base64 인코딩</span><span class="sxs-lookup"><span data-stu-id="d0be3-147">hello output payload contents are base64 encoded</span></span>
* <span data-ttu-id="d0be3-148">하는지를 결정 합니다. MDN이 필요한, 및 여부 hello MDN이 동기 해야 AS2 규약에서 구성에 비동기 따라</span><span class="sxs-lookup"><span data-stu-id="d0be3-148">Determines whether an MDN is required, and whether hello MDN should be synchronous or asynchronous based on configuration in AS2 agreement</span></span>
* <span data-ttu-id="d0be3-149">(규약 구성에 따라)동기 또는 비동기 MDN 생성</span><span class="sxs-lookup"><span data-stu-id="d0be3-149">Generates a synchronous or asynchronous MDN (based on agreement configurations)</span></span>
* <span data-ttu-id="d0be3-150">Hello MDN에 hello 상관 관계 토큰 및 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d0be3-150">Sets hello correlation tokens and properties on hello MDN</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="d0be3-151">이 샘플 사용해보기</span><span class="sxs-lookup"><span data-stu-id="d0be3-151">Try this sample</span></span>

<span data-ttu-id="d0be3-152">완벽 하 게 작동 논리 앱과 샘플 AS2 시나리오의 배포 tootry 참조 hello [AS2 논리 앱 템플릿 및 시나리오](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d0be3-152">tootry deploying a fully operational logic app and sample AS2 scenario, see hello [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="d0be3-153">Hello swagger 보기</span><span class="sxs-lookup"><span data-stu-id="d0be3-153">View hello swagger</span></span>
<span data-ttu-id="d0be3-154">Hello 참조 [세부 정보를 swagger](/connectors/as2/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d0be3-154">See hello [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d0be3-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d0be3-155">Next steps</span></span>
[<span data-ttu-id="d0be3-156">엔터프라이즈 통합 팩 hello에 대 한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="d0be3-156">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md) 

