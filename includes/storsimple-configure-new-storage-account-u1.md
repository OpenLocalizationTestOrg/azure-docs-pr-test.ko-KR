<!--author=alkohli last changed: 9/17/15-->

#### <a name="tooadd-a-storage-account-in-storsimple-8000-series-update-10"></a><span data-ttu-id="95245-101">tooadd StorSimple 8000 시리즈 업데이트 1.0의 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="95245-101">tooadd a storage account in StorSimple 8000 Series Update 1.0</span></span>
1. <span data-ttu-id="95245-102">Hello StorSimple 관리자 서비스 방문 페이지에서 서비스를 선택 하 고 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="95245-102">On hello StorSimple Manager service landing page, select your service and double-click it.</span></span> <span data-ttu-id="95245-103">그러면 toohello **빠른 시작** 페이지.</span><span class="sxs-lookup"><span data-stu-id="95245-103">This will take you toohello **Quick Start** page.</span></span> <span data-ttu-id="95245-104">선택 hello **구성** 페이지.</span><span class="sxs-lookup"><span data-stu-id="95245-104">Select hello **Configure** page.</span></span>
2. <span data-ttu-id="95245-105">**저장소 계정 추가/편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="95245-105">Click **Add/edit storage account**.</span></span>
3. <span data-ttu-id="95245-106">Hello에 **저장소 계정 추가/편집** 대화 상자를 클릭 **새로 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="95245-106">In hello **Add/Edit Storage Account** dialog box, click **Add new**.</span></span>
4. <span data-ttu-id="95245-107">Hello에 **공급자** 필드를 선택 하는 hello 적절 한 클라우드 서비스 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="95245-107">In hello **Provider** field, select hello appropriate cloud service provider.</span></span> <span data-ttu-id="95245-108">지원 되는 hello 공급자는 Azure, Amazon S3, RR, HP 및 OpenStack Amazon S3입니다.</span><span class="sxs-lookup"><span data-stu-id="95245-108">hello supported providers are Azure, Amazon S3, Amazon S3 with RRS, HP and OpenStack.</span></span> <span data-ttu-id="95245-109">Hello 자격 증명 및 연결 된 클라우드 서비스 공급자의 저장소 계정 hello hello 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="95245-109">Specify hello credentials and hello location associated with hello storage account of your cloud service providers.</span></span> <span data-ttu-id="95245-110">자격 증명을 제공 하는 hello 필드를 사용자가 지정한 hello 클라우드 서비스 공급자에 따라 달라질 수. 있습니다</span><span class="sxs-lookup"><span data-stu-id="95245-110">hello fields presented for credentials will be different depending upon hello cloud service provider you have specified.</span></span> 
   
   * <span data-ttu-id="95245-111">Azure 클라우드 서비스 공급자를 선택한 경우에 제공 hello **이름** 및 기본 hello **선택 키** Microsoft Azure 저장소 계정에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="95245-111">If you have selected Azure as your cloud service provider, supply hello **Name** and hello primary **Access Key** for your Microsoft Azure storage account.</span></span> <span data-ttu-id="95245-112">Azure 계정에 대 한 hello 위치 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="95245-112">For an Azure account, hello location will be automatically populated.</span></span>
     
        ![Azure Storage 계정 추가](./media/storsimple-configure-new-storage-account-u1/AddAzureStorageaccount-include.png)
   * <span data-ttu-id="95245-114">Amazon S3 또는 Amazon S3 with RRS을 선택한 경우 친숙한 **저장소 계정 이름**, **액세스 키** 및 **비밀 키**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="95245-114">If you have selected Amazon S3 or Amazon S3 with RRS, provide a friendly **Storage Account name**, **Access Key**, and **Secret Key**.</span></span> <span data-ttu-id="95245-115">Amazon S3 및 Amazon S3 RR으로 다음 위치 hello 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95245-115">For Amazon S3 and Amazon S3 with RRS, hello following locations are supported:</span></span>
     
     * <span data-ttu-id="95245-116">미국 표준</span><span class="sxs-lookup"><span data-stu-id="95245-116">US Standard</span></span>
     * <span data-ttu-id="95245-117">미국 서부(오리건)</span><span class="sxs-lookup"><span data-stu-id="95245-117">US West (Oregon)</span></span>
     * <span data-ttu-id="95245-118">미국 서부(캘리포니아 북부)</span><span class="sxs-lookup"><span data-stu-id="95245-118">US West (Northern California)</span></span>
     * <span data-ttu-id="95245-119">EU(아일랜드)</span><span class="sxs-lookup"><span data-stu-id="95245-119">EU (Ireland)</span></span>
     * <span data-ttu-id="95245-120">아시아 태평양(싱가포르)</span><span class="sxs-lookup"><span data-stu-id="95245-120">Asia Pacific (Singapore)</span></span>
     * <span data-ttu-id="95245-121">아시아 태평양(시드니)</span><span class="sxs-lookup"><span data-stu-id="95245-121">Asia Pacific (Sydney)</span></span>
     * <span data-ttu-id="95245-122">아시아 태평양(도쿄)</span><span class="sxs-lookup"><span data-stu-id="95245-122">Asia Pacific (Tokyo)</span></span>
     * <span data-ttu-id="95245-123">남미(상파울루)</span><span class="sxs-lookup"><span data-stu-id="95245-123">South America (Sao Paulo)</span></span>
       
       ![Amazon 저장소 계정 추가](./media/storsimple-configure-new-storage-account-u1/AddAmazonStorageaccount-include.png)
   * <span data-ttu-id="95245-125">클라우드 서비스 공급자로 HP를 선택한 경우, 친숙한 **저장소 계정 이름**, **테넌트 ID**, **사용자 이름** 및 **암호**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="95245-125">If you have selected HP as your cloud service provider, supply a friendly **Storage Account Name**, **Tenant ID**, **Username**, and **Password**.</span></span> <span data-ttu-id="95245-126">HP, 다음 위치 hello 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95245-126">For HP, hello following locations are supported:</span></span>
     
     * <span data-ttu-id="95245-127">미국 동부</span><span class="sxs-lookup"><span data-stu-id="95245-127">US East</span></span>
     * <span data-ttu-id="95245-128">미국 서부</span><span class="sxs-lookup"><span data-stu-id="95245-128">US West</span></span>
       
       ![HP 저장소 계정 추가](./media/storsimple-configure-new-storage-account-u1/AddHPStorageaccount-include.png)
   * <span data-ttu-id="95245-130">**Openstack**을 클라우드 서비스 공급자로 선택한 경우, **호스트 이름**, **액세스 키** 및 **비밀 키**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="95245-130">If you have selected **Openstack** as your cloud service provider, provide a **Hostname**, **Access Key**, and **Secret Key**.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="95245-131">Azure에서 제외 하 고 hello 클라우드 서비스 공급자, 모든에 대 한 이름을 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95245-131">For all hello cloud service providers, excluding Azure, a friendly name is allowed.</span></span> <span data-ttu-id="95245-132">서로 다른 친숙 한 이름을 사용 하 고 자격 증명의 집합 동일 hello로 둘 이상의 저장소 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95245-132">You can use different friendly names and create more than one storage account with hello same set of credentials.</span></span>
     > 
     > 
     
        ![Openstack 저장소 계정 추가](./media/storsimple-configure-new-storage-account-u1/AddOpenstackStorageaccount-include.png)
