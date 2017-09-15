> [!div class="op_single_selector"]
> * [<span data-ttu-id="ad637-101">장치: Node.js 서비스: Node.js</span><span class="sxs-lookup"><span data-stu-id="ad637-101">Device: Node.js Service: Node.js</span></span>](../articles/iot-hub/iot-hub-node-node-device-management-get-started.md)
> * [<span data-ttu-id="ad637-102">장치: Node.js 서비스: C#</span><span class="sxs-lookup"><span data-stu-id="ad637-102">Device: Node.js Service: C#</span></span>](../articles/iot-hub/iot-hub-csharp-node-device-management-get-started.md)
> * [<span data-ttu-id="ad637-103">장치: Java 서비스: Java</span><span class="sxs-lookup"><span data-stu-id="ad637-103">Device: Java Service: Java</span></span>](../articles/iot-hub/iot-hub-java-java-device-management-getstarted.md)

<span data-ttu-id="ad637-104">백 엔드 앱은 Azure IoT Hub 기본 형식, 즉 [장치 쌍][lnk-devtwin] 및 [직접 메서드][lnk-c2dmethod]를 사용하여 장치에서 장치 관리 작업을 원격으로 시작하고 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad637-104">Back-end apps can use Azure IoT Hub primitives, such as [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod], to remotely start and monitor device management actions on devices.</span></span> <span data-ttu-id="ad637-105">이 자습서에서는 백 엔드 앱 및 장치 앱이 함께 작동하여 IoT Hub를 사용하여 원격 장치 다시 부팅을 시작하고 모니터링하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ad637-105">This tutorial shows you how a back-end app and a device app can work together to initiate and monitor a remote device reboot using IoT Hub.</span></span>

<span data-ttu-id="ad637-106">직접 메서드를 사용하여 클라우드의 백 엔드 앱에서 장치 관리 작업(예: 재부팅, 초기화 및 펌웨어 업데이트)을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ad637-106">Use a direct method to initiate device management actions (such as reboot, factory reset, and firmware update) from a back-end app in the cloud.</span></span> <span data-ttu-id="ad637-107">장치는 다음과 같은 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad637-107">The device is responsible for:</span></span>

* <span data-ttu-id="ad637-108">IoT Hub에서 보낸 메서드 요청 처리.</span><span class="sxs-lookup"><span data-stu-id="ad637-108">Handling the method request sent from IoT Hub.</span></span>
* <span data-ttu-id="ad637-109">장치에서 해당하는 장치 특정 작업 시작.</span><span class="sxs-lookup"><span data-stu-id="ad637-109">Initiating the corresponding device-specific action on the device.</span></span>
* <span data-ttu-id="ad637-110">*reported 속성*을 통해 IoT Hub에 상태 업데이트 제공.</span><span class="sxs-lookup"><span data-stu-id="ad637-110">Providing status updates through *reported properties* to IoT Hub.</span></span>

<span data-ttu-id="ad637-111">클라우드에서 백 엔드 앱을 사용하여 장치 쌍 쿼리를 실행하고 장치 관리 작업의 진행 상태를 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad637-111">You can use a back-end app in the cloud to run device twin queries to report on the progress of your device management actions.</span></span>

[lnk-devtwin]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
