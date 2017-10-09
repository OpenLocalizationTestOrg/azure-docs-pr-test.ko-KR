## <a name="configure-hello-nodejs-simulated-device"></a><span data-ttu-id="76189-101">Hello Node.js 시뮬레이션 된 장치를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="76189-101">Configure hello Node.js simulated device</span></span>
1. <span data-ttu-id="76189-102">Hello 원격 모니터링 대시보드에서 **장치 추가 +** 다음 추가 *사용자 지정 장치*합니다.</span><span class="sxs-lookup"><span data-stu-id="76189-102">On hello remote monitoring dashboard, click **+ Add a device** and then add a *custom device*.</span></span> <span data-ttu-id="76189-103">호스트 이름, 장치 id 및 장치 키 hello IoT Hub를 메모를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="76189-103">Make a note of hello IoT Hub hostname, device id, and device key.</span></span> <span data-ttu-id="76189-104">원하는이 자습서의 뒷부분에 나오는 hello remote_monitoring.js 장치 클라이언트 응용 프로그램을 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="76189-104">You need them later in this tutorial when you prepare hello remote_monitoring.js device client application.</span></span>
2. <span data-ttu-id="76189-105">Node.js 버전 0.12.x 이상이 개발 컴퓨터에 설치되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="76189-105">Ensure that Node.js version 0.12.x or later is installed on your development machine.</span></span> <span data-ttu-id="76189-106">실행 `node --version` 명령 프롬프트 또는 셸 toocheck hello 버전에서입니다.</span><span class="sxs-lookup"><span data-stu-id="76189-106">Run `node --version` at a command prompt or in a shell toocheck hello version.</span></span> <span data-ttu-id="76189-107">Linux에서 패키지 관리자 tooinstall Node.js를 사용 하는 방법에 대 한 정보를 참조 하십시오. [패키지 관리자를 통해 Node.js 설치][node-linux]합니다.</span><span class="sxs-lookup"><span data-stu-id="76189-107">For information about using a package manager tooinstall Node.js on Linux, see [Installing Node.js via package manager][node-linux].</span></span>
3. <span data-ttu-id="76189-108">Node.js를 설치한 경우 복제 hello 최신 버전의 hello [azure iot-sdk 노드] [ lnk-github-repo] 리포지토리 tooyour 개발 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="76189-108">When you have installed Node.js, clone hello latest version of hello [azure-iot-sdk-node][lnk-github-repo] repository tooyour development machine.</span></span> <span data-ttu-id="76189-109">항상 hello를 사용 하 여 **마스터** hello 최신 버전의 hello 라이브러리 및 샘플에 대 한 분기입니다.</span><span class="sxs-lookup"><span data-stu-id="76189-109">Always use hello **master** branch for hello latest version of hello libraries and samples.</span></span>
4. <span data-ttu-id="76189-110">Hello의 로컬 복사본에서 [azure iot-sdk 노드] [ lnk-github-repo] 저장소, hello 노드/장치/samples 폴더 tooan 빈 폴더에서 두 개의 파일에 나오는 개발 컴퓨터에 복사 hello:</span><span class="sxs-lookup"><span data-stu-id="76189-110">From your local copy of hello [azure-iot-sdk-node][lnk-github-repo] repository, copy hello following two files from hello node/device/samples folder tooan empty folder on your development machine:</span></span>
   
   * <span data-ttu-id="76189-111">packages.json</span><span class="sxs-lookup"><span data-stu-id="76189-111">packages.json</span></span>
   * <span data-ttu-id="76189-112">remote_monitoring.js</span><span class="sxs-lookup"><span data-stu-id="76189-112">remote_monitoring.js</span></span>
5. <span data-ttu-id="76189-113">Hello remote_monitoring.js 파일을 열고 변수 정의 뒤 hello를 찾아보십시오.</span><span class="sxs-lookup"><span data-stu-id="76189-113">Open hello remote_monitoring.js file and look for hello following variable definition:</span></span>
   
    ```
    var connectionString = "[IoT Hub device connection string]";
    ```
6. <span data-ttu-id="76189-114">**[IoT Hub device connection string]** 을 장치 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="76189-114">Replace **[IoT Hub device connection string]** with your device connection string.</span></span> <span data-ttu-id="76189-115">IoT Hub 호스트 이름, 장치 id 및 메모 1 단계에서 만든 장치 키에 대 한 hello 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="76189-115">Use hello values for your IoT Hub hostname, device id, and device key that you made a note of in step 1.</span></span> <span data-ttu-id="76189-116">장치 연결 문자열에 형식에 따라 hello:</span><span class="sxs-lookup"><span data-stu-id="76189-116">A device connection string has hello following format:</span></span>
   
    ```
    HostName={your IoT Hub hostname};DeviceId={your device id};SharedAccessKey={your device key}
    ```
   
    <span data-ttu-id="76189-117">IoT Hub 호스트 이름이 경우 **contoso** 장치 id는 **mydevice**, 연결 문자열에 다음 코드 조각 hello 같습니다.</span><span class="sxs-lookup"><span data-stu-id="76189-117">If your IoT Hub hostname is **contoso** and your device id is **mydevice**, your connection string looks like hello following snippet:</span></span>
   
    ```
    var connectionString = "HostName=contoso.azure-devices.net;DeviceId=mydevice;SharedAccessKey=2s ... =="
    ```
7. Hello 파일을 저장 합니다. <span data-ttu-id="76189-119">Hello 명령 셸 또는 이러한 파일 tooinstall hello 필요한 패키지를 포함 하는 hello 폴더에서 명령 프롬프트에서 다음을 실행 하 고 hello 샘플 응용 프로그램을 실행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="76189-119">Run hello following commands in a shell or command prompt in hello folder that contains these files tooinstall hello necessary packages and then run hello sample application:</span></span>
   
    ```
    npm install
    node remote_monitoring.js
    ```

## <a name="observe-dynamic-telemetry-in-action"></a><span data-ttu-id="76189-120">작업 중인 동적 원격 분석 관찰</span><span class="sxs-lookup"><span data-stu-id="76189-120">Observe dynamic telemetry in action</span></span>
<span data-ttu-id="76189-121">hello 대시보드 hello 기존 시뮬레이션 된 장치에서 hello 온도 및 습도 원격 분석을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="76189-121">hello dashboard shows hello temperature and humidity telemetry from hello existing simulated devices:</span></span>

![hello 기본 대시보드][image1]

<span data-ttu-id="76189-123">Hello 이전 섹션에서 실행 된 hello Node.js 시뮬레이션 된 장치 수를 선택 하면 온도, 습도, 및 외부 온도 원격 분석 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76189-123">If you select hello Node.js simulated device you ran in hello previous section, you see temperature, humidity, and external temperature telemetry:</span></span>

![외부 온도 toohello 대시보드를 추가 합니다.][image2]

<span data-ttu-id="76189-125">자동으로 hello 원격 모니터링 솔루션 hello 추가 외부 온도 원격 분석 유형을 검색 하 고 hello 대시보드에서 toohello 차트 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="76189-125">hello remote monitoring solution automatically detects hello additional external temperature telemetry type and adds it toohello chart on hello dashboard.</span></span>

[node-linux]: https://github.com/nodejs/node-v0.x-archive/wiki/Installing-Node.js-via-package-manager
[lnk-github-repo]: https://github.com/Azure/azure-iot-sdk-node
[image1]: media/iot-suite-send-external-temperature/image1.png
[image2]: media/iot-suite-send-external-temperature/image2.png