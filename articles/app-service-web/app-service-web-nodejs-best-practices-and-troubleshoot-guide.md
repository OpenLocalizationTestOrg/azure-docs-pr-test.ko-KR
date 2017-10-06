---
title: "aaaBest 사례 및 Azure 웹 앱의 노드 응용 프로그램에 대 한 문제 해결 가이드"
description: "Hello에 대 한 유용한 정보 및 Azure 웹 앱의 노드 응용 프로그램에 대 한 문제 해결 단계에 알아봅니다."
services: app-service\web
documentationcenter: nodejs
author: ranjithr
manager: wadeh
editor: 
ms.assetid: 387ea217-7910-4468-8987-9a1022a99bef
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 06/06/2016
ms.author: ranjithr
ms.openlocfilehash: 975898142a224f14df1091a46d16e9074d9e2831
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-and-troubleshooting-guide-for-node-applications-on-azure-web-apps"></a>Azure 웹앱에서 노드 응용 프로그램에 대한 모범 사례 및 문제 해결 가이드
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

이 문서에서는 배웁니다 hello에 대 한 유용한 정보 및 문제 해결 단계에 대 한 [node 응용 프로그램](app-service-web-get-started-nodejs.md) Webapps Azure에서 실행 중인 (으로 [iisnode](https://github.com/azure/iisnode)).

> [!WARNING]
> 프로덕션 사이트에서 문제 해결 단계를 사용할 때는 주의하세요. 권장 사항은 tootroubleshoot 응용 프로그램에 비-프로덕션 예를 들어 프로그램 스테이징 슬롯을 설정 하 고 hello 문제를 해결할 때 프로덕션 슬롯에 스테이징 슬롯의 교환 합니다.
> 
> 

## <a name="iisnode-configuration"></a>IISNODE 구성
이 [스키마 파일](https://github.com/Azure/iisnode/blob/master/src/config/iisnode_schema_x64.xml) iisnode에 대해 구성할 수 있는 모든 hello 설정을 보여 줍니다. 응용 프로그램에 대 한 유용한 여러 가지 hello 설정을 다음과 같습니다.

* nodeProcessCountPerApplication
  
    이 설정은 IIS 응용 프로그램 마다 실행 되는 노드 프로세스의 hello 개수를 제어 합니다. 기본값은 1입니다. 이 too0를 설정 하 여 많은 node.exe VM 코어 수로 시작할 수 있습니다. 권장된 값 대부분의 응용 프로그램에 대 한 0 이므로 hello 코어의 모든 컴퓨터에 사용할 수 있습니다. Node.exe는 단일 스레드이므로 한 node.exe 최대 1 core 및 tooget에서 최대 성능 node 응용 프로그램을 사용 하면 원할 tooutilize 모든 코어입니다.
* nodeProcessCommandLine
  
    이 설정은 hello 경로 toohello node.exe를 제어합니다. 이 값 toopoint tooyour node.exe 버전을 설정할 수 있습니다.
* maxConcurrentRequestsPerProcess
  
    이 설정은 hello iisnode tooeach node.exe 보낸 동시 요청의 최대 수를 제어 합니다. Azure webapps에 hello이 기본값이 무한 합니다. 이 설정에 대 한 tooworry를 체계가 없습니다. Azure webapps 외부 hello 기본값은 1024입니다. 몇 개의 응용 프로그램 요청에 따라이 tooconfigure 및 응용 프로그램에서 각 요청을 처리 하는 속도 할 수 있습니다.
* maxNamedPipeConnectionRetry
  
    이 설정은 제어 hello 최대 횟수 iisnode toonode.exe 통해 파이프 toosend hello 요청을 명명 된 hello에 함으로써 연결을 다시 시도 합니다. 이 설정은 namedPipeConnectionRetryDelay 함께에서 iisnode 내에서 각 요청의 총 시간 제한 hello를 결정합니다. azure 웹앱에서 기본값이 200입니다. 총 시간 제한(초) = (maxNamedPipeConnectionRetry \* namedPipeConnectionRetryDelay) / 1000
* namedPipeConnectionRetryDelay
  
    이러한 설정은 컨트롤 hello 양의 시간 (밀리초) iisnode hello 명명 된 파이프를 통해 각 재시도 toosend 요청 toonode.exe 사이 기다립니다. 기본값은 250ms입니다.
    총 시간 제한(초) = (maxNamedPipeConnectionRetry \* namedPipeConnectionRetryDelay) / 1000
  
    기본적으로 azure webapps에 iisnode에서 총 시간 제한 hello는 200 \* 증가가 = 50 초로 설정 합니다.
* logDirectory
  
    이 설정은 제어 hello 디렉터리 iisnode stdout/stderr를 기록 합니다. 기본값은 iisnode 디렉터리인 상대 toohello 주 스크립트 (where 주 server.js가 있는 디렉터리)
* debuggerExtensionDll
  
    이 설정은 노드 응용 프로그램을 디버깅할 때 node-inspector iisnode가 사용할 버전을 제어합니다. 현재 iisnode-관리자-0.7.3.dll 및 iisnode inspector.dll는 hello 2만 유효한 값이이 설정에 대 한 합니다. 기본값은 iisnode-inspector-0.7.3.dll입니다. iisnode-관리자-0.7.3.dll 버전 노드-관리자-0.7.3 tooenable websocket에서 필요한 azure webapp toouse이이 버전 하므로 websocket을 사용 하 합니다. 참조 <http://www.ranjithr.com/?p=98> tooconfigure iisnode toouse 새 노드 검사기 hello 하는 방법에 대 한 자세한 내용은 합니다.
* flushResponse
  
    hello 기본 IIS의 동작은에 플러시하기 전에 too4MB 응답 데이터를 버퍼링 하거나 hello 응답을 hello 완료 될 때까지 중 먼저 끝나는 쪽입니다. iisnode toooverride이이 동작을 설정 하는 구성을 제공: tooflush hello 응답 엔터티 본문의 조각 iisnode 빨리 수신에서 node.exe를 tooset hello iisnode/@flushResponse web.config too'true의 특성 ':
  
    ```
    <configuration>    
        <system.webServer>    
            <!-- ... -->    
            <iisnode flushResponse="true" />    
        </system.webServer>    
    </configuration>
    ```
  
    Hello 응답 엔터티 본문의 모든 조각의 플러시을 사용 하면 (현재 v0.1.13) ~ 5 %hello 시스템의 hello 처리량을 감소 된 성능 오버 헤드를 추가, 것 이므로 tooscope 응답 스트리밍 (예:를 사용 하 여 hello를 필요로 하는이 설정을 tooendpoints를 가장 <location> hello web.config의 요소)
  
    응용 프로그램의 경우 스트리밍에 대 한 추가 toothis에서 iisnode 처리기 too0의 tooalso 집합 responseBufferLimit 해야 합니다.
  
    ```
    <handlers>    
        <add name="iisnode" path="app.js" verb="\*" modules="iisnode" responseBufferLimit="0"/>    
    </handlers>
    ```
* watchedFiles
  
    변경 내용을 감시하는 세미콜론으로 구분된 파일 목록입니다. 변경 tooa 파일 hello 응용 프로그램 toorecycle를 하면 됩니다. 각 항목 선택적 디렉터리 이름과 상대 toohello hello 주 응용 프로그램 진입점 위치한 디렉터리는 필요한 파일 이름 구성 됩니다. Hello 파일 이름 부분은에 와일드 카드는 사용할 수 있습니다. 기본값은 "\*.js;web.config"입니다.
* recycleSignalEnabled
  
    기본값은 False입니다. Node 응용 프로그램 tooa 명명 된 파이프를 연결할 수 있습니다를 사용 하는 경우 (환경 변수 IISNODE\_제어\_파이프) "재생" 메시지를 보냅니다. 이렇게 hello w3wp toorecycle를 하면 적절 하 게 됩니다.
* idlePageOutTimePeriod
  
    기본값은 이 기능을 사용하지 않는다는 의미의 0입니다. 모든 자식 아웃 설정 toosome 값 iisnode 0 보다 큰 경우 페이징하지 'idlePageOutTimePeriod' 밀리초 마다 처리 합니다. toounderstand 방법으로 대상 페이지를 참조 하십시오. toothis [설명서](https://msdn.microsoft.com/library/windows/desktop/ms682606.aspx)합니다. 이 설정은 toopageout 메모리 toodisk 하 고 메모리를 많이 소비 하는 응용 프로그램에 대 한 유용할 일부 RAM toofree 가끔 있습니다.

> [!WARNING]
> Hello 나오는 프로덕션 응용 프로그램에 따라 구성 설정을 사용 하도록 설정할 때는 주의 해야 합니다. 권장 사항은 toonot 라이브 프로덕션 응용 프로그램에서 사용할 수 있도록 합니다.
> 
> 

* debugHeaderEnabled
  
    hello 기본값은 false입니다. 경우 tootrue, 설정 iisnode hello iisnode 디버그 헤더 값은 URL 보내는 HTTP 응답 헤더 iisnode 디버그 tooevery HTTP 응답을 추가 합니다. Hello URL 조각 확인 하 여 개별 가지 진단 정보를 수집할 수 있지만 더 나은 시각화 hello URL hello 브라우저에서 열에 의해 이루어집니다.
* loggingEnabled
  
    이 설정은 iisnode stdout 및 stderr의 hello 로깅을 제어합니다. Iisnode 시작 노드 프로세스에서 stdout/stderr 캡처하고 toohello 디렉터리 hello '로그 디렉터리' 설정에 지정 된 쓰기 됩니다. 사용 되 면 응용 프로그램 로그 toohello 파일 시스템에 기록 및 로깅 hello 응용 프로그램에 의해 수행 양을 hello 따라 있을 수 성능에 미치는 영향입니다.
* devErrorsEnabled
  
    기본값은 False입니다. Tootrue, 설정 된 경우 iisnode hello HTTP 상태 코드 및 Win32 오류 코드를 브라우저에 표시 됩니다. hello win32 코드는 특정 유형의 문제를 디버깅 하는 데 도움이 됩니다.
* debuggingEnabled(라이브 프로덕션 사이트에서 사용 안 함)
  
    이 설정은 디버깅 기능을 제어합니다. Iisnode는 node-inspector에 통합됩니다. 이 설정을 사용하여 노드 응용 프로그램의 디버깅을 사용하도록 설정합니다. 이 설정을 활성화 되 면 iisnode 레이아웃 hello 필요한 노드 검사기 'debuggerVirtualDir' 디렉터리에 파일 hello 첫 번째 디버그 요청 tooyour 노드 응용 프로그램 됩니다. 요청 toohttp://yoursite/server.js/debug 전송 하 여 hello 노드 검사를 로드할 수 있습니다. 'DebuggerPathSegment' 설정을 사용 하 여 hello 디버그 URL 세그먼트를 제어할 수 있습니다. 기본적으로 debuggerPathSegment='debug'입니다. 다른 사용자가 검색 하기가 더 어려워지므로 toobe 있도록 예를 들어가이 tooa GUID를 설정할 수 있습니다.
  
    디버깅에 대한 자세한 내용은 이 [링크](https://tomasz.janczuk.org/2011/11/debug-nodejs-applications-on-windows.html) 를 확인하세요.

## <a name="scenarios-and-recommendationstroubleshooting"></a>시나리오 및 권장 사항/문제 해결
### <a name="my-node-application-is-making-too-many-outbound-calls"></a>내 노드 응용 프로그램에서 너무 많은 아웃바운드 호출을 생성합니다.
대부분의 응용 프로그램의 일반 작업의 일부로 toomake 아웃 바운드 연결 하 게 됩니다. 예를 들어 대 한 요청이 들어오면 노드 앱 toocontact REST API를 다른 곳에서 원하는 고 게 get 일부 정보 tooprocess hello 요청 됩니다. Http 또는 https을 호출할 때 toouse keep alive 에이전트를 사용할 수 있습니다. 예를 들어 이러한 아웃 바운드 호출 하는 경우 keep alive 에이전트로 hello agentkeepalive 모듈을 사용할 수 있습니다. 이렇게 하면 hello 소켓 azure webapp VM 및 아웃 바운드 요청을 보낼 때마다 새 소켓 만드는 줄여서 hello 오버 헤드에 사용 됩니다. 또한 이렇게 하면 많은 아웃 바운드 요청 및 따라서 하면 VM 당 할당 되는 hello maxSockets를 초과 하지 않도록 하는 소켓 toomake 수를 사용 하는입니다. Azure Webapps을 위한 권장 tooset hello agentKeepAlive maxSockets VM 당 160 소켓의 tooa 총 값 수 있습니다. 이 hello VM에서 실행 되는 4 node.exe를 설정한 경우 VM 당 총 160 인 node.exe 당 tooset hello agentKeepAlive maxSockets too40 원하는 것을 의미 합니다.

[agentKeepALive](https://www.npmjs.com/package/agentkeepalive) 구성 예제:

```
var keepaliveAgent = new Agent({    
    maxSockets: 40,    
    maxFreeSockets: 10,    
    timeout: 60000,    
    keepAliveTimeout: 300000    
});
```

이 예에서는 VM에서 4개의 node.exe를 실행 중이라고 가정합니다. Node.exe hello VM에서 실행 되는 다른 개수의 설정한 경우 toomodify hello maxSockets 적절 하 게 설정 해야 합니다.

### <a name="my-node-application-is-consuming-too-much-cpu"></a>내 노드 응용 프로그램이 너무 많은 CPU를 사용하고 있습니다.
포털의 Azure 웹앱에서 높은 cpu 사용량에 대한 권장 사항을 받게 됩니다. 수도 있습니다 설치 모니터 toowatch 특정 [메트릭](web-sites-monitor.md)합니다. Hello에 hello CPU 사용량을 확인할 때 [Azure 포털의 대시보드](../application-insights/app-insights-web-monitor-performance.md), hello 최고 값 아웃 잊지 하므로 CPU에 대 한 hello 최대 값 확인 하십시오.
응용 프로그램 CPU를 너무 많이 사용 하 고 이유를 설명할 수 없는 생각 하는 경우에서 tooprofile를 노드 응용 프로그램이 필요 합니다.

### 
#### <a name="profiling-your-node-application-on-azure-webapps-with-v8-profiler"></a>azure 웹앱에서 V8-Profiler로 노드 응용 프로그램 프로파일링
예를 들어 있을 때는 상황이 아래와 같이 않겠다고 tooprofile hello world 응용 프로그램:

```
var http = require('http');    
function WriteConsoleLog() {    
    for(var i=0;i<99999;++i) {    
        console.log('hello world');    
    }    
}

function HandleRequest() {    
    WriteConsoleLog();    
}

http.createServer(function (req, res) {    
    res.writeHead(200, {'Content-Type': 'text/html'});    
    HandleRequest();    
    res.end('Hello world!');    
}).listen(process.env.PORT);
```

Tooyour scm 사이트 https://yoursite.scm.azurewebsites.net/DebugConsole 이동

아래와 같이 명령 프롬프트가 표시됩니다. site/wwwroot 디렉터리로 이동합니다.

![](./media/app-service-web-nodejs-best-practices-and-troubleshoot-guide/scm_install_v8.png)

"Npm 설치 v8 프로파일러" hello 명령 실행

그러면 node\_modules 디렉터리 아래에 v8-profiler와 모든 종속성이 설치됩니다.
이제 server.js tooprofile 응용 프로그램을 편집 합니다.

```
var http = require('http');    
var profiler = require('v8-profiler');    
var fs = require('fs');

function WriteConsoleLog() {    
    for(var i=0;i<99999;++i) {    
        console.log('hello world');    
    }    
}

function HandleRequest() {    
    profiler.startProfiling('HandleRequest');    
    WriteConsoleLog();    
    fs.writeFileSync('profile.cpuprofile', JSON.stringify(profiler.stopProfiling('HandleRequest')));    
}

http.createServer(function (req, res) {    
    res.writeHead(200, {'Content-Type': 'text/html'});    
    HandleRequest();    
    res.end('Hello world!');    
}).listen(process.env.PORT);
```

변경 내용 위에 hello hello WriteConsoleLog 함수 프로 파일링 되며 hello 프로필 출력 too'profile.cpuprofile 작성 한 다음 ' 파일에서 사이트 wwwroot 합니다. 요청 tooyour 응용 프로그램을 보냅니다. 사이트의 wwwroot 아래에 'profile.cpuprofile' 파일이 생성된 것을 확인할 수 있습니다.

![](./media/app-service-web-nodejs-best-practices-and-troubleshoot-guide/scm_profile.cpuprofile.png)

이 파일을 다운로드 하 고 tooopen 크롬 F12 도구와 함께이 파일이 필요 합니다. Chrome에서 F12 적중 "프로필 탭" hello에서 클릭 합니다. "로드" 단추를 클릭합니다. 방금 다운로드한 profile.cpuprofile 파일을 선택합니다. 방금 로드 hello 프로필을 클릭 합니다.

![](./media/app-service-web-nodejs-best-practices-and-troubleshoot-guide/chrome_tools_view.png)

아래와 같이 hello 시간의 95 %WriteConsoleLog 함수에서 사용한 표시 됩니다. 이 또한 보면 hello 정확한 줄 번호 및 hello 문제가 발생 하는 소스 파일.

### <a name="my-node-application-is-consuming-too-much-memory"></a>내 노드 응용 프로그램이 너무 많은 메모리를 사용하고 있습니다.
포털의 Azure 웹앱에서 높은 메모리 사용량에 대한 권장 사항을 받게 됩니다. 수도 있습니다 설치 모니터 toowatch 특정 [메트릭](web-sites-monitor.md)합니다. Hello에 hello 메모리 사용량을 확인할 때 [Azure 포털의 대시보드](../application-insights/app-insights-web-monitor-performance.md), hello 최고 값 아웃 잊지 되므로 메모리에 대 한 hello 최대 값을 확인 하십시오.

#### <a name="leak-detection-and-heap-diffing-for-nodejs"></a>node.js에 대한 누수 감지 및 힙 Diff
사용할 수 있습니다 [노드 memwatch](https://github.com/lloyd/node-memwatch) 누수 toohelp 메모리를 식별 합니다.
응용 프로그램에 프로파일러 v8 및 편집 코드 toocapture 및 diff 힙을 tooidentify hello 메모리 누수와 마찬가지로 memwatch를 설치할 수 있습니다.

### <a name="my-nodeexes-are-getting-killed-randomly"></a>내 node.exe가 임의로 중지됨
이러한 현상이 발생하는 몇 가지 이유가 있습니다.

1. 응용 프로그램를 throw 하는 확인할 수 없는 예외 – 하세요 검사 d:\\홈\\LogFiles\\응용 프로그램\\hello 예외 발생 시 hello 세부 정보에 대 한 로깅 errors.txt 파일입니다. 이 파일에이에 따라 응용 프로그램 수정 hello 스택 추적이 있습니다.
2. 응용 프로그램에서 너무 많은 메모리를 사용하여 다른 프로세스가 시작되는 데 영향을 줍니다. Node.exe의을 중지할 수 hello 총 VM 메모리 닫기 too100% 인 경우 hello 프로세스 관리자 toolet 다른 프로세스 확보할 기회 toodo 몇 가지 작업입니다. toofix이 응용 프로그램 메모리 누수가 아닙니다 있는지 확인 하거나 실제로 toouse 메모리가 매우 많이 필요한 응용 프로그램 하십시오를 확대 tooa 더 많은 ram이 더 큰 VM입니다.

### <a name="my-node-application-does-not-start"></a>내 노드 응용 프로그램이 시작되지 않음
응용 프로그램 시작 시 500 오류를 반환하는 경우 몇 가지 원인이 있을 수 있습니다.

1. Node.exe는 hello 올바른 위치에 나타나지 않습니다. nodeProcessCommandLine 설정을 확인합니다.
2. 기본 스크립트 파일 hello 올바른 위치에 나타나지 않습니다. Web.config hello 처리기 섹션 일치 hello 주 스크립트 파일에 hello 주 스크립트 파일의 hello 이름이 있는지 확인 하십시오.
3. Web.config 구성이 잘못 되었습니다-hello 설정 이름/값을 확인 합니다.
4. 콜드 시작-응용 프로그램 toostartup 너무 오래 걸리고 있습니다. 응용 프로그램이 (maxNamedPipeConnectionRetry \* namedPipeConnectionRetryDelay) / 1000초보다 오래 걸리면 iisnode에서 500 오류를 반환합니다. 이러한 설정 toomatch hello 500 오류를 반환 하 고 제한 시간 초과 시간 tooprevent iisnode를 시작 하는 응용 프로그램의 hello 값을 늘립니다.

### <a name="my-node-application-crashed"></a>내 노드 응용 프로그램에 충돌 발생
응용 프로그램를 throw 하는 확인할 수 없는 예외 – 하세요 검사 d:\\홈\\LogFiles\\응용 프로그램\\hello 예외 발생 시 hello 세부 정보에 대 한 로깅 errors.txt 파일입니다. 이 파일에이에 따라 응용 프로그램 수정 hello 스택 추적이 있습니다.

### <a name="my-node-application-takes-too-much-time-toostartup-cold-start"></a>내 노드 응용 프로그램이 우선권을 너무 많은 시간 toostartup (콜드 시작)
가장 일반적인 이유는 hello 응용 프로그램에는 많은 hello 노드에 파일\_모듈 및 hello 응용 프로그램 시도 tooload 시작 하는 동안 이러한 파일의 대부분 합니다. 기본적으로 너무 많은 파일을 로드할 파일 Azure Webapps hello 네트워크 공유에 상주 하므로 약간의 시간이 걸릴 수 있습니다.
이 더 빠르게 솔루션 toomake 일부:

1. 모듈 npm3 tooinstall를 사용 하 여 플랫 종속성 구조와 중복 된 종속성을 가진 있는지 확인 합니다.
2. 노드가 toolazy 로드 시도\_모듈의 모든 시작 시 hello 모듈을 로드 하지 합니다. 즉, 실제로 필요할 때 수행 해야 하는 hello 호출 toorequire('module') toouse hello 모듈 hello 함수 내에서 하려고 합니다.
3. Azure 웹앱은 로컬 캐시라는 기능을 제공합니다. 이 기능은 hello 네트워크 공유 toohello 로컬 디스크에 hello VM에서 콘텐츠를 복사합니다. 로컬 hello 파일 이므로 hello 로드 시간 노드의\_모듈 훨씬 빠릅니다. -이 [설명서](../app-service/app-service-local-cache.md) 방법을 toouse 로컬 캐시에서 더 자세히 설명에 대해 설명 합니다.

## <a name="iisnode-http-status-and-substatus"></a>IISNODE http 상태 및 하위 상태
이 [소스 파일](https://github.com/Azure/iisnode/blob/master/src/iisnode/cnodeconstants.h) 목록 모든 hello 가능한 상태/하위 상태 조합 iisnode 오류 발생 시 반환할 수 있습니다.

응용 프로그램 toosee hello win32 오류 코드에 대 한 FREB를 설정 (있는지 확인 하십시오 FREB 성능상의 이유로 비-프로덕션 사이트에만 사용 하도록 설정).

| HTTP 상태 | HTTP 하위 상태 | 가능한 원인 |
| --- | --- | --- |
| 500 |1000 |Hello 요청 tooIISNODE 디스패치 몇 가지 문제가 발생 했습니다.-node.exe 시작한 경우를 확인 합니다. Node.exe가 시작 시 충돌되었을 수 있습니다. web.config 구성에 오류가 있는지 확인하세요. |
| 500 |1001 |-Win32Error 0x2-응용 프로그램 toohello URL 응답 하지 않습니다. 확인 URL에는 규칙 또는 빠른 응용 프로그램에 정의 된 hello 올바른 경로 경우 다시 작성 합니다. -Win32Error 0x6d – 명명 된 파이프 사용 중입니다-Node.exe hello 파이프 사용 중이기 때문에 요청을 수락 하지 않습니다. 높은 cpu 사용량을 확인하세요. - 기타 오류 – node.exe가 충돌되었는지 확인하세요. |
| 500 |1002 |Node.exe가 충돌됨 – d:\\home\\LogFiles\\logging-errors.txt에서 스택 추적을 확인하세요. |
| 500 |1003 |파이프 구성 문제가 표시 되 면 안이 있지만 이렇게 하면 hello 파이프 구성 이름이 올바르지 않습니다. |
| 500 |1004-1018 |으로/에서 node.exe hello 요청 또는 처리 hello 응답을 보내는 동안 일부 오류가 발생이 했습니다. Node.exe가 충돌되었는지 확인하세요. d:\\home\\LogFiles\\logging-errors.txt에서 스택 추적을 확인하세요. |
| 503 |1000 |메모리 tooallocate 더 명명 된 파이프 연결 충분 하지 않습니다. 앱에서 많은 메모리를 사용하는 이유를 확인하세요. maxConcurrentRequestsPerProcess 설정 값을 확인하세요. 경우 아닙니다 infinite 하 고 요청을 많이 있는,이 값 tooprevent이이 오류를 늘립니다. |
| 503 |1001 |Hello 응용 프로그램 재활용 되 요청 디스패치 된 toonode.exe 수 없습니다. Hello 응용 프로그램 재생 된 후 요청이 정상적으로 처리 됩니다. |
| 503 |1002 |실제 이유가 – 요청에 대 한 확인 win32 오류 코드에 디스패치 된 tooa node.exe를 사용할 수 없습니다. |
| 503 |1003 |명명된 파이프 사용량이 너무 많음 – 노드에서 많은 CPU를 사용 중인지 확인하세요. |

NODE.exe 내에 NODE\_PENDING\_PIPE\_INSTANCES라는 설정이 있습니다. 기본적으로 azure 웹앱 이외에서는 이 값은 4입니다. 즉, 해당 node.exe hello 명명 된 파이프에 한 번에 요청 4 받아들일 수 있습니다. Azure Webapps이이 값은 too5000를 설정 하 고이 값은 azure webapps에서 실행 되는 대부분 노드 응용 프로그램에 맞게 이어야 합니다. 표시 되지 않습니다 503.1003 azure webapps에 hello 노드 값이 높은 지정 했으므로\_PENDING\_파이프\_인스턴스.  |

## <a name="more-resources"></a>추가 리소스
Azure 앱 서비스에 node.js 응용 프로그램에 대 한 자세한 이러한 링크 toolearn를 따릅니다.

* [Azure 앱 서비스에서 Node.js 웹앱 시작](app-service-web-get-started-nodejs.md)
* [어떻게 toodebug는 Node.js 웹 응용 프로그램을 Azure 앱 서비스](web-sites-nodejs-debug.md)
* [Azure 응용 프로그램에 Node.js 모듈 사용](../nodejs-use-node-modules-azure-apps.md)
* [Azure 앱 서비스 웹앱: Node.js](https://blogs.msdn.microsoft.com/silverlining/2012/06/14/windows-azure-websites-node-js/)
* [Node.js 개발자 센터](../nodejs-use-node-modules-azure-apps.md)
* [Hello 슈퍼 비밀 Kudu 디버그 콘솔 탐색](https://azure.microsoft.com/documentation/videos/super-secret-kudu-debug-console-for-azure-web-sites/)

