---
title: "hello Azure 릴레이 노드 Api의 aaaOverview | Microsoft Docs"
description: "Relay 노드 API 개요"
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b7d6e822-7c32-4cb5-a4b8-df7d009bdc85
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: sethm
ms.openlocfilehash: d231acc854be0eaa965dec0229cf63b08ff27067
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="relay-hybrid-connections-node-api-overview"></a>Relay 하이브리드 연결 노드 API 개요

## <a name="overview"></a>개요

hello [ `hyco-ws` ](https://www.npmjs.com/package/hyco-ws) Azure 릴레이 하이브리드 연결에 대 한 노드 패키지는에서 구축 되며 hello 확장 ['ws'](https://www.npmjs.com/package/ws) NPM 패키지 합니다. 이 패키지는 해당 기본 패키지의 모든 내보내기를 다시 내보냅니다 하 고 hello Azure 릴레이 서비스 하이브리드 연결 기능과 통합을 사용 하는 새 내보내기를 추가 합니다. 

기존 응용 프로그램 하 `require('ws')` 사용 하 여이 패키지를 사용할 수 `require('hyco-ws')` 대신도 그러면 하이브리드 시나리오에서 모두 응용 프로그램에서 로컬로 "내부"hello 방화벽 및 하이브리드 연결을 통해 WebSocket 연결을 수신 수 동일한 hello 시간입니다.
  
## <a name="documentation"></a>설명서

hello Api는 [hello 주 'w s' 패키지에 문서화 되어](https://github.com/websockets/ws/blob/master/doc/ws.md)합니다. 이 문서에서는 이 패키지가 해당 기준과 어떻게 다른지를 설명합니다. 

hello hello 기본 패키지 및이 ' hyco w '의 주요 차이점은 내보낸를 통해 새 서버 클래스를 추가 함을 `require('hyco-ws').RelayedServer`, 및 몇 가지 도우미 메서드.

### <a name="package-helper-methods"></a>패키지 도우미 메서드

다음과 같이 참조할 수 있는 hello 패키지 내보내기에 사용 가능한 여러 가지 유틸리티 메서드 있는지:

```JavaScript
const WebSocket = require('hyco-ws');

var listenUri = WebSocket.createRelayListenUri('namespace.servicebus.windows.net', 'path');
listenUri = WebSocket.appendRelayToken(listenUri, 'ruleName', '...key...')
...

```

hello 도우미 메서드는이 패키지와 함께 사용할 수 이지만 웹 또는 장치 클라이언트 toocreate 수신기 또는 보낸 사람을 설정할 수에 대 한 노드 서버에서 사용할 수도 있습니다. hello 서버 수명이 짧은 토큰을 포함 하는 Uri를 전달 하 여 이러한 메서드를 사용 합니다. 이러한 Uri는 WebSocket 핸드셰이크 hello에 대 한 HTTP 헤더 설정을 지원 하지 않는 일반적인 WebSocket 스택을 사용 하 여 사용할 수도 있습니다. URI는 이러한 외부 라이브러리 사용 시나리오에 주로 지원 hello에 권한 부여 토큰을 포함 합니다. 

#### <a name="createrelaylistenuri"></a>createRelayListenUri

```JavaScript
var uri = createRelayListenUri([namespaceName], [path], [[token]], [[id]])
```

네임 스페이스 경로 매개 변수로 받아 hello에 대 한 올바른 Azure 릴레이 하이브리드 연결 수신기 URI를 만듭니다. 이 URI hello WebSocketServer 클래스의 hello 릴레이 버전으로 사용할 수 있습니다.

- `namespaceName`(필수)-hello hello Azure 릴레이 네임 스페이스 toouse의 정규화 된 도메인 이름입니다.
- `path`(필수)-hello 해당 네임 스페이스에서 기존 Azure 릴레이 하이브리드 연결의 이름입니다.
- `token`(선택 사항)-이전에 발급 된 릴레이 액세스 토큰에 hello 수신기 URI에에서 포함 됩니다 (다음 예제는 hello 참조).
- `id`(선택 사항) - 요청의 종단 간 진단 추적을 활성화하는 추적 식별자

hello `token` 값은 선택 사항이 며만 사용 해야 hello WebSocket 핸드셰이크 함께 가능한 toosend HTTP 헤더가 없으면으로 hello hello W3C WebSocket 스택 사용 됩니다.                  


#### <a name="createrelaysenduri"></a>createRelaySendUri
 
```JavaScript
var uri = createRelaySendUri([namespaceName], [path], [[token]], [[id]])
```

네임 스페이스 경로 매개 변수로 받아 hello에 대 한 올바른 Azure 릴레이 하이브리드 연결 전송 URI를 만듭니다. 이 URI는 WebSocket 클라이언트와 함께 사용할 수 있습니다.

- `namespaceName`(필수)-hello hello Azure 릴레이 네임 스페이스 toouse의 정규화 된 도메인 이름입니다.
- `path`(필수)-hello 해당 네임 스페이스에서 기존 Azure 릴레이 하이브리드 연결의 이름입니다.
- `token`(선택 사항)-hello에 포함 된 이전에 발급 된 릴레이 액세스 토큰을 보낼 URI (다음 예제는 hello 참조).
- `id`(선택 사항) - 요청의 종단 간 진단 추적을 활성화하는 추적 식별자

hello `token` 값은 선택 사항이 며만 사용 해야 hello WebSocket 핸드셰이크 함께 가능한 toosend HTTP 헤더가 없으면으로 hello hello W3C WebSocket 스택 사용 됩니다.                   


#### <a name="createrelaytoken"></a>createRelayToken 

```JavaScript
var token = createRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

Hello 지정 된 대상 URI, SAS 규칙 및에서 제공 된 시간 (초) 또는 1 시간 동안 현재 hello 인스턴트 hello 만료 인수를 생략 하면 hello에 대 한 유효한 SAS 규칙 키에 대 한 Azure 릴레이 공유 액세스 서명 (SAS) 토큰을 만듭니다.

- `uri`URI는 hello에 대 한 토큰 발급 toobe hello (필수)-합니다. hello URI는 정규화 된 toouse hello HTTP 체계 및 쿼리 문자열 정보 제거 됩니다.
- `ruleName`SAS 규칙 (필수)-URI를 지정 하는 hello 나타내는 hello 엔터티 중 하나에 대 한 이름 또는 hello에 대 한 네임 스페이스 나타내는 hello URI 호스트 부분입니다.
- `key`(필수)-hello SAS 규칙에 대 한 올바른 키입니다. 
- `expirationSeconds`(선택 사항)-hello 시간 (초) hello 토큰 생성 될 때까지 만료 되어야 합니다. 지정 하지 않으면 hello 기본값은 1 시간 (3600)입니다.

hello 발급 토큰 지정 하는 hello와 관련 된 hello 권한을 제공 기간을 지정 하는 hello에 대 한 SAS 규칙입니다.

#### <a name="appendrelaytoken"></a>appendRelayToken

```JavaScript
var uri = appendRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

이 메서드는 기능적으로 동일한 toohello `createRelayToken` 메서드 이전에 문서화 되어 있지만 반환 hello 올바르게 추가 된 toohello 입력 URI가 토큰입니다.

### <a name="class-wsrelayedserver"></a>클래스 ws.RelayedServer

hello `hycows.RelayedServer` 클래스는 대체 toohello `ws.Server` hello 로컬 네트워크에서 수신 대기 하지 않는 하지만 수신 toohello Azure 릴레이 서비스에 위임 클래스를 합니다.

hello 두 클래스는 계약 호환 hello를 사용 하 여 기존 응용 프로그램을 의미 하는 대부분 `ws.Server` 클래스는 변경 된 toouse 헤더 블록이 릴레이 hello 버전 가능성이 높습니다. hello 주요 차이점은 되며 hello 생성자 hello 사용할 수 있는 옵션에 없습니다.

#### <a name="constructor"></a>생성자  

```JavaScript 
var ws = require('hyco-ws');
var server = ws.RelayedServer;

var wss = new server(
    {
        server: ws.createRelayListenUri(ns, path),
        token: function() { return ws.createRelayToken('http://' + ns, keyrule, key); }
    });
```

hello `RelayedServer` 생성자는 다른 집합이 hello 보다 인수를 지원 `Server`(가) 독립 실행형 수신기 또는 수 toobe HTTP 수신기 프레임 워크에 포함 되지 않습니다. 더 적은 옵션도 있습니다 사용할 수 있는 hello WebSocket 관리는 주로 위임된 toohello 릴레이 서비스입니다.

생성자 인수:

- `server`(필수)-hello 정규화 된 URI에 일반적으로 hello WebSocket.createRelayListenUri() 도우미 메서드를 사용 하 여 생성 하는 toolisten 하이브리드 연결 이름에 대 한 합니다.
- `token`(필수)-이 인수는 이전에 발급 된 토큰 문자열 또는 tooobtain 토큰 문자열 호출할 수 있는 콜백 함수를 보유 합니다. hello 콜백 옵션은 토큰 갱신 수 있기 때문에 기본 방법입니다.

#### <a name="events"></a>이벤트

`RelayedServer`인스턴스 연결을 설정 및 오류 조건을 검색 하면 toohandle 들어오는 요청을 수 있는 3 개의 이벤트를 내보냅니다. Toohello 가입 해야 `connect` 이벤트 toohandle 메시지입니다. 

##### <a name="headers"></a>headers

```JavaScript 
function(headers)
```

hello `headers` 들어오는 연결이 수락 되 면 hello 헤더 toosend toohello 클라이언트의 수정을 사용 하도록 설정 하기 바로 전에 이벤트가 발생 합니다. 

##### <a name="connection"></a>connection

```JavaScript
function(socket)
```

새로운 WebSocket 연결이 수락되면 보내집니다. 형식의 개체가 다음 hello `ws.WebSocket`hello 기본 패키지와 동일 합니다.


##### <a name="error"></a>error

```JavaScript
function(error)
```

Hello 내부 서버 오류를 내보냅니다 여기 전달 됩니다.  

#### <a name="helpers"></a>도우미

릴레이 된 서버와 즉시 가입 tooincoming 연결 hello 패키지 toosimplify 시작도 사용 되는 hello 예제에 다음과 같이 간단한 도우미 함수를 노출 합니다.

##### <a name="createrelayedlistener"></a>createRelayedListener

```JavaScript
var WebSocket = require('hyco-ws');

var wss = WebSocket.createRelayedServer(
    {
        server: WebSocket.createRelayListenUri(ns, path),
        token: function() { return WebSocket.createRelayToken('http://' + ns, keyrule, key); }
    }, 
    function (ws) {
        console.log('connection accepted');
        ws.onmessage = function (event) {
            console.log(JSON.parse(event.data));
        };
        ws.on('close', function () {
            console.log('connection closed');
        });       
});
``` 

##### <a name="createrelayedserver"></a>createRelayedServer

```javascript
var server = createRelayedServer([options], [connectCallback] )
```

이 메서드는 hello 생성자 toocreate hello RelayedServer의 새 인스턴스를 호출 하 고 한 다음 제공 된 hello 콜백 toohello 'connection' 이벤트를 구독.
 
##### <a name="relayedconnect"></a>relayedConnect

단순히 hello 미러링 `createRelayedServer` 도우미 함수에서 `relayedConnect` hello 결과 소켓에서 toohello '열기' 이벤트를 구독 하 고 클라이언트 연결을 만듭니다.

```JavaScript
var uri = WebSocket.createRelaySendUri(ns, path);
WebSocket.relayedConnect(
    uri,
    WebSocket.createRelayToken(uri, keyrule, key),
    function (socket) {
        ...
    }
);
```

## <a name="next-steps"></a>다음 단계
다음이 링크를 방문 하는 Azure 릴레이 대 한 자세한 toolearn:
* [Azure 릴레이란?](relay-what-is-it.md)
* [사용 가능한 Relay API](relay-api-overview.md)
