---
title: "StorSimple 볼륨 관리(업데이트 3) | Microsoft Docs"
description: "StorSimple 볼륨을 추가, 수정, 모니터링 및 삭제하는 방법 및 필요에 따라 이를 오프라인으로 전환하는 방법을 설명합니다."
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
ms.openlocfilehash: 09f4de79ab9b0cdfafd10c7c7c29b0f8e6304f14
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="use-the-storsimple-device-manager-service-to-manage-volumes-update-3-or-later"></a><span data-ttu-id="a32bf-103">StorSimple 장치 관리자 서비스를 사용하여 볼륨 관리(업데이트 3 이후)</span><span class="sxs-lookup"><span data-stu-id="a32bf-103">Use the StorSimple Device Manager service to manage volumes (Update 3 or later)</span></span>

## <a name="overview"></a><span data-ttu-id="a32bf-104">개요</span><span class="sxs-lookup"><span data-stu-id="a32bf-104">Overview</span></span>

<span data-ttu-id="a32bf-105">이 자습서는 StorSimple 장치 관리자 서비스를 사용하여 업데이트 3 이후를 실행하는 StorSimple 8000 시리즈 장치에서 볼륨을 만들고 관리하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-105">This tutorial explains how to use the StorSimple Device Manager service to create and manage volumes on the StorSimple 8000 series devices running Update 3 and later.</span></span>

<span data-ttu-id="a32bf-106">StorSimple 장치 관리자 서비스는 단일 웹 인터페이스에서 StorSimple 솔루션을 관리하는 Azure Portal의 확장입니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-106">The StorSimple Device Manager service is an extension in the Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="a32bf-107">Azure Portal을 사용하여 모든 장치에서 볼륨을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-107">Use the Azure portal to manage volumes on all your devices.</span></span> <span data-ttu-id="a32bf-108">StorSimple 서비스를 만들고 관리하고, 장치를 관리하고, 정책을 백업하고, 카탈로그를 백업하고, 경고를 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-108">You can also create and manage StorSimple services, manage devices, backup policies, and backup catalog, and view alerts.</span></span>

## <a name="volume-types"></a><span data-ttu-id="a32bf-109">볼륨 유형</span><span class="sxs-lookup"><span data-stu-id="a32bf-109">Volume types</span></span>

<span data-ttu-id="a32bf-110">StorSimple 볼륨은 다음과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-110">StorSimple volumes can be:</span></span>

* <span data-ttu-id="a32bf-111">**로컬로 고정된 볼륨**: 이러한 볼륨의 데이터를 로컬 StorSimple 장치에 항상 그대로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-111">**Locally pinned volumes**: Data in these volumes remains on the local StorSimple device at all times.</span></span>
* <span data-ttu-id="a32bf-112">**계층화된 볼륨**: 이러한 볼륨의 데이터를 클라우드로 분산할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-112">**Tiered volumes**: Data in these volumes can spill to the cloud.</span></span>

<span data-ttu-id="a32bf-113">보관 볼륨은 계층화된 볼륨의 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-113">An archival volume is a type of tiered volume.</span></span> <span data-ttu-id="a32bf-114">보관 볼륨에 사용된 더 큰 중복 제거 청크 크기를 통해 장치에서 데이터의 더 큰 세그먼트를 클라우드로 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-114">The larger deduplication chunk size used for archival volumes allows the device to transfer larger segments of data to the cloud.</span></span>

