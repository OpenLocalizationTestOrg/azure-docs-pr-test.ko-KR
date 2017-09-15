### <a name="create-a-new-logical-sql-server-in-the-azure-portal"></a><span data-ttu-id="c8145-101">Azure Portal에서 새 논리 SQL 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="c8145-101">Create a new logical SQL server in the Azure portal</span></span>

1. <span data-ttu-id="c8145-102">**새로 만들기**를 클릭하고 **논리 서버**를 검색한 다음 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="c8145-102">Click **New**, search **logical server**, and then hit **ENTER**.</span></span>

    ![논리 서버 검색](./media/sql-data-warehouse-create-logical-server/search-logical-server.png)
2. <span data-ttu-id="c8145-104">**SQL 서버(논리 서버)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c8145-104">Select **SQL server (logical server)**</span></span> 

    ![논리 서버 선택](./media/sql-data-warehouse-create-logical-server/select-logical-server.png)
  
3. <span data-ttu-id="c8145-106">**만들기**를 클릭하여 새 SQL Server(논리 서버) 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c8145-106">Click **Create** to open the new SQL Server (logical server) blade.</span></span>

   <span data-ttu-id="c8145-107"><kbd>![논리 서버 블레이드를 여세요](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd> ![논리 서버 블레이드](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png)</kbd></span><span class="sxs-lookup"><span data-stu-id="c8145-107"><kbd> ![open logical server blade](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd>![logical server blade](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png) </kbd></span></span>
  
3. <span data-ttu-id="c8145-108">[SQL Server(논리 서버)] 블레이드의 서버 이름 텍스트 상자에서 새 논리 서버의 유효한 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c8145-108">In the SQL Server (logical server) blade's server name text box, provide a valid name for the new logical server.</span></span> <span data-ttu-id="c8145-109">녹색 확인 표시가 유효한 이름을 제공한 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c8145-109">A green check mark indicates that you have provided a valid name.</span></span>
    
    ![새 서버 이름](./media/sql-data-warehouse-create-logical-server/new-name-logical-server.png)

    > [!IMPORTANT]
    > <span data-ttu-id="c8145-111">새 서버의 정규화된 이름은 <your_server_name>.database.windows.net입니다.</span><span class="sxs-lookup"><span data-stu-id="c8145-111">The fully qualified name for your new server will be <your_server_name>.database.windows.net.</span></span>
    >
    
4. <span data-ttu-id="c8145-112">[서버 관리자 로그인] 텍스트 상자에서 이 서버의 SQL 인증 로그인을 위한 사용자 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c8145-112">In the Server admin login text box, provide a user name for the SQL authentication login for this server.</span></span> <span data-ttu-id="c8145-113">이 로그인은 서버 보안 주체 로그인으로 알려져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8145-113">This login is known as the server principal login.</span></span> <span data-ttu-id="c8145-114">녹색 확인 표시가 유효한 이름을 제공한 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c8145-114">A green check mark indicates that you have provided a valid name.</span></span>
    
    ![SQL 관리자 로그인](./media/sql-data-warehouse-create-logical-server/sql-admin-login.png)
5. <span data-ttu-id="c8145-116">**암호** 및 **암호 확인** 텍스트 상자에서 서버 보안 주체 로그인 계정에 대한 암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c8145-116">In the **Password** and **Confirm password** text boxes, provide a password for the server principal login account.</span></span> <span data-ttu-id="c8145-117">녹색 확인 표시가 유효한 암호를 제공한 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c8145-117">A green check mark indicates that you have provided a valid password.</span></span>
    
    ![SQL 관리자 암호](./media/sql-data-warehouse-create-logical-server/sql-admin-password.png)
6. <span data-ttu-id="c8145-119">개체를 만들 수 있는 권한이 있는 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c8145-119">Select a subscription in which you have permission to create objects.</span></span>

    ![subscription](./media/sql-data-warehouse-create-logical-server/subscription.png)
7. <span data-ttu-id="c8145-121">[리소스 그룹] 텍스트 상자에서 **새로 만들기**를 선택한 다음 [리소스 그룹] 텍스트 상자에서 새 리소스 그룹의 유효한 이름을 제공합니다. 이미 사용자 자신의 리소스 그룹을 만든 경우 기존 리소스 그룹을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8145-121">In the Resource group text box, select **Create new** and then, in the resource group text box, provide a valid name for the new resource group (you can also use an existing resource group if you have already created one for yourself).</span></span> <span data-ttu-id="c8145-122">녹색 확인 표시가 유효한 이름을 제공한 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c8145-122">A green check mark indicates that you have provided a valid name.</span></span>

    ![새 리소스 그룹](./media/sql-data-warehouse-create-logical-server/new-resource-group.png)

8. <span data-ttu-id="c8145-124">**위치** 텍스트 상자에서 위치에 적합한 데이터 센터(예: "오스트레일리아 동부")를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c8145-124">In the **Location** text box, select a data center appropriate to your location - such as "Australia East".</span></span>
    
    ![서버 위치](./media/sql-data-warehouse-create-logical-server/server-location.png)
    
    > [!TIP]
    > <span data-ttu-id="c8145-126">**Azure 서비스의 서버 액세스 허용** 확인란은 이 블레이드에서 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c8145-126">The checkbox for **Allow azure services to access server** cannot be changed on this blade.</span></span> <span data-ttu-id="c8145-127">[서버 방화벽] 블레이드에서 이 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8145-127">You can change this setting on the server firewall blade.</span></span> <span data-ttu-id="c8145-128">자세한 내용은 [보안 시작](../articles/sql-database/sql-database-manage-servers-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8145-128">For more information, see [Get started with security](../articles/sql-database/sql-database-manage-servers-portal.md).</span></span>
    >
    
9. <span data-ttu-id="c8145-129">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c8145-129">Click **Create**.</span></span>

    ![만들기 단추](./media/sql-data-warehouse-create-logical-server/create.png)

