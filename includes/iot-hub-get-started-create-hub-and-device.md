## <a name="create-an-iot-hub"></a>IoT Hub 만들기

1. Hello에 [Azure 포털](https://portal.azure.com/), 클릭 **새로** > **사물 인터넷** > **IoT Hub**합니다.

   ![Hello Azure 포털에서에서 IoT 허브를 만듭니다.](../articles/iot-hub/media/iot-hub-create-hub-and-device/1_create-azure-iot-hub-portal.png)
2. Hello에 **IoT hub** 창 hello 다음 IoT 허브에 대 한 정보를 입력 합니다.

     **이름**: IoT 허브의 hello 이름을 입력 합니다. 입력 한 hello 이름이 유효한 경우 녹색 확인 표시가 나타납니다.

     **가격 및 크기 계층**: 선택 hello **F1-무료** 계층입니다. 이 데모의 경우 이 옵션이면 충분합니다. 자세한 내용은 참조 hello [가격 및 크기 계층](https://azure.microsoft.com/pricing/details/iot-hub/)합니다.

     **리소스 그룹**: 리소스 그룹 toohost hello IoT 허브를 만들거나 기존 집합을 사용 합니다. 자세한 내용은 참조 [사용 하 여 리소스 그룹의 Azure 리소스 toomanage](../articles/azure-resource-manager/resource-group-portal.md)합니다.

     **위치**: 선택 hello 가장 가까운 위치 tooyou hello IoT hub를 만들 위치입니다.

     **Pin toodashboard**: hello 대시보드에서 쉽게 액세스할 수 있도록 tooyour IoT 허브에 대 한이 옵션을 선택 합니다.

   ![IoT hub toocreate 정보를 입력 합니다.](../articles/iot-hub/media/iot-hub-create-hub-and-device/2_fill-in-fields-for-azure-iot-hub-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]

3. **만들기**를 클릭합니다. IoT hub는 몇 분 toocreate를 걸릴 수 있습니다. Hello에서 진행률을 볼 수 있습니다 **알림** 창.

   ![IoT Hub의 진행 알림을 참조하세요.](../articles/iot-hub/media/iot-hub-create-hub-and-device/3_notification-azure-iot-hub-creation-progress-portal.png)

4. IoT 허브를 만든 후 hello 대시보드에서 클릭 합니다. Hello 메모 **Hostname**, 클릭 하 고 **공유 액세스 정책을**합니다.

   ![IoT hub의 hello 호스트 이름 가져오기](../articles/iot-hub/media/iot-hub-create-hub-and-device/4_get-azure-iot-hub-hostname-portal.png)

5. Hello에 **공유 액세스 정책을** 창 hello 클릭 **iothubowner** 정책을 선택한 후 복사 하 hello 기록 **연결 문자열** IoT hub의. 자세한 내용은 참조 [컨트롤 액세스 tooIoT 허브](../articles/iot-hub/iot-hub-devguide-security.md)합니다.

> [!NOTE] 
이 설치 자습서에는 이 iothubowner 연결 문자열이 필요 없습니다. 그러나 해야 것 hello IoT의 서로 다른 시나리오 자습서의 일부에 대 한이 설치를 완료 한 후 합니다.

   ![IoT Hub 연결 문자열 가져오기](../articles/iot-hub/media/iot-hub-create-hub-and-device/5_get-azure-iot-hub-connection-string-portal.png)

## <a name="register-a-device-in-hello-iot-hub-for-your-device"></a>장치에 대 한 hello IoT 허브에서 장치 등록

1. Hello에 [Azure 포털](https://portal.azure.com/), IoT 허브를 엽니다.

2. **장치 탐색기**를 클릭합니다.
3. Hello 장치 탐색기 창에서 클릭 **추가** tooadd 장치 tooyour IoT 허브입니다. 그런 다음 않습니다 다음 hello:

   **장치 ID**: hello 새 장치의 hello ID를 입력 합니다. 장치 ID는 대/소문자를 구분합니다.

   **인증 형식**: **대칭 키**를 선택합니다.

   **자동 생성 키**:이 확인란을 선택합니다.

   **장치 tooIoT 허브 연결**: 클릭 **사용**합니다.

   ![IoT hub의 장치 탐색기 hello에 장치를 추가 합니다.](../articles/iot-hub/media/iot-hub-create-hub-and-device/6_add-device-in-azure-iot-hub-device-explorer-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

4. **Save**를 클릭합니다.
5. Hello 장치를 만든 후 hello에 hello 장치를 열 **장치 탐색기** 창.
6. Hello hello 연결 문자열의 기본 키를 기록해 둡니다.

   ![Hello 장치 연결 문자열 가져오기](../articles/iot-hub/media/iot-hub-create-hub-and-device/7_get-device-connection-string-in-device-explorer-portal.png)
