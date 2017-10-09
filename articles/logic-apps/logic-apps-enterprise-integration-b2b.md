---
title: "Azure 논리 앱-aaaCreate B2B 솔루션 | Microsoft Docs"
description: "엔터프라이즈 통합 팩 hello의 hello B2B 기능을 사용 하 여 논리 앱에서 데이터를 수신"
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
ms.openlocfilehash: 8f01318a0415d81c37b216f9b991c060edec2053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="receive-data-in-logic-apps-with-hello-b2b-features-in-hello-enterprise-integration-pack"></a><span data-ttu-id="42411-103">엔터프라이즈 통합 팩 hello의 hello B2B 기능을 사용 하 여 논리 앱에서 데이터를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="42411-103">Receive data in logic apps with hello B2B features in hello Enterprise Integration Pack</span></span>

<span data-ttu-id="42411-104">Hello 사용 하 여 논리 앱에 대 한 준비 toocreate 비즈니스 toobusiness (B2B) 워크플로은 파트너와 규약 있는 통합 계정을 만든 후 [엔터프라이즈 통합 팩](logic-apps-enterprise-integration-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="42411-104">After you create an integration account that has partners and agreements, you are ready toocreate a business toobusiness (B2B) workflow for your logic app with hello [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42411-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="42411-105">Prerequisites</span></span>

<span data-ttu-id="42411-106">AS2 및 X12 toouse hello 동작을 엔터프라이즈 통합 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="42411-106">toouse hello AS2 and X12 actions, you must have an Enterprise Integration Account.</span></span> <span data-ttu-id="42411-107">자세한 내용은 [어떻게 toocreate 엔터프라이즈 통합 계정](../logic-apps/logic-apps-enterprise-integration-accounts.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="42411-107">Learn [how toocreate an Enterprise Integration Account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

## <a name="create-a-logic-app-with-b2b-connectors"></a><span data-ttu-id="42411-108">B2B 커넥터를 사용하여 논리 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="42411-108">Create a logic app with B2B connectors</span></span>

<span data-ttu-id="42411-109">X12 및 AS2 hello를 사용 하 여 이러한 단계는 B2B toocreate 논리 앱에 따라 거래 업체 로부터 작업 tooreceive 데이터:</span><span class="sxs-lookup"><span data-stu-id="42411-109">Follow these steps toocreate a B2B logic app that uses hello AS2 and X12 actions tooreceive data from a trading partner:</span></span>

1. <span data-ttu-id="42411-110">다음 논리 앱을 만드는 [계정을 연결 하려면 앱 tooyour 통합](../logic-apps/logic-apps-enterprise-integration-accounts.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="42411-110">Create a logic app, then [link your app tooyour integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

2. <span data-ttu-id="42411-111">추가 **요청-때 HTTP 요청을 받으면** 트리거 tooyour 논리 앱.</span><span class="sxs-lookup"><span data-stu-id="42411-111">Add a **Request - When an HTTP request is received** trigger tooyour logic app.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)

3. <span data-ttu-id="42411-112">tooadd hello **AS2 디코딩** 동작을 **동작 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="42411-112">tooadd hello **Decode AS2** action, select **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/transform-2.png)

4. <span data-ttu-id="42411-113">toofilter hello 단어를 입력 하는 모든 작업 toohello 원하는 하나 **as2** hello 검색 상자에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42411-113">toofilter all actions toohello one that you want, enter hello word **as2** in hello search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-5.png)

5. <span data-ttu-id="42411-114">선택 hello **AS2-디코딩할 AS2 메시지** 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="42411-114">Select hello **AS2 - Decode AS2 message** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-6.png)

6. <span data-ttu-id="42411-115">Hello 추가 **본문** 입력으로 toouse 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="42411-115">Add hello **Body** that you want toouse as input.</span></span> <span data-ttu-id="42411-116">이 예에서는 트리거 논리 앱 hello는 hello HTTP 요청의 hello 본문을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="42411-116">In this example, select hello body of hello HTTP request that triggers hello logic app.</span></span> <span data-ttu-id="42411-117">Hello에 hello 헤더를 입력 하는 식을 입력 하거나 **헤더** 필드:</span><span class="sxs-lookup"><span data-stu-id="42411-117">Or enter an expression that inputs hello headers in hello **HEADERS** field:</span></span>

    <span data-ttu-id="42411-118">@triggerOutputs()['헤더']</span><span class="sxs-lookup"><span data-stu-id="42411-118">@triggerOutputs()['headers']</span></span>

7. <span data-ttu-id="42411-119">필요한 hello 추가 **헤더** a s 2를 hello HTTP 요청 헤더에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42411-119">Add hello required **Headers** for AS2, which you can find in hello HTTP request headers.</span></span> <span data-ttu-id="42411-120">이 예제에서는 해당 트리거 hello 논리 앱 hello HTTP 요청의 헤더 hello 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="42411-120">In this example, select hello headers of hello HTTP request that trigger hello logic app.</span></span>

8. <span data-ttu-id="42411-121">이제 hello 디코드 X12 메시지 동작을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="42411-121">Now add hello Decode X12 message action.</span></span> <span data-ttu-id="42411-122">**작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="42411-122">Select **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-9.png)

9. <span data-ttu-id="42411-123">toofilter hello 단어를 입력 하는 모든 작업 toohello 원하는 하나 **x12** hello 검색 상자에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42411-123">toofilter all actions toohello one that you want, enter hello word **x12** in hello search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-10.png)

10. <span data-ttu-id="42411-124">선택 hello **X12-디코딩할 X12 메시지** 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="42411-124">Select hello **X12 - Decode X12 message** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-as2message.png)

11. <span data-ttu-id="42411-125">이제 hello 입력된 toothis 동작을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="42411-125">Now you must specify hello input toothis action.</span></span> <span data-ttu-id="42411-126">이 입력은 hello 출력 hello 이전 AS2 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="42411-126">This input is hello output from hello previous AS2 action.</span></span>

    <span data-ttu-id="42411-127">hello 실제 메시지 내용을 JSON 개체 이며 base64 인코딩, 이므로 식을 hello 입력으로 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="42411-127">hello actual message content is in a JSON object and is base64 encoded, so you must specify an expression as hello input.</span></span> 
    <span data-ttu-id="42411-128">다음 식은 hello에 hello 입력 **X12 플랫 파일 메시지 tooDECODE** 입력된 필드:</span><span class="sxs-lookup"><span data-stu-id="42411-128">Enter hello following expression in hello **X12 FLAT FILE MESSAGE tooDECODE** input field:</span></span>
    
    <span data-ttu-id="42411-129">@base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])</span><span class="sxs-lookup"><span data-stu-id="42411-129">@base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])</span></span>

    <span data-ttu-id="42411-130">이제 toodecode hello X12 데이터 hello 거래 업체에서에서 받은 및 JSON 개체의 항목을 출력 하는 단계를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="42411-130">Now add steps toodecode hello X12 data received from hello trading partner and output items in a JSON object.</span></span> 
    <span data-ttu-id="42411-131">데이터 hello toonotify hello 파트너 받았습니다, 그리고 hello AS2 알림 MDN (Message Disposition)에서 HTTP 응답 동작을 포함 하는 응답 클라이언트로 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42411-131">toonotify hello partner that hello data was received, you can send back a response containing hello AS2 Message Disposition Notification (MDN) in an HTTP Response Action.</span></span>

