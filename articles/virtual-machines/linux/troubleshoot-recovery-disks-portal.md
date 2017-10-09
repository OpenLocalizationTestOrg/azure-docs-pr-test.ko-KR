---
title: "Linux VM hello Azure 포털의에서 문제 해결에는 aaaUse | Microsoft Docs"
description: "Tootroubleshoot Linux 가상 컴퓨터 문제 연결 hello OS 디스크 tooa 복구 VM 사용 하 여 Azure 포털을 hello 하는 방법에 대해 알아봅니다"
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 11/14/2016
ms.author: iainfou
ms.openlocfilehash: 794daa06d7436215af84a61ab9088524254c47df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-portal"></a><span data-ttu-id="0594c-103">Linux VM hello OS 디스크 tooa 복구 VM을 연결 하 여 문제 해결 Azure 포털 hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="0594c-103">Troubleshoot a Linux VM by attaching hello OS disk tooa recovery VM using hello Azure portal</span></span>
<span data-ttu-id="0594c-104">Linux 가상 컴퓨터 (VM) 부팅 또는 디스크 오류가 발생 하는 경우 문제 해결 단계는 자체 hello 가상 하드 디스크에서 tooperform을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="0594c-105">일반적인 예로 것에 잘못 된 항목이 `/etc/fstab` hello VM 성공적으로 tooboot 수 없도록 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-105">A common example would be an invalid entry in `/etc/fstab` that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="0594c-106">이 문서에 자세히 설명 방법 toouse hello Azure 포털 tooconnect 가상 하드 디스크 tooanother Linux VM toofix 오류를 다음 다시 원래 VM를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-106">This article details how toouse hello Azure portal tooconnect your virtual hard disk tooanother Linux VM toofix any errors, then re-create your original VM.</span></span>

## <a name="recovery-process-overview"></a><span data-ttu-id="0594c-107">복구 프로세스 개요</span><span class="sxs-lookup"><span data-stu-id="0594c-107">Recovery process overview</span></span>
<span data-ttu-id="0594c-108">hello 문제 해결 과정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-108">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="0594c-109">Hello VM 발생 문제, 유지 hello 가상 하드 디스크를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-109">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="0594c-110">첨부 하 고 문제 해결을 위해 hello 가상 하드 디스크 tooanother Linux VM에 탑재 합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-110">Attach and mount hello virtual hard disk tooanother Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="0594c-111">Toohello VM 문제 해결을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-111">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="0594c-112">파일을 편집 하거나 hello 원래 가상 하드 디스크에서 다양 한 도구 toofix 문제를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-112">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="0594c-113">탑재 해제 하 고 VM의 문제를 해결 하는 hello에서 hello 가상 하드 디스크를 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-113">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="0594c-114">Hello 원래 가상 하드 디스크를 사용 하는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-114">Create a VM using hello original virtual hard disk.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="0594c-115">부팅 문제 확인</span><span class="sxs-lookup"><span data-stu-id="0594c-115">Determine boot issues</span></span>
<span data-ttu-id="0594c-116">부트 진단이 hello와 VM 스크린 샷 toodetermine VM 없는 이유 수 tooboot 올바르게 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-116">Examine hello boot diagnostics and VM screenshot toodetermine why your VM is not able tooboot correctly.</span></span> <span data-ttu-id="0594c-117">일반적인 예로는 `/etc/fstab`의 잘못된 항목 또는 삭제하거나 이동 중인 기본 가상 하드 디스크입니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-117">A common example would be an invalid entry in `/etc/fstab`, or an underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="0594c-118">Hello 포털에서 VM을 선택 하 고 다음 toohello 아래쪽으로 스크롤하여 **지원 + 문제 해결** 섹션.</span><span class="sxs-lookup"><span data-stu-id="0594c-118">Select your VM in hello portal and then scroll down toohello **Support + Troubleshooting** section.</span></span> <span data-ttu-id="0594c-119">클릭 **진단 부팅** tooview hello 콘솔 메시지 VM에서 스트리밍됩니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-119">Click **Boot diagnostics** tooview hello console messages streamed from your VM.</span></span> <span data-ttu-id="0594c-120">검토 hello 콘솔 로그 toosee 이유 hello VM은 발생 한 문제를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-120">Review hello console logs toosee if you can determine why hello VM is encountering an issue.</span></span> <span data-ttu-id="0594c-121">hello 다음 예제는 수동 조작이 필요한 유지 관리 모드에서 VM 중지.</span><span class="sxs-lookup"><span data-stu-id="0594c-121">hello following example shows a VM stuck in maintenance mode that requires manual interaction:</span></span>

