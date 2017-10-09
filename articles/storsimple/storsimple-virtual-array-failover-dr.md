---
title: "aaaStorSimple 가상 배열 재해 복구 및 장치 장애 조치 | Microsoft Docs"
description: "에 대 한 자세한 방법에 대 한 toofailover StorSimple 가상 배열입니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 3c1f9c62-af57-4634-a0d8-435522d969aa
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5f125efd1ffb94489cdfa7cfaafae7d57cc10131
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-and-device-failover-for-your-storsimple-virtual-array-via-azure-portal"></a><span data-ttu-id="a9a17-103">Azure Portal을 통해 StorSimple 가상 배열에 대한 재해 복구 및 장치 장애 조치</span><span class="sxs-lookup"><span data-stu-id="a9a17-103">Disaster recovery and device failover for your StorSimple Virtual Array via Azure portal</span></span>

## <a name="overview"></a><span data-ttu-id="a9a17-104">개요</span><span class="sxs-lookup"><span data-stu-id="a9a17-104">Overview</span></span>
<span data-ttu-id="a9a17-105">이 문서에서는 Microsoft Azure StorSimple 가상 배열 hello를 포함 하 여 자세한 단계를 통해 tooanother 가상 배열 toofail hello 재해 복구를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-105">This article describes hello disaster recovery for your Microsoft Azure StorSimple Virtual Array including hello detailed steps toofail over tooanother virtual array.</span></span> <span data-ttu-id="a9a17-106">장애 조치 하면 toomove에서 데이터는 *소스* hello 데이터 센터 tooa에서 장치 *대상* 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-106">A failover allows you toomove your data from a *source* device in hello datacenter tooa *target* device.</span></span> <span data-ttu-id="a9a17-107">hello 대상 장치에 못할 동일 하거나 서로 다른 지리적 위치 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-107">hello target device may be located in hello same or a different geographical location.</span></span> <span data-ttu-id="a9a17-108">장치 장애 조치 hello hello 전체 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-108">hello device failover is for hello entire device.</span></span> <span data-ttu-id="a9a17-109">장애 조치 중 hello 소스 장치에 대 한 클라우드 데이터 hello hello 대상 장치의 소유권 toothat을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-109">During failover, hello cloud data for hello source device changes ownership toothat of hello target device.</span></span>

<span data-ttu-id="a9a17-110">이 문서는 해당 tooStorSimple 가상 배열만 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-110">This article is applicable tooStorSimple Virtual Arrays only.</span></span> <span data-ttu-id="a9a17-111">8000 시리즈 장치를 통해 toofail 너무 이동[StorSimple 장치의 장치 장애 조치 및 재해 복구](storsimple-device-failover-disaster-recovery.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-111">toofail over an 8000 series device, go too[Device failover and disaster recovery of your StorSimple device](storsimple-device-failover-disaster-recovery.md).</span></span>

## <a name="what-is-disaster-recovery-and-device-failover"></a><span data-ttu-id="a9a17-112">재해 복구 및 장치 장애 조치(Failover)란 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="a9a17-112">What is disaster recovery and device failover?</span></span>

<span data-ttu-id="a9a17-113">장애 복구 (DR) 시나리오에서 기본 장치 hello 작동이 중지 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-113">In a disaster recovery (DR) scenario, hello primary device stops functioning.</span></span> <span data-ttu-id="a9a17-114">이 시나리오에서는 실패 한 장치 tooanother 장치 hello와 관련 된 hello 클라우드 데이터를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-114">In this scenario, you can move hello cloud data associated with hello failed device tooanother device.</span></span> <span data-ttu-id="a9a17-115">Hello 기본 장치를 사용 하 여 hello로 *소스* hello로 다른 장치를 지정 하 고 *대상*합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-115">You can use hello primary device as hello *source* and specify another device as hello *target*.</span></span> <span data-ttu-id="a9a17-116">이 프로세스는 참조 된 tooas hello *장애 조치*합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-116">This process is referred tooas hello *failover*.</span></span> <span data-ttu-id="a9a17-117">장애 조치 중 모든 hello 볼륨 또는 hello 공유 hello 원본 장치의 소유권이 변경 되며 대상 장치에 전송 된 toohello 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-117">During failover, all hello volumes or hello shares from hello source device change ownership and are transferred toohello target device.</span></span> <span data-ttu-id="a9a17-118">Hello 데이터의 필터링을 하지 않고 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-118">No filtering of hello data is allowed.</span></span>

