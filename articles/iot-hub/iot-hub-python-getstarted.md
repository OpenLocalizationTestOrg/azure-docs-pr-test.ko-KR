---
title: "Azure IoT Hub (Python) aaaGet 시작 | Microsoft Docs"
description: "Toosend 장치-클라우드 tooAzure IoT Sdk를 사용 하 여 Python에 대 한 IoT Hub를 메시지 하는 방법을 알아봅니다. 시뮬레이션 된 장치 및 서비스 응용 프로그램 tooregister 장치, 메시지를 보낼 만들고 IoT 허브에서 메시지를 읽은 합니다."
services: iot-hub
author: dsk-2015
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: python
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: dkshir
ms.custom: na
ms.openlocfilehash: aa23e792fb144202e121274723bcfaeae0c04723
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-python"></a>Python을 사용 하 여 시뮬레이션 된 장치 tooyour IoT 허브를 연결 합니다.
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

이 자습서의 hello 끝 두 Python 응용 프로그램 해야 합니다.

* **CreateDeviceIdentity.py**, 장치 id를 만듦 및 연결 된 보안 키 tooconnect 시뮬레이션 된 장치 앱.
* **SimulatedDevice.py**앞에서 만든 hello 장치 id를 가진 tooyour IoT 허브를 연결 하는, 및 원격 분석 전송할 hello MQTT 프로토콜을 사용 하 여 메시지 주기적으로 합니다.

> [!NOTE]
> hello 문서 [Azure IoT Sdk] [ lnk-hub-sdks] 사용할 수 있는 toobuild 두 응용 프로그램 toorun 장치와 솔루션 백 엔드에, Azure IoT Sdk hello에 대 한 정보를 제공 합니다.
> 
> 

toocomplete이이 자습서에서는 다음 hello 필요:

* [Python 2.x 또는 3.x][lnk-python-download]. 있는지 toouse hello 32 비트 또는 64 비트 설치 프로그램 설치 프로그램에서 필요에 따라 확인 합니다. Hello 설치 하는 동안 대화 상자가 나타나면 있는지 tooadd Python tooyour 플랫폼 특정 환경 변수를 확인 합니다. Python을 사용 하는 경우 2.x를 할 수 있습니다 너무[설치 또는 업그레이드 *pip*, hello Python 패키지 관리 시스템][lnk-install-pip]합니다.
* 다음 Windows 운영 체제를 사용 하는 경우 [Visual c + + 재배포 가능 패키지] [ lnk-visual-c-redist] Python에서 네이티브 Dll tooallow hello 사용 합니다.
* [Node.js 4.0 이상][lnk-node-download]. 있는지 toouse hello 32 비트 또는 64 비트 설치 프로그램 설치 프로그램에서 필요에 따라 확인 합니다. 이 필요한 tooinstall hello [IoT 허브 탐색기 도구][lnk-iot-hub-explorer]합니다.
* 활성 Azure 계정. 계정이 없는 경우 몇 분 내에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.

> [!NOTE]
> hello *pip* 패키지로 `azure-iothub-service-client` 및 `azure-iothub-device-client` 현재 Windows 운영 체제에 대해서만 사용할 수 있습니다. Linux/Mac OS hello에 toohello Linux 및 Mac OS 관련 섹션을 참조 하십시오 [Python에 대 한 개발 환경을 준비] [ lnk-python-devbox] 게시 합니다.
> 

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

IoT Hub를 만들었습니다. 이 자습서의 나머지 부분 hello hello IoT Hub 호스트 이름 및 hello IoT 허브 연결 문자열을 사용 합니다.

> [!NOTE]
> 또한 또는 만들 수 있습니다 IoT hub 명령줄에서 Python hello를 사용 하 여 Node.js Azure CLI를 기반으로 합니다. hello 문서 [hello Azure CLI 2.0을 사용 하 여 IoT 허브를 만듭니다.] [ lnk-azure-cli-hub] toodo 빠른 단계를 따라서 hello 보여 줍니다. 
> 

