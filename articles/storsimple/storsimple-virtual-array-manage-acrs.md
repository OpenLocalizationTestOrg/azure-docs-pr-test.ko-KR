---
title: "StorSimple Virtual Array에 대한 액세스 제어 레코드 관리 | Microsoft Docs"
description: "ACR(액세스 제어 레코드)을 관리하여 어떤 호스트가 StorSimple 가상 배열의 볼륨에 연결할 수 있는지 지정하는 방법에 대해 설명합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: e154bb4f-faab-4d92-a593-900c3ddc9595
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2ce65aa4efba735305208f7a6d761bc2814d1b8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-device-manager-to-manage-access-control-records-for-storsimple-virtual-array"></a><span data-ttu-id="5c51c-103">StorSimple 장치 관리자를 사용하여 StorSimple 가상 배열에 대한 액세스 제어 레코드 관리</span><span class="sxs-lookup"><span data-stu-id="5c51c-103">Use StorSimple Device Manager to manage access control records for StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="5c51c-104">개요</span><span class="sxs-lookup"><span data-stu-id="5c51c-104">Overview</span></span>

<span data-ttu-id="5c51c-105">ACR(액세스 제어 레코드)을 사용하면 어떤 호스트가 StorSimple 가상 배열(StorSimple 온-프레미스 가상 장치라고도 함)장치의 볼륨에 연결할 수 있는지 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-105">Access control records (ACRs) allow you to specify which hosts can connect to a volume on the StorSimple Virtual Array (also known as the StorSimple on-premises virtual device).</span></span> <span data-ttu-id="5c51c-106">ACR은 특정 볼륨으로 설정되며 호스트의 IQN(iSCSI 정규화된 이름)을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-106">ACRs are set to a specific volume and contain the iSCSI Qualified Names (IQNs) of the hosts.</span></span> <span data-ttu-id="5c51c-107">호스트가 볼륨에 연결하려고 할 때 해당 장치는 IQN 이름에 대한 볼륨과 연결된 ACR을 확인하고 일치하는 경우 이 연결이 확정됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-107">When a host tries to connect to a volume, the device checks the ACR associated with that volume for the IQN name, and if there is a match, then the connection is established.</span></span> <span data-ttu-id="5c51c-108">장치 관리자 서비스의 **구성** 섹션 내에 있는 **액세스 제어 레코드** 블레이드는 호스트의 해당 IQN으로 모든 액세스 제어 레코드를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-108">The **Access control records** blade within the **Configuration** section of your Device Manager service displays all the access control records with the corresponding IQNs of the hosts.</span></span>

![액세스 제어 레코드 관리](./media/storsimple-virtual-array-manage-acrs/ova-manage-acrs.png)

<span data-ttu-id="5c51c-110">이 자습서에서는 다음과 같은 일반적인 ACR 관련 작업을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-110">This tutorial explains the following common ACR-related tasks:</span></span>

* <span data-ttu-id="5c51c-111">IQN 가져오기</span><span class="sxs-lookup"><span data-stu-id="5c51c-111">Get the IQN</span></span>
* <span data-ttu-id="5c51c-112">액세스 제어 레코드 추가</span><span class="sxs-lookup"><span data-stu-id="5c51c-112">Add an access control record</span></span>
* <span data-ttu-id="5c51c-113">액세스 제어 레코드 편집</span><span class="sxs-lookup"><span data-stu-id="5c51c-113">Edit an access control record</span></span>
* <span data-ttu-id="5c51c-114">액세스 제어 레코드 삭제</span><span class="sxs-lookup"><span data-stu-id="5c51c-114">Delete an access control record</span></span>

> [!IMPORTANT]
> 
> * <span data-ttu-id="5c51c-115">볼륨에 ACR을 할당할 때 이 볼륨을 손상시킬 수 있으므로 하나 이상의 클러스터되지 않은 호스트에서 동시에 액세스하지 않은 볼륨에 주의를 기울여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-115">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span></span>
> * <span data-ttu-id="5c51c-116">볼륨에서 ACR을 삭제할 때 삭제로 인해 읽기-쓰기 중단이 발생할 수 있기 때문에 해당 호스트가 볼륨에 액세스하지 않는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-116">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span></span>


## <a name="get-the-iqn"></a><span data-ttu-id="5c51c-117">IQN 가져오기</span><span class="sxs-lookup"><span data-stu-id="5c51c-117">Get the IQN</span></span>

<span data-ttu-id="5c51c-118">Windows Server 2012를 실행하는 Windows 호스트의 IQN을 가져오려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-118">Perform the following steps to get the IQN of a Windows host that is running Windows Server 2012.</span></span>

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]

