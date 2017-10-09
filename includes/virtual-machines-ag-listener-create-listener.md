<span data-ttu-id="bab1f-101">이 단계에서는 수동으로 장애 조치 클러스터 관리자 및 SQL Server Management Studio에서 hello 가용성 그룹 수신기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bab1f-101">In this step, you manually create hello availability group listener in Failover Cluster Manager and SQL Server Management Studio.</span></span>

1. <span data-ttu-id="bab1f-102">Hello 주 복제본을 호스트 하는 hello 노드에서 장애 조치 클러스터 관리자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bab1f-102">Open Failover Cluster Manager from hello node that hosts hello primary replica.</span></span>

2. <span data-ttu-id="bab1f-103">선택 hello **네트워크** 노드를 마우스 참고 hello 클러스터 네트워크 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="bab1f-103">Select hello **Networks** node, and then note hello cluster network name.</span></span> <span data-ttu-id="bab1f-104">이 이름은 hello $ClusterNetworkName 변수 hello PowerShell 스크립트에서에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bab1f-104">This name is used in hello $ClusterNetworkName variable in hello PowerShell script.</span></span>

3. <span data-ttu-id="bab1f-105">Hello 클러스터 이름을 확장 한 다음 클릭 **역할**합니다.</span><span class="sxs-lookup"><span data-stu-id="bab1f-105">Expand hello cluster name, and then click **Roles**.</span></span>

4. <span data-ttu-id="bab1f-106">Hello에 **역할** 창에서 마우스 오른쪽 단추로 클릭 hello 가용성 그룹 이름 및 선택한 후 **리소스 추가** > **클라이언트 액세스 지점**합니다.</span><span class="sxs-lookup"><span data-stu-id="bab1f-106">In hello **Roles** pane, right-click hello availability group name, and then select **Add Resource** > **Client Access Point**.</span></span>
   
    ![가용성 그룹에 대한 클라이언트 액세스 지점 추가](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678769.gif)

5. <span data-ttu-id="bab1f-108">Hello에 **이름** 상자이 새 수신기 이름을 클릭 하 고 **다음** 을 두 번 클릭 하 고 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="bab1f-108">In hello **Name** box, create a name for this new listener, click **Next** twice, and then click **Finish**.</span></span>  
    <span data-ttu-id="bab1f-109">으로 설정 하지 않습니다 hello 수신기 또는 리소스를 온라인이 시점에서.</span><span class="sxs-lookup"><span data-stu-id="bab1f-109">Do not bring hello listener or resource online at this point.</span></span>

6. <span data-ttu-id="bab1f-110">Hello 클릭 **리소스** 탭을 클릭 한 다음 방금 만든 hello 클라이언트 액세스 지점을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="bab1f-110">Click hello **Resources** tab, and then expand hello client access point you just created.</span></span> 
    <span data-ttu-id="bab1f-111">클러스터의 각 클러스터 네트워크에 대 한 IP 주소 리소스 hello 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bab1f-111">hello IP address resource for each cluster network in your cluster is displayed.</span></span> <span data-ttu-id="bab1f-112">Azure 전용 솔루션인 경우 하나의 IP 주소 리소스만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bab1f-112">If this is an Azure-only solution, only one IP address resource is displayed.</span></span>

7. <span data-ttu-id="bab1f-113">Hello 다음 중 하나를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bab1f-113">Do either of hello following:</span></span>
   
   * <span data-ttu-id="bab1f-114">tooconfigure 하이브리드 솔루션:</span><span class="sxs-lookup"><span data-stu-id="bab1f-114">tooconfigure a hybrid solution:</span></span>
     
        <span data-ttu-id="bab1f-115">a.</span><span class="sxs-lookup"><span data-stu-id="bab1f-115">a.</span></span> <span data-ttu-id="bab1f-116">Hello tooyour 온-프레미스 서브넷에 해당 하는 IP 주소 리소스를 마우스 오른쪽 단추로 클릭 한 다음 선택 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="bab1f-116">Right-click hello IP address resource that corresponds tooyour on-premises subnet, and then select **Properties**.</span></span> <span data-ttu-id="bab1f-117">참고 hello IP 주소 이름 및 네트워크 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="bab1f-117">Note hello IP address name and network name.</span></span>
   
        <span data-ttu-id="bab1f-118">b.</span><span class="sxs-lookup"><span data-stu-id="bab1f-118">b.</span></span> <span data-ttu-id="bab1f-119">**고정 IP 주소**를 선택하고 사용되지 않은 IP 주소를 할당한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bab1f-119">Select **Static IP Address**, assign an unused IP address, and then click **OK**.</span></span>
 
   * <span data-ttu-id="bab1f-120">Azure 전용 솔루션 tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="bab1f-120">tooconfigure an Azure-only solution:</span></span>

        <span data-ttu-id="bab1f-121">a.</span><span class="sxs-lookup"><span data-stu-id="bab1f-121">a.</span></span> <span data-ttu-id="bab1f-122">Hello tooyour Azure 서브넷에 해당 하는 IP 주소 리소스를 마우스 오른쪽 단추로 클릭 한 다음 선택 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="bab1f-122">Right-click hello IP address resource that corresponds tooyour Azure subnet, and then select **Properties**.</span></span>
       
       > [!NOTE]
       > <span data-ttu-id="bab1f-123">나중에 hello 수신기 toocome 온라인 DHCP에 의해 선택 되는 충돌 하는 IP 주소로 인해 실패할 경우이 속성 창에서 유효한 고정 IP 주소를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bab1f-123">If hello listener later fails toocome online because of a conflicting IP address selected by DHCP, you can configure a valid static IP address in this properties window.</span></span>
       > 
       > 

       <span data-ttu-id="bab1f-124">b.</span><span class="sxs-lookup"><span data-stu-id="bab1f-124">b.</span></span> <span data-ttu-id="bab1f-125">동일한 hello **IP 주소** 속성 창, 변경 hello **IP 주소 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="bab1f-125">In hello same **IP Address** properties window, change hello **IP Address Name**.</span></span>  
        <span data-ttu-id="bab1f-126">이 이름은 hello PowerShell 스크립트의 hello $IPResourceName 변수에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bab1f-126">This name is used in hello $IPResourceName variable of hello PowerShell script.</span></span> <span data-ttu-id="bab1f-127">솔루션이 여러 Azure 가상 네트워크에 걸쳐 있는 경우 각 IP 리소스에 대해 이 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="bab1f-127">If your solution spans multiple Azure virtual networks, repeat this step for each IP resource.</span></span>

