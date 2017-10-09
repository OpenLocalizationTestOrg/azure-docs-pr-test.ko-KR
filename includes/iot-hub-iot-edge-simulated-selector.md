> [!div class="op_single_selector"]
> * [<span data-ttu-id="15d55-101">Linux</span><span class="sxs-lookup"><span data-stu-id="15d55-101">Linux</span></span>](../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md)
> * [<span data-ttu-id="15d55-102">Windows</span><span class="sxs-lookup"><span data-stu-id="15d55-102">Windows</span></span>](../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md)

<span data-ttu-id="15d55-103">이 연습에서는의 hello [시뮬레이션 된 장치 클라우드 업로드 샘플] 방법을 보여 줍니다 toouse [Azure IoT 가장자리] [ lnk-sdk] 시뮬레이션에서 toosend 장치-클라우드 원격 분석 tooIoT 허브 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="15d55-103">This walkthrough of hello [Simulated Device Cloud Upload sample] shows you how toouse [Azure IoT Edge][lnk-sdk] toosend device-to-cloud telemetry tooIoT Hub from simulated devices.</span></span>

<span data-ttu-id="15d55-104">이 연습에서는 다음 내용을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="15d55-104">This walkthrough covers:</span></span>

* <span data-ttu-id="15d55-105">**아키텍처**: hello에 대 한 아키텍처 정보 [시뮬레이션 된 장치 클라우드 업로드 샘플]합니다.</span><span class="sxs-lookup"><span data-stu-id="15d55-105">**Architecture**: architectural information about hello [Simulated Device Cloud Upload sample].</span></span>
* <span data-ttu-id="15d55-106">**빌드 및 실행**: hello 단계 필요한 toobuild 및 실행된 hello 샘플.</span><span class="sxs-lookup"><span data-stu-id="15d55-106">**Build and run**: hello steps required toobuild and run hello sample.</span></span>

## <a name="architecture"></a><span data-ttu-id="15d55-107">아키텍처</span><span class="sxs-lookup"><span data-stu-id="15d55-107">Architecture</span></span>

<span data-ttu-id="15d55-108">hello [시뮬레이션 된 장치 클라우드 업로드 샘플] toocreate에서 원격 분석을 전송 하는 게이트웨이 장치 tooan IoT 허브를 시뮬레이션 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="15d55-108">hello [Simulated Device Cloud Upload sample] shows how toocreate a gateway that sends telemetry from simulated devices tooan IoT hub.</span></span> <span data-ttu-id="15d55-109">장치 수 tooconnect 아닐 tooIoT 허브 직접 때문에 hello 장치:</span><span class="sxs-lookup"><span data-stu-id="15d55-109">A device may not be able tooconnect directly tooIoT Hub because hello device:</span></span>

* <span data-ttu-id="15d55-110">IoT Hub가 이해하는 통신 프로토콜을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15d55-110">Does not use a communications protocol understood by IoT Hub.</span></span>
* <span data-ttu-id="15d55-111">IoT Hub에서 정도로 스마트 tooremember hello 할당 identity tooit이 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15d55-111">Is not smart enough tooremember hello identity assigned tooit by IoT Hub.</span></span>

<span data-ttu-id="15d55-112">IoT 지 게이트웨이 hello 같은 방법으로 다음에서 이러한 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d55-112">An IoT Edge gateway can solve these problems in hello following ways:</span></span>

* <span data-ttu-id="15d55-113">hello 게이트웨이 hello 장치에서 사용 하는 hello 프로토콜에 대 한 이해, hello 장치에서 장치-클라우드 원격 분석을 수신 및 이러한 메시지 tooIoT hello IoT 허브에서 인식 하는 프로토콜을 사용 하 여 허브를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d55-113">hello gateway understands hello protocol used by hello device, receives device-to-cloud telemetry from hello device, and forwards those messages tooIoT Hub using a protocol understood by hello IoT hub.</span></span>

* <span data-ttu-id="15d55-114">hello 게이트웨이 IoT Hub identities toodevices 매핑하고 프록시 역할을 하는 장치를 보내면 메시지 tooIoT 허브 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d55-114">hello gateway maps IoT Hub identities toodevices and acts as a proxy when a device sends messages tooIoT Hub.</span></span>

<span data-ttu-id="15d55-115">다음 다이어그램 hello hello hello 샘플의 주 구성 요소, IoT 가장자리 모듈 hello 포함 하 여 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="15d55-115">hello following diagram shows hello main components of hello sample, including hello IoT Edge modules:</span></span>

![][1]

