---
title: "Windows VM에 관리되지 않는 데이터 디스크 연결 - Azure | Microsoft Docs"
description: "리소스 관리자 배포 모델을 사용하여 Azure Portal에서 Windows VM에 신규 및 기존 관리되지 않는 데이터 디스크를 연결하는 방법입니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3790fc59-7264-41df-b7a3-8d1226799885
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: c0886302c82641f8cc1a00d3972870d58ba8afb4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-attach-an-unmanaged-data-disk-to-a-windows-vm-in-the-azure-portal"></a><span data-ttu-id="bc45d-103">Azure Portal에서 Windows VM에 관리되지 않는 데이터 디스크를 연결하는 방법</span><span class="sxs-lookup"><span data-stu-id="bc45d-103">How to attach an unmanaged data disk to a Windows VM in the Azure portal</span></span>

<span data-ttu-id="bc45d-104">이 문서에서는 Azure Portal을 통해 신규 및 기존 관리되지 않는 디스크를 Windows 가상 컴퓨터에 연결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-104">This article shows you how to attach both new and existing unmanaged disks to Windows virtual machines through the Azure portal.</span></span> <span data-ttu-id="bc45d-105">또한 [PowerShell을 사용하여 데이터 디스크를 연결](./attach-disk-ps.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-105">You can also [attach a data disk using PowerShell](./attach-disk-ps.md).</span></span> <span data-ttu-id="bc45d-106">이 작업을 수행 하기 전에 다음 팁을 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="bc45d-106">Before you do this, review these tips:</span></span>

* <span data-ttu-id="bc45d-107">가상 컴퓨터의 크기로 연결할 수 있는 디스크 개수가 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-107">The size of the virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="bc45d-108">자세한 내용은 [가상 컴퓨터의 크기](sizes.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bc45d-108">For details, see [Sizes for virtual machines](sizes.md).</span></span>
* <span data-ttu-id="bc45d-109">프리미엄 저장소를 사용하려면 DS 시리즈 또는 GS 시리즈 가상 컴퓨터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-109">To use Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="bc45d-110">이 가상 컴퓨터를 사용하여 프리미엄 및 표준 저장소 계정에서 모두 디스크를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-110">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="bc45d-111">프리미엄 저장소는 특정 지역에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-111">Premium storage is available in certain regions.</span></span> <span data-ttu-id="bc45d-112">자세한 내용은 [프리미엄 저장소: Azure 가상 컴퓨터 작업을 위한 고성능 저장소](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bc45d-112">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="bc45d-113">새 디스크의 경우 Azure가 디스크를 연결할 때 생성하므로 먼저 생성하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-113">For a new disk, you don't need to create it first because Azure creates it when you attach it.</span></span>


