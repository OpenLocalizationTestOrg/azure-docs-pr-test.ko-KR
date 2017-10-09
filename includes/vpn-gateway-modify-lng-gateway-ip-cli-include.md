### <a name="toomodify-hello-local-network-gateway-gatewayipaddress"></a><span data-ttu-id="1fb53-101">toomodify hello 로컬 네트워크 게이트웨이 'gatewayIpAddress'</span><span class="sxs-lookup"><span data-stu-id="1fb53-101">toomodify hello local network gateway 'gatewayIpAddress'</span></span>

<span data-ttu-id="1fb53-102">원하는 tooconnect toohas hello VPN 장치에 공용 IP 주소 변경 된 경우 toomodify hello 로컬 네트워크 게이트웨이 tooreflect 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb53-102">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="1fb53-103">hello 게이트웨이 IP 주소 (있는 경우 하나) 기존 VPN 게이트웨이 연결을 제거 하지 않고 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fb53-103">hello gateway IP address can be changed without removing an existing VPN gateway connection (if you have one).</span></span> <span data-ttu-id="1fb53-104">toomodify hello 게이트웨이 IP 주소, replace hello 값 'Site2' 및 'TestRG1'를 사용 하 여 hello로 [az 네트워크 로컬 게이트웨이 업데이트](https://docs.microsoft.com/cli/azure/network/local-gateway#update) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="1fb53-104">toomodify hello gateway IP address, replace hello values 'Site2' and 'TestRG1' with your own using hello [az network local-gateway update](https://docs.microsoft.com/cli/azure/network/local-gateway#update) command.</span></span>

```azurecli
az network local-gateway update --gateway-ip-address 23.99.222.170 --name Site2 --resource-group TestRG1
```

<span data-ttu-id="1fb53-105">Hello 출력에 hello IP 주소가 올바른지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fb53-105">Verify that hello IP address is correct in hello output:</span></span>

```
"gatewayIpAddress": "23.99.222.170",
```