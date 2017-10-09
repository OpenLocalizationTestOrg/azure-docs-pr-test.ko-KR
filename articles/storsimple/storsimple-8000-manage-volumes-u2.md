---
title: "aaaManage StorSimple 볼륨 (업데이트 3) | Microsoft Docs"
description: "고 tooadd, 수정, 모니터링 및 StorSimple 볼륨을 삭제 하는 방법에 대해 설명 tootake 필요한 경우 오프 라인입니다."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 6228c4486dd5a7887df670c4c4584c4edcdfc509
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-volumes-update-3-or-later"></a><span data-ttu-id="c33a3-103">Hello StorSimple 장치 관리자 서비스 toomanage 볼륨 (업데이트 3 이상)를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="c33a3-103">Use hello StorSimple Device Manager service toomanage volumes (Update 3 or later)</span></span>

## <a name="overview"></a><span data-ttu-id="c33a3-104">개요</span><span class="sxs-lookup"><span data-stu-id="c33a3-104">Overview</span></span>

<span data-ttu-id="c33a3-105">이 자습서에서는 toouse StorSimple 장치 관리자 서비스 toocreate hello 하 및 3 이상 업데이트를 실행 하는 hello StorSimple 8000 시리즈 장치에 볼륨을 관리 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-105">This tutorial explains how toouse hello StorSimple Device Manager service toocreate and manage volumes on hello StorSimple 8000 series devices running Update 3 and later.</span></span>

<span data-ttu-id="c33a3-106">hello StorSimple 장치 관리자 서비스는 hello 단일 웹 인터페이스에서 StorSimple 솔루션을 관리할 수 있는 Azure 포털의에서 확장입니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-106">hello StorSimple Device Manager service is an extension in hello Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="c33a3-107">모든 장치에서 hello Azure 포털 toomanage 볼륨을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-107">Use hello Azure portal toomanage volumes on all your devices.</span></span> <span data-ttu-id="c33a3-108">StorSimple 서비스를 만들고 관리하고, 장치를 관리하고, 정책을 백업하고, 카탈로그를 백업하고, 경고를 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-108">You can also create and manage StorSimple services, manage devices, backup policies, and backup catalog, and view alerts.</span></span>

## <a name="volume-types"></a><span data-ttu-id="c33a3-109">볼륨 유형</span><span class="sxs-lookup"><span data-stu-id="c33a3-109">Volume types</span></span>

<span data-ttu-id="c33a3-110">StorSimple 볼륨은 다음과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-110">StorSimple volumes can be:</span></span>

* <span data-ttu-id="c33a3-111">**로컬로 고정 볼륨**: 이러한 볼륨의 데이터에 항상 hello 로컬 StorSimple 장치에 남아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-111">**Locally pinned volumes**: Data in these volumes remains on hello local StorSimple device at all times.</span></span>
* <span data-ttu-id="c33a3-112">**볼륨을 계층화 된**: 이러한 볼륨의 데이터 toohello 클라우드 spill 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-112">**Tiered volumes**: Data in these volumes can spill toohello cloud.</span></span>

<span data-ttu-id="c33a3-113">보관 볼륨은 계층화된 볼륨의 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-113">An archival volume is a type of tiered volume.</span></span> <span data-ttu-id="c33a3-114">hello 더 큰 중복 제거 청크 크기 보관 볼륨에 사용 되는 hello 장치 tootransfer toohello 클라우드 데이터의 더 큰 세그먼트 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-114">hello larger deduplication chunk size used for archival volumes allows hello device tootransfer larger segments of data toohello cloud.</span></span>

