---
title: "StorSimple에서 액세스 제어 레코드 관리 | Microsoft Docs"
description: "ACR(액세스 제어 레코드)을 사용하여 어떤 호스트가 StorSimple 장치의 볼륨에 연결할 수 있는지 지정하는 방법에 대해 설명합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: alkohli
ms.openlocfilehash: 9173e34f889ce1c082b20bb382cb6ca9a03dd797
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-access-control-records"></a><span data-ttu-id="6603e-103">StorSimple 관리자 서비스를 사용하여 액세스 제어 레코드 관리</span><span class="sxs-lookup"><span data-stu-id="6603e-103">Use the StorSimple Manager service to manage access control records</span></span>

## <a name="overview"></a><span data-ttu-id="6603e-104">개요</span><span class="sxs-lookup"><span data-stu-id="6603e-104">Overview</span></span>
<span data-ttu-id="6603e-105">ACR(액세스 제어 레코드)을 사용하면 어떤 호스트가 StorSimple 장치의 볼륨에 연결할 수 있는지 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-105">Access control records (ACRs) allow you to specify which hosts can connect to a volume on the StorSimple device.</span></span> <span data-ttu-id="6603e-106">ACR은 특정 볼륨으로 설정되며 호스트의 IQN(iSCSI 정규화된 이름)을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-106">ACRs are set to a specific volume and contain the iSCSI Qualified Names (IQNs) of the hosts.</span></span> <span data-ttu-id="6603e-107">호스트가 볼륨에 연결하려고 할 때 해당 장치는 IQN 이름에 대한 볼륨과 연결된 ACR을 확인하고 일치하는 경우 이 연결이 확정됩니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-107">When a host tries to connect to a volume, the device checks the ACR associated with that volume for the IQN name and if there is a match, then the connection is established.</span></span> <span data-ttu-id="6603e-108">StorSimple 장치 관리자 서비스 블레이드의 **구성** 섹션 내에 있는 액세스 제어 레코드는 호스트의 해당 IQN으로 모든 액세스 제어 레코드를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-108">The access control records in the **Configuration** section of your StorSimple Device Manager service blade display all the access control records with the corresponding IQNs of the hosts.</span></span>

<span data-ttu-id="6603e-109">이 자습서에서는 다음과 같은 일반적인 ACR 관련 작업을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-109">This tutorial explains the following common ACR-related tasks:</span></span>

* <span data-ttu-id="6603e-110">액세스 제어 레코드 추가</span><span class="sxs-lookup"><span data-stu-id="6603e-110">Add an access control record</span></span>
* <span data-ttu-id="6603e-111">액세스 제어 레코드 편집</span><span class="sxs-lookup"><span data-stu-id="6603e-111">Edit an access control record</span></span>
* <span data-ttu-id="6603e-112">액세스 제어 레코드 삭제</span><span class="sxs-lookup"><span data-stu-id="6603e-112">Delete an access control record</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="6603e-113">볼륨에 ACR을 할당할 때 이 볼륨을 손상시킬 수 있으므로 하나 이상의 클러스터되지 않은 호스트에서 동시에 액세스하지 않은 볼륨에 주의를 기울여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-113">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span></span>
> * <span data-ttu-id="6603e-114">볼륨에서 ACR을 삭제할 때 삭제로 인해 읽기-쓰기 중단이 발생할 수 있기 때문에 해당 호스트가 볼륨에 액세스하지 않는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-114">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span></span>

## <a name="get-the-iqn"></a><span data-ttu-id="6603e-115">IQN 가져오기</span><span class="sxs-lookup"><span data-stu-id="6603e-115">Get the IQN</span></span>

<span data-ttu-id="6603e-116">Windows Server 2012를 실행하는 Windows 호스트의 IQN을 가져오려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-116">Perform the following steps to get the IQN of a Windows host that is running Windows Server 2012.</span></span>

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]


## <a name="add-an-access-control-record"></a><span data-ttu-id="6603e-117">액세스 제어 레코드 추가</span><span class="sxs-lookup"><span data-stu-id="6603e-117">Add an access control record</span></span>
<span data-ttu-id="6603e-118">StorSimple 장치 관리자 서비스 블레이드의 **구성** 섹션을 사용하여 ACR을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-118">You use the **Configuration** section in the StorSimple Device Manager service blade to add ACRs.</span></span> <span data-ttu-id="6603e-119">일반적으로 하나의 볼륨으로 하나의 ACR을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-119">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="6603e-120">ACR을 추가하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-120">Perform the following steps to add an ACR.</span></span>

