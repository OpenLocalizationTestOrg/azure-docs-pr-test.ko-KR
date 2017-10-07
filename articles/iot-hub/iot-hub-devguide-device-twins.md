---
title: "aaaUnderstand Azure IoT Hub 장치 트윈스 | Microsoft Docs"
description: "개발자 가이드-장치 사용 트윈스 IoT Hub와 장치 간에 toosynchronize 상태 및 구성 데이터"
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 8a3da072-a5bf-46e5-8de4-24cdbb2a03fa
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7dade18665108ed352ff3d18e864dc34f451bbf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-use-device-twins-in-iot-hub"></a>IoT Hub의 장치 쌍 이해 및 사용
## <a name="overview"></a>개요
*장치 쌍*은 장치 상태 정보(메타데이터, 구성 및 조건)를 저장하는 JSON 문서입니다. IoT Hub tooIoT 허브에 연결 해야 하는 각 장치에 대 한 장치로 이중을 유지 합니다. 이 문서에서는 다음을 설명합니다.

* hello 장치로 이중의 구조를 hello: *태그*, *원하는* 및 *속성을 보고*, 및
* 장치 앱과 백 엔드 트윈스 장치에서 수행할 수 있는 hello 작업입니다.

> [!NOTE]
> 현재 장치 트윈스 tooIoT 허브를 연결 하는 장치 에서만에서 액세스할 수는 hello MQTT 프로토콜을 사용 합니다. Toohello 참조 [MQTT 지원] [ lnk-devguide-mqtt] 방법에 대 한 문서 tooconvert 기존 장치 앱 toouse MQTT 합니다.
> 
> 

### <a name="when-toouse"></a>때 toouse
장치 쌍의 용도:

* Hello 클라우드에서 장치 관련 메타 데이터를 저장 합니다. 예를 들어 hello 배포의 위치는 판매기입니다.
* 장치 앱의 사용 가능한 기능 및 상태와 같은 현재 상태 정보를 보고합니다. 예를 들어 장치는 연결 된 tooyour IoT 허브 셀룰러 또는 병렬 WiFi 합니다.
* 장치 앱과 백 엔드 응용 프로그램 간에 장기 실행 워크플로 hello 상태를 동기화 합니다. 예를 들어 hello 솔루션 다시 끝 새 펌웨어 버전 tooinstall hello 및 hello 장치 응용 프로그램 보고서 hello hello 업데이트 프로세스의 다양 한 단계를 지정 합니다.
* 장치 메타데이터, 구성 또는 상태를 쿼리합니다.

너무 참조[장치-클라우드 통신 지침] [ lnk-d2c-guidance] 보고 속성, 장치-클라우드 메시지 또는 파일 업로드를 사용 하 여에 대 한 지침입니다.
너무 참조[클라우드-장치 통신 지침] [ lnk-c2d-guidance] 원하는 속성, 직접 메서드 또는 클라우드-장치 메시지를 사용 하 여에 대 한 지침입니다.

## <a name="device-twins"></a>장치 쌍
장치 쌍이 저장하는 장치 관련 정보는:

* 장치 및 백 엔드 toosynchronize 장치 조건 및 구성에 사용할 수 있습니다.
* hello 솔루션 백 엔드 tooquery를 사용할 수 있으며 대상 장기 실행 작업.

연결 된 장치로 이중의 hello 수명 주기 toohello 해당 [장치 id][lnk-identity]합니다. IoT Hub에서 새 장치 ID를 만들거나 삭제하면 장치 쌍이 암시적으로 만들어지거나 삭제됩니다.

장치 쌍은 JSON 문서이며 다음을 포함합니다.