<span data-ttu-id="a9a17-119">DR은 hello 열 지도 기반 계층 구성 및 추적을 사용 하 여 전체 장치 복원으로 모델링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-119">DR is modeled as a full device restore using hello heat map–based tiering and tracking.</span></span> <span data-ttu-id="a9a17-120">열 지도 기반으로 데이터를 읽고 쓰기 패턴이 열 값 toohello 할당 하 여 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-120">A heat map is defined by assigning a heat value toohello data based on read and write patterns.</span></span> <span data-ttu-id="a9a17-121">이 열에는 계층 hello 가장 낮은 열 데이터 청크 toohello 클라우드 먼저 hello 로컬 계층의 hello (가장 사용 되는) 높은 열 데이터 청크를 유지 하면서 다음 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-121">This heat map then tiers hello lowest heat data chunks toohello cloud first while keeping hello high heat (most used) data chunks in hello local tier.</span></span> <span data-ttu-id="a9a17-122">DR StorSimple 열 지도 toorestore hello를 사용 하 여 처리 도중과 hello 클라우드에서 hello 데이터 리하이드레이션 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-122">During a DR, StorSimple uses hello heat map toorestore and rehydrate hello data from hello cloud.</span></span> <span data-ttu-id="a9a17-123">hello 장치 (내부적으로 결정)에 따라 모든 hello 볼륨/공유 hello 마지막 최근 백업에 인출 하 고 해당 백업에서 복원을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-123">hello device fetches all hello volumes/shares in hello last recent backup (as determined internally) and performs a restore from that backup.</span></span> <span data-ttu-id="a9a17-124">hello 가상 배열 hello 전체 DR 프로세스를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-124">hello virtual array orchestrates hello entire DR process.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a9a17-125">따라서 장애 복구는 지원 되지 않습니다 및 장치 장애 조치의 hello 끝에 hello 원본 장치가 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-125">hello source device is deleted at hello end of device failover and hence a failback is not supported.</span></span>
> 
> 

<span data-ttu-id="a9a17-126">재해 복구 hello 장치 장애 조치 기능을 통해 오케스트레이션 및 hello에서 시작 됩니다 **장치** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-126">Disaster recovery is orchestrated via hello device failover feature and is initiated from hello **Devices** blade.</span></span> <span data-ttu-id="a9a17-127">이 블레이드 표로 모든 hello StorSimple 장치 연결 된 tooyour StorSimple 장치 관리자 서비스를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-127">This blade tabulates all hello StorSimple devices connected tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="a9a17-128">각 장치에 대 한 hello 이름, 상태, 프로 비전 된 / 최대 용량, 형식 및 모델을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-128">For each device, you can see hello friendly name, status, provisioned and maximum capacity, type, and model.</span></span>

## <a name="prerequisites-for-device-failover"></a><span data-ttu-id="a9a17-129">장치 장애 조치에 대한 필수 조건</span><span class="sxs-lookup"><span data-stu-id="a9a17-129">Prerequisites for device failover</span></span>

### <a name="prerequisites"></a><span data-ttu-id="a9a17-130">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a9a17-130">Prerequisites</span></span>

<span data-ttu-id="a9a17-131">장치 장애 조치에 대 한 필수 구성 요소를 다음 해당 hello 충족 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-131">For a device failover, ensure that hello following prerequisites are satisfied:</span></span>

