### <a name="create-a-tcp-endpoint-for-the-virtual-machine"></a><span data-ttu-id="842ac-101">가상 컴퓨터용 TCP 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="842ac-101">Create a TCP endpoint for the virtual machine</span></span>
<span data-ttu-id="842ac-102">인터넷에서 SQL 서버에 연결하려면, 가상 컴퓨터에 들어오는 TCP 통신을 수신하는 끝점이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="842ac-102">In order to access SQL Server from the internet, the virtual machine must have an endpoint to listen for incoming TCP communication.</span></span> <span data-ttu-id="842ac-103">이 Azure 구성 단계에서는 들어오는 TCP 포트 트래픽을 가상 컴퓨터에 액세스 가능한 TCP 포트로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="842ac-103">This Azure configuration step, directs incoming TCP port traffic to a TCP port that is accessible to the virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="842ac-104">동일한 클라우드 서버 또는 가상 네트워크 내에서 연결하는 경우, 공개적으로 엑세스 할 수 있는 끝점을 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="842ac-104">If you are connecting within the same cloud service or virtual network, you do not have to create a publically accessible endpoint.</span></span> <span data-ttu-id="842ac-105">이 경우, 다음 단계를 계속 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="842ac-105">In that case, you could continue to the next step.</span></span> <span data-ttu-id="842ac-106">자세한 내용은 [연결 시나리오](../articles/virtual-machines/windows/sqlclassic/virtual-machines-windows-classic-sql-connect.md#connection-scenarios)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="842ac-106">For more information, see [Connection Scenarios](../articles/virtual-machines/windows/sqlclassic/virtual-machines-windows-classic-sql-connect.md#connection-scenarios).</span></span>
> 
> 

1. <span data-ttu-id="842ac-107">Azure 포털에서 **가상 컴퓨터(클래식)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="842ac-107">On the Azure Portal, select **Virtual machines (classic)**.</span></span>
2. <span data-ttu-id="842ac-108">그런 후 SQL Server 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="842ac-108">Then select you SQL Server virtual machine.</span></span>
3. <span data-ttu-id="842ac-109">**끝점**을 선택하고 끝점 블레이드 맨 위에 있는 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="842ac-109">Select **Endpoints**, and then click the **Add** button at the top of the Endpoints blade.</span></span>
   
    ![포털의 끝점 만들기 단계](./media/virtual-machines-sql-server-connection-steps/portal-endpoint-creation.png)
4. <span data-ttu-id="842ac-111">**끝점 추가** 블레이드에서 **이름**(예: SQLEndpoint)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="842ac-111">On the **Add Endpoint** blade, provide a **Name** such as SQLEndpoint.</span></span>
5. <span data-ttu-id="842ac-112">**프로토콜**로 **TCP**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="842ac-112">Select **TCP** for the **Protocol**.</span></span>
6. <span data-ttu-id="842ac-113">**공용 포트**에 대해 포트 번호(예: **57500**)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="842ac-113">For **Public port**, specify a port number such as **57500**.</span></span>
7. <span data-ttu-id="842ac-114">**개인 포트**에 대해 기본값이 **1433**인 SQL Server의 수신 대기 포트를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="842ac-114">For **Private port**, specify SQL Server's listening port, which defaults to **1433**.</span></span>
8. <span data-ttu-id="842ac-115">**확인** 을 클릭하여 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="842ac-115">Click **Ok** to create the endpoint.</span></span>

