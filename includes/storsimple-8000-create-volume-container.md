<!--author=alkohli last changed: 06/22/17-->

#### <a name="toocreate-a-volume-container"></a><span data-ttu-id="1f535-101">toocreate 볼륨 컨테이너</span><span class="sxs-lookup"><span data-stu-id="1f535-101">toocreate a volume container</span></span>
1. <span data-ttu-id="1f535-102">Tooyour StorSimple 장치 관리자 서비스를 이동 하 고 클릭 **장치**합니다.</span><span class="sxs-lookup"><span data-stu-id="1f535-102">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="1f535-103">Hello hello 장치 나열 하는 테이블 형식에서 선택 하 고 장치를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f535-103">From hello tabular listing of hello devices, select and click a device.</span></span> 

    ![볼륨 컨테이너 블레이드](./media/storsimple-8000-create-volume-container/createvolumecontainer1.png)

2. <span data-ttu-id="1f535-105">Hello 장치 대시보드 클릭 **+ 볼륨 컨테이너 추가**</span><span class="sxs-lookup"><span data-stu-id="1f535-105">In hello device dashboard, click **+ Add volume container**</span></span>

    ![볼륨 컨테이너 블레이드](./media/storsimple-8000-create-volume-container/createvolumecontainer2.png)

3. <span data-ttu-id="1f535-107">Hello에 **추가 볼륨 컨테이너** 블레이드:</span><span class="sxs-lookup"><span data-stu-id="1f535-107">In hello **Add volume container** blade:</span></span>
   
   1. <span data-ttu-id="1f535-108">hello 장치가 자동으로 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f535-108">hello device is automatically selected.</span></span>
   2. <span data-ttu-id="1f535-109">볼륨 컨테이너의 **이름** 을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1f535-109">Supply a **Name** for your volume container.</span></span> <span data-ttu-id="1f535-110">hello 이름은 3 too32 자 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f535-110">hello name must be 3 too32 characters long.</span></span> <span data-ttu-id="1f535-111">볼륨 컨테이너를 만든 후에는 이름을 바꿀 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1f535-111">You cannot rename a volume container once it is created.</span></span>
   3. <span data-ttu-id="1f535-112">선택 **클라우드 저장소 암호화 사용** tooenable hello 장치 toohello 클라우드에서 전송 하는 hello 데이터를 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f535-112">Select **Enable Cloud Storage Encryption** tooenable encryption of hello data sent from hello device toohello cloud.</span></span>
   4. <span data-ttu-id="1f535-113">입력 하 고 확인 한 **클라우드 저장소 암호화 키** 즉 8 too32 자입니다.</span><span class="sxs-lookup"><span data-stu-id="1f535-113">Provide and confirm a **Cloud Storage Encryption Key** that is 8 too32 characters long.</span></span> <span data-ttu-id="1f535-114">이 키는 hello 장치 tooaccess 암호화 된 데이터에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f535-114">This key is used by hello device tooaccess encrypted data.</span></span>
   5. <span data-ttu-id="1f535-115">선택 된 **저장소 계정** tooassociate이 볼륨 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="1f535-115">Select a **Storage Account** tooassociate with this volume container.</span></span> <span data-ttu-id="1f535-116">기존 저장소 계정 또는 서비스를 만들 hello 시 발생 하는 hello 기본 계정을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f535-116">You can choose an existing storage account or hello default account that is generated at hello time of service creation.</span></span> <span data-ttu-id="1f535-117">Hello를 사용할 수도 있습니다 **새로 추가** 옵션 toospecify 하지 않은 저장소 계정 toothis 서비스 구독을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f535-117">You can also use hello **Add new** option toospecify a storage account that is not linked toothis service subscription.</span></span>
   6. <span data-ttu-id="1f535-118">선택 **무제한** hello에 **대역폭 지정** tooconsume hello 사용 가능한 모든 대역폭을 원하는 경우 드롭다운 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="1f535-118">Select **Unlimited** in hello **Specify bandwidth** drop-down list if you wish tooconsume all hello available bandwidth.</span></span> <span data-ttu-id="1f535-119">또한이 옵션 설정할 수 있습니다이 너무**사용자 지정** tooemploy 대역폭 제어 1mbps에서 1, 000mbps 사이의 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f535-119">You can also set this option too**Custom** tooemploy bandwidth controls, and specify a value between 1 Mbps and 1,000 Mbps.</span></span>
      <span data-ttu-id="1f535-120">사용할 수 있는 대역폭 사용 정보를 설정한 경우 수를 지정 하 여 일정에 따라 수 tooallocate 대역폭 **대역폭 템플릿 선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="1f535-120">If you have your bandwidth usage information available, you may be able tooallocate bandwidth based on a schedule by specifying **Select a bandwidth template**.</span></span> <span data-ttu-id="1f535-121">단계별 절차에 대 한 이동 너무[대역폭 템플릿 추가](../articles/storsimple/storsimple-8000-manage-bandwidth-templates.md#add-a-bandwidth-template)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f535-121">For a step-by-step procedure, go too[Add a bandwidth template](../articles/storsimple/storsimple-8000-manage-bandwidth-templates.md#add-a-bandwidth-template).</span></span>

      ![볼륨 컨테이너 블레이드](./media/storsimple-8000-create-volume-container/createvolumecontainer6b.png)
   7. <span data-ttu-id="1f535-123">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f535-123">Click **Create**.</span></span>

        ![볼륨 컨테이너 블레이드](./media/storsimple-8000-create-volume-container/createvolumecontainer6.png)
   
       <span data-ttu-id="1f535-125">Hello 볼륨 컨테이너 성공적으로 만들어지면 알림이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f535-125">You are notified when hello volume container is successfully created.</span></span>

       ![볼륨 컨테이너 만들기 알림](./media/storsimple-8000-create-volume-container/createvolumecontainer8.png)

   <span data-ttu-id="1f535-127">볼륨 컨테이너를 새로 만든 hello hello 장치에 대 한 볼륨 컨테이너 목록에 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f535-127">hello newly created volume container is listed in hello list of volume containers for your device.</span></span>

   ![볼륨 컨테이너 추가 블레이드](./media/storsimple-8000-create-volume-container/createvolumecontainer9.png)


