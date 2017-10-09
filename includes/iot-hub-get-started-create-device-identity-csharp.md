## <a name="create-a-device-identity"></a><span data-ttu-id="84d96-101">장치 ID 만들기</span><span class="sxs-lookup"><span data-stu-id="84d96-101">Create a device identity</span></span>
<span data-ttu-id="84d96-102">이 섹션에서는 IoT 허브에 대 한 hello identity 레지스트리에 장치 id를 생성 하 여.NET 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="84d96-102">In this section, you create a .NET console app that creates a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="84d96-103">장치 id 레지스트리에 hello에 항목이 없는 경우 tooIoT 허브를 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="84d96-103">A device cannot connect tooIoT hub unless it has an entry in hello identity registry.</span></span> <span data-ttu-id="84d96-104">자세한 내용은 hello의 hello "Id 레지스트리에" 섹션을 참조 [IoT 허브 개발자 가이드][lnk-devguide-identity]합니다.</span><span class="sxs-lookup"><span data-stu-id="84d96-104">For more information, see hello "Identity registry" section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="84d96-105">이 콘솔 응용 프로그램을 실행 하면 고유한 장치 ID를 생성 및 메시지 tooIoT 허브를 키 장치-클라우드 보낼 때 장치가 tooidentify 자체를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84d96-105">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span> <span data-ttu-id="84d96-106">장치 ID는 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="84d96-106">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="84d96-107">Visual Studio에서 Visual C# Windows 클래식 데스크톱 프로젝트 tooa 새 솔루션 hello를 사용 하 여 추가 **콘솔 응용 프로그램 (.NET Framework)** 서식 파일 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="84d96-107">In Visual Studio, add a Visual C# Windows Classic Desktop project tooa new solution by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="84d96-108">Hello.NET Framework 버전 4.5.1 인지 확인 하거나 나중에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84d96-108">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="84d96-109">이름 hello 프로젝트 **CreateDeviceIdentity** 및 이름 hello 솔루션 **IoTHubGetStarted**합니다.</span><span class="sxs-lookup"><span data-stu-id="84d96-109">Name hello project **CreateDeviceIdentity** and name hello solution **IoTHubGetStarted**.</span></span>
   
    ![새 Visual C# Windows 클래식 데스크톱 프로젝트][10]
2. <span data-ttu-id="84d96-111">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **CreateDeviceIdentity** 프로젝트를 마우스 클릭 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="84d96-111">In Solution Explorer, right-click hello **CreateDeviceIdentity** project, and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="84d96-112">Hello에 **NuGet 패키지 관리자** 창에서 **찾아보기**, 검색할 **microsoft.azure.devices**선택, **설치** tooinstall hello **Microsoft.Azure.Devices** 패키지 및 hello 사용 약관에 동의 합니다.</span><span class="sxs-lookup"><span data-stu-id="84d96-112">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="84d96-113">이 절차를 다운로드, 설치 하 고 참조 toohello 추가 [Azure IoT 서비스 SDK] [ lnk-nuget-service-sdk] NuGet 패키지 및 해당 종속성.</span><span class="sxs-lookup"><span data-stu-id="84d96-113">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet 패키지 관리자 창][11]
4. <span data-ttu-id="84d96-115">Hello 다음 추가 `using` hello 위쪽 hello에 문을 **Program.cs** 파일:</span><span class="sxs-lookup"><span data-stu-id="84d96-115">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Common.Exceptions;
5. <span data-ttu-id="84d96-116">다음 필드 toohello hello 추가 **프로그램** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="84d96-116">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="84d96-117">Hello hello 이전 섹션에서 만든 hello 허브에 대 한 IoT 허브 연결 문자열 hello 자리 표시자 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="84d96-117">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="84d96-118">다음 메서드 toohello hello 추가 **프로그램** 클래스:</span><span class="sxs-lookup"><span data-stu-id="84d96-118">Add hello following method toohello **Program** class:</span></span>
   
        private static async Task AddDeviceAsync()
        {
            string deviceId = "myFirstDevice";
            Device device;
            try
            {
                device = await registryManager.AddDeviceAsync(new Device(deviceId));
            }
            catch (DeviceAlreadyExistsException)
            {
                device = await registryManager.GetDeviceAsync(deviceId);
            }
            Console.WriteLine("Generated device key: {0}", device.Authentication.SymmetricKey.PrimaryKey);
        }
   
    <span data-ttu-id="84d96-119">이 메서드는 ID **myFirstDevice**로 장치 ID를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="84d96-119">This method creates a device identity with ID **myFirstDevice**.</span></span> <span data-ttu-id="84d96-120">(해당 장치 ID에에서 이미 있으면 hello id 레지스트리에, hello 코드 단순히 hello 기존 장치 정보 검색 합니다.) hello 앱 hello 해당 id에 대 한 기본 키를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="84d96-120">(If that device ID already exists in hello identity registry, hello code simply retrieves hello existing device information.) hello app then displays hello primary key for that identity.</span></span> <span data-ttu-id="84d96-121">시뮬레이션 된 hello 장치 앱 tooconnect tooyour IoT 허브에서이 키를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="84d96-121">You use this key in hello simulated device app tooconnect tooyour IoT hub.</span></span>
[!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

7. <span data-ttu-id="84d96-122">마지막으로 다음 줄 toohello hello 추가 **Main** 메서드:</span><span class="sxs-lookup"><span data-stu-id="84d96-122">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddDeviceAsync().Wait();
        Console.ReadLine();
8. <span data-ttu-id="84d96-123">이 응용 프로그램을 실행 하 고 hello 장치 키를 메모 합니다.</span><span class="sxs-lookup"><span data-stu-id="84d96-123">Run this application, and make a note of hello device key.</span></span>
   
    ![Hello 응용 프로그램에 의해 생성 된 장치 키][12]

> [!NOTE]
> <span data-ttu-id="84d96-125">IoT Hub id 레지스트리에 hello만 장치 identities tooenable 보안 액세스 toohello IoT 허브를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="84d96-125">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="84d96-126">장치 Id와 키 toouse 보안 자격 증명 및 개별 장치에 대 한 toodisable 액세스를 사용할 수 있는 사용/사용 안 함 플래그로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="84d96-126">It stores device IDs and keys toouse as security credentials, and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="84d96-127">응용 프로그램는 toostore 다른 장치 관련 메타 데이터를 필요한 경우에 응용 프로그램별 저장소를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="84d96-127">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="84d96-128">자세한 내용은 [IoT Hub 개발자 가이드][lnk-devguide-identity]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="84d96-128">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 

<!-- Images. -->
[10]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp1.png
[11]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp2.png
[12]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp3.png


<!-- Links -->
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
