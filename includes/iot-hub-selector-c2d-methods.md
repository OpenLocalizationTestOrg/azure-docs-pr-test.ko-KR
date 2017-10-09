> [!div class="op_single_selector"]
> * [Node.JS](../articles/iot-hub/iot-hub-node-node-direct-methods.md)
> * [C#/Node.js](../articles/iot-hub/iot-hub-csharp-node-direct-methods.md)
> * [C#](../articles/iot-hub/iot-hub-csharp-csharp-direct-methods.md)
> * [Java](../articles/iot-hub/iot-hub-java-java-direct-methods.md)

Azure IoT Hub는 수백만의 장치와 솔루션 백 엔드 간에서 안정적이고 안전한 양방향 통신이 가능하도록 완전히 관리되는 서비스입니다. 이전 자습서 ([IoT 허브 시작] 및 [IoT Hub와 클라우드-장치 메시지를 보낼]) hello 장치-클라우드 및 클라우드-장치 메시징의 기본 기능 IoT Hub를 보여 줍니다. 또한 제공 IoT Hub hello hello 클라우드에서 장치에 대 한 기능 tooinvoke 비영구 메서드. 메서드는 요청-회신 상호 작용을 나타냅니다 직접 HTTP 호출 한다는 점에서 성공 하거나 실패 (직후 사용자가 지정한 시간 제한)은 장치 비슷한 tooan toolet hello 사용자 알 hello 호출의 hello 상태. [장치에서 직접 메서드를 호출] [ lnk-devguide-methods] 자세히 직접 메서드를 설명 하 고 toouse 원하는 속성이 나 클라우드-장치 메시지를 사용 하는 대신 메서드를 직접 하는 경우에 대 한 지침을 제공 합니다.

이 자습서에서는 다음을 수행하는 방법에 대해 설명합니다.

* Azure 포털 toocreate IoT hub hello를 사용 하 및 IoT 허브에서 장치 id를 만드는 키를 누릅니다.
* Hello 클라우드에서 호출 될 수 있는 직접 메서드가 있는 시뮬레이트된 장치 앱을 만듭니다.
* IoT 허브를 통해 hello 시뮬레이션 된 장치 응용 프로그램에서 직접 메서드를 호출 하 여 콘솔 응용 프로그램을 만듭니다.

> [!NOTE]
> 이때 직접 메서드 tooIoT 허브를 사용 하 여 연결 하는 장치에서 지원된만 hello MQTT 프로토콜은입니다. Toohello를 참조 하십시오 [MQTT 지원] [ lnk-devguide-mqtt] 방법에 대 한 문서 tooconvert 기존 장치 앱 toouse MQTT 합니다.


[lnk-devguide-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md

[IoT Hub와 클라우드-장치 메시지를 보낼]: ../articles/iot-hub/iot-hub-csharp-csharp-c2d.md
[IoT 허브 시작]: ../articles/iot-hub/iot-hub-node-node-getstarted.md