<span data-ttu-id="bc45d-114">또한 [Powershell을 사용하여 데이터 디스크를 연결](attach-disk-ps.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-114">You can also [attach a data disk using Powershell](attach-disk-ps.md).</span></span>


## <a name="find-the-virtual-machine"></a><span data-ttu-id="bc45d-115">가상 컴퓨터 찾기</span><span class="sxs-lookup"><span data-stu-id="bc45d-115">Find the virtual machine</span></span>
1. <span data-ttu-id="bc45d-116">[Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-116">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="bc45d-117">왼쪽 메뉴에서 **가상 컴퓨터**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-117">In the menu on the left, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="bc45d-118">목록에서 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-118">Select the virtual machine from the list.</span></span>
4. <span data-ttu-id="bc45d-119">가상 컴퓨터 블레이드에서 **디스크**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-119">In the Virtual machines blade, click **Disks**.</span></span>
   
<span data-ttu-id="bc45d-120">[새 디스크](#option-1-attach-a-new-disk) 또는 [기존 디스크](#option-2-attach-an-existing-disk) 중 하나를 연결하려면 다음 지침에 따라 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-120">Continue by following instructions for attaching either a [new disk](#option-1-attach-a-new-disk) or an [existing disk](#option-2-attach-an-existing-disk).</span></span>

## <a name="option-1-attach-and-initialize-a-new-disk"></a><span data-ttu-id="bc45d-121">옵션 1: 새 디스크 연결 및 초기화</span><span class="sxs-lookup"><span data-stu-id="bc45d-121">Option 1: Attach and initialize a new disk</span></span>
1. <span data-ttu-id="bc45d-122">**디스크** 블레이드에서 **+ 데이터 디스크 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-122">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="bc45d-123">**관리되는 디스크 연결** 블레이드에서 **이름**에 디스크의 이름을 입력한 다음 **원본 유형**에서 **새로 만들기(빈 디스크)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-123">In the **Attach managed disk** blade, type a name for the disk in **Name** and then select **New (empty disk)** in **Source type**.</span></span>
3. <span data-ttu-id="bc45d-124">**저장소 컨테이너**에서 **찾아보기** 단추를 클릭하고 새 VHD를 저장할 컨테이너 및 저장소 계정으로 이동한 다음 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-124">Under **Storage container**, click the **Browse** button and browse to the storage account and container where you would like the new VHD to be stored and then click **Select**.</span></span> 
  
   ![디스크 설정 검토](./media/attach-disk-portal/attach-empty-unmanaged.png)
   
3. <span data-ttu-id="bc45d-126">데이터 디스크에 대한 설정을 마쳤으면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-126">When you are done with the settings for the data disk, click **OK**.</span></span>
4. <span data-ttu-id="bc45d-127">다시 **디스크** 블레이드에서 **저장**을 클릭하여 VM 구성에 디스크를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-127">Back in the **Disks** blade, click **Save** to add the disk to the VM configuration.</span></span>


### <a name="initialize-a-new-data-disk"></a><span data-ttu-id="bc45d-128">새 데이터 디스크 초기화</span><span class="sxs-lookup"><span data-stu-id="bc45d-128">Initialize a new data disk</span></span>

1. <span data-ttu-id="bc45d-129">가상 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-129">Connect to the virtual machine.</span></span> <span data-ttu-id="bc45d-130">자세한 내용은 [Windows를 실행하는 Azure 가상 컴퓨터에 연결하고 로그온하는 방법](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bc45d-130">For instructions, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
1. <span data-ttu-id="bc45d-131">VM 내에서 **시작** 메뉴를 클릭하고 **diskmgmt.msc**를 입력한 다음 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-131">Click the **Start** menu inside the VM and type **diskmgmt.msc** and hit **Enter**.</span></span> <span data-ttu-id="bc45d-132">그러면 디스크 관리 스냅인이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-132">This starts the Disk Management snap-in.</span></span>
2. <span data-ttu-id="bc45d-133">디스크 관리에서 초기화되지 않은 새 디스크가 있다고 인식하고 디스크 초기화 창이 팝업됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-133">Disk Management recognizes that you have a new, uninitialized disk and the Initialize Disk window will pop up.</span></span>
3. <span data-ttu-id="bc45d-134">새 디스크가 선택되어 있는지 확인하고 **확인**을 클릭하여 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-134">Make sure the new disk is selected and click **OK** to initialize it.</span></span>
4. <span data-ttu-id="bc45d-135">이제 새 디스크가 **할당되지 않음**으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-135">The new disk now appears as **unallocated**.</span></span> <span data-ttu-id="bc45d-136">디스크의 아무 곳이나 마우스 오른쪽 단추로 클릭하고 **새 단순 볼륨**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-136">Right-click anywhere on the disk and select **New simple volume**.</span></span> <span data-ttu-id="bc45d-137">**새 단순 볼륨 마법사**가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-137">The **New Simple Volume Wizard** starts.</span></span>
5. <span data-ttu-id="bc45d-138">모든 기본값을 유지하여 마법사를 계속 진행하고 완료하면 **마침**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-138">Go through the wizard, keeping all of the defaults, when you are done select **Finish**.</span></span>
6. <span data-ttu-id="bc45d-139">디스크 관리를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-139">Close Disk Management.</span></span>
7. <span data-ttu-id="bc45d-140">새 디스크를 사용하려면 먼저 포맷해야 한다는 팝업이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-140">You get a pop-up that you need to format the new disk before you can use it.</span></span> <span data-ttu-id="bc45d-141">**디스크 포맷**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-141">Click **Format disk**.</span></span>
8. <span data-ttu-id="bc45d-142">**새 디스크 포맷** 대화 상자에서 설정을 확인하고 **시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-142">In the **Format new disk** dialog, check the settings and then click **Start**.</span></span>
9. <span data-ttu-id="bc45d-143">디스크를 포맷하면 모든 데이터가 지워진다는 경고가 표시됩니다. **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-143">You get a warning that formatting the disks erases all of the data, click **OK**.</span></span>
10. <span data-ttu-id="bc45d-144">포맷이 완료되면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-144">When the format is complete, click **OK**.</span></span>


## <a name="option-2-attach-an-existing-disk"></a><span data-ttu-id="bc45d-145">옵션 2: 기존 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="bc45d-145">Option 2: Attach an existing disk</span></span>
1. <span data-ttu-id="bc45d-146">**디스크** 블레이드에서 **+ 데이터 디스크 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-146">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="bc45d-147">**관리되지 않는 디스크 연결** 블레이드의 **원본 유형**에서 **Existing blob**(기존 Blob)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-147">On the **Attach unmanaged disk** blade, in **Source type** select **Existing blob**.</span></span>

    ![디스크 설정 검토](./media/attach-disk-portal/attach-existing-unmanaged.png)

    3. <span data-ttu-id="bc45d-149">**찾아보기**를 클릭하여 기존 VHD가 있는 컨테이너 및 저장소 계정으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-149">Click **Browse** to navigate to the storage account and container where the existing VHD is located.</span></span> <span data-ttu-id="bc45d-150">VHD를 클릭한 다음 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-150">Click and the VHD and then click **Select**.</span></span>
4. <span data-ttu-id="bc45d-151">**관리되지 않는 디스크 연결** 블레이드에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-151">Click **OK** in the **Attach unmanaged disk** blade.</span></span>
5. <span data-ttu-id="bc45d-152">**디스크** 블레이드에서 **저장**을 클릭하여 VM에 대한 구성에 디스크를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-152">In the **Disks** blade, click **Save** to add the disk to the configuration for the VM.</span></span>
   


## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="bc45d-153">표준 저장소와 TRIM 사용</span><span class="sxs-lookup"><span data-stu-id="bc45d-153">Use TRIM with standard storage</span></span>

<span data-ttu-id="bc45d-154">표준 저장소(HDD)를 사용하는 경우 TRIM을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-154">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="bc45d-155">TRIM은 디스크에서 사용되지 않는 블록을 삭제하므로 실제로 사용 중인 저장소에 대해 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-155">TRIM discards unused blocks on the disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="bc45d-156">큰 파일을 만들고 삭제하는 경우 비용을 절감할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-156">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="bc45d-157">TRIM 설정을 확인하도록 이 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-157">You can run this command to check the TRIM setting.</span></span> <span data-ttu-id="bc45d-158">Windows VM에서 명령 프롬프트를 열어 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-158">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="bc45d-159">명령이 0을 반환하는 경우 TRIM이 올바르게 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-159">If the command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="bc45d-160">1을 반환하는 경우, 다음 명령을 실행하여 TRIM을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-160">If it returns 1, run the following command to enable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

<span data-ttu-id="bc45d-161">디스크에서 데이터를 삭제한 후 TRIM으로 조각 모음을 실행하여 TRIM 작업이 제대로 플러시되는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-161">After deleting data from your disk, you can ensure the TRIM operations flush properly by running defrag with TRIM:</span></span>

```
defrag.exe <volume:> -l
```

<span data-ttu-id="bc45d-162">볼륨을 포맷하여 전체 볼륨이 잘리는지도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-162">You can also ensure the entire volume is trimmed by formatting the volume.</span></span>


## <a name="next-steps"></a><span data-ttu-id="bc45d-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bc45d-163">Next steps</span></span>
<span data-ttu-id="bc45d-164">응용 프로그램이 데이터를 저장하는 데 D: 드라이브를 사용해야 하면 [Windows 임시 디스크의 드라이브 문자를 변경](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc45d-164">If you application needs to use the D: drive to store data, you can [change the drive letter of the Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

