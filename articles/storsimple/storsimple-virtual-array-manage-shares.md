---
title: "aaaManage StorSimple 가상 배열 공유 | Microsoft Docs"
description: "Hello StorSimple 장치 관리자를 설명 하 고 설명 어떻게 toouse 것 StorSimple 가상 배열에서 toomanage 공유 합니다."
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
ms.openlocfilehash: 9b57d7ec7c0b7de5a22e1b816daa8852d0f32a48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-shares-on-hello-storsimple-virtual-array"></a><span data-ttu-id="67396-103">StorSimple 가상 배열 hello에 hello StorSimple 장치 관리자 서비스 toomanage 공유 사용</span><span class="sxs-lookup"><span data-stu-id="67396-103">Use hello StorSimple Device Manager service toomanage shares on hello StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="67396-104">개요</span><span class="sxs-lookup"><span data-stu-id="67396-104">Overview</span></span>

<span data-ttu-id="67396-105">이 자습서에서는 toouse StorSimple 장치 관리자 서비스 toocreate hello 하 및 StorSimple 가상 배열에서 공유를 관리 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="67396-105">This tutorial explains how toouse hello StorSimple Device Manager service toocreate and manage shares on your StorSimple Virtual Array.</span></span>

<span data-ttu-id="67396-106">hello StorSimple 장치 관리자 서비스는 hello 단일 웹 인터페이스에서 StorSimple 솔루션을 관리할 수 있는 Azure 포털의에서 확장입니다.</span><span class="sxs-lookup"><span data-stu-id="67396-106">hello StorSimple Device Manager service is an extension in hello Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="67396-107">또한 toomanaging 공유 및 볼륨에서 있습니다 수 StorSimple 장치 관리자 서비스 tooview hello를 사용 하 여 및 장치를 관리, 경고 보기, 백업 정책 관리 및 hello 백업 카탈로그를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="67396-107">In addition toomanaging shares and volumes, you can use hello StorSimple Device Manager service tooview and manage devices, view alerts, manage backup policies, and manage hello backup catalog.</span></span>

## <a name="share-types"></a><span data-ttu-id="67396-108">공유 유형</span><span class="sxs-lookup"><span data-stu-id="67396-108">Share Types</span></span>

<span data-ttu-id="67396-109">StorSimple 공유는 다음과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67396-109">StorSimple shares can be:</span></span>

* <span data-ttu-id="67396-110">**로컬로 고정**:이 공유에는 데이터가 항상 hello 배열에 유지 되 고 toohello 클라우드를 분산 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67396-110">**Locally pinned**: Data in these shares stays on hello array at all times and does not spill toohello cloud.</span></span>
* <span data-ttu-id="67396-111">**계층**:이 공유에 데이터 toohello 클라우드 spill 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67396-111">**Tiered**: Data in these shares can spill toohello cloud.</span></span> <span data-ttu-id="67396-112">계층화 된 공유를 만들 때 hello 공간의 약 10 %hello 로컬 계층에서 프로 비전 하 고 hello 공간을 90 %hello 클라우드 프로 비전 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67396-112">When you create a tiered share, approximately 10 % of hello space is provisioned on hello local tier and 90 % of hello space is provisioned in hello cloud.</span></span> <span data-ttu-id="67396-113">예를 들어 1TB 공유를 프로 비전, 100GB hello 로컬 공간에 있게 및 900GB hello 클라우드에서 사용할 수 있도록 하는 경우 데이터 계층이 때 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="67396-113">For example, if you provisioned a 1 TB share, 100 GB would reside in hello local space and 900 GB would be used in hello cloud when hello data tiers.</span></span> <span data-ttu-id="67396-114">이 차례로 hello 장치에서 모든 hello 로컬 공간이 소진 되 면 제공 해야 할 수 없습니다 계층화 된 공유 (필요 하기 때문에 hello 10 %hello 로컬에서 계층을 사용할 수 없습니다)을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="67396-114">This in turn implies that if you run out of all hello local space on hello device, you cannot provision a tiered share (because hello 10 % required on hello local tier will not be available).</span></span>

