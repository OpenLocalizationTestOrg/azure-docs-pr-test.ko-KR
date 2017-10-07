---
title: "C를 사용 하 여 Windows에서 장치 aaaConnect | Microsoft Docs"
description: "어떻게 tooconnect 장치 toohello Azure IoT Suite 미리 구성 된 Windows에서 실행 되는 C로 작성 된 응용 프로그램을 사용 하 여 원격 모니터링 솔루션에 설명 합니다."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 34e39a58-2434-482c-b3fa-29438a0c05e8
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 51041e0cec113a5cfa006ab2276096baf928eef5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-windows"></a>사용자 장치 toohello 모니터링 미리 구성 된 솔루션 (Windows) 원격 연결
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-c-sample-solution-on-windows"></a>Windows에서 C 샘플 솔루션 만들기
단계를 수행 하는 hello toocreate hello 원격 모니터링와 통신 하는 클라이언트 응용 프로그램 미리 솔루션을 구성 하는 방법을 보여 줍니다. 이 응용 프로그램은 C로 작성되었으며 Windows에서 작성 및 실행됩니다.

Visual Studio 2015 또는 Visual Studio 2017에서 시작 프로젝트를 만들고 hello IoT Hub 장치 클라이언트 NuGet 패키지를 추가 합니다.

1. Visual Studio에서 Visual c + + hello를 사용 하 여 C 콘솔 응용 프로그램을 만들 **Win32 콘솔 응용 프로그램** 템플릿. 이름 hello 프로젝트 **RMDevice**합니다.
2. Hello에 **응용 프로그램 설정** hello에서 페이지 **Win32 응용 프로그램 마법사**, 되도록 **콘솔 응용 프로그램** 을 선택 하 고의 선택을 취소 **미리 컴파일된 헤더** 및 **보안 SDL (Development Lifecycle) 검사**합니다.
3. **솔루션 탐색기**, hello 파일 stdafx.h, targetver.h, stdafx.cpp을 삭제 합니다.
4. **솔루션 탐색기**, hello 파일 RMDevice.cpp tooRMDevice.c 이름을 바꿉니다.
5. **솔루션 탐색기**, hello를 마우스 오른쪽 단추로 클릭 **RMDevice** 프로젝트를 마우스 클릭 **NuGet 패키지 관리**합니다. 클릭 **찾아보기**, 다음 검색 하 고 hello 다음 NuGet 패키지 설치:
   
   * Microsoft.Azure.IoTHub.Serializer
   * Microsoft.Azure.IoTHub.IoTHubClient
   * Microsoft.Azure.IoTHub.MqttTransport
6. **솔루션 탐색기**, hello를 마우스 오른쪽 단추로 클릭 **RMDevice** 프로젝트를 마우스 클릭 **속성** tooopen hello 프로젝트 **속성 페이지**대화 상자. 자세한 내용은 [Visual C++ 프로젝트 속성 설정][lnk-c-project-properties]을 참조하세요. 
7. Hello 클릭 **링커** 폴더를 클릭 hello **입력** 속성 페이지.
8. 추가 **crypt32.lib** toohello **추가 종속성** 속성입니다. 클릭 **확인** 차례로 **확인** 다시 toosave hello 프로젝트 속성 값입니다.

Hello Parson JSON 라이브러리 toohello 추가 **RMDevice** 필요한 hello를 더하고 프로젝트 `#include` 문:

1. 컴퓨터에 적합 한 폴더에서 다음 명령을 hello를 사용 하 여 hello Parson GitHub 리포지토리를 복제 합니다.

    ```
    git clone https://github.com/kgabis/parson.git
    ```

1. Hello hello Parson 리포지토리 tooyour의 로컬 복사본에서 hello parson.h 및 parson.c 파일 복사 **RMDevice** 프로젝트 폴더입니다.

1. Visual Studio에서 마우스 오른쪽 단추로 클릭 hello **RMDevice** 프로젝트를 클릭 하 여 **추가**, 클릭 하 고 **기존 항목**합니다.

1. Hello에 **기존 항목 추가** 대화 상자에서 선택 hello parson.h parson.c에서에서 파일과 hello **RMDevice** 프로젝트 폴더입니다. 클릭 **추가** tooadd 이러한 두 파일 tooyour 프로젝트.

1. Visual Studio에서 hello RMDevice.c 파일을 엽니다. Hello 기존 항목 바꾸기 `#include` 코드 다음 hello로 문:
   
    ```c
    #include "iothubtransportmqtt.h"
    #include "schemalib.h"
    #include "iothub_client.h"
    #include "serializer_devicetwin.h"
    #include "schemaserializer.h"
    #include "azure_c_shared_utility/threadapi.h"
    #include "azure_c_shared_utility/platform.h"
    #include "parson.h"
    ```

    > [!NOTE]
    > 이제 프로젝트를 빌드하는 방법 설정 hello 올바른 종속성에 있는지 확인할 수 있습니다.

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a>빌드 및 실행 hello 샘플

추가 코드 tooinvoke hello **원격\_모니터링\_실행** 함수 로컬 폴더를 빌드하고 hello 장치 응용 프로그램을 실행 합니다.

1. Hello 대체 **주** 다음 코드 tooinvoke hello로 함수 **원격\_모니터링\_실행** 함수:
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. 클릭 **빌드** 차례로 **솔루션 빌드** toobuild hello 장치 응용 프로그램입니다.

1. **솔루션 탐색기**, 마우스 오른쪽 단추로 클릭 hello **RMDevice** 프로젝트를 클릭 하 여 **디버그**, 클릭 하 고 **새 인스턴스 시작** toorun hello 샘플입니다. hello 콘솔 hello 응용 프로그램 보내는 원격 분석 toohello 샘플 솔루션을 미리 구성 된, hello 솔루션 대시보드에서 설정 원하는 속성 값을 받는 및 toomethods hello 솔루션 대시보드에서 호출 응답 메시지를 표시 합니다.

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-c-project-properties]: https://msdn.microsoft.com/library/669zx6zc.aspx
