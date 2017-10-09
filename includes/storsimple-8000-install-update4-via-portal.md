<!--author=alkohli last changed: 07/07/17-->

#### <a name="tooinstall-an-update-from-hello-azure-portal"></a><span data-ttu-id="73161-101">tooinstall hello Azure 포털의 업데이트</span><span class="sxs-lookup"><span data-stu-id="73161-101">tooinstall an update from hello Azure portal</span></span>

1. <span data-ttu-id="73161-102">Hello StorSimple 서비스 페이지에서 장치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="73161-102">On hello StorSimple service page, select your device.</span></span>

    ![장치 선택](./media/storsimple-8000-install-update4-via-portal/update1.png)

2. <span data-ttu-id="73161-104">너무 이동**장치 설정** > **장치 업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="73161-104">Navigate too**Device settings** > **Device updates**.</span></span>

    ![장치 업데이트 클릭](./media/storsimple-8000-install-update4-via-portal/update2.png)

2. <span data-ttu-id="73161-106">새 업데이트를 사용할 수 있는 경우 알림이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="73161-106">A notification appears if new updates are available.</span></span> <span data-ttu-id="73161-107">Hello 또는에서 **장치 업데이트** 블레이드에서 클릭 **업데이트 스캔**합니다.</span><span class="sxs-lookup"><span data-stu-id="73161-107">Alternatively, in hello **Device updates** blade, click **Scan Updates**.</span></span> <span data-ttu-id="73161-108">작업은 사용 가능한 업데이트에 대 한 tooscan을 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="73161-108">A job is created tooscan for available updates.</span></span> <span data-ttu-id="73161-109">Hello 작업이 성공적으로 완료 되었을 때 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="73161-109">You are notified when hello job completes successfully.</span></span>

    ![장치 업데이트 클릭](./media/storsimple-8000-install-update4-via-portal/update3.png)

3. <span data-ttu-id="73161-111">장치에 대 한 업데이트를 적용 하기 전에 hello 릴리스 정보를 검토 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="73161-111">We recommend that you review hello release notes before you apply an update on your device.</span></span> <span data-ttu-id="73161-112">tooapply 업데이트 클릭 **업데이트 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="73161-112">tooapply updates, click **Install updates**.</span></span> <span data-ttu-id="73161-113">Hello에 **정기적으로 업데이트 확인** 블레이드를 검토 hello 필수 구성 요소 toocomplete 업데이트를 적용 하기 전에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73161-113">In hello **Confirm regular updates** blade, review hello prerequisites toocomplete before you apply updates.</span></span> <span data-ttu-id="73161-114">Hello 확인란 tooindicate 준비 tooupdate hello 장치 하 고을 클릭 한 다음 선택 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="73161-114">Select hello checkbox tooindicate that you are ready tooupdate hello device and then click **Install**.</span></span>

    ![장치 업데이트 클릭](./media/storsimple-8000-install-update4-via-portal/update4.png)

6. <span data-ttu-id="73161-116">일련의 필수 조건 검사가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="73161-116">A set of prerequisite checks starts.</span></span> <span data-ttu-id="73161-117">이들 검사는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="73161-117">These checks include:</span></span>
   
   * <span data-ttu-id="73161-118">**컨트롤러 상태 검사** tooverify 장치 컨트롤러를 hello 둘 다는 정상 상태이 고 온라인입니다.</span><span class="sxs-lookup"><span data-stu-id="73161-118">**Controller health checks** tooverify that both hello device controllers are healthy and online.</span></span>
   * <span data-ttu-id="73161-119">**하드웨어 구성 요소 상태 검사** tooverify StorSimple 장치에서 하드웨어 구성 요소를 hello 모든 요소가 정상 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="73161-119">**Hardware component health checks** tooverify that all hello hardware components on your StorSimple device are healthy.</span></span>
   * <span data-ttu-id="73161-120">**데이터 0 확인** tooverify 장치에서 DATA 0은 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="73161-120">**DATA 0 checks** tooverify that DATA 0 is enabled on your device.</span></span> <span data-ttu-id="73161-121">이 인터페이스를 사용하지 않는 경우 다음을 사용하도록 설정하고 다시 시도해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="73161-121">If this interface is not enabled, you must enable it and then retry.</span></span>

    <span data-ttu-id="73161-122">hello 업데이트가 다운로드 되 고 모든 hello 검사를 성공적으로 완료 하는 경우에 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="73161-122">hello update is downloaded and installed only if all hello checks are successfully completed.</span></span> <span data-ttu-id="73161-123">Hello 검사가 진행 되는 경우 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="73161-123">You are notified when hello checks are in progress.</span></span> <span data-ttu-id="73161-124">Hello prechecks 실패 하는 경우 다음 됩니다 표시 hello 실패 이유입니다.</span><span class="sxs-lookup"><span data-stu-id="73161-124">If hello prechecks fail, then you will be provided with hello reasons for failure.</span></span> <span data-ttu-id="73161-125">그러한 문제를 해결 하 고 hello 작업을 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="73161-125">Address those issues and then retry hello operation.</span></span> <span data-ttu-id="73161-126">혼자서 이러한 문제를 해결 수 없는 경우 Microsoft 지원 toocontact을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73161-126">You may need toocontact Microsoft Support if you cannot address these issues by yourself.</span></span>

7. <span data-ttu-id="73161-127">Hello prechecks를 성공적으로 완료 한 후 업데이트 작업이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="73161-127">After hello prechecks are successfully completed, an update job is created.</span></span> <span data-ttu-id="73161-128">Hello 업데이트 작업이 성공적으로 만들어지면 알림이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="73161-128">You are notified when hello update job is successfully created.</span></span>
   
    ![업데이트 작업 만들기](./media/storsimple-8000-install-update4-via-portal/update6.png)
   
    <span data-ttu-id="73161-130">hello 업데이트를 장치에 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="73161-130">hello update is then applied on your device.</span></span>

9. <span data-ttu-id="73161-131">hello 업데이트는 몇 시간 toocomplete 합니다.</span><span class="sxs-lookup"><span data-stu-id="73161-131">hello update takes a few hours toocomplete.</span></span> <span data-ttu-id="73161-132">Hello 업데이트 작업을 선택 하 고 클릭 **세부 정보** 언제 든 지 hello 작업의 tooview hello 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="73161-132">Select hello update job and click **Details** tooview hello details of hello job at any time.</span></span>

    ![업데이트 작업 만들기](./media/storsimple-8000-install-update4-via-portal/update8.png)

     <span data-ttu-id="73161-134">Hello 업데이트 작업에서의 hello 진행률을 모니터링할 수 있습니다 **장치 설정 > 작업**합니다.</span><span class="sxs-lookup"><span data-stu-id="73161-134">You can also monitor hello progress of hello update job from **Device settings > Jobs**.</span></span> <span data-ttu-id="73161-135">Hello에 **작업** 블레이드에서 hello 업데이트 진행률을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73161-135">On hello **Jobs** blade, you can see hello update progress.</span></span>

     ![업데이트 작업 만들기](./media/storsimple-8000-install-update4-via-portal/update7.png)

10. <span data-ttu-id="73161-137">Hello 작업이 완료 되 면 이동 toohello **장치 설정 > 장치 업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="73161-137">After hello job is complete, navigate toohello **Device settings > Device updates**.</span></span> <span data-ttu-id="73161-138">이제 hello 소프트웨어 버전을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="73161-138">hello software version should now be updated.</span></span>

    ![업데이트 작업 만들기](./media/storsimple-8000-install-update4-via-portal/update9.png)

