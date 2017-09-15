## <a name="create-a-device-identity"></a><span data-ttu-id="5a513-101">장치 ID 만들기</span><span class="sxs-lookup"><span data-stu-id="5a513-101">Create a device identity</span></span>

<span data-ttu-id="5a513-102">이 섹션에서는 [Azure Portal][lnk-azure-portal]을 사용하여 IoT hub의 ID 레지스트리에 장치 ID를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5a513-102">In this section, you use the [Azure portal][lnk-azure-portal] to create a device identity in the identity registry in your IoT hub.</span></span> <span data-ttu-id="5a513-103">ID 레지스트리에 항목이 없는 경우 장치를 IoT Hub에 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5a513-103">A device cannot connect to IoT hub unless it has an entry in the identity registry.</span></span> <span data-ttu-id="5a513-104">자세한 내용은 [IoT Hub 개발자 가이드][lnk-devguide-identity]의 "ID 레지스트리" 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5a513-104">For more information, see the "Identity registry" section of the [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="5a513-105">포털의 **Device Explorer**를 사용하면 IoT Hub에 연결할 때 장치가 자신을 식별하는 데 사용할 수 있는 고유한 장치 ID 및 키를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a513-105">The **Device Explorer** in the portal helps you generate a unique device ID and key that your device can use to identify itself when it connects to IoT Hub.</span></span> <span data-ttu-id="5a513-106">장치 ID는 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="5a513-106">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="5a513-107">[Azure Portal][lnk-azure-portal]에 로그인되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a513-107">Make sure you are signed in to the [Azure portal][lnk-azure-portal].</span></span>

1. <span data-ttu-id="5a513-108">표시줄에서 **모든 리소스**를 클릭하고 IoT hub 리소스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5a513-108">In the Jumpbar, click **All resources** and find your IoT hub resource.</span></span>

    ![IoT Hub로 이동][img-find-iothub]

1. <span data-ttu-id="5a513-110">IoT Hub 리소스가 열리면 **Device Explorer** 도구를 클릭한 다음 위쪽에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a513-110">When your IoT hub resource is opened, click the **Device Explorer** tool, and then click **Add** at the top.</span></span> <span data-ttu-id="5a513-111">**myDeviceId**와 같이 새 장치의 이름을 입력하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a513-111">Provide the name for your new device, such as **myDeviceId**, and click **Save**.</span></span>

    ![포털에서 장치 ID 만들기][img-create-device]

   <span data-ttu-id="5a513-113">IoT Hub에 대한 새 장치 ID를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5a513-113">This creates a new device identity for your IoT hub.</span></span>

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

1. <span data-ttu-id="5a513-114">**Device Explorer**의 장치 목록에서 새로 만든 장치를 클릭하고 **연결 문자열---기본 키**를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="5a513-114">In the **Device Explorer**'s device list, click the newly created device and make note of the **Connection string---primary key**.</span></span> 

    ![장치 연결 문자열][img-connection-string]

> [!NOTE]
> <span data-ttu-id="5a513-116">IoT Hub ID 레지스트리는 장치 ID만 저장하여 IoT Hub에 보안 액세스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5a513-116">The IoT Hub identity registry only stores device identities to enable secure access to the IoT hub.</span></span> <span data-ttu-id="5a513-117">보안 자격 증명으로 사용하기 위해 장치 ID 및 키와 개별 장치에 대해 액세스하지 못하도록 설정할 수 있는 사용/사용 안 함 플래그를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5a513-117">It stores device IDs and keys to use as security credentials, and an enabled/disabled flag that you can use to disable access for an individual device.</span></span> <span data-ttu-id="5a513-118">응용 프로그램이 다른 장치별 메타데이터를 저장해야 할 경우 응용 프로그램별 저장소를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a513-118">If your application needs to store other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="5a513-119">자세한 내용은 [IoT Hub 개발자 가이드][lnk-devguide-identity]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5a513-119">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span></span>

<!-- Images. -->
[img-find-iothub]: ./media/iot-hub-get-started-create-device-identity-portal/find-iothub.png
[img-create-device]: ./media/iot-hub-get-started-create-device-identity-portal/create-identity-portal.png
[img-connection-string]: ./media/iot-hub-get-started-create-device-identity-portal/device-connection-string.png


<!-- Links -->
[lnk-azure-portal]: https://portal.azure.com
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md

