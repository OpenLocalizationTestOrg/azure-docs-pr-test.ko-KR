> [!div class="op_single_selector"]
> * [<span data-ttu-id="4ebe7-101">Linux</span><span class="sxs-lookup"><span data-stu-id="4ebe7-101">Linux</span></span>](../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md)
> * [<span data-ttu-id="4ebe7-102">Windows</span><span class="sxs-lookup"><span data-stu-id="4ebe7-102">Windows</span></span>](../articles/iot-hub/iot-hub-windows-iot-edge-get-started.md)
> 
> 

<span data-ttu-id="4ebe7-103">이 문서에서는 hello의 자세한 연습 [Hello World 예제 코드] [ lnk-helloworld-sample] tooillustrate hello의 기본 구성 요소 hello [Azure IoT 가장자리] [ lnk-iot-edge] 아키텍처.</span><span class="sxs-lookup"><span data-stu-id="4ebe7-103">This article provides a detailed walkthrough of hello [Hello World sample code][lnk-helloworld-sample] tooillustrate hello fundamental components of hello [Azure IoT Edge][lnk-iot-edge] architecture.</span></span> <span data-ttu-id="4ebe7-104">hello 샘플에서는 hello Azure IoT 가장자리 toobuild "hello world" 메시지 tooa 파일 5 초 마다 기록 하는 간단한 게이트웨이 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ebe7-104">hello sample uses hello Azure IoT Edge toobuild a simple gateway that logs a "hello world" message tooa file every five seconds.</span></span>

<span data-ttu-id="4ebe7-105">이 연습에서는 다음 내용을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="4ebe7-105">This walkthrough covers:</span></span>

* <span data-ttu-id="4ebe7-106">**Hello World 샘플 아키텍처**: 설명 방법을 [Azure IoT 가장자리 아키텍처 개념] [ lnk-edge-concepts] toohello Hello World 예제 추가 정보 및 구성 요소 hello 개념이 서로 어떻게 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ebe7-106">**Hello World sample architecture**: Describes how [Azure IoT Edge architectural concepts][lnk-edge-concepts] apply toohello Hello World sample and how hello components fit together.</span></span>
* <span data-ttu-id="4ebe7-107">**어떻게 toobuild hello 샘플**: hello 단계 필요한 toobuild hello 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="4ebe7-107">**How toobuild hello sample**: hello steps required toobuild hello sample.</span></span>
* <span data-ttu-id="4ebe7-108">**어떻게 toorun hello 샘플**: hello 단계 필요한 toorun hello 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="4ebe7-108">**How toorun hello sample**: hello steps required toorun hello sample.</span></span> 
* <span data-ttu-id="4ebe7-109">**일반적인 출력**: hello의 예는 hello 샘플을 실행 하면 tooexpect를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ebe7-109">**Typical output**: An example of hello output tooexpect when you run hello sample.</span></span>
* <span data-ttu-id="4ebe7-110">**코드 조각**: 핵심 IoT 가장자리 게이트웨이 구성 요소 코드 조각 tooshow hello Hello World 예제 구현 하는 방법의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="4ebe7-110">**Code snippets**: A collection of code snippets tooshow how hello Hello World sample implements key IoT Edge gateway components.</span></span>


## <a name="hello-world-sample-architecture"></a><span data-ttu-id="4ebe7-111">Hello World 샘플 아키텍처</span><span class="sxs-lookup"><span data-stu-id="4ebe7-111">Hello World sample architecture</span></span>
<span data-ttu-id="4ebe7-112">hello Hello World 예제는 hello 이전 섹션에 설명 된 hello 개념을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4ebe7-112">hello Hello World sample illustrates hello concepts described in hello previous section.</span></span> <span data-ttu-id="4ebe7-113">hello Hello World 예제는 두 IoT 가장자리 모듈로 구성 하는 파이프라인에 있는 IoT 지 게이트웨이 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ebe7-113">hello Hello World sample implements a IoT Edge gateway that has a pipeline made up of two IoT Edge modules:</span></span>

* <span data-ttu-id="4ebe7-114">hello *hello world* 모듈 메시지 5 초 마다를 만들고 toohello로 거 모듈을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ebe7-114">hello *hello world* module creates a message every five seconds and passes it toohello logger module.</span></span>
* <span data-ttu-id="4ebe7-115">hello *로 거* 모듈 쓰기 hello 메시지 tooa 파일을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="4ebe7-115">hello *logger* module writes hello messages it receives tooa file.</span></span>

![Azure IoT Edge로 만든 헬로 월드 샘플 아키텍처][4]

<span data-ttu-id="4ebe7-117">Hello 이전 섹션에서 설명한 대로 모듈은 전달 하지는 Hello World hello 메시지 직접 toohello로 거 모듈 5 초 마다 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ebe7-117">As described in hello previous section, hello Hello World module does not pass messages directly toohello logger module every five seconds.</span></span> <span data-ttu-id="4ebe7-118">대신, 메시지 toohello 브로커 5 초 마다 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="4ebe7-118">Instead, it publishes a message toohello broker every five seconds.</span></span>

<span data-ttu-id="4ebe7-119">hello로 거 모듈 hello 브로커에서 hello 메시지를 수신 하 고 hello 메시지 tooa 파일의 hello 콘텐츠 쓰기,에 대해 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ebe7-119">hello logger module receives hello message from hello broker and acts upon it, writing hello contents of hello message tooa file.</span></span>

<span data-ttu-id="4ebe7-120">hello로 거 모듈을 사용 하므로 hello broker에서 메시지를 새 메시지 toohello 브로커를 게시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4ebe7-120">hello logger module only consumes messages from hello broker, it never publishes new messages toohello broker.</span></span>

![Hello 브로커 Azure IoT 가장자리의 모듈 간에 메시지를 라우팅하 하는 방법][5]

<span data-ttu-id="4ebe7-122">hello 위의 그림 hello 아키텍처 hello Hello World 예제 추가 정보 및 상대 경로 hello hello에 hello 샘플의 서로 다른 부분을 구현 하는 toohello 소스 파일 [리포지토리][lnk-iot-edge]합니다.</span><span class="sxs-lookup"><span data-stu-id="4ebe7-122">hello figure above shows hello architecture of hello Hello World sample and hello relative paths toohello source files that implement different portions of hello sample in hello [repository][lnk-iot-edge].</span></span> <span data-ttu-id="4ebe7-123">직접 hello 코드를 탐색 하거나 아래 코드 조각 hello 가이드로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ebe7-123">Explore hello code on your own, or use hello code snippets below as a guide.</span></span>

<!-- Images -->
[4]: media/iot-hub-iot-edge-getstarted-selector/high_level_architecture.png
[5]: media/iot-hub-iot-edge-getstarted-selector/detailed_architecture.png

<!-- Links -->
[lnk-helloworld-sample]: https://github.com/Azure/iot-edge/tree/master/samples/hello_world
[lnk-iot-edge]: https://github.com/Azure/iot-edge
[lnk-edge-concepts]: ../articles/iot-hub/iot-hub-iot-edge-overview.md