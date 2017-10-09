## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="d1e8b-101">Azure 포털 toohello에 로그인</span><span class="sxs-lookup"><span data-stu-id="d1e8b-101">Log in toohello Azure portal</span></span>

<span data-ttu-id="d1e8b-102">Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-102">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-blank-sql-database-using-hello-azure-portal"></a><span data-ttu-id="d1e8b-103">Hello Azure 포털을 사용 하 여 빈 SQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="d1e8b-103">Create a blank SQL database using hello Azure portal</span></span>

<span data-ttu-id="d1e8b-104">Azure SQL Database는 일련의 정의된 [계산 및 저장소 리소스](../articles/sql-database/sql-database-service-tiers.md)를 사용하여 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-104">An Azure SQL database is created with a defined set of [compute and storage resources](../articles/sql-database/sql-database-service-tiers.md).</span></span> <span data-ttu-id="d1e8b-105">hello 데이터베이스 내에서 만들어집니다는 [Azure 리소스 그룹](../articles/azure-resource-manager/resource-group-overview.md) 및는 [Azure SQL 데이터베이스 논리 서버](../articles/sql-database/sql-database-features.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-105">hello database is created within an [Azure resource group](../articles/azure-resource-manager/resource-group-overview.md) and in an [Azure SQL Database logical server](../articles/sql-database/sql-database-features.md).</span></span> 

<span data-ttu-id="d1e8b-106">이러한 단계 toocreate 빈 SQL 데이터베이스를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-106">Follow these steps toocreate a blank SQL database.</span></span> 

1. <span data-ttu-id="d1e8b-107">Hello 클릭 **새로** 단추 hello 왼쪽 위 모서리의 hello Azure 포털에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-107">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="d1e8b-108">선택 **데이터베이스** hello에서 **새로** 선택한 페이지 **SQL 데이터베이스** hello에서 **데이터베이스** 페이지.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-108">Select **Databases** from hello **New** page, and select **SQL Database** from hello **Databases** page.</span></span> 

   ![빈 데이터베이스 만들기](../articles/sql-database/media/sql-database-design-first-database/create-empty-database.png)

