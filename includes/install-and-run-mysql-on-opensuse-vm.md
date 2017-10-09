
1. <span data-ttu-id="8df60-101">형식 tooescalate 권한:</span><span class="sxs-lookup"><span data-stu-id="8df60-101">tooescalate privileges, type:</span></span>
   
        sudo -s
   
    <span data-ttu-id="8df60-102">암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8df60-102">Enter your password.</span></span>
2. <span data-ttu-id="8df60-103">MySQL Community 서버 에디션 tooinstall 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8df60-103">tooinstall MySQL Community Server edition, type:</span></span>
   
        zypper install mysql-community-server
   
    <span data-ttu-id="8df60-104">MySQL이 다운로드되어 설치될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="8df60-104">Wait while MySQL downloads and installs.</span></span>
3. <span data-ttu-id="8df60-105">hello 시스템을 부팅할 때 tooset MySQL toostart, 유형:</span><span class="sxs-lookup"><span data-stu-id="8df60-105">tooset MySQL toostart when hello system boots, type:</span></span>
   
        insserv mysql
4. <span data-ttu-id="8df60-106">이 명령을 사용 하 여 hello MySQL 디먼 (mysqld)를 수동으로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="8df60-106">Start hello MySQL daemon (mysqld) manually with this command:</span></span>
   
        rcmysql start
   
    <span data-ttu-id="8df60-107">toocheck hello 상태 hello MySQL 데몬을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8df60-107">toocheck hello status of hello MySQL daemon, type:</span></span>
   
        rcmysql status
   
    <span data-ttu-id="8df60-108">toostop hello MySQL 데몬 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8df60-108">toostop hello MySQL daemon, type:</span></span>
   
        rcmysql stop
   
   > [!IMPORTANT]
   > <span data-ttu-id="8df60-109">설치가 끝나면 hello MySQL 루트 암호는 기본적으로 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8df60-109">After installation, hello MySQL root password is empty by default.</span></span> <span data-ttu-id="8df60-110">MySQL 보안에 도움이 되는 **mysql\_secure\_installation** 스크립트를 실행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8df60-110">We recommended that you run **mysql\_secure\_installation**, a script that helps secure MySQL.</span></span> <span data-ttu-id="8df60-111">hello 스크립트 묻는 toochange hello MySQL 루트 암호, 익명 사용자 계정을 제거, 원격 루트 로그인을 사용 하지 않도록 설정, 테스트 데이터베이스를 제거 및 hello 권한 테이블을 다시 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="8df60-111">hello script prompts you toochange hello MySQL root password, remove anonymous user accounts, disable remote root logins, remove test databases, and reload hello privileges table.</span></span> <span data-ttu-id="8df60-112">이러한 옵션의 예 tooall 대답 hello 루트 암호를 변경 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8df60-112">We recommended that you answer yes tooall of these options and change hello root password.</span></span>
   > 
   > 
5. <span data-ttu-id="8df60-113">이 toorun hello 스크립트 MySQL 설치 스크립트를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8df60-113">Type this toorun hello script MySQL installation script:</span></span>
   
        mysql_secure_installation
6. <span data-ttu-id="8df60-114">TooMySQL 로그인:</span><span class="sxs-lookup"><span data-stu-id="8df60-114">Log in tooMySQL:</span></span>
   
        mysql -u root -p
   
    <span data-ttu-id="8df60-115">Hello MySQL 루트 암호 (hello 이전 단계에서 변경 됨)을 입력 하 고 제공 됩니다는 메시지로 hello 데이터베이스와 SQL 문을 toointeract 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8df60-115">Enter hello MySQL root password (which you changed in hello previous step) and you'll be presented with a prompt where you can issue SQL statements toointeract with hello database.</span></span>
7. <span data-ttu-id="8df60-116">hello에 hello 다음 실행 하는 새 MySQL 사용자 toocreate **mysql >** 프롬프트:</span><span class="sxs-lookup"><span data-stu-id="8df60-116">toocreate a new MySQL user, run hello following at hello **mysql>** prompt:</span></span>
   
        CREATE USER 'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    <span data-ttu-id="8df60-117">Hello 세미콜론 (;)으로 설명 하면 hello의 hello 끝에 줄은 보류 된 hello 명령에 대 한 매우 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8df60-117">Note, hello semi-colons (;) at hello end of hello lines are crucial for ending hello commands.</span></span>
