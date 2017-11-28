<!--author=alkohli last changed: 9/17/15-->

#### <a name="to-add-a-storage-account-in-storsimple-8000-series-update-10"></a><span data-ttu-id="1152f-101">StorSimple 8000 시리즈 업데이트 1.0에서 저장소 계정을 추가하려면</span><span class="sxs-lookup"><span data-stu-id="1152f-101">To add a storage account in StorSimple 8000 Series Update 1.0</span></span>
1. <span data-ttu-id="1152f-102">StorSimple 관리자 서비스 방문 페이지에서 서비스를 선택하고 두번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1152f-102">On the StorSimple Manager service landing page, select your service and double-click it.</span></span> <span data-ttu-id="1152f-103">이렇게 하면 **퀵 스타트** 페이지로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="1152f-103">This will take you to the **Quick Start** page.</span></span> <span data-ttu-id="1152f-104">**구성** 페이지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1152f-104">Select the **Configure** page.</span></span>
2. <span data-ttu-id="1152f-105">**저장소 계정 추가/편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1152f-105">Click **Add/edit storage account**.</span></span>
3. <span data-ttu-id="1152f-106">**저장소 계정 추가/편집** 대화 상자에서 **새로 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1152f-106">In the **Add/Edit Storage Account** dialog box, click **Add new**.</span></span>
4. <span data-ttu-id="1152f-107">**공급자** 필드에서 적절한 클라우드 서비스 공급자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1152f-107">In the **Provider** field, select the appropriate cloud service provider.</span></span> <span data-ttu-id="1152f-108">지원되는 공급자는 Azure, Amazon S3, Amazon S3 with RRS, HP 및 OpenStack입니다.</span><span class="sxs-lookup"><span data-stu-id="1152f-108">The supported providers are Azure, Amazon S3, Amazon S3 with RRS, HP and OpenStack.</span></span> <span data-ttu-id="1152f-109">클라우드 서비스 공급자의 저장소 계정과 연결된 위치 및 자격 증명을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1152f-109">Specify the credentials and the location associated with the storage account of your cloud service providers.</span></span> <span data-ttu-id="1152f-110">자격 증명에 대해 제공하는 필드는 지정하는 클라우드 서비스 공급자에 따라 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1152f-110">The fields presented for credentials will be different depending upon the cloud service provider you have specified.</span></span> 
   
   * <span data-ttu-id="1152f-111">Azure를 클라우드 서비스 공급자로 선택한 경우 Microsoft Azure Storage 계정에 대한 **이름** 및 기본 **액세스 키**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1152f-111">If you have selected Azure as your cloud service provider, supply the **Name** and the primary **Access Key** for your Microsoft Azure storage account.</span></span> <span data-ttu-id="1152f-112">Azure 계정에 대한 위치는 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="1152f-112">For an Azure account, the location will be automatically populated.</span></span>
     
        ![Azure Storage 계정 추가](./media/storsimple-configure-new-storage-account-u1/AddAzureStorageaccount-include.png)
   * <span data-ttu-id="1152f-114">Amazon S3 또는 Amazon S3 with RRS을 선택한 경우 친숙한 **저장소 계정 이름**, **액세스 키** 및 **비밀 키**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1152f-114">If you have selected Amazon S3 or Amazon S3 with RRS, provide a friendly **Storage Account name**, **Access Key**, and **Secret Key**.</span></span> <span data-ttu-id="1152f-115">Amazon S3 및 Amazon S3 with RRS의 경우 다음 위치가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="1152f-115">For Amazon S3 and Amazon S3 with RRS, the following locations are supported:</span></span>
     
     * <span data-ttu-id="1152f-116">미국 표준</span><span class="sxs-lookup"><span data-stu-id="1152f-116">US Standard</span></span>
     * <span data-ttu-id="1152f-117">미국 서부(오리건)</span><span class="sxs-lookup"><span data-stu-id="1152f-117">US West (Oregon)</span></span>
     * <span data-ttu-id="1152f-118">미국 서부(캘리포니아 북부)</span><span class="sxs-lookup"><span data-stu-id="1152f-118">US West (Northern California)</span></span>
     * <span data-ttu-id="1152f-119">EU(아일랜드)</span><span class="sxs-lookup"><span data-stu-id="1152f-119">EU (Ireland)</span></span>
     * <span data-ttu-id="1152f-120">아시아 태평양(싱가포르)</span><span class="sxs-lookup"><span data-stu-id="1152f-120">Asia Pacific (Singapore)</span></span>
     * <span data-ttu-id="1152f-121">아시아 태평양(시드니)</span><span class="sxs-lookup"><span data-stu-id="1152f-121">Asia Pacific (Sydney)</span></span>
     * <span data-ttu-id="1152f-122">아시아 태평양(도쿄)</span><span class="sxs-lookup"><span data-stu-id="1152f-122">Asia Pacific (Tokyo)</span></span>
     * <span data-ttu-id="1152f-123">남미(상파울루)</span><span class="sxs-lookup"><span data-stu-id="1152f-123">South America (Sao Paulo)</span></span>
       
       ![Amazon 저장소 계정 추가](./media/storsimple-configure-new-storage-account-u1/AddAmazonStorageaccount-include.png)
   * <span data-ttu-id="1152f-125">클라우드 서비스 공급자로 HP를 선택한 경우, 친숙한 **저장소 계정 이름**, **테넌트 ID**, **사용자 이름** 및 **암호**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1152f-125">If you have selected HP as your cloud service provider, supply a friendly **Storage Account Name**, **Tenant ID**, **Username**, and **Password**.</span></span> <span data-ttu-id="1152f-126">HP의 경우 다음 위치가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="1152f-126">For HP, the following locations are supported:</span></span>
     
     * <span data-ttu-id="1152f-127">미국 동부</span><span class="sxs-lookup"><span data-stu-id="1152f-127">US East</span></span>
     * <span data-ttu-id="1152f-128">미국 서부</span><span class="sxs-lookup"><span data-stu-id="1152f-128">US West</span></span>
       
       ![HP 저장소 계정 추가](./media/storsimple-configure-new-storage-account-u1/AddHPStorageaccount-include.png)
   * <span data-ttu-id="1152f-130">**Openstack**을 클라우드 서비스 공급자로 선택한 경우, **호스트 이름**, **액세스 키** 및 **비밀 키**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1152f-130">If you have selected **Openstack** as your cloud service provider, provide a **Hostname**, **Access Key**, and **Secret Key**.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="1152f-131">Azure를 제외한 모든 클라우드 서비스 공급자는 친숙한 이름을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="1152f-131">For all the cloud service providers, excluding Azure, a friendly name is allowed.</span></span> <span data-ttu-id="1152f-132">따라서 다른 친숙한 이름을 사용할 수 있고 동일한 자격 증명 집합을 가진 둘 이상의 저장소 계정을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1152f-132">You can use different friendly names and create more than one storage account with the same set of credentials.</span></span>
     > 
     > 
     
        ![Openstack 저장소 계정 추가](./media/storsimple-configure-new-storage-account-u1/AddOpenstackStorageaccount-include.png)
