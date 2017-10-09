### <a name="noconnection"></a>toomodify 로컬 네트워크 게이트웨이 IP 주소 접두사 게이트웨이 연결 없음

Hello 게이트웨이 연결 되어 있지 않으면 tooadd 하거나 IP 주소 접두사를 제거를 사용 하 여 toocreate hello 로컬 네트워크 게이트웨이 사용 하는 명령을 동일 [az 네트워크 로컬 게이트웨이 만들기](https://docs.microsoft.com/cli/azure/network/local-gateway#create)합니다. 또한 hello VPN 장치에 대 한이 명령은 tooupdate hello 게이트웨이 IP 주소를 사용할 수 있습니다. toooverwrite hello 현재 설정에는 로컬 네트워크 게이트웨이의 hello 기존 이름을 사용 합니다. 다른 이름을 사용 하는 경우 새 로컬 네트워크 게이트웨이 만들을 덮어쓰지 않고 기존 hello 있습니다.

때마다 변경, hello 전체 접두사 목록을 지정 해야 합니다, 그리고 뿐 아니라 hello toochange 원하는 접두사를 추가 합니다. 원하는 tookeep만 hello 접두사를 지정 합니다. 이 예에서는 10.0.0.0/24 및 20.0.0.0/24입니다.

```azurecli
az network local-gateway create --gateway-ip-address 23.99.221.164 --name Site2 --connection-name TestRG1 --local-address-prefixes 10.0.0.0/24 20.0.0.0/24
```

### <a name="withconnection"></a>toomodify 로컬 네트워크 게이트웨이 IP 주소 접두사-기존 게이트웨이 연결

게이트웨이 연결 하 고 원하는 tooadd 또는 IP 주소 접두사를 제거 하는 경우 사용 하 여 hello 접두사를 업데이트할 수 있습니다 [az 네트워크 로컬 게이트웨이 업데이트](https://docs.microsoft.com/cli/azure/network/local-gateway#update)합니다. 이로 인해 VPN 연결에 약간의 가동 중지 시간이 발생합니다. 접두사 hello IP 주소를 수정 하는 경우 toodelete hello VPN 게이트웨이 필요는 없습니다.

때마다 변경, hello 전체 접두사 목록을 지정 해야 합니다, 그리고 뿐 아니라 hello toochange 원하는 접두사를 추가 합니다. 이 예제에서는 10.0.0.0/24 및 20.0.0.0/24가 이미 있습니다. Hello 접두사 30.0.0.0/24 및 40.0.0.0/24 추가 하 고 업데이트할 때 모든 4 hello 접두사를 지정 합니다.

```azurecli
az network local-gateway update --local-address-prefixes 10.0.0.0/24 20.0.0.0/24 30.0.0.0/24 40.0.0.0/24 --name VNet1toSite2 --connection-name TestRG1
```