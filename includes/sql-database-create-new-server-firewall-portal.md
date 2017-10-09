
<!--
includes/sql-database-create-new-server-firewall-portal.md

Latest Freshness check:  2016-11-28 , rickbyh.

As of circa 2016-04-11, hello following topics might include this include:
articles/sql-database/sql-database-get-started.md
articles/sql-database/sql-database-configure-firewall-settings
articles/sql-data-warehouse-get-started-provision.md

-->
### <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="f7c39-101">Hello Azure 포털에에서 서버 수준 방화벽 규칙을 만들려면</span><span class="sxs-lookup"><span data-stu-id="f7c39-101">Create a server-level firewall rule in hello Azure portal</span></span>

1. <span data-ttu-id="f7c39-102">설정에서 hello SQL server 블레이드 클릭 **방화벽** tooopen hello 방화벽 블레이드 hello SQL server에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c39-102">On hello SQL server blade, under Settings, click **Firewall** tooopen hello Firewall blade for hello SQL server.</span></span>

    <!-- ![sql server firewall](../articles/sql-database/media/sql-database-get-started/sql-server-firewall.png) -->

2. <span data-ttu-id="f7c39-103">Hello 클라이언트 IP 주소 표시를 검토 하 고 hello 원하는 브라우저를 사용 하 여 인터넷에서 사용자의 IP 주소 인지 확인 ("what is 내 IP 주소 확인).</span><span class="sxs-lookup"><span data-stu-id="f7c39-103">Review hello client IP address displayed and validate that this is your IP address on hello Internet using a browser of your choice (ask "what is my IP address).</span></span> <span data-ttu-id="f7c39-104">때로는 여러 가지 이유로 일치하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c39-104">Occasionally they do not match for a various reasons.</span></span>

    <!-- ![your IP address](../articles/sql-database/media/sql-database-get-started/your-ip-address.png) -->

3. <span data-ttu-id="f7c39-105">클릭 하 여 hello IP 주소와 일치 이라고 가정할 **클라이언트 IP 추가** hello 도구 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="f7c39-105">Assuming that hello IP addresses match, click **Add client IP** on hello toolbar.</span></span>

    ![클라이언트 IP 추가](../articles/sql-data-warehouse/media/sql-data-warehouse-get-started-provision/add-client-ip.png)

    > [!NOTE]
    > <span data-ttu-id="f7c39-107">Hello 서버 tooa 단일 IP 주소에서 hello SQL 데이터베이스 방화벽 또는 주소 범위는 전체 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c39-107">You can open hello SQL Database firewall on hello server tooa single IP address or an entire range of addresses.</span></span> <span data-ttu-id="f7c39-108">Opening hello 방화벽을 SQL 관리자가 사용 하 고 사용자가 toologin tooany 데이터베이스에 hello 서버 toowhich 유효한 자격 증명을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="f7c39-108">Opening hello firewall enables SQL administrators and users toologin tooany database on hello server toowhich they have valid credentials.</span></span>
    >

4. <span data-ttu-id="f7c39-109">클릭 **저장** 에서 hello 도구 모음 toosave이 서버 수준 방화벽 규칙을 클릭 한 다음 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7c39-109">Click **Save** on hello toolbar toosave this server-level firewall rule and then click **OK**.</span></span>

    ![클라이언트 IP 추가](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule.png)

> [!Tip]
> <span data-ttu-id="f7c39-111">자습서에 대해서는 [SQL Database 자습서: 서버, 서버 수준 방화벽 규칙, 샘플 데이터베이스, 데이터베이스 수준 방화벽 규칙 및 SQL Server 연결 만들기](../articles/sql-database/sql-database-get-started.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7c39-111">For a tutorial, see [SQL Database tutorial: Create a server, a server-level firewall rule, a sample database, a database-level firewall rule and connect with SQL Server](../articles/sql-database/sql-database-get-started.md).</span></span>    
>
