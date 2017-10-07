---
title: "Connect Raspberry Pi (C) tooAzure IoT-문제 해결 | Microsoft Docs"
description: "Hello 라스베리 Pi Node.js 경험에 대 한 페이지 문제 해결"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "IoT 문제, 사물 인터넷 문제"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 22cf50dc-8206-42a2-a1fc-f75fa85135fa
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8f0807104550e8e53a132f7741564b33f1db17ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a>문제 해결
## <a name="hardware-issues"></a>하드웨어 문제
### <a name="hello-application-runs-well-but-hello-led-is-not-blinking"></a>hello 응용 프로그램 실행 외에 있지만 hello LED가 깜박이고 하지
이 문제는 항상 관련된 toohardware 회로 연결입니다. 다음 단계 tooidentify 문제 hello를 사용 합니다.

1. 올바른 hello 선택 했음을 확인 **GPIO** 보드에 있습니다. hello 두 포트 해야 **GPIO GND (Pin 6)** 및 **GPIO 04 (Pin 7)**합니다.
2. 프로그램 led hello 극성이 정확한 지 확인 합니다. hello 긴 레그 hello 나타내야 **양의**, anode pin입니다.
3. 사용 하 여 hello **3.3 v 고정** 및 **GND Pin** 라스베리 Pi 3에 있습니다. Pi hello DC 전원 취급 합니다. 해당 hello LED는 정상 작동을 확인 합니다.

