## <a name="typical-output"></a>일반적인 출력

hello 다음 예제에서는 hello 출력을 표시 hello Hello World 예제가 toohello 로그 파일을 작성 합니다. 쉽게 읽을 수 있도록 hello 출력 서식을 지정 합니다.

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

## <a name="code-snippets"></a>코드 조각

이 섹션에서는 몇 가지 주요 hello에서에서 섹션 hello hello\_world 예제 추가 정보입니다.

### <a name="iot-edge-gateway-creation"></a>IoT Edge 게이트웨이 만들기

*게이트웨이 프로세스*를 구현해야 합니다. Hello 내부 인프라 (hello 브로커) 만들어지고 hello IoT 가장자리 모듈 로드 hello 게이트웨이 프로세스를 구성 하는이 프로그램 됩니다. IoT 가장자리 제공 hello **게이트웨이\_만들기\_에서\_JSON** tooenable 함수 toobootstrap JSON 파일에서 게이트웨이 합니다. toouse hello **게이트웨이\_만들기\_에서\_JSON** 함수 hello 모듈 tooload IoT 가장자리를 지정 하는 hello 경로 tooa JSON 파일을 전달 합니다.

Hello 게이트웨이 프로세스 hello에 대 한 hello 코드를 찾을 수 *Hello World* hello 샘플 [main.c] [ lnk-main-c] 파일입니다. 쉽게 읽을 수 있도록, hello 다음 코드 조각에서는 hello 게이트웨이 프로세스 코드의 축약된 버전 이 예제 프로그램 게이트웨이 만들고 hello 사용자 toopress hello 후 대기 **ENTER** hello 게이트웨이 해제 하기 전에 키입니다.