## <a name="create-a-device-identity"></a>장치 ID 만들기
이 섹션에서는 hello 단계 toocreate hello id 레지스트리에 IoT 허브에서 장치 id를 작성 하는 Python 콘솔 앱을 나열 합니다. 장치는 hello identity 레지스트리에 항목을 설정한 경우에 tooIoT 허브를 연결할 수 있습니다. 자세한 내용은 참조 hello **Id 레지스트리에** hello 섹션 [IoT 허브 개발자 가이드][lnk-devguide-identity]합니다. 이 콘솔 응용 프로그램을 실행 하면 고유한 장치 ID를 생성 및 메시지 tooIoT 허브를 키 장치-클라우드 보낼 때 장치가 tooidentify 자체를 사용할 수 있습니다.

1. 명령 프롬프트를 열고 hello 설치 **Python 용 Azure IoT 허브 서비스 SDK**합니다. Hello SDK를 설치한 후 hello 명령 프롬프트를 닫습니다.

    ```
    pip install azure-iothub-service-client
    ```

2. **CreateDeviceIdentity.py**라는 이름의 Python 파일을 만듭니다. 열 [Python 편집기/IDE를 원하는][lnk-python-ide-list], 예를 들어 기본 hello [IDLE][lnk-idle]합니다.

3. Hello 코드 tooimport hello 필요한 모듈 hello 서비스 SDK에서에서 다음을 추가 합니다.

    ```python
    import sys
    import iothub_service_client
    from iothub_service_client import IoTHubRegistryManager, IoTHubRegistryManagerAuthMethod
    from iothub_service_client import IoTHubDeviceStatus, IoTHubError
    ```
