## <a name="scenario"></a><span data-ttu-id="32c35-101">시나리오</span><span class="sxs-lookup"><span data-stu-id="32c35-101">Scenario</span></span>
<span data-ttu-id="32c35-102">toobetter 사용 방법을 보여 줍니다 toocreate VNet 및 서브넷이이 문서는 아래 hello 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="32c35-102">toobetter illustrate how toocreate a VNet and subnets, this document will use hello scenario below.</span></span>

![VNet 시나리오](./media/virtual-networks-create-vnet-scenario-include/vnet-scenario.png)

<span data-ttu-id="32c35-104">이 시나리오에서는 예약된 CIDR 블록 **192.168.0.0./16**을 사용하여 **TestVNet**이라는 VNet을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="32c35-104">In this scenario you will create a VNet named **TestVNet** with a reserved CIDR block of **192.168.0.0./16**.</span></span> <span data-ttu-id="32c35-105">VNet hello 다음 서브넷이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32c35-105">Your VNet will contain hello following subnets:</span></span> 

* <span data-ttu-id="32c35-106">**FrontEnd**, CIDR 블록으로 **192.168.1.0/24** 사용</span><span class="sxs-lookup"><span data-stu-id="32c35-106">**FrontEnd**, using **192.168.1.0/24** as its CIDR block.</span></span>
* <span data-ttu-id="32c35-107">**BackEnd**, CIDR 블록으로 **192.168.2.0/24** 사용</span><span class="sxs-lookup"><span data-stu-id="32c35-107">**BackEnd**, using **192.168.2.0/24** as its CIDR block.</span></span>

