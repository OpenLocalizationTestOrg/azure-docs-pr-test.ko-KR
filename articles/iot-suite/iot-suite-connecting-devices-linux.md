---
title: "C를 사용 하 여 Linux 기반 장치 aaaConnect | Microsoft Docs"
description: "어떻게 tooconnect 장치 toohello Azure IoT Suite 미리 구성 된 Linux에서 실행 중인 C로 작성 된 응용 프로그램을 사용 하 여 원격 모니터링 솔루션에 설명 합니다."
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
ms.openlocfilehash: 57393817d40d3555177956a01fa71058bc256988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-linux"></a><span data-ttu-id="6f067-103">사용자 장치 toohello 모니터링 미리 구성 된 솔루션 (Linux) 원격 연결</span><span class="sxs-lookup"><span data-stu-id="6f067-103">Connect your device toohello remote monitoring preconfigured solution (Linux)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="build-and-run-a-sample-c-client-linux"></a><span data-ttu-id="6f067-104">샘플 C 클라이언트 Linux 빌드 및 실행</span><span class="sxs-lookup"><span data-stu-id="6f067-104">Build and run a sample C client Linux</span></span>
<span data-ttu-id="6f067-105">단계를 수행 하는 hello toocreate hello 원격 모니터링와 통신 하는 클라이언트 응용 프로그램 미리 솔루션을 구성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6f067-105">hello following steps show you how toocreate a client application that communicates with hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="6f067-106">이 응용 프로그램은 C로 작성되었으며 Ubuntu Linux에서 작성 및 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f067-106">This application is written in C and built and run on Ubuntu Linux.</span></span>

<span data-ttu-id="6f067-107">이 단계는 toocomplete, Ubuntu 15.04 또는 15.10 버전을 실행 하는 장치가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f067-107">toocomplete these steps, you need a device running Ubuntu version 15.04 or 15.10.</span></span> <span data-ttu-id="6f067-108">계속 하기 전에 hello 필수 구성 요소 패키지가 hello 다음 명령을 사용 하 여 Ubuntu 장치에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f067-108">Before proceeding, install hello prerequisite packages on your Ubuntu device using hello following command:</span></span>

```
sudo apt-get install cmake gcc g++
```

## <a name="install-hello-client-libraries-on-your-device"></a><span data-ttu-id="6f067-109">장치에 hello 클라이언트 라이브러리를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f067-109">Install hello client libraries on your device</span></span>
<span data-ttu-id="6f067-110">hello Azure IoT Hub 클라이언트 라이브러리를 hello를 사용 하 여 Ubuntu 장치에 설치할 수 있습니다 패키지로 **apt get** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="6f067-110">hello Azure IoT Hub client libraries are available as a package you can install on your Ubuntu device using hello **apt-get** command.</span></span> <span data-ttu-id="6f067-111">다음 단계 tooinstall hello 패키지 hello IoT 허브 클라이언트 라이브러리 및 Ubuntu 컴퓨터에 있는 헤더 파일을 포함 하는 hello를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f067-111">Complete hello following steps tooinstall hello package that contains hello IoT Hub client library and header files on your Ubuntu computer:</span></span>

1. <span data-ttu-id="6f067-112">셸에서 hello AzureIoT 리포지토리 tooyour 컴퓨터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f067-112">In a shell, add hello AzureIoT repository tooyour computer:</span></span>
   
    ```
    sudo add-apt-repository ppa:aziotsdklinux/ppa-azureiot
    sudo apt-get update
    ```
2. <span data-ttu-id="6f067-113">Hello azure-iot-sdk-c-dev 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="6f067-113">Install hello azure-iot-sdk-c-dev package</span></span>
   
    ```
    sudo apt-get install -y azure-iot-sdk-c-dev
    ```

## <a name="install-hello-parson-json-parser"></a><span data-ttu-id="6f067-114">Hello Parson JSON 파서를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f067-114">Install hello Parson JSON parser</span></span>
<span data-ttu-id="6f067-115">IoT Hub 클라이언트 라이브러리를 사용 하 여 hello hello Parson JSON 파서 tooparse 메시지 페이로드입니다.</span><span class="sxs-lookup"><span data-stu-id="6f067-115">hello IoT Hub client libraries use hello Parson JSON parser tooparse message payloads.</span></span> <span data-ttu-id="6f067-116">컴퓨터에 적합 한 폴더에서 다음 명령을 hello를 사용 하 여 hello Parson GitHub 리포지토리를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f067-116">In a suitable folder on your computer, clone hello Parson GitHub repository using hello following command:</span></span>

```
git clone https://github.com/kgabis/parson.git
```