#### <a name="to-add-an-acr"></a><span data-ttu-id="6603e-121">ACR을 추가하려면</span><span class="sxs-lookup"><span data-stu-id="6603e-121">To add an ACR</span></span>

1. <span data-ttu-id="6603e-122">StorSimple 장치 관리자 서비스로 이동한 후 서비스 이름을 두 번 클릭하고 **구성** 섹션 내에서 **액세스 제어 레코드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-122">Go to your StorSimple Device Manager service, double-click the service name, and then within the **Configuration** section, click **Access control records**.</span></span>
2. <span data-ttu-id="6603e-123">**액세스 제어 레코드** 블레이드에서 **+ ACR 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-123">In the **Access control records** blade, click **+ Add ACR**.</span></span>

    ![ACR 추가 클릭](./media/storsimple-8000-manage-acrs/createacr1.png)

3. <span data-ttu-id="6603e-125">**ACR 추가** 블레이드에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-125">In the **Add ACR** blade, do the following steps:</span></span>

    1. <span data-ttu-id="6603e-126">ACR의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-126">Supply a name for your ACR.</span></span>
    
    2. <span data-ttu-id="6603e-127">**IQN(iSCSI 초기자 이름)**에서 Windows Server 호스트의 IQN 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-127">Provide the IQN name of your Windows Server host under **iSCSI Initiator Name (IQN)**.</span></span>

    3. <span data-ttu-id="6603e-128">**추가**를 클릭하여 ACR을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-128">Click **Add** to create the ACR.</span></span>

        ![ACR 추가 클릭](./media/storsimple-8000-manage-acrs/createacr2.png)

4.  <span data-ttu-id="6603e-130">새로 추가된 테이블 형식의 ACR 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-130">The newly added ACR will display in the tabular listing of ACRs.</span></span>

    ![ACR 추가 클릭](./media/storsimple-8000-manage-acrs/createacr5.png)


## <a name="edit-an-access-control-record"></a><span data-ttu-id="6603e-132">액세스 제어 레코드 편집</span><span class="sxs-lookup"><span data-stu-id="6603e-132">Edit an access control record</span></span>
<span data-ttu-id="6603e-133">StorSimple 장치 관리자 서비스 블레이드의 **구성** 섹션을 사용하여 ACR을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-133">You use the **Configuration** section in the StorSimple Device Manager service blade to edit ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="6603e-134">현재 사용하지 않고 있는 ACR만 수정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-134">It is recommended that you modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="6603e-135">현재 사용 중인 볼륨과 연관된 ACR을 편집하려면 먼저 볼륨을 오프라인으로 전환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-135">To edit an ACR associated with a volume that is currently in use, you must first take the volume offline.</span></span>

<span data-ttu-id="6603e-136">ACR을 편집하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-136">Perform the following steps to edit an ACR.</span></span>

#### <a name="to-edit-an-access-control-record"></a><span data-ttu-id="6603e-137">액세스 제어 레코드를 편집하려면</span><span class="sxs-lookup"><span data-stu-id="6603e-137">To edit an access control record</span></span>
1.  <span data-ttu-id="6603e-138">StorSimple 장치 관리자 서비스로 이동한 후 서비스 이름을 두 번 클릭하고 **구성** 섹션 내에서 **액세스 제어 레코드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-138">Go to your StorSimple Device Manager service, double-click the service name, and then within the **Configuration** section, click **Access control records**.</span></span>

    ![액세스 제어 레코드로 이동](./media/storsimple-8000-manage-acrs/createacr1.png)

2. <span data-ttu-id="6603e-140">액세스 제어 레코드의 테이블 형식 목록에서 수정하려는 ACR을 클릭하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-140">In the tabular listing of the access control records, click and select the ACR that you wish to modify.</span></span>

    ![액세스 제어 레코드 편집](./media/storsimple-8000-manage-acrs/editacr1.png)

3. <span data-ttu-id="6603e-142">**액세스 제어 레코드 편집** 블레이드에서 다른 호스트에 해당하는 다른 IQN을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-142">In the **Edit access control record** blade, provide a different IQN corresponding to another host.</span></span>

    ![액세스 제어 레코드 편집](./media/storsimple-8000-manage-acrs/editacr2.png)

