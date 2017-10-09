<span data-ttu-id="da4ff-101">여부에 관계 없이 hello ' Get AzureRmVirtualNetworkGatewayConnection' cmdlet을 사용 하 여 연결에 성공 했는지를 확인할 수 있습니다 '-디버그 '.</span><span class="sxs-lookup"><span data-stu-id="da4ff-101">You can verify that your connection succeeded by using hello 'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet, with or without '-Debug'.</span></span> 

1. <span data-ttu-id="da4ff-102">다음 예에서는 cmdlet hello 값 toomatch를 구성, 사용 하 여 hello 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="da4ff-102">Use hello following cmdlet example, configuring hello values toomatch your own.</span></span> <span data-ttu-id="da4ff-103">메시지가 표시 되 면 순서 toorun에서 'A' 선택 'All'.</span><span class="sxs-lookup"><span data-stu-id="da4ff-103">If prompted, select 'A' in order toorun 'All'.</span></span> <span data-ttu-id="da4ff-104">Hello 예에서 '-이름 ' tootest hello 연결의 toohello 이름을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="da4ff-104">In hello example, '-Name' refers toohello name of hello connection that you want tootest.</span></span>

  ```powershell
  Get-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnection -ResourceGroupName MyRG
  ```
2. <span data-ttu-id="da4ff-105">Hello cmdlet을 마친 후 hello 값을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="da4ff-105">After hello cmdlet has finished, view hello values.</span></span> <span data-ttu-id="da4ff-106">Hello 아래 예제에서는 hello 연결 상태는 '연결' 하 고 송 / 수신 바이트를 볼 수를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="da4ff-106">In hello example below, hello connection status shows as 'Connected' and you can see ingress and egress bytes.</span></span>
   
  ```
  "connectionStatus": "Connected",
  "ingressBytesTransferred": 33509044,
  "egressBytesTransferred": 4142431
  ```