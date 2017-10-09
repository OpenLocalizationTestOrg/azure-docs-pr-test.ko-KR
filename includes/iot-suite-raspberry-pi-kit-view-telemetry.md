## <a name="view-hello-telemetry"></a><span data-ttu-id="72306-101">Hello 원격 분석 보기</span><span class="sxs-lookup"><span data-stu-id="72306-101">View hello telemetry</span></span>

<span data-ttu-id="72306-102">이제 hello 라스베리 Pi 원격 분석 toohello 원격 모니터링 솔루션을 보내는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="72306-102">hello Raspberry Pi is now sending telemetry toohello remote monitoring solution.</span></span> <span data-ttu-id="72306-103">Hello 솔루션 대시보드에서 hello 원격 분석을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72306-103">You can view hello telemetry on hello solution dashboard.</span></span> <span data-ttu-id="72306-104">Hello 솔루션 대시보드에서 메시지 tooyour 라스베리 Pi를 보낼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72306-104">You can also send messages tooyour Raspberry Pi from hello solution dashboard.</span></span>

- <span data-ttu-id="72306-105">Toohello 솔루션 대시보드를 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="72306-105">Navigate toohello solution dashboard.</span></span>
- <span data-ttu-id="72306-106">Hello에 장치를 선택 합니다. **장치 tooView** 드롭다운입니다.</span><span class="sxs-lookup"><span data-stu-id="72306-106">Select your device in hello **Device tooView** dropdown.</span></span>
- <span data-ttu-id="72306-107">hello에서 hello 원격 분석 라스베리 Pi hello 대시보드에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72306-107">hello telemetry from hello Raspberry Pi displays on hello dashboard.</span></span>

![Hello 라스베리 Pi에서에서 원격 분석 표시][img-telemetry-display]

## <a name="act-on-hello-device"></a><span data-ttu-id="72306-109">Hello 장치에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="72306-109">Act on hello device</span></span>

<span data-ttu-id="72306-110">Hello 솔루션 대시보드에서 라스베리 원주율 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72306-110">From hello solution dashboard, you can invoke methods on your Raspberry Pi.</span></span> <span data-ttu-id="72306-111">Hello 라스베리 Pi toohello 원격 모니터링 솔루션에 연결 되 면 지원 hello 방법에 대 한 정보를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="72306-111">When hello Raspberry Pi connects toohello remote monitoring solution, it sends information about hello methods it supports.</span></span>

- <span data-ttu-id="72306-112">Hello 솔루션 대시보드 클릭 **장치** toovisit hello **장치** 페이지.</span><span class="sxs-lookup"><span data-stu-id="72306-112">In hello solution dashboard, click **Devices** toovisit hello **Devices** page.</span></span> <span data-ttu-id="72306-113">Hello에 라스베리 Pi 선택 **장치 목록**합니다.</span><span class="sxs-lookup"><span data-stu-id="72306-113">Select your Raspberry Pi in hello **Device List**.</span></span> <span data-ttu-id="72306-114">그런 다음 **메서드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="72306-114">Then choose **Methods**:</span></span>

    ![대시보드에서 장치 나열][img-list-devices]

- <span data-ttu-id="72306-116">Hello에 **메서드 호출** 페이지에서 선택 **LightBlink** hello에 **메서드** 드롭다운입니다.</span><span class="sxs-lookup"><span data-stu-id="72306-116">On hello **Invoke Method** page, choose **LightBlink** in hello **Method** dropdown.</span></span>

- <span data-ttu-id="72306-117">**InvokeMethod**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="72306-117">Choose **InvokeMethod**.</span></span> <span data-ttu-id="72306-118">hello LED 연결 toohello 라스베리 Pi 여러 번 깜박입니다.</span><span class="sxs-lookup"><span data-stu-id="72306-118">hello LED connected toohello Raspberry Pi flashes several times.</span></span> <span data-ttu-id="72306-119">hello 응용 프로그램에 액세스 hello 라스베리 Pi 승인 백 toohello 솔루션 대시보드를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="72306-119">hello app on hello Raspberry Pi sends an acknowledgment back toohello solution dashboard:</span></span>

    ![메서드 기록 표시][img-method-history]

- <span data-ttu-id="72306-121">전환할 수 있습니다 hello LED 켜고 hello를 사용 하 여 **ChangeLightStatus** 메서드는 **LightStatusValue** 도**1** 에 대 한에 또는 **0** 에 대 한 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="72306-121">You can switch hello LED on and off using hello **ChangeLightStatus** method with a **LightStatusValue** set too**1** for on or **0** for off.</span></span>

> [!WARNING]
> <span data-ttu-id="72306-122">Hello를 모니터링 하 여 Azure 계정에서 실행 되는 솔루션 원격 두면 실행 hello 시간에 대 한 요금이 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="72306-122">If you leave hello remote monitoring solution running in your Azure account, you are billed for hello time it runs.</span></span> <span data-ttu-id="72306-123">Hello 원격 솔루션 실행을 모니터링 하는 동안 소비 감소 하는 방법에 대 한 자세한 내용은 참조 [데모 목적에 대 한 솔루션을 미리 구성 된 Azure IoT Suite 구성][lnk-demo-config]합니다.</span><span class="sxs-lookup"><span data-stu-id="72306-123">For more information about reducing consumption while hello remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="72306-124">사용을 마쳤으면 Azure 계정에서 hello 미리 구성 된 솔루션을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="72306-124">Delete hello preconfigured solution from your Azure account when you have finished using it.</span></span>


[img-telemetry-display]: media/iot-suite-raspberry-pi-kit-view-telemetry/telemetry.png
[img-list-devices]: media/iot-suite-raspberry-pi-kit-view-telemetry/listdevices.png
[img-method-history]: media/iot-suite-raspberry-pi-kit-view-telemetry/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md