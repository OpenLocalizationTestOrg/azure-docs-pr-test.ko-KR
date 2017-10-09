### <a name="tooview-local-network-gateways"></a>tooview 로컬 네트워크 게이트웨이

tooview hello 로컬 네트워크 게이트웨이 사용 하 여 hello 목록 [az 네트워크 로컬 게이트웨이 목록](https://docs.microsoft.com/cli/azure/network/local-gateway#list) 명령입니다.

```azurecli
az network local-gateway list --resource-group TestRG1
```

[!INCLUDE [modify-prefix](vpn-gateway-modify-ip-prefix-cli-include.md)]

[!INCLUDE [modify-gateway-IP](vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

### <a name="tooverify-hello-shared-key-values"></a>tooverify hello 공유 키 값

키 값을 공유 하는 hello hello 인지 확인 VPN 장치 구성에 사용 된 값과 같아야 합니다. 없는 경우에 hello 연결 hello 장치에서 hello 값을 사용 하 여 다시 실행 하거나 hello 값 반환 hello부터 hello 장치를 업데이트 합니다. hello 값과 일치 해야 합니다. 공유 키를 사용 하 여 hello tooview hello [az 네트워크 vpn 연결 목록](https://docs.microsoft.com/cli/azure/network/vpn-connection#list)합니다.

```azurecli
az network vpn-connection shared-key show --connection-name VNet1toSite2 --resource-group TestRG1
```
### <a name="tooview-hello-vpn-gateway-public-ip-address"></a>tooview hello VPN 게이트웨이 공용 IP 주소

가상 네트워크 게이트웨이 사용 하 여 hello의 toofind hello 공용 IP 주소 [az 네트워크 공개 ip 목록](https://docs.microsoft.com/cli/azure/network/public-ip#list) 명령입니다. 읽기 쉽도록이 예제에 대 한 hello 출력은 서식이 지정 된 toodisplay hello 목록 표 형식으로 공용 Ip입니다.

```azurecli
az network public-ip list --resource-group TestRG1 --output table
```
