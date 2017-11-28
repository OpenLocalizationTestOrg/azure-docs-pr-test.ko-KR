---
title: "관리 되지 않는 데이터 디스크 tooa Windows VM-Azure aaaAttach | Microsoft Docs"
description: "어떻게 tooattach 새로운 또는 기존의 관리 되지 않는 데이터 디스크 tooa Windows VM에 Azure 포털 사용 하 여 hello hello 리소스 관리자 배포 모델입니다."
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
ms.openlocfilehash: 923a6663974143bf359970f9b0eb0d36cabcba9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-an-unmanaged-data-disk-tooa-windows-vm-in-hello-azure-portal"></a><span data-ttu-id="1ebe4-103">Tooattach 관리 되지 않는 데이터 hello Azure 포털에서에서 tooa Windows VM 디스크 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1ebe4-103">How tooattach an unmanaged data disk tooa Windows VM in hello Azure portal</span></span>

<span data-ttu-id="1ebe4-104">이 문서에서는 hello Azure 포털을 통해 tooWindows 가상 컴퓨터 디스크 tooattach 신규 및 기존 관리 되지 않는 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-104">This article shows you how tooattach both new and existing unmanaged disks tooWindows virtual machines through hello Azure portal.</span></span> <span data-ttu-id="1ebe4-105">또한 [PowerShell을 사용하여 데이터 디스크를 연결](./attach-disk-ps.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-105">You can also [attach a data disk using PowerShell](./attach-disk-ps.md).</span></span> <span data-ttu-id="1ebe4-106">이 작업을 수행 하기 전에 다음 팁을 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-106">Before you do this, review these tips:</span></span>

* <span data-ttu-id="1ebe4-107">hello 가상 컴퓨터의 hello 크기 첨부할 수 데이터 디스크 수를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-107">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="1ebe4-108">자세한 내용은 [가상 컴퓨터의 크기](sizes.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-108">For details, see [Sizes for virtual machines](sizes.md).</span></span>
* <span data-ttu-id="1ebe4-109">프리미엄 저장소 toouse DS 시리즈 또는 GS 시리즈 가상 컴퓨터 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-109">toouse Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="1ebe4-110">이 가상 컴퓨터를 사용하여 프리미엄 및 표준 저장소 계정에서 모두 디스크를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-110">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="1ebe4-111">프리미엄 저장소는 특정 지역에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-111">Premium storage is available in certain regions.</span></span> <span data-ttu-id="1ebe4-112">자세한 내용은 [프리미엄 저장소: Azure 가상 컴퓨터 작업을 위한 고성능 저장소](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-112">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="1ebe4-113">새 디스크에 대 한 toocreate 필요 하지 않습니다 것 첫 번째 Azure가 연결 하는 경우 만들기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-113">For a new disk, you don't need toocreate it first because Azure creates it when you attach it.</span></span>


