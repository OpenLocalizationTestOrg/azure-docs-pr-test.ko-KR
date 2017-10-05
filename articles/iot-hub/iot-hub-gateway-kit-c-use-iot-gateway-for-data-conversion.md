---
title: "IoT 게이트웨이에서 Azure IoT Edge를 통해 데이터 변환 | Microsoft Docs"
description: "IoT 게이트웨이를 사용하여 Azure IoT Edge의 사용자 지정 모듈을 통해 센서 데이터의 형식을 변환합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "IoT 게이트웨이 데이터 변환, IoT 게이트웨이 데이터 변환"
ms.assetid: 75f2573d-500b-4405-bff7-61021c4c3500
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: d5c735a4adbc59e9526ec4fd40720c5ec136d63d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="use-iot-gateway-for-sensor-data-transformation-with-azure-iot-edge"></a><span data-ttu-id="d0fc9-104">IoT 게이트웨이를 사용하여 Azure IoT Edge를 통해 센서 데이터 변환</span><span class="sxs-lookup"><span data-stu-id="d0fc9-104">Use IoT gateway for sensor data transformation with Azure IoT Edge</span></span>

> [!NOTE]
> <span data-ttu-id="d0fc9-105">이 자습서를 시작하기 전에 순서대로 다음 단원을 완료했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fc9-105">Before you start this tutorial, make sure you’ve completed the following lessons in sequence:</span></span>
> * [<span data-ttu-id="d0fc9-106">Intel NUC를 IoT 게이트웨이로 설정</span><span class="sxs-lookup"><span data-stu-id="d0fc9-106">Set up Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
> * [<span data-ttu-id="d0fc9-107">IoT 게이트웨이를 사용하여 클라우드에 작업 연결 - SensorTag에서 Azure IoT Hub로</span><span class="sxs-lookup"><span data-stu-id="d0fc9-107">Use IoT gateway to connect things to the cloud - SensorTag to Azure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

<span data-ttu-id="d0fc9-108">Iot 게이트웨이의 한 가지 목적은 먼저 수집된 데이터를 처리한 후에 클라우드로 보내는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d0fc9-108">One purpose of an Iot gateway is to process collected data before sending it to the cloud.</span></span> <span data-ttu-id="d0fc9-109">Azure IoT Edge에서는 데이터 처리 워크플로를 구성하기 위해 만들고 어셈블할 수 있는 모듈이 도입되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d0fc9-109">Azure IoT Edge introduces modules which can be created and assembled to form the data processing workflow.</span></span> <span data-ttu-id="d0fc9-110">모듈은 메시지를 받고, 관련 작업을 수행한 다음, 다른 모듈에서 처리하도록 해당 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d0fc9-110">A module receives a message, performs some action on it, and then move it on for other modules to process.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="d0fc9-111">학습 내용</span><span class="sxs-lookup"><span data-stu-id="d0fc9-111">What you learn</span></span>

<span data-ttu-id="d0fc9-112">SensorTag의 메시지를 다른 형식으로 변환하는 모듈을 만드는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d0fc9-112">You learn how to create a module to convert messages from the SensorTag into a different format.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="d0fc9-113">수행할 작업</span><span class="sxs-lookup"><span data-stu-id="d0fc9-113">What you do</span></span>

* <span data-ttu-id="d0fc9-114">받은 메시지를 .json 형식으로 변환하는 모듈을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d0fc9-114">Create a module to convert a received message into the .json format.</span></span>
* <span data-ttu-id="d0fc9-115">모듈을 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fc9-115">Compile the module.</span></span>
* <span data-ttu-id="d0fc9-116">Azure IoT Edge의 BLE 샘플 응용 프로그램에 모듈을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fc9-116">Add the module to the BLE sample application from Azure IoT Edge.</span></span>
* <span data-ttu-id="d0fc9-117">샘플 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fc9-117">Run the sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="d0fc9-118">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="d0fc9-118">What you need</span></span>

* <span data-ttu-id="d0fc9-119">이전에 순서대로 완료된 다음 자습서:</span><span class="sxs-lookup"><span data-stu-id="d0fc9-119">The following tutorials completed in sequence:</span></span>
  * [<span data-ttu-id="d0fc9-120">Intel NUC를 IoT 게이트웨이로 설정</span><span class="sxs-lookup"><span data-stu-id="d0fc9-120">Set up Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
  * [<span data-ttu-id="d0fc9-121">IoT 게이트웨이를 사용하여 클라우드에 작업 연결 - SensorTag에서 Azure IoT Hub로</span><span class="sxs-lookup"><span data-stu-id="d0fc9-121">Use IoT gateway to connect things to the cloud - SensorTag to Azure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)
* <span data-ttu-id="d0fc9-122">호스트 컴퓨터에서 실행되는 SSH 클라이언트 -</span><span class="sxs-lookup"><span data-stu-id="d0fc9-122">An SSH client that runs on your host computer.</span></span> <span data-ttu-id="d0fc9-123">Windows의 경우 PuTTY를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d0fc9-123">PuTTY is recommended on Windows.</span></span> <span data-ttu-id="d0fc9-124">Linux와 macOS의 경우 이미 SSH 클라이언트와 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0fc9-124">Linux and macOS already come with an SSH client.</span></span>
* <span data-ttu-id="d0fc9-125">SSH 클라이언트에서 게이트웨이에 액세스하기 위한 IP 주소와 사용자 이름 및 암호.</span><span class="sxs-lookup"><span data-stu-id="d0fc9-125">The IP address and the username and password to access the gateway from the SSH client.</span></span>
* <span data-ttu-id="d0fc9-126">인터넷 연결</span><span class="sxs-lookup"><span data-stu-id="d0fc9-126">An Internet connection.</span></span>

## <a name="create-a-module"></a><span data-ttu-id="d0fc9-127">모듈 만들기</span><span class="sxs-lookup"><span data-stu-id="d0fc9-127">Create a module</span></span>

1. <span data-ttu-id="d0fc9-128">호스트 컴퓨터에서 SSH 클라이언트를 실행하고 IoT 게이트웨이에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fc9-128">On the host computer, run the SSH client and connect to the IoT gateway.</span></span>
1. <span data-ttu-id="d0fc9-129">다음 명령을 실행하여 변환 모듈의 소스 파일을 GitHub에서 IoT 게이트웨이의 홈 디렉터리로 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fc9-129">Clone the source files of the conversion module from GitHub to the home directory of the IoT gateway by running the following commands:</span></span>

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-nuc-gateway-customized-module.git
   ```

   <span data-ttu-id="d0fc9-130">이 모듈은 C 프로그래밍 언어로 작성된 네이티브 Azure Edge 모듈이며,</span><span class="sxs-lookup"><span data-stu-id="d0fc9-130">This is a native Azure Edge module written in the C programming language.</span></span> <span data-ttu-id="d0fc9-131">받은 메시지의 형식을 다음 형식으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fc9-131">The module converts the format of received messages into the following one:</span></span>

   ```json
   {"deviceId": "Intel NUC Gateway", "messageId": 0, "temperature": 0.0}
   ```

## <a name="compile-the-module"></a><span data-ttu-id="d0fc9-132">모듈 컴파일</span><span class="sxs-lookup"><span data-stu-id="d0fc9-132">Compile the module</span></span>

<span data-ttu-id="d0fc9-133">모듈을 컴파일하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fc9-133">To compile the module, run the following commands:</span></span>

```bash
cd iot-hub-c-intel-nuc-gateway-customized-module/my_module
# change the build script runnable
chmod 777 build.sh
# remove the invalid windows character
sed -i -e "s/\r$//" build.sh
# run the build shell script
./build.sh
```

<span data-ttu-id="d0fc9-134">컴파일이 완료되면 `libmy_module.so` 파일이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d0fc9-134">You get a `libmy_module.so` file after the compile is completed.</span></span> <span data-ttu-id="d0fc9-135">이 파일의 절대 경로를 기록해 두세요.</span><span class="sxs-lookup"><span data-stu-id="d0fc9-135">Make a note of the absolute path of this file.</span></span>

## <a name="add-the-module-to-the-ble-sample-application"></a><span data-ttu-id="d0fc9-136">BLE 샘플 응용 프로그램에 모듈 추가</span><span class="sxs-lookup"><span data-stu-id="d0fc9-136">Add the module to the BLE sample application</span></span>

1. <span data-ttu-id="d0fc9-137">다음 명령을 실행하여 samples 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fc9-137">Go to the samples folder by running the following command:</span></span>

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples
   ```

1. <span data-ttu-id="d0fc9-138">다음 명령을 실행하여 구성 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d0fc9-138">Open the configuration file by running the following command:</span></span>

   ```bash
   vi ble_gateway.json
   ```

1. <span data-ttu-id="d0fc9-139">`modules` 섹션에 다음 코드를 삽입하여 모듈을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fc9-139">Add a module by inserting the following code to the `modules` section.</span></span>

   ```json
   {
       "name": "MyModule",
       "loader": {
           "name": "native",
           "entrypoint":{
               "module.path": "[Your libmy_module.so path]"
               }
            },
        "args": null
    },
    ```

1. <span data-ttu-id="d0fc9-140">코드의 `[Your libmy_module.so path]`를 libmy_module.so 파일의 절대 경로로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d0fc9-140">Replace `[Your libmy_module.so path]` in the code with the absolute path of the libmy_module.so\` file.</span></span>
1. <span data-ttu-id="d0fc9-141">`links` 섹션의 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d0fc9-141">Replace the code in the `links` section with the following one:</span></span>

   ```json
   {
       "source": "SensorTag",
       "sink": "MyModule"
   },
   {
       "source": "MyModule",
       "sink": "mapping"
   }
   ```

1. <span data-ttu-id="d0fc9-142">`ESC`를 누른 다음 `:wq`를 입력하여 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fc9-142">Press `ESC`, and then type `:wq` to save the file.</span></span>

## <a name="run-the-sample-application"></a><span data-ttu-id="d0fc9-143">샘플 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="d0fc9-143">Run the sample application</span></span>

1. <span data-ttu-id="d0fc9-144">SensorTag의 전원을 켭니다.</span><span class="sxs-lookup"><span data-stu-id="d0fc9-144">Power on the SensorTag.</span></span>
1. <span data-ttu-id="d0fc9-145">다음 명령을 실행하여 SSL_CERT_FILE 환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fc9-145">Set the SSL_CERT_FILE environment variable by running the following command:</span></span>

   ```bash
   export SSL_CERT_FILE=/etc/ssl/certs/ca-certificates.crt
   ```

1. <span data-ttu-id="d0fc9-146">다음 명령을 실행하여 추가된 모듈로 샘플 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fc9-146">Run the sample application with the added module by running the following command:</span></span>

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a><span data-ttu-id="d0fc9-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d0fc9-147">Next steps</span></span>

<span data-ttu-id="d0fc9-148">IoT 게이트웨이를 사용하여 SensorTag의 메시지를 .json 형식으로 성공적으로 변환했습니다.</span><span class="sxs-lookup"><span data-stu-id="d0fc9-148">You’ve successfully use the IoT gateway to convert the message from SensorTag into the .json format.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
