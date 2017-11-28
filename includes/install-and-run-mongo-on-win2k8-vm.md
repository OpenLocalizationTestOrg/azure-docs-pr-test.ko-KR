<span data-ttu-id="33255-101">다음 단계에 따라 Windows Server를 실행하는 가상 컴퓨터에 MongoDB를 설치하고 실행하세요.</span><span class="sxs-lookup"><span data-stu-id="33255-101">Follow these steps to install and run MongoDB on a virtual machine running Windows Server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="33255-102">인증 및 IP 주소 바인딩과 같은 MongoDB 보안 기능은 기본적으로 사용하도록 설정되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="33255-102">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span></span> <span data-ttu-id="33255-103">MongoDB를 프로덕션 환경에 배포하기 전에 보안 기능을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33255-103">Security features should be enabled before deploying MongoDB to a production environment.</span></span>  <span data-ttu-id="33255-104">자세한 내용은 [보안 및 인증](http://www.mongodb.org/display/DOCS/Security+and+Authentication)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="33255-104">For more information, see [Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span></span>
>
>

1. <span data-ttu-id="33255-105">원격 데스크톱을 사용하여 가상 컴퓨터에 연결한 후 가상 컴퓨터의 **시작** 메뉴에서 Internet Explorer를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="33255-105">After you've connected to the virtual machine using Remote Desktop, open Internet Explorer from the **Start** menu on the virtual machine.</span></span>
2. <span data-ttu-id="33255-106">오른쪽 위에 있는 **도구** 버튼을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33255-106">Select the **Tools** button in the upper right corner.</span></span>  <span data-ttu-id="33255-107">**인터넷 옵션**에서 **보안** 탭을 선택한 후 **신뢰할 수 있는 사이트** 아이콘을 선택하고 마지막으로 **사이트** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33255-107">In **Internet Options**, select the **Security** tab, and then select the **Trusted Sites** icon, and finally click the **Sites** button.</span></span> <span data-ttu-id="33255-108">신뢰할 수 있는 사이트 목록에 *https://\*.mongodb.org*를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="33255-108">Add *https://\*.mongodb.org* to the list of trusted sites.</span></span>
3. <span data-ttu-id="33255-109">[다운로드 - MongoDB](https://www.mongodb.com/download-center#community)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="33255-109">Go to [Downloads - MongoDB](https://www.mongodb.com/download-center#community).</span></span>
4. <span data-ttu-id="33255-110">**커뮤니티 서버**의 **현재 안정적인 릴리스**를 찾고 Windows 열에서 최신 **64비트** 버전을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33255-110">Find the **Current Stable Release** of **Community Server**, select the latest **64-bit** version in the Windows column.</span></span> <span data-ttu-id="33255-111">MSI 설치 관리자를 다운로드하여 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="33255-111">Download, then run the MSI installer.</span></span>
5. <span data-ttu-id="33255-112">일반적으로 MongoDB는 C:\Program Files\MongoDB에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="33255-112">MongoDB is typically installed in C:\Program Files\MongoDB.</span></span> <span data-ttu-id="33255-113">바탕 화면에서 환경 변수를 검색하고는 PATH 변수에 MongoDB 이진 파일 경로를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="33255-113">Search for Environment Variables on the desktop and add the MongoDB binaries path to the PATH variable.</span></span> <span data-ttu-id="33255-114">예를 들어 컴퓨터의 C:\Program Files\MongoDB\Server\3.4\bin에서 이진 파일을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33255-114">For example, you might find the binaries at C:\Program Files\MongoDB\Server\3.4\bin on your machine.</span></span>
6. <span data-ttu-id="33255-115">앞의 단계에서 만든 데이터 디스크(예: **F:** 드라이브)에서 MongoDB 데이터 및 로그 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33255-115">Create MongoDB data and log directories in the data disk (such as drive **F:**) you created in the preceding steps.</span></span> <span data-ttu-id="33255-116">**시작**에서 **명령 프롬프트**를 선택하여 명령 프롬프트 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="33255-116">From **Start**, select **Command Prompt** to open a command prompt window.</span></span>  <span data-ttu-id="33255-117">형식:</span><span class="sxs-lookup"><span data-stu-id="33255-117">Type:</span></span>

        C:\> F:
        F:\> mkdir \MongoData
        F:\> mkdir \MongoLogs
7. <span data-ttu-id="33255-118">데이터베이스를 실행하려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="33255-118">To run the database, run:</span></span>

        F:\> C:
        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log

    <span data-ttu-id="33255-119">mongod.exe 서버를 시작하고 저널 파일을 사전 할당하면 모든 로그 메시지가 *F:\MongoLogs\mongolog.log* 파일로 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="33255-119">All log messages are directed to the *F:\MongoLogs\mongolog.log* file as mongod.exe server starts and preallocates journal files.</span></span> <span data-ttu-id="33255-120">MongoDB가 저널 파일을 사전 할당하고 연결이 수신될 때까지 몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33255-120">It may take several minutes for MongoDB to preallocate the journal files and start listening for connections.</span></span> <span data-ttu-id="33255-121">명령 프롬프트는 MongoDB 인스턴스가 실행되는 동안 이 태스크에 계속 집중합니다.</span><span class="sxs-lookup"><span data-stu-id="33255-121">The command prompt stays focused on this task while your MongoDB instance is running.</span></span>
8. <span data-ttu-id="33255-122">MongoDB 관리 셸을 시작하려면 **시작**에서 명령 창을 하나 더 열어 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="33255-122">To start the MongoDB administrative shell, open another command window from **Start** and type the following commands:</span></span>

        C:\> cd \my_mongo_dir\bin  
        C:\my_mongo_dir\bin> mongo  
        >db  
        test
        > db.foo.insert( { a : 1 } )  
        > db.foo.find()  
        { _id : ..., a : 1 }  
        > show dbs  
        ...  
        > show collections  
        ...  
        > help  

    <span data-ttu-id="33255-123">이렇게 하면 데이터베이스가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="33255-123">The database is created by the insert.</span></span>
9. <span data-ttu-id="33255-124">또는 mongod.exe를 서비스로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33255-124">Alternatively, you can install mongod.exe as a service:</span></span>

        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log --logappend  --install

    <span data-ttu-id="33255-125">이렇게 하면 "Mongo DB"에 대한 설명이 포함된 MongoDB라는 서비스가 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="33255-125">A service is installed named MongoDB with a description of "Mongo DB".</span></span> <span data-ttu-id="33255-126">실행 중인 서비스는 명령 창에 결과가 표시되지 않으므로 `--logpath` 옵션을 사용하여 로그 파일을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33255-126">The `--logpath` option must be used to specify a log file, since the running service does not have a command window to display output.</span></span>  <span data-ttu-id="33255-127">`--logappend` 옵션은 서비스를 다시 시작할 때 기존 로그 파일에 출력을 추가하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="33255-127">The `--logappend` option specifies that a restart of the service causes output to append to the existing log file.</span></span>  <span data-ttu-id="33255-128">`--dbpath` 옵션은 데이터 디렉터리의 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="33255-128">The `--dbpath` option specifies the location of the data directory.</span></span> <span data-ttu-id="33255-129">서비스 관련 명령줄 옵션에 대한 자세한 내용은 [서비스 관련 명령줄 옵션][MongoWindowsSvcOptions](영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="33255-129">For more service-related command-line options, see [Service-related command-line options][MongoWindowsSvcOptions].</span></span>

    <span data-ttu-id="33255-130">서비스를 시작하려면 이 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="33255-130">To start the service, run this command:</span></span>

        C:\> net start MongoDB
10. <span data-ttu-id="33255-131">이제 MongoDB가 설치되고 실행됩니다. 원격으로 MongoDB에 연결하려면 Windows 방화벽에 있는 포트를 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33255-131">Now that MongoDB is installed and running, you need to open a port in Windows Firewall so you can remotely connect to MongoDB.</span></span>  <span data-ttu-id="33255-132">**시작** 메뉴에서 **관리 도구**를 선택한 후 **고급 보안이 포함된 Windows 방화벽**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33255-132">From the **Start** menu, select **Administrative Tools** and then **Windows Firewall with Advanced Security**.</span></span>
11. <span data-ttu-id="33255-133">a) 왼쪽 창에서 **인바운드 규칙**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33255-133">a) In the left pane, select **Inbound Rules**.</span></span>  <span data-ttu-id="33255-134">오른쪽에 있는 **작업** 창에서 **새 규칙...**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33255-134">In the **Actions** pane on the right, select **New Rule...**.</span></span>

    ![Windows 방화벽][Image1]

    <span data-ttu-id="33255-136">b) **새 인바운드 규칙 마법사**에서 **포트**를 선택한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33255-136">b) In the **New Inbound Rule Wizard**, select **Port** and then click **Next**.</span></span>

    ![Windows 방화벽][Image2]

    <span data-ttu-id="33255-138">c) **TCP**를 선택한 후 **특정 로컬 포트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33255-138">c) Select **TCP** and then **Specific local ports**.</span></span>  <span data-ttu-id="33255-139">"27017" 포트(MongoDB의 기본 수신 포트)를 지정하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33255-139">Specify a port of "27017" (the default port MongoDB listens on) and click **Next**.</span></span>

    ![Windows 방화벽][Image3]

    <span data-ttu-id="33255-141">d) **연결 허용**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33255-141">d) Select **Allow the connection** and click **Next**.</span></span>

    ![Windows 방화벽][Image4]

    <span data-ttu-id="33255-143">e) 다시 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33255-143">e) Click **Next** again.</span></span>

    ![Windows 방화벽][Image5]

    <span data-ttu-id="33255-145">f) "MongoPort"와 같은 규칙 이름을 지정하고 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33255-145">f) Specify a name for the rule, such as "MongoPort", and click **Finish**.</span></span>

    ![Windows 방화벽][Image6]