4. <span data-ttu-id="6603e-144">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-144">Click **Save**.</span></span> <span data-ttu-id="6603e-145">확인하라는 메시지가 표시되면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-145">When prompted for confirmation, click **Yes**.</span></span> 

    ![액세스 제어 레코드 편집](./media/storsimple-8000-manage-acrs/editacr3.png)

5. <span data-ttu-id="6603e-147">ACR이 업데이트되면 알림이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-147">You are notified when the ACR is updated.</span></span> <span data-ttu-id="6603e-148">이러한 변경을 반영하도록 테이블 형식 목록도 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-148">The tabular listing also updates to reflect the change.</span></span>

   
## <a name="delete-an-access-control-record"></a><span data-ttu-id="6603e-149">액세스 제어 레코드 삭제</span><span class="sxs-lookup"><span data-stu-id="6603e-149">Delete an access control record</span></span>
<span data-ttu-id="6603e-150">StorSimple 장치 관리자 서비스 블레이드의 **구성** 섹션을 사용하여 ACR을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-150">You use the **Configuration** section in the StorSimple Device Manager service blade to delete ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="6603e-151">현재 사용하지 않고 있는 ACR만 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-151">You can delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="6603e-152">현재 사용 중인 볼륨과 연관된 ACR을 삭제하려면 먼저 볼륨을 오프라인으로 전환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-152">To delete an ACR associated with a volume that is currently in use, you must first take the volume offline.</span></span>

<span data-ttu-id="6603e-153">액세스 제어 레코드를 삭제하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-153">Perform the following steps to delete an access control record.</span></span>

#### <a name="to-delete-an-access-control-record"></a><span data-ttu-id="6603e-154">액세스 제어 레코드를 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="6603e-154">To delete an access control record</span></span>
1.  <span data-ttu-id="6603e-155">StorSimple 장치 관리자 서비스로 이동한 후 서비스 이름을 두 번 클릭하고 **구성** 섹션 내에서 **액세스 제어 레코드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-155">Go to your StorSimple Device Manager service, double-click the service name, and then within the **Configuration** section, click **Access control records**.</span></span>

    ![액세스 제어 레코드로 이동](./media/storsimple-8000-manage-acrs/createacr1.png)

2. <span data-ttu-id="6603e-157">액세스 제어 레코드의 테이블 형식 목록에서 삭제하려는 ACR을 클릭하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-157">In the tabular listing of the access control records, click and select the ACR that you wish to delete.</span></span>

    ![액세스 제어 레코드로 이동](./media/storsimple-8000-manage-acrs/deleteacr1.png)

3. <span data-ttu-id="6603e-159">마우스 오른쪽 단추를 클릭하여 상황에 맞는 메뉴를 호출하고 **삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-159">Right-click to invoke the context menu and select **Delete**.</span></span>

    ![액세스 제어 레코드로 이동](./media/storsimple-8000-manage-acrs/deleteacr2.png)

4. <span data-ttu-id="6603e-161">확인을 위한 메시지가 나타나면 정보를 검토하고 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-161">When prompted for confirmation, review the information and then click **Delete**.</span></span>

    ![액세스 제어 레코드로 이동](./media/storsimple-8000-manage-acrs/deleteacr3.png)

5. <span data-ttu-id="6603e-163">삭제가 완료되면 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-163">You are notified when the deletion completes.</span></span> <span data-ttu-id="6603e-164">테이블 형식 목록이 삭제를 반영하도록 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-164">The tabular listing is updated to reflect the deletion.</span></span>

    ![액세스 제어 레코드로 이동](./media/storsimple-8000-manage-acrs/deleteacr5.png)

## <a name="next-steps"></a><span data-ttu-id="6603e-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6603e-166">Next steps</span></span>
* <span data-ttu-id="6603e-167">[StorSimple 볼륨 관리](storsimple-8000-manage-volumes-u2.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-167">Learn more about [managing StorSimple volumes](storsimple-8000-manage-volumes-u2.md).</span></span>
* <span data-ttu-id="6603e-168">[StorSimple Manager 서비스를 사용하여 StorSimple 장치를 관리](storsimple-8000-manager-service-administration.md)하는 방법을 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6603e-168">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

