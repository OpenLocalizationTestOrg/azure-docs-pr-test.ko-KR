---
title: "StorSimple Manager 서비스 aaaDeploy hello | Microsoft Docs"
description: "어떻게 toocreate 및 delete hello hello Azure 클래식 포털에서에서 StorSimple Manager 서비스에 설명 하 고 toomanage 서비스 등록 키를 hello 하는 방법을 설명 합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: bc1d5650-275c-42ed-bc77-cdb596f85943
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/14/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f49b647d91b03bb89ebd0e5cce196e50e3c00296
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-manager-service-in-hello-azure-classic-portal"></a><span data-ttu-id="df98c-103">Hello Azure 클래식 포털에서에서 hello StorSimple Manager 서비스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-103">Deploy hello StorSimple Manager service in hello Azure classic portal</span></span>

## <a name="overview"></a><span data-ttu-id="df98c-104">개요</span><span class="sxs-lookup"><span data-stu-id="df98c-104">Overview</span></span>
<span data-ttu-id="df98c-105">hello StorSimple Manager 서비스는 Microsoft Azure에서 실행 하 고 toomultiple StorSimple 장치를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-105">hello StorSimple Manager service runs in Microsoft Azure and connects toomultiple StorSimple devices.</span></span> <span data-ttu-id="df98c-106">Hello 서비스를 만든 후 toomanage hello 장치 hello Microsoft Azure 클래식 포털에서 실행 되는 브라우저에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-106">After you create hello service, you can use it toomanage hello devices from hello Microsoft Azure classic portal running in a browser.</span></span> <span data-ttu-id="df98c-107">이렇게 하면 하므로 관리 부담이 최소화 하나의 중앙 위치에서 모든 hello 장치에 연결 된 toohello StorSimple 관리자 서비스 toomonitor 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-107">This allows you toomonitor all hello devices that are connected toohello StorSimple Manager service from a single, central location, thereby minimizing administrative burden.</span></span>

<span data-ttu-id="df98c-108">StorSimple Manager 방문 페이지 hello 모든 hello StorSimple Manager 서비스를 사용할 수 있는 toomanage StorSimple 저장소 장치를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-108">hello StorSimple Manager landing page lists all hello StorSimple Manager services that you can use toomanage your StorSimple storage devices.</span></span> <span data-ttu-id="df98c-109">각 StorSimple Manager 서비스에 대해 다음 정보는 hello hello StorSimple 관리자 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-109">For each StorSimple Manager service, hello following information is presented on hello StorSimple Manager page:</span></span>

* <span data-ttu-id="df98c-110">**이름** – tooyour StorSimple Manager 서비스를 만들 때 할당 된 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-110">**Name** – hello name that was assigned tooyour StorSimple Manager service when it was created.</span></span> <span data-ttu-id="df98c-111">**hello 서비스를 만든 후에 hello 서비스 이름을 변경할 수 없습니다. 장치, 볼륨, 볼륨 컨테이너 및 백업 정책을 hello Azure 클래식 포털에서에서 이름을 바꿀 수 없는 같은 다른 엔터티에도 마찬가지 이기도 합니다.**</span><span class="sxs-lookup"><span data-stu-id="df98c-111">**hello service name cannot be changed after hello service is created. This is also true for other entities such as devices, volumes, volume containers, and backup policies that cannot be renamed in hello Azure classic portal.**</span></span>
* <span data-ttu-id="df98c-112">**상태** – 될 수 있는 hello 서비스의 상태를 hello **활성**, **만들기**, 또는 **온라인**합니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-112">**Status** – hello status of hello service, which can be **Active**, **Creating**, or **Online**.</span></span>
* <span data-ttu-id="df98c-113">**위치** – hello 지리적 위치는 hello StorSimple 장치 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-113">**Location** – hello geographical location in which hello StorSimple device will be deployed.</span></span>
* <span data-ttu-id="df98c-114">**구독** – hello 서비스와 연결 된 구독을 청구 합니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-114">**Subscription** – hello billing subscription that is associated with your service.</span></span>

<span data-ttu-id="df98c-115">hello hello StorSimple 관리자 페이지를 통해 수행할 수 있는 일반적인 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-115">hello common tasks that can be performed through hello StorSimple Manager page are:</span></span>

