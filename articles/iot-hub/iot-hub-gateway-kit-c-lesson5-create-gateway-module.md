---
title: "첫 번째 Azure IoT 게이트웨이 모듈 만들기 | Microsoft Docs"
description: "모듈을 만들고 샘플 앱에 추가하여 모듈 동작을 사용자 지정합니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: 
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cd7660f4-7b8b-4091-8d71-bb8723165b0b
ms.service: iot-hub
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5e28422158684c3aaf0ac3fdf5b19c80fbccfb02
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-5-create-your-first-azure-iot-gateway-module"></a><span data-ttu-id="16f59-103">5단원: 첫 번째 Azure IoT 게이트웨이 모듈 만들기</span><span class="sxs-lookup"><span data-stu-id="16f59-103">Lesson 5: Create your first Azure IoT Gateway module</span></span>
<span data-ttu-id="16f59-104">Azure IoT Edge를 통해 Java, .NET 또는 Node.js로 작성된 모듈을 빌드할 수 있지만 이 자습서는 C에서 모듈을 빌드하기 위한 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-104">While Azure IoT Edge allows you to build modules written in Java, .NET, or Node.js, this tutorial walks you through the steps for building a module in C.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="16f59-105">수행할 사항</span><span class="sxs-lookup"><span data-stu-id="16f59-105">What you will do</span></span>

- <span data-ttu-id="16f59-106">Intel NUC에서 hello_world 샘플 앱을 컴파일하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-106">Compile and run the hello_world sample app on Intel NUC.</span></span>
- <span data-ttu-id="16f59-107">모듈을 만들고 Intel NUC에서 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-107">Create a module and compile it on Intel NUC.</span></span>
- <span data-ttu-id="16f59-108">새 모듈을 hello_world 샘플 앱에 추가하고 Intel NUC에서 샘플을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-108">Add the new module to the hello_world sample app and then run the sample on Intel NUC.</span></span> <span data-ttu-id="16f59-109">새 모듈은 타임스탬프가 있는 "hello_world" 메시지를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-109">The new module prints out "hello_world" messages with a timestamp.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="16f59-110">알아볼 내용</span><span class="sxs-lookup"><span data-stu-id="16f59-110">What you will learn</span></span>

- <span data-ttu-id="16f59-111">Intel NUC에서 샘플 앱을 컴파일하고 실행하는 방법</span><span class="sxs-lookup"><span data-stu-id="16f59-111">How to compile and run a sample app on Intel NUC.</span></span>
- <span data-ttu-id="16f59-112">모듈을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="16f59-112">How to create a module.</span></span>
- <span data-ttu-id="16f59-113">샘플 앱에 모듈을 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="16f59-113">How to add module to a sample app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="16f59-114">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="16f59-114">What you need</span></span>

<span data-ttu-id="16f59-115">호스트 컴퓨터에 설치된 Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="16f59-115">Azure IoT Edge that has been installed on your host computer.</span></span>

## <a name="folder-structure"></a><span data-ttu-id="16f59-116">폴더 구조</span><span class="sxs-lookup"><span data-stu-id="16f59-116">Folder structure</span></span>

<span data-ttu-id="16f59-117">1단원에서 복제한 샘플 코드의 5단원 하위 폴더에는 `module` 폴더와 `sample` 폴더가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-117">In the Lesson 5 subfolder of the sample code which you cloned in lesson 1, there is a `module` folder and a `sample` folder.</span></span>

![my_module](media/iot-hub-gateway-kit-lessons/lesson5/my_module.png)

- <span data-ttu-id="16f59-119">`module/my_module` 폴더는 모듈을 빌드하기 위한 소스 코드 및 스크립트를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-119">The `module/my_module` folder contains the source code and script to build the module.</span></span>
- <span data-ttu-id="16f59-120">`sample` 폴더는 샘플 앱을 빌드하기 위한 소스 코드 및 스크립트를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-120">The `sample` folder contains the source code and script to build the sample app.</span></span>

## <a name="compile-and-run-the-helloworld-sample-app-on-intel-nuc"></a><span data-ttu-id="16f59-121">Intel NUC에서 hello_world 샘플 앱 컴파일 및 실행</span><span class="sxs-lookup"><span data-stu-id="16f59-121">Compile and run the hello_world sample app on Intel NUC</span></span>

<span data-ttu-id="16f59-122">`hello_world` 샘플은 앱과 연결된 미리 정의된 2개의 모듈을 지정하는 `hello_world.json` 파일을 기준으로 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-122">The `hello_world` sample creates a gateway based on the `hello_world.json` file which specifies the two predefined modules associated with the app.</span></span> <span data-ttu-id="16f59-123">이 게이트웨이는 "hello world" 메시지를 5초마다 파일에 로깅합니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-123">The gateway logs a "hello world" message to a file every 5 seconds.</span></span> <span data-ttu-id="16f59-124">이 섹션에서는 기본 모듈을 사용하여 `hello_world` 앱을 컴파일하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-124">In this section, you compile and run the `hello_world` app with its default module.</span></span>