![VM 부팅 진단 콘솔 로그 보기](./media/troubleshoot-recovery-disks-portal/boot-diagnostics-error.png)

<span data-ttu-id="0594c-123">클릭할 수도 있습니다 **스크린 샷** hello 부팅 진단 로그 toodownload hello VM 스크린 샷 캡처의 hello 위쪽 합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-123">You can also click **Screenshot** across hello top of hello boot diagnostics log toodownload a capture of hello VM screenshot.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="0594c-124">기존 가상 하드 디스크 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="0594c-124">View existing virtual hard disk details</span></span>
<span data-ttu-id="0594c-125">가상 하드 디스크 tooanother VM에 연결할 수 있습니다, 전에 hello 가상 하드 디스크 (VHD)의 tooidentify hello 이름이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-125">Before you can attach your virtual hard disk tooanother VM, you need tooidentify hello name of hello virtual hard disk (VHD).</span></span> 

<span data-ttu-id="0594c-126">Hello 포털에서 리소스 그룹을 선택 하 고 저장소 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-126">Select your resource group from hello portal, then select your storage account.</span></span> <span data-ttu-id="0594c-127">클릭 **Blob**와 같이, 다음 예제는 hello:</span><span class="sxs-lookup"><span data-stu-id="0594c-127">Click **Blobs**, as in hello following example:</span></span>

![저장소 Blob 선택](./media/troubleshoot-recovery-disks-portal/storage-account-overview.png)

<span data-ttu-id="0594c-129">일반적으로 가상 하드 디스크를 저장하는 **vhd**로 명명된 컨테이너가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-129">Typically you have a container named **vhds** that stores your virtual hard disks.</span></span> <span data-ttu-id="0594c-130">Hello 컨테이너 tooview 가상 하드 디스크의 목록을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-130">Select hello container tooview a list of virtual hard disks.</span></span> <span data-ttu-id="0594c-131">VHD의 참고 hello 이름 (hello 접두사는 일반적으로 hello 이름 VM의):</span><span class="sxs-lookup"><span data-stu-id="0594c-131">Note hello name of your VHD (hello prefix is usually hello name of your VM):</span></span>

![저장소 컨테이너에서 VHD 식별](./media/troubleshoot-recovery-disks-portal/storage-container.png)

<span data-ttu-id="0594c-133">Hello 목록에서 기존 가상 하드 디스크를 선택 하 고 단계를 수행 하는 hello에 사용 하기 위해 hello URL을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-133">Select your existing virtual hard disk from hello list and copy hello URL for use in hello following steps:</span></span>

![기존 가상 하드 디스크 URL 복사](./media/troubleshoot-recovery-disks-portal/copy-vhd-url.png)


## <a name="delete-existing-vm"></a><span data-ttu-id="0594c-135">기존 VM 삭제</span><span class="sxs-lookup"><span data-stu-id="0594c-135">Delete existing VM</span></span>
<span data-ttu-id="0594c-136">가상 하드 디스크와 VM은 Azure의 두 가지 별개의 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-136">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="0594c-137">가상 하드 디스크는 자체 hello 운영 체제, 응용 프로그램 및 구성 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-137">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="0594c-138">hello VM 자체 hello 크기 또는 위치를 정의 하 고 가상 하드 디스크 또는 가상 네트워크 인터페이스 카드 (NIC) 등의 리소스를 참조 하는 메타 데이터 일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-138">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="0594c-139">각 가상 하드 디스크에 연결 되어 있을 때 할당 한 임 대권을 tooa VM입니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-139">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="0594c-140">데이터 디스크를 연결 하 고 hello VM에서 실행 중인 동안에 분리 수, 있지만 hello VM 리소스는 삭제 하지 않는 한 hello OS 디스크를 분리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-140">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="0594c-141">hello 임대는 해당 VM 중지 및 할당 취소 된 상태에 있을 경우에 tooassociate hello OS 디스크는 VM으로 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-141">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="0594c-142">첫 번째 단계 toorecover hello VM은 자체 toodelete hello VM 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-142">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="0594c-143">VM 삭제 hello 저장소 계정의 hello 가상 하드 디스크를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-143">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="0594c-144">VM을 삭제 하는 hello, 후 hello 가상 하드 디스크 tooanother VM tootroubleshoot 첨부 고 hello 오류를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-144">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="0594c-145">Hello 포털에서 VM을 선택한 다음 클릭 **삭제**:</span><span class="sxs-lookup"><span data-stu-id="0594c-145">Select your VM in hello portal, then click **Delete**:</span></span>