* **태그**. 솔루션 백 엔드 hello hello JSON 문서의 섹션에서 읽고 쓸 수 있습니다. 태그 표시 toodevice 앱 않습니다.
* **desired 속성**. 보고 속성 toosynchronize 장치 구성 또는 조건을 함께 사용합니다. 원하는 속성에만 설정할 수 hello 솔루션 다시에서 끝 및 hello 장치 응용 프로그램에서 읽을 수 있습니다. 또한 hello 원하는 속성의 변경 내용 중 실시간으로에서 hello 장치 앱을 알릴 수 있습니다.
* **reported 속성**. 원하는 속성 toosynchronize 장치 구성 또는 조건을 함께 사용합니다. 보고 속성 hello 장치 앱만 설정할 수 있습니다 및 읽고 hello 솔루션 백 엔드도 쿼리할 수 수 있습니다.

Hello 장치로 이중 JSON 문서의 hello 루트 hello에 저장 된 hello 해당 장치의 id 로부터 hello 읽기 전용 속성을 포함 하는 또한 [id 레지스트리에][lnk-identity]합니다.

![][img-twin]

다음 예제는 hello 장치로 이중 JSON 문서를 보여 줍니다.

        {
            "deviceId": "devA",
            "generationId": "123",
            "status": "enabled",
            "statusReason": "provisioned",
            "connectionState": "connected",
            "connectionStateUpdatedTime": "2015-02-28T16:24:48.789Z",
            "lastActivityTime": "2015-02-30T16:24:48.789Z",

            "tags": {
                "$etag": "123",
                "deploymentLocation": {
                    "building": "43",
                    "floor": "1"
                }
            },
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata" : {...},
                    "$version": 1
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": 55,
                    "$metadata" : {...},
                    "$version": 4
                }
            }
        }

Hello 루트 개체는 hello 시스템 속성 및 컨테이너에 대 한 개체 `tags` 및 둘 다 `reported` 및 `desired` 속성입니다. hello `properties` 일부 읽기 전용 요소를 포함 하는 컨테이너 (`$metadata`, `$etag`, 및 `$version`) hello에 설명 된 [장치로 이중 메타 데이터] [ lnk-twin-metadata] 및 [ 낙관적 동시성] [ lnk-concurrency] 섹션.

### <a name="reported-property-example"></a>reported 속성 예
Hello 이전 예에서는 hello 장치로 이중 포함 한 `batteryLevel` hello 장치 앱 로부터 보고 되는 속성입니다. 이 속성 가능한 tooquery 있고 hello 마지막 보고 된 배터리 수준에 따라 장치에 작동 합니다. 다른 예로 hello 장치 앱 보고 장치 기능 또는 연결 옵션입니다.

> [!NOTE]
> 보고 속성 hello 솔루션 백 엔드 hello 마지막 속성의 값으로는 관심이 시나리오를 단순화 합니다. 사용 하 여 [장치-클라우드 메시지] [ lnk-d2c] hello 솔루션 백 엔드 경우 시계열 같은 타임 스탬프 이벤트의 시퀀스의 hello 형태로 tooprocess 장치 원격 분석에 필요 합니다.

### <a name="desired-property-example"></a>desired 속성 예제
Hello 이전 예에서 hello `telemetryConfig` 장치로 이중 원하는 및 보고 된 속성은이 장치에 대 한 솔루션의 백 엔드 hello 및 hello 장치 앱 toosynchronize hello 원격 분석 구성에서 사용 됩니다. 예:

1. hello 솔루션 백 엔드 hello 원하는 속성을 원하는 hello 구성 값으로 설정합니다. 다음은 필요한 hello 속성이 설정 된 hello 문서 hello 부분이입니다.
   
        ...
        "desired": {
            "telemetryConfig": {
                "sendFrequency": "5m"
            },
            ...
        },
        ...
2. hello 장치 앱에 연결 하거나 hello에서 먼저 다시 연결 하는 경우에 즉시 hello 변경 알림이 전송 됩니다. hello 장치 응용 프로그램이 다음 보고 업데이트 하는 hello 구성 (또는 hello를 사용 하 여 오류 조건을 `status` 속성). 다음은 hello 부분의 hello 속성을 보고 합니다.
   
        ...
        "reported": {
            "telemetryConfig": {
                "sendFrequency": "5m",
                "status": "success"
            }
            ...
        }
        ...
3. hello 솔루션 백 엔드 여 hello 결과 hello 구성 작업의 여러 장치에서 추적할 수 [쿼리] [ lnk-query] 장치 트윈스 합니다.

