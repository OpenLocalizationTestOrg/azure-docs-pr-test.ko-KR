---
title: "StorSimple에 대 한 액세스 제어 레코드 aaaManage | Microsoft Docs"
description: "Toouse 액세스 제어 (Acr) toodetermine tooa 볼륨 hello StorSimple 장치에 연결할 수 있는 호스트를 기록 하는 방법을 설명 합니다."
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
ms.openlocfilehash: cf532206e2c0bc49da853663ba34ae993ec2981d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-access-control-records"></a><span data-ttu-id="a0e3d-103">Hello StorSimple 관리자 서비스 toomanage 액세스 제어 레코드를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="a0e3d-103">Use hello StorSimple Manager service toomanage access control records</span></span>

## <a name="overview"></a><span data-ttu-id="a0e3d-104">개요</span><span class="sxs-lookup"><span data-stu-id="a0e3d-104">Overview</span></span>
<span data-ttu-id="a0e3d-105">액세스 제어 레코드 (Acr) toospecify tooa 볼륨 hello StorSimple 장치에 연결할 수 있는 호스트를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-105">Access control records (ACRs) allow you toospecify which hosts can connect tooa volume on hello StorSimple device.</span></span> <span data-ttu-id="a0e3d-106">Acr tooa 특정 볼륨을 설정 하 고 hello iSCSI 포함 hello 호스트의 정규화 된 이름 (iqn이 포함).</span><span class="sxs-lookup"><span data-stu-id="a0e3d-106">ACRs are set tooa specific volume and contain hello iSCSI Qualified Names (IQNs) of hello hosts.</span></span> <span data-ttu-id="a0e3d-107">호스트 tooconnect tooa 볼륨 오류 값을 hello 장치 hello ACR 해당 볼륨에 연결 된 일치 하는 경우 hello 연결이 설정 되 고 hello IQN 이름을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-107">When a host tries tooconnect tooa volume, hello device checks hello ACR associated with that volume for hello IQN name and if there is a match, then hello connection is established.</span></span> <span data-ttu-id="a0e3d-108">hello에 대 한 액세스 제어 레코드 hello **구성** StorSimple 장치 관리자 서비스 블레이드의 섹션 hello 해당 hello 호스트의 iqn이 포함 된 모든 hello 액세스 제어 레코드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-108">hello access control records in hello **Configuration** section of your StorSimple Device Manager service blade display all hello access control records with hello corresponding IQNs of hello hosts.</span></span>

<span data-ttu-id="a0e3d-109">이 자습서에서는 일반적인 ACR 관련 작업을 수행 하는 hello를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-109">This tutorial explains hello following common ACR-related tasks:</span></span>

* <span data-ttu-id="a0e3d-110">액세스 제어 레코드 추가</span><span class="sxs-lookup"><span data-stu-id="a0e3d-110">Add an access control record</span></span>
* <span data-ttu-id="a0e3d-111">액세스 제어 레코드 편집</span><span class="sxs-lookup"><span data-stu-id="a0e3d-111">Edit an access control record</span></span>
* <span data-ttu-id="a0e3d-112">액세스 제어 레코드 삭제</span><span class="sxs-lookup"><span data-stu-id="a0e3d-112">Delete an access control record</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="a0e3d-113">ACR tooa 볼륨을 할당할 때 주의 해야이 hello 볼륨 손상 될 수 있으므로 hello 볼륨 하나 이상의 클러스터 되지 않은 호스트에서 동시에 액세스 하지 않은 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-113">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span>
> * <span data-ttu-id="a0e3d-114">볼륨에서 ACR을 삭제할 때는 해당 호스트에서 해당 hello 하지에 액세스 하는 hello 볼륨 hello 삭제 읽기-쓰기 중단이 발생할 수 있기 때문에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-114">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>

## <a name="get-hello-iqn"></a><span data-ttu-id="a0e3d-115">Hello IQN 가져오기</span><span class="sxs-lookup"><span data-stu-id="a0e3d-115">Get hello IQN</span></span>

<span data-ttu-id="a0e3d-116">Hello 단계 tooget hello Windows Server 2012를 실행 중인 Windows 호스트의 IQN을 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-116">Perform hello following steps tooget hello IQN of a Windows host that is running Windows Server 2012.</span></span>

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]


## <a name="add-an-access-control-record"></a><span data-ttu-id="a0e3d-117">액세스 제어 레코드 추가</span><span class="sxs-lookup"><span data-stu-id="a0e3d-117">Add an access control record</span></span>
<span data-ttu-id="a0e3d-118">Hello를 사용 하 여 **구성** hello StorSimple 장치 관리자 서비스 블레이드 tooadd Acr의에서 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-118">You use hello **Configuration** section in hello StorSimple Device Manager service blade tooadd ACRs.</span></span> <span data-ttu-id="a0e3d-119">일반적으로 하나의 볼륨으로 하나의 ACR을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-119">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="a0e3d-120">Hello 단계 tooadd ACR 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-120">Perform hello following steps tooadd an ACR.</span></span>