12. <span data-ttu-id="33255-147">가상 컴퓨터를 만들 때 MongoDB에 대한 끝점을 구성하지 않은 경우 지금 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33255-147">If you didn't configure an endpoint for MongoDB when you created the virtual machine, you can do it now.</span></span> <span data-ttu-id="33255-148">원격으로 MongoDB에 연결하려면 방화벽 규칙 및 끝점이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33255-148">You need both the firewall rule and the endpoint to be able to connect to MongoDB remotely.</span></span>

  <span data-ttu-id="33255-149">Azure Portal에서 **Virtual Machines(클래식)**를 클릭하고 새 가상 컴퓨터의 이름을 클릭한 다음 **끝점**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33255-149">In the Azure portal, click **Virtual Machines (classic)**, click the name of your new virtual machine, and then click **Endpoints**.</span></span>

    ![끝점][Image7]

13. <span data-ttu-id="33255-151">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="33255-151">Click **Add**.</span></span>

14. <span data-ttu-id="33255-152">이름이 "Mongo"이고 프로토콜이 **TCP**이며 **공용** 및 **개인** 포트를 "27017"로 설정한 끝점을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="33255-152">Add an endpoint with name "Mongo", protocol **TCP**, and both **Public** and **Private** ports set to "27017".</span></span> <span data-ttu-id="33255-153">이 포트를 열면 MongoDB에 원격으로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33255-153">Opening this port allows MongoDB to be accessed remotely.</span></span>

    ![끝점][Image9]