2. 추가 코드 다음, hello 자리 표시자에 대 한 대체 hello `[IoTHub Connection String]` hello 이전 섹션에서 만든 hello IoT 허브에 대 한 hello 연결 문자열을 사용 합니다. Hello로 모든 이름을 사용할 수 있습니다 `DEVICE_ID`합니다.
   
    ```python
    CONNECTION_STRING = "[IoTHub Connection String]"
    DEVICE_ID = "MyFirstPythonDevice"
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

3. 추가 함수 tooprint 다음 hello 장치 정보 중 일부 hello 합니다.

    ```python
    def print_device_info(title, iothub_device):
        print ( title + ":" )
        print ( "iothubDevice.deviceId                    = {0}".format(iothub_device.deviceId) )
        print ( "iothubDevice.primaryKey                  = {0}".format(iothub_device.primaryKey) )
        print ( "iothubDevice.secondaryKey                = {0}".format(iothub_device.secondaryKey) )
        print ( "iothubDevice.connectionState             = {0}".format(iothub_device.connectionState) )
        print ( "iothubDevice.status                      = {0}".format(iothub_device.status) )
        print ( "iothubDevice.lastActivityTime            = {0}".format(iothub_device.lastActivityTime) )
        print ( "iothubDevice.cloudToDeviceMessageCount   = {0}".format(iothub_device.cloudToDeviceMessageCount) )
        print ( "iothubDevice.isManaged                   = {0}".format(iothub_device.isManaged) )
        print ( "iothubDevice.authMethod                  = {0}".format(iothub_device.authMethod) )
        print ( "" )
    ```
3. Hello 함수 toocreate hello 장치 식별 hello 레지스트리 관리자를 사용 하 여 다음을 추가 합니다. 

    ```python
    def iothub_createdevice():
        try:
            iothub_registry_manager = IoTHubRegistryManager(CONNECTION_STRING)
            auth_method = IoTHubRegistryManagerAuthMethod.SHARED_PRIVATE_KEY
            new_device = iothub_registry_manager.create_device(DEVICE_ID, "", "", auth_method)
            print_device_info("CreateDevice", new_device)

        except IoTHubError as iothub_error:
            print ( "Unexpected error {0}".format(iothub_error) )
            return
        except KeyboardInterrupt:
            print ( "iothub_createdevice stopped" )
    ```
4. 마지막으로 다음과 같이 hello main 함수를 추가 하 고 hello 파일을 저장 합니다.

    ```python
    if __name__ == '__main__':
        print ( "" )
        print ( "Python {0}".format(sys.version) )
        print ( "Creating device using hello Azure IoT Hub Service SDK for Python" )
        print ( "" )
        print ( "    Connection string = {0}".format(CONNECTION_STRING) )
        print ( "    Device ID         = {0}".format(DEVICE_ID) )

        iothub_createdevice()
    ```
5. Hello 명령 프롬프트에서 실행 hello **CreateDeviceIdentity.py** 다음과 같습니다.

    ```python
    python CreateDeviceIdentity.py
    ```
6. 만든 가져오는 hello 시뮬레이션 된 장치에 표시 됩니다. Hello 기록해 **deviceId** 및 hello **primaryKey** 이 장치의 합니다. 이 값이 필요 하면 이러한 나중 tooIoT 장치로 허브를 연결 하는 응용 프로그램을 만들 때.

    ![장치 만들기 성공][1]

> [!NOTE]
> IoT Hub id 레지스트리에 hello만 장치 identities tooenable 보안 액세스 toohello IoT 허브를 저장합니다. 장치 Id와 키 toouse 보안 자격 증명 및 개별 장치에 대 한 toodisable 액세스를 사용할 수 있는 사용/사용 안 함 플래그로 저장 합니다. 응용 프로그램는 toostore 다른 장치 관련 메타 데이터를 필요한 경우에 응용 프로그램별 저장소를 사용 해야 합니다. 자세한 내용은 참조 hello [IoT 허브 개발자 가이드][lnk-devguide-identity]합니다.
> 
> 


## <a name="create-a-simulated-device-app"></a>시뮬레이션된 장치 앱 만들기
이 섹션에는 hello 단계 toocreate 시뮬레이트하는 장치 및 장치-클라우드 메시지 tooyour IoT 허브를 전송 하는 Python 콘솔 앱, 나열 됩니다.

1. 새 명령 프롬프트를 열고 다음과 같이 Python에 대 한 hello Azure IoT 허브 장치 SDK를 설치 합니다. Hello 설치 후 hello 명령 프롬프트를 닫습니다.

    ```
    pip install azure-iothub-device-client
    ```
2. **SimulatedDevice.py**라는 이름의 파일을 만듭니다. 원하는 Python 편집기/IDE(예: IDLE)에서 이 파일을 엽니다.

3. Hello 코드 tooimport hello 필요한 모듈 hello 장치 SDK에서에서 다음을 추가 합니다.

    ```python
    import random
    import time
    import sys
    import iothub_client
    from iothub_client import IoTHubClient, IoTHubClientError, IoTHubTransportProvider, IoTHubClientResult
    from iothub_client import IoTHubMessage, IoTHubMessageDispositionResult, IoTHubError, DeviceMethodReturnValue
    ```
4. Hello 다음 코드로 바꾸고 hello 자리 표시자에 대 한 대체 추가 `[IoTHub Device Connection String]` 장치에 대 한 hello 연결 문자열을 사용 합니다. 장치 연결 문자열 hello는 일반적으로의 hello 형식 `HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`합니다. 사용 하 여 hello **deviceId** 및 **primaryKey** hello 이전 섹션 tooreplace hello에서 만든 hello 장치의 `<deviceId>` 및 `<primaryKey>` 각각. `<hostName>`을 IoT Hub의 호스트 이름으로 바꿉니다. 일반적으로 `<IoT hub name>.azure-devices.net`입니다.

    ```python
    # String containing Hostname, Device Id & Device Key in hello format
    CONNECTION_STRING = "[IoTHub Device Connection String]"
    # choose HTTP, AMQP or MQTT as transport protocol
    PROTOCOL = IoTHubTransportProvider.MQTT
    MESSAGE_TIMEOUT = 10000
    AVG_WIND_SPEED = 10.0
    SEND_CALLBACKS = 0
    MSG_TXT = "{\"deviceId\": \"MyFirstPythonDevice\",\"windSpeed\": %.2f}"    
    ```
5. 다음 코드 toodefine 송신 확인 콜백 hello를 추가 합니다. 

    ```python
    def send_confirmation_callback(message, result, user_context):
        global SEND_CALLBACKS
        print ( "Confirmation[%d] received for message with result = %s" % (user_context, result) )
        map_properties = message.properties()
        print ( "    message_id: %s" % message.message_id )
        print ( "    correlation_id: %s" % message.correlation_id )
        key_value_pair = map_properties.get_internals()
        print ( "    Properties: %s" % key_value_pair )
        SEND_CALLBACKS += 1
        print ( "    Total calls confirmed: %d" % SEND_CALLBACKS )
    ```
6. 다음 코드 tooinitialize hello 장치 클라이언트 hello를 추가 합니다.

    ```python
    def iothub_client_init():
        # prepare iothub client
        client = IoTHubClient(CONNECTION_STRING, PROTOCOL)
        # set hello time until a message times out
        client.set_option("messageTimeout", MESSAGE_TIMEOUT)
        client.set_option("logtrace", 0)
        return client
    ```
7. Hello 다음 tooformat 작동을 시뮬레이션 된 장치 tooyour IoT 허브에서 메시지를 보냅니다를 추가 합니다.

    ```python
    def iothub_client_telemetry_sample_run():

        try:
            client = iothub_client_init()
            print ( "IoT Hub device sending periodic messages, press Ctrl-C tooexit" )
            message_counter = 0

            while True:
                msg_txt_formatted = MSG_TXT % (AVG_WIND_SPEED + (random.random() * 4 + 2))
                # messages can be encoded as string or bytearray
                if (message_counter & 1) == 1:
                    message = IoTHubMessage(bytearray(msg_txt_formatted, 'utf8'))
                else:
                    message = IoTHubMessage(msg_txt_formatted)
                # optional: assign ids
                message.message_id = "message_%d" % message_counter
                message.correlation_id = "correlation_%d" % message_counter
                # optional: assign properties
                prop_map = message.properties()
                prop_text = "PropMsg_%d" % message_counter
                prop_map.add("Property", prop_text)

                client.send_event_async(message, send_confirmation_callback, message_counter)
                print ( "IoTHubClient.send_event_async accepted message [%d] for transmission tooIoT Hub." % message_counter )

                status = client.get_send_status()
                print ( "Send status: %s" % status )
                time.sleep(30)

                status = client.get_send_status()
                print ( "Send status: %s" % status )

                message_counter += 1

        except IoTHubError as iothub_error:
            print ( "Unexpected error %s from IoTHub" % iothub_error )
            return
        except KeyboardInterrupt:
            print ( "IoTHubClient sample stopped" )
    ```
8. 마지막으로 hello main 함수를 추가 합니다. 

    ```python
    if __name__ == '__main__':
        print ( "Simulating a device using hello Azure IoT Hub Device SDK for Python" )
        print ( "    Protocol %s" % PROTOCOL )
        print ( "    Connection string=%s" % CONNECTION_STRING )

        iothub_client_telemetry_sample_run()
    ```
9. 저장 후 닫기 hello **SimulatedDevice.py** 파일입니다. 사용자는 이제 준비 toorun이 응용이 프로그램입니다.

> [!NOTE]
> 단순 tookeep 항목을이 자습서는 어떠한 재시도 정책도 구현 하지 않습니다. 프로덕션 코드에서는 hello MSDN 문서에 설명 된 대로 다시 시도 정책 (예: 지 수 백오프)를 구현 해야 [일시적인 오류 처리][lnk-transient-faults]합니다.
> 
> 

## <a name="receive-messages-from-your-simulated-device"></a>시뮬레이션된 장치에서 메시지 받기
장치에서 원격 분석 메시지 tooreceive 해야 toouse는 [이벤트 허브][lnk-event-hubs-overview]-호환 되는 hello hello 장치-클라우드 메시지를 읽는 IoT 허브에 의해 노출 된 끝점입니다. 읽기 hello [이벤트 허브 시작] [ lnk-eventhubs-tutorial] IoT 허브의 이벤트 허브 호환 끝점에 대 한 이벤트 허브에서 메시지 tooprocess 방법을 대 한 정보에 대 한 자습서입니다. 이벤트 허브 아직 지원 하지 않는 원격 분석에서 Python, 하거나 만들 수 있도록 한 [Node.js](iot-hub-node-node-getstarted.md#D2C_node) 또는 [.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp) IoT 허브에서 이벤트 허브 기반 콘솔 앱 tooread hello 장치-클라우드 메시지입니다. Hello를 사용 하는 방법을 보여 주는이 자습서 [IoT 허브 탐색기 도구] [ lnk-iot-hub-explorer] tooread 이러한 장치 메시지입니다.

1. 명령 프롬프트를 열고 hello IoT 허브 탐색기를 설치 합니다. 

    ```
    npm install -g iothub-explorer
    ```

2. Hello hello 명령 프롬프트에 다음 명령을 실행 하면 장치에서 장치-클라우드 메시지 hello toobegin 모니터링 합니다. IoT 허브의 연결 문자열을 사용 하 여 후 hello 자리 표시자의 `--login`합니다.

    ```
    iothub-explorer monitor-events MyFirstPythonDevice --login "[IoTHub connection string]"
    ```

3. 새 명령 프롬프트를 열고 hello를 포함 하는 toohello 디렉터리 **SimulatedDevice.py** 파일입니다.

4. Hello 실행 **SimulatedDevice.py** 원격 분석 데이터 tooyour IoT 허브를 주기적으로 전송 하는 파일입니다. 
   
    ```
    python SimulatedDevice.py
    ```
5. Hello 이전 섹션에서 hello IoT 허브 탐색기를 실행 하는 hello 명령 프롬프트에 hello 장치 메시지를 관찰 합니다. 

    ![Python 장치-클라우드 메시지][2]

## <a name="next-steps"></a>다음 단계
이 자습서에서는 hello Azure 포털에서에서 새 IoT 허브를 구성 하 고 id 레지스트리에 hello IoT hub에서 장치 id를 만든 다음 합니다. 이 장치 identity tooenable hello 시뮬레이션 된 장치 앱 toosend 장치-클라우드 메시지 toohello IoT 허브를 사용 했습니다. Hello 메시지를 사용 하 여 hello hello IoT 허브 탐색기 도구 hello IoT 허브에서 받은 준수 합니다. 

심층, Azure IoT Hub 사용에 대 한 Python SDK tooexplore hello 방문 [이 허브 Git 리포지토리에][lnk-python-github]합니다. hello Python 용 Azure IoT 허브 서비스 SDK의 tooreview hello의 메시징 기능을 다운로드 하 고 실행할 수 [iothub_messaging_sample.py][lnk-messaging-sample]합니다. Python 용 Azure IoT 허브 장치 SDK hello를 사용 하 여 장치 쪽 시뮬레이션에 대 한 다운로드 하 고 실행할 수 hello [iothub_client_sample.py][lnk-client-sample]합니다.

시작 toocontinue IoT 허브와 tooexplore 다른 IoT 시나리오를 참조 하세요.

* [장치 연결][lnk-connect-device]
* [장치 관리 시작][lnk-device-management]
* [Azure IoT Hub 시작][lnk-iot-edge]

toolearn tooextend 배율 사용할 때 IoT 솔루션 및 프로세스 장치-클라우드 메시지를 확인 하려면 어떻게 hello [장치-클라우드 메시지를 처리] [ lnk-process-d2c-tutorial] 자습서입니다.
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[1]: ./media/iot-hub-python-getstarted/createdevice.png
[2]: ./media/iot-hub-python-getstarted/sendd2cmessage.png

<!-- Links -->
[lnk-python-download]: https://www.python.org/downloads/
[lnk-visual-c-redist]: http://www.microsoft.com/download/confirmation.aspx?id=48145
[lnk-node-download]: https://nodejs.org/en/download/
[lnk-install-pip]: https://pip.pypa.io/en/stable/installing/
[lnk-azure-cli-hub]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-create-using-cli
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-idle]: https://docs.python.org/3/library/idle.html
[lnk-python-ide-list]: https://wiki.python.org/moin/IntegratedDevelopmentEnvironments
[lnk-iot-hub-explorer]: https://github.com/Azure/iothub-explorer
[lnk-python-github]: https://github.com/Azure/azure-iot-sdk-python
[lnk-messaging-sample]: https://github.com/Azure/azure-iot-sdk-python/blob/master/service/samples/iothub_messaging_sample.py
[lnk-client-sample]: https://github.com/Azure/azure-iot-sdk-python/blob/master/device/samples/iothub_client_sample.py

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md
[lnk-python-devbox]: https://github.com/Azure/azure-iot-sdk-python/blob/master/doc/python-devbox-setup.md

[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
