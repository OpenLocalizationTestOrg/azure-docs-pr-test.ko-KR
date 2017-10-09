### <a name="create-a-nodejs-application"></a>Node.js 응용 프로그램 만들기

`listener.js`라는 새 JavaScript 파일을 만듭니다.

### <a name="add-hello-relay-npm-package"></a>Hello 릴레이 NPM 패키지 추가

프로젝트 폴더에 있는 노드 명령 프롬프트에서 `npm install hyco-ws`를 실행합니다.

### <a name="write-some-code-tooreceive-messages"></a>Tooreceive 메시지 일부 코드를 작성 합니다.

1. Hello 상수 toohello 맨 뒤 hello 추가 `listener.js` 파일입니다.
   
    ```js
    const WebSocket = require('hyco-ws');
    ```
2. 다음 상수 toohello hello 추가 `listener.js` hello 하이브리드 연결 세부 정보에 대 한 파일입니다. Hello 값 hello 하이브리드 연결을 만들 때 대괄호의 hello 자리 표시자를 바꿉니다.
   
   1. `const ns`-hello 릴레이 네임 스페이스입니다. 수 있는지 toouse hello 정규화 된 네임 스페이스 이름입니다. 예를 들어 `{namespace}.servicebus.windows.net`합니다.
   2. `const path`-hello 하이브리드 연결의 hello 이름입니다.
   3. `const keyrule`-hello hello SAS 키 이름입니다.
   4. `const key`-hello SAS 키 값입니다.

3. 다음 코드 toohello hello 추가 `listener.js` 파일:
   
    ```js
    var wss = WebSocket.createRelayedServer(
    {
        server : WebSocket.createRelayListenUri(ns, path),
        token: WebSocket.createRelayToken('http://' + ns, keyrule, key)
    }, 
    function (ws) {
        console.log('connection accepted');
        ws.onmessage = function (event) {
            console.log(event.data);
        };
        ws.on('close', function () {
            console.log('connection closed');
        });       
    });
   
    console.log('listening');
   
    wss.on('error', function(err) {
        console.log('error' + err);
    });
    ```
    listener.js 파일은 다음과 같아야 합니다.
   
    ```js
    const WebSocket = require('hyco-ws');
   
    const ns = "{RelayNamespace}";
    const path = "{HybridConnectionName}";
    const keyrule = "{SASKeyName}";
    const key = "{SASKeyValue}";
   
    var wss = WebSocket.createRelayedServer(
        {
            server : WebSocket.createRelayListenUri(ns, path),
            token: WebSocket.createRelayToken('http://' + ns, keyrule, key)
        }, 
        function (ws) {
            console.log('connection accepted');
            ws.onmessage = function (event) {
                console.log(event.data);
            };
            ws.on('close', function () {
                console.log('connection closed');
            });       
    });
   
    console.log('listening');
   
    wss.on('error', function(err) {
        console.log('error' + err);
    });
    ```

