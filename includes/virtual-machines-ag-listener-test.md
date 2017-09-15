<span data-ttu-id="1a6e6-101">이 단계에서는 동일한 네트워크에서 실행 중인 클라이언트 응용 프로그램을 사용하여 가용성 그룹 수신기를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="1a6e6-101">In this step, you test the availability group listener by using a client application that's running on the same network.</span></span>

<span data-ttu-id="1a6e6-102">클라이언트 연결에는 다음 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a6e6-102">Client connectivity has the following requirements:</span></span>

* <span data-ttu-id="1a6e6-103">수신기에 대한 클라이언트 연결은 AlwaysOn 가용성 복제본을 호스팅하는 클라우드 서비스와 다른 클라우드 서비스에 있는 컴퓨터에서 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a6e6-103">Client connections to the listener must come from machines that reside in a different cloud service than the one that hosts the Always On availability replicas.</span></span>
* <span data-ttu-id="1a6e6-104">Always On 복제본이 다른 서브넷에 있는 경우 클라이언트는 연결 문자열에 *MultisubnetFailover=True* 를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a6e6-104">If the Always On replicas are in different subnets, clients must specify *MultisubnetFailover=True* in the connection string.</span></span> <span data-ttu-id="1a6e6-105">이 조건은 다양한 서브넷에 있는 복제본에 대한 병렬 연결을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="1a6e6-105">This condition results in parallel connection attempts to replicas in the various subnets.</span></span> <span data-ttu-id="1a6e6-106">이 시나리오에는 지역 간 AlwaysOn 가용성 그룹 배포가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a6e6-106">This scenario includes a cross-region Always On availability group deployment.</span></span>

<span data-ttu-id="1a6e6-107">하나의 예로, 동일한 Azure 가상 네트워크의 VM(하지만 복제본을 호스팅하지 않는 VM) 중 하나에서 수신기에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="1a6e6-107">One example is to connect to the listener from one of the VMs in the same Azure virtual network (but not one that hosts a replica).</span></span> <span data-ttu-id="1a6e6-108">이 테스트를 완료하는 쉬운 방법은 SQL Server Management Studio를 가용성 그룹 수신기에 연결하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1a6e6-108">An easy way to complete this test is to try to connect SQL Server Management Studio to the availability group listener.</span></span> <span data-ttu-id="1a6e6-109">또 다른 간단한 방법은 다음과 같이 [SQLCMD.exe](https://technet.microsoft.com/library/ms162773.aspx)를 실행하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1a6e6-109">Another simple method is to run [SQLCMD.exe](https://technet.microsoft.com/library/ms162773.aspx), as follows:</span></span>

    sqlcmd -S "<ListenerName>,<EndpointPort>" -d "<DatabaseName>" -Q "select @@servername, db_name()" -l 15

> [!NOTE]
> <span data-ttu-id="1a6e6-110">EndpointPort 값이 *1433*이면 호출에서 이를 지정하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a6e6-110">If the EndpointPort value is *1433*, you are not required to specify it in the call.</span></span> <span data-ttu-id="1a6e6-111">또한 이전 호출에서는 클라이언트 컴퓨터가 동일한 도메인에 조인되어 있고 Windows 인증을 사용하여 호출자에게 데이터베이스에 대한 권한이 부여되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="1a6e6-111">The previous call also assumes that the client machine is joined to the same domain and that the caller has been granted permissions on the database by using Windows authentication.</span></span>
> 
> 

<span data-ttu-id="1a6e6-112">수신기를 테스트할 때 클라이언트에서 장애 조치를 통해 수신기에 연결할 수 있는지 확인하려면 가용성 그룹을 장애 조치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a6e6-112">When you test the listener, be sure to fail over the availability group to make sure that clients can connect to the listener across failovers.</span></span>

