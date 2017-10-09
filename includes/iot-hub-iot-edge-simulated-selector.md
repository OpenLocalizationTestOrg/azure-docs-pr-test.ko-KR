> [!div class="op_single_selector"]
> * [Linux](../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md)
> * [Windows](../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md)

이 연습에서는의 hello [시뮬레이션 된 장치 클라우드 업로드 샘플] 방법을 보여 줍니다 toouse [Azure IoT 가장자리] [ lnk-sdk] 시뮬레이션에서 toosend 장치-클라우드 원격 분석 tooIoT 허브 장치입니다.

이 연습에서는 다음 내용을 다룹니다.

* **아키텍처**: hello에 대 한 아키텍처 정보 [시뮬레이션 된 장치 클라우드 업로드 샘플]합니다.
* **빌드 및 실행**: hello 단계 필요한 toobuild 및 실행된 hello 샘플.

## <a name="architecture"></a>아키텍처

hello [시뮬레이션 된 장치 클라우드 업로드 샘플] toocreate에서 원격 분석을 전송 하는 게이트웨이 장치 tooan IoT 허브를 시뮬레이션 하는 방법을 보여 줍니다. 장치 수 tooconnect 아닐 tooIoT 허브 직접 때문에 hello 장치:

* IoT Hub가 이해하는 통신 프로토콜을 사용하지 않습니다.
* IoT Hub에서 정도로 스마트 tooremember hello 할당 identity tooit이 않습니다.

IoT 지 게이트웨이 hello 같은 방법으로 다음에서 이러한 문제를 해결할 수 있습니다.

* hello 게이트웨이 hello 장치에서 사용 하는 hello 프로토콜에 대 한 이해, hello 장치에서 장치-클라우드 원격 분석을 수신 및 이러한 메시지 tooIoT hello IoT 허브에서 인식 하는 프로토콜을 사용 하 여 허브를 전달 합니다.

* hello 게이트웨이 IoT Hub identities toodevices 매핑하고 프록시 역할을 하는 장치를 보내면 메시지 tooIoT 허브 합니다.

다음 다이어그램 hello hello hello 샘플의 주 구성 요소, IoT 가장자리 모듈 hello 포함 하 여 보여 줍니다.

![][1]

hello 모듈 메시지를 전달 하지 않는 직접 tooeach 다른 합니다. hello 모듈 hello 메시지 toohello 구독 메커니즘을 사용 하 여 다른 모듈을 제공 하는 메시지 tooan 내부 브로커를 게시 합니다. 자세한 내용은 [Azure IoT Edge 시작][lnk-gw-getstarted]을 참조하세요.

### <a name="protocol-ingestion-module"></a>프로토콜 수집 모듈

이 모듈은 hello hello 게이트웨이 통해 및 hello 클라우드로 장치에서 데이터 받기 위한 기준으로 합니다. Hello 샘플에서는 hello 모듈:

1. 시뮬레이션된 온도 데이터를 만듭니다. 물리적 장치를 사용 하는 경우 hello 모듈 실제 장치에서 데이터를 읽습니다.
1. 메시지를 만듭니다.
1. 시뮬레이션 된 hello 온도 데이터 hello 메시지 내용을 붙여 넣습니다.
1. 가짜 MAC 주소 toohello 메시지를 사용 하 여 속성을 추가합니다.
1. Hello 체인의 다음 모듈로를 사용할 수 있는 toohello hello 메시지를 만듭니다.

호출 하는 hello 모듈 **프로토콜 X 수집** hello 이전 다이어그램 라고 **시뮬레이션 된 장치** hello 소스 코드에서.

### <a name="mac-lt-gt-iot-hub-id-module"></a>MAC &lt;-&gt; IoT Hub ID 모듈

이 모듈은 Mac 주소 속성이 있는 메시지를 검색합니다. Hello 샘플 hello 프로토콜 수집 모듈 hello MAC 주소 속성을 추가합니다. Hello 모듈은 이러한 속성을 찾는 경우 IoT Hub 장치 키 toohello 메시지와 함께 다른 속성을 추가 합니다. hello 모듈 hello 체인의 다음 모듈로 사용할 수 있는 toohello hello 메시지를 사용합니다.

hello 개발자 MAC 주소와 IoT Hub 장치 id 사용 하 여 IoT Hub identities tooassociate hello 시뮬레이션 된 장치 간의 매핑을 설정합니다. hello 개발자 hello 모듈 구성의 일부분으로 hello 매핑을 수동으로 추가합니다.

> [!NOTE]
> 이 샘플은 MAC 주소를 유일한 장치 식별자로 사용하고, 이것을 IoT Hub 장치 ID와 상호 연결시킵니다. 하지만, 다른 고유 식별자를 사용하는 자신만의 모듈을 작성할 수 있습니다. 예를 들어 장치에는 고유한 일련 번호 있을 수 있습니다 또는 hello 원격 분석 데이터는 포함 된 고유한 장치 이름에 포함 될 수 있습니다.

### <a name="iot-hub-communication-module"></a>IoT Hub 통신 모듈

이 모듈에서는 IoT 허브를 사용 하 여 메시지 hello 이전 모듈에 의해 할당 된 장치 키 속성을 사용 합니다. hello 모듈 HTTP 프로토콜 hello 콘텐츠 tooIoT 허브를 사용 하 여 hello 메시지를 보냅니다. HTTP은 IoT Hub에서 hello 이해 하는 세 가지 프로토콜 중 하나입니다.

각 시뮬레이션 된 장치에 대 한 연결을 여는 대신이 모듈 hello 게이트웨이 toohello IoT 허브에서 단일 HTTP 연결을 엽니다. hello 모듈은 다음 해당 연결을 통해 모든 hello 시뮬레이션 된 장치에서의 연결 멀티플렉싱 합니다. 이 방법을 단일 게이트웨이 tooconnect 많은 더 많은 장치를 사용 하면 됩니다.

## <a name="before-you-get-started"></a>시작하기 전에

시작하기 전에 다음을 수행해야 합니다.

* [IoT 허브를 만듭니다.] [ lnk-create-hub] Azure 구독에 필요한 허브 toocomplete의 hello 이름을이 연습 합니다. 계정이 없는 경우 몇 분 내에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.
* 두 장치 tooyour IoT 허브를 추가 하 고 해당 id와 장치 키를 기록 합니다. Hello를 사용할 수 있습니다 [장치 탐색기] [ lnk-device-explorer] 또는 [iothub 탐색기] [ lnk-iothub-explorer] tooadd hello에서 만든 장치 toohello IoT 허브 도구 이전 단계 및 해당 키를 검색 합니다.

![][2]

<!-- Images -->
[1]: media/iot-hub-iot-edge-simulated-selector/image1.png
[2]: media/iot-hub-iot-edge-simulated-selector/image2.png

<!-- Links -->
[시뮬레이션 된 장치 클라우드 업로드 샘플]: https://github.com/Azure/iot-edge/blob/master/samples/simulated_device_cloud_upload/README.md
[lnk-sdk]: https://github.com/Azure/iot-edge
[lnk-gw-getstarted]: ../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md
[lnk-create-hub]: ../articles/iot-hub/iot-hub-create-through-portal.md