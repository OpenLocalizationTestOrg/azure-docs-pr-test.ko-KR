## <a name="overview"></a><span data-ttu-id="316af-101">개요</span><span class="sxs-lookup"><span data-stu-id="316af-101">Overview</span></span>

<span data-ttu-id="316af-102">이 자습서에서는 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="316af-102">In this tutorial, you complete the following steps:</span></span>

- <span data-ttu-id="316af-103">Azure 구독에서 미리 구성된 원격 모니터링 솔루션의 인스턴스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="316af-103">Deploy an instance of the remote monitoring preconfigured solution to your Azure subscription.</span></span> <span data-ttu-id="316af-104">이 단계에서는 여러 Azure 서비스를 자동으로 배포하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="316af-104">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="316af-105">사용자 컴퓨터 및 원격 모니터링 솔루션과 통신하도록 장치를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="316af-105">Set up your device to communicate with your computer and the remote monitoring solution.</span></span>
- <span data-ttu-id="316af-106">샘플 장치 코드를 업데이트하여 원격 모니터링 솔루션에 연결하고 솔루션 대시보드에서 볼 수 있는 시뮬레이션된 원격 분석을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="316af-106">Update the sample device code to connect to the remote monitoring solution, and send simulated telemetry that you can view on the solution dashboard.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="316af-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="316af-107">Prerequisites</span></span>

<span data-ttu-id="316af-108">이 자습서를 완료하려면 활성 Azure 구독이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="316af-108">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="316af-109">계정이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="316af-109">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="316af-110">자세한 내용은 [Azure 무료 평가판][lnk-free-trial]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="316af-110">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

### <a name="required-software"></a><span data-ttu-id="316af-111">필수 소프트웨어</span><span class="sxs-lookup"><span data-stu-id="316af-111">Required software</span></span>

<span data-ttu-id="316af-112">Raspberry Pi의 명령줄에 원격으로 액세스할 수 있도록 데스크톱 컴퓨터에 SSH 클라이언트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="316af-112">You need SSH client on your desktop machine to enable you to remotely access the command line on the Raspberry Pi.</span></span>

- <span data-ttu-id="316af-113">Windows에서는 SSH 클라이언트를 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="316af-113">Windows does not include an SSH client.</span></span> <span data-ttu-id="316af-114">[PuTTY](http://www.putty.org/)를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="316af-114">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="316af-115">대부분의 Linux 배포판 및 Mac OS는 명령줄 SSH 유틸리티를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="316af-115">Most Linux distributions and Mac OS include the command-line SSH utility.</span></span> <span data-ttu-id="316af-116">자세한 내용은 [Linux 또는 Mac OS를 사용하는 SSH](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="316af-116">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

### <a name="required-hardware"></a><span data-ttu-id="316af-117">필수 하드웨어</span><span class="sxs-lookup"><span data-stu-id="316af-117">Required hardware</span></span>

<span data-ttu-id="316af-118">Raspberry Pi의 명령줄에 원격으로 연결할 수 있는 데스크톱 컴퓨터이며</span><span class="sxs-lookup"><span data-stu-id="316af-118">A desktop computer to enable you to connect remotely to the command line on the Raspberry Pi.</span></span>

<span data-ttu-id="316af-119">[Raspberry Pi 3용 Microsoft IoT 시작 키트][lnk-starter-kits] 또는 동등한 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="316af-119">[Microsoft IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] or equivalent components.</span></span> <span data-ttu-id="316af-120">이 자습서에서는 키트에서 다음 항목을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="316af-120">This tutorial uses the following items from the kit:</span></span>

- <span data-ttu-id="316af-121">Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="316af-121">Raspberry Pi 3</span></span>
- <span data-ttu-id="316af-122">MicroSD 카드(NOOBS 포함)</span><span class="sxs-lookup"><span data-stu-id="316af-122">MicroSD Card (with NOOBS)</span></span>
- <span data-ttu-id="316af-123">USB 미니 케이블</span><span class="sxs-lookup"><span data-stu-id="316af-123">A USB Mini cable</span></span>
- <span data-ttu-id="316af-124">이더넷 케이블</span><span class="sxs-lookup"><span data-stu-id="316af-124">An Ethernet cable</span></span>

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/