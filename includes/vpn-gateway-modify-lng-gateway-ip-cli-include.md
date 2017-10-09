### <a name="toomodify-hello-local-network-gateway-gatewayipaddress"></a>toomodify hello 로컬 네트워크 게이트웨이 'gatewayIpAddress'

원하는 tooconnect toohas hello VPN 장치에 공용 IP 주소 변경 된 경우 toomodify hello 로컬 네트워크 게이트웨이 tooreflect 변경 해야 합니다. hello 게이트웨이 IP 주소 (있는 경우 하나) 기존 VPN 게이트웨이 연결을 제거 하지 않고 변경할 수 있습니다. toomodify hello 게이트웨이 IP 주소, replace hello 값 'Site2' 및 'TestRG1'를 사용 하 여 hello로 [az 네트워크 로컬 게이트웨이 업데이트](https://docs.microsoft.com/cli/azure/network/local-gateway#update) 명령입니다.

```azurecli
az network local-gateway update --gateway-ip-address 23.99.222.170 --name Site2 --resource-group TestRG1
```

Hello 출력에 hello IP 주소가 올바른지 확인 합니다.

```
"gatewayIpAddress": "23.99.222.170",
```