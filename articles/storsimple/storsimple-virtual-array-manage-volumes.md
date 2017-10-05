---
title: "StorSimple Virtual Array에서 볼륨 관리 | Microsoft Docs"
description: "StorSimple 장치 관리자 및 이 기능을 사용하여 StorSimple 가상 배열에서 볼륨을 관리하는 방법을 설명합니다."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: caa6a26b-b7ba-4a05-b092-1a79450225cf
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: a507bf1866952cb79fa6334fed80c88cd207cd0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-device-manager-service-to-manage-volumes-on-the-storsimple-virtual-array"></a><span data-ttu-id="b4a6f-103">StorSimple 장치 관리자 서비스를 사용하여 StorSimple 가상 배열에서 볼륨 관리</span><span class="sxs-lookup"><span data-stu-id="b4a6f-103">Use StorSimple Device Manager service to manage volumes on the StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="b4a6f-104">개요</span><span class="sxs-lookup"><span data-stu-id="b4a6f-104">Overview</span></span>

<span data-ttu-id="b4a6f-105">이 자습서는 StorSimple 장치 관리자 서비스를 사용하여 StorSimple 가상 배열에서 볼륨을 만들고 관리하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-105">This tutorial explains how to use the StorSimple Device Manager service to create and manage volumes on your StorSimple Virtual Array.</span></span>

<span data-ttu-id="b4a6f-106">StorSimple 장치 관리자 서비스는 단일 웹 인터페이스에서 StorSimple 솔루션을 관리하는 Azure Portal의 확장입니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-106">The StorSimple Device Manager service is an extension in the Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="b4a6f-107">공유 및 볼륨 관리 외에도 StorSimple 장치 관리자 서비스를 사용하여 장치를 보고 관리하며, 경고를 보고, 백업 정책 및 백업 카탈로그를 보고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-107">In addition to managing shares and volumes, you can use the StorSimple Device Manager service to view and manage devices, view alerts, and view and manage backup policies and the backup catalog.</span></span>

## <a name="volume-types"></a><span data-ttu-id="b4a6f-108">볼륨 유형</span><span class="sxs-lookup"><span data-stu-id="b4a6f-108">Volume Types</span></span>

<span data-ttu-id="b4a6f-109">StorSimple 볼륨은 다음과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-109">StorSimple volumes can be:</span></span>

* <span data-ttu-id="b4a6f-110">**로컬로 고정**: 이러한 볼륨의 데이터는 항상 배열에 유지되고 클라우드로 분산되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-110">**Locally pinned**: Data in these volumes stays on the array at all times and does not spill to the cloud.</span></span>
* <span data-ttu-id="b4a6f-111">**계층화**: 이러한 볼륨의 데이터를 클라우드로 분산할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-111">**Tiered**: Data in these volumes can spill to the cloud.</span></span> <span data-ttu-id="b4a6f-112">계층화된 볼륨을 만들 때 공간의 약 10%는 로컬 계층에 프로비전되고 공간의 90%는 클라우드에 프로비전됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-112">When you create a tiered volume, approximately 10 % of the space is provisioned on the local tier and 90 % of the space is provisioned in the cloud.</span></span> <span data-ttu-id="b4a6f-113">예를 들어, 1TB 볼륨을 프로비전하는 경우 100GB는 로컬 공간에 상주하고 900GB는 데이터가 계층화될 때 클라우드에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-113">For example, if you provisioned a 1 TB volume, 100 GB would reside in the local space and 900 GB would be used in the cloud when the data tiers.</span></span> <span data-ttu-id="b4a6f-114">따라서 장치의 로컬 공간이 부족하면 로컬 계층에 필요한 10%를 사용할 수 없기 때문에 계층화된 볼륨을 프로비전할 수 없다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-114">This in turn implies that if you run out of all the local space on the device, you cannot provision a tiered volume (because the 10 % required on the local tier will not be available).</span></span>

### <a name="provisioned-capacity"></a><span data-ttu-id="b4a6f-115">프로비전된 용량</span><span class="sxs-lookup"><span data-stu-id="b4a6f-115">Provisioned capacity</span></span>
<span data-ttu-id="b4a6f-116">각 볼륨 유형에 대한 최대 프로비전된 용량에 대해 다음 표를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-116">Refer to the following table for maximum provisioned capacity for each volume type.</span></span>

