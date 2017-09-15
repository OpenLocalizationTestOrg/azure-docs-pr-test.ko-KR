<!--author=SharS last changed: 12/01/15-->

### <a name="step-1-authorize-a-device-to-change-the-service-data-encryption-key-in-the-azure-classic-portal"></a><span data-ttu-id="ab8cc-101">1단계: Azure 클래식 포털에서 장치에 서비스 데이터 암호화 키를 변경할 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-101">Step 1: Authorize a device to change the service data encryption key in the Azure classic portal</span></span>
<span data-ttu-id="ab8cc-102">일반적으로 장치 관리자는 서비스 관리자가 장치에 서비스 데이터 암호화 키를 변경할 수 있는 권한을 부여하도록 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-102">Typically, the device administrator will request that the service administrator authorize a device to change service data encryption keys.</span></span> <span data-ttu-id="ab8cc-103">그러면 서비스 관리자는 장치에 키를 변경할 수 있는 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-103">The service administrator will then authorize the device to change the key.</span></span>

<span data-ttu-id="ab8cc-104">이 단계는 Azure 클래식 포털에서 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-104">This step is performed in the Azure classic portal.</span></span> <span data-ttu-id="ab8cc-105">서비스 관리자는 권한을 부여할 수 있는 표시된 장치 목록에서 장치를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-105">The service administrator can select a device from a displayed list of the devices that are eligible to be authorized.</span></span> <span data-ttu-id="ab8cc-106">그러면 장치에 서비스 데이터 암호화 키 변경 프로세스를 시작할 수 있는 권한이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-106">The device is then authorized to start the service data encryption key change process.</span></span>

#### <a name="which-devices-can-be-authorized-to-change-service-data-encryption-keys"></a><span data-ttu-id="ab8cc-107">서비스 데이터 암호화 키를 변경할 권한이 부여될 수 있는 장치</span><span class="sxs-lookup"><span data-stu-id="ab8cc-107">Which devices can be authorized to change service data encryption keys?</span></span>
<span data-ttu-id="ab8cc-108">서비스 데이터 암호화 키 변경을 시작할 권한을 부여받으려면 장치가 다음 조건을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-108">A device must meet the following criteria before it can be authorized to initiate service data encryption key changes:</span></span>

* <span data-ttu-id="ab8cc-109">장치는 온라인 상태여야 서비스 데이터 암호화 키 변경 권한 부여 대상이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-109">The device must be online to be eligible for service data encryption key change authorization.</span></span>
* <span data-ttu-id="ab8cc-110">키 변경이 시작되지 않은 경우 30분 후에 동일한 장치에 권한을 다시 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-110">You can authorize the same device again after 30 minutes if the key change has not been initiated.</span></span>
* <span data-ttu-id="ab8cc-111">이전에 권한을 부여받은 장치에서 키 변경을 시작하지 않은 경우 다른 장치에 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-111">You can authorize a different device, provided that the key change has not been initiated by the previously authorized device.</span></span> <span data-ttu-id="ab8cc-112">새 장치에 권한을 부여하면 이전 장치는 변경을 시작할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-112">After the new device has been authorized, the old device cannot initiate the change.</span></span>
* <span data-ttu-id="ab8cc-113">서비스 데이터 암호화 키 롤오버가 진행 중인 동안에는 장치에 권한을 부여할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-113">You cannot authorize a device while the rollover of the service data encryption key is in progress.</span></span>
* <span data-ttu-id="ab8cc-114">서비스에 등록된 장치 중 일부만 롤오버한 경우에는 장치에 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-114">You can authorize a device when some of the devices registered with the service have rolled over the encryption while others have not.</span></span> <span data-ttu-id="ab8cc-115">이 경우는 적합한 장치는 서비스 데이터 암호화 키 변경을 완료한 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-115">In such cases, the eligible devices are the ones that have completed the service data encryption key change.</span></span>

> [!NOTE]
> <span data-ttu-id="ab8cc-116">StorSimple 가상 장치는 Azure 클래식 포털에서 키 변경을 시작할 권한을 부여받을 수 있는 장치 목록에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-116">In the Azure classic portal, StorSimple virtual devices are not shown in the list of devices that can be authorized to start the key change.</span></span>
> 
> 

