### <a name="tooview-local-network-gateways"></a><span data-ttu-id="b16ac-101">tooview 로컬 네트워크 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="b16ac-101">tooview local network gateways</span></span>

<span data-ttu-id="b16ac-102">tooview hello 로컬 네트워크 게이트웨이 사용 하 여 hello 목록 [az 네트워크 로컬 게이트웨이 목록](https://docs.microsoft.com/cli/azure/network/local-gateway#list) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b16ac-102">tooview a list of hello local network gateways, use hello [az network local-gateway list](https://docs.microsoft.com/cli/azure/network/local-gateway#list) command.</span></span>

```azurecli
az network local-gateway list --resource-group TestRG1
```

[!INCLUDE [modify-prefix](vpn-gateway-modify-ip-prefix-cli-include.md)]

[!INCLUDE [modify-gateway-IP](vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

### <a name="tooverify-hello-shared-key-values"></a><span data-ttu-id="b16ac-103">tooverify hello 공유 키 값</span><span class="sxs-lookup"><span data-stu-id="b16ac-103">tooverify hello shared key values</span></span>

<span data-ttu-id="b16ac-104">키 값을 공유 하는 hello hello 인지 확인 VPN 장치 구성에 사용 된 값과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b16ac-104">Verify that hello shared key value is hello same value that you used for your VPN device configuration.</span></span> <span data-ttu-id="b16ac-105">없는 경우에 hello 연결 hello 장치에서 hello 값을 사용 하 여 다시 실행 하거나 hello 값 반환 hello부터 hello 장치를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b16ac-105">If it is not, either run hello connection again using hello value from hello device, or update hello device with hello value from hello return.</span></span> <span data-ttu-id="b16ac-106">hello 값과 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b16ac-106">hello values must match.</span></span> <span data-ttu-id="b16ac-107">공유 키를 사용 하 여 hello tooview hello [az 네트워크 vpn 연결 목록](https://docs.microsoft.com/cli/azure/network/vpn-connection#list)합니다.</span><span class="sxs-lookup"><span data-stu-id="b16ac-107">tooview hello shared key, use hello [az network vpn-connection-list](https://docs.microsoft.com/cli/azure/network/vpn-connection#list).</span></span>

```azurecli
az network vpn-connection shared-key show --connection-name VNet1toSite2 --resource-group TestRG1
```
### <a name="tooview-hello-vpn-gateway-public-ip-address"></a><span data-ttu-id="b16ac-108">tooview hello VPN 게이트웨이 공용 IP 주소</span><span class="sxs-lookup"><span data-stu-id="b16ac-108">tooview hello VPN gateway Public IP address</span></span>

<span data-ttu-id="b16ac-109">가상 네트워크 게이트웨이 사용 하 여 hello의 toofind hello 공용 IP 주소 [az 네트워크 공개 ip 목록](https://docs.microsoft.com/cli/azure/network/public-ip#list) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b16ac-109">toofind hello public IP address of your virtual network gateway, use hello [az network public-ip list](https://docs.microsoft.com/cli/azure/network/public-ip#list) command.</span></span> <span data-ttu-id="b16ac-110">읽기 쉽도록이 예제에 대 한 hello 출력은 서식이 지정 된 toodisplay hello 목록 표 형식으로 공용 Ip입니다.</span><span class="sxs-lookup"><span data-stu-id="b16ac-110">For easy reading, hello output for this example is formatted toodisplay hello list of public IPs in table format.</span></span>

```azurecli
az network public-ip list --resource-group TestRG1 --output table
```
