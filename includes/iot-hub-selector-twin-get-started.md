> [!div class="op_single_selector"]
> * [Node.JS](../articles/iot-hub/iot-hub-node-node-twin-getstarted.md)
> * [C#/Node.js](../articles/iot-hub/iot-hub-csharp-node-twin-getstarted.md)
> * [C#](../articles/iot-hub/iot-hub-csharp-csharp-twin-getstarted.md)
> * [Java](../articles/iot-hub/iot-hub-java-java-twin-getstarted.md)

장치 쌍은 장치의 상태 정보(메타데이터, 상태 및 조건)를 저장하는 JSON 문서입니다. IoT Hub tooit 연결 하는 각 장치에 대 한 장치로 이중을 유지 합니다.

장치 쌍의 용도:

* 솔루션 백 엔드의 장치 메타데이터를 저장합니다.
* 장치 앱에서 사용할 수 있는 기능 및 조건 (예를 들어 hello 연결 방법 사용)와 같은 현재 상태 정보를 보고 합니다.
* 장치 앱과 백 엔드 응용 프로그램 간에 장기 실행 워크플로 (예: 펌웨어 및 구성 업데이트)의 hello 상태를 동기화 합니다.
* 장치 메타데이터, 구성 또는 상태를 쿼리합니다.

> [!NOTE]
> 장치 쌍은 장치 구성 및 상태를 동기화하고 쿼리하기 위해 설계되었습니다. Toouse 장치 트윈스에서 확인할 수 있습니다 시기에 대 한 자세한 내용은 [장치 트윈스 이해][lnk-twins]합니다.

장치 쌍은 IoT hub에 저장되고 다음을 포함합니다.

* *태그*, hello 솔루션 백 엔드;만 액세스할 수 있게 장치 메타 데이터
* *원하는 속성을*, hello 솔루션에서 수정할 수 있는 JSON 개체 hello 장치 응용 프로그램에서 종료 되 고 관찰 가능 개체를 다시 및
* *속성을 보고*, hello 장치 응용 프로그램에서 수정할 수 있는 인수와 hello 솔루션 백 엔드에서 읽을 수 있는 JSON 개체입니다. 태그 및 속성은 배열을 포함할 수 없지만, 개체는 중첩될 수 있습니다.

![][img-twin]

또한 hello 솔루션 백 엔드 데이터 위에 모든 hello에 따라 장치 트윈스 쿼리할 수 있습니다.
너무 참조[장치 트윈스 이해] [ lnk-twins] 장치 트윈스 및 toohello에 대 한 자세한 내용은 [IoT Hub 쿼리 언어] [ lnk-query] 참조 쿼리 합니다.

> [!NOTE]
> 이때 장치 트윈스는 tooIoT 허브를 연결 하는 장치 에서만에서 액세스할 수 hello MQTT 프로토콜을 사용 합니다. Toohello를 참조 하십시오 [MQTT 지원] [ lnk-devguide-mqtt] 방법에 대 한 문서 tooconvert 기존 장치 앱 toouse MQTT 합니다.

이 자습서에서는 다음을 수행하는 방법에 대해 설명합니다.

* 추가 하는 백 엔드 앱 만들기 *태그* tooa 장치로 이중 및 연결을 보고 하는 시뮬레이션 된 장치 응용 프로그램으로 채널을 *속성을 보고* hello 장치로 이중에 합니다.
* Hello 태그 및 이전에 만든 속성에 필터를 사용 하 여 백 엔드 앱에서 장치를 쿼리 합니다.

<!-- images -->
[img-twin]: media/iot-hub-selector-twin-get-started/twin.png

<!-- links -->
[lnk-query]: ../articles/iot-hub/iot-hub-devguide-query-language.md
[lnk-twins]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-d2c]: ../articles/iot-hub/iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md