### <a name="provisioned-capacity"></a><span data-ttu-id="67396-115">프로비전된 용량</span><span class="sxs-lookup"><span data-stu-id="67396-115">Provisioned capacity</span></span>

<span data-ttu-id="67396-116">Toohello 다음 각 공유 종류에 대 한 프로 비전 된 최대 용량에 대 한 표를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="67396-116">Refer toohello following table for maximum provisioned capacity for each share type.</span></span>

| <span data-ttu-id="67396-117">**제한 식별자**</span><span class="sxs-lookup"><span data-stu-id="67396-117">**Limit identifier**</span></span> | <span data-ttu-id="67396-118">**제한**</span><span class="sxs-lookup"><span data-stu-id="67396-118">**Limit**</span></span> |
| --- | --- |
| <span data-ttu-id="67396-119">계층화 공유의 최소 크기</span><span class="sxs-lookup"><span data-stu-id="67396-119">Minimum size of a tiered share</span></span> |<span data-ttu-id="67396-120">500GB</span><span class="sxs-lookup"><span data-stu-id="67396-120">500 GB</span></span> |
| <span data-ttu-id="67396-121">계층화 공유의 최대 크기</span><span class="sxs-lookup"><span data-stu-id="67396-121">Maximum size of a tiered share</span></span> |<span data-ttu-id="67396-122">20TB</span><span class="sxs-lookup"><span data-stu-id="67396-122">20 TB</span></span> |
| <span data-ttu-id="67396-123">로컬로 고정된 공유의 최소 크기</span><span class="sxs-lookup"><span data-stu-id="67396-123">Minimum size of a locally pinned share</span></span> |<span data-ttu-id="67396-124">50GB</span><span class="sxs-lookup"><span data-stu-id="67396-124">50 GB</span></span> |
| <span data-ttu-id="67396-125">로컬로 고정된 공유의 최대 크기</span><span class="sxs-lookup"><span data-stu-id="67396-125">Maximum size of a locally pinned share</span></span> |<span data-ttu-id="67396-126">2TB</span><span class="sxs-lookup"><span data-stu-id="67396-126">2 TB</span></span> |

## <a name="hello-shares-blade"></a><span data-ttu-id="67396-127">hello 공유 블레이드</span><span class="sxs-lookup"><span data-stu-id="67396-127">hello Shares blade</span></span>

<span data-ttu-id="67396-128">hello **공유** StorSimple 서비스 요약 블레이드에서 메뉴를 지정 된 StorSimple 배열에 저장소 공유의 hello 목록을 표시 하 고 toomanage 있습니다 이러한.</span><span class="sxs-lookup"><span data-stu-id="67396-128">hello **Shares** menu on your StorSimple service summary blade displays hello list of storage shares on a given StorSimple array and allows you toomanage them.</span></span>

![공유 블레이드](./media/storsimple-virtual-array-manage-shares/shares-blade.png)

<span data-ttu-id="67396-130">공유는 다음과 같은 특성으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="67396-130">A share consists of a series of attributes:</span></span>

