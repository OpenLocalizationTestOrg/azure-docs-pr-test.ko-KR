---
title: "Connect Intel Edison (C) tooAzure IoT-1 단원: 응용 프로그램 배포 | Microsoft Docs"
description: "GitHub에서 hello C 샘플 응용 프로그램을 복제 하 고이 응용 프로그램 tooyour Intel Edison 보드 gulp toodeploy를 실행 합니다. 이 샘플 응용 프로그램 2 초 마다 hello 연결 LED toohello 보드를 깜박입니다."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino led 프로젝트, arduino led 깜박임, arduino led 깜박임 코드, arduino 깜박임 프로그램, arduino 깜박임 예제"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: b02dfd3f-28fd-4b52-8775-eb0eaf74d707
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: fa84fae812dd742a2ad4997a5e213c8e40e6fcf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a>만들기 및 hello 깜박임 응용 프로그램 배포
## <a name="what-you-will-do"></a>수행할 사항
GitHub에서 hello C 샘플 응용 프로그램을 복제 하 고 hello gulp 도구 toodeploy hello 샘플 응용 프로그램 tooIntel Edison를 사용 합니다. hello 샘플 응용 프로그램 2 초 마다 hello 연결 LED toohello 보드를 깜박입니다. 문제가 있는 경우 hello에 솔루션을 찾는 [문제 해결 페이지][troubleshooting]합니다.

## <a name="what-you-will-learn"></a>알아볼 내용
* 어떻게 toodeploy 및 실행된 hello 샘플 Edison에서 응용 프로그램입니다.

## <a name="what-you-need"></a>필요한 항목
성공적으로 완료 해야 다음 작업 hello:

* [장치 구성][configure-your-device]
* [Hello 도구 가져오기][get-the-tools]

## <a name="open-hello-sample-application"></a>열기 hello 샘플 응용 프로그램
tooopen hello 샘플 응용 프로그램, 다음이 단계를 수행 합니다.

1. Hello 다음 명령을 실행 하 여 GitHub에서 hello 샘플 리포지토리를 복제 합니다.

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-edison-getting-started.git
   ```
2. Hello 다음 명령을 실행 하 여 Visual Studio Code에서 hello 샘플 응용 프로그램을 엽니다.

   ```bash
   cd iot-hub-c-edison-getting-started
   cd Lesson1
   code .
   ```

   ![Repo 구조][repo-structure]

hello에 hello 파일 `app` 하위 폴더는 hello 코드 toocontrol hello LED가 있는 hello 키 원본 파일입니다.

### <a name="install-application-dependencies"></a>응용 프로그램 종속성 설치
Hello 라이브러리 및 hello 다음 명령을 실행 하 여 hello 샘플 응용 프로그램에 필요한 다른 모듈을 설치 합니다.

```bash
npm install
```

## <a name="configure-hello-device-connection"></a>Hello 장치 연결 구성
tooconfigure 장치 연결 hello, 다음이 단계를 수행 합니다.

1. Hello 다음 명령을 실행 하 여 hello 장치 구성 파일을 생성 합니다.

   ```bash
   gulp init
   ```

   hello 구성 파일 `config-edison.json` toolog tooEdison에서 사용 하 여 hello 사용자 자격 증명을 포함 합니다. tooavoid hello 누수 hello 하위 폴더에 사용자 자격 증명의 hello 구성 파일이 생성 됩니다 `.iot-hub-getting-started` hello 컴퓨터에서 홈 폴더의 합니다.

2. Hello 다음 명령을 실행 하 여 Visual Studio Code에서 hello 장치 구성 파일을 엽니다.

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. Hello 자리 표시자 대체 `[device hostname or IP address]` 및 `[device password]` hello IP 주소 및 암호를 이전 단원에서 가격 인하 합니다.

   ![Config.json](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

축하합니다. Hello 첫 번째 Edison에 대 한 샘플 응용 프로그램을 성공적으로 만들었습니다.

## <a name="deploy-and-run-hello-sample-application"></a>배포 하 고 hello 샘플 응용 프로그램 실행
### <a name="install-hello-azure-iot-hub-sdk-on-edison"></a>Edison에 hello Azure IoT 허브 SDK를 설치 합니다.
Hello 다음 명령을 실행 하 여 Edison에 hello Azure IoT 허브 SDK를 설치 합니다.

```bash
gulp install-tools
```

이 작업은 네트워크 연결에 따라 시간이 오래 toocomplete, 걸릴 수 있습니다. 이것 필요 toobe 실행 한 번만 하나의 Edison에 대 한 합니다.

### <a name="deploy-and-run-hello-sample-app"></a>배포 하 고 hello 샘플 응용 프로그램 실행
배포 하 고 hello 다음 명령을 실행 하 여 hello 샘플 응용 프로그램을 실행 합니다.

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a>Hello 앱 작동 확인
hello 샘플 응용 프로그램 hello led가 깜박입니다 20 배에 대 한 후 자동으로 종료 합니다. Hello led가 깜박입니다.이 표시 되지 않으면 참조 hello [문제 해결 가이드] [ troubleshooting] toocommon 문제 해결 방법에 대 한 합니다.

![LED 깜박임][led-blinking]

## <a name="summary"></a>요약
Edison와 필요한 hello 도구 toowork를 설치 하 고 샘플 응용 프로그램 tooEdison tooblink hello LED를 배포 합니다. 있습니다 수 이제 만들고, 배포, 및 Edison tooAzure toosend IoT 허브를 연결 하는 또 다른 샘플 응용 프로그램을 실행 하 고 메시지를 수신 합니다.

## <a name="next-steps"></a>다음 단계
[Hello Azure 도구 가져오기][get-the-azure-tools]

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-c-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure_c.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking_c.jpg
[get-the-azure-tools]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