> [!NOTE]
> hello 이전 조각은 예제를 보려면 장치 구성 및 서버 인스턴스의 상태는 한 가지 방법은 tooencode의 가독성을 위해 최적화 되어 있습니다. IoT Hub는 hello 장치로 이중 원하는 hello 장치 트윈스에서 속성을 보고에 대 한 특정 스키마를 적용 하지 않습니다.
> 
> 

예: 펌웨어 업데이트 트윈스 toosynchronize 장기 실행 작업을 사용할 수 있습니다. Toouse 속성 toosynchronize 및 장치에서 장기 실행 작업 추적 참조 하는 방법에 대 한 자세한 내용은 [속성 tooconfigure 장치 원하는 사용할][lnk-twin-properties]합니다.

## <a name="back-end-operations"></a>백 엔드 작업
HTTP를 통해 노출 하는 원자성 작업을 수행 하는 hello를 사용 하 여 hello 장치로 이중에서 작동 하는 hello 솔루션 백 엔드:

1. **ID로 장치 쌍 검색** 이 작업은 반환 hello 장치로 이중 문서를 태그를 포함 하 고 원하는 경우 보고 및 시스템 속성입니다.
2. **장치 쌍 부분 업데이트**. 이 작업에는 hello 솔루션 백 엔드 toopartially 업데이트 hello 태그 또는 장치로 이중에서 원하는 속성 수 있습니다. hello 부분 업데이트를 추가 하거나 속성을 업데이트 하는 JSON 문서로 표현 됩니다. 속성이 너무 설정`null` 제거 됩니다. hello 다음 예제에서는 속성을 새로 만들고 원하는 값으로 `{"newProperty": "newValue"}`, hello의 기존 값을 덮어쓰게 `existingProperty` 와 `"otherNewValue"`, 제거 및 `otherOldProperty`합니다. 다른 변경 내용이 없는 원하는 tooexisting 속성 또는 태그:
   
        {
            "properties": {
                "desired": {
                    "newProperty": {
                        "nestedProperty": "newValue"
                    },
                    "existingProperty": "otherNewValue",
                    "otherOldProperty": null
                }
            }
        }
3. **desired 속성 바꾸기**. 이 작업을 사용 하면 hello 솔루션 백 엔드 toocompletely 모든 기존 원하는 속성을 덮어쓸 및 새 JSON 문서에 대 한 대체 `properties/desired`합니다.
4. **태그 바꾸기**. 이 작업을 사용 하면 hello 솔루션 백 엔드 toocompletely 모든 기존 태그를 덮어쓰고 새 JSON 문서에 대 한 대체 `tags`합니다.
5. **쌍 알림을 받습니다**. 이 작업에는 hello 솔루션 백 엔드 toobe를 hello로 이중 수정 될 때 알릴 수 있습니다. toodo, 하면 IoT 솔루션 필요한 등 toocreate 경로 및 tooset hello 데이터 소스 같음 너무*twinChangeEvents*합니다. 기본적으로 쌍 알림이 전송되지 않습니다. 즉, 이러한 경로는 미리 존재하지 않습니다. 변경의 hello 속도가 너무 빨라 또는 내부 오류와 같은 다른 이유로 hello IoT Hub 모든 변경 내용이 포함 된 하나의 알림을 보낼 수 있습니다. 따라서 응용 프로그램에 신뢰할 수 있는 감사 및 모든 중간 상태의 로깅이 필요한 경우 D2C 메시지를 사용하는 것이 여전히 좋습니다. hello로 이중 알림 메시지에 속성 및 본문에 포함 됩니다.

    - properties

    | 이름 | 값 |
    | --- | --- |
    $content-type | application/json |
    $iothub-enqueuedtime |  Hello 알림을 전송 시간 |
    $iothub-message-source | twinChangeEvents |
    $content-encoding | utf-8 |
    deviceId | Hello 장치의 id |
    hubName | IoT Hub의 이름 |
    operationTimestamp | [ISO8601] 작업의 타임스탬프 |
    iothub-message-schema | deviceLifecycleNotification |
    opType | "replaceTwin" 또는 "updateTwin" |

    메시지 시스템 속성은 hello로 접두사가 `'$'` 기호입니다.

    - body
        
    이 섹션에는 JSON 형식의 hello로 이중 변경 내용을 모두 포함 되어 있습니다. 동일한 형식 hello를 사용 하 여 패치로, hello 차이만 한다는 섹션이 포함 되어야 모두로 이중: 태그, properties.reported, properties.desired를 포함 하 고 "$metadata" hello 요소입니다. 예를 들면 다음과 같습니다.
    ```
    {
        "properties": {
            "desired": {
                "$metadata": {
                    "$lastUpdated": "2016-02-30T16:24:48.789Z"
                },
                "$version": 1
            },
            "reported": {
                "$metadata": {
                    "$lastUpdated": "2016-02-30T16:24:48.789Z"
                },
                "$version": 1
            }
        }
    }
    ``` 

