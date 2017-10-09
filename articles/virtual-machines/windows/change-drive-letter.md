---
title: "VM 데이터 디스크의 d: 드라이브 hello 확인 | Microsoft Docs"
description: "데이터 드라이브로 hello d: 드라이브를 사용할 수 있도록 toochange 드라이브는 Windows VM에 대 한 문자가 방법을 설명 합니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 0867a931-0055-4e31-8403-9b38a3eeb904
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: cynthn
ms.openlocfilehash: 43939da1a890ac4049266487951e3889aa0ed9d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-d-drive-as-a-data-drive-on-a-windows-vm"></a><span data-ttu-id="80f57-103">Windows VM에서 데이터 드라이브로 hello d: 드라이브를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="80f57-103">Use hello D: drive as a data drive on a Windows VM</span></span>
<span data-ttu-id="80f57-104">응용 프로그램 toouse hello D 드라이브 toostore 데이터를 필요한 경우 이러한 지침 toouse hello 임시 디스크에 대 한 다른 드라이브 문자를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="80f57-104">If your application needs toouse hello D drive toostore data, follow these instructions toouse a different drive letter for hello temporary disk.</span></span> <span data-ttu-id="80f57-105">Tookeep 해야 하는 hello 임시 디스크 toostore 데이터를 사용 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="80f57-105">Never use hello temporary disk toostore data that you need tookeep.</span></span>

<span data-ttu-id="80f57-106">크기를 조정 하면 또는 **중지 (할당 취소)** 가상 컴퓨터이 hello 가상 컴퓨터 tooa 새 하이퍼바이저의 배치를 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80f57-106">If you resize or **Stop (Deallocate)** a virtual machine, this may trigger placement of hello virtual machine tooa new hypervisor.</span></span> <span data-ttu-id="80f57-107">계획되거나 계획되지 않은 유지 관리 이벤트로 이 배치가 트리거될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80f57-107">A planned or unplanned maintenance event may also trigger this placement.</span></span> <span data-ttu-id="80f57-108">이 시나리오에서는 hello 임시 디스크에 다시 할당 된 toohello 첫 번째 사용 가능한 드라이브 문자가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="80f57-108">In this scenario, hello temporary disk will be reassigned toohello first available drive letter.</span></span> <span data-ttu-id="80f57-109">특히 hello d: 드라이브를 필요로 하는 응용 프로그램의 경우 이러한 단계 tootemporarily 이동 hello pagefile.sys, 새 데이터 디스크를 연결 하 고 D hello 문자를 할당 한 다음 toohello 임시 드라이브를 다시 이동 hello pagefile.sys toofollow 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="80f57-109">If you have an application that specifically requires hello D: drive, you need toofollow these steps tootemporarily move hello pagefile.sys, attach a new data disk and assign it hello letter D and then move hello pagefile.sys back toohello temporary drive.</span></span> <span data-ttu-id="80f57-110">완료 되 면 Azure 사항을 다시 hello d: hello VM tooa 다른 하이퍼바이저를 이동 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="80f57-110">Once complete, Azure will not take back hello D: if hello VM moves tooa different hypervisor.</span></span>

