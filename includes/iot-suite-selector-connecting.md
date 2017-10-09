> [!div class="op_single_selector"]
> * [<span data-ttu-id="fdd0b-101">Windows에서 C</span><span class="sxs-lookup"><span data-stu-id="fdd0b-101">C on Windows</span></span>](../articles/iot-suite/iot-suite-connecting-devices.md)
> * [<span data-ttu-id="fdd0b-102">Linux에서 C</span><span class="sxs-lookup"><span data-stu-id="fdd0b-102">C on Linux</span></span>](../articles/iot-suite/iot-suite-connecting-devices-linux.md)
> * [<span data-ttu-id="fdd0b-103">Node.JS</span><span class="sxs-lookup"><span data-stu-id="fdd0b-103">Node.js</span></span>](../articles/iot-suite/iot-suite-connecting-devices-node.md)
> 
> 

## <a name="scenario-overview"></a><span data-ttu-id="fdd0b-104">시나리오 개요</span><span class="sxs-lookup"><span data-stu-id="fdd0b-104">Scenario overview</span></span>
<span data-ttu-id="fdd0b-105">이 시나리오에서는 원격 분석 toohello 원격 모니터링을 수행 하는 hello를 전송 하는 장치를 만들 [솔루션 미리 구성 된][lnk-what-are-preconfig-solutions]:</span><span class="sxs-lookup"><span data-stu-id="fdd0b-105">In this scenario, you create a device that sends hello following telemetry toohello remote monitoring [preconfigured solution][lnk-what-are-preconfig-solutions]:</span></span>

* <span data-ttu-id="fdd0b-106">외부 온도</span><span class="sxs-lookup"><span data-stu-id="fdd0b-106">External temperature</span></span>
* <span data-ttu-id="fdd0b-107">내부 온도</span><span class="sxs-lookup"><span data-stu-id="fdd0b-107">Internal temperature</span></span>
* <span data-ttu-id="fdd0b-108">습도</span><span class="sxs-lookup"><span data-stu-id="fdd0b-108">Humidity</span></span>

<span data-ttu-id="fdd0b-109">간단한 설명을 위해 hello 장치에서 hello 코드 샘플 값을 생성 하지만 실제 센서 tooyour 장치를 연결 하 고 실제 원격 분석 보내기 tooextend hello 샘플 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="fdd0b-109">For simplicity, hello code on hello device generates sample values, but we encourage you tooextend hello sample by connecting real sensors tooyour device and sending real telemetry.</span></span>

<span data-ttu-id="fdd0b-110">hello 장치 수 toorespond toomethods hello 솔루션 대시보드에서 호출 하 고 원하는 hello 솔루션 대시보드에 설정 된 속성 값 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd0b-110">hello device is also able toorespond toomethods invoked from hello solution dashboard and desired property values set in hello solution dashboard.</span></span>

<span data-ttu-id="fdd0b-111">toocomplete이이 자습서에서는 활성 Azure 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd0b-111">toocomplete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="fdd0b-112">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdd0b-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="fdd0b-113">자세한 내용은 [Azure 무료 평가판][lnk-free-trial]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fdd0b-113">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="fdd0b-114">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="fdd0b-114">Before you start</span></span>
<span data-ttu-id="fdd0b-115">장치에 대한 코드를 작성하기 전에, 미리 구성된 원격 모니터링 솔루션을 프로비전하고 이 솔루션에 새로운 사용자 지정 장치를 프로비전해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd0b-115">Before you write any code for your device, you must provision your remote monitoring preconfigured solution and provision a new custom device in that solution.</span></span>

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="fdd0b-116">미리 구성된 사용자의 원격 모니터링 솔루션 프로비전</span><span class="sxs-lookup"><span data-stu-id="fdd0b-116">Provision your remote monitoring preconfigured solution</span></span>
<span data-ttu-id="fdd0b-117">hello의 tooan 인스턴스 데이터를 전송 하는이 자습서에서 만드는 hello 장치 [원격 모니터링] [ lnk-remote-monitoring] 솔루션 미리 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd0b-117">hello device you create in this tutorial sends data tooan instance of hello [remote monitoring][lnk-remote-monitoring] preconfigured solution.</span></span> <span data-ttu-id="fdd0b-118">원격 Azure 계정에서 미리 구성 된 솔루션을 모니터링 하는 hello를 프로 비전 이미 하지 않은 경우 단계를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd0b-118">If you haven't already provisioned hello remote monitoring preconfigured solution in your Azure account, use hello following steps:</span></span>

