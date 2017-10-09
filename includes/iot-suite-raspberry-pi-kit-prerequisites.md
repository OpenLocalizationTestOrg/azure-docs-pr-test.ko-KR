## <a name="prerequisites"></a><span data-ttu-id="1d4e7-101">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1d4e7-101">Prerequisites</span></span>

<span data-ttu-id="1d4e7-102">toocomplete이이 자습서에서는 활성 Azure 구독이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d4e7-102">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="1d4e7-103">계정이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d4e7-103">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="1d4e7-104">자세한 내용은 [Azure 무료 평가판][lnk-free-trial]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d4e7-104">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

### <a name="required-software"></a><span data-ttu-id="1d4e7-105">필수 소프트웨어</span><span class="sxs-lookup"><span data-stu-id="1d4e7-105">Required software</span></span>

<span data-ttu-id="1d4e7-106">사용자 데스크톱 컴퓨터 tooenable 있습니다 tooremotely 액세스 hello 명령줄로 라스베리 Pi hello에에 SSH 클라이언트를 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d4e7-106">You need SSH client on your desktop machine tooenable you tooremotely access hello command line on hello Raspberry Pi.</span></span>

- <span data-ttu-id="1d4e7-107">Windows에서는 SSH 클라이언트를 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1d4e7-107">Windows does not include an SSH client.</span></span> <span data-ttu-id="1d4e7-108">[PuTTY](http://www.putty.org/)를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1d4e7-108">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="1d4e7-109">대부분의 Linux 배포판 및 Mac OS 명령줄 SSH 유틸리티 hello를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1d4e7-109">Most Linux distributions and Mac OS include hello command-line SSH utility.</span></span> <span data-ttu-id="1d4e7-110">자세한 내용은 [Linux 또는 Mac OS를 사용하는 SSH](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d4e7-110">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

### <a name="required-hardware"></a><span data-ttu-id="1d4e7-111">필수 하드웨어</span><span class="sxs-lookup"><span data-stu-id="1d4e7-111">Required hardware</span></span>

<span data-ttu-id="1d4e7-112">데스크톱 컴퓨터 tooenable tooconnect 하면 원격으로 toohello 명령줄로 라스베리 Pi hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d4e7-112">A desktop computer tooenable you tooconnect remotely toohello command line on hello Raspberry Pi.</span></span>

<span data-ttu-id="1d4e7-113">[Raspberry Pi 3용 Microsoft IoT 시작 키트][lnk-starter-kits] 또는 동등한 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="1d4e7-113">[Microsoft IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] or equivalent components.</span></span> <span data-ttu-id="1d4e7-114">이 자습서에서는 hello hello 키트에서 다음 항목을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d4e7-114">This tutorial uses hello following items from hello kit:</span></span>

- <span data-ttu-id="1d4e7-115">Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="1d4e7-115">Raspberry Pi 3</span></span>
- <span data-ttu-id="1d4e7-116">MicroSD 카드(NOOBS 포함)</span><span class="sxs-lookup"><span data-stu-id="1d4e7-116">MicroSD Card (with NOOBS)</span></span>
- <span data-ttu-id="1d4e7-117">USB 미니 케이블</span><span class="sxs-lookup"><span data-stu-id="1d4e7-117">A USB Mini cable</span></span>
- <span data-ttu-id="1d4e7-118">이더넷 케이블</span><span class="sxs-lookup"><span data-stu-id="1d4e7-118">An Ethernet cable</span></span>
- <span data-ttu-id="1d4e7-119">BME280 센서</span><span class="sxs-lookup"><span data-stu-id="1d4e7-119">BME280 sensor</span></span>
- <span data-ttu-id="1d4e7-120">브레드보드</span><span class="sxs-lookup"><span data-stu-id="1d4e7-120">Breadboard</span></span>
- <span data-ttu-id="1d4e7-121">점퍼 와이어</span><span class="sxs-lookup"><span data-stu-id="1d4e7-121">Jumper wires</span></span>
- <span data-ttu-id="1d4e7-122">저항기</span><span class="sxs-lookup"><span data-stu-id="1d4e7-122">Resistors</span></span>
- <span data-ttu-id="1d4e7-123">LED</span><span class="sxs-lookup"><span data-stu-id="1d4e7-123">LEDs</span></span>

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/