## <a name="add-an-acr"></a><span data-ttu-id="5c51c-119">ACR 추가</span><span class="sxs-lookup"><span data-stu-id="5c51c-119">Add an ACR</span></span>

<span data-ttu-id="5c51c-120">StorSimple Device Manager 서비스의 **구성** 섹션 내에 있는 **액세스 제어 레코드** 블레이드를 사용하여 ACR을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-120">You use **Access control records** blade within the **Configuration** section of your StorSimple Device Manager service to add ACRs.</span></span> <span data-ttu-id="5c51c-121">일반적으로 볼륨 하나와 ACR 하나를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-121">Typically, you associate one ACR with one volume.</span></span>

<span data-ttu-id="5c51c-122">볼륨과 ACR을 연결하는 방법에 대한 정보는 [볼륨 추가](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-122">For information about associating an ACR with a volume, go to [add a volume](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5c51c-123">볼륨에 ACR을 할당할 때 이 볼륨을 손상시킬 수 있으므로 하나 이상의 클러스터되지 않은 호스트에서 동시에 액세스하지 않은 볼륨에 주의를 기울여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-123">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span></span>


<span data-ttu-id="5c51c-124">ACR을 추가하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-124">Perform the following steps to add an ACR.</span></span>

#### <a name="to-add-an-acr"></a><span data-ttu-id="5c51c-125">ACR을 추가하려면</span><span class="sxs-lookup"><span data-stu-id="5c51c-125">To add an ACR</span></span>

1. <span data-ttu-id="5c51c-126">서비스 방문 페이지에서 서비스를 선택하고 서비스 이름을 두 번 클릭한 다음 **구성** 섹션 내에서 **액세스 제어 레코드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-126">On the service landing page, select your service, double-click the service name, and then within the **Configuration** section, click **Access control records**.</span></span>
2. <span data-ttu-id="5c51c-127">**액세스 제어 레코드** 블레이드에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-127">In the **Access control records** blade, click **Add**.</span></span>
3. <span data-ttu-id="5c51c-128">**ACR 추가** 블레이드에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-128">In the **Add ACR** blade, do the following:</span></span>
   
    1. <span data-ttu-id="5c51c-129">ACR의 **이름** 을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-129">Supply a **Name** for your ACR.</span></span>
    
    2. <span data-ttu-id="5c51c-130">**iSCSI 초기자 이름**에서 Windows 호스트의 IQN 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-130">Under **iSCSI Initiator Name**, provide the IQN name of your Windows host.</span></span> <span data-ttu-id="5c51c-131">Windows Server 호스트의 IQN을 가져오려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-131">To get the IQN of your Windows Server host, do the following:</span></span>
   
    3. <span data-ttu-id="5c51c-132">Windows 호스트에서 Microsoft iSCSI 초기자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-132">Start the Microsoft iSCSI initiator on your Windows host.</span></span> <span data-ttu-id="5c51c-133">iSCSI 초기자 속성 창의 **구성** 탭에서 **초기자 이름** 필드의 문자열을 선택하고 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-133">In the iSCSI Initiator Properties window, on the **Configuration** tab, select and copy the string from the **Initiator Name** field.</span></span>
    <span data-ttu-id="5c51c-134">**ACR 추가** 블레이드의 **IQN** 필드에 이 문자열을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-134">Paste this string in the **IQN** field in the **Add ACR** blade.</span></span>
   
    6. <span data-ttu-id="5c51c-135">**추가**를 클릭하여 ACR을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-135">Click **Add** to add the ACR.</span></span>  
   
        ![액세스 제어 레코드 추가](./media/storsimple-virtual-array-manage-acrs/ova-add-acrs.png)
4. <span data-ttu-id="5c51c-137">테이블 형식 목록이 이 추가 사항을 반영하도록 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-137">The tabular listing is updated to reflect this addition.</span></span>

## <a name="edit-an-acr"></a><span data-ttu-id="5c51c-138">ACR 편집</span><span class="sxs-lookup"><span data-stu-id="5c51c-138">Edit an ACR</span></span>

<span data-ttu-id="5c51c-139">Azure Portal에서 장치 관리자 서비스의 **구성** 섹션 내에 있는 **액세스 제어 레코드** 블레이드를 사용하여 ACR을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-139">You use the **Access control records** blade within the **Configuration** section of your Device Manager service in the Azure portal to edit ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="5c51c-140">현재 사용 중인 ACR을 수정하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-140">You should not modify an ACR that is currently in use.</span></span> <span data-ttu-id="5c51c-141">현재 사용 중인 볼륨과 연관된 ACR을 편집하려면 먼저 볼륨을 오프라인으로 전환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-141">To edit an ACR associated with a volume that is currently in use, you should first take the volume offline.</span></span>


<span data-ttu-id="5c51c-142">ACR을 편집하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-142">Perform the following steps to edit an ACR.</span></span>

#### <a name="to-edit-an-acr"></a><span data-ttu-id="5c51c-143">ACR을 편집하려면</span><span class="sxs-lookup"><span data-stu-id="5c51c-143">To edit an ACR</span></span>

1. <span data-ttu-id="5c51c-144">서비스 방문 페이지에서 서비스를 선택하고 서비스 이름을 두 번 클릭한 다음 **구성** 섹션 내에서 **액세스 제어 레코드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-144">On the service landing page, select your service, double-click the service name, and then within the **Configuration** section, **Access control records**.</span></span>
2. <span data-ttu-id="5c51c-145">**액세스 제어 레코드** 블레이드에서 액세스 제어 레코드의 테이블 형식 목록에서 수정하려는 ACR을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-145">In the **Access control records** blade, from the tabular listing of the access control records, double-click the ACR that you wish to modify.</span></span>
3. <span data-ttu-id="5c51c-146">**액세스 제어 레코드 편집** 블레이드에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-146">In the **Edit access control records** blade, do the following:</span></span>
   
    1. <span data-ttu-id="5c51c-147">ACR에 IQN을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-147">Supply the IQN for the ACR.</span></span>
   
    2. <span data-ttu-id="5c51c-148">블레이드의 맨 위에서 **저장**을 클릭하여 수정된 ACR을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-148">Click **Save** at the top of the blade to save the modified ACR.</span></span> <span data-ttu-id="5c51c-149">다음과 같은 확인 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-149">You see the following confirmation message:</span></span>
   
        ![액세스 제어 레코드 편집](./media/storsimple-virtual-array-manage-acrs/ova-edit-acrs.png)

## <a name="delete-an-access-control-record"></a><span data-ttu-id="5c51c-151">액세스 제어 레코드 삭제</span><span class="sxs-lookup"><span data-stu-id="5c51c-151">Delete an access control record</span></span>

<span data-ttu-id="5c51c-152">Azure Portal에서 **구성** 페이지를 사용하여 ACR을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-152">You use the **Configuration** page in the Azure portal to delete ACRs.</span></span>

> [!NOTE]
> 
> * <span data-ttu-id="5c51c-153">현재 사용 중인 ACR을 삭제하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-153">You should not delete an ACR that is currently in use.</span></span> <span data-ttu-id="5c51c-154">현재 사용 중인 볼륨과 연관된 ACR을 삭제하려면 먼저 볼륨을 오프라인으로 전환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-154">To delete an ACR associated with a volume that is currently in use, you should first take the volume offline.</span></span>
> * <span data-ttu-id="5c51c-155">볼륨에서 ACR을 삭제할 때 삭제로 인해 읽기-쓰기 중단이 발생할 수 있기 때문에 해당 호스트가 볼륨에 액세스하지 않는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-155">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span></span>


<span data-ttu-id="5c51c-156">액세스 제어 레코드를 삭제하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-156">Perform the following steps to delete an access control record.</span></span>

#### <a name="to-delete-an-access-control-record"></a><span data-ttu-id="5c51c-157">액세스 제어 레코드를 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="5c51c-157">To delete an access control record</span></span>

1. <span data-ttu-id="5c51c-158">서비스 방문 페이지에서 서비스를 선택하고 서비스 이름을 두 번 클릭한 다음 **구성** 섹션 내에서 **액세스 제어 레코드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-158">On the service landing page, select your service, double-click the service name, and then within the **Configuration** section, **Access control records**.</span></span>

2. <span data-ttu-id="5c51c-159">**액세스 제어 레코드** 블레이드에서 액세스 제어 레코드의 테이블 형식 목록에서 삭제하려는 ACR을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-159">In the **Access control records** blade, from the tabular listing of the access control records, double-click the ACR that you wish to delete.</span></span>

3. <span data-ttu-id="5c51c-160">액세스 제어 레코드 편집 블레이드에서 **삭제**를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-160">In the Edit access control records blade, click **Delete**.</span></span>
   
    ![ACR 삭제](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs.png)

4. <span data-ttu-id="5c51c-162">확인 메시지가 나타나면 **삭제**를 클릭하여 삭제를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-162">When prompted for confirmation, click **Delete** to continue with the deletion.</span></span> <span data-ttu-id="5c51c-163">테이블 형식 목록이 삭제를 반영하도록 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-163">The tabular listing is updated to reflect the deletion.</span></span>
   
   ![경고 메시지](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs-warning.png)

## <a name="next-steps"></a><span data-ttu-id="5c51c-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5c51c-165">Next steps</span></span>

* <span data-ttu-id="5c51c-166">[볼륨 추가 및 ACR 구성](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5c51c-166">Learn more about [adding volumes and configuring ACRs](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span></span>

