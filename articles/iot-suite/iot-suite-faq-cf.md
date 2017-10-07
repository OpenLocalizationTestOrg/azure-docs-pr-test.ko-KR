---
title: "aaaAzure IoT Suite 연결 팩터리 FAQ | Microsoft Docs"
description: "IoT Suite 연결된 팩터리에 대한 질문과 대답"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: 4ae9beb0daf1b0578850cd652eaca7635b0d039d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-iot-suite-connected-factory-preconfigured-solution"></a>IoT Suite 연결된 팩터리 미리 구성된 솔루션에 대한 질문과 대답

참고 항목, 일반 hello [FAQ](iot-suite-faq.md) IoT Suite에 대 한 합니다.

### <a name="where-can-i-find-hello-source-code-for-hello-preconfigured-solution"></a>미리 구성 하는 hello 솔루션에 대 한 hello 소스 코드는 어디서 찾을 수 있습니까?

hello 소스 코드는 다음 GitHub 리포지토리 hello에 저장 됩니다.

* [연결된 팩터리 미리 구성된 솔루션](https://github.com/Azure/azure-iot-connected-factory)

### <a name="what-is-opc-ua"></a>OPC UA란?

2008년에 발표된 OPC UA(통합 아키텍처)는 플랫폼 독립적이며 서비스 지향 상호 운용성 표준입니다. OPC UA는 산업 PC, PLC 및 센서와 같은 다양한 산업 시스템 및 장치에서 사용됩니다. OPC UA 기본 제공 보안 hello OPC 클래식 사양의 hello 기능 하나의 확장 가능한 프레임 워크에 통합합니다. 이것은 OPC Foundation hello에 의해 발생 하는 표준입니다. hello [OPC Foundation](http://opcfoundation.org/) 이상 440 구성원과 수익에 대 한 not 조직입니다. hello hello 조직의 ´ ֲ toouse OPC 사양 toofacilitate 여러 공급 업체, 다중 플랫폼, 보안 및 신뢰할 수 있는 상호 운용성을 통해:

* 인프라
* 사양
* 기술
* 프로세스

### <a name="why-did-microsoft-choose-opc-ua-for-hello-connected-factory-preconfigured-solution"></a>이유 않은 Microsoft 선택 hello에 대 한 OPC UA 미리 구성 하는 팩터리 솔루션 연결 하나요?

Microsoft는 플랫폼 독립적이고 업계에서 통용되며 입증된 오픈 비독점 표준인 OPC UA를 선택했습니다. 광범위한 제조 프로세스 및 장비 간의 상호 운용성을 보장하는 Industrie 4.0(RAMI4.0) 참조 아키텍처 솔루션을 위해 이 제품이 필요합니다. Microsoft는 고객 toobuild Industrie 4.0 솔루션에서 요청을 볼 수 있습니다. OPC UA에 대 한 지원 tooachieve 고객에 대 한 낮은 hello 장벽 목표를 사용 하 고 비즈니스 값 toothem를 제공 합니다.

### <a name="how-do-i-add-a-public-ip-address-toohello-simulation-vm"></a>공용 IP 주소 toohello 시뮬레이션 VM을 추가 하려면 어떻게 해야 합니까?

두 옵션 tooadd hello IP 주소가:

* Hello PowerShell 스크립트를 사용 하 여 `Simulation/Factory/Add-SimulationPublicIp.ps1` hello에 [리포지토리](https://github.com/Azure/azure-iot-connected-factory)합니다. 배포 이름을 매개 변수로 전달합니다. 로컬 배포의 경우 `<your username>ConnFactoryLocal`을 사용합니다. hello 스크립트 hello VM의 IP 주소 hello 출력합니다.

* Hello Azure 포털에서에서 배포의 hello 리소스 그룹을 찾습니다. 로컬 배포의 경우를 제외 하 고 hello 리소스 그룹에 지정한 솔루션으로 hello 이름 또는 배포 이름. Hello 빌드 스크립트를 사용 하 여 로컬 배포에 대 한 hello hello 리소스 그룹 이름은 `<your username>ConnFactoryLocal`합니다. 이제 새 추가할 **공용 IP 주소** toohello 될 리소스 그룹입니다.

> [!NOTE]
> 두 경우 모두 hello 최신 패치 hello에 대 한 hello 지침에 따라 설치를 확인 [Ubuntu 웹 사이트](https://wiki.ubuntu.com/Security/Upgrades)합니다. VM은 공용 IP 주소를 통해 액세스할 수 있는 상태로 hello 설치에 대 한 toodate 유지 합니다.

### <a name="how-do-i-remove-hello-public-ip-address-toohello-simulation-vm"></a>Hello 공용 IP 주소 toohello 시뮬레이션 VM을 제거 하려면 어떻게 해야 합니까?

두 옵션 tooremove hello IP 주소가:

* PowerShell 스크립트의 hello Simulation/Factory/Remove-SimulationPublicIp.ps1 hello를 사용 하 여 [리포지토리](https://github.com/Azure/azure-iot-connected-factory)합니다. 배포 이름을 매개 변수로 전달합니다. 로컬 배포의 경우 `<your username>ConnFactoryLocal`을 사용합니다. hello 스크립트 hello VM의 IP 주소 hello 출력합니다.

* Hello Azure 포털에서에서 배포의 hello 리소스 그룹을 찾습니다. 로컬 배포의 경우를 제외 하 고 hello 리소스 그룹에 지정한 솔루션으로 hello 이름 또는 배포 이름. Hello 빌드 스크립트를 사용 하 여 로컬 배포에 대 한 hello hello 리소스 그룹 이름은 `<your username>ConnFactoryLocal`합니다. 이제 제거할 hello **공용 IP 주소** hello 리소스 그룹에서 리소스입니다.

### <a name="how-do-i-sign-in-toohello-simulation-vm"></a>Toohello 시뮬레이션 VM에에서 등록 하려면 어떻게 해야 하나요?

Hello PowerShell 스크립트를 사용 하 여 솔루션을 배포한 경우에 지원 됩니다 toohello 시뮬레이션 VM에에서 로그인 `build.ps1` hello에 [리포지토리](https://github.com/Azure/azure-iot-connected-factory)합니다.

Www.azureiotsuite.com에서 hello 솔루션을 배포한 경우 toohello VM에에서 로그인 할 수 없습니다. 사용자 로그인 할 수 없습니다, hello 암호는 임의로 생성 되 고 다시 설정할 수 없습니다.

1. 공용 IP 주소 toohello VM을 추가 합니다. 참조 [공용 IP 주소 toohello 시뮬레이션 VM을 어떻게 추가 합니까?](#how-do-i-remove-the-public-ip-address-to-the-simulation-vm)
1. SSH 세션 tooyour VM 만들기 hello VM의 hello IP 주소를 사용 합니다.
1. hello username toouse은: `docker`합니다.
1. hello 암호 toouse toodeploy를 사용 하는 hello 버전에 따라 다릅니다.
    * Hello 암호는 1 년 6 월 2017 하기 전에 hello build.ps1 스크립트를 사용 하 여 배포할 솔루션의 경우: `Passw0rd`합니다.
    * 1 년 6 월 2017 후 hello build.ps1 스크립트를 사용 하 여 배포할 솔루션의 경우 hello 암호 hello에서 찾을 수 있습니다 `<name of your deployment>.config.user` 파일입니다. hello 암호는 hello에 저장 **VmAdminPassword** 설정 합니다. hello 암호는 임의로 생성 배포 시 hello를 사용 하 여 지정 하지 않으면 `build.ps1` 매개 변수를 스크립팅 합니다.`-VmAdminPassword`

### <a name="how-do-i-stop-and-start-all-docker-processes-in-hello-simulation-vm"></a>어떻게 중지 하 고 hello 시뮬레이션 VM의에서 모든 docker 프로세스 시작?

1. Toohello 시뮬레이션 VM에에서 로그인 합니다. 참조 [toohello 시뮬레이션 VM에에서 등록 하려면 어떻게는 하나요?](#how-do-i-sign-in-to-the-simulation-vm)
1. 컨테이너 상태인 toocheck 실행: `docker ps`합니다.
1. toostop 모든 시뮬레이션 컨테이너 실행: `./stopsimulation`합니다.
1. toostart 모든 시뮬레이션 컨테이너:
    * Hello 이름의 셸 변수를 내보내기 **IOTHUB_CONNECTIONSTRING**합니다. Hello hello 값을 사용 하 여 **IotHubOwnerConnectionString** hello에서 설정 `<name of your deployment>.config.user` 파일입니다. 예:

        ```
        export IOTHUB_CONNECTIONSTRING="HostName={yourdeployment}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={your key}"
        ```

    * `./startsimulation`을 실행합니다.

### <a name="how-do-i-update-hello-simulation-in-hello-vm"></a>Hello VM에서에서 hello 시뮬레이션을 업데이트 하려면 어떻게 해야 합니까?

Hello PowerShell 스크립트를 사용 하면 변경한 경우 변경 내용을 toohello 시뮬레이션을 `build.ps1` hello에 [리포지토리](https://github.com/Azure/azure-iot-connected-factory) hello를 사용 하 여 `updatedimulation` 명령입니다. 이 스크립트 모든 hello 시뮬레이션 구성 요소를 작성, hello VM에서에서 hello 시뮬레이션을 중지, 업로드는 설치 및 시작 합니다.

### <a name="how-do-i-find-out-hello-connection-string-of-hello-iot-hub-used-by-my-solution"></a>솔루션 내에서 사용 하는 hello IoT 허브의 hello 연결 문자열을 찾으려면 어떻게 해야 합니까?

Hello로 솔루션을 배포한 경우 `build.ps1` hello에서 스크립트 [리포지토리](https://github.com/Azure/azure-iot-connected-factory), hello 연결 문자열의 hello 값은 **IotHubOwnerConnectionString** hello에 `<name of your deployment>.config.user` 파일입니다.

또한 hello Azure 포털을 사용 하 여 hello 연결 문자열을 찾을 수 있습니다. IoT Hub 리소스 hello 리소스 그룹 배포의 hello hello 연결 문자열 설정을 찾습니다.

### <a name="which-iot-hub-devices-does-hello-connected-factory-simulation-use"></a>IoT Hub 장치에 연결 된 팩터리 시뮬레이션 사용 hello가?

자체를 등록 하는 시뮬레이션 hello hello 다음 장치:

* proxy.beijing.corp.contoso
* proxy.capetown.corp.contoso
* proxy.mumbai.corp.contoso
* proxy.munich0.corp.contoso
* proxy.rio.corp.contoso
* proxy.seattle.corp.contoso
* publisher.beijing.corp.contoso
* publisher.capetown.corp.contoso
* publisher.mumbai.corp.contoso
* publisher.munich0.corp.contoso
* publisher.rio.corp.contoso
* publisher.seattle.corp.contoso

Hello를 사용 하 여 [DeviceExplorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) 또는 [iothub 탐색기](https://github.com/azure/iothub-explorer) 도구를 장치에 등록 된 솔루션을 사용 하 여 hello IoT hub를 확인할 수 있습니다. 이러한 도구는 toouse, hello 연결 문자열이 필요한 hello IoT 허브에 대 한 배포에 합니다.

### <a name="how-can-i-get-log-data-from-hello-simulation-components"></a>Hello 시뮬레이션 구성 요소에서 로그 데이터는 어떻게 얻을 수 있습니까?

Hello 시뮬레이션의 모든 구성 요소는 toolog 파일에서 정보를 기록 합니다. 이러한 파일에에서 있습니다 hello VM hello 폴더에 `home/docker/Logs`합니다. tooretrieve hello 로그 hello PowerShell 스크립트를 사용할 수 있습니다 `Simulation/Factory/Get-SimulationLogs.ps1` hello에 [리포지토리](https://github.com/Azure/azure-iot-connected-factory)합니다.

이 스크립트는 toosign toohello VM에에서 필요합니다. Hello에 대 한 로그인에 대 한 tooprovide 자격 증명을 할 수 있습니다. 참조 [toohello 시뮬레이션 VM에에서 로그인 방법을?](#how-do-i-sign-in-to-the-simulation-vm) toofind hello 자격 증명입니다.

hello 스크립트 추가/제거 공용 IP 주소 toohello VM 아직 없는 경우 제거 합니다. hello 스크립트는 보관 파일의 모든 로그 파일을 저장 하 고 hello 보관 tooyour 개발 워크스테이션을 다운로드 합니다.

또는 toohello SSH 통해 VM에에서 로그인 하 고 런타임 시 hello 로그 파일을 검사 합니다.

### <a name="how-can-i-check-if-hello-simulation-is-sending-data-toohello-cloud"></a>Hello 시뮬레이션 toohello 클라우드 데이터를 보내는 경우 어떻게 확인할 수 있습니까?

Hello로 [DeviceExplorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) 또는 hello [iothub 탐색기](https://github.com/azure/iothub-explorer) 도구, 특정 장치에서 tooIoT 허브 전송 된 hello 데이터를 검사할 수 있습니다. 이러한 도구는 toouse, tooknow hello 연결 문자열이 필요한 hello IoT 허브에 대 한 배포에 합니다. 참조 [방법을 확인 하는 솔루션 내에서 사용 하는 hello IoT hub의 연결 문자열 hello?](#how-do-i-find-out-the-connection-string-of-the-iot-hub-used-by-my-solution)

Hello 게시자 장치 중 하나에서 보낸 hello 데이터를 검사 합니다.

* publisher.beijing.corp.contoso
* publisher.capetown.corp.contoso
* publisher.mumbai.corp.contoso
* publisher.munich0.corp.contoso
* publisher.rio.corp.contoso
* publisher.seattle.corp.contoso

TooIoT 허브 전송 데이터를 볼 경우 없기 hello 시뮬레이션에 문제가 있습니다. 첫 번째 분석 단계 hello 로그 파일의 hello 시뮬레이션 구성 요소를 분석 해야 합니다. 참조 [어떻게 구할 수 있습니까 로그 데이터 hello에서 시뮬레이션 구성 요소가 있습니까?](#how-can-i-get-log-data-from-the-simulation-components) 다음으로 toostop hello 시뮬레이션을 시작 하 고 전송 된 데이터는 여전히, 경우 hello 시뮬레이션을 완전히 업데이트 합니다. 참조 [hello VM에서에서 hello 시뮬레이션을 업데이트 하려면 어떻게 합니까?](#how-do-i-update-the-simulation-in-the-vm)

### <a name="next-steps"></a>다음 단계

탐색할 수도 있습니다 hello 중 일부 다른 기능 및 hello IoT Suite 미리 구성 된 솔루션의 기능:

* [예측 유지 관리 사전 구성 솔루션 개요](iot-suite-predictive-overview.md)
* [연결된 팩터리 미리 구성된 솔루션 개요](iot-suite-connected-factory-overview.md)
* [Hello 접지에서 IoT 보안](securing-iot-ground-up.md)
