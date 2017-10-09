## <a name="create-a-device-identity"></a>장치 ID 만들기

이 섹션을 사용 하 여 hello [Azure 포털] [ lnk-azure-portal] toocreate hello id 레지스트리에 IoT 허브에서에서 장치 id입니다. 장치 id 레지스트리에 hello에 항목이 없는 경우 tooIoT 허브를 연결할 수 없습니다. 자세한 내용은 hello의 hello "Id 레지스트리에" 섹션을 참조 [IoT 허브 개발자 가이드][lnk-devguide-identity]합니다. hello **장치 탐색기** hello에 포털을 통해 고유한 장치 ID와 tooIoT 허브에 연결할 때 장치에서 tooidentify 자체를 사용할 수 있는 키를 생성할 수 있습니다. 장치 ID는 대/소문자를 구분합니다.

1. Toohello 로그인 되어 있는지 확인 [Azure 포털][lnk-azure-portal]합니다.

1. Hello Jumpbar, 클릭 **모든 리소스** IoT 허브 리소스를 찾습니다.

    ![Tooyour Iot 허브를 이동 합니다.][img-find-iothub]

1. IoT 허브 리소스를 열 때 클릭 hello **장치 탐색기** 도구를 클릭 한 다음 클릭 **추가** hello 위쪽에 있습니다. 새 장치에 대 한 hello 이름 같은 제공 **myDeviceId**를 클릭 하 고 **저장**합니다.

    ![포털에서 장치 ID 만들기][img-create-device]

   IoT Hub에 대한 새 장치 ID를 만듭니다.

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

1. Hello에 **장치 탐색기**의 장치 목록에서 새로 만든 hello 장치를 클릭 하 고 hello 기록 **연결 문자열---기본 키**합니다. 

    ![장치 연결 문자열][img-connection-string]

> [!NOTE]
> IoT Hub id 레지스트리에 hello만 장치 identities tooenable 보안 액세스 toohello IoT 허브를 저장합니다. 장치 Id와 키 toouse 보안 자격 증명 및 개별 장치에 대 한 toodisable 액세스를 사용할 수 있는 사용/사용 안 함 플래그로 저장 합니다. 응용 프로그램는 toostore 다른 장치 관련 메타 데이터를 필요한 경우에 응용 프로그램별 저장소를 사용 해야 합니다. 자세한 내용은 [IoT Hub 개발자 가이드][lnk-devguide-identity]를 참조하세요.

<!-- Images. -->
[img-find-iothub]: ./media/iot-hub-get-started-create-device-identity-portal/find-iothub.png
[img-create-device]: ./media/iot-hub-get-started-create-device-identity-portal/create-identity-portal.png
[img-connection-string]: ./media/iot-hub-get-started-create-device-identity-portal/device-connection-string.png


<!-- Links -->
[lnk-azure-portal]: https://portal.azure.com
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md