<span data-ttu-id="15d55-116">hello 모듈 메시지를 전달 하지 않는 직접 tooeach 다른 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d55-116">hello modules do not pass messages directly tooeach other.</span></span> <span data-ttu-id="15d55-117">hello 모듈 hello 메시지 toohello 구독 메커니즘을 사용 하 여 다른 모듈을 제공 하는 메시지 tooan 내부 브로커를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d55-117">hello modules publish messages tooan internal broker that delivers hello messages toohello other modules using a subscription mechanism.</span></span> <span data-ttu-id="15d55-118">자세한 내용은 [Azure IoT Edge 시작][lnk-gw-getstarted]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15d55-118">For more information, see [Get started with Azure IoT Edge][lnk-gw-getstarted].</span></span>

### <a name="protocol-ingestion-module"></a><span data-ttu-id="15d55-119">프로토콜 수집 모듈</span><span class="sxs-lookup"><span data-stu-id="15d55-119">Protocol ingestion module</span></span>

<span data-ttu-id="15d55-120">이 모듈은 hello hello 게이트웨이 통해 및 hello 클라우드로 장치에서 데이터 받기 위한 기준으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d55-120">This module is hello starting point for receiving data from devices, through hello gateway, and into hello cloud.</span></span> <span data-ttu-id="15d55-121">Hello 샘플에서는 hello 모듈:</span><span class="sxs-lookup"><span data-stu-id="15d55-121">In hello sample, hello module:</span></span>

1. <span data-ttu-id="15d55-122">시뮬레이션된 온도 데이터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="15d55-122">Creates simulated temperature data.</span></span> <span data-ttu-id="15d55-123">물리적 장치를 사용 하는 경우 hello 모듈 실제 장치에서 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="15d55-123">If you use physical devices, hello module reads data from those physical devices.</span></span>
1. <span data-ttu-id="15d55-124">메시지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="15d55-124">Creates a message.</span></span>
1. <span data-ttu-id="15d55-125">시뮬레이션 된 hello 온도 데이터 hello 메시지 내용을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="15d55-125">Places hello simulated temperature data into hello message content.</span></span>
1. <span data-ttu-id="15d55-126">가짜 MAC 주소 toohello 메시지를 사용 하 여 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="15d55-126">Adds a property with a fake MAC address toohello message.</span></span>
1. <span data-ttu-id="15d55-127">Hello 체인의 다음 모듈로를 사용할 수 있는 toohello hello 메시지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="15d55-127">Makes hello message available toohello next module in hello chain.</span></span>

<span data-ttu-id="15d55-128">호출 하는 hello 모듈 **프로토콜 X 수집** hello 이전 다이어그램 라고 **시뮬레이션 된 장치** hello 소스 코드에서.</span><span class="sxs-lookup"><span data-stu-id="15d55-128">hello module called **Protocol X ingestion** in hello previous diagram is called **Simulated device** in hello source code.</span></span>

### <a name="mac-lt-gt-iot-hub-id-module"></a><span data-ttu-id="15d55-129">MAC &lt;-&gt; IoT Hub ID 모듈</span><span class="sxs-lookup"><span data-stu-id="15d55-129">MAC &lt;-&gt; IoT Hub ID module</span></span>

<span data-ttu-id="15d55-130">이 모듈은 Mac 주소 속성이 있는 메시지를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="15d55-130">This module scans for messages that have a Mac address property.</span></span> <span data-ttu-id="15d55-131">Hello 샘플 hello 프로토콜 수집 모듈 hello MAC 주소 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="15d55-131">In hello sample, hello protocol ingestion module adds hello MAC address property.</span></span> <span data-ttu-id="15d55-132">Hello 모듈은 이러한 속성을 찾는 경우 IoT Hub 장치 키 toohello 메시지와 함께 다른 속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d55-132">If hello module finds such a property, it adds another property with an IoT Hub device key toohello message.</span></span> <span data-ttu-id="15d55-133">hello 모듈 hello 체인의 다음 모듈로 사용할 수 있는 toohello hello 메시지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="15d55-133">hello module then makes hello message available toohello next module in hello chain.</span></span>