이전 작업 지원 hello 모든 [낙관적 동시성] [ lnk-concurrency] hello 필요 **ServiceConnect** hello에 정의 된 사용 권한 [보안 ] [ lnk-security] 문서.

또한 작업 toothese hello 솔루션 다시 끝 수 있습니다.

* Hello 장치 트윈스 hello를 사용 하 여 쿼리 SQL과 비슷한 [IoT Hub 쿼리 언어][lnk-query]합니다.
* [작업][lnk-jobs]을 사용하여 장치 쌍의 큰 집합에서 작업을 수행합니다.

## <a name="device-operations"></a>장치 작업
hello 장치 응용 프로그램에서 원자성 작업을 수행 하는 hello를 사용 하 여 hello 장치로 이중은 작동 합니다.

1. **장치 쌍 검색** 이 작업 hello 장치로 이중 문서를 반환 합니다 (태그를 포함 하 고 원하는, 보고 및 시스템 속성) hello 현재 연결 된 장치에 대 한 합니다.
2. **reported 속성 부분 업데이트**. 이 작업을 사용 하면 hello의 부분 업데이트 hello hello 현재 연결 된 장치의 속성을 보고 합니다. 이 작업을 사용 하 여 hello 동일한 JSON 업데이트에 해당 hello 솔루션 백 엔드 사용 하 여 원하는 속성의 부분 업데이트에 대 한 서식을 지정 합니다.
3. **desired 속성 관찰**. 현재 연결 된 장치 hello toobe 발생할 때 업데이트 toohello 필요한 속성에 대 한 알림을 선택할 수 있습니다. hello 장치 hello 솔루션 백 엔드에 의해 같은 형태의 업데이트 (전체 또는 일부 대체) 실행 하는 hello를 받습니다.

이전 작업이 모두 hello hello 필요 **DeviceConnect** hello에 정의 된 사용 권한 [보안] [ lnk-security] 문서.

hello [Azure IoT 장치 Sdk] [ lnk-sdks] 쉽게 toouse hello 앞에 다양 한 언어 및 플랫폼에서 작업을 확인 합니다. 자세한 내용은 hello 원하는 속성이 동기화에 대 한 IoT Hub 기본 형식에 있습니다 [장치 다시 연결 흐름][lnk-reconnection]합니다.

> [!NOTE]
> 현재 장치 트윈스 tooIoT 허브를 연결 하는 장치 에서만에서 액세스할 수는 hello MQTT 프로토콜을 사용 합니다.
> 
> 

## <a name="reference-topics"></a>참조 항목:
hello 다음 참조 항목 제공 제어 액세스 tooyour IoT 허브에 대 한 자세한 내용은 합니다.

## <a name="tags-and-properties-format"></a>태그 및 속성 형식
태그를 원하는 및 보고 속성 제한 사항에 따라 hello 사용 하 여 JSON 개체는:

