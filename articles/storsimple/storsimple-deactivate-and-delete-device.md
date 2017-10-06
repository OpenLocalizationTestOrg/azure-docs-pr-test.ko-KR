---
title: "aaaDeactivate StorSimple 장치를 삭제 하 고 | Microsoft Docs"
description: "설명 방법을 tooremove StorSimple 장치에서 서비스를 먼저 비활성화 한 후이 삭제 합니다."
services: storsimple
documentationcenter: 
author: SharS
manager: timlt
editor: 
ms.assetid: 155cda38-c5ae-45dc-b7e8-6444494afc9e
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: anbacker
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ed86bcd089aa957128e14b1709c836d938c131a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-8000-series-device-via-storsimple-manager-service"></a><span data-ttu-id="0fbad-103">StorSimple Manager 서비스를 통해 StorSimple 8000 시리즈 장치 비활성화 및 삭제</span><span class="sxs-lookup"><span data-stu-id="0fbad-103">Deactivate and delete a StorSimple 8000 series device via StorSimple Manager service</span></span>
## <a name="overview"></a><span data-ttu-id="0fbad-104">개요</span><span class="sxs-lookup"><span data-stu-id="0fbad-104">Overview</span></span>
<span data-ttu-id="0fbad-105">(예를 들어 교체 하거나 장치를 업그레이드 하는 경우 또는 StorSimple 더 이상 사용 하는 경우) 서비스에서 StorSimple 장치 tootake을 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-105">You may wish tootake a StorSimple device out of service (for example, if you are replacing or upgrading your device or if you are no longer using StorSimple).</span></span> <span data-ttu-id="0fbad-106">Hello 대/소문자 이면 toodeactivate hello 장치를 삭제 하기 전에 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-106">If this is hello case, you will need toodeactivate hello device before you can delete it.</span></span> <span data-ttu-id="0fbad-107">Hello 장치와 StorSimple Manager 서비스를 해당 하는 hello hello 연결을 서버를 비활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-107">Deactivating severs hello connection between hello device and hello corresponding StorSimple Manager service.</span></span> <span data-ttu-id="0fbad-108">이 자습서에 설명 방법을 tooremove 먼저 비활성화 및 삭제 하 여 서비스에서 StorSimple 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-108">This tutorial explains how tooremove a StorSimple device from service by first deactivating it and then deleting it.</span></span> 

<span data-ttu-id="0fbad-109">장치를 비활성화 하면 hello 장치에서 로컬로 저장 된 모든 데이터는 더 이상 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-109">When you deactivate a device, any data that was stored locally on hello device will no longer be accessible.</span></span> <span data-ttu-id="0fbad-110">Hello 클라우드에 저장 된 hello 장치와 연결 된 hello 데이터만 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-110">Only hello data associated with hello device that was stored in hello cloud can be recovered.</span></span>  

> [!WARNING]
> <span data-ttu-id="0fbad-111">비활성화는 영구 작업이며 실행 취소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-111">Deactivation is a PERMANENT operation and cannot be undone.</span></span> <span data-ttu-id="0fbad-112">비활성화 된 장치는 먼저 toohello 출하 시 기본 설정 다시 설정 하지 않은 hello StorSimple Manager 서비스에 등록할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-112">A deactivated device cannot be registered with hello StorSimple Manager service unless it is first reset toohello default factory settings.</span></span> 
> 
> <span data-ttu-id="0fbad-113">hello 공장 기본 장치에서 로컬로 저장 된 모든 hello 데이터 프로세스 삭제를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-113">hello factory reset process deletes all hello data that was stored locally on your device.</span></span> <span data-ttu-id="0fbad-114">따라서 반드시 장치를 비장치를 비활성화하기 전에 모든 데이터의 클라우드 스냅숏을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-114">Therefore, it is essential that you take a cloud snapshot of all your data before you deactivate a device.</span></span> <span data-ttu-id="0fbad-115">이렇게 하면 toorecover 이후 단계에서 데이터를 hello 모든 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-115">This will allow you toorecover all hello data at a later stage.</span></span>
> 
> 

