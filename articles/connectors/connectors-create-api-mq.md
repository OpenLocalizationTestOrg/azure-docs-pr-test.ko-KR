---
title: "aaaLearn 어떻게 toouse hello Azure 논리 앱에 대 한 MQ 커넥터 | Microsoft Docs"
description: "프로그램 논리 앱 워크플로 toobrowse에서 tooan 온-프레미스 또는 Azure MQ 서버를 연결, 수신, 및 메시지 tooWebSphere MQ 보내기"
services: logic-apps
author: valthom
manager: anneta
documentationcenter: 
editor: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 06/01/2017
ms.author: valthom; ladocs
ms.openlocfilehash: 8b36d53b457ced1a7461c229aecfcf8e4ae668a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-ibm-mq-server-from-logic-apps-using-hello-mq-connector"></a><span data-ttu-id="aa6df-103">Hello MQ 커넥터를 사용 하 여 논리 앱에서 tooan IBM MQ 서버 연결</span><span class="sxs-lookup"><span data-stu-id="aa6df-103">Connect tooan IBM MQ server from logic apps using hello MQ connector</span></span> 

<span data-ttu-id="aa6df-104">MQ용 Microsoft 커넥터는 MQ 서버 온-프레미스 또는 Azure에 저장된 메시지를 전송하고 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-104">Microsoft Connector for MQ sends and retrieves messages stored in an MQ Server on-premises, or in Azure.</span></span> <span data-ttu-id="aa6df-105">이 커넥터는 TCP/IP 네트워크를 통해 원격 IBM MQ 서버와 통신하는 Microsoft MQ 클라이언트를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-105">This connector includes a Microsoft MQ client that communicates with a remote IBM MQ server across a TCP/IP network.</span></span> <span data-ttu-id="aa6df-106">이 문서는 시작 가이드 toouse hello MQ 커넥터입니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-106">This document is a starter guide toouse hello MQ connector.</span></span> <span data-ttu-id="aa6df-107">큐에서 단일 메시지를 검색 하 여 시작 하 고 다른 작업을 hello 보는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-107">We recommended you begin by browsing a single message on a queue, and then trying hello other actions.</span></span>    

<span data-ttu-id="aa6df-108">hello MQ 커넥터 hello 다음 작업을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-108">hello MQ connector includes hello following actions.</span></span> <span data-ttu-id="aa6df-109">트리거는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-109">There are no triggers.</span></span>

-   <span data-ttu-id="aa6df-110">Hello IBM MQ Server에서에서 hello 메시지를 삭제 하지 않고 단일 메시지 찾아보기</span><span class="sxs-lookup"><span data-stu-id="aa6df-110">Browse a single message without deleting hello message from hello IBM MQ Server</span></span>
-   <span data-ttu-id="aa6df-111">Hello IBM MQ Server에서에서 hello 메시지를 삭제 하지 않고 일괄 처리 메시지 찾아보기</span><span class="sxs-lookup"><span data-stu-id="aa6df-111">Browse a batch of messages without deleting hello messages from hello IBM MQ Server</span></span>
-   <span data-ttu-id="aa6df-112">단일 메시지를 수신 하 고 hello IBM MQ Server에서에서 hello 메시지를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-112">Receive a single message and delete hello message from hello IBM MQ Server</span></span>
-   <span data-ttu-id="aa6df-113">일괄 처리 메시지를 수신 하 고 hello IBM MQ Server에서에서 hello 메시지 삭제</span><span class="sxs-lookup"><span data-stu-id="aa6df-113">Receive a batch of messages and delete hello messages from hello IBM MQ Server</span></span>
-   <span data-ttu-id="aa6df-114">단일 메시지 toohello IBM MQ Server 보내기</span><span class="sxs-lookup"><span data-stu-id="aa6df-114">Send a single message toohello IBM MQ Server</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="aa6df-115">필수 조건</span><span class="sxs-lookup"><span data-stu-id="aa6df-115">Prerequisites</span></span>

