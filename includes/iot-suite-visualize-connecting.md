## <a name="view-device-telemetry-in-hello-dashboard"></a><span data-ttu-id="ff255-101">Hello 대시보드에 장치 원격 분석 보기</span><span class="sxs-lookup"><span data-stu-id="ff255-101">View device telemetry in hello dashboard</span></span>
<span data-ttu-id="ff255-102">hello 대시보드에서 hello 원격 tooview hello 원격 장치 보내기 tooIoT 허브 솔루션 사용을 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff255-102">hello dashboard in hello remote monitoring solution enables you tooview hello telemetry your devices send tooIoT Hub.</span></span>

1. <span data-ttu-id="ff255-103">반환 toohello 원격 모니터링 솔루션 대시보드를 브라우저에서 클릭 **장치** hello 왼쪽 패널 toonavigate toohello에 **장치 목록**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff255-103">In your browser, return toohello remote monitoring solution dashboard, click **Devices** in hello left-hand panel toonavigate toohello **Devices list**.</span></span>
2. <span data-ttu-id="ff255-104">Hello에 **장치 목록**, 장치의 hello 상태 인지 표시 되어야 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff255-104">In hello **Devices list**, you should see that hello status of your device is **Running**.</span></span> <span data-ttu-id="ff255-105">그렇지 않은 경우 클릭 **장치 사용** hello에 **장치 세부 정보** 패널입니다.</span><span class="sxs-lookup"><span data-stu-id="ff255-105">If not, click **Enable Device** in hello **Device Details** panel.</span></span>
   
    ![장치 상태 보기][18]
3. <span data-ttu-id="ff255-107">클릭 **대시보드** tooreturn toohello 대시보드 hello에 장치를 선택 합니다. **장치 tooView** 드롭 다운 tooview 해당 원격 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff255-107">Click **Dashboard** tooreturn toohello dashboard, select your device in hello **Device tooView** drop-down tooview its telemetry.</span></span> <span data-ttu-id="ff255-108">hello 샘플 응용 프로그램에서 hello 원격 분석 내부 온도 대 한 50 단위, 55 단위 외부 온도 및 습도에 50 명의 단위 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff255-108">hello telemetry from hello sample application is 50 units for internal temperature, 55 units for external temperature, and 50 units for humidity.</span></span>
   
    ![장치 원격 분석 보기][img-telemetry]

## <a name="invoke-a-method-on-your-device"></a><span data-ttu-id="ff255-110">장치에서 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="ff255-110">Invoke a method on your device</span></span>
<span data-ttu-id="ff255-111">hello 원격 모니터링 솔루션에서 hello 대시보드 IoT 허브를 사용 하 여 장치의 tooinvoke 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff255-111">hello dashboard in hello remote monitoring solution enables you tooinvoke methods on your devices through IoT Hub.</span></span> <span data-ttu-id="ff255-112">예를 들어 hello 모니터링 솔루션 원격 장치를 다시 부팅 메서드 toosimulate를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff255-112">For example, in hello remote monitoring solution you can invoke a method toosimulate rebooting a device.</span></span>

1. <span data-ttu-id="ff255-113">Hello 원격 모니터링 솔루션 대시보드에 클릭 **장치** hello 왼쪽 패널 toonavigate toohello에 **장치 목록**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff255-113">In hello remote monitoring solution dashboard, click **Devices** in hello left-hand panel toonavigate toohello **Devices list**.</span></span>
2. <span data-ttu-id="ff255-114">클릭 **장치 ID** hello에 장치에 대 한 **장치 목록**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff255-114">Click **Device ID** for your device in hello **Devices list**.</span></span>
3. <span data-ttu-id="ff255-115">Hello에 **장치 세부 정보** 에서 **메서드**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff255-115">In hello **Device details** panel, click **Methods**.</span></span>
   
    ![장치 메서드][13]
4. <span data-ttu-id="ff255-117">Hello에 **메서드** 드롭다운 목록에서 선택 **InitiateFirmwareUpdate**, 한 다음 **FWPACKAGEURI** 더미 URL을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff255-117">In hello **Method** drop-down, select **InitiateFirmwareUpdate**, and then in **FWPACKAGEURI** enter a dummy URL.</span></span> <span data-ttu-id="ff255-118">클릭 **메서드 호출** hello 장치에서 toocall hello 메서드.</span><span class="sxs-lookup"><span data-stu-id="ff255-118">Click **Invoke Method** toocall hello method on hello device.</span></span>
   
    ![장치 메서드 호출][14]
   

5. <span data-ttu-id="ff255-120">Hello 장치 hello 메서드를 처리할 때 장치 코드를 실행 하는 hello 콘솔에 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff255-120">You see a message in hello console running your device code when hello device handles hello method.</span></span> <span data-ttu-id="ff255-121">hello 메서드의 hello 결과 hello 솔루션 포털에서 toohello 기록을 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff255-121">hello results of hello method are added toohello history in hello solution portal:</span></span>

    ![메서드 기록 보기][img-method-history]

## <a name="next-steps"></a><span data-ttu-id="ff255-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ff255-123">Next steps</span></span>
<span data-ttu-id="ff255-124">hello 문서 [사용자 지정 솔루션을 미리 구성 된] [ lnk-customize] 이 샘플을 확장 하는 몇 가지 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff255-124">hello article [Customizing preconfigured solutions][lnk-customize] describes some ways you can extend this sample.</span></span> <span data-ttu-id="ff255-125">가능한 확장에는 실제 센서 사용 및 추가적인 명령 구현이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff255-125">Possible extensions include using real sensors and implementing additional commands.</span></span>

<span data-ttu-id="ff255-126">Hello에 대 한 자세히 알아볼 수 있습니다 [hello azureiotsuite.com 사이트에 대 한 권한을][lnk-permissions]합니다.</span><span class="sxs-lookup"><span data-stu-id="ff255-126">You can learn more about hello [permissions on hello azureiotsuite.com site][lnk-permissions].</span></span>

[13]: ./media/iot-suite-visualize-connecting/suite4.png
[14]: ./media/iot-suite-visualize-connecting/suite7-1.png
[18]: ./media/iot-suite-visualize-connecting/suite10.png
[img-telemetry]: ./media/iot-suite-visualize-connecting/telemetry.png
[img-method-history]: ./media/iot-suite-visualize-connecting/history.png
[lnk-customize]: ../articles/iot-suite/iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-permissions]: ../articles/iot-suite/iot-suite-permissions.md