![부팅 오류를 보여 주는 VM 부팅 진단 스크린샷](./media/troubleshoot-recovery-disks-portal/stop-delete-vm.png)

<span data-ttu-id="0594c-147">Hello VM가 hello 가상 하드 디스크 tooanother VM을 연결 하기 전에 삭제를 마치기 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-147">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="0594c-148">hello 임대 VM hello로 연결 하는 hello 가상 하드 디스크에 toobe hello 가상 하드 디스크 tooanother VM을 연결 하기 전에 해제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-148">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="0594c-149">기존 가상 하드 디스크 tooanother VM 연결</span><span class="sxs-lookup"><span data-stu-id="0594c-149">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="0594c-150">에 대 한 hello 다음 몇 단계 문제 해결을 위해 다른 VM을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-150">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="0594c-151">Hello 기존 가상 하드 디스크 toothis VM toobe 수 toobrowse 문제 해결을 첨부 하 고이 정보를 hello 디스크의 콘텐츠를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-151">You attach hello existing virtual hard disk toothis troubleshooting VM toobe able toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="0594c-152">이 프로세스 toocorrect를 통해 모든 구성 오류 또는 추가 응용 프로그램을 확인 또는 로그 파일, 예를 들어 시스템.</span><span class="sxs-lookup"><span data-stu-id="0594c-152">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="0594c-153">선택 하거나 문제 해결을 위해 다른 VM toouse 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-153">Choose or create another VM toouse for troubleshooting purposes.</span></span>

1. <span data-ttu-id="0594c-154">Hello 포털에서 리소스 그룹을 선택 하 고 문제 해결 VM을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-154">Select your resource group from hello portal, then select your troubleshooting VM.</span></span> <span data-ttu-id="0594c-155">**디스크**를 선택한 다음 **기존 연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-155">Select **Disks** and then click **Attach existing**:</span></span>

    ![Hello 포털에서 기존 디스크 연결](./media/troubleshoot-recovery-disks-portal/attach-existing-disk.png)

2. <span data-ttu-id="0594c-157">tooselect 기존 가상 하드 디스크를 클릭 **VHD 파일**:</span><span class="sxs-lookup"><span data-stu-id="0594c-157">tooselect your existing virtual hard disk, click **VHD File**:</span></span>

    ![기존 VHD 찾아보기](./media/troubleshoot-recovery-disks-portal/select-vhd-location.png)

3. <span data-ttu-id="0594c-159">저장소 계정 및 컨테이너를 선택한 다음 기존 VHD를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-159">Select your storage account and container, then click your existing VHD.</span></span> <span data-ttu-id="0594c-160">Hello 클릭 **선택** tooconfirm 선택한 단추:</span><span class="sxs-lookup"><span data-stu-id="0594c-160">Click hello **Select** button tooconfirm your choice:</span></span>

    ![기존 VHD 선택](./media/troubleshoot-recovery-disks-portal/select-vhd.png)

4. <span data-ttu-id="0594c-162">이제 선택한 VHD를 클릭 **확인** tooattach hello 기존 가상 하드 디스크:</span><span class="sxs-lookup"><span data-stu-id="0594c-162">With your VHD now selected, click **OK** tooattach hello existing virtual hard disk:</span></span>

    ![기존 가상 하드 디스크 연결 확인](./media/troubleshoot-recovery-disks-portal/attach-disk-confirm.png)

5. <span data-ttu-id="0594c-164">몇 초 후 hello **디스크** VM에 대 한 창에 데이터 디스크로 연결 된 기존 가상 하드 디스크를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-164">After a few seconds, hello **Disks** pane for your VM lists your existing virtual hard disk connected as a data disk:</span></span>

    ![데이터 디스크로 연결된 기존 가상 하드 디스크](./media/troubleshoot-recovery-disks-portal/attached-disk.png)


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="0594c-166">Hello 연결 된 데이터 디스크를 탑재</span><span class="sxs-lookup"><span data-stu-id="0594c-166">Mount hello attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="0594c-167">hello 다음 예에서는 Ubuntu VM에서 필요한 hello 단계.</span><span class="sxs-lookup"><span data-stu-id="0594c-167">hello following examples detail hello steps required on an Ubuntu VM.</span></span> <span data-ttu-id="0594c-168">Red Hat Enterprise Linux, SUSE 등 다른 Linux 배포판을 사용 하는 경우 로그 파일 위치 hello 및 `mount` 명령을 약간 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-168">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, hello log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="0594c-169">명령에 적절 한 변경 내용 hello에 대 한 특정 프로그램 distro toohello 설명서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="0594c-169">Refer toohello documentation for your specific distro for hello appropriate changes in commands.</span></span>

