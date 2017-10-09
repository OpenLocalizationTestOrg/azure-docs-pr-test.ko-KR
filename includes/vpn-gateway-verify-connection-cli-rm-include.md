<span data-ttu-id="ab391-101">Hello를 사용 하 여 연결 성공 했는지를 확인할 수 있습니다 [az 네트워크 vpn 연결 표시](/cli/azure/network/vpn-connection#show) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="ab391-101">You can verify that your connection succeeded by using hello [az network vpn-connection show](/cli/azure/network/vpn-connection#show) command.</span></span> <span data-ttu-id="ab391-102">Hello 예에서 '-이름 ' tootest hello 연결의 toohello 이름을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab391-102">In hello example, '--name' refers toohello name of hello connection that you want tootest.</span></span> <span data-ttu-id="ab391-103">Hello 연결이 설정 되 고 hello 프로세스의 경우 연결 상태에 '연결' 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ab391-103">When hello connection is in hello process of being established, its connection status shows 'Connecting'.</span></span> <span data-ttu-id="ab391-104">Hello 상태가 변경 too'Connected hello 연결이 설정 되 면 '.</span><span class="sxs-lookup"><span data-stu-id="ab391-104">Once hello connection is established, hello status changes too'Connected'.</span></span>

```azurecli
az network vpn-connection show --name VNet1toSite2 --resource-group TestRG1
```

