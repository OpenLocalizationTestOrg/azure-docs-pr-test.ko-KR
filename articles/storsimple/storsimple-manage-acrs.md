---
title: "StorSimple에 대 한 액세스 제어 레코드 aaaManage | Microsoft Docs"
description: "Toouse 액세스 제어 (Acr) toodetermine tooa 볼륨 hello StorSimple 장치에 연결할 수 있는 호스트를 기록 하는 방법을 설명 합니다."
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
ms.openlocfilehash: a1e718c2679301b34221a233557a1eaae869a94f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-access-control-records"></a><span data-ttu-id="08905-103">Hello StorSimple 관리자 서비스 toomanage 액세스 제어 레코드를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="08905-103">Use hello StorSimple Manager service toomanage access control records</span></span>
## <a name="overview"></a><span data-ttu-id="08905-104">개요</span><span class="sxs-lookup"><span data-stu-id="08905-104">Overview</span></span>
<span data-ttu-id="08905-105">액세스 제어 레코드 (Acr) toospecify tooa 볼륨 hello StorSimple 장치에 연결할 수 있는 호스트를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="08905-105">Access control records (ACRs) allow you toospecify which hosts can connect tooa volume on hello StorSimple device.</span></span> <span data-ttu-id="08905-106">Acr tooa 특정 볼륨을 설정 하 고 hello iSCSI 포함 hello 호스트의 정규화 된 이름 (iqn이 포함).</span><span class="sxs-lookup"><span data-stu-id="08905-106">ACRs are set tooa specific volume and contain hello iSCSI Qualified Names (IQNs) of hello hosts.</span></span> <span data-ttu-id="08905-107">호스트 tooconnect tooa 볼륨 오류 값을 hello 장치 hello ACR 해당 볼륨에 연결 된 일치 하는 경우 hello 연결이 설정 되 고 hello IQN 이름을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="08905-107">When a host tries tooconnect tooa volume, hello device checks hello ACR associated with that volume for hello IQN name and if there is a match, then hello connection is established.</span></span> <span data-ttu-id="08905-108">hello 액세스 제어 레코드 섹션 hello에 **구성** hello 호스트의 iqn이 포함에 해당 하는 hello로 hello 액세스 제어 레코드를 모든 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08905-108">hello access control records section on hello **Configure** page displays all hello access control records with hello corresponding IQNs of hello hosts.</span></span>

<span data-ttu-id="08905-109">이 자습서에서는 일반적인 ACR 관련 작업을 수행 하는 hello를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="08905-109">This tutorial explains hello following common ACR-related tasks:</span></span>

* <span data-ttu-id="08905-110">액세스 제어 레코드 추가</span><span class="sxs-lookup"><span data-stu-id="08905-110">Add an access control record</span></span> 
* <span data-ttu-id="08905-111">액세스 제어 레코드 편집</span><span class="sxs-lookup"><span data-stu-id="08905-111">Edit an access control record</span></span> 
* <span data-ttu-id="08905-112">액세스 제어 레코드 삭제</span><span class="sxs-lookup"><span data-stu-id="08905-112">Delete an access control record</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="08905-113">ACR tooa 볼륨을 할당할 때 주의 해야이 hello 볼륨 손상 될 수 있으므로 hello 볼륨 하나 이상의 클러스터 되지 않은 호스트에서 동시에 액세스 하지 않은 합니다.</span><span class="sxs-lookup"><span data-stu-id="08905-113">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span> 
> * <span data-ttu-id="08905-114">볼륨에서 ACR을 삭제할 때는 해당 호스트에서 해당 hello 하지에 액세스 하는 hello 볼륨 hello 삭제 읽기-쓰기 중단이 발생할 수 있기 때문에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="08905-114">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>
> 
> 

## <a name="add-an-access-control-record"></a><span data-ttu-id="08905-115">액세스 제어 레코드 추가</span><span class="sxs-lookup"><span data-stu-id="08905-115">Add an access control record</span></span>
<span data-ttu-id="08905-116">Hello StorSimple Manager 서비스를 사용 하 여 **구성** tooadd Acr 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="08905-116">You use hello StorSimple Manager service **Configure** page tooadd ACRs.</span></span> <span data-ttu-id="08905-117">일반적으로 하나의 볼륨으로 하나의 ACR을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="08905-117">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="08905-118">Hello 단계 tooadd ACR 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="08905-118">Perform hello following steps tooadd an ACR.</span></span>

