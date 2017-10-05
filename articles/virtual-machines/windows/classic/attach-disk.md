---
title: "클래식 Azure VM에 디스크 연결 | Microsoft Docs"
description: "클래식 배포 모델을 사용하여 만든 Windows 가상 컴퓨터에 데이터 디스크를 연결하고 초기화합니다."
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
ms.openlocfilehash: 087d5cda354f6e1780bddd3725859444177abd16
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="attach-a-data-disk-to-a-windows-virtual-machine-created-with-the-classic-deployment-model"></a><span data-ttu-id="aec3f-103">클래식 배포 모델을 사용하여 만든 Windows 가상 컴퓨터에 데이터 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="aec3f-103">Attach a data disk to a Windows virtual machine created with the classic deployment model</span></span>
<!--
Refernce article:
    If you want to use the new portal, see [How to attach a data disk to a Windows VM in the Azure portal](../../virtual-machines-windows-attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

<span data-ttu-id="aec3f-104">이 문서에서는 Azure Portal을 사용하여 클래식 배포 모델에서 만든 신규 및 기존 디스크를 Windows 가상 컴퓨터에 연결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-104">This article shows you how to attach new and existing disks created with the Classic deployment model to a Windows virtual machine using the Azure portal.</span></span>

<span data-ttu-id="aec3f-105">또한 [Azure 포털에서 Linux VM에 데이터 디스크를 연결](../../linux/attach-disk-portal.md)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-105">You can also [attach a data disk to a Linux VM in the Azure portal](../../linux/attach-disk-portal.md).</span></span>

<span data-ttu-id="aec3f-106">디스크를 연결하기 전에 다음과 같은 팁을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-106">Before you attach a disk, review these tips:</span></span>

* <span data-ttu-id="aec3f-107">가상 컴퓨터의 크기로 연결할 수 있는 디스크 개수가 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-107">The size of the virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="aec3f-108">자세한 내용은 [가상 컴퓨터의 크기](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aec3f-108">For details, see [Sizes for virtual machines](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="aec3f-109">프리미엄 저장소를 사용하려면 DS 시리즈 또는 GS 시리즈 가상 컴퓨터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-109">To use Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="aec3f-110">이 가상 컴퓨터를 사용하여 프리미엄 및 표준 저장소 계정에서 모두 디스크를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-110">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="aec3f-111">프리미엄 저장소는 특정 지역에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-111">Premium storage is available in certain regions.</span></span> <span data-ttu-id="aec3f-112">자세한 내용은 [프리미엄 저장소: Azure 가상 컴퓨터 작업을 위한 고성능 저장소](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aec3f-112">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="aec3f-113">새 디스크의 경우 Azure가 디스크를 연결할 때 생성하므로 먼저 생성하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-113">For a new disk, you don't need to create it first because Azure creates it when you attach it.</span></span>

<span data-ttu-id="aec3f-114">또한 [Powershell을 사용하여 데이터 디스크를 연결](../../virtual-machines-windows-attach-disk-ps.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-114">You can also [attach a data disk using Powershell](../../virtual-machines-windows-attach-disk-ps.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aec3f-115">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-115">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span>

## <a name="find-the-virtual-machine"></a><span data-ttu-id="aec3f-116">가상 컴퓨터 찾기</span><span class="sxs-lookup"><span data-stu-id="aec3f-116">Find the virtual machine</span></span>
1. <span data-ttu-id="aec3f-117">[Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-117">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="aec3f-118">대시보드에 나열된 리소스에서 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-118">Select the virtual machine from the resource listed on the dashboard.</span></span>
3. <span data-ttu-id="aec3f-119">**설정** 아래 왼쪽 창에서 **디스크**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-119">In the left pane under **Settings**, click **Disks**.</span></span>

    ![디스크 설정 열기](./media/attach-disk/virtualmachinedisks.png)

<span data-ttu-id="aec3f-121">[새 디스크](#option-1-attach-a-new-disk) 또는 [기존 디스크](#option-2-attach-an-existing-disk) 중 하나를 연결하려면 다음 지침에 따라 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-121">Continue by following instructions for attaching either a [new disk](#option-1-attach-a-new-disk) or an [existing disk](#option-2-attach-an-existing-disk).</span></span>

## <a name="option-1-attach-and-initialize-a-new-disk"></a><span data-ttu-id="aec3f-122">옵션 1: 새 디스크 연결 및 초기화</span><span class="sxs-lookup"><span data-stu-id="aec3f-122">Option 1: Attach and initialize a new disk</span></span>

1. <span data-ttu-id="aec3f-123">**디스크** 블레이드에서 **새 연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-123">On the **Disks** blade, click **Attach new**.</span></span>
2. <span data-ttu-id="aec3f-124">기본 설정을 검토하고 필요에 따라 업데이트한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-124">Review the default settings, update as necessary, and then click **OK**.</span></span>

   ![디스크 설정 검토](./media/attach-disk/attach-new.png)

3. <span data-ttu-id="aec3f-126">Azure가 디스크를 만들고 가상 컴퓨터에 연결하면 가상 컴퓨터의 디스크 설정의 **데이터 디스크**아래에 새 디스크가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-126">After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span></span>

### <a name="initialize-a-new-data-disk"></a><span data-ttu-id="aec3f-127">새 데이터 디스크 초기화</span><span class="sxs-lookup"><span data-stu-id="aec3f-127">Initialize a new data disk</span></span>

1. <span data-ttu-id="aec3f-128">가상 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-128">Connect to the virtual machine.</span></span> <span data-ttu-id="aec3f-129">지침은 [Windows를 실행하는 Azure 가상 컴퓨터에 연결하고 로그온하는 방법](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aec3f-129">For instructions, see [How to connect and log on to an Azure virtual machine running Windows](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
2. <span data-ttu-id="aec3f-130">가상 컴퓨터에 로그온한 후 **Server Manager**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-130">After you log on to the virtual machine, open **Server Manager**.</span></span> <span data-ttu-id="aec3f-131">왼쪽 창에서 **파일 및 저장소 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-131">In the left pane, select **File and Storage Services**.</span></span>

    ![서버 관리자 열기](../media/attach-disk-portal/fileandstorageservices.png)

3. <span data-ttu-id="aec3f-133">**디스크**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-133">Select **Disks**.</span></span>
4. <span data-ttu-id="aec3f-134">**디스크** 섹션은 디스크를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-134">The **Disks** section lists the disks.</span></span> <span data-ttu-id="aec3f-135">대부분의 경우 가상 컴퓨터에는 디스크 0, 디스크 1, 디스크 2가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-135">Most often, a virtual machine has disk 0, disk 1, and disk 2.</span></span> <span data-ttu-id="aec3f-136">디스크 0은 운영 체제 디스크이고, 디스크 1은 임시 디스크이며, 디스크 2는 가상 컴퓨터에 새로 연결한 데이터 디스크입니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-136">Disk 0 is the operating system disk, disk 1 is the temporary disk, and disk 2 is the data disk newly attached to the virtual machine.</span></span> <span data-ttu-id="aec3f-137">데이터 디스크는 파티션을 **알 수 없음**으로 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-137">The data disk lists the Partition as **Unknown**.</span></span>

 <span data-ttu-id="aec3f-138">디스크를 마우스 오른쪽 단추로 클릭한 다음 **초기화**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-138">Right-click the disk and select **Initialize**.</span></span>

5. <span data-ttu-id="aec3f-139">디스크가 초기화 될 때 모든 데이터를 삭제된다고 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-139">You're notified that all data will be erased when the disk is initialized.</span></span> <span data-ttu-id="aec3f-140">**예** 를 클릭하여 경고를 확인하고 디스크를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-140">Click **Yes** to acknowledge the warning and initialize the disk.</span></span> <span data-ttu-id="aec3f-141">완료되면 파티션이 **GPT**로 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-141">Once complete, the partition will be listed as **GPT**.</span></span> <span data-ttu-id="aec3f-142">디스크를 다시 마우스 오른쪽 단추로 클릭하고 **새 볼륨**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-142">Right-click the disk again and select **New Volume**.</span></span>

6. <span data-ttu-id="aec3f-143">기본값을 사용하여 마법사를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-143">Complete the wizard using the default values.</span></span> <span data-ttu-id="aec3f-144">마법사를 완료하면 새 볼륨이 **볼륨** 섹션에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-144">When the wizard is done, the **Volumes** section lists the new volume.</span></span> <span data-ttu-id="aec3f-145">이제 디스크가 온라인 상태이며 데이터를 저장할 준비가 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-145">The disk is now online and ready to store data.</span></span>

    ![볼륨 초기화됨](./media/attach-disk/newdiskafterinitialization.png)

## <a name="option-2-attach-an-existing-disk"></a><span data-ttu-id="aec3f-147">옵션 2: 기존 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="aec3f-147">Option 2: Attach an existing disk</span></span>
1. <span data-ttu-id="aec3f-148">**디스크** 블레이드에서 **기존 연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-148">On the **Disks** blade, click **Attach existing**.</span></span>
2. <span data-ttu-id="aec3f-149">**기존 디스크 연결**에서 **위치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-149">Under **Attach existing disk**, click **Location**.</span></span>

   ![기존 디스크 연결](./media/attach-disk/attachexistingdisksettings.png)
3. <span data-ttu-id="aec3f-151">**저장소 계정**에서 계정 및 .vhd 파일을 보관하는 컨테이너를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-151">Under **Storage accounts**, select the account and container that holds the .vhd file.</span></span>

   ![VHD 위치 찾기](./media/attach-disk/existdiskstorageaccountandcontainer.png)

4. <span data-ttu-id="aec3f-153">.vhd 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-153">Select the .vhd file.</span></span>
5. <span data-ttu-id="aec3f-154">**기존 디스크 연결**에서 방금 선택한 파일이 **VHD 파일** 아래에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-154">Under **Attach existing disk**, the file you just selected is listed under **VHD File**.</span></span> <span data-ttu-id="aec3f-155">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-155">Click **OK**.</span></span>
6. <span data-ttu-id="aec3f-156">Azure가 디스크를 가상 컴퓨터에 연결한 후 가상 컴퓨터의 디스크 설정의 **데이터 디스크**아래에 해당 디스크가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-156">After Azure attaches the disk to the virtual machine, it's listed in the virtual machine's disk settings under **Data Disks**.</span></span>

## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="aec3f-157">표준 저장소와 TRIM 사용</span><span class="sxs-lookup"><span data-stu-id="aec3f-157">Use TRIM with standard storage</span></span>

<span data-ttu-id="aec3f-158">표준 저장소(HDD)를 사용하는 경우 TRIM을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-158">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="aec3f-159">TRIM은 디스크에서 사용되지 않는 블록을 삭제하므로 실제로 사용 중인 저장소에 대해 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-159">TRIM discards unused blocks on the disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="aec3f-160">TRIM을 사용하면 큰 파일의 삭제로 발생하는 사용되지 않는 블록을 포함하여 비용을 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-160">Using TRIM can save costs, including unused blocks that result from deleting large files.</span></span>

<span data-ttu-id="aec3f-161">TRIM 설정을 확인하도록 이 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-161">You can run this command to check the TRIM setting.</span></span> <span data-ttu-id="aec3f-162">Windows VM에서 명령 프롬프트를 열어 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-162">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="aec3f-163">명령이 0을 반환하는 경우 TRIM이 올바르게 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-163">If the command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="aec3f-164">1을 반환하는 경우, 다음 명령을 실행하여 TRIM을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-164">If it returns 1, run the following command to enable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

## <a name="next-steps"></a><span data-ttu-id="aec3f-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="aec3f-165">Next steps</span></span>
<span data-ttu-id="aec3f-166">응용 프로그램이 데이터를 저장하는 데 D: 드라이브를 사용해야 하면 [Windows 임시 디스크의 드라이브 문자를 변경](../../virtual-machines-windows-change-drive-letter.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aec3f-166">If your application needs to use the D: drive to store data, you can [change the drive letter of the Windows temporary disk](../../virtual-machines-windows-change-drive-letter.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="aec3f-167">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="aec3f-167">Additional resources</span></span>
[<span data-ttu-id="aec3f-168">가상 컴퓨터용 디스크 및 VHD에 대하여</span><span class="sxs-lookup"><span data-stu-id="aec3f-168">About disks and VHDs for virtual machines</span></span>](../../virtual-machines-linux-about-disks-vhds.md)