* <span data-ttu-id="67396-131">**공유 이름** –를 설명 하는 이름을 고유 해야 하며 hello 공유를 식별 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67396-131">**Share Name** – A descriptive name that must be unique and helps identify hello share.</span></span>
* <span data-ttu-id="67396-132">**상태** – 온라인 또는 오프라인 상태가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67396-132">**Status** – Can be online or offline.</span></span> <span data-ttu-id="67396-133">공유 오프 라인 상태 이면 hello 공유의 사용자가 됩니다 수 tooaccess 것입니다.</span><span class="sxs-lookup"><span data-stu-id="67396-133">If a share is offline, users of hello share will not be able tooaccess it.</span></span>
* <span data-ttu-id="67396-134">**형식** – hello 공유 인지를 나타내는 **계층화 됨** (기본 hello) 또는 **로컬로 고정**합니다.</span><span class="sxs-lookup"><span data-stu-id="67396-134">**Type** – Indicates whether hello share is **Tiered** (hello default) or **Locally pinned**.</span></span>
* <span data-ttu-id="67396-135">**용량** – hello 비교 toohello hello 공유에 저장할 수 있는 데이터의 총 금액으로 사용 되는 데이터 양을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="67396-135">**Capacity** – specifies hello amount of data used as compared toohello total amount of data that can be stored on hello share.</span></span>
* <span data-ttu-id="67396-136">**설명** – hello 공유에 설명 하는 데 도움이 되는 선택적 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="67396-136">**Description** – An optional setting that helps describe hello share.</span></span>
* <span data-ttu-id="67396-137">**사용 권한** -Windows 탐색기를 통해 관리할 수 있는 hello NTFS 권한 toohello 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="67396-137">**Permissions** - hello NTFS permissions toohello share that can be managed through Windows Explorer.</span></span>
* <span data-ttu-id="67396-138">**백업** – 경우의 hello StorSimple 가상 배열, 모든 공유는 자동으로 백업에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67396-138">**Backup** – In case of hello StorSimple Virtual Array, all shares are automatically enabled for backup.</span></span>

![공유 세부 정보](./media/storsimple-virtual-array-manage-shares/share-details.png)

<span data-ttu-id="67396-140">이 자습서 tooperform hello 작업 다음에 hello 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="67396-140">Use hello instructions in this tutorial tooperform hello following tasks:</span></span>

* <span data-ttu-id="67396-141">공유 추가</span><span class="sxs-lookup"><span data-stu-id="67396-141">Add a share</span></span>
* <span data-ttu-id="67396-142">공유 수정</span><span class="sxs-lookup"><span data-stu-id="67396-142">Modify a share</span></span>
* <span data-ttu-id="67396-143">오프라인으로 공유 전환</span><span class="sxs-lookup"><span data-stu-id="67396-143">Take a share offline</span></span>
* <span data-ttu-id="67396-144">공유 삭제</span><span class="sxs-lookup"><span data-stu-id="67396-144">Delete a share</span></span>

## <a name="add-a-share"></a><span data-ttu-id="67396-145">공유 추가</span><span class="sxs-lookup"><span data-stu-id="67396-145">Add a share</span></span>

1. <span data-ttu-id="67396-146">Hello StorSimple 서비스 요약 블레이드를에서 클릭 **+ 추가 공유** hello 명령 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="67396-146">From hello StorSimple service summary blade, click **+ Add share** from hello command bar.</span></span> <span data-ttu-id="67396-147">Hello를 열어서이 **추가 공유** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="67396-147">This opens up hello **Add share** blade.</span></span>

    ![공유 추가](./media/storsimple-virtual-array-manage-shares/add-share.png)