1. <span data-ttu-id="0594c-170">SSH tooyour hello 적절 한 자격 증명을 사용 하 여 VM의 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-170">SSH tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="0594c-171">이 디스크는 hello 첫 번째 데이터 연결 된 디스크 tooyour VM 문제 해결, 면 가능성이 연결 되 너무`/dev/sdc`합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-171">If this disk is hello first data disk attached tooyour troubleshooting VM, it is likely connected too`/dev/sdc`.</span></span> <span data-ttu-id="0594c-172">사용 하 여 `dmseg` toolist 연결 된 디스크:</span><span class="sxs-lookup"><span data-stu-id="0594c-172">Use `dmseg` toolist attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```
    <span data-ttu-id="0594c-173">hello 비슷한 toohello 다음은 예제 출력:</span><span class="sxs-lookup"><span data-stu-id="0594c-173">hello output is similar toohello following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="0594c-174">앞 예제는 hello, hello OS 디스크에는 `/dev/sda` 및 hello 임시 디스크에는 각 VM에 대해 제공 된 `/dev/sdb`합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-174">In hello preceding example, hello OS disk is at `/dev/sda` and hello temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="0594c-175">여러 데이터 디스크가 있는 경우 `/dev/sdd`, `/dev/sde` 등에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-175">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="0594c-176">디렉터리 toomount 기존 가상 하드 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-176">Create a directory toomount your existing virtual hard disk.</span></span> <span data-ttu-id="0594c-177">hello 다음 예에서는 라는 디렉터리를 만듭니다 `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="0594c-177">hello following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="0594c-178">기존 가상 하드 디스크에 파티션이 여러 개 있으면 필요한 hello 파티션을 탑재 합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-178">If you have multiple partitions on your existing virtual hard disk, mount hello required partition.</span></span> <span data-ttu-id="0594c-179">hello 다음 예제에서는 탑재 hello에서 첫 번째 주 파티션 `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="0594c-179">hello following example mounts hello first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="0594c-180">사용 하 여 Azure에서 Vm에 데이터 디스크 toomount hello hello 가상 하드 디스크의 범용 고유 식별자 (UUID) 하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-180">Best practice is toomount data disks on VMs in Azure using hello universally unique identifier (UUID) of hello virtual hard disk.</span></span> <span data-ttu-id="0594c-181">이 짧은 문제 해결 시나리오에 대 한 탑재 hello 가상 하드 디스크 UUID hello를 사용 하 여 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-181">For this short troubleshooting scenario, mounting hello virtual hard disk using hello UUID is not necessary.</span></span> <span data-ttu-id="0594c-182">그러나 일반적인 사용에서 편집 `/etc/fstab` toomount 가상 하드 디스크 UUID 않을 대신 장치 이름을 사용 하 여 VM toofail tooboot hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-182">However, under normal use, editing `/etc/fstab` toomount virtual hard disks using device name rather than UUID may cause hello VM toofail tooboot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="0594c-183">원래 가상 하드 디스크의 문제 해결</span><span class="sxs-lookup"><span data-stu-id="0594c-183">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="0594c-184">이제 hello 기존 가상 하드 디스크를 탑재, 모든 유지 관리 및 문제 해결 단계는 필요에 따라 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-184">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="0594c-185">Hello 문제를 해결 한 후 단계를 수행 하는 hello로 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-185">Once you have addressed hello issues, continue with hello following steps.</span></span>

## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="0594c-186">원래 가상 하드 디스크의 탑재 해제 및 분리</span><span class="sxs-lookup"><span data-stu-id="0594c-186">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="0594c-187">프로그램 오류가 해결 되 면 hello 기존 가상 하드 디스크 문제 해결 VM에서 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-187">Once your errors are resolved, detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="0594c-188">VM의 문제를 해결 하는 hello 가상 하드 디스크 toohello 연결 hello 임대가 해제 될 때까지 다른 VM과 가상 하드 디스크를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-188">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="0594c-189">Hello SSH 세션 tooyour VM 문제 해결에서 hello 기존 가상 하드 디스크를 분리 하십시오.</span><span class="sxs-lookup"><span data-stu-id="0594c-189">From hello SSH session tooyour troubleshooting VM, unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="0594c-190">먼저 탑재 지점에 대 한 부모 디렉터리 hello 밖으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-190">Change out of hello parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="0594c-191">이제 hello 기존 가상 하드 디스크를 탑재 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-191">Now unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="0594c-192">hello 다음 예제에서는 분리 hello 해당 장치 `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="0594c-192">hello following example unmounts hello device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="0594c-193">이제 hello hello VM에서에서 가상 하드 디스크를 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-193">Now detach hello virtual hard disk from hello VM.</span></span> <span data-ttu-id="0594c-194">Hello 포털에서 VM을 선택 하 고 클릭 **디스크**합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-194">Select your VM in hello portal and click **Disks**.</span></span> <span data-ttu-id="0594c-195">기존 가상 하드 디스크를 선택한 다음 **분리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-195">Select your existing virtual hard disk and then click **Detach**:</span></span>

    ![기존 가상 하드 디스크 분리](./media/troubleshoot-recovery-disks-portal/detach-disk.png)

    <span data-ttu-id="0594c-197">계속 하기 전에 VM hello hello 데이터 디스크를 성공적으로 분리 된 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-197">Wait until hello VM has successfully detached hello data disk before continuing.</span></span>

## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="0594c-198">원래 하드 디스크에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="0594c-198">Create VM from original hard disk</span></span>
<span data-ttu-id="0594c-199">원래 가상 하드 디스크에서 VM에서 사용할 toocreate [이 Azure 리소스 관리자 템플릿을](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet)합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-199">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="0594c-200">hello에서 VHD URL hello를 사용 하 여 기존 가상 네트워크를으로 VM을 배포 하는 hello 템플릿 이전 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-200">hello template deploys a VM into an existing virtual network, using hello VHD URL from hello earlier command.</span></span> <span data-ttu-id="0594c-201">Hello 클릭 **tooAzure 배포** 다음과 같이 단추:</span><span class="sxs-lookup"><span data-stu-id="0594c-201">Click hello **Deploy tooAzure** button as follows:</span></span>

![GitHub의 템플릿에서 VM 배포](./media/troubleshoot-recovery-disks-portal/deploy-template-from-github.png)

<span data-ttu-id="0594c-203">hello 템플릿 배포에 대 한 Azure 포털 hello에 로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-203">hello template is loaded into hello Azure portal for deployment.</span></span> <span data-ttu-id="0594c-204">새 VM 및 기존 Azure 리소스에 대 한 hello 이름을 입력 하 고 hello URL tooyour 기존 가상 하드 디스크를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-204">Enter hello names for your new VM and existing Azure resources, and paste hello URL tooyour existing virtual hard disk.</span></span> <span data-ttu-id="0594c-205">toobegin hello 배포 클릭 **구매**:</span><span class="sxs-lookup"><span data-stu-id="0594c-205">toobegin hello deployment, click **Purchase**:</span></span>

![템플릿에서 VM 배포](./media/troubleshoot-recovery-disks-portal/deploy-from-image.png)


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="0594c-207">부트 진단 다시 사용</span><span class="sxs-lookup"><span data-stu-id="0594c-207">Re-enable boot diagnostics</span></span>
<span data-ttu-id="0594c-208">Hello 기존 가상 하드 디스크에서 VM을 만들 때 부트 진단이 자동으로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-208">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="0594c-209">toocheck 부트 진단의 상태를 hello 및 hello 포털에서 VM을 선택 합니다. 필요한 경우 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-209">toocheck hello status of boot diagnostics and turn on if needed, select your VM in hello portal.</span></span> <span data-ttu-id="0594c-210">**모니터링**에서 **진단 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-210">Under **Monitoring**, click **Diagnostics settings**.</span></span> <span data-ttu-id="0594c-211">Hello 상태는 확인 **에**, 너무 확인 표시를 다음 hello 및**진단 부팅** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-211">Ensure hello status is **On**, and hello check mark next too**Boot diagnostics** is selected.</span></span> <span data-ttu-id="0594c-212">항목을 변경하려면 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-212">If you make any changes, click **Save**:</span></span>

![부팅 진단 설정 업데이트](./media/troubleshoot-recovery-disks-portal/reenable-boot-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="0594c-214">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0594c-214">Next steps</span></span>
<span data-ttu-id="0594c-215">Tooyour VM을 연결 하는 데 문제가 있는 경우 참조 [해결 SSH 연결 tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="0594c-215">If you are having issues connecting tooyour VM, see [Troubleshoot SSH connections tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="0594c-216">VM에서 실행 중인 응용 프로그램에 액세스하는 데 문제가 있는 경우 [Linux VM에서 응용 프로그램 연결 문제 해결](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0594c-216">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="0594c-217">Resource Manager를 사용하는 방법에 대한 자세한 내용은 [Azure Resource Manager 개요](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0594c-217">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
