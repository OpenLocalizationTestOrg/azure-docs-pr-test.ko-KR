#### <a name="toostop-and-start-a-virtual-device"></a>toostop 및 가상 장치 시작
가상 장치 toostop 해당 이름을 클릭 하 고 클릭 **종료**합니다. 상태는 hello 가상 장치를 종료 하는 동안 **중지**합니다. 가상 장치 hello 중지 된 후에 상태가 **Stopped**합니다.

다음 cmdlet toostop hello를 사용 하 고 가상 장치를 시작 합니다.

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-virtual-device"></a>toorestart 가상 장치
가상 장치가 실행 되 고 toorestart 원하는 해당 이름을 클릭 한 다음 클릭 **다시 시작**합니다. 상태는 hello 가상 장치를 다시 시작 하는 동안 **를 다시 설치 하면**합니다. 상태는 hello 가상 장치 toouse 있습니다에 대 한 준비 되 면 **실행**합니다.

다음 cmdlet toorestart 가상 장치 hello를 사용 합니다.

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