<span data-ttu-id="16f59-125">`hello_world` 앱을 컴파일 및 실행하려면 호스트 컴퓨터에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-125">To compile and run the `hello_world` app, follow these steps on your host computer:</span></span>

1. <span data-ttu-id="16f59-126">다음 명령을 실행하여 구성 파일을 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-126">Initialize the configuration files by running the following commands:</span></span>

   ```bash
   cd iot-hub-c-intel-nuc-gateway-getting-started
   cd Lesson5
   npm install
   gulp init
   ```

1. <span data-ttu-id="16f59-127">Intel NUC의 MAC 주소로 게이트웨이 구성 파일을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-127">Update the gateway configuration file with the MAC address of Intel NUC.</span></span> <span data-ttu-id="16f59-128">[BLE 샘플 응용 프로그램 구성 및 실행][config_ble] 단계를 마친 경우 이 단계를 건너뛰세요.</span><span class="sxs-lookup"><span data-stu-id="16f59-128">Skip this step if you have gone through the lesson to [configure and run a BLE sample application][config_ble].</span></span>

   1. <span data-ttu-id="16f59-129">다음 명령을 실행하여 게이트웨이 구성 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-129">Open the gateway configuration file by running the following command:</span></span>

      ```bash
      # For Windows command prompt
      code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json

      # For MacOS or Ubuntu
      code ~/.iot-hub-getting-started/config-gateway.json
      ```

   1. <span data-ttu-id="16f59-130">[Intel NUC를 IoT 게이트웨이로 설정][setup_nuc]하면 게이트웨이의 MAC 주소를 업데이트한 후 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-130">Update the gateway's MAC address when you [set up Intel NUC as a IoT gateway][setup_nuc], and then save the file.</span></span>

1. <span data-ttu-id="16f59-131">다음 명령을 실행하여 샘플 소스 코드를 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-131">Compile the sample source code by running the following command:</span></span>

   ```bash
   gulp compile
   ```

   <span data-ttu-id="16f59-132">이 명령은 샘플 소스 코드를 Intel NUC로 전송하고 `build.sh`를 실행하여 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-132">The command transfers the sample source code to Intel NUC and runs `build.sh` to compile it.</span></span>

1. <span data-ttu-id="16f59-133">다음 명령을 실행하여 Intel NUC에서 `hello_world` 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-133">Run the `hello_world` app on Intel NUC by running the following command:</span></span>

   ```bash
   gulp run
   ```

   <span data-ttu-id="16f59-134">이 명령은 `config.json`에 지정된 `../Tools/run-hello-world.js`를 실행하여 Intel NUC에서 샘플 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-134">The command runs `../Tools/run-hello-world.js` that is specified in `config.json` to start the sample app on Intel NUC.</span></span>

   ![run_sample](media/iot-hub-gateway-kit-lessons/lesson5/run_sample.png)

## <a name="create-a-new-module-and-compile-it-on-intel-nuc"></a><span data-ttu-id="16f59-136">새 모듈을 만들고 Intel NUC에서 컴파일</span><span class="sxs-lookup"><span data-stu-id="16f59-136">Create a new module and compile it on Intel NUC</span></span>

<span data-ttu-id="16f59-137">아래 단계는 새 모듈을 만들고 Intel NUC에서 컴파일하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-137">The steps below walk you through creating a new module and compile it on Intel NUC.</span></span> <span data-ttu-id="16f59-138">모듈은 메시지가 발생하면 타임스탬프와 함께 메시지를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-138">The module prints out messages with a timestamp upon receiving them.</span></span> <span data-ttu-id="16f59-139">이 섹션에서는 첫 번째 사용자 지정된 게이트웨이 모듈을 만들 것입니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-139">You will create your first customized gateway module in this section.</span></span>

<span data-ttu-id="16f59-140">Azure IoT Edge 모듈은 다음 인터페이스를 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-140">Any Azure IoT Edge module must implement the following interfaces:</span></span>

   ```C
   pfModule_ParseConfigurationFromJson Module_ParseConfigurationFromJson
   pfModule_FreeConfiguration Module_FreeConfiguration
   pfModule_Create Module_Create
   pfModule_Destroy Module_Destroy
   pfModule_Receive Module_Receive
   ```

<span data-ttu-id="16f59-141">필요에 따라 다음 인터페이스를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-141">You can optionally implement the following interface:</span></span>

   ```C
   pfModule_Start Module_Start
   ```

