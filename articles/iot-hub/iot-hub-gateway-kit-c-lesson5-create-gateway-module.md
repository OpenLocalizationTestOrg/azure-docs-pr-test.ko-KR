---
title: "aaaCreate 첫 번째 Azure IoT 게이트웨이 모듈 | Microsoft Docs"
description: "모듈 만들고 tooa 샘플 앱 toocustomize 모듈 동작을 추가 합니다."
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
ms.openlocfilehash: 48996fc026c8b708e328b5629801465810e5b6a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="lesson-5-create-your-first-azure-iot-gateway-module"></a>5단원: 첫 번째 Azure IoT 게이트웨이 모듈 만들기
반면 Azure IoT 가장자리 Java,.NET 또는 Node.js로 작성 된 toobuild 모듈 있습니다,이 자습서에서는 C에서 모듈을 작성 하기 위한 hello 단계

## <a name="what-you-will-do"></a>수행할 사항

- 컴파일하고 Intel NUC에 hello hello_world 샘플 응용 프로그램을 실행 합니다.
- 모듈을 만들고 Intel NUC에서 컴파일합니다.
- Hello 새 모듈 toohello hello_world 샘플 앱을 추가 하 고 Intel NUC에 hello 샘플을 실행 하십시오. 새 모듈 hello 타임 스탬프를 갖는 "hello_world" 메시지를 출력합니다.

## <a name="what-you-will-learn"></a>알아볼 내용

- 어떻게 toocompile Intel NUC에서 샘플 응용 프로그램을 실행 합니다.
- 어떻게 toocreate 모듈입니다.
- 어떻게 tooadd 모듈 tooa 샘플 앱을 사용 합니다.

## <a name="what-you-need"></a>필요한 항목

호스트 컴퓨터에 설치된 Azure IoT Edge

## <a name="folder-structure"></a>폴더 구조

1 단원에서 복제 하는 hello 샘플 코드의 5 단원 hello 하위 폴더에는 한 `module` 폴더 및 `sample` 폴더입니다.

![my_module](media/iot-hub-gateway-kit-lessons/lesson5/my_module.png)

- hello `module/my_module` hello 소스 코드 및 스크립트 toobuild hello 모듈 폴더에 포함 되어 있습니다.
- hello `sample` hello 소스 코드 및 스크립트 toobuild hello 샘플 응용 프로그램 폴더에 포함 되어 있습니다.

## <a name="compile-and-run-hello-helloworld-sample-app-on-intel-nuc"></a>컴파일 및 Intel NUC에 hello hello_world 샘플 응용 프로그램 실행

hello `hello_world` 샘플 hello에 따라 한 게이트웨이 만듭니다 `hello_world.json` hello 앱과 연결 된 hello 두 개의 미리 정의 된 모듈을 지정 하는 파일입니다. hello 게이트웨이 "hello world" 메시지 tooa 파일 5 초 마다 기록합니다. 이 섹션에서는 컴파일 및 실행 하기 hello `hello_world` 응용 프로그램의 기본 모듈입니다.

toocompile 및 실행 hello `hello_world` 앱을 호스트 컴퓨터에서 다음이 단계를 수행 합니다.

1. Hello 다음 명령을 실행 하 여 hello 구성 파일을 초기화 합니다.

   ```bash
   cd iot-hub-c-intel-nuc-gateway-getting-started
   cd Lesson5
   npm install
   gulp init
   ```

1. Intel NUC의 MAC 주소 hello로 hello 게이트웨이 구성 파일을 업데이트 합니다. 이 단계는 모두 수행한 경우 hello 단원 통해 너무[구성 및 배포용 샘플 응용 프로그램을 실행][config_ble]합니다.

   1. Hello 다음 명령을 실행 하 여 hello 게이트웨이 구성 파일을 엽니다.

      ```bash
      # For Windows command prompt
      code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json

      # For MacOS or Ubuntu
      code ~/.iot-hub-getting-started/config-gateway.json
      ```

   1. Hello 게이트웨이 업데이트의 MAC 주소 때 있습니다 [IoT 게이트웨이로 Intel NUC 설정][setup_nuc], hello 파일을 저장 합니다.

