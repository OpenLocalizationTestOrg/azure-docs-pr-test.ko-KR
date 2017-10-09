<span data-ttu-id="578f7-101">hello 가용성 그룹 수신기는 가용성 그룹에서 수신 대기 하는 SQL Server hello는 IP 주소와 네트워크 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-101">hello availability group listener is an IP address and network name that hello SQL Server availability group listens on.</span></span> <span data-ttu-id="578f7-102">toocreate hello 가용성 그룹 수신기는 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-102">toocreate hello availability group listener, do hello following:</span></span>

1. <span data-ttu-id="578f7-103"><a name="getnet"></a>Hello 클러스터 네트워크 리소스의 hello 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-103"><a name="getnet"></a>Get hello name of hello cluster network resource.</span></span>

    <span data-ttu-id="578f7-104">a.</span><span class="sxs-lookup"><span data-stu-id="578f7-104">a.</span></span> <span data-ttu-id="578f7-105">RDP tooconnect toohello hello 주 복제본을 호스팅하는 Azure 가상 컴퓨터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-105">Use RDP tooconnect toohello Azure virtual machine that hosts hello primary replica.</span></span> 

    <span data-ttu-id="578f7-106">b.</span><span class="sxs-lookup"><span data-stu-id="578f7-106">b.</span></span> <span data-ttu-id="578f7-107">장애 조치(failover) 클러스터 관리자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-107">Open Failover Cluster Manager.</span></span>

    <span data-ttu-id="578f7-108">c.</span><span class="sxs-lookup"><span data-stu-id="578f7-108">c.</span></span> <span data-ttu-id="578f7-109">선택 hello **네트워크** 노드와 참고 hello 클러스터 네트워크 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-109">Select hello **Networks** node, and note hello cluster network name.</span></span> <span data-ttu-id="578f7-110">Hello에이 이름을 사용 `$ClusterNetworkName` hello PowerShell 스크립트의에서 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-110">Use this name in hello `$ClusterNetworkName` variable in hello PowerShell script.</span></span> <span data-ttu-id="578f7-111">Hello은 이미지 hello 클러스터 네트워크 이름 뒤에 나오는 **클러스터 네트워크 1**:</span><span class="sxs-lookup"><span data-stu-id="578f7-111">In hello following image hello cluster network name is **Cluster Network 1**:</span></span>

   ![클러스터 네트워크 이름](./media/virtual-machines-ag-listener-configure/90-clusternetworkname.png)

2. <span data-ttu-id="578f7-113"><a name="addcap"></a>Hello 클라이언트 액세스 지점을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-113"><a name="addcap"></a>Add hello client access point.</span></span>  
    <span data-ttu-id="578f7-114">hello 클라이언트 액세스 지점 이름이 hello 네트워크 응용 프로그램에서 사용할 tooconnect toohello 데이터베이스는 가용성 그룹 에서입니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-114">hello client access point is hello network name that applications use tooconnect toohello databases in an availability group.</span></span> <span data-ttu-id="578f7-115">Hello 클라이언트 액세스 지점에서 장애 조치 클러스터 관리자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-115">Create hello client access point in Failover Cluster Manager.</span></span>

    <span data-ttu-id="578f7-116">a.</span><span class="sxs-lookup"><span data-stu-id="578f7-116">a.</span></span> <span data-ttu-id="578f7-117">Hello 클러스터 이름을 확장 한 다음 클릭 **역할**합니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-117">Expand hello cluster name, and then click **Roles**.</span></span>

    <span data-ttu-id="578f7-118">b.</span><span class="sxs-lookup"><span data-stu-id="578f7-118">b.</span></span> <span data-ttu-id="578f7-119">Hello에 **역할** 창에서 마우스 오른쪽 단추로 클릭 hello 가용성 그룹 이름 및 선택한 후 **리소스 추가** > **클라이언트 액세스 지점**합니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-119">In hello **Roles** pane, right-click hello availability group name, and then select **Add Resource** > **Client Access Point**.</span></span>

   ![클라이언트 액세스 지점](./media/virtual-machines-ag-listener-configure/92-addclientaccesspoint.png)

    <span data-ttu-id="578f7-121">c.</span><span class="sxs-lookup"><span data-stu-id="578f7-121">c.</span></span> <span data-ttu-id="578f7-122">Hello에 **이름** 상자에서이 새 수신기의 이름을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-122">In hello **Name** box, create a name for this new listener.</span></span> 
   <span data-ttu-id="578f7-123">hello hello 새 수신기 이름이 응용 프로그램에서 사용할 tooconnect toodatabases hello SQL Server 가용성 그룹의 hello 네트워크 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-123">hello name for hello new listener is hello network name that applications use tooconnect toodatabases in hello SQL Server availability group.</span></span>
   
    <span data-ttu-id="578f7-124">d.</span><span class="sxs-lookup"><span data-stu-id="578f7-124">d.</span></span> <span data-ttu-id="578f7-125">hello 수신기를 만드는 toofinish를 클릭 하 여 **다음** 을 두 번 클릭 하 고 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-125">toofinish creating hello listener, click **Next** twice, and then click **Finish**.</span></span> <span data-ttu-id="578f7-126">으로 설정 하지 않습니다 hello 수신기 또는 리소스를 온라인이 시점에서.</span><span class="sxs-lookup"><span data-stu-id="578f7-126">Do not bring hello listener or resource online at this point.</span></span>

