이 단계에서는 수동으로 장애 조치 클러스터 관리자 및 SQL Server Management Studio에서 hello 가용성 그룹 수신기를 만듭니다.

1. Hello 주 복제본을 호스트 하는 hello 노드에서 장애 조치 클러스터 관리자를 엽니다.

2. 선택 hello **네트워크** 노드를 마우스 참고 hello 클러스터 네트워크 이름입니다. 이 이름은 hello $ClusterNetworkName 변수 hello PowerShell 스크립트에서에서 사용 됩니다.

3. Hello 클러스터 이름을 확장 한 다음 클릭 **역할**합니다.

4. Hello에 **역할** 창에서 마우스 오른쪽 단추로 클릭 hello 가용성 그룹 이름 및 선택한 후 **리소스 추가** > **클라이언트 액세스 지점**합니다.
   
    ![가용성 그룹에 대한 클라이언트 액세스 지점 추가](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678769.gif)

5. Hello에 **이름** 상자이 새 수신기 이름을 클릭 하 고 **다음** 을 두 번 클릭 하 고 **마침**합니다.  
    으로 설정 하지 않습니다 hello 수신기 또는 리소스를 온라인이 시점에서.

6. Hello 클릭 **리소스** 탭을 클릭 한 다음 방금 만든 hello 클라이언트 액세스 지점을 확장 합니다. 
    클러스터의 각 클러스터 네트워크에 대 한 IP 주소 리소스 hello 표시 됩니다. Azure 전용 솔루션인 경우 하나의 IP 주소 리소스만 표시됩니다.

7. Hello 다음 중 하나를 수행 합니다.
   
   * tooconfigure 하이브리드 솔루션:
     
        a. Hello tooyour 온-프레미스 서브넷에 해당 하는 IP 주소 리소스를 마우스 오른쪽 단추로 클릭 한 다음 선택 **속성**합니다. 참고 hello IP 주소 이름 및 네트워크 이름입니다.
   
        b. **고정 IP 주소**를 선택하고 사용되지 않은 IP 주소를 할당한 다음 **확인**을 클릭합니다.
 
   * Azure 전용 솔루션 tooconfigure:

        a. Hello tooyour Azure 서브넷에 해당 하는 IP 주소 리소스를 마우스 오른쪽 단추로 클릭 한 다음 선택 **속성**합니다.
       
       > [!NOTE]
       > 나중에 hello 수신기 toocome 온라인 DHCP에 의해 선택 되는 충돌 하는 IP 주소로 인해 실패할 경우이 속성 창에서 유효한 고정 IP 주소를 구성할 수 있습니다.
       > 
       > 

       b. 동일한 hello **IP 주소** 속성 창, 변경 hello **IP 주소 이름**합니다.  
        이 이름은 hello PowerShell 스크립트의 hello $IPResourceName 변수에 사용 됩니다. 솔루션이 여러 Azure 가상 네트워크에 걸쳐 있는 경우 각 IP 리소스에 대해 이 단계를 반복합니다.