<span data-ttu-id="1ebe4-114">또한 [Powershell을 사용하여 데이터 디스크를 연결](attach-disk-ps.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-114">You can also [attach a data disk using Powershell](attach-disk-ps.md).</span></span>


## <a name="find-hello-virtual-machine"></a><span data-ttu-id="1ebe4-115">Hello 가상 컴퓨터를 찾을</span><span class="sxs-lookup"><span data-stu-id="1ebe4-115">Find hello virtual machine</span></span>
1. <span data-ttu-id="1ebe4-116">Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-116">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1ebe4-117">Hello hello 왼쪽 메뉴를 클릭 **가상 컴퓨터**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-117">In hello menu on hello left, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="1ebe4-118">Hello 목록에서 hello 가상 컴퓨터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-118">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="1ebe4-119">Hello 가상 컴퓨터 블레이드 클릭 **디스크**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-119">In hello Virtual machines blade, click **Disks**.</span></span>
   
<span data-ttu-id="1ebe4-120">[새 디스크](#option-1-attach-a-new-disk) 또는 [기존 디스크](#option-2-attach-an-existing-disk) 중 하나를 연결하려면 다음 지침에 따라 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-120">Continue by following instructions for attaching either a [new disk](#option-1-attach-a-new-disk) or an [existing disk](#option-2-attach-an-existing-disk).</span></span>

## <a name="option-1-attach-and-initialize-a-new-disk"></a><span data-ttu-id="1ebe4-121">옵션 1: 새 디스크 연결 및 초기화</span><span class="sxs-lookup"><span data-stu-id="1ebe4-121">Option 1: Attach and initialize a new disk</span></span>
1. <span data-ttu-id="1ebe4-122">Hello에 **디스크** 블레이드에서 클릭 **+ 추가 데이터 디스크**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-122">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="1ebe4-123">Hello에 **연결 관리 되는 디스크** 블레이드에서 hello 디스크의 이름 입력 **이름** 선택한 후 **새로 만들기 (빈 디스크)** 에 **소스 형식**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-123">In hello **Attach managed disk** blade, type a name for hello disk in **Name** and then select **New (empty disk)** in **Source type**.</span></span>
3. <span data-ttu-id="1ebe4-124">아래 **저장소 컨테이너**, hello 클릭 **찾아보기** 단추 및 toohello 저장소 계정 및 컨테이너를 hello 새 VHD toobe 저장 선택한 다음 클릭 찾아보기 **선택**.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-124">Under **Storage container**, click hello **Browse** button and browse toohello storage account and container where you would like hello new VHD toobe stored and then click **Select**.</span></span> 
  
   ![디스크 설정 검토](./media/attach-disk-portal/attach-empty-unmanaged.png)
   
3. <span data-ttu-id="1ebe4-126">Hello 데이터 디스크에 대 한 hello 설정을 사용 하 여 작업을 완료 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-126">When you are done with hello settings for hello data disk, click **OK**.</span></span>
4. <span data-ttu-id="1ebe4-127">Hello에 다시 **디스크** 블레이드에서 클릭 **저장** tooadd hello 디스크 toohello VM 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-127">Back in hello **Disks** blade, click **Save** tooadd hello disk toohello VM configuration.</span></span>


### <a name="initialize-a-new-data-disk"></a><span data-ttu-id="1ebe4-128">새 데이터 디스크 초기화</span><span class="sxs-lookup"><span data-stu-id="1ebe4-128">Initialize a new data disk</span></span>

1. <span data-ttu-id="1ebe4-129">Toohello 가상 컴퓨터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-129">Connect toohello virtual machine.</span></span> <span data-ttu-id="1ebe4-130">자세한 내용은 [어떻게 tooconnect 로그온 tooan Azure 가상 컴퓨터 및 Windows를 실행](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-130">For instructions, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
1. <span data-ttu-id="1ebe4-131">Hello 클릭 **시작** hello VM 및 형식 내부 메뉴 **diskmgmt.msc** 적중 및 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-131">Click hello **Start** menu inside hello VM and type **diskmgmt.msc** and hit **Enter**.</span></span> <span data-ttu-id="1ebe4-132">Hello 디스크 관리 스냅인 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-132">This starts hello Disk Management snap-in.</span></span>
2. <span data-ttu-id="1ebe4-133">디스크 관리 새, 초기화 되지 않은 디스크 hello 디스크 초기화 창이 팝업 됩니다 인식 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-133">Disk Management recognizes that you have a new, uninitialized disk and hello Initialize Disk window will pop up.</span></span>
3. <span data-ttu-id="1ebe4-134">Hello 새 디스크가 선택 되어 있는지 확인 하 고 클릭 **확인** tooinitialize 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-134">Make sure hello new disk is selected and click **OK** tooinitialize it.</span></span>
4. <span data-ttu-id="1ebe4-135">hello 새 디스크로 나타납니다으로 **할당 되지 않은**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-135">hello new disk now appears as **unallocated**.</span></span> <span data-ttu-id="1ebe4-136">Hello 디스크에서 아무 곳 이나 마우스 오른쪽 단추로 클릭 하 고 선택 **새 단순 볼륨**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-136">Right-click anywhere on hello disk and select **New simple volume**.</span></span> <span data-ttu-id="1ebe4-137">hello **새 단순 볼륨 마법사** 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-137">hello **New Simple Volume Wizard** starts.</span></span>
5. <span data-ttu-id="1ebe4-138">선택 작업이 완료 되 면 hello 기본값을 유지 하는 hello 마법사를 통해 이동 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-138">Go through hello wizard, keeping all of hello defaults, when you are done select **Finish**.</span></span>
6. <span data-ttu-id="1ebe4-139">디스크 관리를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-139">Close Disk Management.</span></span>
7. <span data-ttu-id="1ebe4-140">있는 팝업 하 게 사용 하려면 먼저 tooformat hello에 대 한 새 디스크가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-140">You get a pop-up that you need tooformat hello new disk before you can use it.</span></span> <span data-ttu-id="1ebe4-141">**디스크 포맷**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-141">Click **Format disk**.</span></span>
8. <span data-ttu-id="1ebe4-142">Hello에 **새 디스크를 포맷** 검사 hello 설정, 클릭 한 다음 대화 상자, **시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-142">In hello **Format new disk** dialog, check hello settings and then click **Start**.</span></span>
9. <span data-ttu-id="1ebe4-143">경고가 있는지 hello 데이터를 모두 지웁니다 hello 디스크 포맷, 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-143">You get a warning that formatting hello disks erases all of hello data, click **OK**.</span></span>
10. <span data-ttu-id="1ebe4-144">Hello 포맷이 완료 되 면 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-144">When hello format is complete, click **OK**.</span></span>


## <a name="option-2-attach-an-existing-disk"></a><span data-ttu-id="1ebe4-145">옵션 2: 기존 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="1ebe4-145">Option 2: Attach an existing disk</span></span>
1. <span data-ttu-id="1ebe4-146">Hello에 **디스크** 블레이드에서 클릭 **+ 추가 데이터 디스크**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-146">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="1ebe4-147">Hello에 **연결 관리 되지 않는 디스크** 블레이드, **소스 형식** 선택 **기존 blob**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-147">On hello **Attach unmanaged disk** blade, in **Source type** select **Existing blob**.</span></span>

    ![디스크 설정 검토](./media/attach-disk-portal/attach-existing-unmanaged.png)

    3. <span data-ttu-id="1ebe4-149">클릭 **찾아보기** toonavigate toohello 저장소 계정 및 컨테이너 hello 기존 VHD의 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-149">Click **Browse** toonavigate toohello storage account and container where hello existing VHD is located.</span></span> <span data-ttu-id="1ebe4-150">클릭 하 고 VHD hello 한 다음 클릭 **선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-150">Click and hello VHD and then click **Select**.</span></span>
4. <span data-ttu-id="1ebe4-151">클릭 **확인** hello에 **연결 관리 되지 않는 디스크** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-151">Click **OK** in hello **Attach unmanaged disk** blade.</span></span>
5. <span data-ttu-id="1ebe4-152">Hello에 **디스크** 블레이드에서 클릭 **저장** hello VM tooadd hello 디스크 toohello 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-152">In hello **Disks** blade, click **Save** tooadd hello disk toohello configuration for hello VM.</span></span>
   


## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="1ebe4-153">표준 저장소와 TRIM 사용</span><span class="sxs-lookup"><span data-stu-id="1ebe4-153">Use TRIM with standard storage</span></span>

<span data-ttu-id="1ebe4-154">표준 저장소(HDD)를 사용하는 경우 TRIM을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-154">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="1ebe4-155">TRIM 실제로 사용 하는 저장소에 대 한만 청구 됩니다 하므로 hello 디스크에 사용 하지 않는 블록을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-155">TRIM discards unused blocks on hello disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="1ebe4-156">큰 파일을 만들고 삭제하는 경우 비용을 절감할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-156">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="1ebe4-157">이 명령은 toocheck hello 트림 설정을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-157">You can run this command toocheck hello TRIM setting.</span></span> <span data-ttu-id="1ebe4-158">Windows VM에서 명령 프롬프트를 열어 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-158">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="1ebe4-159">Hello 명령이 0을 반환 하는 경우 TRIM 올바르게 활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-159">If hello command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="1ebe4-160">1을 반환 하는 경우 다음 명령을 tooenable TRIM hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-160">If it returns 1, run hello following command tooenable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

<span data-ttu-id="1ebe4-161">디스크에서 데이터를 삭제 한 후 TRIM으로 조각 모음 hello 자르기 작업을 실행 하 여 제대로 플러시 되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-161">After deleting data from your disk, you can ensure hello TRIM operations flush properly by running defrag with TRIM:</span></span>

```
defrag.exe <volume:> -l
```

<span data-ttu-id="1ebe4-162">Hello 볼륨을 포맷 하 여 hello 전체 볼륨을 잘라내는 보장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-162">You can also ensure hello entire volume is trimmed by formatting hello volume.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1ebe4-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1ebe4-163">Next steps</span></span>
<span data-ttu-id="1ebe4-164">응용 프로그램에 toouse hello d: 드라이브 toostore 데이터가 필요 하면 [hello Windows 임시 디스크의 드라이브 문자 hello 변경](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="1ebe4-164">If you application needs toouse hello D: drive toostore data, you can [change hello drive letter of hello Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