| <span data-ttu-id="b4a6f-117">**제한 식별자**</span><span class="sxs-lookup"><span data-stu-id="b4a6f-117">**Limit identifier**</span></span>                                       | <span data-ttu-id="b4a6f-118">**제한**</span><span class="sxs-lookup"><span data-stu-id="b4a6f-118">**Limit**</span></span>     |
|------------------------------------------------------------|---------------|
| <span data-ttu-id="b4a6f-119">계층화 볼륨의 최소 크기</span><span class="sxs-lookup"><span data-stu-id="b4a6f-119">Minimum size of a tiered volume</span></span>                            | <span data-ttu-id="b4a6f-120">500GB</span><span class="sxs-lookup"><span data-stu-id="b4a6f-120">500 GB</span></span>        |
| <span data-ttu-id="b4a6f-121">계층화 볼륨의 최대 크기</span><span class="sxs-lookup"><span data-stu-id="b4a6f-121">Maximum size of a tiered volume</span></span>                            | <span data-ttu-id="b4a6f-122">5TB</span><span class="sxs-lookup"><span data-stu-id="b4a6f-122">5 TB</span></span>          |
| <span data-ttu-id="b4a6f-123">로컬로 고정된 볼륨의 최소 크기</span><span class="sxs-lookup"><span data-stu-id="b4a6f-123">Minimum size of a locally pinned volume</span></span>                    | <span data-ttu-id="b4a6f-124">50GB</span><span class="sxs-lookup"><span data-stu-id="b4a6f-124">50 GB</span></span>         |
| <span data-ttu-id="b4a6f-125">로컬로 고정된 볼륨의 최대 크기</span><span class="sxs-lookup"><span data-stu-id="b4a6f-125">Maximum size of a locally pinned volume</span></span>                    | <span data-ttu-id="b4a6f-126">500GB</span><span class="sxs-lookup"><span data-stu-id="b4a6f-126">500 GB</span></span>        |

## <a name="the-volumes-blade"></a><span data-ttu-id="b4a6f-127">볼륨 블레이드</span><span class="sxs-lookup"><span data-stu-id="b4a6f-127">The Volumes blade</span></span>
<span data-ttu-id="b4a6f-128">StorSimple 서비스 요약 블레이드의 **볼륨** 메뉴에서는 지정된 StorSimple 배열의 저장소 볼륨의 목록을 표시하고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-128">The **Volumes** menu on your StorSimple service summary blade displays the list of storage volumes on a given StorSimple array and allows you to manage them.</span></span>

![볼륨 블레이드](./media/storsimple-virtual-array-manage-volumes/volumes-blade.png)

<span data-ttu-id="b4a6f-130">볼륨은 다음과 같은 특성으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-130">A volume consists of a series of attributes:</span></span>

* <span data-ttu-id="b4a6f-131">**볼륨 이름** – 설명이 포함된 이름은 고유해야 하며 볼륨을 식별하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-131">**Volume Name** – A descriptive name that must be unique and helps identify the volume.</span></span>
* <span data-ttu-id="b4a6f-132">**상태** – 온라인 또는 오프라인 상태가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-132">**Status** – Can be online or offline.</span></span> <span data-ttu-id="b4a6f-133">오프라인인 경우 볼륨은 해당 볼륨을 사용하는 데 액세스가 허용된 초기자(서버)에 보이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-133">If a volume is offline, it is not visible to initiators (servers) that are allowed access to use the volume.</span></span>
* <span data-ttu-id="b4a6f-134">**유형** – 볼륨이 **계층화됨**(기본값) 또는 **로컬로 고정**인지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-134">**Type** – Indicates whether the volume is **Tiered** (the default) or **Locally pinned**.</span></span>
* <span data-ttu-id="b4a6f-135">**용량** - 용량은 초기자(서버)가 저장할 수 있는 데이터의 전체 크기에 비해 사용된 데이터의 양을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-135">**Capacity** – specifies the amount of data used as compared to the total amount of data that can be stored by the initiator (server).</span></span>
* <span data-ttu-id="b4a6f-136">**백업** – StorSimple 가상 배열의 경우에 모든 볼륨은 자동으로 백업에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-136">**Backup** – In case of the StorSimple Virtual Array, all volumes are automatically enabled for backup.</span></span>
* <span data-ttu-id="b4a6f-137">**연결된 호스트** – 이 볼륨에 대한 액세스가 허용된 초기자(서버)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-137">**Connected hosts** – Specifies the initiators (servers) that are allowed access to this volume.</span></span>

![볼륨 세부 정보](./media/storsimple-virtual-array-manage-volumes/volume-details.png)

<span data-ttu-id="b4a6f-139">이 자습서의 지침을 사용하여 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-139">Use the instructions in this tutorial to perform the following tasks:</span></span>

