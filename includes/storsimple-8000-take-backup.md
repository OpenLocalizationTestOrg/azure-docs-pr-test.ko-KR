<!--author=alkohli last changed: 01/12/17-->

### <a name="tootake-a-backup"></a><span data-ttu-id="4eadd-101">tootake 백업</span><span class="sxs-lookup"><span data-stu-id="4eadd-101">tootake a backup</span></span>

1. <span data-ttu-id="4eadd-102">Tooyour StorSimple 장치 관리자 서비스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eadd-102">Go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="4eadd-103">hello 테이블 형식 목록이 장치를 선택 하 고 장치를 클릭 하 고 클릭 **모든 설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="4eadd-103">From hello tabular listing of devices, select and click your device and then click **All settings**.</span></span> <span data-ttu-id="4eadd-104">Hello에 **설정** 블레이드에서 너무 이동**설정 > 관리 > 백업 정책**합니다.</span><span class="sxs-lookup"><span data-stu-id="4eadd-104">In hello **Settings** blade, go too**Settings > Manage > Backup policy**.</span></span>

    ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu1.png)

2. <span data-ttu-id="4eadd-106">Hello에 **백업 정책** 블레이드에서 클릭 **+ 정책 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="4eadd-106">In hello **Backup policy** blade, click **+ Add policy**.</span></span>

    ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu2.png)

3. <span data-ttu-id="4eadd-108">Hello에 **백업 정책을 만들려면** 블레이드, 백업 정책에 대 한 3 ~ 150 자 사이 포함 하는 이름 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eadd-108">In hello **Create backup policy** blade, supply a name that contains between 3 and 150 characters for your backup policy.</span></span>

4. <span data-ttu-id="4eadd-109">백업 hello 볼륨 toobe를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eadd-109">Select hello volumes toobe backed up.</span></span> <span data-ttu-id="4eadd-110">하나 이상의 볼륨을 선택 하면 이러한 볼륨은 그룹화 된 함께 toocreate 크래시 일관성이 있는 백업을입니다.</span><span class="sxs-lookup"><span data-stu-id="4eadd-110">If you select more than one volume, these volumes are grouped together toocreate a crash-consistent backup.</span></span>

    ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu4.png)

5. <span data-ttu-id="4eadd-112">**첫 번째 일정 추가** 블레이드에서:</span><span class="sxs-lookup"><span data-stu-id="4eadd-112">On **Add first schedule** blade:</span></span>

    1. <span data-ttu-id="4eadd-113">Hello 백업 유형을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eadd-113">Select hello type of backup.</span></span> <span data-ttu-id="4eadd-114">빠른 복원을 위해서는 **로컬** 스냅숏을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4eadd-114">For faster restores, select **Local** snapshot.</span></span> <span data-ttu-id="4eadd-115">데이터 복원력을 위해서는 **클라우드** 스냅숏을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4eadd-115">For data resiliency, select **Cloud** snapshot.</span></span>
    2. <span data-ttu-id="4eadd-116">분, 시간, 일 또는 주에 hello 백업 빈도 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eadd-116">Specify hello backup frequency in minutes, hours, days, or weeks.</span></span>
    3. <span data-ttu-id="4eadd-117">보존 시간을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4eadd-117">Select a retention time.</span></span> <span data-ttu-id="4eadd-118">hello 보존 선택 hello 백업 빈도에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="4eadd-118">hello retention choices depend on hello backup frequency.</span></span> <span data-ttu-id="4eadd-119">예를 들어 일별 정책의 경우에 대 한 hello 보존 수 수 주 단위로 지정 월별 정책의 경우 월 단위로.</span><span class="sxs-lookup"><span data-stu-id="4eadd-119">For example, for a daily policy, hello retention can be specified in weeks, whereas retention for a monthly policy is in months.</span></span>
    4. <span data-ttu-id="4eadd-120">Hello 백업 정책에 대 한 날짜 및 시간을 시작 하는 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eadd-120">Select hello starting time and date for hello backup policy.</span></span>
    5. <span data-ttu-id="4eadd-121">클릭 **확인** toocreate hello 백업 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="4eadd-121">Click **OK** toocreate hello backup policy.</span></span>

        ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu5.png) 

6. <span data-ttu-id="4eadd-123">클릭 **만들기** toostart hello 백업 정책 만들기.</span><span class="sxs-lookup"><span data-stu-id="4eadd-123">Click **Create** toostart hello backup policy creation.</span></span> <span data-ttu-id="4eadd-124">Hello 백업 정책이 성공적으로 만들어지면 알림이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4eadd-124">You are notified when hello backup policy is successfully created.</span></span> <span data-ttu-id="4eadd-125">백업 정책 hello 목록도 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4eadd-125">hello list of backup policies is also updated.</span></span>
      
      ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu9.png)
      
      <span data-ttu-id="4eadd-127">이제 볼륨 데이터의 예약된 백업을 만드는 백업 정책이 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4eadd-127">You now have a backup policy that creates scheduled backups of your volume data.</span></span>




