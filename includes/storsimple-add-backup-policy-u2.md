<!--author=v-sharos last changed: 11/06/15-->

#### <a name="to-add-a-storsimple-backup-policy"></a><span data-ttu-id="18dd4-101">StorSimple 백업 정책을 추가하려면</span><span class="sxs-lookup"><span data-stu-id="18dd4-101">To add a StorSimple backup policy</span></span>
1. <span data-ttu-id="18dd4-102">장치 **빠른 시작** 페이지에서 **백업 정책** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18dd4-102">On the device **Quick Start** page, click the **Backup Policies** tab.</span></span> <span data-ttu-id="18dd4-103">이렇게 하면 **백업 정책** 페이지로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="18dd4-103">This will take you to the **Backup Policies** page.</span></span>
2. <span data-ttu-id="18dd4-104">페이지의 아래쪽에서 **추가** 를 클릭하여 백업 정책 추가 마법사를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="18dd4-104">At the bottom of the page, click **Add** to start the Add Backup Policy wizard.</span></span>
   
    ![백업 정책 1 추가](./media/storsimple-add-backup-policy-u2/AddBackupPolicy1.png)
3. <span data-ttu-id="18dd4-106">**백업 정책 추가** 대화 상자의 **백업 정책 정의**에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="18dd4-106">In the **Add Backup Policy** dialog box, under **Define your backup policy**, do the following:</span></span>
   
   1. <span data-ttu-id="18dd4-107">백업 정책 이름을 3~150자 사이로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="18dd4-107">Specify a backup policy name that contains between 3 and 150 characters.</span></span>
   2. <span data-ttu-id="18dd4-108">이 백업 정책에 하나 이상의 볼륨을 할당하려면 확인란을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18dd4-108">Click the check box(es) to assign one or more volumes to this backup policy.</span></span> <span data-ttu-id="18dd4-109">서로 다른 클라우드 서비스 공급자를 사용하는 볼륨을 선택할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="18dd4-109">Note that you cannot select volumes that use different cloud service providers.</span></span> <span data-ttu-id="18dd4-110">첫 번째 선택에 따라 여러 클라우드 서비스 공급자를 사용하는 경우 목록에 해당 클라우드 서비스 공급자에 속하는 볼륨만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="18dd4-110">If you are using multiple cloud service providers, based on your first selection, the list will show volumes belonging to only that cloud service provider.</span></span> <span data-ttu-id="18dd4-111">이렇게 하면 스냅숏의 단일 클라우드 서비스 공급자에 속하는 볼륨을 그룹화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18dd4-111">This will allow you to group volumes belonging to a single cloud service provider in a snapshot.</span></span>
   3. <span data-ttu-id="18dd4-112">화살표 아이콘</span><span class="sxs-lookup"><span data-stu-id="18dd4-112">Click the arrow icon</span></span> ![화살표 아이콘](./media/storsimple-add-backup-policy-u2/HCS_ArrowIcon-include.png) <span data-ttu-id="18dd4-114">을 클릭하여 다음 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="18dd4-114">to go to the next page.</span></span>
      
      ![백업 정책 2 추가](./media/storsimple-add-backup-policy-u2/AddBackupPolicy2.png)
4. <span data-ttu-id="18dd4-116">**일정 정의**에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="18dd4-116">Under **Define a schedule**, do the following:</span></span>
   
   1. <span data-ttu-id="18dd4-117">**백업 유형** 상자의 드롭다운 목록에서 **클라우드 스냅숏** 또는 **로컬 스냅숏**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="18dd4-117">In the **Type of Backup** box, select **Cloud Snapshot** or **Local Snapshot** from the drop-down list.</span></span>
   2. <span data-ttu-id="18dd4-118">백업 빈도를 표시합니다. 숫자를 지정한 다음 드롭다운 목록에서 **일** 또는 **주**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="18dd4-118">Indicate the frequency of backups (specify a number and then choose **Days** or **Weeks** from the drop-down list).</span></span>
   3. <span data-ttu-id="18dd4-119">보존 일정을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="18dd4-119">Enter a retention schedule.</span></span>
   4. <span data-ttu-id="18dd4-120">백업 정책의 시작 시간과 날짜를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="18dd4-120">Enter a time and date for the backup policy to begin.</span></span>  
   5. <span data-ttu-id="18dd4-121">확인 아이콘 </span><span class="sxs-lookup"><span data-stu-id="18dd4-121">Click the check icon</span></span> ![확인 아이콘](./media/storsimple-add-backup-policy-u2/HCS_CheckIcon-include.png) <span data-ttu-id="18dd4-123">을 클릭하여 정책을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="18dd4-123">to save the policy.</span></span>

<span data-ttu-id="18dd4-124">새로 추가된 정책은 **백업 정책** 페이지입에서 테이블 형식 뷰로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="18dd4-124">The newly added policy will be displayed in the tabular view on the **Backup Policies** page.</span></span>

