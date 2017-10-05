---
title: "Azure Portal에서 Windows 문제 해결 VM 사용 | Microsoft Docs"
description: "Azure Portal을 사용하여 OS 디스크를 복구 VM에 연결함으로써 Azure에서 Windows 가상 컴퓨터 문제를 해결하는 방법을 알아봅니다."
services: virtual-machines-windows
documentationCenter: 
authors: genlin
manager: timlt
editor: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 2c1524949931d69d7553d284bb92c550a61c521a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-a-windows-vm-by-attaching-the-os-disk-to-a-recovery-vm-using-the-azure-portal"></a><span data-ttu-id="d6983-103">Azure Portal을 사용하여 OS 디스크를 복구 VM에 연결함으로써 Windows VM 문제 해결</span><span class="sxs-lookup"><span data-stu-id="d6983-103">Troubleshoot a Windows VM by attaching the OS disk to a recovery VM using the Azure portal</span></span>
<span data-ttu-id="d6983-104">Azure에서 Windows VM(가상 컴퓨터)에 부팅 또는 디스크 오류가 발생하는 경우 가상 하드 디스크에서 바로 문제 해결 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-104">If your Windows virtual machine (VM) in Azure encounters a boot or disk error, you may need to perform troubleshooting steps on the virtual hard disk itself.</span></span> <span data-ttu-id="d6983-105">일반적인 예로는 응용 프로그램 업데이트가 실패하여 VM이 성공적으로 부팅되지 않는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-105">A common example would be a failed application update that prevents the VM from being able to boot successfully.</span></span> <span data-ttu-id="d6983-106">이 문서에는 가상 하드 디스크를 다른 Windows VM에 연결하여 모든 오류를 수정한 후 원래 VM을 다시 만들기 위해 Azure Portal을 사용하는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-106">This article details how to use the Azure portal to connect your virtual hard disk to another Windows VM to fix any errors, then re-create your original VM.</span></span>

## <a name="recovery-process-overview"></a><span data-ttu-id="d6983-107">복구 프로세스 개요</span><span class="sxs-lookup"><span data-stu-id="d6983-107">Recovery process overview</span></span>
<span data-ttu-id="d6983-108">문제 해결 프로세스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-108">The troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="d6983-109">문제가 발생하는 VM을 삭제하여, 가상 하드 디스크를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-109">Delete the VM encountering issues, keeping the virtual hard disks.</span></span>
2. <span data-ttu-id="d6983-110">문제 해결을 위해 가상 하드 디스크를 다른 Windows VM에 연결하고 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-110">Attach and mount the virtual hard disk to another Windows VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="d6983-111">문제 해결 VM에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-111">Connect to the troubleshooting VM.</span></span> <span data-ttu-id="d6983-112">파일을 편집하거나 도구를 실행하여 원래의 가상 하드 디스크에서 문제를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-112">Edit files or run any tools to fix issues on the original virtual hard disk.</span></span>
4. <span data-ttu-id="d6983-113">문제 해결 VM에서 가상 하드 디스크를 탑재 해제하고 분리합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-113">Unmount and detach the virtual hard disk from the troubleshooting VM.</span></span>
5. <span data-ttu-id="d6983-114">원래 가상 하드 디스크를 사용하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-114">Create a VM using the original virtual hard disk.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="d6983-115">부팅 문제 확인</span><span class="sxs-lookup"><span data-stu-id="d6983-115">Determine boot issues</span></span>
<span data-ttu-id="d6983-116">VM이 올바르게 부팅할 수 없는 원인을 확인하려면 부팅 진단 VM 스크린샷을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-116">To determine why your VM is not able to boot correctly, examine the boot diagnostics VM screenshot.</span></span> <span data-ttu-id="d6983-117">일반적인 예로는 응용 프로그램 업데이트가 실패하거나 기본 가상 하드 디스크를 삭제 또는 이동하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-117">A common example would be a failed application update, or an underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="d6983-118">포털에서 VM을 선택하고 **지원+문제 해결** 섹션까지 아래로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-118">Select your VM in the portal and then scroll down to the **Support + Troubleshooting** section.</span></span> <span data-ttu-id="d6983-119">스크린샷을 보려면 **부팅 진단**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-119">Click **Boot diagnostics** to view the screenshot.</span></span> <span data-ttu-id="d6983-120">VM에서 문제가 발생하는 이유를 확인하는 데 도움이 되는 특정 오류 메시지 또는 오류 코드를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-120">Note any specific error messages or error codes to help determine why the VM is encountering an issue.</span></span> <span data-ttu-id="d6983-121">다음 예는 VM이 서비스가 중지되기를 기다리는 상태를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-121">The following example shows a VM waiting on stopping services:</span></span>

