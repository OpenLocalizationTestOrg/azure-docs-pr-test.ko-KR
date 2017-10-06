---
title: "서비스 패브릭 aaaAzure 역방향 프록시 진단 | Microsoft Docs"
description: "자세한 방법을 toomonitor hello 역방향 프록시에 대 한 요청 처리를 진단 하 고 있습니다."
services: service-fabric
documentationcenter: .net
author: kavyako
manager: vipulm
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/08/2017
ms.author: kavyako
ms.openlocfilehash: 9687b9688dc26ba619cbdfab1b1f49a3035345c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-diagnose-request-processing-at-hello-reverse-proxy"></a>모니터링 및 진단 hello 역방향 프록시에 대 한 요청 처리

서비스 패브릭의 hello 5.7 버전부터 역방향 프록시 이벤트는 컬렉션에 사용할 수 있습니다. 두 개의 채널에서 사용할 수 있는 hello 이벤트 hello 역방향 프록시 및 항목이 성공 및 실패 한 요청에 대 한 자세한 정보 표시 이벤트를 포함 하는 두 번째 채널에서 toorequest 처리 작업이 실패와 관련 된만 오류 이벤트를 사용 합니다.

너무 참조[역방향 프록시 이벤트 수집](service-fabric-diagnostics-event-aggregation-wad.md#collect-reverse-proxy-events) tooenable 로컬 및 Azure 서비스 패브릭 클러스터의 이러한 채널에서 이벤트를 수집 합니다.

## <a name="troubleshoot-using-diagnostics-logs"></a>진단 로그를 사용한 문제 해결 
다음은에 어떻게 toointerpret hello 일반적인 오류 로그는 하나 일어날 수 있는 몇 가지 예입니다.

1. 역방향 프록시에서 응답 상태 코드 504(시간 제한) 반환

    한 가지 이유는 hello 요청 제한 시간 내 toohello 서비스 실패 tooreply 원인일 수 있습니다.
아래의 첫 번째 이벤트 hello hello 역방향 프록시에서 수신 하는 hello 요청의 hello 세부 정보를 기록 합니다. hello 두 번째 이벤트 나타냅니다 해당 hello 요청이 실패 하는 동안 전달 tooservice 인해 너무 "내부 오류 ERROR_WINHTTP_TIMEOUT =" 

    hello 페이로드 포함 되어 있습니다.

    *  **traceId**:이 GUID 수 toocorrelate tooa 단일 요청에 해당 하는 모든 hello 이벤트를 사용 합니다. 두 개의 이벤트 아래 hello에서 traceId hello = **2f87b722-e254-4ac2-a802-fd315c1a0271**, toohello 속해 암시 같은 요청 합니다.
    *  **requestUrl**: hello URL (역방향 프록시 URL) toowhich hello 요청을 보냈습니다.
    *  **verb**: HTTP 동사입니다.
    *  **remoteAddress**: hello 요청을 보내는 클라이언트의 주소입니다.
    *  **resolvedServiceUrl**: 해결 된 서비스 끝점 URL toowhich hello 들어오는 요청입니다. 
    *  **errorDetails**: hello 실패에 대 한 추가 정보입니다.

    ```
    {
      "Timestamp": "2017-07-20T15:57:59.9871163-07:00",
      "ProviderName": "Microsoft-ServiceFabric",
      "Id": 51477,
      "Message": "2f87b722-e254-4ac2-a802-fd315c1a0271 Request url = https://localhost:19081/LocationApp/LocationFEService?zipcode=98052, verb = GET, remote (client) address = ::1, resolved service url = Https://localhost:8491/LocationApp/?zipcode=98052, request processing start time =     15:58:00.074114 (745,608.196 MSec) ",
      "ProcessId": 57696,
      "Level": "Informational",
      "Keywords": "0x1000000000000021",
      "EventName": "ReverseProxy",
      "ActivityID": null,
      "RelatedActivityID": null,
      "Payload": {
        "traceId": "2f87b722-e254-4ac2-a802-fd315c1a0271",
        "requestUrl": "https://localhost:19081/LocationApp/LocationFEService?zipcode=98052",
        "verb": "GET",
        "remoteAddress": "::1",
        "resolvedServiceUrl": "Https://localhost:8491/LocationApp/?zipcode=98052",
        "requestStartTime": "2017-07-20T15:58:00.0741142-07:00"
      }
    }

    {
      "Timestamp": "2017-07-20T16:00:01.3173605-07:00",
      ...
      "Message": "2f87b722-e254-4ac2-a802-fd315c1a0271 Error while forwarding request tooservice: response status code = 504, description = Reverse proxy Timeout, phase = FinishSendRequest, internal error = ERROR_WINHTTP_TIMEOUT ",
      ...
      "Payload": {
        "traceId": "2f87b722-e254-4ac2-a802-fd315c1a0271",
        "statusCode": 504,
        "description": "Reverse Proxy Timeout",
        "sendRequestPhase": "FinishSendRequest",
        "errorDetails": "internal error = ERROR_WINHTTP_TIMEOUT"
      }
    }
    ```

2. 역방향 프록시가 응답 상태 코드 404(없음)를 반환합니다. 
    
    다음은 서비스 끝점 일치 toofind hello 못했으므로 역방향 프록시 404를 반환 하는 위치는 예에서는 이벤트입니다.
    몇 가지 흥미로운 hello 페이로드 항목은:
    *  **processRequestPhase**: hello 오류가 발생 했을 때 요청을 처리 하는 동안 hello 단계를 나타냅니다 ***TryGetEndpoint*** 즉, 동안 동안 toofetch hello 서비스 끝점 tooforward 하 합니다. 
    *  **errorDetails**: hello 끝점 검색 조건을 나열 합니다. 여기서 지정 하는 hello listenerName를 확인할 수 있습니다 = **FrontEndListener** hello 이름의 수신기 hello 복제본 끝점 목록에 포함 하는 반면 **OldListener**합니다.
    
    ```
    {
      ...
      "Message": "c1cca3b7-f85d-4fef-a162-88af23604343 Error while processing request, cannot forward tooservice: request url = https://localhost:19081/LocationApp/LocationFEService?ListenerName=FrontEndListener&zipcode=98052, verb = GET, remote (client) address = ::1, request processing start time = 16:43:02.686271 (3,448,220.353 MSec), error = FABRIC_E_ENDPOINT_NOT_FOUND, message = , phase = TryGetEndoint, SecureOnlyMode = false, gateway protocol = https, listenerName = FrontEndListener, replica endpoint = {\"Endpoints\":{\"\":\"Https:\/\/localhost:8491\/LocationApp\/\"}} ",
      "ProcessId": 57696,
      "Level": "Warning",
      "EventName": "ReverseProxy",
      "Payload": {
        "traceId": "c1cca3b7-f85d-4fef-a162-88af23604343",
        "requestUrl": "https://localhost:19081/LocationApp/LocationFEService?ListenerName=NewListener&zipcode=98052",
        ...
        "processRequestPhase": "TryGetEndoint",
        "errorDetails": "SecureOnlyMode = false, gateway protocol = https, listenerName = FrontEndListener, replica endpoint = {\"Endpoints\":{\"OldListener\":\"Https:\/\/localhost:8491\/LocationApp\/\"}}"
      }
    }
    ```
    역방향 프록시 404를 반환할 수 있는 또 다른 예로 찾을 수 없습니다: ApplicationGateway\Http 구성 매개 변수 **SecureOnlyMode** tootrue에서 수신 대기 하는 hello 역방향 프록시를 사용 하 여 설정 **HTTPS**, 그러나 모든 hello 복제본 끝점은 (http 수신) 안전 하지 않습니다.
    HTTPS tooforward hello 요청에서 수신 대기 끝점을 찾을 수 없기 때문에 프록시 반환 404를 반대로 바꿉니다. Hello 이벤트 페이로드의 hello 매개 변수를 분석 toonarrow hello 문제를 확인할 수 있습니다.
    
    ```
        "errorDetails": "SecureOnlyMode = true, gateway protocol = https, listenerName = NewListener, replica endpoint = {\"Endpoints\":{\"OldListener\":\"Http:\/\/localhost:8491\/LocationApp\/\", \"NewListener\":\"Http:\/\/localhost:8492\/LocationApp\/\"}}"
    ```

3. 요청 toohello 역방향 프록시 제한 시간 오류로 실패합니다. 
    hello 이벤트 로그 hello 받은 요청 세부 정보 (여기 표시 되지 않음)로 이벤트를 포함 합니다.
    hello 다음 이벤트는 hello 서비스 404 상태 코드로 응답 했 고 역방향 프록시를 다시 확인할 시작을 표시 합니다. 

    ```
    {
      ...
      "Message": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e Request tooservice returned: status code = 404, status description = , Reresolving ",
      "Payload": {
        "traceId": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e",
        "statusCode": 404,
        "statusDescription": ""
      }
    }
    {
      ...
      "Message": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e Re-resolved service url = Https://localhost:8491/LocationApp/?zipcode=98052 ",
      "Payload": {
        "traceId": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e",
        "requestUrl": "Https://localhost:8491/LocationApp/?zipcode=98052"
      }
    }
    ```
    모든 hello 이벤트를 수집 하려는 모든를 해결 하 고 앞으로 시도 표시 하는 이벤트의 기차를 표시 됩니다.
    hello 계열의 마지막 이벤트 hello hello 성공적으로 해결 시도 횟수와 함께 시간 초과로 hello 요청을 처리 하지 못한 보여 줍니다.
    
    > [!NOTE]
    > 기본적으로 사용 하지 않도록 설정 하는 tookeep hello verbose 채널 이벤트 컬렉션 것이 좋습니다 하 고 필요 무휴로 문제 해결을 위해 사용 하도록 설정 합니다.

    ```
    {
      ...
      "Message": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e Error while processing request: number of successful resolve attempts = 12, error = FABRIC_E_TIMEOUT, message = , phase = ResolveServicePartition,  ",
      "EventName": "ReverseProxy",
      ...
      "Payload": {
        "traceId": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e",
        "resolveCount": 12,
        "errorval": -2147017729,
        "errorMessage": "",
        "processRequestPhase": "ResolveServicePartition",
        "errorDetails": ""
      }
    }
    ```
    
    위험/오류 이벤트에만 수집을 활성화 하는 hello 제한 시간 및 해결 시도의 횟수 hello에 대 한 세부 정보를 사용 하 여 하나의 이벤트를 표시 됩니다. 
    
    Hello 서비스 toosend 404 상태 코드 백 toohello 사용자가을 "X ServiceFabric" 헤더에 의해 함께 해야 합니다. 이 해결 한 후 해당 역방향 프록시 전달 hello 상태 코드 백 toohello 클라이언트를 표시 됩니다.  

4. Hello 클라이언트의 연결이 끊어진 경우 hello 요청 합니다.

    hello 이벤트 아래에 역방향 프록시 hello 응답 tooclient 전달 하지만 hello 클라이언트가 연결을 끊을 때 기록 됩니다.

    ```
    {
      ...
      "Message": "6e2571a3-14a8-4fc7-93bb-c202c23b50b8 Unable toosend response tooclient: phase = SendResponseHeaders, error = -805306367, internal error = ERROR_SUCCESS ",
      "ProcessId": 57696,
      "Level": "Warning",
      ...
      "EventName": "ReverseProxy",
      "Payload": {
        "traceId": "6e2571a3-14a8-4fc7-93bb-c202c23b50b8",
        "sendResponsePhase": "SendResponseHeaders",
        "errorval": -805306367,
        "winHttpError": "ERROR_SUCCESS"
      }
    }
    ```

> [!NOTE]
> 현재 이벤트 관련된 toowebsocket 요청 처리 기록 되지 않습니다. Hello 다음 릴리스에서 추가 됩니다.

## <a name="next-steps"></a>다음 단계
* Azure 클러스터에서의 로그 수집을 활성화하기 위해 [Windows Azure 진단을 사용한 이벤트 집계 및 수집](service-fabric-diagnostics-event-aggregation-wad.md) 
* Visual Studio에서 서비스 패브릭 이벤트 tooview 참조 [모니터 하 고 로컬로 진단](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)합니다.
* 너무 참조[역방향 프록시 tooconnect toosecure 서비스 구성](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) Azure 리소스 관리자에 대 한 서식 파일을 tooconfigure 보안 역방향 프록시 hello 다양 한 서비스 인증서 유효성 검사 옵션으로 샘플링 합니다.
* 읽기 [서비스 패브릭 역방향 프록시](service-fabric-reverseproxy.md) toolearn 더 합니다.
