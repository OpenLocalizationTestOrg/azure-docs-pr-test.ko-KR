> [!div class="op_single_selector"]
> * [<span data-ttu-id="26ccd-101">Node.JS</span><span class="sxs-lookup"><span data-stu-id="26ccd-101">Node.js</span></span>](../articles/iot-hub/iot-hub-node-node-twin-how-to-configure.md)
> * [<span data-ttu-id="26ccd-102">C#/Node.js</span><span class="sxs-lookup"><span data-stu-id="26ccd-102">C#/Node.js</span></span>](../articles/iot-hub/iot-hub-csharp-node-twin-how-to-configure.md)
> * [<span data-ttu-id="26ccd-103">C#</span><span class="sxs-lookup"><span data-stu-id="26ccd-103">C#</span></span>](../articles/iot-hub/iot-hub-csharp-csharp-twin-how-to-configure.md)
> 
> 

## <a name="introduction"></a><span data-ttu-id="26ccd-104">소개</span><span class="sxs-lookup"><span data-stu-id="26ccd-104">Introduction</span></span>

<span data-ttu-id="26ccd-105">[IoT Hub 장치 트윈스 시작][lnk-twin-tutorial]를 사용 하 여 tooset 장치 메타 데이터에서 다시 솔루션을 종료 하는 방법을 알아보았습니다 *태그*, 장치 앱에서 장치 조건을 보고 사용 하 여 *속성을 보고*, 및 SQL 유사 언어를 사용 하 여이 정보를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="26ccd-105">In [Get started with IoT Hub device twins][lnk-twin-tutorial], you learned how tooset device metadata from your solution back end using *tags*, report device conditions from a device app using *reported properties*, and query this information using a SQL-like language.</span></span>

<span data-ttu-id="26ccd-106">이 자습서에 설명 합니다 방법을 toouse hello hello 장치로 이중의 *원하는 속성을* 와 함께 *속성을 보고*, tooremotely 장치 앱을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="26ccd-106">In this tutorial, you will learn how toouse hello hello device twin's *desired properties* along with *reported properties*, tooremotely configure device apps.</span></span> <span data-ttu-id="26ccd-107">보다 구체적으로, 장치로 이중 보고 하는 방법을 보여 주는이 자습서 및 원하는 속성 장치 응용 프로그램의 여러 단계 구성을 사용 하도록 설정 하 고 모든 장치에서 hello 가시성 toohello 솔루션의 백 엔드가이 작업의 hello 상태를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="26ccd-107">More specifically, this tutorial shows how a device twin's reported and desired properties enable a multi-step configuration of a device application, and provide hello visibility toohello solution back end of hello status of this operation across all devices.</span></span> <span data-ttu-id="26ccd-108">장치 구성의 hello 역할에 대 한 자세한 정보를 찾을 수 있습니다 [IoT Hub와 장치 관리의 개요][lnk-dm-overview]합니다.</span><span class="sxs-lookup"><span data-stu-id="26ccd-108">You can find more information regarding hello role of device configurations in [Overview of device management with IoT Hub][lnk-dm-overview].</span></span>

<span data-ttu-id="26ccd-109">상위 수준 트윈스 장치를 사용 하 여 구성할 수 있도록 hello 솔루션 백 엔드 toospecify hello 원하는 특정 명령을 전송 하는 대신 hello 관리 되는 장치에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="26ccd-109">At a high level, using device twins enables hello solution back end toospecify hello desired configuration for hello managed devices, instead of sending specific commands.</span></span> <span data-ttu-id="26ccd-110">이렇게 하면 추가 구성을 설정 하는 가장 좋은 방법은 tooupdate hello 해당 (매우 소중한 자료 특정 장치 조건은 hello 특정 명령을 tooimmediately 전달 하는 기능에 영향을 여기서 IoT 시나리오에서)을 담당 hello 장치 toohello 지속적으로 보고 하는 동안 솔루션 다시 끝 hello 현재 상태와 hello 업데이트 프로세스의 잠재적 오류 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="26ccd-110">This puts hello device in charge of setting up hello best way tooupdate its configuration (very important in IoT scenarios where specific device conditions affect hello ability tooimmediately carry out specific commands), while continually reporting toohello solution back end hello current state and potential error conditions of hello update process.</span></span> <span data-ttu-id="26ccd-111">이 패턴은 큰 장치 집합의 계측 toohello 관리 hello 솔루션 백 엔드 toohave 전체의 표시 유형을 hello 상태 hello 구성 프로세스의 모든 장치에서 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="26ccd-111">This pattern is instrumental toohello management of large sets of devices, as it enables hello solution back end toohave full visibility of hello state of hello configuration process across all devices.</span></span>

> [!NOTE]
> <span data-ttu-id="26ccd-112">장치가 좀 더 대화형 방식으로 제어되는 시나리오(예: 사용자 제어 앱에서 팬 켜기)에서는 [직접 메서드][lnk-methods] 사용을 고려하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="26ccd-112">In scenarios where devices are controlled in a more interactive fashion (turn on a fan from a user-controlled app), consider using [direct methods][lnk-methods].</span></span>
> 
> 

<span data-ttu-id="26ccd-113">이 자습서에서는 hello 솔루션 백 엔드 변경 hello 원격 분석 구성의 대상 장치를 하는 hello 장치 응용 프로그램의 결과로 여러 단계의 프로세스가 tooapply 구성 따릅니다 (예: 소프트웨어 모듈을 다시 시작이 필요한 업데이트 자습서 간단한 지연 시간 시뮬레이션) 합니다.</span><span class="sxs-lookup"><span data-stu-id="26ccd-113">In this tutorial, hello solution back end changes hello telemetry configuration of a target device and, as a result of that, hello device app follows a multi-step process tooapply a configuration update (for example, requiring a software module restart, which this tutorial simulates with a simple delay).</span></span>

<span data-ttu-id="26ccd-114">hello 솔루션 백 엔드 hello 구성 방법은 다음 hello에 hello 장치로 이중의 원하는 속성에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="26ccd-114">hello solution back end stores hello configuration in hello device twin's desired properties in hello following way:</span></span>

        {
            ...
            "properties": {
                ...
                "desired": {
                    "telemetryConfig": {
                        "configId": "{id of hello configuration}",
                        "sendFrequency": "{config}"
                    }
                }
                ...
            }
            ...
        }

> [!NOTE]
> <span data-ttu-id="26ccd-115">구성은 복잡 한 일 수 있으므로 일반적으로 배정 된 고유 id (해시 또는 [Guid][lnk-guid]) toosimplify 자신의 비교 합니다.</span><span class="sxs-lookup"><span data-stu-id="26ccd-115">Since configurations can be complex objects, they are usually assigned unique ids (hashes or [GUIDs][lnk-guid]) toosimplify their comparisons.</span></span>
> 
> 

<span data-ttu-id="26ccd-116">hello 장치 응용 프로그램의 현재 구성을 보고 필요한 hello 속성 미러링 **telemetryConfig** hello에 속성을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="26ccd-116">hello device app reports its current configuration mirroring hello desired property **telemetryConfig** in hello reported properties:</span></span>

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of hello current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Success",
                    }
                }
                ...
            }
        }