8. <span data-ttu-id="8df60-118">데이터베이스 및 부여 hello toocreate `mysqluser` 것 문제 hello 명령 다음에 대 한 사용자 권한을:</span><span class="sxs-lookup"><span data-stu-id="8df60-118">toocreate a database and grant hello `mysqluser` user permissions on it, issue hello following commands:</span></span>
   
        CREATE DATABASE testdatabase;
        GRANT ALL ON testdatabase.* too'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    <span data-ttu-id="8df60-119">사용 되는 데이터베이스 사용자 이름 및 암호는 스크립트 toohello 데이터베이스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="8df60-119">Note that database user names and passwords are only used by scripts connecting toohello database.</span></span>  <span data-ttu-id="8df60-120">데이터베이스 사용자 계정 이름은 반드시 hello 시스템에서 실제 사용자 계정을 나타내지는지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8df60-120">Database user account names do not necessarily represent actual user accounts on hello system.</span></span>
9. <span data-ttu-id="8df60-121">다른 컴퓨터 종류에서에서에서 toolog:</span><span class="sxs-lookup"><span data-stu-id="8df60-121">toolog in from another computer, type:</span></span>
   
        GRANT ALL ON testdatabase.* too'mysqluser'@'<ip-address>' IDENTIFIED BY 'password';
   
    <span data-ttu-id="8df60-122">여기서 `ip-address` tooMySQL 연결 될 있는 hello 컴퓨터의 hello IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="8df60-122">where `ip-address` is hello IP address of hello computer from which you will connect tooMySQL.</span></span>
10. <span data-ttu-id="8df60-123">tooexit hello MySQL 데이터베이스 관리 유틸리티를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8df60-123">tooexit hello MySQL database administration utility, type:</span></span>
    
        quit

## <a name="add-an-endpoint"></a><span data-ttu-id="8df60-124">끝점 추가</span><span class="sxs-lookup"><span data-stu-id="8df60-124">Add an endpoint</span></span>
1. <span data-ttu-id="8df60-125">MySQL 설치 된 후 원격 끝점 tooaccess MySQL tooconfigure가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8df60-125">After MySQL is installed, you'll need tooconfigure an endpoint tooaccess MySQL remotely.</span></span> <span data-ttu-id="8df60-126">Toohello 로그인 [Azure 클래식 포털][AzurePortal]합니다.</span><span class="sxs-lookup"><span data-stu-id="8df60-126">Log in toohello [Azure  classic portal][AzurePortal].</span></span> <span data-ttu-id="8df60-127">클릭 **가상 컴퓨터**새 가상 컴퓨터의 hello 이름을 클릭 하 고 클릭 **끝점**합니다.</span><span class="sxs-lookup"><span data-stu-id="8df60-127">Click **Virtual Machines**, click hello name of your new virtual machine, and then click **Endpoints**.</span></span>
2. <span data-ttu-id="8df60-128">클릭 **추가** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8df60-128">Click **Add** at hello bottom of hello page.</span></span>
3. <span data-ttu-id="8df60-129">끝점 프로토콜 "MySQL" 라는 추가 **TCP**, 및 **공용** 및 **개인** 포트 집합 너무 "3306" 합니다.</span><span class="sxs-lookup"><span data-stu-id="8df60-129">Add an endpoint named "MySQL" with protocol **TCP**, and **Public** and **Private** ports set too"3306".</span></span>
4. <span data-ttu-id="8df60-130">tooremotely는 컴퓨터 종류에서에서 toohello 가상 컴퓨터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="8df60-130">tooremotely connect toohello virtual machine from your computer, type:</span></span>
   
        mysql -u mysqluser -p -h <yourservicename>.cloudapp.net
   
    <span data-ttu-id="8df60-131">예를 들어이 자습서에서 만든 hello 가상 컴퓨터를 사용 하 여이 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8df60-131">For example, using hello virual machine we created in this tutorial, type this command:</span></span>
   
        mysql -u mysqluser -p -h testlinuxvm.cloudapp.net

[MySQLDocs]: http://dev.mysql.com/doc/
[AzurePortal]: http://manage.windowsazure.com

[Image9]: ./media/install-and-run-mysql-on-opensuse-vm/LinuxVmAddEndpointMySQL.png