![VM 부팅 진단 콘솔 로그 보기](./media/troubleshoot-recovery-disks-portal/screenshot-error.png)

<span data-ttu-id="d6983-123">**스크린샷**을 클릭하여 VM 스크린샷 캡처를 다운로드할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-123">You can also click **Screenshot** to download a capture of the VM screenshot.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="d6983-124">기존 가상 하드 디스크 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="d6983-124">View existing virtual hard disk details</span></span>
<span data-ttu-id="d6983-125">가상 하드 디스크를 다른 VM에 연결하기 전에 가상 하드 디스크(VHD)의 이름을 식별해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-125">Before you can attach your virtual hard disk to another VM, you need to identify the name of the virtual hard disk (VHD).</span></span> 

<span data-ttu-id="d6983-126">포털에서 리소스 그룹을 선택하고 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-126">Select your resource group from the portal, then select your storage account.</span></span> <span data-ttu-id="d6983-127">**Blob**를 다음 예제와 같이 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-127">Click **Blobs**, as in the following example:</span></span>

![저장소 Blob 선택](./media/troubleshoot-recovery-disks-portal/storage-account-overview.png)

<span data-ttu-id="d6983-129">일반적으로 가상 하드 디스크를 저장하는 **vhd**로 명명된 컨테이너가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-129">Typically you have a container named **vhds** that stores your virtual hard disks.</span></span> <span data-ttu-id="d6983-130">가상 하드 디스크의 목록을 보려면 컨테이너를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-130">Select the container to view a list of virtual hard disks.</span></span> <span data-ttu-id="d6983-131">VHD의 이름을 적어둡니다(접두사는 일반적으로 VM의 이름임).</span><span class="sxs-lookup"><span data-stu-id="d6983-131">Note the name of your VHD (the prefix is usually the name of your VM):</span></span>

![저장소 컨테이너에서 VHD 식별](./media/troubleshoot-recovery-disks-portal/storage-container.png)

<span data-ttu-id="d6983-133">목록에서 기존 가상 하드 디스크를 선택하고 다음 단계에 사용하기 위해 URL을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-133">Select your existing virtual hard disk from the list and copy the URL for use in the following steps:</span></span>

![기존 가상 하드 디스크 URL 복사](./media/troubleshoot-recovery-disks-portal/copy-vhd-url.png)


## <a name="delete-existing-vm"></a><span data-ttu-id="d6983-135">기존 VM 삭제</span><span class="sxs-lookup"><span data-stu-id="d6983-135">Delete existing VM</span></span>
<span data-ttu-id="d6983-136">가상 하드 디스크와 VM은 Azure의 두 가지 별개의 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-136">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="d6983-137">가상 하드 디스크에는 운영 체제 자체, 응용 프로그램 및 구성이 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-137">A virtual hard disk is where the operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="d6983-138">VM 자체는 크기 또는 위치를 정의하고 가상 하드 디스크 또는 가상 네트워크 인터페이스 카드(NIC)와 같은 리소스를 참조하는 메타데이터일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-138">The VM itself is just metadata that defines the size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="d6983-139">각 가상 하드 디스크에는 VM에 연결할 때 할당된 임대가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-139">Each virtual hard disk has a lease assigned when attached to a VM.</span></span> <span data-ttu-id="d6983-140">VM을 실행하는 동안에도 데이터 디스크를 연결하고 분리할 수 있지만, VM 리소스를 삭제하지 않는 한 OS 디스크를 분리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-140">Although data disks can be attached and detached even while the VM is running, the OS disk cannot be detached unless the VM resource is deleted.</span></span> <span data-ttu-id="d6983-141">해당 VM이 중지 및 할당 취소된 상태에 있을 때에도 임대는 OS 디스크와 VM을 계속 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-141">The lease continues to associate the OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="d6983-142">VM을 복구하는 첫 번째 단계는 자체 VM 리소스를 삭제하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-142">The first step to recover your VM is to delete the VM resource itself.</span></span> <span data-ttu-id="d6983-143">VM을 삭제하면 가상 하드 디스크는 저장소 계정에 남게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-143">Deleting the VM leaves the virtual hard disks in your storage account.</span></span> <span data-ttu-id="d6983-144">VM을 삭제한 후 가상 하드 디스크를 다른 VM에 연결하여 문제와 오류를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-144">After the VM is deleted, you attach the virtual hard disk to another VM to troubleshoot and resolve the errors.</span></span>