* <span data-ttu-id="aa6df-116">온-프레미스 MQ 서버를 사용 하는 경우 [hello 온-프레미스 데이터 게이트웨이 설치](../logic-apps/logic-apps-gateway-install.md) 네트워크 내의 서버에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-116">If using an on-premises MQ server, [install hello on-premises data gateway](../logic-apps/logic-apps-gateway-install.md) on a server within your network.</span></span> <span data-ttu-id="aa6df-117">MQ 서버 hello 공개적으로 Azure 내에서 제공 하거나, 사용할 수 있으면 다음 hello 데이터 게이트웨이 사용 되지 않거나 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-117">If hello MQ Server is publicly available, or available within Azure, then hello data gateway is not used or required.</span></span>

    > [!NOTE]
    > <span data-ttu-id="aa6df-118">hello 서버에 온-프레미스 데이터 게이트웨이가 설치 된 hello도 있어야.Net Framework 4.6이 MQ 커넥터 toofunction hello에 대 한 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-118">hello server where hello On-Premises Data Gateway is installed must also have .Net Framework 4.6 installed for hello MQ Connector toofunction.</span></span>

* <span data-ttu-id="aa6df-119">Hello hello 온-프레미스 데이터 게이트웨이-에 대 한 Azure 리소스 만들기 [hello 데이터 게이트웨이 연결을 설정](../logic-apps/logic-apps-gateway-connection.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-119">Create hello Azure resource for hello on-premises data gateway - [Set up hello data gateway connection](../logic-apps/logic-apps-gateway-connection.md).</span></span>

* <span data-ttu-id="aa6df-120">공식적으로 지원되는 IBM WebSphere MQ 버전:</span><span class="sxs-lookup"><span data-stu-id="aa6df-120">Officially supported IBM WebSphere MQ versions:</span></span>
   * <span data-ttu-id="aa6df-121">MQ 7.5</span><span class="sxs-lookup"><span data-stu-id="aa6df-121">MQ 7.5</span></span>
   * <span data-ttu-id="aa6df-122">MQ 8.0</span><span class="sxs-lookup"><span data-stu-id="aa6df-122">MQ 8.0</span></span>

## <a name="create-a-logic-app"></a><span data-ttu-id="aa6df-123">논리 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="aa6df-123">Create a logic app</span></span>

1. <span data-ttu-id="aa6df-124">Hello에 **Azure 시작 보드**선택,  **+**  (더하기 기호) **웹 + 모바일**, 차례로 **논리 앱**합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-124">In hello **Azure start board**, select **+** (plus sign), **Web + Mobile**, and then **Logic App**.</span></span> 
2. <span data-ttu-id="aa6df-125">Hello 입력 **이름**, MQTestApp, 같은 **구독**, **리소스 그룹**, 및 **위치** (여기서 hello hello 위치 사용 온-프레미스 데이터 게이트웨이 연결 구성 됨).</span><span class="sxs-lookup"><span data-stu-id="aa6df-125">Enter hello **Name**, such as MQTestApp, **Subscription**, **Resource group**, and **Location** (use hello location where hello on-premises Data Gateway connection is configured).</span></span> <span data-ttu-id="aa6df-126">선택 **Pin toodashboard**를 선택 하 고 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-126">Select **Pin toodashboard**, and select **Create**.</span></span>  
<span data-ttu-id="aa6df-127">![논리 앱 만들기](media/connectors-create-api-mq/Create_Logic_App.png)</span><span class="sxs-lookup"><span data-stu-id="aa6df-127">![Create Logic App](media/connectors-create-api-mq/Create_Logic_App.png)</span></span>

## <a name="add-a-trigger"></a><span data-ttu-id="aa6df-128">트리거 추가</span><span class="sxs-lookup"><span data-stu-id="aa6df-128">Add a trigger</span></span>

> [!NOTE]
> <span data-ttu-id="aa6df-129">hello MQ 커넥터는 모든 트리거는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-129">hello MQ Connector does not have any triggers.</span></span> <span data-ttu-id="aa6df-130">따라서 사용 하 여 다른 트리거 toostart hello와 같은 논리 앱 **되풀이** 트리거.</span><span class="sxs-lookup"><span data-stu-id="aa6df-130">So, use another trigger toostart your logic app, such as hello **Recurrence** trigger.</span></span> 

1. <span data-ttu-id="aa6df-131">hello **논리 앱 디자이너** 열립니다, **되풀이** 일반적인 트리거의 hello 목록의 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-131">hello **Logic Apps Designer** opens, select **Recurrence** in hello list of common triggers.</span></span>
2. <span data-ttu-id="aa6df-132">선택 **편집** hello 되풀이 트리거 내에서.</span><span class="sxs-lookup"><span data-stu-id="aa6df-132">Select **Edit** within hello Recurrence Trigger.</span></span> 
3. <span data-ttu-id="aa6df-133">집합 hello **주파수** 너무**일**, 및 집합 hello **간격** 너무**7**합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-133">Set hello **Frequency** too**Day**, and set hello **Interval** too**7**.</span></span> 

## <a name="browse-a-single-message"></a><span data-ttu-id="aa6df-134">단일 메시지 찾아보기</span><span class="sxs-lookup"><span data-stu-id="aa6df-134">Browse a single message</span></span>
1. <span data-ttu-id="aa6df-135">**+ 새 단계**를 선택한 다음 **작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-135">Select **+ New step**, and select **Add an action**.</span></span>
2. <span data-ttu-id="aa6df-136">Hello 검색 상자에 입력 `mq`를 선택한 후 **MQ-찾아보기 메시지**합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-136">In hello search box, type `mq`, and then select **MQ - Browse message**.</span></span>  
<span data-ttu-id="aa6df-137">![메시지 찾아보기](media/connectors-create-api-mq/Browse_message.png)</span><span class="sxs-lookup"><span data-stu-id="aa6df-137">![Browse message](media/connectors-create-api-mq/Browse_message.png)</span></span>

3. <span data-ttu-id="aa6df-138">기존 MQ 연결 없으면 다음 hello 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-138">If there isn't an existing MQ connection, then create hello connection:</span></span>  

    1. <span data-ttu-id="aa6df-139">선택 **온-프레미스 데이터 게이트웨이 통해 연결**, 한 MQ 서버의 hello 속성을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-139">Select **Connect via on-premises data gateway**, and enter hello properties of your MQ server.</span></span>  
    <span data-ttu-id="aa6df-140">에 대 한 **서버**, hello MQ 서버 이름을 입력 하거나 뒤에 콜론과 hello 포트 번호로 hello IP 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-140">For **Server**, you can enter hello MQ server name, or enter hello IP address followed by a colon and hello port number.</span></span> 
    2. <span data-ttu-id="aa6df-141">hello **게이트웨이** 구성 된 모든 기존 게이트웨이 연결을 나열 하는 드롭다운입니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-141">hello **gateway** dropdown lists any existing gateway connections that have been configured.</span></span> <span data-ttu-id="aa6df-142">게이트웨이를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-142">Select your gateway.</span></span>
    3. <span data-ttu-id="aa6df-143">작업을 완료하면 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-143">Select **Create** when finished.</span></span> <span data-ttu-id="aa6df-144">연결에는 비슷한 toohello 다음 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-144">Your connection looks similar toohello following:</span></span>   
    <span data-ttu-id="aa6df-145">![연결 속성](media/connectors-create-api-mq/Connection_Properties.png)</span><span class="sxs-lookup"><span data-stu-id="aa6df-145">![Connection Properties](media/connectors-create-api-mq/Connection_Properties.png)</span></span>

4. <span data-ttu-id="aa6df-146">Hello 작업 속성에서 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-146">In hello action properties, you can:</span></span>  

    * <span data-ttu-id="aa6df-147">사용 하 여 hello **큐** 속성 tooaccess hello 연결에 정의 된 것 보다 다른 큐 이름</span><span class="sxs-lookup"><span data-stu-id="aa6df-147">Use hello **Queue** property tooaccess a different queue name than what is defined in hello connection</span></span>
    * <span data-ttu-id="aa6df-148">사용 하 여 hello **MessageId**, **CorrelationId**, **GroupId**, 및 기타 속성 toobrowse hello 다른 MQ 메시지 속성에 따라 메시지에 대 한</span><span class="sxs-lookup"><span data-stu-id="aa6df-148">Use hello **MessageId**, **CorrelationId**, **GroupId**, and other properties toobrowse for a message based on hello different MQ message properties</span></span>
    * <span data-ttu-id="aa6df-149">설정 **IncludeInfo** 너무**True** hello 출력의 tooinclude 추가 메시지 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-149">Set **IncludeInfo** too**True** tooinclude additional message information in hello output.</span></span> <span data-ttu-id="aa6df-150">너무 설정 또는**False** toonot hello 출력에 추가 메시지 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-150">Or, set it too**False** toonot include additional message information in hello output.</span></span>
    * <span data-ttu-id="aa6df-151">입력 한 **제한 시간** 값 toodetermine 비어 있는 큐에서 메시지 tooarrive에 대 한 시간 toowait 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-151">Enter a **Timeout** value toodetermine how long toowait for a message tooarrive in an empty queue.</span></span> <span data-ttu-id="aa6df-152">아무 것도 입력 되지 hello 큐의 첫 번째 메시지 hello이 검색 되 고 메시지 tooappear 기다리는 데 걸린 시간이 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-152">If nothing is entered, hello first message in hello queue is retrieved, and there is no time spent waiting for a message tooappear.</span></span>  
    <span data-ttu-id="aa6df-153">![메시지 속성 찾아보기](media/connectors-create-api-mq/Browse_message_Props.png)</span><span class="sxs-lookup"><span data-stu-id="aa6df-153">![Browse Message Properties](media/connectors-create-api-mq/Browse_message_Props.png)</span></span>

5. <span data-ttu-id="aa6df-154">변경 내용을 **저장**한 다음 논리 앱을 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-154">**Save** your changes, and then **Run** your logic app:</span></span>  
<span data-ttu-id="aa6df-155">![저장 및 실행](media/connectors-create-api-mq/Save_Run.png)</span><span class="sxs-lookup"><span data-stu-id="aa6df-155">![Save and run](media/connectors-create-api-mq/Save_Run.png)</span></span>

6. <span data-ttu-id="aa6df-156">몇 초 후 실행 하는 hello hello 단계 표시 되어 있으며, hello 출력 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-156">After a few seconds, hello steps of hello run are shown, and you can look at hello output.</span></span> <span data-ttu-id="aa6df-157">각 단계의 hello 녹색 확인 표시가 toosee 세부 정보를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-157">Select hello green checkmark toosee details of each step.</span></span> <span data-ttu-id="aa6df-158">선택 **원시 출력 참조** toosee hello에 대 한 추가 세부 정보 데이터를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-158">Select **See raw outputs** toosee additional details on hello output data.</span></span>  
<span data-ttu-id="aa6df-159">![메시지 출력 찾아보기](media/connectors-create-api-mq/Browse_message_output.png)</span><span class="sxs-lookup"><span data-stu-id="aa6df-159">![Browse message output](media/connectors-create-api-mq/Browse_message_output.png)</span></span>  

    <span data-ttu-id="aa6df-160">원시 출력:</span><span class="sxs-lookup"><span data-stu-id="aa6df-160">Raw output:</span></span>  
    ![메시지 원시 출력 찾아보기](media/connectors-create-api-mq/Browse_message_raw_output.png)

7. <span data-ttu-id="aa6df-162">Hello 때 **IncludeInfo** tootrue 옵션 설정, hello 출력 뒤에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-162">When hello **IncludeInfo** option is set tootrue, hello following output is displayed:</span></span>  
<span data-ttu-id="aa6df-163">![메시지 포함 정보 찾아보기](media/connectors-create-api-mq/Browse_message_Include_Info.png)</span><span class="sxs-lookup"><span data-stu-id="aa6df-163">![Browse message include info](media/connectors-create-api-mq/Browse_message_Include_Info.png)</span></span>

## <a name="browse-multiple-messages"></a><span data-ttu-id="aa6df-164">여러 메시지 찾아보기</span><span class="sxs-lookup"><span data-stu-id="aa6df-164">Browse multiple messages</span></span>
<span data-ttu-id="aa6df-165">hello **메시지 찾아보기** 액션에 포함 된 **BatchSize** 옵션 tooindicate hello 큐에서 메시지 반환 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-165">hello **Browse messages** action includes a **BatchSize** option tooindicate how many messages should be returned from hello queue.</span></span>  <span data-ttu-id="aa6df-166">**BatchSize**에 항목이 없는 경우 모든 메시지가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-166">If **BatchSize** has no entry, all messages are returned.</span></span> <span data-ttu-id="aa6df-167">hello 출력은 메시지의 배열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-167">hello returned output is an array of messages.</span></span>

1. <span data-ttu-id="aa6df-168">Hello를 추가할 때 **메시지 찾아보기** hello 첫 번째 연결을 구성 된 작업은 기본적으로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-168">When adding hello **Browse messages** action, hello first connection that is configured is selected by default.</span></span> <span data-ttu-id="aa6df-169">선택 **연결 변경** toocreate 새 연결 하거나 다른 연결을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-169">Select **Change connection** toocreate a new connection, or select a different connection.</span></span>

2. <span data-ttu-id="aa6df-170">찾아보기의 hello 출력 메시지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-170">hello output of Browse messages shows:</span></span>  
![메시지 출력 찾아보기](media/connectors-create-api-mq/Browse_messages_output.png)

## <a name="receive-a-single-message"></a><span data-ttu-id="aa6df-172">단일 메시지 수신</span><span class="sxs-lookup"><span data-stu-id="aa6df-172">Receive a single message</span></span>
<span data-ttu-id="aa6df-173">hello **메시지 받기** 동작 hello로 동일한 입력 및 출력을 hello에 **찾아보기 메시지** 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-173">hello **Receive message** action has hello same inputs and outputs as hello **Browse message** action.</span></span> <span data-ttu-id="aa6df-174">사용 하는 경우 **메시지 받기**, hello 메시지 hello 큐에서 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-174">When using **Receive message**, hello message is deleted from hello queue.</span></span>

## <a name="receive-multiple-messages"></a><span data-ttu-id="aa6df-175">여러 메시지 수신</span><span class="sxs-lookup"><span data-stu-id="aa6df-175">Receive multiple messages</span></span>
<span data-ttu-id="aa6df-176">hello **메시지를 받을** 동작 hello로 동일한 입력 및 출력을 hello에 **메시지 찾아보기** 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-176">hello **Receive messages** action has hello same inputs and outputs as hello **Browse messages** action.</span></span> <span data-ttu-id="aa6df-177">사용 하는 경우 **메시지를 받을**, hello 메시지 hello 큐에서 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-177">When using **Receive messages**, hello messages are deleted from hello queue.</span></span>

<span data-ttu-id="aa6df-178">메시지가 없는 hello 큐에는 찾아보기 또는 receive를 수행 하는 경우, 다음 출력 hello로 hello 단계가 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-178">If there are no messages in hello queue when doing a browse or a receive, hello step fails with hello following output:</span></span>  
![MQ 메시지 오류 없음](media/connectors-create-api-mq/MQ_No_Msg_Error.png)

## <a name="send-a-message"></a><span data-ttu-id="aa6df-180">메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="aa6df-180">Send a message</span></span>
1. <span data-ttu-id="aa6df-181">Hello를 추가할 때 **메시지 보내기** hello 첫 번째 연결을 구성 된 작업은 기본적으로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-181">When adding hello **Send message** action, hello first connection that is configured is selected by default.</span></span> <span data-ttu-id="aa6df-182">선택 **연결 변경** toocreate 새 연결 하거나 다른 연결을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-182">Select **Change connection** toocreate a new connection, or select a different connection.</span></span> <span data-ttu-id="aa6df-183">유효한 hello **메시지 유형** 는 **데이터 그램**, **회신**, 또는 **요청**합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-183">hello valid **Message Types** are **Datagram**, **Reply**, or **Request**.</span></span>  
<span data-ttu-id="aa6df-184">![메시지 속성 전송](media/connectors-create-api-mq/Send_Msg_Props.png)</span><span class="sxs-lookup"><span data-stu-id="aa6df-184">![Send Msg Props](media/connectors-create-api-mq/Send_Msg_Props.png)</span></span>

2. <span data-ttu-id="aa6df-185">hello 메시지 보내기의 출력 hello 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-185">hello output of Send message looks like hello following:</span></span>  
![메시지 출력 전송](media/connectors-create-api-mq/Send_Msg_Output.png)

## <a name="connector-specific-details"></a><span data-ttu-id="aa6df-187">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="aa6df-187">Connector-specific details</span></span>

<span data-ttu-id="aa6df-188">모든 트리거 및 hello swagger에 정의 된 작업을 확인 하 고 hello에 어떠한 제한도 볼 [connector 세부 정보](/connectors/mq/)합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-188">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/mq/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa6df-189">다음 단계</span><span class="sxs-lookup"><span data-stu-id="aa6df-189">Next steps</span></span>
<span data-ttu-id="aa6df-190">[논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)</span><span class="sxs-lookup"><span data-stu-id="aa6df-190">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="aa6df-191">탐색에서 논리 앱에서 사용할 수 있는 다른 커넥터 hello 우리의 [Api 목록](apis-list.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6df-191">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
