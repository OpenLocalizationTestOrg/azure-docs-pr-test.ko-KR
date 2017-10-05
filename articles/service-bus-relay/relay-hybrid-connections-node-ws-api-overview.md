---
title: "Azure Relay 노드 API 개요 | Microsoft Docs"
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
ms.openlocfilehash: 28526c05c7f364f0fcaaa362fc97857f850040ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="relay-hybrid-connections-node-api-overview"></a><span data-ttu-id="32947-103">Relay 하이브리드 연결 노드 API 개요</span><span class="sxs-lookup"><span data-stu-id="32947-103">Relay Hybrid Connections Node API overview</span></span>

## <a name="overview"></a><span data-ttu-id="32947-104">개요</span><span class="sxs-lookup"><span data-stu-id="32947-104">Overview</span></span>

<span data-ttu-id="32947-105">Azure Relay 하이브리드 연결에 대한 [`hyco-ws`](https://www.npmjs.com/package/hyco-ws) 노드 패키지는 ['ws'](https://www.npmjs.com/package/ws) NPM 패키지를 기반으로 하며 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="32947-105">The [`hyco-ws`](https://www.npmjs.com/package/hyco-ws) Node package for Azure Relay Hybrid Connections is built on and extends the ['ws'](https://www.npmjs.com/package/ws) NPM package.</span></span> <span data-ttu-id="32947-106">이 패키지는 해당 기본 패키지의 모든 내보내기를 다시 내보내며 Azure Relay 서비스 하이브리드 연결 기능과 통합할 수 있는 새로운 내보내기를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="32947-106">This package re-exports all exports of that base package and adds new exports that enable integration with the Azure Relay service Hybrid Connections feature.</span></span> 

<span data-ttu-id="32947-107">`require('ws')`이 `require('hyco-ws')` 대신 이 패키지를 사용할 수 있는 기존 응용 프로그램을 사용하면 응용 프로그램이 WebSocket 연결을 "방화벽 내부"에서 로컬로 및 하이브리드 연결을 통해 동시에 수신 대기할 수 있는 하이브리드 시나리오를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32947-107">Existing applications that `require('ws')` can use this package with `require('hyco-ws')` instead, which also enables hybrid scenarios in which an application can listen for WebSocket connections locally from "inside the firewall" and via Hybrid Connections, all at the same time.</span></span>
  
## <a name="documentation"></a><span data-ttu-id="32947-108">설명서</span><span class="sxs-lookup"><span data-stu-id="32947-108">Documentation</span></span>

<span data-ttu-id="32947-109">API는 [주 'ws' 패키지에 문서화되어](https://github.com/websockets/ws/blob/master/doc/ws.md) 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32947-109">The APIs are [documented in the main 'ws' package](https://github.com/websockets/ws/blob/master/doc/ws.md).</span></span> <span data-ttu-id="32947-110">이 문서에서는 이 패키지가 해당 기준과 어떻게 다른지를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="32947-110">This article describes how this package differs from that baseline.</span></span> 

<span data-ttu-id="32947-111">기본 패키지와 이 'hyco-ws' 간의 주요 차이점은 `require('hyco-ws').RelayedServer`를 통해 내보낸 새 서버 클래스와 몇 가지 도우미 메서드를 추가한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="32947-111">The key differences between the base package and this 'hyco-ws' is that it adds a new server class, exported via `require('hyco-ws').RelayedServer`, and a few helper methods.</span></span>

### <a name="package-helper-methods"></a><span data-ttu-id="32947-112">패키지 도우미 메서드</span><span class="sxs-lookup"><span data-stu-id="32947-112">Package helper methods</span></span>

<span data-ttu-id="32947-113">다음과 같이 사용자가 참조할 수 있는 패키지 내보내기에서 사용 가능한 몇 가지 유틸리티 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32947-113">There are several utility methods available on the package export that you can reference as follows:</span></span>

```JavaScript
const WebSocket = require('hyco-ws');

var listenUri = WebSocket.createRelayListenUri('namespace.servicebus.windows.net', 'path');
listenUri = WebSocket.appendRelayToken(listenUri, 'ruleName', '...key...')
...

```

<span data-ttu-id="32947-114">도우미 메서드는 이 패키지와 함께 사용하기 위한 것이지만 웹 또는 장치 클라이언트에서 수신기 또는 보낸 사람을 만들 수 있도록 노드 서버에서 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32947-114">The helper methods are for use with this package, but can also be used by a Node server for enabling web or device clients to create listeners or senders.</span></span> <span data-ttu-id="32947-115">서버는 수명이 짧은 토큰을 포함하는 URI를 전달하여 이러한 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="32947-115">The server uses these methods by passing them URIs that embed short-lived tokens.</span></span> <span data-ttu-id="32947-116">또한 이러한 URI는 WebSocket 핸드셰이크에 대한 HTTP 헤더 설정을 지원하지 않는 일반적인 WebSocket 스택을 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32947-116">These URIs can also be used with common WebSocket stacks that do not support setting HTTP headers for the WebSocket handshake.</span></span> <span data-ttu-id="32947-117">URI에 권한 부여 토큰을 포함하는 것은 그러한 라이브러리 외부 사용 시나리오에 주로 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="32947-117">Embedding authorization tokens into the URI is supported primarily for those library-external usage scenarios.</span></span> 

#### <a name="createrelaylistenuri"></a><span data-ttu-id="32947-118">createRelayListenUri</span><span class="sxs-lookup"><span data-stu-id="32947-118">createRelayListenUri</span></span>

```JavaScript
var uri = createRelayListenUri([namespaceName], [path], [[token]], [[id]])
```

<span data-ttu-id="32947-119">지정된 네임스페이스 및 경로에 대한 유효한 Azure Relay 하이브리드 연결 수신기 URI를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="32947-119">Creates a valid Azure Relay Hybrid Connection listener URI for the given namespace and path.</span></span> <span data-ttu-id="32947-120">이 URI는 WebSocketServer 클래스의 릴레이 버전으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32947-120">This URI can then be used with the relay version of the WebSocketServer class.</span></span>

- <span data-ttu-id="32947-121">`namespaceName`(필수) - 사용할 Azure Relay 네임스페이스의 정규화된 도메인 이름</span><span class="sxs-lookup"><span data-stu-id="32947-121">`namespaceName` (required) - the domain-qualified name of the Azure Relay namespace to use.</span></span>
- <span data-ttu-id="32947-122">`path`(필수) - 해당 네임스페이스에서 기존 Azure Relay 하이브리드 연결의 이름</span><span class="sxs-lookup"><span data-stu-id="32947-122">`path` (required) - the name of an existing Azure Relay Hybrid Connection in that namespace.</span></span>
- <span data-ttu-id="32947-123">`token`(선택 사항) - 수신기 URI에 포함되어 있는 이전에 발급된 Relay 액세스 토큰(다음 예제 참조)</span><span class="sxs-lookup"><span data-stu-id="32947-123">`token` (optional) - a previously issued Relay access token that is embedded in the listener URI (see the following example).</span></span>
- <span data-ttu-id="32947-124">`id`(선택 사항) - 요청의 종단 간 진단 추적을 활성화하는 추적 식별자</span><span class="sxs-lookup"><span data-stu-id="32947-124">`id` (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests.</span></span>

<span data-ttu-id="32947-125">`token` 값은 선택 사항이며 W3C WebSocket 스택을 사용하는 경우와 마찬가지로 WebSocket 핸드셰이크와 함께 HTTP 헤더를 보낼 수 없는 경우에만 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32947-125">The `token` value is optional and should only be used when it is not possible to send HTTP headers along with the WebSocket handshake, as is the case with the W3C WebSocket stack.</span></span>                  


#### <a name="createrelaysenduri"></a><span data-ttu-id="32947-126">createRelaySendUri</span><span class="sxs-lookup"><span data-stu-id="32947-126">createRelaySendUri</span></span>
 
```JavaScript
var uri = createRelaySendUri([namespaceName], [path], [[token]], [[id]])
```

<span data-ttu-id="32947-127">지정된 네임스페이스 및 경로에 대해 유효한 Azure Relay 하이브리드 연결 송신 URI를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="32947-127">Creates a valid Azure Relay Hybrid Connection send URI for the given namespace and path.</span></span> <span data-ttu-id="32947-128">이 URI는 WebSocket 클라이언트와 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32947-128">This URI can be used with any WebSocket client.</span></span>

- <span data-ttu-id="32947-129">`namespaceName`(필수) - 사용할 Azure Relay 네임스페이스의 정규화된 도메인 이름</span><span class="sxs-lookup"><span data-stu-id="32947-129">`namespaceName` (required) - the domain-qualified name of the Azure Relay namespace to use.</span></span>
- <span data-ttu-id="32947-130">`path`(필수) - 해당 네임스페이스에서 기존 Azure Relay 하이브리드 연결의 이름</span><span class="sxs-lookup"><span data-stu-id="32947-130">`path` (required) - the name of an existing Azure Relay Hybrid Connection in that namespace.</span></span>
- <span data-ttu-id="32947-131">`token`(선택 사항) - 송신 URI에 포함되어 있는 이전에 발급된 Relay 액세스 토큰(다음 예제 참조)</span><span class="sxs-lookup"><span data-stu-id="32947-131">`token` (optional) - a previously issued Relay access token that is embedded in the send URI (see the following example).</span></span>
- <span data-ttu-id="32947-132">`id`(선택 사항) - 요청의 종단 간 진단 추적을 활성화하는 추적 식별자</span><span class="sxs-lookup"><span data-stu-id="32947-132">`id` (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests.</span></span>

<span data-ttu-id="32947-133">`token` 값은 선택 사항이며 W3C WebSocket 스택을 사용하는 경우와 마찬가지로 WebSocket 핸드셰이크와 함께 HTTP 헤더를 보낼 수 없는 경우에만 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32947-133">The `token` value is optional and should only be used when it is not possible to send HTTP headers along with the WebSocket handshake, as is the case with the W3C WebSocket stack.</span></span>                   


#### <a name="createrelaytoken"></a><span data-ttu-id="32947-134">createRelayToken</span><span class="sxs-lookup"><span data-stu-id="32947-134">createRelayToken</span></span> 

```JavaScript
var token = createRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

<span data-ttu-id="32947-135">만료 인수가 생략된 경우 현재 인스턴스에서 지정된 시간(초) 또는 한 시간 동안 유효한 지정된 대상 URI, SAS 규칙 및 SAS 규칙 키에 대한 Azure Relay SAS(공유 액세스 서명) 토큰을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="32947-135">Creates an Azure Relay Shared Access Signature (SAS) token for the given target URI, SAS rule, and SAS rule key that is valid for the given number of seconds or for an hour from the current instant if the expiry argument is omitted.</span></span>

- <span data-ttu-id="32947-136">`uri`(필수) - 토큰이 발급되는 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="32947-136">`uri` (required) - the URI for which the token is to be issued.</span></span> <span data-ttu-id="32947-137">URI는 HTTP 체계를 사용하도록 표준화되고 쿼리 문자열 정보가 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="32947-137">The URI is normalized to use the HTTP scheme, and query string information is stripped.</span></span>
- <span data-ttu-id="32947-138">`ruleName`(필수) - 지정된 URI에 표시된 엔터티 또는 URI 호스트 부분에 표시된 네임스페이스 중 하나에 대한 SAS 규칙 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="32947-138">`ruleName` (required) - SAS rule name for either the entity represented by the given URI, or for the namespace represented by the URI host portion.</span></span>
- <span data-ttu-id="32947-139">`key`(필수) - SAS 규칙에 유효한 키입니다.</span><span class="sxs-lookup"><span data-stu-id="32947-139">`key` (required) - valid key for the SAS rule.</span></span> 
- <span data-ttu-id="32947-140">`expirationSeconds`(선택 사항) - 생성된 토큰이 만료될 때까지의 시간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="32947-140">`expirationSeconds` (optional) - the number of seconds until the generated token should expire.</span></span> <span data-ttu-id="32947-141">지정하지 않은 경우 기본값은 1시간(3600)입니다.</span><span class="sxs-lookup"><span data-stu-id="32947-141">If not specified, the default is 1 hour (3600).</span></span>

<span data-ttu-id="32947-142">발급된 토큰은 지정된 기간 동안 특정 SAS 규칙과 관련된 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="32947-142">The issued token confers the rights associated with the specified SAS rule for the given duration.</span></span>

#### <a name="appendrelaytoken"></a><span data-ttu-id="32947-143">appendRelayToken</span><span class="sxs-lookup"><span data-stu-id="32947-143">appendRelayToken</span></span>

```JavaScript
var uri = appendRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

<span data-ttu-id="32947-144">이 메서드는 이전에 문서화된 `createRelayToken` 메서드와 기능적으로 동일하나, 입력 URI에 추가된 토큰을 올바르게 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="32947-144">This method is functionally equivalent to the `createRelayToken` method documented previously, but returns the token correctly appended to the input URI.</span></span>

### <a name="class-wsrelayedserver"></a><span data-ttu-id="32947-145">클래스 ws.RelayedServer</span><span class="sxs-lookup"><span data-stu-id="32947-145">Class ws.RelayedServer</span></span>

<span data-ttu-id="32947-146">`hycows.RelayedServer` 클래스는 로컬 네트워크에서 수신 대기하지 않는 `ws.Server` 클래스에 대한 대안이지만 Azure Relay 서비스에 대한 수신 대기를 위임합니다.</span><span class="sxs-lookup"><span data-stu-id="32947-146">The `hycows.RelayedServer` class is an alternative to the `ws.Server` class that does not listen on the local network, but delegates listening to the Azure Relay service.</span></span>

<span data-ttu-id="32947-147">두 클래스는 대체로 계약과 호환되므로, `ws.Server` 클래스를 사용하는 기존 응용 프로그램이 릴레이된 버전을 사용하도록 쉽게 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32947-147">The two classes are mostly contract compatible, meaning that an existing application using the `ws.Server` class can easily be changed to use the relayed version.</span></span> <span data-ttu-id="32947-148">주요 차이점은 생성자와 사용 가능한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="32947-148">The main differences are in the constructor and in the available options.</span></span>

#### <a name="constructor"></a><span data-ttu-id="32947-149">생성자</span><span class="sxs-lookup"><span data-stu-id="32947-149">Constructor</span></span>  

```JavaScript 
var ws = require('hyco-ws');
var server = ws.RelayedServer;

var wss = new server(
    {
        server: ws.createRelayListenUri(ns, path),
        token: function() { return ws.createRelayToken('http://' + ns, keyrule, key); }
    });
```

<span data-ttu-id="32947-150">`RelayedServer` 생성자는 독립 실행형 수신기이거나 기존 HTTP 수신기 프레임워크에 포함할 수 있기 때문에 `Server`와는 다른 인수 집합을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="32947-150">The `RelayedServer` constructor supports a different set of arguments than the `Server`, because it is not a standalone listener, or able to be embedded into an existing HTTP listener framework.</span></span> <span data-ttu-id="32947-151">WebSocket 관리는 주로 Relay 서비스에 위임되었기 때문에 사용할 수 있는 옵션은 적습니다.</span><span class="sxs-lookup"><span data-stu-id="32947-151">There are also fewer options available since the WebSocket management is largely delegated to the Relay service.</span></span>

<span data-ttu-id="32947-152">생성자 인수:</span><span class="sxs-lookup"><span data-stu-id="32947-152">Constructor arguments:</span></span>

- <span data-ttu-id="32947-153">`server`(필수) - 수신하는 하이브리드 연결 이름에 대한 정규화된 URI로, 일반적으로 WebSocket.createRelayListenUri() 도우미 메서드로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="32947-153">`server` (required) - the fully qualified URI for a Hybrid Connection name on which to listen, usually constructed with the WebSocket.createRelayListenUri() helper method.</span></span>
- <span data-ttu-id="32947-154">`token`(필수) - 이 인수는 이전에 발급된 토큰 문자열 또는 그러한 토큰 문자열을 가져오도록 호출할 수 있는 콜백 함수를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="32947-154">`token` (required) - this argument holds either a previously issued token string or a callback function that can be called to obtain such a token string.</span></span> <span data-ttu-id="32947-155">콜백 옵션은 토큰 갱신을 활성화하기 때문에 기본으로 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32947-155">The callback option is preferred, as it enables token renewal.</span></span>

#### <a name="events"></a><span data-ttu-id="32947-156">이벤트</span><span class="sxs-lookup"><span data-stu-id="32947-156">Events</span></span>

<span data-ttu-id="32947-157">`RelayedServer` 인스턴스는 들어오는 요청을 처리하고, 연결을 설정하며, 오류 상태를 검색할 수 있도록 하는 세 가지 이벤트를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="32947-157">`RelayedServer` instances emit three events that enable you to handle incoming requests, establish connections, and detect error conditions.</span></span> <span data-ttu-id="32947-158">메시지를 처리하는 `connect` 이벤트를 구독해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32947-158">You must subscribe to the `connect` event to handle messages.</span></span> 

##### <a name="headers"></a><span data-ttu-id="32947-159">headers</span><span class="sxs-lookup"><span data-stu-id="32947-159">headers</span></span>

```JavaScript 
function(headers)
```

<span data-ttu-id="32947-160">들어오는 연결이 수락되기 바로 전에 `headers` 이벤트가 발생하여 클라이언트에 전송할 헤더를 수정할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="32947-160">The `headers` event is raised just before an incoming connection is accepted, enabling modification of the headers to send to the client.</span></span> 

##### <a name="connection"></a><span data-ttu-id="32947-161">connection</span><span class="sxs-lookup"><span data-stu-id="32947-161">connection</span></span>

```JavaScript
function(socket)
```

<span data-ttu-id="32947-162">새로운 WebSocket 연결이 수락되면 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="32947-162">Emitted when a new WebSocket connection is accepted.</span></span> <span data-ttu-id="32947-163">개체는 기본 패키지와 동일한 형식 `ws.WebSocket`입니다.</span><span class="sxs-lookup"><span data-stu-id="32947-163">The object is of type `ws.WebSocket`, same as with the base package.</span></span>


##### <a name="error"></a><span data-ttu-id="32947-164">error</span><span class="sxs-lookup"><span data-stu-id="32947-164">error</span></span>

```JavaScript
function(error)
```

<span data-ttu-id="32947-165">내부 서버에서 오류를 보내면 여기서 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="32947-165">If the underlying server emits an error, it is forwarded here.</span></span>  

#### <a name="helpers"></a><span data-ttu-id="32947-166">도우미</span><span class="sxs-lookup"><span data-stu-id="32947-166">Helpers</span></span>

<span data-ttu-id="32947-167">릴레이된 서버를 시작하고 들어오는 연결에 즉시 가입하는 작업을 간소화하기 위해 패키지는 간단한 도우미 함수를 제공하며, 다음과 같이 예제에서도 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="32947-167">To simplify starting a relayed server and immediately subscribing to incoming connections, the package exposes a simple helper function, which is also used in the examples, as follows:</span></span>

##### <a name="createrelayedlistener"></a><span data-ttu-id="32947-168">createRelayedListener</span><span class="sxs-lookup"><span data-stu-id="32947-168">createRelayedListener</span></span>

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

##### <a name="createrelayedserver"></a><span data-ttu-id="32947-169">createRelayedServer</span><span class="sxs-lookup"><span data-stu-id="32947-169">createRelayedServer</span></span>

```javascript
var server = createRelayedServer([options], [connectCallback] )
```

<span data-ttu-id="32947-170">이 메서드는 생성자를 호출하여 RelayedServer의 새 인스턴스를 만든 다음, 공급된 콜백을 '연결' 이벤트로 구독합니다.</span><span class="sxs-lookup"><span data-stu-id="32947-170">This method calls the constructor to create a new instance of the RelayedServer and then subscribes the provided callback to the 'connection' event.</span></span>
 
##### <a name="relayedconnect"></a><span data-ttu-id="32947-171">relayedConnect</span><span class="sxs-lookup"><span data-stu-id="32947-171">relayedConnect</span></span>

<span data-ttu-id="32947-172">`relayedConnect`는 함수에서 `createRelayedServer` 도우미를 간단히 미러링하면서 클라이언트 연결을 만들고 결과 소켓에 '열기' 이벤트를 구독합니다.</span><span class="sxs-lookup"><span data-stu-id="32947-172">Simply mirroring the `createRelayedServer` helper in function, `relayedConnect` creates a client connection and subscribes to the 'open' event on the resulting socket.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="32947-173">다음 단계</span><span class="sxs-lookup"><span data-stu-id="32947-173">Next steps</span></span>
<span data-ttu-id="32947-174">Azure Relay에 대한 자세한 내용은 다음 링크를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="32947-174">To learn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="32947-175">Azure 릴레이란?</span><span class="sxs-lookup"><span data-stu-id="32947-175">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="32947-176">사용 가능한 Relay API</span><span class="sxs-lookup"><span data-stu-id="32947-176">Available Relay APIs</span></span>](relay-api-overview.md)