5. <span data-ttu-id="95245-134">선택 **SSL 모드 사용** toocreate 장치와 hello 클라우드 사이의 네트워크 통신을 위한 보안 채널입니다.</span><span class="sxs-lookup"><span data-stu-id="95245-134">Select **Enable SSL Mode** toocreate a secure channel for network communication between your device and hello cloud.</span></span> <span data-ttu-id="95245-135">지우기 hello **SSL 모드 사용** 확인란 사설 클라우드 내에서 작동 하는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="95245-135">Clear hello **Enable SSL Mode** check box only if you are operating within a private cloud.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="95245-136">HP를 공급자로 사용하는 경우 SSL을 항상 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95245-136">If you are using HP as your provider, SSL will always be enabled.</span></span>
   > 
   > 
6. <span data-ttu-id="95245-137">Hello 확인 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="95245-137">Click hello check icon</span></span> ![확인 아이콘](./media/storsimple-configure-new-storage-account/HCS_CheckIcon-include.png)<span data-ttu-id="95245-139">에서도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95245-139">.</span></span> <span data-ttu-id="95245-140">Hello 저장소 계정이 정상적으로 만들어지면 알림이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95245-140">You will be notified after hello storage account is successfully created.</span></span>
7. <span data-ttu-id="95245-141">새로 만든 저장소 계정 hello hello에 표시 될 **구성** 페이지 **저장소 계정은**합니다.</span><span class="sxs-lookup"><span data-stu-id="95245-141">hello newly created storage account will be displayed on hello **Configure** page under **Storage accounts**.</span></span> <span data-ttu-id="95245-142">클릭 **저장** toosave hello 새 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="95245-142">Click **Save** toosave hello new storage account.</span></span> <span data-ttu-id="95245-143">확인하라는 메시지가 표시되면 **확인** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="95245-143">Click **OK** when prompted for confirmation.</span></span>