<span data-ttu-id="26ccd-117">Hello 보고 하는 방법을 **telemetryConfig** 에 추가 속성 **상태**, tooreport hello 상태의 hello 구성 업데이트 프로세스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="26ccd-117">Note how hello reported **telemetryConfig** has an additional property **status**, used tooreport hello state of hello configuration update process.</span></span>

<span data-ttu-id="26ccd-118">원하는 새 구성 수신 되 면 hello 장치 앱 hello 정보를 변경 하 여 보류 중인 구성을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="26ccd-118">When a new desired configuration is received, hello device app reports a pending configuration by changing hello information:</span></span>

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of hello current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Pending",
                        "pendingConfig": {
                            "changeId": "{id of hello pending configuration}",
                            "sendFrequency": "{pending configuration}"
                        }
                    }
                }
                ...
            }
        }

<span data-ttu-id="26ccd-119">그런 다음 일정 시간 후에 hello 장치 앱 됩니다 hello 성공 또는 실패 보고이 작업의 속성 위에 hello를 업데이트 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="26ccd-119">Then, at some later time, hello device app will report hello success or failure of this operation by updating hello above property.</span></span>
<span data-ttu-id="26ccd-120">언제 든 지 모든 hello 장치에서 hello 구성 프로세스의 tooquery hello 상태 hello 솔루션 백 엔드가 수, 어떻게 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="26ccd-120">Note how hello solution back end is able, at any time, tooquery hello status of hello configuration process across all hello devices.</span></span>

<span data-ttu-id="26ccd-121">이 자습서에서는 다음을 수행하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="26ccd-121">This tutorial shows you how to:</span></span>

* <span data-ttu-id="26ccd-122">Hello 솔루션 백 엔드에서 구성 업데이트를 받아으로 여러 업데이트를 보고 하는 시뮬레이션 된 장치 앱 만들기 *속성을 보고* hello 구성 프로세스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="26ccd-122">Create a simulated device app that receives configuration updates from hello solution back end, and reports multiple updates as *reported properties* on hello configuration update process.</span></span>
* <span data-ttu-id="26ccd-123">백 엔드 응용 프로그램 업데이트 hello 원하는 장치를 구성 하 고 다음 쿼리 hello 구성 업데이트 프로세스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="26ccd-123">Create a back-end app that updates hello desired configuration of a device, and then queries hello configuration update process.</span></span>

<!-- links -->

[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: ../articles/iot-hub/iot-hub-device-management-overview.md
[lnk-twin-tutorial]: ../articles/iot-hub/iot-hub-node-node-twin-getstarted.md
[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier
