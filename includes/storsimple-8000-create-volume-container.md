<!--author=alkohli last changed: 06/22/17-->

#### <a name="to-create-a-volume-container"></a><span data-ttu-id="c9b4c-101">볼륨 컨테이너를 만들려면</span><span class="sxs-lookup"><span data-stu-id="c9b4c-101">To create a volume container</span></span>
1. <span data-ttu-id="c9b4c-102">StorSimple 장치 관리자 서비스로 이동한 다음 **장치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-102">Go to your StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="c9b4c-103">테이블 형식 장치 목록에서 장치를 선택하여 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-103">From the tabular listing of the devices, select and click a device.</span></span> 

    ![볼륨 컨테이너 블레이드](./media/storsimple-8000-create-volume-container/createvolumecontainer1.png)

2. <span data-ttu-id="c9b4c-105">장치 대시보드에서 **+ 볼륨 컨테이너 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-105">In the device dashboard, click **+ Add volume container**</span></span>

    ![볼륨 컨테이너 블레이드](./media/storsimple-8000-create-volume-container/createvolumecontainer2.png)

3. <span data-ttu-id="c9b4c-107">**볼륨 컨테이너 추가** 블레이드에서:</span><span class="sxs-lookup"><span data-stu-id="c9b4c-107">In the **Add volume container** blade:</span></span>
   
   1. <span data-ttu-id="c9b4c-108">장치가 자동으로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-108">The device is automatically selected.</span></span>
   2. <span data-ttu-id="c9b4c-109">볼륨 컨테이너의 **이름** 을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-109">Supply a **Name** for your volume container.</span></span> <span data-ttu-id="c9b4c-110">이름은 3~32자 길이여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-110">The name must be 3 to 32 characters long.</span></span> <span data-ttu-id="c9b4c-111">볼륨 컨테이너를 만든 후에는 이름을 바꿀 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-111">You cannot rename a volume container once it is created.</span></span>
   3. <span data-ttu-id="c9b4c-112">**클라우드 저장소 암호화 사용** 을 선택하여 장치에서 클라우드로 보낸 데이터의 암호화를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-112">Select **Enable Cloud Storage Encryption** to enable encryption of the data sent from the device to the cloud.</span></span>
   4. <span data-ttu-id="c9b4c-113">8~32자 길이의 **클라우드 저장소 암호화 키** 를 제공 및 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-113">Provide and confirm a **Cloud Storage Encryption Key** that is 8 to 32 characters long.</span></span> <span data-ttu-id="c9b4c-114">이 키는 암호화된 데이터에 액세스하는 장치가 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-114">This key is used by the device to access encrypted data.</span></span>
   5. <span data-ttu-id="c9b4c-115">**저장소 계정** 을 선택하여 이 볼륨 컨테이너와 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-115">Select a **Storage Account** to associate with this volume container.</span></span> <span data-ttu-id="c9b4c-116">서비스를 만들 때 생성되는 기본 계정 또는 기존 저장소 계정을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-116">You can choose an existing storage account or the default account that is generated at the time of service creation.</span></span> <span data-ttu-id="c9b4c-117">**새로 추가** 옵션을 사용하여 이 서비스 구독에 연결되지 않은 저장소 계정을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-117">You can also use the **Add new** option to specify a storage account that is not linked to this service subscription.</span></span>
   6. <span data-ttu-id="c9b4c-118">사용 가능한 모든 대역폭을 사용하려는 경우 **대역폭 지정** 드롭다운 목록에서 **제한 없음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-118">Select **Unlimited** in the **Specify bandwidth** drop-down list if you wish to consume all the available bandwidth.</span></span> <span data-ttu-id="c9b4c-119">이 옵션을 **사용자 지정** 으로 설정하여 대역폭 제어를 사용하고 1Mbps~1,000Mbps 사이의 값을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-119">You can also set this option to **Custom** to employ bandwidth controls, and specify a value between 1 Mbps and 1,000 Mbps.</span></span>
      <span data-ttu-id="c9b4c-120">사용 가능한 대역폭 사용 정보가 있는 경우 **대역폭 템플릿 선택**을 지정하여 일정에 따라 대역폭을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-120">If you have your bandwidth usage information available, you may be able to allocate bandwidth based on a schedule by specifying **Select a bandwidth template**.</span></span> <span data-ttu-id="c9b4c-121">단계별 절차의 경우 [대역폭 템플릿 추가](../articles/storsimple/storsimple-8000-manage-bandwidth-templates.md#add-a-bandwidth-template)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-121">For a step-by-step procedure, go to [Add a bandwidth template](../articles/storsimple/storsimple-8000-manage-bandwidth-templates.md#add-a-bandwidth-template).</span></span>

      ![볼륨 컨테이너 블레이드](./media/storsimple-8000-create-volume-container/createvolumecontainer6b.png)
   7. <span data-ttu-id="c9b4c-123">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-123">Click **Create**.</span></span>

        ![볼륨 컨테이너 블레이드](./media/storsimple-8000-create-volume-container/createvolumecontainer6.png)
   
       <span data-ttu-id="c9b4c-125">볼륨 컨테이너가 성공적으로 만들어지면 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-125">You are notified when the volume container is successfully created.</span></span>

       ![볼륨 컨테이너 만들기 알림](./media/storsimple-8000-create-volume-container/createvolumecontainer8.png)

   <span data-ttu-id="c9b4c-127">새로 만들어진 볼륨 컨테이너가 장치에 대한 볼륨 컨테이너 목록에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-127">The newly created volume container is listed in the list of volume containers for your device.</span></span>

   ![볼륨 컨테이너 추가 블레이드](./media/storsimple-8000-create-volume-container/createvolumecontainer9.png)