* <span data-ttu-id="df98c-116">서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="df98c-116">Create a service</span></span>
* <span data-ttu-id="df98c-117">서비스 삭제</span><span class="sxs-lookup"><span data-stu-id="df98c-117">Delete a service</span></span>
* <span data-ttu-id="df98c-118">Hello 서비스 등록 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="df98c-118">Get hello service registration key</span></span>
* <span data-ttu-id="df98c-119">Hello 서비스 등록 키 다시 생성</span><span class="sxs-lookup"><span data-stu-id="df98c-119">Regenerate hello service registration key</span></span>

<span data-ttu-id="df98c-120">이 자습서에서는 설명 방법을 각 tooperform 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-120">This tutorial describes how tooperform each of these tasks.</span></span>

## <a name="create-a-service"></a><span data-ttu-id="df98c-121">서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="df98c-121">Create a service</span></span>
<span data-ttu-id="df98c-122">사용 하 여 hello **빠른 생성** toocreate StorSimple Manager 서비스 toodeploy StorSimple 장치를 원하는 경우 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-122">Use hello **Quick Create** option toocreate a StorSimple Manager service if you want toodeploy your StorSimple device.</span></span> <span data-ttu-id="df98c-123">서비스 toocreate toohave가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-123">toocreate a service, you need toohave:</span></span>

* <span data-ttu-id="df98c-124">엔터프라이즈 계약을 사용하여 구독</span><span class="sxs-lookup"><span data-stu-id="df98c-124">A subscription with an Enterprise Agreement</span></span>
* <span data-ttu-id="df98c-125">활성 Microsoft Azure 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="df98c-125">An active Microsoft Azure storage account</span></span>
* <span data-ttu-id="df98c-126">hello 청구 액세스 관리에 사용 되는 정보</span><span class="sxs-lookup"><span data-stu-id="df98c-126">hello billing information that is used for access management</span></span>

<span data-ttu-id="df98c-127">선택할 수 있습니다도 toogenerate 기본 저장소 계정 hello 서비스를 만들 때.</span><span class="sxs-lookup"><span data-stu-id="df98c-127">You can also choose toogenerate a default storage account when you create hello service.</span></span>

<span data-ttu-id="df98c-128">하나의 서비스로 여러 장치를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-128">A single service can manage multiple devices.</span></span> <span data-ttu-id="df98c-129">하지만 하나의 장치는 여러 서비스로 확장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-129">However, a device cannot span multiple services.</span></span> <span data-ttu-id="df98c-130">대규모 엔터프라이즈는 여러 서비스 인스턴스 toowork 서로 다른 구독, 조직 또는 배포 위치를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-130">A large enterprise can have multiple service instances toowork with different subscriptions, organizations, or even deployment locations.</span></span> <span data-ttu-id="df98c-131">StorSimple Manager 서비스 toomanage StorSimple 8000 시리즈 장치 및 StorSimple 가상 배열의 인스턴스를 개별 필요한 note 하십시오.</span><span class="sxs-lookup"><span data-stu-id="df98c-131">Please note that you need separate instances of StorSimple Manager service toomanage StorSimple 8000 series devices and StorSimple Virtual Arrays.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="df98c-132">사용 하지 않는 서비스 (이 리소스에 대해 작업이 장치 없음)이 생성 하는 경우 이전 tooAugust 2016의 경우 Azure 포털 또는 Azure 클래식 포털을 통해 관리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-132">If you have an unused service created (no device operations were performed on this resource) prior tooAugust 2016, it cannot be managed via Azure portal or Azure classic portal.</span></span> <span data-ttu-id="df98c-133">Hello Azure 포털에서에서 새 서비스를 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-133">We recommend that you create a new service in hello Azure portal.</span></span>

<span data-ttu-id="df98c-134">다음 단계 toocreate 서비스는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-134">Perform hello following steps toocreate a service.</span></span>

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-create-new-service.md)]

