<!--author=alkohli last changed: 02/10/17-->

#### <a name="to-add-a-storsimple-backup-policy"></a><span data-ttu-id="fb228-101">StorSimple 백업 정책을 추가하려면</span><span class="sxs-lookup"><span data-stu-id="fb228-101">To add a StorSimple backup policy</span></span>

1. <span data-ttu-id="fb228-102">StorSimple 장치로 이동하고 **백업 정책**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fb228-102">Go to your StorSimple device and click **Backup policy**.</span></span>

2. <span data-ttu-id="fb228-103">**백업 정책** 블레이드의 명령 모음에서 **+ 정책 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fb228-103">In the **Backup policy** blade, click **+ Add policy** from the command bar.</span></span>
   
    ![백업 정책 추가](./media/storsimple-8000-add-backup-policy-u2/addbupol1.png)

3. <span data-ttu-id="fb228-105">**백업 정책 만들기** 블레이드에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fb228-105">In the **Create backup policy** blade, do the following steps:</span></span>
   
   1. <span data-ttu-id="fb228-106">선택한 장치에 따라 **장치 선택**이 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="fb228-106">**Select device** is automatically populated based on the device you selected.</span></span>
   
   2. <span data-ttu-id="fb228-107">백업 **정책 이름**을 3~150자 사이로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fb228-107">Specify a backup **Policy name** that contains between 3 and 150 characters.</span></span> <span data-ttu-id="fb228-108">정책을 만든 후에는 정책 이름을 바꿀 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fb228-108">Once the policy is created, you cannot rename the policy.</span></span>
       
   3. <span data-ttu-id="fb228-109">이 백업 정책에 볼륨을 할당하려면 선택 **볼륨 추가**를 선택한 후 테이블 형식 볼륨 목록에서 해당 확인란을 클릭하여 이 백업 정책에 하나 이상의 볼륨을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="fb228-109">To assign volumes to this backup policy, select **Add volumes** and then from the tabular listing of volumes, click the check box(es) to assign one or more volumes to this backup policy.</span></span>

       ![백업 정책 추가](./media/storsimple-8000-add-backup-policy-u2/addbupol2.png)

   4. <span data-ttu-id="fb228-111">이 백업 정책에 대한 일정을 정의하려면 **첫 번째 일정**을 클릭한 후 다음 매개 변수를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="fb228-111">To define a schedule for this backup policy, click **First schedule** and then modify the following parameters:</span></span>

       ![백업 정책 추가](./media/storsimple-8000-add-backup-policy-u2/addbupol3.png)

       1. <span data-ttu-id="fb228-113">**스냅숏 유형**으로 **클라우드** 또는 **로컬**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fb228-113">For **Snapshot type**, select **Cloud** or **Local**.</span></span>

       2. <span data-ttu-id="fb228-114">백업 빈도를 표시합니다. 숫자를 지정한 다음 드롭다운 목록에서 **일** 또는 **주**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fb228-114">Indicate the frequency of backups (specify a number and then choose **Days** or **Weeks** from the drop-down list.</span></span>

       3. <span data-ttu-id="fb228-115">보존 일정을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fb228-115">Enter a retention schedule.</span></span>

       4. <span data-ttu-id="fb228-116">백업 정책의 시작 시간과 날짜를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fb228-116">Enter a time and date for the backup policy to begin.</span></span>

       5. <span data-ttu-id="fb228-117">일정을 정의하려면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fb228-117">Click **OK** to define the schedule.</span></span>

   5. <span data-ttu-id="fb228-118">백업 정책을 만들려면 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fb228-118">Click **Create** to create a backup policy.</span></span>

       ![백업 정책 추가](./media/storsimple-8000-add-backup-policy-u2/addbupol4.png)
   
   6. <span data-ttu-id="fb228-120">백업 정책이 만들어지면 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb228-120">You are notified when the backup policy is created.</span></span> <span data-ttu-id="fb228-121">새로 추가된 정책은 **백업 정책** 블레이드에서 테이블 형식 뷰로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb228-121">The newly added policy is displayed in the tabular view on the **Backup Policy** blade.</span></span>

       ![백업 정책 추가](./media/storsimple-8000-add-backup-policy-u2/addbupol7.png)

