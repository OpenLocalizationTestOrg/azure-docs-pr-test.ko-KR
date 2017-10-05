---
title: "StorSimple에서 액세스 제어 레코드 관리 | Microsoft Docs"
description: "ACR(액세스 제어 레코드)을 사용하여 어떤 호스트가 StorSimple 장치의 볼륨에 연결할 수 있는지 지정하는 방법에 대해 설명합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 2f1475d8-36a5-4cc4-84b9-adf8a310b60c
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: a87624b5706c1d9b8c2b9926e5580996a89ce984
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-access-control-records"></a><span data-ttu-id="52a8c-103">StorSimple 관리자 서비스를 사용하여 액세스 제어 레코드 관리</span><span class="sxs-lookup"><span data-stu-id="52a8c-103">Use the StorSimple Manager service to manage access control records</span></span>
## <a name="overview"></a><span data-ttu-id="52a8c-104">개요</span><span class="sxs-lookup"><span data-stu-id="52a8c-104">Overview</span></span>
<span data-ttu-id="52a8c-105">ACR(액세스 제어 레코드)을 사용하면 어떤 호스트가 StorSimple 장치의 볼륨에 연결할 수 있는지 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-105">Access control records (ACRs) allow you to specify which hosts can connect to a volume on the StorSimple device.</span></span> <span data-ttu-id="52a8c-106">ACR은 특정 볼륨으로 설정되며 호스트의 IQN(iSCSI 정규화된 이름)을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-106">ACRs are set to a specific volume and contain the iSCSI Qualified Names (IQNs) of the hosts.</span></span> <span data-ttu-id="52a8c-107">호스트가 볼륨에 연결하려고 할 때 해당 장치는 IQN 이름에 대한 볼륨과 연결된 ACR을 확인하고 일치하는 경우 이 연결이 확정됩니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-107">When a host tries to connect to a volume, the device checks the ACR associated with that volume for the IQN name and if there is a match, then the connection is established.</span></span> <span data-ttu-id="52a8c-108">**구성** 페이지의 액세스 제어 레코드를 섹션은 호스트의 해당 IQN으로 모든 액세스 제어 레코드를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-108">The access control records section on the **Configure** page displays all the access control records with the corresponding IQNs of the hosts.</span></span>

<span data-ttu-id="52a8c-109">이 자습서에서는 다음과 같은 일반적인 ACR 관련 작업을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-109">This tutorial explains the following common ACR-related tasks:</span></span>

* <span data-ttu-id="52a8c-110">액세스 제어 레코드 추가</span><span class="sxs-lookup"><span data-stu-id="52a8c-110">Add an access control record</span></span> 
* <span data-ttu-id="52a8c-111">액세스 제어 레코드 편집</span><span class="sxs-lookup"><span data-stu-id="52a8c-111">Edit an access control record</span></span> 
* <span data-ttu-id="52a8c-112">액세스 제어 레코드 삭제</span><span class="sxs-lookup"><span data-stu-id="52a8c-112">Delete an access control record</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="52a8c-113">볼륨에 ACR을 할당할 때 이 볼륨을 손상시킬 수 있으므로 하나 이상의 클러스터되지 않은 호스트에서 동시에 액세스하지 않은 볼륨에 주의를 기울여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-113">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span></span> 
> * <span data-ttu-id="52a8c-114">볼륨에서 ACR을 삭제할 때 삭제로 인해 읽기-쓰기 중단이 발생할 수 있기 때문에 해당 호스트가 볼륨에 액세스하지 않는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-114">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span></span>
> 
> 

## <a name="add-an-access-control-record"></a><span data-ttu-id="52a8c-115">액세스 제어 레코드 추가</span><span class="sxs-lookup"><span data-stu-id="52a8c-115">Add an access control record</span></span>
<span data-ttu-id="52a8c-116">StorSimple 관리자 서비스 **구성** 페이지를 사용하여 ACR을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-116">You use the StorSimple Manager service **Configure** page to add ACRs.</span></span> <span data-ttu-id="52a8c-117">일반적으로 하나의 볼륨으로 하나의 ACR을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-117">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="52a8c-118">ACR을 추가하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-118">Perform the following steps to add an ACR.</span></span>

#### <a name="to-add-an-access-control-record"></a><span data-ttu-id="52a8c-119">액세스 제어 레코드를 추가하려</span><span class="sxs-lookup"><span data-stu-id="52a8c-119">To add an access control record</span></span>
1. <span data-ttu-id="52a8c-120">서비스 방문 페이지에서 서비스를 선택하고 서비스 이름을 두 번 클릭한 다음 **구성** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-120">On the service landing page, select your service, double-click the service name, and then click the **Configure** tab.</span></span>
2. <span data-ttu-id="52a8c-121">**액세스 제어 레코드** 아래 테이블 형식 목록에서 ACR에 대한 **이름**을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-121">In the tabular listing under **Access control records**, supply a **Name** for your ACR.</span></span>
3. <span data-ttu-id="52a8c-122">**iSCSI 초기자 이름**에서 Windows 호스트의 IQN 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-122">Provide the IQN name of your Windows host under **iSCSI Initiator Name**.</span></span> <span data-ttu-id="52a8c-123">Windows Server 호스트의 IQN을 가져오려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-123">To get the IQN of your Windows Server host, do the following:</span></span>
   
   * <span data-ttu-id="52a8c-124">Windows 호스트에서 Microsoft iSCSI 초기자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-124">Start the Microsoft iSCSI initiator on your Windows host.</span></span>
   * <span data-ttu-id="52a8c-125">**iSCSI 초기자 속성** 창의 **구성** 탭에서 **초기자 이름** 필드의 문자열을 선택하고 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-125">In the **iSCSI Initiator Properties** window, on the **Configuration** tab, select and copy the string from the **Initiator Name** field.</span></span>
   * <span data-ttu-id="52a8c-126">Azure 클래식 포털에 있는 ACR 표의 **iSCSI 초기자 이름** 필드에 이 문자열을 붙입니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-126">Paste this string in the **iSCSI Initiator Name** field on the ACRs table in the Azure classic portal.</span></span>
