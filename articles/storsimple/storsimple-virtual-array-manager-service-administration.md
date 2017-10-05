---
title: "Microsoft Azure StorSimple Manager 가상 배열 관리 | Microsoft Docs"
description: "Azure Portal에서 StorSimple 장치 관리자 서비스를 사용하여 StorSimple 온-프레미스 가상 배열을 관리하는 방법을 알아봅니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 958244a5-f9f5-455e-b7ef-71a65558872e
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/1/2016
ms.author: alkohli
ms.openlocfilehash: a74a160eae88a2d03460a1346479c333d8f9d524
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-administer-your-storsimple-virtual-array"></a><span data-ttu-id="e16e2-103">StorSimple 장치 관리자 서비스를 사용하여 StorSimple 가상 배열 관리</span><span class="sxs-lookup"><span data-stu-id="e16e2-103">Use the StorSimple Device Manager service to administer your StorSimple Virtual Array</span></span>
![설정 프로세스 흐름](./media/storsimple-virtual-array-manager-service-administration/manage4.png)

## <a name="overview"></a><span data-ttu-id="e16e2-105">개요</span><span class="sxs-lookup"><span data-stu-id="e16e2-105">Overview</span></span>
<span data-ttu-id="e16e2-106">이 문서에서는 연결 방법, 사용 가능한 여러 옵션을 포함한 StorSimple 장치 관리자 서비스 인터페이스를 설명하고 이 UI를 통해 수행될 수 있는 특정 워크로드에 대한 링크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e16e2-106">This article describes the StorSimple Device Manager service interface, including how to connect to it and the various options available, and provides links to the specific workflows that can be performed via this UI.</span></span>

<span data-ttu-id="e16e2-107">이 문서를 읽은 후 다음 방법에 대해 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e16e2-107">After reading this article, you will know how to:</span></span>

* <span data-ttu-id="e16e2-108">StorSimple 장치 관리자 서비스에 연결</span><span class="sxs-lookup"><span data-stu-id="e16e2-108">Connect to the StorSimple Device Manager service</span></span>
* <span data-ttu-id="e16e2-109">StorSimple 장치 관리자 UI로 이동</span><span class="sxs-lookup"><span data-stu-id="e16e2-109">Navigate the StorSimple Device Manager UI</span></span>
* <span data-ttu-id="e16e2-110">StorSimple 장치 관리자 서비스를 통한 StorSimple 가상 배열 관리</span><span class="sxs-lookup"><span data-stu-id="e16e2-110">Administer your StorSimple Virtual Array via the StorSimple Device Manager service</span></span>