<span data-ttu-id="d6983-145">포털에서 VM을 선택한 다음 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-145">Select your VM in the portal, then click **Delete**:</span></span>

![부팅 오류를 보여 주는 VM 부팅 진단 스크린샷](./media/troubleshoot-recovery-disks-portal/stop-delete-vm.png)

<span data-ttu-id="d6983-147">가상 하드 디스크를 다른 VM에 연결 하기 전에 VM이 삭제 작업을 끝낼 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-147">Wait until the VM has finished deleting before you attach the virtual hard disk to another VM.</span></span> <span data-ttu-id="d6983-148">VM과 연결하는 가상 하드 디스크의 임대는 가상 하드 디스크를 다른 VM에 연결하기 전에 해제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-148">The lease on the virtual hard disk that associates it with the VM needs to be released before you can attach the virtual hard disk to another VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-to-another-vm"></a><span data-ttu-id="d6983-149">기존 가상 하드 디스크를 다른 VM에 연결</span><span class="sxs-lookup"><span data-stu-id="d6983-149">Attach existing virtual hard disk to another VM</span></span>
<span data-ttu-id="d6983-150">다음 몇 단계에서는 문제 해결을 위해 다른 VM을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-150">For the next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="d6983-151">기존 가상 하드 디스크를 이 문제 해결 VM에 연결하여 디스크의 콘텐츠를 찾아 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-151">You attach the existing virtual hard disk to this troubleshooting VM to be able to browse and edit the disk's content.</span></span> <span data-ttu-id="d6983-152">예를 들어 이 프로세스를 사용하면 구성 오류를 수정하거나 추가 응용 프로그램 또는 시스템 로그 파일을 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-152">This process allows you to correct any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="d6983-153">다른 VM을 선택하거나 만들어 문제 해결에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-153">Choose or create another VM to use for troubleshooting purposes.</span></span>

1. <span data-ttu-id="d6983-154">포털에서 리소스 그룹을 선택하고 문제를 해결하는 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-154">Select your resource group from the portal, then select your troubleshooting VM.</span></span> <span data-ttu-id="d6983-155">**디스크**를 선택한 다음 **기존 연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-155">Select **Disks** and then click **Attach existing**:</span></span>

    ![포털에서 기존 디스크 연결](./media/troubleshoot-recovery-disks-portal/attach-existing-disk.png)

2. <span data-ttu-id="d6983-157">기존 가상 하드 디스크를 선택하려면 **VHD 파일**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-157">To select your existing virtual hard disk, click **VHD File**:</span></span>

    ![기존 VHD 찾아보기](./media/troubleshoot-recovery-disks-portal/select-vhd-location.png)

3. <span data-ttu-id="d6983-159">저장소 계정 및 컨테이너를 선택한 다음 기존 VHD를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-159">Select your storage account and container, then click your existing VHD.</span></span> <span data-ttu-id="d6983-160">**선택** 단추를 클릭하여 선택 내용을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-160">Click the **Select** button to confirm your choice:</span></span>

    ![기존 VHD 선택](./media/troubleshoot-recovery-disks-portal/select-vhd.png)

4. <span data-ttu-id="d6983-162">이제 VHD를 선택하였으므로 **확인**을 클릭하여 기존 가상 하드 디스크를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-162">With your VHD now selected, click **OK** to attach the existing virtual hard disk:</span></span>

    ![기존 가상 하드 디스크 연결 확인](./media/troubleshoot-recovery-disks-portal/attach-disk-confirm.png)