* <span data-ttu-id="b4a6f-140">볼륨 추가</span><span class="sxs-lookup"><span data-stu-id="b4a6f-140">Add a volume</span></span>
* <span data-ttu-id="b4a6f-141">볼륨 수정</span><span class="sxs-lookup"><span data-stu-id="b4a6f-141">Modify a volume</span></span>
* <span data-ttu-id="b4a6f-142">볼륨을 오프라인으로 전환</span><span class="sxs-lookup"><span data-stu-id="b4a6f-142">Take a volume offline</span></span>
* <span data-ttu-id="b4a6f-143">볼륨 삭제</span><span class="sxs-lookup"><span data-stu-id="b4a6f-143">Delete a volume</span></span>

## <a name="add-a-volume"></a><span data-ttu-id="b4a6f-144">볼륨 추가</span><span class="sxs-lookup"><span data-stu-id="b4a6f-144">Add a volume</span></span>

1. <span data-ttu-id="b4a6f-145">StorSimple 서비스 요약 블레이드의 명령 모음에서 **+볼륨 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-145">From the StorSimple service summary blade, click **+ Add volume** from the command bar.</span></span> <span data-ttu-id="b4a6f-146">그려면 **볼륨 추가** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-146">This opens up the **Add volume** blade.</span></span>
   
    ![볼륨 추가](./media/storsimple-virtual-array-manage-volumes/add-volume.png)
2. <span data-ttu-id="b4a6f-148">**볼륨 추가** 블레이드에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-148">In the **Add volume** blade, do the following:</span></span>
   
   * <span data-ttu-id="b4a6f-149">**볼륨 이름** 필드에서 볼륨의 고유 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-149">In the **Volume name** field, enter a unique name for your volume.</span></span> <span data-ttu-id="b4a6f-150">이름은 3~127개의 문자를 포함하는 문자열이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-150">The name must be a string that contains 3 to 127 characters.</span></span>
   * <span data-ttu-id="b4a6f-151">**형식** 드롭다운 목록에서 **계층** 또는 **로컬로 고정** 볼륨을 만들지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-151">In the **Type** dropdown list, specify whether to create a **Tiered** or **Locally pinned** volume.</span></span> <span data-ttu-id="b4a6f-152">로컬 보증, 낮은 대기 시간 및 높은 성능을 필요로 하는 워크로드의 경우 **로컬로 고정된 볼륨**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-152">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned volume**.</span></span> <span data-ttu-id="b4a6f-153">다른 모든 데이터에 대해서는 **계층화된** 볼륨을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-153">For all other data, select **Tiered** volume.</span></span>
   * <span data-ttu-id="b4a6f-154">**용량** 필드에서 볼륨의 크기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-154">In the **Capacity** field, specify the size of the volume.</span></span> <span data-ttu-id="b4a6f-155">계층화된 볼륨은 500GB에서 5TB 사이여야 하고 로컬로 고정된 볼륨은 50GB에서 500GB 사이여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-155">A tiered volume must be between 500 GB and 5 TB and a locally pinned volume must be between 50 GB and 500 GB.</span></span>
   * * <span data-ttu-id="b4a6f-156">**호스트 연결**을 클릭하고 이 볼륨에 연결하려는 iSCSI 초기자에 해당하는 ACR(액세스 제어 레코드)를 선택한 다음 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-156">Click **Connected hosts**, select an access control record (ACR) corresponding to the iSCSI initiator that you want to connect to this volume, and then click **Select**.</span></span>
3. <span data-ttu-id="b4a6f-157">새롭게 연결된 호스트를 추가하려면 **새로 추가**를 클릭하고 호스트의 이름 및 해당 IQN(iSCSI 정규화 이름)을 입력한 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-157">To add a new connected host, click **Add new**, enter a name for the host and its iSCSI Qualified Name (IQN), and then click **Add**.</span></span>
   
    ![볼륨 추가](./media/storsimple-virtual-array-manage-volumes/volume-add-acr.png)
4. <span data-ttu-id="b4a6f-159">볼륨 구성을 완료했다면 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-159">When you've finished configuring your volume, click **Create**.</span></span> <span data-ttu-id="b4a6f-160">볼륨이 지정된 설정으로 만들어지면 동일하게 성공적으로 만들었다는 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-160">A volume will be created with the specified settings and you will see a notification on the successful creation of the same.</span></span> <span data-ttu-id="b4a6f-161">기본적으로 볼륨에 대한 백업을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-161">By default backup will be enabled for the volume.</span></span>
5. <span data-ttu-id="b4a6f-162">볼륨이 성공적으로 만들어졌는지 확인하려면 **볼륨** 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-162">To confirm that the volume was successfully created, go to the **Volumes** blade.</span></span> <span data-ttu-id="b4a6f-163">볼륨이 목록으로 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-163">You should see the volume listed.</span></span>
   
    ![볼륨 만들기 성공](./media/storsimple-virtual-array-manage-volumes/volume-success.png)