2. <span data-ttu-id="67396-149">Hello에 **추가 공유** 블레이드에서 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67396-149">In hello **Add share** blade, do hello following:</span></span>
   
    1. <span data-ttu-id="67396-150">Hello에 **공유 이름** 필드에서 해당 공유에 대 한 고유한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="67396-150">In hello **Share name** field, enter a unique name for your share.</span></span> <span data-ttu-id="67396-151">hello 이름에는 3 too127 문자를 포함 하는 문자열 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67396-151">hello name must be a string that contains 3 too127 characters.</span></span>

    2. <span data-ttu-id="67396-152">선택적 **설명** hello 공유에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="67396-152">An optional **Description** for hello share.</span></span> <span data-ttu-id="67396-153">hello 설명 hello 공유 소유자를 식별 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67396-153">hello description will help identify hello share owners.</span></span>

    3. <span data-ttu-id="67396-154">Hello에 **형식** 드롭다운 목록에서 지정 하는지 여부를 toocreate는 **계층화 됨** 또는 **로컬로 고정** 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="67396-154">In hello **Type** dropdown list, specify whether toocreate a **Tiered** or **Locally pinned** share.</span></span> <span data-ttu-id="67396-155">로컬 보증, 낮은 대기 시간 및 높은 성능이 필요한 워크로드의 경우 **로컬로 고정된 공유**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="67396-155">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned share**.</span></span> <span data-ttu-id="67396-156">다른 모든 데이터에 대해서는 **계층화된** 공유를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="67396-156">For all other data, select **Tiered** share.</span></span>

    4. <span data-ttu-id="67396-157">Hello에 **용량** 필드 hello hello 공유 크기를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="67396-157">In hello **Capacity** field, specify hello size of hello share.</span></span> <span data-ttu-id="67396-158">계층화된 공유는 500GB에서 20TB 사이여야 하고 로컬로 고정된 공유는 50GB에서 2TB 사이여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67396-158">A tiered share must be between 500 GB and 20 TB and a locally pinned share must be between 50 GB and 2 TB.</span></span>

    5. <span data-ttu-id="67396-159">Hello에 **기본 대 한 모든 권한을 설정할** 필드, hello 권한 toohello 사용자 또는이 공유에 액세스 하는 hello 그룹을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="67396-159">In hello **Set default full permissions to** field, assign hello permissions toohello user, or hello group that is accessing this share.</span></span> <span data-ttu-id="67396-160">Hello 사용자 또는 사용자 그룹에 hello의 hello 이름을 지정  _john@contoso.com_  형식입니다.</span><span class="sxs-lookup"><span data-stu-id="67396-160">Specify hello name of hello user or hello user group in _john@contoso.com_ format.</span></span> <span data-ttu-id="67396-161">사용 하는 사용자 그룹 (단일 사용자)가 아니라 tooallow admin 권한이 tooaccess 이러한 공유 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="67396-161">We recommend that you use a user group (instead of a single user) tooallow admin privileges tooaccess these shares.</span></span> <span data-ttu-id="67396-162">Hello 권한을 여기에 할당 한 후 파일 탐색기 toomodify를 이러한 사용 권한은 다음 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67396-162">After you have assigned hello permissions here, you can then use File Explorer toomodify these permissions.</span></span>
3. <span data-ttu-id="67396-163">공유 구성을 완료했다면 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="67396-163">When you've finished configuring your share, click **Create**.</span></span> <span data-ttu-id="67396-164">지정 된 hello로는 공유를 만들 수는 설정 하 고 알림이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67396-164">A share will be created with hello specified settings and you will see a notification.</span></span> <span data-ttu-id="67396-165">기본적으로 hello 공유에 대 한 백업 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67396-165">By default, backup will be enabled for hello share.</span></span>
4. <span data-ttu-id="67396-166">공유 hello tooconfirm를 만드는 방법, 이동 toohello **공유** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="67396-166">tooconfirm that hello share was successfully created, go toohello **Shares** blade.</span></span> <span data-ttu-id="67396-167">나열 된 공유 hello를 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67396-167">You should see hello share listed.</span></span>
   
    ![공유 만들기 성공](./media/storsimple-virtual-array-manage-shares/share-success.png)

## <a name="modify-a-share"></a><span data-ttu-id="67396-169">공유 수정</span><span class="sxs-lookup"><span data-stu-id="67396-169">Modify a share</span></span>

<span data-ttu-id="67396-170">Toochange hello에 대 한 설명 hello 공유 해야 하는 경우 공유를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="67396-170">Modify a share when you need toochange hello description of hello share.</span></span> <span data-ttu-id="67396-171">Hello 공유 만들어지면 없는 다른 공유 속성을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67396-171">No other share properties can be modified once hello share is created.</span></span>

#### <a name="toomodify-a-share"></a><span data-ttu-id="67396-172">toomodify 공유</span><span class="sxs-lookup"><span data-stu-id="67396-172">toomodify a share</span></span>