1. <span data-ttu-id="fdd0b-119">Hello에 <https://www.azureiotsuite.com/> 페이지  **+**  toocreate 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="fdd0b-119">On hello <https://www.azureiotsuite.com/> page, click **+** toocreate a solution.</span></span>
2. <span data-ttu-id="fdd0b-120">클릭 **선택** hello에 **원격 모니터링** toocreate 솔루션 패널입니다.</span><span class="sxs-lookup"><span data-stu-id="fdd0b-120">Click **Select** on hello **Remote monitoring** panel toocreate your solution.</span></span>
3. <span data-ttu-id="fdd0b-121">Hello에 **원격 만들 모니터링 솔루션** 페이지에서 입력는 **솔루션 이름** 의 선택한 hello 선택 **지역** , toodeploy 한 hello Azure를 선택 합니다. 구독 toowant toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd0b-121">On hello **Create Remote monitoring solution** page, enter a **Solution name** of your choice, select hello **Region** you want toodeploy to, and select hello Azure subscription toowant toouse.</span></span> <span data-ttu-id="fdd0b-122">그런 다음 **솔루션 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd0b-122">Then click **Create solution**.</span></span>
4. <span data-ttu-id="fdd0b-123">Hello를 프로 비전 프로세스가 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="fdd0b-123">Wait until hello provisioning process completes.</span></span>

> [!WARNING]
> <span data-ttu-id="fdd0b-124">미리 구성 하는 hello 솔루션 청구 가능한 Azure 서비스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd0b-124">hello preconfigured solutions use billable Azure services.</span></span> <span data-ttu-id="fdd0b-125">Tooremove 완료 되 면 구독에서 미리 구성 된 솔루션을 hello 반드시 tooavoid 불필요 한 비용이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdd0b-125">Be sure tooremove hello preconfigured solution from your subscription when you are done with it tooavoid any unnecessary charges.</span></span> <span data-ttu-id="fdd0b-126">Hello를 방문 하 여 구독에서 미리 구성 된 솔루션을 완전히 제거할 수 <https://www.azureiotsuite.com/> 페이지.</span><span class="sxs-lookup"><span data-stu-id="fdd0b-126">You can completely remove a preconfigured solution from your subscription by visiting hello <https://www.azureiotsuite.com/> page.</span></span>
> 
> 

<span data-ttu-id="fdd0b-127">Hello 모니터링 솔루션 원격 hello에 대 한 프로세스를 프로 비전 완료 되 면, 클릭 **시작** 브라우저에서 tooopen hello 솔루션 대시보드 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd0b-127">When hello provisioning process for hello remote monitoring solution finishes, click **Launch** tooopen hello solution dashboard in your browser.</span></span>

![솔루션 대시보드][img-dashboard]

### <a name="provision-your-device-in-hello-remote-monitoring-solution"></a><span data-ttu-id="fdd0b-129">Hello 원격 모니터링 솔루션에서에서 장치를 프로 비전</span><span class="sxs-lookup"><span data-stu-id="fdd0b-129">Provision your device in hello remote monitoring solution</span></span>
> [!NOTE]
> <span data-ttu-id="fdd0b-130">솔루션에 장치가 이미 프로비전되어 있으면 이 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="fdd0b-130">If you have already provisioned a device in your solution, you can skip this step.</span></span> <span data-ttu-id="fdd0b-131">Hello 클라이언트 응용 프로그램을 만들 때 tooknow hello에 대 한 장치 자격 증명이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd0b-131">You need tooknow hello device credentials when you create hello client application.</span></span>
> 
> 

