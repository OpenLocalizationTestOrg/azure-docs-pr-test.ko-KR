---
title: "aaaConnect 라스베리 Pi tooAzure C toosupport 펌웨어를 사용 하 여 IoT Suite 업데이트 | Microsoft Docs"
description: "Hello 라스베리 Pi 3에 대 한 Microsoft Azure IoT 시작 키트 hello와, Azure IoT Suite를 사용 합니다. C tooconnect 프로그램 라스베리 Pi toohello 원격 모니터링 솔루션을 사용 하 고 toohello 클라우드 센서에서 원격 분석을 전송 원격 펌웨어 업데이트를 수행 합니다."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 36d39c6d754ddb025fd3f6b74d7795ed907b754c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-enable-remote-firmware-updates-using-c"></a>원격 모니터링 솔루션 라스베리 Pi 3 toohello 사용자를 연결 하 고 C를 사용 하 여 원격 펌웨어 업데이트를 사용 하도록 설정

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

이 자습서 toouse 라스베리 Pi 3에 대 한 Microsoft Azure IoT 시작 키트를 hello 하는 방법을 보여 줍니다.

* Hello 클라우드와 통신할 수 있는 온도 및 습도 판독기를 개발 합니다.
* 사용 하도록 설정 하 고 hello 라스베리 Pi에서 원격 펌웨어 업데이트 tooupdate hello 클라이언트 응용 프로그램을 수행 합니다.

hello 자습서를 사용합니다.

* Raspbian OS, hello C 프로그래밍 언어 및 C tooimplement 샘플 장치에 대 한 Microsoft Azure IoT SDK hello 합니다.
* hello IoT Suite 원격 모니터링 솔루션 hello 클라우드 기반 백 엔드 응용 프로그램으로 미리 구성 합니다.

## <a name="overview"></a>개요

이 자습서의 단계를 수행 하는 hello를 완료 합니다.

* Hello 원격 모니터링 미리 구성 된 솔루션 tooyour Azure 구독의 인스턴스를 배포 합니다. 이 단계에서는 여러 Azure 서비스를 자동으로 배포하고 구성합니다.
* 설정 하면 장치 및 센서 toocommunicate 컴퓨터 및 hello와 원격 솔루션 모니터링 합니다.
* Hello 샘플 장치 코드 tooconnect toohello 원격 모니터링 솔루션을 업데이트 하 고 hello 솔루션 대시보드에서 볼 수 있는 원격 분석을 보냅니다.
* Hello 샘플 장치 코드 tooupdate hello 클라이언트 응용 프로그램을 사용 합니다.

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> 원격 hello 솔루션 프로 비전 한 일련의 Azure 구독에서 Azure 서비스를 모니터링합니다. hello 배포 실제 엔터프라이즈 아키텍처를 반영합니다. 종료 되었음을 tooavoid 불필요 한 Azure 사용료가 부과 azureiotsuite.com에 hello 미리 구성 된 솔루션의 인스턴스를 삭제 합니다. 미리 구성 된 솔루션을 다시 hello 필요, 있습니다 쉽게 다시 만들 수 있습니다. Hello 원격 솔루션 실행을 모니터링 하는 동안 소비 감소 하는 방법에 대 한 자세한 내용은 참조 [데모 목적에 대 한 솔루션을 미리 구성 된 Azure IoT Suite 구성][lnk-demo-config]합니다.

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a>다운로드 하 고 hello 샘플 구성

이제 다운로드 하 고 라스베리 원주율 hello 원격 모니터링 클라이언트 응용 프로그램을 구성할 수 있습니다.

### <a name="clone-hello-repositories"></a>Hello 리포지토리 복제

아직 수행 하지 않은 경우 복제 hello를 실행 하 여 저장소 hello 나오는 명령에 Pi에 필요 합니다.

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a>Hello 장치 연결 문자열 업데이트

Hello에 샘플 구성 파일을 열고 hello **nano** hello 다음 명령을 사용 하 여 편집기:

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

Hello 장치 ID 및 IoT 허브 정보를 만들고이 자습서의 hello 시작 시 저장 hello 자리 표시자 값을 대체 합니다.

완료 되 면 다음 예제는 hello 같이 hello hello deviceinfo 파일 내용의 표시 됩니다.

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

변경 내용을 저장 (**Ctrl-O**, **Enter**) 및 exit hello 편집기 (**Ctrl-X**).

## <a name="build-hello-sample"></a>Hello 예제 빌드

