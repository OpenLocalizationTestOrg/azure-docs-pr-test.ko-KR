---
title: "StorSimple 볼륨 관리 | Microsoft Docs"
description: "StorSimple 볼륨을 추가, 수정, 모니터링 및 삭제하는 방법 및 필요에 따라 이를 오프라인으로 전환하는 방법을 설명합니다."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: ccabd859-590c-4568-a81d-6ff38f125be3
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/11/2016
ms.author: v-sharos
ms.openlocfilehash: 31ed9dad8ba56a3746873b7b35e678e97743fbfe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-volumes"></a><span data-ttu-id="b225f-103">StorSimple 관리자 서비스를 사용하여 볼륨 관리</span><span class="sxs-lookup"><span data-stu-id="b225f-103">Use the StorSimple Manager service to manage volumes</span></span>
[!INCLUDE [storsimple-version-selector-manage-volumes](../../includes/storsimple-version-selector-manage-volumes.md)]

## <a name="overview"></a><span data-ttu-id="b225f-104">개요</span><span class="sxs-lookup"><span data-stu-id="b225f-104">Overview</span></span>
<span data-ttu-id="b225f-105">이 자습서는 StorSimple 관리자 서비스를 사용하여 StorSimple 장치 및 StorSimple 가상 장치에서 볼륨을 만들고 관리하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-105">This tutorial explains how to use the StorSimple Manager service to create and manage volumes on the StorSimple device and StorSimple virtual device.</span></span>

<span data-ttu-id="b225f-106">StorSimple 관리자 서비스는 단일 웹 인터페이스에서 StorSimple 솔루션을 관리하는 Azure 클래식 포털의 확장입니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-106">The StorSimple Manager service is an extension of the Azure classic portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="b225f-107">볼륨 관리뿐 아니라 StorSimple 관리자 서비스를 사용하여 StorSimple 서비스를 만들고 관리하며, 장치를 보고 관리하며, 경고를 보고, 백업 정책 및 백업 카탈로그를 보고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-107">In addition to managing volumes, you can use the StorSimple Manager service to create and manage StorSimple services, view and manage devices, view alerts, and view and manage backup policies and the backup catalog.</span></span>

> [!NOTE]
> <span data-ttu-id="b225f-108">Azure StorSimple은 씬 프로비저닝된 볼륨만 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-108">Azure StorSimple can create thinly provisioned volumes only.</span></span> <span data-ttu-id="b225f-109">Azure StorSimple 시스템에서 완전히 프로비전되거나 부분적으로 프로비전된 볼륨은 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-109">You cannot create fully provisioned or partially provisioned volumes on an Azure StorSimple system.</span></span>
> 
> <span data-ttu-id="b225f-110">씬 프로비저닝은 사용 가능한 저장소가 실제 리소스를 초과하는 것처럼 표시하는 가상화 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-110">Thin provisioning is a virtualization technology in which available storage appears to exceed physical resources.</span></span> <span data-ttu-id="b225f-111">충분한 저장소를 사전에 예약하는 대신 Azure StorSimple는 씬 프로비저닝을 사용하여 현재 요구 사항에 맞게 충분한 공간을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-111">Instead of reserving sufficient storage in advance, Azure StorSimple uses thin provisioning to allocate just enough space to meet current requirements.</span></span> <span data-ttu-id="b225f-112">클라우드 저장소의 탄력적인 특징은 Azure StorSimple가 변화하는 요구에 맞게 클라우드 저장소를 늘리거나 줄일 수 있으므로 이 방법을 용이하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-112">The elastic nature of cloud storage facilitates this approach because Azure StorSimple can increase or decrease cloud storage to meet changing demands.</span></span>
> 
> 

## <a name="the-volumes-page"></a><span data-ttu-id="b225f-113">볼륨 페이지</span><span class="sxs-lookup"><span data-stu-id="b225f-113">The Volumes page</span></span>
<span data-ttu-id="b225f-114">**볼륨** 페이지를 사용하여 초기자(서버)에 대해 Microsoft Azure StorSimple 장치에서 프로비전되는 저장소 볼륨을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-114">The **Volumes** page allows you to manage the storage volumes that are provisioned on the Microsoft Azure StorSimple device for your initiators (servers).</span></span> <span data-ttu-id="b225f-115">StorSimple 장치에 볼륨 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-115">It displays the list of volumes on your StorSimple device.</span></span>

 ![볼륨 페이지](./media/storsimple-manage-volumes/HCS_VolumesPage.png)

