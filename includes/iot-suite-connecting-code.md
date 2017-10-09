## <a name="specify-hello-behavior-of-hello-iot-device"></a><span data-ttu-id="0b6fa-101">Hello IoT 장치의 hello 동작 지정</span><span class="sxs-lookup"><span data-stu-id="0b6fa-101">Specify hello behavior of hello IoT device</span></span>

<span data-ttu-id="0b6fa-102">IoT Hub serializer 클라이언트 라이브러리 hello IoT Hub와 hello 메시지 hello 장치 교환 모델 toospecify hello 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0b6fa-102">hello IoT Hub serializer client library uses a model toospecify hello format of hello messages hello device exchanges with IoT Hub.</span></span>

1. <span data-ttu-id="0b6fa-103">변수 선언 hello 후 다음 hello 추가 `#include` 문.</span><span class="sxs-lookup"><span data-stu-id="0b6fa-103">Add hello following variable declarations after hello `#include` statements.</span></span> <span data-ttu-id="0b6fa-104">대체 hello 자리 표시자 값 [장치 Id] 및 [장치 Key] hello 원격 모니터링 솔루션 대시보드에서 장치에서 기록한 값으로.</span><span class="sxs-lookup"><span data-stu-id="0b6fa-104">Replace hello placeholder values [Device Id] and [Device Key] with values you noted for your device in hello remote monitoring solution dashboard.</span></span> <span data-ttu-id="0b6fa-105">Hello 솔루션 대시보드 tooreplace [IoTHub Name]에서 hello IoT 허브 호스트 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b6fa-105">Use hello IoT Hub Hostname from hello solution dashboard tooreplace [IoTHub Name].</span></span> <span data-ttu-id="0b6fa-106">예를 들어 IoT Hub 호스트 이름이 **contoso.azure-devices.net**인 경우 [IoTHub Name]을 **contoso**로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0b6fa-106">For example, if your IoT Hub Hostname is **contoso.azure-devices.net**, replace [IoTHub Name] with **contoso**:</span></span>
   
    ```c
    static const char* deviceId = "[Device Id]";
    static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
    ```