3. <span data-ttu-id="578f7-127"><a name="congroup"></a>Hello 가용성 그룹에 대 한 hello IP 리소스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-127"><a name="congroup"></a>Configure hello IP resource for hello availability group.</span></span>

    <span data-ttu-id="578f7-128">a.</span><span class="sxs-lookup"><span data-stu-id="578f7-128">a.</span></span> <span data-ttu-id="578f7-129">Hello 클릭 **리소스** 탭을 클릭 한 다음 만든 hello 클라이언트 액세스 지점을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-129">Click hello **Resources** tab, and then expand hello client access point you created.</span></span>  
    <span data-ttu-id="578f7-130">hello 클라이언트 액세스 지점이 오프 라인입니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-130">hello client access point is offline.</span></span>

   ![클라이언트 액세스 지점](./media/virtual-machines-ag-listener-configure/94-newclientaccesspoint.png) 

    <span data-ttu-id="578f7-132">b.</span><span class="sxs-lookup"><span data-stu-id="578f7-132">b.</span></span> <span data-ttu-id="578f7-133">Hello IP 리소스를 마우스 오른쪽 단추로 클릭 하 고 properties를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-133">Right-click hello IP resource, and then click properties.</span></span> <span data-ttu-id="578f7-134">Hello IP 주소의 hello 이름을 확인 하 고 사용 하 여 hello에 `$IPResourceName` hello PowerShell 스크립트의에서 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-134">Note hello name of hello IP address, and use it in hello `$IPResourceName` variable in hello PowerShell script.</span></span>

    <span data-ttu-id="578f7-135">c.</span><span class="sxs-lookup"><span data-stu-id="578f7-135">c.</span></span> <span data-ttu-id="578f7-136">**IP 주소**에서 **고정 IP 주소**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-136">Under **IP Address**, click **Static IP Address**.</span></span> <span data-ttu-id="578f7-137">Hello 동일한 주소 한 hello Azure 포털에 hello 부하 분산 장치 주소를 설정할 때 사용 하는 hello IP 주소를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-137">Set hello IP address as hello same address that you used when you set hello load balancer address on hello Azure portal.</span></span>

   ![IP 리소스](./media/virtual-machines-ag-listener-configure/96-ipresource.png) 

    <!-----------------------I don't see this option on server 2016
    1. Disable NetBIOS for this address and click **OK**. Repeat this step for each IP resource if your solution spans multiple Azure VNets. 
    ------------------------->

4. <span data-ttu-id="578f7-139"><a name = "dependencyGroup"></a>Hello SQL Server 가용성 그룹 리소스가 hello 클라이언트 액세스 지점에 종속 되 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-139"><a name = "dependencyGroup"></a>Make hello SQL Server availability group resource dependent on hello client access point.</span></span>

    <span data-ttu-id="578f7-140">a.</span><span class="sxs-lookup"><span data-stu-id="578f7-140">a.</span></span> <span data-ttu-id="578f7-141">[장애 조치(Failover) 클러스터 관리자]에서 **역할**을 클릭한 다음 가용성 그룹을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-141">In Failover Cluster Manager, click **Roles**, and then click your availability group.</span></span>

    <span data-ttu-id="578f7-142">b.</span><span class="sxs-lookup"><span data-stu-id="578f7-142">b.</span></span> <span data-ttu-id="578f7-143">Hello에 **리소스** 탭의 **기타 리소스**hello 가용성 리소스 그룹을 마우스 오른쪽 단추로 클릭 한 다음 클릭 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-143">On hello **Resources** tab, under **Other Resources**, right-click hello availability resource group, and then click **Properties**.</span></span> 

    <span data-ttu-id="578f7-144">c.</span><span class="sxs-lookup"><span data-stu-id="578f7-144">c.</span></span> <span data-ttu-id="578f7-145">Hello 종속성 탭에서 hello 클라이언트 액세스 지점 (hello 수신기) 리소스의 hello 이름을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-145">On hello dependencies tab, add hello name of hello client access point (hello listener) resource.</span></span>

   ![IP 리소스](./media/virtual-machines-ag-listener-configure/97-propertiesdependencies.png) 

    <span data-ttu-id="578f7-147">d.</span><span class="sxs-lookup"><span data-stu-id="578f7-147">d.</span></span> <span data-ttu-id="578f7-148">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-148">Click **OK**.</span></span>

5. <span data-ttu-id="578f7-149"><a name="listname"></a>Hello 클라이언트 액세스 지점 hello IP 주소에 종속 되는 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-149"><a name="listname"></a>Make hello client access point resource dependent on hello IP address.</span></span>

    <span data-ttu-id="578f7-150">a.</span><span class="sxs-lookup"><span data-stu-id="578f7-150">a.</span></span> <span data-ttu-id="578f7-151">[장애 조치(Failover) 클러스터 관리자]에서 **역할**을 클릭한 다음 가용성 그룹을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-151">In Failover Cluster Manager, click **Roles**, and then click your availability group.</span></span> 

    <span data-ttu-id="578f7-152">b.</span><span class="sxs-lookup"><span data-stu-id="578f7-152">b.</span></span> <span data-ttu-id="578f7-153">Hello에 **리소스** 탭에서 아래 hello 클라이언트 액세스 지점 리소스를 마우스 오른쪽 단추로 클릭 **서버 이름**, 클릭 하 고 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-153">On hello **Resources** tab, right-click hello client access point resource under **Server Name**, and then click **Properties**.</span></span> 

   ![IP 리소스](./media/virtual-machines-ag-listener-configure/98-dependencies.png) 

    <span data-ttu-id="578f7-155">c.</span><span class="sxs-lookup"><span data-stu-id="578f7-155">c.</span></span> <span data-ttu-id="578f7-156">Hello 클릭 **종속성** 탭 합니다. Hello IP 주소 종속성 인지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="578f7-156">Click hello **Dependencies** tab. Verify that hello IP address is a dependency.</span></span> <span data-ttu-id="578f7-157">그럴 경우 hello IP 주소에 대 한 종속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-157">If it is not, set a dependency on hello IP address.</span></span> <span data-ttu-id="578f7-158">나열 된 여러 리소스가 있으면 hello IP 주소 OR, not 한지 확인 종속성이 AND가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-158">If there are multiple resources listed, verify that hello IP addresses have OR, not AND, dependencies.</span></span> <span data-ttu-id="578f7-159">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-159">Click **OK**.</span></span> 

   ![IP 리소스](./media/virtual-machines-ag-listener-configure/98-propertiesdependencies.png) 

    <span data-ttu-id="578f7-161">d.</span><span class="sxs-lookup"><span data-stu-id="578f7-161">d.</span></span> <span data-ttu-id="578f7-162">Hello 수신기 이름을 마우스 오른쪽 단추로 클릭 한 다음 **온라인 상태로 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-162">Right-click hello listener name, and then click **Bring Online**.</span></span> 

    >[!TIP]
    ><span data-ttu-id="578f7-163">종속성이 올바르게 구성 되어 해당 hello를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-163">You can validate that hello dependencies are correctly configured.</span></span> <span data-ttu-id="578f7-164">장애 조치 클러스터 관리자에서 이동 tooRoles hello 가용성 그룹을 마우스 오른쪽 단추로 클릭 하 여 **기타 작업**, 클릭 하 고 **종속성 보고서 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-164">In Failover Cluster Manager, go tooRoles, right-click hello availability group, click **More Actions**, and then click  **Show Dependency Report**.</span></span> <span data-ttu-id="578f7-165">Hello 종속성이 제대로 구성 하는 경우 hello 가용성 그룹 hello 네트워크 이름 뒤에 종속적 이며 hello 네트워크 이름 hello IP 주소에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-165">When hello dependencies are correctly configured, hello availability group is dependent on hello network name, and hello network name is dependent on hello IP address.</span></span> 


6. <span data-ttu-id="578f7-166"><a name="setparam"></a>PowerShell에서 hello 클러스터 매개 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-166"><a name="setparam"></a>Set hello cluster parameters in PowerShell.</span></span>
    
    <span data-ttu-id="578f7-167">a.</span><span class="sxs-lookup"><span data-stu-id="578f7-167">a.</span></span> <span data-ttu-id="578f7-168">다음 PowerShell 스크립트 tooone SQL Server 인스턴스의 hello를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-168">Copy hello following PowerShell script tooone of your SQL Server instances.</span></span> <span data-ttu-id="578f7-169">사용자 환경에 대 한 hello 변수를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-169">Update hello variables for your environment.</span></span>     
    
    ```PowerShell
    $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
    $IPResourceName = "<IPResourceName>" # hello IP Address resource name
    $ILBIP = “<n.n.n.n>” # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
    [int]$ProbePort = <nnnnn>
    
    Import-Module FailoverClusters
    
    Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
    ```

    <span data-ttu-id="578f7-170">b.</span><span class="sxs-lookup"><span data-stu-id="578f7-170">b.</span></span> <span data-ttu-id="578f7-171">Hello 클러스터 노드 중 하나에서 hello PowerShell 스크립트를 실행 하 여 hello 클러스터 매개 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-171">Set hello cluster parameters by running hello PowerShell script on one of hello cluster nodes.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="578f7-172">SQL Server 인스턴스가 별도 영역에 있는 경우 toorun hello PowerShell 스크립트 두 번 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-172">If your SQL Server instances are in separate regions, you need toorun hello PowerShell script twice.</span></span> <span data-ttu-id="578f7-173">처음으로 hello, hello를 사용 하 여 `$ILBIP` 및 `$ProbePort` hello 첫 번째 지역에서입니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-173">hello first time, use hello `$ILBIP` and `$ProbePort` from hello first region.</span></span> <span data-ttu-id="578f7-174">두 번째로 hello, hello를 사용 하 여 `$ILBIP` 및 `$ProbePort` hello 두 번째 지역에서입니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-174">hello second time, use hello `$ILBIP` and `$ProbePort` from hello second region.</span></span> <span data-ttu-id="578f7-175">hello 클러스터 네트워크 이름 및 클러스터 IP 리소스 이름을 hello 같은 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="578f7-175">hello cluster network name and hello cluster IP resource name are hello same.</span></span> 
