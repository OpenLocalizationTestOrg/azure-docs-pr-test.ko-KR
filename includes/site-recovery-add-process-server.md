1. <span data-ttu-id="5c9b3-101">Azure Site Recovery UnifiedSetup.exe 시작</span><span class="sxs-lookup"><span data-stu-id="5c9b3-101">Launch the Azure Site Recovery UnifiedSetup.exe</span></span>
2. <span data-ttu-id="5c9b3-102">**시작하기 전에**에서 **배포 규모 확장을 위해 추가 프로세스 서버 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5c9b3-102">In **Before you begin**, select **Add additional process servers to scale out deployment**.</span></span>

  ![프로세스 서버 추가](./media/site-recovery-add-process-server/ps-page-1.png)

3. <span data-ttu-id="5c9b3-104">**구성 서버 세부 정보**에서 구성 서버의 IP 주소 및 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5c9b3-104">In **Configuration Server Details**, specify the IP address of the Configuration Server, and the passphrase.</span></span>

  ![프로세스 서버 2 추가](./media/site-recovery-add-process-server/ps-page-2.png)
4. <span data-ttu-id="5c9b3-106">**인터넷 설정**에서 구성 서버에서 실행 중인 공급자가 인터넷을 통해 Azure Site Recovery에 연결하는 방법을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5c9b3-106">In **Internet Settings**, specify how the Provider running on the Configuration Server connects to Azure Site Recovery over the Internet.</span></span>

  ![프로세스 서버 3 추가](./media/site-recovery-add-process-server/ps-page-3.png)

   * <span data-ttu-id="5c9b3-108">현재 컴퓨터에 설정된 프록시를 사용하여 연결하려면 **기존 프록시 설정을 사용하여 연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5c9b3-108">If you want to connect with the proxy that's currently set up on the machine, select **Connect with existing proxy settings**.</span></span>
   * <span data-ttu-id="5c9b3-109">공급자가 직접 연결되도록 하려면 **프록시 없이 직접 연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5c9b3-109">If you want the Provider to connect directly, select **Connect directly without a proxy**.</span></span>
   * <span data-ttu-id="5c9b3-110">기존 프록시에 인증이 필요하거나 공급자 연결에 대해 사용자 지정 프록시를 사용하려면 **사용자 지정 프록시 설정을 사용하여 연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5c9b3-110">If the existing proxy requires authentication, or if you want to use a custom proxy for the Provider connection, select **Connect with custom proxy settings**.</span></span>

     * <span data-ttu-id="5c9b3-111">사용자 지정 프록시를 사용하는 경우 주소, 포트 및 자격 증명을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c9b3-111">If you use a custom proxy, you need to specify the address, port, and credentials.</span></span>
     * <span data-ttu-id="5c9b3-112">프록시를 사용하는 경우 이미 서비스 URL에 대한 액세스를 허용했어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c9b3-112">If you're using a proxy, you should have already allowed access to the service urls.</span></span>

5. <span data-ttu-id="5c9b3-113">**필수 조건 확인**에서 설치 프로그램은 설치가 실행될 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5c9b3-113">In **Prerequisites Check**, Setup runs a check to make sure that installation can run.</span></span> <span data-ttu-id="5c9b3-114">**글로벌 시간 동기화 확인**에 대한 경고가 표시되면 시스템 시계의 시간(**날짜 및 시간** 설정)이 표준 시간대와 같은지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5c9b3-114">If a warning appears about the **Global time sync check**, verify that the time on the system clock (**Date and Time** settings) is the same as the time zone.</span></span>

     ![프로세스 서버 4 추가](./media/site-recovery-add-process-server/ps-page-4.png)

6. <span data-ttu-id="5c9b3-116">**환경 세부 정보**에서 VMware VM을 복제 여부를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5c9b3-116">In **Environment Details**, select whether you're going to replicate VMware VMs.</span></span> <span data-ttu-id="5c9b3-117">복제할 경우 설치 프로그램에서 PowerCLI 6.0이 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5c9b3-117">If you are, then setup checks that PowerCLI 6.0 is installed.</span></span>

     ![프로세스 서버 5 추가](./media/site-recovery-add-process-server/ps-page-5.png)

7. <span data-ttu-id="5c9b3-119">**설치 위치**에서 이진 파일을 설치하고 캐시를 저장할 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5c9b3-119">In **Install Location**, select where you want to install the binaries and store the cache.</span></span> <span data-ttu-id="5c9b3-120">최소 5GB의 디스크 공간이 있는 드라이브를 선택해야 하지만 600GB 이상의 사용 가능한 공간이 있는 캐시 드라이브를 선택하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5c9b3-120">The drive you select must have at least 5 GB of disk space available, but we recommend a cache drive with at least 600 GB of free space.</span></span>
     <span data-ttu-id="5c9b3-121">![프로세스 서버 5 추가](./media/site-recovery-add-process-server/ps-page-6.png)</span><span class="sxs-lookup"><span data-stu-id="5c9b3-121">![Add process server 5](./media/site-recovery-add-process-server/ps-page-6.png)</span></span>

8. <span data-ttu-id="5c9b3-122">**네트워크 선택**에서 구성 서버가 복제 데이터를 전송 및 수신할 수신기(네트워크 어댑터 및 SSL 포트)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5c9b3-122">In **Network Selection**, specify the listener (network adapter and SSL port) on which the Configuration Server sends and receives replication data.</span></span> <span data-ttu-id="5c9b3-123">9443 포트는 복제 트래픽을 보내고 받는 데 사용되는 기본 포트이지만, 환경의 요구 사항에 맞게 이 포트 번호를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c9b3-123">Port 9443 is the default port used for sending and receiving replication traffic, but you can modify this port number to suit your environment's requirements.</span></span> <span data-ttu-id="5c9b3-124">9443 포트 외에도 웹 서버에서 복제 작업을 조정하기 위해 사용하는 443 포트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5c9b3-124">In addition to the port 9443, we also open port 443, which is used by a web server to orchestrate replication operations.</span></span> <span data-ttu-id="5c9b3-125">복제 트래픽을 보내거나 받는 데 443 포트를 사용하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c9b3-125">Do not use Port 443 for sending or receiving replication traffic.</span></span>

     ![프로세스 서버 6 추가](./media/site-recovery-add-process-server/ps-page-7.png)
9. <span data-ttu-id="5c9b3-127">**요약**에서 정보를 검토하고 **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c9b3-127">In **Summary**, review the information and click **Install**.</span></span> <span data-ttu-id="5c9b3-128">설치가 완료되면 암호가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c9b3-128">When installation finishes, a passphrase is generated.</span></span> <span data-ttu-id="5c9b3-129">복제를 사용하도록 설정할 때 필요하므로 암호를 복사하고 안전한 위치에 보관합니다.</span><span class="sxs-lookup"><span data-stu-id="5c9b3-129">You will need this when you enable replication, so copy it and keep it in a secure location.</span></span>

     ![프로세스 서버 7 추가](./media/site-recovery-add-process-server/ps-page-8.png)
