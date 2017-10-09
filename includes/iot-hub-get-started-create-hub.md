## <a name="create-an-iot-hub"></a><span data-ttu-id="9f164-101">IoT Hub 만들기</span><span class="sxs-lookup"><span data-stu-id="9f164-101">Create an IoT hub</span></span>
<span data-ttu-id="9f164-102">시뮬레이션 된 장치 앱 tooconnect 프로그램에 대 한 IoT 허브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f164-102">Create an IoT hub for your simulated device app tooconnect to.</span></span> <span data-ttu-id="9f164-103">hello 다음 단계 보여 어떻게 toocomplete이 작업 하 여 Azure 포털 hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f164-103">hello following steps show you how toocomplete this task by using hello Azure portal.</span></span>

1. <span data-ttu-id="9f164-104">Toohello 로그인 [Azure 포털][lnk-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="9f164-104">Sign in toohello [Azure portal][lnk-portal].</span></span>
1. <span data-ttu-id="9f164-105">Hello Jumpbar, 클릭 **새로** > **사물 인터넷** > **IoT Hub**합니다.</span><span class="sxs-lookup"><span data-stu-id="9f164-105">In hello Jumpbar, click **New** > **Internet of Things** > **IoT Hub**.</span></span>
   
    ![Azure 포털 표시줄][1]
1. <span data-ttu-id="9f164-107">Hello에 **IoT hub** 블레이드에서 IoT 허브에 대 한 hello 구성을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f164-107">In hello **IoT hub** blade, choose hello configuration for your IoT hub.</span></span>
   
    ![IoT Hub 블레이드][2]
   
   1. <span data-ttu-id="9f164-109">Hello에 **이름** 상자 IoT 허브에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f164-109">In hello **Name** box, enter a name for your IoT hub.</span></span> <span data-ttu-id="9f164-110">경우 hello **이름** 유효 하 고 hello에 녹색 확인 표시가 표시를 사용할 수 **이름** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="9f164-110">If hello **Name** is valid and available, a green check mark appears in hello **Name** box.</span></span>
    [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]
   
   1. <span data-ttu-id="9f164-111">[가격 책정 및 크기 조정 계층][lnk-pricing]을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f164-111">Select a [pricing and scale tier][lnk-pricing].</span></span> <span data-ttu-id="9f164-112">이 자습서에는 특정 계층이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9f164-112">This tutorial does not require a specific tier.</span></span> <span data-ttu-id="9f164-113">이 자습서에 대 한 hello 무료 F1 계층을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f164-113">For this tutorial, use hello free F1 tier.</span></span>
   1. <span data-ttu-id="9f164-114">**리소스 그룹**에서 리소스 그룹을 만들거나 기존 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f164-114">In **Resource group**, either create a resource group, or select an existing one.</span></span> <span data-ttu-id="9f164-115">자세한 내용은 참조 [toomanage Azure 리소스 그룹 리소스를 사용 하 여][lnk-resource-groups]합니다.</span><span class="sxs-lookup"><span data-stu-id="9f164-115">For more information, see [Using resource groups toomanage your Azure resources][lnk-resource-groups].</span></span>
   1. <span data-ttu-id="9f164-116">**위치**, 선택 hello 위치 toohost IoT 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="9f164-116">In **Location**, select hello location toohost your IoT hub.</span></span> <span data-ttu-id="9f164-117">이 자습서에 대한 가장 가까운 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f164-117">For this tutorial, choose your nearest location.</span></span>
1. <span data-ttu-id="9f164-118">IoT hub 구성 옵션을 선택한 경우 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9f164-118">When you have chosen your IoT hub configuration options, click **Create**.</span></span>  <span data-ttu-id="9f164-119">IoT hub Azure toocreate 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f164-119">It can take a few minutes for Azure toocreate your IoT hub.</span></span> <span data-ttu-id="9f164-120">toocheck hello 상태 hello 알림 패널 또는 hello 시작 보드에 hello 진행률을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f164-120">toocheck hello status, you can monitor hello progress on hello Startboard or in hello Notifications panel.</span></span>
   
    ![새 IoT Hub 상태][3]
1. <span data-ttu-id="9f164-122">Hello IoT hub 성공적으로 생성 되 면 hello hello Azure 포털 tooopen hello 블레이드에서 hello 새 IoT 허브에 대 한 IoT 허브에 대 한 새 타일을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f164-122">When hello IoT hub has been created successfully, click hello new tile for your IoT hub in hello Azure portal tooopen hello blade for hello new IoT hub.</span></span> <span data-ttu-id="9f164-123">Hello 메모 **Hostname**, 클릭 하 고 **공유 액세스 정책을**합니다.</span><span class="sxs-lookup"><span data-stu-id="9f164-123">Make a note of hello **Hostname**, and then click **Shared access policies**.</span></span>
   
    ![새 IoT Hub 블레이드][4]
1. <span data-ttu-id="9f164-125">Hello에 **공유 액세스 정책을** 블레이드에서 hello 클릭 **iothubowner** 정책을 복사 하 고 hello hello IoT 허브 연결 문자열을 적어 **iothubowner** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="9f164-125">In hello **Shared access policies** blade, click hello **iothubowner** policy, and then copy and make note of hello IoT Hub connection string in hello **iothubowner** blade.</span></span> <span data-ttu-id="9f164-126">자세한 내용은 참조 [액세스 제어] [ lnk-access-control] hello "IoT 허브 개발자 가이드"의</span><span class="sxs-lookup"><span data-stu-id="9f164-126">For more information, see [Access control][lnk-access-control] in hello "IoT Hub developer guide."</span></span>
   
    ![공유 액세스 정책 블레이드][5]

<!-- Images. -->
[1]: ./media/iot-hub-get-started-create-hub/create-iot-hub1.png
[2]: ./media/iot-hub-get-started-create-hub/create-iot-hub2.png
[3]: ./media/iot-hub-get-started-create-hub/create-iot-hub3.png
[4]: ./media/iot-hub-get-started-create-hub/create-iot-hub4.png
[5]: ./media/iot-hub-get-started-create-hub/create-iot-hub5.png

<!-- Links -->
[lnk-resource-groups]: ../articles/azure-resource-manager/resource-group-portal.md
[lnk-portal]: https://portal.azure.com/
[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-access-control]: ../articles/iot-hub/iot-hub-devguide-security.md
