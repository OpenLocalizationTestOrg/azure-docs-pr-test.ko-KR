## <a name="create-a-device-identity"></a>장치 ID 만들기
이 섹션에서는 IoT 허브에 대 한 hello identity 레지스트리에 장치 id를 생성 하 여.NET 콘솔 응용 프로그램을 만듭니다. 장치 id 레지스트리에 hello에 항목이 없는 경우 tooIoT 허브를 연결할 수 없습니다. 자세한 내용은 hello의 hello "Id 레지스트리에" 섹션을 참조 [IoT 허브 개발자 가이드][lnk-devguide-identity]합니다. 이 콘솔 응용 프로그램을 실행 하면 고유한 장치 ID를 생성 및 메시지 tooIoT 허브를 키 장치-클라우드 보낼 때 장치가 tooidentify 자체를 사용할 수 있습니다. 장치 ID는 대/소문자를 구분합니다.

1. Visual Studio에서 Visual C# Windows 클래식 데스크톱 프로젝트 tooa 새 솔루션 hello를 사용 하 여 추가 **콘솔 응용 프로그램 (.NET Framework)** 서식 파일 프로젝트. Hello.NET Framework 버전 4.5.1 인지 확인 하거나 나중에 있습니다. 이름 hello 프로젝트 **CreateDeviceIdentity** 및 이름 hello 솔루션 **IoTHubGetStarted**합니다.
   
    ![새 Visual C# Windows 클래식 데스크톱 프로젝트][10]
2. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **CreateDeviceIdentity** 프로젝트를 마우스 클릭 **NuGet 패키지 관리**합니다.
3. Hello에 **NuGet 패키지 관리자** 창에서 **찾아보기**, 검색할 **microsoft.azure.devices**선택, **설치** tooinstall hello **Microsoft.Azure.Devices** 패키지 및 hello 사용 약관에 동의 합니다. 이 절차를 다운로드, 설치 하 고 참조 toohello 추가 [Azure IoT 서비스 SDK] [ lnk-nuget-service-sdk] NuGet 패키지 및 해당 종속성.
   
    ![NuGet 패키지 관리자 창][11]
4. Hello 다음 추가 `using` hello 위쪽 hello에 문을 **Program.cs** 파일:
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Common.Exceptions;
5. 다음 필드 toohello hello 추가 **프로그램** 클래스입니다. Hello hello 이전 섹션에서 만든 hello 허브에 대 한 IoT 허브 연결 문자열 hello 자리 표시자 값을 바꿉니다.
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
6. 다음 메서드 toohello hello 추가 **프로그램** 클래스:
   
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
   
    이 메서드는 ID **myFirstDevice**로 장치 ID를 만듭니다. (해당 장치 ID에에서 이미 있으면 hello id 레지스트리에, hello 코드 단순히 hello 기존 장치 정보 검색 합니다.) hello 앱 hello 해당 id에 대 한 기본 키를 표시합니다. 시뮬레이션 된 hello 장치 앱 tooconnect tooyour IoT 허브에서이 키를 사용 합니다.
[!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

7. 마지막으로 다음 줄 toohello hello 추가 **Main** 메서드:
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddDeviceAsync().Wait();
        Console.ReadLine();
8. 이 응용 프로그램을 실행 하 고 hello 장치 키를 메모 합니다.
   
    ![Hello 응용 프로그램에 의해 생성 된 장치 키][12]

> [!NOTE]
> IoT Hub id 레지스트리에 hello만 장치 identities tooenable 보안 액세스 toohello IoT 허브를 저장합니다. 장치 Id와 키 toouse 보안 자격 증명 및 개별 장치에 대 한 toodisable 액세스를 사용할 수 있는 사용/사용 안 함 플래그로 저장 합니다. 응용 프로그램는 toostore 다른 장치 관련 메타 데이터를 필요한 경우에 응용 프로그램별 저장소를 사용 해야 합니다. 자세한 내용은 [IoT Hub 개발자 가이드][lnk-devguide-identity]를 참조하세요.
> 
> 

<!-- Images. -->
[10]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp1.png
[11]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp2.png
[12]: ./media/iot-hub-get-started-create-device-identity-csharp/create-identity-csharp3.png


<!-- Links -->
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
