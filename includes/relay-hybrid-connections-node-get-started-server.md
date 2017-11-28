### <a name="create-a-nodejs-application"></a><span data-ttu-id="53644-101">Node.js 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="53644-101">Create a Node.js application</span></span>

<span data-ttu-id="53644-102">`listener.js`라는 새 JavaScript 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="53644-102">Create a new JavaScript file called `listener.js`.</span></span>

### <a name="add-the-relay-npm-package"></a><span data-ttu-id="53644-103">릴레이 NPM 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="53644-103">Add the Relay NPM package</span></span>

<span data-ttu-id="53644-104">프로젝트 폴더에 있는 노드 명령 프롬프트에서 `npm install hyco-ws`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="53644-104">Run `npm install hyco-ws` from a Node command prompt in your project folder.</span></span>

### <a name="write-some-code-to-receive-messages"></a><span data-ttu-id="53644-105">메시지를 수신하는 코드 작성</span><span class="sxs-lookup"><span data-stu-id="53644-105">Write some code to receive messages</span></span>

1. <span data-ttu-id="53644-106">다음 상수를 `listener.js` 파일의 맨 위에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="53644-106">Add the following constant to the top of the `listener.js` file.</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    ```
2. <span data-ttu-id="53644-107">다음 상수를 하이브리드 연결 정보에 대한 `listener.js` 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="53644-107">Add the following constants to the `listener.js` file for the hybrid connection details.</span></span> <span data-ttu-id="53644-108">대괄호 안의 자리 표시자를 하이브리드 연결을 만들 때 얻은 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="53644-108">Replace the placeholders in brackets with the values you obtained when you created the hybrid connection.</span></span>
   
   1. <span data-ttu-id="53644-109">`const ns` - 릴레이 네임스페이스</span><span class="sxs-lookup"><span data-stu-id="53644-109">`const ns` - The Relay namespace.</span></span> <span data-ttu-id="53644-110">정규화된 네임스페이스 이름을 사용해야 합니다. 예: `{namespace}.servicebus.windows.net`</span><span class="sxs-lookup"><span data-stu-id="53644-110">Be sure to use the fully qualified namespace name; for example, `{namespace}.servicebus.windows.net`.</span></span>
   2. <span data-ttu-id="53644-111">`const path` - 하이브리드 연결의 이름</span><span class="sxs-lookup"><span data-stu-id="53644-111">`const path` - The name of the hybrid connection.</span></span>
   3. <span data-ttu-id="53644-112">`const keyrule` - SAS 키의 이름</span><span class="sxs-lookup"><span data-stu-id="53644-112">`const keyrule` - The name of the SAS key.</span></span>
   4. <span data-ttu-id="53644-113">`const key` - SAS 키 값</span><span class="sxs-lookup"><span data-stu-id="53644-113">`const key` - The SAS key value.</span></span>

3. <span data-ttu-id="53644-114">`listener.js` 파일에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="53644-114">Add the following code to the `listener.js` file:</span></span>
   
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
    <span data-ttu-id="53644-115">listener.js 파일은 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53644-115">Here is what your listener.js file should look like:</span></span>
   
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