1. <span data-ttu-id="0b6fa-107">Hello 코드 toodefine hello 모델로 IoT Hub와 장치 toocommunicate hello를 사용 하 여 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b6fa-107">Add hello following code toodefine hello model that enables hello device toocommunicate with IoT Hub.</span></span> <span data-ttu-id="0b6fa-108">이 모델 hello 장치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0b6fa-108">This model specifies that hello device:</span></span>

   - <span data-ttu-id="0b6fa-109">온도, 외부 온도, 습도 및 장치 ID를 원격 분석으로 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b6fa-109">Can send temperature, external temperature, humidity, and a device id as telemetry.</span></span>
   - <span data-ttu-id="0b6fa-110">Hello 장치 tooIoT 허브에 대 한 메타 데이터를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b6fa-110">Can send metadata about hello device tooIoT Hub.</span></span> <span data-ttu-id="0b6fa-111">기본 메타 데이터를 전송 하는 hello 장치는 **DeviceInfo** 시작 시 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="0b6fa-111">hello device sends basic metadata in a **DeviceInfo** object at startup.</span></span>
   - <span data-ttu-id="0b6fa-112">보고 속성을 toohello 장치로 이중 IoT Hub에 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b6fa-112">Can send reported properties, toohello device twin in IoT Hub.</span></span> <span data-ttu-id="0b6fa-113">이러한 reported 속성은 구성, 장치 및 시스템 속성으로 그룹화됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b6fa-113">These reported properties are grouped into configuration, device, and system properties.</span></span>
   - <span data-ttu-id="0b6fa-114">수신 하 고 원하는 속성 집합이 hello 장치로 이중 IoT 허브에서 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b6fa-114">Can receive and act on desired properties set in hello device twin in IoT Hub.</span></span>
   - <span data-ttu-id="0b6fa-115">Toohello 응답할 수 **재부팅** 및 **InitiateFirmwareUpdate** hello 솔루션 포털을 통해 호출 된 메서드를 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b6fa-115">Can respond toohello **Reboot** and **InitiateFirmwareUpdate** direct methods invoked through hello solution portal.</span></span> <span data-ttu-id="0b6fa-116">보고 속성을 사용 하 여 지원 hello 직접 방법에 대 한 정보를 전송 하는 hello 장치.</span><span class="sxs-lookup"><span data-stu-id="0b6fa-116">hello device sends information about hello direct methods it supports using reported properties.</span></span>
   
    ```c
    // Define hello Model
    BEGIN_NAMESPACE(Contoso);

    /* Reported properties */
    DECLARE_STRUCT(SystemProperties,
      ascii_char_ptr, Manufacturer,
      ascii_char_ptr, FirmwareVersion,
      ascii_char_ptr, InstalledRAM,
      ascii_char_ptr, ModelNumber,
      ascii_char_ptr, Platform,
      ascii_char_ptr, Processor,
      ascii_char_ptr, SerialNumber
    );

    DECLARE_STRUCT(LocationProperties,
      double, Latitude,
      double, Longitude
    );

    DECLARE_STRUCT(ReportedDeviceProperties,
      ascii_char_ptr, DeviceState,
      LocationProperties, Location
    );

    DECLARE_MODEL(ConfigProperties,
      WITH_REPORTED_PROPERTY(double, TemperatureMeanValue),
      WITH_REPORTED_PROPERTY(uint8_t, TelemetryInterval)
    );

    /* Part of DeviceInfo */
    DECLARE_STRUCT(DeviceProperties,
      ascii_char_ptr, DeviceID,
      _Bool, HubEnabledState
    );

    DECLARE_DEVICETWIN_MODEL(Thermostat,
      /* Telemetry (temperature, external temperature and humidity) */
      WITH_DATA(double, Temperature),
      WITH_DATA(double, ExternalTemperature),
      WITH_DATA(double, Humidity),
      WITH_DATA(ascii_char_ptr, DeviceId),

      /* DeviceInfo */
      WITH_DATA(ascii_char_ptr, ObjectType),
      WITH_DATA(_Bool, IsSimulatedDevice),
      WITH_DATA(ascii_char_ptr, Version),
      WITH_DATA(DeviceProperties, DeviceProperties),

      /* Device twin properties */
      WITH_REPORTED_PROPERTY(ReportedDeviceProperties, Device),
      WITH_REPORTED_PROPERTY(ConfigProperties, Config),
      WITH_REPORTED_PROPERTY(SystemProperties, System),

      WITH_DESIRED_PROPERTY(double, TemperatureMeanValue, onDesiredTemperatureMeanValue),
      WITH_DESIRED_PROPERTY(uint8_t, TelemetryInterval, onDesiredTelemetryInterval),

      /* Direct methods implemented by hello device */
      WITH_METHOD(Reboot),
      WITH_METHOD(InitiateFirmwareUpdate, ascii_char_ptr, FwPackageURI),

      /* Register direct methods with solution portal */
      WITH_REPORTED_PROPERTY(ascii_char_ptr_no_quotes, SupportedMethods)
    );

    END_NAMESPACE(Contoso);
    ```

## <a name="implement-hello-behavior-of-hello-device"></a><span data-ttu-id="0b6fa-117">Hello 장치의 hello 동작 구현</span><span class="sxs-lookup"><span data-stu-id="0b6fa-117">Implement hello behavior of hello device</span></span>
<span data-ttu-id="0b6fa-118">이제 hello 모델에 정의 된 hello 동작을 구현 하는 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b6fa-118">Now add code that implements hello behavior defined in hello model.</span></span>

1. <span data-ttu-id="0b6fa-119">Hello 함수 hello 솔루션 대시보드에서 설정 hello 원하는 속성을 처리 하는 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b6fa-119">Add hello following functions that handle hello desired properties set in hello solution dashboard.</span></span> <span data-ttu-id="0b6fa-120">원하는 이러한 속성은 hello 모델에서 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b6fa-120">These desired properties are defined in hello model:</span></span>

    ```c
    void onDesiredTemperatureMeanValue(void* argument)
    {
      /* By convention 'argument' is of hello type of hello MODEL */
      Thermostat* thermostat = argument;
      printf("Received a new desired_TemperatureMeanValue = %f\r\n", thermostat->TemperatureMeanValue);

    }

    void onDesiredTelemetryInterval(void* argument)
    {
      /* By convention 'argument' is of hello type of hello MODEL */
      Thermostat* thermostat = argument;
      printf("Received a new desired_TelemetryInterval = %d\r\n", thermostat->TelemetryInterval);
    }
    ```

