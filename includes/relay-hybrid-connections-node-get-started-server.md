### <a name="create-a-nodejs-application"></a><span data-ttu-id="ce670-101">Node.js 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="ce670-101">Create a Node.js application</span></span>

<span data-ttu-id="ce670-102">`listener.js`라는 새 JavaScript 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ce670-102">Create a new JavaScript file called `listener.js`.</span></span>

### <a name="add-hello-relay-npm-package"></a><span data-ttu-id="ce670-103">Hello 릴레이 NPM 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="ce670-103">Add hello Relay NPM package</span></span>

<span data-ttu-id="ce670-104">프로젝트 폴더에 있는 노드 명령 프롬프트에서 `npm install hyco-ws`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ce670-104">Run `npm install hyco-ws` from a Node command prompt in your project folder.</span></span>

### <a name="write-some-code-tooreceive-messages"></a><span data-ttu-id="ce670-105">Tooreceive 메시지 일부 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce670-105">Write some code tooreceive messages</span></span>

1. <span data-ttu-id="ce670-106">Hello 상수 toohello 맨 뒤 hello 추가 `listener.js` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ce670-106">Add hello following constant toohello top of hello `listener.js` file.</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    ```
2. <span data-ttu-id="ce670-107">다음 상수 toohello hello 추가 `listener.js` hello 하이브리드 연결 세부 정보에 대 한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ce670-107">Add hello following constants toohello `listener.js` file for hello hybrid connection details.</span></span> <span data-ttu-id="ce670-108">Hello 값 hello 하이브리드 연결을 만들 때 대괄호의 hello 자리 표시자를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ce670-108">Replace hello placeholders in brackets with hello values you obtained when you created hello hybrid connection.</span></span>
   
   1. <span data-ttu-id="ce670-109">`const ns`-hello 릴레이 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="ce670-109">`const ns` - hello Relay namespace.</span></span> <span data-ttu-id="ce670-110">수 있는지 toouse hello 정규화 된 네임 스페이스 이름입니다. 예를 들어 `{namespace}.servicebus.windows.net`합니다.</span><span class="sxs-lookup"><span data-stu-id="ce670-110">Be sure toouse hello fully qualified namespace name; for example, `{namespace}.servicebus.windows.net`.</span></span>
   2. <span data-ttu-id="ce670-111">`const path`-hello 하이브리드 연결의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ce670-111">`const path` - hello name of hello hybrid connection.</span></span>
   3. <span data-ttu-id="ce670-112">`const keyrule`-hello hello SAS 키 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ce670-112">`const keyrule` - hello name of hello SAS key.</span></span>
   4. <span data-ttu-id="ce670-113">`const key`-hello SAS 키 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ce670-113">`const key` - hello SAS key value.</span></span>

3. <span data-ttu-id="ce670-114">다음 코드 toohello hello 추가 `listener.js` 파일:</span><span class="sxs-lookup"><span data-stu-id="ce670-114">Add hello following code toohello `listener.js` file:</span></span>
   
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
    <span data-ttu-id="ce670-115">listener.js 파일은 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce670-115">Here is what your listener.js file should look like:</span></span>
   
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

