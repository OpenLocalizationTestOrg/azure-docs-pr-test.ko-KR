<span data-ttu-id="a201f-101">'Get-AzureVNetConnection' cmdlet을 사용하여 연결이 성공했는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a201f-101">You can verify that your connection succeeded by using the 'Get-AzureVNetConnection' cmdlet.</span></span>

1. <span data-ttu-id="a201f-102">일치하는 값을 구성하는 데 다음 cmdlet 예제를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a201f-102">Use the following cmdlet example, configuring the values to match your own.</span></span> <span data-ttu-id="a201f-103">공백이 포함된 가상 네트워크의 이름은 따옴표로 묶어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a201f-103">The name of the virtual network must be in quotes if it contains spaces.</span></span>

  ```powershell
  Get-AzureVNetConnection "Group ClassicRG ClassicVNet"
  ```
2. <span data-ttu-id="a201f-104">cmdlet이 완료되면 값을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="a201f-104">After the cmdlet has finished, view the values.</span></span> <span data-ttu-id="a201f-105">아래 예제에서는 [연결 상태]가 '연결됨'으로 표시되고 송/수신 바이트를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a201f-105">In the example below, the Connectivity State shows as 'Connected' and you can see ingress and egress bytes.</span></span>

        ConnectivityState         : Connected
        EgressBytesTransferred    : 181664
        IngressBytesTransferred   : 182080
        LastConnectionEstablished : 1/7/2016 12:40:54 AM
        LastEventID               : 24401
        LastEventMessage          : The connectivity state for the local network site 'RMVNetLocal' changed from Connecting to
                                    Connected.
        LastEventTimeStamp        : 1/7/2016 12:40:54 AM
        LocalNetworkSiteName      : RMVNetLocal