## <a name="delete-a-service"></a><span data-ttu-id="df98c-135">서비스 삭제</span><span class="sxs-lookup"><span data-stu-id="df98c-135">Delete a service</span></span>
<span data-ttu-id="df98c-136">서비스를 삭제하기 전에 사용 중인 연결 장치가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-136">Before you delete a service, make sure that no connected devices are using it.</span></span> <span data-ttu-id="df98c-137">Hello 서비스를 사용 하는 경우 연결 된 hello 장치를 비활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-137">If hello service is in use, deactivate hello connected devices.</span></span> <span data-ttu-id="df98c-138">작업을 비활성화 하는 hello 서버 hello 장치와 hello 서비스 hello 연결 하지만 hello 클라우드에서 hello 장치 데이터를 보존 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-138">hello deactivate operation will sever hello connection between hello device and hello service, but preserve hello device data in hello cloud.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="df98c-139">서비스가 삭제 된 후에 hello 작업을 되돌릴 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-139">After a service is deleted, hello operation cannot be reversed.</span></span> <span data-ttu-id="df98c-140">Hello 서비스를 사용 하는 모든 장치 toobe 할 초기값으로 재설정 다른 서비스와 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-140">Any device that was using hello service will need toobe factory reset before it can be used with another service.</span></span> <span data-ttu-id="df98c-141">이 시나리오에서는 hello 구성 뿐만 아니라 hello 장치에서 hello 로컬 데이터가 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-141">In this scenario, hello local data on hello device, as well as hello configuration, will be lost.</span></span>

<span data-ttu-id="df98c-142">다음 단계 toodelete 서비스는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-142">Perform hello following steps toodelete a service.</span></span>

### <a name="toodelete-a-service"></a><span data-ttu-id="df98c-143">toodelete 서비스</span><span class="sxs-lookup"><span data-stu-id="df98c-143">toodelete a service</span></span>
1. <span data-ttu-id="df98c-144">Hello에 **StorSimple Manager 서비스** toodelete 한다고 hello 선택 서비스 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-144">On hello **StorSimple Manager service** page, select hello service that you wish toodelete.</span></span>
2. <span data-ttu-id="df98c-145">클릭 **삭제** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-145">Click **Delete** at hello bottom of hello page.</span></span>
3. <span data-ttu-id="df98c-146">클릭 **예** hello 알림이에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-146">Click **Yes** in hello confirmation notification.</span></span> <span data-ttu-id="df98c-147">삭제 하는 hello 서비스 toobe 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-147">It may take a few minutes for hello service toobe deleted.</span></span>

## <a name="get-hello-service-registration-key"></a><span data-ttu-id="df98c-148">Hello 서비스 등록 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="df98c-148">Get hello service registration key</span></span>
<span data-ttu-id="df98c-149">서비스를 성공적으로 만든 후 hello 서비스와 StorSimple 장치의 tooregister 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-149">After you have successfully created a service, you will need tooregister your StorSimple device with hello service.</span></span> <span data-ttu-id="df98c-150">tooregister 첫 번째 StorSimple 장치의 서비스 등록 키 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-150">tooregister your first StorSimple device, you will need hello service registration key.</span></span> <span data-ttu-id="df98c-151">tooregister 기존 StorSimple 서비스와 장치를 추가할 필요가 hello 등록 키와 hello 서비스 데이터 암호화 키 (생성 된 hello 첫 번째 장치에 등록 하는 동안) 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-151">tooregister additional devices with an existing StorSimple service, you will need both hello registration key and hello service data encryption key (which is generated on hello first device during registration).</span></span> <span data-ttu-id="df98c-152">Hello 서비스 데이터 암호화 키에 대 한 자세한 내용은 참조 [StorSimple 보안](storsimple-security.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-152">For more information about hello service data encryption key, see [StorSimple security](storsimple-security.md).</span></span> <span data-ttu-id="df98c-153">에 액세스 하 여 hello 등록 키를 받을 수 **등록 키** hello에 **서비스** 페이지.</span><span class="sxs-lookup"><span data-stu-id="df98c-153">You can get hello registration key by accessing **Registration Key** on hello **Services** page.</span></span>

<span data-ttu-id="df98c-154">Hello 단계 tooget hello 서비스 등록 키를 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-154">Perform hello following steps tooget hello service registration key.</span></span>

[!INCLUDE [storsimple-get-service-registration-key](../../includes/storsimple-get-service-registration-key.md)]

<span data-ttu-id="df98c-155">Hello 서비스 등록 키를 안전한 위치에 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-155">Keep hello service registration key in a safe location.</span></span> <span data-ttu-id="df98c-156">이 키를으로 hello 서비스 데이터 암호화 키를이 서비스를 사용 하 여 추가 장치 tooregister 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-156">You will need this key, as well as hello service data encryption key, tooregister additional devices with this service.</span></span> <span data-ttu-id="df98c-157">Hello 서비스 등록 키를 얻은 후 StorSimple 인터페이스에 대 한 tooconfigure에 hello Windows PowerShell을 통해 장치가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-157">After obtaining hello service registration key, you will need tooconfigure your device through hello Windows PowerShell for StorSimple interface.</span></span>