![LED 사양](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a>다른 하드웨어 문제
라스베리 Pi 3에 대 한 일반적인 문제를 해결 하는 방법에 대 한 정보를 참조 hello [공식 문제 해결 페이지](http://elinux.org/R-Pi_Troubleshooting)합니다.

## <a name="nodejs-package-issues"></a>Node.js 패키지 문제
### <a name="no-response-during-gulp-tasks"></a>gulp 작업 중 응답 없음
Gulp 작업 실행 중에 문제가 발생 하면 hello를 추가할 수 있습니다 `--verbose` 디버깅에 대 한 옵션입니다. Ctrl + C를 사용 하 여 tooterminate 현재 gulp 작업을 시도 하 고 다음 콘솔 창 toosee 디버그 메시지에 명령을 hello를 실행 하십시오. 콘솔 출력에서 자세한 오류 메시지를 볼 수 있습니다.

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a>장치 검색 문제
Hello 된 일반적인 문제 해결에 대 한 도움말 `devdisco` 명령에서 확인 hello [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md)합니다.

### <a name="npm-issues"></a>NPM 문제
Tooupdate npm 패키지를 hello 다음 명령을 사용 하 여 시도해 보십시오.

```bash
npm install -g npm
```

Hello 문제가 여전히 지속 되는 경우이 문서의 끝 hello에 의견을 남겨 만들거나에 GitHub 문제 우리의 [샘플 리포지토리](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started)합니다.

## <a name="remote-debugging"></a>원격 디버깅
### <a name="run-hello-sample-application-in-debug-mode"></a>Hello 샘플 응용 프로그램을 디버그 모드에서 실행
```bash
gulp run --debug
```

Hello 디버그 엔진 준비 되 면 표시 되어야 ```Debugger listening on port 5858``` hello 콘솔 출력에 있습니다.

### <a name="configure-visual-studio-code-tooconnect-toohello-remote-device"></a>Visual Studio Code tooconnect toohello 원격 장치를 구성 합니다.
1. 열기 hello **디버그** hello 왼쪽 패널입니다.
2. 녹색 hello 클릭 **디버깅 시작** 단추 (F5). Visual Studio Code에 launch.json 파일이 열립니다.
3. 콘텐츠를 다음 hello로 hello launch.json 파일을 업데이트 합니다. 대체 `[device hostname or IP address]` hello 실제 장치 IP 주소 또는 호스트 이름으로 합니다.

> [!NOTE]
> Visual Studio 디버깅 hello에 대 한 자세한 toolearn 너무 참조 하십시오[Visual Studio 코드에서 디버깅](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes)합니다.


```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Attach",
            "type": "node",
            "request": "attach",
            "port": 5858,
            "address": "[device hostname or IP address]",
            "restart": false,
            "sourceMaps": false,
            "outDir": null,
            "localRoot": "${workspaceRoot}",
            "remoteRoot": null
        }
    ]
}
```

![원격 디버깅 구성](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a>Toohello 원격 응용 프로그램 연결
녹색 hello 클릭 **디버깅 시작** 단추 toostart 디버깅 (F5).

읽기 [VS Code에서 JavaScript](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn 디버거 hello에 대 한 자세한 합니다.

![대화형 원격 디버깅](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a>Azure CLI 문제
hello Azure CLI (명령줄 인터페이스 Azure) 미리 보기 빌드를 수행 합니다. tooseek 솔루션 hello를 사용할 수 있습니다 [미리 보기 설치 가이드](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md)합니다.

파일 hello 도구를 사용 하 여 모든 버그를 발생 하는 경우는 [문제](https://github.com/Azure/azure-cli/issues) hello에 **문제** hello GitHub 리포지토리의 섹션입니다.

일반적인 문제 해결에 도움이 필요 하면 확인 hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst)합니다.

## <a name="python-installation-issues"></a>Python 설치 문제
### <a name="legacy-installation-issues-macos"></a>레거시 설치 문제(macOS)
pip를 설치하는 경우 이전 패키지가 **su** 권한으로 설치되어 있으면 권한 오류가 throw됩니다. 이러한 문제는 brew(macOS)를 사용하는 이전 Python 설치가 완전히 제거되지 않으면 발생합니다. 이전 설치의 일부 pip 패키지가 hello 사용 권한 오류를 일으키는 루트에 의해 생성 됩니다. 솔루션을 hello tooremove 루트에 의해 설치 된 해당 패키지 됩니다. 이 작업 단계 toocomplete 다음 hello를 사용 합니다.

1. /usr/local/lib/python2.7/site-packages로 이동
2. root에 의해 생성된 패키지 나열: `ls -l | grep root`
3. 2단계의 패키지 제거: `sudo rm -rf {package name}`
4. Python을 다시 설치합니다.

## <a name="azure-iot-hub-issues"></a>Azure IoT Hub 문제
Azure CLI 있는 Azure IoT 허브를 사용 하 여 성공적으로 프로 비전 한 tooyour IoT 허브를 연결 하는 도구 toomanage hello 장치 해야 하는 경우 도구 다음 hello 해 보십시오.

### <a name="device-explorer"></a>장치 탐색기
hello [장치 탐색기](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) 도구 Windows 로컬 컴퓨터에서 실행 되며 Azure에서 tooyour IoT 허브를 연결 합니다. Hello 다음 통신할 [IoT Hub 끝점](iot-hub-devguide.md):


* *장치 id 관리* tooprovision IoT hub와 등록 된 장치를 관리 합니다.
* *장치-클라우드 수신* 장치 tooyour IoT 허브에서 보낸 메시지를 모니터링할 수 있도록 합니다.
* *클라우드-장치 보내기* IoT 허브에서 tooyour 장치 메시지를 보낼 수 있도록 합니다.

이 도구 toouse 내에서 IoT 허브 연결 문자열의 모든 기능을 구성 합니다.

### <a name="iothub-explorer"></a>iothub-explorer
[iothub 탐색기](https://github.com/Azure/iothub-explorer) 샘플 다중 플랫폼 CLI 도구 toomanage 장치입니다. Hello id 레지스트리에의 hello 도구 toomanage hello 장치를 사용 하 고, 장치-클라우드 메시지를 모니터링 하 고, 클라우드-장치 메시지를 보낼 수 있습니다.

tooinstall hello (시험판) 최신 버전의 hello iothub 탐색기 도구를 hello 다음 명령줄 환경에서 명령을 실행 합니다.

```bash
npm install -g iothub-explorer@latest
```

다음 명령을 iothub 탐색기 명령 및 매개 변수 모두에 대 한 추가 도움말 tooget hello hello를 사용할 수 있습니다.

```bash
iothub-explorer help
```

### <a name="azure-portal"></a>Azure portal
전체 CLI 환경은 모든 Azure 리소스를 만들고 관리하는 데 도움이 됩니다. Toouse hello 수도 [Azure 포털](../azure-portal-overview.md) toohelp 프로 비전, 관리 및 Azure 리소스를 디버그 합니다.

## <a name="azure-storage-issues"></a>Azure Storage
[Microsoft Azure 저장소 탐색기 (미리 보기)](http://storageexplorer.com) toowork Windows, macOS 등 및 Linux에서 Azure 저장소 데이터와 함께 사용할 수 있는 Microsoft에서 독립 실행형 앱입니다. 이 도구를 사용 하 여 tooyour 테이블을 연결 하 고 그 안에 hello 데이터를 확인할 수 있습니다. 이 도구 tootroubleshoot Azure 저장소 문제를 사용할 수 있습니다.

