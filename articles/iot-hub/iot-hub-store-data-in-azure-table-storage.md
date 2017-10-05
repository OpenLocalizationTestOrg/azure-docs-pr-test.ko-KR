---
title: "Azure 데이터 저장소에 IoT Hub 메시지 저장 | Microsoft Docs"
description: "Azure 함수 앱을 사용하여 Azure Table Storage에 IoT Hub 메시지를 저장합니다. IoT Hub 메시지에는 IoT 장치에서 보낸 센서 데이터와 같은 정보가 있습니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "IoT 데이터 저장소, IoT 센서 데이터 저장소"
ms.assetid: 62fd14fd-aaaa-4b3d-8367-75c1111b6269
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 06503f9564e00ef62587d02f2da4778974e246c5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="save-iot-hub-messages-that-contain-sensor-data-to-your-azure-table-storage"></a><span data-ttu-id="6b97f-105">Azure Table Storage에 센서 데이터를 포함한 IoT Hub 메시지 저장</span><span class="sxs-lookup"><span data-stu-id="6b97f-105">Save IoT hub messages that contain sensor data to your Azure table storage</span></span>

![종단 간 다이어그램](media/iot-hub-get-started-e2e-diagram/3.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="6b97f-107">학습 내용</span><span class="sxs-lookup"><span data-stu-id="6b97f-107">What you learn</span></span>

<span data-ttu-id="6b97f-108">Azure Storage 계정 및 Azure 함수 앱을 만들어 Table Storage에 IoT Hub 메시지를 저장하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-108">You learn how to create an Azure storage account and an Azure function app to store IoT hub messages in your table storage.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="6b97f-109">수행할 작업</span><span class="sxs-lookup"><span data-stu-id="6b97f-109">What you do</span></span>

- <span data-ttu-id="6b97f-110">Azure 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="6b97f-110">Create an Azure storage account.</span></span>
- <span data-ttu-id="6b97f-111">메시지를 읽도록 IoT Hub 연결 준비</span><span class="sxs-lookup"><span data-stu-id="6b97f-111">Prepare your IoT hub connection to read messages.</span></span>
- <span data-ttu-id="6b97f-112">Azure 함수 앱 만들기 및 배포</span><span class="sxs-lookup"><span data-stu-id="6b97f-112">Create and deploy an Azure function app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="6b97f-113">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="6b97f-113">What you need</span></span>

- <span data-ttu-id="6b97f-114">다음 요구 사항에 맞게 [장치를 설정](iot-hub-raspberry-pi-kit-node-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-114">[Set up your device](iot-hub-raspberry-pi-kit-node-get-started.md) to cover the following requirements:</span></span>
  - <span data-ttu-id="6b97f-115">활성 Azure 구독</span><span class="sxs-lookup"><span data-stu-id="6b97f-115">An active Azure subscription</span></span>
  - <span data-ttu-id="6b97f-116">구독 중인 IoT Hub</span><span class="sxs-lookup"><span data-stu-id="6b97f-116">An IoT hub under your subscription</span></span> 
  - <span data-ttu-id="6b97f-117">메시지를 IoT Hub로 보내는 실행 중인 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="6b97f-117">A running application that sends messages to your IoT hub</span></span>

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="6b97f-118">Azure 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="6b97f-118">Create an Azure storage account</span></span>

1. <span data-ttu-id="6b97f-119">[Azure Portal](https://portal.azure.com/)에서 **새로 만들기** > **저장소** > **저장소 계정** > **만들기**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-119">In the [Azure portal](https://portal.azure.com/), click **New** > **Storage** > **Storage account** > **Create**.</span></span>

2. <span data-ttu-id="6b97f-120">저장소 계정에 필요한 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-120">Enter the necessary information for the storage account:</span></span>

   ![Azure Portal에서 저장소 계정 만들기](media\iot-hub-store-data-in-azure-table-storage\1_azure-portal-create-storage-account.png)

   * <span data-ttu-id="6b97f-122">**이름** - 저장소 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-122">**Name**: The name of the storage account.</span></span> <span data-ttu-id="6b97f-123">이름은 전역적으로 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-123">The name must be globally unique.</span></span>

   * <span data-ttu-id="6b97f-124">**리소스 그룹**: IoT Hub에서 사용하는 것과 동일한 리소스 그룹을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-124">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   * <span data-ttu-id="6b97f-125">**대시보드에 고정**: 대시보드에서 IoT Hub에 쉽게 액세스하려면 이 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-125">**Pin to dashboard**: Select this option for easy access to your IoT hub from the dashboard.</span></span>

3. <span data-ttu-id="6b97f-126">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-126">Click **Create**.</span></span>

## <a name="prepare-your-iot-hub-connection-to-read-messages"></a><span data-ttu-id="6b97f-127">메시지를 읽도록 IoT Hub 연결 준비</span><span class="sxs-lookup"><span data-stu-id="6b97f-127">Prepare your IoT hub connection to read messages</span></span>

<span data-ttu-id="6b97f-128">IoT Hub에서 기본 제공 Event Hub 호환 끝점을 노출하여 응용 프로그램이 IoT Hub 메시지를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-128">IoT hub exposes a built-in event hub-compatible endpoint to enable applications to read IoT hub messages.</span></span> <span data-ttu-id="6b97f-129">한편 응용 프로그램은 소비자 그룹을 사용하여 IoT Hub에서 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-129">Meanwhile, applications use consumer groups to read data from your IoT hub.</span></span> <span data-ttu-id="6b97f-130">IoT Hub에서 데이터를 읽는 Azure 함수 앱을 만들기 전에 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-130">Before you create an Azure function app to read data from your IoT hub, do the following:</span></span>

- <span data-ttu-id="6b97f-131">IoT Hub 끝점의 연결 문자열 가져오기</span><span class="sxs-lookup"><span data-stu-id="6b97f-131">Get the connection string of your IoT hub endpoint.</span></span>
- <span data-ttu-id="6b97f-132">IoT Hub에 대한 소비자 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="6b97f-132">Create a consumer group for your IoT hub.</span></span>

### <a name="get-the-connection-string-of-your-iot-hub-endpoint"></a><span data-ttu-id="6b97f-133">IoT Hub 끝점의 연결 문자열 가져오기</span><span class="sxs-lookup"><span data-stu-id="6b97f-133">Get the connection string of your IoT hub endpoint</span></span>

1. <span data-ttu-id="6b97f-134">IoT Hub를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-134">Open your IoT hub.</span></span>

2. <span data-ttu-id="6b97f-135">**IoT Hub** 창에서 **메시지** 아래에 있는 **끝점**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-135">On the **IoT Hub** pane, under **Messaging**, click **Endpoints**.</span></span>

3. <span data-ttu-id="6b97f-136">오른쪽 창에서 **기본 제공 끝점** 아래에 있는 **이벤트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-136">In the right pane, under **Built-in endpoints**, click **Events**.</span></span>

4. <span data-ttu-id="6b97f-137">**속성** 창에서 다음 값을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-137">In the **Properties** pane, note the following values:</span></span>
   - <span data-ttu-id="6b97f-138">Event Hub 호환 끝점</span><span class="sxs-lookup"><span data-stu-id="6b97f-138">Event hub-compatible endpoint</span></span>
   - <span data-ttu-id="6b97f-139">Event Hub 호환 이름</span><span class="sxs-lookup"><span data-stu-id="6b97f-139">Event hub-compatible name</span></span>

   ![Azure Portal에서 IoT Hub 끝점의 연결 문자열 가져오기](media\iot-hub-store-data-in-azure-table-storage\2_azure-portal-iot-hub-endpoint-connection-string.png)

5. <span data-ttu-id="6b97f-141">**IoT Hub** 창에서 **설정** 아래에 있는 **공유 액세스 정책**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-141">In the **IoT Hub** pane, under **Settings**, click **Shared access policies**.</span></span>

6. <span data-ttu-id="6b97f-142">**iothubowner**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-142">Click **iothubowner**.</span></span>

7. <span data-ttu-id="6b97f-143">**기본 키** 값을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-143">Note the **Primary key** value.</span></span>

8. <span data-ttu-id="6b97f-144">IoT Hub 끝점의 연결 문자열을 다음과 같이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-144">Create the connection string of your IoT hub endpoint as follows:</span></span>

   `Endpoint=<Event Hub-compatible endpoint>;SharedAccessKeyName=iothubowner;SharedAccessKey=<Primary key>`

   > [!NOTE]
   > <span data-ttu-id="6b97f-145">`<Event Hub-compatible endpoint>` 및 `<Primary key>`를 앞에서 기록해 둔 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-145">Replace `<Event Hub-compatible endpoint>` and `<Primary key>` with the values that you noted earlier.</span></span>

### <a name="create-a-consumer-group-for-your-iot-hub"></a><span data-ttu-id="6b97f-146">IoT Hub에 대한 소비자 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="6b97f-146">Create a consumer group for your IoT hub</span></span>

1. <span data-ttu-id="6b97f-147">IoT Hub를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-147">Open your IoT hub.</span></span>

2. <span data-ttu-id="6b97f-148">**IoT Hub** 창에서 **메시지** 아래에 있는 **끝점**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-148">In the **IoT Hub** pane, under **Messaging**, click **Endpoints**.</span></span>

3. <span data-ttu-id="6b97f-149">오른쪽 창에서 **기본 제공 끝점** 아래에 있는 **이벤트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-149">In the right pane, under **Built-in endpoints**, click **Events**.</span></span>

4. <span data-ttu-id="6b97f-150">**속성** 창의 **소비자 그룹** 아래에서 이름을 입력하고 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-150">In the **Properties** pane, under **Consumer groups**, enter a name, and then make a note of it.</span></span>

5. <span data-ttu-id="6b97f-151">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-151">Click **Save**.</span></span>

## <a name="create-and-deploy-an-azure-function-app"></a><span data-ttu-id="6b97f-152">Azure 함수 앱 만들기 및 배포</span><span class="sxs-lookup"><span data-stu-id="6b97f-152">Create and deploy an Azure function app</span></span>

1. <span data-ttu-id="6b97f-153">[Azure Portal](https://portal.azure.com/)에서 **새로 만들기** > **계산** > **함수 앱** > **만들기**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-153">In the [Azure portal](https://portal.azure.com/), click **New** > **Compute** > **Function App** > **Create**.</span></span>

2. <span data-ttu-id="6b97f-154">함수 앱에 필요한 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-154">Enter the necessary information for the function app.</span></span>

   ![Azure Portal에서 함수 앱 만들기](media\iot-hub-store-data-in-azure-table-storage\3_azure-portal-create-function-app.png)

   * <span data-ttu-id="6b97f-156">**앱 이름**: 함수 앱의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-156">**App name**: The name of the function app.</span></span> <span data-ttu-id="6b97f-157">이름은 전역적으로 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-157">The name must be globally unique.</span></span>

   * <span data-ttu-id="6b97f-158">**리소스 그룹**: IoT Hub에서 사용하는 것과 동일한 리소스 그룹을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-158">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   * <span data-ttu-id="6b97f-159">**저장소 계정**: 만든 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-159">**Storage Account**: The storage account that you created.</span></span>

   * <span data-ttu-id="6b97f-160">**대시보드에 고정**: 대시보드에서 함수 앱에 쉽게 액세스하려면 이 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-160">**Pin to dashboard**: Check this option for easy access to the function app from the dashboard.</span></span>

3. <span data-ttu-id="6b97f-161">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-161">Click **Create**.</span></span>

4. <span data-ttu-id="6b97f-162">만들어진 함수 앱을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-162">After the function app has been created, open it.</span></span>

5. <span data-ttu-id="6b97f-163">함수 앱에서 다음을 수행하여 새 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-163">In the function app, create a new function by doing the following:</span></span>

   <span data-ttu-id="6b97f-164">a.</span><span class="sxs-lookup"><span data-stu-id="6b97f-164">a.</span></span> <span data-ttu-id="6b97f-165">**새 함수**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-165">Click **New Function**.</span></span>

   <span data-ttu-id="6b97f-166">b.</span><span class="sxs-lookup"><span data-stu-id="6b97f-166">b.</span></span> <span data-ttu-id="6b97f-167">**언어**에서 **JavaScript**를 선택하고, **시나리오**에서 **데이터 처리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-167">Select **JavaScript** for **Language**, and **Data Processing** for **Scenario**.</span></span>

   <span data-ttu-id="6b97f-168">c.</span><span class="sxs-lookup"><span data-stu-id="6b97f-168">c.</span></span> <span data-ttu-id="6b97f-169">**이 함수 만들기**를 클릭한 다음, **새 함수**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-169">Click **Create this function**, and then click **New Function**.</span></span>

   <span data-ttu-id="6b97f-170">d.</span><span class="sxs-lookup"><span data-stu-id="6b97f-170">d.</span></span> <span data-ttu-id="6b97f-171">언어에서 **JavaScript**를, 시나리오에서 **데이터 처리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-171">Select **JavaScript** for the language, and **Data Processing** for the scenario.</span></span>

   <span data-ttu-id="6b97f-172">e.</span><span class="sxs-lookup"><span data-stu-id="6b97f-172">e.</span></span> <span data-ttu-id="6b97f-173">**EventHubTrigger-JavaScript** 템플릿을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-173">Click the **EventHubTrigger-JavaScript** template.</span></span>

   <span data-ttu-id="6b97f-174">f.</span><span class="sxs-lookup"><span data-stu-id="6b97f-174">f.</span></span> <span data-ttu-id="6b97f-175">템플릿에 필요한 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-175">Enter the necessary information for the template.</span></span>

      * <span data-ttu-id="6b97f-176">**함수 이름 지정**: 함수 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-176">**Name your function**: The name of the function.</span></span>

      * <span data-ttu-id="6b97f-177">**Event Hub 이름**: 기록해 둔 Event Hub 호환 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-177">**Event Hub name**: The event hub-compatible name that you noted earlier.</span></span>

      * <span data-ttu-id="6b97f-178">**Event Hub 연결**: 만든 IoT Hub 끝점의 연결 문자열을 추가하려면 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-178">**Event Hub connection**: To add the connection string of the IoT hub endpoint that you created, click **New**.</span></span>

   <span data-ttu-id="6b97f-179">g.</span><span class="sxs-lookup"><span data-stu-id="6b97f-179">g.</span></span> <span data-ttu-id="6b97f-180">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-180">Click **Create**.</span></span>

6. <span data-ttu-id="6b97f-181">다음을 수행하여 함수의 출력을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-181">Configure an output of the function by doing the following:</span></span>

   <span data-ttu-id="6b97f-182">a.</span><span class="sxs-lookup"><span data-stu-id="6b97f-182">a.</span></span> <span data-ttu-id="6b97f-183">**통합** > **새 출력** > **Azure Table Storage** > **선택**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-183">Click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span></span>

      ![Azure Portal에서 함수 앱에 Table Storage 추가](media\iot-hub-store-data-in-azure-table-storage\4_azure-portal-function-app-add-output-table-storage.png)

   <span data-ttu-id="6b97f-185">b.</span><span class="sxs-lookup"><span data-stu-id="6b97f-185">b.</span></span> <span data-ttu-id="6b97f-186">필요한 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-186">Enter the necessary information.</span></span>

      * <span data-ttu-id="6b97f-187">**테이블 매개 변수 이름**: `outputTable`을 사용합니다. 이 이름은 Azure 함수의 코드에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-187">**Table parameter name**: Use `outputTable`, which will be used in the Azure function's code.</span></span>
      
      * <span data-ttu-id="6b97f-188">**테이블 이름**: `deviceData`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-188">**Table name**: Use `deviceData`.</span></span>

      * <span data-ttu-id="6b97f-189">**저장소 계정 연결**: **새로 만들기**를 클릭하고 저장소 계정을 선택하거나 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-189">**Storage account connection**: Click **New**, and then select or enter your storage account.</span></span> <span data-ttu-id="6b97f-190">저장소 계정이 표시되지 않는 경우 [저장소 계정 요구 사항](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b97f-190">If the storage account is not displayed, see [Storage account requirements](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements).</span></span>
      
   <span data-ttu-id="6b97f-191">c.</span><span class="sxs-lookup"><span data-stu-id="6b97f-191">c.</span></span> <span data-ttu-id="6b97f-192">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-192">Click **Save**.</span></span>

7. <span data-ttu-id="6b97f-193">**트리거** 아래에서 **Azure Event Hub(eventHubMessages)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-193">Under **Triggers**, click **Azure Event Hub (eventHubMessages)**.</span></span>

8. <span data-ttu-id="6b97f-194">**Event Hub 소비자 그룹** 아래에서 만든 소비자 그룹의 이름을 입력한 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-194">Under **Event Hub consumer group**, enter the name of the consumer group that you created, and then click **Save**.</span></span>

9. <span data-ttu-id="6b97f-195">왼쪽에서 만든 함수를 클릭한 다음 오른쪽의 **파일 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-195">Click the function you've created on the left and then click **View Files** on the right.</span></span>

10. <span data-ttu-id="6b97f-196">`index.js`의 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-196">Replace the code in `index.js` with the following:</span></span>

   ```javascript
   'use strict';

   // This function is triggered each time a message is received in the IoT hub.
   // The message payload is persisted in an Azure storage table
 
   module.exports = function (context, iotHubMessage) {
    context.log('Message received: ' + JSON.stringify(iotHubMessage));
    var date = Date.now();
    var partitionKey = Math.floor(date / (24 * 60 * 60 * 1000)) + '';
    var rowKey = date + '';
    context.bindings.outputTable = {
     "partitionKey": partitionKey,
     "rowKey": rowKey,
     "message": JSON.stringify(iotHubMessage)
    };
    context.done();
   };
   ```

11. <span data-ttu-id="6b97f-197">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-197">Click **Save**.</span></span>

<span data-ttu-id="6b97f-198">이제 함수 앱을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-198">You have now created the function app.</span></span> <span data-ttu-id="6b97f-199">이 앱은 IoT Hub에서 받는 메시지를 Table Storage에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-199">It stores messages that your IoT hub receives in your table storage.</span></span>

> [!NOTE]
> <span data-ttu-id="6b97f-200">**실행** 단추를 사용하여 함수 앱을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-200">You can use the **Run** button to test the function app.</span></span> <span data-ttu-id="6b97f-201">**실행**을 클릭하면 테스트 메시지를 IoT Hub로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-201">When you click **Run**, the test message is sent to your IoT hub.</span></span> <span data-ttu-id="6b97f-202">메시지가 도착하면 함수 앱을 트리거하여 시작하고 Table Storage에 메시지를 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-202">The arrival of the message should trigger the function app to start and then save the message to your table storage.</span></span> <span data-ttu-id="6b97f-203">**로그** 창에서 프로세스의 세부 정보를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-203">The **Logs** pane records the details of the process.</span></span>

## <a name="verify-your-message-in-your-table-storage"></a><span data-ttu-id="6b97f-204">테이블 저장소에 있는 메시지 확인</span><span class="sxs-lookup"><span data-stu-id="6b97f-204">Verify your message in your table storage</span></span>

1. <span data-ttu-id="6b97f-205">장치에서 샘플 응용 프로그램을 실행하여 IoT Hub로 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-205">Run the sample application on your device to send messages to your IoT hub.</span></span>

2. <span data-ttu-id="6b97f-206">[Azure Storage 탐색기를 다운로드하고 설치](http://storageexplorer.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-206">[Download and install Azure Storage Explorer](http://storageexplorer.com/).</span></span>

3. <span data-ttu-id="6b97f-207">Storage 탐색기를 열고 **Azure 계정 추가** > **로그인**을 차례로 클릭한 다음 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-207">Open Storage Explorer, click **Add an Azure Account** > **Sign in**, and then sign in to your Azure account.</span></span>

4. <span data-ttu-id="6b97f-208">Azure 구독 > **저장소 계정** > 저장소 계정 > **테이블** > **deviceData**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-208">Click your Azure subscription > **Storage Accounts** > your storage account > **Tables** > **deviceData**.</span></span>

   <span data-ttu-id="6b97f-209">장치에서 IoT Hub로 보낸 메시지가 `deviceData` 테이블에 기록되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-209">You should see messages sent from your device to your IoT hub logged in the `deviceData` table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b97f-210">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6b97f-210">Next steps</span></span>

<span data-ttu-id="6b97f-211">Azure Storage 계정과 Azure 함수 앱을 만들어 IoT Hub에서 받는 메시지를 Table Storage에 저장하도록 했습니다.</span><span class="sxs-lookup"><span data-stu-id="6b97f-211">You’ve successfully created your Azure storage account and Azure function app, which stores messages that your IoT hub receives in your table storage.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
