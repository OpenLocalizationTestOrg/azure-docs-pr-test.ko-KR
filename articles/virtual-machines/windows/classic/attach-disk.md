---
title: "디스크 tooa aaaAttach 클래식 Azure VM | Microsoft Docs"
description: "Hello 클래식 배포 모델을 사용 하 여 만든 데이터 디스크 tooa Windows 가상 컴퓨터를 연결 하 고 초기화 합니다."
services: virtual-machines-windows, storage
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: be4e3e74-05bc-4527-969f-84f10a1d66a7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/21/2017
ms.author: cynthn
ms.openlocfilehash: bfe1b0fa066277d28d3862a18da4b1023cb4452d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="attach-a-data-disk-tooa-windows-virtual-machine-created-with-hello-classic-deployment-model"></a><span data-ttu-id="a2eee-103">Hello 클래식 배포 모델을 사용 하 여 만든 데이터 디스크 tooa Windows 가상 컴퓨터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-103">Attach a data disk tooa Windows virtual machine created with hello classic deployment model</span></span>
<!--
Refernce article:
    If you want toouse hello new portal, see [How tooattach a data disk tooa Windows VM in hello Azure portal](../../virtual-machines-windows-attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

<span data-ttu-id="a2eee-104">이 문서에서는 어떻게 tooattach 신규 또는 기존 디스크 hello 클래식 배포 모델 tooa Windows 가상 컴퓨터로 만든 hello를 사용 하 여 Azure 포털을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-104">This article shows you how tooattach new and existing disks created with hello Classic deployment model tooa Windows virtual machine using hello Azure portal.</span></span>

<span data-ttu-id="a2eee-105">수도 있습니다 [hello Azure 포털에서에서 데이터 디스크 tooa Linux VM 연결](../../linux/attach-disk-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-105">You can also [attach a data disk tooa Linux VM in hello Azure portal](../../linux/attach-disk-portal.md).</span></span>

<span data-ttu-id="a2eee-106">디스크를 연결하기 전에 다음과 같은 팁을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-106">Before you attach a disk, review these tips:</span></span>

* <span data-ttu-id="a2eee-107">hello 가상 컴퓨터의 hello 크기 첨부할 수 데이터 디스크 수를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-107">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="a2eee-108">자세한 내용은 [가상 컴퓨터의 크기](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a2eee-108">For details, see [Sizes for virtual machines](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="a2eee-109">프리미엄 저장소 toouse DS 시리즈 또는 GS 시리즈 가상 컴퓨터 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-109">toouse Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="a2eee-110">이 가상 컴퓨터를 사용하여 프리미엄 및 표준 저장소 계정에서 모두 디스크를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-110">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="a2eee-111">프리미엄 저장소는 특정 지역에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-111">Premium storage is available in certain regions.</span></span> <span data-ttu-id="a2eee-112">자세한 내용은 [프리미엄 저장소: Azure 가상 컴퓨터 작업을 위한 고성능 저장소](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a2eee-112">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="a2eee-113">새 디스크에 대 한 toocreate 필요 하지 않습니다 것 첫 번째 Azure가 연결 하는 경우 만들기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-113">For a new disk, you don't need toocreate it first because Azure creates it when you attach it.</span></span>

<span data-ttu-id="a2eee-114">또한 [Powershell을 사용하여 데이터 디스크를 연결](../../virtual-machines-windows-attach-disk-ps.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-114">You can also [attach a data disk using Powershell](../../virtual-machines-windows-attach-disk-ps.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a2eee-115">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-115">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span>

## <a name="find-hello-virtual-machine"></a><span data-ttu-id="a2eee-116">Hello 가상 컴퓨터를 찾을</span><span class="sxs-lookup"><span data-stu-id="a2eee-116">Find hello virtual machine</span></span>
1. <span data-ttu-id="a2eee-117">Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-117">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="a2eee-118">선택 hello hello 대시보드에 나열 된 hello 리소스에서 가상 컴퓨터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-118">Select hello virtual machine from hello resource listed on hello dashboard.</span></span>
3. <span data-ttu-id="a2eee-119">Hello 아래 왼쪽된 창에서 **설정**, 클릭 **디스크**합니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-119">In hello left pane under **Settings**, click **Disks**.</span></span>

    ![디스크 설정 열기](./media/attach-disk/virtualmachinedisks.png)

<span data-ttu-id="a2eee-121">[새 디스크](#option-1-attach-a-new-disk) 또는 [기존 디스크](#option-2-attach-an-existing-disk) 중 하나를 연결하려면 다음 지침에 따라 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-121">Continue by following instructions for attaching either a [new disk](#option-1-attach-a-new-disk) or an [existing disk](#option-2-attach-an-existing-disk).</span></span>

## <a name="option-1-attach-and-initialize-a-new-disk"></a><span data-ttu-id="a2eee-122">옵션 1: 새 디스크 연결 및 초기화</span><span class="sxs-lookup"><span data-stu-id="a2eee-122">Option 1: Attach and initialize a new disk</span></span>

1. <span data-ttu-id="a2eee-123">Hello에 **디스크** 블레이드에서 클릭 **새 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-123">On hello **Disks** blade, click **Attach new**.</span></span>
2. <span data-ttu-id="a2eee-124">Hello 기본 설정을 검토, 필요에 따라 업데이트 한 다음 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-124">Review hello default settings, update as necessary, and then click **OK**.</span></span>

   ![디스크 설정 검토](./media/attach-disk/attach-new.png)

3. <span data-ttu-id="a2eee-126">Azure hello 디스크를 만들고이 toohello 가상 컴퓨터 연결을 새 디스크 hello hello 가상 컴퓨터의 디스크 설정이 아래에 나열 됩니다 **데이터 디스크**합니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-126">After Azure creates hello disk and attaches it toohello virtual machine, hello new disk is listed in hello virtual machine's disk settings under **Data Disks**.</span></span>

### <a name="initialize-a-new-data-disk"></a><span data-ttu-id="a2eee-127">새 데이터 디스크 초기화</span><span class="sxs-lookup"><span data-stu-id="a2eee-127">Initialize a new data disk</span></span>

1. <span data-ttu-id="a2eee-128">Toohello 가상 컴퓨터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-128">Connect toohello virtual machine.</span></span> <span data-ttu-id="a2eee-129">자세한 내용은 [어떻게 tooconnect 로그온 tooan Azure 가상 컴퓨터 및 Windows를 실행](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-129">For instructions, see [How tooconnect and log on tooan Azure virtual machine running Windows](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
2. <span data-ttu-id="a2eee-130">Toohello 가상 컴퓨터에 로그인 하면 열고 **서버 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-130">After you log on toohello virtual machine, open **Server Manager**.</span></span> <span data-ttu-id="a2eee-131">Hello 왼쪽된 창에서 선택 **파일 및 저장소 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-131">In hello left pane, select **File and Storage Services**.</span></span>

    ![서버 관리자 열기](../media/attach-disk-portal/fileandstorageservices.png)

3. <span data-ttu-id="a2eee-133">**디스크**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-133">Select **Disks**.</span></span>
4. <span data-ttu-id="a2eee-134">hello **디스크** 섹션 hello 디스크를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-134">hello **Disks** section lists hello disks.</span></span> <span data-ttu-id="a2eee-135">대부분의 경우 가상 컴퓨터에는 디스크 0, 디스크 1, 디스크 2가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-135">Most often, a virtual machine has disk 0, disk 1, and disk 2.</span></span> <span data-ttu-id="a2eee-136">디스크 0는 hello 운영 체제 디스크, 디스크 1은 hello 임시 디스크 및 디스크 2는 hello 데이터 디스크가 새로 toohello 가상 컴퓨터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-136">Disk 0 is hello operating system disk, disk 1 is hello temporary disk, and disk 2 is hello data disk newly attached toohello virtual machine.</span></span> <span data-ttu-id="a2eee-137">hello 데이터 디스크 목록을 hello 파티션으로 **알 수 없는**합니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-137">hello data disk lists hello Partition as **Unknown**.</span></span>

 <span data-ttu-id="a2eee-138">Hello 디스크를 마우스 오른쪽 단추로 클릭 하 고 선택 **초기화**합니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-138">Right-click hello disk and select **Initialize**.</span></span>

5. <span data-ttu-id="a2eee-139">Hello 디스크를 초기화 하는 경우 모든 데이터가 삭제 됩니다 알림을 받으면.</span><span class="sxs-lookup"><span data-stu-id="a2eee-139">You're notified that all data will be erased when hello disk is initialized.</span></span> <span data-ttu-id="a2eee-140">클릭 **예** tooacknowledge hello 경고 및 초기화 hello 디스크.</span><span class="sxs-lookup"><span data-stu-id="a2eee-140">Click **Yes** tooacknowledge hello warning and initialize hello disk.</span></span> <span data-ttu-id="a2eee-141">완료 되 면 hello 파티션으로 나열 됩니다 **GPT**합니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-141">Once complete, hello partition will be listed as **GPT**.</span></span> <span data-ttu-id="a2eee-142">Hello 디스크를 다시 마우스 오른쪽 단추로 클릭 하 고 선택 **새 볼륨**합니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-142">Right-click hello disk again and select **New Volume**.</span></span>

6. <span data-ttu-id="a2eee-143">Hello 기본값을 사용 하는 hello 마법사를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-143">Complete hello wizard using hello default values.</span></span> <span data-ttu-id="a2eee-144">Hello 마법사가 완료 한 후에 hello **볼륨** 섹션 hello 새 볼륨을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-144">When hello wizard is done, hello **Volumes** section lists hello new volume.</span></span> <span data-ttu-id="a2eee-145">이제 hello 디스크가 온라인 상태이 고 준비 toostore 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-145">hello disk is now online and ready toostore data.</span></span>

    ![볼륨 초기화됨](./media/attach-disk/newdiskafterinitialization.png)

## <a name="option-2-attach-an-existing-disk"></a><span data-ttu-id="a2eee-147">옵션 2: 기존 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="a2eee-147">Option 2: Attach an existing disk</span></span>
1. <span data-ttu-id="a2eee-148">Hello에 **디스크** 블레이드에서 클릭 **연결 기존**합니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-148">On hello **Disks** blade, click **Attach existing**.</span></span>
2. <span data-ttu-id="a2eee-149">**기존 디스크 연결**에서 **위치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-149">Under **Attach existing disk**, click **Location**.</span></span>

   ![기존 디스크 연결](./media/attach-disk/attachexistingdisksettings.png)
3. <span data-ttu-id="a2eee-151">아래 **저장소 계정은**, hello 계정과 hello.vhd 파일을 보유 하는 컨테이너를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-151">Under **Storage accounts**, select hello account and container that holds hello .vhd file.</span></span>

   ![VHD 위치 찾기](./media/attach-disk/existdiskstorageaccountandcontainer.png)

4. <span data-ttu-id="a2eee-153">Hello.vhd 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-153">Select hello .vhd file.</span></span>
5. <span data-ttu-id="a2eee-154">아래 **기존 디스크 연결**, 방금 선택한 hello 파일 아래에 있는지 **VHD 파일**합니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-154">Under **Attach existing disk**, hello file you just selected is listed under **VHD File**.</span></span> <span data-ttu-id="a2eee-155">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-155">Click **OK**.</span></span>
6. <span data-ttu-id="a2eee-156">Azure 연결 hello 디스크 toohello 가상 컴퓨터, hello 가상 컴퓨터의 디스크 설정이 아래에 나열 됩니다 **데이터 디스크**합니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-156">After Azure attaches hello disk toohello virtual machine, it's listed in hello virtual machine's disk settings under **Data Disks**.</span></span>

## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="a2eee-157">표준 저장소와 TRIM 사용</span><span class="sxs-lookup"><span data-stu-id="a2eee-157">Use TRIM with standard storage</span></span>

<span data-ttu-id="a2eee-158">표준 저장소(HDD)를 사용하는 경우 TRIM을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-158">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="a2eee-159">TRIM 실제로 사용 하는 저장소에 대 한만 청구 됩니다 하므로 hello 디스크에 사용 하지 않는 블록을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-159">TRIM discards unused blocks on hello disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="a2eee-160">TRIM을 사용하면 큰 파일의 삭제로 발생하는 사용되지 않는 블록을 포함하여 비용을 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-160">Using TRIM can save costs, including unused blocks that result from deleting large files.</span></span>

<span data-ttu-id="a2eee-161">이 명령은 toocheck hello 트림 설정을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-161">You can run this command toocheck hello TRIM setting.</span></span> <span data-ttu-id="a2eee-162">Windows VM에서 명령 프롬프트를 열어 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-162">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="a2eee-163">Hello 명령이 0을 반환 하는 경우 TRIM 올바르게 활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-163">If hello command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="a2eee-164">1을 반환 하는 경우 다음 명령을 tooenable TRIM hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-164">If it returns 1, run hello following command tooenable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

## <a name="next-steps"></a><span data-ttu-id="a2eee-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a2eee-165">Next steps</span></span>
<span data-ttu-id="a2eee-166">응용 프로그램 toouse hello d: 드라이브 toostore 데이터를 필요한 경우 다음을 할 수 있습니다 [hello Windows 임시 디스크의 드라이브 문자 hello 변경](../../virtual-machines-windows-change-drive-letter.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a2eee-166">If your application needs toouse hello D: drive toostore data, you can [change hello drive letter of hello Windows temporary disk](../../virtual-machines-windows-change-drive-letter.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a2eee-167">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="a2eee-167">Additional resources</span></span>
[<span data-ttu-id="a2eee-168">가상 컴퓨터용 디스크 및 VHD에 대하여</span><span class="sxs-lookup"><span data-stu-id="a2eee-168">About disks and VHDs for virtual machines</span></span>](../../virtual-machines-linux-about-disks-vhds.md)
