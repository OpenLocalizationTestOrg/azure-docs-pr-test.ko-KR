---
title: "StorSimple 장치 관리자 서비스 aaaDeploy | Microsoft Docs"
description: "어떻게 toocreate 및 delete hello hello Azure 포털에서에서 StorSimple 장치 관리자 서비스에 설명 하 고 toomanage 서비스 등록 키를 hello 하는 방법을 설명 합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 28499494-8c4d-4a7f-9d44-94b2b8a93c93
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: alkohli
ms.openlocfilehash: 9064053addc7b3dfcce08b47e81b38c2e0e1b559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-device-manager-service-for-storsimple-virtual-array"></a><span data-ttu-id="2e131-103">StorSimple 가상 배열에 대 한 hello StorSimple 장치 관리자 서비스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-103">Deploy hello StorSimple Device Manager service for StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="2e131-104">개요</span><span class="sxs-lookup"><span data-stu-id="2e131-104">Overview</span></span>

<span data-ttu-id="2e131-105">hello StorSimple 장치 관리자 서비스는 Microsoft Azure에서 실행 하 고 toomultiple StorSimple 장치를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-105">hello StorSimple Device Manager service runs in Microsoft Azure and connects toomultiple StorSimple devices.</span></span> <span data-ttu-id="2e131-106">Hello 서비스를 만든 후 toomanage hello 장치 hello Microsoft Azure 포털에서 실행 되는 브라우저에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-106">After you create hello service, you can use it toomanage hello devices from hello Microsoft Azure portal running in a browser.</span></span> <span data-ttu-id="2e131-107">이렇게 하면 모든 hello 장치에 연결 된 toohello StorSimple 장치 관리자 하므로 관리 부담이 최소화 하나의 중앙 위치에서 서비스 toomonitor 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-107">This allows you toomonitor all hello devices that are connected toohello StorSimple Device Manager service from a single, central location, thereby minimizing administrative burden.</span></span>

<span data-ttu-id="2e131-108">hello 일반적인 작업 관련된 tooa StorSimple 장치 관리자 서비스는.</span><span class="sxs-lookup"><span data-stu-id="2e131-108">hello common tasks related tooa StorSimple Device Manager service are:</span></span>

* <span data-ttu-id="2e131-109">서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="2e131-109">Create a service</span></span>
* <span data-ttu-id="2e131-110">서비스 삭제</span><span class="sxs-lookup"><span data-stu-id="2e131-110">Delete a service</span></span>
* <span data-ttu-id="2e131-111">Hello 서비스 등록 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="2e131-111">Get hello service registration key</span></span>
* <span data-ttu-id="2e131-112">Hello 서비스 등록 키 다시 생성</span><span class="sxs-lookup"><span data-stu-id="2e131-112">Regenerate hello service registration key</span></span>