<span data-ttu-id="df98c-158">방법에 대 한 자세한 내용은 toouse이 등록 키가 참조 [3 단계: 구성 및 StorSimple 용 Windows PowerShell을 통해 hello 장치를 등록](storsimple-deployment-walkthrough.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple)합니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-158">For details on how toouse this registration key, see [Step 3: Configure and register hello device through Windows PowerShell for StorSimple](storsimple-deployment-walkthrough.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span></span>

## <a name="regenerate-hello-service-registration-key"></a><span data-ttu-id="df98c-159">Hello 서비스 등록 키 다시 생성</span><span class="sxs-lookup"><span data-stu-id="df98c-159">Regenerate hello service registration key</span></span>
<span data-ttu-id="df98c-160">필요한 tooperform 키 회전 또는 서비스 관리자 목록이 hello에 변경 되었는지 여부 tooregenerate 서비스 등록 키가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-160">You will need tooregenerate a service registration key if you are required tooperform key rotation or if hello list of service administrators has changed.</span></span> <span data-ttu-id="df98c-161">Hello 키를 다시 생성 하면 hello 새 키는 후속 장치를 등록 하는 중에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-161">When you regenerate hello key, hello new key is used only for registering subsequent devices.</span></span> <span data-ttu-id="df98c-162">이미 등록 된 hello 장치가이 프로세스에 의해 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-162">hello devices that were already registered are unaffected by this process.</span></span>

<span data-ttu-id="df98c-163">Hello 단계 tooregenerate 서비스 등록 키가 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-163">Perform hello following steps tooregenerate a service registration key.</span></span>

### <a name="tooregenerate-hello-service-registration-key"></a><span data-ttu-id="df98c-164">tooregenerate hello 서비스 등록 키</span><span class="sxs-lookup"><span data-stu-id="df98c-164">tooregenerate hello service registration key</span></span>
1. <span data-ttu-id="df98c-165">Hello에 **StorSimple Manager 서비스** 페이지 **등록 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-165">On hello **StorSimple Manager service** page, click **Registration Key**.</span></span>
2. <span data-ttu-id="df98c-166">Hello에 **서비스 등록 키** 대화 상자를 클릭 **다시 생성**합니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-166">In hello **Service Registration Key** dialog box, click **Regenerate**.</span></span>
3. <span data-ttu-id="df98c-167">확인 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-167">You will see a confirmation message.</span></span> <span data-ttu-id="df98c-168">클릭 **확인** toocontinue와 hello 재생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-168">Click **OK** toocontinue with hello regeneration.</span></span>
4. <span data-ttu-id="df98c-169">새 서비스 등록 키가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-169">A new service registration key will appear.</span></span>
5. <span data-ttu-id="df98c-170">이 서비스에 새 장치 등록을 위해 이 키를 복사하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-170">Copy this key and save it for registering any new devices with this service.</span></span>
6. <span data-ttu-id="df98c-171">Hello 확인 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-171">Click hello check icon</span></span> ![확인 아이콘](./media/storsimple-manage-service/HCS_CheckIcon.png) <span data-ttu-id="df98c-173">tooclose이 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="df98c-173">tooclose this dialog box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="df98c-174">다음 단계</span><span class="sxs-lookup"><span data-stu-id="df98c-174">Next steps</span></span>
* <span data-ttu-id="df98c-175">Hello에 대 한 자세한 [StorSimple 배포 프로세스](storsimple-deployment-walkthrough-u2.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-175">Learn more about hello [StorSimple deployment process](storsimple-deployment-walkthrough-u2.md).</span></span>
* <span data-ttu-id="df98c-176">[StorSimple 저장소 계정 관리](storsimple-manage-storage-accounts.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-176">Learn more about [managing your StorSimple storage account](storsimple-manage-storage-accounts.md).</span></span>
* <span data-ttu-id="df98c-177">너무 방법에 대 한 자세한[사용 하 여 StorSimple 장치를 StorSimple Manager 서비스 tooadminister hello](storsimple-manager-service-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="df98c-177">Learn more about how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>