* <span data-ttu-id="a9a17-132">hello 소스 장치에서 toobe 필요는 **Deactivated** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-132">hello source device needs toobe in a **Deactivated** state.</span></span>
* <span data-ttu-id="a9a17-133">hello 대상 장치에 필요한 tooshow를으로 **를 tooset 준비** hello Azure 포털의에서.</span><span class="sxs-lookup"><span data-stu-id="a9a17-133">hello target device needs tooshow up as **Ready tooset up** in hello Azure portal.</span></span> <span data-ttu-id="a9a17-134">대상 가상 배열의 hello 프로 비전 동일 하거나 더 높은 용량입니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-134">Provision a target virtual array of hello same or higher capacity.</span></span> <span data-ttu-id="a9a17-135">로컬 웹 UI tooconfigure hello를 사용 하 고 성공적으로 hello 대상 가상 배열을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-135">Use hello local web UI tooconfigure and successfully register hello target virtual array.</span></span>
  
  > [!IMPORTANT]
  > <span data-ttu-id="a9a17-136">Tooconfigure hello 등록 된 가상 장치를 hello 서비스를 통해 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="a9a17-136">Do not attempt tooconfigure hello registered virtual device through hello service.</span></span> <span data-ttu-id="a9a17-137">장치 구성이 hello 서비스를 통해 수행 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-137">No device configuration should be performed through hello service.</span></span>
  > 
  > 
* <span data-ttu-id="a9a17-138">hello 대상 장치 hello hello 소스 장치로 이름과 같은 이름을 가질 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-138">hello target device cannot have hello same name as hello source device.</span></span>
* <span data-ttu-id="a9a17-139">hello 소스 및 대상 장치에 없으면 toobe hello 같은 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-139">hello source and target device have toobe hello same type.</span></span> <span data-ttu-id="a9a17-140">파일 서버 tooanother 파일 서버로 구성 하는 가상 배열만 조치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-140">You can only fail over a virtual array configured as a file server tooanother file server.</span></span> <span data-ttu-id="a9a17-141">hello에 마찬가지입니다 iSCSI 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-141">hello same is true for an iSCSI server.</span></span>
* <span data-ttu-id="a9a17-142">DR에는 파일 서버에 대 한 hello 대상 장치 toohello 참가 하는 권장 hello 소스와 같은 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-142">For a file server DR, we recommend that you join hello target device toohello same domain as hello source.</span></span> <span data-ttu-id="a9a17-143">이 구성을 통해 hello 공유 사용 권한을 자동으로 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-143">This configuration ensures that hello share permissions are automatically resolved.</span></span> <span data-ttu-id="a9a17-144">Hello 장애 조치 tooa 대상 장치에만 hello에 동일한 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-144">Only hello failover tooa target device in hello same domain.</span></span>
* <span data-ttu-id="a9a17-145">DR에 대 한 hello 사용 가능한 대상 장치는 장치에 있는 동일 hello 또는 용량이 더 큰 toohello 소스 장치 비교입니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-145">hello available target devices for DR are devices that have hello same or larger capacity compared toohello source device.</span></span> <span data-ttu-id="a9a17-146">hello 연결된 tooyour는 장치에 서비스에서 하지만 hello에 맞지 않는 장치를 대상으로 사용할 수 없는 충분 한 공간 조건을 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-146">hello devices that are connected tooyour service but do not meet hello criteria of sufficient space are not available as target devices.</span></span>

### <a name="other-considerations"></a><span data-ttu-id="a9a17-147">기타 고려 사항</span><span class="sxs-lookup"><span data-stu-id="a9a17-147">Other considerations</span></span>

* <span data-ttu-id="a9a17-148">계획된 장애 조치(Failover)의 경우</span><span class="sxs-lookup"><span data-stu-id="a9a17-148">For a planned failover</span></span> 
  
  * <span data-ttu-id="a9a17-149">모든 hello 볼륨 또는 공유가 오프 라인으로 hello 소스 장치에서 수행 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-149">We recommend that you take all hello volumes or shares on hello source device offline.</span></span>
  * <span data-ttu-id="a9a17-150">Hello 장치의 백업을 만들 다음 hello 장애 조치 toominimize 데이터 손실을 진행 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-150">We recommend that you take a backup of hello device and then proceed with hello failover toominimize data loss.</span></span> 
