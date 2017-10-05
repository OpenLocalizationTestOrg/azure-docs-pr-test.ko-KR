---
title: "StorSimple Virtual Array 공유 관리 | Microsoft Docs"
description: "StorSimple 장치 관리자 및 이 기능을 사용하여 StorSimple 가상 배열에서 공유를 관리하는 방법을 설명합니다."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: 0a799c83-fde5-4f3f-af0e-67535d1882b6
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: e5c62689de36baa175001f5f4f70d87568876ef0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-manage-shares-on-the-storsimple-virtual-array"></a><span data-ttu-id="dbe96-103">StorSimple 장치 관리자 서비스를 사용하여 StorSimple 가상 배열에서 공유 관리</span><span class="sxs-lookup"><span data-stu-id="dbe96-103">Use the StorSimple Device Manager service to manage shares on the StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="dbe96-104">개요</span><span class="sxs-lookup"><span data-stu-id="dbe96-104">Overview</span></span>

<span data-ttu-id="dbe96-105">이 자습서는 StorSimple 장치 관리자 서비스를 사용하여 StorSimple 가상 배열에서 공유를 만들고 관리하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-105">This tutorial explains how to use the StorSimple Device Manager service to create and manage shares on your StorSimple Virtual Array.</span></span>

<span data-ttu-id="dbe96-106">StorSimple 장치 관리자 서비스는 단일 웹 인터페이스에서 StorSimple 솔루션을 관리하는 Azure Portal의 확장입니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-106">The StorSimple Device Manager service is an extension in the Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="dbe96-107">공유 및 볼륨 관리 외에도 StorSimple 장치 관리자 서비스를 사용하여 장치를 보고 관리하며, 경고를 보고, 백업 정책을 관리하고, 백업 카탈로그를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-107">In addition to managing shares and volumes, you can use the StorSimple Device Manager service to view and manage devices, view alerts, manage backup policies, and manage the backup catalog.</span></span>

## <a name="share-types"></a><span data-ttu-id="dbe96-108">공유 유형</span><span class="sxs-lookup"><span data-stu-id="dbe96-108">Share Types</span></span>

<span data-ttu-id="dbe96-109">StorSimple 공유는 다음과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-109">StorSimple shares can be:</span></span>

* <span data-ttu-id="dbe96-110">**로컬로 고정**: 이러한 공유의 데이터는 항상 배열에 유지되고 클라우드로 분산되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-110">**Locally pinned**: Data in these shares stays on the array at all times and does not spill to the cloud.</span></span>
* <span data-ttu-id="dbe96-111">**계층화**: 이러한 공유의 데이터를 클라우드로 분산할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-111">**Tiered**: Data in these shares can spill to the cloud.</span></span> <span data-ttu-id="dbe96-112">계층화된 공유를 만들 때 공간의 약 10%는 로컬 계층에 프로비전되고 공간의 90%는 클라우드에 프로비전됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-112">When you create a tiered share, approximately 10 % of the space is provisioned on the local tier and 90 % of the space is provisioned in the cloud.</span></span> <span data-ttu-id="dbe96-113">예를 들어, 1TB 공유를 프로비전하는 경우 100GB는 로컬 공간에 상주하고 900GB는 데이터가 계층화될 때 클라우드에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-113">For example, if you provisioned a 1 TB share, 100 GB would reside in the local space and 900 GB would be used in the cloud when the data tiers.</span></span> <span data-ttu-id="dbe96-114">따라서 장치의 로컬 공간이 부족하면 로컬 계층에 필요한 10%를 사용할 수 없기 때문에 계층화된 공유를 프로비전할 수 없다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-114">This in turn implies that if you run out of all the local space on the device, you cannot provision a tiered share (because the 10 % required on the local tier will not be available).</span></span>

### <a name="provisioned-capacity"></a><span data-ttu-id="dbe96-115">프로비전된 용량</span><span class="sxs-lookup"><span data-stu-id="dbe96-115">Provisioned capacity</span></span>

<span data-ttu-id="dbe96-116">각 공유 유형에 대한 최대 프로비전된 용량에 대해 다음 표를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dbe96-116">Refer to the following table for maximum provisioned capacity for each share type.</span></span>

