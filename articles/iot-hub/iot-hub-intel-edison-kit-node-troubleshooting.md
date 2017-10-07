---
title: "연결 Intel Edison (노드) tooAzure IoT-4 단원: 문제 해결 | Microsoft Docs"
description: "Intel Edison Node.js 환경 문제 해결 페이지"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino 문제 해결"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: f11c5521-8a36-44c0-baad-f5ec26ab4618
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9502300f7f372255572b49bea45dd3e1fdaeeb37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a>문제 해결
## <a name="hardware-issues"></a>하드웨어 문제
Intel Edison에서 일반적인 문제를 해결 하는 방법에 대 한 정보를 참조 hello [공식 문제 해결 페이지](https://software.intel.com/en-us/node/637974)합니다.

## <a name="nodejs-package-issues"></a>Node.js 패키지 문제
### <a name="no-response-during-gulp-tasks"></a>gulp 작업 중 응답 없음
Gulp 작업을 실행 하는 문제가 발생 하면 hello를 추가할 수 있습니다 `--verbose` 디버깅에 대 한 옵션입니다. 사용 하 여 tooterminate 현재 gulp 작업 시도 `Ctrl + C`, 누른 실행된 hello 다음 콘솔 창 toosee 디버그 메시지에 명령 합니다. 콘솔 출력에서 자세한 오류 메시지를 볼 수 있습니다. 

```bash
gulp --verbose
```

### <a name="npm-issues"></a>NPM 문제
다음 명령을 hello로 tooupdate NPM 패키지를 시도 합니다.

```bash
npm install -g npm
```

Hello 문제가 여전히 지속 되는 경우이 문서의 끝 hello에 의견을 남겨 만들거나에 GitHub 문제 우리의 [샘플 리포지토리][sample-repository]합니다.

## <a name="remote-debugging"></a>원격 디버깅

### <a name="run-hello-sample-application-in-debug-mode"></a>Hello 샘플 응용 프로그램을 디버그 모드에서 실행

```bash
gulp run --debug
```

수 toosee 있어야 hello 디버그 엔진 준비 되 면 ```Debugger listening on port 5858``` hello 콘솔 출력에서 합니다.

### <a name="configure-vs-code-tooconnect-toohello-remote-device"></a>VS Code tooconnect toohello 원격 장치를 구성 합니다.

열기 hello **디버그** hello 왼쪽 패널입니다.

녹색 hello 클릭 **디버깅 시작** 단추 (F5). VS Code 열리지는 **launch.json** 있는 파일 tooupdate 필요 합니다.

업데이트 hello **launch.json** 파일 다음 hello로 콘텐츠를 교체 `[device hostname or IP address]` hello 실제 장치 IP 주소 또는 호스트 이름입니다.  

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

![원격 디버깅 구성](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a>Toohello 원격 응용 프로그램 연결

녹색 hello 클릭 **디버깅 시작** (F5) 단추를 선택한 디버깅을 이용 하세요.

읽을 수 [VS Code에서 JavaScript](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn 디버거 hello에 대 한 자세한 합니다.

![대화형 원격 디버깅](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a>Azure-CLI 문제
hello Azure CLI (명령줄 인터페이스 Azure) 미리 보기 빌드를 수행 합니다. Hello에서 솔루션을 찾고 [미리 보기 설치 가이드](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek 솔루션입니다. 명령을 예상 대로 작동 하지 않는 경우 tooupgrade Azure cli toolatest 버전을 시도 합니다.

파일 hello 도구를 사용 하 여 모든 버그를 발생 하는 경우는 [문제](https://github.com/Azure/azure-cli/issues) hello에 **문제** hello GitHub 리포지토리의 섹션입니다.

일반적인 문제 해결 도움말에 대 한 확인 hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst)합니다.

충족 하는 경우 "을 찾을 수 없는 hello 요구 사항을 만족 하는 버전" 하십시오 실행된 hello 다음 명령은 tooupgrade pip toolastest 버전입니다.

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a>Python 설치 문제
### <a name="legacy-installation-issues-macos"></a>레거시 설치 문제(macOS)
**pip**를 설치하는 경우 이전 패키지가 **su** 권한으로 설치되어 있으면 권한 오류가 발생합니다. 이러한 문제는 brew(macOS)를 사용하는 이전 Python 설치가 완전히 제거되지 않으면 발생합니다. 일부 **pip** 이전 설치에서 패키지는 hello 사용 권한 오류를 생성 하는 루트에 의해 만들어진 합니다. 솔루션을 hello tooremove 루트에 의해 설치 된 해당 패키지 됩니다. 이 작업 단계 toocomplete 다음 hello를 사용 합니다.

1. /usr/local/lib/python2.7/site-packages로 이동
2. root에 의해 생성된 패키지를 나열입니다. `ls -l | grep root`
3. 2단계의 패키지 제거: `sudo rm -rf {package name}`
4. Python을 다시 설치합니다.

## <a name="azure-iot-hub-issues"></a>Azure IoT Hub 문제
Azure IoT 허브를 구축 했습니다 했습니다 `azure-cli`, 도구 다음 시도 hello tooyour IoT 허브를 연결 하는 도구 toomanage hello 장치 필요:

### <a name="device-explorer"></a>장치 탐색기
[장치 탐색기](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) Windows 로컬 컴퓨터에서 실행 되며 Azure에서 tooyour IoT 허브를 연결 합니다. Hello 다음 통신할 [IoT Hub 끝점](iot-hub-devguide.md):

- _장치 id 관리_ tooprovision IoT hub와 등록 된 장치를 관리 합니다.
- _장치-클라우드 수신_ 장치 tooyour IoT 허브에서 보낸 메시지를 모니터링할 수 있도록 합니다.
- _클라우드-장치 보내기_ IoT 허브에서 tooyour 장치 메시지를 보낼 수 있도록 합니다.

구성 프로그램 `IoT hub connection string` 이 도구 toouse 내에서 모든 기능입니다.

### <a name="iot-hub-explorer"></a>IoT hub Explorer
[IoT 허브 탐색기](https://github.com/Azure/iothub-explorer) 샘플 다중 플랫폼 CLI 도구 toomanage 장치 클라이언트입니다. Hello id 레지스트리에의 hello 도구 toomanage hello 장치를 사용 하 고, 장치-클라우드 메시지를 모니터링 하 고, 클라우드-장치 명령을 보낼 수 있습니다.

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

## <a name="azure-storage-issues"></a>Azure Storage 문제
[Microsoft Azure 저장소 탐색기 (미리 보기)](http://storageexplorer.com) toowork와 사용할 수 있는 Microsoft에서 독립 실행형 응용 프로그램은 [Azure 저장소](https://azure.microsoft.com/en-us/services/storage/) 창, macOS 등 및 Linux에 대 한 데이터입니다. 이 도구를 사용 하 여 tooyour 테이블을 연결 하 고 그 안에 hello 데이터를 확인할 수 있습니다. 이 도구 tootroubleshoot Azure 저장소 문제를 사용할 수 있습니다.

## <a name="next-steps"></a>다음 단계
이 페이지에는 Intel Edison 키트의 가장 일반적인 문제 hello만 포함 됩니다. 또한 자세한 문제 해결에 대 한 tooreport 문제 아래쪽 메모를 둘 수 있습니다.

너무 돌아가서[Intel Edison (Node.js) 시작](iot-hub-intel-edison-kit-node-get-started.md)

<!-- Images and links -->

[sample-repository]: https://github.com/Azure-Samples/iot-hub-node-edison-getting-started