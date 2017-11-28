## <a name="view-the-solution-dashboard"></a><span data-ttu-id="c42d4-101">솔루션 대시보드 보기</span><span class="sxs-lookup"><span data-stu-id="c42d4-101">View the solution dashboard</span></span>

<span data-ttu-id="c42d4-102">솔루션 대시보드를 사용하면 배포된 솔루션을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c42d4-102">The solution dashboard enables you to manage the deployed solution.</span></span> <span data-ttu-id="c42d4-103">예를 들어 원격 분석 보기, 장치 추가 및 메서드 호출 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c42d4-103">For example, you can view telemetry, add devices, and invoke methods.</span></span>

1. <span data-ttu-id="c42d4-104">프로비전이 완료되고 미리 구성된 솔루션에 대한 타일이 **준비**를 가리키면 **시작**을 선택하여 새 탭에서 원격 모니터링 솔루션 포털을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c42d4-104">When the provisioning is complete and the tile for your preconfigured solution indicates **Ready**, choose **Launch** to open your remote monitoring solution portal in a new tab.</span></span>

    ![미리 구성된 솔루션 시작][img-launch-solution]

1. <span data-ttu-id="c42d4-106">기본적으로 솔루션 포털에 *대시보드*가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c42d4-106">By default, the solution portal shows the *dashboard*.</span></span> <span data-ttu-id="c42d4-107">페이지 왼쪽의 메뉴를 사용하여 솔루션 포털의 다른 영역으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c42d4-107">Navigate to other areas of the solution portal using the menu on the left-hand side of the page.</span></span>

    ![미리 구성된 원격 모니터링 솔루션 대시보드][img-menu]

## <a name="add-a-device"></a><span data-ttu-id="c42d4-109">장치 추가</span><span class="sxs-lookup"><span data-stu-id="c42d4-109">Add a device</span></span>

<span data-ttu-id="c42d4-110">미리 구성된 솔루션에 연결하는 장치는 유효한 자격 증명을 사용하여 IoT Hub에 자신을 식별할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c42d4-110">For a device to connect to the preconfigured solution, it must identify itself to IoT Hub using valid credentials.</span></span> <span data-ttu-id="c42d4-111">솔루션 대시보드에서 장치 자격 증명을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c42d4-111">You can retrieve the device credentials from the solution dashboard.</span></span> <span data-ttu-id="c42d4-112">이 자습서의 뒷부분에서는 클라이언트 응용 프로그램에 있는 장치 자격 증명을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c42d4-112">You include the device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="c42d4-113">원격 모니터링 솔루션에 장치를 추가하려면 솔루션 대시보드에서 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="c42d4-113">To add a device to your remote monitoring solution, complete the following steps in the solution dashboard:</span></span>

1. <span data-ttu-id="c42d4-114">대시보드의 왼쪽 아래 모서리에서 **장치 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c42d4-114">In the lower left-hand corner of the dashboard, click **Add a device**.</span></span>

   ![장치 추가][1]

1. <span data-ttu-id="c42d4-116">**사용자 지정 장치** 패널에서 **새로 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c42d4-116">In the **Custom Device** panel, click **Add new**.</span></span>

   ![사용자 지정 장치 추가][2]

1. <span data-ttu-id="c42d4-118">**직접 나만의 장치 ID 정의**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c42d4-118">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="c42d4-119">장치 ID(예: **device01**)를 입력하고 **ID 확인**을 클릭하여 솔루션에서 해당 이름이 이미 사용되고 있는지 확인한 다음 **만들기**를 클릭하여 장치를 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="c42d4-119">Enter a Device ID such as **device01**, click **Check ID** to verify you haven't already used the name in your solution, and then click **Create** to provision the device.</span></span>

   ![장치 ID 추가][3]

1. <span data-ttu-id="c42d4-121">장치 자격 증명(**장치 ID**, **IoT Hub 호스트 이름** 및 **장치 키**)을 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="c42d4-121">Make a note the device credentials (**Device ID**, **IoT Hub Hostname**, and **Device Key**).</span></span> <span data-ttu-id="c42d4-122">원격 모니터링 솔루션에 연결하려면 Intel NUC의 클라이언트 응용 프로그램에 이러한 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c42d4-122">Your client application on the Intel NUC needs these values to connect to the remote monitoring solution.</span></span> <span data-ttu-id="c42d4-123">**완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c42d4-123">Then click **Done**.</span></span>

    ![장치 자격 증명 보기][4]

1. <span data-ttu-id="c42d4-125">솔루션 대시보드의 장치 목록에서 장치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c42d4-125">Select your device in the device list in the solution dashboard.</span></span> <span data-ttu-id="c42d4-126">그런 다음 **장치 세부 정보** 패널에서 **장치 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c42d4-126">Then, in the **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="c42d4-127">현재 장치 상태는 **실행 중**입니다.</span><span class="sxs-lookup"><span data-stu-id="c42d4-127">The status of your device is now **Running**.</span></span> <span data-ttu-id="c42d4-128">이제 원격 모니터링 솔루션은 장치에서 원격 분석을 수신하고 장치에서 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c42d4-128">The remote monitoring solution can now receive telemetry from your device and invoke methods on the device.</span></span>

[img-launch-solution]: media/iot-suite-gateway-kit-view-solution/launch.png
[img-menu]: media/iot-suite-gateway-kit-view-solution/menu.png
[1]: media/iot-suite-gateway-kit-view-solution/suite0.png
[2]: media/iot-suite-gateway-kit-view-solution/suite1.png
[3]: media/iot-suite-gateway-kit-view-solution/suite2.png
[4]: media/iot-suite-gateway-kit-view-solution/suite3.png