---
title: "Azure 앱 서비스에서 Socket.IO를 사용하여 Node.js 채팅 응용 프로그램 만들기"
description: "Azure에서 호스트되는 node.js 웹 앱에서 socket.io를 사용하는 방법을 보여 주는 자습서입니다."
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: c4c4af36-3ecf-4619-b586-ca90d53ce35b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: e1aa539e1134884261ea7464bfda6d14815618d4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-nodejs-chat-application-with-socketio-in-azure-app-service"></a>Azure 앱 서비스에서 Socket.IO를 사용하여 Node.js 채팅 응용 프로그램 만들기
Socket.IO는 WebSocket을 사용하여 node.js 서버와 클라이언트 간의 실시간 통신을 제공합니다. 또한 이전 브라우저에서 작동하는 다른 전송(예: 긴 폴링)으로의 대체를 지원합니다. 이 자습서는 Azure 웹앱으로 Socket.IO를 기반으로 하는 호스팅을 안내하고 [Azure Redis Cache]를 사용하여 응용 프로그램의 크기를 조정하는 방법을 보여줍니다. Socket.IO에 대한 자세한 내용은 <http://socket.io/>(영문)를 참조하세요.

> [!NOTE]
> 이 작업의 절차는 [App Service Web Apps]에 적용됩니다. 클라우드 서비스에 대해서는 [Azure 클라우드 서비스에서 Socket.IO를 사용하여 Node.js 채팅 응용 프로그램 빌드]를 참조하세요.
> 
> 

## <a name="download-the-chat-example"></a>채팅 예제 다운로드
이 프로젝트에서는 [Socket.IO GitHub 리포지토리](영문)의 채팅 예제를 사용합니다. 다음 단계에 따라 예제를 다운로드하여 이전에 만든 프로젝트에 추가하세요.

1. Socket.IO 프로젝트의 [ZIP 또는 GZ 보관 릴리스] 를 다운로드합니다(이 문서에서는 버전 1.3.5 사용).
2. 보관 파일을 추출하고 **examples\\chat** 디렉터리를 새 위치에 복사합니다. 예를 들어 **\\node\\chat**입니다.

## <a name="modify-appjs-and-install-modules"></a>app.js 수정 및 모듈 설치
1. **index.js** 파일의 이름을 **app.js**로 바꿉니다. 그러면 Azure에서 이 파일을 Node.js 응용 프로그램으로 검색할 수 있습니다.
2. 텍스트 편집기에서 **app.js** 파일을 엽니다. 아래와 같이 `var io = require('../..')(server);` 을 포함한 줄을 변경합니다.
   
       var express = require('express');
       var app = express();
       var server = require('http').createServer(app);
       // var io = require('../..')(server);
       // New:
       var io = require('socket.io')(server);
       var port = process.env.PORT || 3000;
3. 아래와 같이 **package.json** 파일을 열고 `dependencies` 아래의 socket.io에 참조를 추가합니다.
   
        "dependencies": {
          "express": "3.4.8",
          "socket.io": "1.3.5"
        }
4. 명령줄에서 **\\node\\chat** 디렉터리로 변경하고 npm을 사용하여 이 응용 프로그램에 필요한 모듈을 설치합니다.
   
        npm install
   
    이는 모듈을 **node_modules**라는 하위 폴더에 설치합니다.

## <a name="create-an-azure-web-app"></a>Azure 웹 앱 만들기
다음 단계에 따라 Azure 웹 앱을 만들고, Git 게시를 사용하도록 설정한 다음, 웹 앱에 대한 WebSocket 지원을 사용하도록 설정합니다.

> [!NOTE]
> 이 자습서를 완료하려면 Azure 계정이 필요합니다. 계정이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다. 자세한 내용은 <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Azure 무료 평가판</a>을 참조하세요.
> 
> 

1. Azure CLI(Azure 명령줄 인터페이스)를 설치하고 Azure 구독에 연결합니다. [Azure CLI 설치 및 구성](../cli-install-nodejs.md)을 참조하세요.
2. Azure에서 리포지토리를 처음 설정하는 경우 로그인 자격 증명을 만들어야 합니다. Azure CLI에서 다음 명령을 입력합니다.
   
        azure site deployment user set [username] [password]