<span data-ttu-id="fdd0b-132">장치 tooconnect toohello 미리 구성 된 솔루션을 식별 해야 합니다 자체 tooIoT 허브 유효한 자격 증명을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd0b-132">For a device tooconnect toohello preconfigured solution, it must identify itself tooIoT Hub using valid credentials.</span></span> <span data-ttu-id="fdd0b-133">Hello 솔루션 대시보드에서 hello 장치 자격 증명을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdd0b-133">You can retrieve hello device credentials from hello solution dashboard.</span></span> <span data-ttu-id="fdd0b-134">이 자습서의 뒷부분에 나오는 클라이언트 응용 프로그램에 hello 장치 자격 증명을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd0b-134">You include hello device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="fdd0b-135">hello 솔루션 대시보드에 전체 hello 다음 단계를 장치 tooyour 원격 모니터링 솔루션 tooadd 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd0b-135">tooadd a device tooyour remote monitoring solution, complete hello following steps in hello solution dashboard:</span></span>

1. <span data-ttu-id="fdd0b-136">Hello 왼쪽 아래 모퉁이의 hello 대시보드, 클릭 **장치 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd0b-136">In hello lower left-hand corner of hello dashboard, click **Add a device**.</span></span>
   
   ![장치 추가][1]
2. <span data-ttu-id="fdd0b-138">Hello에 **사용자 지정 장치** 에서 **새로 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd0b-138">In hello **Custom Device** panel, click **Add new**.</span></span>
   
   ![사용자 지정 장치 추가][2]
3. <span data-ttu-id="fdd0b-140">**직접 나만의 장치 ID 정의**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd0b-140">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="fdd0b-141">같은 장치 ID를 입력 **mydevice**, 클릭 **ID 확인** tooverify 해당 이름을 이미와에 없는 사용 클릭 **만들기** tooprovision hello 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="fdd0b-141">Enter a Device ID such as **mydevice**, click **Check ID** tooverify that name isn't already in use, and then click **Create** tooprovision hello device.</span></span>
   
   ![장치 ID 추가][3]
4. <span data-ttu-id="fdd0b-143">참고 hello 장치 자격 증명 (장치 ID, IoT 허브 호스트 이름 및 장치 키)를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd0b-143">Make a note hello device credentials (Device ID, IoT Hub Hostname, and Device Key).</span></span> <span data-ttu-id="fdd0b-144">클라이언트 응용 프로그램 모니터링 솔루션 원격 이러한 값 tooconnect toohello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd0b-144">Your client application needs these values tooconnect toohello remote monitoring solution.</span></span> <span data-ttu-id="fdd0b-145">**완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd0b-145">Then click **Done**.</span></span>
   
    ![장치 자격 증명 보기][4]
5. <span data-ttu-id="fdd0b-147">Hello 솔루션 대시보드에 hello 장치 목록에서 장치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd0b-147">Select your device in hello device list in hello solution dashboard.</span></span> <span data-ttu-id="fdd0b-148">그런 다음, hello **장치 세부 정보** 에서 **장치 사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd0b-148">Then, in hello **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="fdd0b-149">현재 장치의 hello 상태는 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd0b-149">hello status of your device is now **Running**.</span></span> <span data-ttu-id="fdd0b-150">원격 모니터링 솔루션 hello 수 이제 장치에서 원격 분석을 수신 하 고 hello 장치에서 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd0b-150">hello remote monitoring solution can now receive telemetry from your device and invoke methods on hello device.</span></span>

[img-dashboard]: ./media/iot-suite-selector-connecting/dashboard.png
[1]: ./media/iot-suite-selector-connecting/suite0.png
[2]: ./media/iot-suite-selector-connecting/suite1.png
[3]: ./media/iot-suite-selector-connecting/suite2.png
[4]: ./media/iot-suite-selector-connecting/suite3.png

[lnk-what-are-preconfig-solutions]: ../articles/iot-suite/iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: ../articles/iot-suite/iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/