3. <span data-ttu-id="d1e8b-110">Hello 이미지 앞에 표시 된 대로 hello SQL 데이터베이스에 대 한 양식을 사용 hello 다음 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-110">Fill out hello SQL Database form with hello following information, as shown on hello preceding image:</span></span>   

   | <span data-ttu-id="d1e8b-111">설정</span><span class="sxs-lookup"><span data-stu-id="d1e8b-111">Setting</span></span> | <span data-ttu-id="d1e8b-112">제안 값</span><span class="sxs-lookup"><span data-stu-id="d1e8b-112">Suggested value</span></span> | <span data-ttu-id="d1e8b-113">설명</span><span class="sxs-lookup"><span data-stu-id="d1e8b-113">Description</span></span> |
   | --------| --------------- | ----------- | 
   | <span data-ttu-id="d1e8b-114">**데이터베이스 이름**</span><span class="sxs-lookup"><span data-stu-id="d1e8b-114">**Database name**</span></span> | <span data-ttu-id="d1e8b-115">mySampleDatabase</span><span class="sxs-lookup"><span data-stu-id="d1e8b-115">mySampleDatabase</span></span> | <span data-ttu-id="d1e8b-116">유효한 데이터베이스 이름은 [데이터베이스 식별자](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-116">For valid database names, see [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers).</span></span> | 
   | <span data-ttu-id="d1e8b-117">**구독**</span><span class="sxs-lookup"><span data-stu-id="d1e8b-117">**Subscription**</span></span> | <span data-ttu-id="d1e8b-118">사용자의 구독</span><span class="sxs-lookup"><span data-stu-id="d1e8b-118">Your subscription</span></span>  | <span data-ttu-id="d1e8b-119">구독에 대한 자세한 내용은 [구독](https://account.windowsazure.com/Subscriptions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-119">For details about your subscriptions, see [Subscriptions](https://account.windowsazure.com/Subscriptions).</span></span> |
   | <span data-ttu-id="d1e8b-120">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="d1e8b-120">**Resource group**</span></span> | <span data-ttu-id="d1e8b-121">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d1e8b-121">myResourceGroup</span></span> | <span data-ttu-id="d1e8b-122">유효한 리소스 그룹 이름은 [명명 규칙 및 제한 사항](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-122">For valid resource group names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> |
   | <span data-ttu-id="d1e8b-123">**원본 선택**</span><span class="sxs-lookup"><span data-stu-id="d1e8b-123">**Select source**</span></span> | <span data-ttu-id="d1e8b-124">빈 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d1e8b-124">Blank database</span></span> | <span data-ttu-id="d1e8b-125">빈 데이터베이스를 만들도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-125">Specifies that a blank database should be created.</span></span> |
   ||||

4. <span data-ttu-id="d1e8b-126">클릭 **서버** toocreate 하 고 새 데이터베이스에 대 한 새 서버를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-126">Click **Server** toocreate and configure a new server for your new database.</span></span> <span data-ttu-id="d1e8b-127">Hello 채울 **새 폼 서버** hello 다음 정보로:</span><span class="sxs-lookup"><span data-stu-id="d1e8b-127">Fill out hello **New server form** with hello following information:</span></span> 

   | <span data-ttu-id="d1e8b-128">설정</span><span class="sxs-lookup"><span data-stu-id="d1e8b-128">Setting</span></span> | <span data-ttu-id="d1e8b-129">제안 값</span><span class="sxs-lookup"><span data-stu-id="d1e8b-129">Suggested value</span></span> | <span data-ttu-id="d1e8b-130">설명</span><span class="sxs-lookup"><span data-stu-id="d1e8b-130">Description</span></span> |
   | --------| --------------- | ----------- | 
   | <span data-ttu-id="d1e8b-131">**서버 이름**</span><span class="sxs-lookup"><span data-stu-id="d1e8b-131">**Server name**</span></span> | <span data-ttu-id="d1e8b-132">전역적으로 고유한 이름</span><span class="sxs-lookup"><span data-stu-id="d1e8b-132">Any globally unique name.</span></span> | <span data-ttu-id="d1e8b-133">유효한 서버 이름은 [명명 규칙 및 제한 사항](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-133">For valid server names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> | 
   | <span data-ttu-id="d1e8b-134">**서버 관리자 로그인**</span><span class="sxs-lookup"><span data-stu-id="d1e8b-134">**Server admin login**</span></span> | <span data-ttu-id="d1e8b-135">모든 유효한 이름</span><span class="sxs-lookup"><span data-stu-id="d1e8b-135">Any valid name.</span></span> | <span data-ttu-id="d1e8b-136">유효한 로그인 이름은 [데이터베이스 식별자](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-136">For valid login names, see [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers).</span></span>|
   | <span data-ttu-id="d1e8b-137">**암호**</span><span class="sxs-lookup"><span data-stu-id="d1e8b-137">**Password**</span></span> | <span data-ttu-id="d1e8b-138">유효한 암호</span><span class="sxs-lookup"><span data-stu-id="d1e8b-138">Any valid password.</span></span> | <span data-ttu-id="d1e8b-139">암호가 8 자 이상 있어야 하며 hello 다음 범주 중 세 범주의 문자를 포함 해야 합니다: 대문자, 소문자, 숫자 및 영숫자가 아닌 문자.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-139">Your password must have at least eight characters and must contain characters from three of hello following categories: upper case characters, lower case characters, numbers, and non-alphanumeric characters.</span></span> |
   | <span data-ttu-id="d1e8b-140">**위치**:</span><span class="sxs-lookup"><span data-stu-id="d1e8b-140">**Location**</span></span> | <span data-ttu-id="d1e8b-141">모든 유효한 위치</span><span class="sxs-lookup"><span data-stu-id="d1e8b-141">Any valid location.</span></span> | <span data-ttu-id="d1e8b-142">지역에 대한 자세한 내용은 [Azure 지역](https://azure.microsoft.com/regions/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-142">For information about regions, see [Azure Regions](https://azure.microsoft.com/regions/).</span></span> |
   ||||

   ![create database-server](../articles/sql-database/media/sql-database-design-first-database/create-database-server.png)

5. <span data-ttu-id="d1e8b-144">**선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-144">Click **Select**.</span></span>

6. <span data-ttu-id="d1e8b-145">클릭 **가격 책정 계층** toospecify hello 서비스 계층과 성능 수준을 새 데이터베이스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-145">Click **Pricing tier** toospecify hello service tier and performance level for your new database.</span></span> <span data-ttu-id="d1e8b-146">이 자습서에서는 **20 DTU** 및 **250**GB의 저장소를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-146">For this tutorial, select **20 DTUs** and **250** GB of storage.</span></span>

   ![create database-s1](../articles/sql-database/media/sql-database-design-first-database/create-empty-database-pricing-tier.png)

7. <span data-ttu-id="d1e8b-148">**Apply**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-148">Click **Apply**.</span></span>  

8. <span data-ttu-id="d1e8b-149">선택 된 **데이터 정렬** hello 빈 데이터베이스에 대 한 (이 자습서에서는 hello 기본값 사용).</span><span class="sxs-lookup"><span data-stu-id="d1e8b-149">Select a **collation** for hello blank database (for this tutorial, use hello default value).</span></span> <span data-ttu-id="d1e8b-150">데이터 정렬에 대한 자세한 내용은 [데이터 정렬](https://docs.microsoft.com/sql/t-sql/statements/collations)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-150">For more information about collations, see [Collations](https://docs.microsoft.com/sql/t-sql/statements/collations)</span></span>

9. <span data-ttu-id="d1e8b-151">클릭 **만들기** tooprovision hello 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-151">Click **Create** tooprovision hello database.</span></span> <span data-ttu-id="d1e8b-152">하나 있으며 toocomplete에 대 한 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-152">Provisioning takes about a minute and a half toocomplete.</span></span> 

10. <span data-ttu-id="d1e8b-153">Hello 도구 모음에서 **알림** toomonitor hello 배포 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-153">On hello toolbar, click **Notifications** toomonitor hello deployment process.</span></span>

   ![알림](../articles/sql-database/media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule-using-hello-azure-portal"></a><span data-ttu-id="d1e8b-155">Hello Azure 포털을 사용 하 여 서버 수준 방화벽 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="d1e8b-155">Create a server-level firewall rule using hello Azure portal</span></span>

<span data-ttu-id="d1e8b-156">hello SQL 데이터베이스 서비스는 hello 서버 수준 방화벽을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-156">hello SQL Database service creates a firewall at hello server-level.</span></span> <span data-ttu-id="d1e8b-157">처음 hello 방화벽 외부 도구와 응용 프로그램이 toohello 서버나 tooany hello 서버에 있는 데이터베이스를 연결 하지 못하도록 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-157">Initially hello firewall prevents external tools and applications from connecting toohello server, or tooany databases on hello server.</span></span> <span data-ttu-id="d1e8b-158">방화벽 규칙 tooopen 특정 IP 주소를 만든 후 연결이 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-158">Connections are allowed after a firewall rule is created tooopen specific IP addresses.</span></span> <span data-ttu-id="d1e8b-159">이러한 단계 toocreate에 따라 한 [SQL 데이터베이스 서버 수준 방화벽 규칙](../articles/sql-database/sql-database-firewall-configure.md) 클라이언트의 IP 주소 및 사용자만 IP 주소에 대 한 hello SQL 데이터베이스 방화벽을 통해 tooenable 외부 연결에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-159">Follow these steps toocreate a [SQL Database server-level firewall rule](../articles/sql-database/sql-database-firewall-configure.md) for your client's IP address, and tooenable external connectivity through hello SQL Database firewall for your IP address only.</span></span> 


> [!NOTE]
> <span data-ttu-id="d1e8b-160">Azure SQL Database는 포트 1433을 통해 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-160">Azure SQL Database communicates over port 1433.</span></span> <span data-ttu-id="d1e8b-161">네트워크의 hello 방화벽 포트 1433 통해 아웃 바운드 트래픽을 허용 하는 후에 tooSQL 데이터베이스를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-161">You can connect tooSQL Database only after hello firewall of your network allows outbound traffic through port 1433.</span></span>


1. <span data-ttu-id="d1e8b-162">Hello 배포가 완료 된 후 클릭 **SQL 데이터베이스** hello 왼쪽 메뉴에서 **mySampleDatabase** hello에 **SQL 데이터베이스** 페이지.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-162">After hello deployment completes, click **SQL databases** from hello left-hand menu and then click **mySampleDatabase** on hello **SQL databases** page.</span></span> <span data-ttu-id="d1e8b-163">hello 완벽 하 게 hello 보여 주는 데이터베이스 열리면 프로그램에 대 한 개요 페이지에 정규화 된 서버 이름 (예: **mynewserver20170313.database.windows.net**) 하 고 더 이상의 구성에 대 한 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-163">hello overview page for your database opens, showing you hello fully qualified server name (such as **mynewserver20170313.database.windows.net**) and provides options for further configuration.</span></span> <span data-ttu-id="d1e8b-164">나중에 사용하기 위해 이 정규화된 서버 이름을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-164">Copy this fully qualified server name for use later.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="d1e8b-165">이 정규화 된 서버 이름 tooconnect tooyour 서버와 데이터베이스의 후속 빠른 시작 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-165">You need this fully qualified server name tooconnect tooyour server and its databases in subsequent quick starts.</span></span>
   > 

   ![서버 이름](../articles/sql-database/media/sql-database-get-started-portal/server-name.png) 

2. <span data-ttu-id="d1e8b-167">클릭 **서버 방화벽 설정** hello 이전 그림에 나와 있는 것 처럼 hello 도구 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-167">Click **Set server firewall** on hello toolbar as shown in hello previous image.</span></span> <span data-ttu-id="d1e8b-168">hello **방화벽 설정** hello SQL 데이터베이스 서버에 대 한 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-168">hello **Firewall settings** page for hello SQL Database server opens.</span></span> 

   ![서버 방화벽 규칙](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule.png) 


3. <span data-ttu-id="d1e8b-170">클릭 **클라이언트 IP 추가** hello 도구 모음 tooadd에 현재 IP 주소 tooa 새 방화벽 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-170">Click **Add client IP** on hello toolbar tooadd your current IP address tooa new firewall rule.</span></span> <span data-ttu-id="d1e8b-171">방화벽 규칙은 단일 IP 주소 또는 IP 주소의 범위에 1433 포트를 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-171">A firewall rule can open port 1433 for a single IP address or a range of IP addresses.</span></span>

4. <span data-ttu-id="d1e8b-172">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-172">Click **Save**.</span></span> <span data-ttu-id="d1e8b-173">서버 수준 방화벽 규칙 hello 논리 서버에 포트 1433을 열지 현재 IP 주소에 대해 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-173">A server-level firewall rule is created for your current IP address opening port 1433 on hello logical server.</span></span>

   ![set server firewall rule](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule-set.png) 

4. <span data-ttu-id="d1e8b-175">클릭 **확인** hello 다음 닫고 **방화벽 설정** 페이지.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-175">Click **OK** and then close hello **Firewall settings** page.</span></span>

<span data-ttu-id="d1e8b-176">SQL Server Management Studio (SSMS)와 같은 도구를 사용 하 여 toohello Azure SQL 데이터베이스 서버와 데이터베이스를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-176">You can now connect toohello Azure SQL Database server and its databases by using a tool such as SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="d1e8b-177">이 IP 주소에서 hello 연결 이며 hello 서버 관리자 계정은 이전에 만든를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-177">hello connection is from this IP address, and it uses hello server admin account created previously.</span></span>


> [!IMPORTANT]
> <span data-ttu-id="d1e8b-178">기본적으로 액세스 hello SQL 데이터베이스 방화벽을 통해 모든 Azure 서비스에 대해 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-178">By default, access through hello SQL Database firewall is enabled for all Azure services.</span></span> <span data-ttu-id="d1e8b-179">클릭 **OFF** 모든 Azure 서비스에 대 한이 페이지 toodisable에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-179">Click **OFF** on this page toodisable for all Azure services.</span></span>


## <a name="get-connection-string-values-using-hello-azure-portal"></a><span data-ttu-id="d1e8b-180">Hello Azure 포털을 사용 하 여 연결 문자열 값 가져오기</span><span class="sxs-lookup"><span data-stu-id="d1e8b-180">Get connection string values using hello Azure portal</span></span>

<span data-ttu-id="d1e8b-181">Hello Azure 포털에서에서 Azure SQL 데이터베이스 서버에 대 한 정규화 된 서버 이름을 hello를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-181">Get hello fully qualified server name for your Azure SQL Database server in hello Azure portal.</span></span> <span data-ttu-id="d1e8b-182">SQL Server Management Studio를 사용 하 여 hello 정규화 된 서버 이름 tooconnect tooyour 서버를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-182">You use hello fully qualified server name tooconnect tooyour server using SQL Server Management Studio.</span></span>

1. <span data-ttu-id="d1e8b-183">Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-183">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="d1e8b-184">선택 **SQL 데이터베이스** hello 왼쪽 메뉴에서 hello에 데이터베이스를 클릭 하 고 **SQL 데이터베이스** 페이지.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-184">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 

3. <span data-ttu-id="d1e8b-185">Hello에 **Essentials** hello 프로그램 데이터베이스에 대 한 Azure 포털 페이지의에서 창 찾아 다음 hello 복사 **서버 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1e8b-185">In hello **Essentials** pane in hello Azure portal page for your database, locate and then copy hello **Server name**.</span></span>

   ![연결 정보](../articles/sql-database/media/sql-database-get-started-portal/server-name.png) 