## <a name="modify-a-volume"></a><span data-ttu-id="b4a6f-165">볼륨 수정</span><span class="sxs-lookup"><span data-stu-id="b4a6f-165">Modify a volume</span></span>

<span data-ttu-id="b4a6f-166">볼륨에 액세스하는 호스트를 변경할 경우 볼륨을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-166">Modify a volume when you need to change the hosts that access the volume.</span></span> <span data-ttu-id="b4a6f-167">볼륨을 만든 후에 볼륨의 다른 특성을 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-167">The other attributes of a volume cannot be modified once the volume has been created.</span></span>

#### <a name="to-modify-a-volume"></a><span data-ttu-id="b4a6f-168">볼륨을 수정하려면</span><span class="sxs-lookup"><span data-stu-id="b4a6f-168">To modify a volume</span></span>

1. <span data-ttu-id="b4a6f-169">StorSimple 서비스 요약 블레이드의 **볼륨** 설정에서 수정하려는 볼륨이 상주하는 가상 배열을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-169">From the **Volumes** setting on the StorSimple service summary blade, select the virtual array on which the volume you wish you to modify resides.</span></span>
2. <span data-ttu-id="b4a6f-170">볼륨을 **선택**하고 **연결된 호스트**를 클릭하여 현재 연결된 호스트를 보고 다른 서버로 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-170">**Select** the volume and click **Connected hosts** to view the currently connected host and modify it to a different server.</span></span>
   
    ![볼륨 편집](./media/storsimple-virtual-array-manage-volumes/volume-edit-acr.png)
3. <span data-ttu-id="b4a6f-172">**저장** 명령 모음을 클릭하여 변경 사항을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-172">Save your changes by clicking the **Save** command bar.</span></span> <span data-ttu-id="b4a6f-173">지정된 설정이 적용되고 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-173">Your specified settings will be applied and you will see a notification.</span></span>

## <a name="take-a-volume-offline"></a><span data-ttu-id="b4a6f-174">볼륨을 오프라인으로 전환</span><span class="sxs-lookup"><span data-stu-id="b4a6f-174">Take a volume offline</span></span>

<span data-ttu-id="b4a6f-175">볼륨을 수정 또는 삭제하려는 경우 볼륨을 오프라인으로 전환해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-175">You may need to take a volume offline when you are planning to modify it or delete it.</span></span> <span data-ttu-id="b4a6f-176">볼륨이 오프라인 상태인 경우 읽기 전용 액세스를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-176">When a volume is offline, it is not available for read-write access.</span></span> <span data-ttu-id="b4a6f-177">장치에서뿐 아니라 호스트에서도 볼륨을 오프라인으로 전환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-177">You will need to take the volume offline on the host as well as on the device.</span></span>

#### <a name="to-take-a-volume-offline"></a><span data-ttu-id="b4a6f-178">볼륨을 오프라인으로 전환하려면</span><span class="sxs-lookup"><span data-stu-id="b4a6f-178">To take a volume offline</span></span>

