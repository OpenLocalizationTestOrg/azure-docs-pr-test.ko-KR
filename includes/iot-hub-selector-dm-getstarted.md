> [!div class="op_single_selector"]
> * [<span data-ttu-id="a4e70-101">장치: Node.js 서비스: Node.js</span><span class="sxs-lookup"><span data-stu-id="a4e70-101">Device: Node.js Service: Node.js</span></span>](../articles/iot-hub/iot-hub-node-node-device-management-get-started.md)
> * [<span data-ttu-id="a4e70-102">장치: Node.js 서비스: C#</span><span class="sxs-lookup"><span data-stu-id="a4e70-102">Device: Node.js Service: C#</span></span>](../articles/iot-hub/iot-hub-csharp-node-device-management-get-started.md)
> * [<span data-ttu-id="a4e70-103">장치: Java 서비스: Java</span><span class="sxs-lookup"><span data-stu-id="a4e70-103">Device: Java Service: Java</span></span>](../articles/iot-hub/iot-hub-java-java-device-management-getstarted.md)

<span data-ttu-id="a4e70-104">백 엔드 앱 צ ְ ײ Azure IoT Hub 기본 형식과 같은 [장치로 이중] [ lnk-devtwin] 및 [메서드를 직접][lnk-c2dmethod], tooremotely 시작 하 고 모니터링 장치에서 장치 관리 작업을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e70-104">Back-end apps can use Azure IoT Hub primitives, such as [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod], tooremotely start and monitor device management actions on devices.</span></span> <span data-ttu-id="a4e70-105">이 자습서에서는 어떻게 백 엔드 앱 및 장치 앱 tooinitiate 함께 작동 하 고 모니터링할 수 IoT 허브를 사용 하는 원격 장치를 다시 부팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e70-105">This tutorial shows you how a back-end app and a device app can work together tooinitiate and monitor a remote device reboot using IoT Hub.</span></span>

<span data-ttu-id="a4e70-106">Hello 클라우드에서 백 엔드 응용 프로그램에서 (예: 다시 부팅, 공장 기본 설정 및 펌웨어 업데이트) 직접적인 방법 tooinitiate 장치 관리 작업을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e70-106">Use a direct method tooinitiate device management actions (such as reboot, factory reset, and firmware update) from a back-end app in hello cloud.</span></span> <span data-ttu-id="a4e70-107">hello 장치에 대 한 책임이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e70-107">hello device is responsible for:</span></span>

* <span data-ttu-id="a4e70-108">IoT 허브에서 보낸 hello 메서드 요청을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e70-108">Handling hello method request sent from IoT Hub.</span></span>
* <span data-ttu-id="a4e70-109">Hello hello 장치에서 해당 장치 관련 작업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a4e70-109">Initiating hello corresponding device-specific action on hello device.</span></span>
* <span data-ttu-id="a4e70-110">상태 업데이트를 통해 제공 *속성을 보고* tooIoT 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="a4e70-110">Providing status updates through *reported properties* tooIoT Hub.</span></span>

<span data-ttu-id="a4e70-111">Hello 클라우드 toorun 장치로 이중 쿼리 tooreport 장치 관리 작업의 진행률 hello에에서 백 엔드 응용 프로그램을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4e70-111">You can use a back-end app in hello cloud toorun device twin queries tooreport on hello progress of your device management actions.</span></span>

[lnk-devtwin]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
