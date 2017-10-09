> [!div class="op_single_selector"]
> * [장치: Node.js 서비스: Node.js](../articles/iot-hub/iot-hub-node-node-device-management-get-started.md)
> * [장치: Node.js 서비스: C#](../articles/iot-hub/iot-hub-csharp-node-device-management-get-started.md)
> * [장치: Java 서비스: Java](../articles/iot-hub/iot-hub-java-java-device-management-getstarted.md)

백 엔드 앱 צ ְ ײ Azure IoT Hub 기본 형식과 같은 [장치로 이중] [ lnk-devtwin] 및 [메서드를 직접][lnk-c2dmethod], tooremotely 시작 하 고 모니터링 장치에서 장치 관리 작업을 선택 합니다. 이 자습서에서는 어떻게 백 엔드 앱 및 장치 앱 tooinitiate 함께 작동 하 고 모니터링할 수 IoT 허브를 사용 하는 원격 장치를 다시 부팅 합니다.

Hello 클라우드에서 백 엔드 응용 프로그램에서 (예: 다시 부팅, 공장 기본 설정 및 펌웨어 업데이트) 직접적인 방법 tooinitiate 장치 관리 작업을 사용 합니다. hello 장치에 대 한 책임이 있습니다.

* IoT 허브에서 보낸 hello 메서드 요청을 처리 합니다.
* Hello hello 장치에서 해당 장치 관련 작업을 시작합니다.
* 상태 업데이트를 통해 제공 *속성을 보고* tooIoT 허브입니다.

Hello 클라우드 toorun 장치로 이중 쿼리 tooreport 장치 관리 작업의 진행률 hello에에서 백 엔드 응용 프로그램을 사용할 수 있습니다.

[lnk-devtwin]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
