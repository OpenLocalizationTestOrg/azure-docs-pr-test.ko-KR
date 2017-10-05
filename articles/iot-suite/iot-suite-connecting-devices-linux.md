---
title: "Linux에서 C를 사용하여 장치 연결 | Microsoft Docs"
description: "Linux에서 실행되는 C로 작성된 응용 프로그램을 사용하여 미리 구성된 Azure IoT Suite 원격 모니터링 솔루션에 장치를 연결하는 방법을 설명합니다."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0c7c8039-0bbf-4bb5-9e79-ed8cff433629
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 9adbc9cc13f0b4cafa3a3a7703c46f8085b15232
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-device-to-the-remote-monitoring-preconfigured-solution-linux"></a><span data-ttu-id="4948a-103">미리 구성된 원격 모니터링 솔루션에 장치 연결(Linux)</span><span class="sxs-lookup"><span data-stu-id="4948a-103">Connect your device to the remote monitoring preconfigured solution (Linux)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="build-and-run-a-sample-c-client-linux"></a><span data-ttu-id="4948a-104">샘플 C 클라이언트 Linux 빌드 및 실행</span><span class="sxs-lookup"><span data-stu-id="4948a-104">Build and run a sample C client Linux</span></span>
<span data-ttu-id="4948a-105">다음 단계에서는 미리 구성된 원격 모니터링 솔루션과 통신하는 클라이언트 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4948a-105">The following steps show you how to create a client application that communicates with the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="4948a-106">이 응용 프로그램은 C로 작성되었으며 Ubuntu Linux에서 작성 및 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="4948a-106">This application is written in C and built and run on Ubuntu Linux.</span></span>

<span data-ttu-id="4948a-107">이러한 단계를 완료하려면 Ubuntu 버전 15.04 또는 15.10을 실행하는 장치가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4948a-107">To complete these steps, you need a device running Ubuntu version 15.04 or 15.10.</span></span> <span data-ttu-id="4948a-108">계속하기 전에 다음 명령을 사용하여 Ubuntu 장치에서 필수 구성 요소 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="4948a-108">Before proceeding, install the prerequisite packages on your Ubuntu device using the following command:</span></span>

```
sudo apt-get install cmake gcc g++
```

## <a name="install-the-client-libraries-on-your-device"></a><span data-ttu-id="4948a-109">장치에 클라이언트 라이브러리 설치</span><span class="sxs-lookup"><span data-stu-id="4948a-109">Install the client libraries on your device</span></span>
<span data-ttu-id="4948a-110">Azure IoT Hub 클라이언트 라이브러리를 **apt-get** 명령을 사용하여 Ubuntu 장치에 설치할 수 있는 패키지로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4948a-110">The Azure IoT Hub client libraries are available as a package you can install on your Ubuntu device using the **apt-get** command.</span></span> <span data-ttu-id="4948a-111">Ubuntu 컴퓨터에서 IoT Hub 클라이언트 라이브러리와 헤더 파일을 포함하는 패키지를 설치하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="4948a-111">Complete the following steps to install the package that contains the IoT Hub client library and header files on your Ubuntu computer:</span></span>

1. <span data-ttu-id="4948a-112">셸에서 AzureIoT 리포지토리를 컴퓨터에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4948a-112">In a shell, add the AzureIoT repository to your computer:</span></span>
   
    ```
    sudo add-apt-repository ppa:aziotsdklinux/ppa-azureiot
    sudo apt-get update
    ```
2. <span data-ttu-id="4948a-113">azure-iot-sdk-c-dev 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="4948a-113">Install the azure-iot-sdk-c-dev package</span></span>
   
    ```
    sudo apt-get install -y azure-iot-sdk-c-dev
    ```

## <a name="install-the-parson-json-parser"></a><span data-ttu-id="4948a-114">Parson JSON 파서 설치</span><span class="sxs-lookup"><span data-stu-id="4948a-114">Install the Parson JSON parser</span></span>
<span data-ttu-id="4948a-115">IoT Hub 클라이언트 라이브러리는 Parson JSON 파서를 사용하여 메시지 페이로드를 구문 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="4948a-115">The IoT Hub client libraries use the Parson JSON parser to parse message payloads.</span></span> <span data-ttu-id="4948a-116">컴퓨터의 적합한 폴더에서 다음 명령을 사용하여 Parson GitHub 리포지토리를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="4948a-116">In a suitable folder on your computer, clone the Parson GitHub repository using the following command:</span></span>

```
git clone https://github.com/kgabis/parson.git
```

## <a name="prepare-your-project"></a><span data-ttu-id="4948a-117">프로젝트 준비</span><span class="sxs-lookup"><span data-stu-id="4948a-117">Prepare your project</span></span>
<span data-ttu-id="4948a-118">Ubuntu 컴퓨터에서 **remote\_monitoring**이라는 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4948a-118">On your Ubuntu machine, create a folder called **remote\_monitoring**.</span></span> <span data-ttu-id="4948a-119">**remote\_monitoring** 폴더에서:</span><span class="sxs-lookup"><span data-stu-id="4948a-119">In the **remote\_monitoring** folder:</span></span>