1. Hello 다음 명령을 실행 하 여 hello 샘플 소스 코드를 컴파일하십시오.

   ```bash
   gulp compile
   ```

   hello hello 샘플 소스 코드 tooIntel NUC 전송 명령과 실행 `build.sh` toocompile 것입니다.

1. Hello 실행 `hello_world` hello 다음 명령을 실행 하 여 응용 프로그램에 액세스 Intel NUC:

   ```bash
   gulp run
   ```

   명령 실행 hello `../Tools/run-hello-world.js` 에 지정 된 `config.json` toostart hello 샘플 응용 프로그램 Intel NUC에 액세스 합니다.

   ![run_sample](media/iot-hub-gateway-kit-lessons/lesson5/run_sample.png)

## <a name="create-a-new-module-and-compile-it-on-intel-nuc"></a>새 모듈을 만들고 Intel NUC에서 컴파일

다음 hello 단계는 새 모듈을 만드는 과정을 안내 하 고 Intel NUC에 컴파일합니다. hello 모듈에 수신 되 면 타임 스탬프를 사용 하 여 메시지를 출력 합니다. 이 섹션에서는 첫 번째 사용자 지정된 게이트웨이 모듈을 만들 것입니다.

모든 Azure IoT 지 모듈 hello 다음 인터페이스를 구현 해야 합니다.

   ```C
   pfModule_ParseConfigurationFromJson Module_ParseConfigurationFromJson
   pfModule_FreeConfiguration Module_FreeConfiguration
   pfModule_Create Module_Create
   pfModule_Destroy Module_Destroy
   pfModule_Receive Module_Receive
   ```

필요에 따라 hello 다음 인터페이스를 구현할 수 있습니다.

   ```C
   pfModule_Start Module_Start
   ```

hello 다음 그림에 모듈의 hello 중요 상태 경로가 있습니다. hello 정사각형 사각형 hello 모듈 상태 간에 이동할 때 tooperform 작업을 구현 하는 메서드를 나타냅니다. hello 타원은 hello 모듈에 수 있는 주요 상태입니다.

![state_path](media/iot-hub-gateway-kit-lessons/lesson5/state_path.png)

이제 hello 템플릿을 기반으로 하는 모듈을 만들어 보겠습니다.

1. Hello 다음 명령을 실행 하 여 hello 템플릿 폴더를 엽니다.

   ```bash
   code module/my_module
   ```

   ![code_module](media/iot-hub-gateway-kit-lessons/lesson5/code_module.png)

   - `src/my_module.c`모듈의 hello 생성을 용이 하 게 하는 템플릿으로 사용 됩니다. hello 템플릿 hello 인터페이스를 선언합니다. Toodo 있으면 tooadd 논리 toohello `MyModule_Receive` 함수입니다.
   - `build.sh`Intel NUC에 hello 빌드 스크립트 toocompile hello 모듈입니다.
1. 열기 hello `src/my_module.c` 파일을 두 개의 헤더 파일 포함:

   ```C
   #include <stdio.h>
   #include "azure_c_shared_utility/xlogging.h"
   ```

1. 다음 코드 toohello hello 추가 `MyModule_Receive` 함수:

   ```C
   if (message == NULL)
   {
      LogError("invalid arg message");
   }
   else
   {
      // get hello message content
      const CONSTBUFFER * content = Message_GetContent(message);
      // get hello local time and format it
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
                  LogError("unable toostrftime");
              }
              else
              {
                  printf("[%s] %.*s\r\n", timetemp, (int)content->size, content->buffer);
              }
          }
      }
   }
   ```