#### <a name="tooadd-an-acr"></a><span data-ttu-id="a0e3d-121">ACR tooadd</span><span class="sxs-lookup"><span data-stu-id="a0e3d-121">tooadd an ACR</span></span>

1. <span data-ttu-id="a0e3d-122">Tooyour StorSimple 장치 관리자 서비스를 이동, hello 서비스 이름 및 다음 hello 내에서 두 번 클릭 **구성** 섹션에서 클릭 **액세스 제어 레코드**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-122">Go tooyour StorSimple Device Manager service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>
2. <span data-ttu-id="a0e3d-123">Hello에 **액세스 제어 레코드** 블레이드에서 클릭 **ACR 추가 +**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-123">In hello **Access control records** blade, click **+ Add ACR**.</span></span>

    ![ACR 추가 클릭](./media/storsimple-8000-manage-acrs/createacr1.png)

3. <span data-ttu-id="a0e3d-125">Hello에 **ACR 추가** 블레이드에서 다음 단계 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-125">In hello **Add ACR** blade, do hello following steps:</span></span>

    1. <span data-ttu-id="a0e3d-126">ACR의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-126">Supply a name for your ACR.</span></span>
    
    2. <span data-ttu-id="a0e3d-127">Windows Server 호스트의 IQN 이름을 hello 제공 **iSCSI 초기자 이름 (IQN)**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-127">Provide hello IQN name of your Windows Server host under **iSCSI Initiator Name (IQN)**.</span></span>

    3. <span data-ttu-id="a0e3d-128">클릭 **추가** toocreate hello ACR 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-128">Click **Add** toocreate hello ACR.</span></span>

        ![ACR 추가 클릭](./media/storsimple-8000-manage-acrs/createacr2.png)

4.  <span data-ttu-id="a0e3d-130">hello는 ACR hello Acr의 테이블 형식 목록에 표시 됩니다 새로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-130">hello newly added ACR will display in hello tabular listing of ACRs.</span></span>

    ![ACR 추가 클릭](./media/storsimple-8000-manage-acrs/createacr5.png)


## <a name="edit-an-access-control-record"></a><span data-ttu-id="a0e3d-132">액세스 제어 레코드 편집</span><span class="sxs-lookup"><span data-stu-id="a0e3d-132">Edit an access control record</span></span>
<span data-ttu-id="a0e3d-133">Hello를 사용 하 여 **구성** hello StorSimple 장치 관리자 서비스 블레이드 tooedit Acr의에서 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-133">You use hello **Configuration** section in hello StorSimple Device Manager service blade tooedit ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="a0e3d-134">현재 사용하지 않고 있는 ACR만 수정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-134">It is recommended that you modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="a0e3d-135">현재 사용 중인 볼륨와 연결 된 ACR tooedit를 먼저 수행 해야 hello 볼륨 오프 라인으로.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-135">tooedit an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>

<span data-ttu-id="a0e3d-136">Hello 단계 tooedit ACR 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-136">Perform hello following steps tooedit an ACR.</span></span>

#### <a name="tooedit-an-access-control-record"></a><span data-ttu-id="a0e3d-137">tooedit 액세스 제어 레코드</span><span class="sxs-lookup"><span data-stu-id="a0e3d-137">tooedit an access control record</span></span>
1.  <span data-ttu-id="a0e3d-138">Tooyour StorSimple 장치 관리자 서비스를 이동, hello 서비스 이름 및 다음 hello 내에서 두 번 클릭 **구성** 섹션에서 클릭 **액세스 제어 레코드**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-138">Go tooyour StorSimple Device Manager service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>

    ![Tooaccess 기록 제어 이동](./media/storsimple-8000-manage-acrs/createacr1.png)

2. <span data-ttu-id="a0e3d-140">Hello 액세스 제어 레코드의 테이블 형식 목록 hello 클릭 하 고 hello toomodify 하려는 ACR을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-140">In hello tabular listing of hello access control records, click and select hello ACR that you wish toomodify.</span></span>

    ![액세스 제어 레코드 편집](./media/storsimple-8000-manage-acrs/editacr1.png)

3. <span data-ttu-id="a0e3d-142">Hello에 **액세스 제어 레코드 편집** 블레이드에서 다른 IQN 해당 tooanother 호스트를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-142">In hello **Edit access control record** blade, provide a different IQN corresponding tooanother host.</span></span>

    ![액세스 제어 레코드 편집](./media/storsimple-8000-manage-acrs/editacr2.png)

