---
title: "Windows VM에 관리되는 데이터 디스크 연결 - Azure | Microsoft Docs"
description: "리소스 관리자 배포 모델을 사용하여 Azure Portal에서 Windows VM에 신규 관리되는 데이터 디스크를 연결하는 방법입니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: f0cf88a06c5470ef173b22e7213419a6c8760723
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-attach-a-managed-data-disk-to-a-windows-vm-in-the-azure-portal"></a><span data-ttu-id="7ab68-103">Azure Portal에서 Windows VM에 관리되는 데이터 디스크를 연결하는 방법</span><span class="sxs-lookup"><span data-stu-id="7ab68-103">How to attach a managed data disk to a Windows VM in the Azure portal</span></span>

<span data-ttu-id="7ab68-104">이 문서에서는 Azure Portal을 통해 신규 관리되는 데이터 디스크를 Windows 가상 컴퓨터에 연결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7ab68-104">This article shows you how to attach a new managed data disk to Windows virtual machines through the Azure portal.</span></span> <span data-ttu-id="7ab68-105">이 작업을 수행 하기 전에 다음 팁을 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="7ab68-105">Before you do this, review these tips:</span></span>

* <span data-ttu-id="7ab68-106">가상 컴퓨터의 크기로 연결할 수 있는 디스크 개수가 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab68-106">The size of the virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="7ab68-107">자세한 내용은 [가상 컴퓨터의 크기](sizes.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ab68-107">For details, see [Sizes for virtual machines](sizes.md).</span></span>
* <span data-ttu-id="7ab68-108">새 디스크의 경우 Azure가 디스크를 연결할 때 생성하므로 먼저 생성하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab68-108">For a new disk, you don't need to create it first because Azure creates it when you attach it.</span></span>

