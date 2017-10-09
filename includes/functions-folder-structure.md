
<span data-ttu-id="f84c5-101">호스트 구성 파일 및 hello 다음 예제와 같이 별도 함수에 대 한 hello 코드를 포함 하는 각각 하나 이상의 하위 폴더를 포함 하는 루트 폴더에 거주 하 고 hello에 모든 함수가 지정된 함수 응용 프로그램에 대 한 hello 코드:</span><span class="sxs-lookup"><span data-stu-id="f84c5-101">hello code for all of hello functions in a given function app lives in a root folder that contains a host configuration file and one or more subfolders, each of which contain hello code for a separate function, as in hello following example:</span></span>

```
wwwroot
 | - host.json
 | - mynodefunction
 | | - function.json
 | | - index.js
 | | - node_modules
 | | | - ... packages ...
 | | - package.json
 | - mycsharpfunction
 | | - function.json
 | | - run.csx
```

<span data-ttu-id="f84c5-102">hello *host.json* 파일 일부 런타임 관련 구성을 포함 하 고 hello 함수 앱의 hello 루트 폴더에 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f84c5-102">hello *host.json* file contains some runtime-specific configuration and sits in hello root folder of hello function app.</span></span> <span data-ttu-id="f84c5-103">사용할 수 있는 설정에 대 한 자세한 내용은 참조 [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) hello WebJobs.Script 리포지토리 wiki에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f84c5-103">For information on settings that are available, see [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) in hello WebJobs.Script repository wiki.</span></span>

<span data-ttu-id="f84c5-104">각 함수는 하나 이상의 코드 파일, hello function.json 구성 및 기타 종속성을 포함 하는 폴더를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f84c5-104">Each function has a folder that contains one or more code files, hello function.json configuration and other dependencies.</span></span>