> [!NOTE]
> <span data-ttu-id="e16e2-111">StorSimple 8000 시리즈 장치에 사용 가능한 관리 옵션을 보려면 [StorSimple 관리자 서비스를 사용하여 StorSimple 장치 관리](storsimple-manager-service-administration.md)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="e16e2-111">To view the management options available for the StorSimple 8000 series device, go to [Use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>
> 
> 

## <a name="connect-to-the-storsimple-device-manager-service"></a><span data-ttu-id="e16e2-112">StorSimple 장치 관리자 서비스에 연결</span><span class="sxs-lookup"><span data-stu-id="e16e2-112">Connect to the StorSimple Device Manager service</span></span>
<span data-ttu-id="e16e2-113">StorSimple 장치 관리자 서비스는 Microsoft Azure에서 실행되며 여러 StorSimple 가상 배열에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="e16e2-113">The StorSimple Device Manager service runs in Microsoft Azure and connects to multiple StorSimple Virtual Arrays.</span></span> <span data-ttu-id="e16e2-114">이러한 장치를 관리하는 브라우저에서 실행되는 중앙 Microsoft Azure Portal을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e16e2-114">You use a central Microsoft Azure portal running in a browser to manage these devices.</span></span> <span data-ttu-id="e16e2-115">StorSimple 장치 관리자 서비스에 연결하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e16e2-115">To connect to the StorSimple Device Manager service, do the following.</span></span>

#### <a name="to-connect-to-the-service"></a><span data-ttu-id="e16e2-116">해당 서비스에 연결하려면</span><span class="sxs-lookup"><span data-stu-id="e16e2-116">To connect to the service</span></span>
1. <span data-ttu-id="e16e2-117">[https://ms.portal.azure.com](https://ms.portal.azure.com)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e16e2-117">Go to [https://ms.portal.azure.com](https://ms.portal.azure.com).</span></span>
2. <span data-ttu-id="e16e2-118">Microsoft 계정 자격 증명을 사용하여 Microsoft Azure Portal(해당 창의 상단 오른쪽에 있는)로 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="e16e2-118">Using your Microsoft account credentials, log on to the Microsoft Azure portal (located at the top-right of the pane).</span></span>
3. <span data-ttu-id="e16e2-119">지정된 구독에서 모든 장치 관리자를 보려면 StorSimple 장치 관리자에서 찾아보기 --> '필터'로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e16e2-119">Navigate to Browse --> 'Filter' on StorSimple Device Managers to view all your device managers in a given subscription.</span></span>

## <a name="use-the-storsimple-device-manager-service-to-perform-management-tasks"></a><span data-ttu-id="e16e2-120">StorSimple 장치 관리자 서비스를 사용하여 관리 작업 수행</span><span class="sxs-lookup"><span data-stu-id="e16e2-120">Use the StorSimple Device Manager service to perform management tasks</span></span>
<span data-ttu-id="e16e2-121">다음 표에서 모든 일반 관리 작업 및 StorSimple 장치 관리자 서비스 요약 블레이드 내에서 수행할 수 있는 복잡한 워크플로의 요약을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="e16e2-121">The following table shows a summary of all the common management tasks and complex workflows that can be performed within the StorSimple Device Manager service summary blade.</span></span> <span data-ttu-id="e16e2-122">이러한 작업은 시작되는 블레이드 페이지에 따라 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e16e2-122">These tasks are organized based on the blades on which they are initiated.</span></span>

<span data-ttu-id="e16e2-123">각 워크플로에 대한 자세한 내용은 표에서 적절한 절차를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e16e2-123">For more information about each workflow, click the appropriate procedure in the table.</span></span>

#### <a name="storsimple-device-manager-workflows"></a><span data-ttu-id="e16e2-124">StorSimple 장치 관리자 워크플로</span><span class="sxs-lookup"><span data-stu-id="e16e2-124">StorSimple Device Manager workflows</span></span>
| <span data-ttu-id="e16e2-125">수행하려는 작업 ...</span><span class="sxs-lookup"><span data-stu-id="e16e2-125">If you want to do this ...</span></span> | <span data-ttu-id="e16e2-126">이 절차 사용</span><span class="sxs-lookup"><span data-stu-id="e16e2-126">Use this procedure</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e16e2-127">서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="e16e2-127">Create a service</span></span></br><span data-ttu-id="e16e2-128">서비스 삭제</span><span class="sxs-lookup"><span data-stu-id="e16e2-128">Delete a service</span></span></br><span data-ttu-id="e16e2-129">서비스 등록 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="e16e2-129">Get the service registration key</span></span></br><span data-ttu-id="e16e2-130">서비스 등록 키 다시 생성</span><span class="sxs-lookup"><span data-stu-id="e16e2-130">Regenerate the service registration key</span></span> |[<span data-ttu-id="e16e2-131">StorSimple 장치 관리자 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="e16e2-131">Deploy the StorSimple Device Manager service</span></span>](storsimple-virtual-array-manage-service.md) |
| <span data-ttu-id="e16e2-132">작업 로그 보기</span><span class="sxs-lookup"><span data-stu-id="e16e2-132">View the activity logs</span></span> |[<span data-ttu-id="e16e2-133">StorSimple 서비스 요약 사용</span><span class="sxs-lookup"><span data-stu-id="e16e2-133">Use the StorSimple service summary</span></span>](storsimple-virtual-array-service-summary.md) |
| <span data-ttu-id="e16e2-134">가상 배열 비활성화</span><span class="sxs-lookup"><span data-stu-id="e16e2-134">Deactivate a Virtual Array</span></span></br><span data-ttu-id="e16e2-135">가상 배열 삭제</span><span class="sxs-lookup"><span data-stu-id="e16e2-135">Delete a Virtual Array</span></span> |[<span data-ttu-id="e16e2-136">가상 배열 비활성화 또는 삭제</span><span class="sxs-lookup"><span data-stu-id="e16e2-136">Deactivate or delete a virtual array</span></span>](storsimple-virtual-array-deactivate-and-delete-device.md) |
| <span data-ttu-id="e16e2-137">재해 복구 및 장치 장애 조치(Failover)</span><span class="sxs-lookup"><span data-stu-id="e16e2-137">Disaster recovery and device failover</span></span></br><span data-ttu-id="e16e2-138">장애 조치 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="e16e2-138">Failover prerequisites</span></span></br><span data-ttu-id="e16e2-139">비즈니스 연속성 재해 복구(BCDR)</span><span class="sxs-lookup"><span data-stu-id="e16e2-139">Business continuity disaster recovery (BCDR)</span></span></br><span data-ttu-id="e16e2-140">재해 복구 중 오류</span><span class="sxs-lookup"><span data-stu-id="e16e2-140">Errors during disaster recovery</span></span> |[<span data-ttu-id="e16e2-141">StorSimple 가상 배열에 대한 재해 복구 및 장치 장애 조치(failover)</span><span class="sxs-lookup"><span data-stu-id="e16e2-141">Disaster recovery and device failover for your StorSimple Virtual Array</span></span>](storsimple-virtual-array-failover-dr.md) |
| <span data-ttu-id="e16e2-142">공유 및 볼륨 백업</span><span class="sxs-lookup"><span data-stu-id="e16e2-142">Back up shares and volumes</span></span></br><span data-ttu-id="e16e2-143">수동 백업 수행</span><span class="sxs-lookup"><span data-stu-id="e16e2-143">Take a manual backup</span></span></br><span data-ttu-id="e16e2-144">백업 일정 변경</span><span class="sxs-lookup"><span data-stu-id="e16e2-144">Change the backup schedule</span></span></br><span data-ttu-id="e16e2-145">기존 백업 확인</span><span class="sxs-lookup"><span data-stu-id="e16e2-145">View existing backups</span></span> |[<span data-ttu-id="e16e2-146">StorSimple 가상 배열 백업</span><span class="sxs-lookup"><span data-stu-id="e16e2-146">Back up your StorSimple Virtual Array</span></span>](storsimple-virtual-array-backup.md) |
| <span data-ttu-id="e16e2-147">백업 세트에서 공유 복제</span><span class="sxs-lookup"><span data-stu-id="e16e2-147">Clone shares from a backup set</span></span></br><span data-ttu-id="e16e2-148">백업 세트에서 볼륨 복제</span><span class="sxs-lookup"><span data-stu-id="e16e2-148">Clone volumes from a backup set</span></span></br><span data-ttu-id="e16e2-149">항목 수준 복구(파일 서버에만 해당)</span><span class="sxs-lookup"><span data-stu-id="e16e2-149">Item-level recovery (file server only)</span></span> |[<span data-ttu-id="e16e2-150">StorSimple 가상 배열의 백업에서 복제</span><span class="sxs-lookup"><span data-stu-id="e16e2-150">Clone from a backup of your StorSimple Virtual Array</span></span>](storsimple-virtual-array-clone.md) |
| <span data-ttu-id="e16e2-151">Storage 계정 정보</span><span class="sxs-lookup"><span data-stu-id="e16e2-151">About  storage accounts</span></span></br><span data-ttu-id="e16e2-152">저장소 계정 추가</span><span class="sxs-lookup"><span data-stu-id="e16e2-152">Add a storage account</span></span></br><span data-ttu-id="e16e2-153">저장소 계정 편집</span><span class="sxs-lookup"><span data-stu-id="e16e2-153">Edit a storage account</span></span></br><span data-ttu-id="e16e2-154">저장소 계정 삭제</span><span class="sxs-lookup"><span data-stu-id="e16e2-154">Delete a storage account</span></span> |[<span data-ttu-id="e16e2-155">StorSimple 가상 배열에 대한 저장소 계정 관리</span><span class="sxs-lookup"><span data-stu-id="e16e2-155">Manage storage accounts for the StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-storage-accounts.md) |
| <span data-ttu-id="e16e2-156">액세스 제어 레코드 정보</span><span class="sxs-lookup"><span data-stu-id="e16e2-156">About access control records</span></span></br><span data-ttu-id="e16e2-157">액세스 제어 레코드 추가 또는 수정</span><span class="sxs-lookup"><span data-stu-id="e16e2-157">Add or modify an access control record</span></span> </br><span data-ttu-id="e16e2-158">액세스 제어 레코드 삭제</span><span class="sxs-lookup"><span data-stu-id="e16e2-158">Delete an access control record</span></span> |[<span data-ttu-id="e16e2-159">StorSimple 가상 배열에 대한 액세스 제어 레코드 관리</span><span class="sxs-lookup"><span data-stu-id="e16e2-159">Manage access control records for the StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-acrs.md) |
| <span data-ttu-id="e16e2-160">작업 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="e16e2-160">View job details</span></span> |[<span data-ttu-id="e16e2-161">StorSimple 가상 배열 작업 관리</span><span class="sxs-lookup"><span data-stu-id="e16e2-161">Manage StorSimple Virtual Array jobs</span></span>](storsimple-virtual-array-manage-jobs.md) |
| <span data-ttu-id="e16e2-162">경고 설정 구성</span><span class="sxs-lookup"><span data-stu-id="e16e2-162">Configure alert settings</span></span></br><span data-ttu-id="e16e2-163">경고 알림 받기</span><span class="sxs-lookup"><span data-stu-id="e16e2-163">Receive alert notifications</span></span></br><span data-ttu-id="e16e2-164">경고 관리</span><span class="sxs-lookup"><span data-stu-id="e16e2-164">Manage alerts</span></span></br><span data-ttu-id="e16e2-165">경고 검토</span><span class="sxs-lookup"><span data-stu-id="e16e2-165">Review alerts</span></span> |[<span data-ttu-id="e16e2-166">StorSimple 가상 배열에 대한 경고 보기 및 관리</span><span class="sxs-lookup"><span data-stu-id="e16e2-166">View and manage alerts for the StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-alerts.md) |
| <span data-ttu-id="e16e2-167">장치 관리자 암호 수정</span><span class="sxs-lookup"><span data-stu-id="e16e2-167">Modify the device administrator password</span></span> |[<span data-ttu-id="e16e2-168">StorSimple 가상 배열 장치 관리자 암호 변경</span><span class="sxs-lookup"><span data-stu-id="e16e2-168">Change the StorSimple Virtual Array device administrator password</span></span>](storsimple-virtual-array-change-device-admin-password.md) |
| <span data-ttu-id="e16e2-169">소프트웨어 업데이트 설치</span><span class="sxs-lookup"><span data-stu-id="e16e2-169">Install software updates</span></span> |[<span data-ttu-id="e16e2-170">가상 배열 업데이트</span><span class="sxs-lookup"><span data-stu-id="e16e2-170">Update your Virtual Array</span></span>](storsimple-virtual-array-install-update.md) |

> [!NOTE]
> <span data-ttu-id="e16e2-171">다음과 같은 작업에 대해 [로컬 웹 UI](storsimple-ova-web-ui-admin.md) 를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e16e2-171">You must use the [local web UI](storsimple-ova-web-ui-admin.md) for the following tasks:</span></span>
> 
> * [<span data-ttu-id="e16e2-172">서비스 데이터 암호화 키 검색</span><span class="sxs-lookup"><span data-stu-id="e16e2-172">Retrieve the service data encryption key</span></span>](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key)
> * [<span data-ttu-id="e16e2-173">지원 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="e16e2-173">Create a support package</span></span>](storsimple-ova-web-ui-admin.md#generate-a-log-package)
> * [<span data-ttu-id="e16e2-174">가상 배열 중지 및 다시 시작</span><span class="sxs-lookup"><span data-stu-id="e16e2-174">Stop and restart a Virtual Array</span></span>](storsimple-ova-web-ui-admin.md#shut-down-and-restart-your-device)
> 
> 

## <a name="next-steps"></a><span data-ttu-id="e16e2-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e16e2-175">Next steps</span></span>
<span data-ttu-id="e16e2-176">웹 UI 및 사용 방법에 대한 자세한 내용은 [StorSimple 웹 UI를 사용하여 StorSimple 가상 배열 관리](storsimple-ova-web-ui-admin.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e16e2-176">For information about the web UI and how to use it, go to [Use the StorSimple web UI to administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