1. <span data-ttu-id="67396-173">Hello에서 **공유** hello StorSimple 서비스 요약 블레이드의 설정을 선택 hello는 hello 있습니다 toomodify 원하는 공유 상주 하는 가상 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="67396-173">From hello **Shares** setting on hello StorSimple service summary blade, select hello virtual array on which hello share you wish you toomodify resides.</span></span>
2. <span data-ttu-id="67396-174">**선택** 공유 tooview hello 현재 설명 hello을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="67396-174">**Select** hello share tooview hello current description and modify it.</span></span>
3. <span data-ttu-id="67396-175">Hello를 클릭 하 여 변경 내용을 저장 **저장** 명령 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="67396-175">Save your changes by clicking hello **Save** command bar.</span></span> <span data-ttu-id="67396-176">지정된 설정이 적용되고 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="67396-176">Your specified settings will be applied and you will see a notification.</span></span>
   
    ![ <span data-ttu-id="67396-177">공유 편집</span><span class="sxs-lookup"><span data-stu-id="67396-177">Edit share</span></span>](./media/storsimple-virtual-array-manage-shares/share-edit.png)

## <a name="take-a-share-offline"></a><span data-ttu-id="67396-178">오프라인으로 공유 전환</span><span class="sxs-lookup"><span data-stu-id="67396-178">Take a share offline</span></span>

<span data-ttu-id="67396-179">계획할 때 toomodify 하거나 삭제 tootake 공유를 오프 라인으로 작업을 할 수 있습니다 것입니다.</span><span class="sxs-lookup"><span data-stu-id="67396-179">You may need tootake a share offline when you are planning toomodify it or delete it.</span></span> <span data-ttu-id="67396-180">공유가 오프라인 상태인 경우 읽기 전용 액세스를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="67396-180">When a share is offline, it is not available for read-write access.</span></span> <span data-ttu-id="67396-181">Tootake hello 공유 오프 라인으로 hello 장치 뿐 아니라 hello 호스트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67396-181">You will need tootake hello share offline on hello host as well as on hello device.</span></span>

#### <a name="tootake-a-share-offline"></a><span data-ttu-id="67396-182">오프 라인으로 공유 tootake</span><span class="sxs-lookup"><span data-stu-id="67396-182">tootake a share offline</span></span>

1. <span data-ttu-id="67396-183">문제의 hello 공유 하는 오프 라인으로 전환 하기 전에 사용 하지 않는 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="67396-183">Make sure that hello share in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="67396-184">Hello 다음 단계를 수행 하 여 오프 라인으로 hello 배열에 hello 공유를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="67396-184">Take hello share on hello array offline by performing hello following steps:</span></span>
   
    1. <span data-ttu-id="67396-185">Hello에서 **공유** hello StorSimple 서비스 요약 블레이드의 설정을 선택 hello는 hello tootake 오프 하면 원하는 공유 상주 하는 가상 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="67396-185">From hello **Shares** setting on hello StorSimple service summary blade, select hello virtual array on which hello share you wish you tootake offline resides.</span></span>

    2. <span data-ttu-id="67396-186">**선택** hello 공유 및 클릭 **...**  (또는이 행의 오른쪽 클릭) hello 상황에 맞는 메뉴에서 선택 하 고 **오프 라인 상태로 만드는**합니다.</span><span class="sxs-lookup"><span data-stu-id="67396-186">**Select** hello share and Click **...** (alternately right-click in this row) and from hello context menu, select **Take offline**.</span></span>
     
        ![오프라인 공유](./media/storsimple-virtual-array-manage-shares/shares-offline.png)

    3. <span data-ttu-id="67396-188">Hello hello 정보를 검토 **오프 라인 상태로 만드는** 블레이드 hello 작업의 동의 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="67396-188">Review hello information in hello **Take offline** blade and confirm your acceptance of hello operation.</span></span> <span data-ttu-id="67396-189">클릭 **오프 라인 상태로 만드는** tootake hello 오프 라인으로 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="67396-189">Click **Take offline** tootake hello share offline.</span></span> <span data-ttu-id="67396-190">진행 중인 hello 작업의 알림이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67396-190">You will see a notification of hello operation in progress.</span></span>

    4. <span data-ttu-id="67396-191">공유 hello tooconfirm에서 오프 라인, 이동 toohello 성공적으로 수행한 **공유** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="67396-191">tooconfirm that hello share was successfully taken offline, go toohello **Shares** blade.</span></span> <span data-ttu-id="67396-192">Hello 상태의 hello 공유 오프 라인으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="67396-192">You should see hello status of hello share as offline.</span></span>