1. 업데이트 hello `config.json` 파일 toospecify hello `workspace` 폴더 Intel NUC에 호스트 컴퓨터와 hello 배포 경로에 있습니다. Hello hello에 파일을 컴파일하는 동안 `workspace` 폴더가 전송된 toohello 배포 경로 됩니다.

   1. 열기 hello `config.json` hello 다음 명령을 실행 하 여 파일:

      ```bash
      code config.json
      ```

   1. 업데이트 `config.json` 같은 구성이 hello로:

      ```json
      "workspace": "./module/my_module",
      "deploy_path": "module/my_module"
      ```

      ![config_json](media/iot-hub-gateway-kit-lessons/lesson5/config_json.png)

1. Hello 다음 명령을 실행 하 여 hello 모듈을 컴파일하십시오.

   ```bash
   gulp compile
   ```

   hello hello 소스 코드 tooIntel NUC 전송 명령과 실행 `build.sh` toocompile hello 모듈입니다.

## <a name="add-hello-module-toohello-helloworld-sample-app-and-run-hello-app-on-intel-nuc"></a>Hello 모듈 toohello hello_world 샘플 응용 프로그램을 추가 하 고 Intel NUC에 hello 앱 실행

이 작업 tooperform, 다음이 단계를 수행 합니다.

1. Intel NUC에 hello 다음 명령을 실행 하 여 모든 hello 사용 가능한 모듈 이진 파일 (.so 파일)를 나열 합니다.

   ```bash
   gulp modules --list
   ```

   이진 경로 hello `my_module` 컴파일 했는지에 나타납니다 아래:

   ```path
   /root/gateway_sample/module/my_module/build/libmy_module.so
   ```

   Hello 기본 로그인 사용자 이름에 변경한 경우 `config-gateway.json`, 이진 경로 hello로 시작 됩니다 `home/<your username>` 대신 `root`합니다.

1. 추가 `my_module` toohello `hello_world` 샘플 응용 프로그램:

   1. 열기 hello `hello_world.json` hello 다음 명령을 실행 하 여 파일:

      ```bash
      code sample/hello_world/src/hello_world.json
      ```

   1. 다음 코드 toohello hello 추가 `modules` 섹션:

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

      값을 hello `module.path` 해야 `/root/gateway_sample/module/my_module/build/libmy_module.so`합니다. hello 코드 선언 `my_module` 으로 hello 게이트웨이 hello 모듈에 지정 된 이진 파일의 hello 위치와 관련 된 toobe `module.path`합니다.
   1. 다음 코드 toohello hello 추가 `links` 섹션:

      ```json
      {
        "source": "hello_world",
        "sink": "my_module"
      }
      ```

      이 코드는 hello에서 메시지가 전송 됨을 지정 `hello_world` 모듈 너무`my_module`합니다.

      ![hello_world_json](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_json.png)

1. Hello 실행 `hello_world` hello 다음 명령을 실행 하 여 샘플 응용 프로그램:

   ```bash
   gulp run --config sample/hello_world/src/hello_world.json
   ```

   hello `--config` 매개 변수는 hello 강제로 `run-hello-world.js` toorun hello를 사용 하 여 스크립트 `hello_world.json` 파일입니다.

   ![hello_world_new](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_new.png)

축하합니다. 타임 스탬프를 사용 하 여 "hello world" 메시지, hello 원래 "hello_world" 모듈에서 다른 결과 인쇄 하면,이 새 모듈의 hello 동작 이제 볼 수 있습니다.

## <a name="next-steps"></a>다음 단계

새 모듈을 생성, 게이트웨이에 toohello hello_world 샘플과 get hello 샘플 앱 toorun hello 새 모듈과 함께 추가 했습니다. Azure IoT 게이트웨이 모듈에 대 한 자세한 toolearn 원하는 경우에 많은 모듈이 샘플을 찾을 수 있습니다: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules)합니다.

<!-- Images and links -->

[config_ble]: iot-hub-gateway-kit-c-lesson3-configure-ble-app.md
[setup_nuc]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
