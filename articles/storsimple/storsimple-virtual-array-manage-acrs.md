---
title: "StorSimple 가상 배열에 대 한 액세스 제어 레코드 aaaManage | Microsoft Docs"
description: "Toomanage 액세스 제어 (Acr) toodetermine tooa 볼륨 hello StorSimple 가상 배열에 연결할 수 있는 호스트를 기록 하는 방법을 설명 합니다."
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
ms.openlocfilehash: 608fdf72413761ce3c9c4bf297a748489c415685
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-access-control-records-for-storsimple-virtual-array"></a><span data-ttu-id="32cd8-103">StorSimple 가상 배열에 대 한 StorSimple 장치 관리자를 사용 하 여 toomanage 액세스 제어 레코드</span><span class="sxs-lookup"><span data-stu-id="32cd8-103">Use StorSimple Device Manager toomanage access control records for StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="32cd8-104">개요</span><span class="sxs-lookup"><span data-stu-id="32cd8-104">Overview</span></span>

<span data-ttu-id="32cd8-105">액세스 제어 레코드 (Acr) toospecify tooa 볼륨 hello StorSimple 가상 배열 (라고도 hello StorSimple 온-프레미스 가상 장치)에 연결할 수 있는 호스트를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-105">Access control records (ACRs) allow you toospecify which hosts can connect tooa volume on hello StorSimple Virtual Array (also known as hello StorSimple on-premises virtual device).</span></span> <span data-ttu-id="32cd8-106">Acr tooa 특정 볼륨을 설정 하 고 hello iSCSI 포함 hello 호스트의 정규화 된 이름 (iqn이 포함).</span><span class="sxs-lookup"><span data-stu-id="32cd8-106">ACRs are set tooa specific volume and contain hello iSCSI Qualified Names (IQNs) of hello hosts.</span></span> <span data-ttu-id="32cd8-107">호스트 오류 tooconnect tooa 볼륨 값을 hello 장치 hello 해당 볼륨 hello IQN 이름에 대 한 연결 된 ACR 확인 하 고 일치 하는 경우 hello 연결이 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-107">When a host tries tooconnect tooa volume, hello device checks hello ACR associated with that volume for hello IQN name, and if there is a match, then hello connection is established.</span></span> <span data-ttu-id="32cd8-108">hello **액세스 제어 레코드** hello 내 블레이드 **구성** 장치 관리자 서비스의 섹션 hello 해당 hello 호스트의 iqn이 포함 된 모든 hello 액세스 제어 레코드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-108">hello **Access control records** blade within hello **Configuration** section of your Device Manager service displays all hello access control records with hello corresponding IQNs of hello hosts.</span></span>

![액세스 제어 레코드 관리](./media/storsimple-virtual-array-manage-acrs/ova-manage-acrs.png)

<span data-ttu-id="32cd8-110">이 자습서에서는 일반적인 ACR 관련 작업을 수행 하는 hello를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-110">This tutorial explains hello following common ACR-related tasks:</span></span>

* <span data-ttu-id="32cd8-111">Hello IQN 가져오기</span><span class="sxs-lookup"><span data-stu-id="32cd8-111">Get hello IQN</span></span>
* <span data-ttu-id="32cd8-112">액세스 제어 레코드 추가</span><span class="sxs-lookup"><span data-stu-id="32cd8-112">Add an access control record</span></span>
* <span data-ttu-id="32cd8-113">액세스 제어 레코드 편집</span><span class="sxs-lookup"><span data-stu-id="32cd8-113">Edit an access control record</span></span>
* <span data-ttu-id="32cd8-114">액세스 제어 레코드 삭제</span><span class="sxs-lookup"><span data-stu-id="32cd8-114">Delete an access control record</span></span>

> [!IMPORTANT]
> 
> * <span data-ttu-id="32cd8-115">ACR tooa 볼륨을 할당할 때 주의 해야이 hello 볼륨 손상 될 수 있으므로 hello 볼륨 하나 이상의 클러스터 되지 않은 호스트에서 동시에 액세스 하지 않은 합니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-115">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span>
> * <span data-ttu-id="32cd8-116">볼륨에서 ACR을 삭제할 때는 해당 호스트에서 해당 hello 하지에 액세스 하는 hello 볼륨 hello 삭제 읽기-쓰기 중단이 발생할 수 있기 때문에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-116">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>


## <a name="get-hello-iqn"></a><span data-ttu-id="32cd8-117">Hello IQN 가져오기</span><span class="sxs-lookup"><span data-stu-id="32cd8-117">Get hello IQN</span></span>

<span data-ttu-id="32cd8-118">Hello 단계 tooget hello Windows Server 2012를 실행 중인 Windows 호스트의 IQN을 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-118">Perform hello following steps tooget hello IQN of a Windows host that is running Windows Server 2012.</span></span>

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]

## <a name="add-an-acr"></a><span data-ttu-id="32cd8-119">ACR 추가</span><span class="sxs-lookup"><span data-stu-id="32cd8-119">Add an ACR</span></span>

