## <a name="defining-a-backup-policy"></a><span data-ttu-id="3ae9e-101">백업 정책 정의</span><span class="sxs-lookup"><span data-stu-id="3ae9e-101">Defining a backup policy</span></span>
<span data-ttu-id="3ae9e-102">백업 정책을 및의 행렬을 hello 데이터 스냅숏을 만드는 경우, 해당 스냅숏으로 보관 하는 기간을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae9e-102">A backup policy defines a matrix of when hello data snapshots are taken, and how long those snapshots are retained.</span></span> <span data-ttu-id="3ae9e-103">VM 백업을 위한 정책을 정의할 때 백업 작업을 *하루에 한 번*트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ae9e-103">When defining a policy for backing up a VM, you can trigger a backup job *once a day*.</span></span> <span data-ttu-id="3ae9e-104">새 정책을 만들 때 적용 된 toohello 자격 증명 모음 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ae9e-104">When you create a new policy, it is applied toohello vault.</span></span> <span data-ttu-id="3ae9e-105">hello 백업 정책 인터페이스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3ae9e-105">hello backup policy interface looks like this:</span></span>

![백업 정책](./media/backup-create-policy-for-vms/backup-policy.png)

<span data-ttu-id="3ae9e-107">toocreate 정책:</span><span class="sxs-lookup"><span data-stu-id="3ae9e-107">toocreate a policy:</span></span>

1. <span data-ttu-id="3ae9e-108">Hello에 대 한 이름을 입력 **정책 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae9e-108">Enter a name for hello **Policy name**.</span></span>
2. <span data-ttu-id="3ae9e-109">데이터의 스냅숏을 매일 또는 매주 간격으로 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ae9e-109">Snapshots of your data can be taken at Daily or Weekly intervals.</span></span> <span data-ttu-id="3ae9e-110">사용 하 여 hello **백업 빈도** 드롭 다운 메뉴 toochoose 여부 데이터 스냅숏을 매일 또는 매주입니다.</span><span class="sxs-lookup"><span data-stu-id="3ae9e-110">Use hello **Backup Frequency** drop-down menu toochoose whether data snapshots are taken Daily or Weekly.</span></span>
   
   * <span data-ttu-id="3ae9e-111">일 단위 간격을 선택 하면 hello 스냅숏에 대 한 강조 표시 하는 hello 제어 tooselect hello 시간 hello 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae9e-111">If you choose a Daily interval, use hello highlighted control tooselect hello time of hello day for hello snapshot.</span></span> <span data-ttu-id="3ae9e-112">toochange hello 시간 hello 시간을 선택 취소 하 고 hello 새 시간을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae9e-112">toochange hello hour, de-select hello hour, and select hello new hour.</span></span>
     
     ![매일 백업 정책](./media/backup-create-policy-for-vms/backup-policy-daily.png) <br/>
   * <span data-ttu-id="3ae9e-114">주별 간격을 선택 하면 hello 강조 표시 된 컨트롤 tooselect hello 요일 hello, hello 스냅숏의 시간 일 tootake hello 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae9e-114">If you choose a Weekly interval, use hello highlighted controls tooselect hello day(s) of hello week, and hello time of day tootake hello snapshot.</span></span> <span data-ttu-id="3ae9e-115">Hello 일 메뉴에서 하나 또는 여러 날짜를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae9e-115">In hello day menu, select one or multiple days.</span></span> <span data-ttu-id="3ae9e-116">Hello 시간 메뉴에서 한 시간을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae9e-116">In hello hour menu, select one hour.</span></span> <span data-ttu-id="3ae9e-117">toochange hello 시간 hello 선택 된 시간을 선택 취소 하 고 hello 새 시간을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae9e-117">toochange hello hour, de-select hello selected hour, and select hello new hour.</span></span>
     
     ![매주 백업 정책](./media/backup-create-policy-for-vms/backup-policy-weekly.png)
3. <span data-ttu-id="3ae9e-119">기본적으로 모든 **보존 범위** 옵션이 선택되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ae9e-119">By default, all **Retention Range** options are selected.</span></span> <span data-ttu-id="3ae9e-120">보존 범위 제한이 toouse 하지 않으려면 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae9e-120">Uncheck any retention range limit you do not want toouse.</span></span> <span data-ttu-id="3ae9e-121">그런 다음 hello interval(s) toouse를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae9e-121">Then, specify hello interval(s) toouse.</span></span>
   
    <span data-ttu-id="3ae9e-122">매월 및 매년 보존 범위는 주간 또는 일간 증분 기반 toospecify hello 스냅숏을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae9e-122">Monthly and Yearly retention ranges allow you toospecify hello snapshots based on a weekly or daily increment.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="3ae9e-123">VM을 보호하는 경우, 백업 작업이 하루에 한 번 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ae9e-123">When protecting a VM, a backup job runs once a day.</span></span> <span data-ttu-id="3ae9e-124">때 hello 백업 실행은 hello 동일 각 보존 범위에 대 한 hello 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="3ae9e-124">hello time when hello backup runs is hello same for each retention range.</span></span>
   > 
   > 
4. <span data-ttu-id="3ae9e-125">Hello 정책에 대 한 모든 옵션을 설정한 후 hello의 위쪽 hello 블레이드 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae9e-125">After setting all options for hello policy, at hello top of hello blade click **Save**.</span></span>
   
    <span data-ttu-id="3ae9e-126">hello 새 정책이 즉시 적용 된 toohello 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="3ae9e-126">hello new policy is immediately applied toohello vault.</span></span>