이미 수행 하는 경우 C에 대 한 Microsoft Azure IoT 장치 SDK hello에 대 한 필수 구성 요소 패키지가 hello hello 나오는 라스베리 Pi hello에 따라 종료에서 명령을 실행 하 여 설치 합니다.

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

이제 라스베리 Pi hello에 hello 샘플 솔루션을 빌드할 수 있습니다.

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/advanced/1.0/build.sh
```

이제 라스베리 Pi hello에 hello 샘플 프로그램을 실행할 수 있습니다. Hello 명령을 입력 합니다.

  ```sh
  sudo ~/cmake/remote_monitoring/remote_monitoring
  ```

hello 다음 샘플 출력은 hello 라스베리 Pi hello 명령 프롬프트에서 참조 하는 hello 출력 예입니다.

![Raspberry Pi 앱의 출력][img-raspberry-output]

키를 눌러 **Ctrl-c** 언제 든 지 tooexit hello 프로그램입니다.

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-advanced.md)]

1. Hello 솔루션 대시보드 클릭 **장치** toovisit hello **장치** 페이지. Hello에 라스베리 Pi 선택 **장치 목록**합니다. 그런 다음 **메서드**를 선택합니다.

    ![대시보드에서 장치 나열][img-list-devices]

1. Hello에 **메서드 호출** 페이지에서 선택 **InitiateFirmwareUpdate** hello에 **메서드** 드롭다운입니다.

1. Hello에 **FWPackageURI** 필드에, 입력 **https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit/raw/master/advanced/2.0/package/remote_monitoring.zip**합니다. 이 보관 파일에는 hello 펌웨어 버전 2.0의 hello 구현을 포함합니다.

1. **InvokeMethod**를 선택합니다. hello 응용 프로그램에 액세스 hello 라스베리 Pi 승인 백 toohello 솔루션 대시보드를 보냅니다. 다음 hello 펌웨어 hello 새 버전을 다운로드 하 여 hello 펌웨어 업데이트 프로세스를 시작 합니다.

    ![메서드 기록 표시][img-method-history]

## <a name="observe-hello-firmware-update-process"></a>Hello 펌웨어 업데이트 프로세스를 관찰 합니다.

Hello 장치에서 실행 되는 때에 hello 펌웨어 업데이트 프로세스를 확인할 수 및 hello를 확인 하 여 hello 솔루션 대시보드에 속성을 보고 합니다.

1. Hello 라스베리 Pi에 hello 업데이트 프로세스에서 hello 진행 상황을 볼 수 있습니다.

    ![업데이트 진행률 표시][img-update-progress]

    > [!NOTE]
    > hello 업데이트가 완료 되 면 hello 원격 모니터링 응용 프로그램 다시 자동으로 시작 합니다. Hello 명령을 사용 하 여 `ps -ef` tooverify 실행 되 고 있습니다. Hello를 사용 하 여 tooterminate hello 프로세스를 사용 하도록 하려는 경우 `kill` 명령을 hello 프로세스 id입니다.

1. Hello 솔루션 포털에서 hello 장치에서 보고 hello 펌웨어 업데이트의 hello 상태를 볼 수 있습니다. hello 다음 스크린샷은 hello 상태 및 기간이 hello 새로운 펌웨어 버전 및 hello 업데이트 프로세스의 각 단계:

    ![작업 상태 보기][img-job-status]

    뒤로 toohello 대시보드를 탐색 하면 hello 장치에서 여전히 hello 펌웨어 업데이트를 수행 하는 원격 분석을 보내는 것을 확인할 수 있습니다.

> [!WARNING]
> Hello를 모니터링 하 여 Azure 계정에서 실행 되는 솔루션 원격 두면 실행 hello 시간에 대 한 요금이 청구 됩니다. Hello 원격 솔루션 실행을 모니터링 하는 동안 소비 감소 하는 방법에 대 한 자세한 내용은 참조 [데모 목적에 대 한 솔루션을 미리 구성 된 Azure IoT Suite 구성][lnk-demo-config]합니다. 사용을 마쳤으면 Azure 계정에서 hello 미리 구성 된 솔루션을 삭제 합니다.

## <a name="next-steps"></a>다음 단계

Hello 방문 [Azure IoT 개발자 센터](https://azure.microsoft.com/develop/iot/) 에 더 많은 샘플 및 Azure IoT에 대 한 설명서입니다.


[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-raspberry-pi-kit-c-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md