## <a name="delete-a-share"></a><span data-ttu-id="67396-193">공유 삭제</span><span class="sxs-lookup"><span data-stu-id="67396-193">Delete a share</span></span>

> [!IMPORTANT]
> <span data-ttu-id="67396-194">오프라인 상태인 경우에만 공유를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67396-194">You can delete a share only if it is offline.</span></span>


<span data-ttu-id="67396-195">다음 단계 toodelete 공유 hello를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="67396-195">Complete hello following steps toodelete a share.</span></span>

#### <a name="toodelete-a-share"></a><span data-ttu-id="67396-196">toodelete 공유</span><span class="sxs-lookup"><span data-stu-id="67396-196">toodelete a share</span></span>

1. <span data-ttu-id="67396-197">Hello에서 **공유** hello StorSimple 서비스 요약 블레이드의 설정을 선택 hello toodelete 있는 원하는 어떤 hello 공유에 가상 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="67396-197">From hello **Shares** setting on hello StorSimple service summary blade, select hello virtual array on which hello share you wish toodelete resides.</span></span>
2. <span data-ttu-id="67396-198">**선택** hello 공유 및 클릭 **...**  (또는이 행의 오른쪽 클릭) hello 상황에 맞는 메뉴에서 선택 하 고 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="67396-198">**Select** hello share and Click **...** (alternately right-click in this row) and from hello context menu, select **Delete**.</span></span>
   
    ![공유 삭제](./media/storsimple-virtual-array-manage-shares/share-delete.png)
3. <span data-ttu-id="67396-200">Hello 상태를 확인 하려는 toodelete hello 공유의 합니다.</span><span class="sxs-lookup"><span data-stu-id="67396-200">Check hello status of hello share you want toodelete.</span></span> <span data-ttu-id="67396-201">Toodelete hello 공유 오프 라인 이면 오프 라인 상태로 먼저 합니다.</span><span class="sxs-lookup"><span data-stu-id="67396-201">If hello share you want toodelete is not offline, take it offline first.</span></span> <span data-ttu-id="67396-202">Hello 단계에 따라 [오프 라인 상태로 공유](#take-a-share-offline)합니다.</span><span class="sxs-lookup"><span data-stu-id="67396-202">Follow hello steps in [Take a share offline](#take-a-share-offline).</span></span>
4. <span data-ttu-id="67396-203">Hello에 확인 메시지가 나타나면 **삭제** 블레이드에서 hello 확인을 적용 하 고 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="67396-203">When prompted for confirmation in hello **Delete** blade, accept hello confirmation and click **Delete**.</span></span> <span data-ttu-id="67396-204">hello 공유 이제 삭제 되 고 hello **공유** 블레이드 hello 가상 배열 내에서 공유 hello 업데이트 목록을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="67396-204">hello share will now be deleted and hello **Shares** blade shows hello updated list of shares within hello virtual array.</span></span>

## <a name="next-steps"></a><span data-ttu-id="67396-205">다음 단계</span><span class="sxs-lookup"><span data-stu-id="67396-205">Next steps</span></span>
<span data-ttu-id="67396-206">너무 방법에 대해 알아봅니다[StorSimple 공유를 복제할](storsimple-virtual-array-clone.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="67396-206">Learn how too[clone a StorSimple share](storsimple-virtual-array-clone.md).</span></span>