<span data-ttu-id="b225f-117">볼륨은 다음과 같은 특성으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-117">A volume consists of a series of attributes:</span></span>

* <span data-ttu-id="b225f-118">**이름** – 설명이 포함된 이름은 고유해야 하며 볼륨을 식별하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-118">**Name** – A descriptive name that must be unique and helps identify the volume.</span></span> <span data-ttu-id="b225f-119">이 이름은 특정 볼륨에 필터링하는 경우 모니터링 보고서에서도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-119">This name is also used in monitoring reports when you filter on a specific volume.</span></span>
* <span data-ttu-id="b225f-120">**상태** – 온라인 또는 오프라인 상태가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-120">**Status** – Can be online or offline.</span></span> <span data-ttu-id="b225f-121">오프라인인 경우 볼륨은 해당 볼륨을 사용하는 데 액세스가 허용된 초기자(서버)에 보이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-121">If a volume if offline, it is not visible to initiators (servers) that are allowed access to use the volume.</span></span>
* <span data-ttu-id="b225f-122">**용량** – 초기자(서버)가 감지할 수 있는 볼륨의 크기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-122">**Capacity** – Specifies how large the volume is, as perceived by the initiator (server).</span></span> <span data-ttu-id="b225f-123">용량은 초기자(서버)가 저장할 수 있는 데이터의 전체 크기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-123">Capacity specifies the total amount of data that can be stored by the initiator (server).</span></span> <span data-ttu-id="b225f-124">볼륨은 씬 프로 비전되며 데이터는 중복 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-124">Volumes are thinly provisioned, and data is deduplicated.</span></span> <span data-ttu-id="b225f-125">이는 장치가 구성된 볼륨 용량에 따라 클라우드에서 또는 내부적으로 실제 저장소 용량을 미리 할당하지 않는다는 뜻입니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-125">This implies that your device doesn’t pre-allocate physical storage capacity internally or on the cloud according to configured volume capacity.</span></span> <span data-ttu-id="b225f-126">볼륨 용량이 할당되고 필요에 따라 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-126">The volume capacity is allocated and consumed on demand.</span></span>
* <span data-ttu-id="b225f-127">**유형** - 볼륨 유형은 계층형 또는 보관(계층화된 하위 유형)이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-127">**Type** – The volume type can be tiered or archival (a sub-type of tiered)</span></span>
* <span data-ttu-id="b225f-128">**액세스** – 이 볼륨에 대한 액세스가 허용된 초기자(서버)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-128">**Access** – Specifies the initiators (servers) that are allowed access to this volume.</span></span> <span data-ttu-id="b225f-129">볼륨에 연결된 ACR(액세스 제어 레코드)의 구성원이 아닌 초기자는 해당 볼륨을 보지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-129">Initiators that are not members of access control record (ACR) that is associated with the volume will not see the volume.</span></span>
* <span data-ttu-id="b225f-130">**모니터링** – 볼륨을 모니터링 하는지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-130">**Monitoring** – Specifies whether or not a volume is being monitored.</span></span> <span data-ttu-id="b225f-131">볼륨이 만들어질 때 기본적으로 모니터링이 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-131">A volume will have monitoring enabled by default when it is created.</span></span> <span data-ttu-id="b225f-132">하지만 모니터링은 볼륨 클론에 대해서는 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-132">Monitoring will, however, be disabled for a volume clone.</span></span> <span data-ttu-id="b225f-133">볼륨에 대한 모니터링을 사용하려면 볼륨 모니터링의 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-133">To enable monitoring for a volume, follow the instructions in Monitor a volume.</span></span>

<span data-ttu-id="b225f-134">다음은 볼륨과 관련된 가장 일반적인 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-134">The most common tasks associated with a volume are:</span></span>