1. <span data-ttu-id="b4a6f-179">오프라인으로 전환하기 전에 해당 볼륨을 사용 중이 아니어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-179">Make sure that the volume in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="b4a6f-180">먼저 호스트에서 볼륨을 오프라인으로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-180">Take the volume offline on the host first.</span></span> <span data-ttu-id="b4a6f-181">이렇게 하면 볼륨에서 데이터가 손상될 잠재적 위험이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-181">This eliminates any potential risk of data corruption on the volume.</span></span> <span data-ttu-id="b4a6f-182">특정 단계의 경우 호스트 운영 체제에 대한 지침을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-182">For specific steps, refer to the instructions for your host operating system.</span></span>
3. <span data-ttu-id="b4a6f-183">호스트의 볼륨이 오프라인이 되면 다음 단계를 수행하여 배열의 볼륨을 오프라인으로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-183">After the volume on the host is offline, take the volume on the array  offline by performing the following steps:</span></span>
   
   * <span data-ttu-id="b4a6f-184">StorSimple 서비스 요약 블레이드의 **볼륨** 설정에서 오프라인으로 전환하려는 볼륨이 상주하는 가상 배열을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-184">From the **Volumes** setting on the StorSimple service summary blade, select the virtual array on which the volume you wish you to take offline resides.</span></span>
   * <span data-ttu-id="b4a6f-185">볼륨을 **선택**하고 **...**(또는 이 행의 오른쪽)를 클릭하고 상황에 맞는 메뉴에서 **오프라인으로 전환**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-185">**Select** the volume and click **...** (alternately right-click in this row) and from the context menu, select **Take offline**.</span></span>
     
        ![오프라인 볼륨](./media/storsimple-virtual-array-manage-volumes/volume-offline.png)
   * <span data-ttu-id="b4a6f-187">**오프라인** 블레이드에서 정보를 검토하고 작업에 대한 동의를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-187">Review the information in the **Take offline** blade and confirm your acceptance of the operation.</span></span> <span data-ttu-id="b4a6f-188">**오프라인으로 전환**을 클릭하여 볼륨을 오프라인으로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-188">Click **Take offline** to take the volume offline.</span></span> <span data-ttu-id="b4a6f-189">진행 중인 작업의 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-189">You will see a notification of the operation in progress.</span></span>
   * <span data-ttu-id="b4a6f-190">볼륨이 성공적으로 오프라인으로 전환되었는지 확인하려면 **볼륨** 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-190">To confirm that the volume was successfully taken offline, go to the **Volumes** blade.</span></span> <span data-ttu-id="b4a6f-191">볼륨의 상태가 오프라인으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-191">You should see the status of the volume as offline.</span></span>
     
       ![오프라인 볼륨 확인](./media/storsimple-virtual-array-manage-volumes/volume-offline-confirm.png)

## <a name="delete-a-volume"></a><span data-ttu-id="b4a6f-193">볼륨 삭제</span><span class="sxs-lookup"><span data-stu-id="b4a6f-193">Delete a volume</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b4a6f-194">오프라인 상태인 경우에만 볼륨을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-194">You can delete a volume only if it is offline.</span></span>
> 
> 

<span data-ttu-id="b4a6f-195">볼륨을 삭제하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-195">Complete the following steps to delete a volume.</span></span>

#### <a name="to-delete-a-volume"></a><span data-ttu-id="b4a6f-196">볼륨을 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="b4a6f-196">To delete a volume</span></span>

1. <span data-ttu-id="b4a6f-197">StorSimple 서비스 요약 블레이드의 **볼륨** 설정에서 삭제하려는 볼륨이 상주하는 가상 배열을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-197">From the **Volumes** setting on the StorSimple service summary blade, select the virtual array on which the volume you wish you to delete resides.</span></span>
2. <span data-ttu-id="b4a6f-198">볼륨을 **선택**하고 **...**(또는 이 행의 오른쪽)를 클릭하고 상황에 맞는 메뉴에서 **삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-198">**Select** the volume and click **...** (alternately right-click in this row) and from the context menu, select **Delete**.</span></span>
   
    ![볼륨 삭제](./media/storsimple-virtual-array-manage-volumes/volume-delete.png)
3. <span data-ttu-id="b4a6f-200">삭제하려는 볼륨의 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-200">Check the status of the volume you want to delete.</span></span> <span data-ttu-id="b4a6f-201">삭제하려는 볼륨이 오프라인 상태가 아닌 경우 [볼륨을 오프라인으로 전환](#take-a-volume-offline)의 단계를 따라 먼저 오프라인 상태로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-201">If the volume you want to delete is not offline, take it offline first, following the steps in [Take a volume offline](#take-a-volume-offline).</span></span>
4. <span data-ttu-id="b4a6f-202">**삭제** 블레이드에서 확인하라는 메시지가 나타나면 확인을 수락하고 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-202">When prompted for confirmation in the **Delete** blade, accept the confirmation and click **Delete**.</span></span> <span data-ttu-id="b4a6f-203">이제 볼륨이 삭제되고 **볼륨** 블레이드가 가상 배열 내의 업데이트된 볼륨 목록을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-203">The volume will now be deleted and the **Volumes** blade will show the updated list of volumes within the virtual array.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4a6f-204">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b4a6f-204">Next steps</span></span>

<span data-ttu-id="b4a6f-205">[StorSimple 볼륨 복제](storsimple-virtual-array-clone.md)방법에 대해 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="b4a6f-205">Learn how to [clone a StorSimple volume](storsimple-virtual-array-clone.md).</span></span>

