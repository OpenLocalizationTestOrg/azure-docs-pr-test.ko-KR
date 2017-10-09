## <a name="create-a-device-identity"></a><span data-ttu-id="4655b-101">장치 ID 만들기</span><span class="sxs-lookup"><span data-stu-id="4655b-101">Create a device identity</span></span>

<span data-ttu-id="4655b-102">이 섹션에서는 라는 Node.js 도구를 사용 하면 [iothub 탐색기] [ iot-hub-explorer] toocreate이이 자습서에 대 한 장치 id입니다.</span><span class="sxs-lookup"><span data-stu-id="4655b-102">In this section, you use a Node.js tool called [iothub-explorer][iot-hub-explorer] toocreate a device identity for this tutorial.</span></span> <span data-ttu-id="4655b-103">장치 ID는 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="4655b-103">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="4655b-104">Hello 다음 명령줄 환경에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4655b-104">Run hello following in your command-line environment:</span></span>

    `npm install -g iothub-explorer@latest`

1. <span data-ttu-id="4655b-105">다음 명령은 toologin tooyour 허브 hello를 실행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="4655b-105">Then, run hello following command toologin tooyour hub.</span></span> <span data-ttu-id="4655b-106">대체 `{iot hub connection string}` IoT 허브 연결 문자열을 이전에 복사한 hello로:</span><span class="sxs-lookup"><span data-stu-id="4655b-106">Substitute `{iot hub connection string}` with hello IoT Hub connection string you previously copied:</span></span>

    `iothub-explorer login "{iot hub connection string}"`

1. <span data-ttu-id="4655b-107">마지막으로 호출 하 여 새 장치 id를 만들 `myDeviceId` hello 명령을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="4655b-107">Finally, create a new device identity called `myDeviceId` with hello command:</span></span>

    `iothub-explorer create myDeviceId --connection-string`

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

<span data-ttu-id="4655b-108">Hello 결과에서 hello 장치 연결 문자열을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="4655b-108">Make a note of hello device connection string from hello result.</span></span> <span data-ttu-id="4655b-109">이 장치 연결 문자열은 장치로 hello 장치 앱 tooconnect tooyour IoT 허브에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4655b-109">This device connection string is used by hello device app tooconnect tooyour IoT Hub as a device.</span></span>

![][img-identity]

<span data-ttu-id="4655b-110">너무 참조[IoT 허브 시작] [ lnk-getstarted] tooprogrammatically 장치 id를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4655b-110">Refer too[Getting started with IoT Hub][lnk-getstarted] tooprogrammatically create device identities.</span></span>

<!-- images and links -->
[img-identity]: media/iot-hub-get-started-create-device-identity/devidentity.png

[iot-hub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md

[lnk-getstarted]: ../articles/iot-hub/iot-hub-csharp-csharp-getstarted.md