<span data-ttu-id="7ab68-109">또한 [Powershell을 사용하여 데이터 디스크를 연결](attach-disk-ps.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab68-109">You can also [attach a data disk using Powershell](attach-disk-ps.md).</span></span>



## <a name="add-a-data-disk"></a><span data-ttu-id="7ab68-110">데이터 디스크 추가</span><span class="sxs-lookup"><span data-stu-id="7ab68-110">Add a data disk</span></span>
1. <span data-ttu-id="7ab68-111">왼쪽 메뉴에서 **가상 컴퓨터**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab68-111">In the menu on the left, click **Virtual Machines**.</span></span>
2. <span data-ttu-id="7ab68-112">목록에서 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab68-112">Select the virtual machine from the list.</span></span>
3. <span data-ttu-id="7ab68-113">가상 컴퓨터 블레이드에서 **디스크**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab68-113">On the virtual machine blade, click **Disks**.</span></span>
   4. <span data-ttu-id="7ab68-114">**디스크** 블레이드에서 **+ 데이터 디스크 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab68-114">On the **Disks** blade, click **+ Add data disk**.</span></span>
5. <span data-ttu-id="7ab68-115">새 디스크에 대한 드롭다운에서 **빈 항목 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab68-115">In the drop-down for the new disk, select **Create empty**.</span></span>
6. <span data-ttu-id="7ab68-116">**Create managed disk**(관리 디스크 만들기) 블레이드에서 디스크의 이름을 입력하고 필요에 따라 다른 설정을 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab68-116">In the **Create managed disk** blade, type in a name for the disk and adjust the other settings as necessary.</span></span> <span data-ttu-id="7ab68-117">완료하면 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab68-117">When you are done, click **Create**.</span></span>
7. <span data-ttu-id="7ab68-118">**디스크** 블레이드에서 [저장]을 클릭하여 VM에 대한 새 디스크 구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab68-118">In the **Disks** blade, click save to save the new disk configuration for the VM.</span></span>
6. <span data-ttu-id="7ab68-119">Azure가 디스크를 만들고 가상 컴퓨터에 연결하면 가상 컴퓨터의 디스크 설정의 **데이터 디스크**아래에 새 디스크가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab68-119">After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span></span>


## <a name="initialize-a-new-data-disk"></a><span data-ttu-id="7ab68-120">새 데이터 디스크 초기화</span><span class="sxs-lookup"><span data-stu-id="7ab68-120">Initialize a new data disk</span></span>

1. <span data-ttu-id="7ab68-121">VM에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab68-121">Connect to the VM.</span></span>
1. <span data-ttu-id="7ab68-122">VM 내에서 시작 메뉴를 클릭하고 **diskmgmt.msc**를 입력한 다음 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="7ab68-122">Click the start menu inside the VM and type **diskmgmt.msc** and hit **Enter**.</span></span> <span data-ttu-id="7ab68-123">그러면 디스크 관리 스냅인이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab68-123">This will start the Disk Management snap-in.</span></span>
2. <span data-ttu-id="7ab68-124">디스크 관리에서 초기화되지 않은 새 디스크가 있다고 인식하고 [디스크 초기화] 창이 팝업됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab68-124">Disk Management will recognize that you have a new, un-initialized disk and the Initialize Disk window will pop up.</span></span>
3. <span data-ttu-id="7ab68-125">새 디스크가 선택되어 있는지 확인하고 **확인**을 클릭하여 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab68-125">Make sure the new disk is selected and click **OK** to initialize it.</span></span>
4. <span data-ttu-id="7ab68-126">이제 새 디스크가 **할당되지 않음**으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="7ab68-126">The new disk will now appear as **unallocated**.</span></span> <span data-ttu-id="7ab68-127">디스크의 아무 곳이나 마우스 오른쪽 단추로 클릭하고 **새 단순 볼륨**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab68-127">Right-click anywhere on the disk and select **New simple volume**.</span></span> <span data-ttu-id="7ab68-128">**새 단순 볼륨 마법사**가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab68-128">The **New Simple Volume Wizard** will start.</span></span>
5. <span data-ttu-id="7ab68-129">모든 기본값을 유지하여 마법사를 계속 진행하고 완료하면 **마침**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab68-129">Go through the wizard, keeping all of the defaults, when you are done select **Finish**.</span></span>
6. <span data-ttu-id="7ab68-130">디스크 관리를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab68-130">Close Disk Management.</span></span>
7. <span data-ttu-id="7ab68-131">새 디스크를 사용하려면 먼저 포맷해야 한다는 팝업이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab68-131">You will get a pop-up that you need to format the new disk before you can use it.</span></span> <span data-ttu-id="7ab68-132">**디스크 포맷**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab68-132">Click **Format disk**.</span></span>
8. <span data-ttu-id="7ab68-133">**새 디스크 포맷** 대화 상자에서 설정을 확인하고 **시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab68-133">In the **Format new disk** dialog, check the settings and then click **Start**.</span></span>
9. <span data-ttu-id="7ab68-134">디스크를 포맷하면 모든 데이터가 지워진다는 경고가 표시됩니다. **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab68-134">You will get a warning that formatting the disks will erase all of the data, click **OK**.</span></span>
10. <span data-ttu-id="7ab68-135">포맷이 완료되면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab68-135">When the format is complete, click **OK**.</span></span>

## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="7ab68-136">표준 저장소와 TRIM 사용</span><span class="sxs-lookup"><span data-stu-id="7ab68-136">Use TRIM with standard storage</span></span>

<span data-ttu-id="7ab68-137">표준 저장소(HDD)를 사용하는 경우 TRIM을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab68-137">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="7ab68-138">TRIM은 디스크에서 사용되지 않는 블록을 삭제하므로 실제로 사용 중인 저장소에 대해 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab68-138">TRIM discards unused blocks on the disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="7ab68-139">큰 파일을 만들고 삭제하는 경우 비용을 절감할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab68-139">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="7ab68-140">TRIM 설정을 확인하도록 이 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab68-140">You can run this command to check the TRIM setting.</span></span> <span data-ttu-id="7ab68-141">Windows VM에서 명령 프롬프트를 열어 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab68-141">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="7ab68-142">명령이 0을 반환하는 경우 TRIM이 올바르게 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab68-142">If the command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="7ab68-143">1을 반환하는 경우, 다음 명령을 실행하여 TRIM을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab68-143">If it returns 1, run the following command to enable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

<span data-ttu-id="7ab68-144">디스크에서 데이터를 삭제한 후 TRIM으로 조각 모음을 실행하여 TRIM 작업이 제대로 플러시되는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab68-144">After deleting data from your disk, you can ensure the TRIM operations flush properly by running defrag with TRIM:</span></span>

```
defrag.exe <volume:> -l
```

<span data-ttu-id="7ab68-145">볼륨을 포맷하여 전체 볼륨이 잘리는지도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab68-145">You can also ensure the entire volume is trimmed by formatting the volume.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ab68-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7ab68-146">Next steps</span></span>
<span data-ttu-id="7ab68-147">응용 프로그램이 데이터를 저장하는 데 D: 드라이브를 사용해야 하면 [Windows 임시 디스크의 드라이브 문자를 변경](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab68-147">If you application needs to use the D: drive to store data, you can [change the drive letter of the Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
