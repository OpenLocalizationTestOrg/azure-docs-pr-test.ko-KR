---
title: "IoT 게이트웨이 tooconnect 장치 tooAzure IoT Hub aaaUse | Microsoft Docs"
description: "Toouse IoT 게이트웨이 tooconnect TI SensorTag으로 Intel NUC 및 송신 센서 데이터 tooAzure IoT Hub hello에서 클라우드 방식에 대해 알아봅니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "iot 게이트웨이 장치 toocloud 연결"
ms.assetid: cb851648-018c-4a7e-860f-b62ed3b493a5
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: 418af34bf29992d46b76ae59ef548744808664c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-tooconnect-things-toohello-cloud---sensortag-tooazure-iot-hub"></a><span data-ttu-id="18ad1-104">IoT 게이트웨이 tooconnect 작업 toohello 클라우드 SensorTag tooAzure IoT 허브를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="18ad1-104">Use IoT gateway tooconnect things toohello cloud - SensorTag tooAzure IoT Hub</span></span>

> [!NOTE]
> <span data-ttu-id="18ad1-105">이 자습서를 시작하기 전에 먼저 [Intel NUC를 IoT 게이트웨이로 설정](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)을 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-105">Before you start this tutorial, make sure you’ve completed [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md).</span></span> <span data-ttu-id="18ad1-106">[IoT 게이트웨이로 Intel NUC 설정](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), IoT 게이트웨이로 hello Intel NUC 장치를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-106">In [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), you set up hello Intel NUC device as an IoT gateway.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="18ad1-107">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="18ad1-107">What you will learn</span></span>

<span data-ttu-id="18ad1-108">배웁니다 어떻게 toouse IoT 게이트웨이 tooconnect 텍사스 기기 SensorTag (CC2650STK) tooAzure IoT 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-108">You learn how toouse an IoT gateway tooconnect a Texas Instruments SensorTag (CC2650STK) tooAzure IoT Hub.</span></span> <span data-ttu-id="18ad1-109">hello IoT 게이트웨이 온도 보내고 SensorTag tooAzure IoT 허브에서 hello 습도 데이터 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-109">hello IoT gateway sends temperature and humidity data collected from hello SensorTag tooAzure IoT Hub.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="18ad1-110">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="18ad1-110">What you will do</span></span>

- <span data-ttu-id="18ad1-111">IoT Hub를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-111">Create an IoT hub.</span></span>
- <span data-ttu-id="18ad1-112">SensorTag hello에 대 한 hello IoT hub에 장치를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-112">Register a device in hello IoT hub for hello SensorTag.</span></span>
- <span data-ttu-id="18ad1-113">Hello IoT 게이트웨이와 hello SensorTag 간 hello 연결을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-113">Enable hello connection between hello IoT gateway and hello SensorTag.</span></span>
- <span data-ttu-id="18ad1-114">배포용 샘플 응용 프로그램 toosend SensorTag 데이터 tooyour IoT 허브를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-114">Run a BLE sample application toosend SensorTag data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="18ad1-115">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="18ad1-115">What you need</span></span>