<span data-ttu-id="16f59-142">다음 다이어그램에서는 모듈의 중요한 상태 경로를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-142">The following diagram shows the important state paths of a module.</span></span> <span data-ttu-id="16f59-143">정사각형은 모듈이 상태 간을 전환할 때 작업을 수행하기 위해 구현하는 메서드를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-143">The square rectangles represent methods you implement to perform operations when the module moves between states.</span></span> <span data-ttu-id="16f59-144">타원은 모듈이 있을 수 있는 주요 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-144">The ovals are major states the module can be in.</span></span>

![state_path](media/iot-hub-gateway-kit-lessons/lesson5/state_path.png)

<span data-ttu-id="16f59-146">이제 템플릿을 기반으로 모듈을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-146">Now let’s create a module based on the template:</span></span>

1. <span data-ttu-id="16f59-147">다음 명령을 실행하여 템플릿 폴더를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-147">Open the template folder by running the following command:</span></span>

   ```bash
   code module/my_module
   ```

   ![code_module](media/iot-hub-gateway-kit-lessons/lesson5/code_module.png)

   - <span data-ttu-id="16f59-149">`src/my_module.c`는 모듈을 간편하게 만들 수 있는 템플릿으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-149">`src/my_module.c` serves as a template that facilitates the creation of a module.</span></span> <span data-ttu-id="16f59-150">이 템플릿은 인터페이스를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-150">The template declares the interfaces.</span></span> <span data-ttu-id="16f59-151">`MyModule_Receive` 함수에 논리를 추가하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-151">All you need to do is to add logic to the `MyModule_Receive` function.</span></span>
   - <span data-ttu-id="16f59-152">`build.sh`는 Intel NUC에서 모듈을 컴파일하기 위한 빌드 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-152">`build.sh` is the build script to compile the module on Intel NUC.</span></span>
1. <span data-ttu-id="16f59-153">`src/my_module.c` 파일을 열고 다음 두 개의 헤더 파일을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-153">Open the `src/my_module.c` file and include two header files:</span></span>

   ```C
   #include <stdio.h>
   #include "azure_c_shared_utility/xlogging.h"
   ```

1. <span data-ttu-id="16f59-154">`MyModule_Receive` 함수에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-154">Add the following code to the `MyModule_Receive` function:</span></span>

   ```C
   if (message == NULL)
   {
      LogError("invalid arg message");
   }
   else
   {
      // get the message content
      const CONSTBUFFER * content = Message_GetContent(message);
      // get the local time and format it
      time_t temp = time(NULL);
      if (temp == (time_t)-1)
      {
          LogError("time function failed");
      }
      else
      {
          struct tm* t = localtime(&temp);
          if (t == NULL)
          {
              LogError("localtime failed");
          }
          else
          {
              char timetemp[80] = { 0 };
              if (strftime(timetemp, sizeof(timetemp) / sizeof(timetemp[0]), "%c", t) == 0)
              {
                  LogError("unable to strftime");
              }
              else
              {
                  printf("[%s] %.*s\r\n", timetemp, (int)content->size, content->buffer);
              }
          }
      }
   }
   ```

1. <span data-ttu-id="16f59-155">`config.json` 파일을 업데이트하여 호스트 컴퓨터의 `workspace` 폴더와 Intel NUC의 배포 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-155">Update the `config.json` file to specify the `workspace` folder on your host computer and the deployment path on Intel NUC.</span></span> <span data-ttu-id="16f59-156">컴파일하는 동안 `workspace` 폴더의 파일은 배포 경로로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-156">During compiling, the files in the `workspace` folder will be transferred to the deployment path.</span></span>

   1. <span data-ttu-id="16f59-157">다음 명령을 실행하여 `config.json` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-157">Open the `config.json` file by running the following command:</span></span>

      ```bash
      code config.json
      ```

   1. <span data-ttu-id="16f59-158">`config.json`을 다음 구성으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-158">Update `config.json` with the following configuration:</span></span>

      ```json
      "workspace": "./module/my_module",
      "deploy_path": "module/my_module"
      ```

      ![config_json](media/iot-hub-gateway-kit-lessons/lesson5/config_json.png)

1. <span data-ttu-id="16f59-160">다음 명령을 실행하여 모듈을 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-160">Compile the module by running the following command:</span></span>

   ```bash
   gulp compile
   ```

   <span data-ttu-id="16f59-161">이 명령은 소스 코드를 Intel NUC로 전송하고 `build.sh`를 실행하여 모듈을 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-161">The command transfers the source code to Intel NUC and runs `build.sh` to compile the module.</span></span>

## <a name="add-the-module-to-the-helloworld-sample-app-and-run-the-app-on-intel-nuc"></a><span data-ttu-id="16f59-162">모듈을 hello_world 샘플 앱에 추가하고 Intel NUC에서 해당 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-162">Add the module to the hello_world sample app and run the app on Intel NUC</span></span>