5. <span data-ttu-id="d6983-164">몇 초 후에 VM의 **디스크** 창에서는 데이터 디스크로 연결된 기존 가상 하드 디스크를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-164">After a few seconds, the **Disks** pane for your VM lists your existing virtual hard disk connected as a data disk:</span></span>

    ![데이터 디스크로 연결된 기존 가상 하드 디스크](./media/troubleshoot-recovery-disks-portal/attached-disk.png)


## <a name="mount-the-attached-data-disk"></a><span data-ttu-id="d6983-166">연결된 데이터 디스크 탑재</span><span class="sxs-lookup"><span data-stu-id="d6983-166">Mount the attached data disk</span></span>

1. <span data-ttu-id="d6983-167">VM에 대한 원격 데스크톱 연결을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-167">Open a Remote Desktop connection to your VM.</span></span> <span data-ttu-id="d6983-168">포털에서 VM을 선택하고 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-168">Select your VM in the portal and click **Connect**.</span></span> <span data-ttu-id="d6983-169">RDP 연결 파일을 다운로드하여 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-169">Download and open the RDP connection file.</span></span> <span data-ttu-id="d6983-170">다음과 같이 자격 증명을 입력하여 VM에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-170">Enter your credentials to log in to your VM as follows:</span></span>

    ![원격 데스크톱을 사용하여 VM에 로그인](./media/troubleshoot-recovery-disks-portal/open-remote-desktop.png)

2. <span data-ttu-id="d6983-172">**서버 관리자**를 연 다음 **파일 및 저장소 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-172">Open **Server Manager**, then select **File and Storage Services**.</span></span> 

    ![서버 관리자에서 파일 및 저장소 서비스 선택](./media/troubleshoot-recovery-disks-portal/server-manager-select-storage.png)

3. <span data-ttu-id="d6983-174">데이터 디스크가 자동으로 감지되고 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-174">The data disk is automatically detected and attached.</span></span> <span data-ttu-id="d6983-175">연결된 디스크 목록을 보려면 **디스크**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-175">To see a list of the connected disks, select **Disks**.</span></span> <span data-ttu-id="d6983-176">데이터 디스크를 선택하여 드라이브 문자를 포함한 볼륨 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-176">You can select your data disk to view volume information, including the drive letter.</span></span> <span data-ttu-id="d6983-177">다음 예에서는 **F:**를 사용하여 연결된 데이터 디스크를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-177">The following example shows the data disk attached and using **F:**:</span></span>

    ![서버 관리자의 연결된 디스크 및 볼륨 정보](./media/troubleshoot-recovery-disks-portal/server-manager-disk-attached.png)


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="d6983-179">원래 가상 하드 디스크의 문제 해결</span><span class="sxs-lookup"><span data-stu-id="d6983-179">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="d6983-180">기존 가상 하드 디스크가 탑재되면 이제 필요에 따라 모든 유지 관리 및 문제 해결 단계를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-180">With the existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="d6983-181">문제가 해결되면 다음 단계를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-181">Once you have addressed the issues, continue with the following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="d6983-182">원래 가상 하드 디스크의 탑재 해제 및 분리</span><span class="sxs-lookup"><span data-stu-id="d6983-182">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="d6983-183">오류가 해결되면 문제 해결 VM에서 기존 가상 하드 디스크를 분리합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-183">Once your errors are resolved, detach the existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="d6983-184">가상 하드 디스크를 문제 해결 VM에 연결하는 임대가 해제될 때까지 가상 하드 디스크를 다른 VM과 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-184">You cannot use your virtual hard disk with any other VM until the lease attaching the virtual hard disk to the troubleshooting VM is released.</span></span>

1. <span data-ttu-id="d6983-185">VM에 대한 RDP 세션에서 **서버 관리자**를 연 다음 **파일 및 저장소 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-185">From the RDP session to your VM, open **Server Manager**, then select **File and Storage Services**:</span></span>

    ![서버 관리자에서 파일 및 저장소 서비스 선택](./media/troubleshoot-recovery-disks-portal/server-manager-select-storage.png)

2. <span data-ttu-id="d6983-187">**디스크**를 선택한 다음 데이터 디스크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-187">Select **Disks** and then select your data disk.</span></span> <span data-ttu-id="d6983-188">데이터 디스크를 마우스 오른쪽 단추로 클릭하고 **오프라인 상태로 전환**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-188">Right-click on your data disk and select **Take Offline**:</span></span>

    ![서버 관리자에서 데이터 디스크를 오프라인으로 설정](./media/troubleshoot-recovery-disks-portal/server-manager-set-disk-offline.png)

