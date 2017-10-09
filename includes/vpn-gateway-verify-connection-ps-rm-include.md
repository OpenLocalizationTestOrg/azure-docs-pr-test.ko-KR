여부에 관계 없이 hello ' Get AzureRmVirtualNetworkGatewayConnection' cmdlet을 사용 하 여 연결에 성공 했는지를 확인할 수 있습니다 '-디버그 '. 

1. 다음 예에서는 cmdlet hello 값 toomatch를 구성, 사용 하 여 hello 직접 합니다. 메시지가 표시 되 면 순서 toorun에서 'A' 선택 'All'. Hello 예에서 '-이름 ' tootest hello 연결의 toohello 이름을 참조 합니다.

  ```powershell
  Get-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnection -ResourceGroupName MyRG
  ```
2. Hello cmdlet을 마친 후 hello 값을 확인 합니다. Hello 아래 예제에서는 hello 연결 상태는 '연결' 하 고 송 / 수신 바이트를 볼 수를 표시 합니다.
   
  ```
  "connectionStatus": "Connected",
  "ingressBytesTransferred": 33509044,
  "egressBytesTransferred": 4142431
  ```