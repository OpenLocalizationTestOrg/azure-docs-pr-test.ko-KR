---
title: "시뮬레이션된 장치 및 Azure IoT 게이트웨이 - 문제 해결 | Microsoft Docs"
description: "Intel NUC 게이트웨이 문제 해결 페이지"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "IoT 문제, 사물 인터넷 문제"
ROBOTS: NOINDEX
ms.assetid: 3ee8f4b0-5799-40a3-8cf0-8d5aa44dbc2b
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: cc7add6273e66aadeca9a4915a44f5edf61a0a59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a>문제 해결

## <a name="hardware-issues"></a>하드웨어 문제

### <a name="ti-sensortag-cannot-be-connected"></a>TI SensorTag는 연결할 수 없음

tootroubleshoot SensorTag 연결 문제를 사용 하 여 hello [SensorTag 앱](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide)합니다.

### <a name="have-an-issue-with-intel-nuc"></a>Intel NUC에 문제가 있음

tootroubleshoot 부팅 문제 참조 너무[Intel NUC의 No 부팅 문제 해결](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html)합니다.

tootroubleshoot 운영 체제 문제 참조 너무[Intel NUC에 운영 체제 문제 해결](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html)합니다.

tootroubleshoot의 다른 문제가 너무 참조[Blink 코드 및 Intel NUC에 대 한 코드 경고음을 발생시킬지](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html)합니다.

## <a name="nodejs-package-issues"></a>Node.js 패키지 문제

### <a name="no-response-during-gulp-tasks"></a>gulp 작업 중 응답 없음

Gulp 작업 실행 중에 문제가 발생 하면 hello를 추가할 수 있습니다 `--verbose` 디버깅에 대 한 옵션입니다. 사용 하 여 tooterminate 현재 gulp 작업 시도 `Ctrl + C`, 누른 실행된 hello 다음 콘솔 창 toosee 디버그 메시지에 명령 합니다. 콘솔 출력에서 자세한 오류 메시지를 볼 수 있습니다.

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a>장치 검색 문제

Hello 된 일반적인 문제 해결에 대 한 도움말 `discover-sensortag` 명령에서 확인 hello [wiki 페이지](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl)합니다.

### <a name="npm-issues"></a>NPM 문제

Tooupdate npm 패키지를 hello 다음 명령을 실행 하 여 시도해 보십시오.

```bash
npm install -g npm
```

Hello 문제가 여전히 지속 되는 경우이 문서의 끝 hello에 의견을 남겨 만들거나에 GitHub 문제 우리의 [샘플 리포지토리](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started)합니다.

## <a name="remote-debugging"></a>원격 디버깅
> 아래 지침은 이 자습서에서 사용된 node.js 스크립트를 디버깅하기 위한 것입니다.
### <a name="run-hello-sample-application-in-debug-mode"></a>Hello 샘플 응용 프로그램을 디버그 모드에서 실행

Hello 다음 명령을 실행 하 여 디버그 모드에서 hello 샘플 응용 프로그램을 실행 합니다.

```bash
gulp run --debug
```

Hello 디버그 엔진 준비 되 면 표시 되어야 `Debugger listening on port 5858` hello 콘솔 출력에 있습니다.

### <a name="configure-visual-studio-code-tooconnect-toohello-remote-device"></a>Visual Studio Code tooconnect toohello 원격 장치를 구성 합니다.

1. 열기 hello **디버그** hello 왼쪽 패널입니다.
2. 녹색 hello 클릭 **디버깅 시작** 단추 (F5). Visual Studio Code에 `launch.json` 파일이 열립니다.
3. 업데이트 hello `launch.json` hello 콘텐츠를 다음으로 파일입니다. 대체 `[device hostname or IP address]` hello 실제 장치 IP 주소 또는 호스트 이름으로 합니다.

   ``` json
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
            "remoteRoot": "~/ble_sample"
        }
     ]
   }
   ```

