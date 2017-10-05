---
title: "Azure IoT Hub에서 센서 데이터의 실시간 데이터 시각화 – Web Apps | Microsoft Docs"
description: "Microsoft Azure App Service의 Web Apps 기능을 사용하여 센서에서 수집하여 IoT Hub로 보낸 온도 및 습도 데이터를 시각화할 수 있습니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "실시간 데이터 시각화, 라이브 데이터 시각화, 센서 데이터 시각화"
ms.assetid: e42b07a8-ddd4-476e-9bfb-903d6b033e91
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: e037f5c29cabf8e5d0d3e7ded187280a0652d5c3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="visualize-real-time-sensor-data-from-your-azure-iot-hub-by-using-the-web-apps-feature-of-azure-app-service"></a><span data-ttu-id="e6e60-104">Azure App Service의 Web Apps 기능을 사용하여 Azure IoT Hub에서 실시간 센서 데이터 시각화</span><span class="sxs-lookup"><span data-stu-id="e6e60-104">Visualize real-time sensor data from your Azure IoT hub by using the Web Apps feature of Azure App Service</span></span>

![종단 간 다이어그램](media/iot-hub-get-started-e2e-diagram/5.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="e6e60-106">학습 내용</span><span class="sxs-lookup"><span data-stu-id="e6e60-106">What you learn</span></span>

<span data-ttu-id="e6e60-107">이 자습서에서는 웹앱에서 호스팅되는 웹 응용 프로그램을 실행하여 IoT Hub에서 받는 실시간 센서 데이터를 시각화하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e6e60-107">In this tutorial, you learn how to visualize real-time sensor data that your IoT hub receives by running a web application that is hosted on a web app.</span></span> <span data-ttu-id="e6e60-108">Power BI를 사용하여 IoT Hub의 데이터를 시각화하려면 [Power BI를 사용하여 Azure IoT Hub에서 실시간 센서 데이터 시각화](iot-hub-live-data-visualization-in-power-bi.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6e60-108">If you want to try to visualize the data in your IoT hub by using Power BI, see [Use Power BI to visualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-power-bi.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="e6e60-109">수행할 작업</span><span class="sxs-lookup"><span data-stu-id="e6e60-109">What you do</span></span>

- <span data-ttu-id="e6e60-110">Azure Portal에서 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="e6e60-110">Create a web app in the Azure portal.</span></span>
- <span data-ttu-id="e6e60-111">소비자 그룹을 추가하여 IoT Hub에서 데이터 액세스 준비</span><span class="sxs-lookup"><span data-stu-id="e6e60-111">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="e6e60-112">IoT Hub에서 센서 데이터를 읽도록 웹앱 구성</span><span class="sxs-lookup"><span data-stu-id="e6e60-112">Configure the web app to read sensor data from your IoT hub.</span></span>
- <span data-ttu-id="e6e60-113">웹앱에서 호스팅할 웹 응용 프로그램 업로드</span><span class="sxs-lookup"><span data-stu-id="e6e60-113">Upload a web application to be hosted by the web app.</span></span>
- <span data-ttu-id="e6e60-114">웹앱을 열어 IoT Hub에서 실시간 온도 및 습도 데이터 확인</span><span class="sxs-lookup"><span data-stu-id="e6e60-114">Open the web app to see real-time temperature and humidity data from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e6e60-115">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="e6e60-115">What you need</span></span>

- <span data-ttu-id="e6e60-116">다음 요구 사항을 다루는 [장치 설정](iot-hub-raspberry-pi-kit-node-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="e6e60-116">[Set up your device](iot-hub-raspberry-pi-kit-node-get-started.md), which covers the following requirements:</span></span>
  - <span data-ttu-id="e6e60-117">활성 Azure 구독</span><span class="sxs-lookup"><span data-stu-id="e6e60-117">An active Azure subscription</span></span>
  - <span data-ttu-id="e6e60-118">구독 중인 IoT Hub</span><span class="sxs-lookup"><span data-stu-id="e6e60-118">An Iot hub under your subscription</span></span>
  - <span data-ttu-id="e6e60-119">메시지를 IoT Hub로 보내는 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="e6e60-119">A client application that sends messages to your Iot hub</span></span>
- [<span data-ttu-id="e6e60-120">Git 다운로드</span><span class="sxs-lookup"><span data-stu-id="e6e60-120">Download Git</span></span>](https://www.git-scm.com/downloads)

## <a name="create-a-web-app"></a><span data-ttu-id="e6e60-121">웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="e6e60-121">Create a web app</span></span>

1. <span data-ttu-id="e6e60-122">[Azure Portal](https://ms.portal.azure.com/)에서 **새로 만들기** > **웹 + 모바일** > **웹앱**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e6e60-122">In the [Azure portal](https://ms.portal.azure.com/), click **New** > **Web + Mobile** > **Web App**.</span></span>
2. <span data-ttu-id="e6e60-123">고유한 작업 이름을 입력하고, 구독을 확인하며, 리소스 그룹 및 위치를 지정하고, **대시보드에 고정**을 선택한 다음, **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e6e60-123">Enter a unique job name, verify the subscription, specify a resource group and a location, select **Pin to dashboard**, and then click **Create**.</span></span>

   <span data-ttu-id="e6e60-124">리소스 그룹과 동일한 위치를 선택하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e6e60-124">We recommend that you select the same location as that of your resource group.</span></span> <span data-ttu-id="e6e60-125">이렇게 하면 데이터 전송 속도를 높이고 비용을 절감할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6e60-125">Doing so assists with processing speed and reduces the cost of data transfer.</span></span>

   ![웹앱 만들기](media/iot-hub-live-data-visualization-in-web-apps/2_create-web-app-azure.png)

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="configure-the-web-app-to-read-data-from-your-iot-hub"></a><span data-ttu-id="e6e60-127">IoT Hub에서 데이터를 읽도록 웹앱 구성</span><span class="sxs-lookup"><span data-stu-id="e6e60-127">Configure the web app to read data from your IoT hub</span></span>

1. <span data-ttu-id="e6e60-128">방금 프로비전한 웹앱을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e6e60-128">Open the web app you’ve just provisioned.</span></span>
2. <span data-ttu-id="e6e60-129">**응용 프로그램 설정**을 클릭한 다음 **앱 설정** 아래에서 다음 키/값 쌍을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e6e60-129">Click **Application settings**, and then, under **App settings**, add the following key/value pairs:</span></span>

   | <span data-ttu-id="e6e60-130">키</span><span class="sxs-lookup"><span data-stu-id="e6e60-130">Key</span></span>                                   | <span data-ttu-id="e6e60-131">값</span><span class="sxs-lookup"><span data-stu-id="e6e60-131">Value</span></span>                                                        |
   |---------------------------------------|--------------------------------------------------------------|
   | <span data-ttu-id="e6e60-132">Azure.IoT.IoTHub.ConnectionString</span><span class="sxs-lookup"><span data-stu-id="e6e60-132">Azure.IoT.IoTHub.ConnectionString</span></span>     | <span data-ttu-id="e6e60-133">iothub-explorer에서 얻음</span><span class="sxs-lookup"><span data-stu-id="e6e60-133">Obtained from iothub-explorer</span></span>                                |
   | <span data-ttu-id="e6e60-134">Azure.IoT.IoTHub.ConsumerGroup</span><span class="sxs-lookup"><span data-stu-id="e6e60-134">Azure.IoT.IoTHub.ConsumerGroup</span></span>        | <span data-ttu-id="e6e60-135">IoT Hub에 추가하는 소비자 그룹의 이름</span><span class="sxs-lookup"><span data-stu-id="e6e60-135">The name of the consumer group that you add to your IoT hub</span></span>  |

   ![키/값 쌍을 사용하여 Azure 웹앱에 설정 추가](media/iot-hub-live-data-visualization-in-web-apps/4_web-app-settings-key-value-azure.png)

3. <span data-ttu-id="e6e60-137">**응용 프로그램 설정**을 클릭하고 **일반 설정**에서 **웹 소켓** 옵션을 설정/해제한 후 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e6e60-137">Click **Application settings**, under **General settings**, toggle the **Web sockets** option, and then click **Save**.</span></span>

   ![웹 소켓 옵션 설정/해제](media/iot-hub-live-data-visualization-in-web-apps/10_toggle_web_sockets.png)

## <a name="upload-a-web-application-to-be-hosted-by-the-web-app"></a><span data-ttu-id="e6e60-139">웹앱에서 호스팅할 웹 응용 프로그램 업로드</span><span class="sxs-lookup"><span data-stu-id="e6e60-139">Upload a web application to be hosted by the web app</span></span>

<span data-ttu-id="e6e60-140">GitHub에서 IoT Hub의 실시간 센서 데이터를 표시하는 웹 응용 프로그램을 사용할 수 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="e6e60-140">On GitHub, we've made available a web application that displays real-time sensor data from your IoT hub.</span></span> <span data-ttu-id="e6e60-141">Git 리포지토리에서 작동하도록 웹앱을 구성하고, GitHub에서 웹 응용 프로그램을 다운로드하고, Azure에 업로드하여 웹앱에서 호스트하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6e60-141">All you need to do is configure the web app to work with a Git repository, download the web application from GitHub, and then upload it to Azure for the web app to host.</span></span>

1. <span data-ttu-id="e6e60-142">웹앱에서 **배포 옵션** > **원본 선택** > **로컬 Git 리포지토리**를 차례로 클릭한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e6e60-142">In the web app, click **Deployment Options** > **Choose Source** > **Local Git Repository**, and then click **OK**.</span></span>

   ![로컬 Git 리포지토리를 사용하도록 웹앱 배포 구성](media/iot-hub-live-data-visualization-in-web-apps/5_configure-web-app-deployment-local-git-repository-azure.png)

2. <span data-ttu-id="e6e60-144">**배포 자격 증명**을 클릭하고 Azure에서 Git 리포지토리에 연결하는 데 사용할 사용자 이름과 암호를 만든 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e6e60-144">Click **Deployment Credentials**, create a user name and password to use to connect to the Git repository in Azure, and then click **Save**.</span></span>

3. <span data-ttu-id="e6e60-145">**개요**를 클릭하고 **Git 복제 URL** 값을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="e6e60-145">Click **Overview**, and note the value of **Git clone url**.</span></span>

   ![웹앱의 Git Clone URL 가져오기](media/iot-hub-live-data-visualization-in-web-apps/7_web-app-git-clone-url-azure.png)

4. <span data-ttu-id="e6e60-147">로컬 컴퓨터에서 명령 창 또는 터미널 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e6e60-147">Open a command or terminal window on your local computer.</span></span>

5. <span data-ttu-id="e6e60-148">GitHub에서 웹앱을 다운로드하고, Azure를 업로드하여 웹앱을 호스팅합니다.</span><span class="sxs-lookup"><span data-stu-id="e6e60-148">Download the web app from GitHub, and upload it to Azure for the web app to host.</span></span> <span data-ttu-id="e6e60-149">이렇게 하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e6e60-149">To do so, run the following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/web-apps-node-iot-hub-data-visualization.git
   cd web-apps-node-iot-hub-data-visualization
   git remote add webapp <Git clone URL>
   git push webapp master:master
   ```

   > [!NOTE]
   > <span data-ttu-id="e6e60-150">\<Git 복제 URL\>은 웹앱의 **개요** 페이지에서 있는 Git 리포지토리의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="e6e60-150">\<Git clone URL\> is the URL of the Git repository found on the **Overview** page of the web app.</span></span>

## <a name="open-the-web-app-to-see-real-time-temperature-and-humidity-data-from-your-iot-hub"></a><span data-ttu-id="e6e60-151">웹앱을 열어 IoT Hub에서 실시간 온도 및 습도 데이터 확인</span><span class="sxs-lookup"><span data-stu-id="e6e60-151">Open the web app to see real-time temperature and humidity data from your IoT hub</span></span>

<span data-ttu-id="e6e60-152">웹앱의 **개요** 페이지에서 URL을 클릭하여 웹앱을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e6e60-152">On the **Overview** page of your web app, click the URL to open the web app.</span></span>

![웹앱의 URL 가져오기](media/iot-hub-live-data-visualization-in-web-apps/8_web-app-url-azure.png)

<span data-ttu-id="e6e60-154">IoT Hub에서 실시간 온도 및 습도 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6e60-154">You should see the real-time temperature and humidity data from your IoT hub.</span></span>

![실시간 온도 및 습도를 보여 주는 웹앱 페이지](media/iot-hub-live-data-visualization-in-web-apps/9_web-app-page-show-real-time-temperature-humidity-azure.png)

> [!NOTE]
> <span data-ttu-id="e6e60-156">응용 프로그램 예제가 사용자 장치에서 실행 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e6e60-156">Ensure the sample application is running on your device.</span></span> <span data-ttu-id="e6e60-157">그렇지 않은 경우 빈 차트를 받습니다. [사용자 장치 설정](iot-hub-raspberry-pi-kit-node-get-started.md)에 있는 자습서를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6e60-157">If not, you will get a blank chart, you can refer to the tutorials under [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6e60-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e6e60-158">Next steps</span></span>
<span data-ttu-id="e6e60-159">웹앱을 사용하여 IoT Hub에서 실시간 센서 데이터를 시각화했습니다.</span><span class="sxs-lookup"><span data-stu-id="e6e60-159">You've successfully used your web app to visualize real-time sensor data from your IoT hub.</span></span>

<span data-ttu-id="e6e60-160">Azure IoT Hub에서 데이터를 시각화하는 다른 방법은 [Power BI를 사용하여 IoT Hub에서 실시간 센서 데이터 시각화](iot-hub-live-data-visualization-in-power-bi.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6e60-160">For an alternative way to visualize data from Azure IoT Hub, see [Use Power BI to visualize real-time sensor data from your IoT hub](iot-hub-live-data-visualization-in-power-bi.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
