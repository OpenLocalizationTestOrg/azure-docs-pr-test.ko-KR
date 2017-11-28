> [!div class="op_single_selector"]
> * [<span data-ttu-id="8658e-101">Linux</span><span class="sxs-lookup"><span data-stu-id="8658e-101">Linux</span></span>](../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md)
> * [<span data-ttu-id="8658e-102">Windows</span><span class="sxs-lookup"><span data-stu-id="8658e-102">Windows</span></span>](../articles/iot-hub/iot-hub-windows-iot-edge-get-started.md)
> 
> 

<span data-ttu-id="8658e-103">이 문서에서는 [헬로 월드 샘플 코드][lnk-helloworld-sample]에 대한 자세한 연습을 제공하여 [Azure IoT Edge][lnk-iot-edge] 아키텍처의 기본 구성 요소에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8658e-103">This article provides a detailed walkthrough of the [Hello World sample code][lnk-helloworld-sample] to illustrate the fundamental components of the [Azure IoT Edge][lnk-iot-edge] architecture.</span></span> <span data-ttu-id="8658e-104">샘플에서 Azure IoT Edge를 사용하여 5초마다 "헬로 월드" 메시지를 파일에 기록하는 간단한 게이트웨이를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="8658e-104">The sample uses the Azure IoT Edge to build a simple gateway that logs a "hello world" message to a file every five seconds.</span></span>

<span data-ttu-id="8658e-105">이 연습에서는 다음 내용을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="8658e-105">This walkthrough covers:</span></span>

* <span data-ttu-id="8658e-106">**Hello World 샘플 아키텍처**: Hello World 샘플에 [Azure IoT Edge 아키텍처 개념][lnk-edge-concepts]이 어떻게 적용되는지 구성 요소가 어떻게 배치되는지를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8658e-106">**Hello World sample architecture**: Describes how [Azure IoT Edge architectural concepts][lnk-edge-concepts] apply to the Hello World sample and how the components fit together.</span></span>
* <span data-ttu-id="8658e-107">**샘플 작성 방법**: 샘플 작성에 필요한 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="8658e-107">**How to build the sample**: The steps required to build the sample.</span></span>
* <span data-ttu-id="8658e-108">**샘플 실행 방법**: 샘플 실행에 필요한 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="8658e-108">**How to run the sample**: The steps required to run the sample.</span></span> 
* <span data-ttu-id="8658e-109">**일반적인 출력**: 샘플을 실행할 때 예상되는 출력의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="8658e-109">**Typical output**: An example of the output to expect when you run the sample.</span></span>
* <span data-ttu-id="8658e-110">**코드 조각**: 헬로 월드 샘플에서 주요 IoT Edge 게이트웨이 구성 요소를 구현하는 방법을 보여 주는 코드 조각의 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="8658e-110">**Code snippets**: A collection of code snippets to show how the Hello World sample implements key IoT Edge gateway components.</span></span>


## <a name="hello-world-sample-architecture"></a><span data-ttu-id="8658e-111">Hello World 샘플 아키텍처</span><span class="sxs-lookup"><span data-stu-id="8658e-111">Hello World sample architecture</span></span>
<span data-ttu-id="8658e-112">Hello World 샘플은 이전 섹션에서 설명한 개념을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8658e-112">The Hello World sample illustrates the concepts described in the previous section.</span></span> <span data-ttu-id="8658e-113">헬로 월드 샘플은 두 개의 IoT Edge 모듈로 구성된 파이프라인이 있는 IoT Edge 게이트웨이를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="8658e-113">The Hello World sample implements a IoT Edge gateway that has a pipeline made up of two IoT Edge modules:</span></span>

* <span data-ttu-id="8658e-114">*hello world* 모듈은 5초마다 메시지를 생성하여 로거 모듈에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="8658e-114">The *hello world* module creates a message every five seconds and passes it to the logger module.</span></span>
* <span data-ttu-id="8658e-115">*로거* 모듈은 수신하는 메시지를 파일에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="8658e-115">The *logger* module writes the messages it receives to a file.</span></span>

![Azure IoT Edge로 만든 헬로 월드 샘플 아키텍처][4]

<span data-ttu-id="8658e-117">이전 섹션의 설명처럼, Hello World 모듈은 로거 모듈에 5초마다 메시지를 직접 전달하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8658e-117">As described in the previous section, the Hello World module does not pass messages directly to the logger module every five seconds.</span></span> <span data-ttu-id="8658e-118">대신, 5초마다 broker에 메시지를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="8658e-118">Instead, it publishes a message to the broker every five seconds.</span></span>

<span data-ttu-id="8658e-119">로거 모듈은 broker에서 메시지를 받고 broker에서 메세지를 실행하며 메시지의 내용을 파일에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="8658e-119">The logger module receives the message from the broker and acts upon it, writing the contents of the message to a file.</span></span>

<span data-ttu-id="8658e-120">로거 모듈은 broker의 메시지를 사용하기만 하고 broker에 새 메시지를 게시하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8658e-120">The logger module only consumes messages from the broker, it never publishes new messages to the broker.</span></span>

![Azure IoT Edge에서 Broker가 모듈 간에 메시지를 라우팅하는 방법][5]

<span data-ttu-id="8658e-122">위 그림은 Hello World 샘플의 아키텍처와 [리포지토리][lnk-iot-edge]에서 샘플의 다른 부분을 구현하는 원본 파일에 대한 상대 경로를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8658e-122">The figure above shows the architecture of the Hello World sample and the relative paths to the source files that implement different portions of the sample in the [repository][lnk-iot-edge].</span></span> <span data-ttu-id="8658e-123">코드를 직접 알아보거나 아래 코드 조각을 참조용으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8658e-123">Explore the code on your own, or use the code snippets below as a guide.</span></span>

<!-- Images -->
[4]: media/iot-hub-iot-edge-getstarted-selector/high_level_architecture.png
[5]: media/iot-hub-iot-edge-getstarted-selector/detailed_architecture.png

<!-- Links -->
[lnk-helloworld-sample]: https://github.com/Azure/iot-edge/tree/master/samples/hello_world
[lnk-iot-edge]: https://github.com/Azure/iot-edge
[lnk-edge-concepts]: ../articles/iot-hub/iot-hub-iot-edge-overview.md