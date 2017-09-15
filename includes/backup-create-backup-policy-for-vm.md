## <a name="defining-a-backup-policy"></a><span data-ttu-id="00d1e-101">백업 정책 정의</span><span class="sxs-lookup"><span data-stu-id="00d1e-101">Defining a backup policy</span></span>
<span data-ttu-id="00d1e-102">백업 정책은 데이터 스냅숏이 생성된 시간 및 스냅숏을 보관하는 기간에 대한 행렬을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="00d1e-102">A backup policy defines a matrix of when the data snapshots are taken, and how long those snapshots are retained.</span></span> <span data-ttu-id="00d1e-103">VM 백업을 위한 정책을 정의할 때 백업 작업을 *하루에 한 번*트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00d1e-103">When defining a policy for backing up a VM, you can trigger a backup job *once a day*.</span></span> <span data-ttu-id="00d1e-104">새 정책을 만들면 자격 증명 모음에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="00d1e-104">When you create a new policy, it is applied to the vault.</span></span> <span data-ttu-id="00d1e-105">백업 정책 인터페이스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="00d1e-105">The backup policy interface looks like this:</span></span>

![백업 정책](./media/backup-create-policy-for-vms/backup-policy.png)

<span data-ttu-id="00d1e-107">정책을 만들려면:</span><span class="sxs-lookup"><span data-stu-id="00d1e-107">To create a policy:</span></span>

1. <span data-ttu-id="00d1e-108">**정책 이름**에 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="00d1e-108">Enter a name for the **Policy name**.</span></span>
2. <span data-ttu-id="00d1e-109">데이터의 스냅숏을 매일 또는 매주 간격으로 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00d1e-109">Snapshots of your data can be taken at Daily or Weekly intervals.</span></span> <span data-ttu-id="00d1e-110">**백업 주기** 드롭다운 메뉴를 사용하여 데이터 스냅숏을 매일 또는 매주 생성할지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00d1e-110">Use the **Backup Frequency** drop-down menu to choose whether data snapshots are taken Daily or Weekly.</span></span>
   
   * <span data-ttu-id="00d1e-111">매일 간격을 선택한 경우 강조 표시된 컨트롤을 사용하여 스냅숏을 생성할 하루 중 시간을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00d1e-111">If you choose a Daily interval, use the highlighted control to select the time of the day for the snapshot.</span></span> <span data-ttu-id="00d1e-112">시간을 변경하려면 시간을 선택 취소하고 새 시간을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00d1e-112">To change the hour, de-select the hour, and select the new hour.</span></span>
     
     ![매일 백업 정책](./media/backup-create-policy-for-vms/backup-policy-daily.png) <br/>
   * <span data-ttu-id="00d1e-114">매주 간격을 선택한 경우 강조 표시된 컨트롤을 사용하여 스냅숏을 생성할 요일 및 시간을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00d1e-114">If you choose a Weekly interval, use the highlighted controls to select the day(s) of the week, and the time of day to take the snapshot.</span></span> <span data-ttu-id="00d1e-115">일 메뉴에서 하루 또는 여러 날짜를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00d1e-115">In the day menu, select one or multiple days.</span></span> <span data-ttu-id="00d1e-116">시간 메뉴에서 시간을 하나 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00d1e-116">In the hour menu, select one hour.</span></span> <span data-ttu-id="00d1e-117">시간을 변경하려면 선택한 시간을 선택 취소하고 새 시간을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00d1e-117">To change the hour, de-select the selected hour, and select the new hour.</span></span>
     
     ![매주 백업 정책](./media/backup-create-policy-for-vms/backup-policy-weekly.png)
3. <span data-ttu-id="00d1e-119">기본적으로 모든 **보존 범위** 옵션이 선택되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00d1e-119">By default, all **Retention Range** options are selected.</span></span> <span data-ttu-id="00d1e-120">사용하지 않으려면 보존 범위 제한을 선택 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="00d1e-120">Uncheck any retention range limit you do not want to use.</span></span> <span data-ttu-id="00d1e-121">그런 다음 사용할 간격을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="00d1e-121">Then, specify the interval(s) to use.</span></span>
   
    <span data-ttu-id="00d1e-122">매월 및 매년 보존 범위를 통해 매주 또는 매일 증분으로 스냅숏을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00d1e-122">Monthly and Yearly retention ranges allow you to specify the snapshots based on a weekly or daily increment.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="00d1e-123">VM을 보호하는 경우, 백업 작업이 하루에 한 번 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="00d1e-123">When protecting a VM, a backup job runs once a day.</span></span> <span data-ttu-id="00d1e-124">백업이 실행되는 시간은 보존 범위마다 같습니다.</span><span class="sxs-lookup"><span data-stu-id="00d1e-124">The time when the backup runs is the same for each retention range.</span></span>
   > 
   > 
4. <span data-ttu-id="00d1e-125">정책에 대한 모든 옵션을 설정한 후 블레이드 맨 위에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00d1e-125">After setting all options for the policy, at the top of the blade click **Save**.</span></span>
   
    <span data-ttu-id="00d1e-126">자격 증명 모음에 새 정책이 즉시 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="00d1e-126">The new policy is immediately applied to the vault.</span></span>

