## <a name="view-the-telemetry"></a><span data-ttu-id="5915f-101">원격 분석 보기</span><span class="sxs-lookup"><span data-stu-id="5915f-101">View the telemetry</span></span>

<span data-ttu-id="5915f-102">이제 Raspberry Pi는 원격 분석을 원격 모니터링 솔루션으로 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="5915f-102">The Raspberry Pi is now sending telemetry to the remote monitoring solution.</span></span> <span data-ttu-id="5915f-103">솔루션 대시보드에서 원격 분석을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5915f-103">You can view the telemetry on the solution dashboard.</span></span> <span data-ttu-id="5915f-104">솔루션 대시보드에서 Raspberry Pi로 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5915f-104">You can also send messages to your Raspberry Pi from the solution dashboard.</span></span>

- <span data-ttu-id="5915f-105">솔루션 대시보드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5915f-105">Navigate to the solution dashboard.</span></span>
- <span data-ttu-id="5915f-106">**볼 장치** 드롭다운에서 장치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5915f-106">Select your device in the **Device to View** dropdown.</span></span>
- <span data-ttu-id="5915f-107">Raspberry Pi의 원격 분석은 대시보드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5915f-107">The telemetry from the Raspberry Pi displays on the dashboard.</span></span>

![Raspberry Pi의 원격 분석 표시][img-telemetry-display]

## <a name="act-on-the-device"></a><span data-ttu-id="5915f-109">장치에 대한 작업</span><span class="sxs-lookup"><span data-stu-id="5915f-109">Act on the device</span></span>

<span data-ttu-id="5915f-110">솔루션 대시보드에서 Raspberry Pi에 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5915f-110">From the solution dashboard, you can invoke methods on your Raspberry Pi.</span></span> <span data-ttu-id="5915f-111">Raspberry Pi가 원격 모니터링 솔루션에 연결되는 경우 지원되는 메서드에 대한 정보를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="5915f-111">When the Raspberry Pi connects to the remote monitoring solution, it sends information about the methods it supports.</span></span>

- <span data-ttu-id="5915f-112">솔루션 대시보드에서 **장치**를 클릭하여 **장치** 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5915f-112">In the solution dashboard, click **Devices** to visit the **Devices** page.</span></span> <span data-ttu-id="5915f-113">**장치 목록**에서 Raspberry Pi를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5915f-113">Select your Raspberry Pi in the **Device List**.</span></span> <span data-ttu-id="5915f-114">그런 다음 **메서드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5915f-114">Then choose **Methods**:</span></span>

    ![대시보드에서 장치 나열][img-list-devices]

- <span data-ttu-id="5915f-116">**메서드 호출** 페이지의 **메서드** 드롭다운에서 **LightBlink**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5915f-116">On the **Invoke Method** page, choose **LightBlink** in the **Method** dropdown.</span></span>

- <span data-ttu-id="5915f-117">**InvokeMethod**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5915f-117">Choose **InvokeMethod**.</span></span> <span data-ttu-id="5915f-118">시뮬레이터는 Raspberry Pi의 콘솔에 메시지를 인쇄합니다.</span><span class="sxs-lookup"><span data-stu-id="5915f-118">The simulator prints a message in the console on the Raspberry Pi.</span></span> <span data-ttu-id="5915f-119">Raspberry Pi의 앱은 솔루션 대시보드로 승인 메시지를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="5915f-119">The app on the Raspberry Pi sends an acknowledgment back to the solution dashboard:</span></span>

    ![메서드 기록 표시][img-method-history]

- <span data-ttu-id="5915f-121">**LightStatusValue**를 사용하려면 **1**, 해제하려면 **0**으로 설정하는 **ChangeLightStatus** 메서드를 사용하여 LED 켜기 및 끄기를 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5915f-121">You can switch the LED on and off using the **ChangeLightStatus** method with a **LightStatusValue** set to **1** for on or **0** for off.</span></span>

> [!WARNING]
> <span data-ttu-id="5915f-122">Azure 계정에서 원격 모니터링 솔루션을 실행하는 경우 실행하는 동안 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="5915f-122">If you leave the remote monitoring solution running in your Azure account, you are billed for the time it runs.</span></span> <span data-ttu-id="5915f-123">원격 모니터링 솔루션이 실행되는 동안 소비를 감소하는 방법에 대한 자세한 내용은 [데모 목적으로 미리 구성된 Azure IoT Suite 솔루션 구성][lnk-demo-config]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5915f-123">For more information about reducing consumption while the remote monitoring solution runs, see [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config].</span></span> <span data-ttu-id="5915f-124">사용을 마친 경우 Azure 계정에서 미리 구성된 솔루션을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="5915f-124">Delete the preconfigured solution from your Azure account when you have finished using it.</span></span>


[img-telemetry-display]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/telemetry.png
[img-list-devices]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/listdevices.png
[img-method-history]: media/iot-suite-raspberry-pi-kit-view-telemetry-simulator/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md