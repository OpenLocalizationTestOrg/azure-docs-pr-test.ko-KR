#### <a name="to-create-public-endpoints-on-the-cloud-appliance"></a><span data-ttu-id="4426c-101">클라우드 어플라이언스에 공용 끝점을 만들려면</span><span class="sxs-lookup"><span data-stu-id="4426c-101">To create public endpoints on the cloud appliance</span></span>

1. <span data-ttu-id="4426c-102">Azure 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4426c-102">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="4426c-103">**Virtual Machines**로 이동한 후 클라우드 어플라이언스로 사용 중인 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4426c-103">Go to **Virtual Machines**, and then select and click the virtual machine that is being used as your cloud appliance.</span></span>
    
3. <span data-ttu-id="4426c-104">가상 컴퓨터 내부 및 외부로 흐름을 제어하는 NSG(네트워크 보안 그룹) 규칙을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4426c-104">You need to create a network security group (NSG) rule to control the flow of traffic in and out of your virtual machine.</span></span> <span data-ttu-id="4426c-105">NSG 규칙을 만들려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4426c-105">Perform the following steps to create an NSG rule.</span></span>
    1. <span data-ttu-id="4426c-106">**네트워크 보안 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4426c-106">Select **Network security group**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt1.png)

    2. <span data-ttu-id="4426c-107">표시되는 기본 네트워크 보안 그룹을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4426c-107">Click the default network security group that is presented.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt2.png)

    3. <span data-ttu-id="4426c-108">**인바운드 보안 규칙**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4426c-108">Select **Inbound security rules**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt3.png)

    4. <span data-ttu-id="4426c-109">**+ 추가**를 클릭하여 인바운드 보안 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4426c-109">Click **+ Add** to create an inbound security rule.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt4.png)

        <span data-ttu-id="4426c-110">인바운드 보안 규칙 추가 블레이드에서:</span><span class="sxs-lookup"><span data-stu-id="4426c-110">In the Add inbound security rule blade:</span></span>

        1. <span data-ttu-id="4426c-111">**이름**의 경우, 끝점에 대해 WinRMHttps를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4426c-111">For the **Name**, type the following name for the endpoint: WinRMHttps.</span></span>
        
        2. <span data-ttu-id="4426c-112">**우선 순위**로는 1000(기본 규칙에 대한 우선 순위임)보다 작은 숫자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4426c-112">For the **Priority**, select a number lesser than 1000 (which is the priority for the default rule).</span></span> <span data-ttu-id="4426c-113">값이 높을수록 우선 순위는 더 낮아집니다.</span><span class="sxs-lookup"><span data-stu-id="4426c-113">Higher the value, lower the priority.</span></span>

        3. <span data-ttu-id="4426c-114">**원본**을 **모두**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4426c-114">Set the **Source** to **Any**.</span></span>

        4. <span data-ttu-id="4426c-115">**서비스**로는 **WinRM**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4426c-115">For the **Service**, select **WinRM**.</span></span> <span data-ttu-id="4426c-116">**프로토콜**은 **TCP**로 자동으로 설정되고 **포트 범위**는 **5986**으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="4426c-116">The **Protocol** is automatically set to **TCP** and the **Port range** is set to **5986**.</span></span>

        5. <span data-ttu-id="4426c-117">**확인**을 클릭하여 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4426c-117">Click **OK** to create the rule.</span></span>

            ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt5.png)

4. <span data-ttu-id="4426c-118">마지막 단계는 네트워크 보안 그룹을 서브넷 또는 특정 네트워크 인터페이스에 연결하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4426c-118">Your final step is to associate your network security group with a subnet or a specific network interface.</span></span> <span data-ttu-id="4426c-119">네트워크 보안 그룹을 서브넷과 연결하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4426c-119">Perform the following steps to associate your network security group with a subnet.</span></span>
    1. <span data-ttu-id="4426c-120">**서브넷**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4426c-120">Go to **Subnets**.</span></span>
    2. <span data-ttu-id="4426c-121">**+ 연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4426c-121">Click **+ Associate**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt7.png)

    3. <span data-ttu-id="4426c-122">가상 네트워크를 선택하고 적절한 서브넷을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4426c-122">Select your virtual network, and then select the appropriate subnet.</span></span>
    4. <span data-ttu-id="4426c-123">**확인**을 클릭하여 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4426c-123">Click **OK** to create the rule.</span></span>

        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt11.png)

<span data-ttu-id="4426c-124">규칙이 생성되면, 세부 정보를 보고 VIP(공용 가상 IP) 주소를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4426c-124">After the rule is created, you can view its details to determine the Public Virtual IP (VIP) address.</span></span> <span data-ttu-id="4426c-125">이 주소를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="4426c-125">Record this address.</span></span>


