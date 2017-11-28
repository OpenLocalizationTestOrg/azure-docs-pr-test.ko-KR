---
title: "VM의 D: 드라이브를 데이터 디스크로 만들기 | Microsoft Docs"
description: "Windows VM의 D: 드라이브를 데이터 드라이브로 사용할 수 있도록 드라이브 문자를 변경하는 방법을 설명합니다."
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
ms.openlocfilehash: 7667175c01be2421bfc3badd83b1d8aaeb29bfde
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-d-drive-as-a-data-drive-on-a-windows-vm"></a><span data-ttu-id="aa713-103">D: 드라이브를 Windows VM의 데이터 드라이브로 사용</span><span class="sxs-lookup"><span data-stu-id="aa713-103">Use the D: drive as a data drive on a Windows VM</span></span>
<span data-ttu-id="aa713-104">응용 프로그램에서 D 드라이브를 사용하여 데이터를 저장해야 하는 경우 다음 지침에 따라 임시 디스크에 다른 드라이브 문자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa713-104">If your application needs to use the D drive to store data, follow these instructions to use a different drive letter for the temporary disk.</span></span> <span data-ttu-id="aa713-105">보관해야 하는 데이터를 저장하는 데 임시 디스크를 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="aa713-105">Never use the temporary disk to store data that you need to keep.</span></span>

<span data-ttu-id="aa713-106">가상 컴퓨터의 크기를 조정하거나 **중지(할당 취소)** 하는 경우 새 하이퍼바이저로 가상 컴퓨터의 배치를 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa713-106">If you resize or **Stop (Deallocate)** a virtual machine, this may trigger placement of the virtual machine to a new hypervisor.</span></span> <span data-ttu-id="aa713-107">계획되거나 계획되지 않은 유지 관리 이벤트로 이 배치가 트리거될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa713-107">A planned or unplanned maintenance event may also trigger this placement.</span></span> <span data-ttu-id="aa713-108">이 시나리오에서는 임시 디스크가 첫 번째 사용 가능한 드라이브 문자에 다시 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa713-108">In this scenario, the temporary disk will be reassigned to the first available drive letter.</span></span> <span data-ttu-id="aa713-109">특히 D: 드라이브가 필요한 응용 프로그램의 경우 이러한 단계를 사용하여 pagefile.sys를 일시적으로 이동하고, 새 데이터 디스크를 연결한 후 문자 D를 할당한 다음, pagefile.sys를 임시 드라이브로 다시 이동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa713-109">If you have an application that specifically requires the D: drive, you need to follow these steps to temporarily move the pagefile.sys, attach a new data disk and assign it the letter D and then move the pagefile.sys back to the temporary drive.</span></span> <span data-ttu-id="aa713-110">완료된 후 VM이 다른 하이퍼바이저로 이동되어도 Azure는 D:를 다시 취소하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="aa713-110">Once complete, Azure will not take back the D: if the VM moves to a different hypervisor.</span></span>