## <a name="prepare-your-project"></a><span data-ttu-id="6f067-117">프로젝트 준비</span><span class="sxs-lookup"><span data-stu-id="6f067-117">Prepare your project</span></span>
<span data-ttu-id="6f067-118">Ubuntu 컴퓨터에서 **remote\_monitoring**이라는 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6f067-118">On your Ubuntu machine, create a folder called **remote\_monitoring**.</span></span> <span data-ttu-id="6f067-119">Hello에 **원격\_모니터링** 폴더:</span><span class="sxs-lookup"><span data-stu-id="6f067-119">In hello **remote\_monitoring** folder:</span></span>

- <span data-ttu-id="6f067-120">Hello 4 개의 파일을 만듭니다 **main.c**, **원격\_monitoring.c**, **원격\_monitoring.h**, 및 **CMakeLists.txt**.</span><span class="sxs-lookup"><span data-stu-id="6f067-120">Create hello four files **main.c**, **remote\_monitoring.c**, **remote\_monitoring.h**, and **CMakeLists.txt**.</span></span>
- <span data-ttu-id="6f067-121">**parson**이라는 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6f067-121">Create folder called **parson**.</span></span>

<span data-ttu-id="6f067-122">Hello 파일 복사 **parson.c** 및 **parson.h** hello에 hello Parson 저장소의 로컬 복사본에서 **원격\_모니터링/parson** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="6f067-122">Copy hello files **parson.c** and **parson.h** from your local copy of hello Parson repository into hello **remote\_monitoring/parson** folder.</span></span>

<span data-ttu-id="6f067-123">텍스트 편집기를 열고 hello **원격\_monitoring.c** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6f067-123">In a text editor, open hello **remote\_monitoring.c** file.</span></span> <span data-ttu-id="6f067-124">Hello 다음 추가 `#include` 문:</span><span class="sxs-lookup"><span data-stu-id="6f067-124">Add hello following `#include` statements:</span></span>
   
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

## <a name="call-hello-remotemonitoringrun-function"></a><span data-ttu-id="6f067-125">Hello 원격 호출\_모니터링\_함수 실행</span><span class="sxs-lookup"><span data-stu-id="6f067-125">Call hello remote\_monitoring\_run function</span></span>
<span data-ttu-id="6f067-126">텍스트 편집기를 열고 hello **remote_monitoring.h** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6f067-126">In a text editor, open hello **remote_monitoring.h** file.</span></span> <span data-ttu-id="6f067-127">Hello 코드 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f067-127">Add hello following code:</span></span>

```
void remote_monitoring_run(void);
```

<span data-ttu-id="6f067-128">텍스트 편집기를 열고 hello **main.c** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6f067-128">In a text editor, open hello **main.c** file.</span></span> <span data-ttu-id="6f067-129">Hello 코드 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f067-129">Add hello following code:</span></span>

```
#include "remote_monitoring.h"

int main(void)
{
    remote_monitoring_run();

    return 0;
}
```

## <a name="build-and-run-hello-application"></a><span data-ttu-id="6f067-130">빌드 및 hello 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="6f067-130">Build and run hello application</span></span>
<span data-ttu-id="6f067-131">hello 다음과 같은 단계로 진행 방법을 toouse *CMake* toobuild 클라이언트 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="6f067-131">hello following steps describe how toouse *CMake* toobuild your client application.</span></span>

1. <span data-ttu-id="6f067-132">텍스트 편집기를 열고 hello **CMakeLists.txt** hello에 대 한 파일 **remote_monitoring** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="6f067-132">In a text editor, open hello **CMakeLists.txt** file in hello **remote_monitoring** folder.</span></span>

1. <span data-ttu-id="6f067-133">추가 지침 toodefine 방법을 따라 hello toobuild 클라이언트 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="6f067-133">Add hello following instructions toodefine how toobuild your client application:</span></span>
   
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
1. <span data-ttu-id="6f067-134">Hello에 **remote_monitoring** 폴더를 만들 폴더 toostore hello *확인* 해당 CMake를 생성 하 고 다음 실행 파일 hello **cmake** 및 **확인** 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6f067-134">In hello **remote_monitoring** folder, create a folder toostore hello *make* files that CMake generates and then run hello **cmake** and **make** commands as follows:</span></span>
   
    ```
    mkdir cmake
    cd cmake
    cmake ../
    make
    ```

1. <span data-ttu-id="6f067-135">Hello 클라이언트 응용 프로그램을 실행 하 고 원격 분석 tooIoT 허브 보내기:</span><span class="sxs-lookup"><span data-stu-id="6f067-135">Run hello client application and send telemetry tooIoT Hub:</span></span>
   
    ```
    ./sample_app
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