<span data-ttu-id="32cd8-120">사용 하면 **액세스 제어 레코드** hello 내 블레이드 **구성** StorSimple 장치 관리자 서비스 tooadd Acr의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-120">You use **Access control records** blade within hello **Configuration** section of your StorSimple Device Manager service tooadd ACRs.</span></span> <span data-ttu-id="32cd8-121">일반적으로 볼륨 하나와 ACR 하나를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-121">Typically, you associate one ACR with one volume.</span></span>

<span data-ttu-id="32cd8-122">볼륨에 ACR을 연결 하는 방법에 대 한 내용은 이동 너무[볼륨 추가](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume)합니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-122">For information about associating an ACR with a volume, go too[add a volume](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="32cd8-123">ACR tooa 볼륨을 할당할 때 주의 해야이 hello 볼륨 손상 될 수 있으므로 hello 볼륨 하나 이상의 클러스터 되지 않은 호스트에서 동시에 액세스 하지 않은 합니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-123">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span>


<span data-ttu-id="32cd8-124">Hello 단계 tooadd ACR 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-124">Perform hello following steps tooadd an ACR.</span></span>

#### <a name="tooadd-an-acr"></a><span data-ttu-id="32cd8-125">ACR tooadd</span><span class="sxs-lookup"><span data-stu-id="32cd8-125">tooadd an ACR</span></span>

1. <span data-ttu-id="32cd8-126">Hello 서비스 방문 페이지에서 서비스를 선택, hello 서비스 이름 및 다음 hello 내에서 두 번 클릭 **구성** 섹션에서 클릭 **액세스 제어 레코드**합니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-126">On hello service landing page, select your service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>
2. <span data-ttu-id="32cd8-127">Hello에 **액세스 제어 레코드** 블레이드에서 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-127">In hello **Access control records** blade, click **Add**.</span></span>
3. <span data-ttu-id="32cd8-128">Hello에 **ACR 추가** 블레이드에서 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-128">In hello **Add ACR** blade, do hello following:</span></span>
   
    1. <span data-ttu-id="32cd8-129">ACR의 **이름** 을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-129">Supply a **Name** for your ACR.</span></span>
    
    2. <span data-ttu-id="32cd8-130">아래 **iSCSI 초기자 이름**, Windows 호스트의 IQN 이름을 hello를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-130">Under **iSCSI Initiator Name**, provide hello IQN name of your Windows host.</span></span> <span data-ttu-id="32cd8-131">Windows Server 호스트의 IQN tooget hello 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-131">tooget hello IQN of your Windows Server host, do hello following:</span></span>
   
    3. <span data-ttu-id="32cd8-132">Windows 호스트에 hello Microsoft iSCSI 초기자를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-132">Start hello Microsoft iSCSI initiator on your Windows host.</span></span> <span data-ttu-id="32cd8-133">Hello iSCSI 초기자 속성 창의 hello에서 **구성** 탭 선택 하 고 hello에서 hello 문자열을 복사 **초기자 이름** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-133">In hello iSCSI Initiator Properties window, on hello **Configuration** tab, select and copy hello string from hello **Initiator Name** field.</span></span>
    <span data-ttu-id="32cd8-134">Hello에이 문자열을 붙여 넣습니다. **IQN** 필드 hello에 **ACR 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-134">Paste this string in hello **IQN** field in hello **Add ACR** blade.</span></span>
   
    6. <span data-ttu-id="32cd8-135">클릭 **추가** tooadd hello ACR 합니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-135">Click **Add** tooadd hello ACR.</span></span>  
   
        ![액세스 제어 레코드 추가](./media/storsimple-virtual-array-manage-acrs/ova-add-acrs.png)
4. <span data-ttu-id="32cd8-137">테이블 형식 목록 hello 업데이트 tooreflect이이 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-137">hello tabular listing is updated tooreflect this addition.</span></span>

## <a name="edit-an-acr"></a><span data-ttu-id="32cd8-138">ACR 편집</span><span class="sxs-lookup"><span data-stu-id="32cd8-138">Edit an ACR</span></span>

<span data-ttu-id="32cd8-139">Hello를 사용 하 여 **액세스 제어 레코드** hello 내 블레이드 **구성** hello Azure 포털 tooedit Acr에서에서 장치 관리자 서비스의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-139">You use hello **Access control records** blade within hello **Configuration** section of your Device Manager service in hello Azure portal tooedit ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="32cd8-140">현재 사용 중인 ACR을 수정하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-140">You should not modify an ACR that is currently in use.</span></span> <span data-ttu-id="32cd8-141">현재 사용 중인 볼륨와 연결 된 ACR tooedit, 먼저 수행 해야 hello 볼륨 오프 라인입니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-141">tooedit an ACR associated with a volume that is currently in use, you should first take hello volume offline.</span></span>


<span data-ttu-id="32cd8-142">Hello 단계 tooedit ACR 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-142">Perform hello following steps tooedit an ACR.</span></span>