<span data-ttu-id="aa713-111">Azure에서 임시 디스크를 사용하는 방법에 대한 자세한 내용은 [Microsoft Azure 가상 컴퓨터에서의 임시 드라이브 이해](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="aa713-111">For more information about how Azure uses the temporary disk, see [Understanding the temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span></span>

## <a name="attach-the-data-disk"></a><span data-ttu-id="aa713-112">데이터 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="aa713-112">Attach the data disk</span></span>
<span data-ttu-id="aa713-113">우선 가상 컴퓨터에 데이터 디스크를 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa713-113">First, you'll need to attach the data disk to the virtual machine.</span></span> <span data-ttu-id="aa713-114">포털을 사용하여 이를 수행하려면 [Azure Portal에서 관리되는 데이터 디스크를 연결하는 방법](attach-managed-disk-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aa713-114">To do this using the portal, see [How to attach a managed data disk in the Azure portal](attach-managed-disk-portal.md).</span></span>

## <a name="temporarily-move-pagefilesys-to-c-drive"></a><span data-ttu-id="aa713-115">pagefile.sys를 C 드라이브로 임시 이동</span><span class="sxs-lookup"><span data-stu-id="aa713-115">Temporarily move pagefile.sys to C drive</span></span>
1. <span data-ttu-id="aa713-116">가상 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="aa713-116">Connect to the virtual machine.</span></span> 
2. <span data-ttu-id="aa713-117">**시작** 메뉴를 마우스 오른쪽 단추로 클릭하고 **시스템**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aa713-117">Right-click the **Start** menu and select **System**.</span></span>
3. <span data-ttu-id="aa713-118">왼쪽 메뉴에서 **고급 시스템 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aa713-118">In the left-hand menu, select **Advanced system settings**.</span></span>
4. <span data-ttu-id="aa713-119">**성능** 섹션에서 **설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aa713-119">In the **Performance** section, select **Settings**.</span></span>
5. <span data-ttu-id="aa713-120">**고급** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aa713-120">Select the **Advanced** tab.</span></span>
6. <span data-ttu-id="aa713-121">**가상 메모리** 섹션에서 **변경**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aa713-121">In the **Virtual memory** section, select **Change**.</span></span>
7. <span data-ttu-id="aa713-122">**C** 드라이브를 선택한 후 **시스템이 관리하는 크기**를 클릭하고 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aa713-122">Select the **C** drive and then click **System managed size** and then click **Set**.</span></span>
8. <span data-ttu-id="aa713-123">**D** 드라이브를 선택하고 **페이징 파일 없음**을 클릭하고 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aa713-123">Select the **D** drive and then click **No paging file** and then click **Set**.</span></span>
9. <span data-ttu-id="aa713-124">적용을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aa713-124">Click Apply.</span></span> <span data-ttu-id="aa713-125">변경 내용을 적용하려면 컴퓨터를 다시 시작해야 한다는 경고가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa713-125">You will get a warning that the computer needs to be restarted for the changes to take affect.</span></span>
10. <span data-ttu-id="aa713-126">가상 컴퓨터를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="aa713-126">Restart the virtual machine.</span></span>

## <a name="change-the-drive-letters"></a><span data-ttu-id="aa713-127">드라이브 문자 변경</span><span class="sxs-lookup"><span data-stu-id="aa713-127">Change the drive letters</span></span>
1. <span data-ttu-id="aa713-128">VM이 다시 시작되면 VM에 다시 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="aa713-128">Once the VM restarts, log back on to the VM.</span></span>
2. <span data-ttu-id="aa713-129">**시작** 메뉴를 클릭하고 **diskmgmt.msc**를 입력한 후 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="aa713-129">Click the **Start** menu and type **diskmgmt.msc** and hit Enter.</span></span> <span data-ttu-id="aa713-130">디스크 관리가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa713-130">Disk Management will start.</span></span>
3. <span data-ttu-id="aa713-131">임시 저장소 드라이브인 **D**를 마우스 오른쪽 단추로 클릭하고 **드라이브 문자 및 경로 변경**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aa713-131">Right-click on **D**, the Temporary Storage drive, and select **Change Drive Letter and Paths**.</span></span>
4. <span data-ttu-id="aa713-132">드라이브 문자에서 **T**와 같은 새 드라이브를 선택한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aa713-132">Under Drive letter, select a new drive such as **T** and then click **OK**.</span></span> 
5. <span data-ttu-id="aa713-133">데이터 디스크를 마우스 오른쪽 단추로 클릭하고 **드라이브 문자 및 경로 변경**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aa713-133">Right-click on the data disk, and select **Change Drive Letter and Paths**.</span></span>
6. <span data-ttu-id="aa713-134">드라이브 문자에서 드라이브 **D**를 선택한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aa713-134">Under Drive letter, select drive **D** and then click **OK**.</span></span> 

## <a name="move-pagefilesys-back-to-the-temporary-storage-drive"></a><span data-ttu-id="aa713-135">pagefile.sys를 임시 저장소 드라이브로 다시 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="aa713-135">Move pagefile.sys back to the temporary storage drive</span></span>
1. <span data-ttu-id="aa713-136">**시작** 메뉴를 마우스 오른쪽 단추로 클릭하고 **시스템**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aa713-136">Right-click the **Start** menu and select **System**</span></span>
2. <span data-ttu-id="aa713-137">왼쪽 메뉴에서 **고급 시스템 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aa713-137">In the left-hand menu, select **Advanced system settings**.</span></span>
3. <span data-ttu-id="aa713-138">**성능** 섹션에서 **설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aa713-138">In the **Performance** section, select **Settings**.</span></span>
4. <span data-ttu-id="aa713-139">**고급** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aa713-139">Select the **Advanced** tab.</span></span>
5. <span data-ttu-id="aa713-140">**가상 메모리** 섹션에서 **변경**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aa713-140">In the **Virtual memory** section, select **Change**.</span></span>
6. <span data-ttu-id="aa713-141">OS 드라이브 **C**를 선택하고 **페이징 파일 없음**을 클릭하고 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aa713-141">Select the OS drive **C** and click **No paging file** and then click **Set**.</span></span>
7. <span data-ttu-id="aa713-142">임시 저장소 드라이브 **T**를 선택한 후 **시스템이 관리하는 크기**를 클릭하고 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aa713-142">Select the temporary storage drive **T** and then click **System managed size** and then click **Set**.</span></span>
8. <span data-ttu-id="aa713-143">**Apply**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aa713-143">Click **Apply**.</span></span> <span data-ttu-id="aa713-144">변경 내용을 적용하려면 컴퓨터를 다시 시작해야 한다는 경고가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa713-144">You will get a warning that the computer needs to be restarted for the changes to take affect.</span></span>
9. <span data-ttu-id="aa713-145">가상 컴퓨터를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="aa713-145">Restart the virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa713-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="aa713-146">Next steps</span></span>
* <span data-ttu-id="aa713-147">[추가 데이터 디스크를 연결](attach-managed-disk-portal.md)하여 가상 컴퓨터에서 사용할 수 있는 저장소를 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa713-147">You can increase the storage available to your virtual machine by [attaching a additional data disk](attach-managed-disk-portal.md).</span></span>