* <span data-ttu-id="a9a17-151">계획 되지 않은 장애 조치의 경우 hello 장치 hello 가장 최근의 백업 toorestore hello 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-151">For an unplanned failover, hello device uses hello most recent backup toorestore hello data.</span></span>

### <a name="device-failover-prechecks"></a><span data-ttu-id="a9a17-152">장치 장애 조치 사전 검사</span><span class="sxs-lookup"><span data-stu-id="a9a17-152">Device failover prechecks</span></span>

<span data-ttu-id="a9a17-153">DR을 시작 하는 hello, 하기 전에 hello 장치 prechecks를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-153">Before hello DR begins, hello device performs prechecks.</span></span> <span data-ttu-id="a9a17-154">이러한 검사는 DR이 시작된 후 오류가 발생하지 않도록 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-154">These checks help ensure that no errors occur when DR commences.</span></span> <span data-ttu-id="a9a17-155">hello prechecks 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-155">hello prechecks include:</span></span>

* <span data-ttu-id="a9a17-156">Hello 저장소 계정의 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-156">Validating hello storage account.</span></span>
* <span data-ttu-id="a9a17-157">Hello 클라우드 연결 tooAzure 확인 중입니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-157">Checking hello cloud connectivity tooAzure.</span></span>
* <span data-ttu-id="a9a17-158">Hello 대상 장치에서 사용 가능한 공간을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-158">Checking available space on hello target device.</span></span>
* <span data-ttu-id="a9a17-159">iSCSI 서버 원본 장치 볼륨에 다음 항목이 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="a9a17-159">Checking if an iSCSI server source device volume has</span></span>
  
  * <span data-ttu-id="a9a17-160">유효한 ACR 이름</span><span class="sxs-lookup"><span data-stu-id="a9a17-160">valid ACR names.</span></span>
  * <span data-ttu-id="a9a17-161">유효한 IQN(220자를 초과하지 않음)</span><span class="sxs-lookup"><span data-stu-id="a9a17-161">valid IQN (not exceeding 220 characters).</span></span>
  * <span data-ttu-id="a9a17-162">유효한 CHAP 암호(12-16자 길이)</span><span class="sxs-lookup"><span data-stu-id="a9a17-162">valid CHAP passwords (12-16 characters long).</span></span>

<span data-ttu-id="a9a17-163">Hello prechecks 앞에 실패할 경우 hello DR 계속할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-163">If any of hello preceding prechecks fail, you cannot proceed with hello DR.</span></span> <span data-ttu-id="a9a17-164">해당 문제를 해결한 후 DR을 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-164">Resolve those issues and then retry DR.</span></span>

<span data-ttu-id="a9a17-165">DR hello 성공적으로 완료 되 면 hello 소스 장치에서 클라우드 데이터 hello hello 소유권은 전송 된 toohello 대상 장치.</span><span class="sxs-lookup"><span data-stu-id="a9a17-165">After hello DR is successfully completed, hello ownership of hello cloud data on hello source device is transferred toohello target device.</span></span> <span data-ttu-id="a9a17-166">hello 소스 장치를 다음 hello 포털에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-166">hello source device is then no longer available in hello portal.</span></span> <span data-ttu-id="a9a17-167">액세스 tooall hello 볼륨/공유 hello 소스 장치에서 차단 하 고 hello 대상 장치 활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-167">Access tooall hello volumes/shares on hello source device is blocked and hello target device becomes active.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a9a17-168">Hello 장치를 더 이상 사용할 수 있지만 hello 호스트 시스템에서 프로 비전 하는 hello 가상 컴퓨터는 여전히 리소스를 소비 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-168">Though hello device is no longer available, hello virtual machine that you provisioned on hello host system is still consuming resources.</span></span> <span data-ttu-id="a9a17-169">DR hello 성공적으로 완료 되 면 호스트 시스템에서이 가상 컴퓨터를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-169">Once hello DR is successfully complete, you can delete this virtual machine from your host system.</span></span>
> 
> 

