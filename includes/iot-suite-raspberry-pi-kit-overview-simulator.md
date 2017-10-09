## <a name="overview"></a><span data-ttu-id="a169b-101">개요</span><span class="sxs-lookup"><span data-stu-id="a169b-101">Overview</span></span>

<span data-ttu-id="a169b-102">이 자습서의 단계를 수행 하는 hello를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="a169b-102">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="a169b-103">Hello 원격 모니터링 미리 구성 된 솔루션 tooyour Azure 구독의 인스턴스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="a169b-103">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="a169b-104">이 단계에서는 여러 Azure 서비스를 자동으로 배포하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a169b-104">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="a169b-105">컴퓨터 및 원격 모니터링 솔루션 hello와 장치 toocommunicate 사용자를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a169b-105">Set up your device toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="a169b-106">Hello 샘플 장치 코드 tooconnect toohello 원격 모니터링 솔루션을 업데이트 하 고 hello 솔루션 대시보드에서 볼 수 있는 시뮬레이션 된 원격 분석.</span><span class="sxs-lookup"><span data-stu-id="a169b-106">Update hello sample device code tooconnect toohello remote monitoring solution, and send simulated telemetry that you can view on hello solution dashboard.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a169b-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a169b-107">Prerequisites</span></span>

<span data-ttu-id="a169b-108">toocomplete이이 자습서에서는 활성 Azure 구독이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a169b-108">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="a169b-109">계정이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a169b-109">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="a169b-110">자세한 내용은 [Azure 무료 평가판][lnk-free-trial]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a169b-110">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

### <a name="required-software"></a><span data-ttu-id="a169b-111">필수 소프트웨어</span><span class="sxs-lookup"><span data-stu-id="a169b-111">Required software</span></span>

<span data-ttu-id="a169b-112">사용자 데스크톱 컴퓨터 tooenable 있습니다 tooremotely 액세스 hello 명령줄로 라스베리 Pi hello에에 SSH 클라이언트를 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a169b-112">You need SSH client on your desktop machine tooenable you tooremotely access hello command line on hello Raspberry Pi.</span></span>

- <span data-ttu-id="a169b-113">Windows에서는 SSH 클라이언트를 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a169b-113">Windows does not include an SSH client.</span></span> <span data-ttu-id="a169b-114">[PuTTY](http://www.putty.org/)를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a169b-114">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="a169b-115">대부분의 Linux 배포판 및 Mac OS 명령줄 SSH 유틸리티 hello를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a169b-115">Most Linux distributions and Mac OS include hello command-line SSH utility.</span></span> <span data-ttu-id="a169b-116">자세한 내용은 [Linux 또는 Mac OS를 사용하는 SSH](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a169b-116">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

### <a name="required-hardware"></a><span data-ttu-id="a169b-117">필수 하드웨어</span><span class="sxs-lookup"><span data-stu-id="a169b-117">Required hardware</span></span>

<span data-ttu-id="a169b-118">데스크톱 컴퓨터 tooenable tooconnect 하면 원격으로 toohello 명령줄로 라스베리 Pi hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a169b-118">A desktop computer tooenable you tooconnect remotely toohello command line on hello Raspberry Pi.</span></span>

<span data-ttu-id="a169b-119">[Raspberry Pi 3용 Microsoft IoT 시작 키트][lnk-starter-kits] 또는 동등한 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="a169b-119">[Microsoft IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] or equivalent components.</span></span> <span data-ttu-id="a169b-120">이 자습서에서는 hello hello 키트에서 다음 항목을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a169b-120">This tutorial uses hello following items from hello kit:</span></span>

- <span data-ttu-id="a169b-121">Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="a169b-121">Raspberry Pi 3</span></span>
- <span data-ttu-id="a169b-122">MicroSD 카드(NOOBS 포함)</span><span class="sxs-lookup"><span data-stu-id="a169b-122">MicroSD Card (with NOOBS)</span></span>
- <span data-ttu-id="a169b-123">USB 미니 케이블</span><span class="sxs-lookup"><span data-stu-id="a169b-123">A USB Mini cable</span></span>
- <span data-ttu-id="a169b-124">이더넷 케이블</span><span class="sxs-lookup"><span data-stu-id="a169b-124">An Ethernet cable</span></span>

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/