- <span data-ttu-id="18ad1-116">[Intel NUC를 IoT 게이트웨이로 설정](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) 자습서를 완료하여 Intel NUC를 IoT 게이트웨이로 설정.</span><span class="sxs-lookup"><span data-stu-id="18ad1-116">Tutorial [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) completed in which you set up Intel NUC as an IoT gateway.</span></span>
- * <span data-ttu-id="18ad1-117">활성 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="18ad1-117">An active Azure subscription.</span></span> <span data-ttu-id="18ad1-118">Azure 계정이 없는 경우 몇 분 만에 [Azure 평가판 계정](https://azure.microsoft.com/free/)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-118">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
- <span data-ttu-id="18ad1-119">호스트 컴퓨터에서 실행되는 SSH 클라이언트 -</span><span class="sxs-lookup"><span data-stu-id="18ad1-119">An SSH client that runs on your host computer.</span></span> <span data-ttu-id="18ad1-120">Windows의 경우 PuTTY를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-120">PuTTY is recommended on Windows.</span></span> <span data-ttu-id="18ad1-121">Linux와 macOS의 경우 이미 SSH 클라이언트와 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-121">Linux and macOS already come with an SSH client.</span></span>
- <span data-ttu-id="18ad1-122">hello IP 주소 및 hello SSH 클라이언트에서 hello 사용자 이름 및 암호 tooaccess hello 게이트웨이 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-122">hello IP address and hello username and password tooaccess hello gateway from hello SSH client.</span></span>
- <span data-ttu-id="18ad1-123">인터넷 연결.</span><span class="sxs-lookup"><span data-stu-id="18ad1-123">An Internet connection.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

> [!NOTE]
> <span data-ttu-id="18ad1-124">여기서 SensorTag용 새 장치 등록</span><span class="sxs-lookup"><span data-stu-id="18ad1-124">Here you register this new device for your SensorTag</span></span>

## <a name="enable-hello-connection-between-hello-iot-gateway-and-hello-sensortag"></a><span data-ttu-id="18ad1-125">Hello IoT 게이트웨이와 hello SensorTag 간 hello 연결을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="18ad1-125">Enable hello connection between hello IoT gateway and hello SensorTag</span></span>

<span data-ttu-id="18ad1-126">이 단원의 태스크를 수행 하는 hello를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-126">In this section, you perform hello following tasks:</span></span>

- <span data-ttu-id="18ad1-127">Bluetooth 연결에 대 한 hello SensorTag의 hello MAC 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-127">Get hello MAC address of hello SensorTag for Bluetooth connection.</span></span>
- <span data-ttu-id="18ad1-128">Hello IoT 게이트웨이 toohello SensorTag에서에서 Bluetooth 연결을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-128">Initiate a Bluetooth connection from hello IoT gateway toohello SensorTag.</span></span>

### <a name="get-hello-mac-address-of-hello-sensortag-for-bluetooth-connection"></a><span data-ttu-id="18ad1-129">Bluetooth 연결에 대 한 hello SensorTag의 hello MAC 주소 가져오기</span><span class="sxs-lookup"><span data-stu-id="18ad1-129">Get hello MAC address of hello SensorTag for Bluetooth connection</span></span>

1. <span data-ttu-id="18ad1-130">Hello 호스트 컴퓨터에서 hello SSH 클라이언트를 실행 하 고 toohello IoT 게이트웨이 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-130">On hello host computer, run hello SSH client and connect toohello IoT gateway.</span></span>
1. <span data-ttu-id="18ad1-131">Bluetooth hello 다음 명령을 실행 하 여 차단을 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-131">Unblock Bluetooth by running hello following command:</span></span>

   ```bash
   sudo rfkill unblock bluetooth
   ```

1. <span data-ttu-id="18ad1-132">Hello IoT 게이트웨이에서 hello Bluetooth 서비스를 시작 하 고 다음 명령을 실행 하 여 Bluetooth hello Bluetooth 셸 tooconfigure를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-132">Start hello Bluetooth service on hello IoT gateway and enter a Bluetooth shell tooconfigure Bluetooth by running hello following commands:</span></span>

   ```bash
   sudo systemctl start bluetooth
   bluetoothctl
   ```

1. <span data-ttu-id="18ad1-133">실행 하 여 hello Bluetooth 컨트롤러에서 전원 다음 Bluetooth 셸 hello에서 명령을 hello:</span><span class="sxs-lookup"><span data-stu-id="18ad1-133">Power on hello Bluetooth controller by running hello following command at hello Bluetooth shell:</span></span>

   ```bash
   power on
   ```

   ![hello Bluetooth 컨트롤러 bluetoothctl IoT 게이트웨이 hello에 대 한 전원](./media/iot-hub-iot-gateway-connect-device-to-cloud/8_power-on-bluetooth-controller-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="18ad1-135">Hello 다음 명령을 실행 하 여 주변 Bluetooth 장치에 대 한 검색을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-135">Start scanning for nearby Bluetooth devices by running hello following command:</span></span>

   ```bash
   scan on
   ```

   ![bluetoothctl을 사용하여 주변의 Bluetooth 장치 검색](./media/iot-hub-iot-gateway-connect-device-to-cloud/9_start-scan-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="18ad1-137">Hello SensorTag 단추 쌍으로 연결 하는 hello 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-137">Press hello pairing button on hello SensorTag.</span></span> <span data-ttu-id="18ad1-138">hello SensorTag 깜박입니다에서 hello 녹색 LED.</span><span class="sxs-lookup"><span data-stu-id="18ad1-138">hello green LED on hello SensorTag flashes.</span></span>
1. <span data-ttu-id="18ad1-139">Bluetooth 셸 hello에 hello SensorTag가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-139">At hello Bluetooth shell, you should see hello SensorTag is found.</span></span> <span data-ttu-id="18ad1-140">Hello hello SensorTag의 MAC 주소를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-140">Make a note of hello MAC address of hello SensorTag.</span></span> <span data-ttu-id="18ad1-141">이 예에서 hello hello SensorTag의 MAC 주소는 `24:71:89:C0:7F:82`합니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-141">In this example, hello MAC address of hello SensorTag is `24:71:89:C0:7F:82`.</span></span>
1. <span data-ttu-id="18ad1-142">Hello 다음 명령을 실행 하 여 hello 검사를 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-142">Turn off hello scan by running hello following command:</span></span>

   ```bash
   scan off
   ```

   ![bluetoothctl을 사용하여 주변의 Bluetooth 장치 검색 중지](./media/iot-hub-iot-gateway-connect-device-to-cloud/10_stop-scanning-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

### <a name="initiate-a-bluetooth-connection-from-hello-iot-gateway-toohello-sensortag"></a><span data-ttu-id="18ad1-144">Bluetooth 연결 hello IoT 게이트웨이 toohello SensorTag에서 시작</span><span class="sxs-lookup"><span data-stu-id="18ad1-144">Initiate a Bluetooth connection from hello IoT gateway toohello SensorTag</span></span>

1. <span data-ttu-id="18ad1-145">Toohello SensorTag hello 다음 명령을 실행 하 여 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-145">Connect toohello SensorTag by running hello following command:</span></span>

   ```bash
   connect <MAC address>
   ```

   ![Toohello SensorTag bluetoothctl를 사용 하 여 연결](./media/iot-hub-iot-gateway-connect-device-to-cloud/11_connect-to-sensortag-at-bluetooth-shell-bluetoothctl.png)

1. <span data-ttu-id="18ad1-147">Hello SensorTag 끊고 hello 다음 명령을 실행 하 여 hello Bluetooth 셸 종료:</span><span class="sxs-lookup"><span data-stu-id="18ad1-147">Disconnect from hello SensorTag and exit hello Bluetooth shell by running hello following commands:</span></span>

   ```bash
   disconnect
   exit
   ```

   ![Hello SensorTag bluetoothctl와에서 연결 끊기](./media/iot-hub-iot-gateway-connect-device-to-cloud/12_disconnect-from-sensortag-at-bluetooth-shell-bluetoothctl.png)

<span data-ttu-id="18ad1-149">성공적으로 SensorTag hello와 hello IoT 게이트웨이 간의 hello 연결 사용 설정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-149">You've successfully enabled hello connection between hello SensorTag and hello IoT gateway.</span></span>

## <a name="run-a-ble-sample-application-toosend-sensortag-data-tooyour-iot-hub"></a><span data-ttu-id="18ad1-150">배포용 샘플 응용 프로그램 toosend SensorTag 데이터 tooyour IoT 허브를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-150">Run a BLE sample application toosend SensorTag data tooyour IoT hub</span></span>

<span data-ttu-id="18ad1-151">hello Bluetooth 낮은 에너지 (배포용) 샘플 응용 프로그램은 Azure IoT 가장자리에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-151">hello Bluetooth Low Energy (BLE) sample application is provided by Azure IoT Edge.</span></span> <span data-ttu-id="18ad1-152">hello 샘플 응용 프로그램에는 배포용 연결에서 데이터를 수집 및 hello 데이터 tooyou IoT 허브를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-152">hello sample application collects data from BLE connection and send hello data tooyou IoT hub.</span></span> <span data-ttu-id="18ad1-153">toorun hello 샘플 응용 프로그램을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-153">toorun hello sample application, you need to:</span></span>

1. <span data-ttu-id="18ad1-154">Hello 샘플 응용 프로그램을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-154">Configure hello sample application.</span></span>
1. <span data-ttu-id="18ad1-155">Hello IoT 게이트웨이에서 hello 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-155">Run hello sample application on hello IoT gateway.</span></span>

### <a name="configure-hello-sample-application"></a><span data-ttu-id="18ad1-156">Hello 샘플 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="18ad1-156">Configure hello sample application</span></span>

1. <span data-ttu-id="18ad1-157">Hello 다음 명령을 실행 하 여 hello 샘플 응용 프로그램의 toohello 폴더를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-157">Go toohello folder of hello sample application by running hello following command:</span></span>

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples/ble_gateway
   ```

1. <span data-ttu-id="18ad1-158">Hello 다음 명령을 실행 하 여 hello 구성 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-158">Open hello configuration file by running hello following command:</span></span>

   ```bash
   vi ble_gateway.json
   ```

1. <span data-ttu-id="18ad1-159">Hello 구성 파일에 다음 값에는 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-159">In hello configuration file, fill in hello following values:</span></span>

   <span data-ttu-id="18ad1-160">**IoTHubName**: IoT 허브의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-160">**IoTHubName**: hello name of your IoT hub.</span></span>

   <span data-ttu-id="18ad1-161">**IoTHubSuffix**: 가져오기 IoTHubSuffix hello 기본 키의 hello 장치 연결 문자열의 아래쪽에 표시 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-161">**IoTHubSuffix**: Get IoTHubSuffix from hello primary key of hello device connection string that you noted down.</span></span> <span data-ttu-id="18ad1-162">Hello hello 장치 연결 문자열의 기본 키를 가져올 하지 IoT 허브 연결 문자열의 기본 키를 hello 하 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-162">Ensure that you get hello primary key of hello device connection string, not hello primary key of your IoT hub connection string.</span></span> <span data-ttu-id="18ad1-163">hello 장치 연결 문자열의 기본 키 hello hello 형식으로 되어 `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`합니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-163">hello primary key of hello device connection string is in hello format of `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.</span></span>

   <span data-ttu-id="18ad1-164">**전송**: hello 기본값은 `amqp`합니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-164">**Transport**: hello default value is `amqp`.</span></span> <span data-ttu-id="18ad1-165">이 값 transpotation 중 hello 프로토콜을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-165">This value shows hello protocol during transpotation.</span></span> <span data-ttu-id="18ad1-166">`http`, `amqp` 또는 `mqtt`입니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-166">It could be `http`, `amqp`, or `mqtt`.</span></span>

   <span data-ttu-id="18ad1-167">**macAddress**: hello hello 아래로 기록해둔 SensorTag의 MAC 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-167">**macAddress**: hello MAC address of hello SensorTag that you noted down.</span></span>

   <span data-ttu-id="18ad1-168">**deviceID**: hello 장치의 IoT 허브에서 만든 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-168">**deviceID**: ID of hello device that you created in your IoT hub.</span></span>

   <span data-ttu-id="18ad1-169">**deviceKey**: hello hello 장치 연결 문자열의 기본 키입니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-169">**deviceKey**: hello primary key of hello device connection string.</span></span>

   ![Hello 배포용 샘플 응용 프로그램의 전체 hello 구성 파일](./media/iot-hub-iot-gateway-connect-device-to-cloud/13_edit-config-file-of-ble-sample.png)

1. <span data-ttu-id="18ad1-171">키를 눌러 `ESC` 유형과 `:wq` toosave hello 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-171">Press `ESC` and type `:wq` toosave hello file.</span></span>

### <a name="run-hello-sample-application"></a><span data-ttu-id="18ad1-172">Hello 샘플 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="18ad1-172">Run hello sample application</span></span>

1. <span data-ttu-id="18ad1-173">SensorTag 켜져 있는지 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-173">Make sure hello SensorTag is powered on.</span></span>
1. <span data-ttu-id="18ad1-174">Hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ad1-174">Run hello following command:</span></span>

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a><span data-ttu-id="18ad1-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="18ad1-175">Next steps</span></span>

[<span data-ttu-id="18ad1-176">IoT 게이트웨이를 사용하여 Azure IoT Edge를 통해 센서 데이터 변환</span><span class="sxs-lookup"><span data-stu-id="18ad1-176">Use IoT gateway for sensor data transformation with Azure IoT Edge</span></span>](iot-hub-gateway-kit-c-use-iot-gateway-for-data-conversion.md)