## <a name="fail-over-tooa-virtual-array"></a><span data-ttu-id="a9a17-170">장애 조치 tooa 가상 배열</span><span class="sxs-lookup"><span data-stu-id="a9a17-170">Fail over tooa virtual array</span></span>

<span data-ttu-id="a9a17-171">이 절차를 실행하기 전에 StorSimple 장치 관리자 서비스에 다른 StorSimple 가상 배열을 프로비전, 구성 및 등록하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-171">We recommend that you provision, configure, and register another StorSimple Virtual Array with your StorSimple Device Manager service before you run this procedure.</span></span>

> [!IMPORTANT]
> 
> * <span data-ttu-id="a9a17-172">StorSimple 8000 시리즈 장치 tooa 1200 가상 장치에서 조치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-172">You cannot fail over from a StorSimple 8000 series device tooa 1200 virtual device.</span></span>
> * <span data-ttu-id="a9a17-173">Federal FIPS Information Processing Standard () 사용 하도록 설정 가상 장치 tooanother FIPS 사용 장치 또는 hello 정부 포털에 배포 된 tooa 비 FIPS 장치에서 조치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-173">You can fail over from a Federal Information Processing Standard (FIPS) enabled virtual device tooanother FIPS enabled device or tooa non-FIPS device deployed in hello Government portal.</span></span>


<span data-ttu-id="a9a17-174">Hello 단계 toorestore hello 장치 tooa 대상 StorSimple 가상 장치를 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-174">Perform hello following steps toorestore hello device tooa target StorSimple virtual device.</span></span>

