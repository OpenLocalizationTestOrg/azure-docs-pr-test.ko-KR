## <a name="associate-an-azure-storage-account-tooiot-hub"></a>Azure 저장소 계정 tooIoT 허브 연결

Hello 시뮬레이션 된 장치 응용 프로그램 파일 tooa blob을 업로드 하므로 있어야는 [Azure 저장소](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account) tooIoT 허브를 연결 하는 계정이 있습니다. IoT hub와 Azure 저장소 계정을 연결한 hello IoT hub SAS URI를 생성 합니다. 장치가 SAS URI toosecurely 업로드 파일 tooa blob 컨테이너를 사용할 수 있습니다. IoT Hub 서비스 hello 및 hello 장치 Sdk hello SAS URI를 생성 하 고 사용할 수 있는 tooa 장치 toouse tooupload 파일을 사용 하면 hello 프로세스를 조정 합니다.

Hello 지침에 따라 [hello Azure 포털을 사용 하 여 구성 파일 업로드](../articles/iot-hub/iot-hub-configure-file-upload.md) tooassociate Azure 저장소 계정 tooyour IoT hub 합니다. Blob 컨테이너가 IoT Hub와 연결되고 파일 알림을 사용하는지 확인합니다.

![포털에서 파일 알림 사용](media/iot-hub-associate-storage/enable-file-notifications.png)