#### <a name="tooadd-an-access-control-record"></a><span data-ttu-id="08905-119">tooadd 액세스 제어 레코드</span><span class="sxs-lookup"><span data-stu-id="08905-119">tooadd an access control record</span></span>
1. <span data-ttu-id="08905-120">Hello 서비스 방문 페이지에서 서비스를 선택 합니다. hello 서비스 이름을 두 번 클릭 하 고 클릭 hello **구성** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="08905-120">On hello service landing page, select your service, double-click hello service name, and then click hello **Configure** tab.</span></span>
2. <span data-ttu-id="08905-121">아래 나열 하는 테이블 형식 hello에 **액세스 제어 레코드**지정는 **이름** ACR에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="08905-121">In hello tabular listing under **Access control records**, supply a **Name** for your ACR.</span></span>
3. <span data-ttu-id="08905-122">Windows 호스트의 IQN 이름을 hello 제공 **iSCSI 초기자 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="08905-122">Provide hello IQN name of your Windows host under **iSCSI Initiator Name**.</span></span> <span data-ttu-id="08905-123">Windows Server 호스트의 IQN tooget hello 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="08905-123">tooget hello IQN of your Windows Server host, do hello following:</span></span>
   
   * <span data-ttu-id="08905-124">Windows 호스트에 hello Microsoft iSCSI 초기자를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="08905-124">Start hello Microsoft iSCSI initiator on your Windows host.</span></span>
   * <span data-ttu-id="08905-125">Hello에 **iSCSI 초기자 속성** 창의 hello에 **구성** 탭 선택 하 고 hello에서 hello 문자열을 복사 **초기자 이름** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="08905-125">In hello **iSCSI Initiator Properties** window, on hello **Configuration** tab, select and copy hello string from hello **Initiator Name** field.</span></span>
   * <span data-ttu-id="08905-126">Hello에이 문자열을 붙여 넣습니다. **iSCSI 초기자 이름** hello Azure 클래식 포털의에서 hello Acr 테이블에 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="08905-126">Paste this string in hello **iSCSI Initiator Name** field on hello ACRs table in hello Azure classic portal.</span></span>
4. <span data-ttu-id="08905-127">클릭 **저장** toosave hello 새로 ACR을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="08905-127">Click **Save** toosave hello newly created ACR.</span></span> <span data-ttu-id="08905-128">hello 나열 하는 테이블 형식 될 업데이트 된 tooreflect이이 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08905-128">hello tabular listing will be updated tooreflect this addition.</span></span>

## <a name="edit-an-access-control-record"></a><span data-ttu-id="08905-129">액세스 제어 레코드 편집</span><span class="sxs-lookup"><span data-stu-id="08905-129">Edit an access control record</span></span>
<span data-ttu-id="08905-130">Hello를 사용 하 여 **구성** hello Azure 클래식 포털 tooedit Acr의에서 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="08905-130">You use hello **Configure** page in hello Azure classic portal tooedit ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="08905-131">현재 사용하지 않고 있는 ACR만 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08905-131">You can modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="08905-132">현재 사용 중인 볼륨와 연결 된 ACR tooedit를 먼저 수행 해야 hello 볼륨 오프 라인으로.</span><span class="sxs-lookup"><span data-stu-id="08905-132">tooedit an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>
> 
> 

<span data-ttu-id="08905-133">Hello 단계 tooedit ACR 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="08905-133">Perform hello following steps tooedit an ACR.</span></span>