12. <span data-ttu-id="42411-132">tooadd hello **응답** 동작을 선택 **동작 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="42411-132">tooadd hello **Response** action, choose **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-14.png)

13. <span data-ttu-id="42411-133">toofilter hello 단어를 입력 하는 모든 작업 toohello 원하는 하나 **응답** hello 검색 상자에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42411-133">toofilter all actions toohello one that you want, enter hello word **response** in hello search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-15.png)

14. <span data-ttu-id="42411-134">선택 hello **응답** 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="42411-134">Select hello **Response** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-16.png)

15. <span data-ttu-id="42411-135">tooaccess hello의 hello 출력에서 MDN을 hello **디코드 X12 메시지** 작업, 집합 hello 응답 **본문** 이 식을 사용 하 여 필드:</span><span class="sxs-lookup"><span data-stu-id="42411-135">tooaccess hello MDN from hello output of hello **Decode X12 message** action, set hello response **BODY** field with this expression:</span></span>

    <span data-ttu-id="42411-136">@base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])</span><span class="sxs-lookup"><span data-stu-id="42411-136">@base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-17.png)  

16. <span data-ttu-id="42411-137">작업을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="42411-137">Save your work.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/transform-5.png)  

<span data-ttu-id="42411-138">이제 B2B 논리 앱 설정이 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="42411-138">You are now done setting up your B2B logic app.</span></span> <span data-ttu-id="42411-139">실제 응용 프로그램에서 할 수 있습니다 toostore hello 디코딩된 X12 기간 업무 (LOB) 응용 프로그램 또는 데이터 저장소의 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="42411-139">In a real world application, you might want toostore hello decoded X12 data in a line-of-business (LOB) app or data store.</span></span> <span data-ttu-id="42411-140">tooconnect LOB 앱 및 논리 앱에서 이러한 Api를 사용 하 여, 사용자 지정 Api를 작성 하거나 작업을 더 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42411-140">tooconnect your own LOB apps and use these APIs in your logic app, you can add further actions or write custom APIs.</span></span>

## <a name="features-and-use-cases"></a><span data-ttu-id="42411-141">기능 및 사용 사례</span><span class="sxs-lookup"><span data-stu-id="42411-141">Features and use cases</span></span>

* <span data-ttu-id="42411-142">hello AS2 및 X12 디코딩 및 동작을 인코딩하 let 논리 앱의 산업 표준 프로토콜을 사용 하 여 거래 파트너 간에 데이터를 교환 합니다.</span><span class="sxs-lookup"><span data-stu-id="42411-142">hello AS2 and X12 decode and encode actions let you exchange data between trading partners by using industry standard protocols in logic apps.</span></span>
* <span data-ttu-id="42411-143">거래 업체와 tooexchange 데이터를 사용할 수 있습니다 AS2 및 X12 상관 없이 서로.</span><span class="sxs-lookup"><span data-stu-id="42411-143">tooexchange data with trading partners, you can use AS2 and X12 with or without each other.</span></span>
* <span data-ttu-id="42411-144">hello B2B 작업을 사용 하 여 통합 계정에서 파트너와 규약을 쉽게 만들기 및 논리 앱에서을 사용할 수 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42411-144">hello B2B actions help you create partners and agreements easily in your integration account and consume them in a logic app.</span></span>
* <span data-ttu-id="42411-145">논리 앱을 다른 작업으로 확장하면 다른 앱과 서비스(예: SalesForce) 간에 데이터를 보내고 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42411-145">When you extend your logic app with other actions, you can send and receive data between other apps and services like SalesForce.</span></span>

## <a name="learn-more"></a><span data-ttu-id="42411-146">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="42411-146">Learn more</span></span>
[<span data-ttu-id="42411-147">엔터프라이즈 통합 팩 hello에 대 한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="42411-147">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md)