<span data-ttu-id="c33a3-115">필요한 경우 로컬 tootiered 또는 계층화 된 toolocal hello 볼륨 유형을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-115">If necessary, you can change hello volume type from local tootiered or from tiered toolocal.</span></span> <span data-ttu-id="c33a3-116">자세한 내용은 이동 너무[hello 볼륨 유형 변경](#change-the-volume-type)합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-116">For more information, go too[Change hello volume type](#change-the-volume-type).</span></span>

### <a name="locally-pinned-volumes"></a><span data-ttu-id="c33a3-117">로컬로 고정된 볼륨</span><span class="sxs-lookup"><span data-stu-id="c33a3-117">Locally pinned volumes</span></span>

<span data-ttu-id="c33a3-118">로컬로 고정 된 볼륨 데이터 toohello 클라우드 계층 하지 않는 완전 하 게 볼륨을 기본 데이터의 경우 클라우드 연결의 독립적인 보장 되므로 로컬 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-118">Locally pinned volumes are fully provisioned volumes that do not tier data toohello cloud, thereby ensuring local guarantees for primary data, independent of cloud connectivity.</span></span> <span data-ttu-id="c33a3-119">로컬로 고정된 볼륨의 데이터는 중복 제거되고 압축되지 않지만 로컬로 고정된 볼륨의 스냅숏은 중복 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-119">Data on locally pinned volumes is not deduplicated and compressed; however, snapshots of locally pinned volumes are deduplicated.</span></span> 

<span data-ttu-id="c33a3-120">로컬로 고정된 볼륨은 완전히 프로비전되므로 만들 때 장치에 충분한 공간이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-120">Locally pinned volumes are fully provisioned; therefore, you must have sufficient space on your device when you create them.</span></span> <span data-ttu-id="c33a3-121">로컬 고정된 볼륨이 tooa 8TB hello StorSimple 8100 장치 및 hello 8600 장치의 20TB의 최대 크기를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-121">You can provision locally pinned volumes up tooa maximum size of 8 TB on hello StorSimple 8100 device and 20 TB on hello 8600 device.</span></span> <span data-ttu-id="c33a3-122">StorSimple는 스냅숏, 메타 데이터 및 데이터 처리에 대 한 hello 장치에 hello 나머지 로컬 공간을 예약합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-122">StorSimple reserves hello remaining local space on hello device for snapshots, metadata, and data processing.</span></span> <span data-ttu-id="c33a3-123">Hello 크기의는 로컬 고정된 볼륨 toohello 최대 사용 가능한 공간을 늘릴 수 있습니다 하지만 한 번 만든 볼륨의 hello 크기를 줄일 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-123">You can increase hello size of a locally pinned volume toohello maximum space available, but you cannot decrease hello size of a volume once created.</span></span>

<span data-ttu-id="c33a3-124">로컬로 고정 된 볼륨을 만들 경우 계층화 된 볼륨 만들기에 대 한 사용 가능한 공간 hello 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-124">When you create a locally pinned volume, hello available space for creation of tiered volumes is reduced.</span></span> <span data-ttu-id="c33a3-125">역방향 hello도 마찬가지입니다: 고정 된 볼륨을 로컬 만들기에 사용할 수 있는 hello 공간 위에 명시 된 hello 최대 제한 보다 작아야 기존 계층화 된 볼륨이 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="c33a3-125">hello reverse is also true: if you have existing tiered volumes, hello space available for creating locally pinned volumes will be lower than hello maximum limits stated above.</span></span> <span data-ttu-id="c33a3-126">로컬 볼륨에 대 한 자세한 내용은 참조 toohello [로컬 고정된 볼륨에 자주 묻는 질문](storsimple-8000-local-volume-faq.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-126">For more information on local volumes, refer toohello [frequently asked questions on locally pinned volumes](storsimple-8000-local-volume-faq.md).</span></span>

### <a name="tiered-volumes"></a><span data-ttu-id="c33a3-127">계층화된 볼륨</span><span class="sxs-lookup"><span data-stu-id="c33a3-127">Tiered volumes</span></span>

<span data-ttu-id="c33a3-128">계층화 된 볼륨은 씬 프로 비전 된 볼륨에는 hello 자주 액세스 데이터가 로컬 hello 장치에 유지 되 고 자주 사용 되는 데이터를 적게는 자동으로 toohello 클라우드 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-128">Tiered volumes are thinly provisioned volumes in which hello frequently accessed data stays local on hello device and less frequently used data is automatically tiered toohello cloud.</span></span> <span data-ttu-id="c33a3-129">씬 프로비저닝는 사용 가능한 저장소 tooexceed 물리적 리소스를 표시 되는 가상화 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-129">Thin provisioning is a virtualization technology in which available storage appears tooexceed physical resources.</span></span> <span data-ttu-id="c33a3-130">충분 한 저장소를 미리 예약 하는 대신 StorSimple 데 충분 한 공간이 toomeet 현재 요구 씬 프로 비전 tooallocate을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-130">Instead of reserving sufficient storage in advance, StorSimple uses thin provisioning tooallocate just enough space toomeet current requirements.</span></span> <span data-ttu-id="c33a3-131">클라우드 저장소의 탄력적인 특징 hello StorSimple 거 나 낮출 수 클라우드 저장소 toomeet 변화 하는 요구 하기 때문에이 방법을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-131">hello elastic nature of cloud storage facilitates this approach because StorSimple can increase or decrease cloud storage toomeet changing demands.</span></span>

<span data-ttu-id="c33a3-132">사용 중인 경우 선택 hello 않는 아카이브 데이터를 계층화 된 볼륨 hello **이 볼륨을 사용 하 여 자주 액세스 하지 않는 아카이브 데이터에 대 한** 볼륨에 대 한 확인란 toochange hello 중복 제거 청크 크기 too512 (kb)입니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-132">If you are using hello tiered volume for archival data, select hello **Use this volume for less frequently accessed archival data** check box toochange hello deduplication chunk size for your volume too512 KB.</span></span> <span data-ttu-id="c33a3-133">이 옵션을 선택 하지 않으면 해당 계층화 된 볼륨 hello 64KB의 청크 크기를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-133">If you do not select this option, hello corresponding tiered volume will use a chunk size of 64 KB.</span></span> <span data-ttu-id="c33a3-134">더 큰 중복 제거 청크 크기가 큰 않는 아카이브 데이터 toohello 클라우드의 hello 장치 tooexpedite hello 전송을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-134">A larger deduplication chunk size allows hello device tooexpedite hello transfer of large archival data toohello cloud.</span></span>


### <a name="provisioned-capacity"></a><span data-ttu-id="c33a3-135">프로비전된 용량</span><span class="sxs-lookup"><span data-stu-id="c33a3-135">Provisioned capacity</span></span>

<span data-ttu-id="c33a3-136">Toohello 다음 각 볼륨 및 장치 유형에 대 한 프로 비전 된 최대 용량에 대 한 표를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c33a3-136">Refer toohello following table for maximum provisioned capacity for each device and volume type.</span></span> <span data-ttu-id="c33a3-137">(로컬로 고정된 볼륨은 가상 장치에서 사용할 수 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="c33a3-137">(Note that locally pinned volumes are not available on a virtual device.)</span></span>

|  | <span data-ttu-id="c33a3-138">최대 계층화된 볼륨 크기</span><span class="sxs-lookup"><span data-stu-id="c33a3-138">Maximum tiered volume size</span></span> | <span data-ttu-id="c33a3-139">최대 로컬로 고정된 볼륨 크기</span><span class="sxs-lookup"><span data-stu-id="c33a3-139">Maximum locally pinned volume size</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c33a3-140">**물리적 장치**</span><span class="sxs-lookup"><span data-stu-id="c33a3-140">**Physical devices**</span></span> | | |
| <span data-ttu-id="c33a3-141">8100</span><span class="sxs-lookup"><span data-stu-id="c33a3-141">8100</span></span> |<span data-ttu-id="c33a3-142">64TB</span><span class="sxs-lookup"><span data-stu-id="c33a3-142">64 TB</span></span> |<span data-ttu-id="c33a3-143">8TB</span><span class="sxs-lookup"><span data-stu-id="c33a3-143">8 TB</span></span> |
| <span data-ttu-id="c33a3-144">8600</span><span class="sxs-lookup"><span data-stu-id="c33a3-144">8600</span></span> |<span data-ttu-id="c33a3-145">64TB</span><span class="sxs-lookup"><span data-stu-id="c33a3-145">64 TB</span></span> |<span data-ttu-id="c33a3-146">20TB</span><span class="sxs-lookup"><span data-stu-id="c33a3-146">20 TB</span></span> |
| <span data-ttu-id="c33a3-147">**가상 장치**</span><span class="sxs-lookup"><span data-stu-id="c33a3-147">**Virtual devices**</span></span> | | |
| <span data-ttu-id="c33a3-148">8010</span><span class="sxs-lookup"><span data-stu-id="c33a3-148">8010</span></span> |<span data-ttu-id="c33a3-149">30TB</span><span class="sxs-lookup"><span data-stu-id="c33a3-149">30 TB</span></span> |<span data-ttu-id="c33a3-150">해당 없음</span><span class="sxs-lookup"><span data-stu-id="c33a3-150">N/A</span></span> |
| <span data-ttu-id="c33a3-151">8020</span><span class="sxs-lookup"><span data-stu-id="c33a3-151">8020</span></span> |<span data-ttu-id="c33a3-152">64TB</span><span class="sxs-lookup"><span data-stu-id="c33a3-152">64 TB</span></span> |<span data-ttu-id="c33a3-153">해당 없음</span><span class="sxs-lookup"><span data-stu-id="c33a3-153">N/A</span></span> |

## <a name="hello-volumes-blade"></a><span data-ttu-id="c33a3-154">hello 볼륨 블레이드</span><span class="sxs-lookup"><span data-stu-id="c33a3-154">hello volumes blade</span></span>

<span data-ttu-id="c33a3-155">hello **볼륨** 블레이드에서는 초기자 (서버)에 대 한 hello Microsoft Azure StorSimple 장치에서 프로 비전 되는 toomanage hello 저장소 볼륨 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-155">hello **Volumes** blade allows you toomanage hello storage volumes that are provisioned on hello Microsoft Azure StorSimple device for your initiators (servers).</span></span> <span data-ttu-id="c33a3-156">Hello StorSimple 장치 tooyour 연결 된 서비스에 볼륨 목록이 hello를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-156">It displays hello list of volumes on hello StorSimple devices connected tooyour service.</span></span>

 ![볼륨 페이지](./media/storsimple-8000-manage-volumes-u2/volumeslist.png)

<span data-ttu-id="c33a3-158">볼륨은 다음과 같은 특성으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-158">A volume consists of a series of attributes:</span></span>

* <span data-ttu-id="c33a3-159">**볼륨 이름** –를 설명 하는 이름을 고유 해야 하며 hello 볼륨을 식별 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-159">**Volume Name** – A descriptive name that must be unique and helps identify hello volume.</span></span> <span data-ttu-id="c33a3-160">이 이름은 특정 볼륨에 필터링하는 경우 모니터링 보고서에서도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-160">This name is also used in monitoring reports when you filter on a specific volume.</span></span> <span data-ttu-id="c33a3-161">Hello 볼륨을 만든 후에 바꿀 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-161">Once hello volume is created, it cannot be renamed.</span></span>
* <span data-ttu-id="c33a3-162">**상태** – 온라인 또는 오프라인 상태가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-162">**Status** – Can be online or offline.</span></span> <span data-ttu-id="c33a3-163">볼륨이 오프 라인 상태 이면 허용 되는 액세스 toouse hello 볼륨 표시 tooinitiators (서버) 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-163">If a volume is offline, it is not visible tooinitiators (servers) that are allowed access toouse hello volume.</span></span>
* <span data-ttu-id="c33a3-164">**용량** – hello 총 hello 초기자 (서버)가 저장 될 수 있는 데이터의 양을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-164">**Capacity** – specifies hello total amount of data that can be stored by hello initiator (server).</span></span> <span data-ttu-id="c33a3-165">로컬로 고정 된 볼륨이 완전히 프로 비전 및 hello StorSimple 장치에 상주 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-165">Locally-pinned volumes are fully provisioned and reside on hello StorSimple device.</span></span> <span data-ttu-id="c33a3-166">계층화 된 볼륨은 씬 프로비저닝 및 hello 데이터는 중복 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-166">Tiered volumes are thinly provisioned and hello data is deduplicated.</span></span> <span data-ttu-id="c33a3-167">씬 프로 비전 된 볼륨으로 장치에 미리 할당 하지 않습니다 실제 저장소 용량 내부적으로 또는 tooconfigured 볼륨 용량에 따라 hello 클라우드입니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-167">With thinly provisioned volumes, your device doesn’t pre-allocate physical storage capacity internally or on hello cloud according tooconfigured volume capacity.</span></span> <span data-ttu-id="c33a3-168">hello 볼륨 용량 할당 되 고 필요에 따라 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-168">hello volume capacity is allocated and consumed on demand.</span></span>
* <span data-ttu-id="c33a3-169">**형식** – hello 볼륨 인지를 나타내는 **계층화 됨** (기본 hello) 또는 **로컬로 고정**합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-169">**Type** – Indicates whether hello volume is **Tiered** (hello default) or **Locally pinned**.</span></span>

<span data-ttu-id="c33a3-170">이 자습서 tooperform hello 작업 다음에 hello 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="c33a3-170">Use hello instructions in this tutorial tooperform hello following tasks:</span></span>

* <span data-ttu-id="c33a3-171">볼륨 추가</span><span class="sxs-lookup"><span data-stu-id="c33a3-171">Add a volume</span></span> 
* <span data-ttu-id="c33a3-172">볼륨 수정</span><span class="sxs-lookup"><span data-stu-id="c33a3-172">Modify a volume</span></span> 
* <span data-ttu-id="c33a3-173">Hello 볼륨 유형 변경</span><span class="sxs-lookup"><span data-stu-id="c33a3-173">Change hello volume type</span></span>
* <span data-ttu-id="c33a3-174">볼륨 삭제</span><span class="sxs-lookup"><span data-stu-id="c33a3-174">Delete a volume</span></span> 
* <span data-ttu-id="c33a3-175">볼륨을 오프라인으로 전환</span><span class="sxs-lookup"><span data-stu-id="c33a3-175">Take a volume offline</span></span> 
* <span data-ttu-id="c33a3-176">볼륨 모니터링</span><span class="sxs-lookup"><span data-stu-id="c33a3-176">Monitor a volume</span></span> 

## <a name="add-a-volume"></a><span data-ttu-id="c33a3-177">볼륨 추가</span><span class="sxs-lookup"><span data-stu-id="c33a3-177">Add a volume</span></span>

<span data-ttu-id="c33a3-178">StorSimple 8000 시리즈 장치를 배포하는 동안 [볼륨을 만들었습니다](storsimple-8000-deployment-walkthrough-u2.md#step-6-create-a-volume).</span><span class="sxs-lookup"><span data-stu-id="c33a3-178">You [created a volume](storsimple-8000-deployment-walkthrough-u2.md#step-6-create-a-volume) during deployment of your StorSimple 8000 series device.</span></span> <span data-ttu-id="c33a3-179">볼륨 추가는 과정이 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-179">Adding a volume is a similar procedure.</span></span>

#### <a name="tooadd-a-volume"></a><span data-ttu-id="c33a3-180">tooadd 볼륨</span><span class="sxs-lookup"><span data-stu-id="c33a3-180">tooadd a volume</span></span>

1. <span data-ttu-id="c33a3-181">Hello에서 hello 장치 hello 테이블 형식 목록에서 **장치** 블레이드에서 장치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-181">From hello tabular listing of hello devices in hello **Devices** blade, select your device.</span></span> <span data-ttu-id="c33a3-182">**+ 볼륨 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-182">Click **+ Add volume**.</span></span>

    ![새 볼륨 추가](./media/storsimple-8000-manage-volumes-u2/step5createvol1.png)

2. <span data-ttu-id="c33a3-184">Hello에 **볼륨 추가** 블레이드:</span><span class="sxs-lookup"><span data-stu-id="c33a3-184">In hello **Add a volume** blade:</span></span>
   
    1. <span data-ttu-id="c33a3-185">hello **선택 장치** 필드는 현재 장치의 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-185">hello **Select device** field is automatically populated with your current device.</span></span>

    2. <span data-ttu-id="c33a3-186">Hello 드롭 다운 목록에서 볼륨 tooadd 해야 하는 hello 볼륨 컨테이너를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-186">From hello drop-down list, select hello volume container where you need tooadd a volume.</span></span>

    3.  <span data-ttu-id="c33a3-187">볼륨의 **이름** 을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-187">Type a **Name** for your volume.</span></span> <span data-ttu-id="c33a3-188">Hello 볼륨을 만든 후 hello 볼륨을 바꿀 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-188">Once hello volume is created, you cannot rename hello volume.</span></span>

    4. <span data-ttu-id="c33a3-189">Hello 드롭 다운 목록에서 선택 hello **형식** 볼륨에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-189">On hello drop-down list, select hello **Type** for your volume.</span></span> <span data-ttu-id="c33a3-190">로컬 보증, 낮은 대기 시간 및 높은 성능이 필요한 워크로드의 경우 **로컬로 고정** 볼륨을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-190">For workloads that require local guarantees, low latencies, and higher performance, select a **Locally pinned** volume.</span></span> <span data-ttu-id="c33a3-191">다른 모든 데이터에 대해서는 **계층화됨** 볼륨을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-191">For all other data, select a **Tiered** volume.</span></span> <span data-ttu-id="c33a3-192">아카이브 데이터에 이 볼륨을 사용하려면 **자주 액세스하지 않는 아카이브 데이터에 대해 이 볼륨 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-192">If you are using this volume for archival data, check **Use this volume for less frequently accessed archival data**.</span></span>
      
       <span data-ttu-id="c33a3-193">계층화된 볼륨은 씬 프로비전되며 빠르게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-193">A tiered volume is thinly provisioned and can be created quickly.</span></span> <span data-ttu-id="c33a3-194">선택 하면 **자주 액세스 하지 않는 아카이브 데이터에이 볼륨 사용** 볼륨에 대 한 아카이브 데이터 변경 내용 hello 중복 제거 청크 크기에 대 한 대상으로 하는 계층화 된 볼륨에 대 한 too512 (kb)입니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-194">Selecting **Use this volume for less frequently accessed archival data** for tiered volume targeted for archival data changes hello deduplication chunk size for your volume too512 KB.</span></span> <span data-ttu-id="c33a3-195">이 필드를 선택 하지 않으면 해당 계층화 된 볼륨 hello 청크 크기는 64KB를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-195">If this field is not checked, hello corresponding tiered volume uses a chunk size of 64 KB.</span></span> <span data-ttu-id="c33a3-196">더 큰 중복 제거 청크 크기가 큰 않는 아카이브 데이터 toohello 클라우드의 hello 장치 tooexpedite hello 전송을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-196">A larger deduplication chunk size allows hello device tooexpedite hello transfer of large archival data toohello cloud.</span></span>
       
       <span data-ttu-id="c33a3-197">로컬 고정된 볼륨 씩 프로 비전 하 고 hello hello 볼륨에 기본 데이터를 로컬 toohello 장치 상태를 유지 하 고 toohello 클라우드를 분산 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-197">A locally pinned volume is thickly provisioned and ensures that hello primary data on hello volume stays local toohello device and does not spill toohello cloud.</span></span>  <span data-ttu-id="c33a3-198">Hello 장치가 hello 로컬 계층에서 사용 가능한 공간을 확인 하는 로컬 고정된 볼륨을 만드는 경우의 hello tooprovision hello 볼륨 크기를 요청 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-198">If you create a locally pinned volume, hello device checks for available space on hello local tiers tooprovision hello volume of hello requested size.</span></span> <span data-ttu-id="c33a3-199">로컬 고정된 볼륨 만들기의 hello 작동 hello 장치 toohello 클라우드에서 기존 데이터를 모두 포함 될 수 있습니다 및 toocreate hello 볼륨 hello 시간이 길어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-199">hello operation of creating a locally pinned volume may involve spilling existing data from hello device toohello cloud and hello time taken toocreate hello volume may be long.</span></span> <span data-ttu-id="c33a3-200">hello 총 시간 hello 프로 비전 된 볼륨, 사용 가능한 네트워크 대역폭 및 장치의 hello 데이터의 hello 크기에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-200">hello total time depends on hello size of hello provisioned volume, available network bandwidth, and hello data on your device.</span></span>

    5. <span data-ttu-id="c33a3-201">Hello 지정 **프로 비전 된 용량** 볼륨에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-201">Specify hello **Provisioned Capacity** for your volume.</span></span> <span data-ttu-id="c33a3-202">선택 하는 hello 볼륨 종류에 따라 사용할 수 있는 hello 용량의 메모를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-202">Make a note of hello capacity that is available based on hello volume type selected.</span></span> <span data-ttu-id="c33a3-203">hello 지정 hello 사용 가능한 공간 볼륨 크기를 초과할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-203">hello specified volume size must not exceed hello available space.</span></span>
      
       <span data-ttu-id="c33a3-204">Too8.5 TB 로컬로 고정 된 볼륨 또는 hello 8100 장치에서 too200 TB 계층화 된 볼륨을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-204">You can provision locally pinned volumes up too8.5 TB or tiered volumes up too200 TB on hello 8100 device.</span></span> <span data-ttu-id="c33a3-205">Hello 큰 8600 장치의 too22.5 TB 로컬로 고정 된 볼륨 또는 too500 TB 계층화 된 볼륨을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-205">On hello larger 8600 device, you can provision locally pinned volumes up too22.5 TB or tiered volumes up too500 TB.</span></span> <span data-ttu-id="c33a3-206">Hello 장치의 로컬 공간이 필요한 toohost hello 작업 계층화 된 볼륨의 집합 이므로 로컬 고정된 볼륨 만들기 hello 공간을 계층화 된 볼륨을 프로 비전에 사용할 수 있는 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-206">As local space on hello device is required toohost hello working set of tiered volumes, creation of locally pinned volumes impacts hello space available for provisioning tiered volumes.</span></span> <span data-ttu-id="c33a3-207">따라서 로컬로 고정된 볼륨을 만드는 경우 계층화된 볼륨을 만드는 데 사용할 수 있는 공간이 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-207">Therefore, if you create a locally pinned volume, space available for creation of tiered volumes is reduced.</span></span> <span data-ttu-id="c33a3-208">마찬가지로, 계층화 된 볼륨을 만들면 로컬 고정된 볼륨 만들기에 대 한 hello 사용 가능한 공간이 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-208">Similarly, if a tiered volume is created, hello available space for creation of locally pinned volumes is reduced.</span></span>
      
       <span data-ttu-id="c33a3-209">8100 장치에서 로컬로 고정 된 양의 8.5 TB (최대 허용 크기)를 프로 비전 hello 장치에서 사용 가능한 모든 hello 로컬 공간이 소진 되었을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-209">If you provision a locally pinned volume of 8.5 TB (maximum allowable size) on your 8100 device, then you have exhausted all hello local space available on hello device.</span></span> <span data-ttu-id="c33a3-210">Hello의 hello 장치 toohost hello 작업 집합에 로컬 공간이 없을 때부터 해당 지점에서 모든 계층화 된 볼륨을 만들 수 없습니다 볼륨 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-210">You can't create any tiered volume from that point onwards as there is no local space on hello device toohost hello working set of hello tiered volume.</span></span> <span data-ttu-id="c33a3-211">기존의 계층화 된 볼륨에 사용할 수 있는 hello 공간을 영향이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-211">Existing tiered volumes also affect hello space available.</span></span> <span data-ttu-id="c33a3-212">예를 들어 대략 106TB의 계층화된 볼륨이 있는 8100 장치에서는 로컬 고정 볼륨에 대해 4TB의 공간만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-212">For example, if you have an 8100 device that already has tiered volumes of roughly 106 TB, only 4 TB of space is available for locally pinned volumes.</span></span>

    6. <span data-ttu-id="c33a3-213">Hello에 **호스트 연결** 필드 hello 화살표를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-213">In hello **Connected hosts** field, click hello arrow.</span></span> 

        ![연결된 호스트](./media/storsimple-8000-manage-volumes-u2/step5createvol2.png)

    7. <span data-ttu-id="c33a3-215">Hello에 **호스트 연결** 블레이드에서 기존 ACR을 선택 하거나 새 ACR을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-215">In hello **Connected hosts** blade, choose an existing ACR or add a new ACR.</span></span> <span data-ttu-id="c33a3-216">새 ACR을 선택 하는 경우 제공 합니다는 **이름** ACR를 hello 제공 **iSCSI Qualified Name** (IQN) Windows 호스트의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-216">If you choose a new ACR, then supply a **Name** for your ACR, provide hello **iSCSI Qualified Name** (IQN) of your Windows host.</span></span> <span data-ttu-id="c33a3-217">IQN hello를 설정 하지 않은 경우 너무 이동[Get hello Windows Server 호스트의 IQN](#get-the-iqn-of-a-windows-server-host)합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-217">If you don't have hello IQN, go too[Get hello IQN of a Windows Server host](#get-the-iqn-of-a-windows-server-host).</span></span> <span data-ttu-id="c33a3-218">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-218">Click **Create**.</span></span> <span data-ttu-id="c33a3-219">볼륨을 지정 하는 hello로 만들면 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-219">A volume is created with hello specified settings.</span></span>

        ![만들기 클릭](./media/storsimple-8000-manage-volumes-u2/step5createvol3.png)

<span data-ttu-id="c33a3-221">새 볼륨 toouse 준비 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-221">Your new volume is now ready toouse.</span></span>

> [!NOTE]
> <span data-ttu-id="c33a3-222">그런 다음 hello 볼륨 만들기 작업 실행 순서 대로 즉시 로컬 고정된 볼륨 만들기 한 다음 다른 로컬로 만드는 경우 고정 볼륨.</span><span class="sxs-lookup"><span data-stu-id="c33a3-222">If you create a locally pinned volume and then create another locally pinned volume immediately afterwards, hello volume creation jobs run sequentially.</span></span> <span data-ttu-id="c33a3-223">hello 다음 볼륨 만들기 작업을 시작 하기 전에 hello 첫 번째 볼륨 만들기 작업이 완료 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-223">hello first volume creation job must finish before hello next volume creation job can begin.</span></span>

## <a name="modify-a-volume"></a><span data-ttu-id="c33a3-224">볼륨 수정</span><span class="sxs-lookup"><span data-stu-id="c33a3-224">Modify a volume</span></span>

<span data-ttu-id="c33a3-225">Tooexpand 또는 hello 볼륨에 액세스 하는 호스트 hello 변경 해야 하는 경우 볼륨을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-225">Modify a volume when you need tooexpand it or change hello hosts that access hello volume.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="c33a3-226">Hello 장치에서 hello 볼륨 크기를 수정 하면 hello 볼륨 크기 toobe hello 호스트 에서도 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-226">If you modify hello volume size on hello device, hello volume size needs toobe changed on hello host as well.</span></span>
> * <span data-ttu-id="c33a3-227">여기에 설명 된 hello 호스트 측 단계는 Windows Server 2012 (2012R2) 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-227">hello host-side steps described here are for Windows Server 2012 (2012R2).</span></span> <span data-ttu-id="c33a3-228">Linux 또는 다른 호스트 운영 체제에 대한 절차는 이와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-228">Procedures for Linux or other host operating systems will be different.</span></span> <span data-ttu-id="c33a3-229">다른 운영 체제를 실행 하는 호스트의 hello 볼륨을 수정할 때 tooyour 호스트 운영 체제 지침을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c33a3-229">Refer tooyour host operating system instructions when modifying hello volume on a host running another operating system.</span></span>

#### <a name="toomodify-a-volume"></a><span data-ttu-id="c33a3-230">toomodify 볼륨</span><span class="sxs-lookup"><span data-stu-id="c33a3-230">toomodify a volume</span></span>

1. <span data-ttu-id="c33a3-231">StorSimple 장치 관리자 서비스 tooyour 이동한 다음 클릭 **장치**합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-231">Go tooyour StorSimple Device Manager service and then click **Devices**.</span></span> <span data-ttu-id="c33a3-232">테이블 형식 목록 hello 장치의 hello에서 toomodify 덮어쓸지를 hello 볼륨이 있는 hello 장치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-232">From hello tabular listing of hello devices, select hello device that has hello volume that you intend toomodify.</span></span> <span data-ttu-id="c33a3-233">**설정 > 볼륨**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-233">Click **Settings > Volumes**.</span></span>

    ![TooVolumes 블레이드로 이동](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

2. <span data-ttu-id="c33a3-235">Hello 나열 하는 볼륨의 테이블 형식에서 hello 볼륨을 선택 하 고 tooinvoke hello 상황에 맞는 메뉴를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-235">From hello tabular listing of volumes, select hello volume and right-click tooinvoke hello context menu.</span></span> <span data-ttu-id="c33a3-236">선택 **오프 라인 상태로 만드는** tootake hello 볼륨을 오프 라인을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-236">Select **Take offline** tootake hello volume you will modify offline.</span></span>

    ![볼륨 선택 및 오프라인으로 전환](./media/storsimple-8000-manage-volumes-u2/modifyvol4.png)

3. <span data-ttu-id="c33a3-238">Hello에 **오프 라인 상태로 만드는** 블레이드에서 hello 볼륨을 오프 라인의 hello 영향을 검토 하 고 hello 해당 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-238">In hello **Take offline** blade, review hello impact of taking hello volume offline and select hello corresponding checkbox.</span></span> <span data-ttu-id="c33a3-239">먼저 hello hello 호스트에서 해당 볼륨은 오프 라인 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-239">Ensure that hello corresponding volume on hello host is offline first.</span></span> <span data-ttu-id="c33a3-240">볼륨을 오프 라인 tootake 호스트 서버에 연결 하는 방법을 tooStorSimple 대 한 자세한 내용은 toooperating 시스템에 대 한 구체적인 지침을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c33a3-240">For information on how tootake a volume offline on your host server connected tooStorSimple, refer toooperating system specific instructions.</span></span> <span data-ttu-id="c33a3-241">**오프라인으로 전환**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-241">Click **Take offline**.</span></span>

    ![볼륨을 오프라인으로 전환하는 영향 검토](./media/storsimple-8000-manage-volumes-u2/modifyvol5.png)

4. <span data-ttu-id="c33a3-243">Hello 볼륨이 오프 라인 (같이 hello 볼륨 상태별) 일 후 hello 볼륨을 선택 하 고 tooinvoke hello 상황에 맞는 메뉴를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-243">After hello volume is offline (as shown by hello volume status), select hello volume and right-click tooinvoke hello context menu.</span></span> <span data-ttu-id="c33a3-244">**볼륨 수정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-244">Select **Modify volume**.</span></span>

    ![볼륨 수정 선택](./media/storsimple-8000-manage-volumes-u2/modifyvol9.png)


5. <span data-ttu-id="c33a3-246">Hello에 **볼륨 수정** 블레이드에서 hello 변경 내용에 따라 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-246">In hello **Modify volume** blade, you can make hello following changes:</span></span>
   
   1. <span data-ttu-id="c33a3-247">볼륨 hello **이름** 편집할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-247">hello volume **Name** cannot be edited.</span></span>
   2. <span data-ttu-id="c33a3-248">Hello 변환 **형식** 로컬로 고정 된 tootiered 또는 고정 된 계층화 된 toolocally (참조 [hello 볼륨 유형 변경](#change-the-volume-type) 에 대 한 자세한 내용은).</span><span class="sxs-lookup"><span data-stu-id="c33a3-248">Convert hello **Type** from locally pinned tootiered or from tiered toolocally pinned (see [Change hello volume type](#change-the-volume-type) for more information).</span></span>
   3. <span data-ttu-id="c33a3-249">Hello 증가 **프로 비전 된 용량**합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-249">Increase hello **Provisioned Capacity**.</span></span> <span data-ttu-id="c33a3-250">hello **프로 비전 된 용량** 늘릴 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-250">hello **Provisioned Capacity** can only be increased.</span></span> <span data-ttu-id="c33a3-251">만든 후에는 볼륨을 축소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-251">You cannot shrink a volume after it is created.</span></span>
   4. <span data-ttu-id="c33a3-252">아래 **호스트 연결**, hello ACR을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-252">Under **Connected hosts**, you can modify hello ACR.</span></span> <span data-ttu-id="c33a3-253">ACR toomodify hello 볼륨은 오프 라인 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-253">toomodify an ACR, hello volume must be offline.</span></span>

       ![볼륨을 오프라인으로 전환하는 영향 검토](./media/storsimple-8000-manage-volumes-u2/modifyvol11.png)

5. <span data-ttu-id="c33a3-255">클릭 **저장** toosave 변경 내용을 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-255">Click **Save** toosave your changes.</span></span> <span data-ttu-id="c33a3-256">확인하라는 메시지가 표시되면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-256">When prompted for confirmation, click **Yes**.</span></span> <span data-ttu-id="c33a3-257">hello Azure 포털에서 업데이트 볼륨 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-257">hello Azure portal will display an updating volume message.</span></span> <span data-ttu-id="c33a3-258">Hello 볼륨 성공적으로 업데이트 되었을 때 성공 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-258">It will display a success message when hello volume has been successfully updated.</span></span>

    ![볼륨을 오프라인으로 전환하는 영향 검토](./media/storsimple-8000-manage-volumes-u2/modifyvol5.png)

7. <span data-ttu-id="c33a3-260">볼륨을 확장 하는 경우 hello Windows 호스트 컴퓨터에서 다음 단계를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-260">If you are expanding a volume, complete hello following steps on your Windows host computer:</span></span>
   
   1. <span data-ttu-id="c33a3-261">너무 이동**컴퓨터 관리** ->**디스크 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-261">Go too**Computer Management** ->**Disk Management**.</span></span>
   2. <span data-ttu-id="c33a3-262">**디스크 관리**를 마우스 오른쪽 단추로 클릭하고 **디스크 다시 검사**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-262">Right-click **Disk Management** and select **Rescan Disks**.</span></span>
   3. <span data-ttu-id="c33a3-263">디스크의 hello 목록에서 업데이트 된 hello 볼륨, 마우스 오른쪽 단추를 선택한 후 선택 **볼륨 확장**합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-263">In hello list of disks, select hello volume that you updated, right-click, and then select **Extend Volume**.</span></span> <span data-ttu-id="c33a3-264">hello 볼륨 확장 마법사를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-264">hello Extend Volume wizard starts.</span></span> <span data-ttu-id="c33a3-265">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-265">Click **Next**.</span></span>
   4. <span data-ttu-id="c33a3-266">Hello 기본값을 적용 하는 hello 마법사를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-266">Complete hello wizard, accepting hello default values.</span></span> <span data-ttu-id="c33a3-267">Hello 마법사가 완료 되 면 hello 볼륨 hello 증가 크기를 나타내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-267">After hello wizard is finished, hello volume should show hello increased size.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="c33a3-268">로컬로 고정 된 볼륨을 확장 한 다음를 확장 하는 경우 다른 로컬로 고정 된 볼륨 hello 볼륨 확장 작업이 순차적으로 실행 하는 그 후에 즉시입니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-268">If you expand a locally pinned volume and then expand another locally pinned volume immediately afterwards, hello volume expansion jobs run sequentially.</span></span> <span data-ttu-id="c33a3-269">hello 다음 볼륨 확장 작업이 시작 하기 전에 hello 첫 번째 볼륨 확장 작업이 완료 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-269">hello first volume expansion job must finish before hello next volume expansion job can begin.</span></span>
      

## <a name="change-hello-volume-type"></a><span data-ttu-id="c33a3-270">Hello 볼륨 유형 변경</span><span class="sxs-lookup"><span data-stu-id="c33a3-270">Change hello volume type</span></span>

<span data-ttu-id="c33a3-271">로컬로 고정 된 tootiered 또는 고정 된 계층화 된 toolocally에서 hello 볼륨 유형을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-271">You can change hello volume type from tiered toolocally pinned or from locally pinned tootiered.</span></span> <span data-ttu-id="c33a3-272">그러나 이 변환은 자주 발생해서는 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-272">However, this conversion should not be a frequent occurrence.</span></span>

### <a name="tiered-toolocal-volume-conversion-considerations"></a><span data-ttu-id="c33a3-273">Toolocal 계층화 된 볼륨에 대 한 변환 고려 사항</span><span class="sxs-lookup"><span data-stu-id="c33a3-273">Tiered toolocal volume conversion considerations</span></span>

<span data-ttu-id="c33a3-274">고정 된 계층화 된 toolocally에서 볼륨을 변환 하기 위한 몇 가지 원인은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-274">Some reasons for converting a volume from tiered toolocally pinned are:</span></span>

* <span data-ttu-id="c33a3-275">데이터 가용성 및 성능에 대한 로컬 보장</span><span class="sxs-lookup"><span data-stu-id="c33a3-275">Local guarantees regarding data availability and performance</span></span>
* <span data-ttu-id="c33a3-276">클라우드 대기 시간 및 클라우드 연결 문제를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-276">Elimination of cloud latencies and cloud connectivity issues.</span></span>

<span data-ttu-id="c33a3-277">작은 이들은 일반적으로 기존 볼륨 tooaccess 자주 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-277">Typically, these are small existing volumes that you want tooaccess frequently.</span></span> <span data-ttu-id="c33a3-278">로컬로 고정된 볼륨은 생성될 때 완벽하게 프로비전됩니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-278">A locally pinned volume is fully provisioned when it is created.</span></span> 

<span data-ttu-id="c33a3-279">계층화 된 볼륨 tooa 로컬로 고정 된 볼륨을 변환 하는 경우 StorSimple hello 변환을 시작 하기 전에 장치에 공간이 충분 한지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-279">If you are converting a tiered volume tooa locally pinned volume, StorSimple verifies that you have sufficient space on your device before it starts hello conversion.</span></span> <span data-ttu-id="c33a3-280">공간이 부족 한 경우 오류가 표시 됩니다 및 hello 작업이 취소 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-280">If you have insufficient space, you will receive an error and hello operation will be canceled.</span></span> 

> [!NOTE]
> <span data-ttu-id="c33a3-281">계층화 된 toolocally 고정으로 변환을 시작 하기 전에 고려해 야 hello 다른 워크 로드의 공간 요구 사항을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-281">Before you begin a conversion from tiered toolocally pinned, make sure that you consider hello space requirements of your other workloads.</span></span> 

<span data-ttu-id="c33a3-282">로컬로 고정 된 계층화 된 tooa 볼륨으로 변환 하면 장치 성능이 저하 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-282">Conversion from a tiered tooa locally pinned volume can adversely affect device performance.</span></span> <span data-ttu-id="c33a3-283">또한 요인에 따라 hello toocomplete hello 변환 hello 시간을 늘어날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-283">Additionally, hello following factors might increase hello time it takes toocomplete hello conversion:</span></span>

* <span data-ttu-id="c33a3-284">대역폭이 충분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-284">There is insufficient bandwidth.</span></span>
* <span data-ttu-id="c33a3-285">현재 백업이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-285">There is no current backup.</span></span>

<span data-ttu-id="c33a3-286">이러한 요인이 있을 수 있는 toominimize hello 효과:</span><span class="sxs-lookup"><span data-stu-id="c33a3-286">toominimize hello effects that these factors may have:</span></span>

* <span data-ttu-id="c33a3-287">대역폭 제한 정책을 검토하고 전용 40Mbps 대역폭을 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-287">Review your bandwidth throttling policies and make sure that a dedicated 40 Mbps bandwidth is available.</span></span>
* <span data-ttu-id="c33a3-288">사용량이 적은 시간에 대 한 hello 변환을 예약 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-288">Schedule hello conversion for off-peak hours.</span></span>
* <span data-ttu-id="c33a3-289">Hello 변환을 시작 하기 전에 클라우드 스냅숏을 만드십시오.</span><span class="sxs-lookup"><span data-stu-id="c33a3-289">Take a cloud snapshot before you start hello conversion.</span></span>

<span data-ttu-id="c33a3-290">(다른 작업을 지 원하는) 여러 볼륨을 변환 하는 경우 다음 하면 우선 순위를 매기 hello 볼륨으로의 변환 더 높은 우선 순위 볼륨 먼저 변환 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-290">If you are converting multiple volumes (supporting different workloads), then you should prioritize hello volume conversion so that higher priority volumes are converted first.</span></span> <span data-ttu-id="c33a3-291">예를 들어 파일 공유 워크로드가 있는 볼륨을 변환하기 전에 VM(가상 컴퓨터)을 호스트하는 볼륨 또는 SQL 워크로드가 있는 볼륨을 변환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-291">For example, you should convert volumes that host virtual machines (VMs) or volumes with SQL workloads before you convert volumes with file share workloads.</span></span>

### <a name="local-tootiered-volume-conversion-considerations"></a><span data-ttu-id="c33a3-292">로컬 tootiered 볼륨 변환 고려 사항</span><span class="sxs-lookup"><span data-stu-id="c33a3-292">Local tootiered volume conversion considerations</span></span>

<span data-ttu-id="c33a3-293">로컬 고정된 볼륨 tooa toochange 계층화 된 볼륨 추가 공간 tooprovision 해야 할 경우 다른 볼륨을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-293">You may want toochange a locally pinned volume tooa tiered volume if you need additional space tooprovision other volumes.</span></span> <span data-ttu-id="c33a3-294">로컬로 고정 hello 볼륨 tootiered를 변환할 때는 hello hello 장치에서 사용 가능한 용량 출시 hello 용량의 hello 크기에 따라 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-294">When you convert hello locally pinned volume tootiered, hello available capacity on hello device increases by hello size of hello released capacity.</span></span> <span data-ttu-id="c33a3-295">연결에 문제가 있어 hello 변환할 볼륨의 hello 지역 형식 toohello에서 계층 유형, hello 로컬 볼륨 발생할 것 계층화 된 볼륨의 속성 hello 변환이 완료 될 때까지 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-295">If connectivity issues prevent hello conversion of a volume from hello local type toohello tiered type, hello local volume will exhibit properties of a tiered volume until hello conversion is complete.</span></span> <span data-ttu-id="c33a3-296">즉, 일부 데이터가 유출 toohello 클라우드를 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-296">This is because some data might have spilled toohello cloud.</span></span> <span data-ttu-id="c33a3-297">이 이러한 데이터 toooccupy hello 작업을 다시 시작 하 고 완료 될 때까지 해제 될 수 없습니다 hello 장치의 로컬 공간을 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-297">This spilled data continues toooccupy local space on hello device that cannot be freed until hello operation is restarted and completed.</span></span>

> [!NOTE]
> <span data-ttu-id="c33a3-298">볼륨 변환은 다소 시간이 걸릴 수 있으며 시작된 후에 변환을 취소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-298">Converting a volume can take some time and you cannot cancel a conversion after it starts.</span></span> <span data-ttu-id="c33a3-299">hello 볼륨을 hello 변환 하는 동안 온라인 상태로 유지 하 고 백업을 가져올 수 있지만 확장 하거나 hello 변환이 수행 되는 동안 hello 볼륨을 복원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-299">hello volume remains online during hello conversion, and you can take backups, but you cannot expand or restore hello volume while hello conversion is taking place.</span></span>


#### <a name="toochange-hello-volume-type"></a><span data-ttu-id="c33a3-300">toochange hello 볼륨 유형</span><span class="sxs-lookup"><span data-stu-id="c33a3-300">toochange hello volume type</span></span>

1. <span data-ttu-id="c33a3-301">StorSimple 장치 관리자 서비스 tooyour 이동한 다음 클릭 **장치**합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-301">Go tooyour StorSimple Device Manager service and then click **Devices**.</span></span> <span data-ttu-id="c33a3-302">테이블 형식 목록 hello 장치의 hello에서 toomodify 덮어쓸지를 hello 볼륨이 있는 hello 장치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-302">From hello tabular listing of hello devices, select hello device that has hello volume that you intend toomodify.</span></span> <span data-ttu-id="c33a3-303">**설정 > 볼륨**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-303">Click **Settings > Volumes**.</span></span>

    ![TooVolumes 블레이드로 이동](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

3. <span data-ttu-id="c33a3-305">Hello 나열 하는 볼륨의 테이블 형식에서 hello 볼륨을 선택 하 고 tooinvoke hello 상황에 맞는 메뉴를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-305">From hello tabular listing of volumes, select hello volume and right-click tooinvoke hello context menu.</span></span> <span data-ttu-id="c33a3-306">**수정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-306">Select **Modify**.</span></span>

    ![상황에 맞는 메뉴에서 수정 선택](./media/storsimple-8000-manage-volumes-u2/changevoltype2.png)

4. <span data-ttu-id="c33a3-308">Hello에 **볼륨 수정** 블레이드에서 hello에서 hello 새 유형을 선택 하 여 hello 볼륨 형식을 변경 **형식** 드롭 다운 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-308">On hello **Modify volume** blade, change hello volume type by selecting hello new type from hello **Type** drop-down list.</span></span>
   
   * <span data-ttu-id="c33a3-309">형식을 변경 하는 hello 너무 경우**로컬로 고정**, 충분 한 용량이 있는 경우 StorSimple toosee를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-309">If you are changing hello type too**Locally pinned**, StorSimple will check toosee if there is sufficient capacity.</span></span>
   * <span data-ttu-id="c33a3-310">형식을 변경 하는 hello 너무 경우**계층화 됨** 고이 볼륨을 사용 하 여 보관 데이터 선택 hello 됩니다 **자주 액세스 하지 않는 아카이브 데이터에이 볼륨 사용** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-310">If you are changing hello type too**Tiered** and this volume will be used for archival data, select hello **Use this volume for less frequently accessed archival data** check box.</span></span>
   * <span data-ttu-id="c33a3-311">계층화 된 대로 로컬 고정된 볼륨을 구성 하는 경우 또는 _반대로_, hello 다음과 같은 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-311">If you are configuring a locally pinned volume as tiered or _vice-versa_, hello following message appears.</span></span>
   
    ![볼륨 유형 변경 메시지](./media/storsimple-8000-manage-volumes-u2/changevoltype3.png)

7. <span data-ttu-id="c33a3-313">클릭 **저장** toosave hello 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-313">Click **Save** toosave hello changes.</span></span> <span data-ttu-id="c33a3-314">확인 메시지가 나타나면 클릭 **예** toostart hello 변환 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-314">When prompted for confirmation, click **Yes** toostart hello conversion process.</span></span> 

    ![저장 및 확인](./media/storsimple-8000-manage-volumes-u2/modifyvol11.png)

8. <span data-ttu-id="c33a3-316">Azure 포털 hello hello 볼륨을 업데이트 하는 hello 작업 만들기에 대 한 알림을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-316">hello Azure portal displays a notification for hello job creation that would update hello volume.</span></span> <span data-ttu-id="c33a3-317">Hello 볼륨 변환 작업이의 hello 알림 toomonitor hello 상태를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-317">Click on hello notification toomonitor hello status of hello volume conversion job.</span></span>

    ![볼륨 전환을 위한 작업](./media/storsimple-8000-manage-volumes-u2/changevoltype5.png)

## <a name="take-a-volume-offline"></a><span data-ttu-id="c33a3-319">볼륨을 오프라인으로 전환</span><span class="sxs-lookup"><span data-stu-id="c33a3-319">Take a volume offline</span></span>

<span data-ttu-id="c33a3-320">Toomodify 제작 하거나 hello 볼륨을 삭제 하는 경우 볼륨을 오프 tootake를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-320">You may need tootake a volume offline when you are planning toomodify or delete hello volume.</span></span> <span data-ttu-id="c33a3-321">볼륨이 오프라인 상태인 경우 읽기 전용 액세스를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-321">When a volume is offline, it is not available for read-write access.</span></span> <span data-ttu-id="c33a3-322">Hello 호스트와 hello 장치에서 hello 볼륨을 오프 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-322">You must take hello volume offline on hello host and hello device.</span></span>

#### <a name="tootake-a-volume-offline"></a><span data-ttu-id="c33a3-323">tootake 오프 라인 볼륨</span><span class="sxs-lookup"><span data-stu-id="c33a3-323">tootake a volume offline</span></span>

1. <span data-ttu-id="c33a3-324">Hello 볼륨이 오프 라인으로 전환 하기 전에 있지 않은지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-324">Make sure that hello volume in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="c33a3-325">첫 번째 hello 호스트에서 hello 볼륨을 오프 라인입니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-325">Take hello volume offline on hello host first.</span></span> <span data-ttu-id="c33a3-326">따라서 hello 볼륨에서 데이터가 손상 될 위험이 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-326">This eliminates any potential risk of data corruption on hello volume.</span></span> <span data-ttu-id="c33a3-327">특정 단계에 대 한 호스트 운영 체제에 대 한 toohello 지침을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c33a3-327">For specific steps, refer toohello instructions for your host operating system.</span></span>
3. <span data-ttu-id="c33a3-328">Hello 호스트 오프 라인 상태 이면 후 hello 다음 단계를 수행 하 여 hello 볼륨 hello 장치에 오프 라인에서 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-328">After hello host is offline, take hello volume on hello device offline by performing hello following steps:</span></span>
   
    1. <span data-ttu-id="c33a3-329">StorSimple 장치 관리자 서비스 tooyour 이동한 다음 클릭 **장치**합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-329">Go tooyour StorSimple Device Manager service and then click **Devices**.</span></span> <span data-ttu-id="c33a3-330">테이블 형식 목록 hello 장치의 hello에서 toomodify 덮어쓸지를 hello 볼륨이 있는 hello 장치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-330">From hello tabular listing of hello devices, select hello device that has hello volume that you intend toomodify.</span></span> <span data-ttu-id="c33a3-331">**설정 > 볼륨**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-331">Click **Settings > Volumes**.</span></span>

        ![TooVolumes 블레이드로 이동](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

    2. <span data-ttu-id="c33a3-333">Hello 나열 하는 볼륨의 테이블 형식에서 hello 볼륨을 선택 하 고 tooinvoke hello 상황에 맞는 메뉴를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-333">From hello tabular listing of volumes, select hello volume and right-click tooinvoke hello context menu.</span></span> <span data-ttu-id="c33a3-334">선택 **오프 라인 상태로 만드는** tootake hello 볼륨을 오프 라인을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-334">Select **Take offline** tootake hello volume you will modify offline.</span></span>

        ![볼륨 선택 및 오프라인으로 전환](./media/storsimple-8000-manage-volumes-u2/modifyvol4.png)

3. <span data-ttu-id="c33a3-336">Hello에 **오프 라인 상태로 만드는** 블레이드에서 hello 볼륨을 오프 라인의 hello 영향을 검토 하 고 hello 해당 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-336">In hello **Take offline** blade, review hello impact of taking hello volume offline and select hello corresponding checkbox.</span></span> <span data-ttu-id="c33a3-337">**오프라인으로 전환**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-337">Click **Take offline**.</span></span> 

    ![볼륨을 오프라인으로 전환하는 영향 검토](./media/storsimple-8000-manage-volumes-u2/modifyvol5.png)
      
      <span data-ttu-id="c33a3-339">Hello 볼륨이 오프 라인 상태일 때 알림이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-339">You are notified when hello volume is offline.</span></span> <span data-ttu-id="c33a3-340">또한 hello 볼륨 상태 tooOffline를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-340">hello volume status also updates tooOffline.</span></span>
      
4. <span data-ttu-id="c33a3-341">볼륨은 오프 라인 hello 볼륨 및 마우스 오른쪽 단추를 선택 하는 경우 후 **온라인 상태로 만들기** 옵션을 hello 상황에 맞는 메뉴에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-341">After a volume is offline, if you select hello volume and right-click, **Bring Online** option becomes available in hello context menu.</span></span>

> [!NOTE]
> <span data-ttu-id="c33a3-342">hello **오프 라인으로 전환** 명령은 요청 toohello 장치 tootake hello 볼륨을 오프 라인으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-342">hello **Take Offline** command sends a request toohello device tootake hello volume offline.</span></span> <span data-ttu-id="c33a3-343">호스트는 hello 볼륨을 사용 하는 경우이 인해 연결이 끊어지지만된 하지만 hello 볼륨을 오프 라인 실패 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-343">If hosts are still using hello volume, this results in broken connections, but taking hello volume offline will not fail.</span></span>

## <a name="delete-a-volume"></a><span data-ttu-id="c33a3-344">볼륨 삭제</span><span class="sxs-lookup"><span data-stu-id="c33a3-344">Delete a volume</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c33a3-345">오프라인 상태인 경우에만 볼륨을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-345">You can delete a volume only if it is offline.</span></span>

<span data-ttu-id="c33a3-346">다음 단계 toodelete 볼륨 hello를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-346">Complete hello following steps toodelete a volume.</span></span>

#### <a name="toodelete-a-volume"></a><span data-ttu-id="c33a3-347">toodelete 볼륨</span><span class="sxs-lookup"><span data-stu-id="c33a3-347">toodelete a volume</span></span>

1. <span data-ttu-id="c33a3-348">StorSimple 장치 관리자 서비스 tooyour 이동한 다음 클릭 **장치**합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-348">Go tooyour StorSimple Device Manager service and then click **Devices**.</span></span> <span data-ttu-id="c33a3-349">테이블 형식 목록 hello 장치의 hello에서 toomodify 덮어쓸지를 hello 볼륨이 있는 hello 장치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-349">From hello tabular listing of hello devices, select hello device that has hello volume that you intend toomodify.</span></span> <span data-ttu-id="c33a3-350">**설정 > 볼륨**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-350">Click **Settings > Volumes**.</span></span>

    ![TooVolumes 블레이드로 이동](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

3. <span data-ttu-id="c33a3-352">Hello 상태를 확인 하려는 toodelete hello 볼륨의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-352">Check hello status of hello volume you want toodelete.</span></span> <span data-ttu-id="c33a3-353">Toodelete hello 볼륨을 오프 라인 없으면 오프 라인 상태로 먼저 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-353">If hello volume you want toodelete is not offline, take it offline first.</span></span> <span data-ttu-id="c33a3-354">Hello 단계에 따라 [볼륨을 오프 라인](#take-a-volume-offline)합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-354">Follow hello steps in [Take a volume offline](#take-a-volume-offline).</span></span>
4. <span data-ttu-id="c33a3-355">Hello 볼륨이 오프 라인 상태 이면 후 hello 볼륨을 선택 tooinvoke hello 상황에 맞는 메뉴를 마우스 오른쪽 단추로 클릭 한 다음 선택 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-355">After hello volume is offline, select hello volume, right-click tooinvoke hello context menu and then select **Delete**.</span></span>

    ![상황에 맞는 메뉴에서 삭제 선택](./media/storsimple-8000-manage-volumes-u2/deletevol1.png)

5. <span data-ttu-id="c33a3-357">Hello에 **삭제** 블레이드, 검토 및 선택 hello 볼륨을 삭제의 hello 영향에 대 한 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-357">In hello **Delete** blade, review and select hello checkbox against hello impact of deleting a volume.</span></span> <span data-ttu-id="c33a3-358">볼륨을 삭제 하면 hello 볼륨에 있는 모든 hello 데이터가 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-358">When you delete a volume, all hello data that resides on hello volume is lost.</span></span> 

    ![변경 내용 저장 및 확인](./media/storsimple-8000-manage-volumes-u2/deletevol2.png)

6. <span data-ttu-id="c33a3-360">Hello 볼륨을 삭제 한 후 볼륨의 테이블 형식 목록을 hello tooindicate hello 삭제를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-360">After hello volume is deleted, hello tabular list of volumes updates tooindicate hello deletion.</span></span>

    ![업데이트된 볼륨 목록](./media/storsimple-8000-manage-volumes-u2/deletevol3.png)
   
   > [!NOTE]
   > <span data-ttu-id="c33a3-362">로컬로 고정 된 볼륨을 삭제 하면 hello 공간 새 볼륨에 사용할 수 있는 즉시 업데이트 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-362">If you delete a locally pinned volume, hello space available for new volumes may not be updated immediately.</span></span> <span data-ttu-id="c33a3-363">StorSimple 장치 관리자 서비스 hello 사용 가능한 로컬 공간 hello를 주기적으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-363">hello StorSimple Device Manager Service updates hello local space available periodically.</span></span> <span data-ttu-id="c33a3-364">Toocreate hello 새 볼륨을 시도 하기 전에 몇 분 정도 대기 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-364">We suggest you wait for a few minutes before you try toocreate hello new volume.</span></span>
   >
   > <span data-ttu-id="c33a3-365">또한 로컬로 고정 된 볼륨을 삭제 한 다음 다른 로컬로 삭제 하는 경우 고정 된 볼륨 hello 볼륨 삭제 작업 순차적으로 실행 하는 그 후에 즉시입니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-365">Additionally, if you delete a locally pinned volume and then delete another locally pinned volume immediately afterwards, hello volume deletion jobs run sequentially.</span></span> <span data-ttu-id="c33a3-366">볼륨 삭제 작업을 첫 번째 hello hello 다음 볼륨 삭제 작업을 시작 하기 전에 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-366">hello first volume deletion job must finish before hello next volume deletion job can begin.</span></span>

## <a name="monitor-a-volume"></a><span data-ttu-id="c33a3-367">볼륨 모니터링</span><span class="sxs-lookup"><span data-stu-id="c33a3-367">Monitor a volume</span></span>

<span data-ttu-id="c33a3-368">볼륨 모니터링 toocollect 볼륨에 대 한 통계를 O 관련 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-368">Volume monitoring allows you toocollect I/O-related statistics for a volume.</span></span> <span data-ttu-id="c33a3-369">기본적으로 hello에 대해 모니터링이 활성화를 만들면 처음 32 개 볼륨입니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-369">Monitoring is enabled by default for hello first 32 volumes that you create.</span></span> <span data-ttu-id="c33a3-370">추가 볼륨의 모니터링은 기본적으로 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-370">Monitoring of additional volumes is disabled by default.</span></span> 

> [!NOTE]
> <span data-ttu-id="c33a3-371">복제된 볼륨의 모니터링은 기본적으로 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-371">Monitoring of cloned volumes is disabled by default.</span></span>


<span data-ttu-id="c33a3-372">다음 단계 tooenable hello 하거나 볼륨에 대 한 모니터링을 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-372">Perform hello following steps tooenable or disable monitoring for a volume.</span></span>

#### <a name="tooenable-or-disable-volume-monitoring"></a><span data-ttu-id="c33a3-373">볼륨 모니터링을 비활성화 또는 tooenable</span><span class="sxs-lookup"><span data-stu-id="c33a3-373">tooenable or disable volume monitoring</span></span>

1. <span data-ttu-id="c33a3-374">StorSimple 장치 관리자 서비스 tooyour 이동한 다음 클릭 **장치**합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-374">Go tooyour StorSimple Device Manager service and then click **Devices**.</span></span> <span data-ttu-id="c33a3-375">테이블 형식 목록 hello 장치의 hello에서 toomodify 덮어쓸지를 hello 볼륨이 있는 hello 장치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-375">From hello tabular listing of hello devices, select hello device that has hello volume that you intend toomodify.</span></span> <span data-ttu-id="c33a3-376">**설정 > 볼륨**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-376">Click **Settings > Volumes**.</span></span>
2. <span data-ttu-id="c33a3-377">Hello 나열 하는 볼륨의 테이블 형식에서 hello 볼륨을 선택 하 고 tooinvoke hello 상황에 맞는 메뉴를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-377">From hello tabular listing of volumes, select hello volume and right-click tooinvoke hello context menu.</span></span> <span data-ttu-id="c33a3-378">**수정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-378">Select **Modify**.</span></span>
3. <span data-ttu-id="c33a3-379">Hello에 **볼륨 수정** 블레이드에서 대 한 **모니터링** 선택 **사용** 또는 **사용 하지 않도록 설정** tooenable 하거나 모니터링을 사용 하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-379">In hello **Modify volume** blade, for **Monitoring** select **Enable** or **Disable** tooenable or disable monitoring.</span></span>

    ![모니터링 사용 안 함](./media/storsimple-8000-manage-volumes-u2/monitorvol1.png) 

4. <span data-ttu-id="c33a3-381">**저장**을 클릭하고 확인하라는 메시지가 표시되면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-381">Click **Save** and when prompted for confirmation, click **Yes**.</span></span> <span data-ttu-id="c33a3-382">Azure 포털 hello hello 볼륨 및 성공 메시지 hello 볼륨 업데이트 된 후 업데이트에 대 한 알림을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-382">hello Azure portal displays a notification for updating hello volume and then a success message, after hello volume is successfully updated.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c33a3-383">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c33a3-383">Next steps</span></span>

* <span data-ttu-id="c33a3-384">너무 방법에 대해 알아봅니다[StorSimple 볼륨을 복제](storsimple-8000-clone-volume-u2.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-384">Learn how too[clone a StorSimple volume](storsimple-8000-clone-volume-u2.md).</span></span>
* <span data-ttu-id="c33a3-385">너무 방법에 대해 알아봅니다[사용 하 여 StorSimple 장치를 StorSimple 장치 관리자 서비스 tooadminister hello](storsimple-8000-manager-service-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c33a3-385">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