| <span data-ttu-id="dbe96-117">**제한 식별자**</span><span class="sxs-lookup"><span data-stu-id="dbe96-117">**Limit identifier**</span></span> | <span data-ttu-id="dbe96-118">**제한**</span><span class="sxs-lookup"><span data-stu-id="dbe96-118">**Limit**</span></span> |
| --- | --- |
| <span data-ttu-id="dbe96-119">계층화 공유의 최소 크기</span><span class="sxs-lookup"><span data-stu-id="dbe96-119">Minimum size of a tiered share</span></span> |<span data-ttu-id="dbe96-120">500GB</span><span class="sxs-lookup"><span data-stu-id="dbe96-120">500 GB</span></span> |
| <span data-ttu-id="dbe96-121">계층화 공유의 최대 크기</span><span class="sxs-lookup"><span data-stu-id="dbe96-121">Maximum size of a tiered share</span></span> |<span data-ttu-id="dbe96-122">20TB</span><span class="sxs-lookup"><span data-stu-id="dbe96-122">20 TB</span></span> |
| <span data-ttu-id="dbe96-123">로컬로 고정된 공유의 최소 크기</span><span class="sxs-lookup"><span data-stu-id="dbe96-123">Minimum size of a locally pinned share</span></span> |<span data-ttu-id="dbe96-124">50GB</span><span class="sxs-lookup"><span data-stu-id="dbe96-124">50 GB</span></span> |
| <span data-ttu-id="dbe96-125">로컬로 고정된 공유의 최대 크기</span><span class="sxs-lookup"><span data-stu-id="dbe96-125">Maximum size of a locally pinned share</span></span> |<span data-ttu-id="dbe96-126">2TB</span><span class="sxs-lookup"><span data-stu-id="dbe96-126">2 TB</span></span> |

## <a name="the-shares-blade"></a><span data-ttu-id="dbe96-127">공유 블레이드</span><span class="sxs-lookup"><span data-stu-id="dbe96-127">The Shares blade</span></span>

<span data-ttu-id="dbe96-128">StorSimple 서비스 요약 블레이드의 **공유** 메뉴에서는 지정된 StorSimple 배열의 저장소 공유의 목록을 표시하고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-128">The **Shares** menu on your StorSimple service summary blade displays the list of storage shares on a given StorSimple array and allows you to manage them.</span></span>

![공유 블레이드](./media/storsimple-virtual-array-manage-shares/shares-blade.png)

<span data-ttu-id="dbe96-130">공유는 다음과 같은 특성으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-130">A share consists of a series of attributes:</span></span>

* <span data-ttu-id="dbe96-131">**공유 이름** – 설명이 포함된 이름은 고유해야 하며 공유를 식별하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-131">**Share Name** – A descriptive name that must be unique and helps identify the share.</span></span>
* <span data-ttu-id="dbe96-132">**상태** – 온라인 또는 오프라인 상태가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-132">**Status** – Can be online or offline.</span></span> <span data-ttu-id="dbe96-133">공유가 오프라인 상태이면 공유 사용자는 공유에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-133">If a share is offline, users of the share will not be able to access it.</span></span>
* <span data-ttu-id="dbe96-134">**유형** – 공유가 **계층화됨**(기본값) 또는 **로컬로 고정**인지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-134">**Type** – Indicates whether the share is **Tiered** (the default) or **Locally pinned**.</span></span>
* <span data-ttu-id="dbe96-135">**용량** - 용량은 공유에 저장할 수 있는 데이터의 전체 크기에 비해 사용된 데이터의 양을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-135">**Capacity** – specifies the amount of data used as compared to the total amount of data that can be stored on the share.</span></span>
* <span data-ttu-id="dbe96-136">**설명** – 공유를 설명하는 데 도움이 되는 옵션 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-136">**Description** – An optional setting that helps describe the share.</span></span>
* <span data-ttu-id="dbe96-137">**사용 권한** - Windows 탐색기를 통해 관리할 수 있는 공유에 대한 NTFS 사용 권한입니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-137">**Permissions** - The NTFS permissions to the share that can be managed through Windows Explorer.</span></span>
* <span data-ttu-id="dbe96-138">**백업** – StorSimple 가상 배열의 경우에 모든 공유는 자동으로 백업에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-138">**Backup** – In case of the StorSimple Virtual Array, all shares are automatically enabled for backup.</span></span>