* JSON 개체의 모든 키는 대/소문자를 구분하는 64바이트 UTF-8 유니코드 문자열입니다. 허용되는 문자에서 유니코드 제어 문자(세그먼트 C0 및 C1) 및 `'.'`, `' '` 및 `'$'`는 제외됩니다.
* JSON 개체의 모든 값의 JSON 유형만 hello 될 수 있습니다: 부울, 숫자, 문자열, 개체입니다. 배열은 허용되지 않습니다.
* tags, desired 속성 및reported 속성의 모든 JSON 개체는 최대 5의 깊이를 가질 수 있습니다. 예를 들어, 다음 개체는 hello가 올바릅니다.

        {
            ...
            "tags": {
                "one": {
                    "two": {
                        "three": {
                            "four": {
                                "five": {
                                    "property": "value"
                                }
                            }
                        }
                    }
                }
            },
            ...
        }

* 모든 문자열 값의 길이는 최대 512바이트입니다.

## <a name="device-twin-size"></a>장치 쌍 크기
IoT Hub는 8KB 크기 제한의 hello 값에 적용 `tags`, `properties/desired`, 및 `properties/reported`, 읽기 전용 요소 제외 합니다.
hello 크기는 계산를 계산 하 여 모든 문자를 제외한 유니코드 제어 문자 (세그먼트 C0 및 C1) 및 공간 `' '` 는 문자열 상수 외부에서 표시 되 면입니다.
IoT Hub 오류가 발생 하 여 hello 제한 초과 이러한 문서의 hello 크기를 증가 하 게 하는 모든 작업을 거부 합니다.

## <a name="device-twin-metadata"></a>장치 쌍 메타데이터
IoT Hub 원하는 스탬프와 속성을 보고 hello hello로 이중 장치에 있는 각 JSON 개체에 대 한 마지막 업데이트 타임 스탬프를 유지 관리 합니다. hello 타임 스탬프가 UTC에 있으며 hello에 인코딩된 [ISO8601] 형식 `YYYY-MM-DDTHH:MM:SS.mmmZ`합니다.
예:

        {
            ...
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": {
                                "$lastUpdated": "2016-03-30T16:24:48.789Z"
                            },
                            "$lastUpdated": "2016-03-30T16:24:48.789Z"
                        },
                        "$lastUpdated": "2016-03-30T16:24:48.789Z"
                    },
                    "$version": 23
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": "55%",
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": "5m",
                            "status": {
                                "$lastUpdated": "2016-03-31T16:35:48.789Z"
                            },
                            "$lastUpdated": "2016-03-31T16:35:48.789Z"
                        }
                        "batteryLevel": {
                            "$lastUpdated": "2016-04-01T16:35:48.789Z"
                        },
                        "$lastUpdated": "2016-04-01T16:24:48.789Z"
                    },
                    "$version": 123
                }
            }
            ...
        }

이 정보는 키 개체를 제거 하는 모든 수준 (JSON 구조 hello의 뿐 아니라 hello 잎) toopreserve 업데이트에서 유지 됩니다.

## <a name="optimistic-concurrency"></a>낙관적 동시성
태그, desired 및 reported 속성은 모두 낙관적 동시성을 지원합니다.
태그는 ETag를 기준으로 한 [RFC7232], hello 태그의 JSON 표현을 나타내는입니다. Etag는 hello 솔루션 백 엔드 tooensure 일관성에서 조건부 업데이트 작업에 사용할 수 있습니다.

장치로 이중 필요 하 고 속성을 보고 했지만 Etag를 하지 않은 한 `$version` toobe 증분 보장 되는 값입니다. 마찬가지로 tooan ETag, hello 버전 hello 파티 tooenforce 일관성 업데이트를 업데이트 하 여 사용할 수 있습니다. 예를 들어 보고 된 속성이 나 hello 솔루션 백 엔드 원하는 속성에 대 한 장치 앱.

버전 (예: hello 원하는 속성을 관찰 hello 장치 응용 프로그램) 관찰 에이전트 검색 작업의 hello 결과 업데이트 알림을 간의 경합을 조정 해야 하는 경우에 유용 합니다. 섹션 hello [장치 다시 연결 흐름] [ lnk-reconnection] 자세한 정보를 제공 합니다.