#### <a name="tooedit-an-access-control-record"></a><span data-ttu-id="08905-134">tooedit 액세스 제어 레코드</span><span class="sxs-lookup"><span data-stu-id="08905-134">tooedit an access control record</span></span>
1. <span data-ttu-id="08905-135">Hello 서비스 방문 페이지에서 서비스를 선택 합니다. hello 서비스 이름을 두 번 클릭 하 고 클릭 hello **구성** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="08905-135">On hello service landing page, select your service, double-click hello service name, and then click hello **Configure** tab.</span></span>
2. <span data-ttu-id="08905-136">Hello 액세스 제어 레코드의 테이블 형식 목록 hello에서에서 hello toomodify 하려는 ACR 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="08905-136">In hello tabular listing of hello access control records, hover over hello ACR that you wish toomodify.</span></span>
3. <span data-ttu-id="08905-137">ACR hello에 대 한 새 이름 및/또는 IQN을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="08905-137">Supply a new name and/or IQN for hello ACR.</span></span>
4. <span data-ttu-id="08905-138">클릭 **저장** toosave hello ACR을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="08905-138">Click **Save** toosave hello modified ACR.</span></span> <span data-ttu-id="08905-139">hello 나열 하는 테이블 형식 업데이트 tooreflect이이 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08905-139">hello tabular listing will be updated tooreflect this change.</span></span>

## <a name="delete-an-access-control-record"></a><span data-ttu-id="08905-140">액세스 제어 레코드 삭제</span><span class="sxs-lookup"><span data-stu-id="08905-140">Delete an access control record</span></span>
<span data-ttu-id="08905-141">Hello를 사용 하 여 **구성** hello Azure 클래식 포털 toodelete Acr의에서 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="08905-141">You use hello **Configure** page in hello Azure classic portal toodelete ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="08905-142">현재 사용하지 않고 있는 ACR만 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08905-142">You can delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="08905-143">현재 사용 중인 볼륨와 연결 된 ACR toodelete를 먼저 수행 해야 hello 볼륨 오프 라인으로.</span><span class="sxs-lookup"><span data-stu-id="08905-143">toodelete an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>
> 
> 

<span data-ttu-id="08905-144">Hello 단계 toodelete 액세스 제어 레코드를 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="08905-144">Perform hello following steps toodelete an access control record.</span></span>

#### <a name="toodelete-an-access-control-record"></a><span data-ttu-id="08905-145">toodelete 액세스 제어 레코드</span><span class="sxs-lookup"><span data-stu-id="08905-145">toodelete an access control record</span></span>
1. <span data-ttu-id="08905-146">Hello 서비스 방문 페이지에서 서비스를 선택 합니다. hello 서비스 이름을 두 번 클릭 하 고 클릭 hello **구성** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="08905-146">On hello service landing page, select your service, double-click hello service name, and then click hello **Configure** tab.</span></span>
2. <span data-ttu-id="08905-147">Hello (Acr) hello 액세스 제어 레코드의 테이블 형식 목록에서 hello toodelete 하려는 ACR 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="08905-147">In hello tabular listing of hello access control records (ACRs), hover over hello ACR that you wish toodelete.</span></span>
3. <span data-ttu-id="08905-148">삭제 아이콘 (**x**) ACR 선택 하는 hello에 대 한 hello 맨 오른쪽 열에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08905-148">A delete icon (**x**) will appear in hello extreme right column for hello ACR that you select.</span></span> <span data-ttu-id="08905-149">Hello 클릭 **x** 아이콘 toodelete hello ACR 합니다.</span><span class="sxs-lookup"><span data-stu-id="08905-149">Click hello **x** icon toodelete hello ACR.</span></span>
4. <span data-ttu-id="08905-150">확인 메시지가 나타나면 클릭 **예** toocontinue hello 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="08905-150">When prompted for confirmation, click **YES** toocontinue with hello deletion.</span></span> <span data-ttu-id="08905-151">hello 테이블 형식 목록에는 업데이트 된 tooreflect hello 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08905-151">hello tabular listing will be updated tooreflect hello deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08905-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="08905-152">Next steps</span></span>
* <span data-ttu-id="08905-153">[StorSimple 볼륨 관리](storsimple-manage-volumes.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="08905-153">Learn more about [managing StorSimple volumes](storsimple-manage-volumes.md).</span></span>
* <span data-ttu-id="08905-154">에 대 한 자세한 내용은 [StorSimple 장치의 StorSimple Manager 서비스 tooadminister를 hello를 사용 하 여](storsimple-manager-service-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="08905-154">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