![공유 세부 정보](./media/storsimple-virtual-array-manage-shares/share-details.png)

<span data-ttu-id="dbe96-140">이 자습서의 지침을 사용하여 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-140">Use the instructions in this tutorial to perform the following tasks:</span></span>

* <span data-ttu-id="dbe96-141">공유 추가</span><span class="sxs-lookup"><span data-stu-id="dbe96-141">Add a share</span></span>
* <span data-ttu-id="dbe96-142">공유 수정</span><span class="sxs-lookup"><span data-stu-id="dbe96-142">Modify a share</span></span>
* <span data-ttu-id="dbe96-143">오프라인으로 공유 전환</span><span class="sxs-lookup"><span data-stu-id="dbe96-143">Take a share offline</span></span>
* <span data-ttu-id="dbe96-144">공유 삭제</span><span class="sxs-lookup"><span data-stu-id="dbe96-144">Delete a share</span></span>

## <a name="add-a-share"></a><span data-ttu-id="dbe96-145">공유 추가</span><span class="sxs-lookup"><span data-stu-id="dbe96-145">Add a share</span></span>

1. <span data-ttu-id="dbe96-146">StorSimple 서비스 요약 블레이드의 명령 모음에서 **+공유 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-146">From the StorSimple service summary blade, click **+ Add share** from the command bar.</span></span> <span data-ttu-id="dbe96-147">그려면 **공유 추가** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-147">This opens up the **Add share** blade.</span></span>

    ![공유 추가](./media/storsimple-virtual-array-manage-shares/add-share.png)

2. <span data-ttu-id="dbe96-149">**공유 추가** 블레이드에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-149">In the **Add share** blade, do the following:</span></span>
   
    1. <span data-ttu-id="dbe96-150">**공유 이름** 필드에서 공유의 고유 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-150">In the **Share name** field, enter a unique name for your share.</span></span> <span data-ttu-id="dbe96-151">이름은 3~127개의 문자를 포함하는 문자열이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-151">The name must be a string that contains 3 to 127 characters.</span></span>

    2. <span data-ttu-id="dbe96-152">공유에 대한 선택적 **설명**입니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-152">An optional **Description** for the share.</span></span> <span data-ttu-id="dbe96-153">설명은 공유 소유자를 식별하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-153">The description will help identify the share owners.</span></span>

    3. <span data-ttu-id="dbe96-154">**형식** 드롭다운 목록에서 **계층** 또는 **로컬로 고정** 공유를 만들지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-154">In the **Type** dropdown list, specify whether to create a **Tiered** or **Locally pinned** share.</span></span> <span data-ttu-id="dbe96-155">로컬 보증, 낮은 대기 시간 및 높은 성능이 필요한 워크로드의 경우 **로컬로 고정된 공유**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-155">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned share**.</span></span> <span data-ttu-id="dbe96-156">다른 모든 데이터에 대해서는 **계층화된** 공유를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-156">For all other data, select **Tiered** share.</span></span>

    4. <span data-ttu-id="dbe96-157">**용량** 필드에서 공유의 크기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-157">In the **Capacity** field, specify the size of the share.</span></span> <span data-ttu-id="dbe96-158">계층화된 공유는 500GB에서 20TB 사이여야 하고 로컬로 고정된 공유는 50GB에서 2TB 사이여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-158">A tiered share must be between 500 GB and 20 TB and a locally pinned share must be between 50 GB and 2 TB.</span></span>

    5. <span data-ttu-id="dbe96-159">**전체 기본 사용 권한 설정** 필드에서 공유에 액세스할 사용자 또는 그룹에 권한을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-159">In the **Set default full permissions to** field, assign the permissions to the user, or the group that is accessing this share.</span></span> <span data-ttu-id="dbe96-160">사용자 또는 사용자 그룹의 이름을 _john@contoso.com_ 형식으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-160">Specify the name of the user or the user group in _john@contoso.com_ format.</span></span> <span data-ttu-id="dbe96-161">이 공유에 액세스하는 관리자 권한은 사용자 그룹(단일 사용자 대신)을 사용하여 허용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-161">We recommend that you use a user group (instead of a single user) to allow admin privileges to access these shares.</span></span> <span data-ttu-id="dbe96-162">여기에서 권한을 할당한 후에 파일 탐색기를 사용하여 해당 권한을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-162">After you have assigned the permissions here, you can then use File Explorer to modify these permissions.</span></span>
