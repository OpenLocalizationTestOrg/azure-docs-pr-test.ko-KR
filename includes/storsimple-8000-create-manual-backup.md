
<!--author=alkohli last changed: 01/20/2017-->

#### <a name="to-create-a-manual-backup"></a><span data-ttu-id="75798-101">수동 백업을 만들려면</span><span class="sxs-lookup"><span data-stu-id="75798-101">To create a manual backup</span></span>

1. <span data-ttu-id="75798-102">StorSimple 장치 관리자 서비스로 이동한 다음 **장치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75798-102">Go to your StorSimple Device Manager service and then click **Devices**.</span></span> <span data-ttu-id="75798-103">테이블 형식 장치 목록에서 장치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="75798-103">From the tabular listing of devices, select your device.</span></span> <span data-ttu-id="75798-104">**설정 >관리 > 백업 정책**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="75798-104">Go to **Settings > Manage > Backup policies**.</span></span>

2. <span data-ttu-id="75798-105">**백업 정책** 블레이드에는 백업하려는 볼륨에 대한 정책을 비롯한 테이블 형식의 모든 백업 정책이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="75798-105">The **Backup policies** blade lists all the backup policies in a tabular format, including the policy for the volume that you want to back up.</span></span> <span data-ttu-id="75798-106">백업하려는 볼륨과 연결된 정책을 선택하고 마우스 오른쪽 단추를 클릭하여 상황에 맞는 메뉴를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="75798-106">Select the policy associated with the volume you want to back up and right-click to invoke the context menu.</span></span> <span data-ttu-id="75798-107">드롭다운 목록에서 **지금 백업**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="75798-107">From the dropdown list, select **Back up now**.</span></span>

    ![수동 백업 만들기](./media/storsimple-8000-create-manual-backup/createmanualbu1.png)

3. <span data-ttu-id="75798-109">**지금 백업** 블레이드에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="75798-109">In the **Back up now** blade, do the following steps:</span></span>

    1. <span data-ttu-id="75798-110">**로컬** 스냅숏 또는 **클라우드** 스냅숏의 드롭다운 목록에서 적절한 **스냅숏 유형**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="75798-110">Choose the appropriate **Snapshot type** from the dropdown list: **Local** snapshot or **Cloud** snapshot.</span></span> <span data-ttu-id="75798-111">빠른 백업 또는 복원을 위해서는 로컬 스냅숏을, 데이터 복원력을 위해서는 클라우드 스냅숏을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="75798-111">Select local snapshot for fast backups or restores, and cloud snapshot for data resiliency.</span></span>

        ![수동 백업 만들기](./media/storsimple-8000-create-manual-backup/createmanualbu2.png)

    2. <span data-ttu-id="75798-113">**확인**을 클릭하면 스냅숏을 만들기 위한 작업이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="75798-113">Click **OK** to start a job to create a snapshot.</span></span> <span data-ttu-id="75798-114">작업이 성공적으로 만들어지면 페이지 맨 아래에 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="75798-114">You will see a notification at the top of the page after the job is successfully created.</span></span>

        ![수동 백업 만들기](./media/storsimple-8000-create-manual-backup/createmanualbu4.png)

    3. <span data-ttu-id="75798-116">작업을 모니터링하려면 알림을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="75798-116">To monitor the job, click the notification.</span></span> <span data-ttu-id="75798-117">작업 진행 상태를 볼 수 있는 **작업** 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="75798-117">This takes you to the **Jobs** blade where you can view the job progress.</span></span>


5. <span data-ttu-id="75798-118">백업 작업이 완료되면 **백업 카탈로그** 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="75798-118">After the backup job is finished, go to the **Backup catalog** tab.</span></span>

6. <span data-ttu-id="75798-119">적절한 장치, 백업 정책 및 시간 범위로 필터 선택을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="75798-119">Set the filter selections to the appropriate device, backup policy, and time range.</span></span> <span data-ttu-id="75798-120">카탈로그에 표시되는 백업 세트의 목록에 백업이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="75798-120">The backup should appear in the list of backup sets that is displayed in the catalog.</span></span>

