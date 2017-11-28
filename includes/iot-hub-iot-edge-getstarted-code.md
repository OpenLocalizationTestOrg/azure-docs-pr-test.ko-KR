## <a name="typical-output"></a><span data-ttu-id="baa06-101">일반적인 출력</span><span class="sxs-lookup"><span data-stu-id="baa06-101">Typical output</span></span>

<span data-ttu-id="baa06-102">다음은 Hello World 샘플을 통해 로그 파일에 기록된 출력의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-102">The following example shows the output written to the log file by the Hello World sample.</span></span> <span data-ttu-id="baa06-103">쉽게 읽을 수 있도록 출력 형식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-103">The output is formatted for legibility:</span></span>

```json
[{
    "time": "Mon Apr 11 13:48:07 2016",
    "content": "Log started"
}, {
    "time": "Mon Apr 11 13:48:48 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:48:55 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:49:01 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:49:04 2016",
    "content": "Log stopped"
}]
```

## <a name="code-snippets"></a><span data-ttu-id="baa06-104">코드 조각</span><span class="sxs-lookup"><span data-stu-id="baa06-104">Code snippets</span></span>

<span data-ttu-id="baa06-105">이 섹션은 hello\_world 샘플에서 코드의 일부 주요 섹션을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-105">This section discusses some key sections of the code in the hello\_world sample.</span></span>

### <a name="iot-edge-gateway-creation"></a><span data-ttu-id="baa06-106">IoT Edge 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="baa06-106">IoT Edge gateway creation</span></span>

<span data-ttu-id="baa06-107">*게이트웨이 프로세스*를 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-107">You must implement a *gateway process*.</span></span> <span data-ttu-id="baa06-108">이 프로그램은 내부 인프라(broker)를 만들고, IoT Edge 모듈을 로드하며, 게이트웨이 프로세스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-108">This program creates the internal infrastructure (the broker), loads the IoT Edge modules, and configures the gateway process.</span></span> <span data-ttu-id="baa06-109">IoT Edge는 JSON 파일에서 게이트웨이를 부트스트랩할 수 있도록 **Gateway\_Create\_From\_JSON** 함수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-109">IoT Edge provides the **Gateway\_Create\_From\_JSON** function to enable you to bootstrap a gateway from a JSON file.</span></span> <span data-ttu-id="baa06-110">**Gateway\_Create\_From\_JSON** 함수를 사용하려면 로드할 IoT Edge 모듈을 지정하는 JSON 파일에 대한 경로를 이 함수에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-110">To use the **Gateway\_Create\_From\_JSON** function, pass it the path to a JSON file that specifies the IoT Edge modules to load.</span></span>

<span data-ttu-id="baa06-111">*Hello World* 샘플의 게이트웨이 프로세스에 대한 코드는 [main.c][lnk-main-c] 파일에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-111">You can find the code for the gateway process in the *Hello World* sample in the [main.c][lnk-main-c] file.</span></span> <span data-ttu-id="baa06-112">읽기 쉽도록, 다음 코드 조각에서는 게이트웨이 프로세스 코드의 간략한 버전을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-112">For legibility, the following snippet shows an abbreviated version of the gateway process code.</span></span> <span data-ttu-id="baa06-113">이 예제 프로그램은 게이트웨이를 만든 다음 게이트웨이를 허물기 전에 사용자가 **ENTER** 키를 누를 때까지 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-113">This example program creates a gateway and then waits for the user to press the **ENTER** key before it tears down the gateway.</span></span>

```c
int main(int argc, char** argv)
{
    GATEWAY_HANDLE gateway;
    if ((gateway = Gateway_Create_From_JSON(argv[1])) == NULL)
    {
        printf("failed to create the gateway from JSON\n");
    }
    else
    {
        printf("gateway successfully created from JSON\n");
        printf("gateway shall run until ENTER is pressed\n");
        (void)getchar();
        Gateway_LL_Destroy(gateway);
    }
    return 0;
}
```

<span data-ttu-id="baa06-114">JSON 설정 파일에는 로드할 IoT Edge 모듈의 목록과 모듈 간의 링크가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-114">The JSON settings file contains a list of IoT Edge modules to load and the links between the modules.</span></span> <span data-ttu-id="baa06-115">각각의 IoT Edge 모듈에서 다음을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-115">Each IoT Edge module must specify a:</span></span>

