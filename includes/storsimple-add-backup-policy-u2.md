<!--author=v-sharos last changed: 11/06/15-->

#### <a name="tooadd-a-storsimple-backup-policy"></a><span data-ttu-id="49c7e-101">tooadd StorSimple 백업 정책</span><span class="sxs-lookup"><span data-stu-id="49c7e-101">tooadd a StorSimple backup policy</span></span>
1. <span data-ttu-id="49c7e-102">Hello 장치에서 **빠른 시작** 페이지에서 hello **백업 정책** 탭 합니다. 그러면 toohello **백업 정책** 페이지.</span><span class="sxs-lookup"><span data-stu-id="49c7e-102">On hello device **Quick Start** page, click hello **Backup Policies** tab. This will take you toohello **Backup Policies** page.</span></span>
2. <span data-ttu-id="49c7e-103">Hello hello 페이지의 아래쪽에 있는 클릭 **추가** toostart hello 백업 정책 추가 마법사.</span><span class="sxs-lookup"><span data-stu-id="49c7e-103">At hello bottom of hello page, click **Add** toostart hello Add Backup Policy wizard.</span></span>
   
    ![백업 정책 1 추가](./media/storsimple-add-backup-policy-u2/AddBackupPolicy1.png)
3. <span data-ttu-id="49c7e-105">Hello에 **백업 정책 추가** 대화 상자의 **백업 정책 정의**, 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="49c7e-105">In hello **Add Backup Policy** dialog box, under **Define your backup policy**, do hello following:</span></span>
   
   1. <span data-ttu-id="49c7e-106">백업 정책 이름을 3~150자 사이로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="49c7e-106">Specify a backup policy name that contains between 3 and 150 characters.</span></span>
   2. <span data-ttu-id="49c7e-107">Hello 확인 하면 tooassign 클릭 하 여 하나 이상의 볼륨 toothis 백업 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="49c7e-107">Click hello check box(es) tooassign one or more volumes toothis backup policy.</span></span> <span data-ttu-id="49c7e-108">서로 다른 클라우드 서비스 공급자를 사용하는 볼륨을 선택할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="49c7e-108">Note that you cannot select volumes that use different cloud service providers.</span></span> <span data-ttu-id="49c7e-109">첫 번째 선택에 따라 여러 클라우드 서비스 공급자를 사용 하는 경우 클라우드 서비스 공급자 tooonly 속한 볼륨 hello 목록에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="49c7e-109">If you are using multiple cloud service providers, based on your first selection, hello list will show volumes belonging tooonly that cloud service provider.</span></span> <span data-ttu-id="49c7e-110">따라서 있습니다 toogroup 볼륨이 속해 있는 볼륨 스냅숏에서 tooa 단일 클라우드 서비스 공급자 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49c7e-110">This will allow you toogroup volumes belonging tooa single cloud service provider in a snapshot.</span></span>
   3. <span data-ttu-id="49c7e-111">Hello 화살표 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="49c7e-111">Click hello arrow icon</span></span> ![화살표 아이콘](./media/storsimple-add-backup-policy-u2/HCS_ArrowIcon-include.png) <span data-ttu-id="49c7e-113">toogo toohello 다음 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="49c7e-113">toogo toohello next page.</span></span>
      
      ![백업 정책 2 추가](./media/storsimple-add-backup-policy-u2/AddBackupPolicy2.png)
4. <span data-ttu-id="49c7e-115">아래 **일정 정의**, 다음 hello지 않습니다:</span><span class="sxs-lookup"><span data-stu-id="49c7e-115">Under **Define a schedule**, do hello following:</span></span>
   
   1. <span data-ttu-id="49c7e-116">Hello에 **백업 종류** 상자 **클라우드 스냅숏** 또는 **로컬 스냅숏** hello 드롭 다운 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="49c7e-116">In hello **Type of Backup** box, select **Cloud Snapshot** or **Local Snapshot** from hello drop-down list.</span></span>
   2. <span data-ttu-id="49c7e-117">Hello 백업 빈도 나타냅니다 (번호를 지정 하 고 눌러 **일** 또는 **주** hello 드롭 다운 목록에서).</span><span class="sxs-lookup"><span data-stu-id="49c7e-117">Indicate hello frequency of backups (specify a number and then choose **Days** or **Weeks** from hello drop-down list).</span></span>
   3. <span data-ttu-id="49c7e-118">보존 일정을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="49c7e-118">Enter a retention schedule.</span></span>
   4. <span data-ttu-id="49c7e-119">된 백업 정책 toobegin hello에 대 한 날짜와 시간을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="49c7e-119">Enter a time and date for hello backup policy toobegin.</span></span>  
   5. <span data-ttu-id="49c7e-120">Hello 확인 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="49c7e-120">Click hello check icon</span></span> ![확인 아이콘](./media/storsimple-add-backup-policy-u2/HCS_CheckIcon-include.png) <span data-ttu-id="49c7e-122">toosave hello 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="49c7e-122">toosave hello policy.</span></span>

<span data-ttu-id="49c7e-123">hello 새로 추가 된 정책 hello hello에서 테이블 형식 보기에 표시 됩니다 **백업 정책** 페이지.</span><span class="sxs-lookup"><span data-stu-id="49c7e-123">hello newly added policy will be displayed in hello tabular view on hello **Backup Policies** page.</span></span>