> [!NOTE]
> <span data-ttu-id="33255-155">27017 포트가 MongoDB 사용되는 기본 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="33255-155">The port 27017 is the default port used by MongoDB.</span></span> <span data-ttu-id="33255-156">mongod.exe 서버를 시작할 때 `--port` 매개 변수를 지정하여 이 기본 포트를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33255-156">You can change this default port by specifying the `--port` parameter when starting the mongod.exe server.</span></span> <span data-ttu-id="33255-157">방화벽에서 동일한 포트 번호 및 앞의 지침에 있는 "Mongo" 끝점을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33255-157">Make sure to give the same port number in the firewall and the "Mongo" endpoint in the preceding instructions.</span></span>
>
>

[MongoDownloads]: http://www.mongodb.org/downloads

[MongoWindowsSvcOptions]: http://www.mongodb.org/display/DOCS/Windows+Service


[Image1]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall1.png
[Image2]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall2.png
[Image3]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall3.png
[Image4]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall4.png
[Image5]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall5.png
[Image6]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall6.png
[Image7]: ./media/install-and-run-mongo-on-win2k8-vm/menusendpointadd.png
<!-- Removed 03/08/2017. Not in new portal. -->
<!-- [Image8]: ./media/install-and-run-mongo-on-win2k8-vm/WinVmAddEndpoint2.png
-->
[Image9]: ./media/install-and-run-mongo-on-win2k8-vm/newendpointdetails.png
