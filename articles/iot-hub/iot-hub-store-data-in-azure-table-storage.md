---
title: "aaaSave IoT hub tooAzure 데이터 저장소를 메시지 | Microsoft Docs"
description: "Azure 함수 앱 toosave IoT 허브 메시지 tooyour Azure 테이블 저장소를 사용 합니다. hello IoT 허브 메시지 IoT 장치에서 전송 된 센서 데이터가 같은 정보를 포함 합니다."
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
ms.openlocfilehash: be72d9ba9a781822926364351b50f58f5d96e94a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="save-iot-hub-messages-that-contain-sensor-data-tooyour-azure-table-storage"></a><span data-ttu-id="363d7-105">센서 데이터 tooyour Azure 테이블 저장소를 포함 하는 IoT 허브 메시지 저장</span><span class="sxs-lookup"><span data-stu-id="363d7-105">Save IoT hub messages that contain sensor data tooyour Azure table storage</span></span>

![종단 간 다이어그램](media/iot-hub-get-started-e2e-diagram/3.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="363d7-107">학습 내용</span><span class="sxs-lookup"><span data-stu-id="363d7-107">What you learn</span></span>

<span data-ttu-id="363d7-108">어떻게 toocreate Azure 저장소 계정 및 Azure 테이블 저장소에 앱 toostore IoT 허브 메시지 작동 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-108">You learn how toocreate an Azure storage account and an Azure function app toostore IoT hub messages in your table storage.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="363d7-109">수행할 작업</span><span class="sxs-lookup"><span data-stu-id="363d7-109">What you do</span></span>

- <span data-ttu-id="363d7-110">Azure 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="363d7-110">Create an Azure storage account.</span></span>
- <span data-ttu-id="363d7-111">연결 tooread 메시지가 IoT hub를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-111">Prepare your IoT hub connection tooread messages.</span></span>
- <span data-ttu-id="363d7-112">Azure 함수 앱 만들기 및 배포</span><span class="sxs-lookup"><span data-stu-id="363d7-112">Create and deploy an Azure function app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="363d7-113">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="363d7-113">What you need</span></span>

- <span data-ttu-id="363d7-114">[장치 설정](iot-hub-raspberry-pi-kit-node-get-started.md) toocover hello 요구 사항:</span><span class="sxs-lookup"><span data-stu-id="363d7-114">[Set up your device](iot-hub-raspberry-pi-kit-node-get-started.md) toocover hello following requirements:</span></span>
  - <span data-ttu-id="363d7-115">활성 Azure 구독</span><span class="sxs-lookup"><span data-stu-id="363d7-115">An active Azure subscription</span></span>
  - <span data-ttu-id="363d7-116">구독 중인 IoT Hub</span><span class="sxs-lookup"><span data-stu-id="363d7-116">An IoT hub under your subscription</span></span> 
  - <span data-ttu-id="363d7-117">메시지 tooyour IoT 허브에서 전송 하는 실행 중인 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="363d7-117">A running application that sends messages tooyour IoT hub</span></span>

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="363d7-118">Azure 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="363d7-118">Create an Azure storage account</span></span>

1. <span data-ttu-id="363d7-119">Hello에 [Azure 포털](https://portal.azure.com/), 클릭 **새로** > **저장소** > **저장소 계정**  >   **만들**합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-119">In hello [Azure portal](https://portal.azure.com/), click **New** > **Storage** > **Storage account** > **Create**.</span></span>

2. <span data-ttu-id="363d7-120">Hello hello 저장소 계정에 대 한 필요한 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-120">Enter hello necessary information for hello storage account:</span></span>

   ![Hello Azure 포털에서에서 저장소 계정 만들기](media\iot-hub-store-data-in-azure-table-storage\1_azure-portal-create-storage-account.png)

   * <span data-ttu-id="363d7-122">**이름**: hello hello 저장소 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-122">**Name**: hello name of hello storage account.</span></span> <span data-ttu-id="363d7-123">hello 이름은 전역적으로 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-123">hello name must be globally unique.</span></span>

   * <span data-ttu-id="363d7-124">**리소스 그룹**: 동일 사용 하 여 hello IoT 허브를 사용 하는 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-124">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   * <span data-ttu-id="363d7-125">**Pin toodashboard**: hello 대시보드에서 쉽게 액세스할 수 있도록 tooyour IoT 허브에 대 한이 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-125">**Pin toodashboard**: Select this option for easy access tooyour IoT hub from hello dashboard.</span></span>

3. <span data-ttu-id="363d7-126">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-126">Click **Create**.</span></span>

## <a name="prepare-your-iot-hub-connection-tooread-messages"></a><span data-ttu-id="363d7-127">연결 tooread 메시지가 IoT hub를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-127">Prepare your IoT hub connection tooread messages</span></span>

<span data-ttu-id="363d7-128">IoT 허브는 기본 제공 이벤트 허브 호환 끝점 tooenable 응용 프로그램 tooread IoT 허브 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-128">IoT hub exposes a built-in event hub-compatible endpoint tooenable applications tooread IoT hub messages.</span></span> <span data-ttu-id="363d7-129">한편, 응용 프로그램에서 IoT hub 소비자 그룹 tooread 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-129">Meanwhile, applications use consumer groups tooread data from your IoT hub.</span></span> <span data-ttu-id="363d7-130">IoT hub에서 Azure 함수 앱 tooread 데이터를 만들기 전에 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-130">Before you create an Azure function app tooread data from your IoT hub, do hello following:</span></span>

- <span data-ttu-id="363d7-131">IoT hub 끝점의 hello 연결 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-131">Get hello connection string of your IoT hub endpoint.</span></span>
- <span data-ttu-id="363d7-132">IoT Hub에 대한 소비자 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="363d7-132">Create a consumer group for your IoT hub.</span></span>

### <a name="get-hello-connection-string-of-your-iot-hub-endpoint"></a><span data-ttu-id="363d7-133">IoT hub 끝점의 hello 연결 문자열 가져오기</span><span class="sxs-lookup"><span data-stu-id="363d7-133">Get hello connection string of your IoT hub endpoint</span></span>

1. <span data-ttu-id="363d7-134">IoT Hub를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-134">Open your IoT hub.</span></span>

2. <span data-ttu-id="363d7-135">Hello에 **IoT Hub** 창 아래에서 **메시징**, 클릭 **끝점**합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-135">On hello **IoT Hub** pane, under **Messaging**, click **Endpoints**.</span></span>

3. <span data-ttu-id="363d7-136">Hello에서 마우스 오른쪽 단추로 창 아래에서 **기본 제공 끝점**, 클릭 **이벤트**합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-136">In hello right pane, under **Built-in endpoints**, click **Events**.</span></span>

4. <span data-ttu-id="363d7-137">Hello에 **속성** 창에서 다음 값에 참고 hello:</span><span class="sxs-lookup"><span data-stu-id="363d7-137">In hello **Properties** pane, note hello following values:</span></span>
   - <span data-ttu-id="363d7-138">Event Hub 호환 끝점</span><span class="sxs-lookup"><span data-stu-id="363d7-138">Event hub-compatible endpoint</span></span>
   - <span data-ttu-id="363d7-139">Event Hub 호환 이름</span><span class="sxs-lookup"><span data-stu-id="363d7-139">Event hub-compatible name</span></span>

   ![IoT hub 끝점의 연결 문자열 hello hello Azure 포털에서 가져오기](media\iot-hub-store-data-in-azure-table-storage\2_azure-portal-iot-hub-endpoint-connection-string.png)

5. <span data-ttu-id="363d7-141">Hello에 **IoT Hub** 창 아래에서 **설정**, 클릭 **공유 액세스 정책을**합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-141">In hello **IoT Hub** pane, under **Settings**, click **Shared access policies**.</span></span>

6. <span data-ttu-id="363d7-142">**iothubowner**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-142">Click **iothubowner**.</span></span>

7. <span data-ttu-id="363d7-143">참고 hello **기본 키** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-143">Note hello **Primary key** value.</span></span>

8. <span data-ttu-id="363d7-144">IoT hub 끝점의 hello 연결 문자열을 다음과 같이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-144">Create hello connection string of your IoT hub endpoint as follows:</span></span>

   `Endpoint=<Event Hub-compatible endpoint>;SharedAccessKeyName=iothubowner;SharedAccessKey=<Primary key>`

   > [!NOTE]
   > <span data-ttu-id="363d7-145">대체 `<Event Hub-compatible endpoint>` 및 `<Primary key>` hello 값이 앞에서 설명한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-145">Replace `<Event Hub-compatible endpoint>` and `<Primary key>` with hello values that you noted earlier.</span></span>

### <a name="create-a-consumer-group-for-your-iot-hub"></a><span data-ttu-id="363d7-146">IoT Hub에 대한 소비자 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="363d7-146">Create a consumer group for your IoT hub</span></span>

1. <span data-ttu-id="363d7-147">IoT Hub를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-147">Open your IoT hub.</span></span>

2. <span data-ttu-id="363d7-148">Hello에 **IoT Hub** 창 아래에서 **메시징**, 클릭 **끝점**합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-148">In hello **IoT Hub** pane, under **Messaging**, click **Endpoints**.</span></span>

3. <span data-ttu-id="363d7-149">Hello에서 마우스 오른쪽 단추로 창 아래에서 **기본 제공 끝점**, 클릭 **이벤트**합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-149">In hello right pane, under **Built-in endpoints**, click **Events**.</span></span>

4. <span data-ttu-id="363d7-150">Hello에 **속성** 창 아래에서 **소비자 그룹**는 이름을 입력 한 다음 확인을 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-150">In hello **Properties** pane, under **Consumer groups**, enter a name, and then make a note of it.</span></span>

5. <span data-ttu-id="363d7-151">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-151">Click **Save**.</span></span>

## <a name="create-and-deploy-an-azure-function-app"></a><span data-ttu-id="363d7-152">Azure 함수 앱 만들기 및 배포</span><span class="sxs-lookup"><span data-stu-id="363d7-152">Create and deploy an Azure function app</span></span>

1. <span data-ttu-id="363d7-153">Hello에 [Azure 포털](https://portal.azure.com/), 클릭 **새로** > **계산** > **함수 앱**  >   **만들**합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-153">In hello [Azure portal](https://portal.azure.com/), click **New** > **Compute** > **Function App** > **Create**.</span></span>

2. <span data-ttu-id="363d7-154">Hello hello 함수 앱에 대 한 필요한 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-154">Enter hello necessary information for hello function app.</span></span>

   ![Hello Azure 포털에서에서 함수 앱 만들기](media\iot-hub-store-data-in-azure-table-storage\3_azure-portal-create-function-app.png)

   * <span data-ttu-id="363d7-156">**응용 프로그램 이름**: hello 이름 hello 함수 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-156">**App name**: hello name of hello function app.</span></span> <span data-ttu-id="363d7-157">hello 이름은 전역적으로 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-157">hello name must be globally unique.</span></span>

   * <span data-ttu-id="363d7-158">**리소스 그룹**: 동일 사용 하 여 hello IoT 허브를 사용 하는 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-158">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   * <span data-ttu-id="363d7-159">**저장소 계정**: hello 만든 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-159">**Storage Account**: hello storage account that you created.</span></span>

   * <span data-ttu-id="363d7-160">**Pin toodashboard**: hello 대시보드에서 쉽게 액세스할 수 있도록 toohello 함수 앱에 대 한이 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-160">**Pin toodashboard**: Check this option for easy access toohello function app from hello dashboard.</span></span>

3. <span data-ttu-id="363d7-161">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-161">Click **Create**.</span></span>

4. <span data-ttu-id="363d7-162">Hello 함수 앱을 만든 후이 엽니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-162">After hello function app has been created, open it.</span></span>

5. <span data-ttu-id="363d7-163">Hello 함수 응용 프로그램에서 hello 다음을 수행 하 여 새 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-163">In hello function app, create a new function by doing hello following:</span></span>

   <span data-ttu-id="363d7-164">a.</span><span class="sxs-lookup"><span data-stu-id="363d7-164">a.</span></span> <span data-ttu-id="363d7-165">**새 함수**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-165">Click **New Function**.</span></span>

   <span data-ttu-id="363d7-166">b.</span><span class="sxs-lookup"><span data-stu-id="363d7-166">b.</span></span> <span data-ttu-id="363d7-167">**언어**에서 **JavaScript**를 선택하고, **시나리오**에서 **데이터 처리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-167">Select **JavaScript** for **Language**, and **Data Processing** for **Scenario**.</span></span>

   <span data-ttu-id="363d7-168">c.</span><span class="sxs-lookup"><span data-stu-id="363d7-168">c.</span></span> <span data-ttu-id="363d7-169">**이 함수 만들기**를 클릭한 다음, **새 함수**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-169">Click **Create this function**, and then click **New Function**.</span></span>

   <span data-ttu-id="363d7-170">d.</span><span class="sxs-lookup"><span data-stu-id="363d7-170">d.</span></span> <span data-ttu-id="363d7-171">선택 **JavaScript** hello 언어에 대 한 및 **데이터 처리** hello 시나리오에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-171">Select **JavaScript** for hello language, and **Data Processing** for hello scenario.</span></span>

   <span data-ttu-id="363d7-172">e.</span><span class="sxs-lookup"><span data-stu-id="363d7-172">e.</span></span> <span data-ttu-id="363d7-173">Hello 클릭 **EventHubTrigger JavaScript** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="363d7-173">Click hello **EventHubTrigger-JavaScript** template.</span></span>

   <span data-ttu-id="363d7-174">f.</span><span class="sxs-lookup"><span data-stu-id="363d7-174">f.</span></span> <span data-ttu-id="363d7-175">Hello hello 서식 파일에 대 한 필요한 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-175">Enter hello necessary information for hello template.</span></span>

      * <span data-ttu-id="363d7-176">**함수 이름을**: hello hello 함수의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-176">**Name your function**: hello name of hello function.</span></span>

      * <span data-ttu-id="363d7-177">**이벤트 허브 이름**: hello 이벤트 허브 호환 이름 앞에서 설명한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-177">**Event Hub name**: hello event hub-compatible name that you noted earlier.</span></span>

      * <span data-ttu-id="363d7-178">**이벤트 허브 연결**: 사용자가 만든 hello IoT hub 끝점의 tooadd hello 연결 문자열 클릭 **새로**합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-178">**Event Hub connection**: tooadd hello connection string of hello IoT hub endpoint that you created, click **New**.</span></span>

   <span data-ttu-id="363d7-179">g.</span><span class="sxs-lookup"><span data-stu-id="363d7-179">g.</span></span> <span data-ttu-id="363d7-180">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-180">Click **Create**.</span></span>

6. <span data-ttu-id="363d7-181">Hello 다음을 수행 하 여 hello 함수의 출력을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-181">Configure an output of hello function by doing hello following:</span></span>

   <span data-ttu-id="363d7-182">a.</span><span class="sxs-lookup"><span data-stu-id="363d7-182">a.</span></span> <span data-ttu-id="363d7-183">**통합** > **새 출력** > **Azure Table Storage** > **선택**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-183">Click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span></span>

      ![테이블 저장소 tooyour 함수 앱 hello Azure 포털에 추가](media\iot-hub-store-data-in-azure-table-storage\4_azure-portal-function-app-add-output-table-storage.png)

   <span data-ttu-id="363d7-185">b.</span><span class="sxs-lookup"><span data-stu-id="363d7-185">b.</span></span> <span data-ttu-id="363d7-186">Hello 필요한 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-186">Enter hello necessary information.</span></span>

      * <span data-ttu-id="363d7-187">**테이블 매개 변수 이름**: 사용 `outputTable`, Azure hello에 사용 되는 함수의 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-187">**Table parameter name**: Use `outputTable`, which will be used in hello Azure function's code.</span></span>
      
      * <span data-ttu-id="363d7-188">**테이블 이름**: `deviceData`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-188">**Table name**: Use `deviceData`.</span></span>

      * <span data-ttu-id="363d7-189">**저장소 계정 연결**: **새로 만들기**를 클릭하고 저장소 계정을 선택하거나 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-189">**Storage account connection**: Click **New**, and then select or enter your storage account.</span></span> <span data-ttu-id="363d7-190">Hello 저장소 계정이 표시 되지 않으면 참조 [저장소 계정 요구 사항](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements)합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-190">If hello storage account is not displayed, see [Storage account requirements](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements).</span></span>
      
   <span data-ttu-id="363d7-191">c.</span><span class="sxs-lookup"><span data-stu-id="363d7-191">c.</span></span> <span data-ttu-id="363d7-192">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-192">Click **Save**.</span></span>

7. <span data-ttu-id="363d7-193">**트리거** 아래에서 **Azure Event Hub(eventHubMessages)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-193">Under **Triggers**, click **Azure Event Hub (eventHubMessages)**.</span></span>

8. <span data-ttu-id="363d7-194">아래 **이벤트 허브 소비자 그룹**를 생성 하 고 클릭 hello 소비자 그룹의 hello 이름을 입력 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-194">Under **Event Hub consumer group**, enter hello name of hello consumer group that you created, and then click **Save**.</span></span>

9. <span data-ttu-id="363d7-195">왼쪽 hello에 만든 hello 함수를 클릭 한 다음 클릭 **파일 보기** hello 오른쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-195">Click hello function you've created on hello left and then click **View Files** on hello right.</span></span>

10. <span data-ttu-id="363d7-196">hello 코드 `index.js` hello 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-196">Replace hello code in `index.js` with hello following:</span></span>

   ```javascript
   'use strict';

   // This function is triggered each time a message is received in hello IoT hub.
   // hello message payload is persisted in an Azure storage table
 
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

11. <span data-ttu-id="363d7-197">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-197">Click **Save**.</span></span>

<span data-ttu-id="363d7-198">이제 hello 함수 응용 프로그램을 작성 했습니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-198">You have now created hello function app.</span></span> <span data-ttu-id="363d7-199">이 앱은 IoT Hub에서 받는 메시지를 Table Storage에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-199">It stores messages that your IoT hub receives in your table storage.</span></span>

> [!NOTE]
> <span data-ttu-id="363d7-200">Hello를 사용할 수 있습니다 **실행** 단추 tootest hello 함수 앱.</span><span class="sxs-lookup"><span data-stu-id="363d7-200">You can use hello **Run** button tootest hello function app.</span></span> <span data-ttu-id="363d7-201">클릭할 때 **실행**, hello 테스트 메시지를 tooyour IoT 허브를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-201">When you click **Run**, hello test message is sent tooyour IoT hub.</span></span> <span data-ttu-id="363d7-202">hello 메시지의 도착 hello hello 함수 앱 toostart 트리거할 하 고 hello 메시지 tooyour 테이블 저장소를 저장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-202">hello arrival of hello message should trigger hello function app toostart and then save hello message tooyour table storage.</span></span> <span data-ttu-id="363d7-203">hello **로그** 창 hello 프로세스의 hello 세부 정보를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-203">hello **Logs** pane records hello details of hello process.</span></span>

## <a name="verify-your-message-in-your-table-storage"></a><span data-ttu-id="363d7-204">테이블 저장소에 있는 메시지 확인</span><span class="sxs-lookup"><span data-stu-id="363d7-204">Verify your message in your table storage</span></span>

1. <span data-ttu-id="363d7-205">장치 toosend 메시지 tooyour IoT 허브에서 hello 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-205">Run hello sample application on your device toosend messages tooyour IoT hub.</span></span>

2. <span data-ttu-id="363d7-206">[Azure Storage 탐색기를 다운로드하고 설치](http://storageexplorer.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-206">[Download and install Azure Storage Explorer](http://storageexplorer.com/).</span></span>

3. <span data-ttu-id="363d7-207">저장소 탐색기를 열고 **Azure 계정 추가** > **로그인**, tooyour Azure 계정에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-207">Open Storage Explorer, click **Add an Azure Account** > **Sign in**, and then sign in tooyour Azure account.</span></span>

4. <span data-ttu-id="363d7-208">Azure 구독 > **저장소 계정** > 저장소 계정 > **테이블** > **deviceData**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-208">Click your Azure subscription > **Storage Accounts** > your storage account > **Tables** > **deviceData**.</span></span>

   <span data-ttu-id="363d7-209">Hello에 기록 하 여 장치 tooyour IoT 허브에서 보낸 메시지를 표시 되어야 `deviceData` 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-209">You should see messages sent from your device tooyour IoT hub logged in hello `deviceData` table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="363d7-210">다음 단계</span><span class="sxs-lookup"><span data-stu-id="363d7-210">Next steps</span></span>

<span data-ttu-id="363d7-211">Azure Storage 계정과 Azure 함수 앱을 만들어 IoT Hub에서 받는 메시지를 Table Storage에 저장하도록 했습니다.</span><span class="sxs-lookup"><span data-stu-id="363d7-211">You’ve successfully created your Azure storage account and Azure function app, which stores messages that your IoT hub receives in your table storage.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