<span data-ttu-id="a32bf-115">필요에 따라 로컬에서 계층화 또는 계층화에서 로컬로 볼륨 유형을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-115">If necessary, you can change the volume type from local to tiered or from tiered to local.</span></span> <span data-ttu-id="a32bf-116">자세한 내용은 [볼륨 유형 변경](#change-the-volume-type)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-116">For more information, go to [Change the volume type](#change-the-volume-type).</span></span>

### <a name="locally-pinned-volumes"></a><span data-ttu-id="a32bf-117">로컬로 고정된 볼륨</span><span class="sxs-lookup"><span data-stu-id="a32bf-117">Locally pinned volumes</span></span>

<span data-ttu-id="a32bf-118">로컬로 고정된 볼륨은 데이터를 클라우드로 계층화하지 않는 완벽하게 프로비전된 볼륨이므로 독립적인 클라우드 연결의 기본 데이터에 대한 로컬 보장을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-118">Locally pinned volumes are fully provisioned volumes that do not tier data to the cloud, thereby ensuring local guarantees for primary data, independent of cloud connectivity.</span></span> <span data-ttu-id="a32bf-119">로컬로 고정된 볼륨의 데이터는 중복 제거되고 압축되지 않지만 로컬로 고정된 볼륨의 스냅숏은 중복 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-119">Data on locally pinned volumes is not deduplicated and compressed; however, snapshots of locally pinned volumes are deduplicated.</span></span> 

<span data-ttu-id="a32bf-120">로컬로 고정된 볼륨은 완전히 프로비전되므로 만들 때 장치에 충분한 공간이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-120">Locally pinned volumes are fully provisioned; therefore, you must have sufficient space on your device when you create them.</span></span> <span data-ttu-id="a32bf-121">StorSimple 8100 장치에서는 최대 8TB의 크기를, 8600 장치에서는 20TB까지 로컬 고정 볼륨을 프로비저닝할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-121">You can provision locally pinned volumes up to a maximum size of 8 TB on the StorSimple 8100 device and 20 TB on the 8600 device.</span></span> <span data-ttu-id="a32bf-122">StorSimple은 스냅숏, 메타데이터 및 데이터 처리에 대해 장치에서 나머지 로컬 공간을 예약합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-122">StorSimple reserves the remaining local space on the device for snapshots, metadata, and data processing.</span></span> <span data-ttu-id="a32bf-123">로컬로 고정된 볼륨의 크기를 사용 가능한 최대 공간으로 늘릴 수 있지만 만든 볼륨의 크기를 줄일 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-123">You can increase the size of a locally pinned volume to the maximum space available, but you cannot decrease the size of a volume once created.</span></span>

<span data-ttu-id="a32bf-124">로컬로 고정된 볼륨을 만드는 경우 계층화된 볼륨을 만드는 데 사용할 수 있는 공간이 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-124">When you create a locally pinned volume, the available space for creation of tiered volumes is reduced.</span></span> <span data-ttu-id="a32bf-125">반대로도 마찬가지입니다. 기존 계층화된 볼륨이 있는 경우 로컬로 고정된 볼륨을 만드는 데 사용할 수 있는 공간은 위에서 언급한 최대 한도보다 작게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-125">The reverse is also true: if you have existing tiered volumes, the space available for creating locally pinned volumes will be lower than the maximum limits stated above.</span></span> <span data-ttu-id="a32bf-126">로컬 볼륨에 대한 자세한 내용은 [로컬로 고정된 볼륨에 대한 질문과 대답](storsimple-8000-local-volume-faq.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a32bf-126">For more information on local volumes, refer to the [frequently asked questions on locally pinned volumes](storsimple-8000-local-volume-faq.md).</span></span>

### <a name="tiered-volumes"></a><span data-ttu-id="a32bf-127">계층화된 볼륨</span><span class="sxs-lookup"><span data-stu-id="a32bf-127">Tiered volumes</span></span>

<span data-ttu-id="a32bf-128">계층화된 볼륨은 장치에서 로컬로 유지되는 빈번히 액세스되는 데이터에서 씬 프로비저닝된 볼륨이며 덜 자주 사용되는 데이터는 클라우드로 자동으로 계층화됩니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-128">Tiered volumes are thinly provisioned volumes in which the frequently accessed data stays local on the device and less frequently used data is automatically tiered to the cloud.</span></span> <span data-ttu-id="a32bf-129">씬 프로비저닝은 사용 가능한 저장소가 실제 리소스를 초과하는 것처럼 표시하는 가상화 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-129">Thin provisioning is a virtualization technology in which available storage appears to exceed physical resources.</span></span> <span data-ttu-id="a32bf-130">충분한 저장소를 사전에 예약하는 대신 StorSimple는 씬 프로비저닝을 사용하여 현재 요구 사항에 맞게 충분한 공간을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-130">Instead of reserving sufficient storage in advance, StorSimple uses thin provisioning to allocate just enough space to meet current requirements.</span></span> <span data-ttu-id="a32bf-131">클라우드 저장소의 탄력적인 특징은 StorSimple가 변화 하는 요구에 맞게 클라우드 저장소를 늘리거나 줄일 수 있으므로 이 방법을 용이하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-131">The elastic nature of cloud storage facilitates this approach because StorSimple can increase or decrease cloud storage to meet changing demands.</span></span>

<span data-ttu-id="a32bf-132">보관 데이터에 계층화된 볼륨을 사용하는 경우 **자주 액세스하지 않는 아카이브 데이터에 이 볼륨 사용** 확인란을 선택하여 볼륨의 중복 제거 청크 크기를 512KB로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-132">If you are using the tiered volume for archival data, select the **Use this volume for less frequently accessed archival data** check box to change the deduplication chunk size for your volume to 512 KB.</span></span> <span data-ttu-id="a32bf-133">이 옵션을 선택하지 않으면 해당 계층화된 볼륨에서 64KB의 청크 크기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-133">If you do not select this option, the corresponding tiered volume will use a chunk size of 64 KB.</span></span> <span data-ttu-id="a32bf-134">중복 제거 청크 크기를 늘리면 장치에서 대용량 아카이브 데이터를 클라우드로 신속하게 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-134">A larger deduplication chunk size allows the device to expedite the transfer of large archival data to the cloud.</span></span>


### <a name="provisioned-capacity"></a><span data-ttu-id="a32bf-135">프로비전된 용량</span><span class="sxs-lookup"><span data-stu-id="a32bf-135">Provisioned capacity</span></span>

<span data-ttu-id="a32bf-136">각 장치 및 볼륨 유형에 대한 최대 프로비전된 용량에 대해 다음 표를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a32bf-136">Refer to the following table for maximum provisioned capacity for each device and volume type.</span></span> <span data-ttu-id="a32bf-137">(로컬로 고정된 볼륨은 가상 장치에서 사용할 수 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="a32bf-137">(Note that locally pinned volumes are not available on a virtual device.)</span></span>

|  | <span data-ttu-id="a32bf-138">최대 계층화된 볼륨 크기</span><span class="sxs-lookup"><span data-stu-id="a32bf-138">Maximum tiered volume size</span></span> | <span data-ttu-id="a32bf-139">최대 로컬로 고정된 볼륨 크기</span><span class="sxs-lookup"><span data-stu-id="a32bf-139">Maximum locally pinned volume size</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a32bf-140">**물리적 장치**</span><span class="sxs-lookup"><span data-stu-id="a32bf-140">**Physical devices**</span></span> | | |
| <span data-ttu-id="a32bf-141">8100</span><span class="sxs-lookup"><span data-stu-id="a32bf-141">8100</span></span> |<span data-ttu-id="a32bf-142">64TB</span><span class="sxs-lookup"><span data-stu-id="a32bf-142">64 TB</span></span> |<span data-ttu-id="a32bf-143">8TB</span><span class="sxs-lookup"><span data-stu-id="a32bf-143">8 TB</span></span> |
| <span data-ttu-id="a32bf-144">8600</span><span class="sxs-lookup"><span data-stu-id="a32bf-144">8600</span></span> |<span data-ttu-id="a32bf-145">64TB</span><span class="sxs-lookup"><span data-stu-id="a32bf-145">64 TB</span></span> |<span data-ttu-id="a32bf-146">20TB</span><span class="sxs-lookup"><span data-stu-id="a32bf-146">20 TB</span></span> |
| <span data-ttu-id="a32bf-147">**가상 장치**</span><span class="sxs-lookup"><span data-stu-id="a32bf-147">**Virtual devices**</span></span> | | |
| <span data-ttu-id="a32bf-148">8010</span><span class="sxs-lookup"><span data-stu-id="a32bf-148">8010</span></span> |<span data-ttu-id="a32bf-149">30TB</span><span class="sxs-lookup"><span data-stu-id="a32bf-149">30 TB</span></span> |<span data-ttu-id="a32bf-150">해당 없음</span><span class="sxs-lookup"><span data-stu-id="a32bf-150">N/A</span></span> |
| <span data-ttu-id="a32bf-151">8020</span><span class="sxs-lookup"><span data-stu-id="a32bf-151">8020</span></span> |<span data-ttu-id="a32bf-152">64TB</span><span class="sxs-lookup"><span data-stu-id="a32bf-152">64 TB</span></span> |<span data-ttu-id="a32bf-153">해당 없음</span><span class="sxs-lookup"><span data-stu-id="a32bf-153">N/A</span></span> |

## <a name="the-volumes-blade"></a><span data-ttu-id="a32bf-154">볼륨 블레이드</span><span class="sxs-lookup"><span data-stu-id="a32bf-154">The volumes blade</span></span>

<span data-ttu-id="a32bf-155">**볼륨** 블레이드를 사용하면 초기자(서버)에 대해 Microsoft Azure StorSimple 장치에서 프로비전되는 저장소 볼륨을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-155">The **Volumes** blade allows you to manage the storage volumes that are provisioned on the Microsoft Azure StorSimple device for your initiators (servers).</span></span> <span data-ttu-id="a32bf-156">서비스에 연결된 StorSimple 장치에서 볼륨의 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-156">It displays the list of volumes on the StorSimple devices connected to your service.</span></span>

 ![볼륨 페이지](./media/storsimple-8000-manage-volumes-u2/volumeslist.png)

<span data-ttu-id="a32bf-158">볼륨은 다음과 같은 특성으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-158">A volume consists of a series of attributes:</span></span>

* <span data-ttu-id="a32bf-159">**볼륨 이름** – 설명이 포함된 이름은 고유해야 하며 볼륨을 식별하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-159">**Volume Name** – A descriptive name that must be unique and helps identify the volume.</span></span> <span data-ttu-id="a32bf-160">이 이름은 특정 볼륨에 필터링하는 경우 모니터링 보고서에서도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-160">This name is also used in monitoring reports when you filter on a specific volume.</span></span> <span data-ttu-id="a32bf-161">볼륨을 만들면 이름을 바꿀 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-161">Once the volume is created, it cannot be renamed.</span></span>
* <span data-ttu-id="a32bf-162">**상태** – 온라인 또는 오프라인 상태가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-162">**Status** – Can be online or offline.</span></span> <span data-ttu-id="a32bf-163">오프라인인 경우 볼륨은 해당 볼륨을 사용하는 데 액세스가 허용된 초기자(서버)에 보이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-163">If a volume is offline, it is not visible to initiators (servers) that are allowed access to use the volume.</span></span>
* <span data-ttu-id="a32bf-164">**용량** - 용량은 초기자(서버)가 저장할 수 있는 데이터의 전체 크기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-164">**Capacity** – specifies the total amount of data that can be stored by the initiator (server).</span></span> <span data-ttu-id="a32bf-165">로컬로 고정된 볼륨은 완전히 프로비전되고 StorSimple 장치에 상주합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-165">Locally-pinned volumes are fully provisioned and reside on the StorSimple device.</span></span> <span data-ttu-id="a32bf-166">계층화된 볼륨은 씬 프로비전되며 데이터는 중복 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-166">Tiered volumes are thinly provisioned and the data is deduplicated.</span></span> <span data-ttu-id="a32bf-167">씬 프로비전된 볼륨으로 장치가 구성된 볼륨 용량에 따라 클라우드에서 또는 내부적으로 실제 저장소 용량을 미리 할당하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-167">With thinly provisioned volumes, your device doesn’t pre-allocate physical storage capacity internally or on the cloud according to configured volume capacity.</span></span> <span data-ttu-id="a32bf-168">볼륨 용량이 할당되고 필요에 따라 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-168">The volume capacity is allocated and consumed on demand.</span></span>
* <span data-ttu-id="a32bf-169">**유형** – 볼륨이 **계층화됨**(기본값) 또는 **로컬로 고정**인지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-169">**Type** – Indicates whether the volume is **Tiered** (the default) or **Locally pinned**.</span></span>

<span data-ttu-id="a32bf-170">이 자습서의 지침을 사용하여 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-170">Use the instructions in this tutorial to perform the following tasks:</span></span>

* <span data-ttu-id="a32bf-171">볼륨 추가</span><span class="sxs-lookup"><span data-stu-id="a32bf-171">Add a volume</span></span> 
* <span data-ttu-id="a32bf-172">볼륨 수정</span><span class="sxs-lookup"><span data-stu-id="a32bf-172">Modify a volume</span></span> 
* <span data-ttu-id="a32bf-173">볼륨 유형 변경</span><span class="sxs-lookup"><span data-stu-id="a32bf-173">Change the volume type</span></span>
* <span data-ttu-id="a32bf-174">볼륨 삭제</span><span class="sxs-lookup"><span data-stu-id="a32bf-174">Delete a volume</span></span> 
* <span data-ttu-id="a32bf-175">볼륨을 오프라인으로 전환</span><span class="sxs-lookup"><span data-stu-id="a32bf-175">Take a volume offline</span></span> 
* <span data-ttu-id="a32bf-176">볼륨 모니터링</span><span class="sxs-lookup"><span data-stu-id="a32bf-176">Monitor a volume</span></span> 

## <a name="add-a-volume"></a><span data-ttu-id="a32bf-177">볼륨 추가</span><span class="sxs-lookup"><span data-stu-id="a32bf-177">Add a volume</span></span>

<span data-ttu-id="a32bf-178">StorSimple 8000 시리즈 장치를 배포하는 동안 [볼륨을 만들었습니다](storsimple-8000-deployment-walkthrough-u2.md#step-6-create-a-volume).</span><span class="sxs-lookup"><span data-stu-id="a32bf-178">You [created a volume](storsimple-8000-deployment-walkthrough-u2.md#step-6-create-a-volume) during deployment of your StorSimple 8000 series device.</span></span> <span data-ttu-id="a32bf-179">볼륨 추가는 과정이 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-179">Adding a volume is a similar procedure.</span></span>

#### <a name="to-add-a-volume"></a><span data-ttu-id="a32bf-180">볼륨을 추가하려면</span><span class="sxs-lookup"><span data-stu-id="a32bf-180">To add a volume</span></span>

1. <span data-ttu-id="a32bf-181">**장치** 블레이드의 테이블 형식 장치 목록에서 장치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-181">From the tabular listing of the devices in the **Devices** blade, select your device.</span></span> <span data-ttu-id="a32bf-182">**+ 볼륨 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-182">Click **+ Add volume**.</span></span>

    ![새 볼륨 추가](./media/storsimple-8000-manage-volumes-u2/step5createvol1.png)

2. <span data-ttu-id="a32bf-184">**볼륨 추가** 블레이드에서:</span><span class="sxs-lookup"><span data-stu-id="a32bf-184">In the **Add a volume** blade:</span></span>
   
    1. <span data-ttu-id="a32bf-185">**장치 선택** 필드가 현재 장치로 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-185">The **Select device** field is automatically populated with your current device.</span></span>

    2. <span data-ttu-id="a32bf-186">드롭다운 목록에서 볼륨을 추가해야 하는 볼륨 컨테이너를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-186">From the drop-down list, select the volume container where you need to add a volume.</span></span>

    3.  <span data-ttu-id="a32bf-187">볼륨의 **이름** 을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-187">Type a **Name** for your volume.</span></span> <span data-ttu-id="a32bf-188">볼륨을 만들면 이름을 바꿀 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-188">Once the volume is created, you cannot rename the volume.</span></span>

    4. <span data-ttu-id="a32bf-189">드롭다운 목록에서 볼륨의 **유형**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-189">On the drop-down list, select the **Type** for your volume.</span></span> <span data-ttu-id="a32bf-190">로컬 보증, 낮은 대기 시간 및 높은 성능이 필요한 워크로드의 경우 **로컬로 고정** 볼륨을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-190">For workloads that require local guarantees, low latencies, and higher performance, select a **Locally pinned** volume.</span></span> <span data-ttu-id="a32bf-191">다른 모든 데이터에 대해서는 **계층화됨** 볼륨을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-191">For all other data, select a **Tiered** volume.</span></span> <span data-ttu-id="a32bf-192">아카이브 데이터에 이 볼륨을 사용하려면 **자주 액세스하지 않는 아카이브 데이터에 대해 이 볼륨 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-192">If you are using this volume for archival data, check **Use this volume for less frequently accessed archival data**.</span></span>
      
       <span data-ttu-id="a32bf-193">계층화된 볼륨은 씬 프로비전되며 빠르게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-193">A tiered volume is thinly provisioned and can be created quickly.</span></span> <span data-ttu-id="a32bf-194">아카이브 데이터를 대상으로 하는 계층화된 볼륨에 **자주 액세스하지 않는 아카이브 데이터에 이 볼륨 사용** 을 선택하면 볼륨의 중복 제거 청크 크기가 512KB로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-194">Selecting **Use this volume for less frequently accessed archival data** for tiered volume targeted for archival data changes the deduplication chunk size for your volume to 512 KB.</span></span> <span data-ttu-id="a32bf-195">이 필드를 선택하지 않으면 해당 계층화된 볼륨에서 64KB의 청크 크기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-195">If this field is not checked, the corresponding tiered volume uses a chunk size of 64 KB.</span></span> <span data-ttu-id="a32bf-196">중복 제거 청크 크기를 늘리면 장치에서 대용량 아카이브 데이터를 클라우드로 신속하게 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-196">A larger deduplication chunk size allows the device to expedite the transfer of large archival data to the cloud.</span></span>
       
       <span data-ttu-id="a32bf-197">로컬로 고정된 볼륨은 씩 프로비전되며, 볼륨의 기본 데이터가 장치에 로컬로 유지되고 클라우드로 유출되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-197">A locally pinned volume is thickly provisioned and ensures that the primary data on the volume stays local to the device and does not spill to the cloud.</span></span>  <span data-ttu-id="a32bf-198">로컬로 고정된 볼륨을 만드는 경우 장치에서는 요청된 크기의 볼륨을 프로비전하기 위해 로컬 계층에서 사용 가능한 공간을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-198">If you create a locally pinned volume, the device checks for available space on the local tiers to provision the volume of the requested size.</span></span> <span data-ttu-id="a32bf-199">로컬로 고정된 볼륨을 만드는 작업에는 장치에서 클라우드로 기존 데이터를 분산하는 과정이 포함될 수 있으므로 볼륨을 만드는 데 시간이 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-199">The operation of creating a locally pinned volume may involve spilling existing data from the device to the cloud and the time taken to create the volume may be long.</span></span> <span data-ttu-id="a32bf-200">전체 시간은 프로비전되는 볼륨의 크기, 사용 가능한 네트워크 대역폭 및 장치의 데이터에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-200">The total time depends on the size of the provisioned volume, available network bandwidth, and the data on your device.</span></span>

    5. <span data-ttu-id="a32bf-201">볼륨의 **프로비전된 용량** 을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-201">Specify the **Provisioned Capacity** for your volume.</span></span> <span data-ttu-id="a32bf-202">선택한 볼륨 유형에 따라 사용할 수 있는 용량을 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-202">Make a note of the capacity that is available based on the volume type selected.</span></span> <span data-ttu-id="a32bf-203">지정된 볼륨 크기는 사용 가능한 공간을 초과하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-203">The specified volume size must not exceed the available space.</span></span>
      
       <span data-ttu-id="a32bf-204">8100 장치에서 로컬로 고정된 볼륨은 최대 8.5TB, 계층화된 볼륨은 최대 200TB까지 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-204">You can provision locally pinned volumes up to 8.5 TB or tiered volumes up to 200 TB on the 8100 device.</span></span> <span data-ttu-id="a32bf-205">더 큰 8600 장치에서 로컬로 고정된 볼륨은 최대 22.5TB, 계층화된 볼륨은 최대 500TB까지 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-205">On the larger 8600 device, you can provision locally pinned volumes up to 22.5 TB or tiered volumes up to 500 TB.</span></span> <span data-ttu-id="a32bf-206">장치의 로컬 공간은 계층화된 볼륨의 작업 집합을 호스트하는 데 필요하므로 로컬로 고정된 볼륨을 만들면 계층화된 볼륨을 프로비전하는 데 사용할 수 있는 공간이 영향을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-206">As local space on the device is required to host the working set of tiered volumes, creation of locally pinned volumes impacts the space available for provisioning tiered volumes.</span></span> <span data-ttu-id="a32bf-207">따라서 로컬로 고정된 볼륨을 만드는 경우 계층화된 볼륨을 만드는 데 사용할 수 있는 공간이 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-207">Therefore, if you create a locally pinned volume, space available for creation of tiered volumes is reduced.</span></span> <span data-ttu-id="a32bf-208">마찬가지로 계층화된 볼륨을 만드는 경우 로컬로 고정된 볼륨을 만드는 데 사용할 수 있는 공간이 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-208">Similarly, if a tiered volume is created, the available space for creation of locally pinned volumes is reduced.</span></span>
      
       <span data-ttu-id="a32bf-209">8100 장치에 8.5TB(최대 허용 크기)의 로컬 고정 볼륨을 프로비전하면 해당 장치에서 사용 가능한 로컬 공간이 모두 소진됩니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-209">If you provision a locally pinned volume of 8.5 TB (maximum allowable size) on your 8100 device, then you have exhausted all the local space available on the device.</span></span> <span data-ttu-id="a32bf-210">따라서 계층화된 볼륨의 작업 집합을 호스트할 로컬 공간이 장치에 없기 때문에 더 이상 계층화된 볼륨을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-210">You can't create any tiered volume from that point onwards as there is no local space on the device to host the working set of the tiered volume.</span></span> <span data-ttu-id="a32bf-211">기존 계층화된 볼륨도 사용 가능한 공간에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-211">Existing tiered volumes also affect the space available.</span></span> <span data-ttu-id="a32bf-212">예를 들어 대략 106TB의 계층화된 볼륨이 있는 8100 장치에서는 로컬 고정 볼륨에 대해 4TB의 공간만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-212">For example, if you have an 8100 device that already has tiered volumes of roughly 106 TB, only 4 TB of space is available for locally pinned volumes.</span></span>

    6. <span data-ttu-id="a32bf-213">**연결된 호스트** 필드에서 화살표를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-213">In the **Connected hosts** field, click the arrow.</span></span> 

        ![연결된 호스트](./media/storsimple-8000-manage-volumes-u2/step5createvol2.png)

    7. <span data-ttu-id="a32bf-215">**연결된 호스트** 블레이드에서 기존 ACR을 선택하거나 새 ACR을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-215">In the **Connected hosts** blade, choose an existing ACR or add a new ACR.</span></span> <span data-ttu-id="a32bf-216">새 ACR을 선택하는 경우 ACR의 **이름**을 입력하고 Windows 호스트의 IQN(**iSCSI Qualified Name**)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-216">If you choose a new ACR, then supply a **Name** for your ACR, provide the **iSCSI Qualified Name** (IQN) of your Windows host.</span></span> <span data-ttu-id="a32bf-217">IQN이 없는 경우 [Windows Server 호스트의 IQN 가져오기](#get-the-iqn-of-a-windows-server-host)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-217">If you don't have the IQN, go to [Get the IQN of a Windows Server host](#get-the-iqn-of-a-windows-server-host).</span></span> <span data-ttu-id="a32bf-218">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-218">Click **Create**.</span></span> <span data-ttu-id="a32bf-219">지정한 설정으로 볼륨이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-219">A volume is created with the specified settings.</span></span>

        ![만들기 클릭](./media/storsimple-8000-manage-volumes-u2/step5createvol3.png)

<span data-ttu-id="a32bf-221">이제 새 볼륨을 사용할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-221">Your new volume is now ready to use.</span></span>

> [!NOTE]
> <span data-ttu-id="a32bf-222">로컬로 고정된 볼륨을 만든 다음 그 후에 다른 로컬로 고정된 볼륨을 즉시 만드는 경우 볼륨 만들기 작업은 순차적으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-222">If you create a locally pinned volume and then create another locally pinned volume immediately afterwards, the volume creation jobs run sequentially.</span></span> <span data-ttu-id="a32bf-223">첫 번째 볼륨 만들기 작업은 다음 볼륨 만들기 작업을 시작하기 전에 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-223">The first volume creation job must finish before the next volume creation job can begin.</span></span>

## <a name="modify-a-volume"></a><span data-ttu-id="a32bf-224">볼륨 수정</span><span class="sxs-lookup"><span data-stu-id="a32bf-224">Modify a volume</span></span>

<span data-ttu-id="a32bf-225">볼륨을 확장하거나 볼륨에 액세스하는 호스트를 변경할 경우 볼륨을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-225">Modify a volume when you need to expand it or change the hosts that access the volume.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="a32bf-226">장치에서 볼륨 크기를 수정하는 경우 볼륨 크기를 호스트에서도 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-226">If you modify the volume size on the device, the volume size needs to be changed on the host as well.</span></span>
> * <span data-ttu-id="a32bf-227">여기에 설명된 호스트 쪽 단계는 Windows Server 2012(2012R2)에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-227">The host-side steps described here are for Windows Server 2012 (2012R2).</span></span> <span data-ttu-id="a32bf-228">Linux 또는 다른 호스트 운영 체제에 대한 절차는 이와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-228">Procedures for Linux or other host operating systems will be different.</span></span> <span data-ttu-id="a32bf-229">다른 운영 체제를 실행하는 호스트의 볼륨을 수정하는 경우 해당 호스트 운영 체제 지침을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a32bf-229">Refer to your host operating system instructions when modifying the volume on a host running another operating system.</span></span>

#### <a name="to-modify-a-volume"></a><span data-ttu-id="a32bf-230">볼륨을 수정하려면</span><span class="sxs-lookup"><span data-stu-id="a32bf-230">To modify a volume</span></span>

1. <span data-ttu-id="a32bf-231">StorSimple 장치 관리자 서비스로 이동한 다음 **장치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-231">Go to your StorSimple Device Manager service and then click **Devices**.</span></span> <span data-ttu-id="a32bf-232">장치의 테이블 형식 목록에서 수정하려는 볼륨이 있는 장치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-232">From the tabular listing of the devices, select the device that has the volume that you intend to modify.</span></span> <span data-ttu-id="a32bf-233">**설정 > 볼륨**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-233">Click **Settings > Volumes**.</span></span>

    ![볼륨 블레이드로 이동](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

2. <span data-ttu-id="a32bf-235">볼륨의 테이블 형식 목록에서 볼륨을 선택하고 마우스 오른쪽 단추로 클릭하여 상황에 맞는 메뉴 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-235">From the tabular listing of volumes, select the volume and right-click to invoke the context menu.</span></span> <span data-ttu-id="a32bf-236">**오프라인으로 전환**을 선택하여 오프라인 상태를 수정할 볼륨을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-236">Select **Take offline** to take the volume you will modify offline.</span></span>

    ![볼륨 선택 및 오프라인으로 전환](./media/storsimple-8000-manage-volumes-u2/modifyvol4.png)

3. <span data-ttu-id="a32bf-238">**오프라인으로 전환** 블레이드에서 볼륨을 오프라인으로 전환하는 영향을 검토하고 해당하는 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-238">In the **Take offline** blade, review the impact of taking the volume offline and select the corresponding checkbox.</span></span> <span data-ttu-id="a32bf-239">먼저 호스트에서 해당 볼륨이 오프라인 상태인지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-239">Ensure that the corresponding volume on the host is offline first.</span></span> <span data-ttu-id="a32bf-240">StorSimple에 연결된 호스트 서버에서 볼륨을 오프라인으로 전환하는 방법에 대한 정보는 운영 체제 관련 지침을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a32bf-240">For information on how to take a volume offline on your host server connected to StorSimple, refer to operating system specific instructions.</span></span> <span data-ttu-id="a32bf-241">**오프라인으로 전환**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-241">Click **Take offline**.</span></span>

    ![볼륨을 오프라인으로 전환하는 영향 검토](./media/storsimple-8000-manage-volumes-u2/modifyvol5.png)

4. <span data-ttu-id="a32bf-243">볼륨이 오프라인 상태가 되면(볼륨 상태에 표시된 대로) 볼륨을 선택하고 마우스 오른쪽 단추로 클릭하여 상황에 맞는 메뉴를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-243">After the volume is offline (as shown by the volume status), select the volume and right-click to invoke the context menu.</span></span> <span data-ttu-id="a32bf-244">**볼륨 수정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-244">Select **Modify volume**.</span></span>

    ![볼륨 수정 선택](./media/storsimple-8000-manage-volumes-u2/modifyvol9.png)


5. <span data-ttu-id="a32bf-246">**볼륨 수정** 블레이드에서 다음과 같이 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-246">In the **Modify volume** blade, you can make the following changes:</span></span>
   
   1. <span data-ttu-id="a32bf-247">볼륨 **이름**을 편집할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-247">The volume **Name** cannot be edited.</span></span>
   2. <span data-ttu-id="a32bf-248">**형식**을 로컬로 고정에서 계층화 또는 계층화에서 로컬로 고정으로 변환합니다(자세한 내용은 [볼륨 유형 변경](#change-the-volume-type) 참조).</span><span class="sxs-lookup"><span data-stu-id="a32bf-248">Convert the **Type** from locally pinned to tiered or from tiered to locally pinned (see [Change the volume type](#change-the-volume-type) for more information).</span></span>
   3. <span data-ttu-id="a32bf-249">**프로비전된 용량**을 늘립니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-249">Increase the **Provisioned Capacity**.</span></span> <span data-ttu-id="a32bf-250">**프로비전된 용량** 은 늘릴 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-250">The **Provisioned Capacity** can only be increased.</span></span> <span data-ttu-id="a32bf-251">만든 후에는 볼륨을 축소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-251">You cannot shrink a volume after it is created.</span></span>
   4. <span data-ttu-id="a32bf-252">**연결된 호스트**에서 ACR을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-252">Under **Connected hosts**, you can modify the ACR.</span></span> <span data-ttu-id="a32bf-253">ACR을 수정하려면 볼륨은 오프라인 상태여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-253">To modify an ACR, the volume must be offline.</span></span>

       ![볼륨을 오프라인으로 전환하는 영향 검토](./media/storsimple-8000-manage-volumes-u2/modifyvol11.png)

5. <span data-ttu-id="a32bf-255">**저장**을 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-255">Click **Save** to save your changes.</span></span> <span data-ttu-id="a32bf-256">확인하라는 메시지가 표시되면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-256">When prompted for confirmation, click **Yes**.</span></span> <span data-ttu-id="a32bf-257">Azure 포털에 볼륨 업데이트 중 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-257">The Azure portal will display an updating volume message.</span></span> <span data-ttu-id="a32bf-258">볼륨이 성공적으로 업데이트되면 성공 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-258">It will display a success message when the volume has been successfully updated.</span></span>

    ![볼륨을 오프라인으로 전환하는 영향 검토](./media/storsimple-8000-manage-volumes-u2/modifyvol5.png)

7. <span data-ttu-id="a32bf-260">볼륨을 확장하는 경우 Windows 호스트 컴퓨터에서 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-260">If you are expanding a volume, complete the following steps on your Windows host computer:</span></span>
   
   1. <span data-ttu-id="a32bf-261">**컴퓨터 관리** ->**디스크 관리**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-261">Go to **Computer Management** ->**Disk Management**.</span></span>
   2. <span data-ttu-id="a32bf-262">**디스크 관리**를 마우스 오른쪽 단추로 클릭하고 **디스크 다시 검사**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-262">Right-click **Disk Management** and select **Rescan Disks**.</span></span>
   3. <span data-ttu-id="a32bf-263">디스크 목록에서 업데이트한 볼륨을 선택하고 마우스 오른쪽 단추를 클릭한 다음 **볼륨 확장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-263">In the list of disks, select the volume that you updated, right-click, and then select **Extend Volume**.</span></span> <span data-ttu-id="a32bf-264">볼륨 확장 마법사가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-264">The Extend Volume wizard starts.</span></span> <span data-ttu-id="a32bf-265">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-265">Click **Next**.</span></span>
   4. <span data-ttu-id="a32bf-266">기본값을 적용하여 마법사를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-266">Complete the wizard, accepting the default values.</span></span> <span data-ttu-id="a32bf-267">마법사가 완료되면 볼륨에 증가된 크기가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-267">After the wizard is finished, the volume should show the increased size.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="a32bf-268">로컬로 고정된 볼륨을 확장한 다음 그 후에 다른 로컬로 고정된 볼륨을 즉시 확장하는 경우 볼륨 확장 작업은 순차적으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-268">If you expand a locally pinned volume and then expand another locally pinned volume immediately afterwards, the volume expansion jobs run sequentially.</span></span> <span data-ttu-id="a32bf-269">첫 번째 볼륨 확장 작업은 다음 볼륨 확장 작업을 시작하기 전에 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-269">The first volume expansion job must finish before the next volume expansion job can begin.</span></span>
      

## <a name="change-the-volume-type"></a><span data-ttu-id="a32bf-270">볼륨 유형 변경</span><span class="sxs-lookup"><span data-stu-id="a32bf-270">Change the volume type</span></span>

<span data-ttu-id="a32bf-271">계층화에서 로컬로 고정 또는 로컬로 고정에서 계층화로 볼륨 유형을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-271">You can change the volume type from tiered to locally pinned or from locally pinned to tiered.</span></span> <span data-ttu-id="a32bf-272">그러나 이 변환은 자주 발생해서는 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-272">However, this conversion should not be a frequent occurrence.</span></span>

### <a name="tiered-to-local-volume-conversion-considerations"></a><span data-ttu-id="a32bf-273">계층화된 볼륨에서 로컬 볼륨으로 전환 시 고려 사항</span><span class="sxs-lookup"><span data-stu-id="a32bf-273">Tiered to local volume conversion considerations</span></span>

<span data-ttu-id="a32bf-274">볼륨을 계층화에서 로컬로 고정으로 변환하는 몇 가지 이유는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-274">Some reasons for converting a volume from tiered to locally pinned are:</span></span>

* <span data-ttu-id="a32bf-275">데이터 가용성 및 성능에 대한 로컬 보장</span><span class="sxs-lookup"><span data-stu-id="a32bf-275">Local guarantees regarding data availability and performance</span></span>
* <span data-ttu-id="a32bf-276">클라우드 대기 시간 및 클라우드 연결 문제를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-276">Elimination of cloud latencies and cloud connectivity issues.</span></span>

<span data-ttu-id="a32bf-277">일반적으로 자주 액세스하려는 작은 기존 볼륨입니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-277">Typically, these are small existing volumes that you want to access frequently.</span></span> <span data-ttu-id="a32bf-278">로컬로 고정된 볼륨은 생성될 때 완벽하게 프로비전됩니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-278">A locally pinned volume is fully provisioned when it is created.</span></span> 

<span data-ttu-id="a32bf-279">계층화된 볼륨을 로컬로 고정된 볼륨으로 변환하는 경우 StorSimple에서 변환을 시작하기 전에 장치에 공간이 충분한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-279">If you are converting a tiered volume to a locally pinned volume, StorSimple verifies that you have sufficient space on your device before it starts the conversion.</span></span> <span data-ttu-id="a32bf-280">공간이 부족한 경우 오류 메시지가 나타나고 작업이 취소됩니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-280">If you have insufficient space, you will receive an error and the operation will be canceled.</span></span> 

> [!NOTE]
> <span data-ttu-id="a32bf-281">계층화에서 로컬로 고정으로 변환을 시작하기 전에 다른 작업의 공간 요구 사항을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-281">Before you begin a conversion from tiered to locally pinned, make sure that you consider the space requirements of your other workloads.</span></span> 

<span data-ttu-id="a32bf-282">계층화된 볼륨에서 로컬로 고정된 볼륨으로 변환하면 장치 성능에 부정적인 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-282">Conversion from a tiered to a locally pinned volume can adversely affect device performance.</span></span> <span data-ttu-id="a32bf-283">또한 다음과 같은 요소가 변환을 완료하는 데 걸리는 시간을 증가시킬 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-283">Additionally, the following factors might increase the time it takes to complete the conversion:</span></span>

* <span data-ttu-id="a32bf-284">대역폭이 충분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-284">There is insufficient bandwidth.</span></span>
* <span data-ttu-id="a32bf-285">현재 백업이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-285">There is no current backup.</span></span>

<span data-ttu-id="a32bf-286">이러한 요소에 있는 영향을 최소화하려면</span><span class="sxs-lookup"><span data-stu-id="a32bf-286">To minimize the effects that these factors may have:</span></span>

* <span data-ttu-id="a32bf-287">대역폭 제한 정책을 검토하고 전용 40Mbps 대역폭을 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-287">Review your bandwidth throttling policies and make sure that a dedicated 40 Mbps bandwidth is available.</span></span>
* <span data-ttu-id="a32bf-288">사용량이 적은 시간에 변환을 예약합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-288">Schedule the conversion for off-peak hours.</span></span>
* <span data-ttu-id="a32bf-289">변환을 시작하기 전에 클라우드 스냅숏을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-289">Take a cloud snapshot before you start the conversion.</span></span>

<span data-ttu-id="a32bf-290">다양한 워크로드를 지원하는 여러 볼륨을 변환하는 경우 우선 순위가 높은 볼륨이 먼저 변환되도록 볼륨 변환의 우선 순위를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-290">If you are converting multiple volumes (supporting different workloads), then you should prioritize the volume conversion so that higher priority volumes are converted first.</span></span> <span data-ttu-id="a32bf-291">예를 들어 파일 공유 워크로드가 있는 볼륨을 변환하기 전에 VM(가상 컴퓨터)을 호스트하는 볼륨 또는 SQL 워크로드가 있는 볼륨을 변환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-291">For example, you should convert volumes that host virtual machines (VMs) or volumes with SQL workloads before you convert volumes with file share workloads.</span></span>

### <a name="local-to-tiered-volume-conversion-considerations"></a><span data-ttu-id="a32bf-292">로컬 볼륨에서 계층화된 볼륨으로 전환 시 고려 사항</span><span class="sxs-lookup"><span data-stu-id="a32bf-292">Local to tiered volume conversion considerations</span></span>

<span data-ttu-id="a32bf-293">다른 볼륨을 프로비전할 추가 공간이 필요한 경우 로컬 고정 볼륨을 계층화된 볼륨으로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-293">You may want to change a locally pinned volume to a tiered volume if you need additional space to provision other volumes.</span></span> <span data-ttu-id="a32bf-294">로컬로 고정된 볼륨을 계층화로 변환하는 경우 장치의 사용 가능한 용량은 출시된 용량의 크기에 따라 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-294">When you convert the locally pinned volume to tiered, the available capacity on the device increases by the size of the released capacity.</span></span> <span data-ttu-id="a32bf-295">연결 문제로 인해 로컬 유형에서 계층화 유형으로 볼륨의 변환을 막는 경우 로컬 볼륨은 전환이 완료될 때까지 계층화된 볼륨의 속성을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-295">If connectivity issues prevent the conversion of a volume from the local type to the tiered type, the local volume will exhibit properties of a tiered volume until the conversion is complete.</span></span> <span data-ttu-id="a32bf-296">일부 데이터가 클라우드로 분산되었을 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-296">This is because some data might have spilled to the cloud.</span></span> <span data-ttu-id="a32bf-297">이 분산된 데이터는 장치에서 로컬 공간을 계속 차지하고 작업을 다시 시작하고 완료할 때까지 해제될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-297">This spilled data continues to occupy local space on the device that cannot be freed until the operation is restarted and completed.</span></span>

> [!NOTE]
> <span data-ttu-id="a32bf-298">볼륨 변환은 다소 시간이 걸릴 수 있으며 시작된 후에 변환을 취소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-298">Converting a volume can take some time and you cannot cancel a conversion after it starts.</span></span> <span data-ttu-id="a32bf-299">볼륨을 변환하는 동안 온라인 상태로 유지되고 백업을 가져올 수 있지만 변환이 진행되는 동안 볼륨을 확장하거나 복원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-299">The volume remains online during the conversion, and you can take backups, but you cannot expand or restore the volume while the conversion is taking place.</span></span>


#### <a name="to-change-the-volume-type"></a><span data-ttu-id="a32bf-300">볼륨 유형을 변경하려면</span><span class="sxs-lookup"><span data-stu-id="a32bf-300">To change the volume type</span></span>

1. <span data-ttu-id="a32bf-301">StorSimple 장치 관리자 서비스로 이동한 다음 **장치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-301">Go to your StorSimple Device Manager service and then click **Devices**.</span></span> <span data-ttu-id="a32bf-302">장치의 테이블 형식 목록에서 수정하려는 볼륨이 있는 장치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-302">From the tabular listing of the devices, select the device that has the volume that you intend to modify.</span></span> <span data-ttu-id="a32bf-303">**설정 > 볼륨**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-303">Click **Settings > Volumes**.</span></span>

    ![볼륨 블레이드로 이동](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

3. <span data-ttu-id="a32bf-305">볼륨의 테이블 형식 목록에서 볼륨을 선택하고 마우스 오른쪽 단추로 클릭하여 상황에 맞는 메뉴 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-305">From the tabular listing of volumes, select the volume and right-click to invoke the context menu.</span></span> <span data-ttu-id="a32bf-306">**수정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-306">Select **Modify**.</span></span>

    ![상황에 맞는 메뉴에서 수정 선택](./media/storsimple-8000-manage-volumes-u2/changevoltype2.png)

4. <span data-ttu-id="a32bf-308">**볼륨 수정** 블레이드의 **형식** 드롭다운 목록에서 새 형식을 선택하여 볼륨 형식을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-308">On the **Modify volume** blade, change the volume type by selecting the new type from the **Type** drop-down list.</span></span>
   
   * <span data-ttu-id="a32bf-309">유형을 **로컬로 고정**으로 변경하는 경우 StorSimple에서 충분한 용량이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-309">If you are changing the type to **Locally pinned**, StorSimple will check to see if there is sufficient capacity.</span></span>
   * <span data-ttu-id="a32bf-310">유형을 **계층화됨**으로 변경하고 이 볼륨을 보관 데이터에 대해 사용하는 경우 **자주 액세스하지 않는 아카이브 데이터에 이 볼륨 사용** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-310">If you are changing the type to **Tiered** and this volume will be used for archival data, select the **Use this volume for less frequently accessed archival data** check box.</span></span>
   * <span data-ttu-id="a32bf-311">로컬 고정 볼륨을 계층화된 볼륨으로 구성하거나 _반대로_ 구성하는 경우 다음과 같은 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-311">If you are configuring a locally pinned volume as tiered or _vice-versa_, the following message appears.</span></span>
   
    ![볼륨 유형 변경 메시지](./media/storsimple-8000-manage-volumes-u2/changevoltype3.png)

7. <span data-ttu-id="a32bf-313">**저장**을 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-313">Click **Save** to save the changes.</span></span> <span data-ttu-id="a32bf-314">확인 메시지가 나타나면 **예**를 클릭하여 전환 프로세스가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-314">When prompted for confirmation, click **Yes** to start the conversion process.</span></span> 

    ![저장 및 확인](./media/storsimple-8000-manage-volumes-u2/modifyvol11.png)

8. <span data-ttu-id="a32bf-316">Azure Portal은 볼륨을 업데이트하는 작업 생성에 대한 알림을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-316">The Azure portal displays a notification for the job creation that would update the volume.</span></span> <span data-ttu-id="a32bf-317">볼륨 전환 작업의 상태를 모니터링하려면 알림을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-317">Click on the notification to monitor the status of the volume conversion job.</span></span>

    ![볼륨 전환을 위한 작업](./media/storsimple-8000-manage-volumes-u2/changevoltype5.png)

## <a name="take-a-volume-offline"></a><span data-ttu-id="a32bf-319">볼륨을 오프라인으로 전환</span><span class="sxs-lookup"><span data-stu-id="a32bf-319">Take a volume offline</span></span>

<span data-ttu-id="a32bf-320">볼륨을 수정 또는 삭제하려는 경우 볼륨을 오프라인으로 전환해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-320">You may need to take a volume offline when you are planning to modify or delete the volume.</span></span> <span data-ttu-id="a32bf-321">볼륨이 오프라인 상태인 경우 읽기 전용 액세스를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-321">When a volume is offline, it is not available for read-write access.</span></span> <span data-ttu-id="a32bf-322">호스트 및 장치에서 볼륨을 오프라인으로 전환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-322">You must take the volume offline on the host and the device.</span></span>

#### <a name="to-take-a-volume-offline"></a><span data-ttu-id="a32bf-323">볼륨을 오프라인으로 전환하려면</span><span class="sxs-lookup"><span data-stu-id="a32bf-323">To take a volume offline</span></span>

1. <span data-ttu-id="a32bf-324">오프라인으로 전환하기 전에 해당 볼륨을 사용 중이 아니어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-324">Make sure that the volume in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="a32bf-325">먼저 호스트에서 볼륨을 오프라인으로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-325">Take the volume offline on the host first.</span></span> <span data-ttu-id="a32bf-326">이렇게 하면 볼륨에서 데이터가 손상될 잠재적 위험이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-326">This eliminates any potential risk of data corruption on the volume.</span></span> <span data-ttu-id="a32bf-327">특정 단계의 경우 호스트 운영 체제에 대한 지침을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a32bf-327">For specific steps, refer to the instructions for your host operating system.</span></span>
3. <span data-ttu-id="a32bf-328">호스트가 오프라인이 되면 다음 단계를 수행하여 장치의 볼륨을 오프라인으로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-328">After the host is offline, take the volume on the device offline by performing the following steps:</span></span>
   
    1. <span data-ttu-id="a32bf-329">StorSimple 장치 관리자 서비스로 이동한 다음 **장치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-329">Go to your StorSimple Device Manager service and then click **Devices**.</span></span> <span data-ttu-id="a32bf-330">장치의 테이블 형식 목록에서 수정하려는 볼륨이 있는 장치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-330">From the tabular listing of the devices, select the device that has the volume that you intend to modify.</span></span> <span data-ttu-id="a32bf-331">**설정 > 볼륨**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-331">Click **Settings > Volumes**.</span></span>

        ![볼륨 블레이드로 이동](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

    2. <span data-ttu-id="a32bf-333">볼륨의 테이블 형식 목록에서 볼륨을 선택하고 마우스 오른쪽 단추로 클릭하여 상황에 맞는 메뉴 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-333">From the tabular listing of volumes, select the volume and right-click to invoke the context menu.</span></span> <span data-ttu-id="a32bf-334">**오프라인으로 전환**을 선택하여 오프라인 상태를 수정할 볼륨을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-334">Select **Take offline** to take the volume you will modify offline.</span></span>

        ![볼륨 선택 및 오프라인으로 전환](./media/storsimple-8000-manage-volumes-u2/modifyvol4.png)

3. <span data-ttu-id="a32bf-336">**오프라인으로 전환** 블레이드에서 볼륨을 오프라인으로 전환하는 영향을 검토하고 해당하는 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-336">In the **Take offline** blade, review the impact of taking the volume offline and select the corresponding checkbox.</span></span> <span data-ttu-id="a32bf-337">**오프라인으로 전환**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-337">Click **Take offline**.</span></span> 

    ![볼륨을 오프라인으로 전환하는 영향 검토](./media/storsimple-8000-manage-volumes-u2/modifyvol5.png)
      
      <span data-ttu-id="a32bf-339">볼륨이 오프라인 상태가 되면 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-339">You are notified when the volume is offline.</span></span> <span data-ttu-id="a32bf-340">볼륨 상태도 오프라인으로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-340">The volume status also updates to Offline.</span></span>
      
4. <span data-ttu-id="a32bf-341">볼륨이 오프라인 상태가 된 후에 볼륨을 선택하고 마우스 오른쪽 단추로 클릭한 경우 **온라인 상태로 만들기** 옵션은 상황에 맞는 메뉴에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-341">After a volume is offline, if you select the volume and right-click, **Bring Online** option becomes available in the context menu.</span></span>

> [!NOTE]
> <span data-ttu-id="a32bf-342">**오프라인으로 전환** 명령은 볼륨을 오프라인으로 전환하라는 요청을 장치에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-342">The **Take Offline** command sends a request to the device to take the volume offline.</span></span> <span data-ttu-id="a32bf-343">호스트에서 여전히 해당 볼륨을 사용하는 경우 연결이 끊어지고 볼륨을 오프라인으로 전환이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-343">If hosts are still using the volume, this results in broken connections, but taking the volume offline will not fail.</span></span>

## <a name="delete-a-volume"></a><span data-ttu-id="a32bf-344">볼륨 삭제</span><span class="sxs-lookup"><span data-stu-id="a32bf-344">Delete a volume</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a32bf-345">오프라인 상태인 경우에만 볼륨을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-345">You can delete a volume only if it is offline.</span></span>

<span data-ttu-id="a32bf-346">볼륨을 삭제하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-346">Complete the following steps to delete a volume.</span></span>

#### <a name="to-delete-a-volume"></a><span data-ttu-id="a32bf-347">볼륨을 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="a32bf-347">To delete a volume</span></span>

1. <span data-ttu-id="a32bf-348">StorSimple 장치 관리자 서비스로 이동한 다음 **장치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-348">Go to your StorSimple Device Manager service and then click **Devices**.</span></span> <span data-ttu-id="a32bf-349">장치의 테이블 형식 목록에서 수정하려는 볼륨이 있는 장치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-349">From the tabular listing of the devices, select the device that has the volume that you intend to modify.</span></span> <span data-ttu-id="a32bf-350">**설정 > 볼륨**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-350">Click **Settings > Volumes**.</span></span>

    ![볼륨 블레이드로 이동](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

3. <span data-ttu-id="a32bf-352">삭제하려는 볼륨의 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-352">Check the status of the volume you want to delete.</span></span> <span data-ttu-id="a32bf-353">삭제하려는 볼륨이 오프라인 상태가 아니면 먼저 오프라인으로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-353">If the volume you want to delete is not offline, take it offline first.</span></span> <span data-ttu-id="a32bf-354">[볼륨을 오프라인으로 전환](#take-a-volume-offline)단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-354">Follow the steps in [Take a volume offline](#take-a-volume-offline).</span></span>
4. <span data-ttu-id="a32bf-355">볼륨이 오프라인 상태가 된 후에 볼륨을 선택하고, 마우스 오른쪽 단추를 클릭하여 상황에 맞는 메뉴를 호출하고, **삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-355">After the volume is offline, select the volume, right-click to invoke the context menu and then select **Delete**.</span></span>

    ![상황에 맞는 메뉴에서 삭제 선택](./media/storsimple-8000-manage-volumes-u2/deletevol1.png)

5. <span data-ttu-id="a32bf-357">**삭제** 블레이드에서 볼륨을 삭제하는 영향에 대한 확인란을 검토하고 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-357">In the **Delete** blade, review and select the checkbox against the impact of deleting a volume.</span></span> <span data-ttu-id="a32bf-358">볼륨을 삭제하면 해당 볼륨에 있는 모든 데이터가 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-358">When you delete a volume, all the data that resides on the volume is lost.</span></span> 

    ![변경 내용 저장 및 확인](./media/storsimple-8000-manage-volumes-u2/deletevol2.png)

6. <span data-ttu-id="a32bf-360">볼륨을 삭제한 후에 볼륨의 테이블 형식 목록이 삭제를 나타내도록 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-360">After the volume is deleted, the tabular list of volumes updates to indicate the deletion.</span></span>

    ![업데이트된 볼륨 목록](./media/storsimple-8000-manage-volumes-u2/deletevol3.png)
   
   > [!NOTE]
   > <span data-ttu-id="a32bf-362">로컬에 고정된 볼륨을 삭제하면 새 볼륨에 사용할 수 있는 공간이 즉시 업데이트되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-362">If you delete a locally pinned volume, the space available for new volumes may not be updated immediately.</span></span> <span data-ttu-id="a32bf-363">StorSimple 장치 관리자 서비스는 사용 가능한 로컬 공간을 주기적으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-363">The StorSimple Device Manager Service updates the local space available periodically.</span></span> <span data-ttu-id="a32bf-364">새 볼륨을 만들기 전에 몇 분 동안 기다려 주세요.</span><span class="sxs-lookup"><span data-stu-id="a32bf-364">We suggest you wait for a few minutes before you try to create the new volume.</span></span>
   >
   > <span data-ttu-id="a32bf-365">또한 로컬로 고정된 볼륨을 삭제한 다음 그 후에 다른 로컬로 고정된 볼륨을 즉시 삭제하는 경우 볼륨 삭제 작업은 순차적으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-365">Additionally, if you delete a locally pinned volume and then delete another locally pinned volume immediately afterwards, the volume deletion jobs run sequentially.</span></span> <span data-ttu-id="a32bf-366">첫 번째 볼륨 삭제 작업은 다음 볼륨 삭제 작업을 시작하기 전에 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-366">The first volume deletion job must finish before the next volume deletion job can begin.</span></span>

## <a name="monitor-a-volume"></a><span data-ttu-id="a32bf-367">볼륨 모니터링</span><span class="sxs-lookup"><span data-stu-id="a32bf-367">Monitor a volume</span></span>

<span data-ttu-id="a32bf-368">볼륨 모니터링을 사용하면 볼륨에 대한 I/O 관련 통계를 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-368">Volume monitoring allows you to collect I/O-related statistics for a volume.</span></span> <span data-ttu-id="a32bf-369">사용자가 만드는 첫 32개의 볼륨에 대해 기본적으로 모니터링을 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-369">Monitoring is enabled by default for the first 32 volumes that you create.</span></span> <span data-ttu-id="a32bf-370">추가 볼륨의 모니터링은 기본적으로 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-370">Monitoring of additional volumes is disabled by default.</span></span> 

> [!NOTE]
> <span data-ttu-id="a32bf-371">복제된 볼륨의 모니터링은 기본적으로 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-371">Monitoring of cloned volumes is disabled by default.</span></span>


<span data-ttu-id="a32bf-372">볼륨 모니터링을 사용하도록 또는 사용하지 않도록 설정하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-372">Perform the following steps to enable or disable monitoring for a volume.</span></span>

#### <a name="to-enable-or-disable-volume-monitoring"></a><span data-ttu-id="a32bf-373">볼륨 모니터링을 사용 또는 사용하지 않도록 설정하려면</span><span class="sxs-lookup"><span data-stu-id="a32bf-373">To enable or disable volume monitoring</span></span>

1. <span data-ttu-id="a32bf-374">StorSimple 장치 관리자 서비스로 이동한 다음 **장치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-374">Go to your StorSimple Device Manager service and then click **Devices**.</span></span> <span data-ttu-id="a32bf-375">장치의 테이블 형식 목록에서 수정하려는 볼륨이 있는 장치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-375">From the tabular listing of the devices, select the device that has the volume that you intend to modify.</span></span> <span data-ttu-id="a32bf-376">**설정 > 볼륨**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-376">Click **Settings > Volumes**.</span></span>
2. <span data-ttu-id="a32bf-377">볼륨의 테이블 형식 목록에서 볼륨을 선택하고 마우스 오른쪽 단추로 클릭하여 상황에 맞는 메뉴 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-377">From the tabular listing of volumes, select the volume and right-click to invoke the context menu.</span></span> <span data-ttu-id="a32bf-378">**수정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-378">Select **Modify**.</span></span>
3. <span data-ttu-id="a32bf-379">**볼륨 수정** 블레이드의 **모니터링**에서 **사용** 또는 **사용 안 함**을 선택하여 모니터링을 사용하거나 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-379">In the **Modify volume** blade, for **Monitoring** select **Enable** or **Disable** to enable or disable monitoring.</span></span>

    ![모니터링 사용 안 함](./media/storsimple-8000-manage-volumes-u2/monitorvol1.png) 

4. <span data-ttu-id="a32bf-381">**저장**을 클릭하고 확인하라는 메시지가 표시되면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-381">Click **Save** and when prompted for confirmation, click **Yes**.</span></span> <span data-ttu-id="a32bf-382">Azure Portal에서는 볼륨을 업데이트하기 위한 알림을 표시한 다음 볼륨이 성공적으로 업데이트된 후에 성공 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-382">The Azure portal displays a notification for updating the volume and then a success message, after the volume is successfully updated.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a32bf-383">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a32bf-383">Next steps</span></span>

* <span data-ttu-id="a32bf-384">[StorSimple 볼륨 복제](storsimple-8000-clone-volume-u2.md)방법에 대해 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-384">Learn how to [clone a StorSimple volume](storsimple-8000-clone-volume-u2.md).</span></span>
* <span data-ttu-id="a32bf-385">[StorSimple 장치 관리자 서비스를 사용하여 StorSimple 장치를 관리](storsimple-8000-manager-service-administration.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a32bf-385">Learn how to [use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

