> [!div class="op_single_selector"]
> * [Node.JS](../articles/iot-hub/iot-hub-node-node-twin-how-to-configure.md)
> * [C#/Node.js](../articles/iot-hub/iot-hub-csharp-node-twin-how-to-configure.md)
> * [C#](../articles/iot-hub/iot-hub-csharp-csharp-twin-how-to-configure.md)
> 
> 

## <a name="introduction"></a>소개

[IoT Hub 장치 트윈스 시작][lnk-twin-tutorial]를 사용 하 여 tooset 장치 메타 데이터에서 다시 솔루션을 종료 하는 방법을 알아보았습니다 *태그*, 장치 앱에서 장치 조건을 보고 사용 하 여 *속성을 보고*, 및 SQL 유사 언어를 사용 하 여이 정보를 쿼리 합니다.

이 자습서에 설명 합니다 방법을 toouse hello hello 장치로 이중의 *원하는 속성을* 와 함께 *속성을 보고*, tooremotely 장치 앱을 구성 합니다. 보다 구체적으로, 장치로 이중 보고 하는 방법을 보여 주는이 자습서 및 원하는 속성 장치 응용 프로그램의 여러 단계 구성을 사용 하도록 설정 하 고 모든 장치에서 hello 가시성 toohello 솔루션의 백 엔드가이 작업의 hello 상태를 제공 합니다. 장치 구성의 hello 역할에 대 한 자세한 정보를 찾을 수 있습니다 [IoT Hub와 장치 관리의 개요][lnk-dm-overview]합니다.

상위 수준 트윈스 장치를 사용 하 여 구성할 수 있도록 hello 솔루션 백 엔드 toospecify hello 원하는 특정 명령을 전송 하는 대신 hello 관리 되는 장치에 대 한 합니다. 이렇게 하면 추가 구성을 설정 하는 가장 좋은 방법은 tooupdate hello 해당 (매우 소중한 자료 특정 장치 조건은 hello 특정 명령을 tooimmediately 전달 하는 기능에 영향을 여기서 IoT 시나리오에서)을 담당 hello 장치 toohello 지속적으로 보고 하는 동안 솔루션 다시 끝 hello 현재 상태와 hello 업데이트 프로세스의 잠재적 오류 상태입니다. 이 패턴은 큰 장치 집합의 계측 toohello 관리 hello 솔루션 백 엔드 toohave 전체의 표시 유형을 hello 상태 hello 구성 프로세스의 모든 장치에서 수 있기 때문입니다.

> [!NOTE]
> 장치가 좀 더 대화형 방식으로 제어되는 시나리오(예: 사용자 제어 앱에서 팬 켜기)에서는 [직접 메서드][lnk-methods] 사용을 고려하는 것이 좋습니다.
> 
> 

이 자습서에서는 hello 솔루션 백 엔드 변경 hello 원격 분석 구성의 대상 장치를 하는 hello 장치 응용 프로그램의 결과로 여러 단계의 프로세스가 tooapply 구성 따릅니다 (예: 소프트웨어 모듈을 다시 시작이 필요한 업데이트 자습서 간단한 지연 시간 시뮬레이션) 합니다.

hello 솔루션 백 엔드 hello 구성 방법은 다음 hello에 hello 장치로 이중의 원하는 속성에 저장 합니다.

        {
            ...
            "properties": {
                ...
                "desired": {
                    "telemetryConfig": {
                        "configId": "{id of hello configuration}",
                        "sendFrequency": "{config}"
                    }
                }
                ...
            }
            ...
        }

> [!NOTE]
> 구성은 복잡 한 일 수 있으므로 일반적으로 배정 된 고유 id (해시 또는 [Guid][lnk-guid]) toosimplify 자신의 비교 합니다.
> 
> 

hello 장치 응용 프로그램의 현재 구성을 보고 필요한 hello 속성 미러링 **telemetryConfig** hello에 속성을 보고 합니다.

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of hello current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Success",
                    }
                }
                ...
            }
        }

Hello 보고 하는 방법을 **telemetryConfig** 에 추가 속성 **상태**, tooreport hello 상태의 hello 구성 업데이트 프로세스를 사용 합니다.

원하는 새 구성 수신 되 면 hello 장치 앱 hello 정보를 변경 하 여 보류 중인 구성을 보고 합니다.

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of hello current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Pending",
                        "pendingConfig": {
                            "changeId": "{id of hello pending configuration}",
                            "sendFrequency": "{pending configuration}"
                        }
                    }
                }
                ...
            }
        }

그런 다음 일정 시간 후에 hello 장치 앱 됩니다 hello 성공 또는 실패 보고이 작업의 속성 위에 hello를 업데이트 하 여 합니다.
언제 든 지 모든 hello 장치에서 hello 구성 프로세스의 tooquery hello 상태 hello 솔루션 백 엔드가 수, 어떻게 note 합니다.

이 자습서에서는 다음을 수행하는 방법에 대해 설명합니다.

* Hello 솔루션 백 엔드에서 구성 업데이트를 받아으로 여러 업데이트를 보고 하는 시뮬레이션 된 장치 앱 만들기 *속성을 보고* hello 구성 프로세스를 업데이트 합니다.
* 백 엔드 응용 프로그램 업데이트 hello 원하는 장치를 구성 하 고 다음 쿼리 hello 구성 업데이트 프로세스를 만듭니다.

<!-- links -->

[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: ../articles/iot-hub/iot-hub-device-management-overview.md
[lnk-twin-tutorial]: ../articles/iot-hub/iot-hub-node-node-twin-getstarted.md
[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier
