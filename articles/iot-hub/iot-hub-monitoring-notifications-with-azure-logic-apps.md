---
title: "Azure Logic Apps를 사용하여 IoT 원격 모니터링 및 알림 | Microsoft Docs"
description: "Azure Logic Apps을 사용하여 IoT Hub에서 IoT 온도를 모니터링하고 감지된 이상에 대한 전자 메일 알림을 자동으로 사서함에 보낼 수 있습니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "iot 모니터링, iot 알림, iot 온도 모니터링"
ms.assetid: 43043067-2e1f-42c9-953d-e2dce8fd86df
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: xshi
ms.openlocfilehash: 7a611912ae55eb22103539dbba9f1a06aaa543b7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="iot-remote-monitoring-and-notifications-with-azure-logic-apps-connecting-your-iot-hub-and-mailbox"></a><span data-ttu-id="70469-104">Azure Logic Apps으로 IoT Hub와 사서함을 연결하여 IoT 원격 모니터링 및 알림</span><span class="sxs-lookup"><span data-stu-id="70469-104">IoT remote monitoring and notifications with Azure Logic Apps connecting your IoT hub and mailbox</span></span>

![종단 간 다이어그램](media/iot-hub-get-started-e2e-diagram/7.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="70469-106">Azure Logic Apps은 일련의 단계로 프로세스를 자동화하는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-106">Azure Logic Apps provides a way to automate processes as a series of steps.</span></span> <span data-ttu-id="70469-107">논리 앱은 다양한 서비스 및 프로토콜을 통해 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70469-107">A logic app can connect across various services and protocols.</span></span> <span data-ttu-id="70469-108">'계정이 추가되면' 같은 트리거로 시작하여 '푸시 알림 전송' 같은 작업 조합이 이어집니다.</span><span class="sxs-lookup"><span data-stu-id="70469-108">It begins with a trigger such as 'When an account is added', and followed by a combination of actions, one like 'sending a push notification'.</span></span> <span data-ttu-id="70469-109">이 기능 덕분에 Logic Apps은 다른 여러 사용 시나리오도 지원하지만 특히 이상을 지속적으로 감지할 수 있다는 점에서 IoT 모니터링을 위한 완벽한 IoT 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="70469-109">This feature makes Logic Apps a perfect IoT solution for IoT monitoring, such as staying alert for anomalies, among other usage scenarios.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="70469-110">학습 내용</span><span class="sxs-lookup"><span data-stu-id="70469-110">What you learn</span></span>

<span data-ttu-id="70469-111">IoT Hub와 사서함을 연결하여 온도를 모니터링하고 알림을 보내는 논리 앱을 만드는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="70469-111">You learn how to create a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span></span> <span data-ttu-id="70469-112">온도가 30C를 넘으면 클라이언트 응용 프로그램은 IoT Hub로 보내는 메시지에 `temperatureAlert = "true"`를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-112">When the temperature is above 30 C, the client application marks `temperatureAlert = "true"` in the message it sends to your IoT hub.</span></span> <span data-ttu-id="70469-113">이 메시지는 사용자에게 전자 메일 알림을 보내도록 논리 앱을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-113">The message triggers the logic app to send you an email notification.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="70469-114">수행할 작업</span><span class="sxs-lookup"><span data-stu-id="70469-114">What you do</span></span>

* <span data-ttu-id="70469-115">Service Bus 네임스페이스를 만들고 큐를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-115">Create a service bus namespace and add a queue to it.</span></span>
* <span data-ttu-id="70469-116">IoT Hub에 끝점과 라우팅 규칙을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-116">Add an endpoint and a routing rule to your IoT hub.</span></span>
* <span data-ttu-id="70469-117">논리 앱을 만들고, 구성하고, 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-117">Create, configure, and test a logic app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="70469-118">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="70469-118">What you need</span></span>

* <span data-ttu-id="70469-119">다음 요구 사항을 다루는 자습서 [장치 설정](iot-hub-raspberry-pi-kit-node-get-started.md) 완료:</span><span class="sxs-lookup"><span data-stu-id="70469-119">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  * <span data-ttu-id="70469-120">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="70469-120">An active Azure subscription.</span></span>
  * <span data-ttu-id="70469-121">구독 중인 Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="70469-121">An Azure IoT hub under your subscription.</span></span>
  * <span data-ttu-id="70469-122">메시지를 Azure IoT Hub로 보내는 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="70469-122">A client application that sends messages to your Azure IoT hub.</span></span>

## <a name="create-service-bus-namespace-and-add-a-queue-to-it"></a><span data-ttu-id="70469-123">Service Bus 네임스페이스를 만들고 큐 추가</span><span class="sxs-lookup"><span data-stu-id="70469-123">Create service bus namespace and add a queue to it</span></span>

### <a name="create-a-service-bus-namespace"></a><span data-ttu-id="70469-124">Service Bus 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="70469-124">Create a service bus namespace</span></span>

1. <span data-ttu-id="70469-125">[Azure Portal](https://portal.azure.com/)에서 **새로 만들기** > **엔터프라이즈 통합** > **Service Bus**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-125">On the [Azure portal](https://portal.azure.com/), click **New** > **Enterprise Integration** > **Service Bus**.</span></span>
1. <span data-ttu-id="70469-126">다음 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-126">Provide the following information:</span></span>

   <span data-ttu-id="70469-127">**이름**: Service Bus 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="70469-127">**Name**: The name of the service bus.</span></span>

   <span data-ttu-id="70469-128">**가격 책정 계층**: **기본** > **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-128">**Pricing tier**: Click **Basic** > **Select**.</span></span> <span data-ttu-id="70469-129">이 자습서에서는 기본 계층이면 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-129">The Basic tier is sufficient for this tutorial.</span></span>

   <span data-ttu-id="70469-130">**리소스 그룹**: IoT Hub에서 사용하는 것과 동일한 리소스 그룹을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-130">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="70469-131">**위치**: IoT Hub에서 사용하는 것과 같은 위치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-131">**Location**: Use the same location that your IoT hub uses.</span></span>
1. <span data-ttu-id="70469-132">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-132">Click **Create**.</span></span>

   ![Azure Portal에서 Service Bus 네임스페이스 만들기](media/iot-hub-monitoring-notifications-with-azure-logic-apps/1_create-service-bus-namespace-azure-portal.png)

### <a name="add-a-service-bus-queue"></a><span data-ttu-id="70469-134">Service Bus 큐 추가</span><span class="sxs-lookup"><span data-stu-id="70469-134">Add a service bus queue</span></span>

1. <span data-ttu-id="70469-135">Service Bus 네임스페이스를 열고 **+ 큐**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-135">Open the service bus namespace, and then click **+ Queue**.</span></span>
1. <span data-ttu-id="70469-136">큐 이름을 입력한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-136">Enter a name for the queue and then click **Create**.</span></span>
1. <span data-ttu-id="70469-137">Service Bus 큐를 열고 **공유 액세스 정책** > **+ 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-137">Open the service bus queue, and then click **Shared access policies** > **+ Add**.</span></span>
1. <span data-ttu-id="70469-138">정책 이름을 입력하고, **관리**를 선택한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-138">Enter a name for the policy, check **Manage**, and then click **Create**.</span></span>

   ![Azure Portal에서 Service Bus 큐 추가](media/iot-hub-monitoring-notifications-with-azure-logic-apps/2_add-service-bus-queue-azure-portal.png)

## <a name="add-an-endpoint-and-a-routing-rule-to-your-iot-hub"></a><span data-ttu-id="70469-140">IoT Hub에 끝점과 라우팅 규칙 추가</span><span class="sxs-lookup"><span data-stu-id="70469-140">Add an endpoint and a routing rule to your IoT hub</span></span>

### <a name="add-an-endpoint"></a><span data-ttu-id="70469-141">끝점 추가</span><span class="sxs-lookup"><span data-stu-id="70469-141">Add an endpoint</span></span>

1. <span data-ttu-id="70469-142">IoT Hub를 열고 끝점 > + 추가를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-142">Open your IoT hub, click Endpoints > + Add.</span></span>
1. <span data-ttu-id="70469-143">다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-143">Enter the following information:</span></span>

   <span data-ttu-id="70469-144">**이름**: 끝점의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="70469-144">**Name**: The name of the endpoint.</span></span>

   <span data-ttu-id="70469-145">**끝점 유형**: **Service Bus 큐**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-145">**Endpoint type**: Select **Service Bus Queue**.</span></span>

   <span data-ttu-id="70469-146">**Service Bus 네임스페이스**: 앞에서 만든 네임스페이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-146">**Service Bus namespace**: Select the namespace you created.</span></span>

   <span data-ttu-id="70469-147">**Service Bus 큐**: 앞에서 만든 큐를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-147">**Service Bus queue**: Select the queue you created.</span></span>
1. <span data-ttu-id="70469-148">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-148">Click **OK**.</span></span>

   ![Azure Portal에서 IoT Hub에 끝점 추가](media/iot-hub-monitoring-notifications-with-azure-logic-apps/3_add-iot-hub-endpoint-azure-portal.png)

### <a name="add-a-routing-rule"></a><span data-ttu-id="70469-150">라우팅 규칙 추가</span><span class="sxs-lookup"><span data-stu-id="70469-150">Add a routing rule</span></span>

1. <span data-ttu-id="70469-151">IoT Hub에서 **경로** > **+ 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-151">In your IoT hub, click **Routes** > **+ Add**.</span></span>
1. <span data-ttu-id="70469-152">다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-152">Enter the following information:</span></span>

   <span data-ttu-id="70469-153">**이름**: 라우팅 규칙의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="70469-153">**Name**: The name of the routing rule.</span></span>

   <span data-ttu-id="70469-154">**데이터 원본**: **DeviceMessages**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-154">**Data source**: Select **DeviceMessages**.</span></span>

   <span data-ttu-id="70469-155">**끝점**: 앞에서 만든 끝점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-155">**Endpoint**: Select the endpoint you created.</span></span>

   <span data-ttu-id="70469-156">**쿼리 문자열**: `temperatureAlert = "true"`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-156">**Query string**: Enter `temperatureAlert = "true"`.</span></span>
1. <span data-ttu-id="70469-157">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-157">Click **Save**.</span></span>

   ![Azure Portal에서 라우팅 규칙 추가](media/iot-hub-monitoring-notifications-with-azure-logic-apps/4_add-routing-rule-azure-portal.png)

## <a name="create-and-configure-a-logic-app"></a><span data-ttu-id="70469-159">논리 앱을 만들고 구성</span><span class="sxs-lookup"><span data-stu-id="70469-159">Create and configure a logic app</span></span>

### <a name="create-a-logic-app"></a><span data-ttu-id="70469-160">논리 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="70469-160">Create a logic app</span></span>

1. <span data-ttu-id="70469-161">[Azure Portal](https://portal.azure.com/)에서 **새로 만들기** > **엔터프라이즈 통합** > **논리 앱**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-161">In the [Azure portal](https://portal.azure.com/), click **New** > **Enterprise Integration** > **Logic App**.</span></span>
1. <span data-ttu-id="70469-162">다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-162">Enter the following information:</span></span>

   <span data-ttu-id="70469-163">**이름**: 논리 앱의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="70469-163">**Name**: The name of the logic app.</span></span>

   <span data-ttu-id="70469-164">**리소스 그룹**: IoT Hub에서 사용하는 것과 동일한 리소스 그룹을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-164">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="70469-165">**위치**: IoT Hub에서 사용하는 것과 같은 위치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-165">**Location**: Use the same location that your IoT hub uses.</span></span>
1. <span data-ttu-id="70469-166">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-166">Click **Create**.</span></span>

### <a name="configure-the-logic-app"></a><span data-ttu-id="70469-167">논리 앱 구성</span><span class="sxs-lookup"><span data-stu-id="70469-167">Configure the logic app</span></span>

1. <span data-ttu-id="70469-168">논리 앱을 열면 논리 앱 디자이너가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="70469-168">Open the logic app that opens into the Logic Apps Designer.</span></span>
1. <span data-ttu-id="70469-169">논리 앱 디자이너에서 **빈 논리 앱**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-169">In the Logic Apps Designer, click **Blank Logic App**.</span></span>

   ![Azure Portal에서 빈 논리 앱 시작](media/iot-hub-monitoring-notifications-with-azure-logic-apps/5_start-with-blank-logic-app-azure-portal.png)

1. <span data-ttu-id="70469-171">**Service Bus**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-171">Click **Service Bus**.</span></span>

   ![Service Bus를 선택하여 Azure Portal에서 논리 앱 만들기 시작](media/iot-hub-monitoring-notifications-with-azure-logic-apps/6_select-service-bus-when-creating-blank-logic-app-azure-portal.png)

1. <span data-ttu-id="70469-173">**Service Bus – 큐에 하나 이상의 메시지가 도착하는 경우(자동 완성)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-173">Click **Service Bus – When one or more messages arrive in a queue (auto-complete)**.</span></span>
1. <span data-ttu-id="70469-174">Service Bus 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="70469-174">Create a service bus connection.</span></span>
   1. <span data-ttu-id="70469-175">연결 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-175">Enter a connection name.</span></span>
   1. <span data-ttu-id="70469-176">Service Bus 네임스페이스 > Service Bus 정책 > **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-176">Click the service bus namespace > the service bus policy > **Create**.</span></span>

      ![Azure Portal에서 논리 앱에 대한 Service Bus 연결 만들기](media/iot-hub-monitoring-notifications-with-azure-logic-apps/7_create-service-bus-connection-in-logic-app-azure-portal.png)

   1. <span data-ttu-id="70469-178">Service Bus 연결을 만든 후 **계속**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-178">Click **Continue** after the service bus connection is created.</span></span>
   1. <span data-ttu-id="70469-179">앞에서 만든 큐를 선택하고 **최대 메시지 수**에 `175`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-179">Select the queue that you created and enter `175` for **Maximum message count**</span></span>

      ![논리 앱에서 Service Bus 연결의 최대 메시지 수 지정](media/iot-hub-monitoring-notifications-with-azure-logic-apps/8_specify-maximum-message-count-for-service-bus-connection-logic-app-azure-portal.png)
   1. <span data-ttu-id="70469-181">“저장” 단추를 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-181">Click "Save" button to save the changes.</span></span>

1. <span data-ttu-id="70469-182">SMTP 서비스 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="70469-182">Create an SMTP service connection.</span></span>
   1. <span data-ttu-id="70469-183">**다음 단계** > **작업 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-183">Click **New step** > **Add an action**.</span></span>
   1. <span data-ttu-id="70469-184">`SMTP`를 입력하고, 검색 결과에서 **SMTP** 서비스를 클릭한 다음 **SMTP - 전자 메일 보내기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-184">Type `SMTP`, click the **SMTP** service in the search result, and then click **SMTP - Send Email**.</span></span>

      ![Azure Portal에서 논리 앱에 SMTP 연결 만들기](media/iot-hub-monitoring-notifications-with-azure-logic-apps/9_create-smtp-connection-logic-app-azure-portal.png)

   1. <span data-ttu-id="70469-186">사서함의 SMTP 정보를 입력한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-186">Enter the SMTP information of your mailbox, and then click **Create**.</span></span>

      ![Azure Portal에서 논리 앱에 SMTP 연결 정보 입력](media/iot-hub-monitoring-notifications-with-azure-logic-apps/10_enter-smtp-connection-info-logic-app-azure-portal.png)

      <span data-ttu-id="70469-188">[Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en) 및 [Yahoo Mail](https://help.yahoo.com/kb/SLN4075.html)에 대한 SMTP 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="70469-188">Get the SMTP information for [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en), and [Yahoo Mail](https://help.yahoo.com/kb/SLN4075.html).</span></span>
   1. <span data-ttu-id="70469-189">**보내는 사람** 및 **받는 사람**의 전자 메일 주소를 입력하고, **제목** 및 **본문**에 `High temperature detected`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-189">Enter your email address for **From** and **To**, and `High temperature detected` for **Subject** and **Body**.</span></span>
   1. <span data-ttu-id="70469-190">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-190">Click **Save**.</span></span>

<span data-ttu-id="70469-191">논리 앱을 저장할 때 논리 앱이 정상적으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-191">The logic app is in working order when you save it.</span></span>

## <a name="test-the-logic-app"></a><span data-ttu-id="70469-192">논리 앱 테스트</span><span class="sxs-lookup"><span data-stu-id="70469-192">Test the logic app</span></span>

1. <span data-ttu-id="70469-193">[Azure IoT Hub에 ESP8266 연결](iot-hub-arduino-huzzah-esp8266-get-started.md)에서 장치에 배포한 클라이언트 응용 프로그램을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="70469-193">Start the client application that you deploy to your device in [Connect ESP8266 to Azure IoT Hub](iot-hub-arduino-huzzah-esp8266-get-started.md).</span></span>
1. <span data-ttu-id="70469-194">SensorTag 주변의 환경 온도를 30C 이상으로 높입니다. 예를 들어 SensorTag 주변에 촛불을 켭니다.</span><span class="sxs-lookup"><span data-stu-id="70469-194">Increase the environment temperature around the SensorTag to be above 30 C. For example, light a candle around your SensorTag.</span></span>
1. <span data-ttu-id="70469-195">논리 앱에서 보낸 전자 메일 알림을 수신하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="70469-195">You should receive an email notification sent by the logic app.</span></span>

   > [!NOTE]
   > <span data-ttu-id="70469-196">전자 메일을 보낸 사람이 본인이라는 것을 확인하기 위해 전자 메일 서비스 공급자가 발신자의 신분을 확인해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70469-196">Your email service provider may need to verify the sender identity to make sure it is you who sends the email.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70469-197">다음 단계</span><span class="sxs-lookup"><span data-stu-id="70469-197">Next steps</span></span>

<span data-ttu-id="70469-198">IoT Hub와 사서함을 연결하여 온도를 모니터링하고 알림을 보내는 논리 앱을 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="70469-198">You have successfully created a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