<span data-ttu-id="80f57-111">Azure hello 임시 디스크를 사용 하는 방법에 대 한 자세한 내용은 참조 [hello 임시 드라이브를 Microsoft Azure 가상 컴퓨터 이해](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="80f57-111">For more information about how Azure uses hello temporary disk, see [Understanding hello temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span></span>

## <a name="attach-hello-data-disk"></a><span data-ttu-id="80f57-112">Hello 데이터 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="80f57-112">Attach hello data disk</span></span>
<span data-ttu-id="80f57-113">첫째, tooattach hello 데이터 디스크 toohello 가상 컴퓨터 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="80f57-113">First, you'll need tooattach hello data disk toohello virtual machine.</span></span> <span data-ttu-id="80f57-114">toodo이 hello 포털을 사용 하 여, 참조 [tooattach 관리 되는 데이터 디스크 hello Azure 포털에에서 어떻게](attach-managed-disk-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="80f57-114">toodo this using hello portal, see [How tooattach a managed data disk in hello Azure portal](attach-managed-disk-portal.md).</span></span>

## <a name="temporarily-move-pagefilesys-tooc-drive"></a><span data-ttu-id="80f57-115">Pagefile.sys tooC 드라이브를 일시적으로 이동</span><span class="sxs-lookup"><span data-stu-id="80f57-115">Temporarily move pagefile.sys tooC drive</span></span>
1. <span data-ttu-id="80f57-116">Toohello 가상 컴퓨터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="80f57-116">Connect toohello virtual machine.</span></span> 
2. <span data-ttu-id="80f57-117">마우스 오른쪽 단추로 클릭 hello **시작** 메뉴와 선택 **시스템**합니다.</span><span class="sxs-lookup"><span data-stu-id="80f57-117">Right-click hello **Start** menu and select **System**.</span></span>
3. <span data-ttu-id="80f57-118">Hello 왼쪽 메뉴에서 선택 **고급 시스템 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="80f57-118">In hello left-hand menu, select **Advanced system settings**.</span></span>
4. <span data-ttu-id="80f57-119">Hello에 **성능** 섹션에서 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="80f57-119">In hello **Performance** section, select **Settings**.</span></span>
5. <span data-ttu-id="80f57-120">선택 hello **고급** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="80f57-120">Select hello **Advanced** tab.</span></span>
6. <span data-ttu-id="80f57-121">Hello에 **가상 메모리** 섹션에서 **변경**합니다.</span><span class="sxs-lookup"><span data-stu-id="80f57-121">In hello **Virtual memory** section, select **Change**.</span></span>
7. <span data-ttu-id="80f57-122">선택 hello **C** 드라이브 및 클릭 **시스템 관리 하는 크기** 클릭 하 고 **설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="80f57-122">Select hello **C** drive and then click **System managed size** and then click **Set**.</span></span>
8. <span data-ttu-id="80f57-123">선택 hello **D** 드라이브 및 클릭 **페이징 파일 없음** 클릭 하 고 **설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="80f57-123">Select hello **D** drive and then click **No paging file** and then click **Set**.</span></span>
9. <span data-ttu-id="80f57-124">적용을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80f57-124">Click Apply.</span></span> <span data-ttu-id="80f57-125">해당 hello 컴퓨터 toobe hello 변경 tootake 영향에 대 한 다시 시작 필요 경고를 받아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80f57-125">You will get a warning that hello computer needs toobe restarted for hello changes tootake affect.</span></span>
10. <span data-ttu-id="80f57-126">Hello 가상 컴퓨터를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="80f57-126">Restart hello virtual machine.</span></span>

## <a name="change-hello-drive-letters"></a><span data-ttu-id="80f57-127">Hello 드라이브 문자 변경</span><span class="sxs-lookup"><span data-stu-id="80f57-127">Change hello drive letters</span></span>
1. <span data-ttu-id="80f57-128">한 번 hello VM 다시 시작 하면 toohello VM에 다시 로그온 합니다.</span><span class="sxs-lookup"><span data-stu-id="80f57-128">Once hello VM restarts, log back on toohello VM.</span></span>
2. <span data-ttu-id="80f57-129">Hello 클릭 **시작** 메뉴 및 형식 **diskmgmt.msc** Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="80f57-129">Click hello **Start** menu and type **diskmgmt.msc** and hit Enter.</span></span> <span data-ttu-id="80f57-130">디스크 관리가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="80f57-130">Disk Management will start.</span></span>
3. <span data-ttu-id="80f57-131">마우스 오른쪽 단추로 클릭 **D**, 임시 저장소 드라이브 hello 및 선택 **드라이브 문자 및 경로 변경**합니다.</span><span class="sxs-lookup"><span data-stu-id="80f57-131">Right-click on **D**, hello Temporary Storage drive, and select **Change Drive Letter and Paths**.</span></span>
4. <span data-ttu-id="80f57-132">드라이브 문자에서 **T**와 같은 새 드라이브를 선택한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80f57-132">Under Drive letter, select a new drive such as **T** and then click **OK**.</span></span> 
5. <span data-ttu-id="80f57-133">Hello 데이터 디스크를 마우스 오른쪽 단추로 클릭 하 고 선택 **드라이브 문자 및 경로 변경**합니다.</span><span class="sxs-lookup"><span data-stu-id="80f57-133">Right-click on hello data disk, and select **Change Drive Letter and Paths**.</span></span>
6. <span data-ttu-id="80f57-134">드라이브 문자에서 드라이브 **D**를 선택한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80f57-134">Under Drive letter, select drive **D** and then click **OK**.</span></span> 

## <a name="move-pagefilesys-back-toohello-temporary-storage-drive"></a><span data-ttu-id="80f57-135">Pagefile.sys 백 toohello 임시 저장소 드라이브를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="80f57-135">Move pagefile.sys back toohello temporary storage drive</span></span>
1. <span data-ttu-id="80f57-136">마우스 오른쪽 단추로 클릭 hello **시작** 메뉴와 선택 **시스템**</span><span class="sxs-lookup"><span data-stu-id="80f57-136">Right-click hello **Start** menu and select **System**</span></span>
2. <span data-ttu-id="80f57-137">Hello 왼쪽 메뉴에서 선택 **고급 시스템 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="80f57-137">In hello left-hand menu, select **Advanced system settings**.</span></span>
3. <span data-ttu-id="80f57-138">Hello에 **성능** 섹션에서 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="80f57-138">In hello **Performance** section, select **Settings**.</span></span>
4. <span data-ttu-id="80f57-139">선택 hello **고급** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="80f57-139">Select hello **Advanced** tab.</span></span>
5. <span data-ttu-id="80f57-140">Hello에 **가상 메모리** 섹션에서 **변경**합니다.</span><span class="sxs-lookup"><span data-stu-id="80f57-140">In hello **Virtual memory** section, select **Change**.</span></span>
6. <span data-ttu-id="80f57-141">Hello 운영 체제 드라이브를 선택 **C** 클릭 **페이징 파일 없음** 클릭 하 고 **설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="80f57-141">Select hello OS drive **C** and click **No paging file** and then click **Set**.</span></span>
7. <span data-ttu-id="80f57-142">Hello 임시 저장소 드라이브를 선택 **T** 클릭 하 고 **시스템 관리 하는 크기** 클릭 하 고 **설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="80f57-142">Select hello temporary storage drive **T** and then click **System managed size** and then click **Set**.</span></span>
8. <span data-ttu-id="80f57-143">**Apply**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="80f57-143">Click **Apply**.</span></span> <span data-ttu-id="80f57-144">해당 hello 컴퓨터 toobe hello 변경 tootake 영향에 대 한 다시 시작 필요 경고를 받아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80f57-144">You will get a warning that hello computer needs toobe restarted for hello changes tootake affect.</span></span>
9. <span data-ttu-id="80f57-145">Hello 가상 컴퓨터를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="80f57-145">Restart hello virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="80f57-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="80f57-146">Next steps</span></span>
* <span data-ttu-id="80f57-147">Hello 하 여 사용 가능한 tooyour 가상 컴퓨터 저장소를 늘릴 수 [추가 데이터 디스크 연결](attach-managed-disk-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="80f57-147">You can increase hello storage available tooyour virtual machine by [attaching a additional data disk](attach-managed-disk-portal.md).</span></span>