3. <span data-ttu-id="d6983-190">이제 VM에서 가상 하드 디스크를 분리합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-190">Now detach the virtual hard disk from the VM.</span></span> <span data-ttu-id="d6983-191">Azure Portal에서 VM을 선택하고 **디스크**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-191">Select your VM in the Azure portal and click **Disks**.</span></span> <span data-ttu-id="d6983-192">기존 가상 하드 디스크를 선택한 다음 **분리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-192">Select your existing virtual hard disk and then click **Detach**:</span></span>

    ![기존 가상 하드 디스크 분리](./media/troubleshoot-recovery-disks-portal/detach-disk.png)

    <span data-ttu-id="d6983-194">계속하기 전에 VM이 데이터 디스크를 성공적으로 분리할 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-194">Wait until the VM has successfully detached the data disk before continuing.</span></span>

## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="d6983-195">원래 하드 디스크에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="d6983-195">Create VM from original hard disk</span></span>
<span data-ttu-id="d6983-196">원래 가상 하드 디스크에서 VM을 만들려면 [이 Azure Resource Manager 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-196">To create a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="d6983-197">템플릿은 이전 명령의 VHD URL을 사용하여 VM을 기존 가상 네트워크에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-197">The template deploys a VM into an existing virtual network, using the VHD URL from the earlier command.</span></span> <span data-ttu-id="d6983-198">다음과 같이 **Azure에 배포** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-198">Click the **Deploy to Azure** button as follows:</span></span>

![GitHub의 템플릿에서 VM 배포](./media/troubleshoot-recovery-disks-portal/deploy-template-from-github.png)

<span data-ttu-id="d6983-200">템플릿은 배포를 위해 Azure Portal에 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-200">The template is loaded into the Azure portal for deployment.</span></span> <span data-ttu-id="d6983-201">새 VM 및 기존 Azure 리소스의 이름을 입력하고 URL을 기존 가상 하드 디스크에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-201">Enter the names for your new VM and existing Azure resources, and paste the URL to your existing virtual hard disk.</span></span> <span data-ttu-id="d6983-202">배포를 시작하려면 **구매**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-202">To begin the deployment, click **Purchase**:</span></span>

![템플릿에서 VM 배포](./media/troubleshoot-recovery-disks-portal/deploy-from-image.png)


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="d6983-204">부트 진단 다시 사용</span><span class="sxs-lookup"><span data-stu-id="d6983-204">Re-enable boot diagnostics</span></span>
<span data-ttu-id="d6983-205">기존 가상 하드 디스크에서 VM을 만든 경우 부팅 진단을 자동으로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-205">When you create your VM from the existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="d6983-206">부팅 진단의 상태를 확인하고 필요한 경우 사용하려면 포털에서 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-206">To check the status of boot diagnostics and turn on if needed, select your VM in the portal.</span></span> <span data-ttu-id="d6983-207">**모니터링**에서 **진단 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-207">Under **Monitoring**, click **Diagnostics settings**.</span></span> <span data-ttu-id="d6983-208">상태가 **켜기**이고 **진단 부팅** 옆에 있는 확인 표시가 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-208">Ensure the status is **On**, and the check mark next to **Boot diagnostics** is selected.</span></span> <span data-ttu-id="d6983-209">항목을 변경하려면 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d6983-209">If you make any changes, click **Save**:</span></span>

![부팅 진단 설정 업데이트](./media/troubleshoot-recovery-disks-portal/reenable-boot-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="d6983-211">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d6983-211">Next steps</span></span>
<span data-ttu-id="d6983-212">VM에 연결하는 데 문제가 있는 경우 [Azure VM에 RDP 연결 문제 해결](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6983-212">If you are having issues connecting to your VM, see [Troubleshoot RDP connections to an Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="d6983-213">VM에서 실행 중인 응용 프로그램에 액세스하는 데 문제가 있는 경우 [Windows VM에서 응용 프로그램 연결 문제 해결](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6983-213">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Windows VM](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="d6983-214">Resource Manager를 사용하는 방법에 대한 자세한 내용은 [Azure Resource Manager 개요](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d6983-214">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>