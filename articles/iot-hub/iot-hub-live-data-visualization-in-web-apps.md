---
title: "웹 응용 프로그램 – 프로그램 Azure IoT 허브에서 센서 데이터의 타임 aaaReal 데이터 시각화 | Microsoft Docs"
description: "Microsoft Azure 앱 서비스 toovisualize 온도 및 습도 데이터의 hello 센서에서 수집 되 고 tooyour Iot 허브를 전송 하는 hello 웹 응용 프로그램 기능을 사용 합니다."
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
ms.openlocfilehash: 72f2dffee1c2f975948820eee9f2e287c3f77255
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-real-time-sensor-data-from-your-azure-iot-hub-by-using-hello-web-apps-feature-of-azure-app-service"></a><span data-ttu-id="93cb4-104">Azure 앱 서비스의 hello 웹 응용 프로그램 기능을 사용 하 여 Azure IoT 허브에서 실시간 센서 데이터 시각화</span><span class="sxs-lookup"><span data-stu-id="93cb4-104">Visualize real-time sensor data from your Azure IoT hub by using hello Web Apps feature of Azure App Service</span></span>

![종단 간 다이어그램](media/iot-hub-get-started-e2e-diagram/5.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="93cb4-106">학습 내용</span><span class="sxs-lookup"><span data-stu-id="93cb4-106">What you learn</span></span>

<span data-ttu-id="93cb4-107">이 자습서에서는 toovisualize 실시간 센서 데이터는 웹 응용 프로그램을 실행 하 여 IoT hub를 수신 하는 웹 응용 프로그램에서 호스트 되는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="93cb4-107">In this tutorial, you learn how toovisualize real-time sensor data that your IoT hub receives by running a web application that is hosted on a web app.</span></span> <span data-ttu-id="93cb4-108">Power BI를 사용 하 여 IoT 허브에서 tootry toovisualize hello 데이터를 원하는 경우 참조 [Azure IoT 허브에서 사용 하 여 Power BI toovisualize 실시간 센서 데이터](iot-hub-live-data-visualization-in-power-bi.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="93cb4-108">If you want tootry toovisualize hello data in your IoT hub by using Power BI, see [Use Power BI toovisualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-power-bi.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="93cb4-109">수행할 작업</span><span class="sxs-lookup"><span data-stu-id="93cb4-109">What you do</span></span>

- <span data-ttu-id="93cb4-110">Hello Azure 포털에서에서 웹 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="93cb4-110">Create a web app in hello Azure portal.</span></span>
- <span data-ttu-id="93cb4-111">소비자 그룹을 추가하여 IoT Hub에서 데이터 액세스 준비</span><span class="sxs-lookup"><span data-stu-id="93cb4-111">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="93cb4-112">IoT 허브에서 hello 웹 앱 tooread 센서 데이터를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="93cb4-112">Configure hello web app tooread sensor data from your IoT hub.</span></span>
- <span data-ttu-id="93cb4-113">Hello 웹 응용 프로그램에서 호스팅되는 웹 응용 프로그램 toobe를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="93cb4-113">Upload a web application toobe hosted by hello web app.</span></span>
- <span data-ttu-id="93cb4-114">IoT 허브에서 hello 웹 앱 toosee 실시간 온도 및 습도 데이터를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="93cb4-114">Open hello web app toosee real-time temperature and humidity data from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="93cb4-115">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="93cb4-115">What you need</span></span>

- <span data-ttu-id="93cb4-116">[장치 설정](iot-hub-raspberry-pi-kit-node-get-started.md)는 hello 요구 사항에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="93cb4-116">[Set up your device](iot-hub-raspberry-pi-kit-node-get-started.md), which covers hello following requirements:</span></span>
  - <span data-ttu-id="93cb4-117">활성 Azure 구독</span><span class="sxs-lookup"><span data-stu-id="93cb4-117">An active Azure subscription</span></span>
  - <span data-ttu-id="93cb4-118">구독 중인 IoT Hub</span><span class="sxs-lookup"><span data-stu-id="93cb4-118">An Iot hub under your subscription</span></span>
  - <span data-ttu-id="93cb4-119">메시지 tooyour Iot 허브에서 전송 하는 클라이언트 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="93cb4-119">A client application that sends messages tooyour Iot hub</span></span>
- [<span data-ttu-id="93cb4-120">Git 다운로드</span><span class="sxs-lookup"><span data-stu-id="93cb4-120">Download Git</span></span>](https://www.git-scm.com/downloads)

## <a name="create-a-web-app"></a><span data-ttu-id="93cb4-121">웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="93cb4-121">Create a web app</span></span>

1. <span data-ttu-id="93cb4-122">Hello에 [Azure 포털](https://ms.portal.azure.com/), 클릭 **새로** > **웹 + 모바일** > **웹 앱**합니다.</span><span class="sxs-lookup"><span data-stu-id="93cb4-122">In hello [Azure portal](https://ms.portal.azure.com/), click **New** > **Web + Mobile** > **Web App**.</span></span>
2. <span data-ttu-id="93cb4-123">고유한 작업 이름을 입력, hello 구독을 확인 하 고, 리소스 그룹 및 위치를 선택 지정한 **Pin toodashboard**, 클릭 하 고 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="93cb4-123">Enter a unique job name, verify hello subscription, specify a resource group and a location, select **Pin toodashboard**, and then click **Create**.</span></span>

   <span data-ttu-id="93cb4-124">Hello를 선택 하는 것이 좋습니다 리소스 그룹의 동일한 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="93cb4-124">We recommend that you select hello same location as that of your resource group.</span></span> <span data-ttu-id="93cb4-125">이렇게 속도 처리 하는 데 도움이 되 고 hello 데이터 전송 비용을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93cb4-125">Doing so assists with processing speed and reduces hello cost of data transfer.</span></span>

   ![웹앱 만들기](media/iot-hub-live-data-visualization-in-web-apps/2_create-web-app-azure.png)

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="configure-hello-web-app-tooread-data-from-your-iot-hub"></a><span data-ttu-id="93cb4-127">IoT 허브에서 hello 웹 앱 tooread 데이터 구성</span><span class="sxs-lookup"><span data-stu-id="93cb4-127">Configure hello web app tooread data from your IoT hub</span></span>

1. <span data-ttu-id="93cb4-128">방금 프로 비전 하는 hello web app을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="93cb4-128">Open hello web app you’ve just provisioned.</span></span>
2. <span data-ttu-id="93cb4-129">클릭 **응용 프로그램 설정**를 차례로 선택한 다음 **앱 설정**를 키/값 쌍을 다음 hello 추가:</span><span class="sxs-lookup"><span data-stu-id="93cb4-129">Click **Application settings**, and then, under **App settings**, add hello following key/value pairs:</span></span>

   | <span data-ttu-id="93cb4-130">키</span><span class="sxs-lookup"><span data-stu-id="93cb4-130">Key</span></span>                                   | <span data-ttu-id="93cb4-131">값</span><span class="sxs-lookup"><span data-stu-id="93cb4-131">Value</span></span>                                                        |
   |---------------------------------------|--------------------------------------------------------------|
   | <span data-ttu-id="93cb4-132">Azure.IoT.IoTHub.ConnectionString</span><span class="sxs-lookup"><span data-stu-id="93cb4-132">Azure.IoT.IoTHub.ConnectionString</span></span>     | <span data-ttu-id="93cb4-133">iothub-explorer에서 얻음</span><span class="sxs-lookup"><span data-stu-id="93cb4-133">Obtained from iothub-explorer</span></span>                                |
   | <span data-ttu-id="93cb4-134">Azure.IoT.IoTHub.ConsumerGroup</span><span class="sxs-lookup"><span data-stu-id="93cb4-134">Azure.IoT.IoTHub.ConsumerGroup</span></span>        | <span data-ttu-id="93cb4-135">tooyour IoT 허브를 추가 하는 hello 소비자 그룹의 hello 이름</span><span class="sxs-lookup"><span data-stu-id="93cb4-135">hello name of hello consumer group that you add tooyour IoT hub</span></span>  |

   ![키/값 쌍이 있는 tooyour 웹 앱 설정 추가](media/iot-hub-live-data-visualization-in-web-apps/4_web-app-settings-key-value-azure.png)

3. <span data-ttu-id="93cb4-137">클릭 **응용 프로그램 설정**아래 **일반 설정**, 토글 hello **웹 소켓** 옵션을 선택한 다음 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="93cb4-137">Click **Application settings**, under **General settings**, toggle hello **Web sockets** option, and then click **Save**.</span></span>

   ![Hello 웹 소켓 옵션을 설정/해제](media/iot-hub-live-data-visualization-in-web-apps/10_toggle_web_sockets.png)

## <a name="upload-a-web-application-toobe-hosted-by-hello-web-app"></a><span data-ttu-id="93cb4-139">Hello 웹 응용 프로그램에서 호스팅되는 웹 응용 프로그램 toobe 업로드</span><span class="sxs-lookup"><span data-stu-id="93cb4-139">Upload a web application toobe hosted by hello web app</span></span>

<span data-ttu-id="93cb4-140">GitHub에서 IoT Hub의 실시간 센서 데이터를 표시하는 웹 응용 프로그램을 사용할 수 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="93cb4-140">On GitHub, we've made available a web application that displays real-time sensor data from your IoT hub.</span></span> <span data-ttu-id="93cb4-141">Git 리포지토리를 사용 하 여 웹 앱 toowork hello 구성 GitHub에서 hello 웹 응용 프로그램을 다운로드 하 여 웹 응용 프로그램 toohost hello에 대 한 tooAzure 업로드 toodo 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93cb4-141">All you need toodo is configure hello web app toowork with a Git repository, download hello web application from GitHub, and then upload it tooAzure for hello web app toohost.</span></span>

1. <span data-ttu-id="93cb4-142">Hello 웹 응용 프로그램에서 클릭 **배포 옵션** > **소스 선택** > **로컬 Git 리포지토리**, 클릭 하 고 **확인**.</span><span class="sxs-lookup"><span data-stu-id="93cb4-142">In hello web app, click **Deployment Options** > **Choose Source** > **Local Git Repository**, and then click **OK**.</span></span>

   ![웹 응용 프로그램 배포 toouse hello 로컬 Git 리포지토리를 구성 합니다.](media/iot-hub-live-data-visualization-in-web-apps/5_configure-web-app-deployment-local-git-repository-azure.png)

2. <span data-ttu-id="93cb4-144">클릭 **배포 자격 증명**클릭을 Azure에서 사용자 이름 및 암호 toouse tooconnect toohello Git 리포지토리를 만들거나 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="93cb4-144">Click **Deployment Credentials**, create a user name and password toouse tooconnect toohello Git repository in Azure, and then click **Save**.</span></span>

3. <span data-ttu-id="93cb4-145">클릭 **개요**의 hello 값을 확인 하 고 **Git 복제 url**합니다.</span><span class="sxs-lookup"><span data-stu-id="93cb4-145">Click **Overview**, and note hello value of **Git clone url**.</span></span>

   ![웹 응용 프로그램의 hello Git 복제 URL 가져오기](media/iot-hub-live-data-visualization-in-web-apps/7_web-app-git-clone-url-azure.png)

4. <span data-ttu-id="93cb4-147">로컬 컴퓨터에서 명령 창 또는 터미널 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="93cb4-147">Open a command or terminal window on your local computer.</span></span>

5. <span data-ttu-id="93cb4-148">GitHub에서 hello 웹 앱을 다운로드 하 고 웹 응용 프로그램 toohost hello에 대 한 tooAzure 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="93cb4-148">Download hello web app from GitHub, and upload it tooAzure for hello web app toohost.</span></span> <span data-ttu-id="93cb4-149">따라서 toodo hello 명령 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="93cb4-149">toodo so, run hello following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/web-apps-node-iot-hub-data-visualization.git
   cd web-apps-node-iot-hub-data-visualization
   git remote add webapp <Git clone URL>
   git push webapp master:master
   ```

   > [!NOTE]
   > <span data-ttu-id="93cb4-150">\<Git 복제 URL\> hello에 hello Git 리포지토리의 url hello **개요** hello 웹 응용 프로그램의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="93cb4-150">\<Git clone URL\> is hello URL of hello Git repository found on hello **Overview** page of hello web app.</span></span>

## <a name="open-hello-web-app-toosee-real-time-temperature-and-humidity-data-from-your-iot-hub"></a><span data-ttu-id="93cb4-151">IoT hub에서 hello 웹 앱 toosee 실시간 온도 및 습도 데이터 열</span><span class="sxs-lookup"><span data-stu-id="93cb4-151">Open hello web app toosee real-time temperature and humidity data from your IoT hub</span></span>

<span data-ttu-id="93cb4-152">Hello에 **개요** 페이지 웹 응용 프로그램의 hello URL tooopen hello 웹 응용 프로그램을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="93cb4-152">On hello **Overview** page of your web app, click hello URL tooopen hello web app.</span></span>

![웹 응용 프로그램의 hello URL 가져오기](media/iot-hub-live-data-visualization-in-web-apps/8_web-app-url-azure.png)

<span data-ttu-id="93cb4-154">IoT 허브에서 hello 실시간 온도 및 습도 데이터 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93cb4-154">You should see hello real-time temperature and humidity data from your IoT hub.</span></span>

![실시간 온도 및 습도를 보여 주는 웹앱 페이지](media/iot-hub-live-data-visualization-in-web-apps/9_web-app-page-show-real-time-temperature-humidity-azure.png)

> [!NOTE]
> <span data-ttu-id="93cb4-156">Hello 샘플 응용 프로그램 장치에서 실행 중인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="93cb4-156">Ensure hello sample application is running on your device.</span></span> <span data-ttu-id="93cb4-157">그렇지 않은 빈 차트 받아볼 수, 아래 toohello 자습서를 참조할 수 있습니다 [사용자 장치를 설정](iot-hub-raspberry-pi-kit-node-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="93cb4-157">If not, you will get a blank chart, you can refer toohello tutorials under [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="93cb4-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="93cb4-158">Next steps</span></span>
<span data-ttu-id="93cb4-159">IoT 허브에서 웹 앱 toovisualize 실시간 센서 데이터를 성공적으로 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="93cb4-159">You've successfully used your web app toovisualize real-time sensor data from your IoT hub.</span></span>

<span data-ttu-id="93cb4-160">Azure IoT 허브에서 다른 방법으로 toovisualize 데이터에 대 한 참조 [IoT 허브에서 사용 하 여 Power BI toovisualize 실시간 센서 데이터](iot-hub-live-data-visualization-in-power-bi.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="93cb4-160">For an alternative way toovisualize data from Azure IoT Hub, see [Use Power BI toovisualize real-time sensor data from your IoT hub](iot-hub-live-data-visualization-in-power-bi.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
