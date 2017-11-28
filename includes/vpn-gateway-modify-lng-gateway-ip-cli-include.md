### <a name="to-modify-the-local-network-gateway-gatewayipaddress"></a><span data-ttu-id="b40d0-101">로컬 네트워크 게이트웨이의 'gatewayIpAddress'를 수정하려면</span><span class="sxs-lookup"><span data-stu-id="b40d0-101">To modify the local network gateway 'gatewayIpAddress'</span></span>

<span data-ttu-id="b40d0-102">연결하려는 VPN 장치의 공용 IP 주소가 변경된 경우 해당 변경 내용을 반영하도록 로컬 네트워크 게이트웨이를 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b40d0-102">If the VPN device that you want to connect to has changed its public IP address, you need to modify the local network gateway to reflect that change.</span></span> <span data-ttu-id="b40d0-103">기존 VPN Gateway 연결을 제거하지 않고도(있는 경우) 게이트웨이 IP 주소를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b40d0-103">The gateway IP address can be changed without removing an existing VPN gateway connection (if you have one).</span></span> <span data-ttu-id="b40d0-104">게이트웨이 IP 주소를 수정하려면 [az network local-gateway update](https://docs.microsoft.com/cli/azure/network/local-gateway#update) 명령을 사용하여 'Site2' 및 'TestRG1' 값을 사용자 고유의 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b40d0-104">To modify the gateway IP address, replace the values 'Site2' and 'TestRG1' with your own using the [az network local-gateway update](https://docs.microsoft.com/cli/azure/network/local-gateway#update) command.</span></span>

```azurecli
az network local-gateway update --gateway-ip-address 23.99.222.170 --name Site2 --resource-group TestRG1
```

<span data-ttu-id="b40d0-105">출력에서 IP 주소가 올바른지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b40d0-105">Verify that the IP address is correct in the output:</span></span>

```
"gatewayIpAddress": "23.99.222.170",
```