* <span data-ttu-id="baa06-116">**name**: 모듈의 고유한 이름.</span><span class="sxs-lookup"><span data-stu-id="baa06-116">**name**: a unique name for the module.</span></span>
* <span data-ttu-id="baa06-117">**loader**: 원하는 모듈을 로드하는 방법을 알고 있는 로더.</span><span class="sxs-lookup"><span data-stu-id="baa06-117">**loader**: a loader that knows how to load the desired module.</span></span> <span data-ttu-id="baa06-118">로더는 다양한 유형의 모듈을 로드하기 위한 확장 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-118">Loaders are an extension point for loading different types of modules.</span></span> <span data-ttu-id="baa06-119">IoT Edge는 Native C, Node.js, Java 및 .NET으로 작성된 모듈을 사용하기 위해 로더를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-119">IoT Edge provides loaders for use with modules written in native C, Node.js, Java, and .NET.</span></span> <span data-ttu-id="baa06-120">헬로 월드 샘플에 있는 모든 모듈이 C 언어로 작성된 동적 라이브러리이므로 이 샘플에서는 네이티브 C 로더만 사용합니다. 다른 언어로 작성된 IoT Edge 모듈을 사용하는 방법에 대한 자세한 내용은 [Node.js](https://github.com/Azure/iot-edge/blob/master/samples/nodejs_simple_sample/), [Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample) 또는 [.NET](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample) 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="baa06-120">The Hello World sample only uses the native C loader because all the modules in this sample are dynamic libraries written in C. For more information about how to use IoT Edge modules written in different languages, see the [Node.js](https://github.com/Azure/iot-edge/blob/master/samples/nodejs_simple_sample/), [Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample), or [.NET](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample) samples.</span></span>
    * <span data-ttu-id="baa06-121">**name**: 모듈을 로드하는 데 사용되는 로더의 이름.</span><span class="sxs-lookup"><span data-stu-id="baa06-121">**name**: the name of the loader used to load the module.</span></span>
    * <span data-ttu-id="baa06-122">**entrypoint**: 모듈을 포함하는 라이브러리에 대한 경로.</span><span class="sxs-lookup"><span data-stu-id="baa06-122">**entrypoint**: the path to the library containing the module.</span></span> <span data-ttu-id="baa06-123">이 라이브러리는 Linux에서 .so 파일이고 Windows에서 .dll 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-123">On Linux this library is a .so file, on Windows this library is a .dll file.</span></span> <span data-ttu-id="baa06-124">진입점은 사용된 로더의 유형에 따라 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-124">The entry point is specific to the type of loader being used.</span></span> <span data-ttu-id="baa06-125">Node.js 로더의 진입점은 .js 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-125">The Node.js loader entry point is a .js file.</span></span> <span data-ttu-id="baa06-126">Java 로더의 진입점은 클래스 경로와 클래스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-126">The Java loader entry point is a classpath and a class name.</span></span> <span data-ttu-id="baa06-127">.NET 로더의 진입점은 어셈블리 이름과 클래스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-127">The .NET loader entry point is an assembly name and a class name.</span></span>

* <span data-ttu-id="baa06-128">**args**: 모듈에 필요한 구성 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-128">**args**: any configuration information the module needs.</span></span>

<span data-ttu-id="baa06-129">다음 코드에서는 Linux에서 헬로 월드 샘플에 대한 모든 IoT Edge 모듈을 선언하는 데 사용된 JSON을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-129">The following code shows the JSON used to declare all the IoT Edge modules for the Hello World sample on Linux.</span></span> <span data-ttu-id="baa06-130">모듈에 인수가 필요한지 여부는 모듈의 디자인에 달려 있습니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-130">Whether a module requires any arguments depends on the design of the module.</span></span> <span data-ttu-id="baa06-131">이 예에서 로거 모듈은 출력 파일에 대한 경로를 인수로 사용하고 hello\_world 모듈에는 인수가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-131">In this example, the logger module takes an argument that is the path to the output file and the hello\_world module has no arguments.</span></span>

```json
"modules" :
[
    {
        "name" : "logger",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "./modules/logger/liblogger.so"
        }
        },
        "args" : {"filename":"log.txt"}
    },
    {
        "name" : "hello_world",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "./modules/hello_world/libhello_world.so"
        }
        },
        "args" : null
    }
]
```

<span data-ttu-id="baa06-132">또한 JSON 파일에는 broker에 전달되는 모듈 간의 링크가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-132">The JSON file also contains the links between the modules that are passed to the broker.</span></span> <span data-ttu-id="baa06-133">링크에는 두 가지 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-133">A link has two properties:</span></span>

* <span data-ttu-id="baa06-134">**source**: `modules` 섹션 또는 `\*`의 모듈 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-134">**source**: a module name from the `modules` section, or `\*`.</span></span>
* <span data-ttu-id="baa06-135">**sink**: `modules` 섹션의 모듈 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-135">**sink**: a module name from the `modules` section.</span></span>

<span data-ttu-id="baa06-136">각 링크는 메시지 경로 및 방향을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-136">Each link defines a message route and direction.</span></span> <span data-ttu-id="baa06-137">**source** 모듈의 메시지는 **sink** 모듈에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-137">Messages from the **source** module are delivered to the **sink** module.</span></span> <span data-ttu-id="baa06-138">**source** 모듈을 `\*`로 설정할 수 있습니다. 이것은 **sink** 모듈이 모든 모듈에서 메시지를 수신함을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-138">You can set the **source** module to `\*`, which indicates that the **sink** module receives messages from any module.</span></span>

<span data-ttu-id="baa06-139">다음 코드에서는 Linux의 hello\_world 샘플에서 사용된 모듈 간의 링크를 구성하는 데 사용된 JSON을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-139">The following code shows the JSON used to configure links between the modules used in the hello\_world sample on Linux.</span></span> <span data-ttu-id="baa06-140">모듈 `hello_world`에 의해 생성된 모든 메시지는 모듈 `logger`에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-140">Every message produced by the `hello_world` module is consumed by the `logger` module.</span></span>

```json
"links":
[
    {
        "source": "hello_world",
        "sink": "logger"
    }
]
```

### <a name="helloworld-module-message-publishing"></a><span data-ttu-id="baa06-141">Hello\_world 모듈 메시지 게시</span><span class="sxs-lookup"><span data-stu-id="baa06-141">Hello\_world module message publishing</span></span>

<span data-ttu-id="baa06-142">메시지를 게시하기 위해 hello\_world 모듈에 사용되는 코드는 ['hello_world.c'][lnk-helloworld-c] 파일에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-142">You can find the code used by the hello\_world module to publish messages in the ['hello_world.c'][lnk-helloworld-c] file.</span></span> <span data-ttu-id="baa06-143">다음 코드 조각은 읽기 쉽도록 코멘트가 추가되고 일부 오류 처리 코드가 제거된 수정 버전을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-143">The following snippet shows an amended version of the code with comments added and some error handling code removed for legibility:</span></span>

```c
int helloWorldThread(void *param)
{
    // create data structures used in function.
    HELLOWORLD_HANDLE_DATA* handleData = param;
    MESSAGE_CONFIG msgConfig;
    MAP_HANDLE propertiesMap = Map_Create(NULL);

    // add a property named "helloWorld" with a value of "from Azure IoT
    // Gateway SDK simple sample!" to a set of message properties that
    // will be appended to the message before publishing it. 
    Map_AddOrUpdate(propertiesMap, "helloWorld", "from Azure IoT Gateway SDK simple sample!")

    // set the content for the message
    msgConfig.size = strlen(HELLOWORLD_MESSAGE);
    msgConfig.source = HELLOWORLD_MESSAGE;

    // set the properties for the message
    msgConfig.sourceProperties = propertiesMap;

    // create a message based on the msgConfig structure
    MESSAGE_HANDLE helloWorldMessage = Message_Create(&msgConfig);

    while (1)
    {
        if (handleData->stopThread)
        {
            (void)Unlock(handleData->lockHandle);
            break; /*gets out of the thread*/
        }
        else
        {
            // publish the message to the broker
            (void)Broker_Publish(handleData->brokerHandle, helloWorldMessage);
            (void)Unlock(handleData->lockHandle);
        }

        (void)ThreadAPI_Sleep(5000); /*every 5 seconds*/
    }

    Message_Destroy(helloWorldMessage);

    return 0;
}
```

### <a name="helloworld-module-message-processing"></a><span data-ttu-id="baa06-144">Hello\_world 모듈 메시지 처리</span><span class="sxs-lookup"><span data-stu-id="baa06-144">Hello\_world module message processing</span></span>

<span data-ttu-id="baa06-145">hello\_world 모듈에서는 다른 IoT Edge 모듈이 broker에 게시하는 메시지를 절대로 처리하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-145">The hello\_world module never processes messages that other IoT Edge modules publish to the broker.</span></span> <span data-ttu-id="baa06-146">따라서 hello\_world 모듈에서 메시지 콜백의 구현은 수행되지 않는 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-146">Therefore, the implementation of the message callback in the hello\_world module is a no-op function.</span></span>

```c
static void HelloWorld_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{
    /* No action, HelloWorld is not interested in any messages. */
}
```

### <a name="logger-module-message-publishing-and-processing"></a><span data-ttu-id="baa06-147">로거 모듈 메시지 게시 및 처리</span><span class="sxs-lookup"><span data-stu-id="baa06-147">Logger module message publishing and processing</span></span>

<span data-ttu-id="baa06-148">로거 모듈은 broker에서 메시지를 수신하고 파일에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-148">The logger module receives messages from the broker and writes them to a file.</span></span> <span data-ttu-id="baa06-149">메시지를 게시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-149">It never publishes any messages.</span></span> <span data-ttu-id="baa06-150">따라서 로거 모듈의 코드는 **Broker_Publish** 함수를 절대 호출하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-150">Therefore, the code of the logger module never calls the **Broker_Publish** function.</span></span>

<span data-ttu-id="baa06-151">[logger.c][lnk-logger-c] 파일의 **Logger_Recieve** 함수는 broker가 로거 모듈에 메시지를 전달하기 위해 호출하는 콜백입니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-151">The **Logger_Receive** function in the [logger.c][lnk-logger-c] file is the callback the broker invokes to deliver messages to the logger module.</span></span> <span data-ttu-id="baa06-152">다음 코드 조각은 읽기 쉽도록 코멘트가 추가되고 일부 오류 처리 코드가 제거된 수정 버전을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-152">The following snippet shows an amended version with comments added and some error handling code removed for legibility:</span></span>

```c
static void Logger_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{

    time_t temp = time(NULL);
    struct tm* t = localtime(&temp);
    char timetemp[80] = { 0 };

    // Get the message properties from the message
    CONSTMAP_HANDLE originalProperties = Message_GetProperties(messageHandle); 
    MAP_HANDLE propertiesAsMap = ConstMap_CloneWriteable(originalProperties);

    // Convert the collection of properties into a JSON string
    STRING_HANDLE jsonProperties = Map_ToJSON(propertiesAsMap);

    //  base64 encode the message content
    const CONSTBUFFER * content = Message_GetContent(messageHandle);
    STRING_HANDLE contentAsJSON = Base64_Encode_Bytes(content->buffer, content->size);

    // Start the construction of the final string to be logged by adding
    // the timestamp
    STRING_HANDLE jsonToBeAppended = STRING_construct(",{\"time\":\"");
    STRING_concat(jsonToBeAppended, timetemp);

    // Add the message properties
    STRING_concat(jsonToBeAppended, "\",\"properties\":"); 
    STRING_concat_with_STRING(jsonToBeAppended, jsonProperties);

    // Add the content
    STRING_concat(jsonToBeAppended, ",\"content\":\"");
    STRING_concat_with_STRING(jsonToBeAppended, contentAsJSON);
    STRING_concat(jsonToBeAppended, "\"}]");

    // Write the formatted string
    LOGGER_HANDLE_DATA *handleData = (LOGGER_HANDLE_DATA *)moduleHandle;
    addJSONString(handleData->fout, STRING_c_str(jsonToBeAppended);
}
```

## <a name="next-steps"></a><span data-ttu-id="baa06-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="baa06-153">Next steps</span></span>

<span data-ttu-id="baa06-154">이 문서에서는 메시지를 로그 파일에 기록하는 단순한 IoT Edge 게이트웨이를 실행했습니다.</span><span class="sxs-lookup"><span data-stu-id="baa06-154">In this article, you ran a simple IoT Edge gateway that writes messages to a log file.</span></span> <span data-ttu-id="baa06-155">메시지를 IoT Hub에 보내는 샘플을 실행하려면 [IoT Edge – Linux를 사용하는 시뮬레이션된 장치에서 장치-클라우드 메시지 보내기][lnk-gateway-simulated-linux] 또는 [IoT Edge – Windows를 사용하는 시뮬레이션된 장치에서 장치-클라우드 메시지 보내기][lnk-gateway-simulated-windows]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="baa06-155">To run a sample that sends messages to IoT Hub, see [IoT Edge – send device-to-cloud messages with a simulated device using Linux][lnk-gateway-simulated-linux] or [IoT Edge – send device-to-cloud messages with a simulated device using Windows][lnk-gateway-simulated-windows].</span></span>


<!-- Links -->
[lnk-main-c]: https://github.com/Azure/iot-edge/blob/master/samples/hello_world/src/main.c
[lnk-helloworld-c]: https://github.com/Azure/iot-edge/blob/master/modules/hello_world/src/hello_world.c
[lnk-logger-c]: https://github.com/Azure/iot-edge/blob/master/modules/logger/src/logger.c
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-gateway-simulated-linux]: ../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md
[lnk-gateway-simulated-windows]: ../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md