1. <span data-ttu-id="0b6fa-121">Hello 함수 hello IoT 허브를 통해 호출 된 hello 직접 메서드를 처리 하는 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b6fa-121">Add hello following functions that handle hello direct methods invoked through hello IoT hub.</span></span> <span data-ttu-id="0b6fa-122">이러한 직접 메서드 hello 모델에서 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b6fa-122">These direct methods are defined in hello model:</span></span>

    ```c
    /* Handlers for direct methods */
    METHODRETURN_HANDLE Reboot(Thermostat* thermostat)
    {
      (void)(thermostat);

      METHODRETURN_HANDLE result = MethodReturn_Create(201, "\"Rebooting\"");
      printf("Received reboot request\r\n");
      return result;
    }

    METHODRETURN_HANDLE InitiateFirmwareUpdate(Thermostat* thermostat, ascii_char_ptr FwPackageURI)
    {
      (void)(thermostat);

      METHODRETURN_HANDLE result = MethodReturn_Create(201, "\"Initiating Firmware Update\"");
      printf("Recieved firmware update request. Use package at: %s\r\n", FwPackageURI);
      return result;
    }
    ```

1. <span data-ttu-id="0b6fa-123">Hello 메시지 toohello 미리 구성 된 솔루션에 보내는 함수를 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b6fa-123">Add hello following function that sends a message toohello preconfigured solution:</span></span>
   
    ```c
    /* Send data tooIoT Hub */
    static void sendMessage(IOTHUB_CLIENT_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
    {
      IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
      if (messageHandle == NULL)
      {
        printf("unable toocreate a new IoTHubMessage\r\n");
      }
      else
      {
        if (IoTHubClient_SendEventAsync(iotHubClientHandle, messageHandle, NULL, NULL) != IOTHUB_CLIENT_OK)
        {
          printf("failed toohand over hello message tooIoTHubClient");
        }
        else
        {
          printf("IoTHubClient accepted hello message for delivery\r\n");
        }

        IoTHubMessage_Destroy(messageHandle);
      }
      free((void*)buffer);
    }
    ```

1. <span data-ttu-id="0b6fa-124">Hello 보내면 hello 장치에 새 보고 된 속성 값 toohello 미리 구성 된 솔루션을 실행 하는 콜백 처리기를 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b6fa-124">Add hello following callback handler that runs when hello device has sent new reported property values toohello preconfigured solution:</span></span>

    ```c
    /* Callback after sending reported properties */
    void deviceTwinCallback(int status_code, void* userContextCallback)
    {
      (void)(userContextCallback);
      printf("IoTHub: reported properties delivered with status_code = %u\n", status_code);
    }
    ```