<span data-ttu-id="ab8cc-117">다음 단계에 따라 장치를 선택하고 서비스 데이터 암호화 키 변경을 시작할 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-117">Perform the following steps to select and authorize a device to initiate the service data encryption key change.</span></span>

#### <a name="to-authorize-a-device-to-change-the-key"></a><span data-ttu-id="ab8cc-118">장치에 키 변경 권한을 부여하려면</span><span class="sxs-lookup"><span data-stu-id="ab8cc-118">To authorize a device to change the key</span></span>
1. <span data-ttu-id="ab8cc-119">서비스 대시보드 페이지에서 **서비스 데이터 암호화 키 변경**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-119">On the service dashboard page, click **Change service data encryption key**.</span></span>
   
    ![서비스 암호화 키 변경](./media/storsimple-change-data-encryption-key/HCS_ChangeServiceDataEncryptionKey-include.png)
2. <span data-ttu-id="ab8cc-121">**서비스 데이터 암호화 키 변경** 대화 상자에서 장치를 선택하고 서비스 데이터 암호화 키 변경을 시작할 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-121">In the **Change service data encryption key** dialog box, select and authorize a device to initiate the service data encryption key change.</span></span> <span data-ttu-id="ab8cc-122">드롭다운 목록에 권한을 부여할 수 있는 모든 장치가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-122">The drop-down list has all the eligible devices that can be authorized.</span></span>
3. <span data-ttu-id="ab8cc-123">확인 아이콘</span><span class="sxs-lookup"><span data-stu-id="ab8cc-123">Click the check icon</span></span> ![확인 아이콘](./media/storsimple-change-data-encryption-key/HCS_CheckIcon-include.png)<span data-ttu-id="ab8cc-125">을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-125">.</span></span>

### <a name="step-2-use-windows-powershell-for-storsimple-to-initiate-the-service-data-encryption-key-change"></a><span data-ttu-id="ab8cc-126">2단계: StorSimple용 Windows PowerShell을 사용하여 서비스 데이터 암호화 키 변경 시작</span><span class="sxs-lookup"><span data-stu-id="ab8cc-126">Step 2: Use Windows PowerShell for StorSimple to initiate the service data encryption key change</span></span>
<span data-ttu-id="ab8cc-127">이 단계는 권한이 부여된 StorSimple 장치의 StorSimple용 Windows PowerShell 인터페이스에서 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-127">This step is performed in the Windows PowerShell for StorSimple interface on the authorized StorSimple device.</span></span>

> [!NOTE]
> <span data-ttu-id="ab8cc-128">키 롤오버가 완료될 때까지 StorSimple 관리자 서비스의 Azure 클래식 포털에서 수행할 수 있는 작업은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-128">No operations can be performed in the Azure classic portal of your StorSimple Manager service until the key rollover is completed.</span></span>
> 
> 

<span data-ttu-id="ab8cc-129">장치 직렬 콘솔을 사용하여 Windows PowerShell 인터페이스에 연결하는 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-129">If you are using the device serial console to connect to the Windows PowerShell interface, perform the following steps.</span></span>

#### <a name="to-initiate-the-service-data-encryption-key-change"></a><span data-ttu-id="ab8cc-130">서비스 데이터 암호화 키 변경을 시작하려면</span><span class="sxs-lookup"><span data-stu-id="ab8cc-130">To initiate the service data encryption key change</span></span>
1. <span data-ttu-id="ab8cc-131">옵션 1을 선택하여 모든 권한으로 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-131">Select option 1 to log on with full access.</span></span>
2. <span data-ttu-id="ab8cc-132">명령 프롬프트에 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-132">At the command prompt, type:</span></span>
   
     `Invoke-HcsmServiceDataEncryptionKeyChange`
