1. <span data-ttu-id="f079c-101">[장애 조치(Failover) 클러스터 관리자]에서 **역할**을 펼친 다음 가용성 그룹을 강조 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f079c-101">In Failover Cluster Manager, expand **Roles**, and then highlight your availability group.</span></span>  

2. <span data-ttu-id="f079c-102">**리소스** 탭에서 수신기 이름을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f079c-102">On the **Resources** tab, right-click the listener name, and then click **Properties**.</span></span>

3. <span data-ttu-id="f079c-103">**종속성** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f079c-103">Click the **Dependencies** tab.</span></span> <span data-ttu-id="f079c-104">여러 리소스가 나열되면 IP 주소에 AND가 아니라 OR 종속성이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f079c-104">If multiple resources are listed, verify that the IP addresses have OR, not AND, dependencies.</span></span>  

4. <span data-ttu-id="f079c-105">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f079c-105">Click **OK**.</span></span>

5. <span data-ttu-id="f079c-106">수신기 이름을 마우스 오른쪽 단추로 클릭한 다음 **온라인 상태로 전환**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f079c-106">Right-click the listener name, and then click **Bring Online**.</span></span>

6. <span data-ttu-id="f079c-107">수신기가 온라인 상태로 전환되면 **리소스** 탭에서 가용성 그룹을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f079c-107">After the listener is online, on the **Resources** tab, right-click the availability group, and then click **Properties**.</span></span>
   
    ![가용성 그룹 리소스 구성](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678772.gif)

7. <span data-ttu-id="f079c-109">수신기 이름 리소스(IP 주소 리소스 이름이 아님)에 대한 종속성을 만든 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f079c-109">Create a dependency on the listener name resource (not the IP address resources name), and then click **OK**.</span></span>
   
    ![수신기 이름에 대한 종속성 추가](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678773.gif)

8. <span data-ttu-id="f079c-111">SQL Server Management Studio를 시작한 다음 주 복제본에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f079c-111">Start SQL Server Management Studio, and then connect to the primary replica.</span></span>

9. <span data-ttu-id="f079c-112">**AlwaysOn 고가용성** > **가용성 그룹** > **\<AvailabilityGroupName\>** > **가용성 그룹 수신기**로 차례로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f079c-112">Go to **AlwaysOn High Availability** > **Availability Groups** > **\<AvailabilityGroupName\>** > **Availability Group Listeners**.</span></span>  
    <span data-ttu-id="f079c-113">[장애 조치(Failover) 클러스터 관리자]에서 만든 수신기 이름이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f079c-113">The listener name that you created in Failover Cluster Manager should be displayed.</span></span>

10. <span data-ttu-id="f079c-114">수신기 이름을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f079c-114">Right-click the listener name, and then click **Properties**.</span></span>

11. <span data-ttu-id="f079c-115">**포트** 상자에서 이전에 사용한 $EndpointPort를 사용하여 가용성 그룹 수신기에 대한 포트 번호(이 자습서에서는 1433이 기본값임)를 지정한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f079c-115">In the **Port** box, specify the port number for the availability group listener by using the $EndpointPort that you used earlier (in this tutorial, 1433 was the default), and then click **OK**.</span></span>