1. <span data-ttu-id="0b6fa-125">Hello 다음 tooconnect hello 클라우드에서 장치 toohello 미리 구성 된 솔루션을 작동 하 고 데이터를 교환에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b6fa-125">Add hello following function tooconnect your device toohello preconfigured solution in hello cloud, and exchange data.</span></span> <span data-ttu-id="0b6fa-126">이 함수는 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b6fa-126">This function performs hello following steps:</span></span>

    - <span data-ttu-id="0b6fa-127">Hello 플랫폼을 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="0b6fa-127">Initializes hello platform.</span></span>
    - <span data-ttu-id="0b6fa-128">Hello serialization 라이브러리와 hello Contoso 네임 스페이스를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="0b6fa-128">Registers hello Contoso namespace with hello serialization library.</span></span>
    - <span data-ttu-id="0b6fa-129">Hello 장치 연결 문자열을 사용 하 여 hello 클라이언트를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="0b6fa-129">Initializes hello client with hello device connection string.</span></span>
    - <span data-ttu-id="0b6fa-130">Hello의 인스턴스를 만들고 **자동 온도 조절기** 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="0b6fa-130">Create an instance of hello **Thermostat** model.</span></span>
    - <span data-ttu-id="0b6fa-131">reported 속성 값을 만들고 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="0b6fa-131">Creates and sends reported property values.</span></span>
    - <span data-ttu-id="0b6fa-132">**DeviceInfo** 개체를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="0b6fa-132">Sends a **DeviceInfo** object.</span></span>
    - <span data-ttu-id="0b6fa-133">1 초 마다 루프 toosend 원격 분석을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b6fa-133">Creates a loop toosend telemetry every second.</span></span>
    - <span data-ttu-id="0b6fa-134">모든 리소스의 초기화를 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="0b6fa-134">Deinitializes all resources.</span></span>

      ```c
      void remote_monitoring_run(void)
      {
        if (platform_init() != 0)
        {
          printf("Failed tooinitialize hello platform.\n");
        }
        else
        {
          if (SERIALIZER_REGISTER_NAMESPACE(Contoso) == NULL)
          {
            printf("Unable tooSERIALIZER_REGISTER_NAMESPACE\n");
          }
          else
          {
            IOTHUB_CLIENT_HANDLE iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, MQTT_Protocol);
            if (iotHubClientHandle == NULL)
            {
              printf("Failure in IoTHubClient_CreateFromConnectionString\n");
            }
            else
            {
      #ifdef MBED_BUILD_TIMESTAMP
              // For mbed add hello certificate information
              if (IoTHubClient_SetOption(iotHubClientHandle, "TrustedCerts", certificates) != IOTHUB_CLIENT_OK)
              {
                  printf("Failed tooset option \"TrustedCerts\"\n");
              }
      #endif // MBED_BUILD_TIMESTAMP
              Thermostat* thermostat = IoTHubDeviceTwin_CreateThermostat(iotHubClientHandle);
              if (thermostat == NULL)
              {
                printf("Failure in IoTHubDeviceTwin_CreateThermostat\n");
              }
              else
              {
                /* Set values for reported properties */
                thermostat->Config.TemperatureMeanValue = 55.5;
                thermostat->Config.TelemetryInterval = 3;
                thermostat->Device.DeviceState = "normal";
                thermostat->Device.Location.Latitude = 47.642877;
                thermostat->Device.Location.Longitude = -122.125497;
                thermostat->System.Manufacturer = "Contoso Inc.";
                thermostat->System.FirmwareVersion = "2.22";
                thermostat->System.InstalledRAM = "8 MB";
                thermostat->System.ModelNumber = "DB-14";
                thermostat->System.Platform = "Plat 9.75";
                thermostat->System.Processor = "i3-7";
                thermostat->System.SerialNumber = "SER21";
                /* Specify hello signatures of hello supported direct methods */
                thermostat->SupportedMethods = "{\"Reboot\": \"Reboot hello device\", \"InitiateFirmwareUpdate--FwPackageURI-string\": \"Updates device Firmware. Use parameter FwPackageURI toospecifiy hello URI of hello firmware file\"}";

                /* Send reported properties tooIoT Hub */
                if (IoTHubDeviceTwin_SendReportedStateThermostat(thermostat, deviceTwinCallback, NULL) != IOTHUB_CLIENT_OK)
                {
                  printf("Failed sending serialized reported state\n");
                }
                else
                {
                  printf("Send DeviceInfo object tooIoT Hub at startup\n");
      
                  thermostat->ObjectType = "DeviceInfo";
                  thermostat->IsSimulatedDevice = 0;
                  thermostat->Version = "1.0";
                  thermostat->DeviceProperties.HubEnabledState = 1;
                  thermostat->DeviceProperties.DeviceID = (char*)deviceId;

                  unsigned char* buffer;
                  size_t bufferSize;

                  if (SERIALIZE(&buffer, &bufferSize, thermostat->ObjectType, thermostat->Version, thermostat->IsSimulatedDevice, thermostat->DeviceProperties) != CODEFIRST_OK)
                  {
                    (void)printf("Failed serializing DeviceInfo\n");
                  }
                  else
                  {
                    sendMessage(iotHubClientHandle, buffer, bufferSize);
                  }

                  /* Send telemetry */
                  thermostat->Temperature = 50;
                  thermostat->ExternalTemperature = 55;
                  thermostat->Humidity = 50;
                  thermostat->DeviceId = (char*)deviceId;

                  while (1)
                  {
                    unsigned char*buffer;
                    size_t bufferSize;

                    (void)printf("Sending sensor value Temperature = %f, Humidity = %f\n", thermostat->Temperature, thermostat->Humidity);

                    if (SERIALIZE(&buffer, &bufferSize, thermostat->DeviceId, thermostat->Temperature, thermostat->Humidity, thermostat->ExternalTemperature) != CODEFIRST_OK)
                    {
                      (void)printf("Failed sending sensor value\r\n");
                    }
                    else
                    {
                      sendMessage(iotHubClientHandle, buffer, bufferSize);
                    }

                    ThreadAPI_Sleep(1000);
                  }

                  IoTHubDeviceTwin_DestroyThermostat(thermostat);
                }
              }
              IoTHubClient_Destroy(iotHubClientHandle);
            }
            serializer_deinit();
          }
        }
        platform_deinit();
      }
    ```
   
    <span data-ttu-id="0b6fa-135">참조용으로 다음은 샘플 **원격 분석** 보낸 메시지 toohello 미리 솔루션 구성:</span><span class="sxs-lookup"><span data-stu-id="0b6fa-135">For reference, here is a sample **Telemetry** message sent toohello preconfigured solution:</span></span>
   
    ```
    {"DeviceId":"mydevice01", "Temperature":50, "Humidity":50, "ExternalTemperature":55}
    ```