---
title: "Azure Logic Apps에서 MQ 커넥터를 사용하는 방법 알아보기 | Microsoft Docs"
description: "논리 앱 워크플로에서 온-프레미스 또는 Azure MQ 서버에 연결하여 메시지 찾아보기, 수신 및 WebSphere MQ에 전송"
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
ms.openlocfilehash: 17c651585b56dae186286f5d8c68c363ae9c524d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-to-an-ibm-mq-server-from-logic-apps-using-the-mq-connector"></a><span data-ttu-id="4febf-103">MQ 커넥터를 사용하여 논리 앱에서 IBM MQ 서버에 연결</span><span class="sxs-lookup"><span data-stu-id="4febf-103">Connect to an IBM MQ server from logic apps using the MQ connector</span></span> 

<span data-ttu-id="4febf-104">MQ용 Microsoft 커넥터는 MQ 서버 온-프레미스 또는 Azure에 저장된 메시지를 전송하고 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-104">Microsoft Connector for MQ sends and retrieves messages stored in an MQ Server on-premises, or in Azure.</span></span> <span data-ttu-id="4febf-105">이 커넥터는 TCP/IP 네트워크를 통해 원격 IBM MQ 서버와 통신하는 Microsoft MQ 클라이언트를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-105">This connector includes a Microsoft MQ client that communicates with a remote IBM MQ server across a TCP/IP network.</span></span> <span data-ttu-id="4febf-106">이 문서는 MQ 커넥터를 사용하는 시작 가이드입니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-106">This document is a starter guide to use the MQ connector.</span></span> <span data-ttu-id="4febf-107">큐에서 단일 메시지를 검색하고 다른 작업을 시도하여 시작하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-107">We recommended you begin by browsing a single message on a queue, and then trying the other actions.</span></span>    

<span data-ttu-id="4febf-108">MQ 커넥터에는 다음 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-108">The MQ connector includes the following actions.</span></span> <span data-ttu-id="4febf-109">트리거는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-109">There are no triggers.</span></span>

-   <span data-ttu-id="4febf-110">IBM MQ 서버에서 메시지를 삭제하지 않고 단일 메시지 찾아보기</span><span class="sxs-lookup"><span data-stu-id="4febf-110">Browse a single message without deleting the message from the IBM MQ Server</span></span>
-   <span data-ttu-id="4febf-111">IBM MQ 서버에서 메시지를 삭제하지 않고 일괄 처리 메시지 찾아보기</span><span class="sxs-lookup"><span data-stu-id="4febf-111">Browse a batch of messages without deleting the messages from the IBM MQ Server</span></span>
-   <span data-ttu-id="4febf-112">단일 메시지 수신 및 IBM MQ 서버에서 메시지 삭제</span><span class="sxs-lookup"><span data-stu-id="4febf-112">Receive a single message and delete the message from the IBM MQ Server</span></span>
-   <span data-ttu-id="4febf-113">일괄 처리 메시지 수신 및 IBM MQ 서버에서 메시지 삭제</span><span class="sxs-lookup"><span data-stu-id="4febf-113">Receive a batch of messages and delete the messages from the IBM MQ Server</span></span>
-   <span data-ttu-id="4febf-114">IBM MQ 서버에 단일 메시지 전송</span><span class="sxs-lookup"><span data-stu-id="4febf-114">Send a single message to the IBM MQ Server</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4febf-115">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4febf-115">Prerequisites</span></span>

