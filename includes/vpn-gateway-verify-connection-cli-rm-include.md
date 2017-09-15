<span data-ttu-id="b31fc-101">[az network vpn-connection show](/cli/azure/network/vpn-connection#show) 명령을 사용하여 연결이 성공했는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b31fc-101">You can verify that your connection succeeded by using the [az network vpn-connection show](/cli/azure/network/vpn-connection#show) command.</span></span> <span data-ttu-id="b31fc-102">예제에서  --name은 테스트하려는 연결의 이름을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="b31fc-102">In the example, '--name' refers to the name of the connection that you want to test.</span></span> <span data-ttu-id="b31fc-103">연결이 계속 설정 중이면 연결 상태가 '연결 중'으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b31fc-103">When the connection is in the process of being established, its connection status shows 'Connecting'.</span></span> <span data-ttu-id="b31fc-104">연결이 설정되면 상태가 '연결됨'으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="b31fc-104">Once the connection is established, the status changes to 'Connected'.</span></span>

```azurecli
az network vpn-connection show --name VNet1toSite2 --resource-group TestRG1
```

