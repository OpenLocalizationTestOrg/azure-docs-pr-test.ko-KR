1. [장애 조치(Failover) 클러스터 관리자]에서 **역할**을 펼친 다음 가용성 그룹을 강조 표시합니다.  

2. Hello에 **리소스** 탭, hello 수신기 이름을 마우스 오른쪽 단추로 클릭 한 후 **속성**합니다.

3. Hello 클릭 **종속성** 탭 합니다. 여러 리소스 목록에 없으면 IP 주소 hello OR, not 한지 확인 종속성이 AND가 있습니다.  

4. **확인**을 클릭합니다.

5. Hello 수신기 이름을 마우스 오른쪽 단추로 클릭 한 다음 **온라인 상태로 만들기**합니다.

6. 수신기는 hello에서 온라인으로 hello 후 **리소스** 탭, hello 가용성 그룹을 마우스 오른쪽 단추로 클릭 한 후 **속성**합니다.
   
    ![Hello 가용성 그룹 리소스 구성](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678772.gif)

7. (Hello IP 주소 리소스 이름 아님), hello 수신기 이름 리소스에 종속성을 만들고 클릭 **확인**합니다.
   
    ![Hello 수신기 이름에 종속성을 추가 합니다.](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678773.gif)

8. SQL Server Management Studio를 시작 하 고 toohello 주 복제본을 연결 합니다.

9. 너무 이동**AlwaysOn 고가용성** > **가용성 그룹** > **\<AvailabilityGroupName\>**   >  **가용성 그룹 수신기**합니다.  
    장애 조치 클러스터 관리자에서 만든 hello 수신기 이름이 표시 됩니다.

10. Hello 수신기 이름을 마우스 오른쪽 단추로 클릭 한 다음 **속성**합니다.

11. Hello에 **포트** 상자 이전 사용 $EndpointPort hello를 사용 하 여 hello 가용성 그룹 수신기에 대 한 hello 포트 번호를 지정 합니다 (이 자습서에서는 1433 hello이 기본값 이었습니다)를 클릭 하 고 **확인**합니다.

