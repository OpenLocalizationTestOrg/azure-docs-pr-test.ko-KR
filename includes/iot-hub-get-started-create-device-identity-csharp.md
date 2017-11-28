## <a name="create-a-device-identity"></a><span data-ttu-id="4117c-101">장치 ID 만들기</span><span class="sxs-lookup"><span data-stu-id="4117c-101">Create a device identity</span></span>
<span data-ttu-id="4117c-102">이 섹션에서는 IoT Hub의 ID 레지스트리에서 장치 ID를 만드는 .NET 콘솔 앱을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="4117c-102">In this section, you create a .NET console app that creates a device identity in the identity registry in your IoT hub.</span></span> <span data-ttu-id="4117c-103">ID 레지스트리에 항목이 없는 경우 장치를 IoT Hub에 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4117c-103">A device cannot connect to IoT hub unless it has an entry in the identity registry.</span></span> <span data-ttu-id="4117c-104">자세한 내용은 [IoT Hub 개발자 가이드][lnk-devguide-identity]의 "ID 레지스트리" 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4117c-104">For more information, see the "Identity registry" section of the [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="4117c-105">이 콘솔 앱을 실행하면 장치-클라우드 메시지를 IoT Hub로 보낼 때 장치가 자체적으로 ID를 식별하는 데 사용할 수 있는 고유한 장치 ID와 키를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="4117c-105">When you run this console app, it generates a unique device ID and key that your device can use to identify itself when it sends device-to-cloud messages to IoT Hub.</span></span> <span data-ttu-id="4117c-106">장치 ID는 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="4117c-106">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="4117c-107">Visual Studio에서 **콘솔 앱(.NET Framework)** 프로젝트 템플릿을 사용하여 Visual C# Windows 클래식 바탕화면 프로젝트를 새 솔루션에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4117c-107">In Visual Studio, add a Visual C# Windows Classic Desktop project to a new solution by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="4117c-108">.NET Framework 버전이 4.5.1 이상인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4117c-108">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="4117c-109">프로젝트 이름을 **CreateDeviceIdentity**로 솔루션 이름을 **IoTHubGetStarted**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4117c-109">Name the project **CreateDeviceIdentity** and name the solution **IoTHubGetStarted**.</span></span>
   
    ![새 Visual C# Windows 클래식 데스크톱 프로젝트][10]
2. <span data-ttu-id="4117c-111">솔루션 탐색기에서 **CreateDeviceIdentity** 프로젝트를 마우스 오른쪽 단추로 클릭한 다음, **NuGet 패키지 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4117c-111">In Solution Explorer, right-click the **CreateDeviceIdentity** project, and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="4117c-112">**NuGet 패키지 관리자** 창에서 **찾아보기**를 선택하고 **microsoft.azure.devices**를 검색한 다음 **설치**를 선택하여 **Microsoft.Azure.Devices** 패키지를 설치하고 사용 약관에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="4117c-112">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="4117c-113">이 프로시저에서는 [Azure IoT 서비스 SDK][lnk-nuget-service-sdk] NuGet 패키지 및 종속 항목에 참조를 다운로드, 설치 및 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4117c-113">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet 패키지 관리자 창][11]
4. <span data-ttu-id="4117c-115">**Program.cs** 파일 위에 다음 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4117c-115">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Common.Exceptions;
5. <span data-ttu-id="4117c-116">**Program** 클래스에 다음 필드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4117c-116">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="4117c-117">자리 표시자 값을 이전 섹션에서 만든 허브의 IoT Hub 연결 문자열로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="4117c-117">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="4117c-118">**Program** 클래스에 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4117c-118">Add the following method to the **Program** class:</span></span>
   
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
   
    <span data-ttu-id="4117c-119">이 메서드는 ID **myFirstDevice**로 장치 ID를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4117c-119">This method creates a device identity with ID **myFirstDevice**.</span></span> <span data-ttu-id="4117c-120">ID 레지스트리에 해당 장치 ID가 이미 있는 경우 코드는 기존 장치 정보만 검색합니다. 그러면 앱에서 해당 ID에 대한 기본 키를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="4117c-120">(If that device ID already exists in the identity registry, the code simply retrieves the existing device information.) The app then displays the primary key for that identity.</span></span> <span data-ttu-id="4117c-121">이 키를 시뮬레이션된 장치 앱에서 사용하여 IoT Hub에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="4117c-121">You use this key in the simulated device app to connect to your IoT hub.</span></span>
[!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

7. <span data-ttu-id="4117c-122">마지막으로 **Main** 메서드에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4117c-122">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddDeviceAsync().Wait();
        Console.ReadLine();
8. <span data-ttu-id="4117c-123">이 응용 프로그램을 실행하고 장치 키를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="4117c-123">Run this application, and make a note of the device key.</span></span>
   
    ![응용 프로그램에서 생성된 장치 키][12]

> [!NOTE]
> <span data-ttu-id="4117c-125">IoT Hub ID 레지스트리는 장치 ID만 저장하여 IoT Hub에 보안 액세스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4117c-125">The IoT Hub identity registry only stores device identities to enable secure access to the IoT hub.</span></span> <span data-ttu-id="4117c-126">보안 자격 증명으로 사용하기 위해 장치 ID 및 키와 개별 장치에 대해 액세스하지 못하도록 설정할 수 있는 사용/사용 안 함 플래그를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="4117c-126">It stores device IDs and keys to use as security credentials, and an enabled/disabled flag that you can use to disable access for an individual device.</span></span> <span data-ttu-id="4117c-127">응용 프로그램이 다른 장치별 메타데이터를 저장해야 할 경우 응용 프로그램별 저장소를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4117c-127">If your application needs to store other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="4117c-128">자세한 내용은 [IoT Hub 개발자 가이드][lnk-devguide-identity]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4117c-128">For more information, see [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 

<!-- Images. -->
[10]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp1.png
[11]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp2.png
[12]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp3.png


<!-- Links -->
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
