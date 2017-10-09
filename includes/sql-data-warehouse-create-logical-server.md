### <a name="create-a-new-logical-sql-server-in-hello-azure-portal"></a><span data-ttu-id="7165a-101">Hello Azure 포털에서에서 새 논리 SQL server 만들기</span><span class="sxs-lookup"><span data-stu-id="7165a-101">Create a new logical SQL server in hello Azure portal</span></span>

1. <span data-ttu-id="7165a-102">**새로 만들기**를 클릭하고 **논리 서버**를 검색한 다음 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="7165a-102">Click **New**, search **logical server**, and then hit **ENTER**.</span></span>

    ![논리 서버 검색](./media/sql-data-warehouse-create-logical-server/search-logical-server.png)
2. <span data-ttu-id="7165a-104">**SQL 서버(논리 서버)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7165a-104">Select **SQL server (logical server)**</span></span> 

    ![논리 서버 선택](./media/sql-data-warehouse-create-logical-server/select-logical-server.png)
  
3. <span data-ttu-id="7165a-106">클릭 **만들기** tooopen hello 새 SQL Server (논리 서버) 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="7165a-106">Click **Create** tooopen hello new SQL Server (logical server) blade.</span></span>

   <span data-ttu-id="7165a-107"><kbd>![논리 서버 블레이드를 여세요](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd> ![논리 서버 블레이드](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png)</kbd></span><span class="sxs-lookup"><span data-stu-id="7165a-107"><kbd> ![open logical server blade](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd>![logical server blade](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png) </kbd></span></span>
  
3. <span data-ttu-id="7165a-108">Hello SQL Server (논리 서버) 블레이드에서 서버 이름 텍스트 상자에 새 논리 서버 hello에 대 한 올바른 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7165a-108">In hello SQL Server (logical server) blade's server name text box, provide a valid name for hello new logical server.</span></span> <span data-ttu-id="7165a-109">녹색 확인 표시가 유효한 이름을 제공한 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7165a-109">A green check mark indicates that you have provided a valid name.</span></span>
    
    ![새 서버 이름](./media/sql-data-warehouse-create-logical-server/new-name-logical-server.png)

    > [!IMPORTANT]
    > <span data-ttu-id="7165a-111">hello 새 서버의 정규화 된 이름이 됩니다 < your_server_name >. database.windows.net 합니다.</span><span class="sxs-lookup"><span data-stu-id="7165a-111">hello fully qualified name for your new server will be <your_server_name>.database.windows.net.</span></span>
    >
    
4. <span data-ttu-id="7165a-112">Hello 서버 관리자 로그인 텍스트 상자에이 서버에 대 한 hello SQL 인증 로그인에 대 한 사용자 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7165a-112">In hello Server admin login text box, provide a user name for hello SQL authentication login for this server.</span></span> <span data-ttu-id="7165a-113">이 로그인을 서버 보안 주체 로그인 hello 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7165a-113">This login is known as hello server principal login.</span></span> <span data-ttu-id="7165a-114">녹색 확인 표시가 유효한 이름을 제공한 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7165a-114">A green check mark indicates that you have provided a valid name.</span></span>
    
    ![SQL 관리자 로그인](./media/sql-data-warehouse-create-logical-server/sql-admin-login.png)
5. <span data-ttu-id="7165a-116">Hello에 **암호** 및 **암호 확인** 텍스트 상자 hello 서버 보안 주체 로그인 계정의 암호를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7165a-116">In hello **Password** and **Confirm password** text boxes, provide a password for hello server principal login account.</span></span> <span data-ttu-id="7165a-117">녹색 확인 표시가 유효한 암호를 제공한 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7165a-117">A green check mark indicates that you have provided a valid password.</span></span>
    
    ![SQL 관리자 암호](./media/sql-data-warehouse-create-logical-server/sql-admin-password.png)
6. <span data-ttu-id="7165a-119">사용 권한 toocreate 개체에 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7165a-119">Select a subscription in which you have permission toocreate objects.</span></span>

    ![subscription](./media/sql-data-warehouse-create-logical-server/subscription.png)
7. <span data-ttu-id="7165a-121">Hello 리소스 그룹 텍스트 상자에서 선택 **새로 만들기** 다음 hello 리소스 그룹 텍스트 상자에 hello (있습니다 에서도 사용할 수 있는 기존 리소스 그룹 이미 만든 경우 자신에 대 한 하나)는 새 리소스 그룹에 대 한 올바른 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7165a-121">In hello Resource group text box, select **Create new** and then, in hello resource group text box, provide a valid name for hello new resource group (you can also use an existing resource group if you have already created one for yourself).</span></span> <span data-ttu-id="7165a-122">녹색 확인 표시가 유효한 이름을 제공한 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7165a-122">A green check mark indicates that you have provided a valid name.</span></span>

    ![새 리소스 그룹](./media/sql-data-warehouse-create-logical-server/new-resource-group.png)

8. <span data-ttu-id="7165a-124">Hello에 **위치** 텍스트 상자를 선택한 데이터 센터 "오스트레일리아 동부"와 같은 적절 한 tooyour 위치-합니다.</span><span class="sxs-lookup"><span data-stu-id="7165a-124">In hello **Location** text box, select a data center appropriate tooyour location - such as "Australia East".</span></span>
    
    ![서버 위치](./media/sql-data-warehouse-create-logical-server/server-location.png)
    
    > [!TIP]
    > <span data-ttu-id="7165a-126">에 대 한 확인란 hello **허용 azure 서비스 tooaccess 서버** 이 블레이드를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7165a-126">hello checkbox for **Allow azure services tooaccess server** cannot be changed on this blade.</span></span> <span data-ttu-id="7165a-127">Hello 서버 방화벽 블레이드에서이 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7165a-127">You can change this setting on hello server firewall blade.</span></span> <span data-ttu-id="7165a-128">자세한 내용은 [보안 시작](../articles/sql-database/sql-database-manage-servers-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7165a-128">For more information, see [Get started with security](../articles/sql-database/sql-database-manage-servers-portal.md).</span></span>
    >
    
9. <span data-ttu-id="7165a-129">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7165a-129">Click **Create**.</span></span>

    ![만들기 단추](./media/sql-data-warehouse-create-logical-server/create.png)

