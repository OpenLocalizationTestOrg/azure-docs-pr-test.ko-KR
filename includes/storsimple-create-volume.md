<!--author=SharS last changed: 02/04/2016-->

#### <a name="toocreate-a-volume"></a><span data-ttu-id="f7149-101">toocreate 볼륨</span><span class="sxs-lookup"><span data-stu-id="f7149-101">toocreate a volume</span></span>
1. <span data-ttu-id="f7149-102">Hello 장치에서 **빠른 시작** 페이지 **볼륨 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7149-102">On hello device **Quick Start** page, click **Add a volume**.</span></span> <span data-ttu-id="f7149-103">Hello 추가 볼륨 마법사를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f7149-103">This starts hello Add a volume wizard.</span></span>
2. <span data-ttu-id="f7149-104">Hello 볼륨 마법사를 아래에서 추가 **기본 설정**, 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f7149-104">In hello Add a volume wizard, under **Basic Settings**, do hello following:</span></span>
   
   1. <span data-ttu-id="f7149-105">볼륨의 **이름** 을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f7149-105">Supply a **Name** for your volume.</span></span>
   2. <span data-ttu-id="f7149-106">Hello 지정 **프로 비전 된 용량** GB 또는 TB에서 볼륨에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7149-106">Specify hello **Provisioned Capacity** for your volume in GB or TB.</span></span> <span data-ttu-id="f7149-107">볼륨 용량은 hello 물리적 장치에 대 한 1GB ~ 64TB 사이 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7149-107">hello volume capacity must be between 1 GB and 64 TB for a physical device.</span></span>
   3. <span data-ttu-id="f7149-108">Hello 드롭 다운 목록에서 선택 hello **사용 유형을** 볼륨에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7149-108">On hello drop-down list, select hello **Usage Type** for your volume.</span></span> 
   4. <span data-ttu-id="f7149-109">이 볼륨 않는 아카이브 데이터를 사용 하는 경우 선택 hello **자주 액세스 하지 않는 아카이브 데이터에이 볼륨 사용** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7149-109">If you are using this volume for archival data, select hello **Use this volume for less frequently accessed archival data** check box.</span></span> <span data-ttu-id="f7149-110">기타 모든 경우에는 **계층화된 볼륨**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7149-110">For all other use cases, simply select **Tiered Volume**.</span></span> <span data-ttu-id="f7149-111">(계층화된 볼륨이 이전에는 기본 볼륨이었습니다.)</span><span class="sxs-lookup"><span data-stu-id="f7149-111">(Tiered volumes were formerly called primary volumes).</span></span>
      
        ![볼륨 추가](./media/storsimple-create-volume/ScreenshotUpdate1VolumeFlow.png)
      
      1. <span data-ttu-id="f7149-113">Hello 화살표 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7149-113">Click hello arrow icon</span></span> ![화살표 아이콘](./media/storsimple-create-volume/HCS_ArrowIcon-include.png) <span data-ttu-id="f7149-115">toogo toohello 다음 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="f7149-115">toogo toohello next page.</span></span>
3. <span data-ttu-id="f7149-116">Hello에 **추가 설정을** 대화 상자, 새로운 액세스 제어 레코드 (ACR) 추가:</span><span class="sxs-lookup"><span data-stu-id="f7149-116">In hello **Additional Settings** dialog box, add a new access control record (ACR):</span></span>
   
   1. <span data-ttu-id="f7149-117">ACR의 **이름** 을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f7149-117">Supply a **Name** for your ACR.</span></span>
   2. <span data-ttu-id="f7149-118">아래 **iSCSI 초기자 이름**, 제공 hello iSCSI 정규화 된 이름 (IQN) Windows 호스트의 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7149-118">Under **iSCSI Initiator Name**, provide hello iSCSI Qualified Name (IQN) of your Windows host.</span></span> <span data-ttu-id="f7149-119">IQN hello를 설정 하지 않은 경우 너무 이동[Get hello Windows Server 호스트의 IQN](#get-the-iqn-of-a-windows-server-host)합니다.</span><span class="sxs-lookup"><span data-stu-id="f7149-119">If you don't have hello IQN, go too[Get hello IQN of a Windows Server host](#get-the-iqn-of-a-windows-server-host).</span></span>
   3. <span data-ttu-id="f7149-120">Hello를 선택 하 여 기본 백업을 사용 하도록 설정한 것이 좋습니다 **이 볼륨에 대 한 기본 백업 사용** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7149-120">We recommend that you enable a default backup by selecting hello **Enable a default backup for this volume** check box.</span></span> <span data-ttu-id="f7149-121">hello 기본 백업에서 22 시 30 매일 (장치 시간) 실행 하 고이 볼륨의 클라우드 스냅숏을 만드는 하는 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f7149-121">hello default backup will create a policy that executes at 22:30 each day (device time) and creates a cloud snapshot of this volume.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="f7149-122">여기에 hello 백업을 사용 하는지, 되돌릴 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f7149-122">After hello backup is enabled here, it cannot be reverted.</span></span> <span data-ttu-id="f7149-123">이 설정은 tooedit hello 볼륨 toomodify 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7149-123">You will need tooedit hello volume toomodify this setting.</span></span>
      > 
      > 
      
        ![볼륨 추가](./media/storsimple-create-volume/AddVolume2-include.png)
4. <span data-ttu-id="f7149-125">Hello 확인 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7149-125">Click hello check icon</span></span> ![확인 아이콘](./media/storsimple-create-volume/HCS_CheckIcon-include.png)<span data-ttu-id="f7149-127">에서도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7149-127">.</span></span> <span data-ttu-id="f7149-128">지정 된 hello로 볼륨을 만들 수는 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="f7149-128">A volume will be created with hello specified settings.</span></span>

<span data-ttu-id="f7149-129">![동영상 사용 가능](./media/storsimple-create-volume/Video_icon.png) **동영상 사용 가능**</span><span class="sxs-lookup"><span data-stu-id="f7149-129">![Video available](./media/storsimple-create-volume/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="f7149-130">toowatch 보여 주는 비디오에서 toocreate StorSimple 볼륨을 클릭 하는 방법을 [여기](https://azure.microsoft.com/documentation/videos/create-a-storsimple-volume/)합니다.</span><span class="sxs-lookup"><span data-stu-id="f7149-130">toowatch a video that demonstrates how toocreate a StorSimple volume, click [here](https://azure.microsoft.com/documentation/videos/create-a-storsimple-volume/).</span></span>