<span data-ttu-id="2e131-113">이 자습서에서는 각 tooperform의 선행 작업 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-113">This tutorial describes how tooperform each of hello preceding tasks.</span></span> <span data-ttu-id="2e131-114">이 문서에 포함 된 hello 정보에만 적용 가능한 tooStorSimple 가상 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-114">hello information contained in this article is applicable only tooStorSimple Virtual Arrays.</span></span> <span data-ttu-id="2e131-115">StorSimple 8000 시리즈에 대 한 자세한 내용은 이동 너무[StorSimple Manager 서비스를 배포](storsimple-manage-service.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-115">For more information on StorSimple 8000 series, go too[deploy a StorSimple Manager service](storsimple-manage-service.md).</span></span>

## <a name="create-a-service"></a><span data-ttu-id="2e131-116">서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="2e131-116">Create a service</span></span>

<span data-ttu-id="2e131-117">서비스 toocreate toohave가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-117">toocreate a service, you need toohave:</span></span>

* <span data-ttu-id="2e131-118">엔터프라이즈 계약을 사용하여 구독</span><span class="sxs-lookup"><span data-stu-id="2e131-118">A subscription with an Enterprise Agreement</span></span>
* <span data-ttu-id="2e131-119">활성 Microsoft Azure 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="2e131-119">An active Microsoft Azure storage account</span></span>
* <span data-ttu-id="2e131-120">hello 청구 액세스 관리에 사용 되는 정보</span><span class="sxs-lookup"><span data-stu-id="2e131-120">hello billing information that is used for access management</span></span>

<span data-ttu-id="2e131-121">선택할 수 있습니다도 toogenerate 저장소 계정을 hello 서비스를 만들 때.</span><span class="sxs-lookup"><span data-stu-id="2e131-121">You can also choose toogenerate a storage account when you create hello service.</span></span>

<span data-ttu-id="2e131-122">하나의 서비스로 여러 장치를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-122">A single service can manage multiple devices.</span></span> <span data-ttu-id="2e131-123">하지만 하나의 장치는 여러 서비스로 확장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-123">However, a device cannot span multiple services.</span></span> <span data-ttu-id="2e131-124">대규모 엔터프라이즈는 여러 서비스 인스턴스 toowork 서로 다른 구독, 조직 또는 배포 위치를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-124">A large enterprise can have multiple service instances toowork with different subscriptions, organizations, or even deployment locations.</span></span>

> [!NOTE]
> <span data-ttu-id="2e131-125">StorSimple 장치 관리자 서비스 toomanage StorSimple 8000 시리즈 장치 및 StorSimple 가상 배열의 별도 인스턴스 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-125">You need separate instances of StorSimple Device Manager service toomanage StorSimple 8000 series devices and StorSimple Virtual Arrays.</span></span>


<span data-ttu-id="2e131-126">다음 단계 toocreate 서비스는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-126">Perform hello following steps toocreate a service.</span></span>

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

## <a name="delete-a-service"></a><span data-ttu-id="2e131-127">서비스 삭제</span><span class="sxs-lookup"><span data-stu-id="2e131-127">Delete a service</span></span>

<span data-ttu-id="2e131-128">서비스를 삭제하기 전에 사용 중인 연결 장치가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-128">Before you delete a service, make sure that no connected devices are using it.</span></span> <span data-ttu-id="2e131-129">Hello 서비스를 사용 하는 경우 연결 된 hello 장치를 비활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-129">If hello service is in use, deactivate hello connected devices.</span></span> <span data-ttu-id="2e131-130">작업을 비활성화 하는 hello 서버 hello 장치와 hello 서비스 hello 연결 하지만 hello 클라우드에서 hello 장치 데이터를 보존 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-130">hello deactivate operation will sever hello connection between hello device and hello service, but preserve hello device data in hello cloud.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2e131-131">서비스가 삭제 된 후에 hello 작업을 되돌릴 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-131">After a service is deleted, hello operation cannot be reversed.</span></span> <span data-ttu-id="2e131-132">Hello 서비스를 사용 하는 모든 장치 toobe 할 초기값으로 재설정 다른 서비스와 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-132">Any device that was using hello service will need toobe factory reset before it can be used with another service.</span></span> <span data-ttu-id="2e131-133">이 시나리오에서는 hello 구성 뿐만 아니라 hello 장치에서 hello 로컬 데이터가 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-133">In this scenario, hello local data on hello device, as well as hello configuration, will be lost.</span></span>
 

<span data-ttu-id="2e131-134">다음 단계 toodelete 서비스는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-134">Perform hello following steps toodelete a service.</span></span>

#### <a name="toodelete-a-service"></a><span data-ttu-id="2e131-135">toodelete 서비스</span><span class="sxs-lookup"><span data-stu-id="2e131-135">toodelete a service</span></span>

1. <span data-ttu-id="2e131-136">너무 이동**모든 리소스**합니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-136">Go too**All resources**.</span></span> <span data-ttu-id="2e131-137">StorSimple Device Manager 서비스를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-137">Search for your StorSimple Device Manager service.</span></span> <span data-ttu-id="2e131-138">원하는 toodelete hello 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-138">Select hello service that you wish toodelete.</span></span>
   
    ![서비스 toodelete 선택](./media/storsimple-virtual-array-manage-service/deleteservice2.png)
2. <span data-ttu-id="2e131-140">이동 tooyour 서비스 대시보드 tooensure는 연결 된 toohello 서비스는 장치가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-140">Go tooyour service dashboard tooensure there are no devices connected toohello service.</span></span> <span data-ttu-id="2e131-141">이 서비스에 등록 된 장치가 경우 배너 메시지 toohello 효과를 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-141">If there are no devices registered with this service, you will also see a banner message toohello effect.</span></span> <span data-ttu-id="2e131-142">**삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-142">Click **Delete**.</span></span>
   
    ![서비스 삭제](./media/storsimple-virtual-array-manage-service/deleteservice3.png)

3. <span data-ttu-id="2e131-144">확인 메시지가 나타나면 클릭 **예** hello 알림이에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-144">When prompted for confirmation, click **Yes** in hello confirmation notification.</span></span> 
   
    ![서비스 삭제 확인](./media/storsimple-virtual-array-manage-service/deleteservice4.png)
4. <span data-ttu-id="2e131-146">삭제 하는 hello 서비스 toobe 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-146">It may take a few minutes for hello service toobe deleted.</span></span> <span data-ttu-id="2e131-147">Hello 후 서비스가 성공적으로 삭제 된 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-147">After hello service is successfully deleted, you will be notified.</span></span>
   
    ![성공적인 서비스 삭제](./media/storsimple-virtual-array-manage-service/deleteservice6.png)

<span data-ttu-id="2e131-149">서비스의 hello 목록이 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-149">hello list of services will be refreshed.</span></span>

 ![업데이트된 서비스 목록](./media/storsimple-virtual-array-manage-service/deleteservice7.png)

## <a name="get-hello-service-registration-key"></a><span data-ttu-id="2e131-151">Hello 서비스 등록 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="2e131-151">Get hello service registration key</span></span>
<span data-ttu-id="2e131-152">서비스를 성공적으로 만든 후 hello 서비스와 StorSimple 장치의 tooregister 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-152">After you have successfully created a service, you will need tooregister your StorSimple device with hello service.</span></span> <span data-ttu-id="2e131-153">tooregister 첫 번째 StorSimple 장치의 서비스 등록 키 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-153">tooregister your first StorSimple device, you will need hello service registration key.</span></span> <span data-ttu-id="2e131-154">tooregister 기존 StorSimple 서비스와 장치를 추가할 필요가 hello 등록 키와 hello 서비스 데이터 암호화 키 (생성 된 hello 첫 번째 장치에 등록 하는 동안) 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-154">tooregister additional devices with an existing StorSimple service, you will need both hello registration key and hello service data encryption key (which is generated on hello first device during registration).</span></span> <span data-ttu-id="2e131-155">Hello 서비스 데이터 암호화 키에 대 한 자세한 내용은 참조 [StorSimple 보안](storsimple-security.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-155">For more information about hello service data encryption key, see [StorSimple security](storsimple-security.md).</span></span> <span data-ttu-id="2e131-156">Hello에 액세스 하 여 hello 등록 키를 받을 수 **키** 블레이드 서비스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-156">You can get hello registration key by accessing hello **Keys** blade for your service.</span></span>

<span data-ttu-id="2e131-157">Hello 단계 tooget hello 서비스 등록 키를 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-157">Perform hello following steps tooget hello service registration key.</span></span>

#### <a name="tooget-hello-service-registration-key"></a><span data-ttu-id="2e131-158">tooget hello 서비스 등록 키</span><span class="sxs-lookup"><span data-stu-id="2e131-158">tooget hello service registration key</span></span>
1. <span data-ttu-id="2e131-159">Hello에 **StorSimple 장치 관리자** 블레이드에서 너무 이동**관리 &gt;**  **키**합니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-159">In hello **StorSimple Device Manager** blade, go too**Management &gt;** **Keys**.</span></span>
   
   ![키 블레이드](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="2e131-161">Hello에 **키** 블레이드에서 서비스 등록 키가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-161">In hello **Keys** blade, a service registration key appears.</span></span> <span data-ttu-id="2e131-162">Hello 복사 아이콘을 사용 하 여 hello 등록 키를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-162">Copy hello registration key using hello copy icon.</span></span> 

<span data-ttu-id="2e131-163">Hello 서비스 등록 키를 안전한 위치에 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-163">Keep hello service registration key in a safe location.</span></span> <span data-ttu-id="2e131-164">이 키를으로 hello 서비스 데이터 암호화 키를이 서비스를 사용 하 여 추가 장치 tooregister 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-164">You will need this key, as well as hello service data encryption key, tooregister additional devices with this service.</span></span> <span data-ttu-id="2e131-165">Hello 서비스 등록 키를 얻은 후 StorSimple 인터페이스에 대 한 tooconfigure에 hello Windows PowerShell을 통해 장치가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-165">After obtaining hello service registration key, you will need tooconfigure your device through hello Windows PowerShell for StorSimple interface.</span></span>

## <a name="regenerate-hello-service-registration-key"></a><span data-ttu-id="2e131-166">Hello 서비스 등록 키 다시 생성</span><span class="sxs-lookup"><span data-stu-id="2e131-166">Regenerate hello service registration key</span></span>
<span data-ttu-id="2e131-167">필요한 tooperform 키 회전 또는 서비스 관리자 목록이 hello에 변경 되었는지 여부 tooregenerate 서비스 등록 키가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-167">You will need tooregenerate a service registration key if you are required tooperform key rotation or if hello list of service administrators has changed.</span></span> <span data-ttu-id="2e131-168">Hello 키를 다시 생성 하면 hello 새 키는 후속 장치를 등록 하는 중에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-168">When you regenerate hello key, hello new key is used only for registering subsequent devices.</span></span> <span data-ttu-id="2e131-169">이미 등록 된 hello 장치가이 프로세스에 의해 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-169">hello devices that were already registered are unaffected by this process.</span></span>

<span data-ttu-id="2e131-170">Hello 단계 tooregenerate 서비스 등록 키가 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-170">Perform hello following steps tooregenerate a service registration key.</span></span>

#### <a name="tooregenerate-hello-service-registration-key"></a><span data-ttu-id="2e131-171">tooregenerate hello 서비스 등록 키</span><span class="sxs-lookup"><span data-stu-id="2e131-171">tooregenerate hello service registration key</span></span>
1. <span data-ttu-id="2e131-172">Hello에 **StorSimple 장치 관리자** 블레이드에서 너무 이동**관리 &gt;**  **키**합니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-172">In hello **StorSimple Device Manager** blade, go too**Management &gt;** **Keys**.</span></span>
   
   ![키 블레이드](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="2e131-174">Hello에 **키** 블레이드에서 클릭 **다시 생성**합니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-174">In hello **Keys** blade, click **Regenerate**.</span></span>
   
   ![다시 생성 클릭](./media/storsimple-virtual-array-manage-service/getregkey5.png)
3. <span data-ttu-id="2e131-176">Hello에 **Regenerate 서비스 등록 키** 블레이드를 검토 hello 작업 때 필요한 hello 키 다시 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-176">In hello **Regenerate service registration key** blade, review hello action required when hello keys are regenerated.</span></span> <span data-ttu-id="2e131-177">이 서비스에 등록 된 하는 모든 hello 후속 장치 hello 새 등록 키를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-177">All hello subsequent devices that are registered with this service will use hello new registration key.</span></span> <span data-ttu-id="2e131-178">클릭 **다시 생성** tooconfirm 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-178">Click **Regenerate** tooconfirm.</span></span> <span data-ttu-id="2e131-179">Hello 등록 완료 되 면 알림이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-179">You will be notified after hello registration is complete.</span></span>
   
   ![다시 생성 키 확인](./media/storsimple-virtual-array-manage-service/getregkey3.png)
4. <span data-ttu-id="2e131-181">새 서비스 등록 키가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-181">A new service registration key will appear.</span></span>
   
    ![다시 생성 키 확인](./media/storsimple-virtual-array-manage-service/getregkey4.png)
   
   <span data-ttu-id="2e131-183">이 서비스에 새 장치 등록을 위해 이 키를 복사하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-183">Copy this key and save it for registering any new devices with this service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e131-184">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2e131-184">Next steps</span></span>
* <span data-ttu-id="2e131-185">너무 방법에 대해 알아봅니다[시작](storsimple-virtual-array-deploy1-portal-prep.md) StorSimple 가상 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-185">Learn how too[get started](storsimple-virtual-array-deploy1-portal-prep.md) with a StorSimple Virtual Array.</span></span>
* <span data-ttu-id="2e131-186">너무 방법에 대해 알아봅니다[StorSimple 장치를 관리할](storsimple-ova-web-ui-admin.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2e131-186">Learn how too[administer your StorSimple device](storsimple-ova-web-ui-admin.md).</span></span>