![원격 디버깅 구성](./media/iot-hub-gateway-kit-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a>Toohello 원격 응용 프로그램 연결

녹색 hello 클릭 **디버깅 시작** 단추 toostart 디버깅 (F5).

읽기 [VS Code에서 JavaScript](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn 디버거 hello에 대 한 자세한 합니다.

![디버깅 BLE 샘플](./media/iot-hub-gateway-kit-lessons/troubleshooting/debugging_ble_sample.png)

## <a name="azure-cli-issues"></a>Azure CLI 문제

hello Azure CLI (명령줄 인터페이스 Azure) 미리 보기 빌드를 수행 합니다. tooseek 솔루션 hello를 사용할 수 있습니다 [미리 보기 설치 가이드](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md)합니다.

파일 hello 도구를 사용 하 여 모든 버그를 발생 하는 경우는 [문제](https://github.com/Azure/azure-cli/issues) hello에 **문제** hello GitHub 리포지토리의 섹션입니다.

일반적인 문제 해결에 도움이 필요 하면 확인 hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst)합니다.

충족 하는 경우 "을 찾을 수 없는 hello 요구 사항을 만족 하는 버전" 하십시오 실행된 hello 다음 명령은 tooupgrade pip toolastest 버전입니다.

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a>Python 설치 문제

### <a name="legacy-installation-issues-macos"></a>레거시 설치 문제(macOS)

pip를 설치하는 경우 이전 패키지가 **su** 권한으로 설치되어 있으면 권한 오류가 throw됩니다. 이러한 문제는 brew(macOS)를 사용하는 이전 Python 설치가 완전히 제거되지 않으면 발생합니다. 이전 설치의 일부 pip 패키지가 hello 사용 권한 오류를 일으키는 루트에 의해 생성 됩니다. 솔루션을 hello tooremove 루트에 의해 설치 된 해당 패키지 됩니다. 이 작업 단계 toocomplete 다음 hello를 사용 합니다.

1. 너무 이동`/usr/local/lib/python2.7/site-packages`
2. root에 의해 생성된 패키지 나열: `ls -l | grep root`
3. 2단계의 패키지 제거: `sudo rm -rf {package name}`
4. Python을 다시 설치합니다.

## <a name="azure-iot-hub-issues"></a>Azure IoT Hub 문제

Hello Azure CLI로 Azure IoT 허브 성공적으로 프로 비전 한 tooyour IoT 허브를 연결 하는 도구 toomanage hello 장치 해야 하는 경우 도구 다음 hello 해 보십시오.

### <a name="device-explorer"></a>장치 탐색기

[장치 탐색기](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) Windows 로컬 컴퓨터에서 실행 되며 Azure에서 tooyour IoT 허브를 연결 합니다. Hello 다음 통신할 [IoT Hub 끝점](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):

- 장치 identity management tooprovision IoT hub와 등록 된 장치를 관리 합니다.
- 장치 tooyour IoT 허브에서 보낸 메시지를 모니터링할 수 있도록 장치-클라우드를 수신 합니다.
- IoT 허브에서 tooyour 장치 메시지를 보낼 수 있도록 클라우드-장치를 보냅니다.

이 도구 toouse 내에서 IoT 허브 연결 문자열의 모든 기능을 구성 합니다.

### <a name="iothub-explorer"></a>iothub-explorer

[iothub 탐색기](https://github.com/Azure/iothub-explorer) 샘플 다중 플랫폼 CLI 도구 toomanage 장치 클라이언트입니다. Hello id 레지스트리에의 hello 도구 toomanage hello 장치를 사용 하 고, 장치-클라우드 메시지를 모니터링 하 고, 클라우드-장치 명령을 보낼 수 있습니다.

tooinstall hello 최신 (시험판) 버전의 hello iothub 탐색기 도구를 hello 다음 명령을 실행 합니다.

```bash
npm install -g iothub-explorer@latest
```

모든에 대 한 추가 도움말 tooget hello iothub 탐색기 명령 및 매개 변수, hello 다음 명령을 실행 합니다.

```bash
iothub-explorer help
```

### <a name="hello-azure-portal"></a>hello Azure 포털

전체 CLI 환경은 모든 Azure 리소스를 만들고 관리하는 데 도움이 됩니다. Toouse hello 수도 [Azure 포털](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) toohelp 프로 비전, 관리 및 Azure 리소스를 디버그 합니다.

## <a name="azure-storage-issues"></a>Azure Storage

[Microsoft Azure 저장소 탐색기 (미리 보기)](http://storageexplorer.com/) toowork Windows, macOS 등 및 Linux에서 Azure 저장소 데이터와 함께 사용할 수 있는 Microsoft에서 독립 실행형 앱입니다. 이 도구를 사용 하 여 tooyour 테이블을 연결 하 고 그 안에 hello 데이터를 확인할 수 있습니다. 이 도구 tootroubleshoot Azure 저장소 문제를 사용할 수 있습니다.
