<!--author=alkohli last changed: 01/12/17-->

### <a name="to-take-a-backup"></a><span data-ttu-id="dc3bc-101">백업을 수행하려면</span><span class="sxs-lookup"><span data-stu-id="dc3bc-101">To take a backup</span></span>

1. <span data-ttu-id="dc3bc-102">StorSimple 장치 관리자 서비스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3bc-102">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="dc3bc-103">테이블 형식 장치 목록에서 장치를 선택하고 클릭한 후 **모든 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3bc-103">From the tabular listing of devices, select and click your device and then click **All settings**.</span></span> <span data-ttu-id="dc3bc-104">**설정** 블레이드에서 **설정 > 관리 > 백업 정책**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3bc-104">In the **Settings** blade, go to **Settings > Manage > Backup policy**.</span></span>

    ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu1.png)

2. <span data-ttu-id="dc3bc-106">**백업 정책** 블레이드에서 **+ 정책 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3bc-106">In the **Backup policy** blade, click **+ Add policy**.</span></span>

    ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu2.png)

3. <span data-ttu-id="dc3bc-108">**백업 정책 만들기** 블레이드에서 백업 정책 이름을 3~150자 사이로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3bc-108">In the **Create backup policy** blade, supply a name that contains between 3 and 150 characters for your backup policy.</span></span>

4. <span data-ttu-id="dc3bc-109">백업할 볼륨을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3bc-109">Select the volumes to be backed up.</span></span> <span data-ttu-id="dc3bc-110">볼륨을 두 개 이상 선택하면 충돌에 일관성이 있는 백업을 만들기 위해 볼륨이 그룹화됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc3bc-110">If you select more than one volume, these volumes are grouped together to create a crash-consistent backup.</span></span>

    ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu4.png)

5. <span data-ttu-id="dc3bc-112">**첫 번째 일정 추가** 블레이드에서:</span><span class="sxs-lookup"><span data-stu-id="dc3bc-112">On **Add first schedule** blade:</span></span>

    1. <span data-ttu-id="dc3bc-113">백업 유형을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3bc-113">Select the type of backup.</span></span> <span data-ttu-id="dc3bc-114">빠른 복원을 위해서는 **로컬** 스냅숏을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3bc-114">For faster restores, select **Local** snapshot.</span></span> <span data-ttu-id="dc3bc-115">데이터 복원력을 위해서는 **클라우드** 스냅숏을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3bc-115">For data resiliency, select **Cloud** snapshot.</span></span>
    2. <span data-ttu-id="dc3bc-116">백업 빈도를 분, 시간, 일 또는 주 단위로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3bc-116">Specify the backup frequency in minutes, hours, days, or weeks.</span></span>
    3. <span data-ttu-id="dc3bc-117">보존 시간을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3bc-117">Select a retention time.</span></span> <span data-ttu-id="dc3bc-118">보존 선택 항목은 백업 빈도에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="dc3bc-118">The retention choices depend on the backup frequency.</span></span> <span data-ttu-id="dc3bc-119">예를 들어 일별 정책의 경우 보존을 주 단위로 지정하고 월별 정책의 경우 월 단위로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc3bc-119">For example, for a daily policy, the retention can be specified in weeks, whereas retention for a monthly policy is in months.</span></span>
    4. <span data-ttu-id="dc3bc-120">백업 정책의 시작 시간과 날짜를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3bc-120">Select the starting time and date for the backup policy.</span></span>
    5. <span data-ttu-id="dc3bc-121">**확인**을 클릭하여 백업 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dc3bc-121">Click **OK** to create the backup policy.</span></span>

        ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu5.png) 

6. <span data-ttu-id="dc3bc-123">**만들기**를 클릭하면 백업 정책 만들기가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc3bc-123">Click **Create** to start the backup policy creation.</span></span> <span data-ttu-id="dc3bc-124">백업 정책이 성공적으로 만들어지면 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc3bc-124">You are notified when the backup policy is successfully created.</span></span> <span data-ttu-id="dc3bc-125">백업 정책 목록도 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc3bc-125">The list of backup policies is also updated.</span></span>
      
      ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu9.png)
      
      <span data-ttu-id="dc3bc-127">이제 볼륨 데이터의 예약된 백업을 만드는 백업 정책이 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="dc3bc-127">You now have a backup policy that creates scheduled backups of your volume data.</span></span>




