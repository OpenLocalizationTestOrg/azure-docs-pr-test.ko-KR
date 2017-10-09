## <a name="create-a-device-identity"></a><span data-ttu-id="2633d-101">장치 ID 만들기</span><span class="sxs-lookup"><span data-stu-id="2633d-101">Create a device identity</span></span>

<span data-ttu-id="2633d-102">이 섹션을 사용 하 여 hello [Azure 포털] [ lnk-azure-portal] toocreate hello id 레지스트리에 IoT 허브에서에서 장치 id입니다.</span><span class="sxs-lookup"><span data-stu-id="2633d-102">In this section, you use hello [Azure portal][lnk-azure-portal] toocreate a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="2633d-103">장치 id 레지스트리에 hello에 항목이 없는 경우 tooIoT 허브를 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2633d-103">A device cannot connect tooIoT hub unless it has an entry in hello identity registry.</span></span> <span data-ttu-id="2633d-104">자세한 내용은 hello의 hello "Id 레지스트리에" 섹션을 참조 [IoT 허브 개발자 가이드][lnk-devguide-identity]합니다.</span><span class="sxs-lookup"><span data-stu-id="2633d-104">For more information, see hello "Identity registry" section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="2633d-105">hello **장치 탐색기** hello에 포털을 통해 고유한 장치 ID와 tooIoT 허브에 연결할 때 장치에서 tooidentify 자체를 사용할 수 있는 키를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2633d-105">hello **Device Explorer** in hello portal helps you generate a unique device ID and key that your device can use tooidentify itself when it connects tooIoT Hub.</span></span> <span data-ttu-id="2633d-106">장치 ID는 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="2633d-106">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="2633d-107">Toohello 로그인 되어 있는지 확인 [Azure 포털][lnk-azure-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="2633d-107">Make sure you are signed in toohello [Azure portal][lnk-azure-portal].</span></span>

1. <span data-ttu-id="2633d-108">Hello Jumpbar, 클릭 **모든 리소스** IoT 허브 리소스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="2633d-108">In hello Jumpbar, click **All resources** and find your IoT hub resource.</span></span>

    ![Tooyour Iot 허브를 이동 합니다.][img-find-iothub]

1. <span data-ttu-id="2633d-110">IoT 허브 리소스를 열 때 클릭 hello **장치 탐색기** 도구를 클릭 한 다음 클릭 **추가** hello 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2633d-110">When your IoT hub resource is opened, click hello **Device Explorer** tool, and then click **Add** at hello top.</span></span> <span data-ttu-id="2633d-111">새 장치에 대 한 hello 이름 같은 제공 **myDeviceId**를 클릭 하 고 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="2633d-111">Provide hello name for your new device, such as **myDeviceId**, and click **Save**.</span></span>

    ![포털에서 장치 ID 만들기][img-create-device]

   <span data-ttu-id="2633d-113">IoT Hub에 대한 새 장치 ID를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2633d-113">This creates a new device identity for your IoT hub.</span></span>

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

1. <span data-ttu-id="2633d-114">Hello에 **장치 탐색기**의 장치 목록에서 새로 만든 hello 장치를 클릭 하 고 hello 기록 **연결 문자열---기본 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="2633d-114">In hello **Device Explorer**'s device list, click hello newly created device and make note of hello **Connection string---primary key**.</span></span> 

    ![장치 연결 문자열][img-connection-string]

> [!NOTE]
> <span data-ttu-id="2633d-116">IoT Hub id 레지스트리에 hello만 장치 identities tooenable 보안 액세스 toohello IoT 허브를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2633d-116">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="2633d-117">장치 Id와 키 toouse 보안 자격 증명 및 개별 장치에 대 한 toodisable 액세스를 사용할 수 있는 사용/사용 안 함 플래그로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2633d-117">It stores device IDs and keys toouse as security credentials, and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="2633d-118">응용 프로그램는 toostore 다른 장치 관련 메타 데이터를 필요한 경우에 응용 프로그램별 저장소를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2633d-118">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="2633d-119">자세한 내용은 [IoT Hub 개발자 가이드][lnk-devguide-identity]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2633d-119">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span></span>

<!-- Images. -->
[img-find-iothub]: ./media/iot-hub-get-started-create-device-identity-portal/find-iothub.png
[img-create-device]: ./media/iot-hub-get-started-create-device-identity-portal/create-identity-portal.png
[img-connection-string]: ./media/iot-hub-get-started-create-device-identity-portal/device-connection-string.png


<!-- Links -->
[lnk-azure-portal]: https://portal.azure.com
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md