4. <span data-ttu-id="52a8c-127">**저장** 을 클릭하여 새로 만들어진 ACR을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-127">Click **Save** to save the newly created ACR.</span></span> <span data-ttu-id="52a8c-128">테이블 형식 목록이 이 추가 사항을 반영하도록 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-128">The tabular listing will be updated to reflect this addition.</span></span>

## <a name="edit-an-access-control-record"></a><span data-ttu-id="52a8c-129">액세스 제어 레코드 편집</span><span class="sxs-lookup"><span data-stu-id="52a8c-129">Edit an access control record</span></span>
<span data-ttu-id="52a8c-130">Azure 클래식 포털의 **구성** 페이지에서 ACR을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-130">You use the **Configure** page in the Azure classic portal to edit ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="52a8c-131">현재 사용하지 않고 있는 ACR만 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-131">You can modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="52a8c-132">현재 사용 중인 볼륨과 연관된 ACR을 편집하려면 먼저 볼륨을 오프라인으로 전환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-132">To edit an ACR associated with a volume that is currently in use, you must first take the volume offline.</span></span>
> 
> 

<span data-ttu-id="52a8c-133">ACR을 편집하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-133">Perform the following steps to edit an ACR.</span></span>

#### <a name="to-edit-an-access-control-record"></a><span data-ttu-id="52a8c-134">액세스 제어 레코드를 편집하려면</span><span class="sxs-lookup"><span data-stu-id="52a8c-134">To edit an access control record</span></span>
1. <span data-ttu-id="52a8c-135">서비스 방문 페이지에서 서비스를 선택하고 서비스 이름을 두 번 클릭한 다음 **구성** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-135">On the service landing page, select your service, double-click the service name, and then click the **Configure** tab.</span></span>
2. <span data-ttu-id="52a8c-136">액세스 제어 레코드의 테이블 형식 목록에서 수정하려는 ACR 위로 커서를 가져갑니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-136">In the tabular listing of the access control records, hover over the ACR that you wish to modify.</span></span>
3. <span data-ttu-id="52a8c-137">ACR의 새 이름 및/또는 IQN을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-137">Supply a new name and/or IQN for the ACR.</span></span>
4. <span data-ttu-id="52a8c-138">**저장** 을 클릭하여 수정된 ACR을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-138">Click **Save** to save the modified ACR.</span></span> <span data-ttu-id="52a8c-139">테이블 형식 목록이 이 변경 내용을 반영하도록 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-139">The tabular listing will be updated to reflect this change.</span></span>

## <a name="delete-an-access-control-record"></a><span data-ttu-id="52a8c-140">액세스 제어 레코드 삭제</span><span class="sxs-lookup"><span data-stu-id="52a8c-140">Delete an access control record</span></span>
<span data-ttu-id="52a8c-141">Azure 클래식 포털의 **구성** 페이지에서 ACR을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-141">You use the **Configure** page in the Azure classic portal to delete ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="52a8c-142">현재 사용하지 않고 있는 ACR만 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-142">You can delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="52a8c-143">현재 사용 중인 볼륨과 연관된 ACR을 삭제하려면 먼저 볼륨을 오프라인으로 전환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-143">To delete an ACR associated with a volume that is currently in use, you must first take the volume offline.</span></span>
> 
> 

<span data-ttu-id="52a8c-144">액세스 제어 레코드를 삭제하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-144">Perform the following steps to delete an access control record.</span></span>

#### <a name="to-delete-an-access-control-record"></a><span data-ttu-id="52a8c-145">액세스 제어 레코드를 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="52a8c-145">To delete an access control record</span></span>
1. <span data-ttu-id="52a8c-146">서비스 방문 페이지에서 서비스를 선택하고 서비스 이름을 두 번 클릭한 다음 **구성** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-146">On the service landing page, select your service, double-click the service name, and then click the **Configure** tab.</span></span>
2. <span data-ttu-id="52a8c-147">ACR(액세스 제어 레코드)의 테이블 형식 목록에서 삭제하려는 ACR 위로 커서를 가져갑니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-147">In the tabular listing of the access control records (ACRs), hover over the ACR that you wish to delete.</span></span>
3. <span data-ttu-id="52a8c-148">삭제 아이콘(**x**)이 선택한 ACR의 맨 오른쪽 열에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-148">A delete icon (**x**) will appear in the extreme right column for the ACR that you select.</span></span> <span data-ttu-id="52a8c-149">**x** 아이콘을 클릭하여 ACR을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-149">Click the **x** icon to delete the ACR.</span></span>
4. <span data-ttu-id="52a8c-150">확인 메시지가 나타나면 **예** 를 클릭하여 삭제를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-150">When prompted for confirmation, click **YES** to continue with the deletion.</span></span> <span data-ttu-id="52a8c-151">테이블 형식 목록이 삭제를 반영하도록 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-151">The tabular listing will be updated to reflect the deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="52a8c-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="52a8c-152">Next steps</span></span>
* <span data-ttu-id="52a8c-153">[StorSimple 볼륨 관리](storsimple-manage-volumes.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-153">Learn more about [managing StorSimple volumes](storsimple-manage-volumes.md).</span></span>
* <span data-ttu-id="52a8c-154">[StorSimple Manager 서비스를 사용하여 StorSimple 장치를 관리](storsimple-manager-service-administration.md)하는 방법을 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="52a8c-154">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