<span data-ttu-id="15d55-134">hello 개발자 MAC 주소와 IoT Hub 장치 id 사용 하 여 IoT Hub identities tooassociate hello 시뮬레이션 된 장치 간의 매핑을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="15d55-134">hello developer sets up a mapping between MAC addresses and IoT Hub identities tooassociate hello simulated devices with IoT Hub device identities.</span></span> <span data-ttu-id="15d55-135">hello 개발자 hello 모듈 구성의 일부분으로 hello 매핑을 수동으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="15d55-135">hello developer adds hello mapping manually as part of hello module configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="15d55-136">이 샘플은 MAC 주소를 유일한 장치 식별자로 사용하고, 이것을 IoT Hub 장치 ID와 상호 연결시킵니다.</span><span class="sxs-lookup"><span data-stu-id="15d55-136">This sample uses a MAC address as a unique device identifier and correlates it with an IoT Hub device identity.</span></span> <span data-ttu-id="15d55-137">하지만, 다른 고유 식별자를 사용하는 자신만의 모듈을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d55-137">However, you can write your own module that uses a different unique identifier.</span></span> <span data-ttu-id="15d55-138">예를 들어 장치에는 고유한 일련 번호 있을 수 있습니다 또는 hello 원격 분석 데이터는 포함 된 고유한 장치 이름에 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d55-138">For example, your devices may have unique serial numbers or hello telemetry data may include a unique embedded device name.</span></span>

### <a name="iot-hub-communication-module"></a><span data-ttu-id="15d55-139">IoT Hub 통신 모듈</span><span class="sxs-lookup"><span data-stu-id="15d55-139">IoT Hub communication module</span></span>

<span data-ttu-id="15d55-140">이 모듈에서는 IoT 허브를 사용 하 여 메시지 hello 이전 모듈에 의해 할당 된 장치 키 속성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d55-140">This module takes messages with an IoT Hub device key property that was assigned by hello previous module.</span></span> <span data-ttu-id="15d55-141">hello 모듈 HTTP 프로토콜 hello 콘텐츠 tooIoT 허브를 사용 하 여 hello 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="15d55-141">hello module sends hello message content tooIoT Hub using hello HTTP protocol.</span></span> <span data-ttu-id="15d55-142">HTTP은 IoT Hub에서 hello 이해 하는 세 가지 프로토콜 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="15d55-142">HTTP is one of hello three protocols understood by IoT Hub.</span></span>

<span data-ttu-id="15d55-143">각 시뮬레이션 된 장치에 대 한 연결을 여는 대신이 모듈 hello 게이트웨이 toohello IoT 허브에서 단일 HTTP 연결을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="15d55-143">Instead of opening a connection for each simulated device, this module opens a single HTTP connection from hello gateway toohello IoT hub.</span></span> <span data-ttu-id="15d55-144">hello 모듈은 다음 해당 연결을 통해 모든 hello 시뮬레이션 된 장치에서의 연결 멀티플렉싱 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d55-144">hello module then multiplexes connections from all hello simulated devices over that connection.</span></span> <span data-ttu-id="15d55-145">이 방법을 단일 게이트웨이 tooconnect 많은 더 많은 장치를 사용 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15d55-145">This approach enables a single gateway tooconnect many more devices.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="15d55-146">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="15d55-146">Before you get started</span></span>

<span data-ttu-id="15d55-147">시작하기 전에 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d55-147">Before you get started, you must:</span></span>

* <span data-ttu-id="15d55-148">[IoT 허브를 만듭니다.] [ lnk-create-hub] Azure 구독에 필요한 허브 toocomplete의 hello 이름을이 연습 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d55-148">[Create an IoT hub][lnk-create-hub] in your Azure subscription, you need hello name of your hub toocomplete this walkthrough.</span></span> <span data-ttu-id="15d55-149">계정이 없는 경우 몇 분 내에 [무료 계정][lnk-free-trial]을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d55-149">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="15d55-150">두 장치 tooyour IoT 허브를 추가 하 고 해당 id와 장치 키를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d55-150">Add two devices tooyour IoT hub and make a note of their ids and device keys.</span></span> <span data-ttu-id="15d55-151">Hello를 사용할 수 있습니다 [장치 탐색기] [ lnk-device-explorer] 또는 [iothub 탐색기] [ lnk-iothub-explorer] tooadd hello에서 만든 장치 toohello IoT 허브 도구 이전 단계 및 해당 키를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d55-151">You can use hello [device explorer][lnk-device-explorer] or [iothub-explorer][lnk-iothub-explorer] tool tooadd your devices toohello IoT hub you created in hello previous step and retrieve their keys.</span></span>

![][2]

<!-- Images -->
[1]: media/iot-hub-iot-edge-simulated-selector/image1.png
[2]: media/iot-hub-iot-edge-simulated-selector/image2.png

<!-- Links -->
[시뮬레이션 된 장치 클라우드 업로드 샘플]: https://github.com/Azure/iot-edge/blob/master/samples/simulated_device_cloud_upload/README.md
[lnk-sdk]: https://github.com/Azure/iot-edge
[lnk-gw-getstarted]: ../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md
[lnk-create-hub]: ../articles/iot-hub/iot-hub-create-through-portal.md