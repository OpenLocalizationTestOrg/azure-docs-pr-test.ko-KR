## <a name="create-a-device-identity"></a>장치 ID 만들기

이 섹션에서는 라는 Node.js 도구를 사용 하면 [iothub 탐색기] [ iot-hub-explorer] toocreate이이 자습서에 대 한 장치 id입니다. 장치 ID는 대/소문자를 구분합니다.

1. Hello 다음 명령줄 환경에서 실행 합니다.

    `npm install -g iothub-explorer@latest`

1. 다음 명령은 toologin tooyour 허브 hello를 실행 하십시오. 대체 `{iot hub connection string}` IoT 허브 연결 문자열을 이전에 복사한 hello로:

    `iothub-explorer login "{iot hub connection string}"`

1. 마지막으로 호출 하 여 새 장치 id를 만들 `myDeviceId` hello 명령을 사용 하 여:

    `iothub-explorer create myDeviceId --connection-string`

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

Hello 결과에서 hello 장치 연결 문자열을 기록해 둡니다. 이 장치 연결 문자열은 장치로 hello 장치 앱 tooconnect tooyour IoT 허브에서 사용 됩니다.

![][img-identity]

너무 참조[IoT 허브 시작] [ lnk-getstarted] tooprogrammatically 장치 id를 만들 수 있습니다.

<!-- images and links -->
[img-identity]: media/iot-hub-get-started-create-device-identity/devidentity.png

[iot-hub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md

[lnk-getstarted]: ../articles/iot-hub/iot-hub-csharp-csharp-getstarted.md
