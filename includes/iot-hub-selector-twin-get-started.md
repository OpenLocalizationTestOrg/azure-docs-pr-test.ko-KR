> [!div class="op_single_selector"]
> * [<span data-ttu-id="2a005-101">Node.JS</span><span class="sxs-lookup"><span data-stu-id="2a005-101">Node.js</span></span>](../articles/iot-hub/iot-hub-node-node-twin-getstarted.md)
> * [<span data-ttu-id="2a005-102">C#/Node.js</span><span class="sxs-lookup"><span data-stu-id="2a005-102">C#/Node.js</span></span>](../articles/iot-hub/iot-hub-csharp-node-twin-getstarted.md)
> * [<span data-ttu-id="2a005-103">C#</span><span class="sxs-lookup"><span data-stu-id="2a005-103">C#</span></span>](../articles/iot-hub/iot-hub-csharp-csharp-twin-getstarted.md)
> * [<span data-ttu-id="2a005-104">Java</span><span class="sxs-lookup"><span data-stu-id="2a005-104">Java</span></span>](../articles/iot-hub/iot-hub-java-java-twin-getstarted.md)

<span data-ttu-id="2a005-105">장치 쌍은 장치의 상태 정보(메타데이터, 상태 및 조건)를 저장하는 JSON 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="2a005-105">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="2a005-106">IoT Hub tooit 연결 하는 각 장치에 대 한 장치로 이중을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a005-106">IoT Hub persists a device twin for each device that connects tooit.</span></span>

<span data-ttu-id="2a005-107">장치 쌍의 용도:</span><span class="sxs-lookup"><span data-stu-id="2a005-107">Use device twins to:</span></span>

* <span data-ttu-id="2a005-108">솔루션 백 엔드의 장치 메타데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2a005-108">Store device metadata from your solution back end.</span></span>
* <span data-ttu-id="2a005-109">장치 앱에서 사용할 수 있는 기능 및 조건 (예를 들어 hello 연결 방법 사용)와 같은 현재 상태 정보를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a005-109">Report current state information such as available capabilities and conditions (for example, hello connectivity method used) from your device app.</span></span>
* <span data-ttu-id="2a005-110">장치 앱과 백 엔드 응용 프로그램 간에 장기 실행 워크플로 (예: 펌웨어 및 구성 업데이트)의 hello 상태를 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a005-110">Synchronize hello state of long-running workflows (such as firmware and configuration updates) between a device app and a back-end app.</span></span>
* <span data-ttu-id="2a005-111">장치 메타데이터, 구성 또는 상태를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="2a005-111">Query your device metadata, configuration, or state.</span></span>

> [!NOTE]
> <span data-ttu-id="2a005-112">장치 쌍은 장치 구성 및 상태를 동기화하고 쿼리하기 위해 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2a005-112">Device twins are designed for synchronization and for querying device configurations and conditions.</span></span> <span data-ttu-id="2a005-113">Toouse 장치 트윈스에서 확인할 수 있습니다 시기에 대 한 자세한 내용은 [장치 트윈스 이해][lnk-twins]합니다.</span><span class="sxs-lookup"><span data-stu-id="2a005-113">More informations on when toouse device twins can be found in [Understand device twins][lnk-twins].</span></span>

<span data-ttu-id="2a005-114">장치 쌍은 IoT hub에 저장되고 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2a005-114">Device twins are stored in an IoT hub and contain:</span></span>

* <span data-ttu-id="2a005-115">*태그*, hello 솔루션 백 엔드;만 액세스할 수 있게 장치 메타 데이터</span><span class="sxs-lookup"><span data-stu-id="2a005-115">*tags*, device metadata accessible only by hello solution back end;</span></span>
* <span data-ttu-id="2a005-116">*원하는 속성을*, hello 솔루션에서 수정할 수 있는 JSON 개체 hello 장치 응용 프로그램에서 종료 되 고 관찰 가능 개체를 다시 및</span><span class="sxs-lookup"><span data-stu-id="2a005-116">*desired properties*, JSON objects modifiable by hello solution back end and observable by hello device app; and</span></span>
* <span data-ttu-id="2a005-117">*속성을 보고*, hello 장치 응용 프로그램에서 수정할 수 있는 인수와 hello 솔루션 백 엔드에서 읽을 수 있는 JSON 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="2a005-117">*reported properties*, JSON objects modifiable by hello device app and readable by hello solution back end.</span></span> <span data-ttu-id="2a005-118">태그 및 속성은 배열을 포함할 수 없지만, 개체는 중첩될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a005-118">Tags and properties cannot contain arrays, but objects can be nested.</span></span>

![][img-twin]

<span data-ttu-id="2a005-119">또한 hello 솔루션 백 엔드 데이터 위에 모든 hello에 따라 장치 트윈스 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a005-119">Additionally, hello solution back end can query device twins based on all hello above data.</span></span>
<span data-ttu-id="2a005-120">너무 참조[장치 트윈스 이해] [ lnk-twins] 장치 트윈스 및 toohello에 대 한 자세한 내용은 [IoT Hub 쿼리 언어] [ lnk-query] 참조 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a005-120">Refer too[Understand device twins][lnk-twins] for more information about device twins, and toohello [IoT Hub query language][lnk-query] reference for querying.</span></span>

> [!NOTE]
> <span data-ttu-id="2a005-121">이때 장치 트윈스는 tooIoT 허브를 연결 하는 장치 에서만에서 액세스할 수 hello MQTT 프로토콜을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a005-121">At this time, device twins are accessible only from devices that connect tooIoT Hub using hello MQTT protocol.</span></span> <span data-ttu-id="2a005-122">Toohello를 참조 하십시오 [MQTT 지원] [ lnk-devguide-mqtt] 방법에 대 한 문서 tooconvert 기존 장치 앱 toouse MQTT 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a005-122">Please refer toohello [MQTT support][lnk-devguide-mqtt] article for instructions on how tooconvert existing device app toouse MQTT.</span></span>

<span data-ttu-id="2a005-123">이 자습서에서는 다음을 수행하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2a005-123">This tutorial shows you how to:</span></span>

* <span data-ttu-id="2a005-124">추가 하는 백 엔드 앱 만들기 *태그* tooa 장치로 이중 및 연결을 보고 하는 시뮬레이션 된 장치 응용 프로그램으로 채널을 *속성을 보고* hello 장치로 이중에 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a005-124">Create a back-end app that adds *tags* tooa device twin, and a simulated device app that reports its connectivity channel as a *reported property* on hello device twin.</span></span>
* <span data-ttu-id="2a005-125">Hello 태그 및 이전에 만든 속성에 필터를 사용 하 여 백 엔드 앱에서 장치를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a005-125">Query devices from your back-end app using filters on hello tags and properties previously created.</span></span>

<!-- images -->
[img-twin]: media/iot-hub-selector-twin-get-started/twin.png

<!-- links -->
[lnk-query]: ../articles/iot-hub/iot-hub-devguide-query-language.md
[lnk-twins]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-d2c]: ../articles/iot-hub/iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md