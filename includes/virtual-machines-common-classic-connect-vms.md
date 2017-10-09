

![독립 실행형 클라우드 서비스의 가상 컴퓨터](./media/virtual-machines-common-classic-connect-vms/CloudServiceExample.png)

<span data-ttu-id="c4758-102">가상 네트워크의 가상 컴퓨터를 배치 하는 경우 개수 클라우드 서비스에 대 한 toouse 원하는 부하 분산 및 가용성 집합을 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4758-102">If you place your virtual machines in a virtual network, you can decide how many cloud services you want toouse for load balancing and availability sets.</span></span> <span data-ttu-id="c4758-103">Hello 가상 컴퓨터를 구성할 수는 또한 hello의 서브넷에서 같은 방식으로 온-프레미스 네트워크 및 가상 네트워크 tooyour hello 연결 온-프레미스 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="c4758-103">Additionally, you can organize hello virtual machines on subnets in hello same way as your on-premises network and connect hello virtual network tooyour on-premises network.</span></span> <span data-ttu-id="c4758-104">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c4758-104">Here's an example:</span></span>

![가상 네트워크의 가상 컴퓨터](./media/virtual-machines-common-classic-connect-vms/VirtualNetworkExample.png)

<span data-ttu-id="c4758-106">가상 네트워크는 hello Azure의 방식으로 tooconnect 가상 컴퓨터를 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4758-106">Virtual networks are hello recommended way tooconnect virtual machines in Azure.</span></span> <span data-ttu-id="c4758-107">가장 좋은 방법은 hello tooconfigure 별도 클라우드 서비스에서 응용 프로그램의 각 계층은 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4758-107">hello best practice is tooconfigure each tier of your application in a separate cloud service.</span></span> <span data-ttu-id="c4758-108">그러나 해야 toocombine 일부 가상 컴퓨터 hello에 여러 응용 프로그램 계층에서 동일한 클라우드 서비스 tooremain hello 최대 구독 당 200 클라우드 서비스 내에서.</span><span class="sxs-lookup"><span data-stu-id="c4758-108">However, you may need toocombine some virtual machines from different application tiers into hello same cloud service tooremain within hello maximum of 200 cloud services per subscription.</span></span> <span data-ttu-id="c4758-109">tooreview이 및 다른 제한을 참조 [Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../articles/azure-subscription-service-limits.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4758-109">tooreview this and other limits, see [Azure Subscription and Service Limits, Quotas, and Constraints](../articles/azure-subscription-service-limits.md).</span></span>

## <a name="connect-vms-in-a-virtual-network"></a><span data-ttu-id="c4758-110">가상 네트워크에서 VM 연결</span><span class="sxs-lookup"><span data-stu-id="c4758-110">Connect VMs in a virtual network</span></span>
<span data-ttu-id="c4758-111">가상 네트워크의 가상 컴퓨터를 tooconnect:</span><span class="sxs-lookup"><span data-stu-id="c4758-111">tooconnect virtual machines in a virtual network:</span></span>

1. <span data-ttu-id="c4758-112">Hello에 hello 가상 네트워크 만들기 [Azure 포털](../articles/virtual-network/virtual-networks-create-vnet-classic-pportal.md) '클래식 배포'를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4758-112">Create hello virtual network in hello [Azure portal](../articles/virtual-network/virtual-networks-create-vnet-classic-pportal.md) and specify 'classic deployment'.</span></span>
2. <span data-ttu-id="c4758-113">Hello 집합 배포 tooreflect에 대 한 클라우드 서비스의 가용성 집합에 대 한 디자인 만들고 부하 분산 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4758-113">Create hello set of cloud services for your deployment tooreflect your design for availability sets and load balancing.</span></span> <span data-ttu-id="c4758-114">Hello Azure 포털에서에서 클릭 **새로 만들기 > 계산 > 클라우드 서비스** 각 클라우드 서비스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4758-114">In hello Azure portal, click **New > Compute > Cloud service** for each cloud service.</span></span>

  <span data-ttu-id="c4758-115">Hello 클라우드 서비스 정보를 입력으로 선택 동일 hello _리소스 그룹_ hello 가상 네트워크와 함께 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4758-115">As you fill out hello cloud service details, choose hello same _resource group_ used with hello virtual network.</span></span>

3. <span data-ttu-id="c4758-116">toocreate 각각의 새 가상 컴퓨터를 클릭 **새로 만들기 > 계산**, 선택 hello hello에서 적절 한 VM 이미지 다음 **추천 앱**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4758-116">toocreate each new virtual machine, click **New > Compute**, then select hello appropriate VM image from hello **Featured apps**.</span></span>

  <span data-ttu-id="c4758-117">Hello VM에서에서 **기본 사항** 블레이드에서 선택 동일 hello _리소스 그룹_ hello 가상 네트워크와 함께 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4758-117">In hello VM **Basics** blade, choose hello same _resource group_ used with hello virtual network.</span></span>

  ![VNet을 사용하는 경우 VM 기본 블레이드](./media/virtual-machines-common-classic-connect-vms/CreateVM_Basics_VN.png)

4. <span data-ttu-id="c4758-119">작성할 때 VM hello 양식에 **설정**, 올바른 hello 선택 _클라우드 서비스_ 또는 _가상 네트워크_ hello VM에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4758-119">As you fill out hello VM **Settings**, choose hello correct _Cloud service_ or _virtual network_ for hello VM.</span></span>

  <span data-ttu-id="c4758-120">Azure는 hello 다른 선택에 따라 항목을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4758-120">Azure will select hello other item based on your selection.</span></span>

  ![VNet을 사용하는 경우 VM 설정 블레이드](./media/virtual-machines-common-classic-connect-vms/CreateVM_Settings_VN.png)


## <a name="connect-vms-in-a-standalone-cloud-service"></a><span data-ttu-id="c4758-122">독립 실행형 클라우드 서비스에서 VM 연결</span><span class="sxs-lookup"><span data-stu-id="c4758-122">Connect VMs in a standalone cloud service</span></span>
<span data-ttu-id="c4758-123">독립 실행형 클라우드 서비스에서 tooconnect 가상 컴퓨터:</span><span class="sxs-lookup"><span data-stu-id="c4758-123">tooconnect virtual machines in a standalone cloud service:</span></span>

1. <span data-ttu-id="c4758-124">Hello에 hello 클라우드 서비스를 만들 [Azure 포털](http://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4758-124">Create hello cloud service in hello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="c4758-125">**새로 만들기 > 계산 > 클라우드 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4758-125">Click **New > Compute > Cloud service**.</span></span> <span data-ttu-id="c4758-126">또는 첫 번째 가상 컴퓨터를 만들 때 배포에 대 한 hello 클라우드 서비스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4758-126">Or, you can create hello cloud service for your deployment when you create your first virtual machine.</span></span>
2. <span data-ttu-id="c4758-127">Hello 가상 컴퓨터를 만들 때 hello hello 클라우드 서비스와 함께 사용 되는 동일한 리소스 그룹을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4758-127">When you create hello virtual machines, choose hello same resource group used with hello cloud service.</span></span>

  ![가상 컴퓨터 tooan 기존 클라우드 서비스를 추가 합니다.](./media/virtual-machines-common-classic-connect-vms/CreateVM_Basics_SA.png)

3.  <span data-ttu-id="c4758-129">Hello VM 세부 정보를 입력 하는 대로 hello 첫 번째 단계에서 만든 클라우드 서비스의 hello 이름을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4758-129">As you fill out hello VM details, choose hello name of cloud service created in hello first step.</span></span>

  ![가상 컴퓨터에 대한 클라우드 서비스 선택](./media/virtual-machines-common-classic-connect-vms/CreateVM_Settings_SA.png)
