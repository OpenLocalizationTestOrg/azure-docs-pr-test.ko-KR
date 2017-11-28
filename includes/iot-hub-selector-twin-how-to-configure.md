> [!div class="op_single_selector"]
> * [<span data-ttu-id="ac947-101">Node.JS</span><span class="sxs-lookup"><span data-stu-id="ac947-101">Node.js</span></span>](../articles/iot-hub/iot-hub-node-node-twin-how-to-configure.md)
> * [<span data-ttu-id="ac947-102">C#/Node.js</span><span class="sxs-lookup"><span data-stu-id="ac947-102">C#/Node.js</span></span>](../articles/iot-hub/iot-hub-csharp-node-twin-how-to-configure.md)
> * [<span data-ttu-id="ac947-103">C#</span><span class="sxs-lookup"><span data-stu-id="ac947-103">C#</span></span>](../articles/iot-hub/iot-hub-csharp-csharp-twin-how-to-configure.md)
> 
> 

## <a name="introduction"></a><span data-ttu-id="ac947-104">소개</span><span class="sxs-lookup"><span data-stu-id="ac947-104">Introduction</span></span>

<span data-ttu-id="ac947-105">[IoT Hub 장치 쌍 시작][lnk-twin-tutorial]에서 *태그*를 사용하여 솔루션 백 엔드에서 장치 메타데이터를 설정하고, *보고된 속성*을 사용하여 장치 앱에서 장치 조건을 보고하며, SQL 유사 언어를 사용하여 이 정보를 쿼리하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="ac947-105">In [Get started with IoT Hub device twins][lnk-twin-tutorial], you learned how to set device metadata from your solution back end using *tags*, report device conditions from a device app using *reported properties*, and query this information using a SQL-like language.</span></span>

<span data-ttu-id="ac947-106">이 자습서에서는 장치 앱을 원격으로 구성하기 위해 장치 쌍의 *desired 속성*을 *reported 속성*과 함께 사용하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ac947-106">In this tutorial, you will learn how to use the the device twin's *desired properties* along with *reported properties*, to remotely configure device apps.</span></span> <span data-ttu-id="ac947-107">더 구체적으로 말하자면, 이 자습서에서는 장치 쌍의 reported 및 desired 속성이 장치 응용 프로그램의 다중 구성을 사용하도록 설정하는 방법을 보여주고 모든 장치에서 이 작업 상태의 솔루션 백 엔드에 대한 가시성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ac947-107">More specifically, this tutorial shows how a device twin's reported and desired properties enable a multi-step configuration of a device application, and provide the visibility to the solution back end of the status of this operation across all devices.</span></span> <span data-ttu-id="ac947-108">장치 구성의 역할과 관련된 자세한 내용은 [IoT Hub를 사용한 장치 관리 개요][lnk-dm-overview]에서 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac947-108">You can find more information regarding the role of device configurations in [Overview of device management with IoT Hub][lnk-dm-overview].</span></span>

<span data-ttu-id="ac947-109">높은 수준에서 장치 쌍을 사용하면 솔루션 백 엔드가 특정 명령을 전송하는 대신 관리되는 장치에 대해 원하는 구성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac947-109">At a high level, using device twins enables the solution back end to specify the desired configuration for the managed devices, instead of sending specific commands.</span></span> <span data-ttu-id="ac947-110">이렇게 하면 업데이트 프로세스의 현재 상태와 잠재적인 오류 조건을 지속적으로 솔루션 백 엔드에 보고하는 한편 장치가 해당 구성을 업데이트하는 가장 좋은 방법을 설정하는 역할을 담당하게 됩니다. 이는 특정 장치 조건이 특정 명령을 즉시 수행하는 능력에 영향을 미치는 IoT 시나리오에서 매우 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="ac947-110">This puts the device in charge of setting up the best way to update its configuration (very important in IoT scenarios where specific device conditions affect the ability to immediately carry out specific commands), while continually reporting to the solution back end the current state and potential error conditions of the update process.</span></span> <span data-ttu-id="ac947-111">이 패턴은 솔루션 백 엔드가 모든 장치에 대한 구성 프로세스 상태의 전체 가시성을 갖도록 설정되어 있어 대량의 장치 집합을 관리하는데 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="ac947-111">This pattern is instrumental to the management of large sets of devices, as it enables the solution back end to have full visibility of the state of the configuration process across all devices.</span></span>

> [!NOTE]
> <span data-ttu-id="ac947-112">장치가 좀 더 대화형 방식으로 제어되는 시나리오(예: 사용자 제어 앱에서 팬 켜기)에서는 [직접 메서드][lnk-methods] 사용을 고려하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ac947-112">In scenarios where devices are controlled in a more interactive fashion (turn on a fan from a user-controlled app), consider using [direct methods][lnk-methods].</span></span>
> 
> 

<span data-ttu-id="ac947-113">이 자습서에서 솔루션 백 엔드는 대상 장치의 원격 분석 구성을 변경하며, 그 결과, 장치 앱은 구성 업데이트를 적용하기 위해 다중 단계 프로세스를 따릅니다. 예를 들어 소프트웨어 모듈 다시 시작과 같은 요구 사항을 이 자습서에서는 간단한 지연으로 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="ac947-113">In this tutorial, the solution back end changes the telemetry configuration of a target device and, as a result of that, the device app follows a multi-step process to apply a configuration update (for example, requiring a software module restart, which this tutorial simulates with a simple delay).</span></span>

<span data-ttu-id="ac947-114">솔루션 백 엔드는 장치 쌍의 필요한 속성에 들어 있는 구성을 다음과 같은 방식으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ac947-114">The solution back end stores the configuration in the device twin's desired properties in the following way:</span></span>

        {
            ...
            "properties": {
                ...
                "desired": {
                    "telemetryConfig": {
                        "configId": "{id of the configuration}",
                        "sendFrequency": "{config}"
                    }
                }
                ...
            }
            ...
        }

> [!NOTE]
> <span data-ttu-id="ac947-115">구성은 복잡한 개체일 수 있으므로 일반적으로 비교를 단순화 하기 위해 고유한 ID(해시 또는 [GUID][lnk-guid])가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac947-115">Since configurations can be complex objects, they are usually assigned unique ids (hashes or [GUIDs][lnk-guid]) to simplify their comparisons.</span></span>
> 
> 

<span data-ttu-id="ac947-116">장치 앱은 reported 속성에 desired 속성 **telemetryConfig**을 미러링하는 현재 구성을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="ac947-116">The device app reports its current configuration mirroring the desired property **telemetryConfig** in the reported properties:</span></span>

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of the current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Success",
                    }
                }
                ...
            }
        }

