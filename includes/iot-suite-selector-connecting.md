> [!div class="op_single_selector"]
> * [<span data-ttu-id="5d106-101">Windows에서 C</span><span class="sxs-lookup"><span data-stu-id="5d106-101">C on Windows</span></span>](../articles/iot-suite/iot-suite-connecting-devices.md)
> * [<span data-ttu-id="5d106-102">Linux에서 C</span><span class="sxs-lookup"><span data-stu-id="5d106-102">C on Linux</span></span>](../articles/iot-suite/iot-suite-connecting-devices-linux.md)
> * [<span data-ttu-id="5d106-103">Node.JS</span><span class="sxs-lookup"><span data-stu-id="5d106-103">Node.js</span></span>](../articles/iot-suite/iot-suite-connecting-devices-node.md)
> 
> 

## <a name="scenario-overview"></a><span data-ttu-id="5d106-104">시나리오 개요</span><span class="sxs-lookup"><span data-stu-id="5d106-104">Scenario overview</span></span>
<span data-ttu-id="5d106-105">이 시나리오에서는 원격 모니터링 [미리 구성된 솔루션][lnk-what-are-preconfig-solutions]에 다음과 같은 원격 분석 데이터를 보낼 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5d106-105">In this scenario, you create a device that sends the following telemetry to the remote monitoring [preconfigured solution][lnk-what-are-preconfig-solutions]:</span></span>

* <span data-ttu-id="5d106-106">외부 온도</span><span class="sxs-lookup"><span data-stu-id="5d106-106">External temperature</span></span>
* <span data-ttu-id="5d106-107">내부 온도</span><span class="sxs-lookup"><span data-stu-id="5d106-107">Internal temperature</span></span>
* <span data-ttu-id="5d106-108">습도</span><span class="sxs-lookup"><span data-stu-id="5d106-108">Humidity</span></span>

<span data-ttu-id="5d106-109">간소함을 위하여 장치의 코드가 샘플 값을 생성하지만, 사용자는 자신의 장치에 실제 센서를 연결하고 실제 원격 분석 데이터를 보내어 샘플을 확장할 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="5d106-109">For simplicity, the code on the device generates sample values, but we encourage you to extend the sample by connecting real sensors to your device and sending real telemetry.</span></span>

<span data-ttu-id="5d106-110">장치는 솔루션 대시보드에서 호출된 메서드 및 솔루션 대시보드에 설정된 desired 속성 값에 응답할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d106-110">The device is also able to respond to methods invoked from the solution dashboard and desired property values set in the solution dashboard.</span></span>

<span data-ttu-id="5d106-111">이 자습서를 완료하려면 활성 Azure 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5d106-111">To complete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="5d106-112">계정이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d106-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="5d106-113">자세한 내용은 [Azure 무료 평가판][lnk-free-trial]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5d106-113">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="5d106-114">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="5d106-114">Before you start</span></span>
<span data-ttu-id="5d106-115">장치에 대한 코드를 작성하기 전에, 미리 구성된 원격 모니터링 솔루션을 프로비전하고 이 솔루션에 새로운 사용자 지정 장치를 프로비전해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d106-115">Before you write any code for your device, you must provision your remote monitoring preconfigured solution and provision a new custom device in that solution.</span></span>

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="5d106-116">미리 구성된 사용자의 원격 모니터링 솔루션 프로비전</span><span class="sxs-lookup"><span data-stu-id="5d106-116">Provision your remote monitoring preconfigured solution</span></span>
<span data-ttu-id="5d106-117">이 자습서에서 만드는 장치는 미리 구성된 [원격 모니터링][lnk-remote-monitoring] 솔루션의 인스턴스에 데이터를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="5d106-117">The device you create in this tutorial sends data to an instance of the [remote monitoring][lnk-remote-monitoring] preconfigured solution.</span></span> <span data-ttu-id="5d106-118">Azure 계정에서 미리 구성된 원격 모니터링 솔루션을 미리 프로비전하지 않은 경우 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5d106-118">If you haven't already provisioned the remote monitoring preconfigured solution in your Azure account, use the following steps:</span></span>

1. <span data-ttu-id="5d106-119"><https://www.azureiotsuite.com/> 페이지에서 솔루션을 만들려면 **+**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5d106-119">On the <https://www.azureiotsuite.com/> page, click **+** to create a solution.</span></span>
2. <span data-ttu-id="5d106-120">**원격 모니터링** 패널에서 **선택**을 클릭하여 솔루션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5d106-120">Click **Select** on the **Remote monitoring** panel to create your solution.</span></span>
3. <span data-ttu-id="5d106-121">**원격 모니터링 솔루션 만들기** 페이지에서 선택한 **솔루션 이름**을 입력하고, 배포하려는 **지역**을 선택한 후, 사용하려는 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5d106-121">On the **Create Remote monitoring solution** page, enter a **Solution name** of your choice, select the **Region** you want to deploy to, and select the Azure subscription to want to use.</span></span> <span data-ttu-id="5d106-122">그런 다음 **솔루션 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5d106-122">Then click **Create solution**.</span></span>
4. <span data-ttu-id="5d106-123">프로비전 프로세스가 완료될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="5d106-123">Wait until the provisioning process completes.</span></span>

> [!WARNING]
> <span data-ttu-id="5d106-124">미리 구성된 솔루션에서는 청구 가능한 Azure 서비스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5d106-124">The preconfigured solutions use billable Azure services.</span></span> <span data-ttu-id="5d106-125">불필요한 비용을 방지하기 위해 완료된 후에는 미리 구성된 솔루션을 구독에서 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d106-125">Be sure to remove the preconfigured solution from your subscription when you are done with it to avoid any unnecessary charges.</span></span> <span data-ttu-id="5d106-126"><https://www.azureiotsuite.com/> 페이지를 방문하여 미리 구성된 솔루션을 구독에서 완전히 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d106-126">You can completely remove a preconfigured solution from your subscription by visiting the <https://www.azureiotsuite.com/> page.</span></span>
> 
> 

<span data-ttu-id="5d106-127">원격 모니터링 솔루션의 프로비전 프로세스가 완료되면 **시작** 을 클릭하여 브라우저에서 솔루션 대시보드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5d106-127">When the provisioning process for the remote monitoring solution finishes, click **Launch** to open the solution dashboard in your browser.</span></span>

![솔루션 대시보드][img-dashboard]

### <a name="provision-your-device-in-the-remote-monitoring-solution"></a><span data-ttu-id="5d106-129">원격 모니터링 솔루션에서 장치 프로비전</span><span class="sxs-lookup"><span data-stu-id="5d106-129">Provision your device in the remote monitoring solution</span></span>
> [!NOTE]
> <span data-ttu-id="5d106-130">솔루션에 장치가 이미 프로비전되어 있으면 이 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="5d106-130">If you have already provisioned a device in your solution, you can skip this step.</span></span> <span data-ttu-id="5d106-131">클라이언트 응용 프로그램을 만들 때 장치 자격 증명을 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d106-131">You need to know the device credentials when you create the client application.</span></span>
> 
> 

<span data-ttu-id="5d106-132">미리 구성된 솔루션에 연결하는 장치는 유효한 자격 증명을 사용하여 IoT Hub에 자신을 식별할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d106-132">For a device to connect to the preconfigured solution, it must identify itself to IoT Hub using valid credentials.</span></span> <span data-ttu-id="5d106-133">솔루션 대시보드에서 장치 자격 증명을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d106-133">You can retrieve the device credentials from the solution dashboard.</span></span> <span data-ttu-id="5d106-134">이 자습서의 뒷부분에서는 클라이언트 응용 프로그램에 있는 장치 자격 증명을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5d106-134">You include the device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="5d106-135">원격 모니터링 솔루션에 장치를 추가하려면 솔루션 대시보드에서 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="5d106-135">To add a device to your remote monitoring solution, complete the following steps in the solution dashboard:</span></span>

1. <span data-ttu-id="5d106-136">대시보드의 왼쪽 아래 모서리에서 **장치 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5d106-136">In the lower left-hand corner of the dashboard, click **Add a device**.</span></span>
   
   ![장치 추가][1]
2. <span data-ttu-id="5d106-138">**사용자 지정 장치** 패널에서 **새로 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5d106-138">In the **Custom Device** panel, click **Add new**.</span></span>
   
   ![사용자 지정 장치 추가][2]
3. <span data-ttu-id="5d106-140">**직접 나만의 장치 ID 정의**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5d106-140">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="5d106-141">장치 ID(예: **mydevice**)를 입력하고 **ID 확인**을 클릭하여 해당 이름이 이미 사용되고 있는지 확인한 후 **만들기**를 클릭하여 장치를 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="5d106-141">Enter a Device ID such as **mydevice**, click **Check ID** to verify that name isn't already in use, and then click **Create** to provision the device.</span></span>
   
   ![장치 ID 추가][3]
4. <span data-ttu-id="5d106-143">장치 자격 증명(장치 ID, IoT Hub 호스트 이름 및 장치 키)을 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="5d106-143">Make a note the device credentials (Device ID, IoT Hub Hostname, and Device Key).</span></span> <span data-ttu-id="5d106-144">원격 모니터링 솔루션에 연결하려면 클라이언트 응용 프로그램에 이러한 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5d106-144">Your client application needs these values to connect to the remote monitoring solution.</span></span> <span data-ttu-id="5d106-145">**완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5d106-145">Then click **Done**.</span></span>
   
    ![장치 자격 증명 보기][4]
5. <span data-ttu-id="5d106-147">솔루션 대시보드의 장치 목록에서 장치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5d106-147">Select your device in the device list in the solution dashboard.</span></span> <span data-ttu-id="5d106-148">그런 다음 **장치 세부 정보** 패널에서 **장치 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5d106-148">Then, in the **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="5d106-149">현재 장치 상태는 **실행 중**입니다.</span><span class="sxs-lookup"><span data-stu-id="5d106-149">The status of your device is now **Running**.</span></span> <span data-ttu-id="5d106-150">이제 원격 모니터링 솔루션은 장치에서 원격 분석을 수신하고 장치에서 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d106-150">The remote monitoring solution can now receive telemetry from your device and invoke methods on the device.</span></span>

[img-dashboard]: ./media/iot-suite-selector-connecting/dashboard.png
[1]: ./media/iot-suite-selector-connecting/suite0.png
[2]: ./media/iot-suite-selector-connecting/suite1.png
[3]: ./media/iot-suite-selector-connecting/suite2.png
[4]: ./media/iot-suite-selector-connecting/suite3.png

[lnk-what-are-preconfig-solutions]: ../articles/iot-suite/iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: ../articles/iot-suite/iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/