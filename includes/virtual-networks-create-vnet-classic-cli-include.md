## <a name="how-toocreate-a-classic-vnet-using-azure-cli"></a><span data-ttu-id="d70f0-101">어떻게 toocreate Azure CLI를 사용 하 여 클래식 VNet</span><span class="sxs-lookup"><span data-stu-id="d70f0-101">How toocreate a classic VNet using Azure CLI</span></span>
<span data-ttu-id="d70f0-102">Hello Azure CLI toomanage hello 명령 프롬프트에서 Windows, Linux 또는 OSX를 실행 하는 컴퓨터에서 Azure 리소스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d70f0-102">You can use hello Azure CLI toomanage your Azure resources from hello command prompt from any computer running Windows, Linux, or OSX.</span></span> <span data-ttu-id="d70f0-103">toocreate hello Azure CLI를 사용 하 여 VNet 아래 hello 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="d70f0-103">toocreate a VNet by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="d70f0-104">Azure CLI 처음 사용 하는 경우 참조 [설치 및 구성 hello Azure CLI](../articles/cli-install-nodejs.md) Azure 계정 및 구독을 선택 하면 toohello 포인트 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="d70f0-104">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../articles/cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="d70f0-105">Hello 실행 **azure 네트워크 vnet 만들기** 명령 toocreate VNet 서브넷에 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="d70f0-105">Run hello **azure network vnet create** command toocreate a VNet and a subnet, as shown below.</span></span> <span data-ttu-id="d70f0-106">hello 출력 뒤에 표시 된 hello 목록 사용 되는 hello 매개 변수를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d70f0-106">hello list shown after hello output explains hello parameters used.</span></span>
   
            azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
   
    <span data-ttu-id="d70f0-107">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="d70f0-107">Expected output:</span></span>
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK
   
   * <span data-ttu-id="d70f0-108">**--vnet**.</span><span class="sxs-lookup"><span data-stu-id="d70f0-108">**--vnet**.</span></span> <span data-ttu-id="d70f0-109">만든 hello VNet toobe의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d70f0-109">Name of hello VNet toobe created.</span></span> <span data-ttu-id="d70f0-110">이 시나리오에서는 *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="d70f0-110">For our scenario, *TestVNet*</span></span>
   * <span data-ttu-id="d70f0-111">**-e(또는 --address-space)**.</span><span class="sxs-lookup"><span data-stu-id="d70f0-111">**-e (or --address-space)**.</span></span> <span data-ttu-id="d70f0-112">VNet 주소 공간입니다.</span><span class="sxs-lookup"><span data-stu-id="d70f0-112">VNet address space.</span></span> <span data-ttu-id="d70f0-113">이 시나리오에서는 *192.168.0.0*</span><span class="sxs-lookup"><span data-stu-id="d70f0-113">For our scenario, *192.168.0.0*</span></span>
   * <span data-ttu-id="d70f0-114">**-i(또는 -cidr)**.</span><span class="sxs-lookup"><span data-stu-id="d70f0-114">**-i (or -cidr)**.</span></span> <span data-ttu-id="d70f0-115">CIDR 형식의 네트워크 마스크입니다.</span><span class="sxs-lookup"><span data-stu-id="d70f0-115">Network mask in CIDR format.</span></span> <span data-ttu-id="d70f0-116">이 시나리오에서는 *16*입니다.</span><span class="sxs-lookup"><span data-stu-id="d70f0-116">For our scenario, *16*.</span></span>
   * <span data-ttu-id="d70f0-117">**-n(또는 --subnet-name**).</span><span class="sxs-lookup"><span data-stu-id="d70f0-117">**-n (or --subnet-name**).</span></span> <span data-ttu-id="d70f0-118">Hello 첫 번째 서브넷의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d70f0-118">Name of hello first subnet.</span></span> <span data-ttu-id="d70f0-119">이 시나리오에서는 *FrontEnd*입니다.</span><span class="sxs-lookup"><span data-stu-id="d70f0-119">For our scenario, *FrontEnd*.</span></span>
   * <span data-ttu-id="d70f0-120">**-p(또는 --subnet-start-ip)**.</span><span class="sxs-lookup"><span data-stu-id="d70f0-120">**-p (or --subnet-start-ip)**.</span></span> <span data-ttu-id="d70f0-121">서브넷 또는 서브넷 주소 공간의 시작 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="d70f0-121">Starting IP address for subnet, or subnet address space.</span></span> <span data-ttu-id="d70f0-122">이 시나리오에서는 *192.168.1.0*입니다.</span><span class="sxs-lookup"><span data-stu-id="d70f0-122">For our scenario, *192.168.1.0*.</span></span>
   * <span data-ttu-id="d70f0-123">**-r(또는 --subnet-cidr)**.</span><span class="sxs-lookup"><span data-stu-id="d70f0-123">**-r (or --subnet-cidr)**.</span></span> <span data-ttu-id="d70f0-124">서브넷에 대한 CIDR 형식의 네트워크 마스크입니다.</span><span class="sxs-lookup"><span data-stu-id="d70f0-124">Network mask in CIDR format for subnet.</span></span> <span data-ttu-id="d70f0-125">이 시나리오에서는 *24*입니다.</span><span class="sxs-lookup"><span data-stu-id="d70f0-125">For our scenario, *24*.</span></span>
   * <span data-ttu-id="d70f0-126">**-l(또는 --location)**.</span><span class="sxs-lookup"><span data-stu-id="d70f0-126">**-l (or --location)**.</span></span> <span data-ttu-id="d70f0-127">Azure 지역 VNet hello 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d70f0-127">Azure region where hello VNet will be created.</span></span> <span data-ttu-id="d70f0-128">이 시나리오에서는 *Central US*입니다.</span><span class="sxs-lookup"><span data-stu-id="d70f0-128">For our scenario, *Central US*.</span></span>
