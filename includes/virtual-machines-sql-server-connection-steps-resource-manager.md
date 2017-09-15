### <a name="configure-a-dns-label-for-the-public-ip-address"></a><span data-ttu-id="d3e8f-101">공용 IP 주소에 대한 DNS 레이블 구성</span><span class="sxs-lookup"><span data-stu-id="d3e8f-101">Configure a DNS Label for the public IP address</span></span>

<span data-ttu-id="d3e8f-102">인터넷에서 SQL Server 데이터베이스 엔진에 연결하려면 공용 IP 주소에 대한 DNS 레이블을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d3e8f-102">To connect to the SQL Server Database Engine from the Internet, consider creating a DNS Label for your public IP address.</span></span> <span data-ttu-id="d3e8f-103">IP 주소로 연결할 수 있지만 DNS 레이블이 기본 공용 IP 주소를 쉽게 식별 및 추상화하는 A 레코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d3e8f-103">You can connect by IP address, but the DNS Label creates an A Record that is easier to identify and abstracts the underlying public IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="d3e8f-104">동일한 가상 네트워크 내에서 또는 로컬로 SQL Server 인스턴스에 연결하려는 경우 DNS 레이블이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d3e8f-104">DNS Labels are not required if you plan to only connect to the SQL Server instance within the same Virtual Network or only locally.</span></span>

<span data-ttu-id="d3e8f-105">DNS 레이블을 만들려면 먼저 포털에서 **가상 컴퓨터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d3e8f-105">To create a DNS Label, first select **Virtual machines** in the portal.</span></span> <span data-ttu-id="d3e8f-106">SQL Server VM을 선택하여 속성을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d3e8f-106">Select your SQL Server VM to bring up its properties.</span></span>

1. <span data-ttu-id="d3e8f-107">가상 컴퓨터 개요에서 **공용 IP 주소**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d3e8f-107">In the virtual machine overview, select your **Public IP address**.</span></span>

    ![공용 IP 주소](./media/virtual-machines-sql-server-connection-steps/rm-public-ip-address.png)

1. <span data-ttu-id="d3e8f-109">공용 IP 주소에 대한 속성에서 **구성**을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="d3e8f-109">In the properties for your Public IP address, expand **Configuration**.</span></span>

1. <span data-ttu-id="d3e8f-110">DNS 레이블 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d3e8f-110">Enter a DNS Label name.</span></span> <span data-ttu-id="d3e8f-111">이 이름은 IP 주소로 직접 연결하는 대신 이름으로 SQL Server VM에 연결하는 데 사용할 수 있는 A 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="d3e8f-111">This name is an A Record that can be used to connect to your SQL Server VM by name instead of by IP Address directly.</span></span>

1. <span data-ttu-id="d3e8f-112">**저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3e8f-112">Click the **Save** button.</span></span>

    ![dns 레이블](./media/virtual-machines-sql-server-connection-steps/rm-dns-label.png)

### <a name="connect-to-the-database-engine-from-another-computer"></a><span data-ttu-id="d3e8f-114">다른 컴퓨터에서 데이터베이스 엔진에 연결</span><span class="sxs-lookup"><span data-stu-id="d3e8f-114">Connect to the Database Engine from another computer</span></span>

1. <span data-ttu-id="d3e8f-115">인터넷에 연결된 컴퓨터에서 SSMS(SQL Server Management Studio)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d3e8f-115">On a computer connected to the internet, open SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="d3e8f-116">SQL Server Management Studio가 없는 경우 [여기](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3e8f-116">If you do not have SQL Server Management Studio, you can download it [here](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>

1. <span data-ttu-id="d3e8f-117">**서버에 연결** 또는 **데이터베이스 엔진에 연결** 대화 상자에서 **서버 이름** 값을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="d3e8f-117">In the **Connect to Server** or **Connect to Database Engine** dialog box, edit the **Server name** value.</span></span> <span data-ttu-id="d3e8f-118">가상 컴퓨터의 IP 주소 또는 전체 DNS 이름을 입력합니다(이전 작업에서 확인).</span><span class="sxs-lookup"><span data-stu-id="d3e8f-118">Enter the IP address or full DNS name of the virtual machine (determined in the previous task).</span></span> <span data-ttu-id="d3e8f-119">쉼표를 추가하고 SQL Server의 TCP 포트를 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3e8f-119">You can also add a comma and provide SQL Server's TCP port.</span></span> <span data-ttu-id="d3e8f-120">예: `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.</span><span class="sxs-lookup"><span data-stu-id="d3e8f-120">For example, `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.</span></span>

1. <span data-ttu-id="d3e8f-121">**인증** 상자에 **SQL Server 인증**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d3e8f-121">In the **Authentication** box, select **SQL Server Authentication**.</span></span>

1. <span data-ttu-id="d3e8f-122">**로그인** 상자에 올바른 SQL 로그인 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d3e8f-122">In the **Login** box, type the name of a valid SQL login.</span></span>

1. <span data-ttu-id="d3e8f-123">**암호** 상자에 로그인 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d3e8f-123">In the **Password** box, type the password of the login.</span></span>

1. <span data-ttu-id="d3e8f-124">**Connect**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3e8f-124">Click **Connect**.</span></span>

    ![ssms 연결](./media/virtual-machines-sql-server-connection-steps/rm-ssms-connect.png)