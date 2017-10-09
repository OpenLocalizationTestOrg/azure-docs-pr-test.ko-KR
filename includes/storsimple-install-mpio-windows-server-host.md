#### <a name="tooinstall-mpio-on-hello-host"></a><span data-ttu-id="d32ab-101">hello 호스트에 MPIO tooinstall</span><span class="sxs-lookup"><span data-stu-id="d32ab-101">tooinstall MPIO on hello host</span></span>
1. <span data-ttu-id="d32ab-102">Windows Server 호스트에서 서버 관리자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d32ab-102">Open Server Manager on your Windows Server host.</span></span> <span data-ttu-id="d32ab-103">기본적으로 서버 관리자 hello Administrators 그룹의 멤버인 Windows Server 2012 R2 또는 Windows Server 2012를 실행 하는 tooa 컴퓨터 로그온 할 때 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d32ab-103">By default, Server Manager starts when a member of hello Administrators group logs on tooa computer that is running Windows Server 2012 R2 or Windows Server 2012.</span></span> <span data-ttu-id="d32ab-104">서버 관리자 hello 열려 있지 않으면 클릭 **시작 > 서버 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="d32ab-104">If hello Server Manager is not already open, click **Start > Server Manager**.</span></span>
   
    ![서버 관리자](./media/storsimple-install-mpio-windows-server/IC740997.png)
2. <span data-ttu-id="d32ab-106">**서버 관리자 > 대시보드 > 역할 및 기능 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d32ab-106">Click **Server Manager > Dashboard > Add roles and features**.</span></span> <span data-ttu-id="d32ab-107">그러면 시작 hello **역할 및 기능 추가** 마법사.</span><span class="sxs-lookup"><span data-stu-id="d32ab-107">This starts hello **Add Roles and Features** wizard.</span></span>
   
    ![역할 및 기능 추가 마법사 1](./media/storsimple-install-mpio-windows-server/IC740998.png)
3. <span data-ttu-id="d32ab-109">Hello에 **역할 및 기능 추가** 마법사에서 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d32ab-109">In hello **Add Roles and Features** wizard, do hello following:</span></span>
   
   * <span data-ttu-id="d32ab-110">Hello에 **시작 하기 전에** 페이지 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="d32ab-110">On hello **Before you begin** page, click **Next**.</span></span>
   * <span data-ttu-id="d32ab-111">Hello에 **설치 유형 선택** 페이지에서의 hello 기본 설정을 그대로 적용 **역할 기반 또는 기능 기반** 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="d32ab-111">On hello **Select installation type** page, accept hello default setting of **Role-based or feature-based** installation.</span></span> <span data-ttu-id="d32ab-112">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d32ab-112">Click **Next**.</span></span>
     
       ![역할 및 기능 추가 마법사 2](./media/storsimple-install-mpio-windows-server/IC740999.png)
   * <span data-ttu-id="d32ab-114">Hello에 **대상 서버 선택** 페이지에서 선택 **hello 서버 풀에서 서버 선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="d32ab-114">On hello **Select destination server** page, choose **Select a server from hello server pool**.</span></span> <span data-ttu-id="d32ab-115">호스트 서버가 자동으로 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="d32ab-115">Your host server should be discovered automatically.</span></span> <span data-ttu-id="d32ab-116">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d32ab-116">Click **Next**.</span></span>
   * <span data-ttu-id="d32ab-117">Hello에 **서버 역할 선택** 페이지 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="d32ab-117">On hello **Select server roles** page, click **Next**.</span></span>
   * <span data-ttu-id="d32ab-118">Hello에 **기능 선택** 페이지 **다중 경로 I/O**를 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="d32ab-118">On hello **Select features** page, select **Multipath I/O**, and click **Next**.</span></span>
     
       ![역할 및 기능 추가 마법사 5](./media/storsimple-install-mpio-windows-server/IC741000.png)
   * <span data-ttu-id="d32ab-120">Hello에 **설치 선택 확인** 페이지 hello 선택 영역을 확인 한 다음 선택 **필요한 경우 자동으로 hello 대상 서버 다시 시작**다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="d32ab-120">On hello **Confirm installation selections** page, confirm hello selection and then select **Restart hello destination server automatically if required**, as shown below.</span></span> <span data-ttu-id="d32ab-121">**Install**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d32ab-121">Click **Install**.</span></span>
     
       ![역할 및 기능 추가 마법사 8](./media/storsimple-install-mpio-windows-server/IC741001.png)
   * <span data-ttu-id="d32ab-123">Hello 설치가 완료 되 면 알림이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d32ab-123">You will be notified when hello installation is complete.</span></span> <span data-ttu-id="d32ab-124">클릭 **닫기** tooclose hello 마법사.</span><span class="sxs-lookup"><span data-stu-id="d32ab-124">Click **Close** tooclose hello wizard.</span></span>
     
       ![역할 및 기능 추가 마법사 9](./media/storsimple-install-mpio-windows-server/IC741002.png)