3. <span data-ttu-id="dbe96-163">공유 구성을 완료했다면 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-163">When you've finished configuring your share, click **Create**.</span></span> <span data-ttu-id="dbe96-164">지정한 설정으로 공유가 만들어지면 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-164">A share will be created with the specified settings and you will see a notification.</span></span> <span data-ttu-id="dbe96-165">기본적으로 공유에 대한 백업을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-165">By default, backup will be enabled for the share.</span></span>
4. <span data-ttu-id="dbe96-166">공유가 성공적으로 만들어졌는지 확인하려면 **공유** 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-166">To confirm that the share was successfully created, go to the **Shares** blade.</span></span> <span data-ttu-id="dbe96-167">공유가 목록으로 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-167">You should see the share listed.</span></span>
   
    ![공유 만들기 성공](./media/storsimple-virtual-array-manage-shares/share-success.png)

## <a name="modify-a-share"></a><span data-ttu-id="dbe96-169">공유 수정</span><span class="sxs-lookup"><span data-stu-id="dbe96-169">Modify a share</span></span>

<span data-ttu-id="dbe96-170">공유에 대한 설명을 변경해야 하는 경우 공유를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-170">Modify a share when you need to change the description of the share.</span></span> <span data-ttu-id="dbe96-171">공유가 만들어지면 다른 공유 속성을 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-171">No other share properties can be modified once the share is created.</span></span>

#### <a name="to-modify-a-share"></a><span data-ttu-id="dbe96-172">공유를 수정하려면</span><span class="sxs-lookup"><span data-stu-id="dbe96-172">To modify a share</span></span>

1. <span data-ttu-id="dbe96-173">StorSimple 서비스 요약 블레이드의 **공유** 설정에서 수정하려는 공유가 상주하는 가상 배열을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-173">From the **Shares** setting on the StorSimple service summary blade, select the virtual array on which the share you wish you to modify resides.</span></span>
2. <span data-ttu-id="dbe96-174">공유를 **선택**하여 공유에 대한 현재 설명을 보고 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-174">**Select** the share to view the current description and modify it.</span></span>
3. <span data-ttu-id="dbe96-175">**저장** 명령 모음을 클릭하여 변경 사항을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-175">Save your changes by clicking the **Save** command bar.</span></span> <span data-ttu-id="dbe96-176">지정된 설정이 적용되고 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-176">Your specified settings will be applied and you will see a notification.</span></span>
   
    ![ <span data-ttu-id="dbe96-177">공유 편집</span><span class="sxs-lookup"><span data-stu-id="dbe96-177">Edit share</span></span>](./media/storsimple-virtual-array-manage-shares/share-edit.png)

## <a name="take-a-share-offline"></a><span data-ttu-id="dbe96-178">오프라인으로 공유 전환</span><span class="sxs-lookup"><span data-stu-id="dbe96-178">Take a share offline</span></span>

<span data-ttu-id="dbe96-179">공유를 수정 또는 삭제하려는 경우 공유를 오프라인으로 전환해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-179">You may need to take a share offline when you are planning to modify it or delete it.</span></span> <span data-ttu-id="dbe96-180">공유가 오프라인 상태인 경우 읽기 전용 액세스를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-180">When a share is offline, it is not available for read-write access.</span></span> <span data-ttu-id="dbe96-181">장치에서뿐 아니라 호스트에서도 공유를 오프라인으로 전환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-181">You will need to take the share offline on the host as well as on the device.</span></span>

#### <a name="to-take-a-share-offline"></a><span data-ttu-id="dbe96-182">오프라인으로 공유를 전환하려면</span><span class="sxs-lookup"><span data-stu-id="dbe96-182">To take a share offline</span></span>