* <span data-ttu-id="b225f-135">볼륨 추가</span><span class="sxs-lookup"><span data-stu-id="b225f-135">Add a volume</span></span>
* <span data-ttu-id="b225f-136">볼륨 수정</span><span class="sxs-lookup"><span data-stu-id="b225f-136">Modify a volume</span></span>
* <span data-ttu-id="b225f-137">볼륨 삭제</span><span class="sxs-lookup"><span data-stu-id="b225f-137">Delete a volume</span></span>
* <span data-ttu-id="b225f-138">볼륨을 오프라인으로 전환</span><span class="sxs-lookup"><span data-stu-id="b225f-138">Take a volume offline</span></span>
* <span data-ttu-id="b225f-139">볼륨 모니터링</span><span class="sxs-lookup"><span data-stu-id="b225f-139">Monitor a volume</span></span>

## <a name="add-a-volume"></a><span data-ttu-id="b225f-140">볼륨 추가</span><span class="sxs-lookup"><span data-stu-id="b225f-140">Add a volume</span></span>
<span data-ttu-id="b225f-141">StorSimple 솔루션 배포 중 [볼륨을 만들었습니다](storsimple-deployment-walkthrough-u1.md#step-6-create-a-volume) .</span><span class="sxs-lookup"><span data-stu-id="b225f-141">You [created a volume](storsimple-deployment-walkthrough-u1.md#step-6-create-a-volume) during deployment of your StorSimple solution.</span></span> <span data-ttu-id="b225f-142">볼륨 추가는 과정이 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-142">Adding a volume is a similar procedure.</span></span>

### <a name="to-add-a-volume"></a><span data-ttu-id="b225f-143">볼륨을 추가하려면</span><span class="sxs-lookup"><span data-stu-id="b225f-143">To add a volume</span></span>
1. <span data-ttu-id="b225f-144">**장치** 페이지에서 장치를 선택하고 두 번 클릭한 다음 **볼륨 컨테이너** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-144">On the **Devices** page, select the device, double-click it, and then click the **Volume Containers** tab.</span></span>
2. <span data-ttu-id="b225f-145">볼륨 컨테이너를 선택하고 해당 행에 있는 화살표를 클릭하여 컨테이너에 연결된 볼륨에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-145">Select a volume container and click the arrow in the corresponding row to access the volumes associated with the container.</span></span>
3. <span data-ttu-id="b225f-146">페이지 맨 아래에 있는 **추가** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-146">Click **Add** at the bottom of the page.</span></span> <span data-ttu-id="b225f-147">볼륨 추가 마법사가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-147">The Add a volume wizard starts.</span></span>
   
     ![볼륨 추가 마법사 기본 설정](./media/storsimple-manage-volumes/AddVolume1.png)
4. <span data-ttu-id="b225f-149">볼륨 추가 마법사의 **기본 설정**에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-149">In the Add a volume wizard, under **Basic Settings**, do the following:</span></span>
   
   1. <span data-ttu-id="b225f-150">볼륨의 **이름** 을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-150">Supply a **Name** for your volume.</span></span>
   2. <span data-ttu-id="b225f-151">볼륨의 **프로비전된 용량** 을 GB 또는 TB로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-151">Specify the **Provisioned Capacity** for your volume in GB or TB.</span></span> <span data-ttu-id="b225f-152">용량은 실제 장치에 대해 1GB 및 64TB 사이여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-152">The capacity must be between 1 GB and 64 TB for a physical device.</span></span> <span data-ttu-id="b225f-153">StorSimple 가상 장치에 있는 볼륨에 대해 프로비전할 수 있는 최대 용량은 30TB입니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-153">The maximum capacity that can be provisioned for a volume on a StorSimple virtual device is 30 TB.</span></span>
   3. <span data-ttu-id="b225f-154">볼륨의 **사용 유형**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-154">Select the **Usage Type** for your volume.</span></span> <span data-ttu-id="b225f-155">보관 데이터에 계층화된 볼륨을 사용하는 경우 **자주 액세스하지 않는 아카이브 데이터에 이 볼륨 사용** 확인란을 선택하면 볼륨의 중복 제거 청크 크기가 512KB로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-155">If you are using the tiered volume for archival data, selecting the **Use this volume for less frequently accessed archival data** check box changes the deduplication chunk size for your volume to 512 KB.</span></span> <span data-ttu-id="b225f-156">이 옵션을 선택하지 않으면 해당 계층화된 볼륨에서 64KB의 청크 크기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-156">If you do not select this option, the corresponding tiered volume will use a chunk size of 64 KB.</span></span> <span data-ttu-id="b225f-157">중복 제거 청크 크기를 늘리면 장치에서 대용량 아카이브 데이터를 클라우드로 신속하게 전송할 수 있습니다. (계층화된 볼륨은 이전에 기본 볼륨이라고 했습니다.)</span><span class="sxs-lookup"><span data-stu-id="b225f-157">A larger deduplication chunk size allows the device to expedite the transfer of large archival data to the cloud.(Tiered volumes were formerly called primary volumes.)</span></span>
   4. <span data-ttu-id="b225f-158">화살표 아이콘 ![화살표 아이콘](./media/storsimple-manage-volumes/HCS_ArrowIcon.png)을 클릭하여 **추가 설정** 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-158">Click the arrow icon ![Arrow icon](./media/storsimple-manage-volumes/HCS_ArrowIcon.png)to go to the **Additional Settings** page.</span></span>
      
        ![볼륨 추가 마법사 추가 설정](./media/storsimple-manage-volumes/AddVolume2.png)
5. <span data-ttu-id="b225f-160">**추가 설정**에서 새 ACR(액세스 제어 레코드)을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-160">Under **Additional Settings**, add a new access control record (ACR):</span></span>
   
   1. <span data-ttu-id="b225f-161">드롭다운 목록에서 ACR(액세스 제어 레코드)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-161">Select an access control record (ACR) from the drop-down list.</span></span> <span data-ttu-id="b225f-162">또는 새 ACR을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-162">Alternatively, you can add a new ACR.</span></span> <span data-ttu-id="b225f-163">ACR은 호스트 IQN을 레코드에 나열된 항목과 비교하여 볼륨에 액세스할 수 있는 호스트를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-163">ACRs determine which hosts can access your volumes by matching the host IQN with that listed in the record.</span></span>
   2. <span data-ttu-id="b225f-164">**이 볼륨에 대해 기본 백업 사용** 확인란을 선택하여 기본 백업을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-164">We recommend that you enable a default backup by selecting the **Enable a default backup for this volume** check box.</span></span>
   3. <span data-ttu-id="b225f-165">확인 아이콘</span><span class="sxs-lookup"><span data-stu-id="b225f-165">Click the check icon</span></span> ![확인 아이콘](./media/storsimple-manage-volumes/HCS_CheckIcon.png) <span data-ttu-id="b225f-167">을 클릭하여 지정된 설정으로 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-167">to create the volume with the specified settings.</span></span>

<span data-ttu-id="b225f-168">이제 새 볼륨을 사용할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-168">Your new volume is now ready to use.</span></span>

## <a name="modify-a-volume"></a><span data-ttu-id="b225f-169">볼륨 수정</span><span class="sxs-lookup"><span data-stu-id="b225f-169">Modify a volume</span></span>
<span data-ttu-id="b225f-170">볼륨을 확장하거나 볼륨에 액세스하는 호스트를 변경할 경우 볼륨을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-170">Modify a volume when you need to expand it or change the hosts that access the volume.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="b225f-171">장치에서 볼륨 크기를 수정하는 경우 볼륨 크기를 호스트에서도 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-171">If you modify the volume size on the device, the volume size needs to be changed on the host as well.</span></span>
> * <span data-ttu-id="b225f-172">여기에 설명된 호스트 쪽 단계는 Windows Server 2012(2012R2)에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-172">The host-side steps described here are for Windows Server 2012 (2012R2).</span></span> <span data-ttu-id="b225f-173">Linux 또는 다른 호스트 운영 체제에 대한 절차는 이와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-173">Procedures for Linux or other host operating systems will be different.</span></span> <span data-ttu-id="b225f-174">다른 운영 체제를 실행하는 호스트의 볼륨을 수정하는 경우 해당 호스트 운영 체제 지침을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b225f-174">Refer to your host operating system instructions when modifying the volume on a host running another operating system.</span></span>
> 
> 

### <a name="to-modify-a-volume"></a><span data-ttu-id="b225f-175">볼륨을 수정하려면</span><span class="sxs-lookup"><span data-stu-id="b225f-175">To modify a volume</span></span>
1. <span data-ttu-id="b225f-176">**장치** 페이지에서 장치를 선택하고 두 번 클릭한 다음 **볼륨 컨테이너** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-176">On the **Devices** page, select the device, double-click it, and then click the **Volume Container** tab.</span></span> <span data-ttu-id="b225f-177">이 페이지는 장치와 연결된 모든 볼륨 컨테이너를 표 형식으로 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-177">This page lists in a tabular format all the volume containers that are associated with the device.</span></span>
2. <span data-ttu-id="b225f-178">볼륨 컨테이너를 선택하고 클릭하여 컨테이너 내의 모든 볼륨 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-178">Select a volume container and click it to display the list of all the volumes within the container.</span></span>
3. <span data-ttu-id="b225f-179">**볼륨** 페이지에서 볼륨을 선택하고 **수정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-179">On the **Volumes** page, select a volume and click **Modify**.</span></span>
4. <span data-ttu-id="b225f-180">볼륨 수정 마법사의 **기본 설정**에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-180">In the Modify volume wizard, under **Basic Settings**, you can do the following:</span></span>
   
   * <span data-ttu-id="b225f-181">**자주 액세스하지 않는 아카이브 데이터에 이 볼륨 사용** 확인란을 선택하고 볼륨의 중복 제거 청크 크기를 512KB로 변경하여 계층화된 볼륨을 아카이브 볼륨을 수정하려는 경우 **이름**과 **유형**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-181">Edit the **Name** and **Type** if you wish to modify a tiered volume to an archival volume by selecting the **Use this volume for less frequently accessed archival data** check box to change the deduplication chunk size for your volume to 512 KB.</span></span>
   * <span data-ttu-id="b225f-182">**프로비전된 용량**을 늘립니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-182">Increase the **Provisioned Capacity**.</span></span> <span data-ttu-id="b225f-183">**프로비전된 용량** 은 늘릴 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-183">The **Provisioned Capacity** can only be increased.</span></span> <span data-ttu-id="b225f-184">만든 후에는 볼륨을 축소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-184">You cannot shrink a volume after it is created.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="b225f-185">볼륨에 할당한 후에는 볼륨 컨테이너를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-185">You cannot change the volume container after it is assigned to a volume.</span></span>
     > 
     > 
5. <span data-ttu-id="b225f-186">**추가 설정**에서 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-186">Under **Additional Settings**, you can do the following:</span></span>
   
   * <span data-ttu-id="b225f-187">오프라인인 볼륨이 제공된 ACR을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-187">Modify the ACRs, provided that the volume is offline.</span></span> <span data-ttu-id="b225f-188">볼륨이 온라인 상태이면 먼저 오프라인 상태로 전환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-188">If the volume is online, you will need to take it offline first.</span></span> <span data-ttu-id="b225f-189">ACR을 수정하기 전에 [볼륨을 오프라인을 전환](#take-a-volume-offline) 에서 단계를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b225f-189">Refer to the steps in [Take a volume offline](#take-a-volume-offline) prior to modifying the ACR.</span></span>
   * <span data-ttu-id="b225f-190">볼륨을 오프라인으로 전환한 후 ACR 목록을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-190">Modify the list of ACRs after the volume is offline.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="b225f-191">볼륨에 대해 **이 볼륨에 대해 기본 백업 사용** 옵션을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-191">You cannot change the **Enable a default backup for this volume** option for the volume.</span></span>
     > 
     > 
6. <span data-ttu-id="b225f-192">확인 아이콘</span><span class="sxs-lookup"><span data-stu-id="b225f-192">Save your changes by clicking the check icon</span></span> ![check-icon](./media/storsimple-manage-volumes/HCS_CheckIcon.png)<span data-ttu-id="b225f-194">을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-194">.</span></span> <span data-ttu-id="b225f-195">Azure 클래식 포털은 업데이트 볼륨 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-195">The Azure classic portal will display an updating volume message.</span></span> <span data-ttu-id="b225f-196">볼륨이 성공적으로 업데이트되면 성공 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-196">It will display a success message when the volume has been successfully updated.</span></span>
7. <span data-ttu-id="b225f-197">볼륨을 확장하는 경우 Windows 호스트 컴퓨터에서 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-197">If you are expanding a volume, complete the following steps on your Windows host computer:</span></span>
   
   1. <span data-ttu-id="b225f-198">**컴퓨터 관리** ->**디스크 관리**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-198">Go to **Computer Management** ->**Disk Management**.</span></span>
   2. <span data-ttu-id="b225f-199">**디스크 관리**를 마우스 오른쪽 단추로 클릭하고 **디스크 다시 검사**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-199">Right-click **Disk Management** and select **Rescan Disks**.</span></span>
   3. <span data-ttu-id="b225f-200">디스크 목록에서 업데이트한 볼륨을 선택하고 마우스 오른쪽 단추를 클릭한 다음 **볼륨 확장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-200">In the list of disks, select the volume that you updated, right-click, and then select **Extend Volume**.</span></span> <span data-ttu-id="b225f-201">볼륨 확장 마법사가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-201">The Extend Volume wizard starts.</span></span> <span data-ttu-id="b225f-202">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-202">Click **Next**.</span></span>
   4. <span data-ttu-id="b225f-203">기본값을 적용하여 마법사를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-203">Complete the wizard, accepting the default values.</span></span> <span data-ttu-id="b225f-204">마법사가 완료되면 볼륨에 증가된 크기가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-204">After the wizard is finished, the volume should show the increased size.</span></span>

<span data-ttu-id="b225f-205">![동영상 사용 가능](./media/storsimple-manage-volumes/Video_icon.png) **동영상 사용 가능**</span><span class="sxs-lookup"><span data-stu-id="b225f-205">![Video available](./media/storsimple-manage-volumes/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="b225f-206">볼륨을 확장하는 방법을 보여 주는 동영상을 시청하려면 [여기](https://azure.microsoft.com/documentation/videos/expand-a-storsimple-volume/)를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="b225f-206">To watch a video that demonstrates how to expand a volume, click [here](https://azure.microsoft.com/documentation/videos/expand-a-storsimple-volume/).</span></span>

## <a name="take-a-volume-offline"></a><span data-ttu-id="b225f-207">볼륨을 오프라인으로 전환</span><span class="sxs-lookup"><span data-stu-id="b225f-207">Take a volume offline</span></span>
<span data-ttu-id="b225f-208">볼륨을 수정 또는 삭제하려는 경우 볼륨을 오프라인으로 전환해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-208">You may need to take a volume offline when you are planning to modify it or delete it.</span></span> <span data-ttu-id="b225f-209">볼륨이 오프라인 상태인 경우 읽기 전용 액세스를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-209">When a volume is offline, it is not available for read-write access.</span></span> <span data-ttu-id="b225f-210">장치에서뿐 아니라 호스트에서도 볼륨을 오프라인으로 전환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-210">You will need to take the volume offline on the host as well as on the device.</span></span> <span data-ttu-id="b225f-211">볼륨을 오프라인을 전환하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-211">Perform the following steps to take a volume offline.</span></span>

### <a name="to-take-a-volume-offline"></a><span data-ttu-id="b225f-212">볼륨을 오프라인으로 전환하려면</span><span class="sxs-lookup"><span data-stu-id="b225f-212">To take a volume offline</span></span>
1. <span data-ttu-id="b225f-213">오프라인으로 전환하기 전에 해당 볼륨을 사용 중이 아니어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-213">Make sure that the volume in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="b225f-214">먼저 호스트에서 볼륨을 오프라인으로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-214">Take the volume offline on the host first.</span></span> <span data-ttu-id="b225f-215">이렇게 하면 볼륨에서 데이터가 손상될 잠재적 위험이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-215">This eliminates any potential risk of data corruption on the volume.</span></span> <span data-ttu-id="b225f-216">특정 단계의 경우 호스트 운영 체제에 대한 지침을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b225f-216">For specific steps, refer to the instructions for your host operating system.</span></span>
3. <span data-ttu-id="b225f-217">호스트가 오프라인이 되면 다음 단계를 수행하여 장치의 볼륨을 오프라인으로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-217">After the host is offline, take the volume on the device offline by performing the following steps:</span></span>
   
   1. <span data-ttu-id="b225f-218">**장치** 페이지에서 장치를 선택하고 두 번 클릭한 다음 **볼륨 컨테이너** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-218">On the **Devices** page, select the device, double-click it, and then click the **Volume Containers** tab.</span></span> <span data-ttu-id="b225f-219">**볼륨 컨테이너** 탭은 장치와 연결된 모든 볼륨 컨테이너를 표 형식으로 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-219">The **Volume Containers** tab lists in a tabular format all the volume containers that are associated with the device.</span></span>
   2. <span data-ttu-id="b225f-220">볼륨 컨테이너를 선택하고 클릭하여 컨테이너 내의 모든 볼륨 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-220">Select a volume container and click it to display the list of all the volumes within the container.</span></span>
   3. <span data-ttu-id="b225f-221">볼륨을 선택하고 **오프라인으로 전환**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-221">Select a volume and click **Take offline**.</span></span>
   4. <span data-ttu-id="b225f-222">확인하라는 메시지가 표시되면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-222">When prompted for confirmation, click **Yes**.</span></span> <span data-ttu-id="b225f-223">이제 볼륨이 오프라인 상태로 전환됩니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-223">The volume should now be offline.</span></span>
      
      <span data-ttu-id="b225f-224">볼륨이 오프라인이 되면 **온라인 상태로 전환** 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-224">After a volume is offline, the **Bring Online** option becomes available.</span></span>

> [!NOTE]
> <span data-ttu-id="b225f-225">**오프라인으로 전환** 명령은 볼륨을 오프라인으로 전환하라는 요청을 장치에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-225">The **Take Offline** command sends a request to the device to take the volume offline.</span></span> <span data-ttu-id="b225f-226">호스트에서 여전히 해당 볼륨을 사용하는 경우 연결이 끊어지고 볼륨을 오프라인으로 전환이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-226">If hosts are still using the volume, this results in broken connections, but taking the volume offline will not fail.</span></span>
> 
> 

## <a name="delete-a-volume"></a><span data-ttu-id="b225f-227">볼륨 삭제</span><span class="sxs-lookup"><span data-stu-id="b225f-227">Delete a volume</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b225f-228">오프라인 상태인 경우에만 볼륨을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-228">You can delete a volume only if it is offline.</span></span>
> 
> 

<span data-ttu-id="b225f-229">볼륨을 삭제하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-229">Complete the following steps to delete a volume.</span></span>

### <a name="to-delete-a-volume"></a><span data-ttu-id="b225f-230">볼륨을 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="b225f-230">To delete a volume</span></span>
1. <span data-ttu-id="b225f-231">**장치** 페이지에서 장치를 선택하고 두 번 클릭한 다음 **볼륨 컨테이너** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-231">On the **Devices** page, select the device, double-click it, and then click the **Volume Containers** tab.</span></span>
2. <span data-ttu-id="b225f-232">삭제하려는 볼륨이 있는 볼륨 컨테이너를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-232">Select the volume container that has the volume you want to delete.</span></span> <span data-ttu-id="b225f-233">볼륨 컨테이너를 클릭하여 **볼륨** 페이지에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-233">Click the volume container to access the **Volumes** page.</span></span>
3. <span data-ttu-id="b225f-234">이 컨테이너와 연결된 모든 볼륨은 테이블 형식으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-234">All the volumes associated with this container are displayed in a tabular format.</span></span> <span data-ttu-id="b225f-235">삭제하려는 볼륨의 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-235">Check the status of the volume you want to delete.</span></span> <span data-ttu-id="b225f-236">삭제하려는 볼륨이 오프라인 상태가 아닌 경우 [볼륨을 오프라인으로 전환](#take-a-volume-offline)의 단계를 따라 먼저 오프라인 상태로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-236">If the volume you want to delete is not offline, take it offline first, following the steps in [Take a volume offline](#take-a-volume-offline).</span></span>
4. <span data-ttu-id="b225f-237">볼륨이 오프라인 상태가 되면 페이지 맨 아래에서 **삭제** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-237">After the volume is offline, click **Delete** at the bottom of the page.</span></span>
5. <span data-ttu-id="b225f-238">확인하라는 메시지가 표시되면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-238">When prompted for confirmation, click **Yes**.</span></span> <span data-ttu-id="b225f-239">이제 볼륨이 삭제되며 **볼륨** 페이지가 컨테이너 내의 업데이트된 볼륨 목록을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-239">The volume will now be deleted and the **Volumes** page will show the updated list of volumes within the container.</span></span>

## <a name="monitor-a-volume"></a><span data-ttu-id="b225f-240">볼륨 모니터링</span><span class="sxs-lookup"><span data-stu-id="b225f-240">Monitor a volume</span></span>
<span data-ttu-id="b225f-241">볼륨 모니터링을 사용하면 볼륨에 대한 I/O 관련 통계를 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-241">Volume monitoring allows you to collect I/O-related statistics for a volume.</span></span> <span data-ttu-id="b225f-242">사용자가 만드는 첫 32개의 볼륨에 대해 기본적으로 모니터링을 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-242">Monitoring is enabled by default for the first 32 volumes that you create.</span></span> <span data-ttu-id="b225f-243">추가 볼륨의 모니터링은 기본적으로 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-243">Monitoring of additional volumes is disabled by default.</span></span> <span data-ttu-id="b225f-244">복제된 볼륨의 모니터링도 기본적으로 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-244">Monitoring of cloned volumes is also disabled by default.</span></span>

<span data-ttu-id="b225f-245">볼륨 모니터링을 사용하도록 또는 사용하지 않도록 설정하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-245">Perform the following steps to enable or disable monitoring for a volume.</span></span>

### <a name="to-enable-or-disable-volume-monitoring"></a><span data-ttu-id="b225f-246">볼륨 모니터링을 사용 또는 사용하지 않도록 설정하려면</span><span class="sxs-lookup"><span data-stu-id="b225f-246">To enable or disable volume monitoring</span></span>
1. <span data-ttu-id="b225f-247">**장치** 페이지에서 장치를 선택하고 두 번 클릭한 다음 **볼륨 컨테이너** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-247">On the **Devices** page, select the device, double-click it, and then click the **Volume Containers** tab.</span></span>
2. <span data-ttu-id="b225f-248">볼륨이 있는 볼륨 컨테이너를 선택한 다음 볼륨 컨테이너를 클릭하여 **볼륨** 페이지에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-248">Select the volume container in which the volume resides, and then click the volume container to access the **Volumes** page.</span></span>
3. <span data-ttu-id="b225f-249">이 컨테이너와 연결된 모든 볼륨은 테이블 형식으로 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-249">All the volumes associated with this container are listed in the tabular display.</span></span> <span data-ttu-id="b225f-250">볼륨 또는 볼륨 클론을 클릭하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-250">Click and select the volume or volume clone.</span></span>
4. <span data-ttu-id="b225f-251">페이지 맨 아래에 있는 **수정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-251">At the bottom of the page, click **Modify**.</span></span>
5. <span data-ttu-id="b225f-252">볼륨 수정 마법사의 **기본 설정**에 있는 **모니터링** 드롭다운 목록에서 **사용** 또는 **사용 안 함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-252">In the Modify Volume wizard, under **Basic Settings**, select **Enable** or **Disable** from the **Monitoring** drop-down list.</span></span>
   
    ![볼륨 기본 설정 수정](./media/storsimple-manage-volumes/HCS_MonitorVolumeM.png)

## <a name="next-steps"></a><span data-ttu-id="b225f-254">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b225f-254">Next steps</span></span>
* <span data-ttu-id="b225f-255">[StorSimple 볼륨 복제](storsimple-clone-volume.md)방법에 대해 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-255">Learn how to [clone a StorSimple volume](storsimple-clone-volume.md).</span></span>
* <span data-ttu-id="b225f-256">[StorSimple Manager 서비스를 사용하여 StorSimple 장치를 관리](storsimple-manager-service-administration.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b225f-256">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