#### <a name="tooedit-an-acr"></a><span data-ttu-id="32cd8-143">ACR tooedit</span><span class="sxs-lookup"><span data-stu-id="32cd8-143">tooedit an ACR</span></span>

1. <span data-ttu-id="32cd8-144">Hello 서비스 방문 페이지에서 서비스를 선택, hello 서비스 이름 및 다음 hello 내에서 두 번 클릭 **구성** 섹션 **액세스 제어 레코드**합니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-144">On hello service landing page, select your service, double-click hello service name, and then within hello **Configuration** section, **Access control records**.</span></span>
2. <span data-ttu-id="32cd8-145">Hello에 **액세스 제어 레코드** hello hello 액세스 제어 레코드의 테이블 형식 목록에서 블레이드 hello toomodify 한다고 ACR를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-145">In hello **Access control records** blade, from hello tabular listing of hello access control records, double-click hello ACR that you wish toomodify.</span></span>
3. <span data-ttu-id="32cd8-146">Hello에 **액세스 제어 레코드 편집** 블레이드에서 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-146">In hello **Edit access control records** blade, do hello following:</span></span>
   
    1. <span data-ttu-id="32cd8-147">ACR hello에 대 한 hello IQN을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-147">Supply hello IQN for hello ACR.</span></span>
   
    2. <span data-ttu-id="32cd8-148">클릭 **저장** hello hello 블레이드 toosave hello 위쪽에 ACR을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-148">Click **Save** at hello top of hello blade toosave hello modified ACR.</span></span> <span data-ttu-id="32cd8-149">Hello 다음 확인 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-149">You see hello following confirmation message:</span></span>
   
        ![액세스 제어 레코드 편집](./media/storsimple-virtual-array-manage-acrs/ova-edit-acrs.png)

## <a name="delete-an-access-control-record"></a><span data-ttu-id="32cd8-151">액세스 제어 레코드 삭제</span><span class="sxs-lookup"><span data-stu-id="32cd8-151">Delete an access control record</span></span>

<span data-ttu-id="32cd8-152">Hello를 사용 하 여 **구성** hello Azure 포털 toodelete Acr의에서 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-152">You use hello **Configuration** page in hello Azure portal toodelete ACRs.</span></span>

> [!NOTE]
> 
> * <span data-ttu-id="32cd8-153">현재 사용 중인 ACR을 삭제하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-153">You should not delete an ACR that is currently in use.</span></span> <span data-ttu-id="32cd8-154">현재 사용 중인 볼륨와 연결 된 ACR toodelete, 먼저 수행 해야 hello 볼륨 오프 라인입니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-154">toodelete an ACR associated with a volume that is currently in use, you should first take hello volume offline.</span></span>
> * <span data-ttu-id="32cd8-155">볼륨에서 ACR을 삭제할 때는 해당 호스트에서 해당 hello 하지에 액세스 하는 hello 볼륨 hello 삭제 읽기-쓰기 중단이 발생할 수 있기 때문에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-155">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>


<span data-ttu-id="32cd8-156">Hello 단계 toodelete 액세스 제어 레코드를 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-156">Perform hello following steps toodelete an access control record.</span></span>

#### <a name="toodelete-an-access-control-record"></a><span data-ttu-id="32cd8-157">toodelete 액세스 제어 레코드</span><span class="sxs-lookup"><span data-stu-id="32cd8-157">toodelete an access control record</span></span>

1. <span data-ttu-id="32cd8-158">Hello 서비스 방문 페이지에서 서비스를 선택, hello 서비스 이름 및 다음 hello 내에서 두 번 클릭 **구성** 섹션 **액세스 제어 레코드**합니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-158">On hello service landing page, select your service, double-click hello service name, and then within hello **Configuration** section, **Access control records**.</span></span>

2. <span data-ttu-id="32cd8-159">Hello에 **액세스 제어 레코드** hello hello 액세스 제어 레코드의 테이블 형식 목록에서 블레이드 hello toodelete 한다고 ACR를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-159">In hello **Access control records** blade, from hello tabular listing of hello access control records, double-click hello ACR that you wish toodelete.</span></span>

3. <span data-ttu-id="32cd8-160">Hello 편집 액세스 제어 레코드 블레이드에서 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-160">In hello Edit access control records blade, click **Delete**.</span></span>
   
    ![ACR 삭제](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs.png)

4. <span data-ttu-id="32cd8-162">확인 메시지가 나타나면 클릭 **삭제** toocontinue hello 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-162">When prompted for confirmation, click **Delete** toocontinue with hello deletion.</span></span> <span data-ttu-id="32cd8-163">hello 테이블 형식 목록에는 업데이트 된 tooreflect hello 삭제입니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-163">hello tabular listing is updated tooreflect hello deletion.</span></span>
   
   ![경고 메시지](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs-warning.png)

## <a name="next-steps"></a><span data-ttu-id="32cd8-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="32cd8-165">Next steps</span></span>

* <span data-ttu-id="32cd8-166">[볼륨 추가 및 ACR 구성](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="32cd8-166">Learn more about [adding volumes and configuring ACRs](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span></span>