3. <span data-ttu-id="ab8cc-133">cmdlet이 성공적으로 완료되면 새 서비스 데이터 암호화 키를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-133">After the cmdlet has successfully completed, you will get a new service data encryption key.</span></span> <span data-ttu-id="ab8cc-134">이 키를 복사하고 저장해 두었다가 이 프로세스의 3단계에서 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-134">Copy and save this key for use in step 3 of this process.</span></span> <span data-ttu-id="ab8cc-135">이 키는 StorSimple 관리자 서비스에 등록된 나머지 모든 장치를 업데이트하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-135">This key will be used to update all the remaining devices registered with the StorSimple Manager service.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ab8cc-136">이 프로세스는 StorSimple 장치에 권한을 부여한 후 4시간 이내에 시작되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-136">This process must be initiated within four hours of authorizing a StorSimple device.</span></span>
   > 
   > 
   
   <span data-ttu-id="ab8cc-137">이 새 키는 서비스로 전송되어 서비스에 등록된 모든 장치에 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-137">This new key is then sent to the service to be pushed to all the devices that are registered with the service.</span></span> <span data-ttu-id="ab8cc-138">서비스 대시보드에 경고가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-138">An alert will then appear on the service dashboard.</span></span> <span data-ttu-id="ab8cc-139">서비스는 등록된 장치에서 모든 작업을 사용할 수 없도록 설정합니다. 그러면 장치 관리자는 다른 장치에서 서비스 데이터 암호화 키를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-139">The service will disable all the operations on the registered devices, and the device administrator will then need to update the service data encryption key on the other devices.</span></span> <span data-ttu-id="ab8cc-140">그러나 I/O(클라우드로 데이터를 보내는 호스트)는 중단되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-140">However, the I/Os (hosts sending data to the cloud) will not be disrupted.</span></span>
   
   <span data-ttu-id="ab8cc-141">단일 장치를 서비스에 등록한 경우 이제 롤오버 프로세스가 완료되었으므로 다음 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-141">If you have a single device registered to your service, the rollover process is now complete and you can skip the next step.</span></span> <span data-ttu-id="ab8cc-142">여러 장치를 서비스에 등록한 경우 3단계를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-142">If you have multiple devices registered to your service, proceed to step 3.</span></span>

### <a name="step-3-update-the-service-data-encryption-key-on-other-storsimple-devices"></a><span data-ttu-id="ab8cc-143">3단계: 다른 StorSimple 장치에서 서비스 데이터 암호화 키 업데이트</span><span class="sxs-lookup"><span data-stu-id="ab8cc-143">Step 3: Update the service data encryption key on other StorSimple devices</span></span>
<span data-ttu-id="ab8cc-144">여러 장치를 StorSimple 관리자 서비스에 등록한 경우 StorSimple 장치의 Windows PowerShell 인터페이스에서 다음 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-144">These steps must be performed in the Windows PowerShell interface of your StorSimple device if you have multiple devices registered to your StorSimple Manager service.</span></span> <span data-ttu-id="ab8cc-145">2단계: StorSimple용 Windows PowerShell을 사용하여 서비스 데이터 암호화 키 변경 시작에서 얻은 키를 사용하여 StorSimple 관리자 장치에 등록된 나머지 모든 StorSimple 장치를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-145">The key that you obtained in Step 2: Use Windows PowerShell for StorSimple to initiate the service data encryption key change must be used to update all the remaining StorSimple device registered with the StorSimple Manager service.</span></span>

<span data-ttu-id="ab8cc-146">다음 단계를 수행하여 장치에서 서비스 데이터 암호화를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-146">Perform the following steps to update the service data encryption on your device.</span></span>

#### <a name="to-update-the-service-data-encryption-key"></a><span data-ttu-id="ab8cc-147">서비스 데이터 암호화 키를 업데이트하려면</span><span class="sxs-lookup"><span data-stu-id="ab8cc-147">To update the service data encryption key</span></span>
1. <span data-ttu-id="ab8cc-148">StorSimple용 Windows PowerShell을 사용하여 콘솔에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-148">Use Windows PowerShell for StorSimple to connect to the console.</span></span> <span data-ttu-id="ab8cc-149">옵션 1을 선택하여 모든 권한으로 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-149">Select option 1 to log on with full access.</span></span>
2. <span data-ttu-id="ab8cc-150">명령 프롬프트에 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-150">At the command prompt, type:</span></span>
   
    `Invoke-HcsmServiceDataEncryptionKeyChange – ServiceDataEncryptionKey`
3. <span data-ttu-id="ab8cc-151">[2단계: StorSimple용 Windows PowerShell을 사용하여 서비스 데이터 암호화 키 변경 시작](#to-initiate-the-service-data-encryption-key-change)에서 얻은 서비스 데이터 암호화 키를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ab8cc-151">Provide the service data encryption key that you obtained in [Step 2: Use Windows PowerShell for StorSimple to initiate the service data encryption key change](#to-initiate-the-service-data-encryption-key-change).</span></span>

