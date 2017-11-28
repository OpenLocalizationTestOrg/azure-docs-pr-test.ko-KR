<!--author=alkohli last changed: 11/07/16 -->

#### <a name="to-install-updates-via-the-azure-portal"></a><span data-ttu-id="79f01-101">Azure Portal을 통해 업데이트를 설치하려면</span><span class="sxs-lookup"><span data-stu-id="79f01-101">To install updates via the Azure portal</span></span>

1. <span data-ttu-id="79f01-102">StorSimple 장치 관리자를 이동하고 **장치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="79f01-102">Go to your StorSimple Device Manager and select **Devices**.</span></span> <span data-ttu-id="79f01-103">서비스에 연결된 장치 목록에서 업데이트하려는 장치를 선택하고 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79f01-103">From the list of devices connected to your service, select and click the device you want to update.</span></span> 

    ![장치 업데이트](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate1m.png) 

2. <span data-ttu-id="79f01-105">**설정** 블레이드에서 **장치 업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79f01-105">In the **Settings** blade, click **Device updates**.</span></span> 

    ![장치 업데이트](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate2m.png)  

3. <span data-ttu-id="79f01-107">소프트웨어 업데이트를 사용할 수 있는 경우 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="79f01-107">You see a message if the software updates are available.</span></span> <span data-ttu-id="79f01-108">업데이트를 확인하려면 **스캔**을 클릭할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79f01-108">To check for updates, you can also click **Scan**.</span></span>

    ![장치 업데이트](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate3m.png)

    <span data-ttu-id="79f01-110">스캔이 시작되고 성공적으로 완료되면 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="79f01-110">You will be notified when the scan starts and completes successfully.</span></span>

    ![장치 업데이트](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate5m.png)

4. <span data-ttu-id="79f01-112">업데이트가 스캔되면 **업데이트 다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79f01-112">Once the updates are scanned, click **Download updates**.</span></span> 

    ![장치 업데이트](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate6m.png)

5. <span data-ttu-id="79f01-114">**새 업데이트** 블레이드에서 업데이트를 다운로드한 후에 정보를 검토하고 설치를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79f01-114">In the **New updates** blade, review the information that after the updates are downloaded, you need to confirm the installation.</span></span> <span data-ttu-id="79f01-115">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79f01-115">Click **OK**.</span></span>

    ![장치 업데이트](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate7m.png)

6. <span data-ttu-id="79f01-117">업로드가 시작되고 성공적으로 완료되면 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="79f01-117">You are notified when the upload starts and completes successfully.</span></span>

     ![장치 업데이트](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate8m.png)

5. <span data-ttu-id="79f01-119">**장치 업데이트** 블레이드에서 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="79f01-119">In the **Device updates** blade, click **Install**.</span></span>

     ![장치 업데이트](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate11m.png)   

6. <span data-ttu-id="79f01-121">**새 업데이트** 블레이드에서 업데이트가 중단되었다는 경고가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="79f01-121">In the **New updates** blade, you are warned that the update is disruptive.</span></span> <span data-ttu-id="79f01-122">가상 배열이 단일 노드 장치인 경우 장치가 업데이트된 후에 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="79f01-122">As virtual array is a single node device, the device restarts after it is updated.</span></span> <span data-ttu-id="79f01-123">따라서 진행 중인 모든 IO가 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="79f01-123">This disrupts any IO in progress.</span></span> <span data-ttu-id="79f01-124">**확인**을 클릭하여 업데이트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="79f01-124">Click **OK** to install the updates.</span></span> 

    ![장치 업데이트](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate12m.png) 

7. <span data-ttu-id="79f01-126">설치 작업이 시작될 때 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="79f01-126">You are notified when the install job starts.</span></span> 

    ![장치 업데이트](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate13m.png)

8.  <span data-ttu-id="79f01-128">설치 작업을 성공적으로 완료한 후에 **장치 업데이트** 블레이드에서 **작업 보기** 링크를 클릭하여 설치를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="79f01-128">After the install job completes successfully, click **View Job** link in the **Device updates** blade to monitor the installation.</span></span> 

    ![장치 업데이트](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate15m.png)

    <span data-ttu-id="79f01-130">**업데이트 설치** 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="79f01-130">This takes you to the **Install Updates** blade.</span></span> <span data-ttu-id="79f01-131">이 작업에 대한 자세한 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="79f01-131">You can view detailed information about the job here.</span></span>

    ![장치 업데이트](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate16m.png)

9. <span data-ttu-id="79f01-133">업데이트가 성공적으로 설치된 후에 장치 업데이트 블레이드에서 이 효과에 대한 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="79f01-133">After the updates are successfully installed, you see a message to this effect in the Device updates blade.</span></span> <span data-ttu-id="79f01-134">소프트웨어 버전도 **10.0.10288.0**으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="79f01-134">The software version also changes to **10.0.10288.0**.</span></span> 

    ![장치 업데이트](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate17m.png)