<span data-ttu-id="0fbad-116">이 자습서에서는 다음을 수행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-116">This tutorial explains how to:</span></span>

* <span data-ttu-id="0fbad-117">장치를 비활성화 하 고 hello 데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="0fbad-117">Deactivate a device and delete hello data</span></span>
* <span data-ttu-id="0fbad-118">장치를 비활성화 하 고 hello 데이터 보존</span><span class="sxs-lookup"><span data-stu-id="0fbad-118">Deactivate a device and retain hello data</span></span>

<span data-ttu-id="0fbad-119">StorSimple 가상 장치에서 비활성화 및 삭제가 어떻게 작동하는지도 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-119">It also explains how deactivation and deletion works on a StorSimple virtual device.</span></span>

> [!NOTE]
> <span data-ttu-id="0fbad-120">StorSimple 물리적 또는 가상 장치를 비활성화 하기 전에 toostop 있는지 확인 하거나 클라이언트와 해당 장치에 종속 된 호스트를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-120">Before you deactivate a StorSimple physical or virtual device, make sure toostop or delete clients and hosts that depend on that device.</span></span>
> 
> 

## <a name="deactivate-and-delete-data"></a><span data-ttu-id="0fbad-121">데이터 비활성화 및 삭제</span><span class="sxs-lookup"><span data-stu-id="0fbad-121">Deactivate and delete data</span></span>
<span data-ttu-id="0fbad-122">Hello 장치를 완전히 삭제 하 고 hello 장치에 tooretain hello 데이터 하지 않을 경우 다음 단계를 수행 하는 hello를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-122">If you are interested in deleting hello device completely and do not want tooretain hello data on hello device, then complete hello following steps.</span></span>

#### <a name="toodeactivate-hello-device-and-delete-hello-data"></a><span data-ttu-id="0fbad-123">toodeactivate hello 장치 및 delete hello 데이터</span><span class="sxs-lookup"><span data-stu-id="0fbad-123">toodeactivate hello device and delete hello data</span></span>
1. <span data-ttu-id="0fbad-124">이전 toodeactivating 장치, 모든 hello 볼륨 컨테이너 (및 hello 볼륨) hello 장치와 연결 된 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-124">Prior toodeactivating a device, you must delete all hello volume containers (and hello volumes) associated with hello device.</span></span> <span data-ttu-id="0fbad-125">연결 된 hello 백업을 삭제 한 후에 볼륨 컨테이너를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-125">You can delete volume containers only after you have deleted hello associated backups.</span></span>
2. <span data-ttu-id="0fbad-126">다음과 같이 hello 장치를 비활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-126">Deactivate hello device as follows:</span></span>
   
   1. <span data-ttu-id="0fbad-127">Hello StorSimple Manager 서비스에서 **장치** 페이지, 선택 hello 장치 toodeactivate 원하는, hello 페이지의 맨 아래 hello에 클릭 **비활성화**합니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-127">On hello StorSimple Manager service **Devices** page, select hello device that you wish toodeactivate and, at hello bottom of hello page, click **Deactivate**.</span></span>
   2. <span data-ttu-id="0fbad-128">확인 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-128">A confirmation message will appear.</span></span> <span data-ttu-id="0fbad-129">클릭 **예** toocontinue 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-129">Click **Yes** toocontinue.</span></span> <span data-ttu-id="0fbad-130">hello 비활성화 프로세스가 시작 되 고 몇 분 toocomplete 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-130">hello deactivate process will start and take a few minutes toocomplete.</span></span>
