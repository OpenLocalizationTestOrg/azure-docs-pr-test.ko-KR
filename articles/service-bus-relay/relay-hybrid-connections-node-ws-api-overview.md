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
# <a name="relay-hybrid-connections-node-api-overview"></a><span data-ttu-id="6ea4b-103">Relay 하이브리드 연결 노드 API 개요</span><span class="sxs-lookup"><span data-stu-id="6ea4b-103">Relay Hybrid Connections Node API overview</span></span>

## <a name="overview"></a><span data-ttu-id="6ea4b-104">개요</span><span class="sxs-lookup"><span data-stu-id="6ea4b-104">Overview</span></span>

<span data-ttu-id="6ea4b-105">hello [ `hyco-ws` ](https://www.npmjs.com/package/hyco-ws) Azure 릴레이 하이브리드 연결에 대 한 노드 패키지는에서 구축 되며 hello 확장 ['ws'](https://www.npmjs.com/package/ws) NPM 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-105">hello [`hyco-ws`](https://www.npmjs.com/package/hyco-ws) Node package for Azure Relay Hybrid Connections is built on and extends hello ['ws'](https://www.npmjs.com/package/ws) NPM package.</span></span> <span data-ttu-id="6ea4b-106">이 패키지는 해당 기본 패키지의 모든 내보내기를 다시 내보냅니다 하 고 hello Azure 릴레이 서비스 하이브리드 연결 기능과 통합을 사용 하는 새 내보내기를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-106">This package re-exports all exports of that base package and adds new exports that enable integration with hello Azure Relay service Hybrid Connections feature.</span></span> 

<span data-ttu-id="6ea4b-107">기존 응용 프로그램 하 `require('ws')` 사용 하 여이 패키지를 사용할 수 `require('hyco-ws')` 대신도 그러면 하이브리드 시나리오에서 모두 응용 프로그램에서 로컬로 "내부"hello 방화벽 및 하이브리드 연결을 통해 WebSocket 연결을 수신 수 동일한 hello 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-107">Existing applications that `require('ws')` can use this package with `require('hyco-ws')` instead, which also enables hybrid scenarios in which an application can listen for WebSocket connections locally from "inside hello firewall" and via Hybrid Connections, all at hello same time.</span></span>
  
## <a name="documentation"></a><span data-ttu-id="6ea4b-108">설명서</span><span class="sxs-lookup"><span data-stu-id="6ea4b-108">Documentation</span></span>

<span data-ttu-id="6ea4b-109">hello Api는 [hello 주 'w s' 패키지에 문서화 되어](https://github.com/websockets/ws/blob/master/doc/ws.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-109">hello APIs are [documented in hello main 'ws' package](https://github.com/websockets/ws/blob/master/doc/ws.md).</span></span> <span data-ttu-id="6ea4b-110">이 문서에서는 이 패키지가 해당 기준과 어떻게 다른지를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-110">This article describes how this package differs from that baseline.</span></span> 

<span data-ttu-id="6ea4b-111">hello hello 기본 패키지 및이 ' hyco w '의 주요 차이점은 내보낸를 통해 새 서버 클래스를 추가 함을 `require('hyco-ws').RelayedServer`, 및 몇 가지 도우미 메서드.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-111">hello key differences between hello base package and this 'hyco-ws' is that it adds a new server class, exported via `require('hyco-ws').RelayedServer`, and a few helper methods.</span></span>

### <a name="package-helper-methods"></a><span data-ttu-id="6ea4b-112">패키지 도우미 메서드</span><span class="sxs-lookup"><span data-stu-id="6ea4b-112">Package helper methods</span></span>

<span data-ttu-id="6ea4b-113">다음과 같이 참조할 수 있는 hello 패키지 내보내기에 사용 가능한 여러 가지 유틸리티 메서드 있는지:</span><span class="sxs-lookup"><span data-stu-id="6ea4b-113">There are several utility methods available on hello package export that you can reference as follows:</span></span>

```JavaScript
const WebSocket = require('hyco-ws');

var listenUri = WebSocket.createRelayListenUri('namespace.servicebus.windows.net', 'path');
listenUri = WebSocket.appendRelayToken(listenUri, 'ruleName', '...key...')
...

```

<span data-ttu-id="6ea4b-114">hello 도우미 메서드는이 패키지와 함께 사용할 수 이지만 웹 또는 장치 클라이언트 toocreate 수신기 또는 보낸 사람을 설정할 수에 대 한 노드 서버에서 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-114">hello helper methods are for use with this package, but can also be used by a Node server for enabling web or device clients toocreate listeners or senders.</span></span> <span data-ttu-id="6ea4b-115">hello 서버 수명이 짧은 토큰을 포함 하는 Uri를 전달 하 여 이러한 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-115">hello server uses these methods by passing them URIs that embed short-lived tokens.</span></span> <span data-ttu-id="6ea4b-116">이러한 Uri는 WebSocket 핸드셰이크 hello에 대 한 HTTP 헤더 설정을 지원 하지 않는 일반적인 WebSocket 스택을 사용 하 여 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-116">These URIs can also be used with common WebSocket stacks that do not support setting HTTP headers for hello WebSocket handshake.</span></span> <span data-ttu-id="6ea4b-117">URI는 이러한 외부 라이브러리 사용 시나리오에 주로 지원 hello에 권한 부여 토큰을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-117">Embedding authorization tokens into hello URI is supported primarily for those library-external usage scenarios.</span></span> 

#### <a name="createrelaylistenuri"></a><span data-ttu-id="6ea4b-118">createRelayListenUri</span><span class="sxs-lookup"><span data-stu-id="6ea4b-118">createRelayListenUri</span></span>

```JavaScript
var uri = createRelayListenUri([namespaceName], [path], [[token]], [[id]])
```

<span data-ttu-id="6ea4b-119">네임 스페이스 경로 매개 변수로 받아 hello에 대 한 올바른 Azure 릴레이 하이브리드 연결 수신기 URI를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-119">Creates a valid Azure Relay Hybrid Connection listener URI for hello given namespace and path.</span></span> <span data-ttu-id="6ea4b-120">이 URI hello WebSocketServer 클래스의 hello 릴레이 버전으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-120">This URI can then be used with hello relay version of hello WebSocketServer class.</span></span>

- <span data-ttu-id="6ea4b-121">`namespaceName`(필수)-hello hello Azure 릴레이 네임 스페이스 toouse의 정규화 된 도메인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-121">`namespaceName` (required) - hello domain-qualified name of hello Azure Relay namespace toouse.</span></span>
- <span data-ttu-id="6ea4b-122">`path`(필수)-hello 해당 네임 스페이스에서 기존 Azure 릴레이 하이브리드 연결의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-122">`path` (required) - hello name of an existing Azure Relay Hybrid Connection in that namespace.</span></span>
- <span data-ttu-id="6ea4b-123">`token`(선택 사항)-이전에 발급 된 릴레이 액세스 토큰에 hello 수신기 URI에에서 포함 됩니다 (다음 예제는 hello 참조).</span><span class="sxs-lookup"><span data-stu-id="6ea4b-123">`token` (optional) - a previously issued Relay access token that is embedded in hello listener URI (see hello following example).</span></span>
- <span data-ttu-id="6ea4b-124">`id`(선택 사항) - 요청의 종단 간 진단 추적을 활성화하는 추적 식별자</span><span class="sxs-lookup"><span data-stu-id="6ea4b-124">`id` (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests.</span></span>

<span data-ttu-id="6ea4b-125">hello `token` 값은 선택 사항이 며만 사용 해야 hello WebSocket 핸드셰이크 함께 가능한 toosend HTTP 헤더가 없으면으로 hello hello W3C WebSocket 스택 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-125">hello `token` value is optional and should only be used when it is not possible toosend HTTP headers along with hello WebSocket handshake, as is hello case with hello W3C WebSocket stack.</span></span>                  


#### <a name="createrelaysenduri"></a><span data-ttu-id="6ea4b-126">createRelaySendUri</span><span class="sxs-lookup"><span data-stu-id="6ea4b-126">createRelaySendUri</span></span>
 
```JavaScript
var uri = createRelaySendUri([namespaceName], [path], [[token]], [[id]])
```

<span data-ttu-id="6ea4b-127">네임 스페이스 경로 매개 변수로 받아 hello에 대 한 올바른 Azure 릴레이 하이브리드 연결 전송 URI를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-127">Creates a valid Azure Relay Hybrid Connection send URI for hello given namespace and path.</span></span> <span data-ttu-id="6ea4b-128">이 URI는 WebSocket 클라이언트와 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-128">This URI can be used with any WebSocket client.</span></span>

- <span data-ttu-id="6ea4b-129">`namespaceName`(필수)-hello hello Azure 릴레이 네임 스페이스 toouse의 정규화 된 도메인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-129">`namespaceName` (required) - hello domain-qualified name of hello Azure Relay namespace toouse.</span></span>
- <span data-ttu-id="6ea4b-130">`path`(필수)-hello 해당 네임 스페이스에서 기존 Azure 릴레이 하이브리드 연결의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-130">`path` (required) - hello name of an existing Azure Relay Hybrid Connection in that namespace.</span></span>
- <span data-ttu-id="6ea4b-131">`token`(선택 사항)-hello에 포함 된 이전에 발급 된 릴레이 액세스 토큰을 보낼 URI (다음 예제는 hello 참조).</span><span class="sxs-lookup"><span data-stu-id="6ea4b-131">`token` (optional) - a previously issued Relay access token that is embedded in hello send URI (see hello following example).</span></span>
- <span data-ttu-id="6ea4b-132">`id`(선택 사항) - 요청의 종단 간 진단 추적을 활성화하는 추적 식별자</span><span class="sxs-lookup"><span data-stu-id="6ea4b-132">`id` (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests.</span></span>

<span data-ttu-id="6ea4b-133">hello `token` 값은 선택 사항이 며만 사용 해야 hello WebSocket 핸드셰이크 함께 가능한 toosend HTTP 헤더가 없으면으로 hello hello W3C WebSocket 스택 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-133">hello `token` value is optional and should only be used when it is not possible toosend HTTP headers along with hello WebSocket handshake, as is hello case with hello W3C WebSocket stack.</span></span>                   


#### <a name="createrelaytoken"></a><span data-ttu-id="6ea4b-134">createRelayToken</span><span class="sxs-lookup"><span data-stu-id="6ea4b-134">createRelayToken</span></span> 

```JavaScript
var token = createRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

<span data-ttu-id="6ea4b-135">Hello 지정 된 대상 URI, SAS 규칙 및에서 제공 된 시간 (초) 또는 1 시간 동안 현재 hello 인스턴트 hello 만료 인수를 생략 하면 hello에 대 한 유효한 SAS 규칙 키에 대 한 Azure 릴레이 공유 액세스 서명 (SAS) 토큰을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-135">Creates an Azure Relay Shared Access Signature (SAS) token for hello given target URI, SAS rule, and SAS rule key that is valid for hello given number of seconds or for an hour from hello current instant if hello expiry argument is omitted.</span></span>

- <span data-ttu-id="6ea4b-136">`uri`URI는 hello에 대 한 토큰 발급 toobe hello (필수)-합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-136">`uri` (required) - hello URI for which hello token is toobe issued.</span></span> <span data-ttu-id="6ea4b-137">hello URI는 정규화 된 toouse hello HTTP 체계 및 쿼리 문자열 정보 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-137">hello URI is normalized toouse hello HTTP scheme, and query string information is stripped.</span></span>
- <span data-ttu-id="6ea4b-138">`ruleName`SAS 규칙 (필수)-URI를 지정 하는 hello 나타내는 hello 엔터티 중 하나에 대 한 이름 또는 hello에 대 한 네임 스페이스 나타내는 hello URI 호스트 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-138">`ruleName` (required) - SAS rule name for either hello entity represented by hello given URI, or for hello namespace represented by hello URI host portion.</span></span>
- <span data-ttu-id="6ea4b-139">`key`(필수)-hello SAS 규칙에 대 한 올바른 키입니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-139">`key` (required) - valid key for hello SAS rule.</span></span> 
- <span data-ttu-id="6ea4b-140">`expirationSeconds`(선택 사항)-hello 시간 (초) hello 토큰 생성 될 때까지 만료 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-140">`expirationSeconds` (optional) - hello number of seconds until hello generated token should expire.</span></span> <span data-ttu-id="6ea4b-141">지정 하지 않으면 hello 기본값은 1 시간 (3600)입니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-141">If not specified, hello default is 1 hour (3600).</span></span>

<span data-ttu-id="6ea4b-142">hello 발급 토큰 지정 하는 hello와 관련 된 hello 권한을 제공 기간을 지정 하는 hello에 대 한 SAS 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-142">hello issued token confers hello rights associated with hello specified SAS rule for hello given duration.</span></span>

#### <a name="appendrelaytoken"></a><span data-ttu-id="6ea4b-143">appendRelayToken</span><span class="sxs-lookup"><span data-stu-id="6ea4b-143">appendRelayToken</span></span>

```JavaScript
var uri = appendRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

<span data-ttu-id="6ea4b-144">이 메서드는 기능적으로 동일한 toohello `createRelayToken` 메서드 이전에 문서화 되어 있지만 반환 hello 올바르게 추가 된 toohello 입력 URI가 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-144">This method is functionally equivalent toohello `createRelayToken` method documented previously, but returns hello token correctly appended toohello input URI.</span></span>

### <a name="class-wsrelayedserver"></a><span data-ttu-id="6ea4b-145">클래스 ws.RelayedServer</span><span class="sxs-lookup"><span data-stu-id="6ea4b-145">Class ws.RelayedServer</span></span>

<span data-ttu-id="6ea4b-146">hello `hycows.RelayedServer` 클래스는 대체 toohello `ws.Server` hello 로컬 네트워크에서 수신 대기 하지 않는 하지만 수신 toohello Azure 릴레이 서비스에 위임 클래스를 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-146">hello `hycows.RelayedServer` class is an alternative toohello `ws.Server` class that does not listen on hello local network, but delegates listening toohello Azure Relay service.</span></span>

<span data-ttu-id="6ea4b-147">hello 두 클래스는 계약 호환 hello를 사용 하 여 기존 응용 프로그램을 의미 하는 대부분 `ws.Server` 클래스는 변경 된 toouse 헤더 블록이 릴레이 hello 버전 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-147">hello two classes are mostly contract compatible, meaning that an existing application using hello `ws.Server` class can easily be changed toouse hello relayed version.</span></span> <span data-ttu-id="6ea4b-148">hello 주요 차이점은 되며 hello 생성자 hello 사용할 수 있는 옵션에 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-148">hello main differences are in hello constructor and in hello available options.</span></span>

#### <a name="constructor"></a><span data-ttu-id="6ea4b-149">생성자</span><span class="sxs-lookup"><span data-stu-id="6ea4b-149">Constructor</span></span>  

```JavaScript 
var ws = require('hyco-ws');
var server = ws.RelayedServer;

var wss = new server(
    {
        server: ws.createRelayListenUri(ns, path),
        token: function() { return ws.createRelayToken('http://' + ns, keyrule, key); }
    });
```

<span data-ttu-id="6ea4b-150">hello `RelayedServer` 생성자는 다른 집합이 hello 보다 인수를 지원 `Server`(가) 독립 실행형 수신기 또는 수 toobe HTTP 수신기 프레임 워크에 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-150">hello `RelayedServer` constructor supports a different set of arguments than hello `Server`, because it is not a standalone listener, or able toobe embedded into an existing HTTP listener framework.</span></span> <span data-ttu-id="6ea4b-151">더 적은 옵션도 있습니다 사용할 수 있는 hello WebSocket 관리는 주로 위임된 toohello 릴레이 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-151">There are also fewer options available since hello WebSocket management is largely delegated toohello Relay service.</span></span>

<span data-ttu-id="6ea4b-152">생성자 인수:</span><span class="sxs-lookup"><span data-stu-id="6ea4b-152">Constructor arguments:</span></span>

- <span data-ttu-id="6ea4b-153">`server`(필수)-hello 정규화 된 URI에 일반적으로 hello WebSocket.createRelayListenUri() 도우미 메서드를 사용 하 여 생성 하는 toolisten 하이브리드 연결 이름에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-153">`server` (required) - hello fully qualified URI for a Hybrid Connection name on which toolisten, usually constructed with hello WebSocket.createRelayListenUri() helper method.</span></span>
- <span data-ttu-id="6ea4b-154">`token`(필수)-이 인수는 이전에 발급 된 토큰 문자열 또는 tooobtain 토큰 문자열 호출할 수 있는 콜백 함수를 보유 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-154">`token` (required) - this argument holds either a previously issued token string or a callback function that can be called tooobtain such a token string.</span></span> <span data-ttu-id="6ea4b-155">hello 콜백 옵션은 토큰 갱신 수 있기 때문에 기본 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-155">hello callback option is preferred, as it enables token renewal.</span></span>

#### <a name="events"></a><span data-ttu-id="6ea4b-156">이벤트</span><span class="sxs-lookup"><span data-stu-id="6ea4b-156">Events</span></span>

<span data-ttu-id="6ea4b-157">`RelayedServer`인스턴스 연결을 설정 및 오류 조건을 검색 하면 toohandle 들어오는 요청을 수 있는 3 개의 이벤트를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-157">`RelayedServer` instances emit three events that enable you toohandle incoming requests, establish connections, and detect error conditions.</span></span> <span data-ttu-id="6ea4b-158">Toohello 가입 해야 `connect` 이벤트 toohandle 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-158">You must subscribe toohello `connect` event toohandle messages.</span></span> 

##### <a name="headers"></a><span data-ttu-id="6ea4b-159">headers</span><span class="sxs-lookup"><span data-stu-id="6ea4b-159">headers</span></span>

```JavaScript 
function(headers)
```

<span data-ttu-id="6ea4b-160">hello `headers` 들어오는 연결이 수락 되 면 hello 헤더 toosend toohello 클라이언트의 수정을 사용 하도록 설정 하기 바로 전에 이벤트가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-160">hello `headers` event is raised just before an incoming connection is accepted, enabling modification of hello headers toosend toohello client.</span></span> 

##### <a name="connection"></a><span data-ttu-id="6ea4b-161">connection</span><span class="sxs-lookup"><span data-stu-id="6ea4b-161">connection</span></span>

```JavaScript
function(socket)
```

<span data-ttu-id="6ea4b-162">새로운 WebSocket 연결이 수락되면 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-162">Emitted when a new WebSocket connection is accepted.</span></span> <span data-ttu-id="6ea4b-163">형식의 개체가 다음 hello `ws.WebSocket`hello 기본 패키지와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-163">hello object is of type `ws.WebSocket`, same as with hello base package.</span></span>


##### <a name="error"></a><span data-ttu-id="6ea4b-164">error</span><span class="sxs-lookup"><span data-stu-id="6ea4b-164">error</span></span>

```JavaScript
function(error)
```

<span data-ttu-id="6ea4b-165">Hello 내부 서버 오류를 내보냅니다 여기 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-165">If hello underlying server emits an error, it is forwarded here.</span></span>  

#### <a name="helpers"></a><span data-ttu-id="6ea4b-166">도우미</span><span class="sxs-lookup"><span data-stu-id="6ea4b-166">Helpers</span></span>

<span data-ttu-id="6ea4b-167">릴레이 된 서버와 즉시 가입 tooincoming 연결 hello 패키지 toosimplify 시작도 사용 되는 hello 예제에 다음과 같이 간단한 도우미 함수를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-167">toosimplify starting a relayed server and immediately subscribing tooincoming connections, hello package exposes a simple helper function, which is also used in hello examples, as follows:</span></span>

##### <a name="createrelayedlistener"></a><span data-ttu-id="6ea4b-168">createRelayedListener</span><span class="sxs-lookup"><span data-stu-id="6ea4b-168">createRelayedListener</span></span>

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

##### <a name="createrelayedserver"></a><span data-ttu-id="6ea4b-169">createRelayedServer</span><span class="sxs-lookup"><span data-stu-id="6ea4b-169">createRelayedServer</span></span>

```javascript
var server = createRelayedServer([options], [connectCallback] )
```

<span data-ttu-id="6ea4b-170">이 메서드는 hello 생성자 toocreate hello RelayedServer의 새 인스턴스를 호출 하 고 한 다음 제공 된 hello 콜백 toohello 'connection' 이벤트를 구독.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-170">This method calls hello constructor toocreate a new instance of hello RelayedServer and then subscribes hello provided callback toohello 'connection' event.</span></span>
 
##### <a name="relayedconnect"></a><span data-ttu-id="6ea4b-171">relayedConnect</span><span class="sxs-lookup"><span data-stu-id="6ea4b-171">relayedConnect</span></span>

<span data-ttu-id="6ea4b-172">단순히 hello 미러링 `createRelayedServer` 도우미 함수에서 `relayedConnect` hello 결과 소켓에서 toohello '열기' 이벤트를 구독 하 고 클라이언트 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6ea4b-172">Simply mirroring hello `createRelayedServer` helper in function, `relayedConnect` creates a client connection and subscribes toohello 'open' event on hello resulting socket.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="6ea4b-173">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6ea4b-173">Next steps</span></span>
<span data-ttu-id="6ea4b-174">다음이 링크를 방문 하는 Azure 릴레이 대 한 자세한 toolearn:</span><span class="sxs-lookup"><span data-stu-id="6ea4b-174">toolearn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="6ea4b-175">Azure 릴레이란?</span><span class="sxs-lookup"><span data-stu-id="6ea4b-175">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="6ea4b-176">사용 가능한 Relay API</span><span class="sxs-lookup"><span data-stu-id="6ea4b-176">Available Relay APIs</span></span>](relay-api-overview.md)