1. <span data-ttu-id="a9a17-175">프로 비전 및 구성 hello를 충족 하는 대상 장치 [장치 장애 조치에 대 한 필수 구성 요소](#prerequisites)합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-175">Provision and configure a target device that meets hello [prerequisites for device failover](#prerequisites).</span></span> <span data-ttu-id="a9a17-176">Hello 로컬 웹 UI 통해 hello 장치 구성을 완료 하 고 tooyour StorSimple 장치 관리자 서비스를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-176">Complete hello device configuration via hello local web UI and register it tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="a9a17-177">파일 서버를 만드는 경우 이동의 1 toostep [파일 서버로 설정](storsimple-virtual-array-deploy3-fs-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device)합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-177">If creating a file server, go toostep 1 of [set up as file server](storsimple-virtual-array-deploy3-fs-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device).</span></span> <span data-ttu-id="a9a17-178">ISCSI 서버를 만드는 경우 이동의 1 toostep [iSCSI 서버로 설정](storsimple-virtual-array-deploy3-iscsi-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device)합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-178">If creating an iSCSI server, go toostep 1 of [set up as iSCSI server](storsimple-virtual-array-deploy3-iscsi-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device).</span></span>

2. <span data-ttu-id="a9a17-179">Hello 호스트에서 오프 라인 볼륨/공유를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-179">Take volumes/shares offline on hello host.</span></span> <span data-ttu-id="a9a17-180">tootake hello 볼륨/공유 오프 라인으로 hello 호스트에 대 한 toohello 운영 체제 관련 지침을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="a9a17-180">tootake hello volumes/shares offline, refer toohello operating system–specific instructions for hello host.</span></span> <span data-ttu-id="a9a17-181">이미 오프 하지 해야 tootake 모든 hello 볼륨/공유 오프 라인으로 hello 장치에서 hello 다음을 수행 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-181">If not already offline, you need tootake all hello volumes/shares offline on hello device by doing hello following.</span></span>
   
    1. <span data-ttu-id="a9a17-182">너무 이동**장치** 블레이드 하 고 장치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-182">Go too**Devices** blade and select your device.</span></span>
   
    2. <span data-ttu-id="a9a17-183">너무 이동**설정 > 관리 > 공유** (또는 **설정 > 관리 > 볼륨**).</span><span class="sxs-lookup"><span data-stu-id="a9a17-183">Go too**Settings > Manage > Shares** (or **Settings > Manage > Volumes**).</span></span> 
   
    3. <span data-ttu-id="a9a17-184">공유/볼륨을 선택하고 **오프라인으로 전환**을 마우스 오른쪽 단추로 클릭하고 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-184">Select a share/volume, right click and select **Take offline**.</span></span> 
   
    4. <span data-ttu-id="a9a17-185">확인 메시지가 표시 되 면 확인 **오프 라인으로이 공유의 hello 영향을 이해 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a9a17-185">When prompted for confirmation, check **I understand hello impact of taking this share offline.**</span></span> 
   
    5. <span data-ttu-id="a9a17-186">**오프라인으로 전환**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-186">Click **Take offline**.</span></span>

3. <span data-ttu-id="a9a17-187">StorSimple 장치 관리자 서비스에 이동 너무**관리 > 장치**합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-187">In your StorSimple Device Manager service, go too**Management > Devices**.</span></span> <span data-ttu-id="a9a17-188">Hello에 **장치** 블레이드를 선택 하 고 원본 장치를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-188">In hello **Devices** blade, select and click your source device.</span></span>

4. <span data-ttu-id="a9a17-189">**장치 대시보드** 블레이드에서 **비활성화**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-189">In your **Device dashboard** blade, click **Deactivate**.</span></span>

5. <span data-ttu-id="a9a17-190">Hello에 **비활성화** 블레이드를 확인 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-190">In hello **Deactivate** blade, you are prompted for confirmation.</span></span> <span data-ttu-id="a9a17-191">장치 비활성화는 *영구적인* 프로세스이며 취소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-191">Device deactivation is a *permanent* process that cannot be undone.</span></span> <span data-ttu-id="a9a17-192">사용자는 또한 알림을 tootake 공유/볼륨 오프 라인으로 hello 호스트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-192">You are also reminded tootake your shares/volumes offline on hello host.</span></span> <span data-ttu-id="a9a17-193">장치 이름 tooconfirm hello를 입력 하 고 클릭 **비활성화**합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-193">Type hello device name tooconfirm and click **Deactivate**.</span></span>
   
    ![](./media/storsimple-virtual-array-failover-dr/failover1.png)
6. <span data-ttu-id="a9a17-194">hello 비활성화가 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-194">hello deactivation starts.</span></span> <span data-ttu-id="a9a17-195">Hello 비활성화 성공적으로 완료 된 후에 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-195">You will receive a notification after hello deactivation is successfully completed.</span></span>
   
    ![](./media/storsimple-virtual-array-failover-dr/failover2.png)
7. <span data-ttu-id="a9a17-196">Hello 장치 페이지 hello 장치 상태는 이제 바뀝니다 너무**Deactivated**합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-196">On hello Devices page, hello device state will now change too**Deactivated**.</span></span>
    ![](./media/storsimple-virtual-array-failover-dr/failover3.png)
8. <span data-ttu-id="a9a17-197">Hello에 **장치** 장애 조치에 대 한 hello 비활성화 된 소스 장치 블레이드 선택 하 고을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-197">In hello **Devices** blade, select and click hello deactivated source device for failover.</span></span> 
9. <span data-ttu-id="a9a17-198">Hello에 **장치 대시보드** 블레이드에서 클릭 **장애 조치**합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-198">In hello **Device dashboard** blade, click **Fail over**.</span></span> 
10. <span data-ttu-id="a9a17-199">Hello에 **장치 장애 조치할** 블레이드에서 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-199">In hello **Fail over device** blade, do hello following:</span></span>
    
    1. <span data-ttu-id="a9a17-200">hello 소스 장치 필드가 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-200">hello source device field is automatically populated.</span></span> <span data-ttu-id="a9a17-201">Note hello 소스 장치에 대 한 hello 총 데이터 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-201">Note hello total data size for hello source device.</span></span> <span data-ttu-id="a9a17-202">hello 데이터 크기는 hello hello 대상 장치에서 사용 가능한 용량 보다 더 작은 값 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-202">hello data size should be lesser than hello available capacity on hello target device.</span></span> <span data-ttu-id="a9a17-203">장치 이름, 전체 용량 및 장애 조치 됩니다 hello 공유 hello 이름과 같은 hello 원본 장치와 관련 된 hello 세부 정보를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-203">Review hello details associated with hello source device such as device name, total capacity, and hello names of hello shares that are failed over.</span></span>

    2. <span data-ttu-id="a9a17-204">사용 가능한 장치 hello 드롭다운 목록에서 선택 된 **대상 장치**합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-204">From hello dropdown list of available devices, choose a **Target device**.</span></span> <span data-ttu-id="a9a17-205">충분 한 용량이 있는 장치만 hello hello 드롭다운 목록에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-205">Only hello devices that have sufficient capacity are displayed in hello dropdown list.</span></span>

    3. <span data-ttu-id="a9a17-206">확인 **데이터 toohello 대상 장치를 통해이 작업을 수행할 이해**합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-206">Check that **I understand that this operation will fail over data toohello target device**.</span></span> 

    4. <span data-ttu-id="a9a17-207">**장애 조치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-207">Click **Fail over**.</span></span>
    
        ![](./media/storsimple-virtual-array-failover-dr/failover4.png)
11. <span data-ttu-id="a9a17-208">장애 조치 작업을 시작하면 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-208">A failover job initiates and you receive a notification.</span></span> <span data-ttu-id="a9a17-209">너무 이동**장치 > 작업** toomonitor hello 장애 조치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-209">Go too**Devices > Jobs** toomonitor hello failover.</span></span>
    
     ![](./media/storsimple-virtual-array-failover-dr/failover5.png)
12. <span data-ttu-id="a9a17-210">Hello에 **작업** 블레이드에 hello 소스 장치에 대해 만든 장애 조치 작업을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-210">In hello **Jobs** blade, you see a failover job created for hello source device.</span></span> <span data-ttu-id="a9a17-211">이 작업은 DR prechecks hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-211">This job performs hello DR prechecks.</span></span>
    
    ![](./media/storsimple-virtual-array-failover-dr/failover6.png)
    
     <span data-ttu-id="a9a17-212">DR hello prechecks 성공 후 hello 장애 조치 작업에는 소스 장치에 있는 각 공유/볼륨에 대 한 복원 작업이 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-212">After hello DR prechecks are successful, hello failover job will spawn restore jobs for each share/volume that exists on your source device.</span></span>
    
    ![](./media/storsimple-virtual-array-failover-dr/failover7.png)
13. <span data-ttu-id="a9a17-213">Hello 장애 조치가 완전 하 고 이동 toohello 후 **장치** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-213">After hello failover is complete, go toohello **Devices** blade.</span></span>
    
    1. <span data-ttu-id="a9a17-214">선택한 hello 장애 조치 프로세스에 대 한 hello 대상 장치로 사용 했던 hello StorSimple 장치를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-214">Select and click hello StorSimple device that was used as hello target device for hello failover process.</span></span>
    2. <span data-ttu-id="a9a17-215">너무 이동**설정 > 관리 > 공유** (또는 **볼륨** 경우 iSCSI 서버).</span><span class="sxs-lookup"><span data-stu-id="a9a17-215">Go too**Settings > Management > Shares** (or **Volumes** if iSCSI server).</span></span> <span data-ttu-id="a9a17-216">Hello에 **공유** 블레이드에서 hello 오래 된 장치에서 모든 hello 공유 (볼륨)를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-216">In hello **Shares** blade, you can view all hello shares (volumes) from hello old device.</span></span>
        ![](./media/storsimple-virtual-array-failover-dr/failover9.png)
14. <span data-ttu-id="a9a17-217">너무 필요 합니다[DNS 별칭 만들기](https://support.microsoft.com/kb/168322) 를 시도 하 고 있는 응용 프로그램을 hello 모든 tooconnect 리디렉션된 toohello 새 장치를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-217">You will need too[create a DNS alias](https://support.microsoft.com/kb/168322) so that all hello applications that are trying tooconnect can get redirected toohello new device.</span></span>

## <a name="errors-during-dr"></a><span data-ttu-id="a9a17-218">DR 중 오류</span><span class="sxs-lookup"><span data-stu-id="a9a17-218">Errors during DR</span></span>

<span data-ttu-id="a9a17-219">**DR 중 클라우드 연결 중단**</span><span class="sxs-lookup"><span data-stu-id="a9a17-219">**Cloud connectivity outage during DR**</span></span>

<span data-ttu-id="a9a17-220">후 hello 클라우드 연결에 문제가 있을 경우 DR을 시작 하 고 hello 장치 복원이 완료 되 면 전에 hello DR 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-220">If hello cloud connectivity is disrupted after DR has started and before hello device restore is complete, hello DR will fail.</span></span> <span data-ttu-id="a9a17-221">장애 조치 알림을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-221">You receive a failore notification.</span></span> <span data-ttu-id="a9a17-222">DR에 대 한 대상 장치 hello로 표시 되어 *사용할 수 없게 됩니다.*</span><span class="sxs-lookup"><span data-stu-id="a9a17-222">hello target device for DR is marked as *unusable.*</span></span> <span data-ttu-id="a9a17-223">Hello를 사용할 수 없는 이후 DRs에 대 한 동일한 대상 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-223">You cannot use hello same target device for future DRs.</span></span>

<span data-ttu-id="a9a17-224">**호환되는 대상 장치 없음**</span><span class="sxs-lookup"><span data-stu-id="a9a17-224">**No compatible target devices**</span></span>

<span data-ttu-id="a9a17-225">Hello 사용 가능한 대상 장치에 충분 한 공간이 없는 경우 호환 되는 대상 장치가 없는 오류 toohello 효과 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-225">If hello available target devices do not have sufficient space, you see an error toohello effect that there are no compatible target devices.</span></span>

<span data-ttu-id="a9a17-226">**사전 검사 실패**</span><span class="sxs-lookup"><span data-stu-id="a9a17-226">**Precheck failures**</span></span>

<span data-ttu-id="a9a17-227">Hello prechecks 중 하나가 충족 되지 않은 경우 precheck 실패가 표시 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-227">If one of hello prechecks is not satisfied, then you see precheck failures.</span></span>

## <a name="business-continuity-disaster-recovery-bcdr"></a><span data-ttu-id="a9a17-228">비즈니스 연속성 재해 복구(BCDR)</span><span class="sxs-lookup"><span data-stu-id="a9a17-228">Business continuity disaster recovery (BCDR)</span></span>

<span data-ttu-id="a9a17-229">비즈니스 연속성 장애 복구 (BCDR) 시나리오에는 hello 전체 Azure 데이터 센터가 작동 중지 될 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-229">A business continuity disaster recovery (BCDR) scenario occurs when hello entire Azure datacenter stops functioning.</span></span> <span data-ttu-id="a9a17-230">StorSimple 장치 관리자 서비스에 영향을 줄 수 있습니다 및 hello StorSimple 장치에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-230">This can affect your StorSimple Device Manager service and hello associated StorSimple devices.</span></span>

<span data-ttu-id="a9a17-231">재해가 발생 하기 직전에 등록 된 StorSimple 장치가 없을 경우 이러한 StorSimple 장치 toobe 삭제 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-231">If there are StorSimple devices that were registered just before a disaster occurred, then these StorSimple devices may need toobe deleted.</span></span> <span data-ttu-id="a9a17-232">Hello 재해 발생 후 다시 만들고 해당 장치를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-232">After hello disaster, you can recreate and configure those devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9a17-233">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a9a17-233">Next steps</span></span>

<span data-ttu-id="a9a17-234">너무 방법에 대 한 자세한[hello 로컬 웹 UI를 사용 하 여 StorSimple 가상 배열 관리](storsimple-ova-web-ui-admin.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a9a17-234">Learn more about how too[administer your StorSimple Virtual Array using hello local web UI](storsimple-ova-web-ui-admin.md).</span></span>