3. <span data-ttu-id="0fbad-131">비활성화 한 후 hello 장치를 완전히 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-131">After deactivation, you can delete hello device completely.</span></span> <span data-ttu-id="0fbad-132">장치 삭제 장치 toohello 연결 된 서비스의 hello 목록에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-132">Deleting a device removes it from hello list of devices connected toohello service.</span></span> <span data-ttu-id="0fbad-133">그런 다음 hello 서비스 삭제 hello 장치를 더 이상 관리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-133">hello service can then no longer manage hello deleted device.</span></span> <span data-ttu-id="0fbad-134">다음 단계 toodelete hello 장치 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-134">Use hello following steps toodelete hello device:</span></span>
   
   1. <span data-ttu-id="0fbad-135">Hello StorSimple Manager 서비스에서 **장치** 페이지에서 원하는 toodelete 비활성화 된 장치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-135">On hello StorSimple Manager service **Devices** page, select a deactivated device that you wish toodelete.</span></span>
   2. <span data-ttu-id="0fbad-136">Hello hello 페이지 아래쪽에서 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-136">On hello bottom on hello page, click **Delete**.</span></span>
   3. <span data-ttu-id="0fbad-137">확인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-137">You will be prompted for confirmation.</span></span> <span data-ttu-id="0fbad-138">클릭 **예** toocontinue 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-138">Click **Yes** toocontinue.</span></span>
      
      <span data-ttu-id="0fbad-139">삭제 하는 hello 장치 toobe 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-139">It may take a few minutes for hello device toobe deleted.</span></span>

## <a name="deactivate-and-retain-data"></a><span data-ttu-id="0fbad-140">데이터 비활성화 및 보존</span><span class="sxs-lookup"><span data-stu-id="0fbad-140">Deactivate and retain data</span></span>
<span data-ttu-id="0fbad-141">관심 있는 hello 장치를 삭제 해도 tooretain hello 데이터를 원하는 경우 다음 단계를 수행 하는 hello를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-141">If you are interested in deleting hello device but want tooretain hello data, then complete hello following steps.</span></span>

#### <a name="toodeactivate-a-device-and-retain-hello-data"></a><span data-ttu-id="0fbad-142">장치 toodeactivate hello 데이터를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-142">toodeactivate a device and retain hello data</span></span>
1. <span data-ttu-id="0fbad-143">Hello 장치를 비활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-143">Deactivate hello device.</span></span> <span data-ttu-id="0fbad-144">모든 볼륨 컨테이너를 hello 및 hello 장치의 hello 스냅숏은 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-144">All hello volume containers and hello snapshots of hello device will remain.</span></span>
   
   1. <span data-ttu-id="0fbad-145">Hello StorSimple Manager 서비스에서 **장치** 페이지, 선택 hello 장치 toodeactivate 원하는, hello 페이지의 맨 아래 hello에 클릭 **비활성화**합니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-145">On hello StorSimple Manager service **Devices** page, select hello device that you wish toodeactivate and, at hello bottom of hello page, click **Deactivate**.</span></span>
   2. <span data-ttu-id="0fbad-146">확인 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-146">A confirmation message will appear.</span></span> <span data-ttu-id="0fbad-147">클릭 **예** toocontinue 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-147">Click **Yes** toocontinue.</span></span> <span data-ttu-id="0fbad-148">hello 비활성화 프로세스가 시작 되 고 몇 분 toocomplete 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-148">hello deactivate process will start and take a few minutes toocomplete.</span></span>
2. <span data-ttu-id="0fbad-149">이제 hello 볼륨 컨테이너와 연결 된 hello 스냅숏을 조치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-149">You can now fail over hello volume containers and hello associated snapshots.</span></span> <span data-ttu-id="0fbad-150">너무 절차를 보려면[StorSimple 장치에 대 한 장애 조치 및 재해 복구](storsimple-device-failover-disaster-recovery.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-150">For procedures, go too[Failover and disaster recovery for your StorSimple device](storsimple-device-failover-disaster-recovery.md).</span></span>
3. <span data-ttu-id="0fbad-151">비활성화 및 장애 조치 후 hello 장치를 완전히 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-151">After deactivation and failover, you can delete hello device completely.</span></span> <span data-ttu-id="0fbad-152">장치 삭제 장치 toohello 연결 된 서비스의 hello 목록에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-152">Deleting a device removes it from hello list of devices connected toohello service.</span></span> <span data-ttu-id="0fbad-153">그런 다음 hello 서비스 삭제 hello 장치를 더 이상 관리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-153">hello service can then no longer manage hello deleted device.</span></span> <span data-ttu-id="0fbad-154">다음 단계 toodelete hello 장치 hello를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-154">Complete hello following steps toodelete hello device:</span></span>
   
   1. <span data-ttu-id="0fbad-155">Hello StorSimple Manager 서비스에서 **장치** 페이지에서 원하는 toodelete 비활성화 된 장치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-155">On hello StorSimple Manager service **Devices** page, select a deactivated device that you wish toodelete.</span></span>
   2. <span data-ttu-id="0fbad-156">Hello hello 페이지 아래쪽에서 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-156">On hello bottom on hello page, click **Delete**.</span></span>
   3. <span data-ttu-id="0fbad-157">확인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-157">You will be prompted for confirmation.</span></span> <span data-ttu-id="0fbad-158">클릭 **예** toocontinue 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-158">Click **Yes** toocontinue.</span></span>
      
      <span data-ttu-id="0fbad-159">삭제 하는 hello 장치 toobe 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-159">It may take a few minutes for hello device toobe deleted.</span></span>

