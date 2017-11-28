---
title: "B2B 솔루션 만들기 - Azure Logic Apps | Microsoft Docs"
description: "엔터프라이즈 통합 팩의 B2B 기능을 사용하여 Logic Apps에서 데이터를 수신합니다."
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 20fc3722-6f8b-402f-b391-b84e9df6fcff
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 0625787ddcbc0091e70b111f687e25929720ad15
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="receive-data-in-logic-apps-with-the-b2b-features-in-the-enterprise-integration-pack"></a><span data-ttu-id="93bbf-103">엔터프라이즈 통합 팩의 B2B 기능을 사용하여 Logic Apps에서 데이터 수신</span><span class="sxs-lookup"><span data-stu-id="93bbf-103">Receive data in logic apps with the B2B features in the Enterprise Integration Pack</span></span>

<span data-ttu-id="93bbf-104">파트너와 규약이 있는 통합 계정을 만들면 [엔터프라이즈 통합 팩](logic-apps-enterprise-integration-overview.md)을 사용하여 논리 앱을 위한 B2B 워크플로를 만들 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="93bbf-104">After you create an integration account that has partners and agreements, you are ready to create a business to business (B2B) workflow for your logic app with the [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93bbf-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="93bbf-105">Prerequisites</span></span>

<span data-ttu-id="93bbf-106">AS2 및 X12 작업을 사용하려면 엔터프라이즈 통합 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93bbf-106">To use the AS2 and X12 actions, you must have an Enterprise Integration Account.</span></span> <span data-ttu-id="93bbf-107">[엔터프라이즈 통합 계정을 만드는 방법](../logic-apps/logic-apps-enterprise-integration-accounts.md)에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="93bbf-107">Learn [how to create an Enterprise Integration Account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

## <a name="create-a-logic-app-with-b2b-connectors"></a><span data-ttu-id="93bbf-108">B2B 커넥터를 사용하여 논리 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="93bbf-108">Create a logic app with B2B connectors</span></span>

<span data-ttu-id="93bbf-109">다음 단계에 따라 AS2 및 X12 작업을 사용하여 거래 업체로부터 데이터를 받는 B2B 논리 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="93bbf-109">Follow these steps to create a B2B logic app that uses the AS2 and X12 actions to receive data from a trading partner:</span></span>

1. <span data-ttu-id="93bbf-110">논리 앱을 만든 다음 [앱을 통합 계정에 연결](../logic-apps/logic-apps-enterprise-integration-accounts.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="93bbf-110">Create a logic app, then [link your app to your integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

2. <span data-ttu-id="93bbf-111">**요청 - HTTP 요청을 받은 경우** 트리거를 논리 앱에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="93bbf-111">Add a **Request - When an HTTP request is received** trigger to your logic app.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)

3. <span data-ttu-id="93bbf-112">**AS2 디코딩** 작업을 추가하려면 **작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93bbf-112">To add the **Decode AS2** action, select **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/transform-2.png)

4. <span data-ttu-id="93bbf-113">모든 작업에서 원하는 작업을 필터링하려면 검색 상자에서 **as2** 단어를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="93bbf-113">To filter all actions to the one that you want, enter the word **as2** in the search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-5.png)

5. <span data-ttu-id="93bbf-114">**AS2 - AS2 메시지 디코딩** 작업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93bbf-114">Select the **AS2 - Decode AS2 message** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-6.png)

6. <span data-ttu-id="93bbf-115">입력으로 사용할 **본문**을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="93bbf-115">Add the **Body** that you want to use as input.</span></span> <span data-ttu-id="93bbf-116">이 예제에서는 논리 앱을 트리거하는 HTTP 요청의 본문을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93bbf-116">In this example, select the body of the HTTP request that triggers the logic app.</span></span> <span data-ttu-id="93bbf-117">또는 **헤더** 필드에서 헤더를 입력하는 식을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="93bbf-117">Or enter an expression that inputs the headers in the **HEADERS** field:</span></span>

    <span data-ttu-id="93bbf-118">@triggerOutputs()['헤더']</span><span class="sxs-lookup"><span data-stu-id="93bbf-118">@triggerOutputs()['headers']</span></span>

7. <span data-ttu-id="93bbf-119">HTTP 요청 헤더에서 찾을 수 있는 AS2에 필요한 **헤더**를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="93bbf-119">Add the required **Headers** for AS2, which you can find in the HTTP request headers.</span></span> <span data-ttu-id="93bbf-120">이 예제에서는 논리 앱을 트리거하는 HTTP 요청의 헤더를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93bbf-120">In this example, select the headers of the HTTP request that trigger the logic app.</span></span>

8. <span data-ttu-id="93bbf-121">이제 X12 메시지 디코딩 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="93bbf-121">Now add the Decode X12 message action.</span></span> <span data-ttu-id="93bbf-122">**작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93bbf-122">Select **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-9.png)

9. <span data-ttu-id="93bbf-123">모든 작업에서 원하는 작업을 필터링하려면 검색 상자에서 **x12** 단어를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="93bbf-123">To filter all actions to the one that you want, enter the word **x12** in the search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-10.png)

10. <span data-ttu-id="93bbf-124">**X12 - X12 메시지 디코딩** 작업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93bbf-124">Select the **X12 - Decode X12 message** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-as2message.png)