```c
int main(int argc, char** argv)
{
    GATEWAY_HANDLE gateway;
    if ((gateway = Gateway_Create_From_JSON(argv[1])) == NULL)
    {
        printf("failed toocreate hello gateway from JSON\n");
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

hello JSON 설정 파일 IoT 가장자리 모듈 tooload 및 hello 모듈 간에 hello 링크 목록이 포함 되어 있습니다. 각각의 IoT Edge 모듈에서 다음을 지정해야 합니다.

* **이름**: hello 모듈에 대 한 고유 이름입니다.
* **로더**: tooload hello 모듈을 원하는 하는 방법을 알고 있는 로더 합니다. 로더는 다양한 유형의 모듈을 로드하기 위한 확장 지점입니다. IoT Edge는 Native C, Node.js, Java 및 .NET으로 작성된 모듈을 사용하기 위해 로더를 제공합니다. 이 샘플의 모든 hello 모듈은 C 언어로 작성 된 동적 라이브러리 때문에 hello 네이티브 C 로더를 사용 hello Hello World 예제 추가 정보 방법에 대 한 자세한 내용은 다른 언어로 작성 된 toouse IoT 가장자리 모듈 참조 hello [Node.js](https://github.com/Azure/iot-edge/blob/master/samples/nodejs_simple_sample/), [Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample), 또는 [.NET](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample) 샘플입니다.
    * **이름**: hello 로더 hello 이름이 tooload hello 모듈을 사용 합니다.
    * **entrypoint**: hello 모듈을 포함 하는 hello 경로 toohello 라이브러리입니다. 이 라이브러리는 Linux에서 .so 파일이고 Windows에서 .dll 파일입니다. hello 진입점에는 로더를 사용 하 고 특정 toohello 유형입니다. Node.js 로더 진입점 hello.js 파일입니다. hello Java 로더 진입점 클래스는 경로 이며 클래스 이름입니다. hello.NET 로더 진입점은 어셈블리 이름 및 클래스 이름입니다.

* **args**: 모든 구성 정보 hello 모듈 필요 합니다.

다음 코드에서는 hello 사용 되는 JSON toodeclare 모든 hello hello linux hello Hello World 예제 추가 정보에 대 한 IoT 가장자리 모듈입니다. 모듈 인수를 필요한 지 여부를 hello 모듈의 hello 디자인에 따라 달라 집니다. 이 예제에서는 hello로 거 모듈은 hello 경로 toohello 출력 파일이 며 hello hello 되는 인수\_세계 모듈에 인수가 없습니다.

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

hello JSON 파일에는 또한 toohello broker 전달 되는 hello 모듈 간에 hello 링크가 포함 되어 있습니다. 링크에는 두 가지 속성이 있습니다.

* **소스**: hello에서 모듈 이름을 `modules` 섹션 또는 `\*`합니다.
* **싱크**: hello에서 모듈 이름을 `modules` 섹션.

각 링크는 메시지 경로 및 방향을 정의합니다. Hello 메시지 **소스** 모듈 제공 되며, toohello **싱크** 모듈입니다. Hello를 설정할 수 있습니다 **소스** 모듈 너무`\*`, 해당 hello 나타냅니다 **싱크** 모듈 모든 모듈에서 메시지를 수신 합니다.

hello 다음 코드를 보여 줍니다 hello hello에 사용 되는 hello 모듈 간의 tooconfigure 링크를 사용 하는 hello JSON\_linux world 예제 추가 정보입니다. Hello에서 모든 메시지 생성 `hello_world` hello에서 모듈 사용 `logger` 모듈입니다.

```json
"links":
[
    {
        "source": "hello_world",
        "sink": "logger"
    }
]
```

### <a name="helloworld-module-message-publishing"></a>Hello\_world 모듈 메시지 게시

Hello hello에서 사용 하는 hello 코드를 찾을 수 있습니다\_hello world 모듈 toopublish 메시지 ['hello_world.c'] [ lnk-helloworld-c] 파일입니다. hello 다음 코드 조각은 함께 보여 줍니다 수정 된 버전의 hello 코드 주석 추가 및 오류 처리 코드를 쉽게 읽을 수 있도록 제거.

```c
int helloWorldThread(void *param)
{
    // create data structures used in function.
    HELLOWORLD_HANDLE_DATA* handleData = param;
    MESSAGE_CONFIG msgConfig;
    MAP_HANDLE propertiesMap = Map_Create(NULL);

    // add a property named "helloWorld" with a value of "from Azure IoT
    // Gateway SDK simple sample!" tooa set of message properties that
    // will be appended toohello message before publishing it. 
    Map_AddOrUpdate(propertiesMap, "helloWorld", "from Azure IoT Gateway SDK simple sample!")

    // set hello content for hello message
    msgConfig.size = strlen(HELLOWORLD_MESSAGE);
    msgConfig.source = HELLOWORLD_MESSAGE;

    // set hello properties for hello message
    msgConfig.sourceProperties = propertiesMap;

    // create a message based on hello msgConfig structure
    MESSAGE_HANDLE helloWorldMessage = Message_Create(&msgConfig);

    while (1)
    {
        if (handleData->stopThread)
        {
            (void)Unlock(handleData->lockHandle);
            break; /*gets out of hello thread*/
        }
        else
        {
            // publish hello message toohello broker
            (void)Broker_Publish(handleData->brokerHandle, helloWorldMessage);
            (void)Unlock(handleData->lockHandle);
        }

        (void)ThreadAPI_Sleep(5000); /*every 5 seconds*/
    }

    Message_Destroy(helloWorldMessage);

    return 0;
}
```

### <a name="helloworld-module-message-processing"></a>Hello\_world 모듈 메시지 처리

hello hello\_세계 모듈에서 다른 IoT 가장자리 모듈 toohello 브로커를 게시 메시지를 처리 하지 않습니다. 따라서 hello hello에 hello 메시지 콜백 구현의 hello\_세계 모듈은 아무 함수입니다.

```c
static void HelloWorld_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{
    /* No action, HelloWorld is not interested in any messages. */
}
```

### <a name="logger-module-message-publishing-and-processing"></a>로거 모듈 메시지 게시 및 처리

hello로 거 모듈 hello broker에서 메시지를 수신 하 고 tooa 파일에 기록 합니다. 메시지를 게시하지 않습니다. 따라서 hello로 거 모듈의 hello 코드를 호출 하지 않습니다 hello **Broker_Publish** 함수입니다.

hello **Logger_Receive** 함수 hello에 [logger.c] [ lnk-logger-c] 파일은 hello 콜백 hello 브로커 toodeliver 메시지 toohello로 거 모듈을 호출 합니다. hello 다음 코드 조각은 함께 보여 줍니다 수정 된 버전 주석 추가 및 오류 처리 코드를 쉽게 읽을 수 있도록 제거.

```c
static void Logger_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{

    time_t temp = time(NULL);
    struct tm* t = localtime(&temp);
    char timetemp[80] = { 0 };

    // Get hello message properties from hello message
    CONSTMAP_HANDLE originalProperties = Message_GetProperties(messageHandle); 
    MAP_HANDLE propertiesAsMap = ConstMap_CloneWriteable(originalProperties);

    // Convert hello collection of properties into a JSON string
    STRING_HANDLE jsonProperties = Map_ToJSON(propertiesAsMap);

    //  base64 encode hello message content
    const CONSTBUFFER * content = Message_GetContent(messageHandle);
    STRING_HANDLE contentAsJSON = Base64_Encode_Bytes(content->buffer, content->size);

    // Start hello construction of hello final string toobe logged by adding
    // hello timestamp
    STRING_HANDLE jsonToBeAppended = STRING_construct(",{\"time\":\"");
    STRING_concat(jsonToBeAppended, timetemp);

    // Add hello message properties
    STRING_concat(jsonToBeAppended, "\",\"properties\":"); 
    STRING_concat_with_STRING(jsonToBeAppended, jsonProperties);

    // Add hello content
    STRING_concat(jsonToBeAppended, ",\"content\":\"");
    STRING_concat_with_STRING(jsonToBeAppended, contentAsJSON);
    STRING_concat(jsonToBeAppended, "\"}]");

    // Write hello formatted string
    LOGGER_HANDLE_DATA *handleData = (LOGGER_HANDLE_DATA *)moduleHandle;
    addJSONString(handleData->fout, STRING_c_str(jsonToBeAppended);
}
```

## <a name="next-steps"></a>다음 단계

이 문서에서는 메시지 tooa 로그 파일에 기록 하는 간단한 IoT 지 게이트웨이 실행 했습니다. 보내는 메시지 tooIoT 허브 샘플 toorun 참조 [IoT 가장자리 – Linux를 사용 하는 시뮬레이션 된 장치를 사용 하 여 장치-클라우드 메시지를 보냅니다] [ lnk-gateway-simulated-linux] 또는 [IoT 가장자리 – 장치-클라우드 메시지를 보낼는 Windows를 사용 하 여 시뮬레이션 된 장치][lnk-gateway-simulated-windows]합니다.


<!-- Links -->
[lnk-main-c]: https://github.com/Azure/iot-edge/blob/master/samples/hello_world/src/main.c
[lnk-helloworld-c]: https://github.com/Azure/iot-edge/blob/master/modules/hello_world/src/hello_world.c
[lnk-logger-c]: https://github.com/Azure/iot-edge/blob/master/modules/logger/src/logger.c
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-gateway-simulated-linux]: ../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md
[lnk-gateway-simulated-windows]: ../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md