1. <span data-ttu-id="dbe96-183">오프라인으로 전환하기 전에 해당 공유를 사용 중이 아니어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-183">Make sure that the share in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="dbe96-184">다음 단계를 수행하여 오프라인으로 배열의 공유를 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-184">Take the share on the array offline by performing the following steps:</span></span>
   
    1. <span data-ttu-id="dbe96-185">StorSimple 서비스 요약 블레이드의 **공유** 설정에서 오프라인으로 전환하려는 공유가 상주하는 가상 배열을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-185">From the **Shares** setting on the StorSimple service summary blade, select the virtual array on which the share you wish you to take offline resides.</span></span>

    2. <span data-ttu-id="dbe96-186">공유를 **선택**하고 **...**(또는 이 행의 오른쪽)를 클릭하고 상황에 맞는 메뉴에서 **오프라인으로 전환**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-186">**Select** the share and Click **...** (alternately right-click in this row) and from the context menu, select **Take offline**.</span></span>
     
        ![오프라인 공유](./media/storsimple-virtual-array-manage-shares/shares-offline.png)

    3. <span data-ttu-id="dbe96-188">**오프라인** 블레이드에서 정보를 검토하고 작업에 대한 동의를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-188">Review the information in the **Take offline** blade and confirm your acceptance of the operation.</span></span> <span data-ttu-id="dbe96-189">**오프라인으로 전환**을 클릭하여 공유를 오프라인으로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-189">Click **Take offline** to take the share offline.</span></span> <span data-ttu-id="dbe96-190">진행 중인 작업의 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-190">You will see a notification of the operation in progress.</span></span>

    4. <span data-ttu-id="dbe96-191">공유가 성공적으로 오프라인으로 전환되었는지 확인하려면 **공유** 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-191">To confirm that the share was successfully taken offline, go to the **Shares** blade.</span></span> <span data-ttu-id="dbe96-192">공유의 상태가 오프라인으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-192">You should see the status of the share as offline.</span></span>

## <a name="delete-a-share"></a><span data-ttu-id="dbe96-193">공유 삭제</span><span class="sxs-lookup"><span data-stu-id="dbe96-193">Delete a share</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dbe96-194">오프라인 상태인 경우에만 공유를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-194">You can delete a share only if it is offline.</span></span>


<span data-ttu-id="dbe96-195">공유를 삭제하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-195">Complete the following steps to delete a share.</span></span>

#### <a name="to-delete-a-share"></a><span data-ttu-id="dbe96-196">공유를 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="dbe96-196">To delete a share</span></span>

1. <span data-ttu-id="dbe96-197">StorSimple 서비스 요약 블레이드의 **공유** 설정에서 삭제하려는 공유가 상주하는 가상 배열을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-197">From the **Shares** setting on the StorSimple service summary blade, select the virtual array on which the share you wish to delete resides.</span></span>
2. <span data-ttu-id="dbe96-198">공유를 **선택**하고 **...**(또는 이 행의 오른쪽)를 클릭하고 상황에 맞는 메뉴에서 **삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-198">**Select** the share and Click **...** (alternately right-click in this row) and from the context menu, select **Delete**.</span></span>
   
    ![공유 삭제](./media/storsimple-virtual-array-manage-shares/share-delete.png)
3. <span data-ttu-id="dbe96-200">삭제하려는 공유의 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-200">Check the status of the share you want to delete.</span></span> <span data-ttu-id="dbe96-201">삭제하려는 공유가 오프라인 상태가 아니면 먼저 오프라인으로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-201">If the share you want to delete is not offline, take it offline first.</span></span> <span data-ttu-id="dbe96-202">[오프라인으로 공유 전환](#take-a-share-offline) 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-202">Follow the steps in [Take a share offline](#take-a-share-offline).</span></span>
4. <span data-ttu-id="dbe96-203">**삭제** 블레이드에서 확인하라는 메시지가 나타나면 확인을 수락하고 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-203">When prompted for confirmation in the **Delete** blade, accept the confirmation and click **Delete**.</span></span> <span data-ttu-id="dbe96-204">이제 공유가 삭제되고 **공유** 블레이드가 가상 배열 내의 업데이트된 공유 목록을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-204">The share will now be deleted and the **Shares** blade shows the updated list of shares within the virtual array.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dbe96-205">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dbe96-205">Next steps</span></span>
<span data-ttu-id="dbe96-206">[StorSimple 공유를 복제](storsimple-virtual-array-clone.md)하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="dbe96-206">Learn how to [clone a StorSimple share](storsimple-virtual-array-clone.md).</span></span>

