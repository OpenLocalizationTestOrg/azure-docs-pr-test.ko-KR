### <a name="open-tcp-ports-in-hello-windows-firewall-for-hello-default-instance-of-hello-database-engine"></a><span data-ttu-id="aa543-101">Hello 데이터베이스 엔진의 기본 인스턴스 hello에 대 한 hello Windows 방화벽에서 TCP 포트를 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-101">Open TCP ports in hello Windows firewall for hello default instance of hello Database Engine</span></span>
1. <span data-ttu-id="aa543-102">원격 데스크톱으로 toohello 가상 컴퓨터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-102">Connect toohello virtual machine with Remote Desktop.</span></span> <span data-ttu-id="aa543-103">Toohello VM 연결 방법에 대 한 자세한 내용은 참조 하십시오. [SQL VM 원격 데스크톱으로 열고](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md#open-the-vm-with-remote-desktop)합니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-103">For detailed instructions on connecting toohello VM, see [Open a SQL VM with Remote Desktop](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md#open-the-vm-with-remote-desktop).</span></span>
2. <span data-ttu-id="aa543-104">Hello 시작 화면에서 로그인 되 면 입력 **WF.msc**, 한 다음 ENTER 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-104">Once logged in, at hello Start screen, type **WF.msc**, and then hit ENTER.</span></span>
   
    ![Hello 방화벽 프로그램을 시작 합니다.](./media/virtual-machines-sql-server-connection-steps/12Open-WF.png)
3. <span data-ttu-id="aa543-106">Hello에 **고급 보안이 포함 된 Windows 방화벽**hello 왼쪽된 창에서 마우스 오른쪽 단추로 클릭 **인바운드 규칙**, 클릭 하 고 **새 규칙** hello 작업 창에서.</span><span class="sxs-lookup"><span data-stu-id="aa543-106">In hello **Windows Firewall with Advanced Security**, in hello left pane, right-click **Inbound Rules**, and then click **New Rule** in hello action pane.</span></span>
   
    ![새 규칙](./media/virtual-machines-sql-server-connection-steps/13New-FW-Rule.png)
4. <span data-ttu-id="aa543-108">Hello에 **새 인바운드 규칙 마법사** 대화 상자의 **규칙 유형**선택, **포트**, 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-108">In hello **New Inbound Rule Wizard** dialog box, under **Rule Type**, select **Port**, and then click **Next**.</span></span>
5. <span data-ttu-id="aa543-109">Hello에 **프로토콜 및 포트** 대화 상자에서 사용 하 여 hello 기본 **TCP**합니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-109">In hello **Protocol and Ports** dialog, use hello default **TCP**.</span></span> <span data-ttu-id="aa543-110">Hello에 **특정 로컬 포트** 상자 다음 형식 hello에 대 한 포트 번호의 hello hello 데이터베이스 엔진 인스턴스의 (**1433** hello 기본 인스턴스 또는 hello hello 끝점 단계에서 개인 포트에 대해 선택한 사항에 대 한).</span><span class="sxs-lookup"><span data-stu-id="aa543-110">In hello **Specific local ports** box, then type hello port number of hello instance of hello Database Engine (**1433** for hello default instance or your choice for hello private port in hello endpoint step).</span></span>
   
    ![TCP 포트 1433](./media/virtual-machines-sql-server-connection-steps/14Port-1433.png)
6. <span data-ttu-id="aa543-112">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-112">Click **Next**.</span></span>
7. <span data-ttu-id="aa543-113">Hello에 **동작** 대화 상자에서 **hello 연결 허용**, 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-113">In hello **Action** dialog box, select **Allow hello connection**, and then click **Next**.</span></span>
   
    <span data-ttu-id="aa543-114">**보안 정보:** Selecting **보안 hello 연결을 허용** 추가 보안을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-114">**Security Note:** Selecting **Allow hello connection if it is secure** can provide additional security.</span></span> <span data-ttu-id="aa543-115">사용자 환경에서 tooconfigure 추가 보안 옵션을 원하는 경우이 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-115">Select this option if you want tooconfigure additional security options in your environment.</span></span>
   
    ![연결 허용](./media/virtual-machines-sql-server-connection-steps/15Allow-Connection.png)
8. <span data-ttu-id="aa543-117">Hello에 **프로필** 대화 상자에서 **공용**, **개인**, 및 **도메인**합니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-117">In hello **Profile** dialog box, select **Public**, **Private**, and **Domain**.</span></span> <span data-ttu-id="aa543-118">그런 후 **Next**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-118">Then click **Next**.</span></span>
   
    <span data-ttu-id="aa543-119">**보안 정보:** Selecting **공용** 를 통해 액세스할 수 있도록 인터넷 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-119">**Security Note:**  Selecting **Public** allows access over hello internet.</span></span> <span data-ttu-id="aa543-120">가능하면 더 제한적인 프로필을 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="aa543-120">Whenever possible, select a more restrictive profile.</span></span>
   
    ![공개 프로필](./media/virtual-machines-sql-server-connection-steps/16Public-Private-Domain-Profile.png)
9. <span data-ttu-id="aa543-122">Hello에 **이름** 대화 상자에서 이름 및이 규칙에 대 한 설명을 입력 하 고 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-122">In hello **Name** dialog box, type a name and description for this rule, and then click **Finish**.</span></span>
   
    ![규칙 이름](./media/virtual-machines-sql-server-connection-steps/17Rule-Name.png)

<span data-ttu-id="aa543-124">필요한 경우 다른 구성 요소의 추가 포트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-124">Open additional ports for other components as needed.</span></span> <span data-ttu-id="aa543-125">자세한 내용은 참조 [hello Windows 방화벽 tooAllow SQL Server 액세스를 구성](http://msdn.microsoft.com/library/cc646023.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-125">For more information, see [Configuring hello Windows Firewall tooAllow SQL Server Access](http://msdn.microsoft.com/library/cc646023.aspx).</span></span>

### <a name="configure-sql-server-toolisten-on-hello-tcp-protocol"></a><span data-ttu-id="aa543-126">SQL Server toolisten hello TCP 프로토콜에서 구성</span><span class="sxs-lookup"><span data-stu-id="aa543-126">Configure SQL Server toolisten on hello TCP protocol</span></span>

[!INCLUDE [Enable TCP](virtual-machines-sql-server-connection-tcp-protocol.md)]

### <a name="configure-sql-server-for-mixed-mode-authentication"></a><span data-ttu-id="aa543-127">혼합 모드 인증을 위해 SQL Server 구성</span><span class="sxs-lookup"><span data-stu-id="aa543-127">Configure SQL Server for mixed mode authentication</span></span>
<span data-ttu-id="aa543-128">SQL Server 데이터베이스 엔진 hello 도메인 환경이 없는 Windows 인증을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-128">hello SQL Server Database Engine cannot use Windows Authentication without domain environment.</span></span> <span data-ttu-id="aa543-129">다른 컴퓨터에서 데이터베이스 엔진 tooconnect toohello 혼합된 모드 인증에 대 한 SQL Server를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-129">tooconnect toohello Database Engine from another computer, configure SQL Server for mixed mode authentication.</span></span> <span data-ttu-id="aa543-130">혼합 모드 인증은 SQL Server 인증과 Windows 인증을 모두 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-130">Mixed mode authentication allows both SQL Server Authentication and Windows Authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="aa543-131">Azure 가상 네트워크를, 구성된 도메인 환경으로 구성한 경우, 혼합 모드 인증은 구성할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-131">Configuring mixed mode authentication might not be necessary if you have configured an Azure Virtual Network with a configured domain environment.</span></span>
> 
> 

1. <span data-ttu-id="aa543-132">Hello 시작 페이지에서 가상 컴퓨터를 연결 된 toohello 하는 동안 입력 **SQL Server Management Studio** hello 선택한 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-132">While connected toohello virtual machine, on hello Start page, type **SQL Server Management Studio** and click hello selected icon.</span></span>
   
    <span data-ttu-id="aa543-133">처음으로 Management Studio hello 사용자가 Management Studio 환경을 만들어야 열 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-133">hello first time you open Management Studio it must create hello users Management Studio environment.</span></span> <span data-ttu-id="aa543-134">어느 정도 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-134">This may take a few moments.</span></span>
2. <span data-ttu-id="aa543-135">Management Studio 제공 hello **tooServer 연결** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="aa543-135">Management Studio presents hello **Connect tooServer** dialog box.</span></span> <span data-ttu-id="aa543-136">Hello에 **서버 이름** 상자 hello 개체 탐색기로 hello 가상 컴퓨터 tooconnect toohello 데이터베이스 엔진의 hello 이름을 입력 합니다 (사용할 수 있습니다 hello 가상 컴퓨터 이름 대신 **(local)** 또는 단일 기간의 hello로 **서버 이름**).</span><span class="sxs-lookup"><span data-stu-id="aa543-136">In hello **Server name** box, type hello name of hello virtual machine tooconnect toohello Database Engine  with hello Object Explorer (Instead of hello virtual machine name you can also use **(local)** or a single period as hello **Server name**).</span></span> <span data-ttu-id="aa543-137">선택 **Windows 인증**, 둡니다  ***your_VM_name*\your_local_administrator** hello에 **사용자 이름** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-137">Select **Windows Authentication**, and leave ***your_VM_name*\your_local_administrator** in hello **User name** box.</span></span> <span data-ttu-id="aa543-138">**Connect**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-138">Click **Connect**.</span></span>
   
    ![TooServer 연결](./media/virtual-machines-sql-server-connection-steps/19Connect-to-Server.png)
3. <span data-ttu-id="aa543-140">SQL Server Management Studio 개체 탐색기에서 hello (hello 가상 컴퓨터 이름), SQL Server의 hello 인스턴스 이름을 마우스 오른쪽 단추로 클릭 하 고 클릭 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-140">In SQL Server Management Studio Object Explorer, right-click hello name of hello instance of SQL Server (hello virtual machine name), and then click **Properties**.</span></span>
   
    ![서버 속성](./media/virtual-machines-sql-server-connection-steps/20Server-Properties.png)
4. <span data-ttu-id="aa543-142">Hello에 **보안** 페이지의 **서버 인증**선택, **SQL Server 및 Windows 인증 모드**, 클릭 하 고 **확인** .</span><span class="sxs-lookup"><span data-stu-id="aa543-142">On hello **Security** page, under **Server authentication**, select **SQL Server and Windows Authentication mode**, and then click **OK**.</span></span>
   
    ![인증 모드 선택](./media/virtual-machines-sql-server-connection-steps/21Mixed-Mode.png)
5. <span data-ttu-id="aa543-144">Hello SQL Server Management Studio 대화 상자에서 클릭 **확인** tooacknowledge hello 요구 사항 toorestart SQL Server.</span><span class="sxs-lookup"><span data-stu-id="aa543-144">In hello SQL Server Management Studio dialog box, click **OK** tooacknowledge hello requirement toorestart SQL Server.</span></span>
6. <span data-ttu-id="aa543-145">개체 탐색기에서 서버를 마우스 오른쪽 단추로 클릭한 후 **다시 시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-145">In Object Explorer, right-click your server, and then click **Restart**.</span></span> <span data-ttu-id="aa543-146">SQL Server 에이전트가 실행 중인 경우 에이전트도 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-146">(If SQL Server Agent is running, it must also be restarted.)</span></span>
   
    ![다시 시작](./media/virtual-machines-sql-server-connection-steps/22Restart2.png)
7. <span data-ttu-id="aa543-148">Hello SQL Server Management Studio 대화 상자에서 클릭 **예** tooagree toorestart SQL Server 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-148">In hello SQL Server Management Studio dialog box, click **Yes** tooagree that you want toorestart SQL Server.</span></span>

### <a name="create-sql-server-authentication-logins"></a><span data-ttu-id="aa543-149">SQL Server 인증 로그인 만들기</span><span class="sxs-lookup"><span data-stu-id="aa543-149">Create SQL Server authentication logins</span></span>
<span data-ttu-id="aa543-150">다른 컴퓨터에서 tooconnect toohello 데이터베이스 엔진, SQL Server 인증 로그인을 하나 이상 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-150">tooconnect toohello Database Engine from another computer, you must create at least one SQL Server authentication login.</span></span>

1. <span data-ttu-id="aa543-151">SQL Server Management Studio 개체 탐색기에서 toocreate hello에 대 한 새 로그인 원하는 hello 서버 인스턴스의 hello 폴더를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-151">In SQL Server Management Studio Object Explorer, expand hello folder of hello server instance in which you want toocreate hello new login.</span></span>
2. <span data-ttu-id="aa543-152">마우스 오른쪽 단추로 클릭 hello **보안** 폴더를 너무 가리킨**새로**, 선택한 **로그인...** .</span><span class="sxs-lookup"><span data-stu-id="aa543-152">Right-click hello **Security** folder, point too**New**, and select **Login...**.</span></span>
   
    ![새 로그인](./media/virtual-machines-sql-server-connection-steps/23New-Login.png)
3. <span data-ttu-id="aa543-154">Hello에 **로그인-신규** 대화 상자의 hello **일반** 페이지에서 hello에 hello 새 사용자의 hello 이름을 입력 **로그인 이름** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-154">In hello **Login - New** dialog box, on hello **General** page, enter hello name of hello new user in hello **Login name** box.</span></span>
4. <span data-ttu-id="aa543-155">**SQL Server 인증**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-155">Select **SQL Server authentication**.</span></span>
5. <span data-ttu-id="aa543-156">Hello에 **암호** 상자에 새 사용자 hello에 대 한 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-156">In hello **Password** box, enter a password for hello new user.</span></span> <span data-ttu-id="aa543-157">Hello에 해당 암호를 다시 입력 **암호 확인** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-157">Enter that password again into hello **Confirm Password** box.</span></span>
6. <span data-ttu-id="aa543-158">필요한 hello 암호 적용 옵션을 선택 (**암호 정책 강제 적용**, **암호 만료 강제 적용**, 및 **사용자는 다음 로그인 시 암호를 변경 해야**).</span><span class="sxs-lookup"><span data-stu-id="aa543-158">Select hello password enforcement options required (**Enforce password policy**, **Enforce password expiration**, and **User must change password at next login**).</span></span> <span data-ttu-id="aa543-159">이 로그인을 직접 사용 하는 경우에 hello 다음 로그인 시 암호 변경 toorequire를 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-159">If you are using this login for yourself, you do not need toorequire a password change at hello next login.</span></span>
7. <span data-ttu-id="aa543-160">Hello에서 **기본 데이터베이스** 목록 hello 로그인에 대 한 기본 데이터베이스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-160">From hello **Default database** list, select a default database for hello login.</span></span> <span data-ttu-id="aa543-161">**마스터** 이 옵션에 대 한 hello 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-161">**master** is hello default for this option.</span></span> <span data-ttu-id="aa543-162">사용자 데이터베이스를 아직 만들지 않은 경우에이 둡니다**마스터**합니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-162">If you have not yet created a user database, leave this set too**master**.</span></span>
   
    ![로그인 속성](./media/virtual-machines-sql-server-connection-steps/24Test-Login.png)
8. <span data-ttu-id="aa543-164">Hello 처음 로그인을 만들려는 경우 수도 있습니다 toodesignate이 로그인이 SQL Server 관리자 역할.</span><span class="sxs-lookup"><span data-stu-id="aa543-164">If this is hello first login you are creating, you may want toodesignate this login as a SQL Server administrator.</span></span> <span data-ttu-id="aa543-165">Hello에 그렇다면 **서버 역할** 페이지 **sysadmin**합니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-165">If so, on hello **Server Roles** page, check **sysadmin**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="aa543-166">Hello sysadmin 고정 서버 역할의 멤버가 데이터베이스 엔진 hello를 완전히 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-166">Members of hello sysadmin fixed server role have complete control of hello Database Engine.</span></span> <span data-ttu-id="aa543-167">따라서 이 역할의 구성원은 신중하게 제한해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-167">You should carefully restrict membership in this role.</span></span>
   > 
   > 
   
   ![sysadmin](./media/virtual-machines-sql-server-connection-steps/25sysadmin.png)
9. <span data-ttu-id="aa543-169">확인을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aa543-169">Click OK.</span></span>

<span data-ttu-id="aa543-170">SQL Server 로그인에 대한 자세한 내용은 [로그인 만들기](http://msdn.microsoft.com/library/aa337562.aspx)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="aa543-170">For more information about SQL Server logins, see [Create a Login](http://msdn.microsoft.com/library/aa337562.aspx).</span></span>