3. **\\node\chat** 디렉터리로 변경하고 다음 명령을 사용하여 새 Azure 웹앱 및 로컬 Git 리포지토리를 만듭니다. 이 명령은 'azure'라는 Git 원격도 만듭니다.
   
        azure site create mysitename --git
   
    'mysitename'을 웹 앱의 고유한 이름으로 바꿔야 합니다.
4. 다음 명령을 사용하여 기존 파일을 로컬 리포지토리로 커밋합니다.
   
        git add .
        git commit -m "Initial commit"
5. 다음 명령으로 파일을 Azure 웹 앱 리포지토리로 푸시합니다.
   
        git push azure master
   
    메시지가 표시되면 2단계에서 자격 증명을 입력합니다. 서버에서 모듈을 가져올 때 상태 메시지가 표시됩니다. 이 프로세스가 완료되면 응용 프로그램이 Azure 웹 앱에 호스트됩니다.
   
   > [!NOTE]
   > 모듈이 설치되는 동안 'The imported project ... was not found' 오류가 발생할 수 있습니다. 이 오류는 무시해도 됩니다.
   > 
   > 
6. Socket.IO는 Azure에서 기본적으로 사용되지 않는 WebSocket을 사용합니다. WebSocket을 사용하도록 설정하려면 다음 명령을 사용하십시오.
   
        azure site set -w
   
    메시지가 표시되면 웹 앱 이름을 입력하세요.
   
   > [!NOTE]
   > 'azure site set -w' 명령은 버전 0.7.4 이상의 Azure 명령줄 인터페이스에서만 작동합니다. 또한 [Azure 포털](https://portal.azure.com)에서 WebSocket 지원을 사용하도록 설정할 수도 있습니다.
   > 
   > Azure Portal에서 WebSocket을 사용하도록 설정하려면 Web Apps 블레이드에서 해당 웹앱을 클릭하고 **모든 설정** > **응용 프로그램 설정**을 클릭합니다. **웹 소켓**에서 **켜기**를 클릭합니다. 그런 다음 **Save**를 클릭합니다.
   > 
   > 
7. Azure에서 웹 앱을 보려면 다음 명령을 사용하여 웹 브라우저를 시작하고 호스트되는 웹 앱으로 이동합니다.
   
        azure site browse

현재 앱이 Azure에서 실행되고 있으며 Socket.IO를 사용하여 다른 클라이언트 간에 채팅 메시지를 릴레이할 수 있습니다.

## <a name="scale-out"></a>확장
**어댑터**를 사용하여 여러 응용 프로그램 인스턴스 간에 메시지 및 이벤트를 배포하는 방식으로 Socket.IO 응용 프로그램을 확장할 수 있습니다. 사용 가능한 여러 어댑터가 있지만 Azure Redis 캐시 기능에 사용하기 편리한 어댑터는 [socket.io-redis] 어댑터입니다.

> [!NOTE]
> Socket.IO 솔루션 확장에 대한 추가 요구 사항은 고정 세션의 지원입니다. 고정 세션은 Azure 요청 라우팅을 통해 Azure 웹 앱에서 기본적으로 사용하도록 설정됩니다. 자세한 내용은 [Azure 웹 사이트의 인스턴스 선호도]를 참조하세요.
> 
> 

### <a name="create-a-redis-cache"></a>Redis 캐시 만들기
[Azure Redis 캐시에서 캐시 만들기] 의 단계를 수행하여 새 캐시를 만듭니다.

> [!NOTE]
> 캐시의 **호스트 이름** 및 **기본 키**를 저장합니다. 이러한 정보는 다음 단계에서 필요합니다.
> 
> 

### <a name="add-the-redis-and-socketio-redis-modules"></a>Redis 및 socket.io-redis 모듈 추가
1. 명령줄에서 **\\node\\chat** 디렉터리로 변경하여 다음 명령을 사용합니다.
   
        npm install socket.io-redis@0.1.4 redis@0.12.1 --save
   
   > [!NOTE]
   > 이 명령에 지정된 버전은 이 문서를 테스트할 때 사용된 버전입니다.
   > 
   > 
2. **app.js** 파일을 수정하여 다음 줄을 `var io = require('socket.io')(server);` 바로 뒤에 추가합니다.
   
        var pub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
        var sub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
   
        var redis = require('socket.io-redis');
        io.adapter(redis({pubClient: pub, subClient: sub}));
   
    **redishostname** 및 **rediskey**를 Redis 캐시의 호스트 이름 및 키로 바꿉니다.
   
    그러면 이전에 만든 Redis 캐시에 대한 게시 및 구독 클라이언트가 만들어집니다. 이 클라이언트는 어댑터에서 응용 프로그램의 인스턴스 간에 메시지 및 이벤트를 전달하는 데 Redis 캐시를 사용하도록 Socket.IO를 구성하는 데 사용됩니다.
   
   > [!NOTE]
   > **socket.io-redis** 어댑터는 Redis와 직접 통신할 수 있지만 현재 버전에서는 Azure Redis 캐시에 필요한 인증을 지원하지 않습니다. 따라서 **redis** 모듈을 통해 초기 연결이 만들어진 다음 **socket.io-redis** 어댑터로 클라이언트가 전달됩니다.
   > 
   > Azure Redis 캐시는 포트 6380을 사용한 보안 연결을 지원하지만 이 예제에 사용된 모듈에서는 2014년 7월 14일 현재 보안 연결을 지원하지 않습니다. 위의 코드에서는 기본적으로 비보안 포트 6379를 사용합니다.
   > 
   > 
3. 수정한 **app.js** 저장

### <a name="commit-changes-and-redeploy"></a>변경 내용 커밋 및 다시 배포
**\\node\\chat** 디렉터리의 명령줄에서 다음 명령을 사용하여 변경 내용을 커밋하고 응용 프로그램을 다시 배포합니다.

    git add .
    git commit -m "implementing scale out"
    git push azure master

변경 내용이 서버에 푸시되고 나면 다음 명령을 사용하여 여러 인스턴스 간에 사이트를 확장할 수 있습니다.

    azure site scale instances --instances #

여기서 **#**은 만들 인스턴스 수입니다.

여러 브라우저 또는 컴퓨터에서 웹 앱에 연결하여 메시지가 모든 클라이언트에 올바르게 전송되었는지 확인할 수 있습니다.

## <a name="troubleshooting"></a>문제 해결
### <a name="connection-limits"></a>연결 제한
Azure 웹 앱은 여러 SKU에서 사용할 수 있으며, 이러한 SKU에 따라 사이트에 사용 가능한 리소스가 결정됩니다. 여기에는 허용되는 WebSocket 연결 수가 포함됩니다. 자세한 내용은 [웹 앱 가격 책정 페이지]를 참조하세요.

### <a name="messages-arent-being-sent-using-websockets"></a>메시지가 WebSocket을 사용하여 전송되지 않음
클라이언트 브라우저에서 WebSocket을 사용하는 대신 긴 폴링으로의 대체를 유지하는 경우 다음 중 하나가 원인일 수 있습니다.

* **전송을 WebSocket으로만 제한**
  
    Socket.IO에서 WebSocket을 메시징 전송으로 사용하려면 서버와 클라이언트가 모두 WebSocket을 지원해야 합니다. 둘 중 하나가 지원하지 않으면 Socket.IO에서 긴 폴링과 같은 다른 전송을 협상합니다. Socket.IO에서 사용하는 기본 전송 목록은 ` websocket, htmlfile, xhr-polling, jsonp-polling`입니다. **app.js** 파일에서 `, nicknames = {};`가 포함된 줄 뒤에 다음 코드를 추가하여 Socket.IO에서 WebSocket만 사용하도록 강제로 설정할 수 있습니다.
  
        io.configure(function() {
          io.set('transports', ['websocket']);
        });
  
  > [!NOTE]
  > 위 코드가 활성화되어 있는 동안에는 통신이 WebSocket으로만 제한되므로 WebSocket을 지원하지 않는 이전 브라우저에서 사이트에 연결할 수 없게 됩니다.
  > 
  > 
* **SSL 사용**
  
    WebSocket은 **Upgrade** 헤더와 같은 보다 적은 수의 사용된 HTTP 헤더를 기반으로 합니다. 웹 프록시와 같은 일부 중간 네트워크 장치는 이러한 헤더를 제거할 수 있습니다. 이 문제를 방지하기 위해 SSL을 통해 WebSocket 연결을 설정할 수 있습니다.
  
    이 작업을 수행하는 간단한 방법은 `match origin protocol`로 Socket.IO를 구성하는 것입니다. 이 명령은 Socket.IO에 웹 페이지에 대한 시작 HTTP/HTTPS 요청과 동일하게 WebSockets 통신의 보안을 유지하도록 지시합니다. 브라우저에서 HTTPS URL을 사용하여 웹 사이트를 방문한 경우 Socket.IO를 통한 이후의 WebSocket 통신은 SSL을 통해 보안이 유지됩니다.
  
    이 구성을 사용하도록 이 예제를 수정하려면 **app.js** 파일에서 `, nicknames = {};`가 포함된 줄 뒤에 다음 코드를 추가합니다.
  
        io.configure(function() {
          io.set('match origin protocol', true);
        });
* **web.config 설정 확인**
  
    Node.js 응용 프로그램을 호스트하는 Azure 웹 앱에서는 **web.config** 파일을 사용하여 들어오는 요청을 Node.js 응용 프로그램으로 라우팅합니다. Node.js 응용 프로그램에서 WebSocket이 올바르게 작동하려면 **web.config** 에 다음 항목이 포함되어야 합니다.
  
        <webSocket enabled="false"/>
  
    그러면 WebSocket의 자체 구현을 포함하고 Socket.IO와 같은 Node.js 관련 WebSocket 모듈과 충돌하는 IIS WebSocket 모듈이 사용하지 않도록 설정됩니다. 이 줄이 없거나 `true`로 설정되면 WebSocket 전송이 사용자 응용 프로그램에 작동하지 않기 때문일 수 있습니다.
  
    일반적으로 Node.js 응용 프로그램에는 **web.config** 파일이 포함되어 있지 않으므로 Azure 웹 사이트를 배포할 때 해당 웹 사이트에서 Node.js 응용 프로그램에 대해 이 파일을 자동으로 생성합니다. 이 파일은 서버에서 자동으로 생성되기 때문에 이 파일을 보려면 웹 사이트에 FTP 또는 FTPS URL을 사용해야 합니다. 사이트의 FTP 및 FTPS URL은 클래식 포털에서 웹앱을 선택한 후 **대시보드** 링크를 선택하여 찾을 수 있습니다. 이러한 URL은 **간략 상태** 섹션에 표시됩니다.
  
  > [!NOTE]
  > **web.config** 파일은 응용 프로그램에서 제공하지 않는 경우에만 Azure 웹 사이트에서 생성됩니다. 응용 프로그램 프로젝트의 루트에 **web.config** 파일을 제공한 경우에는 Azure 웹 앱에서 이 파일이 사용됩니다.
  > 
  > 
  
    이 항목이 없거나 `true` 값으로 설정된 경우 Node.js 응용 프로그램의 루트에 **web.config**를 만들고 `false` 값을 지정해야 합니다.  참고로 다음은 **app.js**를 진입점으로 사용하는 응용 프로그램의 기본 **web.config**입니다.
  
        <?xml version="1.0" encoding="utf-8"?>
        <!--
             This configuration file is required if iisnode is used to run node processes behind
             IIS or IIS Express.  For more information, visit:
  
             https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config
        -->
  
        <configuration>
          <system.webServer>
            <!-- Visit http://blogs.msdn.com/b/windowsazure/archive/2013/11/14/introduction-to-websockets-on-windows-azure-web-sites.aspx for more information on WebSocket support -->
            <webSocket enabled="false" />
            <handlers>
              <!-- Indicates that the server.js file is a node.js web app to be handled by the iisnode module -->
              <add name="iisnode" path="app.js" verb="*" modules="iisnode"/>
            </handlers>
            <rewrite>
              <rules>
                <!-- Do not interfere with requests for node-inspector debugging -->
                <rule name="NodeInspector" patternSyntax="ECMAScript" stopProcessing="true">
                  <match url="^app.js\/debug[\/]?" />
                </rule>
  
                <!-- First we consider whether the incoming URL matches a physical file in the /public folder -->
                <rule name="StaticContent">
                  <action type="Rewrite" url="public{REQUEST_URI}"/>
                </rule>
  
                <!-- All other URLs are mapped to the node.js web app entry point -->
                <rule name="DynamicContent">
                  <conditions>
                    <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="True"/>
                  </conditions>
                  <action type="Rewrite" url="app.js"/>
                </rule>
              </rules>
            </rewrite>
            <!--
              You can control how Node is hosted within IIS using the following options:
                * watchedFiles: semi-colon separated list of files that will be watched for changes to restart the server
                * node_env: will be propagated to node as NODE_ENV environment variable
                * debuggingEnabled - controls whether the built-in debugger is enabled
  
              See https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config for a full list of options
            -->
            <!--<iisnode watchedFiles="web.config;*.js"/>-->
          </system.webServer>
        </configuration>
  
    사용자 응용 프로그램에서 **app.js**가 아닌 다른 진입점을 사용하는 경우, 표시되는 **app.js**를 모두 올바른 진입점으로 바꿔야 합니다. 예를 들어 **app.js**를 **server.js**로 바꿉니다.

> [!NOTE]
> Azure 계정을 등록하기 전에 Azure App Service를 시작하려면 [App Service 체험]으로 이동합니다. App Service에서 단기 스타터 웹앱을 즉시 만들 수 있습니다. 신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.
> 
> 

## <a name="next-steps"></a>다음 단계
이 자습서에서는 Azure 웹 앱에 호스트되는 기본 채팅 응용 프로그램을 만드는 방법을 알아보았습니다. 이 응용 프로그램은 Azure 클라우드 서비스로 호스트할 수도 있습니다. 이를 수행하는 방법에 대한 단계는 [Azure 클라우드 서비스에서 Socket.IO를 사용하여 Node.js 채팅 응용 프로그램 빌드]를 참조하십시오.

자세한 내용은 [Node.js 개발자 센터]도 참조하세요.

## <a name="whats-changed"></a>변경된 내용
* 웹 사이트에서 앱 서비스로 변경에 대한 지침은 [Azure 앱 서비스와 이 서비스가 기존 Azure 서비스에 미치는 영향]을 참조하세요.

<!-- URL List -->

[Azure Redis Cache]: /documentation/services/redis-cache/
[App Service Web Apps]: http://go.microsoft.com/fwlink/?LinkId=529714
[웹 앱 가격 책정 페이지]: http://go.microsoft.com/fwlink/?LinkId=511643
[Azure 클라우드 서비스에서 Socket.IO를 사용하여 Node.js 채팅 응용 프로그램 빌드]: ../cloud-services/cloud-services-nodejs-chat-app-socketio.md
[Install and Configure the Azure CLI]: ../cli-install-nodejs.md
[Azure 앱 서비스와 이 서비스가 기존 Azure 서비스에 미치는 영향]: http://go.microsoft.com/fwlink/?LinkId=529714
[Node.js 개발자 센터]: /develop/nodejs/
[App Service 체험]: https://azure.microsoft.com/try/app-service/
[Azure 웹 사이트의 인스턴스 선호도]: https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/
[Azure Redis 캐시에서 캐시 만들기]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md

[socket.io-redis]: https://github.com/socketio/socket.io-redis
[Socket.IO GitHub 리포지토리]: https://github.com/socketio/socket.io
[ZIP 또는 GZ 보관 릴리스]: https://github.com/socketio/socket.io/releases

<!-- IMG List -->

[chat-example-view]: ./media/web-sites-nodejs-chat-app-socketio/socketio-2.png
[npm-output]: ./media/web-sites-nodejs-chat-app-socketio/socketio-7.png
[completed-app]: ./media/web-sites-nodejs-chat-app-socketio/websitesocketcomplete.png
