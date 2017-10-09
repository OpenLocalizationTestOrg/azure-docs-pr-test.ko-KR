<!--author=alkohli last changed: 9/16/15-->


#### <a name="toocable-your-device-for-power"></a><span data-ttu-id="5bb6a-101">toocable 여 전원 장치를</span><span class="sxs-lookup"><span data-stu-id="5bb6a-101">toocable your device for power</span></span>
> [!NOTE]
> <span data-ttu-id="5bb6a-102">StorSimple 장치의 두 엔클로저 모두가 중복 PCM을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5bb6a-102">Both enclosures on your StorSimple device include redundant PCMs.</span></span> <span data-ttu-id="5bb6a-103">각 인클로저에 대해 hello Pcm 설치 하 고 toodifferent 전원 소스 tooensure 높은 가용성을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bb6a-103">For each enclosure, hello PCMs must be installed and connected toodifferent power sources tooensure high availability.</span></span>
> 
> 

1. <span data-ttu-id="5bb6a-104">Hello 모든 hello Pcm 전원 스위치가 OFF 위치 hello에에서 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bb6a-104">Make sure that hello power switches on all hello PCMs are in hello OFF position.</span></span>
2. <span data-ttu-id="5bb6a-105">Hello 기본 인클로저의 hello 전원 코드 tooboth Pcm을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bb6a-105">On hello primary enclosure, connect hello power cords tooboth PCMs.</span></span> <span data-ttu-id="5bb6a-106">hello 전원 코드는 아래 다이어그램, 케이블 hello 전원에서 빨간색으로 식별 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5bb6a-106">hello power cords are identified in red in hello power cabling diagram, below.</span></span>
3. <span data-ttu-id="5bb6a-107">두 Pcm이 hello 기본 인클로저 별도 전원 사용 하는 hello 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bb6a-107">Make sure that hello two PCMs on hello primary enclosure use separate power sources.</span></span>
4. <span data-ttu-id="5bb6a-108">Hello 전원 코드 toohello 전원 hello 전원 케이블 다이어그램에에서 표시 된 대로 hello 랙 배전 장치에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bb6a-108">Attach hello power cords toohello power on hello rack distribution units as shown in hello power cabling diagram.</span></span>
5. <span data-ttu-id="5bb6a-109">Hello EBOD 인클로저에 대해 2-4 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bb6a-109">Repeat steps 2 through 4 for hello EBOD enclosure.</span></span>
6. <span data-ttu-id="5bb6a-110">Hello 전원 스위치를 각 PCM toohello ON 위치로 전환 하 여 hello EBOD 인클로저를 켭니다.</span><span class="sxs-lookup"><span data-stu-id="5bb6a-110">Turn on hello EBOD enclosure by flipping hello power switch on each PCM toohello ON position.</span></span>
7. <span data-ttu-id="5bb6a-111">Hello hello EBOD 컨트롤러 후면의 녹색 hello led가 ON으로 설정 된 있는지 확인 하 여 해당 hello EBOD 인클로저가 켜져 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bb6a-111">Verify that hello EBOD enclosure is turned on by checking that hello green LEDs on hello back of hello EBOD controller are turned ON.</span></span>
8. <span data-ttu-id="5bb6a-112">각 PCM 스위치 toohello ON 위치로 전환 하 여 hello 기본 인클로저를 켭니다.</span><span class="sxs-lookup"><span data-stu-id="5bb6a-112">Turn on hello primary enclosure by flipping each PCM switch toohello ON position.</span></span>
9. <span data-ttu-id="5bb6a-113">Hello 장치 컨트롤러 Led가 켜 되도록 하 여 hello 시스템을 줄 켜져 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bb6a-113">Verify that hello system is on by ensuring hello device controller LEDs have turned ON.</span></span>
10. <span data-ttu-id="5bb6a-114">Hello 4 개의 led가 다음 toohello SAS 포트 hello EBOD 컨트롤러가 녹색 인지 확인 하 여 hello EBOD 컨트롤러와 hello 장치 컨트롤러 간의 hello 연결이 활성 상태 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5bb6a-114">Make sure that hello connection between hello EBOD controller and hello device controller is active by verifying that hello four LEDs next toohello SAS port on hello EBOD controller are green.</span></span>
    
    > [!IMPORTANT]
    > <span data-ttu-id="5bb6a-115">시스템에 대 한 높은 수준의 가용성 tooensure toohello 전원 케이블 연결 hello 다음 다이어그램에에서 표시 된 체계를 엄격 하 게 준수 하는 두는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5bb6a-115">tooensure high availability for your system, we recommend that you strictly adhere toohello power cabling scheme shown in hello following diagram.</span></span>
    > 
    > 
    
    ![전원에 4U 장치를 케이블로 연결](./media/storsimple-cable-8600-for-power/HCSCableYour4UDeviceforPower.png)
    
    <span data-ttu-id="5bb6a-117">**전원 케이블 연결**</span><span class="sxs-lookup"><span data-stu-id="5bb6a-117">**Power cabling**</span></span>
    
    | <span data-ttu-id="5bb6a-118">레이블</span><span class="sxs-lookup"><span data-stu-id="5bb6a-118">Label</span></span> | <span data-ttu-id="5bb6a-119">설명</span><span class="sxs-lookup"><span data-stu-id="5bb6a-119">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="5bb6a-120">1</span><span class="sxs-lookup"><span data-stu-id="5bb6a-120">1</span></span> |<span data-ttu-id="5bb6a-121">기본 인클로저</span><span class="sxs-lookup"><span data-stu-id="5bb6a-121">Primary enclosure</span></span> |
    | <span data-ttu-id="5bb6a-122">2</span><span class="sxs-lookup"><span data-stu-id="5bb6a-122">2</span></span> |<span data-ttu-id="5bb6a-123">PCM 0</span><span class="sxs-lookup"><span data-stu-id="5bb6a-123">PCM 0</span></span> |
    | <span data-ttu-id="5bb6a-124">3</span><span class="sxs-lookup"><span data-stu-id="5bb6a-124">3</span></span> |<span data-ttu-id="5bb6a-125">PCM 1</span><span class="sxs-lookup"><span data-stu-id="5bb6a-125">PCM 1</span></span> |
    | <span data-ttu-id="5bb6a-126">4</span><span class="sxs-lookup"><span data-stu-id="5bb6a-126">4</span></span> |<span data-ttu-id="5bb6a-127">컨트롤러 0</span><span class="sxs-lookup"><span data-stu-id="5bb6a-127">Controller 0</span></span> |
    | <span data-ttu-id="5bb6a-128">5</span><span class="sxs-lookup"><span data-stu-id="5bb6a-128">5</span></span> |<span data-ttu-id="5bb6a-129">컨트롤러 1</span><span class="sxs-lookup"><span data-stu-id="5bb6a-129">Controller 1</span></span> |
    | <span data-ttu-id="5bb6a-130">6</span><span class="sxs-lookup"><span data-stu-id="5bb6a-130">6</span></span> |<span data-ttu-id="5bb6a-131">EBOD 컨트롤러 0</span><span class="sxs-lookup"><span data-stu-id="5bb6a-131">EBOD controller 0</span></span> |
    | <span data-ttu-id="5bb6a-132">7</span><span class="sxs-lookup"><span data-stu-id="5bb6a-132">7</span></span> |<span data-ttu-id="5bb6a-133">EBOD 컨트롤러 1</span><span class="sxs-lookup"><span data-stu-id="5bb6a-133">EBOD controller 1</span></span> |
    | <span data-ttu-id="5bb6a-134">8</span><span class="sxs-lookup"><span data-stu-id="5bb6a-134">8</span></span> |<span data-ttu-id="5bb6a-135">EBOD 인클로저</span><span class="sxs-lookup"><span data-stu-id="5bb6a-135">EBOD enclosure</span></span> |
    | <span data-ttu-id="5bb6a-136">9</span><span class="sxs-lookup"><span data-stu-id="5bb6a-136">9</span></span> |<span data-ttu-id="5bb6a-137">PDU</span><span class="sxs-lookup"><span data-stu-id="5bb6a-137">PDUs</span></span> |