11. <span data-ttu-id="93bbf-125">이제 이 작업의 입력을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93bbf-125">Now you must specify the input to this action.</span></span> <span data-ttu-id="93bbf-126">이 입력은 이전 AS2 작업의 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="93bbf-126">This input is the output from the previous AS2 action.</span></span>

    <span data-ttu-id="93bbf-127">실제 메시지 내용은 JSON 개체에 있고 base64로 인코딩되어 있으므로 식을 입력으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93bbf-127">The actual message content is in a JSON object and is base64 encoded, so you must specify an expression as the input.</span></span> 
    <span data-ttu-id="93bbf-128">**디코딩할 X12 플랫 파일 메시지** 입력 필드에서 다음 식을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="93bbf-128">Enter the following expression in the **X12 FLAT FILE MESSAGE TO DECODE** input field:</span></span>
    
    <span data-ttu-id="93bbf-129">@base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])</span><span class="sxs-lookup"><span data-stu-id="93bbf-129">@base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])</span></span>

    <span data-ttu-id="93bbf-130">이제 거래 업체로부터 받은 X12 데이터를 디코딩하고 JSON 개체의 항목을 출력하는 단계를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="93bbf-130">Now add steps to decode the X12 data received from the trading partner and output items in a JSON object.</span></span> 
    <span data-ttu-id="93bbf-131">데이터를 받았음을 파트너에게 알리려면 HTTP 응답 작업에서 AS2 MDN(메시지 처리 알림)을 포함하는 응답을 다시 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93bbf-131">To notify the partner that the data was received, you can send back a response containing the AS2 Message Disposition Notification (MDN) in an HTTP Response Action.</span></span>

12. <span data-ttu-id="93bbf-132">**응답** 작업을 추가하려면 **작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93bbf-132">To add the **Response** action, choose **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-14.png)

13. <span data-ttu-id="93bbf-133">모든 작업에서 원하는 작업을 필터링하려면 검색 상자에서 **응답** 단어를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="93bbf-133">To filter all actions to the one that you want, enter the word **response** in the search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-15.png)

14. <span data-ttu-id="93bbf-134">**응답** 작업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93bbf-134">Select the **Response** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-16.png)

15. <span data-ttu-id="93bbf-135">**X12 메시지 디코딩** 작업의 출력에서 MDN에 액세스하려면 다음 식으로 응답 **본문** 필드를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="93bbf-135">To access the MDN from the output of the **Decode X12 message** action, set the response **BODY** field with this expression:</span></span>

    <span data-ttu-id="93bbf-136">@base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])</span><span class="sxs-lookup"><span data-stu-id="93bbf-136">@base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-17.png)  

16. <span data-ttu-id="93bbf-137">작업을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="93bbf-137">Save your work.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/transform-5.png)  

<span data-ttu-id="93bbf-138">이제 B2B 논리 앱 설정이 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="93bbf-138">You are now done setting up your B2B logic app.</span></span> <span data-ttu-id="93bbf-139">실제 응용 프로그램에서는 디코딩된 X12 데이터를 LOB(기간 업무) 앱 또는 데이터 저장소에 저장하려고 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93bbf-139">In a real world application, you might want to store the decoded X12 data in a line-of-business (LOB) app or data store.</span></span> <span data-ttu-id="93bbf-140">자신의 LOB 앱을 연결하고 논리 앱에서 이러한 API를 사용하려면 추가 작업을 추가하거나 사용자 지정 API를 작성하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93bbf-140">To connect your own LOB apps and use these APIs in your logic app, you can add further actions or write custom APIs.</span></span>

## <a name="features-and-use-cases"></a><span data-ttu-id="93bbf-141">기능 및 사용 사례</span><span class="sxs-lookup"><span data-stu-id="93bbf-141">Features and use cases</span></span>

* <span data-ttu-id="93bbf-142">AS2 및 X12 디코딩 및 인코딩 작업을 통해 논리 앱에서 업계 표준 프로토콜을 사용하여 거래 업체 간에 데이터를 교환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93bbf-142">The AS2 and X12 decode and encode actions let you exchange data between trading partners by using industry standard protocols in logic apps.</span></span>
* <span data-ttu-id="93bbf-143">거래 업체와 데이터를 교환하려면 AS2와 X12를 함께 또는 개별로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93bbf-143">To exchange data with trading partners, you can use AS2 and X12 with or without each other.</span></span>
* <span data-ttu-id="93bbf-144">B2B 작업을 사용하면 통합 계정에서 파트너와 규약을 쉽게 만들고 논리 앱에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93bbf-144">The B2B actions help you create partners and agreements easily in your integration account and consume them in a logic app.</span></span>
* <span data-ttu-id="93bbf-145">논리 앱을 다른 작업으로 확장하면 다른 앱과 서비스(예: SalesForce) 간에 데이터를 보내고 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93bbf-145">When you extend your logic app with other actions, you can send and receive data between other apps and services like SalesForce.</span></span>

## <a name="learn-more"></a><span data-ttu-id="93bbf-146">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="93bbf-146">Learn more</span></span>
[<span data-ttu-id="93bbf-147">엔터프라이즈 통합 팩에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="93bbf-147">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md)