<span data-ttu-id="16f59-163">이 작업을 수행하려면 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-163">To perform this task, follow these steps:</span></span>

1. <span data-ttu-id="16f59-164">다음 명령을 실행하여 Intel NUC의 사용 가능한 모든 모듈 이진 파일(.so 파일)을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-164">List all the available module binaries (.so files) on Intel NUC by running the following command:</span></span>

   ```bash
   gulp modules --list
   ```

   <span data-ttu-id="16f59-165">컴파일한 `my_module`의 이진 경로는 아래와 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-165">The binary path of `my_module` that you compiled should be listed as below:</span></span>

   ```path
   /root/gateway_sample/module/my_module/build/libmy_module.so
   ```

   <span data-ttu-id="16f59-166">`config-gateway.json`에서 기본 로그인 사용자 이름을 변경하는 경우 이진 경로는 `root` 대신 `home/<your username>`으로 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-166">If you change the default login username in `config-gateway.json`, the binary path will start with `home/<your username>` instead of `root`.</span></span>

1. <span data-ttu-id="16f59-167">`hello_world` 샘플 앱에 `my_module`을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-167">Add `my_module` to the `hello_world` sample app:</span></span>

   1. <span data-ttu-id="16f59-168">다음 명령을 실행하여 `hello_world.json` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-168">Open the `hello_world.json` file by running the following command:</span></span>

      ```bash
      code sample/hello_world/src/hello_world.json
      ```

   1. <span data-ttu-id="16f59-169">`modules` 섹션에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-169">Add the following code to the `modules` section:</span></span>

      ```json
      {
       "name": "my_module",
       "loader": {
       "name": "native",
       "entrypoint": {
       "module.path": "/root/gateway_sample/module/my_module/build/libmy_module.so"
         }
        },
       "args": null
      }
      ```

      <span data-ttu-id="16f59-170">`module.path` 값은 `/root/gateway_sample/module/my_module/build/libmy_module.so`여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-170">The value of `module.path` should be `/root/gateway_sample/module/my_module/build/libmy_module.so`.</span></span> <span data-ttu-id="16f59-171">이 코드는 `my_module`이 `module.path`에 지정된 모듈 이진 파일의 위치 및 게이트웨이와 연결되도록 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-171">The code declares `my_module` to be associated with the gateway as well as the location of the module binary specified in `module.path`.</span></span>
   1. <span data-ttu-id="16f59-172">`links` 섹션에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-172">Add the following code to the `links` section:</span></span>

      ```json
      {
        "source": "hello_world",
        "sink": "my_module"
      }
      ```

      <span data-ttu-id="16f59-173">이 코드는 `hello_world` 모듈에서 `my_module`로 메시지가 전송되도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-173">This code specifies that messages are transferred from the `hello_world` module to `my_module`.</span></span>

      ![hello_world_json](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_json.png)

1. <span data-ttu-id="16f59-175">다음 명령을 실행하여 `hello_world` 샘플 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-175">Run the `hello_world` sample app by running the following command:</span></span>

   ```bash
   gulp run --config sample/hello_world/src/hello_world.json
   ```

   <span data-ttu-id="16f59-176">`--config` 매개 변수는 `hello_world.json` 파일을 사용하여 `run-hello-world.js` 스크립트가 강제로 실행되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-176">The `--config` parameter forces the `run-hello-world.js` script to run by using the `hello_world.json` file.</span></span>

   ![hello_world_new](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_new.png)

<span data-ttu-id="16f59-178">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-178">Congratulations.</span></span> <span data-ttu-id="16f59-179">이제 이 새 모듈의 동작을 볼 수 있습니다. 이 모듈은 타임스탬프와 함께 "hello world" 메시지를 출력합니다. 이것은 원래 "hello_world" 모듈의 결과와는 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-179">You can now see the behavior of this new module, it simply prints out "hello world" messages with a timestamp, a different result from the original "hello_world" module.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16f59-180">다음 단계</span><span class="sxs-lookup"><span data-stu-id="16f59-180">Next Steps</span></span>

<span data-ttu-id="16f59-181">새 모듈을 만들었으며 hello_world 샘플에 추가하고 샘플 앱이 게이트웨이의 새 모듈로 실행되도록 했습니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-181">You’ve created a new module, added it to the hello_world sample, and get the sample app to run with the new module on your gateway.</span></span> <span data-ttu-id="16f59-182">Azure IoT 게이트웨이 모듈에 대한 자세한 내용을 보려면 [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules)에서 더 많은 모듈 샘플을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16f59-182">If you want to learn more about Azure IoT gateway modules, you can find more module samples here: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).</span></span>

<!-- Images and links -->

[config_ble]: iot-hub-gateway-kit-c-lesson3-configure-ble-app.md
[setup_nuc]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