## <a name="deactivate-and-delete-a-virtual-device"></a><span data-ttu-id="0fbad-160">가상 장치 비활성화 및 삭제</span><span class="sxs-lookup"><span data-stu-id="0fbad-160">Deactivate and delete a virtual device</span></span>
<span data-ttu-id="0fbad-161">StorSimple 가상 장치에 대 한 비활성화 hello 가상 컴퓨터를 할당 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-161">For a StorSimple virtual device, deactivation deallocates hello virtual machine.</span></span> <span data-ttu-id="0fbad-162">그런 다음 hello 가상 컴퓨터 및 프로 비전 된 경우 생성 된 hello 리소스를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-162">You can then delete hello virtual machine and hello resources created when it was provisioned.</span></span> <span data-ttu-id="0fbad-163">Hello 가상 장치를 비활성화 한 후 수 없습니다 tooits 이전 상태로 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-163">After hello virtual device is deactivated, it cannot be restored tooits previous state.</span></span> 

<span data-ttu-id="0fbad-164">작업을 수행 하는 hello에 비활성화 결과:</span><span class="sxs-lookup"><span data-stu-id="0fbad-164">Deactivation results in hello following actions:</span></span>

* <span data-ttu-id="0fbad-165">hello StorSimple 가상 장치 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-165">hello StorSimple virtual device is removed.</span></span>
* <span data-ttu-id="0fbad-166">hello OSDisk 및 hello StorSimple 가상 장치에 대해 생성 된 데이터 디스크 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-166">hello OSDisk and Data Disks created for hello StorSimple virtual device are removed.</span></span>
* <span data-ttu-id="0fbad-167">hello 호스 티 드 서비스 및 가상 네트워크를 프로 비전 중에 만들어진 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-167">hello Hosted Service and Virtual Network that were created during provisioning are retained.</span></span> <span data-ttu-id="0fbad-168">이러한 엔터티를 사용하지 않는 경우 수동으로 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-168">If you are not using these entities, you should delete them manually.</span></span>
* <span data-ttu-id="0fbad-169">Hello StorSimple 가상 장치에서 만든 클라우드 스냅숏은 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-169">Cloud snapshots created by hello StorSimple virtual device are retained.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0fbad-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0fbad-170">Next steps</span></span>
* <span data-ttu-id="0fbad-171">toorestore 비활성화 된 장치 toofactory 기본값 hello, 너무 이동[hello 장치 toofactory 기본 설정으로 초기화](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings)합니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-171">toorestore hello deactivated device toofactory defaults, go too[Reset hello device toofactory default settings](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>
* <span data-ttu-id="0fbad-172">기술 지원을 받으려면 [Microsoft 지원에 문의](storsimple-contact-microsoft-support.md)하세요.</span><span class="sxs-lookup"><span data-stu-id="0fbad-172">For technical assistance, [contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
* <span data-ttu-id="0fbad-173">toouse hello StorSimple Manager 서비스 너무 이동 하는 방법에 대해 더 알아봅니다을 toolearn[사용 하 여 StorSimple 장치를 StorSimple Manager 서비스 tooadminister hello](storsimple-manager-service-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0fbad-173">toolearn more about how toouse hello StorSimple Manager service, go too[Use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span> 

