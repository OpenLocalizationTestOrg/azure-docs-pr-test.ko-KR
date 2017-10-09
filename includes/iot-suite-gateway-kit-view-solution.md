## <a name="view-hello-solution-dashboard"></a><span data-ttu-id="62a28-101">Hello 솔루션 대시보드 보기</span><span class="sxs-lookup"><span data-stu-id="62a28-101">View hello solution dashboard</span></span>

<span data-ttu-id="62a28-102">hello 솔루션 대시보드 toomanage 배포 된 hello 솔루션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62a28-102">hello solution dashboard enables you toomanage hello deployed solution.</span></span> <span data-ttu-id="62a28-103">예를 들어 원격 분석 보기, 장치 추가 및 메서드 호출 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62a28-103">For example, you can view telemetry, add devices, and invoke methods.</span></span>

1. <span data-ttu-id="62a28-104">Hello 프로 비전이 완료 된 시점과 미리 구성 된 솔루션에 대 한 hello 타일 나타냅니다 **준비**, 선택 **시작** tooopen 새 탭에서 원격 모니터링 솔루션 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="62a28-104">When hello provisioning is complete and hello tile for your preconfigured solution indicates **Ready**, choose **Launch** tooopen your remote monitoring solution portal in a new tab.</span></span>

    ![미리 구성 하는 hello 솔루션 시작][img-launch-solution]

1. <span data-ttu-id="62a28-106">기본적으로 hello 솔루션 포털 표시 hello *대시보드*합니다.</span><span class="sxs-lookup"><span data-stu-id="62a28-106">By default, hello solution portal shows hello *dashboard*.</span></span> <span data-ttu-id="62a28-107">Hello 메뉴를 사용 하 여 hello hello 페이지의 왼쪽에 hello 솔루션 포털의 tooother 영역을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="62a28-107">Navigate tooother areas of hello solution portal using hello menu on hello left-hand side of hello page.</span></span>

    ![미리 구성된 원격 모니터링 솔루션 대시보드][img-menu]

## <a name="add-a-device"></a><span data-ttu-id="62a28-109">장치 추가</span><span class="sxs-lookup"><span data-stu-id="62a28-109">Add a device</span></span>

<span data-ttu-id="62a28-110">장치 tooconnect toohello 미리 구성 된 솔루션을 식별 해야 합니다 자체 tooIoT 허브 유효한 자격 증명을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="62a28-110">For a device tooconnect toohello preconfigured solution, it must identify itself tooIoT Hub using valid credentials.</span></span> <span data-ttu-id="62a28-111">Hello 솔루션 대시보드에서 hello 장치 자격 증명을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62a28-111">You can retrieve hello device credentials from hello solution dashboard.</span></span> <span data-ttu-id="62a28-112">이 자습서의 뒷부분에 나오는 클라이언트 응용 프로그램에 hello 장치 자격 증명을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="62a28-112">You include hello device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="62a28-113">hello 솔루션 대시보드에 전체 hello 다음 단계를 장치 tooyour 원격 모니터링 솔루션 tooadd 합니다.</span><span class="sxs-lookup"><span data-stu-id="62a28-113">tooadd a device tooyour remote monitoring solution, complete hello following steps in hello solution dashboard:</span></span>

1. <span data-ttu-id="62a28-114">Hello 왼쪽 아래 모퉁이의 hello 대시보드, 클릭 **장치 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="62a28-114">In hello lower left-hand corner of hello dashboard, click **Add a device**.</span></span>

   ![장치 추가][1]

1. <span data-ttu-id="62a28-116">Hello에 **사용자 지정 장치** 에서 **새로 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="62a28-116">In hello **Custom Device** panel, click **Add new**.</span></span>

   ![사용자 지정 장치 추가][2]

1. <span data-ttu-id="62a28-118">**직접 나만의 장치 ID 정의**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="62a28-118">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="62a28-119">장치 ID와 같은 입력 **device01**, 클릭 **ID 확인** tooverify hello 이름, 솔루션에서 이미 사용 하지 않은 하 고 클릭 **만들기** tooprovision hello 장치.</span><span class="sxs-lookup"><span data-stu-id="62a28-119">Enter a Device ID such as **device01**, click **Check ID** tooverify you haven't already used hello name in your solution, and then click **Create** tooprovision hello device.</span></span>

   ![장치 ID 추가][3]

1. <span data-ttu-id="62a28-121">참고 hello 장치 자격 증명 확인 (**장치 ID**, **IoT 허브 호스트 이름을**, 및 **장치 키**).</span><span class="sxs-lookup"><span data-stu-id="62a28-121">Make a note hello device credentials (**Device ID**, **IoT Hub Hostname**, and **Device Key**).</span></span> <span data-ttu-id="62a28-122">Intel NUC hello에 클라이언트 응용 프로그램 모니터링 솔루션 원격 이러한 값 tooconnect toohello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="62a28-122">Your client application on hello Intel NUC needs these values tooconnect toohello remote monitoring solution.</span></span> <span data-ttu-id="62a28-123">**완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62a28-123">Then click **Done**.</span></span>

    ![장치 자격 증명 보기][4]

1. <span data-ttu-id="62a28-125">Hello 솔루션 대시보드에 hello 장치 목록에서 장치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="62a28-125">Select your device in hello device list in hello solution dashboard.</span></span> <span data-ttu-id="62a28-126">그런 다음, hello **장치 세부 정보** 에서 **장치 사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="62a28-126">Then, in hello **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="62a28-127">현재 장치의 hello 상태는 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="62a28-127">hello status of your device is now **Running**.</span></span> <span data-ttu-id="62a28-128">원격 모니터링 솔루션 hello 수 이제 장치에서 원격 분석을 수신 하 고 hello 장치에서 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="62a28-128">hello remote monitoring solution can now receive telemetry from your device and invoke methods on hello device.</span></span>

[img-launch-solution]: media/iot-suite-gateway-kit-view-solution/launch.png
[img-menu]: media/iot-suite-gateway-kit-view-solution/menu.png
[1]: media/iot-suite-gateway-kit-view-solution/suite0.png
[2]: media/iot-suite-gateway-kit-view-solution/suite1.png
[3]: media/iot-suite-gateway-kit-view-solution/suite2.png
[4]: media/iot-suite-gateway-kit-view-solution/suite3.png