<span data-ttu-id="ac947-117">reported **telemetryConfig**에 구성 업데이트 프로세스의 상태를 보고하는 데 사용되는 추가 속성 **상태**가 어떻게 들어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ac947-117">Note how the reported **telemetryConfig** has an additional property **status**, used to report the state of the configuration update process.</span></span>

<span data-ttu-id="ac947-118">새 원하는 구성을 받을 때, 장치 앱은 정보 변경에 따라 보류된 구성을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="ac947-118">When a new desired configuration is received, the device app reports a pending configuration by changing the information:</span></span>

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of the current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Pending",
                        "pendingConfig": {
                            "changeId": "{id of the pending configuration}",
                            "sendFrequency": "{pending configuration}"
                        }
                    }
                }
                ...
            }
        }

<span data-ttu-id="ac947-119">일정 시간 후에 장치 앱은 위의 속성을 업데이트하여 이 작업의 성공 또는 실패 여부를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="ac947-119">Then, at some later time, the device app will report the success or failure of this operation by updating the above property.</span></span>
<span data-ttu-id="ac947-120">솔루션 백 엔드가 언제라도 모든 장치에 대한 구성 프로세스의 상태를 어떻게 쿼리할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ac947-120">Note how the solution back end is able, at any time, to query the status of the configuration process across all the devices.</span></span>

<span data-ttu-id="ac947-121">이 자습서에서는 다음을 수행하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ac947-121">This tutorial shows you how to:</span></span>

* <span data-ttu-id="ac947-122">솔루션 백 엔드에서 구성 업데이트를 받아 구성 업데이트 프로세스에 여러 업데이트를 *보고된 속성*으로 보고하는 시뮬레이션된 장치 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ac947-122">Create a simulated device app that receives configuration updates from the solution back end, and reports multiple updates as *reported properties* on the configuration update process.</span></span>
* <span data-ttu-id="ac947-123">장치의 원하는 구성을 업데이트한 다음 구성 업데이트 프로세스를 쿼리하는 백 엔드 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ac947-123">Create a back-end app that updates the desired configuration of a device, and then queries the configuration update process.</span></span>

<!-- links -->

[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: ../articles/iot-hub/iot-hub-device-management-overview.md
[lnk-twin-tutorial]: ../articles/iot-hub/iot-hub-node-node-twin-getstarted.md
[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier
