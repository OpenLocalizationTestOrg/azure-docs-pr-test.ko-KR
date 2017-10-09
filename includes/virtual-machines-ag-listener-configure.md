hello 가용성 그룹 수신기는 가용성 그룹에서 수신 대기 하는 SQL Server hello는 IP 주소와 네트워크 이름입니다. toocreate hello 가용성 그룹 수신기는 다음 hello지 않습니다.

1. <a name="getnet"></a>Hello 클러스터 네트워크 리소스의 hello 이름을 가져옵니다.

    a. RDP tooconnect toohello hello 주 복제본을 호스팅하는 Azure 가상 컴퓨터를 사용 합니다. 

    b. 장애 조치(failover) 클러스터 관리자를 엽니다.

    c. 선택 hello **네트워크** 노드와 참고 hello 클러스터 네트워크 이름입니다. Hello에이 이름을 사용 `$ClusterNetworkName` hello PowerShell 스크립트의에서 변수입니다. Hello은 이미지 hello 클러스터 네트워크 이름 뒤에 나오는 **클러스터 네트워크 1**:

   ![클러스터 네트워크 이름](./media/virtual-machines-ag-listener-configure/90-clusternetworkname.png)

2. <a name="addcap"></a>Hello 클라이언트 액세스 지점을 추가 합니다.  
    hello 클라이언트 액세스 지점 이름이 hello 네트워크 응용 프로그램에서 사용할 tooconnect toohello 데이터베이스는 가용성 그룹 에서입니다. Hello 클라이언트 액세스 지점에서 장애 조치 클러스터 관리자를 만듭니다.

    a. Hello 클러스터 이름을 확장 한 다음 클릭 **역할**합니다.

    b. Hello에 **역할** 창에서 마우스 오른쪽 단추로 클릭 hello 가용성 그룹 이름 및 선택한 후 **리소스 추가** > **클라이언트 액세스 지점**합니다.

   ![클라이언트 액세스 지점](./media/virtual-machines-ag-listener-configure/92-addclientaccesspoint.png)

    c. Hello에 **이름** 상자에서이 새 수신기의 이름을 만듭니다. 
   hello hello 새 수신기 이름이 응용 프로그램에서 사용할 tooconnect toodatabases hello SQL Server 가용성 그룹의 hello 네트워크 이름입니다.
   
    d. hello 수신기를 만드는 toofinish를 클릭 하 여 **다음** 을 두 번 클릭 하 고 **마침**합니다. 으로 설정 하지 않습니다 hello 수신기 또는 리소스를 온라인이 시점에서.

3. <a name="congroup"></a>Hello 가용성 그룹에 대 한 hello IP 리소스를 구성 합니다.

    a. Hello 클릭 **리소스** 탭을 클릭 한 다음 만든 hello 클라이언트 액세스 지점을 확장 합니다.  
    hello 클라이언트 액세스 지점이 오프 라인입니다.

   ![클라이언트 액세스 지점](./media/virtual-machines-ag-listener-configure/94-newclientaccesspoint.png) 

    b. Hello IP 리소스를 마우스 오른쪽 단추로 클릭 하 고 properties를 클릭 합니다. Hello IP 주소의 hello 이름을 확인 하 고 사용 하 여 hello에 `$IPResourceName` hello PowerShell 스크립트의에서 변수입니다.

    c. **IP 주소**에서 **고정 IP 주소**를 클릭합니다. Hello 동일한 주소 한 hello Azure 포털에 hello 부하 분산 장치 주소를 설정할 때 사용 하는 hello IP 주소를 설정 합니다.

   ![IP 리소스](./media/virtual-machines-ag-listener-configure/96-ipresource.png) 

    <!-----------------------I don't see this option on server 2016
    1. Disable NetBIOS for this address and click **OK**. Repeat this step for each IP resource if your solution spans multiple Azure VNets. 
    ------------------------->

4. <a name = "dependencyGroup"></a>Hello SQL Server 가용성 그룹 리소스가 hello 클라이언트 액세스 지점에 종속 되 게 합니다.

    a. [장애 조치(Failover) 클러스터 관리자]에서 **역할**을 클릭한 다음 가용성 그룹을 클릭합니다.

    b. Hello에 **리소스** 탭의 **기타 리소스**hello 가용성 리소스 그룹을 마우스 오른쪽 단추로 클릭 한 다음 클릭 **속성**합니다. 

    c. Hello 종속성 탭에서 hello 클라이언트 액세스 지점 (hello 수신기) 리소스의 hello 이름을 추가 합니다.

   ![IP 리소스](./media/virtual-machines-ag-listener-configure/97-propertiesdependencies.png) 

    d. **확인**을 클릭합니다.

5. <a name="listname"></a>Hello 클라이언트 액세스 지점 hello IP 주소에 종속 되는 리소스입니다.

    a. [장애 조치(Failover) 클러스터 관리자]에서 **역할**을 클릭한 다음 가용성 그룹을 클릭합니다. 

    b. Hello에 **리소스** 탭에서 아래 hello 클라이언트 액세스 지점 리소스를 마우스 오른쪽 단추로 클릭 **서버 이름**, 클릭 하 고 **속성**합니다. 

   ![IP 리소스](./media/virtual-machines-ag-listener-configure/98-dependencies.png) 

    c. Hello 클릭 **종속성** 탭 합니다. Hello IP 주소 종속성 인지 확인 하십시오. 그럴 경우 hello IP 주소에 대 한 종속성을 설정 합니다. 나열 된 여러 리소스가 있으면 hello IP 주소 OR, not 한지 확인 종속성이 AND가 있습니다. **확인**을 클릭합니다. 

   ![IP 리소스](./media/virtual-machines-ag-listener-configure/98-propertiesdependencies.png) 

    d. Hello 수신기 이름을 마우스 오른쪽 단추로 클릭 한 다음 **온라인 상태로 만들기**합니다. 

    >[!TIP]
    >종속성이 올바르게 구성 되어 해당 hello를 확인할 수 있습니다. 장애 조치 클러스터 관리자에서 이동 tooRoles hello 가용성 그룹을 마우스 오른쪽 단추로 클릭 하 여 **기타 작업**, 클릭 하 고 **종속성 보고서 표시**합니다. Hello 종속성이 제대로 구성 하는 경우 hello 가용성 그룹 hello 네트워크 이름 뒤에 종속적 이며 hello 네트워크 이름 hello IP 주소에 따라 달라 집니다. 


6. <a name="setparam"></a>PowerShell에서 hello 클러스터 매개 변수를 설정 합니다.
    
    a. 다음 PowerShell 스크립트 tooone SQL Server 인스턴스의 hello를 복사 합니다. 사용자 환경에 대 한 hello 변수를 업데이트 합니다.     
    
    ```PowerShell
    $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
    $IPResourceName = "<IPResourceName>" # hello IP Address resource name
    $ILBIP = “<n.n.n.n>” # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
    [int]$ProbePort = <nnnnn>
    
    Import-Module FailoverClusters
    
    Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
    ```

    b. Hello 클러스터 노드 중 하나에서 hello PowerShell 스크립트를 실행 하 여 hello 클러스터 매개 변수를 설정 합니다.  

    > [!NOTE]
    > SQL Server 인스턴스가 별도 영역에 있는 경우 toorun hello PowerShell 스크립트 두 번 필요 합니다. 처음으로 hello, hello를 사용 하 여 `$ILBIP` 및 `$ProbePort` hello 첫 번째 지역에서입니다. 두 번째로 hello, hello를 사용 하 여 `$ILBIP` 및 `$ProbePort` hello 두 번째 지역에서입니다. hello 클러스터 네트워크 이름 및 클러스터 IP 리소스 이름을 hello 같은 hello 됩니다. 
