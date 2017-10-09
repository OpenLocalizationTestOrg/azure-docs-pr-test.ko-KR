<!--author=alkohli last changed: 9/17/15-->

### <a name="tootake-a-backup"></a><span data-ttu-id="e1dee-101">tootake 백업</span><span class="sxs-lookup"><span data-stu-id="e1dee-101">tootake a backup</span></span>
1. <span data-ttu-id="e1dee-102">Hello 장치에서 **빠른 시작** 페이지 **백업 정책 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="e1dee-102">On hello device **Quick Start** page, click **Add a backup policy**.</span></span> <span data-ttu-id="e1dee-103">Hello 백업 정책 추가 마법사가 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1dee-103">This will start hello Add Backup Policy wizard.</span></span> 
2. <span data-ttu-id="e1dee-104">Hello에 **백업 정책 정의** 페이지:</span><span class="sxs-lookup"><span data-stu-id="e1dee-104">On hello **Define your backup policy** page:</span></span>
   
   1. <span data-ttu-id="e1dee-105">백업 정책 이름을 3~150자 사이로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e1dee-105">Supply a name that contains between 3 and 150 characters for your backup policy.</span></span>
   2. <span data-ttu-id="e1dee-106">백업 hello 볼륨 toobe를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1dee-106">Select hello volumes toobe backed up.</span></span> <span data-ttu-id="e1dee-107">하나 이상의 볼륨을 선택 하면 이러한 볼륨은 그룹화 된 함께 toocreate는 크래시 일관성이 있는 백업이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1dee-107">If you select more than one volume, these volumes will be grouped together toocreate a crash-consistent backup.</span></span>
   3. <span data-ttu-id="e1dee-108">Hello 화살표 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1dee-108">Click hello arrow icon</span></span> ![화살표 아이콘](./media/storsimple-take-backup/HCS_ArrowIcon-include.png)<span data-ttu-id="e1dee-110">를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e1dee-110">.</span></span> 
      
      ![Add-backup-policy](./media/storsimple-take-backup/HCS_AddBackupPolicyWizard1M-include.png)
3. <span data-ttu-id="e1dee-112">Hello에 **일정 정의** 페이지:</span><span class="sxs-lookup"><span data-stu-id="e1dee-112">On hello **Define a schedule** page:</span></span>
   
   1. <span data-ttu-id="e1dee-113">Hello 드롭 다운 목록에서 백업 hello 종류를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1dee-113">Select hello type of backup from hello drop-down list.</span></span> <span data-ttu-id="e1dee-114">빠른 복원을 수행하려면 **로컬 스냅숏**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e1dee-114">For faster restores, select **Local Snapshot**.</span></span> <span data-ttu-id="e1dee-115">데이터를 복원하려면 **클라우드 스냅숏**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e1dee-115">For data resiliency, select **Cloud Snapshot**.</span></span>
   2. <span data-ttu-id="e1dee-116">분, 시간, 일 또는 주에 hello 백업 빈도 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1dee-116">Specify hello backup frequency in minutes, hours, days, or weeks.</span></span>
   3. <span data-ttu-id="e1dee-117">보존 시간을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e1dee-117">Select a retention time.</span></span> <span data-ttu-id="e1dee-118">hello 보존 선택 hello 백업 빈도에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="e1dee-118">hello retention choices depend on hello backup frequency.</span></span> <span data-ttu-id="e1dee-119">예를 들어 일별 정책의 경우에 대 한 hello 보존 수 수 주 단위로 지정 월별 정책의 경우 월 단위로.</span><span class="sxs-lookup"><span data-stu-id="e1dee-119">For example, for a daily policy, hello retention can be specified in weeks, whereas retention for a monthly policy is in months.</span></span>
   4. <span data-ttu-id="e1dee-120">Hello 백업 정책에 대 한 날짜 및 시간을 시작 하는 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1dee-120">Select hello starting time and date for hello backup policy.</span></span>
   5. <span data-ttu-id="e1dee-121">선택 hello **사용** 확인란 tooenable hello에 대 한 백업 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="e1dee-121">Select hello **Enable** check box tooenable hello backup policy.</span></span> 
   6. <span data-ttu-id="e1dee-122">Hello 확인 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1dee-122">Click hello check icon</span></span> ![check-icon](./media/storsimple-take-backup/HCS_CheckIcon-include.png) <span data-ttu-id="e1dee-124">toosave hello 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="e1dee-124">toosave hello policy.</span></span>
      
      ![Add-backup-policy](./media/storsimple-take-backup/HCS_AddBackupPolicyWizard2M-include.png)
      
      <span data-ttu-id="e1dee-126">이제 볼륨 데이터의 예약된 백업을 만드는 백업 정책이 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e1dee-126">You now have a backup policy that will create scheduled backups of your volume data.</span></span>

<span data-ttu-id="e1dee-127">Hello 장치 구성을 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e1dee-127">You have completed hello device configuration.</span></span> 

<span data-ttu-id="e1dee-128">![동영상 사용 가능](./media/storsimple-take-backup/Video_icon.png) **동영상 사용 가능**</span><span class="sxs-lookup"><span data-stu-id="e1dee-128">![Video available](./media/storsimple-take-backup/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="e1dee-129">toowatch 보여 주는 비디오에서 StorSimple 백업 tootake 클릭 방법을 [여기](https://azure.microsoft.com/documentation/videos/take-a-storsimple-backup/)합니다.</span><span class="sxs-lookup"><span data-stu-id="e1dee-129">toowatch a video that demonstrates how tootake a StorSimple backup, click [here](https://azure.microsoft.com/documentation/videos/take-a-storsimple-backup/).</span></span>

