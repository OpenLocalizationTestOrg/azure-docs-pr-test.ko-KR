<!--author=alkohli last changed: 08/04/17-->

#### <a name="to-install-an-update-from-the-azure-portal"></a><span data-ttu-id="acc98-101">Azure 포털에서 업데이트를 설치하려면</span><span class="sxs-lookup"><span data-stu-id="acc98-101">To install an update from the Azure portal</span></span>

1. <span data-ttu-id="acc98-102">StorSimple 서비스 페이지에서 장치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="acc98-102">On the StorSimple service page, select your device.</span></span>

    ![장치 선택](./media/storsimple-8000-install-update5-via-portal/update1.png)

2. <span data-ttu-id="acc98-104">**장치 설정** > **장치 업데이트**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="acc98-104">Navigate to **Device settings** > **Device updates**.</span></span>

    ![장치 업데이트 클릭](./media/storsimple-8000-install-update5-via-portal/update2.png)

2. <span data-ttu-id="acc98-106">새 업데이트를 사용할 수 있는 경우 알림이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="acc98-106">A notification appears if new updates are available.</span></span> <span data-ttu-id="acc98-107">또는 **장치 업데이트** 블레이드에서 **업데이트 검색**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="acc98-107">Alternatively, in the **Device updates** blade, click **Scan Updates**.</span></span> <span data-ttu-id="acc98-108">사용 가능한 업데이트를 검색하는 작업이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="acc98-108">A job is created to scan for available updates.</span></span> <span data-ttu-id="acc98-109">작업이 성공적으로 완료되면 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="acc98-109">You are notified when the job completes successfully.</span></span>

    ![장치 업데이트 클릭](./media/storsimple-8000-install-update5-via-portal/update3.png)

3. <span data-ttu-id="acc98-111">장치에 업데이트를 적용하기 전에 릴리스 정보를 검토하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="acc98-111">We recommend that you review the release notes before you apply an update on your device.</span></span> <span data-ttu-id="acc98-112">업데이트를 적용하려면 **업데이트 설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="acc98-112">To apply updates, click **Install updates**.</span></span> <span data-ttu-id="acc98-113">**Confirm regular updates(정기 업데이트 확인)** 블레이드에서 업데이트를 적용하기 전에 완료할 필수 구성 요소를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="acc98-113">In the **Confirm regular updates** blade, review the prerequisites to complete before you apply updates.</span></span> <span data-ttu-id="acc98-114">장치를 업데이트할 준비가 되었음을 나타내는 확인란을 선택한 후 **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="acc98-114">Select the checkbox to indicate that you are ready to update the device and then click **Install**.</span></span>

    ![장치 업데이트 클릭](./media/storsimple-8000-install-update5-via-portal/update4.png)

6. <span data-ttu-id="acc98-116">일련의 필수 조건 검사가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="acc98-116">A set of prerequisite checks starts.</span></span> <span data-ttu-id="acc98-117">이들 검사는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="acc98-117">These checks include:</span></span>
   
   * <span data-ttu-id="acc98-118">**컨트롤러 상태 검사** 장치 컨트롤러가 정상이고 온라인에 있는지 모두 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="acc98-118">**Controller health checks** to verify that both the device controllers are healthy and online.</span></span>
   * <span data-ttu-id="acc98-119">**하드웨어 구성 요소 상태 검사** StorSimple 장치에서 모든 하드웨어 구성 요소가 정상인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="acc98-119">**Hardware component health checks** to verify that all the hardware components on your StorSimple device are healthy.</span></span>
   * <span data-ttu-id="acc98-120">**데이터 0 검사** 데이터 0이 장치에서 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="acc98-120">**DATA 0 checks** to verify that DATA 0 is enabled on your device.</span></span> <span data-ttu-id="acc98-121">이 인터페이스를 사용하지 않는 경우 다음을 사용하도록 설정하고 다시 시도해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="acc98-121">If this interface is not enabled, you must enable it and then retry.</span></span>

    <span data-ttu-id="acc98-122">모든 검사가 성공적으로 완료된 경우에만 업데이트가 다운로드되어 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="acc98-122">The update is downloaded and installed only if all the checks are successfully completed.</span></span> <span data-ttu-id="acc98-123">검사가 진행 중인 경우 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="acc98-123">You are notified when the checks are in progress.</span></span> <span data-ttu-id="acc98-124">사전 검사가 실패하면 실패한 이유가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="acc98-124">If the prechecks fail, then you will be provided with the reasons for failure.</span></span> <span data-ttu-id="acc98-125">이러한 문제를 해결한 다음 작업을 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="acc98-125">Address those issues and then retry the operation.</span></span> <span data-ttu-id="acc98-126">혼자서 이러한 문제를 해결할 수 없는 경우 Microsoft 지원에 문의해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acc98-126">You may need to contact Microsoft Support if you cannot address these issues by yourself.</span></span>

7. <span data-ttu-id="acc98-127">사전 검사를 성공적으로 완료한 후 업데이트 작업이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="acc98-127">After the prechecks are successfully completed, an update job is created.</span></span> <span data-ttu-id="acc98-128">업데이트 작업이 성공적으로 만들어지면 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="acc98-128">You are notified when the update job is successfully created.</span></span>
   
    ![업데이트 작업 만들기](./media/storsimple-8000-install-update5-via-portal/update6.png)
   
    <span data-ttu-id="acc98-130">그런 다음 업데이트가 장치에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="acc98-130">The update is then applied on your device.</span></span>

9. <span data-ttu-id="acc98-131">업데이트를 완료하는 데 몇 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="acc98-131">The update takes a few hours to complete.</span></span> <span data-ttu-id="acc98-132">업데이트 작업을 선택하고 **세부 정보** 를 클릭하여 언제든지 작업의 세부 정보를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="acc98-132">Select the update job and click **Details** to view the details of the job at any time.</span></span>

    ![업데이트 작업 만들기](./media/storsimple-8000-install-update5-via-portal/update8.png)

     <span data-ttu-id="acc98-134">**장치 설정 > 작업**에서 업데이트 작업의 진행률을 모니터링할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acc98-134">You can also monitor the progress of the update job from **Device settings > Jobs**.</span></span> <span data-ttu-id="acc98-135">**작업** 블레이드에서 업데이트 진행률을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acc98-135">On the **Jobs** blade, you can see the update progress.</span></span>

     ![업데이트 작업 만들기](./media/storsimple-8000-install-update5-via-portal/update7.png)

10. <span data-ttu-id="acc98-137">작업이 완료되면 **장치 설정 > 장치 업데이트**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="acc98-137">After the job is complete, navigate to the **Device settings > Device updates**.</span></span> <span data-ttu-id="acc98-138">이제 소프트웨어 버전이 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="acc98-138">The software version should now be updated.</span></span>

