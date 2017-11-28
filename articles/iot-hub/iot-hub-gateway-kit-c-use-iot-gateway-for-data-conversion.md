---
title: "Azure IoT 가장자리에 맞춰 IoT 게이트웨이에서 aaaData 변환 | Microsoft Docs"
description: "IoT 게이트웨이 tooconvert hello Azure IoT 가장자리에서 사용자 지정 된 모듈을 통해 센서 데이터의 형식을 사용 합니다."
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
ms.openlocfilehash: ae94b1f96f36dfcb4f77fadc0ece3cff3d0bba91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-for-sensor-data-transformation-with-azure-iot-edge"></a><span data-ttu-id="50cb0-104">IoT 게이트웨이를 사용하여 Azure IoT Edge를 통해 센서 데이터 변환</span><span class="sxs-lookup"><span data-stu-id="50cb0-104">Use IoT gateway for sensor data transformation with Azure IoT Edge</span></span>

> [!NOTE]
> <span data-ttu-id="50cb0-105">이 자습서를 시작 하기 전에 확인 완료 된 hello 단원을 순서에서 다음을 저장 했습니다.</span><span class="sxs-lookup"><span data-stu-id="50cb0-105">Before you start this tutorial, make sure you’ve completed hello following lessons in sequence:</span></span>
> * [<span data-ttu-id="50cb0-106">Intel NUC를 IoT 게이트웨이로 설정</span><span class="sxs-lookup"><span data-stu-id="50cb0-106">Set up Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
> * [<span data-ttu-id="50cb0-107">IoT 게이트웨이 tooconnect 작업 toohello 클라우드 SensorTag tooAzure IoT 허브를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="50cb0-107">Use IoT gateway tooconnect things toohello cloud - SensorTag tooAzure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

<span data-ttu-id="50cb0-108">하나는 Iot 게이트웨이 데이터 수집 tooprocess toohello 클라우드를 보내기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="50cb0-108">One purpose of an Iot gateway is tooprocess collected data before sending it toohello cloud.</span></span> <span data-ttu-id="50cb0-109">Azure IoT 가장자리는 생성 되 고 어셈블된 tooform hello 데이터 처리 워크플로 수 있는 모듈을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="50cb0-109">Azure IoT Edge introduces modules which can be created and assembled tooform hello data processing workflow.</span></span> <span data-ttu-id="50cb0-110">모듈은 메시지를 수신, 특별 한 조치를 수행 및 다른 모듈 tooprocess에 대 한에서 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="50cb0-110">A module receives a message, performs some action on it, and then move it on for other modules tooprocess.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="50cb0-111">학습 내용</span><span class="sxs-lookup"><span data-stu-id="50cb0-111">What you learn</span></span>

<span data-ttu-id="50cb0-112">다른 형식으로 SensorTag hello에서 toocreate 모듈 tooconvert 메시지 방법을 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="50cb0-112">You learn how toocreate a module tooconvert messages from hello SensorTag into a different format.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="50cb0-113">수행할 작업</span><span class="sxs-lookup"><span data-stu-id="50cb0-113">What you do</span></span>

* <span data-ttu-id="50cb0-114">Hello.json 형식으로 모듈 tooconvert 받은 메시지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="50cb0-114">Create a module tooconvert a received message into hello .json format.</span></span>
* <span data-ttu-id="50cb0-115">Hello 모듈을 컴파일하십시오.</span><span class="sxs-lookup"><span data-stu-id="50cb0-115">Compile hello module.</span></span>
* <span data-ttu-id="50cb0-116">Azure IoT 가장자리에서 hello 모듈 toohello 배포용 샘플 응용 프로그램을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="50cb0-116">Add hello module toohello BLE sample application from Azure IoT Edge.</span></span>
* <span data-ttu-id="50cb0-117">Hello 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="50cb0-117">Run hello sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="50cb0-118">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="50cb0-118">What you need</span></span>

* <span data-ttu-id="50cb0-119">다음 순서 대로 완료할 자습서 hello:</span><span class="sxs-lookup"><span data-stu-id="50cb0-119">hello following tutorials completed in sequence:</span></span>
  * [<span data-ttu-id="50cb0-120">Intel NUC를 IoT 게이트웨이로 설정</span><span class="sxs-lookup"><span data-stu-id="50cb0-120">Set up Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
  * [<span data-ttu-id="50cb0-121">IoT 게이트웨이 tooconnect 작업 toohello 클라우드 SensorTag tooAzure IoT 허브를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="50cb0-121">Use IoT gateway tooconnect things toohello cloud - SensorTag tooAzure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)
* <span data-ttu-id="50cb0-122">호스트 컴퓨터에서 실행되는 SSH 클라이언트 -</span><span class="sxs-lookup"><span data-stu-id="50cb0-122">An SSH client that runs on your host computer.</span></span> <span data-ttu-id="50cb0-123">Windows의 경우 PuTTY를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="50cb0-123">PuTTY is recommended on Windows.</span></span> <span data-ttu-id="50cb0-124">Linux와 macOS의 경우 이미 SSH 클라이언트와 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="50cb0-124">Linux and macOS already come with an SSH client.</span></span>
* <span data-ttu-id="50cb0-125">hello IP 주소 및 hello SSH 클라이언트에서 hello 사용자 이름 및 암호 tooaccess hello 게이트웨이 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="50cb0-125">hello IP address and hello username and password tooaccess hello gateway from hello SSH client.</span></span>
* <span data-ttu-id="50cb0-126">인터넷 연결.</span><span class="sxs-lookup"><span data-stu-id="50cb0-126">An Internet connection.</span></span>

## <a name="create-a-module"></a><span data-ttu-id="50cb0-127">모듈 만들기</span><span class="sxs-lookup"><span data-stu-id="50cb0-127">Create a module</span></span>

1. <span data-ttu-id="50cb0-128">Hello 호스트 컴퓨터에서 hello SSH 클라이언트를 실행 하 고 toohello IoT 게이트웨이 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="50cb0-128">On hello host computer, run hello SSH client and connect toohello IoT gateway.</span></span>
1. <span data-ttu-id="50cb0-129">GitHub의 hello IoT 게이트웨이 toohello 홈 디렉터리에서 hello 변환 모듈의 소스 파일 hello hello 다음 명령을 실행 하 여 복제:</span><span class="sxs-lookup"><span data-stu-id="50cb0-129">Clone hello source files of hello conversion module from GitHub toohello home directory of hello IoT gateway by running hello following commands:</span></span>

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-nuc-gateway-customized-module.git
   ```

   <span data-ttu-id="50cb0-130">이것이 hello C 프로그래밍 언어로 작성 된 네이티브 Azure 가장자리 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="50cb0-130">This is a native Azure Edge module written in hello C programming language.</span></span> <span data-ttu-id="50cb0-131">hello 모듈 하나를 따르는 hello에 수신된 된 메시지의 hello 형식을 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="50cb0-131">hello module converts hello format of received messages into hello following one:</span></span>

   ```json
   {"deviceId": "Intel NUC Gateway", "messageId": 0, "temperature": 0.0}
   ```

## <a name="compile-hello-module"></a><span data-ttu-id="50cb0-132">Hello 모듈을 컴파일합니다</span><span class="sxs-lookup"><span data-stu-id="50cb0-132">Compile hello module</span></span>

<span data-ttu-id="50cb0-133">toocompile hello 모듈을 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="50cb0-133">toocompile hello module, run hello following commands:</span></span>

```bash
cd iot-hub-c-intel-nuc-gateway-customized-module/my_module
# change hello build script runnable
chmod 777 build.sh
# remove hello invalid windows character
sed -i -e "s/\r$//" build.sh
# run hello build shell script
./build.sh
```

<span data-ttu-id="50cb0-134">얻게는 `libmy_module.so` hello 컴파일 완료 된 후 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="50cb0-134">You get a `libmy_module.so` file after hello compile is completed.</span></span> <span data-ttu-id="50cb0-135">이 파일의 절대 경로 hello 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="50cb0-135">Make a note of hello absolute path of this file.</span></span>

## <a name="add-hello-module-toohello-ble-sample-application"></a><span data-ttu-id="50cb0-136">Hello 모듈 toohello 배포용 샘플 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="50cb0-136">Add hello module toohello BLE sample application</span></span>

1. <span data-ttu-id="50cb0-137">Hello 다음 명령을 실행 하 여 toohello samples 폴더를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="50cb0-137">Go toohello samples folder by running hello following command:</span></span>

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples
   ```

1. <span data-ttu-id="50cb0-138">Hello 다음 명령을 실행 하 여 hello 구성 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="50cb0-138">Open hello configuration file by running hello following command:</span></span>

   ```bash
   vi ble_gateway.json
   ```

1. <span data-ttu-id="50cb0-139">다음 코드 toohello hello를 삽입 하 여 모듈을 추가 `modules` 섹션.</span><span class="sxs-lookup"><span data-stu-id="50cb0-139">Add a module by inserting hello following code toohello `modules` section.</span></span>

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

1. <span data-ttu-id="50cb0-140">대체 `[Your libmy_module.so path]` hello hello libmy_module.so의 절대 경로 사용 하 여 hello 코드에서 ' 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="50cb0-140">Replace `[Your libmy_module.so path]` in hello code with hello absolute path of hello libmy_module.so\` file.</span></span>
1. <span data-ttu-id="50cb0-141">Hello의 hello 코드 `links` 하나를 따르는 hello로 섹션:</span><span class="sxs-lookup"><span data-stu-id="50cb0-141">Replace hello code in hello `links` section with hello following one:</span></span>

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

1. <span data-ttu-id="50cb0-142">키를 눌러 `ESC`, 한 다음 입력 `:wq` toosave hello 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="50cb0-142">Press `ESC`, and then type `:wq` toosave hello file.</span></span>

## <a name="run-hello-sample-application"></a><span data-ttu-id="50cb0-143">Hello 샘플 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="50cb0-143">Run hello sample application</span></span>

1. <span data-ttu-id="50cb0-144">Hello SensorTag 켭니다.</span><span class="sxs-lookup"><span data-stu-id="50cb0-144">Power on hello SensorTag.</span></span>
1. <span data-ttu-id="50cb0-145">Hello 다음 명령을 실행 하 여 hello SSL_CERT_FILE 환경 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="50cb0-145">Set hello SSL_CERT_FILE environment variable by running hello following command:</span></span>

   ```bash
   export SSL_CERT_FILE=/etc/ssl/certs/ca-certificates.crt
   ```

1. <span data-ttu-id="50cb0-146">Hello 다음 명령을 실행 하 여 hello 추가 된 모듈과 함께 hello 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="50cb0-146">Run hello sample application with hello added module by running hello following command:</span></span>

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a><span data-ttu-id="50cb0-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="50cb0-147">Next steps</span></span>

<span data-ttu-id="50cb0-148">성공적으로 사용 하 여 hello IoT 게이트웨이 tooconvert hello 메시지를 SensorTag에서 hello.json 형식으로 했습니다.</span><span class="sxs-lookup"><span data-stu-id="50cb0-148">You’ve successfully use hello IoT gateway tooconvert hello message from SensorTag into hello .json format.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