4. <span data-ttu-id="a0e3d-144">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-144">Click **Save**.</span></span> <span data-ttu-id="a0e3d-145">확인하라는 메시지가 표시되면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-145">When prompted for confirmation, click **Yes**.</span></span> 

    ![액세스 제어 레코드 편집](./media/storsimple-8000-manage-acrs/editacr3.png)

5. <span data-ttu-id="a0e3d-147">ACR hello 업데이트 될 때 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-147">You are notified when hello ACR is updated.</span></span> <span data-ttu-id="a0e3d-148">또한 테이블 형식 목록 hello tooreflect hello 변경을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-148">hello tabular listing also updates tooreflect hello change.</span></span>

   
## <a name="delete-an-access-control-record"></a><span data-ttu-id="a0e3d-149">액세스 제어 레코드 삭제</span><span class="sxs-lookup"><span data-stu-id="a0e3d-149">Delete an access control record</span></span>
<span data-ttu-id="a0e3d-150">Hello를 사용 하 여 **구성** hello StorSimple 장치 관리자 서비스 블레이드 toodelete Acr의에서 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-150">You use hello **Configuration** section in hello StorSimple Device Manager service blade toodelete ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="a0e3d-151">현재 사용하지 않고 있는 ACR만 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-151">You can delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="a0e3d-152">현재 사용 중인 볼륨와 연결 된 ACR toodelete를 먼저 수행 해야 hello 볼륨 오프 라인으로.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-152">toodelete an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>

<span data-ttu-id="a0e3d-153">Hello 단계 toodelete 액세스 제어 레코드를 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-153">Perform hello following steps toodelete an access control record.</span></span>

#### <a name="toodelete-an-access-control-record"></a><span data-ttu-id="a0e3d-154">toodelete 액세스 제어 레코드</span><span class="sxs-lookup"><span data-stu-id="a0e3d-154">toodelete an access control record</span></span>
1.  <span data-ttu-id="a0e3d-155">Tooyour StorSimple 장치 관리자 서비스를 이동, hello 서비스 이름 및 다음 hello 내에서 두 번 클릭 **구성** 섹션에서 클릭 **액세스 제어 레코드**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-155">Go tooyour StorSimple Device Manager service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>

    ![Tooaccess 기록 제어 이동](./media/storsimple-8000-manage-acrs/createacr1.png)

2. <span data-ttu-id="a0e3d-157">Hello 액세스 제어 레코드의 테이블 형식 목록 hello 클릭 하 고 hello toodelete 하려는 ACR을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-157">In hello tabular listing of hello access control records, click and select hello ACR that you wish toodelete.</span></span>

    ![Tooaccess 기록 제어 이동](./media/storsimple-8000-manage-acrs/deleteacr1.png)

3. <span data-ttu-id="a0e3d-159">Tooinvoke hello 상황에 맞는 메뉴를 마우스 오른쪽 단추로 클릭 하 고 선택 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-159">Right-click tooinvoke hello context menu and select **Delete**.</span></span>

    ![Tooaccess 기록 제어 이동](./media/storsimple-8000-manage-acrs/deleteacr2.png)

4. <span data-ttu-id="a0e3d-161">확인 메시지가 표시 되 면 hello 정보를 검토 한 다음 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-161">When prompted for confirmation, review hello information and then click **Delete**.</span></span>

    ![Tooaccess 기록 제어 이동](./media/storsimple-8000-manage-acrs/deleteacr3.png)

5. <span data-ttu-id="a0e3d-163">Hello 삭제 완료 될 때 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-163">You are notified when hello deletion completes.</span></span> <span data-ttu-id="a0e3d-164">hello 테이블 형식 목록에는 업데이트 된 tooreflect hello 삭제입니다.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-164">hello tabular listing is updated tooreflect hello deletion.</span></span>

    ![Tooaccess 기록 제어 이동](./media/storsimple-8000-manage-acrs/deleteacr5.png)

## <a name="next-steps"></a><span data-ttu-id="a0e3d-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a0e3d-166">Next steps</span></span>
* <span data-ttu-id="a0e3d-167">[StorSimple 볼륨 관리](storsimple-8000-manage-volumes-u2.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-167">Learn more about [managing StorSimple volumes](storsimple-8000-manage-volumes-u2.md).</span></span>
* <span data-ttu-id="a0e3d-168">에 대 한 자세한 내용은 [StorSimple 장치의 StorSimple Manager 서비스 tooadminister를 hello를 사용 하 여](storsimple-8000-manager-service-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a0e3d-168">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