## <a name="device-reconnection-flow"></a>장치 다시 연결 흐름
IoT Hub는 연결되지 않은 장치에 대한 desired 속성 업데이트 알림을 유지하지 않습니다. _ 연결 하는 장치에서 업데이트 알림에 대 한 추가 toosubscribing hello 전체 원하는 속성 문서를 검색 해야 합니다. 업데이트 알림 및 전체 검색 사이의 레이스가 hello 가능성이 들어 hello 흐름 확보 되어야 합니다.

1. 장치 앱 tooan IoT 허브를 연결합니다.
2. 장치 앱이 desired 속성 업데이트 알림을 구독합니다.
3. 장치 앱 hello 원하는 속성에 대 한 전체 문서를 검색합니다.

hello 장치 응용 프로그램을 사용 하 여 모든 알림을 무시할 수 `$version` hello 전체 검색 된 문서의 hello 버전 보다 작거나 합니다. 이 방법은 IoT Hub가 버전이 항상 증가한다는 것을 보장하기 때문에 가능합니다.

> [!NOTE]
> 이 논리 hello에서 이미 구현 되어 [Azure IoT 장치 Sdk][lnk-sdks]합니다. 이 설명은 hello 장치 응용 프로그램이 Azure IoT 장치 Sdk 중 하나를 사용할 수 없는 hello MQTT 인터페이스를 직접 프로그래밍 해야 하는 경우에 유용 합니다.
> 
> 

## <a name="additional-reference-material"></a>추가 참조 자료
Hello IoT 허브 개발자 가이드에서에서 다른 참조 항목은 다음과 같습니다.

* hello [IoT Hub 끝점] [ lnk-endpoints] 설명 hello 런타임 및 관리 작업에 대 한 각 IoT 허브를 노출 하는 다양 한 끝점입니다.
* hello [제한 및 할당량] [ lnk-quotas] hello 서비스를 사용 하는 경우 조정 동작 tooexpect hello와 toohello IoT 허브 서비스를 적용 하는 hello 할당량에 설명 합니다.
* hello [Azure IoT 장치 및 서비스 Sdk] [ lnk-sdks] 문서 목록을 hello 다양 한 언어 Sdk IoT Hub와 상호 작용 하는 장치 및 서비스 모두 앱을 개발할 때 사용할 수 있습니다.
* hello [장치 트윈스, 작업 및 메시지 라우팅에 대 한 IoT Hub 쿼리 언어] [ lnk-query] hello 장치 트윈스 및 작업에 대 한 IoT 허브에서 tooretrieve 정보를 사용 하려면 IoT Hub 쿼리 언어에 설명 .
* hello [IoT 허브 MQTT 지원] [ lnk-devguide-mqtt] 문서 hello MQTT 프로토콜에 대 한 IoT Hub 지원에 대 한 자세한 정보를 제공 합니다.

## <a name="next-steps"></a>다음 단계
이제 장치 트윈스 알아보았습니다 hello 다음 IoT 허브 개발자 가이드 항목에에서 관심이 있을 수 있습니다.

* [장치에서 직접 메서드 호출][lnk-methods]
* [여러 장치에서 jobs 예약][lnk-jobs]

이 문서에서 설명 하는 hello 개념 중 일부는 tootry, 원하는 경우 IoT Hub 자습서를 따라 hello에 관심이 있을 수 있습니다.

* [Toouse 장치로 이중 hello 하는 방법][lnk-twin-tutorial]
* [어떻게 toouse 장치로 이중 속성][lnk-twin-properties]

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-identity]: iot-hub-devguide-identity-registry.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-security]: iot-hub-devguide-security.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[ISO8601]: https://en.wikipedia.org/wiki/ISO_8601
[RFC7232]: https://tools.ietf.org/html/rfc7232
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-twin-metadata]: iot-hub-devguide-device-twins.md#device-twin-metadata
[lnk-concurrency]: iot-hub-devguide-device-twins.md#optimistic-concurrency
[lnk-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow

[img-twin]: media/iot-hub-devguide-device-twins/twin.png