* <span data-ttu-id="4febf-116">온-프레미스 MQ 서버를 사용하는 경우 네트워크 내의 서버에서 [온-프레미스 데이터 게이트웨이를 설치](../logic-apps/logic-apps-gateway-install.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-116">If using an on-premises MQ server, [install the on-premises data gateway](../logic-apps/logic-apps-gateway-install.md) on a server within your network.</span></span> <span data-ttu-id="4febf-117">MQ 서버가 공개적으로 사용할 수 있거나 Azure 내에서 사용할 수 있는 경우 데이터 게이트웨이를 사용하지 않거나 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-117">If the MQ Server is publicly available, or available within Azure, then the data gateway is not used or required.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4febf-118">온-프레미스 데이터 게이트웨이를 설치한 서버에는 MQ 커넥터가 작동하기 위한 .Net Framework 4.6도 설치되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-118">The server where the On-Premises Data Gateway is installed must also have .Net Framework 4.6 installed for the MQ Connector to function.</span></span>

* <span data-ttu-id="4febf-119">온-프레미스 데이터 게이트웨이에 Azure 리소스 만들기 - [데이터 게이트웨이 연결을 설정합니다](../logic-apps/logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="4febf-119">Create the Azure resource for the on-premises data gateway - [Set up the data gateway connection](../logic-apps/logic-apps-gateway-connection.md).</span></span>

* <span data-ttu-id="4febf-120">공식적으로 지원되는 IBM WebSphere MQ 버전:</span><span class="sxs-lookup"><span data-stu-id="4febf-120">Officially supported IBM WebSphere MQ versions:</span></span>
   * <span data-ttu-id="4febf-121">MQ 7.5</span><span class="sxs-lookup"><span data-stu-id="4febf-121">MQ 7.5</span></span>
   * <span data-ttu-id="4febf-122">MQ 8.0</span><span class="sxs-lookup"><span data-stu-id="4febf-122">MQ 8.0</span></span>

## <a name="create-a-logic-app"></a><span data-ttu-id="4febf-123">논리 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="4febf-123">Create a logic app</span></span>

1. <span data-ttu-id="4febf-124">**Azure 시작 보드**에서 **+**(더하기 기호), **웹 + 모바일**, **논리 앱**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-124">In the **Azure start board**, select **+** (plus sign), **Web + Mobile**, and then **Logic App**.</span></span> 
2. <span data-ttu-id="4febf-125">MQTestApp, **구독**, **리소스 그룹** 및 **위치**와 같은 **이름**을 입력합니다(온-프레미스 데이터 게이트웨이 연결이 구성된 위치를 사용).</span><span class="sxs-lookup"><span data-stu-id="4febf-125">Enter the **Name**, such as MQTestApp, **Subscription**, **Resource group**, and **Location** (use the location where the on-premises Data Gateway connection is configured).</span></span> <span data-ttu-id="4febf-126">**대시보드에 고정**을 선택하고 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-126">Select **Pin to dashboard**, and select **Create**.</span></span>  
<span data-ttu-id="4febf-127">![논리 앱 만들기](media/connectors-create-api-mq/Create_Logic_App.png)</span><span class="sxs-lookup"><span data-stu-id="4febf-127">![Create Logic App](media/connectors-create-api-mq/Create_Logic_App.png)</span></span>

## <a name="add-a-trigger"></a><span data-ttu-id="4febf-128">트리거 추가</span><span class="sxs-lookup"><span data-stu-id="4febf-128">Add a trigger</span></span>

> [!NOTE]
> <span data-ttu-id="4febf-129">MQ 커넥터에는 트리거가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-129">The MQ Connector does not have any triggers.</span></span> <span data-ttu-id="4febf-130">따라서 다른 트리거를 사용하여 **되풀이** 트리거와 같은 논리 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-130">So, use another trigger to start your logic app, such as the **Recurrence** trigger.</span></span> 

1. <span data-ttu-id="4febf-131">**Logic Apps 디자이너**가 열리면 일반적인 트리거의 목록에서 **되풀이**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-131">The **Logic Apps Designer** opens, select **Recurrence** in the list of common triggers.</span></span>
2. <span data-ttu-id="4febf-132">되풀이 트리거 내에서 **편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-132">Select **Edit** within the Recurrence Trigger.</span></span> 
3. <span data-ttu-id="4febf-133">**빈도**를 **일**로, **간격**을 **7**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-133">Set the **Frequency** to **Day**, and set the **Interval** to **7**.</span></span> 

## <a name="browse-a-single-message"></a><span data-ttu-id="4febf-134">단일 메시지 찾아보기</span><span class="sxs-lookup"><span data-stu-id="4febf-134">Browse a single message</span></span>
1. <span data-ttu-id="4febf-135">**+ 새 단계**를 선택한 다음 **작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-135">Select **+ New step**, and select **Add an action**.</span></span>
2. <span data-ttu-id="4febf-136">검색 상자에 `mq`을 입력한 다음 **MQ - 메시지 찾아보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-136">In the search box, type `mq`, and then select **MQ - Browse message**.</span></span>  
<span data-ttu-id="4febf-137">![메시지 찾아보기](media/connectors-create-api-mq/Browse_message.png)</span><span class="sxs-lookup"><span data-stu-id="4febf-137">![Browse message](media/connectors-create-api-mq/Browse_message.png)</span></span>

3. <span data-ttu-id="4febf-138">기존 MQ 연결이 없으면 다음 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-138">If there isn't an existing MQ connection, then create the connection:</span></span>  

    1. <span data-ttu-id="4febf-139">**온-프레미스 데이터 게이트웨이를 통해 연결**을 선택하고 MQ 서버의 속성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-139">Select **Connect via on-premises data gateway**, and enter the properties of your MQ server.</span></span>  
    <span data-ttu-id="4febf-140">**서버**에서 MQ 서버 이름을 입력하거나 콜론과 포트 번호 뒤에 IP 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-140">For **Server**, you can enter the MQ server name, or enter the IP address followed by a colon and the port number.</span></span> 
    2. <span data-ttu-id="4febf-141">**게이트웨이** 드롭다운은 구성된 기존 게이트웨이 연결을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-141">The **gateway** dropdown lists any existing gateway connections that have been configured.</span></span> <span data-ttu-id="4febf-142">게이트웨이를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-142">Select your gateway.</span></span>
    3. <span data-ttu-id="4febf-143">작업을 완료하면 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-143">Select **Create** when finished.</span></span> <span data-ttu-id="4febf-144">연결은 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-144">Your connection looks similar to the following:</span></span>   
    <span data-ttu-id="4febf-145">![연결 속성](media/connectors-create-api-mq/Connection_Properties.png)</span><span class="sxs-lookup"><span data-stu-id="4febf-145">![Connection Properties](media/connectors-create-api-mq/Connection_Properties.png)</span></span>

4. <span data-ttu-id="4febf-146">작업 속성에서 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-146">In the action properties, you can:</span></span>  

    * <span data-ttu-id="4febf-147">**큐** 속성을 사용하여 연결에 정의된 것과 다른 큐 이름에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-147">Use the **Queue** property to access a different queue name than what is defined in the connection</span></span>
    * <span data-ttu-id="4febf-148">**MessageId**, **CorrelationId**, **GroupId** 및 기타 속성을 사용하여 다른 MQ 메시지 속성에 따라 메시지를 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-148">Use the **MessageId**, **CorrelationId**, **GroupId**, and other properties to browse for a message based on the different MQ message properties</span></span>
    * <span data-ttu-id="4febf-149">**IncludeInfo**를 **True**로 설정하여 출력에서 추가 메시지 정보를 포함하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-149">Set **IncludeInfo** to **True** to include additional message information in the output.</span></span> <span data-ttu-id="4febf-150">또는 해당 항목을 **False**로 설정하여 출력에서 추가 메시지 정보를 포함하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-150">Or, set it to **False** to not include additional message information in the output.</span></span>
    * <span data-ttu-id="4febf-151">비어 있는 큐에 도달하는 메시지를 기다리는 기간을 결정하는 **시간 제한** 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-151">Enter a **Timeout** value to determine how long to wait for a message to arrive in an empty queue.</span></span> <span data-ttu-id="4febf-152">아무 것도 입력하지 않은 경우 큐의 첫 번째 메시지를 검색하면 메시지가 표시되는 시간이 없어집니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-152">If nothing is entered, the first message in the queue is retrieved, and there is no time spent waiting for a message to appear.</span></span>  
    <span data-ttu-id="4febf-153">![메시지 속성 찾아보기](media/connectors-create-api-mq/Browse_message_Props.png)</span><span class="sxs-lookup"><span data-stu-id="4febf-153">![Browse Message Properties](media/connectors-create-api-mq/Browse_message_Props.png)</span></span>

5. <span data-ttu-id="4febf-154">변경 내용을 **저장**한 다음 논리 앱을 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-154">**Save** your changes, and then **Run** your logic app:</span></span>  
<span data-ttu-id="4febf-155">![저장 및 실행](media/connectors-create-api-mq/Save_Run.png)</span><span class="sxs-lookup"><span data-stu-id="4febf-155">![Save and run](media/connectors-create-api-mq/Save_Run.png)</span></span>

6. <span data-ttu-id="4febf-156">몇 초 후에 실행 단계가 표시되고 출력을 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-156">After a few seconds, the steps of the run are shown, and you can look at the output.</span></span> <span data-ttu-id="4febf-157">각 단계에 대한 자세한 내용을 보려면 녹색 확인 표시를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-157">Select the green checkmark to see details of each step.</span></span> <span data-ttu-id="4febf-158">**원시 출력 참조**를 선택하여 출력 데이터에 대한 추가 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-158">Select **See raw outputs** to see additional details on the output data.</span></span>  
<span data-ttu-id="4febf-159">![메시지 출력 찾아보기](media/connectors-create-api-mq/Browse_message_output.png)</span><span class="sxs-lookup"><span data-stu-id="4febf-159">![Browse message output](media/connectors-create-api-mq/Browse_message_output.png)</span></span>  

    <span data-ttu-id="4febf-160">원시 출력:</span><span class="sxs-lookup"><span data-stu-id="4febf-160">Raw output:</span></span>  
    ![메시지 원시 출력 찾아보기](media/connectors-create-api-mq/Browse_message_raw_output.png)

7. <span data-ttu-id="4febf-162">**IncludeInfo** 옵션이 true로 설정되면 다음과 같은 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-162">When the **IncludeInfo** option is set to true, the following output is displayed:</span></span>  
<span data-ttu-id="4febf-163">![메시지 포함 정보 찾아보기](media/connectors-create-api-mq/Browse_message_Include_Info.png)</span><span class="sxs-lookup"><span data-stu-id="4febf-163">![Browse message include info](media/connectors-create-api-mq/Browse_message_Include_Info.png)</span></span>

## <a name="browse-multiple-messages"></a><span data-ttu-id="4febf-164">여러 메시지 찾아보기</span><span class="sxs-lookup"><span data-stu-id="4febf-164">Browse multiple messages</span></span>
<span data-ttu-id="4febf-165">**메시지 찾아보기** 작업은 큐에서 반환되는 메시지의 수를 나타내는 **BatchSize** 옵션을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-165">The **Browse messages** action includes a **BatchSize** option to indicate how many messages should be returned from the queue.</span></span>  <span data-ttu-id="4febf-166">**BatchSize**에 항목이 없는 경우 모든 메시지가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-166">If **BatchSize** has no entry, all messages are returned.</span></span> <span data-ttu-id="4febf-167">반환된 출력은 메시지의 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-167">The returned output is an array of messages.</span></span>

1. <span data-ttu-id="4febf-168">**메시지 찾아보기** 작업을 추가하는 경우 기본적으로 구성된 첫 번째 연결이 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-168">When adding the **Browse messages** action, the first connection that is configured is selected by default.</span></span> <span data-ttu-id="4febf-169">**연결 변경**을 선택하여 새 연결을 만들거나 다른 연결을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-169">Select **Change connection** to create a new connection, or select a different connection.</span></span>

2. <span data-ttu-id="4febf-170">찾아보기 메시지의 출력은 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-170">The output of Browse messages shows:</span></span>  
![메시지 출력 찾아보기](media/connectors-create-api-mq/Browse_messages_output.png)

## <a name="receive-a-single-message"></a><span data-ttu-id="4febf-172">단일 메시지 수신</span><span class="sxs-lookup"><span data-stu-id="4febf-172">Receive a single message</span></span>
<span data-ttu-id="4febf-173">**메시지 수신** 작업에는 **메시지 찾아보기** 작업과 동일한 입력 및 출력이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-173">The **Receive message** action has the same inputs and outputs as the **Browse message** action.</span></span> <span data-ttu-id="4febf-174">**메시지 수신**을 사용하는 경우 메시지는 큐에서 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-174">When using **Receive message**, the message is deleted from the queue.</span></span>

## <a name="receive-multiple-messages"></a><span data-ttu-id="4febf-175">여러 메시지 수신</span><span class="sxs-lookup"><span data-stu-id="4febf-175">Receive multiple messages</span></span>
<span data-ttu-id="4febf-176">**메시지 수신** 작업에는 **메시지 찾아보기** 작업과 동일한 입력 및 출력이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-176">The **Receive messages** action has the same inputs and outputs as the **Browse messages** action.</span></span> <span data-ttu-id="4febf-177">**메시지 수신**을 사용하는 경우 메시지는 큐에서 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-177">When using **Receive messages**, the messages are deleted from the queue.</span></span>

<span data-ttu-id="4febf-178">찾아보기 또는 수신을 수행하는 경우 큐에 메시지가 없으면 단계는 다음과 같은 출력을 표시하여 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-178">If there are no messages in the queue when doing a browse or a receive, the step fails with the following output:</span></span>  
![MQ 메시지 오류 없음](media/connectors-create-api-mq/MQ_No_Msg_Error.png)

## <a name="send-a-message"></a><span data-ttu-id="4febf-180">메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="4febf-180">Send a message</span></span>
1. <span data-ttu-id="4febf-181">**메시지 발신** 작업을 추가하는 경우 기본적으로 구성된 첫 번째 연결이 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-181">When adding the **Send message** action, the first connection that is configured is selected by default.</span></span> <span data-ttu-id="4febf-182">**연결 변경**을 선택하여 새 연결을 만들거나 다른 연결을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-182">Select **Change connection** to create a new connection, or select a different connection.</span></span> <span data-ttu-id="4febf-183">유효한 **메시지 형식**은 **데이터그램**, **회신** 또는 **요청**입니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-183">The valid **Message Types** are **Datagram**, **Reply**, or **Request**.</span></span>  
<span data-ttu-id="4febf-184">![메시지 속성 전송](media/connectors-create-api-mq/Send_Msg_Props.png)</span><span class="sxs-lookup"><span data-stu-id="4febf-184">![Send Msg Props](media/connectors-create-api-mq/Send_Msg_Props.png)</span></span>

2. <span data-ttu-id="4febf-185">메시지 전송의 출력은 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-185">The output of Send message looks like the following:</span></span>  
![메시지 출력 전송](media/connectors-create-api-mq/Send_Msg_Output.png)

## <a name="connector-specific-details"></a><span data-ttu-id="4febf-187">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="4febf-187">Connector-specific details</span></span>

<span data-ttu-id="4febf-188">[커넥터 세부 정보](/connectors/mq/)에서 swagger에 정의된 모든 트리거 및 작업과 제한 사항도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4febf-188">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/mq/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4febf-189">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4febf-189">Next steps</span></span>
<span data-ttu-id="4febf-190">[논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)</span><span class="sxs-lookup"><span data-stu-id="4febf-190">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="4febf-191">[API 목록](apis-list.md)에서 Logic Apps의 사용 가능한 다른 커넥터를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="4febf-191">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
