### <a name="open-tcp-ports-in-the-windows-firewall-for-the-default-instance-of-the-database-engine"></a><span data-ttu-id="5cf31-101">Windows 방화벽에서 데이터베이스 엔진의 기본 인스턴스용 TCP 포트 열기</span><span class="sxs-lookup"><span data-stu-id="5cf31-101">Open TCP ports in the Windows firewall for the default instance of the Database Engine</span></span>
1. <span data-ttu-id="5cf31-102">원격 데스크톱을 사용하여 가상 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-102">Connect to the virtual machine with Remote Desktop.</span></span> <span data-ttu-id="5cf31-103">VM에 연결하는 방법에 대한 자세한 내용은 [원격 데스크톱으로 SQL VM 열기](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md#open-the-vm-with-remote-desktop)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5cf31-103">For detailed instructions on connecting to the VM, see [Open a SQL VM with Remote Desktop](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md#open-the-vm-with-remote-desktop).</span></span>
2. <span data-ttu-id="5cf31-104">시작 화면에서 로그인한 후 **WF.msc**를 입력하고 ENTER를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-104">Once logged in, at the Start screen, type **WF.msc**, and then hit ENTER.</span></span>
   
    ![방화벽 프로그램 시작](./media/virtual-machines-sql-server-connection-steps/12Open-WF.png)
3. <span data-ttu-id="5cf31-106">**고급 보안이 포함된 Windows 방화벽**의 왼쪽 창에 있는 작업 창에서 **인바운드 규칙**을 마우스 오른쪽 단추로 클릭한 후 **새 규칙**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-106">In the **Windows Firewall with Advanced Security**, in the left pane, right-click **Inbound Rules**, and then click **New Rule** in the action pane.</span></span>
   
    ![새 규칙](./media/virtual-machines-sql-server-connection-steps/13New-FW-Rule.png)
4. <span data-ttu-id="5cf31-108">**새 인바운드 규칙 마법사** 대화 상자의 **규칙 유형**에서 **포트**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-108">In the **New Inbound Rule Wizard** dialog box, under **Rule Type**, select **Port**, and then click **Next**.</span></span>
5. <span data-ttu-id="5cf31-109">**프로토콜 및 포트** 대화 상자에서 기본 **TCP**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-109">In the **Protocol and Ports** dialog, use the default **TCP**.</span></span> <span data-ttu-id="5cf31-110">**특정 로컬 포트** 상자에 데이터베이스 엔진의 인스턴스 포트 번호(기본 인스턴스의 경우 **1433** 또는 끝점 단계에서 개인 포트에 대해 선택한 포트)를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-110">In the **Specific local ports** box, then type the port number of the instance of the Database Engine (**1433** for the default instance or your choice for the private port in the endpoint step).</span></span>
   
    ![TCP 포트 1433](./media/virtual-machines-sql-server-connection-steps/14Port-1433.png)
6. <span data-ttu-id="5cf31-112">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-112">Click **Next**.</span></span>
7. <span data-ttu-id="5cf31-113">**작업** 대화 상자에서 **연결 허용**을 선택한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-113">In the **Action** dialog box, select **Allow the connection**, and then click **Next**.</span></span>
   
    <span data-ttu-id="5cf31-114">**보안 정보:** **안전한 경우 연결 허용**을 선택하면 추가 보안을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-114">**Security Note:** Selecting **Allow the connection if it is secure** can provide additional security.</span></span> <span data-ttu-id="5cf31-115">사용자 환경에서 추가 보안을 구성하려는 경우 이 옵션을 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="5cf31-115">Select this option if you want to configure additional security options in your environment.</span></span>
   
    ![연결 허용](./media/virtual-machines-sql-server-connection-steps/15Allow-Connection.png)
8. <span data-ttu-id="5cf31-117">**프로필** 대화 상자에서 **공용**, **개인** 및 **도메인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-117">In the **Profile** dialog box, select **Public**, **Private**, and **Domain**.</span></span> <span data-ttu-id="5cf31-118">그런 후 **Next** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-118">Then click **Next**.</span></span>
   
    <span data-ttu-id="5cf31-119">**보안 정보:** **공개**를 선택하면 인터넷을 통한 액세스가 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-119">**Security Note:**  Selecting **Public** allows access over the internet.</span></span> <span data-ttu-id="5cf31-120">가능하면 더 제한적인 프로필을 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="5cf31-120">Whenever possible, select a more restrictive profile.</span></span>
   
    ![공개 프로필](./media/virtual-machines-sql-server-connection-steps/16Public-Private-Domain-Profile.png)
9. <span data-ttu-id="5cf31-122">**이름** 대화 상자에서 이 규칙의 이름 및 설명을 입력한 후 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-122">In the **Name** dialog box, type a name and description for this rule, and then click **Finish**.</span></span>
   
    ![규칙 이름](./media/virtual-machines-sql-server-connection-steps/17Rule-Name.png)

<span data-ttu-id="5cf31-124">필요한 경우 다른 구성 요소의 추가 포트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-124">Open additional ports for other components as needed.</span></span> <span data-ttu-id="5cf31-125">자세한 내용은 [SQL Server 액세스를 허용하도록 Windows 방화벽 구성](http://msdn.microsoft.com/library/cc646023.aspx)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="5cf31-125">For more information, see [Configuring the Windows Firewall to Allow SQL Server Access](http://msdn.microsoft.com/library/cc646023.aspx).</span></span>

### <a name="configure-sql-server-to-listen-on-the-tcp-protocol"></a><span data-ttu-id="5cf31-126">TCP 프로토콜을 수신 대기하도록 SQL Server 구성</span><span class="sxs-lookup"><span data-stu-id="5cf31-126">Configure SQL Server to listen on the TCP protocol</span></span>

[!INCLUDE [Enable TCP](virtual-machines-sql-server-connection-tcp-protocol.md)]

### <a name="configure-sql-server-for-mixed-mode-authentication"></a><span data-ttu-id="5cf31-127">혼합 모드 인증을 위해 SQL Server 구성</span><span class="sxs-lookup"><span data-stu-id="5cf31-127">Configure SQL Server for mixed mode authentication</span></span>
<span data-ttu-id="5cf31-128">SQL Server 데이터베이스 엔진은 도메인 환경에서만 Windows 인증을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-128">The SQL Server Database Engine cannot use Windows Authentication without domain environment.</span></span> <span data-ttu-id="5cf31-129">다른 컴퓨터에서 데이터베이스 엔진에 연결하려면 혼합 모드 인증을 위해 SQL Server를 구성하십시오.</span><span class="sxs-lookup"><span data-stu-id="5cf31-129">To connect to the Database Engine from another computer, configure SQL Server for mixed mode authentication.</span></span> <span data-ttu-id="5cf31-130">혼합 모드 인증은 SQL Server 인증과 Windows 인증을 모두 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-130">Mixed mode authentication allows both SQL Server Authentication and Windows Authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="5cf31-131">Azure 가상 네트워크를, 구성된 도메인 환경으로 구성한 경우, 혼합 모드 인증은 구성할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-131">Configuring mixed mode authentication might not be necessary if you have configured an Azure Virtual Network with a configured domain environment.</span></span>
> 
> 

1. <span data-ttu-id="5cf31-132">가상 컴퓨터에 연결되어 있는 동안 시작 페이지에서 **SQL Server Management Studio** 를 입력하고 선택한 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-132">While connected to the virtual machine, on the Start page, type **SQL Server Management Studio** and click the selected icon.</span></span>
   
    <span data-ttu-id="5cf31-133">처음으로 Management Studio를 열 때 사용자 Management Studio 환경이 만들어져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-133">The first time you open Management Studio it must create the users Management Studio environment.</span></span> <span data-ttu-id="5cf31-134">어느 정도 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-134">This may take a few moments.</span></span>
2. <span data-ttu-id="5cf31-135">Management Studio에서 **서버에 연결** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-135">Management Studio presents the **Connect to Server** dialog box.</span></span> <span data-ttu-id="5cf31-136">**서버 이름** 상자에 개체 탐색기를 사용하여 데이터베이스 엔진에 연결할 가상 컴퓨터의 이름을 입력합니다(가상 컴퓨터 이름 대신 **(로컬)** 또는 점(.)을 **서버 이름**으로 사용할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="5cf31-136">In the **Server name** box, type the name of the virtual machine to connect to the Database Engine  with the Object Explorer (Instead of the virtual machine name you can also use **(local)** or a single period as the **Server name**).</span></span> <span data-ttu-id="5cf31-137">**Windows 인증**을 선택하고, **사용자 이름** 상자의 ***VM_이름*\로컬_관리자**를 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-137">Select **Windows Authentication**, and leave ***your_VM_name*\your_local_administrator** in the **User name** box.</span></span> <span data-ttu-id="5cf31-138">**Connect** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-138">Click **Connect**.</span></span>
   
    ![서버에 연결](./media/virtual-machines-sql-server-connection-steps/19Connect-to-Server.png)
3. <span data-ttu-id="5cf31-140">SQL Server Management Studio 개체 탐색기에서 SQL Server 인스턴스의 이름(가상 컴퓨터 이름)을 마우스 오른쪽 단추로 클릭한 후 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-140">In SQL Server Management Studio Object Explorer, right-click the name of the instance of SQL Server (the virtual machine name), and then click **Properties**.</span></span>
   
    ![서버 속성](./media/virtual-machines-sql-server-connection-steps/20Server-Properties.png)
4. <span data-ttu-id="5cf31-142">**보안** 페이지의 **서버 인증**에서 **SQL Server 및 Windows 인증 모드**를 선택한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-142">On the **Security** page, under **Server authentication**, select **SQL Server and Windows Authentication mode**, and then click **OK**.</span></span>
   
    ![인증 모드 선택](./media/virtual-machines-sql-server-connection-steps/21Mixed-Mode.png)
5. <span data-ttu-id="5cf31-144">SQL Server Management Studio 대화 상자에서 **확인** 을 클릭하여 SQL Server를 다시 시작해야 하는 요구 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-144">In the SQL Server Management Studio dialog box, click **OK** to acknowledge the requirement to restart SQL Server.</span></span>
6. <span data-ttu-id="5cf31-145">개체 탐색기에서 서버를 마우스 오른쪽 단추로 클릭한 후 **다시 시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-145">In Object Explorer, right-click your server, and then click **Restart**.</span></span> <span data-ttu-id="5cf31-146">SQL Server 에이전트가 실행 중인 경우 에이전트도 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-146">(If SQL Server Agent is running, it must also be restarted.)</span></span>
   
    ![다시 시작](./media/virtual-machines-sql-server-connection-steps/22Restart2.png)
7. <span data-ttu-id="5cf31-148">SQL Server Management Studio 대화 상자에서 **예** 를 클릭하여 SQL Server를 다시 시작한다는 데 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-148">In the SQL Server Management Studio dialog box, click **Yes** to agree that you want to restart SQL Server.</span></span>

### <a name="create-sql-server-authentication-logins"></a><span data-ttu-id="5cf31-149">SQL Server 인증 로그인 만들기</span><span class="sxs-lookup"><span data-stu-id="5cf31-149">Create SQL Server authentication logins</span></span>
<span data-ttu-id="5cf31-150">다른 컴퓨터에서 데이터베이스 엔진에 연결하려면 SQL Server 인증 로그인을 하나 이상 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-150">To connect to the Database Engine from another computer, you must create at least one SQL Server authentication login.</span></span>

1. <span data-ttu-id="5cf31-151">SQL Server Management Studio 개체 탐색기에서 새 로그인을 만들 서버 인스턴스의 폴더를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-151">In SQL Server Management Studio Object Explorer, expand the folder of the server instance in which you want to create the new login.</span></span>
2. <span data-ttu-id="5cf31-152">**보안** 폴더를 마우스 오른쪽 단추로 클릭하고, **새로 만들기**를 가리키고 **로그인...**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-152">Right-click the **Security** folder, point to **New**, and select **Login...**.</span></span>
   
    ![새 로그인](./media/virtual-machines-sql-server-connection-steps/23New-Login.png)
3. <span data-ttu-id="5cf31-154">**로그인 - 신규** 대화 상자의 **일반** 페이지에 있는 **로그인 이름** 상자에 새 사용자의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-154">In the **Login - New** dialog box, on the **General** page, enter the name of the new user in the **Login name** box.</span></span>
4. <span data-ttu-id="5cf31-155">**SQL Server 인증**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-155">Select **SQL Server authentication**.</span></span>
5. <span data-ttu-id="5cf31-156">**암호** 상자에 새 사용자의 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-156">In the **Password** box, enter a password for the new user.</span></span> <span data-ttu-id="5cf31-157">**암호 확인** 상자에 암호를 다시 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-157">Enter that password again into the **Confirm Password** box.</span></span>
6. <span data-ttu-id="5cf31-158">필요한 암호 적용 옵션(**암호 정책 강제 적용**, **암호 만료 강제 적용** 및 **다음 로그인할 때 반드시 암호 변경**)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-158">Select the password enforcement options required (**Enforce password policy**, **Enforce password expiration**, and **User must change password at next login**).</span></span> <span data-ttu-id="5cf31-159">이 로그인을 직접 사용하는 경우 다음 로그인 시 암호를 변경하도록 요구할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-159">If you are using this login for yourself, you do not need to require a password change at the next login.</span></span>
7. <span data-ttu-id="5cf31-160">**기본 데이터베이스** 목록에서 로그인의 기본 데이터베이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-160">From the **Default database** list, select a default database for the login.</span></span> <span data-ttu-id="5cf31-161">**master** 가 이 옵션의 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-161">**master** is the default for this option.</span></span> <span data-ttu-id="5cf31-162">사용자 데이터베이스를 아직 만들지 않은 경우 **master**로 설정된 상태로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-162">If you have not yet created a user database, leave this set to **master**.</span></span>
   
    ![로그인 속성](./media/virtual-machines-sql-server-connection-steps/24Test-Login.png)
8. <span data-ttu-id="5cf31-164">처음 로그인을 만드는 경우 이 로그인을 SQL Server 관리자로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-164">If this is the first login you are creating, you may want to designate this login as a SQL Server administrator.</span></span> <span data-ttu-id="5cf31-165">그렇게 하는 경우 **서버 역할** 페이지에서 **sysadmin**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-165">If so, on the **Server Roles** page, check **sysadmin**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5cf31-166">sysadmin 고정 서버 역할의 구성원은 데이터베이스 엔진을 완전히 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-166">Members of the sysadmin fixed server role have complete control of the Database Engine.</span></span> <span data-ttu-id="5cf31-167">따라서 이 역할의 구성원은 신중하게 제한해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-167">You should carefully restrict membership in this role.</span></span>
   > 
   > 
   
   ![sysadmin](./media/virtual-machines-sql-server-connection-steps/25sysadmin.png)
9. <span data-ttu-id="5cf31-169">확인을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf31-169">Click OK.</span></span>

<span data-ttu-id="5cf31-170">SQL Server 로그인에 대한 자세한 내용은 [로그인 만들기](http://msdn.microsoft.com/library/aa337562.aspx)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="5cf31-170">For more information about SQL Server logins, see [Create a Login](http://msdn.microsoft.com/library/aa337562.aspx).</span></span>

