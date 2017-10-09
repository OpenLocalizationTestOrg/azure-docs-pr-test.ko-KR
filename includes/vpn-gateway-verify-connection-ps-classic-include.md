' Get AzureVNetConnection' hello cmdlet을 사용 하 여 연결에 성공 했는지 확인할 수 있습니다.

1. 다음 예에서는 cmdlet hello 값 toomatch를 구성, 사용 하 여 hello 직접 합니다. 공백이 포함 되어 있으면 hello 가상 네트워크의 hello 이름을 따옴표로 묶어야 합니다.

  ```powershell
  Get-AzureVNetConnection "Group ClassicRG ClassicVNet"
  ```
2. Hello cmdlet을 마친 후 hello 값을 확인 합니다. Hello 아래 예제에서는 '연결 됨'으로 hello 연결 상태를 표시 하 고 송 / 수신 바이트를 볼 수 있습니다.

        ConnectivityState         : Connected
        EgressBytesTransferred    : 181664
        IngressBytesTransferred   : 182080
        LastConnectionEstablished : 1/7/2016 12:40:54 AM
        LastEventID               : 24401
        LastEventMessage          : hello connectivity state for hello local network site 'RMVNetLocal' changed from Connecting to
                                    Connected.
        LastEventTimeStamp        : 1/7/2016 12:40:54 AM
        LocalNetworkSiteName      : RMVNetLocal