5. <span data-ttu-id="1152f-134">**SSL 모드 사용** 을 선택하여 장치와 클라우드 간의 네트워크 통신을 위한 안전한 채널을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1152f-134">Select **Enable SSL Mode** to create a secure channel for network communication between your device and the cloud.</span></span> <span data-ttu-id="1152f-135">사설 클라우드 내에서 작업 중인 경우에만 **SSL 모드 사용** 확인란을 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="1152f-135">Clear the **Enable SSL Mode** check box only if you are operating within a private cloud.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1152f-136">HP를 공급자로 사용하는 경우 SSL을 항상 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1152f-136">If you are using HP as your provider, SSL will always be enabled.</span></span>
   > 
   > 
6. <span data-ttu-id="1152f-137">확인 아이콘</span><span class="sxs-lookup"><span data-stu-id="1152f-137">Click the check icon</span></span> ![확인 아이콘](./media/storsimple-configure-new-storage-account/HCS_CheckIcon-include.png)<span data-ttu-id="1152f-139">을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1152f-139">.</span></span> <span data-ttu-id="1152f-140">저장소 계정이 성공적으로 만들어진 후 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1152f-140">You will be notified after the storage account is successfully created.</span></span>
7. <span data-ttu-id="1152f-141">새로 만들어진 저장소 계정이 **저장소 계정**의 **구성** 페이지에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1152f-141">The newly created storage account will be displayed on the **Configure** page under **Storage accounts**.</span></span> <span data-ttu-id="1152f-142">**저장** 을 클릭하여 새 저장소 계정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1152f-142">Click **Save** to save the new storage account.</span></span> <span data-ttu-id="1152f-143">확인하라는 메시지가 표시되면 **확인** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1152f-143">Click **OK** when prompted for confirmation.</span></span>