3. <span data-ttu-id="d70f0-129">Hello 실행 **만드는 azure 네트워크 vnet 서브넷** 명령 toocreate 아래와 같이 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="d70f0-129">Run hello **azure network vnet subnet create** command toocreate a subnet as shown below.</span></span> <span data-ttu-id="d70f0-130">hello 출력 뒤에 표시 된 hello 목록 사용 되는 hello 매개 변수를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d70f0-130">hello list shown after hello output explains hello parameters used.</span></span>
   
            azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
   
    <span data-ttu-id="d70f0-131">다음은 위의 hello 명령에 대 한 예상 hello 출력이입니다.</span><span class="sxs-lookup"><span data-stu-id="d70f0-131">Here is hello expected output for hello command above:</span></span>
   
            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK
   
   * <span data-ttu-id="d70f0-132">**-t(또는 --vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="d70f0-132">**-t (or --vnet-name**.</span></span> <span data-ttu-id="d70f0-133">Hello hello 서브넷을 만들 수는 VNet의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d70f0-133">Name of hello VNet where hello subnet will be created.</span></span> <span data-ttu-id="d70f0-134">이 시나리오에서는 *TestVNet*입니다.</span><span class="sxs-lookup"><span data-stu-id="d70f0-134">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="d70f0-135">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="d70f0-135">**-n (or --name)**.</span></span> <span data-ttu-id="d70f0-136">Hello 새 서브넷의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d70f0-136">Name of hello new subnet.</span></span> <span data-ttu-id="d70f0-137">이 시나리오에서는 *BackEnd*입니다.</span><span class="sxs-lookup"><span data-stu-id="d70f0-137">For our scenario, *BackEnd*.</span></span>
   * <span data-ttu-id="d70f0-138">**-a(또는 --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="d70f0-138">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="d70f0-139">서브넷 CIDR 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="d70f0-139">Subnet CIDR block.</span></span> <span data-ttu-id="d70f0-140">이 시나리오에서는 *192.168.2.0/24*입니다.</span><span class="sxs-lookup"><span data-stu-id="d70f0-140">Four our scenario, *192.168.2.0/24*.</span></span>
4. <span data-ttu-id="d70f0-141">Hello 실행 **azure 네트워크 vnet 표시** 아래와 같이 hello 새 vnet의 tooview hello 속성 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="d70f0-141">Run hello **azure network vnet show** command tooview hello properties of hello new vnet, as shown below.</span></span>
   
            azure network vnet show
   
    <span data-ttu-id="d70f0-142">다음은 위의 hello 명령에 대 한 예상 hello 출력이입니다.</span><span class="sxs-lookup"><span data-stu-id="d70f0-142">Here is hello expected output for hello command above:</span></span>
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

