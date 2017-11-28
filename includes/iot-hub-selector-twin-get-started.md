> [!div class="op_single_selector"]
> * [<span data-ttu-id="ee8eb-101">Node.JS</span><span class="sxs-lookup"><span data-stu-id="ee8eb-101">Node.js</span></span>](../articles/iot-hub/iot-hub-node-node-twin-getstarted.md)
> * [<span data-ttu-id="ee8eb-102">C#/Node.js</span><span class="sxs-lookup"><span data-stu-id="ee8eb-102">C#/Node.js</span></span>](../articles/iot-hub/iot-hub-csharp-node-twin-getstarted.md)
> * [<span data-ttu-id="ee8eb-103">C#</span><span class="sxs-lookup"><span data-stu-id="ee8eb-103">C#</span></span>](../articles/iot-hub/iot-hub-csharp-csharp-twin-getstarted.md)
> * [<span data-ttu-id="ee8eb-104">Java</span><span class="sxs-lookup"><span data-stu-id="ee8eb-104">Java</span></span>](../articles/iot-hub/iot-hub-java-java-twin-getstarted.md)

<span data-ttu-id="ee8eb-105">장치 쌍은 장치의 상태 정보(메타데이터, 상태 및 조건)를 저장하는 JSON 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="ee8eb-105">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="ee8eb-106">IoT Hub는 여기에 연결하는 각 장치에 대해 하나의 장치 쌍을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="ee8eb-106">IoT Hub persists a device twin for each device that connects to it.</span></span>

<span data-ttu-id="ee8eb-107">장치 쌍의 용도:</span><span class="sxs-lookup"><span data-stu-id="ee8eb-107">Use device twins to:</span></span>

* <span data-ttu-id="ee8eb-108">솔루션 백 엔드의 장치 메타데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ee8eb-108">Store device metadata from your solution back end.</span></span>
* <span data-ttu-id="ee8eb-109">장치 앱의 사용 가능한 기능 및 상태(예: 사용된 연결 방법)와 같은 현재 상태 정보를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="ee8eb-109">Report current state information such as available capabilities and conditions (for example, the connectivity method used) from your device app.</span></span>
* <span data-ttu-id="ee8eb-110">장치 앱과 백 엔드 앱 간에 장기 실행 워크플로(예: 펌웨어 및 구성 업데이트)의 상태를 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="ee8eb-110">Synchronize the state of long-running workflows (such as firmware and configuration updates) between a device app and a back-end app.</span></span>
* <span data-ttu-id="ee8eb-111">장치 메타데이터, 구성 또는 상태를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="ee8eb-111">Query your device metadata, configuration, or state.</span></span>

> [!NOTE]
> <span data-ttu-id="ee8eb-112">장치 쌍은 장치 구성 및 상태를 동기화하고 쿼리하기 위해 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ee8eb-112">Device twins are designed for synchronization and for querying device configurations and conditions.</span></span> <span data-ttu-id="ee8eb-113">장치 쌍을 사용하는 경우 자세한 내용은 [장치 쌍 이해][lnk-twins]에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee8eb-113">More informations on when to use device twins can be found in [Understand device twins][lnk-twins].</span></span>

<span data-ttu-id="ee8eb-114">장치 쌍은 IoT hub에 저장되고 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ee8eb-114">Device twins are stored in an IoT hub and contain:</span></span>

* <span data-ttu-id="ee8eb-115">*태그*, 솔루션 백 엔드만 액세스할 수 있는 장치 메타데이터.</span><span class="sxs-lookup"><span data-stu-id="ee8eb-115">*tags*, device metadata accessible only by the solution back end;</span></span>
* <span data-ttu-id="ee8eb-116">*desired 속성*, 솔루션 백 엔드에서 수정할 수 있고 장치 앱에서 관찰할 수 있는 JSON 개체.</span><span class="sxs-lookup"><span data-stu-id="ee8eb-116">*desired properties*, JSON objects modifiable by the solution back end and observable by the device app; and</span></span>
* <span data-ttu-id="ee8eb-117">*reported 속성*, 장치 앱에서 수정할 수 있고 솔루션 백 엔드에서 읽을 수 있는 JSON 개체.</span><span class="sxs-lookup"><span data-stu-id="ee8eb-117">*reported properties*, JSON objects modifiable by the device app and readable by the solution back end.</span></span> <span data-ttu-id="ee8eb-118">태그 및 속성은 배열을 포함할 수 없지만, 개체는 중첩될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee8eb-118">Tags and properties cannot contain arrays, but objects can be nested.</span></span>

![][img-twin]

<span data-ttu-id="ee8eb-119">또한 솔루션 백 엔드는 위의 모든 데이터를 기반으로 하는 장치 쌍을 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee8eb-119">Additionally, the solution back end can query device twins based on all the above data.</span></span>
<span data-ttu-id="ee8eb-120">장치 쌍에 대한 자세한 내용은 [쌍 장치 이해][lnk-twins]를 참조하고 쿼리는 [IoT Hub 쿼리 언어][lnk-query] 참조를 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="ee8eb-120">Refer to [Understand device twins][lnk-twins] for more information about device twins, and to the [IoT Hub query language][lnk-query] reference for querying.</span></span>

> [!NOTE]
> <span data-ttu-id="ee8eb-121">현재 장치 쌍은 MQTT 프로토콜을 사용하여 IoT Hub에 연결하는 장치에서만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee8eb-121">At this time, device twins are accessible only from devices that connect to IoT Hub using the MQTT protocol.</span></span> <span data-ttu-id="ee8eb-122">기존 장치 앱이 MQTT를 사용하도록 변환하는 방법에 관한 설명은 [MQTT 지원][lnk-devguide-mqtt] 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ee8eb-122">Please refer to the [MQTT support][lnk-devguide-mqtt] article for instructions on how to convert existing device app to use MQTT.</span></span>

<span data-ttu-id="ee8eb-123">이 자습서에서는 다음을 수행하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ee8eb-123">This tutorial shows you how to:</span></span>

* <span data-ttu-id="ee8eb-124">*태그*를 장치 쌍에 추가하는 백 엔드 앱과 연결 채널을 *보고된 속성*으로 장치 쌍에 보고하는 시뮬레이션된 장치 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ee8eb-124">Create a back-end app that adds *tags* to a device twin, and a simulated device app that reports its connectivity channel as a *reported property* on the device twin.</span></span>
* <span data-ttu-id="ee8eb-125">이전에 만든 태그 및 속성에 필터를 사용하여 백 엔드 앱에서 장치를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="ee8eb-125">Query devices from your back-end app using filters on the tags and properties previously created.</span></span>

<!-- images -->
[img-twin]: media/iot-hub-selector-twin-get-started/twin.png

<!-- links -->
[lnk-query]: ../articles/iot-hub/iot-hub-devguide-query-language.md
[lnk-twins]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-d2c]: ../articles/iot-hub/iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md