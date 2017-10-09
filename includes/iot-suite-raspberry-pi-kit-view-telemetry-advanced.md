## <a name="view-hello-telemetry"></a><span data-ttu-id="27500-101">Hello 원격 분석 보기</span><span class="sxs-lookup"><span data-stu-id="27500-101">View hello telemetry</span></span>

<span data-ttu-id="27500-102">이제 hello 라스베리 Pi 원격 분석 toohello 원격 모니터링 솔루션을 보내는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="27500-102">hello Raspberry Pi is now sending telemetry toohello remote monitoring solution.</span></span> <span data-ttu-id="27500-103">Hello 솔루션 대시보드에서 hello 원격 분석을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27500-103">You can view hello telemetry on hello solution dashboard.</span></span> <span data-ttu-id="27500-104">Hello 솔루션 대시보드에서 메시지 tooyour 라스베리 Pi를 보낼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27500-104">You can also send messages tooyour Raspberry Pi from hello solution dashboard.</span></span>

- <span data-ttu-id="27500-105">Toohello 솔루션 대시보드를 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="27500-105">Navigate toohello solution dashboard.</span></span>
- <span data-ttu-id="27500-106">Hello에 장치를 선택 합니다. **장치 tooView** 드롭다운입니다.</span><span class="sxs-lookup"><span data-stu-id="27500-106">Select your device in hello **Device tooView** dropdown.</span></span>
- <span data-ttu-id="27500-107">hello에서 hello 원격 분석 라스베리 Pi hello 대시보드에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="27500-107">hello telemetry from hello Raspberry Pi displays on hello dashboard.</span></span>

![Hello 라스베리 Pi에서에서 원격 분석 표시][img-telemetry-display]

## <a name="initiate-hello-firmware-update"></a><span data-ttu-id="27500-109">Hello 펌웨어 업데이트를 시작</span><span class="sxs-lookup"><span data-stu-id="27500-109">Initiate hello firmware update</span></span>

<span data-ttu-id="27500-110">hello 펌웨어 업데이트 프로세스 다운로드 하 고 hello 라스베리 Pi에 hello 장치 클라이언트 응용 프로그램의 업데이트 된 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="27500-110">hello firmware update process downloads and installs an updated version of hello device client application on hello Raspberry Pi.</span></span> <span data-ttu-id="27500-111">Hello 펌웨어 업데이트 프로세스에 대 한 자세한 내용은 hello 펌웨어 업데이트 패턴의 hello 설명 참조 [IoT Hub와 장치 관리의 개요][lnk-update-pattern]합니다.</span><span class="sxs-lookup"><span data-stu-id="27500-111">For more information about hello firmware update process, see hello description of hello firmware update pattern in [Overview of device management with IoT Hub][lnk-update-pattern].</span></span>

<span data-ttu-id="27500-112">Hello 장치에 대 한 메서드를 호출 하 여 hello 펌웨어 업데이트 프로세스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="27500-112">You initiate hello firmware update process by invoking a method on hello device.</span></span> <span data-ttu-id="27500-113">이 메서드는 비동기적 이며 하 고 hello 업데이트 프로세스가 시작 되는 즉시 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="27500-113">This method is asynchronous, and returns as soon as hello update process begins.</span></span> <span data-ttu-id="27500-114">hello 장치 사용 하 여 hello 업데이트 hello 진행률에 대 한 속성 toonotify hello 솔루션을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="27500-114">hello device uses reported properties toonotify hello solution about hello progress of hello update.</span></span>

<span data-ttu-id="27500-115">Hello 솔루션 대시보드에서 라스베리 원주율 프로그램 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="27500-115">You invoke methods on your Raspberry Pi from hello solution dashboard.</span></span> <span data-ttu-id="27500-116">Hello 라스베리 Pi toohello 원격 모니터링 솔루션을 처음 연결 되 면 지원 hello 방법에 대 한 정보를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="27500-116">When hello Raspberry Pi first connects toohello remote monitoring solution, it sends information about hello methods it supports.</span></span> 

[img-telemetry-display]: media/iot-suite-raspberry-pi-kit-view-telemetry-advanced/telemetry.png
[lnk-update-pattern]: ../articles/iot-hub/iot-hub-device-management-overview.md