- <span data-ttu-id="4948a-120">**main.c**, **remote\_monitoring.c**, **remote\_monitoring.h**, **CMakeLists.txt**의 4개 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4948a-120">Create the four files **main.c**, **remote\_monitoring.c**, **remote\_monitoring.h**, and **CMakeLists.txt**.</span></span>
- <span data-ttu-id="4948a-121">**parson**이라는 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4948a-121">Create folder called **parson**.</span></span>

<span data-ttu-id="4948a-122">Parson 리포지토리의 로컬 복사본에서 파일 **parson.c** 및 **parson.h**를 **remote\_monitoring/parson** 폴더로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="4948a-122">Copy the files **parson.c** and **parson.h** from your local copy of the Parson repository into the **remote\_monitoring/parson** folder.</span></span>

<span data-ttu-id="4948a-123">텍스트 편집기에서 **remote\_monitoring.c** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4948a-123">In a text editor, open the **remote\_monitoring.c** file.</span></span> <span data-ttu-id="4948a-124">다음 `#include` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4948a-124">Add the following `#include` statements:</span></span>
   
```
#include "iothubtransportmqtt.h"
#include "schemalib.h"
#include "iothub_client.h"
#include "serializer_devicetwin.h"
#include "schemaserializer.h"
#include "azure_c_shared_utility/threadapi.h"
#include "azure_c_shared_utility/platform.h"
#include "parson.h"
```

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="call-the-remotemonitoringrun-function"></a><span data-ttu-id="4948a-125">remote\_monitoring\_run 함수 실행</span><span class="sxs-lookup"><span data-stu-id="4948a-125">Call the remote\_monitoring\_run function</span></span>
<span data-ttu-id="4948a-126">텍스트 편집기에서 **remote_monitoring.h** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4948a-126">In a text editor, open the **remote_monitoring.h** file.</span></span> <span data-ttu-id="4948a-127">다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4948a-127">Add the following code:</span></span>

```
void remote_monitoring_run(void);
```

<span data-ttu-id="4948a-128">텍스트 편집기에서 **main.c** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4948a-128">In a text editor, open the **main.c** file.</span></span> <span data-ttu-id="4948a-129">다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4948a-129">Add the following code:</span></span>

```
#include "remote_monitoring.h"

int main(void)
{
    remote_monitoring_run();

    return 0;
}
```

## <a name="build-and-run-the-application"></a><span data-ttu-id="4948a-130">응용 프로그램 빌드 및 실행</span><span class="sxs-lookup"><span data-stu-id="4948a-130">Build and run the application</span></span>
<span data-ttu-id="4948a-131">다음 단계에서는 *CMake* 를 사용하여 클라이언트 응용 프로그램을 빌드하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4948a-131">The following steps describe how to use *CMake* to build your client application.</span></span>

1. <span data-ttu-id="4948a-132">텍스트 편집기에서 **remote_monitoring** 폴더의 **CMakeLists.txt** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4948a-132">In a text editor, open the **CMakeLists.txt** file in the **remote_monitoring** folder.</span></span>

1. <span data-ttu-id="4948a-133">클라이언트 응용 프로그램을 작성하는 방법을 정의하려면 다음 지침을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4948a-133">Add the following instructions to define how to build your client application:</span></span>
   
    ```
    macro(compileAsC99)
      if (CMAKE_VERSION VERSION_LESS "3.1")
        if (CMAKE_C_COMPILER_ID STREQUAL "GNU")
          set (CMAKE_C_FLAGS "--std=c99 ${CMAKE_C_FLAGS}")
          set (CMAKE_CXX_FLAGS "--std=c++11 ${CMAKE_CXX_FLAGS}")
        endif()
      else()
        set (CMAKE_C_STANDARD 99)
        set (CMAKE_CXX_STANDARD 11)
      endif()
    endmacro(compileAsC99)

    cmake_minimum_required(VERSION 2.8.11)
    compileAsC99()

    set(AZUREIOT_INC_FOLDER "${CMAKE_SOURCE_DIR}" "${CMAKE_SOURCE_DIR}/parson" "/usr/include/azureiot" "/usr/include/azureiot/inc")

    include_directories(${AZUREIOT_INC_FOLDER})

    set(sample_application_c_files
        ./parson/parson.c
        ./remote_monitoring.c
        ./main.c
    )

    set(sample_application_h_files
        ./parson/parson.h
        ./remote_monitoring.h
    )

    add_executable(sample_app ${sample_application_c_files} ${sample_application_h_files})

    target_link_libraries(sample_app
        serializer
        iothub_client
        iothub_client_mqtt_transport
        aziotsharedutil
        umqtt
        pthread
        curl
        ssl
        crypto
        m
    )
    ```
1. <span data-ttu-id="4948a-134">**remote_monitoring** 폴더에서 CMake가 생성하는 *make* 파일을 저장할 폴더를 만든 후 다음과 같이 **cmake** 및 **make** 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4948a-134">In the **remote_monitoring** folder, create a folder to store the *make* files that CMake generates and then run the **cmake** and **make** commands as follows:</span></span>
   
    ```
    mkdir cmake
    cd cmake
    cmake ../
    make
    ```

1. <span data-ttu-id="4948a-135">클라이언트 응용 프로그램을 실행하고 IoT Hub에 원격 분석을 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="4948a-135">Run the client application and send telemetry to IoT Hub:</span></span>
   
    ```
    ./sample_app
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

