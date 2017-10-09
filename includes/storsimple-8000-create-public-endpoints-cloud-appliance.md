#### <a name="toocreate-public-endpoints-on-hello-cloud-appliance"></a><span data-ttu-id="dd4c5-101">hello 클라우드 어플라이언스에 toocreate 공용 끝점</span><span class="sxs-lookup"><span data-stu-id="dd4c5-101">toocreate public endpoints on hello cloud appliance</span></span>

1. <span data-ttu-id="dd4c5-102">Azure 포털 toohello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd4c5-102">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="dd4c5-103">너무 이동**가상 컴퓨터**을 다음 선택 하 고 hello 가상 컴퓨터 클라우드 어플라이언스에으로 사용 되 고를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd4c5-103">Go too**Virtual Machines**, and then select and click hello virtual machine that is being used as your cloud appliance.</span></span>
    
3. <span data-ttu-id="dd4c5-104">가상 컴퓨터 내부 및 외부로 toocreate를 네트워크 보안 그룹 (NSG) 규칙 toocontrol hello 트래픽 흐름을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="dd4c5-104">You need toocreate a network security group (NSG) rule toocontrol hello flow of traffic in and out of your virtual machine.</span></span> <span data-ttu-id="dd4c5-105">Hello 단계 toocreate NSG 규칙 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd4c5-105">Perform hello following steps toocreate an NSG rule.</span></span>
    1. <span data-ttu-id="dd4c5-106">**네트워크 보안 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd4c5-106">Select **Network security group**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt1.png)

    2. <span data-ttu-id="dd4c5-107">표시 되는 hello 기본 네트워크 보안 그룹을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd4c5-107">Click hello default network security group that is presented.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt2.png)

    3. <span data-ttu-id="dd4c5-108">**인바운드 보안 규칙**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dd4c5-108">Select **Inbound security rules**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt3.png)

    4. <span data-ttu-id="dd4c5-109">클릭 **+ 추가** toocreate 인바운드 보안 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="dd4c5-109">Click **+ Add** toocreate an inbound security rule.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt4.png)

        <span data-ttu-id="dd4c5-110">Hello 추가 인바운드 보안 규칙 블레이드에서:</span><span class="sxs-lookup"><span data-stu-id="dd4c5-110">In hello Add inbound security rule blade:</span></span>

        1. <span data-ttu-id="dd4c5-111">Hello에 대 한 **이름**, hello 끝점에 대 한 형식 hello 다음 이름을: WinRMHttps 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd4c5-111">For hello **Name**, type hello following name for hello endpoint: WinRMHttps.</span></span>
        
        2. <span data-ttu-id="dd4c5-112">Hello에 대 한 **우선 순위**선택 합니다 (즉, hello 기본 규칙에 대 한 hello 우선 순위) 숫자 1000 보다 낮습니다.</span><span class="sxs-lookup"><span data-stu-id="dd4c5-112">For hello **Priority**, select a number lesser than 1000 (which is hello priority for hello default rule).</span></span> <span data-ttu-id="dd4c5-113">Hello 값이 높을수록 더 낮은 hello 우선 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd4c5-113">Higher hello value, lower hello priority.</span></span>

        3. <span data-ttu-id="dd4c5-114">집합 hello **소스** 너무**모든**합니다.</span><span class="sxs-lookup"><span data-stu-id="dd4c5-114">Set hello **Source** too**Any**.</span></span>

        4. <span data-ttu-id="dd4c5-115">Hello에 대 한 **서비스**선택, **WinRM**합니다.</span><span class="sxs-lookup"><span data-stu-id="dd4c5-115">For hello **Service**, select **WinRM**.</span></span> <span data-ttu-id="dd4c5-116">hello **프로토콜** 는 자동으로 너무 설정**TCP** 및 hello **포트 범위가** 너무 설정 되어**5986**합니다.</span><span class="sxs-lookup"><span data-stu-id="dd4c5-116">hello **Protocol** is automatically set too**TCP** and hello **Port range** is set too**5986**.</span></span>

        5. <span data-ttu-id="dd4c5-117">클릭 **확인** toocreate hello 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="dd4c5-117">Click **OK** toocreate hello rule.</span></span>

            ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt5.png)

4. <span data-ttu-id="dd4c5-118">마지막 단계는 tooassociate 서브넷 또는 특정 네트워크 인터페이스를 네트워크 보안 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="dd4c5-118">Your final step is tooassociate your network security group with a subnet or a specific network interface.</span></span> <span data-ttu-id="dd4c5-119">네트워크 보안 그룹은 서브넷과 hello 단계 tooassociate 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd4c5-119">Perform hello following steps tooassociate your network security group with a subnet.</span></span>
    1. <span data-ttu-id="dd4c5-120">너무 이동**서브넷**합니다.</span><span class="sxs-lookup"><span data-stu-id="dd4c5-120">Go too**Subnets**.</span></span>
    2. <span data-ttu-id="dd4c5-121">**+ 연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dd4c5-121">Click **+ Associate**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt7.png)

    3. <span data-ttu-id="dd4c5-122">가상 네트워크를 선택 하 고 hello 적절 한 서브넷을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd4c5-122">Select your virtual network, and then select hello appropriate subnet.</span></span>
    4. <span data-ttu-id="dd4c5-123">클릭 **확인** toocreate hello 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="dd4c5-123">Click **OK** toocreate hello rule.</span></span>

        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt11.png)

<span data-ttu-id="dd4c5-124">Hello 규칙을 만든 후 해당 세부 정보 toodetermine hello 공용 VIP (가상 IP) 주소를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd4c5-124">After hello rule is created, you can view its details toodetermine hello Public Virtual IP (VIP) address.</span></span> <span data-ttu-id="dd4c5-125">이 주소를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="dd4c5-125">Record this address.</span></span>


